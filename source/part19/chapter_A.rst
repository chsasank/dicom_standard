.. _chapter_A:

Data Exchange Models
====================

.. _sect_A.1:

Native DICOM Model
------------------

.. _sect_A.1.1:

Usage
~~~~~

The Native DICOM Model defines a representation of binary-encoded DICOM
SOP Instances as XML Infosets that allows a recipient of data to
navigate through a binary DICOM data set using XML-based tools instead
of relying on tool kits that understand the binary encoding of DICOM.

.. note::

   It is not the intention that this form be utilized as the basis for
   other uses. This form does not take advantage of the self-validation
   features that could be possible with a pure XML representation of the
   data.

With the exception of padding to an even byte length, a data source that
is creating a new instance of a Native DICOM Model (e.g., the result
from some analysis application) shall follow the DICOM encoding rules
(e.g., the handling of character sets) in creating Values for the
DicomAttributes within the instance of the Native DICOM Model. Attribute
Values encoded in a Native DICOM Model are not required to be padded to
an even byte length.

Group Length (gggg,0000) attributes shall not be included in a Native
DICOM Model instance.

A data recipient that converts data from an instance of the Native DICOM
Model back into a binary encoded DICOM object shall adjust the padding
to an even byte length as necessary to meet the encoding rules specified
in DICOM .

.. _sect_A.1.2:

Identification
~~~~~~~~~~~~~~

The ObjectDescriptors MIME content type for the Native DICOM Model shall
be "application/x-dicom.native".

The ObjectDescriptors class UID for the Native DICOM Model shall be
"1.2.840.10008.7.1.1".

.. _sect_A.1.3:

Support
~~~~~~~

Support of the Native DICOM Model as both a data source and a data
recipient shall be required of all Hosting Systems implementing the
interface.

Support of the Native DICOM Model as either a data source or a data
recipient shall be optional for all Hosted Applications implementing the
interface.

.. _sect_A.1.4:

Information Model
~~~~~~~~~~~~~~~~~

A diagram of the Native DICOM Model appears in
`figure_title <#figure_A.1.4-1>`__.

.. _sect_A.1.5:

Description
~~~~~~~~~~~

