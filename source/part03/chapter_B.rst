.. _chapter_B:

Normalized Information Object Definitions (Normative)
=====================================================

.. _sect_B.1:

Patient Information Object Definition
-------------------------------------

Retired. See
`PS3.3-2004 <ftp://medical.nema.org/MEDICAL/Dicom/2004/printed/04_03pu3.pdf>`__.

.. _sect_B.2:

Visit Information Object Definition
-----------------------------------

Retired. See
`PS3.3-2004 <ftp://medical.nema.org/MEDICAL/Dicom/2004/printed/04_03pu3.pdf>`__.

.. _sect_B.3:

Study Information Object Definition
-----------------------------------

Retired. See
`PS3.3-2004 <ftp://medical.nema.org/MEDICAL/Dicom/2004/printed/04_03pu3.pdf>`__.

.. _sect_B.4:

Study Component Information Object Definition
---------------------------------------------

Retired. See
`PS3.3-2004 <ftp://medical.nema.org/MEDICAL/Dicom/2004/printed/04_03pu3.pdf>`__.

.. _sect_B.5:

Results Information Object Definition
-------------------------------------

Retired. See
`PS3.3-2004 <ftp://medical.nema.org/MEDICAL/Dicom/2004/printed/04_03pu3.pdf>`__.

.. _sect_B.6:

Interpretation Information Object Definition
--------------------------------------------

Retired. See
`PS3.3-2004 <ftp://medical.nema.org/MEDICAL/Dicom/2004/printed/04_03pu3.pdf>`__.

.. _sect_B.7:

Basic Film Session Information Object Definition
------------------------------------------------

.. _sect_B.7.1:

IOD Description
~~~~~~~~~~~~~~~

The Basic Film Session Information Object Definition describes the
presentation parameters that are common for all the films of a film
session (e.g., number of films, film destination).

.. _sect_B.7.2:

IOD Modules
~~~~~~~~~~~

.. table:: Film Session IOD Modules

   +----------------------+----------------------+----------------------+
   | Module               | Reference            | Module Description   |
   +======================+======================+======================+
   | SOP Common           | `SOP Common          | Contains SOP Common  |
   |                      | Modu                 | information          |
   |                      | le <#sect_C.12.1>`__ |                      |
   +----------------------+----------------------+----------------------+
   | Basic Film Session   | `Basic Film Session  | Contains Film        |
   | Presentation         | Presentation         | Session              |
   |                      | Modu                 | presentations        |
   |                      | le <#sect_C.13.1>`__ | information          |
   +----------------------+----------------------+----------------------+
   | Basic Film Session   | `Basic Film Session  | References to        |
   | Relationship         | Relationship         | related SOP Classes  |
   |                      | Modu                 |                      |
   |                      | le <#sect_C.13.2>`__ |                      |
   +----------------------+----------------------+----------------------+

.. _sect_B.8:

Basic Film Box Information Object Definition
--------------------------------------------

.. _sect_B.8.1:

IOD Description
~~~~~~~~~~~~~~~

The Basic Film Box Information Object Definition is an abstraction of
the presentation of one film of the film session. The Basic Film Box IOD
describes the presentation parameters that are common for all images on
a given sheet of film.

.. _sect_B.8.2:

IOD Modules
~~~~~~~~~~~

.. table:: Basic Film Box IOD Modules

   +----------------------+----------------------+----------------------+
   | Module               | Reference            | Module Description   |
   +======================+======================+======================+
   | SOP Common           | `SOP Common          | Contains SOP Common  |
   |                      | Modu                 | information          |
   |                      | le <#sect_C.12.1>`__ |                      |
   +----------------------+----------------------+----------------------+
   | Basic Film Box       | `Basic Film Box      | Contains Film Box    |
   | Presentation         | Presentation         | presentation         |
   |                      | Modu                 | information          |
   |                      | le <#sect_C.13.3>`__ |                      |
   +----------------------+----------------------+----------------------+
   | Basic Film Box       | `Basic Film Box      | References to        |
   | Relationship         | Relationship         | related SOP Classes  |
   |                      | Modu                 |                      |
   |                      | le <#sect_C.13.4>`__ |                      |
   +----------------------+----------------------+----------------------+

