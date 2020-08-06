.. _chapter_9:

URI Service
===========

.. _sect_9.1:

Overview
--------

The URI Service, also known as WADO-URI, enables a user agent to
retrieve representations of Instances using HTTP.

.. _sect_9.1.1:

Resource Descriptions
~~~~~~~~~~~~~~~~~~~~~

The URI Service does not define resources in the form of a Target
Resource Path, such as {/resource}. The Target URI of each transaction
is a reference to the Base URI ("/") and the Target Resource is
identified using query parameter values. The resources for the URI
Service are instances of Composite Storage SOP Classes defined in .

.. _sect_9.1.2:

Common Query Parameters
~~~~~~~~~~~~~~~~~~~~~~~

The Query Parameters specified in this Section may be used with either
the Retrieve DICOM Instance or Retrieve Rendered Instance transactions,
and are applicable to all supported SOP Classes.

.. _sect_9.1.2.1:

Mandatory Query Parameters
^^^^^^^^^^^^^^^^^^^^^^^^^^

The origin server shall support Query Parameters as required in
`table_title <#table_9.1.2-1>`__.

The user agent shall supply in the request Query Parameters as required
in `table_title <#table_9.1.2-1>`__.

The Query Parameters may appear in any order.

.. table:: Mandatory Query Parameters

   =========== ====== ===== ======= ==================================
   Name        Values Usage Section 
   =========== ====== ===== ======= ==================================
   requestType "WADO" M     M       `Request Type <#sect_9.1.2.1.1>`__
   studyUID    uid    M     M       `Series UID <#sect_9.1.2.1.3>`__
   seriesUID   uid    M     M       `Series UID <#sect_9.1.2.1.3>`__
   objectUID   uid    M     M       `Instance UID <#sect_9.1.2.1.4>`__
   =========== ====== ===== ======= ==================================

See `Query Parameters <#sect_8.3>`__.

.. note::

   To identify a SOP Instance, only a SOP Instance UID is required,
   because any UID is globally unique. However, the Standard requires
   that the UIDs of the higher levels in the DICOM Information Model
   (i.e., series and study) are specified, in order to support the use
   of DICOM devices that support only the baseline hierarchical (rather
   than extended relational) Query/Retrieve model, which requires the
   Study Instance UID and Series Instance UID to be defined when
   retrieving an Instance, as defined in .

.. _sect_9.1.2.1.1:

Request Type
''''''''''''

::

   requestType = %s"requestType=" token

::

   token       = "WADO"

This parameter specifies that this is a URI service request. The
parameter name shall be "requestType", and the value shall be "WADO".

If the value is other than "WADO", and the origin server does not
support the value, the response shall be 400 (Bad Request), and may
include a payload containing an appropriate error message.

.. _sect_9.1.2.1.2:

Study UID
'''''''''

::

   study = %s"studyUID=" uid

The value of this parameter is a Study Instance UID.

.. _sect_9.1.2.1.3:

Series UID
''''''''''

::

   series = %s"seriesUID=" uid

The value of this parameter is a Series Instance UID.

.. _sect_9.1.2.1.4:

Instance UID
''''''''''''

::

   instance = %s"objectUID=" uid

The value of this parameter is a SOP Instance UID.

.. _sect_9.1.2.2:

Optional Query Parameters
^^^^^^^^^^^^^^^^^^^^^^^^^

The parameters defined in this section are optional for all URI
requests.

.. table:: Optional Query Parameters

   +-------------+------------+-------+---------+------------------+
   | Key         | Values     | Usage | Section |                  |
   +=============+============+=======+=========+==================+
   | contentType | media-type | O     | O       | `Accept Query    |
   |             |            |       |         | Parameter <#     |
   |             |            |       |         | sect_8.3.3.1>`__ |
   +-------------+------------+-------+---------+------------------+
   | charset     | token      | O     | O       | `Character Set   |
   |             |            |       |         | Query            |
   |             |            |       |         | Parameter <#     |
   |             |            |       |         | sect_8.3.3.2>`__ |
   +-------------+------------+-------+---------+------------------+

See `Query Parameters <#sect_8.3>`__.

.. _sect_9.1.2.2.1:

Acceptable Media Types
''''''''''''''''''''''

The Accept Query Parameter specifies the Acceptable Media Types for the
response payload. See `Acceptable Media Types <#sect_8.7.5>`__. The
case-sensitive name of the parameter is "contentType". Its syntax is:

::

   accept = %s"contentType=" dicom / 1#rendered-media-type

The value of this parameter, if present, shall be either
application/dicom, or one or more of the Rendered Media Types.

The DICOM Media Type transfer-syntax and character set parameters are
forbidden in the request. If either are present, the response shall be
400 (Bad Request), and may include a payload containing an appropriate
error message.

See `Acceptable Media Types <#sect_8.7.5>`__ for other errors related to
this parameter.

.. note::

   URI origin servers may support Transfer Syntax and charset Query
   Parameters. This is different from the approach used by the DICOM
   RESTful services, which uses transfer-syntax and charset media type
   parameters.

.. _sect_9.1.2.2.2:

Acceptable Character Sets
'''''''''''''''''''''''''

::

   charset-qp = %s"charset=" 1#(charset [weight])

The value of this parameter is a comma-separated list of one or more
character-set identifiers. See `Acceptable Character
Sets <#sect_8.8.1>`__.

.. _sect_9.1.3:

Common Media Types
~~~~~~~~~~~~~~~~~~

The origin server shall support the application/dicom media type as
described in `The application/dicom Media Type <#sect_8.7.3.1>`__ and
Rendered Media Types as described in `Rendered Media
Types <#sect_8.7.4>`__.

Support for the Transfer Syntax and Character Set media type parameters
is forbidden for URI Services.

.. _sect_9.2:

Conformance
-----------

An implementation conforming to the URI service shall support retrieval
of one or more of the Information Objects specified for the Storage
Service Class, as specified in .

An implementation's Conformance Statement shall document the Information
Objects supported for the URI service, and whether it plays the role of
origin server or user agent, or both.

.. _sect_9.3:

Transactions Overview
---------------------

The URI Service has two transactions:

Retrieve DICOM Instance
   This transaction retrieves a single Instance in the application/dicom
   media type.

Retrieve Rendered Instance
   This transaction retrieves a single Instance in a Rendered Media
   Type.

These two transactions have the same "requestType" type but are
differentiated by their Selected Media Type.

If there is no "contentType" Query Parameter and the Accept header field
is '*/*', then the Selected Media Type defaults to 'image/jpeg' media
type and the transaction defaults to Retrieve Rendered Instance.

.. _sect_9.4:

Retrieve DICOM Instance Transaction
-----------------------------------

This transaction retrieves a single Instance in the application/dicom
media type. See `DICOM Media Types and Media Types For
Bulkdata <#sect_8.7.3>`__.

.. _sect_9.4.1:

Request
~~~~~~~

The request shall have the following syntax:

::

   GET SP / ?{requestType}&{study}&{series}&{instance}

::

            {&accept}

::

            {&charset}

::

            {&anonymize}

::

            {&transferSyntax}

::

            SP HTTP/1.1 CRLF

::

   Accept: uri-media-type CRLF

::

   *(header-field CRLF)

::

   CRLF

.. _sect_9.4.1.1:

Target Resource
^^^^^^^^^^^^^^^

The Target Resource shall be an Instance of a Composite Storage SOP
class defined in .

.. _sect_9.4.1.2:

Query Parameters
^^^^^^^^^^^^^^^^

The origin server shall support Query Parameters as required in
`table_title <#table_9.4.1-1>`__ .

The user agent shall supply in the request Query Parameters as required
in `table_title <#table_9.4.1-1>`__ .

.. table:: Optional Query Parameters

   +----------------+-------------+-------+---------+----------------+
   | Key            | Values      | Usage | Section |                |
   +================+=============+=======+=========+================+
   | anonymize      | "yes"       | O     | O       | `An            |
   |                |             |       |         | onymize <#sect |
   |                |             |       |         | _9.4.1.2.1>`__ |
   +----------------+-------------+-------+---------+----------------+
   | annotation     | "patient"   | O     | O       | `Ann           |
   |                |             |       |         | otation <#sect |
   |                | "technique" |       |         | _9.4.1.2.2>`__ |
   +----------------+-------------+-------+---------+----------------+
   | transferSyntax | uid         | O     | O       | `Transfer      |
   |                |             |       |         | Syntax <#sect  |
   |                |             |       |         | _9.4.1.2.3>`__ |
   +----------------+-------------+-------+---------+----------------+

.. _sect_9.4.1.2.1:

Anonymize
'''''''''

::

   anonymize = %s"anonymize=" token

::

   token = "yes"

This parameter specifies that the returned representations shall have
all Individually Identifiable Information (III) removed, as defined in
Basic Profile with Clean Pixel Data Option. Its name is "anonymize" and
its value is a token. The defined token is "yes". If this parameter is
not present, no anonymization is requested.

.. _sect_9.4.1.2.2:

