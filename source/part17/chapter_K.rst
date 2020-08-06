.. _chapter_K:

Ultrasound Staged Protocol Data Management (Informative)
========================================================

.. _sect_K.1:

Purpose of this Annex
---------------------

The purpose of this annex is to enhance consistency and interoperability
among creators and consumers of Ultrasound images within Staged Protocol
Exams. An ultrasound "Staged Protocol Exam" is an exam that acquires a
set of images under specified conditions during time intervals called
"Stages". An example of such an exam is a cardiac stress-echo Staged
Protocol.

This informative annex describes the use of ultrasound Staged Protocol
Attributes within the following DICOM Services: Ultrasound Image,
Ultrasound Multi-frame Image, and Key Object Selection Document Storage,
Modality Worklist, and Modality Performed Procedure Step Services.

.. _sect_K.2:

Prerequisites For Support
-------------------------

The support of ultrasound Staged Protocol Data Management requires
support for the Ultrasound Image SOP Class or Ultrasound Multi-frame
Image SOP Class as appropriate for the nature of the Protocol. By
supporting some optional Elements of these SOP Classes, Staged-Protocols
can be managed. Support of Key Object Selection allows control of the
order of View and Stage presentation. Support of Modality Worklist
Management and Modality Performed Procedure Step allow control over
specific workflow use cases as described in this Annex.

.. _sect_K.3:

Definition of a Staged Protocol Exam
------------------------------------

A "Staged Protocol Exam" acquires images in two or more distinct time
intervals called "Stages" with a consistent set of images called "Views"
acquired during each Stage of the exam. A View is of a particular cross
section of the anatomy acquired with a specific ultrasound transducer
position and orientation. During the acquisition of a Staged Protocol
Exam, the modality may also acquire non-Protocol images at one or more
Protocol Stages.

A common real-world example of an ultrasound Staged Protocol exam is a
cardiac stress-echo ultrasound exam. Images are acquired in distinct
time intervals (Stages) of different levels of stress and Views as shown
in `figure_title <#figure_K.3-1>`__. Typically, stress is induced by
means of patient exercise or medication. Typical Stages for such an exam
are baseline, mid-stress, peak-stress, and recovery. During the baseline
Stage the patient is at rest, prior to inducing stress through
medication or exercise. At mid-stress Stage the heart is under a
moderate level of stress. During peak-stress Stage the patient's heart
experiences maximum stress appropriate for the patient's condition.
Finally, during the recovery Stage, the heart recovers because the
source of stress is absent.

At each Stage an equivalent set of Views is acquired. Examples of
typical Views are parasternal long axis and parasternal short axis.
Examination of wall motion between the corresponding Views of different
Stages may reveal ischemia of one or more regions ("segments") of the
myocardium. `figure_title <#figure_K.3-1>`__ illustrates the typical
results of a cardiac stress-echo ultrasound exam.

.. _sect_K.4:

Attributes Used in Staged Protocol Exams
----------------------------------------

The DICOM Standard includes a number of Attributes of significance to
Staged Protocol Exams. This Annex explains how scheduling and
acquisition systems may use these Attributes to convey Staged Protocol
related information.

`table_title <#table_K.4-1>`__ lists all the Attributes relevant to
convey Staged Protocol related information (see for details about these
Attributes).

