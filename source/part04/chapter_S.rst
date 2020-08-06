.. _chapter_S:

Media Creation Management Service Class (Normative)
===================================================

.. _sect_S.1:

Overview
--------

.. _sect_S.1.1:

Scope
~~~~~

The Media Creation Management Service Class defines a mechanism by which
an SCU can instruct a device to create Interchange Media containing a
set of Composite SOP Instances that have already been transferred to the
media creation device using the Storage Service Class.

This Service Class does not address archival storage requirements. It is
intended only for the management of media creation devices. There is no
requirement by the Standard that an SCP of this Service Class will
commit to taking responsibility for archival of Composite Instances,
such that an SCU may then discard them. Such behavior is entirely
outside the scope of the Standard. In other words, Media Creation does
not imply Storage Commitment.

The application profile(s) for the set of instances, which implies the
form of the media created (i.e., CD, DVD or MOD), can either be left to
the discretion of the SCP, or explicitly specified in the media creation
request. In the latter case, if the device is unable to create the
requested profiles, an error shall be returned.

.. note::

   1. More than one profile may be requested or used by default, since
      the requested set of instances may not be compatible with a single
      profile. DICOM media may always contain instances written by more
      than one profile. See .

   2. It is the responsibility of the SCU to negotiate and store
      instances with an appropriate Transfer Syntax should a specific
      Transfer Syntax be required by a requested profile. The SCP is not
      required to support compression or decompression of stored
      instances in order to convert stored instances into a form
      suitable for a requested profile. It may do so, if so requested,
      but the level of lossy compression would be at the discretion of
      the SCP. If the degree of compression is important to the
      application, then the SCU may compress the images before sending
      them to the SCP.

The request controls whether or not a label is to be generated on the
media, be it from information contained in the instances (such as
patient demographics) or from text explicitly specified in the request.

.. note::

   1. An SCP may or may not be physically capable of labeling the media.
      This capability is outside the scope of conformance to the
      Standard. Inability to create a label is not an error.

   2. De-identification of instances (and labels), such as for teaching
      file media or clinical trial media is the responsibility of the
      SCU and is outside the scope of this service. That is, the SCU
      must de-identify the composite instances before sending them,
      prior to the media creation request.

The Service Class contains a limited capability to return status
information. A media creation request may initially either fail or be
accepted. Subsequently, the SCP may be polled as to the status of the
request (idle, pending/creating, successful or failed) by the SCU on the
same or on a separate Association. There is no asynchronous
notification. There is no dependence on the duration or persistence of
an Association.

.. note::

   There is no requirement to manage the handling of transient failures
   (such as an empty supply of blank media or labels or ink). Whether or
   not the SCP queues stored instances and requests in such cases, or
   fails to accept the request, is outside the scope of the Standard.

.. _sect_S.2:

Conformance Overview
--------------------

The application-level services addressed by this Service Class are
specified via the Media Creation Management SOP Class.

The Media Creation Management SOP Class specifies Attributes, operations
and behavior applicable to the SOP Class. The conformance requirements
shall be specified in terms of the Service Class Provider (SCP) and the
Service Class User (SCU).

The Media Creation Management Service Class uses the Media Creation
Management IOD as defined in and the N-CREATE, N-ACTION and N-GET
Services specified in .

.. _sect_S.2.1:

Association Negotiation
~~~~~~~~~~~~~~~~~~~~~~~

Association establishment is the first phase of any instance of
communication between peer DICOM AEs. The Association negotiation rules
as specified in shall be used to negotiate the supported SOP Classes.

Support for the SCP/SCU Role Selection Negotiation is not applicable.
The SOP Class Extended Negotiation is not defined for this Service
Class.

.. _sect_S.3:

Media Creation Management SOP Class
-----------------------------------

The SCU transmits the SOP Instances to the SCP using the Storage Service
Class. The request for media creation is transmitted to the SCP and
contains a list of references to one or more SOP Instances. Success or
failure of media creation is subsequently indicated by the SCU
requesting the status from the SCP on the same or a separate
association.

.. _sect_S.3.1:

DIMSE Service Group
~~~~~~~~~~~~~~~~~~~

The following DIMSE-N Services are applicable to the Media Creation
Management SOP Class.

.. table:: DIMSE Service Group Applicable to Media Creation Management

   ============================= =============
   DICOM Message Service Element Usage SCU/SCP
   ============================= =============
   N-CREATE                      M/M
   N-ACTION                      M/M
   N-GET                         U/M
   ============================= =============

The DIMSE-N Services and Protocol are specified in .

.. _sect_S.3.2:

Operations
~~~~~~~~~~

The DICOM AEs that claim conformance to this SOP Class as an SCU shall
invoke the N-CREATE and the N-ACTION operations. The DICOM AEs that
claim conformance to this SOP Class as an SCP shall support the
N-CREATE, the N-ACTION and the N-GET operations.

.. _sect_S.3.2.1:

Create a Media Creation Request
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

