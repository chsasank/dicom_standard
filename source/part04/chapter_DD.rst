.. _chapter_DD:

RT Machine Verification Service Classes (Normative)
===================================================

.. _sect_DD.1:

Scope
-----

The RT Machine Verification Service Classes define an application-level
class-of-service that facilitates the independent verification of
geometric and dosimetric settings on a radiation delivery system prior
to delivery of a radiation treatment. The service classes are intended
for use with both conventional (e.g., photon, electron) as well as
particle therapy (e.g., proton, ion) treatments.

.. _sect_DD.2:

RT Machine Verification Model
-----------------------------

.. _sect_DD.2.1:

RT Machine Verification Data Flow
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

In the RT Machine Verification Model, the Service Class User (SCU) of
the applicable Machine Verification Service Class is the radiation
delivery system used to administer the treatment. The Machine Parameter
Verifier (MPV) acts in the role of Service Class Provider (SCP).

The communication states between the SCU and SCP can be described in two
levels shown in `figure_title <#figure_DD.2-1>`__: A) the Plan Level and
B) the Beam Level.

The first level (A in the diagram) is the Plan Level. The SCU
initializes external verification of a new plan using the N-CREATE
command. The MPV then retrieves the data necessary to perform
verification through DICOM or other means. In general, there is a close
relationship between an MPV and a Treatment Management System (TMS) or
Archive. If DICOM is the protocol used to retrieve this data, this might
be done using one or more C-MOVEs on the Archive.

The second level (B in the diagram) is the Beam Level. The SCU uses the
N-SET command request to instruct the SCP on the specified Attributes to
be verified. The SCU then requests that the verification start using an
N-ACTION command. The SCP compares the values of the specified
Attributes against the values of the Attributes from the referenced
plan, and signals the status of the verification using N-EVENT-REPORT
command with the Treatment Verification Status (3008,002C) Attribute
indicating the verification result. The MPV's use of tolerance values in
the verification process shall be described in a Conformance Statement.
The SCU may then optionally request the beam's verification parameters
using an N-GET.

Finally, when all beams have been delivered or abandoned, the SCU
terminates the verification session at the Plan Level using an N-DELETE.

.. _sect_DD.3:

Machine Verification SOP Class Definitions
------------------------------------------

.. _sect_DD.3.1:

IOD Description
~~~~~~~~~~~~~~~

The Machine Verification IODs are abstractions of the information needed
to verify the correct setup of a treatment delivery system prior to
radiation treatment.

.. _sect_DD.3.2:

DIMSE Service Group
~~~~~~~~~~~~~~~~~~~

`table_title <#table_DD.3.2-1>`__ shows DIMSE Services applicable to the
IODs.

.. table:: DIMSE Service Group Applicable to Machine Verification

   ============================= =============
   DICOM Message Service Element Usage SCU/SCP
   ============================= =============
   N-CREATE                      M/M
   N-SET                         M/M
   N-GET                         M/M
   N-ACTION                      M/M
   N-DELETE                      M/M
   N-EVENT-REPORT                M/M
   ============================= =============

The meaning of the Usage SCU/SCP is described in `Usage
Specifications <#sect_H.2.4>`__.

This Section describes the behavior of the DIMSE Services that are
specific for this IOD. The general behavior of the DIMSE services is
specified in .

.. _sect_DD.3.2.1:

N-CREATE and N-SET
^^^^^^^^^^^^^^^^^^

The N-CREATE is used to create an instance of the applicable Machine
Verification SOP Class.

The N-SET is used to communicate parameters for verification to an MPV
by setting Attributes on an instance of the applicable Machine
Verification SOP Class.

All Attributes in the table relating to the number of a certain item
(e.g., Number of Wedges, Number of Control Points) specify the number in
the N-SET command. The numbering in the Beams Verification Request is
not necessarily the same as the numbering in the referenced RT Plan.

.. _sect_DD.3.2.1.1:

Attributes
''''''''''

The Attribute list of the N-CREATE and N-SET for the RT Conventional
Machine Verification SOP Class is shown in
`table_title <#table_DD.3.2.1-1>`__. See Section 5.4 for usage notation.

.. table:: N-CREATE and N-SET Attribute List - RT Conventional Machine
Verification SOP Class

   +-----------------+-------------+-----------------+-----------------+
   | Attribute Name  | Tag         | N-CREATE Usage  | N-SET Usage     |
   |                 |             | SCU/SCP         | SCU/SCP         |
   +=================+=============+=================+=================+
   | **RT General    |             |                 |                 |
   | Machine         |             |                 |                 |
   | Verification    |             |                 |                 |
   | Module**        |             |                 |                 |
   +-----------------+-------------+-----------------+-----------------+
   | Referenced RT   | (300C,0002) | 1/1             | Not allowed     |
   | Plan Sequence   |             |                 |                 |
   |                 |             | (only a single  |                 |
   |                 |             | Item shall be   |                 |
   |                 |             | permitted)      |                 |
   +-----------------+-------------+-----------------+-----------------+
   | >Referenced SOP | (0008,1150) | 1/1             | Not allowed     |
   | Class UID       |             |                 |                 |
   +-----------------+-------------+-----------------+-----------------+
   | >Referenced SOP | (0008,1155) | 1/1             | Not allowed     |
   | Instance UID    |             |                 |                 |
   +-----------------+-------------+-----------------+-----------------+
   | Referenced      | (300C,0022) | 1C/1            | Not allowed     |
   | Fraction Group  |             |                 |                 |
   | Number          |             | (required if    |                 |
   |                 |             | plan has more   |                 |
   |                 |             | than one        |                 |
   |                 |             | fraction group) |                 |
   +-----------------+-------------+-----------------+-----------------+
   | Patient ID      | (0010,0020) | 1/1             | Not allowed     |
   +-----------------+-------------+-----------------+-----------------+
   | *Include*\ `tab |             |                 |                 |
   | le_title <#tabl |             |                 |                 |
   | e_CC.2.5-2e>`__ |             |                 |                 |
   +-----------------+-------------+-----------------+-----------------+
   | Treatment       | (3008,002C) | Not allowed     | Not allowed     |
   | Verification    |             |                 |                 |
   | Status          |             |                 |                 |
   +-----------------+-------------+-----------------+-----------------+
   | Failed          | (0074,1048) | Not allowed     | Not allowed     |
   | Parameters      |             |                 |                 |
   | Sequence        |             |                 |                 |
   +-----------------+-------------+-----------------+-----------------+
   | Overridden      | (0074,104A) | Not allowed     | Not allowed     |
   | Parameters      |             |                 |                 |
   | Sequence        |             |                 |                 |
   +-----------------+-------------+-----------------+-----------------+
   | General Machine | (0074,1042) | 2/2             | 1/1             |
   | Verification    |             |                 |                 |
   | Sequence        |             | (sequence shall | (only a single  |
   |                 |             | contain zero    | Item shall be   |
   |                 |             | items)          | permitted)      |
   +-----------------+-------------+-----------------+-----------------+
   | >Specified      | (3008,0032) | -/-             | 3/3             |
   | Primary         |             |                 |                 |
   | Meterset        |             |                 |                 |
   +-----------------+-------------+-----------------+-----------------+
   | >Specified      | (3008,0033) | -/-             | 3/3             |
   | Secondary       |             |                 |                 |
   | Meterset        |             |                 |                 |
   +-----------------+-------------+-----------------+-----------------+
   | >Specified      | (3008,003A) | -/-             | 3/3             |
   | Treatment Time  |             |                 |                 |
   +-----------------+-------------+-----------------+-----------------+
   | >Beam Limiting  | (3008,00A0) | -/-             | 3/3             |
   | Device Leaf     |             |                 |                 |
   | Pairs Sequence  |             |                 |                 |
   +-----------------+-------------+-----------------+-----------------+
   | >>RT Beam       | (300A,00B8) | -/-             | 1/1             |
   | Limiting Device |             |                 |                 |
   | Type            |             |                 |                 |
   +-----------------+-------------+-----------------+-----------------+
   | >>Number of     | (300A,00BC) | -/-             | 1/1             |
   | Leaf/Jaw Pairs  |             |                 |                 |
   +-----------------+-------------+-----------------+-----------------+
   | >Recorded Wedge | (3008,00B0) | -/-             | 2C/2C           |
   | Sequence        |             |                 |                 |
   |                 |             |                 | (required if    |
   |                 |             |                 | MPV is capable  |
   |                 |             |                 | of verifying    |
   |                 |             |                 | wedges). See    |
   |                 |             |                 | `Beam           |
   |                 |             |                 | Modi            |
   |                 |             |                 | fiers <#sect_DD |
   |                 |             |                 | .3.2.1.1.1>`__. |
   +-----------------+-------------+-----------------+-----------------+
   | >>Wedge Number  | (300A,00D2) | -/-             | 1/1             |
   +-----------------+-------------+-----------------+-----------------+
   | >>Wedge ID      | (300A,00D4) | -/-             | 3/3             |
   +-----------------+-------------+-----------------+-----------------+
   | >>Wedge Angle   | (300A,00D5) | -/-             | 3/3             |
   +-----------------+-------------+-----------------+-----------------+
   | >>Wedge         | (300A,00D8) | -/-             | 3/3             |
   | Orientation     |             |                 |                 |
   +-----------------+-------------+-----------------+-----------------+
   | >>Accessory     | (300A,00F9) | -/-             | 3/3             |
   | Code            |             |                 |                 |
   +-----------------+-------------+-----------------+-----------------+
   | >Recorded       | (3008,00C0) | -/-             | 2C/2C           |
   | Compensator     |             |                 |                 |
   | Sequence        |             |                 | (required if    |
   |                 |             |                 | MPV is capable  |
   |                 |             |                 | of verifying    |
   |                 |             |                 | compensators).  |
   |                 |             |                 | See `Beam       |
   |                 |             |                 | Modi            |
   |                 |             |                 | fiers <#sect_DD |
   |                 |             |                 | .3.2.1.1.1>`__. |
   +-----------------+-------------+-----------------+-----------------+
   | >>Compensator   | (300A,00E5) | -/-             | 3/3             |
   | ID              |             |                 |                 |
   +-----------------+-------------+-----------------+-----------------+
   | >>Accessory     | (300A,00F9) | -/-             | 3/3             |
   | Code            |             |                 |                 |
   +-----------------+-------------+-----------------+-----------------+
   | >>Referenced    | (300C,00D0) | -/-             | 1/1             |
   | Compensator     |             |                 |                 |
   | Number          |             |                 |                 |
   +-----------------+-------------+-----------------+-----------------+
   | >Recorded Block | (3008,00D0) | -/-             | 2C/2C           |
   | Sequence        |             |                 |                 |
   |                 |             |                 | (required if    |
   |                 |             |                 | MPV is capable  |
   |                 |             |                 | of verifying    |
   |                 |             |                 | blocks). See    |
   |                 |             |                 | `Beam           |
   |                 |             |                 | Modi            |
   |                 |             |                 | fiers <#sect_DD |
   |                 |             |                 | .3.2.1.1.1>`__. |
   +-----------------+-------------+-----------------+-----------------+
   | >>Block Tray ID | (300A,00F5) | -/-             | 3/3             |
   +-----------------+-------------+-----------------+-----------------+
   | >>Accessory     | (300A,00F9) | -/-             | 3/3             |
   | Code            |             |                 |                 |
   +-----------------+-------------+-----------------+-----------------+
   | >>Referenced    | (300C,00E0) | -/-             | 1/1             |
   | Block Number    |             |                 |                 |
   +-----------------+-------------+-----------------+-----------------+
   | >Treatment      | (300A,00B2) | -/-             | 1/1             |
   | Machine Name    |             |                 |                 |
   +-----------------+-------------+-----------------+-----------------+
   | >Beam Name      | (300A,00C2) | -/-             | 3/3             |
   +-----------------+-------------+-----------------+-----------------+
   | >Radiation Type | (300A,00C6) | -/-             | 1/1             |
   +-----------------+-------------+-----------------+-----------------+
   | >Number of      | (300A,00D0) | -/-             | 1/1             |
   | Wedges          |             |                 |                 |
   +-----------------+-------------+-----------------+-----------------+
   | >Number of      | (300A,00E0) | -/-             | 1/1             |
   | Compensators    |             |                 |                 |
   +-----------------+-------------+-----------------+-----------------+
   | >Number of Boli | (300A,00ED) | -/-             | 1/1             |
   +-----------------+-------------+-----------------+-----------------+
   | >Number of      | (300A,00F0) | -/-             | 1/1             |
   | Blocks          |             |                 |                 |
   +-----------------+-------------+-----------------+-----------------+
   | >Applicator     | (300A,0107) | -/-             | 2C/2C           |
   | Sequence        |             |                 |                 |
   |                 |             |                 | (required if    |
   |                 |             |                 | MPV is capable  |
   |                 |             |                 | of verifying    |
   |                 |             |                 | applicators).   |
   |                 |             |                 | See `Beam       |
   |                 |             |                 | Modi            |
   |                 |             |                 | fiers <#sect_DD |
   |                 |             |                 | .3.2.1.1.1>`__. |
   +-----------------+-------------+-----------------+-----------------+
   | >>Accessory     | (300A,00F9) | -/-             | 3/3             |
   | Code            |             |                 |                 |
   +-----------------+-------------+-----------------+-----------------+
   | >>Applicator ID | (300A,0108) | -/-             | 3/3             |
   +-----------------+-------------+-----------------+-----------------+
   | >>Applicator    | (300A,0109) | -/-             | 1/1             |
   | Type            |             |                 |                 |
   +-----------------+-------------+-----------------+-----------------+
   | >Number of      | (300A,0110) | -/-             | 1/1             |
   | Control Points  |             |                 |                 |
   |                 |             |                 | (value shall be |
   |                 |             |                 | 1)              |
   +-----------------+-------------+-----------------+-----------------+
   | >Patient Setup  | (300A,0180) | -/-             | 3/3             |
   | Sequence        |             |                 |                 |
   |                 |             |                 | (one or more    |
   |                 |             |                 | Items may be    |
   |                 |             |                 | included)       |
   +-----------------+-------------+-----------------+-----------------+
   | >>Patient Setup | (300A,0182) | -/-             | 1/1             |
   | Number          |             |                 |                 |
   +-----------------+-------------+-----------------+-----------------+
   | >>Fixation      | (300A,0190) | -/-             | 2C/2C           |
   | Device Sequence |             |                 |                 |
   |                 |             |                 | (required if    |
   |                 |             |                 | MPV is capable  |
   |                 |             |                 | of verifying    |
   |                 |             |                 | fixation        |
   |                 |             |                 | devices). See   |
   |                 |             |                 | `Beam           |
   |                 |             |                 | Modi            |
   |                 |             |                 | fiers <#sect_DD |
   |                 |             |                 | .3.2.1.1.1>`__. |
   +-----------------+-------------+-----------------+-----------------+
   | >>>Accessory    | (300A,00F9) | -/-             | 3/3             |
   | Code            |             |                 |                 |
   +-----------------+-------------+-----------------+-----------------+
   | >>>Fixation     | (300A,0192) | -/-             | 1/1             |
   | Device Type     |             |                 |                 |
   +-----------------+-------------+-----------------+-----------------+
   | >Referenced     | (300C,0006) | -/-             | 1/1             |
   | Beam Number     |             |                 |                 |
   +-----------------+-------------+-----------------+-----------------+
   | >Referenced     | (300C,00B0) | -/-             | 2C/2C           |
   | Bolus Sequence  |             |                 |                 |
   |                 |             |                 | (required if    |
   |                 |             |                 | MPV is capable  |
   |                 |             |                 | of verifying    |
   |                 |             |                 | bolus). See     |
   |                 |             |                 | `Beam           |
   |                 |             |                 | Modi            |
   |                 |             |                 | fiers <#sect_DD |
   |                 |             |                 | .3.2.1.1.1>`__. |
   +-----------------+-------------+-----------------+-----------------+
   | >>Referenced    | (3006,0084) | -/-             | 1/1             |
   | ROI Number      |             |                 |                 |
   +-----------------+-------------+-----------------+-----------------+
   | >>Accessory     | (300A,00F9) | -/-             | 3/3             |
   | Code            |             |                 |                 |
   +-----------------+-------------+-----------------+-----------------+
   | *All other      | -           | -/-             | 3/3             |
   | Attributes of   |             |                 |                 |
   | the*            |             |                 |                 |
   +-----------------+-------------+-----------------+-----------------+
   | **RT            |             |                 |                 |
   | Conventional    |             |                 |                 |
   | Machine         |             |                 |                 |
   | Verification    |             |                 |                 |
   | Module**        |             |                 |                 |
   +-----------------+-------------+-----------------+-----------------+
   | Conventional    | (0074,1044) | 2/2             | 1/1             |
   | Machine         |             |                 |                 |
   | Verification    |             | (sequence shall | (only a single  |
   | Sequence        |             | contain zero    | Item shall be   |
   |                 |             | items)          | permitted)      |
   +-----------------+-------------+-----------------+-----------------+
   | >Conventional   | (0074,104C) | -/-             | 1/1             |
   | Control Point   |             |                 |                 |
   | Verification    |             |                 | (only a single  |
   | Sequence        |             |                 | Item shall be   |
   |                 |             |                 | permitted)      |
   +-----------------+-------------+-----------------+-----------------+
   | >>Nominal Beam  | (300A,0114) | -/-             | 3/3             |
   | Energy          |             |                 |                 |
   +-----------------+-------------+-----------------+-----------------+
   | >>Dose Rate Set | (300A,0115) | -/-             | 3/3             |
   +-----------------+-------------+-----------------+-----------------+
   | >>Wedge         | (300A,0116) | -/-             | 1C/1C           |
   | Position        |             |                 |                 |
   | Sequence        |             |                 | (required if    |
   |                 |             |                 | Number of       |
   |                 |             |                 | Wedges          |
   |                 |             |                 | (300A,00D0) is  |
   |                 |             |                 | non-zero,one or |
   |                 |             |                 | more Items may  |
   |                 |             |                 | be included)    |
   +-----------------+-------------+-----------------+-----------------+
   | >>>Wedge        | (300A,0118) | -/-             | 1/1             |
   | Position        |             |                 |                 |
   +-----------------+-------------+-----------------+-----------------+
   | >>>Referenced   | (300C,00C0) | -/-             | 1/1             |
   | Wedge Number    |             |                 |                 |
   +-----------------+-------------+-----------------+-----------------+
   | >>Beam Limiting | (300A,011A) | -/-             | 1C/1C           |
   | Device Position |             |                 |                 |
   | Sequence        |             |                 | (required if    |
   |                 |             |                 | Beam Limiting   |
   |                 |             |                 | Device Leaf     |
   |                 |             |                 | Pairs Sequence  |
   |                 |             |                 | (3008,00A0) is  |
   |                 |             |                 | sent,one or     |
   |                 |             |                 | more Items may  |
   |                 |             |                 | be included)    |
   +-----------------+-------------+-----------------+-----------------+
   | >>>RT Beam      | (300A,00B8) | -/-             | 1/1             |
   | Limiting Device |             |                 |                 |
   | Type            |             |                 |                 |
   +-----------------+-------------+-----------------+-----------------+
   | >>>Leaf/Jaw     | (300A,011C) | -/-             | 1/1             |
   | Positions       |             |                 |                 |
   +-----------------+-------------+-----------------+-----------------+
   | >>Gantry Angle  | (300A,011E) | -/-             | 3/3             |
   +-----------------+-------------+-----------------+-----------------+
   | >>Gantry        | (300A,011F) | -/-             | 2/2             |
   | Rotation        |             |                 |                 |
   | Direction       |             |                 |                 |
   +-----------------+-------------+-----------------+-----------------+
   | >>Beam Limiting | (300A,0120) | -/-             | 3/3             |
   | Device Angle    |             |                 |                 |
   +-----------------+-------------+-----------------+-----------------+
   | >>Beam Limiting | (300A,0121) | -/-             | 3/3             |
   | Device Rotation |             |                 |                 |
   | Direction       |             |                 |                 |
   +-----------------+-------------+-----------------+-----------------+
   | >>Patient       | (300A,0122) | -/-             | 3/3             |
   | Support Angle   |             |                 |                 |
   +-----------------+-------------+-----------------+-----------------+
   | >>Patient       | (300A,0123) | -/-             | 3/3             |
   | Support         |             |                 |                 |
   | Rotation        |             |                 |                 |
   | Direction       |             |                 |                 |
   +-----------------+-------------+-----------------+-----------------+
   | >>Table Top     | (300A,0124) | -/-             | 3/3             |
   | Eccentric Axis  |             |                 |                 |
   | Distance        |             |                 |                 |
   +-----------------+-------------+-----------------+-----------------+
   | >>Table Top     | (300A,0125) | -/-             | 3/3             |
   | Eccentric Angle |             |                 |                 |
   +-----------------+-------------+-----------------+-----------------+
   | >>Table Top     | (300A,0126) | -/-             | 3/3             |
   | Eccentric       |             |                 |                 |
   | Rotation        |             |                 |                 |
   | Direction       |             |                 |                 |
   +-----------------+-------------+-----------------+-----------------+
   | >>Table Top     | (300A,0128) | -/-             | 3/3             |
   | Vertical        |             |                 |                 |
   | Position        |             |                 |                 |
   +-----------------+-------------+-----------------+-----------------+
   | >>Table Top     | (300A,0129) | -/-             | 3/3             |
   | Longitudinal    |             |                 |                 |
   | Position        |             |                 |                 |
   +-----------------+-------------+-----------------+-----------------+
   | >>Table Top     | (300A,012A) | -/-             | 3/3             |
   | Lateral         |             |                 |                 |
   | Position        |             |                 |                 |
   +-----------------+-------------+-----------------+-----------------+
   | >>Table Top     | (300A,0140) | -/-             | 3/3             |
   | Pitch Angle     |             |                 |                 |
   +-----------------+-------------+-----------------+-----------------+
   | >>Table Top     | (300A,0142) | -/-             | 3/3             |
   | Pitch Rotation  |             |                 |                 |
   | Direction       |             |                 |                 |
   +-----------------+-------------+-----------------+-----------------+
   | >>Table Top     | (300A,0144) | -/-             | 3/3             |
   | Roll Angle      |             |                 |                 |
   +-----------------+-------------+-----------------+-----------------+
   | >>Table Top     | (300A,0146) | -/-             | 3/3             |
   | Roll Rotation   |             |                 |                 |
   | Direction       |             |                 |                 |
   +-----------------+-------------+-----------------+-----------------+
   | >>Referenced    | (300C,00F0) | -/-             | 1/1             |
   | Control Point   |             |                 |                 |
   | Index           |             |                 |                 |
   +-----------------+-------------+-----------------+-----------------+
   | *All other      | -           | -/-             | 3/3             |
   | Attributes of   |             |                 |                 |
   | the*            |             |                 |                 |
   +-----------------+-------------+-----------------+-----------------+

The Attribute list of the N-CREATE and N-SET for the RT Ion Machine
Verification SOP Class is shown in `table_title <#table_DD.3.2.1-2>`__.

.. table:: N-CREATE and N-SET Attribute List - RT Ion Machine
Verification SOP Class

   +-----------------+-------------+-----------------+-----------------+
   | Attribute Name  | Tag         | N-CREATE Usage  | N-SET Usage     |
   |                 |             | SCU/SCP         | SCU/SCP         |
   +=================+=============+=================+=================+
   | **RT General    |             |                 |                 |
   | Machine         |             |                 |                 |
   | Verification    |             |                 |                 |
   | Module**        |             |                 |                 |
   +-----------------+-------------+-----------------+-----------------+
   | Referenced RT   | (300C,0002) | 1/1             | Not allowed     |
   | Plan Sequence   |             |                 |                 |
   |                 |             | (only a single  |                 |
   |                 |             | Item shall be   |                 |
   |                 |             | permitted)      |                 |
   +-----------------+-------------+-----------------+-----------------+
   | >Referenced SOP | (0008,1150) | 1/1             | Not allowed     |
   | Class UID       |             |                 |                 |
   +-----------------+-------------+-----------------+-----------------+
   | >Referenced SOP | (0008,1155) | 1/1             | Not allowed     |
   | Instance UID    |             |                 |                 |
   +-----------------+-------------+-----------------+-----------------+
   | Referenced      | (300C,0022) | 1C/1            | Not allowed     |
   | Fraction Group  |             |                 |                 |
   | Number          |             | (required if    |                 |
   |                 |             | plan has more   |                 |
   |                 |             | than one        |                 |
   |                 |             | fraction group) |                 |
   +-----------------+-------------+-----------------+-----------------+
   | Patient ID      | (0010,0020) | 1/1             | Not allowed     |
   +-----------------+-------------+-----------------+-----------------+
   | *Include*\ `tab |             |                 |                 |
   | le_title <#tabl |             |                 |                 |
   | e_CC.2.5-2e>`__ |             |                 |                 |
   +-----------------+-------------+-----------------+-----------------+
   | Treatment       | (3008,002C) | Not allowed     | Not allowed     |
   | Verification    |             |                 |                 |
   | Status          |             |                 |                 |
   +-----------------+-------------+-----------------+-----------------+
   | Failed          | (0074,1048) | Not allowed     | Not allowed     |
   | Parameters      |             |                 |                 |
   | Sequence        |             |                 |                 |
   +-----------------+-------------+-----------------+-----------------+
   | Overridden      | (0074,104A) | Not allowed     | Not allowed     |
   | Parameters      |             |                 |                 |
   | Sequence        |             |                 |                 |
   +-----------------+-------------+-----------------+-----------------+
   | General Machine | (0074,1042) | 2/2             | 1/1             |
   | Verification    |             |                 |                 |
   | Sequence        |             | (sequence shall | (only a single  |
   |                 |             | contain zero    | Item shall be   |
   |                 |             | items)          | permitted)      |
   +-----------------+-------------+-----------------+-----------------+
   | >Specified      | (3008,0032) | -/-             | 3/3             |
   | Primary         |             |                 |                 |
   | Meterset        |             |                 |                 |
   +-----------------+-------------+-----------------+-----------------+
   | >Specified      | (3008,0033) | -/-             | 3/3             |
   | Secondary       |             |                 |                 |
   | Meterset        |             |                 |                 |
   +-----------------+-------------+-----------------+-----------------+
   | >Specified      | (3008,003A) | -/-             | 3/3             |
   | Treatment Time  |             |                 |                 |
   +-----------------+-------------+-----------------+-----------------+
   | >Beam Limiting  | (3008,00A0) | -/-             | 3/3             |
   | Device Leaf     |             |                 |                 |
   | Pairs Sequence  |             |                 | See `Beam       |
   |                 |             |                 | Modi            |
   |                 |             |                 | fiers <#sect_DD |
   |                 |             |                 | .3.2.1.1.1>`__. |
   +-----------------+-------------+-----------------+-----------------+
   | >>RT Beam       | (300A,00B8) | -/-             | 1/1             |
   | Limiting Device |             |                 |                 |
   | Type            |             |                 |                 |
   +-----------------+-------------+-----------------+-----------------+
   | >>Number of     | (300A,00BC) | -/-             | 1/1             |
   | Leaf/Jaw Pairs  |             |                 |                 |
   +-----------------+-------------+-----------------+-----------------+
   | >Recorded Wedge | (3008,00B0) | -/-             | 2C/2C           |
   | Sequence        |             |                 |                 |
   |                 |             |                 | (required if    |
   |                 |             |                 | MPV is capable  |
   |                 |             |                 | of verifying    |
   |                 |             |                 | wedges). See    |
   |                 |             |                 | `Beam           |
   |                 |             |                 | Modi            |
   |                 |             |                 | fiers <#sect_DD |
   |                 |             |                 | .3.2.1.1.1>`__. |
   +-----------------+-------------+-----------------+-----------------+
   | >>Wedge Number  | (300A,00D2) | -/-             | 1/1             |
   +-----------------+-------------+-----------------+-----------------+
   | >>Wedge ID      | (300A,00D4) | -/-             | 3/3             |
   +-----------------+-------------+-----------------+-----------------+
   | >>Wedge Angle   | (300A,00D5) | -/-             | 3/3             |
   +-----------------+-------------+-----------------+-----------------+
   | >>Wedge         | (300A,00D8) | -/-             | 3/3             |
   | Orientation     |             |                 |                 |
   +-----------------+-------------+-----------------+-----------------+
   | >>Accessory     | (300A,00F9) | -/-             | 3/3             |
   | Code            |             |                 |                 |
   +-----------------+-------------+-----------------+-----------------+
   | >Recorded       | (3008,00C0) | -/-             | 2C/2C           |
   | Compensator     |             |                 |                 |
   | Sequence        |             |                 | (required if    |
   |                 |             |                 | MPV is capable  |
   |                 |             |                 | of verifying    |
   |                 |             |                 | compensators).  |
   |                 |             |                 | See `Beam       |
   |                 |             |                 | Modi            |
   |                 |             |                 | fiers <#sect_DD |
   |                 |             |                 | .3.2.1.1.1>`__. |
   +-----------------+-------------+-----------------+-----------------+
   | >>Compensator   | (300A,00E5) | -/-             | 3/3             |
   | ID              |             |                 |                 |
   +-----------------+-------------+-----------------+-----------------+
   | >>Accessory     | (300A,00F9) | -/-             | 3/3             |
   | Code            |             |                 |                 |
   +-----------------+-------------+-----------------+-----------------+
   | >>Referenced    | (300C,00D0) | -/-             | 1/1             |
   | Compensator     |             |                 |                 |
   | Number          |             |                 |                 |
   +-----------------+-------------+-----------------+-----------------+
   | >Recorded Block | (3008,00D0) | -/-             | 2C/2C           |
   | Sequence        |             |                 |                 |
   |                 |             |                 | (required if    |
   |                 |             |                 | MPV is capable  |
   |                 |             |                 | of verifying    |
   |                 |             |                 | blocks). See    |
   |                 |             |                 | `Beam           |
   |                 |             |                 | Modi            |
   |                 |             |                 | fiers <#sect_DD |
   |                 |             |                 | .3.2.1.1.1>`__. |
   +-----------------+-------------+-----------------+-----------------+
   | >>Block Tray ID | (300A,00F5) | -/-             | 3/3             |
   +-----------------+-------------+-----------------+-----------------+
   | >>Accessory     | (300A,00F9) | -/-             | 3/3             |
   | Code            |             |                 |                 |
   +-----------------+-------------+-----------------+-----------------+
   | >>Referenced    | (300C,00E0) | -/-             | 1/1             |
   | Block Number    |             |                 |                 |
   +-----------------+-------------+-----------------+-----------------+
   | >Treatment      | (300A,00B2) | -/-             | 1/1             |
   | Machine Name    |             |                 |                 |
   +-----------------+-------------+-----------------+-----------------+
   | >Beam Name      | (300A,00C2) | -/-             | 3/3             |
   +-----------------+-------------+-----------------+-----------------+
   | >Radiation Type | (300A,00C6) | -/-             | 1/1             |
   +-----------------+-------------+-----------------+-----------------+
   | >Number of      | (300A,00D0) | -/-             | 1/1             |
   | Wedges          |             |                 |                 |
   +-----------------+-------------+-----------------+-----------------+
   | >Number of      | (300A,00E0) | -/-             | 1/1             |
   | Compensators    |             |                 |                 |
   +-----------------+-------------+-----------------+-----------------+
   | >Number of Boli | (300A,00ED) | -/-             | 1/1             |
   +-----------------+-------------+-----------------+-----------------+
   | >Number of      | (300A,00F0) | -/-             | 1/1             |
   | Blocks          |             |                 |                 |
   +-----------------+-------------+-----------------+-----------------+
   | >Applicator     | (300A,0107) | -/-             | 2C/2C           |
   | Sequence        |             |                 |                 |
   |                 |             |                 | (required if    |
   |                 |             |                 | MPV is capable  |
   |                 |             |                 | of verifying    |
   |                 |             |                 | applicators).   |
   |                 |             |                 | See `Beam       |
   |                 |             |                 | Modi            |
   |                 |             |                 | fiers <#sect_DD |
   |                 |             |                 | .3.2.1.1.1>`__. |
   +-----------------+-------------+-----------------+-----------------+
   | >>Accessory     | (300A,00F9) | -/-             | 3/3             |
   | Code            |             |                 |                 |
   +-----------------+-------------+-----------------+-----------------+
   | >>Applicator ID | (300A,0108) | -/-             | 3/3             |
   +-----------------+-------------+-----------------+-----------------+
   | >>Applicator    | (300A,0109) | -/-             | 1/1             |
   | Type            |             |                 |                 |
   +-----------------+-------------+-----------------+-----------------+
   | >Number of      | (300A,0110) | -/-             | 1/1             |
   | Control Points  |             |                 |                 |
   |                 |             |                 | (value shall be |
   |                 |             |                 | 1)              |
   +-----------------+-------------+-----------------+-----------------+
   | >Patient Setup  | (300A,0180) | -/-             | 3/3             |
   | Sequence        |             |                 |                 |
   |                 |             |                 | See `Beam       |
   |                 |             |                 | Modi            |
   |                 |             |                 | fiers <#sect_DD |
   |                 |             |                 | .3.2.1.1.1>`__. |
   +-----------------+-------------+-----------------+-----------------+
   | >>Patient Setup | (300A,0182) | -/-             | 1/1             |
   | Number          |             |                 |                 |
   +-----------------+-------------+-----------------+-----------------+
   | >>Fixation      | (300A,0190) | -/-             | 2C/2C           |
   | Device Sequence |             |                 |                 |
   |                 |             |                 | (required if    |
   |                 |             |                 | MPV is capable  |
   |                 |             |                 | of verifying    |
   |                 |             |                 | fixation        |
   |                 |             |                 | devices). See   |
   |                 |             |                 | `Beam           |
   |                 |             |                 | Modi            |
   |                 |             |                 | fiers <#sect_DD |
   |                 |             |                 | .3.2.1.1.1>`__. |
   +-----------------+-------------+-----------------+-----------------+
   | >>>Accessory    | (300A,00F9) | -/-             | 3/3             |
   | Code            |             |                 |                 |
   +-----------------+-------------+-----------------+-----------------+
   | >>>Fixation     | (300A,0192) | -/-             | 1/1             |
   | Device Type     |             |                 |                 |
   +-----------------+-------------+-----------------+-----------------+
   | >Referenced     | (300C,0006) | -/-             | 1/1             |
   | Beam Number     |             |                 |                 |
   +-----------------+-------------+-----------------+-----------------+
   | >Referenced     | (300C,00B0) | -/-             | 2C/2C           |
   | Bolus Sequence  |             |                 |                 |
   |                 |             |                 | (required if    |
   |                 |             |                 | MPV is capable  |
   |                 |             |                 | of verifying    |
   |                 |             |                 | bolus). See     |
   |                 |             |                 | `Beam           |
   |                 |             |                 | Modi            |
   |                 |             |                 | fiers <#sect_DD |
   |                 |             |                 | .3.2.1.1.1>`__. |
   +-----------------+-------------+-----------------+-----------------+
   | >>Referenced    | (3006,0084) | -/-             | 1/1             |
   | ROI Number      |             |                 |                 |
   +-----------------+-------------+-----------------+-----------------+
   | >>Accessory     | (300A,00F9) | -/-             | 3/3             |
   | Code            |             |                 |                 |
   +-----------------+-------------+-----------------+-----------------+
   | *All other      | -           | -/-             | 3/3             |
   | Attributes of   |             |                 |                 |
   | the*            |             |                 |                 |
   +-----------------+-------------+-----------------+-----------------+
   | **RT Ion        |             |                 |                 |
   | Machine         |             |                 |                 |
   | Verification    |             |                 |                 |
   | Module**        |             |                 |                 |
   +-----------------+-------------+-----------------+-----------------+
   | Ion Machine     | (0074,1046) | 2/2             | 1/1             |
   | Verification    |             |                 |                 |
   | Sequence        |             | (sequence shall | (only a single  |
   |                 |             | contain zero    | Item shall be   |
   |                 |             | items)          | permitted)      |
   +-----------------+-------------+-----------------+-----------------+
   | >Ion Control    | (0074,104E) | -/-             | 1/1             |
   | Point           |             |                 |                 |
   | Verification    |             |                 | (only a single  |
   | Sequence        |             |                 | Item shall be   |
   |                 |             |                 | permitted)      |
   +-----------------+-------------+-----------------+-----------------+
   | >>Meterset Rate | (3008,0045) | -/-             | 3/3             |
   | Set             |             |                 |                 |
   +-----------------+-------------+-----------------+-----------------+
   | >>Nominal Beam  | (300A,0114) | -/-             | 3/3             |
   | Energy          |             |                 |                 |
   +-----------------+-------------+-----------------+-----------------+
   | >>Beam Limiting | (300A,011A) | -/-             | 1C/1C           |
   | Device Position |             |                 |                 |
   | Sequence        |             |                 | (required if    |
   |                 |             |                 | Beam Limiting   |
   |                 |             |                 | Device Leaf     |
   |                 |             |                 | Pairs Sequence  |
   |                 |             |                 | (3008,00A0) is  |
   |                 |             |                 | sent,one or     |
   |                 |             |                 | more Items may  |
   |                 |             |                 | be included)    |
   +-----------------+-------------+-----------------+-----------------+
   | >>>RT Beam      | (300A,00B8) | -/-             | 1/1             |
   | Limiting Device |             |                 |                 |
   | Type            |             |                 |                 |
   +-----------------+-------------+-----------------+-----------------+
   | >>>Leaf/Jaw     | (300A,011C) | -/-             | 1/1             |
   | Positions       |             |                 |                 |
   +-----------------+-------------+-----------------+-----------------+
   | >>Gantry Angle  | (300A,011E) | -/-             | 3/3             |
   +-----------------+-------------+-----------------+-----------------+
   | >>Gantry        | (300A,011F) | -/-             | 2/2             |
   | Rotation        |             |                 |                 |
   | Direction       |             |                 |                 |
   +-----------------+-------------+-----------------+-----------------+
   | >>Beam Limiting | (300A,0120) | -/-             | 3/3             |
   | Device Angle    |             |                 |                 |
   +-----------------+-------------+-----------------+-----------------+
   | >>Beam Limiting | (300A,0121) | -/-             | 3/3             |
   | Device Rotation |             |                 |                 |
   | Direction       |             |                 |                 |
   +-----------------+-------------+-----------------+-----------------+
   | >>Patient       | (300A,0122) | -/-             | 3/3             |
   | Support Angle   |             |                 |                 |
   +-----------------+-------------+-----------------+-----------------+
   | >>Patient       | (300A,0123) | -/-             | 3/3             |
   | Support         |             |                 |                 |
   | Rotation        |             |                 |                 |
   | Direction       |             |                 |                 |
   +-----------------+-------------+-----------------+-----------------+
   | >>Table Top     | (300A,0128) | -/-             | 3/3             |
   | Vertical        |             |                 |                 |
   | Position        |             |                 |                 |
   +-----------------+-------------+-----------------+-----------------+
   | >>Table Top     | (300A,0129) | -/-             | 3/3             |
   | Longitudinal    |             |                 |                 |
   | Position        |             |                 |                 |
   +-----------------+-------------+-----------------+-----------------+
   | >>Table Top     | (300A,012A) | -/-             | 3/3             |
   | Lateral         |             |                 |                 |
   | Position        |             |                 |                 |
   +-----------------+-------------+-----------------+-----------------+
   | >>Table Top     | (300A,0140) | -/-             | 3/3             |
   | Pitch Angle     |             |                 |                 |
   +-----------------+-------------+-----------------+-----------------+
   | >>Table Top     | (300A,0142) | -/-             | 3/3             |
   | Pitch Rotation  |             |                 |                 |
   | Direction       |             |                 |                 |
   +-----------------+-------------+-----------------+-----------------+
   | >>Table Top     | (300A,0144) | -/-             | 3/3             |
   | Roll Angle      |             |                 |                 |
   +-----------------+-------------+-----------------+-----------------+
   | >>Table Top     | (300A,0146) | -/-             | 3/3             |
   | Roll Rotation   |             |                 |                 |
   | Direction       |             |                 |                 |
   +-----------------+-------------+-----------------+-----------------+
   | >>Head Fixation | (300A,0148) | -/-             | 3/3             |
   | Angle           |             |                 |                 |
   +-----------------+-------------+-----------------+-----------------+
   | >>Gantry Pitch  | (300A,014A) | -/-             | 3/3             |
   | Angle           |             |                 |                 |
   +-----------------+-------------+-----------------+-----------------+
   | >>Gantry Pitch  | (300A,014C) | -/-             | 3/3             |
   | Rotation        |             |                 |                 |
   | Direction       |             |                 |                 |
   +-----------------+-------------+-----------------+-----------------+
   | >>Snout         | (300A,030D) | -/-             | 3/3             |
   | Position        |             |                 |                 |
   +-----------------+-------------+-----------------+-----------------+
   | >>Range Shifter | (300A,0360) | -/-             | 1C/1C           |
   | Settings        |             |                 |                 |
   | Sequence        |             |                 | (required if    |
   |                 |             |                 | Number of Range |
   |                 |             |                 | Shifters        |
   |                 |             |                 | (300A,0312) is  |
   |                 |             |                 | non-zero,one or |
   |                 |             |                 | more Items may  |
   |                 |             |                 | be included)    |
   +-----------------+-------------+-----------------+-----------------+
   | >>>Range        | (300A,0362) | -/-             | 1/1             |
   | Shifter Setting |             |                 |                 |
   +-----------------+-------------+-----------------+-----------------+
   | >>>Referenced   | (300C,0100) | -/-             | 1/1             |
   | Range Shifter   |             |                 |                 |
   | Number          |             |                 |                 |
   +-----------------+-------------+-----------------+-----------------+
   | >>Lateral       | (300A,0370) | -/-             | 1C/1C           |
   | Spreading       |             |                 |                 |
   | Device Settings |             |                 | (required if    |
   | Sequence        |             |                 | Number of       |
   |                 |             |                 | Lateral         |
   |                 |             |                 | Spreading       |
   |                 |             |                 | Devices         |
   |                 |             |                 | (300A,0330) is  |
   |                 |             |                 | non-zero,one or |
   |                 |             |                 | more Items may  |
   |                 |             |                 | be included)    |
   +-----------------+-------------+-----------------+-----------------+
   | >>>Lateral      | (300A,0372) | -/-             | 1/1             |
   | Spreading       |             |                 |                 |
   | Device Setting  |             |                 |                 |
   +-----------------+-------------+-----------------+-----------------+
   | >>>Referenced   | (300C,0102) | -/-             | 1/1             |
   | Lateral         |             |                 |                 |
   | Spreading       |             |                 |                 |
   | Device Number   |             |                 |                 |
   +-----------------+-------------+-----------------+-----------------+
   | >>Range         | (300A,0380) | -/-             | 1C/1C           |
   | Modulator       |             |                 |                 |
   | Settings        |             |                 | (required if    |
   | Sequence        |             |                 | Number of Range |
   |                 |             |                 | Modulators      |
   |                 |             |                 | (300A,0340) is  |
   |                 |             |                 | non-zero,one or |
   |                 |             |                 | more Items may  |
   |                 |             |                 | be included)    |
   +-----------------+-------------+-----------------+-----------------+
   | >>>Range        | (300A,0382) | -/-             | 1/1             |
   | Modulator       |             |                 |                 |
   | Gating Start    |             |                 |                 |
   | Value           |             |                 |                 |
   +-----------------+-------------+-----------------+-----------------+
   | >>>Range        | (300A,0384) | -/-             | 1/1             |
   | Modulator       |             |                 |                 |
   | Gating Stop     |             |                 |                 |
   | Value           |             |                 |                 |
   +-----------------+-------------+-----------------+-----------------+
   | >>>Referenced   | (300C,0104) | -/-             | 1/1             |
   | Range Modulator |             |                 |                 |
   | Number          |             |                 |                 |
   +-----------------+-------------+-----------------+-----------------+
   | >>Ion Wedge     | (300A,03AC) | -/-             | 1C/1C           |
   | Position        |             |                 |                 |
   | Sequence        |             |                 | (required if    |
   |                 |             |                 | Number of       |
   |                 |             |                 | Wedges          |
   |                 |             |                 | (300A,00D0) is  |
   |                 |             |                 | non-zero,one or |
   |                 |             |                 | more Items may  |
   |                 |             |                 | be included)    |
   +-----------------+-------------+-----------------+-----------------+
   | >>>Wedge Thin   | (300A,00DB) | -/-             | 1C/1C           |
   | Edge Position   |             |                 |                 |
   |                 |             |                 | (required if    |
   |                 |             |                 | Wedge Type      |
   |                 |             |                 | (300A,00D3) of  |
   |                 |             |                 | the wedge       |
   |                 |             |                 | referenced by   |
   |                 |             |                 | Referenced      |
   |                 |             |                 | Wedge Number    |
   |                 |             |                 | (300C,00C0) is  |
   |                 |             |                 | P               |
   |                 |             |                 | ARTIAL_STANDARD |
   |                 |             |                 | or              |
   |                 |             |                 | P               |
   |                 |             |                 | ARTIAL_MOTORIZ) |
   +-----------------+-------------+-----------------+-----------------+
   | >>>Wedge        | (300A,0118) | -/-             | 1/1             |
   | Position        |             |                 |                 |
   +-----------------+-------------+-----------------+-----------------+
   | >>Referenced    | (300C,00F0) | -/-             | 1/1             |
   | Control Point   |             |                 |                 |
   | Index           |             |                 |                 |
   +-----------------+-------------+-----------------+-----------------+
   | >Recorded Snout | (3008,00F0) | -/-             | 1C/1C           |
   | Sequence        |             |                 |                 |
   |                 |             |                 | (required if    |
   |                 |             |                 | Snout Sequence  |
   |                 |             |                 | is included in  |
   |                 |             |                 | the RT Ion Plan |
   |                 |             |                 | referenced      |
   |                 |             |                 | within the      |
   |                 |             |                 | Referenced RT   |
   |                 |             |                 | Plan Sequence   |
   |                 |             |                 | (300C,0002);    |
   |                 |             |                 | only a single   |
   |                 |             |                 | Item is         |
   |                 |             |                 | permitted in    |
   |                 |             |                 | this sequence)  |
   +-----------------+-------------+-----------------+-----------------+
   | >>Accessory     | (300A,00F9) | -/-             | 3/3             |
   | Code            |             |                 |                 |
   +-----------------+-------------+-----------------+-----------------+
   | >>Snout ID      | (300A,030F) | -/-             | 3/3             |
   +-----------------+-------------+-----------------+-----------------+
   | >Recorded Range | (3008,00F2) | -/-             | 2C/2C           |
   | Shifter         |             |                 |                 |
   | Sequence        |             |                 | (required if    |
   |                 |             |                 | MPV is capable  |
   |                 |             |                 | of verifying    |
   |                 |             |                 | range           |
   |                 |             |                 | shifters). See  |
   |                 |             |                 | `Beam           |
   |                 |             |                 | Modi            |
   |                 |             |                 | fiers <#sect_DD |
   |                 |             |                 | .3.2.1.1.1>`__. |
   +-----------------+-------------+-----------------+-----------------+
   | >>Accessory     | (300A,00F9) | -/-             | 3/3             |
   | Code            |             |                 |                 |
   +-----------------+-------------+-----------------+-----------------+
   | >>Range Shifter | (300A,0318) | -/-             | 3/3             |
   | ID              |             |                 |                 |
   +-----------------+-------------+-----------------+-----------------+
   | >>Referenced    | (300C,0100) | -/-             | 1/1             |
   | Range Shifter   |             |                 |                 |
   | Number          |             |                 |                 |
   +-----------------+-------------+-----------------+-----------------+
   | >Recorded       | (3008,00F4) | -/-             | 2C/2C           |
   | Lateral         |             |                 |                 |
   | Spreading       |             |                 | (required if    |
   | Device Sequence |             |                 | MPV is capable  |
   |                 |             |                 | of verifying    |
   |                 |             |                 | lateral         |
   |                 |             |                 | spreading       |
   |                 |             |                 | devices). See   |
   |                 |             |                 | `Beam           |
   |                 |             |                 | Modi            |
   |                 |             |                 | fiers <#sect_DD |
   |                 |             |                 | .3.2.1.1.1>`__. |
   +-----------------+-------------+-----------------+-----------------+
   | >>Accessory     | (300A,00F9) | -/-             | 3/3             |
   | Code            |             |                 |                 |
   +-----------------+-------------+-----------------+-----------------+
   | >>Lateral       | (300A,0336) | -/-             | 3/3             |
   | Spreading       |             |                 |                 |
   | Device ID       |             |                 |                 |
   +-----------------+-------------+-----------------+-----------------+
   | >>Referenced    | (300C,0102) | -/-             | 1/1             |
   | Lateral         |             |                 |                 |
   | Spreading       |             |                 |                 |
   | Device Number   |             |                 |                 |
   +-----------------+-------------+-----------------+-----------------+
   | >Recorded Range | (3008,00F6) | -/-             | 2C/2C           |
   | Modulator       |             |                 |                 |
   | Sequence        |             |                 | (required if    |
   |                 |             |                 | MPV is capable  |
   |                 |             |                 | of verifying    |
   |                 |             |                 | range           |
   |                 |             |                 | modulators).    |
   |                 |             |                 | See `Beam       |
   |                 |             |                 | Modi            |
   |                 |             |                 | fiers <#sect_DD |
   |                 |             |                 | .3.2.1.1.1>`__. |
   +-----------------+-------------+-----------------+-----------------+
   | >>Accessory     | (300A,00F9) | -/-             | 3/3             |
   | Code            |             |                 |                 |
   +-----------------+-------------+-----------------+-----------------+
   | >>Range         | (300A,0346) | -/-             | 3/3             |
   | Modulator ID    |             |                 |                 |
   +-----------------+-------------+-----------------+-----------------+
   | >>Range         | (300A,0348) | -/-             | 1/1             |
   | Modulator Type  |             |                 |                 |
   +-----------------+-------------+-----------------+-----------------+
   | >>Beam Current  | (300A,034C) | -/-             | 1C/1C           |
   | Modulation ID   |             |                 |                 |
   |                 |             |                 | (required if    |
   |                 |             |                 | Range Modulator |
   |                 |             |                 | Type            |
   |                 |             |                 | (300A,0348) is  |
   |                 |             |                 | WHL_MODWEIGHTS) |
   +-----------------+-------------+-----------------+-----------------+
   | >>Referenced    | (300C,0104) | -/-             | 1/1             |
   | Range Modulator |             |                 |                 |
   | Number          |             |                 |                 |
   +-----------------+-------------+-----------------+-----------------+
   | >Radiation Mass | (300A,0302) | -/-             | 1C/1C           |
   | Number          |             |                 |                 |
   |                 |             |                 | (required if    |
   |                 |             |                 | Radiation Type  |
   |                 |             |                 | (300A,00C6) is  |
   |                 |             |                 | ION)            |
   +-----------------+-------------+-----------------+-----------------+
   | >Radiation      | (300A,0304) | -/-             | 1C/1C           |
   | Atomic Number   |             |                 |                 |
   |                 |             |                 | (required if    |
   |                 |             |                 | Radiation Type  |
   |                 |             |                 | (300A,00C6) is  |
   |                 |             |                 | ION)            |
   +-----------------+-------------+-----------------+-----------------+
   | >Radiation      | (300A,0306) | -/-             | 1C/1C           |
   | Charge State    |             |                 |                 |
   |                 |             |                 | (required if    |
   |                 |             |                 | Radiation Type  |
   |                 |             |                 | (300A,00C6) is  |
   |                 |             |                 | ION)            |
   +-----------------+-------------+-----------------+-----------------+
   | >Scan Mode      | (300A,0308) | -/-             | 1/1             |
   +-----------------+-------------+-----------------+-----------------+
   | >Number of      | (300A,0312) | -/-             | 1/1             |
   | Range Shifters  |             |                 |                 |
   +-----------------+-------------+-----------------+-----------------+
   | >Number of      | (300A,0330) | -/-             | 1/1             |
   | Lateral         |             |                 |                 |
   | Spreading       |             |                 |                 |
   | Devices         |             |                 |                 |
   +-----------------+-------------+-----------------+-----------------+
   | >Number of      | (300A,0340) | -/-             | 1/1             |
   | Range           |             |                 |                 |
   | Modulators      |             |                 |                 |
   +-----------------+-------------+-----------------+-----------------+
   | >Patient        | (300A,0350) | -/-             | 3/3             |
   | Support Type    |             |                 |                 |
   +-----------------+-------------+-----------------+-----------------+
   | >Patient        | (300A,0352) | -/-             | 3/3             |
   | Support ID      |             |                 |                 |
   +-----------------+-------------+-----------------+-----------------+
   | >Patient        | (300A,0354) | -/-             | 3/3             |
   | Support         |             |                 |                 |
   | Accessory Code  |             |                 |                 |
   +-----------------+-------------+-----------------+-----------------+
   | >Fixation Light | (300A,0356) | -/-             | 3/3             |
   | Azimuthal Angle |             |                 |                 |
   +-----------------+-------------+-----------------+-----------------+
   | >Fixation Light | (300A,0358) | -/-             | 3/3             |
   | Polar Angle     |             |                 |                 |
   +-----------------+-------------+-----------------+-----------------+
   | *All other      | -           | -/-             | 3/3             |
   | Attributes of   |             |                 |                 |
   | the*            |             |                 |                 |
   +-----------------+-------------+-----------------+-----------------+

.. _sect_DD.3.2.1.1.1:

Beam Modifiers
              

If the MPV is not capable of performing the type of verification
required by the Attribute, then the Attribute shall not be present. If
the MPV is capable of performing the type of verification required by
the Attribute, then the Attribute will be zero length if there are no
such modifiers, and valued with one or more items if there are one or
more such modifiers.

.. _sect_DD.3.2.1.2:

Status
''''''

`table_title <#table_DD.3.2.1.2-1>`__ defines the status code values
that might be returned in a N-CREATE response. General status code
values and fields related to status code values are defined for N-CREATE
DIMSE Service in .

.. table:: RT Ion Machine Verification SOP Class N-CREATE Status Values

   +--------------------------+--------------------------+-------------+
   | Service Status           | Further Meaning          | Status Code |
   +==========================+==========================+=============+
   | Success                  | Machine Verification     | 0000        |
   |                          | successfully created     |             |
   +--------------------------+--------------------------+-------------+
   | Failure                  | Failed: No such object   | C227        |
   |                          | instance - Referenced RT |             |
   |                          | Plan not found           |             |
   +--------------------------+--------------------------+-------------+
   | Failed: The Referenced   | C221                     |             |
   | Fraction Group Number    |                          |             |
   | does not exist in the    |                          |             |
   | referenced plan          |                          |             |
   +--------------------------+--------------------------+-------------+
   | Failed: No beams exist   | C222                     |             |
   | within the referenced    |                          |             |
   | fraction group           |                          |             |
   +--------------------------+--------------------------+-------------+
   | Failed: SCU already      | C223                     |             |
   | verifying and cannot     |                          |             |
   | currently process this   |                          |             |
   | request.                 |                          |             |
   +--------------------------+--------------------------+-------------+

The status values for N-SET that are specific for these SOP Classes are
defined as follows:

.. table:: RT Ion Machine Verification SOP Class N-SET Status Values

   +------------------------------+------------------------------+------+
   | Status                       | Meaning                      | Code |
   +==============================+==============================+======+
   | Success                      | Machine Verification         | 0000 |
   |                              | successfully updated         |      |
   +------------------------------+------------------------------+------+
   | Failure                      | Failed: Referenced Beam      | C224 |
   |                              | Number not found within the  |      |
   |                              | referenced Fraction Group    |      |
   +------------------------------+------------------------------+------+
   | Failed: Referenced device or | C225                         |      |
   | accessory not supported      |                              |      |
   +------------------------------+------------------------------+------+
   | Failed: Referenced device or | C226                         |      |
   | accessory not found within   |                              |      |
   | the referenced beam          |                              |      |
   +------------------------------+------------------------------+------+

.. _sect_DD.3.2.1.3:

Behavior
''''''''

.. _sect_DD.3.2.1.3.1:

N-CREATE
        

The SCU uses N-CREATE to request the SCP to create an applicable Machine
Verification SOP Instance. The SCP shall create the SOP Instance and
shall initialize Attributes of the SOP Class.

The General Machine Verification Sequence, Conventional Machine
Verification Sequence, and Ion Machine Verification Sequence are created
with an empty value, and specification of the contained Attributes is
deferred until the N-SET operation.

The SCP shall return the status code of the requested SOP Instance
creation. The meaning of success, warning and failure status codes is
defined in `Status <#sect_DD.3.2.1.2>`__.

.. _sect_DD.3.2.1.3.2:

N-SET
     

The SCU uses the N-SET to request the SCP to update an applicable
Machine Verification instance. The SCU shall specify the SOP Instance to
be updated and shall specify the list of Attributes for which the
Attribute Values are to be set. The Attributes in the Conventional/Ion
Control Point Verification Sequence represent the Treatment Delivery
System's actual geometric values at the time the N-SET request is issued
and therefore, the Conventional/Ion Control Point Verification Sequence
shall always contain one sequence item. The Referenced Control Point
Index shall be zero for NORMAL treatments, and may be greater than zero
for CONTINUATION treatments.

Within an Attribute sequence such as the General Machine Verification
Sequence, Conventional Machine Verification Sequence, and Ion Machine
Verification Sequence, values for all required Attributes must be
supplied with each N-SET, or else the missing Attributes will have any
previously set values removed from the SOP Instance. Existing parameters
may be cleared by sending an empty sequence or Attribute. The MPV's
Conformance Statement shall specify the set of Attributes that it
requires for verification.

The SCU shall set the new values for the specified Attributes of the
specified SOP Instance. The SCP shall then compare the values of
Attributes of the specified SOP Instance to the values of the same
Attributes found in the RT Plan referenced in N-CREATE. Values shall be
compared using the tolerance values also found in the referenced RT
Plan. The result of this comparison shall be available for use when the
SCU requests the Treatment Verification Status using an N-GET.

.. _sect_DD.3.2.2:

N-GET
^^^^^

The N-GET is used to get the verification status and results of the
applicable Machine Verification SOP Class.

.. _sect_DD.3.2.2.1Verification:

Parameters Selector Attribute Macro
'''''''''''''''''''''''''''''''''''

