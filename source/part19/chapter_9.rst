.. _chapter_9:

Data Types and Structures
=========================

.. _sect_9.1:

Arrayof[type]
-------------

A wrapper object representing the encapsulation of an array of a
specific type. Used in parameters to and return values from API
functions to enable cross-platform compatibility. The wrapper contains a
single field, which is an array of the type being stored. The field name
is the Type name with the first letter in lowercase instead of
uppercase.

.. note::

   This construct was needed to support Microsoft® .NET language
   bindings even though it looks ugly in Java.

.. _sect_9.2:

AvailableData
-------------

A data structure that communicates what data is available to the
recipient. The data is organized in a hierarchical fashion,
communicating patients, studies, series, and finally ObjectDescriptors
that identify available data objects. The fields in the data structure
are:

-  ObjectDescriptors : ObjectDescriptor[] - An array of ObjectDescriptor
   data structures listing data that either applies to multiple
   patients, or does not fit into the patient / study / series
   hierarchy.

-  Patients : Patient[] - An array of Patient data structures.

.. _sect_9.2.1:

ObjectDescriptor
~~~~~~~~~~~~~~~~

A data structure with the following fields:

-  DescriptorUUID : UUID - the UUID that the interface utilizes to track
   this particular data object.

-  MimeType : MimeType - the MIME content type of this particular data
   object, in its most natural form available from the source. The most
   natural form is typically the form in which the source maintains the
   data in its database, for example a DICOM file.

-  ClassUID : UID - the UID that represents the class of this data
   object in the form described by mimeType. For objects whose mimeType
   refers to a data exchange model such as those defined in `Data
   Exchange Models <#chapter_A>`__, this is the UID of that model. For
   objects whose mimeType is application/dicom, this is the SOP Class
   UID of the DICOM object. This may be empty for those objects whose
   MIME content types have no additional classes.

-  TransferSyntaxUID : UID - the UID that represents the Transfer Syntax
   of this data object in the form described by mimeType. This may be
   empty for those objects of a MIME content type where Transfer Syntax
   has no meaning.

-  Modality : String - the modality that best represents where this data
   originated from. Standard values are drawn from the Defined Terms
   listed for the Modality (0008,0060) Attribute in the .

.. _sect_9.2.2:

Patient
~~~~~~~

A data structure that communicates data for a particular patient. The
fields in the data structure are:

-  Name : String - The name of the patient, formatted as described for
   the PN VR in . For DICOM SOP Instances this is the value of the
   Patient's Name (0010,0010) Attribute.

-  ID : String - A string used as the identifier for a particular
   patient, formatted as described for the LO VR in . For DICOM SOP
   Instances this is the value of the Patient ID (0010,0020) Attribute.

-  AssigningAuthority : String - The organization who assigned the id to
   the patient, formatted as described for the LO VR in . For DICOM SOP
   Instances this is the value of the Issuer of Patient ID (0010,0021)
   Attribute.

-  Sex : String - The sex of the patient. For DICOM SOP Instances this
   is the value of the Patient's Sex (0010,0040) Attribute. In all other
   cases it shall take on the values permissible for the DICOM Sex
   (0010,0040) Attribute.

-  BirthDate: String The birth date of the patient, formatted as
   described for the DA VR in . For DICOM SOP Instances this is the
   value of the Patient's Birth Date (0010,0030) Attribute.

-  ObjectDescriptors : ObjectDescriptor[] - An array of ObjectDescriptor
   data structures listing data that applies to this patient, but that
   do not apply to any particular study of this patient.

-  Studies : Study[] - An array of Study data structures.

At least one of objectDescriptors or studies shall be present.

.. _sect_9.2.3:

Study
~~~~~

A data structure that communicates data for a particular study. The
fields in the data structure are:

-  StudyUID : UID - The UID of the study. For DICOM SOP Instances this
   is the value of the Study Instance UID (0020,000D) Attribute.

-  ObjectDescriptors : ObjectDescriptor[] - An array of ObjectDescriptor
   data structures listing data that applies to this study (within the
   enclosing patient), but that do not apply to any particular series
   within this study.

-  Series : Series[] - An array of Series data structures.

.. _sect_9.2.4:

