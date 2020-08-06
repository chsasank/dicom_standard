.. _chapter_C:

Waveforms (Informative)
=======================

This Annex was formerly located in in the 2003 and earlier revisions of
the Standard.

.. _sect_C.1:

Domain of Application
---------------------

Waveform acquisition is part of both the medical imaging environment and
the general clinical environment. Because of its broad use, there has
been significant previous and complementary work in waveform
standardization of which the following are particularly important:

ASTM E31.16 - E1467
   Specification for Transferring Digital Neurophysiological Data
   Between Independent Computer Systems

CEN TC251 PT5-007 - prENV1064 draft
   Standard Communications Protocol for Computer-Assisted
   Electrocardiography (SCP-ECG).

CEN TC251 PT5-021 - draft
   Vital Signs Information Representation Standard (VITAL)

HL7 Automated Data SIG
   HL7 Version 2.3, Chapter 7.14-20

IEEE P1073 - draft
   Medical Information Bus Standard (MIB)

DICOM
   Standalone Curve Information Object Definition

For DICOM, the domain of waveform standardization is waveform
acquisition within the imaging context. It is specifically meant to
address waveform acquisitions that will be analyzed with other data that
is transferred and managed using the DICOM protocol. It allows the
addition of waveform data to that context with minimal incremental cost.
Further, it leverages the DICOM persistent object capability for
maintaining referential relationships to other data collected in a
multi-modality environment, including references necessary for
multi-modality synchronization.

Waveform interchange in other clinical contexts may use different
protocols more appropriate to those domains. In particular, HL7 may be
used for transfer of waveform observations to general clinical
information systems, and MIB may be used for real-time physiological
monitoring and therapy.

The waveform information object definition in DICOM has been
specifically harmonized at the semantic level with the HL7 waveform
message format. The use of a common object model allows straightforward
transcoding and interoperation between systems that use DICOM for
waveform interchange and those that use HL7, and may be viewed as an
example of common semantics implemented in the differing syntaxes of two
messaging systems.

.. note::

   HL7 allows transport of DICOM SOP Instances (information objects)
   encapsulated within HL7 messages. Since the DICOM and HL7 waveform
   semantics are harmonized, DICOM Waveform SOP Instances need not be
   transported as encapsulated data, as they can be transcoded to native
   HL7 Waveform Observation format.

.. _sect_C.2:

Use Cases
---------

The following are specific use case examples for waveforms in the
imaging environment.

-  *Case 1: Catheterization Laboratory* - During a cardiac
   catheterization, several independent pieces of data acquisition
   equipment may be brought together for the exam. An
   electrocardiographic subsystem records surface ECG waveforms; an
   X-ray angiographic subsystem records motion images; a hemodynamic
   subsystem records intracardiac pressures from a sensor on the
   catheter. These subsystems send their acquired data by network to a
   repository. These data are assembled at an analytic workstation by
   retrieving from the repository. For a left ventriculographic
   procedure, the ECG is used by the physician to determine the time of
   maximum and minimum ventricular fill, and when coordinated with the
   angiographic images, an accurate estimate of the ejection fraction
   can be calculated. For a valvuloplasty procedure, the hemodynamic
   waveforms are used to calculate the pre-intervention and
   post-intervention pressure gradients.

-  *Case 2: Electrophysiology Laboratory* - An electrophysiological exam
   will capture waveforms from multiple sensors on a catheter; the
   placement of the catheter in the heart is captured on an angiographic
   image. At an analytic workstation, the exact location of the sensors
   can thus be aligned with a model of the heart, and the relative
   timing of the arrival of the electrophysiological waves at different
   cardiac locations can be mapped.

-  *Case 3: Stress Exam* - A stress exam may involve the acquisition of
   both ECG waveforms and echocardiographic ultrasound images from
   portable equipment at different stages of the test. The waveforms and
   the echocardiograms are output on an interchange disk, which is then
   input and read at a review station. The physician analyzes both types
   of data to make a diagnosis of cardiac health.

.. _sect_C.3:

Time Synchronization Frame of Reference
---------------------------------------

Synchronization of acquisition across multiple modalities in a single
study (e.g., angiography and electrocardiography) requires either a
shared trigger, or a shared clock. A Synchronization Module within the
Frame of Reference Information Entity specifies the synchronization
mechanism. A common temporal environment used by multiple equipment is
identified by a shared Synchronization Frame of Reference UID. How this
UID is determined and distributed to the participating equipment is
outside the scope of the Standard.

The method used for time synchronization of equipment clocks is
implementation or site specific, and therefore outside the scope of this
proposal. If required, standard time distribution protocols are
available (e.g., NTP, IRIG, GPS).

An informative description of time distribution methods can be found at:
http://web.archive.org/web/20001001065227/http://www.bancomm.com/cntpApp.htm

