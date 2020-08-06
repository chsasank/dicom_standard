.. _chapter_3:

Definitions
===========

For the purposes of this Standard the following definitions apply.

Application Entity
   See `biblioentry_title <#biblio_ISO7498-1>`__.

Application Process
   See `biblioentry_title <#biblio_ISO7498-1>`__.

Service
   See `biblioentry_title <#biblio_ISO7498-1>`__.

Transfer Syntax
   See `biblioentry_title <#biblio_ISO7498-1>`__.

Data Confidentiality
   See `biblioentry_title <#biblio_ISO7498-2>`__.

   .. note::

      The definition is "the property that information is not made
      available or disclosed to unauthorized individuals, entities or
      processes."

Data Origin Authentication
   See `biblioentry_title <#biblio_ISO7498-2>`__.

   .. note::

      The definition is "the corroboration that the source of data
      received is as claimed."

Data Integrity
   See `biblioentry_title <#biblio_ISO7498-2>`__.

   .. note::

      The definition is "the property that data has not been altered or
      destroyed in an unauthorized manner."

Service Provider
   See `biblioentry_title <#biblio_ISO8509>`__.

Service User
   See `biblioentry_title <#biblio_ISO8509>`__.

Abstract Syntax
   See `biblioentry_title <#biblio_ISO8822>`__.

Abstract Syntax Name
   See `biblioentry_title <#biblio_ISO8822>`__.

Attribute
   .

Service-Object Pair Class
   .

Information Object Definition
   .

Data Element
   .

Data Set
   .

Data Element Type
   .

Value
   .

Value Multiplicity
   .

Value Representation
   .

Service Object Pair Instance
   .

Implementation Class UID
   .

Application Profile
   A Media Storage Application Profile defines a selection of choices at
   the various layers of the DICOM Media Storage Model that are
   applicable to a specific need or context in which the media
   interchange is intended to be performed.

DICOM File Service
   The DICOM File Service specifies a minimum abstract view of files to
   be provided by the Media Format Layer. Constraining access to the
   content of files by the Application Entities through such a DICOM
   File Service boundary ensures Media Format and Physical Media
   independence.

DICOM File
   A DICOM File is a File with a content formatted according to the
   requirements of this Part of the DICOM Standard. In particular such
   files shall contain, the File Meta Information and a properly
   formatted Data Set.

DICOMDIR File
   A unique and mandatory DICOM File within a File-set that contains the
   Media Storage Directory SOP Class. This File is given a single
   component File ID, DICOMDIR.

File
   A File is an ordered string of zero or more bytes, where the first
   byte is at the beginning of the file and the last byte at the end of
   the File. Files are identified by a unique File ID and may by
   written, read and/or deleted.

File ID
   Files are identified by a File ID that is unique within the context
   of the File-set they belong to. A set of ordered File ID Components
   (up to a maximum of eight) forms a File ID.

File ID Component
   A string of one to eight characters of a defined character set.

File Meta Information
   The File Meta Information includes identifying information on the
   encapsulated Data Set. It is a mandatory header at the beginning of
   every DICOM File.

File-set
   A File-set is a collection of DICOM Files (and possibly non-DICOM
   Files) that share a common naming space within which File IDs are
   unique.

File-set Creator
   An Application Entity that creates the DICOMDIR File (see `Reserved
   DICOMDIR File ID <#sect_8.6>`__) and zero or more DICOM Files.

File-set Reader
   An Application Entity that accesses one or more files in a File-set.

File-set Updater
   An Application Entity that accesses Files, creates additional Files,
   or deletes existing Files in a File-set. A File-set Updater makes the
   appropriate alterations to the DICOMDIR file reflecting the additions
   or deletions.

DICOM File Format
   The DICOM File Format provides a means to encapsulate in a File the
   Data Set representing a SOP Instance related to a DICOM Information
   Object.

Media Format
   Data structures and associated policies that organize the bit streams
   defined by the Physical Media format into data file structures and
   associated file directories.

Media Storage Model
   The DICOM Media Storage Model pertains to the data structures used at
   different layers to achieve interoperability through media
   interchange.

Media Storage Services
   DICOM Media Storage Services define a set of operations with media
   that facilitate storage to and retrieval from the media of DICOM SOP
   Instances.

Physical Media
   A piece of material with recording capabilities for streams of bits.
   Characteristics of a Physical Media include form factor, mechanical
   characteristics, recording properties and rules for recording and
   organizing bit streams in accessible structures

Secure DICOM File
   A DICOM File that is encapsulated with the Cryptographic Message
   Syntax specified in RFC2630.

Secure File-set
   A File-set in which all DICOM Files are Secure DICOM Files.

Secure Media Storage Application Profile
   A DICOM Media Storage Application Profile that requires a Secure
   File-set.

