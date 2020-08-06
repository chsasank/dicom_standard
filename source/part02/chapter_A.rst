.. _chapter_A:

DICOM Conformance Statement Template (Normative)
================================================

This Annex is a template that shall be used to generate a DICOM
Conformance Statement. The document is hierarchically structured in
three different levels:

-  A DICOM Conformance Statement Overview, which is typically one page,
   geared towards people that want to get a quick overview of the
   functionality and services.

-  For Networking and Media, the relationship between the AEs, followed
   by the information for each AE

-  For the services supported as SCU and SCP all the SOP specific
   details

Annexes are provided to specify the Object descriptions (IODs), with
specifics about the field usage as well as the data dictionaries.

.. note::

   The numbering scheme for numbering paragraphs in this document is to
   be used as a guideline in preparing the outline of the Conformance
   Statement. Although strongly encouraged, the Conformance Statement is
   not required to have exactly the same paragraph numbers because a
   particular Conformance Statement might have special considerations,
   which will cause the outline to differ in certain details from the
   outline of this document. In addition, a vendor might have internal
   company guidelines prescribing a specific format. Note however, that
   the overall structure, tables, definition of variables and
   information such as headers, should be strictly followed.

.. _sect_A.0:

Cover Page
----------

A DICOM Conformance Statement may have a cover page, which, if present,
shall include:

a. The commercial name and version(s) of the concerned product or
   products (if applicable to several products) including all optional
   features. The product version shall correspond to the functionality
   as described in this conformance statement.

b. Date of the document

.. _sect_A.1:

Conformance Statement Overview
------------------------------

The Overview consist of typically 5-10 lines describing the network
services and media storage capabilities supported by the product in
layman's terms (i.e., no DICOM acronyms should be used).

A table of Supported Networking DICOM Service (SOP) Classes is provided
with roles (User/Provider), organized in 4 categories:

-  Transfer

-  Query/Retrieve

-  Workflow Management

-  Print Management

The first column shall specify the SOP Classes exactly as named in .,
Registry of DICOM Unique Identifiers. The phrase "and specializations"
may be added to indicate support of all specializations negotiated
through the SOP Class Common Extended Negotiation. If the implementation
supports all SOP Classes of a particular Service Class through SOP Class
Common Extended Negotiation, the first column shall specify "All
services of the <x> Service Class".

.. table:: Network Services

   +----------------------+----------------------+----------------------+
   | SOP Classes          | User of Service      | Provider of Service  |
   |                      | (SCU)                | (SCP)                |
   +======================+======================+======================+
   | Transfer             |                      |                      |
   +----------------------+----------------------+----------------------+
   | CT Image Storage     | Yes                  | No                   |
   +----------------------+----------------------+----------------------+
   | US Image Storage     | Yes                  | Yes                  |
   +----------------------+----------------------+----------------------+
   | Query/Retrieve       |                      |                      |
   +----------------------+----------------------+----------------------+
   | Patient Root         | Option               | No                   |
   | Information Model    |                      |                      |
   | FIND                 |                      |                      |
   +----------------------+----------------------+----------------------+
   | Notes, Reports,      |                      |                      |
   | Measurements         |                      |                      |
   | Transfer             |                      |                      |
   +----------------------+----------------------+----------------------+
   | Comprehensive SR,    | No                   | Yes                  |
   | and specializations  |                      |                      |
   +----------------------+----------------------+----------------------+
   | …                    |                      |                      |
   +----------------------+----------------------+----------------------+

The services can be specified as a SCU, SCP or as an Option, which means
that it is either configurable or that it can be purchased separately.

.. note::

   Verification SCP (C-Echo) is not included in the table above because
   it is required for any Acceptor of an Association. The Verification
   SCU details are covered in the details of the conformance statement.

The SOP Classes are categorized as follows:

