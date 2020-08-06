.. _chapter_3:

Definitions
===========

For the purposes of this Standard, the following definitions apply.

Application Entity
   See `biblioentry_title <#biblio_ISO7498>`__.

OSI Presentation Protocol
   See `biblioentry_title <#biblio_ISO7498>`__.

Association
   See `biblioentry_title <#biblio_ISO8649>`__.

Presentation Context
   See `biblioentry_title <#biblio_ISO8822>`__.

Presentation Data Value
   See `biblioentry_title <#biblio_ISO8822>`__.

Transfer Syntax
   See `biblioentry_title <#biblio_ISO8822>`__.

Transfer Syntax Name
   See `biblioentry_title <#biblio_ISO8822>`__.

OSI Object Identification
   See `biblioentry_title <#biblio_ISOIEC8824>`__.

Attribute
   .

Command Element
   .

Data Dictionary
   .

Service-Object Pair Class

Conformance Statement
   .

Attribute Tag
   .

Information Entity
   .

Information Object Definition
   .

Multi-frame Image
   .

Service-Object Pair Instance

DICOM Upper Layer Service
   .

Basic Offset Table
   A table of 32-bit pointers to individual frames of an encapsulated
   Multi-frame Image.

Big Endian
   A form of byte ordering where multiple byte binary values are encoded
   with the most significant byte encoded first, and the remaining bytes
   encoded in decreasing order of significance.

Character Repertoire
   A finite set of different characters that is considered to be
   complete for a given purpose and is specified independently of their
   encoding (also referred to as a character set).

Code String
   A string of characters identifying a controlled concept, including
   Defined Terms and Enumerated Values when represented as character
   strings. The scope of the controlled concept is limited to the
   attribute for which the string provides the value; i.e., the
   attribute defines the allowed set of values for the Code String, and
   a particular string may have different meanings in different
   attributes. A Code String is formally an arbitrary code representing
   a semantic concept; however, English language words (using the
   constrained character set of the CS Value Representation) are often
   used as codes for the semantics of those words.

Data Element
   A unit of information as defined by a single entry in the data
   dictionary. An encoded Information Object Definition (IOD) Attribute
   that is composed of, at a minimum, three fields: a Data Element Tag,
   a Value Length, and a Value Field. For some specific Transfer
   Syntaxes, a Data Element also contains a VR Field where the Value
   Representation of that Data Element is specified explicitly.

Data Element Tag
   A unique identifier for a Data Element composed of an ordered pair of
   numbers (a Group Number followed by an Element Number).

Data Element Type
   Used to specify whether an Attribute of an Information Object
   Definition or an Attribute of a SOP Class Definition is mandatory,
   mandatory only under certain conditions, or optional. This translates
   to whether a Data Element of a Data Set is mandatory, mandatory only
   under certain conditions, or optional.

Data Set
   Exchanged information consisting of a structured set of Attribute
   values directly or indirectly related to Information Objects. The
   value of each Attribute in a Data Set is expressed as a Data Element.
   A collection of Data Elements ordered by increasing Data Element Tag
   number that is an encoding of the values of Attributes of a real
   world object.

Defined Term
   The Value of a Data Element is a Defined Term when the Value of the
   element may be one of an explicitly specified set of standard values,
   and these values may be extended by implementers.

Element Number
   The second number in the ordered pair of numbers that makes up a Data
   Element Tag.

Enumerated Value
   The Value of a Data Element is an Enumerated Value when the value of
   the element must be one of an explicitly specified set of standard
   values, and these values shall not be extended by implementers.

Extended Offset Table
   A table of 64-bit pointers to individual frames of an encapsulated
   Multi-frame Image.

Group Number
   The first number in the ordered pair of numbers that makes up a Data
   Element Tag.

Item
   A component of the Value of a Data Element that is of Value
   Representation Sequence of Items. An Item contains a Data Set.

Item Delimitation Data Element
   Used to mark the end of an Item of Undefined Length in a Sequence of
   Items. This is the last Data Element in an Item of Undefined Length.

