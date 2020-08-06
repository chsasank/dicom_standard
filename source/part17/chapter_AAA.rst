.. _chapter_AAA:

Implantation Plan SR Document (Informative)
===========================================

For the implantation of bone mounted implants, information that has been
generated during the implantation planning phase is needed in the OR. To
convey this information to the OR, a DICOM format for the results of an
implantation planning activity referring to implant templates has been
introduced. An Implantation Plan SR Document should be utilized by
surgeons, navigation devices, and for documentation purposes. The Plan
contains relevant intraoperative information concerning the assembly of
the implant components, resection lines, registration information, and
relevant patient data. Thus, the Implantation Plan SR Document can help
to enhance information logistics within the workflow. It does not
contain any information about the planned surgical workflow. This
information may be addressed by other DICOM Supplements. Nevertheless,
this SR document may reference to or may be referenced by objects
containing workflow information.

Additionally, once an implantation plan has been generated, it can be
used as input for a planning application to facilitate adaption of a
plan in cases where this is necessary due to unforeseen situations.

The workflow is considered to be the following:

Some kind of planning application helps the user to perform implantation
planning; he can choose the optimal implant for a patient using implant
templates from a repository. The user aligns the implant template with
patient data with or without the help of the application. (Planning
without patient data can be stored in the Implantation Plan SR Document
as well.)

Subsequently, an Implantation Plan SR Document Instance will be created
that contains the results of the planning. No information of the process
itself (previously chosen implant templates, methods, etc.) will be
stored. However, an Implantation Plan Document is considered to contain
the important parameters to retrace a planning result.

There are two main components an Implantation Plan SR Document consists
of (see `figure_title <#figure_AAA.1-1>`__). The implant component
selection is used to point to a selected implant template in the
repository, whereas the assembly is used to describe the composition of
the selected implant templates. `figure_title <#figure_AAA.2-1>`__ shows
how the Implantation Plan SR Document parts make references to the
implant templates. Each Implantation Plan SR Document can contain a
single implant component selection and several assemblies but it
describes only one planning result for one particular patient.

The recipient of the Implantation Plan SR Document can decide whether to
read only the "list" of used implants or to go into detail and read the
compositions as well. In both cases, he must have access to the
repository of the Implant Templates to get detailed information about
the implant (such as its geometry).

.. _sect_AAA.1:

Implantation Plan SR Document Content Tree Structure
----------------------------------------------------

The following structure shows the main content of an Implantation Plan
SR Document. As can be seen in `figure_title <#figure_AAA.1-1>`__, the
Implantation Plan consists mainly of the selected Implant Components and
their Assemblies.

.. _sect_AAA.2:

Relationship Between Implant Template and Implantation Plan
-----------------------------------------------------------

The Implantation Plan SR Document is tightly related to Implantation
Templates (see and ). The following `figure_title <#figure_AAA.2-1>`__
shows the relationship between the Implant Templates and the
Implantation Plan.

.. _sect_AAA.3:

Implantation Plan SR Document Total Hip Replacement Example
-----------------------------------------------------------

The following example shows the planning result of a simple THR (Total
Hip Replacement) without any registration information. One Patient Image
was used and one visualization was produced. One Femoral Stem, one
Femoral Head, one Acetabular Bearing Insert and one Acetabular Fixation
Cup were selected to be implanted (see
`figure_title <#figure_AAA.3-1>`__).