Annotation
''''''''''

::

   annotation = 1#( %s"patient" / %s"technique" )

This parameter specifies that the rendered images shall be annotated
with patient and/or procedure information. Its value is a
comma-separated list of one or more keywords.

Where

+----------------+----------------------------------------------------+
| ::             | indicates that the rendered images shall be        |
|                | annotated with patient information (e.g., patient  |
|    "patient"   | name, birth date, etc.).                           |
+----------------+----------------------------------------------------+
| ::             | indicates that the rendered images shall be        |
|                | annotated with information about the procedure     |
|    "technique" | that was performed (e.g., image number, study      |
|                | date, image position, etc.).                       |
+----------------+----------------------------------------------------+

The origin server may support additional keywords, which should be
included in the Conformance Statement and the Retrieve Capabilities
response.

.. _sect_9.4.1.2.3:

Transfer Syntax
'''''''''''''''

::

   transfer-syntax = %s"transferSyntax" "=" transfer-syntax-uid

This parameter specifies a Transfer Syntax UID. Its name is
"transferSyntax" and its value is a single Transfer Syntax UID. It is
optional for both the user agent and origin server. See `DICOM Media
Type Syntax <#sect_8.7.3.5>`__ for details.

.. _sect_9.4.1.3:

Request Header Fields
^^^^^^^^^^^^^^^^^^^^^

The origin server shall support header fields as required in
`table_title <#table_9.4.1-2>`__ in the request.

The user agent shall supply in the request header fields as required in
`table_title <#table_9.4.1-2>`__.

.. table:: Request Header Fields

   +---------------+------------+-------+-------------+---------------+
   | Name          | Values     | Usage | Description |               |
   +===============+============+=======+=============+===============+
   | Accept        | media-type | O     | M           | The           |
   |               |            |       |             | Acceptable    |
   |               |            |       |             | Media Types   |
   |               |            |       |             | for the       |
   |               |            |       |             | response      |
   |               |            |       |             | payload       |
   +---------------+------------+-------+-------------+---------------+
   | A             | charset    | O     | M           | The           |
   | ccept-Charset |            |       |             | Acceptable    |
   |               |            |       |             | Character     |
   |               |            |       |             | Sets of the   |
   |               |            |       |             | response      |
   |               |            |       |             | payload       |
   +---------------+------------+-------+-------------+---------------+

See also `Header Fields <#sect_8.4>`__.

.. _sect_9.4.1.4:

Request Payload
^^^^^^^^^^^^^^^

The request has no payload.

.. _sect_9.4.2:

Behavior
~~~~~~~~

A success response shall contain the Target Resource in an Acceptable
DICOM Media Type. See `Acceptable Media Types <#sect_8.7.5>`__.

.. _sect_9.4.2.1:

Request Type
^^^^^^^^^^^^

If the Query Parameter is not present; or if it is present with a value
other than "WADO" and the origin server does not support the value, then
the origin server shall return a 400 (Bad Request) response and may
include a payload containing an appropriate error message.

.. _sect_9.4.2.2:

Study, Series, and Instance UIDs
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

If the Study, Series, or Instance UID Query Parameters are not present,
the origin server shall return a 400 (Bad Request) response and may
include a payload containing an appropriate error message.

.. _sect_9.4.2.3:

Anonymize
^^^^^^^^^

If the Query Parameter is supported and present, and if any of the
following are true:

-  the number of parameter values is not equal to one, or

-  the parameter value is not "yes"

then the origin server shall return a 400 (Bad Request) response and may
include a payload containing an appropriate error message.

If the Target Resource has not already been de-identified, the returned
Instance shall have a new SOP Instance UID.

If the origin server is either unable or refuses to anonymize the Target
Resource, it may return an error response.

.. _sect_9.4.2.4:

Transfer Syntax UID
^^^^^^^^^^^^^^^^^^^

If this Query Parameter is supported and present with a value that is a
valid Transfer Syntax UID, the response payload shall be encoded in the
specified Transfer Syntax.

If it is not present, the response payload shall be encoded in the
default Transfer Syntax for DICOM Web Services, which is Explicit VR
Little Endian Uncompressed.

If the Query Parameter is supported and present, and if any of the
following are true:

-  the number of parameter values is not equal to one, or

-  the parameter value is not a valid UID

then the origin server shall return a 400 (Bad Request) response and may
include a payload containing an appropriate error message.

If the parameter value is a valid Transfer Syntax UID, but is not
supported by the origin server, the response shall be 406 (Not
Acceptable), and may include a payload containing a list of the Transfer
Syntaxes supported by the origin server.