The Create a Media Creation Request operation allows an SCU to create an
instance of the Media Creation Management SOP Class and initialize
Attributes of the SOP Class. The SCP uses this operation to create a new
media creation request containing the set of SOP Instances that shall be
included in the Interchange Media. This operation shall be invoked
through the N-CREATE primitive

.. _sect_S.3.2.1.1:

Attributes
''''''''''

The DICOM AEs that claim conformance to this SOP Class as an SCU may
choose to provide a subset of the Attributes maintained by the SCP. The
DICOM AEs that claim conformance to this SOP Class as an SCP shall
support a subset of the Media Creation Management specified in
`table_title <#table_S.3.2.1.1-1>`__.

.. table:: Media Creation Management - N-CREATE Attributes

   +--------------------------+-------------+--------------------------+
   | Attribute Name           | Tag         | Requirement Type SCU/SCP |
   +==========================+=============+==========================+
   | Specific Character Set   | (0008,0005) | 1C/1C (Required if       |
   |                          |             | expanded or replacement  |
   |                          |             | character set is used)   |
   +--------------------------+-------------+--------------------------+
   | Storage Media File-Set   | (0088,0130) | 3/3                      |
   | ID                       |             |                          |
   |                          |             | See `Storage Media       |
   |                          |             | File-Set                 |
   |                          |             | Attributes               |
   |                          |             |  <#sect_S.3.2.1.1.1>`__. |
   +--------------------------+-------------+--------------------------+
   | Storage Media File-Set   | (0088,0140) | 3/3                      |
   | UID                      |             |                          |
   |                          |             | See `Storage Media       |
   |                          |             | File-Set                 |
   |                          |             | Attributes               |
   |                          |             |  <#sect_S.3.2.1.1.1>`__. |
   +--------------------------+-------------+--------------------------+
   | Label Using Information  | (2200,0001) | 3/1C                     |
   | Extracted From Instances |             |                          |
   |                          |             | See                      |
   |                          |             | `Labeling                |
   |                          |             |  <#sect_S.3.2.1.1.4>`__. |
   +--------------------------+-------------+--------------------------+
   | Label Text               | (2200,0002) | 3/1C                     |
   |                          |             |                          |
   |                          |             | See                      |
   |                          |             | `Labeling                |
   |                          |             |  <#sect_S.3.2.1.1.4>`__. |
   +--------------------------+-------------+--------------------------+
   | Label Style Selection    | (2200,0003) | 3/1C                     |
   |                          |             |                          |
   |                          |             | See                      |
   |                          |             | `Labeling                |
   |                          |             |  <#sect_S.3.2.1.1.4>`__. |
   +--------------------------+-------------+--------------------------+
   | Barcode Value            | (2200,0005) | 3/3                      |
   |                          |             |                          |
   |                          |             | See                      |
   |                          |             | `Labelin                 |
   |                          |             | g <#sect_S.3.2.1.1.4>`__ |
   +--------------------------+-------------+--------------------------+
   | Barcode Symbology        | (2200,0006) | 3/3                      |
   |                          |             |                          |
   |                          |             | See                      |
   |                          |             | `Labelin                 |
   |                          |             | g <#sect_S.3.2.1.1.4>`__ |
   +--------------------------+-------------+--------------------------+
   | Media Disposition        | (2200,0004) | 3/3                      |
   |                          |             |                          |
   |                          |             | See `Media               |
   |                          |             | Disposition              |
   |                          |             |  <#sect_S.3.2.1.1.5>`__. |
   +--------------------------+-------------+--------------------------+
   | Allow Media Splitting    | (2200,0007) | 3/1C                     |
   |                          |             |                          |
   |                          |             | See `Allow Media         |
   |                          |             | Splittin                 |
   |                          |             | g <#sect_S.3.2.1.1.6>`__ |
   +--------------------------+-------------+--------------------------+
   | Allow Lossy Compression  | (2200,000F) | 3/1C                     |
   |                          |             |                          |
   |                          |             | See `Allow Lossy         |
   |                          |             | Compressio               |
   |                          |             | n <#sect_S.3.2.1.1.9>`__ |
   +--------------------------+-------------+--------------------------+
   | Include Non-DICOM        | (2200,0008) | 3/1C                     |
   | Objects                  |             |                          |
   |                          |             | See `Include Non-DICOM   |
   |                          |             | Object                   |
   |                          |             | s <#sect_S.3.2.1.1.7>`__ |
   +--------------------------+-------------+--------------------------+
   | Include Display          | (2200,0009) | 3/1C                     |
   | Application              |             |                          |
   |                          |             | See `Include Display     |
   |                          |             | Applicatio               |
   |                          |             | n <#sect_S.3.2.1.1.8>`__ |
   +--------------------------+-------------+--------------------------+
   | Preserve Composite       | (2200,000A) | 3/3                      |
   | Instances After Media    |             |                          |
   | Creation                 |             |                          |
   +--------------------------+-------------+--------------------------+
   | Referenced SOP Sequence  | (0008,1199) | 1/1                      |
   +--------------------------+-------------+--------------------------+
   | >Referenced SOP Class    | (0008,1150) | 1/1                      |
   | UID                      |             |                          |
   +--------------------------+-------------+--------------------------+
   | >Referenced SOP Instance | (0008,1155) | 1/1                      |
   | UID                      |             |                          |
   +--------------------------+-------------+--------------------------+
   | >Requested Media         | (2200,000C) | 3/1                      |
   | Application Profile      |             |                          |
   |                          |             | See `Requested Media     |
   |                          |             | Application              |
   |                          |             | Profile                  |
   |                          |             |  <#sect_S.3.2.1.1.2>`__. |
   +--------------------------+-------------+--------------------------+
   | >Icon Image Sequence     | (0088,0200) | 3/1C                     |
   |                          |             |                          |
   |                          |             | See `Icon Image          |
   |                          |             | Sequence                 |
   |                          |             |  <#sect_S.3.2.1.1.3>`__. |
   +--------------------------+-------------+--------------------------+

.. _sect_S.3.2.1.1.1:

Storage Media File-Set Attributes
                                 

If present, the Storage Media File-Set ID (0088,0130) and Storage Media
File-Set UID (0088,0140) shall be used on the media created. If absent,
the media shall contain values generated by the SCP.

If the media request will not fit on a single volume (single piece or
side of media), then whether or not the SCP ignores Storage Media
File-Set ID (0088,0130), or uses it as a prefix and appends information
to distinguish volumes, is implementation dependent. Different values of
Storage Media File-Set UID (0088,0140) shall be used for different
volumes.

If multiple copies are requested, the same Storage Media File-Set ID
(0088,0130) and Storage Media File-Set UID (0088,0140) shall be used on
all copies.

.. note::

   Care should be taken with multiple copies written to rewritable media
   that their contents do not diverge even though their identifiers are
   identical.

.. _sect_S.3.2.1.1.2:

Requested Media Application Profile
                                   

The Requested Media Application Profile (2200,000C), if present, shall
be used by the SCP for the specified SOP Instance. If absent for a
particular instance, the choice of Media Application Profile for that
instance shall be at the discretion of the SCP.

.. note::

   1. Different Media Application Profiles may be used for different
      instances on the same piece of media.

   2. The form of the DICOMDIR directory records that the SCP must
      create may be significantly influenced by the media application
      profiles used.

.. _sect_S.3.2.1.1.3:

Icon Image Sequence
                   

The Icon Image Sequence (0088,0200), if present:

-  shall be used by the SCP for inclusion in the instance-level DICOM
   Directory Record for the specified SOP Instance, if the Media
   Application Profile requires its inclusion, and the icon supplied by
   the SCU meets the requirements of the profile

-  may be used by the SCP for inclusion in the instance-level DICOM
   Directory Record for the specified SOP Instance, if the Media
   Application Profile does not require its inclusion

If absent for a particular instance, the choice of Media Application
Profile for that instance dictates whether or not the SCP is required to
create its own Icon Image Sequence (0088,0200) from the contents of the
SOP Instance.

.. note::

   1. Some Media Application Profiles require the inclusion of an Icon
      Image Sequence (0088,0200) in the directory records.

   2. Some Media Application Profiles specify constraints on the form of
      the Icon Image Sequence (0088,0200).

   3. The SCP may choose to extend the Media Application Profile by
      generating and including icons anyway.

.. _sect_S.3.2.1.1.4:

Labeling
        

The SCP may or may not have the capability to print a label on (or for)
the media. If it does, then the following SCP behavior shall apply and
the specified Attributes are required to be supported by the SCP.

The Label Using Information Extracted From Instances (2200,0001)
Attribute is a flag that instructs the SCP whether or not to create any
label using the Patient and Study information contained within the
instances themselves.

.. note::

   The SCP may implement whatever it considers to be an appropriate
   subset of any Attributes of any Modules at the Patient, Specimen and
   Study entities in the DICOM Information Model specified in .
   Typically included are such Attributes as Patient Name (0010,0010),
   Patient ID (0010,0020), Study ID (0020,0010), and Study Date
   (0008,0020).

The Label Text (2200,0002) Attribute is additional text that the SCP
shall include on any label, either in addition to or instead of any
extracted demographics, depending on the value of Label Using
Information Extracted From Instances (2200,0001).

The Label Style Selection (2200,0003) Attribute is a code string, which
if present, may be used by the SCP to choose one or more
implementation-dependent styles of labeling.

The Barcode Value (2200,0005) and the Barcode Symbology (2200,0006), if
present, may be used by the SCP to print a barcode on the label.

Note It is SCU responsibility to convey a value for the Barcode Value
(2200,0005) Attribute consistent in length and content with the
requested Barcode Symbology (2200,0006).

.. _sect_S.3.2.1.1.5:

Media Disposition
                 

The Media Disposition (2200,0004), if present, may be used by the SCP to
determine where and to whom to send the media when completed.

.. note::

   For example, it may contain the name and address of a referring
   doctor, and be used to print a label for an envelope or mailer, or as
   additional material to be printed on the media label.

.. _sect_S.3.2.1.1.6:

Allow Media Splitting
                     

The SCP may or may not have the capability to split a request over more
than one piece of media (e.g., if it doesn't fit on one). If it does,
then the following SCP behavior shall apply and the specified Attributes
are required to be supported by the SCP.

The Allow Media Splitting Attribute (2200,0007) shall be used by the SCP
to determine if it is permitted to split this request over more than one
piece of media.

.. note::

   1. If the file-set size exceeds the media storage capacity, and this
      flag has been set to NO, the SCP shall refuse to process the
      request.

   2. If the requested Media Application Profile allows for lossless
      compression, and images are not already compressed, such
      compression may be applied by the SCP in order to fit all
      instances on a single piece of media. This also applies to lossy
      compression if it has not been allowed by the value of Allow Lossy
      Compression (2200,000F).

.. _sect_S.3.2.1.1.7:

Include Non-DICOM Objects
                         

The SCP may or may not have the capability to include on the created
media additional Non-DICOM objects (e.g., HTML files, JPEG images) that
are a rendering of the DICOM instances. If it does, then the following
SCP behavior shall apply and the specified Attributes are required to be
supported by the SCP.

The Include Non-DICOM Objects (2200,0008) shall be used to request the
SCP to add additional Non-DICOM objects onto the created media.

An SCP is not required to be able to add such files. Inability to add
Non-DICOM objects is not an error.

If Include Non-DICOM Objects (2200,0008) is set to NO, the SCP shall not
include additional non-DICOM objects on the media.

.. _sect_S.3.2.1.1.8:

Include Display Application
                           

The SCP may or may not have the capability to include on the created
media an application for displaying DICOM instances. If it does, then
the following SCP behavior shall apply and the specified Attributes are
required to be supported by the SCP.

The Include Display Application (2200,0009) shall be used to request the
SCP to add an application for displaying DICOM instances onto the
created media.

An SCP is not required to be able to add such an application. Inability
to add a display application is not an error.

Whether the display application is capable of displaying all stored
instances is beyond the scope of the Standard.

Whether the display application automatically executes when media is
inserted for reading is beyond the scope of the Standard.

Which platforms are supported by the display application(s) is beyond
the scope of the Standard.

.. note::

   Multiple files may need to be included in the media to support the
   display application, rather than a single executable file, and these
   may be present, even if the Include Non-DICOM Objects (2200,0008)
   Attribute has a value of NO.

If Include Display Application (2200,0009) is set to NO, the SCP shall
not include a display application on the media.

.. _sect_S.3.2.1.1.9:

Allow Lossy Compression
                       

If Allow Lossy Compression (2200,000F) has a value of YES, the SCP is
allowed to perform lossy compression under the following circumstances:

-  if it receives uncompressed or lossless compressed images yet is
   requested to use a profile that requires lossy compression, or

-  if Allow Media Splitting (2200,0007) is NO, and the request would
   otherwise need to be split across media.

If Allow Lossy Compression (2200,000F) has a value of YES but the
requested profile does not permit lossy compression, lossy compression
shall not be performed.

The level of compression is at the SCP's discretion.

The SCP shall not decompress and recompress already lossy compressed
images, but may use images that have already been lossy compressed.

The SCP is never required to perform lossy compression.

If Allow Lossy Compression (2200,000F) has a value of NO, the SCP is not
allowed to perform lossy compression. If Allow Lossy Compression
(2200,000F) has a value of NO and the requested profile requires lossy
compression, an error shall be returned.

.. _sect_S.3.2.1.2:

Service Class User Behavior
'''''''''''''''''''''''''''