.. table:: Attributes That Convey Staged Protocol Related Information

   +----------------------+----------------------+----------------------+
   | Modality Worklist    | US Image and US      | MPPS IOD             |
   |                      | Multi-frame IOD      |                      |
   | (Tag) [Return Key    |                      | (Tag) [SCU/SCP Type] |
   | Type]                | (TAG) [Type]         |                      |
   +======================+======================+======================+
   | ----                 | ----                 | Scheduled Step       |
   |                      |                      | Attributes Sequence  |
   |                      |                      | (0040,0270) [1/1]    |
   |                      |                      | (b)                  |
   +----------------------+----------------------+----------------------+
   | Study Instance UID   | Study Instance UID   | >Study Instance UID  |
   | (0020,000D) [1]      | (0020,000D) [1]      | (0020,000D) [1/1]    |
   +----------------------+----------------------+----------------------+
   | Scheduled Procedure  | Request Attributes   | ----                 |
   | Step Sequence        | Sequence (0040,0275) |                      |
   | (0040,0100)          | [3] (a,b)            |                      |
   +----------------------+----------------------+----------------------+
   | >Scheduled Procedure | >Scheduled Procedure | >Scheduled Procedure |
   | Step Description     | Step Description     | Step Description     |
   | (0040,0007) [1C]     | (0040,0007) [3]      | (0040,0007) [2/2]    |
   +----------------------+----------------------+----------------------+
   | >Scheduled Protocol  | >Scheduled Protocol  | >Scheduled Protocol  |
   | Code Sequence        | Code Sequence        | Code Sequence        |
   | (0040,0008) [1C]     | (0040,0008) [3]      | (0040,0008) [2/2]    |
   +----------------------+----------------------+----------------------+
   | ----                 | Performed Procedure  | Performed Procedure  |
   |                      | Step Description     | Step Description     |
   |                      | (0040,0254) [3]      | (0040,0254) [2/2]    |
   +----------------------+----------------------+----------------------+
   | ----                 | Protocol Name        | Performed Series     |
   |                      | (0018,1030) [3]      | Sequence             |
   |                      |                      | (0040,0340)>Protocol |
   |                      |                      | Name (0018,1030)     |
   |                      |                      | [1/1]                |
   +----------------------+----------------------+----------------------+
   | ----                 | Performed Protocol   | Performed Protocol   |
   |                      | Code Sequence        | Code Sequence        |
   |                      | (0040,0260) [3]      | (0040,0260) [1/1]    |
   +----------------------+----------------------+----------------------+
   | ----                 | Number of Stages     | ----                 |
   |                      | (0008,2124) [2C]     |                      |
   +----------------------+----------------------+----------------------+
   | ----                 | Number of Views In   | ----                 |
   |                      | Stage (0008,212A)    |                      |
   |                      | [2C]                 |                      |
   +----------------------+----------------------+----------------------+
   | ----                 | Stage Name           | ----                 |
   |                      | (0008,2120) [3]      |                      |
   +----------------------+----------------------+----------------------+
   | ----                 | Stage Number         | ----                 |
   |                      | (0008,2122) [3]      |                      |
   +----------------------+----------------------+----------------------+
   | ----                 | Stage Code Sequence  | ----                 |
   |                      | (0040,000A) [3]      |                      |
   +----------------------+----------------------+----------------------+
   | ----                 | View Name            | ----                 |
   |                      | (0008,2127) [3]      |                      |
   +----------------------+----------------------+----------------------+
   | ----                 | View Number          | ----                 |
   |                      | (0008,2128) [3]      |                      |
   +----------------------+----------------------+----------------------+
   | ----                 | Number of Event      | ----                 |
   |                      | Timers (0008,2129)   |                      |
   |                      | [3]                  |                      |
   +----------------------+----------------------+----------------------+
   | ----                 | Event Elapsed        | ----                 |
   |                      | Time(s) (0008,2130)  |                      |
   |                      | [3]                  |                      |
   +----------------------+----------------------+----------------------+
   | ----                 | Event Timer Name(s)  | ----                 |
   |                      | (0008,2132) [3]      |                      |
   +----------------------+----------------------+----------------------+
   | ----                 | View Code Sequence   | ----                 |
   |                      | (0054,0220) [3]      |                      |
   +----------------------+----------------------+----------------------+
   | ----                 | >View Modifier Code  | ----                 |
   |                      | Sequence (0054,0222) |                      |
   |                      | [3]                  |                      |
   +----------------------+----------------------+----------------------+

a. Recommended if the Modality conforms as an SCU to the Modality
   Worklist SOP Class and Modality Performed Procedure Step

b. Sequence may have one or more Items

.. _sect_K.5:

Guidelines
----------

This annex provides guidelines for implementation of the following
aspects of Staged Protocol exams:

-  Identification of a Staged Protocol exam.

-  Identification of Stages and Views within a Staged Protocol exam.

-  Identification of extra-Protocol images within a Staged Protocol
   exam.

-  Acquisition of multiple images of a View during a Stage, and
   identification of the preferred image for that Stage.

-  Workflow management of Staged Protocol images.

.. _sect_K.5.1:

Staged Protocol Exam Identification
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

The Attributes Number of Stages (0008,2124) and Number of Views in Stage
(0008,212A) are each Type 2C with the condition "Required if this image
was acquired in a Staged Protocol." These two Attributes will be present
with values in image SOP Instances if the exam meets the definition of a
Staged Protocol Exam stated in `Definition of a Staged Protocol
Exam <#sect_K.3>`__. This includes both the Protocol View images as well
as any extra-Protocol images acquired during the Protocol Stages.