.. _sect_B.9:

Basic Image Box Information Object Definition
---------------------------------------------

.. _sect_B.9.1:

IOD Description
~~~~~~~~~~~~~~~

The Basic Image Box Information Object Definition is an abstraction of
the presentation of an image and image related data in the image area of
a film. The Basic Image Box IOD describes the presentation parameters
and image pixel data that apply to a single image of a sheet of film.

.. _sect_B.9.2:

IOD Modules
~~~~~~~~~~~

.. table:: Basic Image Box IOD Modules

   +----------------------+----------------------+----------------------+
   | Module               | Reference            | Module Description   |
   +======================+======================+======================+
   | SOP Common           | `SOP Common          | Contains SOP Common  |
   |                      | Modu                 | information          |
   |                      | le <#sect_C.12.1>`__ |                      |
   +----------------------+----------------------+----------------------+
   | Image Box            | `Image Box Pixel     | Contains Image Box   |
   | Presentation         | Presentation         | presentation         |
   |                      | Modu                 | information          |
   |                      | le <#sect_C.13.5>`__ |                      |
   +----------------------+----------------------+----------------------+

The `Image Box Relationship Module (Retired) <#sect_C.13.6>`__ was
previously defined in DICOM. It is now retired. See PS3.3-1998.

.. _sect_B.10:

Basic Annotation Box Information Object Definition
--------------------------------------------------

.. _sect_B.10.1:

IOD Description
~~~~~~~~~~~~~~~

The Basic Annotation Box Information Object Definition is an abstraction
of the presentation of an annotation (e.g., text string) on a film. The
Basic Annotation Box IOD describes the most used text related
presentation parameters.

.. _sect_B.10.2:

IOD Modules
~~~~~~~~~~~

.. table:: Basic Annotation Box IOD Modules

   +----------------------+----------------------+----------------------+
   | Module               | Reference            | Module Description   |
   +======================+======================+======================+
   | SOP Common           | `SOP Common          | Contains SOP Common  |
   |                      | Modu                 | information          |
   |                      | le <#sect_C.12.1>`__ |                      |
   +----------------------+----------------------+----------------------+
   | Basic Annotation     | `Basic Annotation    | Contains annotation  |
   | Presentation         | Presentation         | presentation         |
   |                      | Modu                 | information          |
   |                      | le <#sect_C.13.7>`__ |                      |
   +----------------------+----------------------+----------------------+

.. _sect_B.11:

Print Job Information Object Definition
---------------------------------------

.. _sect_B.11.1:

IOD Description
~~~~~~~~~~~~~~~

The Print Job Information Object Definition is an abstraction of the
print job transaction and is the basic information entity to monitor the
execution of the print process. A print job contains one film or
multiple films, all belonging to the same film session.

.. _sect_B.11.2:

IOD Modules
~~~~~~~~~~~

.. table:: Print Job IOD Modules

   +------------+---------------------------+---------------------------+
   | Module     | Reference                 | Module Description        |
   +============+===========================+===========================+
   | SOP Common | `SOP Common               | Contains SOP Common       |
   |            | Module <#sect_C.12.1>`__  | information               |
   +------------+---------------------------+---------------------------+
   | Print Job  | `Print Job                | Contains print job        |
   |            | Module <#sect_C.13.8>`__  | transaction information   |
   +------------+---------------------------+---------------------------+

.. _sect_B.12:

Printer Information Object Definition
-------------------------------------

.. _sect_B.12.1:

IOD Description
~~~~~~~~~~~~~~~

The Printer Information Object Definition is an abstraction of the
hardcopy printer and is the basic information entity to monitor the
status of the printer.

.. _sect_B.12.2:

IOD Modules
~~~~~~~~~~~

