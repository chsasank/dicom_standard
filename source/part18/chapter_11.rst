.. _chapter_11:

Worklist Service and Resources
==============================

.. _sect_11.1:

Overview
--------

The Worklist Service, also known as UPS-RS, defines a RESTful interface
to the Unified Procedure Step Service SOP Classes defined in and , in
which UPS behavior is specified.

The Worklist Service manages a single Worklist containing one or more
Workitems. Each Workitem represents a procedure step. User agents and
origin servers can create, retrieve, update, search for, and change the
state of Workitems. See for an overview of Worklists and Workitems (UPS
Instances).

.. _sect_11.1.1:

Resource Description
~~~~~~~~~~~~~~~~~~~~

There are three resources defined by this service:

+--------------+------------------------------------------------------+
| worklist     | A collection of Workitems managed by the origin      |
|              | server.                                              |
+--------------+------------------------------------------------------+
| workitem     | A dataset containing the Attributes specified in .   |
+--------------+------------------------------------------------------+
| subscription | A resource that specifies a Subscriber, to whom      |
|              | notifications about changes in the resource's state  |
|              | should be sent.                                      |
+--------------+------------------------------------------------------+

In the Worklist Service, the Workitem is identified by a Workitem UID,
which corresponds to the Affected SOP Instance UID and Requested SOP
Instance UID used in the UPS Service.

The following URI Template variables are used in the definitions of the
resources throughout `Worklist Service and Resources <#chapter_11>`__.

========== =============================================
{workitem} the Workitem UID.
{aetitle}  The Application Entity Title of a Subscriber.
========== =============================================

The Worklist Service manages a UPS Worklist and its Workitems. The URI
Templates defined by this service are specified in
`table_title <#table_11.1.1-1>`__.

.. table:: Resources, URI Templates and Descriptions

   +----------------------+----------------------+----------------------+
   | Resource             | URI Template         | Description          |
   +======================+======================+======================+
   | Worklist             | /                    | The Base URI of the  |
   |                      |                      | Worklist Service. A  |
   |                      |                      | Worklist contains    |
   |                      |                      | and manages a        |
   |                      |                      | collection of        |
   |                      |                      | Workitems. There is  |
   |                      |                      | only one Worklist    |
   |                      |                      | per service.         |
   +----------------------+----------------------+----------------------+
   | All Workitems        | /workitems           | The Workitems        |
   |                      |                      | resource contains    |
   |                      |                      | the entire           |
   |                      |                      | collection of        |
   |                      |                      | workitems in the     |
   |                      |                      | Worklist.            |
   +----------------------+----------------------+----------------------+
   | Workitem             | /                    | The Workitem         |
   |                      | workitems/{workitem} | resource contains a  |
   |                      |                      | single Workitem.     |
   +----------------------+----------------------+----------------------+
   | Workitem State       | /workit              | The Workitem State   |
   |                      | ems/{workitem}/state | resource is used to  |
   |                      |                      | change the state of  |
   |                      |                      | a Workitem.          |
   +----------------------+----------------------+----------------------+
   | Workitem Request     | /workitems/{wor      | The Workitem Cancel  |
   | Cancellation         | kitem}/cancelrequest | resource is used to  |
   |                      |                      | request the          |
   |                      |                      | cancellation of a    |
   |                      |                      | Workitem.            |
   +----------------------+----------------------+----------------------+
   | Workitem             | /wo                  | The Subscription to  |
   | Subscription         | rkitems/{workitem}/s | a Workitem.          |
   |                      | ubscribers/{aetitle} |                      |
   +----------------------+----------------------+----------------------+
   | Worklist             | /workitems/1.2.84    | The Workitem         |
   | Subscription         | 0.10008.5.1.4.34.5/s | Subscription         |
   |                      | ubscribers/{aetitle} | resource contains a  |
   |                      |                      | Subscription to the  |
   |                      |                      | Worklist             |
   +----------------------+----------------------+----------------------+
   | Filtered Worklist    | /workitems/1.2.840.  | The Workitem         |
   | Subscription         | 10008.5.1.4.34.5.1/s | Subscribers resource |
   |                      | ubscribers/{aetitle} | contains a single    |
   |                      |                      | Worklist Subscriber. |
   +----------------------+----------------------+----------------------+

.. _sect_11.1.1.1:

Workitems
^^^^^^^^^

A Workitem is what is referred to in as a procedure step.

Workitems represent a variety of steps such as: Image Processing,
Quality Control, Computer Aided Detection, Interpretation,
Transcription, Report Verification, or Printing. The steps may or may
not be formally scheduled.

.. _sect_11.1.1.2:

Web Services and DIMSE Terminology
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

.. table:: Correspondence between RESTful and DIMSE Terminology

   ======================= ==============================
   RESTful Term            DIMSE Term
   ======================= ==============================
   Worklist                Worklist
   Workitem                UPS Instance
   Deletion Lock           Deletion Lock
   Filter                  Matching Keys
   Matching Key            Matching Key
   Subscribe               Subscribe
   Unsubscribe             Unsubscribe
   Subscription            Subscription
   Subscription Generator  Worklist Subscription
                           
                           Filtered Worklist Subscription
   Subscriber              Subscriber
   Suspend Subscription    Suspend Worklist Subscription
   Notification Connection Association
   Transaction             N-GET, N-SET, N-ACTION
   Notification            N-EVENT-REPORT
   ======================= ==============================

.. _sect_11.1.2:

Common Query Parameters
~~~~~~~~~~~~~~~~~~~~~~~

The origin server shall support Query Parameters as required in
`table_title <#table_11.1.2-1>`__.

The user agent shall supply in the request Query Parameters as required
in `table_title <#table_11.1.2-1>`__.

.. table:: Common Query Parameters

   +----------------+------------+-------+---------+------------------+
   | Name           | Value      | Usage | Section |                  |
   +================+============+=======+=========+==================+
   | Accept         | media-type | M     | M       | `Accept Query    |
   |                |            |       |         | Parameter <#     |
   |                |            |       |         | sect_8.3.3.1>`__ |
   +----------------+------------+-------+---------+------------------+
   | Accept-Charset | charset    | O     | M       | `Character Set   |
   |                |            |       |         | Query            |
   |                |            |       |         | Parameter <#     |
   |                |            |       |         | sect_8.3.3.2>`__ |
   +----------------+------------+-------+---------+------------------+

See also `Header Fields <#sect_8.4>`__.

.. _sect_11.1.3:

Common Media Types
~~~~~~~~~~~~~~~~~~

The origin server shall support the media types listed as Default or
Required in `table_title <#table_11.1.3-1>`__.

.. table:: Default, Required, and Optional Media Types

   +----------------------------+----------+----------------------------+
   | Media Type                 | Usage    | Section                    |
   +============================+==========+============================+
   | application/dicom+json     | Default  | `DICOM Metadata Media      |
   |                            |          | Types <#sect_8.7.3.2>`__   |
   +----------------------------+----------+----------------------------+
   | multipart/related;         | Required | `DICOM Metadata Media      |
   | ty                         |          | Types <#sect_8.7.3.2>`__   |
   | pe="application/dicom+xml" |          |                            |
   +----------------------------+----------+----------------------------+

multipart/related; type="application/dicom+xml"; boundary={boundary}
   Specifies that the payload is a multipart message body where each
   part is a Native DICOM Model XML Infoset containing the appropriate
   Workitem Attributes. See .

application/dicom+json
   Specifies that the payload is a JSON array containing Workitems, and
   each Workitem contains the appropriate Attributes. SeeSection F.2.

The transactions shall not support Metadata or Bulkdata objects.

.. _sect_11.2:

Conformance
-----------

An origin server shall support sets of transactions of this service that
correspond to one or more UPS SOP Classes (DIMSE Service Groups). See .
Additional requirements for an origin server that is also a Unified
Worklist and Procedure Step SCP are described in .

A user agent or origin server implementing the Worklist Service shall
comply with all requirements placed on the SCU or SCP, respectively, for
the corresponding services in including Conformance Statement
requirements.

An implementation supporting the Worklist Service shall describe its
support in its Conformance Statement and in its response to the Retrieve
Capabilities transaction, and whether it plays the role of origin
server, user agent, or both.

.. _sect_11.3:

Transactions Overview
---------------------

The Worklist Service consists of the Transactions in
`table_title <#table_11.3-1>`__.

.. table:: Worklist Service Methods and Resource Templates

   +----------------+--------+---------+-------------+----------------+
   | Transaction    | Method | Payload | Description |                |
   +================+========+=========+=============+================+
   | Create         | POST   | dataset | none        | Creates a new  |
   |                |        |         |             | Workitem       |
   +----------------+--------+---------+-------------+----------------+
   | Retrieve       | GET    | none    | dataset     | Retrieves the  |
   |                |        |         |             | Target         |
   |                |        |         |             | Workitem       |
   +----------------+--------+---------+-------------+----------------+
   | Update         | POST   | dataset | none        | Updates the    |
   |                |        |         |             | Target         |
   |                |        |         |             | Workitem       |
   +----------------+--------+---------+-------------+----------------+
   | Change State   | PUT    | none    | none        | Changes the    |
   |                |        |         |             | state of the   |
   |                |        |         |             | Target         |
   |                |        |         |             | Workitem       |
   +----------------+--------+---------+-------------+----------------+
   | Request        | POST   | dataset | none        | Requests that  |
   | Cancellation   |        |         |             | the origin     |
   |                |        |         |             | server cancel  |
   |                |        |         |             | a Workitem     |
   +----------------+--------+---------+-------------+----------------+
   | Search         | GET    | none    | results     | Searches for   |
   |                |        |         |             | Workitems      |
   +----------------+--------+---------+-------------+----------------+
   | Subscribe      | POST   | none    | none        | Creates a      |
   |                |        |         |             | Subscription   |
   |                |        |         |             | to the Target  |
   |                |        |         |             | Worklist or    |
   |                |        |         |             | Target         |
   |                |        |         |             | Workitem       |
   +----------------+--------+---------+-------------+----------------+
   | Unsubscribe    | DELETE | none    | none        | Cancels a      |
   |                |        |         |             | Subscription   |
   |                |        |         |             | from the       |
   |                |        |         |             | Target         |
   |                |        |         |             | Worklist or    |
   |                |        |         |             | Target         |
   |                |        |         |             | Workitem       |
   +----------------+--------+---------+-------------+----------------+

