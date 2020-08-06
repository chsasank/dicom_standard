.. _chapter_1:

Scope and Field of Application
==============================

PS3.1 provides an overview of the entire Digital Imaging and
Communications in Medicine (DICOM) Standard. It describes the history,
scope, goals, and structure of the Standard. In particular, it contains
a brief description of the contents of each Part of the Standard.

.. _sect_1.1:

Scope of DICOM
--------------

Digital Imaging and Communications in Medicine (DICOM) is the standard
for the communication and management of medical imaging information and
related data.

The DICOM Standard facilitates interoperability of medical imaging
equipment by specifying:

-  For network communications, a set of protocols to be followed by
   devices claiming conformance to the Standard.

-  The syntax and semantics of Commands and associated information that
   can be exchanged using these protocols.

-  For media communication, a set of media storage services to be
   followed by devices claiming conformance to the Standard, as well as
   a File Format and a medical directory structure to facilitate access
   to the images and related information stored on interchange media.

-  Information that must be supplied with an implementation for which
   conformance to the Standard is claimed.

The DICOM Standard does not specify:

-  The implementation details of any features of the Standard on a
   device claiming conformance.

-  The overall set of features and functions to be expected from a
   system implemented by integrating a group of devices each claiming
   DICOM conformance.

-  A testing/validation procedure to assess an implementation's
   conformance to the Standard.

.. _sect_1.2:

Field of Application
--------------------

The DICOM Standard pertains to the field of Medical Informatics. Within
that field, it addresses the exchange of digital information between
medical imaging equipment and other systems. Because such equipment may
interoperate with other medical devices and information systems, the
scope of this Standard needs to overlap with other areas of medical
informatics. However, the DICOM Standard does not address the breadth of
this field.

This Standard has been developed with an emphasis on diagnostic medical
imaging as practiced in radiology, cardiology, pathology, dentistry,
ophthalmology and related disciplines, and image-based therapies such as
interventional radiology, radiotherapy and surgery. However, it is also
applicable to a wide range of image and non-image related information
exchanged in clinical, research, veterinary, and other medical
environments.

This Standard facilitates interoperability of systems claiming
conformance in a multi-vendor environment, but does not, by itself,
guarantee interoperability.

.. _sect_1.3:

History
-------

With the introduction of computed tomography (CT) followed by other
digital diagnostic imaging modalities in the 1970's, and the increasing
use of computers in clinical applications, the American College of
Radiology (ACR) and the National Electrical Manufacturers Association
(NEMA) recognized the emerging need for a standard method for
transferring images and associated information between devices
manufactured by various vendors. These devices produce a variety of
digital image formats.

The American College of Radiology (ACR) and the National Electrical
Manufacturers Association (NEMA) formed a joint committee in 1983 to
develop a standard to:

-  Promote communication of digital image information, regardless of
   device manufacturer

-  Facilitate the development and expansion of picture archiving and
   communication systems (PACS) that can also interface with other
   systems of hospital information

-  Allow the creation of diagnostic information data bases that can be
   interrogated by a wide variety of devices distributed geographically.

ACR-NEMA Standards Publication No. 300-1985, published in 1985 was
designated version 1.0. The Standard was followed by two revisions: No.
1, dated October 1986 and No. 2, dated January 1988. These Standards
Publications specified a hardware interface, a minimum set of software
commands, and a consistent set of data formats.

ACR-NEMA Standards Publication No. 300-1988, published in 1988 was
designated version 2.0. It included version 1.0, the published
revisions, and additional revisions. It also included new material to
provide command support for display devices, to introduce a new
hierarchy scheme to identify an image, and to add data elements for
increased specificity when describing an image.

In 1993, ACR-NEMA Standard 300 was substantially revised and replaced by
this Standard, designated Digital Imaging and Communications in Medicine
(DICOM). It embodies a number of major enhancements to previous versions
of the ACR-NEMA Standard:

-  It is applicable to a networked environment. The ACR-NEMA Standard
   was applicable in a point-to-point environment only; for operation in
   a networked environment a Network Interface Unit (NIU) was required.
   DICOM supports operation in a networked environment using the
   industry standard networking protocol TCP/IP.

-  It is applicable to off-line media exchange. The ACR-NEMA Standard
   did not specify a file format or choice of physical media or logical
   filesystem. DICOM supports operation in an off-line media environment
   using industry standard media such as CD-R, DVD-R and USB and common
   file systems.

-  It is a service oriented protocol, specifying the semantics of
   commands and associated data, and how devices claiming conformance to
   the Standard react to commands and data being exchanged. Specified
   services include support for management of the workflow of an imaging
   department. The ACR-NEMA Standard was confined to the transfer of
   data with only implicit service requirements.