.. table:: UID Values

   +----------------------+----------------------+----------------------+
   | UID Value            | UID Name             | Category             |
   +======================+======================+======================+
   | 1.2.840.10008.1.20.1 | Storage Commitment   | Workflow Management  |
   |                      | Push Model SOP Class |                      |
   +----------------------+----------------------+----------------------+
   | 1.2.840.10008.1.40   | Procedural Event     | Workflow Management  |
   |                      | Logging SOP Class    |                      |
   +----------------------+----------------------+----------------------+
   | 1.2.840.10008.1.42   | Substance            | Workflow Management  |
   |                      | Administration       |                      |
   |                      | Logging SOP Class    |                      |
   +----------------------+----------------------+----------------------+
   | 1.­2                 | Modality Performed   | Workflow Management  |
   | .840.10008.3.1.2.3.3 | Procedure Step SOP   |                      |
   |                      | Class                |                      |
   +----------------------+----------------------+----------------------+
   | 1.­2                 | Modality Performed   | Workflow Management  |
   | .840.10008.3.1.2.3.4 | Procedure Step       |                      |
   |                      | Retrieve SOP Class   |                      |
   +----------------------+----------------------+----------------------+
   | 1.­2                 | Modality Performed   | Workflow Management  |
   | .840.10008.3.1.2.3.5 | Procedure Step       |                      |
   |                      | Notification SOP     |                      |
   |                      | Class                |                      |
   +----------------------+----------------------+----------------------+
   | 1.2.840.10008.4.2    | Storage Service      | Transfer             |
   |                      | Class                |                      |
   +----------------------+----------------------+----------------------+
   | 1                    | Basic Film Session   | Print Management     |
   | .2.840.10008.5.1.1.1 | SOP Class            |                      |
   +----------------------+----------------------+----------------------+
   | 1                    | Basic Film Box SOP   | Print Management     |
   | .2.840.10008.5.1.1.2 | Class                |                      |
   +----------------------+----------------------+----------------------+
   | 1                    | Basic Grayscale      | Print Management     |
   | .2.840.10008.5.1.1.4 | Image Box SOP Class  |                      |
   +----------------------+----------------------+----------------------+
   | 1.2                  | Basic Color Image    | Print Management     |
   | .840.10008.5.1.1.4.1 | Box SOP Class        |                      |
   +----------------------+----------------------+----------------------+
   | 1                    | Basic Grayscale      | Print Management     |
   | .2.840.10008.5.1.1.9 | Print Management     |                      |
   |                      | Meta SOP Class       |                      |
   +----------------------+----------------------+----------------------+
   | 1.                   | Print Job SOP Class  | Print Management     |
   | 2.840.10008.5.1.1.14 |                      |                      |
   +----------------------+----------------------+----------------------+
   | 1.                   | Basic Annotation Box | Print Management     |
   | 2.840.10008.5.1.1.15 | SOP Class            |                      |
   +----------------------+----------------------+----------------------+
   | 1.                   | Printer SOP Class    | Print Management     |
   | 2.840.10008.5.1.1.16 |                      |                      |
   +----------------------+----------------------+----------------------+
   | 1.2.84               | Printer              | Print Management     |
   | 0.10008.5.1.1.16.376 | Configuration        |                      |
   |                      | Retrieval SOP Class  |                      |
   +----------------------+----------------------+----------------------+
   | 1.                   | Basic Color Print    | Print Management     |
   | 2.840.10008.5.1.1.18 | Management Meta SOP  |                      |
   |                      | Class                |                      |
   +----------------------+----------------------+----------------------+
   | 1.                   | Presentation LUT SOP | Print Management     |
   | 2.840.10008.5.1.1.23 | Class                |                      |
   +----------------------+----------------------+----------------------+
   | 1.2.                 | Basic Print Image    | Print Management     |
   | 840.10008.5.1.1.24.1 | Overlay Box SOP      |                      |
   |                      | Class                |                      |
   +----------------------+----------------------+----------------------+
   | 1.                   | Media Creation       | Print Management     |
   | 2.840.10008.5.1.1.33 | Management SOP Class |                      |
   +----------------------+----------------------+----------------------+
   | 1.2.8                | Computed Radiography | Transfer             |
   | 40.10008.5.1.4.1.1.1 | Image Storage SOP    |                      |
   |                      | Class                |                      |
   +----------------------+----------------------+----------------------+
   | 1.2.840              | Digital X-Ray Image  | Transfer             |
   | .10008.5.1.4.1.1.1.1 | Storage - For        |                      |
   |                      | Presentation SOP     |                      |
   |                      | Class                |                      |
   +----------------------+----------------------+----------------------+
   | 1.2.840.1            | Digital X-Ray Image  | Transfer             |
   | 0008.5.1.4.1.1.1.1.1 | Storage - For        |                      |
   |                      | Processing SOP Class |                      |
   +----------------------+----------------------+----------------------+
   | 1.2.840              | Digital Mammography  | Transfer             |
   | .10008.5.1.4.1.1.1.2 | X-Ray Image Storage  |                      |
   |                      | - For Presentation   |                      |
   |                      | SOP Class            |                      |
   +----------------------+----------------------+----------------------+
   | 1.2.840.1            | Digital Mammography  | Transfer             |
   | 0008.5.1.4.1.1.1.2.1 | X-Ray Image Storage  |                      |
   |                      | - For Processing SOP |                      |
   |                      | Class                |                      |
   +----------------------+----------------------+----------------------+
   | 1.2.840              | Digital Intra-oral   | Transfer             |
   | .10008.5.1.4.1.1.1.3 | X-Ray Image Storage  |                      |
   |                      | - For Presentation   |                      |
   |                      | SOP Class            |                      |
   +----------------------+----------------------+----------------------+
   | 1.2.840.1            | Digital Intra-oral   | Transfer             |
   | 0008.5.1.4.1.1.1.3.1 | X-Ray Image Storage  |                      |
   |                      | - For Processing SOP |                      |
   |                      | Class                |                      |
   +----------------------+----------------------+----------------------+
   | 1.2.8                | CT Image Storage SOP | Transfer             |
   | 40.10008.5.1.4.1.1.2 | Class                |                      |
   +----------------------+----------------------+----------------------+
   | 1.2.840              | Enhanced CT Image    | Transfer             |
   | .10008.5.1.4.1.1.2.1 | Storage SOP Class    |                      |
   +----------------------+----------------------+----------------------+
   | 1.2.840              | Ultrasound           | Transfer             |
   | .10008.5.1.4.1.1.3.1 | Multi-frame Image    |                      |
   |                      | Storage SOP Class    |                      |
   +----------------------+----------------------+----------------------+
   | 1.2.8                | MR Image Storage SOP | Transfer             |
   | 40.10008.5.1.4.1.1.4 | Class                |                      |
   +----------------------+----------------------+----------------------+
   | 1.2.840              | Enhanced MR Image    | Transfer             |
   | .10008.5.1.4.1.1.4.1 | Storage SOP Class    |                      |
   +----------------------+----------------------+----------------------+
   | 1.2.840              | MR Spectroscopy      | Transfer             |
   | .10008.5.1.4.1.1.4.2 | Storage SOP Class    |                      |
   +----------------------+----------------------+----------------------+
   | 1.2.840              | Enhanced MR Color    | Transfer             |
   | .10008.5.1.4.1.1.4.3 | Image Storage SOP    |                      |
   |                      | Class                |                      |
   +----------------------+----------------------+----------------------+
   | 1.2.840              | Ultrasound Image     | Transfer             |
   | .10008.5.1.4.1.1.6.1 | Storage SOP Class    |                      |
   +----------------------+----------------------+----------------------+
   | 1.2.840              | Enhanced US Volume   | Transfer             |
   | .10008.5.1.4.1.1.6.2 | Storage SOP Class    |                      |
   +----------------------+----------------------+----------------------+
   | 1.2.8                | Secondary Capture    | Transfer             |
   | 40.10008.5.1.4.1.1.7 | Image Storage SOP    |                      |
   |                      | Class                |                      |
   +----------------------+----------------------+----------------------+
   | 1.2.840              | Multi-frame Single   | Transfer             |
   | .10008.5.1.4.1.1.7.1 | Bit Secondary        |                      |
   |                      | Capture Image        |                      |
   |                      | Storage SOP Class    |                      |
   +----------------------+----------------------+----------------------+
   | 1.2.840              | Multi-frame          | Transfer             |
   | .10008.5.1.4.1.1.7.2 | Grayscale Byte       |                      |
   |                      | Secondary Capture    |                      |
   |                      | Image Storage SOP    |                      |
   |                      | Class                |                      |
   +----------------------+----------------------+----------------------+
   | 1.2.840              | Multi-frame          | Transfer             |
   | .10008.5.1.4.1.1.7.3 | Grayscale Word       |                      |
   |                      | Secondary Capture    |                      |
   |                      | Image Storage SOP    |                      |
   |                      | Class                |                      |
   +----------------------+----------------------+----------------------+
   | 1.2.840              | Multi-frame True     | Transfer             |
   | .10008.5.1.4.1.1.7.4 | Color Secondary      |                      |
   |                      | Capture Image        |                      |
   |                      | Storage SOP Class    |                      |
   +----------------------+----------------------+----------------------+
   | 1.2.840.1            | 12-lead ECG Waveform | Transfer             |
   | 0008.5.1.4.1.1.9.1.1 | Storage SOP Class    |                      |
   +----------------------+----------------------+----------------------+
   | 1.2.840.1            | General ECG Waveform | Transfer             |
   | 0008.5.1.4.1.1.9.1.2 | Storage SOP Class    |                      |
   +----------------------+----------------------+----------------------+
   | 1.2.840.1            | Ambulatory ECG       | Transfer             |
   | 0008.5.1.4.1.1.9.1.3 | Waveform Storage SOP |                      |
   |                      | Class                |                      |
   +----------------------+----------------------+----------------------+
   | 1.2.840.1            | Hemodynamic Waveform | Transfer             |
   | 0008.5.1.4.1.1.9.2.1 | Storage SOP Class    |                      |
   +----------------------+----------------------+----------------------+
   | 1.2.840.1            | Cardiac              | Transfer             |
   | 0008.5.1.4.1.1.9.3.1 | Electrophysiology    |                      |
   |                      | Waveform Storage SOP |                      |
   |                      | Class                |                      |
   +----------------------+----------------------+----------------------+
   | 1.2.840.1            | Basic Voice Audio    | Transfer             |
   | 0008.5.1.4.1.1.9.4.1 | Waveform Storage SOP |                      |
   |                      | Class                |                      |
   +----------------------+----------------------+----------------------+
   | 1.2.840.1            | General Audio        | Transfer             |
   | 0008.5.1.4.1.1.9.4.2 | Waveform Storage SOP |                      |
   |                      | Class                |                      |
   +----------------------+----------------------+----------------------+
   | 1.2.840.1            | Arterial Pulse       | Transfer             |
   | 0008.5.1.4.1.1.9.5.1 | Waveform Storage SOP |                      |
   |                      | Class                |                      |
   +----------------------+----------------------+----------------------+
   | 1.2.840.1            | Respiratory Waveform | Transfer             |
   | 0008.5.1.4.1.1.9.6.1 | Storage SOP Class    |                      |
   +----------------------+----------------------+----------------------+
   | 1.2.840.1            | Multi-channel        | Transfer             |
   | 0008.5.1.4.1.1.9.6.2 | Respiratory Waveform |                      |
   |                      | Storage SOP Class    |                      |
   +----------------------+----------------------+----------------------+
   | 1.2.840.1            | Routine Scalp        | Transfer             |
   | 0008.5.1.4.1.1.9.7.1 | Electroencephalogram |                      |
   |                      | Waveform Storage SOP |                      |
   |                      | Class                |                      |
   +----------------------+----------------------+----------------------+
   | 1.2.840.1            | Electromyogram       | Transfer             |
   | 0008.5.1.4.1.1.9.7.2 | Waveform Storage SOP |                      |
   |                      | Class                |                      |
   +----------------------+----------------------+----------------------+
   | 1.2.840.1            | Electrooculogram     | Transfer             |
   | 0008.5.1.4.1.1.9.7.3 | Waveform Storage SOP |                      |
   |                      | Class                |                      |
   +----------------------+----------------------+----------------------+
   | 1.2.840.1            | Sleep                | Transfer             |
   | 0008.5.1.4.1.1.9.7.4 | Electroencephalogram |                      |
   |                      | Waveform Storage SOP |                      |
   |                      | Class                |                      |
   +----------------------+----------------------+----------------------+
   | 1.2.840.1            | Body Position        | Transfer             |
   | 0008.5.1.4.1.1.9.8.1 | Waveform Storage SOP |                      |
   |                      | Class                |                      |
   +----------------------+----------------------+----------------------+
   | 1.2.840.             | Grayscale Softcopy   | Transfer             |
   | 10008.5.1.4.1.1.11.1 | Presentation State   |                      |
   |                      | Storage SOP Class    |                      |
   +----------------------+----------------------+----------------------+
   | 1.2.840.             | Color Softcopy       | Transfer             |
   | 10008.5.1.4.1.1.11.2 | Presentation State   |                      |
   |                      | Storage SOP Class    |                      |
   +----------------------+----------------------+----------------------+
   | 1.2.840.             | Pseudo-Color         | Transfer             |
   | 10008.5.1.4.1.1.11.3 | Softcopy             |                      |
   |                      | Presentation State   |                      |
   |                      | Storage SOP Class    |                      |
   +----------------------+----------------------+----------------------+
   | 1.2.840.             | Blending Softcopy    | Transfer             |
   | 10008.5.1.4.1.1.11.4 | Presentation State   |                      |
   |                      | Storage SOP Class    |                      |
   +----------------------+----------------------+----------------------+
   | 1.2.840.             | XA/XRF Grayscale     | Transfer             |
   | 10008.5.1.4.1.1.11.5 | Softcopy             |                      |
   |                      | Presentation State   |                      |
   |                      | Storage SOP Class    |                      |
   +----------------------+----------------------+----------------------+
   | 1.2.840.10008.​      | Grayscale Planar MPR | Transfer             |
   | 5.​1.​4.​1.​1.​11.​6 | Volumetric           |                      |
   |                      | Presentation State   |                      |
   |                      | Storage SOP Class    |                      |
   +----------------------+----------------------+----------------------+
   | 1.2.840.10008.​      | Compositing Planar   | Transfer             |
   | 5.​1.​4.​1.​1.​11.​7 | MPR Volumetric       |                      |
   |                      | Presentation State   |                      |
   |                      | Storage SOP Class    |                      |
   +----------------------+----------------------+----------------------+
   | 1.2.840.10008.​      | Advanced Blending    | Transfer             |
   | 5.​1.​4.​1.​1.​11.​8 | Presentation State   |                      |
   |                      | Storage SOP Class    |                      |
   +----------------------+----------------------+----------------------+
   | 1.2.840.10008.​      | Volume Rendering     | Transfer             |
   | 5.​1.​4.​1.​1.​11.​9 | Volumetric           |                      |
   |                      | Presentation State   |                      |
   |                      | Storage SOP Class    |                      |
   +----------------------+----------------------+----------------------+
   | 1.2.840.10008.​5     | Segmented Volume     | Transfer             |
   | .​1.​4.​1.​1.​11.​10 | Rendering Volumetric |                      |
   |                      | Presentation State   |                      |
   |                      | Storage SOP Class    |                      |
   +----------------------+----------------------+----------------------+
   | 1.2.840.10008.​5     | Multiple Volume      | Transfer             |
   | .​1.​4.​1.​1.​11.​11 | Rendering Volumetric |                      |
   |                      | Presentation State   |                      |
   |                      | Storage SOP Class    |                      |
   +----------------------+----------------------+----------------------+
   | 1.2.840.             | X-Ray Angiographic   | Transfer             |
   | 10008.5.1.4.1.1.12.1 | Image Storage SOP    |                      |
   |                      | Class                |                      |
   +----------------------+----------------------+----------------------+
   | 1.2.840.10           | Enhanced XA Image    | Transfer             |
   | 008.5.1.4.1.1.12.1.1 | Storage SOP Class    |                      |
   +----------------------+----------------------+----------------------+
   | 1.2.840.             | X-Ray                | Transfer             |
   | 10008.5.1.4.1.1.12.2 | Radiofluoroscopic    |                      |
   |                      | Image Storage SOP    |                      |
   |                      | Class                |                      |
   +----------------------+----------------------+----------------------+
   | 1.2.840.10           | Enhanced XRF Image   | Transfer             |
   | 008.5.1.4.1.1.12.2.1 | Storage SOP Class    |                      |
   +----------------------+----------------------+----------------------+
   | 1.2.840.10           | X-Ray 3D             | Transfer             |
   | 008.5.1.4.1.1.13.1.1 | Angiographic Image   |                      |
   |                      | Storage SOP Class    |                      |
   +----------------------+----------------------+----------------------+
   | 1.2.840.10           | X-Ray 3D             | Transfer             |
   | 008.5.1.4.1.1.13.1.2 | Craniofacial Image   |                      |
   |                      | Storage SOP Class    |                      |
   +----------------------+----------------------+----------------------+
   | 1.2.840.10           | Breast Tomosynthesis | Transfer             |
   | 008.5.1.4.1.1.13.1.3 | Image Storage SOP    |                      |
   |                      | Class                |                      |
   +----------------------+----------------------+----------------------+
   | 1.2.840.10           | Breast Projection    | Transfer             |
   | 008.5.1.4.1.1.13.1.4 | X-Ray Image Storage  |                      |
   |                      | - For Presentation   |                      |
   |                      | SOP Class            |                      |
   +----------------------+----------------------+----------------------+
   | 1.2.840.10           | Breast Projection    | Transfer             |
   | 008.5.1.4.1.1.13.1.5 | X-Ray Image Storage  |                      |
   |                      | - For Processing SOP |                      |
   |                      | Class                |                      |
   +----------------------+----------------------+----------------------+
   | 1.2.840.             | Intravascular        | Transfer             |
   | 10008.5.1.4.1.1.14.1 | Optical Coherence    |                      |
   |                      | Tomography Image     |                      |
   |                      | Storage - For        |                      |
   |                      | Presentation SOP     |                      |
   |                      | Class                |                      |
   +----------------------+----------------------+----------------------+
   | 1.2.840.             | Intravascular        | Transfer             |
   | 10008.5.1.4.1.1.14.2 | Optical Coherence    |                      |
   |                      | Tomography Image     |                      |
   |                      | Storage - For        |                      |
   |                      | Processing SOP Class |                      |
   +----------------------+----------------------+----------------------+
   | 1.2.84               | Nuclear Medicine     | Transfer             |
   | 0.10008.5.1.4.1.1.20 | Image Storage SOP    |                      |
   |                      | Class                |                      |
   +----------------------+----------------------+----------------------+
   | 1.2.84               | Parametric Map       | Transfer             |
   | 0.10008.5.1.4.1.1.30 | Storage SOP Class    |                      |
   +----------------------+----------------------+----------------------+
   | 1.2.84               | Raw Data Storage SOP | Transfer             |
   | 0.10008.5.1.4.1.1.66 | Class                |                      |
   +----------------------+----------------------+----------------------+
   | 1.2.840.             | Spatial Registration | Transfer             |
   | 10008.5.1.4.1.1.66.1 | Storage SOP Class    |                      |
   +----------------------+----------------------+----------------------+
   | 1.2.840.             | Spatial Fiducials    | Transfer             |
   | 10008.5.1.4.1.1.66.2 | Storage SOP Class    |                      |
   +----------------------+----------------------+----------------------+
   | 1.2.840.             | Deformable Spatial   | Transfer             |
   | 10008.5.1.4.1.1.66.3 | Registration Storage |                      |
   |                      | SOP Class            |                      |
   +----------------------+----------------------+----------------------+
   | 1.2.840.             | Segmentation Storage | Transfer             |
   | 10008.5.1.4.1.1.66.4 | SOP Class            |                      |
   +----------------------+----------------------+----------------------+
   | 1.2.840.             | Surface Segmentation | Transfer             |
   | 10008.5.1.4.1.1.66.5 | Storage SOP Class    |                      |
   +----------------------+----------------------+----------------------+
   | 1.2.840.             | Tractography Results | Transfer             |
   | 10008.5.1.4.1.1.66.6 | Storage SOP Class    |                      |
   +----------------------+----------------------+----------------------+
   | 1.2.84               | Real World Value     | Transfer             |
   | 0.10008.5.1.4.1.1.67 | Mapping Storage SOP  |                      |
   |                      | Class                |                      |
   +----------------------+----------------------+----------------------+
   | 1.2.840.             | Surface Scan Mesh    | Transfer             |
   | 10008.5.1.4.1.1.68.1 | Storage SOP Class    |                      |
   +----------------------+----------------------+----------------------+
   | 1.2.840.             | Surface Scan Point   | Transfer             |
   | 10008.5.1.4.1.1.68.2 | Cloud Storage SOP    |                      |
   |                      | Class                |                      |
   +----------------------+----------------------+----------------------+
   | 1.2.840.10           | VL Endoscopic Image  | Transfer             |
   | 008.5.1.4.1.1.77.1.1 | Storage SOP Class    |                      |
   +----------------------+----------------------+----------------------+
   | 1.2.840.1000         | Video Endoscopic     | Transfer             |
   | 8.5.1.4.1.1.77.1.1.1 | Image Storage SOP    |                      |
   |                      | Class                |                      |
   +----------------------+----------------------+----------------------+
   | 1.2.840.10           | VL Microscopic Image | Transfer             |
   | 008.5.1.4.1.1.77.1.2 | Storage SOP Class    |                      |
   +----------------------+----------------------+----------------------+
   | 1.2.840.1000         | Video Microscopic    | Transfer             |
   | 8.5.1.4.1.1.77.1.2.1 | Image Storage SOP    |                      |
   |                      | Class                |                      |
   +----------------------+----------------------+----------------------+
   | 1.2.840.10           | VL Slide-Coordinates | Transfer             |
   | 008.5.1.4.1.1.77.1.3 | Microscopic Image    |                      |
   |                      | Storage SOP Class    |                      |
   +----------------------+----------------------+----------------------+
   | 1.2.840.10           | VL Photographic      | Transfer             |
   | 008.5.1.4.1.1.77.1.4 | Image Storage SOP    |                      |
   |                      | Class                |                      |
   +----------------------+----------------------+----------------------+
   | 1.2.840.1000         | Video Photographic   | Transfer             |
   | 8.5.1.4.1.1.77.1.4.1 | Image Storage SOP    |                      |
   |                      | Class                |                      |
   +----------------------+----------------------+----------------------+
   | 1.2.840.1000         | Ophthalmic           | Transfer             |
   | 8.5.1.4.1.1.77.1.5.1 | Photography 8 Bit    |                      |
   |                      | Image Storage SOP    |                      |
   |                      | Class                |                      |
   +----------------------+----------------------+----------------------+
   | 1.2.840.1000         | Ophthalmic           | Transfer             |
   | 8.5.1.4.1.1.77.1.5.2 | Photography 16 Bit   |                      |
   |                      | Image Storage SOP    |                      |
   |                      | Class                |                      |
   +----------------------+----------------------+----------------------+
   | 1.2.840.1000         | Stereometric         | Transfer             |
   | 8.5.1.4.1.1.77.1.5.3 | Relationship Storage |                      |
   |                      | SOP Class            |                      |
   +----------------------+----------------------+----------------------+
   | 1.2.840.1000         | Ophthalmic           | Transfer             |
   | 8.5.1.4.1.1.77.1.5.4 | Tomography Image     |                      |
   |                      | Storage SOP Class    |                      |
   +----------------------+----------------------+----------------------+
   | 1.2.840.1000         | Wide Field           | Transfer             |
   | 8.5.1.4.1.1.77.1.5.5 | Ophthalmic           |                      |
   |                      | Photography          |                      |
   |                      | Stereographic        |                      |
   |                      | Projection Image     |                      |
   |                      | Storage SOP Class    |                      |
   +----------------------+----------------------+----------------------+
   | 1.2.840.1000         | Wide Field           | Transfer             |
   | 8.5.1.4.1.1.77.1.5.6 | Ophthalmic           |                      |
   |                      | Photography 3D       |                      |
   |                      | Coordinates Image    |                      |
   |                      | Storage SOP Class    |                      |
   +----------------------+----------------------+----------------------+
   | 1.2.840.1000         | Ophthalmic Optical   | Transfer             |
   | 8.5.1.4.1.1.77.1.5.7 | Coherence Tomography |                      |
   |                      | En Face Image        |                      |
   |                      | Storage SOP Class    |                      |
   +----------------------+----------------------+----------------------+
   | 1.2.840.1000         | Ophthalmic Optical   | Transfer             |
   | 8.5.1.4.1.1.77.1.5.8 | Coherence Tomography |                      |
   |                      | B-scan Volume        |                      |
   |                      | Analysis Storage SOP |                      |
   |                      | Class                |                      |
   +----------------------+----------------------+----------------------+
   | 1.2.840.10           | VL Whole Slide       | Transfer             |
   | 008.5.1.4.1.1.77.1.6 | Microscopy Image     |                      |
   |                      | Storage SOP Class    |                      |
   +----------------------+----------------------+----------------------+
   | 1.2.840.             | Lensometry           | Transfer             |
   | 10008.5.1.4.1.1.78.1 | Measurements Storage |                      |
   |                      | SOP Class            |                      |
   +----------------------+----------------------+----------------------+
   | 1.2.840.             | Autorefraction       | Transfer             |
   | 10008.5.1.4.1.1.78.2 | Measurements Storage |                      |
   |                      | SOP Class            |                      |
   +----------------------+----------------------+----------------------+
   | 1.2.840.             | Keratometry          | Transfer             |
   | 10008.5.1.4.1.1.78.3 | Measurements Storage |                      |
   |                      | SOP Class            |                      |
   +----------------------+----------------------+----------------------+
   | 1.2.840.             | Subjective           | Transfer             |
   | 10008.5.1.4.1.1.78.4 | Refraction           |                      |
   |                      | Measurements Storage |                      |
   |                      | SOP Class            |                      |
   +----------------------+----------------------+----------------------+
   | 1.2.840.             | Visual Acuity        | Transfer             |
   | 10008.5.1.4.1.1.78.5 | Measurements Storage |                      |
   |                      | SOP Class            |                      |
   +----------------------+----------------------+----------------------+
   | 1.2.840.             | Spectacle            | Transfer             |
   | 10008.5.1.4.1.1.78.6 | Prescription Report  |                      |
   |                      | Storage SOP Class    |                      |
   +----------------------+----------------------+----------------------+
   | 1.2.840.             | Ophthalmic Axial     | Transfer             |
   | 10008.5.1.4.1.1.78.7 | Measurements Storage |                      |
   |                      | SOP Class            |                      |
   +----------------------+----------------------+----------------------+
   | 1.2.840.             | Intraocular Lens     | Transfer             |
   | 10008.5.1.4.1.1.78.8 | Calculations Storage |                      |
   |                      | SOP Class            |                      |
   +----------------------+----------------------+----------------------+
   | 1.2.840.             | Macular Grid         | Transfer             |
   | 10008.5.1.4.1.1.79.1 | Thickness and Volume |                      |
   |                      | Report Storage SOP   |                      |
   |                      | Class                |                      |
   +----------------------+----------------------+----------------------+
   | 1.2.840.             | Ophthalmic Visual    | Transfer             |
   | 10008.5.1.4.1.1.80.1 | Field Static         |                      |
   |                      | Perimetry            |                      |
   |                      | Measurements Storage |                      |
   |                      | SOP Class            |                      |
   +----------------------+----------------------+----------------------+
   | 1.2.840.             | Ophthalmic Thickness | Transfer             |
   | 10008.5.1.4.1.1.81.1 | Map Storage SOP      |                      |
   |                      | Class                |                      |
   +----------------------+----------------------+----------------------+
   | 1.2.840.             | Corneal Topography   | Transfer             |
   | 10008.5.1.4.1.1.82.1 | Map Storage SOP      |                      |
   |                      | Class                |                      |
   +----------------------+----------------------+----------------------+
   | 1.2.840.1            | Basic Text SR        | Transfer             |
   | 0008.5.1.4.1.1.88.11 | Storage SOP Class    |                      |
   +----------------------+----------------------+----------------------+
   | 1.2.840.1            | Enhanced SR Storage  | Transfer             |
   | 0008.5.1.4.1.1.88.22 | SOP Class            |                      |
   +----------------------+----------------------+----------------------+
   | 1.2.840.1            | Comprehensive SR     | Transfer             |
   | 0008.5.1.4.1.1.88.33 | Storage SOP Class    |                      |
   +----------------------+----------------------+----------------------+
   | 1.2.840.1            | Comprehensive 3D SR  | Transfer             |
   | 0008.5.1.4.1.1.88.34 | Storage SOP Class    |                      |
   +----------------------+----------------------+----------------------+
   | 1.2.840.1            | Procedure Log        | Transfer             |
   | 0008.5.1.4.1.1.88.40 | Storage SOP Class    |                      |
   +----------------------+----------------------+----------------------+
   | 1.2.840.1            | Mammography CAD SR   | Transfer             |
   | 0008.5.1.4.1.1.88.50 | Storage SOP Class    |                      |
   +----------------------+----------------------+----------------------+
   | 1.2.840.1            | Key Object Selection | Transfer             |
   | 0008.5.1.4.1.1.88.59 | Document Storage SOP |                      |
   |                      | Class                |                      |
   +----------------------+----------------------+----------------------+
   | 1.2.840.1            | Chest CAD SR Storage | Transfer             |
   | 0008.5.1.4.1.1.88.65 | SOP Class            |                      |
   +----------------------+----------------------+----------------------+
   | 1.2.840.1            | X-Ray Radiation Dose | Transfer             |
   | 0008.5.1.4.1.1.88.67 | SR Storage SOP Class |                      |
   +----------------------+----------------------+----------------------+
   | 1.2.840.1            | Radiopharmaceutical  | Transfer             |
   | 0008.5.1.4.1.1.88.68 | Radiation Dose SR    |                      |
   |                      | Storage SOP Class    |                      |
   +----------------------+----------------------+----------------------+
   | 1.2.840.1            | Colon CAD SR Storage | Transfer             |
   | 0008.5.1.4.1.1.88.69 | SOP Class            |                      |
   +----------------------+----------------------+----------------------+
   | 1.2.840.1            | Implantation Plan SR | Transfer             |
   | 0008.5.1.4.1.1.88.70 | Document Storage SOP |                      |
   |                      | Class                |                      |
   +----------------------+----------------------+----------------------+
   | 1.2.840.10008.5      | Acquisition Context  | Transfer             |
   | .​1.​4.​1.​1.​88.​71 | SR Storage SOP Class |                      |
   +----------------------+----------------------+----------------------+
   | 1.2.840.10008.5      | Simplified Adult     | Transfer             |
   | .​1.​4.​1.​1.​88.​72 | Echo SR Storage SOP  |                      |
   |                      | Class                |                      |
   +----------------------+----------------------+----------------------+
   | 1.2.840.10008.5      | Patient Radiation    | Transfer             |
   | .​1.​4.​1.​1.​88.​73 | Dose SR Storage SOP  |                      |
   |                      | Class                |                      |
   +----------------------+----------------------+----------------------+
   | 1.2.840.10008.5      | Planned Imaging      | Transfer             |
   | .​1.​4.​1.​1.​88.​74 | Agent Administration |                      |
   |                      | SR Storage SOP Class |                      |
   +----------------------+----------------------+----------------------+
   | 1.2.840.10008.5      | Performed Imaging    | Transfer             |
   | .​1.​4.​1.​1.​88.​75 | Agent Administration |                      |
   |                      | SR Storage SOP Class |                      |
   +----------------------+----------------------+----------------------+
   | 1.2.840.             | Content Assessment   | Transfer             |
   | 10008.5.1.4.1.1.90.1 | Results Storage SOP  |                      |
   |                      | Class                |                      |
   +----------------------+----------------------+----------------------+
   | 1.2.840.1            | Encapsulated PDF     | Transfer             |
   | 0008.5.1.4.1.1.104.1 | Storage SOP Class    |                      |
   +----------------------+----------------------+----------------------+
   | 1.2.840.1            | Encapsulated CDA     | Transfer             |
   | 0008.5.1.4.1.1.104.2 | Storage SOP Class    |                      |
   +----------------------+----------------------+----------------------+
   | 1.2.840.1            | Encapsulated STL     | Transfer             |
   | 0008.5.1.4.1.1.104.3 | Storage SOP Class    |                      |
   +----------------------+----------------------+----------------------+
   | 1.2.840.1            | Encapsulated OBJ     | Transfer             |
   | 0008.5.1.4.1.1.104.4 | Storage SOP Class    |                      |
   +----------------------+----------------------+----------------------+
   | 1.2.840.1            | Encapsulated MTL     | Transfer             |
   | 0008.5.1.4.1.1.104.5 | Storage SOP Class    |                      |
   +----------------------+----------------------+----------------------+
   | 1.2.840              | Positron Emission    | Transfer             |
   | .10008.5.1.4.1.1.128 | Tomography Image     |                      |
   |                      | Storage SOP Class    |                      |
   +----------------------+----------------------+----------------------+
   | 1.2.840              | Enhanced PET Image   | Transfer             |
   | .10008.5.1.4.1.1.130 | Storage SOP Class    |                      |
   +----------------------+----------------------+----------------------+
   | 1.2.840              | Basic Structured     | Transfer             |
   | .10008.5.1.4.1.1.131 | Display Storage SOP  |                      |
   |                      | Class                |                      |
   +----------------------+----------------------+----------------------+
   | 1.2.840.1            | CT Defined Procedure | Transfer             |
   | 0008.5.1.4.1.1.200.1 | Protocol Storage SOP |                      |
   |                      | Class                |                      |
   +----------------------+----------------------+----------------------+
   | 1.2.840.1            | CT Performed         | Transfer             |
   | 0008.5.1.4.1.1.200.2 | Procedure Protocol   |                      |
   |                      | Storage SOP Class    |                      |
   +----------------------+----------------------+----------------------+
   | 1.2.840.1            | Protocol Approval    | Transfer             |
   | 0008.5.1.4.1.1.200.3 | Storage SOP Class    |                      |
   +----------------------+----------------------+----------------------+
   | 1.2.840.1            | RT Image Storage SOP | Transfer             |
   | 0008.5.1.4.1.1.481.1 | Class                |                      |
   +----------------------+----------------------+----------------------+
   | 1.2.840.1            | RT Dose Storage SOP  | Transfer             |
   | 0008.5.1.4.1.1.481.2 | Class                |                      |
   +----------------------+----------------------+----------------------+
   | 1.2.840.1            | RT Structure Set     | Transfer             |
   | 0008.5.1.4.1.1.481.3 | Storage SOP Class    |                      |
   +----------------------+----------------------+----------------------+
   | 1.2.840.1            | RT Beams Treatment   | Transfer             |
   | 0008.5.1.4.1.1.481.4 | Record Storage SOP   |                      |
   |                      | Class                |                      |
   +----------------------+----------------------+----------------------+
   | 1.2.840.1            | RT Plan Storage SOP  | Transfer             |
   | 0008.5.1.4.1.1.481.5 | Class                |                      |
   +----------------------+----------------------+----------------------+
   | 1.2.840.1            | RT Brachy Treatment  | Transfer             |
   | 0008.5.1.4.1.1.481.6 | Record Storage SOP   |                      |
   |                      | Class                |                      |
   +----------------------+----------------------+----------------------+
   | 1.2.840.1            | RT Treatment Summary | Transfer             |
   | 0008.5.1.4.1.1.481.7 | Record Storage SOP   |                      |
   |                      | Class                |                      |
   +----------------------+----------------------+----------------------+
   | 1.2.840.1            | RT Ion Plan Storage  | Transfer             |
   | 0008.5.1.4.1.1.481.8 | SOP Class            |                      |
   +----------------------+----------------------+----------------------+
   | 1.2.840.1            | RT Ion Beams         | Transfer             |
   | 0008.5.1.4.1.1.481.9 | Treatment Record     |                      |
   |                      | Storage SOP Class    |                      |
   +----------------------+----------------------+----------------------+
   | 1.2.840.10           | RT Physician Intent  | Transfer             |
   | 008.5.1.4.1.1.481.10 | Storage SOP Class    |                      |
   +----------------------+----------------------+----------------------+
   | 1.2.840.10           | RT Segment           | Transfer             |
   | 008.5.1.4.1.1.481.11 | Annotation Storage   |                      |
   |                      | SOP Class            |                      |
   +----------------------+----------------------+----------------------+
   | 1.2.840.10           | RT Radiation Set     | Transfer             |
   | 008.5.1.4.1.1.481.12 | Storage              |                      |
   +----------------------+----------------------+----------------------+
   | 1.2.840.10           | C-Arm                | Transfer             |
   | 008.5.1.4.1.1.481.13 | Photon-Electron      |                      |
   |                      | Radiation Storage    |                      |
   +----------------------+----------------------+----------------------+
   | 1.2.840.10           | Tomotherapeutic      | Transfer             |
   | 008.5.1.4.1.1.481.14 | Radiation Storage    |                      |
   +----------------------+----------------------+----------------------+
   | 1.2.840.10           | Robotic-Arm          | Transfer             |
   | 008.5.1.4.1.1.481.15 | Radiation Storage    |                      |
   +----------------------+----------------------+----------------------+
   | 1.2.840.10           | RT Radiation Record  | Transfer             |
   | 008.5.1.4.1.1.481.16 | Set Storage          |                      |
   +----------------------+----------------------+----------------------+
   | 1.2.840.10           | RT Radiation Salvage | Transfer             |
   | 008.5.1.4.1.1.481.17 | Record Storage       |                      |
   +----------------------+----------------------+----------------------+
   | 1.2.840.10           | Tomotherapeutic      | Transfer             |
   | 008.5.1.4.1.1.481.18 | Radiation Record     |                      |
   |                      | Storage              |                      |
   +----------------------+----------------------+----------------------+
   | 1.2.840.10           | C-Arm Photon         | Transfer             |
   | 008.5.1.4.1.1.481.19 | Electron Radiation   |                      |
   |                      | Record Storage       |                      |
   +----------------------+----------------------+----------------------+
   | 1.2.840.10           | Robotic-Arm          | Transfer             |
   | 008.5.1.4.1.1.481.20 | Radiation Record     |                      |
   |                      | Storage              |                      |
   +----------------------+----------------------+----------------------+
   | 1.2.840              | Patient Root         | Query/Retrieve       |
   | .10008.5.1.4.1.2.1.1 | Query/Retrieve       |                      |
   |                      | Information Model -  |                      |
   |                      | FIND SOP Class       |                      |
   +----------------------+----------------------+----------------------+
   | 1.2.840              | Patient Root         | Query/Retrieve       |
   | .10008.5.1.4.1.2.1.2 | Query/Retrieve       |                      |
   |                      | Information Model -  |                      |
   |                      | MOVE SOP Class       |                      |
   +----------------------+----------------------+----------------------+
   | 1.2.840              | Patient Root         | Query/Retrieve       |
   | .10008.5.1.4.1.2.1.3 | Query/Retrieve       |                      |
   |                      | Information Model -  |                      |
   |                      | GET SOP Class        |                      |
   +----------------------+----------------------+----------------------+
   | 1.2.840              | Study Root           | Query/Retrieve       |
   | .10008.5.1.4.1.2.2.1 | Query/Retrieve       |                      |
   |                      | Information Model -  |                      |
   |                      | FIND SOP Class       |                      |
   +----------------------+----------------------+----------------------+
   | 1.2.840              | Study Root           | Query/Retrieve       |
   | .10008.5.1.4.1.2.2.2 | Query/Retrieve       |                      |
   |                      | Information Model -  |                      |
   |                      | MOVE SOP Class       |                      |
   +----------------------+----------------------+----------------------+
   | 1.2.840              | Study Root           | Query/Retrieve       |
   | .10008.5.1.4.1.2.2.3 | Query/Retrieve       |                      |
   |                      | Information Model -  |                      |
   |                      | GET SOP Class        |                      |
   +----------------------+----------------------+----------------------+
   | 1.2.840              | Composite Instance   | Query/Retrieve       |
   | .10008.5.1.4.1.2.4.2 | Root Retrieve - MOVE |                      |
   |                      | SOP Class            |                      |
   +----------------------+----------------------+----------------------+
   | 1.2.840              | Composite Instance   | Query/Retrieve       |
   | .10008.5.1.4.1.2.4.3 | Root Retrieve - GET  |                      |
   |                      | SOP Class            |                      |
   +----------------------+----------------------+----------------------+
   | 1.2.840              | Composite Instance   | Query/Retrieve       |
   | .10008.5.1.4.1.2.5.3 | Retrieve Without     |                      |
   |                      | Bulk Data - GET SOP  |                      |
   |                      | Class                |                      |
   +----------------------+----------------------+----------------------+
   | 1.2.                 | Defined Procedure    | Query/Retrieve       |
   | 840.10008.5.1.4.20.1 | Protocol Information |                      |
   |                      | Model - FIND SOP     |                      |
   |                      | Class                |                      |
   +----------------------+----------------------+----------------------+
   | 1.2.                 | Defined Procedure    | Query/Retrieve       |
   | 840.10008.5.1.4.20.2 | Protocol Information |                      |
   |                      | Model - MOVE SOP     |                      |
   |                      | Class                |                      |
   +----------------------+----------------------+----------------------+
   | 1.2.                 | Defined Procedure    | Query/Retrieve       |
   | 840.10008.5.1.4.20.3 | Protocol Information |                      |
   |                      | Model - GET SOP      |                      |
   |                      | Class                |                      |
   +----------------------+----------------------+----------------------+
   | 1.2.840.1            | Protocol Approval    | Query/Retrieve       |
   | 0008.5.1.4.1.1.200.4 | Information Model -  |                      |
   |                      | FIND SOP Class       |                      |
   +----------------------+----------------------+----------------------+
   | 1.2.840.1            | Protocol Approval    | Query/Retrieve       |
   | 0008.5.1.4.1.1.200.5 | Information Model -  |                      |
   |                      | MOVE SOP Class       |                      |
   +----------------------+----------------------+----------------------+
   | 1.2.840.1            | Protocol Approval    | Query/Retrieve       |
   | 0008.5.1.4.1.1.200.6 | Information Model -  |                      |
   |                      | GET SOP Class        |                      |
   +----------------------+----------------------+----------------------+
   | 1.                   | Modality Worklist    | Workflow Management  |
   | 2.840.10008.5.1.4.31 | Information Model -  |                      |
   |                      | FIND SOP Class       |                      |
   +----------------------+----------------------+----------------------+
   | *1.2.8               | *General Purpose     | *Workflow            |
   | 40.10008.5.1.4.32.1* | Worklist Information | Management*          |
   |                      | Model - FIND SOP     |                      |
   |                      | Class (Retired)*     |                      |
   +----------------------+----------------------+----------------------+
   | *1.2.8               | *General Purpose     | *Workflow            |
   | 40.10008.5.1.4.32.2* | Scheduled Procedure  | Management*          |
   |                      | Step SOP Class       |                      |
   |                      | (Retired)*           |                      |
   +----------------------+----------------------+----------------------+
   | *1.2.8               | *General Purpose     | *Workflow            |
   | 40.10008.5.1.4.32.3* | Performed Procedure  | Management*          |
   |                      | Step SOP Class       |                      |
   |                      | (Retired)*           |                      |
   +----------------------+----------------------+----------------------+
   | *1.2                 | *General Purpose     | *Workflow            |
   | .840.10008.5.1.4.32* | Worklist Management  | Management*          |
   |                      | Meta SOP Class       |                      |
   |                      | (Retired)*           |                      |
   +----------------------+----------------------+----------------------+
   | 1.                   | Instance             | Workflow Management  |
   | 2.840.10008.5.1.4.33 | Availability         |                      |
   |                      | Notification SOP     |                      |
   |                      | Class                |                      |
   +----------------------+----------------------+----------------------+
   | 1.2.84               | Unified Procedure    | Workflow Management  |
   | 0.10008.5.1.4.34.6.1 | Step - Push SOP      |                      |
   |                      | Class                |                      |
   +----------------------+----------------------+----------------------+
   | 1.2.84               | Unified Procedure    | Workflow Management  |
   | 0.10008.5.1.4.34.6.2 | Step - Watch SOP     |                      |
   |                      | Class                |                      |
   +----------------------+----------------------+----------------------+
   | 1.2.84               | Unified Procedure    | Workflow Management  |
   | 0.10008.5.1.4.34.6.3 | Step - Pull SOP      |                      |
   |                      | Class                |                      |
   +----------------------+----------------------+----------------------+
   | 1.2.84               | Unified Procedure    | Workflow Management  |
   | 0.10008.5.1.4.34.6.4 | Step - Event SOP     |                      |
   |                      | Class                |                      |
   +----------------------+----------------------+----------------------+
   | 1.2.84               | Unified Procedure    | Workflow Management  |
   | 0.10008.5.1.4.34.6.5 | Step - Query SOP     |                      |
   |                      | Class                |                      |
   +----------------------+----------------------+----------------------+
   | 1.2.                 | RT Beams Delivery    | Transfer             |
   | 840.10008.5.1.4.34.7 | Instruction Storage  |                      |
   |                      | SOP Class            |                      |
   +----------------------+----------------------+----------------------+
   | 1.2.                 | RT Conventional      | Workflow Management  |
   | 840.10008.5.1.4.34.8 | Machine Verification |                      |
   |                      | SOP Class            |                      |
   +----------------------+----------------------+----------------------+
   | 1.2.                 | RT Ion Machine       | Workflow Management  |
   | 840.10008.5.1.4.34.9 | Verification SOP     |                      |
   |                      | Class                |                      |
   +----------------------+----------------------+----------------------+
   | 1.2.8                | RT Brachy            | Transfer             |
   | 40.10008.5.1.4.34.10 | Application Setup    |                      |
   |                      | Delivery Instruction |                      |
   |                      | Storage SOP Class    |                      |
   +----------------------+----------------------+----------------------+
   | 1.2.                 | General Relevant     | Query/Retrieve       |
   | 840.10008.5.1.4.37.1 | Patient Information  |                      |
   |                      | Query SOP Class      |                      |
   +----------------------+----------------------+----------------------+
   | 1.2.                 | Breast Imaging       | Query/Retrieve       |
   | 840.10008.5.1.4.37.2 | Relevant Patient     |                      |
   |                      | Information Query    |                      |
   |                      | SOP Class            |                      |
   +----------------------+----------------------+----------------------+
   | 1.2.                 | Cardiac Relevant     | Query/Retrieve       |
   | 840.10008.5.1.4.37.3 | Patient Information  |                      |
   |                      | Query SOP Class      |                      |
   +----------------------+----------------------+----------------------+
   | 1.2.                 | Hanging Protocol     | Transfer             |
   | 840.10008.5.1.4.38.1 | Storage SOP Class    |                      |
   +----------------------+----------------------+----------------------+
   | 1.2.                 | Hanging Protocol     | Query/Retrieve       |
   | 840.10008.5.1.4.38.2 | Information Model -  |                      |
   |                      | FIND SOP Class       |                      |
   +----------------------+----------------------+----------------------+
   | 1.2.                 | Hanging Protocol     | Query/Retrieve       |
   | 840.10008.5.1.4.38.3 | Information Model -  |                      |
   |                      | MOVE SOP Class       |                      |
   +----------------------+----------------------+----------------------+
   | 1.2.                 | Color Palette        | Transfer             |
   | 840.10008.5.1.4.39.1 | Storage SOP Class    |                      |
   +----------------------+----------------------+----------------------+
   | 1.2.                 | Color Palette        | Query/Retrieve       |
   | 840.10008.5.1.4.39.2 | Information Model -  |                      |
   |                      | FIND SOP Class       |                      |
   +----------------------+----------------------+----------------------+
   | 1.2.                 | Color Palette        | Query/Retrieve       |
   | 840.10008.5.1.4.39.3 | Information Model -  |                      |
   |                      | MOVE SOP Class       |                      |
   +----------------------+----------------------+----------------------+
   | 1.2.                 | Color Palette        | Query/Retrieve       |
   | 840.10008.5.1.4.39.4 | Information Model -  |                      |
   |                      | GET SOP Class        |                      |
   +----------------------+----------------------+----------------------+
   | 1.                   | Product              | Query/Retrieve       |
   | 2.840.10008.5.1.4.41 | Characteristics      |                      |
   |                      | Query SOP Class      |                      |
   +----------------------+----------------------+----------------------+
   | 1.                   | Substance Approval   | Query/Retrieve       |
   | 2.840.10008.5.1.4.42 | Query SOP Class      |                      |
   +----------------------+----------------------+----------------------+
   | 1.2.                 | Generic Implant      | Transfer             |
   | 840.10008.5.1.4.43.1 | Template Storage SOP |                      |
   |                      | Class                |                      |
   +----------------------+----------------------+----------------------+
   | 1.2.                 | Generic Implant      | Query / Retrieve     |
   | 840.10008.5.1.4.43.2 | Template Information |                      |
   |                      | Model - FIND SOP     |                      |
   |                      | Class                |                      |
   +----------------------+----------------------+----------------------+
   | 1.2.                 | Generic Implant      | Query / Retrieve     |
   | 840.10008.5.1.4.43.3 | Template Information |                      |
   |                      | Model - MOVE SOP     |                      |
   |                      | Class                |                      |
   +----------------------+----------------------+----------------------+
   | 1.2.                 | Generic Implant      | Query / Retrieve     |
   | 840.10008.5.1.4.43.4 | Template Information |                      |
   |                      | Model - GET SOP      |                      |
   |                      | Class                |                      |
   +----------------------+----------------------+----------------------+
   | 1.2.                 | Implant Assembly     | Transfer             |
   | 840.10008.5.1.4.44.1 | Template Storage SOP |                      |
   |                      | Class                |                      |
   +----------------------+----------------------+----------------------+
   | 1.2.                 | Implant Assembly     | Query / Retrieve     |
   | 840.10008.5.1.4.44.2 | Template Information |                      |
   |                      | Model - FIND SOP     |                      |
   |                      | Class                |                      |
   +----------------------+----------------------+----------------------+
   | 1.2.                 | Implant Assembly     | Query / Retrieve     |
   | 840.10008.5.1.4.44.3 | Template Information |                      |
   |                      | Model - MOVE SOP     |                      |
   |                      | Class                |                      |
   +----------------------+----------------------+----------------------+
   | 1.2.                 | Implant Assembly     | Query / Retrieve     |
   | 840.10008.5.1.4.44.4 | Template Information |                      |
   |                      | Model - GET SOP      |                      |
   |                      | Class                |                      |
   +----------------------+----------------------+----------------------+
   | 1.2.                 | Implant Template     | Transfer             |
   | 840.10008.5.1.4.45.1 | Group Storage SOP    |                      |
   |                      | Class                |                      |
   +----------------------+----------------------+----------------------+
   | 1.2.                 | Implant Template     | Query / Retrieve     |
   | 840.10008.5.1.4.45.2 | Group Information    |                      |
   |                      | Model - FIND SOP     |                      |
   |                      | Class                |                      |
   +----------------------+----------------------+----------------------+
   | 1.2.                 | Implant Template     | Query / Retrieve     |
   | 840.10008.5.1.4.45.3 | Group Information    |                      |
   |                      | Model - MOVE SOP     |                      |
   |                      | Class                |                      |
   +----------------------+----------------------+----------------------+
   | 1.2.                 | Implant Template     | Query / Retrieve     |
   | 840.10008.5.1.4.45.4 | Group Information    |                      |
   |                      | Model - GET SOP      |                      |
   |                      | Class                |                      |
   +----------------------+----------------------+----------------------+