The details of all state transition requirements can be found in .

The Request Cancellation transaction does not perform an actual state
transition, but it might cause a state transition.

When creating a new Workitem, to convey the Workitem UID that is to be
assigned, DIMSE uses the Affected SOP instance UID in the DIMSE header.
In the Web Services, the Workitem UID is included as a Query Parameter
to the Create request. All Attributes in the HTTP transaction payloads
are the same as those in the DIMSE payload.

.. _sect_11.4:

Create Workitem Transaction
---------------------------

This transaction creates a Workitem on the target Worklist. It
corresponds to the UPS DIMSE N-CREATE operation.

.. _sect_11.4.1:

Request
~~~~~~~

The request shall have the following syntax:

::

   POST SP /workitems ?{workitem} SP version CRLF

::

   Accept: dicom-media-type CRLF

::

   Content-Type: dicom-media-type CRLF

::

   (Content-Length: uint / Content-Encoding: encoding) CRLF

::

   *(header-field CRLF)

::

   CRLF

::

   Workitem

The user agent shall conform to the SCU behavior specified in .

.. _sect_11.4.1.1:

Target Resources
^^^^^^^^^^^^^^^^

The Target Resource is either the Worklist, or a Workitem.

.. table:: Create Transaction Resources

   ======== =====================
   Resource URI Template
   ======== =====================
   Worklist /workitems
   Workitem /workitems?{workitem}
   ======== =====================

If the Target Resource is the Worklist, then the Workitem dataset in the
payload shall contain the Workitem UID

The value of the workitem Query Parameter is the Workitem UID, which
corresponds to the Affected SOP Instance UID of the UPS DIMSE N-CREATE
operation.

.. _sect_11.4.1.2:

Query Parameters
^^^^^^^^^^^^^^^^

The origin server shall support Query Parameters as required in `Common
Query Parameters <#sect_11.1.2>`__.

The user agent shall supply in the request Query Parameters as required
in `Common Query Parameters <#sect_11.1.2>`__.

.. _sect_11.4.1.3:

Request Header Fields
^^^^^^^^^^^^^^^^^^^^^

The origin server shall support header fields in
`table_title <#table_11.4.1-3>`__.

The user agent shall supply in the request header fields as defined in
`table_title <#table_11.4.1-3>`__.

.. table:: Request Header Fields

   +--------------+--------------+-------+-------------+--------------+
   | Name         | Values       | Usage | Description |              |
   +==============+==============+=======+=============+==============+
   | Content-Type | dico         | M     | M           | The          |
   |              | m-media-type |       |             | media-type   |
   |              |              |       |             | of the       |
   |              |              |       |             | payload      |
   +--------------+--------------+-------+-------------+--------------+
   | Co           | uint         | C     | M           | Shall be     |
   | ntent-Length |              |       |             | present if a |
   |              |              |       |             | content      |
   |              |              |       |             | encoding has |
   |              |              |       |             | not been     |
   |              |              |       |             | applied to   |
   |              |              |       |             | the payload  |
   +--------------+--------------+-------+-------------+--------------+
   | Cont         | encoding     | C     | M           | Shall be     |
   | ent-Encoding |              |       |             | present if a |
   |              |              |       |             | content      |
   |              |              |       |             | encoding has |
   |              |              |       |             | been applied |
   |              |              |       |             | to the       |
   |              |              |       |             | payload      |
   +--------------+--------------+-------+-------------+--------------+

See also `Header Fields <#sect_8.4>`__.

.. _sect_11.4.1.4:

Request Payload
^^^^^^^^^^^^^^^

The payload shall have a single part, containing a Workitem encoded in
the media type specified in the Content-Type header field. The payload
shall contain all data elements to be stored. The Affected SOP Instance
UID shall not be present in the Workitem dataset.

The Workitem in the payload shall comply with all Instance requirements
in the Req. Type N-CREATE column of .

.. _sect_11.4.2:

Behavior
~~~~~~~~

The origin server shall create a new Workitem in the SCHEDULED state and
return a URL referencing the newly created Workitem in the Location
header field of the response. A Workitem will only be added to the
Worklist once.

The origin server shall create and maintain the Workitem as specified by
the SCP behavior defined in .

.. _sect_11.4.3:

Response
~~~~~~~~

The response shall have the following syntax:

::

   version SP status-code SP reason-phrase CRLF

::

   Content-Location: representation CRLF

::

   Location: resource CRLF

::

   *(header-field CRLF)

::

   CRLF

::

   [status-report]

.. _sect_11.4.3.1:

Status Codes
^^^^^^^^^^^^

`table_title <#table_11.4.3-1>`__ shows some common status codes
corresponding to this transaction. See also `Status Codes <#sect_8.5>`__
for additional status codes.

.. table:: Status Code Meaning

   +----------------+-------------------------+-------------------------+
   | Status         | Code                    | Meaning                 |
   +================+=========================+=========================+
   | Success        | 201 (Created)           | The Target Workitem was |
   |                |                         | successfully added to   |
   |                |                         | the Worklist.           |
   +----------------+-------------------------+-------------------------+
   | Failure        | 400 (Bad Request)       | There was a problem     |
   |                |                         | with the request. For   |
   |                |                         | example, the request    |
   |                |                         | payload did not satisfy |
   |                |                         | the requirements of the |
   |                |                         | Req. Type N-CREATE      |
   |                |                         | column of .             |
   +----------------+-------------------------+-------------------------+
   | 409 (Conflict) | The Target Workitem     |                         |
   |                | already exists.         |                         |
   +----------------+-------------------------+-------------------------+

.. _sect_11.4.3.2:

Response Header Fields
^^^^^^^^^^^^^^^^^^^^^^

The origin server shall support header fields as required in
`table_title <#table_11.4.3-2>`__.

.. table:: Response Header Fields

   +-----------------+------------+-----------------+-----------------+
   | Names           | Value      | Origin Server   | Condition       |
   |                 |            | Usage           |                 |
   +=================+============+=================+=================+
   | Content-Type    | media-type | C               | Shall be        |
   |                 |            |                 | present if the  |
   |                 |            |                 | response has a  |
   |                 |            |                 | payload         |
   +-----------------+------------+-----------------+-----------------+
   | Content-Length  | uint       | C               | Shall be        |
   |                 |            |                 | present if a    |
   |                 |            |                 | content coding  |
   |                 |            |                 | has not been    |
   |                 |            |                 | applied to the  |
   |                 |            |                 | payload         |
   +-----------------+------------+-----------------+-----------------+
   | C               | encoding   | C               | Shall be        |
   | ontent-Encoding |            |                 | present if      |
   |                 |            |                 | content         |
   |                 |            |                 | encoding has    |
   |                 |            |                 | been applied to |
   |                 |            |                 | the payload     |
   +-----------------+------------+-----------------+-----------------+
   | C               | url        | O               | Shall be        |
   | ontent-Location |            |                 | present if the  |
   |                 |            |                 | response has a  |
   |                 |            |                 | payload         |
   |                 |            |                 | containing a    |
   |                 |            |                 | resource. See   |
   |                 |            |                 | `Payload Header |
   |                 |            |                 | Fields <#       |
   |                 |            |                 | sect_8.4.3>`__. |
   |                 |            |                 |                 |
   |                 |            |                 | May be present  |
   |                 |            |                 | otherwise       |
   +-----------------+------------+-----------------+-----------------+
   | Location        | url        | C               | A URL-reference |
   |                 |            |                 | to the created  |
   |                 |            |                 | Workitem.       |
   |                 |            |                 |                 |
   |                 |            |                 | Shall be        |
   |                 |            |                 | present if a    |
   |                 |            |                 | Workitem was    |
   |                 |            |                 | created.        |
   |                 |            |                 |                 |
   |                 |            |                 | May be present  |
   |                 |            |                 | if the payload  |
   |                 |            |                 | contains a      |
   |                 |            |                 | resource        |
   +-----------------+------------+-----------------+-----------------+
   | Warning         | See below  | C               | Shall be        |
   |                 |            |                 | present if the  |
   |                 |            |                 | Target Workitem |
   |                 |            |                 | was modified by |
   |                 |            |                 | the origin      |
   |                 |            |                 | server and      |
   |                 |            |                 | shall include   |
   |                 |            |                 | the warning     |
   |                 |            |                 | below           |
   +-----------------+------------+-----------------+-----------------+

If the Target Workitem was modified by the origin server, the response
shall also have the following Warning header:

::

   Warning: 299 <service>: The Workitem was created with modifications.CRLF

See also `Header Fields <#sect_8.4>`__.

.. _sect_11.4.3.3:

Response Payload
^^^^^^^^^^^^^^^^

A success response should have no payload.

A failure response payload may contain a Status Report describing any
failures, warnings, or other useful information.

.. _sect_11.5:

Retrieve Workitem Transaction
-----------------------------

This transaction retrieves a Workitem. It corresponds to the UPS DIMSE
N-GET operation.

