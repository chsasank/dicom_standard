.. _chapter_10:

Studies Service and Resources
=============================

.. _sect_10.1:

Overview
--------

The Studies Resource enables a user agent to store, retrieve, update,
and search an origin server for DICOM Studies, Series, and Instances,
along with their /metadata, /rendered, and /thumbnail variants; as well
as Frames and Bulkdata.

The Retrieve transaction of this Service is also known as WADO-RS. The
Store transaction of this Service is also known as STOW-RS. The Search
transaction of this Service is also known as QIDO-RS. See `Transactions
Overview <#sect_10.3>`__.

.. _sect_10.1.1:

Resource Descriptions
~~~~~~~~~~~~~~~~~~~~~

The Studies Service manages a collection of DICOM Study resources. Each
Study is organized in a hierarchy of sub-resources that correspond to
the DICOM Information Model. See .

There are three top level resources:

========== ================================================
/studies   references all Studies managed by the service.
/series    references all Series managed by the service.
/instances references all Instances managed by the service.
========== ================================================

The following URI Template variables are used in resource definitions in
this Section.

+-------------+-------------------------------------------------------+
| {study}     | the Study Instance UID of a Study managed by the      |
|             | Studies Service.                                      |
+-------------+-------------------------------------------------------+
| {series}    | the Series Instance UID of a Series contained within  |
|             | a Study resource.                                     |
+-------------+-------------------------------------------------------+
| {instance}  | the SOP Instance UID of an Instance contained within  |
|             | a Series resource.                                    |
+-------------+-------------------------------------------------------+
| {frames}    | a comma-separated list of frame numbers, in ascending |
|             | order, contained within an Instance.                  |
+-------------+-------------------------------------------------------+
| {/bulkdata} | an opaque URI that references a Bulkdata Value.       |
+-------------+-------------------------------------------------------+

The Studies Service defines the following resources:

.. table:: Resources and Descriptions

   +--------------------+------------------------------------------------+
   | Resource           | Description                                    |
   +====================+================================================+
   | Studies Service    | The Base URI of the Studies Service.           |
   +--------------------+------------------------------------------------+
   | All Studies        | The All Studies resource references the entire |
   |                    | collection of Studies contained in the Studies |
   |                    | Service.                                       |
   +--------------------+------------------------------------------------+
   | Study              | The Study resource references a single Study.  |
   +--------------------+------------------------------------------------+
   | Study Metadata     | The Study Metadata resource references the     |
   |                    | Metadata of a single Study.                    |
   +--------------------+------------------------------------------------+
   | Rendered Study     | The Rendered Study resource references a Study |
   |                    | to be rendered.                                |
   +--------------------+------------------------------------------------+
   | Study Thumbnail    | The Study Thumbnail resource references a      |
   |                    | thumbnail image of a Study.                    |
   +--------------------+------------------------------------------------+
   | Study's Series     | The Study's Series resource references the     |
   |                    | collection of all Series contained in a Study. |
   +--------------------+------------------------------------------------+
   | Study's Instances  | The Study's Instances resource references the  |
   |                    | collection of all Instances in a single Study. |
   +--------------------+------------------------------------------------+
   | All Series         | The All Series resource references the         |
   |                    | collection of all Series in all Studies        |
   |                    | contained in the Studies Service.              |
   +--------------------+------------------------------------------------+
   | Series             | The Series resource references a single        |
   |                    | Series.                                        |
   +--------------------+------------------------------------------------+
   | Series Metadata    | The Series Metadata resource contains the      |
   |                    | Metadata of a single Series in a Study.        |
   +--------------------+------------------------------------------------+
   | Rendered Series    | The Rendered Series resource references a      |
   |                    | Series to be rendered.                         |
   +--------------------+------------------------------------------------+
   | Series Thumbnail   | The Series Thumbnail resource references a     |
   |                    | thumbnail image of a Series.                   |
   +--------------------+------------------------------------------------+
   | Series' Instances  | The Series' Instances resource references the  |
   |                    | collection of all Instances in a single        |
   |                    | Series.                                        |
   +--------------------+------------------------------------------------+
   | All Instances      | The All Instances resource references the      |
   |                    | collection of all Instances in all Series in   |
   |                    | all Studies contained in the Studies Service.  |
   +--------------------+------------------------------------------------+
   | Instance           | The Instance resource references a single      |
   |                    | Instance.                                      |
   +--------------------+------------------------------------------------+
   | Instance Metadata  | The Instance Metadata resource contains the    |
   |                    | Metadata of a single Instance.                 |
   +--------------------+------------------------------------------------+
   | Rendered Instance  | The Rendered Instance resource references an   |
   |                    | Instance to be rendered.                       |
   +--------------------+------------------------------------------------+
   | Instance Thumbnail | The Instance Thumbnail resource references a   |
   |                    | thumbnail image of an Instance.                |
   +--------------------+------------------------------------------------+
   | Frames             | The Frames resource references an ordered      |
   |                    | collection of frames in a single multi-frame   |
   |                    | Instance.                                      |
   +--------------------+------------------------------------------------+
   | Rendered Frames    | The Rendered Frames resource references an     |
   |                    | ordered collection of frames of a single       |
   |                    | multi-frame Instance, to be rendered.          |
   +--------------------+------------------------------------------------+
   | Frame Thumbnail    | The Frame Thumbnail resource references a      |
   |                    | thumbnail image for frames within an Instance. |
   +--------------------+------------------------------------------------+
   | Bulkdata           | The Bulkdata resource contains one or more     |
   |                    | Bulkdata Values.                               |
   +--------------------+------------------------------------------------+

.. _sect_10.1.2:

Common Query Parameters
~~~~~~~~~~~~~~~~~~~~~~~

The origin server shall support Query Parameters as required in
`table_title <#table_10.1.2-1>`__.

The user agent shall supply in the request Query Parameters as required
in `table_title <#table_10.1.2-1>`__.

.. table:: Common Query Parameters

   +----------------+------------+-------+---------+------------------+
   | Name           | Value      | Usage | Section |                  |
   +================+============+=======+=========+==================+
   | Accept         | media-type | O     | M       | `Accept Query    |
   |                |            |       |         | Parameter <#     |
   |                |            |       |         | sect_8.3.3.1>`__ |
   +----------------+------------+-------+---------+------------------+
   | Accept-Charset | charset    | O     | M       | `Character Set   |
   |                |            |       |         | Query            |
   |                |            |       |         | Parameter <#     |
   |                |            |       |         | sect_8.3.3.2>`__ |
   +----------------+------------+-------+---------+------------------+

.. _sect_10.1.3:

Common Media Types
~~~~~~~~~~~~~~~~~~

The origin server media type requirements are defined in each
Transaction of this Service.

The origin server shall support the Transfer Syntax and Character Set
media type parameters. See `Transfer Syntax
Parameter <#sect_8.7.3.5.2>`__ and `Character Set
Parameter <#sect_8.7.3.5.3>`__.

.. _sect_10.2:

Conformance
-----------

An origin server claiming conformance to the Retrieve Transaction of the
Studies Service:

-  shall support the Retrieve Capabilities Transaction (see
   `Request <#sect_8.9.1>`__);

-  shall support the Retrieve Transaction for all mandatory resources in
   `table_title <#table_10.3-2>`__.

An origin server claiming conformance to the Store Transaction of the
Studies Service:

-  shall support the Retrieve Capabilities Transaction (see
   `Request <#sect_8.9.1>`__);

-  shall support the Store Transaction for all mandatory resources in
   `table_title <#table_10.3-2>`__.

An origin server claiming conformance to the Search Transaction of the
Studies Service:

-  shall support the Retrieve Capabilities Transaction (see
   `Request <#sect_8.9.1>`__);

-  shall support the Search Transaction for all mandatory resources in
   `table_title <#table_10.3-2>`__.

The user agent may support any of the transactions for any of the
corresponding resources in `table_title <#table_10.3-2>`__.

.. _sect_10.3:

Transactions Overview
---------------------

The Studies Service consists of the following transactions:

.. table:: Studies Service Transactions

   +--------------+--------+-------------+--------------+--------------+
   | Transaction  | Method | Payload     | Description  |              |
   | Name         |        |             |              |              |
   +==============+========+=============+==============+==============+
   | Retrieve     | GET    | N/A         | Instance(s)  | Retrieve one |
   |              |        |             | or Bulkdata  | or more      |
   |              |        |             |              | rep          |
   |              |        |             |              | resentations |
   |              |        |             |              | of DICOM     |
   |              |        |             |              | Resources.   |
   +--------------+--------+-------------+--------------+--------------+
   | Store        | POST   | Instance(s) | Store        | Stores one   |
   |              |        |             | Instances    | or more      |
   |              |        |             | Response     | rep          |
   |              |        |             | Module       | resentations |
   |              |        |             |              | of DICOM     |
   |              |        |             |              | Resources,   |
   |              |        |             |              | contained in |
   |              |        |             |              | the request  |
   |              |        |             |              | payload, in  |
   |              |        |             |              | the location |
   |              |        |             |              | referenced   |
   |              |        |             |              | by the       |
   |              |        |             |              | Target       |
   |              |        |             |              | Resource.    |
   +--------------+--------+-------------+--------------+--------------+
   | Search       | GET    | N/A         | Result(s)    | Searches the |
   |              |        |             |              | Target       |
   |              |        |             |              | Resource for |
   |              |        |             |              | DICOM        |
   |              |        |             |              | objects that |
   |              |        |             |              | match the    |
   |              |        |             |              | search       |
   |              |        |             |              | parameters   |
   |              |        |             |              | and returns  |
   |              |        |             |              | a list of    |
   |              |        |             |              | matches in   |
   |              |        |             |              | an           |
   |              |        |             |              | Acceptable   |
   |              |        |             |              | Media Type.  |
   +--------------+--------+-------------+--------------+--------------+

