.. _chapter_I:

Store Instances Response Module
===============================

.. _sect_I.1:

Response Message Body
---------------------

`table_title <#table_I.1-1>`__ defines the Attributes for referencing
SOP Instances that are contained in a Store Instances Response Module in
the response message body.

.. table:: Store Instances Response Module Attributes

   +--------------------+-------------+----------+--------------------+
   | **Attribute Name** | **Tag**     | **Type** | **Attribute        |
   |                    |             |          | Description**      |
   +====================+=============+==========+====================+
   | Retrieve URL       | (0008,1190) | 2        | The URL where the  |
   |                    |             |          | Study is available |
   |                    |             |          | for retrieval via  |
   |                    |             |          | a Studies Retrieve |
   |                    |             |          | Transaction        |
   |                    |             |          | (`Retrieve         |
   |                    |             |          | Transaction        |
   |                    |             |          |  <#sect_10.4>`__). |
   |                    |             |          |                    |
   |                    |             |          | .. note::          |
   |                    |             |          |                    |
   |                    |             |          |    The VR of this  |
   |                    |             |          |    attribute has   |
   |                    |             |          |    changed from UT |
   |                    |             |          |    to UR.          |
   +--------------------+-------------+----------+--------------------+
   | Failed SOP         | (0008,1198) | 1C       | A Sequence of      |
   | Sequence           |             |          | Items where each   |
   |                    |             |          | Item references a  |
   |                    |             |          | single SOP         |
   |                    |             |          | Instance for which |
   |                    |             |          | storage could not  |
   |                    |             |          | be provided.       |
   |                    |             |          |                    |
   |                    |             |          | Required if one or |
   |                    |             |          | more SOP Instances |
   |                    |             |          | failed to store.   |
   +--------------------+-------------+----------+--------------------+
   | *>*                |             |          |                    |
   +--------------------+-------------+----------+--------------------+
   | >Failure Reason    | (0008,1197) | 1        | The reason that    |
   |                    |             |          | storage could not  |
   |                    |             |          | be provided for    |
   |                    |             |          | this SOP Instance. |
   |                    |             |          |                    |
   |                    |             |          | See `Failure       |
   |                    |             |          | Reason             |
   |                    |             |          |  <#sect_I.2.2>`__. |
   +--------------------+-------------+----------+--------------------+
   | Referenced SOP     | (0008,1199) | 1C       | A Sequence of      |
   | Sequence           |             |          | Items where each   |
   |                    |             |          | Item references a  |
   |                    |             |          | single SOP         |
   |                    |             |          | Instance that was  |
   |                    |             |          | successfully       |
   |                    |             |          | stored.            |
   |                    |             |          |                    |
   |                    |             |          | Required if one or |
   |                    |             |          | more SOP Instances |
   |                    |             |          | were successfully  |
   |                    |             |          | stored.            |
   +--------------------+-------------+----------+--------------------+
   | *>*                |             |          |                    |
   +--------------------+-------------+----------+--------------------+
   | >Retrieve URL      | (0008,1190) | 2        | The URL where the  |
   |                    |             |          | SOP Instance is    |
   |                    |             |          | available for      |
   |                    |             |          | retrieval via a    |
   |                    |             |          | Studies Retrieve   |
   |                    |             |          | Transaction        |
   |                    |             |          | (`Retrieve         |
   |                    |             |          | Transaction        |
   |                    |             |          |  <#sect_10.4>`__). |
   |                    |             |          |                    |
   |                    |             |          | .. note::          |
   |                    |             |          |                    |
   |                    |             |          |    The VR of this  |
   |                    |             |          |    attribute has   |
   |                    |             |          |    changed from UT |
   |                    |             |          |    to UR.          |
   +--------------------+-------------+----------+--------------------+
   | >Warning Reason    | (0008,1196) | 1C       | The reason that    |
   |                    |             |          | this SOP Instance  |
   |                    |             |          | was accepted with  |
   |                    |             |          | warnings.          |
   |                    |             |          |                    |
   |                    |             |          | Required if there  |
   |                    |             |          | was a warning for  |
   |                    |             |          | this SOP Instance. |
   |                    |             |          |                    |
   |                    |             |          | See `Warning       |
   |                    |             |          | Reason             |
   |                    |             |          |  <#sect_I.2.1>`__. |
   +--------------------+-------------+----------+--------------------+
   | >Original          | (0400,0561) | 3        | Sequence of Items  |
   | Attributes         |             |          | containing all     |
   | Sequence           |             |          | attributes that    |
   |                    |             |          | were removed or    |
   |                    |             |          | replaced by other  |
   |                    |             |          | values.            |
   |                    |             |          |                    |
   |                    |             |          | One or more Items  |
   |                    |             |          | are permitted in   |
   |                    |             |          | this sequence.     |
   +--------------------+-------------+----------+--------------------+
   | >>Attribute        | (0400,0562) | 1        | Date and time the  |
   | Modification       |             |          | attributes were    |
   | DateTime           |             |          | removed and/or     |
   |                    |             |          | replaced.          |
   +--------------------+-------------+----------+--------------------+
   | >>Modifying System | (0400,0563) | 1        | Identification of  |
   |                    |             |          | the system that    |
   |                    |             |          | removed and/or     |
   |                    |             |          | replaced the       |
   |                    |             |          | attributes.        |
   +--------------------+-------------+----------+--------------------+
   | >>Reason for the   | (0400,0565) | 1        | Reason for the     |
   | Attribute          |             |          | attribute          |
   | Modification       |             |          | modification.      |
   |                    |             |          |                    |
   |                    |             |          | COERCE             |
   |                    |             |          |    Replace values  |
   |                    |             |          |    of attributes   |
   |                    |             |          |    such as Patient |
   |                    |             |          |    Name, ID,       |
   |                    |             |          |    Accession       |
   |                    |             |          |    Number, for     |
   |                    |             |          |    example, during |
   |                    |             |          |    import of media |
   |                    |             |          |    from an         |
   |                    |             |          |    external        |
   |                    |             |          |    institution, or |
   |                    |             |          |    reconciliation  |
   |                    |             |          |    against a       |
   |                    |             |          |    master patient  |
   |                    |             |          |    index.          |
   |                    |             |          |                    |
   |                    |             |          | CORRECT            |
   |                    |             |          |    Replace         |
   |                    |             |          |    incorrect       |
   |                    |             |          |    values, such as |
   |                    |             |          |    Patient Name or |
   |                    |             |          |    ID, for         |
   |                    |             |          |    example, when   |
   |                    |             |          |    incorrect       |
   |                    |             |          |    worklist item   |
   |                    |             |          |    was chosen or   |
   |                    |             |          |    operator input  |
   |                    |             |          |    error.          |
   +--------------------+-------------+----------+--------------------+
   | >>Modified         | (0400,0550) | 1        | Sequence that      |
   | Attributes         |             |          | contains all the   |
   | Sequence           |             |          | Attributes, with   |
   |                    |             |          | their previous     |
   |                    |             |          | values, that were  |
   |                    |             |          | modified or        |
   |                    |             |          | removed from the   |
   |                    |             |          | main Data Set.     |
   |                    |             |          |                    |
   |                    |             |          | Only a single Item |
   |                    |             |          | shall be included  |
   |                    |             |          | in this sequence.  |
   +--------------------+-------------+----------+--------------------+
   | *>>Any Attribute   |             |          |                    |
   | from the main Data |             |          |                    |
   | Set that was       |             |          |                    |
   | modified or        |             |          |                    |
   | removed; may       |             |          |                    |
   | include Sequence   |             |          |                    |
   | Attributes and     |             |          |                    |
   | their Items.*      |             |          |                    |
   +--------------------+-------------+----------+--------------------+
   | Other Failures     | (0008,119A) | 1C       | Reasons not        |
   | Sequence           |             |          | associated with a  |
   |                    |             |          | specific SOP       |
   |                    |             |          | Instance that      |
   |                    |             |          | storage could not  |
   |                    |             |          | be provided.       |
   |                    |             |          |                    |
   |                    |             |          | Each Item          |
   |                    |             |          | references a       |
   |                    |             |          | single storage     |
   |                    |             |          | failure.           |
   |                    |             |          |                    |
   |                    |             |          | Required if there  |
   |                    |             |          | are one or more    |
   |                    |             |          | failures not       |
   |                    |             |          | associated with a  |
   |                    |             |          | specific SOP       |
   |                    |             |          | Instance.          |
   +--------------------+-------------+----------+--------------------+
   | >Failure Reason    | (0008,1197) | 1        | The reason that    |
   |                    |             |          | storage could not  |
   |                    |             |          | be provided for    |
   |                    |             |          | this message item. |
   |                    |             |          |                    |
   |                    |             |          | See `Failure       |
   |                    |             |          | Reason             |
   |                    |             |          |  <#sect_I.2.2>`__. |
   +--------------------+-------------+----------+--------------------+