.. note::

   The requirement for the origin server to respond to Retrieve Workitem
   requests for UPS Instances that have moved to the COMPLETED or
   CANCELED state is limited. See .

.. _sect_11.5.1:

Request
~~~~~~~

The request shall have the following syntax:

::

   GET SP /workitems/{workitem} SP version CRLF

::

   Accept dicom-media-type CRLF

::

   [Cache-Control: no-cache CRLF]

::

   *(header-field CRLF)

::

   CRLF

The user agent shall conform to the SCU behavior specified in .

.. _sect_11.5.1.1:

Target Resources
^^^^^^^^^^^^^^^^

The Target Resource of this transaction is a Workitem.

.. _sect_11.5.1.2:

Query Parameters
^^^^^^^^^^^^^^^^

The user agent shall supply, and the origin server shall support, the
Common Query Parameters in `Common Query Parameters <#sect_11.1.2>`__.

.. _sect_11.5.1.3:

Request Header Fields
^^^^^^^^^^^^^^^^^^^^^

The origin server shall support header fields as required in
`table_title <#table_11.5.1-1>`__.

The user agent shall supply in the request header fields as defined in
`table_title <#table_11.5.1-1>`__.

.. table:: Request Header Fields

   +--------+----------------+-------+-------------+----------------+
   | Name   | Values         | Usage | Description |                |
   +========+================+=======+=============+================+
   | Accept | 1#-di          | M     | M           | The Acceptable |
   |        | com-media-type |       |             | Media Types of |
   |        |                |       |             | the response   |
   |        |                |       |             | payload        |
   +--------+----------------+-------+-------------+----------------+

See also `Header Fields <#sect_8.4>`__.

.. _sect_11.5.1.4:

Request Payload
^^^^^^^^^^^^^^^

The request shall have no payload.

.. _sect_11.5.2:

Behavior
~~~~~~~~

If the Workitem exists on the origin server, the Workitem shall be
returned in an Acceptable Media Type (see `Rendered Media
Types <#sect_8.7.4>`__); however, the origin server may send a failure
response to requests for Workitems that have moved to the COMPLETED or
CANCELED state. See .

The returned Workitem shall not contain the Transaction UID (0008,1195)
Attribute. This is necessary to preserve this Attribute's role as an
access lock.

.. _sect_11.5.3:

Response
~~~~~~~~

The response shall have the following syntax:

::

   version SP status-code SP reason-phrase CRLF

::

   [Content-Type: dicom-media-type CRLF]

::

   [(Content-Length: uint / Content-Encoding: encoding) CRLF]

::

   [Content-Location: url CRLF]

::

   *(header-field CRLF)

::

   CRLF

::

   [workitem / status-report]

.. _sect_11.5.3.1:

Status Codes
^^^^^^^^^^^^

`table_title <#table_11.5.3-1>`__ shows some common status codes
corresponding to this transaction. See also `Status Codes <#sect_8.5>`__
for additional status codes.

.. table:: Status Code Meaning

   +-----------------+------------------------+------------------------+
   | Status          | Code                   | Meaning                |
   +=================+========================+========================+
   | Success         | 200 (OK)               | All Instances were     |
   |                 |                        | successfully           |
   |                 |                        | retrieved.             |
   +-----------------+------------------------+------------------------+
   | Failure         | 400 (Bad Request)      | There was a problem    |
   |                 |                        | with the request.      |
   +-----------------+------------------------+------------------------+
   | 404 (Not Found) | The origin server has  |                        |
   |                 | no knowledge of the    |                        |
   |                 | Target Workitem. See . |                        |
   +-----------------+------------------------+------------------------+
   | 409 (Conflict)  | The request cannot be  |                        |
   |                 | performed for one of   |                        |
   |                 | the following reasons: |                        |
   |                 |                        |                        |
   |                 | -  the submitted       |                        |
   |                 |    request is          |                        |
   |                 |    inconsistent with   |                        |
   |                 |    the current state   |                        |
   |                 |    of the Target       |                        |
   |                 |    Workitem            |                        |
   |                 |                        |                        |
   |                 | -  the Transaction UID |                        |
   |                 |    is missing          |                        |
   |                 |                        |                        |
   |                 | -  the Transaction UID |                        |
   |                 |    is incorrect        |                        |
   +-----------------+------------------------+------------------------+
   | 410 (Gone)      | The origin server      |                        |
   |                 | knows that the Target  |                        |
   |                 | Workitem did exist but |                        |
   |                 | has been deleted.      |                        |
   +-----------------+------------------------+------------------------+

.. _sect_11.5.3.2:

Response Header Fields
^^^^^^^^^^^^^^^^^^^^^^

The origin server shall support header fields as required in
`table_title <#table_11.5.3-2>`__.

.. table:: Response Header Fields

   +-----------------+------------+-----------------+-----------------+
   | Name            | center     | Origin Server   | Description     |
   |                 |            | Usage           |                 |
   +=================+============+=================+=================+
   | Content-Type    | media-type | M               | media type of   |
   |                 |            |                 | the Target      |
   |                 |            |                 | Workitem or     |
   |                 |            |                 | Status Report   |
   |                 |            |                 | in payload      |
   +-----------------+------------+-----------------+-----------------+
   | C               | url        | O               | Shall be        |
   | ontent-Location |            |                 | present if the  |
   |                 |            |                 | response has a  |
   |                 |            |                 | payload         |
   |                 |            |                 | containing a    |
   |                 |            |                 | resource. See   |
   |                 |            |                 | `Payload Header |
   |                 |            |                 | Fields <#       |
   |                 |            |                 | sect_8.4.3>`__. |
   |                 |            |                 |                 |
   |                 |            |                 | May be present  |
   |                 |            |                 | otherwise       |
   +-----------------+------------+-----------------+-----------------+
   | Content-Length  | uint       | C               | Shall be        |
   |                 |            |                 | present if no   |
   |                 |            |                 | content         |
   |                 |            |                 | encoding has    |
   |                 |            |                 | been applied to |
   |                 |            |                 | the payload     |
   +-----------------+------------+-----------------+-----------------+
   | C               | encoding   | C               | Shall be        |
   | ontent-Encoding |            |                 | present if a    |
   |                 |            |                 | content         |
   |                 |            |                 | encoding has    |
   |                 |            |                 | been applied to |
   |                 |            |                 | the payload     |
   +-----------------+------------+-----------------+-----------------+

See also `Header Fields <#sect_8.4>`__.

.. _sect_11.5.3.3:

Response Payload
^^^^^^^^^^^^^^^^

A success response has a single part payload containing the requested
Workitem in the Selected Media Type.

If the Workitem is in the IN PROGRESS state, the returned Workitem shall
not contain the Transaction UID (0008,1195) Attribute of the Workitem,
since that should only be known to the Owner.

A failure response payload may contain a Status Report describing any
failures, warnings, or other useful information.

.. _sect_11.6:

Update Workitem Transaction
---------------------------

This transaction modifies Attributes of an existing Workitem. It
corresponds to the UPS DIMSE N-SET operation.

.. _sect_11.6.1:

Request
~~~~~~~

The request shall have the following syntax:

::

   POST SP /workitems/{workitem}?{transaction-uid} SP version CRLF

::

   Content-Type: dicom-media-type CRLF

::

   (Content-Length: uint / Content-Encoding: encoding) CRLF

::

   Content-Location: url CRLF

::

   *(header-field CRLF)

::

   CRLF

::

   Payload

The user agent shall conform to the SCU behavior specified in .

.. _sect_11.6.1.1:

Target Resources
^^^^^^^^^^^^^^^^

The Target Resource for this transaction is a Workitem.

.. _sect_11.6.1.2:

Query Parameters
^^^^^^^^^^^^^^^^

The origin server and user agent shall supply the Common Query
Parameters in `Common Query Parameters <#sect_11.1.2>`__.

The origin server shall also supply the Transaction UID Query Parameter,
which specifies the Transaction UID of the Workitem to be updated.

.. _sect_11.6.1.3:

Request Header Fields
^^^^^^^^^^^^^^^^^^^^^

The origin server shall support header fields as required in
`table_title <#table_11.6.1-1>`__.

The user agent shall supply in the request header fields as defined in
`table_title <#table_11.6.1-1>`__.

.. table:: Request Header Fields

   +--------------+--------------+-------+-------------+--------------+
   | Name         | Values       | Usage | Description |              |
   +==============+==============+=======+=============+==============+
   | Content-Type | dico         | M     | M           | The          |
   |              | m-media-type |       |             | media-type   |
   |              |              |       |             | of the       |
   |              |              |       |             | payload      |
   +--------------+--------------+-------+-------------+--------------+
   | Co           | uint         | C     | M           | Shall be     |
   | ntent-Length |              |       |             | present if a |
   |              |              |       |             | content      |
   |              |              |       |             | encoding has |
   |              |              |       |             | not been     |
   |              |              |       |             | applied to   |
   |              |              |       |             | the payload  |
   +--------------+--------------+-------+-------------+--------------+
   | Cont         | encoding     | C     | M           | Shall be     |
   | ent-Encoding |              |       |             | present if a |
   |              |              |       |             | content      |
   |              |              |       |             | encoding has |
   |              |              |       |             | been applied |
   |              |              |       |             | to the       |
   |              |              |       |             | payload      |
   +--------------+--------------+-------+-------------+--------------+

See also `Header Fields <#sect_8.4>`__.

.. _sect_11.6.1.4:

Request Payload
^^^^^^^^^^^^^^^

The request payload contains a dataset with the changes to the target
Workitem. The dataset shall include all elements that are to be
modified. All modifications to the Workitem shall comply with all
requirements described in .

.. _sect_11.6.2:

Behavior
~~~~~~~~