In `table_title <#table_10.3-2>`__, the Target Resources permitted for
each transaction are marked with M if support is mandatory for the
origin server and O if it is optional. A blank cell indicates that the
resource is not allowed in the transaction.

.. table:: Resources by Transaction

   ================== ======== ===== ======
   Resource           Retrieve Store Search
   ================== ======== ===== ======
   Studies Service                   
   All Studies                 M     M
   Study              M        M     M
   Study Metadata     M              
   Study Bulkdata     M              
   Rendered Study     M              
   Study Thumbnail    O              
   Study's Series                    M
   Study's Instances                 M
   All Series                        M
   Series             M              M
   Series Metadata    M              
   Series Bulkdata    M              
   Series' Instances                 M
   Rendered Series    M              
   Series Thumbnail   O              
   All Instances                     M
   Instance           M              M
   Instance Metadata  M              
   Instance Bulkdata  M              
   Rendered Instance  M              
   Instance Thumbnail O              
   Frames             M              
   Rendered Frames    M              
   Frame Thumbnail    O              
   Bulkdata           M        M     
   ================== ======== ===== ======

.. _sect_10.4:

Retrieve Transaction
--------------------

This Transaction uses the GET method to retrieve the Target Resource.
The media type in the response payload will depend on the Target URI and
the Query Parameters; for example, Instances as application/dicom,
Metadata as application/dicom+json or rendered Instances as
application/jpeg images.

The retrieve transaction supports DICOM, Rendered, and Thumbnail
Resources.

.. _sect_10.4.1:

Request
~~~~~~~

The request shall have the following syntax:

::

   GET SP "/" {/resource} {?parameter*} SP versionCRLF

::

   Accept: 1#media-type CRLF

::

   *(header-fieldCRLF)

::

   CRLF

Where parameter is one of the Query Parameters defined for the Target
Resource in `Query Parameters <#sect_10.4.1.2>`__.

.. _sect_10.4.1.1:

Target Resources
^^^^^^^^^^^^^^^^

.. _sect_10.4.1.1.1:

DICOM Resources
'''''''''''''''

`table_title <#table_10.4.1-1>`__ defines the DICOM resources that may
be retrieved.

.. table:: Retrieve Transaction DICOM Resources

   +----------+----------------------------------------------------------+
   | Resource | URI Template                                             |
   +==========+==========================================================+
   | Study    | ::                                                       |
   |          |                                                          |
   |          |    /studies/{study}                                      |
   +----------+----------------------------------------------------------+
   | Series   | ::                                                       |
   |          |                                                          |
   |          |    /studies/{study}/series/{series}                      |
   +----------+----------------------------------------------------------+
   | Instance | ::                                                       |
   |          |                                                          |
   |          |    /studies/{study}/series/{series}/instances/{instance} |
   +----------+----------------------------------------------------------+
   | Frames   | ::                                                       |
   |          |                                                          |
   |          |    /studies/{stu                                         |
   |          | dy}/series/{series}/instances/{instance}/frames/{frames} |
   +----------+----------------------------------------------------------+
   | Bulkdata | ::                                                       |
   |          |                                                          |
   |          |    /{/bulkdata}                                          |
   +----------+----------------------------------------------------------+

.. _sect_10.4.1.1.2:

Metadata Resources
''''''''''''''''''

`table_title <#table_10.4.1-2>`__ defines the resources used to retrieve
the metadata contained in Instances.

.. table:: Retrieve Transaction Metadata Resources

   +-------------------+-------------------------------------------------+
   | Resource          | URI Template                                    |
   +===================+=================================================+
   | Study Metadata    | ::                                              |
   |                   |                                                 |
   |                   |    /studies/{study}/metadata                    |
   +-------------------+-------------------------------------------------+
   | Series Metadata   | ::                                              |
   |                   |                                                 |
   |                   |    /studies/{study}/series/{series}/metadata    |
   +-------------------+-------------------------------------------------+
   | Instance Metadata | ::                                              |
   |                   |                                                 |
   |                   |    /studies/{study                              |
   |                   | }/series/{series}/instances/{instance}/metadata |
   +-------------------+-------------------------------------------------+

The Metadata Resources are used to retrieve the DICOM instances without
retrieving Bulkdata. The Metadata returned for a study, series, or
instance resource includes all Attributes in the resource. For Data
Elements having a Value Representation (VR) of DS, FL, FD, IS, LT, OB,
OD, OF, OL, OV, OW, SL, SS, ST, SV, UC, UL, UN, US, UT and UV, the
origin server is permitted to replace the Value Field of the Data
Element with a Bulkdata URI. The user agent can use the Bulkdata URI to
retrieve the Bulkdata.

.. _sect_10.4.1.1.3:

Rendered Resources
''''''''''''''''''

A Retrieve Transaction on a Rendered Resource will return a response
that contains representations of a DICOM Resource rendered as
appropriate images, videos, text documents, or other representations.
Its primary use case is to provide user agents with a simple means to
display medical images and related documents, without requiring deep
knowledge of DICOM data structures and encodings.

A Rendered Resource contains one or more rendered representations, i.e.,
in a Rendered Media type, of its parent DICOM Resource.
`table_title <#table_10.4.1-3>`__ shows the Rendered Resources supported
by the Retrieve transaction along with their associated URI templates.

.. table:: Retrieve Transaction Rendered Resources

   +-------------------+-------------------------------------------------+
   | Resource          | URI Template                                    |
   +===================+=================================================+
   | Rendered Study    | ::                                              |
   |                   |                                                 |
   |                   |    /studies/{study}/rendered                    |
   +-------------------+-------------------------------------------------+
   | Rendered Series   | ::                                              |
   |                   |                                                 |
   |                   |    /studies/{study}/series/{series}/rendered    |
   +-------------------+-------------------------------------------------+
   | Rendered Instance | ::                                              |
   |                   |                                                 |
   |                   |    /studies/{study                              |
   |                   | }/series/{series}/instances/{instance}/rendered |
   +-------------------+-------------------------------------------------+
   | Rendered Frames   | ::                                              |
   |                   |                                                 |
   |                   |    /studies/{study}/series/{series              |
   |                   | }/instances/{instance}/frames/{frames}/rendered |
   +-------------------+-------------------------------------------------+

The origin server shall be able to render all valid Instances of the
Composite SOP classes for which conformance is claimed, e.g., origin
server shall be able to render all Photometric Interpretations that are
defined in the IOD for that SOP class.

The content type of the response payload shall be a Rendered Media Type.
See `Rendered Media Types <#sect_8.7.4>`__.

.. _sect_10.4.1.1.4:

Thumbnail Resources
'''''''''''''''''''

A Retrieve Transaction on a Thumbnail resource will return a response
that contains a rendered representation of its parent DICOM Resource.

`table_title <#table_10.4.1-4>`__ shows the Thumbnail resources
supported by the Retrieve transaction along with their associated URI
templates.

.. table:: Retrieve Transaction Thumbnail Resources

   +--------------------+------------------------------------------------+
   | Resource           | URI Template                                   |
   +====================+================================================+
   | Study Thumbnail    | ::                                             |
   |                    |                                                |
   |                    |    /studies/{study}/thumbnail                  |
   +--------------------+------------------------------------------------+
   | Series Thumbnail   | ::                                             |
   |                    |                                                |
   |                    |    /studies/{study}/series/{series}/thumbnail  |
   +--------------------+------------------------------------------------+
   | Instance Thumbnail | ::                                             |
   |                    |                                                |
   |                    |    /studies/{study}/                           |
   |                    | series/{series}/instances/{instance}/thumbnail |
   +--------------------+------------------------------------------------+
   | Frame Thumbnail    | ::                                             |
   |                    |                                                |
   |                    |    /studies/{study}/series/{series}/           |
   |                    | instances/{instance}/frames/{frames}/thumbnail |
   +--------------------+------------------------------------------------+

The representation returned in the response to a Retrieve Thumbnail
resource request shall be in a Rendered Media Type. The Thumbnail shall
not contain any Patient Identifying Information. Only a single image
shall be returned.

If the origin server supports any of the Thumbnail resources, it shall
support all of them.

The origin server will determine what constitutes a meaningful
representation.

The origin server may return a redirection response (HTTP status code
302) to a rendered resource instead of returning a rendered image.

There is no requirement that Thumbnail resources be related to any Icon
Image Sequence (0088,0200) encoded in Instances or returned in query
responses.

.. _sect_10.4.1.2:

Query Parameters
^^^^^^^^^^^^^^^^

The origin server shall support Query Parameters as required in
`table_title <#table_10.4.1-5>`__.

The user agent shall supply in the request Query Parameters as required
in `table_title <#table_10.4.1-5>`__.

.. table:: Query Parameters by Resource

   +------------+------------------+-------+---------+------------------+
   | Key        | Resource         | Usage | Section |                  |
   |            | Category         |       |         |                  |
   +============+==================+=======+=========+==================+
   | accept     | All              | O     | M       | `Accept Query    |
   |            |                  |       |         | Parameter <#     |
   |            |                  |       |         | sect_8.3.3.1>`__ |
   +------------+------------------+-------+---------+------------------+
   | charset    | Text             | O     | M       | `Character Set   |
   |            |                  |       |         | Query            |
   |            |                  |       |         | Parameter <#     |
   |            |                  |       |         | sect_8.3.3.2>`__ |
   +------------+------------------+-------+---------+------------------+
   | annotation | Rendered         | O     | M       | `Image           |
   |            |                  |       |         | Annotation <#se  |
   |            |                  |       |         | ct_8.3.5.1.1>`__ |
   +------------+------------------+-------+---------+------------------+
   | quality    | Rendered         | O     | M       | `Image           |
   |            |                  |       |         | Quality <#se     |
   |            |                  |       |         | ct_8.3.5.1.2>`__ |
   +------------+------------------+-------+---------+------------------+
   | viewport   | Rendered         | O     | M       | `Viewport        |
   |            |                  |       |         | Scaling <#se     |
   |            |                  |       |         | ct_8.3.5.1.3>`__ |
   +------------+------------------+-------+---------+------------------+
   | Thumbnail  | O                | O     |         |                  |
   +------------+------------------+-------+---------+------------------+
   | window     | Rendered         | O     | M       | `Windowing <#se  |
   |            |                  |       |         | ct_8.3.5.1.4>`__ |
   +------------+------------------+-------+---------+------------------+
   | iccprofile | Rendered         | O     | O       | `ICC             |
   |            |                  |       |         | Profile <#se     |
   |            |                  |       |         | ct_8.3.5.1.5>`__ |
   +------------+------------------+-------+---------+------------------+

.. _sect_10.4.1.3:

Request Header Fields
^^^^^^^^^^^^^^^^^^^^^

The origin server shall support header fields as required in
`table_title <#table_10.4.1-6>`__ in the request.

The user agent shall supply in the request header fields as required in
`table_title <#table_10.4.1-6>`__.

.. table:: Request Header Fields

   +---------------+------------+-------+-------------+---------------+
   | Name          | Values     | Usage | Description |               |
   +===============+============+=======+=============+===============+
   | Accept        | media-type | M     | M           | The           |
   |               |            |       |             | Acceptable    |
   |               |            |       |             | Media Types   |
   |               |            |       |             | of the        |
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

.. _sect_10.4.1.4:

Request Payload
^^^^^^^^^^^^^^^

The request shall have no payload.

.. _sect_10.4.2:

Behavior
~~~~~~~~

A success response shall contain the Target Resource in an Acceptable
Media Type. See `Rendered Media Types <#sect_8.7.4>`__.

.. _sect_10.4.3:

Response
~~~~~~~~

The response shall have the following syntax:

::

   version SP status-code SP reason-phrase CRLF

::

   [Content-Type: media-type CRLF]

::

   [(Content-Length: uint / Content-Encoding: encoding) CRLF]

::

   [Content-Location: url CRLF]

::

   *(header-field CRLF)

::

   CRLF

::

   payload / status-report

.. _sect_10.4.3.1:

Status Codes
^^^^^^^^^^^^

`table_title <#table_10.4.3-1>`__ shows some common status codes
corresponding to this transaction. See also `Status Codes <#sect_8.5>`__
for additional status codes.

.. table:: Status Code Meaning

   +----------------------+----------------------+----------------------+
   | Status               | Code                 | Meaning              |
   +======================+======================+======================+
   | Success              | 200 (OK)             | The response payload |
   |                      |                      | contains             |
   |                      |                      | representations for  |
   |                      |                      | all of the Target    |
   |                      |                      | Resource(s)          |
   +----------------------+----------------------+----------------------+
   | 206 (Partial         | The response payload |                      |
   | Content)             | contains             |                      |
   |                      | representations for  |                      |
   |                      | some, but not all,   |                      |
   |                      | of the Target        |                      |
   |                      | Resource(s)          |                      |
   +----------------------+----------------------+----------------------+
   | Failure              | 400 (Bad Request)    | The origin cannot    |
   |                      |                      | process the request  |
   |                      |                      | because of errors in |
   |                      |                      | the request headers  |
   |                      |                      | or parameters.       |
   +----------------------+----------------------+----------------------+
   | 404 (Not Found)      | The Target Resource  |                      |
   |                      | does not exist       |                      |
   +----------------------+----------------------+----------------------+
   | 406 (Not Acceptable) | The origin server    |                      |
   |                      | does not support any |                      |
   |                      | of the Acceptable    |                      |
   |                      | Media Types          |                      |
   +----------------------+----------------------+----------------------+
   | 410 (Gone)           | The Target Resource  |                      |
   |                      | has been deleted     |                      |
   +----------------------+----------------------+----------------------+
   | 413 (Payload Too     | The Target Resource  |                      |
   | Large)               | is too large to be   |                      |
   |                      | returned by the      |                      |
   |                      | origin server.       |                      |
   +----------------------+----------------------+----------------------+

.. _sect_10.4.3.2:

Response Header Fields
^^^^^^^^^^^^^^^^^^^^^^

The origin server shall supply header fields as required by
`table_title <#table_10.4.3-2>`__.

.. table:: Response Header Fields

   +--------------+------------+-------------------+-------------------+
   | Name         | center     | Origin Server     | Description       |
   |              |            | Usage             |                   |
   +==============+============+===================+===================+
   | Content-Type | media-type | C                 | The media type of |
   |              |            |                   | the payload.      |
   |              |            |                   |                   |
   |              |            |                   | Shall be present  |
   |              |            |                   | if the response   |
   |              |            |                   | has a payload.    |
   +--------------+------------+-------------------+-------------------+

See also `Header Fields <#sect_8.4>`__.

.. _sect_10.4.3.3:

Response Payload
^^^^^^^^^^^^^^^^

A success response shall have a payload containing one or more
representations of the Target Resource in an Acceptable Media Type. The
payload may be single part or multipart depending on the media type.

A failure response payload should contain a Status Report describing any
failures, warnings, or other useful information.

`table_title <#table_10.4.3-3>`__ shows the media type category for each
resource type. The origin server shall support the default and required
media types in the media type category specified.

.. table:: Resource Media Types

   +---------------------+----------------------+----------------------+
   | Resource            | Section              | Media Type Category  |
   +=====================+======================+======================+
   | DICOM Resources     | `DICOM               | DICOM Media Types    |
   |                     | Resources <          |                      |
   |                     | #sect_10.4.1.1.1>`__ |                      |
   +---------------------+----------------------+----------------------+
   | Metadata Resources  | `Metadata            | DICOM Media Types    |
   |                     | Resources <          |                      |
   |                     | #sect_10.4.1.1.2>`__ |                      |
   +---------------------+----------------------+----------------------+
   | Rendered Resources  | `Rendered            | Rendered Media Types |
   |                     | Resources <          |                      |
   |                     | #sect_10.4.1.1.3>`__ |                      |
   +---------------------+----------------------+----------------------+
   | Thumbnail Resources | `Thumbnail           | Rendered Media Types |
   |                     | Resources <          |                      |
   |                     | #sect_10.4.1.1.4>`__ |                      |
   +---------------------+----------------------+----------------------+

DICOM Media Types are described in `DICOM Media Types and Media Types
For Bulkdata <#sect_8.7.3>`__. Rendered Media Types are described in
`Rendered Media Types <#sect_8.7.4>`__.

.. _sect_10.4.4:

Media Types
~~~~~~~~~~~

The origin server shall support the media types specified as default or
required in `table_title <#table_10.4.4-1>`__.

.. table:: Default, Required, and Optional Media Types

   +----------------------------+----------+----------------------------+
   | Media Type                 | Usage    | Section                    |
   +============================+==========+============================+
   | application/dicom          | Required | `The application/dicom     |
   |                            |          | Media                      |
   |                            |          | Type <#sect_8.7.3.1>`__    |
   +----------------------------+----------+----------------------------+
   | application/dicom+json     | Default  | `DICOM Metadata Media      |
   |                            |          | Types <#sect_8.7.3.2>`__   |
   +----------------------------+----------+----------------------------+
   | multipart/related;         | Required | `DICOM Metadata Media      |
   | ty                         |          | Types <#sect_8.7.3.2>`__   |
   | pe="application/dicom+xml" |          |                            |
   +----------------------------+----------+----------------------------+
   | multipart/related;         | Required | `DICOM Bulkdata Media      |
   | type=                      |          | Types <#sect_8.7.3.3>`__   |
   | "application/octet-stream" |          |                            |
   +----------------------------+----------+----------------------------+
   | Rendered Media Types       | Optional | `Rendered Media            |
   |                            |          | Types <#sect_8.7.4>`__     |
   +----------------------------+----------+----------------------------+
   | Rendered Media Types       | Optional | `Rendered Media            |
   |                            |          | Types <#sect_8.7.4>`__     |
   +----------------------------+----------+----------------------------+

.. _sect_10.4.5:

Conformance Statement
~~~~~~~~~~~~~~~~~~~~~

The creator of an implementation shall document in its Conformance
Statement:

-  the origin server and/or user agent role(s) played,

-  the resources supported for this transaction,

-  the media types supported for this transaction,

-  the optional Query Parameters supported,

-  the optional Header Fields supported.

The creator of an implementation shall also document:

-  The Composite SOP classes supported, including:

   -  the Image Storage SOP classes supported,

   -  the Image Storage SOP classes supported by Rendered Presentation
      States.

-  If Thumbnails are supported:

   -  A high-level description of the method used to render thumbnails
      for the study, series, or instance.

      .. note::

         The description could indicate, for example, whether a
         representative instance is chosen from a series, and how that
         instance is selected, or that per-modality fixed content is
         used.

   -  The minimum and maximum sizes for thumbnails.

   -  Character sets supported for Thumbnail resources (if other than
      UTF-8).

.. _sect_10.5:

Store Transaction
-----------------

This transaction uses the POST method to Store representations of
Studies, Series, and Instances contained in the request payload.

The Store transaction supports only DICOM resources. The resource can be
supplied as a single Instance, or as separate Metadata and Bulkdata.

.. _sect_10.5.1:

Request
~~~~~~~

The request shall have the following syntax:

::

   POST SP "/" {/resource} SP version CRLF

::

   Accept: 1#media-type CRLF

::

   Content-Type: dicom-media-type CRLF

::

   (Content-Length: uint / Content-Encoding: encoding) CRLF

::

   *(header-field CRLF)

::

   CRLF

::

   payload

.. _sect_10.5.1.1:

Target Resources
^^^^^^^^^^^^^^^^

.. _sect_10.5.1.1.1:

DICOM Resources
'''''''''''''''

