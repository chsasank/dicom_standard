.. _chapter_A:

Registry of DICOM Unique Identifiers (UIDs) (Normative)
=======================================================

`table_title <#table_A-1>`__ lists the UID values that are registered
and used throughout the Parts of the DICOM Standard. This central
registry ensures that when additional UIDs are assigned, non-duplicate
values are assigned. For retired UIDs, the edition of the Standard in
parentheses is the edition in which the item last appeared before it was
retired.

.. table:: UID Values

   +----------------+----------------+----------------+----------------+
   | **UID Value**  | **UID Name**   | **UID Type**   | **Part**       |
   +================+================+================+================+
   | 1.2.           | Verification   | SOP Class      |                |
   | 840.10008.1.​1 | SOP Class      |                |                |
   +----------------+----------------+----------------+----------------+
   | 1.2.           | Implicit VR    | Transfer       |                |
   | 840.10008.1.​2 | Little Endian: | Syntax         |                |
   |                | Default        |                |                |
   |                | Transfer       |                |                |
   |                | Syntax for     |                |                |
   |                | DICOM          |                |                |
   +----------------+----------------+----------------+----------------+
   | 1.2.840        | Explicit VR    | Transfer       |                |
   | .10008.1.​2.​1 | Little Endian  | Syntax         |                |
   +----------------+----------------+----------------+----------------+
   | 1.2.840.10     | Deflated       | Transfer       |                |
   | 008.1.2.​1.​99 | Explicit VR    | Syntax         |                |
   |                | Little Endian  |                |                |
   +----------------+----------------+----------------+----------------+
   | *1.2.840.      | *Explicit VR   | *Transfer      | *(2011)*       |
   | 10008.1.​2.​2* | Big Endian     | Syntax*        |                |
   |                | (Retired)*     |                |                |
   +----------------+----------------+----------------+----------------+
   | 1.2.840.10     | JPEG Baseline  | Transfer       |                |
   | 008.1.2.​4.​50 | (Process 1):   | Syntax         |                |
   |                | Default        |                |                |
   |                | Transfer       |                |                |
   |                | Syntax for     |                |                |
   |                | Lossy JPEG 8   |                |                |
   |                | Bit Image      |                |                |
   |                | Compression    |                |                |
   +----------------+----------------+----------------+----------------+
   | 1.2.840.10     | JPEG Extended  | Transfer       |                |
   | 008.1.2.​4.​51 | (Process 2 &   | Syntax         |                |
   |                | 4): Default    |                |                |
   |                | Transfer       |                |                |
   |                | Syntax for     |                |                |
   |                | Lossy JPEG 12  |                |                |
   |                | Bit Image      |                |                |
   |                | Compression    |                |                |
   |                | (Process 4     |                |                |
   |                | only)          |                |                |
   +----------------+----------------+----------------+----------------+
   | *1.2.840.100   | *JPEG Extended | *Transfer      | *(2001)*       |
   | 08.1.2.​4.​52* | (Process 3 &   | Syntax*        |                |
   |                | 5) (Retired)*  |                |                |
   +----------------+----------------+----------------+----------------+
   | *1.2.840.100   | *JPEG Spectral | *Transfer      | *(2001)*       |
   | 08.1.2.​4.​53* | Selection,     | Syntax*        |                |
   |                | No             |                |                |
   |                | n-Hierarchical |                |                |
   |                | (Process 6 &   |                |                |
   |                | 8) (Retired)*  |                |                |
   +----------------+----------------+----------------+----------------+
   | *1.2.840.100   | *JPEG Spectral | *Transfer      | *(2001)*       |
   | 08.1.2.​4.​54* | Selection,     | Syntax*        |                |
   |                | No             |                |                |
   |                | n-Hierarchical |                |                |
   |                | (Process 7 &   |                |                |
   |                | 9) (Retired)*  |                |                |
   +----------------+----------------+----------------+----------------+
   | *1.2.840.100   | *JPEG Full     | *Transfer      | *(2001)*       |
   | 08.1.2.​4.​55* | Progression,   | Syntax*        |                |
   |                | No             |                |                |
   |                | n-Hierarchical |                |                |
   |                | (Process 10 &  |                |                |
   |                | 12) (Retired)* |                |                |
   +----------------+----------------+----------------+----------------+
   | *1.2.840.100   | *JPEG Full     | *Transfer      | *(2001)*       |
   | 08.1.2.​4.​56* | Progression,   | Syntax*        |                |
   |                | No             |                |                |
   |                | n-Hierarchical |                |                |
   |                | (Process 11 &  |                |                |
   |                | 13) (Retired)* |                |                |
   +----------------+----------------+----------------+----------------+
   | 1.2.840.10     | JPEG Lossless, | Transfer       |                |
   | 008.1.2.​4.​57 | No             | Syntax         |                |
   |                | n-Hierarchical |                |                |
   |                | (Process 14)   |                |                |
   +----------------+----------------+----------------+----------------+
   | *1.2.840.100   | *JPEG          | *Transfer      | *(2001)*       |
   | 08.1.2.​4.​58* | Lossless,      | Syntax*        |                |
   |                | No             |                |                |
   |                | n-Hierarchical |                |                |
   |                | (Process 15)   |                |                |
   |                | (Retired)*     |                |                |
   +----------------+----------------+----------------+----------------+
   | *1.2.840.100   | *JPEG          | *Transfer      | *(2001)*       |
   | 08.1.2.​4.​59* | Extended,      | Syntax*        |                |
   |                | Hierarchical   |                |                |
   |                | (Process 16 &  |                |                |
   |                | 18) (Retired)* |                |                |
   +----------------+----------------+----------------+----------------+
   | *1.2.840.100   | *JPEG          | *Transfer      | *(2001)*       |
   | 08.1.2.​4.​60* | Extended,      | Syntax*        |                |
   |                | Hierarchical   |                |                |
   |                | (Process 17 &  |                |                |
   |                | 19) (Retired)* |                |                |
   +----------------+----------------+----------------+----------------+
   | *1.2.840.100   | *JPEG Spectral | *Transfer      | *(2001)*       |
   | 08.1.2.​4.​61* | Selection,     | Syntax*        |                |
   |                | Hierarchical   |                |                |
   |                | (Process 20 &  |                |                |
   |                | 22) (Retired)* |                |                |
   +----------------+----------------+----------------+----------------+
   | *1.2.840.100   | *JPEG Spectral | *Transfer      | *(2001)*       |
   | 08.1.2.​4.​62* | Selection,     | Syntax*        |                |
   |                | Hierarchical   |                |                |
   |                | (Process 21 &  |                |                |
   |                | 23) (Retired)* |                |                |
   +----------------+----------------+----------------+----------------+
   | *1.2.840.100   | *JPEG Full     | *Transfer      | *(2001)*       |
   | 08.1.2.​4.​63* | Progression,   | Syntax*        |                |
   |                | Hierarchical   |                |                |
   |                | (Process 24 &  |                |                |
   |                | 26) (Retired)* |                |                |
   +----------------+----------------+----------------+----------------+
   | *1.2.840.100   | *JPEG Full     | *Transfer      | *(2001)*       |
   | 08.1.2.​4.​64* | Progression,   | Syntax*        |                |
   |                | Hierarchical   |                |                |
   |                | (Process 25 &  |                |                |
   |                | 27) (Retired)* |                |                |
   +----------------+----------------+----------------+----------------+
   | *1.2.840.100   | *JPEG          | *Transfer      | *(2001)*       |
   | 08.1.2.​4.​65* | Lossless,      | Syntax*        |                |
   |                | Hierarchical   |                |                |
   |                | (Process 28)   |                |                |
   |                | (Retired)*     |                |                |
   +----------------+----------------+----------------+----------------+
   | *1.2.840.100   | *JPEG          | *Transfer      | *(2001)*       |
   | 08.1.2.​4.​66* | Lossless,      | Syntax*        |                |
   |                | Hierarchical   |                |                |
   |                | (Process 29)   |                |                |
   |                | (Retired)*     |                |                |
   +----------------+----------------+----------------+----------------+
   | 1.2.840.10     | JPEG Lossless, | Transfer       |                |
   | 008.1.2.​4.​70 | Non            | Syntax         |                |
   |                | -Hierarchical, |                |                |
   |                | First-Order    |                |                |
   |                | Prediction     |                |                |
   |                | (Process 14    |                |                |
   |                | [Selection     |                |                |
   |                | Value 1]):     |                |                |
   |                | Default        |                |                |
   |                | Transfer       |                |                |
   |                | Syntax for     |                |                |
   |                | Lossless JPEG  |                |                |
   |                | Image          |                |                |
   |                | Compression    |                |                |
   +----------------+----------------+----------------+----------------+
   | 1.2.840.10     | JPEG-LS        | Transfer       |                |
   | 008.1.2.​4.​80 | Lossless Image | Syntax         |                |
   |                | Compression    |                |                |
   +----------------+----------------+----------------+----------------+
   | 1.2.840.10     | JPEG-LS Lossy  | Transfer       |                |
   | 008.1.2.​4.​81 | (              | Syntax         |                |
   |                | Near-Lossless) |                |                |
   |                | Image          |                |                |
   |                | Compression    |                |                |
   +----------------+----------------+----------------+----------------+
   | 1.2.840.10     | JPEG 2000      | Transfer       |                |
   | 008.1.2.​4.​90 | Image          | Syntax         |                |
   |                | Compression    |                |                |
   |                | (Lossless      |                |                |
   |                | Only)          |                |                |
   +----------------+----------------+----------------+----------------+
   | 1.2.840.10     | JPEG 2000      | Transfer       |                |
   | 008.1.2.​4.​91 | Image          | Syntax         |                |
   |                | Compression    |                |                |
   +----------------+----------------+----------------+----------------+
   | 1.2.840.10     | JPEG 2000 Part | Transfer       |                |
   | 008.1.2.​4.​92 | 2              | Syntax         |                |
   |                | M              |                |                |
   |                | ulti-component |                |                |
   |                | Image          |                |                |
   |                | Compression    |                |                |
   |                | (Lossless      |                |                |
   |                | Only)          |                |                |
   +----------------+----------------+----------------+----------------+
   | 1.2.840.10     | JPEG 2000 Part | Transfer       |                |
   | 008.1.2.​4.​93 | 2              | Syntax         |                |
   |                | M              |                |                |
   |                | ulti-component |                |                |
   |                | Image          |                |                |
   |                | Compression    |                |                |
   +----------------+----------------+----------------+----------------+
   | 1.2.840.10     | JPIP           | Transfer       |                |
   | 008.1.2.​4.​94 | Referenced     | Syntax         |                |
   +----------------+----------------+----------------+----------------+
   | 1.2.840.10     | JPIP           | Transfer       |                |
   | 008.1.2.​4.​95 | Referenced     | Syntax         |                |
   |                | Deflate        |                |                |
   +----------------+----------------+----------------+----------------+
   | 1.2.840.100    | MPEG2 Main     | Transfer       |                |
   | 08.1.2.​4.​100 | Profile / Main | Syntax         |                |
   |                | Level          |                |                |
   +----------------+----------------+----------------+----------------+
   | 1.2.840.100    | MPEG2 Main     | Transfer       |                |
   | 08.1.2.​4.​101 | Profile / High | Syntax         |                |
   |                | Level          |                |                |
   +----------------+----------------+----------------+----------------+
   | 1.2.840.100    | MPEG-4         | Transfer       |                |
   | 08.1.2.​4.​102 | AVC/H.264 High | Syntax         |                |
   |                | Profile /      |                |                |
   |                | Level 4.1      |                |                |
   +----------------+----------------+----------------+----------------+
   | 1.2.840.100    | MPEG-4         | Transfer       |                |
   | 08.1.2.​4.​103 | AVC/H.264      | Syntax         |                |
   |                | BD-compatible  |                |                |
   |                | High Profile / |                |                |
   |                | Level 4.1      |                |                |
   +----------------+----------------+----------------+----------------+
   | 1.2.840.100    | MPEG-4         | Transfer       |                |
   | 08.1.2.​4.​104 | AVC/H.264 High | Syntax         |                |
   |                | Profile /      |                |                |
   |                | Level 4.2 For  |                |                |
   |                | 2D Video       |                |                |
   +----------------+----------------+----------------+----------------+
   | 1.2.840.100    | MPEG-4         | Transfer       |                |
   | 08.1.2.​4.​105 | AVC/H.264 High | Syntax         |                |
   |                | Profile /      |                |                |
   |                | Level 4.2 For  |                |                |
   |                | 3D Video       |                |                |
   +----------------+----------------+----------------+----------------+
   | 1.2.840.100    | MPEG-4         | Transfer       |                |
   | 08.1.2.​4.​106 | AVC/H.264      | Syntax         |                |
   |                | Stereo High    |                |                |
   |                | Profile /      |                |                |
   |                | Level 4.2      |                |                |
   +----------------+----------------+----------------+----------------+
   | 1.2.840.10     | HEVC/H.265     | Transfer       |                |
   | 008.1.2.​4.107 | Main Profile / | Syntax         |                |
   |                | Level 5.1      |                |                |
   +----------------+----------------+----------------+----------------+
   | 1.2.840.10     | HEVC/H.265     | Transfer       |                |
   | 008.1.2.​4.108 | Main 10        | Syntax         |                |
   |                | Profile /      |                |                |
   |                | Level 5.1      |                |                |
   +----------------+----------------+----------------+----------------+
   | 1.2.840        | RLE Lossless   | Transfer       |                |
   | .10008.1.​2.​5 |                | Syntax         |                |
   +----------------+----------------+----------------+----------------+
   | *1.2.840.10    | *RFC 2557 MIME | *Transfer      | *(2018b)*      |
   | 008.1.2.​6.​1* | encapsulation  | Syntax*        |                |
   |                | (Retired)*     |                |                |
   +----------------+----------------+----------------+----------------+
   | *1.2.840.10    | *XML Encoding  | *Transfer      | *(2018b)*      |
   | 008.1.2.​6.​2* | (Retired)*     | Syntax*        |                |
   +----------------+----------------+----------------+----------------+
   | 1.2.840        | SMPTE ST       | Transfer       |                |
   | .10008.1.2.7.1 | 2110-20        | Syntax         |                |
   |                | Uncompressed   |                |                |
   |                | Progressive    |                |                |
   |                | Active Video   |                |                |
   +----------------+----------------+----------------+----------------+
   | 1.2.840        | SMPTE ST       | Transfer       |                |
   | .10008.1.2.7.2 | 2110-20        | Syntax         |                |
   |                | Uncompressed   |                |                |
   |                | Interlaced     |                |                |
   |                | Active Video   |                |                |
   +----------------+----------------+----------------+----------------+
   | 1.2.840        | SMPTE ST       | Transfer       |                |
   | .10008.1.2.7.3 | 2110-30 PCM    | Syntax         |                |
   |                | Digital Audio  |                |                |
   +----------------+----------------+----------------+----------------+
   | 1.2.840.       | Media Storage  | SOP Class      |                |
   | 10008.1.​3.​10 | Directory      |                |                |
   |                | Storage        |                |                |
   +----------------+----------------+----------------+----------------+
   | 1.2.840.1      | Talairach      | Well-known     |                |
   | 0008.1.4.​1.​1 | Brain Atlas    | frame of       |                |
   |                | Frame of       | reference      |                |
   |                | Reference      |                |                |
   +----------------+----------------+----------------+----------------+
   | 1.2.840.1      | SPM2 T1 Frame  | Well-known     |                |
   | 0008.1.4.​1.​2 | of Reference   | frame of       |                |
   |                |                | reference      |                |
   +----------------+----------------+----------------+----------------+
   | 1.2.840.1      | SPM2 T2 Frame  | Well-known     |                |
   | 0008.1.4.​1.​3 | of Reference   | frame of       |                |
   |                |                | reference      |                |
   +----------------+----------------+----------------+----------------+
   | 1.2.840.1      | SPM2 PD Frame  | Well-known     |                |
   | 0008.1.4.​1.​4 | of Reference   | frame of       |                |
   |                |                | reference      |                |
   +----------------+----------------+----------------+----------------+
   | 1.2.840.1      | SPM2 EPI Frame | Well-known     |                |
   | 0008.1.4.​1.​5 | of Reference   | frame of       |                |
   |                |                | reference      |                |
   +----------------+----------------+----------------+----------------+
   | 1.2.840.1      | SPM2 FIL T1    | Well-known     |                |
   | 0008.1.4.​1.​6 | Frame of       | frame of       |                |
   |                | Reference      | reference      |                |
   +----------------+----------------+----------------+----------------+
   | 1.2.840.1      | SPM2 PET Frame | Well-known     |                |
   | 0008.1.4.​1.​7 | of Reference   | frame of       |                |
   |                |                | reference      |                |
   +----------------+----------------+----------------+----------------+
   | 1.2.840.1      | SPM2 TRANSM    | Well-known     |                |
   | 0008.1.4.​1.​8 | Frame of       | frame of       |                |
   |                | Reference      | reference      |                |
   +----------------+----------------+----------------+----------------+
   | 1.2.840.1      | SPM2 SPECT     | Well-known     |                |
   | 0008.1.4.​1.​9 | Frame of       | frame of       |                |
   |                | Reference      | reference      |                |
   +----------------+----------------+----------------+----------------+
   | 1.2.840.10     | SPM2 GRAY      | Well-known     |                |
   | 008.1.4.​1.​10 | Frame of       | frame of       |                |
   |                | Reference      | reference      |                |
   +----------------+----------------+----------------+----------------+
   | 1.2.840.10     | SPM2 WHITE     | Well-known     |                |
   | 008.1.4.​1.​11 | Frame of       | frame of       |                |
   |                | Reference      | reference      |                |
   +----------------+----------------+----------------+----------------+
   | 1.2.840.10     | SPM2 CSF Frame | Well-known     |                |
   | 008.1.4.​1.​12 | of Reference   | frame of       |                |
   |                |                | reference      |                |
   +----------------+----------------+----------------+----------------+
   | 1.2.840.10     | SPM2 BRAINMASK | Well-known     |                |
   | 008.1.4.​1.​13 | Frame of       | frame of       |                |
   |                | Reference      | reference      |                |
   +----------------+----------------+----------------+----------------+
   | 1.2.840.10     | SPM2 AVG305T1  | Well-known     |                |
   | 008.1.4.​1.​14 | Frame of       | frame of       |                |
   |                | Reference      | reference      |                |
   +----------------+----------------+----------------+----------------+
   | 1.2.840.10     | SPM2 AVG152T1  | Well-known     |                |
   | 008.1.4.​1.​15 | Frame of       | frame of       |                |
   |                | Reference      | reference      |                |
   +----------------+----------------+----------------+----------------+
   | 1.2.840.10     | SPM2 AVG152T2  | Well-known     |                |
   | 008.1.4.​1.​16 | Frame of       | frame of       |                |
   |                | Reference      | reference      |                |
   +----------------+----------------+----------------+----------------+
   | 1.2.840.10     | SPM2 AVG152PD  | Well-known     |                |
   | 008.1.4.​1.​17 | Frame of       | frame of       |                |
   |                | Reference      | reference      |                |
   +----------------+----------------+----------------+----------------+
   | 1.2.840.10     | SPM2           | Well-known     |                |
   | 008.1.4.​1.​18 | SINGLESUBJT1   | frame of       |                |
   |                | Frame of       | reference      |                |
   |                | Reference      |                |                |
   +----------------+----------------+----------------+----------------+
   | 1.2.840.1      | ICBM 452 T1    | Well-known     |                |
   | 0008.1.4.​2.​1 | Frame of       | frame of       |                |
   |                | Reference      | reference      |                |
   +----------------+----------------+----------------+----------------+
   | 1.2.840.1      | ICBM Single    | Well-known     |                |
   | 0008.1.4.​2.​2 | Subject MRI    | frame of       |                |
   |                | Frame of       | reference      |                |
   |                | Reference      |                |                |
   +----------------+----------------+----------------+----------------+
   | 1.2.840        | IEC 61217      | Well-known     | PS3.3          |
   | .10008.1.4.3.1 | Fixed          | frame of       |                |
   |                | Coordinate     | reference      |                |
   |                | System Frame   |                |                |
   |                | of Reference   |                |                |
   +----------------+----------------+----------------+----------------+
   | 1.2.840        | Standard       | Well-known     | PS3.3          |
   | .10008.1.4.3.2 | Robotic-Arm    | frame of       |                |
   |                | Coordinate     | reference      |                |
   |                | System Frame   |                |                |
   |                | of Reference   |                |                |
   +----------------+----------------+----------------+----------------+
   | 1.2.840        | Hot Iron Color | Well-known SOP | PS3.6          |
   | .10008.1.​5.​1 | Palette SOP    | Instance       |                |
   |                | Instance       |                |                |
   +----------------+----------------+----------------+----------------+
   | 1.2.840        | PET Color      | Well-known SOP | PS3.6          |
   | .10008.1.​5.​2 | Palette SOP    | Instance       |                |
   |                | Instance       |                |                |
   +----------------+----------------+----------------+----------------+
   | 1.2.840        | Hot Metal Blue | Well-known SOP | PS3.6          |
   | .10008.1.​5.​3 | Color Palette  | Instance       |                |
   |                | SOP Instance   |                |                |
   +----------------+----------------+----------------+----------------+
   | 1.2.840        | PET 20 Step    | Well-known SOP | PS3.6          |
   | .10008.1.​5.​4 | Color Palette  | Instance       |                |
   |                | SOP Instance   |                |                |
   +----------------+----------------+----------------+----------------+
   | 1.2.840        | Spring Color   | Well-known SOP | PS3.6          |
   | .10008.1.​5.​5 | Palette SOP    | Instance       |                |
   |                | Instance       |                |                |
   +----------------+----------------+----------------+----------------+
   | 1.2.840        | Summer Color   | Well-known SOP | PS3.6          |
   | .10008.1.​5.​6 | Palette SOP    | Instance       |                |
   |                | Instance       |                |                |
   +----------------+----------------+----------------+----------------+
   | 1.2.840        | Fall Color     | Well-known SOP | PS3.6          |
   | .10008.1.​5.​7 | Palette SOP    | Instance       |                |
   |                | Instance       |                |                |
   +----------------+----------------+----------------+----------------+
   | 1.2.840        | Winter Color   | Well-known SOP | PS3.6          |
   | .10008.1.​5.​8 | Palette SOP    | Instance       |                |
   |                | Instance       |                |                |
   +----------------+----------------+----------------+----------------+
   | *1.2.8         | *Basic Study   | *SOP Class*    | *(2004)*       |
   | 40.10008.1.​9* | Content        |                |                |
   |                | Notification   |                |                |
   |                | SOP Class      |                |                |
   |                | (Retired)*     |                |                |
   +----------------+----------------+----------------+----------------+
   | *1.2.84        | *Papyrus 3     | *Transfer      | *(2015c)*      |
   | 0.10008.1.​20* | Implicit VR    | Syntax*        |                |
   |                | Little Endian  |                |                |
   |                | (Retired)*     |                |                |
   +----------------+----------------+----------------+----------------+
   | 1.2.840.       | Storage        | SOP Class      |                |
   | 10008.1.​20.​1 | Commitment     |                |                |
   |                | Push Model SOP |                |                |
   |                | Class          |                |                |
   +----------------+----------------+----------------+----------------+
   | 1.2.840.10     | Storage        | Well-known SOP |                |
   | 008.1.20.​1.​1 | Commitment     | Instance       |                |
   |                | Push Model SOP |                |                |
   |                | Instance       |                |                |
   +----------------+----------------+----------------+----------------+
   | *1.2.840.1     | *Storage       | *SOP Class*    | *(2001)*       |
   | 0008.1.​20.​2* | Commitment     |                |                |
   |                | Pull Model SOP |                |                |
   |                | Class          |                |                |
   |                | (Retired)*     |                |                |
   +----------------+----------------+----------------+----------------+
   | *1.2.840.100   | *Storage       | *Well-known    | *(2001)*       |
   | 08.1.20.​2.​1* | Commitment     | SOP Instance*  |                |
   |                | Pull Model SOP |                |                |
   |                | Instance       |                |                |
   |                | (Retired)*     |                |                |
   +----------------+----------------+----------------+----------------+
   | 1.2.8          | Procedural     | SOP Class      |                |
   | 40.10008.1.​40 | Event Logging  |                |                |
   |                | SOP Class      |                |                |
   +----------------+----------------+----------------+----------------+
   | 1.2.840.       | Procedural     | Well-known SOP |                |
   | 10008.1.​40.​1 | Event Logging  | Instance       |                |
   |                | SOP Instance   |                |                |
   +----------------+----------------+----------------+----------------+
   | 1.2.8          | Substance      | SOP Class      |                |
   | 40.10008.1.​42 | Administration |                |                |
   |                | Logging SOP    |                |                |
   |                | Class          |                |                |
   +----------------+----------------+----------------+----------------+
   | 1.2.840.       | Substance      | Well-known SOP |                |
   | 10008.1.​42.​1 | Administration | Instance       |                |
   |                | Logging SOP    |                |                |
   |                | Instance       |                |                |
   +----------------+----------------+----------------+----------------+
   | 1.2.840        | DICOM UID      | DICOM UIDs as  | PS3.6          |
   | .10008.2.​6.​1 | Registry       | a Coding       |                |
   |                |                | Scheme         |                |
   +----------------+----------------+----------------+----------------+
   | 1.2.840.       | DICOM          | Coding Scheme  |                |
   | 10008.2.​16.​4 | Controlled     |                |                |
   |                | Terminology    |                |                |
   +----------------+----------------+----------------+----------------+
   | 1.2.840.       | Adult Mouse    | Coding Scheme  |                |
   | 10008.2.​16.​5 | Anatomy        |                |                |
   |                | Ontology       |                |                |
   +----------------+----------------+----------------+----------------+
   | 1.2.840.       | Uberon         | Coding Scheme  |                |
   | 10008.2.​16.​6 | Ontology       |                |                |
   +----------------+----------------+----------------+----------------+
   | 1.2.840.       | Integrated     | Coding Scheme  |                |
   | 10008.2.​16.​7 | Taxonomic      |                |                |
   |                | Information    |                |                |
   |                | System (ITIS)  |                |                |
   |                | Taxonomic      |                |                |
   |                | Serial Number  |                |                |
   |                | (TSN)          |                |                |
   +----------------+----------------+----------------+----------------+
   | 1.2.840.       | Mouse Genome   | Coding Scheme  |                |
   | 10008.2.​16.​8 | Initiative     |                |                |
   |                | (MGI)          |                |                |
   +----------------+----------------+----------------+----------------+
   | 1.2.840.       | PubChem        | Coding Scheme  |                |
   | 10008.2.​16.​9 | Compound CID   |                |                |
   +----------------+----------------+----------------+----------------+
   | 1.2.840.1      | ICD-11         | Coding Scheme  |                |
   | 0008.2.​16.​10 |                |                |                |
   +----------------+----------------+----------------+----------------+
   | 1.2.840.1      | New York       | Coding Scheme  |                |
   | 0008.2.​16.​11 | University     |                |                |
   |                | Melanoma       |                |                |
   |                | Clinical       |                |                |
   |                | Cooperative    |                |                |
   |                | Group          |                |                |
   +----------------+----------------+----------------+----------------+
   | 1.2.840.1      | Mayo Clinic    | Coding Scheme  |                |
   | 0008.2.​16.​12 | No             |                |                |
   |                | n-radiological |                |                |
   |                | Images         |                |                |
   |                | Specific Body  |                |                |
   |                | Structure      |                |                |
   |                | Anatomical     |                |                |
   |                | Surface Region |                |                |
   |                | Guide          |                |                |
   +----------------+----------------+----------------+----------------+
   | 1.2.840.1      | Image          | Coding Scheme  |                |
   | 0008.2.​16.​13 | Biomarker      |                |                |
   |                | S              |                |                |
   |                | tandardisation |                |                |
   |                | Initiative     |                |                |
   +----------------+----------------+----------------+----------------+
   | 1.2.840.1      | Radiomics      | Coding Scheme  |                |
   | 0008.2.​16.​14 | Ontology       |                |                |
   +----------------+----------------+----------------+----------------+
   | 1.2.840.1      | RadElement     | Coding Scheme  |                |
   | 0008.2.​16.​15 |                |                |                |
   +----------------+----------------+----------------+----------------+
   | 1.2.840.1      | DICOM          | Application    |                |
   | 0008.3.1.​1.​1 | Application    | Context Name   |                |
   |                | Context Name   |                |                |
   +----------------+----------------+----------------+----------------+
   | *1.2.840.1000  | *Detached      | *SOP Class*    | *(2004)*       |
   | 8.3.1.2.​1.​1* | Patient        |                |                |
   |                | Management SOP |                |                |
   |                | Class          |                |                |
   |                | (Retired)*     |                |                |
   +----------------+----------------+----------------+----------------+
   | *1.2.840.1000  | *Detached      | *Meta SOP      | *(2004)*       |
   | 8.3.1.2.​1.​4* | Patient        | Class*         |                |
   |                | Management     |                |                |
   |                | Meta SOP Class |                |                |
   |                | (Retired)*     |                |                |
   +----------------+----------------+----------------+----------------+
   | *1.2.840.1000  | *Detached      | *SOP Class*    | *(2004)*       |
   | 8.3.1.2.​2.​1* | Visit          |                |                |
   |                | Management SOP |                |                |
   |                | Class          |                |                |
   |                | (Retired)*     |                |                |
   +----------------+----------------+----------------+----------------+
   | *1.2.840.1000  | *Detached      | *SOP Class*    | *(2004)*       |
   | 8.3.1.2.​3.​1* | Study          |                |                |
   |                | Management SOP |                |                |
   |                | Class          |                |                |
   |                | (Retired)*     |                |                |
   +----------------+----------------+----------------+----------------+
   | *1.2.840.1000  | *Study         | *SOP Class*    | *(2004)*       |
   | 8.3.1.2.​3.​2* | Component      |                |                |
   |                | Management SOP |                |                |
   |                | Class          |                |                |
   |                | (Retired)*     |                |                |
   +----------------+----------------+----------------+----------------+
   | 1.2.840.100    | Modality       | SOP Class      |                |
   | 08.3.1.2.​3.​3 | Performed      |                |                |
   |                | Procedure Step |                |                |
   |                | SOP Class      |                |                |
   +----------------+----------------+----------------+----------------+
   | 1.2.840.100    | Modality       | SOP Class      |                |
   | 08.3.1.2.​3.​4 | Performed      |                |                |
   |                | Procedure Step |                |                |
   |                | Retrieve SOP   |                |                |
   |                | Class          |                |                |
   +----------------+----------------+----------------+----------------+
   | 1.2.840.100    | Modality       | SOP Class      |                |
   | 08.3.1.2.​3.​5 | Performed      |                |                |
   |                | Procedure Step |                |                |
   |                | Notification   |                |                |
   |                | SOP Class      |                |                |
   +----------------+----------------+----------------+----------------+
   | *1.2.840.1000  | *Detached      | *SOP Class*    | *(2004)*       |
   | 8.3.1.2.​5.​1* | Results        |                |                |
   |                | Management SOP |                |                |
   |                | Class          |                |                |
   |                | (Retired)*     |                |                |
   +----------------+----------------+----------------+----------------+
   | *1.2.840.1000  | *Detached      | *Meta SOP      | *(2004)*       |
   | 8.3.1.2.​5.​4* | Results        | Class*         |                |
   |                | Management     |                |                |
   |                | Meta SOP Class |                |                |
   |                | (Retired)*     |                |                |
   +----------------+----------------+----------------+----------------+
   | *1.2.840.1000  | *Detached      | *Meta SOP      | *(2004)*       |
   | 8.3.1.2.​5.​5* | Study          | Class*         |                |
   |                | Management     |                |                |
   |                | Meta SOP Class |                |                |
   |                | (Retired)*     |                |                |
   +----------------+----------------+----------------+----------------+
   | *1.2.840.1000  | *Detached      | *SOP Class*    | *(2004)*       |
   | 8.3.1.2.​6.​1* | Interpretation |                |                |
   |                | Management SOP |                |                |
   |                | Class          |                |                |
   |                | (Retired)*     |                |                |
   +----------------+----------------+----------------+----------------+
   | 1.2.           | Storage        | Service Class  |                |
   | 840.10008.4.​2 | Service Class  |                |                |
   +----------------+----------------+----------------+----------------+
   | 1.2.840.1      | Basic Film     | SOP Class      |                |
   | 0008.5.1.​1.​1 | Session SOP    |                |                |
   |                | Class          |                |                |
   +----------------+----------------+----------------+----------------+
   | 1.2.840.1      | Basic Film Box | SOP Class      |                |
   | 0008.5.1.​1.​2 | SOP Class      |                |                |
   +----------------+----------------+----------------+----------------+
   | 1.2.840.1      | Basic          | SOP Class      |                |
   | 0008.5.1.​1.​4 | Grayscale      |                |                |
   |                | Image Box SOP  |                |                |
   |                | Class          |                |                |
   +----------------+----------------+----------------+----------------+
   | 1.2.840.100    | Basic Color    | SOP Class      |                |
   | 08.5.1.1.​4.​1 | Image Box SOP  |                |                |
   |                | Class          |                |                |
   +----------------+----------------+----------------+----------------+
   | *1.2.840.1000  | *Referenced    | *SOP Class*    | *(1998)*       |
   | 8.5.1.1.​4.​2* | Image Box SOP  |                |                |
   |                | Class          |                |                |
   |                | (Retired)*     |                |                |
   +----------------+----------------+----------------+----------------+
   | 1.2.840.1      | Basic          | Meta SOP Class |                |
   | 0008.5.1.​1.​9 | Grayscale      |                |                |
   |                | Print          |                |                |
   |                | Management     |                |                |
   |                | Meta SOP Class |                |                |
   +----------------+----------------+----------------+----------------+
   | *1.2.840.1000  | *Referenced    | *Meta SOP      | *(1998)*       |
   | 8.5.1.1.​9.​1* | Grayscale      | Class*         |                |
   |                | Print          |                |                |
   |                | Management     |                |                |
   |                | Meta SOP Class |                |                |
   |                | (Retired)*     |                |                |
   +----------------+----------------+----------------+----------------+
   | 1.2.840.10     | Print Job SOP  | SOP Class      |                |
   | 008.5.1.​1.​14 | Class          |                |                |
   +----------------+----------------+----------------+----------------+
   | 1.2.840.10     | Basic          | SOP Class      |                |
   | 008.5.1.​1.​15 | Annotation Box |                |                |
   |                | SOP Class      |                |                |
   +----------------+----------------+----------------+----------------+
   | 1.2.840.10     | Printer SOP    | SOP Class      |                |
   | 008.5.1.​1.​16 | Class          |                |                |
   +----------------+----------------+----------------+----------------+
   | 1.2.840.10008. | Printer        | SOP Class      |                |
   | 5.1.1.​16.​376 | Configuration  |                |                |
   |                | Retrieval SOP  |                |                |
   |                | Class          |                |                |
   +----------------+----------------+----------------+----------------+
   | 1.2.840.10     | Printer SOP    | Well-known     |                |
   | 008.5.1.​1.​17 | Instance       | Printer SOP    |                |
   |                |                | Instance       |                |
   +----------------+----------------+----------------+----------------+
   | 1.2.840.10008. | Printer        | Well-known     |                |
   | 5.1.1.​17.​376 | Configuration  | Printer SOP    |                |
   |                | Retrieval SOP  | Instance       |                |
   |                | Instance       |                |                |
   +----------------+----------------+----------------+----------------+
   | 1.2.840.10     | Basic Color    | Meta SOP Class |                |
   | 008.5.1.​1.​18 | Print          |                |                |
   |                | Management     |                |                |
   |                | Meta SOP Class |                |                |
   +----------------+----------------+----------------+----------------+
   | *1.2.840.10008 | *Referenced    | *Meta SOP      | *(1998)*       |
   | .5.1.1.​18.​1* | Color Print    | Class*         |                |
   |                | Management     |                |                |
   |                | Meta SOP Class |                |                |
   |                | (Retired)*     |                |                |
   +----------------+----------------+----------------+----------------+
   | 1.2.840.10     | VOI LUT Box    | SOP Class      |                |
   | 008.5.1.​1.​22 | SOP Class      |                |                |
   +----------------+----------------+----------------+----------------+
   | 1.2.840.10     | Presentation   | SOP Class      |                |
   | 008.5.1.​1.​23 | LUT SOP Class  |                |                |
   +----------------+----------------+----------------+----------------+
   | *1.2.840.100   | *Image Overlay | *SOP Class*    | *(1998)*       |
   | 08.5.1.​1.​24* | Box SOP Class  |                |                |
   |                | (Retired)*     |                |                |
   +----------------+----------------+----------------+----------------+
   | *1.2.840.10008 | *Basic Print   | *SOP Class*    | *(2004)*       |
   | .5.1.1.​24.​1* | Image Overlay  |                |                |
   |                | Box SOP Class  |                |                |
   |                | (Retired)*     |                |                |
   +----------------+----------------+----------------+----------------+
   | *1.2.840.100   | *Print Queue   | *Well-known    | *(2004)*       |
   | 08.5.1.​1.​25* | SOP Instance   | Print Queue    |                |
   |                | (Retired)*     | SOP Instance*  |                |
   +----------------+----------------+----------------+----------------+
   | *1.2.840.100   | *Print Queue   | *SOP Class*    | *(2004)*       |
   | 08.5.1.​1.​26* | Management SOP |                |                |
   |                | Class          |                |                |
   |                | (Retired)*     |                |                |
   +----------------+----------------+----------------+----------------+
   | *1.2.840.100   | *Stored Print  | *SOP Class*    | *(2004)*       |
   | 08.5.1.​1.​27* | Storage SOP    |                |                |
   |                | Class          |                |                |
   |                | (Retired)*     |                |                |
   +----------------+----------------+----------------+----------------+
   | *1.2.840.100   | *Hardcopy      | *SOP Class*    | *(2004)*       |
   | 08.5.1.​1.​29* | Grayscale      |                |                |
   |                | Image Storage  |                |                |
   |                | SOP Class      |                |                |
   |                | (Retired)*     |                |                |
   +----------------+----------------+----------------+----------------+
   | *1.2.840.100   | *Hardcopy      | *SOP Class*    | *(2004)*       |
   | 08.5.1.​1.​30* | Color Image    |                |                |
   |                | Storage SOP    |                |                |
   |                | Class          |                |                |
   |                | (Retired)*     |                |                |
   +----------------+----------------+----------------+----------------+
   | *1.2.840.100   | *Pull Print    | *SOP Class*    | *(2004)*       |
   | 08.5.1.​1.​31* | Request SOP    |                |                |
   |                | Class          |                |                |
   |                | (Retired)*     |                |                |
   +----------------+----------------+----------------+----------------+
   | *1.2.840.100   | *Pull Stored   | *Meta SOP      | *(2004)*       |
   | 08.5.1.​1.​32* | Print          | Class*         |                |
   |                | Management     |                |                |
   |                | Meta SOP Class |                |                |
   |                | (Retired)*     |                |                |
   +----------------+----------------+----------------+----------------+
   | 1.2.840.10     | Media Creation | SOP Class      |                |
   | 008.5.1.​1.​33 | Management SOP |                |                |
   |                | Class UID      |                |                |
   +----------------+----------------+----------------+----------------+
   | 1.2.840.       | Display System | SOP Class      |                |
   | 10008.5.1.1.40 | SOP Class      |                |                |
   +----------------+----------------+----------------+----------------+
   | 1.2.840.10     | Display System | Well-known SOP |                |
   | 008.5.1.1.40.1 | SOP Instance   | Instance       |                |
   +----------------+----------------+----------------+----------------+
   | 1.2.840.10008  | Computed       | SOP Class      |                |
   | .5.1.4.1.​1.​1 | Radiography    |                |                |
   |                | Image Storage  |                |                |
   +----------------+----------------+----------------+----------------+
   | 1.2.84         | Digital X-Ray  | SOP Class      |                |
   | 0.10008.​5.​1. | Image Storage  |                |                |
   | ​4.​1.​1.​1.​1 | - For          |                |                |
   |                | Presentation   |                |                |
   +----------------+----------------+----------------+----------------+
   | 1.2.840.       | Digital X-Ray  | SOP Class      |                |
   | 10008.​5.​1.​4 | Image Storage  |                |                |
   | .​1.​1.1.​1.​1 | - For          |                |                |
   |                | Processing     |                |                |
   +----------------+----------------+----------------+----------------+
   | 1.2.84         | Digital        | SOP Class      |                |
   | 0.10008.​5.​1. | Mammography    |                |                |
   | ​4.​1.​1.​1.​2 | X-Ray Image    |                |                |
   |                | Storage - For  |                |                |
   |                | Presentation   |                |                |
   +----------------+----------------+----------------+----------------+
   | 1.2.840.       | Digital        | SOP Class      |                |
   | 10008.​5.​1.​4 | Mammography    |                |                |
   | .​1.​1.1.​2.​1 | X-Ray Image    |                |                |
   |                | Storage - For  |                |                |
   |                | Processing     |                |                |
   +----------------+----------------+----------------+----------------+
   | 1.2.84         | Digital        | SOP Class      |                |
   | 0.10008.​5.​1. | Intra-Oral     |                |                |
   | ​4.​1.​1.​1.​3 | X-Ray Image    |                |                |
   |                | Storage - For  |                |                |
   |                | Presentation   |                |                |
   +----------------+----------------+----------------+----------------+
   | 1.2.840.       | Digital        | SOP Class      |                |
   | 10008.​5.​1.​4 | Intra-Oral     |                |                |
   | .​1.​1.1.​3.​1 | X-Ray Image    |                |                |
   |                | Storage - For  |                |                |
   |                | Processing     |                |                |
   +----------------+----------------+----------------+----------------+
   | 1.2.840.10008  | CT Image       | SOP Class      |                |
   | .5.1.4.1.​1.​2 | Storage        |                |                |
   +----------------+----------------+----------------+----------------+
   | 1.2.84         | Enhanced CT    | SOP Class      |                |
   | 0.10008.​5.​1. | Image Storage  |                |                |
   | ​4.​1.​1.​2.​1 |                |                |                |
   +----------------+----------------+----------------+----------------+
   | 1.2.84         | Legacy         | SOP Class      |                |
   | 0.10008.​5.​1. | Converted      |                |                |
   | ​4.​1.​1.​2.​2 | Enhanced CT    |                |                |
   |                | Image Storage  |                |                |
   +----------------+----------------+----------------+----------------+
   | *              | *Ultrasound    | *SOP Class*    | *(1993)*       |
   | 1.2.840.10008. | Multi-frame    |                |                |
   | 5.1.4.1.​1.​3* | Image Storage  |                |                |
   |                | (Retired)*     |                |                |
   +----------------+----------------+----------------+----------------+
   | 1.2.84         | Ultrasound     | SOP Class      |                |
   | 0.10008.​5.​1. | Multi-frame    |                |                |
   | ​4.​1.​1.​3.​1 | Image Storage  |                |                |
   +----------------+----------------+----------------+----------------+
   | 1.2.840.10008  | MR Image       | SOP Class      |                |
   | .5.1.4.1.​1.​4 | Storage        |                |                |
   +----------------+----------------+----------------+----------------+
   | 1.2.84         | Enhanced MR    | SOP Class      |                |
   | 0.10008.​5.​1. | Image Storage  |                |                |
   | ​4.​1.​1.​4.​1 |                |                |                |
   +----------------+----------------+----------------+----------------+
   | 1.2.84         | MR             | SOP Class      |                |
   | 0.10008.​5.​1. | Spectroscopy   |                |                |
   | ​4.​1.​1.​4.​2 | Storage        |                |                |
   +----------------+----------------+----------------+----------------+
   | 1.2.84         | Enhanced MR    | SOP Class      |                |
   | 0.10008.​5.​1. | Color Image    |                |                |
   | ​4.​1.​1.​4.​3 | Storage        |                |                |
   +----------------+----------------+----------------+----------------+
   | 1.2.84         | Legacy         | SOP Class      |                |
   | 0.10008.​5.​1. | Converted      |                |                |
   | ​4.​1.​1.​4.​4 | Enhanced MR    |                |                |
   |                | Image Storage  |                |                |
   +----------------+----------------+----------------+----------------+
   | *              | *Nuclear       | *SOP Class*    | *(1993)*       |
   | 1.2.840.10008. | Medicine Image |                |                |
   | 5.1.4.1.​1.​5* | Storage        |                |                |
   |                | (Retired)*     |                |                |
   +----------------+----------------+----------------+----------------+
   | *              | *Ultrasound    | *SOP Class*    | *(1993)*       |
   | 1.2.840.10008. | Image Storage  |                |                |
   | 5.1.4.1.​1.​6* | (Retired)*     |                |                |
   +----------------+----------------+----------------+----------------+
   | 1.2.84         | Ultrasound     | SOP Class      |                |
   | 0.10008.​5.​1. | Image Storage  |                |                |
   | ​4.​1.​1.​6.​1 |                |                |                |
   +----------------+----------------+----------------+----------------+
   | 1.2.84         | Enhanced US    | SOP Class      |                |
   | 0.10008.​5.​1. | Volume Storage |                |                |
   | ​4.​1.​1.​6.​2 |                |                |                |
   +----------------+----------------+----------------+----------------+
   | 1.2.840.10008  | Secondary      | SOP Class      |                |
   | .5.1.4.1.​1.​7 | Capture Image  |                |                |
   |                | Storage        |                |                |
   +----------------+----------------+----------------+----------------+
   | 1.2.84         | Multi-frame    | SOP Class      |                |
   | 0.10008.​5.​1. | Single Bit     |                |                |
   | ​4.​1.​1.​7.​1 | Secondary      |                |                |
   |                | Capture Image  |                |                |
   |                | Storage        |                |                |
   +----------------+----------------+----------------+----------------+
   | 1.2.84         | Multi-frame    | SOP Class      |                |
   | 0.10008.​5.​1. | Grayscale Byte |                |                |
   | ​4.​1.​1.​7.​2 | Secondary      |                |                |
   |                | Capture Image  |                |                |
   |                | Storage        |                |                |
   +----------------+----------------+----------------+----------------+
   | 1.2.84         | Multi-frame    | SOP Class      |                |
   | 0.10008.​5.​1. | Grayscale Word |                |                |
   | ​4.​1.​1.​7.​3 | Secondary      |                |                |
   |                | Capture Image  |                |                |
   |                | Storage        |                |                |
   +----------------+----------------+----------------+----------------+
   | 1.2.84         | Multi-frame    | SOP Class      |                |
   | 0.10008.​5.​1. | True Color     |                |                |
   | ​4.​1.​1.​7.​4 | Secondary      |                |                |
   |                | Capture Image  |                |                |
   |                | Storage        |                |                |
   +----------------+----------------+----------------+----------------+
   | *              | *Standalone    | *SOP Class*    | *(2004)*       |
   | 1.2.840.10008. | Overlay        |                |                |
   | 5.1.4.1.​1.​8* | Storage        |                |                |
   |                | (Retired)*     |                |                |
   +----------------+----------------+----------------+----------------+
   | *              | *Standalone    | *SOP Class*    | *(2004)*       |
   | 1.2.840.10008. | Curve Storage  |                |                |
   | 5.1.4.1.​1.​9* | (Retired)*     |                |                |
   +----------------+----------------+----------------+----------------+
   | *1.2.840       | *Waveform      | *SOP Class*    | *(2007)*       |
   | .10008.​5.​1.​ | Storage -      |                |                |
   | 4.​1.​1.​9.​1* | Trial          |                |                |
   |                | (Retired)*     |                |                |
   +----------------+----------------+----------------+----------------+
   | 1.2.840.       | 12-lead ECG    | SOP Class      |                |
   | 10008.​5.​1.​4 | Waveform       |                |                |
   | .​1.​1.9.​1.​1 | Storage        |                |                |
   +----------------+----------------+----------------+----------------+
   | 1.2.840.       | General ECG    | SOP Class      |                |
   | 10008.​5.​1.​4 | Waveform       |                |                |
   | .​1.​1.9.​1.​2 | Storage        |                |                |
   +----------------+----------------+----------------+----------------+
   | 1.2.840.       | Ambulatory ECG | SOP Class      |                |
   | 10008.​5.​1.​4 | Waveform       |                |                |
   | .​1.​1.9.​1.​3 | Storage        |                |                |
   +----------------+----------------+----------------+----------------+
   | 1.2.840.       | Hemodynamic    | SOP Class      |                |
   | 10008.​5.​1.​4 | Waveform       |                |                |
   | .​1.​1.9.​2.​1 | Storage        |                |                |
   +----------------+----------------+----------------+----------------+
   | 1.2.840.       | Cardiac        | SOP Class      |                |
   | 10008.​5.​1.​4 | Ele            |                |                |
   | .​1.​1.9.​3.​1 | ctrophysiology |                |                |
   |                | Waveform       |                |                |
   |                | Storage        |                |                |
   +----------------+----------------+----------------+----------------+
   | 1.2.840.       | Basic Voice    | SOP Class      |                |
   | 10008.​5.​1.​4 | Audio Waveform |                |                |
   | .​1.​1.9.​4.​1 | Storage        |                |                |
   +----------------+----------------+----------------+----------------+
   | 1.2.840.       | General Audio  | SOP Class      |                |
   | 10008.​5.​1.​4 | Waveform       |                |                |
   | .​1.​1.9.​4.​2 | Storage        |                |                |
   +----------------+----------------+----------------+----------------+
   | 1.2.840.       | Arterial Pulse | SOP Class      |                |
   | 10008.​5.​1.​4 | Waveform       |                |                |
   | .​1.​1.9.​5.​1 | Storage        |                |                |
   +----------------+----------------+----------------+----------------+
   | 1.2.840.       | Respiratory    | SOP Class      |                |
   | 10008.​5.​1.​4 | Waveform       |                |                |
   | .​1.​1.9.​6.​1 | Storage        |                |                |
   +----------------+----------------+----------------+----------------+
   | 1.2.840.       | Multi-channel  | SOP Class      |                |
   | 10008.​5.​1.​4 | Respiratory    |                |                |
   | .​1.​1.9.​6.​2 | Waveform       |                |                |
   |                | Storage        |                |                |
   +----------------+----------------+----------------+----------------+
   | 1.2.840.       | Routine Scalp  | SOP Class      |                |
   | 10008.​5.​1.​4 | Electr         |                |                |
   | .​1.​1.9.​7.​1 | oencephalogram |                |                |
   |                | Waveform       |                |                |
   |                | Storage        |                |                |
   +----------------+----------------+----------------+----------------+
   | 1.2.840.       | Electromyogram | SOP Class      |                |
   | 10008.​5.​1.​4 | Waveform       |                |                |
   | .​1.​1.9.​7.​2 | Storage        |                |                |
   +----------------+----------------+----------------+----------------+
   | 1.2.840.       | El             | SOP Class      |                |
   | 10008.​5.​1.​4 | ectrooculogram |                |                |
   | .​1.​1.9.​7.​3 | Waveform       |                |                |
   |                | Storage        |                |                |
   +----------------+----------------+----------------+----------------+
   | 1.2.840.       | Sleep          | SOP Class      |                |
   | 10008.​5.​1.​4 | Electr         |                |                |
   | .​1.​1.9.​7.​4 | oencephalogram |                |                |
   |                | Waveform       |                |                |
   |                | Storage        |                |                |
   +----------------+----------------+----------------+----------------+
   | 1.2.840.       | Body Position  | SOP Class      |                |
   | 10008.​5.​1.​4 | Waveform       |                |                |
   | .​1.​1.9.​8.​1 | Storage        |                |                |
   +----------------+----------------+----------------+----------------+
   | *1             | *Standalone    | *SOP Class*    | *(2004)*       |
   | .2.840.10008.5 | Modality LUT   |                |                |
   | .1.4.1.​1.​10* | Storage        |                |                |
   |                | (Retired)*     |                |                |
   +----------------+----------------+----------------+----------------+
   | *1             | *Standalone    | *SOP Class*    | *(2004)*       |
   | .2.840.10008.5 | VOI LUT        |                |                |
   | .1.4.1.​1.​11* | Storage        |                |                |
   |                | (Retired)*     |                |                |
   +----------------+----------------+----------------+----------------+
   | 1.2.840        | Grayscale      | SOP Class      |                |
   | .10008.​5.​1.​ | Softcopy       |                |                |
   | 4.​1.​1.​11.​1 | Presentation   |                |                |
   |                | State Storage  |                |                |
   +----------------+----------------+----------------+----------------+
   | 1.2.840        | Color Softcopy | SOP Class      |                |
   | .10008.​5.​1.​ | Presentation   |                |                |
   | 4.​1.​1.​11.​2 | State Storage  |                |                |
   +----------------+----------------+----------------+----------------+
   | 1.2.840        | Pseudo-Color   | SOP Class      |                |
   | .10008.​5.​1.​ | Softcopy       |                |                |
   | 4.​1.​1.​11.​3 | Presentation   |                |                |
   |                | State Storage  |                |                |
   +----------------+----------------+----------------+----------------+
   | 1.2.840        | Blending       | SOP Class      |                |
   | .10008.​5.​1.​ | Softcopy       |                |                |
   | 4.​1.​1.​11.​4 | Presentation   |                |                |
   |                | State Storage  |                |                |
   +----------------+----------------+----------------+----------------+
   | 1.2.840        | XA/XRF         | SOP Class      |                |
   | .10008.​5.​1.​ | Grayscale      |                |                |
   | 4.​1.​1.​11.​5 | Softcopy       |                |                |
   |                | Presentation   |                |                |
   |                | State Storage  |                |                |
   +----------------+----------------+----------------+----------------+
   | 1.2.840        | Grayscale      | SOP Class      |                |
   | .10008.​5.​1.​ | Planar MPR     |                |                |
   | 4.​1.​1.​11.​6 | Volumetric     |                |                |
   |                | Presentation   |                |                |
   |                | State Storage  |                |                |
   +----------------+----------------+----------------+----------------+
   | 1.2.840        | Compositing    | SOP Class      |                |
   | .10008.​5.​1.​ | Planar MPR     |                |                |
   | 4.​1.​1.​11.​7 | Volumetric     |                |                |
   |                | Presentation   |                |                |
   |                | State Storage  |                |                |
   +----------------+----------------+----------------+----------------+
   | 1.2.840        | Advanced       | SOP Class      |                |
   | .10008.​5.​1.​ | Blending       |                |                |
   | 4.​1.​1.​11.​8 | Presentation   |                |                |
   |                | State Storage  |                |                |
   +----------------+----------------+----------------+----------------+
   | 1.2.840        | Volume         | SOP Class      |                |
   | .10008.​5.​1.​ | Rendering      |                |                |
   | 4.​1.​1.​11.​9 | Volumetric     |                |                |
   |                | Presentation   |                |                |
   |                | State Storage  |                |                |
   +----------------+----------------+----------------+----------------+
   | 1.2.840.       | Segmented      | SOP Class      |                |
   | 10008.​5.​1.​4 | Volume         |                |                |
   | .​1.​1.​11.​10 | Rendering      |                |                |
   |                | Volumetric     |                |                |
   |                | Presentation   |                |                |
   |                | State Storage  |                |                |
   +----------------+----------------+----------------+----------------+
   | 1.2.840.       | Multiple       | SOP Class      |                |
   | 10008.​5.​1.​4 | Volume         |                |                |
   | .​1.​1.​11.​11 | Rendering      |                |                |
   |                | Volumetric     |                |                |
   |                | Presentation   |                |                |
   |                | State Storage  |                |                |
   +----------------+----------------+----------------+----------------+
   | 1.2.840        | X-Ray          | SOP Class      |                |
   | .10008.​5.​1.​ | Angiographic   |                |                |
   | 4.​1.​1.​12.​1 | Image Storage  |                |                |
   +----------------+----------------+----------------+----------------+
   | 1.2.840.1      | Enhanced XA    | SOP Class      |                |
   | 0008.​5.​1.​4. | Image Storage  |                |                |
   | ​1.​1.12.​1.​1 |                |                |                |
   +----------------+----------------+----------------+----------------+
   | 1.2.840        | X-Ray          | SOP Class      |                |
   | .10008.​5.​1.​ | Rad            |                |                |
   | 4.​1.​1.​12.​2 | iofluoroscopic |                |                |
   |                | Image Storage  |                |                |
   +----------------+----------------+----------------+----------------+
   | 1.2.840.1      | Enhanced XRF   | SOP Class      |                |
   | 0008.​5.​1.​4. | Image Storage  |                |                |
   | ​1.​1.12.​2.​1 |                |                |                |
   +----------------+----------------+----------------+----------------+
   | *1.2.840.      | *X-Ray         | *SOP Class*    | *(1998)*       |
   | 10008.​5.​1.​4 | Angiographic   |                |                |
   | .​1.​1.​12.​3* | Bi-Plane Image |                |                |
   |                | Storage        |                |                |
   |                | (Retired)*     |                |                |
   +----------------+----------------+----------------+----------------+
   | *1.2.840.1     | *(Retired)*    | *SOP Class*    | *(2015c)*      |
   | 0008.​5.​1.​4. |                |                |                |
   | ​1.​1.​12.​77* |                |                |                |
   +----------------+----------------+----------------+----------------+
   | 1.2.840.1      | X-Ray 3D       | SOP Class      |                |
   | 0008.​5.​1.​4. | Angiographic   |                |                |
   | ​1.​1.13.​1.​1 | Image Storage  |                |                |
   +----------------+----------------+----------------+----------------+
   | 1.2.840.1      | X-Ray 3D       | SOP Class      |                |
   | 0008.​5.​1.​4. | Craniofacial   |                |                |
   | ​1.​1.13.​1.​2 | Image Storage  |                |                |
   +----------------+----------------+----------------+----------------+
   | 1.2.840.1      | Breast         | SOP Class      |                |
   | 0008.​5.​1.​4. | Tomosynthesis  |                |                |
   | ​1.​1.13.​1.​3 | Image Storage  |                |                |
   +----------------+----------------+----------------+----------------+
   | 1.2            | Breast         | SOP Class      |                |
   | .840.10008.​5. | Projection     |                |                |
   | 1.4.1.1.13.1.4 | X-Ray Image    |                |                |
   |                | Storage - For  |                |                |
   |                | Presentation   |                |                |
   +----------------+----------------+----------------+----------------+
   | 1.2            | Breast         | SOP Class      |                |
   | .840.10008.​5. | Projection     |                |                |
   | 1.4.1.1.13.1.5 | X-Ray Image    |                |                |
   |                | Storage - For  |                |                |
   |                | Processing     |                |                |
   +----------------+----------------+----------------+----------------+
   | 1.2.840        | Intravascular  | SOP Class      |                |
   | .10008.​5.​1.​ | Optical        |                |                |
   | 4.​1.​1.​14.​1 | Coherence      |                |                |
   |                | Tomography     |                |                |
   |                | Image Storage  |                |                |
   |                | - For          |                |                |
   |                | Presentation   |                |                |
   +----------------+----------------+----------------+----------------+
   | 1.2.840        | Intravascular  | SOP Class      |                |
   | .10008.​5.​1.​ | Optical        |                |                |
   | 4.​1.​1.​14.​2 | Coherence      |                |                |
   |                | Tomography     |                |                |
   |                | Image Storage  |                |                |
   |                | - For          |                |                |
   |                | Processing     |                |                |
   +----------------+----------------+----------------+----------------+
   | 1.2.840.10008. | Nuclear        | SOP Class      |                |
   | 5.1.4.1.​1.​20 | Medicine Image |                |                |
   |                | Storage        |                |                |
   +----------------+----------------+----------------+----------------+
   | 1.2.840.10008. | Parametric Map | SOP Class      |                |
   | 5.1.4.1.​1.​30 | Storage        |                |                |
   +----------------+----------------+----------------+----------------+
   | *1             | *(Retired)*    | *SOP Class*    | *(2015c)*      |
   | .2.840.10008.5 |                |                |                |
   | .1.4.1.​1.​40* |                |                |                |
   +----------------+----------------+----------------+----------------+
   | 1.2.840.10008. | Raw Data       | SOP Class      |                |
   | 5.1.4.1.​1.​66 | Storage        |                |                |
   +----------------+----------------+----------------+----------------+
   | 1.2.840        | Spatial        | SOP Class      |                |
   | .10008.​5.​1.​ | Registration   |                |                |
   | 4.​1.​1.​66.​1 | Storage        |                |                |
   +----------------+----------------+----------------+----------------+
   | 1.2.840        | Spatial        | SOP Class      |                |
   | .10008.​5.​1.​ | Fiducials      |                |                |
   | 4.​1.​1.​66.​2 | Storage        |                |                |
   +----------------+----------------+----------------+----------------+
   | 1.2.840        | Deformable     | SOP Class      |                |
   | .10008.​5.​1.​ | Spatial        |                |                |
   | 4.​1.​1.​66.​3 | Registration   |                |                |
   |                | Storage        |                |                |
   +----------------+----------------+----------------+----------------+
   | 1.2.840        | Segmentation   | SOP Class      |                |
   | .10008.​5.​1.​ | Storage        |                |                |
   | 4.​1.​1.​66.​4 |                |                |                |
   +----------------+----------------+----------------+----------------+
   | 1.2.840        | Surface        | SOP Class      |                |
   | .10008.​5.​1.​ | Segmentation   |                |                |
   | 4.​1.​1.​66.​5 | Storage        |                |                |
   +----------------+----------------+----------------+----------------+
   | 1.2.840        | Tractography   | SOP Class      |                |
   | .10008.​5.​1.​ | Results        |                |                |
   | 4.​1.​1.​66.​6 | Storage        |                |                |
   +----------------+----------------+----------------+----------------+
   | 1.2.840.10008. | Real World     | SOP Class      |                |
   | 5.1.4.1.​1.​67 | Value Mapping  |                |                |
   |                | Storage        |                |                |
   +----------------+----------------+----------------+----------------+
   | 1.2.840        | Surface Scan   | SOP Class      |                |
   | .10008.​5.​1.​ | Mesh Storage   |                |                |
   | 4.​1.​1.​68.​1 |                |                |                |
   +----------------+----------------+----------------+----------------+
   | 1.2.840        | Surface Scan   | SOP Class      |                |
   | .10008.​5.​1.​ | Point Cloud    |                |                |
   | 4.​1.​1.​68.​2 | Storage        |                |                |
   +----------------+----------------+----------------+----------------+
   | *1.2.840.      | *VL Image      | *SOP Class*    | *(1998)*       |
   | 10008.​5.​1.​4 | Storage -      |                |                |
   | .​1.​1.​77.​1* | Trial          |                |                |
   |                | (Retired)*     |                |                |
   +----------------+----------------+----------------+----------------+
   | *1.2.840.      | *VL            | *SOP Class*    | *(1998)*       |
   | 10008.​5.​1.​4 | Multi-frame    |                |                |
   | .​1.​1.​77.​2* | Image Storage  |                |                |
   |                | - Trial        |                |                |
   |                | (Retired)*     |                |                |
   +----------------+----------------+----------------+----------------+
   | 1.2.840.1      | VL Endoscopic  | SOP Class      |                |
   | 0008.​5.​1.​4. | Image Storage  |                |                |
   | ​1.​1.77.​1.​1 |                |                |                |
   +----------------+----------------+----------------+----------------+
   | 1.2.840.100    | Video          | SOP Class      |                |
   | 08.​5.​1.​4.​1 | Endoscopic     |                |                |
   | .​1.77.1.​1.​1 | Image Storage  |                |                |
   +----------------+----------------+----------------+----------------+
   | 1.2.840.1      | VL Microscopic | SOP Class      |                |
   | 0008.​5.​1.​4. | Image Storage  |                |                |
   | ​1.​1.77.​1.​2 |                |                |                |
   +----------------+----------------+----------------+----------------+
   | 1.2.840.100    | Video          | SOP Class      |                |
   | 08.​5.​1.​4.​1 | Microscopic    |                |                |
   | .​1.77.1.​2.​1 | Image Storage  |                |                |
   +----------------+----------------+----------------+----------------+
   | 1.2.840.1      | VL             | SOP Class      |                |
   | 0008.​5.​1.​4. | Sli            |                |                |
   | ​1.​1.77.​1.​3 | de-Coordinates |                |                |
   |                | Microscopic    |                |                |
   |                | Image Storage  |                |                |
   +----------------+----------------+----------------+----------------+
   | 1.2.840.1      | VL             | SOP Class      |                |
   | 0008.​5.​1.​4. | Photographic   |                |                |
   | ​1.​1.77.​1.​4 | Image Storage  |                |                |
   +----------------+----------------+----------------+----------------+
   | 1.2.840.100    | Video          | SOP Class      |                |
   | 08.​5.​1.​4.​1 | Photographic   |                |                |
   | .​1.77.1.​4.​1 | Image Storage  |                |                |
   +----------------+----------------+----------------+----------------+
   | 1.2.840.100    | Ophthalmic     | SOP Class      |                |
   | 08.​5.​1.​4.​1 | Photography 8  |                |                |
   | .​1.77.1.​5.​1 | Bit Image      |                |                |
   |                | Storage        |                |                |
   +----------------+----------------+----------------+----------------+
   | 1.2.840.100    | Ophthalmic     | SOP Class      |                |
   | 08.​5.​1.​4.​1 | Photography 16 |                |                |
   | .​1.77.1.​5.​2 | Bit Image      |                |                |
   |                | Storage        |                |                |
   +----------------+----------------+----------------+----------------+
   | 1.2.840.100    | Stereometric   | SOP Class      |                |
   | 08.​5.​1.​4.​1 | Relationship   |                |                |
   | .​1.77.1.​5.​3 | Storage        |                |                |
   +----------------+----------------+----------------+----------------+
   | 1.2.840.100    | Ophthalmic     | SOP Class      |                |
   | 08.​5.​1.​4.​1 | Tomography     |                |                |
   | .​1.77.1.​5.​4 | Image Storage  |                |                |
   +----------------+----------------+----------------+----------------+
   | 1.2.840.100    | Wide Field     | SOP Class      |                |
   | 08.​5.​1.​4.​1 | Ophthalmic     |                |                |
   | .​1.77.1.​5.​5 | Photography    |                |                |
   |                | Stereographic  |                |                |
   |                | Projection     |                |                |
   |                | Image Storage  |                |                |
   +----------------+----------------+----------------+----------------+
   | 1.2.840.100    | Wide Field     | SOP Class      |                |
   | 08.​5.​1.​4.​1 | Ophthalmic     |                |                |
   | .​1.77.1.​5.​6 | Photography 3D |                |                |
   |                | Coordinates    |                |                |
   |                | Image Storage  |                |                |
   +----------------+----------------+----------------+----------------+
   | 1.2.840.100    | Ophthalmic     | SOP Class      |                |
   | 08.​5.​1.​4.​1 | Optical        |                |                |
   | .​1.77.1.​5.​7 | Coherence      |                |                |
   |                | Tomography En  |                |                |
   |                | Face Image     |                |                |
   |                | Storage        |                |                |
   +----------------+----------------+----------------+----------------+
   | 1.2.840.100    | Ophthalmic     | SOP Class      |                |
   | 08.​5.​1.​4.​1 | Optical        |                |                |
   | .​1.77.1.​5.​8 | Coherence      |                |                |
   |                | Tomography     |                |                |
   |                | B-scan Volume  |                |                |
   |                | Analysis       |                |                |
   |                | Storage        |                |                |
   +----------------+----------------+----------------+----------------+
   | 1.2.840.1      | VL Whole Slide | SOP Class      |                |
   | 0008.​5.​1.​4. | Microscopy     |                |                |
   | ​1.​1.77.​1.​6 | Image Storage  |                |                |
   +----------------+----------------+----------------+----------------+
   | 1.2.840        | Lensometry     | SOP Class      |                |
   | .10008.​5.​1.​ | Measurements   |                |                |
   | 4.​1.​1.​78.​1 | Storage        |                |                |
   +----------------+----------------+----------------+----------------+
   | 1.2.840        | Autorefraction | SOP Class      |                |
   | .10008.​5.​1.​ | Measurements   |                |                |
   | 4.​1.​1.​78.​2 | Storage        |                |                |
   +----------------+----------------+----------------+----------------+
   | 1.2.840        | Keratometry    | SOP Class      |                |
   | .10008.​5.​1.​ | Measurements   |                |                |
   | 4.​1.​1.​78.​3 | Storage        |                |                |
   +----------------+----------------+----------------+----------------+
   | 1.2.840        | Subjective     | SOP Class      |                |
   | .10008.​5.​1.​ | Refraction     |                |                |
   | 4.​1.​1.​78.​4 | Measurements   |                |                |
   |                | Storage        |                |                |
   +----------------+----------------+----------------+----------------+
   | 1.2.840        | Visual Acuity  | SOP Class      |                |
   | .10008.​5.​1.​ | Measurements   |                |                |
   | 4.​1.​1.​78.​5 | Storage        |                |                |
   +----------------+----------------+----------------+----------------+
   | 1.2.840        | Spectacle      | SOP Class      |                |
   | .10008.​5.​1.​ | Prescription   |                |                |
   | 4.​1.​1.​78.​6 | Report Storage |                |                |
   +----------------+----------------+----------------+----------------+
   | 1.2.840        | Ophthalmic     | SOP Class      |                |
   | .10008.​5.​1.​ | Axial          |                |                |
   | 4.​1.​1.​78.​7 | Measurements   |                |                |
   |                | Storage        |                |                |
   +----------------+----------------+----------------+----------------+
   | 1.2.840        | Intraocular    | SOP Class      |                |
   | .10008.​5.​1.​ | Lens           |                |                |
   | 4.​1.​1.​78.​8 | Calculations   |                |                |
   |                | Storage        |                |                |
   +----------------+----------------+----------------+----------------+
   | 1.2.840        | Macular Grid   | SOP Class      |                |
   | .10008.​5.​1.​ | Thickness and  |                |                |
   | 4.​1.​1.​79.​1 | Volume Report  |                |                |
   |                | Storage        |                |                |
   +----------------+----------------+----------------+----------------+
   | 1.2.840        | Ophthalmic     | SOP Class      |                |
   | .10008.​5.​1.​ | Visual Field   |                |                |
   | 4.​1.​1.​80.​1 | Static         |                |                |
   |                | Perimetry      |                |                |
   |                | Measurements   |                |                |
   |                | Storage        |                |                |
   +----------------+----------------+----------------+----------------+
   | 1.2.840        | Ophthalmic     | SOP Class      |                |
   | .10008.​5.​1.​ | Thickness Map  |                |                |
   | 4.​1.​1.​81.​1 | Storage        |                |                |
   +----------------+----------------+----------------+----------------+
   | 1.2.840        | Corneal        | SOP Class      |                |
   | .10008.​5.​1.​ | Topography Map |                |                |
   | 4.​1.​1.​82.​1 | Storage        |                |                |
   +----------------+----------------+----------------+----------------+
   | *1.2.840.      | *Text SR       | *SOP Class*    | *(2007)*       |
   | 10008.​5.​1.​4 | Storage -      |                |                |
   | .​1.​1.​88.​1* | Trial          |                |                |
   |                | (Retired)*     |                |                |
   +----------------+----------------+----------------+----------------+
   | *1.2.840.      | *Audio SR      | *SOP Class*    | *(2007)*       |
   | 10008.​5.​1.​4 | Storage -      |                |                |
   | .​1.​1.​88.​2* | Trial          |                |                |
   |                | (Retired)*     |                |                |
   +----------------+----------------+----------------+----------------+
   | *1.2.840.      | *Detail SR     | *SOP Class*    | *(2007)*       |
   | 10008.​5.​1.​4 | Storage -      |                |                |
   | .​1.​1.​88.​3* | Trial          |                |                |
   |                | (Retired)*     |                |                |
   +----------------+----------------+----------------+----------------+
   | *1.2.840.      | *Comprehensive | *SOP Class*    | *(2007)*       |
   | 10008.​5.​1.​4 | SR Storage -   |                |                |
   | .​1.​1.​88.​4* | Trial          |                |                |
   |                | (Retired)*     |                |                |
   +----------------+----------------+----------------+----------------+
   | 1.2.840.       | Basic Text SR  | SOP Class      |                |
   | 10008.​5.​1.​4 | Storage        |                |                |
   | .​1.​1.​88.​11 |                |                |                |
   +----------------+----------------+----------------+----------------+
   | 1.2.840.       | Enhanced SR    | SOP Class      |                |
   | 10008.​5.​1.​4 | Storage        |                |                |
   | .​1.​1.​88.​22 |                |                |                |
   +----------------+----------------+----------------+----------------+
   | 1.2.840.       | Comprehensive  | SOP Class      |                |
   | 10008.​5.​1.​4 | SR Storage     |                |                |
   | .​1.​1.​88.​33 |                |                |                |
   +----------------+----------------+----------------+----------------+
   | 1.2.840.       | Comprehensive  | SOP Class      |                |
   | 10008.​5.​1.​4 | 3D SR Storage  |                |                |
   | .​1.​1.​88.​34 |                |                |                |
   +----------------+----------------+----------------+----------------+
   | 1.2.840.       | Extensible SR  | SOP Class      |                |
   | 10008.​5.​1.​4 | Storage        |                |                |
   | .​1.​1.​88.​35 |                |                |                |
   +----------------+----------------+----------------+----------------+
   | 1.2.840.       | Procedure Log  | SOP Class      |                |
   | 10008.​5.​1.​4 | Storage        |                |                |
   | .​1.​1.​88.​40 |                |                |                |
   +----------------+----------------+----------------+----------------+
   | 1.2.840.       | Mammography    | SOP Class      |                |
   | 10008.​5.​1.​4 | CAD SR Storage |                |                |
   | .​1.​1.​88.​50 |                |                |                |
   +----------------+----------------+----------------+----------------+
   | 1.2.840.       | Key Object     | SOP Class      |                |
   | 10008.​5.​1.​4 | Selection      |                |                |
   | .​1.​1.​88.​59 | Document       |                |                |
   |                | Storage        |                |                |
   +----------------+----------------+----------------+----------------+
   | 1.2.840.       | Chest CAD SR   | SOP Class      |                |
   | 10008.​5.​1.​4 | Storage        |                |                |
   | .​1.​1.​88.​65 |                |                |                |
   +----------------+----------------+----------------+----------------+
   | 1.2.840.       | X-Ray          | SOP Class      |                |
   | 10008.​5.​1.​4 | Radiation Dose |                |                |
   | .​1.​1.​88.​67 | SR Storage     |                |                |
   +----------------+----------------+----------------+----------------+
   | 1.2.840.       | Radio          | SOP Class      |                |
   | 10008.​5.​1.​4 | pharmaceutical |                |                |
   | .​1.​1.​88.​68 | Radiation Dose |                |                |
   |                | SR Storage     |                |                |
   +----------------+----------------+----------------+----------------+
   | 1.2.840.       | Colon CAD SR   | SOP Class      |                |
   | 10008.​5.​1.​4 | Storage        |                |                |
   | .​1.​1.​88.​69 |                |                |                |
   +----------------+----------------+----------------+----------------+
   | 1.2.840.       | Implantation   | SOP Class      |                |
   | 10008.​5.​1.​4 | Plan SR        |                |                |
   | .​1.​1.​88.​70 | Storage        |                |                |
   +----------------+----------------+----------------+----------------+
   | 1.2.840        | Acquisition    | SOP Class      |                |
   | .10008.5.​1.​4 | Context SR     |                |                |
   | .​1.​1.​88.​71 | Storage        |                |                |
   +----------------+----------------+----------------+----------------+
   | 1.2.840        | Simplified     | SOP Class      |                |
   | .10008.5.​1.​4 | Adult Echo SR  |                |                |
   | .​1.​1.​88.​72 | Storage        |                |                |
   +----------------+----------------+----------------+----------------+
   | 1.2.840        | Patient        | SOP Class      |                |
   | .10008.5.​1.​4 | Radiation Dose |                |                |
   | .​1.​1.​88.​73 | SR Storage     |                |                |
   +----------------+----------------+----------------+----------------+
   | 1.2.840        | Planned        | SOP Class      |                |
   | .10008.5.​1.​4 | Imaging Agent  |                |                |
   | .​1.​1.​88.​74 | Administration |                |                |
   |                | SR Storage     |                |                |
   +----------------+----------------+----------------+----------------+
   | 1.2.840        | Performed      | SOP Class      |                |
   | .10008.5.​1.​4 | Imaging Agent  |                |                |
   | .​1.​1.​88.​75 | Administration |                |                |
   |                | SR Storage     |                |                |
   +----------------+----------------+----------------+----------------+
   | 1.2.84         | Content        | SOP Class      |                |
   | 0.10008.5.​1.​ | Assessment     |                |                |
   | 4.​1.​1.​90.​1 | Results        |                |                |
   |                | Storage        |                |                |
   +----------------+----------------+----------------+----------------+
   | 1.2.840.       | Encapsulated   | SOP Class      |                |
   | 10008.​5.​1.​4 | PDF Storage    |                |                |
   | .​1.​1.​104.​1 |                |                |                |
   +----------------+----------------+----------------+----------------+
   | 1.2.840.       | Encapsulated   | SOP Class      |                |
   | 10008.​5.​1.​4 | CDA Storage    |                |                |
   | .​1.​1.​104.​2 |                |                |                |
   +----------------+----------------+----------------+----------------+
   | 1.2.840.       | Encapsulated   | SOP Class      |                |
   | 10008.​5.​1.​4 | STL Storage    |                |                |
   | .​1.​1.​104.​3 |                |                |                |
   +----------------+----------------+----------------+----------------+
   | 1.2.840.       | Encapsulated   | SOP Class      |                |
   | 10008.​5.​1.​4 | OBJ Storage    |                |                |
   | .​1.​1.​104.​4 |                |                |                |
   +----------------+----------------+----------------+----------------+
   | 1.2.840.       | Encapsulated   | SOP Class      |                |
   | 10008.​5.​1.​4 | MTL Storage    |                |                |
   | .​1.​1.​104.​5 |                |                |                |
   +----------------+----------------+----------------+----------------+
   | 1              | Positron       | SOP Class      |                |
   | .2.840.10008.5 | Emission       |                |                |
   | .1.4.1.​1.​128 | Tomography     |                |                |
   |                | Image Storage  |                |                |
   +----------------+----------------+----------------+----------------+
   | 1.2.840.       | Legacy         | SOP Class      |                |
   | 10008.​5.​1.​4 | Converted      |                |                |
   | .​1.​1.​128.​1 | Enhanced PET   |                |                |
   |                | Image Storage  |                |                |
   +----------------+----------------+----------------+----------------+
   | *1.            | *Standalone    | *SOP Class*    | *(2004)*       |
   | 2.840.10008.5. | PET Curve      |                |                |
   | 1.4.1.​1.​129* | Storage        |                |                |
   |                | (Retired)*     |                |                |
   +----------------+----------------+----------------+----------------+
   | 1              | Enhanced PET   | SOP Class      |                |
   | .2.840.10008.5 | Image Storage  |                |                |
   | .1.4.1.​1.​130 |                |                |                |
   +----------------+----------------+----------------+----------------+
   | 1              | Basic          | SOP Class      |                |
   | .2.840.10008.5 | Structured     |                |                |
   | .1.4.1.​1.​131 | Display        |                |                |
   |                | Storage        |                |                |
   +----------------+----------------+----------------+----------------+
   | 1              | CT Defined     | SOP Class      |                |
   | .2.840.10008.5 | Procedure      |                |                |
   | .1.4.1.1.200.1 | Protocol       |                |                |
   |                | Storage        |                |                |
   +----------------+----------------+----------------+----------------+
   | 1              | CT Performed   | SOP Class      |                |
   | .2.840.10008.5 | Procedure      |                |                |
   | .1.4.1.1.200.2 | Protocol       |                |                |
   |                | Storage        |                |                |
   +----------------+----------------+----------------+----------------+
   | 1              | Protocol       | SOP Class      |                |
   | .2.840.10008.5 | Approval       |                |                |
   | .1.4.1.1.200.3 | Storage        |                |                |
   +----------------+----------------+----------------+----------------+
   | 1              | Protocol       | SOP Class      |                |
   | .2.840.10008.5 | Approval       |                |                |
   | .1.4.1.1.200.4 | Information    |                |                |
   |                | Model - FIND   |                |                |
   +----------------+----------------+----------------+----------------+
   | 1              | Protocol       | SOP Class      |                |
   | .2.840.10008.5 | Approval       |                |                |
   | .1.4.1.1.200.5 | Information    |                |                |
   |                | Model - MOVE   |                |                |
   +----------------+----------------+----------------+----------------+
   | 1              | Protocol       | SOP Class      |                |
   | .2.840.10008.5 | Approval       |                |                |
   | .1.4.1.1.200.6 | Information    |                |                |
   |                | Model - GET    |                |                |
   +----------------+----------------+----------------+----------------+
   | 1.2.840.       | RT Image       | SOP Class      |                |
   | 10008.​5.​1.​4 | Storage        |                |                |
   | .​1.​1.​481.​1 |                |                |                |
   +----------------+----------------+----------------+----------------+
   | 1.2.840.       | RT Dose        | SOP Class      |                |
   | 10008.​5.​1.​4 | Storage        |                |                |
   | .​1.​1.​481.​2 |                |                |                |
   +----------------+----------------+----------------+----------------+
   | 1.2.840.       | RT Structure   | SOP Class      |                |
   | 10008.​5.​1.​4 | Set Storage    |                |                |
   | .​1.​1.​481.​3 |                |                |                |
   +----------------+----------------+----------------+----------------+
   | 1.2.840.       | RT Beams       | SOP Class      |                |
   | 10008.​5.​1.​4 | Treatment      |                |                |
   | .​1.​1.​481.​4 | Record Storage |                |                |
   +----------------+----------------+----------------+----------------+
   | 1.2.840.       | RT Plan        | SOP Class      |                |
   | 10008.​5.​1.​4 | Storage        |                |                |
   | .​1.​1.​481.​5 |                |                |                |
   +----------------+----------------+----------------+----------------+
   | 1.2.840.       | RT Brachy      | SOP Class      |                |
   | 10008.​5.​1.​4 | Treatment      |                |                |
   | .​1.​1.​481.​6 | Record Storage |                |                |
   +----------------+----------------+----------------+----------------+
   | 1.2.840.       | RT Treatment   | SOP Class      |                |
   | 10008.​5.​1.​4 | Summary Record |                |                |
   | .​1.​1.​481.​7 | Storage        |                |                |
   +----------------+----------------+----------------+----------------+
   | 1.2.840.       | RT Ion Plan    | SOP Class      |                |
   | 10008.​5.​1.​4 | Storage        |                |                |
   | .​1.​1.​481.​8 |                |                |                |
   +----------------+----------------+----------------+----------------+
   | 1.2.840.       | RT Ion Beams   | SOP Class      |                |
   | 10008.​5.​1.​4 | Treatment      |                |                |
   | .​1.​1.​481.​9 | Record Storage |                |                |
   +----------------+----------------+----------------+----------------+
   | 1.2.840.1      | RT Physician   | SOP Class      |                |
   | 0008.​5.​1.​4. | Intent Storage |                |                |
   | ​1.​1.​481.​10 |                |                |                |
   +----------------+----------------+----------------+----------------+
   | 1.2.840.1      | RT Segment     | SOP Class      |                |
   | 0008.​5.​1.​4. | Annotation     |                |                |
   | ​1.​1.​481.​11 | Storage        |                |                |
   +----------------+----------------+----------------+----------------+
   | 1.2.840.1      | RT Radiation   | SOP Class      |                |
   | 0008.​5.​1.​4. | Set Storage    |                |                |
   | ​1.​1.​481.​12 |                |                |                |
   +----------------+----------------+----------------+----------------+
   | 1.2.840.1      | C-Arm          | SOP Class      |                |
   | 0008.​5.​1.​4. | P              |                |                |
   | ​1.​1.​481.​13 | hoton-Electron |                |                |
   |                | Radiation      |                |                |
   |                | Storage        |                |                |
   +----------------+----------------+----------------+----------------+
   | 1.2.840.1      | T              | SOP Class      |                |
   | 0008.​5.​1.​4. | omotherapeutic |                |                |
   | ​1.​1.​481.​14 | Radiation      |                |                |
   |                | Storage        |                |                |
   +----------------+----------------+----------------+----------------+
   | 1.2.840.1      | Robotic-Arm    | SOP Class      |                |
   | 0008.​5.​1.​4. | Radiation      |                |                |
   | ​1.​1.​481.​15 | Storage        |                |                |
   +----------------+----------------+----------------+----------------+
   | 1.2.840.1      | RT Radiation   | SOP Class      |                |
   | 0008.​5.​1.​4. | Record Set     |                |                |
   | ​1.​1.​481.​16 | Storage        |                |                |
   +----------------+----------------+----------------+----------------+
   | 1.2.840.1      | RT Radiation   | SOP Class      |                |
   | 0008.​5.​1.​4. | Salvage Record |                |                |
   | ​1.​1.​481.​17 | Storage        |                |                |
   +----------------+----------------+----------------+----------------+
   | 1.2.840.1      | T              | SOP Class      |                |
   | 0008.​5.​1.​4. | omotherapeutic |                |                |
   | ​1.​1.​481.​18 | Radiation      |                |                |
   |                | Record Storage |                |                |
   +----------------+----------------+----------------+----------------+
   | 1.2.840.1      | C-Arm          | SOP Class      |                |
   | 0008.​5.​1.​4. | P              |                |                |
   | ​1.​1.​481.​19 | hoton-Electron |                |                |
   |                | Radiation      |                |                |
   |                | Record Storage |                |                |
   +----------------+----------------+----------------+----------------+
   | 1.2.840.1      | Robotic        | SOP Class      |                |
   | 0008.​5.​1.​4. | Radiation      |                |                |
   | ​1.​1.​481.​20 | Record Storage |                |                |
   +----------------+----------------+----------------+----------------+
   | 1.2.840.       | DICOS CT Image | SOP Class      | DICOS          |
   | 10008.​5.​1.​4 | Storage        |                |                |
   | .​1.​1.​501.​1 |                |                |                |
   +----------------+----------------+----------------+----------------+
   | 1.2.840.10     | DICOS Digital  | SOP Class      | DICOS          |
   | 008.​5.​1.​4.​ | X-Ray Image    |                |                |
   | 1.​1.501.​2.​1 | Storage - For  |                |                |
   |                | Presentation   |                |                |
   +----------------+----------------+----------------+----------------+
   | 1.2.840.10     | DICOS Digital  | SOP Class      | DICOS          |
   | 008.​5.​1.​4.​ | X-Ray Image    |                |                |
   | 1.​1.501.​2.​2 | Storage - For  |                |                |
   |                | Processing     |                |                |
   +----------------+----------------+----------------+----------------+
   | 1.2.840.       | DICOS Threat   | SOP Class      | DICOS          |
   | 10008.​5.​1.​4 | Detection      |                |                |
   | .​1.​1.​501.​3 | Report Storage |                |                |
   +----------------+----------------+----------------+----------------+
   | 1.2.840.       | DICOS 2D AIT   | SOP Class      | DICOS          |
   | 10008.​5.​1.​4 | Storage        |                |                |
   | .​1.​1.​501.​4 |                |                |                |
   +----------------+----------------+----------------+----------------+
   | 1.2.840.       | DICOS 3D AIT   | SOP Class      | DICOS          |
   | 10008.​5.​1.​4 | Storage        |                |                |
   | .​1.​1.​501.​5 |                |                |                |
   +----------------+----------------+----------------+----------------+
   | 1.2.840.       | DICOS          | SOP Class      | DICOS          |
   | 10008.​5.​1.​4 | Quadrupole     |                |                |
   | .​1.​1.​501.​6 | Resonance (QR) |                |                |
   |                | Storage        |                |                |
   +----------------+----------------+----------------+----------------+
   | 1.2.840.       | Eddy Current   | SOP Class      | DICONDE ASTM   |
   | 10008.​5.​1.​4 | Image Storage  |                | E2934          |
   | .​1.​1.​601.​1 |                |                |                |
   +----------------+----------------+----------------+----------------+
   | 1.2.840.       | Eddy Current   | SOP Class      | DICONDE ASTM   |
   | 10008.​5.​1.​4 | Multi-frame    |                | E2934          |
   | .​1.​1.​601.​2 | Image Storage  |                |                |
   +----------------+----------------+----------------+----------------+
   | 1              | Patient Root   | SOP Class      |                |
   | .2.840.10008.5 | Query/Retrieve |                |                |
   | .1.4.1.2.​1.​1 | Information    |                |                |
   |                | Model - FIND   |                |                |
   +----------------+----------------+----------------+----------------+
   | 1              | Patient Root   | SOP Class      |                |
   | .2.840.10008.5 | Query/Retrieve |                |                |
   | .1.4.1.2.​1.​2 | Information    |                |                |
   |                | Model - MOVE   |                |                |
   +----------------+----------------+----------------+----------------+
   | 1              | Patient Root   | SOP Class      |                |
   | .2.840.10008.5 | Query/Retrieve |                |                |
   | .1.4.1.2.​1.​3 | Information    |                |                |
   |                | Model - GET    |                |                |
   +----------------+----------------+----------------+----------------+
   | 1              | Study Root     | SOP Class      |                |
   | .2.840.10008.5 | Query/Retrieve |                |                |
   | .1.4.1.2.​2.​1 | Information    |                |                |
   |                | Model - FIND   |                |                |
   +----------------+----------------+----------------+----------------+
   | 1              | Study Root     | SOP Class      |                |
   | .2.840.10008.5 | Query/Retrieve |                |                |
   | .1.4.1.2.​2.​2 | Information    |                |                |
   |                | Model - MOVE   |                |                |
   +----------------+----------------+----------------+----------------+
   | 1              | Study Root     | SOP Class      |                |
   | .2.840.10008.5 | Query/Retrieve |                |                |
   | .1.4.1.2.​2.​3 | Information    |                |                |
   |                | Model - GET    |                |                |
   +----------------+----------------+----------------+----------------+
   | *1.            | *Patient/Study | *SOP Class*    | *(2004)*       |
   | 2.840.10008.5. | Only           |                |                |
   | 1.4.1.2.​3.​1* | Query/Retrieve |                |                |
   |                | Information    |                |                |
   |                | Model - FIND   |                |                |
   |                | (Retired)*     |                |                |
   +----------------+----------------+----------------+----------------+
   | *1.            | *Patient/Study | *SOP Class*    | *(2004)*       |
   | 2.840.10008.5. | Only           |                |                |
   | 1.4.1.2.​3.​2* | Query/Retrieve |                |                |
   |                | Information    |                |                |
   |                | Model - MOVE   |                |                |
   |                | (Retired)*     |                |                |
   +----------------+----------------+----------------+----------------+
   | *1.            | *Patient/Study | *SOP Class*    | *(2004)*       |
   | 2.840.10008.5. | Only           |                |                |
   | 1.4.1.2.​3.​3* | Query/Retrieve |                |                |
   |                | Information    |                |                |
   |                | Model - GET    |                |                |
   |                | (Retired)*     |                |                |
   +----------------+----------------+----------------+----------------+
   | 1              | Composite      | SOP Class      |                |
   | .2.840.10008.5 | Instance Root  |                |                |
   | .1.4.1.2.​4.​2 | Retrieve -     |                |                |
   |                | MOVE           |                |                |
   +----------------+----------------+----------------+----------------+
   | 1              | Composite      | SOP Class      |                |
   | .2.840.10008.5 | Instance Root  |                |                |
   | .1.4.1.2.​4.​3 | Retrieve - GET |                |                |
   +----------------+----------------+----------------+----------------+
   | 1              | Composite      | SOP Class      |                |
   | .2.840.10008.5 | Instance       |                |                |
   | .1.4.1.2.​5.​3 | Retrieve       |                |                |
   |                | Without Bulk   |                |                |
   |                | Data - GET     |                |                |
   +----------------+----------------+----------------+----------------+
   | 1.2.840.10     | Defined        | SOP Class      |                |
   | 008.5.1.4.20.1 | Procedure      |                |                |
   |                | Protocol       |                |                |
   |                | Information    |                |                |
   |                | Model - FIND   |                |                |
   +----------------+----------------+----------------+----------------+
   | 1.2.840.10     | Defined        | SOP Class      |                |
   | 008.5.1.4.20.2 | Procedure      |                |                |
   |                | Protocol       |                |                |
   |                | Information    |                |                |
   |                | Model - MOVE   |                |                |
   +----------------+----------------+----------------+----------------+
   | 1.2.840.10     | Defined        | SOP Class      |                |
   | 008.5.1.4.20.3 | Procedure      |                |                |
   |                | Protocol       |                |                |
   |                | Information    |                |                |
   |                | Model - GET    |                |                |
   +----------------+----------------+----------------+----------------+
   | 1.2.840.10     | Modality       | SOP Class      |                |
   | 008.5.1.​4.​31 | Worklist       |                |                |
   |                | Information    |                |                |
   |                | Model - FIND   |                |                |
   +----------------+----------------+----------------+----------------+
   | *1.2.840.100   | *General       | *Meta SOP      | *(2011)*       |
   | 08.5.1.​4.​32* | Purpose        | Class*         |                |
   |                | Worklist       |                |                |
   |                | Management     |                |                |
   |                | Meta SOP Class |                |                |
   |                | (Retired)*     |                |                |
   +----------------+----------------+----------------+----------------+
   | *1.2.840.10008 | *General       | *SOP Class*    | *(2011)*       |
   | .5.1.4.​32.​1* | Purpose        |                |                |
   |                | Worklist       |                |                |
   |                | Information    |                |                |
   |                | Model - FIND   |                |                |
   |                | (Retired)*     |                |                |
   +----------------+----------------+----------------+----------------+
   | *1.2.840.10008 | *General       | *SOP Class*    | *(2011)*       |
   | .5.1.4.​32.​2* | Purpose        |                |                |
   |                | Scheduled      |                |                |
   |                | Procedure Step |                |                |
   |                | SOP Class      |                |                |
   |                | (Retired)*     |                |                |
   +----------------+----------------+----------------+----------------+
   | *1.2.840.10008 | *General       | *SOP Class*    | *(2011)*       |
   | .5.1.4.​32.​3* | Purpose        |                |                |
   |                | Performed      |                |                |
   |                | Procedure Step |                |                |
   |                | SOP Class      |                |                |
   |                | (Retired)*     |                |                |
   +----------------+----------------+----------------+----------------+
   | 1.2.840.10     | Instance       | SOP Class      |                |
   | 008.5.1.​4.​33 | Availability   |                |                |
   |                | Notification   |                |                |
   |                | SOP Class      |                |                |
   +----------------+----------------+----------------+----------------+
   | *1.2.840.10008 | *RT Beams      | *SOP Class*    | *(2009)*       |
   | .5.1.4.​34.​1* | Delivery       |                |                |
   |                | Instruction    |                |                |
   |                | Storage -      |                |                |
   |                | Trial          |                |                |
   |                | (Retired)*     |                |                |
   +----------------+----------------+----------------+----------------+
   | *1.2.840.10008 | *RT            | *SOP Class*    | *(2009)*       |
   | .5.1.4.​34.​2* | Conventional   |                |                |
   |                | Machine        |                |                |
   |                | Verification - |                |                |
   |                | Trial          |                |                |
   |                | (Retired)*     |                |                |
   +----------------+----------------+----------------+----------------+
   | *1.2.840.10008 | *RT Ion        | *SOP Class*    | *(2009)*       |
   | .5.1.4.​34.​3* | Machine        |                |                |
   |                | Verification - |                |                |
   |                | Trial          |                |                |
   |                | (Retired)*     |                |                |
   +----------------+----------------+----------------+----------------+
   | *1.2.840.10008 | *Unified       | *Service       | *(2009)*       |
   | .5.1.4.​34.​4* | Worklist and   | Class*         |                |
   |                | Procedure Step |                |                |
   |                | Service Class  |                |                |
   |                | - Trial        |                |                |
   |                | (Retired)*     |                |                |
   +----------------+----------------+----------------+----------------+
   | *1             | *Unified       | *SOP Class*    | *(2009)*       |
   | .2.840.10008.5 | Procedure Step |                |                |
   | .1.4.34.​4.​1* | - Push SOP     |                |                |
   |                | Class - Trial  |                |                |
   |                | (Retired)*     |                |                |
   +----------------+----------------+----------------+----------------+
   | *1             | *Unified       | *SOP Class*    | *(2009)*       |
   | .2.840.10008.5 | Procedure Step |                |                |
   | .1.4.34.​4.​2* | - Watch SOP    |                |                |
   |                | Class - Trial  |                |                |
   |                | (Retired)*     |                |                |
   +----------------+----------------+----------------+----------------+
   | *1             | *Unified       | *SOP Class*    | *(2009)*       |
   | .2.840.10008.5 | Procedure Step |                |                |
   | .1.4.34.​4.​3* | - Pull SOP     |                |                |
   |                | Class - Trial  |                |                |
   |                | (Retired)*     |                |                |
   +----------------+----------------+----------------+----------------+
   | *1             | *Unified       | *SOP Class*    | *(2009)*       |
   | .2.840.10008.5 | Procedure Step |                |                |
   | .1.4.34.​4.​4* | - Event SOP    |                |                |
   |                | Class - Trial  |                |                |
   |                | (Retired)*     |                |                |
   +----------------+----------------+----------------+----------------+
   | 1.2.840.1000   | UPS Global     | Well-known SOP |                |
   | 8.5.1.4.​34.​5 | Subscription   | Instance       |                |
   |                | SOP Instance   |                |                |
   +----------------+----------------+----------------+----------------+
   | 1              | UPS Filtered   | Well-known SOP |                |
   | .2.840.10008.5 | Global         | Instance       |                |
   | .1.4.​34.​5.​1 | Subscription   |                |                |
   |                | SOP Instance   |                |                |
   +----------------+----------------+----------------+----------------+
   | 1.2.840.1000   | Unified        | Service Class  |                |
   | 8.5.1.4.​34.​6 | Worklist and   |                |                |
   |                | Procedure Step |                |                |
   |                | Service Class  |                |                |
   +----------------+----------------+----------------+----------------+
   | 1.2.840.10008. | Unified        | SOP Class      |                |
   | 5.1.4.34.​6.​1 | Procedure Step |                |                |
   |                | - Push SOP     |                |                |
   |                | Class          |                |                |
   +----------------+----------------+----------------+----------------+
   | 1.2.840.10008. | Unified        | SOP Class      |                |
   | 5.1.4.34.​6.​2 | Procedure Step |                |                |
   |                | - Watch SOP    |                |                |
   |                | Class          |                |                |
   +----------------+----------------+----------------+----------------+
   | 1.2.840.10008. | Unified        | SOP Class      |                |
   | 5.1.4.34.​6.​3 | Procedure Step |                |                |
   |                | - Pull SOP     |                |                |
   |                | Class          |                |                |
   +----------------+----------------+----------------+----------------+
   | 1.2.840.10008. | Unified        | SOP Class      |                |
   | 5.1.4.34.​6.​4 | Procedure Step |                |                |
   |                | - Event SOP    |                |                |
   |                | Class          |                |                |
   +----------------+----------------+----------------+----------------+
   | 1.2.840.10008. | Unified        | SOP Class      |                |
   | 5.1.4.34.​6.​5 | Procedure Step |                |                |
   |                | - Query SOP    |                |                |
   |                | Class          |                |                |
   +----------------+----------------+----------------+----------------+
   | 1.2.840.1000   | RT Beams       | SOP Class      |                |
   | 8.5.1.4.​34.​7 | Delivery       |                |                |
   |                | Instruction    |                |                |
   |                | Storage        |                |                |
   +----------------+----------------+----------------+----------------+
   | 1.2.840.1000   | RT             | SOP Class      |                |
   | 8.5.1.4.​34.​8 | Conventional   |                |                |
   |                | Machine        |                |                |
   |                | Verification   |                |                |
   +----------------+----------------+----------------+----------------+
   | 1.2.840.1000   | RT Ion Machine | SOP Class      |                |
   | 8.5.1.4.​34.​9 | Verification   |                |                |
   +----------------+----------------+----------------+----------------+
   | 1.2.840.10008  | RT Brachy      | SOP Class      |                |
   | .5.1.4.​34.​10 | Application    |                |                |
   |                | Setup Delivery |                |                |
   |                | Instruction    |                |                |
   |                | Storage        |                |                |
   +----------------+----------------+----------------+----------------+
   | 1.2.840.1000   | General        | SOP Class      |                |
   | 8.5.1.4.​37.​1 | Relevant       |                |                |
   |                | Patient        |                |                |
   |                | Information    |                |                |
   |                | Query          |                |                |
   +----------------+----------------+----------------+----------------+
   | 1.2.840.1000   | Breast Imaging | SOP Class      |                |
   | 8.5.1.4.​37.​2 | Relevant       |                |                |
   |                | Patient        |                |                |
   |                | Information    |                |                |
   |                | Query          |                |                |
   +----------------+----------------+----------------+----------------+
   | 1.2.840.1000   | Cardiac        | SOP Class      |                |
   | 8.5.1.4.​37.​3 | Relevant       |                |                |
   |                | Patient        |                |                |
   |                | Information    |                |                |
   |                | Query          |                |                |
   +----------------+----------------+----------------+----------------+
   | 1.2.840.1000   | Hanging        | SOP Class      |                |
   | 8.5.1.4.​38.​1 | Protocol       |                |                |
   |                | Storage        |                |                |
   +----------------+----------------+----------------+----------------+
   | 1.2.840.1000   | Hanging        | SOP Class      |                |
   | 8.5.1.4.​38.​2 | Protocol       |                |                |
   |                | Information    |                |                |
   |                | Model - FIND   |                |                |
   +----------------+----------------+----------------+----------------+
   | 1.2.840.1000   | Hanging        | SOP Class      |                |
   | 8.5.1.4.​38.​3 | Protocol       |                |                |
   |                | Information    |                |                |
   |                | Model - MOVE   |                |                |
   +----------------+----------------+----------------+----------------+
   | 1.2.840.1000   | Hanging        | SOP Class      |                |
   | 8.5.1.4.​38.​4 | Protocol       |                |                |
   |                | Information    |                |                |
   |                | Model - GET    |                |                |
   +----------------+----------------+----------------+----------------+
   | 1.2.840.1000   | Color Palette  | SOP Class      |                |
   | 8.5.1.4.​39.​1 | Storage        |                |                |
   +----------------+----------------+----------------+----------------+
   | 1.2.840.1000   | Color Palette  | SOP Class      |                |
   | 8.5.1.4.​39.​2 | Query/Retrieve |                |                |
   |                | Information    |                |                |
   |                | Model - FIND   |                |                |
   +----------------+----------------+----------------+----------------+
   | 1.2.840.1000   | Color Palette  | SOP Class      |                |
   | 8.5.1.4.​39.​3 | Query/Retrieve |                |                |
   |                | Information    |                |                |
   |                | Model - MOVE   |                |                |
   +----------------+----------------+----------------+----------------+
   | 1.2.840.1000   | Color Palette  | SOP Class      |                |
   | 8.5.1.4.​39.​4 | Query/Retrieve |                |                |
   |                | Information    |                |                |
   |                | Model - GET    |                |                |
   +----------------+----------------+----------------+----------------+
   | 1.2.840.10     | Product        | SOP Class      |                |
   | 008.5.1.​4.​41 | C              |                |                |
   |                | haracteristics |                |                |
   |                | Query SOP      |                |                |
   |                | Class          |                |                |
   +----------------+----------------+----------------+----------------+
   | 1.2.840.10     | Substance      | SOP Class      |                |
   | 008.5.1.​4.​42 | Approval Query |                |                |
   |                | SOP Class      |                |                |
   +----------------+----------------+----------------+----------------+
   | 1.2.840.1000   | Generic        | SOP Class      |                |
   | 8.5.1.4.​43.​1 | Implant        |                |                |
   |                | Template       |                |                |
   |                | Storage        |                |                |
   +----------------+----------------+----------------+----------------+
   | 1.2.840.1000   | Generic        | SOP Class      |                |
   | 8.5.1.4.​43.​2 | Implant        |                |                |
   |                | Template       |                |                |
   |                | Information    |                |                |
   |                | Model - FIND   |                |                |
   +----------------+----------------+----------------+----------------+
   | 1.2.840.1000   | Generic        | SOP Class      |                |
   | 8.5.1.4.​43.​3 | Implant        |                |                |
   |                | Template       |                |                |
   |                | Information    |                |                |
   |                | Model - MOVE   |                |                |
   +----------------+----------------+----------------+----------------+
   | 1.2.840.1000   | Generic        | SOP Class      |                |
   | 8.5.1.4.​43.​4 | Implant        |                |                |
   |                | Template       |                |                |
   |                | Information    |                |                |
   |                | Model - GET    |                |                |
   +----------------+----------------+----------------+----------------+
   | 1.2.840.1000   | Implant        | SOP Class      |                |
   | 8.5.1.4.​44.​1 | Assembly       |                |                |
   |                | Template       |                |                |
   |                | Storage        |                |                |
   +----------------+----------------+----------------+----------------+
   | 1.2.840.1000   | Implant        | SOP Class      |                |
   | 8.5.1.4.​44.​2 | Assembly       |                |                |
   |                | Template       |                |                |
   |                | Information    |                |                |
   |                | Model - FIND   |                |                |
   +----------------+----------------+----------------+----------------+
   | 1.2.840.1000   | Implant        | SOP Class      |                |
   | 8.5.1.4.​44.​3 | Assembly       |                |                |
   |                | Template       |                |                |
   |                | Information    |                |                |
   |                | Model - MOVE   |                |                |
   +----------------+----------------+----------------+----------------+
   | 1.2.840.1000   | Implant        | SOP Class      |                |
   | 8.5.1.4.​44.​4 | Assembly       |                |                |
   |                | Template       |                |                |
   |                | Information    |                |                |
   |                | Model - GET    |                |                |
   +----------------+----------------+----------------+----------------+
   | 1.2.840.1000   | Implant        | SOP Class      |                |
   | 8.5.1.4.​45.​1 | Template Group |                |                |
   |                | Storage        |                |                |
   +----------------+----------------+----------------+----------------+
   | 1.2.840.1000   | Implant        | SOP Class      |                |
   | 8.5.1.4.​45.​2 | Template Group |                |                |
   |                | Information    |                |                |
   |                | Model - FIND   |                |                |
   +----------------+----------------+----------------+----------------+
   | 1.2.840.1000   | Implant        | SOP Class      |                |
   | 8.5.1.4.​45.​3 | Template Group |                |                |
   |                | Information    |                |                |
   |                | Model - MOVE   |                |                |
   +----------------+----------------+----------------+----------------+
   | 1.2.840.1000   | Implant        | SOP Class      |                |
   | 8.5.1.4.​45.​4 | Template Group |                |                |
   |                | Information    |                |                |
   |                | Model - GET    |                |                |
   +----------------+----------------+----------------+----------------+
   | 1.2.840        | Native DICOM   | Application    |                |
   | .10008.7.​1.​1 | Model          | Hosting Model  |                |
   +----------------+----------------+----------------+----------------+
   | 1.2.840        | Abstract       | Application    |                |
   | .10008.7.​1.​2 | Mul            | Hosting Model  |                |
   |                | ti-Dimensional |                |                |
   |                | Image Model    |                |                |
   +----------------+----------------+----------------+----------------+
   | 1.2.840        | DICOM Content  | Mapping        |                |
   | .10008.8.​1.​1 | Mapping        | Resource       |                |
   |                | Resource       |                |                |
   +----------------+----------------+----------------+----------------+
   | 1.2.           | Video          | SOP Class      |                |
   | 840.10008.10.1 | Endoscopic     |                |                |
   |                | Image          |                |                |
   |                | Real-Time      |                |                |
   |                | Communication  |                |                |
   +----------------+----------------+----------------+----------------+
   | 1.2.           | Video          | SOP Class      |                |
   | 840.10008.10.2 | Photographic   |                |                |
   |                | Image          |                |                |
   |                | Real-Time      |                |                |
   |                | Communication  |                |                |
   +----------------+----------------+----------------+----------------+
   | 1.2.           | Audio Waveform | SOP Class      |                |
   | 840.10008.10.3 | Real-Time      |                |                |
   |                | Communication  |                |                |
   +----------------+----------------+----------------+----------------+
   | 1.2.           | Rendition      | SOP Class      |                |
   | 840.10008.10.4 | Selection      |                |                |
   |                | Document       |                |                |
   |                | Real-Time      |                |                |
   |                | Communication  |                |                |
   +----------------+----------------+----------------+----------------+
   | 1.2.840.10     | dic            | LDAP OID       |                |
   | 008.15.0.​3.​1 | om​Device​Name |                |                |
   +----------------+----------------+----------------+----------------+
   | 1.2.840.10     | dic            | LDAP OID       |                |
   | 008.15.0.​3.​2 | om​Description |                |                |
   +----------------+----------------+----------------+----------------+
   | 1.2.840.10     | dico           | LDAP OID       |                |
   | 008.15.0.​3.​3 | m​Manufacturer |                |                |
   +----------------+----------------+----------------+----------------+
   | 1.2.840.10     | d              | LDAP OID       |                |
   | 008.15.0.​3.​4 | icom​Manufactu |                |                |
   |                | rer​Model​Name |                |                |
   +----------------+----------------+----------------+----------------+
   | 1.2.840.10     | dicom​So       | LDAP OID       |                |
   | 008.15.0.​3.​5 | ftware​Version |                |                |
   +----------------+----------------+----------------+----------------+
   | 1.2.840.10     | dic            | LDAP OID       |                |
   | 008.15.0.​3.​6 | om​Vendor​Data |                |                |
   +----------------+----------------+----------------+----------------+
   | 1.2.840.10     | dicomAE​Title  | LDAP OID       |                |
   | 008.15.0.​3.​7 |                |                |                |
   +----------------+----------------+----------------+----------------+
   | 1.2.840.10     | dicom​         | LDAP OID       |                |
   | 008.15.0.​3.​8 | Network​Connec |                |                |
   |                | tion​Reference |                |                |
   +----------------+----------------+----------------+----------------+
   | 1.2.840.10     | dicom​Appli    | LDAP OID       |                |
   | 008.15.0.​3.​9 | cation​Cluster |                |                |
   +----------------+----------------+----------------+----------------+
   | 1.2.840.100    | dicom​Associa  | LDAP OID       |                |
   | 08.15.0.​3.​10 | tion​Initiator |                |                |
   +----------------+----------------+----------------+----------------+
   | 1.2.840.100    | dicom​Associ   | LDAP OID       |                |
   | 08.15.0.​3.​11 | ation​Acceptor |                |                |
   +----------------+----------------+----------------+----------------+
   | 1.2.840.100    | dicom​Hostname | LDAP OID       |                |
   | 08.15.0.​3.​12 |                |                |                |
   +----------------+----------------+----------------+----------------+
   | 1.2.840.100    | dicom​Port     | LDAP OID       |                |
   | 08.15.0.​3.​13 |                |                |                |
   +----------------+----------------+----------------+----------------+
   | 1.2.840.100    | dicomSOP​Class | LDAP OID       |                |
   | 08.15.0.​3.​14 |                |                |                |
   +----------------+----------------+----------------+----------------+
   | 1.2.840.100    | dicom          | LDAP OID       |                |
   | 08.15.0.​3.​15 | ​Transfer​Role |                |                |
   +----------------+----------------+----------------+----------------+
   | 1.2.840.100    | dicom​T        | LDAP OID       |                |
   | 08.15.0.​3.​16 | ransfer​Syntax |                |                |
   +----------------+----------------+----------------+----------------+
   | 1.2.840.100    | dicom​Prima    | LDAP OID       |                |
   | 08.15.0.​3.​17 | ry​Device​Type |                |                |
   +----------------+----------------+----------------+----------------+
   | 1.2.840.100    | di             | LDAP OID       |                |
   | 08.15.0.​3.​18 | com​Related​De |                |                |
   |                | vice​Reference |                |                |
   +----------------+----------------+----------------+----------------+
   | 1.2.840.100    | di             | LDAP OID       |                |
   | 08.15.0.​3.​19 | com​Preferred​ |                |                |
   |                | CalledAE​Title |                |                |
   +----------------+----------------+----------------+----------------+
   | 1.2.840.100    | dicomT         | LDAP OID       |                |
   | 08.15.0.​3.​20 | LS​Cyphersuite |                |                |
   +----------------+----------------+----------------+----------------+
   | 1.2.840.100    | d              | LDAP OID       |                |
   | 08.15.0.​3.​21 | icom​Authorize |                |                |
   |                | d​Node​Certifi |                |                |
   |                | cate​Reference |                |                |
   +----------------+----------------+----------------+----------------+
   | 1.2.840.100    | dicom​Thi      | LDAP OID       |                |
   | 08.15.0.​3.​22 | s​Node​Certifi |                |                |
   |                | cate​Reference |                |                |
   +----------------+----------------+----------------+----------------+
   | 1.2.840.100    | d              | LDAP OID       |                |
   | 08.15.0.​3.​23 | icom​Installed |                |                |
   +----------------+----------------+----------------+----------------+
   | 1.2.840.100    | dico           | LDAP OID       |                |
   | 08.15.0.​3.​24 | m​Station​Name |                |                |
   +----------------+----------------+----------------+----------------+
   | 1.2.840.100    | dicom​Device   | LDAP OID       |                |
   | 08.15.0.​3.​25 | ​Serial​Number |                |                |
   +----------------+----------------+----------------+----------------+
   | 1.2.840.100    | dicom​In       | LDAP OID       |                |
   | 08.15.0.​3.​26 | stitution​Name |                |                |
   +----------------+----------------+----------------+----------------+
   | 1.2.840.100    | dicom​Insti    | LDAP OID       |                |
   | 08.15.0.​3.​27 | tution​Address |                |                |
   +----------------+----------------+----------------+----------------+
   | 1.2.840.100    | dicom          | LDAP OID       |                |
   | 08.15.0.​3.​28 | ​Institution​D |                |                |
   |                | epartment​Name |                |                |
   +----------------+----------------+----------------+----------------+
   | 1.2.840.100    | dicom​Issu     | LDAP OID       |                |
   | 08.15.0.​3.​29 | er​OfPatientID |                |                |
   +----------------+----------------+----------------+----------------+
   | 1.2.840.100    | dic            | LDAP OID       |                |
   | 08.15.0.​3.​30 | om​Preferred​C |                |                |
   |                | allingAE​Title |                |                |
   +----------------+----------------+----------------+----------------+
   | 1.2.840.100    | d              | LDAP OID       |                |
   | 08.15.0.​3.​31 | icom​Supported |                |                |
   |                | ​Character​Set |                |                |
   +----------------+----------------+----------------+----------------+
   | 1.2.840.10     | dicom​Conf     | LDAP OID       |                |
   | 008.15.0.​4.​1 | iguration​Root |                |                |
   +----------------+----------------+----------------+----------------+
   | 1.2.840.10     | dico           | LDAP OID       |                |
   | 008.15.0.​4.​2 | m​Devices​Root |                |                |
   +----------------+----------------+----------------+----------------+
   | 1.2.840.10     | dicom​U        | LDAP OID       |                |
   | 008.15.0.​4.​3 | niqueAE​Titles |                |                |
   |                | ​Registry​Root |                |                |
   +----------------+----------------+----------------+----------------+
   | 1.2.840.10     | dicom​Device   | LDAP OID       |                |
   | 008.15.0.​4.​4 |                |                |                |
   +----------------+----------------+----------------+----------------+
   | 1.2.840.10     | d              | LDAP OID       |                |
   | 008.15.0.​4.​5 | icom​NetworkAE |                |                |
   +----------------+----------------+----------------+----------------+
   | 1.2.840.10     | dicom​Netw     | LDAP OID       |                |
   | 008.15.0.​4.​6 | ork​Connection |                |                |
   +----------------+----------------+----------------+----------------+
   | 1.2.840.10     | dicom​         | LDAP OID       |                |
   | 008.15.0.​4.​7 | UniqueAE​Title |                |                |
   +----------------+----------------+----------------+----------------+
   | 1.2.840.10     | dicom​Trans    | LDAP OID       |                |
   | 008.15.0.​4.​8 | fer​Capability |                |                |
   +----------------+----------------+----------------+----------------+
   | 1.2.840.       | Universal      | S              |                |
   | 10008.15.​1.​1 | Coordinated    | ynchronization |                |
   |                | Time           | Frame of       |                |
   |                |                | Reference      |                |
   +----------------+----------------+----------------+----------------+

