.. _chapter_N:

Externally Defined Value Sets (Informative)
===========================================

This annex identifies those Value Sets defined externally to the DICOM
Standard that are referenced by the Standard. These value sets are
reproduced here for reference only, and might not be the current
version.

These value sets use codes from various coding schemes or code systems,
as identified in `Coding Schemes <#chapter_8>`__.

.. _sect_N.1:

HL7 Value Sets
--------------

HL7 Value Sets are reproduced with the permission of HL7 International.
For the current version of HL7 Value Sets, see the HL7v3 Normative
Edition
(http://www.hl7.org/implement/standards/product_brief.cfm?product_id=186).

.. table:: HL7 Value Sets

   +----------------------+----------------------+----------------------+
   | Value Set Name       | OID                  | Notes                |
   +======================+======================+======================+
   | ActPriority          | 2.16.8               |                      |
   |                      | 40.1.113883.11.16866 |                      |
   +----------------------+----------------------+----------------------+
   | AdministrativeGender | 2.                   |                      |
   |                      | 16.840.1.113883.11.1 |                      |
   +----------------------+----------------------+----------------------+
   | HumanLanguages       | 2.16.8               | Equivalent to        |
   |                      | 40.1.113883.11.11526 | `Languages           |
   |                      |                      |  <#sect_CID_5000>`__ |
   +----------------------+----------------------+----------------------+
   | ImageMediaType       | 2.16.8               |                      |
   |                      | 40.1.113883.11.14839 |                      |
   +----------------------+----------------------+----------------------+
   | NullFlavor           | 2.16.8               |                      |
   |                      | 40.1.113883.11.10609 |                      |
   +----------------------+----------------------+----------------------+
   | Obser                | 2.1                  |                      |
   | vationInterpretation | 6.840.1.113883.11.78 |                      |
   +----------------------+----------------------+----------------------+
   | x_Basi               | 2.16.8               |                      |
   | cConfidentialityKind | 40.1.113883.11.16926 |                      |
   +----------------------+----------------------+----------------------+
   | x_s                  | 2.16.8               |                      |
   | erviceEventPerformer | 40.1.113883.11.19601 |                      |
   +----------------------+----------------------+----------------------+

.. _sect_N.1.1:

ActPriority Value Set
~~~~~~~~~~~~~~~~~~~~~

**Value Set:**
   **ActPriority 2.16.840.1.113883.11.16866**

**Code System(s):**
   **ActPriority 2.16.840.1.113883.5.7**

.. table:: ActPriority Value Set

   ==== =========== ================================
   Code Code System Print Name
   ==== =========== ================================
   A    ActPriority ASAP
   CR   ActPriority Callback results
   CS   ActPriority Callback for scheduling
   CSP  ActPriority Callback placer for scheduling
   CSR  ActPriority Contact recipient for scheduling
   EL   ActPriority Elective
   EM   ActPriority Emergency
   P    ActPriority Preoperative
   PRN  ActPriority As needed
   R    ActPriority Routine
   RR   ActPriority Rush reporting
   S    ActPriority Stat
   T    ActPriority Timing critical
   UD   ActPriority Use as directed
   UR   ActPriority Urgent
   ==== =========== ================================

.. _sect_N.1.2:

AdministrativeGender Value Set
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

**Value Set:**
   **AdministrativeGender 2.16.840.1.113883.11.1**

**Code System(s):**
   **AdministrativeGender 2.16.840.1.113883.5.1**

.. table:: AdministrativeGender Value Set

   ==== ==================== ================
   Code Code System          Print Name
   ==== ==================== ================
   F    AdministrativeGender Female
   M    AdministrativeGender Male
   UN   AdministrativeGender Undifferentiated
   ==== ==================== ================

.. _sect_N.1.3:

ImageMediaType Value Set
~~~~~~~~~~~~~~~~~~~~~~~~

**Value Set:**
   **HL7 ImageMediaType 2.16.840.1.113883.11.14839**

**Code System(s):**
   **mediaType 2.16.840.1.113883.5.79**

.. table:: ImageMediaType Value Set

   =========== =========== ==========
   Code        Code System Print Name
   =========== =========== ==========
   image/g3fax mediaType   g3fax
   image/gif   mediaType   gif
   image/jpeg  mediaType   jpeg
   image/png   mediaType   png
   image/tiff  mediaType   tiff
   =========== =========== ==========

.. _sect_N.1.4:

NullFlavor Value Set
~~~~~~~~~~~~~~~~~~~~

**Value Set:**
   **HL7 NullFlavor 2.16.840.1.113883.11.10609**

**Code System(s):**
   **NullFlavor 2.16.840.1.113883.5.1008**

.. table:: NullFlavor Value Set

   ==== =========== =======================
   Code Code System Print Name
   ==== =========== =======================
   NI   NullFlavor  No Information
   OTH  NullFlavor  other
   NINF NullFlavor  negative infinity
   PINF NullFlavor  positive infinity
   UNK  NullFlavor  unknown
   ASKU NullFlavor  asked but unknown
   NAV  NullFlavor  temporarily unavailable
   NASK NullFlavor  not asked
   TRC  NullFlavor  trace
   MSK  NullFlavor  masked
   NA   NullFlavor  not applicable
   NP   NullFlavor  not present
   ==== =========== =======================

.. _sect_N.1.5:

ObservationInterpretation Value Set
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

**Value Set:**
   **HL7 ObservationInterpretation 2.16.840.1.113883.11.78**

**Code System(s):**
   **ObservationInterpretation 2.16.840.1.113883.5.83**

.. table:: ObservationInterpretation Value Set

   ==== ========================= ======================
   Code Code System               Print Name
   ==== ========================= ======================
   B    ObservationInterpretation better
   D    ObservationInterpretation decreased
   U    ObservationInterpretation increased
   W    ObservationInterpretation worse
   <    ObservationInterpretation low off scale
   >    ObservationInterpretation high off scale
   A    ObservationInterpretation Abnormal
   AA   ObservationInterpretation Abnormal alert
   HH   ObservationInterpretation High alert
   LL   ObservationInterpretation Low alert
   H    ObservationInterpretation High
   L    ObservationInterpretation Low
   N    ObservationInterpretation Normal
   I    ObservationInterpretation intermediate
   MS   ObservationInterpretation moderately susceptible
   R    ObservationInterpretation resistent
   S    ObservationInterpretation susceptible
   VS   ObservationInterpretation very susceptible
   ==== ========================= ======================

.. _sect_N.1.6:

x_BasicConfidentialityKind Value Set
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

**Value Set:**
   **x_BasicConfidentialityKind 2.16.840.1.113883.11.16926**

**Code System(s):**
   **Confidentiality 2.16.840.1.113883.5.25**

.. table:: x_BasicConfidentialityKind Value Set

   ==== =============== ===============
   Code Code System     Print Name
   ==== =============== ===============
   N    Confidentiality Normal
   R    Confidentiality Restricted
   V    Confidentiality Very Restricted
   ==== =============== ===============

.. _sect_N.1.7:

x_serviceEventPerformer Value Set
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

**Value Set:**
   **HL7 x_serviceEventPerformer 2.16.840.1.113883.11.19601**

**Code System(s):**
   **ParticipationType 2.16.840.1.113883.5.90**

.. table:: x_serviceEventPerformer Value Set

   ==== ================= ===================
   Code Code System       Print Name
   ==== ================= ===================
   PRF  ParticipationType Performer
   PPRF ParticipationType Principal performer
   SPRF ParticipationType Secondary performer
   ==== ================= ===================

.. _sect_N.2:

LOINC Value Sets
----------------

LOINC Value Sets are available from Regenstrief Institute, Inc. For the
current version, see the LOINC web site (http://loinc.org/oids).

.. table:: LOINC Value Sets

   ============================ ========================== ========
   Value Set Name               OID                        Notes
   ============================ ========================== ========
   LOINC Imaging Document Codes 1.3.6.1.4.1.12009.10.2.5   
   LOINC Y/N/NA                 1.3.6.1.4.1.12009.10.1.163 LL2850-7
   ============================ ========================== ========

.. _sect_N.2.1:

LOINC Imaging Document Codes (examples)
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

**Value Set:**
   **LOINC Imaging Document Codes 1.3.6.1.4.1.12009.10.2.5**

**Code System(s):**
   **LOINC 2.16.840.1.113883.6.1**

.. table:: LOINC Imaging Document Codes (examples)

   +--------------------------+-------------+--------------------------+
   | Code                     | Code System | Print Name               |
   +==========================+=============+==========================+
   | `11525-3 <http:          | LOINC       | US Pelvis and Fetus for  |
   | //loinc.org/11525-3/>`__ |             | pregnancy                |
   +--------------------------+-------------+--------------------------+
   | `17787-3 <http:          | LOINC       | Thyroid Scan Study       |
   | //loinc.org/17787-3/>`__ |             | report                   |
   +--------------------------+-------------+--------------------------+
   | `18744-3 <http:          | LOINC       | Bronchoscopy study       |
   | //loinc.org/18744-3/>`__ |             |                          |
   +--------------------------+-------------+--------------------------+
   | `18746-8 <http:          | LOINC       | Colonoscopy study        |
   | //loinc.org/18746-8/>`__ |             |                          |
   +--------------------------+-------------+--------------------------+
   | `18748-4 <http:          | LOINC       | Diagnostic imaging study |
   | //loinc.org/18748-4/>`__ |             |                          |
   +--------------------------+-------------+--------------------------+
   | …                        |             |                          |
   +--------------------------+-------------+--------------------------+

.. _sect_N.2.2:

LOINC Y/N/NA
~~~~~~~~~~~~

**Value Set:**
   **LOINC Y/N/NA 1.3.6.1.4.1.12009.10.1.163**

**Code System(s):**
   **LOINC 2.16.840.1.113883.6.1**

.. table:: LOINC Y/N/NA

   ======== =========== ==============
   Code     Code System Print Name
   ======== =========== ==============
   LA33-6   LOINC       Yes
   LA32-8   LOINC       No
   LA4720-4 LOINC       Not Applicable
   ======== =========== ==============

