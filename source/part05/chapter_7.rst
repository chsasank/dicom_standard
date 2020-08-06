.. _chapter_7:

The Data Set
============

A Data Set represents an instance of a real world Information Object. A
Data Set is constructed of Data Elements. Data Elements contain the
encoded Values of Attributes of that object. The specific content and
semantics of these Attributes are specified in Information Object
Definitions (see ).

The construction, characteristics, and encoding of a Data Set and its
Data Elements are discussed in this section. Pixel Data, Overlays, and
Curves are Data Elements whose interpretation depends on other related
elements.

.. _sect_7.1:

Data Elements
-------------

A Data Element is uniquely identified by a Data Element Tag. The Data
Elements in a Data Set shall be ordered by increasing Data Element Tag
Number and shall occur at most once in a Data Set.

.. note::

   A Data Element Tag may occur again within Nested Data Sets (see
   `Nesting of Data Sets <#sect_7.5>`__).

Two types of Data Elements are defined:

-  Standard Data Elements have an even Group Number that is not
   (0000,eeee), (0002,eeee), (0004,eeee), or (0006,eeee).

   .. note::

      Usage of these groups is reserved for DIMSE Commands (see ) and
      DICOM File Formats.

-  Private Data Elements have an odd Group Number that is not
   (0001,eeee), (0003,eeee), (0005,eeee), (0007,eeee), or (FFFF,eeee).
   Private Data Elements are discussed further in `Private Data
   Elements <#sect_7.8>`__.

.. note::

   Although similar or related Data Elements often have the same Group
   Number; a Data Group does not convey any semantic meaning.

A Data Element shall have one of three structures. Two of these
structures contain the VR of the Data Element (Explicit VR) but differ
in the way their lengths are expressed, while the other structure does
not contain the VR (Implicit VR). All three structures contain the Data
Element Tag, Value Length and Value for the Data Element. See
`figure_title <#figure_7.1-1>`__.

Implicit and Explicit VR Data Elements shall not coexist in a Data Set
and Data Sets nested within it (see `Nesting of Data
Sets <#sect_7.5>`__). Whether a Data Set uses Explicit or Implicit VR,
among other characteristics, is determined by the negotiated Transfer
Syntax (see `Transfer Syntax <#chapter_10>`__ and `Transfer Syntax
Specifications (Normative) <#chapter_A>`__).

.. note::

   VRs are not contained in Data Elements when using DICOM Default
   Transfer Syntax (DICOM Implicit VR Little Endian Transfer Syntax).

.. _sect_7.1.1:

Data Element Fields
~~~~~~~~~~~~~~~~~~~

A Data Element is made up of fields. Three fields are common to all
three Data Element structures; these are the Data Element Tag, Value
Length, and Value Field. A fourth field, Value Representation, is only
present in the two Explicit VR Data Element structures. The Data Element
structures are defined in `Data Element Structure with Explicit
VR <#sect_7.1.2>`__ and `Data Element Structure with Implicit
VR <#sect_7.1.3>`__. The definitions of the fields are:

Data Element Tag
   An ordered pair of 16-bit unsigned integers representing the Group
   Number followed by Element Number.

Value Representation
   Two single byte characters containing the VR of the Data Element. The
   VR for a given Data Element Tag shall be as defined by the Data
   Dictionary as specified in . The two byte VR shall be encoded using
   only upper case letters from the DICOM default character set.

Value Length
   Either:

   -  a 16 or 32-bit (dependent on VR and whether VR is explicit or
      implicit) unsigned integer containing the Explicit Length of the
      Value Field as the number of bytes (even) that make up the Value.
      It does not include the length of the Data Element Tag, Value
      Representation, and Value Length Fields.

   -  a 32-bit Length Field set to Undefined Length (FFFFFFFFH).
      Undefined Lengths may be used for Data Elements having the Value
      Representation (VR) Sequence of Items (SQ) and Unknown (UN). For
      Data Elements with Value Representation OW or OB Undefined Length
      may be used depending on the negotiated Transfer Syntax (see
      `Transfer Syntax <#chapter_10>`__ and `Transfer Syntax
      Specifications (Normative) <#chapter_A>`__).

   .. note::

      1. The decoder of a Data Set should support both Explicit and
         Undefined Lengths for VRs of SQ and UN and, when applicable,
         for VRs of OW and OB.

      2. The 32-bit Value Length Field limits the maximum size of large
         data values such as Pixel Data sent in a Native Format (encoded
         in Transfer Syntaxes that use only the unencapsulated form).

Value Field
   An even number of bytes containing the Value(s) of the Data Element.

   The data type of Value(s) stored in this field is specified by the
   Data Element's VR. The VR for a given Data Element Tag can be
   determined using the Data Dictionary in , or using the VR Field if it
   is contained explicitly within the Data Element. The VR of Standard
   Data Elements shall agree with those specified in the Data
   Dictionary.

   The Value Multiplicity specifies how many Values with this VR can be
   placed in the Value Field. If the VM is greater than one, multiple
   values shall be delimited within the Value Field as defined
   previously in `Value Multiplicity (VM) and
   Delimitation <#sect_6.4>`__. The VMs of Standard Data Elements are
   specified in the Data Dictionary in .

   Value Fields with Undefined Length are delimited through the use of
   Sequence Delimitation Items and Item Delimitation Data Elements,
   which are described further in `Nesting of Data Sets <#sect_7.5>`__.

.. _sect_7.1.2:

Data Element Structure with Explicit VR
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

