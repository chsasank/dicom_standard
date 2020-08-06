.. _chapter_A:

Transfer Syntax Specifications (Normative)
==========================================

.. _sect_A.1:

DICOM Implicit VR Little Endian Transfer Syntax
-----------------------------------------------

This Transfer Syntax applies to the encoding of the entire DICOM Data
Set. This implies that when a DICOM Data Set is being encoded with the
DICOM Implicit VR Little Endian Transfer Syntax the following
requirements shall be met:

a. The Data Elements contained in the Data Set structure shall be
   encoded with Implicit VR (without a VR Field) as specified in `Data
   Element Structure with Implicit VR <#sect_7.1.3>`__.

b. The encoding of the overall Data Set structure (Data Element Tags,
   Value Length, and Value) shall be in Little Endian as specified in
   `Little Endian Byte Ordering <#sect_7.3>`__.

c. The encoding of the Data Elements of the Data Set shall be as follows
   according to their Value Representations:

   -  For all Value Representations defined in this Part, except for the
      Value Representations OB and OW, the encoding shall be in Little
      Endian as specified in `Little Endian Byte
      Ordering <#sect_7.3>`__.

   -  For the Value Representations OB, OL, OV and OW, the encoding
      shall meet the following specification depending on the Data
      Element Tag:

      -  Pixel Data (7FE0,0010) has the Value Representation OW and
         shall be encoded in Little Endian.

         .. note::

            1. The OL and OV Value Representations are not used for
               Pixel Data, even if it has a Bits Allocated (0028,0100)
               of 32 or 64, since OL and OV were added to the Standard
               after the encoding of Pixel Data had been established

            2. The 32-bit Value Length Field limits the maximum size of
               the Pixel Data that can be encoded in Implicit VR Little
               Endian Transfer Syntax, since they are sent in a Native
               Format.

      -  Overlay Data (60xx,3000) has the Value Representation OW and
         shall be encoded in Little Endian.

      -  Waveform Data (5400,1010) shall have Value Representation OW
         and shall be encoded in Little Endian.

      -  Red Palette Color Lookup Table Data (0028,1201), Green Palette
         Color Lookup Table Data (0028,1202), Blue Color Palette Lookup
         Table Data (0028,1203) and Alpha Palette Color Lookup Table
         Data (0028,1204) have the Value Representation OW and shall be
         encoded in Little Endian.

         .. note::

            Previous versions of the Standard either did not specify the
            encoding of Red Palette Color Lookup Table Data (0028,1201),
            Green Palette Color Lookup Table Data (0028,1202) and Blue
            Color Palette Lookup Table Data (0028,1203) in this Part,
            but specified a VR of US or SS in PS3.6-1993, or specified
            OW in this Part but a VR of US, SS or OW in PS3.6-1996. The
            actual encoding of the values and their byte order would be
            identical in each case.

   -  Red Palette Color Lookup Table Descriptor (0028,1101), Green
      Palette Color Lookup Table Descriptor (0028,1102) and Blue Palette
      Color Lookup Table Descriptor (0028,1103) have the Value
      Representation SS or US (depending on rules specified in the IOD
      in ), and shall be encoded in Little Endian. The first and third
      values are always interpreted as unsigned, regardless of the Value
      Representation.

   -  Data Elements (0028,1221),(0028,1222),(0028,1223) Segmented Red,
      Green, Blue Palette Color Lookup Table Data have the Value
      Representation OW and shall be encoded in Little Endian.

   -  LUT Data (0028,3006) has the Value Representation US or OW and
      shall be encoded in Little Endian.

      .. note::

         Previous versions of the Standard did not specify the encoding
         of these Data Elements in this Part, but specified a VR of US
         or SS in PS3.6-1998. A VR of OW has been added to support
         explicit VR Transfer Syntaxes. Moreover this element is always
         unsigned, therefore the VR of SS has been removed. The actual
         encoding of the values and their byte order would be identical
         in each case.

   -  LUT Descriptor (0028,3002) has the Value Representation SS or US
      (depending on rules specified in the IOD in ), and shall be
      encoded in Little Endian. The first and third values are always
      interpreted as unsigned, regardless of the Value Representation.

   -  Blending Lookup Table Data (0028,1408) has the Value
      Representation OW and shall be encoded in Little Endian.

   -  Track Point Index List (0066,0129) has the Value Representation OL
      and shall be encoded in Little Endian and is always interpreted as
      unsigned.

.. note::

   1. Encoding of Curve Data (5000,3000) and Audio Sample Data
      (5000,200C) was previously defined but has been retired. See
      PS3.5-2004.

   2. Vertex Point Index List (0066,0025), Edge Point Index List
      (0066,0024), Triangle Point Index List (0066,0023) and Primitive
      Point Index List (0066,0029) were previously defined with a value
      representation of OW and always interpreted as unsigned, but have
      been retired. These have been replaced by corresponding OL data
      elements, which allow values larger than 65535 to index the full
      range of points that can be encoded in Point Coordinates Data
      (0066,0016). See PS3.5-2015c.

This DICOM Implicit VR Little Endian Transfer Syntax shall be identified
by a UID of Value "1.2.840.10008.1.2".

.. _sect_A.2:

DICOM Little Endian Transfer Syntax (Explicit VR)
-------------------------------------------------

This Transfer Syntax applies to the encoding of the entire DICOM Data
Set. This implies that when a DICOM Data Set is being encoded with the
DICOM Little Endian Transfer Syntax the following requirements shall be
met:

a. The Data Elements contained in the Data Set structure shall be
   encoded with Explicit VR (with a VR Field) as specified in `Data
   Element Structure with Explicit VR <#sect_7.1.2>`__.

b. The encoding of the overall Data Set structure (Data Element Tags,
   Value Length, and Value) shall be in Little Endian as specified in
   `Little Endian Byte Ordering <#sect_7.3>`__.

c. The encoding of the Data Elements of the Data Set shall be as follows
   according to their Value Representations:

   -  For all Value Representations defined in this Part, except for the
      Value Representations OB and OW, the encoding shall be in Little
      Endian as specified in `Little Endian Byte
      Ordering <#sect_7.3>`__.

   -  For the Value Representations OB, OL, OV and OW, the encoding
      shall meet the following specification depending on the Data
      Element Tag:

      -  Pixel Data (7FE0,0010)

         -  where Bits Allocated (0028,0100) has a value greater than 8
            shall have Value Representation OW and shall be encoded in
            Little Endian;

         -  where Bits Allocated (0028,0100) has a value less than or
            equal to 8 shall have the Value Representation OB or OW and
            shall be encoded in Little Endian.

         .. note::

            1. The OL and OV Value Representations are not used for
               Pixel Data, even if it has a Bits Allocated (0028,0100)
               of 32 or 64, since OL and OV were added to the Standard
               after the encoding of Pixel Data had been established

            2. The 32-bit Value Length Field limits the maximum size of
               the Pixel Data that can be encoded in Little Endian
               Transfer Syntax (Explicit VR) since they are sent in a
               Native Format.

      -  Overlay Data (60xx,3000)

         -  shall have the Value Representation OB or OW and shall be
            encoded in Little Endian.

            .. note::

               Previous versions of the Standard specified that the
               choice of OB or OW VR was based on whether or not Overlay
               Bits Allocated (60xx,0100) was greater than, or less than
               or equal to, 8. However, since only one bit plane can be
               encoded in each Overlay Data (60xx,3000) Element, no
               value of Overlay Bits Allocated other than 1 makes sense.
               Such a restriction is now present in .

      -  Waveform Data (5400,1010) has the Value Representation
         specified in its Explicit VR Field. The component points shall
         be encoded in Little Endian.

      -  Red Palette Color Lookup Table Data (0028,1201), Green Palette
         Color Lookup Table Data (0028,1202), Blue Color Palette Lookup
         Table Data (0028,1203) and Alpha Palette Color Lookup Table
         Data (0028,1204) have the Value Representation OW and shall be
         encoded in Little Endian.

         .. note::

            Previous versions of the Standard either did not specify the
            encoding of Red Palette Color Lookup Table Data (0028,1201),
            Green Palette Color Lookup Table Data (0028,1202) and Blue
            Color Palette Lookup Table Data (0028,1203) in this Part,
            but specified a VR of US or SS in PS3.6-1993, or specified
            OW in this Part but a VR of US, SS or OW in PS3.6-1996. The
            actual encoding of the values and their byte order would be
            identical in each case, though the explicitly encoded VR
            field would be different. However, an explicit VR of US or
            SS cannot be used to encode a table of 2\ :sup:`16`
            elements, since the Value Length is restricted to 16 bits.

      -  Red Palette Color Lookup Table Descriptor (0028,1101), Green
         Palette Color Lookup Table Descriptor (0028,1102) and Blue
         Palette Color Lookup Table Descriptor (0028,1103) have the
         Value Representation SS or US (depending on rules specified in
         the IOD in ), and shall be encoded in Little Endian. The first
         and third values are always interpreted as unsigned, regardless
         of the Value Representation.

      -  Segmented Red Palette Color Lookup Table Data (0028,1221),
         Segmented Green Palette Color Lookup Table Data (0028,1222) and
         Segmented Blue Palette Color Lookup Table Data (0028,1223) have
         the Value Representation OW and shall be encoded in Little
         Endian.

      -  LUT Data (0028,3006) has the Value Representation US or OW and
         shall be encoded in Little Endian.

         .. note::

            Previous versions of the Standard did not specify the
            encoding of these Data Elements in this Part, but specified
            a VR of US or SS in PS3.6-1998. However, an explicit VR of
            US or SS cannot be used to encode a table of 2\ :sup:`16`
            elements, since the Value Length is restricted to 16 bits.
            Hence a VR of OW has been added. Moreover this element is
            always unsigned, therefore the VR of SS has been removed.
            The actual encoding of the values and their byte order would
            be identical in each case, though the explicitly encoded VR
            field would be different.

      -  LUT Descriptor (0028,3002) has the Value Representation SS or
         US (depending on rules specified in the IOD in ), and shall be
         encoded in Little Endian. The first and third values are always
         interpreted as unsigned, regardless of the Value
         Representation.

      -  Blending Lookup Table Data (0028,1408) has the Value
         Representation OW and shall be encoded in Little Endian.

      -  Track Point Index List (0066,0129) has the Value Representation
         OL and shall be encoded in Little Endian and is always
         interpreted as unsigned.