`table_title <#table_10.5.1-1>`__ defines the resources used to store
Instances.

.. table:: Store Transaction DICOM Resources

   +----------+---------------------+-----------------------------------+
   | Resource | URI Template        | Description                       |
   +==========+=====================+===================================+
   | Studies  | ::                  | Stores a set of representations   |
   |          |                     | that may have different Study     |
   |          |    /studies         | Instance UIDs.                    |
   +----------+---------------------+-----------------------------------+
   | Study    | ::                  | Stores a set of representations   |
   |          |                     | that belong to the same Study,    |
   |          |    /studies/{study} | i.e., each representation shall   |
   |          |                     | have the same Study Instance UID. |
   +----------+---------------------+-----------------------------------+

.. _sect_10.5.1.2:

Query Parameters
^^^^^^^^^^^^^^^^

The Store transaction has no Query Parameters.

.. _sect_10.5.1.3:

Request Header Fields
^^^^^^^^^^^^^^^^^^^^^

The origin server shall support Header Fields as required in
`table_title <#table_10.5.1-2>`__.

The user agent shall supply in the request Header Fields as required in
`table_title <#table_10.5.1-2>`__.

.. table:: Request Header Fields

   +---------------+------------+-------+-------------+---------------+
   | Name          | Values     | Usage | Description |               |
   +===============+============+=======+=============+===============+
   | Content-Type  | media-type | M     | M           | The DICOM     |
   |               |            |       |             | Media Type of |
   |               |            |       |             | the request   |
   |               |            |       |             | payload       |
   |               |            |       |             |               |
   |               |            |       |             | Shall be      |
   |               |            |       |             | present if    |
   |               |            |       |             | the request   |
   |               |            |       |             | has a payload |
   +---------------+------------+-------+-------------+---------------+
   | C             | uint       | C     | M           | Shall be      |
   | ontent-Length |            |       |             | present if a  |
   |               |            |       |             | content       |
   |               |            |       |             | encoding has  |
   |               |            |       |             | not been      |
   |               |            |       |             | applied to    |
   |               |            |       |             | the payload   |
   +---------------+------------+-------+-------------+---------------+
   | Con           | encoding   | C     | M           | Shall be      |
   | tent-Encoding |            |       |             | present if a  |
   |               |            |       |             | content       |
   |               |            |       |             | encoding has  |
   |               |            |       |             | been applied  |
   |               |            |       |             | to the        |
   |               |            |       |             | payload       |
   +---------------+------------+-------+-------------+---------------+

See also `Header Fields <#sect_8.4>`__.

.. _sect_10.5.1.4:

Request Payload
^^^^^^^^^^^^^^^

The request payload shall be present and shall contain one or more
representations specified by the Content-Type header field.

The payload may contain Instances from more than one Study if the Study
Instance UID is not specified in the Target URI.

The request payload shall consist of either:

-  SOP Instances, or

-  Metadata accompanied by Bulkdata.

binary instances shall be encoded with one message part per DICOM
Instance.

Metadata and Bulkdata requests will be encoded in the following manner
(see `figure_title <#figure_8.6-1>`__):

-  All XML request messages shall be encoded as described in the Native
   DICOM Model defined in with one message part per XML object; the
   Attributes of the Image Pixel Description Macro may be omitted for
   the media types specified in `table_title <#table_10.5.2-1>`__.

-  All JSON request messages shall be encoded as an array of DICOM JSON
   Model Objects defined in `DICOM JSON Model <#chapter_F>`__ in a
   single message part; the Attributes of the Image Pixel Description
   Macro may be omitted for the media types specified in
   `table_title <#table_10.5.2-1>`__.

-  Bulkdata (with the exception of Encapsulated Document (0042,0011)
   element) and uncompressed pixel data shall be encoded in a
   Little-Endian format using the application/octet-stream media type
   with one message part per Bulkdata item.

-  Compressed pixel data shall be encoded in one of two ways:

   -  single-frame pixel data encoded using a single-frame media type
      (one message part);

   -  multi-frame or video pixel data encoded using a multi-frame media
      type (multiple frames in one message part).

Uncompressed Bulkdata shall be encoded as application/octet-stream.

An Encapsulated Document (0042,0011) Bulkdata element shall be encoded
using the media-type from the MIME Type of the Encapsulated Document
(0042,0012) Attribute with one message part per document.

.. _sect_10.5.2:

Behavior
~~~~~~~~

The origin server stores Instances from the representations contained in
the request payload.

The stored Instance(s) shall fully conform to the IOD and encoding
requirements of and , respectively.

This Transaction stores one or more new Instances, and adds them to new
or existing Series and Studies.

While creating resources from the representations, the origin server may
coerce or replace the values of data elements. For example, Patient
Name, Patient ID, and Accession Number might be coerced when importing
media from an external institution, reconciling the Instances against a
master patient index, or reconciling them against an imaging procedure
order. The origin server may also fix incorrect values, such as Patient
Name or Patient ID; for example, because an incorrect work list item was
chosen, or an operator input error has occurred.

If any Attribute is coerced or corrected, the Original Attribute
Sequence (0400,0561) shall be included in the DICOM Object that is
stored and may be included in the Store Instances Response Module (see
`Store Instances Response Module <#chapter_I>`__) in the response.

.. note::

   For more information on populating the Original Attribute Sequence
   see .

The origin server shall encapsulate or convert any compressed pixel data
received as Bulkdata into an appropriate DICOM Transfer Syntax, as
defined in `table_title <#table_10.5.2-1>`__.

If the request message contains compressed Bulkdata with a Content Type
that is one of the media types specified in
`table_title <#table_10.5.2-1>`__, the request may omit the Image Pixel
Description Macro Attributes and the origin server will derive them from
the compressed octet stream. Some media types do not directly correspond
to a DICOM Transfer Syntax and the origin server will transform the
received bit stream into an uncompressed or lossless (reversibly)
compressed Transfer Syntax.

.. note::

   1. This allows a user agent to use consumer media types to encode the
      pixel data even though it may not have:

      -  the pixel data in a form that directly corresponds to a
         lossless (reversible) DICOM Transfer Syntax, or

      -  an API to access the information required to populate the Image
         Pixel Description Macro.

   2. If the supplied compressed bit stream is in a lossless
      (reversible) format, the intent is to allow full fidelity
      retrieval of the decompressed pixels, not the format in which it
      happened to be submitted.