The Attributes Protocol Name (0018,1030) and Performed Protocol Code
Sequence (0040,0260) identify the Protocol of a Staged Protocol Exam,
but the mere presence of one or both of these Attributes does not in
itself identify the acquisition as a Staged Protocol Exam. If both
Protocol Name and Performed Protocol Code Sequence Attributes are
present, the Protocol Name value takes precedence over the Performed
Protocol Code Sequence Code Meaning value as a display label for the
Protocol, since the Protocol Name would convey the institutional
preference better than the standardized code meaning.

.. _sect_K.5.2:

Stage and View Identification
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

Display devices usually include capabilities that aid in the
organization and presentation of images acquired as part of the Staged
Protocol. These capabilities allow a clinician to display images of a
given View acquired during different Stages of the Protocol side by side
for comparison. A View is a particular combination of the transducer
position and orientation at the time of image acquisition. Images are
acquired at the same View in different Protocol Stages for the purpose
of comparison. For these features to work properly, the display device
must be able to determine the Stage and View of each image in an
unambiguous fashion.

There are three possible mechanisms for conveying Stage and View
identification in the image SOP Instances:

-  "Numbers" (Stage Number (0008,2122) and View Number (0008,2128) ),
   which number Stages and Views, starting with one.

-  "Names" (Stage Name (0008,2120) and View Name (0008,2127) ), which
   specify textual names for each Stage and View, respectively.

-  "Code sequences" (Stage Code Sequence (0040,000A) for Stage
   identification, and View Code Sequence (0054,0220) for View
   identification), which give identification "codes" to the Stage and
   View respectively.

The use of code sequences to identify Stage and View, using Context
Group values specified in (e.g., and ), allows a display application
with knowledge of the code semantics to render a display in accordance
with clinical domain uses and user preferences (e.g., populating each
quadrant of an echocardiographic display with the user desired stage and
view). The IHE Echocardiography Workflow Profile requires such use of
code sequences for stress-echo studies.

`table_title <#table_K.5-1>`__ provides an example of the Staged
Protocol relevant Attributes in images acquired during a typical cardiac
stress-echo ultrasound exam.

