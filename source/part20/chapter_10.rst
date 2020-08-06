.. _chapter_10:

Entry-level Templates
=====================

.. _sect_10.1:

Coded Observation
-----------------

+----------------------+----------------------------------------------+
| **Template ID**      | 2.16.840.1.113883.​10.20.6.2.13              |
+----------------------+----------------------------------------------+
| **Name**             | Coded Observation                            |
+----------------------+----------------------------------------------+
| **Effective Date**   | 2015/03/24                                   |
+----------------------+----------------------------------------------+
| **Version Label**    | DICOM-20150324                               |
+----------------------+----------------------------------------------+
| **Status**           | Active                                       |
+----------------------+----------------------------------------------+
| **Description**      | Qualitative or categorical observation using |
|                      | a value of type CD.                          |
+----------------------+----------------------------------------------+
| **Classification**   | CDA Entry Level                              |
+----------------------+----------------------------------------------+
| **Relationships**    | Included in all sections                     |
+----------------------+----------------------------------------------+
| **Context**          | parent node                                  |
+----------------------+----------------------------------------------+
| **Open/Closed**      | open                                         |
+----------------------+----------------------------------------------+
| **Revision History** | From Consolidated CDA r1.1                   |
|                      |                                              |
|                      | DICOM-20150324: Added optional negationInd,  |
|                      | interpretationCode, targetSiteCode, and      |
|                      | methodCode with Business Names; added        |
|                      | optional subject Coded Observation           |
+----------------------+----------------------------------------------+