.. note::

   The origin server may not be able to convert all Instances to all the
   Transfer Syntaxes it supports.

.. _sect_9.4.3:

Response
~~~~~~~~

::

   version SP status-code SP reason-phrase

::

   [Content-Type: media-type CRLF]

::

   [(Content-Length: uint / Content-Encoding: encoding) CRLF]

::

   Content-Location: url CRLF

::

   *(header-field CRLF)

::

   CRLF

::

   [payload / status-report]

.. _sect_9.4.3.1:

Status Codes
^^^^^^^^^^^^

`table_title <#table_9.4.3-1>`__ shows some common status codes
corresponding to this transaction. See also `Status Codes <#sect_8.5>`__
for additional status codes.

.. table:: Status Code Meaning

   +-----------------+------------------------+------------------------+
   | Status          | Code                   | Meaning                |
   +=================+========================+========================+
   | Success         | 200 (OK)               | The Instance was       |
   |                 |                        | successfully           |
   |                 |                        | retrieved.             |
   +-----------------+------------------------+------------------------+
   | Failure         | 400 (Bad Request)      | There was a problem    |
   |                 |                        | with the request.      |
   +-----------------+------------------------+------------------------+
   | 404 (Not Found) | The resource           |                        |
   |                 | corresponding to the   |                        |
   |                 | UIDs in the Query      |                        |
   |                 | Parameters was not     |                        |
   |                 | found.                 |                        |
   +-----------------+------------------------+------------------------+
   | 410 (Gone)      | The resource           |                        |
   |                 | corresponding to the   |                        |
   |                 | UIDs in the Query      |                        |
   |                 | Parameters, once       |                        |
   |                 | existed, but no longer |                        |
   |                 | exists.                |                        |
   +-----------------+------------------------+------------------------+

.. _sect_9.4.3.2:

Response Header Fields
^^^^^^^^^^^^^^^^^^^^^^

The origin server shall support header fields as required in
`table_title <#table_9.4.3-2>`__.

.. table:: Response Header Fields

   +----------------+----------------+----------------+----------------+
   | Name           | center         | Origin Server  | Description    |
   |                |                | Usage          |                |
   +================+================+================+================+
   | Content-Type   | di             | M              | The media-type |
   |                | com-media-type |                | of the payload |
   +----------------+----------------+----------------+----------------+
   | Content-Length | uint           | M              | Shall be       |
   |                |                |                | present if a   |
   |                |                |                | content        |
   |                |                |                | encoding has   |
   |                |                |                | not been       |
   |                |                |                | applied to the |
   |                |                |                | payload        |
   +----------------+----------------+----------------+----------------+
   | Co             | encoding       | M              | Shall be       |
   | ntent-Encoding |                |                | present if a   |
   |                |                |                | content        |
   |                |                |                | encoding has   |
   |                |                |                | been applied   |
   |                |                |                | to the payload |
   +----------------+----------------+----------------+----------------+

See `Header Fields <#sect_8.4>`__.

.. _sect_9.4.3.3:

Response Payload
^^^^^^^^^^^^^^^^

A successful response shall have a payload containing the Target
Resource in the application/dicom media type.

A failure response payload may contain a Status Report describing any
failures, warnings, or other useful information.

.. _sect_9.5:

Retrieve Rendered Instance Transaction
--------------------------------------

This transaction returns a single Instance in a Rendered Media Type. See
`Rendered Media Types <#sect_8.7.4>`__.

The Acceptable Media Type shall not be application/dicom. If it is, the
response should be 406 (Not Acceptable) response.

.. _sect_9.5.1:

Request
~~~~~~~

The request shall have the following syntax:

::

   GET SP /?{requestType}&{study}&{series}&{instance}{&frameNumber}

::

            {&accept}

::

            {&charset}

::

            {&annotation}

::

            {&rows}

::

            {&columns}

::

            {&region}

::

            {&windowCenter}

::

            {&windowWidth}

::

            {&imageQuality}

::

            {&annotation}

::

            {&presentationSeriesUID}

::

            {&presentationUID}

::

   SP HTTP/1.1 CRLF

::

   Accept: 1#media-type CRLF

::

   *(header-field CRLF)

::

   CRLF

.. _sect_9.5.1.1:

Target Resource
^^^^^^^^^^^^^^^

The Target Resource shall be an Instance of a Composite SOP Class as
defined in .

.. _sect_9.5.1.2:

Query Parameters
^^^^^^^^^^^^^^^^