`table_title <#table_DD.3.2.2.1-1>`__ describes N-GET support
requirements for the Selector Attribute Macro. See Section 5.4 for
requirements type code meaning.

.. table:: Verification Parameters Selector Attribute Macro

   +--------------------------+-------------+--------------------------+
   | Attribute Name           | Tag         | Req. Type N-GET          |
   |                          |             | (SCU/SCP)                |
   +==========================+=============+==========================+
   | Selector Attribute       | (0072,0026) | -/1                      |
   +--------------------------+-------------+--------------------------+
   | Selector Value Number    | (0072,0028) | -/1                      |
   +--------------------------+-------------+--------------------------+
   | Selector Sequence        | (0072,0052) | -/1                      |
   | Pointer                  |             |                          |
   +--------------------------+-------------+--------------------------+
   | Selector Sequence        | (0072,0054) | -/1                      |
   | Pointer Private Creator  |             |                          |
   +--------------------------+-------------+--------------------------+
   | Selector Sequence        | (0074,1057) | -/1                      |
   | Pointer Items            |             |                          |
   +--------------------------+-------------+--------------------------+
   | Selector Attribute       | (0072,0056) | -/1                      |
   | Private Creator          |             |                          |
   +--------------------------+-------------+--------------------------+

.. _sect_DD.3.2.2.2:

Attributes
''''''''''

The Attribute list of the N-GET for the RT Conventional Machine
Verification SOP Class and RT Ion Machine Verification SOP Class is
shown in `table_title <#table_DD.3.2.2.2-1>`__. See Section 5.4 for
usage notation.

.. table:: N-GET Attribute List- RT Conventional Machine Verification
SOP Class and RT Ion Machine Verification SOP Class

   +--------------------------+-------------+--------------------------+
   | Attribute Name           | Tag         | Usage SCU/SCP            |
   +==========================+=============+==========================+
   | Referenced RT Plan       | (300C,0002) | -/1                      |
   | Sequence                 |             |                          |
   +--------------------------+-------------+--------------------------+
   | >Referenced SOP Class    | (0008,1150) | -/1                      |
   | UID                      |             |                          |
   +--------------------------+-------------+--------------------------+
   | >Referenced SOP Instance | (0008,1155) | -/1                      |
   | UID                      |             |                          |
   +--------------------------+-------------+--------------------------+
   | Referenced Fraction      | (300C,0022) | -/1                      |
   | Group Number             |             |                          |
   +--------------------------+-------------+--------------------------+
   | Patient ID               | (0010,0020) | -/1                      |
   +--------------------------+-------------+--------------------------+
   | *Include*\ `table_tit    |             |                          |
   | le <#table_CC.2.5-2e>`__ |             |                          |
   +--------------------------+-------------+--------------------------+
   | Treatment Verification   | (3008,002C) | -/1                      |
   | Status                   |             |                          |
   +--------------------------+-------------+--------------------------+
   | Failed Parameters        | (0074,1048) | -/2                      |
   | Sequence                 |             |                          |
   |                          |             | (zero or more items      |
   |                          |             | shall be included in     |
   |                          |             | this Sequence)           |
   +--------------------------+-------------+--------------------------+
   | *                        |             |                          |
   | >Include*\ `table_title  |             |                          |
   | <#table_DD.3.2.2.1-1>`__ |             |                          |
   +--------------------------+-------------+--------------------------+
   | Overridden Parameters    | (0074,104A) | -/2                      |
   | Sequence                 |             |                          |
   |                          |             | (zero or more items      |
   |                          |             | shall be included in     |
   |                          |             | this Sequence)           |
   +--------------------------+-------------+--------------------------+
   | *                        |             |                          |
   | >Include*\ `table_title  |             |                          |
   | <#table_DD.3.2.2.1-1>`__ |             |                          |
   +--------------------------+-------------+--------------------------+
   | >Operators' Name         | (0008,1070) | -/2                      |
   +--------------------------+-------------+--------------------------+
   | >Override Reason         | (3008,0066) | -/2                      |
   +--------------------------+-------------+--------------------------+
   | *All other Attributes*   | -           | 3/2                      |
   +--------------------------+-------------+--------------------------+

.. _sect_DD.3.2.2.3:

Status
''''''

`table_title <#table_DD.3.2.2.3-1>`__ defines the status code values
that might be returned in a N-GET response. General status code values
and fields related to status code values are defined for N-GET DIMSE
Service in .

.. table:: RT Conventional Machine and RT Ion Machine Verification SOP
Class N-GET Status Values

   +----------------+-------------------------------------+-------------+
   | Service Status | Further Meaning                     | Status Code |
   +================+=====================================+=============+
   | Success        | Treatment Verification Status of    | 0000        |
   |                | the applicable Machine Verification |             |
   |                | instance successfully returned.     |             |
   +----------------+-------------------------------------+-------------+
   | Failure        | Failed: Applicable Machine          | C112        |
   |                | Verification instance not found     |             |
   +----------------+-------------------------------------+-------------+

.. _sect_DD.3.2.2.4:

Behavior
''''''''

The SCU uses N-GET to retrieve from the SCP the verification status and
results of the applicable Machine Verification SOP Instance.

The SCP shall return the Treatment Verification Status (3008,002C)
Attribute as well as the status code of the requested SOP Instance
update. Treatment Verification Status shall have one of the following
values:

VERIFIED = treatment verified

VERIFIED_OVR = treatment verified with at least one out-of-range value
overridden

NOT_VERIFIED = verification of treatment was not successful

The VERIFIED state indicates that all required parameters have been
checked and no out-of-range values have been detected. The VERIFIED_OVR
state indicates that the treatment failed to verify due to one or more
out-of-range values that were then overridden. NOT_VERIFIED indicates
that one of more of the out-of-range values has not yet been overridden
and the treatment cannot go ahead. This could be because at least one
out-of-range value was detected, or one or more values required for
verification were not supplied. The site- and vendor-specific
configuration of the MPV determines the Attributes and ranges required
for successful verification.

If the Treatment Verification Status is VERIFIED_OVR, one or more
parameter occurrences shall be returned in Overridden Parameters
Sequence (0074,104A), otherwise the sequence shall be empty.

If the Treatment Verification Status is NOT_VERIFIED, one or more
parameter occurrences shall be returned in Failed Parameters Sequence
(0074,1048), otherwise the sequence shall be empty.

See for specification of how the Attribute tags and position within a
sequence are encoded.

The SCP shall return the status code of the requested action. The
meanings of success, warning and failure status codes are defined in
`Status <#sect_DD.3.2.2.3>`__.

.. _sect_DD.3.2.3:

N-ACTION
^^^^^^^^

The N-ACTION is used to initiate parameter verification of an instance
of the applicable Machine Verification SOP Class.

.. _sect_DD.3.2.3.1:

Attributes
''''''''''

