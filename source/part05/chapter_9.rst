.. _chapter_9:

Unique Identifiers (UIDs)
=========================

Unique Identifiers (UIDs) provide the capability to uniquely identify a
wide variety of items. They guarantee uniqueness across multiple
countries, sites, vendors and equipment. Different classes of objects,
instance of objects and information entities can be distinguished from
one another across the DICOM universe of discourse irrespective of any
semantic context.

.. note::

   For example the same UID value cannot be used to identify both a
   study instance (Study Instance UID) and a series instance (Series
   Instance UID) within that study or a different study. Implementers
   also need to be cautioned against building new UID values by
   derivation (for example by adding a suffix) from a UID assigned by
   another implementation.

The UID identification scheme is based on the OSI Object Identification
(numeric form) as defined by the
`biblioentry_title <#biblio_ISOIEC8824>`__ standard. All Unique
Identifiers, used within the context of the DICOM Standard, are
registered values as defined by
`biblioentry_title <#biblio_ISOIEC9834-1>`__ to ensure global
uniqueness. The uses of such UIDs are defined in the various Parts of
the DICOM Standard.

Each UID is composed of two parts, an <org root> and a <suffix>:

-  UID = <org root>.<suffix>

The <org root> portion of the UID uniquely identifies an organization,
(i.e., manufacturer, research organization, NEMA, etc.), and is composed
of a number of numeric components as defined by
`biblioentry_title <#biblio_ISOIEC8824>`__. The <suffix> portion of the
UID is also composed of a number of numeric components, and shall be
unique within the scope of the <org root>. This implies that the
organization identified in the <org root> is responsible for
guaranteeing <suffix> uniqueness by providing registration policies.
These policies shall guarantee <suffix> uniqueness for all UIDs created
by that organization. Unlike the <org root>, which may be common for
UIDs in an organization, the <suffix> shall take different unique values
between different UIDs that identify different objects.

The <org root> "1.2.840.10008" is reserved for DICOM defined items (such
as DICOM Transfer Syntaxes) and shall not be used for privately defined
items (such as an Image Instance).

Although a specific implementation may choose some particular structure
for its generated UIDs, it should never assume that a UID carries any
semantics. Thus, a UID shall not be "parsed" to find a particular value
or component. Component definition (for the suffix) is implementation
specific and may change as long as uniqueness is maintained. Parsing
UIDs may jeopardize the ability to inter-operate as implementations
evolve.

Example of UID structure is given in `DICOM Unique Identifier
Registration Process (Informative) <#chapter_C>`__.

.. _sect_9.1:

UID Encoding Rules
------------------

The DICOM UID encoding rules are defined as follows:

-  Each component of a UID is a number and shall consist of one or more
   digits. The first digit of each component shall not be zero unless
   the component is a single digit.

   .. note::

      Registration authorities may distribute components with
      non-significant leading zeroes. The leading zeroes should be
      ignored when being encoded (i.e.,"00029" would be encoded "29").

-  Each component numeric value shall be encoded using the characters
   0-9 of the Basic G0 Set of the International Reference Version of ISO
   646:1990 (the DICOM Default Character Repertoire).

-  Components shall be separated by the character "." (2EH).

-  If ending on an odd byte boundary, except when used for network
   negotiation (see ), one trailing NULL (00H), as a padding character,
   shall follow the last component in order to align the UID on an even
   byte boundary.

-  UIDs, shall not exceed 64 total characters, including the digits of
   each component, separators between components, and the NULL (00H)
   padding character if needed.

.. _sect_9.2:

Unique Identifier Registration
------------------------------

Each UID used in DICOM shall be defined and registered in one of the
following two ways:

-  DICOM defined and registered UIDs

-  Privately defined and registered UIDs

Both UIDs use the same encoding rules as defined in `UID Encoding
Rules <#sect_9.1>`__. See `DICOM Unique Identifier Registration Process
(Informative) <#chapter_C>`__ for a more detailed description of the UID
registration process.

.. _sect_9.2.1:

DICOM Defined and Registered Unique Identifiers
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

A limited number of registered DICOM Defined UIDs are used within the
DICOM Standard. The organization responsible for the definition and
registration of such DICOM UIDs is NEMA.

The registration process will rely on the publication of the DICOM
Registered UIDs in .

.. _sect_9.2.2:

Privately Defined Unique Identifiers
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

Privately Defined UIDs are commonly used within DICOM. However, such
UIDs will not be registered by NEMA. Organizations that define private
UIDs are responsible for properly registering their UIDs (at least
obtain a registered <Org Root>) as defined for OSI Object Identifiers
`biblioentry_title <#biblio_ISOIEC9834-1>`__. The private organization
defining the UID shall accept the responsibility of ensuring its
uniqueness.