When using the Explicit VR structures, the Data Element shall be
constructed of four consecutive fields: Data Element Tag, VR, Value
Length, and Value. Depending on the VR of the Data Element, the Data
Element will be structured in one of two ways:

-  for VRs of AE, AS, AT, CS, DA, DS, DT, FL, FD, IS, LO, LT, PN, SH,
   SL, SS, ST, TM, UI, UL and US the Value Length Field is the 16-bit
   unsigned integer following the two byte VR Field
   (`table_title <#table_7.1-2>`__). The value of the Value Length Field
   shall equal the length of the Value Field.

-  for all other VRs the 16 bits following the two byte VR Field are
   reserved for use by later versions of the DICOM Standard. These
   reserved bytes shall be set to 0000H and shall not be used or decoded
   (`table_title <#table_7.1-1>`__). The Value Length Field is a 32-bit
   unsigned integer.

   -  for VRs of OB, OD, OF, OL, OV, OW, SQ and UN, if the Value Field
      has an Explicit Length, then the Value Length Field shall contain
      a value equal to the length (in bytes) of the Value Field,
      otherwise, the Value Field has an Undefined Length and a Sequence
      Delimitation Item marks the end of the Value Field.

   -  for all other VRs with a 32-bit Value Length Field, the Value
      Length Field shall contain a value equal to the length (in bytes)
      of the Value Field.

   .. note::

      VRs of SV, UC, UR, UV and UT may not have an Undefined Length,
      i.e.,a Value Length of FFFFFFFFH.

.. table:: Data Element with Explicit VR other than as shown in
`table_title <#table_7.1-2>`__

   +----------+----------+----------+----------+----------+----------+
   | **Tag**  | **VR**   | **Value  | *        |          |          |
   |          |          | Length** | *Value** |          |          |
   +==========+==========+==========+==========+==========+==========+
   | Group    | Element  | VR       | Reserved | 32-bit   | Even     |
   | Number   | Number   |          | (2       | unsigned | number   |
   |          |          | (2       | bytes)   | integer  | of bytes |
   | (16-bit  | (16-bit  | single   | set to a |          | co       |
   | unsigned | unsigned | byte     | value of |          | ntaining |
   | integer) | integer) | cha      | 0000H    |          | the Data |
   |          |          | racters) |          |          | Element  |
   |          |          |          |          |          | Value(s) |
   |          |          |          |          |          | encoded  |
   |          |          |          |          |          | a        |
   |          |          |          |          |          | ccording |
   |          |          |          |          |          | to the   |
   |          |          |          |          |          | VR and   |
   |          |          |          |          |          | ne       |
   |          |          |          |          |          | gotiated |
   |          |          |          |          |          | Transfer |
   |          |          |          |          |          | Syntax.  |
   |          |          |          |          |          | D        |
   |          |          |          |          |          | elimited |
   |          |          |          |          |          | with     |
   |          |          |          |          |          | Sequence |
   |          |          |          |          |          | Deli     |
   |          |          |          |          |          | mitation |
   |          |          |          |          |          | Item if  |
   |          |          |          |          |          | of       |
   |          |          |          |          |          | U        |
   |          |          |          |          |          | ndefined |
   |          |          |          |          |          | Length.  |
   +----------+----------+----------+----------+----------+----------+
   | 2 bytes  | 2 bytes  | 2 bytes  | 2 bytes  | 4 bytes  | 'Value   |
   |          |          |          |          |          | Length'  |
   |          |          |          |          |          | bytes if |
   |          |          |          |          |          | of       |
   |          |          |          |          |          | Explicit |
   |          |          |          |          |          | Length   |
   +----------+----------+----------+----------+----------+----------+

.. table:: Data Element with Explicit VR of AE, AS, AT, CS, DA, DS, DT,
FL, FD, IS, LO, LT, PN, SH, SL, SS, ST, TM, UI, UL and US

   +-------------+-------------+-------------+-------------+-------------+
   | **Tag**     | **VR**      | **Value     | **Value**   |             |
   |             |             | Length**    |             |             |
   +=============+=============+=============+=============+=============+
   | Group       | Element     | VR          | (16-bit     | Even number |
   | Number      | Number      |             | unsigned    | of bytes    |
   |             |             | (2 single   | integer)    | containing  |
   | (16-bit     | (16-bit     | byte        |             | the Data    |
   | unsigned    | unsigned    | characters) |             | Element     |
   | integer)    | integer)    |             |             | Value(s)    |
   |             |             |             |             | encoded     |
   |             |             |             |             | according   |
   |             |             |             |             | to the VR   |
   |             |             |             |             | and         |
   |             |             |             |             | negotiated  |
   |             |             |             |             | Transfer    |
   |             |             |             |             | Syntax.     |
   +-------------+-------------+-------------+-------------+-------------+
   | 2 bytes     | 2 bytes     | 2 bytes     | 2 bytes     | 'Value      |
   |             |             |             |             | Length'     |
   |             |             |             |             | bytes       |
   +-------------+-------------+-------------+-------------+-------------+

.. _sect_7.1.3:

Data Element Structure with Implicit VR
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

When using the Implicit VR structure the Data Element shall be
constructed of three consecutive fields: Data Element Tag, Value Length,
and Value (see `table_title <#table_7.1-3>`__). If the Value Field has
an Explicit Length then the Value Length Field shall contain a value
equal to the length (in bytes) of the Value Field. Otherwise, the Value
Field has an Undefined Length and a Sequence Delimitation Item marks the
end of the Value Field.