.. table:: Printer IOD Modules

   +------------+---------------------------+---------------------------+
   | Module     | Reference                 | Module Description        |
   +============+===========================+===========================+
   | SOP Common | `SOP Common               | Contains SOP Common       |
   |            | Module <#sect_C.12.1>`__  | information               |
   +------------+---------------------------+---------------------------+
   | Printer    | `Printer                  | Contains status           |
   |            | Module <#sect_C.13.9>`__  | information to monitor    |
   |            |                           | the printer               |
   +------------+---------------------------+---------------------------+

.. _sect_B.13:

VOI LUT Box Information Object Definition (Retired)
---------------------------------------------------

This section was previously defined in DICOM. It is now retired. See
PS3.3-1998.

.. _sect_B.14:

Image Overlay Box Information Object Definition (Retired)
---------------------------------------------------------

This section was previously defined in DICOM. It is now retired. See
PS3.3-1998.

.. _sect_B.15:

Storage Commitment Information Object Definition
------------------------------------------------

.. _sect_B.15.1:

Storage Commitment IOD Description
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

The Storage Commitment IOD describes the Attributes that may be present
in a Storage Commitment Request or Response. The SOP Instances
referenced by the Storage Commitment IOD are not restricted to images
and may include other SOP Instances.

.. _sect_B.15.2:

Storage Commitment IOD Modules
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

`table_title <#table_B.15-1>`__ identifies and defines the Modules that
comprise this IOD. The requirements for whether Attributes in these
Modules are mandatory or optional are as specified in .

.. table:: Storage Commitment IOD Modules

   +--------------------+-----------------------+-----------------------+
   | Module             | Reference             | Module Description    |
   +====================+=======================+=======================+
   | SOP Common         | `SOP Common           | Contains SOP common   |
   |                    | Mod                   | information           |
   |                    | ule <#sect_C.12.1>`__ |                       |
   +--------------------+-----------------------+-----------------------+
   | Storage Commitment | `Storage Commitment   | Contains references   |
   |                    | M                     | to the SOP Instances  |
   |                    | odule <#sect_C.14>`__ | and associated        |
   |                    |                       | information that are  |
   |                    |                       | contained in Storage  |
   |                    |                       | Commitment.           |
   +--------------------+-----------------------+-----------------------+

.. _sect_B.16:

Print Queue Information Object Definition
-----------------------------------------

Retired. See
`PS3.3-2004 <ftp://medical.nema.org/MEDICAL/Dicom/2004/printed/04_03pu3.pdf>`__.

.. _sect_B.17:

Modality Performed Procedure Step Information Object Definition
---------------------------------------------------------------

.. _sect_B.17.1:

IOD Description
~~~~~~~~~~~~~~~

A "Modality Performed Procedure Step Information Object Definition" is
an abstraction of the information that describes the activities,
conditions and results of an imaging procedure performed on a modality.
It contains information about the Modality Performed Procedure Step
(MPPS) and its relations to other Information Entities of the DICOM
real-world model as introduced in this Part.

A Modality Performed Procedure Step is related to the actual imaging
procedure carried out at the modality. Other types of Performed
Procedure Steps, e.g., reporting or image processing, are not covered by
the Modality Performed Procedure Step IOD. The information gathered
includes data about the performance of the procedure itself, and data
for billing and material management. The Modality Performed Procedure
Step IOD includes general PPS Modules and image acquisition specific
ones, such as Image Acquisition Results, and Billing and Material
Management.

.. _sect_B.17.2:

IOD Modules
~~~~~~~~~~~

`table_title <#table_B.17.2-1>`__ lists the Modules that make up the
Modality Performed Procedure Step IOD.

