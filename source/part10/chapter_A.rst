.. _chapter_A:

Example of DICOMDIR File Content (Informative)
==============================================

This Annex provides an example of a File content that is based on
selected aspects of the example introduced in for the Basic Directory
Information Object. This is not a normative Annex. It is only an
illustration, which is simply intended to help the reader better
understand the organization of a DICOM Directory stored in a DICOMDIR
File.

.. _sect_A.1:

Simple Directory Content Example
--------------------------------

`table_title <#table_A.1-1>`__ shows in a simplified manner, the content
of a simple DICOMDIR File. Values of elements are noted between square
brackets (e.g., [1.2.840.10008.34.7.6]). Byte Offsets are shown by
symbolic Values noted between brackets (e.g., {1493}).

.. table:: Directory Content Example

   +----------------+----------------+----------------+----------------+
   |                | **Meta-Info**  | 128 bytes      | File Preamble  |
   |                |                |                | **[all bytes   |
   |                |                | 4 bytes        | set to 00H]**  |
   |                |                |                |                |
   |                |                | 0002,0000      | DICOM Prefix   |
   |                |                |                | **[DICM]**     |
   |                |                | 0002,0001      |                |
   |                |                |                | File Meta      |
   |                |                | 0002,0002      | Information    |
   |                |                |                | Group Length   |
   |                |                | 0002,0003      |                |
   |                |                |                | File           |
   |                |                | 0002,0010      | Me             |
   |                |                |                | ta-Information |
   |                |                | 0002,0012      | Version        |
   |                |                |                | **[0001]**     |
   |                |                | ...            |                |
   |                |                |                | Media Storage  |
   |                |                |                | SOP Class UID  |
   |                |                |                | **[1.2.840.1   |
   |                |                |                | 0008.1.3.10]** |
   |                |                |                |                |
   |                |                |                | Media Storage  |
   |                |                |                | SOP Instance   |
   |                |                |                | UID            |
   |                |                |                | **[1.2.840.23  |
   |                |                |                | 856.36.45.3]** |
   |                |                |                |                |
   |                |                |                | Transfer       |
   |                |                |                | Syntax UID     |
   |                |                |                | **[1.2.84      |
   |                |                |                | 0.10008.1.1]** |
   |                |                |                |                |
   |                |                |                | Implementation |
   |                |                |                | Class UID      |
   |                |                |                | **[1.2.840.23  |
   |                |                |                | 856.34.90.3]** |
   |                |                |                |                |
   |                |                |                | ...            |
   +----------------+----------------+----------------+----------------+
   | File-set       | 0004,1130      | File-set ID    |                |
   | Identification |                | **             |                |
   |                | ...            | [EXAMPLE]**... |                |
   +----------------+----------------+----------------+----------------+
   | General        | 0004,1200      | Offset of      |                |
   | Directory      |                | First Record   |                |
   | Information    | 0004,1202      | of Root        |                |
   |                |                | Directory      |                |
   |                | 0004,1212      | Entity         |                |
   |                |                | **{1829}**     |                |
   |                | ...            |                |                |
   |                |                | Offset of Last |                |
   |                | 0004,1220      | Record of Root |                |
   |                |                | Directory      |                |
   |                |                | Entity         |                |
   |                |                | **{6F18}**     |                |
   |                |                |                |                |
   |                |                | File-set       |                |
   |                |                | Consistency    |                |
   |                |                | Flag           |                |
   |                |                | **[0000H]**    |                |
   |                |                |                |                |
   |                |                | ...            |                |
   |                |                |                |                |
   |                |                | Directory      |                |
   |                |                | Record         |                |
   |                |                | Sequence.      |                |
   |                |                |                |                |
   |                |                | This Data      |                |
   |                |                | Element Value  |                |
   |                |                | includes the   |                |
   |                |                | following      |                |
   |                |                | Sequence of    |                |
   |                |                | Items.         |                |
   +----------------+----------------+----------------+----------------+
   | **{1829}**     | **Item Tag**   | FFFE,E000      | Item Data      |
   |                |                |                | Element        |
   |                |                |                | (includes the  |
   |                |                |                | following Data |
   |                |                |                | Elements)      |
   +----------------+----------------+----------------+----------------+
   | **Study 1**    | 0004,1400      | Offset of the  |                |
   |                |                | next Directory |                |
   | Directory      | 0004,1410      | Record in      |                |
   | Record         |                | Directory      |                |
   |                | 0004,1420      | Entity (not    |                |
   |                |                | shown in       |                |
   |                | ...            | example)       |                |
   |                |                |                |                |
   |                |                | Record In-use  |                |
   |                |                | Flag           |                |
   |                |                | **[FFFFH]**    |                |
   |                |                |                |                |
   |                |                | Offset of      |                |
   |                |                | Referenced     |                |
   |                |                | Lower Level    |                |
   |                |                | Directory      |                |
   |                |                | Entity         |                |
   |                |                | **{2299}**     |                |
   |                |                |                |                |
   |                |                | ...            |                |
   +----------------+----------------+----------------+----------------+
   | 0004,1430      | Directory      |                |                |
   |                | Record Type    |                |                |
   |                | **[STUDY]**    |                |                |
   +----------------+----------------+----------------+----------------+
   | *Selection     | 0020,000D      | Study Instance |                |
   | Keys*          |                | UID            |                |
   |                | 0020,0010      | *              |                |
   |                |                | *[1.2.840.4656 |                |
   |                | ...            | .23.4568745]** |                |
   |                |                |                |                |
   |                |                | Study ID       |                |
   |                |                | **[srt78UJ]**  |                |
   |                |                |                |                |
   |                |                | ....           |                |
   +----------------+----------------+----------------+----------------+
   | Item           | FFFE,E00D      | Item           |                |
   | Delimitation   |                | Delimitation   |                |
   | Tag            |                | Tag is present |                |
   |                |                | only if Item   |                |
   |                |                | is of          |                |
   |                |                | undefined      |                |
   |                |                | length         |                |
   +----------------+----------------+----------------+----------------+
   | **{2299}**     | **Item Tag**   | FFFE,E000      | Item Data      |
   |                |                |                | Element        |
   |                |                |                | (includes the  |
   |                |                |                | following Data |
   |                |                |                | Elements)      |
   +----------------+----------------+----------------+----------------+
   | **Series 1**   | 0004,1400      | Offset of the  |                |
   |                |                | next Directory |                |
   | Directory      | 0004,1410      | Record in      |                |
   | Record         |                | Directory      |                |
   |                | 0004,1420      | Entity (not    |                |
   |                |                | shown in       |                |
   |                | ...            | example)       |                |
   |                |                |                |                |
   |                |                | Record In-use  |                |
   |                |                | Flag           |                |
   |                |                | **[0FFFFH]**   |                |
   |                |                |                |                |
   |                |                | Offset of      |                |
   |                |                | Referenced     |                |
   |                |                | Lower Level    |                |
   |                |                | Directory      |                |
   |                |                | Entity         |                |
   |                |                | **{2681}**     |                |
   |                |                |                |                |
   |                |                | ...            |                |
   +----------------+----------------+----------------+----------------+
   | 0004,1430      | Directory      |                |                |
   |                | Record Type    |                |                |
   |                | **[SERIES]**   |                |                |
   +----------------+----------------+----------------+----------------+
   | *Selection     | 0008,0060      | Modality       |                |
   | Keys*          |                | **[NM]**       |                |
   |                | 0020,0011      |                |                |
   |                |                | Series Number  |                |
   |                | ...            | **[2]**        |                |
   |                |                |                |                |
   |                |                | ...            |                |
   +----------------+----------------+----------------+----------------+
   |                | Item           | FFFE,E00D      | Item           |
   |                | Delimitation   |                | Delimitation   |
   |                | Tag            |                | Tag is present |
   |                |                |                | only if Item   |
   |                |                |                | is of          |
   |                |                |                | undefined      |
   |                |                |                | length         |
   +----------------+----------------+----------------+----------------+
   | **{2681}**     | **Item Tag**   | FFFE,E000      | Item Data      |
   |                |                |                | Element        |
   |                |                |                | (includes the  |
   |                |                |                | following Data |
   |                |                |                | Elements)      |
   +----------------+----------------+----------------+----------------+
   | **Image 1**    | 0004,1400      | Offset of the  |                |
   |                |                | next Directory |                |
   | Directory      | 0004,1410      | Record in      |                |
   | Record         |                | Directory      |                |
   |                | 0004,1420      | Entity         |                |
   |                |                | **{3419}**     |                |
   |                | ...            |                |                |
   |                |                | Record In-use  |                |
   |                |                | Flag           |                |
   |                |                | **[FFFFH]**    |                |
   |                |                |                |                |
   |                |                | Offset of      |                |
   |                |                | Referenced     |                |
   |                |                | Lower Level    |                |
   |                |                | Directory      |                |
   |                |                | Entity         |                |
   |                |                | *              |                |
   |                |                | *[00000000H]** |                |
   |                |                |                |                |
   |                |                | ...            |                |
   +----------------+----------------+----------------+----------------+
   | 0004,1430      | Directory      |                |                |
   |                | Record Type    |                |                |
   |                | **[IMAGE]**    |                |                |
   +----------------+----------------+----------------+----------------+
   | 0004,1500      | Referenced     |                |                |
   |                | File ID        |                |                |
   | 0004,1510      | **[DIR\        |                |                |
   |                | TDRI\3856G3]** |                |                |
   | 0004,1511      |                |                |                |
   |                | Referenced SOP |                |                |
   | 0004,1512      | Class UID in   |                |                |
   |                | File           |                |                |
   |                | **[            |                |                |
   |                | 1.2.840.10008. |                |                |
   |                | 5.1.4.1.1.5]** |                |                |
   |                |                |                |                |
   |                | Referenced SOP |                |                |
   |                | Instance UID   |                |                |
   |                | in File        |                |                |
   |                | **[1           |                |                |
   |                | .2.840.34.56.7 |                |                |
   |                | 8999654.234]** |                |                |
   |                |                |                |                |
   |                | Referenced     |                |                |
   |                | Transfer       |                |                |
   |                | Syntax UID in  |                |                |
   |                | File           |                |                |
   |                | **[1.2.840.    |                |                |
   |                | 10008.1.2.1]** |                |                |
   +----------------+----------------+----------------+----------------+
   | *Selection     | 0008,0018      | Image SOP      |                |
   | Keys*          |                | Instance UID   |                |
   |                | 0020,0013      | **[1           |                |
   |                |                | .2.840.34.56.7 |                |
   |                | ...            | 8999654.234]** |                |
   |                |                |                |                |
   |                |                | Image Number   |                |
   |                |                | **[1]**        |                |
   |                |                |                |                |
   |                |                | ...            |                |
   +----------------+----------------+----------------+----------------+
   | Item           | FFFE,E00D      | Item           |                |
   | Delimitation   |                | Delimitation   |                |
   | Tag            |                | Tag is present |                |
   |                |                | only if Item   |                |
   |                |                | is of          |                |
   |                |                | undefined      |                |
   |                |                | length         |                |
   +----------------+----------------+----------------+----------------+
   | **{3419}**     | **Item Tag**   | FFFE,E000      | Item Data      |
   |                |                |                | Element        |
   |                |                |                | (includes the  |
   |                |                |                | following Data |
   |                |                |                | Elements)      |
   +----------------+----------------+----------------+----------------+
   | **Image 2**    | 0004,1400      | Offset of the  |                |
   |                |                | next Directory |                |
   | Directory      | 0004,1410      | Record in      |                |
   | Record         |                | Directory      |                |
   |                | 0004,1420      | Entity (not    |                |
   |                |                | shown in       |                |
   |                | ...            | example)       |                |
   |                |                |                |                |
   |                |                | Record In-use  |                |
   |                |                | Flag           |                |
   |                |                | **[FFFFH]**    |                |
   |                |                |                |                |
   |                |                | Offset of      |                |
   |                |                | Referenced     |                |
   |                |                | Lower Level    |                |
   |                |                | Directory      |                |
   |                |                | Entity         |                |
   |                |                | **[0           |                |
   |                |                | 0000000H]**... |                |
   +----------------+----------------+----------------+----------------+
   | 0004,1430      | Directory      |                |                |
   |                | Record Type    |                |                |
   |                | **[IMAGE]**    |                |                |
   +----------------+----------------+----------------+----------------+
   | 0004,1500      | Referenced     |                |                |
   |                | File ID        |                |                |
   | 0004,1510      | **[DIR\        |                |                |
   |                | TDRI\3856G7]** |                |                |
   | 0004,1511      |                |                |                |
   |                | Referenced SOP |                |                |
   | 0004,1512      | Class UID in   |                |                |
   |                | File           |                |                |
   |                | **[            |                |                |
   |                | 1.2.840.10008. |                |                |
   |                | 5.1.4.1.1.5]** |                |                |
   |                |                |                |                |
   |                | Referenced SOP |                |                |
   |                | Instance UID   |                |                |
   |                | in File        |                |                |
   |                | **[1           |                |                |
   |                | .2.840.34.56.7 |                |                |
   |                | 8999654.235]** |                |                |
   |                |                |                |                |
   |                | Referenced     |                |                |
   |                | Transfer       |                |                |
   |                | Syntax UID in  |                |                |
   |                | File           |                |                |
   |                | **[1.2.840.    |                |                |
   |                | 10008.1.2.2]** |                |                |
   +----------------+----------------+----------------+----------------+
   | *Selection     | 0008,0018      | Image SOP      |                |
   | Keys*          |                | Instance UID   |                |
   |                | 0020,0013      | **[1           |                |
   |                |                | .2.840.34.56.7 |                |
   |                | ...            | 8999654.235]** |                |
   |                |                |                |                |
   |                |                | Image Number   |                |
   |                |                | **[2]**        |                |
   |                |                |                |                |
   |                |                | ...            |                |
   +----------------+----------------+----------------+----------------+
   | Item           | FFFE,E00D      | Item           |                |
   | Delimitation   |                | Delimitation   |                |
   | Tag            |                | Tag is present |                |
   |                |                | only if Item   |                |
   |                |                | is of          |                |
   |                |                | undefined      |                |
   |                |                | length         |                |
   +----------------+----------------+----------------+----------------+
   | **{6F18}**     | **Item Tag**   | FFFE,E000      | Item Data      |
   |                |                |                | Element        |
   |                |                |                | (includes the  |
   |                |                |                | following Data |
   |                |                |                | Elements)      |
   +----------------+----------------+----------------+----------------+
   | **Patient C**  | 0004,1400      | Offset of the  |                |
   |                |                | next Directory |                |
   | Directory      | 0004,1410      | Record in      |                |
   | Record         |                | Directory      |                |
   |                | 0004,1430      | Entity         |                |
   |                |                | *              |                |
   |                | ...            | *{00000000H}** |                |
   |                |                |                |                |
   |                |                | Record In-use  |                |
   |                |                | Flag           |                |
   |                |                | **[FFFFH]**    |                |
   |                |                |                |                |
   |                |                | Directory      |                |
   |                |                | Record Type    |                |
   |                |                | **[PATIENT]**  |                |
   |                |                |                |                |
   |                |                | ...            |                |
   +----------------+----------------+----------------+----------------+
   | *Selection     | 0010,0010      | Patient Name   |                |
   | Keys*          |                | **[Patient     |                |
   |                | 0010,0020      | C]**           |                |
   |                |                |                |                |
   |                | ....           | Patient ID     |                |
   |                |                | **[            |                |
   |                |                | 523-61-8765]** |                |
   |                |                |                |                |
   |                |                | ....           |                |
   +----------------+----------------+----------------+----------------+
   | Item           | FFFE,E00D      | Item           |                |
   | Delimitation   |                | Delimitation   |                |
   | Tag            |                | Tag is present |                |
   |                |                | only if Item   |                |
   |                |                | is of          |                |
   |                |                | undefined      |                |
   |                |                | length         |                |
   +----------------+----------------+----------------+----------------+
   |                | Sequence       | FFFE,E0DD      | Used only if   |
   |                | Delimitation   |                | the Directory  |
   |                | Tag            |                | Record         |
   |                |                |                | Sequence       |
   |                |                |                | (0004,1220) is |
   |                |                |                | of undefined   |
   |                |                |                | length to      |
   |                |                |                | delimit the    |
   |                |                |                | end of the     |
   |                |                |                | Value of the   |
   |                |                |                | Directory      |
   |                |                |                | Record         |
   |                |                |                | Sequence Data  |
   |                |                |                | Element.       |
   +----------------+----------------+----------------+----------------+

.. _sect_A.2:

Example of DICOMDIR File Content With Multiple Referenced Files
---------------------------------------------------------------

This section was previously defined in DICOM. It is now retired. See
PS3.3-1998.

