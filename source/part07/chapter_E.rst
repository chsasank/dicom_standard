.. _chapter_E:

Command Dictionary (Normative)
==============================

.. _sect_E.1:

Registry of DICOM Command Elements
----------------------------------

.. table:: Command Fields

   +-----------+-----------+-----------+--------+--------+-----------+
   | **Tag**   | **Message | **        | **VR** | **VM** | **De      |
   |           | Field**   | Keyword** |        |        | scription |
   |           |           |           |        |        | of        |
   |           |           |           |        |        | Field**   |
   +===========+===========+===========+========+========+===========+
   | (0        | Command   | CommandGr | UL     | 1      | The even  |
   | 000,0000) | Group     | oupLength |        |        | number of |
   |           | Length    |           |        |        | bytes     |
   |           |           |           |        |        | from the  |
   |           |           |           |        |        | end of    |
   |           |           |           |        |        | the value |
   |           |           |           |        |        | field to  |
   |           |           |           |        |        | the       |
   |           |           |           |        |        | beginning |
   |           |           |           |        |        | of the    |
   |           |           |           |        |        | next      |
   |           |           |           |        |        | group.    |
   +-----------+-----------+-----------+--------+--------+-----------+
   | (0        | Affected  | A         | UI     | 1      | The       |
   | 000,0002) | SOP Class | ffectedSO |        |        | affected  |
   |           | UID       | PClassUID |        |        | SOP Class |
   |           |           |           |        |        | UID       |
   |           |           |           |        |        | a         |
   |           |           |           |        |        | ssociated |
   |           |           |           |        |        | with the  |
   |           |           |           |        |        | o         |
   |           |           |           |        |        | peration. |
   +-----------+-----------+-----------+--------+--------+-----------+
   | (0        | Requested | Re        | UI     | 1      | The       |
   | 000,0003) | SOP Class | questedSO |        |        | requested |
   |           | UID       | PClassUID |        |        | SOP Class |
   |           |           |           |        |        | UID       |
   |           |           |           |        |        | a         |
   |           |           |           |        |        | ssociated |
   |           |           |           |        |        | with the  |
   |           |           |           |        |        | o         |
   |           |           |           |        |        | peration. |
   +-----------+-----------+-----------+--------+--------+-----------+
   | (0        | Command   | Com       | US     | 1      | This      |
   | 000,0100) | Field     | mandField |        |        | field     |
   |           |           |           |        |        | dist      |
   |           |           |           |        |        | inguishes |
   |           |           |           |        |        | the DIMSE |
   |           |           |           |        |        | operation |
   |           |           |           |        |        | conveyed  |
   |           |           |           |        |        | by this   |
   |           |           |           |        |        | Message.  |
   |           |           |           |        |        | This      |
   |           |           |           |        |        | field     |
   |           |           |           |        |        | shall be  |
   |           |           |           |        |        | set to    |
   |           |           |           |        |        | one of    |
   |           |           |           |        |        | the       |
   |           |           |           |        |        | following |
   |           |           |           |        |        | values:   |
   |           |           |           |        |        |           |
   |           |           |           |        |        | 0001H     |
   |           |           |           |        |        | C         |
   |           |           |           |        |        | -STORE-RQ |
   |           |           |           |        |        |           |
   |           |           |           |        |        | 8001H     |
   |           |           |           |        |        | C-        |
   |           |           |           |        |        | STORE-RSP |
   |           |           |           |        |        |           |
   |           |           |           |        |        | 0010H     |
   |           |           |           |        |        | C-GET-RQ  |
   |           |           |           |        |        |           |
   |           |           |           |        |        | 8010H     |
   |           |           |           |        |        | C-GET-RSP |
   |           |           |           |        |        |           |
   |           |           |           |        |        | 0020H     |
   |           |           |           |        |        | C-FIND-RQ |
   |           |           |           |        |        |           |
   |           |           |           |        |        | 8020H     |
   |           |           |           |        |        | C         |
   |           |           |           |        |        | -FIND-RSP |
   |           |           |           |        |        |           |
   |           |           |           |        |        | 0021H     |
   |           |           |           |        |        | C-MOVE-RQ |
   |           |           |           |        |        |           |
   |           |           |           |        |        | 8021H     |
   |           |           |           |        |        | C         |
   |           |           |           |        |        | -MOVE-RSP |
   |           |           |           |        |        |           |
   |           |           |           |        |        | 0030H     |
   |           |           |           |        |        | C-ECHO-RQ |
   |           |           |           |        |        |           |
   |           |           |           |        |        | 8030H     |
   |           |           |           |        |        | C         |
   |           |           |           |        |        | -ECHO-RSP |
   |           |           |           |        |        |           |
   |           |           |           |        |        | 0100H     |
   |           |           |           |        |        | N-EVENT-  |
   |           |           |           |        |        | REPORT-RQ |
   |           |           |           |        |        |           |
   |           |           |           |        |        | 8100H     |
   |           |           |           |        |        | N-EVENT-R |
   |           |           |           |        |        | EPORT-RSP |
   |           |           |           |        |        |           |
   |           |           |           |        |        | 0110H     |
   |           |           |           |        |        | N-GET-RQ  |
   |           |           |           |        |        |           |
   |           |           |           |        |        | 8110H     |
   |           |           |           |        |        | N-GET-RSP |
   |           |           |           |        |        |           |
   |           |           |           |        |        | 0120H     |
   |           |           |           |        |        | N-SET-RQ  |
   |           |           |           |        |        |           |
   |           |           |           |        |        | 8120H     |
   |           |           |           |        |        | N-SET-RSP |
   |           |           |           |        |        |           |
   |           |           |           |        |        | 0130H     |
   |           |           |           |        |        | N-        |
   |           |           |           |        |        | ACTION-RQ |
   |           |           |           |        |        |           |
   |           |           |           |        |        | 8130H     |
   |           |           |           |        |        | N-A       |
   |           |           |           |        |        | CTION-RSP |
   |           |           |           |        |        |           |
   |           |           |           |        |        | 0140H     |
   |           |           |           |        |        | N-        |
   |           |           |           |        |        | CREATE-RQ |
   |           |           |           |        |        |           |
   |           |           |           |        |        | 8140H     |
   |           |           |           |        |        | N-C       |
   |           |           |           |        |        | REATE-RSP |
   |           |           |           |        |        |           |
   |           |           |           |        |        | 0150H     |
   |           |           |           |        |        | N-        |
   |           |           |           |        |        | DELETE-RQ |
   |           |           |           |        |        |           |
   |           |           |           |        |        | 8150H     |
   |           |           |           |        |        | N-D       |
   |           |           |           |        |        | ELETE-RSP |
   |           |           |           |        |        |           |
   |           |           |           |        |        | 0FFFH     |
   |           |           |           |        |        | C-        |
   |           |           |           |        |        | CANCEL-RQ |
   +-----------+-----------+-----------+--------+--------+-----------+
   | (0        | Message   | MessageID | US     | 1      | Imple     |
   | 000,0110) | ID        |           |        |        | mentation |
   |           |           |           |        |        | -specific |
   |           |           |           |        |        | value     |
   |           |           |           |        |        | that      |
   |           |           |           |        |        | dist      |
   |           |           |           |        |        | inguishes |
   |           |           |           |        |        | this      |
   |           |           |           |        |        | Message   |
   |           |           |           |        |        | from      |
   |           |           |           |        |        | other     |
   |           |           |           |        |        | Messages. |
   +-----------+-----------+-----------+--------+--------+-----------+
   | (0        | Message   | Message   | US     | 1      | Shall be  |
   | 000,0120) | ID Being  | IDBeingRe |        |        | set to    |
   |           | Responded | spondedTo |        |        | the value |
   |           | To        |           |        |        | of the    |
   |           |           |           |        |        | Message   |
   |           |           |           |        |        | ID        |
   |           |           |           |        |        | (0        |
   |           |           |           |        |        | 000,0110) |
   |           |           |           |        |        | field     |
   |           |           |           |        |        | used in   |
   |           |           |           |        |        | a         |
   |           |           |           |        |        | ssociated |
   |           |           |           |        |        | request   |
   |           |           |           |        |        | Message.  |
   +-----------+-----------+-----------+--------+--------+-----------+
   | (0        | Move      | MoveDe    | AE     | 1      | Shall be  |
   | 000,0600) | De        | stination |        |        | set to    |
   |           | stination |           |        |        | the DICOM |
   |           |           |           |        |        | AE Title  |
   |           |           |           |        |        | of the    |
   |           |           |           |        |        | de        |
   |           |           |           |        |        | stination |
   |           |           |           |        |        | DICOM AE  |
   |           |           |           |        |        | to which  |
   |           |           |           |        |        | the       |
   |           |           |           |        |        | C-STORE   |
   |           |           |           |        |        | sub-o     |
   |           |           |           |        |        | perations |
   |           |           |           |        |        | are being |
   |           |           |           |        |        | p         |
   |           |           |           |        |        | erformed. |
   +-----------+-----------+-----------+--------+--------+-----------+
   | (0        | Priority  | Priority  | US     | 1      | The       |
   | 000,0700) |           |           |        |        | priority  |
   |           |           |           |        |        | shall be  |
   |           |           |           |        |        | set to    |
   |           |           |           |        |        | one of    |
   |           |           |           |        |        | the       |
   |           |           |           |        |        | following |
   |           |           |           |        |        | values:   |
   |           |           |           |        |        |           |
   |           |           |           |        |        | LOW =     |
   |           |           |           |        |        | 0002H     |
   |           |           |           |        |        |           |
   |           |           |           |        |        | MEDIUM =  |
   |           |           |           |        |        | 0000H     |
   |           |           |           |        |        |           |
   |           |           |           |        |        | HIGH =    |
   |           |           |           |        |        | 0001H     |
   +-----------+-----------+-----------+--------+--------+-----------+
   | (0        | Command   | CommandDa | US     | 1      | This      |
   | 000,0800) | Data Set  | taSetType |        |        | field     |
   |           | Type      |           |        |        | indicates |
   |           |           |           |        |        | if a Data |
   |           |           |           |        |        | Set is    |
   |           |           |           |        |        | present   |
   |           |           |           |        |        | in the    |
   |           |           |           |        |        | Message.  |
   |           |           |           |        |        | This      |
   |           |           |           |        |        | field     |
   |           |           |           |        |        | shall be  |
   |           |           |           |        |        | set to    |
   |           |           |           |        |        | the value |
   |           |           |           |        |        | of 0101H  |
   |           |           |           |        |        | if no     |
   |           |           |           |        |        | Data Set  |
   |           |           |           |        |        | is        |
   |           |           |           |        |        | present;  |
   |           |           |           |        |        | any other |
   |           |           |           |        |        | value     |
   |           |           |           |        |        | indicates |
   |           |           |           |        |        | a Data    |
   |           |           |           |        |        | Set is    |
   |           |           |           |        |        | included  |
   |           |           |           |        |        | in the    |
   |           |           |           |        |        | Message.  |
   +-----------+-----------+-----------+--------+--------+-----------+
   | (0        | Status    | Status    | US     | 1      | Con       |
   | 000,0900) |           |           |        |        | firmation |
   |           |           |           |        |        | status of |
   |           |           |           |        |        | the       |
   |           |           |           |        |        | o         |
   |           |           |           |        |        | peration. |
   |           |           |           |        |        | See       |
   |           |           |           |        |        | `Status   |
   |           |           |           |        |        | Type      |
   |           |           |           |        |        | Encoding  |
   |           |           |           |        |        | (         |
   |           |           |           |        |        | Normative |
   |           |           |           |        |        | ) <#chapt |
   |           |           |           |        |        | er_C>`__. |
   +-----------+-----------+-----------+--------+--------+-----------+
   | (0        | Offending | Offendi   | AT     | 1-n    | If status |
   | 000,0901) | Element   | ngElement |        |        | is Cxxx,  |
   |           |           |           |        |        | then this |
   |           |           |           |        |        | field     |
   |           |           |           |        |        | contains  |
   |           |           |           |        |        | a list of |
   |           |           |           |        |        | the       |
   |           |           |           |        |        | elements  |
   |           |           |           |        |        | in which  |
   |           |           |           |        |        | the error |
   |           |           |           |        |        | was       |
   |           |           |           |        |        | detected. |
   +-----------+-----------+-----------+--------+--------+-----------+
   | (0        | Error     | Err       | LO     | 1      | This      |
   | 000,0902) | Comment   | orComment |        |        | field     |
   |           |           |           |        |        | contains  |
   |           |           |           |        |        | an        |
   |           |           |           |        |        | ap        |
   |           |           |           |        |        | plication |
   |           |           |           |        |        | -specific |
   |           |           |           |        |        | text      |
   |           |           |           |        |        | de        |
   |           |           |           |        |        | scription |
   |           |           |           |        |        | of the    |
   |           |           |           |        |        | error     |
   |           |           |           |        |        | detected. |
   +-----------+-----------+-----------+--------+--------+-----------+
   | (0        | Error ID  | ErrorID   | US     | 1      | This      |
   | 000,0903) |           |           |        |        | field     |
   |           |           |           |        |        | shall     |
   |           |           |           |        |        | o         |
   |           |           |           |        |        | ptionally |
   |           |           |           |        |        | contain   |
   |           |           |           |        |        | an        |
   |           |           |           |        |        | ap        |
   |           |           |           |        |        | plication |
   |           |           |           |        |        | -specific |
   |           |           |           |        |        | error     |
   |           |           |           |        |        | code.     |
   +-----------+-----------+-----------+--------+--------+-----------+
   | (0        | Affected  | Affe      | UI     | 1      | Contains  |
   | 000,1000) | SOP       | ctedSOPIn |        |        | the UID   |
   |           | Instance  | stanceUID |        |        | of the    |
   |           | UID       |           |        |        | SOP       |
   |           |           |           |        |        | Instance  |
   |           |           |           |        |        | for which |
   |           |           |           |        |        | this      |
   |           |           |           |        |        | operation |
   |           |           |           |        |        | occurred. |
   +-----------+-----------+-----------+--------+--------+-----------+
   | (0        | Requested | Reque     | UI     | 1      | Contains  |
   | 000,1001) | SOP       | stedSOPIn |        |        | the UID   |
   |           | Instance  | stanceUID |        |        | of the    |
   |           | UID       |           |        |        | SOP       |
   |           |           |           |        |        | Instance  |
   |           |           |           |        |        | for which |
   |           |           |           |        |        | this      |
   |           |           |           |        |        | operation |
   |           |           |           |        |        | occurred. |
   +-----------+-----------+-----------+--------+--------+-----------+
   | (0        | Event     | Ev        | US     | 1      | Values    |
   | 000,1002) | Type ID   | entTypeID |        |        | for this  |
   |           |           |           |        |        | field are |
   |           |           |           |        |        | app       |
   |           |           |           |        |        | lication- |
   |           |           |           |        |        | specific. |
   +-----------+-----------+-----------+--------+--------+-----------+
   | (0        | Attribute | Attri     | AT     | 1-n    | This      |
   | 000,1005) | I         | buteIdent |        |        | field     |
   |           | dentifier | ifierList |        |        | contains  |
   |           | List      |           |        |        | an        |
   |           |           |           |        |        | Attribute |
   |           |           |           |        |        | Tag for   |
   |           |           |           |        |        | each of   |
   |           |           |           |        |        | the n     |
   |           |           |           |        |        | A         |
   |           |           |           |        |        | ttributes |
   |           |           |           |        |        | ap        |
   |           |           |           |        |        | plicable. |
   +-----------+-----------+-----------+--------+--------+-----------+
   | (0        | Action    | Act       | US     | 1      | Values    |
   | 000,1008) | Type ID   | ionTypeID |        |        | for this  |
   |           |           |           |        |        | field are |
   |           |           |           |        |        | app       |
   |           |           |           |        |        | lication- |
   |           |           |           |        |        | specific. |
   +-----------+-----------+-----------+--------+--------+-----------+
   | (0        | Number of | Num       | US     | 1      | The       |
   | 000,1020) | Remaining | berOfRema |        |        | number of |
   |           | Sub-o     | iningSubo |        |        | remaining |
   |           | perations | perations |        |        | C-STORE   |
   |           |           |           |        |        | sub-o     |
   |           |           |           |        |        | perations |
   |           |           |           |        |        | to be     |
   |           |           |           |        |        | invoked   |
   |           |           |           |        |        | for the   |
   |           |           |           |        |        | o         |
   |           |           |           |        |        | peration. |
   +-----------+-----------+-----------+--------+--------+-----------+
   | (0        | Number of | Num       | US     | 1      | The       |
   | 000,1021) | Completed | berOfComp |        |        | number of |
   |           | Sub-o     | letedSubo |        |        | C-STORE   |
   |           | perations | perations |        |        | sub-o     |
   |           |           |           |        |        | perations |
   |           |           |           |        |        | a         |
   |           |           |           |        |        | ssociated |
   |           |           |           |        |        | with this |
   |           |           |           |        |        | operation |
   |           |           |           |        |        | that have |
   |           |           |           |        |        | completed |
   |           |           |           |        |        | succ      |
   |           |           |           |        |        | essfully. |
   +-----------+-----------+-----------+--------+--------+-----------+
   | (0        | Number of | NumberOfF | US     | 1      | The       |
   | 000,1022) | Failed    | ailedSubo |        |        | number of |
   |           | Sub-o     | perations |        |        | C-STORE   |
   |           | perations |           |        |        | sub-o     |
   |           |           |           |        |        | perations |
   |           |           |           |        |        | a         |
   |           |           |           |        |        | ssociated |
   |           |           |           |        |        | with this |
   |           |           |           |        |        | operation |
   |           |           |           |        |        | that have |
   |           |           |           |        |        | failed.   |
   +-----------+-----------+-----------+--------+--------+-----------+
   | (0        | Number of | N         | US     | 1      | The       |
   | 000,1023) | Warning   | umberOfWa |        |        | number of |
   |           | Sub-o     | rningSubo |        |        | C-STORE   |
   |           | perations | perations |        |        | sub-o     |
   |           |           |           |        |        | perations |
   |           |           |           |        |        | a         |
   |           |           |           |        |        | ssociated |
   |           |           |           |        |        | with this |
   |           |           |           |        |        | operation |
   |           |           |           |        |        | that      |
   |           |           |           |        |        | generated |
   |           |           |           |        |        | warning   |
   |           |           |           |        |        | r         |
   |           |           |           |        |        | esponses. |
   +-----------+-----------+-----------+--------+--------+-----------+
   | (0        | Move      | MoveOrigi | AE     | 1      | Contains  |
   | 000,1030) | O         | natorAppl |        |        | the DICOM |
   |           | riginator | icationEn |        |        | AE Title  |
   |           | Ap        | tityTitle |        |        | of the    |
   |           | plication |           |        |        | DICOM AE  |
   |           | Entity    |           |        |        | that      |
   |           | Title     |           |        |        | invoked   |
   |           |           |           |        |        | the       |
   |           |           |           |        |        | C-MOVE    |
   |           |           |           |        |        | operation |
   |           |           |           |        |        | from      |
   |           |           |           |        |        | which     |
   |           |           |           |        |        | this      |
   |           |           |           |        |        | C-STORE   |
   |           |           |           |        |        | sub-      |
   |           |           |           |        |        | operation |
   |           |           |           |        |        | is being  |
   |           |           |           |        |        | p         |
   |           |           |           |        |        | erformed. |
   +-----------+-----------+-----------+--------+--------+-----------+
   | (0        | Move      | MoveO     | US     | 1      | Contains  |
   | 000,1031) | O         | riginator |        |        | the       |
   |           | riginator | MessageID |        |        | Message   |
   |           | Message   |           |        |        | ID        |
   |           | ID        |           |        |        | (0        |
   |           |           |           |        |        | 000,0110) |
   |           |           |           |        |        | of the    |
   |           |           |           |        |        | C-MOVE-RQ |
   |           |           |           |        |        | Message   |
   |           |           |           |        |        | from      |
   |           |           |           |        |        | which     |
   |           |           |           |        |        | this      |
   |           |           |           |        |        | C-STORE   |
   |           |           |           |        |        | sub-      |
   |           |           |           |        |        | operation |
   |           |           |           |        |        | is being  |
   |           |           |           |        |        | p         |
   |           |           |           |        |        | erformed. |
   +-----------+-----------+-----------+--------+--------+-----------+