Series
~~~~~~

A data structure that communicates data for a particular series. The
fields in the data structure are:

-  SeriesUID : UID - The UID of the series. For DICOM SOP Instances this
   is the value of the Series Instance UID (0020,000E) Attribute.

-  ObjectDescriptors : ObjectDescriptor - An array of ObjectDescriptor
   data structures listing data existing in this series (within the
   enclosing Study, within the enclosing Patient).

.. note::

   Most DICOM Composite SOP Instances would be identified by
   objectDescriptors at the Series level.

.. _sect_9.3:

MimeType
--------

A data type whose values are Defined Terms that identify particular MIME
content types. The syntax of the string defining a MIME content type is
defined in IETF RFC2045. Top level MIME content types are defined in
IETF RFC2046. MIME content types are drawn from the list managed by the
Internet Assigned Numbers Authority (IANA) whose web site is at
http://www.iana.org/assignments/media-types/, as described in IETF
RFC2048.

.. _sect_9.4:

ModelSetDescriptor
------------------

A data structure returned from the getAsModels() method with the
following fields:

-  InfosetType : MimeType - the MIME type of the infoset, selected by
   the source of the data from the list passed to it by the recipient in
   a getAsModels() call.

-  Models : UUID[] - an array of UUIDs referring to models that have
   been created from the set of data objects referred to by the array of
   UUIDs passed into the getAsModels() call.

-  FailedSourceObjects : UUID[] - an array of UUIDs designating data
   objects referred to the array of UUIDs passed into the getAsModels()
   call that could not be represented in the requested model class.

.. note::

   For example, if the array of UUIDs passed into the getAsModels() call
   includes 100 CT slices from the same frame of reference (i.e., a
   volume stack), plus 1 GSPS object, and if the caller requested an
   Abstract Multi-Dimensional Image model, then the ModelSetDescriptor
   returned by GetAsModels() would include one UUID in the models array,
   identifying the CT volume image data created from the 100 CT slices,
   and one UUID in the failedSourceObjects array, specifying the UUID
   for the GSPS object.

.. _sect_9.5:

ObjectLocator
-------------

A data structure that represents the location from which the recipient
of a data object can retrieve that object. It consists of the following
fields:

-  Locator : UUID - the UUID that the interface utilizes to track this
   particular ObjectLocator.

-  Source : UUID - the UUID of the source that is supplying data for
   this ObjectLocator. This UUID matches the UUID in the
   ObjectDescriptor if trying to retrieve the data in its natural form
   (e.g., as a file or byte stream). This UUID matches the UUID in a
   bulk data pointer when retrieving bulk data from a model.

-  TransferSyntax : UID - the transfer syntax in which this data is
   encoded, selected by source of the data from the list passed in by
   the recipient of the data in the acceptableTransferSyntaxUIDs
   parameter of the getData() call. This may be empty for those objects
   of a MIME content type where Transfer Syntax has no meaning.

-  Length: long - the length of the data object referred to by the UUID.

-  Offset: long - the offset within the file or byte stream where the
   data object begins.

-  URI: URI - the URI that identifies the resource from which the
   recipient might retrieve the data object, typically but not limited
   to a file on the local file system. The recipient shall be able to
   access the data within the object using file IO or memory mapping.

.. _sect_9.6:

QueryResult
-----------

A data structure that holds the results from an XPath query of a model.
It consists of the following fields:

-  Model : UUID - the UUID of the model from which this result came.

-  XPath : String - the XPath query string that led to this result.

-  Results : XPathNode[] - an array of XPathNodes holding the query
   results.

.. _sect_9.7:

QueryResultInfoset
------------------

A data structure that holds the results from an XPath query of a model.
It consists of the following fields:

-  Model : UUID - the UUID of the model from which this result came.

-  XPath : String - the XPath query string that led to this result.

-  Results : XPathNodeInfoset[] - an array of XPathNodeInfoset
   structures holding the query results.

.. _sect_9.8:

Rectangle
---------

A data structure that defines a rectangular region on a display screen.
The fields in the data structure are:

-  RefPointX : int

-  RefPointY : int

that define the location of the top left corner of the region in screen
coordinates, and

-  Width : int

-  Height : int