The action types of the N-ACTION are defined as shown in
`table_title <#table_DD.3.2.3-1>`__.

.. table:: Action Event Information

   +---------------------------+----------------+----------------+-----+---------------+
   | Action Type Name          | Action Type ID | Attribute Name | Tag | Usage SCU/SCP |
   +===========================+================+================+=====+===============+
   | Request Beam Verification | 1              | None           | -   | -             |
   +---------------------------+----------------+----------------+-----+---------------+

.. _sect_DD.3.2.3.2:

Status
''''''

`table_title <#table_DD.3.2.3-2>`__ defines the status code values that
might be returned in a N-ACTION response. General status code values and
fields related to status code values are defined for N-ACTION DIMSE
Service in .

.. table:: RT Conventional Machine and RT Ion Machine Verification SOP
Class N-ACTION Status Values

   +----------------+-------------------------------------+-------------+
   | Service Status | Further Meaning                     | Status Code |
   +================+=====================================+=============+
   | Success        | Machine Parameter Verification of   | 0000        |
   |                | the applicable Machine Verification |             |
   |                | instance successfully initiated.    |             |
   +----------------+-------------------------------------+-------------+
   | Failure        | Failed: Machine Verification        | C112        |
   |                | requested instance not found.       |             |
   +----------------+-------------------------------------+-------------+