.. table:: Staged Protocol Image Attributes Example

   +----------------------+----------------------+----------------------+
   | **Baseline Stage -   | **Mid-Stress Stage - | **Mid-Stress Stage - |
   | View 1**             | View 1**             | View 2**             |
   +======================+======================+======================+
   | Study Instance UID:  | Study Instance UID:  | Study Instance UID:  |
   |                      |                      |                      |
   | "1.2.840….123.1"     | "1.2.840….123.1"     | "1.2.840….123.1"     |
   +----------------------+----------------------+----------------------+
   | Request Attributes   | Request Attributes   | Request Attributes   |
   | Sequence:            | Sequence:            | Sequence:            |
   +----------------------+----------------------+----------------------+
   | >Scheduled Procedure | >Scheduled Procedure | >Scheduled Procedure |
   | Step Description:    | Step Description:    | Step Description:    |
   | "Exercise stress     | "Exercise stress     | "Exercise stress     |
   | echocardiography"    | echocardiography"    | echocardiography"    |
   +----------------------+----------------------+----------------------+
   | >Scheduled Protocol  | >Scheduled Protocol  | >Scheduled Protocol  |
   | Code Sequence:       | Code Sequence:       | Code Sequence:       |
   +----------------------+----------------------+----------------------+
   | >>Code Value:        | >>Code Value:        | >>Code Value:        |
   | "433233004"          | "433233004"          | "433233004"          |
   +----------------------+----------------------+----------------------+
   | >>Coding Scheme      | >>Coding Scheme      | >>Coding Scheme      |
   | Designator: "SCT"    | Designator: "SCT"    | Designator: "SCT"    |
   +----------------------+----------------------+----------------------+
   | >>Code Meaning:      | >>Code Meaning:      | >>Code Meaning:      |
   | "Exercise stress     | "Exercise stress     | "Exercise stress     |
   | echocardiography"    | echocardiography"    | echocardiography"    |
   +----------------------+----------------------+----------------------+
   | Performed Procedure  | Performed Procedure  | Performed Procedure  |
   | Step Description:    | Step Description:    | Step Description:    |
   | "Exercise stress     | "Exercise stress     | "Exercise stress     |
   | echocardiography"    | echocardiography"    | echocardiography"    |
   +----------------------+----------------------+----------------------+
   | Protocol Name:       | Protocol Name:       | Protocol Name:       |
   |                      |                      |                      |
   | "EXERCISE            | "EXERCISE            | "EXERCISE            |
   | STRESS-ECHO"         | STRESS-ECHO"         | STRESS-ECHO"         |
   +----------------------+----------------------+----------------------+
   | Performed Protocol   | Performed Protocol   | Performed Protocol   |
   | Code Sequence:       | Code Sequence:       | Code Sequence:       |
   +----------------------+----------------------+----------------------+
   | >Code Value:         | >Code Value:         | >Code Value:         |
   | "433233004"          | "433233004"          | "433233004"          |
   +----------------------+----------------------+----------------------+
   | >Coding Scheme       | >Coding Scheme       | >Coding Scheme       |
   | Designator: "SCT"    | Designator: "SCT"    | Designator: "SCT"    |
   +----------------------+----------------------+----------------------+
   | >Code Meaning:       | >Code Meaning:       | >Code Meaning:       |
   | "Exercise stress     | "Exercise stress     | "Exercise stress     |
   | echocardiography"    | echocardiography"    | echocardiography"    |
   +----------------------+----------------------+----------------------+
   | Number of Stages:    | Number of Stages:    | Number of Stages:    |
   | "4"                  | "4"                  | "4"                  |
   +----------------------+----------------------+----------------------+
   | Number of Views In   | Number of Views In   | Number of Views In   |
   | Stage: "2"           | Stage: "2"           | Stage: "2"           |
   +----------------------+----------------------+----------------------+
   | Stage Name:          | Stage Name:          | Stage Name:          |
   | "BASELINE"           | "MID-STRESS"         | "MID-STRESS"         |
   +----------------------+----------------------+----------------------+
   | Stage Number: "1"    | Stage Number: "2"    | Stage Number: "2"    |
   +----------------------+----------------------+----------------------+
   | Stage Code Sequence: | Stage Code Sequence: | Stage Code Sequence: |
   +----------------------+----------------------+----------------------+
   | >Code                | >Code Value:         | >Code Value:         |
   | Value:"128974000"    | "109091"             | "109091"             |
   +----------------------+----------------------+----------------------+
   | >Coding Scheme       | >Coding Scheme       | >Coding Scheme       |
   | Designator: "SCT"    | Designator: "DCM"    | Designator: "DCM"    |
   +----------------------+----------------------+----------------------+
   | >Code Meaning:       | >Code Meaning:       | >Code Meaning:       |
   | "Baseline state"     | "Cardiac Stress      | "Cardiac Stress      |
   |                      | State"               | State"               |
   +----------------------+----------------------+----------------------+
   | View Name:           | View Name:           | View Name:           |
   | "Para-sternal long   | "Para-sternal long   | "Para-sternal short  |
   | axis"                | axis"                | axis"                |
   +----------------------+----------------------+----------------------+
   | View Number: "1"     | View Number: "1"     | View Number: "2"     |
   +----------------------+----------------------+----------------------+
   | ----                 | Number of Event      | Number of Event      |
   |                      | Timers: "1"          | Timers: "1"          |
   +----------------------+----------------------+----------------------+
   | ----                 | Event Elapsed        | Event Elapsed        |
   |                      | Time(s): "10000"     | Time(s): "25000"     |
   |                      | (ms)                 | (ms)                 |
   +----------------------+----------------------+----------------------+
   | ----                 | Event Elapsed Timer  | Event Elapsed Timer  |
   |                      | Name(s): "Time Since | Name(s): "Time Since |
   |                      | Exercise Halted"     | Exercise Halted"     |
   +----------------------+----------------------+----------------------+
   | View Code Sequence:  | View Code Sequence:  | View Code Sequence:  |
   +----------------------+----------------------+----------------------+
   | >Code Value:         | >Code Value:         | >Code Value:         |
   | "399139001"          | "399139001"          | "399306005"          |
   +----------------------+----------------------+----------------------+
   | >Coding Scheme       | >Coding Scheme       | >Coding Scheme       |
   | Designator: "SCT"    | Designator: "SCT"    | Designator: "SCT"    |
   +----------------------+----------------------+----------------------+
   | >Code Meaning:       | >Code Meaning:       | >Code Meaning:       |
   | "Parasternal long    | "Parasternal long    | "Parasternal short   |
   | axis"                | axis"                | axis"                |
   +----------------------+----------------------+----------------------+

.. _sect_K.5.3:

Extra-protocol Image Identification
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

