.. _chapter_8:

Common Aspects of DICOM Web Services
====================================

This section describes details and requirements that are common to all
Web Services defined in this Part of the Standard.

A user agent or origin server that implements a Service in this Part of
the Standard shall conform to `Common Aspects of DICOM Web
Services <#chapter_8>`__ unless stated otherwise in the specification of
that Service and its Transactions.

.. _sect_8.1:

Transactions
------------

Each transaction is composed of a request message and a response
message, sometimes referred to as a request/response pair. When used in
this Part of the Standard the term "request" means "request message",
and "response" means "response message", unless clearly stated
otherwise. `figure_title <#figure_8.1-1>`__ is an interaction diagram
that shows the message flow of a transaction. When it receives the
request, the origin server processes it and returns a response.

The request includes a method, the URI of the Target Resource, and
header fields. It might also include Query Parameters and a payload.

The response includes a status code, a reason phrase, header fields, and
might also include a payload.

.. _sect_8.1.1:

Request Message Syntax
~~~~~~~~~~~~~~~~~~~~~~

This Part of the Standard uses the ABNF defined in `Message
Syntax <#sect_5.1>`__ to define the syntax of transactions.

All Web Services API request messages have the following syntax:

::

   method SP target-uri SP version CRLF

::

   *(header-field CRLF)

::

   CRLF

::

   [payload]

Where

