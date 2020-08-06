.. _chapter_8:

Header Content Templates
========================

.. _sect_8.1:

General Header
--------------

+----------------------+----------------------------------------------+
| **Template ID**      | 1.2.840.10008.9.20                           |
+----------------------+----------------------------------------------+
| **Name**             | General Header Elements                      |
+----------------------+----------------------------------------------+
| **Effective Date**   | 2015/03/24                                   |
+----------------------+----------------------------------------------+
| **Version Label**    | DICOM-20150324                               |
+----------------------+----------------------------------------------+
| **Status**           | Active                                       |
+----------------------+----------------------------------------------+
| **Description**      | CDA Header Elements for all documents,       |
|                      | including primary participations             |
+----------------------+----------------------------------------------+
| **Classification**   | CDA Header Elements                          |
+----------------------+----------------------------------------------+
| **Relationships**    | Included in all document level templates     |
+----------------------+----------------------------------------------+
| **Context**          | sibling node                                 |
+----------------------+----------------------------------------------+
| **Open/Closed**      | Open                                         |
+----------------------+----------------------------------------------+
| **Revision History** | DICOM-20150324: Initial version              |
+----------------------+----------------------------------------------+

+-------+-------+-------+-------+-------+-------+-------+-------+-------+
| Bus   | Nest  | Ele   | Card  | Elem  | Data  | Value | Value | Subsi |
| iness | Level | ment/ |       | /Attr | Type  | Conf  |       | diary |
| Name  |       | ​Attr |       | Conf  |       |       |       | Tem   |
|       |       | ibute |       |       |       |       |       | plate |
+=======+=======+=======+=======+=======+=======+=======+=======+=======+
|       |       | t     | 1..1  | SHALL | II    |       |       |       |
|       |       | empla |       |       |       |       |       |       |
|       |       | te​Id |       |       |       |       |       |       |
+-------+-------+-------+-------+-------+-------+-------+-------+-------+
|       | @     | @root | 1..1  | SHALL | UID   | SHALL | 1.2   |       |
|       |       |       |       |       |       |       | .840. |       |
|       |       |       |       |       |       |       | 10008 |       |
|       |       |       |       |       |       |       | .9.20 |       |
+-------+-------+-------+-------+-------+-------+-------+-------+-------+
| C     |       | t     | 0..\* | MAY   | II    |       |       |       |
| onten |       | empla |       |       |       |       |       |       |
| t​Tem |       | te​Id |       |       |       |       |       |       |
| plate |       |       |       |       |       |       |       |       |
+-------+-------+-------+-------+-------+-------+-------+-------+-------+
|       |       | ty    | 1..1  | SHALL | II    |       |       |       |
|       |       | pe​Id |       |       |       |       |       |       |
+-------+-------+-------+-------+-------+-------+-------+-------+-------+
|       | @     | @root | 1..1  | SHALL | UID   | SHALL | 2.    |       |
|       |       |       |       |       |       |       | 16.84 |       |
|       |       |       |       |       |       |       | 0.1.1 |       |
|       |       |       |       |       |       |       | 13883 |       |
|       |       |       |       |       |       |       | .​1.3 |       |
+-------+-------+-------+-------+-------+-------+-------+-------+-------+
|       | @     | @exte | 1..1  | SHALL | ST    | SHALL | POC   |       |
|       |       | nsion |       |       |       |       | D_HD0 |       |
|       |       |       |       |       |       |       | 00040 |       |
+-------+-------+-------+-------+-------+-------+-------+-------+-------+
|       |       | id    | 1..1  | SHALL | II    |       |       |       |
+-------+-------+-------+-------+-------+-------+-------+-------+-------+
| Title |       | title | 1..1  | SHALL | ST    |       |       |       |
+-------+-------+-------+-------+-------+-------+-------+-------+-------+
| Cre   |       | effe  | 1..1  | SHALL | TS    |       |       |       |
| ation |       | ctive |       |       |       |       |       |       |
| ​Time |       | ​Time |       |       |       |       |       |       |
+-------+-------+-------+-------+-------+-------+-------+-------+-------+
| Confi |       | confi | 1..1  | SHALL | CE    | SHALL | Val   |       |
| denti |       | denti |       |       |       | CWE   | ueSet |       |
| ality |       | ality |       |       |       |       | 2     |       |
|       |       | ​Code |       |       |       |       | .16.8 |       |
|       |       |       |       |       |       |       | 40.1. |       |
|       |       |       |       |       |       |       | 11388 |       |
|       |       |       |       |       |       |       | 3.11. |       |
|       |       |       |       |       |       |       | 16926 |       |
+-------+-------+-------+-------+-------+-------+-------+-------+-------+
| Lan   |       | lan   | 1..1  | SHALL | CS    | SHALL | Val   |       |
| guage |       | guage |       |       |       | CNE   | ueSet |       |
| ​Code |       | ​Code |       |       |       |       |       |       |
+-------+-------+-------+-------+-------+-------+-------+-------+-------+
| S     |       | s     | 0..1  | MAY   | II    |       |       |       |
| et​Id |       | et​Id |       |       |       |       |       |       |
+-------+-------+-------+-------+-------+-------+-------+-------+-------+
| Vers  |       | vers  | 1..1  | COND  | INT   |       |       |       |
| ion​N |       | ion​N |       |       |       |       |       |       |
| umber |       | umber |       |       |       |       |       |       |
+-------+-------+-------+-------+-------+-------+-------+-------+-------+
| **Pa  |       | rec   | 1..\* | SHALL |       |       |       |       |
| tient |       | ord​T |       |       |       |       |       |       |
| [*]** |       | arget |       |       |       |       |       |       |
+-------+-------+-------+-------+-------+-------+-------+-------+-------+
|       | >     | pa    | 1..1  | SHALL |       |       |       |       |
|       |       | tient |       |       |       |       |       |       |
|       |       | ​Role |       |       |       |       |       |       |
+-------+-------+-------+-------+-------+-------+-------+-------+-------+
|       | >>    | id    | 1..\* | SHALL | II    |       |       |       |
+-------+-------+-------+-------+-------+-------+-------+-------+-------+
| IDI   | >>@   | root  | 1..1  | SHALL | UID   |       | *I    |       |
| ssuer |       |       |       |       |       |       | ssuer |       |
|       |       |       |       |       |       |       | of    |       |
|       |       |       |       |       |       |       | Pa    |       |
|       |       |       |       |       |       |       | tient |       |
|       |       |       |       |       |       |       | ID    |       |
|       |       |       |       |       |       |       | Quali |       |
|       |       |       |       |       |       |       | fiers |       |
|       |       |       |       |       |       |       | Seq   |       |
|       |       |       |       |       |       |       | uence |       |
|       |       |       |       |       |       |       | (     |       |
|       |       |       |       |       |       |       | 0010, |       |
|       |       |       |       |       |       |       | 0024) |       |
|       |       |       |       |       |       |       | >     |       |
|       |       |       |       |       |       |       | Univ  |       |
|       |       |       |       |       |       |       | ersal |       |
|       |       |       |       |       |       |       | E     |       |
|       |       |       |       |       |       |       | ntity |       |
|       |       |       |       |       |       |       | ID    |       |
|       |       |       |       |       |       |       | (0    |       |
|       |       |       |       |       |       |       | 040,0 |       |
|       |       |       |       |       |       |       | 032)* |       |
|       |       |       |       |       |       |       |       |       |
|       |       |       |       |       |       |       | *Pa   |       |
|       |       |       |       |       |       |       | tient |       |
|       |       |       |       |       |       |       | ID    |       |
|       |       |       |       |       |       |       | List  |       |
|       |       |       |       |       |       |       | PID-3 |       |
|       |       |       |       |       |       |       | .4.2* |       |
+-------+-------+-------+-------+-------+-------+-------+-------+-------+
| ID    | >>@   | exte  | 1..1  | SHALL | ST    |       | *Pa   |       |
|       |       | nsion |       |       |       |       | tient |       |
|       |       |       |       |       |       |       | ID    |       |
|       |       |       |       |       |       |       | (0    |       |
|       |       |       |       |       |       |       | 010,0 |       |
|       |       |       |       |       |       |       | 020)* |       |
|       |       |       |       |       |       |       |       |       |
|       |       |       |       |       |       |       | *Pa   |       |
|       |       |       |       |       |       |       | tient |       |
|       |       |       |       |       |       |       | ID    |       |
|       |       |       |       |       |       |       | List  |       |
|       |       |       |       |       |       |       | PID   |       |
|       |       |       |       |       |       |       | -3.1* |       |
+-------+-------+-------+-------+-------+-------+-------+-------+-------+
| Addr  | >>    | addr  | 1..\* | SHALL | AD    |       |       |       |
+-------+-------+-------+-------+-------+-------+-------+-------+-------+
| Tele  | >>    | te    | 1..\* | SHALL | TEL   |       |       |       |
|       |       | lecom |       |       |       |       |       |       |
+-------+-------+-------+-------+-------+-------+-------+-------+-------+
|       | >>    | pa    | 1..1  | SHALL |       |       |       |       |
|       |       | tient |       |       |       |       |       |       |
+-------+-------+-------+-------+-------+-------+-------+-------+-------+
| Name  | >>>   | name  | 1..1  | SHALL | PN    |       | *Pati |       |
|       |       |       |       |       |       |       | ent's |       |
|       |       |       |       |       |       |       | Name  |       |
|       |       |       |       |       |       |       | (0    |       |
|       |       |       |       |       |       |       | 010,0 |       |
|       |       |       |       |       |       |       | 010)* |       |
|       |       |       |       |       |       |       |       |       |
|       |       |       |       |       |       |       | *Pa   |       |
|       |       |       |       |       |       |       | tient |       |
|       |       |       |       |       |       |       | Name  |       |
|       |       |       |       |       |       |       | P     |       |
|       |       |       |       |       |       |       | ID-5* |       |
+-------+-------+-------+-------+-------+-------+-------+-------+-------+
| G     | >>>   | a     | 1..1  | SHALL | CE    | SHALL | Val   |       |
| ender |       | dmini |       |       |       | CNE   | ueSet |       |
|       |       | strat |       |       |       |       | 2.    |       |
|       |       | ive​G |       |       |       |       | 16.84 |       |
|       |       | ender |       |       |       |       | 0.1.1 |       |
|       |       | ​Code |       |       |       |       | 13883 |       |
|       |       |       |       |       |       |       | .11.1 |       |
|       |       |       |       |       |       |       |       |       |
|       |       |       |       |       |       |       | *Pati |       |
|       |       |       |       |       |       |       | ent's |       |
|       |       |       |       |       |       |       | Sex   |       |
|       |       |       |       |       |       |       | (00   |       |
|       |       |       |       |       |       |       | 10,00 |       |
|       |       |       |       |       |       |       | 40);* |       |
|       |       |       |       |       |       |       | [Map  |       |
|       |       |       |       |       |       |       | value |       |
|       |       |       |       |       |       |       | "O"   |       |
|       |       |       |       |       |       |       | to    |       |
|       |       |       |       |       |       |       | nullF |       |
|       |       |       |       |       |       |       | lavor |       |
|       |       |       |       |       |       |       | UNK]  |       |
|       |       |       |       |       |       |       |       |       |
|       |       |       |       |       |       |       | *Admi |       |
|       |       |       |       |       |       |       | nistr |       |
|       |       |       |       |       |       |       | ative |       |
|       |       |       |       |       |       |       | Sex   |       |
|       |       |       |       |       |       |       | PID   |       |
|       |       |       |       |       |       |       | -3.8* |       |
+-------+-------+-------+-------+-------+-------+-------+-------+-------+
| Birth | >>>   | birth | 1..1  | SHALL | TS    |       | *Pati |       |
| ​Time |       | ​Time |       |       |       |       | ent's |       |
|       |       |       |       |       |       |       | Birth |       |
|       |       |       |       |       |       |       | Date  |       |
|       |       |       |       |       |       |       | (     |       |
|       |       |       |       |       |       |       | 0010, |       |
|       |       |       |       |       |       |       | 0030) |       |
|       |       |       |       |       |       |       | +     |       |
|       |       |       |       |       |       |       | Pati  |       |
|       |       |       |       |       |       |       | ent's |       |
|       |       |       |       |       |       |       | Birth |       |
|       |       |       |       |       |       |       | Time  |       |
|       |       |       |       |       |       |       | (0    |       |
|       |       |       |       |       |       |       | 010,0 |       |
|       |       |       |       |       |       |       | 032)* |       |
|       |       |       |       |       |       |       |       |       |
|       |       |       |       |       |       |       | *Date |       |
|       |       |       |       |       |       |       | /Time |       |
|       |       |       |       |       |       |       | of    |       |
|       |       |       |       |       |       |       | Birth |       |
|       |       |       |       |       |       |       | P     |       |
|       |       |       |       |       |       |       | ID-7* |       |
+-------+-------+-------+-------+-------+-------+-------+-------+-------+
|       | >>    | p     | 0..1  | MAY   |       |       |       |       |
|       |       | rovid |       |       |       |       |       |       |
|       |       | er​Or |       |       |       |       |       |       |
|       |       | ganiz |       |       |       |       |       |       |
|       |       | ation |       |       |       |       |       |       |
+-------+-------+-------+-------+-------+-------+-------+-------+-------+
| Pr    | >>>   | name  | 1..\* | SHALL | ON    |       | *I    |       |
| ovide |       |       |       |       |       |       | ssuer |       |
| r​Org |       |       |       |       |       |       | of    |       |
| ​Name |       |       |       |       |       |       | Pa    |       |
|       |       |       |       |       |       |       | tient |       |
|       |       |       |       |       |       |       | ID    |       |
|       |       |       |       |       |       |       | (0    |       |
|       |       |       |       |       |       |       | 010,0 |       |
|       |       |       |       |       |       |       | 021)* |       |
+-------+-------+-------+-------+-------+-------+-------+-------+-------+
| P     | >>>   | te    | 0..\* | S     | TEL   |       |       |       |
| rovid |       | lecom |       | HOULD |       |       |       |       |
| er​Or |       |       |       |       |       |       |       |       |
| g​Tel |       |       |       |       |       |       |       |       |
+-------+-------+-------+-------+-------+-------+-------+-------+-------+
| Pr    | >>>   | addr  | 0..\* | S     | AD    |       |       |       |
| ovide |       |       |       | HOULD |       |       |       |       |
| r​Org |       |       |       |       |       |       |       |       |
| ​Addr |       |       |       |       |       |       |       |       |
+-------+-------+-------+-------+-------+-------+-------+-------+-------+
|       |       | lega  | 0..1  | MAY   |       |       |       |       |
|       |       | l​Aut |       |       |       |       |       |       |
|       |       | henti |       |       |       |       |       |       |
|       |       | cator |       |       |       |       |       |       |
+-------+-------+-------+-------+-------+-------+-------+-------+-------+
| Si    | >     | time  | 1..1  | SHALL | TS    |       |       |       |
| gning |       |       |       |       |       |       |       |       |
| ​Time |       |       |       |       |       |       |       |       |
+-------+-------+-------+-------+-------+-------+-------+-------+-------+
|       | >     | sign  | 1..1  | SHALL | CS    | SHALL | S     |       |
|       |       | ature |       |       |       |       |       |       |
|       |       | ​Code |       |       |       |       |       |       |
+-------+-------+-------+-------+-------+-------+-------+-------+-------+
|       | >     | assig | 1..1  | SHALL |       |       |       |       |
|       |       | ned​E |       |       |       |       |       |       |
|       |       | ntity |       |       |       |       |       |       |
+-------+-------+-------+-------+-------+-------+-------+-------+-------+
| Sign  | >>    | id    | 1.\*  | SHALL | II    |       |       |       |
| er​ID |       |       |       |       |       |       |       |       |
+-------+-------+-------+-------+-------+-------+-------+-------+-------+
| S     | >>    | addr  | 1.\*  | SHALL | AD    |       |       |       |
| igner |       |       |       |       |       |       |       |       |
| ​Addr |       |       |       |       |       |       |       |       |
+-------+-------+-------+-------+-------+-------+-------+-------+-------+
| Signe | >>    | te    | 1..\* | SHALL | TEL   |       |       |       |
| r​Tel |       | lecom |       |       |       |       |       |       |
+-------+-------+-------+-------+-------+-------+-------+-------+-------+
|       | >>    | assig | 1..1  | SHALL |       |       |       |       |
|       |       | ned​P |       |       |       |       |       |       |
|       |       | erson |       |       |       |       |       |       |
+-------+-------+-------+-------+-------+-------+-------+-------+-------+
| S     | >>>   | name  | 1..1  | SHALL | PN    |       |       |       |
| igner |       |       |       |       |       |       |       |       |
| ​Name |       |       |       |       |       |       |       |       |
+-------+-------+-------+-------+-------+-------+-------+-------+-------+
| Signa | >     | sdt   | 0..1  | MAY   | ED    |       |       |       |
| ture​ |       | c:sig |       |       |       |       |       |       |
| Block |       | natur |       |       |       |       |       |       |
|       |       | eText |       |       |       |       |       |       |
+-------+-------+-------+-------+-------+-------+-------+-------+-------+
| **A   |       | a     | 1..\* | SHALL |       |       |       |       |
| uthor |       | uthor |       |       |       |       |       |       |
| [*]** |       |       |       |       |       |       |       |       |
+-------+-------+-------+-------+-------+-------+-------+-------+-------+
| Auth  | >     | time  | 1..1  | SHALL | TS    |       |       |       |
| oring |       |       |       |       |       |       |       |       |
| ​Time |       |       |       |       |       |       |       |       |
+-------+-------+-------+-------+-------+-------+-------+-------+-------+
|       | >     | assig | 1..1  | SHALL |       |       |       |       |
|       |       | ned​A |       |       |       |       |       |       |
|       |       | uthor |       |       |       |       |       |       |
+-------+-------+-------+-------+-------+-------+-------+-------+-------+
|       | >>    | id    | 1.\*  | SHALL | II    |       |       |       |
+-------+-------+-------+-------+-------+-------+-------+-------+-------+
| Addr  | >>    | addr  | 1.\*  | SHALL | AD    |       |       |       |
+-------+-------+-------+-------+-------+-------+-------+-------+-------+
| Tel   | >>    | te    | 1..\* | SHALL | TEL   |       |       |       |
|       |       | lecom |       |       |       |       |       |       |
+-------+-------+-------+-------+-------+-------+-------+-------+-------+
|       | >>    | assig | 1..1  | SHALL |       |       |       |       |
|       |       | ned​P |       |       |       |       |       |       |
|       |       | erson |       |       |       |       |       |       |
+-------+-------+-------+-------+-------+-------+-------+-------+-------+
| Name  | >>>   | name  | 1..1  | SHALL | PN    |       |       |       |
+-------+-------+-------+-------+-------+-------+-------+-------+-------+
| *     |       | i     | 0..\* | MAY   |       |       |       |       |
| *Reci |       | nform |       |       |       |       |       |       |
| pient |       | ation |       |       |       |       |       |       |
| [*]** |       | ​Reci |       |       |       |       |       |       |
|       |       | pient |       |       |       |       |       |       |
+-------+-------+-------+-------+-------+-------+-------+-------+-------+
|       | >     | int   | 1..1  | SHALL |       |       |       |       |
|       |       | ended |       |       |       |       |       |       |
|       |       | ​Reci |       |       |       |       |       |       |
|       |       | pient |       |       |       |       |       |       |
+-------+-------+-------+-------+-------+-------+-------+-------+-------+
|       | >@    | @clas | 1..1  | SHALL | CS    | SHALL | ASS   |       |
|       |       | sCode |       |       |       |       | IGNED |       |
+-------+-------+-------+-------+-------+-------+-------+-------+-------+
| Addr  | >>    | addr  | 0.\*  | MAY   | AD    |       |       |       |
+-------+-------+-------+-------+-------+-------+-------+-------+-------+
| Tel   | >>    | te    | 0..\* | MAY   | TEL   |       |       |       |
|       |       | lecom |       |       |       |       |       |       |
+-------+-------+-------+-------+-------+-------+-------+-------+-------+
|       | >>    | i     | 0..1  | MAY   |       |       |       |       |
|       |       | nform |       |       |       |       |       |       |
|       |       | ation |       |       |       |       |       |       |
|       |       | ​Reci |       |       |       |       |       |       |
|       |       | pient |       |       |       |       |       |       |
+-------+-------+-------+-------+-------+-------+-------+-------+-------+
| Name  | >>>   | name  | 1..1  | SHALL | PN    |       |       |       |
+-------+-------+-------+-------+-------+-------+-------+-------+-------+
|       | >>    | r     | 0..1  | MAY   |       |       |       |       |
|       |       | eceiv |       |       |       |       |       |       |
|       |       | ed​Or |       |       |       |       |       |       |
|       |       | ganiz |       |       |       |       |       |       |
|       |       | ation |       |       |       |       |       |       |
+-------+-------+-------+-------+-------+-------+-------+-------+-------+
| Org   | >>>   | name  | 1..1  | SHALL | ON    |       |       |       |
+-------+-------+-------+-------+-------+-------+-------+-------+-------+
|       |       | cust  | 1..1  | SHALL |       |       |       |       |
|       |       | odian |       |       |       |       |       |       |
+-------+-------+-------+-------+-------+-------+-------+-------+-------+
|       | >     | ass   | 1..1  | SHALL |       |       |       |       |
|       |       | igned |       |       |       |       |       |       |
|       |       | ​Cust |       |       |       |       |       |       |
|       |       | odian |       |       |       |       |       |       |
+-------+-------+-------+-------+-------+-------+-------+-------+-------+
|       | >>    | repr  | 1..1  | SHALL |       |       |       |       |
|       |       | esent |       |       |       |       |       |       |
|       |       | ed​Cu |       |       |       |       |       |       |
|       |       | stodi |       |       |       |       |       |       |
|       |       | an​Or |       |       |       |       |       |       |
|       |       | ganiz |       |       |       |       |       |       |
|       |       | ation |       |       |       |       |       |       |
+-------+-------+-------+-------+-------+-------+-------+-------+-------+
| C     | >>>   | id    | 1.\*  | SHALL | II    |       |       |       |
| ustod |       |       |       |       |       |       |       |       |
| ian​O |       |       |       |       |       |       |       |       |
| rg​ID |       |       |       |       |       |       |       |       |
+-------+-------+-------+-------+-------+-------+-------+-------+-------+
| Cus   | >>>   | name  | 1..1  | SHALL | ON    |       |       |       |
| todia |       |       |       |       |       |       |       |       |
| n​Org |       |       |       |       |       |       |       |       |
| ​Name |       |       |       |       |       |       |       |       |
+-------+-------+-------+-------+-------+-------+-------+-------+-------+
| Cus   | >>>   | addr  | 1..1  | SHALL | AD    |       |       |       |
| todia |       |       |       |       |       |       |       |       |
| n​Org |       |       |       |       |       |       |       |       |
| ​Addr |       |       |       |       |       |       |       |       |
+-------+-------+-------+-------+-------+-------+-------+-------+-------+
| Cu    | >>>   | te    | 1..1  | SHALL | TEL   |       |       |       |
| stodi |       | lecom |       |       |       |       |       |       |
| an​Or |       |       |       |       |       |       |       |       |
| g​Tel |       |       |       |       |       |       |       |       |
+-------+-------+-------+-------+-------+-------+-------+-------+-------+