The origin server shall modify the target Workitem as specified by the
request, and in a manner consistent with the SCP behavior specified in .

If the Workitem is in the COMPLETED or CANCELED state, the response
shall be a 400 (Bad Request) failure response.

.. _sect_11.6.3:

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

   [Content-Location: workitem CRLF

::

   *(header-field CRLF)

::

   CRLF

::

   [status-report]

.. _sect_11.6.3.1:

Status Codes
^^^^^^^^^^^^

The response shall contain an appropriate status code.

`table_title <#table_11.6.3-1>`__ shows some common status codes
corresponding to this transaction. See also `Status Codes <#sect_8.5>`__
for additional status codes.

.. table:: Status Code Meaning

   +-----------------+------------------------+------------------------+
   | Status          | Code                   | Meaning                |
   +=================+========================+========================+
   | Success         | 200 (OK)               | The Target Workitem    |
   |                 |                        | was updated.           |
   +-----------------+------------------------+------------------------+
   | Failure         | 400 (Bad Request)      | There was a problem    |
   |                 |                        | with the request. For  |
   |                 |                        | example:               |
   |                 |                        |                        |
   |                 |                        | -  the Target Workitem |
   |                 |                        |    was in the          |
   |                 |                        |    COMPLETED or        |
   |                 |                        |    CANCELED state      |
   |                 |                        |                        |
   |                 |                        | -  the Transaction UID |
   |                 |                        |    is missing          |
   |                 |                        |                        |
   |                 |                        | -  the Transaction UID |
   |                 |                        |    is incorrect, or    |
   |                 |                        |                        |
   |                 |                        | -  the dataset did not |
   |                 |                        |    conform to the      |
   |                 |                        |    requirements        |
   +-----------------+------------------------+------------------------+
   | 404 (Not Found) | The Target Workitem    |                        |
   |                 | was not found.         |                        |
   +-----------------+------------------------+------------------------+
   | 409 (Conflict)  | The request is         |                        |
   |                 | inconsistent with the  |                        |
   |                 | current state of the   |                        |
   |                 | Target Workitem        |                        |
   +-----------------+------------------------+------------------------+
   | 410 (Gone)      | The Target Workitem    |                        |
   |                 | once existed, but no   |                        |
   |                 | longer exists.         |                        |
   +-----------------+------------------------+------------------------+

.. _sect_11.6.3.2:

Response Header Fields
^^^^^^^^^^^^^^^^^^^^^^

The origin server shall support header fields as required in
`table_title <#table_11.6.3-2>`__.

.. table:: Response Header Fields

   +-----------------+------------+-----------------+-----------------+
   | Name            | center     | Origin Server   | Description     |
   |                 |            | Usage           |                 |
   +=================+============+=================+=================+
   | Content-Type    | media-type | M               | The media-type  |
   |                 |            |                 | of the payload  |
   +-----------------+------------+-----------------+-----------------+
   | Content-Length  | uint       | C               | Shall be        |
   |                 |            |                 | present if no   |
   |                 |            |                 | content         |
   |                 |            |                 | encoding has    |
   |                 |            |                 | been applied to |
   |                 |            |                 | the payload     |
   +-----------------+------------+-----------------+-----------------+
   | C               | encoding   | C               | Shall be        |
   | ontent-Encoding |            |                 | present if a    |
   |                 |            |                 | content         |
   |                 |            |                 | encoding has    |
   |                 |            |                 | been applied to |
   |                 |            |                 | the payload     |
   +-----------------+------------+-----------------+-----------------+
   | C               | url        | O               | Shall be        |
   | ontent-Location |            |                 | present if the  |
   |                 |            |                 | response has a  |
   |                 |            |                 | payload         |
   |                 |            |                 | containing a    |
   |                 |            |                 | resource. See   |
   |                 |            |                 | `Payload Header |
   |                 |            |                 | Fields <#       |
   |                 |            |                 | sect_8.4.3>`__. |
   |                 |            |                 |                 |
   |                 |            |                 | May be present  |
   |                 |            |                 | otherwise       |
   +-----------------+------------+-----------------+-----------------+
   | Warning         | see below  | O               | If the Target   |
   |                 |            |                 | Workitem was    |
   |                 |            |                 | modified by the |
   |                 |            |                 | origin server   |
   |                 |            |                 | shall include   |
   |                 |            |                 | one of the      |
   |                 |            |                 | Warning header  |
   |                 |            |                 | fields below.   |
   +-----------------+------------+-----------------+-----------------+

If the Workitem was successfully updated but with modifications made by
the origin server, the response shall include the following in the
Warning header field:

::

   Warning: 299 <service>: The Workitem was updated with modifications.

If optional Attributes were rejected, the response shall include the
following Warning header field:

::

   Warning: 299 <service>: Requested optional Attributes are not supported.

If the request was rejected with a failure status code, the response
shall include a Warning header field with one of following messages that
best describes the nature of the conflict:

::

   Warning: 299 <service>: The target URI did not reference a claimed Workitem.

::

   Warning: 299 <service>: The submitted request is inconsistent with the current state of the Workitem.

See also `Header Fields <#sect_8.4>`__.

.. _sect_11.6.3.3:

Response Payload
^^^^^^^^^^^^^^^^

A success response shall have either no payload, or a payload containing
a Status Report document.

A failure response payload may contain a Status Report describing any
failures, warnings, or other useful information.

.. _sect_11.7:

Change Workitem State
---------------------

This transaction is used to change the state of a Workitem. It
corresponds to the UPS DIMSE N-ACTION operation "Change UPS State".
State changes are used to claim ownership, complete, or cancel a
Workitem.

.. _sect_11.7.1:

Request
~~~~~~~

The request shall have the following syntax:

::

   PUT SP /workitems/{workitem}/state SP version CRLF

::

   Content-Type: dicom-media-type

::

   (Content-Length: uint / Content-Encoding: encoding) CRLF

::

   *(header-field CRLF)

::

   CRLF

::

   Payload

The user agent shall conform to the SCU behavior specified in .

.. _sect_11.7.1.1:

Target Resources
^^^^^^^^^^^^^^^^

The Target Resource for this transaction is a Workitem.

.. _sect_11.7.1.2:

Query Parameters
^^^^^^^^^^^^^^^^

The user agent shall supply, and the origin server shall support, the
Common Query Parameters in `Common Query Parameters <#sect_11.1.2>`__.

.. _sect_11.7.1.3:

Request Header Fields
^^^^^^^^^^^^^^^^^^^^^

The origin server shall support header fields as required in
`table_title <#table_11.7.1-1>`__.

The user agent shall supply in the request header fields as defined in
`table_title <#table_11.7.1-1>`__.

.. table:: Request Header Fields

   +--------------+--------------+-------+-------------+--------------+
   | Name         | Values       | Usage | Description |              |
   +==============+==============+=======+=============+==============+
   | Content-Type | dico         | M     | M           | The          |
   |              | m-media-type |       |             | Acceptable   |
   |              |              |       |             | Media Types  |
   |              |              |       |             | of the       |
   |              |              |       |             | response     |
   |              |              |       |             | payload      |
   +--------------+--------------+-------+-------------+--------------+
   | Co           | uint         | C     | M           | Shall be     |
   | ntent-Length |              |       |             | present if a |
   |              |              |       |             | content      |
   |              |              |       |             | encoding has |
   |              |              |       |             | not been     |
   |              |              |       |             | applied to   |
   |              |              |       |             | the payload  |
   +--------------+--------------+-------+-------------+--------------+
   | Cont         | encoding     | C     | M           | Shall be     |
   | ent-Encoding |              |       |             | present if a |
   |              |              |       |             | content      |
   |              |              |       |             | encoding has |
   |              |              |       |             | been applied |
   |              |              |       |             | to the       |
   |              |              |       |             | payload      |
   +--------------+--------------+-------+-------------+--------------+

See also `Header Fields <#sect_8.4>`__.

.. _sect_11.7.1.4:

Request Payload
^^^^^^^^^^^^^^^

The request payload shall contain the Change UPS State Data Elements as
specified in . These data elements are:

Transaction UID (0008,1195)
   The request payload shall include a Transaction UID. The user agent
   creates the Transaction UID when requesting a transition to the IN
   PROGRESS state for a given Workitem. The user agent provides that
   Transaction UID in subsequent transactions with that Workitem.

Procedure Step State (0074,1000)
   The legal values correspond to the requested state transition. They
   are: "IN PROGRESS", "COMPLETED", or "CANCELLED".

.. _sect_11.7.2:

Behavior
~~~~~~~~

The origin server shall support the state changes to the Workitem
specified in the request as described by the SCP behavior in .

.. _sect_11.7.3:

Response
~~~~~~~~

The response shall have the following syntax:

::

   version SP status-code SP reason-phrase CRLF

::

   [Content-Type: dicom-media-type CRLF]

::

   [(Content-Length: uint / Content-Encoding: encoding) CRLF]

::

   *(header-field CRLF) CRLF

::

   [status-report]

.. _sect_11.7.3.1:

Status Codes
^^^^^^^^^^^^

`table_title <#table_11.7.3-1>`__ shows some common status codes
corresponding to this transaction. See also `Status Codes <#sect_8.5>`__
for additional status codes.

.. table:: Status Code Meaning

   +-----------------+------------------------+------------------------+
   | Status          | Code                   | Meaning                |
   +=================+========================+========================+
   | Success         | 200 (OK)               | The update was         |
   |                 |                        | successful, and the    |
   |                 |                        | response payload       |
   |                 |                        | contains a Status      |
   |                 |                        | Report document.       |
   +-----------------+------------------------+------------------------+
   | Failure         | 400 (Bad Request)      | The request cannot be  |
   |                 |                        | performed for one of   |
   |                 |                        | the following reasons: |
   |                 |                        |                        |
   |                 |                        | -  the request is      |
   |                 |                        |    invalid given the   |
   |                 |                        |    current state of    |
   |                 |                        |    the Target Workitem |
   |                 |                        |                        |
   |                 |                        | -  the Transaction UID |
   |                 |                        |    is missing          |
   |                 |                        |                        |
   |                 |                        | -  the Transaction UID |
   |                 |                        |    is incorrect        |
   +-----------------+------------------------+------------------------+
   | 404 (Not Found) | The Target Workitem    |                        |
   |                 | was not found.         |                        |
   +-----------------+------------------------+------------------------+
   | 409 (Conflict)  | The request is         |                        |
   |                 | inconsistent with the  |                        |
   |                 | current state of the   |                        |
   |                 | Target Workitem        |                        |
   +-----------------+------------------------+------------------------+
   | 410 (Gone)      | The Target Workitem    |                        |
   |                 | once existed, but no   |                        |
   |                 | longer exists.         |                        |
   +-----------------+------------------------+------------------------+

.. _sect_11.7.3.2:

Response Header Fields
^^^^^^^^^^^^^^^^^^^^^^

The origin server shall support header fields as required in
`table_title <#table_11.7.3-2>`__.

.. table:: Response Header Fields

   +-----------------+------------+-----------------+-----------------+
   | Name            | center     | Origin Server   | Description     |
   |                 |            | Usage           |                 |
   +=================+============+=================+=================+
   | Content-Type    | media-type | M               | The media-type  |
   |                 |            |                 | of the payload. |
   +-----------------+------------+-----------------+-----------------+
   | Content-Length  | uint       | C               | Shall be        |
   |                 |            |                 | present if no   |
   |                 |            |                 | content         |
   |                 |            |                 | encoding has    |
   |                 |            |                 | been applied to |
   |                 |            |                 | the payload.    |
   +-----------------+------------+-----------------+-----------------+
   | C               | encoding   | C               | Shall be        |
   | ontent-Encoding |            |                 | present if a    |
   |                 |            |                 | content         |
   |                 |            |                 | encoding has    |
   |                 |            |                 | been applied to |
   |                 |            |                 | the payload.    |
   +-----------------+------------+-----------------+-----------------+
   | C               | url        | O               | Shall be        |
   | ontent-Location |            |                 | present if the  |
   |                 |            |                 | response has a  |
   |                 |            |                 | payload         |
   |                 |            |                 | containing a    |
   |                 |            |                 | resource. See   |
   |                 |            |                 | `Payload Header |
   |                 |            |                 | Fields <#       |
   |                 |            |                 | sect_8.4.3>`__. |
   |                 |            |                 |                 |
   |                 |            |                 | May be present  |
   |                 |            |                 | otherwise.      |
   +-----------------+------------+-----------------+-----------------+
   | Warning         | text       | C               | See below.      |
   +-----------------+------------+-----------------+-----------------+

If the user agent specifies a Procedure Step State (0074,1000) Attribute
with a value of "CANCELED" and the Workitem is already in that state,
the response message shall include the following HTTP Warning header
field:

::

   Warning: 299 <service>: The UPS is already in the requested state of CANCELED.

If the user agent specifies a Procedure Step State (0074,1000) Attribute
with a value of "COMPLETED" and the UPS Instance is already in that
state, the response message shall include the following HTTP Warning
header field:

::

   Warning: 299 <service>: The UPS is already in the requested state of COMPLETED.

If the request was rejected with a failure status code, the response
message shall include one of following messages in the HTTP Warning
header field describing the nature of the conflict:

::

   Warning: 299 <service>: The Transaction UID is missing.

::

   Warning: 299 <service>: The Transaction UID is incorrect.

::

   Warning: 299 <service>: The submitted request is inconsistent with the state of the UPS Instance.

See also `Header Fields <#sect_8.4>`__.

.. _sect_11.7.3.3:

Response Payload
^^^^^^^^^^^^^^^^

A success response shall have no payload.

A failure response payload may contain a Status Report describing any
failures, warnings, or other useful information.

.. _sect_11.8:

Request Cancellation
--------------------

This transaction allows a user agent that does not own a Workitem to
request that it be canceled. It corresponds to the UPS DIMSE N-ACTION
operation "Request UPS Cancel". See .

To cancel a Workitem that the user agent owns, i.e., that is in the IN
PROGRESS state, the user agent uses the Change Workitem State
transaction as described in `Change Workitem State <#sect_11.7>`__.

.. _sect_11.8.1:

Request
~~~~~~~

The request shall have the following syntax:

::

   POST SP /workitems/{workitem}/cancelrequest SP version CRLF

::

   Content-Type: dicom-media-type

::

   (Content-Length: uint / Content-Encoding: encoding) CRLF

::

   *(header-field CRLF)

::

   CRLF

::

   [Payload]

The user agent shall conform to the SCU behavior specified in .

.. _sect_11.8.1.1:

Target Resources
^^^^^^^^^^^^^^^^

The Target Resource for this transaction is a Workitem.

.. _sect_11.8.1.2:

Query Parameters
^^^^^^^^^^^^^^^^

The user agent shall supply, and the origin server shall support, the
Common Query Parameters in `Common Query Parameters <#sect_11.1.2>`__.

.. _sect_11.8.1.3:

Request Header Fields
^^^^^^^^^^^^^^^^^^^^^

The origin server shall support header fields as required in
`table_title <#table_11.8.1-1>`__.

The user agent shall supply in the request header fields as defined in
`table_title <#table_11.8.1-1>`__.

.. table:: Request Header Fields

   +--------------+--------------+-------+-------------+--------------+
   | Name         | Values       | Usage | Description |              |
   +==============+==============+=======+=============+==============+
   | Content-Type | dico         | M     | M           | The          |
   |              | m-media-type |       |             | media-type   |
   |              |              |       |             | of the       |
   |              |              |       |             | payload.     |
   +--------------+--------------+-------+-------------+--------------+
   | Co           | uint         | C     | M           | Shall be     |
   | ntent-Length |              |       |             | present if a |
   |              |              |       |             | content      |
   |              |              |       |             | encoding has |
   |              |              |       |             | not been     |
   |              |              |       |             | applied to   |
   |              |              |       |             | the payload. |
   +--------------+--------------+-------+-------------+--------------+
   | Cont         | encoding     | C     | M           | Shall be     |
   | ent-Encoding |              |       |             | present if a |
   |              |              |       |             | content      |
   |              |              |       |             | encoding has |
   |              |              |       |             | been applied |
   |              |              |       |             | to the       |
   |              |              |       |             | payload.     |
   +--------------+--------------+-------+-------------+--------------+

See also `Header Fields <#sect_8.4>`__.

.. _sect_11.8.1.4:

Request Payload
^^^^^^^^^^^^^^^

The request payload, if present, may describe the reason for requesting
the cancellation of the Workitem, a Contact Display Name, and/or a
Contact URI for the person with whom the cancel request may be
discussed.

The Request UPS Cancel Action Information is specified in .

.. _sect_11.8.2:

Behavior
~~~~~~~~

The origin server shall process the request as described by the SCP
behavior in .

.. _sect_11.8.3:

Response
~~~~~~~~

The response shall have the following syntax:

::

   version SP status-code SP reason-phrase CRLF

::

   [Content-Type dicom-media-type CRLF]

::

   [Content-Type: dicom-media-type CRLF]

::

   [(Content-Length: uint / Content-Encoding: encoding) CRLF]

::

   [Content-Location: url CRLF]

::

   *(header-field CRLF) CRLF

::

   [status-report]

.. _sect_11.8.3.1:

Status Codes
^^^^^^^^^^^^

`table_title <#table_11.8.3-1>`__ shows some common status codes
corresponding to this transaction. See also `Status Codes <#sect_8.5>`__
for additional status codes.

.. table:: Status Code Meaning

   +-----------------+------------------------+------------------------+
   | Status          | Code                   | Meaning                |
   +=================+========================+========================+
   | Success         | 202 (Accepted)         | The request was        |
   |                 |                        | accepted by the origin |
   |                 |                        | server, but the Target |
   |                 |                        | Workitem state has not |
   |                 |                        | necessarily changed    |
   |                 |                        | yet.                   |
   |                 |                        |                        |
   |                 |                        | .. note::              |
   |                 |                        |                        |
   |                 |                        |    The owner of the    |
   |                 |                        |    Workitem is not     |
   |                 |                        |    obliged to honor    |
   |                 |                        |    the request to      |
   |                 |                        |    cancel and, in some |
   |                 |                        |    scenarios, may not  |
   |                 |                        |    even receive        |
   |                 |                        |    notification of the |
   |                 |                        |    request.            |
   |                 |                        |                        |
   |                 |                        | The owner of the       |
   |                 |                        | Workitem is not        |
   |                 |                        | obliged to honor the   |
   |                 |                        | request to cancel and, |
   |                 |                        | in some scenarios, may |
   |                 |                        | not even receive       |
   |                 |                        | notification of the    |
   |                 |                        | request.               |
   +-----------------+------------------------+------------------------+
   | Failure         | 400 (Bad Request)      | There was a problem    |
   |                 |                        | with the syntax of the |
   |                 |                        | request.               |
   +-----------------+------------------------+------------------------+
   | 404 (Not Found) | The Target Workitem    |                        |
   |                 | was not found.         |                        |
   +-----------------+------------------------+------------------------+
   | 409 (Conflict)  | The request is         |                        |
   |                 | inconsistent with the  |                        |
   |                 | current state of the   |                        |
   |                 | Target Workitem. For   |                        |
   |                 | example, the Target    |                        |
   |                 | Workitem is in the     |                        |
   |                 | SCHEDULED or COMPLETED |                        |
   |                 | state.                 |                        |
   +-----------------+------------------------+------------------------+

.. _sect_11.8.3.2:

Response Header Fields
^^^^^^^^^^^^^^^^^^^^^^

The origin server shall support header fields as required in
`table_title <#table_11.8.3-2>`__.

.. table:: Response Header Fields

   +-----------------+------------+-----------------+-----------------+
   | Name            | center     | Origin Server   | Description     |
   |                 |            | Usage           |                 |
   +=================+============+=================+=================+
   | Content-Type    | media-type | C               | The media type  |
   |                 |            |                 | of the Status   |
   |                 |            |                 | Report          |
   |                 |            |                 | document.       |
   |                 |            |                 |                 |
   |                 |            |                 | Shall be        |
   |                 |            |                 | present if the  |
   |                 |            |                 | response        |
   |                 |            |                 | contains a      |
   |                 |            |                 | payload.        |
   +-----------------+------------+-----------------+-----------------+
   | Content-Length  | uint       | C               | Shall be        |
   |                 |            |                 | present if a    |
   |                 |            |                 | content         |
   |                 |            |                 | encoding has    |
   |                 |            |                 | not been        |
   |                 |            |                 | applied to the  |
   |                 |            |                 | payload.        |
   +-----------------+------------+-----------------+-----------------+
   | C               | encoding   | C               | Shall be        |
   | ontent-Encoding |            |                 | present if a    |
   |                 |            |                 | content         |
   |                 |            |                 | encoding has    |
   |                 |            |                 | been applied to |
   |                 |            |                 | the payload.    |
   +-----------------+------------+-----------------+-----------------+

If the Workitem Instance is already in a canceled state, the response
message shall include the following HTTP Warning header field:

::

   Warning: 299 <service>: The UPS is already in the requested state of CANCELED.

See also `Header Fields <#sect_8.4>`__.

.. _sect_11.8.3.3:

Response Payload
^^^^^^^^^^^^^^^^

The response may include a payload containing an appropriate Status
Report.

.. _sect_11.9:

Search Transaction
------------------

This transaction searches the Worklist for Workitems that match the
specified Query Parameters and returns a list of matching Workitems.
Each Workitem in the returned list includes return Attributes specified
in the request. The transaction corresponds to the UPS DIMSE C-FIND
operation.

.. _sect_11.9.1:

Request
~~~~~~~

The request shall have the following syntax:

::

   GET SP /workitems?{&match*}{&includefield}{&fuzzymatching}{&offset}{&limit} SP version CRLF

::

   Accept: dicom-media-types CRLF

::

   *(header-field CRLF)

::

   CRLF

The user agent shall conform to the SCU behavior specified in .

.. _sect_11.9.1.1:

Target Resources
^^^^^^^^^^^^^^^^

The Target Resource for this transaction is the Worklist.

.. _sect_11.9.1.2:

Query Parameters
^^^^^^^^^^^^^^^^

The origin server shall support Query Parameters as required in
`table_title <#table_8.3.4-1>`__.

The user agent shall supply in the request Query Parameters as required
in `table_title <#table_8.3.4-1>`__.

.. _sect_11.9.1.3:

Request Header Fields
^^^^^^^^^^^^^^^^^^^^^

The origin server shall support header fields as required in
`table_title <#table_11.9.1-1>`__.

The user agent shall supply in the request header fields as defined in
`table_title <#table_11.9.1-1>`__.

.. table:: Request Header Fields

   +--------------+--------------+-------+-------------+--------------+
   | Name         | Values       | Usage | Description |              |
   +==============+==============+=======+=============+==============+
   | Accept       | 1#-dico      | M     | M           | The          |
   |              | m-media-type |       |             | Acceptable   |
   |              |              |       |             | Media Types  |
   |              |              |       |             | of the       |
   |              |              |       |             | response     |
   |              |              |       |             | payload.     |
   +--------------+--------------+-------+-------------+--------------+
   | C            | "no-cache"   | O     | M           | If included, |
   | ache-Control |              |       |             | specifies    |
   |              |              |       |             | that search  |
   |              |              |       |             | results      |
   |              |              |       |             | returned     |
   |              |              |       |             | should be    |
   |              |              |       |             | current and  |
   |              |              |       |             | not cached.  |
   +--------------+--------------+-------+-------------+--------------+

See also `Header Fields <#sect_8.4>`__.

.. _sect_11.9.1.4:

Request Payload
^^^^^^^^^^^^^^^

The request payload shall be empty.

.. _sect_11.9.2:

Behavior
~~~~~~~~

The origin server shall perform a search according the requirements
specified in `Search Query Parameters <#sect_8.3.4>`__.

For each matching Workitem, the origin server shall include in the
results:

-  All Unified Procedure Step Instance Attributes in with a Return Key
   Type of 1 or 2.

-  All Unified Procedure Step Instance Attributes in with a Return Key
   Type of 1C for which the conditional requirements are met.

-  All other Workitem Attributes passed as match parameters that are
   supported by the origin server as either matching or return
   Attributes.

-  All other Workitem Attributes passed as includefield parameter values
   that are supported by the origin server as return Attributes.

.. _sect_11.9.3:

Response
~~~~~~~~

The response shall have the following syntax:

::

   version SP status-code SP reason-phrase CRLF

::

   [Content-Type: dicom-media-type CRLF]

::

   [(Content-Length: uint / Content-Encoding: encoding) CRLF]

::

   [Content-Location: url CRLF]

::

   *(header-field CRLF)

::

   CRLF

::

   [search-results / status-report]

.. _sect_11.9.3.1:

Status Codes
^^^^^^^^^^^^

`table_title <#table_11.9.3-1>`__ shows some common status codes
corresponding to this transaction. See also `Status Codes <#sect_8.5>`__
for additional status codes.

.. table:: Status Code Meaning

   +----------------------+----------------------+----------------------+
   | Status               | Code                 | Meaning              |
   +======================+======================+======================+
   | Success              | 200 (OK)             | The search completed |
   |                      |                      | successfully, and    |
   |                      |                      | the matching results |
   |                      |                      | are returned in the  |
   |                      |                      | message body.        |
   +----------------------+----------------------+----------------------+
   | 204 (No Content)     | The search completed |                      |
   |                      | successfully, but    |                      |
   |                      | there were no        |                      |
   |                      | matching results.    |                      |
   +----------------------+----------------------+----------------------+
   | 206 (Partial         | Only some of the     |                      |
   | Content)             | search results were  |                      |
   |                      | returned, and the    |                      |
   |                      | rest can be          |                      |
   |                      | requested through    |                      |
   |                      | the appropriate      |                      |
   |                      | request.             |                      |
   +----------------------+----------------------+----------------------+
   | Failure              | 400 (Bad Request)    | The was a problem    |
   |                      |                      | with the request.    |
   |                      |                      | For example, invalid |
   |                      |                      | Query Parameter      |
   |                      |                      | syntax.              |
   +----------------------+----------------------+----------------------+
   | 413 (Payload Too     | The size of the      |                      |
   | Large)               | results exceeds the  |                      |
   |                      | maximum payload size |                      |
   |                      | supported by the     |                      |
   |                      | origin server. The   |                      |
   |                      | user agent may       |                      |
   |                      | repeat the request   |                      |
   |                      | with paging or with  |                      |
   |                      | a narrower query to  |                      |
   |                      | reduce the size of   |                      |
   |                      | the result.          |                      |
   +----------------------+----------------------+----------------------+

.. _sect_11.9.3.2:

Response Header Fields
^^^^^^^^^^^^^^^^^^^^^^

The origin server shall support header fields as required in
`table_title <#table_11.9.3-2>`__.

.. table:: Response Header Fields

   +-----------------+------------+-----------------+-----------------+
   | Name            | center     | Origin Server   | Description     |
   |                 |            | Usage           |                 |
   +=================+============+=================+=================+
   | Content-Type    | media-type | M               | The media-type  |
   |                 |            |                 | of the payload. |
   +-----------------+------------+-----------------+-----------------+
   | Content-Length  | Uint       | C               | Shall be        |
   |                 |            |                 | present if a    |
   |                 |            |                 | content coding  |
   |                 |            |                 | has not been    |
   |                 |            |                 | applied to the  |
   |                 |            |                 | payload.        |
   +-----------------+------------+-----------------+-----------------+
   | C               | Encoding   | C               | Shall be        |
   | ontent-Encoding |            |                 | present if a    |
   |                 |            |                 | content         |
   |                 |            |                 | encoding has    |
   |                 |            |                 | been applied to |
   |                 |            |                 | the payload.    |
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
   |                 |            |                 |                 |
   |                 |            |                 | May be present  |
   |                 |            |                 | otherwise.      |
   +-----------------+------------+-----------------+-----------------+

See also `Header Fields <#sect_8.4>`__.

.. _sect_11.9.3.3:

Response Payload
^^^^^^^^^^^^^^^^

A success response payload shall contain the search results in an
Acceptable Media Type. See `Acceptable Media Types <#sect_8.7.5>`__. If
there are no matching results the payload will be empty. See
`Payloads <#sect_8.6>`__.

A failure response payload may contain a Status Report describing any
failures, warnings, or other useful information.

.. _sect_11.10:

Subscribe Transaction
---------------------

This transaction creates a Subscription to a Worklist or Workitem
resource. It corresponds to the UPS DIMSE N-ACTION operation "Subscribe
to Receive UPS Event Reports".

Once a Subscription has been created the user agent will receive
notifications containing Event Reports for events associated with the
Subscription's resource. To receive the notifications generated by
Subscriptions, the user agent must have first opened a Notification
Connection between itself and the origin server using the Open
Notification Connection transaction; see `Open Notification Connection
Transaction <#sect_8.10.4>`__.

.. _sect_11.10.1:

Request
~~~~~~~

The request shall have the following syntax:

::

   POST SP /workitems/{resource}/subscribers/{aetitle}{?deletionlock}{&filter} SP version CRLF

::

   *(header-field CRLF)

::

   CRLF

The user agent shall conform to the SCU behavior specified in .

.. _sect_11.10.1.1:

Target Resources
^^^^^^^^^^^^^^^^

The origin server shall support the resources in
`table_title <#table_11.10.1-1>`__.

.. table:: Subscribe Transaction Resources

   +--------------------------------+------------------------------------+
   | Resource                       | URI Template                       |
   +================================+====================================+
   | Worklist Subscription          | /workitems/1.2.840.1000            |
   |                                | 8.5.1.4.34.5/subscribers/{aetitle} |
   +--------------------------------+------------------------------------+
   | Filtered Worklist Subscription | /workitems/1.2.840.10008.          |
   |                                | 5.1.4.34.5.1/subscribers/{aetitle} |
   +--------------------------------+------------------------------------+
   | Workitem Subscription          | /workitem                          |
   |                                | s/{workitem}/subscribers/{aetitle} |
   +--------------------------------+------------------------------------+

.. _sect_11.10.1.2:

Query Parameters
^^^^^^^^^^^^^^^^

The origin server shall support Query Parameters as required in
`table_title <#table_11.10.1-2>`__.

The user agent shall supply in the request Query Parameters as required
in `table_title <#table_11.10.1-2>`__.

.. table:: uery Parameters by Resource

   +----------+----------+----------+-------+----------+----------+
   | Key      | Value    | Resource | Usage | Des      |          |
   |          |          |          |       | cription |          |
   +==========+==========+==========+=======+==========+==========+
   | accept   | media    | W        | O     | M        |          |
   |          | type     | orklist, |       |          |          |
   |          |          | Filtered |       |          |          |
   |          |          | W        |       |          |          |
   |          |          | orklist, |       |          |          |
   |          |          | Workitem |       |          |          |
   +----------+----------+----------+-------+----------+----------+
   | charset  | charset  | W        | O     | M        |          |
   |          |          | orklist, |       |          |          |
   |          |          | Filtered |       |          |          |
   |          |          | W        |       |          |          |
   |          |          | orklist, |       |          |          |
   |          |          | Workitem |       |          |          |
   +----------+----------+----------+-------+----------+----------+
   | dele     | tr       | W        | O     | M        |          |
   | tionlock | ue/false | orklist, |       |          |          |
   |          |          | Filtered |       |          |          |
   |          |          | W        |       |          |          |
   |          |          | orklist, |       |          |          |
   |          |          | Workitem |       |          |          |
   +----------+----------+----------+-------+----------+----------+
   | filter   | 1#(attr  | Filtered | C     | M        | Shall be |
   |          | ibute"=" | Worklist |       |          | present  |
   |          | value)   |          |       |          | if the   |
   |          |          |          |       |          | Target   |
   |          |          |          |       |          | Resource |
   |          |          |          |       |          | is the   |
   |          |          |          |       |          | Filtered |
   |          |          |          |       |          | W        |
   |          |          |          |       |          | orklist. |
   +----------+----------+----------+-------+----------+----------+

