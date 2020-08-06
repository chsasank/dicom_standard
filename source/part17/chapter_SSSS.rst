.. _chapter_SSSS:

Neurophysiology Waveforms
=========================

.. _sect_SSSS.1:

Purpose of This Annex
---------------------

This Annex describes the most common types, methods and use cases
associated with the capture and usage of clinical neurophysiology
waveforms.

.. _sect_SSSS.1.1:

Electroencephalography
~~~~~~~~~~~~~~~~~~~~~~

Electroencephalography(EEG) is a diagnostic technique recording the
electrical activity of the brain. Usually the electrodes are placed on
the scalp; special techniques use electrodes implanted extracranially as
well, such as sphenoidal electrodes.

EEG is used to diagnose seizure disorders and epilepsy, to monitor EEG
background activity in certain conditions such as encephalopathy,
anesthesia and coma, and within polysomnography studies. In clinical
practice, an EEG is typically recorded for 20-60 minutes. Long term
monitoring (e.g., to monitor epilepsy) may last from one hours to
several days. In both cases often video of the patient is recorded as
well.

Within polysomnography recordings, the EEG is used to delineate wake and
sleep stages and diagnosis of parasomnias and nocturnal epilepsy.

Electrical potentials are typically in the range of 1-500 µV.

.. _sect_SSSS.1.2:

Electromyography
~~~~~~~~~~~~~~~~

Electromyography (EMG) is a diagnostic technique recording the
electrical activity of skeletal muscles. The electrical potential of the
muscle cells changes on activation, due to a patient's movement or
triggered by external stimulation. The data are used to detect
neuromuscular abnormalities or to monitor muscular activity. In
polysomnography, electromyography is used to measure muscle tension and
movement.

Two different techniques are used.Surface EMG assesses muscle function
by recording electrical potentials from muscle using macroelectrodes at
the skin surface.Intramuscular EMG uses needle electrodes inserted
through the skin into the muscle, often in combination with surface
electrodes as reference.

Within Polysomnography only surface EMG is used.

Measured values are typically in the range of 50 µV - 30mV.

.. _sect_SSSS.1.3:

Electrooculography
~~~~~~~~~~~~~~~~~~

Electrooculography (EOG) is a diagnostic technique to record eye
movement using electrodes placed on the skin surface around the eye. EOG
is used in polysomnography studies to help define the sleep stage (such
as in rapid eye movement sleep) and in EEG to help differentiate eye
movement artifact from frontal EEG patterns.

Typically two electrodes are used to measure the eye movement. They are
placed above or below the outer canthus of the eyes.

Measured values and sampling rates are approximately in the same range
as EEG.

.. _sect_SSSS.1.4:

Body Position
~~~~~~~~~~~~~

Continuous monitoring of the patient's position synchronously to the
recording of neurophysiology data is an essential requirement especially
in polysomnography.

Besides using synchronized video, body position can be monitored with
various body position monitoring devices. Different techniques are used,
e.g. simple mercury switches or acceleration sensors providing six data
channels with angles and acceleration relatively to gravity.

Two types of data collection are common in polysomnography.

The first uses a single channel and records five discrete, defined
values indicating the patient position: prone, lateral decubitus left,
supine, lateral decubitus right, and upright.

The second used two channels to record two angles. The first channel
records the patient's angle of rotation around the longitudinal axis
(head-feet axis). An angle of zero indicates supine, and angle of 90°
indicates left lateral decubitus, and angle of 180° indicates prone, and
an angle of 270° indicates right lateral decubitus. The second channel
records the angle of elevation of the patient against horizontal, which
could change if the patient sits up in bed, if the head of the bed is
elevated, or if the patient stands up. An angle of zero indicates the
patient is lying flat, an angle of 90° indicates upright, and an angle
of -90° indicates complete reverse Trendelenburg position with the head
down and the legs pointed straight up.

======================= ========= =========
Position Value          Channel I Channel 2
======================= ========= =========
Supine                  0         0
Lateral decubitus left  90        0
Prone                   180       0
Lateral decubitus right 270       0
Upright                 0         90
Feet up                 0         -90
======================= ========= =========

The sampling rate varies but is relatively slow (60 Hz or less).

.. _sect_SSSS.1.5:

Polysomnography
~~~~~~~~~~~~~~~

In sleep medicine, polysomnography (PSG) , also called a "sleep study",
is a test to diagnose sleep disorders.Physiological parameters are
recorded during sleep in order to identify the sleep stages, measure
brain functioning, monitor respiratory control, and monitor patient
movement and body position.

A polysomnography study consists of several measured quantities, the
most important ones are:

-  brain activity (EEG)

-  eye movements (EOG)

-  activity of skeletal muscles (EMG)

Additionally some of the following parameters are recorded:

-  electrical activity of the heart (ECG)

-  changes in blood oxygen levels (pulse oximetry)

-  respiratory parameters like nasal and oral airflow via pressure
   transducers in front of nostrils and mouth or chest and abdominal
   expansion during breathing (via belts)

-  sound recordings to measure snoring

-  body position

Data acquisition is done via a multichannel recording unit which samples
sensors attached to different parts of the patient's body. Study
duration is typically up to 8 hours. Channelselection varies somewhat
between labs. Recommended channels for PSG are defined by the American
Academy of Sleep Medicine (Reference: Berry RB, Albertario CL, Harding
SM, et al.; for the American Academy of Sleep Medicine. The AASM Manual
for the Scoring of Sleep and Associated Events: Rules, Terminology and
Technical Specifications. Version 2.5. Darien, IL: American Academy of
Sleep Medicine; 2018).

In many cases a video is taken to show the person's movements during
sleep.

.. _sect_SSSS.1.5.1:

Mapping of Polysomnographic Data to DICOM
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

Neurophysiology time series SOP Classes relevant to sleep studies are:

Sleep Electroencephalogram Waveform Storage
   The Sleep Electroencephalogram (EEG) Waveform Storage SOP Class is
   the specification of digitized electrical signals from the patient's
   encephalon collected on the skull surface, which has been acquired by
   an EEG modality or by an EEG acquisition function within a
   polysomnography modality.

Electromyogram Waveform Storage
   The Electromyography (EMG) Waveform Storage SOP Class is the
   specification of digitized electrical signals evoked by the patient's
   muscle movements collected on the skin, which has been acquired by an
   EMG modality or by an EMG acquisition function within a
   neurophysiology recording device or a polysomnography modality.

Electrooculogram Waveform Storage
   The Electrooculogram (EOG) Waveform Storage SOP Class is the
   specification of digitized electrical signals evoked by the patient's
   eye movements collected on the face, which has been acquired by an
   EOG modality or by an EOG acquisition function within a
   neurophysiology recording device or a polysomnography modality.

Non-neurophysiologic time series or video SOP Classes relevant to sleep
studies, are:

General ECG Waveform Storage
   The General Electrocardiogram (ECG) Storage SOP Class is used to
   store digitized electrical signals from the patient cardiac
   conduction system collected on the body surface, which has been
   acquired by an ECG modality or by an ECG acquisition function within
   an imaging modality or a recording device.

Basic Voice Audio Waveform Storage
   The Basic Voice Audio Storage SOP Class is used to store digitized
   sound that has been acquired or created by an audio modality or by an
   audio acquisition function within an imaging modality or a recording
   device. A typical use is report dictation. In the context of
   Polysomnography this object could be used for snoring detection

Arterial Pulse Waveform Storage
   The Arterial Pulse Waveform Storage SOP Class is used to store
   digitized electrical signals from the patient arterial system
   collected through pulse oximetry or other means by a Pulse modality
   or by a Pulse acquisition function within an imaging modality or a
   recording device. In the context of polysomnography this object could
   be used to record the oxygen saturation in blood.

Respiratory Waveform Storage and Multi-channel Respiratory Waveform Storage
   The Respiratory Waveform Storage SOP Classes are used to store
   digitized electrical signals from the respiratory system, acquired by
   a Respiratory modality or by a Respiratory acquisition function
   within an imaging modality or a recording device. In the context of
   polysomnography this object could be used to record the patient's
   respiration.

Body Position Waveform Storage
   The Body Position Waveform Storage SOP Class is the specification of
   digitized electrical signals, which have been acquired by adevice or
   sensor on the patient's body. Depending on the measurement method
   either the acquired sensor data or values derived from it are
   recorded.

Video Photographic Image Storage
   Video Photographic Image Storage Storage SOP Class is used to store
   visible light multiframe photographic images. This SOP Class is used
   to store the video data acquired during Video-EEG or in
   polysomnography.

.. _sect_SSSS.1.6:

Considerations On Storing Large Data Recordings
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

In principle, continuous recordings are stored within a single DICOM
object, i.e., as a single file, as long as the limits resulting from
DICOM data restrictions are not exceeded.

The length of Waveform Data (0054,1010), in which all of the data for a
single channel is encoded, is limited to 4 GB of data by the 32 Bit
unsigned integer used to store the length in bytes of the data element

For example, using 24 channels within one multiplex group, a sampling
frequency of 256 Hz, and 16 Bit samples would allow amaximum recording
time of more than 3 days.

Enhanced neurophysiology techniques like High Density EEG using 512
channels and a sampling frequencyof 5 kHz would reach this limit in less
than 15 minutes, if all channels were stored within one multiplex group.

The file system or database, in which the DICOM data is stored, may
place additional constraints on the total size of the DICOM object.

When such limits are reached, the recording has to be split into several
objects with appropriate offsets and times. Synchronization has to be
provided across such multiple objects.

To keep the data objects easy to handle, long duration recordings could
be split in time slices of e.g., single days.

In addition, it may be desirable to use smaller objects to address
reliability and random access concerns.

Such objects consisting of one recording being split to multiple parts
shall belong to the same series.

.. _sect_SSSS.1.7:

Example DICOM Routine Scalp EEG Waveform Object
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

Setup: 24 leads: 1 ECG, 23 EEG

`table_title <#table_SSSS.1.7-1>`__ is a non-comprehensive sample
representation of a 23-lead Routine EEG object.