A table of Supported Media Storage Application Profiles (with roles) is
provided, organized in categories:

-  Compact Disk - Recordable

-  Magneto-Optical Disk

-  DVD

-  BD

-  USB and Flash Memory

-  Email

-  Other Media

.. table:: Media Services

   +------------------------+------------------------+------------------+
   | Media Storage          | Write Files (FSC or    | Read Files (FSR) |
   | Application Profile    | FSU)                   |                  |
   +========================+========================+==================+
   | **Compact Disk -       |                        |                  |
   | Recordable**           |                        |                  |
   +------------------------+------------------------+------------------+
   | General Purpose CD-R   | Option                 | Yes              |
   +------------------------+------------------------+------------------+
   | **Magneto-Optical      |                        |                  |
   | Disk**                 |                        |                  |
   +------------------------+------------------------+------------------+
   | CT/MR 2.3 GB MOD       | Yes                    | Yes              |
   +------------------------+------------------------+------------------+
   | **DVD**                |                        |                  |
   +------------------------+------------------------+------------------+
   | General Purpose        | Yes                    | Yes              |
   | DVD-RAM                |                        |                  |
   +------------------------+------------------------+------------------+
   | **BD**                 |                        |                  |
   +------------------------+------------------------+------------------+
   | General Purpose BD     | Yes                    | Yes              |
   | Interchange with       |                        |                  |
   | MPEG-4 AVC/H.264       |                        |                  |
   | BD-Compatible          |                        |                  |
   | HiP@Level4.1           |                        |                  |
   +------------------------+------------------------+------------------+
   | **USB and Flash        |                        |                  |
   | Memory**               |                        |                  |
   +------------------------+------------------------+------------------+
   | General Purpose USB    | Yes                    | Yes              |
   | Media Interchange with |                        |                  |
   | JPEG                   |                        |                  |
   +------------------------+------------------------+------------------+
   | **Email**              |                        |                  |
   +------------------------+------------------------+------------------+
   | General Purpose MIME   | Yes                    | No               |
   | Interchange            |                        |                  |
   +------------------------+------------------------+------------------+
   | General Purpose ZIP    | Yes                    | No               |
   | Email                  |                        |                  |
   +------------------------+------------------------+------------------+

