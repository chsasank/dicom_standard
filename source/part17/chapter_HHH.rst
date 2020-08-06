.. _chapter_HHH:

Transition from WADO to RESTful Services (Informative)
======================================================

This annex discusses the design considerations that went into the
definition of the WADO extension to Web and REST services.

.. _sect_HHH.1:

Request and Response Parameters
-------------------------------

.. _sect_HHH.1.1:

Request Parameters
~~~~~~~~~~~~~~~~~~

The WADO-RS and STOW-RS requests have no parameters because data is
requested through well defined URLs and content negotiation through HTTP
headers.

.. table:: Summary of DICOM/Rendered URI Based WADO Parameters

   ========================= ================ ======================
   Parameter                 Allowed for      Requirement in Request
   ========================= ================ ======================
   requestType               DICOM & Rendered Required
   studyUID                  DICOM & Rendered Required
   seriesUID                 DICOM & Rendered Required
   objectUID                 DICOM & Rendered Required
   contentType               DICOM & Rendered Optional
   charset                   DICOM & Rendered Optional
   anonymize                 DICOM            Optional
   annotation                Rendered         Optional
   Rows, columns             Rendered         Optional
   region                    Rendered         Optional
   windowCenter, windowWidth Rendered         Optional
   imageQuality              DICOM & Rendered Optional
   presentationUID           Rendered         Optional
   presentationSeriesUID     Rendered         Optional
   transferSyntax            DICOM            Optional
   frameNumber               DICOM & Rendered Optional
   ========================= ================ ======================

.. _sect_HHH.1.2:

Response Parameters
~~~~~~~~~~~~~~~~~~~

.. _sect_HHH.1.2.1:

URI WADO-URI
^^^^^^^^^^^^

In the URI based WADO, the response is the single payload returned in
the HTTP Get response. It may be the DICOM object in a DICOM format or
in a rendered format.

.. _sect_HHH.1.2.2:

Retired
^^^^^^^

See PS3.17-2017b.

.. _sect_HHH.1.2.3:

WADO-RS
^^^^^^^

The WADO-RS Service is a transport service, as opposed to a rendering
service, which provides resources that enable machine to machine
transfers of binary instances, pixel data, bulk data, and metadata.
These services are not primarily intended to be directly displayable in
a browser.

In the REST Services implementation:

-  For the "DICOM Requester", one or more multipart/related parts are
   returned containing binary DICOM instances of a Study, Series, or a
   single Instance.

-  For the "Frame Pixel Data Requester", one or more multipart/related
   parts are returned containing the pixel data of a multi-frame SOP
   Instance.

-  For the "Bulk Data Requester", one or more multipart/related parts
   are returned containing the bulk data of a Study, Series or SOP
   Instance.

-  For the "Metadata Requester", an item is returned containing the XML
   encoded metadata selected from the retrieved objects header as
   described in the Native DICOM Model defined in .

.. _sect_HHH.1.2.4:

STOW-RS
^^^^^^^

The STOW-RS Service provides the ability to STore Over the Web using
RESTful Services (i.e., HTTP based functionality equivalent to C-Store).

-  For the "DICOM Creator", one or more multipart/related parts are
   stored (posted to a STOW-RS Service) containing one or more DICOM
   Composite SOP Instances.

-  For the "Metadata and Bulk Data Creator", one or more
   multipart/related parts are stored (posted to a STOW-RS Service)
   containing the XML encoded metadata defined in and one or more parts
   containing the bulk data of a Study, Series or SOP Instance.

.. _sect_HHH.2:

Web Services Implementation
---------------------------

The implementation architecture has to maximize interoperability,
preserve or improve performance and minimize storage overhead.

The Web Services technologies have been selected to:

a. be firewall friendly and supporting security,

b. be supported by and interoperable between multiple development
   environments, and

c. have sufficient performance for both large and small text and for
   binary data.

The WADO-RS response will be provided as a list of XML and/or binary
instances in a multipart/related response. The type of response depends
on the media types listed in the Accept header.

The STOW-RS response is a standard HTTP status line and possibly an XML
response message body. The meaning of the success, warning, or failure
statuses are defined in .

.. _sect_HHH.3:

Uses for Web Services
---------------------

.. _sect_HHH.3.1:

General Requirements
~~~~~~~~~~~~~~~~~~~~

Imaging information is important in the context of EMR/EHR. But EMR/EHR
systems often do not support the DICOM protocol. The EMR/EHR vendors
need access using web and web service technologies to satisfy their
users.

.. _sect_HHH.3.2:

Analysis of Use Cases
~~~~~~~~~~~~~~~~~~~~~

Examples of use cases / clinical scenarios, as the basis to develop the
requirements, include:

-  Providing access to images and reports from a point-of-service
   application e.g., EMR.

-  Following references to significant images used to create an imaging
   report and displaying those images.

-  Following references / links to relevant images and imaging reports
   in email correspondence or clinical reports e.g., clinical summary.

-  Providing access to anonymized DICOM images and reports for clinical
   research and teaching purposes.

-  Providing access to a DICOM encoded imaging report associated with
   the DICOM IE (patient/study/series/objects) to support remote
   diagnostic workflows e.g., urgent medical incidents, remote
   consultation, clinical training, teleradiology/telemedicine
   applications.

-  Providing access to summary or selected information from DICOM
   objects.

-  Providing access to complete studies for caching, viewing, or image
   processing.

-  Storing DICOM SOP Instances using HTTP over a Network from PACS to
   PACS, from PACS to VNA, from VNA to VNA, from clinical application to
   PACS, or any other DICOM SCP.

