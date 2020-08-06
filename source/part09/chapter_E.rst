.. _chapter_E:

Usage of the P-DATA Service By the DICOM Application Entity (Normative)
=======================================================================

This Annex specifies how DICOM messages are encapsulated into the P-DATA
Service by the DICOM Application Entity.

.. _sect_E.1:

Encapsulation Rules
-------------------

DICOM Messages are encapsulated in P-DATA request primitives as the user
data of Presentation Data Values (PDV). A DICOM Message is fragmented in
Command Fragments and Data Fragments, each placed in a PDV. The same
presentation context shall be used for every fragment of the same
message (i.e., same Presentation Context ID for the user data of the
PDVs containing the fragments of a same message). A PDV User Data
parameter shall contain one and only one fragment (either Command or
Data) preceded by a Message Control Header. This header will indicate:

a. whether the fragment is of the Command or Data type

b. whether the fragment is or is not the last fragment of a Command/Data
   Stream of a DICOM Message

A P-DATA request PDV List parameter shall contain one or more such
PDV(s) (Message Control Header and a complete message fragment). Each
PDV is wholly contained in a given P-DATA request primitive and does not
span across several P-DATA request primitives. The PDVs contained in a
P-DATA request primitive shall be related to the same DICOM message.
Each fragment of a message shall consist of an even number of bytes.

.. note::

   1. No padding is necessary as defines messages on an even byte
      boundary.

   2. The above rules state that each fragment contained in a PDV shall
      consist of an even number of bytes (only). Therefore, encoding
      such as Group Number, Element Number, Value Length, etc. (as
      defined by the DICOM Application Entity, see ) is not guaranteed
      to be within the same PDV.

The fragmentation of any message results in a series of PDVs that shall
be sent, on a given association, by a corresponding series of P-DATA
requests preserving the ordering of the fragments of any message.
Furthermore, no fragments of any other message shall be sent until all
fragments of the current message have been sent (i.e., interleaving of
fragments from different messages is not permitted).

It is strongly recommended that two consecutive PDVs in the same P-DATA
Request primitive (therefore containing fragments of the same message
using the same Presentation Context ID) do not contain two message
Control Headers with the same type (Command or Data). These should have
been combined in a single PDV by the sender. However, receivers must be
able to receive and process such PDVs.

.. note::

   The above rules allow the sending in the same P-DATA
   request/indication of a Command fragment in the first PDV (with the
   last fragment flag set) followed by a Data Fragment in the second PDV
   (with the last fragment flag set or not). In particular, if the
   negotiated maximum length for the PDV List parameter of the P-DATA
   request is sufficient to hold a complete message, a single P-DATA
   request can be used to exchange an entire message.

Individual PDVs shall not be sent with Presentation-data-value fields
consisting only of a single byte containing a Message Control Header,
but without any other content in the fragment. These should have been
combined with the preceding or succeeding PDVs by the sender.

.. note::

   Even though the above rules prohibit the sending of an "empty" PDV
   (such as with the last fragment flag set), it is recommended that
   receivers be able to receive and process such PDVs.

.. _sect_E.2:

Message Control Header Encoding
-------------------------------

The Message Control Header is located in front of each DICOM message
fragment (see `figure_title <#figure_E.2-1>`__). Its presence is
mandatory for all DICOM Abstract Syntaxes (see `Abstract and Transfer
Syntaxes (Informative) <#chapter_B>`__ for further discussion on
Abstract Syntaxes).

The Message Control Header shall be made of one byte with the least
significant bit (bit 0) taking one of the following values:

a. If bit 0 is set to 1, the following fragment shall contain Message
   Command information.

b. If bit 0 is set to 0, the following fragment shall contain Message
   Data Set information.

The next least significant bit (bit 1) shall be defined by the following
rules:

a. If bit 1 is set to 1, the following fragment shall contain the last
   fragment of a Message Data Set or of a Message Command.

b. If bit 1 is set to 0, the following fragment does not contain the
   last fragment of a Message Data Set or of a Message Command.

Bits 2 through 7 are always set to 0 by the sender and never checked by
the receiver.

.. note::

   The Message Control Header, in the Transport data flow, is the 1st
   byte in each PDV. The Transfer Syntax, negotiated at association
   establishment, defines the encoding for the Command/Data fragment.

