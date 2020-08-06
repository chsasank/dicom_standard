.. _chapter_10:

Data Exchange Model Conventions
===============================

Models that can be used by the model-based DataExchange interface
methods are defined in `Data Exchange Models <#chapter_A>`__. These
models are defined in the form of XML Schemas written in Relax NG
Compact form of DSDL as specified by ISO/IEC 19757.

.. note::

   An implementer may translate the Relax NG Compact form to other forms
   for use within their implementation as long as the exchanged XML
   Infosets will validate against the schema specified by the Standard.
   For example, a particular implementation may internally utilize a
   schema with stronger validation rules (e.g., using Schematron rules
   as specified in ISO/IEC 19757, or using XSDL with assertion rules) as
   long as the XML produced for exchange over the interface can be
   parsed with the schema specified in the Standard, and that XML from
   well-formed DICOM objects produced by the schema specified in the
   Standard can still be utilized by the implementation's internal
   schema.

Actual instances of the models are XML Infosets. `Data Exchange
Models <#chapter_A>`__ follows the following conventions in describing
models.

.. note::

   1. The models are defined via XML schemas to allow the use of
      commonly available tools to manipulate and navigate the model. For
      example, an XPath statement can be used to identify portions of
      interest within the model such as a particular DICOM Attribute and
      extract it.

   2. Some implementations may parse directly from the incoming object,
      which may not be in XML form, into an internal representation,
      such as the domain object model (DOM) without ever having
      converted the object to XML.

Within each model description is a table of XML Elements and XML
Attributes used to describe an XML Infoset of that model. These tables
utilize the following conventions:

1. XML Element names (listed in the first column) are in CamelCase, with
   the first letter capitalized.

2. XML Attribute names (listed in the first column) are in camelCase
   with the first letter in lower case.

3. XML Element and XML Attribute names with a set of ">" characters in
   front of them are nested within the first preceding XML Element with
   one fewer ">" characters in front of its name. A nested XML Attribute
   is associated with the immediately enclosing XML Element.

4. The entries in the "Optionality" column have the following
   interpretations:

   -  "R" indicates that the XML Element or XML Attribute is required in
      all models.

   -  "C" indicates that the XML Element or XML Attribute is required in
      all models if the condition stated in the Description is met.

   -  "O" indicates that the XML Element or XML Attribute is optional.

   -  If the XML Element or XML Attribute is nested inside another XML
      Element, and that enclosing XML Element is not present (i.e., it
      is defined with an Optionality of "O" and is not present in the
      XML Infoset, or it is defined with an Optionality of "RC" and is
      not included in the XML Infoset because the condition was not
      met), then the nested XML Element or XML Attribute shall not be
      present in the XML Infoset irrespective of its optionality.

5. The entries in the "Cardinality" column have the following
   interpretations:

   -  "A" indicates that this is represented as an XML Attribute instead
      of an XML Element, hence has a cardinality of 1 by definition.

   -  "1" indicates that only a single instance of this XML Element is
      included inside the immediately enclosing XML Element, or at the
      top level if this XML Element is not nested inside another XML
      Element.

   -  "0-n" indicates that zero to n instances of this XML Element are
      included inside the immediately enclosing XML Element, or at the
      top level if this XML Element is not nested inside another XML
      Element.

   -  "1-n" indicates that one to n instances of this XML Element are
      included inside the immediately enclosing XML Element, or at the
      top level if this XML Element is not nested inside another XML
      Element.

6. Sets of XML Elements and XML Attributes that are often repeated
   within models may be defined as macros. Macros that may have general
   applicability are defined in this section. Macros that are unique to
   a particular model may be defined in the Annex specific that model.
   When a macro is included within a table, it is as if the contents of
   the Macro's table were inserted within the table referencing the
   macro. Any set of ">" characters in front of the directive to include
   a Macro in the table are prepended to the XML Element and XML
   Attribute names listed in the Macro's table.

.. _sect_10.1:

Coded Terminology
-----------------

Models may make use of coded terminology. The representation of coded
terminology in DICOM is described in . Specific terminology of interest,
organized in Context Groups in , can be referenced using the following
macro.

