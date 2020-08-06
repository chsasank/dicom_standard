.. _chapter_7:

Document-level Templates
========================

Document-level templates describe the purpose and rules for constructing
a conforming CDA document. Document templates include constraints on the
CDA header and sections by referring to templates, and constraints on
the vocabulary used in those templates.

.. _sect_7.1:

Imaging Report
--------------

+----------------------+----------------------------------------------+
| **Template ID**      | 1.2.840.10008.9.1                            |
+----------------------+----------------------------------------------+
| **Name**             | Imaging Report                               |
+----------------------+----------------------------------------------+
| **Effective Date**   | 2015/03/24                                   |
+----------------------+----------------------------------------------+
| **Version Label**    | DICOM-20150324                               |
+----------------------+----------------------------------------------+
| **Status**           | Active                                       |
+----------------------+----------------------------------------------+
| **Description**      | This CDA Imaging Report document template    |
|                      | defines the report content and technical     |
|                      | constraints for top level elements,          |
|                      | attributes, sections, and entries to be used |
|                      | in imaging report instances. This template   |
|                      | may apply to screening, diagnostic, or       |
|                      | therapeutic radiology, cardiology, or other  |
|                      | imaging reports.                             |
|                      |                                              |
|                      | The body of an Imaging Report may contain    |
|                      | five main imaging report sections:           |
|                      |                                              |
|                      | -  Clinical information (optionally);        |
|                      |                                              |
|                      | -  Current imaging procedure description;    |
|                      |                                              |
|                      | -  Comparison studies (optionally);          |
|                      |                                              |
|                      | -  Findings (optionally);                    |
|                      |                                              |
|                      | -  Impression;                               |
|                      |                                              |
|                      | -  plus potentially an Addendum(s)           |
|                      |                                              |
|                      | The report templates sponsored by the RSNA   |
|                      | Radiology Reporting Initiative               |
|                      | (http://www.radreport.org) adhere to this    |
|                      | general section outline.                     |
|                      |                                              |
|                      | The section and subsection structure of this |
|                      | template is also identified by LOINC panel   |
|                      | code                                         |
|                      | `87416-4 <http://loinc.org/87416-4/>`__.     |
+----------------------+----------------------------------------------+
| **Classification**   | CDA Document Level                           |
+----------------------+----------------------------------------------+
| **Relationships**    |                                              |
+----------------------+----------------------------------------------+
| **Context**          | parent node                                  |
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
| **I   |       | Cl    |       |       |       |       |       |       |
| magin |       | inica |       |       |       |       |       |       |
| g​Rep |       | l​Doc |       |       |       |       |       |       |
| ort** |       | ument |       |       |       |       |       |       |
+-------+-------+-------+-------+-------+-------+-------+-------+-------+
|       | >     | t     | 1..1  | SHALL | II    |       |       |       |
|       |       | empla |       |       |       |       |       |       |
|       |       | te​Id |       |       |       |       |       |       |
+-------+-------+-------+-------+-------+-------+-------+-------+-------+
|       | >@    | @root | 1..1  | SHALL | UID   | SHALL | 1.    |       |
|       |       |       |       |       |       |       | 2.840 |       |
|       |       |       |       |       |       |       | .1000 |       |
|       |       |       |       |       |       |       | 8.9.1 |       |
+-------+-------+-------+-------+-------+-------+-------+-------+-------+
| Doc   | >     | code  | 1..1  | SHALL | CD    | SHALL | `Val  |       |
| ​Type |       |       |       |       |       | CWE   | ueSet |       |
|       |       |       |       |       |       | n     | LOINC |       |
|       |       |       |       |       |       | oNull | Im    |       |
|       |       |       |       |       |       |       | aging |       |
|       |       |       |       |       |       |       | Doc   |       |
|       |       |       |       |       |       |       | ument |       |
|       |       |       |       |       |       |       | Codes |       |
|       |       |       |       |       |       |       | 1.3   |       |
|       |       |       |       |       |       |       | .6.1. |       |
|       |       |       |       |       |       |       | 4.1.1 |       |
|       |       |       |       |       |       |       | 2009. |       |
|       |       |       |       |       |       |       | 10.2. |       |
|       |       |       |       |       |       |       | 5 <ht |       |
|       |       |       |       |       |       |       | tps:/ |       |
|       |       |       |       |       |       |       | /loin |       |
|       |       |       |       |       |       |       | c.org |       |
|       |       |       |       |       |       |       | /oids |       |
|       |       |       |       |       |       |       | /1.3. |       |
|       |       |       |       |       |       |       | 6.1.4 |       |
|       |       |       |       |       |       |       | .1.12 |       |
|       |       |       |       |       |       |       | 009.1 |       |
|       |       |       |       |       |       |       | 0.2.5 |       |
|       |       |       |       |       |       |       | />`__ |       |
+-------+-------+-------+-------+-------+-------+-------+-------+-------+
|       | >     |       | 1..1  | SHALL |       |       |       | `Ge   |
|       |       |       |       |       |       |       |       | neral |
|       |       |       |       |       |       |       |       | H     |
|       |       |       |       |       |       |       |       | eader |
|       |       |       |       |       |       |       |       |  <#se |
|       |       |       |       |       |       |       |       | ct_8. |
|       |       |       |       |       |       |       |       | 1>`__ |
|       |       |       |       |       |       |       |       | 1.2   |
|       |       |       |       |       |       |       |       | .840. |
|       |       |       |       |       |       |       |       | 10008 |
|       |       |       |       |       |       |       |       | .9.20 |
+-------+-------+-------+-------+-------+-------+-------+-------+-------+
|       | >     |       | 1..1  | SHALL |       |       |       | `Im   |
|       |       |       |       |       |       |       |       | aging |
|       |       |       |       |       |       |       |       | H     |
|       |       |       |       |       |       |       |       | eader |
|       |       |       |       |       |       |       |       |  <#se |
|       |       |       |       |       |       |       |       | ct_8. |
|       |       |       |       |       |       |       |       | 2>`__ |
|       |       |       |       |       |       |       |       | 1.2   |
|       |       |       |       |       |       |       |       | .840. |
|       |       |       |       |       |       |       |       | 10008 |
|       |       |       |       |       |       |       |       | .9.21 |
+-------+-------+-------+-------+-------+-------+-------+-------+-------+
|       | >     |       | 0..1  | MAY   |       |       |       | `P    |
|       |       |       |       |       |       |       |       | arent |
|       |       |       |       |       |       |       |       | Doc   |
|       |       |       |       |       |       |       |       | ument |
|       |       |       |       |       |       |       |       |  <#se |
|       |       |       |       |       |       |       |       | ct_8. |
|       |       |       |       |       |       |       |       | 3>`__ |
|       |       |       |       |       |       |       |       | 1.2   |
|       |       |       |       |       |       |       |       | .840. |
|       |       |       |       |       |       |       |       | 10008 |
|       |       |       |       |       |       |       |       | .9.22 |
+-------+-------+-------+-------+-------+-------+-------+-------+-------+
|       | >     | comp  | 1..1  | SHALL |       |       |       |       |
|       |       | onent |       |       |       |       |       |       |
+-------+-------+-------+-------+-------+-------+-------+-------+-------+
|       | >>    | struc | 1..1  | SHALL |       |       |       |       |
|       |       | tured |       |       |       |       |       |       |
|       |       | ​Body |       |       |       |       |       |       |
+-------+-------+-------+-------+-------+-------+-------+-------+-------+
|       | >>>   | comp  | 0..1  | MAY   |       |       |       |       |
|       |       | onent |       |       |       |       |       |       |
+-------+-------+-------+-------+-------+-------+-------+-------+-------+
| *C    | >>>>  | *sec  |       |       |       |       |       | `Cli  |
| linic |       | tion* |       |       |       |       |       | nical |
| al​In |       |       |       |       |       |       |       | I     |
| forma |       |       |       |       |       |       |       | nform |
| tion* |       |       |       |       |       |       |       | ation |
|       |       |       |       |       |       |       |       |  <#se |
|       |       |       |       |       |       |       |       | ct_9. |
|       |       |       |       |       |       |       |       | 2>`__ |
|       |       |       |       |       |       |       |       | 1.    |
|       |       |       |       |       |       |       |       | 2.840 |
|       |       |       |       |       |       |       |       | .1000 |
|       |       |       |       |       |       |       |       | 8.9.2 |
+-------+-------+-------+-------+-------+-------+-------+-------+-------+
|       | >>>   | comp  | 1..1  | SHALL |       |       |       |       |
|       |       | onent |       |       |       |       |       |       |
+-------+-------+-------+-------+-------+-------+-------+-------+-------+
| *Pr   | >>>>  | *sec  |       |       |       |       |       | `Im   |
| ocedu |       | tion* |       |       |       |       |       | aging |
| re​De |       |       |       |       |       |       |       | Proc  |
| scrip |       |       |       |       |       |       |       | edure |
| tion* |       |       |       |       |       |       |       | D     |
|       |       |       |       |       |       |       |       | escri |
|       |       |       |       |       |       |       |       | ption |
|       |       |       |       |       |       |       |       |  <#se |
|       |       |       |       |       |       |       |       | ct_9. |
|       |       |       |       |       |       |       |       | 3>`__ |
|       |       |       |       |       |       |       |       | 1.    |
|       |       |       |       |       |       |       |       | 2.840 |
|       |       |       |       |       |       |       |       | .1000 |
|       |       |       |       |       |       |       |       | 8.9.3 |
+-------+-------+-------+-------+-------+-------+-------+-------+-------+
|       | >>>   | comp  | 0..1  | MAY   |       |       |       |       |
|       |       | onent |       |       |       |       |       |       |
+-------+-------+-------+-------+-------+-------+-------+-------+-------+
| *Co   | >>>>  | *sec  |       |       |       |       |       | `     |
| mpari |       | tion* |       |       |       |       |       | Compa |
| son​S |       |       |       |       |       |       |       | rison |
| tudy* |       |       |       |       |       |       |       | Study |
|       |       |       |       |       |       |       |       |  <#se |
|       |       |       |       |       |       |       |       | ct_9. |
|       |       |       |       |       |       |       |       | 4>`__ |
|       |       |       |       |       |       |       |       | 1.    |
|       |       |       |       |       |       |       |       | 2.840 |
|       |       |       |       |       |       |       |       | .1000 |
|       |       |       |       |       |       |       |       | 8.9.4 |
+-------+-------+-------+-------+-------+-------+-------+-------+-------+
|       | >>>   | comp  | 0..1  | MAY   |       |       |       |       |
|       |       | onent |       |       |       |       |       |       |
+-------+-------+-------+-------+-------+-------+-------+-------+-------+
| *Find | >>>>  | *sec  |       |       |       |       |       | `Fin  |
| ings* |       | tion* |       |       |       |       |       | dings |
|       |       |       |       |       |       |       |       |  <#se |
|       |       |       |       |       |       |       |       | ct_9. |
|       |       |       |       |       |       |       |       | 5>`__ |
|       |       |       |       |       |       |       |       | 2.16. |
|       |       |       |       |       |       |       |       | 840.1 |
|       |       |       |       |       |       |       |       | .1138 |
|       |       |       |       |       |       |       |       | 83.​1 |
|       |       |       |       |       |       |       |       | 0.20. |
|       |       |       |       |       |       |       |       | 6.1.2 |
+-------+-------+-------+-------+-------+-------+-------+-------+-------+
|       | >>>   | comp  | 1..1  | SHALL |       |       |       |       |
|       |       | onent |       |       |       |       |       |       |
+-------+-------+-------+-------+-------+-------+-------+-------+-------+
| *I    | >>>>  | *sec  |       |       |       |       |       | `     |
| mpres |       | tion* |       |       |       |       |       | Impre |
| sion* |       |       |       |       |       |       |       | ssion |
|       |       |       |       |       |       |       |       |  <#se |
|       |       |       |       |       |       |       |       | ct_9. |
|       |       |       |       |       |       |       |       | 6>`__ |
|       |       |       |       |       |       |       |       | 1.    |
|       |       |       |       |       |       |       |       | 2.840 |
|       |       |       |       |       |       |       |       | .1000 |
|       |       |       |       |       |       |       |       | 8.9.5 |
+-------+-------+-------+-------+-------+-------+-------+-------+-------+
|       | >>>   | comp  | 0..\* | COND  |       |       |       |       |
|       |       | onent |       |       |       |       |       |       |
+-------+-------+-------+-------+-------+-------+-------+-------+-------+
| *Ad   | >>>>  | *sec  |       |       |       |       |       | `Add  |
| dendu |       | tion* |       |       |       |       |       | endum |
| m[*]* |       |       |       |       |       |       |       |  <#se |
|       |       |       |       |       |       |       |       | ct_9. |
|       |       |       |       |       |       |       |       | 7>`__ |
|       |       |       |       |       |       |       |       | 1.    |
|       |       |       |       |       |       |       |       | 2.840 |
|       |       |       |       |       |       |       |       | .1000 |
|       |       |       |       |       |       |       |       | 8.9.6 |
+-------+-------+-------+-------+-------+-------+-------+-------+-------+

.. _sect_7.1.1:

clinicalDocument/code
~~~~~~~~~~~~~~~~~~~~~

Most of the codes in Value Set LOINC Imaging Document Codes are
pre-coordinated with the imaging modality, body part examined, and/or
specific imaging method. When pre-coordinated codes are used, any coded
values elsewhere in the document describing the modality, body part,
etc., must be consistent with the document type code. Local codes used
for report types may be included as a translation element in the code.

.. note::

   Use of Value Set LOINC Imaging Document Codes is harmonized with HL7
   Consolidated CDA Templates for Clinical Notes, Release 2. DICOM ,
   used in , is a subset of the LOINC Imaging Document Codes.

::

   <code code="18748-4"
           displayName="Diagnostic Imaging Report"
           codeSystem="2.16.840.1.113883.6.1"
           codeSystemName="LOINC" >
       <translation code="XRPEDS"
           displayName="Pediatric Radiography Report"
           codeSystem="2.16.840.1.123456.78.9" />
   </code>

.. _sect_7.1.2:

Addendum
~~~~~~~~

COND: If the header includes a relatedDocument element with typeCode
RPLC, and the replaced document had a legalAuthenticator element (i.e.,
was signed), the component/structuredBody SHALL contain at least one
`Addendum <#sect_9.7>`__.

.. _sect_7.2:

Imaging Addendum Report
-----------------------

+----------------------+----------------------------------------------+
| **Template ID**      | 1.2.840.10008.​9.24                          |
+----------------------+----------------------------------------------+
| **Name**             | Imaging Addendum Report                      |
+----------------------+----------------------------------------------+
| **Effective Date**   | 2015/03/24                                   |
+----------------------+----------------------------------------------+
| **Version Label**    | DICOM-20150324                               |
+----------------------+----------------------------------------------+
| **Status**           | Active                                       |
+----------------------+----------------------------------------------+
| **Description**      | Document structure for an Imaging Addendum   |
|                      | Report, i.e., an appendage to an existing    |
|                      | report document that contains supplemental   |
|                      | information. The parent document content     |
|                      | remains unaltered. The Addendum Report must  |
|                      | be read together with its parent document    |
|                      | for full context. Some institutions may have |
|                      | policies that forbid the use of Addendum     |
|                      | Reports, and require revised reports with a  |
|                      | complete restatement of the original         |
|                      | documentation.                               |
+----------------------+----------------------------------------------+
| **Classification**   | CDA Document Level                           |
+----------------------+----------------------------------------------+
| **Relationships**    |                                              |
+----------------------+----------------------------------------------+
| **Context**          | parent node                                  |
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
| **Ima |       | Cl    |       |       |       |       |       |       |
| ging​ |       | inica |       |       |       |       |       |       |
| Adden |       | l​Doc |       |       |       |       |       |       |
| dum** |       | ument |       |       |       |       |       |       |
+-------+-------+-------+-------+-------+-------+-------+-------+-------+
|       | >     | t     | 1..1  | SHALL | II    |       |       |       |
|       |       | empla |       |       |       |       |       |       |
|       |       | te​Id |       |       |       |       |       |       |
+-------+-------+-------+-------+-------+-------+-------+-------+-------+
|       | >@    | @root | 1..1  | SHALL | UID   | SHALL | 1.    |       |
|       |       |       |       |       |       |       | 2.840 |       |
|       |       |       |       |       |       |       | .1000 |       |
|       |       |       |       |       |       |       | 8.9.1 |       |
+-------+-------+-------+-------+-------+-------+-------+-------+-------+
| Doc   | >     | code  | 1..1  | SHALL | CD    | SHALL | `Val  |       |
| ​Type |       |       |       |       |       | CWE   | ueSet |       |
|       |       |       |       |       |       | n     | LOINC |       |
|       |       |       |       |       |       | oNull | Im    |       |
|       |       |       |       |       |       |       | aging |       |
|       |       |       |       |       |       |       | Doc   |       |
|       |       |       |       |       |       |       | ument |       |
|       |       |       |       |       |       |       | Codes |       |
|       |       |       |       |       |       |       | 1.3   |       |
|       |       |       |       |       |       |       | .6.1. |       |
|       |       |       |       |       |       |       | 4.1.1 |       |
|       |       |       |       |       |       |       | 2009. |       |
|       |       |       |       |       |       |       | 10.2. |       |
|       |       |       |       |       |       |       | 5 <ht |       |
|       |       |       |       |       |       |       | tps:/ |       |
|       |       |       |       |       |       |       | /loin |       |
|       |       |       |       |       |       |       | c.org |       |
|       |       |       |       |       |       |       | /oids |       |
|       |       |       |       |       |       |       | /1.3. |       |
|       |       |       |       |       |       |       | 6.1.4 |       |
|       |       |       |       |       |       |       | .1.12 |       |
|       |       |       |       |       |       |       | 009.1 |       |
|       |       |       |       |       |       |       | 0.2.5 |       |
|       |       |       |       |       |       |       | />`__ |       |
+-------+-------+-------+-------+-------+-------+-------+-------+-------+
|       | >     |       | 1..1  | SHALL |       |       |       | `Ge   |
|       |       |       |       |       |       |       |       | neral |
|       |       |       |       |       |       |       |       | H     |
|       |       |       |       |       |       |       |       | eader |
|       |       |       |       |       |       |       |       |  <#se |
|       |       |       |       |       |       |       |       | ct_8. |
|       |       |       |       |       |       |       |       | 1>`__ |
|       |       |       |       |       |       |       |       | 1.2   |
|       |       |       |       |       |       |       |       | .840. |
|       |       |       |       |       |       |       |       | 10008 |
|       |       |       |       |       |       |       |       | .9.20 |
+-------+-------+-------+-------+-------+-------+-------+-------+-------+
|       | >     |       | 1..1  | SHALL |       |       |       | `Im   |
|       |       |       |       |       |       |       |       | aging |
|       |       |       |       |       |       |       |       | H     |
|       |       |       |       |       |       |       |       | eader |
|       |       |       |       |       |       |       |       |  <#se |
|       |       |       |       |       |       |       |       | ct_8. |
|       |       |       |       |       |       |       |       | 2>`__ |
|       |       |       |       |       |       |       |       | 1.2   |
|       |       |       |       |       |       |       |       | .840. |
|       |       |       |       |       |       |       |       | 10008 |
|       |       |       |       |       |       |       |       | .9.21 |
+-------+-------+-------+-------+-------+-------+-------+-------+-------+
|       | >     | r     | 1..1  | SHALL |       |       |       |       |
|       |       | elate |       |       |       |       |       |       |
|       |       | d​Doc |       |       |       |       |       |       |
|       |       | ument |       |       |       |       |       |       |
+-------+-------+-------+-------+-------+-------+-------+-------+-------+
|       | >@    | @typ  | 1.1   | SHALL | CS    | SHALL | APND  |       |
|       |       | ecode |       |       |       |       |       |       |
+-------+-------+-------+-------+-------+-------+-------+-------+-------+
|       | >>    | paren | 1..1  | SHALL |       |       |       |       |
|       |       | t​Doc |       |       |       |       |       |       |
|       |       | ument |       |       |       |       |       |       |
+-------+-------+-------+-------+-------+-------+-------+-------+-------+
| Amen  | >>>   | id    | 1..1  | SHALL | II    |       |       |       |
| ded​D |       |       |       |       |       |       |       |       |
| ocume |       |       |       |       |       |       |       |       |
| nt​ID |       |       |       |       |       |       |       |       |
+-------+-------+-------+-------+-------+-------+-------+-------+-------+
|       | >     | comp  | 1..1  | SHALL |       |       |       |       |
|       |       | onent |       |       |       |       |       |       |
+-------+-------+-------+-------+-------+-------+-------+-------+-------+
|       | >>    | struc | 1..1  | SHALL |       |       |       |       |
|       |       | tured |       |       |       |       |       |       |
|       |       | ​Body |       |       |       |       |       |       |
+-------+-------+-------+-------+-------+-------+-------+-------+-------+
|       | >>>   | comp  | 1..\* | SHALL |       |       |       |       |
|       |       | onent |       |       |       |       |       |       |
+-------+-------+-------+-------+-------+-------+-------+-------+-------+
| *Ad   | >>>>  | *sec  |       |       |       |       |       | `Add  |
| dendu |       | tion* |       |       |       |       |       | endum |
| m[*]* |       |       |       |       |       |       |       |  <#se |
|       |       |       |       |       |       |       |       | ct_9. |
|       |       |       |       |       |       |       |       | 7>`__ |
|       |       |       |       |       |       |       |       | 1.    |
|       |       |       |       |       |       |       |       | 2.840 |
|       |       |       |       |       |       |       |       | .1000 |
|       |       |       |       |       |       |       |       | 8.9.6 |
+-------+-------+-------+-------+-------+-------+-------+-------+-------+