The SCU shall use the N-CREATE primitive to inform the SCP that a new
media creation request has been placed and to convey the proprieties of
this request. The request proprieties (e.g., the set of SOP Instances
that the creating interchange media shall contain) are referenced in the
IOD Attributes as specified in `table_title <#table_S.3.2.1.1-1>`__.

Upon receipt of a successful N-CREATE Response Status Code from the SCP,
the SCU now knows that the SCP has received the N-CREATE request and a
new media creation request has been created.

Upon receipt of a failure N-CREATE Response Status Code from the SCP,
the SCU now knows that the SCP will not process the request. The actions
taken by the SCU upon receiving the status is beyond the scope of this
Standard.

At any time after receipt of the N-CREATE-Response, the SCU may release
the association on which it sent the N-CREATE-Request.

.. note::

   An N-GET of the corresponding of the Media Creation Management SOP
   Class may be performed on the same or subsequent associations.

.. _sect_S.3.2.1.3:

Service Class Provider Behavior
'''''''''''''''''''''''''''''''

Upon receipt of the N-CREATE request, the SCP shall return, via the
N-CREATE response primitive, the N-CREATE Response Status Code
applicable to the associated request. A success status conveys that the
SCP has successfully received the N-CREATE request.

Warning statuses shall not be returned.