A second method of synchronizing acquisitions is to utilize a common
reference channel (temporal fiducial), which is recorded in the data
acquired from the several equipment units participating in a study,
and/or that is used to trigger synchronized data acquisitions. For
instance, the "X-ray on" pulse train that triggers the acquisition of
frames for an X-ray angiographic SOP Instance can be recorded as a
waveform channel in a simultaneously acquired hemodynamic waveform SOP
Instance, and can be used to align the different object instances.
Associated with this Supplement are proposed coded entry channel
identifiers to specifically support this synchronization mechanism
(DICOM Terminology Mapping Resource Context Group ID 3090).

.. _sect_C.4:

Waveform Acquisition Model
--------------------------

`figure_title <#figure_C.4-1>`__ shows a canonical model of waveform
data acquisition. A patient is the subject of the study. There may be
several sensors placed at different locations on or in the patient, and
waveforms are measurements of some physical quality (metric) by those
sensors (e.g., electrical voltage, pressure, gas concentration, or
sound). The sensor is typically connected to an amplifier and filter,
and its output is sampled at constant time intervals and digitized. In
most cases, several signal channels are acquired synchronously. The
measured signal usually originates in the anatomy of the patient, but an
important special case is a signal that originates in the equipment,
either as a stimulus, such as a cardiac pacing signal, as a therapy,
such as a radio frequency signal used for ablation, or as a
synchronization signal.

.. _sect_C.5:

Waveform Information Model
--------------------------

The part of the composite information object that carries the waveform
data is the Waveform Information Entity (IE). The Waveform IE includes
the technical parameters of waveform acquisition and the waveform
samples.

The information model, or internal organizational structure, of the
Waveform IE is shown in `figure_title <#figure_C.5-1>`__. A waveform
information object includes data from a continuous time period during
which signals were acquired. The object may contain several multiplex
groups, each defined by digitization with the same clock whose frequency
is defined for the group. Within each multiplex group there will be one
or more channels, each with a full technical definition. Finally, each
channel has its set of digital waveform samples.

.. _sect_C.6:

Harmonization With HL7
----------------------

This Waveform IE definition is harmonized with the HL7 waveform semantic
constructs, including the channel definition Attributes and the use of
multiplex groups for synchronously acquired channels. The use of a
common object model allows straightforward transcoding and
interoperation between systems that use DICOM for waveform interchange
and those that use HL7, and may be viewed as an example of common
semantics implemented in the differing syntaxes of two messaging
systems.

This section describes the congruence between the DICOM Waveform IE and
the HL7 version 2.3 waveform message format (see HL7 version 2.3 Chapter
7, sections 7.14 - 7.20).

.. _sect_C.6.1:

HL7 Waveform Observation
~~~~~~~~~~~~~~~~~~~~~~~~

Waveforms in HL7 messages are sent in a set of OBX (Observation)
Segments. Four subtypes of OBX segments are defined:

-  The CHN subtype defines one channel in a CD (Channel Definition) Data
   Type

-  The TIM subtype defines the start time of the waveform data in a TS
   (Time String) Data Type

-  The WAV subtype carries the waveform data in an NA (Numeric Array) or
   MA (Multiplexed Array) Data Type (ASCII encoded samples, character
   delimited)

-  The ANO subtype carries an annotation in a CE (Coded Entry) Data Type
   with a reference to a specific time within the waveform to which the
   annotation applies

Other segments of the HL7 message definition specify patient and study
identification, whose harmonization with DICOM constructs is not defined
in this Annex.

.. _sect_C.6.2:

Channel Definition
~~~~~~~~~~~~~~~~~~

The Waveform Module Channel Definition sequence Attribute (003A,0200) is
defined in harmonization with the HL7 Channel Definition (CD) Data Type,
in accordance with the following Table. Each Item in the Channel
Definition sequence Attribute corresponds to an OBX Segment of subtype
CHN.