The Deletion Lock Query Parameter has the following syntax:

::

   deletionlock = "deletionlock=" true / false

If present with a value of true the Subscription will be created with a
Deletion Lock (see ).

The Filter Query Parameter has the following syntax:

::

   filter = 1#(attribute "=" value)

It is a comma-separated list of one or more matching keys
(attribute/value pairs). A Workitem Subscription will be created for any
existing and future Workitem that matches the attribute/value pairs of
the filter. The valid Attributes for this Query Parameter are defined by
the UPS IOD (see ).

See `Attribute Matching <#sect_8.3.4.1>`__ for the syntax of matching
keys.

.. _sect_11.10.1.3:

Request Header Fields
^^^^^^^^^^^^^^^^^^^^^

The request has no mandatory header fields. See `Header
Fields <#sect_8.4>`__.

.. _sect_11.10.1.4:

Request Payload
^^^^^^^^^^^^^^^

The request shall have no payload.

.. _sect_11.10.2:

Behavior
~~~~~~~~

The origin server shall create and manage a Subscription to the Target
Resource for the user agent. The origin server shall conform to the SCP
behavior specified in .

.. _sect_11.10.3:

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

   [status-report]

.. _sect_11.10.3.1:

Status Codes
^^^^^^^^^^^^

`table_title <#table_11.10.3-1>`__ shows some common status codes
corresponding to this transaction. See also `Status Codes <#sect_8.5>`__
for additional status codes.

