.. _chapter_PPP:

Examples of Communication of Display Parameters (Informative)
=============================================================

.. _sect_PPP.1:

The Relationship Between AE and Display System
----------------------------------------------

The Display System SCU and the Display System SCP are peer DICOM
Communication of Display Parameters management application entities. The
application entity of the Display System SCP supports one or more
display subsystems.

Display System SCU and the SCP establish an association by using the
association services of the OSI upper layer service.

While the association is being established, each of application entity
negotiates the supported SOP classes.

.. _sect_PPP.2:

Examples of Message Sequencing
------------------------------

This section provides an examples of message sequencing when using the
Display System SOP Class. This section is not intended to provide an
exhaustive set of use cases but rather an informative example. There are
other valid message sequences that could be used to obtain an equivalent
outcome.

.. _sect_PPP.2.1:

Example of Retrieval of Status and Configuration From Display Systems
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

**QC Management Station**: Manages display systems status and
Configurations. This works as an SCU.

**Display System A and B**: Have display devices. Each display device
may be other display vendors'. These work as SCPs.

Generation and notification of change events are out of a scope of
DICOM.

.. _sect_PPP.3:

Examples of Display System SOP Class
------------------------------------

.. _sect_PPP.3.1:

An Example of A Typical Display System
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

A typical Display System is shown in
`figure_title <#figure_PPP.3.1-1>`__.

The following is an example of an N-GET Request/Response pair for the
Display System SOP Class.

This example is encoded with Undefined Sequence Length and Undefined
Item Length, so it contains Sequence Delimitation Items and Item
Delimitation Items.

ANP
   Attribute Not Present.

VNP
   Attribute Present but Value Not Present.

-
   Not specified.

