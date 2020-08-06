.. _chapter_6:

DICOM Models for Media Storage
==============================

This section defines the DICOM Media Storage Model used by DICOM
Application Entities for the purpose of communication through the
interchange of removable storage media. Specifically, this Section
provides a model to clarify a number of concepts for digital imaging and
communications and introduces key terms used throughout the DICOM
Standard. This model has been used to partition the DICOM Standard into
separate parts related to storage media interchange.

.. _sect_6.1:

General DICOM Communication Model
---------------------------------

presents the general communication model of the DICOM Standard, which
spans both network (on-line) and media interchange (off-line)
communication. Application Entities may utilize any of the following
transport mechanisms:

a. the DICOM Message Service and Upper Layer Service, which provides
   independence from specific physical networking communication support
   and protocols such as TCP/IP,

b. the DICOM Web Service API and HTTP Service, which allows use of
   common hypertext and associated protocols for transport of DICOM
   services, or

c. the Basic DICOM File Service, which provides access to Storage Media
   independently from specific physical media storage formats and file
   structures.

PS3.10 describes the Basic DICOM File Service, as depicted in
`figure_title <#figure_6.1-1>`__.

.. _sect_6.2:

The DICOM Media Storage Model
-----------------------------

The DICOM Media Storage Model is presented by
`figure_title <#figure_6.2-1>`__ and expands on the General DICOM
Communication Model introduced earlier in `General DICOM Communication
Model <#sect_6.1>`__.

The DICOM Media Storage Model focuses on the aspects directly related to
data interchange through removable storage media. It pertains to the
data structures and associated rules used at different layers to achieve
interoperability through media interchange. The Services identified in
this Model are simple boundaries between functional layers.

.. note::

   It is not within the scope of this Standard to specify Application
   Programming Interfaces at these boundaries.

The DICOM Media Storage Model includes three layers, which are described
in the following sections.

.. _sect_6.2.1:

Physical Media Layer
~~~~~~~~~~~~~~~~~~~~

Physical media characteristics are defined at the Physical Media Layer.
Such characteristics include the physical media form factor, dimension,
mechanical characteristics and recording properties. This Layer also
defines the organization and grouping of the recorded bits.

.. note::

   1. An example of a Physical Media Layer in the personal computer
      environment is the 3 1/2 inch floppy disk, double sided, high
      density.

   2. The specification of one or more specific Physical Media for a
      given application is beyond the scope of this Part of the DICOM
      Standard. and its annexes specify several Physical Media choices.
      defines a number of Application Profiles that select specific
      Physical Media depending on the requirements of specific medical
      imaging applications.

.. _sect_6.2.2:

Media Format Layer
~~~~~~~~~~~~~~~~~~

At the Media Format Layer, Physical Media bit streams are organized into
specific structures. Data file structures and associated directory
structures are defined to allow efficient access and management of the
physical media space.

.. note::

   This layer is often specific to a given operating system environment.
   An example of such a Media Format Layer definition associated with
   the 3 1/2 inch floppy disk are the data structures used by the
   operating systems of various personal computer file systems. and its
   annexes specify several Media Format choices.

Media Formats supported by the DICOM Standard are selected to support
the minimum requirements specified by the DICOM File Service as
specified in Section 8 of this Part. Constraining access to the File
content through such a DICOM File Service ensures that the DICOM Data
Format Layer is independent from Media Format and Physical Media
selection.

.. _sect_6.2.3:

DICOM Data Format Layer
~~~~~~~~~~~~~~~~~~~~~~~

The DICOM Data Format Layer includes the following elements of
specification:

a. DICOM Media Storage SOP Classes and associated Information Object
   Definitions;

b. The DICOM File Format;

c. The Secure DICOM File Format;

d. The DICOM Media Storage Directory SOP Class;

e. DICOM Media Storage Application Profiles;

f. DICOM Security Profiles for Media Storage.

.. _sect_6.2.3.1:

DICOM SOP Classes
^^^^^^^^^^^^^^^^^

DICOM SOP Classes and associated Information Object Definitions (IODs)
are used to convey specific medical imaging information at the Data
Format Layer. Examples of such IODs are modality images, patient
information, results, etc.

The use of DICOM IODs in conjunction with Media Storage Services forms a
number of Media Storage Service Object Pair Classes or SOP Classes.
Media Storage Services (e.g., read, write, delete, etc.) shall be
performed through the DICOM File Service. The content of the resulting
DICOM Files shall be formatted according to the DICOM File Format as
specified below.