.. table:: Status Code Meaning

   +-----------------+------------------------+------------------------+
   | Status          | Code                   | Meaning                |
   +=================+========================+========================+
   | Success         | 201 (Created)          | The Subscription was   |
   |                 |                        | created.               |
   +-----------------+------------------------+------------------------+
   | Failure         | 400 (Bad Request)      | There was a problem    |
   |                 |                        | with the syntax of the |
   |                 |                        | request.               |
   +-----------------+------------------------+------------------------+
   | 403 (Forbidden) | The origin server      |                        |
   |                 | understood the request |                        |
   |                 | but is refusing to     |                        |
   |                 | perform the query      |                        |
   |                 | (e.g., the origin      |                        |
   |                 | server does not        |                        |
   |                 | support Worklist       |                        |
   |                 | Subscription           |                        |
   |                 | Filtering, or an       |                        |
   |                 | authenticated user has |                        |
   |                 | insufficient           |                        |
   |                 | privileges).           |                        |
   +-----------------+------------------------+------------------------+
   | 404 (Not Found) | The Target Resource    |                        |
   |                 | was not found.         |                        |
   +-----------------+------------------------+------------------------+

.. _sect_11.10.3.2:

Response Header Fields
^^^^^^^^^^^^^^^^^^^^^^

The origin server shall support header fields as required in
`table_title <#table_11.10.3-2>`__.