.. _sect_I.2:

Store Instances Response Attribute Description
----------------------------------------------

.. _sect_I.2.1:

Warning Reason
~~~~~~~~~~~~~~

`table_title <#table_I.2-1>`__ defines the semantics for which the
associated value shall be used for the Warning Reason (0008,1196):

.. table:: Store Instances Response Warning Reason Values

   +----------------+----------------+----------------+----------------+
   | **Status Code  | **Status Code  | **Meaning**    | *              |
   | (              | (decimal)**    |                | *Explanation** |
   | hexadecimal)** |                |                |                |
   +================+================+================+================+
   | B000           | 45056          | Coercion of    | The Studies    |
   |                |                | Data Elements  | Store          |
   |                |                |                | Transaction    |
   |                |                |                | (`Store        |
   |                |                |                | Transaction <# |
   |                |                |                | sect_10.5>`__) |
   |                |                |                | modified one   |
   |                |                |                | or more data   |
   |                |                |                | elements       |
   |                |                |                | during storage |
   |                |                |                | of the         |
   |                |                |                | instance. See  |
   |                |                |                | `Response <#se |
   |                |                |                | ct_10.5.3>`__. |
   +----------------+----------------+----------------+----------------+
   | B006           | 45062          | Elements       | The Studies    |
   |                |                | Discarded      | Store          |
   |                |                |                | Transaction    |
   |                |                |                | (`Store        |
   |                |                |                | Transaction <# |
   |                |                |                | sect_10.5>`__) |
   |                |                |                | discarded some |
   |                |                |                | data elements  |
   |                |                |                | during storage |
   |                |                |                | of the         |
   |                |                |                | instance. See  |
   |                |                |                | `Response <#se |
   |                |                |                | ct_10.5.3>`__. |
   +----------------+----------------+----------------+----------------+
   | B007           | 45063          | Data Set does  | The Studies    |
   |                |                | not match SOP  | Store          |
   |                |                | Class          | Transaction    |
   |                |                |                | (`Store        |
   |                |                |                | Transaction <# |
   |                |                |                | sect_10.5>`__) |
   |                |                |                | observed that  |
   |                |                |                | the Data Set   |
   |                |                |                | did not match  |
   |                |                |                | the            |
   |                |                |                | constraints of |
   |                |                |                | the SOP Class  |
   |                |                |                | during storage |
   |                |                |                | of the         |
   |                |                |                | instance.      |
   +----------------+----------------+----------------+----------------+