.. table:: Basic Coded Terminology Macro

   +-------------------+-------------+-------------+-------------------+
   | Name              | Optionality | Cardinality | Description       |
   +===================+=============+=============+===================+
   | CodeValue         | R           | 1           | The particular    |
   |                   |             |             | code value        |
   |                   |             |             | identifying the   |
   |                   |             |             | referenced term   |
   |                   |             |             | or concept. See . |
   |                   |             |             |                   |
   |                   |             |             | The same XML      |
   |                   |             |             | Element CodeValue |
   |                   |             |             | is used           |
   |                   |             |             | regardless of the |
   |                   |             |             | length or         |
   |                   |             |             | encoding of the   |
   |                   |             |             | code value. I.e., |
   |                   |             |             | separate XML      |
   |                   |             |             | elements are not  |
   |                   |             |             | used when the     |
   |                   |             |             | value is obtained |
   |                   |             |             | from Long Code    |
   |                   |             |             | Value (0008,0119) |
   |                   |             |             | or URN Code Value |
   |                   |             |             | (0008,0120)       |
   |                   |             |             | rather than Code  |
   |                   |             |             | Value             |
   |                   |             |             | (0008,0100).      |
   +-------------------+-------------+-------------+-------------------+
   | Codin             | R           | 1           | Designates the    |
   | gSchemeDesignator |             |             | coding scheme in  |
   |                   |             |             | which the         |
   |                   |             |             | CodeValue is      |
   |                   |             |             | defined. See .    |
   +-------------------+-------------+-------------+-------------------+
   | Co                | C           | 1           | See . Required if |
   | dingSchemeVersion |             |             | the               |
   |                   |             |             | Codin             |
   |                   |             |             | gSchemeDesignator |
   |                   |             |             | is not sufficient |
   |                   |             |             | to identify the   |
   |                   |             |             | CodeValue         |
   |                   |             |             | unambiguously.    |
   |                   |             |             | May be present    |
   |                   |             |             | otherwise.        |
   +-------------------+-------------+-------------+-------------------+
   | CodeMeaning       | O           | 0-1         | A brief human     |
   |                   |             |             | readable          |
   |                   |             |             | description of    |
   |                   |             |             | what the coded    |
   |                   |             |             | value means. See  |
   |                   |             |             | .                 |
   +-------------------+-------------+-------------+-------------------+

.. table:: Enhanced Coded Terminology Macro

   +-------------------+-------------+-------------+-------------------+
   | Name              | Optionality | Cardinality | Description       |
   +===================+=============+=============+===================+
   | ContextIdentifier | O           | 0-1         | Identifies a      |
   |                   |             |             | Context Group     |
   |                   |             |             | defined within a  |
   |                   |             |             | Mapping Resource  |
   |                   |             |             | from which the    |
   |                   |             |             | values of         |
   |                   |             |             | CodeValue and     |
   |                   |             |             | CodeMeaning were  |
   |                   |             |             | selected or have  |
   |                   |             |             | been added as a   |
   |                   |             |             | Private Context   |
   |                   |             |             | Group extension.  |
   |                   |             |             | See and .         |
   +-------------------+-------------+-------------+-------------------+
   | ContextUID        | O           | 0-1         | Uniquely          |
   |                   |             |             | identifies the    |
   |                   |             |             | Context Group.    |
   |                   |             |             | See .             |
   +-------------------+-------------+-------------+-------------------+
   | MappingResource   | C           | 1           | See . Required if |
   |                   |             |             | ContextIdentifier |
   |                   |             |             | is present.       |
   +-------------------+-------------+-------------+-------------------+
   | M                 | O           | 0-1         | Uniquely          |
   | appingResourceUID |             |             | identifies the    |
   |                   |             |             | Mapping Resource  |
   |                   |             |             | that defines the  |
   |                   |             |             | Context Group.    |
   +-------------------+-------------+-------------+-------------------+
   | Ma                | O           | 0-1         | Name of Mapping   |
   | ppingResourceName |             |             | Resource like     |
   |                   |             |             | name of an        |
   |                   |             |             | Institution or    |
   |                   |             |             | Organization.     |
   +-------------------+-------------+-------------+-------------------+
   | Co                | C           | 1           | See . Required if |
   | ntextGroupVersion |             |             | ContextIdentifier |
   |                   |             |             | is present.       |
   +-------------------+-------------+-------------+-------------------+
   | ContextG          | O           | 0-1         | Indicates whether |
   | roupExtensionFlag |             |             | the Coded Term is |
   |                   |             |             | selected from a   |
   |                   |             |             | private extension |
   |                   |             |             | of the Context    |
   |                   |             |             | Group identified  |
   |                   |             |             | in the            |
   |                   |             |             | C                 |
   |                   |             |             | ontextIdentifier. |
   |                   |             |             | See .             |
   |                   |             |             |                   |
   |                   |             |             | Enumerated        |
   |                   |             |             | Values:           |
   |                   |             |             |                   |
   |                   |             |             | "Y"               |
   |                   |             |             |                   |
   |                   |             |             | "N"               |
   +-------------------+-------------+-------------+-------------------+
   | Context           | C           | 1           | See . Required if |
   | GroupLocalVersion |             |             | the value of      |
   |                   |             |             | ContextG          |
   |                   |             |             | roupExtensionFlag |
   |                   |             |             | is "Y".           |
   +-------------------+-------------+-------------+-------------------+
   | ContextGroupEx    | C           | 1           | Identifies the    |
   | tensionCreatorUID |             |             | person or         |
   |                   |             |             | organization who  |
   |                   |             |             | created an        |
   |                   |             |             | extension to the  |
   |                   |             |             | Context Group.    |
   |                   |             |             | See .             |
   |                   |             |             |                   |
   |                   |             |             | Required if the   |
   |                   |             |             | value of          |
   |                   |             |             | contextG          |
   |                   |             |             | roupExtensionFlag |
   |                   |             |             | is "Y".           |
   +-------------------+-------------+-------------+-------------------+