.. table:: Sample representation of a 23-lead Routine EEG object

   +----------+-----------+-----------+----+----------+-----------+
   | Nesting  | Attribute | Tag       | VR | VL (hex) | Value     |
   +==========+===========+===========+====+==========+===========+
   |          | SOP Class | (0        | UI | 001C     | 1.        |
   |          | UID       | 008,0016) |    |          | 2.840.100 |
   |          |           |           |    |          | 08.5.1.4. |
   |          |           |           |    |          | 1.1.9.7.1 |
   +----------+-----------+-----------+----+----------+-----------+
   |          | SOP       | (0        | UI | 0036     | 1.3.6.1.  |
   |          | Instance  | 008,0018) |    |          | 4.1.23154 |
   |          | UID       |           |    |          | .1.4.2881 |
   |          |           |           |    |          | 783832.12 |
   |          |           |           |    |          | 156.15335 |
   |          |           |           |    |          | 48323.951 |
   +----------+-----------+-----------+----+----------+-----------+
   |          | Study     | (0        | DA | 0008     | 20000101  |
   |          | Date      | 008,0020) |    |          |           |
   +----------+-----------+-----------+----+----------+-----------+
   |          | Content   | (0        | DA | 0008     | 20180806  |
   |          | Date      | 008,0023) |    |          |           |
   +----------+-----------+-----------+----+----------+-----------+
   |          | Ac        | (0        | DT | 0016     | 200       |
   |          | quisition | 008,002a) |    |          | 001010000 |
   |          | Date Time |           |    |          | 00.000000 |
   +----------+-----------+-----------+----+----------+-----------+
   |          | Study     | (0        | TM | 000e     | 0000      |
   |          | Time      | 008,0030) |    |          | 00.000000 |
   +----------+-----------+-----------+----+----------+-----------+
   |          | Content   | (0        | TM | 0006     | 113843    |
   |          | Time      | 008,0033) |    |          |           |
   +----------+-----------+-----------+----+----------+-----------+
   |          | Accession | (0        | SH | 0008     | 76123455  |
   |          | Number    | 008,0050) |    |          |           |
   +----------+-----------+-----------+----+----------+-----------+
   |          | Modality  | (0        | CS | 0004     | EEG       |
   |          |           | 008,0060) |    |          |           |
   +----------+-----------+-----------+----+----------+-----------+
   |          | Man       | (0        | LO | 0014     | so        |
   |          | ufacturer | 008,0070) |    |          | meManufac |
   |          |           |           |    |          | turerName |
   +----------+-----------+-----------+----+----------+-----------+
   |          | Referring | (0        | PN | 0000     |           |
   |          | Ph        | 008,0090) |    |          |           |
   |          | ysician's |           |    |          |           |
   |          | Name      |           |    |          |           |
   +----------+-----------+-----------+----+----------+-----------+
   |          | Patient's | (0        | PN | 000c     | PAT       |
   |          | Name      | 010,0010) |    |          | IENT1^edf |
   +----------+-----------+-----------+----+----------+-----------+
   |          | Patient   | (0        | LO | 000a     | s         |
   |          | ID        | 010,0020) |    |          | sspid0815 |
   +----------+-----------+-----------+----+----------+-----------+
   |          | Patient's | (0        | DA | 0008     | 19670329  |
   |          | Birth     | 010,0030) |    |          |           |
   |          | Date      |           |    |          |           |
   +----------+-----------+-----------+----+----------+-----------+
   |          | Patient's | (0        | CS | 0002     | F         |
   |          | Sex       | 010,0040) |    |          |           |
   +----------+-----------+-----------+----+----------+-----------+
   |          | Synchr    | (0        | CS | 000a     | NO        |
   |          | onization | 018,106a) |    |          | TRIGGER   |
   |          | Trigger   |           |    |          |           |
   +----------+-----------+-----------+----+----------+-----------+
   |          | Ac        | (0        | CS | 0002     | Y         |
   |          | quisition | 018,1800) |    |          |           |
   |          | Time      |           |    |          |           |
   |          | Syn       |           |    |          |           |
   |          | chronized |           |    |          |           |
   +----------+-----------+-----------+----+----------+-----------+
   |          | Study     | (0        | UI | 0036     | 1.3.6.1.  |
   |          | Instance  | 020,000d) |    |          | 4.1.23154 |
   |          | UID       |           |    |          | .1.2.2881 |
   |          |           |           |    |          | 783832.12 |
   |          |           |           |    |          | 156.15335 |
   |          |           |           |    |          | 48324.952 |
   +----------+-----------+-----------+----+----------+-----------+
   |          | Series    | (0        | UI | 0036     | 1.3.6.1.  |
   |          | Instance  | 020,000e) |    |          | 4.1.23154 |
   |          | UID       |           |    |          | .1.3.2881 |
   |          |           |           |    |          | 783832.12 |
   |          |           |           |    |          | 156.15335 |
   |          |           |           |    |          | 48324.953 |
   +----------+-----------+-----------+----+----------+-----------+
   |          | Study ID  | (0        | SH | 0004     | 4711      |
   |          |           | 020,0010) |    |          |           |
   +----------+-----------+-----------+----+----------+-----------+
   |          | Series    | (0        | IS | 0002     | 1         |
   |          | Number    | 020,0011) |    |          |           |
   +----------+-----------+-----------+----+----------+-----------+
   |          | Instance  | (0        | IS | 0002     | 1         |
   |          | Number    | 020,0013) |    |          |           |
   +----------+-----------+-----------+----+----------+-----------+
   |          | Synchr    | (0        | UI | 0036     | 1.3.6.1.  |
   |          | onization | 020,0200) |    |          | 4.1.23154 |
   |          | Frame of  |           |    |          | .1.5.2881 |
   |          | Reference |           |    |          | 783832.12 |
   |          | UID       |           |    |          | 156.15335 |
   |          |           |           |    |          | 48324.954 |
   +----------+-----------+-----------+----+----------+-----------+
   |          | Ac        | (0        | SQ | ffffffff |           |
   |          | quisition | 040,0555) |    |          |           |
   |          | Context   |           |    |          |           |
   |          | Sequence  |           |    |          |           |
   +----------+-----------+-----------+----+----------+-----------+
   | %endseq  |           |           |    |          |           |
   +----------+-----------+-----------+----+----------+-----------+
   |          | Waveform  | (5        | SQ | ffffffff |           |
   |          | Sequence  | 400,0100) |    |          |           |
   +----------+-----------+-----------+----+----------+-----------+
   | %item    |           |           |    |          |           |
   +----------+-----------+-----------+----+----------+-----------+
   |          | Waveform  | (0        | CS | 0008     | ORIGINAL  |
   |          | Or        | 03a,0004) |    |          |           |
   |          | iginality |           |    |          |           |
   +----------+-----------+-----------+----+----------+-----------+
   |          | Number of | (0        | US | 0002     | 0x0017    |
   |          | Waveform  | 03a,0005) |    |          |           |
   |          | Channels  |           |    |          |           |
   +----------+-----------+-----------+----+----------+-----------+
   |          | Number of | (0        | UL | 0004     | 0         |
   |          | Waveform  | 03a,0010) |    |          | x001c1700 |
   |          | Samples   |           |    |          |           |
   +----------+-----------+-----------+----+----------+-----------+
   |          | Sampling  | (0        | DS | 0004     | 256       |
   |          | Frequency | 03a,001a) |    |          |           |
   +----------+-----------+-----------+----+----------+-----------+
   |          | Multiplex | (0        | SH | 0004     | EEG       |
   |          | Group     | 03a,0020) |    |          |           |
   |          | Label     |           |    |          |           |
   +----------+-----------+-----------+----+----------+-----------+
   |          | Channel   | (0        | SQ | ffffffff |           |
   |          | D         | 03a,0200) |    |          |           |
   |          | efinition |           |    |          |           |
   |          | Sequence  |           |    |          |           |
   +----------+-----------+-----------+----+----------+-----------+
   | %item    |           |           |    |          |           |
   +----------+-----------+-----------+----+----------+-----------+
   |          | Waveform  | (0        | IS | 0002     | 1         |
   |          | Channel   | 03a,0202) |    |          |           |
   |          | Number    |           |    |          |           |
   +----------+-----------+-----------+----+----------+-----------+
   |          | Channel   | (0        | SH | 0002     | O1        |
   |          | Label     | 03a,0203) |    |          |           |
   +----------+-----------+-----------+----+----------+-----------+
   |          | Channel   | (0        | SQ | ffffffff |           |
   |          | Source    | 03a,0208) |    |          |           |
   |          | Sequence  |           |    |          |           |
   +----------+-----------+-----------+----+----------+-----------+
   | %item    |           |           |    |          |           |
   +----------+-----------+-----------+----+----------+-----------+
   |          | Code      | (0        | SH | 0006     | 7:1209    |
   |          | Value     | 008,0100) |    |          |           |
   +----------+-----------+-----------+----+----------+-----------+
   |          | Coding    | (0        | SH | 0004     | MDC       |
   |          | Scheme    | 008,0102) |    |          |           |
   |          | D         |           |    |          |           |
   |          | esignator |           |    |          |           |
   +----------+-----------+-----------+----+----------+-----------+
   |          | Code      | (0        | LO | 0002     | O1        |
   |          | Meaning   | 008,0104) |    |          |           |
   +----------+-----------+-----------+----+----------+-----------+
   | %enditem |           |           |    |          |           |
   +----------+-----------+-----------+----+----------+-----------+
   | %endseq  |           |           |    |          |           |
   +----------+-----------+-----------+----+----------+-----------+
   |          | Channel   | (0        | SQ | ffffffff |           |
   |          | Source    | 03a,0209) |    |          |           |
   |          | Modifier  |           |    |          |           |
   |          | Sequence  |           |    |          |           |
   +----------+-----------+-----------+----+----------+-----------+
   | %item    |           |           |    |          |           |
   +----------+-----------+-----------+----+----------+-----------+
   |          | Code      | (0        | SH | 0006     | 109006    |
   |          | Value     | 008,0100) |    |          |           |
   +----------+-----------+-----------+----+----------+-----------+
   |          | Coding    | (0        | SH | 0004     | DCM       |
   |          | Scheme    | 008,0102) |    |          |           |
   |          | D         |           |    |          |           |
   |          | esignator |           |    |          |           |
   +----------+-----------+-----------+----+----------+-----------+
   |          | Code      | (0        | LO | 0014     | Dif       |
   |          | Meaning   | 008,0104) |    |          | ferential |
   |          |           |           |    |          | signal    |
   +----------+-----------+-----------+----+----------+-----------+
   | %enditem |           |           |    |          |           |
   +----------+-----------+-----------+----+----------+-----------+
   | %item    |           |           |    |          |           |
   +----------+-----------+-----------+----+----------+-----------+
   |          | Code      | (0        | SH | 0006     | 7:1020    |
   |          | Value     | 008,0100) |    |          |           |
   +----------+-----------+-----------+----+----------+-----------+
   |          | Coding    | (0        | SH | 0004     | MDC       |
   |          | Scheme    | 008,0102) |    |          |           |
   +----------+-----------+-----------+----+----------+-----------+
   |          | Code      | (0        | LO | 0004     | CPz       |
   |          | Meaning   | 008,0104) |    |          |           |
   +----------+-----------+-----------+----+----------+-----------+
   | %enditem |           |           |    |          |           |
   +----------+-----------+-----------+----+----------+-----------+
   | %endseq  |           |           |    |          |           |
   +----------+-----------+-----------+----+----------+-----------+
   |          | Channel   | (0        | DS | 0008     | 0.100008  |
   |          | Se        | 03a,0210) |    |          |           |
   |          | nsitivity |           |    |          |           |
   +----------+-----------+-----------+----+----------+-----------+
   |          | Channel   | (0        | SQ | ffffffff |           |
   |          | Se        | 03a,0211) |    |          |           |
   |          | nsitivity |           |    |          |           |
   |          | Units     |           |    |          |           |
   |          | Sequence  |           |    |          |           |
   +----------+-----------+-----------+----+----------+-----------+
   | %item    |           |           |    |          |           |
   +----------+-----------+-----------+----+----------+-----------+
   |          | Code      | (0        | SH | 0002     | uV        |
   |          | Value     | 008,0100) |    |          |           |
   +----------+-----------+-----------+----+----------+-----------+
   |          | Coding    | (0        | SH | 0004     | UCUM      |
   |          | Scheme    | 008,0102) |    |          |           |
   |          | D         |           |    |          |           |
   |          | esignator |           |    |          |           |
   +----------+-----------+-----------+----+----------+-----------+
   |          | Code      | (0        | LO | 000a     | uV        |
   |          | Meaning   | 008,0104) |    |          |           |
   +----------+-----------+-----------+----+----------+-----------+
   | %enditem |           |           |    |          |           |
   +----------+-----------+-----------+----+----------+-----------+
   | %endseq  |           |           |    |          |           |
   +----------+-----------+-----------+----+----------+-----------+
   |          | Channel   | (0        | DS | 0002     | 1         |
   |          | Se        | 03a,0212) |    |          |           |
   |          | nsitivity |           |    |          |           |
   |          | C         |           |    |          |           |
   |          | orrection |           |    |          |           |
   |          | Factor    |           |    |          |           |
   +----------+-----------+-----------+----+----------+-----------+
   |          | Channel   | (0        | DS | 000a     | 0.0500038 |
   |          | Baseline  | 03a,0213) |    |          |           |
   +----------+-----------+-----------+----+----------+-----------+
   |          | Channel   | (0        | DS | 0002     | 0         |
   |          | Sample    | 03a,0215) |    |          |           |
   |          | Skew      |           |    |          |           |
   +----------+-----------+-----------+----+----------+-----------+
   |          | Channel   | (0        | DS | 0002     | 0         |
   |          | Offset    | 03a,0218) |    |          |           |
   +----------+-----------+-----------+----+----------+-----------+
   |          | Waveform  | (0        | US | 0002     | 0x0010    |
   |          | Bits      | 03a,021a) |    |          |           |
   |          | Stored    |           |    |          |           |
   +----------+-----------+-----------+----+----------+-----------+
   |          | Channel   | (0        | SQ | ffffffff |           |
   |          | Impedance | 03A,0312) |    |          |           |
   |          | Sequence  |           |    |          |           |
   +----------+-----------+-----------+----+----------+-----------+
   | %item    |           |           |    |          |           |
   +----------+-----------+-----------+----+----------+-----------+
   |          | Impedance | (0        | DS | 0008     | 67        |
   |          | Value     | 03A,0313) |    |          |           |
   +----------+-----------+-----------+----+----------+-----------+
   |          | Impedance | (0        | DT | 0016     | 199       |
   |          | Timepoint | 03A,0314) |    |          | 912312358 |
   |          |           |           |    |          | 35.000000 |
   +----------+-----------+-----------+----+----------+-----------+
   | %enditem |           |           |    |          |           |
   +----------+-----------+-----------+----+----------+-----------+
   | %enditem |           |           |    |          |           |
   +----------+-----------+-----------+----+----------+-----------+
   | %item    |           |           |    |          |           |
   +----------+-----------+-----------+----+----------+-----------+
   |          | Waveform  | (0        | IS | 0002     | 2         |
   |          | Channel   | 03a,0202) |    |          |           |
   |          | Number    |           |    |          |           |
   +----------+-----------+-----------+----+----------+-----------+
   |          | Channel   | (0        | SH | 0002     | P3        |
   |          | Label     | 03a,0203) |    |          |           |
   +----------+-----------+-----------+----+----------+-----------+
   |          | Channel   | (0        | SQ | ffffffff |           |
   |          | Source    | 03a,0208) |    |          |           |
   |          | Sequence  |           |    |          |           |
   +----------+-----------+-----------+----+----------+-----------+
   | %item    |           |           |    |          |           |
   +----------+-----------+-----------+----+----------+-----------+
   |          | Code      | (0        | SH | 0006     | 7:1185    |
   |          | Value     | 008,0100) |    |          |           |
   +----------+-----------+-----------+----+----------+-----------+
   |          | Coding    | (0        | SH | 0004     | MDC       |
   |          | Scheme    | 008,0102) |    |          |           |
   |          | D         |           |    |          |           |
   |          | esignator |           |    |          |           |
   +----------+-----------+-----------+----+----------+-----------+
   |          | Code      | (0        | LO | 0002     | P3        |
   |          | Meaning   | 008,0104) |    |          |           |
   +----------+-----------+-----------+----+----------+-----------+
   | %enditem |           |           |    |          |           |
   +----------+-----------+-----------+----+----------+-----------+
   | %endseq  |           |           |    |          |           |
   +----------+-----------+-----------+----+----------+-----------+
   |          | Channel   | (0        | SQ | ffffffff |           |
   |          | Source    | 03a,0209) |    |          |           |
   |          | Modifier  |           |    |          |           |
   |          | Sequence  |           |    |          |           |
   +----------+-----------+-----------+----+----------+-----------+
   | %item    |           |           |    |          |           |
   +----------+-----------+-----------+----+----------+-----------+
   |          | Code      | (0        | SH | 0006     | 109006    |
   |          | Value     | 008,0100) |    |          |           |
   +----------+-----------+-----------+----+----------+-----------+
   |          | Coding    | (0        | SH | 0004     | DCM       |
   |          | Scheme    | 008,0102) |    |          |           |
   |          | D         |           |    |          |           |
   |          | esignator |           |    |          |           |
   +----------+-----------+-----------+----+----------+-----------+
   |          | Code      | (0        | LO | 0014     | Dif       |
   |          | Meaning   | 008,0104) |    |          | ferential |
   |          |           |           |    |          | signal    |
   +----------+-----------+-----------+----+----------+-----------+
   | %enditem |           |           |    |          |           |
   +----------+-----------+-----------+----+----------+-----------+
   | %item    |           |           |    |          |           |
   +----------+-----------+-----------+----+----------+-----------+
   |          | Code      | (0        | SH | 0006     | 7:1020    |
   |          | Value     | 008,0100) |    |          |           |
   +----------+-----------+-----------+----+----------+-----------+
   |          | Coding    | (0        | SH | 0004     | MDC       |
   |          | Scheme    | 008,0102) |    |          |           |
   +----------+-----------+-----------+----+----------+-----------+
   |          | Code      | (0        | LO | 0004     | CPz       |
   |          | Meaning   | 008,0104) |    |          |           |
   +----------+-----------+-----------+----+----------+-----------+
   | %enditem |           |           |    |          |           |
   +----------+-----------+-----------+----+----------+-----------+
   | %endseq  |           |           |    |          |           |
   +----------+-----------+-----------+----+----------+-----------+
   |          | Channel   | (0        | DS | 0008     | 0.100008  |
   |          | Se        | 03a,0210) |    |          |           |
   |          | nsitivity |           |    |          |           |
   +----------+-----------+-----------+----+----------+-----------+
   |          | Channel   | (0        | SQ | ffffffff |           |
   |          | Se        | 03a,0211) |    |          |           |
   |          | nsitivity |           |    |          |           |
   |          | Units     |           |    |          |           |
   |          | Sequence  |           |    |          |           |
   +----------+-----------+-----------+----+----------+-----------+
   | %item    |           |           |    |          |           |
   +----------+-----------+-----------+----+----------+-----------+
   |          | Code      | (0        | SH | 0002     | uV        |
   |          | Value     | 008,0100) |    |          |           |
   +----------+-----------+-----------+----+----------+-----------+
   |          | Coding    | (0        | SH | 0004     | UCUM      |
   |          | Scheme    | 008,0102) |    |          |           |
   |          | D         |           |    |          |           |
   |          | esignator |           |    |          |           |
   +----------+-----------+-----------+----+----------+-----------+
   |          | Code      | (0        | LO | 000a     | uV        |
   |          | Meaning   | 008,0104) |    |          |           |
   +----------+-----------+-----------+----+----------+-----------+
   | %enditem |           |           |    |          |           |
   +----------+-----------+-----------+----+----------+-----------+
   | %endseq  |           |           |    |          |           |
   +----------+-----------+-----------+----+----------+-----------+
   |          | Channel   | (0        | DS | 0002     | 1         |
   |          | Se        | 03a,0212) |    |          |           |
   |          | nsitivity |           |    |          |           |
   |          | C         |           |    |          |           |
   |          | orrection |           |    |          |           |
   |          | Factor    |           |    |          |           |
   +----------+-----------+-----------+----+----------+-----------+
   |          | Channel   | (0        | DS | 000a     | 0.0500038 |
   |          | Baseline  | 03a,0213) |    |          |           |
   +----------+-----------+-----------+----+----------+-----------+
   |          | Channel   | (0        | DS | 0002     | 0         |
   |          | Sample    | 03a,0215) |    |          |           |
   |          | Skew      |           |    |          |           |
   +----------+-----------+-----------+----+----------+-----------+
   |          | Channel   | (0        | DS | 0002     | 0         |
   |          | Offset    | 03a,0218) |    |          |           |
   +----------+-----------+-----------+----+----------+-----------+
   |          | Waveform  | (0        | US | 0002     | 0x0010    |
   |          | Bits      | 03a,021a) |    |          |           |
   |          | Stored    |           |    |          |           |
   +----------+-----------+-----------+----+----------+-----------+
   | %enditem |           |           |    |          |           |
   +----------+-----------+-----------+----+----------+-----------+
   | %item    |           |           |    |          |           |
   +----------+-----------+-----------+----+----------+-----------+
   |          | Waveform  | (0        | IS | 0002     | 3         |
   |          | Channel   | 03a,0202) |    |          |           |
   |          | Number    |           |    |          |           |
   +----------+-----------+-----------+----+----------+-----------+
   |          | Channel   | (0        | SH | 0002     | C3        |
   |          | Label     | 03a,0203) |    |          |           |
   +----------+-----------+-----------+----+----------+-----------+
   |          | Channel   | (0        | SQ | ffffffff |           |
   |          | Source    | 03a,0208) |    |          |           |
   |          | Sequence  |           |    |          |           |
   +----------+-----------+-----------+----+----------+-----------+
   | %item    |           |           |    |          |           |
   +----------+-----------+-----------+----+----------+-----------+
   |          | Code      | (0        | SH | 0006     | 7:1137    |
   |          | Value     | 008,0100) |    |          |           |
   +----------+-----------+-----------+----+----------+-----------+
   |          | Coding    | (0        | SH | 0004     | MDC       |
   |          | Scheme    | 008,0102) |    |          |           |
   |          | D         |           |    |          |           |
   |          | esignator |           |    |          |           |
   +----------+-----------+-----------+----+----------+-----------+
   |          | Code      | (0        | LO | 0002     | C3        |
   |          | Meaning   | 008,0104) |    |          |           |
   +----------+-----------+-----------+----+----------+-----------+
   | %enditem |           |           |    |          |           |
   +----------+-----------+-----------+----+----------+-----------+
   | %endseq  |           |           |    |          |           |
   +----------+-----------+-----------+----+----------+-----------+
   |          | Channel   | (0        | DS | 0008     | 0.100008  |
   |          | Se        | 03a,0210) |    |          |           |
   |          | nsitivity |           |    |          |           |
   +----------+-----------+-----------+----+----------+-----------+
   |          | Channel   | (0        | SQ | ffffffff |           |
   |          | Se        | 03a,0211) |    |          |           |
   |          | nsitivity |           |    |          |           |
   |          | Units     |           |    |          |           |
   |          | Sequence  |           |    |          |           |
   +----------+-----------+-----------+----+----------+-----------+
   | %item    |           |           |    |          |           |
   +----------+-----------+-----------+----+----------+-----------+
   |          | Code      | (0        | SH | 0002     | uV        |
   |          | Value     | 008,0100) |    |          |           |
   +----------+-----------+-----------+----+----------+-----------+
   |          | Coding    | (0        | SH | 0004     | UCUM      |
   |          | Scheme    | 008,0102) |    |          |           |
   |          | D         |           |    |          |           |
   |          | esignator |           |    |          |           |
   +----------+-----------+-----------+----+----------+-----------+
   |          | Code      | (0        | LO | 000a     | uV        |
   |          | Meaning   | 008,0104) |    |          |           |
   +----------+-----------+-----------+----+----------+-----------+
   | %enditem |           |           |    |          |           |
   +----------+-----------+-----------+----+----------+-----------+
   | %endseq  |           |           |    |          |           |
   +----------+-----------+-----------+----+----------+-----------+
   |          | Channel   | (0        | SQ | ffffffff |           |
   |          | Source    | 03a,0209) |    |          |           |
   |          | Modifier  |           |    |          |           |
   |          | Sequence  |           |    |          |           |
   +----------+-----------+-----------+----+----------+-----------+
   | %item    |           |           |    |          |           |
   +----------+-----------+-----------+----+----------+-----------+
   |          | Code      | (0        | SH | 0006     | 109006    |
   |          | Value     | 008,0100) |    |          |           |
   +----------+-----------+-----------+----+----------+-----------+
   |          | Coding    | (0        | SH | 0004     | DCM       |
   |          | Scheme    | 008,0102) |    |          |           |
   |          | D         |           |    |          |           |
   |          | esignator |           |    |          |           |
   +----------+-----------+-----------+----+----------+-----------+
   |          | Code      | (0        | LO | 0014     | Dif       |
   |          | Meaning   | 008,0104) |    |          | ferential |
   |          |           |           |    |          | signal    |
   +----------+-----------+-----------+----+----------+-----------+
   | %enditem |           |           |    |          |           |
   +----------+-----------+-----------+----+----------+-----------+
   | %item    |           |           |    |          |           |
   +----------+-----------+-----------+----+----------+-----------+
   |          | Code      | (0        | SH | 0006     | 7:1020    |
   |          | Value     | 008,0100) |    |          |           |
   +----------+-----------+-----------+----+----------+-----------+
   |          | Coding    | (0        | SH | 0004     | MDC       |
   |          | Scheme    | 008,0102) |    |          |           |
   +----------+-----------+-----------+----+----------+-----------+
   |          | Code      | (0        | LO | 0004     | CPz       |
   |          | Meaning   | 008,0104) |    |          |           |
   +----------+-----------+-----------+----+----------+-----------+
   | %enditem |           |           |    |          |           |
   +----------+-----------+-----------+----+----------+-----------+
   | %endseq  |           |           |    |          |           |
   +----------+-----------+-----------+----+----------+-----------+
   |          | Channel   | (0        | SQ | ffffffff |           |
   |          | Source    | 03a,0209) |    |          |           |
   |          | Modifier  |           |    |          |           |
   |          | Sequence  |           |    |          |           |
   +----------+-----------+-----------+----+----------+-----------+
   |          | Channel   | (0        | DS | 0002     | 1         |
   |          | Se        | 03a,0212) |    |          |           |
   |          | nsitivity |           |    |          |           |
   |          | C         |           |    |          |           |
   |          | orrection |           |    |          |           |
   |          | Factor    |           |    |          |           |
   +----------+-----------+-----------+----+----------+-----------+
   |          | Channel   | (0        | DS | 000a     | 0.0500038 |
   |          | Baseline  | 03a,0213) |    |          |           |
   +----------+-----------+-----------+----+----------+-----------+
   |          | Channel   | (0        | DS | 0002     | 0         |
   |          | Sample    | 03a,0215) |    |          |           |
   |          | Skew      |           |    |          |           |
   +----------+-----------+-----------+----+----------+-----------+
   |          | Channel   | (0        | DS | 0002     | 0         |
   |          | Offset    | 03a,0218) |    |          |           |
   +----------+-----------+-----------+----+----------+-----------+
   |          | Waveform  | (0        | US | 0002     | 0x0010    |
   |          | Bits      | 03a,021a) |    |          |           |
   |          | Stored    |           |    |          |           |
   +----------+-----------+-----------+----+----------+-----------+
   | %enditem |           |           |    |          |           |
   +----------+-----------+-----------+----+----------+-----------+
   | %item    |           |           |    |          |           |
   +----------+-----------+-----------+----+----------+-----------+
   |          | Waveform  | (0        | IS | 0002     | 4         |
   |          | Channel   | 03a,0202) |    |          |           |
   |          | Number    |           |    |          |           |
   +----------+-----------+-----------+----+----------+-----------+
   |          | Channel   | (0        | SH | 0002     | F3        |
   |          | Label     | 03a,0203) |    |          |           |
   +----------+-----------+-----------+----+----------+-----------+
   |          | Channel   | (0        | SQ | ffffffff |           |
   |          | Source    | 03a,0208) |    |          |           |
   |          | Sequence  |           |    |          |           |
   +----------+-----------+-----------+----+----------+-----------+
   | %item    |           |           |    |          |           |
   +----------+-----------+-----------+----+----------+-----------+
   |          | Code      | (0        | SH | 0006     | 7:1057    |
   |          | Value     | 008,0100) |    |          |           |
   +----------+-----------+-----------+----+----------+-----------+
   |          | Coding    | (0        | SH | 0004     | MDC       |
   |          | Scheme    | 008,0102) |    |          |           |
   |          | D         |           |    |          |           |
   |          | esignator |           |    |          |           |
   +----------+-----------+-----------+----+----------+-----------+
   |          | Code      | (0        | LO | 0002     | F3        |
   |          | Meaning   | 008,0104) |    |          |           |
   +----------+-----------+-----------+----+----------+-----------+
   | %enditem |           |           |    |          |           |
   +----------+-----------+-----------+----+----------+-----------+
   | %endseq  |           |           |    |          |           |
   +----------+-----------+-----------+----+----------+-----------+
   |          | Channel   | (0        | DS | 0008     | 0.100008  |
   |          | Se        | 03a,0210) |    |          |           |
   |          | nsitivity |           |    |          |           |
   +----------+-----------+-----------+----+----------+-----------+
   |          | Channel   | (0        | SQ | ffffffff |           |
   |          | Se        | 03a,0211) |    |          |           |
   |          | nsitivity |           |    |          |           |
   |          | Units     |           |    |          |           |
   |          | Sequence  |           |    |          |           |
   +----------+-----------+-----------+----+----------+-----------+
   | %item    |           |           |    |          |           |
   +----------+-----------+-----------+----+----------+-----------+
   |          | Code      | (0        | SH | 0002     | uV        |
   |          | Value     | 008,0100) |    |          |           |
   +----------+-----------+-----------+----+----------+-----------+
   |          | Coding    | (0        | SH | 0004     | UCUM      |
   |          | Scheme    | 008,0102) |    |          |           |
   |          | D         |           |    |          |           |
   |          | esignator |           |    |          |           |
   +----------+-----------+-----------+----+----------+-----------+
   |          | Code      | (0        | LO | 000a     | uV        |
   |          | Meaning   | 008,0104) |    |          |           |
   +----------+-----------+-----------+----+----------+-----------+
   | %enditem |           |           |    |          |           |
   +----------+-----------+-----------+----+----------+-----------+
   | %endseq  |           |           |    |          |           |
   +----------+-----------+-----------+----+----------+-----------+
   |          | Channel   | (0        | SQ | ffffffff |           |
   |          | Source    | 03a,0209) |    |          |           |
   |          | Modifier  |           |    |          |           |
   |          | Sequence  |           |    |          |           |
   +----------+-----------+-----------+----+----------+-----------+
   | %item    |           |           |    |          |           |
   +----------+-----------+-----------+----+----------+-----------+
   |          | Code      | (0        | SH | 0006     | 109006    |
   |          | Value     | 008,0100) |    |          |           |
   +----------+-----------+-----------+----+----------+-----------+
   |          | Coding    | (0        | SH | 0004     | DCM       |
   |          | Scheme    | 008,0102) |    |          |           |
   |          | D         |           |    |          |           |
   |          | esignator |           |    |          |           |
   +----------+-----------+-----------+----+----------+-----------+
   |          | Code      | (0        | LO | 0014     | Dif       |
   |          | Meaning   | 008,0104) |    |          | ferential |
   |          |           |           |    |          | signal    |
   +----------+-----------+-----------+----+----------+-----------+
   | %enditem |           |           |    |          |           |
   +----------+-----------+-----------+----+----------+-----------+
   | %item    |           |           |    |          |           |
   +----------+-----------+-----------+----+----------+-----------+
   |          | Code      | (0        | SH | 0006     | 7:1020    |
   |          | Value     | 008,0100) |    |          |           |
   +----------+-----------+-----------+----+----------+-----------+
   |          | Coding    | (0        | SH | 0004     | MDC       |
   |          | Scheme    | 008,0102) |    |          |           |
   +----------+-----------+-----------+----+----------+-----------+
   |          | Code      | (0        | LO | 0004     | CPz       |
   |          | Meaning   | 008,0104) |    |          |           |
   +----------+-----------+-----------+----+----------+-----------+
   | %enditem |           |           |    |          |           |
   +----------+-----------+-----------+----+----------+-----------+
   | %endseq  |           |           |    |          |           |
   +----------+-----------+-----------+----+----------+-----------+
   |          | Channel   | (0        | DS | 0002     | 1         |
   |          | Se        | 03a,0212) |    |          |           |
   |          | nsitivity |           |    |          |           |
   |          | C         |           |    |          |           |
   |          | orrection |           |    |          |           |
   |          | Factor    |           |    |          |           |
   +----------+-----------+-----------+----+----------+-----------+
   |          | Channel   | (0        | DS | 000a     | 0.0500038 |
   |          | Baseline  | 03a,0213) |    |          |           |
   +----------+-----------+-----------+----+----------+-----------+
   |          | Channel   | (0        | DS | 0002     | 0         |
   |          | Sample    | 03a,0215) |    |          |           |
   |          | Skew      |           |    |          |           |
   +----------+-----------+-----------+----+----------+-----------+
   |          | Channel   | (0        | DS | 0002     | 0         |
   |          | Offset    | 03a,0218) |    |          |           |
   +----------+-----------+-----------+----+----------+-----------+
   |          | Waveform  | (0        | US | 0002     | 0x0010    |
   |          | Bits      | 03a,021a) |    |          |           |
   |          | Stored    |           |    |          |           |
   +----------+-----------+-----------+----+----------+-----------+
   | %enditem |           |           |    |          |           |
   +----------+-----------+-----------+----+----------+-----------+
   | %item    |           |           |    |          |           |
   +----------+-----------+-----------+----+----------+-----------+
   |          | Waveform  | (0        | IS | 0002     | 5         |
   |          | Channel   | 03a,0202) |    |          |           |
   |          | Number    |           |    |          |           |
   +----------+-----------+-----------+----+----------+-----------+
   |          | Channel   | (0        | SH | 0004     | FP1       |
   |          | Label     | 03a,0203) |    |          |           |
   +----------+-----------+-----------+----+----------+-----------+
   |          | Channel   | (0        | SQ | ffffffff |           |
   |          | Source    | 03a,0208) |    |          |           |
   |          | Sequence  |           |    |          |           |
   +----------+-----------+-----------+----+----------+-----------+
   | %item    |           |           |    |          |           |
   +----------+-----------+-----------+----+----------+-----------+
   |          | Code      | (0        | SH | 0006     | 7:1041    |
   |          | Value     | 008,0100) |    |          |           |
   +----------+-----------+-----------+----+----------+-----------+
   |          | Coding    | (0        | SH | 0004     | MDC       |
   |          | Scheme    | 008,0102) |    |          |           |
   |          | D         |           |    |          |           |
   |          | esignator |           |    |          |           |
   +----------+-----------+-----------+----+----------+-----------+
   |          | Code      | (0        | LO | 0004     | Fp1       |
   |          | Meaning   | 008,0104) |    |          |           |
   +----------+-----------+-----------+----+----------+-----------+
   | %enditem |           |           |    |          |           |
   +----------+-----------+-----------+----+----------+-----------+
   | %endseq  |           |           |    |          |           |
   +----------+-----------+-----------+----+----------+-----------+
   |          | Channel   | (0        | SQ | ffffffff |           |
   |          | Source    | 03a,0209) |    |          |           |
   |          | Modifier  |           |    |          |           |
   |          | Sequence  |           |    |          |           |
   +----------+-----------+-----------+----+----------+-----------+
   | %item    |           |           |    |          |           |
   +----------+-----------+-----------+----+----------+-----------+
   |          | Code      | (0        | SH | 0006     | 109006    |
   |          | Value     | 008,0100) |    |          |           |
   +----------+-----------+-----------+----+----------+-----------+
   |          | Coding    | (0        | SH | 0004     | DCM       |
   |          | Scheme    | 008,0102) |    |          |           |
   |          | D         |           |    |          |           |
   |          | esignator |           |    |          |           |
   +----------+-----------+-----------+----+----------+-----------+
   |          | Code      | (0        | LO | 0014     | Dif       |
   |          | Meaning   | 008,0104) |    |          | ferential |
   |          |           |           |    |          | signal    |
   +----------+-----------+-----------+----+----------+-----------+
   | %enditem |           |           |    |          |           |
   +----------+-----------+-----------+----+----------+-----------+
   | %item    |           |           |    |          |           |
   +----------+-----------+-----------+----+----------+-----------+
   |          | Code      | (0        | SH | 0006     | 7:1020    |
   |          | Value     | 008,0100) |    |          |           |
   +----------+-----------+-----------+----+----------+-----------+
   |          | Coding    | (0        | SH | 0004     | MDC       |
   |          | Scheme    | 008,0102) |    |          |           |
   +----------+-----------+-----------+----+----------+-----------+
   |          | Code      | (0        | LO | 0004     | CPz       |
   |          | Meaning   | 008,0104) |    |          |           |
   +----------+-----------+-----------+----+----------+-----------+
   | %enditem |           |           |    |          |           |
   +----------+-----------+-----------+----+----------+-----------+
   | %endseq  |           |           |    |          |           |
   +----------+-----------+-----------+----+----------+-----------+
   |          | Channel   | (0        | DS | 0008     | 0.100008  |
   |          | Se        | 03a,0210) |    |          |           |
   |          | nsitivity |           |    |          |           |
   +----------+-----------+-----------+----+----------+-----------+
   |          | Channel   | (0        | SQ | ffffffff |           |
   |          | Se        | 03a,0211) |    |          |           |
   |          | nsitivity |           |    |          |           |
   |          | Units     |           |    |          |           |
   |          | Sequence  |           |    |          |           |
   +----------+-----------+-----------+----+----------+-----------+
   | %item    |           |           |    |          |           |
   +----------+-----------+-----------+----+----------+-----------+
   |          | Code      | (0        | SH | 0002     | uV        |
   |          | Value     | 008,0100) |    |          |           |
   +----------+-----------+-----------+----+----------+-----------+
   |          | Coding    | (0        | SH | 0004     | UCUM      |
   |          | Scheme    | 008,0102) |    |          |           |
   |          | D         |           |    |          |           |
   |          | esignator |           |    |          |           |
   +----------+-----------+-----------+----+----------+-----------+
   |          | Code      | (0        | LO | 000a     | uV        |
   |          | Meaning   | 008,0104) |    |          |           |
   +----------+-----------+-----------+----+----------+-----------+
   | %enditem |           |           |    |          |           |
   +----------+-----------+-----------+----+----------+-----------+
   | %endseq  |           |           |    |          |           |
   +----------+-----------+-----------+----+----------+-----------+
   |          | Channel   | (0        | DS | 0002     | 1         |
   |          | Se        | 03a,0212) |    |          |           |
   |          | nsitivity |           |    |          |           |
   |          | C         |           |    |          |           |
   |          | orrection |           |    |          |           |
   |          | Factor    |           |    |          |           |
   +----------+-----------+-----------+----+----------+-----------+
   |          | Channel   | (0        | DS | 000a     | 0.0500038 |
   |          | Baseline  | 03a,0213) |    |          |           |
   +----------+-----------+-----------+----+----------+-----------+
   |          | Channel   | (0        | DS | 0002     | 0         |
   |          | Sample    | 03a,0215) |    |          |           |
   |          | Skew      |           |    |          |           |
   +----------+-----------+-----------+----+----------+-----------+
   |          | Channel   | (0        | DS | 0002     | 0         |
   |          | Offset    | 03a,0218) |    |          |           |
   +----------+-----------+-----------+----+----------+-----------+
   |          | Waveform  | (0        | US | 0002     | 0x0010    |
   |          | Bits      | 03a,021a) |    |          |           |
   |          | Stored    |           |    |          |           |
   +----------+-----------+-----------+----+----------+-----------+
   | %enditem |           |           |    |          |           |
   +----------+-----------+-----------+----+----------+-----------+
   | %item    |           |           |    |          |           |
   +----------+-----------+-----------+----+----------+-----------+
   |          | Waveform  | (0        | IS | 0002     | 6         |
   |          | Channel   | 03a,0202) |    |          |           |
   |          | Number    |           |    |          |           |
   +----------+-----------+-----------+----+----------+-----------+
   |          | Channel   | (0        | SH | 0002     | P7        |
   |          | Label     | 03a,0203) |    |          |           |
   +----------+-----------+-----------+----+----------+-----------+
   |          | Channel   | (0        | SQ | ffffffff |           |
   |          | Source    | 03a,0208) |    |          |           |
   |          | Sequence  |           |    |          |           |
   +----------+-----------+-----------+----+----------+-----------+
   | %item    |           |           |    |          |           |
   +----------+-----------+-----------+----+----------+-----------+
   |          | Code      | (0        | SH | 0006     | 7:1257    |
   |          | Value     | 008,0100) |    |          |           |
   +----------+-----------+-----------+----+----------+-----------+
   |          | Coding    | (0        | SH | 0004     | MDC       |
   |          | Scheme    | 008,0102) |    |          |           |
   |          | D         |           |    |          |           |
   |          | esignator |           |    |          |           |
   +----------+-----------+-----------+----+----------+-----------+
   |          | Code      | (0        | LO | 0002     | P7        |
   |          | Meaning   | 008,0104) |    |          |           |
   +----------+-----------+-----------+----+----------+-----------+
   | %enditem |           |           |    |          |           |
   +----------+-----------+-----------+----+----------+-----------+
   | %endseq  |           |           |    |          |           |
   +----------+-----------+-----------+----+----------+-----------+
   |          | Channel   | (0        | SQ | ffffffff |           |
   |          | Source    | 03a,0209) |    |          |           |
   |          | Modifier  |           |    |          |           |
   |          | Sequence  |           |    |          |           |
   +----------+-----------+-----------+----+----------+-----------+
   | %item    |           |           |    |          |           |
   +----------+-----------+-----------+----+----------+-----------+
   |          | Code      | (0        | SH | 0006     | 109006    |
   |          | Value     | 008,0100) |    |          |           |
   +----------+-----------+-----------+----+----------+-----------+
   |          | Coding    | (0        | SH | 0004     | DCM       |
   |          | Scheme    | 008,0102) |    |          |           |
   |          | D         |           |    |          |           |
   |          | esignator |           |    |          |           |
   +----------+-----------+-----------+----+----------+-----------+
   |          | Code      | (0        | LO | 0014     | Dif       |
   |          | Meaning   | 008,0104) |    |          | ferential |
   |          |           |           |    |          | signal    |
   +----------+-----------+-----------+----+----------+-----------+
   | %enditem |           |           |    |          |           |
   +----------+-----------+-----------+----+----------+-----------+
   | %item    |           |           |    |          |           |
   +----------+-----------+-----------+----+----------+-----------+
   |          | Code      | (0        | SH | 0006     | 7:1020    |
   |          | Value     | 008,0100) |    |          |           |
   +----------+-----------+-----------+----+----------+-----------+
   |          | Coding    | (0        | SH | 0004     | MDC       |
   |          | Scheme    | 008,0102) |    |          |           |
   +----------+-----------+-----------+----+----------+-----------+
   |          | Code      | (0        | LO | 0004     | CPz       |
   |          | Meaning   | 008,0104) |    |          |           |
   +----------+-----------+-----------+----+----------+-----------+
   | %enditem |           |           |    |          |           |
   +----------+-----------+-----------+----+----------+-----------+
   | %endseq  |           |           |    |          |           |
   +----------+-----------+-----------+----+----------+-----------+
   |          | Channel   | (0        | DS | 0008     | 0.100008  |
   |          | Se        | 03a,0210) |    |          |           |
   |          | nsitivity |           |    |          |           |
   +----------+-----------+-----------+----+----------+-----------+
   |          | Channel   | (0        | SQ | ffffffff |           |
   |          | Se        | 03a,0211) |    |          |           |
   |          | nsitivity |           |    |          |           |
   |          | Units     |           |    |          |           |
   |          | Sequence  |           |    |          |           |
   +----------+-----------+-----------+----+----------+-----------+
   | %item    |           |           |    |          |           |
   +----------+-----------+-----------+----+----------+-----------+
   |          | Code      | (0        | SH | 0002     | uV        |
   |          | Value     | 008,0100) |    |          |           |
   +----------+-----------+-----------+----+----------+-----------+
   |          | Coding    | (0        | SH | 0004     | UCUM      |
   |          | Scheme    | 008,0102) |    |          |           |
   |          | D         |           |    |          |           |
   |          | esignator |           |    |          |           |
   +----------+-----------+-----------+----+----------+-----------+
   |          | Code      | (0        | LO | 000a     | uV        |
   |          | Meaning   | 008,0104) |    |          |           |
   +----------+-----------+-----------+----+----------+-----------+
   | %enditem |           |           |    |          |           |
   +----------+-----------+-----------+----+----------+-----------+
   | %endseq  |           |           |    |          |           |
   +----------+-----------+-----------+----+----------+-----------+
   |          | Channel   | (0        | DS | 0002     | 1         |
   |          | Se        | 03a,0212) |    |          |           |
   |          | nsitivity |           |    |          |           |
   |          | C         |           |    |          |           |
   |          | orrection |           |    |          |           |
   |          | Factor    |           |    |          |           |
   +----------+-----------+-----------+----+----------+-----------+
   |          | Channel   | (0        | DS | 000a     | 0.0500038 |
   |          | Baseline  | 03a,0213) |    |          |           |
   +----------+-----------+-----------+----+----------+-----------+
   |          | Channel   | (0        | DS | 0002     | 0         |
   |          | Sample    | 03a,0215) |    |          |           |
   |          | Skew      |           |    |          |           |
   +----------+-----------+-----------+----+----------+-----------+
   |          | Channel   | (0        | DS | 0002     | 0         |
   |          | Offset    | 03a,0218) |    |          |           |
   +----------+-----------+-----------+----+----------+-----------+
   |          | Waveform  | (0        | US | 0002     | 0x0010    |
   |          | Bits      | 03a,021a) |    |          |           |
   |          | Stored    |           |    |          |           |
   +----------+-----------+-----------+----+----------+-----------+
   | %enditem |           |           |    |          |           |
   +----------+-----------+-----------+----+----------+-----------+
   | %item    |           |           |    |          |           |
   +----------+-----------+-----------+----+----------+-----------+
   |          | Waveform  | (0        | IS | 0002     | 7         |
   |          | Channel   | 03a,0202) |    |          |           |
   |          | Number    |           |    |          |           |
   +----------+-----------+-----------+----+----------+-----------+
   |          | Channel   | (0        | SH | 0002     | T7        |
   |          | Label     | 03a,0203) |    |          |           |
   +----------+-----------+-----------+----+----------+-----------+
   |          | Channel   | (0        | SQ | ffffffff |           |
   |          | Source    | 03a,0208) |    |          |           |
   |          | Sequence  |           |    |          |           |
   +----------+-----------+-----------+----+----------+-----------+
   | %item    |           |           |    |          |           |
   +----------+-----------+-----------+----+----------+-----------+
   |          | Code      | (0        | SH | 0006     | 7:1249    |
   |          | Value     | 008,0100) |    |          |           |
   +----------+-----------+-----------+----+----------+-----------+
   |          | Coding    | (0        | SH | 0004     | MDC       |
   |          | Scheme    | 008,0102) |    |          |           |
   |          | D         |           |    |          |           |
   |          | esignator |           |    |          |           |
   +----------+-----------+-----------+----+----------+-----------+
   |          | Code      | (0        | LO | 0002     | T7        |
   |          | Meaning   | 008,0104) |    |          |           |
   +----------+-----------+-----------+----+----------+-----------+
   | %enditem |           |           |    |          |           |
   +----------+-----------+-----------+----+----------+-----------+
   | %endseq  |           |           |    |          |           |
   +----------+-----------+-----------+----+----------+-----------+
   |          | Channel   | (0        | SQ | ffffffff |           |
   |          | Source    | 03a,0209) |    |          |           |
   |          | Modifier  |           |    |          |           |
   |          | Sequence  |           |    |          |           |
   +----------+-----------+-----------+----+----------+-----------+
   | %item    |           |           |    |          |           |
   +----------+-----------+-----------+----+----------+-----------+
   |          | Code      | (0        | SH | 0006     | 109006    |
   |          | Value     | 008,0100) |    |          |           |
   +----------+-----------+-----------+----+----------+-----------+
   |          | Coding    | (0        | SH | 0004     | DCM       |
   |          | Scheme    | 008,0102) |    |          |           |
   |          | D         |           |    |          |           |
   |          | esignator |           |    |          |           |
   +----------+-----------+-----------+----+----------+-----------+
   |          | Code      | (0        | LO | 0014     | Dif       |
   |          | Meaning   | 008,0104) |    |          | ferential |
   |          |           |           |    |          | signal    |
   +----------+-----------+-----------+----+----------+-----------+
   | %enditem |           |           |    |          |           |
   +----------+-----------+-----------+----+----------+-----------+
   | %item    |           |           |    |          |           |
   +----------+-----------+-----------+----+----------+-----------+
   |          | Code      | (0        | SH | 0006     | 7:1020    |
   |          | Value     | 008,0100) |    |          |           |
   +----------+-----------+-----------+----+----------+-----------+
   |          | Coding    | (0        | SH | 0004     | MDC       |
   |          | Scheme    | 008,0102) |    |          |           |
   +----------+-----------+-----------+----+----------+-----------+
   |          | Code      | (0        | LO | 0004     | CPz       |
   |          | Meaning   | 008,0104) |    |          |           |
   +----------+-----------+-----------+----+----------+-----------+
   | %enditem |           |           |    |          |           |
   +----------+-----------+-----------+----+----------+-----------+
   | %endseq  |           |           |    |          |           |
   +----------+-----------+-----------+----+----------+-----------+
   |          | Channel   | (0        | DS | 0008     | 0.100008  |
   |          | Se        | 03a,0210) |    |          |           |
   |          | nsitivity |           |    |          |           |
   +----------+-----------+-----------+----+----------+-----------+
   |          | Channel   | (0        | SQ | ffffffff |           |
   |          | Se        | 03a,0211) |    |          |           |
   |          | nsitivity |           |    |          |           |
   |          | Units     |           |    |          |           |
   |          | Sequence  |           |    |          |           |
   +----------+-----------+-----------+----+----------+-----------+
   | %item    |           |           |    |          |           |
   +----------+-----------+-----------+----+----------+-----------+
   |          | Code      | (0        | SH | 0002     | uV        |
   |          | Value     | 008,0100) |    |          |           |
   +----------+-----------+-----------+----+----------+-----------+
   |          | Coding    | (0        | SH | 0004     | UCUM      |
   |          | Scheme    | 008,0102) |    |          |           |
   |          | D         |           |    |          |           |
   |          | esignator |           |    |          |           |
   +----------+-----------+-----------+----+----------+-----------+
   |          | Code      | (0        | LO | 000a     | uV        |
   |          | Meaning   | 008,0104) |    |          |           |
   +----------+-----------+-----------+----+----------+-----------+
   | %enditem |           |           |    |          |           |
   +----------+-----------+-----------+----+----------+-----------+
   | %endseq  |           |           |    |          |           |
   +----------+-----------+-----------+----+----------+-----------+
   |          | Channel   | (0        | DS | 0002     | 1         |
   |          | Se        | 03a,0212) |    |          |           |
   |          | nsitivity |           |    |          |           |
   |          | C         |           |    |          |           |
   |          | orrection |           |    |          |           |
   |          | Factor    |           |    |          |           |
   +----------+-----------+-----------+----+----------+-----------+
   |          | Channel   | (0        | DS | 000a     | 0.0500038 |
   |          | Baseline  | 03a,0213) |    |          |           |
   +----------+-----------+-----------+----+----------+-----------+
   |          | Channel   | (0        | DS | 0002     | 0         |
   |          | Sample    | 03a,0215) |    |          |           |
   |          | Skew      |           |    |          |           |
   +----------+-----------+-----------+----+----------+-----------+
   |          | Channel   | (0        | DS | 0002     | 0         |
   |          | Offset    | 03a,0218) |    |          |           |
   +----------+-----------+-----------+----+----------+-----------+
   |          | Waveform  | (0        | US | 0002     | 0x0010    |
   |          | Bits      | 03a,021a) |    |          |           |
   |          | Stored    |           |    |          |           |
   +----------+-----------+-----------+----+----------+-----------+
   | %enditem |           |           |    |          |           |
   +----------+-----------+-----------+----+----------+-----------+
   | %item    |           |           |    |          |           |
   +----------+-----------+-----------+----+----------+-----------+
   |          | Waveform  | (0        | IS | 0002     | 8         |
   |          | Channel   | 03a,0202) |    |          |           |
   |          | Number    |           |    |          |           |
   +----------+-----------+-----------+----+----------+-----------+
   |          | Channel   | (0        | SH | 0002     | F7        |
   |          | Label     | 03a,0203) |    |          |           |
   +----------+-----------+-----------+----+----------+-----------+
   |          | Channel   | (0        | SQ | ffffffff |           |
   |          | Source    | 03a,0208) |    |          |           |
   |          | Sequence  |           |    |          |           |
   +----------+-----------+-----------+----+----------+-----------+
   | %item    |           |           |    |          |           |
   +----------+-----------+-----------+----+----------+-----------+
   |          | Code      | (0        | SH | 0006     | 7:1073    |
   |          | Value     | 008,0100) |    |          |           |
   +----------+-----------+-----------+----+----------+-----------+
   |          | Coding    | (0        | SH | 0004     | MDC       |
   |          | Scheme    | 008,0102) |    |          |           |
   |          | D         |           |    |          |           |
   |          | esignator |           |    |          |           |
   +----------+-----------+-----------+----+----------+-----------+
   |          | Code      | (0        | LO | 0002     | F7        |
   |          | Meaning   | 008,0104) |    |          |           |
   +----------+-----------+-----------+----+----------+-----------+
   | %enditem |           |           |    |          |           |
   +----------+-----------+-----------+----+----------+-----------+
   | %endseq  |           |           |    |          |           |
   +----------+-----------+-----------+----+----------+-----------+
   |          | Channel   | (0        | DS | 0008     | 0.100008  |
   |          | Se        | 03a,0210) |    |          |           |
   |          | nsitivity |           |    |          |           |
   +----------+-----------+-----------+----+----------+-----------+
   |          | Channel   | (0        | SQ | ffffffff |           |
   |          | Se        | 03a,0211) |    |          |           |
   |          | nsitivity |           |    |          |           |
   |          | Units     |           |    |          |           |
   |          | Sequence  |           |    |          |           |
   +----------+-----------+-----------+----+----------+-----------+
   | %item    |           |           |    |          |           |
   +----------+-----------+-----------+----+----------+-----------+
   |          | Code      | (0        | SH | 0002     | uV        |
   |          | Value     | 008,0100) |    |          |           |
   +----------+-----------+-----------+----+----------+-----------+
   |          | Coding    | (0        | SH | 0004     | UCUM      |
   |          | Scheme    | 008,0102) |    |          |           |
   |          | D         |           |    |          |           |
   |          | esignator |           |    |          |           |
   +----------+-----------+-----------+----+----------+-----------+
   |          | Code      | (0        | LO | 000a     | uV        |
   |          | Meaning   | 008,0104) |    |          |           |
   +----------+-----------+-----------+----+----------+-----------+
   | %enditem |           |           |    |          |           |
   +----------+-----------+-----------+----+----------+-----------+
   | %endseq  |           |           |    |          |           |
   +----------+-----------+-----------+----+----------+-----------+
   |          | Channel   | (0        | SQ | ffffffff |           |
   |          | Source    | 03a,0209) |    |          |           |
   |          | Modifier  |           |    |          |           |
   |          | Sequence  |           |    |          |           |
   +----------+-----------+-----------+----+----------+-----------+
   | %item    |           |           |    |          |           |
   +----------+-----------+-----------+----+----------+-----------+
   |          | Code      | (0        | SH | 0006     | 109006    |
   |          | Value     | 008,0100) |    |          |           |
   +----------+-----------+-----------+----+----------+-----------+
   |          | Coding    | (0        | SH | 0004     | DCM       |
   |          | Scheme    | 008,0102) |    |          |           |
   |          | D         |           |    |          |           |
   |          | esignator |           |    |          |           |
   +----------+-----------+-----------+----+----------+-----------+
   |          | Code      | (0        | LO | 0014     | Dif       |
   |          | Meaning   | 008,0104) |    |          | ferential |
   |          |           |           |    |          | signal    |
   +----------+-----------+-----------+----+----------+-----------+
   | %enditem |           |           |    |          |           |
   +----------+-----------+-----------+----+----------+-----------+
   | %item    |           |           |    |          |           |
   +----------+-----------+-----------+----+----------+-----------+
   |          | Code      | (0        | SH | 0006     | 7:1020    |
   |          | Value     | 008,0100) |    |          |           |
   +----------+-----------+-----------+----+----------+-----------+
   |          | Coding    | (0        | SH | 0004     | MDC       |
   |          | Scheme    | 008,0102) |    |          |           |
   +----------+-----------+-----------+----+----------+-----------+
   |          | Code      | (0        | LO | 0004     | CPz       |
   |          | Meaning   | 008,0104) |    |          |           |
   +----------+-----------+-----------+----+----------+-----------+
   | %enditem |           |           |    |          |           |
   +----------+-----------+-----------+----+----------+-----------+
   | %endseq  |           |           |    |          |           |
   +----------+-----------+-----------+----+----------+-----------+
   |          | Channel   | (0        | DS | 0002     | 1         |
   |          | Se        | 03a,0212) |    |          |           |
   |          | nsitivity |           |    |          |           |
   |          | C         |           |    |          |           |
   |          | orrection |           |    |          |           |
   |          | Factor    |           |    |          |           |
   +----------+-----------+-----------+----+----------+-----------+
   |          | Channel   | (0        | DS | 000a     | 0.0500038 |
   |          | Baseline  | 03a,0213) |    |          |           |
   +----------+-----------+-----------+----+----------+-----------+
   |          | Channel   | (0        | DS | 0002     | 0         |
   |          | Sample    | 03a,0215) |    |          |           |
   |          | Skew      |           |    |          |           |
   +----------+-----------+-----------+----+----------+-----------+
   |          | Channel   | (0        | DS | 0002     | 0         |
   |          | Offset    | 03a,0218) |    |          |           |
   +----------+-----------+-----------+----+----------+-----------+
   |          | Waveform  | (0        | US | 0002     | 0x0010    |
   |          | Bits      | 03a,021a) |    |          |           |
   |          | Stored    |           |    |          |           |
   +----------+-----------+-----------+----+----------+-----------+
   | %enditem |           |           |    |          |           |
   +----------+-----------+-----------+----+----------+-----------+
   | %item    |           |           |    |          |           |
   +----------+-----------+-----------+----+----------+-----------+
   |          | Waveform  | (0        | IS | 0002     | 9         |
   |          | Channel   | 03a,0202) |    |          |           |
   |          | Number    |           |    |          |           |
   +----------+-----------+-----------+----+----------+-----------+
   |          | Channel   | (0        | SH | 0002     | O2        |
   |          | Label     | 03a,0203) |    |          |           |
   +----------+-----------+-----------+----+----------+-----------+
   |          | Channel   | (0        | SQ | ffffffff |           |
   |          | Source    | 03a,0208) |    |          |           |
   |          | Sequence  |           |    |          |           |
   +----------+-----------+-----------+----+----------+-----------+
   | %item    |           |           |    |          |           |
   +----------+-----------+-----------+----+----------+-----------+
   |          | Code      | (0        | SH | 0006     | 7:1214    |
   |          | Value     | 008,0100) |    |          |           |
   +----------+-----------+-----------+----+----------+-----------+
   |          | Coding    | (0        | SH | 0004     | MDC       |
   |          | Scheme    | 008,0102) |    |          |           |
   |          | D         |           |    |          |           |
   |          | esignator |           |    |          |           |
   +----------+-----------+-----------+----+----------+-----------+
   |          | Code      | (0        | LO | 0002     | O2        |
   |          | Meaning   | 008,0104) |    |          |           |
   +----------+-----------+-----------+----+----------+-----------+
   | %enditem |           |           |    |          |           |
   +----------+-----------+-----------+----+----------+-----------+
   | %endseq  |           |           |    |          |           |
   +----------+-----------+-----------+----+----------+-----------+
   |          | Channel   | (0        | SQ | ffffffff |           |
   |          | Source    | 03a,0209) |    |          |           |
   |          | Modifier  |           |    |          |           |
   |          | Sequence  |           |    |          |           |
   +----------+-----------+-----------+----+----------+-----------+
   | %item    |           |           |    |          |           |
   +----------+-----------+-----------+----+----------+-----------+
   |          | Code      | (0        | SH | 0006     | 109006    |
   |          | Value     | 008,0100) |    |          |           |
   +----------+-----------+-----------+----+----------+-----------+
   |          | Coding    | (0        | SH | 0004     | DCM       |
   |          | Scheme    | 008,0102) |    |          |           |
   |          | D         |           |    |          |           |
   |          | esignator |           |    |          |           |
   +----------+-----------+-----------+----+----------+-----------+
   |          | Code      | (0        | LO | 0014     | Dif       |
   |          | Meaning   | 008,0104) |    |          | ferential |
   |          |           |           |    |          | signal    |
   +----------+-----------+-----------+----+----------+-----------+
   | %enditem |           |           |    |          |           |
   +----------+-----------+-----------+----+----------+-----------+
   | %item    |           |           |    |          |           |
   +----------+-----------+-----------+----+----------+-----------+
   |          | Code      | (0        | SH | 0006     | 7:1020    |
   |          | Value     | 008,0100) |    |          |           |
   +----------+-----------+-----------+----+----------+-----------+
   |          | Coding    | (0        | SH | 0004     | MDC       |
   |          | Scheme    | 008,0102) |    |          |           |
   +----------+-----------+-----------+----+----------+-----------+
   |          | Code      | (0        | LO | 0004     | CPz       |
   |          | Meaning   | 008,0104) |    |          |           |
   +----------+-----------+-----------+----+----------+-----------+
   | %enditem |           |           |    |          |           |
   +----------+-----------+-----------+----+----------+-----------+
   | %endseq  |           |           |    |          |           |
   +----------+-----------+-----------+----+----------+-----------+
   |          | Channel   | (0        | DS | 0008     | 0.100008  |
   |          | Se        | 03a,0210) |    |          |           |
   |          | nsitivity |           |    |          |           |
   +----------+-----------+-----------+----+----------+-----------+
   |          | Channel   | (0        | SQ | ffffffff |           |
   |          | Se        | 03a,0211) |    |          |           |
   |          | nsitivity |           |    |          |           |
   |          | Units     |           |    |          |           |
   |          | Sequence  |           |    |          |           |
   +----------+-----------+-----------+----+----------+-----------+
   | %item    |           |           |    |          |           |
   +----------+-----------+-----------+----+----------+-----------+
   |          | Code      | (0        | SH | 0002     | uV        |
   |          | Value     | 008,0100) |    |          |           |
   +----------+-----------+-----------+----+----------+-----------+
   |          | Coding    | (0        | SH | 0004     | UCUM      |
   |          | Scheme    | 008,0102) |    |          |           |
   |          | D         |           |    |          |           |
   |          | esignator |           |    |          |           |
   +----------+-----------+-----------+----+----------+-----------+
   |          | Code      | (0        | LO | 000a     | uV        |
   |          | Meaning   | 008,0104) |    |          |           |
   +----------+-----------+-----------+----+----------+-----------+
   | %enditem |           |           |    |          |           |
   +----------+-----------+-----------+----+----------+-----------+
   | %endseq  |           |           |    |          |           |
   +----------+-----------+-----------+----+----------+-----------+
   |          | Channel   | (0        | DS | 0002     | 1         |
   |          | Se        | 03a,0212) |    |          |           |
   |          | nsitivity |           |    |          |           |
   |          | C         |           |    |          |           |
   |          | orrection |           |    |          |           |
   |          | Factor    |           |    |          |           |
   +----------+-----------+-----------+----+----------+-----------+
   |          | Channel   | (0        | DS | 000a     | 0.0500038 |
   |          | Baseline  | 03a,0213) |    |          |           |
   +----------+-----------+-----------+----+----------+-----------+
   |          | Channel   | (0        | DS | 0002     | 0         |
   |          | Sample    | 03a,0215) |    |          |           |
   |          | Skew      |           |    |          |           |
   +----------+-----------+-----------+----+----------+-----------+
   |          | Channel   | (0        | DS | 0002     | 0         |
   |          | Offset    | 03a,0218) |    |          |           |
   +----------+-----------+-----------+----+----------+-----------+
   |          | Waveform  | (0        | US | 0002     | 0x0010    |
   |          | Bits      | 03a,021a) |    |          |           |
   |          | Stored    |           |    |          |           |
   +----------+-----------+-----------+----+----------+-----------+
   | %enditem |           |           |    |          |           |
   +----------+-----------+-----------+----+----------+-----------+
   | %item    |           |           |    |          |           |
   +----------+-----------+-----------+----+----------+-----------+
   |          | Waveform  | (0        | IS | 0002     | 10        |
   |          | Channel   | 03a,0202) |    |          |           |
   |          | Number    |           |    |          |           |
   +----------+-----------+-----------+----+----------+-----------+
   |          | Channel   | (0        | SH | 0002     | P4        |
   |          | Label     | 03a,0203) |    |          |           |
   +----------+-----------+-----------+----+----------+-----------+
   |          | Channel   | (0        | SQ | ffffffff |           |
   |          | Source    | 03a,0208) |    |          |           |
   |          | Sequence  |           |    |          |           |
   +----------+-----------+-----------+----+----------+-----------+
   | %item    |           |           |    |          |           |
   +----------+-----------+-----------+----+----------+-----------+
   |          | Code      | (0        | SH | 0006     | 7:1190    |
   |          | Value     | 008,0100) |    |          |           |
   +----------+-----------+-----------+----+----------+-----------+
   |          | Coding    | (0        | SH | 0004     | MDC       |
   |          | Scheme    | 008,0102) |    |          |           |
   |          | D         |           |    |          |           |
   |          | esignator |           |    |          |           |
   +----------+-----------+-----------+----+----------+-----------+
   |          | Code      | (0        | LO | 0002     | P4        |
   |          | Meaning   | 008,0104) |    |          |           |
   +----------+-----------+-----------+----+----------+-----------+
   | %enditem |           |           |    |          |           |
   +----------+-----------+-----------+----+----------+-----------+
   | %endseq  |           |           |    |          |           |
   +----------+-----------+-----------+----+----------+-----------+
   |          | Channel   | (0        | SQ | ffffffff |           |
   |          | Source    | 03a,0209) |    |          |           |
   |          | Modifier  |           |    |          |           |
   |          | Sequence  |           |    |          |           |
   +----------+-----------+-----------+----+----------+-----------+
   | %item    |           |           |    |          |           |
   +----------+-----------+-----------+----+----------+-----------+
   |          | Code      | (0        | SH | 0006     | 109006    |
   |          | Value     | 008,0100) |    |          |           |
   +----------+-----------+-----------+----+----------+-----------+
   |          | Coding    | (0        | SH | 0004     | DCM       |
   |          | Scheme    | 008,0102) |    |          |           |
   |          | D         |           |    |          |           |
   |          | esignator |           |    |          |           |
   +----------+-----------+-----------+----+----------+-----------+
   |          | Code      | (0        | LO | 0014     | Dif       |
   |          | Meaning   | 008,0104) |    |          | ferential |
   |          |           |           |    |          | signal    |
   +----------+-----------+-----------+----+----------+-----------+
   | %enditem |           |           |    |          |           |
   +----------+-----------+-----------+----+----------+-----------+
   | %item    |           |           |    |          |           |
   +----------+-----------+-----------+----+----------+-----------+
   |          | Code      | (0        | SH | 0006     | 7:1020    |
   |          | Value     | 008,0100) |    |          |           |
   +----------+-----------+-----------+----+----------+-----------+
   |          | Coding    | (0        | SH | 0004     | MDC       |
   |          | Scheme    | 008,0102) |    |          |           |
   +----------+-----------+-----------+----+----------+-----------+
   |          | Code      | (0        | LO | 0004     | CPz       |
   |          | Meaning   | 008,0104) |    |          |           |
   +----------+-----------+-----------+----+----------+-----------+
   | %enditem |           |           |    |          |           |
   +----------+-----------+-----------+----+----------+-----------+
   | %endseq  |           |           |    |          |           |
   +----------+-----------+-----------+----+----------+-----------+
   |          | Channel   | (0        | DS | 0008     | 0.100008  |
   |          | Se        | 03a,0210) |    |          |           |
   |          | nsitivity |           |    |          |           |
   +----------+-----------+-----------+----+----------+-----------+
   |          | Channel   | (0        | SQ | ffffffff |           |
   |          | Se        | 03a,0211) |    |          |           |
   |          | nsitivity |           |    |          |           |
   |          | Units     |           |    |          |           |
   |          | Sequence  |           |    |          |           |
   +----------+-----------+-----------+----+----------+-----------+
   | %item    |           |           |    |          |           |
   +----------+-----------+-----------+----+----------+-----------+
   |          | Code      | (0        | SH | 0002     | uV        |
   |          | Value     | 008,0100) |    |          |           |
   +----------+-----------+-----------+----+----------+-----------+
   |          | Coding    | (0        | SH | 0004     | UCUM      |
   |          | Scheme    | 008,0102) |    |          |           |
   |          | D         |           |    |          |           |
   |          | esignator |           |    |          |           |
   +----------+-----------+-----------+----+----------+-----------+
   |          | Code      | (0        | LO | 000a     | uV        |
   |          | Meaning   | 008,0104) |    |          |           |
   +----------+-----------+-----------+----+----------+-----------+
   | %enditem |           |           |    |          |           |
   +----------+-----------+-----------+----+----------+-----------+
   | %endseq  |           |           |    |          |           |
   +----------+-----------+-----------+----+----------+-----------+
   |          | Channel   | (0        | DS | 0002     | 1         |
   |          | Se        | 03a,0212) |    |          |           |
   |          | nsitivity |           |    |          |           |
   |          | C         |           |    |          |           |
   |          | orrection |           |    |          |           |
   |          | Factor    |           |    |          |           |
   +----------+-----------+-----------+----+----------+-----------+
   |          | Channel   | (0        | DS | 000a     | 0.0500038 |
   |          | Baseline  | 03a,0213) |    |          |           |
   +----------+-----------+-----------+----+----------+-----------+
   |          | Channel   | (0        | DS | 0002     | 0         |
   |          | Sample    | 03a,0215) |    |          |           |
   |          | Skew      |           |    |          |           |
   +----------+-----------+-----------+----+----------+-----------+
   |          | Channel   | (0        | DS | 0002     | 0         |
   |          | Offset    | 03a,0218) |    |          |           |
   +----------+-----------+-----------+----+----------+-----------+
   |          | Waveform  | (0        | US | 0002     | 0x0010    |
   |          | Bits      | 03a,021a) |    |          |           |
   |          | Stored    |           |    |          |           |
   +----------+-----------+-----------+----+----------+-----------+
   | %enditem |           |           |    |          |           |
   +----------+-----------+-----------+----+----------+-----------+
   | %item    |           |           |    |          |           |
   +----------+-----------+-----------+----+----------+-----------+
   |          | Waveform  | (0        | IS | 0002     | 11        |
   |          | Channel   | 03a,0202) |    |          |           |
   |          | Number    |           |    |          |           |
   +----------+-----------+-----------+----+----------+-----------+
   |          | Channel   | (0        | SH | 0002     | C4        |
   |          | Label     | 03a,0203) |    |          |           |
   +----------+-----------+-----------+----+----------+-----------+
   |          | Channel   | (0        | SQ | ffffffff |           |
   |          | Source    | 03a,0208) |    |          |           |
   |          | Sequence  |           |    |          |           |
   +----------+-----------+-----------+----+----------+-----------+
   | %item    |           |           |    |          |           |
   +----------+-----------+-----------+----+----------+-----------+
   |          | Code      | (0        | SH | 0006     | 7:1142    |
   |          | Value     | 008,0100) |    |          |           |
   +----------+-----------+-----------+----+----------+-----------+
   |          | Coding    | (0        | SH | 0004     | MDC       |
   |          | Scheme    | 008,0102) |    |          |           |
   |          | D         |           |    |          |           |
   |          | esignator |           |    |          |           |
   +----------+-----------+-----------+----+----------+-----------+
   |          | Code      | (0        | LO | 0002     | C4        |
   |          | Meaning   | 008,0104) |    |          |           |
   +----------+-----------+-----------+----+----------+-----------+
   | %enditem |           |           |    |          |           |
   +----------+-----------+-----------+----+----------+-----------+
   | %endseq  |           |           |    |          |           |
   +----------+-----------+-----------+----+----------+-----------+
   |          | Channel   | (0        | SQ | ffffffff |           |
   |          | Source    | 03a,0209) |    |          |           |
   |          | Modifier  |           |    |          |           |
   |          | Sequence  |           |    |          |           |
   +----------+-----------+-----------+----+----------+-----------+
   | %item    |           |           |    |          |           |
   +----------+-----------+-----------+----+----------+-----------+
   |          | Code      | (0        | SH | 0006     | 109006    |
   |          | Value     | 008,0100) |    |          |           |
   +----------+-----------+-----------+----+----------+-----------+
   |          | Coding    | (0        | SH | 0004     | DCM       |
   |          | Scheme    | 008,0102) |    |          |           |
   |          | D         |           |    |          |           |
   |          | esignator |           |    |          |           |
   +----------+-----------+-----------+----+----------+-----------+
   |          | Code      | (0        | LO | 0014     | Dif       |
   |          | Meaning   | 008,0104) |    |          | ferential |
   |          |           |           |    |          | signal    |
   +----------+-----------+-----------+----+----------+-----------+
   | %enditem |           |           |    |          |           |
   +----------+-----------+-----------+----+----------+-----------+
   | %item    |           |           |    |          |           |
   +----------+-----------+-----------+----+----------+-----------+
   |          | Code      | (0        | SH | 0006     | 7:1020    |
   |          | Value     | 008,0100) |    |          |           |
   +----------+-----------+-----------+----+----------+-----------+
   |          | Coding    | (0        | SH | 0004     | MDC       |
   |          | Scheme    | 008,0102) |    |          |           |
   +----------+-----------+-----------+----+----------+-----------+
   |          | Code      | (0        | LO | 0004     | CPz       |
   |          | Meaning   | 008,0104) |    |          |           |
   +----------+-----------+-----------+----+----------+-----------+
   | %enditem |           |           |    |          |           |
   +----------+-----------+-----------+----+----------+-----------+
   | %endseq  |           |           |    |          |           |
   +----------+-----------+-----------+----+----------+-----------+
   |          | Channel   | (0        | DS | 0008     | 0.100008  |
   |          | Se        | 03a,0210) |    |          |           |
   |          | nsitivity |           |    |          |           |
   +----------+-----------+-----------+----+----------+-----------+
   |          | Channel   | (0        | SQ | ffffffff |           |
   |          | Se        | 03a,0211) |    |          |           |
   |          | nsitivity |           |    |          |           |
   |          | Units     |           |    |          |           |
   |          | Sequence  |           |    |          |           |
   +----------+-----------+-----------+----+----------+-----------+
   | %item    |           |           |    |          |           |
   +----------+-----------+-----------+----+----------+-----------+
   |          | Code      | (0        | SH | 0002     | uV        |
   |          | Value     | 008,0100) |    |          |           |
   +----------+-----------+-----------+----+----------+-----------+
   |          | Coding    | (0        | SH | 0004     | UCUM      |
   |          | Scheme    | 008,0102) |    |          |           |
   |          | D         |           |    |          |           |
   |          | esignator |           |    |          |           |
   +----------+-----------+-----------+----+----------+-----------+
   |          | Code      | (0        | LO | 000a     | uV        |
   |          | Meaning   | 008,0104) |    |          |           |
   +----------+-----------+-----------+----+----------+-----------+
   | %enditem |           |           |    |          |           |
   +----------+-----------+-----------+----+----------+-----------+
   | %endseq  |           |           |    |          |           |
   +----------+-----------+-----------+----+----------+-----------+
   |          | Channel   | (0        | DS | 0002     | 1         |
   |          | Se        | 03a,0212) |    |          |           |
   |          | nsitivity |           |    |          |           |
   |          | C         |           |    |          |           |
   |          | orrection |           |    |          |           |
   |          | Factor    |           |    |          |           |
   +----------+-----------+-----------+----+----------+-----------+
   |          | Channel   | (0        | DS | 000a     | 0.0500038 |
   |          | Baseline  | 03a,0213) |    |          |           |
   +----------+-----------+-----------+----+----------+-----------+
   |          | Channel   | (0        | DS | 0002     | 0         |
   |          | Sample    | 03a,0215) |    |          |           |
   |          | Skew      |           |    |          |           |
   +----------+-----------+-----------+----+----------+-----------+
   |          | Channel   | (0        | DS | 0002     | 0         |
   |          | Offset    | 03a,0218) |    |          |           |
   +----------+-----------+-----------+----+----------+-----------+
   |          | Waveform  | (0        | US | 0002     | 0x0010    |
   |          | Bits      | 03a,021a) |    |          |           |
   |          | Stored    |           |    |          |           |
   +----------+-----------+-----------+----+----------+-----------+
   | %enditem |           |           |    |          |           |
   +----------+-----------+-----------+----+----------+-----------+
   | %item    |           |           |    |          |           |
   +----------+-----------+-----------+----+----------+-----------+
   |          | Waveform  | (0        | IS | 0002     | 12        |
   |          | Channel   | 03a,0202) |    |          |           |
   |          | Number    |           |    |          |           |
   +----------+-----------+-----------+----+----------+-----------+
   |          | Channel   | (0        | SH | 0002     | F4        |
   |          | Label     | 03a,0203) |    |          |           |
   +----------+-----------+-----------+----+----------+-----------+
   |          | Channel   | (0        | SQ | ffffffff |           |
   |          | Source    | 03a,0208) |    |          |           |
   |          | Sequence  |           |    |          |           |
   +----------+-----------+-----------+----+----------+-----------+
   | %item    |           |           |    |          |           |
   +----------+-----------+-----------+----+----------+-----------+
   |          | Code      | (0        | SH | 0006     | 7:1062    |
   |          | Value     | 008,0100) |    |          |           |
   +----------+-----------+-----------+----+----------+-----------+
   |          | Coding    | (0        | SH | 0004     | MDC       |
   |          | Scheme    | 008,0102) |    |          |           |
   |          | D         |           |    |          |           |
   |          | esignator |           |    |          |           |
   +----------+-----------+-----------+----+----------+-----------+
   |          | Code      | (0        | LO | 0002     | F4        |
   |          | Meaning   | 008,0104) |    |          |           |
   +----------+-----------+-----------+----+----------+-----------+
   | %enditem |           |           |    |          |           |
   +----------+-----------+-----------+----+----------+-----------+
   | %endseq  |           |           |    |          |           |
   +----------+-----------+-----------+----+----------+-----------+
   |          | Channel   | (0        | SQ | ffffffff |           |
   |          | Source    | 03a,0209) |    |          |           |
   |          | Modifier  |           |    |          |           |
   |          | Sequence  |           |    |          |           |
   +----------+-----------+-----------+----+----------+-----------+
   | %item    |           |           |    |          |           |
   +----------+-----------+-----------+----+----------+-----------+
   |          | Code      | (0        | SH | 0006     | 109006    |
   |          | Value     | 008,0100) |    |          |           |
   +----------+-----------+-----------+----+----------+-----------+
   |          | Coding    | (0        | SH | 0004     | DCM       |
   |          | Scheme    | 008,0102) |    |          |           |
   |          | D         |           |    |          |           |
   |          | esignator |           |    |          |           |
   +----------+-----------+-----------+----+----------+-----------+
   |          | Code      | (0        | LO | 0014     | Dif       |
   |          | Meaning   | 008,0104) |    |          | ferential |
   |          |           |           |    |          | signal    |
   +----------+-----------+-----------+----+----------+-----------+
   | %enditem |           |           |    |          |           |
   +----------+-----------+-----------+----+----------+-----------+
   | %item    |           |           |    |          |           |
   +----------+-----------+-----------+----+----------+-----------+
   |          | Code      | (0        | SH | 0006     | 7:1020    |
   |          | Value     | 008,0100) |    |          |           |
   +----------+-----------+-----------+----+----------+-----------+
   |          | Coding    | (0        | SH | 0004     | MDC       |
   |          | Scheme    | 008,0102) |    |          |           |
   +----------+-----------+-----------+----+----------+-----------+
   |          | Code      | (0        | LO | 0004     | CPz       |
   |          | Meaning   | 008,0104) |    |          |           |
   +----------+-----------+-----------+----+----------+-----------+
   | %enditem |           |           |    |          |           |
   +----------+-----------+-----------+----+----------+-----------+
   | %endseq  |           |           |    |          |           |
   +----------+-----------+-----------+----+----------+-----------+
   |          | Channel   | (0        | DS | 0008     | 0.100008  |
   |          | Se        | 03a,0210) |    |          |           |
   |          | nsitivity |           |    |          |           |
   +----------+-----------+-----------+----+----------+-----------+
   |          | Channel   | (0        | SQ | ffffffff |           |
   |          | Se        | 03a,0211) |    |          |           |
   |          | nsitivity |           |    |          |           |
   |          | Units     |           |    |          |           |
   |          | Sequence  |           |    |          |           |
   +----------+-----------+-----------+----+----------+-----------+
   | %item    |           |           |    |          |           |
   +----------+-----------+-----------+----+----------+-----------+
   |          | Code      | (0        | SH | 0002     | uV        |
   |          | Value     | 008,0100) |    |          |           |
   +----------+-----------+-----------+----+----------+-----------+
   |          | Coding    | (0        | SH | 0004     | UCUM      |
   |          | Scheme    | 008,0102) |    |          |           |
   |          | D         |           |    |          |           |
   |          | esignator |           |    |          |           |
   +----------+-----------+-----------+----+----------+-----------+
   |          | Code      | (0        | LO | 000a     | uV        |
   |          | Meaning   | 008,0104) |    |          |           |
   +----------+-----------+-----------+----+----------+-----------+
   | %enditem |           |           |    |          |           |
   +----------+-----------+-----------+----+----------+-----------+
   | %endseq  |           |           |    |          |           |
   +----------+-----------+-----------+----+----------+-----------+
   |          | Channel   | (0        | DS | 0002     | 1         |
   |          | Se        | 03a,0212) |    |          |           |
   |          | nsitivity |           |    |          |           |
   |          | C         |           |    |          |           |
   |          | orrection |           |    |          |           |
   |          | Factor    |           |    |          |           |
   +----------+-----------+-----------+----+----------+-----------+
   |          | Channel   | (0        | DS | 000a     | 0.0500038 |
   |          | Baseline  | 03a,0213) |    |          |           |
   +----------+-----------+-----------+----+----------+-----------+
   |          | Channel   | (0        | DS | 0002     | 0         |
   |          | Sample    | 03a,0215) |    |          |           |
   |          | Skew      |           |    |          |           |
   +----------+-----------+-----------+----+----------+-----------+
   |          | Channel   | (0        | DS | 0002     | 0         |
   |          | Offset    | 03a,0218) |    |          |           |
   +----------+-----------+-----------+----+----------+-----------+
   |          | Waveform  | (0        | US | 0002     | 0x0010    |
   |          | Bits      | 03a,021a) |    |          |           |
   |          | Stored    |           |    |          |           |
   +----------+-----------+-----------+----+----------+-----------+
   | %enditem |           |           |    |          |           |
   +----------+-----------+-----------+----+----------+-----------+
   | %item    |           |           |    |          |           |
   +----------+-----------+-----------+----+----------+-----------+
   |          | Waveform  | (0        | IS | 0002     | 13        |
   |          | Channel   | 03a,0202) |    |          |           |
   |          | Number    |           |    |          |           |
   +----------+-----------+-----------+----+----------+-----------+
   |          | Channel   | (0        | SH | 0004     | FP2       |
   |          | Label     | 03a,0203) |    |          |           |
   +----------+-----------+-----------+----+----------+-----------+
   |          | Channel   | (0        | SQ | ffffffff |           |
   |          | Source    | 03a,0208) |    |          |           |
   |          | Sequence  |           |    |          |           |
   +----------+-----------+-----------+----+----------+-----------+
   | %item    |           |           |    |          |           |
   +----------+-----------+-----------+----+----------+-----------+
   |          | Code      | (0        | SH | 0006     | 7:1042    |
   |          | Value     | 008,0100) |    |          |           |
   +----------+-----------+-----------+----+----------+-----------+
   |          | Coding    | (0        | SH | 0004     | MDC       |
   |          | Scheme    | 008,0102) |    |          |           |
   |          | D         |           |    |          |           |
   |          | esignator |           |    |          |           |
   +----------+-----------+-----------+----+----------+-----------+
   |          | Code      | (0        | LO | 0004     | Fp2       |
   |          | Meaning   | 008,0104) |    |          |           |
   +----------+-----------+-----------+----+----------+-----------+
   | %enditem |           |           |    |          |           |
   +----------+-----------+-----------+----+----------+-----------+
   | %endseq  |           |           |    |          |           |
   +----------+-----------+-----------+----+----------+-----------+
   |          | Channel   | (0        | SQ | ffffffff |           |
   |          | Source    | 03a,0209) |    |          |           |
   |          | Modifier  |           |    |          |           |
   |          | Sequence  |           |    |          |           |
   +----------+-----------+-----------+----+----------+-----------+
   | %item    |           |           |    |          |           |
   +----------+-----------+-----------+----+----------+-----------+
   |          | Code      | (0        | SH | 0006     | 109006    |
   |          | Value     | 008,0100) |    |          |           |
   +----------+-----------+-----------+----+----------+-----------+
   |          | Coding    | (0        | SH | 0004     | DCM       |
   |          | Scheme    | 008,0102) |    |          |           |
   |          | D         |           |    |          |           |
   |          | esignator |           |    |          |           |
   +----------+-----------+-----------+----+----------+-----------+
   |          | Code      | (0        | LO | 0014     | Dif       |
   |          | Meaning   | 008,0104) |    |          | ferential |
   |          |           |           |    |          | signal    |
   +----------+-----------+-----------+----+----------+-----------+
   | %enditem |           |           |    |          |           |
   +----------+-----------+-----------+----+----------+-----------+
   | %item    |           |           |    |          |           |
   +----------+-----------+-----------+----+----------+-----------+
   |          | Code      | (0        | SH | 0006     | 7:1020    |
   |          | Value     | 008,0100) |    |          |           |
   +----------+-----------+-----------+----+----------+-----------+
   |          | Coding    | (0        | SH | 0004     | MDC       |
   |          | Scheme    | 008,0102) |    |          |           |
   +----------+-----------+-----------+----+----------+-----------+
   |          | Code      | (0        | LO | 0004     | CPz       |
   |          | Meaning   | 008,0104) |    |          |           |
   +----------+-----------+-----------+----+----------+-----------+
   | %enditem |           |           |    |          |           |
   +----------+-----------+-----------+----+----------+-----------+
   | %endseq  |           |           |    |          |           |
   +----------+-----------+-----------+----+----------+-----------+
   |          | Channel   | (0        | DS | 0008     | 0.100008  |
   |          | Se        | 03a,0210) |    |          |           |
   |          | nsitivity |           |    |          |           |
   +----------+-----------+-----------+----+----------+-----------+
   |          | Channel   | (0        | SQ | ffffffff |           |
   |          | Se        | 03a,0211) |    |          |           |
   |          | nsitivity |           |    |          |           |
   |          | Units     |           |    |          |           |
   |          | Sequence  |           |    |          |           |
   +----------+-----------+-----------+----+----------+-----------+
   | %item    |           |           |    |          |           |
   +----------+-----------+-----------+----+----------+-----------+
   |          | Code      | (0        | SH | 0002     | uV        |
   |          | Value     | 008,0100) |    |          |           |
   +----------+-----------+-----------+----+----------+-----------+
   |          | Coding    | (0        | SH | 0004     | UCUM      |
   |          | Scheme    | 008,0102) |    |          |           |
   |          | D         |           |    |          |           |
   |          | esignator |           |    |          |           |
   +----------+-----------+-----------+----+----------+-----------+
   |          | Code      | (0        | LO | 000a     | uV        |
   |          | Meaning   | 008,0104) |    |          |           |
   +----------+-----------+-----------+----+----------+-----------+
   | %enditem |           |           |    |          |           |
   +----------+-----------+-----------+----+----------+-----------+
   | %endseq  |           |           |    |          |           |
   +----------+-----------+-----------+----+----------+-----------+
   |          | Channel   | (0        | DS | 0002     | 1         |
   |          | Se        | 03a,0212) |    |          |           |
   |          | nsitivity |           |    |          |           |
   |          | C         |           |    |          |           |
   |          | orrection |           |    |          |           |
   |          | Factor    |           |    |          |           |
   +----------+-----------+-----------+----+----------+-----------+
   |          | Channel   | (0        | DS | 000a     | 0.0500038 |
   |          | Baseline  | 03a,0213) |    |          |           |
   +----------+-----------+-----------+----+----------+-----------+
   |          | Channel   | (0        | DS | 0002     | 0         |
   |          | Sample    | 03a,0215) |    |          |           |
   |          | Skew      |           |    |          |           |
   +----------+-----------+-----------+----+----------+-----------+
   |          | Channel   | (0        | DS | 0002     | 0         |
   |          | Offset    | 03a,0218) |    |          |           |
   +----------+-----------+-----------+----+----------+-----------+
   |          | Waveform  | (0        | US | 0002     | 0x0010    |
   |          | Bits      | 03a,021a) |    |          |           |
   |          | Stored    |           |    |          |           |
   +----------+-----------+-----------+----+----------+-----------+
   | %enditem |           |           |    |          |           |
   +----------+-----------+-----------+----+----------+-----------+
   | %item    |           |           |    |          |           |
   +----------+-----------+-----------+----+----------+-----------+
   |          | Waveform  | (0        | IS | 0002     | 14        |
   |          | Channel   | 03a,0202) |    |          |           |
   |          | Number    |           |    |          |           |
   +----------+-----------+-----------+----+----------+-----------+
   |          | Channel   | (0        | SH | 0002     | P8        |
   |          | Label     | 03a,0203) |    |          |           |
   +----------+-----------+-----------+----+----------+-----------+
   |          | Channel   | (0        | SQ | ffffffff |           |
   |          | Source    | 03a,0208) |    |          |           |
   |          | Sequence  |           |    |          |           |
   +----------+-----------+-----------+----+----------+-----------+
   | %item    |           |           |    |          |           |
   +----------+-----------+-----------+----+----------+-----------+
   |          | Code      | (0        | SH | 0006     | 7:1262    |
   |          | Value     | 008,0100) |    |          |           |
   +----------+-----------+-----------+----+----------+-----------+
   |          | Coding    | (0        | SH | 0004     | MDC       |
   |          | Scheme    | 008,0102) |    |          |           |
   |          | D         |           |    |          |           |
   |          | esignator |           |    |          |           |
   +----------+-----------+-----------+----+----------+-----------+
   |          | Code      | (0        | LO | 0002     | P8        |
   |          | Meaning   | 008,0104) |    |          |           |
   +----------+-----------+-----------+----+----------+-----------+
   | %enditem |           |           |    |          |           |
   +----------+-----------+-----------+----+----------+-----------+
   | %endseq  |           |           |    |          |           |
   +----------+-----------+-----------+----+----------+-----------+
   |          | Channel   | (0        | SQ | ffffffff |           |
   |          | Source    | 03a,0209) |    |          |           |
   |          | Modifier  |           |    |          |           |
   |          | Sequence  |           |    |          |           |
   +----------+-----------+-----------+----+----------+-----------+
   | %item    |           |           |    |          |           |
   +----------+-----------+-----------+----+----------+-----------+
   |          | Code      | (0        | SH | 0006     | 109006    |
   |          | Value     | 008,0100) |    |          |           |
   +----------+-----------+-----------+----+----------+-----------+
   |          | Coding    | (0        | SH | 0004     | DCM       |
   |          | Scheme    | 008,0102) |    |          |           |
   |          | D         |           |    |          |           |
   |          | esignator |           |    |          |           |
   +----------+-----------+-----------+----+----------+-----------+
   |          | Code      | (0        | LO | 0014     | Dif       |
   |          | Meaning   | 008,0104) |    |          | ferential |
   |          |           |           |    |          | signal    |
   +----------+-----------+-----------+----+----------+-----------+
   | %enditem |           |           |    |          |           |
   +----------+-----------+-----------+----+----------+-----------+
   | %item    |           |           |    |          |           |
   +----------+-----------+-----------+----+----------+-----------+
   |          | Code      | (0        | SH | 0006     | 7:1020    |
   |          | Value     | 008,0100) |    |          |           |
   +----------+-----------+-----------+----+----------+-----------+
   |          | Coding    | (0        | SH | 0004     | MDC       |
   |          | Scheme    | 008,0102) |    |          |           |
   +----------+-----------+-----------+----+----------+-----------+
   |          | Code      | (0        | LO | 0004     | CPz       |
   |          | Meaning   | 008,0104) |    |          |           |
   +----------+-----------+-----------+----+----------+-----------+
   | %enditem |           |           |    |          |           |
   +----------+-----------+-----------+----+----------+-----------+
   | %endseq  |           |           |    |          |           |
   +----------+-----------+-----------+----+----------+-----------+
   |          | Channel   | (0        | DS | 0008     | 0.100008  |
   |          | Se        | 03a,0210) |    |          |           |
   |          | nsitivity |           |    |          |           |
   +----------+-----------+-----------+----+----------+-----------+
   |          | Channel   | (0        | SQ | ffffffff |           |
   |          | Se        | 03a,0211) |    |          |           |
   |          | nsitivity |           |    |          |           |
   |          | Units     |           |    |          |           |
   |          | Sequence  |           |    |          |           |
   +----------+-----------+-----------+----+----------+-----------+
   | %item    |           |           |    |          |           |
   +----------+-----------+-----------+----+----------+-----------+
   |          | Code      | (0        | SH | 0002     | uV        |
   |          | Value     | 008,0100) |    |          |           |
   +----------+-----------+-----------+----+----------+-----------+
   |          | Coding    | (0        | SH | 0004     | UCUM      |
   |          | Scheme    | 008,0102) |    |          |           |
   |          | D         |           |    |          |           |
   |          | esignator |           |    |          |           |
   +----------+-----------+-----------+----+----------+-----------+
   |          | Code      | (0        | LO | 000a     | uV        |
   |          | Meaning   | 008,0104) |    |          |           |
   +----------+-----------+-----------+----+----------+-----------+
   | %enditem |           |           |    |          |           |
   +----------+-----------+-----------+----+----------+-----------+
   | %endseq  |           |           |    |          |           |
   +----------+-----------+-----------+----+----------+-----------+
   |          | Channel   | (0        | DS | 0002     | 1         |
   |          | Se        | 03a,0212) |    |          |           |
   |          | nsitivity |           |    |          |           |
   |          | C         |           |    |          |           |
   |          | orrection |           |    |          |           |
   |          | Factor    |           |    |          |           |
   +----------+-----------+-----------+----+----------+-----------+
   |          | Channel   | (0        | DS | 000a     | 0.0500038 |
   |          | Baseline  | 03a,0213) |    |          |           |
   +----------+-----------+-----------+----+----------+-----------+
   |          | Channel   | (0        | DS | 0002     | 0         |
   |          | Sample    | 03a,0215) |    |          |           |
   |          | Skew      |           |    |          |           |
   +----------+-----------+-----------+----+----------+-----------+
   |          | Channel   | (0        | DS | 0002     | 0         |
   |          | Offset    | 03a,0218) |    |          |           |
   +----------+-----------+-----------+----+----------+-----------+
   |          | Waveform  | (0        | US | 0002     | 0x0010    |
   |          | Bits      | 03a,021a) |    |          |           |
   |          | Stored    |           |    |          |           |
   +----------+-----------+-----------+----+----------+-----------+
   | %enditem |           |           |    |          |           |
   +----------+-----------+-----------+----+----------+-----------+
   | %item    |           |           |    |          |           |
   +----------+-----------+-----------+----+----------+-----------+
   |          | Waveform  | (0        | IS | 0002     | 15        |
   |          | Channel   | 03a,0202) |    |          |           |
   |          | Number    |           |    |          |           |
   +----------+-----------+-----------+----+----------+-----------+
   |          | Channel   | (0        | SH | 0002     | T8        |
   |          | Label     | 03a,0203) |    |          |           |
   +----------+-----------+-----------+----+----------+-----------+
   |          | Channel   | (0        | SQ | ffffffff |           |
   |          | Source    | 03a,0208) |    |          |           |
   |          | Sequence  |           |    |          |           |
   +----------+-----------+-----------+----+----------+-----------+
   | %item    |           |           |    |          |           |
   +----------+-----------+-----------+----+----------+-----------+
   |          | Code      | (0        | SH | 0006     | 7:1254    |
   |          | Value     | 008,0100) |    |          |           |
   +----------+-----------+-----------+----+----------+-----------+
   |          | Coding    | (0        | SH | 0004     | MDC       |
   |          | Scheme    | 008,0102) |    |          |           |
   |          | D         |           |    |          |           |
   |          | esignator |           |    |          |           |
   +----------+-----------+-----------+----+----------+-----------+
   |          | Code      | (0        | LO | 0002     | T8        |
   |          | Meaning   | 008,0104) |    |          |           |
   +----------+-----------+-----------+----+----------+-----------+
   | %enditem |           |           |    |          |           |
   +----------+-----------+-----------+----+----------+-----------+
   | %endseq  |           |           |    |          |           |
   +----------+-----------+-----------+----+----------+-----------+
   |          | Channel   | (0        | SQ | ffffffff |           |
   |          | Source    | 03a,0209) |    |          |           |
   |          | Modifier  |           |    |          |           |
   |          | Sequence  |           |    |          |           |
   +----------+-----------+-----------+----+----------+-----------+
   | %item    |           |           |    |          |           |
   +----------+-----------+-----------+----+----------+-----------+
   |          | Code      | (0        | SH | 0006     | 109006    |
   |          | Value     | 008,0100) |    |          |           |
   +----------+-----------+-----------+----+----------+-----------+
   |          | Coding    | (0        | SH | 0004     | DCM       |
   |          | Scheme    | 008,0102) |    |          |           |
   |          | D         |           |    |          |           |
   |          | esignator |           |    |          |           |
   +----------+-----------+-----------+----+----------+-----------+
   |          | Code      | (0        | LO | 0014     | Dif       |
   |          | Meaning   | 008,0104) |    |          | ferential |
   |          |           |           |    |          | signal    |
   +----------+-----------+-----------+----+----------+-----------+
   | %enditem |           |           |    |          |           |
   +----------+-----------+-----------+----+----------+-----------+
   | %item    |           |           |    |          |           |
   +----------+-----------+-----------+----+----------+-----------+
   |          | Code      | (0        | SH | 0006     | 7:1020    |
   |          | Value     | 008,0100) |    |          |           |
   +----------+-----------+-----------+----+----------+-----------+
   |          | Coding    | (0        | SH | 0004     | MDC       |
   |          | Scheme    | 008,0102) |    |          |           |
   +----------+-----------+-----------+----+----------+-----------+
   |          | Code      | (0        | LO | 0004     | CPz       |
   |          | Meaning   | 008,0104) |    |          |           |
   +----------+-----------+-----------+----+----------+-----------+
   | %enditem |           |           |    |          |           |
   +----------+-----------+-----------+----+----------+-----------+
   | %endseq  |           |           |    |          |           |
   +----------+-----------+-----------+----+----------+-----------+
   |          | Channel   | (0        | DS | 0008     | 0.100008  |
   |          | Se        | 03a,0210) |    |          |           |
   |          | nsitivity |           |    |          |           |
   +----------+-----------+-----------+----+----------+-----------+
   |          | Channel   | (0        | SQ | ffffffff |           |
   |          | Se        | 03a,0211) |    |          |           |
   |          | nsitivity |           |    |          |           |
   |          | Units     |           |    |          |           |
   |          | Sequence  |           |    |          |           |
   +----------+-----------+-----------+----+----------+-----------+
   | %item    |           |           |    |          |           |
   +----------+-----------+-----------+----+----------+-----------+
   |          | Code      | (0        | SH | 0002     | uV        |
   |          | Value     | 008,0100) |    |          |           |
   +----------+-----------+-----------+----+----------+-----------+
   |          | Coding    | (0        | SH | 0004     | UCUM      |
   |          | Scheme    | 008,0102) |    |          |           |
   |          | D         |           |    |          |           |
   |          | esignator |           |    |          |           |
   +----------+-----------+-----------+----+----------+-----------+
   |          | Code      | (0        | LO | 000a     | uV        |
   |          | Meaning   | 008,0104) |    |          |           |
   +----------+-----------+-----------+----+----------+-----------+
   | %enditem |           |           |    |          |           |
   +----------+-----------+-----------+----+----------+-----------+
   | %endseq  |           |           |    |          |           |
   +----------+-----------+-----------+----+----------+-----------+
   |          | Channel   | (0        | DS | 0002     | 1         |
   |          | Se        | 03a,0212) |    |          |           |
   |          | nsitivity |           |    |          |           |
   |          | C         |           |    |          |           |
   |          | orrection |           |    |          |           |
   |          | Factor    |           |    |          |           |
   +----------+-----------+-----------+----+----------+-----------+
   |          | Channel   | (0        | DS | 000a     | 0.0500038 |
   |          | Baseline  | 03a,0213) |    |          |           |
   +----------+-----------+-----------+----+----------+-----------+
   |          | Channel   | (0        | DS | 0002     | 0         |
   |          | Sample    | 03a,0215) |    |          |           |
   |          | Skew      |           |    |          |           |
   +----------+-----------+-----------+----+----------+-----------+
   |          | Channel   | (0        | DS | 0002     | 0         |
   |          | Offset    | 03a,0218) |    |          |           |
   +----------+-----------+-----------+----+----------+-----------+
   |          | Waveform  | (0        | US | 0002     | 0x0010    |
   |          | Bits      | 03a,021a) |    |          |           |
   |          | Stored    |           |    |          |           |
   +----------+-----------+-----------+----+----------+-----------+
   | %enditem |           |           |    |          |           |
   +----------+-----------+-----------+----+----------+-----------+
   | %item    |           |           |    |          |           |
   +----------+-----------+-----------+----+----------+-----------+
   |          | Waveform  | (0        | IS | 0002     | 16        |
   |          | Channel   | 03a,0202) |    |          |           |
   |          | Number    |           |    |          |           |
   +----------+-----------+-----------+----+----------+-----------+
   |          | Channel   | (0        | SH | 0002     | F8        |
   |          | Label     | 03a,0203) |    |          |           |
   +----------+-----------+-----------+----+----------+-----------+
   |          | Channel   | (0        | SQ | ffffffff |           |
   |          | Source    | 03a,0208) |    |          |           |
   |          | Sequence  |           |    |          |           |
   +----------+-----------+-----------+----+----------+-----------+
   | %item    |           |           |    |          |           |
   +----------+-----------+-----------+----+----------+-----------+
   |          | Code      | (0        | SH | 0006     | 7:1078    |
   |          | Value     | 008,0100) |    |          |           |
   +----------+-----------+-----------+----+----------+-----------+
   |          | Coding    | (0        | SH | 0004     | MDC       |
   |          | Scheme    | 008,0102) |    |          |           |
   |          | D         |           |    |          |           |
   |          | esignator |           |    |          |           |
   +----------+-----------+-----------+----+----------+-----------+
   |          | Code      | (0        | LO | 0002     | F8        |
   |          | Meaning   | 008,0104) |    |          |           |
   +----------+-----------+-----------+----+----------+-----------+
   | %enditem |           |           |    |          |           |
   +----------+-----------+-----------+----+----------+-----------+
   | %endseq  |           |           |    |          |           |
   +----------+-----------+-----------+----+----------+-----------+
   |          | Channel   | (0        | SQ | ffffffff |           |
   |          | Source    | 03a,0209) |    |          |           |
   |          | Modifier  |           |    |          |           |
   |          | Sequence  |           |    |          |           |
   +----------+-----------+-----------+----+----------+-----------+
   | %item    |           |           |    |          |           |
   +----------+-----------+-----------+----+----------+-----------+
   |          | Code      | (0        | SH | 0006     | 109006    |
   |          | Value     | 008,0100) |    |          |           |
   +----------+-----------+-----------+----+----------+-----------+
   |          | Coding    | (0        | SH | 0004     | DCM       |
   |          | Scheme    | 008,0102) |    |          |           |
   |          | D         |           |    |          |           |
   |          | esignator |           |    |          |           |
   +----------+-----------+-----------+----+----------+-----------+
   |          | Code      | (0        | LO | 0014     | Dif       |
   |          | Meaning   | 008,0104) |    |          | ferential |
   |          |           |           |    |          | signal    |
   +----------+-----------+-----------+----+----------+-----------+
   | %enditem |           |           |    |          |           |
   +----------+-----------+-----------+----+----------+-----------+
   | %item    |           |           |    |          |           |
   +----------+-----------+-----------+----+----------+-----------+
   |          | Code      | (0        | SH | 0006     | 7:1020    |
   |          | Value     | 008,0100) |    |          |           |
   +----------+-----------+-----------+----+----------+-----------+
   |          | Coding    | (0        | SH | 0004     | MDC       |
   |          | Scheme    | 008,0102) |    |          |           |
   +----------+-----------+-----------+----+----------+-----------+
   |          | Code      | (0        | LO | 0004     | CPz       |
   |          | Meaning   | 008,0104) |    |          |           |
   +----------+-----------+-----------+----+----------+-----------+
   | %enditem |           |           |    |          |           |
   +----------+-----------+-----------+----+----------+-----------+
   | %endseq  |           |           |    |          |           |
   +----------+-----------+-----------+----+----------+-----------+
   |          | Channel   | (0        | DS | 0008     | 0.100008  |
   |          | Se        | 03a,0210) |    |          |           |
   |          | nsitivity |           |    |          |           |
   +----------+-----------+-----------+----+----------+-----------+
   |          | Channel   | (0        | SQ | ffffffff |           |
   |          | Se        | 03a,0211) |    |          |           |
   |          | nsitivity |           |    |          |           |
   |          | Units     |           |    |          |           |
   |          | Sequence  |           |    |          |           |
   +----------+-----------+-----------+----+----------+-----------+
   | %item    |           |           |    |          |           |
   +----------+-----------+-----------+----+----------+-----------+
   |          | Code      | (0        | SH | 0002     | uV        |
   |          | Value     | 008,0100) |    |          |           |
   +----------+-----------+-----------+----+----------+-----------+
   |          | Coding    | (0        | SH | 0004     | UCUM      |
   |          | Scheme    | 008,0102) |    |          |           |
   |          | D         |           |    |          |           |
   |          | esignator |           |    |          |           |
   +----------+-----------+-----------+----+----------+-----------+
   |          | Code      | (0        | LO | 000a     | uV        |
   |          | Meaning   | 008,0104) |    |          |           |
   +----------+-----------+-----------+----+----------+-----------+
   | %enditem |           |           |    |          |           |
   +----------+-----------+-----------+----+----------+-----------+
   | %endseq  |           |           |    |          |           |
   +----------+-----------+-----------+----+----------+-----------+
   |          | Channel   | (0        | DS | 0002     | 1         |
   |          | Se        | 03a,0212) |    |          |           |
   |          | nsitivity |           |    |          |           |
   |          | C         |           |    |          |           |
   |          | orrection |           |    |          |           |
   |          | Factor    |           |    |          |           |
   +----------+-----------+-----------+----+----------+-----------+
   |          | Channel   | (0        | DS | 000a     | 0.0500038 |
   |          | Baseline  | 03a,0213) |    |          |           |
   +----------+-----------+-----------+----+----------+-----------+
   |          | Channel   | (0        | DS | 0002     | 0         |
   |          | Sample    | 03a,0215) |    |          |           |
   |          | Skew      |           |    |          |           |
   +----------+-----------+-----------+----+----------+-----------+
   |          | Channel   | (0        | DS | 0002     | 0         |
   |          | Offset    | 03a,0218) |    |          |           |
   +----------+-----------+-----------+----+----------+-----------+
   |          | Waveform  | (0        | US | 0002     | 0x0010    |
   |          | Bits      | 03a,021a) |    |          |           |
   |          | Stored    |           |    |          |           |
   +----------+-----------+-----------+----+----------+-----------+
   | %enditem |           |           |    |          |           |
   +----------+-----------+-----------+----+----------+-----------+
   | %item    |           |           |    |          |           |
   +----------+-----------+-----------+----+----------+-----------+
   |          | Waveform  | (0        | IS | 0002     | 17        |
   |          | Channel   | 03a,0202) |    |          |           |
   |          | Number    |           |    |          |           |
   +----------+-----------+-----------+----+----------+-----------+
   |          | Channel   | (0        | SH | 0002     | FZ        |
   |          | Label     | 03a,0203) |    |          |           |
   +----------+-----------+-----------+----+----------+-----------+
   |          | Channel   | (0        | SQ | ffffffff |           |
   |          | Source    | 03a,0208) |    |          |           |
   |          | Sequence  |           |    |          |           |
   +----------+-----------+-----------+----+----------+-----------+
   | %item    |           |           |    |          |           |
   +----------+-----------+-----------+----+----------+-----------+
   |          | Code      | (0        | SH | 0006     | 7:1008    |
   |          | Value     | 008,0100) |    |          |           |
   +----------+-----------+-----------+----+----------+-----------+
   |          | Coding    | (0        | SH | 0004     | MDC       |
   |          | Scheme    | 008,0102) |    |          |           |
   |          | D         |           |    |          |           |
   |          | esignator |           |    |          |           |
   +----------+-----------+-----------+----+----------+-----------+
   |          | Code      | (0        | LO | 0002     | Fz        |
   |          | Meaning   | 008,0104) |    |          |           |
   +----------+-----------+-----------+----+----------+-----------+
   | %enditem |           |           |    |          |           |
   +----------+-----------+-----------+----+----------+-----------+
   | %endseq  |           |           |    |          |           |
   +----------+-----------+-----------+----+----------+-----------+
   |          | Channel   | (0        | SQ | ffffffff |           |
   |          | Source    | 03a,0209) |    |          |           |
   |          | Modifier  |           |    |          |           |
   |          | Sequence  |           |    |          |           |
   +----------+-----------+-----------+----+----------+-----------+
   | %item    |           |           |    |          |           |
   +----------+-----------+-----------+----+----------+-----------+
   |          | Code      | (0        | SH | 0006     | 109006    |
   |          | Value     | 008,0100) |    |          |           |
   +----------+-----------+-----------+----+----------+-----------+
   |          | Coding    | (0        | SH | 0004     | DCM       |
   |          | Scheme    | 008,0102) |    |          |           |
   |          | D         |           |    |          |           |
   |          | esignator |           |    |          |           |
   +----------+-----------+-----------+----+----------+-----------+
   |          | Code      | (0        | LO | 0014     | Dif       |
   |          | Meaning   | 008,0104) |    |          | ferential |
   |          |           |           |    |          | signal    |
   +----------+-----------+-----------+----+----------+-----------+
   | %enditem |           |           |    |          |           |
   +----------+-----------+-----------+----+----------+-----------+
   | %item    |           |           |    |          |           |
   +----------+-----------+-----------+----+----------+-----------+
   |          | Code      | (0        | SH | 0006     | 7:1020    |
   |          | Value     | 008,0100) |    |          |           |
   +----------+-----------+-----------+----+----------+-----------+
   |          | Coding    | (0        | SH | 0004     | MDC       |
   |          | Scheme    | 008,0102) |    |          |           |
   +----------+-----------+-----------+----+----------+-----------+
   |          | Code      | (0        | LO | 0004     | CPz       |
   |          | Meaning   | 008,0104) |    |          |           |
   +----------+-----------+-----------+----+----------+-----------+
   | %enditem |           |           |    |          |           |
   +----------+-----------+-----------+----+----------+-----------+
   | %endseq  |           |           |    |          |           |
   +----------+-----------+-----------+----+----------+-----------+
   |          | Channel   | (0        | DS | 0008     | 0.100008  |
   |          | Se        | 03a,0210) |    |          |           |
   |          | nsitivity |           |    |          |           |
   +----------+-----------+-----------+----+----------+-----------+
   |          | Channel   | (0        | SQ | ffffffff |           |
   |          | Se        | 03a,0211) |    |          |           |
   |          | nsitivity |           |    |          |           |
   |          | Units     |           |    |          |           |
   |          | Sequence  |           |    |          |           |
   +----------+-----------+-----------+----+----------+-----------+
   | %item    |           |           |    |          |           |
   +----------+-----------+-----------+----+----------+-----------+
   |          | Code      | (0        | SH | 0002     | uV        |
   |          | Value     | 008,0100) |    |          |           |
   +----------+-----------+-----------+----+----------+-----------+
   |          | Coding    | (0        | SH | 0004     | UCUM      |
   |          | Scheme    | 008,0102) |    |          |           |
   |          | D         |           |    |          |           |
   |          | esignator |           |    |          |           |
   +----------+-----------+-----------+----+----------+-----------+
   |          | Code      | (0        | LO | 000a     | uV        |
   |          | Meaning   | 008,0104) |    |          |           |
   +----------+-----------+-----------+----+----------+-----------+
   | %enditem |           |           |    |          |           |
   +----------+-----------+-----------+----+----------+-----------+
   | %endseq  |           |           |    |          |           |
   +----------+-----------+-----------+----+----------+-----------+
   |          | Channel   | (0        | DS | 0002     | 1         |
   |          | Se        | 03a,0212) |    |          |           |
   |          | nsitivity |           |    |          |           |
   |          | C         |           |    |          |           |
   |          | orrection |           |    |          |           |
   |          | Factor    |           |    |          |           |
   +----------+-----------+-----------+----+----------+-----------+
   |          | Channel   | (0        | DS | 000a     | 0.0500038 |
   |          | Baseline  | 03a,0213) |    |          |           |
   +----------+-----------+-----------+----+----------+-----------+
   |          | Channel   | (0        | DS | 0002     | 0         |
   |          | Sample    | 03a,0215) |    |          |           |
   |          | Skew      |           |    |          |           |
   +----------+-----------+-----------+----+----------+-----------+
   |          | Channel   | (0        | DS | 0002     | 0         |
   |          | Offset    | 03a,0218) |    |          |           |
   +----------+-----------+-----------+----+----------+-----------+
   |          | Waveform  | (0        | US | 0002     | 0x0010    |
   |          | Bits      | 03a,021a) |    |          |           |
   |          | Stored    |           |    |          |           |
   +----------+-----------+-----------+----+----------+-----------+
   | %enditem |           |           |    |          |           |
   +----------+-----------+-----------+----+----------+-----------+
   | %item    |           |           |    |          |           |
   +----------+-----------+-----------+----+----------+-----------+
   |          | Waveform  | (0        | IS | 0002     | 18        |
   |          | Channel   | 03a,0202) |    |          |           |
   |          | Number    |           |    |          |           |
   +----------+-----------+-----------+----+----------+-----------+
   |          | Channel   | (0        | SH | 0002     | CZ        |
   |          | Label     | 03a,0203) |    |          |           |
   +----------+-----------+-----------+----+----------+-----------+
   |          | Channel   | (0        | SQ | ffffffff |           |
   |          | Source    | 03a,0208) |    |          |           |
   |          | Sequence  |           |    |          |           |
   +----------+-----------+-----------+----+----------+-----------+
   | %item    |           |           |    |          |           |
   +----------+-----------+-----------+----+----------+-----------+
   |          | Code      | (0        | SH | 0006     | 7:1016    |
   |          | Value     | 008,0100) |    |          |           |
   +----------+-----------+-----------+----+----------+-----------+
   |          | Coding    | (0        | SH | 0004     | MDC       |
   |          | Scheme    | 008,0102) |    |          |           |
   |          | D         |           |    |          |           |
   |          | esignator |           |    |          |           |
   +----------+-----------+-----------+----+----------+-----------+
   |          | Code      | (0        | LO | 0002     | Cz        |
   |          | Meaning   | 008,0104) |    |          |           |
   +----------+-----------+-----------+----+----------+-----------+
   | %enditem |           |           |    |          |           |
   +----------+-----------+-----------+----+----------+-----------+
   | %endseq  |           |           |    |          |           |
   +----------+-----------+-----------+----+----------+-----------+
   |          | Channel   | (0        | SQ | ffffffff |           |
   |          | Source    | 03a,0209) |    |          |           |
   |          | Modifier  |           |    |          |           |
   |          | Sequence  |           |    |          |           |
   +----------+-----------+-----------+----+----------+-----------+
   | %item    |           |           |    |          |           |
   +----------+-----------+-----------+----+----------+-----------+
   |          | Code      | (0        | SH | 0006     | 109006    |
   |          | Value     | 008,0100) |    |          |           |
   +----------+-----------+-----------+----+----------+-----------+
   |          | Coding    | (0        | SH | 0004     | DCM       |
   |          | Scheme    | 008,0102) |    |          |           |
   |          | D         |           |    |          |           |
   |          | esignator |           |    |          |           |
   +----------+-----------+-----------+----+----------+-----------+
   |          | Code      | (0        | LO | 0014     | Dif       |
   |          | Meaning   | 008,0104) |    |          | ferential |
   |          |           |           |    |          | signal    |
   +----------+-----------+-----------+----+----------+-----------+
   | %enditem |           |           |    |          |           |
   +----------+-----------+-----------+----+----------+-----------+
   | %item    |           |           |    |          |           |
   +----------+-----------+-----------+----+----------+-----------+
   |          | Code      | (0        | SH | 0006     | 7:1020    |
   |          | Value     | 008,0100) |    |          |           |
   +----------+-----------+-----------+----+----------+-----------+
   |          | Coding    | (0        | SH | 0004     | MDC       |
   |          | Scheme    | 008,0102) |    |          |           |
   +----------+-----------+-----------+----+----------+-----------+
   |          | Code      | (0        | LO | 0004     | CPz       |
   |          | Meaning   | 008,0104) |    |          |           |
   +----------+-----------+-----------+----+----------+-----------+
   | %enditem |           |           |    |          |           |
   +----------+-----------+-----------+----+----------+-----------+
   | %endseq  |           |           |    |          |           |
   +----------+-----------+-----------+----+----------+-----------+
   |          | Channel   | (0        | DS | 0008     | 0.100008  |
   |          | Se        | 03a,0210) |    |          |           |
   |          | nsitivity |           |    |          |           |
   +----------+-----------+-----------+----+----------+-----------+
   |          | Channel   | (0        | SQ | ffffffff |           |
   |          | Se        | 03a,0211) |    |          |           |
   |          | nsitivity |           |    |          |           |
   |          | Units     |           |    |          |           |
   |          | Sequence  |           |    |          |           |
   +----------+-----------+-----------+----+----------+-----------+
   | %item    |           |           |    |          |           |
   +----------+-----------+-----------+----+----------+-----------+
   |          | Code      | (0        | SH | 0002     | uV        |
   |          | Value     | 008,0100) |    |          |           |
   +----------+-----------+-----------+----+----------+-----------+
   |          | Coding    | (0        | SH | 0004     | UCUM      |
   |          | Scheme    | 008,0102) |    |          |           |
   |          | D         |           |    |          |           |
   |          | esignator |           |    |          |           |
   +----------+-----------+-----------+----+----------+-----------+
   |          | Code      | (0        | LO | 000a     | uV        |
   |          | Meaning   | 008,0104) |    |          |           |
   +----------+-----------+-----------+----+----------+-----------+
   | %enditem |           |           |    |          |           |
   +----------+-----------+-----------+----+----------+-----------+
   | %endseq  |           |           |    |          |           |
   +----------+-----------+-----------+----+----------+-----------+
   |          | Channel   | (0        | DS | 0002     | 1         |
   |          | Se        | 03a,0212) |    |          |           |
   |          | nsitivity |           |    |          |           |
   |          | C         |           |    |          |           |
   |          | orrection |           |    |          |           |
   |          | Factor    |           |    |          |           |
   +----------+-----------+-----------+----+----------+-----------+
   |          | Channel   | (0        | DS | 000a     | 0.0500038 |
   |          | Baseline  | 03a,0213) |    |          |           |
   +----------+-----------+-----------+----+----------+-----------+
   |          | Channel   | (0        | DS | 0002     | 0         |
   |          | Sample    | 03a,0215) |    |          |           |
   |          | Skew      |           |    |          |           |
   +----------+-----------+-----------+----+----------+-----------+
   |          | Channel   | (0        | DS | 0002     | 0         |
   |          | Offset    | 03a,0218) |    |          |           |
   +----------+-----------+-----------+----+----------+-----------+
   |          | Waveform  | (0        | US | 0002     | 0x0010    |
   |          | Bits      | 03a,021a) |    |          |           |
   |          | Stored    |           |    |          |           |
   +----------+-----------+-----------+----+----------+-----------+
   | %enditem |           |           |    |          |           |
   +----------+-----------+-----------+----+----------+-----------+
   | %item    |           |           |    |          |           |
   +----------+-----------+-----------+----+----------+-----------+
   |          | Waveform  | (0        | IS | 0002     | 19        |
   |          | Channel   | 03a,0202) |    |          |           |
   |          | Number    |           |    |          |           |
   +----------+-----------+-----------+----+----------+-----------+
   |          | Channel   | (0        | SH | 0002     | PZ        |
   |          | Label     | 03a,0203) |    |          |           |
   +----------+-----------+-----------+----+----------+-----------+
   |          | Channel   | (0        | SQ | ffffffff |           |
   |          | Source    | 03a,0208) |    |          |           |
   |          | Sequence  |           |    |          |           |
   +----------+-----------+-----------+----+----------+-----------+
   | %item    |           |           |    |          |           |
   +----------+-----------+-----------+----+----------+-----------+
   |          | Code      | (0        | SH | 0006     | 7:1024    |
   |          | Value     | 008,0100) |    |          |           |
   +----------+-----------+-----------+----+----------+-----------+
   |          | Coding    | (0        | SH | 0004     | MDC       |
   |          | Scheme    | 008,0102) |    |          |           |
   |          | D         |           |    |          |           |
   |          | esignator |           |    |          |           |
   +----------+-----------+-----------+----+----------+-----------+
   |          | Code      | (0        | LO | 0002     | Pz        |
   |          | Meaning   | 008,0104) |    |          |           |
   +----------+-----------+-----------+----+----------+-----------+
   | %enditem |           |           |    |          |           |
   +----------+-----------+-----------+----+----------+-----------+
   | %endseq  |           |           |    |          |           |
   +----------+-----------+-----------+----+----------+-----------+
   |          | Channel   | (0        | SQ | ffffffff |           |
   |          | Source    | 03a,0209) |    |          |           |
   |          | Modifier  |           |    |          |           |
   |          | Sequence  |           |    |          |           |
   +----------+-----------+-----------+----+----------+-----------+
   | %item    |           |           |    |          |           |
   +----------+-----------+-----------+----+----------+-----------+
   |          | Code      | (0        | SH | 0006     | 109006    |
   |          | Value     | 008,0100) |    |          |           |
   +----------+-----------+-----------+----+----------+-----------+
   |          | Coding    | (0        | SH | 0004     | DCM       |
   |          | Scheme    | 008,0102) |    |          |           |
   |          | D         |           |    |          |           |
   |          | esignator |           |    |          |           |
   +----------+-----------+-----------+----+----------+-----------+
   |          | Code      | (0        | LO | 0014     | Dif       |
   |          | Meaning   | 008,0104) |    |          | ferential |
   |          |           |           |    |          | signal    |
   +----------+-----------+-----------+----+----------+-----------+
   | %enditem |           |           |    |          |           |
   +----------+-----------+-----------+----+----------+-----------+
   | %item    |           |           |    |          |           |
   +----------+-----------+-----------+----+----------+-----------+
   |          | Code      | (0        | SH | 0006     | 7:1020    |
   |          | Value     | 008,0100) |    |          |           |
   +----------+-----------+-----------+----+----------+-----------+
   |          | Coding    | (0        | SH | 0004     | MDC       |
   |          | Scheme    | 008,0102) |    |          |           |
   +----------+-----------+-----------+----+----------+-----------+
   |          | Code      | (0        | LO | 0004     | CPz       |
   |          | Meaning   | 008,0104) |    |          |           |
   +----------+-----------+-----------+----+----------+-----------+
   | %enditem |           |           |    |          |           |
   +----------+-----------+-----------+----+----------+-----------+
   | %endseq  |           |           |    |          |           |
   +----------+-----------+-----------+----+----------+-----------+
   |          | Channel   | (0        | DS | 0008     | 0.100008  |
   |          | Se        | 03a,0210) |    |          |           |
   |          | nsitivity |           |    |          |           |
   +----------+-----------+-----------+----+----------+-----------+
   |          | Channel   | (0        | SQ | ffffffff |           |
   |          | Se        | 03a,0211) |    |          |           |
   |          | nsitivity |           |    |          |           |
   |          | Units     |           |    |          |           |
   |          | Sequence  |           |    |          |           |
   +----------+-----------+-----------+----+----------+-----------+
   | %item    |           |           |    |          |           |
   +----------+-----------+-----------+----+----------+-----------+
   |          | Code      | (0        | SH | 0002     | uV        |
   |          | Value     | 008,0100) |    |          |           |
   +----------+-----------+-----------+----+----------+-----------+
   |          | Coding    | (0        | SH | 0004     | UCUM      |
   |          | Scheme    | 008,0102) |    |          |           |
   |          | D         |           |    |          |           |
   |          | esignator |           |    |          |           |
   +----------+-----------+-----------+----+----------+-----------+
   |          | Code      | (0        | LO | 000a     | uV        |
   |          | Meaning   | 008,0104) |    |          |           |
   +----------+-----------+-----------+----+----------+-----------+
   | %enditem |           |           |    |          |           |
   +----------+-----------+-----------+----+----------+-----------+
   | %endseq  |           |           |    |          |           |
   +----------+-----------+-----------+----+----------+-----------+
   |          | Channel   | (0        | DS | 0002     | 1         |
   |          | Se        | 03a,0212) |    |          |           |
   |          | nsitivity |           |    |          |           |
   |          | C         |           |    |          |           |
   |          | orrection |           |    |          |           |
   |          | Factor    |           |    |          |           |
   +----------+-----------+-----------+----+----------+-----------+
   |          | Channel   | (0        | DS | 000a     | 0.0500038 |
   |          | Baseline  | 03a,0213) |    |          |           |
   +----------+-----------+-----------+----+----------+-----------+
   |          | Channel   | (0        | DS | 0002     | 0         |
   |          | Sample    | 03a,0215) |    |          |           |
   |          | Skew      |           |    |          |           |
   +----------+-----------+-----------+----+----------+-----------+
   |          | Channel   | (0        | DS | 0002     | 0         |
   |          | Offset    | 03a,0218) |    |          |           |
   +----------+-----------+-----------+----+----------+-----------+
   |          | Waveform  | (0        | US | 0002     | 0x0010    |
   |          | Bits      | 03a,021a) |    |          |           |
   |          | Stored    |           |    |          |           |
   +----------+-----------+-----------+----+----------+-----------+
   | %enditem |           |           |    |          |           |
   +----------+-----------+-----------+----+----------+-----------+
   | %item    |           |           |    |          |           |
   +----------+-----------+-----------+----+----------+-----------+
   |          | Waveform  | (0        | IS | 0002     | 20        |
   |          | Channel   | 03a,0202) |    |          |           |
   |          | Number    |           |    |          |           |
   +----------+-----------+-----------+----+----------+-----------+
   |          | Channel   | (0        | SH | 0004     | SP2       |
   |          | Label     | 03a,0203) |    |          |           |
   +----------+-----------+-----------+----+----------+-----------+
   |          | Channel   | (0        | SQ | ffffffff |           |
   |          | Source    | 03a,0208) |    |          |           |
   |          | Sequence  |           |    |          |           |
   +----------+-----------+-----------+----+----------+-----------+
   | %item    |           |           |    |          |           |
   +----------+-----------+-----------+----+----------+-----------+
   |          | Code      | (0        | SH | 0006     | 7:1314    |
   |          | Value     | 008,0100) |    |          |           |
   +----------+-----------+-----------+----+----------+-----------+
   |          | Coding    | (0        | SH | 0004     | MDC       |
   |          | Scheme    | 008,0102) |    |          |           |
   |          | D         |           |    |          |           |
   |          | esignator |           |    |          |           |
   +----------+-----------+-----------+----+----------+-----------+
   |          | Code      | (0        | LO | 0004     | Sp2       |
   |          | Meaning   | 008,0104) |    |          |           |
   +----------+-----------+-----------+----+----------+-----------+
   | %enditem |           |           |    |          |           |
   +----------+-----------+-----------+----+----------+-----------+
   | %endseq  |           |           |    |          |           |
   +----------+-----------+-----------+----+----------+-----------+
   |          | Channel   | (0        | SQ | ffffffff |           |
   |          | Source    | 03a,0209) |    |          |           |
   |          | Modifier  |           |    |          |           |
   |          | Sequence  |           |    |          |           |
   +----------+-----------+-----------+----+----------+-----------+
   | %item    |           |           |    |          |           |
   +----------+-----------+-----------+----+----------+-----------+
   |          | Code      | (0        | SH | 0006     | 109006    |
   |          | Value     | 008,0100) |    |          |           |
   +----------+-----------+-----------+----+----------+-----------+
   |          | Coding    | (0        | SH | 0004     | DCM       |
   |          | Scheme    | 008,0102) |    |          |           |
   |          | D         |           |    |          |           |
   |          | esignator |           |    |          |           |
   +----------+-----------+-----------+----+----------+-----------+
   |          | Code      | (0        | LO | 0014     | Dif       |
   |          | Meaning   | 008,0104) |    |          | ferential |
   |          |           |           |    |          | signal    |
   +----------+-----------+-----------+----+----------+-----------+
   | %enditem |           |           |    |          |           |
   +----------+-----------+-----------+----+----------+-----------+
   | %item    |           |           |    |          |           |
   +----------+-----------+-----------+----+----------+-----------+
   |          | Code      | (0        | SH | 0006     | 7:1020    |
   |          | Value     | 008,0100) |    |          |           |
   +----------+-----------+-----------+----+----------+-----------+
   |          | Coding    | (0        | SH | 0004     | MDC       |
   |          | Scheme    | 008,0102) |    |          |           |
   +----------+-----------+-----------+----+----------+-----------+
   |          | Code      | (0        | LO | 0004     | CPz       |
   |          | Meaning   | 008,0104) |    |          |           |
   +----------+-----------+-----------+----+----------+-----------+
   | %enditem |           |           |    |          |           |
   +----------+-----------+-----------+----+----------+-----------+
   | %endseq  |           |           |    |          |           |
   +----------+-----------+-----------+----+----------+-----------+
   |          | Channel   | (0        | DS | 0008     | 0.100008  |
   |          | Se        | 03a,0210) |    |          |           |
   |          | nsitivity |           |    |          |           |
   +----------+-----------+-----------+----+----------+-----------+
   |          | Channel   | (0        | SQ | ffffffff |           |
   |          | Se        | 03a,0211) |    |          |           |
   |          | nsitivity |           |    |          |           |
   |          | Units     |           |    |          |           |
   |          | Sequence  |           |    |          |           |
   +----------+-----------+-----------+----+----------+-----------+
   | %item    |           |           |    |          |           |
   +----------+-----------+-----------+----+----------+-----------+
   |          | Code      | (0        | SH | 0002     | uV        |
   |          | Value     | 008,0100) |    |          |           |
   +----------+-----------+-----------+----+----------+-----------+
   |          | Coding    | (0        | SH | 0004     | UCUM      |
   |          | Scheme    | 008,0102) |    |          |           |
   |          | D         |           |    |          |           |
   |          | esignator |           |    |          |           |
   +----------+-----------+-----------+----+----------+-----------+
   |          | Code      | (0        | LO | 000a     | uV        |
   |          | Meaning   | 008,0104) |    |          |           |
   +----------+-----------+-----------+----+----------+-----------+
   | %enditem |           |           |    |          |           |
   +----------+-----------+-----------+----+----------+-----------+
   | %endseq  |           |           |    |          |           |
   +----------+-----------+-----------+----+----------+-----------+
   |          | Channel   | (0        | DS | 0002     | 1         |
   |          | Se        | 03a,0212) |    |          |           |
   |          | nsitivity |           |    |          |           |
   |          | C         |           |    |          |           |
   |          | orrection |           |    |          |           |
   |          | Factor    |           |    |          |           |
   +----------+-----------+-----------+----+----------+-----------+
   |          | Channel   | (0        | DS | 000a     | 0.0500038 |
   |          | Baseline  | 03a,0213) |    |          |           |
   +----------+-----------+-----------+----+----------+-----------+
   |          | Channel   | (0        | DS | 0002     | 0         |
   |          | Sample    | 03a,0215) |    |          |           |
   |          | Skew      |           |    |          |           |
   +----------+-----------+-----------+----+----------+-----------+
   |          | Channel   | (0        | DS | 0002     | 0         |
   |          | Offset    | 03a,0218) |    |          |           |
   +----------+-----------+-----------+----+----------+-----------+
   |          | Waveform  | (0        | US | 0002     | 0x0010    |
   |          | Bits      | 03a,021a) |    |          |           |
   |          | Stored    |           |    |          |           |
   +----------+-----------+-----------+----+----------+-----------+
   | %enditem |           |           |    |          |           |
   +----------+-----------+-----------+----+----------+-----------+
   | %item    |           |           |    |          |           |
   +----------+-----------+-----------+----+----------+-----------+
   |          | Waveform  | (0        | IS | 0002     | 21        |
   |          | Channel   | 03a,0202) |    |          |           |
   |          | Number    |           |    |          |           |
   +----------+-----------+-----------+----+----------+-----------+
   |          | Channel   | (0        | SH | 0004     | SP1       |
   |          | Label     | 03a,0203) |    |          |           |
   +----------+-----------+-----------+----+----------+-----------+
   |          | Channel   | (0        | SQ | ffffffff |           |
   |          | Source    | 03a,0208) |    |          |           |
   |          | Sequence  |           |    |          |           |
   +----------+-----------+-----------+----+----------+-----------+
   | %item    |           |           |    |          |           |
   +----------+-----------+-----------+----+----------+-----------+
   |          | Code      | (0        | SH | 0006     | 7:1313    |
   |          | Value     | 008,0100) |    |          |           |
   +----------+-----------+-----------+----+----------+-----------+
   |          | Coding    | (0        | SH | 0004     | MDC       |
   |          | Scheme    | 008,0102) |    |          |           |
   |          | D         |           |    |          |           |
   |          | esignator |           |    |          |           |
   +----------+-----------+-----------+----+----------+-----------+
   |          | Code      | (0        | LO | 0004     | Sp1       |
   |          | Meaning   | 008,0104) |    |          |           |
   +----------+-----------+-----------+----+----------+-----------+
   | %enditem |           |           |    |          |           |
   +----------+-----------+-----------+----+----------+-----------+
   | %endseq  |           |           |    |          |           |
   +----------+-----------+-----------+----+----------+-----------+
   |          | Channel   | (0        | SQ | ffffffff |           |
   |          | Source    | 03a,0209) |    |          |           |
   |          | Modifier  |           |    |          |           |
   |          | Sequence  |           |    |          |           |
   +----------+-----------+-----------+----+----------+-----------+
   | %item    |           |           |    |          |           |
   +----------+-----------+-----------+----+----------+-----------+
   |          | Code      | (0        | SH | 0006     | 109006    |
   |          | Value     | 008,0100) |    |          |           |
   +----------+-----------+-----------+----+----------+-----------+
   |          | Coding    | (0        | SH | 0004     | DCM       |
   |          | Scheme    | 008,0102) |    |          |           |
   |          | D         |           |    |          |           |
   |          | esignator |           |    |          |           |
   +----------+-----------+-----------+----+----------+-----------+
   |          | Code      | (0        | LO | 0014     | Dif       |
   |          | Meaning   | 008,0104) |    |          | ferential |
   |          |           |           |    |          | signal    |
   +----------+-----------+-----------+----+----------+-----------+
   | %enditem |           |           |    |          |           |
   +----------+-----------+-----------+----+----------+-----------+
   | %item    |           |           |    |          |           |
   +----------+-----------+-----------+----+----------+-----------+
   |          | Code      | (0        | SH | 0006     | 7:1020    |
   |          | Value     | 008,0100) |    |          |           |
   +----------+-----------+-----------+----+----------+-----------+
   |          | Coding    | (0        | SH | 0004     | MDC       |
   |          | Scheme    | 008,0102) |    |          |           |
   +----------+-----------+-----------+----+----------+-----------+
   |          | Code      | (0        | LO | 0004     | CPz       |
   |          | Meaning   | 008,0104) |    |          |           |
   +----------+-----------+-----------+----+----------+-----------+
   | %enditem |           |           |    |          |           |
   +----------+-----------+-----------+----+----------+-----------+
   | %endseq  |           |           |    |          |           |
   +----------+-----------+-----------+----+----------+-----------+
   |          | Channel   | (0        | DS | 0008     | 0.100008  |
   |          | Se        | 03a,0210) |    |          |           |
   |          | nsitivity |           |    |          |           |
   +----------+-----------+-----------+----+----------+-----------+
   |          | Channel   | (0        | SQ | ffffffff |           |
   |          | Se        | 03a,0211) |    |          |           |
   |          | nsitivity |           |    |          |           |
   |          | Units     |           |    |          |           |
   |          | Sequence  |           |    |          |           |
   +----------+-----------+-----------+----+----------+-----------+
   | %item    |           |           |    |          |           |
   +----------+-----------+-----------+----+----------+-----------+
   |          | Code      | (0        | SH | 0002     | uV        |
   |          | Value     | 008,0100) |    |          |           |
   +----------+-----------+-----------+----+----------+-----------+
   |          | Coding    | (0        | SH | 0004     | UCUM      |
   |          | Scheme    | 008,0102) |    |          |           |
   |          | D         |           |    |          |           |
   |          | esignator |           |    |          |           |
   +----------+-----------+-----------+----+----------+-----------+
   |          | Code      | (0        | LO | 000a     | uV        |
   |          | Meaning   | 008,0104) |    |          |           |
   +----------+-----------+-----------+----+----------+-----------+
   | %enditem |           |           |    |          |           |
   +----------+-----------+-----------+----+----------+-----------+
   | %endseq  |           |           |    |          |           |
   +----------+-----------+-----------+----+----------+-----------+
   |          | Channel   | (0        | DS | 0002     | 1         |
   |          | Se        | 03a,0212) |    |          |           |
   |          | nsitivity |           |    |          |           |
   |          | C         |           |    |          |           |
   |          | orrection |           |    |          |           |
   |          | Factor    |           |    |          |           |
   +----------+-----------+-----------+----+----------+-----------+
   |          | Channel   | (0        | DS | 000a     | 0.0500038 |
   |          | Baseline  | 03a,0213) |    |          |           |
   +----------+-----------+-----------+----+----------+-----------+
   |          | Channel   | (0        | DS | 0002     | 0         |
   |          | Sample    | 03a,0215) |    |          |           |
   |          | Skew      |           |    |          |           |
   +----------+-----------+-----------+----+----------+-----------+
   |          | Channel   | (0        | DS | 0002     | 0         |
   |          | Offset    | 03a,0218) |    |          |           |
   +----------+-----------+-----------+----+----------+-----------+
   |          | Waveform  | (0        | US | 0002     | 0x0010    |
   |          | Bits      | 03a,021a) |    |          |           |
   |          | Stored    |           |    |          |           |
   +----------+-----------+-----------+----+----------+-----------+
   | %enditem |           |           |    |          |           |
   +----------+-----------+-----------+----+----------+-----------+
   | %item    |           |           |    |          |           |
   +----------+-----------+-----------+----+----------+-----------+
   |          | Waveform  | (0        | IS | 0002     | 22        |
   |          | Channel   | 03a,0202) |    |          |           |
   |          | Number    |           |    |          |           |
   +----------+-----------+-----------+----+----------+-----------+
   |          | Channel   | (0        | SH | 0004     | FT9       |
   |          | Label     | 03a,0203) |    |          |           |
   +----------+-----------+-----------+----+----------+-----------+
   |          | Channel   | (0        | SQ | ffffffff |           |
   |          | Source    | 03a,0208) |    |          |           |
   |          | Sequence  |           |    |          |           |
   +----------+-----------+-----------+----+----------+-----------+
   | %item    |           |           |    |          |           |
   +----------+-----------+-----------+----+----------+-----------+
   |          | Code      | (0        | SH | 0006     | 7:1121    |
   |          | Value     | 008,0100) |    |          |           |
   +----------+-----------+-----------+----+----------+-----------+
   |          | Coding    | (0        | SH | 0004     | MDC       |
   |          | Scheme    | 008,0102) |    |          |           |
   |          | D         |           |    |          |           |
   |          | esignator |           |    |          |           |
   +----------+-----------+-----------+----+----------+-----------+
   |          | Code      | (0        | LO | 0004     | FT9       |
   |          | Meaning   | 008,0104) |    |          |           |
   +----------+-----------+-----------+----+----------+-----------+
   | %enditem |           |           |    |          |           |
   +----------+-----------+-----------+----+----------+-----------+
   | %endseq  |           |           |    |          |           |
   +----------+-----------+-----------+----+----------+-----------+
   |          | Channel   | (0        | SQ | ffffffff |           |
   |          | Source    | 03a,0209) |    |          |           |
   |          | Modifier  |           |    |          |           |
   |          | Sequence  |           |    |          |           |
   +----------+-----------+-----------+----+----------+-----------+
   | %item    |           |           |    |          |           |
   +----------+-----------+-----------+----+----------+-----------+
   |          | Code      | (0        | SH | 0006     | 109006    |
   |          | Value     | 008,0100) |    |          |           |
   +----------+-----------+-----------+----+----------+-----------+
   |          | Coding    | (0        | SH | 0004     | DCM       |
   |          | Scheme    | 008,0102) |    |          |           |
   |          | D         |           |    |          |           |
   |          | esignator |           |    |          |           |
   +----------+-----------+-----------+----+----------+-----------+
   |          | Code      | (0        | LO | 0014     | Dif       |
   |          | Meaning   | 008,0104) |    |          | ferential |
   |          |           |           |    |          | signal    |
   +----------+-----------+-----------+----+----------+-----------+
   | %enditem |           |           |    |          |           |
   +----------+-----------+-----------+----+----------+-----------+
   | %item    |           |           |    |          |           |
   +----------+-----------+-----------+----+----------+-----------+
   |          | Code      | (0        | SH | 0006     | 7:1020    |
   |          | Value     | 008,0100) |    |          |           |
   +----------+-----------+-----------+----+----------+-----------+
   |          | Coding    | (0        | SH | 0004     | MDC       |
   |          | Scheme    | 008,0102) |    |          |           |
   +----------+-----------+-----------+----+----------+-----------+
   |          | Code      | (0        | LO | 0004     | CPz       |
   |          | Meaning   | 008,0104) |    |          |           |
   +----------+-----------+-----------+----+----------+-----------+
   | %enditem |           |           |    |          |           |
   +----------+-----------+-----------+----+----------+-----------+
   | %endseq  |           |           |    |          |           |
   +----------+-----------+-----------+----+----------+-----------+
   |          | Channel   | (0        | DS | 0008     | 0.100008  |
   |          | Se        | 03a,0210) |    |          |           |
   |          | nsitivity |           |    |          |           |
   +----------+-----------+-----------+----+----------+-----------+
   |          | Channel   | (0        | SQ | ffffffff |           |
   |          | Se        | 03a,0211) |    |          |           |
   |          | nsitivity |           |    |          |           |
   |          | Units     |           |    |          |           |
   |          | Sequence  |           |    |          |           |
   +----------+-----------+-----------+----+----------+-----------+
   | %item    |           |           |    |          |           |
   +----------+-----------+-----------+----+----------+-----------+
   |          | Code      | (0        | SH | 0002     | uV        |
   |          | Value     | 008,0100) |    |          |           |
   +----------+-----------+-----------+----+----------+-----------+
   |          | Coding    | (0        | SH | 0004     | UCUM      |
   |          | Scheme    | 008,0102) |    |          |           |
   |          | D         |           |    |          |           |
   |          | esignator |           |    |          |           |
   +----------+-----------+-----------+----+----------+-----------+
   |          | Code      | (0        | LO | 000a     | uV        |
   |          | Meaning   | 008,0104) |    |          |           |
   +----------+-----------+-----------+----+----------+-----------+
   | %enditem |           |           |    |          |           |
   +----------+-----------+-----------+----+----------+-----------+
   | %endseq  |           |           |    |          |           |
   +----------+-----------+-----------+----+----------+-----------+
   |          | Channel   | (0        | DS | 0002     | 1         |
   |          | Se        | 03a,0212) |    |          |           |
   |          | nsitivity |           |    |          |           |
   |          | C         |           |    |          |           |
   |          | orrection |           |    |          |           |
   |          | Factor    |           |    |          |           |
   +----------+-----------+-----------+----+----------+-----------+
   |          | Channel   | (0        | DS | 000a     | 0.0500038 |
   |          | Baseline  | 03a,0213) |    |          |           |
   +----------+-----------+-----------+----+----------+-----------+
   |          | Channel   | (0        | DS | 0002     | 0         |
   |          | Sample    | 03a,0215) |    |          |           |
   |          | Skew      |           |    |          |           |
   +----------+-----------+-----------+----+----------+-----------+
   |          | Channel   | (0        | DS | 0002     | 0         |
   |          | Offset    | 03a,0218) |    |          |           |
   +----------+-----------+-----------+----+----------+-----------+
   |          | Waveform  | (0        | US | 0002     | 0x0010    |
   |          | Bits      | 03a,021a) |    |          |           |
   |          | Stored    |           |    |          |           |
   +----------+-----------+-----------+----+----------+-----------+
   | %enditem |           |           |    |          |           |
   +----------+-----------+-----------+----+----------+-----------+
   | %item    |           |           |    |          |           |
   +----------+-----------+-----------+----+----------+-----------+
   |          | Waveform  | (0        | IS | 0002     | 23        |
   |          | Channel   | 03a,0202) |    |          |           |
   |          | Number    |           |    |          |           |
   +----------+-----------+-----------+----+----------+-----------+
   |          | Channel   | (0        | SH | 0004     | FT10      |
   |          | Label     | 03a,0203) |    |          |           |
   +----------+-----------+-----------+----+----------+-----------+
   |          | Channel   | (0        | SQ | ffffffff |           |
   |          | Source    | 03a,0208) |    |          |           |
   |          | Sequence  |           |    |          |           |
   +----------+-----------+-----------+----+----------+-----------+
   | %item    |           |           |    |          |           |
   +----------+-----------+-----------+----+----------+-----------+
   |          | Code      | (0        | SH | 0006     | 7:1126    |
   |          | Value     | 008,0100) |    |          |           |
   +----------+-----------+-----------+----+----------+-----------+
   |          | Coding    | (0        | SH | 0004     | MDC       |
   |          | Scheme    | 008,0102) |    |          |           |
   |          | D         |           |    |          |           |
   |          | esignator |           |    |          |           |
   +----------+-----------+-----------+----+----------+-----------+
   |          | Code      | (0        | LO | 0004     | FT10      |
   |          | Meaning   | 008,0104) |    |          |           |
   +----------+-----------+-----------+----+----------+-----------+
   | %enditem |           |           |    |          |           |
   +----------+-----------+-----------+----+----------+-----------+
   | %endseq  |           |           |    |          |           |
   +----------+-----------+-----------+----+----------+-----------+
   |          | Channel   | (0        | SQ | ffffffff |           |
   |          | Source    | 03a,0209) |    |          |           |
   |          | Modifier  |           |    |          |           |
   |          | Sequence  |           |    |          |           |
   +----------+-----------+-----------+----+----------+-----------+
   | %item    |           |           |    |          |           |
   +----------+-----------+-----------+----+----------+-----------+
   |          | Code      | (0        | SH | 0006     | 109006    |
   |          | Value     | 008,0100) |    |          |           |
   +----------+-----------+-----------+----+----------+-----------+
   |          | Coding    | (0        | SH | 0004     | DCM       |
   |          | Scheme    | 008,0102) |    |          |           |
   |          | D         |           |    |          |           |
   |          | esignator |           |    |          |           |
   +----------+-----------+-----------+----+----------+-----------+
   |          | Code      | (0        | LO | 0014     | Dif       |
   |          | Meaning   | 008,0104) |    |          | ferential |
   |          |           |           |    |          | signal    |
   +----------+-----------+-----------+----+----------+-----------+
   | %enditem |           |           |    |          |           |
   +----------+-----------+-----------+----+----------+-----------+
   | %item    |           |           |    |          |           |
   +----------+-----------+-----------+----+----------+-----------+
   |          | Code      | (0        | SH | 0006     | 7:1020    |
   |          | Value     | 008,0100) |    |          |           |
   +----------+-----------+-----------+----+----------+-----------+
   |          | Coding    | (0        | SH | 0004     | MDC       |
   |          | Scheme    | 008,0102) |    |          |           |
   +----------+-----------+-----------+----+----------+-----------+
   |          | Code      | (0        | LO | 0004     | CPz       |
   |          | Meaning   | 008,0104) |    |          |           |
   +----------+-----------+-----------+----+----------+-----------+
   | %enditem |           |           |    |          |           |
   +----------+-----------+-----------+----+----------+-----------+
   | %endseq  |           |           |    |          |           |
   +----------+-----------+-----------+----+----------+-----------+
   |          | Channel   | (0        | DS | 0008     | 0.100008  |
   |          | Se        | 03a,0210) |    |          |           |
   |          | nsitivity |           |    |          |           |
   +----------+-----------+-----------+----+----------+-----------+
   |          | Channel   | (0        | SQ | ffffffff |           |
   |          | Se        | 03a,0211) |    |          |           |
   |          | nsitivity |           |    |          |           |
   |          | Units     |           |    |          |           |
   |          | Sequence  |           |    |          |           |
   +----------+-----------+-----------+----+----------+-----------+
   | %item    |           |           |    |          |           |
   +----------+-----------+-----------+----+----------+-----------+
   |          | Code      | (0        | SH | 0002     | uV        |
   |          | Value     | 008,0100) |    |          |           |
   +----------+-----------+-----------+----+----------+-----------+
   |          | Coding    | (0        | SH | 0004     | UCUM      |
   |          | Scheme    | 008,0102) |    |          |           |
   |          | D         |           |    |          |           |
   |          | esignator |           |    |          |           |
   +----------+-----------+-----------+----+----------+-----------+
   |          | Code      | (0        | LO | 000a     | uV        |
   |          | Meaning   | 008,0104) |    |          |           |
   +----------+-----------+-----------+----+----------+-----------+
   | %enditem |           |           |    |          |           |
   +----------+-----------+-----------+----+----------+-----------+
   | %endseq  |           |           |    |          |           |
   +----------+-----------+-----------+----+----------+-----------+
   |          | Channel   | (0        | DS | 0002     | 1         |
   |          | Se        | 03a,0212) |    |          |           |
   |          | nsitivity |           |    |          |           |
   |          | C         |           |    |          |           |
   |          | orrection |           |    |          |           |
   |          | Factor    |           |    |          |           |
   +----------+-----------+-----------+----+----------+-----------+
   |          | Channel   | (0        | DS | 000a     | 0.0500038 |
   |          | Baseline  | 03a,0213) |    |          |           |
   +----------+-----------+-----------+----+----------+-----------+
   |          | Channel   | (0        | DS | 0002     | 0         |
   |          | Sample    | 03a,0215) |    |          |           |
   |          | Skew      |           |    |          |           |
   +----------+-----------+-----------+----+----------+-----------+
   |          | Channel   | (0        | DS | 0002     | 0         |
   |          | Offset    | 03a,0218) |    |          |           |
   +----------+-----------+-----------+----+----------+-----------+
   |          | Waveform  | (0        | US | 0002     | 0x0010    |
   |          | Bits      | 03a,021a) |    |          |           |
   |          | Stored    |           |    |          |           |
   +----------+-----------+-----------+----+----------+-----------+
   | %enditem |           |           |    |          |           |
   +----------+-----------+-----------+----+----------+-----------+
   | %endseq  |           |           |    |          |           |
   +----------+-----------+-----------+----+----------+-----------+
   |          | Multiplex | (0        | UI | 0036     | 1.3.6.1.  |
   |          | Group ID  | 03A,0310) |    |          | 4.1.23154 |
   |          |           |           |    |          | .1.5.2881 |
   |          |           |           |    |          | 783832.12 |
   |          |           |           |    |          | 156.15335 |
   |          |           |           |    |          | 48324.955 |
   +----------+-----------+-----------+----+----------+-----------+
   |          | Powerline | (0        | DS | 0002     | 50        |
   |          | Frequency | 03A,0311) |    |          |           |
   +----------+-----------+-----------+----+----------+-----------+
   |          | Waveform  | (5        | US | 0002     | 0x0010    |
   |          | Bits      | 400,1004) |    |          |           |
   |          | Allocated |           |    |          |           |
   +----------+-----------+-----------+----+----------+-----------+
   |          | Waveform  | (5        | CS | 0002     | SS        |
   |          | Sample    | 400,1006) |    |          |           |
   |          | Inter     |           |    |          |           |
   |          | pretation |           |    |          |           |
   +----------+-----------+-----------+----+----------+-----------+
   |          | Waveform  | (5        | OW | 50c2200  | ...       |
   |          | Data      | 400,1010) |    |          |           |
   +----------+-----------+-----------+----+----------+-----------+
   | %enditem |           |           |    |          |           |
   +----------+-----------+-----------+----+----------+-----------+
   | %endseq  |           |           |    |          |           |
   +----------+-----------+-----------+----+----------+-----------+

.. |image1| image:: figures/PS3.17_FFF.2.1.5.4.2a.svg
.. |image2| image:: figures/PS3.17_FFF.2.1.5.4.2b.svg
.. |image3| image:: figures/PS3.17_FFF.2.1.5.4.2c.svg
.. |image4| image:: figures/PS3.17_FFF.2.1.5.4.2d.svg
.. |image5| image:: figures/PS3.17_FFF.2.1.5.4.2e.svg
.. |image6| image:: figures/PS3.17_FFF.2.1.5.4.2f.svg
.. |image7| image:: figures/PS3.17_FFF.2.1.5.4.2g.svg
.. |image8| image:: figures/PS3.17_FFF.2.1.5.4.2h.svg