.. _sect_A.2:

Table of Contents
-----------------

The table of contents will be provided to assist readers in easily
finding the needed information.

.. _sect_A.3:

Introduction
------------

The introduction specifies product and relevant disclaimers as well as
any general information that the vendor feels is appropriate.

The following subsections are suggested:

.. _sect_A.3.1:

Revision History
~~~~~~~~~~~~~~~~

The revision history provides dates and differences of the different
releases of the product and the Conformance Statement.

.. _sect_A.3.2:

Audience
~~~~~~~~

The audience is specified with their assumed pre-knowledge. The
following example may be used as a template:

This document is written for the people that need to understand how
<Product Name> will integrate into their healthcare facility. This
includes both those responsible for overall imaging network policy and
architecture, as well as integrators who need to have a detailed
understanding of the DICOM features of the product. This document
contains some basic DICOM definitions so that any reader may understand
how this product implements DICOM features. However, integrators are
expected to fully understand all the DICOM terminology, how the tables
in this document relate to the product's functionality, and how that
functionality integrates with other devices that support compatible
DICOM features.

.. _sect_A.3.3:

Remarks
~~~~~~~

Any important remarks, disclaimers, and general information are
specified. The following example may be used as a template:

The scope of this DICOM Conformance Statement is to facilitate
integration between <Product Name> and other DICOM products. The
Conformance Statement should be read and understood in conjunction with
the DICOM Standard. DICOM by itself does not guarantee interoperability.
The Conformance Statement does, however, facilitate a first-level
comparison for interoperability between different applications
supporting compatible DICOM functionality.