.. table:: Data Element with Implicit VR

   +----------------+----------------+----------------+----------------+
   | **Tag**        | **Value        | **Value**      |                |
   |                | Length**       |                |                |
   +================+================+================+================+
   | Group Number   | Element Number | 32-bit         | Even number of |
   |                |                | unsigned       | bytes          |
   | (16-bit        | (16-bit        | integer        | containing the |
   | unsigned       | unsigned       |                | Data Elements  |
   | integer)       | integer)       |                | Value encoded  |
   |                |                |                | according to   |
   |                |                |                | the VR         |
   |                |                |                | specified in   |
   |                |                |                | and the        |
   |                |                |                | negotiated     |
   |                |                |                | Transfer       |
   |                |                |                | Syntax.        |
   |                |                |                | Delimited with |
   |                |                |                | Sequence       |
   |                |                |                | Delimitation   |
   |                |                |                | Item if of     |
   |                |                |                | Undefined      |
   |                |                |                | Length.        |
   +----------------+----------------+----------------+----------------+
   | 2 bytes        | 2 bytes        | 4 bytes        | 'Value Length' |
   |                |                |                | bytes or       |
   |                |                |                | Undefined      |
   |                |                |                | Length         |
   +----------------+----------------+----------------+----------------+

.. _sect_7.2:

Group Length
------------

Group Length (gggg,0000) Data Elements were implicitly defined for
Standard and Private Data Element groups with a Value Representation of
UL and a Value Multiplicity of 1, but have been retired. See PS3.5-2007.

All implementations shall be able to parse Group Length elements, and
may discard and not insert or re-insert them; if present they shall be
consistent with the encoding of the Data Set even if the Transfer Syntax
is changed resulting in a change in the actual length of a group of
elements. No implementation shall require the presence of Group Length
elements.

.. note::

   1. Elements in groups 0, 2, 4 and 6 are not Standard Data Elements.
      Mandatory requirements for Group Length for groups 0 and 2 are
      specified elsewhere in the Standard.

   2. It is recommended that Group Length elements be removed during
      storage or transfer in order to avoid the risk of inconsistencies
      arising during coercion of data element values and changes in
      Transfer Syntax.

.. _sect_7.3:

Little Endian Byte Ordering
---------------------------

All nonretired Transfer Syntaxes in DICOM require the use of Little
Endian Byte Ordering.

Little Endian byte ordering is defined as follows:

-  In a binary number consisting of multiple bytes (e.g., a 32-bit
   unsigned integer value, the Group Number, the Element Number, etc.),
   the least significant byte shall be encoded first; with the remaining
   bytes encoded in increasing order of significance.

-  In a character string consisting of multiple 8-bit single byte codes,
   the characters will be encoded in the order of occurrence in the
   string (left to right).

Big Endian byte ordering was previously described but has been retired,
See PS3.5 2016b.

.. note::

   The packing of bits within values of OB or OW Value Representation
   for Pixel Data and Overlay Data is described in `Encoding of Pixel,
   Overlay and Waveform Data <#chapter_8>`__. The OL and OV Value
   Representations are not used for Pixel Data or Overlay Data.

Byte ordering is a component of an agreed upon Transfer Syntax (see
`Transfer Syntax <#chapter_10>`__). The default DICOM Transfer Syntax,
which shall be supported by all AEs, uses Little Endian encoding and is
specified in `DICOM Implicit VR Little Endian Transfer
Syntax <#sect_A.1>`__. Alternate Little Endian Transfer Syntaxes are
also specified in `Transfer Syntax Specifications
(Normative) <#chapter_A>`__.

.. note::

   The Command Set structure as specified in is encoded using the Little
   Endian Implicit VR Transfer Syntax.

In the case of Little Endian encoding, Big Endian Machines interpreting
Data Sets shall do 'byte swapping' before interpreting or operating on
certain Data Elements. The Data Elements affected are all those having
VRs that are multiple byte Values and that are not a character string of
8-bit single byte codes. VRs constructed of a string of characters of
8-bit single byte codes are really constructed of a string of individual
bytes, and are therefore not affected by byte ordering. The VRs that are
not a string of characters and consist of multiple bytes are:

-  2-byte US, SS, OW and each component of AT

-  4-byte OF, OL, UL, SL, and FL

-  8 byte OD, OV, FD, SV and UV

.. note::

   For the above VRs, the multiple bytes are presented in increasing
   order of significance when in Little Endian format. For example, an
   8-byte Data Element with VR of FD, might be written in hexadecimal as
   68AF4B2CH, but encoded in Little Endian would be 2C4BAF68H.

.. _sect_7.4:

Data Element Type
-----------------

An attribute, encoded as a Data Element, may or may not be required in a
Data Set, depending on that Attribute's Data Element Type.

The Data Element Type of an Attribute of an Information Object
Definition or an Attribute of a SOP Class Definition is used to specify
whether that Attribute is mandatory or optional. The Data Element Type
also indicates if an Attribute is conditional (only mandatory under
certain conditions). The Data Element Types of Attributes of Composite
IODs are specified in . The Data Element Types of Attributes of
Normalized IODs are specified as Attributes of SOP Classes in .

.. _sect_7.4.1:

Type 1 Required Data Elements
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

IODs and SOP Classes define Type 1 Data Elements that shall be included
and are mandatory elements. The Value Field shall contain valid data as
defined by the elements VR and VM as specified in . The Length of the
Value Field shall not be zero. Absence of a valid Value in a Type 1 Data
Element is a protocol violation.