.. table:: Well-known Frames of Reference

   +----------------------+----------------------+----------------------+
   | UID Value            | UID Name             | Normative Reference  |
   +======================+======================+======================+
   | 1.2                  | Talairach Brain      | Talairach J. and     |
   | .840.10008.1.4.​1.​1 | Atlas Frame of       | Tournoux P.          |
   |                      | Reference            | Co-Planar            |
   |                      |                      | stereotactic atlas   |
   |                      |                      | of the human brain.  |
   |                      |                      | Stutgart: Georg      |
   |                      |                      | Thieme Verlag, 1988. |
   +----------------------+----------------------+----------------------+
   | 1.2                  | SPM2 T1 Frame of     | `http://​gi          |
   | .840.10008.1.4.​1.​2 | Reference            | thub.com/​spm/​spm2/ |
   |                      |                      | ​blob/​master/templa |
   |                      |                      | tes/T1.mnc <http://g |
   |                      |                      | ithub.com/spm/spm2/b |
   |                      |                      | lob/master/templates |
   |                      |                      | /T1.mnc?raw=true>`__ |
   +----------------------+----------------------+----------------------+
   | 1.2                  | SPM2 T2 Frame of     | `http://​gi          |
   | .840.10008.1.4.​1.​3 | Reference            | thub.com/​spm/​spm2/ |
   |                      |                      | ​blob/​master/templa |
   |                      |                      | tes/T2.mnc <http://g |
   |                      |                      | ithub.com/spm/spm2/b |
   |                      |                      | lob/master/templates |
   |                      |                      | /T2.mnc?raw=true>`__ |
   +----------------------+----------------------+----------------------+
   | 1.2                  | SPM2 PD Frame of     | `http://​gi          |
   | .840.10008.1.4.​1.​4 | Reference            | thub.com/​spm/​spm2/ |
   |                      |                      | ​blob/​master/templa |
   |                      |                      | tes/PD.mnc <http://g |
   |                      |                      | ithub.com/spm/spm2/b |
   |                      |                      | lob/master/templates |
   |                      |                      | /PD.mnc?raw=true>`__ |
   +----------------------+----------------------+----------------------+
   | 1.2                  | SPM2 EPI Frame of    | `http://​gith        |
   | .840.10008.1.4.​1.​5 | Reference            | ub.com/​spm/​spm2/​b |
   |                      |                      | lob/​master/template |
   |                      |                      | s/EPI.mnc <http://gi |
   |                      |                      | thub.com/spm/spm2/bl |
   |                      |                      | ob/master/templates/ |
   |                      |                      | EPI.mnc?raw=true>`__ |
   +----------------------+----------------------+----------------------+
   | 1.2                  | SPM2 FIL T1 Frame of | `http://​github.c    |
   | .840.10008.1.4.​1.​6 | Reference            | om/​spm/​spm2/​blob/ |
   |                      |                      | ​master/templates/fi |
   |                      |                      | lT1.mnc <http://gith |
   |                      |                      | ub.com/spm/spm2/blob |
   |                      |                      | /master/templates/fi |
   |                      |                      | lT1.mnc?raw=true>`__ |
   +----------------------+----------------------+----------------------+
   | 1.2                  | SPM2 PET Frame of    | `http://​gith        |
   | .840.10008.1.4.​1.​7 | Reference            | ub.com/​spm/​spm2/​b |
   |                      |                      | lob/​master/template |
   |                      |                      | s/PET.mnc <http://gi |
   |                      |                      | thub.com/spm/spm2/bl |
   |                      |                      | ob/master/templates/ |
   |                      |                      | PET.mnc?raw=true>`__ |
   +----------------------+----------------------+----------------------+
   | 1.2                  | SPM2 TRANSM Frame of | `http://​github.com  |
   | .840.10008.1.4.​1.​8 | Reference            | /​spm/​spm2/​blob/​m |
   |                      |                      | aster/templates/Tran |
   |                      |                      | sm.mnc <http://githu |
   |                      |                      | b.com/spm/spm2/blob/ |
   |                      |                      | master/templates/Tra |
   |                      |                      | nsm.mnc?raw=true>`__ |
   +----------------------+----------------------+----------------------+
   | 1.2                  | SPM2 SPECT Frame of  | `http://​github.c    |
   | .840.10008.1.4.​1.​9 | Reference            | om/​spm/​spm2/​blob/ |
   |                      |                      | ​master/templates/SP |
   |                      |                      | ECT.mnc <http://gith |
   |                      |                      | ub.com/spm/spm2/blob |
   |                      |                      | /master/templates/SP |
   |                      |                      | ECT.mnc?raw=true>`__ |
   +----------------------+----------------------+----------------------+
   | 1.2.                 | SPM2 GRAY Frame of   | `http://​gi          |
   | 840.10008.1.4.​1.​10 | Reference            | thub.com/​spm/​spm2/ |
   |                      |                      | ​blob/​master/aprior |
   |                      |                      | i/gray.mnc <http://g |
   |                      |                      | ithub.com/spm/spm2/b |
   |                      |                      | lob/master/apriori/g |
   |                      |                      | ray.mnc?raw=true>`__ |
   +----------------------+----------------------+----------------------+
   | 1.2.                 | SPM2 WHITE Frame of  | `http://​gith        |
   | 840.10008.1.4.​1.​11 | Reference            | ub.com/​spm/​spm2/​b |
   |                      |                      | lob/​master/apriori/ |
   |                      |                      | white.mnc <http://gi |
   |                      |                      | thub.com/spm/spm2/bl |
   |                      |                      | ob/master/apriori/wh |
   |                      |                      | ite.mnc?raw=true>`__ |
   +----------------------+----------------------+----------------------+
   | 1.2.                 | SPM2 CSF Frame of    | `http://​            |
   | 840.10008.1.4.​1.​12 | Reference            | github.com/​spm/​spm |
   |                      |                      | 2/​blob/​master/apri |
   |                      |                      | ori/csf.mnc <http:// |
   |                      |                      | github.com/spm/spm2/ |
   |                      |                      | blob/master/apriori/ |
   |                      |                      | csf.mnc?raw=true>`__ |
   +----------------------+----------------------+----------------------+
   | 1.2.                 | SPM2 BRAINMASK Frame | `                    |
   | 840.10008.1.4.​1.​13 | of Reference         | http://​github.com/​ |
   |                      |                      | spm/​spm2/​blob/​mas |
   |                      |                      | ter/apriori/brainmas |
   |                      |                      | k.mnc <http://github |
   |                      |                      | .com/spm/spm2/blob/m |
   |                      |                      | aster/apriori/brainm |
   |                      |                      | ask.mnc?raw=true>`__ |
   +----------------------+----------------------+----------------------+
   | 1.2.                 | SPM2 AVG305T1 Frame  | `ht                  |
   | 840.10008.1.4.​1.​14 | of Reference         | tp://​github.com/​sp |
   |                      |                      | m/​spm2/​blob/​maste |
   |                      |                      | r/canonical/avg305T1 |
   |                      |                      | .mnc <http://github. |
   |                      |                      | com/spm/spm2/blob/ma |
   |                      |                      | ster/canonical/avg30 |
   |                      |                      | 5T1.mnc?raw=true>`__ |
   +----------------------+----------------------+----------------------+
   | 1.2.                 | SPM2 AVG152T1 Frame  | `ht                  |
   | 840.10008.1.4.​1.​15 | of Reference         | tp://​github.com/​sp |
   |                      |                      | m/​spm2/​blob/​maste |
   |                      |                      | r/canonical/avg152T1 |
   |                      |                      | .mnc <http://github. |
   |                      |                      | com/spm/spm2/blob/ma |
   |                      |                      | ster/canonical/avg15 |
   |                      |                      | 2T1.mnc?raw=true>`__ |
   +----------------------+----------------------+----------------------+
   | 1.2.                 | SPM2 AVG152T2 Frame  | `ht                  |
   | 840.10008.1.4.​1.​16 | of Reference         | tp://​github.com/​sp |
   |                      |                      | m/​spm2/​blob/​maste |
   |                      |                      | r/canonical/avg152T2 |
   |                      |                      | .mnc <http://github. |
   |                      |                      | com/spm/spm2/blob/ma |
   |                      |                      | ster/canonical/avg15 |
   |                      |                      | 2T2.mnc?raw=true>`__ |
   +----------------------+----------------------+----------------------+
   | 1.2.                 | SPM2 AVG152PD Frame  | `ht                  |
   | 840.10008.1.4.​1.​17 | of Reference         | tp://​github.com/​sp |
   |                      |                      | m/​spm2/​blob/​maste |
   |                      |                      | r/canonical/avg152PD |
   |                      |                      | .mnc <http://github. |
   |                      |                      | com/spm/spm2/blob/ma |
   |                      |                      | ster/canonical/avg15 |
   |                      |                      | 2PD.mnc?raw=true>`__ |
   +----------------------+----------------------+----------------------+
   | 1.2.                 | SPM2 SINGLESUBJT1    | `http://​github      |
   | 840.10008.1.4.​1.​18 | Frame of Reference   | .com/​spm/​spm2/​blo |
   |                      |                      | b/​master/canonical/ |
   |                      |                      | single_subj_T1.mnc < |
   |                      |                      | http://github.com/sp |
   |                      |                      | m/spm2/blob/master/c |
   |                      |                      | anonical/single_subj |
   |                      |                      | _T1.mnc?raw=true>`__ |
   +----------------------+----------------------+----------------------+
   | 1.2                  | ICBM 452 T1 Frame of | ICBM452 T1 Atlas     |
   | .840.10008.1.4.​2.​1 | Reference            |                      |
   +----------------------+----------------------+----------------------+
   | 1.2                  | ICBM Single Subject  | ICBM Single Subject  |
   | .840.10008.1.4.​2.​2 | MRI Frame of         | MRI Anatomical       |
   |                      | Reference            | Template             |
   +----------------------+----------------------+----------------------+
   | 1                    | IEC 61217 Fixed      | Fixed coordinate     |
   | .2.840.10008.1.4.3.1 | Coordinate System    | system ("f") of      |
   |                      | Frame of Reference   | `b                   |
   |                      |                      | iblioentry_title <#b |
   |                      |                      | iblio_IEC61217-2>`__ |
   |                      |                      | and                  |
   +----------------------+----------------------+----------------------+
   | 1                    | Standard Robotic-Arm | See .                |
   | .2.840.10008.1.4.3.2 | Coordinate System    |                      |
   |                      | Frame of Reference   |                      |
   +----------------------+----------------------+----------------------+

