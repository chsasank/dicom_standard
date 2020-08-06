.. _chapter_C:

Acquisition Context Module, Protocol and Workflow Context Templates (Normative)
===============================================================================

This Annex specifies the content of Templates for Acquisition, Protocol
and Workflow Context required by DICOM IODs.

.. _sect_TemplatesForAcquisitionAndProtocolContext:

.. _sect_TID_3401:

ECG Acquisition Context
~~~~~~~~~~~~~~~~~~~~~~~

**Type:**
   **Extensible**

**Order:**
   **Non-Significant**

**Root:**
   **No**

.. table:: ECG Acquisition Context

   +---+---------+-----------+-----+----------+-----------+-----------+
   |   | VT      | Concept   | VM  | Req Type | Condition | Value Set |
   |   |         | Name      |     |          |           | C         |
   |   |         |           |     |          |           | onstraint |
   +===+=========+===========+=====+==========+===========+===========+
   | 1 | CODE    | DT        | 1   | U        |           | B\ `      |
   |   |         | (         |     |          |           | Electrode |
   |   |         | 10:11345, |     |          |           | Placement |
   |   |         | MDC,      |     |          |           | Values <  |
   |   |         | "Lead     |     |          |           | #sect_CID |
   |   |         | System")  |     |          |           | _3263>`__ |
   +---+---------+-----------+-----+----------+-----------+-----------+
   | 2 | CODE    | DT        | 1   | U        |           | B\ `ECG   |
   |   |         | `(109054, |     |          |           | Patient   |
   |   |         | DCM,      |     |          |           | State     |
   |   |         | "Patient  |     |          |           | Values <  |
   |   |         | State"    |     |          |           | #sect_CID |
   |   |         | ) <#DCM_1 |     |          |           | _3262>`__ |
   |   |         | 09054>`__ |     |          |           |           |
   +---+---------+-----------+-----+----------+-----------+-----------+
   | 3 | NUMERIC | DT        | 1   | U        |           | UNITS =   |
   |   |         | `(109055, |     |          |           | EV        |
   |   |         | DCM,      |     |          |           | ({stage}, |
   |   |         | "Protocol |     |          |           | UCUM,     |
   |   |         | Stage"    |     |          |           | "stage")  |
   |   |         | ) <#DCM_1 |     |          |           |           |
   |   |         | 09055>`__ |     |          |           |           |
   +---+---------+-----------+-----+----------+-----------+-----------+
   | 4 | CODE    | DT        | 1   | U        |           | B         |
   |   |         | `(109056, |     |          |           | \ `Stress |
   |   |         | DCM,      |     |          |           | Pr        |
   |   |         | "Stress   |     |          |           | otocols < |
   |   |         | Protocol" |     |          |           | #sect_CID |
   |   |         | ) <#DCM_1 |     |          |           | _3261>`__ |
   |   |         | 09056>`__ |     |          |           |           |
   +---+---------+-----------+-----+----------+-----------+-----------+
   | 5 | NUMERIC | D\ `ECG   | 1-n | U        |           |           |
   |   |         | Control   |     |          |           |           |
   |   |         | Variables |     |          |           |           |
   |   |         | Numeric < |     |          |           |           |
   |   |         | #sect_CID |     |          |           |           |
   |   |         | _3690>`__ |     |          |           |           |
   +---+---------+-----------+-----+----------+-----------+-----------+
   | 6 | TEXT    | D\ `ECG   | 1-n | U        |           |           |
   |   |         | Control   |     |          |           |           |
   |   |         | Variables |     |          |           |           |
   |   |         | Text <    |     |          |           |           |
   |   |         | #sect_CID |     |          |           |           |
   |   |         | _3691>`__ |     |          |           |           |
   +---+---------+-----------+-----+----------+-----------+-----------+

.. _sect_TID_3403:

Catheterization Acquisition Context
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

**Type:**
   **Extensible**

**Order:**
   **Non-Significant**

**Root:**
   **No**

.. table:: Catheterization Acquisition Context

   +---+---------+-----------+----+----------+-----------+-----------+
   |   | VT      | Concept   | VM | Req Type | Condition | Value Set |
   |   |         | Name      |    |          |           | C         |
   |   |         |           |    |          |           | onstraint |
   +===+=========+===========+====+==========+===========+===========+
   | 1 | CODE    | EV        | 1  | U        |           | B         |
   |   |         | `(1       |    |          |           | \ `Cathet |
   |   |         | 29085009, |    |          |           | erization |
   |   |         | SCT,      |    |          |           | Procedure |
   |   |         | "Cathet   |    |          |           | Phase <   |
   |   |         | erization |    |          |           | #sect_CID |
   |   |         | Procedure |    |          |           | _3250>`__ |
   |   |         | Phase")   |    |          |           |           |
   |   |         | <http://s |    |          |           |           |
   |   |         | nomed.inf |    |          |           |           |
   |   |         | o/id/1290 |    |          |           |           |
   |   |         | 85009>`__ |    |          |           |           |
   +---+---------+-----------+----+----------+-----------+-----------+
   | 2 | CODE    | EV        | 1  | U        |           | B\        |
   |   |         | `(109058, |    |          |           | `Relative |
   |   |         | DCM,      |    |          |           | Times <   |
   |   |         | "Contrast |    |          |           | #sect_CID |
   |   |         | Phase"    |    |          |           | _3600>`__ |
   |   |         | ) <#DCM_1 |    |          |           |           |
   |   |         | 09058>`__ |    |          |           |           |
   +---+---------+-----------+----+----------+-----------+-----------+
   | 3 | CODE    | EV        | 1  | U        |           | B\ `He    |
   |   |         | `(109059, |    |          |           | modynamic |
   |   |         | DCM,      |    |          |           | Phys      |
   |   |         | "Phys     |    |          |           | iological |
   |   |         | iological |    |          |           | Cha       |
   |   |         | ch        |    |          |           | llenges < |
   |   |         | allenges" |    |          |           | #sect_CID |
   |   |         | ) <#DCM_1 |    |          |           | _3271>`__ |
   |   |         | 09059>`__ |    |          |           |           |
   +---+---------+-----------+----+----------+-----------+-----------+
   | 4 | NUMERIC | EV        | 1  | U        |           | UNITS =   |
   |   |         | `(109060, |    |          |           | EV        |
   |   |         | DCM,      |    |          |           | ({step},  |
   |   |         | "         |    |          |           | UCUM,     |
   |   |         | Procedure |    |          |           | "step")   |
   |   |         | Step      |    |          |           |           |
   |   |         | Number"   |    |          |           |           |
   |   |         | ) <#DCM_1 |    |          |           |           |
   |   |         | 09060>`__ |    |          |           |           |
   +---+---------+-----------+----+----------+-----------+-----------+
   | 5 | TEXT    | EV        | 1  | U        |           |           |
   |   |         | `(121124, |    |          |           |           |
   |   |         | DCM,      |    |          |           |           |
   |   |         | "         |    |          |           |           |
   |   |         | Procedure |    |          |           |           |
   |   |         | Action    |    |          |           |           |
   |   |         | ID"       |    |          |           |           |
   |   |         | ) <#DCM_1 |    |          |           |           |
   |   |         | 21124>`__ |    |          |           |           |
   +---+---------+-----------+----+----------+-----------+-----------+

.. note::

   See `Procedure Action <#sect_TID_3100>`__ in `Structured Reporting
   Templates (Normative) <#chapter_A>`__ for description of Procedure
   Action ID used in Row 5.

.. _sect_TID_3450:

Cardiac Electrophysiology Acquisition Context
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

**Type:**
   **Extensible**

**Order:**
   **Non-Significant**

**Root:**
   **No**

.. table:: Cardiac Electrophysiology Acquisition Context

   +---+------+------------+----+----------+-----------+------------+
   |   | VT   | Concept    | VM | Req Type | Condition | Value Set  |
   |   |      | Name       |    |          |           | Constraint |
   +===+======+============+====+==========+===========+============+
   | 1 | CODE | EV         | 1  | U        |           | B          |
   |   |      | `(109061,  |    |          |           | \ `Electro |
   |   |      | DCM, "EP   |    |          |           | physiology |
   |   |      | Procedure  |    |          |           | Procedure  |
   |   |      | Phas       |    |          |           | Phase      |
   |   |      | e") <#DCM_ |    |          |           |  <#sect_CI |
   |   |      | 109061>`__ |    |          |           | D_3254>`__ |
   +---+------+------------+----+----------+-----------+------------+
   | 2 | NUM  | EV         | 1  | U        |           | UNITS = EV |
   |   |      | `(109060,  |    |          |           | ({step},   |
   |   |      | DCM,       |    |          |           | UCUM,      |
   |   |      | "Procedure |    |          |           | "step")    |
   |   |      | Step       |    |          |           |            |
   |   |      | Numbe      |    |          |           |            |
   |   |      | r") <#DCM_ |    |          |           |            |
   |   |      | 109060>`__ |    |          |           |            |
   +---+------+------------+----+----------+-----------+------------+
   | 3 | TEXT | EV         | 1  | U        |           |            |
   |   |      | `(109063,  |    |          |           |            |
   |   |      | DCM,       |    |          |           |            |
   |   |      | "Pulse     |    |          |           |            |
   |   |      | train      |    |          |           |            |
   |   |      | definitio  |    |          |           |            |
   |   |      | n") <#DCM_ |    |          |           |            |
   |   |      | 109063>`__ |    |          |           |            |
   +---+------+------------+----+----------+-----------+------------+

.. _sect_TID_3460:

Projection Radiography Acquisition Context
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

**Type:**
   **Extensible**

**Order:**
   **Non-Significant**

**Root:**
   **No**

.. table:: Projection Radiography Acquisition Context

   +---+------+------------+-----+----------+-----------+------------+
   |   | VT   | Concept    | VM  | Req Type | Condition | Value Set  |
   |   |      | Name       |     |          |           | Constraint |
   +===+======+============+=====+==========+===========+============+
   | 1 | CODE | DT         | 1-n | U        |           | B\ `       |
   |   |      | `(130324,  |     |          |           | Functional |
   |   |      | DCM,       |     |          |           | Condition  |
   |   |      | "          |     |          |           | Present    |
   |   |      | Functional |     |          |           | During     |
   |   |      | condition  |     |          |           | Acquisiti  |
   |   |      | present    |     |          |           | on <#sect_ |
   |   |      | during     |     |          |           | CID_91>`__ |
   |   |      | acquisitio |     |          |           |            |
   |   |      | n") <#DCM_ |     |          |           |            |
   |   |      | 130324>`__ |     |          |           |            |
   +---+------+------------+-----+----------+-----------+------------+
   | 2 | CODE | DT         | 1   | U        |           | B\ `R      |
   |   |      | `(         |     |          |           | espiratory |
   |   |      | 364062005, |     |          |           | Status     |
   |   |      | SCT,       |     |          |           |  <#sect_CI |
   |   |      | "R         |     |          |           | D_3823>`__ |
   |   |      | espiration |     |          |           |            |
   |   |      | Observabl  |     |          |           |            |
   |   |      | e") <http: |     |          |           |            |
   |   |      | //snomed.i |     |          |           |            |
   |   |      | nfo/id/364 |     |          |           |            |
   |   |      | 062005>`__ |     |          |           |            |
   +---+------+------------+-----+----------+-----------+------------+
   | 3 | CODE | DT         | 1   | U        |           | B\ `Joint  |
   |   |      | `(         |     |          |           | Position   |
   |   |      | 276334009, |     |          |           | During     |
   |   |      | SCT,       |     |          |           | Acquisiti  |
   |   |      | "Joint     |     |          |           | on <#sect_ |
   |   |      | positio    |     |          |           | CID_92>`__ |
   |   |      | n") <http: |     |          |           |            |
   |   |      | //snomed.i |     |          |           |            |
   |   |      | nfo/id/276 |     |          |           |            |
   |   |      | 334009>`__ |     |          |           |            |
   +---+------+------------+-----+----------+-----------+------------+
   | 4 | CODE | DT         | 1   | U        |           | B\ `Joint  |
   |   |      | `(109132,  |     |          |           | P          |
   |   |      | DCM,       |     |          |           | ositioning |
   |   |      | "Joint     |     |          |           | Meth       |
   |   |      | p          |     |          |           | od <#sect_ |
   |   |      | ositioning |     |          |           | CID_93>`__ |
   |   |      | metho      |     |          |           |            |
   |   |      | d") <#DCM_ |     |          |           |            |
   |   |      | 109132>`__ |     |          |           |            |
   +---+------+------------+-----+----------+-----------+------------+
   | 5 | CODE | DT         | 1-n | U        |           | B\         |
   |   |      | `(109133,  |     |          |           |  `Physical |
   |   |      | DCM,       |     |          |           | Force      |
   |   |      | "Physical  |     |          |           | Applied    |
   |   |      | forc       |     |          |           | During     |
   |   |      | e") <#DCM_ |     |          |           | Acquisiti  |
   |   |      | 109133>`__ |     |          |           | on <#sect_ |
   |   |      |            |     |          |           | CID_94>`__ |
   +---+------+------------+-----+----------+-----------+------------+

.. _sect_TID_3470:

NM/PET Acquisition Context
~~~~~~~~~~~~~~~~~~~~~~~~~~

**Type:**
   **Extensible**

**Order:**
   **Non-Significant**

**Root:**
   **No**

.. table:: NM/PET Acquisition Context

   +---+---------+-----------+----+----------+-----------+-----------+
   |   | VT      | Concept   | VM | Req Type | Condition | Value Set |
   |   |         | Name      |    |          |           | C         |
   |   |         |           |    |          |           | onstraint |
   +===+=========+===========+====+==========+===========+===========+
   | 1 | CODE    | DT        | 1  | M        |           | D\        |
   |   |         | `(109054, |    |          |           |  `Cardiac |
   |   |         | DCM,      |    |          |           | P         |
   |   |         | "Patient  |    |          |           | rocedural |
   |   |         | State"    |    |          |           | State     |
   |   |         | ) <#DCM_1 |    |          |           | Values <  |
   |   |         | 09054>`__ |    |          |           | #sect_CID |
   |   |         |           |    |          |           | _3101>`__ |
   +---+---------+-----------+----+----------+-----------+-----------+
   | 2 | INCLUDE | B\ `PET   | 1  | U        |           |           |
   |   |         | C         |    |          |           |           |
   |   |         | ovariates |    |          |           |           |
   |   |         | Ac        |    |          |           |           |
   |   |         | quisition |    |          |           |           |
   |   |         | Context < |    |          |           |           |
   |   |         | #sect_TID |    |          |           |           |
   |   |         | _3471>`__ |    |          |           |           |
   +---+---------+-----------+----+----------+-----------+-----------+

.. _sect_TID_3471:

PET Covariates Acquisition Context
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

**Type:**
   **Extensible**

**Order:**
   **Non-Significant**

**Root:**
   **No**

.. table:: PET Covariates Acquisition Context

   +---+---------+-----------+----+----------+-----------+-----------+
   |   | VT      | Concept   | VM | Req Type | Condition | Value Set |
   |   |         | Name      |    |          |           | C         |
   |   |         |           |    |          |           | onstraint |
   +===+=========+===========+====+==========+===========+===========+
   | 1 | NUMERIC | `         | 1  | U        |           | UNITS =   |
   |   |         | (14749-6, |    |          |           | EV        |
   |   |         | LN,       |    |          |           | (mmol/l,  |
   |   |         | "Gluc     |    |          |           | UCUM,     |
   |   |         | ose") <ht |    |          |           | "mmol/l") |
   |   |         | tp://loin |    |          |           |           |
   |   |         | c.org/147 |    |          |           |           |
   |   |         | 49-6/>`__ |    |          |           |           |
   +---+---------+-----------+----+----------+-----------+-----------+
   | 2 | DATE    | `(127857, | 1  | MC       | IFF Row 1 |           |
   |   |         | DCM,      |    |          | is        |           |
   |   |         | "Glucose  |    |          | present   |           |
   |   |         | Me        |    |          | and does  |           |
   |   |         | asurement |    |          | not       |           |
   |   |         | Date"     |    |          | contain   |           |
   |   |         | ) <#DCM_1 |    |          | Ob        |           |
   |   |         | 27857>`__ |    |          | servation |           |
   |   |         |           |    |          | DateTime  |           |
   |   |         |           |    |          | (0        |           |
   |   |         |           |    |          | 040,A032) |           |
   +---+---------+-----------+----+----------+-----------+-----------+
   | 3 | TIME    | `(127858, | 1  | MC       | IFF Row 1 |           |
   |   |         | DCM,      |    |          | is        |           |
   |   |         | "Glucose  |    |          | present   |           |
   |   |         | Me        |    |          | and does  |           |
   |   |         | asurement |    |          | not       |           |
   |   |         | Time"     |    |          | contain   |           |
   |   |         | ) <#DCM_1 |    |          | Ob        |           |
   |   |         | 27858>`__ |    |          | servation |           |
   |   |         |           |    |          | DateTime  |           |
   |   |         |           |    |          | (0        |           |
   |   |         |           |    |          | 040,A032) |           |
   +---+---------+-----------+----+----------+-----------+-----------+

**Content Item Descriptions**

+-------+--------------------------+-----------------------------+
| Row 2 | Glucose Measurement Date | In an earlier edition of    |
|       |                          | the Standard, an incorrect  |
|       |                          | DCM code was used for this  |
|       |                          | concept, which was already  |
|       |                          | assigned as `(109081, DCM,  |
|       |                          | "Prospective                |
|       |                          | gating") <#DCM_109081>`__.  |
+-------+--------------------------+-----------------------------+
| Row 3 | Glucose Measurement Time | In an earlier edition of    |
|       |                          | the Standard, an incorrect  |
|       |                          | DCM code was used for this  |
|       |                          | concept, which was already  |
|       |                          | assigned as `(109082, DCM,  |
|       |                          | "Retrospective              |
|       |                          | gating") <#DCM_109082>`__.  |
+-------+--------------------------+-----------------------------+

.. _sect_TID_8001:

Specimen Preparation
~~~~~~~~~~~~~~~~~~~~

This Template describes a single specimen preparation step.

**Type:**
   **Extensible**

**Order:**
   **Significant**

**Root:**
   **No**

.. table:: Specimen Preparation

   +----+----------+-----------+----+----------+-----------+-----------+
   |    | VT       | Concept   | VM | Req Type | Condition | Value Set |
   |    |          | Name      |    |          |           | C         |
   |    |          |           |    |          |           | onstraint |
   +====+==========+===========+====+==========+===========+===========+
   | 1  | TEXT     | EV        | 1  | M        |           |           |
   |    |          | `(121041, |    |          |           |           |
   |    |          | DCM,      |    |          |           |           |
   |    |          | "Specimen |    |          |           |           |
   |    |          | Id        |    |          |           |           |
   |    |          | entifier" |    |          |           |           |
   |    |          | ) <#DCM_1 |    |          |           |           |
   |    |          | 21041>`__ |    |          |           |           |
   +----+----------+-----------+----+----------+-----------+-----------+
   | 2  | TEXT     | EV        | 1  | U        |           |           |
   |    |          | `(111724, |    |          |           |           |
   |    |          | DCM,      |    |          |           |           |
   |    |          | "Issuer   |    |          |           |           |
   |    |          | of        |    |          |           |           |
   |    |          | Specimen  |    |          |           |           |
   |    |          | Id        |    |          |           |           |
   |    |          | entifier" |    |          |           |           |
   |    |          | ) <#DCM_1 |    |          |           |           |
   |    |          | 11724>`__ |    |          |           |           |
   +----+----------+-----------+----+----------+-----------+-----------+
   | 3  | CODE     | EV        | 1  | M        |           | D\        |
   |    |          | `(111701, |    |          |           | `Specimen |
   |    |          | DCM,      |    |          |           | Pr        |
   |    |          | "P        |    |          |           | eparation |
   |    |          | rocessing |    |          |           | Pr        |
   |    |          | type"     |    |          |           | ocedure < |
   |    |          | ) <#DCM_1 |    |          |           | #sect_CID |
   |    |          | 11701>`__ |    |          |           | _8111>`__ |
   +----+----------+-----------+----+----------+-----------+-----------+
   | 4  | DATETIME | DT        | 1  | U        |           |           |
   |    |          | `(111702, |    |          |           |           |
   |    |          | DCM,      |    |          |           |           |
   |    |          | "DateTime |    |          |           |           |
   |    |          | of        |    |          |           |           |
   |    |          | pr        |    |          |           |           |
   |    |          | ocessing" |    |          |           |           |
   |    |          | ) <#DCM_1 |    |          |           |           |
   |    |          | 11702>`__ |    |          |           |           |
   +----+----------+-----------+----+----------+-----------+-----------+
   | 5  | TEXT     | DT        | 1  | U        |           |           |
   |    |          | `(111703, |    |          |           |           |
   |    |          | DCM,      |    |          |           |           |
   |    |          | "P        |    |          |           |           |
   |    |          | rocessing |    |          |           |           |
   |    |          | step      |    |          |           |           |
   |    |          | des       |    |          |           |           |
   |    |          | cription" |    |          |           |           |
   |    |          | ) <#DCM_1 |    |          |           |           |
   |    |          | 11703>`__ |    |          |           |           |
   +----+----------+-----------+----+----------+-----------+-----------+
   | 6  | CODE     | DT        | 1  | U        |           | D\        |
   |    |          | `(111703, |    |          |           | `Specimen |
   |    |          | DCM,      |    |          |           | Pr        |
   |    |          | "P        |    |          |           | eparation |
   |    |          | rocessing |    |          |           | Steps <   |
   |    |          | step      |    |          |           | #sect_CID |
   |    |          | des       |    |          |           | _8113>`__ |
   |    |          | cription" |    |          |           |           |
   |    |          | ) <#DCM_1 |    |          |           |           |
   |    |          | 11703>`__ |    |          |           |           |
   +----+----------+-----------+----+----------+-----------+-----------+
   | 7  | CODE     | DT        | 1  | MC       | IFF Row 3 | B\        |
   |    |          | `(        |    |          | P         | `Specimen |
   |    |          | 17636008, |    |          | rocessing | C         |
   |    |          | SCT,      |    |          | Type      | ollection |
   |    |          | "Specimen |    |          | value is  | Pr        |
   |    |          | Col       |    |          | `(        | ocedure < |
   |    |          | lection") |    |          | 17636008, | #sect_CID |
   |    |          |  <http:// |    |          | SCT,      | _8109>`__ |
   |    |          | snomed.in |    |          | "Specimen |           |
   |    |          | fo/id/176 |    |          | Col       |           |
   |    |          | 36008>`__ |    |          | lection") |           |
   |    |          |           |    |          |  <http:// |           |
   |    |          |           |    |          | snomed.in |           |
   |    |          |           |    |          | fo/id/176 |           |
   |    |          |           |    |          | 36008>`__ |           |
   +----+----------+-----------+----+----------+-----------+-----------+
   | 8  | INCLUDE  | D\        | 1  | MC       | IFF Row 3 |           |
   |    |          | `Specimen |    |          | P         |           |
   |    |          | S         |    |          | rocessing |           |
   |    |          | ampling < |    |          | Type      |           |
   |    |          | #sect_TID |    |          | value is  |           |
   |    |          | _8002>`__ |    |          | `(4       |           |
   |    |          |           |    |          | 33465004, |           |
   |    |          |           |    |          | SCT,      |           |
   |    |          |           |    |          | "Specimen |           |
   |    |          |           |    |          | Sa        |           |
   |    |          |           |    |          | mpling")  |           |
   |    |          |           |    |          | <http://s |           |
   |    |          |           |    |          | nomed.inf |           |
   |    |          |           |    |          | o/id/4334 |           |
   |    |          |           |    |          | 65004>`__ |           |
   +----+----------+-----------+----+----------+-----------+-----------+
   | 9  | INCLUDE  | D\        | 1  | MC       | IFF Row 3 |           |
   |    |          | `Specimen |    |          | P         |           |
   |    |          | S         |    |          | rocessing |           |
   |    |          | taining < |    |          | type      |           |
   |    |          | #sect_TID |    |          | value is  |           |
   |    |          | _8003>`__ |    |          | `(1       |           |
   |    |          |           |    |          | 27790008, |           |
   |    |          |           |    |          | SCT,      |           |
   |    |          |           |    |          | "St       |           |
   |    |          |           |    |          | aining")  |           |
   |    |          |           |    |          | <http://s |           |
   |    |          |           |    |          | nomed.inf |           |
   |    |          |           |    |          | o/id/1277 |           |
   |    |          |           |    |          | 90008>`__ |           |
   +----+----------+-----------+----+----------+-----------+-----------+
   | 10 | CODE     | DT        | 1  | U        |           | B\        |
   |    |          | `(4       |    |          |           | `Specimen |
   |    |          | 30864009, |    |          |           | Fi        |
   |    |          | SCT,      |    |          |           | xatives < |
   |    |          | "Tissue   |    |          |           | #sect_CID |
   |    |          | Fi        |    |          |           | _8114>`__ |
   |    |          | xative")  |    |          |           |           |
   |    |          | <http://s |    |          |           |           |
   |    |          | nomed.inf |    |          |           |           |
   |    |          | o/id/4308 |    |          |           |           |
   |    |          | 64009>`__ |    |          |           |           |
   +----+----------+-----------+----+----------+-----------+-----------+
   | 11 | CODE     | DT        | 1  | U        |           | B\        |
   |    |          | `(4       |    |          |           | `Specimen |
   |    |          | 30863003, |    |          |           | Embedding |
   |    |          | SCT,      |    |          |           | Media <   |
   |    |          | "         |    |          |           | #sect_CID |
   |    |          | Embedding |    |          |           | _8115>`__ |
   |    |          | medium")  |    |          |           |           |
   |    |          | <http://s |    |          |           |           |
   |    |          | nomed.inf |    |          |           |           |
   |    |          | o/id/4308 |    |          |           |           |
   |    |          | 63003>`__ |    |          |           |           |
   +----+----------+-----------+----+----------+-----------+-----------+

**Content Item Descriptions**

+-------+-------------------------------------------------------------+
| Row 1 | For sampling steps (which create a child specimen from a    |
|       | parent), the ID is that of the child specimen. For other    |
|       | preparation steps, the ID of a specimen does not change     |
|       | during the processing.                                      |
+-------+-------------------------------------------------------------+
| Row 2 | The issuer shall be formatted in accordance with the HL7v2  |
|       | Hierarchic Designator Data Type. That format is [           |
|       | *Namespace ID*]^[ *Universal ID*\ ^ *Universal ID Type*],   |
|       | where *Namespace ID*\ identifies an entity within the local |
|       | namespace or domain, *Universal ID*\ is a universal or      |
|       | unique identifier for an entity, and *Universal ID          |
|       | Type*\ specifies the standard format of the Universal ID    |
|       | (see HL7 v2 Section 2.A.33).                                |
+-------+-------------------------------------------------------------+

.. _sect_TID_8002:

Specimen Sampling
~~~~~~~~~~~~~~~~~

**Type:**
   **Extensible**

**Order:**
   **Significant**

**Root:**
   **No**

.. table:: Specimen Sampling

   +----+---------+-----------+----+----------+-----------+-----------+
   |    | VT      | Concept   | VM | Req Type | Condition | Value Set |
   |    |         | Name      |    |          |           | C         |
   |    |         |           |    |          |           | onstraint |
   +====+=========+===========+====+==========+===========+===========+
   | 1  | CODE    | DT        | 1  | M        |           | B\        |
   |    |         | `(111704, |    |          |           | `Specimen |
   |    |         | DCM,      |    |          |           | Sampling  |
   |    |         | "Sampling |    |          |           | Pr        |
   |    |         | Method"   |    |          |           | ocedure < |
   |    |         | ) <#DCM_1 |    |          |           | #sect_CID |
   |    |         | 11704>`__ |    |          |           | _8110>`__ |
   +----+---------+-----------+----+----------+-----------+-----------+
   | 2  | TEXT    | DT        | 1  | M        |           |           |
   |    |         | `(111705, |    |          |           |           |
   |    |         | DCM,      |    |          |           |           |
   |    |         | "Parent   |    |          |           |           |
   |    |         | Specimen  |    |          |           |           |
   |    |         | Id        |    |          |           |           |
   |    |         | entifier" |    |          |           |           |
   |    |         | ) <#DCM_1 |    |          |           |           |
   |    |         | 11705>`__ |    |          |           |           |
   +----+---------+-----------+----+----------+-----------+-----------+
   | 3  | TEXT    | DT        | 1  | U        |           |           |
   |    |         | `(111706, |    |          |           |           |
   |    |         | DCM,      |    |          |           |           |
   |    |         | "Issuer   |    |          |           |           |
   |    |         | of Parent |    |          |           |           |
   |    |         | Specimen  |    |          |           |           |
   |    |         | Id        |    |          |           |           |
   |    |         | entifier" |    |          |           |           |
   |    |         | ) <#DCM_1 |    |          |           |           |
   |    |         | 11706>`__ |    |          |           |           |
   +----+---------+-----------+----+----------+-----------+-----------+
   | 4  | CODE    | DT        | 1  | M        |           | B\        |
   |    |         | `(111707, |    |          |           | `Anatomic |
   |    |         | DCM,      |    |          |           | Pathology |
   |    |         | "Parent   |    |          |           | Specimen  |
   |    |         | specimen  |    |          |           | Types <   |
   |    |         | type"     |    |          |           | #sect_CID |
   |    |         | ) <#DCM_1 |    |          |           | _8103>`__ |
   |    |         | 11707>`__ |    |          |           |           |
   +----+---------+-----------+----+----------+-----------+-----------+
   | 5  | TEXT    | DT        | 1  | U        |           |           |
   |    |         | `(111708, |    |          |           |           |
   |    |         | DCM,      |    |          |           |           |
   |    |         | "Position |    |          |           |           |
   |    |         | Frame of  |    |          |           |           |
   |    |         | R         |    |          |           |           |
   |    |         | eference" |    |          |           |           |
   |    |         | ) <#DCM_1 |    |          |           |           |
   |    |         | 11708>`__ |    |          |           |           |
   +----+---------+-----------+----+----------+-----------+-----------+
   | 6  | TEXT    | DT        | 1  | U        |           |           |
   |    |         | `(111709, |    |          |           |           |
   |    |         | DCM,      |    |          |           |           |
   |    |         | "Location |    |          |           |           |
   |    |         | of        |    |          |           |           |
   |    |         | sampling  |    |          |           |           |
   |    |         | site"     |    |          |           |           |
   |    |         | ) <#DCM_1 |    |          |           |           |
   |    |         | 11709>`__ |    |          |           |           |
   +----+---------+-----------+----+----------+-----------+-----------+
   | 7  | NUMERIC | DT        | 1  | U        |           |           |
   |    |         | `(111710, |    |          |           |           |
   |    |         | DCM,      |    |          |           |           |
   |    |         | "Location |    |          |           |           |
   |    |         | of        |    |          |           |           |
   |    |         | sampling  |    |          |           |           |
   |    |         | site X    |    |          |           |           |
   |    |         | offset"   |    |          |           |           |
   |    |         | ) <#DCM_1 |    |          |           |           |
   |    |         | 11710>`__ |    |          |           |           |
   +----+---------+-----------+----+----------+-----------+-----------+
   | 8  | NUMERIC | DT        | 1  | U        |           |           |
   |    |         | `(111711, |    |          |           |           |
   |    |         | DCM,      |    |          |           |           |
   |    |         | "Location |    |          |           |           |
   |    |         | of        |    |          |           |           |
   |    |         | sampling  |    |          |           |           |
   |    |         | site Y    |    |          |           |           |
   |    |         | offset"   |    |          |           |           |
   |    |         | ) <#DCM_1 |    |          |           |           |
   |    |         | 11711>`__ |    |          |           |           |
   +----+---------+-----------+----+----------+-----------+-----------+
   | 9  | NUMERIC | DT        | 1  | U        |           |           |
   |    |         | `(111712, |    |          |           |           |
   |    |         | DCM,      |    |          |           |           |
   |    |         | "Location |    |          |           |           |
   |    |         | of        |    |          |           |           |
   |    |         | sampling  |    |          |           |           |
   |    |         | site Z    |    |          |           |           |
   |    |         | offset"   |    |          |           |           |
   |    |         | ) <#DCM_1 |    |          |           |           |
   |    |         | 11712>`__ |    |          |           |           |
   +----+---------+-----------+----+----------+-----------+-----------+
   | 10 | IMAGE   | DT        | 1  | U        |           |           |
   |    |         | `(111709, |    |          |           |           |
   |    |         | DCM,      |    |          |           |           |
   |    |         | "Location |    |          |           |           |
   |    |         | of        |    |          |           |           |
   |    |         | sampling  |    |          |           |           |
   |    |         | site"     |    |          |           |           |
   |    |         | ) <#DCM_1 |    |          |           |           |
   |    |         | 11709>`__ |    |          |           |           |
   +----+---------+-----------+----+----------+-----------+-----------+

**Content Item Descriptions**

+----------+----------------------------------------------------------+
| Row 3    | The Issuer of Specimen Identifier shall be formatted in  |
|          | accordance with the HL7 v2 Hierarchic Designator data    |
|          | type (see HL7 v2.6 Section 2.A.33), i.e., [ *Namespace   |
|          | ID*]^[ *Universal ID^Universal ID Type*]                 |
+----------+----------------------------------------------------------+
| Row 5    | Description of coordinate system and origin reference    |
|          | point on parent specimen or parent specimen container    |
|          | used for localizing the sampling site                    |
+----------+----------------------------------------------------------+
| Rows 7-9 | The X, Y and Z locations are used as needed to describe  |
|          | the sampling site; not all may be needed. E.g.,          |
|          | resection from 10 cm along the colon may be described as |
|          | only a Y dimension location.                             |
+----------+----------------------------------------------------------+
| Row 10   | Reference to image of parent specimen localizing the     |
|          | sampling site; may include referenced Presentation State |
|          | object                                                   |
+----------+----------------------------------------------------------+

.. _sect_TID_8003:

Specimen Staining
~~~~~~~~~~~~~~~~~

**Type:**
   **Extensible**

**Order:**
   **Significant**

**Root:**
   **No**

.. table:: Specimen Staining

   +---+------+------------+-----+----------+------------+------------+
   |   | VT   | Concept    | VM  | Req Type | Condition  | Value Set  |
   |   |      | Name       |     |          |            | Constraint |
   +===+======+============+=====+==========+============+============+
   | 1 | CODE | DT         | 1-n | MC       | IF Row 2   | D\         |
   |   |      | `(         |     |          | not        |  `Specimen |
   |   |      | 424361007, |     |          | present    | Stains     |
   |   |      | SCT,       |     |          |            |  <#sect_CI |
   |   |      | "Using     |     |          |            | D_8112>`__ |
   |   |      | substanc   |     |          |            |            |
   |   |      | e") <http: |     |          |            |            |
   |   |      | //snomed.i |     |          |            |            |
   |   |      | nfo/id/424 |     |          |            |            |
   |   |      | 361007>`__ |     |          |            |            |
   +---+------+------------+-----+----------+------------+------------+
   | 2 | TEXT | DT         | 1   | MC       | IF Row 1   |            |
   |   |      | `(         |     |          | not        |            |
   |   |      | 424361007, |     |          | present    |            |
   |   |      | SCT,       |     |          |            |            |
   |   |      | "Using     |     |          |            |            |
   |   |      | substanc   |     |          |            |            |
   |   |      | e") <http: |     |          |            |            |
   |   |      | //snomed.i |     |          |            |            |
   |   |      | nfo/id/424 |     |          |            |            |
   |   |      | 361007>`__ |     |          |            |            |
   +---+------+------------+-----+----------+------------+------------+

.. _sect_TID_8004:

Specimen Localization
~~~~~~~~~~~~~~~~~~~~~

**Type:**
   **Extensible**

**Order:**
   **Significant**

**Root:**
   **No**

.. table:: Specimen Localization

   +---+-----------+-----------+----+----------+-----------+-----------+
   |   | VT        | Concept   | VM | Req Type | Condition | Value Set |
   |   |           | Name      |    |          |           | C         |
   |   |           |           |    |          |           | onstraint |
   +===+===========+===========+====+==========+===========+===========+
   | 1 | TEXT      | DT        | 1  | U        |           |           |
   |   |           | `(111708, |    |          |           |           |
   |   |           | DCM,      |    |          |           |           |
   |   |           | "Position |    |          |           |           |
   |   |           | Frame of  |    |          |           |           |
   |   |           | R         |    |          |           |           |
   |   |           | eference" |    |          |           |           |
   |   |           | ) <#DCM_1 |    |          |           |           |
   |   |           | 11708>`__ |    |          |           |           |
   +---+-----------+-----------+----+----------+-----------+-----------+
   | 2 | TEXT      | DT        | 1  | U        |           |           |
   |   |           | `(111718, |    |          |           |           |
   |   |           | DCM,      |    |          |           |           |
   |   |           | "Location |    |          |           |           |
   |   |           | of        |    |          |           |           |
   |   |           | Specimen" |    |          |           |           |
   |   |           | ) <#DCM_1 |    |          |           |           |
   |   |           | 11718>`__ |    |          |           |           |
   +---+-----------+-----------+----+----------+-----------+-----------+
   | 3 | NUMERIC   | DT        | 1  | U        |           |           |
   |   |           | `(111719, |    |          |           |           |
   |   |           | DCM,      |    |          |           |           |
   |   |           | "Location |    |          |           |           |
   |   |           | of        |    |          |           |           |
   |   |           | Specimen  |    |          |           |           |
   |   |           | X         |    |          |           |           |
   |   |           | offset"   |    |          |           |           |
   |   |           | ) <#DCM_1 |    |          |           |           |
   |   |           | 11719>`__ |    |          |           |           |
   +---+-----------+-----------+----+----------+-----------+-----------+
   | 4 | NUMERIC   | DT        | 1  | U        |           |           |
   |   |           | `(111720, |    |          |           |           |
   |   |           | DCM,      |    |          |           |           |
   |   |           | "Location |    |          |           |           |
   |   |           | of        |    |          |           |           |
   |   |           | Specimen  |    |          |           |           |
   |   |           | Y         |    |          |           |           |
   |   |           | offset"   |    |          |           |           |
   |   |           | ) <#DCM_1 |    |          |           |           |
   |   |           | 11720>`__ |    |          |           |           |
   +---+-----------+-----------+----+----------+-----------+-----------+
   | 5 | NUMERIC   | DT        | 1  | U        |           |           |
   |   |           | `(111721, |    |          |           |           |
   |   |           | DCM,      |    |          |           |           |
   |   |           | "Location |    |          |           |           |
   |   |           | of        |    |          |           |           |
   |   |           | Specimen  |    |          |           |           |
   |   |           | Z         |    |          |           |           |
   |   |           | offset"   |    |          |           |           |
   |   |           | ) <#DCM_1 |    |          |           |           |
   |   |           | 11721>`__ |    |          |           |           |
   +---+-----------+-----------+----+----------+-----------+-----------+
   | 6 | IMAGE     | DT        | 1  | U        |           |           |
   |   |           | `(111718, |    |          |           |           |
   |   |           | DCM,      |    |          |           |           |
   |   |           | "Location |    |          |           |           |
   |   |           | of        |    |          |           |           |
   |   |           | Specimen" |    |          |           |           |
   |   |           | ) <#DCM_1 |    |          |           |           |
   |   |           | 11718>`__ |    |          |           |           |
   +---+-----------+-----------+----+----------+-----------+-----------+
   | 7 | COMPOSITE | DT        | 1  | U        |           | Pre       |
   |   |           | `(111718, |    |          |           | sentation |
   |   |           | DCM,      |    |          |           | State SOP |
   |   |           | "Location |    |          |           | Instance  |
   |   |           | of        |    |          |           | reference |
   |   |           | Specimen" |    |          |           |           |
   |   |           | ) <#DCM_1 |    |          |           |           |
   |   |           | 11718>`__ |    |          |           |           |
   +---+-----------+-----------+----+----------+-----------+-----------+
   | 8 | TEXT      | DT        | 1  | U        |           |           |
   |   |           | `(111723, |    |          |           |           |
   |   |           | DCM,      |    |          |           |           |
   |   |           | "Visual   |    |          |           |           |
   |   |           | Marking   |    |          |           |           |
   |   |           | of        |    |          |           |           |
   |   |           | Specimen" |    |          |           |           |
   |   |           | ) <#DCM_1 |    |          |           |           |
   |   |           | 11723>`__ |    |          |           |           |
   +---+-----------+-----------+----+----------+-----------+-----------+

**Content Item Descriptions**

+----------+----------------------------------------------------------+
| Row 1    | Description of coordinate system and origin reference    |
|          | point used for localizing the Specimen. The value        |
|          | "CURRENT IMAGE " identifies the frame of reference as    |
|          | the pixel space of the Image SOP Instance in which this  |
|          | Content Item occurs.                                     |
+----------+----------------------------------------------------------+
| Row 2    | Description of specimen location, either in absolute     |
|          | terms or relative to the Position Frame Reference of Row |
|          | 1                                                        |
+----------+----------------------------------------------------------+
| Rows 3-5 | Location of specimen (nominal center) relative to the    |
|          | Position Frame Reference of Row 1. The Content Items     |
|          | include the units of measurement (e.g., mm). If Row 1    |
|          | value is "CURRENT IMAGE ", measurement shall be from the |
|          | top left hand corner of the Pixel Data of the SOP        |
|          | Instance, using units of ({pixel}, UCUM, "Pixels").      |
+----------+----------------------------------------------------------+
| Row 6    | Reference to image of container localizing the specimen; |
|          | may include referenced Presentation State object         |
+----------+----------------------------------------------------------+
| Row 7    | Reference to Presentation State object for this SOP      |
|          | Instance, with annotations localizing the specimen       |
+----------+----------------------------------------------------------+
| Row 8    | Description of visual distinguishing identifiers, e.g.,  |
|          | ink, or a particular shape of the specimen               |
+----------+----------------------------------------------------------+

.. _sect_TID_8010:

Slide Imaging Parameters
~~~~~~~~~~~~~~~~~~~~~~~~

This Template describes protocol parameters for a Slide Imaging
Procedure Step. As an extensible Template, additional items may be
included using other concept names from standard or private coding
schemes.

**Type:**
   **Extensible**

**Order:**
   **Significant**

**Root:**
   **No**

.. table:: Slide Imaging Parameters

   +---+---------+-----------+-----+----------+-----------+-----------+
   |   | VT      | Concept   | VM  | Req Type | Condition | Value Set |
   |   |         | Name      |     |          |           | C         |
   |   |         |           |     |          |           | onstraint |
   +===+=========+===========+=====+==========+===========+===========+
   | 1 | CODE    | EV        | 1-n | U        |           | D\ `M     |
   |   |         | `(112706, |     |          |           | icroscopy |
   |   |         | DCM,      |     |          |           | Ill       |
   |   |         | "Ill      |     |          |           | umination |
   |   |         | umination |     |          |           | Method <  |
   |   |         | Method"   |     |          |           | #sect_CID |
   |   |         | ) <#DCM_1 |     |          |           | _8123>`__ |
   |   |         | 12706>`__ |     |          |           |           |
   +---+---------+-----------+-----+----------+-----------+-----------+
   | 2 | NUMERIC | EV        | 1   | UC       | XOR Row 3 | UNITS =   |
   |   |         | `(112707, |     |          |           | EV        |
   |   |         | DCM,      |     |          |           | (         |
   |   |         | "Number   |     |          |           | {planes}, |
   |   |         | of focal  |     |          |           | UCUM,     |
   |   |         | planes"   |     |          |           | "planes") |
   |   |         | ) <#DCM_1 |     |          |           |           |
   |   |         | 12707>`__ |     |          |           |           |
   +---+---------+-----------+-----+----------+-----------+-----------+
   | 3 | CODE    | EV        | 1   | UC       | XOR Row 2 | DT        |
   |   |         | `(112707, |     |          |           | `(112714, |
   |   |         | DCM,      |     |          |           | DCM,      |
   |   |         | "Number   |     |          |           | "Multiple |
   |   |         | of focal  |     |          |           | planes"   |
   |   |         | planes"   |     |          |           | ) <#DCM_1 |
   |   |         | ) <#DCM_1 |     |          |           | 12714>`__ |
   |   |         | 12707>`__ |     |          |           |           |
   +---+---------+-----------+-----+----------+-----------+-----------+
   | 4 | NUMERIC | EV        | 1-n | U        |           | UNITS =   |
   |   |         | `(112708, |     |          |           | EV (um,   |
   |   |         | DCM,      |     |          |           | UCUM,     |
   |   |         | "Focal    |     |          |           | "um")     |
   |   |         | plane Z   |     |          |           |           |
   |   |         | offset"   |     |          |           |           |
   |   |         | ) <#DCM_1 |     |          |           |           |
   |   |         | 12708>`__ |     |          |           |           |
   +---+---------+-----------+-----+----------+-----------+-----------+
   | 5 | CODE    | EV        | 1   | U        |           | D\ `Magn  |
   |   |         | `(112709, |     |          |           | ification |
   |   |         | DCM,      |     |          |           | Se        |
   |   |         | "Magn     |     |          |           | lection < |
   |   |         | ification |     |          |           | #sect_CID |
   |   |         | s         |     |          |           | _8132>`__ |
   |   |         | election" |     |          |           |           |
   |   |         | ) <#DCM_1 |     |          |           |           |
   |   |         | 12709>`__ |     |          |           |           |
   +---+---------+-----------+-----+----------+-----------+-----------+
   | 6 | NUMERIC | EV        | 1-n | U        |           | UNITS =   |
   |   |         | `(112710, |     |          |           | EV (nm,   |
   |   |         | DCM,      |     |          |           | UCUM,     |
   |   |         | "Ill      |     |          |           | "nm")     |
   |   |         | umination |     |          |           |           |
   |   |         | wa        |     |          |           |           |
   |   |         | velength" |     |          |           |           |
   |   |         | ) <#DCM_1 |     |          |           |           |
   |   |         | 12710>`__ |     |          |           |           |
   +---+---------+-----------+-----+----------+-----------+-----------+
   | 7 | CODE    | EV        | 1-n | U        |           | D\ `M     |
   |   |         | `(112711, |     |          |           | icroscopy |
   |   |         | DCM,      |     |          |           | Il        |
   |   |         | "Ill      |     |          |           | luminator |
   |   |         | umination |     |          |           | and       |
   |   |         | spectral  |     |          |           | Sensor    |
   |   |         | band"     |     |          |           | Color <   |
   |   |         | ) <#DCM_1 |     |          |           | #sect_CID |
   |   |         | 12711>`__ |     |          |           | _8122>`__ |
   +---+---------+-----------+-----+----------+-----------+-----------+
   | 8 | CODE    | EV        | 1-n | U        |           | D\ `M     |
   |   |         | `(112712, |     |          |           | icroscopy |
   |   |         | DCM,      |     |          |           | Filter <  |
   |   |         | "Optical  |     |          |           | #sect_CID |
   |   |         | filter    |     |          |           | _8124>`__ |
   |   |         | type"     |     |          |           |           |
   |   |         | ) <#DCM_1 |     |          |           |           |
   |   |         | 12712>`__ |     |          |           |           |
   +---+---------+-----------+-----+----------+-----------+-----------+
   | 9 | CODE    | EV        | 1   | U        |           | D         |
   |   |         | `(112713, |     |          |           | \ `Tissue |
   |   |         | DCM,      |     |          |           | Se        |
   |   |         | "Tissue   |     |          |           | lection < |
   |   |         | selection |     |          |           | #sect_CID |
   |   |         | method"   |     |          |           | _8133>`__ |
   |   |         | ) <#DCM_1 |     |          |           |           |
   |   |         | 12713>`__ |     |          |           |           |
   +---+---------+-----------+-----+----------+-----------+-----------+

.. _sect_TID_8200:

Radiology Reading Task Parameters
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

This Template describes parameters for a radiology reading task.

.. note::

   Specialty to Read is nested inside Modality to Read in order to
   facilitate C-FIND matching against both Modality and Specialty.

**Type:**
   **Extensible**

**Order:**
   **Non-Significant**

**Root:**
   **No**

.. table:: Radiology Reading Task Parameters

   +---+----+------+---------+-----+---------+---------+---------+
   |   | NL | VT   | Concept | VM  | Req     | Co      | Value   |
   |   |    |      | Name    |     | Type    | ndition | Set     |
   |   |    |      |         |     |         |         | Con     |
   |   |    |      |         |     |         |         | straint |
   +===+====+======+=========+=====+=========+=========+=========+
   | 1 |    | CODE | EV      | 1   | U       |         | D       |
   |   |    |      | `(      |     |         |         | \ `Acqu |
   |   |    |      | 128002, |     |         |         | isition |
   |   |    |      | DCM,    |     |         |         | Modal   |
   |   |    |      | "M      |     |         |         | ity <#s |
   |   |    |      | odality |     |         |         | ect_CID |
   |   |    |      | to      |     |         |         | _29>`__ |
   |   |    |      | Re      |     |         |         |         |
   |   |    |      | ad") <# |     |         |         |         |
   |   |    |      | DCM_128 |     |         |         |         |
   |   |    |      | 002>`__ |     |         |         |         |
   +---+----+------+---------+-----+---------+---------+---------+
   | 2 | >  | CODE | EV      | 1   | U       |         | D\      |
   |   |    |      | `(      |     |         |         | `Reader |
   |   |    |      | 128003, |     |         |         | S       |
   |   |    |      | DCM,    |     |         |         | pecialt |
   |   |    |      | "Reader |     |         |         | y <#sec |
   |   |    |      | Special |     |         |         | t_CID_7 |
   |   |    |      | ty") <# |     |         |         | 449>`__ |
   |   |    |      | DCM_128 |     |         |         |         |
   |   |    |      | 003>`__ |     |         |         |         |
   +---+----+------+---------+-----+---------+---------+---------+
   | 3 |    | CODE | EV      | 1-n | U       |         | D\ `Re  |
   |   |    |      | `(      |     |         |         | quested |
   |   |    |      | 128004, |     |         |         | Report  |
   |   |    |      | DCM,    |     |         |         | Type    |
   |   |    |      | "M      |     |         |         | s <#sec |
   |   |    |      | odality |     |         |         | t_CID_9 |
   |   |    |      | to      |     |         |         | 233>`__ |
   |   |    |      | Re      |     |         |         |         |
   |   |    |      | ad") <# |     |         |         |         |
   |   |    |      | DCM_128 |     |         |         |         |
   |   |    |      | 004>`__ |     |         |         |         |
   +---+----+------+---------+-----+---------+---------+---------+

.. _sect_TID_15100:

Contrast Agent/Pre-Medication Protocol Context
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

This Template specifies medications to be administered prior to a
diagnostic imaging protocol, imaging contrast agents to be used in the
protocol, and/or bolus agents to be used in the protocol. Each
medication or agent may be modified by a specified route of
administration. The top level Content Items of this Template may appear
in any order in the Protocol Context Sequence, hence the order in this
Template is not significant. There may be significance in the order in
which the Content Items are included in the Protocol Context Sequence,
e.g., the requested order in which pre-medications are to be
administered.

**Type:**
   **Extensible**

**Order:**
   **Non-Significant**

**Root:**
   **No**

.. table:: Contrast Agent/Pre-Medication Protocol Context

   +---+----+------+---------+-----+---------+---------+---------+
   |   | NL | VT   | Concept | VM  | Req     | Co      | Value   |
   |   |    |      | Name    |     | Type    | ndition | Set     |
   |   |    |      |         |     |         |         | Con     |
   |   |    |      |         |     |         |         | straint |
   +===+====+======+=========+=====+=========+=========+=========+
   | 1 |    | CODE | EV      | 1-n | U       |         | B\      |
   |   |    |      | `(      |     |         |         |  `Radio |
   |   |    |      | 123011, |     |         |         | graphic |
   |   |    |      | DCM,    |     |         |         | C       |
   |   |    |      | "       |     |         |         | ontrast |
   |   |    |      | Contras |     |         |         | Ag      |
   |   |    |      | t/Bolus |     |         |         | ent <#s |
   |   |    |      | Age     |     |         |         | ect_CID |
   |   |    |      | nt") <# |     |         |         | _12>`__ |
   |   |    |      | DCM_123 |     |         |         |         |
   |   |    |      | 011>`__ |     |         |         |         |
   +---+----+------+---------+-----+---------+---------+---------+
   | 2 | >  | CODE | EV      | 1   | U       |         | B\      |
   |   |    |      | `(410   |     |         |         |  `Route |
   |   |    |      | 675002, |     |         |         | of      |
   |   |    |      | SCT,    |     |         |         | Admi    |
   |   |    |      | "Route  |     |         |         | nistrat |
   |   |    |      | of      |     |         |         | ion <#s |
   |   |    |      | Admi    |     |         |         | ect_CID |
   |   |    |      | nistrat |     |         |         | _11>`__ |
   |   |    |      | ion") < |     |         |         |         |
   |   |    |      | http:// |     |         |         |         |
   |   |    |      | snomed. |     |         |         |         |
   |   |    |      | info/id |     |         |         |         |
   |   |    |      | /410675 |     |         |         |         |
   |   |    |      | 002>`__ |     |         |         |         |
   +---+----+------+---------+-----+---------+---------+---------+
   | 3 |    | CODE | EV      | 1-n | U       |         |         |
   |   |    |      | `(      |     |         |         |         |
   |   |    |      | 123012, |     |         |         |         |
   |   |    |      | DCM,    |     |         |         |         |
   |   |    |      | "Pre-M  |     |         |         |         |
   |   |    |      | edicati |     |         |         |         |
   |   |    |      | on") <# |     |         |         |         |
   |   |    |      | DCM_123 |     |         |         |         |
   |   |    |      | 012>`__ |     |         |         |         |
   +---+----+------+---------+-----+---------+---------+---------+
   | 4 | >  | CODE | EV      | 1   | U       |         | B\      |
   |   |    |      | `(410   |     |         |         |  `Route |
   |   |    |      | 675002, |     |         |         | of      |
   |   |    |      | SCT,    |     |         |         | Admi    |
   |   |    |      | "Route  |     |         |         | nistrat |
   |   |    |      | of      |     |         |         | ion <#s |
   |   |    |      | Admi    |     |         |         | ect_CID |
   |   |    |      | nistrat |     |         |         | _11>`__ |
   |   |    |      | ion") < |     |         |         |         |
   |   |    |      | http:// |     |         |         |         |
   |   |    |      | snomed. |     |         |         |         |
   |   |    |      | info/id |     |         |         |         |
   |   |    |      | /410675 |     |         |         |         |
   |   |    |      | 002>`__ |     |         |         |         |
   +---+----+------+---------+-----+---------+---------+---------+

.. _sect_TID_15101:

NM/PET Protocol Context
~~~~~~~~~~~~~~~~~~~~~~~

**Type:**
   **Extensible**

**Order:**
   **Significant**

**Root:**
   **No**

.. table:: NM/PET Protocol Context

   +----+----+--------+--------+----+--------+--------+--------+
   |    | NL | VT     | C      | VM | Req    | Con    | Value  |
   |    |    |        | oncept |    | Type   | dition | Set    |
   |    |    |        | Name   |    |        |        | Cons   |
   |    |    |        |        |    |        |        | traint |
   +====+====+========+========+====+========+========+========+
   | 1  |    | CODE   | EV     | 1  | M      |        | B\ `Ra |
   |    |    |        | `(3493 |    |        |        | diopha |
   |    |    |        | 58000, |    |        |        | rmaceu |
   |    |    |        | SCT,   |    |        |        | ticals |
   |    |    |        | "R     |    |        |        |  <#sec |
   |    |    |        | adioph |    |        |        | t_CID_ |
   |    |    |        | armace |    |        |        | 25>`__ |
   |    |    |        | utical |    |        |        |        |
   |    |    |        | ag     |    |        |        | B      |
   |    |    |        | ent")  |    |        |        | \ `PET |
   |    |    |        | <http: |    |        |        | Rad    |
   |    |    |        | //snom |    |        |        | iophar |
   |    |    |        | ed.inf |    |        |        | maceut |
   |    |    |        | o/id/3 |    |        |        | ical < |
   |    |    |        | 493580 |    |        |        | #sect_ |
   |    |    |        | 00>`__ |    |        |        | CID_40 |
   |    |    |        |        |    |        |        | 21>`__ |
   +----+----+--------+--------+----+--------+--------+--------+
   | 2  | >  | CODE   | EV     | 1  | U      |        | B\ `Is |
   |    |    |        | (894   |    |        |        | otopes |
   |    |    |        | 57008, |    |        |        | in     |
   |    |    |        | SCT,   |    |        |        | Ra     |
   |    |    |        | "R     |    |        |        | diopha |
   |    |    |        | adionu |    |        |        | rmaceu |
   |    |    |        | clide) |    |        |        | ticals |
   |    |    |        |        |    |        |        |  <#sec |
   |    |    |        |        |    |        |        | t_CID_ |
   |    |    |        |        |    |        |        | 18>`__ |
   |    |    |        |        |    |        |        |        |
   |    |    |        |        |    |        |        | B      |
   |    |    |        |        |    |        |        | \ `PET |
   |    |    |        |        |    |        |        | Ra     |
   |    |    |        |        |    |        |        | dionuc |
   |    |    |        |        |    |        |        | lide < |
   |    |    |        |        |    |        |        | #sect_ |
   |    |    |        |        |    |        |        | CID_40 |
   |    |    |        |        |    |        |        | 20>`__ |
   +----+----+--------+--------+----+--------+--------+--------+
   | 3  | >  | UIDREF | EV     | 1  | U      |        |        |
   |    |    |        | `(1    |    |        |        |        |
   |    |    |        | 13503, |    |        |        |        |
   |    |    |        | DCM,   |    |        |        |        |
   |    |    |        | "R     |    |        |        |        |
   |    |    |        | adioph |    |        |        |        |
   |    |    |        | armace |    |        |        |        |
   |    |    |        | utical |    |        |        |        |
   |    |    |        | Ad     |    |        |        |        |
   |    |    |        | minist |    |        |        |        |
   |    |    |        | ration |    |        |        |        |
   |    |    |        | Event  |    |        |        |        |
   |    |    |        | UID"   |    |        |        |        |
   |    |    |        | ) <#DC |    |        |        |        |
   |    |    |        | M_1135 |    |        |        |        |
   |    |    |        | 03>`__ |    |        |        |        |
   +----+----+--------+--------+----+--------+--------+--------+
   | 4  | >  | DA     | EV     | 1  | U      |        |        |
   |    |    | TETIME | `(1    |    |        |        |        |
   |    |    |        | 23003, |    |        |        |        |
   |    |    |        | DCM,   |    |        |        |        |
   |    |    |        | "R     |    |        |        |        |
   |    |    |        | adioph |    |        |        |        |
   |    |    |        | armace |    |        |        |        |
   |    |    |        | utical |    |        |        |        |
   |    |    |        | Start  |    |        |        |        |
   |    |    |        | Dat    |    |        |        |        |
   |    |    |        | eTime" |    |        |        |        |
   |    |    |        | ) <#DC |    |        |        |        |
   |    |    |        | M_1230 |    |        |        |        |
   |    |    |        | 03>`__ |    |        |        |        |
   +----+----+--------+--------+----+--------+--------+--------+
   | 5  | >  | DA     | EV     | 1  | U      |        |        |
   |    |    | TETIME | `(1    |    |        |        |        |
   |    |    |        | 23004, |    |        |        |        |
   |    |    |        | DCM,   |    |        |        |        |
   |    |    |        | "R     |    |        |        |        |
   |    |    |        | adioph |    |        |        |        |
   |    |    |        | armace |    |        |        |        |
   |    |    |        | utical |    |        |        |        |
   |    |    |        | Stop   |    |        |        |        |
   |    |    |        | Dat    |    |        |        |        |
   |    |    |        | eTime" |    |        |        |        |
   |    |    |        | ) <#DC |    |        |        |        |
   |    |    |        | M_1230 |    |        |        |        |
   |    |    |        | 04>`__ |    |        |        |        |
   +----+----+--------+--------+----+--------+--------+--------+
   | 6  | >  | N      | EV     | 1  | U      |        | UNITS  |
   |    |    | UMERIC | `(1    |    |        |        | = DT   |
   |    |    |        | 23005, |    |        |        | (cm3,  |
   |    |    |        | DCM,   |    |        |        | UCUM,  |
   |    |    |        | "R     |    |        |        | "cm3") |
   |    |    |        | adioph |    |        |        |        |
   |    |    |        | armace |    |        |        |        |
   |    |    |        | utical |    |        |        |        |
   |    |    |        | V      |    |        |        |        |
   |    |    |        | olume" |    |        |        |        |
   |    |    |        | ) <#DC |    |        |        |        |
   |    |    |        | M_1230 |    |        |        |        |
   |    |    |        | 05>`__ |    |        |        |        |
   +----+----+--------+--------+----+--------+--------+--------+
   | 7  | >  | N      | EV     | 1  | U      |        | UNITS  |
   |    |    | UMERIC | `(1    |    |        |        | = DT   |
   |    |    |        | 23006, |    |        |        | (Bq,   |
   |    |    |        | DCM,   |    |        |        | UCUM,  |
   |    |    |        | "      |    |        |        | "Bq")  |
   |    |    |        | Radion |    |        |        |        |
   |    |    |        | uclide |    |        |        |        |
   |    |    |        | Total  |    |        |        |        |
   |    |    |        | Dose"  |    |        |        |        |
   |    |    |        | ) <#DC |    |        |        |        |
   |    |    |        | M_1230 |    |        |        |        |
   |    |    |        | 06>`__ |    |        |        |        |
   +----+----+--------+--------+----+--------+--------+--------+
   | 8  | >  | N      | EV     | 1  | U      |        | UNITS  |
   |    |    | UMERIC | `(1    |    |        |        | = DT   |
   |    |    |        | 23007, |    |        |        | (B     |
   |    |    |        | DCM,   |    |        |        | q/mol, |
   |    |    |        | "R     |    |        |        | UCUM,  |
   |    |    |        | adioph |    |        |        | "Bq    |
   |    |    |        | armace |    |        |        | /mol") |
   |    |    |        | utical |    |        |        |        |
   |    |    |        | Sp     |    |        |        |        |
   |    |    |        | ecific |    |        |        |        |
   |    |    |        | Act    |    |        |        |        |
   |    |    |        | ivity" |    |        |        |        |
   |    |    |        | ) <#DC |    |        |        |        |
   |    |    |        | M_1230 |    |        |        |        |
   |    |    |        | 07>`__ |    |        |        |        |
   +----+----+--------+--------+----+--------+--------+--------+
   | 9  | >  | CODE   | EV     | 1  | U      |        | B\     |
   |    |    |        | `(4106 |    |        |        | `Route |
   |    |    |        | 75002, |    |        |        | of     |
   |    |    |        | SCT,   |    |        |        | Ad     |
   |    |    |        | "Route |    |        |        | minist |
   |    |    |        | of     |    |        |        | ration |
   |    |    |        | Admin  |    |        |        |  <#sec |
   |    |    |        | istrat |    |        |        | t_CID_ |
   |    |    |        | ion")  |    |        |        | 11>`__ |
   |    |    |        | <http: |    |        |        |        |
   |    |    |        | //snom |    |        |        |        |
   |    |    |        | ed.inf |    |        |        |        |
   |    |    |        | o/id/4 |    |        |        |        |
   |    |    |        | 106750 |    |        |        |        |
   |    |    |        | 02>`__ |    |        |        |        |
   +----+----+--------+--------+----+--------+--------+--------+
   | 10 | >  | N      | EV     | 1  | U      |        | UNITS  |
   |    |    | UMERIC | `(1    |    |        |        | = DT   |
   |    |    |        | 23009, |    |        |        | ({coun |
   |    |    |        | DCM,   |    |        |        | ts}/s, |
   |    |    |        | "      |    |        |        | UCUM   |
   |    |    |        | Radion |    |        |        | "coun  |
   |    |    |        | uclide |    |        |        | ts/s") |
   |    |    |        | S      |    |        |        |        |
   |    |    |        | yringe |    |        |        |        |
   |    |    |        | C      |    |        |        |        |
   |    |    |        | ounts" |    |        |        |        |
   |    |    |        | ) <#DC |    |        |        |        |
   |    |    |        | M_1230 |    |        |        |        |
   |    |    |        | 09>`__ |    |        |        |        |
   +----+----+--------+--------+----+--------+--------+--------+
   | 11 | >  | N      | EV     | 1  | U      |        | UNITS  |
   |    |    | UMERIC | `(1    |    |        |        | = DT   |
   |    |    |        | 23010, |    |        |        | ({coun |
   |    |    |        | DCM,   |    |        |        | ts}/s, |
   |    |    |        | "      |    |        |        | UCUM   |
   |    |    |        | Radion |    |        |        | "coun  |
   |    |    |        | uclide |    |        |        | ts/s") |
   |    |    |        | Re     |    |        |        |        |
   |    |    |        | sidual |    |        |        |        |
   |    |    |        | S      |    |        |        |        |
   |    |    |        | yringe |    |        |        |        |
   |    |    |        | C      |    |        |        |        |
   |    |    |        | ounts" |    |        |        |        |
   |    |    |        | ) <#DC |    |        |        |        |
   |    |    |        | M_1230 |    |        |        |        |
   |    |    |        | 10>`__ |    |        |        |        |
   +----+----+--------+--------+----+--------+--------+--------+
   | 12 |    | N      | EV     | 1  | U      |        | UNITS  |
   |    |    | UMERIC | `(14   |    |        |        | = EV   |
   |    |    |        | 749-6, |    |        |        | (m     |
   |    |    |        | LN,    |    |        |        | mol/l, |
   |    |    |        | "Gluc  |    |        |        | UCUM,  |
   |    |    |        | ose")  |    |        |        | "mm    |
   |    |    |        | <http: |    |        |        | ol/l") |
   |    |    |        | //loin |    |        |        |        |
   |    |    |        | c.org/ |    |        |        |        |
   |    |    |        | 14749- |    |        |        |        |
   |    |    |        | 6/>`__ |    |        |        |        |
   +----+----+--------+--------+----+--------+--------+--------+
   | 13 | >  | DATE   | EV     | 1  | MC     | IFF    |        |
   |    |    |        | `(1    |    |        | Row 12 |        |
   |    |    |        | 27857, |    |        | is     |        |
   |    |    |        | DCM,   |    |        | p      |        |
   |    |    |        | "G     |    |        | resent |        |
   |    |    |        | lucose |    |        | and    |        |
   |    |    |        | Measu  |    |        | does   |        |
   |    |    |        | rement |    |        | not    |        |
   |    |    |        | Date"  |    |        | c      |        |
   |    |    |        | ) <#DC |    |        | ontain |        |
   |    |    |        | M_1278 |    |        | Obser  |        |
   |    |    |        | 57>`__ |    |        | vation |        |
   |    |    |        |        |    |        | Da     |        |
   |    |    |        |        |    |        | teTime |        |
   |    |    |        |        |    |        | (0040  |        |
   |    |    |        |        |    |        | ,A032) |        |
   +----+----+--------+--------+----+--------+--------+--------+
   | 14 | >  | TIME   | EV     | 1  | MC     | IFF    |        |
   |    |    |        | `(1    |    |        | Row 12 |        |
   |    |    |        | 27858, |    |        | is     |        |
   |    |    |        | DCM,   |    |        | p      |        |
   |    |    |        | "G     |    |        | resent |        |
   |    |    |        | lucose |    |        | and    |        |
   |    |    |        | Measu  |    |        | does   |        |
   |    |    |        | rement |    |        | not    |        |
   |    |    |        | Time"  |    |        | c      |        |
   |    |    |        | ) <#DC |    |        | ontain |        |
   |    |    |        | M_1278 |    |        | Obser  |        |
   |    |    |        | 58>`__ |    |        | vation |        |
   |    |    |        |        |    |        | Da     |        |
   |    |    |        |        |    |        | teTime |        |
   |    |    |        |        |    |        | (0040  |        |
   |    |    |        |        |    |        | ,A032) |        |
   +----+----+--------+--------+----+--------+--------+--------+

**Content Item Descriptions**

+--------+--------------------------+-----------------------------+
| Row 13 | Glucose Measurement Date | In an earlier edition of    |
|        |                          | the Standard, an incorrect  |
|        |                          | DCM code was used for this  |
|        |                          | concept, which was already  |
|        |                          | assigned as `(109081, DCM,  |
|        |                          | "Prospective                |
|        |                          | gating") <#DCM_109081>`__.  |
+--------+--------------------------+-----------------------------+
| Row 14 | Glucose Measurement Time | In an earlier edition of    |
|        |                          | the Standard, an incorrect  |
|        |                          | DCM code was used for this  |
|        |                          | concept, which was already  |
|        |                          | assigned as `(109082, DCM,  |
|        |                          | "Retrospective              |
|        |                          | gating") <#DCM_109082>`__.  |
+--------+--------------------------+-----------------------------+

.. _sect_TID_15200:

JJ1017 Protocol Context
~~~~~~~~~~~~~~~~~~~~~~~

This Template defines protocol context concepts to support the
requirements of Japanese Guideline JJ1017. This is expected to be used
with Scheduled or Performed Protocol Codes from Coding Scheme JJ1017-16M
defined in Guideline JJ1017.

**Type:**
   **Extensible**

**Order:**
   **Significant**

**Root:**
   **No**

.. table:: JJ1017 Protocol Context

   +---+----+------+---------+----+---------+---------+---------+
   |   | NL | VT   | Concept | VM | Req     | Co      | Value   |
   |   |    |      | Name    |    | Type    | ndition | Set     |
   |   |    |      |         |    |         |         | Con     |
   |   |    |      |         |    |         |         | straint |
   +===+====+======+=========+====+=========+=========+=========+
   | 1 |    | CODE | EV      | 1  | M       |         | B       |
   |   |    |      | `(      |    |         |         | aseline |
   |   |    |      | 123016, |    |         |         | terms   |
   |   |    |      | DCM,    |    |         |         | from    |
   |   |    |      | "       |    |         |         | Coding  |
   |   |    |      | Imaging |    |         |         | Scheme  |
   |   |    |      | C       |    |         |         | JJ1     |
   |   |    |      | onditio |    |         |         | 017-16S |
   |   |    |      | ns") <# |    |         |         | of      |
   |   |    |      | DCM_123 |    |         |         | JJ1017  |
   |   |    |      | 016>`__ |    |         |         | version |
   |   |    |      |         |    |         |         | 3.0     |
   +---+----+------+---------+----+---------+---------+---------+

.. _sect_TID_15300:

RT Prescription Annotation
~~~~~~~~~~~~~~~~~~~~~~~~~~

The concepts in this TID are topics of advice or information provided by
the prescribing physician for planning, preparation and delivery of
treatment for a prescription.

**Type:**
   **Extensible**

**Order:**
   **Non-Significant**

**Root:**
   **No**

.. table:: RT Prescription Annotation

   +----+--------+--------+--------+----+--------+--------+--------+
   |    | NL     | VT     | C      | VM | Req    | Con    | Value  |
   |    |        |        | oncept |    | Type   | dition | Set    |
   |    |        |        | Name   |    |        |        | Cons   |
   |    |        |        |        |    |        |        | traint |
   +====+========+========+========+====+========+========+========+
   | 1  | TEXT   | EV     | 1      | U  |        |        |        |
   |    |        | `(1    |        |    |        |        |        |
   |    |        | 30022, |        |    |        |        |        |
   |    |        | DCM,   |        |    |        |        |        |
   |    |        | "Rad   |        |    |        |        |        |
   |    |        | iation |        |    |        |        |        |
   |    |        | Cha    |        |    |        |        |        |
   |    |        | racter |        |    |        |        |        |
   |    |        | istics |        |    |        |        |        |
   |    |        | Note"  |        |    |        |        |        |
   |    |        | ) <#DC |        |    |        |        |        |
   |    |        | M_1300 |        |    |        |        |        |
   |    |        | 22>`__ |        |    |        |        |        |
   +----+--------+--------+--------+----+--------+--------+--------+
   | 2  | TEXT   | EV     | 1      | U  |        |        |        |
   |    |        | `(1    |        |    |        |        |        |
   |    |        | 30023, |        |    |        |        |        |
   |    |        | DCM,   |        |    |        |        |        |
   |    |        | "Beam  |        |    |        |        |        |
   |    |        | S      |        |    |        |        |        |
   |    |        | haping |        |    |        |        |        |
   |    |        | Note"  |        |    |        |        |        |
   |    |        | ) <#DC |        |    |        |        |        |
   |    |        | M_1300 |        |    |        |        |        |
   |    |        | 23>`__ |        |    |        |        |        |
   +----+--------+--------+--------+----+--------+--------+--------+
   | 3  | TEXT   | EV     | 1      | U  |        |        |        |
   |    |        | `(1    |        |    |        |        |        |
   |    |        | 30024, |        |    |        |        |        |
   |    |        | DCM,   |        |    |        |        |        |
   |    |        | "Tre   |        |    |        |        |        |
   |    |        | atment |        |    |        |        |        |
   |    |        | Pl     |        |    |        |        |        |
   |    |        | anning |        |    |        |        |        |
   |    |        | Note"  |        |    |        |        |        |
   |    |        | ) <#DC |        |    |        |        |        |
   |    |        | M_1300 |        |    |        |        |        |
   |    |        | 24>`__ |        |    |        |        |        |
   +----+--------+--------+--------+----+--------+--------+--------+
   | 4  | TEXT   | EV     | 1      | U  |        |        |        |
   |    |        | `(1    |        |    |        |        |        |
   |    |        | 30025, |        |    |        |        |        |
   |    |        | DCM,   |        |    |        |        |        |
   |    |        | "S     |        |    |        |        |        |
   |    |        | pecial |        |    |        |        |        |
   |    |        | Pro    |        |    |        |        |        |
   |    |        | cedure |        |    |        |        |        |
   |    |        | Note"  |        |    |        |        |        |
   |    |        | ) <#DC |        |    |        |        |        |
   |    |        | M_1300 |        |    |        |        |        |
   |    |        | 25>`__ |        |    |        |        |        |
   +----+--------+--------+--------+----+--------+--------+--------+
   | 5  | TEXT   | EV     | 1      | U  |        |        |        |
   |    |        | `(1    |        |    |        |        |        |
   |    |        | 30026, |        |    |        |        |        |
   |    |        | DCM,   |        |    |        |        |        |
   |    |        | "P     |        |    |        |        |        |
   |    |        | atient |        |    |        |        |        |
   |    |        | Posit  |        |    |        |        |        |
   |    |        | ioning |        |    |        |        |        |
   |    |        | Note"  |        |    |        |        |        |
   |    |        | ) <#DC |        |    |        |        |        |
   |    |        | M_1300 |        |    |        |        |        |
   |    |        | 26>`__ |        |    |        |        |        |
   +----+--------+--------+--------+----+--------+--------+--------+
   | 6  | TEXT   | EV     | 1      | U  |        |        |        |
   |    |        | `(1    |        |    |        |        |        |
   |    |        | 30028, |        |    |        |        |        |
   |    |        | DCM,   |        |    |        |        |        |
   |    |        | "P     |        |    |        |        |        |
   |    |        | atient |        |    |        |        |        |
   |    |        | Setup  |        |    |        |        |        |
   |    |        | Note"  |        |    |        |        |        |
   |    |        | ) <#DC |        |    |        |        |        |
   |    |        | M_1300 |        |    |        |        |        |
   |    |        | 28>`__ |        |    |        |        |        |
   +----+--------+--------+--------+----+--------+--------+--------+
   | 7  | TEXT   | EV     | 1      | U  |        |        |        |
   |    |        | `(1    |        |    |        |        |        |
   |    |        | 30029, |        |    |        |        |        |
   |    |        | DCM,   |        |    |        |        |        |
   |    |        | "Pr    |        |    |        |        |        |
   |    |        | evious |        |    |        |        |        |
   |    |        | Tre    |        |    |        |        |        |
   |    |        | atment |        |    |        |        |        |
   |    |        | Note"  |        |    |        |        |        |
   |    |        | ) <#DC |        |    |        |        |        |
   |    |        | M_1300 |        |    |        |        |        |
   |    |        | 29>`__ |        |    |        |        |        |
   +----+--------+--------+--------+----+--------+--------+--------+
   | 8  | TEXT   | EV     | 1      | U  |        |        |        |
   |    |        | `(1    |        |    |        |        |        |
   |    |        | 30030, |        |    |        |        |        |
   |    |        | DCM,   |        |    |        |        |        |
   |    |        | "Pl    |        |    |        |        |        |
   |    |        | anning |        |    |        |        |        |
   |    |        | I      |        |    |        |        |        |
   |    |        | maging |        |    |        |        |        |
   |    |        | Note"  |        |    |        |        |        |
   |    |        | ) <#DC |        |    |        |        |        |
   |    |        | M_1300 |        |    |        |        |        |
   |    |        | 30>`__ |        |    |        |        |        |
   +----+--------+--------+--------+----+--------+--------+--------+
   | 9  | TEXT   | EV     | 1      | U  |        |        |        |
   |    |        | `(1    |        |    |        |        |        |
   |    |        | 30031, |        |    |        |        |        |
   |    |        | DCM,   |        |    |        |        |        |
   |    |        | "De    |        |    |        |        |        |
   |    |        | livery |        |    |        |        |        |
   |    |        | Verifi |        |    |        |        |        |
   |    |        | cation |        |    |        |        |        |
   |    |        | Note"  |        |    |        |        |        |
   |    |        | ) <#DC |        |    |        |        |        |
   |    |        | M_1300 |        |    |        |        |        |
   |    |        | 31>`__ |        |    |        |        |        |
   +----+--------+--------+--------+----+--------+--------+--------+
   | 10 | TEXT   | EV     | 1      | U  |        |        |        |
   |    |        | `(1    |        |    |        |        |        |
   |    |        | 30032, |        |    |        |        |        |
   |    |        | DCM,   |        |    |        |        |        |
   |    |        | "Simu  |        |    |        |        |        |
   |    |        | lation |        |    |        |        |        |
   |    |        | Note"  |        |    |        |        |        |
   |    |        | ) <#DC |        |    |        |        |        |
   |    |        | M_1300 |        |    |        |        |        |
   |    |        | 32>`__ |        |    |        |        |        |
   +----+--------+--------+--------+----+--------+--------+--------+
   | 11 | CODE   | DT     | 1-n    | U  |        |        | B      |
   |    |        | `(1    |        |    |        |        | \ `Rad |
   |    |        | 30033, |        |    |        |        | iation |
   |    |        | DCM,   |        |    |        |        | T      |
   |    |        | "Rad   |        |    |        |        | herapy |
   |    |        | iation |        |    |        |        | Part   |
   |    |        | T      |        |    |        |        | icle < |
   |    |        | herapy |        |    |        |        | #sect_ |
   |    |        | Par    |        |    |        |        | CID_95 |
   |    |        | ticle" |        |    |        |        | 25>`__ |
   |    |        | ) <#DC |        |    |        |        |        |
   |    |        | M_1300 |        |    |        |        |        |
   |    |        | 33>`__ |        |    |        |        |        |
   +----+--------+--------+--------+----+--------+--------+--------+
   | 12 | CODE   | DT     | 1-n    | U  |        |        | B      |
   |    |        | `(1    |        |    |        |        | \ `Ion |
   |    |        | 30037, |        |    |        |        | T      |
   |    |        | DCM,   |        |    |        |        | herapy |
   |    |        | "Ion   |        |    |        |        | Part   |
   |    |        | T      |        |    |        |        | icle < |
   |    |        | herapy |        |    |        |        | #sect_ |
   |    |        | Par    |        |    |        |        | CID_95 |
   |    |        | ticle" |        |    |        |        | 26>`__ |
   |    |        | ) <#DC |        |    |        |        |        |
   |    |        | M_1300 |        |    |        |        |        |
   |    |        | 37>`__ |        |    |        |        |        |
   +----+--------+--------+--------+----+--------+--------+--------+
   | 13 | CODE   | DT     | 1-n    | U  |        |        | B\ `B  |
   |    |        | `(1    |        |    |        |        | rachyt |
   |    |        | 30038, |        |    |        |        | herapy |
   |    |        | DCM,   |        |    |        |        | Iso    |
   |    |        | "B     |        |    |        |        | tope < |
   |    |        | rachyt |        |    |        |        | #sect_ |
   |    |        | herapy |        |    |        |        | CID_95 |
   |    |        | Is     |        |    |        |        | 28>`__ |
   |    |        | otope" |        |    |        |        |        |
   |    |        | ) <#DC |        |    |        |        |        |
   |    |        | M_1300 |        |    |        |        |        |
   |    |        | 38>`__ |        |    |        |        |        |
   +----+--------+--------+--------+----+--------+--------+--------+
   | 14 | CODE   | DT     | 1-n    | U  |        |        | B\     |
   |    |        | `(1    |        |    |        |        | `Telet |
   |    |        | 30040, |        |    |        |        | herapy |
   |    |        | DCM,   |        |    |        |        | Iso    |
   |    |        | "Telet |        |    |        |        | tope < |
   |    |        | herapy |        |    |        |        | #sect_ |
   |    |        | Is     |        |    |        |        | CID_95 |
   |    |        | otope" |        |    |        |        | 27>`__ |
   |    |        | ) <#DC |        |    |        |        |        |
   |    |        | M_1300 |        |    |        |        |        |
   |    |        | 40>`__ |        |    |        |        |        |
   +----+--------+--------+--------+----+--------+--------+--------+
   | 15 | N      | DT     | 1-n    | U  |        |        | UNIT   |
   |    | UMERIC | `(1    |        |    |        |        | S=D\ ` |
   |    |        | 30034, |        |    |        |        | Radiot |
   |    |        | DCM,   |        |    |        |        | herapy |
   |    |        | "RT    |        |    |        |        | Tre    |
   |    |        | Beam   |        |    |        |        | atment |
   |    |        | E      |        |    |        |        | Energy |
   |    |        | nergy" |        |    |        |        | Unit < |
   |    |        | ) <#DC |        |    |        |        | #sect_ |
   |    |        | M_1300 |        |    |        |        | CID_95 |
   |    |        | 34>`__ |        |    |        |        | 21>`__ |
   +----+--------+--------+--------+----+--------+--------+--------+
   | 16 | CODE   | DT     | 1-n    | U  |        |        | B\ `   |
   |    |        | `(1    |        |    |        |        | Radiot |
   |    |        | 30035, |        |    |        |        | herapy |
   |    |        | DCM,   |        |    |        |        | Acqui  |
   |    |        | "P     |        |    |        |        | sition |
   |    |        | atient |        |    |        |        | Wo     |
   |    |        | Posit  |        |    |        |        | rkitem |
   |    |        | ioning |        |    |        |        | Defini |
   |    |        | Pro    |        |    |        |        | tion < |
   |    |        | cedure |        |    |        |        | #sect_ |
   |    |        | Note"  |        |    |        |        | CID_92 |
   |    |        | ) <#DC |        |    |        |        | 42>`__ |
   |    |        | M_1300 |        |    |        |        |        |
   |    |        | 35>`__ |        |    |        |        |        |
   +----+--------+--------+--------+----+--------+--------+--------+
   | 17 | TEXT   | EV     | 1      | U  |        |        |        |
   |    |        | `(1    |        |    |        |        |        |
   |    |        | 30036, |        |    |        |        |        |
   |    |        | DCM,   |        |    |        |        |        |
   |    |        | "QA    |        |    |        |        |        |
   |    |        | P      |        |    |        |        |        |
   |    |        | rocess |        |    |        |        |        |
   |    |        | Note"  |        |    |        |        |        |
   |    |        | ) <#DC |        |    |        |        |        |
   |    |        | M_1300 |        |    |        |        |        |
   |    |        | 36>`__ |        |    |        |        |        |
   +----+--------+--------+--------+----+--------+--------+--------+
   | 18 | TEXT   | EV     | 1      | U  |        |        |        |
   |    |        | `(1    |        |    |        |        |        |
   |    |        | 30027, |        |    |        |        |        |
   |    |        | DCM,   |        |    |        |        |        |
   |    |        | "4D    |        |    |        |        |        |
   |    |        | Rad    |        |    |        |        |        |
   |    |        | iation |        |    |        |        |        |
   |    |        | Tre    |        |    |        |        |        |
   |    |        | atment |        |    |        |        |        |
   |    |        | Note"  |        |    |        |        |        |
   |    |        | ) <#DC |        |    |        |        |        |
   |    |        | M_1300 |        |    |        |        |        |
   |    |        | 27>`__ |        |    |        |        |        |
   +----+--------+--------+--------+----+--------+--------+--------+
   | 19 | TEXT   | EV     | 1      | U  |        |        |        |
   |    |        | `(1    |        |    |        |        |        |
   |    |        | 30039, |        |    |        |        |        |
   |    |        | DCM,   |        |    |        |        |        |
   |    |        | "Ad    |        |    |        |        |        |
   |    |        | aptive |        |    |        |        |        |
   |    |        | Rad    |        |    |        |        |        |
   |    |        | iation |        |    |        |        |        |
   |    |        | T      |        |    |        |        |        |
   |    |        | herapy |        |    |        |        |        |
   |    |        | Note"  |        |    |        |        |        |
   |    |        | ) <#DC |        |    |        |        |        |
   |    |        | M_1300 |        |    |        |        |        |
   |    |        | 39>`__ |        |    |        |        |        |
   +----+--------+--------+--------+----+--------+--------+--------+

**Content Item Descriptions**

+---------------------+-----------------------------------------------+
| Rows 11, 12, 13, 14 | The source of radiation to be used for this   |
|                     | RT treatment. More than one source indicates  |
|                     | that the RT treatment may use any combination |
|                     | for treatment. There is no defined            |
|                     | relationship between the entries in Row 11,   |
|                     | 12, 13, 14 and entries in the Rows 15 and 16. |
+---------------------+-----------------------------------------------+
| Row 15              | Including several energies indicates that     |
|                     | they may be used in any combination.          |
+---------------------+-----------------------------------------------+
| Row 16              | The codes identify procedures supporting the  |
|                     | patient positioning process prior to RT       |
|                     | treatment. Including several procedures       |
|                     | indicates that they may be used in any        |
|                     | combination.                                  |
+---------------------+-----------------------------------------------+

.. _sect_TID_15301:

RT Segment Characteristics
~~~~~~~~~~~~~~~~~~~~~~~~~~

**Type:**
   **Extensible**

**Order:**
   **Non-Significant**

**Root:**
   **No**

.. table:: RT Segment Characteristics

   +----+----+--------+--------+-----+--------+--------+--------+
   |    | NL | VT     | C      | VM  | Req    | Con    | Value  |
   |    |    |        | oncept |     | Type   | dition | Set    |
   |    |    |        | Name   |     |        |        | Cons   |
   |    |    |        |        |     |        |        | traint |
   +====+====+========+========+=====+========+========+========+
   | 1  |    | N      | EV     | 1   | U      |        | Units  |
   |    |    | UMERIC | `(1    |     |        |        | = EV   |
   |    |    |        | 30082, |     |        |        | (      |
   |    |    |        | DCM,   |     |        |        | ratio, |
   |    |    |        | "Re    |     |        |        | UCUM,  |
   |    |    |        | lative |     |        |        | "r     |
   |    |    |        | Mass   |     |        |        | atio") |
   |    |    |        | De     |     |        |        |        |
   |    |    |        | nsity" |     |        |        |        |
   |    |    |        | ) <#DC |     |        |        |        |
   |    |    |        | M_1300 |     |        |        |        |
   |    |    |        | 82>`__ |     |        |        |        |
   +----+----+--------+--------+-----+--------+--------+--------+
   | 2  |    | N      | EV     | 1   | U      |        | Units  |
   |    |    | UMERIC | `(1    |     |        |        | = EV   |
   |    |    |        | 30083, |     |        |        | (      |
   |    |    |        | DCM,   |     |        |        | ratio, |
   |    |    |        | "Re    |     |        |        | UCUM,  |
   |    |    |        | lative |     |        |        | "r     |
   |    |    |        | El     |     |        |        | atio") |
   |    |    |        | ectron |     |        |        |        |
   |    |    |        | De     |     |        |        |        |
   |    |    |        | nsity" |     |        |        |        |
   |    |    |        | ) <#DC |     |        |        |        |
   |    |    |        | M_1300 |     |        |        |        |
   |    |    |        | 83>`__ |     |        |        |        |
   +----+----+--------+--------+-----+--------+--------+--------+
   | 3  |    | N      | EV     | 1   | U      |        | Units  |
   |    |    | UMERIC | `(1    |     |        |        | = EV   |
   |    |    |        | 30084, |     |        |        | (1,    |
   |    |    |        | DCM,   |     |        |        | UCUM,  |
   |    |    |        | "Eff   |     |        |        | "no    |
   |    |    |        | ective |     |        |        | u      |
   |    |    |        | Z"     |     |        |        | nits") |
   |    |    |        | ) <#DC |     |        |        |        |
   |    |    |        | M_1300 |     |        |        |        |
   |    |    |        | 84>`__ |     |        |        |        |
   +----+----+--------+--------+-----+--------+--------+--------+
   | 4  |    | N      | EV     | 1   | U      |        | Units  |
   |    |    | UMERIC | `(1    |     |        |        | = EV   |
   |    |    |        | 30085, |     |        |        | (/u,   |
   |    |    |        | DCM,   |     |        |        | UCUM,  |
   |    |    |        | "Eff   |     |        |        | "/u")  |
   |    |    |        | ective |     |        |        |        |
   |    |    |        | Z per  |     |        |        |        |
   |    |    |        | A"     |     |        |        |        |
   |    |    |        | ) <#DC |     |        |        |        |
   |    |    |        | M_1300 |     |        |        |        |
   |    |    |        | 85>`__ |     |        |        |        |
   +----+----+--------+--------+-----+--------+--------+--------+
   | 5  |    | N      | EV     | 1   | U      |        | Units  |
   |    |    | UMERIC | `(1    |     |        |        | = EV   |
   |    |    |        | 30086, |     |        |        | (      |
   |    |    |        | DCM,   |     |        |        | ratio, |
   |    |    |        | "Re    |     |        |        | UCUM,  |
   |    |    |        | lative |     |        |        | "r     |
   |    |    |        | Linear |     |        |        | atio") |
   |    |    |        | St     |     |        |        |        |
   |    |    |        | opping |     |        |        |        |
   |    |    |        | Power" |     |        |        |        |
   |    |    |        | ) <#DC |     |        |        |        |
   |    |    |        | M_1300 |     |        |        |        |
   |    |    |        | 86>`__ |     |        |        |        |
   +----+----+--------+--------+-----+--------+--------+--------+
   | 6  | >  | N      | EV     | 1   | M      |        | Units  |
   |    |    | UMERIC | `(1    |     |        |        | = EV   |
   |    |    |        | 30087, |     |        |        | (MeV,  |
   |    |    |        | DCM,   |     |        |        | UCUM,  |
   |    |    |        | "Ref   |     |        |        | "      |
   |    |    |        | erence |     |        |        | Megael |
   |    |    |        | E      |     |        |        | ectron |
   |    |    |        | nergy" |     |        |        | volt") |
   |    |    |        | ) <#DC |     |        |        |        |
   |    |    |        | M_1300 |     |        |        |        |
   |    |    |        | 87>`__ |     |        |        |        |
   +----+----+--------+--------+-----+--------+--------+--------+
   | 7  |    | N      | EV     | 1   | U      |        | Units  |
   |    |    | UMERIC | `(1    |     |        |        | = EV   |
   |    |    |        | 30088, |     |        |        | (      |
   |    |    |        | DCM,   |     |        |        | ratio, |
   |    |    |        | "      |     |        |        | UCUM,  |
   |    |    |        | Linear |     |        |        | "r     |
   |    |    |        | Cell   |     |        |        | atio") |
   |    |    |        | Kill   |     |        |        |        |
   |    |    |        | F      |     |        |        |        |
   |    |    |        | actor" |     |        |        |        |
   |    |    |        | ) <#DC |     |        |        |        |
   |    |    |        | M_1300 |     |        |        |        |
   |    |    |        | 88>`__ |     |        |        |        |
   +----+----+--------+--------+-----+--------+--------+--------+
   | 8  |    | N      | EV     | 1   | U      |        | Units  |
   |    |    | UMERIC | `(1    |     |        |        | = EV   |
   |    |    |        | 30089, |     |        |        | (      |
   |    |    |        | DCM,   |     |        |        | ratio, |
   |    |    |        | "Qua   |     |        |        | UCUM,  |
   |    |    |        | dratic |     |        |        | "r     |
   |    |    |        | Cell   |     |        |        | atio") |
   |    |    |        | Kill   |     |        |        |        |
   |    |    |        | F      |     |        |        |        |
   |    |    |        | actor" |     |        |        |        |
   |    |    |        | ) <#DC |     |        |        |        |
   |    |    |        | M_1300 |     |        |        |        |
   |    |    |        | 89>`__ |     |        |        |        |
   +----+----+--------+--------+-----+--------+--------+--------+
   | 9  |    | N      | EV     | 1   | U      |        | Units  |
   |    |    | UMERIC | `(1    |     |        |        | = EV   |
   |    |    |        | 30090, |     |        |        | (      |
   |    |    |        | DCM,   |     |        |        | ratio, |
   |    |    |        | "High  |     |        |        | UCUM,  |
   |    |    |        | Dose   |     |        |        | "r     |
   |    |    |        | Fr     |     |        |        | atio") |
   |    |    |        | action |     |        |        |        |
   |    |    |        | Linear |     |        |        |        |
   |    |    |        | Cell   |     |        |        |        |
   |    |    |        | Kill   |     |        |        |        |
   |    |    |        | F      |     |        |        |        |
   |    |    |        | actor" |     |        |        |        |
   |    |    |        | ) <#DC |     |        |        |        |
   |    |    |        | M_1300 |     |        |        |        |
   |    |    |        | 90>`__ |     |        |        |        |
   +----+----+--------+--------+-----+--------+--------+--------+
   | 10 |    | N      | EV     | 1   | U      |        | Units  |
   |    |    | UMERIC | `(1    |     |        |        | = EV   |
   |    |    |        | 30091, |     |        |        | (s,    |
   |    |    |        | DCM,   |     |        |        | UCUM,  |
   |    |    |        | "Hal   |     |        |        | "se    |
   |    |    |        | f-time |     |        |        | cond") |
   |    |    |        | for    |     |        |        |        |
   |    |    |        | Tissue |     |        |        |        |
   |    |    |        | Repair |     |        |        |        |
   |    |    |        | "      |     |        |        |        |
   |    |    |        | ) <#DC |     |        |        |        |
   |    |    |        | M_1300 |     |        |        |        |
   |    |    |        | 91>`__ |     |        |        |        |
   +----+----+--------+--------+-----+--------+--------+--------+
   | 11 |    | N      | EV     | 1   | U      |        | Units  |
   |    |    | UMERIC | `(1    |     |        |        | = EV   |
   |    |    |        | 30092, |     |        |        | (Gy,   |
   |    |    |        | DCM,   |     |        |        | UCUM,  |
   |    |    |        | "High  |     |        |        | "      |
   |    |    |        | Dose   |     |        |        | Gray") |
   |    |    |        | Fr     |     |        |        |        |
   |    |    |        | action |     |        |        |        |
   |    |    |        | Tran   |     |        |        |        |
   |    |    |        | sition |     |        |        |        |
   |    |    |        | Dose"  |     |        |        |        |
   |    |    |        | ) <#DC |     |        |        |        |
   |    |    |        | M_1300 |     |        |        |        |
   |    |    |        | 92>`__ |     |        |        |        |
   +----+----+--------+--------+-----+--------+--------+--------+
   | 12 |    | N      | EV     | 1-n | U      |        | Units  |
   |    |    | UMERIC | `(1    |     |        |        | = EV   |
   |    |    |        | 30093, |     |        |        | (1,    |
   |    |    |        | DCM,   |     |        |        | UCUM,  |
   |    |    |        | "      |     |        |        | "no    |
   |    |    |        | Atomic |     |        |        | u      |
   |    |    |        | N      |     |        |        | nits") |
   |    |    |        | umber" |     |        |        |        |
   |    |    |        | ) <#DC |     |        |        |        |
   |    |    |        | M_1300 |     |        |        |        |
   |    |    |        | 93>`__ |     |        |        |        |
   +----+----+--------+--------+-----+--------+--------+--------+
   | 13 | >  | N      | EV     | 1   | M      |        | Units  |
   |    |    | UMERIC | `(1    |     |        |        | = EV   |
   |    |    |        | 30094, |     |        |        | (      |
   |    |    |        | DCM,   |     |        |        | ratio, |
   |    |    |        | "Ele   |     |        |        | UCUM,  |
   |    |    |        | mental |     |        |        | "r     |
   |    |    |        | Compo  |     |        |        | atio") |
   |    |    |        | sition |     |        |        |        |
   |    |    |        | Atomic |     |        |        |        |
   |    |    |        | Mass   |     |        |        |        |
   |    |    |        | Fra    |     |        |        |        |
   |    |    |        | ction" |     |        |        |        |
   |    |    |        | ) <#DC |     |        |        |        |
   |    |    |        | M_1300 |     |        |        |        |
   |    |    |        | 94>`__ |     |        |        |        |
   +----+----+--------+--------+-----+--------+--------+--------+
   | 14 |    | N      | EV     | 1   | U      |        | Units  |
   |    |    | UMERIC | `(1    |     |        |        | = EV   |
   |    |    |        | 30095, |     |        |        | (      |
   |    |    |        | DCM,   |     |        |        | ratio, |
   |    |    |        | "alpha |     |        |        | UCUM,  |
   |    |    |        | gEUD   |     |        |        | "r     |
   |    |    |        | value" |     |        |        | atio") |
   |    |    |        | ) <#DC |     |        |        |        |
   |    |    |        | M_1300 |     |        |        |        |
   |    |    |        | 95>`__ |     |        |        |        |
   +----+----+--------+--------+-----+--------+--------+--------+

**Content Item Descriptions**

+-------------+-------------------------------------------------------+
| Rows 12, 13 | The value of `(130094, DCM, "Elemental Composition    |
|             | Atomic Mass Fraction") <#DCM_130094>`__ annotates the |
|             | fractional weight of the elements identified by the   |
|             | `(130093, DCM, "Atomic Number") <#DCM_130093>`__ with |
|             | respect to the total mass of the segment. The allowed |
|             | value is in the range of [0, 1].                      |
+-------------+-------------------------------------------------------+

.. _sect_TID_15302:

Patient Support Position Parameters
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

**Type:**
   **Extensible**

**Order:**
   **Non-Significant**

**Root:**
   **No**

.. table:: Patient Support Position Parameters

   +----+---------+-----------+----+----------+-----------+-----------+
   |    | VT      | Concept   | VM | Req Type | Condition | Value Set |
   |    |         | Name      |    |          |           | C         |
   |    |         |           |    |          |           | onstraint |
   +====+=========+===========+====+==========+===========+===========+
   | 1  | NUMERIC | EV        | 1  | U        |           | Units =   |
   |    |         | `(126802, |    |          |           | EV (deg,  |
   |    |         | DCM,      |    |          |           | UCUM,     |
   |    |         | "IEC61217 |    |          |           | "deg")    |
   |    |         | Table Top |    |          |           |           |
   |    |         | C         |    |          |           |           |
   |    |         | ontinuous |    |          |           |           |
   |    |         | Pitch     |    |          |           |           |
   |    |         | Angle"    |    |          |           |           |
   |    |         | ) <#DCM_1 |    |          |           |           |
   |    |         | 26802>`__ |    |          |           |           |
   +----+---------+-----------+----+----------+-----------+-----------+
   | 2  | NUMERIC | EV        | 1  | U        |           | Units =   |
   |    |         | `(126803, |    |          |           | EV (deg,  |
   |    |         | DCM,      |    |          |           | UCUM,     |
   |    |         | "IEC61217 |    |          |           | "deg")    |
   |    |         | Table Top |    |          |           |           |
   |    |         | C         |    |          |           |           |
   |    |         | ontinuous |    |          |           |           |
   |    |         | Roll      |    |          |           |           |
   |    |         | Angle"    |    |          |           |           |
   |    |         | ) <#DCM_1 |    |          |           |           |
   |    |         | 26803>`__ |    |          |           |           |
   +----+---------+-----------+----+----------+-----------+-----------+
   | 3  | NUMERIC | EV        | 1  | U        |           | Units =   |
   |    |         | `(126801, |    |          |           | EV (deg,  |
   |    |         | DCM,      |    |          |           | UCUM,     |
   |    |         | "IEC61217 |    |          |           | "deg")    |
   |    |         | Patient   |    |          |           |           |
   |    |         | Support   |    |          |           |           |
   |    |         | C         |    |          |           |           |
   |    |         | ontinuous |    |          |           |           |
   |    |         | Yaw       |    |          |           |           |
   |    |         | Angle"    |    |          |           |           |
   |    |         | ) <#DCM_1 |    |          |           |           |
   |    |         | 26801>`__ |    |          |           |           |
   +----+---------+-----------+----+----------+-----------+-----------+
   | 4  | NUMERIC | EV        | 1  | U        |           | Units =   |
   |    |         | `(126804, |    |          |           | EV (mm,   |
   |    |         | DCM,      |    |          |           | UCUM,     |
   |    |         | "IEC61217 |    |          |           | "mm")     |
   |    |         | Table Top |    |          |           |           |
   |    |         | Eccentric |    |          |           |           |
   |    |         | Axis      |    |          |           |           |
   |    |         | Distance" |    |          |           |           |
   |    |         | ) <#DCM_1 |    |          |           |           |
   |    |         | 26804>`__ |    |          |           |           |
   +----+---------+-----------+----+----------+-----------+-----------+
   | 5  | NUMERIC | EV        | 1  | U        |           | Units =   |
   |    |         | `(126805, |    |          |           | EV (deg,  |
   |    |         | DCM,      |    |          |           | UCUM,     |
   |    |         | "IEC61217 |    |          |           | "deg")    |
   |    |         | Table Top |    |          |           |           |
   |    |         | C         |    |          |           |           |
   |    |         | ontinuous |    |          |           |           |
   |    |         | Eccentric |    |          |           |           |
   |    |         | Angle"    |    |          |           |           |
   |    |         | ) <#DCM_1 |    |          |           |           |
   |    |         | 26805>`__ |    |          |           |           |
   +----+---------+-----------+----+----------+-----------+-----------+
   | 6  | NUMERIC | EV        | 1  | U        |           | Units =   |
   |    |         | `(126806, |    |          |           | EV (mm,   |
   |    |         | DCM,      |    |          |           | UCUM,     |
   |    |         | "IEC61217 |    |          |           | "mm")     |
   |    |         | Table Top |    |          |           |           |
   |    |         | Lateral   |    |          |           |           |
   |    |         | Position" |    |          |           |           |
   |    |         | ) <#DCM_1 |    |          |           |           |
   |    |         | 26806>`__ |    |          |           |           |
   +----+---------+-----------+----+----------+-----------+-----------+
   | 7  | NUMERIC | EV        | 1  | U        |           | Units =   |
   |    |         | `(126807, |    |          |           | EV (mm,   |
   |    |         | DCM,      |    |          |           | UCUM,     |
   |    |         | "IEC61217 |    |          |           | "mm")     |
   |    |         | Table Top |    |          |           |           |
   |    |         | Lon       |    |          |           |           |
   |    |         | gitudinal |    |          |           |           |
   |    |         | Position" |    |          |           |           |
   |    |         | ) <#DCM_1 |    |          |           |           |
   |    |         | 26807>`__ |    |          |           |           |
   +----+---------+-----------+----+----------+-----------+-----------+
   | 8  | NUMERIC | EV        | 1  | U        |           | Units =   |
   |    |         | `(126808, |    |          |           | EV (mm,   |
   |    |         | DCM,      |    |          |           | UCUM,     |
   |    |         | "IEC61217 |    |          |           | "mm")     |
   |    |         | Table Top |    |          |           |           |
   |    |         | Vertical  |    |          |           |           |
   |    |         | Position" |    |          |           |           |
   |    |         | ) <#DCM_1 |    |          |           |           |
   |    |         | 26808>`__ |    |          |           |           |
   +----+---------+-----------+----+----------+-----------+-----------+
   | 9  | NUMERIC | EV        | 1  | U        |           | Units =   |
   |    |         | `(126812, |    |          |           | EV (deg,  |
   |    |         | DCM,      |    |          |           | UCUM,     |
   |    |         | "I        |    |          |           | "deg")    |
   |    |         | socentric |    |          |           |           |
   |    |         | Patient   |    |          |           |           |
   |    |         | Support   |    |          |           |           |
   |    |         | C         |    |          |           |           |
   |    |         | ontinuous |    |          |           |           |
   |    |         | Pitch     |    |          |           |           |
   |    |         | Angle"    |    |          |           |           |
   |    |         | ) <#DCM_1 |    |          |           |           |
   |    |         | 26812>`__ |    |          |           |           |
   +----+---------+-----------+----+----------+-----------+-----------+
   | 10 | NUMERIC | EV        | 1  | U        |           | Units =   |
   |    |         | `(126813, |    |          |           | EV (deg,  |
   |    |         | DCM,      |    |          |           | UCUM,     |
   |    |         | "I        |    |          |           | "deg")    |
   |    |         | socentric |    |          |           |           |
   |    |         | Patient   |    |          |           |           |
   |    |         | Support   |    |          |           |           |
   |    |         | C         |    |          |           |           |
   |    |         | ontinuous |    |          |           |           |
   |    |         | Roll      |    |          |           |           |
   |    |         | Angle"    |    |          |           |           |
   |    |         | ) <#DCM_1 |    |          |           |           |
   |    |         | 26813>`__ |    |          |           |           |
   +----+---------+-----------+----+----------+-----------+-----------+
   | 11 | NUMERIC | EV        | 1  | U        |           | Units =   |
   |    |         | `(126814, |    |          |           | EV (deg,  |
   |    |         | DCM,      |    |          |           | UCUM,     |
   |    |         | "I        |    |          |           | "deg")    |
   |    |         | socentric |    |          |           |           |
   |    |         | Patient   |    |          |           |           |
   |    |         | Support   |    |          |           |           |
   |    |         | C         |    |          |           |           |
   |    |         | ontinuous |    |          |           |           |
   |    |         | Yaw       |    |          |           |           |
   |    |         | Angle"    |    |          |           |           |
   |    |         | ) <#DCM_1 |    |          |           |           |
   |    |         | 26814>`__ |    |          |           |           |
   +----+---------+-----------+----+----------+-----------+-----------+
   | 12 | NUMERIC | EV        | 1  | U        |           | Units =   |
   |    |         | `(126815, |    |          |           | EV (mm,   |
   |    |         | DCM,      |    |          |           | UCUM,     |
   |    |         | "I        |    |          |           | "mm")     |
   |    |         | socentric |    |          |           |           |
   |    |         | Patient   |    |          |           |           |
   |    |         | Support   |    |          |           |           |
   |    |         | Lateral   |    |          |           |           |
   |    |         | Position" |    |          |           |           |
   |    |         | ) <#DCM_1 |    |          |           |           |
   |    |         | 26815>`__ |    |          |           |           |
   +----+---------+-----------+----+----------+-----------+-----------+
   | 13 | NUMERIC | EV        | 1  | U        |           | Units =   |
   |    |         | `(126816, |    |          |           | EV (mm,   |
   |    |         | DCM,      |    |          |           | UCUM,     |
   |    |         | "I        |    |          |           | "mm")     |
   |    |         | socentric |    |          |           |           |
   |    |         | Patient   |    |          |           |           |
   |    |         | Support   |    |          |           |           |
   |    |         | Lon       |    |          |           |           |
   |    |         | gitudinal |    |          |           |           |
   |    |         | Position" |    |          |           |           |
   |    |         | ) <#DCM_1 |    |          |           |           |
   |    |         | 26816>`__ |    |          |           |           |
   +----+---------+-----------+----+----------+-----------+-----------+
   | 14 | NUMERIC | EV        | 1  | U        |           | Units =   |
   |    |         | `(126817, |    |          |           | EV (mm,   |
   |    |         | DCM,      |    |          |           | UCUM,     |
   |    |         | "I        |    |          |           | "mm")     |
   |    |         | socentric |    |          |           |           |
   |    |         | Patient   |    |          |           |           |
   |    |         | Support   |    |          |           |           |
   |    |         | Vertical  |    |          |           |           |
   |    |         | Position" |    |          |           |           |
   |    |         | ) <#DCM_1 |    |          |           |           |
   |    |         | 26817>`__ |    |          |           |           |
   +----+---------+-----------+----+----------+-----------+-----------+

.. _sect_TID_15303:

Radiotherapy Treatment Scheduled Processing Parameters
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

**Type:**
   **Extensible**

**Order:**
   **Non-Significant**

**Root:**
   **No**

.. table:: Radiotherapy Treatment Scheduled Processing Parameters

   +---+---------+-----------+----+----------+-----------+-----------+
   |   | VT      | Concept   | VM | Req Type | Condition | Value Set |
   |   |         | Name      |    |          |           | C         |
   |   |         |           |    |          |           | onstraint |
   +===+=========+===========+====+==========+===========+===========+
   | 1 | TEXT    | EV        | 1  | U        |           |           |
   |   |         | `(121384, |    |          |           |           |
   |   |         | DCM, "RT  |    |          |           |           |
   |   |         | Plan      |    |          |           |           |
   |   |         | Label"    |    |          |           |           |
   |   |         | ) <#DCM_1 |    |          |           |           |
   |   |         | 21384>`__ |    |          |           |           |
   +---+---------+-----------+----+----------+-----------+-----------+
   | 2 | NUMERIC | EV        | 1  | U        |           | UNIT = EV |
   |   |         | `(121385, |    |          |           | (1, UCUM, |
   |   |         | DCM,      |    |          |           | "no       |
   |   |         | "Current  |    |          |           | units")   |
   |   |         | Fraction  |    |          |           |           |
   |   |         | Number"   |    |          |           |           |
   |   |         | ) <#DCM_1 |    |          |           |           |
   |   |         | 21385>`__ |    |          |           |           |
   +---+---------+-----------+----+----------+-----------+-----------+
   | 3 | NUMERIC | EV        | 1  | U        |           | UNIT = EV |
   |   |         | `(121386, |    |          |           | (1, UCUM, |
   |   |         | DCM,      |    |          |           | "no       |
   |   |         | "Number   |    |          |           | units")   |
   |   |         | of        |    |          |           |           |
   |   |         | Fractions |    |          |           |           |
   |   |         | Planned"  |    |          |           |           |
   |   |         | ) <#DCM_1 |    |          |           |           |
   |   |         | 21386>`__ |    |          |           |           |
   +---+---------+-----------+----+----------+-----------+-----------+
   | 4 | NUMERIC | EV        | 1  | U        |           | UNIT = EV |
   |   |         | `(121387, |    |          |           | (1, UCUM, |
   |   |         | DCM,      |    |          |           | "no       |
   |   |         | "Number   |    |          |           | units")   |
   |   |         | of        |    |          |           |           |
   |   |         | Fractions |    |          |           |           |
   |   |         | C         |    |          |           |           |
   |   |         | ompleted" |    |          |           |           |
   |   |         | ) <#DCM_1 |    |          |           |           |
   |   |         | 21387>`__ |    |          |           |           |
   +---+---------+-----------+----+----------+-----------+-----------+
   | 5 | CODE    | EV        | 1  | U        |           | D\        |
   |   |         | `(121388, |    |          |           |  `Yes-No  |
   |   |         | DCM,      |    |          |           | <#sect_CI |
   |   |         | "C        |    |          |           | D_230>`__ |
   |   |         | hecked-In |    |          |           |           |
   |   |         | Status"   |    |          |           |           |
   |   |         | ) <#DCM_1 |    |          |           |           |
   |   |         | 21388>`__ |    |          |           |           |
   +---+---------+-----------+----+----------+-----------+-----------+

.. _sect_TID_15304:

Radiotherapy Treatment Progress Parameters
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

**Type:**
   **Extensible**

**Order:**
   **Non-Significant**

**Root:**
   **No**

.. table:: Radiotherapy Treatment Progress Parameters

   +---+---------+-----------+----+----------+-----------+-----------+
   |   | VT      | Concept   | VM | Req Type | Condition | Value Set |
   |   |         | Name      |    |          |           | C         |
   |   |         |           |    |          |           | onstraint |
   +===+=========+===========+====+==========+===========+===========+
   | 1 | NUMERIC | EV        | 1  | U        |           | UNIT = EV |
   |   |         | `(121389, |    |          |           | (1, UCUM, |
   |   |         | DCM,      |    |          |           | "no       |
   |   |         | "R        |    |          |           | units")   |
   |   |         | eferenced |    |          |           |           |
   |   |         | Beam      |    |          |           |           |
   |   |         | Number"   |    |          |           |           |
   |   |         | ) <#DCM_1 |    |          |           |           |
   |   |         | 21389>`__ |    |          |           |           |
   +---+---------+-----------+----+----------+-----------+-----------+

.. _sect_TID_15400:

Real-World Quantity Definition
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

**Type:**
   **Extensible**

**Order:**
   **Non-Significant**

**Root:**
   **No**

.. table:: Real-World Quantity Definition

   +---+----+------+---------+-----+---------+---------+---------+
   |   | NL | VT   | Concept | VM  | Req     | Co      | Value   |
   |   |    |      | Name    |     | Type    | ndition | Set     |
   |   |    |      |         |     |         |         | Con     |
   |   |    |      |         |     |         |         | straint |
   +===+====+======+=========+=====+=========+=========+=========+
   | 1 |    | CODE | DT      | 1   | M       |         | B\ `A   |
   |   |    |      | `(246   |     |         |         | bstract |
   |   |    |      | 205007, |     |         |         | Mul     |
   |   |    |      | SCT,    |     |         |         | ti-dime |
   |   |    |      | "Quant  |     |         |         | nsional |
   |   |    |      | ity") < |     |         |         | Image   |
   |   |    |      | http:// |     |         |         | Model   |
   |   |    |      | snomed. |     |         |         | Co      |
   |   |    |      | info/id |     |         |         | mponent |
   |   |    |      | /246205 |     |         |         | S       |
   |   |    |      | 007>`__ |     |         |         | emantic |
   |   |    |      |         |     |         |         | s <#sec |
   |   |    |      |         |     |         |         | t_CID_7 |
   |   |    |      |         |     |         |         | 180>`__ |
   +---+----+------+---------+-----+---------+---------+---------+
   | 2 |    | CODE | B\ `P   | 1-n | U       |         |         |
   |   |    |      | hysical |     |         |         |         |
   |   |    |      | Q       |     |         |         |         |
   |   |    |      | uantity |     |         |         |         |
   |   |    |      | Des     |     |         |         |         |
   |   |    |      | criptor |     |         |         |         |
   |   |    |      | s <#sec |     |         |         |         |
   |   |    |      | t_CID_9 |     |         |         |         |
   |   |    |      | 000>`__ |     |         |         |         |
   +---+----+------+---------+-----+---------+---------+---------+

**Content Item Descriptions**

+-------+-------------------------------------------------------------+
| Row 1 | This row uses a concept name that specifies the quantified  |
|       | characteristic. It is not required that `(246205007, SCT,   |
|       | "Quantity") <http://snomed.info/id/246205007>`__ be used if |
|       | there is a reason to use a similar concept.                 |
+-------+-------------------------------------------------------------+
| Row 2 | May be concept modifiers, such as `(370129005, SCT,         |
|       | "Measurement Method") <http://snomed.info/id/370129005>`__. |
+-------+-------------------------------------------------------------+

.. _sect_TID_15401:

Real-World Quantity Definition for X-Ray Attenuation Properties
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

**Type:**
   **Extensible**

**Order:**
   **Non-Significant**

**Root:**
   **No**

.. table:: Real-World Quantity Definition for X-Ray Attenuation
Properties

   +---+----+---------+---------+----+---------+---------+---------+
   |   | NL | VT      | Concept | VM | Req     | Co      | Value   |
   |   |    |         | Name    |    | Type    | ndition | Set     |
   |   |    |         |         |    |         |         | Con     |
   |   |    |         |         |    |         |         | straint |
   +===+====+=========+=========+====+=========+=========+=========+
   | 1 |    | INCLUDE | D\ `Rea | 1  | M       |         |         |
   |   |    |         | l-World |    |         |         |         |
   |   |    |         | Q       |    |         |         |         |
   |   |    |         | uantity |    |         |         |         |
   |   |    |         | Def     |    |         |         |         |
   |   |    |         | inition |    |         |         |         |
   |   |    |         |  <#sect |    |         |         |         |
   |   |    |         | _TID_15 |    |         |         |         |
   |   |    |         | 400>`__ |    |         |         |         |
   +---+----+---------+---------+----+---------+---------+---------+
   | 2 |    | NUMERIC | EV      | 1  | MC      | IF      | UNITS = |
   |   |    |         | `(DCM,  |    |         | `Rea    | EV      |
   |   |    |         | 130087, |    |         | l-World | ("MeV", |
   |   |    |         | "Re     |    |         | Q       | UCUM,   |
   |   |    |         | ference |    |         | uantity | "Mega   |
   |   |    |         | Ener    |    |         | Def     | electro |
   |   |    |         | gy") <# |    |         | inition | nvolt") |
   |   |    |         | DCM_130 |    |         |  <#sect |         |
   |   |    |         | 087>`__ |    |         | _TID_15 |         |
   |   |    |         |         |    |         | 400>`__ |         |
   |   |    |         |         |    |         | Row 1   |         |
   |   |    |         |         |    |         | Q       |         |
   |   |    |         |         |    |         | uantity |         |
   |   |    |         |         |    |         | value   |         |
   |   |    |         |         |    |         | is      |         |
   |   |    |         |         |    |         | `(      |         |
   |   |    |         |         |    |         | 130086, |         |
   |   |    |         |         |    |         | DCM,    |         |
   |   |    |         |         |    |         | "R      |         |
   |   |    |         |         |    |         | elative |         |
   |   |    |         |         |    |         | Linear  |         |
   |   |    |         |         |    |         | S       |         |
   |   |    |         |         |    |         | topping |         |
   |   |    |         |         |    |         | Pow     |         |
   |   |    |         |         |    |         | er") <# |         |
   |   |    |         |         |    |         | DCM_130 |         |
   |   |    |         |         |    |         | 086>`__ |         |
   +---+----+---------+---------+----+---------+---------+---------+