.. note::

   1. For data elements with a string (CS, SH, LO) rather than binary,
      text or sequence Value Representation, and for which multiple
      Values are allowed, the presence of a single Value is sufficient
      to satisfy the Type 1 requirement, unless specified otherwise in
      the Attribute description, and other Values may be empty, unless
      otherwise specified by the IOD. The presence of one or more
      delimiter (BACKSLASH) characters alone, without any Values, is not
      sufficient to satisfy the Type 1 requirement, since even though
      the Value Length is greater than zero, there is no valid Value
      present.

   2. A Type 1 Sequence Data Element will contain one or more Items, as
      defined by the IOD (irrespective of the VM of the Sequence, which
      is always one (`Nesting of Data Sets <#sect_7.5>`__)). Whether or
      not those Items may be empty (contain no Data Elements) depends on
      the IOD definition of the Data Set for each Item.

.. _sect_7.4.2:

Type 1C Conditional Data Elements
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

IODs and SOP Classes define Data Elements that shall be included under
certain specified conditions. Type 1C elements have the same
requirements as Type 1 elements under these conditions. It is a protocol
violation if the specified conditions are met and the Data Element is
not included.

When the specified conditions are not met, Type 1C elements shall not be
included in the Data Set.

.. _sect_7.4.3:

Type 2 Required Data Elements
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

IODs and SOP Classes define Type 2 Data Elements that shall be included
and are mandatory Data Elements. However, it is permissible that if a
Value for a Type 2 element is unknown it can be encoded with zero Value
Length and no Value. If the Value is known the Value Field shall contain
that value as defined by the elements VR and VM as specified in . These
Data Elements shall be included in the Data Set and their absence is a
protocol violation.

.. note::

   1. The intent of Type 2 Data Elements is to allow a zero length to be
      conveyed when the operator or application does not know its value
      or has a specific reason for not specifying its value. It is the
      intent that the device should support these Data Elements.

   2. A Type 2 Sequence Data Element will contain zero or more Items, as
      defined by the IOD (irrespective of the VM of the Sequence, which
      is always one (`Nesting of Data Sets <#sect_7.5>`__)). An empty
      Type 2 Sequence is one with no Items, as opposed to an Item that
      is present but empty. Whether or not Items may be empty (contain
      no Data Elements) depends on the IOD definition of the Data Set
      for each Item, rather than the Type of the enclosing Sequence Data
      Element.

.. _sect_7.4.4:

Type 2C Conditional Data Elements
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

IODs and SOP Classes define Type 2C elements that have the same
requirements as Type 2 elements under certain specified conditions. It
is a protocol violation if the specified conditions are met and the Data
Element is not included.

When the specified conditions are not met, Type 2C elements shall not be
included in the Data Set.

.. note::

   An example of a Type 2C Data Element is Inversion Time (0018,0082).
   For several SOP Class Definitions, this Data Element is required only
   if the Scanning Sequence (0018,0020) has the Value "IR." It is not
   required otherwise. See .

.. _sect_7.4.5:

Type 3 Optional Data Elements
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

IODs and SOP Classes define Type 3 Data Elements that are optional Data
Elements. Absence of a Type 3 element from a Data Set does not convey
any significance and is not a protocol violation. Type 3 elements may
also be encoded with zero length and no Value. The meaning of a zero
length Type 3 Data Element shall be precisely the same as that element
being absent from the Data Set.

.. _sect_7.4.6:

Data Element Types Within A Sequence
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

When an IOD defines a Sequence Data Element (see `Nesting of Data
Sets <#sect_7.5>`__), the Type of the Sequence attribute defines whether
the Sequence attribute itself must be present, and the Attribute
Description of the Sequence attribute may define whether and how many
Items shall be present in the Sequence. The Types of the attributes of
the Data Set included in the Sequence, including any conditionality, are
specified within the scope of each Data Set, i.e., for each Item present
in the Sequence.

.. note::

   1. The Type and Attribute Description of the Sequence determines
      whether Items are present; conditionality constraints on Data
      Elements of the Items cannot force an Item to be present.

   2. Historically, many IODs declared Type 1 and Type 2 Data Elements
      of the Sequence to be Type 1C and Type 2C, respectively, with the
      condition that an Item is present. This is exactly the same as
      simply defining them as Type 1 and Type 2.

   3. In particular, the conditionality constraint "Required if Sequence
      is sent" on the Type 1C or Type 2C Data Elements subsidiary to a
      Type 2 or 3 Sequence attribute does not imply that an Item must be
      present in the Sequence. These conditions are meant to be
      equivalent to "Required if a Sequence Item is present", and the
      conditionality is not strictly necessary. Any Type 2 or Type 3
      Sequence attribute may be sent with zero length.

   4. In particular, the conditionality constraint "Required if
      <name-of-parent-sequence-attribute> is sent" on the Type 1C or
      Type 2C Data Elements subsidiary to a Type 2 or 3 Sequence
      attribute does not imply that an Item must be present in the
      Sequence. These conditions are meant to be equivalent to "Required
      if a Sequence Item is present", and the conditionality is not
      strictly necessary. Any Type 2 or Type 3 Sequence attribute may be
      sent with zero length.

.. _sect_7.5:

Nesting of Data Sets
--------------------

The VR identified "SQ" shall be used for Data Elements with a Value
consisting of a Sequence of zero or more Items, where each Item contains
a set of Data Elements. SQ provides a flexible encoding scheme that may
be used for simple structures of repeating sets of Data Elements, or the
encoding of more complex Information Object Definitions often called
folders. SQ Data Elements can also be used recursively to contain
multi-level nested structures.