-  It specifies levels of conformance. The ACR-NEMA Standard specified a
   minimum level of conformance. DICOM explicitly describes how an
   implementor must structure a Conformance Statement to select specific
   options.

In 1995, with the addition of DICOM capabilities for cardiology imaging
supported by the American College of Cardiology, the ACR-NEMA Joint
Committee was reorganized as the DICOM Standards Committee, a broad
collaboration of stakeholders across all medical imaging specialties.

.. _sect_1.4:

Principles
----------

.. _sect_1.4.1:

Global Applicability and Localization
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

DICOM is a world-wide standard that can be used in every locale. It
provides mechanisms to handle data that support cultural requirements,
such as different writing systems, character sets, languages, and
structures for addresses and person names. It supports the variety of
workflows, processes and policies used for biomedical imaging in
different geographic regions, medical specialties and local practices.

Localization to meet the requirements of national or local health and
workflow policies can be done without deviating from the Standard. Such
localization may include specifying code sets (e.g., procedure codes),
or profiling data element usage (both specifying locally allowed values,
and making elements that are optional in the Standard mandatory for
local use).

Localization and profiling can be specified in a number of mechanisms
outside the purview of the DICOM Standard. One such mechanism is
Integration Profiles from the Integrating the Healthcare Enterprise
(IHE) organization. It is important that Profiling adhere to the concept
of non-contradiction. A Profile can add requirements but should not
contradict DICOM requirements, as that would make it impossible to
comply with both DICOM and the Profile.

.. _sect_1.4.2:

Continuous Maintenance
~~~~~~~~~~~~~~~~~~~~~~

The DICOM Standard is an evolving standard and it is maintained in
accordance with the Procedures of the DICOM Standards Committee.
Proposals for enhancements are welcome from all users of the Standard,
and may be submitted to the Secretariat. Supplements and corrections to
the Standard are balloted and approved several times a year. When
approved as Final Text, each change becomes official, is published
separately, and goes into effect immediately. At intervals, all of the
approved Final Text changes are consolidated and published in an updated
edition of the Standard. Once changes are consolidated into an updated
edition of the Standard, the individual change documents are not
maintained; readers are directed to use the consolidated edition of the
Standard.

A requirement in updating the Standard is to maintain effective
compatibility with previous editions.

The maintenance process may involve retirement of sections of the
Standard.

Retirement does not imply that these features cannot be used. However,
the DICOM Standards Committee will not maintain the documentation of
retired features. The reader is referred to earlier editions of the
Standard.

The use of the retired features is discouraged for new implementations,
in favor of those alternatives remaining in the Standard.

.. _sect_1.4.3:

Information Objects and Unique Object Identification
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

Many DICOM services involve the exchange of persistent information
objects, such as images. An instance of such an information object may
be exchanged across many systems and many organizational contexts, and
over time. While minor changes may be made to the attributes of an
instance to facilitate its handling within a particular organization
(e.g., by coercing a Patient ID to the value used in a local context),
the semantic content of an instance does not change.

Each instance is identified by a globally unique object identifier,
which persists with the instance across all exchanges. Changes to the
semantic content of an instance are defined to create a new instance,
which is assigned a new globally unique object identifier.

.. _sect_1.4.4:

Conformance
~~~~~~~~~~~

Conformance to the DICOM Standard is stated in terms of Service-Object
Pair (SOP) Classes, which represent Services (such as Storage using
network, media, or web) operating on types of Information Objects (such
as CT or MR images).

SOP Class specifications in the DICOM Standard are only changed in a
manner that is intended to be forward and backward compatible for all
editions of the Standard. Conformance requirements and conformance
claims are therefore referenced to the identifier of the SOP Class, and
never referenced to an edition of the Standard.

Each implementation is required to provide a Conformance Statement, in
accordance with a consistent *pro forma* structure, facilitating
comparison of products for interoperability.

.. _sect_1.4.5:

Consistency of Information Model
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

A large number of information objects defined in the DICOM Standard
follow a common composite information model with information entities
representing Patient, Study, Series, Equipment, Frame of Reference, and
the specific instance data type. This information model is a
simplification of the real world concepts and activities of medical
imaging; for acquisition modalities, a Study is approximately equivalent
to an ordered procedure, and a Series is approximately equivalent to a
performed data acquisition protocol element. In other domains, such as
Radiotherapy, the Study and Series are less clearly related to real
world entities or activities, but are still required for consistency.
This simplified model is sufficient for the pragmatic needs of managing
imaging and related data collected in routine practice.

New information objects defined in DICOM will typically conform to this
existing common information model, allowing reuse of implementations
with minimal changes to support the new objects.