This Conformance Statement is not supposed to replace validation with
other DICOM equipment to ensure proper exchange of intended information.
In fact, the user should be aware of the following important issues:

-  The comparison of different Conformance Statements is just the first
   step towards assessing interconnectivity and interoperability between
   the product and other DICOM conformant equipment.

-  Test procedures should be defined and executed to validate the
   required level of interoperability with specific compatible DICOM
   equipment, as established by the healthcare facility.

If the product has an IHE Integration Statement, the following statement
may be applicable:

<Product Name> has participated in an industry-wide testing program
sponsored by Integrating the Healthcare Enterprise (IHE). The IHE
Integration Statement for <Product Name>, together with the IHE
Technical Framework, may facilitate the process of validation testing.

.. _sect_A.3.4:

Terms and Definitions
~~~~~~~~~~~~~~~~~~~~~

Terms and definitions should be listed here. The following example may
be used as a template:

Informal definitions are provided for the following terms used in this
Conformance Statement. The DICOM Standard is the authoritative source
for formal definitions of these terms.

Abstract Syntax
The information agreed to be exchanged between applications, generally
equivalent to a Service/Object Pair (SOP) Class. Examples: Verification
SOP Class, Modality Worklist Information Model Find SOP Class, Computed
Radiography Image Storage SOP Class.

Application Entity
AE
An end point of a DICOM information exchange, including the DICOM
network or media interface software; i.e., the software that sends or
receives DICOM information objects or messages. A single device may have
multiple Application Entities.

Application Entity Title
AET
The externally known name of an *Application Entity*, used to identify a
DICOM application to other DICOM applications on the network.

Application Context
The specification of the type of communication used between *Application
Entities*. Example: DICOM network protocol.

Association
A network communication channel set up between *Application Entities*.

Attribute
A unit of information in an object definition; a data element identified
by a *tag*. The information may be a complex data structure (Sequence),
itself composed of lower level data elements. Examples: Patient ID
(0010,0020), Accession Number (0008,0050), Photometric Interpretation
(0028,0004), Procedure Code Sequence (0008,1032).

Information Object Definition
IOD
The specified set of *Attributes* that comprise a type of data object;
does not represent a specific instance of the data object, but rather a
class of similar data objects that have the same properties. The
*Attributes* may be specified as Mandatory (Type 1), Required but
possibly unknown (Type 2), or Optional (Type 3), and there may be
conditions associated with the use of an Attribute (Types 1C and 2C).
Examples: MR Image IOD, CT Image IOD, Print Job IOD.

Joint Photographic Experts Group
JPEG
A set of standardized image compression techniques, available for use by
DICOM applications.

Media Application Profile
The specification of DICOM information objects and encoding exchanged on
removable media (e.g., CDs).

Module
A set of *Attributes* within an *Information Object Definition* that are
logically related to each other. Example: Patient Module includes
Patient Name, Patient ID, Patient Birth Date, and Patient Sex.

Negotiation
First phase of *Association* establishment that allows *Application
Entities* to agree on the types of data to be exchanged and how that
data will be encoded.

Presentation Context
The set of DICOM network services used over an *Association*, as
negotiated between *Application Entities*; includes *Abstract Syntaxes*
and *Transfer Syntaxes*.

Protocol Data Unit
PDU
A packet (piece) of a DICOM message sent across the network. Devices
must specify the maximum size packet they can receive for DICOM
messages.

Security Profile
A set of mechanisms, such as encryption, user authentication, or digital
signatures, used by an *Application Entity* to ensure confidentiality,
integrity, and/or availability of exchanged DICOM data.

Service Class Provider
SCP
Role of an *Application Entity* that provides a DICOM network service;
typically, a server that performs operations requested by another
*Application Entity* (*Service Class User*). Examples: Picture Archiving
and Communication System (image storage SCP, and image query/retrieve
SCP), Radiology Information System (modality worklist SCP).

Service Class User
SCU
Role of an *Application Entity* that uses a DICOM network service;
typically, a client. Examples: imaging modality (image storage SCU, and
modality worklist SCU), imaging workstation (image query/retrieve SCU).

Service/Object Pair Class
SOP Class
The specification of the network or media transfer (service) of a
particular type of data (object); the fundamental unit of DICOM
interoperability specification. Examples: Ultrasound Image Storage
Service, Basic Grayscale Print Management.

Service/Object Pair Instance
SOP Instance
An information object; a specific occurrence of information exchanged in
a *SOP Class*. Examples: a specific x-ray image.

Tag
A 32-bit identifier for a data element, represented as a pair of four
digit hexadecimal numbers, the "group" and the "element". If the "group"
number is odd, the tag is for a private (manufacturer-specific) data
element. Examples: (0010,0020) [Patient ID], (07FE,0010) [Pixel Data],
(0019,0210) [private data element].

Transfer Syntax
The encoding used for exchange of DICOM information objects and
messages. Examples: *JPEG* compressed (images), little endian explicit
value representation.

Unique Identifier
UID
A globally unique "dotted decimal" string that identifies a specific
object or a class of objects; an ISO-8824 Object Identifier. Examples:
Study Instance UID, SOP Class UID, SOP Instance UID.

Value Representation
VR
The format type of an individual DICOM data element, such as text, an
integer, a person's name, or a code. DICOM information objects can be
transmitted with either explicit identification of the type of each data
element (Explicit VR), or without explicit identification (Implicit VR);
with Implicit VR, the receiving application must use a DICOM data
dictionary to look up the format of each data element.

.. _sect_A.3.5:

Basics of DICOM Communication
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

A layman's introduction to DICOM may be included here. The following
example may be used as a template:

This section describes terminology used in this Conformance Statement
for the non-specialist. The key terms used in the Conformance Statement
are highlighted in *italics* below. This section is not a substitute for
training about DICOM, and it makes many simplifications about the
meanings of DICOM terms.

Two *Application Entities* (devices) that want to communicate with each
other over a network using DICOM protocol must first agree on several
things during an initial network "handshake". One of the two devices
must initiate an *Association* (a connection to the other device), and
ask if specific services, information, and encoding can be supported by
the other device (*Negotiation*).

DICOM specifies a number of network services and types of information
objects, each of which is called an *Abstract Syntax* for the
Negotiation. DICOM also specifies a variety of methods for encoding
data, denoted *Transfer Syntaxes*. The Negotiation allows the initiating
Application Entity to propose combinations of Abstract Syntax and
Transfer Syntax to be used on the Association; these combinations are
called *Presentation Contexts*. The receiving Application Entity accepts
the Presentation Contexts it supports.

For each Presentation Context, the Association Negotiation also allows
the devices to agree on *Roles* - which one is the *Service Class User*
(SCU - client) and which is the *Service Class Provider* (SCP - server).
Normally the device initiating the connection is the SCU, i.e., the
client system calls the server, but not always.

The Association Negotiation finally enables exchange of maximum network
packet (*PDU*) size, security information, and network service options
(called *Extended Negotiation* information).

The Application Entities, having negotiated the Association parameters,
may now commence exchanging data. Common data exchanges include queries
for worklists and lists of stored images, transfer of image objects and
analyses (structured reports), and sending images to film printers. Each
exchangeable unit of data is formatted by the sender in accordance with
the appropriate *Information Object Definition*, and sent using the
negotiated Transfer Syntax. There is a Default Transfer Syntax that all
systems must accept, but it may not be the most efficient for some use
cases. Each transfer is explicitly acknowledged by the receiver with a
*Response Status* indicating success, failure, or that query or retrieve
operations are still in process.

Two Application Entities may also communicate with each other by
exchanging media (such as a CD-R). Since there is no Association
Negotiation possible, they both use a *Media Application Profile* that
specifies "pre-negotiated" exchange media format, Abstract Syntax, and
Transfer Syntax.

.. _sect_A.3.6:

Abbreviations
~~~~~~~~~~~~~

Abbreviations should be listed here. These may be taken from the
following list, deleting terms that are not used within the Conformance
Statement, and adding any additional terms that are used:

AE
   Application Entity

AET
   Application Entity Title

CAD
   Computer Aided Detection

CDA
   Clinical Document Architecture

CD-R
   Compact Disk Recordable

CSE
   Customer Service Engineer

CR
   Computed Radiography

CT
   Computed Tomography

DHCP
   Dynamic Host Configuration Protocol

DICOM
   Digital Imaging and Communications in Medicine

DIT
   Directory Information Tree (LDAP)

DN
   Distinguished Name (LDAP)

DNS
   Domain Name System

DX
   Digital X-ray

FSC
   File-Set Creator

FSU
   File-Set Updater

FSR
   File-Set Reader

GSDF
   Grayscale Standard Display Function

GSPS
   Grayscale Softcopy Presentation State

HIS
   Hospital Information System

HL7
   Health Level 7 Standard

IHE
   Integrating the Healthcare Enterprise

IOD
   Information Object Definition

IPv4
   Internet Protocol version 4

IPv6
   Internet Protocol version 6

ISO
   International Organization for Standards

IO
   Intra-oral X-ray

JPEG
   Joint Photographic Experts Group

LDAP
   Lightweight Directory Access Protocol

LDIF
   LDAP Data Interchange Format

LUT
   Look-up Table

MAR
   Medication Administration Record

MPEG
   Moving Picture Experts Group

MG
   Mammography (X-ray)

MPPS
   Modality Performed Procedure Step

MR
   Magnetic Resonance Imaging

MSPS
   Modality Scheduled Procedure Step

MTU
   Maximum Transmission Unit (IP)

MWL
   Modality Worklist

NM
   Nuclear Medicine

NTP
   Network Time Protocol

O
   Optional (Key Attribute)

OP
   Ophthalmic Photography

OSI
   Open Systems Interconnection

PACS
   Picture Archiving and Communication System

PET
   Positron Emission Tomography

PDU
   Protocol Data Unit

R
   Required (Key Attribute)

RDN
   Relative Distinguished Name (LDAP)

RF
   Radiofluoroscopy

RIS
   Radiology Information System.

RT
   Radiotherapy

SC
   Secondary Capture

SCP
   Service Class Provider

SCU
   Service Class User

SOP
   Service-Object Pair

SPS
   Scheduled Procedure Step

SR
   Structured Reporting

TCP/IP
   Transmission Control Protocol/Internet Protocol

U
   Unique (Key Attribute)

UL
   Upper Layer

US
   Ultrasound

VL
   Visible Light

VR
   Value Representation

XA
   X-ray Angiography

.. _sect_A.3.7:

References
~~~~~~~~~~

Referenced documents should be listed here, including appropriate
product manuals (such as service manuals that specify how to set DICOM
communication parameters). References to the DICOM Standard should
provide the URL for the free published version of the Standard, but
should not specify a date of publication:

NEMA PS3 Digital Imaging and Communications in Medicine (DICOM)
Standard, available free at http://medical.nema.org/

.. _sect_A.4:

Networking
----------

This section contains the networking related services (vs. the media
related ones).

.. _sect_A.4.1:

Implementation Model
~~~~~~~~~~~~~~~~~~~~

The Implementation model consists of three sections: the Application
Data Flow Diagram, specifying the relationship between the Application
Entities and the "external world" or Real-World activities, a functional
description of each Application Entity, and the sequencing constraints
among them.

.. _sect_A.4.1.1:

Application Data Flow
^^^^^^^^^^^^^^^^^^^^^

As part of the Implementation model, an Application Data Flow Diagram
shall be included. This diagram represents all of the Application
Entities present in an implementation, and graphically depicts the
relationship of the AEs use of DICOM to Real-World Activities as well as
any applicable User interaction. `figure_title <#figure_A.4.1-1>`__ is a
template for such a Data Flow Diagram.

In this illustration, according to figure A.4.1-1, an occurrence of
local Real-World Activity A will cause local Application Entity <1> to
initiate an association for the purpose of causing Real-World Activity X
to occur remotely. It also shows that Real-World Activities B and Y are
interactively related via Application Entity <2>, with B being local and
Y Remote, and that local Application Entity 3 expects to receive an
association request when remote Real-World Activity Z occurs so that it
can perform Real-World Activity C and/or D. When the performance of
Real-World activities relies on interactions within the implementation,
one may depict the circles as overlapping as shown in
`figure_title <#figure_A.4.1-1>`__. Any such overlap shall be discussed
in this section of a Conformance Statement.

Typically, there is a one to one relationship between an AE and an AE
Title. Devices may be capable of configuring the relationship between AE
and AE Title (e.g., by merging Application Entities to use a single AE
Title). This is specified in the configuration section.

The Application Data Flow Diagram shall contain overview text with one
bullet per AE. Each bullet should provide an overview of each one of the
AEs, in relationship to their real-world activities, AE network
exchanges and external real-world activities.