.. note::

   1. For Data encoded with the Value Representation OB, the Data
      encoding is unaffected by byte ordering.

   2. Encoding of Curve Data (5000,3000) and Audio Sample Data
      (5000,200C) was previously defined but has been retired. See
      PS3.5-2004.

   3. Vertex Point Index List (0066,0025), Edge Point Index List
      (0066,0024), Triangle Point Index List (0066,0023) and Primitive
      Point Index List (0066,0029) were previously defined with a value
      representation of OW and always interpreted as unsigned, but have
      been retired. These have been replaced by corresponding OL data
      elements, which allow values larger than 65535 to index the full
      range of points that can be encoded in Point Coordinates Data
      (0066,0016). See PS3.5-2015c.

This DICOM Explicit VR Little Endian Transfer Syntax shall be identified
by a UID of Value "1.2.840.10008.1.2.1".

.. _sect_A.3:

DICOM Big Endian Transfer Syntax (Explicit VR)
----------------------------------------------

This Transfer Syntax was retired in 2006. For the most recent
description of it, see PS3.5 2016b.

.. _sect_A.4:

Transfer Syntaxes For Encapsulation of Encoded Pixel Data
---------------------------------------------------------

These Transfer Syntaxes apply to the encoding of the entire DICOM Data
Set, even though the image Pixel Data (7FE0,0010) portion of the DICOM
Data Set is the only portion that is encoded by an encapsulated format.
These Transfer Syntaxes shall only be used when Pixel Data (7FE0,0010)
is present in the top level Data Set, and hence shall not be used when
Float Pixel Data (7FE0,0008) or Double Float Pixel Data (7FE0,0009) are
present. This implies that when a DICOM Message is being encoded
according to an encapsulation Transfer Syntax the following requirements
shall be met:

1. The Data Elements contained in the Data Set structure shall be
   encoded with Explicit VR (with a VR Field) as specified in `Data
   Element Structure with Explicit VR <#sect_7.1.2>`__.

2. The encoding of the overall Data Set structure (Data Element Tags,
   Value Length, etc.) shall be in Little Endian as specified in `Little
   Endian Byte Ordering <#sect_7.3>`__.

3. The encoding of the Data Elements of the Data Set shall be as follows
   according to their Value Representations:

   -  For all Value Representations defined in this Part of the DICOM
      Standard, except for the Value Representations OB and OW, the
      encoding shall be in Little Endian as specified in `Little Endian
      Byte Ordering <#sect_7.3>`__.

   -  For the Value Representations OB, OL, OV and OW, the encoding
      shall meet the following specification depending on the Data
      Element Tag:

      -  Pixel Data (7FE0,0010) may be encapsulated or native.

         It shall be encapsulated if present in the top-level Data Set
         (i.e., not nested within a Sequence Data Element).

         .. note::

            The distinction between fixed value length (native) and
            undefined value length (encapsulated) is present so that the
            top level Data Set Pixel Data can be compressed (and hence
            encapsulated), but the Pixel Data within an Icon Image
            Sequence may or may not be compressed.

         If native, it shall have a defined Value Length, and be encoded
         as follows:

         -  where Bits Allocated (0028,0100) has a value greater than 8
            shall have Value Representation OW and shall be encoded in
            Little Endian;

         -  where Bits Allocated (0028,0100) has a value less than or
            equal to 8 shall have the Value Representation OB or OW and
            shall be encoded in Little Endian.

         .. note::

            1. The OL and OV Value Representations are not used for
               Pixel Data, even if it has a Bits Allocated (0028,0100)
               of 32 or 64, since OL and OV were added to the Standard
               after the encoding of Pixel Data had been established

            2. That is, as if the Transfer Syntax were Explicit VR
               Little Endian.

         If encapsulated, it has the Value Representation OB and is an
         octet-stream resulting from one of the encoding processes. It
         contains the encoded pixel data stream fragmented into one or
         more Item(s). This Pixel Data Stream may represent a Single or
         Multi-frame Image. See `table_title <#table_A.4-1>`__ and
         `table_title <#table_A.4-2>`__.

         -  The Length of the Data Element (7FE0,0010) shall be set to
            the Value for Undefined Length (FFFFFFFFH).

         -  Each Data Stream Fragment encoded according to the specific
            encoding process shall be encapsulated as a DICOM Item with
            a specific Data Element Tag of Value (FFFE,E000). The Item
            Tag is followed by a 4 byte Item Length field encoding the
            explicit number of bytes of the Item.

            .. note::

               Whether more than one fragment per frame is permitted or
               not is defined per Transfer Syntax.

         -  All items containing an encoded fragment shall be made of an
            even number of bytes greater or equal to two. The last
            fragment of a frame may be padded, if necessary, to meet the
            sequence item format requirements of the DICOM Standard.

            .. note::

               1. Any necessary padding may be added in the JPEG or
                  JPEG-LS compressed data stream as per ISO 10918-1 and
                  ISO 14495-1 such that the End of Image (EOI) marker
                  ends on an even byte boundary, or may be appended
                  after the EOI marker, depending on the implementation.

               2. ISO 10918-1 and ISO 14495-1 define the ability to add
                  any number of padding bytes FFH before any marker (all
                  of which also begin with FFH). It is strongly
                  recommended that FFH padding bytes not be added before
                  the Start of Image (SOI) marker.

         -  The first Item in the Sequence of Items before the encoded
            Pixel Data Stream shall be a Basic Offset Table item. The
            Basic Offset Table Item Value, however, is not required to
            be present:

            -  When the Item Value is not present, the Item Length shall
               be zero (00000000H) (see `table_title <#table_A.4-1>`__).

            -  When the Item Value is present, the Basic Offset Table
               Item Value shall contain concatenated 32-bit unsigned
               integer values that are byte offsets to the first byte of
               the Item Tag of the first fragment for each frame in the
               Sequence of Items. These offsets are measured from the
               first byte of the first Item Tag following the Basic
               Offset Table item (see `table_title <#table_A.4-2>`__).

               .. note::

                  1. For a Multi-Frame Image containing only one frame
                     or a Single Frame Image, the Basic Offset Table
                     Item Value may be present or not. If present it
                     will contain a single 00000000H value.

                  2. Decoders of encapsulated pixel data, whether Single
                     Frame or Multi-Frame, need to accept both an empty
                     Basic Offset Table (zero length) and a Basic Offset
                     Table filled with 32 bit offset values.

                  3. A Basic Offset Table Item Value is not permitted
                     (i.e., the Item Length of the first Item will be
                     zero) if Extended Offset Table (7FE0,0001) is
                     present.

         -  This Sequence of Items is terminated by a Sequence Delimiter
            Item with the Tag (FFFE,E0DD) and an Item Length Field of
            Value (00000000H) (i.e., no Value Field shall be present).

      -  Overlay Data (60xx,3000)

         -  shall have the Value Representation OB or OW and shall be
            encoded in Little Endian.

      -  Waveform Data (5400,1010) has the Value Representation
         specified in its Explicit VR Field. The component points shall
         be encoded in Little Endian.

      -  Red Palette Color Lookup Table Data (0028,1201), Green Palette
         Color Lookup Table Data (0028,1202), Blue Color Palette Lookup
         Table Data (0028,1203) and Alpha Palette Color Lookup Table
         Data (0028,1204) have the Value Representation OW and shall be
         encoded in Little Endian.

         .. note::

            Previous versions of the Standard either did not specify the
            encoding of Data Elements 0028,1201), (0028,1202),
            (0028,1203) in this Part, but specified a VR of US or SS in
            PS3.6-1993, or specified OW in this Part but a VR of US, SS
            or OW in PS3.6-1996. The actual encoding of the values and
            their byte order would be identical in each case, though the
            explicitly encoded VR field would be different. However, an
            explicit VR of US or SS cannot be used to encode a table of
            2\ :sup:`16` elements, since the Value Length is restricted
            to 16 bits.

      -  Red Palette Color Lookup Table Descriptor (0028,1101), Green
         Palette Color Lookup Table Descriptor (0028,1102) and Blue
         Palette Color Lookup Table Descriptor (0028,1103) have the
         Value Representation SS or US (depending on rules specified in
         the IOD in ), and shall be encoded in Little Endian. The first
         and third values are always interpreted as unsigned, regardless
         of the Value Representation.

      -  Segmented Red Palette Color Lookup Table Data (0028,1221),
         Segmented Green Palette Color Lookup Table Data (0028,1222) and
         Segmented Blue Palette Color Lookup Table Data (0028,1223) have
         the Value Representation OW and shall be encoded in Little
         Endian.

      -  LUT Data (0028,3006) has the Value Representation US or OW and
         shall be encoded in Little Endian.

         .. note::

            Previous versions of the Standard did not specify the
            encoding of these Data Elements in this Part, but specified
            a VR of US or SS in PS3.6-1998. However, an explicit VR of
            US or SS cannot be used to encode a table of 2\ :sup:`16`
            elements, since the Value Length is restricted to 16 bits.
            Hence a VR of OW has been added. Moreover this element is
            always unsigned, therefore the VR of SS has been removed.
            The actual encoding of the values and their byte order would
            be identical in each case, though the explicitly encoded VR
            field would be different.

      -  LUT Descriptor (0028,3002) has the Value Representation SS or
         US (depending on rules specified in the IOD in ), and shall be
         encoded in Little Endian. The first and third values are always
         interpreted as unsigned, regardless of the Value
         Representation.

      -  Blending Lookup Table Data (0028,1408) has the Value
         Representation OW and shall be encoded in Little Endian.

      -  Track Point Index List (0066,0129) has the Value Representation
         OL and shall be encoded in Little Endian and is always
         interpreted as unsigned.

