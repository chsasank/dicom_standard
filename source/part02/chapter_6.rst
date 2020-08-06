.. _chapter_6:

Purpose of a Conformance Statement
==================================

An implementation need not employ all the optional components of the
DICOM Standard. After meeting the minimum general requirements, a
conformant DICOM implementation may utilize whatever SOP Classes,
communications protocols, Media Storage Application Profiles, optional
(Type 3) Attributes, codes and controlled terminology, etc., needed to
accomplish its designed task.

.. note::

   In fact, it is expected that an implementation might only support the
   SOP Classes related to its Real World Activities. For example, a
   simple film digitizer may not support the SOP Classes for other
   imaging modalities since such support may not be required. On the
   other hand, a complex storage server might be required to support SOP
   Classes from multiple modalities in order to adequately function as a
   storage server. The choice of which components of the DICOM Standard
   are utilized by an implementation depends heavily on the intended
   application and is beyond the scope of this Standard.

In addition, the DICOM Standard allows an implementation to extend or
specialize the DICOM defined SOP Classes, as well as define Private SOP
classes.

A Conformance Statement allows a user to determine which optional
components of the DICOM Standard are supported by a particular
implementation, and what additional extensions or specializations an
implementation adds. By comparing the Conformance Statements from two
different implementations, a knowledgeable user should be able to
determine whether and to what extent communications might be supported
between the two implementations.

Different structures are used for the content of Conformance Statements
depending on whether the implementation supports a DICOM network
interface, a DICOM Media Storage interface, or a combination thereof. In
the latter case, a single Conformance Statement shall be provided that
consists of the appropriate sections.

The first part of the conformance statement contains a DICOM Conformance
Statement Overview, which is typically a one-page description in the
beginning of the document providing a high level description and also
listing the Networking and Media Service Classes, including their roles
(SCU/SCP, FSC, FSR, etc.).

.. _sect_6.1:

Overview of Networking Section for Conformance Statements
---------------------------------------------------------

The networking section of a Conformance Statement consists of the
following major parts:

-  a functional overview containing the Application Data Flow Diagram
   that shows all the Application Entities, including any sequencing
   constraints among them. It also shows how they relate to both local
   and remote Real World Activities;

-  a more detailed specification of each Application Entity, listing the
   SOP Classes supported and outlining the policies with which it
   initiates or accepts associations;

-  for each Application Entity and Real-World Activity combination, a
   description of proposed (for Association Initiation) and acceptable
   (for Association Acceptance) Presentation Contexts;

.. note::

   A Presentation Context consists of an Abstract Syntax plus a list of
   acceptable Transfer Syntaxes. The Abstract Syntax identifies one SOP
   Class or Meta SOP Class (a collection of related SOP Classes
   identified by a single Abstract Syntax UID). By listing the
   Application Entities with their proposed and accepted Presentation
   Contexts, the Conformance Statement is identifying the set of
   Information Objects and Service Classes that are recognized by this
   implementation;

-  for each SOP Class related to an Abstract Syntax, a list of any SOP
   options supported;

-  a set of communications protocols that this implementation supports;

-  a description of any extensions, specializations, and publicly
   disclosed privatizations in this implementation;

-  a section describing DICOM related configuration details;

-  a description of any implementation details that may be related to
   DICOM conformance or interoperability;

-  a description of what codes and controlled terminology mechanisms are
   used.

.. _sect_6.2:

Overview of Media Storage Section for Conformance Statements
------------------------------------------------------------

The media storage section of a Conformance Statement consists of the
following major parts:

-  a functional overview containing the Application Data Flow Diagram
   that shows all the Application Entities, including any sequencing
   constraints among them. It also shows how they relate to both local
   and remote Real-World Activities;

-  a more detailed specification of each Application Entity listing the
   Media Storage Application Profiles supported (this defines SOP
   Classes supported and media selected), which outlines the policies
   with which it creates, reads, or updates File-sets on the media;

-  a list of optional SOP Classes supported;

-  for each Media Storage SOP Class related to a media storage
   Application Profile, a list of any SOP options supported;

-  for each Media Storage SOP Class related to a media storage
   Application Profile, a list of optional Transfer Syntaxes supported;

-  a description of any extensions, specializations, and publicly
   disclosed privatizations in this implementation such as Augmented or
   Private Application Profiles;

-  a section describing DICOM related configuration details;

-  a description of any implementation details that may be related to
   DICOM conformance or interoperability;

-  a description of what codes and controlled terminology mechanisms are
   used.

