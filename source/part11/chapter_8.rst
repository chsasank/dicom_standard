.. _chapter_8:

Structure of Application Profile
================================

Application Profiles specific to various clinical areas are defined in
the Annexes to this Part. Each Annex defines an Application Profile
Class related to a single area of medical practice, e.g., cardiology, or
to a single functional context, e.g., image transfer to a printer
system. Several specific Application Profiles may be defined in each
Application Profile class, and an identification scheme is established
to label each specific Application Profile.

An example of an Application Profile structure is provided in below. The
section identifier "X" should be replaced by the identifier of the
annex.

.. _sect_X.1:

Class and Profile Identification
--------------------------------

`Class and Profile Identification <#sect_X.1>`__ of the Application
Profile defines the class and specific Application Profiles in that
class.

This section assigns an identifier to each Application Profile of the
form ttt-x...x-y...y, where "ttt" indicates the type of Application
Profile, "x...x" is an abbreviation of a significant term for the
clinical context and "y...y" is a significant term for a distinguishing
feature of the specific Application Profile. The "ttt" type term shall
be one of STD, AUG, or PRI, indicating whether the Application Profile
is a Standard, Augmented, or Private Application Profile respectively
(see ). Identifiers shall be written such that they may be encoded with
LO (Long String) Value Representation (see ).

.. note::

   Conformance Statements may use the earlier prefix of APL, which is
   equivalent to STD. This use is deprecated and may be retired in
   future editions of the Standard.

.. _sect_X.2:

Clinical Context
----------------

`Clinical Context <#sect_X.2>`__ of the Application Profile shall
describe the clinical need for the interchange of medical images and
related information on storage media, and its context of application.
This section shall not require any specific functionality of the
Application Entities exchanging information using media interchange
beyond their capabilities in the roles of File-set Creator, File-set
Reader, and File-set Updater.

.. note::

   This Section does not, for example, place any graphical presentation
   or performance requirements on workstations that read DICOM
   interchange media. Such requirements are beyond the scope of a DICOM
   Media Storage Application Profile. The requirements that fall within
   the scope of an Application Profile are the specific functional
   storage media interchange capabilities associated with the defined
   roles.

.. _sect_X.2.1:

Roles and Service Class Options
-------------------------------

`Roles and Service Class Options <#sect_X.2.1>`__ describes the Service
Class Options used and the contextual application of the roles of
File-set Creator, File-set Reader, and File-set Updater.

.. _sect_X.3:

General Class Profile
---------------------

`General Class Profile <#sect_X.3>`__ defines characteristics of the
Application Profile Class that are constant across all specific
Application Profiles in the class.

.. _sect_X.3.1:

SOP Classes and Transfer Syntaxes
---------------------------------

`SOP Classes and Transfer Syntaxes <#sect_X.3.1>`__ lists the SOP
Classes and Transfer Syntaxes common to all specific Application
Profiles in the class, if any. This section specifies which SOP Classes
are mandatory and optional for the roles of FSC, FSR, and FSU, including
any required groupings or SOP options.

.. _sect_X.3.2:

Physical Media and Media Formats
--------------------------------

`Physical Media and Media Formats <#sect_X.3.2>`__ defines the physical
media and corresponding media formats common to all specific Application
Profiles in the class, if any.

This section also specifies any file service functionality beyond the
DICOM File Service required by the clinical application to be supplied
by the Media Format Layer.

.. _sect_X.3.3:

Directory Information in DICOMDIR
---------------------------------

`Directory Information in DICOMDIR <#sect_X.3.3>`__ specifies the type
of Directory Records that shall be supported and any additional
associated keys. It also defines any extensions to or specializations of
the Basic Directory Information Object Definition, if any.

.. _sect_X.3.4:

Other Parameters
----------------

`Other Parameters <#sect_X.3.4>`__ is optional; if present, it should
define any other parameters common to all specific Application Profiles
in the class, which may need to be specified in order to ensure
interoperable media interchange.

.. _sect_X.4:

Specific Application Profiles
-----------------------------

`Specific Application Profiles <#sect_X.4>`__ and following, each define
the unique characteristics of a specific Application Profile. If there
are any Application Profile specific changes to IODs, Transfer Syntax,
DICOMDIR, or other general class requirements, they should be described
for each Application Profile that specifies such changes.

.. _sect_X.3.5:

Security Parameters
-------------------

`Security Parameters <#sect_X.3.5>`__ is optional; if absent, the
Application Profile is unsecure and the Secure DICOM File Format shall
not be used for any DICOM File in the File-set.

If present, this section defines the Media Storage Security Profile to
be used for encapsulating *all*\ DICOM Files in the File-set, including
the DICOM Directory. If this section is present, the Application Profile
is called *Secure Media Storage Application Profile*.