-  Web clients, including mobile ones, retrieving XML and bulk data from
   a WADO-RS Service and adding new instances to a study.

Examples of the use cases described in 1 above are:

a. The EMR displays in JPEG one image with annotations on it (patient
   and/or technique related), based upon information provided in a
   report.

b. The EMR retrieves from a "Manifest" document all the referenced
   objects in DICOM and launches a DICOM viewer for displaying them (use
   case addressed by the IHE XDS-I.b profile).

c. The EMR displays in JPEG one image per series with information
   describing every series (e.g., series description).

d. The EMR displays in JPEG all the images of a series with information
   describing the series as well as every image (e.g., instance number
   and slice location for scanner images).

e. The EMR populates in its database for all the instances referred in a
   manifest (KOS) the relevant information (study
   ID/UID/AccessionNumber/Description/DateTime, series
   UID/Modality/Description/DateTime, instance
   UID/InstanceNumber/SliceLocation).

f. The EMR displays patient demographics and image slices in a browser
   by accessing studies through URLs that are cached and rendered in a
   remote data center.

g. A hospital transfers a DICOM Study over a network to another
   healthcare provider without needing special ports opened in either
   firewall.

h. A diagnostic visualization client, during post-processing, adds a
   series of Instances containing measurements, annotations, or reports.

i. A healthcare provider transfers a DICOM Study to a Patient Health
   Record (PHR) at the request of the patient.

As an example, the 1c use case is decomposed in the following steps (all
the other use cases can be implemented through a similar sequence of
basic transactions):

A. The EMR sends to the DICOM server the list of the objects
   ("selection"), asking for the object content.

B. The DICOM server sends back the JPEG images corresponding to the
   listed objects.

C. The EMR sends to the DICOM server the "selection" information for
   obtaining the relevant information about the objects retrieved.

D. The DICOM server sends back the corresponding information in the form
   of a "metadata" document, converted in XML.

.. _sect_HHH.3.3:

Description of The Use Cases
~~~~~~~~~~~~~~~~~~~~~~~~~~~~

The use cases described above in terms of clinical scenarios correspond
to the following technical implementation scenarios. In each case the
use is distinguished by the capabilities of the requesting system:

-  Does it prefer the URI based requests, or the web-services based
   requests.

-  Does it have the ability to decode and utilize the DICOM format or
   not.

-  Does it need the metadata describing the image and its acquisition,
   and/or does it need an image to be displayed.

These then become the following technical use cases.

.. _sect_HHH.3.3.1:

URI Based WADO Use Case
^^^^^^^^^^^^^^^^^^^^^^^

A. The requesting system is Web Browser or other application that can
   make simple HTTP/HTTPS requests,

B. Reference information is provided as URL or similar information that
   can be easily converted into a URL.

C. The request specifies:

   1. Individual SOP Instance

   2. Desired format and subset selection for information to be returned

D. The Response provides

   1. SOP instance, reformatted and subset as requested. This may be
      encoded as a DICOM instance, or rendered into a generic image
      format such as JPEG.

.. _sect_HHH.3.3.2:

DICOM (Encoded Content) Requester
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

A. The requesting system is an application capable of making Web Service
   requests and able to process data encoded as a DICOM File, per DICOM
   encodings.

B. Reference information may come in a wide variety of forms. It is
   expected to include at least the Study UID, Series UID, and
   Individual SOP instance information. This may be encoded as part of
   an HL7 reference within a CDA document, a DICOM SOP Instance
   reference, or other formats.

C. The request specifies

   1. Requested Data set

      a. Study UID

      b. List of Series UID

      c. List of SOP Instance UIDs

   2. Optionally, it may also specify subset information

      a. Instance and Frame Level Retrieve SOP classes subset
         information for selecting frames

      b. No-pixel data request (using the Transfer Syntax parameter)

      c. Anonymization

D. The response provides

   1. SOP Instances, encoded per DICOM .

.. _sect_HHH.3.3.3:

Rendered (JPEG/PDF) Requester
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

A. The requesting system: application capable of making Web Service
   requests. System is not capable of decoding DICOM formats. The system
   is capable of processing images in JPEG or other more generic
   formats.

B. Reference information may come in a wide variety of forms. It is
   expected to include at least the Study UID, Series UID, and
   Individual SOP instance information. This may be encoded as part of
   an HL7 reference within a CDA document, a DICOM SOP Instance
   reference, or other formats.

C. Request information

   1. Requested Data set

      a. Study UID

      b. List of Series UID

      c. List of SOP Instance UIDs

   2. Desired format and subset information

      a. JPEG/PDF/etc. selection, subset area, presentation information

      b. Frame selection for subsets of multi-frame objects

      c. What should be done for requests where image shapes and SOP
         classes vary and a subset is requested?

      d. Anonymize or not.

D. Response information

   1. JPEGs

      a. Should JPEGs include tag information within the JPEG? If so,
         what information?

      b. How will JPEGs be related to multi-frame and multi-instance
         requests? Order? Tag?

   2. PDFs

      a. How will PDFs be related to multi-frame and multi-instance
         requests? One per frame? One per instance? One for entire set?

   3. Other encodings?

.. _sect_HHH.3.3.4:

Metadata (XML Without Pixel Data, Waveform Data, etc.) Requester
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

A. The requesting system: application capable of making Web Service
   requests. The requesting System is not capable of decoding DICOM
   formats. The system is capable of processing metadata that describes
   the image, provided that the metadata is encoded in an XML format.
   The system can be programmed based upon the DICOM definitions for XML
   encoding and Attribute meanings.

B. Reference information may come in a wide variety of forms. It is
   expected to include at least the Study UID, Series UID, and
   Individual SOP instance information. This may be encoded as part of
   an HL7 reference within a CDA document, a DICOM SOP Instance
   reference, or other formats.