.. note::

   There is no standard definition or guidelines on the number of AEs
   within a product and what an AE should encompass. Its functionality
   and scope is purely to the discretion of the vendor and typically
   depending on the system architecture.

.. _sect_A.4.1.2:

Functional Definition of AEs
^^^^^^^^^^^^^^^^^^^^^^^^^^^^

This Part shall contain a functional definition for each individual
local Application Entity. This shall describe in general terms the
functions to be performed by the AE, and the DICOM services used to
accomplish these functions. In this sense, "DICOM services" refers not
only to DICOM Service Classes, but also to lower level DICOM services,
such as Association Services.

.. _sect_A.4.1.2.1:

Functional Definition of "Application Entity <1>"
'''''''''''''''''''''''''''''''''''''''''''''''''

Functional description of "Application Entity <1>" (substitute actual AE
name), i.e., what is it that the AE performs.

.. _sect_A.4.1.2.2:

Functional Definition of "Application Entity <2>"
'''''''''''''''''''''''''''''''''''''''''''''''''

Same for "Application Entity <2>".

.. _sect_A.4.1.2.3:

Functional Definition of "Application Entity <3>"
'''''''''''''''''''''''''''''''''''''''''''''''''

Same for "Application Entity <3>".

.. _sect_A.4.1.3:

Sequencing of Real World Activities
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

If applicable, this section shall contain a description of sequencing as
well as potential constraints, of Real-World Activities, including any
applicable user interactions, as performed by all the Application
Entities. A UML sequence diagram, which depicts the Real-World
Activities as vertical bars and shows the events exchanged between them
as arrows, is strongly recommended.

.. _sect_A.4.2:

AE Specifications:
~~~~~~~~~~~~~~~~~~

The next section in the DICOM Conformance Statement is a set of
Application Entity Specifications. There shall be one such specification
for each Application Entity. Each individual AE Specification has a
subsection, A.4.2.x. There are as many of these subsections as there are
different AEs in the implementation. That is, if there are two distinct
AEs, then there will be two subsections, A.4.2.1, and A.4.2.2.

.. _sect_A.4.2.1:

"Application Entity <1>"
^^^^^^^^^^^^^^^^^^^^^^^^

Every detail of this specific Application Entity shall be completely
specified under this section.

AEs that utilize the DIMSE services shall have the following sections.

.. note::

   AEs that utilize other services are described later, and will re-use
   this section numbering.

.. _sect_A.4.2.1.1:

SOP Classes
'''''''''''

The specification for an Application Entity shall contain a statement of
the form:

"This Application Entity provides Standard Conformance to the following
SOP Class(es) :"

.. table:: SOP Class(Es) for "Application Entity <1>"

   +------------------------+---------------------+--------+--------+
   | SOP Class Name         | SOP Class UID       | SCU    | SCP    |
   +========================+=====================+========+========+
   | SOP Class UID Name as  | UID as specified in | Yes/No | Yes/No |
   | specified in the       |                     |        |        |
   | registry table of      |                     |        |        |
   | DICOM Unique           |                     |        |        |
   | Identifiers (UID) in , |                     |        |        |
   | with phrase "and       |                     |        |        |
   | specializations" as    |                     |        |        |
   | appropriate            |                     |        |        |
   +------------------------+---------------------+--------+--------+

.. note::

   Any SOP specific behavior is documented later in the conformance
   statement in the applicable SOP specific conformance section.

.. _sect_A.4.2.1.2:

Association Policies
''''''''''''''''''''

Each AE Specification shall contain a description of the General
Association Establishment and Acceptance policies of the AE.

.. _sect_A.4.2.1.2.1:

General
       

The DICOM standard Application context shall be specified.

.. table:: DICOM Application Context

   ======================== =====================
   Application Context Name 1.2.840.10008.3.1.1.1
   ======================== =====================

.. _sect_A.4.2.1.2.2:

Number of Associations.
                       

The number of simultaneous associations, which an Application Entity may
support as a SCU or SCP, shall be specified. Any rules governing
simultaneity of associations shall be defined here.

.. note::

   For example an AE may have the capability to have up to 10
   simultaneous associations, but may limit itself to have no more than
   2 with any particular other AE. There may also be policies based upon
   combinations of simultaneous Real-World Activities.

.. table:: Number of Associations as an Association Initiator for
"Application Entity <1>"

   =========================================== =
   Maximum number of simultaneous associations x
   =========================================== =

.. table:: Number of Associations as an Association Acceptor for
"Application Entity <1>"

   =========================================== =
   Maximum number of simultaneous associations x
   =========================================== =

.. _sect_A.4.2.1.2.3:

Asynchronous Nature
                   

If the implementation supports negotiation of multiple outstanding
transactions, this shall be stated here, along with the maximum number
of outstanding transactions supported.

.. table:: Asynchronous Nature as an Association Initiator for
"Application Entity <1>"

   ======================================================= =
   Maximum number of outstanding asynchronous transactions x
   ======================================================= =

.. _sect_A.4.2.1.2.4:

Implementation Identifying Information
                                      

The value supplied for Implementation Class UID shall be documented
here. If a version name is supplied, this fact shall be documented here.
Policies defining the values supplied for version name may be stated
here.

.. table:: DICOM Implementation Class and Version for "Application
Entity <1>"

   =========================== ====================
   Implementation Class UID    a.b.c.xxxxxxx.yyy.zz
   Implementation Version Name XYZxyz
   =========================== ====================

.. _sect_A.4.2.1.3:

Association Initiation Policy
'''''''''''''''''''''''''''''

This describes the conditions under which the AE will initiate an
association.

.. _sect_A.4.2.1.3.1:

"Activity <1>"
              

.. _sect_A.4.2.1.3.1.1:

Description and Sequencing of Activities
                                        

If applicable, this section shall contain a description of sequencing of
the events for "Activity <1>" (substitute actual activity name),
including any applicable user interactions, which this specific AE
performs. A UML sequence diagram, which depicts the Application Entity
and Real-World Activities as vertical bars and shows the events
exchanged between them as arrows, is strongly recommended.

.. note::

   An example of a situation in which such a description is required is
   an AE, which supports both the Storage Service Class and the Modality
   Performed Procedure SOP Class. Some implementations might store the
   images before sending the final MPPS N-SET message while other
   implementations might send the final MPPS N-SET message before
   sending the images.

.. _sect_A.4.2.1.3.1.2:

Proposed Presentation Contexts
                              

Each time an association is initiated, the Association Initiator
proposes a number of Presentation Contexts to be used on that
association. In this subsection, the Presentation Contexts proposed by
"Application Entity <1>" for "Activity <1>" shall be defined in a table
with the following format:

.. table:: Proposed Presentation Contexts for "Application Entity <1>"

   +----------+----------+----------+----------+----------+----------+
   | Pres     |          |          |          |          |          |
   | entation |          |          |          |          |          |
   | Context  |          |          |          |          |          |
   | Table    |          |          |          |          |          |
   +==========+==========+==========+==========+==========+==========+
   | name_a   | AS_UID_a | XS       | X        | SCP \|   | None     |
   |          |          | _Name_1, | S_UID_1, | SCU \|   | \|See    |
   |          |          | ...,     | \_,      | BOTH     | Note <1> |
   |          |          | X        | XS_UID_n |          | \| See   |
   |          |          | S_Name_n |          |          | `table_t |
   |          |          |          |          |          | itle <#t |
   |          |          |          |          |          | able_A.4 |
   |          |          |          |          |          | .2-8>`__ |
   +----------+----------+----------+----------+----------+----------+
   | ...      | ...      | ...      | ...      | ...      | ...      |
   +----------+----------+----------+----------+----------+----------+

.. note::

   <1>: <Describe the content of any extended negotiation done for the
   SOP Classes of this Presentation Context. One note may serve multiple
   Presentation Contexts, as a single Abstract Syntax often corresponds
   to a single SOP class, which may appear in different Presentation
   Contexts.>

In `table_title <#table_A.4.2-7>`__, the following meanings are assigned
to the fields:

-  <name_a> This is the name of the Abstract Syntax to be used with this
   Presentation Context.

-  <AS_UID_a> This is the UID of the Abstract Syntax to be used for this
   Presentation Context.

-  <XS_Name_n> This is the name of a Transfer Syntax that may be used
   for this Presentation Context.

-  <XS_UID_n> The UID of the corresponding Transfer Syntax.

If the AE through this Real World Activity might propose any of the SOP
Classes of a particular Service Class (e.g., the Storage Service Class),
the Abstract Syntax Name and UID shall be those of the Service Class.
This section shall describe the conditions under which a SOP Class of
that Service Class will be proposed in a Presentation Context.

.. note::

   For instance, an AE may receive instances of a non-preconfigured SOP
   Class through support of SOP Class Common Extended Negotiation. These
   instances may be limited to specializations of a particular SOP
   Class, or they may be any SOP Class within the Service Class, and any
   such limits should be described.

This section shall describe the conditions under which the AE may change
the SOP Class UID of SOP Instances sent, due to fall-back mechanisms.

.. note::

   For instance, if the SCP does not accept the proposed Abstract Syntax
   (SOP Class) for which there is a Related General SOP Class that was
   accepted, the AE may modify SOP Instances of the refused SOP Class to
   use the Related General SOP Class for transmission.

In the event that the Abstract Syntax of the Presentation Context
represents a Meta-SOP Class (that is, it includes many SOP Classes) and
extended negotiation is supported for some of these SOP Classes, the
following table is required to define this extended negotiation. This
table is referenced in `table_title <#table_A.4.2-7>`__:

.. table:: Extended Negotiation as a SCU

   ============== ============= ====================
   SOP Class Name SOP Class UID Extended Negotiation
   ============== ============= ====================
   Name_i         SOP_UID_I     None \| See Note <1>
   ...            ...           ...
   ============== ============= ====================

.. note::

   <1>: <Describe the content of any extended negotiation done for this
   SOP Class. One note may serve multiple Presentation Contexts, as a
   SOP class that may appear in different Presentation Contexts and/or
   Meta SOP Classes>

The implementation of the initiator shall document which Transfer Syntax
will be chosen in case multiple Transfer Syntaxes are accepted during
the Association Acceptance.

.. _sect_A.4.2.1.3.1.3:

SOP Specific Conformance for SOP Class(Es)
                                          

This section includes the SOP specific behavior, i.e., error codes,
error and exception handling, time-outs, etc. The information shall be
as described in the SOP specific Conformance Statement section of (or
relevant private SOP definition). It shall include the content of any
extended negotiation. Keys shall be specified including how they are
used (Matching, return keys, interactive query, whether they are
displayed to the user, universal and/or list matching, etc.).

In particular, the behavior associated with the exchange of images
available to the AE only in a lossy compressed form shall be documented.
For example, if a lossy compressed transfer syntax is not negotiated,
will the AE decompress the image data and send it using one of the
negotiated transfer syntaxes.

All details regarding the specific conformance, including response
behavior to all status codes, both from an application level and
communication errors shall be provided in the form of a table as
follows:

.. table:: DICOM Command Response Status Handling Behavior

   +----------------+-----------------+------------+-----------------+
   | Service Status | Further Meaning | Error Code | Behavior        |
   +================+=================+============+=================+
   | e.g., Success  | e.g., Matching  | e.g., 0000 | e.g., The SCP   |
   |                | is complete     |            | has             |
   |                |                 |            | successfully    |
   |                |                 |            | returned all    |
   |                |                 |            | matching        |
   |                |                 |            | information.    |
   +----------------+-----------------+------------+-----------------+
   | Warning        |                 |            |                 |
   +----------------+-----------------+------------+-----------------+
   | Error          |                 |            |                 |
   +----------------+-----------------+------------+-----------------+
   | …..            |                 |            |                 |
   +----------------+-----------------+------------+-----------------+

The behavior of the AE during communication failure is summarized in a
table as follows:

.. table:: DICOM Command Communication Failure Behavior

   +---------------------------+-----------------------------------------+
   | Exception                 | Behavior                                |
   +===========================+=========================================+
   | e.g., Timeout             | e.g., The Association is aborted using  |
   |                           | A-ABORT and command marked as failed.   |
   |                           | The reason is logged and reported to    |
   |                           | the user.                               |
   +---------------------------+-----------------------------------------+
   | e.g., Association aborted | e.g., The command is marked as failed.  |
   |                           | The reason is logged and reported to    |
   |                           | the user.                               |
   +---------------------------+-----------------------------------------+

.. _sect_A.4.2.1.4:

Association Acceptance Policy
'''''''''''''''''''''''''''''

Each AE Specification shall contain a description of the Association
Acceptance policies of the AE. This describes the conditions under which
the AE will accept an association.

.. _sect_A.4.2.1.4.1:

"Activity <2>"
              

.. _sect_A.4.2.1.4.1.1:

Description and Sequencing of Activities
                                        

.. _sect_A.4.2.1.4.1.2:

Accepted Presentation Contexts
                              

.. table:: Acceptable Presentation Contexts For"Application Entity <1>"
and "Activity <2>"

   +----------+----------+----------+----------+----------+----------+
   | Pres     |          |          |          |          |          |
   | entation |          |          |          |          |          |
   | Context  |          |          |          |          |          |
   | Table    |          |          |          |          |          |
   +==========+==========+==========+==========+==========+==========+
   | name_a   | AS_UID_a | X        | XS_UID_a | SCP \|   | None     |
   |          |          | S_Name_a |          | SCU \|   | \|See    |
   |          |          |          |          | Both     | Note     |
   |          |          |          |          |          | <1>\|    |
   |          |          |          |          |          | See      |
   |          |          |          |          |          | `        |
   |          |          |          |          |          | table_ti |
   |          |          |          |          |          | tle <#ta |
   |          |          |          |          |          | ble_A.4. |
   |          |          |          |          |          | 2-12>`__ |
   +----------+----------+----------+----------+----------+----------+
   | ...      | ...      | ...      | ...      | ...      | ...      |
   +----------+----------+----------+----------+----------+----------+

.. note::

   <1>: <Describe the content of any extended negotiation done for the
   SOP Classes of this Presentation Context. In particular, acceptance
   of specialized SOP Classes of the Abstract Syntax specified in this
   Presentation Context shall be noted. One note may serve multiple
   Presentation Contexts, as a single Abstract Syntax often corresponds
   to a single SOP class, which may appear in different Presentation
   Contexts>

In `table_title <#table_A.4.2-11>`__, the following meanings are
assigned to the fields:

<name_a> This is the name of the Abstract Syntax to be used with this
Presentation Context.

<AS_UID_a> This is the UID of the Abstract Syntax to be used for this
Presentation Context.

<XS_Name_a> This is the name of a Transfer Syntax that may be used for
this Presentation Context.

<XS_UID_a> The UID of the corresponding transfer syntax.

If the AE through this Real World Activity supports all SOP Classes of a
particular Service Class (e.g., the Storage Service Class) through SOP
Class Common Extended Negotiation, the Abstract Syntax Name and UID
shall be those of the Service Class, and this shall be noted under
Extended Negotiation.

In the event that the Abstract Syntax of the Presentation Context
represents a Meta-SOP Class (that is, it includes many SOP Classes) and
extended negotiation is supported for some of these SOP Classes, the
following table is required to define this extended negotiation. This
table is referenced in `table_title <#table_A.4.2-11>`__

.. table:: Extended Negotiation as a SCP

   ============== ============= ====================
   SOP Class name SOP Class UID Extended Negotiation
   ============== ============= ====================
   Name_i         SOP_UID_I     None \| See Note <1>
   ...            ...           ...
   ============== ============= ====================

.. note::

   <1>: <Describe the content of any extended negotiation done for this
   SOP Class. One note may serve multiple Presentation Contexts, as a
   SOP class, which may appear in different Presentation Contexts,
   and/or Meta SOP Classes>

Any rules that govern the acceptance of presentation contexts for this
AE shall be stated here as well. This includes rules for which
combinations of Abstract/Transfer Syntaxes are acceptable, and rules for
prioritization of presentation contexts. Rules that govern selection of
transfer syntax within a presentation context shall be stated here.

.. _sect_A.4.2.1.4.1.3:

SOP Specific Conformance for SOP Class(Es)
                                          

This section includes the SOP specific behavior, i.e., error codes,
error and exception handling, time-outs, etc. The information shall be
as described in the SOP specific Conformance Statement section of (or
relevant private SOP definition).

The behavior of an Application Entity shall be summarized as shown in
`table_title <#table_4.2-13>`__. Standard as well as the manufacturer
specific status codes and their corresponding behavior shall be
specified.

.. table:: Storage C-STORE Response Status

   ============== ================================= ========== =======
   Service Status Further Meaning                   Error Code Reason
   ============== ================================= ========== =======
   Success        Success                           0000       Explain
   Refused        Out of Resources                  A700-A7FF  Explain
   Error          Data Set does not match SOP Class A900-A9FF  Explain
   Error          Specify                           Specify    Explain
   Warning        Specify                           Specify    Explain
   ============== ================================= ========== =======

.. _sect_A.4.2.2:

"Application Entity <1>"
^^^^^^^^^^^^^^^^^^^^^^^^

An Application Entity that supports Web services shall have the
following sections:

Details of this specific Application Entity shall be specified under
this section.

.. _sect_A.4.2.2.1:

Retired
'''''''

See PS3.2-2017b.

.. _sect_A.4.2.2.2:

WADO-URI Specifications
'''''''''''''''''''''''

All WADO-URI services that are supported shall be listed. Other WADO-URI
services that are not supported may be indicated.

For each supported service, the parameters and restrictions on those
parameters shall be described.

Any connection policies such as restrictions on the number of
connections, support for pipeline requests, etc. shall be described.

.. _sect_A.4.2.2.3:

Restful Services Specifications
'''''''''''''''''''''''''''''''

All RESTful services that are supported shall be listed. Other RESTful
services that are not supported may be indicated.

For each supported service, the parameters and restrictions on those
parameters shall be described.

Any connection policies such as restrictions on the number of
connections, support for pipeline requests, etc. shall be described.

.. _sect_A.4.2.3:

"Application Entity <2>"
^^^^^^^^^^^^^^^^^^^^^^^^

The same info shall be repeated for each additional AE.

.. _sect_A.4.3:

Network Interfaces
~~~~~~~~~~~~~~~~~~

.. _sect_A.4.3.1:

Physical Network Interface
^^^^^^^^^^^^^^^^^^^^^^^^^^

If applicable, specifies what physical network interface(s) are
supported.

.. _sect_A.4.3.2:

Additional Protocols
^^^^^^^^^^^^^^^^^^^^

Additional protocols such as used for configuration management are
listed here. Any conformance to specific System Management Profiles
defined in shall be listed per the following table.

.. table:: System Management Profiles Table

   +-------------+----------+-------------+-------------+-------------+
   | Profile     | Actor    | Protocols   | Optional    | Security    |
   | Name        |          | Used        | T           | Support     |
   |             |          |             | ransactions |             |
   +=============+==========+=============+=============+=============+
   | Profile (1) | P Client | Protocol_1, | N/A         |             |
   |             |          | Protocol_2  |             |             |
   +-------------+----------+-------------+-------------+-------------+
   | Profile (x) | X Client | Protocol_2, | Protocol_3  |             |
   |             |          | Protocol_3  | Option_A    |             |
   |             |          |             | supported   |             |
   +-------------+----------+-------------+-------------+-------------+

If the implementation conforms to the Basic Network Address Management
Profile as a DHCP Client actor (see ), the use of DHCP to configure the
local IP address and hostname shall be described.

.. note::

   The hostname is an alias for the IP address, and has no semantic
   relationship to AE titles. It is solely a convenience for
   configuration description.

If the implementation conforms to the Basic Network Address Management
Profile as a DNS Client actor (see ), the use of DNS to obtain IP
addresses from hostname information shall be described.

If the implementation conforms to the Basic Time Synchronization profile
as an NTP Client or SNTP Client, the available NTP configuration
alternatives shall be described. If the implementation conforms to the
Basic Time Synchronization Profile as an NTP Server, the available
server configuration alternatives shall be described. Any device
specific requirements for accuracy or maximum allowable synchronization
error shall be described.

If there is support for WADO (see ) the options supported and any
restrictions shall be described.

.. _sect_A.4.3.3:

IPv4 and IPv6 Support
'''''''''''''''''''''

The support for specific IPv4 and IPv6 features and associated optional
IPv6 security and configuration facilities shall be documented.

.. _sect_A.4.4:

Configuration
~~~~~~~~~~~~~

Any implementation's DICOM conformance may be dependent upon
configuration, which takes place at the time of installation. Issues
concerning configuration shall be addressed in this section.

.. _sect_A.4.4.1:

AE Title/Presentation Address Mapping
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

An important installation issue is the translation from AE title to
Presentation Address. How this is to be performed shall be described in
this section.

.. note::

   There does not necessarily have to be a one to one relationship
   between AE titles and Application Entities. If so, this should be
   made clear in the tables.

.. _sect_A.4.4.1.1:

Local AE Titles.
''''''''''''''''

The local AE title mapping and configuration shall be specified. The
following table shall be used:

.. table:: AE Title Configuration Table

   ================== ================ ===================
   Application Entity Default AE Title Default TCP/IP Port
   ================== ================ ===================
   AE (1)             Name             Specify
   AE (2)             Name             Specify
   AE (x)                              
   ================== ================ ===================

If the implementation conforms to the Application Configuration
Management Profile as an LDAP Client actor (see ), any use of LDAP to
configure the local AE titles shall be described. Any conformance to the
Update LDAP Server option shall be specified, together with the values
for all component object attributes in the update sent to the LDAP
Server.

.. _sect_A.4.4.1.2:

Remote AE Title/Presentation Address Mapping
''''''''''''''''''''''''''''''''''''''''''''

Configuration of remote host names and port numbers shall be specified
here.

.. _sect_A.4.4.1.2.1:

Remote SCP 1
            

Configuration of the remote AET port number, host-names, IP addresses
and capabilities shall be specified. If applicable, multiple remote SCPs
can be specified.

If the implementation conforms to the Application Configuration
Management Profile as an LDAP Client actor (see ), any use of LDAP to
configure the remote device addresses and capabilities shall be
described. The LDAP queries used to obtain remote device component
object attributes shall be specified.

.. note::

   In particular, use of LDAP to obtain the AE Title, TCP port, and IP
   address for specific system actors (e.g., an Image Archive, or a
   Performed Procedure Step Manager) should be detailed, as well as how
   the LDAP information for remote devices is selected for operational
   use.

.. _sect_A.4.4.1.2.2:

Remote SCP 2
            

Etc.

.. _sect_A.4.4.2:

Parameters
^^^^^^^^^^

The specification of important operational parameters, and if
configurable, their default value and range, shall be specified here.
The parameters that apply to all Application Entities should be
specified in a "General Parameters" section while those specific to
particular Application Entities should be specified in separate sections
specific to each AE. The following table, which is shown here with a
recommended baseline of parameters, shall be used:

.. table:: Configuration Parameters Table

   +-------------------------+-----------------------+---------------+
   | Parameter               | Configurable (Yes/No) | Default Value |
   +=========================+=======================+===============+
   | **General Parameters**  |                       |               |
   +-------------------------+-----------------------+---------------+
   | Time-out waiting for    |                       |               |
   | acceptance or rejection |                       |               |
   | Response to an          |                       |               |
   | Association Open        |                       |               |
   | Request. (Application   |                       |               |
   | Level timeout)          |                       |               |
   +-------------------------+-----------------------+---------------+
   | General DIMSE level     |                       |               |
   | time-out values         |                       |               |
   +-------------------------+-----------------------+---------------+
   | Time-out waiting for    |                       |               |
   | response to TCP/IP      |                       |               |
   | connect request.        |                       |               |
   | (Low-level timeout)     |                       |               |
   +-------------------------+-----------------------+---------------+
   | Time-out waiting for    |                       |               |
   | acceptance of a TCP/IP  |                       |               |
   | message over the        |                       |               |
   | network. (Low-level     |                       |               |
   | timeout)                |                       |               |
   +-------------------------+-----------------------+---------------+
   | Time-out for waiting    |                       |               |
   | for data between TCP/IP |                       |               |
   | packets. (Low-level     |                       |               |
   | timeout)                |                       |               |
   +-------------------------+-----------------------+---------------+
   | Any changes to default  |                       |               |
   | TCP/IP settings, such   |                       |               |
   | as configurable stack   |                       |               |
   | parameters.             |                       |               |
   +-------------------------+-----------------------+---------------+
   | Definition of           |                       |               |
   | arbitrarily chosen      |                       |               |
   | origins                 |                       |               |
   +-------------------------+-----------------------+---------------+
   | Definition of constant  |                       |               |
   | values used in Dose     |                       |               |
   | Related Distance        |                       |               |
   | Measurements            |                       |               |
   +-------------------------+-----------------------+---------------+
   | Other configurable      |                       |               |
   | parameters              |                       |               |
   +-------------------------+-----------------------+---------------+
   | **AE Specific           |                       |               |
   | Parameters**            |                       |               |
   +-------------------------+-----------------------+---------------+
   | Size constraint in      |                       |               |
   | maximum object size     |                       |               |
   | (see note)              |                       |               |
   +-------------------------+-----------------------+---------------+
   | Maximum PDU size the AE |                       |               |
   | can receive             |                       |               |
   +-------------------------+-----------------------+---------------+
   | Maximum PDU size the AE |                       |               |
   | can send                |                       |               |
   +-------------------------+-----------------------+---------------+
   | AE specific DIMSE level |                       |               |
   | time-out values         |                       |               |
   +-------------------------+-----------------------+---------------+
   | Number of simultaneous  |                       |               |
   | Associations by Service |                       |               |
   | and/or SOP Class        |                       |               |
   +-------------------------+-----------------------+---------------+
   | <SOP Class support>     |                       |               |
   | (e.g., Multi-frame vs.  |                       |               |
   | single frame vs. SC     |                       |               |
   | support), when          |                       |               |
   | configurable            |                       |               |
   +-------------------------+-----------------------+---------------+
   | <Transfer Syntax        |                       |               |
   | support>, e.g., JPEG,   |                       |               |
   | Explicit VR, when       |                       |               |
   | configurable            |                       |               |
   +-------------------------+-----------------------+---------------+
   | Other parameters that   |                       |               |
   | are configurable        |                       |               |
   +-------------------------+-----------------------+---------------+

.. note::

   In particular when accommodating Multi-frame objects (e.g.,
   Ultrasound Multi-frame, NM, XA, RF), a receiver might have a certain
   restriction with regard to its maximum length. This restriction
   should be specified here.

Additional configuration parameters such as hardware options for e.g., a
printer shall be specified as well.

.. _sect_A.5:

Media Interchange
-----------------

.. _sect_A.5.1:

Implementation Model
~~~~~~~~~~~~~~~~~~~~

The Implementation Model shall identify the DICOM Application Entities
in a specific implementation and relate the Application Entities to
Real-World Activities.

.. _sect_A.5.1.1:

Application Data Flow Diagram
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

As part of the Implementation Model, an Application Data Flow Diagram
shall be included. This diagram represents all of the Application
Entities present in an implementation and graphically depicts the
relationship of the AEs use of DICOM to real world activities.
`figure_title <#figure_A.5.1-1>`__ is a template for such a Data Flow
Diagram. Accompanying the Application Data Flow Diagram shall be a
discussion of the Application Data Flow represented.

In this illustration, according to `figure_title <#figure_A.5.1-1>`__,
an occurrence of local Real-World Activity A or B will cause the local
Application Entity 1 to initiate either creation of a File-set on a
medium (FSC) for the purpose of interchange with a remote Real-World
Activity X or to access a File-set on a medium for reading (FSR). The
remote Real-World Activity X accesses the medium physically transferred
from Real-World Activity A or B.

An occurrence of Real-World Activity C will cause the local Application
Entity 2 to update a File-set (FSU) on a mounted medium.

.. note::

   If the AE expects a remote Real-World Activity to access the media
   for a specific purpose, this should be shown in the Application Data
   Flow Diagram as well as described in Section `Application Data Flow
   Diagram <#sect_A.5.1.1>`__.

.. _sect_A.5.1.2:

Functional Definitions of AEs
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

The next part of the Conformance Statement shall contain a functional
definition for each local Application Entity. This shall describe in
general terms the functions to be performed by the AE, and the DICOM
services used to accomplish these functions. In this sense "DICOM
services" refers not only to DICOM Service Classes, but also to lower
level DICOM services, such as the Media File System and mapping to
particular Media Formats.

.. _sect_A.5.1.3:

Sequencing of Real World Activities
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

If applicable, this section shall contain a description of sequencing of
Real World Activities that the AEs require.