.. table:: Native DICOM Model

   +-------------------+-------------+-------------+-------------------+
   | Name              | Optionality | Cardinality | Description       |
   +===================+=============+=============+===================+
   | NativeDicomModel  | R           | 1           | An Infoset (as    |
   |                   |             |             | defined in W3C    |
   |                   |             |             | Recommendation    |
   |                   |             |             | XML Information   |
   |                   |             |             | Set               |
   |                   |             |             | "h                |
   |                   |             |             | ttp://www.w3.org/ |
   |                   |             |             | TR/xml-infoset/") |
   |                   |             |             | representing the  |
   |                   |             |             | content of a      |
   |                   |             |             | DICOM Data Set    |
   |                   |             |             | (as defined in ). |
   |                   |             |             |                   |
   |                   |             |             | The               |
   |                   |             |             | directivexml      |
   |                   |             |             | :space="preserve" |
   |                   |             |             | shall be          |
   |                   |             |             | included.         |
   |                   |             |             |                   |
   |                   |             |             | Examples include: |
   |                   |             |             |                   |
   |                   |             |             | -  the contents   |
   |                   |             |             |    of an entire   |
   |                   |             |             |    DICOM          |
   |                   |             |             |    Composite      |
   |                   |             |             |    Instance (as   |
   |                   |             |             |    defined in )   |
   |                   |             |             |    in response to |
   |                   |             |             |    a native model |
   |                   |             |             |    request, or    |
   |                   |             |             |                   |
   |                   |             |             | -  the contents   |
   |                   |             |             |    of part of a   |
   |                   |             |             |    DICOM          |
   |                   |             |             |    Composite      |
   |                   |             |             |    Instance in    |
   |                   |             |             |    response to a  |
   |                   |             |             |    query on a     |
   |                   |             |             |    native model,  |
   |                   |             |             |    or             |
   |                   |             |             |                   |
   |                   |             |             | -  the contents   |
   |                   |             |             |    of a Studies   |
   |                   |             |             |    Service Store  |
   |                   |             |             |    (STOW-RS)      |
   |                   |             |             |    response       |
   |                   |             |             |                   |
   |                   |             |             | -  the contents   |
   |                   |             |             |    of a Sequence  |
   |                   |             |             |    Item (as       |
   |                   |             |             |    defined in ),  |
   |                   |             |             |    recursively    |
   |                   |             |             |    included       |
   |                   |             |             |    within an      |
   |                   |             |             |    Infoset Value  |
   |                   |             |             |    element.       |
   +-------------------+-------------+-------------+-------------------+
   | *Include*         |             |             |                   |
   | \ `table_title <# |             |             |                   |
   | table_A.1.5-2>`__ |             |             |                   |
   +-------------------+-------------+-------------+-------------------+

.. table:: DICOM Data Set Macro

   +-------------------+-------------+-------------+-------------------+
   | Name              | Optionality | Cardinality | Description       |
   +===================+=============+=============+===================+
   | DicomAttribute    | O           | 0-n         | An Infoset        |
   |                   |             |             | element           |
   |                   |             |             | corresponding to  |
   |                   |             |             | each DICOM        |
   |                   |             |             | Attribute.        |
   +-------------------+-------------+-------------+-------------------+
   | >keyword          | C           | A           | The keyword as    |
   |                   |             |             | defined in .      |
   |                   |             |             |                   |
   |                   |             |             | Required unless   |
   |                   |             |             | the DICOM Data    |
   |                   |             |             | Element is        |
   |                   |             |             | unknown to the    |
   |                   |             |             | host.             |
   +-------------------+-------------+-------------+-------------------+
   | >tag              | R           | A           | The four-digit    |
   |                   |             |             | zero-padded       |
   |                   |             |             | hexadecimal       |
   |                   |             |             | values of the     |
   |                   |             |             | Group and Element |
   |                   |             |             | Numbers of the    |
   |                   |             |             | Data Element Tag, |
   |                   |             |             | concatenated as a |
   |                   |             |             | single string     |
   |                   |             |             | without a         |
   |                   |             |             | delimiter and     |
   |                   |             |             | with lowercase    |
   |                   |             |             | letters           |
   |                   |             |             | disallowed. E.g., |
   |                   |             |             | Data Element      |
   |                   |             |             | (0010,0020) would |
   |                   |             |             | have a tag of     |
   |                   |             |             | "00100020".       |
   |                   |             |             |                   |
   |                   |             |             | For Private Data  |
   |                   |             |             | Elements, the two |
   |                   |             |             | most significant  |
   |                   |             |             | hexadecimal       |
   |                   |             |             | characters of the |
   |                   |             |             | Element Number    |
   |                   |             |             | shall be 00,      |
   |                   |             |             | since the Private |
   |                   |             |             | Creator is        |
   |                   |             |             | explicitly        |
   |                   |             |             | conveyed and the  |
   |                   |             |             | block used in the |
   |                   |             |             | DICOM encoding    |
   |                   |             |             | shall not be sent |
   |                   |             |             | (i.e., a Private  |
   |                   |             |             | Data Element has  |
   |                   |             |             | the form          |
   |                   |             |             | gggg00ee).        |
   +-------------------+-------------+-------------+-------------------+
   | >vr               | O           | A           | The Value         |
   |                   |             |             | Representation of |
   |                   |             |             | this element,     |
   |                   |             |             | represented as a  |
   |                   |             |             | two character     |
   |                   |             |             | uppercase string, |
   |                   |             |             | as defined in and |
   |                   |             |             | specified for     |
   |                   |             |             | this Data Element |
   |                   |             |             | in .              |
   |                   |             |             |                   |
   |                   |             |             | .. note::         |
   |                   |             |             |                   |
   |                   |             |             |                   |
   |                   |             |             |   Implementations |
   |                   |             |             |    may utilize    |
   |                   |             |             |    the Value      |
   |                   |             |             |    Representation |
   |                   |             |             |    to validate    |
   |                   |             |             |    data values,   |
   |                   |             |             |    if desired.    |
   +-------------------+-------------+-------------+-------------------+
   | >privateCreator   | C           | A           | The value of the  |
   |                   |             |             | Private Creator   |
   |                   |             |             | Data Element      |
   |                   |             |             | corresponding to  |
   |                   |             |             | the block in      |
   |                   |             |             | which this        |
   |                   |             |             | Private Data      |
   |                   |             |             | Element is used.  |
   |                   |             |             |                   |
   |                   |             |             | Required for      |
   |                   |             |             | Private Data      |
   |                   |             |             | Elements. Shall   |
   |                   |             |             | not be present    |
   |                   |             |             | otherwise (i.e.,  |
   |                   |             |             | for Data Elements |
   |                   |             |             | defined by the    |
   |                   |             |             | DICOM Standard).  |
   +-------------------+-------------+-------------+-------------------+
   | >Value            | C           | 1-n         | A Value from the  |
   |                   |             |             | Value Field of    |
   |                   |             |             | the DICOM Data    |
   |                   |             |             | Element. There is |
   |                   |             |             | one Infoset Value |
   |                   |             |             | element for each  |
   |                   |             |             | DICOM Value or    |
   |                   |             |             | Sequence Item.    |
   |                   |             |             |                   |
   |                   |             |             | Required if the   |
   |                   |             |             | DICOM Data        |
   |                   |             |             | Element           |
   |                   |             |             | represented is    |
   |                   |             |             | not zero length   |
   |                   |             |             | and an Item,      |
   |                   |             |             | PersonName,       |
   |                   |             |             | InlineBinary or   |
   |                   |             |             | BulkData XML      |
   |                   |             |             | element is not    |
   |                   |             |             | present. Shall    |
   |                   |             |             | not be used if    |
   |                   |             |             | the VR of the     |
   |                   |             |             | enclosing         |
   |                   |             |             | Attribute is      |
   |                   |             |             | either SQ or PN.  |
   +-------------------+-------------+-------------+-------------------+
   | >>number          | R           | A           | The order in      |
   |                   |             |             | which the Value   |
   |                   |             |             | occurs within the |
   |                   |             |             | DICOM Value       |
   |                   |             |             | Field, as a       |
   |                   |             |             | number            |
   |                   |             |             | monotonically     |
   |                   |             |             | increasing        |
   |                   |             |             | starting from 1   |
   |                   |             |             | by 1.             |
   |                   |             |             |                   |
   |                   |             |             | .. note::         |
   |                   |             |             |                   |
   |                   |             |             |    The Number XML |
   |                   |             |             |    Attribute is   |
   |                   |             |             |    used to        |
   |                   |             |             |    preserve the   |
   |                   |             |             |    original       |
   |                   |             |             |    order.         |
   +-------------------+-------------+-------------+-------------------+
   | >> *plain         | C           | 1           | A single DICOM    |
   | character data*   |             |             | value encoded as  |
   |                   |             |             | plain character   |
   |                   |             |             | data.             |
   |                   |             |             |                   |
   |                   |             |             | E.g., a DICOM     |
   |                   |             |             | Decimal String    |
   |                   |             |             | Value Field that  |
   |                   |             |             | contained two     |
   |                   |             |             | de                |
   |                   |             |             | limiter-separated |
   |                   |             |             | values, e.g.,     |
   |                   |             |             | "0.5\0.4" would   |
   |                   |             |             | be encoded as two |
   |                   |             |             | Infoset Value     |
   |                   |             |             | elements:<Value   |
   |                   |             |             | number="1">       |
   |                   |             |             | 0.5</Value><Value |
   |                   |             |             | number            |
   |                   |             |             | ="2">0.4</Value>A |
   |                   |             |             | Code String Value |
   |                   |             |             | Field that        |
   |                   |             |             | containing three  |
   |                   |             |             | de                |
   |                   |             |             | limiter-separated |
   |                   |             |             | values, the       |
   |                   |             |             | second of which   |
   |                   |             |             | was zero length,  |
   |                   |             |             | "MPG\\XR3", would |
   |                   |             |             | be encoded        |
   |                   |             |             | as:<Value         |
   |                   |             |             | number="1">       |
   |                   |             |             | MPG</Value><Value |
   |                   |             |             | number="          |
   |                   |             |             | 2"></Value><Value |
   |                   |             |             | number="3">XR     |
   |                   |             |             | 3</Value>Contrast |
   |                   |             |             | the latter        |
   |                   |             |             | example with a    |
   |                   |             |             | zero length Value |
   |                   |             |             | Field, in which   |
   |                   |             |             | case there would  |
   |                   |             |             | be no Infoset     |
   |                   |             |             | Value elements at |
   |                   |             |             | all.              |
   |                   |             |             |                   |
   |                   |             |             | For DICOM Data    |
   |                   |             |             | Elements whose VR |
   |                   |             |             | is AT, each value |
   |                   |             |             | shall be encoded  |
   |                   |             |             | as the four-digit |
   |                   |             |             | zero-padded       |
   |                   |             |             | hexadecimal       |
   |                   |             |             | values of the     |
   |                   |             |             | Group and Element |
   |                   |             |             | Numbers of the    |
   |                   |             |             | Data Element Tag, |
   |                   |             |             | concatenated as a |
   |                   |             |             | single string     |
   |                   |             |             | without a         |
   |                   |             |             | delimiter and     |
   |                   |             |             | with lowercase    |
   |                   |             |             | letters           |
   |                   |             |             | disallowed.       |
   |                   |             |             |                   |
   |                   |             |             | The character     |
   |                   |             |             | encoding is that  |
   |                   |             |             | declared for the  |
   |                   |             |             | Infoset,          |
   |                   |             |             | regardless of any |
   |                   |             |             | DICOM Specific    |
   |                   |             |             | Character Set,    |
   |                   |             |             | and any necessary |
   |                   |             |             | translation from  |
   |                   |             |             | the DICOM         |
   |                   |             |             | Specific          |
   |                   |             |             | Character Set to  |
   |                   |             |             | the Infoset       |
   |                   |             |             | character         |
   |                   |             |             | encoding shall    |
   |                   |             |             | have been         |
   |                   |             |             | performed.        |
   |                   |             |             |                   |
   |                   |             |             | .. note::         |
   |                   |             |             |                   |
   |                   |             |             |    This           |
   |                   |             |             |    translation    |
   |                   |             |             |    might not be   |
   |                   |             |             |    completely     |
   |                   |             |             |    lossless,      |
   |                   |             |             |    particularly   |
   |                   |             |             |    with Asian     |
   |                   |             |             |    character      |
   |                   |             |             |    sets.          |
   +-------------------+-------------+-------------+-------------------+
   | >Item             | C           | 1-n         | A DICOM sequence  |
   |                   |             |             | item, in other    |
   |                   |             |             | words a nested    |
   |                   |             |             | DICOM Data Set.   |
   |                   |             |             |                   |
   |                   |             |             | Required if the   |
   |                   |             |             | DICOM Data        |
   |                   |             |             | Element           |
   |                   |             |             | represented is a  |
   |                   |             |             | Sequence (has a   |
   |                   |             |             | VR of "SQ") and   |
   |                   |             |             | is not zero       |
   |                   |             |             | length. Not       |
   |                   |             |             | allowed           |
   |                   |             |             | otherwise.        |
   +-------------------+-------------+-------------+-------------------+
   | >>number          | R           | A           | The order in      |
   |                   |             |             | which the Item    |
   |                   |             |             | occurs within a   |
   |                   |             |             | Sequence of       |
   |                   |             |             | Items, as a       |
   |                   |             |             | number            |
   |                   |             |             | monotonically     |
   |                   |             |             | increasing from 1 |
   |                   |             |             | by 1.             |
   |                   |             |             |                   |
   |                   |             |             | .. note::         |
   |                   |             |             |                   |
   |                   |             |             |    The Number XML |
   |                   |             |             |    Attribute is   |
   |                   |             |             |    used to        |
   |                   |             |             |    preserve the   |
   |                   |             |             |    original       |
   |                   |             |             |    order.         |
   +-------------------+-------------+-------------+-------------------+
   | >>\ *Include*     | R           | 1           | Recursively       |
   | \ `table_title <# |             |             | includes the Data |
   | table_A.1.5-2>`__ |             |             | Set corresponding |
   |                   |             |             | to a Sequence     |
   |                   |             |             | Item.             |
   +-------------------+-------------+-------------+-------------------+
   | >PersonName       | C           | 1-n         | A parsed          |
   |                   |             |             | representation in |
   |                   |             |             | XML of a DICOM    |
   |                   |             |             | Data Element      |
   |                   |             |             | containing a name |
   |                   |             |             | (i.e., whose VR   |
   |                   |             |             | is PN).           |
   |                   |             |             |                   |
   |                   |             |             | .. note::         |
   |                   |             |             |                   |
   |                   |             |             |    Parsing        |
   |                   |             |             |    Attributes     |
   |                   |             |             |    with a VR of   |
   |                   |             |             |    PN into an XML |
   |                   |             |             |    representation |
   |                   |             |             |    of the name    |
   |                   |             |             |    groups and     |
   |                   |             |             |    components     |
   |                   |             |             |    simplifies the |
   |                   |             |             |    creation of    |
   |                   |             |             |    XPath          |
   |                   |             |             |    statements to  |
   |                   |             |             |    pull only      |
   |                   |             |             |    portions of    |
   |                   |             |             |    names out of   |
   |                   |             |             |    the DICOM      |
   |                   |             |             |    data.          |
   |                   |             |             |                   |
   |                   |             |             | Required if the   |
   |                   |             |             | DICOM Data        |
   |                   |             |             | Element           |
   |                   |             |             | represented has a |
   |                   |             |             | VR of PN and is   |
   |                   |             |             | not zero length.  |
   |                   |             |             | Not allowed       |
   |                   |             |             | otherwise.        |
   |                   |             |             |                   |
   |                   |             |             | The rules defined |
   |                   |             |             | in DICOM on the   |
   |                   |             |             | usage of the      |
   |                   |             |             | Alphabetic,       |
   |                   |             |             | Ideographic, and  |
   |                   |             |             | Phonetic groups   |
   |                   |             |             | of name           |
   |                   |             |             | components within |
   |                   |             |             | a DICOM Attribute |
   |                   |             |             | with a Value      |
   |                   |             |             | Representation of |
   |                   |             |             | PN apply.         |
   +-------------------+-------------+-------------+-------------------+
   | >>number          | R           | A           | The order in      |
   |                   |             |             | which the         |
   |                   |             |             | PersonName occurs |
   |                   |             |             | within the DICOM  |
   |                   |             |             | Value Field, as a |
   |                   |             |             | number            |
   |                   |             |             | monotonically     |
   |                   |             |             | increasing from 1 |
   |                   |             |             | by 1.             |
   |                   |             |             |                   |
   |                   |             |             | .. note::         |
   |                   |             |             |                   |
   |                   |             |             |    The Number XML |
   |                   |             |             |    Attribute is   |
   |                   |             |             |    used to        |
   |                   |             |             |    preserve the   |
   |                   |             |             |    original       |
   |                   |             |             |    order.         |
   +-------------------+-------------+-------------+-------------------+
   | >>Alphabetic      | O           | 0-1         | A group of name   |
   |                   |             |             | components that   |
   |                   |             |             | are represented   |
   |                   |             |             | in alphabetical   |
   |                   |             |             | characters (see   |
   |                   |             |             | the definition    |
   |                   |             |             | for the Value     |
   |                   |             |             | Representation of |
   |                   |             |             | PN in ).          |
   +-------------------+-------------+-------------+-------------------+
   | >>>\ *Include     |             |             |                   |
   | *\ `table_title < |             |             |                   |
   | #table_10.2-1>`__ |             |             |                   |
   +-------------------+-------------+-------------+-------------------+
   | >>Ideographic     | O           | 0-1         | A group of name   |
   |                   |             |             | components that   |
   |                   |             |             | are represented   |
   |                   |             |             | in ideographic    |
   |                   |             |             | characters (see   |
   |                   |             |             | the definition    |
   |                   |             |             | for the Value     |
   |                   |             |             | Representation of |
   |                   |             |             | PN in ).          |
   +-------------------+-------------+-------------+-------------------+
   | >>>\ *Include     |             |             |                   |
   | *\ `table_title < |             |             |                   |
   | #table_10.2-1>`__ |             |             |                   |
   +-------------------+-------------+-------------+-------------------+
   | >>Phonetic        | O           | 0-1         | A group of name   |
   |                   |             |             | components that   |
   |                   |             |             | are represented   |
   |                   |             |             | in phonetic       |
   |                   |             |             | characters (see   |
   |                   |             |             | the definition    |
   |                   |             |             | for the Value     |
   |                   |             |             | Representation of |
   |                   |             |             | PN in ).          |
   +-------------------+-------------+-------------+-------------------+
   | >>>\ *Include     |             |             |                   |
   | *\ `table_title < |             |             |                   |
   | #table_10.2-1>`__ |             |             |                   |
   +-------------------+-------------+-------------+-------------------+
   | >BulkData         | C           | 1           | A reference to a  |
   |                   |             |             | blob of data that |
   |                   |             |             | the recipient may |
   |                   |             |             | retrieve through  |
   |                   |             |             | use of the        |
   |                   |             |             | GetData() method, |
   |                   |             |             | a Studies Service |
   |                   |             |             | Retrieve          |
   |                   |             |             | (WADO-RS)         |
   |                   |             |             | transaction or a  |
   |                   |             |             | Studies Service   |
   |                   |             |             | Store (STOW-RS)   |
   |                   |             |             | transaction.      |
   |                   |             |             |                   |
   |                   |             |             | Required if the   |
   |                   |             |             | DICOM Data        |
   |                   |             |             | Element           |
   |                   |             |             | represented is    |
   |                   |             |             | not zero length   |
   |                   |             |             | and an XML        |
   |                   |             |             | Infoset Value,    |
   |                   |             |             | Item,             |
   |                   |             |             | InlineBinary or   |
   |                   |             |             | PersonName        |
   |                   |             |             | element is not    |
   |                   |             |             | present.          |
   |                   |             |             |                   |
   |                   |             |             | The provider of   |
   |                   |             |             | the data may use  |
   |                   |             |             | a BulkData        |
   |                   |             |             | reference at its  |
   |                   |             |             | discretion to     |
   |                   |             |             | avoid encoding a  |
   |                   |             |             | large DICOM Value |
   |                   |             |             | Field as text by  |
   |                   |             |             | value in the      |
   |                   |             |             | Infoset. For      |
   |                   |             |             | example, pixel    |
   |                   |             |             | data or look up   |
   |                   |             |             | tables.           |
   |                   |             |             |                   |
   |                   |             |             | There is a single |
   |                   |             |             | BulkData Infoset  |
   |                   |             |             | element           |
   |                   |             |             | representing the  |
   |                   |             |             | entire Value      |
   |                   |             |             | Field, and not    |
   |                   |             |             | one per Value in  |
   |                   |             |             | the case where    |
   |                   |             |             | the Value         |
   |                   |             |             | Multiplicity is   |
   |                   |             |             | greater than one. |
   |                   |             |             |                   |
   |                   |             |             | .. note::         |
   |                   |             |             |                   |
   |                   |             |             |    E.g., a LUT    |
   |                   |             |             |    with 4096 16   |
   |                   |             |             |    bit entries    |
   |                   |             |             |    that may be    |
   |                   |             |             |    encoded in     |
   |                   |             |             |    DICOM with a   |
   |                   |             |             |    Value          |
   |                   |             |             |    Representation |
   |                   |             |             |    of OW, with a  |
   |                   |             |             |    VL of 8192 and |
   |                   |             |             |    a VM of 1, or  |
   |                   |             |             |    a US VR with a |
   |                   |             |             |    VL of 8192 and |
   |                   |             |             |    a VM of 4096   |
   |                   |             |             |    would both be  |
   |                   |             |             |    represented as |
   |                   |             |             |    a single       |
   |                   |             |             |    BulkData       |
   |                   |             |             |    element.       |
   |                   |             |             |                   |
   |                   |             |             | All rules (e.g.,  |
   |                   |             |             | byte ordering and |
   |                   |             |             | swapping) in      |
   |                   |             |             | apply.            |
   |                   |             |             |                   |
   |                   |             |             | .. note::         |
   |                   |             |             |                   |
   |                   |             |             |    Implementers   |
   |                   |             |             |    should pay     |
   |                   |             |             |    particular     |
   |                   |             |             |    attention to   |
   |                   |             |             |    the rules      |
   |                   |             |             |    regarding the  |
   |                   |             |             |    value          |
   |                   |             |             |                   |
   |                   |             |             |   representations |
   |                   |             |             |    of OD, OF, OL, |
   |                   |             |             |    OV and OW.     |
   |                   |             |             |                   |
   |                   |             |             | If the BulkData   |
   |                   |             |             | has a string or   |
   |                   |             |             | text Value        |
   |                   |             |             | Representation,   |
   |                   |             |             | the value(s) of   |
   |                   |             |             | the DICOM         |
   |                   |             |             | Specific          |
   |                   |             |             | Character Set     |
   |                   |             |             | Data Element, if  |
   |                   |             |             | present, might be |
   |                   |             |             | necessary to      |
   |                   |             |             | determine its     |
   |                   |             |             | encoding.         |
   +-------------------+-------------+-------------+-------------------+
   | >>uuid            | C           | A           | An identifier of  |
   |                   |             |             | this bulk data    |
   |                   |             |             | reference         |
   |                   |             |             | formatted as a    |
   |                   |             |             | UUID using the    |
   |                   |             |             | hexadecimal       |
   |                   |             |             | representation    |
   |                   |             |             | defined in ITU-T  |
   |                   |             |             | Recommendation    |
   |                   |             |             | X.667.            |
   |                   |             |             |                   |
   |                   |             |             | Required if       |
   |                   |             |             | BulkData URI is   |
   |                   |             |             | not present.      |
   |                   |             |             | Shall not be      |
   |                   |             |             | present           |
   |                   |             |             | otherwise.        |
   +-------------------+-------------+-------------+-------------------+
   | >>uri             | C           | A           | The HTTP(S) URI   |
   |                   |             |             | for this bulk     |
   |                   |             |             | data reference.   |
   |                   |             |             |                   |
   |                   |             |             | Required if the   |
   |                   |             |             | NativeDicomModel  |
   |                   |             |             | was:              |
   |                   |             |             |                   |
   |                   |             |             | -  returned in    |
   |                   |             |             |    response to a  |
   |                   |             |             |    Studies        |
   |                   |             |             |    Service        |
   |                   |             |             |    Retrieve       |
   |                   |             |             |    (WADO-RS)      |
   |                   |             |             |    Retrieve       |
   |                   |             |             |    Metadata       |
   |                   |             |             |    request        |
   |                   |             |             |                   |
   |                   |             |             | Shall not be      |
   |                   |             |             | present           |
   |                   |             |             | otherwise.        |
   +-------------------+-------------+-------------+-------------------+
   | >InlineBinary     | C           | 1           | The Value Field   |
   |                   |             |             | of the enclosing  |
   |                   |             |             | Attribute encoded |
   |                   |             |             | as base64.        |
   |                   |             |             |                   |
   |                   |             |             | Required if the   |
   |                   |             |             | DICOM Data        |
   |                   |             |             | Element           |
   |                   |             |             | represented is:   |
   |                   |             |             |                   |
   |                   |             |             | -  not zero       |
   |                   |             |             |    length         |
   |                   |             |             |                   |
   |                   |             |             | -  the VR if the  |
   |                   |             |             |    enclosing      |
   |                   |             |             |    Attribute is   |
   |                   |             |             |    OB, OD, OF,    |
   |                   |             |             |    OL, OV, OW, or |
   |                   |             |             |    UN             |
   |                   |             |             |                   |
   |                   |             |             | -  an XML Infoset |
   |                   |             |             |    Value or       |
   |                   |             |             |    BulkData XML   |
   |                   |             |             |    element is not |
   |                   |             |             |    present        |
   |                   |             |             |                   |
   |                   |             |             | Shall not be      |
   |                   |             |             | present           |
   |                   |             |             | otherwise.        |
   |                   |             |             |                   |
   |                   |             |             | There is a single |
   |                   |             |             | InlineBinary      |
   |                   |             |             | Infoset element   |
   |                   |             |             | representing the  |
   |                   |             |             | entire Value      |
   |                   |             |             | Field, and not    |
   |                   |             |             | one per Value in  |
   |                   |             |             | the case where    |
   |                   |             |             | the Value         |
   |                   |             |             | Multiplicity is   |
   |                   |             |             | greater than one. |
   |                   |             |             |                   |
   |                   |             |             | .. note::         |
   |                   |             |             |                   |
   |                   |             |             |    E.g., a LUT    |
   |                   |             |             |    with 4096 16   |
   |                   |             |             |    bit entries    |
   |                   |             |             |    that may be    |
   |                   |             |             |    encoded in     |
   |                   |             |             |    DICOM with a   |
   |                   |             |             |    Value          |
   |                   |             |             |    Representation |
   |                   |             |             |    of OW with a   |
   |                   |             |             |    VL of 8192 and |
   |                   |             |             |    a VM of 1      |
   |                   |             |             |    would be       |
   |                   |             |             |    represented as |
   |                   |             |             |    a single       |
   |                   |             |             |    InlineBinary   |
   |                   |             |             |    element.       |
   |                   |             |             |                   |
   |                   |             |             | All rules (e.g.,  |
   |                   |             |             | byte ordering and |
   |                   |             |             | swapping) in      |
   |                   |             |             | apply.            |
   |                   |             |             |                   |
   |                   |             |             | .. note::         |
   |                   |             |             |                   |
   |                   |             |             |    Implementers   |
   |                   |             |             |    should pay     |
   |                   |             |             |    particular     |
   |                   |             |             |    attention to   |
   |                   |             |             |    the rules      |
   |                   |             |             |    regarding the  |
   |                   |             |             |    value          |
   |                   |             |             |                   |
   |                   |             |             |   representations |
   |                   |             |             |    of OD, OF, OL, |
   |                   |             |             |    OV and OW.     |
   +-------------------+-------------+-------------+-------------------+

.. _sect_A.1.6:

Schema
~~~~~~

The Normative version of the XML Schema for the Native DICOM Model
follows:

::

   default namespace="http://dicom.nema.org/PS3.19/models/NativeDICOM"

   # This schema was created as an intermediary, a means of describing
   # native binary encoded DICOM objects as XML Infosets, thus allowing  
   # one to manipulate binary DICOM objects using familiar XML tools. 
   # As such, the schema is designed to facilitate a simple, mechanical,
   # bi-directional translation between binary encoded DICOM and XML-like 
   # constructs without constraints, and to simplify identifying portions 
   # of a DICOM object using XPath statements.
   #
   # Since this schema has minimal type checking, it is neither intended 
   # to be used for any operation that involves hand coding, nor to 
   # describe a definitive, fully validating encoding of DICOM concepts
   # into XML, as what one might use, for example, in a robust XML  
   # database system or in XML-based forms, though it may be used
   # as a means for translating binary DICOM Objects into such a form
   # (e.g., through an XSLT script).

   start = element NativeDicomModel { DicomDataSet }

   # A DICOM Data Set is as defined in PS3.5.  It does not appear 
   # as an XML Element, since it does not appear in the binary encoded 
   # DICOM objects.  It exists here merely as a documentation aid. 
   DicomDataSet = DicomAttribute*

   DicomAttribute = element DicomAttribute {
     Tag, VR, Keyword?, PrivateCreator?, 
     (BulkData | Value+ | Item+ | PersonName+ | InlineBinary)? 
   } 
   BulkData = element BulkData{ UUID | URI } 
   Value = element Value { Number, xsd:string }
   InlineBinary = element InlineBinary { xsd:base64Binary }
   Item = element Item { Number, DicomDataSet }
   PersonName = element PersonName {
     Number,
     element Alphabetic  { NameComponents }?,
     element Ideographic { NameComponents }?,
     element Phonetic    { NameComponents }?
   }

   NameComponents =
     element FamilyName {xsd:string}?,
     element GivenName  {xsd:string}?,
     element MiddleName {xsd:string}?,
     element NamePrefix {xsd:string}?,
     element NameSuffix {xsd:string}?
     
   # keyword is the attribute tag from PS3.6 
   # (derived from the DICOM Attribute's name)
   Keyword = attribute keyword { xsd:token }
   # canonical XML definition of Hex, with lowercase letters disallowed
   Tag = attribute tag { xsd:string{ minLength="8" maxLength="8" pattern="[0-9A-F]{8}" } } 
   VR = attribute vr { "AE" | "AS" | "AT"| "CS" | "DA" | "DS" | "DT" | "FL" | "FD" 
                       | "IS" | "LO" | "LT" | "OB" | "OD" | "OF" | "OL" | "OV" | | "OW" | "PN" | "SH" | "SL" 
                       | "SQ" | "SS" | "ST" | "SV" | "TM" | "UC" | "UI" | "UL" | "UN" | "UR" | "US" | "UT" | "UV" }
   PrivateCreator = attribute privateCreator{ xsd:string }
   UUID = attribute uuid { xsd:string }
   URI = attribute uri { xsd:anyURI }
   Number = attribute number { xsd:positiveInteger } 

.. _sect_A.1.7:

Examples
~~~~~~~~

Here is an example XPath query to extract the code meaning of the first
item in the View Code Sequence:

/NativeDicomModel/DicomAttribute[@keyword="ViewCodeSequence"]/Item[@number=1]/​DicomAttribute[@keyword="CodeMeaning"]/Value[@number=1]

.. _sect_A.2:

Abstract Multi-Dimensional Image Model
--------------------------------------

.. _sect_A.2.1:

Usage
~~~~~

The Abstract Multi-Dimensional Image Model can be used to refer to a
discretely-sampled, multi-dimensional image data. The sample values may
either be single-valued (a scalar) or a vector of values (a vector). An
example would be a time varying series of three dimensional images set
at multiple energy levels. The Abstract Multi-Dimensional Image Model is
patterned after the Enhanced Multi-frame family of DICOM objects. In
mathematical terms, this is any data set that is defined by a function
*I (x,y,z,t,…)*, where *(x,y,z,t,…)* are the dimensions, and the sample
value of *I* is either a vector of components or a scalar (i.e., a
single component). The primary purpose of this model is to allow
applications to process image data without concern as to the underlying
format of the data.

When converting DICOM SOP Instances into Abstract Multi-Dimensional
Image Models, a provider of data shall follow these rules as closely as
it practically can:

.. note::

   Deterministic behavior is not expected nor guaranteed when making
   conversions between DICOM SOP Instances and Abstract
   Multi-Dimensional Image Models. For example, given the same DICOM SOP
   Instances, different Hosting Systems may create Abstract
   Multi-Dimensional Image Models that differ in some details, such as
   the Units of the Component values or in the Dimensions.

1. Multiple DICOM SOP Instances from the same series that have the same
   Frame of Reference UID shall be combined into a single instance of
   the Abstract Multi-Dimensional Image Model. DICOM SOP Instances from
   multiple series that have the same Frame of Reference UUID may be
   combined into a single instance of the Abstract Multi-Dimensional
   Image Model, if appropriate.

2. A single DICOM SOP Instance shall not be divided into multiple
   instances of the Abstract Multi-Dimensional Image Model.

3. The coordinate system utilized within the Abstract Multi-Dimensional
   Image Model shall use the coordinate system defined by the DICOM
   objects utilized in the creation of the Abstract Multi-Dimensional
   Image Model instance if applicable. Where practical, the coordinate
   system and Dimension definitions utilized within the Abstract
   Multi-Dimensional Image Model shall be chosen such that interpolation
   is not required to convert the source data into the Abstract
   Multi-Dimensional Image Model.

   .. note::

      Interpolation may be necessary if the source data is not laid out
      on a frame-based Cartesian coordinate grid.

4. Spatial coordinates, such as Image Position (Patient) (0020,0032),
   shall be transformed into the coordinate system utilized within the
   Abstract Multi-Dimensional Image Model instance.

5. The Pixel Data shall be spatially transformed as needed to match the
   Semantics and Units of the Dimensions of the Abstract
   Multi-Dimensional Image Model into which the pixels values are being
   placed.

6. Any embedded overlays within the Pixel Data (7FE0,0010) Attribute
   shall be stripped out of the pixel values and the pixel values sign
   extended or converted as needed to match the datatype of the
   Component of the Abstract Multi-Dimensional Image Model into which
   the pixels values are being placed.

7. The pixel values of the Pixel Data shall be transformed as needed to
   match the Semantics and Units of the Component of the Abstract
   Multi-Dimensional Image Model into which the pixels values are being
   placed.

   .. note::

      Typically presentation settings such as VOI and Presentation LUTs
      are not used in creating Abstract Multi-Dimensional Image Models
      from DICOM SOP Instances. The exception is when the application of
      such LUTs is needed to match the Semantics and Units of the
      Component. Modality LUTs or Rescale Slope and Intercept often must
      be applied to match the Semantics and Units of the Abstract
      Multi-Dimensional Image Model.

8. Any pixel values that correspond to the pixel padding values shall be
   stripped out (i.e., set to zero or other suitable replacement value)
   and the spatially corresponding values in the PixelMapOfValidData
   shall be set to the outValue or something other than the inValue, as
   appropriate.

When converting data within an instance of the Abstract
Multi-Dimensional Image Models into DICOM SOP Instances, the recipient
of an abstract model instance shall convert the pixel data back into
values compatible with the native form of the DICOM SOP Instances being
created. This conversion may include recreating Modality LUT
information, inserting pixel padding values, converting pixel spacing
and origins, etc. as dictated by the SOP Class the data is being
converted to. When converting a single Abstract Multi-Dimensional Image
Model into multiple DICOM SOP Instances, the DICOM SOP Instances shall
all have the same Frame of Reference UID (0020,0052), if permitted by
the SOP Class.

.. _sect_A.2.2:

Identification
~~~~~~~~~~~~~~

The ObjectDescriptors MIME content type for the Abstract
Multi-Dimensional Image Model is "application/x-dicom.abstract".

.. note::

   This is an experimental MIME type. A formal MIME type will be applied
   for. Implementations will be expected to support both the
   experimental and formal MIME type going forward without a version
   change to the interface.

The ObjectDescriptors class UID for the Abstract Multi-Dimensional Image
Model is "1.2.840.10008.7.1.2".

.. _sect_A.2.3:

Support
~~~~~~~

Support of the Abstract Multi-Dimensional Image Model as both a data
source and a data recipient is required of all Hosting Systems
implementing the interface.

Support of the Abstract Multi-Dimensional Image Model as either a data
source or a data recipient is optional for all Hosted Applications
implementing the interface.

.. _sect_A.2.4:

Information Model
~~~~~~~~~~~~~~~~~

A diagram of the Abstract Multi-Dimensional Image Model appears in
`figure_title <#figure_A.2.4-1>`__.

.. _sect_A.2.5:

Description
~~~~~~~~~~~

.. table:: Abstract Image Model

   +-------------------+-------------+-------------+-------------------+
   | Name              | Optionality | Cardinality | Description       |
   +===================+=============+=============+===================+
   | Abs               | R           | 1           | The top level     |
   | tractImageDataSet |             |             | element required  |
   |                   |             |             | of all abstract   |
   |                   |             |             | image models,     |
   |                   |             |             | holding the       |
   |                   |             |             | entire abstract   |
   |                   |             |             | image Data Set.   |
   +-------------------+-------------+-------------+-------------------+
   | >Component        | R           | 1-n         | Describes a       |
   |                   |             |             | component of the  |
   |                   |             |             | function output.  |
   |                   |             |             | If the output is  |
   |                   |             |             | a scalar, there   |
   |                   |             |             | is only one       |
   |                   |             |             | Component. Vector |
   |                   |             |             | outputs require a |
   |                   |             |             | Component for     |
   |                   |             |             | each position in  |
   |                   |             |             | the vector. When  |
   |                   |             |             | there are         |
   |                   |             |             | multiple          |
   |                   |             |             | components, the   |
   |                   |             |             | components appear |
   |                   |             |             | in each value in  |
   |                   |             |             | the order defined |
   |                   |             |             | by their          |
   |                   |             |             | respective        |
   |                   |             |             | idNumbers.        |
   +-------------------+-------------+-------------+-------------------+
   | >>idNumber        | R           | A           | Identifies this   |
   |                   |             |             | particular        |
   |                   |             |             | component, with   |
   |                   |             |             | numbering         |
   |                   |             |             | monotonically     |
   |                   |             |             | increasing from   |
   |                   |             |             | 1.                |
   +-------------------+-------------+-------------+-------------------+
   | >>datatype        | R           | A           | Describes how     |
   |                   |             |             | this component    |
   |                   |             |             | value is          |
   |                   |             |             | represented.      |
   |                   |             |             | Enumerated values |
   |                   |             |             | are:              |
   |                   |             |             |                   |
   |                   |             |             | SIGNED_INT8       |
   |                   |             |             |                   |
   |                   |             |             | SIGNED_INT16      |
   |                   |             |             |                   |
   |                   |             |             | SIGNED_INT32      |
   |                   |             |             |                   |
   |                   |             |             | UNSIGNED_INT8     |
   |                   |             |             |                   |
   |                   |             |             | UNSIGNED_INT16    |
   |                   |             |             |                   |
   |                   |             |             | UNSIGNED_INT32    |
   |                   |             |             |                   |
   |                   |             |             | FLOAT32           |
   |                   |             |             |                   |
   |                   |             |             | FLOAT64           |
   +-------------------+-------------+-------------+-------------------+
   | >>minValue        | O           | A           | The minimum value |
   |                   |             |             | that this         |
   |                   |             |             | component takes   |
   |                   |             |             | on. If this XML   |
   |                   |             |             | Attribute is      |
   |                   |             |             | missing, this is  |
   |                   |             |             | the minimum value |
   |                   |             |             | that can be       |
   |                   |             |             | represented by    |
   |                   |             |             | the Datatype.     |
   +-------------------+-------------+-------------+-------------------+
   | >>maxValue        | O           | A           | The maximum value |
   |                   |             |             | that this         |
   |                   |             |             | component takes   |
   |                   |             |             | on. If this XML   |
   |                   |             |             | Attribute is      |
   |                   |             |             | missing, this is  |
   |                   |             |             | the maximum value |
   |                   |             |             | that can be       |
   |                   |             |             | represented by    |
   |                   |             |             | the Datatype.     |
   +-------------------+-------------+-------------+-------------------+
   | >>Semantics       | R           | 1           | A coded value     |
   |                   |             |             | describing what   |
   |                   |             |             | this component    |
   |                   |             |             | represents.       |
   +-------------------+-------------+-------------+-------------------+
   | >>>\ *Include     | Defined .   |             |                   |
   | *\ `table_title < |             |             |                   |
   | #table_10.1-1>`__ |             |             |                   |
   +-------------------+-------------+-------------+-------------------+
   | >>Unit            | R           | 1           | A coded value     |
   |                   |             |             | describing what   |
   |                   |             |             | units this        |
   |                   |             |             | dimension is in.  |
   +-------------------+-------------+-------------+-------------------+
   | >>>\ *Include     | Defined .   |             |                   |
   | *\ `table_title < |             |             |                   |
   | #table_10.1-1>`__ |             |             |                   |
   +-------------------+-------------+-------------+-------------------+
   | >Dimension        | R           | 1-n         | Describes a       |
   |                   |             |             | dimension.        |
   +-------------------+-------------+-------------+-------------------+
   | >>idNumber        | R           | A           | Identifies this   |
   |                   |             |             | particular        |
   |                   |             |             | dimension, with   |
   |                   |             |             | numbering         |
   |                   |             |             | starting from 1.  |
   |                   |             |             | Dimensions with a |
   |                   |             |             | lower idNumber    |
   |                   |             |             | vary faster than  |
   |                   |             |             | those with a      |
   |                   |             |             | higher idNumber.  |
   +-------------------+-------------+-------------+-------------------+
   | >>numberOfSamples | R           | A           | The number of     |
   |                   |             |             | samples in this   |
   |                   |             |             | dimension, for    |
   |                   |             |             | example:the       |
   |                   |             |             | number of columns |
   |                   |             |             | along the         |
   |                   |             |             | X-axis,the number |
   |                   |             |             | of rows along the |
   |                   |             |             | Y-axis,the number |
   |                   |             |             | of slices along   |
   |                   |             |             | the Z-axis,the    |
   |                   |             |             | number of         |
   |                   |             |             | qualitative       |
   |                   |             |             | descriptions.     |
   +-------------------+-------------+-------------+-------------------+
   | >>Semantics       | R           | 1           | A coded value     |
   |                   |             |             | describing what   |
   |                   |             |             | this dimension    |
   |                   |             |             | represents.       |
   +-------------------+-------------+-------------+-------------------+
   | >>>\ *Include     | Defined     |             |                   |
   | *\ `table_title < |             |             |                   |
   | #table_10.1-1>`__ |             |             |                   |
   +-------------------+-------------+-------------+-------------------+
   | >> Regular        | C           | 1           | Used to describe  |
   |                   |             |             | regularly spaced  |
   |                   |             |             | samples in this   |
   |                   |             |             | dimension.        |
   |                   |             |             | Required if       |
   |                   |             |             | neither Irregular |
   |                   |             |             | nor Qualitative   |
   |                   |             |             | are present.      |
   |                   |             |             | Shall not be      |
   |                   |             |             | present           |
   |                   |             |             | otherwise.        |
   +-------------------+-------------+-------------+-------------------+
   | >>>width          | R           | A           | The sample width. |
   +-------------------+-------------+-------------+-------------------+
   | >>>spacing        | R           | A           | The sample        |
   |                   |             |             | spacing.          |
   +-------------------+-------------+-------------+-------------------+
   | >>>Unit           | R           | 1           | A coded value     |
   |                   |             |             | describing what   |
   |                   |             |             | units the sample  |
   |                   |             |             | width and spacing |
   |                   |             |             | are in.           |
   +-------------------+-------------+-------------+-------------------+
   | >>>>\ *Include    | Defined .   |             |                   |
   | *\ `table_title < |             |             |                   |
   | #table_10.1-1>`__ |             |             |                   |
   +-------------------+-------------+-------------+-------------------+
   | >>>AxisDirection  | O           | 1           | The direction of  |
   |                   |             |             | the axis of this  |
   |                   |             |             | dimension.        |
   |                   |             |             |                   |
   |                   |             |             | .. note::         |
   |                   |             |             |                   |
   |                   |             |             |    This XML       |
   |                   |             |             |    Element might  |
   |                   |             |             |    only be        |
   |                   |             |             |    applicable to  |
   |                   |             |             |    spatial        |
   |                   |             |             |    dimensions,    |
   |                   |             |             |    such as those  |
   |                   |             |             |    dealing with   |
   |                   |             |             |    linear         |
   |                   |             |             |    displacement.  |
   |                   |             |             |    Typically this |
   |                   |             |             |    is in          |
   |                   |             |             |    relationship   |
   |                   |             |             |    to the         |
   |                   |             |             |    patient.       |
   +-------------------+-------------+-------------+-------------------+
   | >>>>\ *Include    | Defined     |             |                   |
   | *\ `table_title < |             |             |                   |
   | #table_10.1-1>`__ |             |             |                   |
   +-------------------+-------------+-------------+-------------------+
   | >                 | O           | 1           | The orientation   |
   | >>AxisOrientation |             |             | of the axis of    |
   |                   |             |             | this dimension    |
   |                   |             |             | along which       |
   |                   |             |             | values are        |
   |                   |             |             | increasing.       |
   |                   |             |             |                   |
   |                   |             |             | .. note::         |
   |                   |             |             |                   |
   |                   |             |             |    This XML       |
   |                   |             |             |    Element might  |
   |                   |             |             |    only be        |
   |                   |             |             |    applicable to  |
   |                   |             |             |    spatial        |
   |                   |             |             |    dimensions,    |
   |                   |             |             |    such as those  |
   |                   |             |             |    dealing with   |
   |                   |             |             |    linear         |
   |                   |             |             |    displacement.  |
   |                   |             |             |    Typically this |
   |                   |             |             |    is in          |
   |                   |             |             |    relationship   |
   |                   |             |             |    to the         |
   |                   |             |             |    patient.       |
   +-------------------+-------------+-------------+-------------------+
   | >>>>\ *Include    | Defined     |             |                   |
   | *\ `table_title < |             |             |                   |
   | #table_10.1-1>`__ |             |             |                   |
   +-------------------+-------------+-------------+-------------------+
   | >>Irregular       | C           | 1           | Used to describe  |
   |                   |             |             | irregularly       |
   |                   |             |             | spaced samples in |
   |                   |             |             | this dimension.   |
   |                   |             |             | Required if       |
   |                   |             |             | neither Regular   |
   |                   |             |             | nor Qualitative   |
   |                   |             |             | are present.      |
   |                   |             |             | Shall not be      |
   |                   |             |             | present           |
   |                   |             |             | otherwise.        |
   +-------------------+-------------+-------------+-------------------+
   | >>>origin         | R           | A           | The reference     |
   |                   |             |             | location from     |
   |                   |             |             | which each of the |
   |                   |             |             | sample locations  |
   |                   |             |             | are measured.     |
   +-------------------+-------------+-------------+-------------------+
   | >>>SampleLocation | R           | 1-n         | Describes the     |
   |                   |             |             | locations of each |
   |                   |             |             | sample as an      |
   |                   |             |             | offset from the   |
   |                   |             |             | origin. There     |
   |                   |             |             | shall be          |
   |                   |             |             | numberOfSamples   |
   |                   |             |             | SampleLocation    |
   |                   |             |             | XML Elements in   |
   |                   |             |             | this sequence.    |
   +-------------------+-------------+-------------+-------------------+
   | >>>>index         | R           | A           | The index value   |
   |                   |             |             | of this sample    |
   |                   |             |             | location, with    |
   |                   |             |             | numbering         |
   |                   |             |             | starting from 1   |
   |                   |             |             | and incrementing  |
   |                   |             |             | to                |
   |                   |             |             | numberOfSamples.  |
   +-------------------+-------------+-------------+-------------------+
   | >>>>width         | R           | A           | The sample width. |
   +-------------------+-------------+-------------+-------------------+
   | >>>               | R           | A           | The distance of   |
   | >distanceToOrigin |             |             | this sample       |
   |                   |             |             | location from the |
   |                   |             |             | Origin location.  |
   +-------------------+-------------+-------------+-------------------+
   | >>>Unit           | R           | 1           | A coded value     |
   |                   |             |             | describing what   |
   |                   |             |             | units the sample  |
   |                   |             |             | widths and        |
   |                   |             |             | locations are in. |
   +-------------------+-------------+-------------+-------------------+
   | >>>>\ *Include    | Defined .   |             |                   |
   | *\ `table_title < |             |             |                   |
   | #table_10.1-1>`__ |             |             |                   |
   +-------------------+-------------+-------------+-------------------+
   | >>>AxisDirection  | O           | 1           | The direction of  |
   |                   |             |             | the axis of this  |
   |                   |             |             | dimension.        |
   |                   |             |             |                   |
   |                   |             |             | .. note::         |
   |                   |             |             |                   |
   |                   |             |             |    This XML       |
   |                   |             |             |    Element might  |
   |                   |             |             |    only be        |
   |                   |             |             |    applicable to  |
   |                   |             |             |    spatial        |
   |                   |             |             |    dimensions,    |
   |                   |             |             |    such as those  |
   |                   |             |             |    dealing with   |
   |                   |             |             |    linear         |
   |                   |             |             |    displacement.  |
   |                   |             |             |    Typically this |
   |                   |             |             |    is in          |
   |                   |             |             |    relationship   |
   |                   |             |             |    to the         |
   |                   |             |             |    patient.       |
   +-------------------+-------------+-------------+-------------------+
   | >>>>\ *Include    | Defined     |             |                   |
   | *\ `table_title < |             |             |                   |
   | #table_10.1-1>`__ |             |             |                   |
   +-------------------+-------------+-------------+-------------------+
   | >                 | O           | 1           | The orientation   |
   | >>AxisOrientation |             |             | of the axis of    |
   |                   |             |             | this dimension    |
   |                   |             |             | along which       |
   |                   |             |             | values are        |
   |                   |             |             | increasing.       |
   |                   |             |             |                   |
   |                   |             |             | .. note::         |
   |                   |             |             |                   |
   |                   |             |             |    This XML       |
   |                   |             |             |    Element might  |
   |                   |             |             |    only be        |
   |                   |             |             |    applicable to  |
   |                   |             |             |    spatial        |
   |                   |             |             |    dimensions,    |
   |                   |             |             |    such as those  |
   |                   |             |             |    dealing with   |
   |                   |             |             |    linear         |
   |                   |             |             |    displacement.  |
   |                   |             |             |    Typically this |
   |                   |             |             |    is in          |
   |                   |             |             |    relationship   |
   |                   |             |             |    to the         |
   |                   |             |             |    patient.       |
   +-------------------+-------------+-------------+-------------------+
   | >>>>\ *Include    | Defined     |             |                   |
   | *\ `table_title < |             |             |                   |
   | #table_10.1-1>`__ |             |             |                   |
   +-------------------+-------------+-------------+-------------------+
   | >>Qualitative     | C           | 1           | Used to describe  |
   |                   |             |             | a qualitative     |
   |                   |             |             | dimension.        |
   |                   |             |             | Required if       |
   |                   |             |             | neither Regular   |
   |                   |             |             | nor Irregular are |
   |                   |             |             | present. Shall    |
   |                   |             |             | not be present    |
   |                   |             |             | otherwise.        |
   +-------------------+-------------+-------------+-------------------+
   | >>>Sample         | R           | 1-n         | Description of    |
   |                   |             |             | what each sample  |
   |                   |             |             | along this        |
   |                   |             |             | dimension         |
   |                   |             |             | represents. There |
   |                   |             |             | shall be          |
   |                   |             |             | numberOfSamples   |
   |                   |             |             | Sample XML        |
   |                   |             |             | Elements in this  |
   |                   |             |             | sequence.         |
   +-------------------+-------------+-------------+-------------------+
   | >>>>index         | R           | A           | The index value   |
   |                   |             |             | of this sample,   |
   |                   |             |             | with numbering    |
   |                   |             |             | starting from 1   |
   |                   |             |             | and increasing to |
   |                   |             |             | numberOfSamples.  |
   +-------------------+-------------+-------------+-------------------+
   | >>>>Semantics     | R           | 1           | A coded value     |
   |                   |             |             | describing what   |
   |                   |             |             | this sample       |
   |                   |             |             | represents.       |
   +-------------------+-------------+-------------+-------------------+
   | >>>>>\ *Include   | Defined     |             |                   |
   | *\ `table_title < |             |             |                   |
   | #table_10.1-1>`__ |             |             |                   |
   +-------------------+-------------+-------------+-------------------+
   | >>Origin          | O           | 0-n         | Specifies the     |
   |                   |             |             | spatial position  |
   |                   |             |             | in the coordinate |
   |                   |             |             | system of the     |
   |                   |             |             | Abstract          |
   |                   |             |             | Multi-Dimensional |
   |                   |             |             | Image Model of    |
   |                   |             |             | the spatial       |
   |                   |             |             | frames or volumes |
   |                   |             |             | of image data     |
   |                   |             |             | values. Different |
   |                   |             |             | frames or volumes |
   |                   |             |             | may either share  |
   |                   |             |             | an origin, or     |
   |                   |             |             | have a different  |
   |                   |             |             | origin for each   |
   |                   |             |             | frame or volume.  |
   |                   |             |             | If there is only  |
   |                   |             |             | a single Origin   |
   |                   |             |             | XML element       |
   |                   |             |             | within this       |
   |                   |             |             | Dimension, then   |
   |                   |             |             | this Origin       |
   |                   |             |             | applies to all    |
   |                   |             |             | samples along     |
   |                   |             |             | this Dimension.   |
   |                   |             |             | Otherwise, there  |
   |                   |             |             | shall be          |
   |                   |             |             | numberOfSamples   |
   |                   |             |             | Origin XML        |
   |                   |             |             | elements, one for |
   |                   |             |             | each sample along |
   |                   |             |             | this Dimension.   |
   |                   |             |             | Sample index      |
   |                   |             |             | values for        |
   |                   |             |             | Dimensions whose  |
   |                   |             |             | idNumbers are     |
   |                   |             |             | less than this    |
   |                   |             |             | Dimension's       |
   |                   |             |             | idNumber, are all |
   |                   |             |             | equal to 1.       |
   +-------------------+-------------+-------------+-------------------+
   | >>>index          | R           | A           | Index of the      |
   |                   |             |             | sample to which   |
   |                   |             |             | this Origin       |
   |                   |             |             | applies. If this  |
   |                   |             |             | is a single       |
   |                   |             |             | Origin that       |
   |                   |             |             | applies to all    |
   |                   |             |             | samples along     |
   |                   |             |             | this Dimension,   |
   |                   |             |             | then index shall  |
   |                   |             |             | either be left    |
   |                   |             |             | out or given a    |
   |                   |             |             | value of "0"      |
   |                   |             |             | (zero).           |
   |                   |             |             | Otherwise, the    |
   |                   |             |             | value shall be    |
   |                   |             |             | the appropriate   |
   |                   |             |             | number between 1  |
   |                   |             |             | and               |
   |                   |             |             | numberOfSamples.  |
   +-------------------+-------------+-------------+-------------------+
   | >>>xCoord         | R           | A           | The X position of |
   |                   |             |             | this Origin in    |
   |                   |             |             | the coordinate    |
   |                   |             |             | system of the     |
   |                   |             |             | Abstract          |
   |                   |             |             | Multi-Dimensional |
   |                   |             |             | Image Model.      |
   +-------------------+-------------+-------------+-------------------+
   | >>>yCoord         | R           | A           | The Y position of |
   |                   |             |             | this Origin in    |
   |                   |             |             | the coordinate    |
   |                   |             |             | system of the     |
   |                   |             |             | Abstract          |
   |                   |             |             | Multi-Dimensional |
   |                   |             |             | Image Model.      |
   +-------------------+-------------+-------------+-------------------+
   | >>>zCoord         | R           | A           | The Z position of |
   |                   |             |             | this Origin in    |
   |                   |             |             | the coordinate    |
   |                   |             |             | system of the     |
   |                   |             |             | Abstract          |
   |                   |             |             | Multi-Dimensional |
   |                   |             |             | Image Model.      |
   +-------------------+-------------+-------------+-------------------+
   | >                 | O           | 0-n         | Specifies the     |
   | >DirectionCosines |             |             | direction in the  |
   |                   |             |             | coordinate system |
   |                   |             |             | of the Abstract   |
   |                   |             |             | Multi-Dimensional |
   |                   |             |             | Image Model of    |
   |                   |             |             | the Dimension     |
   |                   |             |             | whose idNumber is |
   |                   |             |             | given in          |
   |                   |             |             | concerned         |
   |                   |             |             | SpatialDimension. |
   |                   |             |             | The idNumber of   |
   |                   |             |             | the               |
   |                   |             |             | concerne          |
   |                   |             |             | dSpatialDimension |
   |                   |             |             | shall be less     |
   |                   |             |             | than the idNumber |
   |                   |             |             | of this           |
   |                   |             |             | Dimension. If     |
   |                   |             |             | there is only a   |
   |                   |             |             | single            |
   |                   |             |             | DirectionCosines  |
   |                   |             |             | XML element       |
   |                   |             |             | within this       |
   |                   |             |             | Dimension XML     |
   |                   |             |             | element with a    |
   |                   |             |             | particular        |
   |                   |             |             | concerned         |
   |                   |             |             | SpatialDimension, |
   |                   |             |             | then this         |
   |                   |             |             | Direction Cosine  |
   |                   |             |             | applies to all    |
   |                   |             |             | samples along     |
   |                   |             |             | this Dimension.   |
   |                   |             |             | Otherwise, there  |
   |                   |             |             | shall be          |
   |                   |             |             | numberOfSamples   |
   |                   |             |             | DirectionCosines  |
   |                   |             |             | XML elements with |
   |                   |             |             | this particular   |
   |                   |             |             | concerned         |
   |                   |             |             | SpatialDimension, |
   |                   |             |             | one for each      |
   |                   |             |             | sample along this |
   |                   |             |             | Dimension.        |
   +-------------------+-------------+-------------+-------------------+
   | >>>concerne       | R           | A           | The idNumber of   |
   | dSpatialDimension |             |             | the particular    |
   |                   |             |             | Dimension for     |
   |                   |             |             | which this        |
   |                   |             |             | DirectionCosines  |
   |                   |             |             | XML element       |
   |                   |             |             | applies. The      |
   |                   |             |             | value of          |
   |                   |             |             | concerne          |
   |                   |             |             | dSpatialDimension |
   |                   |             |             | shall be less     |
   |                   |             |             | than the idNumber |
   |                   |             |             | of this           |
   |                   |             |             | Dimension.        |
   +-------------------+-------------+-------------+-------------------+
   | >>>index          | C           | A           | Index of this     |
   |                   |             |             | direction         |
   |                   |             |             | specification,    |
   |                   |             |             | with numbering    |
   |                   |             |             | starting from 1.  |
   |                   |             |             | If this is a      |
   |                   |             |             | single-valued     |
   |                   |             |             | DirectionCosines  |
   |                   |             |             | that applies to   |
   |                   |             |             | all samples along |
   |                   |             |             | this Dimension    |
   |                   |             |             | then index shall  |
   |                   |             |             | either be left    |
   |                   |             |             | out or given a    |
   |                   |             |             | value of "0"      |
   |                   |             |             | (zero).           |
   |                   |             |             | Otherwise, the    |
   |                   |             |             | value of index    |
   |                   |             |             | refers to the     |
   |                   |             |             | DirectionCosines  |
   |                   |             |             | of a particular   |
   |                   |             |             | sample value      |
   |                   |             |             | along this        |
   |                   |             |             | Dimension.        |
   +-------------------+-------------+-------------+-------------------+
   | >>>cosAlongX      | R           | A           | The direction     |
   |                   |             |             | cosine along the  |
   |                   |             |             | X axis of the     |
   |                   |             |             | coordinate system |
   |                   |             |             | of the Abstract   |
   |                   |             |             | Multi-Dimensional |
   |                   |             |             | Image Model for   |
   |                   |             |             | this              |
   |                   |             |             | concerned         |
   |                   |             |             | SpatialDimension. |
   +-------------------+-------------+-------------+-------------------+
   | >>>cosAlongY      | R           | A           | The direction     |
   |                   |             |             | cosine along the  |
   |                   |             |             | Y axis of the     |
   |                   |             |             | coordinate system |
   |                   |             |             | of the Abstract   |
   |                   |             |             | Multi-Dimensional |
   |                   |             |             | Image Model for   |
   |                   |             |             | this              |
   |                   |             |             | concerned         |
   |                   |             |             | SpatialDimension. |
   +-------------------+-------------+-------------+-------------------+
   | >>>cosAlongZ      | R           | A           | The direction     |
   |                   |             |             | cosine along the  |
   |                   |             |             | Z axis of the     |
   |                   |             |             | coordinate system |
   |                   |             |             | of the Abstract   |
   |                   |             |             | Multi-Dimensional |
   |                   |             |             | Image Model for   |
   |                   |             |             | this              |
   |                   |             |             | concerned         |
   |                   |             |             | SpatialDimension. |
   +-------------------+-------------+-------------+-------------------+
   | >PixelData        | R           | 1           | Structure that    |
   |                   |             |             | defines where the |
   |                   |             |             | pixel data is     |
   |                   |             |             | located,          |
   |                   |             |             | organized along   |
   |                   |             |             | dimensional       |
   |                   |             |             | lines.            |
   +-------------------+-------------+-------------+-------------------+
   | *>>Include*       |             |             |                   |
   | \ `table_title <# |             |             |                   |
   | table_A.2.5-2>`__ |             |             |                   |
   +-------------------+-------------+-------------+-------------------+
   | >Pi               | O           | 0-1         | A pixel map that  |
   | xelMapOfValidData |             |             | identifies which  |
   |                   |             |             | pixels either     |
   |                   |             |             | belong in or out  |
   |                   |             |             | of the Data Set.  |
   |                   |             |             | The dimensions of |
   |                   |             |             | the pixel map     |
   |                   |             |             | match the         |
   |                   |             |             | dimensions of the |
   |                   |             |             | image data, i.e., |
   |                   |             |             | there is a        |
   |                   |             |             | one-to-one        |
   |                   |             |             | correspondence    |
   |                   |             |             | between samples   |
   |                   |             |             | in the image data |
   |                   |             |             | and samples in    |
   |                   |             |             | the pixel map.    |
   |                   |             |             | The pointers to   |
   |                   |             |             | the pixel map     |
   |                   |             |             | data are included |
   |                   |             |             | in one of the     |
   |                   |             |             | Dimension XML     |
   |                   |             |             | elements.         |
   +-------------------+-------------+-------------+-------------------+
   | >>datatype        | R           | A           | Describes how     |
   |                   |             |             | samples in the    |
   |                   |             |             | pixel map are     |
   |                   |             |             | encoded.          |
   |                   |             |             | Enumerated values |
   |                   |             |             | are:              |
   |                   |             |             |                   |
   |                   |             |             | BIT1              |
   |                   |             |             |                   |
   |                   |             |             | UNSIGNED_INT8     |
   |                   |             |             |                   |
   |                   |             |             | For BIT1, the bit |
   |                   |             |             | ordering starts   |
   |                   |             |             | from the least    |
   |                   |             |             | significant bit   |
   |                   |             |             | going to the most |
   |                   |             |             | significant bit   |
   |                   |             |             | within an         |
   |                   |             |             | UNSIGNED_INT8     |
   |                   |             |             | (i.e., 8 bit)     |
   |                   |             |             | byte. The bits    |
   |                   |             |             | are zero-padded   |
   |                   |             |             | to make a full    |
   |                   |             |             | 8-bit byte at the |
   |                   |             |             | end of the most   |
   |                   |             |             | rapidly changing  |
   |                   |             |             | dimension (i.e.,  |
   |                   |             |             | the Dimension     |
   |                   |             |             | whose idNumber is |
   |                   |             |             | 1).               |
   +-------------------+-------------+-------------+-------------------+
   | >>inValue         | C           | A           | The value within  |
   |                   |             |             | the pixel map     |
   |                   |             |             | that indicates    |
   |                   |             |             | that this sample  |
   |                   |             |             | shall be          |
   |                   |             |             | considered as     |
   |                   |             |             | part of the Data  |
   |                   |             |             | Set. All samples  |
   |                   |             |             | whose pixel map   |
   |                   |             |             | values do not     |
   |                   |             |             | match inValue     |
   |                   |             |             | shall not be      |
   |                   |             |             | considered as     |
   |                   |             |             | part of the Data  |
   |                   |             |             | Set. Required if  |
   |                   |             |             | outValue is not   |
   |                   |             |             | present. Shall    |
   |                   |             |             | not be present if |
   |                   |             |             | outValue is       |
   |                   |             |             | present.          |
   +-------------------+-------------+-------------+-------------------+
   | >>outValue        | C           | A           | The value within  |
   |                   |             |             | the pixel map     |
   |                   |             |             | that indicates    |
   |                   |             |             | that this sample  |
   |                   |             |             | shall not be      |
   |                   |             |             | considered as     |
   |                   |             |             | part of the Data  |
   |                   |             |             | Set. All samples  |
   |                   |             |             | whose pixel map   |
   |                   |             |             | values do not     |
   |                   |             |             | match outValue    |
   |                   |             |             | shall be          |
   |                   |             |             | considered as     |
   |                   |             |             | part of the Data  |
   |                   |             |             | Set. Required if  |
   |                   |             |             | inValue is not    |
   |                   |             |             | present. Shall    |
   |                   |             |             | not be present if |
   |                   |             |             | inValue is        |
   |                   |             |             | present.          |
   +-------------------+-------------+-------------+-------------------+
   | >>\ *Include*     |             |             |                   |
   | \ `table_title <# |             |             |                   |
   | table_A.2.5-2>`__ |             |             |                   |
   +-------------------+-------------+-------------+-------------------+

.. table:: Dimensional Data Macro

   +-------------------+-------------------+-----+-------------------+
   | >dimensionID      | R                 | A   | The idNumber of   |
   |                   |                   |     | the Dimension in  |
   |                   |                   |     | this              |
   |                   |                   |     | Abs               |
   |                   |                   |     | tractImageDataSet |
   |                   |                   |     | to which this     |
   |                   |                   |     | DimensionalData   |
   |                   |                   |     | refers.           |
   +-------------------+-------------------+-----+-------------------+
   | >DataAt           | O                 | 1-n | References to     |
   |                   |                   |     | where the image   |
   |                   |                   |     | data is located.  |
   |                   |                   |     | Only one          |
   |                   |                   |     | Dimension XML     |
   |                   |                   |     | Element within    |
   |                   |                   |     | this              |
   |                   |                   |     | Abs               |
   |                   |                   |     | tractImageDataSet |
   |                   |                   |     | shall have UUIDs  |
   |                   |                   |     | for bulk pixel    |
   |                   |                   |     | data (i.e., all   |
   |                   |                   |     | bulk data         |
   |                   |                   |     | references are at |
   |                   |                   |     | the same          |
   |                   |                   |     | dimensional       |
   |                   |                   |     | level).           |
   |                   |                   |     |                   |
   |                   |                   |     | .. note::         |
   |                   |                   |     |                   |
   |                   |                   |     |    If the source  |
   |                   |                   |     |    of the data,   |
   |                   |                   |     |    as part of the |
   |                   |                   |     |    model          |
   |                   |                   |     |    preparation,   |
   |                   |                   |     |    creates a      |
   |                   |                   |     |    single file    |
   |                   |                   |     |    for pixel data |
   |                   |                   |     |    from multiple  |
   |                   |                   |     |    smaller native |
   |                   |                   |     |    objects, then  |
   |                   |                   |     |    in order to    |
   |                   |                   |     |    provide the    |
   |                   |                   |     |    descriptorUUID |
   |                   |                   |     |    XML Attributes |
   |                   |                   |     |    the source may |
   |                   |                   |     |    need to create |
   |                   |                   |     |    multiple       |
   |                   |                   |     |    bulkDataUUIDs  |
   |                   |                   |     |    referring to   |
   |                   |                   |     |    different      |
   |                   |                   |     |    offsets within |
   |                   |                   |     |    that single    |
   |                   |                   |     |    pixel data     |
   |                   |                   |     |    file.          |
   +-------------------+-------------------+-----+-------------------+
   | >>ind             | R                 | A   | The ordinal       |
   | exWithinDimension |                   |     | position (e.g.,   |
   |                   |                   |     | index number) of  |
   |                   |                   |     | this sample point |
   |                   |                   |     | in the array of   |
   |                   |                   |     | data at this      |
   |                   |                   |     | level. Numbering  |
   |                   |                   |     | starts from 1.    |
   +-------------------+-------------------+-----+-------------------+
   | >>descriptorUUID  | C                 | A   | A UUID that       |
   |                   |                   |     | refers to the     |
   |                   |                   |     | ObjectDescriptor  |
   |                   |                   |     | from which this   |
   |                   |                   |     | data is drawn,    |
   |                   |                   |     | formatted in the  |
   |                   |                   |     | hexadecimal       |
   |                   |                   |     | representation    |
   |                   |                   |     | defined by ITU-T  |
   |                   |                   |     | Recommendation    |
   |                   |                   |     | X.667.            |
   |                   |                   |     |                   |
   |                   |                   |     | Required at the   |
   |                   |                   |     | level of the      |
   |                   |                   |     | nested tree       |
   |                   |                   |     | structure where   |
   |                   |                   |     | the source added  |
   |                   |                   |     | the data from the |
   |                   |                   |     | descriptorUUID    |
   |                   |                   |     | into the Abstract |
   |                   |                   |     | Multi-Dimensional |
   |                   |                   |     | Image Model.      |
   +-------------------+-------------------+-----+-------------------+
   | >>bulkDataUUID    | C                 | A   | The identifier    |
   |                   |                   |     | that the          |
   |                   |                   |     | recipient of the  |
   |                   |                   |     | data may use in a |
   |                   |                   |     | getData() call to |
   |                   |                   |     | gain access to    |
   |                   |                   |     | the bulk pixel    |
   |                   |                   |     | data formatted as |
   |                   |                   |     | a UUID using the  |
   |                   |                   |     | hexadecimal       |
   |                   |                   |     | representation    |
   |                   |                   |     | defined in ITU-T  |
   |                   |                   |     | Recommendation    |
   |                   |                   |     | X.667.            |
   |                   |                   |     |                   |
   |                   |                   |     | Required if the   |
   |                   |                   |     | Dimensional Data  |
   |                   |                   |     | Macro is not      |
   |                   |                   |     | present at this   |
   |                   |                   |     | level of the      |
   |                   |                   |     | nested tree       |
   |                   |                   |     | structure. Shall  |
   |                   |                   |     | not be present    |
   |                   |                   |     | otherwise.        |
   +-------------------+-------------------+-----+-------------------+
   | >                 | Only one of       |     |                   |
   | >\ *Conditionally | bulkDataUUID or   |     |                   |
   | include*          | Dimensional Data  |     |                   |
   | \ `table_title <# | shall be included |     |                   |
   | table_A.2.5-2>`__ | at each level. If |     |                   |
   |                   | Dimensional Data  |     |                   |
   |                   | is included, it   |     |                   |
   |                   | shall be the next |     |                   |
   |                   | lower level of    |     |                   |
   |                   | the nested tree   |     |                   |
   |                   | structure, that   |     |                   |
   |                   | is the Dimension  |     |                   |
   |                   | with an idNumber  |     |                   |
   |                   | one less than the |     |                   |
   |                   | Dimension         |     |                   |
   |                   | referred to by    |     |                   |
   |                   | the enclosing     |     |                   |
   |                   | DimensionalData.  |     |                   |
   +-------------------+-------------------+-----+-------------------+

.. _sect_A.2.6:

Schema
~~~~~~

The Relax NG Compact schema for the Abstract Multi-Dimensional Image
Model follows:

::

   default namespace = "http://dicom.nema.org/PS3.19/models/AbstractImage"

   start = AbstractImageDataSet
   AbstractImageDataSet = 

    element AbstractImageDataSet {
       element Component{
         attribute idNumber { xsd:positiveInteger },
         attribute datatype { ComponentDatatype },
         attribute minValue { xsd:double }?,
         attribute maxValue { xsd:double }?,
         element Semantics { CodedTerm },
         element Unit { CodedTerm }
       }+,
       element Dimension {
         attribute idNumber { xsd:positiveInteger },
         attribute numberOfSamples { xsd:positiveInteger },
         element Semantics { CodedTerm },
         (element Regular {
            attribute width { xsd:double },
            attribute spacing { xsd:double },
            element Unit { CodedTerm },
            element AxisDirection { CodedTerm }?,
            element AxisOrientation { CodedTerm }?
          }
          | element Irregular {
              attribute origin { xsd:double },
              element SampleLocation {
                attribute index { xsd:positiveInteger },
                attribute width { xsd:double },
                attribute distanceToOrigin { xsd:double }
              }+,
            element Unit { CodedTerm },
            element AxisDirection { CodedTerm }?,
            element AxisOrientation { CodedTerm }?
            }
          | element Qualitative {
              element Sample {
                attribute index { xsd:positiveInteger },
                element Semantics { CodedTerm }
              }+
            }),
         element Origin {
           attribute index { xsd:nonNegativeInteger }?,
           attribute xCoord { xsd:double },
           attribute yCoord { xsd:double },
           attribute zCoord { xsd:double }
         }*,
         element DirectionCosines {
           attribute concernedSpatialDimension { xsd:positiveInteger },
           attribute index { xsd:nonNegativeInteger }?,
           attribute cosAlongX { xsd:double },
           attribute cosAlongY { xsd:double },
           attribute cosAlongZ { xsd:double }
         }*
       }+,
       element PixelData { DimensionalData },
       element PixelMapOfValidData {
         attribute datatype { PixelMapDatatype },
         (
           attribute inValue { xsd:positiveInteger }
           | attribute outValue { xsd:positiveInteger }
         ),
         DimensionalData
       }?
     }

   ComponentDatatype =
       "SIGNED_INT8"
       | "SIGNED_INT16"
       | "SIGNED_INT32"
       | "UNSIGNED_INT8"
       | "UNSIGNED_INT16"
       | "UNSIGNED_INT32"
       | "FLOAT32"
       | "FLOAT64"
     
   PixelMapDatatype = 
       "BIT1"
       | "UNSIGNED_INT8"

   DimensionalData =
     element DimensionalData {
       attribute dimensionID { xsd:positiveInteger },
       element DataAt 
       {
         attribute indexWithinDimension { xsd:positiveInteger },
         attribute descriptorUUID { xsd:string }?,
         (DimensionalData | BulkDataPointer)
       }+
     }

   BulkDataPointer = 
       attribute bulkDataUUID { xsd:string }

   CodedTerm = 
       element CodeValue { xsd:string },
       element CodingSchemeDesignator { xsd:string },
       element CodingSchemeVersion { xsd:string }?,
       element CodeMeaning { xsd:string }?,
       (
         element ContextIdentifier { xsd:string },
         element ContextUID { xsd:string }?,
         element MappingResource { xsd:string },
         element MappingResourceUID { xsd:string }?,
         element ContextGroupVersion { xsd:string }
       )?,
       (
         element ContextGroupExtensionFlag { xsd:string },
         element ContextGroupLocalVersion { xsd:string }?,
         element ContextGroupExtensionCreatorUID { xsd:string }?
       )?

.. _sect_A.2.7:

Examples
~~~~~~~~

.. _sect_A.2.7.1:

Simple 3D Volume
^^^^^^^^^^^^^^^^

.. _sect_A.2.7.2:

Simple 4D Volume
^^^^^^^^^^^^^^^^

.. _sect_A.2.7.3:

2D Ultrasound
^^^^^^^^^^^^^

-  In this particular case, we have three dimensions, numbered #1 for
   displacements along X, #2 for displacements along Y, and #3 to index
   the time series. If we have 200 images along time (i.e., the
   *numberOfSamples* XML Attribute is set to 200), we will then have 400
   occurrences of the *DirectionCosines* XML Element within the
   *Dimension* XML Element whose *idNumber* XML Attribute is set to #3
   (the dimension referring to time). The 200 first occurrences will
   have the XML Attribute *concernedSpatialDimension* with value #1 (to
   specify direction cosines along the X axis) and will be indexed by
   the XML Attribute *index* varying from 1 to 200 corresponding to the
   200 images along time. The 200 following occurrences will have the
   XML Attribute *concernedSpatialDimension* with value #2 (to specify
   direction cosines along the Y axis), and will also be indexed by the
   XML Attribute *index* varying from 1 to 200.

-  Similarly, in this example we will have 200 occurrences of the
   *Origin* XML Element within the Dimension XML Element that has the
   *idNumber* XML Attribute set to the value 3, and of course by the XML
   Attribute *index* varying from 1 to 200.

.. _sect_A.2.7.4:

3D MR Metabolite Map - Single Component
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

.. _sect_A.2.7.5:

3D MR Metabolite Map - Multiple Component
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

