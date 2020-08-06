.. _chapter_X:

Dictation-based Reporting With Image References (Informative)
=============================================================

This Annex describes a use of Key Object Selection (KO) and Grayscale
Softcopy Presentation State (GSPS) SOP Instances, in conjunction with a
typical dictation/transcription process for creating an imaging clinical
report. The result is a clinical report as a Basic Text Structured
Report (SR) SOP Instance that includes annotated image references (see
`Transcribed Diagnostic Imaging SR Instance Content <#sect_X.2>`__).
This report may also (or alternatively) be encoded as an HL7 Clinical
Document Architecture (CDA) document (see `Transcribed Diagnostic
Imaging CDA Instance Content <#sect_X.3>`__).

Similar but more complex processes that include, for instance, numeric
measurements and Enhanced or Comprehensive SR, are not addressed by this
Annex. This Annex also does not specifically address the special issues
associated with reporting across multiple studies (e.g., the "grouped
procedures" case).

.. _sect_X.1:

Basic Data Flows
----------------

.. _sect_X.1.1:

Dictation/transcription Reporting
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

During the softcopy reading of an imaging study, the physician dictates
the report, which is sent to a transcription service or is processed by
a voice recognition system. The transcribed dictation arrives at the
report management system (typically a RIS) by some mechanism not
specified here. The report management system enables the reporting
physician to correct, verify, and "sign" the transcribed report. See
`figure_title <#figure_X.1-1>`__. This data flow applies to reports
stored in a proprietary format, reports stored as DICOM Basic Text SR
SOP Instances, or reports stored as HL7 CDA instances.

The report management system has flexibility in encoding the report
title. For example, it could be any of the following:

-  the generic title "Diagnostic Imaging Report",

-  a report title associated with the department (e.g., "Radiology
   Report"),

-  a report title associated with the imaging modality or procedure
   (e.g., "Ultrasound Report"), or

-  a report title pre-coordinated with the modality and body part (e.g.,
   "CT Chest Report").

There are LOINC codes associated with each of these types of titles, if
a coded title is used on the report (see ).

The transcribed dictation may be either a single text stream, or a
series of text sections each with a title. Division of reports into a
limited number of canonically named sections may be done by the
transcriptionist, or automated division of typical free text reports may
be possible with voice recognition or a natural language processing
algorithm.

For an electronically stored report, the signing function may or may not
involve a cryptographic digital signature; any such cryptographic
signature is beyond the scope of this description.

.. _sect_X.1.2:

Reporting With Image References
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

To augment the basic dictation/transcription reporting use case, it is
desired to select significant images to be attached (by reference) to
the report. During the softcopy reading, the physician may select images
from those displayed on his workstation (e.g., by a point-and-click
function through the user interface). The selection of images is
conveyed to the image repository (PACS) through a DICOM Key Object
Selection (KO) document. When the report management system receives the
transcribed dictation, it queries the image repository for any KO
documents, and appends the image references from the KO to the
transcription. In this process step, the report management system does
not need to access the referenced images; it only needs to copy the
references into the draft report. The correction and signature function
potentially allows the physician to retrieve and view the referenced
images, correct and change text, and to delete individual image
references. See `figure_title <#figure_X.1-2>`__.

The transcribed dictation must have associated with it sufficient key
Attributes for the report management system to query for the appropriate
KO documents in the image repository (e.g., Study ID, or Accession
Number).

Each KO document in this process includes a specific title "For Report
Attachment", a single optional descriptive text field, plus a list of
image references using the SR Image Content Item format. The report
management system may need to retrieve all KO documents of the study to
find those with this title, since the image repository might not support
the object title as a query return key.

Multiple KO instances may be created for a study report, e.g., to
facilitate associating different descriptive text (included in the KO
document) with different images or image sets. All KOs with the title
"For Report Attachment" in the study are to be attached to the dictated
report by copying their content into the draft report (see `Transcribed
Diagnostic Imaging SR Instance Content <#sect_X.2>`__ and `Transcribed
Diagnostic Imaging CDA Instance Content <#sect_X.3>`__). (There may also
be KOs with other titles, such as "For Teaching", that are not to be
attached to the report.)

The nature of the image reference links will differ depending on the
format of the report. A DICOM SR format report will use DICOM native
references, and other formats may use a hyperlink to the referenced
images using the Web Access to DICOM Persistent Objects (WADO) service
(see ).

.. _sect_X.1.3:

Reporting With Annotated Images
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

The KO also allows the referencing of a Grayscale Softcopy Presentation
State (GSPS) instance for each selected image. A GSPS instance can be
created by the workstation for annotation ("electronic grease pencil")
of the selected image, as well as to set the window width/window level,
rotation/flip, and/or display area selection of the image attached to
the report. The created GSPS instances are transferred to the image
repository (PACS) and are referenced in the KO document.

As with image references, the report management system may include the
GSPS instance references in the report. When the report is subsequently
displayed, the reader may retrieve the referenced images together with
the referenced GSPS, so that the image is displayed with the annotations
and other GSPS display controls. See `figure_title <#figure_X.1-3>`__.

Note that the GSPS display controls can also be included in WADO
hyperlinks and invoked from non-DICOM display stations.

.. _sect_X.2:

Transcribed Diagnostic Imaging SR Instance Content
--------------------------------------------------

This section describes the use of transcribed dictation and Key Object
Selection (KO) instances to produce a DICOM Basic Text SR instance. A
specific SR Template, , is defined to support transcribed diagnostic
imaging reports created using this data flow.

.. _sect_X.2.1:

SR Header Content
~~~~~~~~~~~~~~~~~

The Attributes of the Patient and Study Modules will be identical to
those of the Study being reported. The following information is encoded
in the SR Document General Module:

-  Identity of the dictating physician (observer context) in the Author
   Sequence

-  Identity of the transcriptionist or transcribing device (voice
   recognition) in the Participant Sequence

-  Identity of the report signing physician in the Verifying Observer
   Sequence

-  Identity of the institution owning the report in the Custodial
   Organization Sequence

-  Linkages to the order and requested procedures in the Referenced
   Request Sequence

-  A list of all images in the study in the Current Requested Procedure
   Evidence Sequence (from MPPS SOP Instances of the Study, or from
   query of the image repository)

-  A list of all images not in the study, but also attached to the
   report as referenced significant images, in the Pertinent Other
   Evidence Sequence

.. _sect_X.2.2:

Transcribed Text Data Format
~~~~~~~~~~~~~~~~~~~~~~~~~~~~

The transcribed dictation is used to populate one or more section
containers in the content tree of the SR Instance. If the transcription
consists of a single undifferentiated text stream, it will typically be
encoded using a single CONTAINER content item with Concept Name
"Findings", and the text encoded as the value in a subsidiary TEXT
content item with Concept Name "Finding". When the transcription is
differentiated into multiple sections with captions, e.g., using the
concepts in , each section may be encoded in a separate CONTAINER, with
the concept from as the container Concept Name, and the corresponding
term from as the Concept Name for a subsidiary TEXT content item. See
`figure_title <#figure_X.2-1>`__.

.. _sect_X.2.3:

Image Reference Format
~~~~~~~~~~~~~~~~~~~~~~

The content items from each associated KO object will be included in the
SR in a separate CONTAINER with Concept Name (121180, DCM, "Key
Images"). The text item "Key Object Description" and all image reference
items shall be copied from the KO content tree to the corresponding SR
container. See `figure_title <#figure_X.2-2>`__.

The KO and SR IMAGE content item format allows the encoding of an icon
(image thumbnail) with the image reference, as well as a reference to a
GSPS instance controlling image presentation. Whether or not to include
icons or GSPS references is an implementation decision of the softcopy
review station that creates the KO; the IMAGE content item as a whole
may be simply copied by the report management system from the KO to the
Basic Text SR instance.

The intended process is that all KOs "For Report Attachment" are to be
automatically included in the draft report. Therefore, the correction
and signature function of the report management system should allow the
physician to delete image references that were included, perhaps
unintentionally, by the automatic process.

.. _sect_X.3:

Transcribed Diagnostic Imaging CDA Instance Content
---------------------------------------------------

This section describes the use of transcribed dictation and Key Object
Selection (KO) documents to produce an HL7 Clinical Document
Architecture (CDA) Release 2 document.

.. note::

   While this section describes encoding as CDA Release 2, notes are
   provided about encoding issues for CDA Release 1.

.. _sect_X.3.1:

CDA Header Content
~~~~~~~~~~~~~~~~~~

The header of the CDA instance includes:

-  Identity of the patient ("recordTarget" participation)

-  Identity of the requested procedure ("documentationOf" act
   relationship)

-  Identity of the dictating physician ("author" participation)

-  Identity of the transcriptionist ("dataEnterer" participation)

-  Identity of the report signing physician ("legalAuthenticator"
   participation)

-  Identity of the institution owning the report ("custodian"
   participation)

-  Identity of the request/order ("inFulfillmentOf" act relationship)

.. note::

   The markup components in CDA Release 1 use different names.

.. _sect_X.3.2:

Transcribed Text Content
~~~~~~~~~~~~~~~~~~~~~~~~

Each transcription section can be encoded in a Section in the CDA
document. The Section.Code and/or Section.Title can be derived from the
corresponding transcription section title, if any. Although the
transcription text can be encoded in the Section.Text without further
markup, it is recommended that it be enclosed in <paragraph> tags.

.. _sect_X.3.3:

Image References
~~~~~~~~~~~~~~~~

Images are referenced using hypertext links in the narrative text. These
links in CDA are not considered part of the attested content.

.. note::

   1. The primary use case for this Annex is the dictation/transcription
      reporting model. In the historical context of that model, the
      images (film sheets) are usually not considered part of the
      attested content of the report, although they are part of the
      complete exam record. I.e., the report is clinically complete
      without the images, and the referenced images are not formally
      part of the report. Therefore, this Annex discusses only the use
      of image references, not images embedded in the report.

   2. Being part of the attested content would require the images to be
      displayed every time the report is displayed - i.e., they are
      integral to understanding the report. If the images are attested,
      they must also be encapsulated with the CDA package. I.e., the CDA
      document itself is only one part of the interchanged package; the
      referenced images must also always be sent with the CDA document.
      If the images are for reference only and not attested, the Image
      Content Item may be transformed to a simple hypertext link; it is
      then the responsibility of CDA document receiver to follow or not
      follow the hyperlink. Moreover, as the industry moves toward
      ubiquitous network access to a distributed electronic healthcare
      record, there will be less need to prepackage the referenced
      images with the report.

In the current use case, there will be one or more KO instances with
image references. Each KO instance can be transformed to a Section in
the CDA document with a Section.Title "Key Images", and a Section.Code
of 121180 from the DICOM Controlled Terminology (see ). If the KO
includes a TEXT content item, it can be transformed to <paragraph> data
in that Section.Text of the CDA document. Each IMAGE content item can be
transformed to a link item using the <linkHtml> markup.

Within the <linkHtml> markup, the value of the href Attribute is the
DICOM object reference as a Web Access to Persistent DICOM Objects
(WADO) specified URI (see `table_title <#table_X.3-1>`__).

.. note::

   1. When a DICOM object reference is included in an HL7 CDA document,
      it is presumed the recipient would not be a DICOM application; it
      would have access only to general Internet network protocols (and
      not the DICOM upper layer protocol), and would not be configured
      with the means to display a native DICOM image. Therefore, the
      recommended encoding of a DICOM Object Reference in the CDA
      narrative block <linkHtml> uses WADO for access by the HTTP/HTTPS
      network protocol (see ), using one of the formats broadly
      supported in Web browsers (image/jpeg or video/mpeg) as the
      requested content type.

   2. In CDA Release 1, the markup tag for hyperlinks is <link_html>
      within the scope of a <link> tag.

.. table:: WADO Reference in an HL7 CDA <linkHtml>

   +----------------------------------+----------------------------------+
   | **WADO Component**               | **Source**                       |
   +==================================+==================================+
   | *<scheme>*:// *<authority>* /    | Configuration setting, used by   |
   | *<path>*                         | the conversion process,          |
   |                                  | identifying the WADO server      |
   +----------------------------------+----------------------------------+
   | ?requestType=WADO                | Fixed                            |
   +----------------------------------+----------------------------------+
   | &studyUID *=<uid>*               | Study Instance UID for           |
   |                                  | referenced image obtained from   |
   |                                  | the Current Requested Procedure  |
   |                                  | Evidence Sequence or the         |
   |                                  | Pertinent Other Evidence         |
   |                                  | Sequence in the KO Instance      |
   +----------------------------------+----------------------------------+
   | &seriesUID= *<uid>*              | Series Instance UID for          |
   |                                  | referenced image obtained from   |
   |                                  | the Current Requested Procedure  |
   |                                  | Evidence Sequence or the         |
   |                                  | Pertinent Other Evidence         |
   |                                  | Sequence in the KO Instance      |
   +----------------------------------+----------------------------------+
   | &objectUID= *<uid>*              | Referenced SOP Instance UID from |
   |                                  | IMAGE content item               |
   +----------------------------------+----------------------------------+
   | &frameNumber= *<list>*           | Referenced Frame Number from     |
   |                                  | IMAGE content item (if present)  |
   +----------------------------------+----------------------------------+
   | &presentationUID= *<uid>*        | Referenced SOP Instance UID from |
   |                                  | Referenced SOP Sequence within   |
   |                                  | IMAGE content item               |
   +----------------------------------+----------------------------------+
   | &presentationSeriesUID= *<uid>*  | Series Instance UID for          |
   |                                  | referenced presentation state    |
   |                                  | obtained from the Current        |
   |                                  | Requested Procedure Evidence     |
   |                                  | Sequence or the Pertinent Other  |
   |                                  | Evidence Sequence in the KO      |
   |                                  | Instance                         |
   +----------------------------------+----------------------------------+
   | &contentType=video/mpeg          | Present if Referenced SOP Class  |
   |                                  | UID from IMAGE content item is   |
   |                                  | for a Multi-frame Image IOD      |
   +----------------------------------+----------------------------------+

.. note::

   1. Literal strings are in normal typeface, while *<italic typeface
      within angle brackets>* indicates values to be copied from the
      identified source.

   2. The default contentType for single frame images is image/jpeg,
      which does not need to be specified as a WADO component. However,
      the default contentType for multiple frame images is
      application/dicom, which needs to be overridden with the specific
      request for video/mpeg.

   3. There is not yet a standard mechanism for minimizing the potential
      for staleness of the *<scheme>://<authority>/<path>component*.

.. _sect_X.3.4:

Icons
~~~~~

If the IMAGE content item includes an Icon Image Sequence, the report
creation process may embed the icon in the Section.Text narrative. The
Icon Image Sequence Pixel Data is converted into an image file, e.g., in
JPEG or GIF format, and base64 encoded. The file is encoded in an
ObservationMedia entry in the CDA instance, and a <renderMultimedia> tag
reference to the entry is encoded in the Section.Text adjacent to the
<linkHtml> of the image reference.

.. _sect_X.3.5:

Structured Entries
~~~~~~~~~~~~~~~~~~

The Current Requested Procedure Evidence Sequence (0040,A375) of the KO
instance lists all the SOP Instances referenced in the IMAGE content
items in their hierarchical Study/Series/Instance context. It is
recommended that this list be transcoded to CDA Entries in a Section
with Section.Title "DICOM Object Catalog" and a Section.Code of 121181
from the DICOM Controlled Terminology (see ).

.. note::

   1. Structured Entries are not defined in CDA Release 1.

   2. Since the image hypertext links in the Section narrative may refer
      to both an image and a softcopy presentation state, as well as
      possibly being constrained to specific frame numbers, in general
      there is not a simple mapping from the <linkHtml> to an entry.
      Therefore it is not expected that there would be ID reference
      links between the <linkHtml> and related entries.

The purpose of the Structured Entries is to allow DICOM-aware
applications to access the referenced images in their hierarchical
context.

The encoding of the DICOM Object References in CDA Entries is shown in
`figure_title <#figure_X.3-1>`__ and Tables X.3-2 through X.3-6. All of
the mandatory data elements for the Entries are available in the Current
Requested Procedure Evidence Sequence; optional elements (e.g., instance
DateTimes) may also be included if known by the encoding application.

.. note::

   The format of `figure_title <#figure_X.3-1>`__ follows the
   conventions of HL7 v3 Reference Information Model diagrams.

.. table:: DICOM Study Reference in an HL7 V3 Act (CDA Act Entry)

   +---------------+-----------+--------------+------------------------+
   | Attribute     | Data Type | Multiplicity | Value                  |
   +===============+===========+==============+========================+
   | classCode     | CS        | 1..1         | ACT                    |
   +---------------+-----------+--------------+------------------------+
   | moodCode      | CS        | 1..1         | EVN                    |
   +---------------+-----------+--------------+------------------------+
   | id            | II        | 1..1         | *<Study Instance UID   |
   |               |           |              | (0020,000D)* as root   |
   |               |           |              | property with no       |
   |               |           |              | extension property *>* |
   +---------------+-----------+--------------+------------------------+
   | code          | CD        | 1..1         | <113014 as code        |
   |               |           |              | property,              |
   |               |           |              |                        |
   |               |           |              | 1.2.840.10008.2.16.4   |
   |               |           |              | as codeSystem          |
   |               |           |              | property,              |
   |               |           |              |                        |
   |               |           |              | DCM as codeSystemName  |
   |               |           |              | property,              |
   |               |           |              |                        |
   |               |           |              | "DICOM Study" as       |
   |               |           |              | displayName property>  |
   +---------------+-----------+--------------+------------------------+
   | text          | ST        | 0..1         | *<Study Description    |
   |               |           |              | (0008,1030) >*         |
   +---------------+-----------+--------------+------------------------+
   | effectiveTime | TS        | 0..1         | < *Study Date          |
   |               |           |              | (0008,0020)* and       |
   |               |           |              | *Study Time            |
   |               |           |              | (0008,0030) >*         |
   +---------------+-----------+--------------+------------------------+

.. table:: DICOM Series Reference in an HL7 V3 Act (CDA Act Entry)

   +---------------+-----------+--------------+------------------------+
   | Attribute     | Data Type | Multiplicity | Value                  |
   +===============+===========+==============+========================+
   | classCode     | CS        | 1..1         | ACT                    |
   +---------------+-----------+--------------+------------------------+
   | moodCode      | CS        | 1..1         | EVN                    |
   +---------------+-----------+--------------+------------------------+
   | id            | II        | 1..1         | *<Series Instance UID  |
   |               |           |              | (0020,000E)* as root   |
   |               |           |              | property with no       |
   |               |           |              | extension property *>* |
   +---------------+-----------+--------------+------------------------+
   | code          | CD        | 0..1         | <113015 as code        |
   |               |           |              | property,              |
   |               |           |              |                        |
   |               |           |              | 1.2.840.10008.2.16.4   |
   |               |           |              | as codeSystem          |
   |               |           |              | property,              |
   |               |           |              |                        |
   |               |           |              | DCM as codeSystemName  |
   |               |           |              | property,              |
   |               |           |              |                        |
   |               |           |              | "DICOM Series" as      |
   |               |           |              | displayName property,  |
   |               |           |              |                        |
   |               |           |              | *Modality* as          |
   |               |           |              | qualifier property     |
   |               |           |              | (see text and          |
   |               |           |              | `table_ti              |
   |               |           |              | tle <#table_X.3-4>`__) |
   |               |           |              | >                      |
   +---------------+-----------+--------------+------------------------+
   | text          | ST        | 0..1         | < *Series Description  |
   |               |           |              | (0008,103E)* >         |
   +---------------+-----------+--------------+------------------------+
   | effectiveTime | TS        | 0..1         | < *Series Date         |
   |               |           |              | (0008,0021)* and       |
   |               |           |              | *Series Time           |
   |               |           |              | (0008,0031) >*         |
   +---------------+-----------+--------------+------------------------+

The code for the Act representing a Series uses a qualifier property to
indicate the modality. The qualifier property is a list of coded
name/value pairs. For this use, only a single list entry is used, as
described in `table_title <#table_X.3-4>`__.

.. table:: Modality Qualifier for The Series Act.Code

   +----------+-----------+---------------------------------------------+
   | Property | Data Type | Value                                       |
   +==========+===========+=============================================+
   | name     | CV        | <121139 as code property,                   |
   |          |           |                                             |
   |          |           | 1.2.840.10008.2.16.4 as codeSystem          |
   |          |           | property,                                   |
   |          |           |                                             |
   |          |           | DCM as codeSystemName property,             |
   |          |           |                                             |
   |          |           | "Modality" as displayName property>         |
   +----------+-----------+---------------------------------------------+
   | value    | CD        | < *Modality (0008,0060)* as code property,  |
   |          |           |                                             |
   |          |           | 1.2.840.10008.2.16.4 as codeSystem          |
   |          |           | property,                                   |
   |          |           |                                             |
   |          |           | DCM as codeSystemName property,             |
   |          |           |                                             |
   |          |           | *Modality code meaning (from )* as          |
   |          |           | displayName property>                       |
   +----------+-----------+---------------------------------------------+

.. table:: DICOM Composite Object Reference in an HL7 V3 Act (CDA
Observation Entry)

   +---------------+-----------+--------------+------------------------+
   | Attribute     | Data Type | Multiplicity | Value                  |
   +===============+===========+==============+========================+
   | classCode     | CS        | 1..1         | DGIMG                  |
   +---------------+-----------+--------------+------------------------+
   | moodCode      | CS        | 1..1         | EVN                    |
   +---------------+-----------+--------------+------------------------+
   | id            | II        | 1..1         | < *SOP Instance UID    |
   |               |           |              | (0008,0018)* as root   |
   |               |           |              | property with no       |
   |               |           |              | extension property>    |
   +---------------+-----------+--------------+------------------------+
   | code          | CD        | 1..1         | < *SOP Class UID       |
   |               |           |              | (0008,0016)* as code   |
   |               |           |              | property,              |
   |               |           |              |                        |
   |               |           |              | 1.2.840.10008.2.6.1 as |
   |               |           |              | codeSystem property,   |
   |               |           |              |                        |
   |               |           |              | DCMUID as              |
   |               |           |              | codeSystemName         |
   |               |           |              | property,              |
   |               |           |              |                        |
   |               |           |              | *SOP Class UID Name    |
   |               |           |              | (from )* as            |
   |               |           |              | displayName property>  |
   +---------------+-----------+--------------+------------------------+
   | text          | ED        | 0..1         | <application/DICOM as  |
   |               |           |              | mediaType property,    |
   |               |           |              |                        |
   |               |           |              | *WADO reference* (see  |
   |               |           |              | `table_ti              |
   |               |           |              | tle <#table_X.3-6>`__) |
   |               |           |              | as reference property> |
   +---------------+-----------+--------------+------------------------+
   | effectiveTime | TS        | 0..1         | < *Content Date        |
   |               |           |              | (0008,0023)* and       |
   |               |           |              | *Content Time          |
   |               |           |              | (0008,0033) >*         |
   +---------------+-----------+--------------+------------------------+

.. note::

   1. The DGIMG class is used to reference all DICOM Composite
      Instances, not just diagnostic images.

   2. The Observation.Text reference property may alternatively use a
      DICOM protocol based URI, rather than WADO, should such a URI be
      defined.

.. table:: WADO Reference in an HL7 DGIMG Observation.Text

   +----------------------------------+----------------------------------+
   | **WADO Component**               | **Source**                       |
   +==================================+==================================+
   | *<scheme>*:// *<authority>* /    | Configuration setting, used by   |
   | *<path>*                         | the conversion process,          |
   |                                  | identifying the WADO server      |
   +----------------------------------+----------------------------------+
   | ?requestType=WADO                | Fixed                            |
   +----------------------------------+----------------------------------+
   | &studyUID *=<uid>*               | Study Instance UID for           |
   |                                  | referenced instance              |
   +----------------------------------+----------------------------------+
   | &seriesUID= *<uid>*              | Series Instance UID for          |
   |                                  | referenced instance              |
   +----------------------------------+----------------------------------+
   | &objectUID= *<uid>*              | SOP Instance UID for referenced  |
   |                                  | instance                         |
   +----------------------------------+----------------------------------+
   | &contentType=application/DICOM   | Fixed                            |
   +----------------------------------+----------------------------------+

.. _sect_X.4.3:

Using The WADO Reference For DICOM Network Protocol Retrievals
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

An application that receives a CDA with image references, and is capable
of using the full services of DICOM upper layer protocol directly, can
use the WADO parameters in either the linkHtml or in the DGIMG
Observation.Text to retrieve the object using the DICOM network
services. Such an application would need to be pre-configured with the
hostname/IP address, TCP port, and AE Title of the DICOM object server
(C-MOVE or C-GET SCP); this network address is not part of the WADO
string. (Note that pre-configuration of this network address is typical
for DICOM applications, and is facilitated by the LDAP-based DICOM
Application Configuration Management Profile; see .)

The application would open a Query/Retrieve Service Association with the
configured server, and send a C-MOVE or C-GET command using the study,
series, and object instance UIDs identified in the WADO query
parameters. Such an application might also reasonably query the server
for related objects, such as Grayscale Softcopy Presentation State.

.. note::

   When using the C-GET service, the retrieving application needs to
   specify and negotiate the SOP Class of the retrieved objects when it
   opens the Association. This information is not available in the
   linkHtml WADO reference; however, it is available in the DGIMG
   Observation.Code. It may also be obtained from the configured server
   using a C-FIND query on a prior Association.

.. _sect_X.4:

Simultaneous SR and CDA Instance Creation
-----------------------------------------

The report may be created as both an SR instance and a CDA instance. In
this case, the two instances are equivalent, and can cross-reference
each other.

.. _sect_X.4.1:

Equivalence
~~~~~~~~~~~

The CDA Document shall contain clinical content equivalent to the SR
Document.

.. note::

   The HL7 CDA standard specifically addresses transformation of
   documents from a non-CDA format. The requirement in the CDA
   specification is: "A proper transformation must ensure that the human
   readable clinical content of the report is not impacted."

There is no requirement that the transform or transcoding between DICOM
SR and HL7 CDA be reversible. In particular, some Attributes of the
DICOM Patient, Study, and Series IEs have no corresponding standard
encoding in the HL7 CDA Header, and vice versa. Such data elements, if
transcoded, may need to be encoded in "local markup" (in HL7 CDA) or
private data elements (in DICOM SR) in an implementation-dependent
manner; and some such data elements may not be transcoded at all. It is
a responsibility of the transforming application to ensure clinical
equivalence.

Many Attributes of the SR Document General Module can be transcoded to
CDA Header participations or related acts.

.. _sect_X.4.2:

Document Cross-reference
~~~~~~~~~~~~~~~~~~~~~~~~

Due to the inherent differences between DICOM SR and HL7 CDA, a
transcoded document will have a different UID than the source document.
However, the SR Document may reference the CDA Document as equivalent
using the Equivalent CDA Document Sequence (0040,A090) Attribute, and
the CDA Document may reference the SR Document with a relatedDocument
act relationship.

Since the ParentDocument target of the relatedDocument relationship is
constrained to be a simple DOCCLIN act, it is recommended that the
reference to the DICOM SR be encoded per `table_title <#table_X.3-4>`__,
without explicit identification of the Study and Series Instance UIDs,
and with classCode DOCCLIN (rather than DGIMG).

.. note::

   1. The Study and Series Instance UIDs would be encoded in the WADO
      reference in the Act.Text ED data type.

   2. CDA Release 1 does not provide a standard for the relatedDocument
      relationship to another document.