.. table:: Total Hip Replacement Example

   +-----------+------------------------+------------------------+-----+
   | Node      | Code Meaning of        | Code Meaning or        | TID |
   |           | Concept Name           | Example Value          |     |
   +===========+========================+========================+=====+
   | 1         | Implantation Plan      |                        |     |
   +-----------+------------------------+------------------------+-----+
   | 1.1       | Language of Content    | English                |     |
   |           | Item and Descendants   |                        |     |
   +-----------+------------------------+------------------------+-----+
   | **1.2**   | **Observation          |                        |     |
   |           | Context**              |                        |     |
   +-----------+------------------------+------------------------+-----+
   | 1.2.1     | Person Observer Name   | Dr. Michael Mueller    |     |
   +-----------+------------------------+------------------------+-----+
   | 1.2.2     | Subject Name           | John Smith             |     |
   +-----------+------------------------+------------------------+-----+
   | 1.2.3     | Subject ID             | 1.2.3.4.5.6.7.8.9      |     |
   +-----------+------------------------+------------------------+-----+
   | 1.2.4     | Subject Species        | (337915000, SCT, "homo |     |
   |           |                        | sapiens")              |     |
   +-----------+------------------------+------------------------+-----+
   | **1.3**   | **Implant Component    |                        |     |
   |           | List**                 |                        |     |
   +-----------+------------------------+------------------------+-----+
   | 1.3.1     | Implant Assembly       | Reference to THR       |     |
   |           | Template               |                        |     |
   +-----------+------------------------+------------------------+-----+
   | 1.3.2     | Selected Implant       |                        |     |
   |           | Component              |                        |     |
   +-----------+------------------------+------------------------+-----+
   | 1.3.2.1   | Component ID           | 1                      |     |
   +-----------+------------------------+------------------------+-----+
   | 1.3.2.2   | Component Type         | 112310                 |     |
   +-----------+------------------------+------------------------+-----+
   | 1.3.2.3   |                        | Reference to Implant   |     |
   |           |                        | Template "FS1000"      |     |
   |           |                        | (derived)              |     |
   +-----------+------------------------+------------------------+-----+
   | 1.3.2.4   | Frame Of Reference UID | 1.2.3.4.1              |     |
   +-----------+------------------------+------------------------+-----+
   | 1.3.2.5   | Manufacturer Implant   | Reference to Implant   |     |
   |           | Template               | Template "FS1000"      |     |
   |           |                        | (original)             |     |
   +-----------+------------------------+------------------------+-----+
   | 1.3.3     | Selected Implant       |                        |     |
   |           | Component              |                        |     |
   +-----------+------------------------+------------------------+-----+
   | 1.3.3.1   | Component ID           | 2                      |     |
   +-----------+------------------------+------------------------+-----+
   | 1.3.3.2   | Component Type         | (304121006, SCT,       |     |
   |           |                        | "Femoral Head          |     |
   |           |                        | Prosthesis")           |     |
   +-----------+------------------------+------------------------+-----+
   | 1.3.3.3   |                        | Reference to Implant   |     |
   |           |                        | Template "FH2000"      |     |
   |           |                        | (derived)              |     |
   +-----------+------------------------+------------------------+-----+
   | 1.3.3.4   | Frame Of Reference UID | 1.2.3.4.2              |     |
   +-----------+------------------------+------------------------+-----+
   | 1.3.3.5   | Manufacturer Implant   | Reference to Implant   |     |
   |           | Template               | Template "FH2000"      |     |
   |           |                        | (original)             |     |
   +-----------+------------------------+------------------------+-----+
   | 1.3.4     | Selected Implant       |                        |     |
   |           | Component              |                        |     |
   +-----------+------------------------+------------------------+-----+
   | 1.3.4.1   | Component ID           | 3                      |     |
   +-----------+------------------------+------------------------+-----+
   | 1.3.4.2   | Component Type         | 112305                 |     |
   +-----------+------------------------+------------------------+-----+
   | 1.3.4.3   |                        | Reference to Implant   |     |
   |           |                        | Template "AFC3000"     |     |
   |           |                        | (derived)              |     |
   +-----------+------------------------+------------------------+-----+
   | 1.3.4.4   | Frame Of Reference UID | 1.2.3.4.3              |     |
   +-----------+------------------------+------------------------+-----+
   | 1.3.4.5   | Manufacturer Implant   | Reference to Implant   |     |
   |           | Template               | Template "AFC3000"     |     |
   |           |                        | (original)             |     |
   +-----------+------------------------+------------------------+-----+
   | 1.3.5     | Selected Implant       |                        |     |
   |           | Component              |                        |     |
   +-----------+------------------------+------------------------+-----+
   | 1.3.5.1   | Component ID           | 4                      |     |
   +-----------+------------------------+------------------------+-----+
   | 1.3.5.2   | Component Type         | (112306, DCM,          |     |
   |           |                        | "Acetabular Cup        |     |
   |           |                        | Insert")               |     |
   +-----------+------------------------+------------------------+-----+
   | 1.3.5.3   |                        | Reference to Implant   |     |
   |           |                        | Template "ABI4000"     |     |
   |           |                        | (derived)              |     |
   +-----------+------------------------+------------------------+-----+
   | 1.3.5.4   | Frame Of Reference UID | 1.2.3.4.4              |     |
   +-----------+------------------------+------------------------+-----+
   | 1.3.5.5   | Manufacturer Implant   | Reference to Implant   |     |
   |           | Template               | Template "ABI4000"     |     |
   |           |                        | (original)             |     |
   +-----------+------------------------+------------------------+-----+
   | **1.4.**  | **Assembly**           |                        |     |
   +-----------+------------------------+------------------------+-----+
   | 1.4.1     | Component Connection   |                        |     |
   +-----------+------------------------+------------------------+-----+
   | 1.4.1.1   | Connected Implantation |                        |     |
   |           | Plan Component         |                        |     |
   +-----------+------------------------+------------------------+-----+
   | 1.4.1.1.1 | Component ID           | 3                      |     |
   +-----------+------------------------+------------------------+-----+
   | 1.4.1.1.2 | Mating Feature Set ID  | 1                      |     |
   +-----------+------------------------+------------------------+-----+
   | 1.4.1.1.3 | Mating Feature ID      | 1                      |     |
   +-----------+------------------------+------------------------+-----+
   | 1.4.1.2   | Connected Implantation |                        |     |
   |           | Plan Component         |                        |     |
   +-----------+------------------------+------------------------+-----+
   | 1.4.1.2.1 | Component ID           | 4                      |     |
   +-----------+------------------------+------------------------+-----+
   | 1.4.1.2.2 | Mating Feature Set ID  | 1                      |     |
   +-----------+------------------------+------------------------+-----+
   | 1.4.1.2.3 | Mating Feature ID      | 1                      |     |
   +-----------+------------------------+------------------------+-----+
   | 1.4.2     | Component Connection   |                        |     |
   +-----------+------------------------+------------------------+-----+
   | 1.4.2.1   | Connected Implantation |                        |     |
   |           | Plan Component         |                        |     |
   +-----------+------------------------+------------------------+-----+
   | 1.4.2.1.1 | Component ID           | 2                      |     |
   +-----------+------------------------+------------------------+-----+
   | 1.4.2.1.2 | Mating Feature Set ID  | 1                      |     |
   +-----------+------------------------+------------------------+-----+
   | 1.4.2.1.3 | Mating Feature ID      | 1                      |     |
   +-----------+------------------------+------------------------+-----+
   | 1.4.2.2   | Connected Implantation |                        |     |
   |           | Plan Component         |                        |     |
   +-----------+------------------------+------------------------+-----+
   | 1.4.2.2.1 | Component ID           | 1                      |     |
   +-----------+------------------------+------------------------+-----+
   | 1.4.2.2.2 | Mating Feature Set ID  | 1                      |     |
   +-----------+------------------------+------------------------+-----+
   | 1.4.2.2.3 | Mating Feature ID      | 2                      |     |
   +-----------+------------------------+------------------------+-----+
   | 1.4.3     | Component Connection   |                        |     |
   +-----------+------------------------+------------------------+-----+
   | 1.4.3.1   | Connected Implantation |                        |     |
   |           | Plan Component         |                        |     |
   +-----------+------------------------+------------------------+-----+
   | 1.4.3.1.1 | Component ID           | 2                      |     |
   +-----------+------------------------+------------------------+-----+
   | 1.4.3.1.2 | Mating Feature Set ID  | 2                      |     |
   +-----------+------------------------+------------------------+-----+
   | 1.4.3.1.3 | Mating Feature ID      | 1                      |     |
   +-----------+------------------------+------------------------+-----+
   | 1.4.3.2   | Connected Implantation |                        |     |
   |           | Plan Component         |                        |     |
   +-----------+------------------------+------------------------+-----+
   | 1.4.3.2.1 | Component ID           | 4                      |     |
   +-----------+------------------------+------------------------+-----+
   | 1.4.3.2.2 | Mating Feature Set ID  | 2                      |     |
   +-----------+------------------------+------------------------+-----+
   | 1.4.3.2.3 | Mating Feature ID      | 2                      |     |
   +-----------+------------------------+------------------------+-----+
   | **1.5**   | **Information used for |                        |     |
   |           | planning**             |                        |     |
   +-----------+------------------------+------------------------+-----+
   | 1.5.1     | Patient Image          | Reference to Image 01  |     |
   +-----------+------------------------+------------------------+-----+
   | 1.5.1.2   | Horizontal Pixel       | 0.2 mm/pixel           |     |
   |           | Spacing                |                        |     |
   +-----------+------------------------+------------------------+-----+
   | 1.5.1.3   | Vertical Pixel Spacing | 0.2 mm/pixel           |     |
   +-----------+------------------------+------------------------+-----+
   | **1.6**   | **Planning Information |                        |     |
   |           | for Intraoperative     |                        |     |
   |           | Usage**                |                        |     |
   +-----------+------------------------+------------------------+-----+
   | 1.6.1     | Supporting Information | Reference to           |     |
   |           |                        | Encapsulated           |     |
   |           |                        | PDF-Document 01        |     |
   +-----------+------------------------+------------------------+-----+
   | 1.6.2     | Derived Images         | Reference to           |     |
   |           |                        | Visualization 01       |     |
   +-----------+------------------------+------------------------+-----+

.. _sect_AAA.4:

Implantation Plan SR Document Dental Drilling Template Example
--------------------------------------------------------------

The following example shows the result of a planning activity for a
dental implantation using a dental drilling template. The implant
positioning is based on a CT-Scan during which the patient has been
wearing a bite plate with 3 markers. In this example the markers
(visible in the patient's CT images) are detected by the planning
application. After the implants have been positioned, the bite plate, in
combination with the registration information of the implants, can be
used to produce the dental drilling template.

In the following example, two implants are inserted that are not
assembled using Mating Points.

The markers of the bite plate are identified and stored as 3 Fiducials
in one Fiducial Set. This Fiducial Set has its own Frame of Reference
(1.2.3.4.100).

The Registration Object created by the planning application uses the
patient's CT Frame of Reference as main Frame of Reference (see
`figure_title <#figure_AAA.4-1>`__).

.. table:: Dental Drilling Template Example

   +-----------+------------------------+------------------------+-----+
   | Node      | Code Meaning of        | Code Meaning or        | TID |
   |           | Concept Name           | Example Value          |     |
   +===========+========================+========================+=====+
   | 1         | Implantation Plan      |                        |     |
   +-----------+------------------------+------------------------+-----+
   | 1.1       | Language of Content    | English                |     |
   |           | Item and Descendants   |                        |     |
   +-----------+------------------------+------------------------+-----+
   | **1.2**   | **Observation          |                        |     |
   |           | Context**              |                        |     |
   +-----------+------------------------+------------------------+-----+
   | 1.2.1     | Person Observer Name   | Dr. Michael Mueller    |     |
   +-----------+------------------------+------------------------+-----+
   | 1.2.2     | Subject Name           | John Smith             |     |
   +-----------+------------------------+------------------------+-----+
   | 1.2.3     | Subject ID             | 1.2.3.4.5.6.7.8.9      |     |
   +-----------+------------------------+------------------------+-----+
   | 1.2.4     | Subject Species        | (337915000, SCT, "homo |     |
   |           |                        | sapiens")              |     |
   +-----------+------------------------+------------------------+-----+
   | **1.3**   | **Implant Component    |                        |     |
   |           | List**                 |                        |     |
   +-----------+------------------------+------------------------+-----+
   | 1.3.1     | Selected Implant       |                        |     |
   |           | Component              |                        |     |
   +-----------+------------------------+------------------------+-----+
   | 1.3.1.1   | Component ID           | 1                      |     |
   +-----------+------------------------+------------------------+-----+
   | 1.3.1.2   | Component Type         | 112305                 |     |
   +-----------+------------------------+------------------------+-----+
   | 1.3.1.3   |                        | Reference to Implant   |     |
   |           |                        | Template "DI1000"      |     |
   |           |                        | (derived)              |     |
   +-----------+------------------------+------------------------+-----+
   | 1.3.1.4   | Frame Of Reference UID | 1.2.3.4.1              |     |
   +-----------+------------------------+------------------------+-----+
   | 1.3.1.5   | Manufacturer Implant   | Reference to Implant   |     |
   |           | Template               | Template "DI1000"      |     |
   |           |                        | (original)             |     |
   +-----------+------------------------+------------------------+-----+
   | 1.3.2     | Implant Component      |                        |     |
   |           | Selection              |                        |     |
   +-----------+------------------------+------------------------+-----+
   | 1.3.2.1   | Component ID           | 2                      |     |
   +-----------+------------------------+------------------------+-----+
   | 1.3.2.2   | Component Type         | (112306, DCM,          |     |
   |           |                        | "Acetabular Cup        |     |
   |           |                        | Insert")               |     |
   +-----------+------------------------+------------------------+-----+
   | 1.3.2.3   |                        | Reference to Implant   |     |
   |           |                        | Template "DI2000"      |     |
   |           |                        | (derived)              |     |
   +-----------+------------------------+------------------------+-----+
   | 1.3.2.4   | Frame Of Reference UID | 1.2.3.4.2              |     |
   +-----------+------------------------+------------------------+-----+
   | 1.3.2.5   | Manufacturer Implant   | Reference to Implant   |     |
   |           | Template               | Template "DI2000"      |     |
   |           |                        | (original)             |     |
   +-----------+------------------------+------------------------+-----+
   | **1.4**   | **Information used for |                        |     |
   |           | planning**             |                        |     |
   +-----------+------------------------+------------------------+-----+
   | 1.4.1     | Patient Image          | Reference to CT        |     |
   |           |                        | Image01                |     |
   +-----------+------------------------+------------------------+-----+
   | 1.4.1.2   | Horizontal Pixel       | 0.3 mm/pixel           |     |
   |           | Spacing                |                        |     |
   +-----------+------------------------+------------------------+-----+
   | 1.4.1.3   | Vertical Pixel Spacing | 0.3 mm/pixel           |     |
   +-----------+------------------------+------------------------+-----+
   | **1.5**   | **Planning Information |                        |     |
   |           | for Intraoperative     |                        |     |
   |           | Usage**                |                        |     |
   +-----------+------------------------+------------------------+-----+
   | 1.5.1     | Derived Planning       | Reference to           |     |
   |           | Images                 | Visualization01        |     |
   +-----------+------------------------+------------------------+-----+
   | 1.5.2     | Spatial Registration   | Reference to           |     |
   |           |                        | Registration01         |     |
   +-----------+------------------------+------------------------+-----+
   | 1.5.2.1   | Frame Of Reference UID | 1.2.3.4.1              |     |
   +-----------+------------------------+------------------------+-----+
   | 1.5.2.2   | Frame Of Reference UID | 1.2.3.4.2              |     |
   +-----------+------------------------+------------------------+-----+
   | 1.5.2.3   | Frame Of Reference UID | 1.2.3.4.3              |     |
   +-----------+------------------------+------------------------+-----+
   | 1.5.2.4   | Frame Of Reference UID | 1.2.3.4.100            |     |
   +-----------+------------------------+------------------------+-----+
   | 1.5.3     | Derived Planning Data  | Reference to Fiducial  |     |
   |           |                        | 01                     |     |
   +-----------+------------------------+------------------------+-----+
   | 1.5.3.1   | Derived Fiducial       | 1.2.3.4.3              |     |
   +-----------+------------------------+------------------------+-----+
   | 1.5.3.1.1 | Fiducial Intent        | Bite Plate Marker      |     |
   +-----------+------------------------+------------------------+-----+
   | 1.5.3.2   | Derived Fiducial       | 1.2.3.4.4              |     |
   +-----------+------------------------+------------------------+-----+
   | 1.5.3.2.1 | Fiducial Intent        | Bite Plate Marker      |     |
   +-----------+------------------------+------------------------+-----+
   | 1.5.3.3   | Derived Fiducial       | 1.2.3.4.5              |     |
   +-----------+------------------------+------------------------+-----+
   | 1.5.3.3.1 | Fiducial Intent        | Bite Plate Marker      |     |
   +-----------+------------------------+------------------------+-----+