The Query Parameters in this section shall only be included in a request
if the DICOM Category of the Target Resource is Single Frame,
Multi-Frame, or Video as defined in `DICOM Resource
Categories <#sect_8.7.2>`__.

The origin server shall support Query Parameters as required in
`table_title <#table_9.5.1-1>`__.

The user agent shall supply in the request Query Parameters as required
in `table_title <#table_9.5.1-1>`__.

.. table:: Query Parameters

   +----------------+----------------+-------+---------+----------------+
   | Key            | Values         | Usage | Section |                |
   +================+================+=======+=========+================+
   | contentType    | rende          | O     | M       | `Acceptable    |
   |                | red-media-type |       |         | Media          |
   |                |                |       |         | Types <#sect   |
   |                |                |       |         | _9.1.2.2.1>`__ |
   +----------------+----------------+-------+---------+----------------+
   | charset        | charset        | O     | M       | `Acceptable    |
   |                |                |       |         | Character      |
   |                |                |       |         | Sets <#sect    |
   |                |                |       |         | _9.1.2.2.2>`__ |
   +----------------+----------------+-------+---------+----------------+
   | frameNumber    | uint           | O     | O       | `Frame         |
   |                |                |       |         | Number <#sect  |
   |                |                |       |         | _9.5.1.2.1>`__ |
   +----------------+----------------+-------+---------+----------------+
   | i              | "patient" /    | O     | O       | `Image         |
   | mageAnnotation | "technique"    |       |         | Ann            |
   |                |                |       |         | otation <#sect |
   |                |                |       |         | _9.5.1.2.2>`__ |
   +----------------+----------------+-------+---------+----------------+
   | imageQuality   | uint           | O     | O       | `Image         |
   |                |                |       |         | Quality <#sect |
   |                |                |       |         | _9.5.1.2.3>`__ |
   +----------------+----------------+-------+---------+----------------+
   | rows           | uint           | O     | O       | `Viewport      |
   |                |                |       |         | Rows <#sect_9  |
   |                |                |       |         | .5.1.2.4.1>`__ |
   +----------------+----------------+-------+---------+----------------+
   | columns        | uint           | O     | O       | `Viewport      |
   |                |                |       |         | Co             |
   |                |                |       |         | lumns <#sect_9 |
   |                |                |       |         | .5.1.2.4.2>`__ |
   +----------------+----------------+-------+---------+----------------+
   | region         | 4decimal       | O     | O       | `Source Image  |
   |                |                |       |         | Region <#sect  |
   |                |                |       |         | _9.5.1.2.5>`__ |
   +----------------+----------------+-------+---------+----------------+
   | windowCenter   | decimal        | O     | O       | `Window        |
   |                |                |       |         | C              |
   |                |                |       |         | enter <#sect_9 |
   |                |                |       |         | .5.1.2.6.1>`__ |
   +----------------+----------------+-------+---------+----------------+
   | windowWidth    | decimal        | O     | O       | `Window        |
   |                |                |       |         | Width <#sect_9 |
   |                |                |       |         | .5.1.2.6.2>`__ |
   +----------------+----------------+-------+---------+----------------+
   | present        | uid            | O     | O       | `Presentation  |
   | ationSeriesUID |                |       |         | Series         |
   |                |                |       |         | UID <#sect_9   |
   |                |                |       |         | .5.1.2.7.1>`__ |
   +----------------+----------------+-------+---------+----------------+
   | p              | uid            | O     | O       | `Presentation  |
   | resentationUID |                |       |         | UID <#sect_9   |
   |                |                |       |         | .5.1.2.7.2>`__ |
   +----------------+----------------+-------+---------+----------------+

.. _sect_9.5.1.2.1:

Frame Number
''''''''''''

::

   frame-number = %s"frameNumber" "=" uint

This parameter specifies a single frame within a multi-frame image
Instance, as defined in that shall be returned. Its name is
"frameNumber" and its value shall be a positive integer (i.e., starts at
1 not 0).

.. _sect_9.5.1.2.2:

Image Annotation
''''''''''''''''

See `Image Annotation <#sect_8.3.5.1.1>`__.

.. _sect_9.5.1.2.3:

Image Quality
'''''''''''''

See `Image Quality <#sect_8.3.5.1.2>`__.

.. _sect_9.5.1.2.4:

Viewport
''''''''

The Viewport Query Parameters specify the dimensions of the user agent's
viewport. The Viewport Rows and Columns parameters specify the height
and width, in pixels, of the returned image. If either parameter is
present, both shall be present.

The Viewport parameters syntax in this Section overrides that described
in `Viewport Scaling <#sect_8.3.5.1.3>`__; however, the scaling behavior
described in that section still applies.

.. _sect_9.5.1.2.4.1:

Viewport Rows
             

::

   rows = %s"rows" "=" uint

This parameter specifies the number of pixel rows in the returned image.
It corresponds to the height in pixels of the user agent's viewport. Its
name is "rows" and its value shall be a positive integer.

.. _sect_9.5.1.2.4.2:

Viewport Columns
                

::

   columns = %s"columns" "=" uint

This parameter specifies the number of pixel columns in the returned
image. It corresponds to the width, in pixels, of the user agent's
viewport. Its name is "columns" and its value shall be a positive
integer.

.. _sect_9.5.1.2.5:

Source Image Region
'''''''''''''''''''

::

   region = %s"region" "=" xmin "," ymin "," xmax "," ymax

::

   xmin = decimal

::

   ymin = decimal

::

   xmax = decimal

::

   ymax = decimal

This parameter specifies a rectangular region of the Target Resource.
Its name is "region" and its values shall be a comma-separated list of
four positive decimal numbers:

xmin
   the left column of the region

ymin
   the top row of the region

xmax
   the right column of the region

ymax
   the bottom row of the region

The region is specified using a normalized coordinate system relative to
the size of the original image matrix, measured in rows and columns.
Where

-  0.0, 0.0 corresponds to the top row and left column of the image

-  1.0, 1.0 corresponds to the bottom row and right column of the image

and

-  0.0 <= xmin < xmax <= 1.0

-  0.0 <= ymin < ymax <= 1.0

This parameter when used in conjunction with one of the viewport
parameters, allows the user agent to map a selected area of the source
image into its viewport.

.. _sect_9.5.1.2.6:

Windowing
'''''''''

The Windowing parameters (Window Center and Window Width) are optional;
however, if either is present, both shall be present. If only one is
present the origin server shall return a 400 (Bad Request) response and
may include a payload containing an appropriate error message.

The URI Service does not support the "function" Query Parameter, which
is described in `Windowing <#sect_8.3.5.1.4>`__.

The Windowing and Presentation State parameters shall not be present in
the same request. If both are present the origin server shall return a
400 (Bad Request) response and may include a payload containing an
appropriate error message.

The Windowing parameters shall not be present if contentType is
application/dicom; if either is present the origin server shall return a
400 (Bad Request) response and may include a payload containing an
appropriate error message.

.. _sect_9.5.1.2.6.1:

Window Center
             

::

   window-center = %s"windowCenter" "=" decimal

This parameter specifies the Window Center of the returned image as
defined in . Its name is "windowCenter" and its value shall be a decimal
number.

.. _sect_9.5.1.2.6.2:

Window Width
            

::

   window-width = %s"windowWidth" "=" decimal

This parameter specifies the Window Width of the returned image as
defined in . Its name is "windowWidth" and its value shall be a decimal
number.

.. _sect_9.5.1.2.7:

Presentation State
''''''''''''''''''

The parameters below specify the Series and SOP Instance UIDs of a
Presentation State. They are optional. However, if one is present, they
shall both be present.

If the Presentation State parameters are present, then the only other
optional parameters that may be present are Annotation, Image Quality,
Region, and Viewport.

.. _sect_9.5.1.2.7.1:

Presentation Series UID
                       

::

   presentation-series = %s"presentationSeriesUID" "=" uid

This parameter specifies the Series containing the Presentation State
Instance to be used to render the image. Its name shall be
"presentationSeriesUID" and its value shall be a Series Instance UID.

.. _sect_9.5.1.2.7.2:

Presentation UID
                

::

   presentation-instance = %s"presentationUID" "=" uid

This parameter identifies the Presentation State Instance, which is used
to render the image. Its name is "presentationUID" and its value shall
be a Presentation State Instance UID of a Presentation State Instance.

.. _sect_9.5.1.3:

Request Header Fields
^^^^^^^^^^^^^^^^^^^^^

The origin server shall support header fields as required in
`table_title <#table_9.5.1-2>`__.

The user agent shall supply in the request header fields as required in
`table_title <#table_9.5.1-2>`__.

.. table:: Request Header Fields

   +---------------+------------+-------+-------------+---------------+
   | Name          | Values     | Usage | Description |               |
   +===============+============+=======+=============+===============+
   | Accept        | media-type | M     | M           | The           |
   |               |            |       |             | Acceptable    |
   |               |            |       |             | Media Types   |
   |               |            |       |             | for the       |
   |               |            |       |             | response      |
   |               |            |       |             | payload       |
   +---------------+------------+-------+-------------+---------------+
   | A             | charset    | O     | M           | List of one   |
   | ccept-Charset |            |       |             | or more       |
   |               |            |       |             | character     |
   |               |            |       |             | sets          |
   +---------------+------------+-------+-------------+---------------+