.. table:: N-GET Request/Response Example

   +-----------------+-------------+-----------------+-----------------+
   | Attribute Name  | Tag         | N-GET Request   | N-GET Response  |
   |                 |             | (SCU)           | (SCP)           |
   +=================+=============+=================+=================+
   | **SOP Common    |             |                 |                 |
   | and Workstation |             |                 |                 |
   | Modules**       |             |                 |                 |
   +-----------------+-------------+-----------------+-----------------+
   | Specific        | (0008,0005) | ANP             | \\ISO 2022 IR   |
   | Character Set   |             |                 | 87              |
   +-----------------+-------------+-----------------+-----------------+
   | Manufacturer    | (0008,0070) | VNP             | NIPPON          |
   |                 |             |                 | Corporation     |
   +-----------------+-------------+-----------------+-----------------+
   | Institution     | (0008,0080) | VNP             | JIRA Hospital   |
   | Name            |             |                 |                 |
   +-----------------+-------------+-----------------+-----------------+
   | Institution     | (0008,0081) | VNP             | Bunkyo-ku,      |
   | Address         |             |                 | Tokyo, Japan    |
   +-----------------+-------------+-----------------+-----------------+
   | Device Serial   | (0018,1000) | VNP             | SN1234567890    |
   | Number          |             |                 |                 |
   +-----------------+-------------+-----------------+-----------------+
   | Station Name    | (0008,1010) | VNP             | WorkstationX    |
   +-----------------+-------------+-----------------+-----------------+
   | Institutional   | (0008,1040) | VNP             | Radiology Dept. |
   | Department Name |             |                 |                 |
   +-----------------+-------------+-----------------+-----------------+
   | Manufacturer's  | (0008,1090) | VNP             | QASt            |
   | Model Name      |             |                 | ation-Model2013 |
   +-----------------+-------------+-----------------+-----------------+
   | Equipment       | (0028,7000) | VNP             |                 |
   | Administrator   |             |                 |                 |
   | Sequence        |             |                 |                 |
   +-----------------+-------------+-----------------+-----------------+
   | >Item #1 of     | (FFFE,E000) | -               |                 |
   | Equipment       |             |                 |                 |
   | Administrator   |             |                 |                 |
   | Sequence        |             |                 |                 |
   +-----------------+-------------+-----------------+-----------------+
   | >Person Name    | (0040,A123) | -               | Yamada^         |
   |                 |             |                 | Tarou=山田^太郎 |
   |                 |             |                 | =やまだ^たろう  |
   +-----------------+-------------+-----------------+-----------------+
   | >Person         | (0040,1101) | -               |                 |
   | Identification  |             |                 |                 |
   | Code Sequence   |             |                 |                 |
   +-----------------+-------------+-----------------+-----------------+
   | >>Item #1 of    | (FFFE,E000) | -               |                 |
   | Person          |             |                 |                 |
   | Identification  |             |                 |                 |
   | Code Sequence   |             |                 |                 |
   +-----------------+-------------+-----------------+-----------------+
   | >>Code Value    | (0008,0110) | -               | 111111          |
   +-----------------+-------------+-----------------+-----------------+
   | >>Coding Scheme | (0008,0102) | -               | LOCAL           |
   | Designator      |             |                 |                 |
   +-----------------+-------------+-----------------+-----------------+
   | >>Code Meaning  | (0008,0104) | -               | Yamada^Tarou    |
   +-----------------+-------------+-----------------+-----------------+
   | >>Item          | (FFFE,E00D) | -               |                 |
   | Delimiter of    |             |                 |                 |
   | Item #1 of      |             |                 |                 |
   | Person          |             |                 |                 |
   | Identification  |             |                 |                 |
   | Code Sequence   |             |                 |                 |
   +-----------------+-------------+-----------------+-----------------+
   | >>Sequence      | (FFFE,E0DD) | -               |                 |
   | Delimiter of    |             |                 |                 |
   | Person          |             |                 |                 |
   | Identification  |             |                 |                 |
   | Code Sequence   |             |                 |                 |
   +-----------------+-------------+-----------------+-----------------+
   | >Person's       | (0040,1102) | -               |                 |
   | Address         |             |                 |                 |
   +-----------------+-------------+-----------------+-----------------+
   | >Person's       | (0040,1103) | -               | EXT. 1234       |
   | Telephone       |             |                 |                 |
   | Number          |             |                 |                 |
   +-----------------+-------------+-----------------+-----------------+
   | >Institution    | (0008,0080) | -               | IT Support Div. |
   | Name            |             |                 |                 |
   +-----------------+-------------+-----------------+-----------------+
   | >Item Delimiter | (FFFE,E00D) | -               |                 |
   | of Item #1 of   |             |                 |                 |
   | Equipment       |             |                 |                 |
   | Administrator   |             |                 |                 |
   | Sequence        |             |                 |                 |
   +-----------------+-------------+-----------------+-----------------+
   | >Sequence       | (FFFE,E0DD) | -               |                 |
   | Delimiter of    |             |                 |                 |
   | Equipment       |             |                 |                 |
   | Administrator   |             |                 |                 |
   | Sequence        |             |                 |                 |
   +-----------------+-------------+-----------------+-----------------+
   | **Display       |             |                 |                 |
   | System Module** |             |                 |                 |
   +-----------------+-------------+-----------------+-----------------+
   | Number of       | (0028,7001) |                 | 3               |
   | Display         |             |                 |                 |
   | Subsystems      |             |                 |                 |
   +-----------------+-------------+-----------------+-----------------+
   | Display         | (0028,7023) | VNP             |                 |
   | Subsystem       |             |                 |                 |
   | Sequence        |             |                 |                 |
   +-----------------+-------------+-----------------+-----------------+
   | Item #1 of      | (FFFE,E000) | -               |                 |
   | Display         |             |                 |                 |
   | Subsystem       |             |                 |                 |
   | Sequence        |             |                 |                 |
   +-----------------+-------------+-----------------+-----------------+
   | >Display        | (0028,7003) | -               | 1               |
   | Subsystem ID    |             |                 |                 |
   +-----------------+-------------+-----------------+-----------------+
   | >Display        | (0028,7004) | -               | DSS1ofWSX       |
   | Subsystem Name  |             |                 |                 |
   +-----------------+-------------+-----------------+-----------------+
   | >Display        | (0028,7005) | -               | For viewing a   |
   | Subsystem       |             |                 | list and        |
   | Description     |             |                 | reports         |
   +-----------------+-------------+-----------------+-----------------+
   | >Display Device | (0028,7022) | -               |                 |
   | Type Code       |             |                 |                 |
   | Sequence        |             |                 |                 |
   +-----------------+-------------+-----------------+-----------------+
   | >>Item #1 of    | (FFFE,E000) | -               |                 |
   | Display Device  |             |                 |                 |
   | Type Code       |             |                 |                 |
   | Sequence        |             |                 |                 |
   +-----------------+-------------+-----------------+-----------------+
   | >>Code Value    | (0008,0100) | -               | 109992          |
   +-----------------+-------------+-----------------+-----------------+
   | >>Coding Scheme | (0008,0102) | -               | DCM             |
   | Designator      |             |                 |                 |
   +-----------------+-------------+-----------------+-----------------+
   | >>Code Meaning  | (0008,0104) | -               | Liquid Crystal  |
   |                 |             |                 | Display         |
   +-----------------+-------------+-----------------+-----------------+
   | >>Item          | (FFFE,E00D) | -               |                 |
   | Delimiter of    |             |                 |                 |
   | Item #1 of      |             |                 |                 |
   | Display Device  |             |                 |                 |
   | Type Code       |             |                 |                 |
   | Sequence        |             |                 |                 |
   +-----------------+-------------+-----------------+-----------------+
   | >>Sequence      | (FFFE,E0DD) | -               |                 |
   | Delimiter of    |             |                 |                 |
   | Display Device  |             |                 |                 |
   | Type Code       |             |                 |                 |
   | Sequence        |             |                 |                 |
   +-----------------+-------------+-----------------+-----------------+
   | >Manufacturer   | (0008,0070) | -               | Color Monitor   |
   |                 |             |                 | Corp.           |
   +-----------------+-------------+-----------------+-----------------+
   | >Device Serial  | (0018,1000) | -               | C201300011      |
   | Number          |             |                 |                 |
   +-----------------+-------------+-----------------+-----------------+
   | >Manufacturer's | (0008,1090) | -               | 1MC             |
   | Model Name      |             |                 |                 |
   +-----------------+-------------+-----------------+-----------------+
   | > System Status | (0028,7006) | -               | NORMAL          |
   +-----------------+-------------+-----------------+-----------------+
   | > System Status | (0028,7007) | -               |                 |
   | Comment         |             |                 |                 |
   +-----------------+-------------+-----------------+-----------------+
   | >Display        | (0028,700A) | -               |                 |
   | Subsystem       |             |                 |                 |
   | Configuration   |             |                 |                 |
   | Sequence        |             |                 |                 |
   +-----------------+-------------+-----------------+-----------------+
   | >>Item #1 of    | (FFFE,E000) | -               |                 |
   | Display         |             |                 |                 |
   | Subsystem       |             |                 |                 |
   | Configuration   |             |                 |                 |
   | Sequence        |             |                 |                 |
   +-----------------+-------------+-----------------+-----------------+
   | >>              | (0028,700B) | -               | 1               |
   | Configuration   |             |                 |                 |
   | ID              |             |                 |                 |
   +-----------------+-------------+-----------------+-----------------+
   | >>              | (0028,700C) | -               | DSS1Config1     |
   | Configuration   |             |                 |                 |
   | Name            |             |                 |                 |
   +-----------------+-------------+-----------------+-----------------+
   | >>              | (0028,700D) | -               | Configuration1  |
   | Configuration   |             |                 | of Display      |
   | Description     |             |                 | Subsystem ID1   |
   +-----------------+-------------+-----------------+-----------------+
   | >>Referenced    | (0028,700E) | -               | 1               |
   | Target          |             |                 |                 |
   | Luminance       |             |                 |                 |
   | Characteristics |             |                 |                 |
   | ID              |             |                 |                 |
   +-----------------+-------------+-----------------+-----------------+
   | >>Item          | (FFFE,E00D) | -               |                 |
   | Delimiter of    |             |                 |                 |
   | Item #1 of      |             |                 |                 |
   | Display         |             |                 |                 |
   | Subsystem       |             |                 |                 |
   | Configuration   |             |                 |                 |
   | Sequence        |             |                 |                 |
   +-----------------+-------------+-----------------+-----------------+
   | >>Sequence      | (FFFE,E0DD) | -               |                 |
   | Delimiter of    |             |                 |                 |
   | Display         |             |                 |                 |
   | Subsystem       |             |                 |                 |
   | Configuration   |             |                 |                 |
   | Sequence        |             |                 |                 |
   +-----------------+-------------+-----------------+-----------------+
   | >Current        | (0028,7002) | -               | 1               |
   | Configuration   |             |                 |                 |
   | ID              |             |                 |                 |
   +-----------------+-------------+-----------------+-----------------+
   | >Measurement    | (0028,7012) | -               |                 |
   | Equipment       |             |                 |                 |
   | Sequence        |             |                 |                 |
   +-----------------+-------------+-----------------+-----------------+
   | >Sequence       | (FFFE,E0DD) | -               |                 |
   | Delimiter of    |             |                 |                 |
   | Measurement     |             |                 |                 |
   | Equipment       |             |                 |                 |
   | Sequence        |             |                 |                 |
   +-----------------+-------------+-----------------+-----------------+
   | >Item Delimiter | (FFFE,E00D) | -               |                 |
   | of Item #1 of   |             |                 |                 |
   | Display System  |             |                 |                 |
   | Sequence        |             |                 |                 |
   +-----------------+-------------+-----------------+-----------------+
   | >Item #2 of     | (FFFE,E000) | -               |                 |
   | Display         |             |                 |                 |
   | Subsystem       |             |                 |                 |
   | Sequence        |             |                 |                 |
   +-----------------+-------------+-----------------+-----------------+
   | >Display        | (0028,7003) | -               | 2               |
   | Subsystem ID    |             |                 |                 |
   +-----------------+-------------+-----------------+-----------------+
   | >Display        | (0028,7004) | -               | DSS2ofWSX       |
   | Subsystem Name  |             |                 |                 |
   +-----------------+-------------+-----------------+-----------------+
   | >Display        | (0028,7005) | -               | Diagnostic,     |
   | Subsystem       |             |                 | Monochrome      |
   | Description     |             |                 |                 |
   +-----------------+-------------+-----------------+-----------------+
   | >Display Device | (0028,7022) | -               |                 |
   | Type Code       |             |                 |                 |
   | Sequence        |             |                 |                 |
   +-----------------+-------------+-----------------+-----------------+
   | >>Item #1 of    | (FFFE,E00D) | -               |                 |
   | Display Device  |             |                 |                 |
   | Type Code       |             |                 |                 |
   | Sequence        |             |                 |                 |
   +-----------------+-------------+-----------------+-----------------+
   | >>Code Value    | (0008,0100) | -               | 109992          |
   +-----------------+-------------+-----------------+-----------------+
   | >>Coding Scheme | (0008,0102) | -               | DCM             |
   | Designator      |             |                 |                 |
   +-----------------+-------------+-----------------+-----------------+
   | >>Code Meaning  | (0008,0104) | -               | Liquid Crystal  |
   |                 |             |                 | Display         |
   +-----------------+-------------+-----------------+-----------------+
   | >>Item          | (FFFE,E00D) | -               |                 |
   | Delimiter of    |             |                 |                 |
   | Display Device  |             |                 |                 |
   | Type Code       |             |                 |                 |
   | Sequence        |             |                 |                 |
   +-----------------+-------------+-----------------+-----------------+
   | >>Sequence      | (FFFE,E0DD) | -               |                 |
   | Delimiter of    |             |                 |                 |
   | Display Device  |             |                 |                 |
   | Type Code       |             |                 |                 |
   | Sequence        |             |                 |                 |
   +-----------------+-------------+-----------------+-----------------+
   | >Manufacturer   | (0008,0070) | -               | Medical Display |
   |                 |             |                 | Corp.           |
   +-----------------+-------------+-----------------+-----------------+
   | >Device Serial  | (0018,1000) | -               | 3M123456789     |
   | Number          |             |                 |                 |
   +-----------------+-------------+-----------------+-----------------+
   | >Manufacturer's | (0008,1090) | -               | 3MG             |
   | Model Name      |             |                 |                 |
   +-----------------+-------------+-----------------+-----------------+
   | > System Status | (0028,7006) | -               | NORMAL          |
   +-----------------+-------------+-----------------+-----------------+
   | > System Status | (0028,7007) | -               |                 |
   | Comment         |             |                 |                 |
   +-----------------+-------------+-----------------+-----------------+
   | >Display        | (0028,700A) | -               |                 |
   | Subsystem       |             |                 |                 |
   | Configuration   |             |                 |                 |
   | Sequence        |             |                 |                 |
   +-----------------+-------------+-----------------+-----------------+
   | >>Item #1 of    | (FFFE,E000) | -               |                 |
   | Display         |             |                 |                 |
   | Subsystem       |             |                 |                 |
   | Configuration   |             |                 |                 |
   | Sequence        |             |                 |                 |
   +-----------------+-------------+-----------------+-----------------+
   | >>Configuration | (0028,700B) | -               | 1               |
   | ID              |             |                 |                 |
   +-----------------+-------------+-----------------+-----------------+
   | >>              | (0028,700C) | -               | DSS2Config1     |
   | Configuration   |             |                 |                 |
   | Name            |             |                 |                 |
   +-----------------+-------------+-----------------+-----------------+
   | >>              | (0028,700D) | -               | Configuration2  |
   | Configuration   |             |                 | of Display      |
   | Description     |             |                 | Subsystem ID2   |
   +-----------------+-------------+-----------------+-----------------+
   | >>Referenced    | (0028,700E) | -               | 2               |
   | Target          |             |                 |                 |
   | Luminance       |             |                 |                 |
   | Characteristics |             |                 |                 |
   | ID              |             |                 |                 |
   +-----------------+-------------+-----------------+-----------------+
   | >>Item #1 of    | (FFFE,E00D) | -               |                 |
   | Display         |             |                 |                 |
   | Subsystem       |             |                 |                 |
   | Configuration   |             |                 |                 |
   | Sequence        |             |                 |                 |
   +-----------------+-------------+-----------------+-----------------+
   | >>Sequence      | (FFFE,E0DD) | -               |                 |
   | Delimiter of    |             |                 |                 |
   | Display         |             |                 |                 |
   | Subsystem       |             |                 |                 |
   | Configuration   |             |                 |                 |
   | Sequence        |             |                 |                 |
   +-----------------+-------------+-----------------+-----------------+
   | >Current        | (0028,7002) | -               | 1               |
   | Configuration   |             |                 |                 |
   | ID              |             |                 |                 |
   +-----------------+-------------+-----------------+-----------------+
   | >Measurement    | (0028,7012) | -               |                 |
   | Equipment       |             |                 |                 |
   | Sequence        |             |                 |                 |
   +-----------------+-------------+-----------------+-----------------+
   | >>Item #1 of    | (FFFE,E000) | -               |                 |
   | Measurement     |             |                 |                 |
   | Equipment       |             |                 |                 |
   | Sequence        |             |                 |                 |
   +-----------------+-------------+-----------------+-----------------+
   | >>Measurement   | (0028,7013) | -               | PHOTOME         |
   | Functions       |             |                 | TER\COLORIMETER |
   +-----------------+-------------+-----------------+-----------------+
   | >>Measured      | (0028,7026) | -               | UNI             |
   | Characteristics |             |                 | FORMITY\LUMINAN |
   |                 |             |                 | CE\CHROMATICITY |
   +-----------------+-------------+-----------------+-----------------+
   | >>Measurement   | (0028,7014) | -               | BUILT_IN_FRONT  |
   | Equipment Type  |             |                 |                 |
   +-----------------+-------------+-----------------+-----------------+
   | >> Manufacturer | (0008,0070) | -               | Lumin           |
   |                 |             |                 | anceMeasurement |
   |                 |             |                 | Device Inc.     |
   +-----------------+-------------+-----------------+-----------------+
   | >>              | (0008,1090) | -               | LC1000          |
   | Manufacturer's  |             |                 |                 |
   | Model Name      |             |                 |                 |
   +-----------------+-------------+-----------------+-----------------+
   | >> Device       | (0018,1000) | -               | SN99990001      |
   | Serial Number   |             |                 |                 |
   +-----------------+-------------+-----------------+-----------------+
   | >> DateTime of  | (0018,1202) | -               |                 |
   | Last            |             |                 |                 |
   | Calibration     |             |                 |                 |
   +-----------------+-------------+-----------------+-----------------+
   | >>Item          | (FFFE,E00D) | -               |                 |
   | Delimiter of    |             |                 |                 |
   | Item #1 of      |             |                 |                 |
   | Measurement     |             |                 |                 |
   | Equipment       |             |                 |                 |
   | Sequence        |             |                 |                 |
   +-----------------+-------------+-----------------+-----------------+
   | >>Sequence      | (FFFE,E0DD) | -               |                 |
   | Delimiter of    |             |                 |                 |
   | Measurement     |             |                 |                 |
   | Equipment       |             |                 |                 |
   | Sequence        |             |                 |                 |
   +-----------------+-------------+-----------------+-----------------+
   | >Item Delimiter | (FFFE,E00D) | -               |                 |
   | of Item #2 of   |             |                 |                 |
   | Display         |             |                 |                 |
   | Subsystem       |             |                 |                 |
   | Sequence        |             |                 |                 |
   +-----------------+-------------+-----------------+-----------------+
   | >Item #3 of     | (FFFE,E000) | -               |                 |
   | Display         |             |                 |                 |
   | Subsystem       |             |                 |                 |
   | Sequence        |             |                 |                 |
   +-----------------+-------------+-----------------+-----------------+
   | >Display        | (0028,7003) | -               | 3               |
   | Subsystem ID    |             |                 |                 |
   +-----------------+-------------+-----------------+-----------------+
   | >Display        | (0028,7004) | -               | DSS3ofWSX       |
   | Subsystem Name  |             |                 |                 |
   +-----------------+-------------+-----------------+-----------------+
   | >Display        | (0028,7005) | -               | Diagnostic,     |
   | Subsystem       |             |                 | Monochrome      |
   | Description     |             |                 |                 |
   +-----------------+-------------+-----------------+-----------------+
   | >Display Device | (0028,7022) | -               |                 |
   | Type Code       |             |                 |                 |
   | Sequence        |             |                 |                 |
   +-----------------+-------------+-----------------+-----------------+
   | >>Item #1 of    | (FFFE,E000) | -               |                 |
   | Display Device  |             |                 |                 |
   | Type Code       |             |                 |                 |
   | Sequence        |             |                 |                 |
   +-----------------+-------------+-----------------+-----------------+
   | >>Code Value    | (0008,0100) | -               | 109992          |
   +-----------------+-------------+-----------------+-----------------+
   | >>Coding Scheme | (0008,0102) | -               | DCM             |
   | Designator      |             |                 |                 |
   +-----------------+-------------+-----------------+-----------------+
   | >>Code Meaning  | (0008,0104) | -               | Liquid Crystal  |
   |                 |             |                 | Display         |
   +-----------------+-------------+-----------------+-----------------+
   | >>Item          | (FFFE,E00D) | -               |                 |
   | Delimiter of    |             |                 |                 |
   | Item #1 of      |             |                 |                 |
   | Display Device  |             |                 |                 |
   | Type Code       |             |                 |                 |
   | Sequence        |             |                 |                 |
   +-----------------+-------------+-----------------+-----------------+
   | >>Sequence      | (FFFE,E0DD) | -               |                 |
   | Delimiter of    |             |                 |                 |
   | Display Device  |             |                 |                 |
   | Type Code       |             |                 |                 |
   | Sequence        |             |                 |                 |
   +-----------------+-------------+-----------------+-----------------+
   | >Manufacturer   | (0008,0070) | -               | Medical Display |
   |                 |             |                 | Corp.           |
   +-----------------+-------------+-----------------+-----------------+
   | >Device Serial  | (0018,1000) | -               | 3M123456790     |
   | Number          |             |                 |                 |
   +-----------------+-------------+-----------------+-----------------+
   | >Manufacturer's | (0008,1090) | -               | 3MG             |
   | Model Name      |             |                 |                 |
   +-----------------+-------------+-----------------+-----------------+
   | >System Status  | (0028,7006) | -               | NORMAL          |
   +-----------------+-------------+-----------------+-----------------+
   | >System Status  | (0028,7007) | -               |                 |
   | Comment         |             |                 |                 |
   +-----------------+-------------+-----------------+-----------------+
   | > Display       | (0028,700A) | -               |                 |
   | Subsystem       |             |                 |                 |
   | Configuration   |             |                 |                 |
   | Sequence        |             |                 |                 |
   +-----------------+-------------+-----------------+-----------------+
   | >>Item #1 of    | (FFFE,E000) | -               |                 |
   | Display         |             |                 |                 |
   | Subsystem       |             |                 |                 |
   | Configuration   |             |                 |                 |
   | Sequence        |             |                 |                 |
   +-----------------+-------------+-----------------+-----------------+
   | >>              | (0028,700B) | -               | 1               |
   | Configuration   |             |                 |                 |
   | ID              |             |                 |                 |
   +-----------------+-------------+-----------------+-----------------+
   | >>              | (0028,700C) | -               | DSS3Config1     |
   | Configuration   |             |                 |                 |
   | Name            |             |                 |                 |
   +-----------------+-------------+-----------------+-----------------+
   | >>              | (0028,700D) | -               | Configuration3  |
   | Configuration   |             |                 | of Display      |
   | Description     |             |                 | Subsystem ID3   |
   +-----------------+-------------+-----------------+-----------------+
   | >>Referenced    | (0028,700E) | -               | 3               |
   | Target          |             |                 |                 |
   | Luminance       |             |                 |                 |
   | Characteristics |             |                 |                 |
   | ID              |             |                 |                 |
   +-----------------+-------------+-----------------+-----------------+
   | >>Item          | (FFFE,E00D) | -               |                 |
   | Delimiter of    |             |                 |                 |
   | Item #1 of      |             |                 |                 |
   | Display         |             |                 |                 |
   | Subsystem       |             |                 |                 |
   | Configuration   |             |                 |                 |
   | Sequence        |             |                 |                 |
   +-----------------+-------------+-----------------+-----------------+
   | >>Sequence      | (FFFE,E0DD) | -               |                 |
   | Delimiter of    |             |                 |                 |
   | Display         |             |                 |                 |
   | Subsystem       |             |                 |                 |
   | Configuration   |             |                 |                 |
   | Sequence        |             |                 |                 |
   +-----------------+-------------+-----------------+-----------------+
   | >Current        | (0028,7002) | -               | 1               |
   | Configuration   |             |                 |                 |
   | ID              |             |                 |                 |
   +-----------------+-------------+-----------------+-----------------+
   | >Measurement    | (0028,7012) | -               |                 |
   | Equipment       |             |                 |                 |
   | Sequence        |             |                 |                 |
   +-----------------+-------------+-----------------+-----------------+
   | >>Item #1 of    | (FFFE,E000) | -               |                 |
   | Measurement     |             |                 |                 |
   | Equipment       |             |                 |                 |
   | Sequence        |             |                 |                 |
   +-----------------+-------------+-----------------+-----------------+
   | >>Measurement   | (0028,7013) | -               | PHOTOME         |
   | Functions       |             |                 | TER\COLORIMETER |
   +-----------------+-------------+-----------------+-----------------+
   | >>Measured      | (0028,7026) | -               | UNI             |
   | Characteristics |             |                 | FORMITY\LUMINAN |
   |                 |             |                 | CE\CHROMATICITY |
   +-----------------+-------------+-----------------+-----------------+
   | >>Measurement   | (0028,7014) | -               | BUILT_IN_FRONT  |
   | Equipment Type  |             |                 |                 |
   +-----------------+-------------+-----------------+-----------------+
   | >> Manufacturer | (0008,0070) | -               | Lumin           |
   |                 |             |                 | anceMeasurement |
   |                 |             |                 | Device Inc.     |
   +-----------------+-------------+-----------------+-----------------+
   | >               | (0008,1090) | -               | LC1000          |
   | >Manufacturer's |             |                 |                 |
   | Model Name      |             |                 |                 |
   +-----------------+-------------+-----------------+-----------------+
   | >> Device       | (0018,1000) | -               | SN99990011      |
   | Serial Number   |             |                 |                 |
   +-----------------+-------------+-----------------+-----------------+
   | >> DateTime of  | (0018,1202) | -               |                 |
   | Last            |             |                 |                 |
   | Calibration     |             |                 |                 |
   +-----------------+-------------+-----------------+-----------------+
   | >>Item          | (FFFE,E00D) | -               |                 |
   | Delimiter of    |             |                 |                 |
   | Item #1 of      |             |                 |                 |
   | Measurement     |             |                 |                 |
   | Equipment       |             |                 |                 |
   | Sequence        |             |                 |                 |
   +-----------------+-------------+-----------------+-----------------+
   | >>Sequence      | (FFFE,E0DD) | -               |                 |
   | Delimiter of    |             |                 |                 |
   | Measurement     |             |                 |                 |
   | Equipment       |             |                 |                 |
   | Sequence        |             |                 |                 |
   +-----------------+-------------+-----------------+-----------------+
   | >Item Delimiter | (FFFE,E00D) | -               |                 |
   | of Item #3 of   |             |                 |                 |
   | Display         |             |                 |                 |
   | Subsystem       |             |                 |                 |
   | Sequence        |             |                 |                 |
   +-----------------+-------------+-----------------+-----------------+
   | >Sequence       | (FFFE,E0DD) | -               |                 |
   | Delimiter of    |             |                 |                 |
   | Display         |             |                 |                 |
   | Subsystem       |             |                 |                 |
   | Sequence        |             |                 |                 |
   +-----------------+-------------+-----------------+-----------------+
   | **Target        |             |                 |                 |
   | Luminance       |             |                 |                 |
   | Characteristics |             |                 |                 |
   | Module**        |             |                 |                 |
   +-----------------+-------------+-----------------+-----------------+
   | Target          | (0028,7008) | VNP             |                 |
   | Luminance       |             |                 |                 |
   | Characteristics |             |                 |                 |
   | Sequence        |             |                 |                 |
   +-----------------+-------------+-----------------+-----------------+
   | >Item #1 of     | (FFFE,E000) | -               |                 |
   | Target          |             |                 |                 |
   | Luminance       |             |                 |                 |
   | Characteristics |             |                 |                 |
   | Sequence        |             |                 |                 |
   +-----------------+-------------+-----------------+-----------------+
   | >Luminance      | (0028,7009) | -               | 1               |
   | Characteristics |             |                 |                 |
   | ID              |             |                 |                 |
   +-----------------+-------------+-----------------+-----------------+
   | >Display        | (0028,7019) | -               | GAMMA           |
   | Function Type   |             |                 |                 |
   +-----------------+-------------+-----------------+-----------------+
   | >Target Minimum | (0028,701D) | -               | 0.75            |
   | Luminance       |             |                 |                 |
   +-----------------+-------------+-----------------+-----------------+
   | >Target Maximum | (0028,701E) | -               | 250             |
   | Luminance       |             |                 |                 |
   +-----------------+-------------+-----------------+-----------------+
   | >Gamma Value    | (0028,701A) | -               | 2.2             |
   +-----------------+-------------+-----------------+-----------------+
   | >Item Delimiter | (FFFE,E00D) | -               |                 |
   | of Item #1 of   |             |                 |                 |
   | Target          |             |                 |                 |
   | Luminance       |             |                 |                 |
   | Characteristics |             |                 |                 |
   | Sequence        |             |                 |                 |
   +-----------------+-------------+-----------------+-----------------+
   | >Item #2 of     | (FFFE,E000) | -               |                 |
   | Target          |             |                 |                 |
   | Luminance       |             |                 |                 |
   | Characteristics |             |                 |                 |
   | Sequence        |             |                 |                 |
   +-----------------+-------------+-----------------+-----------------+
   | >Luminance      | (0028,7009) | -               | 2               |
   | Characteristics |             |                 |                 |
   | ID              |             |                 |                 |
   +-----------------+-------------+-----------------+-----------------+
   | >Display        | (0028,7019) | -               | GSDF            |
   | Function Type   |             |                 |                 |
   +-----------------+-------------+-----------------+-----------------+
   | >Target Minimum | (0028,701D) | -               | 0.75            |
   | Luminance       |             |                 |                 |
   +-----------------+-------------+-----------------+-----------------+
   | >Target Maximum | (0028,701E) | -               | 521.0           |
   | Luminance       |             |                 |                 |
   +-----------------+-------------+-----------------+-----------------+
   | >Reflected      | (2010,0160) | -               | 0.410           |
   | Ambient Light   |             |                 |                 |
   +-----------------+-------------+-----------------+-----------------+
   | >Ambient Light  | (0028,7025) | -               | DEFAULT         |
   | Value Source    |             |                 |                 |
   +-----------------+-------------+-----------------+-----------------+
   | >Item Delimiter | (FFFE,E00D) | -               |                 |
   | of Item #2 of   |             |                 |                 |
   | Target          |             |                 |                 |
   | Luminance       |             |                 |                 |
   | Characteristics |             |                 |                 |
   | Sequence        |             |                 |                 |
   +-----------------+-------------+-----------------+-----------------+
   | >Item #3 of     | (FFFE,E000) | -               |                 |
   | Target          |             |                 |                 |
   | Luminance       |             |                 |                 |
   | Characteristics |             |                 |                 |
   | Sequence        |             |                 |                 |
   +-----------------+-------------+-----------------+-----------------+
   | >Luminance      | (0028,7009) | -               | 3               |
   | Characteristics |             |                 |                 |
   | ID              |             |                 |                 |
   +-----------------+-------------+-----------------+-----------------+
   | >Display        | (0028,7019) | -               | GSDF            |
   | Function Type   |             |                 |                 |
   +-----------------+-------------+-----------------+-----------------+
   | >Target Minimum | (0028,701D) | -               | 0.75            |
   | Luminance       |             |                 |                 |
   +-----------------+-------------+-----------------+-----------------+
   | >Target Maximum | (0028,701E) | -               | 520.0           |
   | Luminance       |             |                 |                 |
   +-----------------+-------------+-----------------+-----------------+
   | >Reflected      | (2010,0160) | -               | 0.410           |
   | Ambient Light   |             |                 |                 |
   +-----------------+-------------+-----------------+-----------------+
   | >Ambient Light  | (0028,7025) | -               | DEFAULT         |
   | Value Source    |             |                 |                 |
   +-----------------+-------------+-----------------+-----------------+
   | >Item Delimiter | (FFFE,E00D) | -               |                 |
   | of Item #3 of   |             |                 |                 |
   | Target          |             |                 |                 |
   | Luminance       |             |                 |                 |
   | Characteristics |             |                 |                 |
   | Sequence        |             |                 |                 |
   +-----------------+-------------+-----------------+-----------------+
   | >Sequence       | (FFFE,E0DD) | -               |                 |
   | Delimiter of    |             |                 |                 |
   | Target          |             |                 |                 |
   | Luminance       |             |                 |                 |
   | Characteristics |             |                 |                 |
   | Sequence        |             |                 |                 |
   +-----------------+-------------+-----------------+-----------------+
   | **QA Result     |             |                 |                 |
   | Module**        |             |                 |                 |
   +-----------------+-------------+-----------------+-----------------+
   | See             |             |                 |                 |
   | `tabl           |             |                 |                 |
   | e_title <#table |             |                 |                 |
   | _PPP.3.1-2>`__. |             |                 |                 |
   +-----------------+-------------+-----------------+-----------------+