.. note::

   1. For Data encoded with the Value Representation OB, the Data
      encoding is unaffected by byte ordering.

   2. Encoding of Curve Data (5000,3000) and Audio Sample Data
      (5000,200C) was previously defined but has been retired. See
      PS3.5-2004.

   3. Vertex Point Index List (0066,0025), Edge Point Index List
      (0066,0024), Triangle Point Index List (0066,0023) and Primitive
      Point Index List (0066,0029) were previously defined with a value
      representation of OW and always interpreted as unsigned, but have
      been retired. These have been replaced by corresponding OL data
      elements, which allow values larger than 65535 to index the full
      range of points that can be encoded in Point Coordinates Data
      (0066,0016). See PS3.5-2015c.

.. table:: Example for Elements of an Encoded Single-Frame Image Defined
as a Sequence of Three Fragments Without Basic Offset Table Item Value

   +-------+-------+-------+-------+-------+-------+-------+-------+-------+
   | **    | **    | *     | *     |       |       |       |       |       |
   | Pixel | Value | *Data | *Data |       |       |       |       |       |
   | Data  | R     | El    | Elem  |       |       |       |       |       |
   | El    | epres | ement | ent** |       |       |       |       |       |
   | ement | entat | Len   |       |       |       |       |       |       |
   | Tag** | ion** | gth** |       |       |       |       |       |       |
   +=======+=======+=======+=======+=======+=======+=======+=======+=======+
   | (     | OB    | 0000H | FFFF  | **    | **    |       |       |       |
   | 7FE0, |       | Res   | FFFFH | Basic | First |       |       |       |
   | 0010) |       | erved | unde  | O     | Fra   |       |       |       |
   | with  |       |       | fined | ffset | gment |       |       |       |
   | VR of |       |       | l     | Table | (S    |       |       |       |
   | OB    |       |       | ength | with  | ingle |       |       |       |
   |       |       |       |       | NO    | F     |       |       |       |
   |       |       |       |       | Item  | rame) |       |       |       |
   |       |       |       |       | Va    | of    |       |       |       |
   |       |       |       |       | lue** | Pixel |       |       |       |
   |       |       |       |       |       | D     |       |       |       |
   |       |       |       |       |       | ata** |       |       |       |
   +-------+-------+-------+-------+-------+-------+-------+-------+-------+
   | *     | *     | *     | *     | *     |       |       |       |       |
   | *Item | *Item | *Item | *Item | *Item |       |       |       |       |
   | Tag** | Len   | Tag** | Len   | Va    |       |       |       |       |
   |       | gth** |       | gth** | lue** |       |       |       |       |
   +-------+-------+-------+-------+-------+-------+-------+-------+-------+
   | (     | 0000  | (     | 0000  | Compr |       |       |       |       |
   | FFFE, | 0000H | FFFE, | 04C6H | essed |       |       |       |       |
   | E000) |       | E000) |       | Fra   |       |       |       |       |
   |       |       |       |       | gment |       |       |       |       |
   +-------+-------+-------+-------+-------+-------+-------+-------+-------+
   | 4     | 2     | 2     | 4     | 4     | 4     | 4     | 4     | 04C6H |
   | bytes | bytes | bytes | bytes | bytes | bytes | bytes | bytes | bytes |
   +-------+-------+-------+-------+-------+-------+-------+-------+-------+

.. table:: Example for Elements of an Encoded Single-Frame Image Defined
as a Sequence of Three Fragments Without Basic Offset Table Item Value
(continued)

   +-------+-------+-------+-------+-------+-------+-------+-------+
   | *     |       |       |       |       |       |       |       |
   | *Data |       |       |       |       |       |       |       |
   | El    |       |       |       |       |       |       |       |
   | ement |       |       |       |       |       |       |       |
   | C     |       |       |       |       |       |       |       |
   | ontin |       |       |       |       |       |       |       |
   | ued** |       |       |       |       |       |       |       |
   +=======+=======+=======+=======+=======+=======+=======+=======+
   | **S   | **    | **Seq |       |       |       |       |       |
   | econd | Third | uence |       |       |       |       |       |
   | Fra   | Fra   | Deli  |       |       |       |       |       |
   | gment | gment | miter |       |       |       |       |       |
   | (S    | (S    | I     |       |       |       |       |       |
   | ingle | ingle | tem** |       |       |       |       |       |
   | F     | F     |       |       |       |       |       |       |
   | rame) | rame) |       |       |       |       |       |       |
   | of    | of    |       |       |       |       |       |       |
   | Pixel | Pixel |       |       |       |       |       |       |
   | D     | D     |       |       |       |       |       |       |
   | ata** | ata** |       |       |       |       |       |       |
   +-------+-------+-------+-------+-------+-------+-------+-------+
   | *     | *     | *     | *     | *     | *     | **Seq | *     |
   | *Item | *Item | *Item | *Item | *Item | *Item | uence | *Item |
   | Tag** | Len   | Va    | Tag** | Len   | Va    | D     | Len   |
   |       | gth** | lue** |       | gth** | lue** | elim. | gth** |
   |       |       |       |       |       |       | Tag** |       |
   +-------+-------+-------+-------+-------+-------+-------+-------+
   | (     | 0000  | Compr | (     | 0000  | Compr | (     | 0000  |
   | FFFE, | 024AH | essed | FFFE, | 0628H | essed | FFFE, | 0000H |
   | E000) |       | Fra   | E000) |       | Fra   | E0DD) |       |
   |       |       | gment |       |       | gment |       |       |
   +-------+-------+-------+-------+-------+-------+-------+-------+
   | 4     | 4     | 024AH | 4     | 4     | 0628H | 4     | 4     |
   | bytes | bytes | bytes | bytes | bytes | bytes | bytes | bytes |
   +-------+-------+-------+-------+-------+-------+-------+-------+