At any Stage of a Staged Protocol exam, the operator may acquire images
that are not part of the Protocol. These images are so-called
"extra-Protocol images". Information regarding the performed Protocol is
still included because such images are acquired in the same Procedure
Step as the Protocol images. The Stage number and optionally other Stage
identification Attributes (Stage Name and/or Stage Code Sequence) should
still be conveyed in extra-Protocol images. However, the View number
should be omitted to signify that the image is not one of the standard
Views in the Protocol. Other View identifying information, such as name
or code sequences, may indicate the image location.

.. table:: Comparison Of Protocol And Extra-Protocol Image Attributes
Example

   +----------------------------------+----------------------------------+
   | **Mid-Stress Stage - View 1**    | **Mid-Stress Stage**             |
   |                                  |                                  |
   | **Protocol Image**               | **Extra-Protocol Image**         |
   +==================================+==================================+
   | Study Instance UID:              | Study Instance UID:              |
   |                                  |                                  |
   | "1.2.840….123.1"                 | "1.2.840….123.1"                 |
   +----------------------------------+----------------------------------+
   | Request Attributes Sequence:     | Request Attributes Sequence:     |
   +----------------------------------+----------------------------------+
   | >Scheduled Procedure Step        | >Scheduled Procedure Step        |
   | Description: " Exercise stress   | Description: " Exercise stress   |
   | echocardiography protocol"       | echocardiography protocol"       |
   +----------------------------------+----------------------------------+
   | >Scheduled Protocol Code         | >Scheduled Protocol Code         |
   | Sequence:                        | Sequence:                        |
   +----------------------------------+----------------------------------+
   | >>Code Value: " 433233004"       | >>Code Value: " 433233004"       |
   +----------------------------------+----------------------------------+
   | >>Coding Scheme Designator:      | >>Coding Scheme Designator:      |
   | "SCT"                            | "SCT"                            |
   +----------------------------------+----------------------------------+
   | >>Code Meaning:" Exercise stress | >>Code Meaning:" Exercise stress |
   | echocardiography"                | echocardiography"                |
   +----------------------------------+----------------------------------+
   | Performed Procedure Step         | Performed Procedure Step         |
   | Description: "Exercise stress    | Description: "Exercise stress    |
   | echocardiography"                | echocardiography"                |
   +----------------------------------+----------------------------------+
   | Protocol Name:                   | Protocol Name:                   |
   |                                  |                                  |
   | "EXERCISE STRESS-ECHO"           | "EXERCISE STRESS-ECHO"           |
   +----------------------------------+----------------------------------+
   | Performed Protocol Code          | Performed Protocol Code          |
   | Sequence:                        | Sequence:                        |
   +----------------------------------+----------------------------------+
   | >Code Value: "433233004"         | >Code Value: "433233004"         |
   +----------------------------------+----------------------------------+
   | >Coding Scheme Designator: "SCT" | >Coding Scheme Designator: "SCT" |
   +----------------------------------+----------------------------------+
   | >Code Meaning:" Exercise stress  | >Code Meaning:" Exercise stress  |
   | echocardiography"                | echocardiography"                |
   +----------------------------------+----------------------------------+
   | Number of Stages: "4"            | Number of Stages: "4"            |
   +----------------------------------+----------------------------------+
   | Number of Views In Stage: "2"    | Number of Views In Stage: "2"    |
   +----------------------------------+----------------------------------+
   | Stage Name: "MID-STRESS"         | Stage Name: "MID-STRESS"         |
   +----------------------------------+----------------------------------+
   | Stage Number: "2"                | Stage Number: "2"                |
   +----------------------------------+----------------------------------+
   | Stage Code Sequence:             | Stage Code Sequence:             |
   +----------------------------------+----------------------------------+
   | >Code Value: "109091"            | >Code Value: "109091"            |
   +----------------------------------+----------------------------------+
   | >Coding Scheme Designator: "DCM" | >Coding Scheme Designator: "DCM" |
   +----------------------------------+----------------------------------+
   | >Code Meaning: "Cardiac Stress   | >Code Meaning: "Cardiac Stress   |
   | state"                           | state"                           |
   +----------------------------------+----------------------------------+
   | View Name: "Para-sternal long    | ----                             |
   | axis"                            |                                  |
   +----------------------------------+----------------------------------+
   | View Number: "1"                 | ----                             |
   +----------------------------------+----------------------------------+
   | View Code Sequence:              | ----                             |
   +----------------------------------+----------------------------------+
   | >Code Value: "399139001"         | ----                             |
   +----------------------------------+----------------------------------+
   | >Coding Scheme Designator: "SCT" | ----                             |
   +----------------------------------+----------------------------------+
   | >Code Meaning: "Parasternal long | ----                             |
   | axis"                            |                                  |
   +----------------------------------+----------------------------------+

