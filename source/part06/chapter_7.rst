.. _chapter_7:

Registry of DICOM File Meta Elements
====================================

This section specifies the File Meta Elements needed to support the
formatting of the File Meta Information of the DICOM File Format (see ).

.. table:: Registry of DICOM File Meta Elements

   +-------------+-------------+-------------+--------+--------+---+
   | **Tag**     | **Name**    | **Keyword** | **VR** | **VM** |   |
   +=============+=============+=============+========+========+===+
   | (0002,0000) | File Meta   | F           | UL     | 1      |   |
   |             | Information | ile​Meta​In |        |        |   |
   |             | Group       | formation​G |        |        |   |
   |             | Length      | roup​Length |        |        |   |
   +-------------+-------------+-------------+--------+--------+---+
   | (0002,0001) | File Meta   | File​Me     | OB     | 1      |   |
   |             | Information | ta​Informat |        |        |   |
   |             | Version     | ion​Version |        |        |   |
   +-------------+-------------+-------------+--------+--------+---+
   | (0002,0002) | Media       | Media       | UI     | 1      |   |
   |             | Storage SOP | ​Storage​SO |        |        |   |
   |             | Class UID   | P​Class​UID |        |        |   |
   +-------------+-------------+-------------+--------+--------+---+
   | (0002,0003) | Media       | Media​St    | UI     | 1      |   |
   |             | Storage SOP | orage​SOP​I |        |        |   |
   |             | Instance    | nstance​UID |        |        |   |
   |             | UID         |             |        |        |   |
   +-------------+-------------+-------------+--------+--------+---+
   | (0002,0010) | Transfer    | Transfer    | UI     | 1      |   |
   |             | Syntax UID  | ​Syntax​UID |        |        |   |
   +-------------+-------------+-------------+--------+--------+---+
   | (0002,0012) | Imp         | Im          | UI     | 1      |   |
   |             | lementation | plementatio |        |        |   |
   |             | Class UID   | n​Class​UID |        |        |   |
   +-------------+-------------+-------------+--------+--------+---+
   | (0002,0013) | Imp         | Imple       | SH     | 1      |   |
   |             | lementation | mentation​V |        |        |   |
   |             | Version     | ersion​Name |        |        |   |
   |             | Name        |             |        |        |   |
   +-------------+-------------+-------------+--------+--------+---+
   | (0002,0016) | Source      | Source​Ap   | AE     | 1      |   |
   |             | Application | plication​E |        |        |   |
   |             | Entity      | ntity​Title |        |        |   |
   |             | Title       |             |        |        |   |
   +-------------+-------------+-------------+--------+--------+---+
   | (0002,0017) | Sending     | Sending​Ap  | AE     | 1      |   |
   |             | Application | plication​E |        |        |   |
   |             | Entity      | ntity​Title |        |        |   |
   |             | Title       |             |        |        |   |
   +-------------+-------------+-------------+--------+--------+---+
   | (0002,0018) | Receiving   | R           | AE     | 1      |   |
   |             | Application | eceiving​Ap |        |        |   |
   |             | Entity      | plication​E |        |        |   |
   |             | Title       | ntity​Title |        |        |   |
   +-------------+-------------+-------------+--------+--------+---+
   | (0002,0026) | Source      | Sourc       | UR     | 1      |   |
   |             | P           | e​Presentat |        |        |   |
   |             | resentation | ion​Address |        |        |   |
   |             | Address     |             |        |        |   |
   +-------------+-------------+-------------+--------+--------+---+
   | (0002,0027) | Sending     | Sendin      | UR     | 1      |   |
   |             | P           | g​Presentat |        |        |   |
   |             | resentation | ion​Address |        |        |   |
   |             | Address     |             |        |        |   |
   +-------------+-------------+-------------+--------+--------+---+
   | (0002,0028) | Receiving   | Receivin    | UR     | 1      |   |
   |             | P           | g​Presentat |        |        |   |
   |             | resentation | ion​Address |        |        |   |
   |             | Address     |             |        |        |   |
   +-------------+-------------+-------------+--------+--------+---+
   | (0002,0031) | RTV Meta    | RTV​Me      | OB     | 1      |   |
   |             | Information | ta​Informat |        |        |   |
   |             | Version     | ion​Version |        |        |   |
   +-------------+-------------+-------------+--------+--------+---+
   | (0002,0032) | RTV         | RTV​Commu   | UI     | 1      |   |
   |             | Co          | nication​SO |        |        |   |
   |             | mmunication | P​Class​UID |        |        |   |
   |             | SOP Class   |             |        |        |   |
   |             | UID         |             |        |        |   |
   +-------------+-------------+-------------+--------+--------+---+
   | (0002,0033) | RTV         | R           | UI     | 1      |   |
   |             | Co          | TV​Communic |        |        |   |
   |             | mmunication | ation​SOP​I |        |        |   |
   |             | SOP         | nstance​UID |        |        |   |
   |             | Instance    |             |        |        |   |
   |             | UID         |             |        |        |   |
   +-------------+-------------+-------------+--------+--------+---+
   | (0002,0035) | RTV Source  | RTV​Source  | OB     | 1      |   |
   |             | Identifier  | ​Identifier |        |        |   |
   +-------------+-------------+-------------+--------+--------+---+
   | (0002,0036) | RTV Flow    | RTV​Flow    | OB     | 1      |   |
   |             | Identifier  | ​Identifier |        |        |   |
   +-------------+-------------+-------------+--------+--------+---+
   | (0002,0037) | RTV Flow    | RTV​        | UL     | 1      |   |
   |             | RTP         | Flow​RTP​Sa |        |        |   |
   |             | Sampling    | mpling​Rate |        |        |   |
   |             | Rate        |             |        |        |   |
   +-------------+-------------+-------------+--------+--------+---+
   | (0002,0038) | RTV Flow    | RTV​Flow    | FD     | 1      |   |
   |             | Actual      | ​Actual​Fra |        |        |   |
   |             | Frame       | me​Duration |        |        |   |
   |             | Duration    |             |        |        |   |
   +-------------+-------------+-------------+--------+--------+---+
   | (0002,0100) | Private     | Private​I   | UI     | 1      |   |
   |             | Information | nformation​ |        |        |   |
   |             | Creator UID | Creator​UID |        |        |   |
   +-------------+-------------+-------------+--------+--------+---+
   | (0002,0102) | Private     | Private​    | OB     | 1      |   |
   |             | Information | Information |        |        |   |
   +-------------+-------------+-------------+--------+--------+---+