.. table:: Response Header Fields

   +-----------------+------------+-----------------+-----------------+
   | Name            | center     | Origin Server   | Description     |
   |                 |            | Usage           |                 |
   +=================+============+=================+=================+
   | Content-Type    | media-type | C               | Shall be        |
   |                 |            |                 | present if the  |
   |                 |            |                 | response        |
   |                 |            |                 | contains a      |
   |                 |            |                 | payload.        |
   +-----------------+------------+-----------------+-----------------+
   | C               | url        | C               | A URL-reference |
   | ontent-Location |            |                 | to the          |
   |                 |            |                 | WebSocket       |
   |                 |            |                 | Connection.     |
   |                 |            |                 |                 |
   |                 |            |                 | Shall be        |
   |                 |            |                 | present if a    |
   |                 |            |                 | Subscription    |
   |                 |            |                 | was created.    |
   |                 |            |                 |                 |
   |                 |            |                 | The URL shall   |
   |                 |            |                 | include the     |
   |                 |            |                 | WebSocket       |
   |                 |            |                 | protocol        |
   |                 |            |                 | (either WS or   |
   |                 |            |                 | WSS) and may    |
   |                 |            |                 | include a       |
   |                 |            |                 | combination of  |
   |                 |            |                 | authority and   |
   |                 |            |                 | path.           |
   +-----------------+------------+-----------------+-----------------+
   | Warning         | String     | C               | See below.      |
   +-----------------+------------+-----------------+-----------------+

If the Create Subscription request was accepted but the Deletion Lock
was not, the response shall include the following Warning header field:

::

   Warning: 299 <service>: Deletion Lock not granted.

and may include a Status Report.

If the request was rejected with a 403 status code because Filtered
Worklist Subscription is not supported, the response shall include the
following Warning header field:

::

   Warning: 299 <service>: Filtered Worklist Subscriptions are not supported.

See also `Header Fields <#sect_8.4>`__.

.. _sect_11.10.3.3:

Response Payload
^^^^^^^^^^^^^^^^

A success response payload may contain a Status Report.

A failure response payload may contain a Status Report describing any
failures, warnings, or other useful information.

.. _sect_11.11:

Unsubscribe Transaction
-----------------------

This transaction is used to stop the origin server from sending new
Event Reports to the user agent and may also stop the origin server from
subscribing the user agent to new Workitems.

.. _sect_11.11.1:

Request
~~~~~~~

The request shall have the following syntax:

::

   DELETE SP {/resource} SP version CRLF

::

   *(header-field CRLF)

::

   CRLF

.. _sect_11.11.1.1:

Target Resources
^^^^^^^^^^^^^^^^

The origin server shall support the resources in
`table_title <#table_11.11.1-1>`__.

.. table:: Unsubscribe Transaction Resources

   +--------------------------------+------------------------------------+
   | Resource                       | URI Template                       |
   +================================+====================================+
   | Workitem Subscription          | /workitem                          |
   |                                | s/{workitem}/subscribers/{aetitle} |
   +--------------------------------+------------------------------------+
   | Worklist Subscription          | /workitems/1.2.840.1000            |
   |                                | 8.5.1.4.34.5/subscribers/{aetitle} |
   +--------------------------------+------------------------------------+
   | Filtered Worklist Subscription | /workitems/1.2.840.10008.          |
   |                                | 5.1.4.34.5.1/subscribers/{aetitle} |
   +--------------------------------+------------------------------------+

.. _sect_11.11.1.2:

Query Parameters
^^^^^^^^^^^^^^^^