.. _sect_K.5.4:

Multiple Images of A Stage-view
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

Ultrasound systems often acquire multiple images at a particular stage
and view. If one image is difficult to interpret or does not fully
portray the ventricle wall, the physician may choose to view an
alternate. In some cases, the user may identify the preferred image. The
Key Object Selection Document can identify the preferred image for any
or all of the Stage-Views. This specific usage of the Key Object
Selection Document has a Document Title of (113013, DCM, "Best In Set")
and Document Title Modifier of (113017, DCM, "Stage-View").

.. _sect_K.5.5:

Workflow Management of Staged Protocol Images
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

.. _sect_K.5.5.1:

Uninterrupted Exams - Single MPPS
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

Modality Performed Procedure Step (MPPS) is the basic organizational
unit of Staged Protocol Exams. It is recommended that a single MPPS
instance encompass the entire acquisition of an ultrasound Staged
Protocol Exam if possible.

There are no semantics assigned to the use of Series within a Staged
Protocol Exam other than the DICOM requirements as to the relationship
between Series and Modality Performed Procedure Steps. In particular,
all of the following scenarios are possible:

-  one Series for all images in the MPPS.

-  separate Series for Protocol View images and extra-Protocol images in
   the MPPS.

-  separate Series for images of each Stage within the MPPS.

-  more than one Series for the images acquired in a single Protocol
   Stage.

There is no recommendation on the organization of images into Series
because clinical events make such recommendations impractical.
`figure_title <#figure_K.5.5-1>`__ shows a possible sequence of
interactions for a protocol performed as a single MPPS.

.. _sect_K.5.5.2:

Interrupted Exams - Multiple MPPS
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

A special case arises when the acquisition during a Protocol Stage is
halted for some reason. For example, such a situation can occur if signs
of patient distress are observed, such as angina in a cardiac stress
exam. These criteria are part of the normal exam Protocol, and as long
as the conditions defined for the Protocol are met the MPPS status is
set to COMPLETED. Only if the exam terminates before meeting the minimum
acquisition requirements of the selected Protocol would MPPS status be
set to DISCONTINUED. It is recommended that the reason for
discontinuation should be conveyed in the Modality Procedure Step
Discontinuation Reason Code Sequence (0040,0281). Staged Protocols
generally include criteria for ending the exam, such as when a target
time duration is reached or if signs of patient distress are observed.

If a Protocol Stage is to be acquired at a later time with the intention
of using an earlier completed Protocol Stage of a halted Staged Protocol
then a new Scheduled Procedure Step may or may not be created for this
additional acquisition. Workflow management recommendations vary
depending on whether the care institution decides to create a new
Scheduled Procedure Step or not.

Follow-up Stages must use View Numbers, Names, and Code Sequences
identical to those in the prior Stages to enable automatically
correlating images of the original and follow-up Stages.

**K.5.5.2.1 Unscheduled Follow-up Stages**

Follow-up Stages require a separate MPPS. Since follow-up stages are
part of the same Requested Procedure and Scheduled Procedure Step, all
acquired image SOP Instances and generated MPPS instances specify the
same Study Instance UID. If the Study Instance UID is different, systems
will have difficulty associating related images. This creates a
significant problem if Modality Worklist is not supported. Therefore
systems should assign the same Study Instance UID for follow-up Stages
even if Modality Worklist is not supported.
`figure_title <#figure_K.5.5-2>`__ shows a possible interaction sequence
for this scenario.

.. _sect_K.5.5.2.2:

Scheduled Follow-up Stages
''''''''''''''''''''''''''

In some cases a new Scheduled Procedure Step is created to acquire
follow-up Stages. For example, a drug induced stress-echo exam may be
scheduled because an earlier exercise induced stress-echo exam had to be
halted due to patient discomfort. In such cases it would be redundant to
reacquire earlier Stages such as the rest Stage of a cardiac stress-echo
ultrasound exam. One MPPS contains the Image instances of the original
Stage and a separate MPSS contains the follow-up instances.

If Scheduled and Performed Procedure Steps for Staged Protocol Exam data
use the same Study Instance UID, workstations can associate images from
the original and follow-up Stages. `figure_title <#figure_K.5.5-3>`__
shows a possible interaction sequence for this scenario.

