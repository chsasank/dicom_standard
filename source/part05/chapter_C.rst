.. _chapter_C:

DICOM Unique Identifier Registration Process (Informative)
==========================================================

This registration process applies to a number of unique identifiers that
share the same properties, structure and registration process. It
applies to the following identifiers:

-  The Values assigned to DICOM Data Elements of Value Representation VR
   = UID (see `table_title <#table_6.2-1>`__). Such Data Elements are
   defined in , , , and .

-  The DICOM Abstract Syntaxes Names. Abstract Syntax Names are defined
   in .

-  The DICOM Transfer Syntax Names. Transfer Syntax Names are defined in
   `Transfer Syntax Specifications (Normative) <#chapter_A>`__.

-  The DICOM Application Context Names. Application Context Names are
   defined in

UID structure is based on the numeric form of the OSI Object Identifier
as defined by `biblioentry_title <#biblio_ISOIEC8824>`__. Values shall
be registered as defined by `biblioentry_title <#biblio_ISOIEC9834-1>`__
to ensure global uniqueness.

The DICOM Standard assigns Values to a number of such unique
identifiers. The organization responsible for their registration is
NEMA, which guarantees uniqueness.

For privately registered identifiers, NEMA will not act as registration
authority. Related organizations shall obtain their proper registration
as defined for OSI Object Identifiers by
`biblioentry_title <#biblio_ISOIEC9834-1>`__ to ensure global
uniqueness. National Standards Organizations representing a number of
countries (e.g., UK, France, Japan, USA, etc.) for the International
Standards Organization act as a registration authority by delegation
from ISO, as defined by `biblioentry_title <#biblio_ISOIEC9834-1>`__.

.. note::

   1. For example, in the USA ANSI assigns, for a fee, Organization
      Identifiers to any requesting organization. Such an identifier may
      be used by the identified organization as a root to which it may
      add a suffix made of one or more components. The identified
      organization accepts the responsibility to properly register these
      suffixes to ensure uniqueness.

   2. Following are two typical examples of obtaining a UID <org root>.
      These examples are not intended to illustrate all the possible
      methods for obtaining a UID <org root>, see
      `biblioentry_title <#biblio_ISOIEC8824>`__ and
      `biblioentry_title <#biblio_ISOIEC9834-1>`__ for complete
      specifications. Organization identifiers may be obtained from
      various ISO member bodies (e.g., IBN in Belgium, ANSI in the
      United States, AFNOR in France, BSI in Great Britain, DIN in
      Germany, COSIRA in Canada).

      The first example shows the case of an <org root> issued by an ISO
      Member Body (ANSI in the USA in this example). The <org root> is
      composed of an identifier for ISO, a member body branch
      identifier, a country code and an organization ID. Note that there
      is no requirement that an implementation using an ANSI issued <org
      root> be made or located in the USA. The <org root> is made up of
      the following components: 1.2.840.xxxxx

      -  1 identifies ISO

      -  2 identifies the ISO member body branch

      -  840 identifies the country code of a specific ISO member body
         (U.S. for ANSI)

      -  xxxxx identifies a specific organization as registered by the
         ISO member body ANSI.

      The second example shows the case of an <org root> issued by ISO
      (is delegated to BSI) to an international organization. It is
      composed of an identifier for ISO, an international organization
      branch identifier, and an International Code Designator. The value
      of the<org root> is assigned by an international registration
      authority that may be used by many different UIDs defined by the
      same international organization. The <org root> is made up of the
      following components: 1.3.yyyy

      -  1 identifies ISO

      -  3 identifies the international organization branch

      -  yyyy identifies a specific organization as registered by an
         International Code Designator registration authority (see ISO
         6523).

   3. Example components of a <suffix> for unique identification of an
      image could include:

      -  product

      -  system identifier

      -  study, series and image numbers

      -  study, series and image date & times.