.. table:: Correspondence Between DICOM and HL7 Channel Definition

   +--------------------------+-------------+--------------------------+
   | DICOM Attribute          | DICOM Tag   | HL7 CD Data Type         |
   |                          |             | Component                |
   +==========================+=============+==========================+
   | Waveform Channel Number  | (003A,0202) | Channel Identifier       |
   |                          |             | (number&name)            |
   +--------------------------+-------------+--------------------------+
   | Channel Label            | (003A,0203) |                          |
   +--------------------------+-------------+--------------------------+
   | Channel Source Sequence  | (003A,0208) | Waveform Source          |
   +--------------------------+-------------+--------------------------+
   | Channel Source Modifier  | (003A,0209) |                          |
   | Sequence                 |             |                          |
   +--------------------------+-------------+--------------------------+
   | Channel Sensitivity      | (003A,0210) | Channel Sensitivity and  |
   |                          |             | Units                    |
   +--------------------------+-------------+--------------------------+
   | Channel Sensitivity      | (003A,0211) |                          |
   | Units Sequence           |             |                          |
   +--------------------------+-------------+--------------------------+
   | Channel Sensitivity      | (003A,0212) | Channel Calibration      |
   | Correction Factor        |             | Parameters               |
   |                          |             |                          |
   |                          |             | (correctionf             |
   |                          |             | actor&baseline&timeskew) |
   +--------------------------+-------------+--------------------------+
   | Channel Baseline         | (003A,0213) |                          |
   +--------------------------+-------------+--------------------------+
   | Channel Time Skew        | (003A,0214) |                          |
   +--------------------------+-------------+--------------------------+
   | [Group] Sampling         | (003A,001A) | Channel Sampling         |
   | Frequency                |             | Frequency                |
   +--------------------------+-------------+--------------------------+
   | Channel Minimum Value    | (5400,0110) | Minimum and Maximum Data |
   |                          |             | Values                   |
   |                          |             |                          |
   |                          |             | (minimum & maximum)      |
   +--------------------------+-------------+--------------------------+
   | Channel Maximum Value    | (5400,0112) |                          |
   +--------------------------+-------------+--------------------------+
   | Channel Offset           | (003A,0218) | not defined in HL7       |
   +--------------------------+-------------+--------------------------+
   | Channel Status           | (003A,0205) |                          |
   +--------------------------+-------------+--------------------------+
   | Filter Low Frequency     | (003A,0220) |                          |
   +--------------------------+-------------+--------------------------+
   | Filter High Frequency    | (003A,0221) |                          |
   +--------------------------+-------------+--------------------------+
   | Notch Filter Frequency   | (003A,0222) |                          |
   +--------------------------+-------------+--------------------------+
   | Notch Filter Bandwidth   | (003A,0223) |                          |
   +--------------------------+-------------+--------------------------+

In the DICOM information object definition, the sampling frequency is
defined for the multiplex group, while in HL7 it is defined for each
channel, but is required to be identical for all multiplexed channels.

Note that in the HL7 syntax, Waveform Source is a string, rather than a
coded entry as used in DICOM. This should be considered in any
transcoding between the two formats.

.. _sect_C.6.3:

Timing
~~~~~~

In HL7, the exact start time for waveform data is sent in an OBX Segment
of subtype TIM. The corresponding DICOM Attributes, which must be
combined to form the equivalent time string, are:

=========================== ===========
Acquisition DateTime        (0008,002A)
Multiplex Group Time Offset (0018,1068)
=========================== ===========

.. _sect_C.6.4:

Waveform Data
~~~~~~~~~~~~~

The DICOM binary encoding of data samples in the Waveform Data
(5400,1010) corresponds to the ASCII representation of data samples in
the HL7 OBX Segment of subtype WAV. The same channel-interleaved
multiplexing used in the HL7 MA (Multiplexed Array) Data Type is used in
the DICOM Waveform Data Attribute.

Because of its binary representation, DICOM uses several data elements
to specify the precise encoding, as listed in the following Table. There
are no corresponding HL7 data elements, since HL7 uses explicit
character-delimited ASCII encoding of data samples.

============================== ===========
Number of Waveform Channels    (003A,0005)
Number of Waveform Samples     (003A,0010)
Waveform Bits Stored           (003A,021A)
Waveform Bits Allocated        (5400,1004)
Waveform Sample Interpretation (5400,1006)
Waveform Padding Value         (5400,100A)
============================== ===========

.. _sect_C.6.5:

Annotation
~~~~~~~~~~

In HL7, Waveform Annotation is sent in an OBX Segment of subtype ANO,
using the CE (Coded Entry) Data Type CE. This corresponds precisely to
the DICOM Annotation using Coded Entry Sequences. However, HL7
annotation ROI is to a single point only (time reference), while DICOM
allows reference to ranges of samples delimited by time or by explicit
sample position.

.. _sect_C.7:

Harmonization With SCP-ECG
--------------------------

The SCP-ECG standard is designed for recording routine resting
electrocardiograms. Such ECGs are reviewed prior to cardiac imaging
procedures, and a typical use case would be for SCP-ECG waveforms to be
translated to DICOM for inclusion with the full cardiac imaging patient
record.

SCP-ECG provides for either simultaneous or non-simultaneous recording
of the channels, but does not provide a multiplexed data format (each
channel is separately encoded). When translating to DICOM, each subset
of simultaneously recorded channels may be encoded in a Waveform
Sequence Item (multiplex group), and the delay to the recording of each
multiplex group shall be encoded in the Multiplex Group Time Offset
(0018,1068).

The electrode configuration of SCP-ECG Section 1 may be translated to
the DICOM Acquisition Context (0040,0555) sequence items using and
Context Groups 3263 and 3264.

The lead identification of SCP-ECG Section 3, a term coded as an
unsigned integer, may be translated to the DICOM Waveform Channel Source
(003A,0208) coded sequence using .

Pacemaker spike records of SCP-ECG Section 7 may be translated to items
in the Waveform Annotations Sequence (0040,B020) with a code term from .
The annotation sequence item may record the spike amplitude in its
Numeric Value and Measurement Units Attributes.