The Acceptable Media Types shall contain only Rendered Media Types. See
`Rendered Media Types <#sect_8.7.4>`__.

.. _sect_9.5.1.4:

Request Payload
^^^^^^^^^^^^^^^

The request message has no payload.

.. _sect_9.5.2:

Behavior
~~~~~~~~

A success response shall contain the Target Resource in an Acceptable
Rendered Media Type. See `Rendered Media Types <#sect_8.7.4>`__.

The Target Resource shall be rendered and returned as specified in the
Query Parameters. Presentation State transformations are applied using
the appropriate rendering pipeline specified in . Any Source Image
Region parameters are applied after any Presentation State parameters.
Any Viewport parameters are applied after any Source Image Region.

Even if the output of the image is defined in P-Values (grayscale values
intended for display on a device calibrated to the DICOM Grayscale
Standard Display Function ), or contains an ICC profile, the grayscale
or color space for the rendered image is not defined by this Standard.

.. _sect_9.5.2.1:

Frame Number
^^^^^^^^^^^^

If this Query Parameter is supported and is present in the request,the
origin server shall use the specified frame as the Target Resource.

However, if any of the following are true:

-  the Target Resource is not a multi-frame image or video,

-  the number of parameter values is not equal to one, or

-  the parameter value is not a positive integer less than or equal to
   the number of frames in the Instance

the origin server shall return a 400 (Bad Request) responseand may
include a payload containing an appropriate error message.

.. _sect_9.5.2.2:

Windowing
^^^^^^^^^

If these Query Parameters are supported and are present in the request,
the origin server shall use them as described in
`Windowing <#sect_8.3.5.1.4>`__.

However, if any of the following are true:

-  only one of the parameters is present,

-  either of the parameter values is not a decimal number, or

-  the Presentation Series UID or the Presentation UID Query Parameters
   are present

then the origin server shall return a 400 (Bad Request) response and may
include a payload containing an appropriate error message.

.. _sect_9.5.2.3:

Presentation State
^^^^^^^^^^^^^^^^^^

If the Target Resource is a Presentation State and If the Presentation
Size Mode is SCALE TO FIT or TRUE SIZE, then the displayed area
specified in the Presentation State shall be scaled, maintaining the
aspect ratio, to fit the size specified by the rows and columns
parameters if present, otherwise the displayed area selected in the
presentation state will be returned without scaling.

.. note::

   1. The intent of the TRUE SIZE mode in the presentation state cannot
      be satisfied, since the physical size of the pixels displayed by
      the web browser is unlikely to be known. If the Presentation Size
      Mode in the presentation state is MAGNIFY, then the displayed area
      specified in the presentation shall be magnified (scaled) as
      specified in the presentation state. It will then be cropped to
      fit the size specified by the viewport parameters, if present.

   2. Any Displayed Area relative annotations specified in the
      presentation state are rendered relative to the Specified
      Displayed Area within the presentation state, not the size of the
      returned image.

Though the output of the presentation state is defined in DICOM to be in
P-Values (grayscale values intended for display on a device calibrated
to the DICOM Grayscale Standard Display Function ), the grayscale or
color space for the images returned by the request is not defined by
this standard.

However, if any of the following are true:

-  the Frame Number, Source Image Region, or Windowing parameters are
   present,

-  the Presentation Series UID does not correspond to an existing
   Presentation Series on the origin server, or

-  the Presentation UID does not correspond to an existing Presentation
   Instance on the origin server

the origin server shall return a 400 (Bad Request) response and may
include a payload containing an appropriate error message.

.. _sect_9.5.2.4:

Source Image Region
^^^^^^^^^^^^^^^^^^^

If this Query Parameter is supported and present:

-  An image matrix corresponding to the region specified by Source Image
   Region shall be returned with its size corresponding to the specified
   normalized coordinate values.

-  If the Presentation UID parameter is present, the region shall be
   selected after the corresponding presentation state has been applied
   on the images.

However, if any of the following are true:

-  the Query Parameter specifies an ill-defined region,

-  there are greater or fewer than four parameter values present, or

-  any of the parameters do not conform to the requirements specified in
   `Source Image Region <#sect_9.5.1.2.5>`__

the origin server shall return a 400 (Bad Request) response and may
include a payload containing an appropriate error message.