The request has no Query Parameters.

.. _sect_11.11.1.3:

Request Header Fields
^^^^^^^^^^^^^^^^^^^^^

The request has no Mandatory header fields.

.. _sect_11.11.1.4:

Request Payload
^^^^^^^^^^^^^^^

The request payload shall be empty.

.. _sect_11.11.2:

Behavior
~~~~~~~~

Upon receipt of an Unsubscribe request, the origin server shall attempt
to remove the Workitem Subscription, Worklist Subscription, or Filtered
Worklist Subscription of the specified Application Entity with respect
to the specified Workitem UID, Worklist UID, or Filtered Worklist UID as
described in and then return an appropriate response.

For a Workitem resource, this corresponds to the UPS DIMSE N-ACTION
operation "Unsubscribe from Receiving UPS Event Reports".

For a Worklist or Filtered Worklist resource this transaction
corresponds to the UPS DIMSE N-ACTION operation "Unsubscribe from
Receiving UPS Event Reports" for the Global Subscription identified by
the well-known UID.

.. _sect_11.11.3:

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

   [status-report]

.. _sect_11.11.3.1:

Status Codes
^^^^^^^^^^^^

`table_title <#table_11.11.3-1>`__ shows some common status codes
corresponding to this transaction. See also `Status Codes <#sect_8.5>`__
for additional status codes.

.. table:: Status Code Meaning

   +-----------------+------------------------+------------------------+
   | Status          | Code                   | Meaning                |
   +=================+========================+========================+
   | Success         | 200 (OK)               | The Subscription(s)    |
   |                 |                        | were removed.          |
   +-----------------+------------------------+------------------------+
   | Failure         | 400 (Bad Request)      | There was a problem    |
   |                 |                        | with the request. For  |
   |                 |                        | example, the Target    |
   |                 |                        | Workitem UID is        |
   |                 |                        | missing.               |
   +-----------------+------------------------+------------------------+
   | 404 (Not Found) | The target             |                        |
   |                 | Subscription was not   |                        |
   |                 | found.                 |                        |
   +-----------------+------------------------+------------------------+

.. _sect_11.11.3.2:

Response Header Fields
^^^^^^^^^^^^^^^^^^^^^^

The origin server shall support header fields as required in
`table_title <#table_11.11.3-2>`__.

.. table:: Response Header Fields

   +-----------------+------------+-----------------+-----------------+
   | Name            | Value      | Origin Server   | Description     |
   |                 |            | Usage           |                 |
   +=================+============+=================+=================+
   | Content-Type    | media-type | C               | The media-type  |
   |                 |            |                 | of the response |
   |                 |            |                 | payload.        |
   |                 |            |                 |                 |
   |                 |            |                 | Shall be        |
   |                 |            |                 | present if the  |
   |                 |            |                 | response has a  |
   |                 |            |                 | payload.        |
   +-----------------+------------+-----------------+-----------------+
   | Content-Length  | uint       | C               | Shall be        |
   |                 |            |                 | present if no   |
   |                 |            |                 | content         |
   |                 |            |                 | encoding has    |
   |                 |            |                 | been applied to |
   |                 |            |                 | the payload.    |
   +-----------------+------------+-----------------+-----------------+
   | C               | encoding   | C               | Shall be        |
   | ontent-Encoding |            |                 | present if a    |
   |                 |            |                 | content         |
   |                 |            |                 | encoding has    |
   |                 |            |                 | been applied to |
   |                 |            |                 | the payload     |
   +-----------------+------------+-----------------+-----------------+
   | Warning         | text       | O               | A warning       |
   |                 |            |                 | message.        |
   +-----------------+------------+-----------------+-----------------+

See also `Header Fields <#sect_8.4>`__.

.. _sect_11.11.3.3:

Response Payload
^^^^^^^^^^^^^^^^

A success response shall have no payload.

A failure response payload may contain a Status Report describing any
failures, warnings, or other useful information.

.. _sect_11.12:

Suspend Global Subscription Transaction
---------------------------------------

This transaction is used to stop the origin server from automatically
subscribing the User-Agent to new Workitems. This does not delete any
existing subscriptions to specific Workitems.

.. _sect_11.12.1:

Request
~~~~~~~

The request shall have the following syntax:

::

   POST SP {/resource} SP version CRLF

::

   *(header-field CRLF)

::

   CRLF

.. _sect_11.12.1.1:

Target Resources
^^^^^^^^^^^^^^^^

The origin server shall support the resources in
`table_title <#table_11.12.1-1>`__.

.. table:: Unsubscribe Transaction Resources

   +--------------------------------+------------------------------------+
   | Resource                       | URI Template                       |
   +================================+====================================+
   | Worklist Subscription          | /workitems/1.2.840.10008.5.1.4.    |
   |                                | 34.5/subscribers/{aetitle}/suspend |
   +--------------------------------+------------------------------------+
   | Filtered Worklist Subscription | /workitems/1.2.840.10008.5.1.4.34  |
   |                                | .5.1/subscribers/{aetitle}/suspend |
   +--------------------------------+------------------------------------+

.. _sect_11.12.1.2:

Query Parameters
^^^^^^^^^^^^^^^^

The request has no Query Parameters.

.. _sect_11.12.1.3:

Request Header Fields
^^^^^^^^^^^^^^^^^^^^^

The request has no Mandatory header fields.

.. _sect_11.12.1.4:

Request Payload
^^^^^^^^^^^^^^^

The request payload shall be empty.

.. _sect_11.12.2:

Behavior
~~~~~~~~

Upon receipt of a Suspend request, the origin server shall attempt to
remove the Worklist Subscription, or Filtered Worklist Subscription of
the specified Application Entity with respect to the specified Worklist
UID, or Filtered Worklist UID as described in and then return an
appropriate response.

This transaction corresponds to the UPS DIMSE N-ACTION operation
"Suspend Global Subscription"

.. _sect_11.12.3:

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

   [status-report]

.. _sect_11.12.3.1:

Status Codes
^^^^^^^^^^^^

`table_title <#table_11.12.3-1>`__ shows some common status codes
corresponding to this transaction. See also `Status Codes <#sect_8.5>`__
for additional status codes.

.. table:: Status Code Meaning

   +-----------------+------------------------+------------------------+
   | Status          | Code                   | Meaning                |
   +=================+========================+========================+
   | Success         | 200 (OK)               | The Worklist           |
   |                 |                        | Subscription was       |
   |                 |                        | suspended.             |
   +-----------------+------------------------+------------------------+
   | Failure         | 400 (Bad Request)      | There was a problem    |
   |                 |                        | with the request. For  |
   |                 |                        | example, the Target    |
   |                 |                        | Worklist UID is        |
   |                 |                        | missing.               |
   +-----------------+------------------------+------------------------+
   | 404 (Not Found) | The target             |                        |
   |                 | Subscription was not   |                        |
   |                 | found.                 |                        |
   +-----------------+------------------------+------------------------+

.. _sect_11.12.3.2:

Response Header Fields
^^^^^^^^^^^^^^^^^^^^^^

The origin server shall support header fields as required in
`table_title <#table_11.12.3-2>`__.

.. table:: Response Header Fields

   +-----------------+------------+-----------------+-----------------+
   | Name            | center     | Origin Server   | Description     |
   |                 |            | Usage           |                 |
   +=================+============+=================+=================+
   | Content-Type    | media-type | C               | The media-type  |
   |                 |            |                 | of the response |
   |                 |            |                 | payload.        |
   |                 |            |                 |                 |
   |                 |            |                 | Shall be        |
   |                 |            |                 | present if the  |
   |                 |            |                 | response has a  |
   |                 |            |                 | payload.        |
   +-----------------+------------+-----------------+-----------------+
   | Content-Length  | uint       | C               | Shall be        |
   |                 |            |                 | present if no   |
   |                 |            |                 | content         |
   |                 |            |                 | encoding has    |
   |                 |            |                 | been applied to |
   |                 |            |                 | the payload.    |
   +-----------------+------------+-----------------+-----------------+
   | C               | encoding   | C               | Shall be        |
   | ontent-Encoding |            |                 | present if a    |
   |                 |            |                 | content         |
   |                 |            |                 | encoding has    |
   |                 |            |                 | been applied to |
   |                 |            |                 | the payload.    |
   +-----------------+------------+-----------------+-----------------+
   | Warning         | text       | O               | A warning       |
   |                 |            |                 | message.        |
   +-----------------+------------+-----------------+-----------------+

See also `Header Fields <#sect_8.4>`__.

.. _sect_11.12.3.3:

Response Payload
^^^^^^^^^^^^^^^^

A success response shall have no payload.

A failure response payload may contain a Status Report describing any
failures, warnings, or other useful information.

.. _sect_11.13:

Workitem Event Reports
----------------------

The origin server uses the Send Event Report Transaction (see `Send
Event Report Transaction <#sect_8.10.5>`__) to send a Workitem Event
Report, containing the details of any state change in the Workitem to
the user agent.

The origin server shall send Workitem Event Reports as described in .

The Event Report shall contain all mandatory Attributes described in and
.

The following is an example application/dicom+json Workitem Event Report
payload:

::

   {

::

   "00000002": {"vr": "UI", "Value": ["1.2.840.10008.5.1.4.34.6.4"] },

::

   "00000110": {"vr": "US", "Value": [23] },

::

   "00001000": {"vr": "UI", "Value": ["1.2.840.10008.5.1.4.34.6.4.2.3.44.22231"] },

::

   "00001002": {"vr": "US", "Value": [1] },

::

   "00404041": {"vr": "US", "Value": ["READY"] },

::

   "00741000": {"vr": "LT", "Value": ["SCHEDULED"] }

::

   } CRLF