The origin server shall encapsulate or convert any compressed pixel data
received as bulk data into an appropriate DICOM Transfer Syntax, as
defined in `table_title <#table_10.5.2-1>`__.

If the supplied compressed octet stream is in a lossy (irreversible)
format, there will be a corresponding DICOM Transfer Syntax, and the
origin server is not expected to recompress it causing further loss.
`table_title <#table_10.5.2-1>`__ contains a list of media types
containing compressed pixel data from which an origin server shall be
able to derive the Image Pixel Data Description Macro Attribute values.

Requirements are specified in `table_title <#table_10.5.2-1>`__ as
follows:

Transform
   No DICOM Transfer Syntax exists; shall be transformed by the origin
   server into an uncompressed or lossless compressed Transfer Syntax
   (the choice of which is at the discretion of the origin server).

Unchanged
   Shall be encapsulated in the corresponding DICOM Transfer Syntax
   without further lossy compression.

.. table:: Media Type Transformation to Transfer Syntaxes

   =========== ===========
   Media Type  Requirement
   =========== ===========
   image/gif   Transform
   Image/jp2   Unchanged
   image/jpeg  Unchanged
   image/jpx   Unchanged
   image/png   Transform
   video/mp4   Unchanged
   video/mpeg2 Unchanged
   =========== ===========

.. note::

   1. In the case of pixel data supplied as image/gif or image/png, the
      origin server may transform the color representation from indexed
      color to true color (RGB) as necessary to conform to any
      Photometric Interpretation constraints specified by the IOD (i.e.,
      if PALETTE COLOR is not permitted) ; such a transformation is
      considered lossless.

   2. If the number of bits per channel of an image/png file is not
      supported by the IOD, a lossless transformation cannot be
      performed.

   3. An animated image/gif will be converted into a multi-frame image
      by transforming the frame deltas into fully decoded frames;
      image/png does not support animation, and Multiple-image Network
      Graphics (MNG) is not included in
      `table_title <#table_10.5.2-1>`__.

   4. Any transparency information present in an image/gif or image/png
      file will be discarded, since DICOM does not support the concept
      of transparency. The actual pixel value used to replace
      transparent pixels (e.g., black or white) is at the discretion of
      the implementation, but if the value used does not appear
      elsewhere in the image, it may be useful to record it in Pixel
      Padding Value (0028,0120).

   5. If an alpha channel is supplied in an image/png file, the alpha
      channel will be discarded (i.e., considered to consist of all
      opaque values, consistent with the policy of discarding any
      transparency information).

   6. In the case of pixel data that contains a single channel in the
      absence of metadata describing the interpretation of the pixel
      values, the Photometric Interpretation may be assumed by the
      origin server to be MONOCHROME2 (zero is interpreted as black).

.. _sect_10.5.3:

Response
~~~~~~~~

The response shall have the following syntax:

::

   version SP status-code SP reason-phrase CRLF

::

   [Content-Type: media-type CRLF]

::

   [(Content-Length: uint CRLF / Content-Encoding: encoding CRLF) ]

::

   *(header-field CRLF)

::

   CRLF

::

   store-instances-response-module

The response shall contain an appropriate status code.

If any element is coerced or corrected, the Original Attribute Sequence
(0400,0561) shall be included in the DICOM Object that is stored and may
be included in the Store Instances Response Module (see `Store Instances
Response Module <#chapter_I>`__) in the response.

.. _sect_10.5.3.1:

Status Codes
^^^^^^^^^^^^

`table_title <#table_10.5.3-1>`__ shows some common status codes
corresponding to this transaction. See also `Status Codes <#sect_8.5>`__
for additional status codes.

.. table:: Status Code Meaning

   +----------------------+----------------------+----------------------+
   | Status               | Code                 | Description          |
   +======================+======================+======================+
   | Success              | 200 (OK)             | The origin server    |
   |                      |                      | successfully stored  |
   |                      |                      | all Instances.       |
   +----------------------+----------------------+----------------------+
   | 202 (Accepted)       | The origin server    |                      |
   |                      | stored some of the   |                      |
   |                      | Instances but        |                      |
   |                      | warnings or failures |                      |
   |                      | exist for others.    |                      |
   |                      |                      |                      |
   |                      | Additional           |                      |
   |                      | information          |                      |
   |                      | regarding this error |                      |
   |                      | may be found in the  |                      |
   |                      | response message     |                      |
   |                      | body.                |                      |
   +----------------------+----------------------+----------------------+
   | Failure              | 400 (Bad Request)    | The origin server    |
   |                      |                      | was unable to store  |
   |                      |                      | any instances due to |
   |                      |                      | bad syntax.          |
   +----------------------+----------------------+----------------------+
   | 409 (Conflict)       | The request was      |                      |
   |                      | formed correctly but |                      |
   |                      | the origin server    |                      |
   |                      | was unable to store  |                      |
   |                      | any instances due to |                      |
   |                      | a conflict in the    |                      |
   |                      | request (e.g.,       |                      |
   |                      | unsupported SOP      |                      |
   |                      | Class or Study       |                      |
   |                      | Instance UID         |                      |
   |                      | mismatch).           |                      |
   |                      |                      |                      |
   |                      | This may also be     |                      |
   |                      | used to indicate     |                      |
   |                      | that the origin      |                      |
   |                      | server was unable to |                      |
   |                      | store any instances  |                      |
   |                      | for a mixture of     |                      |
   |                      | reasons.             |                      |
   |                      |                      |                      |
   |                      | Additional           |                      |
   |                      | information          |                      |
   |                      | regarding the        |                      |
   |                      | instance errors may  |                      |
   |                      | be found in the      |                      |
   |                      | payload.             |                      |
   +----------------------+----------------------+----------------------+
   | 415 (Unsupported     | The origin server    |                      |
   | Media Type)          | does not support the |                      |
   |                      | media type specified |                      |
   |                      | in the Content-Type  |                      |
   |                      | header field of the  |                      |
   |                      | request              |                      |
   +----------------------+----------------------+----------------------+

.. _sect_10.5.3.2:

Response Header Fields
^^^^^^^^^^^^^^^^^^^^^^

The origin server shall support header fields as required in
`table_title <#table_10.5.3-2>`__.

.. table:: Response Header Fields

   +-----------------+------------+-----------------+-----------------+
   | Name            | center     | Origin Server   | Description     |
   |                 |            | Usage           |                 |
   +=================+============+=================+=================+
   | Content-Type    | media-type | M               | The media type  |
   |                 |            |                 | of the response |
   |                 |            |                 | payload, if     |
   |                 |            |                 | present.        |
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
   | ontent-Location |            |                 | present if a    |
   |                 |            |                 | new resource    |
   |                 |            |                 | was created.    |
   |                 |            |                 | The value is    |
   |                 |            |                 | the URL of the  |
   |                 |            |                 | representation  |
   |                 |            |                 | contained in    |
   |                 |            |                 | the request     |
   |                 |            |                 | payload.        |
   |                 |            |                 |                 |
   |                 |            |                 | May be present  |
   |                 |            |                 | otherwise       |
   +-----------------+------------+-----------------+-----------------+
   | Location        | url        | C               | Shall be        |
   |                 |            |                 | present if a    |
   |                 |            |                 | new resource    |
   |                 |            |                 | was created.    |
   |                 |            |                 | The value is    |
   |                 |            |                 | the URL of the  |
   |                 |            |                 | created         |
   |                 |            |                 | resource.       |
   |                 |            |                 |                 |
   |                 |            |                 | May be present  |
   |                 |            |                 | otherwise       |
   +-----------------+------------+-----------------+-----------------+

All success responses shall also contain the Content Representation (see
`Content Representation Header Fields <#sect_8.4.2>`__) and Payload
header fields (see `Payload Header Fields <#sect_8.4.3>`__) with
appropriate values.

It is recommended that the text returned in the Warning header field
(see `biblioentry_title <#biblio_RFC_7234>`__ `Section
5.5 <http://tools.ietf.org/html/rfc7234#section-5.5>`__) contain a DICOM
Status Code (see and ) and descriptive reason. For example:

::

   Warning: A700 <service>: Out of memory

See also `Header Fields <#sect_8.4>`__.

.. _sect_10.5.3.3:

Response Payload
^^^^^^^^^^^^^^^^

A success response payload shall contain a Store Instances Response
Module. See `Store Instances Response Module <#chapter_I>`__.

A failure response payload may contain a Status Report describing any
failures, warnings, or other useful information.

.. _sect_10.5.4:

Media Types
~~~~~~~~~~~

The origin server shall support the default and required media types in
the media type category specified in `table_title <#table_10.5.4-1>`__.