.. table:: Examples of Elements for an Encoded Two-Frame Image Defined
as a Sequence of Three Fragments with Basic Table Item Values

   +-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+
   | **    | **    | *     | *     |       |       |       |       |       |       |
   | Pixel | Value | *Data | *Data |       |       |       |       |       |       |
   | Data  | R     | El    | Elem  |       |       |       |       |       |       |
   | El    | epres | ement | ent** |       |       |       |       |       |       |
   | ement | entat | Len   |       |       |       |       |       |       |       |
   | Tag** | ion** | gth** |       |       |       |       |       |       |       |
   +=======+=======+=======+=======+=======+=======+=======+=======+=======+=======+
   | (     | OB    | 0000H | FFFF  | **    | **    |       |       |       |       |
   | 7FE0, |       | Res   | FFFFH | Basic | First |       |       |       |       |
   | 0010) |       | erved | unde  | O     | Fra   |       |       |       |       |
   | with  |       |       | fined | ffset | gment |       |       |       |       |
   | VR of |       |       | l     | Table | (     |       |       |       |       |
   | OB    |       |       | ength | with  | Frame |       |       |       |       |
   |       |       |       |       | Item  | 1) of |       |       |       |       |
   |       |       |       |       | Va    | Pixel |       |       |       |       |
   |       |       |       |       | lue** | D     |       |       |       |       |
   |       |       |       |       |       | ata** |       |       |       |       |
   +-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+
   | *     | *     | *     | *     | *     | *     |       |       |       |       |
   | *Item | *Item | *Item | *Item | *Item | *Item |       |       |       |       |
   | Tag** | Len   | Va    | Tag** | Len   | Va    |       |       |       |       |
   |       | gth** | lue** |       | gth** | lue** |       |       |       |       |
   +-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+
   | (     | 0000  | 0000  | (     | 0000  | Compr |       |       |       |       |
   | FFFE, | 0008H | 0000H | FFFE, | 02C8H | essed |       |       |       |       |
   | E000) |       | 0000  | E000) |       | Fra   |       |       |       |       |
   |       |       | 0646H |       |       | gment |       |       |       |       |
   +-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+
   | 4     | 2     | 2     | 4     | 4     | 4     | 0008H | 4     | 4     | 02C8H |
   | bytes | bytes | bytes | bytes | bytes | bytes | bytes | bytes | bytes | bytes |
   +-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+

.. table:: Examples of Elements for an Encoded Two-Frame Image Defined
as a Sequence of Three Fragments with Basic Table Item Values
(continued)

   +-------+-------+-------+-------+-------+-------+-------+-------+
   | *     |       |       |       |       |       |       |       |
   | *Data |       |       |       |       |       |       |       |
   | El    |       |       |       |       |       |       |       |
   | ement |       |       |       |       |       |       |       |
   | C     |       |       |       |       |       |       |       |
   | ontin |       |       |       |       |       |       |       |
   | ued** |       |       |       |       |       |       |       |
   +=======+=======+=======+=======+=======+=======+=======+=======+
   | **S   | **    | **Seq |       |       |       |       |       |
   | econd | Third | uence |       |       |       |       |       |
   | Fra   | Fra   | Deli  |       |       |       |       |       |
   | gment | gment | miter |       |       |       |       |       |
   | (     | (     | I     |       |       |       |       |       |
   | Frame | Frame | tem** |       |       |       |       |       |
   | 1) of | 2) of |       |       |       |       |       |       |
   | Pixel | Pixel |       |       |       |       |       |       |
   | D     | D     |       |       |       |       |       |       |
   | ata** | ata** |       |       |       |       |       |       |
   +-------+-------+-------+-------+-------+-------+-------+-------+
   | *     | *     | *     | *     | *     | *     | **Seq | *     |
   | *Item | *Item | *Item | *Item | *Item | *Item | uence | *Item |
   | Tag** | Len   | Va    | Tag** | Len   | Va    | Deli  | Len   |
   |       | gth** | lue** |       | gth** | lue** | miter | gth** |
   |       |       |       |       |       |       | Tag** |       |
   +-------+-------+-------+-------+-------+-------+-------+-------+
   | (     | 0000  | Compr | (     | 0000  | Compr | (     | 0000  |
   | FFFE, | 036EH | essed | FFFE, | 0BC8H | essed | FFFE, | 0000H |
   | E000) |       | Fra   | E000) |       | Fra   | E0DD) |       |
   |       |       | gment |       |       | gment |       |       |
   +-------+-------+-------+-------+-------+-------+-------+-------+
   | 4     | 4     | 036EH | 4     | 4     | 0BC8H | 4     | 4     |
   | bytes | bytes | bytes | bytes | bytes | bytes | bytes | bytes |
   +-------+-------+-------+-------+-------+-------+-------+-------+

.. _sect_A.4.1:

JPEG Image Compression
~~~~~~~~~~~~~~~~~~~~~~

The International Standards Organization ISO/IEC JTC1 has developed an
International Standard, ISO 10918-1 (JPEG Part 1) and an International
Standard, ISO 10918-2 (JPEG Part 2), known as the JPEG Standard, for
digital compression and coding of continuous-tone still images (see
`Encapsulated Images As Part of A DICOM Message
(Informative) <#chapter_F>`__ for further details).

A DICOM Transfer Syntax for JPEG Image Compression shall be identified
by a UID value, appropriate to its JPEG coding process, chosen from
`table_title <#table_A.4-3>`__.

.. table:: DICOM Transfer Syntax UIDs for JPEG

   +----------------------+----------------------+----------------------+
   | **DICOM Transfer     | **JPEG coding        | **JPEG description** |
   | Syntax UID**         | process**            |                      |
   +======================+======================+======================+
   | 1.                   | 1                    | baseline             |
   | 2.840.10008.1.2.4.50 |                      |                      |
   +----------------------+----------------------+----------------------+
   | 1.                   | 2(8-bit),4(12-bit)   | extended             |
   | 2.840.10008.1.2.4.51 |                      |                      |
   +----------------------+----------------------+----------------------+
   | 1.                   | 14                   | lossless,            |
   | 2.840.10008.1.2.4.57 |                      | non-hierarchical     |
   +----------------------+----------------------+----------------------+
   | 1.                   | 14                   | lossless,            |
   | 2.840.10008.1.2.4.70 |                      | non-hierarchical,    |
   |                      | (Selection Value 1)  | first-order          |
   |                      |                      | prediction           |
   +----------------------+----------------------+----------------------+