.. _sect_DD.3.2.3.3:

Behavior
''''''''

The SCU uses N-ACTION to instruct the SCP to initiate machine parameter
verification of the applicable Machine Verification SOP Instance.

.. _sect_DD.3.2.4:

N-DELETE
^^^^^^^^

The N-DELETE is used to delete an instance of the applicable Machine
Verification SOP Class.

.. _sect_DD.3.2.4.1:

Attributes
''''''''''

There are no specific Attributes.

.. _sect_DD.3.2.4.2:

Status
''''''

There are no specific status codes. See for response status codes.

.. _sect_DD.3.2.4.3:

Behavior
''''''''

The SCU uses the N-DELETE to request the SCP to delete an applicable
Machine Verification SOP Instance. The SCU shall specify in the N-DELETE
request primitive the SOP Instance UID of the applicable Machine
Verification instance.

The SCP shall delete the specified SOP Instance, such that subsequent
operations of the same SOP Instance will fail.

The SCP shall return the status code of the requested SOP Instance
deletion. The meanings of success, warning, and failure status classes
are defined in .

If an N-DELETE is not issued, the SOP Class instance may be deleted on
the SCP by a manual or automatic operation. This behavior is beyond the
scope of the Standard.

.. _sect_DD.3.2.5:

N-EVENT-REPORT
^^^^^^^^^^^^^^

The N-EVENT-REPORT is used by the MPV to notify the TDS of the status of
the verification task (successful or otherwise), or to notify the TDS
that a verification is pending (in progress). The encoding of
Notification Event Information is defined in .

.. _sect_DD.3.2.5.1:

Attributes
''''''''''