.. table:: Default, Required, and Optional Media Types

   +----------------------------+----------+----------------------------+
   | Media Type                 | Usage    | Section                    |
   +============================+==========+============================+
   | application/dicom          | Required | `The application/dicom     |
   |                            |          | Media                      |
   |                            |          | Type <#sect_8.7.3.1>`__    |
   +----------------------------+----------+----------------------------+
   | application/dicom+json     | Default  | `DICOM Metadata Media      |
   |                            |          | Types <#sect_8.7.3.2>`__   |
   +----------------------------+----------+----------------------------+
   | multipart/related;         | Required | `DICOM Metadata Media      |
   | ty                         |          | Types <#sect_8.7.3.2>`__   |
   | pe="application/dicom+xml" |          |                            |
   +----------------------------+----------+----------------------------+
   | multipart/related;         | Required | `DICOM Bulkdata Media      |
   | type=                      |          | Types <#sect_8.7.3.3>`__   |
   | "application/octet-stream" |          |                            |
   +----------------------------+----------+----------------------------+

.. _sect_10.5.5:

Conformance Statement
~~~~~~~~~~~~~~~~~~~~~

An implementation conforming to the Store transaction shall support the
resources and media types specified in `Store
Transaction <#sect_10.5>`__.

An implementation shall declare in its Conformance Statement the SOP
Classes supported for the Store transaction, and whether it plays the
role of origin server or user agent, or both.

Implementation specific warning and error codes shall be included in the
Conformance Statement.

.. _sect_10.6:

Search Transaction
------------------

This Transaction uses the GET method to Search for Studies, Series, and
Instances managed by the origin server.

.. _sect_10.6.1:

Request
~~~~~~~

The request shall have the following syntax:

::

   GET SP "/" {/resource} {?search*} SP version CRLF

::

   Accept: 1#search-media-type CRLF

::

   *(header-field CRLF)

::

   CRLF

Where

::

   search-media-type =multipart/related; type="application/dicom+xml"/ dicom-json

.. _sect_10.6.1.1:

Target Resources
^^^^^^^^^^^^^^^^

The Target Resource Path component of the Target URI specifies the
collection of resources that is the target of the search.

An origin server that is a native implementation shall support all
Mandatory (M) resources specified in the Native column in
`table_title <#table_10.6.1-1>`__.

An origin server that is a DIMSE Proxy implementation shall support all
Mandatory (M) resources specified in the Proxy column in
`table_title <#table_10.6.1-1>`__.

.. table:: Search Transaction Resources

   +----------------+----------------+--------+-------+--------------+
   | Resource       | URI Template   | Native | Proxy | Query Type   |
   +================+================+========+=======+==============+
   | All Studies    | ::             | M      | M     | hierarchical |
   |                |                |        |       |              |
   |                |    /stu        |        |       |              |
   |                | dies{?search*} |        |       |              |
   +----------------+----------------+--------+-------+--------------+
   | Study's Series | ::             | M      | M     | hierarchical |
   |                |                |        |       |              |
   |                |    /stud       |        |       |              |
   |                | ies/{study}/se |        |       |              |
   |                | ries{?search*} |        |       |              |
   +----------------+----------------+--------+-------+--------------+
   | Study's        | ::             | M      | O     | relational   |
   | Instances      |                |        |       |              |
   |                |    /studies    |        |       |              |
   |                | /{study}/insta |        |       |              |
   |                | nces{?search*} |        |       |              |
   +----------------+----------------+--------+-------+--------------+
   | All Series     | ::             | M      | O     | relational   |
   |                |                |        |       |              |
   |                |    /serie      |        |       |              |
   |                | s{?parameter*} |        |       |              |
   +----------------+----------------+--------+-------+--------------+
   | Study's        | ::             | M      | M     | hierarchical |
   | Series'        |                |        |       |              |
   | Instances      |    /studies/{  |        |       |              |
   |                | study}/series/ |        |       |              |
   |                | {series}/insta |        |       |              |
   |                | nces{?search*} |        |       |              |
   +----------------+----------------+--------+-------+--------------+
   | All Instances  | ::             | M      | O     | relational   |
   |                |                |        |       |              |
   |                |    /insta      |        |       |              |
   |                | nces{?search*} |        |       |              |
   +----------------+----------------+--------+-------+--------------+

For more information about Hierarchical Queries see . For more
information about Relational Queries see and .

`table_title <#table_10.6.1-2>`__ shows the resources supported by the
Search transaction along with a description of the search performed and
the results returned.

.. table:: Search Resource Descriptions

   +-------------------------+-------------------------------------------+
   | Resource                | Description                               |
   +=========================+===========================================+
   | All Studies             | Searches the entire service for Studies   |
   |                         | that match the search parameters, and     |
   |                         | returns a list of matching Studies,       |
   |                         | including the default and requested       |
   |                         | Attributes that are supported for each    |
   |                         | Study.                                    |
   +-------------------------+-------------------------------------------+
   | Study's Series          | Searches for all Series in the specified  |
   |                         | Study that match the search parameters,   |
   |                         | and returns a list of matching Series,    |
   |                         | including the default and requested       |
   |                         | Attributes that are supported for each    |
   |                         | Series.                                   |
   +-------------------------+-------------------------------------------+
   | Study's Instances       | Searches for all Instances in the         |
   |                         | specified Study that match the search     |
   |                         | parameters, and returns a list of         |
   |                         | matching Instances, including the default |
   |                         | and requested Attributes that are         |
   |                         | supported for each Instance.              |
   +-------------------------+-------------------------------------------+
   | All Series              | Searches the entire service for Series    |
   |                         | that match the search parameters, and     |
   |                         | returns a list of matching Series,        |
   |                         | including the default and requested       |
   |                         | Attributes that are supported for each    |
   |                         | Series.                                   |
   +-------------------------+-------------------------------------------+
   | Study Series' Instances | Searches for all Instances in the         |
   |                         | specified Study and Series that match the |
   |                         | search parameters, and returns a list of  |
   |                         | matching Instances, including the default |
   |                         | and requested Attributes that are         |
   |                         | supported for each Series.                |
   +-------------------------+-------------------------------------------+
   | All Instances           | Searches the entire service for Instances |
   |                         | that match the search parameters, and     |
   |                         | returns a list of matching Instances,     |
   |                         | including the default and requested       |
   |                         | Attributes that are supported for each    |
   |                         | Series.                                   |
   +-------------------------+-------------------------------------------+

.. _sect_10.6.1.2:

Query Parameters
^^^^^^^^^^^^^^^^

The origin server shall support Query Parameters as required in
`table_title <#table_8.3.4-1>`__ for the corresponding Resource
Categories.

The origin server shall support Query Parameters as required in
`table_title <#table_8.3.4-1>`__ for the supported Resource Categories.

.. _sect_10.6.1.2.1:

Attribute/Value Pair Requirements
'''''''''''''''''''''''''''''''''

DICOM Attribute/Value pairs included as Query Parameters in the request
shall satisfy the requirements in `Attribute
Matching <#sect_8.3.4.1>`__.

The user agent may include the following Attributes in the request:

-  Patient IE Attributes (see `Required Matching
   Attributes <#sect_10.6.1.2.3>`__)

-  Study IE Attributes (only allowed if the resource is All Studies, All
   Series, All Instances)

-  Series IE Attributes (only allowed if the resource is Study's Series,
   All Series, Study's Instances, or All Instances)

-  Composite Instance IE Attributes (only allowed if the resource is
   Study's Instances, Study Series' Instances, or All Instances)

-  Additional Query/Retrieve Attributes (see )

-  Private Data Element Tags and their corresponding Private Creator
   Element Tags

-  Timezone Offset From UTC (0008,0201)

The following are examples of Search URIs with valid Attribute/value
pairs:

::

   /studies?PatientID=11235813

::

   /studies?PatientID=11235813&StudyDate=20130509

::

   /studies?00100010=SMITH*&00101002.00100020=11235813&limit=25

::

   /studies?00100010=SMITH*&OtherPatientIDsSequence.00100020=11235813

::

   /studies?PatientID=11235813&includefield=00081048,00081049,00081060

::

   /studies?PatientID=11235813&includefield=00081048&includefield=00081049&includefield=00081060

::

   /studies?PatientID=11235813&StudyDate=20130509-20130510

::

   /studies?StudyInstanceUID=1.2.392.200036.9116.2.2.2.2162893313.1029997326.94587,1.2.392.200036.9116.2.2.2.2162893313.1029997326.94583

::

   /studies?00230010=AcmeCompany&includefield=00231002&includefield=00231003

::

   /studies?00230010=AcmeCompany&00231001=001239&includefield=00231002&includefield=00231003

.. _sect_10.6.1.2.2:

Search Key Types and Requirements
'''''''''''''''''''''''''''''''''

`table_title <#table_10.6.1-3>`__ defines the Search Key Types and their
requirements.

.. table:: Search Key Types

   ==== =======================
   Type Requirement
   ==== =======================
   U    Unique and Required Key
   R    Required Key
   C    Conditional Key
   O    Optional Key
   ==== =======================

.. _sect_10.6.1.2.3:

Required Matching Attributes
''''''''''''''''''''''''''''

The origin server shall support the IE Levels specified in
`table_title <#table_10.6.1-4>`__.

.. table:: Required IE Levels by Resource

   ======================= ======== = =
   Resource                IE Level   
   ======================= ======== = =
   All Studies             X          
   Study's Series                   X 
   Study's Instances                X X
   All Series              X        X 
   Study Series' Instances            X
   All Instances           X        X X
   ======================= ======== = =

The origin server shall support the matching Attributes specified in
`table_title <#table_10.6.1-5>`__ for each supported IE Level.

.. table:: Required Matching Attributes

   =================================== ============== ===========
   IE Level                            Attribute Name Tag
   =================================== ============== ===========
   Study                               Study Date     (0008,0020)
   Study Time                          (0008,0030)    
   Accession Number                    (0008,0050)    
   Modalities In Study                 (0008,0061)    
   Referring Physician Name            (0008,0090)    
   Patient Name                        (0010,0010)    
   Patient ID                          (0010,0020)    
   Study Instance UID                  (0020,000D)    
   Study ID                            (0020,0010)    
   Series                              Modality       (0008,0060)
   Series Instance UID                 (0020,000E)    
   Series Number                       (0020,0011)    
   Performed Procedure Step Start Date (0040,0244)    
   Performed Procedure Step Start Time (0040,0245)    
   Request Attributes Sequence         (0040,0275)    
   >Scheduled Procedure Step ID        (0040,0009)    
   >Requested Procedure ID             (0040,1001)    
   Instance                            SOP Class UID  (0008,0016)
   SOP Instance UID                    (0008,0018)    
   Instance Number                     (0020,0013)    
   =================================== ============== ===========

.. note::

   While some of the Data Elements in `table_title <#table_10.6.1-5>`__
   in are optional in , the above list is consistent with those required
   for IHE RAD-14. See `biblioentry_title <#biblio_IHE_RAD_TF_Vol2>`__
   Table 4.14-1.

.. _sect_10.6.1.3:

Request Header Fields
^^^^^^^^^^^^^^^^^^^^^

The origin server shall support header fields as required in
`table_title <#table_10.6.1-6>`__ in the request.

The user agent shall supply in the request header fields as required in
`table_title <#table_10.6.1-6>`__.

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
   | A             | charset    | O     | M           | The           |
   | ccept-Charset |            |       |             | Acceptable    |
   |               |            |       |             | Character     |
   |               |            |       |             | Sets of the   |
   |               |            |       |             | response      |
   |               |            |       |             | payload       |
   +---------------+------------+-------+-------------+---------------+

See also `Header Fields <#sect_8.4>`__.

.. _sect_10.6.1.4:

Request Payload
^^^^^^^^^^^^^^^

The request has no payload.

.. _sect_10.6.2:

Behavior
~~~~~~~~

The origin server shall perform the search indicated by the request,
using the matching rules in `Search Query Parameters <#sect_8.3.4>`__.

.. _sect_10.6.3:

Response
~~~~~~~~

The response shall have the following syntax:

::

   version SP status-code SP reason-phrase CRLF

::

   [Content-Type: media-type CRLF]

::

   [Content-Location: url CRLF]

::

   [(Content-Length: uint / Content-Encoding: encoding) CRLF]

::

   *(header-field CRLF)

::

   CRLF

::

   [payload / status-report]

.. _sect_10.6.3.1:

Status Codes
^^^^^^^^^^^^

`table_title <#table_10.6.3-1>`__ shows some common status codes
corresponding to this transaction. See also `Status Codes <#sect_8.5>`__
for additional status codes.

.. table:: Status Code Meaning

   +----------------------+----------------------+----------------------+
   | Status               | Code                 | Meaning              |
   +======================+======================+======================+
   | Success              | 200 (OK)             | The search completed |
   |                      |                      | successfully, and    |
   |                      |                      | the results are      |
   |                      |                      | contained in the     |
   |                      |                      | payload. If there    |
   |                      |                      | are additional       |
   |                      |                      | results available or |
   |                      |                      | there are warnings   |
   |                      |                      | the Warning header   |
   |                      |                      | field shall contain  |
   |                      |                      | a URL referencing a  |
   |                      |                      | Search Status        |
   |                      |                      | report.              |
   +----------------------+----------------------+----------------------+
   | 204 (No Content)     | The search completed |                      |
   |                      | successfully, but    |                      |
   |                      | there were zero      |                      |
   |                      | results.             |                      |
   +----------------------+----------------------+----------------------+
   | Failure              | 400 (Bad Request)    | The was a problem    |
   |                      |                      | with the request.    |
   |                      |                      | For example, the     |
   |                      |                      | Query Parameter      |
   |                      |                      | syntax is incorrect. |
   +----------------------+----------------------+----------------------+
   | 413 (Payload Too     | The search was too   |                      |
   | Large)               | broad, and the body  |                      |
   |                      | of the response      |                      |
   |                      | should contain a     |                      |
   |                      | Status Report with   |                      |
   |                      | additional           |                      |
   |                      | information about    |                      |
   |                      | the failure.         |                      |
   +----------------------+----------------------+----------------------+

.. _sect_10.6.3.2:

Response Header Fields
^^^^^^^^^^^^^^^^^^^^^^

The origin server shall support header fields as required in
`table_title <#table_10.6.3-2>`__.

.. table:: Response Header Fields

   +-----------------+------------+-----------------+-----------------+
   | Name            | center     | Origin Server   | Description     |
   |                 |            | Usage           |                 |
   +=================+============+=================+=================+
   | Content-Type    | media-type | C               | The DICOM Media |
   |                 |            |                 | Type of the     |
   |                 |            |                 | response        |
   |                 |            |                 | payload         |
   |                 |            |                 |                 |
   |                 |            |                 | Shall be        |
   |                 |            |                 | present if the  |
   |                 |            |                 | response has a  |
   |                 |            |                 | payload         |
   +-----------------+------------+-----------------+-----------------+
   | Content-Length  | uint       | C               | Shall be        |
   |                 |            |                 | present if no   |
   |                 |            |                 | content coding  |
   |                 |            |                 | has been        |
   |                 |            |                 | applied to the  |
   |                 |            |                 | payload         |
   +-----------------+------------+-----------------+-----------------+
   | C               | encoding   | C               | Shall be        |
   | ontent-Encoding |            |                 | present if a    |
   |                 |            |                 | content         |
   |                 |            |                 | encoding has    |
   |                 |            |                 | been applied to |
   |                 |            |                 | the payload     |
   +-----------------+------------+-----------------+-----------------+

.. _sect_10.6.3.3:

Response Payload
^^^^^^^^^^^^^^^^

A success response shall contain a list of matching results in an
Acceptable Media Type. See `Rendered Media Types <#sect_8.7.4>`__.

A failure response payload may contain a Status Report describing any
failures, warnings, or other useful information.

.. _sect_10.6.3.3.1:

Study Resource
''''''''''''''

For each matching Study, the origin server response shall contain
Attributes in accordance with `table_title <#table_10.6.3-3>`__. The
"Type" column in the table below refers to the Query/Retrieve Attribute
Types defined in . The unique key for a Study resource Search response
is the Study Instance UID (0020,000D).

.. table:: Study Resource Search Response Payload

   +----------------------+-------------+------+----------------------+
   | Attribute Name       | Tag         | Type | Condition            |
   +======================+=============+======+======================+
   | Study Date           | (0008,0020) | R    |                      |
   +----------------------+-------------+------+----------------------+
   | Study Time           | (0008,0030) | R    |                      |
   +----------------------+-------------+------+----------------------+
   | Accession Number     | (0008,0050) | R    |                      |
   +----------------------+-------------+------+----------------------+
   | Instance             | (0008,0056) | C    | Shall be present if  |
   | Availability         |             |      | known                |
   +----------------------+-------------+------+----------------------+
   | Modalities in Study  | (0008,0061) | R    |                      |
   +----------------------+-------------+------+----------------------+
   | Referring            | (0008,0090) | R    |                      |
   | Physician's Name     |             |      |                      |
   +----------------------+-------------+------+----------------------+
   | Timezone Offset From | (0008,0201) | C    | Shall be present if  |
   | UTC                  |             |      | known                |
   +----------------------+-------------+------+----------------------+
   | Retrieve URL         | (0008,1190) | C    | Shall be present if  |
   |                      |             |      | the Instance is      |
   |                      |             |      | retrievable by the   |
   |                      |             |      | Retrieve transaction |
   +----------------------+-------------+------+----------------------+
   | Patient's Name       | (0010,0010) | R    |                      |
   +----------------------+-------------+------+----------------------+
   | Patient ID           | (0010,0020) | R    |                      |
   +----------------------+-------------+------+----------------------+
   | Patient's Birth Date | (0010,0030) | R    |                      |
   +----------------------+-------------+------+----------------------+
   | Patient's Sex        | (0010,0040) | R    |                      |
   +----------------------+-------------+------+----------------------+
   | Study Instance UID   | (0020,000D) | U    |                      |
   +----------------------+-------------+------+----------------------+
   | Study ID             | (0020,0010) | R    |                      |
   +----------------------+-------------+------+----------------------+
   | Number of Study      | (0020,1206) | R    |                      |
   | Related Series       |             |      |                      |
   +----------------------+-------------+------+----------------------+
   | Number of Study      | (0020,1208) | R    |                      |
   | Related Instances    |             |      |                      |
   +----------------------+-------------+------+----------------------+

.. note::

   While some of the above Attributes are optional in , they are
   consistent with those required in
   `biblioentry_title <#biblio_IHE_RAD_TF_Vol2>`__ Table 4.14-1.

In addition, the response shall contain:

-  All other Study level Attributes passed as match or includefield
   parameters in the request that are supported by the origin server.

-  If the includefield parameter has been specified in the request, and
   its value is "all", all available Study Level Attributes.

-  If a Private Data Element has been specified as an include parameter
   and it is supported by the origin server, the Private Data Element
   and its corresponding Private Creator Element.

Series or Instance Level Attributes contained in includefield parameters
shall not be returned.

.. _sect_10.6.3.3.2:

Series Resources
''''''''''''''''

