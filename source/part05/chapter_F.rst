.. _chapter_F:

Encapsulated Images As Part of A DICOM Message (Informative)
============================================================

The following remarks apply generally to communicating an encoded image
within a message structure according to the DICOM Standard:

a) In the course of including an encoded image in a DICOM message, the
encoding is not changed. The encoded data stream is merely segmented and
encapsulated according to the protocols of the DICOM Standard. After
unpacking the DICOM message, the encoded data stream can be fully
reconstructed at the receiving node.

b) The object definition of the DICOM Standard is always determining
format and other choices that a specific encoding implementation may
offer. The encoded image must be consistent with the definition of the
object of which the encoded image is part. For example:

1) If the object is defined to contain 10-bit pixel data, it is assumed
that the encoding process is one that accepts at least 10-bit data.
Hence, there is no need for defining separate Transfer Syntaxes, e.g.,
for 8-bit or 12-bit implementations. Any 12-bit implementation is
assumed to operate in an 8-bit process if the object is defined to
contain 8-bit data.

2) If the image of an object is interleaved, the encoding process must
reproduce the interleaving.

c) Specifications in the encoding file header must be consistent with
the DICOM Message header, e.g., regarding the number of rows and
columns.

d) The byte order specification of an encoded file is not altered in the
course of encapsulating it in a DICOM message.

.. _sect_F.1:

Encapsulated JPEG Encoded Images
--------------------------------

The International Standards Organization (ISO/IEC JTC1/SC2/WG10) has
prepared an International Standard, ISO 10918-1 (JPEG Part 1) and
International Draft Standard ISO 10918-2 (JPEG Part 2), for the digital
compression and coding of continuous-tone still images. This standard is
collectively known as the JPEG Standard.

Part 1 of the JPEG Standard sets out requirements and implementation
guidelines for the coded representation of compressed image data to be
interchanged between applications. The processes and representations are
intended to be generic in order to support the broad range of
applications for color and grayscale still images for the purpose of
communications and storage within computer systems. Part 2 of the JPEG
Standard defines tests for determining whether implementations comply
with the requirements of the various encoding and decoding processes
specified in Part 1 of the JPEG Standard.

The JPEG Standard specifies lossy and lossless code processes. The lossy
coding is based on the discrete cosine transform (DCT), permitting data
compression with an adjustable compression ratio. The lossless coding
employs differential pulse code modulation (DPCM).

The JPEG Standard permits a variety of coding processes for the coder
and decoder. These processes differ in coding schemes for the quantified
data and in sample precision. The coding processes are consecutively
numbered as defined in the International Draft Standard ISO 10918-2
(JPEG Part 2), and are summarized in `table_title <#table_F.1-1>`__. The
simplest DCT-based coding process is referred to as Baseline Sequential
with Huffman Coding for 8-bit Samples.

.. table:: JPEG Modes of Image Coding

   +-------+-------+-------+-------+-------+-------+-------+-------+
   | **    | **Des | **Lo  | **Non | **Se  | **T   | **Cod | **Acc |
   | No.** | cript | ssy** | -Hier | quent | ransf | ing** | epted |
   |       | ion** |       | archi | ial** | orm** |       | B     |
   |       |       | *     | cal** |       |       |       | its** |
   |       |       | *LY** |       | **S** |       |       |       |
   |       |       |       | *     |       |       |       |       |
   |       |       | **    | *NH** | **Pro |       |       |       |
   |       |       | Lossl |       | gress |       |       |       |
   |       |       | ess** | *     | ive** |       |       |       |
   |       |       |       | *Hier |       |       |       |       |
   |       |       | *     | archi | **P** |       |       |       |
   |       |       | *LL** | cal** |       |       |       |       |
   |       |       |       |       |       |       |       |       |
   |       |       |       | **H** |       |       |       |       |
   +=======+=======+=======+=======+=======+=======+=======+=======+
   | 1     | Bas   | LY    | NH    | S     | DCT   | Hu    | 8     |
   |       | eline |       |       |       |       | ffman |       |
   | 2     |       | LY    | NH    | S     | DCT   |       | 8     |
   |       | Ext   |       |       |       |       | Hu    |       |
   | 4     | ended | LY    | NH    | S     | DCT   | ffman | 12    |
   |       |       |       |       |       |       |       |       |
   |       | Ext   |       |       |       |       | Hu    |       |
   |       | ended |       |       |       |       | ffman |       |
   +-------+-------+-------+-------+-------+-------+-------+-------+
   | 14    | Los   | LL    | NH    | S     | DPCM  | Hu    | 2-16  |
   |       | sless |       |       |       |       | ffman |       |
   +-------+-------+-------+-------+-------+-------+-------+-------+

The different coding processes specified in the JPEG Standard are
closely related. By extending the capability of an implementation,
increasingly more 'lower level' processes can also be executed by the
implementation. This is shown in `table_title <#table_F.1-2>`__ for
Huffman Coding.

Inclusion of a JPEG-coded image in a DICOM message is facilitated by the
use of specific Transfer Syntaxes that are defined in `Transfer Syntax
Specifications (Normative) <#chapter_A>`__. Independent of the JPEG
coding processes, the same syntax applies. The only distinction for
different processes in the syntax (apart from different SOF marker
segments in the JPEG bit stream) is the UID value.
`table_title <#table_F.1-5>`__ lists the UID values in the Transfer
Syntax for the various JPEG coding processes for reference.