defines a number of SOP Classes that may be used for Media Storage in .
These SOP Classes are based on DICOM Standard IODs that may be found in
.

The structure and encoding of a Data Set representing the data
associated with a SOP Class shall follow . The specification of Transfer
Syntaxes that may be used to encode such a Data Set, is also defined in
.

.. _sect_6.2.3.2:

Concept of the DICOM File Format
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

The encapsulation of a DICOM Data Set in a File shall follow the
specifications of Section 7 of this Part. These encapsulation rules
define a DICOM File Format able to contain in a File any DICOM Data Set.
Files are identified by File IDs. No semantics shall be inferred from
these File IDs, nor from their structure.

.. note::

   A medical imaging application acting as a creator of a DICOM File may
   use semantic information to generate a File ID, but readers of DICOM
   files should not rely on apparent semantic content of a File ID.

Data Set encapsulation shall be based on the DICOM File Service as
specified in Section 8 of this Part.

.. note::

   It is acceptable that a specific Media Format offers more file
   services than those specified in the DICOM File Service. Such
   services may be local or internal to an implementation. Their usage
   is beyond the scope of the DICOM Standard. However, in cases where
   such services are reflected in the file structures of the Media
   format Layer or in the Data Set encoding of an Information Object,
   the extension of such services in a manner that jeopardizes
   interoperability should not be done (e.g., File IDs longer than those
   specified in the DICOM File Service).

The encapsulation of a DICOM File in a Secure DICOM File shall follow
the specifications of `Secure DICOM File Format <#sect_7.4>`__ of this
Part. These encapsulation rules define a mechanism for creating a Secure
DICOM File by encapsulating an unprotected DICOM File as payload within
a secure envelope.

.. _sect_6.2.3.3:

DICOM Medical Information Directory
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

In addition to the DICOM Image and Image related SOP Classes (e.g.,
results, patients) other SOP Classes tailored for media storage may be
used to provide references (or directories) based on medical
information, thus facilitating access to the clinical imaging
information. Such a SOP Class is the Media Storage Directory SOP Class
as defined in . Instances of this SOP Class are conveyed in the File
with a File ID of DICOMDIR.

.. _sect_6.2.4:

DICOM Media Storage Application Profiles
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

A Media Storage Application Profile defines a selection of choices at
the various layers of the DICOM Media Storage Model that are applicable
to a specific need or context in which the media interchange is intended
to be performed. Such choices are formally specified as a Media Storage
Application Profile in order to ensure interoperability between
implementations conforming to the same Media Storage Application
Profile. It facilitates conformance statements that allow users to
assess interoperability of different implementations.

Media Storage Application Profiles shall include:

a. The description of the need addressed by the Application Profile
   (e.g., cardiac, echography, angiography) and its context of
   application;

b. The selection, at the Data Format Layer, of a number of specific IODs
   and associated SOP Classes. For standard DICOM SOP Classes, this
   shall be done by reference to . These SOP Classes, like any other
   DICOM SOP Classes are assigned a unique registered UID. For each SOP
   Class it shall be stated if its support is required or optional
   within the context of this profile;

c. The selection of a specific Media Format definition. This is done by
   reference to that specify the selected Physical Medium, a specific
   associated Media Format and the mapping of this Media Format (or file
   system) services onto the DICOM File Service;

d. The selection of appropriate Transfer Syntaxes;

e. The selection of a specific Security Profile. This is done by
   reference to that specifies the cryptographic algorithms to be used
   to encapsulate the DICOM Files of the DICOM File Set into Secure
   DICOM Files. If a Media Storage Application Profile selects no
   Security Profile, then the Application Profile is unsecure and the
   Secure DICOM File Format shall not be used with that Application
   Profile;

f. Other choices facilitating interoperability such as specific limits
   (e.g., maximum file sizes, if necessary, support of options, if any).

The complete definition and structure of a Media Storage Application
Profiles is specified by . A number of Standard Application Profiles
corresponding to different needs are included in .

.. _sect_6.2.5:

Media Storage and The DICOM Standard Structure
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

`figure_title <#figure_6.2-2>`__ provides an overview of the
relationship between the functional areas identified by the DICOM Media
Storage Model introduced in `The DICOM Media Storage
Model <#sect_6.2>`__ and the various Parts of the DICOM Standard related
to Media Storage. A number of Parts of the DICOM Standard are common
between Network Communication and Media Interchange.