Items present in an SQ Data Element shall be an ordered set where each
Item may be referenced by its ordinal position. Each Item shall be
implicitly assigned an ordinal position starting with the value 1 for
the first Item in the Sequence, and incremented by 1 with each
subsequent Item. The last Item in the Sequence shall have an ordinal
position equal to the number of Items in the Sequence.

.. note::

   1. This clause implies that item ordering is preserved during
      transfer and storage.

   2. An IOD or Module Definition may choose to not use this ordering
      property of a Data Element with VR of SQ. This is simply done by
      not specifying any specific semantics to the ordering of Items, or
      by not specifying usage of the referencing of Items by ordering
      position.

The definition of the Data Elements encapsulated in each Item is
provided by the specification of the Data Element (or associated
Attribute) of Value Representation SQ. Items in a sequence of Items may
or may not contain the same set of Data Elements. Data Elements with a
VR of SQ may contain multiple Items but shall always have a Value
Multiplicity of one (i.e., a single Sequence).

There are three special SQ related Data Elements that are not ruled by
the VR encoding rules conveyed by the Transfer Syntax. They shall be
encoded as Implicit VR. These special Data Elements are Item
(FFFE,E000), Item Delimitation Item (FFFE,E00D), and Sequence
Delimitation Item (FFFE,E0DD). However, the Data Set within the Value
Field of the Data Element Item (FFFE,E000) shall be encoded according to
the rules conveyed by the Transfer Syntax.

.. _sect_7.5.1:

Item Encoding Rules
~~~~~~~~~~~~~~~~~~~

Each Item of a Data Element of Value Representation SQ shall be encoded
as a DICOM Standard Data Element with a specific Data Element Tag of
Value (FFFE,E000). The Item Tag is followed by a 4 byte Item Length
field encoded in one of the following two ways:

a. Explicit Length: The number of bytes (even) contained in the Sequence
   Item Value (following but not including the Item Length Field) is
   encoded as a 32-bit unsigned integer value (see `Data
   Elements <#sect_7.1>`__). This length shall include the total length
   of all Data Elements conveyed by this Item. This Item Length shall be
   equal to 00000000H if the Item contains no Data Set.

b. Undefined Length: The Item Length Field shall contain the value
   FFFFFFFFH to indicate an undefined Item length. It shall be used in
   conjunction with an Item Delimitation Data Element. This Item
   Delimitation Data Element has a Data Element Tag of (FFFE,E00D) and
   shall follow the Data Elements encapsulated in the Item. No Value
   shall be present in the Item Delimitation Data Element and its Length
   shall be 00000000H. An Item containing no Data Set is encoded by an
   Item Delimitation Data Element only.

The encoder of a Data Set may choose either one of the two ways of
encoding. Both ways of encoding shall be supported by decoders of Data
Sets. Data Element Tags (FFFF,eeee) are reserved by this Standard and
shall not be used.

Each Item Value shall contain a DICOM Data Set composed of Data
Elements. Within the context of each Item, these Data Elements shall be
ordered by increasing Data Element Tag value and appear only once (as
Data Set is defined in `Data Elements <#sect_7.1>`__). There is no
relationship between the ordering of the Data Elements contained within
an Item and the ordering of the Data Element Tag of SQ Value
Representation that contains that Item. One or more Data Elements in an
Item may be of Value Representation SQ, thus allowing for recursion.

Data Elements with a group of 0000, 0002 and 0006 shall not be present
within Sequence Items.

.. note::

   The use of Transfer Syntax UID (0002,0010) in particular is
   forbidden, since were it to differ from the Transfer Syntax of the
   enclosing Data Set then a change in encoding would be implied, which
   is not allowed.

`Private Data Elements <#sect_7.8>`__ specifies rules for incorporating
Private Data Elements into Sequence Items.

.. _sect_7.5.2:

Delimitation of The Sequence of Items
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

Delimitation of the last Item of a Sequence of Items, encapsulated in a
Data Element of Value Representation SQ, shall be in one of the two
following ways:

a. Explicit Length: The number of bytes (even) contained in the Data
   Element Value (following but not including the Data Element Length
   Field) is encoded as a 32-bit unsigned integer value (see `Data
   Elements <#sect_7.1>`__). This length shall include the total length
   resulting from the sequence of zero or more items conveyed by this
   Data Element. This Data Element Length shall be equal to 00000000H if
   the sequence of Items contains zero Items.

b. Undefined Length: The Data Element Length Field shall contain a Value
   FFFFFFFFH to indicate an Undefined Sequence length. It shall be used
   in conjunction with a Sequence Delimitation Item. A Sequence
   Delimitation Item shall be included after the last Item in the
   sequence. Its Item Tag shall be (FFFE,E0DD) with an Item Length of
   00000000H. No Value shall be present. A Sequence containing zero
   Items is encoded by a Sequence Delimitation Item only.

The encoder of a Sequence of Items may choose either one of the two ways
of encoding. Both ways of encoding shall be supported by decoders of the
Sequence of Items.

.. note::

   The Sequence Delimitation Item Tag (FFFE,E0DD) is different from the
   Item Delimitation Tag (FFFE,E00D) introduced above in that it
   indicates the end of a Sequence of Items whose Length was left
   undefined. If an undefined length Item is the last Item of a Sequence
   of Items of undefined length, then an Item Delimitation Tag will be
   followed by a Sequence Delimitation Tag.

For an example of an SQ Data Element of Explicit Length encapsulating
Items of Explicit Length see `table_title <#table_7.5-1>`__.

For an example of an SQ Data Element of Undefined Length encapsulating
Items of Explicit Length see `table_title <#table_7.5-2>`__.