.. table:: Modality Performed Procedure Step IOD Modules

   +----------------------+----------------------+----------------------+
   | Module               | Reference            | Module Description   |
   +======================+======================+======================+
   | SOP Common           | `SOP Common          | Contains SOP common  |
   |                      | Modu                 | information          |
   |                      | le <#sect_C.12.1>`__ |                      |
   +----------------------+----------------------+----------------------+
   | Performed Procedure  | `Performed Procedure | References the       |
   | Step Relationship    | Step                 | related SOPs and     |
   |                      | Relationsh           | IEs.                 |
   |                      | ip <#sect_C.4.13>`__ |                      |
   +----------------------+----------------------+----------------------+
   | Performed Procedure  | `Performed Procedure | Includes identifying |
   | Step Information     | Step                 | and status           |
   |                      | Informati            | information as well  |
   |                      | on <#sect_C.4.14>`__ | as place and time    |
   +----------------------+----------------------+----------------------+
   | Image Acquisition    | `Image Acquisition   | Identifies Series    |
   | Results              | Results              | and Images related   |
   |                      | Modu                 | to this PPS and      |
   |                      | le <#sect_C.4.15>`__ | specific image       |
   |                      |                      | acquisition          |
   |                      |                      | conditions.          |
   +----------------------+----------------------+----------------------+
   | Billing and Material | `Billing and         | Contains codes for   |
   | Management Codes     | Material Management  | billing and material |
   |                      | Code                 | management.          |
   |                      | Modu                 |                      |
   |                      | le <#sect_C.4.17>`__ |                      |
   +----------------------+----------------------+----------------------+

.. note::

   The `Radiation Dose Module <#sect_C.4.16>`__ has been retired. See
   PS3.3 2017c.

.. _sect_B.18:

Presentation LUT Information Object Definition
----------------------------------------------

.. _sect_B.18.1:

IOD Description
~~~~~~~~~~~~~~~

The Presentation LUT Information Object is an abstraction of a
Presentation LUT. The objective of the Presentation LUT is to realize
image display tailored for specific modalities, applications, and user
preferences. It is used to prepare image pixel data for display on
devices that conform to the Grayscale Standard Display Function defined
in .

The output of the Presentation LUT is Presentation Values (P-Values).
P-Values are approximately related to human perceptual response. They
are intended to facilitate common input for both hardcopy and softcopy
display devices. P-Values are intended to be independent of the specific
class or characteristics of the display device.

.. _sect_B.18.2:

IOD Modules
~~~~~~~~~~~

.. table:: Presentation LUT IOD Modules

   +-----------------------+-----------------------+--------------------+
   | Module                | Reference             | Module Description |
   +=======================+=======================+====================+
   | SOP Common            | `SOP Common           |                    |
   | Information           | Mod                   |                    |
   |                       | ule <#sect_C.12.1>`__ |                    |
   +-----------------------+-----------------------+--------------------+
   | Presentation LUT      | `Presentation LUT     |                    |
   |                       | Mod                   |                    |
   |                       | ule <#sect_C.11.4>`__ |                    |
   +-----------------------+-----------------------+--------------------+

.. _sect_B.19:

Pull Print Request Information Object Definition
------------------------------------------------

Retired. See
`PS3.3-2004 <ftp://medical.nema.org/MEDICAL/Dicom/2004/printed/04_03pu3.pdf>`__.

.. _sect_B.20:

Printer Configuration Information Object Definition
---------------------------------------------------

.. _sect_B.20.1:

IOD Description
~~~~~~~~~~~~~~~

The Printer Configuration IOD describes key imaging characteristics of
the printer.

.. _sect_B.20.2:

IOD Modules
~~~~~~~~~~~

.. table:: Printer Configuration IOD Modules

   +----------------------+----------------------+----------------------+
   | Module               | Reference            | Module Description   |
   +======================+======================+======================+
   | SOP Common           | `SOP Common          | Contains SOP Common  |
   |                      | Modu                 | Information          |
   |                      | le <#sect_C.12.1>`__ |                      |
   +----------------------+----------------------+----------------------+
   | Printer              | `Printer             | Contains information |
   |                      | Modu                 | about the printer    |
   |                      | le <#sect_C.13.9>`__ |                      |
   +----------------------+----------------------+----------------------+
   | Printer              | `Printer             | Contains Printer     |
   | Configuration        | Configuration        | Configuration        |
   |                      | Modul                | Information          |
   |                      | e <#sect_C.13.13>`__ |                      |
   +----------------------+----------------------+----------------------+

.. _sect_B.21:

Basic Print Image Overlay Box Information Object Definition
-----------------------------------------------------------

