.. _chapter_F:

DICOM JSON Model
================

.. _sect_F.1:

Introduction to JavaScript Object Notation (JSON)
-------------------------------------------------

JSON is a text-based open standard, derived from JavaScript, for
representing data structures and associated arrays. It is
language-independent, and primarily used for serializing and
transmitting lightweight structured data over a network connection. It
is described in detail by the Internet Engineering Task Force (IETF) in
`biblioentry_title <#biblio_RFC_4627>`__, available at
http://www.ietf.org/rfc/rfc4627.txt.

The DICOM JSON Model complements the XML-based Native DICOM Model, by
providing a lightweight representation of data returned by DICOM web
services. While this representation can be used to encode any type of
DICOM Data Set it is expected to be used by client applications,
especially mobile clients, such as described in the QIDO-RS use cases
(see ).

With the exception of padding to even byte length, a data source that is
creating a new instance of a DICOM JSON Model shall follow the DICOM
encoding rules in creating Values for the DICOM Attributes within the
instance of the DICOM JSON Model. Attribute Values encoded in a DICOM
JSON Model are not required to be padded to an even byte length.

A data recipient that converts data from an instance of the DICOM JSON
Model back into a binary encoded DICOM object shall adjust the padding
to an even byte length as necessary to meet the encoding rules specified
in .

.. _sect_F.2:

DICOM JSON Model
----------------

The DICOM JSON Model follows the Native DICOM Model for XML very
closely, so that systems can take advantage of both formats without much
retooling. The Media Type for DICOM JSON is application/dicom+json. The
default character repertoire shall be UTF-8 / ISO_IR 192.

.. _sect_F.2.1:

Multiple Results Structure
~~~~~~~~~~~~~~~~~~~~~~~~~~

Multiple results returned in JSON are organized as a single top-level
array of JSON objects. This differs from the Native DICOM Model, which
returns multiple results as a multi-part collection of singular XML
documents.

.. _sect_F.2.1.1:

Examples
^^^^^^^^

.. _sect_F.2.1.1.1:

Native DICOM Model
''''''''''''''''''

::

   <?xml version="1.0" encoding="UTF-8" xml:space="preserve" ?>
   <NativeDicomModel>
     <DicomAttribute tag="0020000D" vr="UI" keyword="StudyInstanceUID">
       <Value number="1">1.2.392.200036.9116.2.2.2.1762893313.1029997326.945873</Value>
     </DicomAttribute>
   </NativeDicomModel>
   …
   <?xml version="1.0" encoding="UTF-8" xml:space="preserve" ?>
   <NativeDicomModel>
     <DicomAttribute tag="0020000D" vr="UI" keyword="StudyInstanceUID">
       <Value number="1">1.2.444.200036.9116.2.2.2.1762893313.1029997326.945876</Value>
     </DicomAttribute>
   </NativeDicomModel>

.. _sect_F.2.1.1.2:

DICOM JSON Model
''''''''''''''''

::

   [
     {
        "0020000D": {
         "vr": "UI",
         "Value": [ "1.2.392.200036.9116.2.2.2.1762893313.1029997326.945873" ]
       }
     },
     {
       "0020000D" : {
         "vr": "UI",
         "Value": [ "1.2.392.200036.9116.2.2.2.2162893313.1029997326.945876" ]
       }
     }
   ]

.. _sect_F.2.2:

DICOM JSON Model Object Structure
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

The DICOM JSON Model object is a representation of a DICOM Data Set.

The internal structure of the DICOM JSON Model object is a sequence of
objects representing attributes within the DICOM Data Set.

Attribute objects within a DICOM JSON Model object must be ordered by
their property name in ascending order.

Group Length (gggg,0000) attributes shall not be included in a DICOM
JSON Model object.

The name of each attribute object is:

-  The eight character uppercase hexadecimal representation of a DICOM
   Tag

Each attribute object contains the following named child objects:

-  vr: A string encoding the DICOM Value Representation. The mapping
   between DICOM Value Representations and JSON Value Representations is
   described in `DICOM JSON Value Representation <#sect_F.2.3>`__.

-  At most one of:

   -  Value: An array containing one of:

      -  The Value Field elements of a DICOM attribute with a VR other
         than PN, SQ, OB, OD, OF, OL, OV, OW, or UN (described in `DICOM
         JSON Value Multiplicity <#sect_F.2.4>`__)

         The encoding of empty Value Field elements is described in
         `DICOM JSON Model Null Values <#sect_F.2.5>`__

      -  The Value Field elements of a DICOM attribute with a VR of PN.
         The non-empty name components of each element are encoded as a
         JSON strings with the following names:

         -  Alphabetic

         -  Ideographic

         -  Phonetic

      -  JSON DICOM Model objects corresponding to the sequence items of
         an attribute with a VR of SQ

         Empty sequence items are represented by empty objects

   -  BulkDataURI: A string encoding the WADO-RS URL of a bulk data item
      describing the Value Field of an enclosing Attribute with a VR of
      DS, FL, FD, IS, LT, OB, OD, OF, OL, OV, OW, SL, SS, ST, SV, UC,
      UL, UN, US, UT or UV (described in `BulkDataURI <#sect_F.2.6>`__)

   -  InlineBinary: A base64 string encoding the Value Field of an
      enclosing Attribute with a VR of OB, OD, OF, OL, OV, OW, or UN
      (described in `InlineBinary <#sect_F.2.7>`__)

.. note::

   1. For Private Data Elements, the group and element numbers will
      follow the rules specified in

   2. The person name representation is more closely aligned with the
      DICOM Data Element representation than the DICOM XML
      representation.

.. _sect_F.2.3:

DICOM JSON Value Representation
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

The DICOM Value Representation (VR) is included in each DICOM JSON Model
attribute object and named "vr". For example:

::

   "vr": "CS"

The JSON encoding of an Attribute shall use the JSON Data Type
corresponding to the DICOM Value Representations in
`table_title <#table_F.2.3-1>`__. The JSON encodings shall conform to
the Definition, Character Repertoire (if applicable) and Length of Value
specified for that DICOM Value Representation (see ) with the following
exceptions:

-  Attributes with a Value Representation of AT shall be restricted to
   eight character uppercase hexadecimal representation of a DICOM Tag

.. table:: DICOM VR to JSON Data Type Mapping

   +-------------+--------------------------+--------------------------+
   | **VR Name** | **Type**                 | **JSON Data Type**       |
   +=============+==========================+==========================+
   | AE          | Application Entity       | String                   |
   +-------------+--------------------------+--------------------------+
   | AS          | Age String               | String                   |
   +-------------+--------------------------+--------------------------+
   | AT          | Attribute Tag            | String                   |
   +-------------+--------------------------+--------------------------+
   | CS          | Code String              | String                   |
   +-------------+--------------------------+--------------------------+
   | DA          | Date                     | String                   |
   +-------------+--------------------------+--------------------------+
   | DS          | Decimal String           | Number or String         |
   |             |                          |                          |
   |             |                          | See note.                |
   +-------------+--------------------------+--------------------------+
   | DT          | Date Time                | String                   |
   +-------------+--------------------------+--------------------------+
   | FL          | Floating Point Single    | Number                   |
   +-------------+--------------------------+--------------------------+
   | FD          | Floating Point Double    | Number                   |
   +-------------+--------------------------+--------------------------+
   | IS          | Integer String           | Number or String         |
   |             |                          |                          |
   |             |                          | See note.                |
   +-------------+--------------------------+--------------------------+
   | LO          | Long String              | String                   |
   +-------------+--------------------------+--------------------------+
   | LT          | Long Text                | String                   |
   +-------------+--------------------------+--------------------------+
   | OB          | Other Byte               | Base64 encoded           |
   |             |                          | octet-stream             |
   +-------------+--------------------------+--------------------------+
   | OD          | Other Double             | Base64 encoded           |
   |             |                          | octet-stream             |
   +-------------+--------------------------+--------------------------+
   | OF          | Other Float              | Base64 encoded           |
   |             |                          | octet-stream             |
   +-------------+--------------------------+--------------------------+
   | OL          | Other Long               | Base64 encoded           |
   |             |                          | octet-stream             |
   +-------------+--------------------------+--------------------------+
   | OV          | Other 64-bit Very Long   | Base64 encoded           |
   |             |                          | octet-stream             |
   +-------------+--------------------------+--------------------------+
   | OW          | Other Word               | Base64 encoded           |
   |             |                          | octet-stream             |
   +-------------+--------------------------+--------------------------+
   | PN          | Person Name              | Object containing Person |
   |             |                          | Name component groups as |
   |             |                          | strings (see `DICOM JSON |
   |             |                          | Model Object             |
   |             |                          | Str                      |
   |             |                          | ucture <#sect_F.2.2>`__) |
   +-------------+--------------------------+--------------------------+
   | SH          | Short String             | String                   |
   +-------------+--------------------------+--------------------------+
   | SL          | Signed Long              | Number                   |
   +-------------+--------------------------+--------------------------+
   | SQ          | Sequence of Items        | Array containing DICOM   |
   |             |                          | JSON Objects             |
   +-------------+--------------------------+--------------------------+
   | SS          | Signed Short             | Number                   |
   +-------------+--------------------------+--------------------------+
   | ST          | Short Text               | String                   |
   +-------------+--------------------------+--------------------------+
   | SV          | Signed 64-bit Very Long  | Number or String         |
   |             |                          |                          |
   |             |                          | See Note.                |
   +-------------+--------------------------+--------------------------+
   | TM          | Time                     | String                   |
   +-------------+--------------------------+--------------------------+
   | UC          | Unlimited Characters     | String                   |
   +-------------+--------------------------+--------------------------+
   | UI          | Unique Identifier (UID)  | String                   |
   +-------------+--------------------------+--------------------------+
   | UL          | Unsigned Long            | Number                   |
   +-------------+--------------------------+--------------------------+
   | UN          | Unknown                  | Base64 encoded           |
   |             |                          | octet-stream             |
   +-------------+--------------------------+--------------------------+
   | UR          | Universal Resource       | String                   |
   |             | Identifier or Universal  |                          |
   |             | Resource Locator         |                          |
   |             | (URI/URL)                |                          |
   +-------------+--------------------------+--------------------------+
   | US          | Unsigned Short           | Number                   |
   +-------------+--------------------------+--------------------------+
   | UT          | Unlimited Text           | String                   |
   +-------------+--------------------------+--------------------------+
   | UV          | Unsigned 64-bit Very     | Number or String.        |
   |             | Long                     |                          |
   |             |                          | See Note.                |
   +-------------+--------------------------+--------------------------+

.. note::

   For IS, DS, SV and UV, a JSON String representation can be used to
   preserve the original format during transformation of the
   representation, or if needed to avoid losing precision of a decimal
   string.

Although data, such as dates, are represented in the DICOM JSON model as
strings, it is expected that they will be treated in the same manner as
the original attribute as defined by .

.. _sect_F.2.4:

DICOM JSON Value Multiplicity
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

The value or values of a given DICOM attribute are given in the "Value"
array. The value multiplicity (VM) is not contained in the DICOM JSON
object.

For example:

::

   "Value": [ "bar", "foo" ]

or:

::

   "Value": [ "bar" ]

.. _sect_F.2.5:

DICOM JSON Model Null Values
~~~~~~~~~~~~~~~~~~~~~~~~~~~~

If an attribute is present in DICOM but empty (i.e., Value Length is 0),
it shall be preserved in the DICOM JSON attribute object containing no
"Value", "BulkDataURI" or "InlineBinary".

If a multi-valued attribute has one or more empty values these are
represented as "null" array elements. For example:

::

   "Value": [ "bar", null, "foo" ]

If a sequence contains empty items these are represented as empty JSON
object in the array.

::

   "Value": [ { … }, { }, { … } ]

.. _sect_F.2.6:

BulkDataURI
~~~~~~~~~~~

If an attribute contains a "BulkDataURI" *,* this contains the URI of a
bulk data element as defined in .

.. _sect_F.2.7:

InlineBinary
~~~~~~~~~~~~

If an attribute contains an "InlineBinary", this contains the base64
encoding of the enclosing attribute's Value Field.

There is a single InlineBinary value representing the entire Value
Field, and not one per Value in the case where the Value Multiplicity is
greater than one. E.g., a LUT with 4096 16 bit entries that may be
encoded in DICOM with a Value Representation of OW, with a VL of 8192
and a VM of 1, or a US VR with a VL of 8192 and a VM of 4096 would both
be represented as a single InlineBinary string.

All rules (e.g., byte ordering and swapping) in DICOM apply.

.. note::

   Implementers should in particular pay attention to the rules
   regarding the value representations of OD, OF, OL and OW.

.. _sect_F.3:

Transformation with other DICOM Formats
---------------------------------------

.. _sect_F.3.1:

Native DICOM Model XML
~~~~~~~~~~~~~~~~~~~~~~

The transformation between the Native DICOM Model XML and the DICOM JSON
model cannot be done through the use of generic XML - JSON converters.

The mapping between the two formats is as follows (see also
`table_title <#table_F.3.1-1>`__):

-  The XML "NativeDicomModel" element maps to the DICOM JSON Model
   Object

-  Each "DicomAttribute" element maps to an attribute object within the
   DICOM JSON model object

   -  The "tag" attribute maps to the JSON object name

      -  The Native DICOM Model XML allows for duplicate Tag values and
         the DICOM JSON model does not. To resolve this, private
         attribute Tag values must be remapped according to the conflict
         avoidance rules specified in .

   -  The "vr" attribute maps to the "vr" child string

-  "Value" elements map to members of the "Value" child array

   -  A "Value" element with the attribute "number=n" maps to
      "Value[n-1]"

   -  Empty "Value" elements are represented by "null" entries in the
      "Value" array

-  "PersonName" elements map to objects within the "Value" array. For a
   "PersonName" element with the attribute "number=n":

   -  The "Alphabetic" element maps to "Value[**n-1**].Alphabetic"

   -  The "Ideographic" element maps to "PersonName[**n**].Ideographic"

   -  The "Phonetic" element maps to "PersonName[**n**].Phonetic"

-  "Item" elements map to members of the "Value" child array

   -  An "Item" element with the attribute "number=n" maps to
      "Value[n-1]"

   -  Empty "Item" elements are represented by empty JSON property
      entries in the "Value" array

-  The "uri" attribute of the "BulkData" element maps to the
   "BulkDataURI" string

-  The "InlineBinary" element maps to the "InlineBinary" string

.. table:: XML to JSON Mapping

   +----------------------------------+----------------------------------+
   | DICOM XML                        | DICOM JSON Model                 |
   +==================================+==================================+
   | ``<NativeDicomModel>``           | ``{``                            |
   |                                  |                                  |
   | ``<DicomAttribute tag=``         | **``ggggee01``** ``: { … },``    |
   | **``ggggee01``** ``… />``        |                                  |
   |                                  | **``ggggee02``** ``: { … },``    |
   | ``<DicomAttribute tag=``         |                                  |
   | **``ggggee02``** ``… />``        | ``…``                            |
   |                                  |                                  |
   | ``…``                            | ``}``                            |
   |                                  |                                  |
   | ``</NativeDicomModel>``          |                                  |
   +----------------------------------+----------------------------------+
   | ``<DicomAttribute``              | **``ggggeeee``** ``: {``         |
   |                                  |                                  |
   | ``tag=`` **``ggggeeee``**        | ``"vr":`` **``VR``** ``,``       |
   |                                  |                                  |
   | ``vr=`` **``VR``** ``>``         | ``"Value": [`` **``Value``**     |
   |                                  | ``]``                            |
   | ``<Value number="1">``           |                                  |
   | **``Value``** ``</Value>``       | ``}``                            |
   |                                  |                                  |
   | ``</DicomAttribute>``            |                                  |
   +----------------------------------+----------------------------------+
   | ``<DicomAttribute tag=``         | **``ggggeeee``** ``: {``         |
   | **``ggggeeee``** ``… >``         |                                  |
   |                                  | ``…``                            |
   | ``<Value number="1">``           |                                  |
   | **``Value1``** ``</Value>``      | ``"Value": [`` **``Value1``**    |
   |                                  | ``,``                            |
   | ``<Value number="2">``           |                                  |
   | **``Value2``** ``</Value>``      | **``Value2``** ``, …``           |
   |                                  |                                  |
   | ``…``                            | ``]``                            |
   |                                  |                                  |
   | ``</DicomAttribute>``            | ``}``                            |
   +----------------------------------+----------------------------------+
   | ``<DicomAttribute tag=``         | **``ggggeeee``** ``: {``         |
   | **``ggggeeee``** ``… >``         |                                  |
   |                                  | ``…``                            |
   | ``</DicomAttribute>``            |                                  |
   |                                  | ``}``                            |
   +----------------------------------+----------------------------------+
   | ``<DicomAttribute tag=``         | **``ggggeeee``** ``: {``         |
   | **``ggggeeee``** ``vr="PN" … >`` |                                  |
   |                                  | ``…``                            |
   | ``<PersonName number="1">``      |                                  |
   |                                  | ``"vr": "PN",``                  |
   | ``<Alphabetic>``                 |                                  |
   |                                  | ``"Value": [``                   |
   | ``<FamilyName>`` **``SB1``**     |                                  |
   |                                  | ``{``                            |
   | ``</FamilyName>``                |                                  |
   |                                  | **``"``** ``Alphabetic``         |
   | ``<GivenName>`` **``SB2``**      | **``"``** ``:``                  |
   |                                  | **``"SB1^SB2^SB3^SB4^SB5",``**   |
   | ``</GivenName>``                 |                                  |
   |                                  | ``"Ideographic":``               |
   | ``<MiddleName>`` **``SB3``**     | **``"ID1^ID2^ID3^ID4^ID5"``**    |
   |                                  | ``,``                            |
   | ``</MiddleName>``                |                                  |
   |                                  | ``"Phonetic":``                  |
   | ``<NamePrefix>`` **``SB4``**     | **``"PH1^PH2^PH3^PH4^PH5"``**    |
   |                                  |                                  |
   | ``</NamePrefix>``                | ``},``                           |
   |                                  |                                  |
   | ``<NameSuffix>`` **``SB5``**     | ``{``                            |
   |                                  |                                  |
   | ``</NameSuffix>``                | ``"Alphabetic":``                |
   |                                  |                                  |
   | ``</Alphabetic>``                | ``"`` **``SB6``** ``"``          |
   |                                  |                                  |
   | ``<Ideographic>``                | ``}``                            |
   |                                  |                                  |
   | ``<FamilyName>`` **``ID1``**     | ``]``                            |
   |                                  |                                  |
   | ``</FamilyName>``                | ``}``                            |
   |                                  |                                  |
   | ``…``                            |                                  |
   |                                  |                                  |
   | ``</Ideographic>``               |                                  |
   |                                  |                                  |
   | ``<Phonetic>``                   |                                  |
   |                                  |                                  |
   | ``<FamilyName>`` **``PH1``**     |                                  |
   |                                  |                                  |
   | ``</FamilyName>``                |                                  |
   |                                  |                                  |
   | ``…``                            |                                  |
   |                                  |                                  |
   | ``</Phonetic>``                  |                                  |
   |                                  |                                  |
   | ``</PersonName>``                |                                  |
   |                                  |                                  |
   | ``<PersonName number="2">``      |                                  |
   |                                  |                                  |
   | ``<Alphabetic>``                 |                                  |
   |                                  |                                  |
   | ``<FamilyName>`` **``SB6``**     |                                  |
   |                                  |                                  |
   | ``</FamilyName>``                |                                  |
   |                                  |                                  |
   | ``</Alphabetic>``                |                                  |
   |                                  |                                  |
   | ``</PersonName>``                |                                  |
   |                                  |                                  |
   | ``</DicomAttribute>``            |                                  |
   +----------------------------------+----------------------------------+
   | ``<DicomAttribute tag=``         | **``ggggeeee``** ``: {``         |
   | **``ggggeeee``** ``vr="SQ" … >`` |                                  |
   |                                  | ``…``                            |
   | ``<Item number="1">``            |                                  |
   |                                  | ``"vr": "SQ",``                  |
   | ``<DicomAttribute tag=``         |                                  |
   | **``ggggee01``** ``… />``        | ``"Value":``                     |
   |                                  |                                  |
   | ``<DicomAttribute tag=``         | ``[``                            |
   | **``ggggee02``** ``… />``        |                                  |
   |                                  | ``{``                            |
   | ``…``                            |                                  |
   |                                  | **``ggggee01``** ``: { … },``    |
   | ``</Item>``                      |                                  |
   |                                  | **``ggggee02``** ``: { … },``    |
   | ``<Item number="2">``            |                                  |
   |                                  | ``…``                            |
   | ``<DicomAttribute tag=``         |                                  |
   | **``ggggee01``** ``… />``        | ``}``                            |
   |                                  |                                  |
   | ``<DicomAttribute tag=``         | ``{``                            |
   | **``ggggee02``** ``… />``        |                                  |
   |                                  | **``ggggee01``** ``: { … },``    |
   | ``…``                            |                                  |
   |                                  | **``ggggee02``** ``: { … },``    |
   | ``</Item>``                      |                                  |
   |                                  | ``…``                            |
   | ``<Item number="3">``            |                                  |
   |                                  | ``}``                            |
   | ``</Item>``                      |                                  |
   |                                  | ``{ }``                          |
   | ``…``                            |                                  |
   |                                  | ``…``                            |
   | ``</DicomAttribute>``            |                                  |
   |                                  | ``]``                            |
   |                                  |                                  |
   |                                  | ``}``                            |
   +----------------------------------+----------------------------------+
   | ``<DicomAttribute tag=``         | **``ggggeeee``** ``: {``         |
   | **``ggggeeee``** ``… >``         |                                  |
   |                                  | ``…``                            |
   | ``<BulkData URI=``               |                                  |
   | **``BulkDataURI``** ``>``        | ``"BulkDataURI":``               |
   |                                  | **``BulkDataURI``**              |
   | ``</DicomAttribute>``            |                                  |
   |                                  | ``}``                            |
   +----------------------------------+----------------------------------+
   | ``<DicomAttribute tag=``         | **``ggggeeee``** ``: {``         |
   | **``ggggeeee``** ``… >``         |                                  |
   |                                  | ``…``                            |
   | ``<InlineBinary>``               |                                  |
   | **``Base64String``**             | ``"InlineBinary": "``            |
   | ``</InlineBinary>``              | **``Base64String"``**            |
   |                                  |                                  |
   | ``</DicomAttribute>``            | ``}``                            |
   +----------------------------------+----------------------------------+
   | ``<DicomAttribute tag=``         | **``ggggXXee``** ``: {``         |
   | **``gggg00ee``**                 |                                  |
   | ``PrivateCreator=``              | ``…``                            |
   | **``PrivateCreator``** ``… >``   |                                  |
   |                                  | ``}``                            |
   | ``…``                            |                                  |
   |                                  |                                  |
   | ``</DicomAttribute>``            |                                  |
   +----------------------------------+----------------------------------+

.. _sect_F.4:

DICOM JSON Model Example
------------------------

::

   // The following example is a QIDO-RS SearchForStudies response consisting 
   // of two matching studies, corresponding to the example QIDO-RS request:
   // GET http://qido.nema.org/studies?PatientID=12345&includefield=all&limit=2
   [
       {   // Result 1
           "00080005": {
               "vr": "CS",
               "Value": [ "ISO_IR 192" ]
           },
           "00080020": {
               "vr": "DT",
               "Value": [ "20130409" ]
           },
           "00080030": {
               "vr": "TM",
               "Value": [ "131600.0000" ]
           },
           "00080050": {
               "vr": "SH",
               "Value": [ "11235813" ]
           },
           "00080056": {
               "vr": "CS",
               "Value": [ "ONLINE" ]
           },
           "00080061": {
               "vr": "CS",
               "Value": [
                   "CT",
                   "PET"
               ]
           },
           "00080090": {
               "vr": "PN",
               "Value": [
                 {
                   "Alphabetic": "^Bob^^Dr."
                 }
               ]
           },
           "00081190": {
               "vr": "UR",
               "Value": [ "http://wado.nema.org/studies/
               1.2.392.200036.9116.2.2.2.1762893313.1029997326.945873" ]
           },
           "00090010": {
               "vr": "LO",
               "Value": [ "Vendor A" ]
           },
           "00091002": {
               "vr": "UN",
               "InlineBinary": [ "z0x9c8v7" ]
           },
           "00100010": {
               "vr": "PN",
               "Value": [
                 {
                   "Alphabetic": "Wang^XiaoDong",
                   "Ideographic": "王^小東"
                 }
               ]
           },
           "00100020": {
               "vr": "LO",
               "Value": [ "12345" ]
           },
           "00100021": {
               "vr": "LO",
               "Value": [ "Hospital A" ]
           },
           "00100030": {
               "vr": "DT",
               "Value": [ "19670701" ]
           },
           "00100040": {
               "vr": "CS",
               "Value": [ "M" ]
           },
           "00101002": {
               "vr": "SQ",
               "Value": [
                   {
                       "00100020": {
                           "vr": "LO",
                           "Value": [ "54321" ]
                       },
                       "00100021": {
                           "vr": "LO",
                           "Value": [ "Hospital B" ]
                       }
                   },
                   {
                       "00100020": {
                           "vr": "LO",
                           "Value": [ "24680" ]
                       },
                       "00100021": {
                           "vr": "LO",
                           "Value": [ "Hospital C" ]
                       }
                   }
               ]
           },
           "0020000D": {
               "vr": "UI",
               "Value": [ "1.2.392.200036.9116.2.2.2.1762893313.1029997326.945873" ]
           },
           "00200010": {
               "vr": "SH",
               "Value": [ "11235813" ]
           },
           "00201206": {
               "vr": "IS",
               "Value": [ 4 ]
           },
           "00201208": {
               "vr": "IS",
               "Value": [ 942 ]
           }
       },
       {   // Result 2
           "00080005": {
               "vr": "CS",
               "Value": [ "ISO_IR 192" ]
           },
           "00080020": {
               "vr": "DT",
               "Value": [ "20130309" ]
           },
           "00080030": {
               "vr": "TM",
               "Value": [ "111900.0000" ]
           },
           "00080050": {
               "vr": "SH",
               "Value": [ "11235821" ]
           },
           "00080056": {
               "vr": "CS",
               "Value": [ "ONLINE" ]
           },
           "00080061": {
               "vr": "CS",
               "Value": [
                   "CT",
                   "PET"
               ]
           },
           "00080090": {
               "vr": "PN",
               "Value": [
                 {
                   "Alphabetic": "^Bob^^Dr." 
                 }
               ]
           },
           "00081190": {
               "vr": "UR",
               "Value": [ "http://wado.nema.org/studies/
               1.2.392.200036.9116.2.2.2.2162893313.1029997326.945876" ]
           },
           "00090010": {
               "vr": "LO",
               "Value": [ "Vendor A" ]
           },
           "00091002": {
               "vr": "UN",
               "InlineBinary": [ "z0x9c8v7" ]
           },
           "00100010": {
               "vr": "PN",
               "Value": [
                 {
                   "Alphabetic": "Wang^XiaoDong",
                   "Ideographic": "王^小東" 
                 }
               ]
           },
           "00100020": {
               "vr": "LO",
               "Value": [ "12345" ]
           },
           "00100021": {
               "vr": "LO",
               "Value": [ "Hospital A" ]
           },
           "00100030": {
               "vr": "DT",
               "Value": [ "19670701" ]
           },
           "00100040": {
               "vr": "CS",
               "Value": [ "M" ]
           },
           "00101002": {
               "vr": "SQ",
               "Value": [
                   {
                       "00100020": {
                           "vr": "LO",
                           "Value": [ "54321" ]
                       },
                       "00100021": {
                           "vr": "LO",
                           "Value": [ "Hospital B" ]
                       }
                   },
                   {
                       "00100020": {
                           "vr": "LO",
                           "Value": [ "24680" ]
                       },
                       "00100021": {
                           "vr": "LO",
                           "Value": [ "Hospital C" ]
                       }
                   }
               ]
           },
           "0020000D": {
               "vr": "UI",
               "Value": [ "1.2.392.200036.9116.2.2.2.2162893313.1029997326.945876" ]
           },
           "00200010": {
               "vr": "SH",
               "Value": [ "11235821" ]
           },
           "00201206": {
               "vr": "IS",
               "Value": [ 5 ]
           },
           "00201208": {
               "vr": "IS",
               "Value": [ 1123 ]
           }
       }
   ]

.. _sect_F.5:

Retired
-------

See PS3.18-2019a.