Additional codes may be used for the Warning Reason (0008,1196) to
address the semantics of other issues.

In the event that multiple codes may apply, the single most appropriate
code shall be used.

.. _sect_I.2.2:

Failure Reason
~~~~~~~~~~~~~~

`table_title <#table_I.2-2>`__ defines the semantics for which the
associated value shall be used for the Failure Reason (0008,1197).
Implementation specific warning and error codes shall be defined in the
conformance statement:

.. table:: Store Instances Response Failure Reason Values

   +----------------+----------------+----------------+----------------+
   | **Status Code  | **Status Code  | **Meaning**    | *              |
   | (              | (decimal)**    |                | *Explanation** |
   | hexadecimal)** |                |                |                |
   +================+================+================+================+
   | A7xx           | 42752 - 43007  | Refused out of | The Studies    |
   |                |                | Resources      | Store          |
   |                |                |                | Transaction    |
   |                |                |                | (`Store        |
   |                |                |                | Transaction <# |
   |                |                |                | sect_10.5>`__) |
   |                |                |                | did not store  |
   |                |                |                | the instance   |
   |                |                |                | because it was |
   |                |                |                | out of         |
   |                |                |                | resources.     |
   +----------------+----------------+----------------+----------------+
   | A9xx           | 43264 - 43519  | Error: Data    | The Studies    |
   |                |                | Set does not   | Store          |
   |                |                | match SOP      | Transaction    |
   |                |                | Class          | (`Store        |
   |                |                |                | Transaction <# |
   |                |                |                | sect_10.5>`__) |
   |                |                |                | did not store  |
   |                |                |                | the instance   |
   |                |                |                | because the    |
   |                |                |                | instance does  |
   |                |                |                | not conform to |
   |                |                |                | its specified  |
   |                |                |                | SOP Class.     |
   +----------------+----------------+----------------+----------------+
   | Cxxx           | 49152 - 53247  | Error: Cannot  | The Studies    |
   |                |                | understand     | Store          |
   |                |                |                | Transaction    |
   |                |                |                | (`Store        |
   |                |                |                | Transaction <# |
   |                |                |                | sect_10.5>`__) |
   |                |                |                | did not store  |
   |                |                |                | the instance   |
   |                |                |                | because it     |
   |                |                |                | cannot         |
   |                |                |                | understand     |
   |                |                |                | certain Data   |
   |                |                |                | Elements.      |
   +----------------+----------------+----------------+----------------+
   | C122           | 49442          | Referenced     | The Studies    |
   |                |                | Transfer       | Store          |
   |                |                | Syntax not     | Transaction    |
   |                |                | supported      | (`Store        |
   |                |                |                | Transaction <# |
   |                |                |                | sect_10.5>`__) |
   |                |                |                | did not store  |
   |                |                |                | the instance   |
   |                |                |                | because it     |
   |                |                |                | does not       |
   |                |                |                | support the    |
   |                |                |                | requested      |
   |                |                |                | Transfer       |
   |                |                |                | Syntax for the |
   |                |                |                | instance.      |
   +----------------+----------------+----------------+----------------+
   | 0110           | 272            | Processing     | The Studies    |
   |                |                | failure        | Store          |
   |                |                |                | Transaction    |
   |                |                |                | (`Store        |
   |                |                |                | Transaction <# |
   |                |                |                | sect_10.5>`__) |
   |                |                |                | did not store  |
   |                |                |                | the instance   |
   |                |                |                | because of a   |
   |                |                |                | general        |
   |                |                |                | failure in     |
   |                |                |                | processing the |
   |                |                |                | operation.     |
   +----------------+----------------+----------------+----------------+
   | 0122           | 290            | Referenced SOP | The Studies    |
   |                |                | Class not      | Store          |
   |                |                | supported      | Transaction    |
   |                |                |                | (`Store        |
   |                |                |                | Transaction <# |
   |                |                |                | sect_10.5>`__) |
   |                |                |                | did not store  |
   |                |                |                | the instance   |
   |                |                |                | because it     |
   |                |                |                | does not       |
   |                |                |                | support the    |
   |                |                |                | requested SOP  |
   |                |                |                | Class.         |
   +----------------+----------------+----------------+----------------+