Note that there is no business name associated with this template.
Rather, this template is an editorial convenience for template
specification, and the Business Names for the elements of this template
are logically part of the business name scope of the invoking template.

.. _sect_8.1.1:

templateId - contentTemplate
~~~~~~~~~~~~~~~~~~~~~~~~~~~~

This templateId may be used to identify the template(s) used to
generate/constrain the content of the report. This element is in
addition to the templateId of the document level template, and typically
represents clinical sub-specialty requirements. See `Template IDs and
Version <#sect_5.1.1>`__ on the structure and use of the templateId.

.. note::

   The IHE MRRT profile defines a "dcterms.identifier" that may be used
   for this templateId.

.. _sect_8.1.2:

title
~~~~~

The title may include the title of the report template used.

.. note::

   The IHE MRRT profile defines a "dcterms.title" that may be used in
   this element.

.. _sect_8.1.3:

effectiveTime
~~~~~~~~~~~~~

The effectiveTime signifies the document creation time, when the
document first came into being. Where the CDA document is a transform
from an original document in some other format, the
ClinicalDocument.effectiveTime is the time the original document is
created. The time when the transform occurred is not represented in CDA.

.. _sect_8.1.4:

setID and versionNumber
~~~~~~~~~~~~~~~~~~~~~~~

The setID and versionNumber elements may be used by the document
creation system to manage document revisions, in accordance with the CDA
specification sections 4.2.1.7 and 4.2.1.8.