+-------+-------+-------+-------+-------+-------+-------+-------+-------+
| Bus   | Nest  | Ele   | Card  | Elem  | Data  | Value | Value | Subsi |
| iness | Level | ment/ |       | /Attr | Type  | Conf  |       | diary |
| Name  |       | ​Attr |       | Conf  |       |       |       | Tem   |
|       |       | ibute |       |       |       |       |       | plate |
+=======+=======+=======+=======+=======+=======+=======+=======+=======+
| **Co  |       | o     |       |       |       |       |       |       |
| ded​O |       | bserv |       |       |       |       |       |       |
| bserv |       | ation |       |       |       |       |       |       |
| ation |       |       |       |       |       |       |       |       |
| [*]** |       |       |       |       |       |       |       |       |
+-------+-------+-------+-------+-------+-------+-------+-------+-------+
|       | @     | @clas | 1..1  | SHALL | CS    | SHALL | OBS   |       |
|       |       | sCode |       |       |       |       |       |       |
+-------+-------+-------+-------+-------+-------+-------+-------+-------+
|       | @     | @moo  | 1..1  | SHALL |       | SHALL | EVN   |       |
|       |       | dCode |       |       |       |       |       |       |
+-------+-------+-------+-------+-------+-------+-------+-------+-------+
| Not   | @     | @n    | 0..1  | MAY   | BL    | SHALL | true  |       |
|       |       | egati |       |       |       |       |       |       |
|       |       | onInd |       |       |       |       |       |       |
+-------+-------+-------+-------+-------+-------+-------+-------+-------+
|       | >     | t     | 1..1  | SHALL | II    |       |       |       |
|       |       | empla |       |       |       |       |       |       |
|       |       | te​Id |       |       |       |       |       |       |
+-------+-------+-------+-------+-------+-------+-------+-------+-------+
|       | >@    | @root | 1..1  | SHALL | UID   | SHALL | 2     |       |
|       |       |       |       |       |       |       | .16.8 |       |
|       |       |       |       |       |       |       | 40.1. |       |
|       |       |       |       |       |       |       | 11388 |       |
|       |       |       |       |       |       |       | 3.​10 |       |
|       |       |       |       |       |       |       | .20.6 |       |
|       |       |       |       |       |       |       | .2.13 |       |
+-------+-------+-------+-------+-------+-------+-------+-------+-------+
|       | >     | id    | 1..1  | SHALL | II    |       |       |       |
+-------+-------+-------+-------+-------+-------+-------+-------+-------+
| Obs   | >     | code  | 1..1  | SHALL | CD    |       | Conc  |       |
| ​Name |       |       |       |       |       |       | ept​D |       |
|       |       |       |       |       |       |       | omain |       |
|       |       |       |       |       |       |       | Obser |       |
|       |       |       |       |       |       |       | vatio |       |
|       |       |       |       |       |       |       | nType |       |
+-------+-------+-------+-------+-------+-------+-------+-------+-------+
|       | >     | text  | 0..1  | S     | ED    |       |       |       |
|       |       |       |       | HOULD |       |       |       |       |
+-------+-------+-------+-------+-------+-------+-------+-------+-------+
| Ref   | >>    | refe  | 1..1  | SHALL | URL   |       | #     |       |
|       |       | rence |       |       | (XML  |       | *co   |       |
|       |       |       |       |       | I     |       | ntent |       |
|       |       |       |       |       | DREF) |       | ​Ref* |       |
+-------+-------+-------+-------+-------+-------+-------+-------+-------+
|       | >     | s     | 1..1  | SHALL | CS    | SHALL | COMP  |       |
|       |       | tatus |       |       |       |       | LETED |       |
|       |       | ​Code |       |       |       |       |       |       |
+-------+-------+-------+-------+-------+-------+-------+-------+-------+
| Time  | >     | effe  | 0..1  | S     | TS    |       |       |       |
|       |       | ctive |       | HOULD |       |       |       |       |
|       |       | ​Time |       |       |       |       |       |       |
+-------+-------+-------+-------+-------+-------+-------+-------+-------+
| Obs​  | >     | value | 1..1  | SHALL | CD    |       | Conc  |       |
| Value |       |       |       |       |       |       | ept​D |       |
|       |       |       |       |       |       |       | omain |       |
|       |       |       |       |       |       |       | O     |       |
|       |       |       |       |       |       |       | bserv |       |
|       |       |       |       |       |       |       | ation |       |
|       |       |       |       |       |       |       | Value |       |
+-------+-------+-------+-------+-------+-------+-------+-------+-------+
|       | >@    | @xsi  | 1..1  | SHALL | ST    | SHALL | CD    |       |
|       |       | :type |       |       |       |       |       |       |
+-------+-------+-------+-------+-------+-------+-------+-------+-------+
| Inte  | >     | inte  | 0..1  | MAY   | CE    | SHALL | Val   |       |
| rpret |       | rpret |       |       |       | CNE   | ueSet |       |
| ation |       | ation |       |       |       |       | 2.1   |       |
| ​Code |       | ​Code |       |       |       |       | 6.840 |       |
|       |       |       |       |       |       |       | .1.11 |       |
|       |       |       |       |       |       |       | 3883. |       |
|       |       |       |       |       |       |       | 11.78 |       |
+-------+-------+-------+-------+-------+-------+-------+-------+-------+
| Acti  | >>    | t     | 0..1  | MAY   | CD    | MAY   | Val   |       |
| onabl |       | ransl |       |       |       | CWE   | ueSet |       |
| e​Pri |       | ation |       |       |       |       |       |       |
| ority |       |       |       |       |       |       | [See  |       |
|       |       |       |       |       |       |       | `int  |       |
|       |       |       |       |       |       |       | erpre |       |
|       |       |       |       |       |       |       | tatio |       |
|       |       |       |       |       |       |       | nCode |       |
|       |       |       |       |       |       |       | and   |       |
|       |       |       |       |       |       |       | t     |       |
|       |       |       |       |       |       |       | ransl |       |
|       |       |       |       |       |       |       | ation |       |
|       |       |       |       |       |       |       | For   |       |
|       |       |       |       |       |       |       | Actio |       |
|       |       |       |       |       |       |       | nable |       |
|       |       |       |       |       |       |       | Fi    |       |
|       |       |       |       |       |       |       | nding |       |
|       |       |       |       |       |       |       | s <#s |       |
|       |       |       |       |       |       |       | ect_1 |       |
|       |       |       |       |       |       |       | 0.1.3 |       |
|       |       |       |       |       |       |       | >`__] |       |
+-------+-------+-------+-------+-------+-------+-------+-------+-------+
| T     | >     | t     | 1..1  | COND  | CD    |       | Conc  |       |
| arget |       | arget |       |       |       |       | ept​D |       |
| ​Site |       | ​Site |       |       |       |       | omain |       |
|       |       | ​Code |       |       |       |       | Obser |       |
|       |       |       |       |       |       |       | vatio |       |
|       |       |       |       |       |       |       | nSite |       |
+-------+-------+-------+-------+-------+-------+-------+-------+-------+
|       | >>    | qual  | 0..1  | COND  |       |       |       |       |
|       |       | ifier |       |       |       |       |       |       |
+-------+-------+-------+-------+-------+-------+-------+-------+-------+
|       | >>>   | name  | 1..1  | SHALL | CD    | SHALL | (     |       |
|       |       |       |       |       |       |       | 27274 |       |
|       |       |       |       |       |       |       | 1003, |       |
|       |       |       |       |       |       |       | S     |       |
|       |       |       |       |       |       |       | NOMED |       |
|       |       |       |       |       |       |       | CT,   |       |
|       |       |       |       |       |       |       | "la   |       |
|       |       |       |       |       |       |       | teral |       |
|       |       |       |       |       |       |       | ity") |       |
+-------+-------+-------+-------+-------+-------+-------+-------+-------+
| Later | >>>   | value | 1..1  | SHALL | CD    | SHALL | Val   |       |
| ality |       |       |       |       |       | CNE   | ueSet |       |
+-------+-------+-------+-------+-------+-------+-------+-------+-------+
|       | >>    | qual  | 0..1  | COND  |       |       |       |       |
|       |       | ifier |       |       |       |       |       |       |
+-------+-------+-------+-------+-------+-------+-------+-------+-------+
|       | >>>   | name  | 1..1  | SHALL | CD    | SHALL | (     |       |
|       |       |       |       |       |       |       | 10623 |       |
|       |       |       |       |       |       |       | 3006, |       |
|       |       |       |       |       |       |       | S     |       |
|       |       |       |       |       |       |       | NOMED |       |
|       |       |       |       |       |       |       | CT,   |       |
|       |       |       |       |       |       |       | "top  |       |
|       |       |       |       |       |       |       | ograp |       |
|       |       |       |       |       |       |       | hical |       |
|       |       |       |       |       |       |       | modif |       |
|       |       |       |       |       |       |       | ier") |       |
+-------+-------+-------+-------+-------+-------+-------+-------+-------+
| Top   | >>>   | value | 1..1  | SHALL | CD    | SHALL | Val   |       |
| o​Mod |       |       |       |       |       | CNE   | ueSet |       |
| ifier |       |       |       |       |       |       |       |       |
+-------+-------+-------+-------+-------+-------+-------+-------+-------+
| M     | >     | m     | 0..1  | MAY   | CD    |       | Conc  |       |
| ethod |       | ethod |       |       |       |       | ept​D |       |
|       |       | ​Code |       |       |       |       | omain |       |
|       |       |       |       |       |       |       | Ob    |       |
|       |       |       |       |       |       |       | serva |       |
|       |       |       |       |       |       |       | tionM |       |
|       |       |       |       |       |       |       | ethod |       |
+-------+-------+-------+-------+-------+-------+-------+-------+-------+
|       | >     | ent   | 0..\* | MAY   |       |       |       |       |
|       |       | ry​Re |       |       |       |       |       |       |
|       |       | latio |       |       |       |       |       |       |
|       |       | nship |       |       |       |       |       |       |
+-------+-------+-------+-------+-------+-------+-------+-------+-------+
|       | >@    | @typ  | 1..1  | SHALL | CS    | SHALL | SPRT  |       |
|       |       | eCode |       |       |       |       |       |       |
+-------+-------+-------+-------+-------+-------+-------+-------+-------+
| *     | >>    | *ob   | 1..1  | SHALL |       |       |       | `SOP  |
| SOPIn |       | serva |       |       |       |       |       | Ins   |
| stanc |       | tion* |       |       |       |       |       | tance |
| e[*]* |       |       |       |       |       |       |       | Ob    |
|       |       |       |       |       |       |       |       | serva |
|       |       |       |       |       |       |       |       | tion  |
|       |       |       |       |       |       |       |       | <#sec |
|       |       |       |       |       |       |       |       | t_10. |
|       |       |       |       |       |       |       |       | 8>`__ |
|       |       |       |       |       |       |       |       | 1.2   |
|       |       |       |       |       |       |       |       | .840. |
|       |       |       |       |       |       |       |       | 10008 |
|       |       |       |       |       |       |       |       | .9.18 |
+-------+-------+-------+-------+-------+-------+-------+-------+-------+
|       | >     | ent   | 0..\* | MAY   |       |       |       |       |
|       |       | ry​Re |       |       |       |       |       |       |
|       |       | latio |       |       |       |       |       |       |
|       |       | nship |       |       |       |       |       |       |
+-------+-------+-------+-------+-------+-------+-------+-------+-------+
|       | >@    | @typ  | 1..1  | SHALL | CS    | SHALL | SPRT  |       |
|       |       | eCode |       |       |       |       |       |       |
+-------+-------+-------+-------+-------+-------+-------+-------+-------+
| *Quan | >     | *ob   | 1..1  | SHALL |       |       |       | `Qua  |
| tity​ |       | serva |       |       |       |       |       | ntity |
| Measu |       | tion* |       |       |       |       |       | Me    |
| remen |       |       |       |       |       |       |       | asure |
| t[*]* |       |       |       |       |       |       |       | ment  |
|       |       |       |       |       |       |       |       | <#sec |
|       |       |       |       |       |       |       |       | t_10. |
|       |       |       |       |       |       |       |       | 5>`__ |
|       |       |       |       |       |       |       |       | 2     |
|       |       |       |       |       |       |       |       | .16.8 |
|       |       |       |       |       |       |       |       | 40.1. |
|       |       |       |       |       |       |       |       | 11388 |
|       |       |       |       |       |       |       |       | 3.​10 |
|       |       |       |       |       |       |       |       | .20.6 |
|       |       |       |       |       |       |       |       | .2.14 |
+-------+-------+-------+-------+-------+-------+-------+-------+-------+
|       | >     | ent   | 0..\* | MAY   |       |       |       |       |
|       |       | ry​Re |       |       |       |       |       |       |
|       |       | latio |       |       |       |       |       |       |
|       |       | nship |       |       |       |       |       |       |
+-------+-------+-------+-------+-------+-------+-------+-------+-------+
|       | >@    | @typ  | 1..1  | SHALL | CS    | SHALL | SUBJ  |       |
|       |       | eCode |       |       |       |       |       |       |
+-------+-------+-------+-------+-------+-------+-------+-------+-------+
| *C    | >     | *ob   | 1..1  | SHALL |       |       |       | `     |
| oded​ |       | serva |       |       |       |       |       | Coded |
| Obser |       | tion* |       |       |       |       |       | Ob    |
| vatio |       |       |       |       |       |       |       | serva |
| n[*]* |       |       |       |       |       |       |       | tion  |
|       |       |       |       |       |       |       |       | <#sec |
|       |       |       |       |       |       |       |       | t_10. |
|       |       |       |       |       |       |       |       | 1>`__ |
|       |       |       |       |       |       |       |       | 2     |
|       |       |       |       |       |       |       |       | .16.8 |
|       |       |       |       |       |       |       |       | 40.1. |
|       |       |       |       |       |       |       |       | 11388 |
|       |       |       |       |       |       |       |       | 3.​10 |
|       |       |       |       |       |       |       |       | .20.6 |
|       |       |       |       |       |       |       |       | .2.13 |
+-------+-------+-------+-------+-------+-------+-------+-------+-------+

.. _sect_10.1.1:

code and @negationInd
~~~~~~~~~~~~~~~~~~~~~

The Observation code element has an associated Concept Domain
ObservationType. A representative binding for this Concept Domain is to
the value (ASSERTION, actcode[2.16.840.1.113883.5.4], "Assertion"),
providing an assertion of a finding concept in the value element.

The Observation may have @negationInd attribute "true", which together
with the code "ASSERTION" indicates that the finding was not observed,
e.g., to represent "No finding of stroke".

.. note::

   This is the pattern used in Consolidated CDA for negative findings.

.. _sect_10.1.2:

text/reference and Related Narrative Block Markup
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

The Observation entry SHOULD include a text/reference element, whose
value attribute (not to be confused with the value element of the
Observation class) SHALL begin with a '#' and SHALL point to its
corresponding narrative in the parent section (using the approach
defined in CDA Release 2, section 4.3.5.1). See `<content> Markup and
Links From Entries <#sect_9.1.1.1>`__.

.. _sect_10.1.3:

interpretationCode and translation For Actionable Findings
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

When an observation is unexpected or "actionable" (one type of which is
denoted a "critical finding"), it may be flagged using the
interpretationCode. For very abnormal findings the interpretationCode
element SHALL be set to (AA, ObservationInterpretation, "abnormal
alert"). Unexpected normal findings, e.g., no findings of disease when
patient treatment had been planned on the presumption of disease, may
also be flagged using interpretationCode (N, ObservationInterpretation,
"normal").

The translation element of the interpretationCode may be used to provide
a further classification as defined in a regionally- or
professionally-specified value set. This template identifies an optional
value set for the ACR Actionable Finding categories 1, 2, and 3, as
defined by: Larson PA, et al. J Am Coll Radiol 2014; published online.
DOI 10.1016/j.jacr.2013.12.016.

The narrative text associated with the actionable finding SHOULD be
highlighted using styleCode Bold. See `text <#sect_9.5.1>`__ and
`<content> Markup and Links From Entries <#sect_9.1.1.1>`__.

Actionable findings that require a specific follow-up action or
procedure SHOULD be referenced from a recommendation in the
`Recommendation <#sect_9.8.11>`__ section.

Communication of actionable findings SHOULD be documented in the
`Communication of Actionable Findings <#sect_9.8.10>`__ section.

.. _sect_10.1.4:

targetSiteCode
~~~~~~~~~~~~~~

Each observation needs to fully specify its site/location.

COND: If the observation site is not pre-coordinated in the
observation/code or observation/value, it SHALL be specified in the
observation/targetSiteCode.

COND: The qualifier element for laterality SHALL be present if the
targetSiteCode represents a paired body part and laterality is not
pre-coordinated in the targetSiteCode.

Note that inclusion in a labeled subsection (see `Labeled
Subsection <#sect_9.8.9>`__) does not imply a finding site for the
observation from the title. The title is not semantically part of the
post-coordination.

.. _sect_10.1.5:

entryRelationship/@typeCode=SUBJ/observation - Coded
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

The Coded Observation entry MAY include an actRelationship of type SUBJ
(has subject) to a subsidiary Coded Observation (recursively invoking
this same template). This allows the constructions of complex clinical
statements.

::

   <text>
       ...
       <content ID="fnd-1"> ...finding of a right hilar mass (abnormal - class 1) ...</content>
   </text>
   ...
   <entry>
       <observation classCode="OBS" moodCode="EVN">
           <templateId root="2.16.840.1.113883.10.20.6.2.13"/>
           <id root="1.2.840.10213.2.62.7044779.114265201"/>
           <code code="ASSERTION" codeSystem="2.16.840.1.113883.5.4"
               codeSystemName="actCode"
               displayName="Assertion"/>
           <text><reference value="#fnd-1"/></text>
           <statusCode code="completed"/>
           <effectiveTime value="20140914171504+0500"/>
           <value xsi:type="CD" code="309530007"
               codeSystem="2.16.840.1.113883.6.96"
               codeSystemName="SNOMED CT"
               displayName="Hilar mass"/>
           <interpretationCode code = "AA" codeSystem="2.16.840.1.113883.5.83"
                   codeSystemName="ObservationInterpretation"
                   displayName="Abnormal Alert">
               <translation code="RID49480" codeSystem="2.16.840.1.113883.6.256"
                   codeSystemName="RADLEX"
                   displayName="ACR Category 1 Actionable Finding"/>
           </interpretationCode>
           <!-- although "hilar mass" is by definition in the lung, the observation.value
                does not describe right or left lung, so targetSite is required -->
           <targetSiteCode code="3341006"
               codeSystem="2.16.840.1.113883.6.96" codeSystemName="SNOMED CT"
               displayName="right lung">
           </targetSiteCode>
           <!-- entryRelationship elements referring to SOP Instance Observations
                or Quantity Measurement Observations may appear here -->
       </observation>
   </entry>

.. _sect_10.2:

Procedural Medication
---------------------

+----------------------+----------------------------------------------+
| **Template ID**      | 1.2.840.10008.9.13                           |
+----------------------+----------------------------------------------+
| **Name**             | Procedural Medication                        |
+----------------------+----------------------------------------------+
| **Effective Date**   | 2015/03/24                                   |
+----------------------+----------------------------------------------+
| **Version Label**    | DICOM-20150324                               |
+----------------------+----------------------------------------------+
| **Status**           | Active                                       |
+----------------------+----------------------------------------------+
| **Description**      | Procedural medication describes a substance  |
|                      | administration that has actually occurred    |
|                      | prior to or during a procedure (e.g.,        |
|                      | imaging contrast/agents, anti-histamines,    |
|                      | anti-anxiety, beta blockers to control heart |
|                      | rate during procedure, etc.).                |
+----------------------+----------------------------------------------+
| **Classification**   | CDA Entry Level                              |
+----------------------+----------------------------------------------+
| **Relationships**    | Included in `Imaging Procedure               |
|                      | Description <#sect_9.3>`__                   |
+----------------------+----------------------------------------------+
| **Context**          | parent node                                  |
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
| **P   |       | subs  | 1..1 | SHALL |       |       |       |       |
| roced |       | tance |      |       |       |       |       |       |
| ural​ |       | ​Admi |      |       |       |       |       |       |
| Medic |       | nistr |      |       |       |       |       |       |
| ation |       | ation |      |       |       |       |       |       |
| [*]** |       |       |      |       |       |       |       |       |
| or    |       |       |      |       |       |       |       |       |
| **Con |       |       |      |       |       |       |       |       |
| trast |       |       |      |       |       |       |       |       |
| [*]** |       |       |      |       |       |       |       |       |
+-------+-------+-------+------+-------+-------+-------+-------+-------+
|       | @     | @clas | 1..1 | SHALL | CS    | SHALL | SBADM |       |
|       |       | sCode |      |       |       |       |       |       |
+-------+-------+-------+------+-------+-------+-------+-------+-------+
|       | @     | @moo  | 1..1 | SHALL | CS    | SHALL | EVN   |       |
|       |       | dCode |      |       |       |       |       |       |
+-------+-------+-------+------+-------+-------+-------+-------+-------+
|       | >     | t     | 1..1 | SHALL | II    |       |       |       |
|       |       | empla |      |       |       |       |       |       |
|       |       | te​Id |      |       |       |       |       |       |
+-------+-------+-------+------+-------+-------+-------+-------+-------+
|       | >@    | @root | 1..1 | SHALL | UID   | SHALL | 1.2   |       |
|       |       |       |      |       |       |       | .840. |       |
|       |       |       |      |       |       |       | 10008 |       |
|       |       |       |      |       |       |       | .9.13 |       |
+-------+-------+-------+------+-------+-------+-------+-------+-------+
|       | >     | id    | 1..1 | SHALL | II    |       |       |       |
+-------+-------+-------+------+-------+-------+-------+-------+-------+
|       | >     | text  | 0..1 | S     | ED    |       |       |       |
|       |       |       |      | HOULD |       |       |       |       |
+-------+-------+-------+------+-------+-------+-------+-------+-------+
| Ref   | >>    | refe  | 0..1 | S     | URL   |       | *#c   |       |
|       |       | rence |      | HOULD | (XML  |       | onten |       |
|       |       |       |      |       | I     |       | tRef* |       |
|       |       |       |      |       | DREF) |       |       |       |
+-------+-------+-------+------+-------+-------+-------+-------+-------+
|       | >     | s     | 1..1 | SHALL | CS    | SHALL | COMP  |       |
|       |       | tatus |      |       |       |       | LETED |       |
|       |       | ​Code |      |       |       |       |       |       |
+-------+-------+-------+------+-------+-------+-------+-------+-------+
| Route | >     | route | 0..1 | MAY   | CE    | S     | Val   |       |
|       |       | ​Code |      |       |       | HOULD | ueSet |       |
|       |       |       |      |       |       | CWE   |       |       |
+-------+-------+-------+------+-------+-------+-------+-------+-------+
| Dose  | >     | dos   | 0..1 | S     | PQ    |       |       |       |
|       |       | e​Qua |      | HOULD |       |       |       |       |
|       |       | ntity |      |       |       |       |       |       |
+-------+-------+-------+------+-------+-------+-------+-------+-------+
| Dose  | >@    | @unit | 0..1 | S     |       | SHALL | Val   |       |
| ​Unit |       |       |      | HOULD |       | CNE   | ueSet |       |
+-------+-------+-------+------+-------+-------+-------+-------+-------+
| Rate  | >     | rat   | 0..1 | MAY   | PQ    |       |       |       |
|       |       | e​Qua |      |       |       |       |       |       |
|       |       | ntity |      |       |       |       |       |       |
+-------+-------+-------+------+-------+-------+-------+-------+-------+
| Rate  | >@    | @unit | 1..1 | SHALL | CS    | SHALL | Val   |       |
| ​Unit |       |       |      |       |       | CNE   | ueSet |       |
+-------+-------+-------+------+-------+-------+-------+-------+-------+
|       | >     | consu | 1..1 | SHALL |       |       |       |       |
|       |       | mable |      |       |       |       |       |       |
+-------+-------+-------+------+-------+-------+-------+-------+-------+
|       | >>    | manuf | 1..1 | SHALL |       |       |       |       |
|       |       | actur |      |       |       |       |       |       |
|       |       | ed​Pr |      |       |       |       |       |       |
|       |       | oduct |      |       |       |       |       |       |
+-------+-------+-------+------+-------+-------+-------+-------+-------+
|       | >>@   | @clas | 1..1 | SHALL | CS    | SHALL | MANU  |       |
|       |       | sCode |      |       |       |       |       |       |
+-------+-------+-------+------+-------+-------+-------+-------+-------+
|       | >>>   | m     | 1..1 | SHALL |       |       |       |       |
|       |       | anufa |      |       |       |       |       |       |
|       |       | cture |      |       |       |       |       |       |
|       |       | d​Mat |      |       |       |       |       |       |
|       |       | erial |      |       |       |       |       |       |
+-------+-------+-------+------+-------+-------+-------+-------+-------+
| Cod   | >>>>  | code  | 1..1 | SHALL | CE    |       | Conc  |       |
| ed​Pr |       |       |      |       |       |       | ept​D |       |
| oduct |       |       |      |       |       |       | omain |       |
| ​Name |       |       |      |       |       |       |       |       |
|       |       |       |      |       |       |       | Me    |       |
|       |       |       |      |       |       |       | d​Con |       |
|       |       |       |      |       |       |       | trast |       |
|       |       |       |      |       |       |       | ​Name |       |
+-------+-------+-------+------+-------+-------+-------+-------+-------+
| Fr    | >>>>> | ori   | 0..1 | S     | ED    |       |       |       |
| ee​Te |       | ginal |      | HOULD |       |       |       |       |
| xt​Pr |       | Text  |      |       |       |       |       |       |
| oduct |       |       |      |       |       |       |       |       |
| ​Name |       |       |      |       |       |       |       |       |
+-------+-------+-------+------+-------+-------+-------+-------+-------+

.. _sect_10.2.1:

Business Name Alias
~~~~~~~~~~~~~~~~~~~

This template defines a primary scoping business name
"ProceduralMedication" and an alias "Contrast". This allows production
logic to use either term, although the structure is identical.

.. _sect_10.2.2:

text/reference and Related Narrative Block Markup
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

The substanceAdministration entry SHOULD include a text/reference
element, whose value attribute SHALL begin with a '#' and SHALL point to
its corresponding narrative in the parent section (using the approach
defined in CDA Release 2, section 4.3.5.1). See `<content> Markup and
Links From Entries <#sect_9.1.1.1>`__.

.. _sect_10.2.3:

doseQuantity
~~~~~~~~~~~~

-  Pre-coordinated consumable: If the consumable code is a
   pre-coordinated unit dose (e.g., "metoprolol 25mg tablet") then
   doseQuantity is a unitless number that indicates the number of
   products given per administration (e.g., "2", meaning 2 x "metoprolol
   25mg tablet").

-  Not pre-coordinated consumable: If the consumable code is not
   pre-coordinated (e.g., is simply "metoprolol"), then doseQuantity
   must represent a physical quantity with @unit, e.g., "25" and "mg",
   specifying the amount of product given per administration.

::

   <substanceAdministration classCode="SBADM" moodCode="EVN">
       <templateId root="1.2.840.10008.9.13"/>
       <id root="cdbd33f0-6cde-11db-9fe1-0800200c9a66"/>
       <text>
           <reference value="#med1"/>
       </text>
       <statusCode code="completed"/>
       <routeCode code="47625008" codeSystem="2.16.840.1.113883.6.96"
           codeSystemName="SNOMED CT" displayName="intravenous route"/>
       <doseQuantity value="100" unit="ml"/>
       <consumable>
           <manufacturedProduct classCode="MANU">
               <templateId root="2.16.840.1.113883.10.20.22.4.23"/>
               <id/>
               <manufacturedMaterial>
                   <code code="412372002"
                           codeSystem="2.16.840.1.113883.6.96"
                           codeSystemName="SNOMED CT"
                           displayName="Meglumine Diatrizoate">
                       <originalText>
                           <reference value="#manmat1"/>
                       </originalText>
                       <translation code="3320"
                           codeSystem="2.16.840.1.113883.6.88" codeSystemName="RxNorm"
                           displayName="Diatrizoate Meglumine"/>
                   </code>
               </manufacturedMaterial>
           </manufacturedProduct>
       </consumable>
   </substanceAdministration>

.. _sect_10.3:

observationMedia
----------------

+----------------------+----------------------------------------------+
| **Template ID**      | 1.3.6.1.4.1.19376.​1.4.1.4.7                 |
+----------------------+----------------------------------------------+
| **Name**             | observation​Media Entry                      |
+----------------------+----------------------------------------------+
| **Effective Date**   | 2011-07                                      |
+----------------------+----------------------------------------------+
| **Version Label**    | IHECIRC-TI                                   |
+----------------------+----------------------------------------------+
| **Status**           | Active                                       |
+----------------------+----------------------------------------------+
| **Description**      | The observationMedia Entry provides an       |
|                      | in-line graphic depiction of the section     |
|                      | findings. It is referenced by a              |
|                      | <renderMultiMedia> element in the section    |
|                      | text. Typical uses are for graphic           |
|                      | representation of findings (e.g., arterial   |
|                      | tree diagrams) or in-line representations of |
|                      | key images.                                  |
+----------------------+----------------------------------------------+
| **Classification**   | CDA Entry Level                              |
+----------------------+----------------------------------------------+
| **Relationships**    |                                              |
+----------------------+----------------------------------------------+
| **Context**          | parent node                                  |
+----------------------+----------------------------------------------+
| **Open/Closed**      | Open                                         |
+----------------------+----------------------------------------------+
| **Revision History** | From IHE Cardiac Imaging Report Content      |
|                      | Profile Supplement for Trial Implementation  |
+----------------------+----------------------------------------------+

+-------+-------+-------+------+-------+-------+-------+-------+-------+
| Bus   | Nest  | Ele   | Card | Elem  | Data  | Value | Value | Subsi |
| iness | Level | ment/ |      | /Attr | Type  | Conf  |       | diary |
| Name  |       | ​Attr |      | Conf  |       |       |       | Tem   |
|       |       | ibute |      |       |       |       |       | plate |
+=======+=======+=======+======+=======+=======+=======+=======+=======+
| **Gr  |       | ob    | 1..1 | SHALL |       |       |       |       |
| aphic |       | serva |      |       |       |       |       |       |
| [*]** |       | tion​ |      |       |       |       |       |       |
|       |       | Media |      |       |       |       |       |       |
+-------+-------+-------+------+-------+-------+-------+-------+-------+
|       | @     | class | 1..1 | SHALL | CS    | OBS   |       |       |
|       |       | ​Code |      |       |       |       |       |       |
+-------+-------+-------+------+-------+-------+-------+-------+-------+
|       | @     | mood  | 1..1 | SHALL | CS    | EVN   |       |       |
|       |       | ​Code |      |       |       |       |       |       |
+-------+-------+-------+------+-------+-------+-------+-------+-------+
| *     | @     | @ID   | 1..1 | SHALL | XML   |       | [See  |       |
| *\*** |       |       |      |       | ID    |       | `XML  |       |
|       |       |       |      |       |       |       | ID <# |       |
|       |       |       |      |       |       |       | sect_ |       |
|       |       |       |      |       |       |       | 5.3.4 |       |
|       |       |       |      |       |       |       | >`__] |       |
+-------+-------+-------+------+-------+-------+-------+-------+-------+
|       | >     | t     | 1..1 | SHALL | II    |       |       |       |
|       |       | empla |      |       |       |       |       |       |
|       |       | te​Id |      |       |       |       |       |       |
+-------+-------+-------+------+-------+-------+-------+-------+-------+
|       | >@    | @root | 1..1 | SHALL | UID   | SHALL | 1.3   |       |
|       |       |       |      |       |       |       | .6.1. |       |
|       |       |       |      |       |       |       | 4.1.1 |       |
|       |       |       |      |       |       |       | 9376. |       |
|       |       |       |      |       |       |       | ​1.4. |       |
|       |       |       |      |       |       |       | 1.4.7 |       |
+-------+-------+-------+------+-------+-------+-------+-------+-------+
|       | >     | id    | 1..1 | SHALL | II    |       |       |       |
+-------+-------+-------+------+-------+-------+-------+-------+-------+
| Image | >     | value | 1..1 | SHALL | ED    |       |       |       |
+-------+-------+-------+------+-------+-------+-------+-------+-------+
|       | >@    | @repr | 1..1 | SHALL | CS    | SHALL | B64   |       |
|       |       | esent |      |       |       |       |       |       |
|       |       | ation |      |       |       |       |       |       |
+-------+-------+-------+------+-------+-------+-------+-------+-------+
| Media | >@    | @medi | 1..1 | SHALL | CS    | SHALL | Val   |       |
| ​Type |       | aType |      |       |       |       | ueSet |       |
|       |       |       |      |       |       | CNE   | 2     |       |
|       |       |       |      |       |       |       | .16.8 |       |
|       |       |       |      |       |       | S     | 40.1. |       |
|       |       |       |      |       |       | TATIC | 11388 |       |
|       |       |       |      |       |       |       | 3.11. |       |
|       |       |       |      |       |       |       | 14839 |       |
+-------+-------+-------+------+-------+-------+-------+-------+-------+
| Imag  | >>    | refe  | 0..1 | MAY   | TEL   |       |       |       |
| e​URI |       | rence |      |       |       |       |       |       |
+-------+-------+-------+------+-------+-------+-------+-------+-------+

.. _sect_10.3.1:

observationMedia/@ID and Related Narrative Block Markup
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

The ObservationMedia entry SHALL include an XML ID attribute (not to be
confused with the id element of the act class) used as a target of
a<renderMultiMedia> element in the section/text narrative block of the
parent section. See `<renderMultiMedia> Markup and Graphical
Content <#sect_9.1.1.3>`__.

.. _sect_10.3.2:

value and Reference
~~~~~~~~~~~~~~~~~~~

The value of type ED SHALL contain an in-line encoding of a graphic
using base64. The <reference> element, if present, SHALL reference a URI
for the same image as included in-line.

::

   <observationMedia classCode="SBADM" moodCode="EVN" ID="obsMedia-1">
       <templateId root="1.3.6.1.4.1.19376.1.4.1.4.7"/>
       <id root="1.2.840.19432234.2342342.23232232"/>
       <value representation="B64" mediaType="image/jpeg">
           Bgd3fsET4g...
       </value>
   </observationMedia>

.. _sect_10.4:

Procedure Technique
-------------------

+----------------------+----------------------------------------------+
| **Template ID**      | 1.2.840.10008.9.14                           |
+----------------------+----------------------------------------------+
| **Name**             | Procedure Technique                          |
+----------------------+----------------------------------------------+
| **Effective Date**   | 2015/03/24                                   |
+----------------------+----------------------------------------------+
| **Version Label**    | DICOM-20150324                               |
+----------------------+----------------------------------------------+
| **Status**           | Active                                       |
+----------------------+----------------------------------------------+
| **Description**      | The Procedure Technique entry allows the     |
|                      | encoding of various parameters of the image  |
|                      | acquisition. Other details may be found in   |
|                      | other entries (e.g., procedural medication). |
+----------------------+----------------------------------------------+
| **Classification**   | CDA Entry Level                              |
+----------------------+----------------------------------------------+
| **Relationships**    | Included in `Imaging Procedure               |
|                      | Description <#sect_9.3>`__ and `Comparison   |
|                      | Study <#sect_9.4>`__                         |
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
| **P   |       | proc  | 1..1  | SHALL |       |       |       |       |
| roced |       | edure |       |       |       |       |       |       |
| ure​T |       |       |       |       |       |       |       |       |
| echni |       |       |       |       |       |       |       |       |
| que** |       |       |       |       |       |       |       |       |
+-------+-------+-------+-------+-------+-------+-------+-------+-------+
|       | @     | @clas | 1..1  | SHALL | CS    | SHALL | PROC  |       |
|       |       | sCode |       |       |       |       |       |       |
+-------+-------+-------+-------+-------+-------+-------+-------+-------+
|       | @     | @moo  | 1..1  | SHALL | CS    | SHALL | EVN   |       |
|       |       | dCode |       |       |       |       |       |       |
+-------+-------+-------+-------+-------+-------+-------+-------+-------+
|       | >     | t     | 1..1  | SHALL | II    |       |       |       |
|       |       | empla |       |       |       |       |       |       |
|       |       | te​Id |       |       |       |       |       |       |
+-------+-------+-------+-------+-------+-------+-------+-------+-------+
|       | >@    | @root | 1..1  | SHALL | UID   |       | 1.2   |       |
|       |       |       |       |       |       |       | .840. |       |
|       |       |       |       |       |       |       | 10008 |       |
|       |       |       |       |       |       |       | .9.14 |       |
+-------+-------+-------+-------+-------+-------+-------+-------+-------+
|       | >     | id    | 1..1  | SHALL | II    |       |       |       |
+-------+-------+-------+-------+-------+-------+-------+-------+-------+
| Proc  | >     | code  | 1..1  | SHALL | CD    |       | Conc  |       |
| edure |       |       |       |       |       |       | ept​D |       |
| ​Code |       |       |       |       |       |       | omain |       |
|       |       |       |       |       |       |       | Pro   |       |
|       |       |       |       |       |       |       | cedur |       |
|       |       |       |       |       |       |       | eCode |       |
+-------+-------+-------+-------+-------+-------+-------+-------+-------+
|       | >     | text  | 0..1  | S     | ED    |       |       |       |
|       |       |       |       | HOULD |       |       |       |       |
+-------+-------+-------+-------+-------+-------+-------+-------+-------+
| Ref   | >>    | refe  | 1..1  | SHALL | URL   |       | #     |       |
|       |       | rence |       |       | (XML  |       | *co   |       |
|       |       |       |       |       | I     |       | ntent |       |
|       |       |       |       |       | DREF) |       | ​Ref* |       |
+-------+-------+-------+-------+-------+-------+-------+-------+-------+
| Effe  | >     | effe  | 0..1  | S     | IVL   |       |       |       |
| ctive |       | ctive |       | HOULD | <TS>  |       |       |       |
| ​Time |       | ​Time |       |       |       |       |       |       |
+-------+-------+-------+-------+-------+-------+-------+-------+-------+
| Mod   | >     | m     | 1..\* | SHALL | CD    | SHALL | Val   |       |
| ality |       | ethod |       |       |       | CNE   | ueSet |       |
|       |       | ​Code |       |       |       |       |       |       |
+-------+-------+-------+-------+-------+-------+-------+-------+-------+
| M     | >     | m     | 0..\* | MAY   | CD    |       | Conc  |       |
| ethod |       | ethod |       |       |       |       | ept​D |       |
| ​Code |       | ​Code |       |       |       |       | omain |       |
|       |       |       |       |       |       |       | I     |       |
|       |       |       |       |       |       |       | magin |       |
|       |       |       |       |       |       |       | gTech |       |
|       |       |       |       |       |       |       | nique |       |
+-------+-------+-------+-------+-------+-------+-------+-------+-------+
| T     | >     | t     | 0..\* | S     | CD    |       | Conc  |       |
| arget |       | arget |       | HOULD |       |       | ept​D |       |
| ​Site |       | ​Site |       |       |       |       | omain |       |
|       |       | ​Code |       |       |       |       | Targe |       |
|       |       |       |       |       |       |       | tSite |       |
+-------+-------+-------+-------+-------+-------+-------+-------+-------+
|       | >>    | qual  | 0..1  | COND  |       |       |       |       |
|       |       | ifier |       |       |       |       |       |       |
+-------+-------+-------+-------+-------+-------+-------+-------+-------+
|       | >>>   | name  | 1..1  | SHALL | CD    | SHALL | (     |       |
|       |       |       |       |       |       |       | 27274 |       |
|       |       |       |       |       |       |       | 1003, |       |
|       |       |       |       |       |       |       | S     |       |
|       |       |       |       |       |       |       | NOMED |       |
|       |       |       |       |       |       |       | CT,   |       |
|       |       |       |       |       |       |       | "la   |       |
|       |       |       |       |       |       |       | teral |       |
|       |       |       |       |       |       |       | ity") |       |
+-------+-------+-------+-------+-------+-------+-------+-------+-------+
| Later | >>>   | value | 1..1  | SHALL | CD    | SHALL | Val   |       |
| ality |       |       |       |       |       | CNE   | ueSet |       |
+-------+-------+-------+-------+-------+-------+-------+-------+-------+
|       | >     | par   | 0..1  | COND  |       |       |       |       |
|       |       | ticip |       |       |       |       |       |       |
|       |       | ation |       |       |       |       |       |       |
+-------+-------+-------+-------+-------+-------+-------+-------+-------+
|       | >@    | @typ  | 1..1  | SHALL | CS    | SHALL | LOC   |       |
|       |       | ecode |       |       |       |       |       |       |
+-------+-------+-------+-------+-------+-------+-------+-------+-------+
|       | >>    | p     | 1..1  | SHALL |       |       |       |       |
|       |       | artic |       |       |       |       |       |       |
|       |       | ipant |       |       |       |       |       |       |
|       |       | ​Role |       |       |       |       |       |       |
+-------+-------+-------+-------+-------+-------+-------+-------+-------+
|       | >>@   | class | 1..1  | SHALL | CS    | SHALL | SDLOC |       |
|       |       | ​Code |       |       |       |       |       |       |
+-------+-------+-------+-------+-------+-------+-------+-------+-------+
|       | >>>   | scop  | 1..1  | SHALL |       |       |       |       |
|       |       | ing​E |       |       |       |       |       |       |
|       |       | ntity |       |       |       |       |       |       |
+-------+-------+-------+-------+-------+-------+-------+-------+-------+
| P     | >>>>  | desc  | 1..1  | SHALL | ST    |       |       |       |
| rovid |       |       |       |       |       |       |       |       |
| er​Or |       |       |       |       |       |       |       |       |
| ganiz |       |       |       |       |       |       |       |       |
| ation |       |       |       |       |       |       |       |       |
+-------+-------+-------+-------+-------+-------+-------+-------+-------+

.. _sect_10.4.1:

id
~~

procedure/id does not correspond to any DICOM UID, but is an arbitrary
identifier for this entry.

.. _sect_10.4.2:

code
~~~~

When invoked from the (current) `Imaging Procedure
Description <#sect_9.3>`__, procedure/code SHALL be identical to
documentationOf/serviceEvent/code in the CDA header.

.. _sect_10.4.3:

text/reference and Related Narrative Block Markup
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

The Procedure entry SHOULD include a text/reference element, whose value
attribute SHALL begin with a '#' and SHALL point to its corresponding
narrative in the parent section (using the approach defined in CDA
Release 2, section 4.3.5.1). See `<content> Markup and Links From
Entries <#sect_9.1.1.1>`__.

.. _sect_10.4.4:

methodCode - Modality
~~~~~~~~~~~~~~~~~~~~~

When invoked from the (current) `Imaging Procedure
Description <#sect_9.3>`__, procedure/methodCode used for modality SHALL
be identical to documentationOf/serviceEvent/code/translation used for
modality in the CDA header (see `code and
translation <#sect_8.2.4.1>`__).

.. _sect_10.4.5:

methodCode - Other Parameters
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

method​Code may be used to encode study type, contrast use, challenge,
views, positioning (, , , ), etc.

.. _sect_10.4.6:

targetSiteCode and Laterality
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

procedure/targetSiteCode may be used to encode the specific anatomic
focus, and is not necessarily identical to
documentationOf/serviceEvent/code/translation used for anatomic region
in the CDA header. This may be derived from *Body Part Examined
(0018,0015)*, as mapped to SNOMED codes in , or from *Anatomic Region
Sequence (0008,2218)*.

COND: The qualifier element for laterality SHALL be present if the
targetSiteCode represents a paired body part and laterality is not
pre-coordinated in the targetSiteCode.

.. _sect_10.4.7:

participation - Location
~~~~~~~~~~~~~~~~~~~~~~~~

COND: If this template is invoked from the Comparison Study section,
procedure/participation MAY be used to identify the location (provider
organization) at which the Comparison Study was performed.

::

   <procedure moodCode="EVN" classCode="PROC">
       <templateId root="1.2.840.10008.9.14"/>
       <id root="1.2.840.6544.33.9100653988998717.997527582345600170"/>
       <code code="RPID465"
           displayName="MR NECK ANGIOGRAPHY"
           codeSystem="2.16.840.1.113883.6.256"
           codeSystemName="RadLex"/>
       <text><reference value="#proc"/></text>
       <effectiveTime value="20140913222400"/>
       <methodCode code="MR"
           displayName="Magnetic Resonance"
           codeSystem="1.2.840.10008.2.16.4" codeSystemName="DCM"/>
       <targetSiteCode code="45048000"
           codeSystem="2.16.840.1.113883.6.96" codeSystemName="SNOMED CT"
           displayName="Neck (structure)">
       </targetSiteCode>
   </procedure>

.. _sect_10.5:

Quantity Measurement
--------------------

+----------------------+----------------------------------------------+
| **Template ID**      | 2.16.840.1.113883.​10.20.6.2.14              |
+----------------------+----------------------------------------------+
| **Name**             | Quantity Measurement                         |
+----------------------+----------------------------------------------+
| **Effective Date**   | 2015/03/24                                   |
+----------------------+----------------------------------------------+
| **Version Label**    | DICOM-20150324                               |
+----------------------+----------------------------------------------+
| **Status**           | Active                                       |
+----------------------+----------------------------------------------+
| **Description**      | A Quantity Measurement records quantitative  |
|                      | measurements such as linear, area, volume,   |
|                      | and numeric measurements. If based on image  |
|                      | data, a reference to the image may be        |
|                      | present.                                     |
+----------------------+----------------------------------------------+
| **Classification**   | CDA Entry Level                              |
+----------------------+----------------------------------------------+
| **Relationships**    |                                              |
+----------------------+----------------------------------------------+
| **Context**          | parent node                                  |
+----------------------+----------------------------------------------+
| **Open/Closed**      | open                                         |
+----------------------+----------------------------------------------+
| **Revision History** | DICOM-20150324: Initial publication, derived |
|                      | from template originally published in DIR    |
|                      | r1-2009, revised in Consolidated CDA r1-2011 |
|                      | as 2.16.840.1.113883.10.20.6.2.14. This      |
|                      | derivation includes Units of Measure         |
|                      | specified with DICOM value set for UCUM (),  |
|                      | equivalent to C-CDA specified value set      |
|                      | (UCUM Units of Measure (case sensitive)      |
|                      | 2.16.840.1.113883.11.12839); addition of     |
|                      | optional interpretationCode and actionable   |
|                      | priority                                     |
+----------------------+----------------------------------------------+

+-------+-------+-------+-------+-------+-------+-------+-------+-------+
| Bus   | Nest  | Ele   | Card  | Elem  | Data  | Value | Value | Subsi |
| iness | Level | ment/ |       | /Attr | Type  | Conf  |       | diary |
| Name  |       | ​Attr |       | Conf  |       |       |       | Tem   |
|       |       | ibute |       |       |       |       |       | plate |
+=======+=======+=======+=======+=======+=======+=======+=======+=======+
| **    |       | o     | 1..1  | SHALL |       |       |       |       |
| Quant |       | bserv |       |       |       |       |       |       |
| ity​M |       | ation |       |       |       |       |       |       |
| easur |       |       |       |       |       |       |       |       |
| ement |       |       |       |       |       |       |       |       |
| [*]** |       |       |       |       |       |       |       |       |
+-------+-------+-------+-------+-------+-------+-------+-------+-------+
|       | @     | @clas | 1..1  | SHALL | CS    | SHALL | OBS   |       |
|       |       | sCode |       |       |       |       |       |       |
+-------+-------+-------+-------+-------+-------+-------+-------+-------+
|       | @     | @moo  | 1..1  | SHALL | CS    | SHALL | EVN   |       |
|       |       | dCode |       |       |       |       |       |       |
+-------+-------+-------+-------+-------+-------+-------+-------+-------+
|       | >     | t     | 1..1  | SHALL | II    |       |       |       |
|       |       | empla |       |       |       |       |       |       |
|       |       | te​Id |       |       |       |       |       |       |
+-------+-------+-------+-------+-------+-------+-------+-------+-------+
|       | >@    | @root | 1..1  | SHALL | UID   | SHALL | 2     |       |
|       |       |       |       |       |       |       | .16.8 |       |
|       |       |       |       |       |       |       | 40.1. |       |
|       |       |       |       |       |       |       | 11388 |       |
|       |       |       |       |       |       |       | 3.​10 |       |
|       |       |       |       |       |       |       | .20.6 |       |
|       |       |       |       |       |       |       | .2.14 |       |
+-------+-------+-------+-------+-------+-------+-------+-------+-------+
|       | >     | id    | 1..1  | SHALL | II    |       |       |       |
+-------+-------+-------+-------+-------+-------+-------+-------+-------+
| M     | >     | code  | 1..1  | SHALL | CD    |       | Conc  |       |
| easur |       |       |       |       |       |       | ept​D |       |
| ement |       |       |       |       |       |       | omain |       |
| ​Name |       |       |       |       |       |       | Obser |       |
|       |       |       |       |       |       |       | vatio |       |
|       |       |       |       |       |       |       | nType |       |
+-------+-------+-------+-------+-------+-------+-------+-------+-------+
|       | >     | text  | 0..1  | S     |       |       |       |       |
|       |       |       |       | HOULD |       |       |       |       |
+-------+-------+-------+-------+-------+-------+-------+-------+-------+
| Ref   | >>    | refe  | 1..1  | SHALL | URL   |       | #     |       |
|       |       | rence |       |       | (XML  |       | *co   |       |
|       |       |       |       |       | I     |       | ntent |       |
|       |       |       |       |       | DREF) |       | ​Ref* |       |
+-------+-------+-------+-------+-------+-------+-------+-------+-------+
|       | >     | s     | 1..1  | SHALL | CS    | SHALL | COMP  |       |
|       |       | tatus |       |       |       |       | LETED |       |
|       |       | ​Code |       |       |       |       |       |       |
+-------+-------+-------+-------+-------+-------+-------+-------+-------+
| Time  | >     | effe  | 0..1  | S     | TS    |       |       |       |
|       |       | ctive |       | HOULD |       |       |       |       |
|       |       | ​Time |       |       |       |       |       |       |
+-------+-------+-------+-------+-------+-------+-------+-------+-------+
|       | >     | value | 1..1  | SHALL |       |       |       |       |
+-------+-------+-------+-------+-------+-------+-------+-------+-------+
|       | >@    | @xsi  | 1..1  | SHALL | ST    | SHALL | PQ    |       |
|       |       | :type |       |       |       |       |       |       |
+-------+-------+-------+-------+-------+-------+-------+-------+-------+
| Me    | >@    | @     | 1..1  | SHALL | REAL  |       |       |       |
| asure |       | value |       |       |       |       |       |       |
| ment​ |       |       |       |       |       |       |       |       |
| Value |       |       |       |       |       |       |       |       |
+-------+-------+-------+-------+-------+-------+-------+-------+-------+
| Me    | >@    | @unit | 1..1  | SHALL | CS    | SHALL | Val   |       |
| asure |       |       |       |       |       |       | ueSet |       |
| ment​ |       |       |       |       |       | CNE   |       |       |
| Units |       |       |       |       |       |       |       |       |
+-------+-------+-------+-------+-------+-------+-------+-------+-------+
| Inte  | >     | inte  | 0..1  | MAY   | CE    | SHALL | Val   |       |
| rpret |       | rpret |       |       |       | CNE   | ueSet |       |
| ation |       | ation |       |       |       |       | 2.1   |       |
| ​Code |       | ​Code |       |       |       |       | 6.840 |       |
|       |       |       |       |       |       |       | .1.11 |       |
|       |       |       |       |       |       |       | 3883. |       |
|       |       |       |       |       |       |       | 11.78 |       |
+-------+-------+-------+-------+-------+-------+-------+-------+-------+
| Acti  | >>    | t     | 1..1  | MAY   | CD    | MAY   | Val   |       |
| onabl |       | ransl |       |       |       | CWE   | ueSet |       |
| e​Pri |       | ation |       |       |       |       |       |       |
| ority |       |       |       |       |       |       | [See  |       |
|       |       |       |       |       |       |       | `int  |       |
|       |       |       |       |       |       |       | erpre |       |
|       |       |       |       |       |       |       | tatio |       |
|       |       |       |       |       |       |       | nCode |       |
|       |       |       |       |       |       |       | and   |       |
|       |       |       |       |       |       |       | t     |       |
|       |       |       |       |       |       |       | ransl |       |
|       |       |       |       |       |       |       | ation |       |
|       |       |       |       |       |       |       | For   |       |
|       |       |       |       |       |       |       | Actio |       |
|       |       |       |       |       |       |       | nable |       |
|       |       |       |       |       |       |       | Fi    |       |
|       |       |       |       |       |       |       | nding |       |
|       |       |       |       |       |       |       | s <#s |       |
|       |       |       |       |       |       |       | ect_1 |       |
|       |       |       |       |       |       |       | 0.1.3 |       |
|       |       |       |       |       |       |       | >`__] |       |
+-------+-------+-------+-------+-------+-------+-------+-------+-------+
| T     | >     | t     | 1..1  | COND  | CD    |       | Conc  |       |
| arget |       | arget |       |       |       |       | ept​D |       |
| ​Site |       | ​Site |       |       |       |       | omain |       |
|       |       | ​Code |       |       |       |       | Obser |       |
|       |       |       |       |       |       |       | vatio |       |
|       |       |       |       |       |       |       | nSite |       |
+-------+-------+-------+-------+-------+-------+-------+-------+-------+
|       | >>    | qual  | 0..1  | COND  |       |       |       |       |
|       |       | ifier |       |       |       |       |       |       |
+-------+-------+-------+-------+-------+-------+-------+-------+-------+
|       | >>>   | name  | 1..1  | SHALL | CD    | SHALL | (     |       |
|       |       |       |       |       |       |       | 27274 |       |
|       |       |       |       |       |       |       | 1003, |       |
|       |       |       |       |       |       |       | S     |       |
|       |       |       |       |       |       |       | NOMED |       |
|       |       |       |       |       |       |       | CT,   |       |
|       |       |       |       |       |       |       | "la   |       |
|       |       |       |       |       |       |       | teral |       |
|       |       |       |       |       |       |       | ity") |       |
+-------+-------+-------+-------+-------+-------+-------+-------+-------+
| Later | >>>   | value | 1..1  | SHALL | CD    | SHALL | Val   |       |
| ality |       |       |       |       |       | CNE   | ueSet |       |
+-------+-------+-------+-------+-------+-------+-------+-------+-------+
|       | >>    | qual  | 0..1  | COND  |       |       |       |       |
|       |       | ifier |       |       |       |       |       |       |
+-------+-------+-------+-------+-------+-------+-------+-------+-------+
|       | >>>   | name  | 1..1  | SHALL | CD    | SHALL | (     |       |
|       |       |       |       |       |       |       | 10623 |       |
|       |       |       |       |       |       |       | 3006, |       |
|       |       |       |       |       |       |       | S     |       |
|       |       |       |       |       |       |       | NOMED |       |
|       |       |       |       |       |       |       | CT,   |       |
|       |       |       |       |       |       |       | "Top  |       |
|       |       |       |       |       |       |       | ograp |       |
|       |       |       |       |       |       |       | hical |       |
|       |       |       |       |       |       |       | modif |       |
|       |       |       |       |       |       |       | ier") |       |
+-------+-------+-------+-------+-------+-------+-------+-------+-------+
| Top   | >>>   | value | 1..1  | SHALL | CD    | SHALL | Val   |       |
| o​Mod |       |       |       |       |       | CNE   | ueSet |       |
| ifier |       |       |       |       |       |       |       |       |
+-------+-------+-------+-------+-------+-------+-------+-------+-------+
| M     | >     | m     | 0..1  | MAY   | CD    |       | Conc  |       |
| ethod |       | ethod |       |       |       |       | ept​D |       |
|       |       | ​Code |       |       |       |       | omain |       |
|       |       |       |       |       |       |       | Ob    |       |
|       |       |       |       |       |       |       | serva |       |
|       |       |       |       |       |       |       | tionM |       |
|       |       |       |       |       |       |       | ethod |       |
+-------+-------+-------+-------+-------+-------+-------+-------+-------+
|       | >     | ent   | 0..\* | MAY   |       |       |       |       |
|       |       | ry​Re |       |       |       |       |       |       |
|       |       | latio |       |       |       |       |       |       |
|       |       | nship |       |       |       |       |       |       |
+-------+-------+-------+-------+-------+-------+-------+-------+-------+
|       | >@    | @typ  | 1..1  | SHALL | CS    | SHALL | SPRT  |       |
|       |       | eCode |       |       |       |       |       |       |
+-------+-------+-------+-------+-------+-------+-------+-------+-------+
| *     | >>    | *ob   | 1..1  | SHALL |       |       |       | `SOP  |
| SOPIn |       | serva |       |       |       |       |       | Ins   |
| stanc |       | tion* |       |       |       |       |       | tance |
| e[*]* |       |       |       |       |       |       |       | Ob    |
|       |       |       |       |       |       |       |       | serva |
|       |       |       |       |       |       |       |       | tion  |
|       |       |       |       |       |       |       |       | <#sec |
|       |       |       |       |       |       |       |       | t_10. |
|       |       |       |       |       |       |       |       | 8>`__ |
|       |       |       |       |       |       |       |       | 1.2   |
|       |       |       |       |       |       |       |       | .840. |
|       |       |       |       |       |       |       |       | 10008 |
|       |       |       |       |       |       |       |       | .9.18 |
+-------+-------+-------+-------+-------+-------+-------+-------+-------+
|       | >     | *entr | 0..\* | MAY   |       |       |       |       |
|       |       | y​Rel |       |       |       |       |       |       |
|       |       | ation |       |       |       |       |       |       |
|       |       | ship* |       |       |       |       |       |       |
+-------+-------+-------+-------+-------+-------+-------+-------+-------+
|       | >@    | *     | 1..1  | SHALL | CS    | SHALL | SPRT  |       |
|       |       | @type |       |       |       |       |       |       |
|       |       | Code* |       |       |       |       |       |       |
+-------+-------+-------+-------+-------+-------+-------+-------+-------+
| *Quan | >     | *ob   | 1..1  | SHALL |       |       |       | `Qua  |
| tity​ |       | serva |       |       |       |       |       | ntity |
| Measu |       | tion* |       |       |       |       |       | Me    |
| remen |       |       |       |       |       |       |       | asure |
| t[*]* |       |       |       |       |       |       |       | ment  |
|       |       |       |       |       |       |       |       | <#sec |
|       |       |       |       |       |       |       |       | t_10. |
|       |       |       |       |       |       |       |       | 5>`__ |
|       |       |       |       |       |       |       |       | 2     |
|       |       |       |       |       |       |       |       | .16.8 |
|       |       |       |       |       |       |       |       | 40.1. |
|       |       |       |       |       |       |       |       | 11388 |
|       |       |       |       |       |       |       |       | 3.​10 |
|       |       |       |       |       |       |       |       | .20.6 |
|       |       |       |       |       |       |       |       | .2.14 |
+-------+-------+-------+-------+-------+-------+-------+-------+-------+

.. _sect_10.5.1:

text/reference and Related Narrative Block Markup
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

The Observation entry SHOULD include a text/reference element, whose
**value** attribute (not to be confused with the **value** element of
the Observation class) SHALL begin with a '#' and SHALL point to its
corresponding narrative in the parent section (using the approach
defined in CDA Release 2, section 4.3.5.1). See `<content> Markup and
Links From Entries <#sect_9.1.1.1>`__.

.. _sect_10.5.2:

interpretationCode and Translation For Actionable Findings
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

When a measurement is out of normal range, it may be flagged using the
interpretationCode. Very abnormal values, often denoted as exceeding
"panic limits", or as "actionable" or "critical findings", may have
values such as (LL, ObservationInterpretation, "low alert"), (HH,
ObservationInterpretation, "high alert"), or (AA,
ObservationInterpretation, "abnormal alert").

The translation element of the interpretationCode may be used to provide
a further classification as defined in a regionally- or
professionally-specified value set. This template identifies an optional
value set for the ACR Actionable Finding categories 1, 2, and 3, as
defined by: Larson PA, et al. J Am Coll Radiol 2014; published online.
DOI 10.1016/j.jacr.2013.12.016.

The narrative text associated with the actionable finding SHOULD be
highlighted using styleCode Bold. See `<content> Markup and Links From
Entries <#sect_9.1.1.1>`__.

Actionable findings that require a specific follow-up action or
procedure SHOULD be referenced from a recommendation in the
`Recommendation <#sect_9.8.11>`__ Section.

Communication of actionable findings SHOULD be documented in the
`Communication of Actionable Findings <#sect_9.8.10>`__ Section.

.. _sect_10.5.3:

targetSiteCode
~~~~~~~~~~~~~~

Each observation needs to fully specify its site/location.

COND: If the observation site is not pre-coordinated in the
observation/code, it SHALL be specified in the
observation/targetSiteCode.

COND: The qualifier element for laterality SHALL be present if the
targetSiteCode represents a paired body part and laterality is not
pre-coordinated in the targetSiteCode.

COND: The qualifier element for topographical modifier SHALL be present
if the targetSiteCode does not fully specify the observation location in
sufficient detail.

.. note::

   Inclusion of a site name in a labeled subsection title (see `Labeled
   Subsection <#sect_9.8.9>`__) does not imply a finding site for
   observations within that subsection. The title is not semantically
   part of the post-coordination, and target sites must be explicitly
   identified.

   See `example_title <#example_10.5-2>`__, an example of a measurement
   using a topographical modifier qualifier.

::

   <text> ...
       <content ID="Q21" styleCode="Bold">Calcium score (Agatston) : 817 [HIGH - ACR Cat3]</content>
       ...
   </text>
   <entry>
       <observation classCode="OBS" moodCode="EVN">
           <templateId root="2.16.840.1.113883.10.20.6.2.14"/>
           <id root="1.2.840.10213.2.62.7044234.11652014"/>
           <code code="112058" codeSystem="1.2.840.10008.2.16.4"
               codeSystemName="DCM" displayName="Calcium score" />
           <text><reference value="#Q21"/></text>
           <statusCode code="COMPLETED"/>
           <effectiveTime value="20140913223912"/>
           <value xsi:type="PQ" unit="[arb'U]" value="817" />
           <interpretationCode code="HH" codeSystem="2.16.840.1.113883.5.83"
                   codeSystemName="ObservationInterpretation" displayName="High alert">
               <translation code="RID49482" codeSystem="2.16.840.1.113883.6.256"
                   codeSystemName="RADLEX" displayName="ACR Category 3 Actionable Finding" />
           </interpretationCode>
           <methodCode code="112055" codeSystem="1.2.840.10008.2.16.4"
               codeSystemName="DCM" displayName="Agatston" />
           <!-- entryRelationships to SOP Instance Observations may go here -->
       </observation>
   </entry>

::

   <section>
       <title>Left femoral artery</title>
       <text>
           ...
           <content ID="M10">Distal lumen stenosis: 75%</content>
           ...
       </text>
       <entry>
           <observation classCode="OBS" moodCode="EVN">
               <templateId root="2.16.840.1.113883.10.20.6.2.14"/>
               <id root="1.2.840.10213.2.62.7044234.988810005"/>
               <code code="408714007" codeSystem="2.16.840.1.113883.6.96"
                   codeSystemName=" SNOMED CT"
                   displayName="Vessel lumen diameter reduction" />
               <text><reference value="#M10"/></text>
               <statusCode code="COMPLETED"/>
               <effectiveTime value="20140913223912"/>
               <value xsi:type="PQ" unit="%" value="75" />
               <targetSiteCode code="113270003"
                       codeSystem="2.16.840.1.113883.6.96" codeSystemName="SNOMED CT"
                       displayName="Left femoral artery">
                   <qualifier>
                       <name code="106233006" codeSystem="2.16.840.1.113883.6.96"
                           codeSystemName="SNOMED CT" displayName="Topographical modifier" />
                       <value code="46053002" codeSystem="2.16.840.1.113883.6.96"
                           codeSystemName="SNOMED CT" displayName="Distal" />
                   </qualifier>
               </targetSiteCode>
           </observation>
       </entry>
   </section>

.. _sect_10.6:

Study Act
---------

+----------------------+----------------------------------------------+
| **Template ID**      | 1.2.840.10008.9.16                           |
+----------------------+----------------------------------------------+
| **Name**             | Study Act                                    |
+----------------------+----------------------------------------------+
| **Effective Date**   | 2015/03/24                                   |
+----------------------+----------------------------------------------+
| **Version Label**    | DICOM-20150324                               |
+----------------------+----------------------------------------------+
| **Status**           | Active                                       |
+----------------------+----------------------------------------------+
| **Description**      | A Study Act contains the DICOM study         |
|                      | information that defines the characteristics |
|                      | of an imaging study performed on a patient.  |
|                      | An imaging study is a collection of one or   |
|                      | more series of medical images, presentation  |
|                      | states, SR documents, overlays, and/or       |
|                      | curves that are logically related for the    |
|                      | purpose of diagnosing a patient. Each study  |
|                      | is associated with exactly one patient. A    |
|                      | study may include composite instances that   |
|                      | are created by a single modality, multiple   |
|                      | modalities, or by multiple devices of the    |
|                      | same modality. The study information is      |
|                      | modality-independent.                        |
+----------------------+----------------------------------------------+
| **Classification**   | CDA Entry Level                              |
+----------------------+----------------------------------------------+
| **Relationships**    | Included in `DICOM Object                    |
|                      | Catalog <#sect_9.8.7>`__ and `Comparison     |
|                      | Study <#sect_9.4>`__                         |
+----------------------+----------------------------------------------+
| **Context**          | parent node                                  |
+----------------------+----------------------------------------------+
| **Open/Closed**      | Open                                         |
+----------------------+----------------------------------------------+
| **Revision History** | DICOM-20150324: Initial publication, derived |
|                      | from template originally published in DIR    |
|                      | r1-2009, revised in Consolidated CDA r1-2011 |
|                      | as 2.16.840.1.113883.10.20.6.2.6. This       |
|                      | derivation makes Series conditional          |
|                      | (required for Object Catalog) to support use |
|                      | in Comparison Study reference, and uses      |
|                      | DICOM-20150324 Series Act subsidiary         |
|                      | template.                                    |
+----------------------+----------------------------------------------+

+-------+-------+-------+-------+-------+-------+-------+-------+-------+
| Bus   | Nest  | Ele   | Card  | Elem  | Data  | Value | Value | Subsi |
| iness | Level | ment/ |       | /Attr | Type  | Conf  |       | diary |
| Name  |       | ​Attr |       | Conf  |       |       |       | Tem   |
|       |       | ibute |       |       |       |       |       | plate |
+=======+=======+=======+=======+=======+=======+=======+=======+=======+
| **    |       | act   | 1..1  | SHALL |       |       |       |       |
| Study |       |       |       |       |       |       |       |       |
| [*]** |       |       |       |       |       |       |       |       |
+-------+-------+-------+-------+-------+-------+-------+-------+-------+
|       | @     | @clas | 1..1  | SHALL | CS    | SHALL | ACT   |       |
|       |       | sCode |       |       |       |       |       |       |
+-------+-------+-------+-------+-------+-------+-------+-------+-------+
|       | @     | @moo  | 1..1  | SHALL | CS    | SHALL | EVN   |       |
|       |       | dCode |       |       |       |       |       |       |
+-------+-------+-------+-------+-------+-------+-------+-------+-------+
|       | >     | t     | 1..1  | SHALL | II    |       |       |       |
|       |       | empla |       |       |       |       |       |       |
|       |       | te​Id |       |       |       |       |       |       |
+-------+-------+-------+-------+-------+-------+-------+-------+-------+
|       | >@    | @root | 1..1  | SHALL | UID   | SHALL | 1.2   |       |
|       |       |       |       |       |       |       | .840. |       |
|       |       |       |       |       |       |       | 10008 |       |
|       |       |       |       |       |       |       | .9.16 |       |
+-------+-------+-------+-------+-------+-------+-------+-------+-------+
|       | >     | id    | 1..1  | SHALL | II    |       |       |       |
+-------+-------+-------+-------+-------+-------+-------+-------+-------+
| Stud  | >@    | @root | 1..1  | SHALL | UID   |       | *     |       |
| y​UID |       |       |       |       |       |       | Study |       |
|       |       |       |       |       |       |       | Ins   |       |
|       |       |       |       |       |       |       | tance |       |
|       |       |       |       |       |       |       | UID   |       |
|       |       |       |       |       |       |       | (0    |       |
|       |       |       |       |       |       |       | 020,0 |       |
|       |       |       |       |       |       |       | 00D)* |       |
+-------+-------+-------+-------+-------+-------+-------+-------+-------+
|       | >@    | @exte | 0..0  | SHALL |       |       |       |       |
|       |       | nsion |       | NOT   |       |       |       |       |
+-------+-------+-------+-------+-------+-------+-------+-------+-------+
|       | >     | code  | 1..1  | SHALL | CD    | SHALL | (11   |       |
|       |       |       |       |       |       |       | 3014, |       |
|       |       |       |       |       |       |       | DCM,  |       |
|       |       |       |       |       |       |       | "St   |       |
|       |       |       |       |       |       |       | udy") |       |
+-------+-------+-------+-------+-------+-------+-------+-------+-------+
| D     | >     | text  | 0..1  | MAY   | ED    |       |       |       |
| escri |       |       |       |       |       |       |       |       |
| ption |       |       |       |       |       |       |       |       |
+-------+-------+-------+-------+-------+-------+-------+-------+-------+
| Time  | >     | effe  | 0..1  | S     | TS    |       | *     |       |
|       |       | ctive |       | HOULD |       |       | Study |       |
|       |       | ​Time |       |       |       |       | Date  |       |
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
+-------+-------+-------+-------+-------+-------+-------+-------+-------+
|       | >     | ent   | 1..\* | COND  |       |       |       |       |
|       |       | ry​Re |       |       |       |       |       |       |
|       |       | latio |       |       |       |       |       |       |
|       |       | nship |       |       |       |       |       |       |
+-------+-------+-------+-------+-------+-------+-------+-------+-------+
|       | >@    | @typ  | 1..1  | SHALL | CS    | SHALL | COMP  |       |
|       |       | eCode |       |       |       |       |       |       |
+-------+-------+-------+-------+-------+-------+-------+-------+-------+
| *     | >>    | *act* |       |       |       |       |       | `S    |
| Serie |       |       |       |       |       |       |       | eries |
| s[*]* |       |       |       |       |       |       |       | Act   |
|       |       |       |       |       |       |       |       | <#sec |
|       |       |       |       |       |       |       |       | t_10. |
|       |       |       |       |       |       |       |       | 7>`__ |
|       |       |       |       |       |       |       |       | 1.2   |
|       |       |       |       |       |       |       |       | .840. |
|       |       |       |       |       |       |       |       | 10008 |
|       |       |       |       |       |       |       |       | .9.17 |
+-------+-------+-------+-------+-------+-------+-------+-------+-------+

.. _sect_10.6.1:

entryRelationship/act - Series
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

COND: If this template is invoked by the `DICOM Object
Catalog <#sect_9.8.7>`__, the entryRelationship to the Series act SHALL
be present, otherwise it MAY be present.

::

   <act classCode="ACT" moodCode="EVN">
       <templateId root="2.16.840.1.113883.10.20.6.2.6"/>
       <id root="1.2.840.113619.2.62.994044785528.114289542805"/>
       <code code="113014" codeSystem="1.2.840.10008.2.16.4"
           codeSystemName="DCM" displayName="Study"/>
       <effectiveTime value="20060823223232"/>
       <!-- **** Series ****-->
       <entryRelationship typeCode="COMP">
           <act classCode="ACT" moodCode="EVN">
               ...
           </act>
       </entryRelationship>
   </act>

.. _sect_10.7:

Series Act
----------

+----------------------+----------------------------------------------+
| **Template ID**      | 1.2.840.10008.9.17                           |
+----------------------+----------------------------------------------+
| **Name**             | Series Act                                   |
+----------------------+----------------------------------------------+
| **Effective Date**   | 2015/03/24                                   |
+----------------------+----------------------------------------------+
| **Version Label**    | DICOM-20150324                               |
+----------------------+----------------------------------------------+
| **Status**           | Active                                       |
+----------------------+----------------------------------------------+
| **Description**      | A Series Act contains the DICOM series       |
|                      | information for referenced DICOM composite   |
|                      | objects. The series information defines the  |
|                      | attributes that are used to group composite  |
|                      | instances into distinct logical sets. Each   |
|                      | series is associated with exactly one study. |
|                      | Series Act clinical statements are only      |
|                      | instantiated in the `DICOM Object            |
|                      | Catalog <#sect_9.8.7>`__ section inside a    |
|                      | `Study Act <#sect_10.6>`__.                  |
+----------------------+----------------------------------------------+
| **Classification**   | CDA Entry Level                              |
+----------------------+----------------------------------------------+
| **Relationships**    | Included in `Study Act <#sect_10.6>`__       |
+----------------------+----------------------------------------------+
| **Context**          | parent node                                  |
+----------------------+----------------------------------------------+
| **Open/Closed**      | open                                         |
+----------------------+----------------------------------------------+
| **Revision History** | DICOM-20150324: Initial publication, derived |
|                      | from template originally published in DIR    |
|                      | r1-2009, revised in Consolidated CDA r1-2011 |
|                      | as 2.16.840.1.113883.10.20.22.4.63. This     |
|                      | derivation uses DICOM-20150324 SOP Instance  |
|                      | subsidiary template.                         |
+----------------------+----------------------------------------------+

+-------+-------+-------+-------+-------+-------+-------+-------+-------+
| Bus   | Nest  | Ele   | Card  | Elem  | Data  | Value | Value | Subsi |
| iness | Level | ment/ |       | /Attr | Type  | Conf  |       | diary |
| Name  |       | ​Attr |       | Conf  |       |       |       | Tem   |
|       |       | ibute |       |       |       |       |       | plate |
+=======+=======+=======+=======+=======+=======+=======+=======+=======+
| **S   |       | act   | 1..1  | SHALL |       |       |       |       |
| eries |       |       |       |       |       |       |       |       |
| [*]** |       |       |       |       |       |       |       |       |
+-------+-------+-------+-------+-------+-------+-------+-------+-------+
|       | @     | @clas | 1..1  | SHALL | CS    | SHALL | ACT   |       |
|       |       | sCode |       |       |       |       |       |       |
+-------+-------+-------+-------+-------+-------+-------+-------+-------+
|       | @     | @moo  | 1..1  | SHALL | CS    | SHALL | EVN   |       |
|       |       | dCode |       |       |       |       |       |       |
+-------+-------+-------+-------+-------+-------+-------+-------+-------+
|       | >     | t     | 1..1  | SHALL | II    |       |       |       |
|       |       | empla |       |       |       |       |       |       |
|       |       | te​Id |       |       |       |       |       |       |
+-------+-------+-------+-------+-------+-------+-------+-------+-------+
|       | >@    | @root | 1..1  | SHALL | UID   | SHALL | 1.2   |       |
|       |       |       |       |       |       |       | .840. |       |
|       |       |       |       |       |       |       | 10008 |       |
|       |       |       |       |       |       |       | .9.17 |       |
+-------+-------+-------+-------+-------+-------+-------+-------+-------+
|       | >     | id    | 1..1  | SHALL |       |       |       |       |
+-------+-------+-------+-------+-------+-------+-------+-------+-------+
| Serie | >@    | @root | 1..1  | SHALL | UID   |       | *S    |       |
| s​UID |       |       |       |       |       |       | eries |       |
|       |       |       |       |       |       |       | Ins   |       |
|       |       |       |       |       |       |       | tance |       |
|       |       |       |       |       |       |       | UID   |       |
|       |       |       |       |       |       |       | (0    |       |
|       |       |       |       |       |       |       | 020,0 |       |
|       |       |       |       |       |       |       | 00E)* |       |
+-------+-------+-------+-------+-------+-------+-------+-------+-------+
|       | >@    | @exte | 0..0  | SHALL |       |       |       |       |
|       |       | nsion |       | NOT   |       |       |       |       |
+-------+-------+-------+-------+-------+-------+-------+-------+-------+
|       | >     | code  | 1..1  | SHALL | CD    | SHALL | (11   |       |
|       |       |       |       |       |       |       | 3015, |       |
|       |       |       |       |       |       |       | DCM,  |       |
|       |       |       |       |       |       |       | "Ser  |       |
|       |       |       |       |       |       |       | ies") |       |
+-------+-------+-------+-------+-------+-------+-------+-------+-------+
|       | >>    | qual  | 1..1  | SHALL |       |       |       |       |
|       |       | ifier |       |       |       |       |       |       |
+-------+-------+-------+-------+-------+-------+-------+-------+-------+
|       | >>>   | name  | 1..1  | SHALL | CD    | SHALL | (12   |       |
|       |       |       |       |       |       |       | 1139, |       |
|       |       |       |       |       |       |       | DCM,  |       |
|       |       |       |       |       |       |       | "     |       |
|       |       |       |       |       |       |       | Modal |       |
|       |       |       |       |       |       |       | ity") |       |
+-------+-------+-------+-------+-------+-------+-------+-------+-------+
| Mod   | >>>   | value | 1..1  | SHALL | CD    |       | *Mod  |       |
| ality |       |       |       |       |       |       | ality |       |
|       |       |       |       |       |       |       | (0    |       |
|       |       |       |       |       |       |       | 008,0 |       |
|       |       |       |       |       |       |       | 060)* |       |
+-------+-------+-------+-------+-------+-------+-------+-------+-------+
| D     | >     | text  | 0..1  | MAY   | ED    |       |       |       |
| escri |       |       |       |       |       |       |       |       |
| ption |       |       |       |       |       |       |       |       |
+-------+-------+-------+-------+-------+-------+-------+-------+-------+
| Time  | >     | effe  | 0..1  | S     | TS    |       | *S    |       |
|       |       | ctive |       | HOULD |       |       | eries |       |
|       |       | ​Time |       |       |       |       | Date  |       |
|       |       |       |       |       |       |       | (     |       |
|       |       |       |       |       |       |       | 0008, |       |
|       |       |       |       |       |       |       | 0021) |       |
|       |       |       |       |       |       |       | +     |       |
|       |       |       |       |       |       |       | S     |       |
|       |       |       |       |       |       |       | eries |       |
|       |       |       |       |       |       |       | Time  |       |
|       |       |       |       |       |       |       | (     |       |
|       |       |       |       |       |       |       | 0008, |       |
|       |       |       |       |       |       |       | 0031) |       |
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
+-------+-------+-------+-------+-------+-------+-------+-------+-------+
|       | >     | ent   | 1..\* | SHALL |       |       |       |       |
|       |       | ry​Re |       |       |       |       |       |       |
|       |       | latio |       |       |       |       |       |       |
|       |       | nship |       |       |       |       |       |       |
+-------+-------+-------+-------+-------+-------+-------+-------+-------+
|       | >@    | @typ  | 1..1  | SHALL | CS    | SHALL | COMP  |       |
|       |       | eCode |       |       |       |       |       |       |
+-------+-------+-------+-------+-------+-------+-------+-------+-------+
| *     | >>    | *ob   | 1..1  |       |       |       |       | `SOP  |
| SOPIn |       | serva |       |       |       |       |       | Ins   |
| stanc |       | tion* |       |       |       |       |       | tance |
| e[*]* |       |       |       |       |       |       |       | Ob    |
|       |       |       |       |       |       |       |       | serva |
|       |       |       |       |       |       |       |       | tion  |
|       |       |       |       |       |       |       |       | <#sec |
|       |       |       |       |       |       |       |       | t_10. |
|       |       |       |       |       |       |       |       | 8>`__ |
|       |       |       |       |       |       |       |       | 1.2   |
|       |       |       |       |       |       |       |       | .840. |
|       |       |       |       |       |       |       |       | 10008 |
|       |       |       |       |       |       |       |       | .9.18 |
+-------+-------+-------+-------+-------+-------+-------+-------+-------+

::

   <act classCode="ACT" moodCode="EVN">
       <templateId root="1.2.840.10008.9.17"/>
       <id root="1.2.840.113619.2.62.994044785528.20060823223142485051"/>
       <code code="113015" codeSystem="1.2.840.10008.2.16.4"
               codeSystemName="DCM" displayName="Series">
           <qualifier>
               <name code="121139" codeSystem="1.2.840.10008.2.16.4"
                   codeSystemName="DCM"
                   displayName="Modality"/>
               <value code="CR" codeSystem="1.2.840.10008.2.16.4"
                   codeSystemName="DCM"
                   displayName="Computed Radiography"/>
           </qualifier>
       </code>
       <!-- **** SOP Instance UID *** -->
       <entryRelationship typeCode="COMP">
           <observation classCode="DGIMG" moodCode="EVN">
               <templateId root="2.16.840.1.113883.10.20.6.2.8"/>
               ...
           </observation>
       </entryRelationship>
   </act>

.. _sect_10.8:

SOP Instance Observation
------------------------

+----------------------+----------------------------------------------+
| **Template ID**      | 1.2.840.10008.9.18                           |
+----------------------+----------------------------------------------+
| **Name**             | SOP Instance Observation                     |
+----------------------+----------------------------------------------+
| **Effective Date**   | 2015/03/24                                   |
+----------------------+----------------------------------------------+
| **Version Label**    | DICOM-20150324                               |
+----------------------+----------------------------------------------+
| **Status**           | Active                                       |
+----------------------+----------------------------------------------+
| **Description**      | A SOP Instance Observation contains the      |
|                      | DICOM Service Object Pair (SOP) Instance     |
|                      | information for referenced DICOM composite   |
|                      | objects. The SOP Instance act class is used  |
|                      | to reference both image and non-image DICOM  |
|                      | instances. The text attribute contains the   |
|                      | DICOM WADO reference.                        |
+----------------------+----------------------------------------------+
| **Classification**   | CDA Entry Level                              |
+----------------------+----------------------------------------------+
| **Relationships**    |                                              |
+----------------------+----------------------------------------------+
| **Context**          | parent node                                  |
+----------------------+----------------------------------------------+
| **Open/Closed**      | open                                         |
+----------------------+----------------------------------------------+
| **Revision History** | DICOM-20150324: Initial publication, derived |
|                      | from template originally published in DIR    |
|                      | r1-2009, revised in Consolidated CDA r1-2011 |
|                      | as 2.16.840.1.113883.10.20.6.2.8             |
|                      |                                              |
|                      | This derivation includes Purpose of          |
|                      | Reference value set specified with DICOM CID |
|                      | 7003; directly incorporates descendant       |
|                      | templates Purpose of Reference Observation,  |
|                      | Referenced Frames, and Boundary Observation  |
+----------------------+----------------------------------------------+

+-------+-------+-------+-------+-------+-------+-------+-------+-------+
| Bus   | Nest  | Ele   | Card  | Elem  | Data  | Value | Value | Subsi |
| iness | Level | ment/ |       | /Attr | Type  | Conf  |       | diary |
| Name  |       | ​Attr |       | Conf  |       |       |       | Tem   |
|       |       | ibute |       |       |       |       |       | plate |
+=======+=======+=======+=======+=======+=======+=======+=======+=======+
| **S   |       | o     | 1..1  | SHALL |       |       |       |       |
| OPIns |       | bserv |       |       |       |       |       |       |
| tance |       | ation |       |       |       |       |       |       |
| [*]** |       |       |       |       |       |       |       |       |
+-------+-------+-------+-------+-------+-------+-------+-------+-------+
|       | @     | @clas | 1..1  | SHALL | CS    | SHALL | DGIMG |       |
|       |       | sCode |       |       |       |       |       |       |
+-------+-------+-------+-------+-------+-------+-------+-------+-------+
|       | @     | @moo  | 1..1  | SHALL | CS    | SHALL | EVN   |       |
|       |       | dCode |       |       |       |       |       |       |
+-------+-------+-------+-------+-------+-------+-------+-------+-------+
|       | >     | t     | 1..1  | SHALL | II    |       |       |       |
|       |       | empla |       |       |       |       |       |       |
|       |       | te​Id |       |       |       |       |       |       |
+-------+-------+-------+-------+-------+-------+-------+-------+-------+
|       | >@    | @root | 1..1  | SHALL | UID   | SHALL | 1.2   |       |
|       |       |       |       |       |       |       | .840. |       |
|       |       |       |       |       |       |       | 10008 |       |
|       |       |       |       |       |       |       | .9.18 |       |
+-------+-------+-------+-------+-------+-------+-------+-------+-------+
| SOPIn | >     | id    | 1..\* | SHALL | II    |       | *SOP  |       |
| stanc |       |       |       |       |       |       | Ins   |       |
| e​UID |       |       |       |       |       |       | tance |       |
|       |       |       |       |       |       |       | UID   |       |
|       |       |       |       |       |       |       | (0    |       |
|       |       |       |       |       |       |       | 008,0 |       |
|       |       |       |       |       |       |       | 018)* |       |
+-------+-------+-------+-------+-------+-------+-------+-------+-------+
|       | >     | code  | 1..1  | SHALL | CD    |       |       |       |
+-------+-------+-------+-------+-------+-------+-------+-------+-------+
| SO    | >@    | @code | 1..1  | SHALL | ST    |       | *SOP  |       |
| PClas |       |       |       |       |       |       | Class |       |
| s​UID |       |       |       |       |       |       | UID   |       |
|       |       |       |       |       |       |       | (0    |       |
|       |       |       |       |       |       |       | 008,0 |       |
|       |       |       |       |       |       |       | 016)* |       |
+-------+-------+-------+-------+-------+-------+-------+-------+-------+
|       | >@    | @     | 1..1  | SHALL | UID   | SHALL | 1.2.  |       |
|       |       | codeS |       |       |       |       | 840.1 |       |
|       |       | ystem |       |       |       |       | 0008. |       |
|       |       |       |       |       |       |       | 2.6.1 |       |
+-------+-------+-------+-------+-------+-------+-------+-------+-------+
|       | >     | text  | 0..1  | S     | ED    |       |       |       |
|       |       |       |       | HOULD |       |       |       |       |
+-------+-------+-------+-------+-------+-------+-------+-------+-------+
|       | >@    | @medi | 1..1  | SHALL | ST    | SHALL | ap    |       |
|       |       | aType |       |       |       |       | plica |       |
|       |       |       |       |       |       |       | tion/ |       |
|       |       |       |       |       |       |       | dicom |       |
+-------+-------+-------+-------+-------+-------+-------+-------+-------+
| WAD   | >>    | refe  | 1..1  | SHALL | URL   |       |       |       |
| ORefe |       | rence |       |       |       |       |       |       |
| rence |       |       |       |       |       |       |       |       |
+-------+-------+-------+-------+-------+-------+-------+-------+-------+
|       | >     | effe  | 0..1  | S     | TS    |       | *Ins  |       |
|       |       | ctive |       | HOULD |       |       | tance |       |
|       |       | ​Time |       |       |       |       | Cre   |       |
|       |       |       |       |       |       |       | ation |       |
|       |       |       |       |       |       |       | Date  |       |
|       |       |       |       |       |       |       | (     |       |
|       |       |       |       |       |       |       | 0008, |       |
|       |       |       |       |       |       |       | 0012) |       |
|       |       |       |       |       |       |       | +     |       |
|       |       |       |       |       |       |       | Ins   |       |
|       |       |       |       |       |       |       | tance |       |
|       |       |       |       |       |       |       | Cre   |       |
|       |       |       |       |       |       |       | ation |       |
|       |       |       |       |       |       |       | Time  |       |
|       |       |       |       |       |       |       | (     |       |
|       |       |       |       |       |       |       | 0008, |       |
|       |       |       |       |       |       |       | 0013) |       |
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
+-------+-------+-------+-------+-------+-------+-------+-------+-------+
|       | >     | ent   | 0..\* | COND  |       |       |       |       |
|       |       | ry​Re |       |       |       |       |       |       |
|       |       | latio |       |       |       |       |       |       |
|       |       | nship |       |       |       |       |       |       |
+-------+-------+-------+-------+-------+-------+-------+-------+-------+
|       | >@    | @typ  | 1..1  | SHALL | CS    | SHALL | SUBJ  |       |
|       |       | eCode |       |       |       |       |       |       |
+-------+-------+-------+-------+-------+-------+-------+-------+-------+
| *     | >>    | *ob   | 1..1  | SHALL |       |       |       | `SOP  |
| SOPIn |       | serva |       |       |       |       |       | Ins   |
| stanc |       | tion* |       |       |       |       |       | tance |
| e[*]* |       |       |       |       |       |       |       | Ob    |
|       |       |       |       |       |       |       |       | serva |
|       |       |       |       |       |       |       |       | tion  |
|       |       |       |       |       |       |       |       | <#sec |
|       |       |       |       |       |       |       |       | t_10. |
|       |       |       |       |       |       |       |       | 8>`__ |
|       |       |       |       |       |       |       |       | 1.2   |
|       |       |       |       |       |       |       |       | .840. |
|       |       |       |       |       |       |       |       | 10008 |
|       |       |       |       |       |       |       |       | .9.18 |
+-------+-------+-------+-------+-------+-------+-------+-------+-------+
|       | >     | ent   | 0..1  | COND  |       |       |       |       |
|       |       | ry​Re |       |       |       |       |       |       |
|       |       | latio |       |       |       |       |       |       |
|       |       | nship |       |       |       |       |       |       |
+-------+-------+-------+-------+-------+-------+-------+-------+-------+
|       | >@    | @typ  | 1..1  | SHALL | CS    | SHALL | RSON  |       |
|       |       | eCode |       |       |       |       |       |       |
+-------+-------+-------+-------+-------+-------+-------+-------+-------+
|       | >>    | o     | 1..1  | SHALL |       |       |       |       |
|       |       | bserv |       |       |       |       |       |       |
|       |       | ation |       |       |       |       |       |       |
+-------+-------+-------+-------+-------+-------+-------+-------+-------+
|       | >>@   | @clas | 1..1  | SHALL | CS    | SHALL | OBS   |       |
|       |       | sCode |       |       |       |       |       |       |
+-------+-------+-------+-------+-------+-------+-------+-------+-------+
|       | >>@   | @moo  | 1..1  | SHALL | CS    | SHALL | EVN   |       |
|       |       | dCode |       |       |       |       |       |       |
+-------+-------+-------+-------+-------+-------+-------+-------+-------+
|       | >>>   | code  | 1..1  | SHALL | CD    | SHALL | (     |       |
|       |       |       |       |       |       |       | ASSER |       |
|       |       |       |       |       |       |       | TION, |       |
|       |       |       |       |       |       |       | Ac    |       |
|       |       |       |       |       |       |       | tCode |       |
|       |       |       |       |       |       |       | [2.1  |       |
|       |       |       |       |       |       |       | 6.840 |       |
|       |       |       |       |       |       |       | .1.11 |       |
|       |       |       |       |       |       |       | 3883. |       |
|       |       |       |       |       |       |       | 5.4], |       |
|       |       |       |       |       |       |       | "A    |       |
|       |       |       |       |       |       |       | ssert |       |
|       |       |       |       |       |       |       | ion") |       |
+-------+-------+-------+-------+-------+-------+-------+-------+-------+
| Purpo | >>>   | value | 1..1  | SHALL | CD    | SHALL | Val   |       |
| se​Of |       |       |       |       |       |       | ueSet |       |
| ​Refe |       |       |       |       |       | CWE   |       |       |
| rence |       |       |       |       |       |       |       |       |
|       |       |       |       |       |       | DY    |       |       |
|       |       |       |       |       |       | NAMIC |       |       |
+-------+-------+-------+-------+-------+-------+-------+-------+-------+
|       | >     | ent   | 0..1  | COND  |       |       |       |       |
|       |       | ry​Re |       |       |       |       |       |       |
|       |       | latio |       |       |       |       |       |       |
|       |       | nship |       |       |       |       |       |       |
+-------+-------+-------+-------+-------+-------+-------+-------+-------+
|       | >@    | @typ  | 1..1  | SHALL | CS    | SHALL | COMP  |       |
|       |       | eCode |       |       |       |       |       |       |
+-------+-------+-------+-------+-------+-------+-------+-------+-------+
|       | >>    | o     | 1..1  | SHALL |       |       |       |       |
|       |       | bserv |       |       |       |       |       |       |
|       |       | ation |       |       |       |       |       |       |
+-------+-------+-------+-------+-------+-------+-------+-------+-------+
|       | >>@   | @clas | 1..1  | SHALL | CS    | SHALL | R     |       |
|       |       | sCode |       |       |       |       | OIBND |       |
+-------+-------+-------+-------+-------+-------+-------+-------+-------+
|       | >>@   | @moo  | 1..1  | SHALL | CS    | SHALL | EVN   |       |
|       |       | dCode |       |       |       |       |       |       |
+-------+-------+-------+-------+-------+-------+-------+-------+-------+
|       | >>    | code  | 1..1  | SHALL | CD    | SHALL | (12   |       |
|       |       |       |       |       |       |       | 1190, |       |
|       |       |       |       |       |       |       | DCM,  |       |
|       |       |       |       |       |       |       | "     |       |
|       |       |       |       |       |       |       | Refer |       |
|       |       |       |       |       |       |       | enced |       |
|       |       |       |       |       |       |       | Fra   |       |
|       |       |       |       |       |       |       | mes") |       |
+-------+-------+-------+-------+-------+-------+-------+-------+-------+
|       | >>    | ent   | 1..1  | SHALL |       |       |       |       |
|       |       | ry​Re |       |       |       |       |       |       |
|       |       | latio |       |       |       |       |       |       |
|       |       | nship |       |       |       |       |       |       |
+-------+-------+-------+-------+-------+-------+-------+-------+-------+
|       | >>@   | @typ  | 1..1  | SHALL | CS    | SHALL | COMP  |       |
|       |       | eCode |       |       |       |       |       |       |
+-------+-------+-------+-------+-------+-------+-------+-------+-------+
|       | >>>   | o     | 1..1  | SHALL |       |       |       |       |
|       |       | bserv |       |       |       |       |       |       |
|       |       | ation |       |       |       |       |       |       |
+-------+-------+-------+-------+-------+-------+-------+-------+-------+
|       | >>>@  | @clas | 1..1  | SHALL | CS    | SHALL | OBS   |       |
|       |       | sCode |       |       |       |       |       |       |
+-------+-------+-------+-------+-------+-------+-------+-------+-------+
|       | >>>@  | @moo  | 1..1  | SHALL | CS    | SHALL | EVN   |       |
|       |       | dCode |       |       |       |       |       |       |
+-------+-------+-------+-------+-------+-------+-------+-------+-------+
|       | >>>   | code  | 1..1  | SHALL | CD    | SHALL | (11   |       |
|       |       |       |       |       |       |       | 3036, |       |
|       |       |       |       |       |       |       | DCM,  |       |
|       |       |       |       |       |       |       | "F    |       |
|       |       |       |       |       |       |       | rames |       |
|       |       |       |       |       |       |       | for   |       |
|       |       |       |       |       |       |       | Disp  |       |
|       |       |       |       |       |       |       | lay") |       |
+-------+-------+-------+-------+-------+-------+-------+-------+-------+
| Re    | >>>   | value | 1..1  | SHALL | LIST  |       |       |       |
| feren |       |       |       |       | <INT> |       |       |       |
| ced​F |       |       |       |       |       |       |       |       |
| rames |       |       |       |       |       |       |       |       |
+-------+-------+-------+-------+-------+-------+-------+-------+-------+

.. _sect_10.8.1:

entryRelationship
~~~~~~~~~~~~~~~~~

COND: entryRelationship SHALL NOT be present in a `SOP Instance
Observation <#sect_10.8>`__ included within a `DICOM Object
Catalog <#sect_9.8.7>`__ section, and MAY be present otherwise.

.. _sect_10.8.1.1:

entryRelationship/@typeCode=SUBJ (SOP Instance)
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

This template recursively invokes itself to allow a Presentation State
SOP Instance reference to identify the target Image SOP Instances, or
for a derived Image to reference its source Image, or similar linkages
between instances.

.. note::

   This is generally not required, as the DICOM SOP Instance itself
   identifies relationships to the relevant other SOP Instances.

.. _sect_10.8.1.2:

entryRelationship/@typeCode=RSON (Purpose of Reference)
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

A Purpose of Reference Observation describes the purpose of the DICOM
composite object reference. Appropriate codes, such as externally
defined DICOM codes, may be used to specify the semantics of the purpose
of reference. When this observation is absent, it implies that the
reason for the reference is unknown.

.. note::

   In Consolidated CDA r1.1, this was defined using a separate "Purpose
   of Reference Observation" template, which is included directly in
   this template specification.

.. _sect_10.8.1.3:

entryRelationship/@typeCode=COMP (Referenced Frames)
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

A Referenced Frames Observation contains a list of integer values for
the referenced frames of a DICOM multi-frame image SOP instance. It
identifies the frame numbers within the referenced SOP instance to which
the reference applies. The observation identifies frames using the same
convention as DICOM, with the first frame in the referenced object being
Frame 1. A Referenced Frames Observation must be used if a referenced
DICOM SOP instance is a multi-frame image and the reference does not
apply to all frames.

.. note::

   In Consolidated CDA r1.1, this was defined using separate "Referenced
   Frames Observation" and "Boundary Observation" templates, which are
   included directly in this template specification.

::

   <observation classCode="DGIMG" moodCode="EVN">
       <templateId root="1.2.840.10008.9.18"/>
       <id root="1.2.840.113619.2.62.994044785528.20060823.200608232232322.3"/>
       <code code="1.2.840.10008.5.1.4.1.1.1"
           codeSystem="1.2.840.10008.2.6.1" codeSystemName="DCMUID"
           displayName="Computed Radiography Image">
       </code>
       <text mediaType="application/dicom">
           <reference value="http://www.example.org/wado?requestType=WADO
               &amp;studyUID=1.2.840.113619.2.62.994044785528.114289542805
               &amp;seriesUID=1.2.840.113619.2.62.994044785528.20060823223142485051
               &amp;objectUID=1.2.840.113619.2.62.994044785528.20060823.200608232232322.3
               &amp;contentType=application/dicom"/>
           <!--reference to image 1 (PA) -->
       </text>
       <effectiveTime value="20060823223232"/>
       <entryRelationship typeCode="RSON">
           <observation classCode="OBS" moodCode="EVN">
               <templateId root="2.16.840.1.113883.10.20.6.2.9"/>
               <code code="ASSERTION" codeSystem="2.16.840.1.113883.5.4"/>
               <value xsi:type="CD" code="121112"
                   codeSystem="1.2.840.10008.2.16.4"
                   codeSystemName="DCM"
                   displayName="Source of Measurement"/>
           </observation>
       </entryRelationship>
   </observation>

.. _sect_10.9:

Image Quality
-------------

+----------------------+----------------------------------------------+
| **Template ID**      | 1.2.840.10008.9.15                           |
+----------------------+----------------------------------------------+
| **Name**             | Image Quality                                |
+----------------------+----------------------------------------------+
| **Effective Date**   | 2015/03/24                                   |
+----------------------+----------------------------------------------+
| **Version Label**    | DICOM-20150324                               |
+----------------------+----------------------------------------------+
| **Status**           | Active                                       |
+----------------------+----------------------------------------------+
| **Description**      | Provides a quality assessment for the image  |
|                      | set identified by the invoking section. By   |
|                      | default unless otherwise identified, applies |
|                      | to the image set interpreted by the document |
|                      | (typically a Study). If the quality rating   |
|                      | applies to only a subset of the Study (e.g., |
|                      | a Series, or a specific Image), that subset  |
|                      | shall be identified in the invoking section. |
+----------------------+----------------------------------------------+
| **Classification**   | CDA Entry Level                              |
+----------------------+----------------------------------------------+
| **Relationships**    | Included in `Imaging Procedure               |
|                      | Description <#sect_9.3>`__                   |
+----------------------+----------------------------------------------+
| **Context**          | parent node                                  |
+----------------------+----------------------------------------------+
| **Open/Closed**      | open                                         |
+----------------------+----------------------------------------------+
| **Revision History** | DICOM-20150324: Initial version Derived from |
|                      | Coded Observation                            |
+----------------------+----------------------------------------------+

+-------+-------+-------+------+-------+-------+-------+-------+-------+
| Name  | Nest  | Ele   | Card | Elem  | Data  | Value | Value | Subsi |
|       | Level | ment/ |      | /Attr | Type  | Conf  |       | diary |
|       |       | ​Attr |      | Conf  |       |       |       | Tem   |
|       |       | ibute |      |       |       |       |       | plate |
+=======+=======+=======+======+=======+=======+=======+=======+=======+
| **    |       | o     | 1..1 | SHALL |       |       |       |       |
| Image |       | bserv |      |       |       |       |       |       |
| ​Qual |       | ation |      |       |       |       |       |       |
| ity** |       |       |      |       |       |       |       |       |
+-------+-------+-------+------+-------+-------+-------+-------+-------+
|       | @     | @clas | 1..1 | SHALL | CS    | SHALL | OBS   |       |
|       |       | sCode |      |       |       |       |       |       |
+-------+-------+-------+------+-------+-------+-------+-------+-------+
|       | @     | @moo  | 1..1 | SHALL | CS    | SHALL | EVN   |       |
|       |       | dCode |      |       |       |       |       |       |
+-------+-------+-------+------+-------+-------+-------+-------+-------+
|       | >     | t     | 1..1 | SHALL | II    |       |       |       |
|       |       | empla |      |       |       |       |       |       |
|       |       | te​Id |      |       |       |       |       |       |
+-------+-------+-------+------+-------+-------+-------+-------+-------+
|       | >@    | @root | 1..1 | SHALL | UID   | SHALL | 1.2   |       |
|       |       |       |      |       |       |       | .840. |       |
|       |       |       |      |       |       |       | 10008 |       |
|       |       |       |      |       |       |       | .9.15 |       |
+-------+-------+-------+------+-------+-------+-------+-------+-------+
|       | >     | id    | 1..1 | SHALL | II    |       |       |       |
+-------+-------+-------+------+-------+-------+-------+-------+-------+
|       | >     | code  | 1..1 | SHALL | CD    |       | (11   |       |
|       |       |       |      |       |       |       | 1050, |       |
|       |       |       |      |       |       |       | DCM,  |       |
|       |       |       |      |       |       |       | "     |       |
|       |       |       |      |       |       |       | Image |       |
|       |       |       |      |       |       |       | Qu    |       |
|       |       |       |      |       |       |       | ality |       |
|       |       |       |      |       |       |       | As    |       |
|       |       |       |      |       |       |       | sessm |       |
|       |       |       |      |       |       |       | ent") |       |
+-------+-------+-------+------+-------+-------+-------+-------+-------+
|       | >     | text  | 0..1 | S     |       |       |       |       |
|       |       |       |      | HOULD |       |       |       |       |
+-------+-------+-------+------+-------+-------+-------+-------+-------+
| Ref   | >>    | refe  | 1..1 | SHALL | URL   |       | #     |       |
|       |       | rence |      |       | (XML  |       | *co   |       |
|       |       |       |      |       | I     |       | ntent |       |
|       |       |       |      |       | DREF) |       | ​Ref* |       |
+-------+-------+-------+------+-------+-------+-------+-------+-------+
|       | >     | s     | 1..1 | SHALL | CS    | SHALL | COMP  |       |
|       |       | tatus |      |       |       |       | LETED |       |
|       |       | ​Code |      |       |       |       |       |       |
+-------+-------+-------+------+-------+-------+-------+-------+-------+
| R     | >     | value | 1..1 | SHALL | CD    | S     | Val   |       |
| ating |       |       |      |       |       | HOULD | ueSet |       |
|       |       |       |      |       |       | CWE   |       |       |
+-------+-------+-------+------+-------+-------+-------+-------+-------+
|       | >@    | @xsi  | 1..1 | SHALL | ST    | SHALL | CD    |       |
|       |       | :type |      |       |       |       |       |       |
+-------+-------+-------+------+-------+-------+-------+-------+-------+

.. _sect_10.9.1:

text/reference and Related Narrative Block Markup
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

The Observation entry SHOULD include a text/reference element, whose
value attribute (not to be confused with the value element of the
Observation class) SHALL begin with a '#' and SHALL point to its
corresponding narrative in the parent section (using the approach
defined in CDA Release 2, section 4.3.5.1). See `<content> Markup and
Links From Entries <#sect_9.1.1.1>`__.

::

   <observation classCode="OBS" moodCode="EVN">
       <templateId root="1.2.840.10008.9.15"/>
       <id root="1.2.840.113619.2.62.994044785528.20060823.200608232232322.3"/>
       <code code="111050" codeSystem="1.2.840.10008.2.6.1"
           codeSystemName="DCM"
           displayName="Image Quality Assessment"/>
       <text>
           <reference value="#Q9"/>
       </text>
       <statusCode code="completed"/>
       <value xsi:type="CD" code="RID12"
           codeSystem="2.16.840.1.113883.6.256"
           codeSystemName="RADLEX"
           displayName="Diagnostic quality"/>
   </observation>