C. Request information

   1. Requested Data set

      a. Study UID

      b. List of Series UID

      c. List of SOP Instance UIDs

   2. Desired format and subset information

      a. XPath definition for subset or total metadata selection

      b. What should be done when SOP classes vary and a subset is
         requested? The XPath will fail.

      c. Frame selection for subsets of multi-frame objects

      d. Anonymize or not.

      e. Response information

D. Response information

   1. XML encoded metadata.

.. _sect_HHH.3.3.5:

DICOM Requester
^^^^^^^^^^^^^^^

A. The requesting system is an application capable of making HTTP
   Service requests and able to process data encoded as a DICOM File,
   per DICOM encodings.

B. Requesting information for DICOM Instances may come from a wide
   variety of forms. It is expected to include at least the Study UID.
   This may be encoded as part of an HL7 reference within a CDA
   document, a DICOM SOP Instance reference, or other formats.

C. The request specifies

   1. Requested Data set

      a. Study UID

   2. Optionally, it may also specify subset information

      a. Series UID

      b. SOP Instance UID

D. The response provides

   1. SOP Instances, encoded per DICOM .

.. _sect_HHH.3.3.6:

Frame Pixel Data Requester
^^^^^^^^^^^^^^^^^^^^^^^^^^

A. The requesting system is an application capable of making HTTP
   requests and able to process pixel data.

B. Requesting information for pixel data may come in a wide variety of
   forms. It is expected to include at least the Study UID, Series UID,
   Individual SOP Instance, and Frame List information. This may be
   encoded as part of an HL7 reference within a CDA document, a DICOM
   SOP Instance reference, or other formats.

C. The request specifies

   1. Requested Data set

      a. Study UID

      b. Series UID

      c. SOP Instance UID

      d. Frame List comprised of one or more frame numbers

D. The response provides pixel data

.. _sect_HHH.3.3.7:

Bulk Data Requester
^^^^^^^^^^^^^^^^^^^

A. The requesting system is an application capable of making HTTP
   requests and able to process bulk data.

B. Requesting information for bulk data may come in a wide variety of
   forms. It is expected to include the Bulk Data URL as provided by the
   RetrieveMetadata resource. This may be encoded as part of an HL7
   reference within a CDA document, a DICOM SOP Instance reference, or
   other formats.

C. The request specifies

   1. Requested Data set

      a. Bulk Data URL

D. The response provides bulk data

.. _sect_HHH.3.3.8:

Metadata Requester
^^^^^^^^^^^^^^^^^^

A. The requesting system is an application capable of making HTTP
   requests and able to process data encoded as a XML, per DICOM
   encodings.

B. The Study UID may be obtained as part of an HL7 reference within a
   CDA document, a DICOM SOP Instance reference, or other formats.

C. Request information

   1. Requested Data set

      a. Study UID

D. The response provides full study metadata encoded in XML, encoded per
   DICOM .

.. _sect_HHH.3.3.9:

DICOM Creator
^^^^^^^^^^^^^

A. The requesting system is an application capable of making HTTP
   Service requests and able to process data encoded as binary
   instances.

B. The request specifies

   1. The STOW-RS Service to store POST requests.

   2. Optionally, it may also specify Study Instance UID indicating all
      POST requests are for the indicated study.

   3. SOP Instances, per DICOM encoding.

C. The response is a standard HTTP status line and an XML response
   message body. The meaning of the success, warning, or failure
   statuses are defined in .

.. _sect_HHH.3.3.10:

Metadata and Bulk Data Creator
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

A. The requesting system is an application capable of making HTTP
   requests and able to process data encoded as XML metadata.

B. The request specifies

   1. The STOW-RS Service to store POST requests.

   2. Optionally, it may also specify Study Instance UID indicating all
      POST requests are for the indicated study.

   3. XML metadata, per DICOM encodings, and bulk data.

C. The response is a standard HTTP status line and an XML response
   message body. The meaning of the success, warning, or failure
   statuses are defined in .

.. _sect_HHH.4:

Uses For QIDO Services
----------------------

.. _sect_HHH.4.1:

General Requirements
~~~~~~~~~~~~~~~~~~~~

Imaging information is important in the context of EMR/EHR. But EMR/EHR
systems often do not support DICOM service classes. The EMR/EHR vendors
need access using web and web service technologies to satisfy their
users.

.. _sect_HHH.4.2:

Analysis of Use Cases
~~~~~~~~~~~~~~~~~~~~~

Examples of use cases / clinical scenarios, used as the basis for the
development of the QIDO-RS requirements, include:

a. Search from EMR

b. Populating FHIR resources

c. Worklist in Viewer

d. Study Import Duplication Check

e. Multiple System Query

f. Clinical Reconstruction

g. Mobile Device Access

.. _sect_HHH.4.2.1:

Search From EMR
^^^^^^^^^^^^^^^

A General Practitioner (GP) in a clinic would like to check for imaging
studies for the current patient. These studies are stored in a PACS,
Vendor Neutral Archive (VNA) or HIE that supports QIDO functionality.
The GP launches an Electronic Medical Record (EMR) application, and keys
in the patient demographics to search for the patient record within the
EMR. Once the record is open, the EMR, using QIDO, makes requests to the
back-end systems, supplying Patient ID (including issuer) and possibly
other parameters (date of birth, date range, modality, etc.). That
system returns the available studies along with meta-data for each study
that will help the GP select the study to open. The meta-data would
include, but is not limited to, Study Description, Study Date, Modality,
and Referring Physician.

