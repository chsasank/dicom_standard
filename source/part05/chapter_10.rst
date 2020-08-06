.. _chapter_10:

Transfer Syntax
===============

A Transfer Syntax is a set of encoding rules able to unambiguously
represent one or more Abstract Syntaxes. In particular, it allows
communicating Application Entities to negotiate common encoding
techniques they both support (e.g., byte ordering, compression, etc.). A
Transfer Syntax is an attribute of a Presentation Context, one or more
of which are negotiated at the establishment of an Association between
DICOM Application Entities. This Association negotiation is specified in
and discussed in .

The selection of a Transfer Syntax applies to the encoding rules for the
Data Set portion of a DICOM Message only. All DICOM Standard and Private
Transfer Syntaxes implicitly specify a fixed encoding for the Command
Set portion of a DICOM Message as specified in .

This Part of the DICOM Standard defines standard DICOM Transfer Syntaxes
and assigns a unique Transfer Syntax Name to each one. The standard
DICOM Transfer Syntaxes are specified in `Transfer Syntax Specifications
(Normative) <#chapter_A>`__. The DICOM notation for Transfer Syntax
names is the notation used for UIDs (see `Unique Identifiers
(UIDs) <#chapter_9>`__).

The organization responsible for the definition and registration of
DICOM Transfer Syntaxes is NEMA. NEMA guarantees uniqueness for all
DICOM Transfer Syntax Names.

Privately defined Transfer Syntax Names may also be used; however, they
will not be registered by NEMA. Organizations that define private
Transfer Syntax Names shall follow the registration process defined in
`Unique Identifier Registration <#sect_9.2>`__.

.. _sect_10.1:

DICOM Default Transfer Syntax
-----------------------------

DICOM defines a default Transfer Syntax, the DICOM Implicit VR Little
Endian Transfer Syntax (UID = "1.2.840.10008.1.2 "), which shall be
supported by every conformant DICOM Implementation. This implies that:

a. If an Application Entity issues an A-ASSOCIATE request, it shall
   offer the DICOM Implicit VR Little Endian Transfer Syntax in at least
   one of the Presentation Contexts associated with each offered
   Abstract Syntax.

   .. note::

      Offering Abstract Syntax (AS1) in two Presentation Contexts with
      Transfer Syntaxes (TS1) and (TS2) is not valid, but offering
      AS1-TS1, AS1-TS2 and AS1-TSD is valid because the DICOM Default
      Little Endian Transfer Syntax (TSD) is present in at least one of
      the Presentation Contexts that are based on Abstract Syntax (AS1).

b. If an Application Entity receives an A-ASSOCIATE indication
   corresponding to a request that follows the requirements specified in
   `DICOM Default Transfer Syntax <#sect_10.1>`__ (a), every
   Presentation Context related to a given Abstract Syntax cannot be
   rejected in an A-ASSOCIATE response for the reason that none of the
   Transfer Syntaxes are supported.

Both of these requirements, (a) and (b), are waived when the Application
Entity sending the pixel data has only access to the pixel data in lossy
compressed form or the pixel data in a lossless compressed form that is
of such length that it cannot be encoded in the default Transfer Syntax,
and a Transfer Syntax that uses a pixel data reference is not offered.

Requirement (b) to accept the default Transfer Syntax is waived if a
Transfer Syntax that uses a pixel data reference is offered.

.. note::

   In other words, every sending AE is required to be able to convert
   any Data Set it is going to transmit into the default Transfer
   Syntax, regardless of the form in which it originally received or
   stored the Data Set, except in the cases of when the decompressed
   Pixel Data is too large to encode in the default Transfer Syntax or
   is received in a lossy compressed form. In the case of lossy
   compressed Pixel Data, the sending AE is permitted to propose only
   the lossy compressed Transfer Syntax appropriate to the lossy form
   that was received. In the case of lossless compressed Pixel Data that
   is too large to encode in the default Transfer Syntax, the sending AE
   is permitted to propose any appropriate lossless compression Transfer
   Syntax, not necessarily that in which the image was received, as an
   alternative to the default Transfer Syntax.

   This waiver does not apply to Data Sets received in a lossless
   compressed form if the decompressed Pixel Data is small enough to
   encode in the default Transfer Syntax, which means that any AE
   receiving a Data Set in a lossless compressed Transfer Syntax that
   needs to re-send the Data Set is required to be able to decompress it
   in order to support (at least) the default Transfer Syntax.

   Similar concerns apply to the Web Services transactions and are
   addressed by specific requirements in .

.. _sect_10.2:

Transfer Syntax for a DICOM Default of Lossless JPEG Compression
----------------------------------------------------------------