+----------------------------------+----------------------------------+
| ::                               | Each transaction defines the     |
|                                  | method it uses.                  |
|    method = "C                   |                                  |
| ONNECT" / "DELETE" / "GET" / "HE |                                  |
| AD" / "OPTIONS" / "POST" / "PUT" |                                  |
+----------------------------------+----------------------------------+
| ::                               | The US-ASCII Space character     |
|                                  |                                  |
|    SP= %x20                      |                                  |
+----------------------------------+----------------------------------+
| ::                               | Each transaction defines a URI   |
|                                  | Template for the Target          |
|    target-uri                    | Resource. The template specifies |
| = "/" {/resource} {?parameters*} | the format of URIs that          |
|                                  | reference the Target Resource of |
|                                  | a request. See `Target           |
|                                  | Resource <#sect_8.1.1.2>`__.     |
+----------------------------------+----------------------------------+
| ::                               | The version of the HTTP          |
|                                  | protocol; one of "HTTP/1.1",     |
|    version = ("HT                | "HTTP/2", "HTTPS/1.1", or        |
| TP" / "HTTPS") "/" ("1.1" / "2") | "HTTPS/2".                       |
+----------------------------------+----------------------------------+
| ::                               | A US-ASCII carriage return       |
|                                  | (%x0D) followed by a linefeed    |
|    CRLF = %x0D.0A                | (%x0A).                          |
+----------------------------------+----------------------------------+
| ::                               | Zero or more header fields each  |
|                                  | followed by a CRLF delimiter.    |
|    *(header-field CRLF)          |                                  |
+----------------------------------+----------------------------------+
| ::                               | An optional payload containing   |
|                                  | zero or more 8-bit OCTETs.       |
|    [paylo                        |                                  |
| ad] = *OCTET / multipart-payload |                                  |
+----------------------------------+----------------------------------+

.. note::

   The method, SP, version, CRLF, Accept, header-field, and payload are
   all HTTP productions from `biblioentry_title <#biblio_RFC_7230>`__,
   and `biblioentry_title <#biblio_RFC_7231>`__. The definitions are
   reproduced here for convenience.

.. _sect_8.1.1.1:

Method
^^^^^^

The request method is one of the HTTP methods, such as CONNECT, DELETE,
GET, HEAD, OPTIONS, POST, PUT. See
`biblioentry_title <#biblio_RFC_7230>`__ `Section
4 <http://tools.ietf.org/html/rfc7230#section-4>`__.

.. _sect_8.1.1.2:

Target Resource
^^^^^^^^^^^^^^^

The Target Resource of a request is specified by the Target URI
contained in the request message. See `Target Resources <#sect_8.2>`__.

.. _sect_8.1.1.3:

Query Parameters
^^^^^^^^^^^^^^^^

Query parameters are contained in the query component (see
`biblioentry_title <#biblio_RFC_3986>`__) of the URI. The user agent may
use Query Parameters to supply parameters to the request. See `Query
Parameters <#sect_8.3>`__.

.. _sect_8.1.1.4:

Request Header Fields
^^^^^^^^^^^^^^^^^^^^^

Request header fields are used to specify metadata for the request. Most
requests have one or more Content Negotiation (see `Content Negotiation
Header Fields <#sect_8.4.1>`__) header fields. If a request has a
payload, the request will have the corresponding Content Representation
(see `Content Representation Header Fields <#sect_8.4.2>`__) and Payload
(see `Payload Header Fields <#sect_8.4.3>`__) header fields.

.. _sect_8.1.1.5:

Request Payload
^^^^^^^^^^^^^^^

The payload of the request is an octet-stream containing the content of
the message. See `Payloads <#sect_8.6>`__. The presence of a payload in
a request is signaled by a Content-Length or Content-Encoding header
field.

.. _sect_8.1.2:

Response Message Syntax
~~~~~~~~~~~~~~~~~~~~~~~

The syntax of a response message is:

::

   versionSP status-codeSP reason-phrase CRLF

::

   *(header-field CRLF)

::

   CRLF

::

   [payload]

Where

+----------------------------------+----------------------------------+
| ::                               | A three-digit code specifying    |
|                                  | the status of the response.      |
|    status-code = 3DIGIT          |                                  |
+----------------------------------+----------------------------------+
| ::                               | A human readable phrase that     |
|                                  | corresponds to the status. An    |
|    reas                          | implementation may define its    |
| on-phrase = *(HTAB / SP / VCHAR) | own reason phrases. The          |
|                                  | reason-phrase syntax is slightly |
|                                  | modified from that in            |
|                                  | `biblioen                        |
|                                  | try_title <#biblio_RFC_7230>`__; |
|                                  | this Part of the Standard does   |
|                                  | not allow obsolete text          |
|                                  | (obs-text) in the reason-phrase. |
+----------------------------------+----------------------------------+

.. note::

   The status-code production is from
   `biblioentry_title <#biblio_RFC_7230>`__.

The origin server shall always return a response message.

.. _sect_8.1.2.1:

Status Codes
^^^^^^^^^^^^

The response message shall always include a valid 3-digit status code.
`Status Codes <#sect_8.5>`__ defines the status codes used by
transactions. IANA maintains a registry of HTTP Status codes. See
`biblioentry_title <#biblio_IANA_HTTPStatusCodeRegistry>`__.

.. _sect_8.1.2.2:

Response Header Fields
^^^^^^^^^^^^^^^^^^^^^^

Response header fields are used to specify metadata for the response.
The response will have the Content Representation (see `Content
Representation Header Fields <#sect_8.4.2>`__) and Payload (see `Payload
Header Fields <#sect_8.4.3>`__) header fields that correspond to the
contents of the payload.

.. _sect_8.1.2.3:

Response Payload
^^^^^^^^^^^^^^^^

The payload of the response is an octet-stream containing one or more
representations. See `Payloads <#sect_8.6>`__.

A transaction typically defines two types of payloads for a response
message: a success payload, and a failure payload.

A failure response payload should contain a Status Report describing any
failures, warnings, or other useful information.

.. _sect_8.2:

Target Resources
----------------

Transaction specifications define what resource types are valid Target
Resources for the transaction and define the format of the URI for the
Target Resource (and Query Parameters) using URI Templates. The URI of a
Target Resource is referred to as the Target URI. Transaction
specifications also define what resource types are valid resources for
the response.

A Target URI is composed of three components: The Base URI, the Target
Resource Path, and Query Parameters (which are often optional).

No whitespace is permitted in URIs. Whitespace around line breaks and
the line breaks themselves should be stripped before parsing the URI.
See `biblioentry_title <#biblio_RFC_3986>`__ Appendix C.

The most general template for a Target URI is:

::

   target-uri = "/" {/resource} {?optional*}

or if any of the Query Parameters are required

::

   target-uri = "/" {/resource} ?{required*}{&optional*}

Where

+-----------------+---------------------------------------------------+
| ::              | The slash character ('/') is used to designate    |
|                 | the Base URI.                                     |
|    "/"          |                                                   |
+-----------------+---------------------------------------------------+
| ::              | A URI template for the Target Resource Path, a    |
|                 | relative path component that references the       |
|    {/resource}  | Target Resource. The '/' in the template          |
|                 | indicates that reserved characters, such as '/',  |
|                 | can be used in the template expansion. See        |
|                 | `biblioentry_title <#biblio_RFC_6570>`__.         |
|                 |                                                   |
|                 | "/{/resource}" indicates the absolute URI to the  |
|                 | Target Resource on the origin server.             |
+-----------------+---------------------------------------------------+
| ::              | A URI Template for one or more required query     |
|                 | parameters. See `Request Message                  |
|    {required*}  | Syntax <#sect_8.1.1>`__ for an example.           |
+-----------------+---------------------------------------------------+
| ::              | A URI Template for zero or more optional query    |
|                 | parameters. See `Query Parameter                  |
|    {&optional*) | Syntax <#sect_8.3.1>`__ for an example.           |
+-----------------+---------------------------------------------------+

The Base URI of a Service is an absolute URI that specifies the location
of the origin server implementing the Service. Each Target URI defined
by this Part of the Standard starts with a "/", which is a shorthand
that designates the Base URI of the Service. The Base URI may support
more than one Service.

The Service Root Path is the Base URI without the Scheme and Authority
components.

The Target Resource Path is a relative URI that specifies the path to
the resource from the Base URI of the Service. It is specified by a URI
Template that uses Path Expansion {/var} as defined in
`biblioentry_title <#biblio_RFC_6570>`__.

For example, given the URI:

::

   http://dicom.nema.org/service/studies/2.25.123456789/series/2.25.987654321

The Base URI is:

::

   http://dicom.nema.org/service

The Service Root Path is:

::

   /service

The Target Resource Path is:

::

   /studies/2.25.123456789/series/2.25.987654321

The URI Template for this resource is:

::

   /studies/{study}/series/{series}

Where

=========== ======================================
::          is the Study Instance UID of a Study
            
   {study}  
::          is the Series Instance UID of a Series
            
   {series} 
=========== ======================================

.. _sect_8.3:

Query Parameters
----------------

Query Parameters are specified in the query component of the URI (see
`biblioentry_title <#biblio_RFC_3986>`__ `Section
3.4 <http://tools.ietf.org/html/rfc3986#section-3.4>`__.

The query component of a request URI may only be used to specify one or
more Query Parameters. These parameters are referred to as Query
Parameters to distinguish them from header field parameters or other
types of parameters that may be contained in the payload.

The Query Parameters are specified using a URI Template that uses Form
{?var} and Query Continuation Style {&var} Query Expansion as defined in
`biblioentry_title <#biblio_RFC_6570>`__.

If a Target URI includes a "query component" (see
`biblioentry_title <#biblio_RFC_3986>`__ `Section
3.4 <http://tools.ietf.org/html/rfc3986#section-3.4>`__), it shall
contain Query Parameters that conform to the syntax defined here.

The Services and Transactions defined elsewhere in this Part of the
Standard may further refine the qp-name and qp-value rules defined
below.

`biblioentry_title <#biblio_RFC_3986>`__ does not permit an empty query
component, i.e., if the "?" appears in the Target URI, then there shall
be at least one Query Parameter in the URI.

The origin server may define and support additional Query Parameters, or
additional Query Parameter values for an existing Query Parameter. If an
origin server defines new or extends existing Query Parameters, they
shall be documented in the Conformance Statement and, if the service
supports it, the Retrieve Capabilities response.

The origin server shall ignore any unsupported Query Parameters. The
origin server shall process the request as if the unsupported parameters
were not present and may return a response containing appropriate
warning and/or error messages.

If a supported Query Parameter has an invalid value, the origin server
shall return a 400 (Bad Request) error response and may include a
payload containing an appropriate Status Report.

.. _sect_8.3.1:

Query Parameter Syntax
~~~~~~~~~~~~~~~~~~~~~~

Query parameters have the following syntax:

::

   query-parameters = "?" parameter [*("&" parameter) ]

Each parameter after the first, is separated from the following
parameter by the "&" character. Each parameter has the following syntax:

::

   parameter = qp-name 
             / qp-name "=" 1#qp-value
             / qp-name "=" 1#attribute
             / attribute 
             / attribute "=" 1#qp-value

The qp-name is case sensitive, and starts with an alphabetic or
underscore character, followed by zero or more alphanumeric or
underscore "_" characters:

::

   qp-name = %s 1*(ALPHA / "_") *(ALPHA / DIGIT / "_")

A qp-name by itself (with no values) is a legal Query Parameter. A
parameter qp-name may also be followed by a comma-separated list of one
or more qp-values, or one or more Attributes.

The qp-values are case-sensitive. A qp-value is composed of qp-chars,
where qp-char is the set of legal query component characters as defined
by `biblioentry_title <#biblio_RFC_3986>`__, minus the equal ("="),
ampersand ("&"), and comma (",") characters.

::

   qp-value   = %s DQ 1*qp-char DQ
   qp-char    = unreserved / pct-encoded / qp-special
   qp-special = "!" / "$" / "'" / "(" / ")" / "*" / "+" / ";" /":" / "@" / "/" / "?"

The only visible US-ASCII characters disallowed in the query component
by `biblioentry_title <#biblio_RFC_3986>`__ are "#", "[", "]". This Part
of the Standard further disallows "&", "=", and ",". However, the
characters ("#", "[", "]" "&", "=", and ",".) may be included in
qp-values if they are percent encoded.

Each Attribute is either a simple-attribute or a sequence-attribute:

::

   attribute = simple-attribute / sequence-attribute

A simple-attribute is a single Data Element Tag or Keyword (see ) that
does not have a VR of SQ:

::

   simple-attribute = keyword / tag
   keyword          = %s DQ 1*ALPHA *(ALPHA / DIGIT) DQ
   tag              = 8HEXDIG

DICOM keywords are case sensitive; they shall start with an alphabetic
character followed by zero or more alphanumeric characters. See .

A sequence-attribute is two or more attributes separated by the dot
character ("."), all but the last attribute shall have a VR of SQ, and
the last attribute shall not have a VR of SQ.

sequence-attribute = (keyword / tag) \*("." attribute)

The following are examples of valid values for attribute:

::

   0020000D

::

   StudyInstanceUID

::

   00101002.00100020

::

   OtherPatientIDsSequence.PatientID

::

   00101002.00100024.00400032

::

   OtherPatientIDsSequence.IssuerOfPatientIDQualifiersSequence.UniversalEntityID

Some Query Parameters have a qp-name, which is an attribute, and a value
that is a comma-separated list of one or more qp-values. The qp-values
of an attribute parameter shall satisfy its Value Representation and
Value Multiplicity, as defined in and , of the corresponding attribute.

Unlike the Value Representations defined in , Query Parameters:

-  shall not be padded to an even length

-  shall not contain any NULL (%x00) characters

-  shall encode UIDs as specified in , except that they shall not be
   padded to an even length

.. _sect_8.3.1.1:

Query Parameter Syntax
^^^^^^^^^^^^^^^^^^^^^^

The syntax and semantics of valid qp-names, qp-values and attributes are
specified by the defining Service or Transaction; however, they shall
conform to the rules in this Section.

`table_title <#table_8.3.1-1>`__ contains the collected syntax of Query
Parameters. The Services and Transactions defined elsewhere in this Part
of the Standard may further refine the qp-name, attribute, and qp-value
rules.

All qp-names are case sensitive.

.. table:: ABNF for Query Parameter

   +-----------------------+---------------------------------------------+
   | Name                  | Rule                                        |
   +=======================+=============================================+
   | ::                    | ::                                          |
   |                       |                                             |
   |    query-parameters   |    = "?" parameter *("&" parameter)         |
   +-----------------------+---------------------------------------------+
   | ::                    | ::                                          |
   |                       |                                             |
   |    parameter          |    = qp-name; a name only                   |
   |                       |                                             |
   |                       | ::                                          |
   |                       |                                             |
   |                       |    / qp-name "="                            |
   |                       | 1#qp-value ; a name with one or more values |
   |                       |                                             |
   |                       | ::                                          |
   |                       |                                             |
   |                       |    / qp-name "=" 1#at                       |
   |                       | tribute; a name with one or more attributes |
   |                       |                                             |
   |                       | ::                                          |
   |                       |                                             |
   |                       |    / attribute; an attribute only           |
   |                       |                                             |
   |                       | ::                                          |
   |                       |                                             |
   |                       |    / attribute "=" 1#qp-v                   |
   |                       | alue ; an attribute with one or more values |
   +-----------------------+---------------------------------------------+
   | ::                    | ::                                          |
   |                       |                                             |
   |    qp-name            |                                             |
   |                       |   = %s (ALPHA / "_") *(ALPHA / DIGIT / "_") |
   +-----------------------+---------------------------------------------+
   | ::                    | ::                                          |
   |                       |                                             |
   |    qp-value           |    =int / uint / pos-i                      |
   |                       | nt / decimal / float /string / base64 / uid |
   |                       |                                             |
   |                       | ::                                          |
   |                       |                                             |
   |                       |                                             |
   |                       | / %s 1*qp-char/ %s DQ 1*qp-special DQ; See  |
   +-----------------------+---------------------------------------------+
   | ::                    | ::                                          |
   |                       |                                             |
   |    qp-char            |    = unreserved / pct-encoded               |
   +-----------------------+---------------------------------------------+
   | ::                    | ::                                          |
   |                       |                                             |
   |    qp-special         |    = "!" / "$" / "'" / "(" / "              |
   |                       | ) " / "*" / "+" / ";"/":" / "@" / "/" / "?" |
   +-----------------------+---------------------------------------------+
   | ::                    | ::                                          |
   |                       |                                             |
   |    simple-attribute   |    = keyword / tag                          |
   +-----------------------+---------------------------------------------+
   | ::                    | ::                                          |
   |                       |                                             |
   |    sequence-attribute |    = keyword                                |
   |                       |  *( "." attribute) / tag *( "." attribute ) |
   +-----------------------+---------------------------------------------+
   | ::                    | ::                                          |
   |                       |                                             |
   |    keyword            |    = %suppercase *( ALPHA / DIGIT )         |
   +-----------------------+---------------------------------------------+
   | ::                    | ::                                          |
   |                       |                                             |
   |    uppercase          |    =%x41-5A                                 |
   +-----------------------+---------------------------------------------+
   | ::                    | ::                                          |
   |                       |                                             |
   |    tag                |    = 8HEXDIG                                |
   +-----------------------+---------------------------------------------+

.. note::

   The syntax of qp-values is defined in `Common Syntactic Rules For
   Data Types <#sect_5.1.1>`__.

   The qp-char (Query Parameter characters) rule defined above is the
   query rule of `biblioentry_title <#biblio_RFC_3986>`__, which defines
   the legal characters for the query component, minus the equal sign
   ("="), comma (","), and ampersand ("&"). So, the qp-char rule is the
   VCHAR rule minus "#", "[", "]", "=", "&", and ",".

All DICOM keywords are case sensitive. See .

.. _sect_8.3.2:

Query Parameter Usage
~~~~~~~~~~~~~~~~~~~~~

An implementation's support for Query Parameters is either Mandatory or
Optional. Each Query Parameter section contains a table specifying Query
Parameter keys, values, user agent and origin server usage requirements.
`table_title <#table_8.3.2-1>`__ specifies the usage symbols, types, and
definitions.

.. table:: Query Parameter Usage

   ====== ===========
   Symbol Type
   ====== ===========
   M      Mandatory
   C      Conditional
   O      Optional
   ====== ===========

`table_title <#table_8.3.2-2>`__ shows an example Query Parameter table.

.. table:: Example Query Parameter Table

   +-------------+------------+-----------+-------------+--------------+
   | **Name**    | **Values** | **Usage** | **Section** |              |
   +=============+============+===========+=============+==============+
   | requestType | "WADO"     | M         | M           | `Request     |
   |             |            |           |             | T            |
   |             |            |           |             | ype <#sect_9 |
   |             |            |           |             | .1.2.1.1>`__ |
   +-------------+------------+-----------+-------------+--------------+
   | studyUID    | uid        | M         | M           | `Series      |
   |             |            |           |             | UID <#sect_9 |
   |             |            |           |             | .1.2.1.3>`__ |
   +-------------+------------+-----------+-------------+--------------+
   | seriesUID   | uid        | M         | M           | `Series      |
   |             |            |           |             | UID <#sect_9 |
   |             |            |           |             | .1.2.1.3>`__ |
   +-------------+------------+-----------+-------------+--------------+
   | objectUID   | uid        | M         | M           | `Instance    |
   |             |            |           |             | UID <#sect_9 |
   |             |            |           |             | .1.2.1.4>`__ |
   +-------------+------------+-----------+-------------+--------------+

The usage columns specify the Query Parameters that the user agent must
supply, and the origin server must support.

.. _sect_8.3.3:

Content Negotiation Query Parameters
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

The parameters defined in this section are primarily designed for use in
hyperlinks, i.e., URIs embedded in documents, where the Content
Negotiation header fields (see `Content Negotiation Query
Parameters <#sect_8.3.3>`__) are not accessible.

.. _sect_8.3.3.1:

Accept Query Parameter
^^^^^^^^^^^^^^^^^^^^^^

The Accept Query Parameter has the following syntax:

::

   accept      = accept-name "=" 1#(media-type [weight])
   accept-name = %s"accept"

The Accept Query Parameter has the same syntax as the Accept header
field (see `Payload Header Fields <#sect_8.4.3>`__), except that it
shall not have wildcards (<type>/\* or \*/*). See `Media
Types <#sect_8.7>`__.

.. note::

   1. The normal name of this parameter is "accept"; however, the URI
      Service uses an accept-name of "contentType". See `Acceptable
      Media Types <#sect_9.1.2.2.1>`__.

   2. The "%s" that prefixes the accept-name specifies that it is a case
      sensitive token. See `biblioentry_title <#biblio_RFC_7405>`__.

The parameter value is a comma-separated list of one or more
media-types.

The Accept Query Parameter should not be used when the user agent can
specify the values by using the Accept header field.

All media types present in an Accept Query Parameter shall be compatible
with a media range in the Accept header field, either explicitly or
implicitly through wildcards.

.. note::

   For example, the presence of image/jpeg in the Accept Query Parameter
   will require the Accept header field to include one or more of the
   following values: image/jpeg, image/*, or \*/*.

If none of the Acceptable Media Types (see `Acceptable Media
Types <#sect_8.7.5>`__) are supported by the origin server, the origin
server response shall be in the default media type for the Resource
Category of the Target Resource. If there is no default media type
defined for the Target Resource, the origin server response shall be 406
(Not Acceptable) and may include a payload containing an appropriate
Status Report.

If a DICOM Media Type is present, non-DICOM Media Types shall not be
present. If both DICOM and non-DICOM Media Types are present, the
response shall be 400 (Bad Request), and may include a payload
containing an appropriate Status Report.

.. _sect_8.3.3.2:

Character Set Query Parameter
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

The Character Set Query Parameter has the following syntax:

::

   character-set = "charset" "=" 1#(charset [weight])

The Character Set Query Parameter value is a comma-separated list of one
or more character set identifiers. It is like the Accept-Charset header
field, except that it shall not have wildcards. See `Character
Sets <#sect_8.8>`__.

.. note::

   Character set identifiers present in the character set Query
   Parameter typically have a corresponding character set identifier in
   the Accept-Charset header field, either explicitly or implicitly
   through wildcards.

If this parameter has a value that is not a valid or supported character
set, the origin server shall return a 400 (Bad Request) response and may
include a payload containing an appropriate Status Report. See `Status
Report <#sect_8.6.3>`__.

.. _sect_8.3.4:

Search Query Parameters
~~~~~~~~~~~~~~~~~~~~~~~

`table_title <#table_8.3.4-1>`__ contains the syntax for the names and
values of search parameters, along with a reference to the section where
their meaning is defined. Search transactions shall support these
parameters. The ABNF for the various search parameters is:

.. table:: Query Parameter Syntax

   +--------------+--------------+-------+-------------+--------------+
   | Term         | Value        | Usage | Description |              |
   +==============+==============+=======+=============+==============+
   | ::           | ::           |       |             |              |
   |              |              |       |             |              |
   |    search    |    =         |       |             |              |
   |              | match / fuzz |       |             |              |
   |              | ymatching /  |       |             |              |
   |              | includefield |       |             |              |
   |              |              |       |             |              |
   |              | ::           |       |             |              |
   |              |              |       |             |              |
   |              |    / li      |       |             |              |
   |              | mit / offset |       |             |              |
   +--------------+--------------+-------+-------------+--------------+
   | ::           | ::           | O     | M           | `Attribute   |
   |              |              |       |             | Mat          |
   |    match     |              |       |             | ching <#sect |
   |              | ; See attrib |       |             | _8.3.4.1>`__ |
   |              | ute matching |       |             |              |
   |              |  rules below |       |             |              |
   +--------------+--------------+-------+-------------+--------------+
   | ::           | ::           | O     | M           | `Fuzzy       |
   |              |              |       |             | Matching of  |
   |    f         |              |       |             | Person       |
   | uzzymatching |   = "fuzzyma |       |             | Names <#sect |
   |              | tching" "="  |       |             | _8.3.4.2>`__ |
   |              | true / false |       |             |              |
   +--------------+--------------+-------+-------------+--------------+
   | ::           | ::           | O     | M           | `Attributes  |
   |              |              |       |             | Included in  |
   |              |    = "i      |       |             | the          |
   | includefield | ncludefield" |       |             | Res          |
   |              |  "=" 1#attri |       |             | ponse <#sect |
   |              | bute / "all" |       |             | _8.3.4.3>`__ |
   +--------------+--------------+-------+-------------+--------------+
   | ::           | ::           | O     | M           | `Response    |
   |              |              |       |             | Pagin        |
   |    limit     |              |       |             | ation <#sect |
   |              |   = "limit"  |       |             | _8.3.4.4>`__ |
   |              | "=" uint ; M |       |             |              |
   |              | aximum numbe |       |             |              |
   |              | r of results |       |             |              |
   +--------------+--------------+-------+-------------+--------------+
   | ::           | ::           | O     | M           | `Response    |
   |              |              |       |             | Pagin        |
   |    offset    |              |       |             | ation <#sect |
   |              |  = "offset"  |       |             | _8.3.4.4>`__ |
   |              | "=" uint ; N |       |             |              |
   |              | umber of ski |       |             |              |
   |              | pped results |       |             |              |
   +--------------+--------------+-------+-------------+--------------+

The following sections describe these parameters in detail.

.. _sect_8.3.4.1:

Attribute Matching
^^^^^^^^^^^^^^^^^^

The syntax of the match Query Parameter shall be:

::

   match          = normal-match / uid-list-match
   normal-match   = 1*("&" attribute "=" value)
   uid-list-match = 1*("&" attribute "=" 1#value)
   attribute      = (attribute-id) *("." attribute-id)
   attribute-id   = tag *("." tag) / keyword *("." keyword)
   tag            = 8HEXDIG

::

   keyword= ;A keyword from .

One or more DICOM Attribute/Values pairs specify the matching criteria
for the search.

Each search transaction defines which Attributes are required or
permitted.

.. note::

   DICOM Attributes should not be confused with XML attributes. The Tags
   and Keywords for DICOM Attributes are defined in .

DICOM Attribute/Values pairs shall satisfy the following requirements:

1. Each attribute-id shall be a Data Element Tag or Keyword.

2. Each attribute in the Query Parameter shall be not be repeated.

3. Each attribute in the Query Parameter shall have a single value,
   unless the associated DICOM Attribute allows UID List matching (see
   ), in which case the value is a comma-separated list of UIDs.

4. If a tag represents a Private Data Element the query shall also
   include a corresponding Private Creator Element (see ).

5. The acceptable values are determined by the types of matching allowed
   by C-FIND for its associated attribute. See . All characters in
   values that are not qp-chars shall be percent-encoded. All non-ASCII
   characters shall be percent encoded. See
   `biblioentry_title <#biblio_RFC_3986>`__ for details.

The following US-ASCII characters"#", "[", "]", "&", "=", and "," shall
be percent encoded in any Query Parameter.

The match Query Parameter corresponds to DIMSE Matching Keys. See .

.. _sect_8.3.4.1.1:

Matching Rules
''''''''''''''

The matching semantics for each attribute are determined by the types of
matching allowed by C-FIND. See .

Matching results shall be generated according to the Hierarchical Search
Method described in .

Combined date-time matching shall be performed as specified in .

.. note::

   If an origin server is acting as a proxy for a C-FIND SCP that does
   not support combined date-time matching, it shall perform a C-FIND
   request using only the date and filter any results that are outside
   the time range before returning a response.

If the Timezone Offset From UTC (0008,0201) Attribute is specified in
the request, dates and times in the request are to be interpreted in the
specified time zone. See .

.. _sect_8.3.4.2:

Fuzzy Matching of Person Names
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

A single parameter specifies whether Fuzzy Matching of Person Names is
to be performed.

This parameter is optional for the user agent.

This parameter is optional for the origin server.

If this parameter is not present its value is "false".

::

   fuzzymatching = "fuzzymatching" "=" ("true" / "false")

If the value is "false", then the search shall be performed without
Fuzzy Matching.

If the value is "true" and the origin server supports Fuzzy Matching,
then the search shall be performed with Fuzzy Matching of Person Name
Attributes as specified in and shall be documented in the Conformance
Statement and, if the service supports it, the Retrieve Capabilities
response.

If the value is "true" and the origin server does not support Fuzzy
Matching, then:

-  The search shall be performed without Fuzzy Matching.

-  The response shall include the following HTTP Warning header (see
   `biblioentry_title <#biblio_RFC_7234>`__ `Section
   5.5 <http://tools.ietf.org/html/rfc7234#section-5.5>`__) :

   ::

      Warning: 299 <service>: The fuzzymatching parameter is not supported. Only literal matching has been performed.

   where <service> is the base URI for the origin server. This may be a
   combination of scheme, authority, and path.

-  The response may include a payload containing an appropriate Status
   Report.

.. _sect_8.3.4.3:

Attributes Included in the Response
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

A parameter specifies the Attributes that should be included in the
response. The value is either a comma-separated list of attributes, or
the single keyword "all", which means that all available attributes of
the object should be included in the response.

::

   includefield = *("includefield" "=" (1#attribute / "all") )

The request may contain one or more include parameters; however, if a
parameter with the value of "all" is present, then other includefield
parameters shall not be present. If an attribute is a value of an
includefield parameter, it is equivalent to C-FIND Universal matching
for that attribute. See .

If an include parameter represents a Private Data Element a
corresponding Private Creator Element shall be specified as an
additional match parameter (see ).

The includefield Query Parameter corresponds to DIMSE Return Keys. See .

.. _sect_8.3.4.4:

Response Pagination
^^^^^^^^^^^^^^^^^^^

The following two parameters can be used to paginate a search response
that might contain more matches than can readily be handled.

::

   offset = "offset" "=" uint

A single parameter specifies the number of matches the origin server
shall skip before the first returned match. The "offset" parameter value
is an unsigned integer (uint). If this Query Parameter is not present,
its value defaults to 0.

::

   limit = "limit" "=" uint

A single parameter specifies the maximum number of matches the origin
server shall return in a single response. The "limit" parameter value is
an unsigned integer. If this parameter is not present, its value is
determined by the origin server.

.. _sect_8.3.4.4.1:

Paging Behavior
'''''''''''''''

The search requests shall be idempotent, that is, two separate search
requests with the same Target Resource, Query Parameters, and header
fields shall return the same ordered list of matches, if the set of
matches on the origin server has not changed.

Given the following definitions:

+---------------+-----------------------------------------------------+
| ::            | the value of the "offset" query parameter.          |
|               |                                                     |
|    offset     |                                                     |
+---------------+-----------------------------------------------------+
| ::            | the value of the "limit" query parameter.           |
|               |                                                     |
|    limit      |                                                     |
+---------------+-----------------------------------------------------+
| ::            | the maximum number of results the origin server     |
|               | allows in a single response.                        |
|    maxResults |                                                     |
+---------------+-----------------------------------------------------+
| ::            | the number of matches resulting from the search.    |
|               |                                                     |
|    matches    |                                                     |
+---------------+-----------------------------------------------------+
| ::            | the number of results returned in the response. It  |
|               | is equal to the minimum of:                         |
|    results    |                                                     |
|               | -  The maximum of zero and the value of matches -   |
|               |    offset                                           |
|               |                                                     |
|               | -  The value of maxResults                          |
|               |                                                     |
|               | -  The value of limit                               |
+---------------+-----------------------------------------------------+
| ::            | the number of matches that were not yet returned.   |
|               |                                                     |
|    remaining  |                                                     |
+---------------+-----------------------------------------------------+

The results returned in the response are determined as follows:

-  If (results <= 0) then there are no matches, and a 204 (No Content)
   response shall be returned with an empty payload.

-  Otherwise, a 200 (OK) response shall be returned with a payload
   containing the results.

-  If (remaining > 0) the response shall include a Warning header field
   (see `biblioentry_title <#biblio_RFC_7234>`__ `Section
   5.5 <http://tools.ietf.org/html/rfc7234#section-5.5>`__) containing
   the following:

   ::

      Warning: 299 <service>: There are <remaining> additional results that can be requested

The response may include a payload containing an appropriate Status
Report.

If the set of matching results has changed due to changes in the origin
server contents, then the ordered list of results may be different for
subsequent transactions with identical requests, and the results of
using the "offset" and "limit" parameters may be inconsistent.

.. _sect_8.3.5:

Rendering Query Parameters
~~~~~~~~~~~~~~~~~~~~~~~~~~

This section defines the Query Parameter syntax and behavior for
Retrieve requests for Rendered Media Types.

All Retrieve transactions for Rendered Media Types shall support these
parameters.

.. _sect_8.3.5.1:

Query Parameters For Rendered Resources
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

The Query Parameters defined in this section specify various rendering
transformations to be applied to the DICOM images, video, and text
contained in the parent DICOM Resource.

The following rules pertain to all parameters defined in this section:

1. All parameters are optional for the user agent.

2. Not all parameters are required to be supported by the origin server.

3. These parameters only apply to resources that are images and video.

The set of transformations specified by the parameters in this section
shall be applied to the images as if the parameters were a Presentation
State, that is, in the order specified by the applicable image rendering
pipeline specified in .

`table_title <#table_8.3.5-1>`__ shows the Query Parameters that may be
used when requesting a Rendered Representation.

.. table:: Retrieve Rendered Query Parameters

   +---------------+----------------+----------------+----------------+
   | Key           | Values         | Target         | Section        |
   |               |                | Resource       |                |
   |               |                | Category       |                |
   +===============+================+================+================+
   | ::            | ::             | All Categories | `Accept Query  |
   |               |                |                | Parameter <#se |
   |    accept     |    Rende       |                | ct_8.3.3.1>`__ |
   |               | red Media Type |                |                |
   +---------------+----------------+----------------+----------------+
   | ::            | ::             | Image (single  | `Image         |
   |               |                | or             | Ann            |
   |    annotation |                | multi-frame)   | otation <#sect |
   |               | "patient" and/ | or Video       | _8.3.5.1.1>`__ |
   |               | or "technique" |                |                |
   +---------------+----------------+----------------+----------------+
   | ::            | ::             | All Categories | `Character Set |
   |               |                |                | Query          |
   |    charset    |    chara       |                | Parameter <#se |
   |               | cter set token |                | ct_8.3.3.2>`__ |
   +---------------+----------------+----------------+----------------+
   | ::            | ::             | Image (single  | `Image         |
   |               |                | or             | Quality <#sect |
   |    quality    |    Integer     | multi-frame)   | _8.3.5.1.2>`__ |
   |               |                | or Video       |                |
   +---------------+----------------+----------------+----------------+
   | ::            | ::             | No             | `Viewport      |
   |               |                | n-Presentation | Scaling <#sect |
   |    viewport   |                | States         | _8.3.5.1.3>`__ |
   |               |   vw, vh, [ sx |                |                |
   |               | , sy, sw, sh ] |                |                |
   +---------------+----------------+----------------+----------------+
   | ::            | ::             | Presentation   | `Viewport      |
   |               |                | States         | Scaling <#sect |
   |    viewport   |    vw, vh,     |                | _8.3.5.1.3>`__ |
   +---------------+----------------+----------------+----------------+
   | ::            | ::             | No             | `Wi            |
   |               |                | n-Presentation | ndowing <#sect |
   |    window     |    center      | States         | _8.3.5.1.4>`__ |
   |               | , width, shape |                |                |
   +---------------+----------------+----------------+----------------+
   | ::            | ::             | Image (single  | `ICC           |
   |               |                | or             | Profile <#sect |
   |    iccprofile |    "n          | multi-frame)   | _8.3.5.1.5>`__ |
   |               | o", "yes", "sr | or Video       |                |
   |               | gb", "adobergb |                |                |
   |               | " or "rommrgb" |                |                |
   +---------------+----------------+----------------+----------------+

.. _sect_8.3.5.1.1:

Image Annotation
''''''''''''''''

This parameter specifies that the rendered images or video will have
annotations. Its name is "annotation" and its value is a comma-separated
list of one or more keywords. It has the following syntax:

::

   annotation = %s"annotation=" 1#( %s"patient" / %s"technique" )

Where

+----------------+----------------------------------------------------+
| ::             | Indicates that the rendered images shall be        |
|                | annotated with patient information (e.g., patient  |
|    "patient"   | name, birth date, etc.).                           |
+----------------+----------------------------------------------------+
| ::             | Indicates that the rendered images shall be        |
|                | annotated with information about the procedure     |
|    "technique" | that was performed (e.g., image number, study      |
|                | date, image position, etc.).                       |
+----------------+----------------------------------------------------+

When this parameter is not present, no annotations shall be applied.

The image rendering pipelines specified in require that annotations be
applied after all other parameters have been applied and the image or
video has been rendered. The exact nature and presentation of the
annotations is determined by the origin server and is "burned-in" to the
rendered content.

The origin server may support additional keywords, which shall be
documented in the Conformance Statement and, if the service supports it,
the Retrieve Capabilities response.

If any of the parameter values are not keywords, or there are no
parameter values, the origin server shall return a 400 (Bad Request)
response and may include a payload containing an appropriate error
message.

The origin server shall ignore any unsupported parameter values. If
unsupported values are present, the origin server shall include the
following header field:

::

   Warning 299 <service>: The following annotation values are not supported: <values>

and may include a payload containing an appropriate warning message.

.. note::

   1. The exact nature and presentation of the annotation is determined
      by the origin server. The annotation is burned into the rendered
      image pixels.

   2. A user agent wanting more control over annotations may retrieve an
      image, omitting the "annotation" parameter, and separately
      retrieve the metadata, and create customized annotations on the
      image.

   3. A user agent wanting more control over annotations can retrieve an
      image, omitting the "annotation" parameter, separately retrieve
      the metadata, and create customized annotations on the image.

   4. The Target Resource could already contain "burned-in" text that is
      beyond the control of this parameter.

.. _sect_8.3.5.1.2:

Image Quality
'''''''''''''

The "quality" parameter specifies the requested quality of the rendered
images or video. It has the following syntax:

::

   quality = %s"quality=" integer

Where

+------------+--------------------------------------------------------+
| ::         | is an unsigned integer between 1 and 100 inclusive,    |
|            | with 100 being the best quality.                       |
|    integer |                                                        |
+------------+--------------------------------------------------------+

If the value of this parameter is missing or is not an integer between 1
and 100 inclusive, the response shall be a 400 (Bad Request) and may
include a payload containing an appropriate error message.

The "quality" parameter is only supported for media types that allow
lossy compression.

The meaning of this parameter is determined by the origin server and
shall be documented in the Conformance Statement and, if the Service
supports it, Retrieve Capabilities response.

.. note::

   1. Decompression and re-compression may degrade the image quality if
      the original image was already irreversibly compressed. If the
      image has been already lossy compressed using the same format as
      required (e.g., jpeg), it may be sent as it is without
      decompressing and re-compressing it.

   2. The origin server could choose to disregard the quality parameter
      if the resultant image quality would be too low.

.. _sect_8.3.5.1.3:

Viewport Scaling
''''''''''''''''

The "viewport" parameter specifies a rectangular region of the source
image(s) or video to be cropped, and a rectangular region corresponding
to the size of the user agent's viewport to which the cropped image or
video should be scaled.

The syntax of this parameter for a Presentation State Instance or a
Thumbnail is:

::

   %s"viewport=" vw "," vh

Otherwise it is:

::

   %s"viewport=" vw "," vh ["," [sx] "," [sy] "," [sw] "," [sh] ]

Where

+--------------+------------------------------------------------------+
| ::           | are positive integers specifying the width and       |
|              | height, in pixels, of the rendered image or video.   |
|    vw and vh | Both values are required.                            |
+--------------+------------------------------------------------------+
| ::           | are decimal numbers whose absolute values specify,   |
|              | in pixels, the top-left corner of the region of the  |
|    sx and sy | source image(s) to be rendered. If either sx or sy   |
|              | is not specified, it defaults to 0. A value of 0,0   |
|              | specifies the top-left corner of the source          |
|              | image(s).                                            |
+--------------+------------------------------------------------------+
| ::           | are decimal numbers whose absolute values specify,   |
|              | in pixels, the width and height of the region of the |
|    sw and sh | source image(s) to be rendered. If sw is not         |
|              | specified, it defaults to the right edge of the      |
|              | source image. If sh is not specified, it defaults to |
|              | the bottom edge of the source image. If sw is a      |
|              | negative value, the image is flipped horizontally.   |
|              | If sh is a negative value, the image is flipped      |
|              | vertically.                                          |
+--------------+------------------------------------------------------+

The origin server shall crop the source images or video to the region
specified by sx, sy, sw, and sh. It shall then scale the source content,
maintaining the aspect ratio of the cropped region, until either the
rendered content width or height is the same as the viewport width or
height, whichever avoids truncation. In other words, viewport scaling
makes the image(s) as large as possible, within the viewport, without
overflowing the viewport area and without distorting the image.

If any of the optional parameter values are not present, the default
value shall be used. Individual values may be elided, but the commas
between the values shall be present. For example:

::

   viewport=512,512,,,512,512

The missing sx and sy parameter values default to 0.

If trailing values are elided, then the trailing commas shall be
omitted. For example:

::

   viewport=1024,1024

The missing sx, sy, sw, sh will have their default values, i.e., the
image(s) shall not be cropped, i.e., the full image is rendered.

If the viewport parameter is not present, the rendered image(s) or video
shall not be scaled, i.e., the rendered image(s) shall contain the same
sized pixel matrix as the source DICOM image.

If any of the following are true:

-  This parameter specifies viewport dimensions that are either
   ill-formed or not supported

-  The Target Resource is a Presentation State or Thumbnail and anything
   other than vw and vh are specified

then the response shall be 400 (Bad Request) and may include a payload
containing an appropriate Status Report.

.. note::

   The default values for sx and sy differ from the defaults in the
   Specified Displayed Area in Presentation States, which uses integer
   values with the top left corner being (1\1). See .

.. _sect_8.3.5.1.4:

Windowing
'''''''''

The "window" parameter controls the windowing of the images or video as
defined in . It has the following syntax:

::

   %s"window=" center "," width "," function

Where

+-------------+-------------------------------------------------------+
| ::          | is a decimal number containing the window-center      |
|             | value                                                 |
|    center   |                                                       |
+-------------+-------------------------------------------------------+
| ::          | is a decimal numbercontaining the window-width value  |
|             |                                                       |
|    width    |                                                       |
+-------------+-------------------------------------------------------+
| ::          | is one of the following keywords: "linear",           |
|             | "linear-exact", or "sigmoid".                         |
|    function |                                                       |
+-------------+-------------------------------------------------------+

.. note::

   These correspond to the differently capitalized and punctuated values
   of VOI LUT Function (0028,1056). See .

All three parameters shall be present with valid values.

If any of the parameter values are missing or ill-formed, the origin
server shall return a 400 (Bad Request) response and may include a
payload containing an appropriate error message.

If the Target Resource is a Presentation State, this parameter shall not
be used. If this parameter is present when the Target Resource is a
Presentation state, the origin server shall return a 400 (Bad Request).

.. _sect_8.3.5.1.5:

ICC Profile
'''''''''''

The "iccprofile" parameter specifies the color characteristics of, and
inclusion of an ICC Profile in, the rendered images. It has the
following syntax:

::

   %s"iccprofile=" 1#( %s"no" / %s"yes" / %s"srgb" / %s"adobergb" / %s"rommrgb" )

Where

+------------+--------------------------------------------------------+
| "no"       | indicates that no ICC profile shall be present in the  |
|            | rendered image in the response.                        |
+------------+--------------------------------------------------------+
| "yes"      | indicates that an ICC profile shall be present in the  |
|            | rendered image in the response, describing its color   |
|            | characteristics, if the Media Type supports embedded   |
|            | ICC Profiles.                                          |
+------------+--------------------------------------------------------+
| "srgb"     | indicates that an sRGB ICC profile shall be present in |
|            | the image, if the Media Type supports embedded ICC     |
|            | Profiles, and that the pixels of the rendered image in |
|            | the response shall be transformed from their original  |
|            | color space and be encoded in the sRGB color space     |
|            | [IEC 61966-2.1].                                       |
+------------+--------------------------------------------------------+
| "adobergb" | indicates that an Adobe RGB ICC profile shall be       |
|            | present in the image, if the Media Type supports       |
|            | embedded ICC Profiles, and that the pixels of the      |
|            | rendered image in the response shall be transformed    |
|            | from their original color space and be encoded in the  |
|            | Adobe RGB color space [Adobe RGB].                     |
+------------+--------------------------------------------------------+
| "rommrgb"  | indicates that a ROMM RGB ICC profile shall be present |
|            | in the image, if the Media Type supports embedded ICC  |
|            | Profiles, and that the pixels of the rendered image in |
|            | the response shall be transformed from their original  |
|            | color space and encoded in the ROMM RGB color space    |
|            | [ISO 22028-2].                                         |
+------------+--------------------------------------------------------+

When this parameter is not present:

-  an ICC profile may or may not be present in the image in the
   response;

-  the color characteristics of the image in the response may or may not
   be consistent with any DICOM ICC Profile (0028,2000) Attribute in the
   metadata.

The ICC Profile in the image in the response shall be:

-  the ICC profile of the color space specified explicitly by the
   parameter,

-  otherwise, the ICC profile encoded in the source DICOM ICC Profile
   (0028,2000) Attribute, if any, appropriate to the selected frame,

-  otherwise, the ICC profile, if any, embedded in the stored compressed
   representation of the selected frame,

-  otherwise, at the discretion of the origin server, the ICC profile of
   a well-known color space listed in that is appropriate to the type
   and source of the image.

If the Media Type does not support embedded ICC Profiles:

-  a 400 Bad Request error shall be returned if the parameter value is
   other than "no"

.. note::

   1. This parameter allows ICC profile information to be present in the
      image in the response so that the user agent can make use of it
      for local color management (e.g., an ICC profile capable browser
      can apply the profile when displaying the rendered image in the
      response).

   2. This parameter provides a limited mechanism for requesting that
      the origin server perform some color management. It provides the
      names of well-known color spaces for the rendered image in the
      response. It does not provide a mechanism to supply an arbitrary
      ICC profile, such as the calibration profile of a display, so it
      does not absolve the user agent from the need to handle its own
      color calibration and color management.

   3. ICC profiles can theoretically be large relative to the compressed
      pixel data of a single frame, so the user agent may specify a
      parameter value of "no", retrieve the DICOM ICC Profile
      (0028,2000) Attribute value(s) that apply to multiple frames from
      the metadata, and combine these itself.

   4. ICC profiles are embedded in rendered images of Media Type
      image/jpeg as one or more chunks in APP2 marker segments with an
      identifier of "ICC_PROFILE", as defined in Annex B of
      `biblioentry_title <#biblio_ISOIEC15076-1>`__.

   5. ICC profiles are embedded in rendered images of Media Type
      image/jp2 either as JP2 Restricted or JPX Full profiles according
      to `biblioentry_title <#biblio_ISOIEC15444-1>`__ and
      `biblioentry_title <#biblio_ISOIEC15444-2>`__, respectively;
      rendered images in the response are not subject to the prohibition
      against inclusion of a JP2 box in JPEG 2000 compressed data
      streams in DICOM images.

   6. ICC profiles are embedded in rendered images of Media Type
      image/png in an iCCP chunk, as defined in
      `biblioentry_title <#biblio_ISO15948>`__.

.. _sect_8.3.5.2:

Query Parameters For Thumbnails
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

`table_title <#table_8.3.5-2>`__\ shows the Query Parameters that may be
used when requesting a Thumbnail representation.

.. table:: Thumbnail Query Parameters

   +-------------+-----------------+-----------------+-----------------+
   | Key         | Values          | Target Resource | Section         |
   |             |                 | Category        |                 |
   +=============+=================+=================+=================+
   | ::          | ::              | All Categories  | `Accept Query   |
   |             |                 |                 | Parameter <#s   |
   |    accept   |    Rend         |                 | ect_8.3.3.1>`__ |
   |             | ered Media Type |                 |                 |
   +-------------+-----------------+-----------------+-----------------+
   | ::          | ::              | All Categories  | `Character Set  |
   |             |                 |                 | Query           |
   |    charset  |    char         |                 | Parameter <#s   |
   |             | acter set token |                 | ect_8.3.3.2>`__ |
   +-------------+-----------------+-----------------+-----------------+
   | ::          | ::              | All Categories  | `Viewport       |
   |             |                 |                 | Scaling <#sec   |
   |    viewport |    vw, vh       |                 | t_8.3.5.1.3>`__ |
   +-------------+-----------------+-----------------+-----------------+

The Viewport parameter only has width and height values. If no viewport
parameter is provided the origin server will determine the size of the
thumbnail.

.. _sect_8.4:

Header Fields
-------------

The following sections specify important header fields, some of which
have stronger requirements than those specified in the HTTP Standard.

.. _sect_8.4.1:

Content Negotiation Header Fields
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

HTTP uses the Accept and Content-Type header fields for content
negotiation and data typing. The media types in the Accept header field
of a request define the media types that the user agent would find
acceptable in the response. The media type in the Content-Type header
field of a message, or payload part, describes the format of the
representation contained in the message payload or payload part.

Content Negotiation header fields in requests allow the user agent to
specify acceptable representations for the response.
`table_title <#table_8.4.1-1>`__ lists the content negotiation header
fields. The values in these fields apply to any content in the response,
including representations of the Target Resource, representations of
error or processing status, and potentially even the miscellaneous text
strings that might appear within the HTTP protocol. See
`biblioentry_title <#biblio_RFC_7231>`__ `Section
5.3 <http://tools.ietf.org/html/rfc7231#section-5.3>`__.

.. table:: Content Negotiation Header Fields

   +-----------------+---------------+-------+---------------------+
   | Name            | Value         | Usage | Description         |
   +=================+===============+=======+=====================+
   | Accept          | 1#media-range | M     | All requests that   |
   |                 |               |       | expect to receive a |
   |                 |               |       | response with a     |
   |                 |               |       | payload shall       |
   |                 |               |       | contain an Accept   |
   |                 |               |       | header field. See   |
   |                 |               |       | `Accept             |
   |                 |               |       | <#sect_8.4.1.1>`__. |
   +-----------------+---------------+-------+---------------------+
   | Accept-Charset  | 1#charset     | O     | The Accept-Charset  |
   |                 |               |       | header field may be |
   |                 |               |       | sent by a user      |
   |                 |               |       | agent to indicate   |
   |                 |               |       | what charsets are   |
   |                 |               |       | acceptable in       |
   |                 |               |       | response content.   |
   |                 |               |       | See                 |
   |                 |               |       | `b                  |
   |                 |               |       | iblioentry_title <# |
   |                 |               |       | biblio_RFC_7231>`__ |
   |                 |               |       | `Section            |
   |                 |               |       | 5.3                 |
   |                 |               |       | .3 <http://tools.ie |
   |                 |               |       | tf.org/html/rfc7231 |
   |                 |               |       | #section-5.3.3>`__. |
   +-----------------+---------------+-------+---------------------+
   | Accept-Encoding | 1#encoding    | O     | The Accept-Encoding |
   |                 |               |       | header field may be |
   |                 |               |       | used to indicate    |
   |                 |               |       | the content-codings |
   |                 |               |       | (see                |
   |                 |               |       | `b                  |
   |                 |               |       | iblioentry_title <# |
   |                 |               |       | biblio_RFC_7231>`__ |
   |                 |               |       | `Section            |
   |                 |               |       | 3.1.2.1             |
   |                 |               |       |  <http://tools.ietf |
   |                 |               |       | .org/html/rfc7231#s |
   |                 |               |       | ection-3.1.2.1>`__) |
   |                 |               |       | acceptable in the   |
   |                 |               |       | response. See       |
   |                 |               |       | `b                  |
   |                 |               |       | iblioentry_title <# |
   |                 |               |       | biblio_RFC_7231>`__ |
   |                 |               |       | `Section            |
   |                 |               |       | 5.3                 |
   |                 |               |       | .4 <http://tools.ie |
   |                 |               |       | tf.org/html/rfc7231 |
   |                 |               |       | #section-5.3.4>`__. |
   +-----------------+---------------+-------+---------------------+
   | Accept-Language | 1#language    | O     | The Accept-Language |
   |                 |               |       | header field may be |
   |                 |               |       | used by user agents |
   |                 |               |       | to indicate the set |
   |                 |               |       | of natural          |
   |                 |               |       | languages that are  |
   |                 |               |       | preferred in the    |
   |                 |               |       | response. See       |
   |                 |               |       | `b                  |
   |                 |               |       | iblioentry_title <# |
   |                 |               |       | biblio_RFC_7231>`__ |
   |                 |               |       | `Section            |
   |                 |               |       | 5.3                 |
   |                 |               |       | .5 <http://tools.ie |
   |                 |               |       | tf.org/html/rfc7231 |
   |                 |               |       | #section-5.3.5>`__. |
   +-----------------+---------------+-------+---------------------+

.. _sect_8.4.1.1:

Accept
^^^^^^

User agents use the Accept header field to specify Acceptable Media
Types for the response payload. The Accept header field can be used to
indicate that the response payload is specifically limited to a set of
desired media types. It has the following syntax:

::

   Accept      = "Accept:" #( media-range [accept-params] )
   media-range = ("*/*" 
                 / (type "/" "*") 
                 / (type "/" subtype)
                 ) *(OWS ";" OWS accept-params)
   accept-params = weight *(accept-ext)

Most requests have an Accept header field that contains a
comma-separated list of one or more media ranges. A media-range extends
media-type with wildcards (*/\* or type/*) and parameters that are not
defined for media-types. See `biblioentry_title <#biblio_RFC_7231>`__
`Section 5.3.2 <http://tools.ietf.org/html/rfc7231#section-5.3.2>`__ for
details.

For example, if the user agent is willing to accept any media type in
the response it should include \*/\* as a value of the Accept header
field.

Many of the content negotiation header fields use a weight parameter,
named "q" (case-insensitive), to assign a relative "weight" to the
preference for that associated kind of content.

The media types in the Accept header can be given a priority ordering by
using weights.

::

   weight = OWS ";" OWS "q=" qvalue
   qvalue = ("0" ["." 0*3DIGIT]) 
          / ("1" ["." 0*3("0")])

This weight is often referred to as "quality value" or "qvalue". See
`biblioentry_title <#biblio_RFC_7231>`__ `Section
5.3.1 <http://tools.ietf.org/html/rfc7231#section-5.3.1>`__.

All requests that might have a response containing a payload shall
provide an Accept header field.

See `Acceptable Media Types <#sect_8.7.5>`__ for Acceptable Media Types.

.. _sect_8.4.1.1.1:

Charset Media Type Parameter
''''''''''''''''''''''''''''

Many media types, especially text/\* types, define a "charset" parameter
that specifies the character set for the representation. See
`biblioentry_title <#biblio_RFC_7231>`__ `Section
3.1.1.2 <http://tools.ietf.org/html/rfc7231#section-3.1.1.2>`__.

DICOM Media Types define a "charset" parameter. See `Character Set
Parameter <#sect_8.7.3.5.3>`__.

For example,

::

   application/dicom; charset=ISO-8859-1

See `Acceptable Character Sets <#sect_8.8.1>`__ for Acceptable Character
Sets.

.. _sect_8.4.2:

Content Representation Header Fields
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

The media type in the Content-Type header field of a message, or payload
part, describes the format of the representation contained in the
payload or part.

When a message has a payload, the Content Representation Header Fields
provide metadata describing how to interpret the representation(s)
contained in the payload. `table_title <#table_8.4.2-1>`__ describes the
Content Representation Header Fields, and the usage requirements
(Mandatory, Conditional, or Optional) for when they shall be present.

.. table:: Content Representation Header Fields

   +------------------+------------+-------+----------------------+
   | Name             | Value      | Usage | Requirement          |
   +==================+============+=======+======================+
   | Content-Type     | media-type | C     | Specifies the media  |
   |                  |            |       | type of the          |
   |                  |            |       | representation       |
   |                  |            |       | contained in the     |
   |                  |            |       | payload.             |
   |                  |            |       |                      |
   |                  |            |       | If a message has a   |
   |                  |            |       | payload, it shall    |
   |                  |            |       | have a Content-Type  |
   |                  |            |       | header field         |
   |                  |            |       | specifying the media |
   |                  |            |       | type of the payload. |
   |                  |            |       | See                  |
   |                  |            |       | `biblioentry_title < |
   |                  |            |       | #biblio_RFC_7231>`__ |
   |                  |            |       | `Section             |
   |                  |            |       | 3.1.                 |
   |                  |            |       | 1.5 <http://tools.ie |
   |                  |            |       | tf.org/html/rfc7231# |
   |                  |            |       | section-3.1.1.5>`__. |
   +------------------+------------+-------+----------------------+
   | Content-Encoding | encoding   | C     | Specifies any        |
   |                  |            |       | content encodings    |
   |                  |            |       | applied to the       |
   |                  |            |       | representation       |
   |                  |            |       | (beyond those        |
   |                  |            |       | inherent in the      |
   |                  |            |       | media type), and     |
   |                  |            |       | thus what decoding   |
   |                  |            |       | to apply to obtain a |
   |                  |            |       | representation in    |
   |                  |            |       | the media type       |
   |                  |            |       | specified by the     |
   |                  |            |       | Content-Type. See    |
   |                  |            |       | `biblioentry_title < |
   |                  |            |       | #biblio_RFC_7230>`__ |
   |                  |            |       | `Section             |
   |                  |            |       | 3.1.                 |
   |                  |            |       | 2.2 <http://tools.ie |
   |                  |            |       | tf.org/html/rfc7230# |
   |                  |            |       | section-3.1.2.2>`__. |
   |                  |            |       |                      |
   |                  |            |       | Content-Encoding     |
   |                  |            |       | allows compression,  |
   |                  |            |       | encryption, and/or   |
   |                  |            |       | authentication of    |
   |                  |            |       | representations.     |
   |                  |            |       |                      |
   |                  |            |       | Shall be present if  |
   |                  |            |       | a content encoding   |
   |                  |            |       | has been applied to  |
   |                  |            |       | the representation   |
   |                  |            |       | in the payload.      |
   +------------------+------------+-------+----------------------+
   | Content-Language | language   | O     | Specifies the        |
   |                  |            |       | natural language(s)  |
   |                  |            |       | of the intended      |
   |                  |            |       | audience used in     |
   |                  |            |       | representation. See  |
   |                  |            |       | [RFC7231] Section    |
   |                  |            |       | 3.1.3.2.             |
   +------------------+------------+-------+----------------------+
   | Content-Location | url        | C     | Contains a URL that  |
   |                  |            |       | references the       |
   |                  |            |       | specific resource    |
   |                  |            |       | corresponding to the |
   |                  |            |       | representation in    |
   |                  |            |       | the payload.         |
   |                  |            |       |                      |
   |                  |            |       | Shall be present if  |
   |                  |            |       | the payload contains |
   |                  |            |       | a representation of  |
   |                  |            |       | a resource.          |
   +------------------+------------+-------+----------------------+

.. _sect_8.4.3:

Payload Header Fields
~~~~~~~~~~~~~~~~~~~~~

The Payload Header Fields contain metadata describing the payload, not
the representation it contains. `table_title <#table_8.4.3-1>`__
describes the payload header fields, and the usage requirements
(Mandatory, Conditional, or Optional) for when they shall be present.

.. table:: Payload Header Fields

   +-------------------+----------+-------+-----------------------+
   | Name              | Value    | Usage | Description           |
   +===================+==========+=======+=======================+
   | Content-Length    | uint     | C     | Specifies the decimal |
   |                   |          |       | number of octets in   |
   |                   |          |       | the payload.          |
   |                   |          |       |                       |
   |                   |          |       | If the response       |
   |                   |          |       | message has a payload |
   |                   |          |       | and does not have a   |
   |                   |          |       | Content-Encoding      |
   |                   |          |       | header field, it      |
   |                   |          |       | shall have a          |
   |                   |          |       | Content-Length header |
   |                   |          |       | field specifying the  |
   |                   |          |       | length in octets      |
   |                   |          |       | (bytes) of the        |
   |                   |          |       | payload.              |
   |                   |          |       |                       |
   |                   |          |       | Shall not be present  |
   |                   |          |       | if the message has a  |
   |                   |          |       | Content-Encoding      |
   |                   |          |       | header field. Shall   |
   |                   |          |       | be present otherwise, |
   |                   |          |       | even is the size of   |
   |                   |          |       | the payload is zero.  |
   +-------------------+----------+-------+-----------------------+
   | Content-Range     | range    | C     | Specifies the range   |
   |                   |          |       | of a partial          |
   |                   |          |       | representation        |
   |                   |          |       | contained in a        |
   |                   |          |       | payload. See          |
   |                   |          |       | `biblioentry_title    |
   |                   |          |       | <#biblio_RFC_7233>`__ |
   |                   |          |       | `Section              |
   |                   |          |       | 4.2 <http://to        |
   |                   |          |       | ols.ietf.org/html/rfc |
   |                   |          |       | 7233#section-4.2>`__. |
   |                   |          |       |                       |
   |                   |          |       | The Content-Range     |
   |                   |          |       | header field is sent  |
   |                   |          |       | in a single part 206  |
   |                   |          |       | (Partial Content)     |
   |                   |          |       | response to indicate  |
   |                   |          |       | the partial range of  |
   |                   |          |       | the selected          |
   |                   |          |       | representation        |
   |                   |          |       | enclosed as the       |
   |                   |          |       | message payload.      |
   |                   |          |       |                       |
   |                   |          |       | It is sent in each    |
   |                   |          |       | part of a multipart   |
   |                   |          |       | 206 response to       |
   |                   |          |       | indicate the range    |
   |                   |          |       | enclosed within each  |
   |                   |          |       | body part.            |
   |                   |          |       |                       |
   |                   |          |       | It is sent in 416     |
   |                   |          |       | (Range Not            |
   |                   |          |       | Satisfiable)          |
   |                   |          |       | responses to provide  |
   |                   |          |       | information about the |
   |                   |          |       | selected              |
   |                   |          |       | representation.       |
   +-------------------+----------+-------+-----------------------+
   | Transfer-Encoding | encoding | C     | See                   |
   |                   |          |       | `biblioentry_title    |
   |                   |          |       | <#biblio_RFC_7230>`__ |
   |                   |          |       | `Section              |
   |                   |          |       | 3.3.1 <http://tool    |
   |                   |          |       | s.ietf.org/html/rfc72 |
   |                   |          |       | 30#section-3.3.1>`__. |
   |                   |          |       |                       |
   |                   |          |       | Shall be present if   |
   |                   |          |       | transfer-encodings    |
   |                   |          |       | have been applied to  |
   |                   |          |       | the payload.          |
   +-------------------+----------+-------+-----------------------+

.. _sect_8.5:

Status Codes
------------

Each response message contains a status-code.

The most common HTTP status codes used are listed in
`table_title <#table_8.5-1>`__ Most of these codes are described in
detail in `biblioentry_title <#biblio_RFC_7231>`__. IANA maintains the
HTTP Status Code Registry
`biblioentry_title <#biblio_IANA_HTTPStatusCodeRegistry>`__, which
contains a complete list of registered status codes.

.. table:: Status Code Meaning

   +---------------------------------+-----------------------------------+
   | Status                          | Code                              |
   +=================================+===================================+
   | Success                         | The 2xx (Successful) class of     |
   |                                 | status code indicates that the    |
   |                                 | client's request was successfully |
   |                                 | received, understood, and         |
   |                                 | accepted.                         |
   +---------------------------------+-----------------------------------+
   | 200                             | All Target Resource               |
   |                                 | representations are contained in  |
   | (Success)                       | the payload. See                  |
   |                                 | `biblio                           |
   |                                 | entry_title <#biblio_RFC_7231>`__ |
   |                                 | `Section                          |
   |                                 | 6.3.1 <http://tools.ietf.or       |
   |                                 | g/html/rfc7231#section-6.3.1>`__. |
   +---------------------------------+-----------------------------------+
   | 201                             | The request has been fulfilled    |
   |                                 | and has resulted in one or more   |
   | (Created)                       | new resources being created. See  |
   |                                 | `biblio                           |
   |                                 | entry_title <#biblio_RFC_7231>`__ |
   |                                 | `Section                          |
   |                                 | 6.3.2 <http://tools.ietf.or       |
   |                                 | g/html/rfc7231#section-6.3.2>`__. |
   +---------------------------------+-----------------------------------+
   | 202                             | The request has been accepted for |
   |                                 | processing, but the processing    |
   | (Accepted)                      | has not been completed. The       |
   |                                 | payload of this response should   |
   |                                 | contain a Status Report.          |
   |                                 | `biblio                           |
   |                                 | entry_title <#biblio_RFC_7231>`__ |
   |                                 | `Section                          |
   |                                 | 6.3.3 <http://tools.ietf.or       |
   |                                 | g/html/rfc7231#section-6.3.3>`__. |
   |                                 |                                   |
   |                                 | The user agent may be able to     |
   |                                 | inspect relevant resources to     |
   |                                 | determine the status at some      |
   |                                 | later time.                       |
   +---------------------------------+-----------------------------------+
   | 203                             | The request was successful, but   |
   |                                 | the enclosed payload has been     |
   | (Non-Authoritative Information) | modified from that of the origin  |
   |                                 | server's 200 (OK) response by a   |
   |                                 | transforming proxy. See           |
   |                                 | `biblio                           |
   |                                 | entry_title <#biblio_RFC_7230>`__ |
   |                                 | `Section                          |
   |                                 | 5.7.2 <http://tools.ietf.o        |
   |                                 | rg/html/rfc7230#section-5.7.2>`__ |
   |                                 | and                               |
   |                                 | `biblio                           |
   |                                 | entry_title <#biblio_RFC_7230>`__ |
   |                                 | `biblio                           |
   |                                 | entry_title <#biblio_RFC_7231>`__ |
   |                                 | `Section                          |
   |                                 | 6.3.4 <http://tools.ietf.or       |
   |                                 | g/html/rfc7231#section-6.3.4>`__. |
   +---------------------------------+-----------------------------------+
   | 204                             | The server has successfully       |
   |                                 | fulfilled the request and there   |
   | (No-Content)                    | is no additional content to send  |
   |                                 | in the response payload body.     |
   |                                 | This should be the response when  |
   |                                 | content is successfully uploaded, |
   |                                 | and the response has no payload.  |
   |                                 |                                   |
   |                                 | For example, this status code is  |
   |                                 | used in the response to a         |
   |                                 | Conditional Retrieve request),    |
   |                                 | when the Target Resource has not  |
   |                                 | been modified. See                |
   |                                 | `biblio                           |
   |                                 | entry_title <#biblio_RFC_7231>`__ |
   |                                 | `Section                          |
   |                                 | 6.3.5 <http://tools.ietf.or       |
   |                                 | g/html/rfc7231#section-6.3.5>`__. |
   +---------------------------------+-----------------------------------+
   | 205                             | The server has fulfilled the      |
   |                                 | request and desires that the user |
   | (Reset Content)                 | agent reset the "document view",  |
   |                                 | which caused the request to be    |
   |                                 | sent, to its original state as    |
   |                                 | received from the origin server.  |
   +---------------------------------+-----------------------------------+
   | 206                             | The 206 (Partial Content) status  |
   |                                 | code indicates that the server is |
   | (Partial Content)               | successfully fulfilling a range   |
   |                                 | request for the Target Resource   |
   |                                 | by transferring one or more parts |
   |                                 | of the selected representation    |
   |                                 | that correspond to the            |
   |                                 | satisfiable ranges found in the   |
   |                                 | request's Range header field.     |
   |                                 |                                   |
   |                                 | This status code shall only be    |
   |                                 | used with Range Requests. See     |
   |                                 | `biblioe                          |
   |                                 | ntry_title <#biblio_RFC_7233>`__. |
   |                                 |                                   |
   |                                 | .. note::                         |
   |                                 |                                   |
   |                                 |    This status code was           |
   |                                 |    previously (erroneously) used  |
   |                                 |    to indicate that only some of  |
   |                                 |    a payload was stored.          |
   +---------------------------------+-----------------------------------+
   | Redirection                     | The 3xx (Redirection) class of    |
   |                                 | status code indicates that        |
   |                                 | further action needs to be taken  |
   |                                 | by the user agent to fulfill the  |
   |                                 | request.                          |
   +---------------------------------+-----------------------------------+
   | 301                             | The origin server has assigned    |
   |                                 | the Target Resource to a new      |
   | (Moved Permanently)             | permanent URI, indicated in a     |
   |                                 | Location header field.            |
   |                                 |                                   |
   |                                 | This status is typically needed   |
   |                                 | when the resource has been moved  |
   |                                 | from one service to another, for  |
   |                                 | example during a migration.       |
   +---------------------------------+-----------------------------------+
   | 303                             | The origin the server is          |
   |                                 | redirecting the user agent to a   |
   | (See Other)                     | different resource, as indicated  |
   |                                 | by a URI in the Location header   |
   |                                 | field, which will provide a       |
   |                                 | response to the original request. |
   +---------------------------------+-----------------------------------+
   | 304                             | The origin server has received a  |
   |                                 | conditional GET or HEAD request   |
   | (Not Modified)                  | that would have resulted in a 200 |
   |                                 | (OK) response if it were not for  |
   |                                 | the fact that the condition       |
   |                                 | evaluated to false.               |
   +---------------------------------+-----------------------------------+
   | Client Error                    | The 4xx (Client Error) class of   |
   |                                 | status code indicates that the    |
   |                                 | user agent has erred.             |
   |                                 |                                   |
   |                                 | For all these error codes,the     |
   |                                 | origin server should return a     |
   |                                 | payload containing an explanation |
   |                                 | of the error situation, and       |
   |                                 | whether it is a temporary or      |
   |                                 | permanent condition, except when  |
   |                                 | responding to a HEAD request.     |
   +---------------------------------+-----------------------------------+
   | 400                             | The server cannot or will not     |
   |                                 | process the request due to        |
   | (Bad Request)                   | something that is perceived to be |
   |                                 | a client error (e.g., malformed   |
   |                                 | request syntax, invalid request   |
   |                                 | â€¦).                             |
   +---------------------------------+-----------------------------------+
   | 401                             | The request has not been          |
   |                                 | fulfilled because it lacks valid  |
   | (Unauthorized)                  | authentication credentials for    |
   |                                 | the service or Target Resource.   |
   |                                 | The server generating a 401       |
   |                                 | response shall send a             |
   |                                 | WWW-Authenticate header field     |
   |                                 | (`biblio                          |
   |                                 | entry_title <#biblio_RFC_7235>`__ |
   |                                 | `Section                          |
   |                                 | 4.1 <http://tools.ietf.           |
   |                                 | org/html/rfc7230#section-4.1>`__) |
   |                                 | containing at least one challenge |
   |                                 | applicable to the server or       |
   |                                 | Target Resource.                  |
   +---------------------------------+-----------------------------------+
   | 403                             | The origin server understood the  |
   |                                 | request, but refused to authorize |
   | (Forbidden)                     | it (e.g., an authorized user with |
   |                                 | insufficient privileges). If      |
   |                                 | authentication credentials were   |
   |                                 | provided in the request, the      |
   |                                 | server considers them             |
   |                                 | insufficient to grant access. The |
   |                                 | origin server may respond with a  |
   |                                 | 404 (Not Found) if not permitted  |
   |                                 | to use this status code.          |
   +---------------------------------+-----------------------------------+
   | 404                             | The origin server did not find a  |
   |                                 | representation for the Target     |
   | (Not Found)                     | Resource or is not willing to     |
   |                                 | disclose that one exists. This    |
   |                                 | might be a temporary condition.   |
   |                                 | If the origin server knows that   |
   |                                 | the resource has been deleted,    |
   |                                 | the 410 (Gone) status code shall  |
   |                                 | be returned rather than 404.      |
   +---------------------------------+-----------------------------------+
   | 405                             | The method in the request is      |
   |                                 | known by the origin server but    |
   | (Method Not Allowed)            | not supported by the target       |
   |                                 | service or resource. The origin   |
   |                                 | server shall include an Allow     |
   |                                 | header field in a 405 response    |
   |                                 | containing a list of the target   |
   |                                 | service or resource's currently   |
   |                                 | supported methods.                |
   +---------------------------------+-----------------------------------+
   | 406                             | The Target Resource does not have |
   |                                 | a representation that would be    |
   | (Not Acceptable)                | acceptable to the user agent, per |
   |                                 | the content negotiation header    |
   |                                 | fields in the request, and the    |
   |                                 | server is unwilling to supply a   |
   |                                 | default representation.           |
   |                                 |                                   |
   |                                 | The origin server should return a |
   |                                 | payload that lists the available  |
   |                                 | media types and corresponding     |
   |                                 | resource identifiers.             |
   +---------------------------------+-----------------------------------+
   | 409                             | The request could not be          |
   |                                 | completed due to a conflict with  |
   | (Conflict)                      | the current state of the Target   |
   |                                 | Resource. This code is used in    |
   |                                 | situations where the user agent   |
   |                                 | might be able to resolve the      |
   |                                 | conflict and resubmit the         |
   |                                 | request. The origin server should |
   |                                 | return a payload containing       |
   |                                 | enough information for the user   |
   |                                 | agent to recognize the source of  |
   |                                 | the conflict.                     |
   |                                 |                                   |
   |                                 | In the DICOM context, this code   |
   |                                 | might indicate that the origin    |
   |                                 | server was unable to store any    |
   |                                 | Instances due to a conflict in    |
   |                                 | the request (e.g., unsupported    |
   |                                 | SOP Class or Instance mismatch).  |
   +---------------------------------+-----------------------------------+
   | 410                             | Access to the Target Resource is  |
   |                                 | no longer available at the origin |
   | (Gone)                          | server and this condition is      |
   |                                 | likely to be permanent. If the    |
   |                                 | origin server does not know, or   |
   |                                 | has no facility to determine,     |
   |                                 | whether the condition is          |
   |                                 | permanent, the 404 (Not Found)    |
   |                                 | status code should be used        |
   |                                 | instead.                          |
   +---------------------------------+-----------------------------------+
   | 411                             | The origin server refuses to      |
   |                                 | accept the request because the    |
   | (Length Required)               | Content-Length header field was   |
   |                                 | not specified.                    |
   +---------------------------------+-----------------------------------+
   | 413                             | The server is refusing to process |
   |                                 | the request because the request   |
   | (Payload Too Large)             | payload is larger than the server |
   |                                 | is willing or able to process.    |
   +---------------------------------+-----------------------------------+
   | 414                             | The server is refusing to service |
   |                                 | the request because the           |
   | (URI Too Long)                  | request-target                    |
   |                                 | (`biblio                          |
   |                                 | entry_title <#biblio_RFC_7230>`__ |
   |                                 | `Section                          |
   |                                 | 5.3 <http://tools.ietf.           |
   |                                 | org/html/rfc7230#section-5.3>`__) |
   |                                 | is longer than the server is      |
   |                                 | willing to interpret.             |
   +---------------------------------+-----------------------------------+
   | 415                             | The origin server does not        |
   |                                 | support the Content-Type in the   |
   | (Unsupported Media Type)        | request payload. This error       |
   |                                 | typically occurs when the user    |
   |                                 | agent is trying to create or      |
   |                                 | update a resource.                |
   |                                 |                                   |
   |                                 | The origin server should return a |
   |                                 | payload that lists the available  |
   |                                 | media types and corresponding     |
   |                                 | resource identifiers.             |
   |                                 |                                   |
   |                                 | .. note::                         |
   |                                 |                                   |
   |                                 |    This is different from 406     |
   |                                 |    (Not Acceptable).              |
   +---------------------------------+-----------------------------------+
   | Server Error                    | The 5xx (Server Error) class of   |
   |                                 | status code indicates that the    |
   |                                 | server is aware that it has erred |
   |                                 | or is incapable of performing the |
   |                                 | requested method.                 |
   |                                 |                                   |
   |                                 | For all these error codes, the    |
   |                                 | server should send an explanation |
   |                                 | of the error situation, and       |
   |                                 | whether it is a temporary or      |
   |                                 | permanent condition, except when  |
   |                                 | responding to a HEAD request.     |
   +---------------------------------+-----------------------------------+
   | 500                             | The server encountered an         |
   |                                 | unexpected condition that         |
   | (Internal Server Error)         | prevented it from fulfilling the  |
   |                                 | request.                          |
   +---------------------------------+-----------------------------------+
   | 501                             | The server does not support the   |
   |                                 | functionality required to fulfill |
   | (Not Implemented)               | the request.                      |
   |                                 |                                   |
   |                                 | In the DICOM context, this status |
   |                                 | code shall be used for SOP Class  |
   |                                 | Not Supported errors.             |
   +---------------------------------+-----------------------------------+
   | 503                             | The origin server is currently    |
   |                                 | unable to handle the request due  |
   | (Service Unavailable)           | to a temporary overload or        |
   |                                 | scheduled maintenance, which will |
   |                                 | likely be alleviated after some   |
   |                                 | delay.                            |
   +---------------------------------+-----------------------------------+
   | 505                             | The origin server does not        |
   |                                 | support, or refuses to support,   |
   | (HTTP Version Not Supported)    | the major version of HTTP that    |
   |                                 | was used in the request message.  |
   +---------------------------------+-----------------------------------+

When a web server determines that a user agent should not receive
certain information, the web server must choose the status code and the
contents of a Status Report carefully. For example, local policy may
dictate that the web service returns a 404 (Not Found) rather than a 401
(Unauthorized) status code to avoid allowing the user agent to infer the
existence of a resource. The status code and payload of the response
needs to be controlled by policy and context, balancing usability of the
returned result against appropriate protection. See also
`biblioentry_title <#biblio_FHIR_AccessDenied>`__ and
`biblioentry_title <#biblio_OWASP_InfoLeakage>`__.

.. _sect_8.6:

Payloads
--------

Both request and response messages may have message bodies. The message
body (if any) of an HTTP message is used to carry the payload of the
message. The message body is identical to the payload unless a content
coding has been applied, as described in
`biblioentry_title <#biblio_RFC_7230>`__ `Section
3.3.1 <http://tools.ietf.org/html/rfc7230#section-3.3.1>`__. This Part
of the Standard uses the term "payload" to denote the message body
before any content coding has been applied to it.

A message may or may not have a payload. A payload may be empty; that
is, its length is zero. If a message has no payload, then the message
shall have neither Content-Encoding nor Content-Length header fields. If
a message has a payload to which a transfer-coding has been applied,
then the message shall have a Content-Encoding header field. If a
message has a payload that has not had a transfer-coding applied, then
the message shall have a Content-Length header field.

Any message containing a payload shall have appropriate Content
Representation `biblioentry_title <#biblio_RFC_7231>`__ `Section
3.1 <http://tools.ietf.org/html/rfc7231#section-3.1>`__ and Payload
Header Fields `biblioentry_title <#biblio_RFC_7231>`__ `Section
3.3 <http://tools.ietf.org/html/rfc7231#section-3.3>`__. Any message
with a payload shall have a Content-Type header field that specifies the
media type of the representation contained in the payload. The media
type specifies whether the payload is single part or multipart (see
`Media Types <#sect_8.7>`__). Any message with a payload should include
a Content-Location header field. See
`biblioentry_title <#biblio_RFC_7231>`__ `Section
3.1.2.2 <http://tools.ietf.org/html/rfc7231#section-3.1.2.2>`__.

.. _sect_8.6.1:

Payload Format
~~~~~~~~~~~~~~

Payloads may be in either single part or multipart format depending on
the media type.

.. _sect_8.6.1.1:

Single Part Payload
^^^^^^^^^^^^^^^^^^^

A single part payload contains one representation that is described by
the Content Representation Header Fields (see `Payload Header
Fields <#sect_8.4.3>`__) contained in the message header. A message with
a single part payload shall have a Content-Type header field with a
single part media-type.

.. _sect_8.6.1.2:

Multipart Payload
^^^^^^^^^^^^^^^^^

A message with a multipart payload contains one or more representations.
The media type of the root representation (see
`biblioentry_title <#biblio_RFC_2387>`__) may be specified by the
Content-Type header field of the message. If no root parameter is
specified, then the root representation is the first representation in
the payload.

Each part in a multipart payload shall start with a boundary string,
followed by a Content-Type header field. See
`table_title <#table_8.6.1-1>`__ for other header fields occurring in
multipart payloads.

.. table:: Multipart Header Fields

   +------------------+------------+-------+----------------------+
   | Name             | Value      | Usage | Description          |
   +==================+============+=======+======================+
   | Content-Type     | media-type | M     |                      |
   +------------------+------------+-------+----------------------+
   | Content-Encoding | encoding   | C     | Shall be present if  |
   |                  |            |       | the response payload |
   |                  |            |       | has a content        |
   |                  |            |       | encoding             |
   +------------------+------------+-------+----------------------+
   | Content-Length   | int        | C     | Shall be present if  |
   |                  |            |       | the response payload |
   |                  |            |       | does not have a      |
   |                  |            |       | content encoding     |
   +------------------+------------+-------+----------------------+
   | Content-Location | url        | C     | Shall be present if  |
   |                  |            |       | the response payload |
   |                  |            |       | contains a           |
   |                  |            |       | representation of a  |
   |                  |            |       | resource. See        |
   |                  |            |       | `biblioentry_title < |
   |                  |            |       | #biblio_RFC_7231>`__ |
   |                  |            |       | `Section             |
   |                  |            |       | 3.1.                 |
   |                  |            |       | 4.2 <http://tools.ie |
   |                  |            |       | tf.org/html/rfc7231# |
   |                  |            |       | section-3.1.4.2>`__. |
   +------------------+------------+-------+----------------------+
   | Location         | url        | C     | See                  |
   |                  |            |       | `biblioentry_title < |
   |                  |            |       | #biblio_RFC_7231>`__ |
   |                  |            |       | `Section             |
   |                  |            |       | 7.1.2 <http://tools. |
   |                  |            |       | ietf.org/html/rfc723 |
   |                  |            |       | 1#section-7.1.2>`__. |
   +------------------+------------+-------+----------------------+

See `Multipart Media Types <#sect_8.7.1>`__ and
`biblioentry_title <#biblio_RFC_7231>`__.

The following is an example template of a multipart request or response
message that has a multipart payload:

::

   request-line / response-line

::

   Content-Type: multipart-media-type CRLF

::

   Content-Location: "/" {/url} CRLF

::

   *(header-field CRLF)

::

   CRLF

::

   multipart-payload

The Content-Type header field shall have a multipart media-type. For
example:

::

   Content-Type: multipart/related; type=DQ root-media-type DQ; boundary="---boundary---"

Where

+-------------------------+-------------------------------------------+
| ::                      | is a media type defined by                |
|                         | `biblioentry_title <#biblio_RFC_2387>`__. |
|    multipart-media-type |                                           |
+-------------------------+-------------------------------------------+
| ::                      | is a single part media type that          |
|                         | specifies the media type of the root,     |
|    root-media-type      | typically the first part, in the payload. |
|                         | If the value of the type parameter and    |
|                         | the root body part's content-type differ  |
|                         | then the user agent's behavior is         |
|                         | undefined.                                |
+-------------------------+-------------------------------------------+
| ::                      | specifies a string that acts as a         |
|                         | boundary between message parts.           |
|    boundary             |                                           |
+-------------------------+-------------------------------------------+

Each part in a multipart payload shall start with a Boundary header
field, followed by a Content-Type header field. Other header fields may
be included, such as Content-Location, and either the Content-Length or
Content-Encoding header field, optionally followed by other header
fields.

If a multipart payload contains Metadata (see `Uncompressed
Bulkdata <#sect_8.7.3.3.1>`__), and Bulkdata (see `Compressed
Bulkdata <#sect_8.7.3.3.2>`__), then all Metadata message parts that
reference a Bulkdata part shall precede the referenced Bulkdata part.

.. _sect_8.6.1.2.1:

Multipart Payload Syntax
''''''''''''''''''''''''

The syntax of a multipart payload is:

::

   multipart-payload = 1*(DASH boundary CRLF part CRLF) DASH boundary DASH

Where

::

   DASH         = "--"
   boundary     = 0*69(bchar / SP) bchar
   bchar        = DIGIT / ALPHA / "'" / "(" / ")" / "+" / "_"   ; The legal boundary characters
                / "," / "-" / "." / "/" / ":" / "=" / "?"
   part         = Content-Type: media-type CRLF
                  Content-Location: url CRLF
                  (Content-Length: uint CRLF / Content-Encoding: encoding CRLF)
                  [Content-Description: text CRLF]
                  *(header-field CRLF)
                  CRLF
                  part-payload
   part-payload = *OCTET

For example, if the boundary is "++++", then a message payload
containing three parts would be structured as follows:

::

   --++++CRLF

::

   Content-Type: media-type CRLF

::

   Content-Location: url CRLF

::

   (Content-Length: uint CRLF / Content-Encoding: encoding CRLF)

::

   [Content-Description: {description} CRLF]

::

   CRLF

::

   payload CRLF

::

   --++++CRLF

::

   Content-Type: media-type CRLF

::

   . . .

::

   payload CRLF

::

   --++++CRLF

::

   Content-Type: media-type CRLF

::

   . . .

::

   payload CRLF

::

   --++++--

`figure_title <#figure_8.6-1>`__ shows the correspondence between the
IOD representation and a multipart payload.

.. _sect_8.6.2:

DICOM Representations
~~~~~~~~~~~~~~~~~~~~~

All DICOM objects are defined by Information Object Definitions (IODs).
See . Representations of DICOM Resources are encodings of DICOM
Information Objects into octet streams.

Each IOD has an associated set of Attributes, which define semantic
concepts. Each Attribute has:

-  a Tag, which identifies the Attribute using an integer

-  a Keyword, which identifies the Attribute using a token

-  a Type, which indicates whether the Attribute is required or optional

-  a Value Representation, which defines the data type of the
   Attribute's value(s)

-  a Value Multiplicity, which specifies the number of values that the
   Attribute may have

A Data Element is a concrete representation of an Attribute See . Each
Data Element has:

-  an identifier, which would typically be its Tag, but could be its
   Keyword

-  a Value Representation, which defines its data type

-  a Value Length

-  a Value Field, which is a sequence of bytes containing zero or more
   values

Each Instance contains Data Elements representing the Attributes from
the Patient, Study, Series, and Instance levels of the IOD. For example,
if a Series resource contains 12 Instances, then a transaction that
retrieves that Series will contain a representation of the Series and
its 12 Instances, in a specific media type, and each Instance will have
Patient, Study, Series, and Instance level Attributes.

This Part of the Standard defines three distinct representations of
DICOM Resources that can be encoded into DICOM Media Types: Instances,
Metadata, and Bulkdata.

DICOM Media Types and their corresponding representations are defined in
`DICOM Media Types and Media Types For Bulkdata <#sect_8.7.3>`__. Other
media types used in this Part of the Standard are defined in `Rendered
Media Types <#sect_8.7.4>`__.

.. _sect_8.6.2.1:

Web Service Constraints
^^^^^^^^^^^^^^^^^^^^^^^

DICOM Web Services only support representations with explicit Value
Representations. Implicit Value Representations (see ) shall not be
used.

.. _sect_8.6.3:

Status Report
~~~~~~~~~~~~~

A Status Report is a description of warnings or errors encountered by
the origin server in processing a request. The contents should be clear
and succinct. If the request does not include an Acceptable Media Type,
the Status Report should use the default media type for the Text
Resource Category, which is text/html.

.. _sect_8.7:

Media Types
-----------

Media types are the basis for both content negotiation and data typing
of message payloads. Each service, and/or transaction defines the media
types and associated representations that are default, required and
optional.

The media type also specifies whether the payload contains a single
representation (single part), or multiple representations (multipart).
Multipart payloads are only defined for the RESTful APIs. See `Multipart
Payload <#sect_8.6.1.2>`__ and `Response <#sect_10.4.3>`__.

Media types are identifiers used to define the data format of a
representation. HTTP uses media types in the Content-Type and Accept
header fields to provide open and extensible data typing and type
negotiation. The syntax of media types is:

::

   media-type = type "/" subtype *(OWS ";" OWS mt-parameter)

Where

::

   type         = token
   subtype      = token
   mt-parameter = mtp-name "=" mtp-value 
   mtp-name     = token
   mtp-value    = (token / quoted-string)

The 'type/subtype' may be followed by parameters in the form of 'name
"=" value' pairs.

The type, subtype, and mtp-name tokens are case-insensitive, but the
case sensitivity of parameter values depends on the semantics of the
parameter name. The presence or absence of a parameter might be
significant to the processing of a media-type, depending on its
definition within the media type registry.

An mtp-value can be transmitted either as a token or quoted-string. The
quoted and unquoted values are equivalent.

Media types are defined in `biblioentry_title <#biblio_RFC_7231>`__
`Section
3.1.1.1 <http://tools.ietf.org/html/rfc7231#section-3.1.1.1>`__.

IANA maintains a registry of media types
`biblioentry_title <#biblio_IANA_MediaTypes>`__.

Many media types specify a character set parameter.

.. note::

   The term "MIME Type" is not synonymous with "Media Type". MIME types
   are defined by Multipurpose Internet Mail Extensions
   `biblioentry_title <#biblio_RFC_2045>`__ and used by email programs.
   Media Types are defined by Media Type Specifications and Registration
   Procedures `biblioentry_title <#biblio_RFC_6838>`__.

.. _sect_8.7.1:

Multipart Media Types
~~~~~~~~~~~~~~~~~~~~~

Some of the services defined in this Part of the Standard support the
multipart media types `biblioentry_title <#biblio_RFC_2387>`__. The
syntax is:

::

   multipart-media-type = "multipart" "/" subtype *(OWS ";" OWS parameter)

The application/multipart-related media type is used by the RESTful
services. Its syntax is:

::

   multipart-related = "multipart/related"
                       OWS ";" OWS "type" "=" DQ media-type DQ
                       OWS ";" OWS "boundary" "=" boundary
                       [related-parameters]

Where

::

   boundary           ; See 

::

   bchar              = bchar-nospace / SP
   bchar-nospace      = DIGIT / ALPHA / "'" / "(" / ")" / "+" / "_" / "," / "-"
                        / "." / "/" / ":" / "=" / "?" "/" / ":" / "=" / "?"
   related-parameters = [";" "start" "=" cid]
                        [";" "start-info" "=" cid-list]
   cid-list           = cid cid-list
   cid                = token / quoted-string

The "type" parameter is required. It contains the media type of the
"root" body part. It always contains the special character "/" and thus
requires quote marks.

The cid is a content identifier. It should be unique for each part of
the multipart message.

Typically, the "start" and "start-info" parameters are not specified,
and the "root" is the first body part.

.. _sect_8.7.2:

DICOM Resource Categories
~~~~~~~~~~~~~~~~~~~~~~~~~

`table_title <#table_8.7.2-1>`__ defines Resource Categories that
correspond to different SOP Classes. The following sections map each
Resource Category to appropriate DICOM and Rendered media types.

.. table:: Resource Categories

   +--------------------+------------------------------------------------+
   | Resource Category  | Definition                                     |
   +====================+================================================+
   | Single Frame Image | This category includes all resources that are: |
   |                    |                                                |
   |                    | 1. Instances of a single frame SOP Class, or   |
   |                    |                                                |
   |                    | 2. Instances of a multi-frame SOP Class that   |
   |                    |    contain only one frame, or                  |
   |                    |                                                |
   |                    | 3. a single frame selected from an Instance of |
   |                    |    a multi-frame SOP Class.                    |
   +--------------------+------------------------------------------------+
   | Multi-Frame Image  | This category includes all resources that are  |
   |                    | Instances of a multi-frame SOP Class, that are |
   |                    | not Video and that contain more than one       |
   |                    | frame.                                         |
   +--------------------+------------------------------------------------+
   | Video              | This category includes all resources that      |
   |                    | contain more than one frame and are:           |
   |                    |                                                |
   |                    | 1. Instances encoded in the MPEG family of     |
   |                    |    Transfer Syntaxes (which includes MP4 and   |
   |                    |    H.265), or                                  |
   |                    |                                                |
   |                    | 2. time-based (motion) multi-frame images that |
   |                    |    the origin server is capable of encoding in |
   |                    |    the MPEG family.                            |
   +--------------------+------------------------------------------------+
   | Text               | This category includes all resources that      |
   |                    | contain:                                       |
   |                    |                                                |
   |                    | 1. the SR Document Content Module (see ), such |
   |                    |    as narrative text, Structured Reports, CAD, |
   |                    |    measurement reports, and key object         |
   |                    |    selection documents, or                     |
   |                    |                                                |
   |                    | 2. the Encapsulated Document Module (see ).    |
   +--------------------+------------------------------------------------+
   | Other              | This category includes all resources that are  |
   |                    | not included above, for example waveforms.     |
   +--------------------+------------------------------------------------+

.. _sect_8.7.3:

DICOM Media Types and Media Types For Bulkdata
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

This section defines the media types used to represent DICOM Instances,
Metadata and Bulkdata. It describes:

-  The media type and Transfer Syntax parameters for DICOM Instances

-  The media types that can be used for Metadata

-  The media types and Transfer Syntaxes parameters for Bulkdata

-  The syntax of DICOM Media Types including their Transfer Syntax and
   character set parameters

-  The Query Parameter for Transfer Syntax

-  The meaning of Acceptable Transfer Syntaxes and Selected Transfer
   Syntax

The media types defined in this section are distinct from those into
which DICOM Instances may be rendered (which are defined in `Rendered
Media Types <#sect_8.7.4>`__); some of the same media types are used for
both rendered content and Bulkdata.

Depending on the service, the media types may be single part or
multipart, and may have required or optional Transfer Syntax and/or
character set parameters.

The Implicit VR Little Endian (1.2.840.10008.1.2), and Explicit VR Big
Endian (1.2.840.10008.1.2.2 - Retired) Transfer Syntaxes shall not be
used with Web Services.

If a Transfer Syntax parameter for a DICOM Media Type is not specified
in a request or response, the Transfer Syntax in the response shall be
the Transfer Syntax specified as the default for the Resource Category
and media type combination in `table_title <#table_8.7.3-2>`__,
`table_title <#table_8.7.3-4>`__ or `table_title <#table_8.7.3-5>`__,
unless the origin server has only access to the pixel data in lossy
compressed form or the pixel data in a lossless compressed form that is
of such length that it cannot be encoded in the Explicit VR Little
Endian Transfer Syntax.

`table_title <#table_8.7.3-1>`__ specifies the definition of media type
requirement terms used in the tables in this section.

.. table:: Definition of Media Type Requirement

   +-------------+-------------+----------------------------------------+
   | Requirement | Optionality | Definition                             |
   +=============+=============+========================================+
   | Default     | D           | The origin server shall return this    |
   |             |             | media type when none of the Acceptable |
   |             |             | Media Types (see `Acceptable Media     |
   |             |             | Types <#sect_8.7.5>`__) are supported. |
   |             |             | The origin server shall support this   |
   |             |             | media type.                            |
   +-------------+-------------+----------------------------------------+
   | Required    | R           | The origin server shall support this   |
   |             |             | media type.                            |
   +-------------+-------------+----------------------------------------+
   | Optional    | O           | The origin server may support this     |
   |             |             | media types.                           |
   +-------------+-------------+----------------------------------------+

`table_title <#table_8.7.3-2>`__, `table_title <#table_8.7.3-3>`__,
`table_title <#table_8.7.3-4>`__, and `table_title <#table_8.7.3-5>`__
specify the media types used to encode different representations of
DICOM Instances. These media types apply to all Resource Categories and
have default encodings for images and video data elements contained in
the Instances.

.. _sect_8.7.3.1:

The application/dicom Media Type
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

The application/dicom media type specifies a representation of Instances
encoded in the DICOM File Format specified in .

.. note::

   The origin server may populate the File Meta Information with the
   identification of the Source, Sending and Receiving AE Titles and
   Presentation Addresses as described in , or these Attributes may have
   been left unaltered from when the origin server received the objects.
   The user agent storing the objects received in the response may
   populate or coerce these Attributes based on its own knowledge of the
   endpoints involved in the transaction, so that they accurately
   identify the most recent storage transaction.

`table_title <#table_8.7.3-2>`__ specifies the default and optional
Transfer Syntax UID combinations for each DICOM Resource Category (see
`table_title <#table_8.7.2-1>`__). The default media type for the
Resource Category shall be returned when the origin server supports none
of the Acceptable Media Types, unless the origin server has only access
to the pixel data in lossy compressed form or the pixel data in a
lossless compressed form that is of such length that it cannot be
encoded in the Explicit VR Little Endian Transfer Syntax.

.. table:: Transfer Syntax UIDs for application/dicom Media Types

   +-----------------+-----------------+-----------------+-------------+
   | Category        | Transfer Syntax | Transfer Syntax | Optionality |
   |                 | UID             | Name            |             |
   +=================+=================+=================+=============+
   | Single Frame    | 1.2.            | Explicit VR     | D           |
   | Image           | 840.10008.1.2.1 | Little Endian   |             |
   +-----------------+-----------------+-----------------+-------------+
   | 1.2.840         | JPEG Lossless,  | O               |             |
   | .10008.1.2.4.70 | No              |                 |             |
   |                 | n-Hierarchical, |                 |             |
   |                 | First-Order     |                 |             |
   |                 | Pre             |                 |             |
   |                 | diction(Process |                 |             |
   |                 | 14 [Selection   |                 |             |
   |                 | Value 1]):      |                 |             |
   |                 | Default         |                 |             |
   |                 | Transfer Syntax |                 |             |
   |                 | for Lossless    |                 |             |
   |                 | JPEG Image      |                 |             |
   |                 | Compression     |                 |             |
   +-----------------+-----------------+-----------------+-------------+
   | 1.2.840         | JPEG Baseline   | O               |             |
   | .10008.1.2.4.50 | (Process 1):    |                 |             |
   |                 | Default         |                 |             |
   |                 | Transfer Syntax |                 |             |
   |                 | for Lossy JPEG  |                 |             |
   |                 | 8 Bit Image     |                 |             |
   |                 | Compression     |                 |             |
   +-----------------+-----------------+-----------------+-------------+
   | 1.2.840         | JPEG Extended   | O               |             |
   | .10008.1.2.4.51 | (Process 2 &    |                 |             |
   |                 | 4): Default     |                 |             |
   |                 | Transfer Syntax |                 |             |
   |                 | for Lossy JPEG  |                 |             |
   |                 | 12 Bit Image    |                 |             |
   |                 | Compression     |                 |             |
   |                 | (Process 4      |                 |             |
   |                 | only)           |                 |             |
   +-----------------+-----------------+-----------------+-------------+
   | 1.2.840         | JPEG Lossless,  | O               |             |
   | .10008.1.2.4.57 | N               |                 |             |
   |                 | on-Hierarchical |                 |             |
   |                 | (Process 14)    |                 |             |
   +-----------------+-----------------+-----------------+-------------+
   | 1.2.            | RLE Lossless    | O               |             |
   | 840.10008.1.2.5 |                 |                 |             |
   +-----------------+-----------------+-----------------+-------------+
   | 1.2.840         | JPEG-LS         | O               |             |
   | .10008.1.2.4.80 | Lossless Image  |                 |             |
   |                 | Compression     |                 |             |
   +-----------------+-----------------+-----------------+-------------+
   | 1.2.840         | JPEG-LS Lossy   | O               |             |
   | .10008.1.2.4.81 | (Near-Lossless) |                 |             |
   |                 | Image           |                 |             |
   |                 | Compression     |                 |             |
   +-----------------+-----------------+-----------------+-------------+
   | 1.2.840         | JPEG 2000 Image | O               |             |
   | .10008.1.2.4.90 | Compression     |                 |             |
   |                 | (Lossless Only) |                 |             |
   +-----------------+-----------------+-----------------+-------------+
   | 1.2.840         | JPEG 2000 Image | O               |             |
   | .10008.1.2.4.91 | Compression     |                 |             |
   +-----------------+-----------------+-----------------+-------------+
   | 1.2.840         | JPEG 2000 Part  | O               |             |
   | .10008.1.2.4.92 | 2               |                 |             |
   |                 | Multi-component |                 |             |
   |                 | Image           |                 |             |
   |                 | Compression     |                 |             |
   |                 | (Lossless Only) |                 |             |
   +-----------------+-----------------+-----------------+-------------+
   | 1.2.840         | JPEG 2000 Part  | O               |             |
   | .10008.1.2.4.93 | 2               |                 |             |
   |                 | Multi-component |                 |             |
   |                 | Image           |                 |             |
   |                 | Compression     |                 |             |
   +-----------------+-----------------+-----------------+-------------+
   | Multi-frame     | 1.2.            | Explicit VR     | D           |
   | Image           | 840.10008.1.2.1 | Little Endian   |             |
   +-----------------+-----------------+-----------------+-------------+
   | 1.2.840         | JPEG 2000 Image | O               |             |
   | .10008.1.2.4.90 | Compression     |                 |             |
   |                 | (Lossless Only) |                 |             |
   +-----------------+-----------------+-----------------+-------------+
   | 1.2.840         | JPEG 2000 Image | O               |             |
   | .10008.1.2.4.91 | Compression     |                 |             |
   +-----------------+-----------------+-----------------+-------------+
   | 1.2.840         | JPEG 2000 Part  | O               |             |
   | .10008.1.2.4.92 | 2               |                 |             |
   |                 | Multi-component |                 |             |
   |                 | Image           |                 |             |
   |                 | Compression     |                 |             |
   |                 | (Lossless Only) |                 |             |
   +-----------------+-----------------+-----------------+-------------+
   | 1.2.840         | JPEG 2000 Part  | O               |             |
   | .10008.1.2.4.93 | 2               |                 |             |
   |                 | Multi-component |                 |             |
   |                 | Image           |                 |             |
   |                 | Compression     |                 |             |
   +-----------------+-----------------+-----------------+-------------+
   | Video           | 1.2.            | Explicit VR     | D           |
   |                 | 840.10008.1.2.1 | Little Endian   |             |
   +-----------------+-----------------+-----------------+-------------+
   | 1.2.840.        | MPEG2 Main      | O               |             |
   | 10008.1.2.4.100 | Profile @ Main  |                 |             |
   |                 | Level           |                 |             |
   +-----------------+-----------------+-----------------+-------------+
   | 1.2.840.        | MPEG2 Main      | O               |             |
   | 10008.1.2.4.101 | Profile @ High  |                 |             |
   |                 | Level           |                 |             |
   +-----------------+-----------------+-----------------+-------------+
   | 1.2.840.        | MPEG-4          | O               |             |
   | 10008.1.2.4.102 | AVC/H.264 High  |                 |             |
   |                 | Profile / Level |                 |             |
   |                 | 4.1             |                 |             |
   +-----------------+-----------------+-----------------+-------------+
   | 1.2.840.        | MPEG-4          | O               |             |
   | 10008.1.2.4.103 | AVC/H.264       |                 |             |
   |                 | BD-compatible   |                 |             |
   |                 | High Profile /  |                 |             |
   |                 | Level 4.1       |                 |             |
   +-----------------+-----------------+-----------------+-------------+
   | 1.2.840.        | MPEG-4          | O               |             |
   | 10008.1.2.4.104 | AVC/H.264 High  |                 |             |
   |                 | Profile / Level |                 |             |
   |                 | 4.2 For 2D      |                 |             |
   |                 | Video           |                 |             |
   +-----------------+-----------------+-----------------+-------------+
   | 1.2.840.        | MPEG-4          | O               |             |
   | 10008.1.2.4.105 | AVC/H.264 High  |                 |             |
   |                 | Profile / Level |                 |             |
   |                 | 4.2 For 3D      |                 |             |
   |                 | Video           |                 |             |
   +-----------------+-----------------+-----------------+-------------+
   | 1.2.840.        | MPEG-4          | O               |             |
   | 10008.1.2.4.106 | AVC/H.264       |                 |             |
   |                 | Stereo High     |                 |             |
   |                 | Profile / Level |                 |             |
   |                 | 4.2             |                 |             |
   +-----------------+-----------------+-----------------+-------------+
   | Text            | 1.2.            | Explicit VR     | D           |
   |                 | 840.10008.1.2.1 | Little Endian   |             |
   +-----------------+-----------------+-----------------+-------------+
   | Other           | 1.2.            | Explicit VR     | D           |
   |                 | 840.10008.1.2.1 | Little Endian   |             |
   +-----------------+-----------------+-----------------+-------------+

.. _sect_8.7.3.2:

DICOM Metadata Media Types
^^^^^^^^^^^^^^^^^^^^^^^^^^

`table_title <#table_8.7.3-3>`__ specifies the media types that may be
used to encode representations of Metadata for the URI and RESTful
services. Only the RESTful Services support Metadata representations.

.. table:: Media Types for Metadata

   +------------------+------------------+----------------+----------+
   | Media Type       | Descriptions     | URI            | RESTful  |
   +==================+==================+================+==========+
   | appli            | Encodes          | not applicable | required |
   | cation/dicom+xml | Instances as XML |                |          |
   |                  | Infosets defined |                |          |
   |                  | in the Native    |                |          |
   |                  | DICOM Model      |                |          |
   |                  | defined in .     |                |          |
   +------------------+------------------+----------------+----------+
   | applic           | Encodes          | not applicable | required |
   | ation/dicom+json | Instances in the |                |          |
   |                  | JSON format      |                |          |
   |                  | defined in       |                |          |
   |                  | `DICOM JSON      |                |          |
   |                  | Model            |                |          |
   |                  | <#chapter_F>`__. |                |          |
   +------------------+------------------+----------------+----------+

.. _sect_8.7.3.3:

DICOM Bulkdata Media Types
^^^^^^^^^^^^^^^^^^^^^^^^^^

Bulkdata representations are only supported by RESTful services. There
are two categories of Bulkdata: uncompressed and compressed.

The default media type for the Resource Category shall be returned when
the origin server supports none of the Acceptable Media Types, unless
the origin server has only access to the pixel data in lossy compressed
form or the pixel data in a lossless compressed form that is of such
length that it cannot be encoded in the Explicit VR Little Endian
Transfer Syntax.

The origin server may support additional Transfer Syntaxes.

If no media type Transfer Syntax parameter is specified, then the
Explicit VR Little Endian Transfer Syntax "1.2.840.10008.1.2.1" shall be
used, unless the origin server has only access to the pixel data in
lossy compressed form or the pixel data in a lossless compressed form
that is of such length that it cannot be encoded in the Explicit VR
Little Endian Transfer Syntax.

.. note::

   The tables in this section have no entries for the URI service, since
   they do not support separate retrieval of Bulkdata.

.. _sect_8.7.3.3.1:

Uncompressed Bulkdata
'''''''''''''''''''''

`table_title <#table_8.7.3-4>`__ specifies the default media type and
Transfer Syntax UIDs, by Resource Category (see
`table_title <#table_8.7.2-1>`__) that can be used with uncompressed
Bulkdata for the RESTful services. Uncompressed Bulkdata is encoded as a
stream of uncompressed bytes (octets) in Little Endian byte order.

.. note::

   This is the same encoding defined in for the returned value of the
   getData() call for uncompressed Bulkdata.

.. table:: Transfer Syntax UIDs for Uncompressed Data in Bulkdata

   +--------------+--------------+--------------+--------------+---------+
   | Category     | Media Type   | Transfer     | Transfer     | RESTful |
   |              |              | Syntax UID   | Syntax Name  |         |
   +==============+==============+==============+==============+=========+
   | Single Frame | application/ | 1.2.840      | Explicit VR  | D       |
   | Image        | octet-stream | .10008.1.2.1 | Little       |         |
   |              |              |              | Endian       |         |
   +--------------+--------------+--------------+--------------+---------+
   | Multi-Frame  | application/ | 1.2.840      | Explicit VR  | D       |
   | Image        | octet-stream | .10008.1.2.1 | Little       |         |
   |              |              |              | Endian       |         |
   +--------------+--------------+--------------+--------------+---------+
   | Video        | application/ | 1.2.840      | Explicit VR  | D       |
   |              | octet-stream | .10008.1.2.1 | Little       |         |
   |              |              |              | Endian       |         |
   +--------------+--------------+--------------+--------------+---------+
   | Text         | application/ | 1.2.840      | Explicit VR  | D       |
   |              | octet-stream | .10008.1.2.1 | Little       |         |
   |              |              |              | Endian       |         |
   +--------------+--------------+--------------+--------------+---------+
   | Other        | application/ | 1.2.840      | Explicit VR  | D       |
   |              | octet-stream | .10008.1.2.1 | Little       |         |
   |              |              |              | Endian       |         |
   +--------------+--------------+--------------+--------------+---------+

.. note::

   Even though the Transfer Syntax is Explicit VR Little Endian, the
   Value Representation is not actually encoded at the beginning of the
   octet-stream. The Value Representation is contained in the Metadata
   that references the Bulkdata.

.. _sect_8.7.3.3.2:

Compressed Bulkdata
'''''''''''''''''''

Compressed Bulkdata contains only the compressed octet stream without
the fragment delimiters.

`table_title <#table_8.7.3-5>`__ specifies the default and optional
media types and Transfer Syntax UID combinations for each Resource
Category (see `table_title <#table_8.7.2-1>`__) of compressed Bulkdata
for the RESTful services.

.. note::

   Some of the Transfer Syntax Names include text about Default Transfer
   Syntax, however this applies to its role in DIMSE transactions,
   rather than the default for RESTful services (which is specified in
   the RESTful column of the table).

These media types can be used to retrieve Bulkdata, such as images or
video, encoded in a specific Transfer Syntax.

.. table:: Media Types and Transfer Syntax UIDs for Compressed Data in
Bulkdata

   +-------------+-------------+-------------+-------------+-------------+
   | Category    | Media Type  | Transfer    | Transfer    | Optionality |
   |             |             | Syntax UID  | Syntax Name |             |
   +=============+=============+=============+=============+=============+
   | Single      | image/jpeg  | 1.2.840.100 | JPEG        | D           |
   | Frame Image |             | 08.1.2.4.70 | Lossless,   |             |
   |             |             |             | Non-Hi      |             |
   |             |             |             | erarchical, |             |
   |             |             |             | First-Order |             |
   |             |             |             | Predict     |             |
   |             |             |             | ion(Process |             |
   |             |             |             | 14          |             |
   |             |             |             | [Selection  |             |
   |             |             |             | Value 1])   |             |
   |             |             |             | :Default    |             |
   |             |             |             | Transfer    |             |
   |             |             |             | Syntax for  |             |
   |             |             |             | Lossless    |             |
   |             |             |             | JPEG Image  |             |
   |             |             |             | Compression |             |
   +-------------+-------------+-------------+-------------+-------------+
   | 1.2.840.100 | JPEG        | O           |             |             |
   | 08.1.2.4.50 | Baseline    |             |             |             |
   |             | (Process 1) |             |             |             |
   |             | :Default    |             |             |             |
   |             | Transfer    |             |             |             |
   |             | Syntax for  |             |             |             |
   |             | Lossy JPEG  |             |             |             |
   |             | 8 Bit Image |             |             |             |
   |             | Compression |             |             |             |
   +-------------+-------------+-------------+-------------+-------------+
   | 1.2.840.100 | JPEG        | O           |             |             |
   | 08.1.2.4.51 | Extended    |             |             |             |
   |             | (Process 2  |             |             |             |
   |             | & 4)        |             |             |             |
   |             | :Default    |             |             |             |
   |             | Transfer    |             |             |             |
   |             | Syntax for  |             |             |             |
   |             | Lossy JPEG  |             |             |             |
   |             | 12 Bit      |             |             |             |
   |             | Image       |             |             |             |
   |             | Compression |             |             |             |
   |             | (Process 4  |             |             |             |
   |             | only)       |             |             |             |
   +-------------+-------------+-------------+-------------+-------------+
   | 1.2.840.100 | JPEG        | O           |             |             |
   | 08.1.2.4.57 | Lossless,   |             |             |             |
   |             | Non-H       |             |             |             |
   |             | ierarchical |             |             |             |
   |             | (Process    |             |             |             |
   |             | 14)         |             |             |             |
   +-------------+-------------+-------------+-------------+-------------+
   | imag        | 1.2.840.    | RLE         | D           |             |
   | e/dicom-rle | 10008.1.2.5 | Lossless    |             |             |
   +-------------+-------------+-------------+-------------+-------------+
   | image/jls   | 1.2.840.100 | JPEG-LS     | D           |             |
   |             | 08.1.2.4.80 | Lossless    |             |             |
   |             |             | Image       |             |             |
   |             |             | Compression |             |             |
   +-------------+-------------+-------------+-------------+-------------+
   | 1.2.840.100 | JPEG-LS     | O           |             |             |
   | 08.1.2.4.81 | Lossy       |             |             |             |
   |             | (Nea        |             |             |             |
   |             | r-Lossless) |             |             |             |
   |             | Image       |             |             |             |
   |             | Compression |             |             |             |
   +-------------+-------------+-------------+-------------+-------------+
   | image/jp2   | 1.2.840.100 | JPEG 2000   | D           |             |
   |             | 08.1.2.4.90 | Image       |             |             |
   |             |             | Compression |             |             |
   |             |             | (Lossless   |             |             |
   |             |             | Only)       |             |             |
   +-------------+-------------+-------------+-------------+-------------+
   | 1.2.840.100 | JPEG 2000   | O           |             |             |
   | 08.1.2.4.91 | Image       |             |             |             |
   |             | Compression |             |             |             |
   +-------------+-------------+-------------+-------------+-------------+
   | image/jpx   | 1.2.840.100 | JPEG 2000   | D           |             |
   |             | 08.1.2.4.92 | Part 2      |             |             |
   |             |             | Mult        |             |             |
   |             |             | i-component |             |             |
   |             |             | Image       |             |             |
   |             |             | Compression |             |             |
   |             |             | (Lossless   |             |             |
   |             |             | Only)       |             |             |
   +-------------+-------------+-------------+-------------+-------------+
   | 1.2.840.100 | JPEG 2000   | O           |             |             |
   | 08.1.2.4.93 | Part 2      |             |             |             |
   |             | Mult        |             |             |             |
   |             | i-component |             |             |             |
   |             | Image       |             |             |             |
   |             | Compression |             |             |             |
   +-------------+-------------+-------------+-------------+-------------+
   | Multi-frame | image/jpeg  | 1.2.840.100 | JPEG        | D           |
   | Image       |             | 08.1.2.4.70 | Lossless,   |             |
   |             |             |             | Non-Hi      |             |
   |             |             |             | erarchical, |             |
   |             |             |             | First-Order |             |
   |             |             |             | Predict     |             |
   |             |             |             | ion(Process |             |
   |             |             |             | 14          |             |
   |             |             |             | [Selection  |             |
   |             |             |             | Value 1])   |             |
   |             |             |             | :Default    |             |
   |             |             |             | Transfer    |             |
   |             |             |             | Syntax for  |             |
   |             |             |             | Lossless    |             |
   |             |             |             | JPEG Image  |             |
   |             |             |             | Compression |             |
   +-------------+-------------+-------------+-------------+-------------+
   | 1.2.840.100 | JPEG        | O           |             |             |
   | 08.1.2.4.50 | Baseline    |             |             |             |
   |             | (Process 1) |             |             |             |
   |             | :Default    |             |             |             |
   |             | Transfer    |             |             |             |
   |             | Syntax for  |             |             |             |
   |             | Lossy JPEG  |             |             |             |
   |             | 8 Bit Image |             |             |             |
   |             | Compression |             |             |             |
   +-------------+-------------+-------------+-------------+-------------+
   | 1.2.840.100 | JPEG        | O           |             |             |
   | 08.1.2.4.51 | Extended    |             |             |             |
   |             | (Process 2  |             |             |             |
   |             | & 4)        |             |             |             |
   |             | :Default    |             |             |             |
   |             | Transfer    |             |             |             |
   |             | Syntax for  |             |             |             |
   |             | Lossy JPEG  |             |             |             |
   |             | 12 Bit      |             |             |             |
   |             | Image       |             |             |             |
   |             | Compression |             |             |             |
   |             | (Process 4  |             |             |             |
   |             | only)       |             |             |             |
   +-------------+-------------+-------------+-------------+-------------+
   | 1.2.840.100 | JPEG        | O           |             |             |
   | 08.1.2.4.57 | Lossless,   |             |             |             |
   |             | Non-H       |             |             |             |
   |             | ierarchical |             |             |             |
   |             | (Process    |             |             |             |
   |             | 14)         |             |             |             |
   +-------------+-------------+-------------+-------------+-------------+
   | imag        | 1.2.840.    | RLE         | D           |             |
   | e/dicom-rle | 10008.1.2.5 | Lossless    |             |             |
   +-------------+-------------+-------------+-------------+-------------+
   | image/jls   | 1.2.840.100 | JPEG-LS     | D           |             |
   |             | 08.1.2.4.80 | Lossless    |             |             |
   |             |             | Image       |             |             |
   |             |             | Compression |             |             |
   +-------------+-------------+-------------+-------------+-------------+
   | 1.2.840.100 | JPEG-LS     | O           |             |             |
   | 08.1.2.4.81 | Lossy       |             |             |             |
   |             | (Nea        |             |             |             |
   |             | r-Lossless) |             |             |             |
   |             | Image       |             |             |             |
   |             | Compression |             |             |             |
   +-------------+-------------+-------------+-------------+-------------+
   | image/jp2   | 1.2.840.100 | JPEG 2000   | D           |             |
   |             | 08.1.2.4.90 | Image       |             |             |
   |             |             | Compression |             |             |
   |             |             | (Lossless   |             |             |
   |             |             | Only)       |             |             |
   +-------------+-------------+-------------+-------------+-------------+
   | 1.2.840.100 | JPEG 2000   | O           |             |             |
   | 08.1.2.4.91 | Image       |             |             |             |
   |             | Compression |             |             |             |
   +-------------+-------------+-------------+-------------+-------------+
   | image/jpx   | 1.2.840.100 | JPEG 2000   | D           |             |
   |             | 08.1.2.4.92 | Part 2      |             |             |
   |             |             | Mult        |             |             |
   |             |             | i-component |             |             |
   |             |             | Image       |             |             |
   |             |             | Compression |             |             |
   |             |             | (Lossless   |             |             |
   |             |             | Only)       |             |             |
   +-------------+-------------+-------------+-------------+-------------+
   | 1.2.840.100 | JPEG 2000   | O           |             |             |
   | 08.1.2.4.93 | Part 2      |             |             |             |
   |             | Mult        |             |             |             |
   |             | i-component |             |             |             |
   |             | Image       |             |             |             |
   |             | Compression |             |             |             |
   +-------------+-------------+-------------+-------------+-------------+
   | Video       | video/mpeg2 | 1           | MPEG2 Main  | O           |
   |             |             | .2.840.1000 | Profile @   |             |
   |             |             | 8.1.2.4.100 | Main Level  |             |
   +-------------+-------------+-------------+-------------+-------------+
   | 1           | MPEG2 Main  | D           |             |             |
   | .2.840.1000 | Profile @   |             |             |             |
   | 8.1.2.4.101 | High Level  |             |             |             |
   +-------------+-------------+-------------+-------------+-------------+
   | video/mp4   | 1           | MPEG-4      | D           |             |
   |             | .2.840.1000 | AVC/H.264   |             |             |
   |             | 8.1.2.4.102 | High        |             |             |
   |             |             | Profile /   |             |             |
   |             |             | Level 4.1   |             |             |
   +-------------+-------------+-------------+-------------+-------------+
   | 1           | MPEG-4      | O           |             |             |
   | .2.840.1000 | AVC/H.264   |             |             |             |
   | 8.1.2.4.103 | BD          |             |             |             |
   |             | -compatible |             |             |             |
   |             | High        |             |             |             |
   |             | Profile /   |             |             |             |
   |             | Level 4.1   |             |             |             |
   +-------------+-------------+-------------+-------------+-------------+
   | 1           | MPEG-4      | O           |             |             |
   | .2.840.1000 | AVC/H.264   |             |             |             |
   | 8.1.2.4.104 | High        |             |             |             |
   |             | Profile /   |             |             |             |
   |             | Level 4.2   |             |             |             |
   |             | For 2D      |             |             |             |
   |             | Video       |             |             |             |
   +-------------+-------------+-------------+-------------+-------------+
   | 1           | MPEG-4      | O           |             |             |
   | .2.840.1000 | AVC/H.264   |             |             |             |
   | 8.1.2.4.105 | High        |             |             |             |
   |             | Profile /   |             |             |             |
   |             | Level 4.2   |             |             |             |
   |             | For 3D      |             |             |             |
   |             | Video       |             |             |             |
   +-------------+-------------+-------------+-------------+-------------+
   | 1           | MPEG-4      | O           |             |             |
   | .2.840.1000 | AVC/H.264   |             |             |             |
   | 8.1.2.4.106 | Stereo High |             |             |             |
   |             | Profile /   |             |             |             |
   |             | Level 4.2   |             |             |             |
   +-------------+-------------+-------------+-------------+-------------+
   | Text        |             | N/A (no     |             |             |
   |             |             | defined     |             |             |
   |             |             | compression |             |             |
   |             |             | transfer    |             |             |
   |             |             | syntaxes    |             |             |
   |             |             | for Text)   |             |             |
   +-------------+-------------+-------------+-------------+-------------+
   | Other       |             | N/A (no     |             |             |
   |             |             | defined     |             |             |
   |             |             | compression |             |             |
   |             |             | transfer    |             |             |
   |             |             | syntaxes    |             |             |
   |             |             | for Other)  |             |             |
   +-------------+-------------+-------------+-------------+-------------+

The origin server may support additional Transfer Syntaxes.

.. note::

   1. For the media type image/jpeg Transfer Syntaxes, the image may or
      may not include the JFIF marker segment. The image may or may not
      include APP2 marker segments with an identifier of "ICC_PROFILE".
      There is no requirement for the origin server to add a JFIF marker
      segment nor to copy the value of the ICC Profile (0028,2000)
      Attribute, if present, into APP2 marker segments in the compressed
      data stream. See .

   2. For the media type image/jp2 and image/jpx Transfer Syntaxes, the
      image does not include the jp2 marker segment. See and

   3. The resource on the origin server may have been encoded in the
      Deflated Explicit VR Little Endian (1.2.840.10008.1.2.1.99)
      Transfer Syntax. If so, the origin server may inflate it, and then
      convert it into an Acceptable Transfer Syntax. Alternatively, if
      the user agent allowed a Content-Encoding header field of
      'deflate', then the deflated bytes may be transferred unaltered,
      but the Transfer Syntax parameter in the response should be the
      Explicit VR Little Endian Transfer Syntax.

   4. Compressed multi-frame image Bulkdata is encoded as one frame per
      part. E.g., each frame of a JPEG 2000 multi-frame image will be
      encoded as a separate part with an image/jp2 media type, rather
      than as a single part with a video/mj2
      (`biblioentry_title <#biblio_RFC_3745>`__) or uncompressed
      application/octet-stream media type.

   5. Video Bulkdata is encoded as a single part containing all frames.
      E.g., all frames of an MPEG-4 video will be encoded as a single
      part with a video/mp4 (`biblioentry_title <#biblio_RFC_4337>`__)
      media type.

   6. Many of the media types used for compressed Pixel Data transferred
      as Bulkdata values are also used for consumer format media types.
      A web browser may not be able to display the encoded data
      directly, even though some of the same media types are also used
      for encoding rendered Pixel Data. See `Rendered Media
      Types <#sect_8.7.4>`__.

      For example, the media type for Bulkdata values of lossless 16-bit
      JPEG `biblioentry_title <#biblio_ISOIEC10918-1>`__ encoded Pixel
      Data is "image/jpeg", the same media type as might be used for
      8-bit JPEG `biblioentry_title <#biblio_ISOIEC10918-1>`__ encoded
      Pixel Data, whether extracted as Bulkdata, or rendered. The
      Transfer Syntax parameter of the Content-Type header field is
      useful to signal the difference.

   7. Each part of a multipart response is distinguished by the
      Content-Type and Content-Location header fields of the part.

   8. Previously, experimental Media Types "image/x-dicom-rle" and
      "image/x-jls" were defined, so origin servers and user agents may
      want to account for these when communicating with older
      implementations. These have been replaced with the standard Media
      Types "image/dicom-rle" and "image/jls", respectively.

.. _sect_8.7.3.4:

Transfer Syntax
^^^^^^^^^^^^^^^

The Default Transfer Syntax for DICOM objects contained in a payload
shall be Explicit VR Little Endian Uncompressed "1.2.840.10008.1.2.1".
If the Transfer Syntax is not specified in a message, then the Default
Transfer Syntax shall be used, unless the origin server has only access
to the pixel data in lossy compressed form or the pixel data in a
lossless compressed form that is of such length that it cannot be
encoded in the Explicit VR Little Endian Transfer Syntax.

.. note::

   1. This is different from the Default Transfer Syntax defined in ,
      which is Implicit VR Little Endian.

   2. Every origin server is required to be able to convert any Data Set
      it is going to return into the Explicit VR Little Endian Transfer
      Syntax, regardless of the form in which it originally received or
      stored the Data Set, except in the cases of when the decompressed
      Pixel Data is too large to encode in the Explicit VR Little Endian
      Transfer Syntax or is received in a lossy compressed form. In the
      case of lossy compressed Pixel Data, the origin server is
      permitted to return the lossy compressed Transfer Syntax
      appropriate to the lossy form that was received. In the case of
      lossless compressed Pixel Data that is too large to encode in the
      Explicit VR Little Endian Transfer Syntax, the origin server is
      permitted to return any appropriate lossless compression Transfer
      Syntax, not necessarily that in which the image was received, as
      an alternative to the Explicit VR Little Endian Transfer Syntax.

   3. If transcoding to the Explicit VR Little Endian Transfer Syntax, a
      VR of UN may be needed for the encoding of Data Elements with
      explicit VR whose value length exceeds 65534 (2\ :sup:`16`-2)
      (FFFEH, the largest even length unsigned 16 bit number) but which
      are defined to have a 16 bit explicit VR length field. See .

Implicit VR Little Endian, or Explicit VR Big Endian shall not be used.

The response payload encoding requirements are defined in `Selected
Media Type and Transfer Syntax <#sect_8.7.8>`__.

.. note::

   The transfer syntax can be one of the JPIP Transfer Syntaxes, in
   which case the returned objects will contain the URL of the JPIP
   provider for retrieving the pixel data.

The origin server may support additional Transfer Syntaxes.

.. _sect_8.7.3.5:

DICOM Media Type Syntax
^^^^^^^^^^^^^^^^^^^^^^^

The syntax of DICOM Media Types is:

::

   dicom-media-type = (dcm-singlepart / dcm-multipart) [dcm-parameters]

Where

::

   dcm-singlepart = dcm-mt-name

::

   dcm-multipart  ;see 

::

   dcm-parameters = transfer-syntax-mtp ;see 

::

                  / charset-mtp;see 

::

   dcm-mt-name    = dicom / dicom-xml / dicom-json ;DICOM Media Type name

::

   dicom          = "application/dicom"

::

   dicom-xml      = "application/dicom+xml"

::

   dicom-json     = "application/dicom+json"

::

   octet-stream   = "application/octet-stream"

All DICOM Media Types may have a Transfer Syntax parameter, but its
usage may be constrained by the service for which they are used.

.. note::

   The application/dicom+xml and application/dicom+json Media Types may
   have a Transfer Syntax parameter in order to specify the encoding of
   base64 data.

All DICOM Media Types may have a character set parameter, but its usage
may be constrained by the service for which they are used.

.. _sect_8.7.3.5.1:

DICOM Multipart Media Types
'''''''''''''''''''''''''''

The syntax of multipart media types is:

::

   dcm-multipart = "multipart/related"

::

                   OWS ";" OWS "type" "=" dcm-mp-mt-name

::

                   OWS ";" OWS "boundary=" boundary

::

                   [dcm-parameters]

::

                   [related-parameters]

Where

::

   dcm-mp-mt-name = dicom / dicom-xml / dicom-json / octet-stream

See `Multipart Payload Syntax <#sect_8.6.1.2.1>`__ for the definition of
boundary and related-parameters.

Each multipart media type shall include a "type" parameter that defines
the media type of the parts and shall also include a "boundary"
parameter that specifies the boundary string that is used to separate
the parts.

.. _sect_8.7.3.5.2:

Transfer Syntax Parameter
'''''''''''''''''''''''''

For a given DICOM Media Type, a single Transfer Syntax parameter value
may be specified, but its usage may be constrained by the service for
which they are used.

RESTful origin servers shall support the Transfer Syntax parameter.

Transfer syntax media type parameters are forbidden in URI Service
requests and responses.

The syntax is:

::

   transfer-syntax-mtp = OWS ";" OWS %s"transfer-syntax=" ts-value

::

   ts-value            = transfer-syntax-uid / "*"

::

   transfer-syntax-uid ; a UID from  with a UID Type of Transfer Syntax

The value of the Transfer Syntax parameter may be either a Transfer
Syntax UID or the token "*".

For example, to specify that 1.2.840.10008.1.2.4.50 is the acceptable
Transfer Syntaxes, an Accept header field could be:

::

   Accept: application/dicom; transfer-syntax=1.2.840.10008.1.2.4.50

A DICOM Media Type may only have one Transfer Syntax parameter and it
shall have only one value.

.. note::

   Per `biblioentry_title <#biblio_RFC_6838>`__ Media Type
   Specifications and Registration Procedures, it is an error for a
   specific parameter to be specified more than once. If a choice of
   Transfer Syntaxes is acceptable. more than one media type may be
   provided in the Accept header with different q parameter values to
   indicate preference. E.g., to specify that 1.2.840.10008.1.2.4.50 and
   to specify that 1.2.840.10008.1.2.4.57 are acceptable but
   1.2.840.10008.1.2.4.50 is preferred, an Accept header field could be:

   ::

      Accept: multipart/related; type="application/dicom";transfer-syntax=1.2.840.10008.1.2.4.50;boundary=**, multipart/related; type="application/dicom";transfer-syntax=1.2.840.10008.1.2.4.57;q=0.5;boundary=**

The wildcard value "*" indicates that the user agent will accept any
Transfer Syntax. This allows, for example, the origin server to respond
without needing to transcode an existing representation to a new
Transfer Syntax, or to respond with the Explicit VR Little Endian
Transfer Syntax regardless of the Transfer Syntax stored, unless the
origin server has only access to the pixel data in lossy compressed form
or the pixel data in a lossless compressed form that is of such length
that it cannot be encoded in the Explicit VR Little Endian Transfer
Syntax.

If an Origin server supports the Transfer Syntax parameter, it shall
support the wildcard value.

Origin servers that support the Transfer Syntax parameter shall specify
in their Conformance Statement those values of Transfer Syntax parameter
that are supported in the response.

User agents that support the Transfer Syntax parameter shall specify in
their Conformance Statement those Transfer Syntax parameter values that
may be supplied in the request.

.. _sect_8.7.3.5.3:

Character Set Parameter
'''''''''''''''''''''''

All DICOM Media Types may have a single Character Set parameter, which
shall have only a single value, that specifies the Acceptable Character
Set for the response.

The syntax is:

::

   charset-mtp = OWS ";" OWS %s"charset" "=" charset

All DICOM Media Types have a Default Character Set of UTF-8. See
`Character Sets <#sect_8.8>`__ for character set details.

.. _sect_8.7.3.6:

Transfer Syntax Query Parameter
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

The Transfer Syntax Query Parameter specifies a comma-separated list of
one or more Transfer Syntax UIDs, as defined in .

The syntax is:

::

   transfer-syntax-qp = %s"transferSyntax" "=" (1#transfer-syntax-uid / "*")

This Query Parameter is only used by the URI Service.

RESTful services specify the Transfer Syntax in the "accept" Query
Parameter (see `Accept Query Parameter <#sect_8.3.3.1>`__) and do not
use Transfer Syntax Query Parameter.

.. _sect_8.7.3.7:

Acceptable Transfer Syntaxes
^^^^^^^^^^^^^^^^^^^^^^^^^^^^

Each DICOM Media Type in the Acceptable Media Types has an Acceptable
Transfer Syntax, which is explicitly specified or has a default value.

Depending on the service, the Acceptable Transfer Syntax for a DICOM
Media Type can be specified in the:

1. Transfer Syntax media type parameter contained in the Accept Query
   Parameter (see `Accept Query Parameter <#sect_8.3.3.1>`__)

2. Transfer Syntax media type parameter contained in the Accept header
   field

3. Transfer Syntax Query Parameter (see `DICOM Media Type
   Syntax <#sect_8.7.3.5>`__)

.. _sect_8.7.4:

Rendered Media Types
~~~~~~~~~~~~~~~~~~~~

DICOM Instances may be converted by a rendering process into non-DICOM
Media Types. This can be useful to display or process them using
non-DICOM software, such as browsers.

For example, an Instance containing:

1. an image could be rendered into the image/jpeg or image/png Rendered
   Media Types.

2. a multi-frame image in a lossless Transfer Syntax could be rendered
   into a video/mpeg or video/mp4 Rendered Media Type.

3. a Structured Report could be rendered into a text/html, text/plain,
   or application/pdf Rendered Media Type.

.. note::

   Rendered Media Types are usually consumer format media types. Some of
   the same non-DICOM Media Types are also used as Bulkdata Media Types,
   that is, for encoding Bulkdata extracted from Encapsulated Pixel Data
   (used with compressed Transfer Syntaxes), without applying a
   rendering process. See `DICOM Bulkdata Media
   Types <#sect_8.7.3.3>`__.

Rendered images shall contain no more than 8 bits per channel.

Origin servers shall support rendering Instances of different Resource
Categories into Rendered Media Types as specified in
`table_title <#table_8.7.4-1>`__.

.. table:: Rendered Media Types by Resource Category

   ================== ========== === =======
   Category           Media Type URI RESTful
   ================== ========== === =======
   Single Frame Image image/jpeg D   D
   image/gif          O          R   
   image/png          O          R   
   image/jp2          O          O   
   Multi-frame Image  image/gif  O   O
   Video              video/mpeg O   O
   video/mp4          O          O   
   video/H265         O          O   
   Text               text/html  D   D
   text/plain         R          R   
   text/xml           O          R   
   text/rtf           O          O   
   application/pdf    O          O   
   ================== ========== === =======

When an image/jpeg media type is returned, the image shall be encoded
using the JPEG baseline lossy 8-bit Huffman encoded non-hierarchical
non-sequential process defined in
`biblioentry_title <#biblio_ISOIEC10918-1>`__.

The origin server may support additional Rendered Media Types, which
shall be documented in the Conformance Statement and, if the service
supports it, the Retrieve Capabilities response.

A Transfer Syntax media type parameter is not permitted for Rendered
Media Types.

.. _sect_8.7.5:

Acceptable Media Types
~~~~~~~~~~~~~~~~~~~~~~

The term Acceptable Media Types denotes the media types that are
acceptable to the user agent in the response. The Acceptable Media Types
are those specified in:

-  The Accept Query Parameter, which may or may not be present.

-  The Accept header field, which shall be present.

The response to a request without an Accept header field shall be 406
(Not Acceptable). The presence of an Accept Query Parameter does not
eliminate the need for an Accept header field. For details see `Accept
Query Parameter <#sect_8.3.3.1>`__.

The Acceptable Media Types shall be either DICOM media-types or Rendered
media types, but not both. If the Acceptable Media Types contains both
DICOM and Rendered Media Types, the origin server shall return 400 (Bad
Request).

The user agent may specify the relative degree of preference for media
types, whether in the Accept Query Parameter or the Accept header field,
using the weight parameter. See `biblioentry_title <#biblio_RFC_7231>`__
`Section 5.3.1 <http://tools.ietf.org/html/rfc7231#section-5.3.1>`__.

::

   weight = OWS ";" OWS "q=" qvalue

::

   qvalue = ("0" ["." 0*3DIGIT]) / ("1" ["." 0*3("0") ])

If no "q" parameter is present, the default qvalue is 1.

.. _sect_8.7.6:

Accept Query Parameter
~~~~~~~~~~~~~~~~~~~~~~

The Accept Query Parameter can be used to specify Acceptable Media
Types. See `Acceptable Media Types <#sect_8.7.5>`__.

.. _sect_8.7.7:

Accept Header Field
~~~~~~~~~~~~~~~~~~~

The Accept header field is used to specify media types acceptable to the
user agent. It has the following syntax:

::

   Accept = 1#(media-range [weight])

The Accept header field value shall be a comma-separated list of one or
more media ranges acceptable in the response. See
`biblioentry_title <#biblio_RFC_7231>`__ `Section
5.3.2 <http://tools.ietf.org/html/rfc7231#section-5.3.2>`__.

A media range is either a media-type or a wildcard. Wildcards use the
asterisk ("*") to group media types into ranges, with <type>/\*
indicating all subtypes of that type, and \*/\* indicating all media
types. For example, the media range image/\* matches image/jpeg, which
is the default media type for the Single Frame Image Resource Category,
and text/\* matches text/html, which is the default media type for the
Text Resource Category. DICOM specifies that the \*/\* media range
matches the default media type for the target's Resource Category. If no
default media type is defined for a Resource Category, then any media
type from the Resource Category is acceptable.

If the response might contain a payload, an Accept header field shall be
present in the request.

If the origin server receives a request without an Accept header field,
but that might have a response payload, it shall return a 406 (Not
Acceptable).

Any Accept header field values, including media type parameters, that
are not valid or not supported shall be ignored by the origin server.

.. _sect_8.7.8:

Selected Media Type and Transfer Syntax
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

The selection of the media type and transfer syntax by the origin server
are interrelated.

.. _sect_8.7.8.1:

Selected Media Type
^^^^^^^^^^^^^^^^^^^

The Selected Media Type is the media type selected by the origin server
for the response payload. The media types in the Accept Query Parameter
and the media ranges in the Accept header field shall each be separately
prioritized according to the rules defined in
`biblioentry_title <#biblio_RFC_7231>`__ `Section
5.3.1 <http://tools.ietf.org/html/rfc7231#section-5.3.1>`__.

For multipart payloads, the Selected Media Type is determined
independently for each message part in the response.

.. note::

   The Selected Media Type of each message part depends on the Resource
   Category of the Instance and the Acceptable Media Types for that
   Resource Category.

The Selected Media Type of each message part depends on the Resource
Category of the Instance and the Acceptable Media Types for that
Resource Category.

The Selected Media Type is chosen as follows:

1. Identify the target's Resource Category

2. Select the representation with the highest priority supported media
   type for that category in the Accept Query Parameter.

3. If no media type in the Accept Query Parameter is supported, select
   the highest priority supported media type for that category in the
   Accept header field, if any.

4. Otherwise, select the default media type for the category, if the
   Accept header field contains a wildcard media range matching the
   category, if any.

5. Otherwise, return a 406 (Not Acceptable).

.. note::

   1. If the Selected Media Type is the Explicit VR Little Endian and
      the pixel data is compressed and when uncompressed is of such
      length that it cannot contained in a value field, then the origin
      server will respond with a 406 (Not Acceptable), and the user
      agent may try again with a different set of Acceptable Media
      Types.

   2. If transcoding to the Explicit VR Little Endian Transfer Syntax, a
      VR of UN may be needed for the encoding of Data Elements with
      explicit VR whose value length exceeds 65534 (2\ :sup:`16`-2)
      (FFFEH, the largest even length unsigned 16-bit number) but which
      are defined to have a 16-bit explicit VR length field. See .

For a set of media types in the Accept Query Parameter (step 2 above),
or for a set of media ranges in the Accept header field (step 3 above),
the highest priority supported media type is determined as follows:

1. Assign a qvalue of 1 to any member of the set that does not have a
   one.

2. Assign each representation supported by the origin server the qvalue
   of the most specific media type that it matches.

3. Select the representation with the highest qvalue. If there is a tie,
   the origin server shall determine which is returned.

For example, consider an origin server which receives a request with the
following Accept header field:

::

   Accept: text/*; q=0.5, text/html; q=0.4, text/html; level=1, text/html; level=2; q=0.7,

::

           image/png, */*; q=0.4

Suppose that for the resource indicated in the request, the origin
server supports representations for the following media types:

::

   text/html (regular, level 1 and level 2)

::

   text/rtf

::

   text/plain

::

   text/x-latex

These media types are assigned the following qvalues, based on the media
ranges above:

.. table:: Media Type QValue Example

   ================== ====== =======================
   Media Type         qvalue Determining Media Range
   ================== ====== =======================
   text/html; level=1 1.0    text/html; level=1
   text/html; level=2 0.7    text/html; level=2
   text/plain         0.5    text/\*
   text/rtf           0.5    text/\*
   text/html          0.4    text/html
   text/x-latex       0.4    \*/\*
   ================== ====== =======================

Although "image/png" has been assigned a default qvalue of 1.0, it is
not among the supported media types for this resource, and thus is not
listed.

The selected media type is 'text/html; level=1' since it is the
supported media type in the Text Category with the highest qvalue.

.. _sect_8.7.8.2:

Selected Transfer Syntax
^^^^^^^^^^^^^^^^^^^^^^^^

The Selected Transfer Syntax is the Transfer Syntax selected by the
origin server to encode a single message part in the response.

The origin server shall first determine the Selected Media Type as
defined in `Selected Media Type and Transfer Syntax <#sect_8.7.8>`__ and
then determine the Selected Transfer Syntax.

If the Selected Media Type was contained in the Accept Query Parameter,
then the Selected Transfer Syntax is determined as follows:

1. Select the value of the Transfer Syntax parameter of the Selected
   Media Type, if any;

2. Otherwise, select the value of the Transfer Syntax in the Transfer
   Syntax Query Parameter, if any;

3. Otherwise select the default Transfer Syntax (see
   `table_title <#table_8.7.3-2>`__, `table_title <#table_8.7.3-4>`__ or
   `table_title <#table_8.7.3-5>`__) for the Selected Media Type.

If the Selected Media Type was contained in the Accept header field,
then the Selected Transfer Syntax is determined as follows:

1. Select the Transfer Syntax parameter for the Selected Media Type, if
   any;

2. Otherwise, select the default Transfer Syntax for the Selected Media
   Type.

.. note::

   1. The Selected Transfer Syntax may be different for each message
      part contained in a response.

   2. Implementers may use a different selection algorithm if the result
      is the same.

.. _sect_8.7.9:

Content-Type Header Field
~~~~~~~~~~~~~~~~~~~~~~~~~

The Content-Type header field specifies the media type of the payload.
It shall only be present when a payload is present, and any media type
parameters shall specify the encoding of the corresponding message part.

In particular, a DICOM Media Type used as the value of a Content-Type
header field shall have zero or one Transfer Syntax parameter (see
`Transfer Syntax Parameter <#sect_8.7.3.5.2>`__), and zero or one
charset parameter (see `Character Set Parameter <#sect_8.7.3.5.3>`__),
which corresponds to the character encoding of the corresponding message
part.

::

   Content-Type: dicom-media-type +transfer-syntax-mtp +charset-mtp

If there is a conflict between the Transfer Syntax specified in the
media type and the one specified in the File Meta Information Transfer
Syntax UID (0002,0010) Attribute, the latter has precedence.

.. _sect_8.8:

Character Sets
--------------

HTTP uses charset names to indicate or negotiate the character encoding
of textual content in representations
`biblioentry_title <#biblio_RFC_6365>`__ `Section
3.3 <http://tools.ietf.org/html/rfc6365#section-3.3>`__.

Character sets may be identified using the value in the IANA Preferred
MIME Name column in `biblioentry_title <#biblio_IANA_CharacterSets>`__.

Character sets may also be identified by using the DICOM Defined Terms
for the character set (see `IANA Character Set Mapping <#chapter_D>`__,
, and ), which shall be quoted strings since they contain the space ('
') character.

The syntax is:

::

   charset = token / defined-term / DQ defined-term DQ

Where

+-----------------+---------------------------------------------------+
| ::              | A case-insensitive charset name from the          |
|                 | Preferred MIME Name in the IANA Character Set     |
|    token        | Registry.                                         |
+-----------------+---------------------------------------------------+
| ::              | See .                                             |
|                 |                                                   |
|    defined-term |                                                   |
+-----------------+---------------------------------------------------+

The origin server shall support the "UTF-8" charset name for RESTful
Retrieve Rendered transaction but is not required to support the DICOM
Defined Term "ISO_IR 192". Some DICOM Defined Terms for character sets
contain space characters, and shall be enclosed in double quotes in HTTP
header fields and percent encoded in URIs.

The Conformance Statement shall document all supported character sets.
The Retrieve Capabilities response for all RESTful Services shall also
document all supported character sets.

A request without any Character Set Query Parameter or Accept-Charset
header field implies that the user agent will accept any character set
in the response.

`IANA Character Set Mapping <#chapter_D>`__ contains a mapping of some
Specific Character Set (0008,0005) Defined Terms to IANA charset tokens.

.. _sect_8.8.1:

Acceptable Character Sets
~~~~~~~~~~~~~~~~~~~~~~~~~

The term Acceptable Character Sets denotes the character sets that are
acceptable to the user agent in the response. The Acceptable Character
Sets are those specified in:

-  the "charset" media type parameter

-  the character set Query Parameter

-  the Accept-Charset header field

-  the default character set for the media type, if any

When Acceptable Character Sets contains a list of one or more Defined
Terms they should be ordered by the user agent as specified in , and .
This is especially important for ISO 2022 character sets.

Any charset values that are not valid or not supported shall be ignored
by the origin server.

.. _sect_8.8.2:

Character Set Query Parameter
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

See `Character Set Query Parameter <#sect_8.3.3.2>`__ .

.. _sect_8.8.3:

Character Set Media Type Parameters
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

DICOM Media Types accept character set (charset) parameters. See
`Character Set Parameter <#sect_8.7.3.5.3>`__.

Many other media types also accept character set (charset) parameters.
See `biblioentry_title <#biblio_IANA_MediaTypes>`__.

.. _sect_8.8.4:

Accept-charset Header Field
~~~~~~~~~~~~~~~~~~~~~~~~~~~

The Accept-Charset header field has the following syntax:

::

   Accept-Charset = 1#(charset [weight]) / ("*" [weight])

The user agent may provide a list of Acceptable Character Sets in the
Accept-Charset header field of the request. Its value is a
comma-separated list of one or more charsets and/or the wildcard value
("*").

The values of the Accept-Charset header field values are prioritized by
their weight parameter.

If no wildcard ("*") is present, then any character sets not explicitly
mentioned in the header field are considered "not acceptable" to the
client.

A request without an Accept-Charset header field implies that the user
agent will accept any charset in response.

If the media type defines a "charset" parameter, it should be included
with the media type in the Accept header field, rather than in the
Accept-Charset header field.

If this header field has a value that is not a valid or supported
character set, the origin server shall return a 400 (Bad Request)
response and may include a payload containing an appropriate Status
Report. See `Status Report <#sect_8.6.3>`__.

Any Accept-Charset header field values that are not valid or not
supported shall be ignored.

.. _sect_8.8.5:

Selected Character Set
~~~~~~~~~~~~~~~~~~~~~~

The origin server shall determine the Selected Character Set(s) as
follows:

1. Select the first supported character set in the "charset"
   parameter(s) of the Selected Media Type.

2. Otherwise, select the highest priority supported charset in the
   character-set Query Parameter.

3. Otherwise, select the highest priority supported charset in the
   Accept-Charset header field.

4. Otherwise, if the Selected Media Type has a default character set
   that is supported, select it.

5. Otherwise, select UTF-8.

Rendered representations returned in the response shall have all
contained strings returned in the Selected Character Sets.

If the character set in which the Target Resource is encoded is not the
Selected CharacterSet:

-  If the origin server supports transcoding all glyphs used in the
   Target Resource into theSelected Character Set, it shall transcode
   the response payload into the Selected Character Set

-  Otherwise, the origin server shall return 406 (Not Acceptable).

.. note::

   This means that some Instances may be convertible, and others will
   not be, even though they have the same Specific Character Set
   (0008,0005).

If the user agent chooses to perform its own conversion rather than have
it done by the origin server:

1. The user agent may omit the Accept-Charset header field or send
   the"*"wildcard

2. The user agent may transcode the character set replacing all unknown
   characters with a suitable replacement. For example:

   -  A question mark ("?"), or other similar character indicating an
      unknown character.

   -  The corresponding Unicode Code Point for the character,
      represented as "U+xxxx".

   -  The four characters "\nnn", where "nnn" is the 3-digit octal
      representation of each byte (see ).

.. _sect_8.9:

Retrieve Capabilities Transaction
---------------------------------

This transaction retrieves a Capabilities Description (see `Capabilities
Description <#chapter_H>`__), which is a machine-readable description of
the service(s) implemented by an origin server. All RESTful services
defined by this Part of the Standard shall implement this transaction.

The Target Resource for this transaction is an origin server. The
response contains a Capabilities Description, which describes the
transactions, resources, representations, etc. that are supported by the
service(s).

.. _sect_8.9.1:

Request
~~~~~~~

The request shall have the following syntax:

::

   OPTIONS SP / SP version CRLF

::

   Accept: 1#media-type CRLF

::

   *(header-field CRLF)

::

   CRLF

.. _sect_8.9.1.1:

Resource
^^^^^^^^

The Target Resource for this transaction is the Base URI ("/") for the
Service. See `Target Resources <#sect_8.2>`__.

.. _sect_8.9.1.2:

Query Parameters
^^^^^^^^^^^^^^^^

This transaction has no Query Parameters.

.. _sect_8.9.1.3:

Request Header Fields
^^^^^^^^^^^^^^^^^^^^^

.. table:: Request Header Fields

   +---------------+------------+-------+-------------+---------------+
   | Name          | Value      | Usage | Description |               |
   +===============+============+=======+=============+===============+
   | Accept        | media-type | M     | M           | The           |
   |               |            |       |             | Acceptable    |
   |               |            |       |             | Media Types   |
   |               |            |       |             | for the       |
   |               |            |       |             | response      |
   |               |            |       |             | payload       |
   +---------------+------------+-------+-------------+---------------+
   | A             | charset    | O     | O           | The           |
   | ccept-Charset |            |       |             | Acceptable    |
   |               |            |       |             | Character     |
   |               |            |       |             | Sets of the   |
   |               |            |       |             | response      |
   |               |            |       |             | payload       |
   +---------------+------------+-------+-------------+---------------+

See also `Header Fields <#sect_8.4>`__.

.. _sect_8.9.1.4:

Request Payload
^^^^^^^^^^^^^^^

The request has no payload.

.. _sect_8.9.2:

Behavior
~~~~~~~~

The origin server shall return a Capabilities Description, as defined in
`Capabilities Description <#chapter_H>`__, in an Acceptable Media Type.

.. _sect_8.9.3:

Response
~~~~~~~~

The format of the response is as follows:

::

   version SP status-code SP reason-phrase CRLF

::

   [Content-Type: media-type CRLF]

::

   [(Content-Length: uint) / (Content-Encoding: encoding) CRLF]

::

   *(header-field CRLF)

::

   CRLF

::

   [payload / status-report]

.. _sect_8.9.3.1:

Status Codes
^^^^^^^^^^^^

`table_title <#table_8.9.3-1>`__ shows some common status codes
corresponding to this transaction. See also `Status Codes <#sect_8.5>`__
for additional status codes.

.. table:: Status Code Meaning

   +--------------------+-----------------------+-----------------------+
   | Status             | Code                  | Meaning               |
   +====================+=======================+=======================+
   | Success            | 200 (OK)              | All Instances were    |
   |                    |                       | successfully          |
   |                    |                       | retrieved.            |
   +--------------------+-----------------------+-----------------------+
   | 304 (Not Modified) | The user agent's      |                       |
   |                    | current               |                       |
   |                    | representation is up  |                       |
   |                    | to date, so no        |                       |
   |                    | payload was returned. |                       |
   |                    | This status code      |                       |
   |                    | shall only be         |                       |
   |                    | returned for a        |                       |
   |                    | conditional request   |                       |
   |                    | containing an         |                       |
   |                    | If-None-Match header  |                       |
   |                    | field.                |                       |
   +--------------------+-----------------------+-----------------------+
   | Failure            | 400 (Bad Request)     | There was a problem   |
   |                    |                       | with the request.     |
   +--------------------+-----------------------+-----------------------+

.. _sect_8.9.3.1.1:

Response Header Fields
''''''''''''''''''''''

.. table:: Response Header Fields

   +----------------+----------------+----------------+----------------+
   | Name           | Value          | Origin Server  | Description    |
   |                |                | Usage          |                |
   +================+================+================+================+
   | Content-Type   | di             | M              | The media-type |
   |                | com-media-type |                | of the payload |
   +----------------+----------------+----------------+----------------+
   | Content-Length | uint           | C              | Shall be       |
   |                |                |                | present if a   |
   |                |                |                | content        |
   |                |                |                | encoding has   |
   |                |                |                | not been       |
   |                |                |                | applied to the |
   |                |                |                | payload        |
   +----------------+----------------+----------------+----------------+
   | Co             | encoding       | C              | Shall be       |
   | ntent-Encoding |                |                | present if a   |
   |                |                |                | content        |
   |                |                |                | encoding has   |
   |                |                |                | been applied   |
   |                |                |                | to the payload |
   +----------------+----------------+----------------+----------------+

See also `Header Fields <#sect_8.4>`__.

.. _sect_8.9.3.2:

Response Payload
^^^^^^^^^^^^^^^^

A success response shall have a payload containing a Capabilities
Description in the Selected Media Type. The Capabilities Description
shall conform to the requirements and structure defined in `Capabilities
Description <#chapter_H>`__.

A failure response payload may contain a Status Report describing any
failures, warnings, or other useful information.

.. _sect_8.9.4:

Media Types
~~~~~~~~~~~

The media types supported by the Retrieve Capabilities service are
application/vnd.sun.wadl+xml (Web Application Description Language) or
application/json.

.. _sect_8.10:

Notifications
-------------

.. _sect_8.10.1:

Overview
~~~~~~~~

Some RESTful Services support Notifications.

.. _sect_8.10.2:

Conformance
~~~~~~~~~~~

An implementation shall document whether or not it supports
notifications in the Conformance Statement. If the service supports
notification it shall describe how WebSocket connections are opened.

.. _sect_8.10.3:

Transaction Overview
~~~~~~~~~~~~~~~~~~~~

Any service that supports Notifications shall support the following
transactions:

.. table:: Notification Sub-System Transactions

   +-----------------------------+--------+-----------------------------+
   | Name                        | Method | Description                 |
   +=============================+========+=============================+
   | Open Notification           | GET    | The user agent requests     |
   | Connection                  |        | that the origin server      |
   |                             |        | create a Notification       |
   |                             |        | Connection between them.    |
   +-----------------------------+--------+-----------------------------+
   | Send Event Report           | N/A    | The origin server sends an  |
   |                             |        | Event Report to an          |
   |                             |        | End-Point                   |
   +-----------------------------+--------+-----------------------------+

.. _sect_8.10.4:

Open Notification Connection Transaction
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

This transaction creates a connection between the user agent and the
origin server over which the origin server can send Event Reports to the
user agent.

.. note::

   An origin server might play the role of a user agent when
   communicating with another origin-server.

The connection uses the WebSocket protocol. The connection can use the
same TCP port as the HTTP connection, but they are separate connections.

See `biblioentry_title <#biblio_RFC_6455>`__ for details of the
WebSocket protocol.

.. _sect_8.10.4.1:

Request
^^^^^^^

There is more than one way to establish a WebSocket connection. An
origin server that conforms to `biblioentry_title <#biblio_RFC_6455>`__
will at least support requests to open a WebSocket over an HTTP
connection that have the following syntax:

::

   GET SP / SP version CRLF

::

   Host: host CRLF

::

   Upgrade: "WebSocket" CRLF

::

   Connection: "Upgrade" CRLF

::

   Origin: url CRLF

::

   Sec-WebSocket-Key: nonce CRLF

::

   Sec-WebSocket-Protocol: protocols CRLF

::

   Sec-WebSocket-Version: "13" CRLF

::

   *(<header-field> CRLF)

::

   CRLF

The origin server may support other methods of opening a WebSocket
connection, which should be included in the Conformance Statement and
the Retrieve Capabilities response.

.. _sect_8.10.4.1.1:

Target Resources
''''''''''''''''

The Target Resource is an origin server implementing a DICOM RESTful
Service.

.. _sect_8.10.4.1.2:

Query Parameters
''''''''''''''''

This transaction has no query parameters.

.. _sect_8.10.4.1.3:

Request Header Fields
'''''''''''''''''''''

`table_title <#table_8.10.4-1>`__ shows the Request Header Field usage
for opening a WebSocket connection over http/https.

.. table:: Request Header Fields

   ====================== =========== =====
   Name                   Value       Usage
   ====================== =========== =====
   Content-Type           media-type  M
   Upgrade                "WebSocket" M
   Connection             "Upgrade"   M
   Origin                 url         M
   Sec-WebSocket-Key      accept-key  M
   Sec-WebSocket-Protocol protocols   O
   Sec-WebSocket-Version  version     M
   ====================== =========== =====

For details of the request header field values and other methods of
opening a WebSocket connection see
`biblioentry_title <#biblio_RFC_6455>`__.

.. _sect_8.10.4.1.4:

Request Payload
'''''''''''''''

The request has no payload.

.. _sect_8.10.4.2:

Behavior
^^^^^^^^

When the origin server receives this request, it shall open and maintain
a WebSocket connection between itself and the user agent.

If the connection is lost at any point, the user agent can re-establish
it by repeating this transaction.

.. _sect_8.10.4.3:

Response
^^^^^^^^

The response shall have the following syntax:

::

   version SP status-code SP reason-phrase CRLF

::

   Upgrade: "WebSocket" CRLF

::

   Connection: "Upgrade" CRLF

::

   Sec-WebSocket-Accept: response-key CRLF

::

   Sec-WebSocket-Protocol: protocol CRLF

::

   *(header-field CRLF)

::

   CRLF

.. _sect_8.10.4.3.1:

Status Codes
''''''''''''

`table_title <#table_8.10.4-2>`__ shows some common status codes
corresponding to this transaction. See also `Status Codes <#sect_8.5>`__
for additional status codes.

.. table:: Status Code Meaning

   +---------+---------------------------+----------------------------+
   | Status  | Code                      | Meaning                    |
   +=========+===========================+============================+
   | Success | 101 (Switching Protocols) | The protocol was           |
   |         |                           | successfully changed to    |
   |         |                           | WebSocket.                 |
   +---------+---------------------------+----------------------------+
   | Failure | 400 (Bad Request)         | There was a problem with   |
   |         |                           | the request.               |
   +---------+---------------------------+----------------------------+

.. _sect_8.10.4.3.2:

Response Header Fields
''''''''''''''''''''''

.. table:: Response Header Fields

   +----------------+--------------+----------------+----------------+
   | Name           | Value        | Origin Server  | Description    |
   |                |              | Usage          |                |
   +================+==============+================+================+
   | Upgrade        | "WebSocket"  | M              |                |
   +----------------+--------------+----------------+----------------+
   | Connection     | "Upgrade"    | M              |                |
   +----------------+--------------+----------------+----------------+
   | Origin         | url          | M              |                |
   +----------------+--------------+----------------+----------------+
   | Sec-We         | response-key | M              | See            |
   | bSocket-Accept |              |                | `biblioentry   |
   |                |              |                | _title <#bibli |
   |                |              |                | o_RFC_6455>`__ |
   +----------------+--------------+----------------+----------------+
   | Sec-WebS       | protocol     | M              | See            |
   | ocket-Protocol |              |                | `biblioentry   |
   |                |              |                | _title <#bibli |
   |                |              |                | o_RFC_6455>`__ |
   +----------------+--------------+----------------+----------------+

See also `Header Fields <#sect_8.4>`__.

.. _sect_8.10.4.3.3:

Response Payload
''''''''''''''''

The response has no payload.

.. _sect_8.10.5:

Send Event Report Transaction
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

The origin server uses this transaction to notify a user agent of
Events.

This transaction sends a notification, containing an Event Report, over
an established Notification Connection from an origin server to a user
agent. Unlike most transactions, this transaction is initiated by the
origin server.

This transaction corresponds to a DIMSE N-EVENT-REPORT action.

Each service may define Events, and the corresponding Event Report
messages and their contents, related to its resources.

.. _sect_8.10.5.1:

Request
^^^^^^^

The request shall use the WebSocket Data Frame transmission protocol.

.. _sect_8.10.5.1.1:

Request Payload
'''''''''''''''

The data frames shall have an opcode of "%x1" (text).

The data frame payload data shall be a DICOM JSON Dataset containing the
Attributes of the Event Report.

.. note::

   1. The WebSocket protocol does not currently allow content
      negotiation so it is not possible to support both XML and JSON
      encoding of Event Report messages.

   2. If the Event Reports are being proxied into DIMSE N-EVENT Reports,
      a Message ID (0000,0110) must be managed by the proxy.

.. _sect_8.10.5.2:

Behavior
^^^^^^^^

The user agent shall accept all Attributes included in any Event Report.
No requirements are placed on what the user agent does with this
information.

.. _sect_8.10.5.3:

Response
^^^^^^^^

None.

.. _sect_8.11:

Security and Privacy
--------------------

It is very likely that DICOM objects contain Protected Health
Information. Privacy regulations in the United States (HIPAA), Europe
(GDPR), and elsewhere, require that Individually Identifiable
Information be kept private. It is the responsibility of those
implementing and deploying the DICOM Standard to ensure that applicable
regulations for security and privacy are satisfied.

See, for example,
`biblioentry_title <#biblio_ONC_PrivacySecurityGuide>`__.

The DICOM PS3.10 File Format has security considerations that will apply
whenever DICOM PS3.10 File format is used. See .