COND: If and only if the setID element is present, the versionNumber
element SHALL be present.

.. _sect_8.1.5:

recordTarget/patientRole
~~~~~~~~~~~~~~~~~~~~~~~~

The recordTarget records the patient whose health information is
described by the clinical document; it must contain at least one
patientRole element.

Multiple recordTarget elements should be used only in the case of
conjoined twins/triplets who are the subject of a single imaging
procedure, or for special cases (e.g., pre-natal surgery, where a
medical record has been established for the fetus).

::

   <typeId root="2.16.840.1.113883.1.3" extension="POCD_HD000040"/>
   <!-- DICOM Imaging Report Template -->
   <templateId root="1.2.840.10008.9.1"/>
   <!-- General Header Template -->
   <templateId root="1.2.840.10008.9.20"/>
   <id extension="999021" root="2.16.840.1.113883.19"/>
   <code codeSystem="2.16.840.1.113883.6.1"
       codeSystemName="LOINC" code="18748-4"
       displayName="Diagnostic Imaging Report"/>
   <title>Radiology Report</title>
   <effectiveTime value="20150329171504+0500"/>
   <confidentialityCode code="N" codeSystem="2.16.840.1.113883.5.25"/>
   <languageCode code="en-US" codeSystem="2.16.840.1.113883.6.121"/>
   <setId extension="111199021" root="2.16.840.1.113883.19"/>
   <versionNumber value="1"/>

.. _sect_8.1.6:

legalAuthenticator
~~~~~~~~~~~~~~~~~~

The legalAuthenticator identifies the single person legally responsible
for the correctness of the content of the document and SHALL be present
if the document has been legally authenticated. In the context of an
imaging report, this means the radiologist, cardiologist, or other
professional who signed or validated the report.

.. note::

   Per the CDA Standard, the legal authenticator, if present, must be a
   person, and the authentication applies to the human-readable
   narrative in section/text and any renderMultiMedia referenced
   content. Structured entries and external images referenced through
   linkHtml are not attested by the legal authentication.

Based on local practice, clinical documents may be released before legal
authentication. This implies that a clinical document that does not
contain this element has not been legally authenticated.

The legalAuthenticator SHALL contain exactly one [1..1] time
representing the time of signature.

The legalAuthenticator MAY contain zero or one [0..1] sdtc:signatureText
extension element. This provides a textual or multimedia depiction of
the signature by which the participant endorses and accepts
responsibility for his or her participation in the Act. The element is
described in the HL7 CDA Digital Signature Standard.

::

   <legalAuthenticator>
       <time value="20050329224411+0500"/>
       <signatureCode code="S"/>
       <assignedEntity>
           <id extension="KP00017" root="2.16.840.1.113883.19"/>
           <addr>
               <streetAddressLine>21 North Ave.</streetAddressLine>
               <city>Burlington</city>
               <state>MA</state>
               <postalCode>02368</postalCode>
               <country>US</country>
           </addr>
           <telecom use="WP" value="tel:(555) 555-1003"/>
           <assignedPerson>
               <name>
                   <given>Henry</given>
                   <family>Seven</family>
               </name>
           </assignedPerson>
       </assignedEntity>
   </legalAuthenticator>

.. _sect_8.1.7:

recordTarget/patientRole/Patient/birthTime
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

Patient birthTime SHALL be precise to year, SHOULD be precise to day.

