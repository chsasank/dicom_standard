.. _chapter_3:

Definitions
===========

For the purposes of this Part of DICOM, the following terms and
definitions apply.

Application Entity
   See `biblioentry_title <#biblio_ISO7498-1>`__.

Real-World Activity
   See `biblioentry_title <#biblio_ISO7498-1>`__.

Service-Object Pair Class
   .

DICOM Message Service Element
   .

Multi-frame Image
   .

Conformance Statement
   .

Data Element
   .

Data Element Tag
   .

Data Set
   .

Sequence of Items
   .

Unique Identifier
   .

Service-Object Pair Instance
   .

HTTP
   See `biblioentry_title <#biblio_RFC_7230>`__.

HTTPS
   See `biblioentry_title <#biblio_RFC_7230>`__.

origin server
   See `biblioentry_title <#biblio_RFC_7230>`__.

user agent
   See `biblioentry_title <#biblio_RFC_7230>`__.

Bulk Data
   An object that contains an octet-stream containing one or more Value
   Fields (typically containing large data, such as Pixel Data)
   extracted from a DICOM Dataset. See
   `Metadata <#glossentry_Metadata>`__.

   .. note::

      1. The octet-stream does not include the Attribute Tag, Value
         Representation, or Attribute Length.

      2. For the value of a frame of a Pixel Data Attribute encoded in a
         compressed Transfer Syntax, it does not include the Basic
         Offset Table and Data Stream Fragment Item tags and lengths.

Bulk Data URI
   A Uniform Resource Identifier that references Bulkdata.

DICOM Object
   An instance of a data object as defined by that has been allocated an
   unique identifier in the format specified for SOP Instance UID in and
   has been chosen as an object to be saved securely for some period of
   time. Within the DICOM Standard, a DICOM Object is typically a
   Composite Service Object Pair (SOP) Instance.

DICOM Resource
   One or more DICOM Objects that are referenced by a URL.

DIMSE Proxy
   An origin server that responds to DICOM Web Service requests by
   executing DIMSE transactions to a backend server.

Event Report
   A Dataset containing elements describing an event that occurred on
   the origin server. See `Suspend Global Subscription
   Transaction <#sect_11.12>`__.

Metadata
   A DICOM Dataset where zero or more elements (typically containing
   large data, such as Pixel Data) have been replaced with Bulkdata
   URIs.

RESTful Web Service
   A web service is RESTful if it is implemented using the REST
   architecture and principles. See
   https://en.wikipedia.org/wiki/Representational_state_transfer.

Service
   When used in this Part of the Standard the term Service means a set
   of transactions and resources to which those transactions apply.

sRGB
   A standard RGB color space defined in
   `biblioentry_title <#biblio_IEC61966-2.1>`__.

Status Report
   A Status Report is information contained in a response payload
   describing warnings or errors related to a request.

Subscriber
   The creator or owner of a Subscription, typically a user agent.

Target URI
   The URI contained in a request message. It designates the resource
   that is the target of the request.

Thumbnail
   A single frame image that is representative of the content of a DICOM
   Study, Series, Instance, or Frame. It is encoded in a Rendered Media
   Type. See `Rendered Media Types <#sect_8.7.4>`__ and `Media
   Types <#sect_10.4.4>`__.

Transaction
   When used in this Part of the Standard the term Transaction means an
   HTTP/HTTPS request/response message pair.

UTF-8
   Unicode UTF-8 character set defined in
   `biblioentry_title <#biblio_ISOIEC10646>`__.