The arguments of the N-EVENT-REPORT are defined as shown in
`table_title <#table_DD.3.2.5-1>`__.

.. table:: Notification Event Information

   +-------------+-------------+-------------+-------------+-------------+
   | Event Type  | Event Type  | Attribute   | Tag         | Usage       |
   | Name        | ID          | Name        |             | SCU/SCP     |
   +=============+=============+=============+=============+=============+
   | Pending     | 1           | None        | -           | -           |
   +-------------+-------------+-------------+-------------+-------------+
   | Done        | 2           | Treatment   | (3008,002C) | -/1         |
   |             |             | V           |             |             |
   |             |             | erification |             |             |
   |             |             | Status      |             |             |
   +-------------+-------------+-------------+-------------+-------------+

.. _sect_DD.3.2.5.2:

Status
''''''

There are no specific status codes. See for response status codes.

.. _sect_DD.3.2.5.3:

Behavior
''''''''

The SCP uses the N-EVENT-REPORT to inform the SCU of the verification
status. See .

If the Event Type ID = 1 then the verification is still in progress, and
the SCU must wait until another event is received. See .

If the Event Type ID = 2 then the verification process has been
completed. The SCU may use the returned value of the Treatment
Verification Status (3008,002C) to determine whether or not the beam is
ready to be delivered, or if a machine adjustment or override needs to
be made. See .