::

   <recordTarget>
       <patientRole>
           <id extension="12345" root="2.16.840.1.113883.19"/>
           <!-Example ID using fake assigning authority OID. ->
           <id extension="111-00-1234" root="2.16.840.1.118975.4.1"/>
           <!-Fake Social Security Number using the actual SSN OID. ->
           <addr use="HP">
               <!-HP is "primary home" from codeSystem 2.16.840.1.113883.5.1119 ->
               <streetAddressLine>17 Daws Rd.</streetAddressLine>
               <city>Blue Bell</city>
               <state>MA</state>
               <postalCode>02368</postalCode>
               <country>US</country>
               <!-US is "United States" from ISO 3166-1 Country Codes: 1.0.3166.1 ->
           </addr>
           <telecom value="tel:(781) 555-1212" use="HP"/>
           <!-HP is "primary home" from AddressUse 2.16.840.1.113883.5.1119 ->
           <patient>
               <name use="L">
                   <!-L is "Legal" from EntityNameUse 2.16.840.1.113883.5.45 ->
                   <prefix>Mr.</prefix>
                   <given>Adam</given>
                   <given qualifier="CL">Frankie</given>
                   <!-CL is "Call me" from EntityNamePartQualifier 2.16.840.1.113883.5.43 ->
                   <family>Everyman</family>
               </name>
               <administrativeGenderCode code="M"
                   codeSystem="2.16.840.1.113883.5.1" displayName="Male"/>
               <birthTime value="19541125"/>
           </patient>
           <providerOrganization>
               <id root="2.16.840.1.113883.19"/>
               <name>Good Health Clinic</name>
               <telecom use="WP" value="tel:(781) 555-1212"/>
               <addr>
                   <streetAddressLine>21 North Ave</streetAddressLine>
                   <city>Burlington</city>
                   <state>MA</state>
                   <postalCode>02368</postalCode>
                   <country>US</country>
               </addr>
           </providerOrganization>
       </patientRole>
   </recordTarget>

.. _sect_8.1.8:

author/assignedAuthor
~~~~~~~~~~~~~~~~~~~~~

The author element represents the creator of the clinical document. This
template restricts the author to be a person.

Such author SHALL contain exactly one [1..1] time representing the start
time of the author's participation in the creation of the content of the
clinical document.

::

   <author>
       <time value="20050329224411+0500"/>
       <assignedAuthor>
           <id extension="KP00017" root="2.16.840.1.113883.19.5"/>
           <addr>
               <streetAddressLine>21 North Ave.</streetAddressLine>
               <city>Burlington</city>
               <state>MA</state>
               <postalCode>02368</postalCode>
               <country>US</country>
           </addr>
           <telecom use="WP" value="tel:(555) 555-1003"/>
           <assignedPerson>
               <name>
                   <given>Henry</given>
                   <family>Seven</family>
               </name>
           </assignedPerson>
       </assignedAuthor>
   </author>

.. _sect_8.1.9:

InformationRecipient/intendedRecipient
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

The informationRecipient participation elements record the intended
recipients of the information at the time the document is created. An
intended recipient may be a person (an informationRecipient entity),
with or without an organization affiliation (receivedOrganization
scoping entity), or simply an organization. If an organization, the
document is expected to be incorporated into an information system of
that organization (e.g., the electronic medical record for the patient).

::

   <informationRecipient>
       <intendedRecipient classCode="ASSIGNED">
           <informationRecipient>
               <name>
                   <given>Henry</given>
                   <family>Seven</family>
               </name>
           </informationRecipient>
           <receivedOrganization>
               <name>Good Health Clinic</name>
           </receivedOrganization>
       </intendedRecipient>
   </informationRecipient>

.. _sect_8.2:

Imaging Header
--------------

+----------------------+----------------------------------------------+
| **Template ID**      | 1.2.840.10008.9.21                           |
+----------------------+----------------------------------------------+
| **Name**             | Imaging Header Elements                      |
+----------------------+----------------------------------------------+
| **Effective Date**   | 2015/03/24                                   |
+----------------------+----------------------------------------------+
| **Version Label**    | DICOM-20150324                               |
+----------------------+----------------------------------------------+
| **Status**           | Active                                       |
+----------------------+----------------------------------------------+
| **Description**      | CDA Header Elements for imaging reports,     |
|                      | including encounter, order, and study        |
|                      | context                                      |
+----------------------+----------------------------------------------+
| **Classification**   | CDA Header Elements                          |
+----------------------+----------------------------------------------+
| **Relationships**    | Included in `Imaging Report <#sect_7.1>`__   |
+----------------------+----------------------------------------------+
| **Context**          | sibling node                                 |
+----------------------+----------------------------------------------+
| **Open/Closed**      | Open                                         |
+----------------------+----------------------------------------------+
| **Revision History** | DICOM-20150324: Initial version              |
+----------------------+----------------------------------------------+