.. note::

   An example of a situation in which a such a description is required
   is an AE that supports roles as a File-set Updater and File-set
   Reader. In some instances, the File-set will be updated then read
   (e.g., for verification); and in other instances, may be read first
   to determine if the File-set needs to be updated.

.. _sect_A.5.1.4:

File Meta Information for Implementation Class and Version
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

This section shall be used to list the values assigned to the File Meta
Information attributes (see ) that pertain to the Implementation Class
and Version. These are:

-  File Meta Information Version

-  Implementation Class UID

-  Implementation Version Name

.. _sect_A.5.2:

AE Specifications
~~~~~~~~~~~~~~~~~

The next section in the DICOM Conformance Statement is a set of
Application Entity Specifications. There shall be one such specification
for each Application Entity type.

.. _sect_A.5.2.1:

"Application Entity <1>" - Specification
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

The following table, `table_title <#table_A.5.2-1>`__, shows that for
one or more Application Profiles in the first column, there are a number
of Real-World Activities in the second column and the roles required for
each of these Real-World Activities in the third column

.. table:: AE Related Application Profiles, Real-World Activities, and
Roles

   ============================= =================== ========
   Supported Application Profile Real-World Activity Roles
   ============================= =================== ========
   STD-AP1                       RWA A               FSR
   \                             RWA B               FSR, FSC
   STD-AP1, AUG-AP2, etc.        RWA C               FSU
   \                             RWA D               FSC
   ============================= =================== ========

This section shall also contain any general policies that apply to all
of the AEs described in subsequent section.

.. _sect_A.5.2.1.1:

File Meta Information for the "Application Entity <1>"
''''''''''''''''''''''''''''''''''''''''''''''''''''''

This section shall contain the values of the File Meta Information that
pertain to the Application Entity (see ). These are:

-  Source Application Entity Title

If Private Information is used in the Application Profile File Meta
Information, the following two File Meta Information attributes may be
documented:

-  Private Information Creator UID

-  Private Information

.. _sect_A.5.2.1.2:

Real-World Activities
'''''''''''''''''''''

The first sentence in this section shall state the Roles and Media
Storage Service Class Options supported by the "Application Entity <1>".

.. _sect_A.5.2.1.2.i:

"Real-World Activity <i>"
                         

The AE Specification shall contain a description of the Real-World
Activities, which invoke the particular AE. There will be one section,
A.5.2.1.2.i where i increments for each RWA, per Real-World Activity.

.. _sect_A.5.2.1.2.i.1:

Media Storage Application Profile
                                 

The Application Profile that is used by the AE described in A.5.2-1 is
specified in this section.

.. _sect_A.5.2.1.2.i.1.y:

Options
       

The options used in the Application Profiled specified in
`table_title <#table_A.5.2-1>`__ shall be detailed in this section.
There will be separate sections for each option specified for the AP. If
there are no options used in the Application Profile specified in
A.5.2.x, this section may be omitted.

.. _sect_A.5.2.2:

"Application Entity <2>" - Specification
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

Each individual AE Specification has a subsection, A.5.2.x. There are as
many of these subsections as there are different AEs in the
implementation. That is, if there are two distinct AEs, then there will
be two subsections, A.5.2.1, and A.5.2.2.

.. _sect_A.5.3:

Augmented and Private Application Profiles
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

This Section shall be used for the description of Augmented and Private
Application Profiles.

.. _sect_A.5.3.1:

Augmented Application Profiles
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

Any Augmented Application Profiles used by an AE shall be described in
these sections. The rules governing the structure of an Augmented AP
shall be described.

.. _sect_A.5.3.1.1:

"Augmented Application Profile <1>"
'''''''''''''''''''''''''''''''''''

Each Augmented Application Profile shall have a section A.5.3.1.x that
describes the specific features of the Application Profile that make it
Augmented. These shall be described in the three repeating sections that
follow.

.. _sect_A.5.3.1.1.1:

SOP Class Augmentations
                       

The additional SOP Classes beyond those specified in the Standard AP on
which this Augmented AP is based shall be detailed in this section.

.. _sect_A.5.3.1.1.2:

Directory Augmentations
                       

Any additions to the Directory IOD that augment this AP shall be
described in this section.

.. _sect_A.5.3.1.1.3:

Other Augmentations
                   

Any additions to, or extensions of the Application Profile shall be
described in this section. An example of such another augmentation is
addition of a role (FSR, FSC, FSU) to the Standard Application Profile
set of defined roles.

.. _sect_A.5.3.1.2:

"Augmented Application Profile <2>"
'''''''''''''''''''''''''''''''''''

To be repeated for the second, third, etc. Augmented Application
Profile.

.. _sect_A.5.3.2:

Private Application Profiles
^^^^^^^^^^^^^^^^^^^^^^^^^^^^

The rules that govern construction of a Private Application Profile
shall be described. This section shall be used to describe the details
of the Private AP.

.. note::

   1. Refer to for a description of constructing a Private Application
      Profile.

   2. If the AP deviates from the rules governing a Private AP in any
      manner, it is non-conformant and is outside the scope of this
      Standard.

.. _sect_A.5.4:

Media Configuration
~~~~~~~~~~~~~~~~~~~

Any implementation's DICOM conformance may be dependent upon
configuration that takes place at the time of installation. Issues
concerning configuration shall be addressed in this section (e.g., the
configuration of the Source AE Title in File Meta Information).

.. _sect_A.6:

Transformation of DICOM to CDA
------------------------------

The supported SR objects and corresponding template identifiers shall be
described. The release version and template identifier of the generated
valid CDA documents shall be documented. The transformation process may
be described by reference to a specific Annex of .

.. _sect_A.7:

Support of Character Sets
-------------------------

Any support for Character Sets beyond the Default Character Repertoire
in Network and Media Services shall be described here.

-  The behavior when an unsupported character set is received shall be
   documented.

-  Character set configuration capabilities, if any, shall be specified.

-  Mapping and/or conversion of character sets across Services and
   Instances shall be specified.

-  Query capabilities for attributes that include non-default character
   sets, both for the Worklist service class and Query service class
   shall be specified. Behavior of attributes using extended character
   sets by a C-FIND, both as SCU and SCP request and response, shall be
   specified. In particular the handling of Person Names (VR of PN)
   shall be specified.

-  The presentation of the characters to a user, i.e., capabilities,
   font limitations and/or substitutions shall be specified.

.. _sect_A.8:

Security
--------

.. _sect_A.8.1:

Security Profiles
~~~~~~~~~~~~~~~~~

Any support for Security Profiles as defined in shall be described here.
Any extensions to Security Profiles shall be described, e.g., extended
schema for audit trail messages.

An implementation shall declare which level of security features it
supports, including such things as:

a. The conditions under which the implementation preserves the integrity
   of Digital Signatures (e.g., is the implementation bit-preserving).

b. The conditions under which the implementation verifies incoming
   Digital Signatures.

c. The conditions under which the implementation replaces Digital
   Signatures.

d. IPv6 Security capabilities

.. _sect_A.8.2:

Association Level Security
~~~~~~~~~~~~~~~~~~~~~~~~~~

Any support for security at the Association level (e.g., allowing only
certain AE-titles and/or IP addresses to open an Association) shall be
specified here.

.. _sect_A.8.3:

Application Level Security
~~~~~~~~~~~~~~~~~~~~~~~~~~

Any support for additional application level security as it applies to
the DICOM communication (e.g., passwords, biometrics) can be described
here.

.. _sect_A.9:

Annexes
-------

.. _sect_A.9.1:

IOD Contents
~~~~~~~~~~~~

.. _sect_A.9.1.1:

Created SOP Instance(s)
^^^^^^^^^^^^^^^^^^^^^^^

This section specifies each IOD created (including Private IODs). It
should specify the Attribute Name, tag, VR, and Value. The Value should
specify the range and source (e.g., User input, Modality Worklist,
automatically generated, etc.). For content items in templates, the
range and source of the concept name and concept values should be
specified. Whether the value is always present or not shall be
specified.

Recommended abbreviations to be used for the tables are:

VNAP Value Not Always Present (attribute sent zero length if no value is
present)

ANAP Attribute Not Always Present

ALWAYS Always Present with a value

EMPTY Attribute is sent without a value

Recommended abbreviations to be used for the source of the data values
in the tables are:

USER the attribute value source is from User input

AUTO the attribute value is generated automatically

MWL,MPPS, etc. the attribute value is the same as the value received
using a DICOM service such as Modality Worklist, Modality Performed
Procedure Step, etc.

CONFIG the attribute value source is a configurable parameter

Specification of a company web address can refer to sample SOP Instances
that are available.

Private attributes should be specified.

.. _sect_A.9.1.2:

Usage of Attributes From Received IODs
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

Each Application that depends on certain fields to function correctly
should specify which ones are required for it to perform its intended
function.

.. _sect_A.9.1.3:

Attribute Mapping
^^^^^^^^^^^^^^^^^

When attributes are used by different SOP Classes, e.g., Modality
Worklist, Storage and Modality Performed Procedure Step, this mapping
shall be specified. For devices that specify other external protocols,
such as HL7, mapping of their fields into the DICOM attributes is not
required but highly recommended.

.. _sect_A.9.1.4:

Coerced/Modified Fields
^^^^^^^^^^^^^^^^^^^^^^^

A SCU might coerce certain Attributes, e.g., the Patient Name. A SCP
might provide a different value of an Attribute than was received. These
changes shall be specified here. An example is Patient Name, which could
be modified using available information from either an internal database
or obtained from an Information System/Information Manager. Another
example is the generation of a new SOP Instance UID for an existing
instance. The conditions influencing such coercion should be specified..

.. _sect_A.9.2:

Data Dictionary of Private Attributes
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

Any private Attributes should be specified, including their VR, VM and
which are known to be safe from identity leakage. Private SOP Classes
and Transfer syntaxes should be listed. Whether or not private
Attributes are described in Private Data Element Characteristics
Sequence (0008,0300) should be specified in `IOD
Contents <#sect_A.9.1>`__.

.. _sect_A.9.3:

Coded Terminology and Templates
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

Support for Coded Terminology and templates shall be described here.

.. _sect_A.9.3.1:

Context Groups
^^^^^^^^^^^^^^

Each Context Group (i.e., use of coded terminology in a specific
context) shall be specified here with its default value set, and whether
the value set is configurable. The configurable options are specified.

.. table:: Context Groups

   +----------------+----------------+----------------+----------------+
   | Context Group  | Default Value  | Configurable   | Use            |
   |                | Set            |                |                |
   +================+================+================+================+
   | Logical        | CID xxx \|     | No\|           | Description of |
   | Context        | extended CID   | Extensib       | method of      |
   | Identification | xxx \| Private | le|Replaceable | selection of a |
   |                | CID yyyy \|    |                | term from the  |
   |                | None           |                | Context Group, |
   |                |                |                | and            |
   |                |                |                | identification |
   |                |                |                | of the IOD,    |
   |                |                |                | Attribute,     |
   |                |                |                | and/or Content |
   |                |                |                | Item that uses |
   |                |                |                | the term       |
   +----------------+----------------+----------------+----------------+
   | e.g.,          | e.g., None     | e.g.,          | e.g., Value of |
   | Acquisition    |                | Replaceable    | Scheduled      |
   | Protocol       |                |                | Protocol Code  |
   | Equipment      |                |                | Sequence       |
   | Settings       |                |                | (0040,0008)    |
   |                |                |                | from selected  |
   |                |                |                | Modality       |
   |                |                |                | Worklist       |
   |                |                |                | Scheduled      |
   |                |                |                | Procedure Step |
   |                |                |                | is matched to  |
   |                |                |                | this group for |
   |                |                |                | pro            |
   |                |                |                | tocol-assisted |
   |                |                |                | equipment      |
   |                |                |                | set-up.        |
   |                |                |                |                |
   |                |                |                | Selected value |
   |                |                |                | from this      |
   |                |                |                | group is used  |
   |                |                |                | in Modality    |
   |                |                |                | Performed      |
   |                |                |                | Procedure Step |
   |                |                |                | Performed      |
   |                |                |                | Protocol Code  |
   |                |                |                | Sequence       |
   |                |                |                | (0040,0260)    |
   +----------------+----------------+----------------+----------------+
   | e.g., Patient  | e.g.,          | e.g., No       | e.g., Mapped   |
   | Orientation    |                |                | from user      |
   |                |                |                | console        |
   |                |                |                | selection of   |
   |                |                |                | Patient        |
   |                |                |                | Orientation.   |
   |                |                |                | Used in        |
   |                |                |                | Patient        |
   |                |                |                | Orientation    |
   |                |                |                | Code Sequence  |
   |                |                |                | (0054,0410)    |
   +----------------+----------------+----------------+----------------+
   | ...            | ...            | ...            | ...            |
   +----------------+----------------+----------------+----------------+

The Default Value Set may be an extension of a standard context group
("extended CID xxx"). If used, a table shall be provided specifying the
extended context group, the Context Group Local Version (0008,0107)
value and the Context Group Creator UID (0008,010D).

This section describes the specification of any private context groups
that are used. It shall follow the format for context groups specified
in .

.. _sect_A.9.3.2:

Template Specifications
^^^^^^^^^^^^^^^^^^^^^^^

This section specifies any extensions to standard templates and/or any
private templates that are used, and defines them. Definitions shall
follow the format for templates specified in

.. _sect_A.9.3.3:

Private Code Definitions
^^^^^^^^^^^^^^^^^^^^^^^^

This section specifies any private codes used and their definitions.

.. _sect_A.9.4:

Grayscale Image Consistency
~~~~~~~~~~~~~~~~~~~~~~~~~~~

Any support for the DICOM Grayscale Standard Display Function will be
specified in this section.

.. _sect_A.9.5:

Standard Extended/Specialized/Private SOP Classes
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

This section describes Standard Extended SOP Class, Specialized SOP
Class, or Private SOP Class that are used.

.. _sect_A.9.5.1:

Standard Extended/Specialized/Private SOP <i>
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

This section describes a particular Standard Extended SOP Class,
Specialized SOP Class, or Private SOP Class.

.. _sect_A.9.6:

Private Transfer Syntaxes
~~~~~~~~~~~~~~~~~~~~~~~~~

This section describes any private Transfer Syntaxes that are listed in
the Transfer Syntax Tables.

.. _sect_A.9.6.1:

Private Transfer Syntax <i>
^^^^^^^^^^^^^^^^^^^^^^^^^^^

This section describes particular private transfer syntax. It shall
follow the guidelines specified in .

