.. _chapter_8:

Encoding of Pixel, Overlay and Waveform Data
============================================

.. _sect_8.1:

Pixel and Overlay Data, and Related Data Elements
-------------------------------------------------

Pixel Data (7FE0,0010), Float Pixel Data (7FE0,0008), Double Float Pixel
Data (7FE0,0009) and Overlay Data (60xx,3000) shall be used for the
exchange of encoded graphical image data. These elements along with
additional Data Elements, specified as Attributes of the Image
Information Entities defined in , shall be used to describe the way in
which the Pixel Data and Overlay Data are encoded and shall be
interpreted. Finally, depending on the negotiated Transfer Syntax (see
`Transfer Syntax <#chapter_10>`__ and `Transfer Syntax Specifications
(Normative) <#chapter_A>`__), Pixel Data may be compressed.

Pixel Data (7FE0,0010) and Overlay Data (60xx,3000) have a VR of OW or
OB, depending on the negotiated Transfer Syntax (see `Transfer Syntax
Specifications (Normative) <#chapter_A>`__). The only difference between
OW and OB being that OB, an octet-stream, shall be unaffected by Byte
Ordering (see `Little Endian Byte Ordering <#sect_7.3>`__).

Float Pixel Data (7FE0,0008) has a Value Representation of OF.

Double Float Pixel Data (7FE0,0009) has a Value Representation of OD.

For Pixel Data values encoded in OF and OD, any value that is permitted
by the IEEE 754:1985 may be used, including NaN, +ve Infinity and -ve
Infinity. See `table_title <#table_6.2-1>`__

.. note::

   Float and double float pixel data values are not arbitrarily
   constrained to finite numbers, since it may be important for the
   application to signal that the result of a calculation that produced
   a pixel is an infinite value or not a number.

.. _sect_8.1.1:

Pixel Data Encoding of Related Data Elements
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

Encoded Pixel Data of various bit depths shall be accommodated. The
following three Data Elements shall define the Pixel structure:

-  Bits Allocated (0028,0100)

-  Bits Stored (0028,0101)

-  High Bit (0028,0102)

Each Pixel Cell shall contain a single Pixel Sample Value. The size of
the Pixel Cell shall be specified by Bits Allocated (0028,0100). Bits
Stored (0028,0101) defines the total number of these allocated bits that
will be used to represent a Pixel Sample Value. Bits Stored (0028,0101)
shall never be larger than Bits Allocated (0028,0100). High Bit
(0028,0102) specifies where the high order bit of the Bits Stored
(0028,0101) is to be placed with respect to the Bits Allocated
(0028,0100) specification. Bits Allocated (0028,0100) shall either be 1,
or a multiple of 8. High Bit (0028,0102) shall be one less than Bits
Stored (0028,0101).

.. note::

   1. For example, in Pixel Data with 16 bits (2 bytes) allocated, 12
      bits stored, and bit 11 specified as the high bit, one pixel
      sample is encoded in each 16-bit word, with the 4 most significant
      bits of each word not containing Pixel Data. See `Examples of
      Various Pixel Data and Overlay Encoding Schemes
      (Informative) <#chapter_D>`__ for other examples of the basic
      encoding schemes.

   2. Formerly, bits not used for Pixel Sample Values were described as
      being usable for overlay planes, but this usage has been retired.
      See PS3.5-2004.

   3. Formerly, High Bit (0028,0102) was not restricted to be one less
      than Bits Stored (0028,0101) in this Part, or in the general case,
      though almost all Information Object Definitions in PS3.3 imposed
      such a restriction. See PS3.5 2014c.

   4. Receiving applications may not assume anything about the contents
      of unused bits, and in particular may not assume that they are
      zero, or that they contain sign extension bits.

Additional restrictions that are placed on acceptable Values for Bits
Allocated (0028,0100), Bits Stored (0028,0101), and High Bit (0028,0102)
for Pixel Data (7FE0,0010) are specified in the Information Object
Definitions in .

Restrictions are placed on acceptable Values for Bits Allocated
(0028,0100) for Float Pixel Data (7FE0,0008) and Double Float Pixel Data
(7FE0,0009), such that only a single Pixel Cell entirely occupies the
allocated bits specified by Bits Allocated (0028,0100), hence Bits
Stored (0028,0101) and High Bit (0028,0102) are not sent.

Also, the Value Field containing Pixel Data, like all other Value Fields
in DICOM, shall be an even number of bytes in length. This means that
the Value Field may need to be padded with data that is not part of the
image and shall not be considered significant. If needed, the padding
bits shall be appended to the end of the Value Field, and shall be used
only to extend the data to the next even byte increment of length.

.. note::

   The 32-bit Value Length Field limits the maximum size of large data
   values such as Pixel Data sent in a Native Format (encoded in
   Transfer Syntaxes that use only the unencapsulated form).

In a multi-frame object that is transmitted in Native Format, the
individual frames are not padded. The individual frames shall be
concatenated and padding bits (if necessary) apply to the complete Value
Field. At least one frame shall be present.

.. note::

   Receiving applications should be aware that some older applications
   may send Pixel Data with excess padding, which was not explicitly
   prohibited in earlier versions of the Standard. Applications should
   be prepared to accept such Pixel Data elements, but may delete the
   excess padding. In no case should a sending application place private
   data in the padding data.

The field of bits representing the value of a Pixel Sample shall be a
binary 2's complement integer or an unsigned integer, as specified by
the Data Element Pixel Representation (0028,0103). The sign bit shall be
the High Bit in a Pixel Sample Value that is a 2's complement integer.
The minimum actual Pixel Sample Value encountered in the Pixel Data is
specified by Smallest Image Pixel Value (0028,0106) while the maximum
value is specified by Largest Image Pixel Value (0028,0107).

.. _sect_8.1.2:

Overlay Data Encoding of Related Data Elements
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

Encoded Overlay Planes always have a bit depth of 1, and are encoded
separately from the Pixel Data in Overlay Data (60xx,3000). The
following two Data Elements shall define the Overlay Plane structure:

-  Overlay Bits Allocated (60xx,0100)

-  Overlay Bit Position (60xx,0102)

.. note::

   1. There is no Data Element analogous to Bits Stored (0028,0101)
      since Overlay Planes always have a bit depth of 1.

   2. Restrictions on the allowed values for these Data Elements are
      defined in . Formerly overlay data stored in unused bits of Pixel
      Data (7FE0,0010) was described, and these attributes had
      meaningful values but this usage has been retired. See PS3.5-2004.
      For overlays encoded in Overlay Data (60xx,3000), Overlay Bits
      Allocated (60xx,0100) is always 1 and Overlay Bit Position
      (60xx,0102) is always 0.

For Overlay Data (60xx,3000), the Value Representation OW is most often
required. The Value Representation OB may also be used for Overlay Data
in cases where the Value Representation is explicitly conveyed (see
`Transfer Syntax Specifications (Normative) <#chapter_A>`__).

.. note::

   The DICOM default Transfer Syntax (Implicit VR Little Endian) does
   not explicitly convey Value Representation and therefore the VR of OB
   may not be used for Pixel Data when using the default Transfer
   Syntax.

Overlay Data is encoded as the direct concatenation of the bits of a
single Overlay Plane, where the first bit of an Overlay Plane is encoded
in the least significant bit, immediately followed by the next bit of
the Overlay Plane in the next most significant bit. When the Overlay
Data crosses a word boundary in the OW case, or a byte boundary in the
OB case, it shall continue to be encoded, least significant bit to most
significant bit, in the next word, or byte, respectively (see `Examples
of Various Pixel Data and Overlay Encoding Schemes
(Informative) <#chapter_D>`__). For Overlay Data encoded with the Value
Representation OW, the byte ordering of the resulting 2-byte words is
defined by the Little Endian Transfer Syntaxes negotiated at the
Association Establishment (see `Transfer Syntax Specifications
(Normative) <#chapter_A>`__).

.. note::

   For Overlay Data encoded with the Value Representation OB, the
   Overlay Data encoding is unaffected by byte ordering.

.. _sect_8.2:

Native or Encapsulated Format Encoding
--------------------------------------

Pixel data conveyed in the Pixel Data (7FE0,0010) may be sent either in
a Native (uncompressed) Format or in an Encapsulated Format (e.g.,
compressed) defined outside the DICOM Standard.

If Pixel Data (7FE0,0010) is sent in a Native Format, then the
Photometric Interpretation (0028,0004) shall be other than:

-  YBR_RCT

-  YBR_ICT

-  YBR_PARTIAL_420

.. note::

   These values are not permitted because they are not encodable in an
   uncompressed form.

Pixel Data conveyed in the Float Pixel Data (7FE0,0008) or Double Float
Pixel Data (7FE0,0009) shall be in a Native (uncompressed) Format if
encoded in a Standard Transfer Syntax.

.. note::

   1. In future, if Standard Transfer Syntaxes are defined for
      compression of Float Pixel Data (7FE0,0008) or Double Float Pixel
      Data (7FE0,0009), this constraint may be relaxed and Encapsulated
      Format permitted.

   2. This constraint does not apply to Private Transfer Syntaxes.

If Pixel Data (7FE0,0010) is sent in a Native Format, the Value
Representation OW is most often required. The Value Representation OB
may also be used for Pixel Data (7FE0,0010) in cases where Bits
Allocated has a value less than or equal to 8, but only with Transfer
Syntaxes where the Value Representation is explicitly conveyed (see
`Transfer Syntax Specifications (Normative) <#chapter_A>`__).

.. note::

   1. The DICOM default Transfer Syntax (Implicit VR Little Endian) does
      not explicitly convey Value Representation and therefore the VR of
      OB may not be used for Pixel Data (7FE0,0010) when using the
      default Transfer Syntax.

   2. The 32-bit Value Length Field limits the maximum size of large
      data values such as Pixel Data sent in a Native Format.

Float Pixel Data (7FE0,0008) is sent in Native Format; the Value
Representation shall be OF, Bits Allocated (0028,0100) shall be 32, Bits
Stored (0028,0101), High Bit (0028,0102) and Pixel Representation
(0028,0103) shall not be present.

Double Float Pixel Data (7FE0,0009) is sent in Native Format; the Value
Representation shall be OD, Bits Allocated (0028,0100) shall be 64, Bits
Stored (0028,0101) and High Bit (0028,0102) and Pixel Representation
(0028,0103) shall not be present.

It is not permitted to have more than one of Pixel Data Provider URL
(0028,7FE0), Pixel Data (7FE0,0010), Float Pixel Data (7FE0,0008) or
Double Float Pixel Data (7FE0,0009) in the top level Data Set.

.. note::

   Pixel Data encoded in Float Pixel Data (7FE0,0008) or Double Float
   Pixel Data (7FE0,0009) can be considered as consisting of Pixel Cells
   that entirely occupy the allocated bits, and therefore do not cross
   word boundaries.

Native format Pixel Cells are encoded as the direct concatenation of the
bits of each Pixel Cell, the least significant bit of each Pixel Cell is
encoded in the least significant bit of the encoded word or byte,
immediately followed by the next most significant bit of each Pixel Cell
in the next most significant bit of the encoded word or byte,
successively until all bits of the Pixel Cell have been encoded, then
immediately followed by the least significant bit of the next Pixel Cell
in the next most significant bit of the encoded word or byte. The number
of bits of each Pixel Cell is defined by the Bits Allocated (0028,0100)
Data Element Value. When a Pixel Cell crosses a word boundary in the OW
case, or a byte boundary in the OB case, it shall continue to be
encoded, least significant bit to most significant bit, in the next
word, or byte, respectively (see `Examples of Various Pixel Data and
Overlay Encoding Schemes (Informative) <#chapter_D>`__). For Pixel Data
(7FE0,0010) encoded with the Value Representation OW, the byte ordering
of the resulting 2-byte words is defined by the Little Endian Transfer
Syntaxes negotiated at the Association Establishment (see `Transfer
Syntax Specifications (Normative) <#chapter_A>`__).

.. note::

   1. For Pixel Data (7FE0,0010) encoded with the Value Representation
      OB, the Pixel Data (7FE0,0010) encoding is unaffected by byte
      ordering.

   2. If encoding Pixel Data (7FE0,0010) with a Value for Bits Allocated
      (0028,0100) not equal to 16 be sure to read and understand
      `Examples of Various Pixel Data and Overlay Encoding Schemes
      (Informative) <#chapter_D>`__.

If sent in an Encapsulated Format (i.e., other than the Native Format)
the Value Representation OB is used. The Pixel Cells are encoded
according to the encoding process defined by one of the negotiated
Transfer Syntaxes (see `Transfer Syntax Specifications
(Normative) <#chapter_A>`__). The encapsulated pixel stream of encoded
pixel data is segmented into one or more Fragments, each of which
conveys its own explicit length. The sequence of Fragments of the
encapsulated pixel stream is terminated by a delimiter, thus allowing
the support of encoding processes where the resulting length of the
entire pixel stream is not known until it is entirely encoded. This
Encapsulated Format supports both Single-Frame and Multi-Frame images
(as defined in ). At least one frame shall be present, and hence at
least one fragment will be present.

.. note::

   Depending on the Transfer Syntax, a frame may be entirely contained
   within a single fragment, or may span multiple fragments to support
   buffering during compression or to avoid exceeding the maximum size
   of a fixed length fragment. A recipient can detect fragmentation of
   frames by comparing the number of fragments (the number of Items
   minus one for the Basic Offset Table) with the number of frames. Some
   performance optimizations may be available to a recipient in the
   absence of fragmentation of frames, but an implementation that fails
   to support such fragmentation does not conform to the Standard.

.. _sect_8.2.1:

JPEG Image Compression
~~~~~~~~~~~~~~~~~~~~~~

DICOM provides a mechanism for supporting the use of JPEG Image
Compression through the Encapsulated Format (see ). `Transfer Syntax
Specifications (Normative) <#chapter_A>`__ defines a number of Transfer
Syntaxes that reference the JPEG Standard and provide a number of
lossless (bit preserving) and lossy compression schemes.

.. note::

   The context where the usage of lossy compression of medical images is
   clinically acceptable is beyond the scope of the DICOM Standard. The
   policies associated with the selection of appropriate compression
   parameters (e.g., compression ratio) for JPEG lossy compression is
   also beyond the scope of this Standard.

In order to facilitate interoperability of implementations conforming to
the DICOM Standard that elect to use one or more of the Transfer
Syntaxes for JPEG Image Compression, the following policy is specified:

-  Any implementation that conforms to the DICOM Standard and has
   elected to support any one of the Transfer Syntaxes for lossless JPEG
   Image Compression, shall support the following lossless compression:
   The subset (first-order horizontal prediction [Selection Value 1) of
   JPEG Process 14 (DPCM, non-hierarchical with Huffman coding) (see
   `Encapsulated Images As Part of A DICOM Message
   (Informative) <#chapter_F>`__).

-  Any implementation that conforms to the DICOM Standard and has
   elected to support any one of the Transfer Syntaxes for 8-bit lossy
   JPEG Image Compression, shall support the JPEG Baseline Compression
   (coding Process 1).

-  Any implementation that conforms to the DICOM Standard and has
   elected to support any one of the Transfer Syntaxes for 12-bit lossy
   JPEG Image Compression, shall support the JPEG Compression Process 4.

.. note::

   The DICOM conformance statement shall differentiate whether or not
   the implementation is capable of simply receiving or receiving and
   processing JPEG encoded images (see ).

The use of the DICOM Encapsulated Format to support JPEG Compressed
Pixel Data requires that the Data Elements that are related to the Pixel
Data encoding (e.g., Photometric Interpretation, Samples per Pixel,
Planar Configuration, Bits Allocated, Bits Stored, High Bit, Pixel
Representation, Rows, Columns, etc.) shall contain values that are
consistent with the characteristics of the compressed data stream.

The requirements when using a Standard Photometric Interpretation (i.e.,
a Defined Term from ) are specified in `table_title <#table_8.2.1-1>`__
and `table_title <#table_8.2.1-2>`__. No other Standard Photometric
Interpretation values shall be used.

.. table:: Valid Values of Pixel Data Related Attributes for JPEG Lossy
Transfer Syntaxes using Standard Photometric Interpretations

   +-------+-------+-------+-------+-------+-------+-------+-------+-------+
   | P     | Tra   | Tra   | Sa    | P     | Pixel | Bits  | Bits  | High  |
   | hotom | nsfer | nsfer | mples | lanar | Repr  | Allo  | S     | Bit   |
   | etric | S     | S     | per   | Con   | esent | cated | tored |       |
   | Inte  | yntax | yntax | Pixel | figur | ation |       |       |       |
   | rpret |       | UID   |       | ation |       |       |       |       |
   | ation |       |       |       |       |       |       |       |       |
   +=======+=======+=======+=======+=======+=======+=======+=======+=======+
   | M     | JPEG  | 1.    | 1     | a     | 0     | 8     | 8     | 7     |
   | ONOCH | Bas   | 2.840 |       | bsent |       |       |       |       |
   | ROME1 | eline | .1000 |       |       |       |       |       |       |
   |       |       | 8.1.2 |       |       |       |       |       |       |
   | M     |       | .4.50 |       |       |       |       |       |       |
   | ONOCH |       |       |       |       |       |       |       |       |
   | ROME2 |       |       |       |       |       |       |       |       |
   +-------+-------+-------+-------+-------+-------+-------+-------+-------+
   | M     | JPEG  | 1.    | 1     | a     | 0     | 8     | 8     | 7     |
   | ONOCH | Ext   | 2.840 |       | bsent |       |       |       |       |
   | ROME1 | ended | .1000 |       |       |       |       |       |       |
   |       |       | 8.1.2 |       |       |       |       |       |       |
   | M     |       | .4.51 |       |       |       |       |       |       |
   | ONOCH |       |       |       |       |       |       |       |       |
   | ROME2 |       |       |       |       |       |       |       |       |
   +-------+-------+-------+-------+-------+-------+-------+-------+-------+
   | M     | JPEG  | 1.    | 1     | a     | 0     | 16    | 12    | 11    |
   | ONOCH | Ext   | 2.840 |       | bsent |       |       |       |       |
   | ROME1 | ended | .1000 |       |       |       |       |       |       |
   |       |       | 8.1.2 |       |       |       |       |       |       |
   | M     |       | .4.51 |       |       |       |       |       |       |
   | ONOCH |       |       |       |       |       |       |       |       |
   | ROME2 |       |       |       |       |       |       |       |       |
   +-------+-------+-------+-------+-------+-------+-------+-------+-------+
   | YB    | JPEG  | 1.    | 3     | 0     | 0     | 8     | 8     | 7     |
   | R_FUL | Bas   | 2.840 |       |       |       |       |       |       |
   | L_422 | eline | .1000 |       |       |       |       |       |       |
   |       |       | 8.1.2 |       |       |       |       |       |       |
   | RGB   |       | .4.50 |       |       |       |       |       |       |
   +-------+-------+-------+-------+-------+-------+-------+-------+-------+

.. table:: Valid Values of Pixel Data Related Attributes for JPEG
Lossless Transfer Syntaxes using Standard Photometric Interpretations

   +-------+-------+-------+-------+-------+-------+-------+-------+-------+
   | P     | Tra   | Tra   | Sa    | P     | Pixel | Bits  | Bits  | High  |
   | hotom | nsfer | nsfer | mples | lanar | Repr  | Allo  | S     | Bit   |
   | etric | S     | S     | per   | Con   | esent | cated | tored |       |
   | Inte  | yntax | yntax | Pixel | figur | ation |       |       |       |
   | rpret |       | UID   |       | ation |       |       |       |       |
   | ation |       |       |       |       |       |       |       |       |
   +=======+=======+=======+=======+=======+=======+=======+=======+=======+
   | M     | JPEG  | 1.    | 1     | a     | 0 or  | 8 or  | 1-16  | 0-15  |
   | ONOCH | Loss  | 2.840 |       | bsent | 1     | 16    |       |       |
   | ROME1 | less, | .1000 |       |       |       |       |       |       |
   |       | N     | 8.1.2 |       |       |       |       |       |       |
   | M     | on-Hi | .4.57 |       |       |       |       |       |       |
   | ONOCH | erarc |       |       |       |       |       |       |       |
   | ROME2 | hical | 1.    |       |       |       |       |       |       |
   |       |       | 2.840 |       |       |       |       |       |       |
   |       | JPEG  | .1000 |       |       |       |       |       |       |
   |       | Loss  | 8.1.2 |       |       |       |       |       |       |
   |       | less, | .4.70 |       |       |       |       |       |       |
   |       | No    |       |       |       |       |       |       |       |
   |       | n-Hie |       |       |       |       |       |       |       |
   |       | rarch |       |       |       |       |       |       |       |
   |       | ical, |       |       |       |       |       |       |       |
   |       | SV1   |       |       |       |       |       |       |       |
   +-------+-------+-------+-------+-------+-------+-------+-------+-------+
   | PA    | JPEG  | 1.    | 1     | a     | 0     | 8 or  | 1-16  | 0-15  |
   | LETTE | Loss  | 2.840 |       | bsent |       | 16    |       |       |
   | COLOR | less, | .1000 |       |       |       |       |       |       |
   |       | N     | 8.1.2 |       |       |       |       |       |       |
   |       | on-Hi | .4.57 |       |       |       |       |       |       |
   |       | erarc |       |       |       |       |       |       |       |
   |       | hical | 1.    |       |       |       |       |       |       |
   |       |       | 2.840 |       |       |       |       |       |       |
   |       | JPEG  | .1000 |       |       |       |       |       |       |
   |       | Loss  | 8.1.2 |       |       |       |       |       |       |
   |       | less, | .4.70 |       |       |       |       |       |       |
   |       | No    |       |       |       |       |       |       |       |
   |       | n-Hie |       |       |       |       |       |       |       |
   |       | rarch |       |       |       |       |       |       |       |
   |       | ical, |       |       |       |       |       |       |       |
   |       | SV1   |       |       |       |       |       |       |       |
   +-------+-------+-------+-------+-------+-------+-------+-------+-------+
   | YBR   | JPEG  | 1.    | 3     | 0     | 0     | 8 or  | 1-16  | 0-15  |
   | _FULL | Loss  | 2.840 |       |       |       | 16    |       |       |
   |       | less, | .1000 |       |       |       |       |       |       |
   | RGB   | N     | 8.1.2 |       |       |       |       |       |       |
   |       | on-Hi | .4.57 |       |       |       |       |       |       |
   |       | erarc |       |       |       |       |       |       |       |
   |       | hical | 1.    |       |       |       |       |       |       |
   |       |       | 2.840 |       |       |       |       |       |       |
   |       | JPEG  | .1000 |       |       |       |       |       |       |
   |       | Loss  | 8.1.2 |       |       |       |       |       |       |
   |       | less, | .4.70 |       |       |       |       |       |       |
   |       | No    |       |       |       |       |       |       |       |
   |       | n-Hie |       |       |       |       |       |       |       |
   |       | rarch |       |       |       |       |       |       |       |
   |       | ical, |       |       |       |       |       |       |       |
   |       | SV1   |       |       |       |       |       |       |       |
   +-------+-------+-------+-------+-------+-------+-------+-------+-------+

The Pixel Data characteristics included in the JPEG Interchange Format
shall be used to decode the compressed data stream.

If APP2 marker segments with an identifier of "ICC_PROFILE" (as defined
in Annex B of `biblioentry_title <#biblio_ISOIEC15076-1>`__) are present
in the compressed data stream, their concatenated value shall be
identical to the value of ICC Profile (0028,2000) Attribute, if present,
excluding padding.

.. note::

   1. These requirements were formerly specified in terms of the
      "uncompressed pixel data from which the compressed data stream was
      derived". However, since the form of the "original" uncompressed
      data stream could vary between different implementations, this
      requirement is now specified in terms of consistency with what is
      encapsulated.

      When decompressing, should the characteristics explicitly
      specified in the compressed data stream (e.g., spatial subsampling
      or number of components or planar configuration) be inconsistent
      with those specified in the DICOM Data Elements, those explicitly
      specified in the compressed data stream should be used to control
      the decompression. The DICOM data elements, if inconsistent, can
      be regarded as suggestions as to the form in which an uncompressed
      Data Set might be encoded, subject to the general and IOD-specific
      rules for uncompressed Photometric Interpretation and Planar
      Configuration, which may require that decompressed data be
      converted to one of the permitted forms.

   2. Those characteristics not explicitly specified in the compressed
      data stream (e.g., the color space of the compressed components,
      which is not specified in the JPEG Interchange Format), or implied
      by the definition of the compression scheme (e.g., always unsigned
      in JPEG), can therefore be determined from the DICOM Data Element
      in the enclosing Data Set. For example a Photometric
      Interpretation of "YBR_FULL_422" would describe the color space
      that is commonly used to lossy compress images using JPEG. It is
      unusual to use an RGB color space for lossy compression, since no
      advantage is taken of correlation between the red, green and blue
      components (e.g., of luminance), and poor compression is achieved;
      however, for some applications this is permitted, e.g., Whole
      Slide Microscopy Images, to allow conversion to DICOM from
      proprietary formats without loss due to color space
      transformation.

   3. The JPEG Interchange Format is distinct from the JPEG File
      Interchange Format (JFIF). The JPEG Interchange Format is defined
      in `biblioentry_title <#biblio_ISOIEC10918-1>`__ section 4.9.1,
      and refers to the inclusion of decoding tables, as distinct from
      the "abbreviated format" in which these tables are not sent (and
      the decoder is assumed to already have them). The JPEG Interchange
      Format does NOT specify the color space. The JPEG File Interchange
      Format, not part of the original JPEG standard, but defined in
      `biblioentry_title <#biblio_ECMA_TR-098>`__ and
      `biblioentry_title <#biblio_ISOIEC10918-5>`__, is often used to
      store JPEG bit streams in consumer format files, and does include
      the ability to specify the color space of the components. The JFIF
      APP0 marker segment is NOT required to be present in DICOM
      encapsulated JPEG bit streams, and should not be relied upon to
      recognize the color space. Its presence is not forbidden (unlike
      the JP2 information for JPEG 2000 Transfer Syntaxes), but it is
      recommended that it be absent.

   4. Should the compression process be incapable of encoding a
      particular form of pixel data representation (e.g., JPEG cannot
      encode signed integers, only unsigned integers), then ideally only
      the appropriate form should be "fed" into the compression process.
      However, for certain characteristics described in DICOM Data
      Elements but not explicitly described in the compressed data
      stream (such as Pixel Representation), then the DICOM Data Element
      should be considered to describe what has been compressed (e.g.,
      the pixel data really is to be interpreted as signed if Pixel
      Representation so specifies).

   5. DICOM Data Elements should not describe characteristics that are
      beyond the capability of the compression scheme used. For example,
      JPEG lossy processes are limited to 12 bits, hence the value of
      Bits Stored should be 12 or less. Bits Allocated is irrelevant,
      and is likely to be constrained by the Information Object
      Definition in to values of 8 or 16. Also, JPEG compressed data
      streams are always color-by-pixel and should be specified as such
      (a decoder can essentially ignore this element however as the
      value for JPEG compressed data is already known).

   6. If JPEG Compressed Pixel Data is decompressed and re-encoded in
      Native (uncompressed) form, then the Data Elements that are
      related to the Pixel Data encoding are updated accordingly. If
      color components are converted from YBR_FULL_422 to RGB during
      decompression and Native re-encoding, the Photometric
      Interpretation will be changed to RGB in the Data Set with the
      Native encoding.

.. _sect_8.2.2:

Run Length Encoding Image Compression
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

DICOM provides a mechanism for supporting the use of Run Length Encoding
(RLE) Image Compression, which is a byte oriented lossless compression
scheme through the encapsulated Format (see of this Standard).
`Encapsulated RLE Compressed Images (Normative) <#chapter_G>`__ defines
RLE Image Compression and its Transfer Syntax.

.. note::

   The RLE Image Compression algorithm described in `Encapsulated RLE
   Compressed Images (Normative) <#chapter_G>`__ is the compression used
   in the TIFF 6.0 specification known as the "PackBits" scheme.

The use of the DICOM Encapsulated Format to support RLE Compressed Pixel
Data requires that the Data Elements that are related to the Pixel Data
encoding (e.g., Photometric Interpretation, Samples per Pixel, Planar
Configuration, Bits Allocated, Bits Stored, High Bit, Pixel
Representation, Rows, Columns, etc.) shall contain values that are
consistent with the compressed data.

The requirements when using a Standard Photometric Interpretation (i.e.,
a Defined Term from PS.3. C.7.6.3.1.2) are specified in
`table_title <#table_8.2.2-1>`__. No other Standard Photometric
Interpretation values shall be used.

.. table:: Valid Values of Pixel Data Related Attributes for RLE
Compression using Standard Photometric Interpretations

   +---------+---------+---------+---------+---------+---------+---------+
   | Phot    | Samples | Planar  | Pixel   | Bits    | Bits    | High    |
   | ometric | per     | Config  | Represe | Al      | Stored  | Bit     |
   | Interpr | Pixel   | uration | ntation | located |         |         |
   | etation |         |         |         |         |         |         |
   +=========+=========+=========+=========+=========+=========+=========+
   | MONO    | 1       | absent  | 0 or 1  | 8 or 16 | 1-16    | 0-15    |
   | CHROME1 |         |         |         |         |         |         |
   |         |         |         |         |         |         |         |
   | MONO    |         |         |         |         |         |         |
   | CHROME2 |         |         |         |         |         |         |
   +---------+---------+---------+---------+---------+---------+---------+
   | PALETTE | 1       | absent  | 0       | 8 or 16 | 1-16    | 0-15    |
   | COLOR   |         |         |         |         |         |         |
   +---------+---------+---------+---------+---------+---------+---------+
   | Y       | 3       | 0 or 1  | 0       | 8       | 1-8     | 0-7     |
   | BR_FULL |         |         |         |         |         |         |
   +---------+---------+---------+---------+---------+---------+---------+
   | RGB     | 3       | 0 or 1  | 0       | 8 or 16 | 1-16    | 0-15    |
   +---------+---------+---------+---------+---------+---------+---------+

.. note::

   1. These requirements were formerly specified in terms of the
      "uncompressed pixel data from which the compressed data was
      derived". However, since the form of the "original" uncompressed
      data stream could vary between different implementations, this
      requirement is now specified in terms of consistency with what is
      encapsulated.

   2. Those characteristics not implied by the definition of the
      compression scheme (e.g., always color-by-plane in RLE), can
      therefore be determined from the DICOM Data Element in the
      enclosing Data Set. For example a Photometric Interpretation of
      "YBR_FULL" would describe the color space that is commonly used to
      losslessly compress images using RLE. It is unusual to use an RGB
      color space for RLE compression, since no advantage is taken of
      correlation between the red, green and blue components (e.g., of
      luminance), and poor compression is achieved (note however that
      the conversion from RGB to YBR_FULL is itself lossy. A new
      photometric interpretation may be proposed in the future that
      allows lossless conversion from RGB and also results in better RLE
      compression ratios).

   3. DICOM Data Elements should not describe characteristics that are
      beyond the capability of the compression scheme used. For example,
      RLE compressed data streams (using the algorithm mandated in the
      DICOM Standard) are always color-by-plane.

   4. If RLE Compressed Pixel Data is decompressed and re-encoded in
      Native (uncompressed) form, then the Data Elements that are
      related to the Pixel Data encoding are updated accordingly. If
      color components are converted from YBR_FULL to RGB during
      decompression and Native re-encoding, the Photometric
      Interpretation will be changed to RGB in the Data Set with the
      Native encoding. It is permitted, however, to leave the YBR_FULL
      color components unconverted but decompressed in the Native
      format, in which case the Photometric Interpretation in the Data
      Set with the Native encoding would be YBR_FULL.

.. _sect_8.2.3:

JPEG-LS Image Compression
~~~~~~~~~~~~~~~~~~~~~~~~~

DICOM provides a mechanism for supporting the use of JPEG-LS Image
Compression through the Encapsulated Format (see ). `Transfer Syntax
Specifications (Normative) <#chapter_A>`__ defines a number of Transfer
Syntaxes that reference the JPEG-LS Standard and provide a number of
lossless (bit preserving) and lossy (near-lossless) compression schemes.

.. note::

   The context where the usage of lossy (near-lossless) compression of
   medical images is clinically acceptable is beyond the scope of the
   DICOM Standard. The policies associated with the selection of
   appropriate compression parameters (e.g., compression ratio) for
   JPEG-LS lossy (near-lossless) compression is also beyond the scope of
   this Standard.

The use of the DICOM Encapsulated Format to support JPEG-LS Compressed
Pixel Data requires that the Data Elements that are related to the Pixel
Data encoding (e.g., Photometric Interpretation, Samples per Pixel,
Planar Configuration, Bits Allocated, Bits Stored, High Bit, Pixel
Representation, Rows, Columns, etc.) shall contain values that are
consistent with the characteristics of the compressed data stream. The
Pixel Data characteristics included in the JPEG-LS Interchange Format
shall be used to decode the compressed data stream.

The requirements when using a Standard Photometric Interpretation (i.e.,
a Defined Term from PS.3. C.7.6.3.1.2) are specified in
`table_title <#table_8.2.3-1>`__. No other Standard Photometric
Interpretation values shall be used.

.. table:: Valid Values of Pixel Data Related Attributes for JPEG-LS
Compression using Standard Photometric Interpretations

   +-------+-------+-------+-------+-------+-------+-------+-------+-------+
   | P     | Tra   | Tra   | Sa    | P     | Pixel | Bits  | Bits  | High  |
   | hotom | nsfer | nsfer | mples | lanar | Repr  | Allo  | S     | Bit   |
   | etric | S     | S     | per   | Con   | esent | cated | tored |       |
   | Inte  | yntax | yntax | Pixel | figur | ation |       |       |       |
   | rpret |       | UID   |       | ation |       |       |       |       |
   | ation |       |       |       |       |       |       |       |       |
   +=======+=======+=======+=======+=======+=======+=======+=======+=======+
   | M     | JP    | 1.2.  | 1     | a     | 0 or  | 8 or  | 2-16  | 1-15  |
   | ONOCH | EG-LS | 840.1 |       | bsent | 1     | 16    |       |       |
   | ROME1 | Los   | 0008. |       |       |       |       |       |       |
   |       | sless | 1.2.​ |       |       |       |       |       |       |
   | M     |       | 4.​80 |       |       |       |       |       |       |
   | ONOCH | JP    |       |       |       |       |       |       |       |
   | ROME2 | EG-LS | 1.2.  |       |       |       |       |       |       |
   |       | Lossy | 840.1 |       |       |       |       |       |       |
   |       | (Near | 0008. |       |       |       |       |       |       |
   |       | -Loss | 1.2.​ |       |       |       |       |       |       |
   |       | less) | 4.​81 |       |       |       |       |       |       |
   +-------+-------+-------+-------+-------+-------+-------+-------+-------+
   | PA    | JP    | 1.2.  | 1     | a     | 0     | 8 or  | 2-16  | 1-15  |
   | LETTE | EG-LS | 840.1 |       | bsent |       | 16    |       |       |
   | COLOR | Los   | 0008. |       |       |       |       |       |       |
   |       | sless | 1.2.​ |       |       |       |       |       |       |
   |       |       | 4.​80 |       |       |       |       |       |       |
   +-------+-------+-------+-------+-------+-------+-------+-------+-------+
   | YBR   | JP    | 1.2.  | 3     | 0     | 0     | 8     | 2-8   | 1-7   |
   | _FULL | EG-LS | 840.1 |       |       |       |       |       |       |
   |       | Los   | 0008. |       |       |       |       |       |       |
   |       | sless | 1.2.​ |       |       |       |       |       |       |
   |       |       | 4.​80 |       |       |       |       |       |       |
   |       | JP    |       |       |       |       |       |       |       |
   |       | EG-LS | 1.2.  |       |       |       |       |       |       |
   |       | Lossy | 840.1 |       |       |       |       |       |       |
   |       | (Near | 0008. |       |       |       |       |       |       |
   |       | -Loss | 1.2.​ |       |       |       |       |       |       |
   |       | less) | 4.​81 |       |       |       |       |       |       |
   +-------+-------+-------+-------+-------+-------+-------+-------+-------+
   | RGB   | JP    | 1.2.  | 3     | 0     | 0     | 8 or  | 2-16  | 1-15  |
   |       | EG-LS | 840.1 |       |       |       | 16    |       |       |
   |       | Los   | 0008. |       |       |       |       |       |       |
   |       | sless | 1.2.​ |       |       |       |       |       |       |
   |       |       | 4.​80 |       |       |       |       |       |       |
   |       | JP    |       |       |       |       |       |       |       |
   |       | EG-LS | 1.2.  |       |       |       |       |       |       |
   |       | Lossy | 840.1 |       |       |       |       |       |       |
   |       | (Near | 0008. |       |       |       |       |       |       |
   |       | -Loss | 1.2.​ |       |       |       |       |       |       |
   |       | less) | 4.​81 |       |       |       |       |       |       |
   +-------+-------+-------+-------+-------+-------+-------+-------+-------+

.. note::

   1. See also the notes in `JPEG Image Compression <#sect_8.2.1>`__.

   2. No color transformation Photometric Interpretation specific for
      JPEG-LS is currently defined in DICOM. Annex F of ISO 14495-2
      describes a *"Sample transformation for inverse colour transform"*
      and a marker segment to encode its parameters, but this is not
      known to have been implemented. Common practice is to compress the
      RGB components unconverted, which sacrifices compression
      performance, and send the Photometric Interpretation as RGB.
      Though the YBR_RCT Photometric Interpretation and component
      conversion could theoretically be used, in the absence of DC
      shifting it results in signed values to be encoded, which are not
      supported by JPEG-LS.

   3. If JPEG-LS Compressed Pixel Data is decompressed and re-encoded in
      Native (uncompressed) form, then the Data Elements that are
      related to the Pixel Data encoding are updated accordingly. If
      color components are converted from any other Photometric
      Interpretation to RGB during decompression and Native re-encoding,
      the Photometric Interpretation will be changed to RGB in the Data
      Set with the Native encoding.

   4. The lower limit of 2 on Bits Stored (0028,0101) reflects the
      minimum JPEG-LS sample precision of 2.

The value of Planar Configuration (0028,0006) is irrelevant since the
manner of encoding components is specified in the JPEG-LS bit stream as
component, line or sample interleaved, hence it shall be set to 0.

.. _sect_8.2.4:

JPEG 2000 Image Compression
~~~~~~~~~~~~~~~~~~~~~~~~~~~

DICOM provides a mechanism for supporting the use of JPEG 2000 Image
Compression through the Encapsulated Format (see ). `Transfer Syntax
Specifications (Normative) <#chapter_A>`__ defines a number of Transfer
Syntaxes that reference the JPEG 2000 Standard and provide lossless (bit
preserving) and lossy compression schemes.

.. note::

   The context where the usage of lossy compression of medical images is
   clinically acceptable is beyond the scope of the DICOM Standard. The
   policies associated with the selection of appropriate compression
   parameters (e.g., compression ratio) for JPEG 2000 lossy compression
   are also beyond the scope of this Standard.

The use of the DICOM Encapsulated Format to support JPEG 2000 Compressed
Pixel Data requires that the Data Elements that are related to the Pixel
Data encoding (e.g., Photometric Interpretation, Samples per Pixel,
Planar Configuration, Bits Allocated, Bits Stored, High Bit, Pixel
Representation, Rows, Columns, etc.) shall contain values that are
consistent with the characteristics of the compressed data stream. The
Pixel Data characteristics included in the JPEG 2000 bit stream shall be
used to decode the compressed data stream.

The requirements when using a Standard Photometric Interpretation (i.e.,
a Defined Term from PS.3. C.7.6.3.1.2) are specified in
`table_title <#table_8.2.4-1>`__. No other Standard Photometric
Interpretation values shall be used.

.. table:: Valid Values of Pixel Data Related Attributes for JPEG 2000
Transfer Syntaxes using Standard Photometric Interpretations

   +-------+-------+-------+-------+-------+-------+-------+-------+-------+
   | P     | Tra   | Tra   | Sa    | P     | Pixel | Bits  | Bits  | High  |
   | hotom | nsfer | nsfer | mples | lanar | Repr  | Allo  | S     | Bit   |
   | etric | S     | S     | per   | Con   | esent | cated | tored |       |
   | Inte  | yntax | yntax | Pixel | figur | ation |       |       |       |
   | rpret |       | UID   |       | ation |       |       |       |       |
   | ation |       |       |       |       |       |       |       |       |
   +=======+=======+=======+=======+=======+=======+=======+=======+=======+
   | M     | JPEG  | 1.2.  | 1     | a     | 0 or  | 8,    | 1-38  | 0-37  |
   | ONOCH | 2000  | 840.1 |       | bsent | 1     | 16,   |       |       |
   | ROME1 | (Los  | 0008. |       |       |       | 24,   |       |       |
   |       | sless | 1.2.​ |       |       |       | 32 or |       |       |
   | M     | Only) | 4.​90 |       |       |       | 40    |       |       |
   | ONOCH |       |       |       |       |       |       |       |       |
   | ROME2 | JPEG  | 1.2.  |       |       |       |       |       |       |
   |       | 2000  | 840.1 |       |       |       |       |       |       |
   |       |       | 0008. |       |       |       |       |       |       |
   |       |       | 1.2.​ |       |       |       |       |       |       |
   |       |       | 4.​91 |       |       |       |       |       |       |
   +-------+-------+-------+-------+-------+-------+-------+-------+-------+
   | PA    | JPEG  | 1.2.  | 1     | a     | 0     | 8 or  | 1-16  | 0-15  |
   | LETTE | 2000  | 840.1 |       | bsent |       | 16    |       |       |
   | COLOR | (Los  | 0008. |       |       |       |       |       |       |
   |       | sless | 1.2.​ |       |       |       |       |       |       |
   |       | Only) | 4.​90 |       |       |       |       |       |       |
   +-------+-------+-------+-------+-------+-------+-------+-------+-------+
   | YB    | JPEG  | 1.2.  | 3     | 0     | 0     | 8,    | 1-38  | 0-37  |
   | R_RCT | 2000  | 840.1 |       |       |       | 16,   |       |       |
   |       | (Los  | 0008. |       |       |       | 24,   |       |       |
   |       | sless | 1.2.​ |       |       |       | 32 or |       |       |
   |       | Only) | 4.​90 |       |       |       | 40    |       |       |
   |       |       |       |       |       |       |       |       |       |
   |       | JPEG  | 1.2.  |       |       |       |       |       |       |
   |       | 2000  | 840.1 |       |       |       |       |       |       |
   |       |       | 0008. |       |       |       |       |       |       |
   |       |       | 1.2.​ |       |       |       |       |       |       |
   |       |       | 4.​91 |       |       |       |       |       |       |
   +-------+-------+-------+-------+-------+-------+-------+-------+-------+
   | YB    | JPEG  | 1.    | 3     | 0     | 0     | 8,    | 1-38  | 0-37  |
   | R_ICT | 2000  | 2.840 |       |       |       | 16,   |       |       |
   |       |       | .1000 |       |       |       | 24,   |       |       |
   |       |       | 8.1.2 |       |       |       | 32 or |       |       |
   |       |       | .4.91 |       |       |       | 40    |       |       |
   +-------+-------+-------+-------+-------+-------+-------+-------+-------+
   | RGB   | JPEG  | 1.2.  | 3     | 0     | 0     | 8,    | 1-38  | 0-37  |
   |       | 2000  | 840.1 |       |       |       | 16,   |       |       |
   |       | (Los  | 0008. |       |       |       | 24,   |       |       |
   |       | sless | 1.2.​ |       |       |       | 32 or |       |       |
   |       | Only) | 4.​90 |       |       |       | 40    |       |       |
   |       |       |       |       |       |       |       |       |       |
   |       | JPEG  | 1.2.  |       |       |       |       |       |       |
   |       | 2000  | 840.1 |       |       |       |       |       |       |
   |       |       | 0008. |       |       |       |       |       |       |
   |       |       | 1.2.​ |       |       |       |       |       |       |
   |       |       | 4.​91 |       |       |       |       |       |       |
   +-------+-------+-------+-------+-------+-------+-------+-------+-------+
   | YBR   | JPEG  | 1.2.  | 3     | 0     | 0     | 8,    | 1-38  | 0-37  |
   | _FULL | 2000  | 840.1 |       |       |       | 16,   |       |       |
   |       | (Los  | 0008. |       |       |       | 24,   |       |       |
   |       | sless | 1.2.​ |       |       |       | 32 or |       |       |
   |       | Only) | 4.​90 |       |       |       | 40    |       |       |
   |       |       |       |       |       |       |       |       |       |
   |       | JPEG  | 1.2.  |       |       |       |       |       |       |
   |       | 2000  | 840.1 |       |       |       |       |       |       |
   |       |       | 0008. |       |       |       |       |       |       |
   |       |       | 1.2.​ |       |       |       |       |       |       |
   |       |       | 4.​91 |       |       |       |       |       |       |
   +-------+-------+-------+-------+-------+-------+-------+-------+-------+

.. note::

   These requirements are specified in terms of consistency with what is
   encapsulated, rather than in terms of the uncompressed pixel data
   from which the compressed data stream may have been derived.

When decompressing, should the characteristics explicitly specified in
the compressed data stream be inconsistent with those specified in the
DICOM Data Elements, those explicitly specified in the compressed data
stream should be used to control the decompression. The DICOM data
elements, if inconsistent, can be regarded as suggestions as to the form
in which an uncompressed Data Set might be encoded, subject to the
general and IOD-specific rules for uncompressed Photometric
Interpretation and Planar Configuration, which may require that
decompressed data be converted to one of the permitted forms.

The JPEG 2000 bit stream specifies whether or not a reversible or
irreversible multi-component (color) transformation [ISO 15444-1 Annex
G], if any, has been applied. If no multi-component transformation has
been applied, then the components shall correspond to those specified by
the DICOM Attribute Photometric Interpretation (0028,0004). If the JPEG
2000 Part 1 reversible multi-component transformation has been applied
then the DICOM Attribute Photometric Interpretation (0028,0004) shall be
YBR_RCT. If the JPEG 2000 Part 1 irreversible multi-component
transformation has been applied then the DICOM Attribute Photometric
Interpretation (0028,0004) shall be YBR_ICT.

.. note::

   1. For example, single component may be present, and the Photometric
      Interpretation (0028,0004) may be MONOCHROME2.

   2. The application of a JPEG 2000 Part 1 reversible multi-component
      transformation is signaled in the JPEG 2000 bit stream by a value
      of 1 rather than 0 in the SGcod Multiple component transformation
      type of the COD marker segment [ISO 15444-1 Table A.17]. No other
      value of Photometric Interpretation than YBR_RCT or YBR_ICT is
      permitted when SGcod Multiple component transformation type is 1.

   3. Though it would be unusual, would not take advantage of
      correlation between the red, green and blue components, and would
      not achieve effective compression, a Photometric Interpretation of
      RGB could be specified as long as no multi-component
      transformation [ISO 15444-1 Annex G] was specified by the JPEG
      2000 bit stream. For some applications the use of RGB is
      permitted, e.g., Whole Slide Microscopy Images, to allow
      conversion to DICOM from proprietary formats without loss due to
      color space transformation. Alternative methods of decorrelation
      of the color components than those specified in [ISO 15444-1 Annex
      G] are permitted as defined in PS3.3, such as a Photometric
      Interpretation of YBR_FULL; this may be useful when converting
      existing YBR_FULL Pixel Data (e.g., in a different Transfer
      Syntax) without further loss.

      In either case (Photometric Interpretation of RGB or YBR_FULL),
      the value of SGcod Multiple component transformation type would be
      0.

      may constrain the values of Photometric Interpretation for
      specific IODs.

   4. Despite the application of a multi-component color transformation
      and its reflection in the Photometric Interpretation attribute,
      the "color space" remains undefined. There is currently no means
      of conveying "standard color spaces" either by fixed values (such
      as sRGB) or by ICC profiles. Note in particular that the JP2 file
      header is not sent in the JPEG 2000 bit stream that is
      encapsulated in DICOM.

   5. If JPEG 2000 Compressed Pixel Data is decompressed and re-encoded
      in Native (uncompressed) form, then the Data Elements that are
      related to the Pixel Data encoding are updated accordingly. If
      color components are converted from YBR_ICT or YBR_RCT to RGB
      during decompression and Native re-encoding, the Photometric
      Interpretation will be changed to RGB in the Data Set with the
      Native encoding.

   6. The upper limit of 40 on Bits Allocated (0028,0100) and 38 on Bits
      Stored (0028,0101) reflects the maximum JPEG 2000 sample precision
      of 38 and the DICOM requirement to describe Bits Allocated
      (0028,0100) as multiples of bytes (octets).

The JPEG 2000 bit stream is capable of encoding both signed and unsigned
pixel values, hence the value of Pixel Representation (0028,0103) may be
either 0 or 1 for monochrome Photometric Interpretations depending on
what has been encoded (as specified in the SIZ marker segment in the
precision and sign of component parameter).

The value of Planar Configuration (0028,0006) is irrelevant since the
manner of encoding components is specified in the JPEG 2000 standard,
hence it shall be set to 0.

.. _sect_8.2.5:

MPEG2 Main Profile / Main Level Video Compression
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

DICOM provides a mechanism for supporting the use of MPEG2 Main Profile
/ Main Level Video Compression through the Encapsulated Format (see ).
`Transfer Syntax Specifications (Normative) <#chapter_A>`__ defines a
Transfer Syntax that references the MPEG2 Main Profile / Main Level
Standard.

.. note::

   MPEG2 compression is inherently lossy. The context where the usage of
   lossy compression of medical images is clinically acceptable is
   beyond the scope of the DICOM Standard. The policies associated with
   the selection of appropriate compression parameters (e.g.,
   compression ratio) for MPEG2 Main Profile / Main Level are also
   beyond the scope of this Standard.

The use of the DICOM Encapsulated Format to support MPEG2 Main Profile /
Main Level compressed pixel data requires that the Data Elements that
are related to the Pixel Data encoding (e.g., Photometric
Interpretation, Samples per Pixel, Planar Configuration, Bits Allocated,
Bits Stored, High Bit, Pixel Representation, Rows, Columns, etc.) shall
contain values that are consistent with the characteristics of the
compressed data stream, with some specific exceptions noted here. The
Pixel Data characteristics included in the MPEG2 Main Profile / Main
Level bit stream shall be used to decode the compressed data stream.

.. note::

   These requirements are specified in terms of consistency with what is
   encapsulated, rather than in terms of the uncompressed pixel data
   from which the compressed data stream may have been derived.

When decompressing, should the characteristics explicitly specified in
the compressed data stream be inconsistent with those specified in the
DICOM Data Elements, those explicitly specified in the compressed data
stream should be used to control the decompression. The DICOM data
elements, if inconsistent, can be regarded as suggestions as to the form
in which an uncompressed Data Set might be encoded, subject to the
general and IOD-specific rules for uncompressed Photometric
Interpretation and Planar Configuration, which may require that
decompressed data be converted to one of the permitted forms.

The MPEG2 Main Profile / Main Level bit stream specifies whether or not
a reversible or irreversible multi-component (color) transformation, if
any, has been applied. If no multi-component transformation has been
applied, then the components shall correspond to those specified by the
DICOM Attribute Photometric Interpretation (0028,0004). MPEG2 Main
Profile / Main Level applies an irreversible multi-component
transformation, so DICOM Attribute Photometric Interpretation
(0028,0004) shall be YBR_PARTIAL_420 in the case of multi-component
data, and MONOCHROME2 in the case of single component data (even though
the MPEG2 bit stream itself is always encoded as three components, one
luminance and two chrominance).

.. note::

   1. If MPEG2 Compressed Pixel Data is decompressed and re-encoded in
      Native (uncompressed) form, then the Data Elements that are
      related to the Pixel Data encoding are updated accordingly. If
      color components are converted from YBR_PARTIAL_420 to RGB during
      decompression and Native re-encoding, the Photometric
      Interpretation will be changed to RGB in the Data Set with the
      Native encoding.

   2. MPEG2 proposes some video formats. Each of the standards specified
      is used in a different market, including: ITU-R BT.470-2 System M
      for SD NTSC and ITU-R BT.470-2 System B/G for SD PAL/SECAM. A PAL
      based system should therefore be based on ITU-BT.470 System B for
      each of Color Primaries, Transfer Characteristic (gamma) and
      matrix coefficients and should take a value of 5 as defined in
      `biblioentry_title <#biblio_ISOIEC13818-2>`__.

The value of Planar Configuration (0028,0006) is irrelevant since the
manner of encoding components is specified in the MPEG2 Main Profile /
Main Level standard, hence it shall be set to 0.

In summary:

-  Samples per Pixel (0028,0002) shall be 3

-  Photometric Interpretation (0028,0004) shall be YBR_PARTIAL_420

-  Bits Allocated (0028,0100) shall be 8

-  Bits Stored (0028,0101) shall be 8

-  High Bit (0028,0102) shall be 7

-  Pixel Representation (0028,0103) shall be 0

-  Planar Configuration (0028,0006) shall be 0

-  Rows (0028,0010), Columns (0028,0011), Cine Rate (0018,0040) and
   Frame Time (0018,1063) or Frame Time Vector (0018,1065) shall be
   consistent with the limitations of Main Profile / Main Level, as
   specified in `table_title <#table_8-1>`__.

.. table:: MPEG2 Main Profile / Main Level Image Transfer Syntax Rows
and Columns Attributes

   +----------+----------+----------+----------+----------+----------+
   | Video    | Spatial  | Frame    | Frame    | Maximum  | Maximum  |
   | Type     | re       | Rate     | Time     | Rows     | Columns  |
   |          | solution |          |          |          |          |
   |          |          | (see     | (see     |          |          |
   |          |          | Note 4)  | Note 5)  |          |          |
   +==========+==========+==========+==========+==========+==========+
   | 525-line | Full     | 30       | 33.33 ms | 480      | 720      |
   | NTSC     |          |          |          |          |          |
   +----------+----------+----------+----------+----------+----------+
   | 625-line | Full     | 25       | 40.0 ms  | 576      | 720      |
   | PAL      |          |          |          |          |          |
   +----------+----------+----------+----------+----------+----------+

.. note::

   1. Although different combinations of values for Rows and Columns
      values are possible while respecting the maximum values listed
      above, it is recommended that the typical 4:3 ratio of image width
      to height be maintained in order to avoid image deformation by
      MPEG2 decoders. A common way to maintain the ratio of width to
      height is to pad the image with black areas on either side.

   2. "Half" definition of pictures (240x352 and 288x352 for NTSC and
      PAL, respectively) are always supported by decoders.

   3. Main Profile / Main Level allows for various different display and
      pixel aspect ratios, including the use of square pixels, and the
      use of non-square pixels with display aspect ratios of 4:3 and
      16:9. DICOM specifies no additional restrictions beyond what is
      provided for in Main Profile / Main Level. All permutations
      allowed by Main Profile / Main Level are valid and are require to
      be supported by all DICOM decoders.

   4. The actual frame rate for NTSC MPEG2 is approximately 29.97
      frames/sec.

   5. The nominal Frame Time is supplied for the purpose of inclusion on
      the DICOM Cine Module Attributes, and should be calculated from
      the actual frame rate.

One fragment shall contain the whole MPEG2 stream.

.. note::

   1. If a video stream exceeds the maximum length of one fragment, it
      may be sent as multiple SOP Instances, but each SOP Instance will
      contain an independent and playable bit stream, and not depend on
      the encoded bit stream in other (previous) instances. The manner
      in which such separate instances are related is not specified in
      the Standard, but mechanisms such as grouping into the same
      Series, and references to earlier instances using Referenced Image
      Sequence may be used.

   2. This constraint limits the length of the compressed bit stream to
      no longer than 2\ :sup:`32`-2 bytes.

The Basic Offset Table shall be empty (present but zero length).

.. note::

   The Basic Offset Table is not used because MPEG2 contains its own
   mechanism for describing navigation of frames. To enable decoding of
   only a part of the sequence, MPEG2 manages a header in any group of
   pictures (GOP) containing a time_code - a 25-bit integer containing
   the following: drop_frame_flag, time_code_hours, time_code_minutes,
   marker_bit, time_code_seconds and time_code_pictures.

The container format for the video bit stream is not constrained. For
example, it may MPEG-2 Transport Stream (MPEG-TS), MPEG-2 Program Stream
(MPEG-PS), MPEG-2 Elementary Stream (MPEG-ES), MPEG-2 Packetized
Elementary Stream (MPEG-PES) (see
`biblioentry_title <#biblio_ISOIEC13818-1>`__) or MPEG-4 (MP4) container
(see `biblioentry_title <#biblio_ISOIEC14496-12>`__ and
`biblioentry_title <#biblio_ISOIEC14496-14>`__).

Any audio components present within the MPEG bit stream shall comply
with the following restrictions:

-  CBR MPEG-1 LAYER III (MP3) Audio Standard

-  up to 24 bits

-  32 kHz, 44.1 kHz or 48 kHz for the main channel (the complementary
   channels can be sampled at the half rate, as defined in the Standard)

-  one main mono or stereo channel, and optionally one or more
   complementary channel(s)

.. note::

   1. MPEG-1 Layer III is standardized in Part 3 of the MPEG-1 standard
      (see `biblioentry_title <#biblio_ISOIEC11172-3>`__).

   2. Although MPEG describes each channel as including up to 5 signals
      (e.g., for surround effects), it is recommended to limit each of
      the two channels to 2 signals each one (stereo).

.. _sect_8.2.6:

MPEG2 Main Profile / High Level Video Compression
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

MPEG2 Main Profile / High Level corresponds to what is commonly known as
HDTV ('High Definition Television'). DICOM provides a mechanism for
supporting the use of MPEG2 Main Profile / High Level Video Compression
through the Encapsulated Format (see ). `Transfer Syntax Specifications
(Normative) <#chapter_A>`__ defines a Transfer Syntax that references
the MPEG2 Main Profile / High Level Standard.

.. note::

   MPEG2 compression is inherently lossy. The context where the usage of
   lossy compression of medical images is clinically acceptable is
   beyond the scope of the DICOM Standard. The policies associated with
   the selection of appropriate compression parameters (e.g.,
   compression ratio) for MPEG2 Main Profile / High Level are also
   beyond the scope of this Standard.

The use of the DICOM Encapsulated Format to support MPEG2 Main Profile /
High Level compressed pixel data requires that the Data Elements that
are related to the Pixel Data encoding (e.g., Photometric
Interpretation, Samples per Pixel, Planar Configuration, Bits Allocated,
Bits Stored, High Bit, Pixel Representation, Rows, Columns, etc.) shall
contain values that are consistent with the characteristics of the
compressed data stream, with some specific exceptions noted here. The
Pixel Data characteristics included in the MPEG2 Main Profile / High
Level bit stream shall be used to decode the compressed data stream.

.. note::

   These requirements are specified in terms of consistency with what is
   encapsulated, rather than in terms of the uncompressed pixel data
   from which the compressed data stream may have been derived.

When decompressing, should the characteristics explicitly specified in
the compressed data stream be inconsistent with those specified in the
DICOM Data Elements, those explicitly specified in the compressed data
stream should be used to control the decompression. The DICOM data
elements, if inconsistent, can be regarded as suggestions as to the form
in which an uncompressed Data Set might be encoded, subject to the
general and IOD-specific rules for uncompressed Photometric
Interpretation and Planar Configuration, which may require that
decompressed data be converted to one of the permitted forms.

.. note::

   If MPEG2 Compressed Pixel Data is decompressed and re-encoded in
   Native (uncompressed) form, then the Data Elements that are related
   to the Pixel Data encoding are updated accordingly. If color
   components are converted from YBR_PARTIAL_420 to RGB during
   decompression and Native re-encoding, the Photometric Interpretation
   will be changed to RGB in the Data Set with the Native encoding.

The requirements are:

-  Planar Configuration (0028,0006) shall be 0

   .. note::

      The value of Planar Configuration (0028,0006) is irrelevant since
      the manner of encoding components is specified in the MPEG2
      standard, hence it is set to 0.

-  Samples per Pixel (0028,0002) shall be 3

-  Photometric Interpretation (0028,0004) shall be YBR_PARTIAL_420 or
   MONOCHROME2

-  Bits Allocated (0028,0100) shall be 8

-  Bits Stored (0028,0101) shall be 8

-  High Bit (0028,0102) shall be 7

-  Pixel Representation (0028,0103) shall be 0

-  Rows (0028,0010) shall be either 720 or 1080

-  Columns (0028,0011) shall be 1280 if Rows is 720, or shall be 1920 if
   Rows is 1080.

-  The value of MPEG2 aspect_ratio_information shall be 0011 in the
   encapsulated MPEG2 data stream corresponding to a 'Display Aspect
   Ratio' (DAR) of 16:9.

-  The DICOM attribute Pixel Aspect Ratio (0028,0034) shall be absent.
   This corresponds to a 'Sampling Aspect Ratio' (SAR) of 1:1.

-  Cine Rate (0018,0040) and Frame Time (0018,1063) or Frame Time Vector
   (0018,1065) shall be consistent with the limitations of Main Profile
   / High Level, as specified in `table_title <#table_8-2>`__.

.. table:: MPEG2 Main Profile / High Level Image Transfer Syntax Frame
Rate Attributes

   +----------------+----------------+----------------+----------------+
   | **Video Type** | **Spatial      | **Frame Rate   | **Frame Time   |
   |                | resolution     | (see Note 2)** | (see Note 3)** |
   |                | layer**        |                |                |
   +================+================+================+================+
   | 30 Hz HD       | Single level,  | 30             | 33.33 ms       |
   |                | Enhancement    |                |                |
   +----------------+----------------+----------------+----------------+
   | 25 Hz HD       | Single level,  | 25             | 40.0 ms        |
   |                | Enhancement    |                |                |
   +----------------+----------------+----------------+----------------+
   | 60 Hz HD       | Single level,  | 60             | 16.67 ms       |
   |                | Enhancement    |                |                |
   +----------------+----------------+----------------+----------------+
   | 50 Hz HD       | Single level,  | 50             | 20.00 ms       |
   |                | Enhancement    |                |                |
   +----------------+----------------+----------------+----------------+

.. note::

   1. The requirements on rows and columns are to maximize
      interoperability between software environments and commonly
      available hardware MPEG2 encoder/decoder implementations. Should
      the source picture have a lower value, it should be re-formatted
      accordingly by scaling and/or pixel padding prior to MPEG2
      encoding.

   2. The frame rate of the acquiring camera for '30 Hz HD' MPEG2 may be
      either 30 or 30/1.001 (approximately 29.97) frames/sec. Similarly,
      the frame rate in the case of 60 Hz may be either 60 or 60/1.001
      (approximately 59.94) frames/sec This may lead to small
      inconsistencies between the video timebase and real time.

   3. The Frame Time (0018,1063) may be calculated from the frame rate
      of the acquiring camera. A frame time of 33.367 ms corresponds to
      29.97 frames per second.

   4. The value of chroma_format for this profile and level is defined
      by MPEG as 4:2:0.

   5. Examples of screen resolutions supported by MPEG2 Main Profile /
      High Level are shown in Table 8-y. Frame rates of 50 Hz and 60 Hz
      (progressive) at the maximum resolution of 1080 by 1920 are not
      supported by Main Profile / High Level. Interlace at the maximum
      resolution is supported at a field rate of 50 Hz or 60 Hz, which
      corresponds to a frame rate of 25 Hz or 30 Hz respectively as
      described in Table 8-y.

   6. An MPEG2 Main Profile / High Level decoder is able to decode bit
      streams conforming to lower levels. These include the 1080 by 1440
      bit streams of MP@H-14, and the Main Level bit streams used in the
      existing MPEG2 Main Profile / Main Level Transfer Syntax in the
      Visible Light IOD.

   7. MP@H-14 is not supported by this Transfer Syntax.

   8. The restriction of DAR to 16:9 is required to ensure
      interoperability because of limitations in commonly available
      hardware chip set implementations for MPEG2 Main Profile / High
      Level.

.. table:: Examples of MPEG2 Main Profile / High Level Screen Resolution

   +----------+-------------+-------------+-------------+-------------+
   | **Rows** | **Columns** | **Frame     | **Video     | **          |
   |          |             | rate**      | Type**      | Progressive |
   |          |             |             |             | or          |
   |          |             |             |             | Interlace** |
   +----------+-------------+-------------+-------------+-------------+
   | 1080     | 1920        | 25          | 25 Hz HD    | P           |
   +----------+-------------+-------------+-------------+-------------+
   | 1080     | 1920        | 29.97, 30   | 30 Hz HD    | P           |
   +----------+-------------+-------------+-------------+-------------+
   | 1080     | 1920        | 25          | 25 Hz HD    | I           |
   +----------+-------------+-------------+-------------+-------------+
   | 1080     | 1920        | 29.97, 30   | 30 Hz HD    | I           |
   +----------+-------------+-------------+-------------+-------------+
   | 720      | 1280        | 25          | 25 Hz HD    | P           |
   +----------+-------------+-------------+-------------+-------------+
   | 720      | 1280        | 29.97, 30,  | 30 Hz HD    | P           |
   +----------+-------------+-------------+-------------+-------------+
   | 720      | 1280        | 50          | 50 Hz HD    | P           |
   +----------+-------------+-------------+-------------+-------------+
   | 720      | 1280        | 59.94, 60   | 60 Hz HD    | P           |
   +----------+-------------+-------------+-------------+-------------+

One fragment shall contain the whole MPEG2 bit stream.

.. note::

   1. If a video stream exceeds the maximum length of one fragment
      (approximately 4 GB), it may be sent as multiple SOP Instances,
      but each SOP Instance will contain an independent and playable bit
      stream, and not depend on the encoded bit stream in other
      (previous) instances. The manner in which such separate instances
      are related is not specified in the Standard, but mechanisms such
      as grouping into the same Series, and references to earlier
      instances using Referenced Image Sequence may be used.

   2. This constraint limits the length of the compressed bit stream to
      no longer than 2\ :sup:`32`-2 bytes.

The Basic Offset Table in the Pixel Data (7FE0,0010) shall be empty
(present but zero length).

.. note::

   The Basic Offset Table is not used because MPEG2 contains its own
   mechanism for describing navigation of frames. To enable decoding of
   only a part of the sequence, MPEG2 manages a header in any group of
   pictures (GOP) containing a time_code - a 25-bit integer containing
   the following: drop_frame_flag, time_code_hours, time_code_minutes,
   marker_bit, time_code_seconds and time_code_pictures.

The container format for the video bit stream is not constrained. For
example, it may MPEG-2 Transport Stream (MPEG-TS), MPEG-2 Program Stream
(MPEG-PS), MPEG-2 Elementary Stream (MPEG-ES), MPEG-2 Packetized
Elementary Stream (MPEG-PES) (see
`biblioentry_title <#biblio_ISOIEC13818-1>`__) or MPEG-4 (MP4) container
(see `biblioentry_title <#biblio_ISOIEC14496-12>`__ and
`biblioentry_title <#biblio_ISOIEC14496-14>`__).

Any audio components present within the MPEG2 Main Profile / High Level
bit stream shall comply with the restrictions as for MPEG2 Main Profile
/ Main Level as stated in `MPEG2 Main Profile / Main Level Video
Compression <#sect_8.2.5>`__.

.. _sect_8.2.7:

MPEG-4 AVC/H.264 High Profile / Level 4.1 Video Compression
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

MPEG-4 AVC/H.264 High Profile / Level 4.1 corresponds to what is
commonly known as HDTV ('High Definition Television'). DICOM provides a
mechanism for supporting the use of MPEG-4 AVC/H.264 Image Compression
through the Encapsulated Format (see ). `Transfer Syntax Specifications
(Normative) <#chapter_A>`__ defines a Transfer Syntax that references
the MPEG-4 AVC/H.264 Standard.

.. note::

   MPEG-4 AVC/H.264 compression / High Profile compression is inherently
   lossy. The context where the usage of lossy compression of medical
   images is clinically acceptable is beyond the scope of the DICOM
   Standard. The policies associated with the selection of appropriate
   compression parameters (e.g., compression ratio) for MPEG-4 AVC/H.264
   High Profile / Level 4.1 are also beyond the scope of this Standard.

The use of the DICOM Encapsulated Format to support MPEG-4 AVC/H.264
compressed pixel data requires that the Data Elements that are related
to the Pixel Data encoding (e.g., Photometric Interpretation, Samples
per Pixel, Planar Configuration, Bits Allocated, Bits Stored, High Bit,
Pixel Representation, Rows, Columns, etc.) shall contain values that are
consistent with the characteristics of the compressed data stream, with
some specific exceptions noted here. The Pixel Data characteristics
included in the MPEG-4 AVC/H.264 bit stream shall be used to decode the
compressed data stream.

.. note::

   These requirements are specified in terms of consistency with what is
   encapsulated, rather than in terms of the uncompressed pixel data
   from which the compressed data stream may have been derived.

When decompressing, should the characteristics explicitly specified in
the compressed data stream be inconsistent with those specified in the
DICOM Data Elements, those explicitly specified in the compressed data
stream should be used to control the decompression. The DICOM data
elements, if inconsistent, can be regarded as suggestions as to the form
in which an uncompressed Data Set might be encoded, subject to the
general and IOD-specific rules for uncompressed Photometric
Interpretation and Planar Configuration, which may require that
decompressed data be converted to one of the permitted forms.

.. note::

   If MPEG-4 Compressed Pixel Data is decompressed and re-encoded in
   Native (uncompressed) form, then the Data Elements that are related
   to the Pixel Data encoding are updated accordingly. If color
   components are converted from YBR_PARTIAL_420 to RGB during
   decompression and Native re-encoding, the Photometric Interpretation
   will be changed to RGB in the Data Set with the Native encoding.

The requirements are:

-  Planar Configuration (0028,0006) shall be 0

-  Samples per Pixel (0028,0002) shall be 3

-  Photometric Interpretation (0028,0004) shall be YBR_PARTIAL_420

-  Bits Allocated (0028,0100) shall be 8

-  Bits Stored (0028,0101) shall be 8

-  High Bit (0028,0102) shall be 7

-  Pixel Representation (0028,0103) shall be 0

-  The value of MPEG-4 AVC/H.264 sample aspect_ratio_idc shall be 1 in
   the encapsulated MPEG-4 AVC/H.264 bit stream if
   aspect_ratio_info_present_flag is 1.

-  Pixel Aspect Ratio (0028,0034) shall be absent. This corresponds to a
   'Sampling Aspect Ratio' (SAR) of 1:1.

-  The possible values for Rows (0028,0010), Columns (0028,0011), Cine
   Rate (0018,0040), and Frame Time (0018,1063) or Frame Time Vector
   (0018,1065) depend on the used Transfer Syntax.

   -  For MPEG-4 AVC/H.264 High Profile / Level 4.1 Transfer Syntax, the
      values for these data elements shall be compliant with the High
      Profile / Level 4.1 of the MPEG-4 AVC/H.264 standard
      (`biblioentry_title <#biblio_ISOIEC14496-10>`__) and restricted to
      a square pixel aspect ratio.

   -  For MPEG-4 AVC/H.264 BD-compatible High Profile / Level 4.1
      Transfer Syntax, the values for these data elements shall be as
      specified in `table_title <#table_8-4>`__.

.. table:: Values Permitted for MPEG-4 AVC/H.264 BD-compatible High
Profile / Level 4.1

   +----------+-------------+-------------+-------------+-------------+
   | **Rows** | **Columns** | **Frame     | **Video     | **          |
   |          |             | rate**      | Type**      | Progressive |
   |          |             |             |             | or          |
   |          |             |             |             | Interlace** |
   +==========+=============+=============+=============+=============+
   | 1080     | 1920        | 25          | 25 Hz HD    | I           |
   +----------+-------------+-------------+-------------+-------------+
   | 1080     | 1920        | 29.97       | 30 Hz HD    | I           |
   +----------+-------------+-------------+-------------+-------------+
   | 1080     | 1920        | 24          | 24 Hz HD    | P           |
   +----------+-------------+-------------+-------------+-------------+
   | 1080     | 1920        | 23.976      | 24 Hz HD    | P           |
   +----------+-------------+-------------+-------------+-------------+
   | 720      | 1280        | 50          | 50 Hz HD    | P           |
   +----------+-------------+-------------+-------------+-------------+
   | 720      | 1280        | 59.94       | 60 Hz HD    | P           |
   +----------+-------------+-------------+-------------+-------------+
   | 720      | 1280        | 24          | 24 Hz HD    | P           |
   +----------+-------------+-------------+-------------+-------------+
   | 720      | 1280        | 23.976      | 24 Hz HD    | P           |
   +----------+-------------+-------------+-------------+-------------+

.. note::

   1. The value of Planar Configuration (0028,0006) is irrelevant since
      the manner of encoding components is specified in the MPEG-4
      AVC/H.264 standard, hence it is set to 0.

   2. The limitation on rows and columns are to maximize
      interoperability between software environments and commonly
      available hardware MPEG-4 AVC/H.264 encoder/decoder
      implementations. Source pictures that have a lower value should be
      re-formatted by scaling and/or pixel padding prior to MPEG-4
      AVC/H.264 encoding.

   3. The frame rate of the acquiring camera for '30 Hz HD' MPEG-4
      AVC/H.264 may be either 30 or 30/1.001 (approximately 29.97)
      frames/sec. Similarly, the frame rate in the case of 60 Hz may be
      either 60 or 60/1.001 (approximately 59.94) frames/sec. This may
      lead to small inconsistencies between the video timebase and real
      time. The relationship between frame rate and frame time is shown
      in Table 8-5.

   4. The Frame Time (0018,1063) may be calculated from the frame rate
      of the acquiring camera. A frame rate of 29.97 frames per second
      corresponds to a frame time of 33.367 ms.

   5. The value of chroma_format for this profile and level is defined
      by MPEG as 4:2:0.

   6. Example screen resolutions supported by MPEG-4 AVC/H.264 High
      Profile / Level 4.1 can be taken from Table 8-4. Frame rates of 50
      Hz and 60 Hz (progressive) at the maximum resolution of 1080 by
      1920 are not supported by MPEG-4 AVC/H.264 High Profile / Level
      4.1. Interlace at the maximum resolution is supported at a field
      rate of 50 Hz or 60 Hz, which corresponds to a frame rate of 25 Hz
      or 30 Hz respectively. Smaller resolutions may be used as long as
      they comply with the square pixel aspect ratio. An example is XGA
      resolution with an image resolution of 768 by 1024 pixels. For
      smaller resolutions there are higher frame rates possible. For
      example it may be up to 80 Hz for XGA.

   7. The display aspect ratio is defined implicitly by the pixel
      resolution of the video picture. Only square pixel aspect ratio is
      allowed. MPEG-4 AVC/H.264 BD-compatible High Profile / Level 4.1
      will only support resolutions that result in a 16:9 display aspect
      ratio

   8. The permitted screen resolutions for the MPEG-4 AVC/H.264
      BD-compatible High Profile / Level 4.1 are listed in Table 8-4.
      Only HD resolutions and no progressive frame rates for 25 or 29.97
      frames per seconds are supported. Frame rates of 50 Hz and 60 Hz
      (progressive) at the maximum resolution of 1080 by 1920 are not
      supported.

.. table:: MPEG-4 AVC/H.264 High Profile / Level 4.1 Image Transfer
Syntax Frame Rate Attributes

   +----------------+----------------+----------------+----------------+
   | **Video Type** | **Spatial      | **Frame Rate   | **Frame Time   |
   |                | resolution     | (see Note 2)** | (see Note 3)** |
   |                | layer**        |                |                |
   +================+================+================+================+
   | 30 Hz HD       | Single level,  | 30             | 33.33 ms       |
   |                | Enhancement    |                |                |
   +----------------+----------------+----------------+----------------+
   | 25 Hz HD       | Single level,  | 25             | 40.0 ms        |
   |                | Enhancement    |                |                |
   +----------------+----------------+----------------+----------------+
   | 60 Hz HD       | Single level,  | 60             | 16.67 ms       |
   |                | Enhancement    |                |                |
   +----------------+----------------+----------------+----------------+
   | 50 Hz HD       | Single level,  | 50             | 20.00 ms       |
   |                | Enhancement    |                |                |
   +----------------+----------------+----------------+----------------+

One fragment shall contain the whole MPEG-4 AVC/H.264 bit stream.

.. note::

   If a video stream exceeds the maximum length of one fragment
   (approximately 4 GB), it may be sent as multiple SOP Instances, but
   each SOP Instance will contain an independent and playable bit
   stream, and not depend on the encoded bit stream in other (previous)
   instances. The manner in which such separate instances are related is
   not specified in the Standard, but mechanisms such as grouping into
   the same Series, and references to earlier instances using Referenced
   Image Sequence may be used.

The container format for the video bit stream shall be MPEG-2 Transport
Stream, a.k.a. MPEG-TS (see
`biblioentry_title <#biblio_ISOIEC13818-1>`__) or MPEG-4, a.k.a. MP4
container (see `biblioentry_title <#biblio_ISOIEC14496-12>`__ and
`biblioentry_title <#biblio_ISOIEC14496-14>`__). The PTS/DTS of the
transport stream shall be used in the MPEG coding.

Any audio components included in the data container shall follow the
constraints detailed in `Constraints for Audio Data Integration in AVC
and HEVC Compressed Bit Streams <#sect_8.2.12>`__.

.. _sect_8.2.8:

MPEG-4 AVC/H.264 High Profile / Level 4.2 Video Compression
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

DICOM provides a mechanism for supporting the use of MPEG-4 AVC/H.264
Image Compression through the Encapsulated Format (see ). `Transfer
Syntax Specifications (Normative) <#chapter_A>`__ defines Transfer
Syntaxes that reference the MPEG-4 AVC/H.264 Standard.

.. note::

   MPEG-4 AVC/H.264 compression / High Profile compression is inherently
   lossy. The context where the usage of lossy compression of medical
   images is clinically acceptable is beyond the scope of the DICOM
   Standard. The policies associated with the selection of appropriate
   compression parameters (e.g., compression ratio) for MPEG-4 AVC/H.264
   High Profile / Level 4.2 are also beyond the scope of this Standard.

The use of the DICOM Encapsulated Format to support MPEG-4 AVC/H.264
compressed pixel data requires that the Data Elements that are related
to the Pixel Data encoding (e.g., Photometric Interpretation, Samples
per Pixel, Planar Configuration, Bits Allocated, Bits Stored, High Bit,
Pixel Representation, Rows, Columns, etc.) shall contain values that are
consistent with the characteristics of the compressed data stream, with
some specific exceptions noted here. The Pixel Data characteristics
included in the MPEG-4 AVC/H.264 bit stream shall be used to decode the
compressed data stream.

.. note::

   These requirements are specified in terms of consistency with what is
   encapsulated, rather than in terms of the uncompressed pixel data
   from which the compressed data stream may have been derived.

When decompressing, should the characteristics explicitly specified in
the compressed data stream be inconsistent with those specified in the
DICOM Data Elements, those explicitly specified in the compressed data
stream should be used to control the decompression. The DICOM data
elements, if inconsistent, can be regarded as suggestions as to the form
in which an uncompressed Data Set might be encoded, subject to the
general and IOD-specific rules for uncompressed Photometric
Interpretation and Planar Configuration, which may require that
decompressed data be converted to one of the permitted forms.

.. note::

   If MPEG-4 Compressed Pixel Data is decompressed and re-encoded in
   Native (uncompressed) form, then the Data Elements that are related
   to the Pixel Data encoding are updated accordingly. If color
   components are converted from YBR_PARTIAL_420 to RGB during
   decompression and Native re-encoding, the Photometric Interpretation
   will be changed to RGB in the Data Set with the Native encoding.

The requirements are:

-  Planar Configuration (0028,0006) shall be 0

-  Samples per Pixel (0028,0002) shall be 3

-  Photometric Interpretation (0028,0004) shall be YBR_PARTIAL_420

-  Bits Allocated (0028,0100) shall be 8

-  Bits Stored (0028,0101) shall be 8

-  High Bit (0028,0102) shall be 7

-  Pixel Representation (0028,0103) shall be 0

-  The value of MPEG-4 AVC/H.264 sample aspect_ratio_idc shall be 1 in
   the encapsulated MPEG-4 AVC/H.264 bit stream if
   aspect_ratio_info_present_flag is 1.

-  Pixel Aspect Ratio (0028,0034) shall be absent. This corresponds to a
   'Sampling Aspect Ratio' (SAR) of 1:1.

-  The values for Rows (0028,0010), Columns (0028,0011), Cine Rate
   (0018,0040), and Frame Time (0018,1063) or Frame Time Vector
   (0018,1065) shall be compliant with the High Profile / Level 4.2 of
   the MPEG-4 AVC/H.264 standard
   (`biblioentry_title <#biblio_ISOIEC14496-10>`__) and restricted to a
   square pixel aspect ratio.

.. note::

   1. The value of Planar Configuration (0028,0006) is irrelevant since
      the manner of encoding components is specified in the MPEG-4
      AVC/H.264 standard, hence it is set to 0.

   2. The frame rate of the acquiring camera for '30 Hz HD' MPEG-4
      AVC/H.264 may be either 30 or 30/1.001 (approximately 29.97)
      frames/sec. Similarly, the frame rate in the case of 60 Hz may be
      either 60 or 60/1.001 (approximately 59.94) frames/sec. This may
      lead to small inconsistencies between the video timebase and real
      time. The relationship between frame rate and frame time is shown
      in `table_title <#table_8-7>`__.

   3. The Frame Time (0018,1063) may be calculated from the frame rate
      of the acquiring camera. A frame rate of 29.97 frames per second
      corresponds to a frame time of 33.367 ms.

   4. The value of chroma_format for this profile and level is defined
      by MPEG as 4:2:0.

.. table:: MPEG-4 AVC/H.264 High Profile / Level 4.2 Image Transfer
Syntax Frame Rate Attributes

   ============== =========================== ===========================
   **Video Type** **Frame Rate (see Note 2)** **Frame Time (see Note 3)**
   ============== =========================== ===========================
   30 Hz HD       30                          33.33 ms
   25 Hz HD       25                          40.0 ms
   60 Hz HD       60                          16.67 ms
   50 Hz HD       50                          20.00 ms
   ============== =========================== ===========================

Stereo Pairs Present (0022,0028) shall be YES if stereoscopic pairs are
present, otherwise shall be NO or absent.

.. table:: MPEG-4 AVC/H.264 High Profile / Level 4.2 Image Transfer
Syntax Stereo Attributes

   +----------------------+----------------------+----------------------+
   | Transfer Syntax      | Stereo Pairs Present | Stereo Frame Packing |
   |                      |                      | Format               |
   +======================+======================+======================+
   | MPEG-4 AVC/H.264     | NO or absent         | absent               |
   | High Profile / Level |                      |                      |
   | 4.2 for 2D Image     |                      |                      |
   | Compression          |                      |                      |
   +----------------------+----------------------+----------------------+
   | MPEG-4 AVC/H.264     | YES                  | present              |
   | High Profile / Level |                      |                      |
   | 4.2 for 3D Image     |                      |                      |
   | Compression          |                      |                      |
   +----------------------+----------------------+----------------------+

One fragment shall contain the whole MPEG-4 AVC/H.264 bit stream.

.. note::

   If a video stream exceeds the maximum length of one fragment
   (approximately 4 GB), it may be sent as multiple SOP Instances, but
   each SOP Instance will contain an independent and playable bit
   stream, and not depend on the encoded bit stream in other (previous)
   instances. The manner in which such separate instances are related is
   not specified in the Standard, but mechanisms such as grouping into
   the same Series, and references to earlier instances using Referenced
   Image Sequence may be used.

The container format for the video bit stream shall be MPEG-2 Transport
Stream, a.k.a. MPEG-TS (see
`biblioentry_title <#biblio_ISOIEC13818-1>`__) or MPEG-4, a.k.a. MP4
container (see `biblioentry_title <#biblio_ISOIEC14496-12>`__ and
`biblioentry_title <#biblio_ISOIEC14496-14>`__). The PTS/DTS of the
transport stream shall be used in the MPEG coding.

Any audio components included in the data container shall follow the
constraints detailed in `Constraints for Audio Data Integration in AVC
and HEVC Compressed Bit Streams <#sect_8.2.12>`__.

.. _sect_8.2.9:

MPEG-4 AVC/H.264 Stereo High Profile / Level 4.2 Video Compression
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

DICOM provides a mechanism for supporting the use of MPEG-4 AVC/H.264
Image Compression through the Encapsulated Format (see ). `Transfer
Syntax Specifications (Normative) <#chapter_A>`__ defines a Transfer
Syntax that references the MPEG-4 AVC/H.264 Standard.

MPEG-4 AVC/H.264 Stereo High Profile can achieve better compression by
additionally making use of prediction between the base and dependent
stereoscopic views. The base view frames make use of intra and inter
prediction as in MPEG-4 AVC/H.264 High Profile. This makes it possible
for decoders which do not know how to decode the stereoscopic data to
decode only the base view. The dependent view is encoded to make use of
redundancy due to prediction based upon similarities between the base
and the dependent views.

MPEG-4 AVC/H.264 Stereo High Profile makes use of the Level table A-1 of
the MPEG-4 specification to set through-put limits. The properties
required by the MPEG-4 AVC/H.264 Stereo High Profile Compression are
identical to the properties defined in `MPEG-4 AVC/H.264 High Profile /
Level 4.2 Video Compression <#sect_8.2.8>`__, except that Stereo Pairs
Present (0022,0028) shall always be YES.

The container format for the video bit stream shall be MPEG-2 Transport
Stream, a.k.a. MPEG-TS (see
`biblioentry_title <#biblio_ISOIEC13818-1>`__) or MPEG-4, a.k.a. MP4
container (see `biblioentry_title <#biblio_ISOIEC14496-12>`__ and
`biblioentry_title <#biblio_ISOIEC14496-14>`__). The PTS/DTS of the
transport stream shall be used in the MPEG coding.

Any audio components included in the data container shall follow the
constraints detailed in `Constraints for Audio Data Integration in AVC
and HEVC Compressed Bit Streams <#sect_8.2.12>`__.

.. _sect_8.2.10:

HEVC/H.265 Main Profile / Level 5.1 Video Compression
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

HEVC/H.265 Main Profile / Level 5.1 Main tier is designed for the
compression of 4:2:0 video formats up to 4k at 60 frames per second with
a bit depth of 8 bits. DICOM provides a mechanism for supporting the use
of HEVC/H.265 Image Compression through the Encapsulated Format (see ).
`Transfer Syntax Specifications (Normative) <#chapter_A>`__ defines a
Transfer Syntax that references the HEVC/H.265 Standard.

The use of the DICOM Encapsulated Format to support HEVC/H.265
compressed pixel data requires that the Data Elements that are related
to the Pixel Data encoding (e.g., Photometric Interpretation, Samples
per Pixel, Planar Configuration, Bits Allocated, Bits Stored, High Bit,
Pixel Representation, Rows, Columns, etc.) shall contain values that are
consistent with the characteristics of the compressed data stream, with
some specific exceptions noted here. The Pixel Data characteristics
included in the HEVC/H.265 bit stream shall be used to decode the
compressed data stream.

.. note::

   1. These requirements are specified in terms of consistency with what
      is encapsulated, rather than in terms of the uncompressed pixel
      data from which the compressed data stream may have been derived.

   2. When decompressing, should the characteristics explicitly
      specified in the compressed data stream be inconsistent with those
      specified in the DICOM Data Elements, those explicitly specified
      in the compressed data stream should be used to control the
      decompression. The DICOM data elements, if inconsistent, can be
      regarded as suggestions as to the form in which an uncompressed
      Data Set might be encoded, subject to the general and IOD-specific
      rules for uncompressed Photometric Interpretation and Planar
      Configuration, which may require that decompressed data be
      converted to one of the permitted forms.

The requirements are:

-  Planar Configuration (0028,0006) shall be 0

-  Samples per Pixel (0028,0002) shall be 3

-  Photometric Interpretation (0028,0004) shall be YBR_PARTIAL_420

-  Bits Allocated (0028,0100) shall be 8

-  Bits Stored (0028,0101) shall be 8

-  High Bit (0028,0102) shall be 7

-  Pixel Representation (0028,0103) shall be 0

-  The value of HEVC/H.265 sample aspect_ratio_idc shall be 1 in the
   encapsulated HEVC/H.265 bit stream if aspect_ratio_info_present_flag
   is 1.

-  Pixel Aspect Ratio (0028,0034) shall be absent. This corresponds to a
   'Sampling Aspect Ratio' (SAR) of 1:1.

-  The values for Rows (0028,0010), Columns (0028,0011), Cine Rate
   (0018,0040) and Frame Time (0018,1063) or Frame Time Vector
   (0018,1065) shall be compliant with the Main Profile / Level 5.1 of
   the HEVC/H.265 standard `biblioentry_title <#biblio_ISOIEC23008-2>`__
   and restricted to a square pixel aspect ratio.

.. note::

   1. The value of Planar Configuration (0028,0006) is irrelevant since
      the manner of encoding components is specified in the HEVC/H.265
      standard, hence it is set to 0.

   2. The limitation on rows and columns are to maximize
      interoperability between software environments and commonly
      available hardware HEVC/H.265 encoder/decoder implementations.
      Source pictures that have a lower value should be re-formatted by
      scaling and/or pixel padding prior to HEVC/H.265 encoding.

   3. The Frame Time (0018,1063) may be calculated from the frame rate
      of the acquiring camera. A frame rate of 29.97 frames per second
      corresponds to a frame time of 33.367 ms.

   4. The value of chroma_format_idc for this profile and level is equal
      to 1, indicating the usage of 4:2:0 content.

The encapsulated pixel data stream may be segmented into more than one
fragment.

.. note::

   The recipient is expected to concatenate the fragments while decoding
   them. This allows for essentially unlimited length streams; the only
   limit imposed is the maximum size of frames (0028,0008) which is
   2^31-1.

The container format for the video bit stream shall be MPEG-2 Transport
Stream, a.k.a. MPEG-TS (see
`biblioentry_title <#biblio_ISOIEC13818-1>`__) or MPEG-4, a.k.a. MP4
container (see `biblioentry_title <#biblio_ISOIEC14496-12>`__ and
`biblioentry_title <#biblio_ISOIEC14496-14>`__). The PTS/DTS of the
transport stream shall be used in the MPEG coding.

Any audio components included in the data container shall follow the
constraints detailed in `Constraints for Audio Data Integration in AVC
and HEVC Compressed Bit Streams <#sect_8.2.12>`__.

.. _sect_8.2.11:

HEVC/H.265 Main 10 Profile / Level 5.1 Video Compression
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

HEVC/H.265 Main 10 Profile / Level 5.1 Main tier is designed for the
compression of 4:2:0 video formats up to 4k at 60 frames per second with
a bit depth of 10 bits. DICOM provides a mechanism for supporting the
use of HEVC/H.265 Image Compression through the Encapsulated Format (see
). `Transfer Syntax Specifications (Normative) <#chapter_A>`__ defines a
Transfer Syntax that references the HEVC/H.265 Standard.

The use of the DICOM Encapsulated Format to support HEVC/H.265
compressed pixel data requires that the Data Elements that are related
to the Pixel Data encoding (e.g., Photometric Interpretation, Samples
per Pixel, Planar Configuration, Bits Allocated, Bits Stored, High Bit,
Pixel Representation, Rows, Columns, etc.) shall contain values that are
consistent with the characteristics of the compressed data stream, with
some specific exceptions noted here. The Pixel Data characteristics
included in the HEVC/H.265 bit stream shall be used to decode the
compressed data stream.

.. note::

   1. These requirements are specified in terms of consistency with what
      is encapsulated, rather than in terms of the uncompressed pixel
      data from which the compressed data stream may have been derived.

   2. When decompressing, should the characteristics explicitly
      specified in the compressed data stream be inconsistent with those
      specified in the DICOM Data Elements, those explicitly specified
      in the compressed data stream should be used to control the
      decompression. The DICOM data elements, if inconsistent, can be
      regarded as suggestions as to the form in which an uncompressed
      Data Set might be encoded, subject to the general and IOD-specific
      rules for uncompressed Photometric Interpretation and Planar
      Configuration, which may require that decompressed data be
      converted to one of the permitted forms.

The requirements are:

-  Planar Configuration (0028,0006) shall be 0

-  Samples per Pixel (0028,0002) shall be 3

-  Photometric Interpretation (0028,0004) shall be YBR_PARTIAL_420

-  Bits Allocated (0028,0100) shall be 16

-  Bits Stored (0028,0101) shall be 10

-  High Bit (0028,0102) shall be 9

-  Pixel Representation (0028,0103) shall be 0

-  The value of HEVC/H.265 sample aspect_ratio_idc shall be 1 in the
   encapsulated HEVC/H.265 bit stream if aspect_ratio_info_present_flag
   is 1.

-  Pixel Aspect Ratio (0028,0034) shall be absent. This corresponds to a
   'Sampling Aspect Ratio' (SAR) of 1:1.

-  The values for Rows (0028,0010) , Columns (0028,0011), Cine Rate
   (0018,0040) , and Frame Time (0018,1063) or Frame Time Vector
   (0018,1065) shall be compliant with the Main 10 Profile / Level 5.1
   of the HEVC/H.265 standard
   `biblioentry_title <#biblio_ISOIEC23008-2>`__ and restricted to a
   square pixel aspect ratio.

.. note::

   1. The value of Planar Configuration (0028,0006) is irrelevant since
      the manner of encoding components is specified in the HEVC/H.265
      standard, hence it is set to 0.

   2. The limitation on rows and columns are to maximize
      interoperability between software environments and commonly
      available hardware HEVC/H.265 encoder/decoder implementations.
      Source pictures that have a lower value should be re-formatted by
      scaling and/or pixel padding prior to HEVC/H.265 encoding.

   3. The Frame Time (0018,1063) may be calculated from the frame rate
      of the acquiring camera. A frame rate of 29.97 frames per second
      corresponds to a frame time of 33.367 ms.

   4. The value of chroma_format_idc for this profile and level is equal
      to 1, indicating the usage of 4:2:0 content.

The encapsulated pixel data stream may be segmented into more than one
fragment.

.. note::

   The recipient is expected to concatenate the fragments while decoding
   them. This allows for essentially unlimited length streams; the only
   limit imposed is the maximum size of frames (0028,0008) which is
   2^31-1.

The container format for the video bit stream shall be MPEG-2 Transport
Stream, a.k.a. MPEG-TS (see
`biblioentry_title <#biblio_ISOIEC13818-1>`__) or MPEG-4, a.k.a. MP4
container (see `biblioentry_title <#biblio_ISOIEC14496-12>`__ and
`biblioentry_title <#biblio_ISOIEC14496-14>`__). The PTS/DTS of the
transport stream shall be used in the MPEG coding.

Any audio components included in the data container shall follow the
constraints detailed in `Constraints for Audio Data Integration in AVC
and HEVC Compressed Bit Streams <#sect_8.2.12>`__.

.. _sect_8.2.12:

Constraints for Audio Data Integration in AVC and HEVC Compressed Bit Streams
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

This section describes the constraints pertaining to the presence of
audio data alongside pixel data in DICOM objects. It affects the
following pixel data encapsulation Transfer Syntaxes:

-  MPEG-4 AVC/H.264 High Profile / Level 4.1

-  MPEG-4 AVC/H.264 BD-compatible High Profile / Level 4.1

-  MPEG-4 AVC/H.264 High Profile / Level 4.2 For 2D Video

-  MPEG-4 AVC/H.264 High Profile / Level 4.2 For 3D Video

-  MPEG-4 AVC/H.264 Stereo High Profile / Level 4.2

-  HEVC/H.265 Main Profile / Level 5.1

-  HEVC/H.265 Main 10 Profile / Level 5.1

Any audio components present within a bit stream whose Transfer Syntax
is among those listed above shall be interleaved in either LPCM, AC-3,
AAC, MP3 or MPEG-1 Layer II audio format and shall comply with the
following restrictions:

.. table:: Allowed Audio Formats

   ===================== ======================= =================
   **Audio Format**      **MPEG-2 TS Container** **MP4 Container**
   ===================== ======================= =================
   LPCM                  Allowed                 -
   AC3                   Allowed                 -
   AAC                   Allowed                 Allowed
   MP3                   Allowed                 Allowed
   MPEG-1 Audio Layer II Allowed                 Allowed
   ===================== ======================= =================

-  LPCM

   -  Maximum bit rate: 4.608 Mbps

   -  Sampling frequency: 48, 96 kHz

   -  Bits per sample: 16, 20 or 24 bits

   -  Number of channels: 2 channels

   .. note::

      If LPCM is used for Audio components, the container format shall
      be MPEG-2 TS.

-  AC-3

   -  Maximum bit rate: 640kbps

   -  Sampling frequency: 48kHz

   -  Bits per sample: 16 bits

   -  Number of channels: 2 or 5.1 channels

   .. note::

      1. AC-3 is standardized in
         `biblioentry_title <#biblio_ETSI_TS_102_366>`__

      2. If AC-3 is used for Audio components, the container format
         shall be MPEG-2 TS.

-  AAC

   -  Maximum bit rate: 640kbps

   -  Sampling frequency: 48kHz

   -  Bits per sample: 16, 20 or 24 bits

   -  Number of channels: 2 or 5.1 channels

   .. note::

      AAC is standardized in Part 7 of the MPEG-2 standard (see
      `biblioentry_title <#biblio_ISOIEC13818-7>`__, and Subpart 4 in
      Part 3 of the MPEG-4 standard (see
      `biblioentry_title <#biblio_ISOIEC14496-3>`__).

-  CBR MPEG-1 LAYER III (MP3) Audio Standard

   -  Maximum bit rate: 320kbps

   -  Sampling frequency: 32 kHz, 44.1 kHz or 48 kHz for the main
      channel (the complementary channels can be sampled at the half
      rate, as defined in the Standard)

   -  Bits per sample: up to 24 bits

   -  Number of channels: one main mono or stereo channel, and
      optionally one or more complementary channel(s)

   .. note::

      1. MPEG-1 Layer III is standardized in Part 3 of the MPEG-1
         standard (see `biblioentry_title <#biblio_ISOIEC11172-3>`__).

      2. Although MPEG describes each channel as including up to 5
         signals (e.g., for surround effects), it is recommended to
         limit each of the two channels to 2 signals each one (stereo).

-  MPEG-1 LAYER II (MP2)

   -  Maximum bit rate: 384kbps

   -  Sampling frequency: 32 kHz, 44.1 kHz or 48 kHz

   -  Bits per sample: up to 24 bits

   -  Number of channels: 2

   .. note::

      MPEG-1 Layer II is standardized in Part 3 of the MPEG-1 standard
      (see `biblioentry_title <#biblio_ISOIEC11172-3>`__).

.. _sect_8.2.13:

Constraints For SMPTE ST 2110-20 Uncompressed Active Video For DICOM-RTV
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

This section describes the constraints applying to pixel data carried in
the DICOM-RTV Flow (separated from DICOM-RTV Metadata Flow) and fully
described in `biblioentry_title <#biblio_SMPTE_ST2110-20>`__ .

The following table describes constraints on the
`biblioentry_title <#biblio_SMPTE_ST2110-20>`__ Video Flow in terms of
the valid values for the corresponding DICOM Attributes in the DICOM-RTV
Metadata Flow:

-  Samples per pixel

-  Bits Allocated

-  Bits Stored

-  High Bit

.. table:: Constraints Applicable to Attributes describing Pixel Data

   +----------------+----------------+----------------+----------------+
   | Samples per    | Bits Allocated | Bits Stored    | High Bit       |
   | Pixel          | (0028,0100)    | (0028,0101)    | (0028,0102)    |
   | (0028,0002)    |                |                |                |
   +================+================+================+================+
   | 3              | 8, 16, 16, 16  | 8, 10, 12, 16  | 7, 9, 11, 15   |
   +----------------+----------------+----------------+----------------+

DICOM Photometric Interpretation is based on CCIR 601 (aka ITU-R
BT.601), therefore some restrictions apply to the possible combination
of Sampling System and Colorimetry parameters as stated by
`biblioentry_title <#biblio_SMPTE_ST2110-20>`__ .

.. table:: List of supported SMPTE ST 2110-20 Parameter Combinations

   +------------------+-------------------------------+-----------------+
   | SMPTE ST 2110-20 | DICOM Photometric             |                 |
   |                  | Interpretation (0028,0004)    |                 |
   +==================+===============================+=================+
   | RGB              | BT601                         | RGB             |
   +------------------+-------------------------------+-----------------+
   | YCbCr-4:4:4      | BT601                         | YBR_FULL        |
   +------------------+-------------------------------+-----------------+
   | YCbCr-4:2:2      | BT601                         | YBR_FULL_422    |
   +------------------+-------------------------------+-----------------+
   | YCbCr-4:2:0      | BT601                         | YBR_PARTIAL_420 |
   +------------------+-------------------------------+-----------------+

Some other `biblioentry_title <#biblio_SMPTE_ST2110-20>`__ parameter
combinations do not correspond to existing DICOM photometric
interpretations, so their use is currently not permitted.
`table_title <#table_8.2.13-3>`__ lists the unsupported combinations.

.. table:: List of unsupported SMPTE ST 2110-20 Parameter Combinations

   ================ =========================================
   SMPTE ST 2110-20 
   ================ =========================================
   RGB              BT2020, BT709, BT2100, ST2065-1, ST2065-3
   YCbCr-4:4:4      BT2020, BT709, BT2100
   YCbCr-4:2:2      BT2020, BT709, BT2100
   YCbCr-4:2:0      BT2020, BT709, BT2100
   CLYCbCr-4:4:4    BT2020
   CLYCbCr-4:2:2    BT2020
   CLYCbCr-4:2:0    BT2020
   ICtCp-4:4:4      BT2100
   ICtCp-4:2:2      BT2100
   XYZ              XYZ
   KEY              
   ================ =========================================

.. _sect_8.3:

Waveform Data and Related Data Elements
---------------------------------------

The DICOM protocol provides for the exchange of encoded time-based
signals, or waveforms, encoded in the Waveform Data 5400,1010).

.. note::

   Per `Repeating Groups <#sect_7.6>`__, an IOD supporting multiple sets
   of Waveform Data will encapsulate Waveform Data (5400,1010) within a
   Sequence.

Encoded Waveform Data of various bit depths is accommodated through the
Waveform Bits Allocated (5400,1004) Data Element. This element defines
the size of each waveform data sample within the Waveform Data
(5400,1010). Allowed values are 8, 16, 32 and 64 bits.

The Value Representation of the Waveform Data (5400,1010) shall be OW;
OB shall be used in cases where Waveform Bits Allocated has a value of
8, but only with Transfer Syntaxes where the Value Representation is
explicitly conveyed.

.. note::

   1. Under the Default Transfer Syntax, OB and OW VRs have the
      identical byte transfer order.

   2. Conversion of a SOP Instance from the Default Transfer Syntax to
      an Explicit VR Transfer Syntax (uncompressed) requires the
      interpretation of the Waveform Bits Allocated (5400,1004) Data
      Element, to determine the proper VR of the Waveform Data.

The following data elements related to Waveform Data shall be encoded
with the same VR as Waveform Data: Channel Minimum Value (5400,0110),
Channel Maximum Value (5400,0112) and Waveform Padding Value
(5400,100A).

.. _sect_8.4:

Pixel Data Provider Service
---------------------------

Specific Transfer Syntaxes allow for the pixel data of the message to be
replaced with a reference to a pixel data provider service. The pixel
data provider service that is referenced supplies the pixel data using a
network protocol that is defined outside DICOM.

.. note::

   The Pixel Data Provider Service is not applicable to Pixel Data
   encoded as Float Pixel Data (7FE0,0008) or Double Float Pixel Data
   (7FE0,0009).

.. _sect_8.4.1:

JPIP Referenced Pixel Data
~~~~~~~~~~~~~~~~~~~~~~~~~~

DICOM provides a mechanism for supporting the use of JPEG 2000
Interactive Protocol through the inclusion of a URL reference to a pixel
data provider service. `Transfer Syntax Specifications
(Normative) <#chapter_A>`__ defines two Transfer Syntaxes that utilize
URL references to a JPIP pixel data provider service.

The use of the these Transfer Syntaxes requires that the Pixel Data
Provider URL specify a URL that will represent the JPIP request
including the specific target information. Additional parameters
required by the application may be appended to the URL when accessing
the pixel data provider.

.. note::

   For example, a JPIP request for a 200 by 200 pixel rendition of the
   entire image can be constructed from the Pixel Data Provider URL as
   follows:

Pixel Data Provider URL (0028,7FE0) =
http://server.xxx/jpipserver.cgi?target=imgxyz.jp2

URL Generated by the application =
http://server.xxx/jpipserver.cgi?target=imgxyz.jp2&fsiz=200,200

The JPIP client shall only request a JPEG 2000 bit stream.

The JPIP server shall return a Content-type of image/jp2,
image/jpp-stream or image/jpt-stream, all of which shall be supported by
the JPIP client.

The Number of Frames (0028,0008) attribute, if present in the Data Set,
identifies the number of frames available for this image. Each frame is
accessible as a separate JPIP code stream. Code streams referenced in
the URL Target shall be sequentially numbered starting with stream 1.

.. note::

   For example, a JPIP request for a 200 by 200 pixel rendition of frame
   17 of a multi-frame image can be constructed from Pixel Data Provider
   URL as follows:

   Pixel Data Provider URL (0028,7FE0) =
   http://server.xxx/multiframeimage.jp2

   URL Generated by the application =
   http://server.xxx/multiframeimage.jp2?fsiz=200,200&stream=17

   A valid stream query parameter value is always less than or equal to
   the value in the Number of Frames (0028,0008).

The syntax of the Pixel Data Provider URL (0028,7FE0) is defined in
`biblioentry_title <#biblio_ISOIEC15444-9>`__ Annex C (Client Request).
That standard respects the URI recommendations
`biblioentry_title <#biblio_RFC_3986>`__. The transport protocol shall
be HTTP or HTTPS.

.. note::

   1. According to `biblioentry_title <#biblio_ISOIEC15444-9>`__, "Each
      JPIP request is directed to a specific representation of a
      specific original named resource or a specific portion of that
      resource. That resource may be a physically stored file or object,
      or may be something that is created virtually by the server upon
      request."

      "The Target request field specifies the original named resource to
      which the request is directed. It is specified using a PATH, which
      could be a simple string or a URI. If the Target field is not
      specified and the request is carried over HTTP, then the JPIP
      request shall be directed to the resource specified through the
      path component of the JPIP request URL."

   2. Transport over UDP or other protocols is not supported.

.. _sect_8.5:

Security Considerations for Encoding of Pixel, Overlay, and Waveform Data (Informative)
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

The encapsulated formats conform to other standards, e.g., JPEG. Many of
these formats have had their own security issues, both with the format
itself and with common implementations for processing the format.

Implementations that support encapsulated format encoding may need to:

-  Perform input validation and sanitation to detect and perhaps remove
   invalid or malicious content.

-  Perform output validation to ensure safe compliance with format
   specification.

-  Monitor library implementations for vulnerability reports, updates,
   and have a process for managing these updates.

Tracking, notification, and remediation of these security problems will
normally be in the context of the encapsulated format and not in the
context of DICOM. This means those implementing and deploying the
encapsulated format must consider security issues from those other
contexts.