+-------+-------+-------+-------+-------+-------+-------+-------+-------+
| Bus   | Nest  | Ele   | Card  | Elem  | Data  | Value | Value | Subsi |
| iness | Level | ment/ |       | /Attr | Type  | Conf  |       | diary |
| Name  |       | ​Attr |       | Conf  |       |       |       | Tem   |
|       |       | ibute |       |       |       |       |       | plate |
+=======+=======+=======+=======+=======+=======+=======+=======+=======+
|       |       | t     | 1..1  | SHALL | II    |       |       |       |
|       |       | empla |       |       |       |       |       |       |
|       |       | te​Id |       |       |       |       |       |       |
+-------+-------+-------+-------+-------+-------+-------+-------+-------+
|       | @     | @root | 1..1  | SHALL | UID   | SHALL | 1.2   |       |
|       |       |       |       |       |       |       | .840. |       |
|       |       |       |       |       |       |       | 10008 |       |
|       |       |       |       |       |       |       | .9.21 |       |
+-------+-------+-------+-------+-------+-------+-------+-------+-------+
|       |       | co    | 1..1  | SHALL |       |       |       |       |
|       |       | mpone |       |       |       |       |       |       |
|       |       | nt​Of |       |       |       |       |       |       |
+-------+-------+-------+-------+-------+-------+-------+-------+-------+
|       | >     | en    | 1..1  | SHALL |       |       |       |       |
|       |       | compa |       |       |       |       |       |       |
|       |       | ssing |       |       |       |       |       |       |
|       |       | ​Enco |       |       |       |       |       |       |
|       |       | unter |       |       |       |       |       |       |
+-------+-------+-------+-------+-------+-------+-------+-------+-------+
|       | >>    | id    | 0..1  | S     | II    |       |       |       |
|       |       |       |       | HOULD |       |       |       |       |
+-------+-------+-------+-------+-------+-------+-------+-------+-------+
| Enc   | >>@   | @root | 1..1  | SHALL | UID   |       | *I    |       |
| ounte |       |       |       |       |       |       | ssuer |       |
| r​IDI |       |       |       |       |       |       | of    |       |
| ssuer |       |       |       |       |       |       | Admi  |       |
|       |       |       |       |       |       |       | ssion |       |
|       |       |       |       |       |       |       | ID    |       |
|       |       |       |       |       |       |       | Seq   |       |
|       |       |       |       |       |       |       | uence |       |
|       |       |       |       |       |       |       | (     |       |
|       |       |       |       |       |       |       | 0038; |       |
|       |       |       |       |       |       |       | 0014) |       |
|       |       |       |       |       |       |       | >     |       |
|       |       |       |       |       |       |       | Univ  |       |
|       |       |       |       |       |       |       | ersal |       |
|       |       |       |       |       |       |       | E     |       |
|       |       |       |       |       |       |       | ntity |       |
|       |       |       |       |       |       |       | ID    |       |
|       |       |       |       |       |       |       | (0    |       |
|       |       |       |       |       |       |       | 040,0 |       |
|       |       |       |       |       |       |       | 032)* |       |
|       |       |       |       |       |       |       |       |       |
|       |       |       |       |       |       |       | *     |       |
|       |       |       |       |       |       |       | Visit |       |
|       |       |       |       |       |       |       | N     |       |
|       |       |       |       |       |       |       | umber |       |
|       |       |       |       |       |       |       | P     |       |
|       |       |       |       |       |       |       | V1-19 |       |
|       |       |       |       |       |       |       | .4.2* |       |
+-------+-------+-------+-------+-------+-------+-------+-------+-------+
| En    | >>@   | @exte | 1..1  | SHALL | ST    |       | *Admi |       |
| count |       | nsion |       |       |       |       | ssion |       |
| er​ID |       |       |       |       |       |       | Id    |       |
|       |       |       |       |       |       |       | (0    |       |
|       |       |       |       |       |       |       | 038,0 |       |
|       |       |       |       |       |       |       | 010)* |       |
|       |       |       |       |       |       |       |       |       |
|       |       |       |       |       |       |       | *     |       |
|       |       |       |       |       |       |       | Visit |       |
|       |       |       |       |       |       |       | N     |       |
|       |       |       |       |       |       |       | umber |       |
|       |       |       |       |       |       |       | PV1-  |       |
|       |       |       |       |       |       |       | 19.1* |       |
+-------+-------+-------+-------+-------+-------+-------+-------+-------+
| Enco  | >>    | effe  | 1..1  | SHALL |       |       |       |       |
| unter |       | ctive |       |       |       |       |       |       |
| ​Time |       | ​Time |       |       |       |       |       |       |
+-------+-------+-------+-------+-------+-------+-------+-------+-------+
|       | >>    | loc   | 0..1  | MAY   |       |       |       |       |
|       |       | ation |       |       |       |       |       |       |
+-------+-------+-------+-------+-------+-------+-------+-------+-------+
|       | >>>   | healt | 1..1  | SHALL |       |       |       |       |
|       |       | h​Car |       |       |       |       |       |       |
|       |       | e​Fac |       |       |       |       |       |       |
|       |       | ility |       |       |       |       |       |       |
+-------+-------+-------+-------+-------+-------+-------+-------+-------+
|       | >>>>  | loc   | 0..1  | S     |       |       |       |       |
|       |       | ation |       | HOULD |       |       |       |       |
+-------+-------+-------+-------+-------+-------+-------+-------+-------+
| Heal  | >>>>> | name  | 1..1  | SHALL | EN    |       |       |       |
| thcar |       |       |       |       |       |       |       |       |
| e​Fac |       |       |       |       |       |       |       |       |
| ility |       |       |       |       |       |       |       |       |
| ​Name |       |       |       |       |       |       |       |       |
+-------+-------+-------+-------+-------+-------+-------+-------+-------+
| He    | >>>>> | addr  | 1..1  | SHALL | AD    |       |       |       |
| althc |       |       |       |       |       |       |       |       |
| are​F |       |       |       |       |       |       |       |       |
| acili |       |       |       |       |       |       |       |       |
| ty​Ad |       |       |       |       |       |       |       |       |
| dress |       |       |       |       |       |       |       |       |
+-------+-------+-------+-------+-------+-------+-------+-------+-------+
|       | >>>>  | serv  | 0..1  | S     |       |       |       |       |
|       |       | ice​P |       | HOULD |       |       |       |       |
|       |       | rovid |       |       |       |       |       |       |
|       |       | er​Or |       |       |       |       |       |       |
|       |       | ganiz |       |       |       |       |       |       |
|       |       | ation |       |       |       |       |       |       |
+-------+-------+-------+-------+-------+-------+-------+-------+-------+
| He    | >>>>> | name  | 1..1  | SHALL | ON    |       |       |       |
| althc |       |       |       |       |       |       |       |       |
| are​P |       |       |       |       |       |       |       |       |
| rovid |       |       |       |       |       |       |       |       |
| er​Or |       |       |       |       |       |       |       |       |
| ganiz |       |       |       |       |       |       |       |       |
| ation |       |       |       |       |       |       |       |       |
| ​Name |       |       |       |       |       |       |       |       |
+-------+-------+-------+-------+-------+-------+-------+-------+-------+
|       | >>    | e     | 0..\* | MAY   |       |       |       |       |
|       |       | ncoun |       |       |       |       |       |       |
|       |       | ter​P |       |       |       |       |       |       |
|       |       | artic |       |       |       |       |       |       |
|       |       | ipant |       |       |       |       |       |       |
+-------+-------+-------+-------+-------+-------+-------+-------+-------+
|       | >>@   | @typ  | 1..1  | SHALL |       |       | ATND  |       |
|       |       | eCode |       |       |       |       |       |       |
+-------+-------+-------+-------+-------+-------+-------+-------+-------+
|       | >>>   | assig | 1..1  | SHALL |       |       |       |       |
|       |       | ned​E |       |       |       |       |       |       |
|       |       | ntity |       |       |       |       |       |       |
+-------+-------+-------+-------+-------+-------+-------+-------+-------+
|       | >>>>  | assig | 1..1  | SHALL |       |       |       |       |
|       |       | ned​P |       |       |       |       |       |       |
|       |       | erson |       |       |       |       |       |       |
+-------+-------+-------+-------+-------+-------+-------+-------+-------+
| Atte  | >>>>> | name  | 1..1  | SHALL | EN    |       |       |       |
| nding |       |       |       |       |       |       |       |       |
| ​Phys |       |       |       |       |       |       |       |       |
| ician |       |       |       |       |       |       |       |       |
| ​Name |       |       |       |       |       |       |       |       |
+-------+-------+-------+-------+-------+-------+-------+-------+-------+
|       |       | in    | 1..\* | SHALL |       |       |       |       |
|       |       | ​Fulf |       |       |       |       |       |       |
|       |       | illme |       |       |       |       |       |       |
|       |       | nt​Of |       |       |       |       |       |       |
+-------+-------+-------+-------+-------+-------+-------+-------+-------+
| **    | >     | order | 1..1  | SHALL |       |       |       |       |
| Order |       |       |       |       |       |       |       |       |
| [*]** |       |       |       |       |       |       |       |       |
+-------+-------+-------+-------+-------+-------+-------+-------+-------+
|       | >>    | id    | 1..1  | SHALL | II    |       |       |       |
+-------+-------+-------+-------+-------+-------+-------+-------+-------+
| Order | >>@   | @root | 1..1  | SHALL | UID   |       | *     |       |
| ​Assi |       |       |       |       |       |       | Order |       |
| gning |       |       |       |       |       |       | P     |       |
| ​Auth |       |       |       |       |       |       | lacer |       |
| ority |       |       |       |       |       |       | Ident |       |
|       |       |       |       |       |       |       | ifier |       |
|       |       |       |       |       |       |       | Seq   |       |
|       |       |       |       |       |       |       | uence |       |
|       |       |       |       |       |       |       | (     |       |
|       |       |       |       |       |       |       | 0040, |       |
|       |       |       |       |       |       |       | 0026) |       |
|       |       |       |       |       |       |       | >     |       |
|       |       |       |       |       |       |       | Univ  |       |
|       |       |       |       |       |       |       | ersal |       |
|       |       |       |       |       |       |       | E     |       |
|       |       |       |       |       |       |       | ntity |       |
|       |       |       |       |       |       |       | ID    |       |
|       |       |       |       |       |       |       | (0    |       |
|       |       |       |       |       |       |       | 040,0 |       |
|       |       |       |       |       |       |       | 032)* |       |
|       |       |       |       |       |       |       |       |       |
|       |       |       |       |       |       |       | *P    |       |
|       |       |       |       |       |       |       | lacer |       |
|       |       |       |       |       |       |       | Order |       |
|       |       |       |       |       |       |       | N     |       |
|       |       |       |       |       |       |       | umber |       |
|       |       |       |       |       |       |       | OBR   |       |
|       |       |       |       |       |       |       | -2.3* |       |
+-------+-------+-------+-------+-------+-------+-------+-------+-------+
| Orde  | >>@   | @exte | 1..1  | SHALL | ST    |       | *P    |       |
| r​Pla |       | nsion |       |       |       |       | lacer |       |
| cer​N |       |       |       |       |       |       | Order |       |
| umber |       |       |       |       |       |       | Numb  |       |
|       |       |       |       |       |       |       | er/Im |       |
|       |       |       |       |       |       |       | aging |       |
|       |       |       |       |       |       |       | Se    |       |
|       |       |       |       |       |       |       | rvice |       |
|       |       |       |       |       |       |       | Re    |       |
|       |       |       |       |       |       |       | quest |       |
|       |       |       |       |       |       |       | (0    |       |
|       |       |       |       |       |       |       | 040,2 |       |
|       |       |       |       |       |       |       | 016)* |       |
|       |       |       |       |       |       |       |       |       |
|       |       |       |       |       |       |       | *P    |       |
|       |       |       |       |       |       |       | lacer |       |
|       |       |       |       |       |       |       | Order |       |
|       |       |       |       |       |       |       | N     |       |
|       |       |       |       |       |       |       | umber |       |
|       |       |       |       |       |       |       | OBR   |       |
|       |       |       |       |       |       |       | -2.1* |       |
+-------+-------+-------+-------+-------+-------+-------+-------+-------+
|       | >>    | ps    | 1..1  | SHALL | II    |       |       |       |
|       |       | 3-20: |       |       |       |       |       |       |
|       |       | acces |       |       |       |       |       |       |
|       |       | sionN |       |       |       |       |       |       |
|       |       | umber |       |       |       |       |       |       |
+-------+-------+-------+-------+-------+-------+-------+-------+-------+
| Acce  | >>@   | @root | 1..1  | SHALL | UID   |       | *I    |       |
| ssion |       |       |       |       |       |       | ssuer |       |
| ​Assi |       |       |       |       |       |       | of    |       |
| gning |       |       |       |       |       |       | Acce  |       |
| ​Auth |       |       |       |       |       |       | ssion |       |
| ority |       |       |       |       |       |       | N     |       |
|       |       |       |       |       |       |       | umber |       |
|       |       |       |       |       |       |       | Seq   |       |
|       |       |       |       |       |       |       | uence |       |
|       |       |       |       |       |       |       | (     |       |
|       |       |       |       |       |       |       | 0008, |       |
|       |       |       |       |       |       |       | 0051) |       |
|       |       |       |       |       |       |       | >     |       |
|       |       |       |       |       |       |       | Univ  |       |
|       |       |       |       |       |       |       | ersal |       |
|       |       |       |       |       |       |       | E     |       |
|       |       |       |       |       |       |       | ntity |       |
|       |       |       |       |       |       |       | ID    |       |
|       |       |       |       |       |       |       | (0    |       |
|       |       |       |       |       |       |       | 040,0 |       |
|       |       |       |       |       |       |       | 032)* |       |
|       |       |       |       |       |       |       |       |       |
|       |       |       |       |       |       |       | *F    |       |
|       |       |       |       |       |       |       | iller |       |
|       |       |       |       |       |       |       | Order |       |
|       |       |       |       |       |       |       | N     |       |
|       |       |       |       |       |       |       | umber |       |
|       |       |       |       |       |       |       | OBR   |       |
|       |       |       |       |       |       |       | -2.3* |       |
+-------+-------+-------+-------+-------+-------+-------+-------+-------+
| A     | >>@   | @exte | 1..1  | SHALL | ST    |       | *Acce |       |
| ccess |       | nsion |       |       |       |       | ssion |       |
| ion​N |       |       |       |       |       |       | N     |       |
| umber |       |       |       |       |       |       | umber |       |
|       |       |       |       |       |       |       | (0    |       |
|       |       |       |       |       |       |       | 008,0 |       |
|       |       |       |       |       |       |       | 050)* |       |
|       |       |       |       |       |       |       |       |       |
|       |       |       |       |       |       |       | *F    |       |
|       |       |       |       |       |       |       | iller |       |
|       |       |       |       |       |       |       | Order |       |
|       |       |       |       |       |       |       | N     |       |
|       |       |       |       |       |       |       | umber |       |
|       |       |       |       |       |       |       | OBR   |       |
|       |       |       |       |       |       |       | -2.1* |       |
+-------+-------+-------+-------+-------+-------+-------+-------+-------+
| Or    | >>    | code  | 0..1  | S     | CE    |       | *Requ |       |
| dered |       |       |       | HOULD |       |       | ested |       |
| ​Proc |       |       |       |       |       |       | Proc  |       |
| edure |       |       |       |       |       |       | edure |       |
| ​Code |       |       |       |       |       |       | Code  |       |
|       |       |       |       |       |       |       | Seq   |       |
|       |       |       |       |       |       |       | uence |       |
|       |       |       |       |       |       |       | (0    |       |
|       |       |       |       |       |       |       | 032,1 |       |
|       |       |       |       |       |       |       | 064)* |       |
|       |       |       |       |       |       |       |       |       |
|       |       |       |       |       |       |       | *Univ |       |
|       |       |       |       |       |       |       | ersal |       |
|       |       |       |       |       |       |       | Se    |       |
|       |       |       |       |       |       |       | rvice |       |
|       |       |       |       |       |       |       | ID    |       |
|       |       |       |       |       |       |       | O     |       |
|       |       |       |       |       |       |       | BR-4* |       |
+-------+-------+-------+-------+-------+-------+-------+-------+-------+
| Orde  | >>    | pri   | 0..1  | S     | CE    |       | Val   |       |
| r​Pri |       | ority |       | HOULD |       |       | ueSet |       |
| ority |       | ​Code |       |       |       |       | 2     |       |
|       |       |       |       |       |       |       | .16.8 |       |
|       |       |       |       |       |       |       | 40.1. |       |
|       |       |       |       |       |       |       | 11388 |       |
|       |       |       |       |       |       |       | 3.11. |       |
|       |       |       |       |       |       |       | 16866 |       |
+-------+-------+-------+-------+-------+-------+-------+-------+-------+
|       |       | d     | 1..\* | SHALL |       |       |       |       |
|       |       | ocume |       |       |       |       |       |       |
|       |       | ntati |       |       |       |       |       |       |
|       |       | on​Of |       |       |       |       |       |       |
+-------+-------+-------+-------+-------+-------+-------+-------+-------+
| **    | >     | ser   | 1..1  | SHALL |       |       |       |       |
| Study |       | vice​ |       |       |       |       |       |       |
| [*]** |       | Event |       |       |       |       |       |       |
+-------+-------+-------+-------+-------+-------+-------+-------+-------+
| Stud  | >>    | id    | 1..1  | SHALL | II    |       | *     |       |
| y​UID |       |       |       |       |       |       | Study |       |
|       |       |       |       |       |       |       | Ins   |       |
|       |       |       |       |       |       |       | tance |       |
|       |       |       |       |       |       |       | UID   |       |
|       |       |       |       |       |       |       | (0    |       |
|       |       |       |       |       |       |       | 020,0 |       |
|       |       |       |       |       |       |       | 00D)* |       |
|       |       |       |       |       |       |       |       |       |
|       |       |       |       |       |       |       | *     |       |
|       |       |       |       |       |       |       | Study |       |
|       |       |       |       |       |       |       | Ins   |       |
|       |       |       |       |       |       |       | tance |       |
|       |       |       |       |       |       |       | UID   |       |
|       |       |       |       |       |       |       | I     |       |
|       |       |       |       |       |       |       | PC-3* |       |
+-------+-------+-------+-------+-------+-------+-------+-------+-------+
| Proc  | >>    | code  | 1..1  | SHALL | CE    |       | *Proc |       |
| edure |       |       |       |       |       |       | edure |       |
| ​Code |       |       |       |       |       |       | Code  |       |
|       |       |       |       |       |       |       | Seq   |       |
|       |       |       |       |       |       |       | uence |       |
|       |       |       |       |       |       |       | (0    |       |
|       |       |       |       |       |       |       | 008,1 |       |
|       |       |       |       |       |       |       | 032)* |       |
+-------+-------+-------+-------+-------+-------+-------+-------+-------+
| Mod   | >>>   | t     | 1..\* | SHALL | CD    | SHALL | *Mod  |       |
| ality |       | ransl |       |       |       | CNE   | ality |       |
|       |       | ation |       |       |       |       | (0    |       |
|       |       |       |       |       |       |       | 008,0 |       |
|       |       |       |       |       |       |       | 060)* |       |
+-------+-------+-------+-------+-------+-------+-------+-------+-------+
| Anato | >>>   | t     | 0..1  | S     | CD    |       | Conc  |       |
| mic​R |       | ransl |       | HOULD |       |       | ept​D |       |
| egion |       | ation |       |       |       |       | omain |       |
| ​Code |       |       |       |       |       |       | Anat  |       |
|       |       |       |       |       |       |       | omicR |       |
|       |       |       |       |       |       |       | egion |       |
+-------+-------+-------+-------+-------+-------+-------+-------+-------+
|       | >>    | effe  | 1..1  | SHALL | IVL   |       |       |       |
|       |       | ctive |       |       | <TS>  |       |       |       |
|       |       | ​Time |       |       |       |       |       |       |
+-------+-------+-------+-------+-------+-------+-------+-------+-------+
| Study | >>>   | low   | 1..1  | SHALL | TS    |       | *     |       |
| ​Time |       |       |       |       |       |       | Study |       |
|       |       |       |       |       |       |       | Date  |       |
|       |       |       |       |       |       |       | (     |       |
|       |       |       |       |       |       |       | 0008, |       |
|       |       |       |       |       |       |       | 0020) |       |
|       |       |       |       |       |       |       | +     |       |
|       |       |       |       |       |       |       | Study |       |
|       |       |       |       |       |       |       | Time  |       |
|       |       |       |       |       |       |       | (     |       |
|       |       |       |       |       |       |       | 0008, |       |
|       |       |       |       |       |       |       | 0030) |       |
|       |       |       |       |       |       |       | +     |       |
|       |       |       |       |       |       |       | Tim   |       |
|       |       |       |       |       |       |       | ezone |       |
|       |       |       |       |       |       |       | O     |       |
|       |       |       |       |       |       |       | ffset |       |
|       |       |       |       |       |       |       | From  |       |
|       |       |       |       |       |       |       | UTC   |       |
|       |       |       |       |       |       |       | (0    |       |
|       |       |       |       |       |       |       | 008,0 |       |
|       |       |       |       |       |       |       | 201)* |       |
|       |       |       |       |       |       |       |       |       |
|       |       |       |       |       |       |       | *O    |       |
|       |       |       |       |       |       |       | bserv |       |
|       |       |       |       |       |       |       | ation |       |
|       |       |       |       |       |       |       | Date  |       |
|       |       |       |       |       |       |       | /Time |       |
|       |       |       |       |       |       |       | O     |       |
|       |       |       |       |       |       |       | BR-7* |       |
+-------+-------+-------+-------+-------+-------+-------+-------+-------+
| *     | >>    | perf  | 0..\* | MAY   |       |       |       |       |
| *Perf |       | ormer |       |       |       |       |       |       |
| ormer |       |       |       |       |       |       |       |       |
| [*]** |       |       |       |       |       |       |       |       |
+-------+-------+-------+-------+-------+-------+-------+-------+-------+
| Type  | >>@   | @typ  | 1..1  | SHALL | CS    | SHALL | Val   |       |
|       |       | eCode |       |       |       |       | ueSet |       |
|       |       |       |       |       |       |       | 2     |       |
|       |       |       |       |       |       |       | .16.8 |       |
|       |       |       |       |       |       |       | 40.1. |       |
|       |       |       |       |       |       |       | 11388 |       |
|       |       |       |       |       |       |       | 3.11. |       |
|       |       |       |       |       |       |       | 19601 |       |
+-------+-------+-------+-------+-------+-------+-------+-------+-------+
|       | >>>   | assig | 1..1  | SHALL |       |       |       |       |
|       |       | ned​E |       |       |       |       |       |       |
|       |       | ntity |       |       |       |       |       |       |
+-------+-------+-------+-------+-------+-------+-------+-------+-------+
| ID    | >>>>  | id    | 1..1  | SHALL | II    |       |       |       |
+-------+-------+-------+-------+-------+-------+-------+-------+-------+
|       | >>>>  | assig | 1..1  | SHALL |       |       |       |       |
|       |       | ned​P |       |       |       |       |       |       |
|       |       | erson |       |       |       |       |       |       |
+-------+-------+-------+-------+-------+-------+-------+-------+-------+
| Name  | >>>>> | name  | 1..1  | SHALL | PN    |       |       |       |
+-------+-------+-------+-------+-------+-------+-------+-------+-------+
|       |       | p     | 1..1  | SHALL |       |       |       |       |
|       |       | artic |       |       |       |       |       |       |
|       |       | ipant |       |       |       |       |       |       |
+-------+-------+-------+-------+-------+-------+-------+-------+-------+
|       | @     | @typ  | 1..1  | SHALL | CS    | SHALL | REF   |       |
|       |       | eCode |       |       |       |       |       |       |
+-------+-------+-------+-------+-------+-------+-------+-------+-------+
|       | >     | as    | 1..1  | SHALL |       |       |       |       |
|       |       | socia |       |       |       |       |       |       |
|       |       | ted​E |       |       |       |       |       |       |
|       |       | ntity |       |       |       |       |       |       |
+-------+-------+-------+-------+-------+-------+-------+-------+-------+
|       | >@    | @clas | 1..1  | SHALL | CS    | SHALL | PROV  |       |
|       |       | sCode |       |       |       |       |       |       |
+-------+-------+-------+-------+-------+-------+-------+-------+-------+
| R     | >>    | id    | 0..1  | S     | II    |       | *Ord  |       |
| eferr |       |       |       | HOULD |       |       | ering |       |
| er​ID |       |       |       |       |       |       | Pro   |       |
|       |       |       |       |       |       |       | vider |       |
|       |       |       |       |       |       |       | ORC   |       |
|       |       |       |       |       |       |       | -12.1 |       |
|       |       |       |       |       |       |       | +     |       |
|       |       |       |       |       |       |       | O     |       |
|       |       |       |       |       |       |       | RC-12 |       |
|       |       |       |       |       |       |       | .9.2* |       |
+-------+-------+-------+-------+-------+-------+-------+-------+-------+
| Ref   | >>    | addr  | 0.\*  | S     | AD    |       | *Ord  |       |
| errer |       |       |       | HOULD |       |       | ering |       |
| ​Addr |       |       |       |       |       |       | Pro   |       |
|       |       |       |       |       |       |       | vider |       |
|       |       |       |       |       |       |       | Ad    |       |
|       |       |       |       |       |       |       | dress |       |
|       |       |       |       |       |       |       | OR    |       |
|       |       |       |       |       |       |       | C-24* |       |
+-------+-------+-------+-------+-------+-------+-------+-------+-------+
| Re    | >>    | te    | 0..\* | S     | TEL   |       | *Call |       |
| ferre |       | lecom |       | HOULD |       |       | Back  |       |
| r​Tel |       |       |       |       |       |       | Phone |       |
|       |       |       |       |       |       |       | N     |       |
|       |       |       |       |       |       |       | umber |       |
|       |       |       |       |       |       |       | OR    |       |
|       |       |       |       |       |       |       | C-14* |       |
+-------+-------+-------+-------+-------+-------+-------+-------+-------+
|       | >>    | as    | 1..1  | SHALL |       |       |       |       |
|       |       | socia |       |       |       |       |       |       |
|       |       | ted​P |       |       |       |       |       |       |
|       |       | erson |       |       |       |       |       |       |
+-------+-------+-------+-------+-------+-------+-------+-------+-------+
| Ref   | >>>   | name  | 1..1  | SHALL | PN    |       | *Refe |       |
| errer |       |       |       |       |       |       | rring |       |
| ​Name |       |       |       |       |       |       | P     |       |
|       |       |       |       |       |       |       | hysic |       |
|       |       |       |       |       |       |       | ian's |       |
|       |       |       |       |       |       |       | Name  |       |
|       |       |       |       |       |       |       | (0    |       |
|       |       |       |       |       |       |       | 008,0 |       |
|       |       |       |       |       |       |       | 090)* |       |
|       |       |       |       |       |       |       |       |       |
|       |       |       |       |       |       |       | *Ord  |       |
|       |       |       |       |       |       |       | ering |       |
|       |       |       |       |       |       |       | Pro   |       |
|       |       |       |       |       |       |       | vider |       |
|       |       |       |       |       |       |       | OR    |       |
|       |       |       |       |       |       |       | C-12* |       |
+-------+-------+-------+-------+-------+-------+-------+-------+-------+
|       |       | da    | 0..1  | MAY   |       |       |       |       |
|       |       | ta​En |       |       |       |       |       |       |
|       |       | terer |       |       |       |       |       |       |
+-------+-------+-------+-------+-------+-------+-------+-------+-------+
|       | @     | @typ  | 1..1  | SHALL | CS    | SHALL | ENT   |       |
|       |       | eCode |       |       |       |       |       |       |
+-------+-------+-------+-------+-------+-------+-------+-------+-------+
|       | >     | assig | 1..1  | SHALL |       |       |       |       |
|       |       | ned​E |       |       |       |       |       |       |
|       |       | ntity |       |       |       |       |       |       |
+-------+-------+-------+-------+-------+-------+-------+-------+-------+
| Tran  | >>    | id    | 0..1  | S     | II    |       | *T    |       |
| scrip |       |       |       | HOULD |       |       | ransc |       |
| tioni |       |       |       |       |       |       | ripti |       |
| st​ID |       |       |       |       |       |       | onist |       |
|       |       |       |       |       |       |       | O     |       |
|       |       |       |       |       |       |       | BR-35 |       |
|       |       |       |       |       |       |       | .1.1* |       |
+-------+-------+-------+-------+-------+-------+-------+-------+-------+
|       | >>    | assig | 0..1  | S     |       |       |       |       |
|       |       | ned​P |       | HOULD |       |       |       |       |
|       |       | erson |       |       |       |       |       |       |
+-------+-------+-------+-------+-------+-------+-------+-------+-------+
| T     | >>>   | name  | 1..1  | SHALL | PN    |       | *T    |       |
| ransc |       |       |       |       |       |       | ransc |       |
| ripti |       |       |       |       |       |       | ripti |       |
| onist |       |       |       |       |       |       | onist |       |
| ​Name |       |       |       |       |       |       | OBR-  |       |
|       |       |       |       |       |       |       | 35.1* |       |
+-------+-------+-------+-------+-------+-------+-------+-------+-------+