.. note::

   1. DICOM identifies, to increase the likelihood of successful
      association, three Transfer Syntaxes for Default JPEG Compression
      Image processes (see `JPEG Image Compression <#sect_8.2.1>`__ and
      `Transfer Syntax <#chapter_10>`__).

   2. Different JPEG processes may use different SOF marker segments.
      E.g., the baseline JPEG process 1 used with the
      1.2.840.10008.1.2.4.50 Transfer Syntax uses the SOF0 marker,
      whereas the extended process 2 used with the
      1.2.840.10008.1.2.4.51 Transfer Syntax uses the SOF1 marker.
      Accordingly, even though both bit streams encode 8 bit images
      using DCT and Huffman coding, the bit streams are not identical.
      Further, the extended process 2 may (but is not required to) use
      more AC and DC tables (up to 4 of each, rather than 2, per ISO
      10918-1 Section F.1.3).

      It is not compliant to send bit streams with the SOF0 marker using
      the 1.2.840.10008.1.2.4.51 Transfer Syntax, but it is recommended
      that receivers of the 1.2.840.10008.1.2.4.51 Transfer Syntax be
      able to decode bit streams with the SOF0 marker (this asymmetry is
      consistent with ISO 10918-2 requirements; see `JPEG Image
      Compression <#sect_A.4.1>`__).

   3. It is recommended that lossy compressed 8 bit images be encoded
      with the 1.2.840.10008.1.2.4.50 Transfer Syntax rather than the
      1.2.840.10008.1.2.4.51 Transfer Syntax, unless the additional
      features of the extended process are required. Support of the
      1.2.840.10008.1.2.4.50 Transfer Syntax is required for 8 bit
      images anyway (as described in `JPEG Image
      Compression <#sect_8.2.1>`__) and to avoid confusion with the use
      of 12 bit images encoded with Process 4 in the
      1.2.840.10008.1.2.4.51 Transfer Syntax (defined as a DICOM Default
      Transfer Syntax for 12 bit images in `Transfer Syntaxes for a
      DICOM Default of Lossy JPEG Compression <#sect_10.3>`__).

If the object allows multi-frame images in the pixel data field, then
each frame shall be encoded separately. Each fragment shall contain
encoded data from a single-frame image.

.. note::

   Though a fragment may not contain encoded data from more than one
   frame, the encoded data from one frame may span multiple fragments.
   See note in `Native or Encapsulated Format Encoding <#sect_8.2>`__.

For all images, including all frames of a multi-frame image, the JPEG
Interchange Format shall be used (the table specification shall be
included).

.. note::

   This refers to the `biblioentry_title <#biblio_ISOIEC10918-1>`__
   "interchange format", not the
   `biblioentry_title <#biblio_ISOIEC10918-5>`__ JPEG File Interchange
   Format (JFIF).

If images with Photometric Interpretation (0028,0004) YBR_FULL_422 or
YBR_PARTIAL_422, are encoded with JPEG coding Process 1 (non
hierarchical with Huffman coding), identified by DICOM Transfer Syntax
UID "1.2.840.10008.1.2.4.50"the minimum compressible unit is YYCBCR,
where Y, CB, and CR are 8 by 8 blocks of pixel values. The data stream
encodes two Y blocks followed by the corresponding CB and CR blocks.

.. _sect_A.4.2:

RLE Image Compression
~~~~~~~~~~~~~~~~~~~~~

`Encapsulated RLE Compressed Images (Normative) <#chapter_G>`__ defines
a RLE Image Compression Transfer Syntax. This transfer Syntax is
identified by the UID value "1.2.840.10008.1.2.5". If the object allows
multi-frame images in the pixel data field, then each frame shall be
encoded separately. Each frame shall be encoded in one and only one
Fragment (see `Native or Encapsulated Format Encoding <#sect_8.2>`__).

.. _sect_A.4.3:

JPEG-LS Image Compression
~~~~~~~~~~~~~~~~~~~~~~~~~

The International Standards Organization ISO/IEC JTC1 has developed an
International Standard, `biblioentry_title <#biblio_ISOIEC14495-1>`__
(JPEG-LS Part 1), for digital compression and coding of continuous-tone
still images (see `Encapsulated Images As Part of A DICOM Message
(Informative) <#chapter_F>`__ for further details).

A DICOM Transfer Syntax for JPEG-LS Image Compression shall be
identified by a UID value, appropriate to its JPEG-LS coding process.

Two Transfer Syntaxes are specified for JPEG-LS:

1. A Transfer Syntax with a UID of "1.2.840.10008.1.2.4.80 ", which
   specifies the use of the lossless mode of JPEG-LS. In this mode the
   absolute error between the source and reconstructed images will be
   zero.

2. A Transfer Syntax with a UID of "1.2.840.10008.1.2.4.81 ", which
   specifies the use of the near-lossless mode of JPEG-LS. In this mode,
   the absolute error between the source and reconstructed images will
   be constrained to a finite value that is conveyed in the compressed
   bit stream. Note that this process can, at the discretion of the
   encoder, be used to compress images with an error constrained to a
   value of zero, resulting in no loss of information.

If the object allows multi-frame images in the pixel data field, then
each frame shall be encoded separately. Each fragment shall contain
encoded data from a single-frame image.

.. note::

   Though a fragment may not contain encoded data from more than one
   frame, the encoded data from one frame may span multiple fragments.
   See note in `Native or Encapsulated Format Encoding <#sect_8.2>`__.

For all images, including all frames of a multi-frame image, the JPEG-LS
Interchange Format shall be used (all parameter specifications shall be
included).

.. _sect_A.4.4:

JPEG 2000 Image Compression
~~~~~~~~~~~~~~~~~~~~~~~~~~~

The International Standards Organization ISO/IEC JTC1 has developed an
International Standard, `biblioentry_title <#biblio_ISOIEC15444-1>`__
(JPEG 2000 Part 1), for digital compression and coding of
continuous-tone still images (see `Encapsulated Images As Part of A
DICOM Message (Informative) <#chapter_F>`__ for further details).

A DICOM Transfer Syntax for JPEG 2000 Image Compression shall be
identified by a UID value, appropriate to the choice of JPEG 2000 coding
process.

Two Transfer Syntaxes are specified for JPEG 2000 Part 1:

1. A Transfer Syntax with a UID of "1.2.840.10008.1.2.4.90 ", which
   specifies the use of the lossless (reversible) mode of JPEG 2000 Part
   1 (`biblioentry_title <#biblio_ISOIEC15444-1>`__) (i.e., the use of a
   reversible wavelet transformation and a reversible color component
   transformation, if applicable, and no quantization).

2. A Transfer Syntax with a UID of "1.2.840.10008.1.2.4.91", which
   specifies the use of either:

   a. the lossless (reversible) mode of JPEG 2000 Part 1
      (`biblioentry_title <#biblio_ISOIEC15444-1>`__) (i.e., the use of
      a reversible wavelet transformation and a reversible color
      component transformation, if applicable, and no quantization or
      code stream truncation), or

   b. the lossy (irreversible) mode of JPEG 2000 Part 1
      (`biblioentry_title <#biblio_ISOIEC15444-1>`__) (i.e., the use of
      an irreversible wavelet transformation and an irreversible color
      component transformation, if applicable, and optionally
      quantization, or the use of a reversible wavelet transformation
      and a reversible color component transformation, if applicable,
      followed by code stream truncation).

   The choice reversible versus irreversible is at the discretion of the
   sender (SCU or FSC/FSU).

   .. note::

      When using the irreversible wavelet transformation and an
      irreversible color component transformation, if applicable, even
      if no quantization is performed, some loss will always occur due
      to the finite precision of the calculation of the wavelet and
      multi-component transformations.

Only the features defined in JPEG 2000 Part 1
(`biblioentry_title <#biblio_ISOIEC15444-1>`__) are permitted for these
two Transfer Syntaxes. Additional features and extensions that may be
defined in other parts of JPEG 2000 shall not be included in the
compressed bit stream unless they can be decoded or ignored without loss
of fidelity by all Part 1 compliant implementations.

If the object allows multi-frame images in the pixel data field, then
for these JPEG 2000 Part 1 Transfer Syntaxes, each frame shall be
encoded separately. Each fragment shall contain encoded data from a
single frame.

.. note::

   1. That is, the processes defined in
      `biblioentry_title <#biblio_ISOIEC15444-1>`__ shall be applied on
      a per-frame basis. The proposal for encapsulation of multiple
      frames in a non-DICOM manner in so-called "Motion-JPEG" or
      "M-JPEG" defined in 15444-3 is not used.

   2. Though a fragment may not contain encoded data from more than one
      frame, the encoded data from one frame may span multiple
      fragments. See note in `Native or Encapsulated Format
      Encoding <#sect_8.2>`__.

For all images, including all frames of a multi-frame image, the JPEG
2000 bit stream specified in
`biblioentry_title <#biblio_ISOIEC15444-1>`__ shall be used. The
optional JP2 file format header shall NOT be included.

.. note::

   The role of the JP2 file format header is fulfilled by the non-pixel
   data attributes in the DICOM Data Set.

