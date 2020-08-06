.. _chapter_D:

Examples of Various Pixel Data and Overlay Encoding Schemes (Informative)
=========================================================================

.. _sect_D.1:

Detailed Example of Pixel Data Encoding
---------------------------------------

As specified in , Image Pixel Data is stored within the Value of the
Pixel Data Element (7FE0,0010). The order in which Pixel Data for an
image plane is encoded is from left to right and top to bottom, a row at
a time (see Figure `figure_title <#figure_D-1>`__).

An individual pixel may consist of one or more Pixel Sample Values
(e.g., color or multi-planar images). Each Pixel Sample Value can be
expressed as either a binary 2's complement integer or a binary unsigned
integer, as specified by the Pixel Representation Data Element (0028,
0103). The number of bits in each Pixel Sample Value is specified by
Bits Stored (0028,0101). For 2's complement integer Pixel Samples the
sign bit is the most significant bit of the Pixel Sample Value.

A Pixel Cell is the container for a Pixel Sample Value and optionally
additional bits. These additional bits are used to place Pixels on
certain boundaries (byte, word, etc.). A Pixel Cell exists for every
individual Pixel Sample Value in the Pixel Data. The size of the Pixel
Cells is specified by Bits Allocated (0028,0100) and is greater than or
equal to the Bits Stored (0028,0101). The placement of the Pixel Sample
Values within the Pixel Cells is specified by High Bit (0028,0102).

Any restrictions on the characteristics of a Pixel Cell and the Pixel
Sample Value contained therein are specific to the Information Object
Definition (e.g., Image Object) containing the Pixel Data Element (see
).

The Pixel Data Element, as specified by the DICOM Default Transfer
Syntax in `DICOM Default Transfer Syntax <#sect_10.1>`__, has a Value
Representation of OW (Other Word). The Pixel Data in DICOM, as it was in
ACR-NEMA 2.0, is packed, except that Bits Allocated is always either 1,
or a multiple of 8 (see Figure `figure_title <#figure_D-2>`__). One way
to visualize this packed encoding is to imagine encoding the Pixel Cells
as a concatenated stream of bits from the least significant bit of the
first Pixel Cell up through the most significant bit of the last Pixel
Cell. Within this stream, the most significant bit of any Pixel Cell is
followed by the least significant bit of the next Pixel Cell. The Pixel
Data can then be broken up into a stream of physical 16-bit words, each
of which is subject to the byte ordering constraints of the Transfer
Syntax.

All other (non-default) DICOM Transfer Syntaxes make use of explicit VR
encoding. For these Transfer Syntaxes, all Pixel Data where Bits
Allocated is less than or equal to 8 may be encoded with an explicit VR
of OB (see `Transfer Syntax Specifications (Normative) <#chapter_A>`__).
As in the OW case, Pixel Cells are packed together, but in this case the
Pixel Data is broken up into a stream of physical 8-bit words.

.. note::

   For Pixel Data encoded with an explicit VR of OB, the encoding of the
   Pixel Data is unaffected by byte ordering.

With the exception of single bit images, Pixel Cells begin and end on
byte or word boundaries and such that the Pixel Sample Value contained
within also fits 'neatly' within a cell.

Figure `figure_title <#figure_D-3>`__ is an example of Pixel Data
encoding using the Value representation of OW for the purposes of
clarification. The Example is a valid example for a CT Image Information
Object.

Figure D-4 shows Pixel Data constructed of these example Pixel Cells as
they are packed into a stream of 16-bit words.

Byte ordering becomes a consideration when we represent the Pixel Data
physically, in memory, a file, or on a network.

In the memory of a byte-addressable Big Endian machine, the highest
order byte (bits 8 - 15) in each 16-bit word has a binary address of
x...x0. While in a byte-addressable Little Endian machine, the lowest
order byte (bits 0 - 7) in each 16-bit word has a binary address of
x...x0. Figure D-5 pictures our example Pixel Data streams as they would
be addressed in the memory of both a Big Endian and a Little Endian
machine.

Byte ordering is also specified as part of the negotiated Transfer
Syntax used in the exchange of a DICOM message. Sixteen bit words are
transmitted across the network (a byte at a time) least significant byte
first in the case of a Little Endian Transfer Syntax (see Figure
`figure_title <#figure_D-6>`__).

As a last pair of examples, for Pixel Data having the Value
Representation OW and the following attributes: 8 bits allocated, 8 bits
stored, and a high bit of 7; the resulting byte streams pictured in
`figure_title <#figure_D-7>`__ are as they would be transmitted across a
network and/or stored on media. For Pixel Data having the same
attributes, but having the explicit Value Representation OB; the
resulting byte streams are unaffected by byte ordering and are pictured
in `figure_title <#figure_D-8>`__.

.. _sect_D.2:

Various Additional Examples of Pixel and Overlay Data Cells
-----------------------------------------------------------

The following examples further illustrate the use of the data elements
for Bits Allocated (0028,0100), Bits Stored (0028,0101) and High Bit
(0028,0102) in the encoding of Pixel and Overlay Data. All examples show
sample Pixel Cells before being encoded in byte streams (and before
being affected by a particular Transfer Syntax).

Figure D.2-2 Example 2 of Pixel and Overlay Data Cells has been retired.
See PS3.3 2014c.

.. note::

   In this example, the Overlay Bits are numbered in the same manner
   that Pixel Cells are numbered in the other examples in this Annex.
   That is Overlay Bit 1 is the first bit of the Overlay Plane, encoded
   from left to right and top to bottom, a row at a time.

.. _sect_D.3:

Examples of Float and Double Float Pixel Data
---------------------------------------------

Float Pixel Data having the Value Representation OF always has 32 bits
allocated; the resulting byte streams pictured in
`figure_title <#figure_D.3-1>`__ are as they would be transmitted across
a network and/or stored on media.

Double Float Pixel Data having the Value Representation OD always has 64
bits allocated; the resulting byte streams pictured in
`figure_title <#figure_D.3-2>`__ are as they would be transmitted across
a network and/or stored on media.