For an example of an SQ Data Element of Undefined Length encapsulating
Items of both Explicit and Undefined Length see
`table_title <#table_7.5-3>`__.

.. table:: Example of a Data Element with Implicit VR Defined as a
Sequence of Items (VR = SQ) with Three Items of Explicit Length

   +-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+
   | *     | *     | *     |       |       |       |       |       |       |       |       |
   | *Data | *Data | *Data |       |       |       |       |       |       |       |       |
   | El    | El    | El    |       |       |       |       |       |       |       |       |
   | ement | ement | ement |       |       |       |       |       |       |       |       |
   | Tag** | Len   | Va    |       |       |       |       |       |       |       |       |
   |       | gth** | lue** |       |       |       |       |       |       |       |       |
   +=======+=======+=======+=======+=======+=======+=======+=======+=======+=======+=======+
   | (     | 0000  | **    | **S   | **    |       |       |       |       |       |       |
   | gggg, | 0F00H | First | econd | Third |       |       |       |       |       |       |
   | eeee) |       | I     | I     | I     |       |       |       |       |       |       |
   | with  |       | tem** | tem** | tem** |       |       |       |       |       |       |
   | VR of |       |       |       |       |       |       |       |       |       |       |
   | SQ    |       |       |       |       |       |       |       |       |       |       |
   +-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+
   | Item  | Item  | Item  | Item  | Item  | Item  | Item  | Item  | Item  |       |       |
   | Tag   | L     | Value | Tag   | L     | Value | Tag   | L     | Value |       |       |
   | (     | ength | Data  | (     | ength | Data  | (     | ength | Data  |       |       |
   | FFFE, | 0000  | Set   | FFFE, | 0000  | Set   | FFFE, | 0000  | Set   |       |       |
   | E000) | 04F8H |       | E000) | 04F8H |       | E000) | 04F8H |       |       |       |
   +-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+
   | 4     | 4     | 4     | 4     | 04F8H | 4     | 4     | 04F8H | 4     | 4     | 04F8H |
   | bytes | bytes | bytes | bytes | bytes | bytes | bytes | bytes | bytes | bytes | bytes |
   +-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+

.. table:: Example of a Data Element with Explicit VR Defined as a
Sequence of Items (VR = SQ) of Undefined Length, Containing Two Items of
Explicit Length

   +-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+
   | *     | **    | *     | *     |       |       |       |       |       |       |       |       |
   | *Data | Value | *Data | *Data |       |       |       |       |       |       |       |       |
   | El    | R     | El    | El    |       |       |       |       |       |       |       |       |
   | ement | epres | ement | ement |       |       |       |       |       |       |       |       |
   | Tag** | entat | Len   | Va    |       |       |       |       |       |       |       |       |
   |       | ion** | gth** | lue** |       |       |       |       |       |       |       |       |
   +=======+=======+=======+=======+=======+=======+=======+=======+=======+=======+=======+=======+
   | (     | SQ    | 0000H | FFFF  | **    | **S   | **Seq |       |       |       |       |       |
   | gggg, |       | Res   | FFFFH | First | econd | uence |       |       |       |       |       |
   | eeee) |       | erved | unde  | I     | I     | De    |       |       |       |       |       |
   | with  |       |       | fined | tem** | tem** | limit |       |       |       |       |       |
   | VR of |       |       | l     |       |       | ation |       |       |       |       |       |
   | SQ    |       |       | ength |       |       | I     |       |       |       |       |       |
   |       |       |       |       |       |       | tem** |       |       |       |       |       |
   +-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+
   | Item  | Item  | Item  | Item  | Item  | Item  | Seq.  | Item  |       |       |       |       |
   | Tag   | L     | Value | Tag   | L     | Value | D     | L     |       |       |       |       |
   | (     | ength | Data  | (     | ength | Data  | elim. | ength |       |       |       |       |
   | FFFE, | 98A5  | Set   | FFFE, | B321  | Set   | Tag   | 0000  |       |       |       |       |
   | E000) | 2C68H |       | E000) | 762CH |       | (     | 0000H |       |       |       |       |
   |       |       |       |       |       |       | FFFE, |       |       |       |       |       |
   |       |       |       |       |       |       | E0DD) |       |       |       |       |       |
   +-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+
   | 4     | 2     | 2     | 4     | 4     | 4     | 98A5  | 4     | 4     | B321  | 4     | 4     |
   | bytes | bytes | bytes | bytes | bytes | bytes | 2C68H | bytes | bytes | 762CH | bytes | bytes |
   |       |       |       |       |       |       | bytes |       |       | bytes |       |       |
   +-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+

.. note::

   The Data Set within the Item Values in `table_title <#table_7.5-2>`__
   have VRs Explicitly defined.

