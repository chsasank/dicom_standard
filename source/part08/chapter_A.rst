.. _chapter_A:

Application Context Names (Informative)
=======================================

.. _sect_A.1:

Application Context Definition
------------------------------

An application context explicitly defines the set of application service
elements, related options and any other information necessary for the
interworking of Application Entities on an association. The usage of the
application context is defined in .

Two Application Entities when establishing an association agree on an
application context. The requestor of an association proposes an
Application Context Name and the acceptor returns either the same or a
different Application Context Name. The returned name specifies the
application context to be used for this association. The offer of an
alternate application context by the acceptor provides a mechanism for
limited negotiation. If the requestor cannot operate in the acceptor's
application context, it will issue an A-Abort request primitive. Such a
negotiation will facilitate the introduction of future versions of the
DICOM Application Entity.

.. _sect_A.2:

DICOM Application Context Name Encoding and Registration
--------------------------------------------------------

The Application Context Name structure is based on the OSI Object
Identification (numeric form) as defined by ISO 8824. Application
Context Names are registered values as defined by ISO 9834-1 to ensure
global uniqueness. They are encoded as defined in `DICOM UL Encoding
Rules for Application Contexts, Abstract Syntaxes, Transfer Syntaxes
(Normative) <#chapter_F>`__ when the TCP/IP network communication
support is used as defined in Section 9.

.. _sect_A.2.1:

DICOM Registered Application Context Names
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

The organization responsible for the definition and registration of
DICOM Application Context Names is NEMA. NEMA guarantees uniqueness for
all DICOM Application Context Names. A choice of DICOM registered
Application Context Names related to the DICOM Application Entities, as
well as the associated negotiation rules, are defined in .