.. table:: Relationship Between the Lossy JPEG Huffman Coding Processes

   =========== ===== ===== =====
   **Process** **1** **2** **4**
   =========== ===== ===== =====
   **1**       \*    \*    \*
   **2**             \*    \*
   **4**                   \*
   =========== ===== ===== =====

\* Coding process of column can execute coding process of row

.. table:: Identification of JPEG Coding Processes in DICOM

   +----------------+----------------+----------------+----------------+
   | **DICOM        | **JPEG         | **JPEG         | **capable of   |
   | Transfer       | process**      | description**  | decoding**     |
   | Syntax UID**   |                |                |                |
   +================+================+================+================+
   | 1.2.840.       | 1              | baseline       | 1              |
   | 10008.1.2.4.50 |                |                |                |
   +----------------+----------------+----------------+----------------+
   | 1.2.840.       | 2,4            | extended       | 1,2,4 (see     |
   | 10008.1.2.4.51 |                |                | `              |
   |                |                |                | note_title <#n |
   |                |                |                | ote_F.1-1>`__) |
   +----------------+----------------+----------------+----------------+
   | 1.2.840.       | 14             | lossless NH    | 14             |
   | 10008.1.2.4.57 |                |                |                |
   +----------------+----------------+----------------+----------------+
   | 1.2.840.       | 14             | lossless NH,   |                |
   | 10008.1.2.4.70 |                | first-order    |                |
   |                | Selection      | prediction     |                |
   |                | Value 1        |                |                |
   +----------------+----------------+----------------+----------------+

.. note::
   :name: note_F.1-1

   Though the coding processes (2, 4) described in ISO 10918-1 are
   capable of decoding the other listed process (1), the bit stream uses
   different SOF marker segments. I.e., the baseline JPEG process 1 used
   with the 1.2.840.10008.1.2.4.50 Transfer Syntax uses the SOF0 marker,
   whereas the extended process 2 used with the 1.2.840.10008.1.2.4.51
   Transfer Syntax uses the SOF1 marker. Accordingly, even though both
   bit streams encode 8 bit images using DCT and Huffman coding, the bit
   streams are not identical.

   ISO 10918-2 describes compliance tests for decoders, and requires
   that implementations of specific extended processes (such as 2 and 4)
   be capable of decoding bit streams of related baseline processes
   (such as 1) (ISO 10918-2 Section 7.4 Compliance tests for DCT-based
   sequential mode decoding processes). The converse is not true for
   encoders however, and the presence of SOF marker segments not defined
   by the specific process is not compliant (ISO 10918-2 Section 5.1.1
   Non-hierarchical coding processes syntax compliance test Tables 1 and
   2).

.. _sect_F.2:

Encapsulated JPEG-LS Encoded Images
-----------------------------------

The International Standards Organization (ISO/IEC JTC1/SC2/WG10) has
prepared an International Standard, ISO/IS-14495-1 (JPEG-LS Part 1), for
the digital compression and coding of continuous-tone still images. This
standard is known as the JPEG-LS Standard.

Part 1 of the JPEG-LS Standard sets out requirements and implementation
guidelines for the coded representation of compressed image data to be
interchanged between applications. The processes and representations are
intended to be generic in order to support the broad range of
applications for color and grayscale still images for the purpose of
communications and storage within computer systems.

The JPEG-LS Standard specifies a single lossy (near-lossless) code
process that can achieve lossless compression by constraining the
absolute error value during encoding to zero. The lossless and lossy
(near-lossless) coding is based on a predictive scheme with statistical
modeling, in which differences between pixels and their surround are
computed and their context modeled prior to coding, with a run-length
escape mechanism. This scheme achieves consistently better compression
in lossless mode than the lossless processes of JPEG defined in ISO
10918-1, with less complexity.

Though a different coding process from those specified in ISO 10918-1 is
used, the syntax of the encoded bit stream is closely related.

A single JPEG-LS process is used for bit depths up to 16 bits.

Inclusion of a JPEG-LS coded image in a DICOM message is facilitated by
the use of specific Transfer Syntaxes that are defined in `Transfer
Syntax Specifications (Normative) <#chapter_A>`__.

.. _sect_F.3:

Encapsulated JPEG 2000 Encoded Images
-------------------------------------

The International Standards Organization (ISO/IEC JTC1/SC2/WG10) has
prepared an International Standard, ISO/IEC-15444 (JPEG 2000), for the
digital compression and coding of continuous-tone still images. This
standard is known as the JPEG 2000 Standard.

The JPEG 2000 Standard sets out requirements and implementation
guidelines for the coded representation of compressed image data to be
interchanged between applications. The processes and representations are
intended to be generic in order to support the broad range of
applications for color and grayscale still images for the purpose of
communications and storage within computer systems.

Though a different coding process from those specified in ISO 10918-1 is
used, the syntax of the encoded bit stream is closely related.

A single JPEG 2000 process is used for bit depths up to 16 bits.

Inclusion of a JPEG 2000 coded image in a DICOM message is facilitated
by the use of specific Transfer Syntaxes that are defined in `Transfer
Syntax Specifications (Normative) <#chapter_A>`__.