Note that there is no business name associated with this template.
Rather, this template is an editorial convenience for template
specification, and the Business Names for the elements of this template
are logically part of the Business Name scope of the invoking template.

.. _sect_8.2.1:

componentOf/encompassingEncounter
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

The id element of the encompassingEncounter represents the identifier
for the encounter. When the diagnostic imaging procedure is performed in
the context of a hospital stay or an outpatient visit for which there is
an Encounter Number, Visit Number, or Admission ID, equivalent to DICOM
attribute (0038,0010), that number should be present as the ID of the
encompassingEncounter.

The effectiveTime of the encompassingEncounter represents the time
interval or point in time in which the encounter took place. The
encompassing encounter might be that of the hospital or office visit in
which the imaging procedure was performed. If the effective time is
unknown, a nullFlavor attribute can be used.

::

   <componentOf>
       <encompassingEncounter>
           <id extension="9937012" root="1.3.6.4.1.4.1.2835.12"/>
           <effectiveTime value="20060828170821"/>
           <encounterParticipant typeCode="ATND">
               <assignedEntity>
                   <id extension="4" root="2.16.840.1.113883.19"/>
                   <code code="208M00000X"
                       codeSystem="2.16.840.1.113883.6.101"
                       codeSystemName="NUCC"
                       displayName="Hospitalist"/>
                   <addr nullFlavor="NI"/>
                   <telecom nullFlavor="NI"/>
                   <assignedPerson>
                       <name>
                           <prefix>Dr.</prefix>
                           <given>Fay </given>
                           <family>Family</family>
                       </name>
                   </assignedPerson>
               </assignedEntity>
           </encounterParticipant>
       </encompassingEncounter>
   </componentOf>