.. _sect_E.2:

Retired Command Fields
----------------------

The following command fields have been retired but are listed here for
compatibility with previous versions of this Standard. Reference for
more information on retired Data Elements and Command Elements.

.. table:: Retired Command Fields

   +-------------+----------------+----------------+--------+--------+
   | **Tag**     | **Message      | **Keyword**    | **VR** | **VM** |
   |             | Field**        |                |        |        |
   +=============+================+================+========+========+
   | (0000,0001) | Command Length | Comm           | UL     | 1      |
   |             | to End         | andLengthToEnd |        |        |
   +-------------+----------------+----------------+--------+--------+
   | (0000,0010) | Command        | CommandR       | SH     | 1      |
   |             | Recognition    | ecognitionCode |        |        |
   |             | Code           |                |        |        |
   +-------------+----------------+----------------+--------+--------+
   | (0000,0200) | Initiator      | Initiator      | AE     | 1      |
   +-------------+----------------+----------------+--------+--------+
   | (0000,0300) | Receiver       | Receiver       | AE     | 1      |
   +-------------+----------------+----------------+--------+--------+
   | (0000,0400) | Find Location  | FindLocation   | AE     | 1      |
   +-------------+----------------+----------------+--------+--------+
   | (0000,0850) | Number of      | N              | US     | 1      |
   |             | Matches        | umberOfMatches |        |        |
   +-------------+----------------+----------------+--------+--------+
   | (0000,0860) | Response       | Response       | US     | 1      |
   |             | Sequence       | SequenceNumber |        |        |
   |             | Number         |                |        |        |
   +-------------+----------------+----------------+--------+--------+
   | (0000,4000) | Dialog         | DialogReceiver | LT     | 1      |
   |             | Receiver       |                |        |        |
   +-------------+----------------+----------------+--------+--------+
   | (0000,4010) | Terminal Type  | TerminalType   | LT     | 1      |
   +-------------+----------------+----------------+--------+--------+
   | (0000,5010) | Message Set ID | MessageSetID   | SH     | 1      |
   +-------------+----------------+----------------+--------+--------+
   | (0000,5020) | End Message ID | EndMessageID   | SH     | 1      |
   +-------------+----------------+----------------+--------+--------+
   | (0000,5110) | Display Format | DisplayFormat  | LT     | 1      |
   +-------------+----------------+----------------+--------+--------+
   | (0000,5120) | Page Position  | PagePositionID | LT     | 1      |
   |             | ID             |                |        |        |
   +-------------+----------------+----------------+--------+--------+
   | (0000,5130) | Text Format ID | TextFormatID   | CS     | 1      |
   +-------------+----------------+----------------+--------+--------+
   | (0000,5140) | Normal/Reverse | NormalReverse  | CS     | 1      |
   +-------------+----------------+----------------+--------+--------+
   | (0000,5150) | Add Gray Scale | AddGrayScale   | CS     | 1      |
   +-------------+----------------+----------------+--------+--------+
   | (0000,5160) | Borders        | Borders        | CS     | 1      |
   +-------------+----------------+----------------+--------+--------+
   | (0000,5170) | Copies         | Copies         | IS     | 1      |
   +-------------+----------------+----------------+--------+--------+
   | (0000,5180) | Command        | CommandMag     | CS     | 1      |
   |             | Magnification  | nificationType |        |        |
   |             | Type           |                |        |        |
   +-------------+----------------+----------------+--------+--------+
   | (0000,5190) | Erase          | Erase          | CS     | 1      |
   +-------------+----------------+----------------+--------+--------+
   | (0000,51A0) | Print          | Print          | CS     | 1      |
   +-------------+----------------+----------------+--------+--------+
   | (0000,51B0) | Overlays       | Overlays       | US     | 1-n    |
   +-------------+----------------+----------------+--------+--------+

.. note::

   For attributes that were present in ACR-NEMA 1.0 and 2.0 and that
   have been retired, the specifications of Value Representation and
   Value Multiplicity provided are recommendations for the purpose of
   interpreting their values in objects created in accordance with
   earlier editions of this Standard. These recommendations are
   suggested as most appropriate for a particular attribute; however,
   there is no guarantee that historical objects will not violate some
   requirements or specified VR and/or VM.