Any other status (i.e., a failure status) conveys that the SCP is not
processing the media creation request.

.. note::

   1. It is not specified by the Standard what checks the SCP shall
      accomplish after the N-CREATE request primitive reception and
      before returning the N-CREATE response. Implementations are
      discouraged from performing extended validation of the contents of
      the N-CREATE request, such as availability of the referenced
      Composite SOP Instances, support for the requested profiles, etc.
      In case of N-CREATE failure, the SCU would not be able to perform
      an N-GET to determine the detailed reasons for failure, and allow
      operators to apply suitable correction actions to make the request
      processable (e.g., resending any missing Composite SOP Instances).
      Such checks are better deferred until after receipt of the
      N-ACTION request, after which an N-GET may be performed.

   2. The Standard does not require the SCP to queue multiple requests,
      though implementations are encouraged to do so. As a consequence,
      a new request before a previous request has been completed may
      fail immediately, or may return a successful response and be
      queued. The size of any such queue is beyond the scope of the
      Standard.

   3. How long the instance of the Media Creation Management SOP Class
      persists once the Execution Status (2100,0020) has been set to
      IDLE is beyond the scope of the Standard.

The N-CREATE implicitly creates the Execution Status (2100,0020) and
Execution Status Info (2100,0030) Attributes, which may subsequently be
retrieved by an N-GET.