This example is encoded with Undefined Sequence Length and Undefined
Item Length , so it contains Sequence Delimitation Items and Item
Delimitation Items.

.. table:: Example of N-GET Request/Response for QA Result Module

   +-----------------+-------------+-----------------+-----------------+
   | Attribute Name  | Tag         | N-GET Request   | N-GET Response  |
   |                 |             | (SCU)           | (SCP)           |
   +=================+=============+=================+=================+
   | **QA Result     |             |                 |                 |
   | Module**        |             |                 |                 |
   +-----------------+-------------+-----------------+-----------------+
   | QA Results      | (0028,700F) | VNP             |                 |
   | Sequence        |             |                 |                 |
   +-----------------+-------------+-----------------+-----------------+
   | >Item #1 of QA  | (FFFE,E000) | -               |                 |
   | Results         |             |                 |                 |
   | Sequence        |             |                 |                 |
   +-----------------+-------------+-----------------+-----------------+
   | >Display        | (0028,7003) | -               | 2               |
   | Subsystem ID    |             |                 |                 |
   +-----------------+-------------+-----------------+-----------------+
   | >Display        | (0028,7010) | -               |                 |
   | Subsystem QA    |             |                 |                 |
   | Results         |             |                 |                 |
   | Sequence        |             |                 |                 |
   +-----------------+-------------+-----------------+-----------------+
   | >>Item #1 of    | (FFFE,E000) | -               |                 |
   | Display System  |             |                 |                 |
   | QA Results      |             |                 |                 |
   | Sequence        |             |                 |                 |
   +-----------------+-------------+-----------------+-----------------+
   | >>Configuration | (0028,700B) | -               | 1               |
   | ID              |             |                 |                 |
   +-----------------+-------------+-----------------+-----------------+
   | >>Configuration | (0028,7011) | -               |                 |
   | QA Results      |             |                 |                 |
   | Sequence        |             |                 |                 |
   +-----------------+-------------+-----------------+-----------------+
   | >>>Item #1 of   | (FFFE,E000) | -               |                 |
   | Configuration   |             |                 |                 |
   | QA Results      |             |                 |                 |
   | Sequence        |             |                 |                 |
   +-----------------+-------------+-----------------+-----------------+
   | >>>Display      | (0028,7016) | -               |                 |
   | Calibration     |             |                 |                 |
   | Result Sequence |             |                 |                 |
   +-----------------+-------------+-----------------+-----------------+
   | >>>>Item #1 of  |             | -               |                 |
   | Display         |             |                 |                 |
   | Calibration     |             |                 |                 |
   | Result Sequence |             |                 |                 |
   +-----------------+-------------+-----------------+-----------------+
   | >>>>Performed   | (0040,4050) | -               | 20130610191010  |
   | Procedure Step  |             |                 |                 |
   | Start DateTime  |             |                 |                 |
   +-----------------+-------------+-----------------+-----------------+
   | >>>>Performed   | (0040,4051) | -               | 20130610192030  |
   | Procedure Step  |             |                 |                 |
   | End DateTime    |             |                 |                 |
   +-----------------+-------------+-----------------+-----------------+
   | >>>>Actual      | (0040,4035) | -               |                 |
   | Human Performer |             |                 |                 |
   | Sequence        |             |                 |                 |
   +-----------------+-------------+-----------------+-----------------+
   | >>>>Item #1 of  | (FFFE,E000) | -               |                 |
   | Actual Human    |             |                 |                 |
   | Performer       |             |                 |                 |
   | Sequence        |             |                 |                 |
   +-----------------+-------------+-----------------+-----------------+
   | >>>>>Human      | (0040,4037) | -               | Kido^Kousei     |
   | Performer's     |             |                 |                 |
   | Name            |             |                 |                 |
   +-----------------+-------------+-----------------+-----------------+
   | >>>>>Human      | (0040,4036) | -               | QA Dept.        |
   | Performer's     |             |                 |                 |
   | Organization    |             |                 |                 |
   +-----------------+-------------+-----------------+-----------------+
   | >>>>> Item      | (FFFE,E00D) | -               |                 |
   | Delimiter of    |             |                 |                 |
   | Item #1 of      |             |                 |                 |
   | Actual Human    |             |                 |                 |
   | Performer       |             |                 |                 |
   | Sequence        |             |                 |                 |
   +-----------------+-------------+-----------------+-----------------+
   | >>>>>Sequence   | (FFFE,E0DD) | -               |                 |
   | Delimiter of    |             |                 |                 |
   | Actual Human    |             |                 |                 |
   | Performer       |             |                 |                 |
   | Sequence        |             |                 |                 |
   +-----------------+-------------+-----------------+-----------------+
   | >>>>Measurement | (0028,7012) | -               |                 |
   | Equipment       |             |                 |                 |
   | Sequence        |             |                 |                 |
   +-----------------+-------------+-----------------+-----------------+
   | >>>>>Item #1 of | (FFFE,E000) | -               |                 |
   | Measurement     |             |                 |                 |
   | Equipment       |             |                 |                 |
   | Sequence        |             |                 |                 |
   +-----------------+-------------+-----------------+-----------------+
   | >               | (0028,7013) | -               | PHOTOMETER      |
   | >>>>Measurement |             |                 |                 |
   | Functions       |             |                 |                 |
   +-----------------+-------------+-----------------+-----------------+
   | >>>>>Measured   | (0028,7026) | -               | LUMINANCE       |
   | Characteristics |             |                 |                 |
   +-----------------+-------------+-----------------+-----------------+
   | >               | (0028,7014) | -               | NEAR_RANGE      |
   | >>>>Measurement |             |                 |                 |
   | Equipment Type  |             |                 |                 |
   +-----------------+-------------+-----------------+-----------------+
   | >>              | (0008,0070) | -               | LUXDEVICE       |
   | >>>Manufacturer |             |                 | COMPANY         |
   +-----------------+-------------+-----------------+-----------------+
   | >>>>            | (0008,1090) | -               | PHOTOMETER      |
   | >Manufacturer's |             |                 | MODEL1          |
   | Model Name      |             |                 |                 |
   +-----------------+-------------+-----------------+-----------------+
   | >>>>>Device     | (0018,1000) | -               | PM1-141421356   |
   | Serial Number   |             |                 |                 |
   +-----------------+-------------+-----------------+-----------------+
   | >>>>>DateTime   | (0018,1202) | -               | 201303310900    |
   | of Last         |             |                 |                 |
   | Calibration     |             |                 |                 |
   +-----------------+-------------+-----------------+-----------------+
   | >>>>> Item      | (FFFE,E00D) | -               |                 |
   | Delimiter of    |             |                 |                 |
   | Item #1 of      |             |                 |                 |
   | Measurement     |             |                 |                 |
   | Equipment       |             |                 |                 |
   | Sequence        |             |                 |                 |
   +-----------------+-------------+-----------------+-----------------+
   | >>>>>Sequence   | (FFFE,E0DD) | -               |                 |
   | Delimiter of    |             |                 |                 |
   | Measurement     |             |                 |                 |
   | Equipment       |             |                 |                 |
   | Sequence        |             |                 |                 |
   +-----------------+-------------+-----------------+-----------------+
   | >>>>Luminance   | (0028,7009) | -               | 2               |
   | Characteristics |             |                 |                 |
   | ID              |             |                 |                 |
   +-----------------+-------------+-----------------+-----------------+
   | >>>>Item #1 of  | (FFFE,E00D) | -               |                 |
   | Display         |             |                 |                 |
   | Calibration     |             |                 |                 |
   | Result Sequence |             |                 |                 |
   +-----------------+-------------+-----------------+-----------------+
   | >>>>Sequence    | (FFFE,E0DD) | -               |                 |
   | Delimiter of    |             |                 |                 |
   | Display         |             |                 |                 |
   | Calibration     |             |                 |                 |
   | Result Sequence |             |                 |                 |
   +-----------------+-------------+-----------------+-----------------+
   | >>>Visual       | (0028,7015) | -               |                 |
   | Evaluation      |             |                 |                 |
   | Result Sequence |             |                 |                 |
   +-----------------+-------------+-----------------+-----------------+
   | >>>>Item #1 of  | (FFFE,E000) | -               |                 |
   | Visual          |             |                 |                 |
   | Evaluation      |             |                 |                 |
   | Result Sequence |             |                 |                 |
   +-----------------+-------------+-----------------+-----------------+
   | >>>>Performed   | (0040,4050) | -               | 201307150900    |
   | Procedure Step  |             |                 |                 |
   | Start DateTime  |             |                 |                 |
   +-----------------+-------------+-----------------+-----------------+
   | >>>>Performed   | (0040,4051) | -               | 201307150910    |
   | Procedure Step  |             |                 |                 |
   | End DateTime    |             |                 |                 |
   +-----------------+-------------+-----------------+-----------------+
   | >>>>Actual      | (0040,4035) | -               |                 |
   | Human Performer |             |                 |                 |
   | Sequence        |             |                 |                 |
   +-----------------+-------------+-----------------+-----------------+
   | >>>>Item #1 of  | (FFFE,E000) | -               |                 |
   | Actual Human    |             |                 |                 |
   | Performer       |             |                 |                 |
   | Sequence        |             |                 |                 |
   +-----------------+-------------+-----------------+-----------------+
   | >>>>>Human      | (0040,4037) | -               | Mokushi^Shirou  |
   | Performer's     |             |                 |                 |
   | Name            |             |                 |                 |
   +-----------------+-------------+-----------------+-----------------+
   | >>>>>Human      | (0040,4036) | -               | Radiology Dept. |
   | Performer's     |             |                 |                 |
   | Organization    |             |                 |                 |
   +-----------------+-------------+-----------------+-----------------+
   | >>>>> Item      | (FFFE,E00D) | -               |                 |
   | Delimiter of    |             |                 |                 |
   | Item #1 of      |             |                 |                 |
   | Actual Human    |             |                 |                 |
   | Performer       |             |                 |                 |
   | Sequence        |             |                 |                 |
   +-----------------+-------------+-----------------+-----------------+
   | >>>>>Sequence   | (FFFE,E0DD) | -               |                 |
   | Delimiter of    |             |                 |                 |
   | Actual Human    |             |                 |                 |
   | Performer       |             |                 |                 |
   | Sequence        |             |                 |                 |
   +-----------------+-------------+-----------------+-----------------+
   | >>>>Visual      | (0028,7028) | -               |                 |
   | Evaluation Test |             |                 |                 |
   | Sequence        |             |                 |                 |
   +-----------------+-------------+-----------------+-----------------+
   | >>>>>Item #1 of | (FFFE,E000) | -               |                 |
   | Visual          |             |                 |                 |
   | Evaluation Test |             |                 |                 |
   | Sequence        |             |                 |                 |
   +-----------------+-------------+-----------------+-----------------+
   | >>>>>Test       | (0028,7029) | -               | PASS            |
   | Result          |             |                 |                 |
   +-----------------+-------------+-----------------+-----------------+
   | >>>>>Test       | (0028,702A) | -               | All appearances |
   | Result Comment  |             |                 | were OK.        |
   +-----------------+-------------+-----------------+-----------------+
   | >>>>>Test       | (0028,702C) | -               |                 |
   | Pattern Code    |             |                 |                 |
   | Sequence        |             |                 |                 |
   +-----------------+-------------+-----------------+-----------------+
   | >>>>>>Item #1   | (FFFE,E000) | -               |                 |
   | of Test Pattern |             |                 |                 |
   | Code Sequence   |             |                 |                 |
   +-----------------+-------------+-----------------+-----------------+
   | >>>>>>Code      | (0008,0100) | -               | 109801          |
   | Value           |             |                 |                 |
   +-----------------+-------------+-----------------+-----------------+
   | >>>>>>Coding    | (0008,0102) | -               | DCM             |
   | Scheme          |             |                 |                 |
   | Designator      |             |                 |                 |
   +-----------------+-------------+-----------------+-----------------+
   | >>>>>>Code      | (0008,0104) | -               | TG18-QC Pattern |
   | Meaning         |             |                 |                 |
   +-----------------+-------------+-----------------+-----------------+
   | >>>>>> Item     | (FFFE,E00D) | -               |                 |
   | Delimiter of    |             |                 |                 |
   | Item #1 of Test |             |                 |                 |
   | Pattern Code    |             |                 |                 |
   | Sequence        |             |                 |                 |
   +-----------------+-------------+-----------------+-----------------+
   | >>>>>>Sequence  | (FFFE,E0DD) | -               |                 |
   | Delimiter of    |             |                 |                 |
   | Test Pattern    |             |                 |                 |
   | Code Sequence   |             |                 |                 |
   +-----------------+-------------+-----------------+-----------------+
   | >>>>>Visual     | (0028,702E) | -               |                 |
   | Evaluation      |             |                 |                 |
   | Method Code     |             |                 |                 |
   | Sequence        |             |                 |                 |
   +-----------------+-------------+-----------------+-----------------+
   | >>>>>>Item #1   | (FFFE,E000) | -               |                 |
   | of Visual       |             |                 |                 |
   | Evaluation      |             |                 |                 |
   | Method Code     |             |                 |                 |
   | Sequence        |             |                 |                 |
   +-----------------+-------------+-----------------+-----------------+
   | >>>>>>Code      | (0008,0100) | -               | 109701          |
   | Value           |             |                 |                 |
   +-----------------+-------------+-----------------+-----------------+
   | >>>>>>Coding    | (0008,0102) | -               | DCM             |
   | Scheme          |             |                 |                 |
   | Designator      |             |                 |                 |
   +-----------------+-------------+-----------------+-----------------+
   | >>>>>>Code      | (0008,0104) | -               | Overall image   |
   | Meaning         |             |                 | quality         |
   |                 |             |                 | evaluation      |
   +-----------------+-------------+-----------------+-----------------+
   | >>>>>> Item     | (FFFE,E00D) | -               |                 |
   | Delimiter of    |             |                 |                 |
   | Item #1 of      |             |                 |                 |
   | Visual          |             |                 |                 |
   | Evaluation      |             |                 |                 |
   | Method Code     |             |                 |                 |
   | Sequence        |             |                 |                 |
   +-----------------+-------------+-----------------+-----------------+
   | >>>>>>Sequence  | (FFFE,E0DD) | -               |                 |
   | Delimiter of    |             |                 |                 |
   | Visual          |             |                 |                 |
   | Evaluation      |             |                 |                 |
   | Method Code     |             |                 |                 |
   | Sequence        |             |                 |                 |
   +-----------------+-------------+-----------------+-----------------+
   | >>>> Item       | (FFFE,E00D) | -               |                 |
   | Delimiter of    |             |                 |                 |
   | Item #1 of      |             |                 |                 |
   | Visual          |             |                 |                 |
   | Evaluation Test |             |                 |                 |
   | Sequence        |             |                 |                 |
   +-----------------+-------------+-----------------+-----------------+
   | >>>Sequence     | (FFFE,E0DD) | -               |                 |
   | Delimiter of    |             |                 |                 |
   | Visual          |             |                 |                 |
   | Evaluation Test |             |                 |                 |
   | Sequence        |             |                 |                 |
   +-----------------+-------------+-----------------+-----------------+
   | >>>Luminance    | (0028,7027) | -               |                 |
   | Uniformity      |             |                 |                 |
   | Result Sequence |             |                 |                 |
   +-----------------+-------------+-----------------+-----------------+
   | >>>>Item #1 of  | (FFFE,E000) | -               |                 |
   | Luminance       |             |                 |                 |
   | Uniformity      |             |                 |                 |
   | Result Sequence |             |                 |                 |
   +-----------------+-------------+-----------------+-----------------+
   | >>>>Performed   | (0040,4050) | -               | 20130610195000  |
   | Procedure Step  |             |                 |                 |
   | Start DateTime  |             |                 |                 |
   +-----------------+-------------+-----------------+-----------------+
   | >>>>Performed   | (0040,4051) | -               | 20130610195900  |
   | Procedure Step  |             |                 |                 |
   | End DateTime    |             |                 |                 |
   +-----------------+-------------+-----------------+-----------------+
   | >>>>Actual      | (0040,4035) | -               |                 |
   | Human Performer |             |                 |                 |
   | Sequence        |             |                 |                 |
   +-----------------+-------------+-----------------+-----------------+
   | >>>>Item #1 of  | (FFFE,E000) | -               |                 |
   | Actual Human    |             |                 |                 |
   | Performer       |             |                 |                 |
   | Sequence        |             |                 |                 |
   +-----------------+-------------+-----------------+-----------------+
   | >>>>>Human      | (0040,4037) | -               | Kido^Kousei     |
   | Performer's     |             |                 |                 |
   | Name            |             |                 |                 |
   +-----------------+-------------+-----------------+-----------------+
   | >>>>>Human      | (0040,4036) | -               | QA Dept.        |
   | Performer's     |             |                 |                 |
   | Organization    |             |                 |                 |
   +-----------------+-------------+-----------------+-----------------+
   | >>>>>Item       | (FFFE,E00D) | -               |                 |
   | Delimiter of    |             |                 |                 |
   | Item #1 of      |             |                 |                 |
   | Actual Human    |             |                 |                 |
   | Performer       |             |                 |                 |
   | Sequence        |             |                 |                 |
   +-----------------+-------------+-----------------+-----------------+
   | >>>>>Sequence   | (FFFE,E0DD) | -               |                 |
   | Delimiter of    |             |                 |                 |
   | Actual Human    |             |                 |                 |
   | Performer       |             |                 |                 |
   | Sequence        |             |                 |                 |
   +-----------------+-------------+-----------------+-----------------+
   | >>>>Measurement | (0028,7012) | -               |                 |
   | Equipment       |             |                 |                 |
   | Sequence        |             |                 |                 |
   +-----------------+-------------+-----------------+-----------------+
   | >>>>>Item #1 of | (FFFE,E000) | -               |                 |
   | Measurement     |             |                 |                 |
   | Equipment       |             |                 |                 |
   | Sequence        |             |                 |                 |
   +-----------------+-------------+-----------------+-----------------+
   | >               | (0028,7013) | -               | PHOTOME         |
   | >>>>Measurement |             |                 | TER\COLORIMETER |
   | Functions       |             |                 |                 |
   +-----------------+-------------+-----------------+-----------------+
   | >>>>>Measured   | (0028,7026) | -               | LUMINAN         |
   | Characteristics |             |                 | CE\CHROMATICITY |
   +-----------------+-------------+-----------------+-----------------+
   | >               | (0028,7014) | -               | NEAR_RANGE      |
   | >>>>Measurement |             |                 |                 |
   | Equipment Type  |             |                 |                 |
   +-----------------+-------------+-----------------+-----------------+
   | >>              | (0008,0070) | -               | LUXDEVICE       |
   | >>>Manufacturer |             |                 | COMPANY         |
   +-----------------+-------------+-----------------+-----------------+
   | >>>>            | (0008,1090) | -               | PHOTOMETER      |
   | >Manufacturer's |             |                 | MODEL1          |
   | Model Name      |             |                 |                 |
   +-----------------+-------------+-----------------+-----------------+
   | >>>>>Device     | (0018,1000) | -               | PM1-141421356   |
   | Serial Number   |             |                 |                 |
   +-----------------+-------------+-----------------+-----------------+
   | >>>>>DateTime   | (0018,1202) | -               | 201303310900    |
   | of Last         |             |                 |                 |
   | Calibration     |             |                 |                 |
   +-----------------+-------------+-----------------+-----------------+
   | >>>>>Item       | (FFFE,E00D) | -               |                 |
   | Delimiter of    |             |                 |                 |
   | Item #1 of      |             |                 |                 |
   | Measurement     |             |                 |                 |
   | Equipment       |             |                 |                 |
   | Sequence        |             |                 |                 |
   +-----------------+-------------+-----------------+-----------------+
   | >>>>>Sequence   | (FFFE,E0DD) | -               |                 |
   | Delimiter of    |             |                 |                 |
   | Measurement     |             |                 |                 |
   | Equipment       |             |                 |                 |
   | Sequence        |             |                 |                 |
   +-----------------+-------------+-----------------+-----------------+
   | >>>>Number of   | (0028,701B) | -               | 5               |
   | Luminance       |             |                 |                 |
   | Points          |             |                 |                 |
   +-----------------+-------------+-----------------+-----------------+
   | >>>>Measurement | (0028,702D) | -               |                 |
   | Pattern Code    |             |                 |                 |
   | Sequence        |             |                 |                 |
   +-----------------+-------------+-----------------+-----------------+
   | >>>>>Item #1 of | (FFFE,E000) | -               |                 |
   | Measurement     |             |                 |                 |
   | Pattern Code    |             |                 |                 |
   | Sequence        |             |                 |                 |
   +-----------------+-------------+-----------------+-----------------+
   | >>>>>Code Value | (0008,0100) | -               | 109844          |
   +-----------------+-------------+-----------------+-----------------+
   | >>>>>Coding     | (0008,0102) | -               | DCM             |
   | Scheme          |             |                 |                 |
   | Designator      |             |                 |                 |
   +-----------------+-------------+-----------------+-----------------+
   | >>>>>Code       | (0008,0104) | -               | TG18-UNL80      |
   | Meaning         |             |                 | Pattern         |
   +-----------------+-------------+-----------------+-----------------+
   | >>>>>Item       | (FFFE,E00D) | -               |                 |
   | Delimiter of    |             |                 |                 |
   | Item #1 of      |             |                 |                 |
   | Measurement     |             |                 |                 |
   | Pattern Code    |             |                 |                 |
   | Sequence        |             |                 |                 |
   +-----------------+-------------+-----------------+-----------------+
   | >>>>>Sequence   | (FFFE,E0DD) | -               |                 |
   | Delimiter of    |             |                 |                 |
   | Measurement     |             |                 |                 |
   | Pattern Code    |             |                 |                 |
   | Sequence        |             |                 |                 |
   +-----------------+-------------+-----------------+-----------------+
   | >>>>DDL Value   | (0028,7017) | -               | 204             |
   +-----------------+-------------+-----------------+-----------------+
   | >>>>White Point | (0028,7021) | -               | YES             |
   | Flag            |             |                 |                 |
   +-----------------+-------------+-----------------+-----------------+
   | >>>>Luminance   | (0028,701C) | -               |                 |
   | Response        |             |                 |                 |
   | Sequence        |             |                 |                 |
   +-----------------+-------------+-----------------+-----------------+
   | >>>>>Item #1 of | (FFFE,E000) | -               |                 |
   | Luminance       |             |                 |                 |
   | Response        |             |                 |                 |
   | Sequence        |             |                 |                 |
   +-----------------+-------------+-----------------+-----------------+
   | >>>>>Luminance  | (0028,701F) | -               | 191.5           |
   | Value           |             |                 |                 |
   +-----------------+-------------+-----------------+-----------------+
   | >>>>>CIExy      | (0028,7018) | -               | 0.              |
   | White Point     |             |                 | 940694\1.455249 |
   +-----------------+-------------+-----------------+-----------------+
   | >>>>>Item       | (FFFE,E00D) | -               |                 |
   | Delimiter of    |             |                 |                 |
   | Item            |             |                 |                 |
   | #1Luminance     |             |                 |                 |
   | Response        |             |                 |                 |
   | Sequence        |             |                 |                 |
   +-----------------+-------------+-----------------+-----------------+
   | >>>>>Item #2 of | (FFFE,E000) | -               |                 |
   | Luminance       |             |                 |                 |
   | Response        |             |                 |                 |
   | Sequence        |             |                 |                 |
   +-----------------+-------------+-----------------+-----------------+
   | >>>>>Luminance  | (0028,701F) | -               | 176.1           |
   | Value           |             |                 |                 |
   +-----------------+-------------+-----------------+-----------------+
   | >>>>>CIExy      | (0028,7018) | -               | 0.              |
   | White Point     |             |                 | 932555\1.421037 |
   +-----------------+-------------+-----------------+-----------------+
   | >>>>>Item       | (FFFE,E00D) | -               |                 |
   | Delimiter of    |             |                 |                 |
   | Item #2         |             |                 |                 |
   | Luminance       |             |                 |                 |
   | Response        |             |                 |                 |
   | Sequence        |             |                 |                 |
   +-----------------+-------------+-----------------+-----------------+
   | >>>>>Item #3 of | (FFFE,E000) | -               |                 |
   | Luminance       |             |                 |                 |
   | Response        |             |                 |                 |
   | Sequence        |             |                 |                 |
   +-----------------+-------------+-----------------+-----------------+
   | >>>>>Luminance  | (0028,701F) | -               | 197.2           |
   | Value           |             |                 |                 |
   +-----------------+-------------+-----------------+-----------------+
   | >>>>>CIExy      | (0028,7018) | -               | 0.              |
   | White Point     |             |                 | 918886\1.416465 |
   +-----------------+-------------+-----------------+-----------------+
   | >>>>>Item       | (FFFE,E00D) | -               |                 |
   | Delimiter of    |             |                 |                 |
   | Item #3 of      |             |                 |                 |
   | Luminance       |             |                 |                 |
   | Response        |             |                 |                 |
   | Sequence        |             |                 |                 |
   +-----------------+-------------+-----------------+-----------------+
   | >>>>>Item #4 of | (FFFE,E000) | -               |                 |
   | Luminance       |             |                 |                 |
   | Response        |             |                 |                 |
   | Sequence        |             |                 |                 |
   +-----------------+-------------+-----------------+-----------------+
   | >>>>>Luminance  | (0028,701F) | -               | 202.5           |
   | Value           |             |                 |                 |
   +-----------------+-------------+-----------------+-----------------+
   | >>>>>CIExy      | (0028,7018) | -               | 0.              |
   | White Point     |             |                 | 940709\1.434902 |
   +-----------------+-------------+-----------------+-----------------+
   | >>>>>Item       | (FFFE,E00D) | -               |                 |
   | Delimiter of    |             |                 |                 |
   | Item #4         |             |                 |                 |
   | Luminance       |             |                 |                 |
   | Response        |             |                 |                 |
   | Sequence        |             |                 |                 |
   +-----------------+-------------+-----------------+-----------------+
   | >>>>>Item #5 of | (FFFE,E000) | -               |                 |
   | Luminance       |             |                 |                 |
   | Response        |             |                 |                 |
   | Sequence        |             |                 |                 |
   +-----------------+-------------+-----------------+-----------------+
   | >>>>>Luminance  | (0028,701F) | -               | 195.8           |
   | Value           |             |                 |                 |
   +-----------------+-------------+-----------------+-----------------+
   | >>>>>CIExy      | (0028,7018) | -               | 0.              |
   | White Point     |             |                 | 946154\1.477551 |
   +-----------------+-------------+-----------------+-----------------+
   | >>>>>Item       | (FFFE,E00D) | -               |                 |
   | Delimiter of    |             |                 |                 |
   | Item            |             |                 |                 |
   | #5Luminance     |             |                 |                 |
   | Response        |             |                 |                 |
   | Sequence        |             |                 |                 |
   +-----------------+-------------+-----------------+-----------------+
   | >>>>>Sequence   | (FFFE,E0DD) | -               |                 |
   | Delimiter of    |             |                 |                 |
   | Luminance       |             |                 |                 |
   | Response        |             |                 |                 |
   | Sequence        |             |                 |                 |
   +-----------------+-------------+-----------------+-----------------+
   | >>>Luminance    | (0028,7024) | -               |                 |
   | Result Sequence |             |                 |                 |
   +-----------------+-------------+-----------------+-----------------+
   | >>>>Item #1 of  | (0028,e000) | -               |                 |
   | Luminance       |             |                 |                 |
   | Result Sequence |             |                 |                 |
   +-----------------+-------------+-----------------+-----------------+
   | >>>>Performed   | (0040,4050) | -               | 20130610194000  |
   | Procedure Step  |             |                 |                 |
   | Start DateTime  |             |                 |                 |
   +-----------------+-------------+-----------------+-----------------+
   | >>>>Performed   | (0040,4051) | -               | 20130610195500  |
   | Procedure Step  |             |                 |                 |
   | End DateTime    |             |                 |                 |
   +-----------------+-------------+-----------------+-----------------+
   | >>>>Actual      | (0040,4035) | -               |                 |
   | Human Performer |             |                 |                 |
   | Sequence        |             |                 |                 |
   +-----------------+-------------+-----------------+-----------------+
   | >>>>Item #1 of  | (FFFE,E000) | -               |                 |
   | Actual Human    |             |                 |                 |
   | Performer       |             |                 |                 |
   | Sequence        |             |                 |                 |
   +-----------------+-------------+-----------------+-----------------+
   | >>>>>Human      | (0040,4037) | -               | Kido^Kousei     |
   | Performer's     |             |                 |                 |
   | Name            |             |                 |                 |
   +-----------------+-------------+-----------------+-----------------+
   | >>>>>Human      | (0040,4036) | -               | QA Dept.        |
   | Performer's     |             |                 |                 |
   | Organization    |             |                 |                 |
   +-----------------+-------------+-----------------+-----------------+
   | >>>>>Item       | (FFFE,E00D) | -               |                 |
   | Delimiter of    |             |                 |                 |
   | Item #1 of      |             |                 |                 |
   | Actual Human    |             |                 |                 |
   | Performer       |             |                 |                 |
   | Sequence        |             |                 |                 |
   +-----------------+-------------+-----------------+-----------------+
   | >>>>>Sequence   | (FFFE,E0DD) | -               |                 |
   | Delimiter of    |             |                 |                 |
   | Actual Human    |             |                 |                 |
   | Performer       |             |                 |                 |
   | Sequence        |             |                 |                 |
   +-----------------+-------------+-----------------+-----------------+
   | >>>>Measurement | (0028,7012) | -               |                 |
   | Equipment       |             |                 |                 |
   | Sequence        |             |                 |                 |
   +-----------------+-------------+-----------------+-----------------+
   | >>>>>Item #1 of | (FFFE,E000) | -               |                 |
   | Measurement     |             |                 |                 |
   | Equipment       |             |                 |                 |
   | Sequence        |             |                 |                 |
   +-----------------+-------------+-----------------+-----------------+
   | >               | (0028,7013) | -               | PHOTOME         |
   | >>>>Measurement |             |                 | TER\COLORIMETER |
   | Functions       |             |                 |                 |
   +-----------------+-------------+-----------------+-----------------+
   | >>>>>Measured   | (0028,7026) | -               | LUMINAN         |
   | Characteristics |             |                 | CE\CHROMATICITY |
   +-----------------+-------------+-----------------+-----------------+
   | >               | (0028,7014) | -               | NEAR_RANGE      |
   | >>>>Measurement |             |                 |                 |
   | Equipment Type  |             |                 |                 |
   +-----------------+-------------+-----------------+-----------------+
   | >>              | (0008,0070) | -               | LUXDEVICE       |
   | >>>Manufacturer |             |                 | COMPANY         |
   +-----------------+-------------+-----------------+-----------------+
   | >>>>            | (0008,1090) | -               | PHOTOMETER      |
   | >Manufacturer's |             |                 | MODEL1          |
   | Model Name      |             |                 |                 |
   +-----------------+-------------+-----------------+-----------------+
   | >>>>>Device     | (0018,1000) | -               | PM1-141421356   |
   | Serial Number   |             |                 |                 |
   +-----------------+-------------+-----------------+-----------------+
   | >>>>>DateTime   | (0018,1202) | -               | 201303310900    |
   | of Last         |             |                 |                 |
   | Calibration     |             |                 |                 |
   +-----------------+-------------+-----------------+-----------------+
   | >>>>>Item       | (FFFE,E00D) | -               |                 |
   | Delimiter of    |             |                 |                 |
   | Item #1 of      |             |                 |                 |
   | Measurement     |             |                 |                 |
   | Equipment       |             |                 |                 |
   | Sequence        |             |                 |                 |
   +-----------------+-------------+-----------------+-----------------+
   | >>>>>Sequence   | (FFFE,E0DD) | -               |                 |
   | Delimiter of    |             |                 |                 |
   | Measurement     |             |                 |                 |
   | Equipment       |             |                 |                 |
   | Sequence        |             |                 |                 |
   +-----------------+-------------+-----------------+-----------------+
   | >>>>Number of   | (0028,701B) | -               | 18              |
   | Luminance       |             |                 |                 |
   | Points          |             |                 |                 |
   +-----------------+-------------+-----------------+-----------------+
   | >>>>Luminance   | (0028,701C) | -               |                 |
   | Response        |             |                 |                 |
   | Sequence        |             |                 |                 |
   +-----------------+-------------+-----------------+-----------------+
   | >>>>>Item #1 of | (FFFE,E000) | -               |                 |
   | Luminance       |             |                 |                 |
   | Result Sequence |             |                 |                 |
   +-----------------+-------------+-----------------+-----------------+
   | >>>>>DDL Value  | (0028,7017) | -               | 0               |
   +-----------------+-------------+-----------------+-----------------+
   | >>>>>Luminance  | (0028,701F) | -               | 0.64            |
   | Value           |             |                 |                 |
   +-----------------+-------------+-----------------+-----------------+
   | >>>>>Item       | (FFFE,E00D) | -               |                 |
   | Delimiter of    |             |                 |                 |
   | Item #1 of      |             |                 |                 |
   | Luminance       |             |                 |                 |
   | Result Sequence |             |                 |                 |
   +-----------------+-------------+-----------------+-----------------+
   | >>>>>Item #2 of | (FFFE,E000) | -               |                 |
   | Luminance       |             |                 |                 |
   | Result Sequence |             |                 |                 |
   +-----------------+-------------+-----------------+-----------------+
   | >>>>>DDL Value  | (0028,7017) | -               | 15              |
   +-----------------+-------------+-----------------+-----------------+
   | >>>>>Luminance  | (0028,701F) | -               | 2.03            |
   | Value           |             |                 |                 |
   +-----------------+-------------+-----------------+-----------------+
   | >>>>>Item       | (FFFE,E00D) | -               |                 |
   | Delimiter of    |             |                 |                 |
   | Item #2 of      |             |                 |                 |
   | Luminance       |             |                 |                 |
   | Result Sequence |             |                 |                 |
   +-----------------+-------------+-----------------+-----------------+
   | >>>>>Item #3 of | (FFFE,E000) | -               |                 |
   | Luminance       |             |                 |                 |
   | Result Sequence |             |                 |                 |
   +-----------------+-------------+-----------------+-----------------+
   | >>>>>DDL Value  | (0028,7017) | -               | 30              |
   +-----------------+-------------+-----------------+-----------------+
   | >>>>>Luminance  | (0028,701F) | -               | 4.17            |
   | Value           |             |                 |                 |
   +-----------------+-------------+-----------------+-----------------+
   | >>>>>Item       | (FFFE,E00D) | -               |                 |
   | Delimiter of    |             |                 |                 |
   | Item #3 of      |             |                 |                 |
   | Luminance       |             |                 |                 |
   | Result Sequence |             |                 |                 |
   +-----------------+-------------+-----------------+-----------------+
   | >>>>>Item #4 of | (FFFE,E000) | -               |                 |
   | Luminance       |             |                 |                 |
   | Result Sequence |             |                 |                 |
   +-----------------+-------------+-----------------+-----------------+
   | >>>>>DDL Value  | (0028,7017) | -               | 45              |
   +-----------------+-------------+-----------------+-----------------+
   | >>>>>Luminance  | (0028,701F) | -               | 7.11            |
   | Value           |             |                 |                 |
   +-----------------+-------------+-----------------+-----------------+
   | >>>>>Item       | (FFFE,E00D) | -               |                 |
   | Delimiter of    |             |                 |                 |
   | Item #4 of      |             |                 |                 |
   | Luminance       |             |                 |                 |
   | Result Sequence |             |                 |                 |
   +-----------------+-------------+-----------------+-----------------+
   | >>>>>Item #5 of | (FFFE,E000) | -               |                 |
   | Luminance       |             |                 |                 |
   | Result Sequence |             |                 |                 |
   +-----------------+-------------+-----------------+-----------------+
   | >>>>>DDL Value  | (0028,7017) | -               | 60              |
   +-----------------+-------------+-----------------+-----------------+
   | >>>>>Luminance  | (0028,701F) | -               | 11.12           |
   | Value           |             |                 |                 |
   +-----------------+-------------+-----------------+-----------------+
   | >>>>>Item       | (FFFE,E00D) | -               |                 |
   | Delimiter of    |             |                 |                 |
   | Item #5 of      |             |                 |                 |
   | Luminance       |             |                 |                 |
   | Result Sequence |             |                 |                 |
   +-----------------+-------------+-----------------+-----------------+
   | >>>>>Item #6 of | (FFFE,E000) | -               |                 |
   | Luminance       |             |                 |                 |
   | Result Sequence |             |                 |                 |
   +-----------------+-------------+-----------------+-----------------+
   | >>>>>DDL Value  | (0028,7017) | -               | 75              |
   +-----------------+-------------+-----------------+-----------------+
   | >>>>>Luminance  | (0028,701F) | -               | 16.75           |
   | Value           |             |                 |                 |
   +-----------------+-------------+-----------------+-----------------+
   | >>>>>Item       | (FFFE,E00D) | -               |                 |
   | Delimiter of    |             |                 |                 |
   | Item #6 of      |             |                 |                 |
   | Luminance       |             |                 |                 |
   | Result Sequence |             |                 |                 |
   +-----------------+-------------+-----------------+-----------------+
   | >>>>>Item #7 of | (FFFE,E000) | -               |                 |
   | Luminance       |             |                 |                 |
   | Result Sequence |             |                 |                 |
   +-----------------+-------------+-----------------+-----------------+
   | >>>>>DDL Value  | (0028,7017) | -               | 90              |
   +-----------------+-------------+-----------------+-----------------+
   | >>>>>Luminance  | (0028,701F) | -               | 24.07           |
   | Value           |             |                 |                 |
   +-----------------+-------------+-----------------+-----------------+
   | >>>>>Item       | (FFFE,E00D) | -               |                 |
   | Delimiter of    |             |                 |                 |
   | Item #7 of      |             |                 |                 |
   | Luminance       |             |                 |                 |
   | Result Sequence |             |                 |                 |
   +-----------------+-------------+-----------------+-----------------+
   | >>>>>Item #8 of | (FFFE,E000) | -               |                 |
   | Luminance       |             |                 |                 |
   | Result Sequence |             |                 |                 |
   +-----------------+-------------+-----------------+-----------------+
   | >>>>>DDL Value  | (0028,7017) | -               | 105             |
   +-----------------+-------------+-----------------+-----------------+
   | >>>>>Luminance  | (0028,701F) | -               | 33.67           |
   | Value           |             |                 |                 |
   +-----------------+-------------+-----------------+-----------------+
   | >>>>>Item       | (FFFE,E00D) | -               |                 |
   | Delimiter of    |             |                 |                 |
   | Item #8 of      |             |                 |                 |
   | Luminance       |             |                 |                 |
   | Result Sequence |             |                 |                 |
   +-----------------+-------------+-----------------+-----------------+
   | >>>>>Item #9 of | (FFFE,E000) | -               |                 |
   | Luminance       |             |                 |                 |
   | Result Sequence |             |                 |                 |
   +-----------------+-------------+-----------------+-----------------+
   | >>>>>DDL Value  | (0028,7017) | -               | 120             |
   +-----------------+-------------+-----------------+-----------------+
   | >>>>>Luminance  | (0028,701F) | -               | 46.24           |
   | Value           |             |                 |                 |
   +-----------------+-------------+-----------------+-----------------+
   | >>>>>Item       | (FFFE,E00D) | -               |                 |
   | Delimiter of    |             |                 |                 |
   | Item #9 of      |             |                 |                 |
   | Luminance       |             |                 |                 |
   | Result Sequence |             |                 |                 |
   +-----------------+-------------+-----------------+-----------------+
   | >>>>>Item #10   | (FFFE,E000) | -               |                 |
   | of Luminance    |             |                 |                 |
   | Result Sequence |             |                 |                 |
   +-----------------+-------------+-----------------+-----------------+
   | >>>>>DDL Value  | (0028,7017) | -               | 135             |
   +-----------------+-------------+-----------------+-----------------+
   | >>>>>Luminance  | (0028,701F) | -               | 63.12           |
   | Value           |             |                 |                 |
   +-----------------+-------------+-----------------+-----------------+
   | >>>>>Item       | (FFFE,E00D) | -               |                 |
   | Delimiter of    |             |                 |                 |
   | Item #10 of     |             |                 |                 |
   | Luminance       |             |                 |                 |
   | Result Sequence |             |                 |                 |
   +-----------------+-------------+-----------------+-----------------+
   | >>>>>Item #11   | (FFFE,E000) | -               |                 |
   | of Luminance    |             |                 |                 |
   | Result Sequence |             |                 |                 |
   +-----------------+-------------+-----------------+-----------------+
   | >>>>>DDL Value  | (0028,7017) | -               | 150             |
   +-----------------+-------------+-----------------+-----------------+
   | >>>>>Luminance  | (0028,701F) | -               | 83.94           |
   | Value           |             |                 |                 |
   +-----------------+-------------+-----------------+-----------------+
   | >>>>>Item       | (FFFE,E00D) | -               |                 |
   | Delimiter of    |             |                 |                 |
   | Item #11 of     |             |                 |                 |
   | Luminance       |             |                 |                 |
   | Result Sequence |             |                 |                 |
   +-----------------+-------------+-----------------+-----------------+
   | >>>>>Item #12   | (FFFE,E000) | -               |                 |
   | of Luminance    |             |                 |                 |
   | Result Sequence |             |                 |                 |
   +-----------------+-------------+-----------------+-----------------+
   | >>>>>DDL Value  | (0028,7017) | -               | 160             |
   +-----------------+-------------+-----------------+-----------------+
   | >>>>>Luminance  | (0028,701F) | -               | 110.6           |
   | Value           |             |                 |                 |
   +-----------------+-------------+-----------------+-----------------+
   | >>>>>Item       | (FFFE,E00D) | -               |                 |
   | Delimiter of    |             |                 |                 |
   | Item #12 of     |             |                 |                 |
   | Luminance       |             |                 |                 |
   | Result Sequence |             |                 |                 |
   +-----------------+-------------+-----------------+-----------------+
   | >>>>>Item #13   | (FFFE,E000) | -               |                 |
   | of Luminance    |             |                 |                 |
   | Result Sequence |             |                 |                 |
   +-----------------+-------------+-----------------+-----------------+
   | >>>>>DDL Value  | (0028,7017) | -               | 180             |
   +-----------------+-------------+-----------------+-----------------+
   | >>>>>Luminance  | (0028,701F) | -               | 144.9           |
   | Value           |             |                 |                 |
   +-----------------+-------------+-----------------+-----------------+
   | >>>>>Item       | (FFFE,E00D) | -               |                 |
   | Delimiter of    |             |                 |                 |
   | Item #13 of     |             |                 |                 |
   | Luminance       |             |                 |                 |
   | Result Sequence |             |                 |                 |
   +-----------------+-------------+-----------------+-----------------+
   | >>>>>Item #14   | (FFFE,E000) | -               |                 |
   | of Luminance    |             |                 |                 |
   | Result Sequence |             |                 |                 |
   +-----------------+-------------+-----------------+-----------------+
   | >>>>>DDL Value  | (0028,7017) | -               | 195             |
   +-----------------+-------------+-----------------+-----------------+
   | >>>>>Luminance  | (0028,701F) | -               | 190.1           |
   | Value           |             |                 |                 |
   +-----------------+-------------+-----------------+-----------------+
   | >>>>>Item       | (FFFE,E00D) | -               |                 |
   | Delimiter of    |             |                 |                 |
   | Item #14 of     |             |                 |                 |
   | Luminance       |             |                 |                 |
   | Result Sequence |             |                 |                 |
   +-----------------+-------------+-----------------+-----------------+
   | >>>>>Item #15   | (FFFE,E000) | -               |                 |
   | of Luminance    |             |                 |                 |
   | Result Sequence |             |                 |                 |
   +-----------------+-------------+-----------------+-----------------+
   | >>>>>DDL Value  | (0028,7017) | -               | 210             |
   +-----------------+-------------+-----------------+-----------------+
   | >>>>>Luminance  | (0028,701F) | -               | 246.3           |
   | Value           |             |                 |                 |
   +-----------------+-------------+-----------------+-----------------+
   | >>>>>Item       | (FFFE,E00D) | -               |                 |
   | Delimiter of    |             |                 |                 |
   | Item #15 of     |             |                 |                 |
   | Luminance       |             |                 |                 |
   | Result Sequence |             |                 |                 |
   +-----------------+-------------+-----------------+-----------------+
   | >>>>>Item #16   | (FFFE,E000) | -               |                 |
   | of Luminance    |             |                 |                 |
   | Result Sequence |             |                 |                 |
   +-----------------+-------------+-----------------+-----------------+
   | >>>>>DDL Value  | (0028,7017) | -               | 225             |
   +-----------------+-------------+-----------------+-----------------+
   | >>>>>Luminance  | (0028,701F) | -               | 317.8           |
   | Value           |             |                 |                 |
   +-----------------+-------------+-----------------+-----------------+
   | >>>>>Item       | (FFFE,E00D) | -               |                 |
   | Delimiter of    |             |                 |                 |
   | Item #16 of     |             |                 |                 |
   | Luminance       |             |                 |                 |
   | Result Sequence |             |                 |                 |
   +-----------------+-------------+-----------------+-----------------+
   | >>>>>Item #17   | (FFFE,E000) | -               |                 |
   | of Luminance    |             |                 |                 |
   | Result Sequence |             |                 |                 |
   +-----------------+-------------+-----------------+-----------------+
   | >>>>>DDL Value  | (0028,7017) | -               | 240             |
   +-----------------+-------------+-----------------+-----------------+
   | >>>>>Luminance  | (0028,701F) | -               | 406.4           |
   | Value           |             |                 |                 |
   +-----------------+-------------+-----------------+-----------------+
   | >>>>>Item       | (FFFE,E00D) | -               |                 |
   | Delimiter of    |             |                 |                 |
   | Item #17 of     |             |                 |                 |
   | Luminance       |             |                 |                 |
   | Result Sequence |             |                 |                 |
   +-----------------+-------------+-----------------+-----------------+
   | >>>>>Item #18   | (FFFE,E000) | -               |                 |
   | of Luminance    |             |                 |                 |
   | Result Sequence |             |                 |                 |
   +-----------------+-------------+-----------------+-----------------+
   | >>>>>DDL Value  | (0028,7017) | -               | 255             |
   +-----------------+-------------+-----------------+-----------------+
   | >>>>>Luminance  | (0028,701F) | -               | 520.9           |
   | Value           |             |                 |                 |
   +-----------------+-------------+-----------------+-----------------+
   | >>>>>Item       | (FFFE,E00D) | -               |                 |
   | Delimiter of    |             |                 |                 |
   | Item #18 of     |             |                 |                 |
   | Luminance       |             |                 |                 |
   | Result Sequence |             |                 |                 |
   +-----------------+-------------+-----------------+-----------------+
   | >>>>>Sequence   | (FFFE,E0DD) | -               |                 |
   | Delimiter of    |             |                 |                 |
   | Luminance       |             |                 |                 |
   | Response        |             |                 |                 |
   | Sequence        |             |                 |                 |
   +-----------------+-------------+-----------------+-----------------+
   | >>>>Reflected   | (2010,0160) | -               | 0.408           |
   | Ambient Light   |             |                 |                 |
   +-----------------+-------------+-----------------+-----------------+
   | >>>>Ambient     | (0028,7025) | -               | MEASURED        |
   | Light Source    |             |                 |                 |
   +-----------------+-------------+-----------------+-----------------+
   | >>>>Item        | (0028,e00D) | -               |                 |
   | Delimiter of    |             |                 |                 |
   | Item #1 of      |             |                 |                 |
   | Luminance       |             |                 |                 |
   | Result Sequence |             |                 |                 |
   +-----------------+-------------+-----------------+-----------------+
   | >>>>Sequence    | (0028,e0DD) | -               |                 |
   | Delimiter of    |             |                 |                 |
   | Luminance       |             |                 |                 |
   | Result Sequence |             |                 |                 |
   +-----------------+-------------+-----------------+-----------------+
   | >>>Item #1      | (0028,e00D) | -               |                 |
   | Configuration   |             |                 |                 |
   | QA Results      |             |                 |                 |
   | Sequence        |             |                 |                 |
   +-----------------+-------------+-----------------+-----------------+
   | >>>Sequence     | (0028,e0DD) | -               |                 |
   | Delimiter of    |             |                 |                 |
   | Configuration   |             |                 |                 |
   | QA Results      |             |                 |                 |
   | Sequence        |             |                 |                 |
   +-----------------+-------------+-----------------+-----------------+
   | >>Item          | (0028,e00D) | -               |                 |
   | Delimiter of    |             |                 |                 |
   | Item #1 of      |             |                 |                 |
   | Display System  |             |                 |                 |
   | QA Results      |             |                 |                 |
   | Sequence        |             |                 |                 |
   +-----------------+-------------+-----------------+-----------------+
   | >Sequence       | (0028,e0DD) | -               |                 |
   | Delimiter of    |             |                 |                 |
   | Display System  |             |                 |                 |
   | QA Results      |             |                 |                 |
   | Sequence        |             |                 |                 |
   +-----------------+-------------+-----------------+-----------------+
   | >Item Delimiter | (0028,e00D) | -               |                 |
   | of Item #1 of   |             |                 |                 |
   | QA Results      |             |                 |                 |
   | Sequence        |             |                 |                 |
   +-----------------+-------------+-----------------+-----------------+
   | >Item #2 of QA  | (FFFE,E000) | -               |                 |
   | Results         |             |                 |                 |
   | Sequence        |             |                 |                 |
   +-----------------+-------------+-----------------+-----------------+
   | >Display        | (0028,7003) | -               | 3               |
   | Subsystem ID    |             |                 |                 |
   +-----------------+-------------+-----------------+-----------------+
   | **…**           |             | -               | The SCP will    |
   |                 |             |                 | return the      |
   |                 |             |                 | values for      |
   |                 |             |                 | Display         |
   |                 |             |                 | Subsystem ID=3. |
   +-----------------+-------------+-----------------+-----------------+
   | >Item Delimiter | (0028,e00D) | -               |                 |
   | of Item #2 of   |             |                 |                 |
   | QA Results      |             |                 |                 |
   | Sequence        |             |                 |                 |
   +-----------------+-------------+-----------------+-----------------+
   | >Sequence       | (0028,e0DD) | -               |                 |
   | Delimiter of QA |             |                 |                 |
   | Results         |             |                 |                 |
   | Sequence        |             |                 |                 |
   +-----------------+-------------+-----------------+-----------------+