DICOM defines a default for lossless JPEG Image Compression, which uses
a subset of coding Process 14 with a first-order prediction (Selection
Value 1). It is identified by Transfer Syntax UID =
"1.2.840.10008.1.2.4.70" and shall be supported by every DICOM
implementation that chooses to support one or more of the lossless JPEG
compression processes. This implies that:

a. If an Application Entity issues an A-ASSOCIATE request where any
   offered Abstract Syntaxes is associated in one or more Presentation
   Context with a JPEG lossless compression Transfer Syntax, at least
   one of the Presentation Contexts that include this Abstract Syntax,
   shall include the DICOM Default Lossless JPEG Compression Transfer
   Syntax and the DICOM Default Transfer Syntax (uncompressed).

   .. note::

      Offering Abstract Syntax (AS1) in two Presentation Contexts with
      Transfer Syntaxes JPEG lossless (JL1) and (JL2) is not valid, but
      offering AS1-JL1, AS1-JL2, AS1-TSD, and AS1-JLD is valid because
      the DICOM Default JPEG Lossless Transfer Syntax (JLD) and the
      DICOM Default Transfer Syntax (TSD) are present in at least one of
      the Presentation Contexts that are based on Abstract Syntax (AS1).

b. If an Application Entity that supports one or more lossless JPEG
   Transfer Syntax receives an A-ASSOCIATE indication corresponding to a
   request that follows the requirements specified in `Transfer Syntax
   for a DICOM Default of Lossless JPEG Compression <#sect_10.2>`__ (a),
   every Presentation Context related to a given Abstract Syntax cannot
   be rejected in an A-ASSOCIATE response for the reason that the DICOM
   Default lossless JPEG Transfer Syntax is not supported.

.. _sect_10.3:

Transfer Syntaxes for a DICOM Default of Lossy JPEG Compression
---------------------------------------------------------------

DICOM defines defaults for Lossy JPEG Image Compression, one for 8-bit
images and the other for 12-bit images. JPEG coding Process 1
(identified by Transfer Syntax UID = "1.2.840.10008.1.2.4.50 ") is used
for 8-bit images. JPEG coding Process 4 (identified by Transfer Syntax
UID = "1.2.840.10008.1.2.4.51 ") is used for 12-bit images. This implies
that:

a. If an Application Entity issues an A-ASSOCIATE request where any
   offered Abstract Syntaxes is associated in one or more Presentation
   Context(s) with a JPEG lossy compression Transfer Syntax, at least
   one of the Presentation Contexts that include this Abstract Syntax,
   shall include the appropriate DICOM Default Lossy JPEG Compression
   Transfer Syntax.

   .. note::

      Offering Abstract Syntax (AS1) in two Presentation Contexts with
      Transfer Syntaxes JPEG lossy (JL1) and (JL2) is not valid, but
      offering AS1-JL1, AS1-JL2 and AS1-JLD is valid because the DICOM
      Default JPEG Lossy Transfer Syntax (JLD) is present in at least
      one of the Presentation Contexts that are based on Abstract Syntax
      (AS1).2. The DICOM Default Transfer Syntax (uncompressed) may be
      offered if the sender has access to the original pixel data in an
      uncompressed or lossless compressed form.

b. If an Application Entity that supports one or more Lossy JPEG
   Transfer Syntaxes receives an A-ASSOCIATE indication corresponding to
   a request that follows the requirements specified in `Transfer
   Syntaxes for a DICOM Default of Lossy JPEG
   Compression <#sect_10.3>`__ (a), every Presentation Context related
   to a given Abstract Syntax cannot be rejected in an A-ASSOCIATE
   response for the reason that the DICOM Default lossy JPEG Transfer
   Syntax is not supported.

.. note::

   The 12 bit default Transfer Syntax 1.2.840.10008.1.2.4.51 can also be
   used to encode 8 bit images, but the bit stream required is not
   identical to that used in the 8 bit default Transfer Syntax
   1.2.840.10008.1.2.4.50 (see `JPEG Image
   Compression <#sect_A.4.1>`__).

.. _sect_10.4:

Transfer Syntax For DICOM RLE Image Compression
-----------------------------------------------

DICOM defines the RLE Image Compression (see `Encapsulated RLE
Compressed Images (Normative) <#chapter_G>`__). This implies that:

a. If an Application Entity issues an A-ASSOCIATE request where any
   offered Abstract Syntaxes is associated in one or more Presentation
   Contexts(s) with RLE compression Transfer Syntax, at least one of the
   Presentation Contexts that include this Abstract Syntax, shall
   include the DICOM Default Transfer Syntax (uncompressed).

.. _sect_10.5:

Transfer Syntax For A DICOM Default of Lossless and Lossy (Near-lossless) JPEG-LS Compression
---------------------------------------------------------------------------------------------

One Transfer Syntax is specified for JPEG-LS Lossless Image Compression,
and one Transfer Syntax is specified for JPEG-LS Lossy (Near-Lossless)
Image Compression. The JPEG-LS Lossless Transfer Syntax shall be
supported as a baseline if the JPEG-LS Lossy (Near-Lossless) Transfer
Syntax is supported.

.. _sect_10.6:

Transfer Syntax For JPEG 2000 Compression
-----------------------------------------

One Transfer Syntax is specified for JPEG 2000 Image Compression
(Lossless Only), and one Transfer Syntax is specified for JPEG 2000
Image Compression. Either of these may be negotiated separately and
there is no default or baseline specified (other than described in
`DICOM Default Transfer Syntax <#sect_10.1>`__).

.. note::

   1. All JPEG 2000 codecs are required by
      `biblioentry_title <#biblio_ISOIEC15444-1>`__ to support both
      reversible and irreversible wavelet and multi-component
      transformations. The reason for specifying two separate Transfer
      Syntaxes in DICOM is to allow an application to request the
      transfer of images in a lossless manner when possible. The JPEG
      2000 Image Compression Transfer Syntax allows for either lossless
      or lossy compression to be used at the sender's discretion.

   2. No baseline using other compression schemes is required.

   3. When the pixel data has been received in the JPEG 2000 Image
      Compression Transfer Syntax, since it may have been lossy
      compressed, the waiver of the requirement in `DICOM Default
      Transfer Syntax <#sect_10.1>`__ to support the DICOM default
      Transfer Syntax still applies.

In addition, one Transfer Syntax is specified for JPEG 2000
Multi-component Image Compression (Lossless Only) with Multi-Component
Transformation Extensions, and one Transfer Syntax is specified for JPEG
2000 Multi-component Image Compression with Multi-Component
Transformation Extensions. Either of these may be negotiated separately
and there is no default or baseline specified (other than described in
`DICOM Default Transfer Syntax <#sect_10.1>`__).

.. note::

   JPEG 2000 codecs that support the Part 2 JPEG 2000 Multi-Component
   Transformation Extensions are required to support all the
   multi-component extensions as described in Annex J of
   `biblioentry_title <#biblio_ISOIEC15444-2>`__. This includes both
   array based transformations and the 9-7 and 5-3 wavelet
   transformations that are also used in Part 1 of JPEG 2000. This also
   includes component reordering, component collections and application
   of more than one multi-component transformation in succession.

.. _sect_10.7:

Transfer Syntax For MPEG2 Main Profile / Main Level Video Compression
---------------------------------------------------------------------

One Transfer Syntax is specified for MPEG2 Main Profile / Main Level
Video Compression.

.. _sect_10.8:

Transfer Syntax For JPIP Referenced Pixel Data
----------------------------------------------

Two Transfer Syntaxes are specified for JPIP Referenced Pixel Data.

The persistence of the references in objects transferred with one of
these Transfer Syntaxes is not defined. That is, applications should
make no assumptions as to the timeframe when the referenced pixel data
will be available. Due to the indeterminate time that the URL remains
valid, it may be inappropriate to cache the URL. Because the pixel data
may not have been retrieved in its entirety or full fidelity, it may be
inappropriate to use this Transfer Syntax for the purpose of permanent
storage or to reference such instances in Storage Commitment and
Performed Procedure Step service classes.

These Transfer Syntaxes shall not be used for media storage defined by .

.. _sect_10.9:

Transfer Syntax For MPEG2 Main Profile / High Level Video Compression
---------------------------------------------------------------------

One Transfer Syntax is specified for MPEG2 Main Profile / High Level
Video Compression.

.. _sect_10.10:

Transfer Syntax For MPEG-4 AVC/H.264 High Profile / Level 4.1 Video Compression
-------------------------------------------------------------------------------

One Transfer Syntax is specified for MPEG-4 AVC/H.264 High Profile /
Level 4.1 Video Compression and one Transfer Syntax is specified for
MPEG-4 AVC/H.264 BD-compliant High Profile / Level 4.1. Transfer Syntax
MPEG-4 AVC/H.264 High Profile / Level 4.1 corresponds to the ITU-T H.264
standard's profile and level specifications. Transfer Syntax MPEG-4
AVC/H.264 BD-compliant High Profile / Level 4.1 corresponds to a
restricted set of spatial and temporal resolutions described Table 8-4.
This Transfer Syntax limits the ITU-T H.264 High Profile / Level 4.1 to
HD video formats that are supported by Blu-ray™ (BDRWP 2.B).