.. _sect_S.3.2.1.4:

Status Codes.
'''''''''''''

`table_title <#table_S.3.2.2.4-1>`__ defines the specific status code
values that might be returned in a N-CREATE response. See for general
response status codes.

.. table:: SOP Class Status Values

   +----------------+-------------------------------------+-------------+
   | Service Status | Further Meaning                     | Status Code |
   +================+=====================================+=============+
   | Failure        | Failed: An Initiate Media Creation  | A510        |
   |                | action has already been received    |             |
   |                | for this SOP Instance.              |             |
   +----------------+-------------------------------------+-------------+

.. _sect_S.3.2.2:

Initiate Media Creation
^^^^^^^^^^^^^^^^^^^^^^^

The Initiate Media Creation operation allows an SCU to request an SCP to
create Interchange Media according to an already created Media Creation
Management SOP Instance. An SCP shall use this operation to schedule the
creation of Interchange Media. This operation shall be invoked through
the N-ACTION primitive.

.. _sect_S.3.2.2.1:

Action Information
''''''''''''''''''

The DICOM AEs that claim conformance to this SOP Class as an SCU and/or
an SCP shall support the Action Types and Action Information as
specified in `table_title <#table_S.3.2.2.1-1>`__.

.. table:: Media Creation Request - Action Information

   +-------------+-------------+-------------+-------------+-------------+
   | Action Type | Action Type | Attribute   | Tag         | Requirement |
   | Name        | ID          | Name        |             | Type        |
   |             |             |             |             | SCU/SCP     |
   +=============+=============+=============+=============+=============+
   | Initiate    | 1           | Number of   | (2000,0010) | 3/1         |
   | Media       |             | Copies      |             |             |
   | Creation    |             |             |             |             |
   +-------------+-------------+-------------+-------------+-------------+
   | Request     | (2200,0020) | 3/3         |             |             |
   | Priority    |             |             |             |             |
   |             |             | See         |             |             |
   |             |             | `Priority   |             |             |
   |             |             | <#sect_S.3. |             |             |
   |             |             | 2.2.1.1>`__ |             |             |
   +-------------+-------------+-------------+-------------+-------------+

.. _sect_S.3.2.2.1.1:

Priority
        

The Request Priority (2200,0020), if present, may be used by the SCP to
prioritize a higher priority request over other pending lower priority
requests.

.. _sect_S.3.2.2.2:

Service Class User Behavior
'''''''''''''''''''''''''''

The SCU shall use the N-ACTION primitive to request the SCP to create
Interchange Media according to an already created Media Creation
Management SOP Instance. Action Information is specified in Table S.
3.2.2.1-1.

Upon receipt of a successful N-ACTION Response Status Code from the SCP,
the SCU now knows that the SCP has received the N-ACTION Initiate Media
Creation request and will process the request.

Upon receipt of a failure N-ACTION Response Status Code from the SCP,
the SCU now knows that the SCP will not process the Initiate Media
Creation request. The actions taken by the SCU upon receiving the status
is beyond the scope of this Standard.

At any time after receipt of the N-ACTION-Response, the SCU may release
the association on which it sent the N-ACTION-Request.

.. note::

   1. An N-GET of the corresponding of the Media Creation Management SOP
      Class may be performed on the same or subsequent associations.

   2. The duration for which the SOP Instance UID of an instance of the
      Media Creation Management SOP Class remains active once the
      request has been completed or has failed is implementation
      dependent, but should be sufficiently long to allow an SCU to
      determine the ultimate outcome of the request.

.. _sect_S.3.2.2.3:

Service Class Provider Behavior
'''''''''''''''''''''''''''''''

Upon receipt of the N-ACTION Initiate Media Creation request, the SCP
shall return, via the N-ACTION response primitive, the N-ACTION Response
Status Code applicable to the associated request. A success status
conveys that the SCP has successfully scheduled the request.

.. note::

   1. The extent of validation of the contents of the request, the
      availability of the referenced Composite SOP Instances, support
      for the requested profiles and other checks that may determine the
      ultimate success or failure of the request are not specified by
      the Standard. In particular, a request may be immediately accepted
      successfully, but subsequently fail for some reason, or the
      N-ACTION response primitive may contain a status that reflects a
      more thorough (and prolonged) check.

   2. How long any Composite Instances that have been transferred via
      the Storage Service Class to the SCP for the purpose of a Media
      Creation Request persist, is beyond the scope of the Standard. The
      Preserve Composite Instances After Media Creation (2200,000A) flag
      is provided as a hint only. Even if this flag is set, a subsequent
      request referencing some or all of the same instances may fail if
      the SCP had reason to flush its cache of instances in the interim,
      and the SCU may need to be prepared to re-send them.

   3. How long the instance of the Media Creation Management SOP Class
      persists once the Execution Status (2100,0020) has been set to
      DONE or FAILED is beyond the scope of the Standard.

The N-ACTION implicitly creates or updates the Execution Status
(2100,0020), Execution Status Info (2100,0030), Total Number of Pieces
of Media Created (2200,000B), Failed SOP Sequence (0008,1198) and
Referenced Storage Media Sequence (2200,000D) Attributes, which may
subsequently be retrieved by an N-GET.

.. _sect_S.3.2.2.4:

Status Codes
''''''''''''

There are no specific status codes. See for response status codes.

.. _sect_S.3.2.3:

Cancel Media Creation
^^^^^^^^^^^^^^^^^^^^^

The Cancel Media Creation operation allows an SCU to request an SCP to
cancel a media creation request, whether or not it has begun to be
processed. This operation shall be invoked through the N-ACTION
primitive.

.. _sect_S.3.2.3.1:

Action Information
''''''''''''''''''

The DICOM AEs that claim conformance to this SOP Class as an SCU and/or
an SCP shall support the Action Types and Action Information as
specified in `table_title <#table_S.3.2.3.1-1>`__.

.. table:: Media Creation Request - Action Information

   +---------------+---------------+---------------+-----+---------------+
   | Action Type   | Action Type   | Attribute     | Tag | Requirement   |
   | Name          | ID            | Name          |     | Type SCU/SCP  |
   +===============+===============+===============+=====+===============+
   | Cancel Media  | 2             |               |     |               |
   | Creation      |               |               |     |               |
   +---------------+---------------+---------------+-----+---------------+

.. _sect_S.3.2.3.2:

Service Class User Behavior
'''''''''''''''''''''''''''

The SCU shall use the N-ACTION primitive to request the SCP to cancel
the media creation request corresponding to the Affected SOP Instance
UID in the N-ACTION request primitive, whether or not it has been
initiated with an N-ACTION Initiate Media Creation request, and whether
or not it has begun to be processed (i.e., is pending or in progress).

Upon receipt of a successful N-ACTION Response Status Code from the SCP,
the SCU knows that the SCP has received the N-ACTION Cancel Media
Creation request, has canceled any pending or in progress media
creation, and deleted the Media Creation Management SOP Instance.

.. note::

   Successful cancellation implies that a subsequent N-GET of the
   corresponding Media Creation Management SOP Instance would fail.

Upon receipt of a failure N-ACTION Response Status Code from the SCP,
the SCU knows that the SCP will not process the Cancel Media Creation
request. The actions taken by the SCU upon receiving the status is
beyond the scope of this Standard.

.. note::

   Cancellation failure implies that media creation has already
   completed (successfully or not), or will proceed. The status of the
   media creation request may still be obtained with an N-GET, unless
   the reason for failure was that the SOP Instance did not exist.

.. _sect_S.3.2.3.3:

Service Class Provider Behavior
'''''''''''''''''''''''''''''''

Upon receipt of the N-ACTION Cancel Media Creation request, the SCP
shall return, via the N-ACTION response primitive, the N-ACTION Response
Status Code applicable to the associated request. A success status
conveys that the SCP has successfully canceled the request.

A failure status conveys that the SCP has failed to cancel the request,
in which case the Execution Status (2100,0020), Execution Status Info
(2100,0030), Total Number of Pieces of Media Created (2200,000B), Failed
SOP Sequence (0008,1198) and Referenced Storage Media Sequence
(2200,000D) Attributes may subsequently be retrieved by an N-GET.

.. _sect_S.3.2.3.4:

Status Codes
''''''''''''

`table_title <#table_S.3.2.3.4-1>`__ defines the specific status code
values that might be returned in a N-ACTION response. See for general
response status codes.

.. table:: Response Statuses

   +--------------------------+--------------------------+--------------+
   | Service Status           | Further Meaning          | Status Codes |
   +==========================+==========================+==============+
   | Failure                  | Failed: Media creation   | C201         |
   |                          | request already          |              |
   |                          | completed.               |              |
   +--------------------------+--------------------------+--------------+
   | Failed: Media creation   | C202                     |              |
   | request already in       |                          |              |
   | progress and cannot be   |                          |              |
   | interrupted.             |                          |              |
   +--------------------------+--------------------------+--------------+
   | Failed: Cancellation     | C203                     |              |
   | denied for unspecified   |                          |              |
   | reason.                  |                          |              |
   +--------------------------+--------------------------+--------------+