Retired. See
`PS3.3-2004 <ftp://medical.nema.org/MEDICAL/Dicom/2004/printed/04_03pu3.pdf>`__.

.. _sect_B.22:

General Purpose Scheduled Procedure Step Information Object Definition (Retired)
--------------------------------------------------------------------------------

Retired. See
`PS3.3-2011 <ftp://medical.nema.org/MEDICAL/Dicom/2011/11_03pu.pdf>`__.

.. _sect_B.23:

General Purpose Performed Procedure Step Information Object Definition (Retired)
--------------------------------------------------------------------------------

Retired. See
`PS3.3-2011 <ftp://medical.nema.org/MEDICAL/Dicom/2011/11_03pu.pdf>`__.

.. _sect_B.24:

Instance Availability Notification Information Object Definition
----------------------------------------------------------------

.. _sect_B.24.1:

IOD Description
~~~~~~~~~~~~~~~

An "Instance Availability Notification Information Object Definition" is
a summary of the information that describes the availability of a set of
Composite Instances.

.. _sect_B.24.2:

IOD Modules
~~~~~~~~~~~

`table_title <#table_B.24.2-1>`__ lists the Modules that make up the
Instance Availability Notification IOD.

.. table:: Instance Availability Notification IOD Modules

   +----------------------+----------------------+----------------------+
   | Module               | Reference            | Module Description   |
   +======================+======================+======================+
   | SOP Common           | `SOP Common          | Contains SOP common  |
   |                      | Modu                 | information          |
   |                      | le <#sect_C.12.1>`__ |                      |
   +----------------------+----------------------+----------------------+
   | Instance             | `Instance            | References the       |
   | Availability         | Availability         | related SOPs and     |
   | Notification         | Notification         | IEs.                 |
   |                      | Modu                 |                      |
   |                      | le <#sect_C.4.23>`__ |                      |
   +----------------------+----------------------+----------------------+

.. _sect_B.25:

Media Creation Management Information Object Definition
-------------------------------------------------------

.. _sect_B.25.1:

IOD Description
~~~~~~~~~~~~~~~

A "Media Creation Management Information Object Definition" is an
abstraction of the information that describes the Attributes and the
status of a media creation request.

.. _sect_B.25.2:

IOD Modules
~~~~~~~~~~~

`table_title <#table_B.25.2-1>`__ lists the Modules that make up the
Media Creation Management IOD.

.. table:: Media Creation Management IOD Modules

   +----------------------+----------------------+----------------------+
   | Module               | Reference            | Module Description   |
   +======================+======================+======================+
   | SOP Common           | `SOP Common          | Contains SOP common  |
   |                      | Modu                 | information          |
   |                      | le <#sect_C.12.1>`__ |                      |
   +----------------------+----------------------+----------------------+
   | Media Creation       | `Media Creation      | Contains references  |
   | Management           | Management           | to the SOP Instances |
   |                      | Modu                 | to be used for this  |
   |                      | le <#sect_C.22.1>`__ | media creation       |
   |                      |                      | request, and the     |
   |                      |                      | information about    |
   |                      |                      | its status.          |
   +----------------------+----------------------+----------------------+

.. _sect_B.26:

Unified Procedure Step Information Object Definition
----------------------------------------------------

.. _sect_B.26.1:

IOD Description
~~~~~~~~~~~~~~~

A Unified Procedure Step (UPS) describes the details of a procedure step
that has been scheduled, the progress details during performance, and
the details of the procedure step actually performed in response.

.. _sect_B.26.2:

IOD Modules
~~~~~~~~~~~

`table_title <#table_B.26.2-1>`__ lists the Modules that make up the
Unified Procedure Step IOD.