The International Standards Organization ISO/IEC JTC1 has also developed
JPEG 2000 Part 2 (`biblioentry_title <#biblio_ISOIEC15444-2>`__), which
includes Extensions to the compression techniques described in Part 1 of
the JPEG 2000 Standard. Annex J of JPEG 2000 Part 2 describes extensions
to the ICT and RCT multiple component transformations allowed in Part 1.
Two types of multiple component transformations are defined in Annex J
of Part 2 of JPEG 2000:

1. Array based multiple component transforms that form linear
   combinations of components to reduce the correlation between
   components. Array based transforms include prediction based
   transformations such as DPCM as well as more complicated
   transformations such as the KLT. These array based transformations
   can be implemented reversibly or irreversibly.

2. Wavelet based multiple component transformations using the same two
   wavelet filters as used in Part 1 of JPEG 2000 (5-3 reversible
   wavelet and 9-7 irreversible wavelet).

Annex J of JPEG 2000 Part 2 also describes a flexible mechanism to allow
these techniques to be applied in sequence. Furthermore, it provides
mechanisms that allow components to be re-ordered and grouped into
component collections. Different multiple component transformation can
then be applied to each component collection.

Two additional Transfer Syntaxes are specified for Part 2 JPEG 2000:

1. A Transfer Syntax with a UID of 1.2.840.10008.1.2.4.92, which
   specifies the use of the lossless (reversible) mode of JPEG 2000 Part
   2 (`biblioentry_title <#biblio_ISOIEC15444-2>`__) multiple component
   transformation extensions, as defined in Annex J of JPEG 2000 Part 2
   (i.e., the use of a reversible wavelet transformation and a
   reversible multiple component transformation, and no quantization or
   code stream truncation).

2. A Transfer Syntax with a UID of 1.2.840.10008.1.2.4.93, which
   specifies the use of either:

   a. the lossless (reversible) mode of JPEG 2000 Part 2
      (`biblioentry_title <#biblio_ISOIEC15444-2>`__) multiple component
      transformation extensions, as defined in Annex J of JPEG 2000 Part
      2 (i.e., the use of a reversible wavelet transformation and a
      reversible multiple component transformation, and no
      quantization), or

   b. the lossy (irreversible) mode of JPEG 2000 Part 2
      (`biblioentry_title <#biblio_ISOIEC15444-2>`__) multiple component
      transformation extensions, as defined in Annex J of JPEG 2000 Part
      2 (i.e., the use of an irreversible wavelet transformation and an
      irreversible multiple component transformation, and optionally
      quantization, or the use of an reversible wavelet transformation
      and a reversible multiple component transformation, followed by
      code stream truncation).

Only the multiple component transformation extensions defined in Annex J
of JPEG 2000 Part 2 (`biblioentry_title <#biblio_ISOIEC15444-2>`__) are
permitted for these two Transfer Syntaxes. Additional features and
extensions that may be defined in other Annexes of JPEG 2000 Part 2
shall not be included in the compressed bit stream.

.. note::

   the arbitrary wavelet transformations, as defined in Annex H of JPEG
   2000 Part 2 (`biblioentry_title <#biblio_ISOIEC15444-2>`__) are not
   allowed for these two Transfer Syntaxes. The only wavelet
   transformations that are allowed to be used as multiple component
   transformations are the reversible 5-3 wavelet transformation and the
   irreversible 9-7 wavelet transformation, as defined in Annex F of
   JPEG 2000 Part 1 (`biblioentry_title <#biblio_ISOIEC15444-1>`__).

If the object allows multi-frame images in the pixel data field, then,
for these JPEG 2000 Part 2 Transfer Syntaxes, the frames in the object
are first processed using the multi-component transformation. After the
multiple component transformation has been applied, the transformed
frames are encoded using the process described in JPEG 2000 Part 1.

Optionally, the frames can be grouped into one or more component
collections. The multiple component transformations are then applied to
each component collection independently. The use of component
collections can be used to reduce computational complexity and to
improve access to specific frames on the decoder. If component
collections are used, each fragment shall contain encoded data from a
single component collection.