.. _sect_PPP.3.2:

An Example of A Tablet Display
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

A Tablet Display System is shown in
`figure_title <#figure_PPP.3.2-1>`__.

The following is an example of an N-GET Request/Response pair for the
Display System SOP Class.

This example is encoded with Undefined Sequence Length and Undefined
Item Length, so it contains Sequence Delimitation Items and Item
Delimitation Items.

ANP
   Attribute Not Present.

VNP
   Attribute Present but Value Not Present.

-
   Not specified.

.. table:: N-GET Request/Response Example

   +-----------------+-------------+-----------------+-----------------+
   | Attribute Name  | Tag         | N-GET Request   | N-GET Response  |
   |                 |             | (SCU)           | (SCP)           |
   +=================+=============+=================+=================+
   | **SOP Common    |             |                 |                 |
   | and Workstation |             |                 |                 |
   | Modules**       |             |                 |                 |
   +-----------------+-------------+-----------------+-----------------+
   | Specific        | (0008,0005) | ANP             | \\ISO 2022 IR   |
   | Character Set   |             |                 | 87              |
   +-----------------+-------------+-----------------+-----------------+
   | Manufacturer    | (0008,0070) | VNP             | Tablet Corp.    |
   +-----------------+-------------+-----------------+-----------------+
   | Institution     | (0008,0080) | VNP             | JIRA Hospital   |
   | Name            |             |                 |                 |
   +-----------------+-------------+-----------------+-----------------+
   | Institution     | (0008,0081) | VNP             | Bunkyo-ku,      |
   | Address         |             |                 | Tokyo, Japan    |
   +-----------------+-------------+-----------------+-----------------+
   | Device Serial   | (0018,1000) | VNP             | AA1B22CCCC3D    |
   | Number          |             |                 |                 |
   +-----------------+-------------+-----------------+-----------------+
   | Station Name    | (0008,1010) | VNP             | TABLET1         |
   +-----------------+-------------+-----------------+-----------------+
   | Institutional   | (0008,1040) | VNP             | Radiology Dept. |
   | Department Name |             |                 |                 |
   +-----------------+-------------+-----------------+-----------------+
   | Manufacturer's  | (0008,1090) | VNP             | MC706J/A        |
   | Model Name      |             |                 |                 |
   +-----------------+-------------+-----------------+-----------------+
   | Equipment       | (0028,7000) | VNP             |                 |
   | Administrator   |             |                 |                 |
   | Sequence        |             |                 |                 |
   +-----------------+-------------+-----------------+-----------------+
   | >Item #1 of     | (FFFE,E000) | -               |                 |
   | Equipment       |             |                 |                 |
   | Administrator   |             |                 |                 |
   | Sequence        |             |                 |                 |
   +-----------------+-------------+-----------------+-----------------+
   | >Person Name    | (0040,A123) | -               | Yamada^         |
   |                 |             |                 | Tarou=山田^太郎 |
   |                 |             |                 | =やまだ^たろう  |
   +-----------------+-------------+-----------------+-----------------+
   | >Person         | (0040,1101) | -               |                 |
   | Identification  |             |                 |                 |
   | Code Sequence   |             |                 |                 |
   +-----------------+-------------+-----------------+-----------------+
   | >>Item #1 of    | (FFFE,E000) | -               |                 |
   | Person          |             |                 |                 |
   | Identification  |             |                 |                 |
   | Code Sequence   |             |                 |                 |
   +-----------------+-------------+-----------------+-----------------+
   | >>Code Value    | (0008,0110) | -               | 111111          |
   +-----------------+-------------+-----------------+-----------------+
   | >>Coding Scheme | (0008,0102) | -               | LOCAL           |
   | Designator      |             |                 |                 |
   +-----------------+-------------+-----------------+-----------------+
   | >>Code Meaning  | (0008,0104) | -               | Yamada^Tarou    |
   +-----------------+-------------+-----------------+-----------------+
   | >>Item          | (FFFE,E00D) | -               |                 |
   | Delimiter of    |             |                 |                 |
   | Item #1 of      |             |                 |                 |
   | Person          |             |                 |                 |
   | Identification  |             |                 |                 |
   | Code Sequence   |             |                 |                 |
   +-----------------+-------------+-----------------+-----------------+
   | >>Sequence      | (FFFE,E0DD) | -               |                 |
   | Delimiter of    |             |                 |                 |
   | Person          |             |                 |                 |
   | Identification  |             |                 |                 |
   | Code Sequence   |             |                 |                 |
   +-----------------+-------------+-----------------+-----------------+
   | >Person's       | (0040,1102) | -               |                 |
   | Address         |             |                 |                 |
   +-----------------+-------------+-----------------+-----------------+
   | >Person's       | (0040,1103) | -               | EXT. 1234       |
   | Telephone       |             |                 |                 |
   | Number          |             |                 |                 |
   +-----------------+-------------+-----------------+-----------------+
   | >Institution    | (0008,0080) | -               | IT Support Div. |
   | Name            |             |                 |                 |
   +-----------------+-------------+-----------------+-----------------+
   | >Item Delimiter | (FFFE,E00D) | -               |                 |
   | of Item #1 of   |             |                 |                 |
   | Equipment       |             |                 |                 |
   | Administrator   |             |                 |                 |
   | Sequence        |             |                 |                 |
   +-----------------+-------------+-----------------+-----------------+
   | >Sequence       | (FFFE,E0DD) | -               |                 |
   | Delimiter of    |             |                 |                 |
   | Equipment       |             |                 |                 |
   | Administrator   |             |                 |                 |
   | Sequence        |             |                 |                 |
   +-----------------+-------------+-----------------+-----------------+
   | **Display       |             |                 |                 |
   | System Module** |             |                 |                 |
   +-----------------+-------------+-----------------+-----------------+
   | Number of       | (0028,7001) | VNP             | 1               |
   | Display         |             |                 |                 |
   | Subsystems      |             |                 |                 |
   +-----------------+-------------+-----------------+-----------------+
   | Display         | (0028,7023) | VNP             |                 |
   | Subsystem       |             |                 |                 |
   | Sequence        |             |                 |                 |
   +-----------------+-------------+-----------------+-----------------+
   | Item #1 of      | (FFFE,E000) | -               |                 |
   | Display         |             |                 |                 |
   | Subsystem       |             |                 |                 |
   | Sequence        |             |                 |                 |
   +-----------------+-------------+-----------------+-----------------+
   | >Display        | (0028,7003) | -               | 1               |
   | Subsystem ID    |             |                 |                 |
   +-----------------+-------------+-----------------+-----------------+
   | >Display        | (0028,7004) | -               | DS1             |
   | Subsystem Name  |             |                 |                 |
   +-----------------+-------------+-----------------+-----------------+
   | >Display        | (0028,7005) | -               | Embedded LCD    |
   | Subsystem       |             |                 |                 |
   | Description     |             |                 |                 |
   +-----------------+-------------+-----------------+-----------------+
   | >Display Device | (0028,7022) | -               |                 |
   | Type Code       |             |                 |                 |
   | Sequence        |             |                 |                 |
   +-----------------+-------------+-----------------+-----------------+
   | >>Item #1 of    | (FFFE,E000) | -               |                 |
   | Display Device  |             |                 |                 |
   | Type Code       |             |                 |                 |
   | Sequence        |             |                 |                 |
   +-----------------+-------------+-----------------+-----------------+
   | >>Code Value    | (0008,0100) | -               | 109992          |
   +-----------------+-------------+-----------------+-----------------+
   | >>Coding Scheme | (0008,0102) | -               | DCM             |
   | Designator      |             |                 |                 |
   +-----------------+-------------+-----------------+-----------------+
   | >>Code Meaning  | (0008,0104) | -               | Liquid Crystal  |
   |                 |             |                 | Display         |
   +-----------------+-------------+-----------------+-----------------+
   | >>Item          | (FFFE,E00D) | -               |                 |
   | Delimiter of    |             |                 |                 |
   | Item #1 of      |             |                 |                 |
   | Display Device  |             |                 |                 |
   | Type Code       |             |                 |                 |
   | Sequence        |             |                 |                 |
   +-----------------+-------------+-----------------+-----------------+
   | >>Sequence      | (FFFE,E0DD) | -               |                 |
   | Delimiter of    |             |                 |                 |
   | Display Device  |             |                 |                 |
   | Type Code       |             |                 |                 |
   | Sequence        |             |                 |                 |
   +-----------------+-------------+-----------------+-----------------+
   | >Manufacturer   | (0008,0070) | -               | Tablet Corp.    |
   +-----------------+-------------+-----------------+-----------------+
   | >Device Serial  | (0018,1000) | -               | AA1B22CCCC3D    |
   | Number          |             |                 |                 |
   +-----------------+-------------+-----------------+-----------------+
   | >Manufacturer's | (0008,1090) | -               | MC706J/A        |
   | Model Name      |             |                 |                 |
   +-----------------+-------------+-----------------+-----------------+
   | >System Status  | (0028,7006) | -               | NORMAL          |
   +-----------------+-------------+-----------------+-----------------+
   | >System Status  | (0028,7007) | -               |                 |
   | Comment         |             |                 |                 |
   +-----------------+-------------+-----------------+-----------------+
   | >Display        | (0028,700A) | -               |                 |
   | Subsystem       |             |                 |                 |
   | Configuration   |             |                 |                 |
   | Sequence        |             |                 |                 |
   +-----------------+-------------+-----------------+-----------------+
   | >>Item #1 of    | (FFFE,E000) | -               |                 |
   | Display         |             |                 |                 |
   | Subsystem       |             |                 |                 |
   | Configuration   |             |                 |                 |
   | Sequence        |             |                 |                 |
   +-----------------+-------------+-----------------+-----------------+
   | >>Configuration | (0028,700B) | -               | 1               |
   | ID              |             |                 |                 |
   +-----------------+-------------+-----------------+-----------------+
   | >>Configuration | (0028,700C) | -               | DS1Config1      |
   | Name            |             |                 |                 |
   +-----------------+-------------+-----------------+-----------------+
   | >>              | (0028,700D) | -               | Configuration1  |
   | Configuration   |             |                 | of Display      |
   | Description     |             |                 | Subsystem ID1   |
   +-----------------+-------------+-----------------+-----------------+
   | >>Referenced    | (0028,700E) | -               | 1               |
   | Target          |             |                 |                 |
   | Luminance       |             |                 |                 |
   | Characteristics |             |                 |                 |
   | ID              |             |                 |                 |
   +-----------------+-------------+-----------------+-----------------+
   | >>Item          | (FFFE,E00D) | -               |                 |
   | Delimiter of    |             |                 |                 |
   | Item #1 of      |             |                 |                 |
   | Display         |             |                 |                 |
   | Subsystem       |             |                 |                 |
   | Configuration   |             |                 |                 |
   | Sequence        |             |                 |                 |
   +-----------------+-------------+-----------------+-----------------+
   | >>Sequence      | (FFFE,E0DD) | -               |                 |
   | Delimiter of    |             |                 |                 |
   | Display         |             |                 |                 |
   | Subsystem       |             |                 |                 |
   | Configuration   |             |                 |                 |
   | Sequence        |             |                 |                 |
   +-----------------+-------------+-----------------+-----------------+
   | >Current        | (0028,7002) | -               | 1               |
   | Configuration   |             |                 |                 |
   | ID              |             |                 |                 |
   +-----------------+-------------+-----------------+-----------------+
   | >Measurement    | (0028,7012) | -               |                 |
   | Equipment       |             |                 |                 |
   | Sequence        |             |                 |                 |
   +-----------------+-------------+-----------------+-----------------+
   | >Sequence       | (FFFE,E0DD) | -               |                 |
   | Delimiter of    |             |                 |                 |
   | Measurement     |             |                 |                 |
   | Equipment       |             |                 |                 |
   | Sequence        |             |                 |                 |
   +-----------------+-------------+-----------------+-----------------+
   | >Item Delimiter | (FFFE,E00D) | -               |                 |
   | of Item #1 of   |             |                 |                 |
   | Display System  |             |                 |                 |
   | Sequence        |             |                 |                 |
   +-----------------+-------------+-----------------+-----------------+
   | >Sequence       | (FFFE,E0DD) | -               |                 |
   | Delimiter of    |             |                 |                 |
   | Display         |             |                 |                 |
   | Subsystem       |             |                 |                 |
   | Sequence        |             |                 |                 |
   +-----------------+-------------+-----------------+-----------------+
   | **Target        |             |                 |                 |
   | Luminance       |             |                 |                 |
   | Characteristics |             |                 |                 |
   | Module**        |             |                 |                 |
   +-----------------+-------------+-----------------+-----------------+
   | Target          | (0028,7008) | VNP             |                 |
   | Luminance       |             |                 |                 |
   | Characteristics |             |                 |                 |
   | Sequence        |             |                 |                 |
   +-----------------+-------------+-----------------+-----------------+
   | >Item #1 of     | (FFFE,E000) | -               |                 |
   | Target          |             |                 |                 |
   | Luminance       |             |                 |                 |
   | Characteristics |             |                 |                 |
   | Sequence        |             |                 |                 |
   +-----------------+-------------+-----------------+-----------------+
   | >Luminance      | (0028,7009) | -               | 1               |
   | Characteristics |             |                 |                 |
   | ID              |             |                 |                 |
   +-----------------+-------------+-----------------+-----------------+
   | >Display        | (0028,7019) | -               | GAMMA           |
   | Function Type   |             |                 |                 |
   +-----------------+-------------+-----------------+-----------------+
   | >Target Minimum | (0028,701D) | -               | 0.75            |
   | Luminance       |             |                 |                 |
   +-----------------+-------------+-----------------+-----------------+
   | >Target Maximum | (0028,701E) | -               | 300             |
   | Luminance       |             |                 |                 |
   +-----------------+-------------+-----------------+-----------------+
   | >Gamma Value    | (0028,701A) | -               | 2.2             |
   +-----------------+-------------+-----------------+-----------------+
   | >Item Delimiter | (FFFE,E00D) | -               |                 |
   | of Item #1 of   |             |                 |                 |
   | Target          |             |                 |                 |
   | Luminance       |             |                 |                 |
   | Characteristics |             |                 |                 |
   | Sequence        |             |                 |                 |
   +-----------------+-------------+-----------------+-----------------+
   | >Sequence       | (FFFE,E0DD) | -               |                 |
   | Delimiter of    |             |                 |                 |
   | Target          |             |                 |                 |
   | Luminance       |             |                 |                 |
   | Characteristics |             |                 |                 |
   | Sequence        |             |                 |                 |
   +-----------------+-------------+-----------------+-----------------+
   | **QA Result     |             |                 |                 |
   | Module**        |             |                 |                 |
   +-----------------+-------------+-----------------+-----------------+
   | QA Results      | (0028,700F) | VNP             |                 |
   | Sequence        |             |                 |                 |
   +-----------------+-------------+-----------------+-----------------+
   | >Item #1 of QA  | (FFFE,E000) | -               |                 |
   | Results         |             |                 |                 |
   | Sequence        |             |                 |                 |
   +-----------------+-------------+-----------------+-----------------+
   | >Display        | (0028,7003) | -               | 1               |
   | Subsystem ID    |             |                 |                 |
   +-----------------+-------------+-----------------+-----------------+
   | >Display        | (0028,7010) | -               | There are no    |
   | Subsystem QA    |             |                 | items in this   |
   | Results         |             |                 | sequence in     |
   | Sequence        |             |                 | this example.   |
   +-----------------+-------------+-----------------+-----------------+