For each matching Series, the origin server shall return all Attributes
listed in `table_title <#table_10.6.3-4>`__. The "Type" column in the
table below refers to the Query/Retrieve Attribute Types defined in .
The unique key for a Series resource Search response is the Series
Instance UID (0020,000E).

.. table:: Series Resources Search Response Payload

   +----------------------+-------------+------+----------------------+
   | Attribute Name       | Tag         | Type | Condition            |
   +======================+=============+======+======================+
   | Modality             | (0008,0060) | R    |                      |
   +----------------------+-------------+------+----------------------+
   | Timezone Offset From | (0008,0201) | C    | Shall be present if  |
   | UTC                  |             |      | known                |
   +----------------------+-------------+------+----------------------+
   | Series Description   | (0008,103E) | C    | Shall be present if  |
   |                      |             |      | known                |
   +----------------------+-------------+------+----------------------+
   | Retrieve URL         | (0008,1190) | R    | Shall be present if  |
   |                      |             |      | the Instance is      |
   |                      |             |      | retrievable by the   |
   |                      |             |      | Retrieve transaction |
   +----------------------+-------------+------+----------------------+
   | Series Instance UID  | (0020,000E) | U    |                      |
   +----------------------+-------------+------+----------------------+
   | Series Number        | (0020,0011) | R    |                      |
   +----------------------+-------------+------+----------------------+
   | Number of Series     | (0020,1209) | R    |                      |
   | Related Instances    |             |      |                      |
   +----------------------+-------------+------+----------------------+
   | Performed Procedure  | (0040,0244) | C    | Shall be present if  |
   | Step Start Date      |             |      | known                |
   +----------------------+-------------+------+----------------------+
   | Performed Procedure  | (0040,0245) | C    | Shall be present if  |
   | Step Start Time      |             |      | known                |
   +----------------------+-------------+------+----------------------+
   | Request Attributes   | (0040,0275) | C    | Shall be present if  |
   | Sequence             |             |      | known                |
   +----------------------+-------------+------+----------------------+
   | >Scheduled Procedure | (0040,0009) | R    |                      |
   | Step ID              |             |      |                      |
   +----------------------+-------------+------+----------------------+
   | >Requested Procedure | (0040,1001) | R    |                      |
   | ID                   |             |      |                      |
   +----------------------+-------------+------+----------------------+

.. note::

   While some of the above Attributes in are optional in , they are
   consistent with the those required in
   `biblioentry_title <#biblio_IHE_RAD_TF_Vol2>`__ Table 4.14-1.

In addition, the response shall contain:

-  All other Series Level Attributes passed as match Query Parameters,
   or Series or Study Level Attributes passed as includefield parameters
   in the request that are supported by the origin server.

-  If the "includefield" parameter has been specified in the request and
   its value is "all", include all available Series Level Attributes.

-  If the Target Resource is All Series, then include all Study Level
   Attributes specified in `Study Resource <#sect_10.6.3.3.1>`__.

-  If a Private Data Element has been specified as an include parameter
   and it is supported by the origin server, the Private Data Element
   and its corresponding Private Creator Element.

Instance Level Attributes contained in includefield parameters shall not
be returned.

.. _sect_10.6.3.3.3:

Instance Resources
''''''''''''''''''

For each matching Instance, the origin server shall return all
Attributes listed in `table_title <#table_10.6.3-5>`__, if present in
the Instance. The Type column in the table below refers to the
Query/Retrieve Attribute Types defined in . The unique key for an
Instance resource search response is the SOP Instance UID (0008,0018).

.. table:: Instance Resources Search Response Payload

   +----------------------+-------------+------+----------------------+
   | Attribute Name       | Tag         | Type | Condition            |
   +======================+=============+======+======================+
   | SOP Class UID        | (0008,0016) | R    |                      |
   +----------------------+-------------+------+----------------------+
   | SOP Instance UID     | (0008,0018) | U    |                      |
   +----------------------+-------------+------+----------------------+
   | Instance             | (0008,0056) | C    | Shall be present if  |
   | Availability         |             |      | known                |
   +----------------------+-------------+------+----------------------+
   | Timezone Offset From | (0008,0201) | C    | Shall be present if  |
   | UTC                  |             |      | known                |
   +----------------------+-------------+------+----------------------+
   | Retrieve URL         | (0008,1190) | R    | Shall be present if  |
   |                      |             |      | the Instance is      |
   |                      |             |      | retrievable by the   |
   |                      |             |      | Retrieve transaction |
   +----------------------+-------------+------+----------------------+
   | Instance Number      | (0020,0013) | R    |                      |
   +----------------------+-------------+------+----------------------+
   | Rows                 | (0028,0010) | C    | Shall be present if  |
   |                      |             |      | known                |
   +----------------------+-------------+------+----------------------+
   | Columns              | (0028,0011) | C    | Shall be present if  |
   |                      |             |      | known                |
   +----------------------+-------------+------+----------------------+
   | Bits Allocated       | (0028,0100) | C    | Shall be present if  |
   |                      |             |      | known                |
   +----------------------+-------------+------+----------------------+
   | Number of Frames     | (0028,0008) | C    | Shall be present if  |
   |                      |             |      | known                |
   +----------------------+-------------+------+----------------------+

.. note::

   While some of the above Attributes in are optional in , they are
   consistent with the those required in
   `biblioentry_title <#biblio_IHE_RAD_TF_Vol2>`__ Table 4.14-1.

In addition, the response shall contain:

-  All other Instance Level Attributes passed as match parameters, or
   Study, Series, or Instance Level Attributes passed as includefield
   parameters that are supported by the origin server.

-  If the "includefield" parameter has been specified in the request and
   its value is "all", Attribute include all available Instance Level
   Attributes

-  If the Target Resource is All Instances, then include all Study level
   Attributes specified in `Study Resource <#sect_10.6.3.3.1>`__.

-  If the Target Resource is All Instances or Study's Instances, then
   include all Series level Attributes specified in `Series
   Resources <#sect_10.6.3.3.2>`__.

-  If a Private Data Element has been specified as an include parameter
   and it is supported by the origin server, the Private Data Element
   and its corresponding Private Creator Element.

The response may optionally include:

-  the Available Transfer Syntax UID (0008,3002) to describe the
   Transfer Syntaxes that the origin server can assure will be supported
   for retrieval of the SOP Instance. See .

.. _sect_10.6.4:

Media Types
~~~~~~~~~~~

The origin server shall support the default and required media types in
the media type category specified in `table_title <#table_10.6.4-1>`__.

.. table:: Default, Required, and Optional Media Types

   +----------------------------+----------+----------------------------+
   | Media Type                 | Usage    | Section                    |
   +============================+==========+============================+
   | application/dicom          | Required | `The application/dicom     |
   |                            |          | Media                      |
   |                            |          | Type <#sect_8.7.3.1>`__    |
   +----------------------------+----------+----------------------------+
   | application/dicom+json     | Default  | `DICOM Metadata Media      |
   |                            |          | Types <#sect_8.7.3.2>`__   |
   +----------------------------+----------+----------------------------+
   | multipart/related;         | Required | `DICOM Metadata Media      |
   | ty                         |          | Types <#sect_8.7.3.2>`__   |
   | pe="application/dicom+xml" |          |                            |
   +----------------------------+----------+----------------------------+
   | multipart/related;         | Required | `DICOM Bulkdata Media      |
   | type=                      |          | Types <#sect_8.7.3.3>`__   |
   | "application/octet-stream" |          |                            |
   +----------------------------+----------+----------------------------+

.. _sect_10.6.5:

Conformance Statement
~~~~~~~~~~~~~~~~~~~~~

An implementation shall declare in its Conformance Statement whether it
plays the role of origin server or user agent, or both.

An implementation playing the role of origin server shall declare the
maximum number of matches supported for a single query.

An implementation playing the role of origin server shall declare its
support for the following in its Conformance Statement:

-  Whether it is a native or proxy implementation

-  Fuzzy Matching

-  Optional resources supported

-  Optional Attributes supported