.. note::

   1. The 3\ :sup:`rd` dimension transformations that are described in
      this Supplement are treated in Part 2 of JPEG 2000 as direct
      extensions to the color component transformations (RGB to YUV)
      that are described in Part 1 of JPEG 2000. For this reason, each
      image or frame in the sequence is called a "component". Although
      the term component is used as a generic term to identify an
      element of the 3\ :sup:`rd` dimension, no restriction is made or
      implied that the transformations in this Supplement apply only to
      multi-component (or multiple color channel) data. To compress a
      volumetric Data Set using this Transfer Syntax, each frame of the
      DICOM image is treated as a component of a multi-component image.

   2. The progressive nature of the JPEG 2000 code stream allows for the
      decompression of the image before the complete image has been
      transferred. If a Storage SCP truncates the code stream by
      aborting the association, the instance has not been completely
      transferred and hence should not persist unless different UIDs are
      assigned (even though it may have been transiently used for
      display purposes).

   3. It has been shown that the use of component collections does not
      significantly affect the compression efficiency (for details, see
      http://medical.nema.org/Dicom/minutes/WG-04/2004/2004-02-18/3D_compression_RSNA_2003_ver2.pdf).

   4. Though a fragment may not contain encoded data from more than one
      component collection, the encoded data from one component
      collection may span multiple fragments.

.. _sect_A.4.5:

MPEG2 Video Compression
~~~~~~~~~~~~~~~~~~~~~~~

The International Standards Organization ISO/IEC MPEG2 has developed an
International Standard, `biblioentry_title <#biblio_ISOIEC13818-2>`__
'Information Technology - Generic coding of moving pictures and
associated audio information: video -- part 2', referred to as "MPEG-2".

A DICOM Transfer Syntax for MPEG2 Video Compression shall be identified
by a UID value of either:

-  1.2.840.10008.1.2.4.100 corresponding to MPEG2 Main Profile / Main
   Level option of the ISO/IEC MPEG2 Video standard

-  1.2.840.10008.1.2.4.101 corresponding to the MPEG2 Main Profile /
   High Level option of the ISO/IEC MPEG2 Video standard.

.. _sect_A.4.6:

MPEG-4 AVC/H.264 High Profile / Level 4.1 Video Compression
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

The International Standards Organization ISO/IEC MPEG4 has developed an
International Standard, `biblioentry_title <#biblio_ISOIEC14496-10>`__
(MPEG-4 Part 10), for the video compression of generic coding of moving
pictures and associated audio information. This standard is jointly
maintained and has identical technical content as the ITU-T H.264
standard.

A DICOM Transfer Syntax for MPEG-4 AVC/H.264 Video Compression shall be
identified by a UID value of either:

-  1.2.840.10008.1.2.4.102 corresponding to the MPEG-4 AVC/H.264 High
   Profile / Level 4.1 of the ITU-T H.264 Video standard

-  1.2.840.10008.1.2.4.103 corresponding to the MPEG-4 AVC/H.264
   BD-compatible High Profile / Level 4.1 of the ITU-T H.264 Video
   standard with the temporal and spatial resolution restrictions
   defined in `table_title <#table_8-4>`__.

.. _sect_A.4.7:

MPEG-4 AVC/H.264 High Profile / Level 4.2 Video Compression
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

The International Standards Organization ISO/IEC MPEG4 has developed an
International Standard, `biblioentry_title <#biblio_ISOIEC14496-10>`__
(MPEG-4 Part 10), for the video compression of generic coding of moving
pictures and associated audio information. This standard is jointly
maintained and has identical technical content as the ITU-T H.264
standard.

A DICOM Transfer Syntax MPEG-4 AVC/H.264 High Profile / Level 4.2 for 2D
Video Compression shall be identified by a UID value of:

-  1.2.840.10008.1.2.4.104 corresponding to the MPEG-4 AVC/H.264 High
   Profile / Level 4.2 of the ITU-T H.264 Video standard with the
   restriction that frame packing for stereoscopic 3D content shall not
   be used as defined in `table_title <#table_8-8>`__.

A DICOM Transfer Syntax MPEG-4 AVC/H.264 High Profile / Level 4.2 for 3D
Video Compression shall be identified by a UID value of:

-  1.2.840.10008.1.2.4.105 corresponding to the MPEG-4 AVC/H.264 High
   Profile / Level 4.2 of the ITU-T H.264 Video standard. It should be
   used for transmitting stereoscopic 3D content with frame packing
   formats as defined in `table_title <#table_8-8>`__.

.. _sect_A.4.8:

MPEG-4 AVC/H.264 Stereo High Profile / Level 4.2 Video Compression
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

The International Standards Organization ISO/IEC MPEG4 has developed an
International Standard, `biblioentry_title <#biblio_ISOIEC14496-10>`__
(MPEG-4 Part 10), for the video compression of generic coding of moving
pictures and associated audio information. This standard is jointly
maintained and has identical technical content as the ITU-T H.264
standard.

A DICOM Transfer Syntax for MPEG-4 AVC/H.264 Stereo High Profile / Level
4.2 Video Compression shall be identified by a UID value of:

-  1.2.840.10008.1.2.4.106 corresponding to the MPEG-4 AVC/H.264 Stereo
   High Profile / Level 4.2 of the ITU-T H.264 Video standard.

.. _sect_A.4.9:

HEVC/H.265 Main Profile / Level 5.1 Video Compression
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

The International Standards Organization ISO/IEC MPEG has developed an
International Standard, `biblioentry_title <#biblio_ISOIEC23008-2>`__
(HEVC), for the video compression of generic coding of moving pictures
and associated audio information. This standard is jointly maintained
and has identical technical content as the
`biblioentry_title <#biblio_ISOIEC23008-2>`__ HEVC standard.

A DICOM Transfer Syntax for HEVC/H.265 Main Profile / Level 5.1 Video
Compression shall be identified by a UID value of:

-  1.2.840.10008.1.2.4.107 corresponding to the HEVC/H.265 Main Profile
   / Level 5.1 of the `biblioentry_title <#biblio_ISOIEC23008-2>`__ HEVC
   Video standard.

.. _sect_A.4.10:

HEVC/H.265 Main 10 Profile / Level 5.1 Video Compression
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

The International Standards Organization ISO/IEC MPEG has developed an
International Standard, `biblioentry_title <#biblio_ISOIEC23008-2>`__
(HEVC), for the video compression of generic coding of moving pictures
and associated audio information. This standard is jointly maintained
and has identical technical content as the
`biblioentry_title <#biblio_ISOIEC23008-2>`__ HEVC standard.

A DICOM Transfer Syntax for HEVC/H.265 Main 10 Profile / Level 5.1 Video
Compression shall be identified by a UID value of:

-  1.2.840.10008.1.2.4.108 corresponding to the HEVC/H.265 Main 10
   Profile / Level 5.1 of the
   `biblioentry_title <#biblio_ISOIEC23008-2>`__ HEVC Video standard.

.. _sect_A.5:

DICOM Deflated Little Endian Transfer Syntax (Explicit VR)
----------------------------------------------------------

This Transfer Syntax applies to the encoding of the entire DICOM Data
Set.

The entire Data Set is first encoded according to the rules specified in
`DICOM Little Endian Transfer Syntax (Explicit VR) <#sect_A.2>`__.

The entire byte stream is then compressed using the "Deflate" algorithm
defined in Internet RFC 1951.

If the deflate algorithm produces an odd number of bytes then a single
trailing NULL byte shall be added after the last byte of the deflated
bit stream.

.. note::

   1. The Pixel Data in Pixel Data (7FE0,0010), Float Pixel Data
      (7FE0,0008) or Double Float Pixel Data (7FE0,0009) is not handled
      in any special manner. The pixel data is first encoded as
      sequential uncompressed frames without encapsulation, and then is
      handled as part of the byte stream fed to the "deflate" compressor
      in the same manner as the value of any other attribute.

   2. This Transfer Syntax is particularly useful for compression of
      objects without pixel data, such as structured reports. It is not
      particularly effective at image compression, since any benefit
      obtained from compressing the non-pixel data is offset by less
      effective compression of the much larger pixel data.

   3. A freely available reference implementation of the "deflate"
      compressor may be found in the zlib package, which may be
      downloaded from http://www.zlib.net/.

   4. Although the encoded stream may be padded by a trailing NULL byte,
      the end of the deflated bit stream will be indicated by the
      delimiter that will occur before the padding.

In order to facilitate interoperability of implementations conforming to
the DICOM Standard that elect to use this Transfer Syntax, the following
policy is specified:

-  Any implementation that has elected to support the Deflated Explicit
   VR Little Endian Transfer Syntax for any Abstract Syntax, shall also
   support the Explicit VR Little Endian Transfer for that Abstract
   Syntax.

.. note::

   1. This requirement to support the (uncompressed) Explicit VR Little
      Endian Transfer Syntax is in order to ensure full-fidelity
      exchange of VR information in the case that the Association
      Acceptor does not support the Deflated Explicit VR Little Endian
      Transfer Syntax. The requirement specified in `DICOM Default
      Transfer Syntax <#sect_10.1>`__ of this Part, that the Default
      Implicit VR Little Endian Transfer Syntax be supported by all
      implementations except those that only have access to lossy
      compressed pixel data, is not waived. In other words, an
      implementation must support all three Transfer Syntaxes.

   2. There are no such "baseline" requirements on media, since such
      requirements are at the discretion of the Media Application
      Profile. Furthermore, sufficient object "management" information
      should be present in the DICOMDIR even if an individual
      application cannot decompress an instance encoded with the
      deflated Transfer Syntax.

This DICOM Deflated Explicit VR Little Endian Transfer Syntax shall be
identified by a UID of Value "1.2.840.10008.1.2.1.99".

.. _sect_A.6:

DICOM JPIP Referenced Transfer Syntax (Explicit VR)
---------------------------------------------------

This Transfer Syntax applies to the encoding of the entire DICOM Data
Set. This Transfer Syntax shall only be used when Pixel Data (7FE0,0010)
is present in the top level Data Set, and hence shall not be used when
Float Pixel Data (7FE0,0008) or Double Float Pixel Data (7FE0,0009) are
present. This implies that when a DICOM Data Set is being encoded with
the DICOM Little Endian Transfer Syntax the following requirements shall
be met:

a. The Data Elements contained in the Data Set structure shall be
   encoded with Explicit VR (with a VR Field) as specified in `Data
   Element Structure with Explicit VR <#sect_7.1.2>`__.

b. The encoding of the overall Data Set structure (Data Element Tags,
   Value Length, and Value) shall be in Little Endian as specified in
   `Little Endian Byte Ordering <#sect_7.3>`__.

c. The encoding of the Data Elements of the Data Set shall be as follows
   according to their Value Representations:

   -  For all Value Representations defined in this Part, except for the
      Value Representations OB and OW, the encoding shall be in Little
      Endian as specified in `Little Endian Byte
      Ordering <#sect_7.3>`__.

   -  For the Value Representations OB and OW, the encoding shall meet
      the following specification depending on the Data Element Tag:

      -  Pixel Data (7FE0,0010) shall not be present, but rather pixel
         data shall be referenced via Data Element (0028,7FE0) Pixel
         Data Provider URL

      -  Overlay data, if present, shall only be encoded in the Overlay
         Data (60xx,3000) Element, which shall have the Value
         Representation OB or OW and shall be encoded in Little Endian.

      -  Data Element (0028,0004) Photometric Interpretation shall be
         limited to the values: MONOCHROME1, MONOCHROME2, YBR_ICT and
         YBR_RCT.

This DICOM JPIP Referenced Transfer Syntax shall be identified by a UID
of Value "1.2.840.10008.1.2.4.94 ".

.. _sect_A.7:

DICOM JPIP Referenced Deflate Transfer Syntax (Explicit VR)
-----------------------------------------------------------

This Transfer Syntax applies to the encoding of the entire DICOM Data
Set.

The entire Data Set is first encoded according to the rules specified in
`DICOM JPIP Referenced Transfer Syntax (Explicit VR) <#sect_A.6>`__.

The entire byte stream is then compressed using the "Deflate" algorithm
defined in Internet RFC 1951.

This DICOM JPIP Referenced Deflate Transfer Syntax shall be identified
by a UID of Value "1.2.840.10008.1.2.4.95".

.. _sect_A.8:

SMPTE ST 2110-20 Uncompressed Progressive Active Video Transfer Syntax
----------------------------------------------------------------------

This Transfer Syntax is used in a DICOM-RTV Metadata Flow in order to
describe the accompanying
`biblioentry_title <#biblio_SMPTE_ST2110-20>`__ Video Flow.

DICOM Attributes

-  Samples per Pixel (0028,0002)

-  Photometric Interpretation (0028,0004)

-  Bits Allocated (0028,0100)

-  Bits Stored (0028,0101)

-  High Bit (0028,0102)

are still applicable with some accommodations below.

As DICOM Photometric Interpretation (0028,0004) values YBR_FULL,
YBR_FULL_422, YBR_PARTIAL_420 are based on CCIR 601 (aka BT.601),
DICOM-RTV supports only the following:

-  `biblioentry_title <#biblio_SMPTE_ST2110-20>`__ YCbCr-4:4:4 sampling
   system

-  `biblioentry_title <#biblio_SMPTE_ST2110-20>`__ RGB sampling system

-  `biblioentry_title <#biblio_SMPTE_ST2110-20>`__ YCbCr-4:2:2 sampling
   system

-  `biblioentry_title <#biblio_SMPTE_ST2110-20>`__ YCbCr-4:2:0 sampling
   system

`table_title <#table_A.8-1>`__ describes the different color resolution.

.. table:: DICOM Attributes for different color resolution

   +-----------+-------------+-------------+-------------+-------------+
   | Bit Depth | Samples per | Bits        | Bits Stored | High Bit    |
   |           | Pixel       | Allocated   | (0028,0101) | (0028,0102) |
   |           | (0028,0002) | (0028,0100) |             |             |
   +===========+=============+=============+=============+=============+
   | 8         | 3           | 8           | 8           | 7           |
   +-----------+-------------+-------------+-------------+-------------+
   | 10        | 3           | 16          | 10          | 9           |
   +-----------+-------------+-------------+-------------+-------------+
   | 12        | 3           | 16          | 12          | 11          |
   +-----------+-------------+-------------+-------------+-------------+
   | 16        | 3           | 16          | 16          | 15          |
   +-----------+-------------+-------------+-------------+-------------+

The way of encoding pixels shall respect SMPTE ST2110-20.

.. note::

   This encoding is different than the encoding of Pixel Data
   (7FE0,0010). Example, for YBR_FULL_422 10 bits:

- SMPTE ST 2110-20 Video Flow YCbCr 4:2:2 10 bits

::

    0                   1                   2                   3
    0 1 2 3 4 5 6 7 8 9 0 1 2 3 4 5 6 7 8 9 0 1 2 3 4 5 6 7 8 9 0 1 2 3 4 5 6 7 8 9
   +-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+
   |   C'B00 (10 bits) |   Y'00 (10 bits)  |   C'R00 (10 bits) |   Y'01 (10 bits)  |
   +-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+

- DICOM Pixel Data (7FE0,0010) YBR_FULL_422 10 bits

::

    0                   1                   2                   3                   4                   5                   6
    0 1 2 3 4 5 6 7 8 9 0 1 2 3 4 5 6 7 8 9 0 1 2 3 4 5 6 7 8 9 0 1 2 3 4 5 6 7 8 9 0 1 2 3 4 5 6 7 8 9 0 1 2 3 4 5 6 7 8 9 0 1 2 3
   +-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+
   |   Y'00 (10 bits)  |0|0|0|0|0|0|    Y'01 (10 bits) |0|0|0|0|0|0|   C'B00 (10 bits) |0|0|0|0|0|0|   C'R00 (10 bits) |0|0|0|0|0|0|
   +-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+

A DICOM Transfer Syntax for SMPTE ST 2110-20 Uncompressed Progressive
Active Video shall be identified by a UID value of

-  1.2.840.10008.1.2.7.1 corresponding to
   `biblioentry_title <#biblio_SMPTE_ST2110-20>`__ for the progressive
   video.

.. _sect_A.9:

SMPTE ST 2110-20 Uncompressed Interlaced Active Video Transfer Syntax
---------------------------------------------------------------------

This Transfer Syntax is used in a DICOM-RTV Metadata Flow in order to
describe the accompanying
`biblioentry_title <#biblio_SMPTE_ST2110-20>`__ Video Flow.

The parameters are similar to the ones described in the
`biblioentry_title <#biblio_SMPTE_ST2110-20>`__ Uncompressed Progressive
Active Video (`SMPTE ST 2110-20 Uncompressed Progressive Active Video
Transfer Syntax <#sect_A.8>`__), but the frames are interlaced, one
frame containing only odd lines and the next one containing only even
lines.

A DICOM Transfer Syntax for SMPTE ST 2110-20 Uncompressed Interlaced
Active Video shall be identified by a UID value of:

-  1.2.840.10008.1.2.7.2 corresponding to
   `biblioentry_title <#biblio_SMPTE_ST2110-20>`__ for the interlaced
   video.

.. _sect_A.10:

: SMPTE ST 2110-30 PCM Audio Transfer Syntax
--------------------------------------------

This Transfer Syntax is used in a DICOM-RTV Metadata Flow in order to
describe the accompanying SMPTE ST21110-30 Audio Flow.

DICOM Attributes

-  Number of Waveform Channels (003A,0005) is limited to 15

-  Number of Waveform Samples (003A,0010) is limited to 96 (1ms at 96
   kHz)

-  Sampling Frequency (003A,001A) shall either be 44100, 48000 or 96000

-  Waveform Bits Stored (003A,021A) shall either be 16 or 24

-  Waveform Bits Allocated (5400,1004) shall either be 16 or 24

-  Waveform Sample Interpretation (5400,1006) shall either be US, SS or
   OB

.. table:: ST 2110-30 and DICOM sampling frequency

   ============================= =============================
   ST 2110-30 Sampling Frequency Sampling frequency(0003,001A)
   ============================= =============================
   44.1 kHz                      44100
   48 kHz\*                      48000
   96 kHz                        96000
   ============================= =============================

.. note::

   \* 48 kHz is recommended by SMPTE

.. table:: Waveform Sample Interpretation

   +-----------+-------------+-------------+-------------+-------------+
   | Bit Depth | Waveform    | Waveform    | Waveform    | Wave Sample |
   |           | Bits Stored | Bits        | Sample      | Int         |
   |           | (003A,021A) | Allocated   | Int         | erpretation |
   |           |             | (5400,1006) | erpretation | meaning     |
   |           |             |             | (5400,1006) |             |
   +===========+=============+=============+=============+=============+
   | 16        | 16          | 16          | SS          | signed      |
   |           |             |             |             | 16-bit      |
   |           |             |             |             | linear      |
   +-----------+-------------+-------------+-------------+-------------+
   | 16        | 16          | 16          | US          | unsigned    |
   |           |             |             |             | 16-bit      |
   |           |             |             |             | linear      |
   +-----------+-------------+-------------+-------------+-------------+
   | 24        | 24          | 24          | OB          | 24 bit      |
   |           |             |             |             | linear      |
   +-----------+-------------+-------------+-------------+-------------+

.. table:: Example of Number of Waveform Samples for 48kHz for basic
Audio (Mono or Stereo)

   +-----------+-------------+-------------+-------------+-------------+
   | Bit Depth | Waveform    | Numbers of  | Number of   | Resulting   |
   |           | Bits Stored | Waveform    | Waveform    | packet      |
   |           | (003A,021A) | Channels    | Sample      | Length      |
   |           |             | (003A,0005) | (003A,0010) | (1ms)       |
   +===========+=============+=============+=============+=============+
   | 16        | 16          | 1           | 48          | 96          |
   +-----------+-------------+-------------+-------------+-------------+
   | 24        | 24          | 1           | 48          | 144         |
   +-----------+-------------+-------------+-------------+-------------+
   | 16        | 16          | 2           | 48          | 192         |
   +-----------+-------------+-------------+-------------+-------------+
   | 24        | 24          | 2           | 48          | 288         |
   +-----------+-------------+-------------+-------------+-------------+

`biblioentry_title <#biblio_SMPTE_ST2110-30>`__ restricts the audio
Flow:

-  Sampling frequency is either 44.1 kHz, 48 kHz or 96 kHz, 48 kHz being
   the recommended value

-  Coding scheme is either L16 (16-bit linear) or L24 (24-bit linear)

-  Packet time should be 1ms (but could get down to 125 Âµs)

-  Number of Waveform Channels is limited to 15

A DICOM Transfer Syntax for SMPTE ST 2110-30 PCM Digital Audio shall be
identified by a UID value of:

-  1.2.840.10008.1.2.7.3 corresponding to the SMPTE ST 2110-30
   Professional Media over IP Networks: PCM Digital Audio.