.. _sect_HHH.4.2.2:

Populating FHIR Resources
^^^^^^^^^^^^^^^^^^^^^^^^^

HL7 has introduced FHIR (Fast Healthcare Interoperability Resources) as
a means of providing access to healthcare informatics information using
RESTful web services.

While FHIR will not replicate the information contained in a PACS or
other medical imaging storage system, it is desirable for FHIR to
present a view of the medical imaging studies available for a particular
patient along with the means of retrieving the imaging data using other
RESTful services.

.. _sect_HHH.4.2.3:

Worklist in Viewer
^^^^^^^^^^^^^^^^^^

A Radiologist, is reading studies in the office, using software that
maintains diagnostic orders for the facility. This system produces the
radiology worklist of studies to be read and provides meta-data about
each scheduled procedure, including the Study Instance UID. When the
next study is selected to be read on the worklist, the system, using the
Study Instance UID, makes a QIDO request to the local archive to
discover the instances and relevant study meta-data associated with the
procedure to display. Subsequent QIDO requests are made to the local
archive and to connected VNA archives to discover candidate relevant
prior studies for that patient.

For each candidate relevant prior, the full study metadata will be
retrieved using WADO-RS and processed to generate the list of relevant
priors.

.. _sect_HHH.4.2.4:

Multiple Systems Query
^^^^^^^^^^^^^^^^^^^^^^

A Radiologist is working in a satellite clinic, which has a system with
QIDO functionality and small image cache. The main hospital with which
the clinic is affiliated has a system with QIDO functionality and a
large historical image archive or VNA. The viewing software displays a
worklist of patients, and a study is selected for viewing. The viewer
checks for prior studies, by making QIDO requests to both the local
cache and remote archive using the Patient ID, Name and Date of Birth,
if available. If the Patient Identifier isn't available, other means
(such as by other demographics, or a Master Patient Index) could be
utilized. Any studies that meet relevant prior criteria can be
pre-fetched.

.. _sect_HHH.4.2.5:

Clinical Reconstruction
^^^^^^^^^^^^^^^^^^^^^^^

A Neurologist is preparing a surgical plan for a patient with a brain
tumor using three-dimensional reconstruction software, which takes CT
images and builds a 3D model of various structures. After supplying the
patient demographics (or Patient Identifier), the software requests a
list of appropriate studies for reconstruction (based on Study Date,
Body Region and Modality). Once the user has selected a study and
series, the software contacts the QIDO server again, requesting the SOP
Instance UIDs of all images of a certain thickness (specified in
specific DICOM tags) and frame of reference to be returned. The software
then uses this information to retrieve, using the WADO-RS service, the
appropriate DICOM objects needed to prepare the rendered volume for
display.

.. _sect_HHH.4.2.6:

Mobile Device Access
^^^^^^^^^^^^^^^^^^^^

A General Practitioner (GP) has left the medical ward for a few hours,
and is paged with a request to look at a patient X-Ray image in order to
grant a discharge. The GP carries a smart phone that has been pre-loaded
with credentials and secured. The device makes a QIDO request to the
server, to look for studies from the last hour that list the GP as the
Referring Physician. The GP is able to retrieve and view the matching
studies, and can make a determination whether to return to the ward for
further review or to sign the discharge order using the phone.

.. _sect_HHH.4.3:

Description of The Use Cases
~~~~~~~~~~~~~~~~~~~~~~~~~~~~

The use cases described above in terms of clinical scenarios correspond
to the following technical implementation scenarios. In each case the
use is distinguished by the capabilities of the requesting system:

a. Does it prefer XML or JSON results?

b. Does it need to perform searches at the Series and Instance level or
   can it process the full Study metadata?

c. What Attributes does it need to search against?

d. What Attributes does it need for each matching Study, Series or
   Composite Instance?

These questions can be applied to the use cases:

a. Search from EMR

   1. JSON or XML

   2. Study

   3. Study Instance UID, Patient ID

   4. Accession Number, Issuer of Accession Number, Study Description,
      Study Date, Modality, Number of Series, Number of Instances