SPM2 (Statistical Parametric Mapping) templates are available at
http://github.com/spm/spm2/, and they are described at
https://github.com/spm/spm2/blob/master/spm_templates.man.

ICBM templates are available at
http://www.loni.ucla.edu/ICBM/ICBM_ICBMAtlases.html.

`table_title <#table_A-3>`__ lists the Context Groups and their UID
values. For retired Context Groups, the edition of the Standard in
parentheses is the edition in which the item last appeared before it was
retired

.. table:: Context Group UID Values

   +----------------+----------------+----------------+--------------+
   | **Context      | **Context      | **Context      | **Comment**  |
   | UID**          | Identifier**   | Group Name**   |              |
   +================+================+================+==============+
   | 1.2.840        |                |                |              |
   | .10008.6.​1.​1 |                |                |              |
   +----------------+----------------+----------------+--------------+
   | 1.2.840        |                |                |              |
   | .10008.6.​1.​2 |                |                |              |
   +----------------+----------------+----------------+--------------+
   | 1.2.840        |                |                |              |
   | .10008.6.​1.​3 |                |                |              |
   +----------------+----------------+----------------+--------------+
   | 1.2.840        |                |                |              |
   | .10008.6.​1.​4 |                |                |              |
   +----------------+----------------+----------------+--------------+
   | 1.2.840        |                |                |              |
   | .10008.6.​1.​5 |                |                |              |
   +----------------+----------------+----------------+--------------+
   | 1.2.840        |                |                |              |
   | .10008.6.​1.​6 |                |                |              |
   +----------------+----------------+----------------+--------------+
   | 1.2.840        |                |                |              |
   | .10008.6.​1.​7 |                |                |              |
   +----------------+----------------+----------------+--------------+
   | 1.2.840        |                |                |              |
   | .10008.6.​1.​8 |                |                |              |
   +----------------+----------------+----------------+--------------+
   | 1.2.840        |                |                |              |
   | .10008.6.​1.​9 |                |                |              |
   +----------------+----------------+----------------+--------------+
   | 1.2.840.       |                |                |              |
   | 10008.6.​1.​10 |                |                |              |
   +----------------+----------------+----------------+--------------+
   | 1.2.840.       |                |                |              |
   | 10008.6.​1.​11 |                |                |              |
   +----------------+----------------+----------------+--------------+
   | 1.2.840.       |                |                |              |
   | 10008.6.​1.​12 |                |                |              |
   +----------------+----------------+----------------+--------------+
   | 1.2.840.       |                |                |              |
   | 10008.6.​1.​13 |                |                |              |
   +----------------+----------------+----------------+--------------+
   | 1.2.840.       |                |                |              |
   | 10008.6.​1.​14 |                |                |              |
   +----------------+----------------+----------------+--------------+
   | 1.2.840.       |                |                |              |
   | 10008.6.​1.​15 |                |                |              |
   +----------------+----------------+----------------+--------------+
   | 1.2.840.       |                |                |              |
   | 10008.6.​1.​16 |                |                |              |
   +----------------+----------------+----------------+--------------+
   | 1.2.840.       |                |                |              |
   | 10008.6.​1.​17 |                |                |              |
   +----------------+----------------+----------------+--------------+
   | 1.2.840.       |                |                |              |
   | 10008.6.​1.​18 |                |                |              |
   +----------------+----------------+----------------+--------------+
   | 1.2.840.       |                |                |              |
   | 10008.6.​1.​19 |                |                |              |
   +----------------+----------------+----------------+--------------+
   | 1.2.840.       |                |                |              |
   | 10008.6.​1.​20 |                |                |              |
   +----------------+----------------+----------------+--------------+
   | 1.2.840.       |                |                |              |
   | 10008.6.​1.​21 |                |                |              |
   +----------------+----------------+----------------+--------------+
   | 1.2.840.       |                |                |              |
   | 10008.6.​1.​22 |                |                |              |
   +----------------+----------------+----------------+--------------+
   | 1.2.840.       |                |                |              |
   | 10008.6.​1.​23 |                |                |              |
   +----------------+----------------+----------------+--------------+
   | 1.2.840.       |                |                |              |
   | 10008.6.​1.​24 |                |                |              |
   +----------------+----------------+----------------+--------------+
   | 1.2.840.       |                |                |              |
   | 10008.6.​1.​25 |                |                |              |
   +----------------+----------------+----------------+--------------+
   | 1.2.840.       |                |                |              |
   | 10008.6.​1.​26 |                |                |              |
   +----------------+----------------+----------------+--------------+
   | 1.2.840.       |                |                |              |
   | 10008.6.​1.​27 |                |                |              |
   +----------------+----------------+----------------+--------------+
   | 1.2.840.       |                |                |              |
   | 10008.6.​1.​28 |                |                |              |
   +----------------+----------------+----------------+--------------+
   | 1.2.840.       |                |                |              |
   | 10008.6.​1.​29 |                |                |              |
   +----------------+----------------+----------------+--------------+
   | 1.2.840.       |                |                |              |
   | 10008.6.​1.​30 |                |                |              |
   +----------------+----------------+----------------+--------------+
   | 1.2.840.       |                |                |              |
   | 10008.6.​1.​31 |                |                |              |
   +----------------+----------------+----------------+--------------+
   | 1.2.840.       |                |                |              |
   | 10008.6.​1.​32 |                |                |              |
   +----------------+----------------+----------------+--------------+
   | 1.2.840.       |                |                |              |
   | 10008.6.​1.​33 |                |                |              |
   +----------------+----------------+----------------+--------------+
   | 1.2.840.       |                |                |              |
   | 10008.6.​1.​34 |                |                |              |
   +----------------+----------------+----------------+--------------+
   | 1.2.840.       |                |                |              |
   | 10008.6.​1.​35 |                |                |              |
   +----------------+----------------+----------------+--------------+
   | 1.2.840.       |                |                |              |
   | 10008.6.​1.​36 |                |                |              |
   +----------------+----------------+----------------+--------------+
   | 1.2.840.       |                |                |              |
   | 10008.6.​1.​37 |                |                |              |
   +----------------+----------------+----------------+--------------+
   | 1.2.840.       |                |                |              |
   | 10008.6.​1.​38 |                |                |              |
   +----------------+----------------+----------------+--------------+
   | 1.2.840.       |                |                |              |
   | 10008.6.​1.​39 |                |                |              |
   +----------------+----------------+----------------+--------------+
   | 1.2.840.       |                |                |              |
   | 10008.6.​1.​40 |                |                |              |
   +----------------+----------------+----------------+--------------+
   | 1.2.840.       |                |                |              |
   | 10008.6.​1.​41 |                |                |              |
   +----------------+----------------+----------------+--------------+
   | 1.2.840.       |                |                |              |
   | 10008.6.​1.​42 |                |                |              |
   +----------------+----------------+----------------+--------------+
   | 1.2.840.       |                |                |              |
   | 10008.6.​1.​43 |                |                |              |
   +----------------+----------------+----------------+--------------+
   | 1.2.840.       |                |                |              |
   | 10008.6.​1.​44 |                |                |              |
   +----------------+----------------+----------------+--------------+
   | 1.2.840.       |                |                |              |
   | 10008.6.​1.​45 |                |                |              |
   +----------------+----------------+----------------+--------------+
   | 1.2.840.       |                |                |              |
   | 10008.6.​1.​46 |                |                |              |
   +----------------+----------------+----------------+--------------+
   | 1.2.840.       |                |                |              |
   | 10008.6.​1.​47 |                |                |              |
   +----------------+----------------+----------------+--------------+
   | 1.2.840.       |                |                |              |
   | 10008.6.​1.​48 |                |                |              |
   +----------------+----------------+----------------+--------------+
   | 1.2.840.       |                |                |              |
   | 10008.6.​1.​49 |                |                |              |
   +----------------+----------------+----------------+--------------+
   | *1.2.840.1     |                |                | *RET (2011)* |
   | 0008.6.​1.​50* |                |                |              |
   +----------------+----------------+----------------+--------------+
   | 1.2.840.       |                |                |              |
   | 10008.6.​1.​51 |                |                |              |
   +----------------+----------------+----------------+--------------+
   | 1.2.840.       |                |                |              |
   | 10008.6.​1.​52 |                |                |              |
   +----------------+----------------+----------------+--------------+
   | 1.2.840.       |                |                |              |
   | 10008.6.​1.​53 |                |                |              |
   +----------------+----------------+----------------+--------------+
   | 1.2.840.       |                |                |              |
   | 10008.6.​1.​54 |                |                |              |
   +----------------+----------------+----------------+--------------+
   | 1.2.840.       |                |                |              |
   | 10008.6.​1.​55 |                |                |              |
   +----------------+----------------+----------------+--------------+
   | 1.2.840.       |                |                |              |
   | 10008.6.​1.​56 |                |                |              |
   +----------------+----------------+----------------+--------------+
   | 1.2.840.       |                |                |              |
   | 10008.6.​1.​57 |                |                |              |
   +----------------+----------------+----------------+--------------+
   | 1.2.840.       |                |                |              |
   | 10008.6.​1.​58 |                |                |              |
   +----------------+----------------+----------------+--------------+
   | 1.2.840.       |                |                |              |
   | 10008.6.​1.​59 |                |                |              |
   +----------------+----------------+----------------+--------------+
   | 1.2.840.       |                |                | *RET (2013)* |
   | 10008.6.​1.​60 |                |                |              |
   +----------------+----------------+----------------+--------------+
   | 1.2.840.       |                |                |              |
   | 10008.6.​1.​61 |                |                |              |
   +----------------+----------------+----------------+--------------+
   | 1.2.840.       |                |                |              |
   | 10008.6.​1.​62 |                |                |              |
   +----------------+----------------+----------------+--------------+
   | 1.2.840.       |                |                |              |
   | 10008.6.​1.​63 |                |                |              |
   +----------------+----------------+----------------+--------------+
   | 1.2.840.       |                |                |              |
   | 10008.6.​1.​64 |                |                |              |
   +----------------+----------------+----------------+--------------+
   | 1.2.840.       |                |                |              |
   | 10008.6.​1.​65 |                |                |              |
   +----------------+----------------+----------------+--------------+
   | 1.2.840.       |                |                |              |
   | 10008.6.​1.​66 |                |                |              |
   +----------------+----------------+----------------+--------------+
   | 1.2.840.       |                |                |              |
   | 10008.6.​1.​67 |                |                |              |
   +----------------+----------------+----------------+--------------+
   | 1.2.840.       |                |                |              |
   | 10008.6.​1.​68 |                |                |              |
   +----------------+----------------+----------------+--------------+
   | 1.2.840.       |                |                |              |
   | 10008.6.​1.​69 |                |                |              |
   +----------------+----------------+----------------+--------------+
   | 1.2.840.       |                |                |              |
   | 10008.6.​1.​70 |                |                |              |
   +----------------+----------------+----------------+--------------+
   | 1.2.840.       |                |                |              |
   | 10008.6.​1.​71 |                |                |              |
   +----------------+----------------+----------------+--------------+
   | 1.2.840.       |                |                |              |
   | 10008.6.​1.​72 |                |                |              |
   +----------------+----------------+----------------+--------------+
   | 1.2.840.       |                |                |              |
   | 10008.6.​1.​73 |                |                |              |
   +----------------+----------------+----------------+--------------+
   | 1.2.840.       |                |                |              |
   | 10008.6.​1.​74 |                |                |              |
   +----------------+----------------+----------------+--------------+
   | 1.2.840.       |                |                |              |
   | 10008.6.​1.​75 |                |                |              |
   +----------------+----------------+----------------+--------------+
   | 1.2.840.       |                |                |              |
   | 10008.6.​1.​76 |                |                |              |
   +----------------+----------------+----------------+--------------+
   | 1.2.840.       |                |                |              |
   | 10008.6.​1.​77 |                |                |              |
   +----------------+----------------+----------------+--------------+
   | 1.2.840.       |                |                |              |
   | 10008.6.​1.​78 |                |                |              |
   +----------------+----------------+----------------+--------------+
   | 1.2.840.       |                |                |              |
   | 10008.6.​1.​79 |                |                |              |
   +----------------+----------------+----------------+--------------+
   | 1.2.840.       |                |                |              |
   | 10008.6.​1.​80 |                |                |              |
   +----------------+----------------+----------------+--------------+
   | 1.2.840.       |                |                |              |
   | 10008.6.​1.​81 |                |                |              |
   +----------------+----------------+----------------+--------------+
   | 1.2.840.       |                |                |              |
   | 10008.6.​1.​82 |                |                |              |
   +----------------+----------------+----------------+--------------+
   | 1.2.840.       |                |                |              |
   | 10008.6.​1.​83 |                |                |              |
   +----------------+----------------+----------------+--------------+
   | 1.2.840.       |                |                |              |
   | 10008.6.​1.​84 |                |                |              |
   +----------------+----------------+----------------+--------------+
   | 1.2.840.       |                |                |              |
   | 10008.6.​1.​85 |                |                |              |
   +----------------+----------------+----------------+--------------+
   | 1.2.840.       |                |                |              |
   | 10008.6.​1.​86 |                |                |              |
   +----------------+----------------+----------------+--------------+
   | 1.2.840.       |                |                |              |
   | 10008.6.​1.​87 |                |                |              |
   +----------------+----------------+----------------+--------------+
   | 1.2.840.       |                |                |              |
   | 10008.6.​1.​88 |                |                |              |
   +----------------+----------------+----------------+--------------+
   | 1.2.840.       |                |                |              |
   | 10008.6.​1.​89 |                |                |              |
   +----------------+----------------+----------------+--------------+
   | 1.2.840.       |                |                |              |
   | 10008.6.​1.​90 |                |                |              |
   +----------------+----------------+----------------+--------------+
   | 1.2.840.       |                |                |              |
   | 10008.6.​1.​91 |                |                |              |
   +----------------+----------------+----------------+--------------+
   | 1.2.840.       |                |                |              |
   | 10008.6.​1.​92 |                |                |              |
   +----------------+----------------+----------------+--------------+
   | 1.2.840.       |                |                |              |
   | 10008.6.​1.​93 |                |                |              |
   +----------------+----------------+----------------+--------------+
   | 1.2.840.       |                |                |              |
   | 10008.6.​1.​94 |                |                |              |
   +----------------+----------------+----------------+--------------+
   | 1.2.840.       |                |                |              |
   | 10008.6.​1.​95 |                |                |              |
   +----------------+----------------+----------------+--------------+
   | 1.2.840.       |                |                |              |
   | 10008.6.​1.​96 |                |                |              |
   +----------------+----------------+----------------+--------------+
   | 1.2.840.       |                |                |              |
   | 10008.6.​1.​97 |                |                |              |
   +----------------+----------------+----------------+--------------+
   | 1.2.840.       |                |                |              |
   | 10008.6.​1.​98 |                |                |              |
   +----------------+----------------+----------------+--------------+
   | 1.2.840.       |                |                |              |
   | 10008.6.​1.​99 |                |                |              |
   +----------------+----------------+----------------+--------------+
   | 1.2.840.1      |                |                |              |
   | 0008.6.​1.​100 |                |                |              |
   +----------------+----------------+----------------+--------------+
   | 1.2.840.1      |                |                |              |
   | 0008.6.​1.​101 |                |                |              |
   +----------------+----------------+----------------+--------------+
   | 1.2.840.1      |                |                |              |
   | 0008.6.​1.​102 |                |                |              |
   +----------------+----------------+----------------+--------------+
   | 1.2.840.1      |                |                |              |
   | 0008.6.​1.​103 |                |                |              |
   +----------------+----------------+----------------+--------------+
   | 1.2.840.1      |                |                |              |
   | 0008.6.​1.​104 |                |                |              |
   +----------------+----------------+----------------+--------------+
   | 1.2.840.1      |                |                |              |
   | 0008.6.​1.​105 |                |                |              |
   +----------------+----------------+----------------+--------------+
   | 1.2.840.1      |                |                |              |
   | 0008.6.​1.​106 |                |                |              |
   +----------------+----------------+----------------+--------------+
   | 1.2.840.1      |                |                |              |
   | 0008.6.​1.​107 |                |                |              |
   +----------------+----------------+----------------+--------------+
   | 1.2.840.1      |                |                |              |
   | 0008.6.​1.​108 |                |                |              |
   +----------------+----------------+----------------+--------------+
   | 1.2.840.1      |                |                |              |
   | 0008.6.​1.​109 |                |                |              |
   +----------------+----------------+----------------+--------------+
   | 1.2.840.1      |                |                |              |
   | 0008.6.​1.​110 |                |                |              |
   +----------------+----------------+----------------+--------------+
   | 1.2.840.1      |                |                |              |
   | 0008.6.​1.​111 |                |                |              |
   +----------------+----------------+----------------+--------------+
   | 1.2.840.1      |                |                |              |
   | 0008.6.​1.​112 |                |                |              |
   +----------------+----------------+----------------+--------------+
   | 1.2.840.1      |                |                |              |
   | 0008.6.​1.​113 |                |                |              |
   +----------------+----------------+----------------+--------------+
   | 1.2.840.1      |                |                |              |
   | 0008.6.​1.​114 |                |                |              |
   +----------------+----------------+----------------+--------------+
   | 1.2.840.1      |                |                |              |
   | 0008.6.​1.​115 |                |                |              |
   +----------------+----------------+----------------+--------------+
   | 1.2.840.1      |                |                |              |
   | 0008.6.​1.​116 |                |                |              |
   +----------------+----------------+----------------+--------------+
   | 1.2.840.1      |                |                |              |
   | 0008.6.​1.​117 |                |                |              |
   +----------------+----------------+----------------+--------------+
   | 1.2.840.1      |                |                |              |
   | 0008.6.​1.​118 |                |                |              |
   +----------------+----------------+----------------+--------------+
   | 1.2.840.1      |                |                |              |
   | 0008.6.​1.​119 |                |                |              |
   +----------------+----------------+----------------+--------------+
   | 1.2.840.1      |                |                |              |
   | 0008.6.​1.​120 |                |                |              |
   +----------------+----------------+----------------+--------------+
   | 1.2.840.1      |                |                |              |
   | 0008.6.​1.​121 |                |                |              |
   +----------------+----------------+----------------+--------------+
   | 1.2.840.1      |                |                |              |
   | 0008.6.​1.​122 |                |                |              |
   +----------------+----------------+----------------+--------------+
   | 1.2.840.1      |                |                |              |
   | 0008.6.​1.​123 |                |                |              |
   +----------------+----------------+----------------+--------------+
   | 1.2.840.1      |                |                |              |
   | 0008.6.​1.​124 |                |                |              |
   +----------------+----------------+----------------+--------------+
   | 1.2.840.1      |                |                |              |
   | 0008.6.​1.​125 |                |                |              |
   +----------------+----------------+----------------+--------------+
   | 1.2.840.1      |                |                |              |
   | 0008.6.​1.​126 |                |                |              |
   +----------------+----------------+----------------+--------------+
   | 1.2.840.1      |                |                |              |
   | 0008.6.​1.​127 |                |                |              |
   +----------------+----------------+----------------+--------------+
   | 1.2.840.1      |                |                |              |
   | 0008.6.​1.​128 |                |                |              |
   +----------------+----------------+----------------+--------------+
   | 1.2.840.1      |                |                |              |
   | 0008.6.​1.​129 |                |                |              |
   +----------------+----------------+----------------+--------------+
   | 1.2.840.1      |                |                |              |
   | 0008.6.​1.​130 |                |                |              |
   +----------------+----------------+----------------+--------------+
   | 1.2.840.1      |                |                |              |
   | 0008.6.​1.​131 |                |                |              |
   +----------------+----------------+----------------+--------------+
   | 1.2.840.1      |                |                |              |
   | 0008.6.​1.​132 |                |                |              |
   +----------------+----------------+----------------+--------------+
   | 1.2.840.1      |                |                |              |
   | 0008.6.​1.​133 |                |                |              |
   +----------------+----------------+----------------+--------------+
   | 1.2.840.1      |                |                |              |
   | 0008.6.​1.​134 |                |                |              |
   +----------------+----------------+----------------+--------------+
   | 1.2.840.1      |                |                |              |
   | 0008.6.​1.​135 |                |                |              |
   +----------------+----------------+----------------+--------------+
   | 1.2.840.1      |                |                |              |
   | 0008.6.​1.​136 |                |                |              |
   +----------------+----------------+----------------+--------------+
   | 1.2.840.1      |                |                |              |
   | 0008.6.​1.​137 |                |                |              |
   +----------------+----------------+----------------+--------------+
   | 1.2.840.1      |                |                |              |
   | 0008.6.​1.​138 |                |                |              |
   +----------------+----------------+----------------+--------------+
   | 1.2.840.1      |                |                |              |
   | 0008.6.​1.​139 |                |                |              |
   +----------------+----------------+----------------+--------------+
   | 1.2.840.1      |                |                |              |
   | 0008.6.​1.​140 |                |                |              |
   +----------------+----------------+----------------+--------------+
   | 1.2.840.1      |                |                |              |
   | 0008.6.​1.​141 |                |                |              |
   +----------------+----------------+----------------+--------------+
   | 1.2.840.1      |                |                |              |
   | 0008.6.​1.​142 |                |                |              |
   +----------------+----------------+----------------+--------------+
   | 1.2.840.1      |                |                |              |
   | 0008.6.​1.​143 |                |                |              |
   +----------------+----------------+----------------+--------------+
   | 1.2.840.1      |                |                |              |
   | 0008.6.​1.​144 |                |                |              |
   +----------------+----------------+----------------+--------------+
   | 1.2.840.1      |                |                |              |
   | 0008.6.​1.​145 |                |                |              |
   +----------------+----------------+----------------+--------------+
   | 1.2.840.1      |                |                |              |
   | 0008.6.​1.​146 |                |                |              |
   +----------------+----------------+----------------+--------------+
   | 1.2.840.1      |                |                |              |
   | 0008.6.​1.​147 |                |                |              |
   +----------------+----------------+----------------+--------------+
   | 1.2.840.1      |                |                |              |
   | 0008.6.​1.​148 |                |                |              |
   +----------------+----------------+----------------+--------------+
   | 1.2.840.1      |                |                |              |
   | 0008.6.​1.​149 |                |                |              |
   +----------------+----------------+----------------+--------------+
   | 1.2.840.1      |                |                |              |
   | 0008.6.​1.​150 |                |                |              |
   +----------------+----------------+----------------+--------------+
   | 1.2.840.1      |                |                |              |
   | 0008.6.​1.​151 |                |                |              |
   +----------------+----------------+----------------+--------------+
   | 1.2.840.1      |                |                |              |
   | 0008.6.​1.​152 |                |                |              |
   +----------------+----------------+----------------+--------------+
   | 1.2.840.1      |                |                |              |
   | 0008.6.​1.​153 |                |                |              |
   +----------------+----------------+----------------+--------------+
   | 1.2.840.1      |                |                |              |
   | 0008.6.​1.​154 |                |                |              |
   +----------------+----------------+----------------+--------------+
   | 1.2.840.1      |                |                |              |
   | 0008.6.​1.​155 |                |                |              |
   +----------------+----------------+----------------+--------------+
   | 1.2.840.1      |                |                |              |
   | 0008.6.​1.​156 |                |                |              |
   +----------------+----------------+----------------+--------------+
   | 1.2.840.1      |                |                |              |
   | 0008.6.​1.​157 |                |                |              |
   +----------------+----------------+----------------+--------------+
   | 1.2.840.1      |                |                |              |
   | 0008.6.​1.​158 |                |                |              |
   +----------------+----------------+----------------+--------------+
   | 1.2.840.1      |                |                |              |
   | 0008.6.​1.​159 |                |                |              |
   +----------------+----------------+----------------+--------------+
   | 1.2.840.1      |                |                |              |
   | 0008.6.​1.​160 |                |                |              |
   +----------------+----------------+----------------+--------------+
   | 1.2.840.1      |                |                |              |
   | 0008.6.​1.​161 |                |                |              |
   +----------------+----------------+----------------+--------------+
   | 1.2.840.1      |                |                |              |
   | 0008.6.​1.​162 |                |                |              |
   +----------------+----------------+----------------+--------------+
   | 1.2.840.1      |                |                |              |
   | 0008.6.​1.​163 |                |                |              |
   +----------------+----------------+----------------+--------------+
   | 1.2.840.1      |                |                |              |
   | 0008.6.​1.​164 |                |                |              |
   +----------------+----------------+----------------+--------------+
   | 1.2.840.1      |                |                |              |
   | 0008.6.​1.​165 |                |                |              |
   +----------------+----------------+----------------+--------------+
   | 1.2.840.1      |                |                |              |
   | 0008.6.​1.​166 |                |                |              |
   +----------------+----------------+----------------+--------------+
   | 1.2.840.1      |                |                |              |
   | 0008.6.​1.​167 |                |                |              |
   +----------------+----------------+----------------+--------------+
   | 1.2.840.1      |                |                |              |
   | 0008.6.​1.​168 |                |                |              |
   +----------------+----------------+----------------+--------------+
   | 1.2.840.1      |                |                |              |
   | 0008.6.​1.​169 |                |                |              |
   +----------------+----------------+----------------+--------------+
   | 1.2.840.1      |                |                |              |
   | 0008.6.​1.​170 |                |                |              |
   +----------------+----------------+----------------+--------------+
   | 1.2.840.1      |                |                |              |
   | 0008.6.​1.​171 |                |                |              |
   +----------------+----------------+----------------+--------------+
   | 1.2.840.1      |                |                |              |
   | 0008.6.​1.​172 |                |                |              |
   +----------------+----------------+----------------+--------------+
   | 1.2.840.1      |                |                |              |
   | 0008.6.​1.​173 |                |                |              |
   +----------------+----------------+----------------+--------------+
   | 1.2.840.1      |                |                |              |
   | 0008.6.​1.​174 |                |                |              |
   +----------------+----------------+----------------+--------------+
   | 1.2.840.1      |                |                |              |
   | 0008.6.​1.​175 |                |                |              |
   +----------------+----------------+----------------+--------------+
   | 1.2.840.1      |                |                |              |
   | 0008.6.​1.​176 |                |                |              |
   +----------------+----------------+----------------+--------------+
   | 1.2.840.1      |                |                |              |
   | 0008.6.​1.​177 |                |                |              |
   +----------------+----------------+----------------+--------------+
   | 1.2.840.1      |                |                |              |
   | 0008.6.​1.​178 |                |                |              |
   +----------------+----------------+----------------+--------------+
   | 1.2.840.1      |                |                |              |
   | 0008.6.​1.​179 |                |                |              |
   +----------------+----------------+----------------+--------------+
   | 1.2.840.1      |                |                |              |
   | 0008.6.​1.​180 |                |                |              |
   +----------------+----------------+----------------+--------------+
   | 1.2.840.1      |                |                |              |
   | 0008.6.​1.​181 |                |                |              |
   +----------------+----------------+----------------+--------------+
   | 1.2.840.1      |                |                |              |
   | 0008.6.​1.​182 |                |                |              |
   +----------------+----------------+----------------+--------------+
   | 1.2.840.1      |                |                |              |
   | 0008.6.​1.​183 |                |                |              |
   +----------------+----------------+----------------+--------------+
   | 1.2.840.1      |                |                |              |
   | 0008.6.​1.​184 |                |                |              |
   +----------------+----------------+----------------+--------------+
   | 1.2.840.1      |                |                |              |
   | 0008.6.​1.​185 |                |                |              |
   +----------------+----------------+----------------+--------------+
   | 1.2.840.1      |                |                |              |
   | 0008.6.​1.​186 |                |                |              |
   +----------------+----------------+----------------+--------------+
   | 1.2.840.1      |                |                |              |
   | 0008.6.​1.​187 |                |                |              |
   +----------------+----------------+----------------+--------------+
   | 1.2.840.1      |                |                | *RET (2013)* |
   | 0008.6.​1.​188 |                |                |              |
   +----------------+----------------+----------------+--------------+
   | 1.2.840.1      |                |                | *RET (2013)* |
   | 0008.6.​1.​189 |                |                |              |
   +----------------+----------------+----------------+--------------+
   | 1.2.840.1      |                |                |              |
   | 0008.6.​1.​190 |                |                |              |
   +----------------+----------------+----------------+--------------+
   | 1.2.840.1      |                |                |              |
   | 0008.6.​1.​191 |                |                |              |
   +----------------+----------------+----------------+--------------+
   | 1.2.840.1      |                |                |              |
   | 0008.6.​1.​192 |                |                |              |
   +----------------+----------------+----------------+--------------+
   | *1.2.840.10    |                |                | *RET (2013)* |
   | 008.6.​1.​193* |                |                |              |
   +----------------+----------------+----------------+--------------+
   | 1.2.840.1      |                |                |              |
   | 0008.6.​1.​194 |                |                |              |
   +----------------+----------------+----------------+--------------+
   | *1.2.840.10    |                |                |              |
   | 008.6.​1.​195* |                |                |              |
   +----------------+----------------+----------------+--------------+
   | *1.2.840.10    |                |                | *RET (2013)* |
   | 008.6.​1.​196* |                |                |              |
   +----------------+----------------+----------------+--------------+
   | *1.2.840.10    |                |                | *RET (2013)* |
   | 008.6.​1.​197* |                |                |              |
   +----------------+----------------+----------------+--------------+
   | *1.2.840.10    |                |                | *RET (2013)* |
   | 008.6.​1.​198* |                |                |              |
   +----------------+----------------+----------------+--------------+
   | *1.2.840.10    |                |                | *RET (2013)* |
   | 008.6.​1.​199* |                |                |              |
   +----------------+----------------+----------------+--------------+
   | *1.2.840.10    |                |                | *RET (2013)* |
   | 008.6.​1.​200* |                |                |              |
   +----------------+----------------+----------------+--------------+
   | 1.2.840.1      |                |                |              |
   | 0008.6.​1.​201 |                |                |              |
   +----------------+----------------+----------------+--------------+
   | 1.2.840.1      |                |                |              |
   | 0008.6.​1.​202 |                |                |              |
   +----------------+----------------+----------------+--------------+
   | 1.2.840.1      |                |                |              |
   | 0008.6.​1.​203 |                |                |              |
   +----------------+----------------+----------------+--------------+
   | 1.2.840.1      |                |                |              |
   | 0008.6.​1.​204 |                |                |              |
   +----------------+----------------+----------------+--------------+
   | 1.2.840.1      |                |                |              |
   | 0008.6.​1.​205 |                |                |              |
   +----------------+----------------+----------------+--------------+
   | 1.2.840.1      |                |                |              |
   | 0008.6.​1.​206 |                |                |              |
   +----------------+----------------+----------------+--------------+
   | 1.2.840.1      |                |                |              |
   | 0008.6.​1.​207 |                |                |              |
   +----------------+----------------+----------------+--------------+
   | 1.2.840.1      |                |                |              |
   | 0008.6.​1.​208 |                |                |              |
   +----------------+----------------+----------------+--------------+
   | 1.2.840.1      |                |                |              |
   | 0008.6.​1.​209 |                |                |              |
   +----------------+----------------+----------------+--------------+
   | 1.2.840.1      |                |                |              |
   | 0008.6.​1.​210 |                |                |              |
   +----------------+----------------+----------------+--------------+
   | 1.2.840.1      |                |                |              |
   | 0008.6.​1.​211 |                |                |              |
   +----------------+----------------+----------------+--------------+
   | 1.2.840.1      |                |                |              |
   | 0008.6.​1.​212 |                |                |              |
   +----------------+----------------+----------------+--------------+
   | 1.2.840.1      |                |                |              |
   | 0008.6.​1.​213 |                |                |              |
   +----------------+----------------+----------------+--------------+
   | 1.2.840.1      |                |                |              |
   | 0008.6.​1.​214 |                |                |              |
   +----------------+----------------+----------------+--------------+
   | 1.2.840.1      |                |                |              |
   | 0008.6.​1.​215 |                |                |              |
   +----------------+----------------+----------------+--------------+
   | 1.2.840.1      |                |                |              |
   | 0008.6.​1.​216 |                |                |              |
   +----------------+----------------+----------------+--------------+
   | 1.2.840.1      |                |                |              |
   | 0008.6.​1.​217 |                |                |              |
   +----------------+----------------+----------------+--------------+
   | 1.2.840.1      |                |                |              |
   | 0008.6.​1.​218 |                |                |              |
   +----------------+----------------+----------------+--------------+
   | 1.2.840.1      |                |                |              |
   | 0008.6.​1.​219 |                |                |              |
   +----------------+----------------+----------------+--------------+
   | 1.2.840.1      |                |                |              |
   | 0008.6.​1.​220 |                |                |              |
   +----------------+----------------+----------------+--------------+
   | *1.2.840.10    |                |                | *RET (2007)* |
   | 008.6.​1.​221* |                |                |              |
   +----------------+----------------+----------------+--------------+
   | 1.2.840.1      |                |                |              |
   | 0008.6.​1.​222 |                |                |              |
   +----------------+----------------+----------------+--------------+
   | 1.2.840.1      |                |                |              |
   | 0008.6.​1.​223 |                |                |              |
   +----------------+----------------+----------------+--------------+
   | 1.2.840.1      |                |                |              |
   | 0008.6.​1.​224 |                |                |              |
   +----------------+----------------+----------------+--------------+
   | 1.2.840.1      |                |                |              |
   | 0008.6.​1.​225 |                |                |              |
   +----------------+----------------+----------------+--------------+
   | 1.2.840.1      |                |                |              |
   | 0008.6.​1.​226 |                |                |              |
   +----------------+----------------+----------------+--------------+
   | 1.2.840.1      |                |                |              |
   | 0008.6.​1.​227 |                |                |              |
   +----------------+----------------+----------------+--------------+
   | 1.2.840.1      |                |                |              |
   | 0008.6.​1.​228 |                |                |              |
   +----------------+----------------+----------------+--------------+
   | 1.2.840.1      |                |                |              |
   | 0008.6.​1.​229 |                |                |              |
   +----------------+----------------+----------------+--------------+
   | 1.2.840.1      |                |                |              |
   | 0008.6.​1.​230 |                |                |              |
   +----------------+----------------+----------------+--------------+
   | 1.2.840.1      |                |                |              |
   | 0008.6.​1.​231 |                |                |              |
   +----------------+----------------+----------------+--------------+
   | 1.2.840.1      |                |                |              |
   | 0008.6.​1.​232 |                |                |              |
   +----------------+----------------+----------------+--------------+
   | 1.2.840.1      |                |                |              |
   | 0008.6.​1.​233 |                |                |              |
   +----------------+----------------+----------------+--------------+
   | 1.2.840.1      |                |                |              |
   | 0008.6.​1.​234 |                |                |              |
   +----------------+----------------+----------------+--------------+
   | 1.2.840.1      |                |                |              |
   | 0008.6.​1.​235 |                |                |              |
   +----------------+----------------+----------------+--------------+
   | 1.2.840.1      |                |                |              |
   | 0008.6.​1.​236 |                |                |              |
   +----------------+----------------+----------------+--------------+
   | 1.2.840.1      |                |                |              |
   | 0008.6.​1.​237 |                |                |              |
   +----------------+----------------+----------------+--------------+
   | 1.2.840.1      |                |                |              |
   | 0008.6.​1.​238 |                |                |              |
   +----------------+----------------+----------------+--------------+
   | 1.2.840.1      |                |                |              |
   | 0008.6.​1.​239 |                |                |              |
   +----------------+----------------+----------------+--------------+
   | 1.2.840.1      |                |                |              |
   | 0008.6.​1.​240 |                |                |              |
   +----------------+----------------+----------------+--------------+
   | 1.2.840.1      |                |                |              |
   | 0008.6.​1.​241 |                |                |              |
   +----------------+----------------+----------------+--------------+
   | 1.2.840.1      |                |                |              |
   | 0008.6.​1.​242 |                |                |              |
   +----------------+----------------+----------------+--------------+
   | 1.2.840.1      |                |                |              |
   | 0008.6.​1.​243 |                |                |              |
   +----------------+----------------+----------------+--------------+
   | 1.2.840.1      |                |                |              |
   | 0008.6.​1.​244 |                |                |              |
   +----------------+----------------+----------------+--------------+
   | 1.2.840.1      |                |                |              |
   | 0008.6.​1.​245 |                |                |              |
   +----------------+----------------+----------------+--------------+
   | 1.2.840.1      |                |                |              |
   | 0008.6.​1.​246 |                |                |              |
   +----------------+----------------+----------------+--------------+
   | 1.2.840.1      |                |                |              |
   | 0008.6.​1.​247 |                |                |              |
   +----------------+----------------+----------------+--------------+
   | 1.2.840.1      |                |                |              |
   | 0008.6.​1.​248 |                |                |              |
   +----------------+----------------+----------------+--------------+
   | 1.2.840.1      |                |                |              |
   | 0008.6.​1.​249 |                |                |              |
   +----------------+----------------+----------------+--------------+
   | 1.2.840.1      |                |                |              |
   | 0008.6.​1.​250 |                |                |              |
   +----------------+----------------+----------------+--------------+
   | 1.2.840.1      |                |                |              |
   | 0008.6.​1.​251 |                |                |              |
   +----------------+----------------+----------------+--------------+
   | 1.2.840.1      |                |                |              |
   | 0008.6.​1.​252 |                |                |              |
   +----------------+----------------+----------------+--------------+
   | 1.2.840.1      |                |                |              |
   | 0008.6.​1.​253 |                |                |              |
   +----------------+----------------+----------------+--------------+
   | 1.2.840.1      |                |                |              |
   | 0008.6.​1.​254 |                |                |              |
   +----------------+----------------+----------------+--------------+
   | 1.2.840.1      |                |                |              |
   | 0008.6.​1.​255 |                |                |              |
   +----------------+----------------+----------------+--------------+
   | 1.2.840.1      |                |                |              |
   | 0008.6.​1.​256 |                |                |              |
   +----------------+----------------+----------------+--------------+
   | 1.2.840.1      |                |                |              |
   | 0008.6.​1.​257 |                |                |              |
   +----------------+----------------+----------------+--------------+
   | 1.2.840.1      |                |                |              |
   | 0008.6.​1.​258 |                |                |              |
   +----------------+----------------+----------------+--------------+
   | 1.2.840.1      |                |                |              |
   | 0008.6.​1.​259 |                |                |              |
   +----------------+----------------+----------------+--------------+
   | 1.2.840.1      |                |                |              |
   | 0008.6.​1.​260 |                |                |              |
   +----------------+----------------+----------------+--------------+
   | 1.2.840.1      |                |                |              |
   | 0008.6.​1.​261 |                |                |              |
   +----------------+----------------+----------------+--------------+
   | 1.2.840.1      |                |                |              |
   | 0008.6.​1.​262 |                |                |              |
   +----------------+----------------+----------------+--------------+
   | 1.2.840.1      |                |                |              |
   | 0008.6.​1.​263 |                |                |              |
   +----------------+----------------+----------------+--------------+
   | 1.2.840.1      |                |                |              |
   | 0008.6.​1.​264 |                |                |              |
   +----------------+----------------+----------------+--------------+
   | 1.2.840.1      |                |                |              |
   | 0008.6.​1.​265 |                |                |              |
   +----------------+----------------+----------------+--------------+
   | 1.2.840.1      |                |                |              |
   | 0008.6.​1.​266 |                |                |              |
   +----------------+----------------+----------------+--------------+
   | 1.2.840.1      |                |                |              |
   | 0008.6.​1.​267 |                |                |              |
   +----------------+----------------+----------------+--------------+
   | 1.2.840.1      |                |                |              |
   | 0008.6.​1.​268 |                |                |              |
   +----------------+----------------+----------------+--------------+
   | 1.2.840.1      |                |                |              |
   | 0008.6.​1.​269 |                |                |              |
   +----------------+----------------+----------------+--------------+
   | 1.2.840.1      |                |                |              |
   | 0008.6.​1.​270 |                |                |              |
   +----------------+----------------+----------------+--------------+
   | 1.2.840.1      |                |                |              |
   | 0008.6.​1.​271 |                |                |              |
   +----------------+----------------+----------------+--------------+
   | 1.2.840.1      |                |                |              |
   | 0008.6.​1.​272 |                |                |              |
   +----------------+----------------+----------------+--------------+
   | 1.2.840.1      |                |                |              |
   | 0008.6.​1.​273 |                |                |              |
   +----------------+----------------+----------------+--------------+
   | 1.2.840.1      |                |                |              |
   | 0008.6.​1.​274 |                |                |              |
   +----------------+----------------+----------------+--------------+
   | 1.2.840.1      |                |                |              |
   | 0008.6.​1.​275 |                |                |              |
   +----------------+----------------+----------------+--------------+
   | 1.2.840.1      |                |                |              |
   | 0008.6.​1.​276 |                |                |              |
   +----------------+----------------+----------------+--------------+
   | 1.2.840.1      |                |                |              |
   | 0008.6.​1.​277 |                |                |              |
   +----------------+----------------+----------------+--------------+
   | 1.2.840.1      |                |                |              |
   | 0008.6.​1.​278 |                |                |              |
   +----------------+----------------+----------------+--------------+
   | 1.2.840.1      |                |                |              |
   | 0008.6.​1.​279 |                |                |              |
   +----------------+----------------+----------------+--------------+
   | 1.2.840.1      |                |                |              |
   | 0008.6.​1.​280 |                |                |              |
   +----------------+----------------+----------------+--------------+
   | 1.2.840.1      |                |                |              |
   | 0008.6.​1.​281 |                |                |              |
   +----------------+----------------+----------------+--------------+
   | 1.2.840.1      |                |                |              |
   | 0008.6.​1.​282 |                |                |              |
   +----------------+----------------+----------------+--------------+
   | 1.2.840.1      |                |                |              |
   | 0008.6.​1.​283 |                |                |              |
   +----------------+----------------+----------------+--------------+
   | 1.2.840.1      |                |                |              |
   | 0008.6.​1.​284 |                |                |              |
   +----------------+----------------+----------------+--------------+
   | 1.2.840.1      |                |                |              |
   | 0008.6.​1.​285 |                |                |              |
   +----------------+----------------+----------------+--------------+
   | 1.2.840.1      |                |                |              |
   | 0008.6.​1.​286 |                |                |              |
   +----------------+----------------+----------------+--------------+
   | 1.2.840.1      |                |                |              |
   | 0008.6.​1.​287 |                |                |              |
   +----------------+----------------+----------------+--------------+
   | 1.2.840.1      |                |                |              |
   | 0008.6.​1.​288 |                |                |              |
   +----------------+----------------+----------------+--------------+
   | 1.2.840.1      |                |                |              |
   | 0008.6.​1.​289 |                |                |              |
   +----------------+----------------+----------------+--------------+
   | 1.2.840.1      |                |                |              |
   | 0008.6.​1.​290 |                |                |              |
   +----------------+----------------+----------------+--------------+
   | 1.2.840.1      |                |                |              |
   | 0008.6.​1.​291 |                |                |              |
   +----------------+----------------+----------------+--------------+
   | 1.2.840.1      |                |                |              |
   | 0008.6.​1.​292 |                |                |              |
   +----------------+----------------+----------------+--------------+
   | 1.2.840.1      |                |                |              |
   | 0008.6.​1.​293 |                |                |              |
   +----------------+----------------+----------------+--------------+
   | 1.2.840.1      |                |                |              |
   | 0008.6.​1.​294 |                |                |              |
   +----------------+----------------+----------------+--------------+
   | 1.2.840.1      |                |                |              |
   | 0008.6.​1.​295 |                |                |              |
   +----------------+----------------+----------------+--------------+
   | 1.2.840.1      |                |                |              |
   | 0008.6.​1.​296 |                |                |              |
   +----------------+----------------+----------------+--------------+
   | 1.2.840.1      |                |                |              |
   | 0008.6.​1.​297 |                |                |              |
   +----------------+----------------+----------------+--------------+
   | 1.2.840.1      |                |                |              |
   | 0008.6.​1.​298 |                |                |              |
   +----------------+----------------+----------------+--------------+
   | 1.2.840.1      |                |                |              |
   | 0008.6.​1.​299 |                |                |              |
   +----------------+----------------+----------------+--------------+
   | 1.2.840.1      |                |                |              |
   | 0008.6.​1.​300 |                |                |              |
   +----------------+----------------+----------------+--------------+
   | 1.2.840.1      |                |                |              |
   | 0008.6.​1.​301 |                |                |              |
   +----------------+----------------+----------------+--------------+
   | 1.2.840.1      |                |                |              |
   | 0008.6.​1.​302 |                |                |              |
   +----------------+----------------+----------------+--------------+
   | 1.2.840.1      |                |                |              |
   | 0008.6.​1.​303 |                |                |              |
   +----------------+----------------+----------------+--------------+
   | 1.2.840.1      |                |                |              |
   | 0008.6.​1.​304 |                |                |              |
   +----------------+----------------+----------------+--------------+
   | 1.2.840.1      |                |                |              |
   | 0008.6.​1.​305 |                |                |              |
   +----------------+----------------+----------------+--------------+
   | 1.2.840.1      |                |                |              |
   | 0008.6.​1.​306 |                |                |              |
   +----------------+----------------+----------------+--------------+
   | 1.2.840.1      |                |                |              |
   | 0008.6.​1.​307 |                |                |              |
   +----------------+----------------+----------------+--------------+
   | 1.2.840.1      |                |                |              |
   | 0008.6.​1.​308 |                |                |              |
   +----------------+----------------+----------------+--------------+
   | 1.2.840.1      |                |                |              |
   | 0008.6.​1.​309 |                |                |              |
   +----------------+----------------+----------------+--------------+
   | 1.2.840.1      |                |                |              |
   | 0008.6.​1.​310 |                |                |              |
   +----------------+----------------+----------------+--------------+
   | 1.2.840.1      |                |                |              |
   | 0008.6.​1.​311 |                |                |              |
   +----------------+----------------+----------------+--------------+
   | 1.2.840.1      |                |                |              |
   | 0008.6.​1.​312 |                |                |              |
   +----------------+----------------+----------------+--------------+
   | 1.2.840.1      |                |                |              |
   | 0008.6.​1.​313 |                |                |              |
   +----------------+----------------+----------------+--------------+
   | 1.2.840.1      |                |                |              |
   | 0008.6.​1.​314 |                |                |              |
   +----------------+----------------+----------------+--------------+
   | 1.2.840.1      |                |                |              |
   | 0008.6.​1.​315 |                |                |              |
   +----------------+----------------+----------------+--------------+
   | 1.2.840.1      |                |                |              |
   | 0008.6.​1.​316 |                |                |              |
   +----------------+----------------+----------------+--------------+
   | 1.2.840.1      |                |                |              |
   | 0008.6.​1.​317 |                |                |              |
   +----------------+----------------+----------------+--------------+
   | 1.2.840.1      |                |                |              |
   | 0008.6.​1.​318 |                |                |              |
   +----------------+----------------+----------------+--------------+
   | 1.2.840.1      |                |                |              |
   | 0008.6.​1.​319 |                |                |              |
   +----------------+----------------+----------------+--------------+
   | 1.2.840.1      |                |                |              |
   | 0008.6.​1.​320 |                |                |              |
   +----------------+----------------+----------------+--------------+
   | 1.2.840.1      |                |                |              |
   | 0008.6.​1.​321 |                |                |              |
   +----------------+----------------+----------------+--------------+
   | 1.2.840.1      |                |                |              |
   | 0008.6.​1.​322 |                |                |              |
   +----------------+----------------+----------------+--------------+
   | 1.2.840.1      |                |                |              |
   | 0008.6.​1.​323 |                |                |              |
   +----------------+----------------+----------------+--------------+
   | 1.2.840.1      |                |                |              |
   | 0008.6.​1.​324 |                |                |              |
   +----------------+----------------+----------------+--------------+
   | 1.2.840.1      |                |                |              |
   | 0008.6.​1.​325 |                |                |              |
   +----------------+----------------+----------------+--------------+
   | 1.2.840.1      |                |                |              |
   | 0008.6.​1.​326 |                |                |              |
   +----------------+----------------+----------------+--------------+
   | 1.2.840.1      |                |                |              |
   | 0008.6.​1.​327 |                |                |              |
   +----------------+----------------+----------------+--------------+
   | 1.2.840.1      |                |                |              |
   | 0008.6.​1.​328 |                |                |              |
   +----------------+----------------+----------------+--------------+
   | 1.2.840.1      |                |                |              |
   | 0008.6.​1.​329 |                |                |              |
   +----------------+----------------+----------------+--------------+
   | 1.2.840.1      |                |                |              |
   | 0008.6.​1.​330 |                |                |              |
   +----------------+----------------+----------------+--------------+
   | 1.2.840.1      |                |                |              |
   | 0008.6.​1.​331 |                |                |              |
   +----------------+----------------+----------------+--------------+
   | 1.2.840.1      |                |                |              |
   | 0008.6.​1.​332 |                |                |              |
   +----------------+----------------+----------------+--------------+
   | 1.2.840.1      |                |                |              |
   | 0008.6.​1.​333 |                |                |              |
   +----------------+----------------+----------------+--------------+
   | 1.2.840.1      |                |                |              |
   | 0008.6.​1.​334 |                |                |              |
   +----------------+----------------+----------------+--------------+
   | 1.2.840.1      |                |                |              |
   | 0008.6.​1.​335 |                |                |              |
   +----------------+----------------+----------------+--------------+
   | 1.2.840.1      |                |                |              |
   | 0008.6.​1.​336 |                |                |              |
   +----------------+----------------+----------------+--------------+
   | 1.2.840.1      |                |                |              |
   | 0008.6.​1.​337 |                |                |              |
   +----------------+----------------+----------------+--------------+
   | 1.2.840.1      |                |                |              |
   | 0008.6.​1.​338 |                |                |              |
   +----------------+----------------+----------------+--------------+
   | 1.2.840.1      |                |                |              |
   | 0008.6.​1.​339 |                |                |              |
   +----------------+----------------+----------------+--------------+
   | 1.2.840.1      |                |                |              |
   | 0008.6.​1.​340 |                |                |              |
   +----------------+----------------+----------------+--------------+
   | 1.2.840.1      |                |                |              |
   | 0008.6.​1.​341 |                |                |              |
   +----------------+----------------+----------------+--------------+
   | 1.2.840.1      |                |                |              |
   | 0008.6.​1.​342 |                |                |              |
   +----------------+----------------+----------------+--------------+
   | 1.2.840.1      |                |                |              |
   | 0008.6.​1.​343 |                |                |              |
   +----------------+----------------+----------------+--------------+
   | 1.2.840.1      |                |                |              |
   | 0008.6.​1.​344 |                |                |              |
   +----------------+----------------+----------------+--------------+
   | 1.2.840.1      |                |                |              |
   | 0008.6.​1.​345 |                |                |              |
   +----------------+----------------+----------------+--------------+
   | 1.2.840.1      |                |                |              |
   | 0008.6.​1.​346 |                |                |              |
   +----------------+----------------+----------------+--------------+
   | 1.2.840.1      |                |                |              |
   | 0008.6.​1.​347 |                |                |              |
   +----------------+----------------+----------------+--------------+
   | 1.2.840.1      |                |                |              |
   | 0008.6.​1.​348 |                |                |              |
   +----------------+----------------+----------------+--------------+
   | 1.2.840.1      |                |                |              |
   | 0008.6.​1.​349 |                |                |              |
   +----------------+----------------+----------------+--------------+
   | 1.2.840.1      |                |                |              |
   | 0008.6.​1.​350 |                |                |              |
   +----------------+----------------+----------------+--------------+
   | 1.2.840.1      |                |                |              |
   | 0008.6.​1.​351 |                |                |              |
   +----------------+----------------+----------------+--------------+
   | 1.2.840.1      |                |                |              |
   | 0008.6.​1.​352 |                |                |              |
   +----------------+----------------+----------------+--------------+
   | 1.2.840.1      |                |                |              |
   | 0008.6.​1.​353 |                |                |              |
   +----------------+----------------+----------------+--------------+
   | 1.2.840.1      |                |                |              |
   | 0008.6.​1.​354 |                |                |              |
   +----------------+----------------+----------------+--------------+
   | 1.2.840.1      |                |                |              |
   | 0008.6.​1.​355 |                |                |              |
   +----------------+----------------+----------------+--------------+
   | 1.2.840.1      |                |                |              |
   | 0008.6.​1.​356 |                |                |              |
   +----------------+----------------+----------------+--------------+
   | 1.2.840.1      |                |                |              |
   | 0008.6.​1.​357 |                |                |              |
   +----------------+----------------+----------------+--------------+
   | 1.2.840.1      |                |                |              |
   | 0008.6.​1.​358 |                |                |              |
   +----------------+----------------+----------------+--------------+
   | 1.2.840.1      |                |                |              |
   | 0008.6.​1.​359 |                |                |              |
   +----------------+----------------+----------------+--------------+
   | 1.2.840.1      |                |                |              |
   | 0008.6.​1.​360 |                |                |              |
   +----------------+----------------+----------------+--------------+
   | 1.2.840.1      |                |                |              |
   | 0008.6.​1.​361 |                |                |              |
   +----------------+----------------+----------------+--------------+
   | 1.2.840.1      |                |                |              |
   | 0008.6.​1.​362 |                |                |              |
   +----------------+----------------+----------------+--------------+
   | 1.2.840.1      |                |                |              |
   | 0008.6.​1.​363 |                |                |              |
   +----------------+----------------+----------------+--------------+
   | 1.2.840.1      |                |                |              |
   | 0008.6.​1.​364 |                |                |              |
   +----------------+----------------+----------------+--------------+
   | 1.2.840.1      |                |                |              |
   | 0008.6.​1.​365 |                |                |              |
   +----------------+----------------+----------------+--------------+
   | 1.2.840.1      |                |                |              |
   | 0008.6.​1.​366 |                |                |              |
   +----------------+----------------+----------------+--------------+
   | 1.2.840.1      |                |                |              |
   | 0008.6.​1.​367 |                |                |              |
   +----------------+----------------+----------------+--------------+
   | 1.2.840.1      |                |                |              |
   | 0008.6.​1.​368 |                |                |              |
   +----------------+----------------+----------------+--------------+
   | 1.2.840.1      |                |                |              |
   | 0008.6.​1.​369 |                |                |              |
   +----------------+----------------+----------------+--------------+
   | 1.2.840.1      |                |                |              |
   | 0008.6.​1.​370 |                |                |              |
   +----------------+----------------+----------------+--------------+
   | 1.2.840.1      |                |                |              |
   | 0008.6.​1.​371 |                |                |              |
   +----------------+----------------+----------------+--------------+
   | 1.2.840.1      |                |                |              |
   | 0008.6.​1.​372 |                |                |              |
   +----------------+----------------+----------------+--------------+
   | 1.2.840.1      |                |                |              |
   | 0008.6.​1.​373 |                |                |              |
   +----------------+----------------+----------------+--------------+
   | 1.2.840.1      |                |                |              |
   | 0008.6.​1.​374 |                |                |              |
   +----------------+----------------+----------------+--------------+
   | 1.2.840.1      |                |                |              |
   | 0008.6.​1.​375 |                |                |              |
   +----------------+----------------+----------------+--------------+
   | 1.2.840.1      |                |                |              |
   | 0008.6.​1.​376 |                |                |              |
   +----------------+----------------+----------------+--------------+
   | 1.2.840.1      |                |                |              |
   | 0008.6.​1.​377 |                |                |              |
   +----------------+----------------+----------------+--------------+
   | 1.2.840.1      |                |                |              |
   | 0008.6.​1.​378 |                |                |              |
   +----------------+----------------+----------------+--------------+
   | 1.2.840.1      |                |                |              |
   | 0008.6.​1.​379 |                |                |              |
   +----------------+----------------+----------------+--------------+
   | 1.2.840.1      |                |                |              |
   | 0008.6.​1.​380 |                |                |              |
   +----------------+----------------+----------------+--------------+
   | 1.2.840.1      |                |                |              |
   | 0008.6.​1.​381 |                |                |              |
   +----------------+----------------+----------------+--------------+
   | 1.2.840.1      |                |                |              |
   | 0008.6.​1.​382 |                |                |              |
   +----------------+----------------+----------------+--------------+
   | 1.2.840.1      |                |                |              |
   | 0008.6.​1.​383 |                |                |              |
   +----------------+----------------+----------------+--------------+
   | 1.2.840.1      |                |                |              |
   | 0008.6.​1.​384 |                |                |              |
   +----------------+----------------+----------------+--------------+
   | 1.2.840.1      |                |                |              |
   | 0008.6.​1.​385 |                |                |              |
   +----------------+----------------+----------------+--------------+
   | 1.2.840.1      |                |                |              |
   | 0008.6.​1.​386 |                |                |              |
   +----------------+----------------+----------------+--------------+
   | 1.2.840.1      |                |                |              |
   | 0008.6.​1.​387 |                |                |              |
   +----------------+----------------+----------------+--------------+
   | 1.2.840.1      |                |                |              |
   | 0008.6.​1.​388 |                |                |              |
   +----------------+----------------+----------------+--------------+
   | 1.2.840.1      |                |                |              |
   | 0008.6.​1.​389 |                |                |              |
   +----------------+----------------+----------------+--------------+
   | 1.2.840.1      |                |                |              |
   | 0008.6.​1.​390 |                |                |              |
   +----------------+----------------+----------------+--------------+
   | 1.2.840.1      |                |                |              |
   | 0008.6.​1.​391 |                |                |              |
   +----------------+----------------+----------------+--------------+
   | 1.2.840.1      |                |                |              |
   | 0008.6.​1.​392 |                |                |              |
   +----------------+----------------+----------------+--------------+
   | 1.2.840.1      |                |                |              |
   | 0008.6.​1.​393 |                |                |              |
   +----------------+----------------+----------------+--------------+
   | 1.2.840.1      |                |                |              |
   | 0008.6.​1.​394 |                |                |              |
   +----------------+----------------+----------------+--------------+
   | 1.2.840.1      |                |                |              |
   | 0008.6.​1.​395 |                |                |              |
   +----------------+----------------+----------------+--------------+
   | 1.2.840.1      |                |                |              |
   | 0008.6.​1.​396 |                |                |              |
   +----------------+----------------+----------------+--------------+
   | 1.2.840.1      |                |                |              |
   | 0008.6.​1.​397 |                |                |              |
   +----------------+----------------+----------------+--------------+
   | 1.2.840.1      |                |                |              |
   | 0008.6.​1.​398 |                |                |              |
   +----------------+----------------+----------------+--------------+
   | 1.2.840.1      |                |                |              |
   | 0008.6.​1.​399 |                |                |              |
   +----------------+----------------+----------------+--------------+
   | 1.2.840.1      |                |                |              |
   | 0008.6.​1.​400 |                |                |              |
   +----------------+----------------+----------------+--------------+
   | 1.2.840.1      |                |                |              |
   | 0008.6.​1.​401 |                |                |              |
   +----------------+----------------+----------------+--------------+
   | 1.2.840.1      |                |                |              |
   | 0008.6.​1.​402 |                |                |              |
   +----------------+----------------+----------------+--------------+
   | 1.2.840.1      |                |                |              |
   | 0008.6.​1.​403 |                |                |              |
   +----------------+----------------+----------------+--------------+
   | 1.2.840.1      |                |                |              |
   | 0008.6.​1.​404 |                |                |              |
   +----------------+----------------+----------------+--------------+
   | 1.2.840.1      |                |                |              |
   | 0008.6.​1.​405 |                |                |              |
   +----------------+----------------+----------------+--------------+
   | 1.2.840.1      |                |                |              |
   | 0008.6.​1.​406 |                |                |              |
   +----------------+----------------+----------------+--------------+
   | 1.2.840.1      |                |                |              |
   | 0008.6.​1.​407 |                |                |              |
   +----------------+----------------+----------------+--------------+
   | 1.2.840.1      |                |                |              |
   | 0008.6.​1.​408 |                |                |              |
   +----------------+----------------+----------------+--------------+
   | 1.2.840.1      |                |                |              |
   | 0008.6.​1.​409 |                |                |              |
   +----------------+----------------+----------------+--------------+
   | 1.2.840.1      |                |                |              |
   | 0008.6.​1.​410 |                |                |              |
   +----------------+----------------+----------------+--------------+
   | 1.2.840.1      |                |                |              |
   | 0008.6.​1.​411 |                |                |              |
   +----------------+----------------+----------------+--------------+
   | 1.2.840.1      |                |                |              |
   | 0008.6.​1.​412 |                |                |              |
   +----------------+----------------+----------------+--------------+
   | 1.2.840.1      |                |                |              |
   | 0008.6.​1.​413 |                |                |              |
   +----------------+----------------+----------------+--------------+
   | 1.2.840.1      |                |                |              |
   | 0008.6.​1.​414 |                |                |              |
   +----------------+----------------+----------------+--------------+
   | 1.2.840.1      |                |                |              |
   | 0008.6.​1.​415 |                |                |              |
   +----------------+----------------+----------------+--------------+
   | 1.2.840.1      |                |                |              |
   | 0008.6.​1.​416 |                |                |              |
   +----------------+----------------+----------------+--------------+
   | 1.2.840.1      |                |                |              |
   | 0008.6.​1.​417 |                |                |              |
   +----------------+----------------+----------------+--------------+
   | 1.2.840.1      |                |                |              |
   | 0008.6.​1.​418 |                |                |              |
   +----------------+----------------+----------------+--------------+
   | 1.2.840.1      |                |                |              |
   | 0008.6.​1.​419 |                |                |              |
   +----------------+----------------+----------------+--------------+
   | 1.2.840.1      |                |                |              |
   | 0008.6.​1.​420 |                |                |              |
   +----------------+----------------+----------------+--------------+
   | 1.2.840.1      |                |                |              |
   | 0008.6.​1.​421 |                |                |              |
   +----------------+----------------+----------------+--------------+
   | 1.2.840.1      |                |                |              |
   | 0008.6.​1.​422 |                |                |              |
   +----------------+----------------+----------------+--------------+
   | 1.2.840.1      |                |                |              |
   | 0008.6.​1.​423 |                |                |              |
   +----------------+----------------+----------------+--------------+
   | 1.2.840.1      |                |                |              |
   | 0008.6.​1.​424 |                |                |              |
   +----------------+----------------+----------------+--------------+
   | 1.2.840.1      |                |                |              |
   | 0008.6.​1.​425 |                |                |              |
   +----------------+----------------+----------------+--------------+
   | 1.2.840.1      |                |                |              |
   | 0008.6.​1.​426 |                |                |              |
   +----------------+----------------+----------------+--------------+
   | 1.2.840.1      |                |                |              |
   | 0008.6.​1.​427 |                |                |              |
   +----------------+----------------+----------------+--------------+
   | 1.2.840.1      |                |                |              |
   | 0008.6.​1.​428 |                |                |              |
   +----------------+----------------+----------------+--------------+
   | 1.2.840.1      |                |                |              |
   | 0008.6.​1.​429 |                |                |              |
   +----------------+----------------+----------------+--------------+
   | 1.2.840.1      |                |                |              |
   | 0008.6.​1.​430 |                |                |              |
   +----------------+----------------+----------------+--------------+
   | 1.2.840.1      |                |                |              |
   | 0008.6.​1.​431 |                |                |              |
   +----------------+----------------+----------------+--------------+
   | 1.2.840.1      |                |                |              |
   | 0008.6.​1.​432 |                |                |              |
   +----------------+----------------+----------------+--------------+
   | 1.2.840.1      |                |                |              |
   | 0008.6.​1.​433 |                |                |              |
   +----------------+----------------+----------------+--------------+
   | 1.2.840.1      |                |                |              |
   | 0008.6.​1.​434 |                |                |              |
   +----------------+----------------+----------------+--------------+
   | 1.2.840.1      |                |                |              |
   | 0008.6.​1.​435 |                |                |              |
   +----------------+----------------+----------------+--------------+
   | 1.2.840.1      |                |                |              |
   | 0008.6.​1.​436 |                |                |              |
   +----------------+----------------+----------------+--------------+
   | 1.2.840.1      |                |                |              |
   | 0008.6.​1.​437 |                |                |              |
   +----------------+----------------+----------------+--------------+
   | 1.2.840.1      |                |                |              |
   | 0008.6.​1.​438 |                |                |              |
   +----------------+----------------+----------------+--------------+
   | 1.2.840.1      |                |                |              |
   | 0008.6.​1.​439 |                |                |              |
   +----------------+----------------+----------------+--------------+
   | 1.2.840.1      |                |                |              |
   | 0008.6.​1.​440 |                |                |              |
   +----------------+----------------+----------------+--------------+
   | 1.2.840.1      |                |                |              |
   | 0008.6.​1.​441 |                |                |              |
   +----------------+----------------+----------------+--------------+
   | 1.2.840.1      |                |                |              |
   | 0008.6.​1.​442 |                |                |              |
   +----------------+----------------+----------------+--------------+
   | 1.2.840.1      |                |                |              |
   | 0008.6.​1.​443 |                |                |              |
   +----------------+----------------+----------------+--------------+
   | 1.2.840.1      |                |                |              |
   | 0008.6.​1.​444 |                |                |              |
   +----------------+----------------+----------------+--------------+
   | 1.2.840.1      |                |                |              |
   | 0008.6.​1.​445 |                |                |              |
   +----------------+----------------+----------------+--------------+
   | 1.2.840.1      |                |                |              |
   | 0008.6.​1.​446 |                |                |              |
   +----------------+----------------+----------------+--------------+
   | 1.2.840.1      |                |                |              |
   | 0008.6.​1.​447 |                |                |              |
   +----------------+----------------+----------------+--------------+
   | 1.2.840.1      |                |                |              |
   | 0008.6.​1.​448 |                |                |              |
   +----------------+----------------+----------------+--------------+
   | 1.2.840.1      |                |                |              |
   | 0008.6.​1.​449 |                |                |              |
   +----------------+----------------+----------------+--------------+
   | 1.2.840.1      |                |                |              |
   | 0008.6.​1.​450 |                |                |              |
   +----------------+----------------+----------------+--------------+
   | 1.2.840.1      |                |                |              |
   | 0008.6.​1.​451 |                |                |              |
   +----------------+----------------+----------------+--------------+
   | 1.2.840.1      |                |                |              |
   | 0008.6.​1.​452 |                |                |              |
   +----------------+----------------+----------------+--------------+
   | 1.2.840.1      |                |                |              |
   | 0008.6.​1.​453 |                |                |              |
   +----------------+----------------+----------------+--------------+
   | 1.2.840.1      |                |                |              |
   | 0008.6.​1.​454 |                |                |              |
   +----------------+----------------+----------------+--------------+
   | 1.2.840.1      |                |                |              |
   | 0008.6.​1.​455 |                |                |              |
   +----------------+----------------+----------------+--------------+
   | 1.2.840.1      |                |                |              |
   | 0008.6.​1.​456 |                |                |              |
   +----------------+----------------+----------------+--------------+
   | 1.2.840.1      |                |                |              |
   | 0008.6.​1.​457 |                |                |              |
   +----------------+----------------+----------------+--------------+
   | 1.2.840.1      |                |                |              |
   | 0008.6.​1.​458 |                |                |              |
   +----------------+----------------+----------------+--------------+
   | 1.2.840.1      |                |                |              |
   | 0008.6.​1.​459 |                |                |              |
   +----------------+----------------+----------------+--------------+
   | 1.2.840.1      |                |                |              |
   | 0008.6.​1.​460 |                |                |              |
   +----------------+----------------+----------------+--------------+
   | 1.2.840.1      |                |                |              |
   | 0008.6.​1.​461 |                |                |              |
   +----------------+----------------+----------------+--------------+
   | 1.2.840.1      |                |                |              |
   | 0008.6.​1.​462 |                |                |              |
   +----------------+----------------+----------------+--------------+
   | 1.2.840.1      |                |                |              |
   | 0008.6.​1.​463 |                |                |              |
   +----------------+----------------+----------------+--------------+
   | 1.2.840.1      |                |                |              |
   | 0008.6.​1.​464 |                |                |              |
   +----------------+----------------+----------------+--------------+
   | 1.2.840.1      |                |                |              |
   | 0008.6.​1.​465 |                |                |              |
   +----------------+----------------+----------------+--------------+
   | 1.2.840.1      |                |                |              |
   | 0008.6.​1.​466 |                |                |              |
   +----------------+----------------+----------------+--------------+
   | 1.2.840.1      |                |                |              |
   | 0008.6.​1.​467 |                |                |              |
   +----------------+----------------+----------------+--------------+
   | 1.2.840.1      |                |                |              |
   | 0008.6.​1.​468 |                |                |              |
   +----------------+----------------+----------------+--------------+
   | 1.2.840.1      |                |                |              |
   | 0008.6.​1.​469 |                |                |              |
   +----------------+----------------+----------------+--------------+
   | 1.2.840.1      |                |                |              |
   | 0008.6.​1.​470 |                |                |              |
   +----------------+----------------+----------------+--------------+
   | 1.2.840.1      |                |                |              |
   | 0008.6.​1.​471 |                |                |              |
   +----------------+----------------+----------------+--------------+
   | 1.2.840.1      |                |                |              |
   | 0008.6.​1.​472 |                |                |              |
   +----------------+----------------+----------------+--------------+
   | 1.2.840.1      |                |                |              |
   | 0008.6.​1.​473 |                |                |              |
   +----------------+----------------+----------------+--------------+
   | 1.2.840.1      |                |                |              |
   | 0008.6.​1.​474 |                |                |              |
   +----------------+----------------+----------------+--------------+
   | 1.2.840.1      |                |                |              |
   | 0008.6.​1.​475 |                |                |              |
   +----------------+----------------+----------------+--------------+
   | 1.2.840.1      |                |                |              |
   | 0008.6.​1.​476 |                |                |              |
   +----------------+----------------+----------------+--------------+
   | 1.2.840.1      |                |                |              |
   | 0008.6.​1.​477 |                |                |              |
   +----------------+----------------+----------------+--------------+
   | 1.2.840.1      |                |                |              |
   | 0008.6.​1.​478 |                |                |              |
   +----------------+----------------+----------------+--------------+
   | 1.2.840.1      |                |                |              |
   | 0008.6.​1.​479 |                |                |              |
   +----------------+----------------+----------------+--------------+
   | 1.2.840.1      |                |                |              |
   | 0008.6.​1.​480 |                |                |              |
   +----------------+----------------+----------------+--------------+
   | 1.2.840.1      |                |                |              |
   | 0008.6.​1.​481 |                |                |              |
   +----------------+----------------+----------------+--------------+
   | 1.2.840.1      |                |                |              |
   | 0008.6.​1.​482 |                |                |              |
   +----------------+----------------+----------------+--------------+
   | 1.2.840.1      |                |                |              |
   | 0008.6.​1.​483 |                |                |              |
   +----------------+----------------+----------------+--------------+
   | 1.2.840.1      |                |                |              |
   | 0008.6.​1.​484 |                |                |              |
   +----------------+----------------+----------------+--------------+
   | 1.2.840.1      |                |                |              |
   | 0008.6.​1.​485 |                |                |              |
   +----------------+----------------+----------------+--------------+
   | 1.2.840.1      |                |                |              |
   | 0008.6.​1.​486 |                |                |              |
   +----------------+----------------+----------------+--------------+
   | 1.2.840.1      |                |                |              |
   | 0008.6.​1.​487 |                |                |              |
   +----------------+----------------+----------------+--------------+
   | 1.2.840.1      |                |                |              |
   | 0008.6.​1.​488 |                |                |              |
   +----------------+----------------+----------------+--------------+
   | 1.2.840.1      |                |                |              |
   | 0008.6.​1.​489 |                |                |              |
   +----------------+----------------+----------------+--------------+
   | 1.2.840.1      |                |                |              |
   | 0008.6.​1.​490 |                |                |              |
   +----------------+----------------+----------------+--------------+
   | 1.2.840.1      |                |                |              |
   | 0008.6.​1.​491 |                |                |              |
   +----------------+----------------+----------------+--------------+
   | 1.2.840.1      |                |                |              |
   | 0008.6.​1.​492 |                |                |              |
   +----------------+----------------+----------------+--------------+
   | 1.2.840.1      |                |                |              |
   | 0008.6.​1.​493 |                |                |              |
   +----------------+----------------+----------------+--------------+
   | 1.2.840.1      |                |                |              |
   | 0008.6.​1.​494 |                |                |              |
   +----------------+----------------+----------------+--------------+
   | 1.2.840.1      |                |                |              |
   | 0008.6.​1.​495 |                |                |              |
   +----------------+----------------+----------------+--------------+
   | 1.2.840.1      |                |                |              |
   | 0008.6.​1.​496 |                |                |              |
   +----------------+----------------+----------------+--------------+
   | 1.2.840.1      |                |                |              |
   | 0008.6.​1.​497 |                |                |              |
   +----------------+----------------+----------------+--------------+
   | 1.2.840.1      |                |                |              |
   | 0008.6.​1.​498 |                |                |              |
   +----------------+----------------+----------------+--------------+
   | 1.2.840.1      |                |                |              |
   | 0008.6.​1.​499 |                |                |              |
   +----------------+----------------+----------------+--------------+
   | 1.2.840.1      |                |                |              |
   | 0008.6.​1.​500 |                |                |              |
   +----------------+----------------+----------------+--------------+
   | 1.2.840.1      |                |                |              |
   | 0008.6.​1.​501 |                |                |              |
   +----------------+----------------+----------------+--------------+
   | 1.2.840.1      |                |                |              |
   | 0008.6.​1.​502 |                |                |              |
   +----------------+----------------+----------------+--------------+
   | 1.2.840.1      |                |                |              |
   | 0008.6.​1.​503 |                |                |              |
   +----------------+----------------+----------------+--------------+
   | 1.2.840.1      |                |                |              |
   | 0008.6.​1.​504 |                |                |              |
   +----------------+----------------+----------------+--------------+
   | 1.2.840.1      |                |                |              |
   | 0008.6.​1.​505 |                |                |              |
   +----------------+----------------+----------------+--------------+
   | 1.2.840.1      |                |                |              |
   | 0008.6.​1.​506 |                |                |              |
   +----------------+----------------+----------------+--------------+
   | 1.2.840.1      |                |                |              |
   | 0008.6.​1.​507 |                |                |              |
   +----------------+----------------+----------------+--------------+
   | 1.2.840.1      |                |                |              |
   | 0008.6.​1.​508 |                |                |              |
   +----------------+----------------+----------------+--------------+
   | 1.2.840.1      |                |                |              |
   | 0008.6.​1.​509 |                |                |              |
   +----------------+----------------+----------------+--------------+
   | 1.2.840.1      |                |                |              |
   | 0008.6.​1.​510 |                |                |              |
   +----------------+----------------+----------------+--------------+
   | 1.2.840.1      |                |                |              |
   | 0008.6.​1.​511 |                |                |              |
   +----------------+----------------+----------------+--------------+
   | 1.2.840.1      |                |                |              |
   | 0008.6.​1.​512 |                |                |              |
   +----------------+----------------+----------------+--------------+
   | 1.2.840.1      |                |                |              |
   | 0008.6.​1.​513 |                |                |              |
   +----------------+----------------+----------------+--------------+
   | 1.2.840.1      |                |                |              |
   | 0008.6.​1.​514 |                |                |              |
   +----------------+----------------+----------------+--------------+
   | 1.2.840.1      |                |                |              |
   | 0008.6.​1.​515 |                |                |              |
   +----------------+----------------+----------------+--------------+
   | 1.2.840.1      |                |                |              |
   | 0008.6.​1.​516 |                |                |              |
   +----------------+----------------+----------------+--------------+
   | 1.2.840.1      |                |                |              |
   | 0008.6.​1.​517 |                |                |              |
   +----------------+----------------+----------------+--------------+
   | 1.2.840.1      |                |                |              |
   | 0008.6.​1.​518 |                |                |              |
   +----------------+----------------+----------------+--------------+
   | 1.2.840.1      |                |                |              |
   | 0008.6.​1.​519 |                |                |              |
   +----------------+----------------+----------------+--------------+
   | 1.2.840.1      |                |                |              |
   | 0008.6.​1.​520 |                |                |              |
   +----------------+----------------+----------------+--------------+
   | 1.2.840.1      |                |                |              |
   | 0008.6.​1.​521 |                |                |              |
   +----------------+----------------+----------------+--------------+
   | 1.2.840.1      |                |                |              |
   | 0008.6.​1.​522 |                |                |              |
   +----------------+----------------+----------------+--------------+
   | 1.2.840.1      |                |                |              |
   | 0008.6.​1.​523 |                |                |              |
   +----------------+----------------+----------------+--------------+
   | 1.2.840.1      |                |                |              |
   | 0008.6.​1.​524 |                |                |              |
   +----------------+----------------+----------------+--------------+
   | 1.2.840.1      |                |                |              |
   | 0008.6.​1.​525 |                |                |              |
   +----------------+----------------+----------------+--------------+
   | 1.2.840.1      |                |                |              |
   | 0008.6.​1.​526 |                |                |              |
   +----------------+----------------+----------------+--------------+
   | 1.2.840.1      |                |                |              |
   | 0008.6.​1.​527 |                |                |              |
   +----------------+----------------+----------------+--------------+
   | 1.2.840.1      |                |                |              |
   | 0008.6.​1.​528 |                |                |              |
   +----------------+----------------+----------------+--------------+
   | 1.2.840.1      |                |                |              |
   | 0008.6.​1.​529 |                |                |              |
   +----------------+----------------+----------------+--------------+
   | 1.2.840.1      |                |                |              |
   | 0008.6.​1.​530 |                |                |              |
   +----------------+----------------+----------------+--------------+
   | 1.2.840.1      |                |                |              |
   | 0008.6.​1.​531 |                |                |              |
   +----------------+----------------+----------------+--------------+
   | *1.2.840.10    |                |                | *RET (2011)* |
   | 008.6.​1.​532* |                |                |              |
   +----------------+----------------+----------------+--------------+
   | 1.2.840.1      |                |                |              |
   | 0008.6.​1.​533 |                |                |              |
   +----------------+----------------+----------------+--------------+
   | 1.2.840.1      |                |                |              |
   | 0008.6.​1.​534 |                |                |              |
   +----------------+----------------+----------------+--------------+
   | 1.2.840.1      |                |                |              |
   | 0008.6.​1.​535 |                |                |              |
   +----------------+----------------+----------------+--------------+
   | 1.2.840.1      |                |                |              |
   | 0008.6.​1.​536 |                |                |              |
   +----------------+----------------+----------------+--------------+
   | 1.2.840.1      |                |                |              |
   | 0008.6.​1.​537 |                |                |              |
   +----------------+----------------+----------------+--------------+
   | 1.2.840.1      |                |                |              |
   | 0008.6.​1.​538 |                |                |              |
   +----------------+----------------+----------------+--------------+
   | 1.2.840.1      |                |                |              |
   | 0008.6.​1.​539 |                |                |              |
   +----------------+----------------+----------------+--------------+
   | 1.2.840.1      |                |                |              |
   | 0008.6.​1.​540 |                |                |              |
   +----------------+----------------+----------------+--------------+
   | 1.2.840.1      |                |                |              |
   | 0008.6.​1.​541 |                |                |              |
   +----------------+----------------+----------------+--------------+
   | 1.2.840.1      |                |                |              |
   | 0008.6.​1.​542 |                |                |              |
   +----------------+----------------+----------------+--------------+
   | 1.2.840.1      |                |                |              |
   | 0008.6.​1.​543 |                |                |              |
   +----------------+----------------+----------------+--------------+
   | 1.2.840.1      |                |                |              |
   | 0008.6.​1.​544 |                |                |              |
   +----------------+----------------+----------------+--------------+
   | 1.2.840.1      |                |                |              |
   | 0008.6.​1.​545 |                |                |              |
   +----------------+----------------+----------------+--------------+
   | 1.2.840.1      |                |                |              |
   | 0008.6.​1.​546 |                |                |              |
   +----------------+----------------+----------------+--------------+
   | 1.2.840.1      |                |                |              |
   | 0008.6.​1.​547 |                |                |              |
   +----------------+----------------+----------------+--------------+
   | 1.2.840.1      |                |                |              |
   | 0008.6.​1.​548 |                |                |              |
   +----------------+----------------+----------------+--------------+
   | 1.2.840.1      |                |                |              |
   | 0008.6.​1.​549 |                |                |              |
   +----------------+----------------+----------------+--------------+
   | 1.2.840.1      |                |                |              |
   | 0008.6.​1.​550 |                |                |              |
   +----------------+----------------+----------------+--------------+
   | 1.2.840.1      |                |                |              |
   | 0008.6.​1.​551 |                |                |              |
   +----------------+----------------+----------------+--------------+
   | 1.2.840.1      |                |                |              |
   | 0008.6.​1.​552 |                |                |              |
   +----------------+----------------+----------------+--------------+
   | 1.2.840.1      |                |                |              |
   | 0008.6.​1.​553 |                |                |              |
   +----------------+----------------+----------------+--------------+
   | 1.2.840.1      |                |                |              |
   | 0008.6.​1.​554 |                |                |              |
   +----------------+----------------+----------------+--------------+
   | 1.2.840.1      |                |                |              |
   | 0008.6.​1.​555 |                |                |              |
   +----------------+----------------+----------------+--------------+
   | 1.2.840.1      |                |                |              |
   | 0008.6.​1.​556 |                |                |              |
   +----------------+----------------+----------------+--------------+
   | 1.2.840.1      |                |                |              |
   | 0008.6.​1.​557 |                |                |              |
   +----------------+----------------+----------------+--------------+
   | 1.2.840.1      |                |                |              |
   | 0008.6.​1.​558 |                |                |              |
   +----------------+----------------+----------------+--------------+
   | 1.2.840.1      |                |                |              |
   | 0008.6.​1.​559 |                |                |              |
   +----------------+----------------+----------------+--------------+
   | 1.2.840.1      |                |                |              |
   | 0008.6.​1.​560 |                |                |              |
   +----------------+----------------+----------------+--------------+
   | 1.2.840.1      |                |                |              |
   | 0008.6.​1.​561 |                |                |              |
   +----------------+----------------+----------------+--------------+
   | 1.2.840.1      |                |                |              |
   | 0008.6.​1.​562 |                |                |              |
   +----------------+----------------+----------------+--------------+
   | 1.2.840.1      |                |                |              |
   | 0008.6.​1.​563 |                |                |              |
   +----------------+----------------+----------------+--------------+
   | 1.2.840.1      |                |                |              |
   | 0008.6.​1.​564 |                |                |              |
   +----------------+----------------+----------------+--------------+
   | 1.2.840.1      |                |                |              |
   | 0008.6.​1.​565 |                |                |              |
   +----------------+----------------+----------------+--------------+
   | 1.2.840.1      |                |                |              |
   | 0008.6.​1.​566 |                |                |              |
   +----------------+----------------+----------------+--------------+
   | 1.2.840.1      |                |                |              |
   | 0008.6.​1.​567 |                |                |              |
   +----------------+----------------+----------------+--------------+
   | 1.2.840.1      |                |                |              |
   | 0008.6.​1.​568 |                |                |              |
   +----------------+----------------+----------------+--------------+
   | 1.2.840.1      |                |                |              |
   | 0008.6.​1.​569 |                |                |              |
   +----------------+----------------+----------------+--------------+
   | 1.2.840.1      |                |                |              |
   | 0008.6.​1.​570 |                |                |              |
   +----------------+----------------+----------------+--------------+
   | 1.2.840.1      |                |                |              |
   | 0008.6.​1.​571 |                |                |              |
   +----------------+----------------+----------------+--------------+
   | 1.2.840.1      |                |                |              |
   | 0008.6.​1.​572 |                |                |              |
   +----------------+----------------+----------------+--------------+
   | 1.2.840.1      |                |                |              |
   | 0008.6.​1.​573 |                |                |              |
   +----------------+----------------+----------------+--------------+
   | 1.2.840.1      |                |                |              |
   | 0008.6.​1.​574 |                |                |              |
   +----------------+----------------+----------------+--------------+
   | 1.2.840.1      |                |                |              |
   | 0008.6.​1.​575 |                |                |              |
   +----------------+----------------+----------------+--------------+
   | 1.2.840.1      |                |                |              |
   | 0008.6.​1.​576 |                |                |              |
   +----------------+----------------+----------------+--------------+
   | 1.2.840.1      |                |                |              |
   | 0008.6.​1.​577 |                |                |              |
   +----------------+----------------+----------------+--------------+
   | 1.2.840.1      |                |                |              |
   | 0008.6.​1.​578 |                |                |              |
   +----------------+----------------+----------------+--------------+
   | 1.2.840.1      |                |                |              |
   | 0008.6.​1.​579 |                |                |              |
   +----------------+----------------+----------------+--------------+
   | 1.2.840.1      |                |                |              |
   | 0008.6.​1.​580 |                |                |              |
   +----------------+----------------+----------------+--------------+
   | 1.2.840.1      |                |                |              |
   | 0008.6.​1.​581 |                |                |              |
   +----------------+----------------+----------------+--------------+
   | 1.2.840.1      |                |                |              |
   | 0008.6.​1.​582 |                |                |              |
   +----------------+----------------+----------------+--------------+
   | 1.2.840.1      |                |                |              |
   | 0008.6.​1.​583 |                |                |              |
   +----------------+----------------+----------------+--------------+
   | 1.2.840.1      |                |                |              |
   | 0008.6.​1.​584 |                |                |              |
   +----------------+----------------+----------------+--------------+
   | 1.2.840.1      |                |                |              |
   | 0008.6.​1.​585 |                |                |              |
   +----------------+----------------+----------------+--------------+
   | 1.2.840.1      |                |                |              |
   | 0008.6.​1.​586 |                |                |              |
   +----------------+----------------+----------------+--------------+
   | 1.2.840.1      |                |                |              |
   | 0008.6.​1.​587 |                |                |              |
   +----------------+----------------+----------------+--------------+
   | 1.2.840.1      |                |                |              |
   | 0008.6.​1.​588 |                |                |              |
   +----------------+----------------+----------------+--------------+
   | 1.2.840.1      |                |                |              |
   | 0008.6.​1.​589 |                |                |              |
   +----------------+----------------+----------------+--------------+
   | 1.2.840.1      |                |                |              |
   | 0008.6.​1.​590 |                |                |              |
   +----------------+----------------+----------------+--------------+
   | 1.2.840.1      |                |                |              |
   | 0008.6.​1.​591 |                |                |              |
   +----------------+----------------+----------------+--------------+
   | 1.2.840.1      |                |                |              |
   | 0008.6.​1.​592 |                |                |              |
   +----------------+----------------+----------------+--------------+
   | 1.2.840.1      |                |                |              |
   | 0008.6.​1.​593 |                |                |              |
   +----------------+----------------+----------------+--------------+
   | 1.2.840.1      |                |                |              |
   | 0008.6.​1.​594 |                |                |              |
   +----------------+----------------+----------------+--------------+
   | 1.2.840.1      |                |                |              |
   | 0008.6.​1.​595 |                |                |              |
   +----------------+----------------+----------------+--------------+
   | 1.2.840.1      |                |                |              |
   | 0008.6.​1.​596 |                |                |              |
   +----------------+----------------+----------------+--------------+
   | 1.2.840.1      |                |                |              |
   | 0008.6.​1.​597 |                |                |              |
   +----------------+----------------+----------------+--------------+
   | 1.2.840.1      |                |                |              |
   | 0008.6.​1.​598 |                |                |              |
   +----------------+----------------+----------------+--------------+
   | 1.2.840.1      |                |                |              |
   | 0008.6.​1.​599 |                |                |              |
   +----------------+----------------+----------------+--------------+
   | 1.2.840.1      |                |                |              |
   | 0008.6.​1.​600 |                |                |              |
   +----------------+----------------+----------------+--------------+
   | 1.2.840.1      |                |                |              |
   | 0008.6.​1.​601 |                |                |              |
   +----------------+----------------+----------------+--------------+
   | 1.2.840.1      |                |                |              |
   | 0008.6.​1.​602 |                |                |              |
   +----------------+----------------+----------------+--------------+
   | 1.2.840.1      |                |                |              |
   | 0008.6.​1.​603 |                |                |              |
   +----------------+----------------+----------------+--------------+
   | 1.2.840.1      |                |                |              |
   | 0008.6.​1.​604 |                |                |              |
   +----------------+----------------+----------------+--------------+
   | 1.2.840.1      |                |                |              |
   | 0008.6.​1.​605 |                |                |              |
   +----------------+----------------+----------------+--------------+
   | 1.2.840.1      |                |                |              |
   | 0008.6.​1.​606 |                |                |              |
   +----------------+----------------+----------------+--------------+
   | 1.2.840.1      |                |                |              |
   | 0008.6.​1.​607 |                |                |              |
   +----------------+----------------+----------------+--------------+
   | 1.2.840.1      |                |                |              |
   | 0008.6.​1.​608 |                |                |              |
   +----------------+----------------+----------------+--------------+
   | 1.2.840.1      |                |                |              |
   | 0008.6.​1.​609 |                |                |              |
   +----------------+----------------+----------------+--------------+
   | 1.2.840.1      |                |                |              |
   | 0008.6.​1.​610 |                |                |              |
   +----------------+----------------+----------------+--------------+
   | 1.2.840.1      |                |                |              |
   | 0008.6.​1.​611 |                |                |              |
   +----------------+----------------+----------------+--------------+
   | 1.2.840.1      |                |                |              |
   | 0008.6.​1.​612 |                |                |              |
   +----------------+----------------+----------------+--------------+
   | 1.2.840.1      |                |                |              |
   | 0008.6.​1.​613 |                |                |              |
   +----------------+----------------+----------------+--------------+
   | 1.2.840.1      |                |                |              |
   | 0008.6.​1.​614 |                |                |              |
   +----------------+----------------+----------------+--------------+
   | 1.2.840.1      |                |                |              |
   | 0008.6.​1.​615 |                |                |              |
   +----------------+----------------+----------------+--------------+
   | 1.2.840.1      |                |                |              |
   | 0008.6.​1.​616 |                |                |              |
   +----------------+----------------+----------------+--------------+
   | 1.2.840.1      |                |                |              |
   | 0008.6.​1.​617 |                |                |              |
   +----------------+----------------+----------------+--------------+
   | 1.2.840.1      |                |                |              |
   | 0008.6.​1.​618 |                |                |              |
   +----------------+----------------+----------------+--------------+
   | 1.2.840.1      |                |                |              |
   | 0008.6.​1.​619 |                |                |              |
   +----------------+----------------+----------------+--------------+
   | 1.2.840.1      |                |                |              |
   | 0008.6.​1.​620 |                |                |              |
   +----------------+----------------+----------------+--------------+
   | 1.2.840.1      |                |                |              |
   | 0008.6.​1.​621 |                |                |              |
   +----------------+----------------+----------------+--------------+
   | 1.2.840.1      |                |                |              |
   | 0008.6.​1.​622 |                |                |              |
   +----------------+----------------+----------------+--------------+
   | 1.2.840.1      |                |                |              |
   | 0008.6.​1.​623 |                |                |              |
   +----------------+----------------+----------------+--------------+
   | 1.2.840.1      |                |                |              |
   | 0008.6.​1.​624 |                |                |              |
   +----------------+----------------+----------------+--------------+
   | 1.2.840.1      |                |                |              |
   | 0008.6.​1.​625 |                |                |              |
   +----------------+----------------+----------------+--------------+
   | 1.2.840.1      |                |                |              |
   | 0008.6.​1.​626 |                |                |              |
   +----------------+----------------+----------------+--------------+
   | 1.2.840.1      |                |                |              |
   | 0008.6.​1.​627 |                |                |              |
   +----------------+----------------+----------------+--------------+
   | 1.2.840.1      |                |                |              |
   | 0008.6.​1.​628 |                |                |              |
   +----------------+----------------+----------------+--------------+
   | 1.2.840.1      |                |                |              |
   | 0008.6.​1.​629 |                |                |              |
   +----------------+----------------+----------------+--------------+
   | 1.2.840.1      |                |                |              |
   | 0008.6.​1.​630 |                |                |              |
   +----------------+----------------+----------------+--------------+
   | 1.2.840.1      |                |                |              |
   | 0008.6.​1.​631 |                |                |              |
   +----------------+----------------+----------------+--------------+
   | 1.2.840.1      |                |                |              |
   | 0008.6.​1.​632 |                |                |              |
   +----------------+----------------+----------------+--------------+
   | 1.2.840.1      |                |                |              |
   | 0008.6.​1.​633 |                |                |              |
   +----------------+----------------+----------------+--------------+
   | 1.2.840.1      |                |                |              |
   | 0008.6.​1.​634 |                |                |              |
   +----------------+----------------+----------------+--------------+
   | 1.2.840.1      |                |                |              |
   | 0008.6.​1.​635 |                |                |              |
   +----------------+----------------+----------------+--------------+
   | 1.2.840.1      |                |                |              |
   | 0008.6.​1.​636 |                |                |              |
   +----------------+----------------+----------------+--------------+
   | 1.2.840.1      |                |                |              |
   | 0008.6.​1.​637 |                |                |              |
   +----------------+----------------+----------------+--------------+
   | 1.2.840.1      |                |                |              |
   | 0008.6.​1.​638 |                |                |              |
   +----------------+----------------+----------------+--------------+
   | 1.2.840.1      |                |                |              |
   | 0008.6.​1.​735 |                |                |              |
   +----------------+----------------+----------------+--------------+
   | 1.2.840.1      |                |                |              |
   | 0008.6.​1.​736 |                |                |              |
   +----------------+----------------+----------------+--------------+
   | 1.2.840.1      |                |                |              |
   | 0008.6.​1.​737 |                |                |              |
   +----------------+----------------+----------------+--------------+
   | 1.2.840.1      |                |                |              |
   | 0008.6.​1.​738 |                |                |              |
   +----------------+----------------+----------------+--------------+
   | 1.2.840.1      |                |                |              |
   | 0008.6.​1.​739 |                |                |              |
   +----------------+----------------+----------------+--------------+
   | 1.2.840.1      |                |                |              |
   | 0008.6.​1.​740 |                |                |              |
   +----------------+----------------+----------------+--------------+
   | 1.2.840.1      |                |                |              |
   | 0008.6.​1.​741 |                |                |              |
   +----------------+----------------+----------------+--------------+
   | 1.2.840.1      |                |                |              |
   | 0008.6.​1.​742 |                |                |              |
   +----------------+----------------+----------------+--------------+
   | 1.2.840.1      |                |                |              |
   | 0008.6.​1.​743 |                |                |              |
   +----------------+----------------+----------------+--------------+
   | 1.2.840.1      |                |                |              |
   | 0008.6.​1.​744 |                |                |              |
   +----------------+----------------+----------------+--------------+
   | 1.2.840.1      |                |                |              |
   | 0008.6.​1.​745 |                |                |              |
   +----------------+----------------+----------------+--------------+
   | 1.2.840.1      |                |                |              |
   | 0008.6.​1.​746 |                |                |              |
   +----------------+----------------+----------------+--------------+
   | 1.2.840.1      |                |                |              |
   | 0008.6.​1.​747 |                |                |              |
   +----------------+----------------+----------------+--------------+
   | 1.2.840.1      |                |                |              |
   | 0008.6.​1.​748 |                |                |              |
   +----------------+----------------+----------------+--------------+
   | 1.2.840.1      |                |                |              |
   | 0008.6.​1.​749 |                |                |              |
   +----------------+----------------+----------------+--------------+
   | 1.2.840.1      |                |                |              |
   | 0008.6.​1.​750 |                |                |              |
   +----------------+----------------+----------------+--------------+
   | 1.2.840.1      |                |                |              |
   | 0008.6.​1.​751 |                |                |              |
   +----------------+----------------+----------------+--------------+
   | 1.2.840.1      |                |                |              |
   | 0008.6.​1.​752 |                |                |              |
   +----------------+----------------+----------------+--------------+
   | 1.2.840.1      |                |                |              |
   | 0008.6.​1.​753 |                |                |              |
   +----------------+----------------+----------------+--------------+
   | 1.2.840.1      |                |                |              |
   | 0008.6.​1.​754 |                |                |              |
   +----------------+----------------+----------------+--------------+
   | 1.2.840.1      |                |                |              |
   | 0008.6.​1.​755 |                |                |              |
   +----------------+----------------+----------------+--------------+
   | 1.2.840.1      |                |                |              |
   | 0008.6.​1.​756 |                |                |              |
   +----------------+----------------+----------------+--------------+
   | 1.2.840.1      |                |                |              |
   | 0008.6.​1.​757 |                |                |              |
   +----------------+----------------+----------------+--------------+
   | 1.2.840.1      |                |                |              |
   | 0008.6.​1.​758 |                |                |              |
   +----------------+----------------+----------------+--------------+
   | 1.2.840.1      |                |                |              |
   | 0008.6.​1.​759 |                |                |              |
   +----------------+----------------+----------------+--------------+
   | 1.2.840.1      |                |                |              |
   | 0008.6.​1.​760 |                |                |              |
   +----------------+----------------+----------------+--------------+
   | 1.2.840.1      |                |                |              |
   | 0008.6.​1.​761 |                |                |              |
   +----------------+----------------+----------------+--------------+
   | 1.2.840.1      |                |                |              |
   | 0008.6.​1.​763 |                |                |              |
   +----------------+----------------+----------------+--------------+
   | 1.2.840.1      |                |                |              |
   | 0008.6.​1.​764 |                |                |              |
   +----------------+----------------+----------------+--------------+
   | 1.2.840.1      |                |                |              |
   | 0008.6.​1.​765 |                |                |              |
   +----------------+----------------+----------------+--------------+
   | 1.2.840.1      |                |                |              |
   | 0008.6.​1.​766 |                |                |              |
   +----------------+----------------+----------------+--------------+
   | 1.2.840.1      |                |                |              |
   | 0008.6.​1.​767 |                |                |              |
   +----------------+----------------+----------------+--------------+
   | 1.2.840.1      |                |                |              |
   | 0008.6.​1.​768 |                |                |              |
   +----------------+----------------+----------------+--------------+
   | 1.2.840.1      |                |                |              |
   | 0008.6.​1.​769 |                |                |              |
   +----------------+----------------+----------------+--------------+
   | 1.2.840.1      |                |                |              |
   | 0008.6.​1.​770 |                |                |              |
   +----------------+----------------+----------------+--------------+
   | 1.2.840.1      |                |                |              |
   | 0008.6.​1.​771 |                |                |              |
   +----------------+----------------+----------------+--------------+
   | 1.2.840.1      |                |                |              |
   | 0008.6.​1.​772 |                |                |              |
   +----------------+----------------+----------------+--------------+
   | 1.2.840.1      |                |                |              |
   | 0008.6.​1.​773 |                |                |              |
   +----------------+----------------+----------------+--------------+
   | 1.2.840.1      |                |                |              |
   | 0008.6.​1.​774 |                |                |              |
   +----------------+----------------+----------------+--------------+
   | 1.2.840.1      |                |                |              |
   | 0008.6.​1.​775 |                |                |              |
   +----------------+----------------+----------------+--------------+
   | 1.2.840.1      |                |                |              |
   | 0008.6.​1.​776 |                |                |              |
   +----------------+----------------+----------------+--------------+
   | 1.2.840.1      |                |                |              |
   | 0008.6.​1.​777 |                |                |              |
   +----------------+----------------+----------------+--------------+
   | 1.2.840.1      |                |                |              |
   | 0008.6.​1.​778 |                |                |              |
   +----------------+----------------+----------------+--------------+
   | 1.2.840.1      |                |                |              |
   | 0008.6.​1.​779 |                |                |              |
   +----------------+----------------+----------------+--------------+
   | 1.2.840.1      |                |                |              |
   | 0008.6.​1.​780 |                |                |              |
   +----------------+----------------+----------------+--------------+
   | 1.2.840.1      |                |                |              |
   | 0008.6.​1.​781 |                |                |              |
   +----------------+----------------+----------------+--------------+
   | 1.2.840.1      |                |                |              |
   | 0008.6.​1.​782 |                |                |              |
   +----------------+----------------+----------------+--------------+
   | 1.2.840.1      |                |                |              |
   | 0008.6.​1.​783 |                |                |              |
   +----------------+----------------+----------------+--------------+
   | 1.2.840.1      |                |                |              |
   | 0008.6.​1.​784 |                |                |              |
   +----------------+----------------+----------------+--------------+
   | 1.2.840.1      |                |                |              |
   | 0008.6.​1.​785 |                |                |              |
   +----------------+----------------+----------------+--------------+
   | 1.2.840.1      |                |                |              |
   | 0008.6.​1.​786 |                |                |              |
   +----------------+----------------+----------------+--------------+
   | 1.2.840.1      |                |                |              |
   | 0008.6.​1.​787 |                |                |              |
   +----------------+----------------+----------------+--------------+
   | 1.2.840.1      |                |                |              |
   | 0008.6.​1.​788 |                |                |              |
   +----------------+----------------+----------------+--------------+
   | 1.2.840.1      |                |                |              |
   | 0008.6.​1.​789 |                |                |              |
   +----------------+----------------+----------------+--------------+
   | 1.2.840.1      |                |                |              |
   | 0008.6.​1.​790 |                |                |              |
   +----------------+----------------+----------------+--------------+
   | 1.2.840.1      |                |                |              |
   | 0008.6.​1.​791 |                |                |              |
   +----------------+----------------+----------------+--------------+
   | 1.2.840.1      |                |                |              |
   | 0008.6.​1.​792 |                |                |              |
   +----------------+----------------+----------------+--------------+
   | 1.2.840.1      |                |                |              |
   | 0008.6.​1.​793 |                |                |              |
   +----------------+----------------+----------------+--------------+
   | 1.2.840.1      |                |                |              |
   | 0008.6.​1.​794 |                |                |              |
   +----------------+----------------+----------------+--------------+
   | 1.2.840.1      |                |                |              |
   | 0008.6.​1.​795 |                |                |              |
   +----------------+----------------+----------------+--------------+
   | 1.2.840.1      |                |                |              |
   | 0008.6.​1.​796 |                |                |              |
   +----------------+----------------+----------------+--------------+
   | 1.2.840.1      |                |                |              |
   | 0008.6.​1.​797 |                |                |              |
   +----------------+----------------+----------------+--------------+
   | 1.2.840.1      |                |                |              |
   | 0008.6.​1.​798 |                |                |              |
   +----------------+----------------+----------------+--------------+
   | 1.2.840.1      |                |                |              |
   | 0008.6.​1.​799 |                |                |              |
   +----------------+----------------+----------------+--------------+
   | 1.2.840.1      |                |                |              |
   | 0008.6.​1.​800 |                |                |              |
   +----------------+----------------+----------------+--------------+
   | 1.2.840.1      |                |                |              |
   | 0008.6.​1.​801 |                |                |              |
   +----------------+----------------+----------------+--------------+
   | 1.2.840.1      |                |                |              |
   | 0008.6.​1.​802 |                |                |              |
   +----------------+----------------+----------------+--------------+
   | 1.2.840.1      |                |                |              |
   | 0008.6.​1.​803 |                |                |              |
   +----------------+----------------+----------------+--------------+
   | 1.2.840.1      |                |                |              |
   | 0008.6.​1.​804 |                |                |              |
   +----------------+----------------+----------------+--------------+
   | 1.2.840.1      |                |                |              |
   | 0008.6.​1.​805 |                |                |              |
   +----------------+----------------+----------------+--------------+
   | 1.2.840.1      |                |                |              |
   | 0008.6.​1.​806 |                |                |              |
   +----------------+----------------+----------------+--------------+
   | 1.2.840.1      |                |                |              |
   | 0008.6.​1.​807 |                |                |              |
   +----------------+----------------+----------------+--------------+
   | 1.2.840.1      |                |                |              |
   | 0008.6.​1.​808 |                |                |              |
   +----------------+----------------+----------------+--------------+
   | 1.2.840.1      |                |                |              |
   | 0008.6.​1.​809 |                |                |              |
   +----------------+----------------+----------------+--------------+
   | 1.2.840.1      |                |                |              |
   | 0008.6.​1.​810 |                |                |              |
   +----------------+----------------+----------------+--------------+
   | 1.2.840.1      |                |                |              |
   | 0008.6.​1.​811 |                |                |              |
   +----------------+----------------+----------------+--------------+
   | 1.2.840.1      |                |                |              |
   | 0008.6.​1.​812 |                |                |              |
   +----------------+----------------+----------------+--------------+
   | 1.2.840.1      |                |                |              |
   | 0008.6.​1.​813 |                |                |              |
   +----------------+----------------+----------------+--------------+
   | 1.2.840.1      |                |                |              |
   | 0008.6.​1.​814 |                |                |              |
   +----------------+----------------+----------------+--------------+
   | 1.2.840.1      |                |                |              |
   | 0008.6.​1.​815 |                |                |              |
   +----------------+----------------+----------------+--------------+
   | 1.2.840.1      |                |                |              |
   | 0008.6.​1.​816 |                |                |              |
   +----------------+----------------+----------------+--------------+
   | 1.2.840.1      |                |                |              |
   | 0008.6.​1.​817 |                |                |              |
   +----------------+----------------+----------------+--------------+
   | 1.2.840.1      |                |                |              |
   | 0008.6.​1.​818 |                |                |              |
   +----------------+----------------+----------------+--------------+
   | 1.2.840.1      |                |                |              |
   | 0008.6.​1.​819 |                |                |              |
   +----------------+----------------+----------------+--------------+
   | 1.2.840.1      |                |                |              |
   | 0008.6.​1.​820 |                |                |              |
   +----------------+----------------+----------------+--------------+
   | 1.2.840.1      |                |                |              |
   | 0008.6.​1.​821 |                |                |              |
   +----------------+----------------+----------------+--------------+
   | 1.2.840.1      |                |                |              |
   | 0008.6.​1.​822 |                |                |              |
   +----------------+----------------+----------------+--------------+
   | 1.2.840.1      |                |                |              |
   | 0008.6.​1.​823 |                |                |              |
   +----------------+----------------+----------------+--------------+
   | 1.2.840.1      |                |                |              |
   | 0008.6.​1.​824 |                |                |              |
   +----------------+----------------+----------------+--------------+
   | 1.2.840.1      |                |                |              |
   | 0008.6.​1.​825 |                |                |              |
   +----------------+----------------+----------------+--------------+
   | 1.2.840.1      |                |                |              |
   | 0008.6.​1.​826 |                |                |              |
   +----------------+----------------+----------------+--------------+
   | 1.2.840.1      |                |                |              |
   | 0008.6.​1.​827 |                |                |              |
   +----------------+----------------+----------------+--------------+
   | 1.2.840.1      |                |                |              |
   | 0008.6.​1.​828 |                |                |              |
   +----------------+----------------+----------------+--------------+
   | 1.2.840.1      |                |                |              |
   | 0008.6.​1.​829 |                |                |              |
   +----------------+----------------+----------------+--------------+
   | 1.2.840.1      |                |                |              |
   | 0008.6.​1.​830 |                |                |              |
   +----------------+----------------+----------------+--------------+
   | 1.2.840.1      |                |                |              |
   | 0008.6.​1.​831 |                |                |              |
   +----------------+----------------+----------------+--------------+
   | 1.2.840.1      |                |                |              |
   | 0008.6.​1.​832 |                |                |              |
   +----------------+----------------+----------------+--------------+
   | 1.2.840.1      |                |                |              |
   | 0008.6.​1.​833 |                |                |              |
   +----------------+----------------+----------------+--------------+
   | 1.2.840.1      |                |                |              |
   | 0008.6.​1.​834 |                |                |              |
   +----------------+----------------+----------------+--------------+
   | 1.2.840.1      |                |                |              |
   | 0008.6.​1.​835 |                |                |              |
   +----------------+----------------+----------------+--------------+
   | 1.2.840.1      |                |                |              |
   | 0008.6.​1.​836 |                |                |              |
   +----------------+----------------+----------------+--------------+
   | 1.2.840.1      |                |                |              |
   | 0008.6.​1.​837 |                |                |              |
   +----------------+----------------+----------------+--------------+
   | 1.2.840.1      |                |                |              |
   | 0008.6.​1.​838 |                |                |              |
   +----------------+----------------+----------------+--------------+
   | 1.2.840.1      |                |                |              |
   | 0008.6.​1.​839 |                |                |              |
   +----------------+----------------+----------------+--------------+
   | 1.2.840.1      |                |                |              |
   | 0008.6.​1.​840 |                |                |              |
   +----------------+----------------+----------------+--------------+
   | 1.2.840.1      |                |                |              |
   | 0008.6.​1.​841 |                |                |              |
   +----------------+----------------+----------------+--------------+
   | 1.2.840.1      |                |                |              |
   | 0008.6.​1.​842 |                |                |              |
   +----------------+----------------+----------------+--------------+
   | 1.2.840.1      |                |                |              |
   | 0008.6.​1.​843 |                |                |              |
   +----------------+----------------+----------------+--------------+
   | 1.2.840.1      |                |                |              |
   | 0008.6.​1.​844 |                |                |              |
   +----------------+----------------+----------------+--------------+
   | 1.2.840.1      |                |                |              |
   | 0008.6.​1.​845 |                |                |              |
   +----------------+----------------+----------------+--------------+
   | 1.2.840.1      |                |                |              |
   | 0008.6.​1.​846 |                |                |              |
   +----------------+----------------+----------------+--------------+
   | 1.2.840.1      |                |                |              |
   | 0008.6.​1.​847 |                |                |              |
   +----------------+----------------+----------------+--------------+
   | 1.2.840.1      |                |                |              |
   | 0008.6.​1.​848 |                |                |              |
   +----------------+----------------+----------------+--------------+
   | 1.2.840.1      |                |                |              |
   | 0008.6.​1.​849 |                |                |              |
   +----------------+----------------+----------------+--------------+
   | 1.2.840.1      |                |                |              |
   | 0008.6.​1.​850 |                |                |              |
   +----------------+----------------+----------------+--------------+
   | 1.2.840.1      |                |                |              |
   | 0008.6.​1.​851 |                |                |              |
   +----------------+----------------+----------------+--------------+
   | 1.2.840.1      |                |                |              |
   | 0008.6.​1.​852 |                |                |              |
   +----------------+----------------+----------------+--------------+
   | 1.2.840.1      |                |                |              |
   | 0008.6.​1.​853 |                |                |              |
   +----------------+----------------+----------------+--------------+
   | 1.2.840.1      |                |                |              |
   | 0008.6.​1.​854 |                |                |              |
   +----------------+----------------+----------------+--------------+
   | 1.2.840.1      |                |                |              |
   | 0008.6.​1.​855 |                |                |              |
   +----------------+----------------+----------------+--------------+
   | 1.2.840.1      |                |                |              |
   | 0008.6.​1.​856 |                |                |              |
   +----------------+----------------+----------------+--------------+
   | 1.2.840.1      |                |                |              |
   | 0008.6.​1.​857 |                |                |              |
   +----------------+----------------+----------------+--------------+
   | 1.2.840.1      |                |                |              |
   | 0008.6.​1.​858 |                |                |              |
   +----------------+----------------+----------------+--------------+
   | 1.2.840.1      |                |                |              |
   | 0008.6.​1.​859 |                |                |              |
   +----------------+----------------+----------------+--------------+
   | 1.2.840.1      |                |                |              |
   | 0008.6.​1.​860 |                |                |              |
   +----------------+----------------+----------------+--------------+
   | 1.2.840.1      |                |                |              |
   | 0008.6.​1.​861 |                |                |              |
   +----------------+----------------+----------------+--------------+
   | 1.2.840.1      |                |                |              |
   | 0008.6.​1.​862 |                |                |              |
   +----------------+----------------+----------------+--------------+
   | 1.2.840.1      |                |                |              |
   | 0008.6.​1.​863 |                |                |              |
   +----------------+----------------+----------------+--------------+
   | 1.2.840.1      |                |                |              |
   | 0008.6.​1.​864 |                |                |              |
   +----------------+----------------+----------------+--------------+
   | 1.2.840.1      |                |                |              |
   | 0008.6.​1.​865 |                |                |              |
   +----------------+----------------+----------------+--------------+
   | 1.2.840.1      |                |                |              |
   | 0008.6.​1.​866 |                |                |              |
   +----------------+----------------+----------------+--------------+
   | 1.2.840.1      |                |                |              |
   | 0008.6.​1.​867 |                |                |              |
   +----------------+----------------+----------------+--------------+
   | 1.2.840.1      |                |                |              |
   | 0008.6.​1.​868 |                |                |              |
   +----------------+----------------+----------------+--------------+
   | 1.2.840.1      |                |                |              |
   | 0008.6.​1.​869 |                |                |              |
   +----------------+----------------+----------------+--------------+
   | 1.2.840.1      |                |                |              |
   | 0008.6.​1.​870 |                |                |              |
   +----------------+----------------+----------------+--------------+
   | 1.2.840.1      |                |                |              |
   | 0008.6.​1.​871 |                |                |              |
   +----------------+----------------+----------------+--------------+
   | 1.2.840.1      |                |                |              |
   | 0008.6.​1.​872 |                |                |              |
   +----------------+----------------+----------------+--------------+
   | 1.2.840.1      |                |                |              |
   | 0008.6.​1.​873 |                |                |              |
   +----------------+----------------+----------------+--------------+
   | 1.2.840.1      |                |                |              |
   | 0008.6.​1.​874 |                |                |              |
   +----------------+----------------+----------------+--------------+
   | 1.2.840.1      |                |                |              |
   | 0008.6.​1.​876 |                |                |              |
   +----------------+----------------+----------------+--------------+
   | 1.2.840.1      |                |                |              |
   | 0008.6.​1.​877 |                |                |              |
   +----------------+----------------+----------------+--------------+
   | 1.2.840.1      |                |                |              |
   | 0008.6.​1.​878 |                |                |              |
   +----------------+----------------+----------------+--------------+
   | 1.2.840.1      |                |                |              |
   | 0008.6.​1.​879 |                |                |              |
   +----------------+----------------+----------------+--------------+
   | 1.2.840.1      |                |                |              |
   | 0008.6.​1.​880 |                |                |              |
   +----------------+----------------+----------------+--------------+
   | 1.2.840.1      |                |                |              |
   | 0008.6.​1.​881 |                |                |              |
   +----------------+----------------+----------------+--------------+
   | 1.2.840.1      |                |                |              |
   | 0008.6.​1.​882 |                |                |              |
   +----------------+----------------+----------------+--------------+
   | 1.2.840.1      |                |                |              |
   | 0008.6.​1.​883 |                |                |              |
   +----------------+----------------+----------------+--------------+
   | 1.2.840.1      |                |                |              |
   | 0008.6.​1.​884 |                |                |              |
   +----------------+----------------+----------------+--------------+
   | 1.2.840.1      |                |                |              |
   | 0008.6.​1.​885 |                |                |              |
   +----------------+----------------+----------------+--------------+
   | 1.2.840.1      |                |                |              |
   | 0008.6.​1.​886 |                |                |              |
   +----------------+----------------+----------------+--------------+
   | 1.2.840.1      |                |                |              |
   | 0008.6.​1.​887 |                |                |              |
   +----------------+----------------+----------------+--------------+
   | 1.2.840.1      |                |                |              |
   | 0008.6.​1.​888 |                |                |              |
   +----------------+----------------+----------------+--------------+
   | 1.2.840.1      |                |                |              |
   | 0008.6.​1.​889 |                |                |              |
   +----------------+----------------+----------------+--------------+
   | 1.2.840.1      |                |                |              |
   | 0008.6.​1.​890 |                |                |              |
   +----------------+----------------+----------------+--------------+
   | 1.2.840.1      |                |                |              |
   | 0008.6.​1.​891 |                |                |              |
   +----------------+----------------+----------------+--------------+
   | 1.2.840.1      |                |                |              |
   | 0008.6.​1.​892 |                |                |              |
   +----------------+----------------+----------------+--------------+
   | 1.2.840.1      |                |                |              |
   | 0008.6.​1.​893 |                |                |              |
   +----------------+----------------+----------------+--------------+
   | 1.2.840.1      |                |                |              |
   | 0008.6.​1.​894 |                |                |              |
   +----------------+----------------+----------------+--------------+
   | 1.2.840.1      |                |                |              |
   | 0008.6.​1.​895 |                |                |              |
   +----------------+----------------+----------------+--------------+
   | 1.2.840.1      |                |                |              |
   | 0008.6.​1.​896 |                |                |              |
   +----------------+----------------+----------------+--------------+
   | 1.2.840.1      |                |                |              |
   | 0008.6.​1.​897 |                |                |              |
   +----------------+----------------+----------------+--------------+
   | 1.2.840.1      |                |                |              |
   | 0008.6.​1.​898 |                |                |              |
   +----------------+----------------+----------------+--------------+
   | 1.2.840.1      |                |                |              |
   | 0008.6.​1.​899 |                |                |              |
   +----------------+----------------+----------------+--------------+
   | 1.2.840.1      |                |                |              |
   | 0008.6.​1.​900 |                |                |              |
   +----------------+----------------+----------------+--------------+
   | 1.2.840.1      |                |                |              |
   | 0008.6.​1.​901 |                |                |              |
   +----------------+----------------+----------------+--------------+
   | 1.2.840.1      |                |                |              |
   | 0008.6.​1.​902 |                |                |              |
   +----------------+----------------+----------------+--------------+
   | 1.2.840.1      |                |                |              |
   | 0008.6.​1.​903 |                |                |              |
   +----------------+----------------+----------------+--------------+
   | 1.2.840.1      |                |                |              |
   | 0008.6.​1.​904 |                |                |              |
   +----------------+----------------+----------------+--------------+
   | 1.2.840.1      |                |                |              |
   | 0008.6.​1.​905 |                |                |              |
   +----------------+----------------+----------------+--------------+
   | 1.2.840.1      |                |                |              |
   | 0008.6.​1.​906 |                |                |              |
   +----------------+----------------+----------------+--------------+
   | 1.2.840.1      |                |                |              |
   | 0008.6.​1.​907 |                |                |              |
   +----------------+----------------+----------------+--------------+
   | 1.2.840.1      |                |                |              |
   | 0008.6.​1.​908 |                |                |              |
   +----------------+----------------+----------------+--------------+
   | 1.2.840.1      |                |                |              |
   | 0008.6.​1.​909 |                |                |              |
   +----------------+----------------+----------------+--------------+
   | 1.2.840.1      |                |                |              |
   | 0008.6.​1.​910 |                |                |              |
   +----------------+----------------+----------------+--------------+
   | 1.2.840.1      |                |                |              |
   | 0008.6.​1.​911 |                |                |              |
   +----------------+----------------+----------------+--------------+
   | 1.2.840.1      |                |                |              |
   | 0008.6.​1.​912 |                |                |              |
   +----------------+----------------+----------------+--------------+
   | 1.2.840.1      |                |                |              |
   | 0008.6.​1.​913 |                |                |              |
   +----------------+----------------+----------------+--------------+
   | 1.2.840.1      |                |                |              |
   | 0008.6.​1.​914 |                |                |              |
   +----------------+----------------+----------------+--------------+
   | 1.2.840.1      |                |                |              |
   | 0008.6.​1.​915 |                |                |              |
   +----------------+----------------+----------------+--------------+
   | 1.2.840.1      |                |                |              |
   | 0008.6.​1.​916 |                |                |              |
   +----------------+----------------+----------------+--------------+
   | 1.2.840.1      |                |                |              |
   | 0008.6.​1.​917 |                |                |              |
   +----------------+----------------+----------------+--------------+
   | 1.2.840.1      |                |                |              |
   | 0008.6.​1.​918 |                |                |              |
   +----------------+----------------+----------------+--------------+
   | 1.2.840.1      |                |                |              |
   | 0008.6.​1.​919 |                |                |              |
   +----------------+----------------+----------------+--------------+
   | 1.2.840.1      |                |                |              |
   | 0008.6.​1.​920 |                |                |              |
   +----------------+----------------+----------------+--------------+
   | 1.2.840.1      |                |                |              |
   | 0008.6.​1.​921 |                |                |              |
   +----------------+----------------+----------------+--------------+
   | 1.2.840.1      |                |                |              |
   | 0008.6.​1.​922 |                |                |              |
   +----------------+----------------+----------------+--------------+
   | 1.2.840.1      |                |                |              |
   | 0008.6.​1.​923 |                |                |              |
   +----------------+----------------+----------------+--------------+
   | 1.2.840.1      |                |                |              |
   | 0008.6.​1.​924 |                |                |              |
   +----------------+----------------+----------------+--------------+
   | 1.2.840.1      |                |                |              |
   | 0008.6.​1.​925 |                |                |              |
   +----------------+----------------+----------------+--------------+
   | 1.2.840.1      |                |                |              |
   | 0008.6.​1.​926 |                |                |              |
   +----------------+----------------+----------------+--------------+
   | 1.2.840.1      |                |                |              |
   | 0008.6.​1.​927 |                |                |              |
   +----------------+----------------+----------------+--------------+
   | 1.2.840.1      |                |                |              |
   | 0008.6.​1.​930 |                |                |              |
   +----------------+----------------+----------------+--------------+
   | 1.2.840.1      |                |                |              |
   | 0008.6.​1.​931 |                |                |              |
   +----------------+----------------+----------------+--------------+
   | 1.2.840.1      |                |                |              |
   | 0008.6.​1.​932 |                |                |              |
   +----------------+----------------+----------------+--------------+
   | 1.2.840.1      |                |                |              |
   | 0008.6.​1.​933 |                |                |              |
   +----------------+----------------+----------------+--------------+
   | 1.2.840.1      |                |                |              |
   | 0008.6.​1.​934 |                |                |              |
   +----------------+----------------+----------------+--------------+
   | 1.2.840.1      |                |                |              |
   | 0008.6.​1.​935 |                |                |              |
   +----------------+----------------+----------------+--------------+
   | 1.2.840.1      |                |                |              |
   | 0008.6.​1.​936 |                |                |              |
   +----------------+----------------+----------------+--------------+
   | 1.2.840.1      |                |                |              |
   | 0008.6.​1.​937 |                |                |              |
   +----------------+----------------+----------------+--------------+
   | 1.2.840.1      |                |                |              |
   | 0008.6.​1.​938 |                |                |              |
   +----------------+----------------+----------------+--------------+
   | 1.2.840.1      |                |                |              |
   | 0008.6.​1.​939 |                |                |              |
   +----------------+----------------+----------------+--------------+
   | 1.2.840.1      |                |                |              |
   | 0008.6.​1.​940 |                |                |              |
   +----------------+----------------+----------------+--------------+
   | 1.2.840.1      |                |                |              |
   | 0008.6.​1.​941 |                |                |              |
   +----------------+----------------+----------------+--------------+
   | 1.2.840.1      |                |                |              |
   | 0008.6.​1.​942 |                |                |              |
   +----------------+----------------+----------------+--------------+
   | 1.2.840.1      |                |                |              |
   | 0008.6.​1.​943 |                |                |              |
   +----------------+----------------+----------------+--------------+
   | 1.2.840.1      |                |                |              |
   | 0008.6.​1.​944 |                |                |              |
   +----------------+----------------+----------------+--------------+
   | 1.2.840.1      |                |                |              |
   | 0008.6.​1.​945 |                |                |              |
   +----------------+----------------+----------------+--------------+
   | 1.2.840.1      |                |                |              |
   | 0008.6.​1.​946 |                |                |              |
   +----------------+----------------+----------------+--------------+
   | 1.2.840.1      |                |                |              |
   | 0008.6.​1.​947 |                |                |              |
   +----------------+----------------+----------------+--------------+
   | 1.2.840.1      |                |                |              |
   | 0008.6.​1.​948 |                |                |              |
   +----------------+----------------+----------------+--------------+
   | 1.2.840.1      |                |                |              |
   | 0008.6.​1.​949 |                |                |              |
   +----------------+----------------+----------------+--------------+
   | 1.2.840.1      |                |                |              |
   | 0008.6.​1.​950 |                |                |              |
   +----------------+----------------+----------------+--------------+
   | 1.2.840.1      |                |                |              |
   | 0008.6.​1.​951 |                |                |              |
   +----------------+----------------+----------------+--------------+
   | 1.2.840.1      |                |                |              |
   | 0008.6.​1.​952 |                |                |              |
   +----------------+----------------+----------------+--------------+
   | 1.2.840.1      |                |                |              |
   | 0008.6.​1.​953 |                |                |              |
   +----------------+----------------+----------------+--------------+
   | 1.2.840.1      |                |                |              |
   | 0008.6.​1.​954 |                |                |              |
   +----------------+----------------+----------------+--------------+
   | 1.2.840.1      |                |                |              |
   | 0008.6.​1.​956 |                |                |              |
   +----------------+----------------+----------------+--------------+
   | 1.2.840.1      |                |                |              |
   | 0008.6.​1.​957 |                |                |              |
   +----------------+----------------+----------------+--------------+
   | 1.2.840.1      |                |                |              |
   | 0008.6.​1.​958 |                |                |              |
   +----------------+----------------+----------------+--------------+
   | 1.2.840.1      |                |                |              |
   | 0008.6.​1.​959 |                |                |              |
   +----------------+----------------+----------------+--------------+
   | 1.2.840.1      |                |                |              |
   | 0008.6.​1.​960 |                |                |              |
   +----------------+----------------+----------------+--------------+
   | 1.2.840.1      |                |                |              |
   | 0008.6.​1.​961 |                |                |              |
   +----------------+----------------+----------------+--------------+
   | 1.2.840.1      |                |                |              |
   | 0008.6.​1.​962 |                |                |              |
   +----------------+----------------+----------------+--------------+
   | 1.2.840.1      |                |                |              |
   | 0008.6.​1.​963 |                |                |              |
   +----------------+----------------+----------------+--------------+
   | 1.2.840.1      |                |                |              |
   | 0008.6.​1.​964 |                |                |              |
   +----------------+----------------+----------------+--------------+
   | 1.2.840.1      |                |                |              |
   | 0008.6.​1.​965 |                |                |              |
   +----------------+----------------+----------------+--------------+
   | 1.2.840.1      |                |                |              |
   | 0008.6.​1.​966 |                |                |              |
   +----------------+----------------+----------------+--------------+
   | 1.2.840.1      |                |                |              |
   | 0008.6.​1.​967 |                |                |              |
   +----------------+----------------+----------------+--------------+
   | 1.2.840.1      |                |                |              |
   | 0008.6.​1.​968 |                |                |              |
   +----------------+----------------+----------------+--------------+
   | 1.2.840.1      |                |                |              |
   | 0008.6.​1.​969 |                |                |              |
   +----------------+----------------+----------------+--------------+
   | 1.2.840        |                |                |              |
   | .10008.6.1.970 |                |                |              |
   +----------------+----------------+----------------+--------------+
   | 1.2.840.1      |                |                |              |
   | 0008.6.​1.​971 |                |                |              |
   +----------------+----------------+----------------+--------------+
   | 1.2.840        |                |                |              |
   | .10008.6.1.972 |                |                |              |
   +----------------+----------------+----------------+--------------+
   | 1.2.840        |                |                |              |
   | .10008.6.1.973 |                |                |              |
   +----------------+----------------+----------------+--------------+
   | 1.2.840        |                |                |              |
   | .10008.6.1.975 |                |                |              |
   +----------------+----------------+----------------+--------------+
   | 1.2.840        |                |                |              |
   | .10008.6.1.976 |                |                |              |
   +----------------+----------------+----------------+--------------+
   | 1.2.840        |                |                |              |
   | .10008.6.1.977 |                |                |              |
   +----------------+----------------+----------------+--------------+
   | 1.2.840        |                |                |              |
   | .10008.6.1.978 |                |                |              |
   +----------------+----------------+----------------+--------------+
   | 1.2.840        |                |                |              |
   | .10008.6.1.979 |                |                |              |
   +----------------+----------------+----------------+--------------+
   | 1.2.840        |                |                |              |
   | .10008.6.1.980 |                |                |              |
   +----------------+----------------+----------------+--------------+
   | 1.2.840        |                |                |              |
   | .10008.6.1.981 |                |                |              |
   +----------------+----------------+----------------+--------------+
   | 1.2.840        |                |                |              |
   | .10008.6.1.982 |                |                |              |
   +----------------+----------------+----------------+--------------+
   | 1.2.840        |                |                |              |
   | .10008.6.1.983 |                |                |              |
   +----------------+----------------+----------------+--------------+
   | 1.2.840        |                |                |              |
   | .10008.6.1.984 |                |                |              |
   +----------------+----------------+----------------+--------------+
   | 1.2.840        |                |                |              |
   | .10008.6.1.985 |                |                |              |
   +----------------+----------------+----------------+--------------+
   | 1.2.840        |                |                |              |
   | .10008.6.1.986 |                |                |              |
   +----------------+----------------+----------------+--------------+
   | 1.2.840        |                |                |              |
   | .10008.6.1.987 |                |                |              |
   +----------------+----------------+----------------+--------------+
   | 1.2.840        |                |                |              |
   | .10008.6.1.988 |                |                |              |
   +----------------+----------------+----------------+--------------+
   | 1.2.840        |                |                |              |
   | .10008.6.1.989 |                |                |              |
   +----------------+----------------+----------------+--------------+
   | 1.2.840        |                |                |              |
   | .10008.6.1.990 |                |                |              |
   +----------------+----------------+----------------+--------------+
   | 1.2.840        |                |                |              |
   | .10008.6.1.991 |                |                |              |
   +----------------+----------------+----------------+--------------+
   | 1.2.840        |                |                |              |
   | .10008.6.1.992 |                |                |              |
   +----------------+----------------+----------------+--------------+
   | 1.2.840        |                |                |              |
   | .10008.6.1.993 |                |                |              |
   +----------------+----------------+----------------+--------------+
   | 1.2.840        |                |                |              |
   | .10008.6.1.994 |                |                |              |
   +----------------+----------------+----------------+--------------+
   | 1.2.840        |                |                |              |
   | .10008.6.1.995 |                |                |              |
   +----------------+----------------+----------------+--------------+
   | 1.2.840        |                |                |              |
   | .10008.6.1.996 |                |                |              |
   +----------------+----------------+----------------+--------------+
   | 1.2.840        |                |                |              |
   | .10008.6.1.997 |                |                |              |
   +----------------+----------------+----------------+--------------+
   | 1.2.840        |                |                |              |
   | .10008.6.1.998 |                |                |              |
   +----------------+----------------+----------------+--------------+
   | 1.2.840        |                |                |              |
   | .10008.6.1.999 |                |                |              |
   +----------------+----------------+----------------+--------------+
   | 1.2.840.       |                |                |              |
   | 10008.6.1.1000 |                |                |              |
   +----------------+----------------+----------------+--------------+
   | 1.2.840.       |                |                |              |
   | 10008.6.1.1001 |                |                |              |
   +----------------+----------------+----------------+--------------+
   | 1.2.840.       |                |                |              |
   | 10008.6.1.1002 |                |                |              |
   +----------------+----------------+----------------+--------------+
   | 1.2.840.       |                |                |              |
   | 10008.6.1.1003 |                |                |              |
   +----------------+----------------+----------------+--------------+
   | 1.2.840.       |                |                |              |
   | 10008.6.1.1004 |                |                |              |
   +----------------+----------------+----------------+--------------+
   | 1.2.840.       |                |                |              |
   | 10008.6.1.1005 |                |                |              |
   +----------------+----------------+----------------+--------------+
   | 1.2.840.       |                |                |              |
   | 10008.6.1.1006 |                |                |              |
   +----------------+----------------+----------------+--------------+
   | 1.2.840.       |                |                |              |
   | 10008.6.1.1007 |                |                |              |
   +----------------+----------------+----------------+--------------+
   | 1.2.840.       |                |                |              |
   | 10008.6.1.1008 |                |                |              |
   +----------------+----------------+----------------+--------------+
   | 1.2.840.       |                |                |              |
   | 10008.6.1.1009 |                |                |              |
   +----------------+----------------+----------------+--------------+
   | 1.2.840.       |                |                |              |
   | 10008.6.1.1010 |                |                |              |
   +----------------+----------------+----------------+--------------+
   | 1.2.840.       |                |                |              |
   | 10008.6.1.1011 |                |                |              |
   +----------------+----------------+----------------+--------------+
   | 1.2.840.       |                |                |              |
   | 10008.6.1.1012 |                |                |              |
   +----------------+----------------+----------------+--------------+
   | 1.2.840.       |                |                |              |
   | 10008.6.1.1013 |                |                |              |
   +----------------+----------------+----------------+--------------+
   | 1.2.840.       |                |                |              |
   | 10008.6.1.1014 |                |                |              |
   +----------------+----------------+----------------+--------------+
   | 1.2.840.       |                |                |              |
   | 10008.6.1.1015 |                |                |              |
   +----------------+----------------+----------------+--------------+
   | 1.2.840.       |                |                |              |
   | 10008.6.1.1016 |                |                |              |
   +----------------+----------------+----------------+--------------+
   | 1.2.840.       |                |                |              |
   | 10008.6.1.1017 |                |                |              |
   +----------------+----------------+----------------+--------------+
   | 1.2.840.       |                |                |              |
   | 10008.6.1.1018 |                |                |              |
   +----------------+----------------+----------------+--------------+
   | 1.2.840.       |                |                |              |
   | 10008.6.1.1019 |                |                |              |
   +----------------+----------------+----------------+--------------+
   | 1.2.840.       |                |                |              |
   | 10008.6.1.1020 |                |                |              |
   +----------------+----------------+----------------+--------------+
   | 1.2.840.       |                |                |              |
   | 10008.6.1.1021 |                |                |              |
   +----------------+----------------+----------------+--------------+
   | 1.2.840.       |                |                |              |
   | 10008.6.1.1022 |                |                |              |
   +----------------+----------------+----------------+--------------+
   | 1.2.840.       |                |                |              |
   | 10008.6.1.1023 |                |                |              |
   +----------------+----------------+----------------+--------------+
   | 1.2.840.       |                |                |              |
   | 10008.6.1.1024 |                |                |              |
   +----------------+----------------+----------------+--------------+
   | 1.2.840.       |                |                |              |
   | 10008.6.1.1025 |                |                |              |
   +----------------+----------------+----------------+--------------+
   | 1.2.840.       |                |                |              |
   | 10008.6.1.1026 |                |                |              |
   +----------------+----------------+----------------+--------------+
   | 1.2.840.       |                |                |              |
   | 10008.6.1.1027 |                |                |              |
   +----------------+----------------+----------------+--------------+
   | 1.2.840.       |                |                |              |
   | 10008.6.1.1028 |                |                |              |
   +----------------+----------------+----------------+--------------+
   | 1.2.840.       |                |                |              |
   | 10008.6.1.1029 |                |                |              |
   +----------------+----------------+----------------+--------------+
   | 1.2.840.       |                |                |              |
   | 10008.6.1.1030 |                |                |              |
   +----------------+----------------+----------------+--------------+
   | 1.2.840.       |                |                |              |
   | 10008.6.1.1031 |                |                |              |
   +----------------+----------------+----------------+--------------+
   | 1.2.840.       |                |                |              |
   | 10008.6.1.1032 |                |                |              |
   +----------------+----------------+----------------+--------------+
   | 1.2.840.       |                |                |              |
   | 10008.6.1.1033 |                |                |              |
   +----------------+----------------+----------------+--------------+
   | 1.2.840.       |                |                |              |
   | 10008.6.1.1034 |                |                |              |
   +----------------+----------------+----------------+--------------+
   | 1.2.840.       |                |                |              |
   | 10008.6.1.1035 |                |                |              |
   +----------------+----------------+----------------+--------------+
   | 1.2.840.       |                |                |              |
   | 10008.6.1.1036 |                |                |              |
   +----------------+----------------+----------------+--------------+
   | 1.2.840.       |                |                |              |
   | 10008.6.1.1037 |                |                |              |
   +----------------+----------------+----------------+--------------+
   | 1.2.840.       |                |                |              |
   | 10008.6.1.1038 |                |                |              |
   +----------------+----------------+----------------+--------------+
   | 1.2.840.       |                |                |              |
   | 10008.6.1.1039 |                |                |              |
   +----------------+----------------+----------------+--------------+
   | 1.2.840.       |                |                |              |
   | 10008.6.1.1040 |                |                |              |
   +----------------+----------------+----------------+--------------+
   | 1.2.840.       |                |                |              |
   | 10008.6.1.1041 |                |                |              |
   +----------------+----------------+----------------+--------------+
   | 1.2.840.       |                |                |              |
   | 10008.6.1.1042 |                |                |              |
   +----------------+----------------+----------------+--------------+
   | 1.2.840.       |                |                |              |
   | 10008.6.1.1043 |                |                |              |
   +----------------+----------------+----------------+--------------+
   | 1.2.840.       |                |                |              |
   | 10008.6.1.1044 |                |                |              |
   +----------------+----------------+----------------+--------------+
   | 1.2.840.       |                |                |              |
   | 10008.6.1.1045 |                |                |              |
   +----------------+----------------+----------------+--------------+
   | 1.2.840.       |                |                |              |
   | 10008.6.1.1046 |                |                |              |
   +----------------+----------------+----------------+--------------+
   | 1.2.840.       |                |                |              |
   | 10008.6.1.1047 |                |                |              |
   +----------------+----------------+----------------+--------------+
   | 1.2.840.       |                |                |              |
   | 10008.6.1.1048 |                |                |              |
   +----------------+----------------+----------------+--------------+
   | 1.2.840.       |                |                |              |
   | 10008.6.1.1049 |                |                |              |
   +----------------+----------------+----------------+--------------+
   | 1.2.840.       |                |                |              |
   | 10008.6.1.1050 |                |                |              |
   +----------------+----------------+----------------+--------------+
   | 1.2.840.       |                |                |              |
   | 10008.6.1.1051 |                |                |              |
   +----------------+----------------+----------------+--------------+
   | 1.2.840.       |                |                |              |
   | 10008.6.1.1052 |                |                |              |
   +----------------+----------------+----------------+--------------+
   | 1.2.840.       |                |                |              |
   | 10008.6.1.1053 |                |                |              |
   +----------------+----------------+----------------+--------------+
   | 1.2.840.       |                |                |              |
   | 10008.6.1.1054 |                |                |              |
   +----------------+----------------+----------------+--------------+
   | 1.2.840.       |                |                |              |
   | 10008.6.1.1055 |                |                |              |
   +----------------+----------------+----------------+--------------+
   | 1.2.840.       |                |                |              |
   | 10008.6.1.1056 |                |                |              |
   +----------------+----------------+----------------+--------------+
   | 1.2.840.       |                |                |              |
   | 10008.6.1.1057 |                |                |              |
   +----------------+----------------+----------------+--------------+
   | 1.2.840.       |                |                |              |
   | 10008.6.1.1058 |                |                |              |
   +----------------+----------------+----------------+--------------+
   | 1.2.840.       |                |                |              |
   | 10008.6.1.1059 |                |                |              |
   +----------------+----------------+----------------+--------------+
   | 1.2.840.       |                |                |              |
   | 10008.6.1.1060 |                |                |              |
   +----------------+----------------+----------------+--------------+
   | 1.2.840.       |                |                |              |
   | 10008.6.1.1061 |                |                |              |
   +----------------+----------------+----------------+--------------+
   | 1.2.840.       |                |                |              |
   | 10008.6.1.1062 |                |                |              |
   +----------------+----------------+----------------+--------------+
   | 1.2.840.10     |                |                |              |
   | 008.6.​1.​1063 |                |                |              |
   +----------------+----------------+----------------+--------------+
   | 1.2.840.10     |                |                |              |
   | 008.6.​1.​1064 |                |                |              |
   +----------------+----------------+----------------+--------------+
   | 1.2.840.10     |                |                |              |
   | 008.6.​1.​1065 |                |                |              |
   +----------------+----------------+----------------+--------------+
   | 1.2.840.10     |                |                |              |
   | 008.6.​1.​1066 |                |                |              |
   +----------------+----------------+----------------+--------------+
   | 1.2.840.10     |                |                |              |
   | 008.6.​1.​1067 |                |                |              |
   +----------------+----------------+----------------+--------------+
   | 1.2.840.10     |                |                |              |
   | 008.6.​1.​1068 |                |                |              |
   +----------------+----------------+----------------+--------------+
   | 1.2.840.10     |                |                |              |
   | 008.6.​1.​1069 |                |                |              |
   +----------------+----------------+----------------+--------------+
   | 1.2.840.10     |                |                |              |
   | 008.6.​1.​1070 |                |                |              |
   +----------------+----------------+----------------+--------------+
   | 1.2.840.10     |                |                |              |
   | 008.6.​1.​1071 |                |                |              |
   +----------------+----------------+----------------+--------------+
   | 1.2.840.10     |                |                |              |
   | 008.6.​1.​1072 |                |                |              |
   +----------------+----------------+----------------+--------------+
   | 1.2.840.10     |                |                |              |
   | 008.6.​1.​1073 |                |                |              |
   +----------------+----------------+----------------+--------------+
   | 1.2.840.10     |                |                |              |
   | 008.6.​1.​1074 |                |                |              |
   +----------------+----------------+----------------+--------------+
   | 1.2.840.10     |                |                |              |
   | 008.6.​1.​1075 |                |                |              |
   +----------------+----------------+----------------+--------------+
   | 1.2.840.10     |                |                |              |
   | 008.6.​1.​1076 |                |                |              |
   +----------------+----------------+----------------+--------------+
   | 1.2.840.10     |                |                |              |
   | 008.6.​1.​1077 |                |                |              |
   +----------------+----------------+----------------+--------------+
   | 1.2.840.10     |                |                |              |
   | 008.6.​1.​1078 |                |                |              |
   +----------------+----------------+----------------+--------------+
   | 1.2.840.10     |                |                |              |
   | 008.6.​1.​1079 |                |                |              |
   +----------------+----------------+----------------+--------------+
   | 1.2.840.10     |                |                |              |
   | 008.6.​1.​1080 |                |                |              |
   +----------------+----------------+----------------+--------------+
   | 1.2.840.10     |                |                |              |
   | 008.6.​1.​1081 |                |                |              |
   +----------------+----------------+----------------+--------------+
   | 1.2.840.10     |                |                |              |
   | 008.6.​1.​1082 |                |                |              |
   +----------------+----------------+----------------+--------------+
   | 1.2.840.10     |                |                |              |
   | 008.6.​1.​1083 |                |                |              |
   +----------------+----------------+----------------+--------------+
   | 1.2.840.10     |                |                |              |
   | 008.6.​1.​1084 |                |                |              |
   +----------------+----------------+----------------+--------------+
   | 1.2.840.10     |                |                |              |
   | 008.6.​1.​1085 |                |                |              |
   +----------------+----------------+----------------+--------------+
   | 1.2.840.10     |                |                |              |
   | 008.6.​1.​1086 |                |                |              |
   +----------------+----------------+----------------+--------------+
   | 1.2.840.10     |                |                |              |
   | 008.6.​1.​1087 |                |                |              |
   +----------------+----------------+----------------+--------------+
   | 1.2.840.10     |                |                |              |
   | 008.6.​1.​1088 |                |                |              |
   +----------------+----------------+----------------+--------------+
   | 1.2.840.10     |                |                |              |
   | 008.6.​1.​1089 |                |                |              |
   +----------------+----------------+----------------+--------------+
   | 1.2.840.10     |                |                |              |
   | 008.6.​1.​1090 |                |                |              |
   +----------------+----------------+----------------+--------------+
   | 1.2.840.10     |                |                |              |
   | 008.6.​1.​1091 |                |                |              |
   +----------------+----------------+----------------+--------------+
   | 1.2.840.10     |                |                |              |
   | 008.6.​1.​1092 |                |                |              |
   +----------------+----------------+----------------+--------------+
   | 1.2.840.10     |                |                |              |
   | 008.6.​1.​1093 |                |                |              |
   +----------------+----------------+----------------+--------------+
   | 1.2.840.10     |                |                |              |
   | 008.6.​1.​1094 |                |                |              |
   +----------------+----------------+----------------+--------------+
   | 1.2.840.10     |                |                |              |
   | 008.6.​1.​1095 |                |                |              |
   +----------------+----------------+----------------+--------------+
   | 1.2.840.10     |                |                |              |
   | 008.6.​1.​1096 |                |                |              |
   +----------------+----------------+----------------+--------------+
   | 1.2.840.10     |                |                |              |
   | 008.6.​1.​1097 |                |                |              |
   +----------------+----------------+----------------+--------------+
   | 1.2.840.10     |                |                |              |
   | 008.6.​1.​1098 |                |                |              |
   +----------------+----------------+----------------+--------------+
   | 1.2.840.10     |                |                |              |
   | 008.6.​1.​1099 |                |                |              |
   +----------------+----------------+----------------+--------------+
   | 1.2.840.10     |                |                |              |
   | 008.6.​1.​1100 |                |                |              |
   +----------------+----------------+----------------+--------------+
   | 1.2.840.10     |                |                |              |
   | 008.6.​1.​1101 |                |                |              |
   +----------------+----------------+----------------+--------------+
   | 1.2.840.10     |                |                |              |
   | 008.6.​1.​1102 |                |                |              |
   +----------------+----------------+----------------+--------------+
   | 1.2.840.10     |                |                |              |
   | 008.6.​1.​1103 |                |                |              |
   +----------------+----------------+----------------+--------------+
   | 1.2.840.10     |                |                |              |
   | 008.6.​1.​1104 |                |                |              |
   +----------------+----------------+----------------+--------------+
   | 1.2.840.10     |                |                |              |
   | 008.6.​1.​1105 |                |                |              |
   +----------------+----------------+----------------+--------------+
   | 1.2.840.10     |                |                |              |
   | 008.6.​1.​1106 |                |                |              |
   +----------------+----------------+----------------+--------------+
   | 1.2.840.10     |                |                |              |
   | 008.6.​1.​1107 |                |                |              |
   +----------------+----------------+----------------+--------------+
   | 1.2.840.10     |                |                |              |
   | 008.6.​1.​1108 |                |                |              |
   +----------------+----------------+----------------+--------------+
   | 1.2.840.10     |                |                |              |
   | 008.6.​1.​1109 |                |                |              |
   +----------------+----------------+----------------+--------------+
   | 1.2.840.10     |                |                |              |
   | 008.6.​1.​1110 |                |                |              |
   +----------------+----------------+----------------+--------------+
   | 1.2.840.10     |                |                |              |
   | 008.6.​1.​1111 |                |                |              |
   +----------------+----------------+----------------+--------------+
   | 1.2.840.10     |                |                |              |
   | 008.6.​1.​1112 |                |                |              |
   +----------------+----------------+----------------+--------------+
   | 1.2.840.10     |                |                |              |
   | 008.6.​1.​1113 |                |                |              |
   +----------------+----------------+----------------+--------------+
   | 1.2.840.10     |                |                |              |
   | 008.6.​1.​1114 |                |                |              |
   +----------------+----------------+----------------+--------------+
   | 1.2.840.10     |                |                |              |
   | 008.6.​1.​1115 |                |                |              |
   +----------------+----------------+----------------+--------------+
   | 1.2.840.10     |                |                |              |
   | 008.6.​1.​1116 |                |                |              |
   +----------------+----------------+----------------+--------------+
   | 1.2.840.10     |                |                |              |
   | 008.6.​1.​1117 |                |                |              |
   +----------------+----------------+----------------+--------------+
   | 1.2.840.10     |                |                |              |
   | 008.6.​1.​1118 |                |                |              |
   +----------------+----------------+----------------+--------------+
   | 1.2.840.10     |                |                |              |
   | 008.6.​1.​1119 |                |                |              |
   +----------------+----------------+----------------+--------------+
   | 1.2.840.10     |                |                |              |
   | 008.6.​1.​1120 |                |                |              |
   +----------------+----------------+----------------+--------------+
   | 1.2.840.       |                |                |              |
   | 10008.6.1.1121 |                |                |              |
   +----------------+----------------+----------------+--------------+
   | 1.2.840.       |                |                |              |
   | 10008.6.1.1122 |                |                |              |
   +----------------+----------------+----------------+--------------+
   | 1.2.840.       |                |                |              |
   | 10008.6.1.1123 |                |                |              |
   +----------------+----------------+----------------+--------------+
   | 1.2.840.       |                |                |              |
   | 10008.6.1.1124 |                |                |              |
   +----------------+----------------+----------------+--------------+
   | 1.2.840.       |                |                |              |
   | 10008.6.1.1125 |                |                |              |
   +----------------+----------------+----------------+--------------+
   | 1.2.840.       |                |                |              |
   | 10008.6.1.1126 |                |                |              |
   +----------------+----------------+----------------+--------------+
   | 1.2.840.       |                |                |              |
   | 10008.6.1.1127 |                |                |              |
   +----------------+----------------+----------------+--------------+
   | 1.2.840.       |                |                |              |
   | 10008.6.1.1128 |                |                |              |
   +----------------+----------------+----------------+--------------+
   | 1.2.840.       |                |                |              |
   | 10008.6.1.1129 |                |                |              |
   +----------------+----------------+----------------+--------------+
   | 1.2.840.       |                |                |              |
   | 10008.6.1.1130 |                |                |              |
   +----------------+----------------+----------------+--------------+
   | 1.2.840.       |                |                |              |
   | 10008.6.1.1131 |                |                |              |
   +----------------+----------------+----------------+--------------+
   | 1.2.840.       |                |                |              |
   | 10008.6.1.1132 |                |                |              |
   +----------------+----------------+----------------+--------------+
   | 1.2.840.       |                |                |              |
   | 10008.6.1.1133 |                |                |              |
   +----------------+----------------+----------------+--------------+
   | 1.2.840.       |                |                |              |
   | 10008.6.1.1134 |                |                |              |
   +----------------+----------------+----------------+--------------+
   | 1.2.840.       |                |                |              |
   | 10008.6.1.1135 |                |                |              |
   +----------------+----------------+----------------+--------------+
   | 1.2.840.       |                |                |              |
   | 10008.6.1.1136 |                |                |              |
   +----------------+----------------+----------------+--------------+
   | 1.2.840.       |                |                |              |
   | 10008.6.1.1137 |                |                |              |
   +----------------+----------------+----------------+--------------+
   | 1.2.840.       |                |                |              |
   | 10008.6.1.1138 |                |                |              |
   +----------------+----------------+----------------+--------------+
   | 1.2.840.       |                |                |              |
   | 10008.6.1.1139 |                |                |              |
   +----------------+----------------+----------------+--------------+
   | 1.2.840.       |                |                |              |
   | 10008.6.1.1140 |                |                |              |
   +----------------+----------------+----------------+--------------+
   | 1.2.840.       |                |                |              |
   | 10008.6.1.1141 |                |                |              |
   +----------------+----------------+----------------+--------------+
   | 1.2.840.       |                |                |              |
   | 10008.6.1.1142 |                |                |              |
   +----------------+----------------+----------------+--------------+
   | 1.2.840.       |                |                |              |
   | 10008.6.1.1143 |                |                |              |
   +----------------+----------------+----------------+--------------+
   | 1.2.840.       |                |                |              |
   | 10008.6.1.1144 |                |                |              |
   +----------------+----------------+----------------+--------------+
   | 1.2.840.       |                |                |              |
   | 10008.6.1.1145 |                |                |              |
   +----------------+----------------+----------------+--------------+
   | 1.2.840.       |                |                |              |
   | 10008.6.1.1146 |                |                |              |
   +----------------+----------------+----------------+--------------+
   | 1.2.840.       |                |                |              |
   | 10008.6.1.1147 |                |                |              |
   +----------------+----------------+----------------+--------------+
   | 1.2.840.       |                |                |              |
   | 10008.6.1.1148 |                |                |              |
   +----------------+----------------+----------------+--------------+
   | 1.2.840.       |                |                |              |
   | 10008.6.1.1149 |                |                |              |
   +----------------+----------------+----------------+--------------+
   | 1.2.840.       |                |                |              |
   | 10008.6.1.1150 |                |                |              |
   +----------------+----------------+----------------+--------------+
   | 1.2.840.       |                |                |              |
   | 10008.6.1.1151 |                |                |              |
   +----------------+----------------+----------------+--------------+
   | 1.2.840.       |                |                |              |
   | 10008.6.1.1152 |                |                |              |
   +----------------+----------------+----------------+--------------+
   | 1.2.840.       |                |                |              |
   | 10008.6.1.1153 |                |                |              |
   +----------------+----------------+----------------+--------------+
   | 1.2.840.       |                |                |              |
   | 10008.6.1.1154 |                |                |              |
   +----------------+----------------+----------------+--------------+
   | 1.2.840.       |                |                |              |
   | 10008.6.1.1155 |                |                |              |
   +----------------+----------------+----------------+--------------+
   | 1.2.840.       |                |                |              |
   | 10008.6.1.1156 |                |                |              |
   +----------------+----------------+----------------+--------------+
   | 1.2.840.       |                |                |              |
   | 10008.6.1.1157 |                |                |              |
   +----------------+----------------+----------------+--------------+
   | 1.2.840.       |                |                |              |
   | 10008.6.1.1158 |                |                |              |
   +----------------+----------------+----------------+--------------+
   | 1.2.840.       |                |                |              |
   | 10008.6.1.1159 |                |                |              |
   +----------------+----------------+----------------+--------------+
   | 1.2.840.       |                |                |              |
   | 10008.6.1.1160 |                |                |              |
   +----------------+----------------+----------------+--------------+
   | 1.2.840.       |                |                |              |
   | 10008.6.1.1161 |                |                |              |
   +----------------+----------------+----------------+--------------+
   | 1.2.840.       |                |                |              |
   | 10008.6.1.1162 |                |                |              |
   +----------------+----------------+----------------+--------------+
   | 1.2.840.       |                |                |              |
   | 10008.6.1.1163 |                |                |              |
   +----------------+----------------+----------------+--------------+
   | 1.2.840.       |                |                |              |
   | 10008.6.1.1164 |                |                |              |
   +----------------+----------------+----------------+--------------+
   | 1.2.840.       |                |                |              |
   | 10008.6.1.1165 |                |                |              |
   +----------------+----------------+----------------+--------------+
   | 1.2.840.       |                |                |              |
   | 10008.6.1.1166 |                |                |              |
   +----------------+----------------+----------------+--------------+
   | 1.2.840.       |                |                |              |
   | 10008.6.1.1167 |                |                |              |
   +----------------+----------------+----------------+--------------+
   | 1.2.840.       |                |                |              |
   | 10008.6.1.1168 |                |                |              |
   +----------------+----------------+----------------+--------------+
   | 1.2.840.       |                |                |              |
   | 10008.6.1.1169 |                |                |              |
   +----------------+----------------+----------------+--------------+
   | 1.2.840.       |                |                |              |
   | 10008.6.1.1170 |                |                |              |
   +----------------+----------------+----------------+--------------+
   | 1.2.840.       |                |                |              |
   | 10008.6.1.1171 |                |                |              |
   +----------------+----------------+----------------+--------------+
   | 1.2.840.       |                |                |              |
   | 10008.6.1.1172 |                |                |              |
   +----------------+----------------+----------------+--------------+
   | 1.2.840.       |                |                |              |
   | 10008.6.1.1173 |                |                |              |
   +----------------+----------------+----------------+--------------+
   | 1.2.840.       |                |                |              |
   | 10008.6.1.1174 |                |                |              |
   +----------------+----------------+----------------+--------------+
   | 1.2.840.       |                |                |              |
   | 10008.6.1.1175 |                |                |              |
   +----------------+----------------+----------------+--------------+
   | 1.2.840.       |                |                |              |
   | 10008.6.1.1176 |                |                |              |
   +----------------+----------------+----------------+--------------+
   | 1.2.840.       |                |                |              |
   | 10008.6.1.1177 |                |                |              |
   +----------------+----------------+----------------+--------------+
   | 1.2.840.       |                |                |              |
   | 10008.6.1.1178 |                |                |              |
   +----------------+----------------+----------------+--------------+
   | 1.2.840.       |                |                |              |
   | 10008.6.1.1179 |                |                |              |
   +----------------+----------------+----------------+--------------+
   | 1.2.840.       |                |                |              |
   | 10008.6.1.1180 |                |                |              |
   +----------------+----------------+----------------+--------------+
   | 1.2.840.       |                |                |              |
   | 10008.6.1.1181 |                |                |              |
   +----------------+----------------+----------------+--------------+
   | 1.2.840.       |                |                |              |
   | 10008.6.1.1182 |                |                |              |
   +----------------+----------------+----------------+--------------+
   | 1.2.840.       |                |                |              |
   | 10008.6.1.1183 |                |                |              |
   +----------------+----------------+----------------+--------------+
   | 1.2.840.       |                |                |              |
   | 10008.6.1.1184 |                |                |              |
   +----------------+----------------+----------------+--------------+
   | 1.2.840.       |                |                |              |
   | 10008.6.1.1185 |                |                |              |
   +----------------+----------------+----------------+--------------+
   | 1.2.840.       |                |                |              |
   | 10008.6.1.1186 |                |                |              |
   +----------------+----------------+----------------+--------------+
   | 1.2.840.       |                |                |              |
   | 10008.6.1.1187 |                |                |              |
   +----------------+----------------+----------------+--------------+
   | 1.2.840.       |                |                |              |
   | 10008.6.1.1188 |                |                |              |
   +----------------+----------------+----------------+--------------+
   | 1.2.840.       |                |                |              |
   | 10008.6.1.1189 |                |                |              |
   +----------------+----------------+----------------+--------------+
   | 1.2.840.       |                |                |              |
   | 10008.6.1.1190 |                |                |              |
   +----------------+----------------+----------------+--------------+
   | 1.2.840.       |                |                |              |
   | 10008.6.1.1191 |                |                |              |
   +----------------+----------------+----------------+--------------+
   | 1.2.840.       |                |                |              |
   | 10008.6.1.1192 |                |                |              |
   +----------------+----------------+----------------+--------------+
   | 1.2.840.       |                |                |              |
   | 10008.6.1.1193 |                |                |              |
   +----------------+----------------+----------------+--------------+
   | 1.2.840.       |                |                |              |
   | 10008.6.1.1194 |                |                |              |
   +----------------+----------------+----------------+--------------+
   | 1.2.840.       |                |                |              |
   | 10008.6.1.1195 |                |                |              |
   +----------------+----------------+----------------+--------------+
   | 1.2.840.       |                |                |              |
   | 10008.6.1.1196 |                |                |              |
   +----------------+----------------+----------------+--------------+
   | 1.2.840.       |                |                |              |
   | 10008.6.1.1197 |                |                |              |
   +----------------+----------------+----------------+--------------+
   | 1.2.840.       |                |                |              |
   | 10008.6.1.1198 |                |                |              |
   +----------------+----------------+----------------+--------------+
   | 1.2.840.       |                |                |              |
   | 10008.6.1.1199 |                |                |              |
   +----------------+----------------+----------------+--------------+
   | 1.2.840.       |                |                |              |
   | 10008.6.1.1200 |                |                |              |
   +----------------+----------------+----------------+--------------+
   | 1.2.840.       |                |                |              |
   | 10008.6.1.1201 |                |                |              |
   +----------------+----------------+----------------+--------------+
   | 1.2.840.       |                |                |              |
   | 10008.6.1.1202 |                |                |              |
   +----------------+----------------+----------------+--------------+
   | 1.2.840.       |                |                |              |
   | 10008.6.1.1203 |                |                |              |
   +----------------+----------------+----------------+--------------+
   | 1.2.840.       |                |                |              |
   | 10008.6.1.1204 |                |                |              |
   +----------------+----------------+----------------+--------------+
   | 1.2.840.       |                |                |              |
   | 10008.6.1.1205 |                |                |              |
   +----------------+----------------+----------------+--------------+
   | 1.2.840.       |                |                |              |
   | 10008.6.1.1206 |                |                |              |
   +----------------+----------------+----------------+--------------+
   | 1.2.840.       |                |                |              |
   | 10008.6.1.1207 |                |                |              |
   +----------------+----------------+----------------+--------------+
   | 1.2.840.       |                |                |              |
   | 10008.6.1.1208 |                |                |              |
   +----------------+----------------+----------------+--------------+
   | 1.2.840.       |                |                |              |
   | 10008.6.1.1209 |                |                |              |
   +----------------+----------------+----------------+--------------+
   | 1.2.840.       |                |                |              |
   | 10008.6.1.1210 |                |                |              |
   +----------------+----------------+----------------+--------------+
   | 1.2.840.       |                |                |              |
   | 10008.6.1.1211 |                |                |              |
   +----------------+----------------+----------------+--------------+
   | 1.2.840.       |                |                |              |
   | 10008.6.1.1212 |                |                |              |
   +----------------+----------------+----------------+--------------+
   | 1.2.840.       |                |                |              |
   | 10008.6.1.1213 |                |                |              |
   +----------------+----------------+----------------+--------------+
   | 1.2.840.       |                |                |              |
   | 10008.6.1.1214 |                |                |              |
   +----------------+----------------+----------------+--------------+
   | 1.2.840.       |                |                |              |
   | 10008.6.1.1215 |                |                |              |
   +----------------+----------------+----------------+--------------+
   | 1.2.840.       |                |                |              |
   | 10008.6.1.1216 |                |                |              |
   +----------------+----------------+----------------+--------------+
   | 1.2.840.       |                |                |              |
   | 10008.6.1.1217 |                |                |              |
   +----------------+----------------+----------------+--------------+
   | 1.2.840.       |                |                |              |
   | 10008.6.1.1218 |                |                |              |
   +----------------+----------------+----------------+--------------+
   | 1.2.840.       |                |                |              |
   | 10008.6.1.1219 |                |                |              |
   +----------------+----------------+----------------+--------------+
   | 1.2.840.       |                |                |              |
   | 10008.6.1.1220 |                |                |              |
   +----------------+----------------+----------------+--------------+
   | 1.2.840.       |                |                |              |
   | 10008.6.1.1221 |                |                |              |
   +----------------+----------------+----------------+--------------+
   | 1.2.840.       |                |                |              |
   | 10008.6.1.1222 |                |                |              |
   +----------------+----------------+----------------+--------------+
   | 1.2.840.       |                |                |              |
   | 10008.6.1.1223 |                |                |              |
   +----------------+----------------+----------------+--------------+
   | 1.2.840.       |                |                |              |
   | 10008.6.1.1224 |                |                |              |
   +----------------+----------------+----------------+--------------+
   | 1.2.840.       |                |                |              |
   | 10008.6.1.1225 |                |                |              |
   +----------------+----------------+----------------+--------------+
   | 1.2.840.       |                |                |              |
   | 10008.6.1.1226 |                |                |              |
   +----------------+----------------+----------------+--------------+
   | 1.2.840.       |                |                |              |
   | 10008.6.1.1227 |                |                |              |
   +----------------+----------------+----------------+--------------+
   | 1.2.840.       |                |                |              |
   | 10008.6.1.1228 |                |                |              |
   +----------------+----------------+----------------+--------------+
   | 1.2.840.       |                |                |              |
   | 10008.6.1.1229 |                |                |              |
   +----------------+----------------+----------------+--------------+
   | 1.2.840.       |                |                |              |
   | 10008.6.1.1230 |                |                |              |
   +----------------+----------------+----------------+--------------+
   | 1.2.840.       |                |                |              |
   | 10008.6.1.1231 |                |                |              |
   +----------------+----------------+----------------+--------------+
   | 1.2.840.       |                |                |              |
   | 10008.6.1.1232 |                |                |              |
   +----------------+----------------+----------------+--------------+
   | 1.2.840.       |                |                |              |
   | 10008.6.1.1233 |                |                |              |
   +----------------+----------------+----------------+--------------+
   | 1.2.840.       |                |                |              |
   | 10008.6.1.1234 |                |                |              |
   +----------------+----------------+----------------+--------------+
   | 1.2.840.       |                |                |              |
   | 10008.6.1.1235 |                |                |              |
   +----------------+----------------+----------------+--------------+
   | 1.2.840.       |                |                |              |
   | 10008.6.1.1236 |                |                |              |
   +----------------+----------------+----------------+--------------+
   | 1.2.840.       |                |                |              |
   | 10008.6.1.1237 |                |                |              |
   +----------------+----------------+----------------+--------------+
   | 1.2.840.       |                |                |              |
   | 10008.6.1.1238 |                |                |              |
   +----------------+----------------+----------------+--------------+
   | 1.2.840.       |                |                |              |
   | 10008.6.1.1239 |                |                |              |
   +----------------+----------------+----------------+--------------+
   | 1.2.840.       |                |                |              |
   | 10008.6.1.1240 |                |                |              |
   +----------------+----------------+----------------+--------------+
   | 1.2.840.       |                |                |              |
   | 10008.6.1.1241 |                |                |              |
   +----------------+----------------+----------------+--------------+
   | 1.2.840.       |                |                |              |
   | 10008.6.1.1242 |                |                |              |
   +----------------+----------------+----------------+--------------+
   | 1.2.840.       |                |                |              |
   | 10008.6.1.1243 |                |                |              |
   +----------------+----------------+----------------+--------------+
   | 1.2.840.       |                |                |              |
   | 10008.6.1.1244 |                |                |              |
   +----------------+----------------+----------------+--------------+
   | 1.2.840.       |                |                |              |
   | 10008.6.1.1245 |                |                |              |
   +----------------+----------------+----------------+--------------+
   | 1.2.840.       |                |                |              |
   | 10008.6.1.1246 |                |                |              |
   +----------------+----------------+----------------+--------------+
   | 1.2.840.       |                |                |              |
   | 10008.6.1.1247 |                |                |              |
   +----------------+----------------+----------------+--------------+
   | 1.2.840.       |                |                |              |
   | 10008.6.1.1248 |                |                |              |
   +----------------+----------------+----------------+--------------+
   | 1.2.840.       |                |                |              |
   | 10008.6.1.1249 |                |                |              |
   +----------------+----------------+----------------+--------------+
   | 1.2.840.       |                |                |              |
   | 10008.6.1.1250 |                |                |              |
   +----------------+----------------+----------------+--------------+
   | 1.2.840.       |                |                |              |
   | 10008.6.1.1251 |                |                |              |
   +----------------+----------------+----------------+--------------+
   | 1.2.840.       |                |                |              |
   | 10008.6.1.1252 |                |                |              |
   +----------------+----------------+----------------+--------------+
   | 1.2.840.       |                |                |              |
   | 10008.6.1.1253 |                |                |              |
   +----------------+----------------+----------------+--------------+
   | 1.2.840.       |                |                |              |
   | 10008.6.1.1254 |                |                |              |
   +----------------+----------------+----------------+--------------+
   | 1.2.840.       |                |                |              |
   | 10008.6.1.1255 |                |                |              |
   +----------------+----------------+----------------+--------------+
   | 1.2.840.       |                |                |              |
   | 10008.6.1.1256 |                |                |              |
   +----------------+----------------+----------------+--------------+
   | 1.2.840.       |                |                |              |
   | 10008.6.1.1257 |                |                |              |
   +----------------+----------------+----------------+--------------+
   | 1.2.840.       |                |                |              |
   | 10008.6.1.1258 |                |                |              |
   +----------------+----------------+----------------+--------------+
   | 1.2.840.       |                |                |              |
   | 10008.6.1.1259 |                |                |              |
   +----------------+----------------+----------------+--------------+
   | 1.2.840.       |                |                |              |
   | 10008.6.1.1260 |                |                |              |
   +----------------+----------------+----------------+--------------+
   | 1.2.840.       |                |                |              |
   | 10008.6.1.1261 |                |                |              |
   +----------------+----------------+----------------+--------------+
   | 1.2.840.       |                |                |              |
   | 10008.6.1.1262 |                |                |              |
   +----------------+----------------+----------------+--------------+
   | 1.2.840.       |                |                |              |
   | 10008.6.1.1263 |                |                |              |
   +----------------+----------------+----------------+--------------+
   | 1.2.840.       |                |                |              |
   | 10008.6.1.1264 |                |                |              |
   +----------------+----------------+----------------+--------------+
   | 1.2.840.       |                |                |              |
   | 10008.6.1.1265 |                |                |              |
   +----------------+----------------+----------------+--------------+
   | 1.2.840.       |                |                |              |
   | 10008.6.1.1266 |                |                |              |
   +----------------+----------------+----------------+--------------+
   | 1.2.840.       |                |                |              |
   | 10008.6.1.1267 |                |                |              |
   +----------------+----------------+----------------+--------------+
   | 1.2.840.       |                |                |              |
   | 10008.6.1.1268 |                |                |              |
   +----------------+----------------+----------------+--------------+
   | 1.2.840.       |                |                |              |
   | 10008.6.1.1269 |                |                |              |
   +----------------+----------------+----------------+--------------+
   | 1.2.840.       |                |                |              |
   | 10008.6.1.1270 |                |                |              |
   +----------------+----------------+----------------+--------------+
   | 1.2.840.       |                |                |              |
   | 10008.6.1.1271 |                |                |              |
   +----------------+----------------+----------------+--------------+
   | 1.2.840.       |                |                |              |
   | 10008.6.1.1272 |                |                |              |
   +----------------+----------------+----------------+--------------+
   | 1.2.840.       |                |                |              |
   | 10008.6.1.1273 |                |                |              |
   +----------------+----------------+----------------+--------------+
   | 1.2.840.       |                |                |              |
   | 10008.6.1.1274 |                |                |              |
   +----------------+----------------+----------------+--------------+
   | 1.2.840.       |                |                |              |
   | 10008.6.1.1275 |                |                |              |
   +----------------+----------------+----------------+--------------+
   | 1.2.840.       |                |                |              |
   | 10008.6.1.1276 |                |                |              |
   +----------------+----------------+----------------+--------------+
   | 1.2.840.       |                |                |              |
   | 10008.6.1.1277 |                |                |              |
   +----------------+----------------+----------------+--------------+
   | 1.2.840.       |                |                |              |
   | 10008.6.1.1278 |                |                |              |
   +----------------+----------------+----------------+--------------+
   | 1.2.840.       |                |                |              |
   | 10008.6.1.1279 |                |                |              |
   +----------------+----------------+----------------+--------------+
   | 1.2.840.       |                |                |              |
   | 10008.6.1.1280 |                |                |              |
   +----------------+----------------+----------------+--------------+
   | 1.2.840.       |                |                |              |
   | 10008.6.1.1281 |                |                |              |
   +----------------+----------------+----------------+--------------+
   | 1.2.840.       |                |                |              |
   | 10008.6.1.1282 |                |                |              |
   +----------------+----------------+----------------+--------------+
   | 1.2.840.       |                |                |              |
   | 10008.6.1.1283 |                |                |              |
   +----------------+----------------+----------------+--------------+
   | 1.2.840.       |                |                |              |
   | 10008.6.1.1284 |                |                |              |
   +----------------+----------------+----------------+--------------+
   | 1.2.840.       |                |                |              |
   | 10008.6.1.1285 |                |                |              |
   +----------------+----------------+----------------+--------------+
   | 1.2.840.       |                |                |              |
   | 10008.6.1.1286 |                |                |              |
   +----------------+----------------+----------------+--------------+
   | 1.2.840.       |                |                |              |
   | 10008.6.1.1287 |                |                |              |
   +----------------+----------------+----------------+--------------+
   | 1.2.840.       |                |                |              |
   | 10008.6.1.1288 |                |                |              |
   +----------------+----------------+----------------+--------------+
   | 1.2.840.       |                |                |              |
   | 10008.6.1.1289 |                |                |              |
   +----------------+----------------+----------------+--------------+
   | 1.2.840.       |                |                |              |
   | 10008.6.1.1290 |                |                |              |
   +----------------+----------------+----------------+--------------+
   | 1.2.840.       |                |                |              |
   | 10008.6.1.1291 |                |                |              |
   +----------------+----------------+----------------+--------------+
   | 1.2.840.       |                |                |              |
   | 10008.6.1.1292 |                |                |              |
   +----------------+----------------+----------------+--------------+
   | 1.2.840.       |                |                |              |
   | 10008.6.1.1293 |                |                |              |
   +----------------+----------------+----------------+--------------+
   | 1.2.840.       |                |                |              |
   | 10008.6.1.1294 |                |                |              |
   +----------------+----------------+----------------+--------------+
   | 1.2.840.       |                |                |              |
   | 10008.6.1.1295 |                |                |              |
   +----------------+----------------+----------------+--------------+
   | 1.2.840.       |                |                |              |
   | 10008.6.1.1296 |                |                |              |
   +----------------+----------------+----------------+--------------+
   | 1.2.840.       |                |                |              |
   | 10008.6.1.1297 |                |                |              |
   +----------------+----------------+----------------+--------------+
   | 1.2.840.       |                |                |              |
   | 10008.6.1.1298 |                |                |              |
   +----------------+----------------+----------------+--------------+
   | 1.2.840.       |                |                |              |
   | 10008.6.1.1299 |                |                |              |
   +----------------+----------------+----------------+--------------+
   | 1.2.840.       |                |                |              |
   | 10008.6.1.1300 |                |                |              |
   +----------------+----------------+----------------+--------------+
   | 1.2.840.       |                |                |              |
   | 10008.6.1.1301 |                |                |              |
   +----------------+----------------+----------------+--------------+
   | 1.2.840.       |                |                |              |
   | 10008.6.1.1302 |                |                |              |
   +----------------+----------------+----------------+--------------+
   | 1.2.840.       |                |                |              |
   | 10008.6.1.1303 |                |                |              |
   +----------------+----------------+----------------+--------------+
   | 1.2.840.       |                |                |              |
   | 10008.6.1.1304 |                |                |              |
   +----------------+----------------+----------------+--------------+
   | 1.2.840.       |                |                |              |
   | 10008.6.1.1305 |                |                |              |
   +----------------+----------------+----------------+--------------+
   | 1.2.840.10     |                |                |              |
   | 008.6.​1.​1306 |                |                |              |
   +----------------+----------------+----------------+--------------+
   | 1.2.840.10     |                |                |              |
   | 008.6.​1.​1307 |                |                |              |
   +----------------+----------------+----------------+--------------+
   | 1.2.840.10     |                |                |              |
   | 008.6.​1.​1308 |                |                |              |
   +----------------+----------------+----------------+--------------+
   | 1.2.840.10     |                |                |              |
   | 008.6.​1.​1309 |                |                |              |
   +----------------+----------------+----------------+--------------+
   | 1.2.840.10     |                |                |              |
   | 008.6.​1.​1310 |                |                |              |
   +----------------+----------------+----------------+--------------+
   | 1.2.840.10     |                |                |              |
   | 008.6.​1.​1311 |                |                |              |
   +----------------+----------------+----------------+--------------+
   | 1.2.840.10     |                |                |              |
   | 008.6.​1.​1312 |                |                |              |
   +----------------+----------------+----------------+--------------+
   | 1.2.840.10     |                |                |              |
   | 008.6.​1.​1313 |                |                |              |
   +----------------+----------------+----------------+--------------+
   | 1.2.840.10     |                |                |              |
   | 008.6.​1.​1314 |                |                |              |
   +----------------+----------------+----------------+--------------+
   | 1.2.840.1      |                |                |              |
   | 0008.6.​1.1315 |                |                |              |
   +----------------+----------------+----------------+--------------+
   | 1.2.840.1      |                |                |              |
   | 0008.6.​1.1316 |                |                |              |
   +----------------+----------------+----------------+--------------+
   | 1.2.840.1      |                |                |              |
   | 0008.6.​1.1317 |                |                |              |
   +----------------+----------------+----------------+--------------+
   | 1.2.840.       |                |                |              |
   | 10008.6.1.1318 |                |                |              |
   +----------------+----------------+----------------+--------------+
   | 1.2.840.       |                |                |              |
   | 10008.6.1.1319 |                |                |              |
   +----------------+----------------+----------------+--------------+
   | 1.2.840.       |                |                |              |
   | 10008.6.1.1320 |                |                |              |
   +----------------+----------------+----------------+--------------+
   | 1.2.840.       |                |                |              |
   | 10008.6.1.1321 |                |                |              |
   +----------------+----------------+----------------+--------------+
   | 1.2.840.       |                |                |              |
   | 10008.6.1.1322 |                |                |              |
   +----------------+----------------+----------------+--------------+
   | 1.2.840.       |                |                |              |
   | 10008.6.1.1323 |                |                |              |
   +----------------+----------------+----------------+--------------+
   | 1.2.840.       |                |                |              |
   | 10008.6.1.1324 |                |                |              |
   +----------------+----------------+----------------+--------------+
   | 1.2.840.       |                |                |              |
   | 10008.6.1.1325 |                |                |              |
   +----------------+----------------+----------------+--------------+
   | 1.2.840.       |                |                |              |
   | 10008.6.1.1326 |                |                |              |
   +----------------+----------------+----------------+--------------+
   | 1.2.840.       |                |                |              |
   | 10008.6.1.1327 |                |                |              |
   +----------------+----------------+----------------+--------------+
   | 1.2.840.       |                |                |              |
   | 10008.6.1.1328 |                |                |              |
   +----------------+----------------+----------------+--------------+
   | 1.2.840.       |                |                |              |
   | 10008.6.1.1329 |                |                |              |
   +----------------+----------------+----------------+--------------+
   | 1.2.840.       |                |                |              |
   | 10008.6.1.1330 |                |                |              |
   +----------------+----------------+----------------+--------------+
   | 1.2.840.       |                |                |              |
   | 10008.6.1.1331 |                |                |              |
   +----------------+----------------+----------------+--------------+
   | 1.2.840.       |                |                |              |
   | 10008.6.1.1332 |                |                |              |
   +----------------+----------------+----------------+--------------+
   | 1.2.840.       |                |                |              |
   | 10008.6.1.1333 |                |                |              |
   +----------------+----------------+----------------+--------------+
   | 1.2.840.       |                |                |              |
   | 10008.6.1.1334 |                |                |              |
   +----------------+----------------+----------------+--------------+
   | 1.2.840.       |                |                |              |
   | 10008.6.1.1335 |                |                |              |
   +----------------+----------------+----------------+--------------+
   | 1.2.840.       |                |                |              |
   | 10008.6.1.1336 |                |                |              |
   +----------------+----------------+----------------+--------------+
   | 1.2.840.       |                |                |              |
   | 10008.6.1.1337 |                |                |              |
   +----------------+----------------+----------------+--------------+
   | 1.2.840.       |                |                |              |
   | 10008.6.1.1338 |                |                |              |
   +----------------+----------------+----------------+--------------+
   | 1.2.840.1      |                |                |              |
   | 0008.6.​1.1339 |                |                |              |
   +----------------+----------------+----------------+--------------+
   | 1.2.840.1      |                |                |              |
   | 0008.6.​1.1340 |                |                |              |
   +----------------+----------------+----------------+--------------+
   | 1.2.840.1      |                |                |              |
   | 0008.6.​1.1341 |                |                |              |
   +----------------+----------------+----------------+--------------+