Little Endian
   A form of byte ordering where multiple byte binary values are encoded
   with the least significant byte encoded first; and the remaining
   bytes encoded in increasing order of significance.

Nested Data Set
   A Data Set contained within a Data Element of another Data Set. Data
   Sets can be nested recursively. Only Data Elements with Value
   Representation Sequence of Items may, themselves, contain Data Sets.

Pixel Cell
   The container for a single Pixel Sample Value that may include unused
   bits. The size of a Pixel Cell shall be specified by the Bits
   Allocated (0028, 0100) Data Element.

Pixel Data
   Graphical data (e.g., images) of variable pixel-depth encoded in the
   Pixel Data, Float Pixel Data or Double Float Pixel Data Element.

Pixel Sample Value
   A value associated with an individual pixel. An individual pixel
   consists of one or more Pixel Sample Values (e.g., color images).

Private Data Element
   Additional Data Element, defined by an implementer, to communicate
   information that is not contained in Standard Data Elements. Private
   Data elements have odd Group Numbers.

Repeating Group
   Standard Data Elements within a particular range of Group Numbers
   where elements that have identical Element Numbers have the same
   meaning within each Group (and the same VR, VM, and Data Element
   Type). Repeating Groups shall only exist for Curves and Overlay
   Planes (Group Numbers (50xx,eeee) and (60xx,eeee), respectively) and
   are a remnant of older versions of this Standard.

Retired Data Element
   A Data Element that is unsupported beginning with the current
   Standard. Implementations may continue to support Retired Data
   Elements for the purpose of backward compatibility, but this is not a
   requirement of the current Standard.

Sequence Delimitation Item
   Item used to mark the end of a Sequence of Items of Undefined Length.
   This Item is the last Item in a Sequence of Items of Undefined
   Length.

Sequence of Items
   A Value Representation for Data Elements that contain a sequence of
   Data Sets. Sequence of Items allows for Nested Data Sets.

Standard Data Element
   A Data Element defined in the DICOM Standard, and therefore listed in
   the DICOM Data Element Dictionary in .

DICOM Transfer Syntax
   A set of encoding rules that allow DICOM Application Entities to
   unambiguously negotiate the encoding techniques (e.g., Data Element
   structure, byte ordering, compression) they are able to support,
   thereby allowing these Application Entities to communicate. See also
   `Transfer Syntax <#glossentry_TransferSyntax>`__.

Undefined Length
   The ability to specify an unknown length for a Data Element Value (of
   Value Representation SQ, UN, OW, or OB) or Item. Data Elements and
   Items of Undefined Length are delimited with Sequence Delimitation
   Items and Item Delimiter Data Elements, respectively.

Unique Identifier
   A string of characters used to provide global unique identification
   of a wide variety of items, guaranteeing uniqueness across multiple
   countries, sites, vendors and equipment. It uses the structure
   defined by `biblioentry_title <#biblio_ISOIEC8824>`__ for OSI Object
   Identifiers.

Value
   A component of a Value Field. A Value Field may consist of one or
   more of these components.

Value Field
   The field within a Data Element that contains the Value(s) of that
   Data Element.

Value Length
   The field within a Data Element that contains the length of the Value
   Field of the Data Element.

Value Multiplicity
   Specifies the number of Values contained in the Value Field of a Data
   Element.

Value Representation
   Specifies the data type and format of the Value(s) contained in the
   Value Field of a Data Element.

Value Representation Field
   The field where the Value Representation of a Data Element is stored
   in the encoding of a Data Element structure with explicit VR.

Coded Character Set
   See `biblioentry_title <#biblio_ISOIEC2022>`__.

Code Extension
   See `biblioentry_title <#biblio_ISOIEC2022>`__.

Control Character
   See `biblioentry_title <#biblio_ISOIEC2022>`__.

To Designate
   See `biblioentry_title <#biblio_ISOIEC2022>`__.

Escape Sequence
   See `biblioentry_title <#biblio_ISOIEC2022>`__.

Graphic Character
   See `biblioentry_title <#biblio_ISOIEC2022>`__.

To Invoke
   See `biblioentry_title <#biblio_ISOIEC2022>`__.