b. Populating FHIR resources

   1. JSON or XML

   2. Study, Series and Instance

   3. Patient ID and Issuer of Patient ID

   4. All Attributes required by the FHIR Imaging Study Resource (see
      http://www.hl7.org/implement/standards/fhir/imagingstudy.htm)

c. Worklist in Viewer

   1. JSON or XML

   2. Study

   3. Study Instance UID, Patient ID, Issuer of Patient ID

   4. Series Instance UIDs, SOP Instance UIDs, patient demographics,
      Study Description, Study Date, Modality, Referring Physician

d. Study Import Duplication Check

   1. JSON or XML

   2. Study

   3. Study Instance UID, Series Instance UID, SOP Instance UID

   4. Study Instance UID

e. Multiple System Query

   1. JSON or XML

   2. Study

   3. Patient ID, Issuer of Patient ID, Patient Name, Patient Date of
      Birth

   4. Study Instance UID, Accession Number, Study Description, Study
      Date, Modalities in Study

f. Clinical Reconstruction

   1. JSON or XML

   2. Study, Series, Instance

   3. Study Instance UID, Series Instance UID

   4. SOP Instance UID, Image Instance Level Attributes

g. Mobile Device Access

   1. JSON

   2. Study, Series and Instance

   3. Patient ID, Issuer of Patient ID, Patient Name, Patient Date of
      Birth, Study Date, Referring Physician

   4. Instance Date/time, Modalities in Study

These then become the following technical use cases.

.. _sect_HHH.4.3.1:

XML Study Search Use Case
^^^^^^^^^^^^^^^^^^^^^^^^^

A. The requesting web-based application can make QIDO-RS requests, parse
   XML and then make WADO-RS requests

B. The request specifies:

   1. Multipart XML

   2. Search parameters, including:

      a. Patient ID

      b. Issuer of Patient ID

      c. Patient Name

      d. Study Description

      e. Study Date

      f. Modalities in Study

      g. Referring Physician

      h. etc.

C. The Response provides

   1. One XML NativeDicomModel element for each matching Study

   2. All requested DICOM Attributes for each matching Study

   3. WADO-RS Retrieve URL for each matching Study

D. The requesting system identifies the Studies of interest and uses
   WADO-RS to retrieve data

.. _sect_HHH.4.3.2:

XML Study, Series and Instance Search Use Case
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

A. The requesting system is a simple web-based application that can make
   QIDO-RS requests and parse XML and then make WADO URL requests

B. The request specifies:

   1. Multipart XML

   2. Search parameters, including:

      a. Patient ID

      b. Issuer of Patient ID

      c. Patient Name

      d. Patient Date of Birth

      e. Study Description

      f. Study Date

      g. Modalities in Study

      h. Referring Physician

C. The Response provides

   1. One XML NativeDicomModel element for each matching Study

   2. All requested DICOM Attributes for each matching Study

D. The requesting system identifies the Study of interest and uses
   Search For Series to identify a series of interest

E. [repeat B-D for Series, Instance]

F. The requesting system uses WADO URL to retrieve specific instances

.. _sect_HHH.4.3.3:

JSON Use Case
^^^^^^^^^^^^^

A. The requesting system is a mobile application that can make QIDO-RS
   requests, parse JSON and then make WADO URL requests.

B. The request specifies:

   1. JSON

   2. Search parameters, including:

      a. Patient ID

      b. Issuer of Patient ID

      c. Patient Name

      d. Patient Date of Birth

      e. Study Description

      f. Study Date

      g. Modalities in Study

      h. Referring Physician

C. The Response provides

   1. One DICOM JSON element containing all matching Studies

   2. All requested DICOM Attributes for each matching Study

D. The requesting system identifies the Study of interest and uses
   Search For Series to identify a series of interest

E. [repeat B-D for Series, Instance]

F. The requesting system uses WADO URL to retrieve specific instances

.. _sect_HHH.5:

Retired
-------

See PS3.17-2017b.

.. _sect_HHH.6:

Retired
-------

See PS3.17-2017b.

.. _sect_HHH.7:

Uses for Server Options Services
--------------------------------

Clients would like to be able to discover a list of devices that support
DICOM RESTful services and query a DICOM RESTful service to determine
which options are supported, such as:

-  Supported services and transactions

-  Supported Transfer Syntaxes and Media Types

-  Supported Accept header values

-  Supported query parameters

.. _sect_HHH.7.1:

WADL Example (XML)
~~~~~~~~~~~~~~~~~~

The following WADL XML example contains all the required elements for an
origin-server that supports WADO-RS, QIDO-RS and STOW-RS with all
required services and parameters.

::

   <application xsi:schemaLocation="http://wadl.dev.java.net/2009/02 wadl.xsd"
                xmlns:xsd="http://www.w3.org/2001/XMLSchema"
                xmlns="http://wadl.dev.java.net/2009/02">
    <resources base="http://medical.examplehospital.org/dicomweb">
     <resource path="studies">
      <method name="GET" id="SearchForStudies">
       <request>
        <param name="Accept" style="header"
               default="type=application/dicom+json">
         <option value="multipart/related; type=application/dicom+xml" />
         <option value="application/dicom+json" />
        </param>
        <param name="Cache-control" style="header">
         <option value="no-cache" />
        </param>
        <param name="limit" style="query" />
        <param name="offset" style="query" />
        <param name="StudyDate" style="query" />
        <param name="00080020" style="query" />
        <param name="StudyTime" style="query" />
        <param name="00080030" style="query" />
        <param name="AccessionNumber" style="query" />
        <param name="00080050" style="query" />
        <param name="ModalitiesInStudy" style="query" />
        <param name="00080061" style="query" />
        <param name="ReferringPhysicianName" style="query" />
        <param name="00080090" style="query" />
        <param name="PatientName" style="query" />
        <param name="00100010" style="query" />
        <param name="PatientID" style="query" />
        <param name="00100020" style="query" />
        <param name="StudyInstanceUID" style="query" repeating="true" />
        <param name="0020000D" style="query" repeating="true" />
        <param name="StudyID" style="query" />
        <param name="00200010" style="query" />
        <param name="includefield" style="query" repeating="true">
         <option value="all" />
        </param>
       </request>
       <response status="200">
        <param name="Warning" style="header"
               fixed="299 {SERVICE}: The fuzzymatching parameter is not supported.
               Only literal matching has been performed." />
        <representation mediaType="multipart/related; type=application/dicom+xml" />
        <representation mediaType="application/dicom+json" />
       </response>
       <response status="400 401 403 413 503" />
      </method>
      <method name="POST" id="StoreInstances">
       <request>
        <param name="Accept" style="header" default="application/dicom+xml">
         <option value="application/dicom+xml" />
        </param>
        <representation mediaType="multipart/related; type=application/dicom" />
        <representation mediaType="multipart/related; type=application/dicom;
                                             transfer-syntax=1.2.840.10008.1.2.1" />
        <representation mediaType="multipart/related; type=application/dicom+xml" />
       </request>
       <response status="202 409">
        <representation mediaType="application/dicom+xml" />
       </response>
       <response status="400 401 403 503" />
      </method>
      <resource path="{StudyInstanceUID}">
       <method name="GET" id="RetrieveStudy">
        <request>
         <param name="Accept" style="header"
                    default="multipart/related; type=application/dicom">
          <option value="multipart/related; type=application/dicom" />
          <option value="multipart/related; type=application/dicom;
                                             transfer-syntax=1.2.840.10008.1.2.1" />
          <option value="multipart/related; type=application/octet-stream" />
         </param>
        </request>
        <response status="200 206">
         <representation mediaType="multipart/related; type=application/dicom" />
         <representation mediaType="multipart/related; type=application/dicom;
                                             transfer-syntax=1.2.840.10008.1.2.1" />
         <representation mediaType="multipart/related; type=application/octet-stream" />
        </response>
        <response status="400 404 406 410 503"></response>
       </method>
       <method name="POST" id="StoreStudyInstances">
        <request>
         <param name="Accept" style="header" default="application/dicom+xml">
          <option value="application/dicom+xml" />
         </param>
         <representation mediaType="multipart/related; type=application/dicom" />
         <representation mediaType="multipart/related; type=application/dicom;
                                             transfer-syntax=1.2.840.10008.1.2.1" />
         <representation mediaType="multipart/related; type=application/dicom+xml" />
        </request>
        <response status="202 409">
         <representation mediaType="application/dicom+xml" />
        </response>
        <response status="400 401 403 503" />
       </method>
       <resource path="series">
        <method name="GET" id="SearchForStudySeries">
         <request>
          <param name="Accept" style="header"
                     default="type=application/dicom+json">
           <option value="multipart/related; type=application/dicom+xml" />
           <option value="application/dicom+json" />
          </param>
          <param name="Cache-control" style="header">
           <option value="no-cache" />
          </param>
          <param name="limit" style="query" />
          <param name="offset" style="query" />
          <param name="Modality" style="query" />
          <param name="00080060" style="query" />
          <param name="SeriesInstanceUID" style="query" repeating="true" />
          <param name="0020000E" style="query" repeating="true" />
          <param name="SeriesNumber" style="query" />
          <param name="00200011" style="query" />
          <param name="PerformedProcedureStepStartDate" style="query" />
          <param name="00400244" style="query" />
          <param name="PerformedProcedureStepStartTime" style="query" />
          <param name="00400245" style="query" />
          <param name="RequestAttributeSequence" style="query" />
          <param name="00400275" style="query" />
          <param name="RequestAttributeSequence.ScheduledProcedureStepID" style="query" />
          <param name="00400275.00400009" style="query" />
          <param name="RequestAttributeSequence.RequestedProcedureID" style="query" />
          <param name="00400275.00401001" style="query" />
          <param name="includefield" style="query" repeating="true">
           <option value="all" />
          </param>
         </request>
         <response status="200">
          <param name="Warning" style="header"
                 fixed="299 {SERVICE}: The fuzzymatching parameter is not supported.
                 Only literal matching has been performed." />
          <representation mediaType="multipart/related; type=application/dicom+xml" />
          <representation mediaType="application/dicom+json" />
         </response>
         <response status="400 401 403 413 503" />
        </method>
        <resource path="{SeriesInstanceUID}">
         <method name="GET" id="RetrieveSeries">
          <request>
           <param name="Accept" style="header"
                    default="multipart/related; type=application/dicom">
            <option value="multipart/related; type=application/dicom" />
            <option value="multipart/related; type=application/dicom;
                                             transfer-syntax=1.2.840.10008.1.2.1" />
            <option value="multipart/related; type=application/octet-stream" />
           </param>
          </request>
          <response status="200 206">
           <representation mediaType="multipart/related; type=application/dicom" />
           <representation mediaType="multipart/related; type=application/dicom;
                                             transfer-syntax=1.2.840.10008.1.2.1" />
           <representation mediaType="multipart/related; type=application/octet-stream" />
          </response>
          <response status="400 404 406 410 503"></response>
         </method>
         <resource path="instances">
          <method name="GET" id="SearchForStudySeriesInstances">
           <request>
            <param name="Accept" style="header"
                   default="type=application/dicom+json">
             <option value="multipart/related; type=application/dicom+xml" />
             <option value="application/dicom+json" />
            </param>
            <param name="Cache-control" style="header">
             <option value="no-cache" />
            </param>
            <param name="limit" style="query" />
            <param name="offset" style="query" />
            <param name="SOPClassUID" style="query" repeating="true" />
            <param name="00080016" style="query" repeating="true" />
            <param name="SOPInstanceUID" style="query" repeating="true" />
            <param name="00080018" style="query" repeating="true" />
            <param name="InstanceNumber" style="query" />
            <param name="00200013" style="query" />
            <param name="includefield" style="query" repeating="true">
             <option value="all" />
            </param>
           </request>
           <response status="200">
            <param name="Warning" style="header"
                   fixed="299 {SERVICE}: The fuzzymatching parameter is not supported.
                   Only literal matching has been performed." />
            <representation mediaType="multipart/related; type=application/dicom+xml" />
            <representation mediaType="application/dicom+json" />
           </response>
           <response status="400 401 403 413 503" />
          </method>
          <resource path="{SOPInstanceUID}">
           <method name="GET" id="RetrieveInstance">
            <request>
             <param name="Accept" style="header"
                    default="multipart/related; type=application/dicom">
              <option value="multipart/related; type=application/dicom" />
              <option value="multipart/related; type=application/dicom;
                                             transfer-syntax=1.2.840.10008.1.2.1" />
              <option value="multipart/related; type=application/octet-stream" />
             </param>
            </request>
            <response status="200 206">
             <representation mediaType="multipart/related; type=application/dicom" />
             <representation mediaType="multipart/related; type=application/dicom;
                                             transfer-syntax=1.2.840.10008.1.2.1" />
             <representation mediaType="multipart/related; type=application/octet-stream" />
            </response>
            <response status="400 404 406 410 503"></response>
           </method>
           <resource path="frames">
            <resource path="{framelist}">
             <method name="GET" id="RetrieveFrames">
              <request>
               <param name="Accept" style="header"
                      default="multipart/related; type=application/octet-stream">
                <option value="multipart/related; type=application/octet-stream" />
               </param>
              </request>
              <response status="200">
               <representation mediaType="multipart/related; type=application/octet-stream" />
              </response>
              <response status="400 404 406 410 503"></response>
             </method>
            </resource>
           </resource>
           <resource path="metadata">
            <method name="GET" id="RetrieveInstanceMetadata">
             <request>
              <param name="Accept" style="header"
                     default="type=application/dicom+json">
               <option value="multipart/related; type=application/dicom+xml" />
               <option value="application/dicom+json" />
              </param>
             </request>
             <response status="200">
              <representation mediaType=" multipart/related; type=application/dicom+xml" />
             </response>
             <response status="400 404 406 410 503"></response>
            </method>
           </resource>
          </resource>
         </resource>
         <resource path="metadata">
          <method name="GET" id="RetrieveSeriesMetadata">
           <request>
            <param name="Accept" style="header"
                     default="type=application/dicom+json">
             <option value="multipart/related; type=application/dicom+xml" />
             <option value="application/dicom+json" />
            </param>
           </request>
           <response status="200">
            <representation mediaType="multipart/related; type=application/dicom+xml" />
           </response>
           <response status="400 404 406 410 503"></response>
          </method>
         </resource>
        </resource>
       </resource>
       <resource path="instances">
        <method name="GET" id="SearchForStudyInstances">
         <request>
          <param name="Accept" style="header"
                     default="type=application/dicom+json">
           <option value="multipart/related; type=application/dicom+xml" />
           <option value="application/dicom+json" />
          </param>
          <param name="Cache-control" style="header">
           <option value="no-cache" />
          </param>
          <param name="limit" style="query" />
          <param name="offset" style="query" />
          <param name="SOPClassUID" style="query" />
          <param name="00080016" style="query" />
          <param name="SOPInstanceUID" style="query" repeating="true" />
          <param name="00080018" style="query" repeating="true" />
          <param name="Modality" style="query" />
          <param name="00080060" style="query" />
          <param name="SeriesInstanceUID" style="query" repeating="true" />
          <param name="0020000E" style="query" repeating="true" />
          <param name="SeriesNumber" style="query" />
          <param name="00200011" style="query" />
          <param name="InstanceNumber" style="query" />
          <param name="00200013" style="query" />
          <param name="PerformedProcedureStepStartDate" style="query" />
          <param name="00400244" style="query" />
          <param name="PerformedProcedureStepStartTime" style="query" />
          <param name="00400245" style="query" />
          <param name="RequestAttributeSequence" style="query" />
          <param name="00400275" style="query" />
          <param name="RequestAttributeSequence.ScheduledProcedureStepID" style="query" />
          <param name="00400275.00400009" style="query" />
          <param name="RequestAttributeSequence.RequestedProcedureID" style="query" />
          <param name="00400275.00401001" style="query" />
          <param name="includefield" style="query" repeating="true">
           <option value="all" />
          </param>
         </request>
         <response status="200">
          <param name="Warning" style="header"
                 fixed="299 {SERVICE}: The fuzzymatching parameter is not supported.
                 Only literal matching has been performed." />
          <representation mediaType="multipart/related; type=application/dicom+xml" />
          <representation mediaType="application/dicom+json" />
         </response>
         <response status="400 401 403 413 503" />
        </method>
       </resource>
       <resource path="metadata">
        <method name="GET" id="RetrieveStudyMetadata">
         <request>
          <param name="Accept" style="header"
                     default="type=application/dicom+json">
           <option value="multipart/related; type=application/dicom+xml" />
           <option value="application/dicom+json" />
          </param>
         </request>
         <response status="200">
          <representation mediaType="multipart/related; type=application/dicom+xml" />
         </response>
         <response status="400 404 406 410 503"></response>
        </method>
       </resource>
      </resource>
     </resource>
     <resource path="series">
      <method name="GET" id="SearchForSeries">
       <request>
        <param name="Accept" style="header"
                     default="type=application/dicom+json">
         <option value="multipart/related; type=application/dicom+xml" />
         <option value="application/dicom+json" />
        </param>
        <param name="Cache-control" style="header">
         <option value="no-cache" />
        </param>
        <param name="limit" style="query" />
        <param name="offset" style="query" />
        <param name="StudyDate" style="query" />
        <param name="00080020" style="query" />
        <param name="StudyTime" style="query" />
        <param name="00080030" style="query" />
        <param name="AccessionNumber" style="query" />
        <param name="00080050" style="query" />
        <param name="Modality" style="query" />
        <param name="00080060" style="query" />
        <param name="ModalitiesInStudy" style="query" />
        <param name="00080061" style="query" />
        <param name="ReferringPhysicianName" style="query" />
        <param name="00080090" style="query" />
        <param name="PatientName" style="query" />
        <param name="00100010" style="query" />
        <param name="PatientID" style="query" />
        <param name="00100020" style="query" />
        <param name="StudyInstanceUID" style="query" repeating="true" />
        <param name="0020000D" style="query" repeating="true" />
        <param name="SeriesInstanceUID" style="query" />
        <param name="0020000E" style="query" />
        <param name="StudyID" style="query" />
        <param name="00200010" style="query" />
        <param name="SeriesNumber" style="query" />
        <param name="00200011" style="query" />
        <param name="PerformedProcedureStepStartDate" style="query" />
        <param name="00400244" style="query" />
        <param name="PerformedProcedureStepStartTime" style="query" />
        <param name="00400245" style="query" />
        <param name="RequestAttributeSequence" style="query" />
        <param name="00400275" style="query" />
        <param name="RequestAttributeSequence.ScheduledProcedureStepID" style="query" />
        <param name="00400275.00400009" style="query" />
        <param name="RequestAttributeSequence.RequestedProcedureID" style="query" />
        <param name="00400275.00401001" style="query" />
        <param name="includefield" style="query" repeating="true">
         <option value="all" />
        </param>
       </request>
       <response status="200">
        <param name="Warning" style="header"
               fixed="299 {SERVICE}: The fuzzymatching parameter is not supported.
               Only literal matching has been performed." />
        <representation mediaType="multipart/related; type=application/dicom+xml" />
        <representation mediaType="application/dicom+json" />
       </response>
       <response status="400 401 403 413 503" />
      </method>
      <resource path="{SeriesInstanceUID}">
       <resource path="instances">
        <method name="GET" id="SearchForSeriesInstances">
         <request>
          <param name="Accept" style="header"
                     default="type=application/dicom+json">
           <option value="multipart/related; type=application/dicom+xml" />
           <option value="application/dicom+json" />
          </param>
          <param name="Cache-control" style="header">
           <option value="no-cache" />
          </param>
          <param name="limit" style="query" />
          <param name="offset" style="query" />
          <param name="SOPClassUID" style="query" repeating="true" />
          <param name="00080016" style="query" repeating="true" />
          <param name="SOPInstanceUID" style="query" repeating="true" />
          <param name="00080018" style="query" repeating="true" />
          <param name="InstanceNumber" style="query" />
          <param name="00200013" style="query" />
          <param name="includefield" style="query" repeating="true">
           <option value="all" />
          </param>
         </request>
         <response status="200">
          <param name="Warning" style="header"
                 fixed="299 {SERVICE}: The fuzzymatching parameter is not supported.
                 Only literal matching has been performed." />
          <representation mediaType="application/dicom+json" />
          <representation mediaType="multipart/related; type=application/dicom+xml" />
         </response>
         <response status="400 401 403 413 503" />
        </method>
       </resource>
      </resource>
     </resource>
     <resource path="instances">
      <method name="GET" id="SearchForInstances">
       <request>
        <param name="Accept" style="header"
                     application/dicom+json">
         <option value="multipart/related; type=application/dicom+xml" />
         <option value="application/dicom+json" />
        </param>
        <param name="Cache-control" style="header">
         <option value="no-cache" />
        </param>
        <param name="limit" style="query" />
        <param name="offset" style="query" />
        <param name="SOPClassUID" style="query" repeating="true" />
        <param name="00080016" style="query" repeating="true" />
        <param name="SOPInstanceUID" style="query" repeating="true" />
        <param name="00080018" style="query" repeating="true" />
        <param name="StudyDate" style="query" />
        <param name="00080020" style="query" />
        <param name="StudyTime" style="query" />
        <param name="00080030" style="query" />
        <param name="AccessionNumber" style="query" />
        <param name="00080050" style="query" />
        <param name="Modality" style="query" />
        <param name="00080060" style="query" />
        <param name="ModalitiesInStudy" style="query" />
        <param name="00080061" style="query" />
        <param name="ReferringPhysicianName" style="query" />
        <param name="00080090" style="query" />
        <param name="PatientName" style="query" />
        <param name="00100010" style="query" />
        <param name="PatientID" style="query" />
        <param name="00100020" style="query" />
        <param name="StudyInstanceUID" style="query" repeating="true" />
        <param name="0020000D" style="query" repeating="true" />
        <param name="SeriesInstanceUID" style="query" repeating="true" />
        <param name="0020000E" style="query" repeating="true" />
        <param name="SeriesNumber" style="query" />
        <param name="00200011" style="query" />
        <param name="InstanceNumber" style="query" />
        <param name="00200013" style="query" />
        <param name="PerformedProcedureStepStartDate" style="query" />
        <param name="00400244" style="query" />
        <param name="PerformedProcedureStepStartTime" style="query" />
        <param name="00400245" style="query" />
        <param name="RequestAttributeSequence" style="query" />
        <param name="00400275" style="query" />
        <param name="RequestAttributeSequence.ScheduledProcedureStepID" style="query" />
        <param name="00400275.00400009" style="query" />
        <param name="RequestAttributeSequence.RequestedProcedureID" style="query" />
        <param name="00400275.00401001" style="query" />
        <param name="includefield" style="query" repeating="true">
         <option value="all" />
        </param>
       </request>
       <response status="200">
        <param name="Warning" style="header"
               fixed="299 {SERVICE}: The fuzzymatching parameter is not supported.
               Only literal matching has been performed." />
        <representation mediaType="multipart/related; type=application/dicom+xml" />
        <representation mediaType="application/dicom+json" />
       </response>
       <response status="400 401 403 413 503" />
      </method>
     </resource>
     <resource path="{BulkDataURL}">
      <method name="GET" id="RetrieveBulkData">
       <request>
        <param name="Accept" style="header"
               default="multipart/related; type=application/octet-stream">
         <option value="multipart/related; type=application/octet-stream" />
        </param>
       </request>
       <response status="200">
        <representation mediaType="multipart/related; type=application/octet-stream" />
       </response>
       <response status="400 404 406 410 503"></response>
      </method>
     </resource>
    </resources>
   </application>