.. table:: Unified Procedure Step IOD Modules

   +----------------------+----------------------+----------------------+
   | Module               | Reference            | Module Description   |
   +======================+======================+======================+
   | SOP Common           | `SOP Common          | Contains SOP common  |
   |                      | Modu                 | information          |
   |                      | le <#sect_C.12.1>`__ |                      |
   +----------------------+----------------------+----------------------+
   | Unified Procedure    | `Unified Procedure   | References the       |
   | Step Relationship    | Step Relationship    | related SOPs and IEs |
   |                      | Modu                 |                      |
   |                      | le <#sect_C.30.4>`__ |                      |
   +----------------------+----------------------+----------------------+
   | Unified Procedure    | `Unified Procedure   | Describes the UPS    |
   | Step Scheduled       | Step Scheduled       | task to be performed |
   | Procedure            | Procedure            | including            |
   | Information          | Information          | information about    |
   |                      | Modu                 | place, time,         |
   |                      | le <#sect_C.30.2>`__ | priority and input   |
   |                      |                      | data                 |
   +----------------------+----------------------+----------------------+
   | Unified Procedure    | `Unified Procedure   | Describes the        |
   | Step Progress        | Step Progress        | progress of a UPS    |
   | Information          | Information          | task                 |
   |                      | Modu                 |                      |
   |                      | le <#sect_C.30.1>`__ |                      |
   +----------------------+----------------------+----------------------+
   | Unified Procedure    | `Unified Procedure   | Describes the work   |
   | Step Performed       | Step Performed       | performed including  |
   | Procedure            | Procedure            | information about    |
   | Information          | Information          | status, place, time  |
   |                      | Modu                 | and result data      |
   |                      | le <#sect_C.30.3>`__ |                      |
   +----------------------+----------------------+----------------------+
   | Patient Demographic  | `Patient Demographic | Describes the        |
   |                      | Mod                  | Patient at the time  |
   |                      | ule <#sect_C.2.3>`__ | of scheduling        |
   +----------------------+----------------------+----------------------+
   | Patient Medical      | `Patient Medical     | Describes the        |
   |                      | Mod                  | Patient's medical    |
   |                      | ule <#sect_C.2.4>`__ | state or history     |
   +----------------------+----------------------+----------------------+
   | Visit Identification | `Visit               | Attributes relevant  |
   |                      | Identification       | to identifying a     |
   |                      | Mod                  | Visit                |
   |                      | ule <#sect_C.3.2>`__ |                      |
   +----------------------+----------------------+----------------------+
   | Visit Status         | `Visit Status        | Attributes relevant  |
   |                      | Mod                  | to the Patient's     |
   |                      | ule <#sect_C.3.3>`__ | stay with the        |
   |                      |                      | healthcare provider  |
   +----------------------+----------------------+----------------------+
   | Visit Admission      | `Visit Admission     | Attributes relevant  |
   |                      | Mod                  | to admitting a       |
   |                      | ule <#sect_C.3.4>`__ | Patient during a     |
   |                      |                      | Visit                |
   +----------------------+----------------------+----------------------+

.. _sect_B.27:

RT Conventional Machine Verification Information Object Definition
------------------------------------------------------------------

.. _sect_B.27.1:

IOD Description
~~~~~~~~~~~~~~~

The RT Conventional Machine Verification IOD describes the Attributes
that are required by an external Machine Parameter Verifier (MPV) when
performing verification of a conventional (photon or electron) radiation
therapy treatment, prior to delivery.

.. _sect_B.27.2:

IOD Modules
~~~~~~~~~~~

.. table:: RT Conventional Machine Verification IOD Modules

   +----------------------+----------------------+----------------------+
   | Module               | Reference            | Module Description   |
   +======================+======================+======================+
   | SOP Common           | `SOP Common          | Contains SOP Common  |
   |                      | Modu                 | Information          |
   |                      | le <#sect_C.12.1>`__ |                      |
   +----------------------+----------------------+----------------------+
   | RT General Machine   | `RT General Machine  | Contains general     |
   | Verification         | Verification         | delivery             |
   |                      | Modu                 | verification         |
   |                      | le <#sect_C.31.1>`__ | information          |
   +----------------------+----------------------+----------------------+
   | RT Conventional      | `RT Conventional     | Contains delivery    |
   | Machine Verification | Machine Verification | verification         |
   |                      | Modu                 | information specific |
   |                      | le <#sect_C.31.2>`__ | to conventional      |
   |                      |                      | (photon or electron) |
   |                      |                      | machines             |
   +----------------------+----------------------+----------------------+