.. _sect_8.2.2:

Physician of Record Participant
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

This encounterParticipant with typeCode="ATND" (Attender) is the
attending physician and is usually different from the Physician Reading
Study Performer defined in documentationOf/serviceEvent.

::

   <encounterParticipant typeCode="ATND">
       <assignedEntity>
           <id extension="44444444" root="2.16.840.1.113883.4.6"/>
           <code code="208M00000X"
               codeSystem="2.16.840.1.113883.6.101"
               codeSystemName="NUCC"
               displayName="Hospitalist"/>
           <addr nullFlavor="NI"/>
           <telecom nullFlavor="NI"/>
           <assignedPerson>
               <name>
                   <prefix>Dr.</prefix>
                   <given>Fay</given>
                   <family>Family</family>
               </name>
           </assignedPerson>
       </assignedEntity>
   </encounterParticipant>

.. _sect_8.2.3:

inFulfillmentOf/Order and @ID
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

An inFulfillmentOf element represents the Placer Order. There may be
more than one inFulfillmentOf element in the case where a single report
is fulfilling multiple orders. There SHALL be one inFulfillmentOf/order
for each distinct Order associated with the report.

In each inFulfillmentOf/order there SHALL be one order/id for the Placer
Order Number (0040,2016). There SHALL be one
order/ps3-20:accessionNumber for the DICOM Accession Number (0008,0050)
associated with the order. The ps3-20:accessionNumber SHALL be Data Type
II; it SHALL have a UID root attribute identifying its assigning
authority, and the DICOM Accession Number SHALL be in the extension
attribute.

::

   <xs:schema ...
       xmlns:ps3-20="urn:dicom-org:ps3-20"
       ...
   </xs:schema>
   <inFulfillmentOf>
       <order>
           <id extension="089-927851" root="2.16.840.1.113883.19.4.33"/>
           <!-- {extension} =
             Placer Order Number/Imaging Service Request (0040,2016) {root} =
             Order Placer Identifier Sequence (0040,0026) > Universal Entity ID (0040,0032) -->
           <ps3-20:accessionNumber extension="10523475" root="2.16.840.1.113883.19.4.27" />
           <!-- {extension}=
             Accession Number (0008,0050) {root} =
             Issuer of Accession Number Sequence (0008,0051) > Universal Entity ID (0040,0032) -->
           <code code="RPID24"
               displayName="CT HEAD WITH IV CONTRAST"
               codeSystem="2.16.840.1.113883.6.256"
               codeSystemName="RadLex Playbook">
           <!-- Ordered Procedure Code is
             Requested Procedure Code Sequence (0032,1064) -->
       </order>
   </inFulfillmentOf>

.. _sect_8.2.4:

documentationOf/serviceEvent
~~~~~~~~~~~~~~~~~~~~~~~~~~~~

Each documentationOf/serviceEvent indicates an imaging procedure that
the provider describes and interprets in the content of the report. The
main activity being described by this document is both the performance
of the imaging procedure and the interpretation of the imaging
procedure.

There may be more than one documentationOf/serviceEvent element if the
report is interpreting multiple DICOM Studies. There may also be
multiple reports for a single DICOM Study.

The serviceEvent/id element contains the DICOM Study Instance UID.

The date and time of the imaging procedure is indicated in the
serviceEvent/effectiveTime element; the date and time of the
interpretation is in the clinicalDocument/effectiveTime.

.. note::

   The serviceEvent/effectiveTime uses the IVL_TS data type with the low
   element required, for harmonization with Consolidated CDA release
   1.1.

.. _sect_8.2.4.1:

code and translation
^^^^^^^^^^^^^^^^^^^^

Within each documentationOf element, there is one serviceEvent element.
The type of imaging procedure may be further described in the
serviceEvent/code element. This guide makes no specific recommendations
about the primary vocabulary to use for describing this event,
identified as Procedure Code.

The serviceEvent/code/translation elements include codes representing
the primary image acquisition modality using DICOM (DCM) terminology,
and target anatomic region (for which SNOMED terminology is
recommended).

.. note::

   1. These codes may be used as health information exchange search
      metadata in accordance with the IHE Radiology Technical Framework
      Cross-Enterprise Document Sharing for Imaging (XDS-I) Profile.

   2. Binding of the Concept Domains ProcedureCode and AnatomicRegion to
      specific Value Sets may be done in a further profiling of the use
      of this Template.

::

   <documentationOf>
       <serviceEvent classCode="ACT" moodCode="EVN">
           <!-- study instance UID (0020,000D) -->
           <id root="1.2.840.113619.2.62.994044785528.114289542805"/>
           <!-- code is DICOM (Performed) Procedure Code Seq (0008,1032) -->
           <code code="71020"
               displayName="Radiologic examination, chest, two views, frontal and lateral"
               codeSystem="2.16.840.1.113883.6.12"
               codeSystemName="CPT4">
               <translation code="XR"
                   displayName="XR"
                   codeSystem="1.2.840.10008.2.16.4"
                   codeSystemName="DCM"/>
           </code>
           <!-- translation code is Modality (0008,0060) -->
           <effectiveTime value="20060823222400+0800"/>
       </serviceEvent>
   </documentationOf>

.. _sect_8.2.4.2:

Performer
^^^^^^^^^

The documentationOf/serviceEvent may include as a participant the
physician reading the study, equivalent to DICOM attribute (0008,1060),
and other healthcare professional participants in the procedure (e.g.,
the surgical performer in an interventional procedure).

.. note::

   In simple procedures, the physician reading the study is identified
   in the Author or LegalAuthenticator participation on the
   ClinicalDocument, and does not need to be re-identified in this
   element. The technologist performing the imaging may be identified in
   this element as a secondary performer, since the interpreting
   physician is the principal performer responsible for the service
   event.

::

   <performer typeCode="PRF">
       <assignedEntity>
           <id extension="111111111" root="2.16.840.1.113883.4.6"/>
           <code code="2085R0202X"
               codeSystem="2.16.840.1.113883.6.101"
               codeSystemName="NUCC"
               displayName="Diagnostic Radiology"/>
           <addr nullFlavor="NI"/>
           <telecom nullFlavor="NI"/>
           <assignedPerson>
               <name><given>Christine</given><family>Cure</family><suffix>MD</suffix></name>
           </assignedPerson>
       </assignedEntity>
   </performer>

::

   <participant typeCode="REF">
       <associatedEntity classCode="PROV">
           <id nullFlavor="NI"/>
           <addr nullFlavor="NI"/>
           <telecom nullFlavor="NI"/>
           <associatedPerson>
               <name><given>Amanda</given><family>Assigned</family><suffix>MD</suffix></name>
           </associatedPerson>
       </associatedEntity>
   </participant>

::

   <dataEnterer>
       <assignedEntity typeCode="ENT">
           <id root="2.16.840.1.113883.19.5" extension="43252"/>
           <addr>
               <streetAddressLine>21 North Ave.</streetAddressLine>
               <city>Burlington</city>
               <state>MA</state>
               <postalCode>02368</postalCode>
               <country>US</country>
           </addr>
           <telecom use="WP" value="tel:(555) 555-1003"/>
           <assignedPerson>
               <name><given>Henry</given><family>Seven</family></name>
           </assignedPerson>
       </assignedEntity>
   </dataEnterer>

.. _sect_8.3:

Parent Document
---------------

+----------------------+----------------------------------------------+
| **Template ID**      | 1.2.840.10008.9.22                           |
+----------------------+----------------------------------------------+
| **Name**             | Parent Document Header Elements              |
+----------------------+----------------------------------------------+
| **Effective Date**   | 2015/03/24                                   |
+----------------------+----------------------------------------------+
| **Version Label**    | DICOM-20150324                               |
+----------------------+----------------------------------------------+
| **Status**           | Active                                       |
+----------------------+----------------------------------------------+
| **Description**      | CDA Header Elements describing relationship  |
|                      | to prior/parent documents                    |
+----------------------+----------------------------------------------+
| **Classification**   | CDA Header Elements                          |
+----------------------+----------------------------------------------+
| **Relationships**    | Included in all document level templates     |
+----------------------+----------------------------------------------+
| **Context**          | sibling node                                 |
+----------------------+----------------------------------------------+
| **Open/Closed**      | Open                                         |
+----------------------+----------------------------------------------+
| **Revision History** | DICOM-20150324: Initial version              |
+----------------------+----------------------------------------------+

+-------+-------+-------+------+-------+-------+-------+-------+-------+
| Bus   | Nest  | Ele   | Card | Elem  | Data  | Value | Value | Subsi |
| iness | Level | ment/ |      | /Attr | Type  | Conf  |       | diary |
| Name  |       | ​Attr |      | Conf  |       |       |       | Tem   |
|       |       | ibute |      |       |       |       |       | plate |
+=======+=======+=======+======+=======+=======+=======+=======+=======+
|       |       | r     | 0..1 | MAY   |       |       |       |       |
|       |       | elate |      |       |       |       |       |       |
|       |       | d​Doc |      |       |       |       |       |       |
|       |       | ument |      |       |       |       |       |       |
+-------+-------+-------+------+-------+-------+-------+-------+-------+
|       | @     | @typ  | 1.1  | SHALL | CS    | SHALL | RPLC  |       |
|       |       | ecode |      |       |       |       |       |       |
+-------+-------+-------+------+-------+-------+-------+-------+-------+
|       | >     | paren | 1..1 | SHALL |       |       |       |       |
|       |       | t​Doc |      |       |       |       |       |       |
|       |       | ument |      |       |       |       |       |       |
+-------+-------+-------+------+-------+-------+-------+-------+-------+
| Repla | >>    | id    | 1..1 | SHALL | II    |       |       |       |
| ced​D |       |       |      |       |       |       |       |       |
| ocume |       |       |      |       |       |       |       |       |
| nt​ID |       |       |      |       |       |       |       |       |
+-------+-------+-------+------+-------+-------+-------+-------+-------+
| Repl  | >>    | s     | 0..1 | MAY   | II    |       |       |       |
| aced​ |       | et​Id |      |       |       |       |       |       |
| Docum |       |       |      |       |       |       |       |       |
| ent​S |       |       |      |       |       |       |       |       |
| et​ID |       |       |      |       |       |       |       |       |
+-------+-------+-------+------+-------+-------+-------+-------+-------+
| Repla | >>    | vers  | 1..1 | COND  | INT   |       |       |       |
| ced​D |       | ion​N |      |       |       |       |       |       |
| ocume |       | umber |      |       |       |       |       |       |
| nt​Ve |       |       |      |       |       |       |       |       |
| rsion |       |       |      |       |       |       |       |       |
+-------+-------+-------+------+-------+-------+-------+-------+-------+
|       |       | r     | 0..1 | MAY   |       |       |       |       |
|       |       | elate |      |       |       |       |       |       |
|       |       | d​Doc |      |       |       |       |       |       |
|       |       | ument |      |       |       |       |       |       |
+-------+-------+-------+------+-------+-------+-------+-------+-------+
|       | @     | @typ  | 1.1  | SHALL | CS    | SHALL | XFRM  |       |
|       |       | ecode |      |       |       |       |       |       |
+-------+-------+-------+------+-------+-------+-------+-------+-------+
|       | >     | paren | 1..1 | SHALL |       |       |       |       |
|       |       | t​Doc |      |       |       |       |       |       |
|       |       | ument |      |       |       |       |       |       |
+-------+-------+-------+------+-------+-------+-------+-------+-------+
| Tra   | >>    | id    | 1..1 | SHALL | II    |       |       |       |
| nsfor |       |       |      |       |       |       |       |       |
| med​D |       |       |      |       |       |       |       |       |
| ocume |       |       |      |       |       |       |       |       |
| nt​ID |       |       |      |       |       |       |       |       |
+-------+-------+-------+------+-------+-------+-------+-------+-------+

.. _sect_8.3.1:

relatedDocument
~~~~~~~~~~~~~~~

A document may have two types of parent document:

-  A superseded version that the present document wholly replaces
   (typeCode =RPLC). Documents may go through stages of revision prior
   to being legally authenticated. Such early stages may be drafts from
   transcription, those created by residents, or other preliminary
   versions. Policies not covered by this specification may govern
   requirements for retention of such earlier versions. Except for
   forensic purposes, the latest version in a chain of revisions
   represents the complete and current report.

-  A source document from which the present document is transformed
   (typeCode = XFRM). A document may be created by transformation from a
   DICOM Structured Report (SR) document (see `SR to CDA Imaging Report
   Transformation Guide <#chapter_C>`__).

The CDA document management vocabulary includes a typeCode APND (append)
relationship to a parent document. This relationship type is not
supported in this specification; rather, append is effected by creating
a replacement document with an `Addendum <#sect_9.7>`__.

.. _sect_8.3.2:

parentDocument/setId and versionNumber
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

COND: If and only if the setID element is present, the versionNumber
element SHALL be present.

::

   <!-- transformation of a DICOM SR -->
   <relatedDocument typeCode="XFRM">
       <parentDocument>
           <id root="1.2.840.113619.2.62.994044785528.20060823.200608232232322.9"/>
           <!-- SOP Instance UID (0008,0018) of SR sample document -->
       </parentDocument>
   </relatedDocument>

