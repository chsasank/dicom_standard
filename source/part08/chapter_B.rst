.. _chapter_B:

Abstract and Transfer Syntaxes (Informative)
============================================

.. _sect_B.1:

Abstract Syntax Definition
--------------------------

An Abstract Syntax is the specification of Application Layer data
elements with associated semantics or Application Layer protocol control
information by using notation rules that are independent of the encoding
technique used to represent them.

.. note::

   In particular, it allows the communicating Application Entities to
   negotiate an agreed set of DICOM Data Elements (e.g., from a specific
   version of the Data Dictionary) and/or Information Object Class
   definitions.

.. _sect_B.2:

Transfer Syntax Definition
--------------------------

A Transfer Syntax is a set of encoding rules able to unambiguously
represent the data elements defined by one or more Abstract Syntaxes. In
particular, negotiation of Transfer Syntaxes allows the communicating
Application Entities to agree on the encoding techniques they are able
to support (e.g., byte ordering, compression, etc.).

.. _sect_B.3:

DICOM Abstract and Transfer Syntax Names Encoding and Registration
------------------------------------------------------------------

The Abstract and Transfer Syntax Name structure is based on the OSI
Object Identification (numeric form) as defined by ISO 8824. Abstract
and Transfer Syntax Names are registered values as defined by ISO 9834-1
to ensure global uniqueness. Abstract and Transfer Syntax Names are
encoded as defined in ISO 8825 (Object Identifiers of numeric form) when
the OSI network communication support is used as defined in Section 8.
They are encoded as defined in `DICOM UL Encoding Rules for Application
Contexts, Abstract Syntaxes, Transfer Syntaxes
(Normative) <#chapter_F>`__ when the TCP/IP network communication
support is used as defined in Section 9.

.. _sect_B.3.1:

DICOM Registered Abstract and Transfer Syntax Names
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

The organization responsible for the definition and registration of
DICOM Abstract and Transfer Syntax Names is NEMA. NEMA guarantees
uniqueness for all DICOM Abstract and Transfer Syntax Names. A choice of
DICOM registered Abstract and Transfer Syntax Names related to a
specific version of the DICOM Application Entities, as well as the
associated negotiation rules, are defined in for Abstract Syntaxes and
for Transfer Syntaxes.

.. _sect_B.3.2:

Privately Defined Abstract and Transfer Syntax Names
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

Privately defined Abstract and Transfer Syntax Names may also be used,
however, they will not be registered by NEMA. Organizations that define
private Abstract and Transfer Syntax Names are responsible to obtain
their proper registration defined for OSI Object Identifiers. National
Standards Organizations representing a number of countries (e.g., UK,
France, Germany, Japan, USA, etc.) to the International Standards
Organization act as a registration authority as defined by ISO 9834-1.

.. note::

   For example, in the USA, ANSI assigns (for a fee) Organization
   Identifiers to any requesting organization. This identifier is made
   of a series of four numeric components; 1 (identifies ISO), 2
   (identifies the ISO member bodies branch), 840 (identifies ANSI as
   the ISO member body representing the USA), and xxxxxx (identifies a
   specific organization and is issued by ANSI). Such an identifier may
   be used by the identified organization as a root to which it may add
   a suffix made of one or more numeric components. The identified
   organization accepts the responsibility to properly register these
   suffixes to ensure uniqueness.