Additional codes may be used for the Failure Reason (0008,1197) to
address the semantics of other issues.

In the event that multiple codes may apply, the single most appropriate
code shall be used.

.. _sect_I.3:

Response Message Body Example
-----------------------------

The following is an example of a XML Store Instances Response Module in
the response message body containing 2 failed SOP Instances, 1
successful SOP Instance, and 1 accepted SOP Instance with a warning:

::

   <?xml version="1.0" encoding="utf-8" xml:space="preserve"?>
   <NativeDicomModel xmlns="http://dicom.nema.org/PS3.19/models/NativeDICOM"
   xsi:schemaLocation="http://dicom.nema.org/PS3.19/models/NativeDICOM"
   xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance">
     <DicomAttribute tag="00081198" vr="SQ" keyword="FailedSOPSequence">
       <Item number="1">
         <DicomAttribute tag="00081150" vr="UI" keyword="ReferencedSOPClassUID">
           <Value number="1">1.2.840.10008.3.1.2.3.1</Value>
         </DicomAttribute>
         <DicomAttribute tag="00081155" vr="UI"
         keyword="ReferencedSOPInstanceUID">
           <Value number="1">
           2.16.124.113543.6003.1011758472.49886.19426.2085542308</Value>
         </DicomAttribute>
         <DicomAttribute tag="00081197" vr="US" keyword="FailureReason">
           <Value number="1">290</Value>
         </DicomAttribute>
       </Item>
       <Item number="2">
         <DicomAttribute tag="00081150" vr="UI" keyword="ReferencedSOPClassUID">
           <Value number="1">1.2.840.10008.3.1.2.3.1</Value>
         </DicomAttribute>
         <DicomAttribute tag="00081155" vr="UI"
         keyword="ReferencedSOPInstanceUID">
           <Value number="1">
           2.16.124.113543.6003.1011758472.49886.19426.2085542309</Value>
         </DicomAttribute>
         <DicomAttribute tag="00081197" vr="US" keyword="FailureReason">
           <Value number="1">290</Value>
         </DicomAttribute>
       </Item>
     </DicomAttribute>
     <DicomAttribute tag="00081199" vr="SQ" keyword="ReferencedSOPSequence">
       <Item number="1">
         <DicomAttribute tag="00081150" vr="UI" keyword="ReferencedSOPClassUID">
           <Value number="1">1.2.840.10008.5.1.4.1.1.2</Value>
         </DicomAttribute>
         <DicomAttribute tag="00081155" vr="UI"
         keyword="ReferencedSOPInstanceUID">
           <Value number="1">
           2.16.124.113543.6003.189642796.63084.16748.2599092903</Value>
         </DicomAttribute>
         <DicomAttribute tag="00081190" vr="UR" keyword="RetrieveURL">
           <Value number="1">
           https://wadors.hospital.com/studies/2.16.124.113543.6003.1154777499.30246.19789.3503430045/
           series/2.16.124.113543.6003.2588828330.45298.17418.2723805630/
           instances/2.16.124.113543.6003.189642796.63084.16748.2599092903</Value>
         </DicomAttribute>
       </Item>
       <Item number="2">
         <DicomAttribute tag="00081150" vr="UI" keyword="ReferencedSOPClassUID">
           <Value number="1">1.2.840.10008.5.1.4.1.1.2</Value>
         </DicomAttribute>
         <DicomAttribute tag="00081155" vr="UI"
         keyword="ReferencedSOPInstanceUID">
           <Value number="1">
           2.16.124.113543.6003.189642796.63084.16748.2599092905</Value>
         </DicomAttribute>
         <DicomAttribute tag="00081196" vr="US" keyword="WarningReason">
           <Value number="1">45056</Value>
         </DicomAttribute>
         <DicomAttribute tag="00081190" vr="UR" keyword="RetrieveURL">
           <Value number="1">
           https://wadors.hospital.com/studies/2.16.124.113543.6003.1154777499.30246.19789.3503430045/
           series/2.16.124.113543.6003.2588828330.45298.17418.2723805630/
           instances/2.16.124.113543.6003.189642796.63084.16748.2599092905</Value>
         </DicomAttribute>
       </Item>
     </DicomAttribute>
     <DicomAttribute tag="00081190" vr="UR" keyword="RetrieveURL">
       <Value number="1">
       https://wadors.hospital.com/studies/2.16.124.113543.6003.1154777499.30246.19789.3503430045</Value>
     </DicomAttribute>
   </NativeDicomModel>
