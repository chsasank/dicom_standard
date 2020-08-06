.. _chapter_8:

Registry of DICOM Directory Structuring Elements
================================================

For retired elements, the last edition of the Standard that documented
the element is indicated in parentheses.

.. table:: Registry of DICOM Directory Structuring Elements

   +-----------+-----------+-----------+--------+--------+-----------+
   | **Tag**   | **Name**  | **        | **VR** | **VM** |           |
   |           |           | Keyword** |        |        |           |
   +===========+===========+===========+========+========+===========+
   | (0        | File-set  | Fi        | CS     | 1      |           |
   | 004,1130) | ID        | le​Set​ID |        |        |           |
   +-----------+-----------+-----------+--------+--------+-----------+
   | (0        | File-set  | File​Set​ | CS     | 1-8    |           |
   | 004,1141) | D         | Descripto |        |        |           |
   |           | escriptor | r​File​ID |        |        |           |
   |           | File ID   |           |        |        |           |
   +-----------+-----------+-----------+--------+--------+-----------+
   | (0        | Specific  | Speci     | CS     | 1      |           |
   | 004,1142) | Character | fic​Chara |        |        |           |
   |           | Set of    | cter​Set​ |        |        |           |
   |           | File-set  | Of​File​S |        |        |           |
   |           | D         | et​Descri |        |        |           |
   |           | escriptor | ptor​File |        |        |           |
   |           | File      |           |        |        |           |
   +-----------+-----------+-----------+--------+--------+-----------+
   | (0        | Offset of | Of        | UL     | 1      |           |
   | 004,1200) | the First | fset​Of​T |        |        |           |
   |           | Directory | he​First​ |        |        |           |
   |           | Record of | Directory |        |        |           |
   |           | the Root  | ​Record​O |        |        |           |
   |           | Directory | f​The​Roo |        |        |           |
   |           | Entity    | t​Directo |        |        |           |
   |           |           | ry​Entity |        |        |           |
   +-----------+-----------+-----------+--------+--------+-----------+
   | (0        | Offset of | O         | UL     | 1      |           |
   | 004,1202) | the Last  | ffset​Of​ |        |        |           |
   |           | Directory | The​Last​ |        |        |           |
   |           | Record of | Directory |        |        |           |
   |           | the Root  | ​Record​O |        |        |           |
   |           | Directory | f​The​Roo |        |        |           |
   |           | Entity    | t​Directo |        |        |           |
   |           |           | ry​Entity |        |        |           |
   +-----------+-----------+-----------+--------+--------+-----------+
   | (0        | File-set  | File​Se   | US     | 1      |           |
   | 004,1212) | Co        | t​Consist |        |        |           |
   |           | nsistency | ency​Flag |        |        |           |
   |           | Flag      |           |        |        |           |
   +-----------+-----------+-----------+--------+--------+-----------+
   | (0        | Directory | Directo   | SQ     | 1      |           |
   | 004,1220) | Record    | ry​Record |        |        |           |
   |           | Sequence  | ​Sequence |        |        |           |
   +-----------+-----------+-----------+--------+--------+-----------+
   | (0        | Offset of | Offset​O  | UL     | 1      |           |
   | 004,1400) | the Next  | f​The​Nex |        |        |           |
   |           | Directory | t​Directo |        |        |           |
   |           | Record    | ry​Record |        |        |           |
   +-----------+-----------+-----------+--------+--------+-----------+
   | (0        | Record    | Record​In | US     | 1      |           |
   | 004,1410) | In-use    | ​Use​Flag |        |        |           |
   |           | Flag      |           |        |        |           |
   +-----------+-----------+-----------+--------+--------+-----------+
   | (0        | Offset of | Offs      | UL     | 1      |           |
   | 004,1420) | R         | et​Of​Ref |        |        |           |
   |           | eferenced | erenced​L |        |        |           |
   |           | Lo        | ower​Leve |        |        |           |
   |           | wer-Level | l​Directo |        |        |           |
   |           | Directory | ry​Entity |        |        |           |
   |           | Entity    |           |        |        |           |
   +-----------+-----------+-----------+--------+--------+-----------+
   | (0        | Directory | Dir       | CS     | 1      |           |
   | 004,1430) | Record    | ectory​Re |        |        |           |
   |           | Type      | cord​Type |        |        |           |
   +-----------+-----------+-----------+--------+--------+-----------+
   | (0        | Private   | Private​R | UI     | 1      |           |
   | 004,1432) | Record    | ecord​UID |        |        |           |
   |           | UID       |           |        |        |           |
   +-----------+-----------+-----------+--------+--------+-----------+
   | (0        | R         | Reference | CS     | 1-8    |           |
   | 004,1500) | eferenced | d​File​ID |        |        |           |
   |           | File ID   |           |        |        |           |
   +-----------+-----------+-----------+--------+--------+-----------+
   | *(00      | *MRDR     | *MR       | *UL*   | *1*    | *RET      |
   | 04,1504)* | Directory | DR​Direct |        |        | (2004)*   |
   |           | Record    | ory​Recor |        |        |           |
   |           | Offset*   | d​Offset* |        |        |           |
   +-----------+-----------+-----------+--------+--------+-----------+
   | (0        | R         | Refer     | UI     | 1      |           |
   | 004,1510) | eferenced | enced​SOP |        |        |           |
   |           | SOP Class | ​Class​UI |        |        |           |
   |           | UID in    | D​In​File |        |        |           |
   |           | File      |           |        |        |           |
   +-----------+-----------+-----------+--------+--------+-----------+
   | (0        | R         | Referenc  | UI     | 1      |           |
   | 004,1511) | eferenced | ed​SOP​In |        |        |           |
   |           | SOP       | stance​UI |        |        |           |
   |           | Instance  | D​In​File |        |        |           |
   |           | UID in    |           |        |        |           |
   |           | File      |           |        |        |           |
   +-----------+-----------+-----------+--------+--------+-----------+
   | (0        | R         | Re        | UI     | 1      |           |
   | 004,1512) | eferenced | ferenced​ |        |        |           |
   |           | Transfer  | Transfer​ |        |        |           |
   |           | Syntax    | Syntax​UI |        |        |           |
   |           | UID in    | D​In​File |        |        |           |
   |           | File      |           |        |        |           |
   +-----------+-----------+-----------+--------+--------+-----------+
   | (0        | R         | Ref       | UI     | 1-n    |           |
   | 004,151A) | eferenced | erenced​R |        |        |           |
   |           | Related   | elated​Ge |        |        |           |
   |           | General   | neral​SOP |        |        |           |
   |           | SOP Class | ​Class​UI |        |        |           |
   |           | UID in    | D​In​File |        |        |           |
   |           | File      |           |        |        |           |
   +-----------+-----------+-----------+--------+--------+-----------+
   | *(00      | *Number   | *Num      | *UL*   | *1*    | *RET      |
   | 04,1600)* | of        | ber​Of​Re |        |        | (2004)*   |
   |           | Re        | ferences* |        |        |           |
   |           | ferences* |           |        |        |           |
   +-----------+-----------+-----------+--------+--------+-----------+

