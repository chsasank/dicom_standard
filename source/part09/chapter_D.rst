.. _chapter_D:

Use and Format of the A-ASSOCIATE User Information Parameter (Normative)
========================================================================

This parameter allows for the negotiation of a number of features
related to the communication of DICOM Application Entities at
association establishment.

.. _sect_D.1:

Maximum Length Negotiation
--------------------------

This negotiation allows the receivers to limit the size of the
Presentation Data Values List parameters of each P-DATA Indication. The
association-requestor shall specify in the user information parameter of
the A-ASSOCIATE request primitive the maximum length in bytes for the
PDV list parameter it is ready to receive in each P-DATA indication. The
association-acceptor shall ensure in its fragmentation of the DICOM
Messages that the list of PDVs included in each P-DATA request does not
exceed this maximum length. Likewise, the association-acceptor can
specify in the user information parameter of A-ASSOCIATE response
primitive the maximum length in bytes for the PDV list parameter it is
ready to receive in each P-DATA indication. The association-requestor
shall ensure in its fragmentation of the DICOM Messages that the list of
PDVs included in each P-DATA request does not exceed this maximum
length. Different maximum lengths can be specified for each direction of
data flow on the association.

The Maximum Length Item support is required for all DICOM V3.0
conforming implementations.

.. _sect_D.1.1:

Maximum Length Sub-Item Structure (A-ASSOCIATE-RQ)
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

The Maximum Length Sub-Item shall be made of a sequence of mandatory
fixed length fields. Only one Maximum Length Sub-Item shall be present
in the User Data information in the A-ASSOCIATE-RQ.
`table_title <#table_D.1-1>`__ shows the sequence of the mandatory
fields.

.. table:: Maximum Length Sub-Item Fields (A-ASSOCIATE-RQ)

   +----------------+-------------------------+-------------------------+
   | **Item bytes** | **Field name**          | **Description of        |
   |                |                         | field**                 |
   +================+=========================+=========================+
   | 1              | Item-type               | 51H                     |
   +----------------+-------------------------+-------------------------+
   | 2              | Reserved                | This reserved field     |
   |                |                         | shall be sent with a    |
   |                |                         | value 00H but not       |
   |                |                         | tested to this value    |
   |                |                         | when received.          |
   +----------------+-------------------------+-------------------------+
   | 3-4            | Item-length             | This Item-length shall  |
   |                |                         | be the number of bytes  |
   |                |                         | from the first byte of  |
   |                |                         | the following field to  |
   |                |                         | the last byte of the    |
   |                |                         | Maximum-length-received |
   |                |                         | field. In the case of   |
   |                |                         | this Item, it shall     |
   |                |                         | have the fixed value of |
   |                |                         | 00000004H encoded as an |
   |                |                         | unsigned binary number. |
   +----------------+-------------------------+-------------------------+
   | 5-8            | Maximum-length-received | This parameter allows   |
   |                |                         | the                     |
   |                |                         | association-requestor   |
   |                |                         | to restrict the maximum |
   |                |                         | length of the variable  |
   |                |                         | field of the P-DATA-TF  |
   |                |                         | PDUs sent by the        |
   |                |                         | acceptor on the         |
   |                |                         | association once        |
   |                |                         | established. This       |
   |                |                         | length value is         |
   |                |                         | indicated as a number   |
   |                |                         | of bytes encoded as an  |
   |                |                         | unsigned binary number. |
   |                |                         | The value of (0)        |
   |                |                         | indicates that no       |
   |                |                         | maximum length is       |
   |                |                         | specified. This maximum |
   |                |                         | length value shall      |
   |                |                         | never be exceeded by    |
   |                |                         | the PDU length values   |
   |                |                         | used in the PDU-length  |
   |                |                         | field of the P-DATA-TF  |
   |                |                         | PDUs received by the    |
   |                |                         | association-requestor.  |
   |                |                         | Otherwise, it shall be  |
   |                |                         | a protocol error.       |
   +----------------+-------------------------+-------------------------+

.. _sect_D.1.2:

Maximum Length Sub-Item Structure (A-ASSOCIATE-AC)
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

The Maximum Length Sub-Item shall be made of a sequence of mandatory
fixed length fields. Only one Maximum Length Sub-Item shall be present
in the User Data information in the A-ASSOCIATE-AC.
`table_title <#table_D.1-2>`__ shows the sequence of the mandatory
fields.

.. table:: Maximum Length Sub-Item Fields (A-ASSOCIATE-AC)

   +----------------+-------------------------+-------------------------+
   | **Item bytes** | **Field name**          | **Description of        |
   |                |                         | field**                 |
   +================+=========================+=========================+
   | 1              | Item-type               | 51H                     |
   +----------------+-------------------------+-------------------------+
   | 2              | Reserved                | This reserved field     |
   |                |                         | shall be sent with a    |
   |                |                         | value 00H but not       |
   |                |                         | tested to this value    |
   |                |                         | when received.          |
   +----------------+-------------------------+-------------------------+
   | 3-4            | Item-length             | This Item-length shall  |
   |                |                         | be the number of bytes  |
   |                |                         | from the first byte of  |
   |                |                         | the following field to  |
   |                |                         | the last byte of the    |
   |                |                         | Maximum-length-received |
   |                |                         | field. In the case of   |
   |                |                         | this Item, it shall     |
   |                |                         | have the fixed value of |
   |                |                         | 00000004H encoded as an |
   |                |                         | unsigned binary number. |
   +----------------+-------------------------+-------------------------+
   | 5-8            | Maximum-length-received | This parameter allows   |
   |                |                         | the                     |
   |                |                         | association-acceptor to |
   |                |                         | restrict the maximum    |
   |                |                         | length of the variable  |
   |                |                         | field of the P-DATA-TF  |
   |                |                         | PDUs sent by the        |
   |                |                         | requestor on the        |
   |                |                         | association once        |
   |                |                         | established. This       |
   |                |                         | length value is         |
   |                |                         | indicated as a number   |
   |                |                         | of bytes encoded as an  |
   |                |                         | unsigned binary number. |
   |                |                         | The value of (0)        |
   |                |                         | indicates that no       |
   |                |                         | maximum length is       |
   |                |                         | specified. This maximum |
   |                |                         | length value shall      |
   |                |                         | never be exceeded by    |
   |                |                         | the PDU length values   |
   |                |                         | used in the PDU-length  |
   |                |                         | field of the P-DATA-TF  |
   |                |                         | PDUs received by the    |
   |                |                         | association-acceptor.   |
   |                |                         | Otherwise, it shall be  |
   |                |                         | a protocol error.       |
   +----------------+-------------------------+-------------------------+

.. _sect_D.2:

Extended User Information Negotiation
-------------------------------------

The user information parameter, of the A-ASSOCIATE primitive, can be
extended to support the negotiation needs of DICOM Application Entities
using the UL Service. This will result in the definition of specific
user information sub-items. These sub-items shall be assigned unique
item-type values registered in .

.. note::

   1. The values of the Sub-Items types in the User Information Field
      are assigned by this Standard in the range of 51H through FFH.
      Sub-Item values are defined by and .

   2. Succeeding editions of the Standard may define additional user
      information Sub-Items in a manner that does not affect the
      semantics of previously defined Sub-Items. Association acceptors
      compliant to an earlier edition of the Standard are required to
      ignore such unrecognized user information Sub-Items and not reject
      an Association because of their presence.