.. _sect_B.28:

RT Ion Machine Verification Information Object Definition
---------------------------------------------------------

.. _sect_B.28.1:

IOD Description
~~~~~~~~~~~~~~~

The RT Ion Machine Verification IOD describes the Attributes that are
required by an external Machine Parameter Verifier (MPV) when performing
verification of an ion radiation therapy treatment, prior to delivery.

.. _sect_B.28.2:

IOD Modules
~~~~~~~~~~~

.. table:: RT Ion Machine Verification IOD Modules

   +----------------------+----------------------+----------------------+
   | Module               | Reference            | Module Description   |
   +======================+======================+======================+
   | SOP Common           | `SOP Common          | Contains SOP Common  |
   |                      | Modu                 | Information          |
   |                      | le <#sect_C.12.1>`__ |                      |
   +----------------------+----------------------+----------------------+
   | RT General Machine   | `RT General Machine  | Contains general     |
   | Verification         | Verification         | delivery             |
   |                      | Modu                 | verification         |
   |                      | le <#sect_C.31.1>`__ | information          |
   +----------------------+----------------------+----------------------+
   | RT Ion Machine       | `RT Ion Machine      | Contains delivery    |
   | Verification         | Verification         | verification         |
   |                      | Modu                 | information specific |
   |                      | le <#sect_C.31.3>`__ | to ion machines      |
   +----------------------+----------------------+----------------------+

.. _sect_B.29:

Display System Information Object Definition
--------------------------------------------

.. _sect_B.29.1:

IOD Description
~~~~~~~~~~~~~~~

An Instance of the Display System IOD describes all of the Display
Subsystems in a given Display System.

Display Subsystems are described in terms of their equipment
identification, display performance (luminance, uniformity, etc.) and
the corresponding configurations. Although a variety of components
(controllers, cables, display devices, etc.) contribute to the
performance of the Display Subsystem to which they belong, these details
are not exposed in the abstraction of the Display Subsystem. Similarly,
each Display Subsystem is addressed independently even though one
controller might drive display devices in multiple Display Subsystems or
multiple controllers might drive a single display device. Effectively,
the Display Subsystem represents the display device and any components
involved behind it.

The IOD only describes emissive display systems.

.. note::

   Hanging Protocols manage Screens based on their physical location and
   arrangement. This IOD does not describe the spatial positioning of
   Display Devices. There is usually a 1:1 relationship between a
   Display Subsystem in this IOD and a Hanging Protocol Screen.

.. table:: Display System IOD Modules

   +----------------------+----------------------+----------------------+
   | Module               | Reference            | Module Description   |
   +======================+======================+======================+
   | SOP Common           | `SOP Common          | Contains SOP Common  |
   |                      | Modu                 | information.         |
   |                      | le <#sect_C.12.1>`__ |                      |
   +----------------------+----------------------+----------------------+
   | Display System       | `Display System      | Describes the        |
   |                      | Modu                 | Display System. The  |
   |                      | le <#sect_C.32.1>`__ | Display System has   |
   |                      |                      | one or more Display  |
   |                      |                      | Subsystem. A Display |
   |                      |                      | Subsystem            |
   |                      |                      | corresponds to one   |
   |                      |                      | Display Device.      |
   +----------------------+----------------------+----------------------+
   | Target Luminance     | `Target Luminance    | Describes the target |
   | Characteristics      | Characteristics      | luminance            |
   |                      | Modu                 | characteristics of   |
   |                      | le <#sect_C.32.2>`__ | the Display          |
   |                      |                      | Subsystem(s)         |
   +----------------------+----------------------+----------------------+
   | QA Results           | `QA Results          | Describes the        |
   |                      | Modu                 | results of QA        |
   |                      | le <#sect_C.32.3>`__ | performed on the     |
   |                      |                      | Display              |
   |                      |                      | Subsystem(s).        |
   +----------------------+----------------------+----------------------+