.. table:: Coded Terminology Macro

   +-----------------+-------------+-----------------+-----------------+
   | Name            | Optionality | Cardinality     | Description     |
   +=================+=============+=================+=================+
   | *BASIC CODED    |             |                 |                 |
   | ENTRY           |             |                 |                 |
   | ATTRIBUTES*     |             |                 |                 |
   +-----------------+-------------+-----------------+-----------------+
   | *Include*\ `t   |             |                 |                 |
   | able_title <#ta |             |                 |                 |
   | ble_10.1-1a>`__ |             |                 |                 |
   +-----------------+-------------+-----------------+-----------------+
   | DicomAttribute  | O           | 0-1 with 1-n    | Codes that are  |
   | that encodes    |             | Item            | considered      |
   | Equival         |             |                 | equivalent by   |
   | entCodeSequence |             |                 | the creating    |
   |                 |             |                 | system.         |
   |                 |             |                 |                 |
   |                 |             |                 | See .           |
   +-----------------+-------------+-----------------+-----------------+
   | *>Include*\ `t  |             |                 |                 |
   | able_title <#ta |             |                 |                 |
   | ble_10.1-1a>`__ |             |                 |                 |
   +-----------------+-------------+-----------------+-----------------+
   | *>Include*\ `t  |             |                 |                 |
   | able_title <#ta |             |                 |                 |
   | ble_10.1-1b>`__ |             |                 |                 |
   +-----------------+-------------+-----------------+-----------------+
   | *ENHANCED       |             |                 |                 |
   | ENCODING MODE*  |             |                 |                 |
   +-----------------+-------------+-----------------+-----------------+
   | *Include*\ `t   |             |                 |                 |
   | able_title <#ta |             |                 |                 |
   | ble_10.1-1b>`__ |             |                 |                 |
   +-----------------+-------------+-----------------+-----------------+

.. _sect_10.2:

Person Name Components
----------------------

The Person Name Components follow the definitions given in of the DICOM
Standard. The description of the usage of Person Name Components also
applies to this macro.

.. table:: Person Name Components Macro

   +------------+-------------+-------------+--------------------------+
   | Name       | Optionality | Cardinality | Description              |
   +============+=============+=============+==========================+
   | FamilyName | O           | 0-1         | The person's family or   |
   |            |             |             | last name. See the       |
   |            |             |             | description of the PN VR |
   |            |             |             | in DICOM .               |
   +------------+-------------+-------------+--------------------------+
   | GivenName  | O           | 0-1         | The person's given or    |
   |            |             |             | first names. See the     |
   |            |             |             | description of the PN VR |
   |            |             |             | in DICOM .               |
   +------------+-------------+-------------+--------------------------+
   | MiddleName | O           | 0-1         | The person's middle      |
   |            |             |             | names. See the           |
   |            |             |             | description of the PN VR |
   |            |             |             | in DICOM .               |
   +------------+-------------+-------------+--------------------------+
   | NamePrefix | O           | 0-1         | The person's name        |
   |            |             |             | prefix. See the          |
   |            |             |             | description of the PN VR |
   |            |             |             | in DICOM .               |
   +------------+-------------+-------------+--------------------------+
   | NameSuffix | O           | 0-1         | The person's name        |
   |            |             |             | suffix. See the          |
   |            |             |             | description of the PN VR |
   |            |             |             | in DICOM .               |
   +------------+-------------+-------------+--------------------------+