.. note::

   For some Context Group UIDs, no Context Group Name or Identifier is
   specified; these are "placeholders" that are not assigned but will
   not be reused.

.. table:: Template UID Values

   ================== ======== ====================== ====
   UID Value          UID Name UID Type               Part
   ================== ======== ====================== ====
   1.2.840.10008.9.1           Document TemplateID    
   1.2.840.10008.9.2           Section TemplateID     
   1.2.840.10008.9.3           Section TemplateID     
   1.2.840.10008.9.4           Section TemplateID     
   1.2.840.10008.9.5           Section TemplateID     
   1.2.840.10008.9.6           Section TemplateID     
   1.2.840.10008.9.7           Section TemplateID     
   1.2.840.10008.9.8           Section TemplateID     
   1.2.840.10008.9.9           Section TemplateID     
   1.2.840.10008.9.10          Section TemplateID     
   1.2.840.10008.9.11          Section TemplateID     
   1.2.840.10008.9.12          Section TemplateID     
   1.2.840.10008.9.13          Entry TemplateID       
   1.2.840.10008.9.14          Entry TemplateID       
   1.2.840.10008.9.15          Entry TemplateID       
   1.2.840.10008.9.16          Entry TemplateID       
   1.2.840.10008.9.17          Entry TemplateID       
   1.2.840.10008.9.18          Entry TemplateID       
   1.2.840.10008.9.19          Element Set TemplateID 
   1.2.840.10008.9.20          Element Set TemplateID 
   1.2.840.10008.9.21          Element Set TemplateID 
   1.2.840.10008.9.22          Element Set TemplateID 
   1.2.840.10008.9.23          Element Set TemplateID 
   1.2.840.10008.9.24          Document TemplateID    
   ================== ======== ====================== ====