that specify the extents of the region. Screen coordinates are defined
starting from an origin of 0,0 in the upper left corner of the screen,
and extend in the positive direction down and to the right.

.. _sect_9.9:

State
-----

State is an enumerated data type with the following values:

-  IDLE

-  INPROGRESS

-  COMPLETED

-  SUSPENDED

-  CANCELED

-  EXIT

The interpretation of these enumerated values is defined in section7.2
States.

.. _sect_9.10:

Status
------

A data structure with the following fields:

-  StatusType : StatusType - the severity level of this status message.

-  CodingSchemeDesignator : String - the coding scheme in which the
   codeValues are defined. The use of codeValue shall be consistent with
   the use of the DICOM Code Value (0008,0100) Attribute as specified in
   .

-  CodeValue : String - the particular code value within the designated
   coding scheme that represents the nature of this status message. The
   use of message shall be consistent with the use of the DICOM Code
   Meaning (0008,0104) Attribute as specified in .

-  CodeMeaning : String - a displayable string for the code value. The
   use of message shall be consistent with the use of the DICOM Code
   Meaning (0008,0104) Attribute as specified in .

-  Any other field from the Coded Terminology macro defined in `Coded
   Terminology <#sect_10.1>`__.

.. _sect_9.10.1:

StatusType
~~~~~~~~~~

An enumerated data type with the following values and definitions:

-  INFORMATION - the status is for informational purposes only.

-  WARNING - indicates a condition that might impact the speed or
   quality of the work done by the Hosted Application, but that does not
   prevent the Hosted Application from completing its task.

-  ERROR - indicates a condition that might prevent the Hosted
   Application from correctly completing its task. The Hosted
   Application will attempt to continue.

-  FATALERROR - indicates a condition that prevents the Hosted
   Application from completing its task. The Hosted Application will not
   attempt to continue, and will transition automatically to the
   CANCELED state.

.. _sect_9.11:

UID
---

A string of period-separated digits representing a Unique Identifier
(see ), formatted as described for the UI VR in .

.. _sect_9.12:

UUID
----

A string representing a Universally Unique Identifier as defined in
ITU-T Recommendation X.667, using the hexadecimal representation form.

.. _sect_9.13:

XPathNode
---------

A data structure with the following fields, which represents the output
from an XPath query of a model, returned in a string-based
representation.

-  NodeType : XPathNodeType

-  Value : String

.. _sect_9.14:

XPathNodeInfoset
----------------

A data structure with the following fields, which represents the output
from an XPath query of a model returned in a byte array representation.

-  NodeType : XPathNodeType

-  InfosetValue : byte[]

.. _sect_9.15:

XPathNodeType
-------------

An enumeration of the types of results that may come back from an XPath
query.

.. note::

   This enumeration is compatible with a similar enumeration utilized in
   the Microsoft .NET framework.

-  Root - the result is the top level node of the XML Infoset (i.e., the
   result is the entire XML Infoset).

-  Element - the result is an XML Element within the XML Infoset (i.e.,
   the result is a subset of the XML Infoset).

-  Attribute - the result is an XML Attribute of an XML Element within
   the XML Infoset.

-  Text - the result is the textual content of an XML Element within the
   XML Infoset. Equivalent to the Document Object Model (DOM) Text and
   CDATA node types. Contains at least one character.

-  SignificantWhitespace - the result is the content of an XML Element
   within the XML Infoset, where the content consists only of
   significant whitespace (e.g., xml:space was set to preserve). White
   space code points are SPACE (U0020), TAB (U0009), CARRIAGE RETURN
   (U000D), or LINE FEED (U000A) of ISO 10646 (Unicode).

-  Whitespace - the result is the content of an XML Element within the
   XML Infoset, where the content consists only of whitespace. White
   space code points are SPACE (U0020), TAB (U0009), CARRIAGE RETURN
   (U000D), or LINE FEED (U000A) of ISO 10646 (Unicode).

-  Comment - the result is a comment within the XML Infoset.

-  Namespace - the result is a namespace directive within the XML
   Infoset.

-  ProcessingInstruction - the result is a processing instruction within
   the XML Infoset.

-  All - the result may contain any of the types defined in
   XPathNodeType.