.. _sect_S.3.2.4:

Get Media Creation Result
^^^^^^^^^^^^^^^^^^^^^^^^^

The Get Media Creation Result operation allows an SCU to request of an
SCP the status of a media creation request. This operation shall be
invoked through the N-GET primitive used in conjunction with the
appropriate Media Creation Management SOP Instance corresponding to the
creation request.

.. _sect_S.3.2.4.1:

Attributes
''''''''''

The Application Entity that claims conformance to this SOP Class as an
SCU may choose to interpret the Attributes maintained by the SCP that
the SCU receives via the operations of the SOP Class. The Application
Entity that claims conformance as an SCP to this SOP Class shall support
the Attributes specified in `table_title <#table_S.3.2.4.1-1>`__.

.. table:: Media Creation Management SOP Class N-GET Attributes

   +--------------------------+-------------+--------------------------+
   | Attribute Name           | Tag         | Requirement Type         |
   |                          |             | (SCU/SCP)                |
   +==========================+=============+==========================+
   | Specific Character Set   | (0008,0005) | 3/1C                     |
   |                          |             |                          |
   |                          |             | (Required if expanded or |
   |                          |             | replacement character    |
   |                          |             | set is used)             |
   +--------------------------+-------------+--------------------------+
   | Execution Status         | (2100,0020) | 3/1                      |
   +--------------------------+-------------+--------------------------+
   | Execution Status Info    | (2100,0030) | 3/1                      |
   +--------------------------+-------------+--------------------------+
   | Total Number of Pieces   | (2200,000B) | 3/1                      |
   | of Media Created         |             |                          |
   +--------------------------+-------------+--------------------------+
   | Failed SOP Sequence      | (0008,1198) | 3/2                      |
   +--------------------------+-------------+--------------------------+
   | Referenced Storage Media | (2200,000D) | 3/2                      |
   | Sequence                 |             |                          |
   +--------------------------+-------------+--------------------------+
   | *All Other Attributes of |             | 3/3                      |
   | the*                     |             |                          |
   +--------------------------+-------------+--------------------------+

.. _sect_S.3.2.4.2:

Service Class User
''''''''''''''''''

The SCU shall specify in the N-GET request primitive the UID of the
Media Creation Management SOP Instance for which Attribute Values are to
be returned. The SCU shall be permitted to request that Attribute Values
be returned for any Media Creation Management SOP Class Attribute
specified in `Attributes <#sect_S.3.2.1.1>`__. Additionally, values may
be requested for optional Media Creation Management Module Attributes.

The SCU shall specify the list of Media Creation Management SOP Class
Attributes for which the Attribute Values are to be returned. The
encoding rules for this list are specified in the N-GET request
primitive specified in .

In an N-GET operation, Sequence Attributes can only be requested in
their entirety, and only the top level Sequence Attribute can be
included in the request.

The SCU shall be capable of receiving all requested Attribute Values
provided by the SCP in response to the N-GET indication primitive. The
SCU may request Attribute Values for optional Attributes that are not
maintained by the SCP. In such a case the SCU shall function properly
regardless of whether the SCP returns values for those Attributes or
not. This Service Class Specification places no requirements on what the
SCU shall do as a result of receiving this information.

.. note::

   In order to interpret accurately the character set used for Attribute
   Values returned, it is recommended that the Attribute Value for
   Specific Character Set (0008,0005) be requested in the N-GET request
   primitive.

.. _sect_S.3.2.4.3:

Service Class Provider
''''''''''''''''''''''

This operation allows the SCU to request from the SCP, selected
Attribute Values for a specific Media Creation Management SOP Instance.
This operation shall be invoked through the use of the DIMSE N-GET
Service used in conjunction with the appropriate Media Creation
Management SOP Instance.

The SCP shall return, via the N-GET response primitive, the N-GET
Response Status Code applicable to the associated request. Contingent on
the N-GET Response Status, the SCP shall return, via the N-GET Response
Primitive, Attribute Values for all requested Attributes maintained by
the SCP (see `table_title <#table_S.3.2.4.1-1>`__). The SCP shall not
return Data Elements for optional Attributes that are not maintained by
the SCP.

The SCP shall return the entire content of a Sequence if a Sequence
Attribute is requested.

.. _sect_S.3.2.4.4:

Status Codes
''''''''''''

`table_title <#table_S.3.2.4.4-1>`__ defines the specific status code
values that might be returned in a N-GET response.

See for general response status codes.

.. table:: Response Statuses

   +----------------+-------------------------+-----------------------+
   | Service Status | Further Meaning         | Response Status Codes |
   +================+=========================+=======================+
   | Warning        | Requested optional      | 0001                  |
   |                | Attributes are not      |                       |
   |                | supported               |                       |
   +----------------+-------------------------+-----------------------+

.. _sect_S.3.3:

Media Creation Management SOP Class UID
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

The Media Creation Management SOP Class shall be uniquely identified by
the Media Creation Management SOP Class UID, which shall have the value
"1.2.840.10008.5.1.1.33".

.. _sect_S.4:

Conformance Requirements
------------------------