.. table:: Example of a Data Element with Implicit VR Defined as a
Sequence of Items (VR = SQ) of Undefined Length, Containing Two Items
Where One Item is of Explicit Length and the Other Item is of Undefined
Length

   +-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+
   | *     | *     | *Data |       |       |       |       |       |       |       |       |       |
   | *Data | *Data | El    |       |       |       |       |       |       |       |       |       |
   | El    | El    | ement |       |       |       |       |       |       |       |       |       |
   | ement | ement | V     |       |       |       |       |       |       |       |       |       |
   | Tag** | Len   | alue* |       |       |       |       |       |       |       |       |       |
   |       | gth** |       |       |       |       |       |       |       |       |       |       |
   +=======+=======+=======+=======+=======+=======+=======+=======+=======+=======+=======+=======+
   | (     | FFFF  | **    | **S   | **Seq |       |       |       |       |       |       |       |
   | gggg, | FFFFH | First | econd | uence |       |       |       |       |       |       |       |
   | eeee) | unde  | I     | I     | De    |       |       |       |       |       |       |       |
   | with  | fined | tem** | tem** | limit |       |       |       |       |       |       |       |
   | VR of | l     |       |       | ation |       |       |       |       |       |       |       |
   | SQ    | ength |       |       | I     |       |       |       |       |       |       |       |
   |       |       |       |       | tem** |       |       |       |       |       |       |       |
   +-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+
   | Item  | Item  | Item  | Item  | Item  | Item  | Item  | L     | Seq.  | Item  |       |       |
   | Tag   | L     | Value | Tag   | L     | Value | D     | ength | D     | L     |       |       |
   | (     | ength | Data  | (     | ength | Data  | elim. | 0000  | elim. | ength |       |       |
   | FFFE, | 0000  | Set   | FFFE, | FFFF  | Set   | Tag   | 0000H | Tag   | 0000  |       |       |
   | E000) | 17B6H |       | E000) | FFFFH |       | (     |       | (     | 0000H |       |       |
   |       |       |       |       | unde  |       | FFFE, |       | FFFE, |       |       |       |
   |       |       |       |       | fined |       | E00D) |       | E0DD) |       |       |       |
   |       |       |       |       | l     |       |       |       |       |       |       |       |
   |       |       |       |       | ength |       |       |       |       |       |       |       |
   +-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+
   | 4     | 4     | 4     | 4     | 17B6H | 4     | 4     | unde  | 4     | 4     | 4     | 4     |
   | bytes | bytes | bytes | bytes | bytes | bytes | bytes | fined | bytes | bytes | bytes | bytes |
   |       |       |       |       |       |       |       | l     |       |       |       |       |
   |       |       |       |       |       |       |       | ength |       |       |       |       |
   +-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+

.. _sect_7.5.3:

Sequence Inheritance
~~~~~~~~~~~~~~~~~~~~

An encapsulated Data Set shall only include the Specific Character Set
(0008,0005) data element if the Attribute Specific Character Set is
defined in the IOD for that sequence of items.

.. note::

   An encapsulated Data Set does not include the Specific Character Set
   data element unless the Specific Character Set Attribute is defined
   as part of the IOD for that sequence.

If an encapsulated Data Set includes the Specific Character Set
Attribute, it shall apply only to the encapsulated Data Set. If the
Attribute Specific Character Set is not explicitly included in an
encapsulated Data Set, then the Specific Character Set value of the
encapsulating Data Set applies.

.. _sect_7.6:

Repeating Groups
----------------

Multiple Overlay Planes and Curves are often associated with a single
Image (see ). Standard Data Elements with even Group Numbers
(5000-501E,eeee) represent Curves, while elements with even Group
Numbers (6000-601E,eeee) represent Overlay Planes. Both of these ranges
of Group numbers are known as Repeating Groups. This use of group
numbers is a remnant of older versions of this Standard, which
associated a semantic meaning with particular Groups.

In each of these ranges of Group Numbers, Standard Data Elements that
have identical Element Numbers have the same meaning within each Group
(and the same VR, VM, and Data Element Type). The notation (50xx,eeee)
and (60xx,eeee) are used for the Group Number in Data Element Tags when
referring to a common Data Element across these groups (see ). Groups
(50xx,eeee) and (60xx,eeee) are called Repeating Groups because of these
characteristics.

Repeating Groups shall only be allowed in the even Groups
(6000-601E,eeee) and even Groups (5000-501E,eeee) cases. In the future,
Data Elements with VRs of SQ shall be used to serve a similar purpose.

.. note::

   Private Groups in the odd Groups (5001-501F,eeee) and
   (6001-601F,eeee) may still be used, but there is no implication of
   repeating semantics, nor any implied shadowing of the standard
   repeating groups.

.. _sect_7.7:

Retired Data Elements
---------------------

Certain Data Elements are no longer supported in the current Standard.
These Data Elements are retired and are denoted as such (RET) in the VR
column in . Implementations may continue to support these Data Elements
for the purpose of backward compatibility with older versions of this
Standard, but this is not a requirement of the current Standard. If a
retired Data Element is used it must contain valid data as specified in
older versions of this Standard. Any other use of a retired Data
Element, and its associated Data Element Tag, is reserved by this
Standard. Retired Data Element Tags shall not be redefined in later
versions of this Standard.

.. _sect_7.8:

Private Data Elements
---------------------

Implementations may require communication of information that cannot be
contained in Standard Data Elements. Private Data Elements are intended
to be used to contain such information. Such Private Data Elements shall
not change the semantics of the Information Object Definition or SOP
Class Definition.

Private Data Elements have the same structure as Standard Data Elements
specified earlier in `Data Elements <#sect_7.1>`__ (i.e., Data Element
Tag field, optional VR field, length field, and value field). The Group
Number used in the Element Tag of Private Data Elements shall be an odd
number. Private Data Elements shall be contained in the Data Set in
increasing numeric order of Data Element Tag. The Value Field of a
Private data element shall have one of the VRs specified by this
Standard in `Value Representation (VR) <#sect_6.2>`__.

For each Information Object Definition or SOP Class Definition, certain
Data Elements are required (Data Element Type 1, 1C, 2, or 2C) as
specified in and . Private Data Elements shall not be used in place of
required Standard Data Elements.

.. _sect_7.8.1:

Private Data Element Tags
~~~~~~~~~~~~~~~~~~~~~~~~~