.. _sect_10.11:

Transfer Syntaxes for MPEG-4 AVC/H.264 High Profile / Level 4.2 Video Compression
---------------------------------------------------------------------------------

One Transfer Syntax is specified for MPEG-4 AVC/H.264 High Profile /
Level 4.2 for 2D Video Compression and one Transfer Syntax is specified
for MPEG-4 AVC/H.264 High Profile / Level 4.2 for 3D Video Compression.
Transfer Syntax MPEG-4 AVC/H.264 High Profile / Level 4.2 for 2D Video
Compression corresponds to the ITU-T H.264 standard's profile and level
specifications except that the use of frame packing formats for 3D video
is not allowed as defined in `table_title <#table_8-8>`__. Transfer
Syntax MPEG-4 AVC/H.264 High Profile / Level 4.2 for 3D Video
Compression corresponds to the ITU-T H.264 standard's profile and level
specifications. It should be used for transmitting stereoscopic 3D
content with frame packing formats as defined in
`table_title <#table_8-8>`__.

.. _sect_10.12:

Transfer Syntax For MPEG-4 AVC/H.264 Stereo High Profile / Level 4.2 Video Compression
--------------------------------------------------------------------------------------

One Transfer Syntax is specified for MPEG-4 AVC/H.264 Stereo High
Profile / Level 4.2 Video Compression. Transfer Syntax MPEG-4 AVC/H.264
Stereo High Profile corresponds to the ITU-T H.264 standard's profile
and level specifications.

.. _sect_10.13:

Transfer Syntax for HEVC/H.265 Main Profile / Level 5.1 Video Compression
-------------------------------------------------------------------------

One Transfer Syntax is specified for HEVC/H.265 Main Profile / Level 5.1
Video Compression. Transfer Syntax HEVC/H.265 Main Profile corresponds
to the `biblioentry_title <#biblio_ISOIEC23008-2>`__ HEVC standard's
profile and level specifications.

.. _sect_10.14:

Transfer Syntax for HEVC/H.265 Main 10 Profile / Level 5.1 Video Compression
----------------------------------------------------------------------------

One Transfer Syntax is specified for HEVC/H.265 Main 10 Profile / Level
5.1 Video Compression. Transfer Syntax HEVC/H.265 Main 10 Profile
corresponds to the `biblioentry_title <#biblio_ISOIEC23008-2>`__ HEVC
standard's profile and level specifications.

.. _sect_10.15:

Transfer Syntax for SMPTE ST 2110-20 Uncompressed Progressive Active Video
--------------------------------------------------------------------------

This Transfer Syntax is used for Uncompressed Video pixels carried in a
DICOM-RTV Flow (separated from DICOM-RTV Metadata Flow) as described by
`biblioentry_title <#biblio_SMPTE_ST2110-20>`__, in the case the video
is progressive (e.g., 1080p). The main parameters of the transfer syntax
are described in `SMPTE ST 2110-20 Uncompressed Progressive Active Video
Transfer Syntax <#sect_A.8>`__.

.. _sect_10.16:

Transfer Syntax for SMPTE ST 2110-20 Uncompressed Interlaced Active Video
-------------------------------------------------------------------------

This Transfer Syntax is used for Uncompressed Video pixels carried in a
DICOM-RTV Flow (separated from DICOM-RTV Metadata Flow) as described by
`biblioentry_title <#biblio_SMPTE_ST2110-20>`__, in the case the video
is interlaced (e.g., 1080i). The main parameters of the transfer syntax
are described in `SMPTE ST 2110-20 Uncompressed Interlaced Active Video
Transfer Syntax <#sect_A.9>`__.

.. _sect_10.16.1:

Interlaced Vs. Progressive Video
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

Interlaced video supports transmitting video with a smaller bandwidth.
One frame contains only odd lines and the next one contains only even
lines. Interlaced video is acceptable for display but may cause problems
in image processing. It is recommended to use progressive video.
However, in case an original interlaced video signal is converted in the
DICOM-RTV format, it is recommended to maintain the interlaced format
and let the processing application deal with it.

.. _sect_10.17:

Transfer Syntax for SMPTE ST 2110-30 PCM Digital Audio
------------------------------------------------------

This Transfer Syntax is used for audio channel data carried in a
DICOM-RTV Flow (separated from DICOM-RTV Metadata Flow) as described by
`biblioentry_title <#biblio_SMPTE_ST2110-30>`__. The main parameters of
the transfer syntax are described in `: SMPTE ST 2110-30 PCM Audio
Transfer Syntax <#sect_A.10>`__.