Implementations claiming Standard SOP Class Conformance to the Media
Creation Management SOP Class shall be conformant as described in this
Section and shall include within their Conformance Statement information
as described in this Section and sub-Sections.

An implementation may claim conformance to this SOP Class as an SCU, SCP
or both. The Conformance Statement shall be in the format defined in .

.. _sect_S.4.1:

SCU Conformance
~~~~~~~~~~~~~~~

An implementation that is conformant to this SOP Class as an SCU shall
meet conformance requirements for

-  the operations and actions that it invokes

The mechanisms used by the SCU to transfer SOP Instances to the SCP
using the Storage Service Class prior to initiating a request operation
shall also be documented, and in particular the Transfer Syntaxes that
may be proposed.

.. _sect_S.4.1.1:

Operations
^^^^^^^^^^

The SCU shall document in the Conformance Statement the actions and
behavior that cause the SCU to generate an N-CREATE primitive (Create
Media Creation Request), an N-ACTION primitive (Initiate Media Creation
and Cancel Media Creation) or an N-GET primitive (Get Media Creation
Result).

The SCU shall specify the SOP Class UIDs for which it may request media
creation.

The SCU shall specify the Media Application Profiles for which it may
request media creation.

The SCU shall specify if it supports the optional Storage Media File-Set
ID & UID Attributes in the N-CREATE.

The SCU shall specify if it supports the optional Icon Image Sequence
Attributes in the N-CREATE.

The SCU shall describe its use of expanded or replacement character
sets, both in the N-CREATE, the N-GET and in its use of the Storage
Service Class for composite instances.

The SCU shall specify whether or not it retries failed requests.

.. note::

   This allows the reader of a Conformance Statement to determine
   whether or not human intervention will be needed in the event of
   transient failures, or whether the SCU may be able to recover
   automatically.

The Conformance Statement shall be formatted as defined in

.. _sect_S.4.2:

SCP Conformance
~~~~~~~~~~~~~~~

An implementation that is conformant to this SOP Class as an SCP shall
meet conformance requirements for

-  the operations and actions that it performs

The Storage Service Class mechanisms accepted by the SCP prior to
receiving a request operation shall also be documented, and in
particular the Transfer Syntaxes that may be accepted.

.. _sect_S.4.2.1:

Operations
^^^^^^^^^^

The SCP shall document in the Conformance Statement the behavior and
actions of the SCP upon receiving the N-CREATE primitive (Create Media
Creation Request), N-ACTION primitive (Initiate Media Creation and
Cancel Media Creation) or the N-GET primitive (Get Media Creation
Result).

The SCP shall specify the SOP Class UIDs for which it will accept media
creation requests.

The SCP shall specify the Media Application Profiles for which it will
accept media creation requests, and what default profiles it will use in
the event that they are not specified by the SCU.

.. note::

   The forms of media that can be created are implicit in the list of
   Media Application Profiles supported, each of which is
   media-specific.

The SCP shall specify whether or not it supports creation of optional
Icon Image Sequence Attributes in the DICOMDIR if none are supplied by
the SCU.

The SCP shall specify the manner of use of label information, and in
particular which:

-  Attributes are extracted from the Composite Instances when so
   instructed

-  barcode symbologies - if any - are supported

The SCP shall describe its use of expanded or replacement character
sets, both in the N-CREATE, the N-GET and in its extraction of
information from the Composite Instances for incorporation in the
DICOMDIR and on the media label. The SCP shall describe its use of the
Attributes both in the N-CREATE, and N-ACTION and the Composite
Instances to create the media label.

The SCP shall specify if and how it supports the following optional
Attributes in the N-CREATE and N-ACTION:

-  Storage Media File-Set ID (0088,0130) & Storage Media File-Set UID
   (0088,0140)

-  Media Disposition (2200,0004)

-  Priority (2000,0020)

-  Preserve Composite Instances After Media Creation (2200,000A)

The SCP shall specify the duration of persistence of received Composite
Instances after a request has been processed successfully or
unsuccessfully.

The SCP shall specify how long it will maintain:

-  the result of the creation of media after the request has succeeded
   or failed

-  the Media Creation Management Instances whose status is IDLE.

The SCP shall specify the action taken when a permanent failure (e.g., a
media writing failure) or a transient failure (e.g., no empty media
available) occurs, and their relationship with the media creation
request status transaction.

.. note::

   For example, how many times the SCP will retry writing a new piece of
   media before setting the Execution Status (2100,0020) to FAILURE, how
   many media creation requests the SCP is able to queue, the SCP
   behavior when the request queue, if any, is full.

The SCP shall specify if it is able to split a media creation request
over more than one piece of media, if the file-set doesn't fit on one.

The SCP shall specify if it is able to add to the created media
Non-DICOM objects (e.g., html files, JPEG images), how these objects are
organized, and how it interprets the Include Non-DICOM Objects
(2200,0008) Attribute.

The SCP shall specify if it is able to add to the created media DICOM
display applications, and how it interprets the Include Display
Application (2200,0009) Attribute.

The Conformance Statement shall be formatted as defined in .