It is possible that multiple implementers may define Private Elements
with the same (odd) group number. To avoid conflicts, Private Elements
shall be assigned Private Data Element Tags according to the following
rules.

a. Private Creator Data Elements numbered (gggg,0010-00FF) (gggg is odd)
   shall be used to reserve a block of Elements with Group Number gggg
   for use by an individual implementer. The implementer shall insert an
   identification code in the first unused (unassigned) Element in this
   series to reserve a block of Private Elements. The VR of the private
   identification code shall be LO (Long String) and the VM shall be
   equal to 1. A Private Creator identifier may be used only once within
   a Group; reserving multiple blocks of Elements in the same Group with
   the same identifier is not allowed. The Private Creator Data Elements
   shall only contain characters from the Default Character Repertoire
   and not an Extended or Replacement Character Repertoire, even though
   the LO VR is one that is affected by the Specific Character Set
   (0008,0005).

   .. note::

      1. If an implementer needs multiple repetitions of a private
         element, a private Sequence attribute (see `Nesting of Data
         Sets <#sect_7.5>`__) may be used to contain these multiple
         items.

      2. An implementer may use the same Private Creator identifier for
         multiple Groups.

b. Private Creator Data Element (gggg,0010), is a Type 1 Data Element
   that identifies the implementer reserving element (gggg,1000-10FF),
   Private Creator Data Element (gggg,0011) identifies the implementer
   reserving elements (gggg,1100-11FF), and so on, until Private Creator
   Data Element (gggg,00FF) identifies the implementer reserving
   elements (gggg,FF00-FFFF).

c. Encoders of Private Data Elements shall be able to dynamically assign
   private data to any available (unreserved) block(s) within the
   Private group, and specify this assignment through the blocks
   corresponding Private Creator Data Element(s). Decoders of Private
   Data shall be able to accept reserved blocks with a given Private
   Creator identification code at any position within the Private group
   specified by the blocks corresponding Private Creator Data Element.

   .. note::

      1. Older versions of this Standard described shadow groups. These
         were groups with a group number one greater than the standard
         groups. Elimination of conflicts in Private Data Element Tags
         have made this distinction obsolete and this terminology has
         been retired.

      2. Older versions of this Standard specified private group element
         numbers (gggg,10FF-7FFF) reserved for manufacturers and private
         group element numbers (gggg, 8100-FFFF) reserved for users.
         Elimination of conflicts in Private Data Element Tags has made
         this distinction obsolete and this specification has been
         retired.

      3. The requirements of this section do not allow any use of
         elements in the ranges (gggg,0001-000F) and (gggg,0100-0FFF)
         where gggg is odd.

d. Elements with Tags (0001,xxxx), (0003,xxxx), (0005,xxxx), (0007,xxxx)
   and (FFFF,xxxx) shall not be used.

e. Whether or not Private Data Elements contain identifying information
   related to de-identification is defined by the Private Data Element
   Characteristics Sequence (0008,0300). See .

f. Data Elements numbered (gggg,0000), where gggg is odd, were Group
   Length Elements, which have been retired, See `Group
   Length <#sect_7.2>`__.

Since each Item within a sequence is a self contained Data Set (see
`Nesting of Data Sets <#sect_7.5>`__ on the nesting of Data Sets via
Sequences of Items), any Item that contains Private Data Elements shall
also have Private Creator Data Elements reserving blocks of Elements for
those Private Data Elements. The scope of the reservation is just within
the Item. Items do not inherit the Private Data Element reservations
made by Private Creator Data Elements in the Data Set in which the Item
is nested.

.. note::

   1. If a sequence is itself a Private Data Element and the Items
      within the sequence also have Private Data Elements, then there
      will be Private Creator Data Elements both outside the sequence
      and within the sequence Items.

   2. Different Items may reserve the same block of Private Data
      Elements for different private creators. This is necessary to
      allow the nesting of Data Sets collected from multiple sources
      into folders.

   3. The recommended convention for referencing a Private Data Element
      is (gggg,xxee,"pcde"), where gggg is the group number, xx is the
      string “xx”, ee is the element number within a reserved block, and
      pcde is the quoted value of the Private Creator Data Element that
      reserved the block, e.g., (0029,xx43,"Acme_CT_Parameters").
      Alternatively, when a block of Private Data Elements is being
      described, one may factor out the description of the Private
      Creator Data Element value, e.g., Private Creator Data Element
      (0029,00xx) = "Acme_CT_Parameters", and (0029,xx43), (0029,xx44),
      etc.

.. _sect_7.8.2:

Encoding of Private Elements
~~~~~~~~~~~~~~~~~~~~~~~~~~~~

The Value Representations used for Private Data Elements shall be the
same as those VRs specified for Standard Data Elements in `Value
Representation (VR) <#sect_6.2>`__. The encoding shall conform to the
requirements for those VRs and shall be in accordance with the
negotiated Transfer Syntax. A Private Data Element with SQ VR (a Private
Data Sequence) may include Items with both Standard and Private Data
Elements. Standard Data Elements used within a Private Data Sequence
shall use the VRs as defined in for those data elements.

The semantics of Standard Data Elements within a Private Data Sequence,
and the definition of Attribute Values, are implementation dependent.

For a Standard Extended SOP Class the Attributes Pixel Data (7FE0,0010),
Float Pixel Data (7FE0,0008), Double Float Pixel Data (7FE0,0009),
Waveform Data (5400,1010) and Overlay Data (60xx,3000) shall not be
included within a Private Sequence Item, nor within a standard Sequence
Item nested directly or indirectly within a Private Sequence Item.