.. _sect_9.5.2.5:

Viewport
^^^^^^^^

Viewport parameters are applied to the region specified by the
Presentation State and/or Source Image Region, if present; otherwise,
the Viewport Query Parameters are applied to the full original image.

If both rows and columns Query Parameters are specified, then each shall
be interpreted as a maximum, and a size will be chosen for the returned
image within these constraints, maintaining the aspect ratio of the
selected region.

If the rows Query Parameter is absent and the columns Query Parameter is
present, the number of rows in the returned image shall be chosen to
maintain the aspect ratio of the selected region.

If the columns Query Parameter is absent and the rows Query Parameter is
present, the number of columns in the returned image shall be chosen to
maintain the aspect ratio of the selected region.

If both Query Parameters are absent, the image (or selected region) is
returned with its original size (or the size of the presentation state
applied to the image), resulting in one pixel in the returned image for
each pixel in the original image.

.. _sect_9.5.3:

Response
~~~~~~~~

::

   version SP status-code SP reason-phrase

::

   [Content-Type: rendered-media-type CRLF]

::

   [(Content-Length: uint / Content-Encoding: encoding) CRLF]

::

   [Content-Location: url CRLF]

::

   *(header-field CRLF)

::

   CRLF

::

   [payload / status-report]

.. _sect_9.5.3.1:

Status Codes
^^^^^^^^^^^^

`table_title <#table_9.5.3-1>`__ shows some common status codes
corresponding to this transaction. See also `Status Codes <#sect_8.5>`__
for additional status codes.

.. table:: Status Code Meaning

   +---------+-------------------+--------------------------------------+
   | Status  | Code              | Meaning                              |
   +=========+===================+======================================+
   | Success | 200 (OK)          | All Instances were successfully      |
   |         |                   | rendered and retrieved.              |
   +---------+-------------------+--------------------------------------+
   | Failure | 400 (Bad Request) | There was a problem with the         |
   |         |                   | request.                             |
   +---------+-------------------+--------------------------------------+

.. _sect_9.5.3.2:

Response Header Fields
^^^^^^^^^^^^^^^^^^^^^^

The origin server shall support header fields as required in
`table_title <#table_9.5.3-2>`__.

.. table:: Response Header Fields

   +-----------------+------------+-----------------+-----------------+
   | Name            | center     | Origin Server   | Description     |
   |                 |            | Usage           |                 |
   +=================+============+=================+=================+
   | Content-Type    | media-type | C               | Shall be        |
   |                 |            |                 | present if the  |
   |                 |            |                 | response        |
   |                 |            |                 | contains a      |
   |                 |            |                 | payload. See    |
   |                 |            |                 | `Payload Header |
   |                 |            |                 | Fields <#       |
   |                 |            |                 | sect_8.4.3>`__. |
   +-----------------+------------+-----------------+-----------------+
   | C               | encoding   | C               | Shall be        |
   | ontent-Encoding |            |                 | present if the  |
   |                 |            |                 | response        |
   |                 |            |                 | payload has a   |
   |                 |            |                 | content         |
   |                 |            |                 | encoding. See   |
   |                 |            |                 | `Payload Header |
   |                 |            |                 | Fields <#       |
   |                 |            |                 | sect_8.4.3>`__. |
   +-----------------+------------+-----------------+-----------------+
   | Content-Length  | uint       | C               | Shall be        |
   |                 |            |                 | present if the  |
   |                 |            |                 | response        |
   |                 |            |                 | payload does    |
   |                 |            |                 | not have a      |
   |                 |            |                 | content         |
   |                 |            |                 | encoding. See   |
   |                 |            |                 | `Payload Header |
   |                 |            |                 | Fields <#       |
   |                 |            |                 | sect_8.4.3>`__. |
   +-----------------+------------+-----------------+-----------------+
   | C               | url        | C               | Shall be        |
   | ontent-Location |            |                 | present if the  |
   |                 |            |                 | response has a  |
   |                 |            |                 | payload         |
   |                 |            |                 | containing a    |
   |                 |            |                 | resource. See   |
   |                 |            |                 | `Payload Header |
   |                 |            |                 | Fields <#       |
   |                 |            |                 | sect_8.4.3>`__. |
   +-----------------+------------+-----------------+-----------------+

See also `Header Fields <#sect_8.4>`__.

.. _sect_9.5.3.3:

Response Payload
^^^^^^^^^^^^^^^^

A success response shall contain a single rendered image encoded in the
Selected Media Type.

A failure response payload may contain a Status Report describing any
failures, warnings, or other useful information.

