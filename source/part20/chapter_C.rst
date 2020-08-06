.. _chapter_C:

SR to CDA Imaging Report Transformation Guide
=============================================

Constrained DICOM SR documents based on Imaging Report templates can be
mapped to HL7 CDA Release 2 Imaging Reports based on Template
1.2.840.10008.9.1, as specified in `Imaging Report <#sect_7.1>`__. The
SR report templates to which this transformation applies include:

-  

-  

-  

SR instances based on other templates may also be able to be mapped
using the transformations in this Annex.

SR documents can be thought of as consisting of a document header and a
document body, corresponding to a CDA document header and body. The
header includes the modules related to the Patient, Study, Series, and
Equipment Information Entities, plus the SR Document General Module, as
specified in . The SR Document Content Module contains the content tree
(structured content) of the document body. Note, however, that DICOM SR
considers the root content item, including the coded report title, and
some context-setting content items as part of the document body content
tree, but these constitute part of the CDA header. See
`figure_title <#figure_C-1>`__.

.. _sect_C.1:

Constraints
-----------

This Annex defines the transformation of an Enhanced SR SOP Instance to
a CDA instance. The following constraints apply to such SOP Instances:

-  Observation Context: The mapping does not support changing the
   observation context for the report as a whole from its default
   context, as specified in the Patient, Study, and Document Information
   Entities (see )

   .. note::

      , and specify inclusion of as Mandatory, but has no content if all
      aspects of context are inherited, as under this constraint.

-  Subject Context: The mapping does not support the subject of any of
   the report sections to be a specimen ), a device (), or a non-human
   subject. Only a fetus subject context is supported for a Findings
   section.

-  Procedure Context: The mapping allows identification of a different
   procedure than the procedure identified in the SR Study IE only as
   context for a Prior Procedure Descriptions section.

-  De-identified Documents: There is no CDA implementation guidance from
   HL7 for de-identified documents, other than general rules for using
   the MSK null flavor (see `Null Flavor <#sect_5.3.2>`__). There is no
   CDA capability equivalent to the Encrypted Attributes Sequence (see )
   for carrying encrypted re-identification data.

-  Patient Study Module: Medical or clinical characteristics of the
   patient specified in the Patient Study Module are not mapped (see )

-  Clinical Trials: Template 1.2.840.10008.9.1 does not define
   attributes for clinical trials equivalent to those of the Patient,
   Study, and Series IEs (Clinical Trial Subject Module, Clinical Trial
   Study Module, Clinical Trial Series Module).

-  Spatial Coordinates: The mapping does not support SCOORD
   observations. As CDA documents are principally for human reading,
   detailed ROI data is presumed to reside in the DICOM SOP Instances of
   the study, or in images ready for rendering with a Presentation
   State, not in the CDA report. Template 1.2.840.10008.9.1 does not
   support the CDA Region of Interest Overlay entry class (see
   `regionOfInterest <#sect_9.1.2.4>`__).

.. _sect_C.2:

Conventions
-----------

Literal values to be encoded in CDA elements are represented in the
mapping tables in normal font, as a string, or as a coded value triplet:

-  "NI"

-  (codeValue, codingScheme, codeMeaning)

Conventions for mapping from DICOM attributes in the transformed SR are
described in `Value Specification <#sect_5.2.8>`__.

Data mapped from an SR Content Item is identified by the Concept Name of
the Content Item, represented in the mapping tables as a triplet in
italic font:

-  *(codeValue, codingScheme, codeMeaning)*

Data mapped from a specific Attribute in an SR Content Item uses the
triplet to identify the Content Item, with the > character and the
specific attribute name and tag:

-  *(codeValue, codingScheme, codeMeaning) > Attribute Name (gggg,eeee)*

Additional notes are within square brackets:

-  [Note]

Mandatory CDA elements for which there is no corresponding source data
in the SR SOP Instance may be coded with a nullFlavor attribute (see
`Null Flavor <#sect_5.3.2>`__).

.. _sect_C.3:

Header Transformation
---------------------

For transformation of the SR content into the CDA header, the target
elements of the CDA instance are listed in
`table_title <#table_C.3-1>`__ by their Business Names, together with
the recommended source in an SR instance. This allows the transforming
application to "pull" the relevant information from the SR to populate
the CDA header.

.. table:: CDA Header content from SR

   +----------------------------------+----------------------------------+
   | CDA Business Name                | DICOM SR                         |
   +==================================+==================================+
   | ImagingReport: DocType           | *Concept Name Code Sequence      |
   |                                  | (0040,A043)* [of the root        |
   |                                  | content item]                    |
   +----------------------------------+----------------------------------+
   | ImagingReport: ContentTemplate   |                                  |
   +----------------------------------+----------------------------------+
   | ImagingReport: DocumentID        |                                  |
   +----------------------------------+----------------------------------+
   | ImagingReport: Title             | *(121050, DCM, "Equivalent       |
   |                                  | Meaning of Concept Name") >      |
   |                                  | Concept Code Sequence            |
   |                                  | (0040,A168) > Code Meaning       |
   |                                  | (0008,0104)* if present;         |
   |                                  | otherwise *Concept Name Code     |
   |                                  | Sequence (0040,A043) > Code      |
   |                                  | Meaning (0008,0104)* [of the     |
   |                                  | root content item].              |
   +----------------------------------+----------------------------------+
   | ImagingReport: CreationTime      | *Content Date (0008,0023) +      |
   |                                  | Content Time (0008,0033) +       |
   |                                  | Timezone Offset From UTC         |
   |                                  | (0008,0201)*                     |
   +----------------------------------+----------------------------------+
   | ImagingReport: Confidentiality   |                                  |
   +----------------------------------+----------------------------------+
   | ImagingReport: LanguageCode      | *(121049, DCM, "Language of      |
   |                                  | Content Item and Descendants")*  |
   +----------------------------------+----------------------------------+
   | ImagingReport: SetId             |                                  |
   +----------------------------------+----------------------------------+
   | ImagingReport: VersionNumber     |                                  |
   +----------------------------------+----------------------------------+
   | ImagingReport: Patient:ID        | *Patient ID (0010,0020)*         |
   +----------------------------------+----------------------------------+
   | ImagingReport: Patient:IDIssuer  | *Issuer of Patient ID Qualifiers |
   |                                  | Sequence (0010,0024) > Universal |
   |                                  | Entity ID (0040,0032)*           |
   +----------------------------------+----------------------------------+
   | ImagingReport: Patient:Addr      | *Patient's Address (0010,1040)*  |
   +----------------------------------+----------------------------------+
   | ImagingReport: Patient:Tele      | *Patient's Telephone Numbers     |
   |                                  | (0010,2154)*                     |
   +----------------------------------+----------------------------------+
   | ImagingReport: Patient:Name      | *Patient's Name (0010,0010)*     |
   +----------------------------------+----------------------------------+
   | ImagingReport: Patient:Gender    | *Patient's Sex (0010,0040)*      |
   |                                  |                                  |
   |                                  | [Map value "O" to nullFlavor     |
   |                                  | UNK]                             |
   +----------------------------------+----------------------------------+
   | ImagingReport: Patient:BirthTime | *Patient's Birth Date            |
   |                                  | (0010,0030) + Patient's Birth    |
   |                                  | Time (0010,0032)*                |
   +----------------------------------+----------------------------------+
   | ImagingReport:                   | *Issuer of Patient ID            |
   | Patient:ProviderOrgName          | (0010,0021)*                     |
   +----------------------------------+----------------------------------+
   | ImagingReport:                   |                                  |
   | Patient:ProviderOrgTel           |                                  |
   +----------------------------------+----------------------------------+
   | ImagingReport:                   |                                  |
   | Patient:ProviderOrgAddr          |                                  |
   +----------------------------------+----------------------------------+
   | ImagingReport: SigningTime       | *Verifying Observer Sequence     |
   |                                  | (0040,A073) > Verification       |
   |                                  | DateTime (0040,A030)*.           |
   +----------------------------------+----------------------------------+
   | ImagingReport: SignerID          | *Verifying Observer Sequence     |
   |                                  | (0040,A073) > Verifying Observer |
   |                                  | Identification Code Sequence     |
   |                                  | (0040,A088)* [code value as      |
   |                                  | identifier]                      |
   +----------------------------------+----------------------------------+
   | ImagingReport: SignerAddr        |                                  |
   +----------------------------------+----------------------------------+
   | ImagingReport: SignerTel         |                                  |
   +----------------------------------+----------------------------------+
   | ImagingReport: SignerName        | *Verifying Observer Sequence     |
   |                                  | (0040,A073) > Verifying Observer |
   |                                  | Name (0040,A075)*                |
   +----------------------------------+----------------------------------+
   | ImagingReport: SignatureBlock    |                                  |
   +----------------------------------+----------------------------------+
   | ImagingReport:                   | *Content Date (0008,0023) +      |
   | Author:AuthoringTime             | Content Time (0008,0033) +       |
   |                                  | Timezone Offset From UTC         |
   |                                  | (0008,0201)*                     |
   +----------------------------------+----------------------------------+
   | ImagingReport: Author:ID         | *Author Observer Sequence        |
   |                                  | (0040,A078) > Person             |
   |                                  | Identification Code Sequence     |
   |                                  | (0040,1101)* [code value as      |
   |                                  | identifier]                      |
   +----------------------------------+----------------------------------+
   | ImagingReport: Author:Addr       |                                  |
   +----------------------------------+----------------------------------+
   | ImagingReport: Author:Tel        |                                  |
   +----------------------------------+----------------------------------+
   | ImagingReport: Author:Name       | *Author Observer Sequence        |
   |                                  | (0040,A078) > Person Name        |
   |                                  | (0040,A123)*                     |
   +----------------------------------+----------------------------------+
   | ImagingReport: Recipient:Addr    |                                  |
   +----------------------------------+----------------------------------+
   | ImagingReport: Recipient:Tel     |                                  |
   +----------------------------------+----------------------------------+
   | ImagingReport: Recipient:Name    |                                  |
   +----------------------------------+----------------------------------+
   | ImagingReport: Recipient:Org     |                                  |
   +----------------------------------+----------------------------------+
   | ImagingReport: CustodianOrgID    | *Custodial Organization Sequence |
   |                                  | (0040,A07C) > Institution Code   |
   |                                  | Sequence (0008,0082)* [code      |
   |                                  | value as identifier]             |
   +----------------------------------+----------------------------------+
   | ImagingReport: CustodianOrgName  | *Custodial Organization Sequence |
   |                                  | (0040,A07C) > Institution Name   |
   |                                  | (0008,0080)*                     |
   +----------------------------------+----------------------------------+
   | ImagingReport: CustodianOrgAddr  |                                  |
   +----------------------------------+----------------------------------+
   | ImagingReport: CustodianOrgTel   |                                  |
   +----------------------------------+----------------------------------+
   | ImagingReport: EncounterID       | *Admission Id (0038,0010)*       |
   +----------------------------------+----------------------------------+
   | ImagingReport: EncounterIDIssuer | *Issuer of Admission ID Sequence |
   |                                  | (0038;0014) > Universal Entity   |
   |                                  | ID (0040,0032)*                  |
   +----------------------------------+----------------------------------+
   | ImagingReport: EncounterTime     |                                  |
   +----------------------------------+----------------------------------+
   | ImagingReport:                   |                                  |
   | HealthcareFacilityName           |                                  |
   +----------------------------------+----------------------------------+
   | ImagingReport:                   | *Institution Address             |
   | HealthcareFacilityAddress        | (0008,0081)*                     |
   +----------------------------------+----------------------------------+
   | ImagingReport:He                 | *Institution Name (0008,0080)*   |
   | althcareProviderOrganizationName |                                  |
   +----------------------------------+----------------------------------+
   | Imag                             | *Physician(s) of Record          |
   | ingReport:AttendingPhysicianName | (0008,1048)*                     |
   +----------------------------------+----------------------------------+
   | ImagingReport:OrderPlacerNumber  | *Referenced Request Sequence     |
   |                                  | (0040,A370) > Placer Order       |
   |                                  | Number/Imaging Service Request   |
   |                                  | (0040,2016)*                     |
   +----------------------------------+----------------------------------+
   | Imagi                            | *Referenced Request Sequence     |
   | ngReport:OrderAssigningAuthority | (0040,A370) > Order Placer       |
   |                                  | Identifier Sequence (0040,0026)  |
   |                                  | > Universal Entity ID            |
   |                                  | (0040,0032)*                     |
   +----------------------------------+----------------------------------+
   | ImagingReport:AccessionNumber    | *Accession Number (0008,0050)*   |
   +----------------------------------+----------------------------------+
   | ImagingRe                        | *Issuer of Accession Number      |
   | port:AccessionAssigningAuthority | Sequence (0008,0051) > Universal |
   |                                  | Entity ID (0040,0032)*           |
   +----------------------------------+----------------------------------+
   | Im                               | *Referenced Request Sequence     |
   | agingReport:OrderedProcedureCode | (0040,A370) > Requested          |
   |                                  | Procedure Code Sequence          |
   |                                  | (0032,1064)*                     |
   +----------------------------------+----------------------------------+
   | ImagingReport: OrderPriority     |                                  |
   +----------------------------------+----------------------------------+
   | ImagingReport:Study:StudyUID     | *Study Instance UID (0020,000D)* |
   +----------------------------------+----------------------------------+
   | I                                | *Procedure Code Sequence         |
   | magingReport:Study:ProcedureCode | (0008,1032)*                     |
   +----------------------------------+----------------------------------+
   | ImagingReport:Study:Modality     | *(122142, DCM, "Acquisition      |
   |                                  | Device Type")* or `(55111-9, LN, |
   |                                  | "Current Procedure               |
   |                                  | Descriptions") <h                |
   |                                  | ttp://loinc.org/55111-9/>`__\ *> |
   |                                  | (122142, DCM, "Acquisition       |
   |                                  | Device Type")*                   |
   +----------------------------------+----------------------------------+
   | Imagin                           | *(123014, DCM, "Target Region")* |
   | gReport:Study:AnatomicRegionCode | or `(55111-9, LN, "Current       |
   |                                  | Procedure                        |
   |                                  | Descriptions") <h                |
   |                                  | ttp://loinc.org/55111-9/>`__\ *> |
   |                                  | (123014, DCM, "Target Region")*  |
   +----------------------------------+----------------------------------+
   | ImagingReport:Study:StudyTime    | *Study Date (0008,0020) + Study  |
   |                                  | Time (0008,0030) + Timezone      |
   |                                  | Offset From UTC (0008,0201)*     |
   +----------------------------------+----------------------------------+
   | ImagingReport: Performer:Type    |                                  |
   +----------------------------------+----------------------------------+
   | ImagingReport: Performer:ID      |                                  |
   +----------------------------------+----------------------------------+
   | ImagingReport: Performer:Name    |                                  |
   +----------------------------------+----------------------------------+
   | ImagingReport: ReferrerAddr      | *Referring Physician             |
   |                                  | Identification Sequence          |
   |                                  | (0008,0096) > Person's Address   |
   |                                  | (0040,1102)*                     |
   +----------------------------------+----------------------------------+
   | ImagingReport: ReferrerTel       | *Referring Physician             |
   |                                  | Identification Sequence          |
   |                                  | (0008,0096) > Person's Telephone |
   |                                  | Numbers (0040,1103)*             |
   +----------------------------------+----------------------------------+
   | ImagingReport: ReferrerName      | *Referring Physician's Name      |
   |                                  | (0008,0090)*                     |
   +----------------------------------+----------------------------------+
   | ImagingReport:                   | *Participant Sequence            |
   | TranscriptionistID               | (0040,A07A) > Person             |
   |                                  | Identification Code Sequence     |
   |                                  | (0040,1101)* , [where            |
   |                                  | Participation Type (0040,A080)   |
   |                                  | equals "ENT" (Data Enterer);     |
   |                                  | code value as identifier]        |
   +----------------------------------+----------------------------------+
   | ImagingReport:                   | *Participant Sequence            |
   | TranscriptionistName             | (0040,A07A) Person Name          |
   |                                  | (0040,A123)* [where              |
   |                                  | Participation Type (0040,A080)   |
   |                                  | equals "ENT" (Data Enterer) ]    |
   +----------------------------------+----------------------------------+
   | ImagingReport:                   | *SOP Instance UID (0008,0018)*   |
   | TransformedDocumentID            |                                  |
   +----------------------------------+----------------------------------+

ImagingReport:Study:Modality and ImagingReport:Study:AnatomicRegionCode
may be mapped from attributes in the root CONTAINER, if present there as
in , or in the Current Procedure Descriptions section CONTAINER, if
present there as in .

.. _sect_C.4:

Body Transformation
-------------------

For transformation of the body, this Section maps the SR content items
to their target CDA elements. This allows the transforming application
to traverse the SR content tree and construct equivalent CDA content.

.. _sect_C.4.1:

Section Mapping
~~~~~~~~~~~~~~~

SR , and specify that imaging report elements are contained in sections,
represented as CONTAINERs with concept name codes from .

Each CONTAINER immediately subsidiary to the root CONTAINER shall be
mapped to the section or subsection as specified in
`table_title <#table_C.4-1>`__. Note that some SR document sections are
mapped to subsections under CDA Template 1.2.840.10008.9.1.

.. table:: SR Section mapping to CDA

   +-----------------+------------+-----------------+-----------------+
   | Coding Scheme   | Code Value | Code Meaning    | Map to Template |
   | Designator      |            |                 | Sec             |
   |                 |            |                 | tion/Subsection |
   +=================+============+=================+=================+
   | LN              | 11329-0    | History         | `Clinical       |
   |                 |            |                 | Information     |
   |                 |            |                 |  <#sect_9.2>`__ |
   |                 |            |                 | / `Medical      |
   |                 |            |                 | (General)       |
   |                 |            |                 | History <       |
   |                 |            |                 | #sect_9.8.3>`__ |
   +-----------------+------------+-----------------+-----------------+
   | LN              | 55115-0    | Request         | `Clinical       |
   |                 |            |                 | Information     |
   |                 |            |                 |  <#sect_9.2>`__ |
   |                 |            |                 | /               |
   |                 |            |                 | `Request <      |
   |                 |            |                 | #sect_9.8.1>`__ |
   +-----------------+------------+-----------------+-----------------+
   | LN              | 55111-9    | Current         | `Imaging        |
   |                 |            | Procedure       | Procedure       |
   |                 |            | Descriptions    | Description     |
   |                 |            |                 |  <#sect_9.3>`__ |
   +-----------------+------------+-----------------+-----------------+
   | LN              | 55114-3    | Prior Procedure | `Comparison     |
   |                 |            | Descriptions    | Study           |
   |                 |            |                 |  <#sect_9.4>`__ |
   +-----------------+------------+-----------------+-----------------+
   | LN              | 18834-2    | Previous        | `Comparison     |
   |                 |            | Findings        | Study           |
   |                 |            |                 |  <#sect_9.4>`__ |
   +-----------------+------------+-----------------+-----------------+
   | LN              | 18782-3    | Findings (Study | `Findings       |
   |                 |            | Observation)    |  <#sect_9.5>`__ |
   |                 |            |                 | or              |
   |                 |            |                 | `Findings       |
   |                 |            |                 |  <#sect_9.5>`__ |
   |                 |            |                 | / `Fetus        |
   |                 |            |                 | Findings <      |
   |                 |            |                 | #sect_9.8.8>`__ |
   |                 |            |                 | (see `Fetus     |
   |                 |            |                 | Subject         |
   |                 |            |                 | Context <#se    |
   |                 |            |                 | ct_C.4.1.3>`__) |
   +-----------------+------------+-----------------+-----------------+
   | LN              | 59776-5    | Findings        | `Findings       |
   |                 |            |                 |  <#sect_9.5>`__ |
   |                 |            |                 | or              |
   |                 |            |                 | `Findings       |
   |                 |            |                 |  <#sect_9.5>`__ |
   |                 |            |                 | / `Fetus        |
   |                 |            |                 | Findings <      |
   |                 |            |                 | #sect_9.8.8>`__ |
   |                 |            |                 | (see `Fetus     |
   |                 |            |                 | Subject         |
   |                 |            |                 | Context <#se    |
   |                 |            |                 | ct_C.4.1.3>`__) |
   +-----------------+------------+-----------------+-----------------+
   | LN              | 19005-8    | Impressions     | `Impression     |
   |                 |            |                 |  <#sect_9.6>`__ |
   +-----------------+------------+-----------------+-----------------+
   | LN              | 18783-1    | Recommendations | `Impression     |
   |                 |            |                 |  <#sect_9.6>`__ |
   |                 |            |                 | /               |
   |                 |            |                 | `Re             |
   |                 |            |                 | commendation <# |
   |                 |            |                 | sect_9.8.11>`__ |
   +-----------------+------------+-----------------+-----------------+
   | LN              | 55110-1    | Conclusions     | `Impression     |
   |                 |            |                 |  <#sect_9.6>`__ |
   +-----------------+------------+-----------------+-----------------+
   | LN              | 55107-7    | Addendum        | `Addendum       |
   |                 |            |                 |  <#sect_9.7>`__ |
   +-----------------+------------+-----------------+-----------------+
   | LN              | 18785-6    | Indications for | `Clinical       |
   |                 |            | Procedure       | Information     |
   |                 |            |                 |  <#sect_9.2>`__ |
   |                 |            |                 | / `Procedure    |
   |                 |            |                 | Indications <   |
   |                 |            |                 | #sect_9.8.2>`__ |
   +-----------------+------------+-----------------+-----------------+
   | LN              | 55108-5    | Patient         | `Clinical       |
   |                 |            | Presentation    | Information     |
   |                 |            |                 |  <#sect_9.2>`__ |
   +-----------------+------------+-----------------+-----------------+
   | LN              | 55109-3    | Complications   | `Imaging        |
   |                 |            |                 | Procedure       |
   |                 |            |                 | Description     |
   |                 |            |                 |  <#sect_9.3>`__ |
   |                 |            |                 | /               |
   |                 |            |                 | `               |
   |                 |            |                 | Complications < |
   |                 |            |                 | #sect_9.8.4>`__ |
   +-----------------+------------+-----------------+-----------------+
   | LN              | 55112-7    | Summary         | `Impression     |
   |                 |            |                 |  <#sect_9.6>`__ |
   +-----------------+------------+-----------------+-----------------+
   | LN              | 55113-5    | Key Images      | `Impression     |
   |                 |            |                 |  <#sect_9.6>`__ |
   |                 |            |                 | / `Key          |
   |                 |            |                 | Images <        |
   |                 |            |                 | #sect_9.8.6>`__ |
   +-----------------+------------+-----------------+-----------------+
   | LN              | 73569-6    | Radiation       | `Imaging        |
   |                 |            | Exposure and    | Procedure       |
   |                 |            | Protection      | Description     |
   |                 |            | Information     |  <#sect_9.3>`__ |
   |                 |            |                 | / `Radiation    |
   |                 |            |                 | Exposure and    |
   |                 |            |                 | Protection      |
   |                 |            |                 | Information <   |
   |                 |            |                 | #sect_9.8.5>`__ |
   +-----------------+------------+-----------------+-----------------+
   | LN              | 55752-0    | Clinical        | `Clinical       |
   |                 |            | Information     | Information     |
   |                 |            |                 |  <#sect_9.2>`__ |
   +-----------------+------------+-----------------+-----------------+
   | LN              | 29549-3    | Medications     | `Imaging        |
   |                 |            | Administered    | Procedure       |
   |                 |            |                 | Description     |
   |                 |            |                 |  <#sect_9.3>`__ |
   |                 |            |                 | / `Procedural   |
   |                 |            |                 | Medication      |
   |                 |            |                 | <#sect_10.2>`__ |
   +-----------------+------------+-----------------+-----------------+
   | LN              | 73568-8    | Communication   | `Impression     |
   |                 |            | of Critical     |  <#sect_9.6>`__ |
   |                 |            | Results         | /               |
   |                 |            |                 | `Communication  |
   |                 |            |                 | of Actionable   |
   |                 |            |                 | Findings <#     |
   |                 |            |                 | sect_9.8.10>`__ |
   +-----------------+------------+-----------------+-----------------+

CDA Template 1.2.840.10008.9.1 requires a minimum of an Imaging
Procedure Description section and an Impression section.

The section/code element shall be populated in accordance with the
relevant CDA template; note that the code might not be the same as the
Concept Name code of the SR section CONTAINER. The title element of each
CDA section shall be populated as shown in
`table_title <#table_C.4-2>`__.

.. table:: CDA Section mapping from SR

   +----------------------------------+----------------------------------+
   | CDA Business Name                | DICOM SR                         |
   +==================================+==================================+
   | <section>: Title                 | *Concept Name Code Sequence      |
   |                                  | (0040,A043) > Code Meaning       |
   |                                  | (0008,0104)* [of the section     |
   |                                  | CONTAINER content item]          |
   +----------------------------------+----------------------------------+
   | <section>: Text                  | [See                             |
   |                                  | `Section/text <#sect_C.4.2>`__]  |
   +----------------------------------+----------------------------------+
   | <section>: CodedObservation[*]   | [See `Coded                      |
   |                                  | Observations <#sect_C.4.3.1>`__  |
   |                                  | and `Text                        |
   |                                  | Observations <#sect_C.4.3.2>`__] |
   +----------------------------------+----------------------------------+
   | <section>:                       | [See `Numeric                    |
   | QuantityMeasurement[*]           | Observations <#sect_C.4.3.4>`__] |
   +----------------------------------+----------------------------------+
   | <section>: SOPInstance[*]        | [See `Image                      |
   |                                  | Observations <#sect_C.4.3.3>`__] |
   +----------------------------------+----------------------------------+

SR allows sections to be qualified by observation context, using and its
subsidiary templates. This capability is constrained in this mapping.

.. _sect_C.4.1.1:

Section Observer Context
^^^^^^^^^^^^^^^^^^^^^^^^

allows identification of a human or device author.

.. table:: CDA Section author mapping from SR

   +-------------------------------+-------------------------------------+
   | CDA Business Name             | DICOM SR                            |
   +===============================+=====================================+
   | <section>: AuthorID           | If *(121005, DCM, "Observer Type")* |
   |                               | = (121007, DCM, "Device"), then     |
   |                               | *(121012, DCM, "Device Observer     |
   |                               | UID")*                              |
   |                               |                                     |
   |                               | ID for human observer not           |
   |                               | represented in SR; use              |
   |                               | nullFlavor="UNK"                    |
   +-------------------------------+-------------------------------------+
   | <section>: AuthorName         | *(121008, DCM, "Person Observer     |
   |                               | Name")*                             |
   +-------------------------------+-------------------------------------+
   | <section>: AuthorOrganization | *(121009, DCM, "Person Observer's   |
   |                               | Organization Name")*                |
   +-------------------------------+-------------------------------------+
   | <section>: AuthorDeviceModel  | *(121015, DCM, "Device Observer     |
   |                               | Model Name")*                       |
   +-------------------------------+-------------------------------------+
   | <section>: AuthorSoftware     | *(121013, DCM, "Device Observer     |
   |                               | Name")*                             |
   +-------------------------------+-------------------------------------+

.. _sect_C.4.1.2:

Comparison Study Procedure Context
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

allows identification of a different procedure than the procedure
identified in the SR Study IE as the context for the section
observations. In the transformations of this Annex, only an identified
comparison procedure is supported as Procedure Context, the SR section
being transformed must be either Prior Procedure Descriptions or
Previous Findings, and the CDA section shall be in accordance with the
Comparison Study section Template 1.2.840.10008.9.4.

SR Instances using have additional attributes of a comparison procedure
specified using , which is used in the Prior Procedure Descriptions
section. The attributes of both and are source data in the
`table_title <#table_C.4-4>`__ mapping.

.. table:: Comparison Study mapping from SR

   +----------------------------------+----------------------------------+
   | CDA Business Name                | DICOM SR                         |
   +==================================+==================================+
   | ComparisonStudy:                 | *(121023, DCM, "Procedure        |
   | ProcedureTechnique:              | Code")*                          |
   | ProcedureCode                    |                                  |
   +----------------------------------+----------------------------------+
   | ComparisonStudy:                 | *(111060, DCM, "Study Date") +   |
   | ProcedureTechnique:              | (111061, DCM, "Study Time")*     |
   | EffectiveTime                    |                                  |
   +----------------------------------+----------------------------------+
   | ComparisonStudy:                 | *(122142, DCM, "Acquisition      |
   | ProcedureTechnique: Modality     | Device Type")*                   |
   +----------------------------------+----------------------------------+
   | ComparisonStudy:                 |                                  |
   | ProcedureTechnique: MethodCode   |                                  |
   +----------------------------------+----------------------------------+
   | ComparisonStudy:                 | *(123014, DCM, "Target Region")* |
   | ProcedureTechnique: TargetSite   |                                  |
   +----------------------------------+----------------------------------+
   | ComparisonStudy:                 |                                  |
   | ProcedureTechnique: Laterality:  |                                  |
   +----------------------------------+----------------------------------+
   | ComparisonStudy:                 |                                  |
   | ProcedureTechnique: Ref:         |                                  |
   +----------------------------------+----------------------------------+
   | ComparisonStudy:                 |                                  |
   | ProcedureTechnique:              |                                  |
   | ProviderOrganization             |                                  |
   +----------------------------------+----------------------------------+
   | ComparisonStudy: Study[*]:       | *(121018, DCM, "Procedure Study  |
   | StudyUID                         | Instance UID")*                  |
   +----------------------------------+----------------------------------+
   | ComparisonStudy: Study[*]:       | *(121065, DCM, "Procedure        |
   | Description                      | Description")* , if present, or  |
   |                                  | *(121023, DCM, "Procedure Code") |
   |                                  | > Code Meaning (0008,0104)*      |
   +----------------------------------+----------------------------------+
   | ComparisonStudy: Study[*]: Time  | *(111060, DCM, "Study Date") +   |
   |                                  | (111061, DCM, "Study Time")*     |
   +----------------------------------+----------------------------------+

.. _sect_C.4.1.3:

Fetus Subject Context
^^^^^^^^^^^^^^^^^^^^^

allows identification of a different subject than the patient identified
in the SR Patient IE. In the transformations of this Annex, only an
identified fetus subject is supported as Subject Context for a Findings
section. An SR section with a fetus subject context shall be mapped to a
CDA section shall be in accordance with the Fetus Findings subsection
Template 1.2.840.10008.9.9. This section is subsidiary to the top level
Findings section; multiple SR fetus findings sections may be mapped to
separate CDA Fetus Findings subsections.

.. table:: CDA Fetus subject mapping from SR

   +----------------------------------+----------------------------------+
   | CDA Business Name                | DICOM SR                         |
   +==================================+==================================+
   | Findings: FetusFindings[*]:      | *(121030, DCM, "Subject ID")* or |
   | FetusID                          | `(11951-1, LN, "Fetus            |
   |                                  | ID"                              |
   |                                  | ) <http://loinc.org/11951-1/>`__ |
   +----------------------------------+----------------------------------+

.. _sect_C.4.2:

Section/text
~~~~~~~~~~~~

DICOM specifies that sections contain imaging report elements of type
CODE, TEXT, IMAGE, or NUM.

Section/text in the CDA document contains the narrative text (attested
content) of the document. Section/text shall be generated from all the
Content Items subsidiary to a section CONTAINER of the SR document, such
that the full meaning is be conveyed in an unambiguous manner in the
narrative block.

The narrative rendered from each Content Item shall be encapsulated in a
<content> element of the narrative block, allowing the associated entry
to reference it.

.. _sect_C.4.3:

Content Item Mapping
~~~~~~~~~~~~~~~~~~~~

Each Content Item immediately subsidiary to a section CONTAINER shall be
mapped to the corresponding entry level template, and shall be included
subsidiary to the associated CDA section or subsection. This is in
addition to its rendering in the section/text narrative block.

Coded concepts that are encoded in the SR using with the Coding Scheme
Designator "SRT" shall be mapped to the equivalent SNOMED CT code.
Mappings for value sets invoked in both SR and CDA are provided in .

.. _sect_C.4.3.1:

Coded Observations
^^^^^^^^^^^^^^^^^^

SR CODE Content Items shall be mapped to Coded Observation entries.

.. table:: CDA Coded Observation mapping from SR CODE

   +----------------------------------+----------------------------------+
   | CDA Business Name                | DICOM SR                         |
   +==================================+==================================+
   | CodedObservation[*]: ObsName     | *Concept Name Code Sequence      |
   |                                  | (0040,A043)*                     |
   +----------------------------------+----------------------------------+
   | CodedObservation[*]: ObsValue    | *Concept Code Sequence           |
   |                                  | (0040,A168)*                     |
   +----------------------------------+----------------------------------+
   | CodedObservation[*]: Time        | *Observation DateTime            |
   |                                  | (0040,A032)*                     |
   +----------------------------------+----------------------------------+
   | CodedObservation[*]:             |                                  |
   | InterpretationCode               |                                  |
   +----------------------------------+----------------------------------+
   | CodedObservation[*]:             |                                  |
   | ActionableFindingCode            |                                  |
   +----------------------------------+----------------------------------+
   | CodedObservation[*]: TargetSite  | `(363698007, SCT, "Finding       |
   |                                  | Site") <htt                      |
   |                                  | p://snomed.info/id/363698007>`__ |
   +----------------------------------+----------------------------------+
   | CodedObservation[*]:Laterality   | `(363698007, SCT, "Finding       |
   |                                  | Site") <http://snomed.info/id/   |
   |                                  | 363698007>`__\ *>*\ `(272741003, |
   |                                  | SCT,                             |
   |                                  | "Laterality") <htt               |
   |                                  | p://snomed.info/id/272741003>`__ |
   +----------------------------------+----------------------------------+
   | CodedObservation[*]:TopoModifier |                                  |
   +----------------------------------+----------------------------------+
   | CodedObservation[*]:Method       |                                  |
   +----------------------------------+----------------------------------+
   | CodedObservation[*]: SOPInstance | [See `Image                      |
   |                                  | Observations <#sect_C.4.3.3>`__] |
   +----------------------------------+----------------------------------+
   | CodedObservation[*]:             | [See `Numeric                    |
   | QuantityMeasurement              | Observations <#sect_C.4.3.4>`__] |
   +----------------------------------+----------------------------------+
   | CodedObservation[*]:             |                                  |
   | CodedObservation                 |                                  |
   +----------------------------------+----------------------------------+

The CODE observations in do not specifically include finding site,
laterality, and topographical modifiers, but these modifiers are not
forbidden in the template, and may be present in a SR SOP Instance being
transformed to CDA.

.. _sect_C.4.3.2:

Text Observations
^^^^^^^^^^^^^^^^^

SR TEXT Content Items are mapped to Coded Observation entries, but the
code is a nullFlavor with the text content in originalText.

.. table:: CDA Coded Observation mapping from SR TEXT

   +----------------------------------+----------------------------------+
   | CDA Business Name or XPath       | DICOM SR                         |
   +==================================+==================================+
   | CodedObservation[*]: ObsName     | *Concept Name Code Sequence      |
   |                                  | (0040,A043)*                     |
   +----------------------------------+----------------------------------+
   | observation/value/@nullFlavor    | "NI"                             |
   +----------------------------------+----------------------------------+
   | observation/value/originalText   | *Text Value (0040,A160)*         |
   +----------------------------------+----------------------------------+
   | CodedObservation[*]: Time        | *Observation DateTime            |
   |                                  | (0040,A032)*                     |
   +----------------------------------+----------------------------------+
   | CodedObservation[*]:             |                                  |
   | InterpretationCode               |                                  |
   +----------------------------------+----------------------------------+
   | CodedObservation[*]:             |                                  |
   | ActionableFindingCode            |                                  |
   +----------------------------------+----------------------------------+
   | CodedObservation[*]: TargetSite  |                                  |
   +----------------------------------+----------------------------------+
   | CodedObservation[*]:Laterality   |                                  |
   +----------------------------------+----------------------------------+
   | CodedObservation[*]:TopoModifier |                                  |
   +----------------------------------+----------------------------------+
   | CodedObservation[*]:Method       |                                  |
   +----------------------------------+----------------------------------+
   | CodedObservation[*]: SOPInstance | [See `Image                      |
   |                                  | Observations <#sect_C.4.3.3>`__] |
   +----------------------------------+----------------------------------+
   | CodedObservation[*]:             | [See `Numeric                    |
   | QuantityMeasurement              | Observations <#sect_C.4.3.4>`__] |
   +----------------------------------+----------------------------------+
   | CodedObservation[*]:             |                                  |
   | CodedObservation                 |                                  |
   +----------------------------------+----------------------------------+

.. _sect_C.4.3.3:

Image Observations
^^^^^^^^^^^^^^^^^^

SR IMAGE Content Items shall be mapped to SOP Instance Observation
entries.

.. table:: CDA SOP Instance Observation mapping from SR IMAGE

   +----------------------------------+----------------------------------+
   | CDA Business Name                | DICOM SR                         |
   +==================================+==================================+
   | SOPInstance[*]:SOPInstanceUID    | *Referenced SOP Sequence         |
   |                                  | (0008,1199) > Referenced SOP     |
   |                                  | Instance UID (0008,1155)*        |
   +----------------------------------+----------------------------------+
   | SOPInstance[*]:SOPClassUID       | *Referenced SOP Sequence         |
   |                                  | (0008,1199) > Referenced SOP     |
   |                                  | Class UID (0008,1150)*           |
   +----------------------------------+----------------------------------+
   | SOPInstance[*]:WADOReference     | [WADO link constructed from      |
   |                                  | image reference; also used in    |
   |                                  | linkHtml in narrative block]     |
   +----------------------------------+----------------------------------+
   | S                                | *Concept Name Code Sequence      |
   | OPInstance[*]:PurposeOfReference | (0040,A043)*                     |
   +----------------------------------+----------------------------------+
   | SOPInstance[*]:ReferencedFrames  | *Referenced SOP Sequence         |
   |                                  | (0008,1199) > Referenced Frame   |
   |                                  | Number (0008,1160)*              |
   +----------------------------------+----------------------------------+

.. _sect_C.4.3.4:

Numeric Observations
^^^^^^^^^^^^^^^^^^^^

SR NUM Content Items shall be mapped to Quantity Measurement entries.

.. table:: CDA Quantity Measurement mapping from SR NUM

   +----------------------------------+----------------------------------+
   | CDA Business Name                | DICOM SR                         |
   +==================================+==================================+
   | QuantityMeasurement[*]:          | *Concept Name Code Sequence      |
   | MeasurementName                  | (0040,A043)*                     |
   +----------------------------------+----------------------------------+
   | QuantityMeasurement[*]:          | *Measured Value Sequence         |
   | MeasurementValue                 | (0040,A300) > Numeric Value      |
   |                                  | (0040,A30A)*                     |
   +----------------------------------+----------------------------------+
   | QuantityMeasurement[*]:          | *Measured Value Sequence         |
   | MeasurementUnits                 | (0040,A300) > Measurement Units  |
   |                                  | Code Sequence (0040,08EA) > Code |
   |                                  | Value (0008,0100)*               |
   +----------------------------------+----------------------------------+
   | QuantityMeasurement[*]: Time     | *Observation DateTime            |
   |                                  | (0040,A032)*                     |
   +----------------------------------+----------------------------------+
   | QuantityMeasurement[*]:          |                                  |
   | InterpretationCode               |                                  |
   +----------------------------------+----------------------------------+
   | QuantityMeasurement[*]:          |                                  |
   | ActionableFindingCode            |                                  |
   +----------------------------------+----------------------------------+
   | QuantityMeasurement[*]:          | `(363698007, SCT, "Finding       |
   | TargetSite                       | Site") <htt                      |
   |                                  | p://snomed.info/id/363698007>`__ |
   +----------------------------------+----------------------------------+
   | Q                                | `(363698007, SCT, "Finding       |
   | uantityMeasurement[*]:Laterality | Site") <http://snomed.info/id/   |
   |                                  | 363698007>`__\ *>*\ `(272741003, |
   |                                  | SCT,                             |
   |                                  | "Laterality") <htt               |
   |                                  | p://snomed.info/id/272741003>`__ |
   +----------------------------------+----------------------------------+
   | QuantityMeasurement[*]:Method    | `(370129005, SCT, "Measurement   |
   |                                  | Method") <htt                    |
   |                                  | p://snomed.info/id/370129005>`__ |
   +----------------------------------+----------------------------------+
   | Qua                              | `(106233006, SCT, "Topographical |
   | ntityMeasurement[*]:TopoModifier | modifier") <htt                  |
   |                                  | p://snomed.info/id/106233006>`__ |
   +----------------------------------+----------------------------------+
   | QuantityMeasurement[*]:          | [See `Image                      |
   | SOPInstance                      | Observations <#sect_C.4.3.3>`__] |
   +----------------------------------+----------------------------------+
   | QuantityMeasurement[*]:          | [See `Numeric                    |
   | QuantityMeasurement              | Observations <#sect_C.4.3.4>`__] |
   +----------------------------------+----------------------------------+

The SR templates invoked for NUM measurements from do not specifically
include finding site, laterality, and topographical modifiers, but these
modifiers are not forbidden in the template, they are used in many other
NUM value templates (e.g., ), and may be present in a SR SOP Instance
being transformed to CDA.

.. _sect_C.4.3.5:

Inferred From Image Observations
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

SR and allow Content Items to be INFERRED FROM IMAGE observations. The
INFERRED FROM relationship is mapped to the entryRelationship with
typeCode=SPRT, and the IMAGE observation is mapped to a CDA SOP Instance
Observation entry subsidiary to its parent CDA Coded Observation or
Quantity Measurement entry. This entryRelationship is shown in the Coded
Observation and Quantity Measurement CDA Templates.

.. _sect_C.4.3.6:

Inferred From Numeric Observations
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

SR and allow Content Items to be INFERRED FROM NUM observations. The
INFERRED FROM relationship is mapped to the entryRelationship with
typeCode=SPRT, and the NUM observation is mapped to CDA Quantity
Measurement entry subsidiary to its parent CDA Coded Observation or
Quantity Measurement entry. This entryRelationship is shown in the Coded
Observation and Quantity Measurement CDA Templates.

.. _sect_C.4.3.7:

Inferred From Spatial Coordinates Observations
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

SR , , , and allow NUM Content Items to be INFERRED FROM SCOORD
observations, which are SELECTED FROM IMAGE observations. This Annex
does not specify the transformation for SCOORD observations; these would
use the CDA Region Of Interest entry, which PS3.20 forbids (see
`regionOfInterest <#sect_9.1.2.4>`__).

.. _sect_C.4.4:

Specific Section Content Mapping
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

Certain sections in a CDA Imaging Report have specific mappings from the
DICOM SR header, or from specialized templates with content for
particular uses.

.. _sect_C.4.4.1:

Procedure Indications
^^^^^^^^^^^^^^^^^^^^^

The DICOM SR Document General Module may specify the Reason for the
Requested Procedure as either free text in attribute (0040,1002), and/or
as multiple coded values in attribute (0040,100A). These are mapped to
the Procedure Indications subsection of the Clinical Information section
of the CDA Imaging Report.

.. note::

   Procedure indications may also be specified as SR content items in
   the `(18785-6, LN, "Indications for
   Procedure") <http://loinc.org/18785-6/>`__ CONTAINER, which may be
   mapped to the CDA instance in accordance with `Content Item
   Mapping <#sect_C.4.3>`__. It is an implementation decision how to
   handle multiple representations of indications in the SR document.

.. table:: Clinical Information Procedure Indications mapping from SR

   +----------------------------------+----------------------------------+
   | CDA Business Name                | DICOM SR                         |
   +==================================+==================================+
   | ClinicalInformation:             | *Referenced Request Sequence     |
   | ProcedureIndications: Text       | (0040,A370) > Reason for the     |
   |                                  | Requested Procedure (0040,1002)* |
   +----------------------------------+----------------------------------+
   | ClinicalInformation:             | (432678004, SNOMED, "Indication  |
   | ProcedureIndications:            | for procedure")                  |
   | CodedObservation[*]: ObsName     |                                  |
   +----------------------------------+----------------------------------+
   | ClinicalInformation:             | *Referenced Request Sequence     |
   | ProcedureIndications:            | (0040,A370) > Reason for the     |
   | CodedObservation[*]: ObsValue    | Requested Procedure Code         |
   |                                  | Sequence (0040,100A)*            |
   +----------------------------------+----------------------------------+

.. _sect_C.4.4.2:

Current Procedure Descriptions
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

SR Instances using have a Current Procedure Descriptions section
specified using . Source data in that template and from the General
Study Module is mapped into the CDA Procedure Description section.

.. table:: Current Procedure Description mapping from SR

   +----------------------------------+----------------------------------+
   | CDA Business Name                | DICOM SR                         |
   +==================================+==================================+
   | ProcedureDescription:            | *Procedure Code Sequence         |
   | ProcedureTechnique:              | (0008,1032)*                     |
   | ProcedureCode                    |                                  |
   +----------------------------------+----------------------------------+
   | ProcedureDescription:            | *(111060, DCM, "Study Date") +   |
   | ProcedureTechnique:              | (111061, DCM, "Study Time")*     |
   | EffectiveTime                    |                                  |
   +----------------------------------+----------------------------------+
   | ProcedureDescription:            | *(122142, DCM, "Acquisition      |
   | ProcedureTechnique: Modality     | Device Type")*                   |
   +----------------------------------+----------------------------------+
   | ProcedureDescription:            |                                  |
   | ProcedureTechnique: MethodCode   |                                  |
   +----------------------------------+----------------------------------+
   | ProcedureDescription:            | *(123014, DCM, "Target Region")* |
   | ProcedureTechnique: TargetSite   |                                  |
   +----------------------------------+----------------------------------+
   | ProcedureDescription:            |                                  |
   | ProcedureTechnique: Laterality   |                                  |
   +----------------------------------+----------------------------------+
   | ProcedureDescription:            |                                  |
   | ProcedureTechnique: Ref          |                                  |
   +----------------------------------+----------------------------------+

.. _sect_C.4.4.3:

Radiation Exposure and Protection Information
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

The Radiation Exposure and Protection Information section defined in SR
is specified using , which provides additional source data for mapping
into the equivalent CDA subsection of the Imaging Procedure Description
section.

.. table:: CDA Radiation Exposure and Protection Information mapping
from SR

   +----------------------------------+----------------------------------+
   | CDA Business Name                | DICOM SR                         |
   +==================================+==================================+
   | RadiationExposure:               |                                  |
   | IrradiationAuthorizingID         |                                  |
   +----------------------------------+----------------------------------+
   | RadiationExposure:               | *(113850, DCM, "Irradiation      |
   | IrradiationAuthorizingName       | Authorizing ")*                  |
   +----------------------------------+----------------------------------+
   | Radiation                        | *(113701, DCM, "X-Ray Radiation  |
   | Exposure:SOPInstance[doseReport] | Dose Report")* [from Current     |
   |                                  | Procedure Description section]   |
   +----------------------------------+----------------------------------+
   | RadiationExpo                    | *(111532, DCM, "Pregnancy        |
   | sure:CodedObservation[pregnancy] | Status")*                        |
   +----------------------------------+----------------------------------+
   | RadiationExpos                   | `(18785-6, LN, "Indications for  |
   | ure:CodedObservation[indication] | Procedure"                       |
   |                                  | ) <http://loinc.org/18785-6/>`__ |
   +----------------------------------+----------------------------------+
   | RadiationExp                     | *(113921, DCM, "Radiation        |
   | osure:CodedObservation[exposure] | Exposure")*                      |
   +----------------------------------+----------------------------------+
   | Radia                            |                                  |
   | tionExposure:QuantityMeasurement |                                  |
   +----------------------------------+----------------------------------+
   | RadiationExposure:               |                                  |
   | RadioactivityDose                |                                  |
   +----------------------------------+----------------------------------+
   | RadiationExposure:               |                                  |
   | Radiopharmaceutical              |                                  |
   +----------------------------------+----------------------------------+
   | RadiationExposure:               | *(113922, DCM, "Radioactive      |
   | FreeTextRadiopharmaceutical      | Substance Administered")*        |
   +----------------------------------+----------------------------------+

The Radiation Exposure Content Item in uses Value Type TEXT, not NUM,
and is therefore mapped to a Coded Observation entry in accordance with
`Text Observations <#sect_C.4.3.2>`__.

.. _sect_C.4.4.4:

Key Images
^^^^^^^^^^

specifies a section structure for the Key Images section of an SR, which
allows mapping into the equivalent CDA subsection of the Impression
section.

.. table:: Key Image mapping from SR

   +----------------------------------+----------------------------------+
   | CDA Business Name                | DICOM SR                         |
   +==================================+==================================+
   | KeyImages: Title                 | "Key Images" [or equivalent in   |
   |                                  | local language]                  |
   +----------------------------------+----------------------------------+
   | KeyImages: Text                  | *(113012, DCM, "Key Object       |
   |                                  | Description")*                   |
   +----------------------------------+----------------------------------+
   | KeyImages: Text: GraphicRef[*]   | [Reference to ObservationMedia   |
   |                                  | entry]                           |
   +----------------------------------+----------------------------------+
   | KeyImages: Text: ExtRef[*]: URL  | [WADO link constructed from      |
   |                                  | image reference]                 |
   +----------------------------------+----------------------------------+
   | KeyImages: SOPInstance[*]        | [See `Image                      |
   |                                  | Observations <#sect_C.4.3.3>`__] |
   +----------------------------------+----------------------------------+
   | KeyImages: Graphic[*]: Image     | [Thumbnail constructed from      |
   |                                  | referenced image]                |
   +----------------------------------+----------------------------------+
   | KeyImages: Graphic[*]: MediaType | [recommended "image/jpeg"]       |
   +----------------------------------+----------------------------------+
   | KeyImages: Graphic[*]: ImageURI  |                                  |
   +----------------------------------+----------------------------------+

.. _sect_C.5:

Example
-------

.. _sect_C.5.1:

DICOM SR "Basic Diagnostic Imaging Report" (TID 2000)
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

The SR sample document encoding includes information on the SR document
body tree depth (column 1: SR Tree Depth), nesting level for nested
artifacts such as sequences and sequence items (column 2: Nesting),
DICOM attribute names (column 3: Attribute), DICOM tag (column 4: Tag),
the DICOM attribute value representation (Column 5: VR as specified in
PS3.5), the hexadecimal value of value length (column 6: VL (hex)) and
the sample document attribute values (column 7: Value).

.. table:: Sample document encoding

   +---------+---------+---------+---------+----+---------+---------+
   | SR Tree | Nesting | At      | Tag     | VR | VL      | Value   |
   | Depth   |         | tribute |         |    | (hex)   |         |
   +=========+=========+=========+=========+====+=========+=========+
   |         |         | I       | (000    | DA | 0008    | 2       |
   |         |         | nstance | 8,0012) |    |         | 0060827 |
   |         |         | C       |         |    |         |         |
   |         |         | reation |         |    |         |         |
   |         |         | Date    |         |    |         |         |
   +---------+---------+---------+---------+----+---------+---------+
   |         |         | I       | (000    | TM | 0006    | 224157  |
   |         |         | nstance | 8,0013) |    |         |         |
   |         |         | C       |         |    |         |         |
   |         |         | reation |         |    |         |         |
   |         |         | Time    |         |    |         |         |
   +---------+---------+---------+---------+----+---------+---------+
   |         |         | I       | (000    | UI | 001c    | 1.2.27  |
   |         |         | nstance | 8,0014) |    |         | 6.0.723 |
   |         |         | Creator |         |    |         | 0010.3. |
   |         |         | UID     |         |    |         | 0.3.5.4 |
   +---------+---------+---------+---------+----+---------+---------+
   |         |         | SOP     | (000    | UI | 001e    | 1       |
   |         |         | Class   | 8,0016) |    |         | .2.840. |
   |         |         | UID     |         |    |         | 10008.5 |
   |         |         |         |         |    |         | .1.4.1. |
   |         |         |         |         |    |         | 1.88.22 |
   +---------+---------+---------+---------+----+---------+---------+
   |         |         | SOP     | (000    | UI | 003c    | 1.2     |
   |         |         | I       | 8,0018) |    |         | .840.11 |
   |         |         | nstance |         |    |         | 3619.2. |
   |         |         | UID     |         |    |         | 62.9940 |
   |         |         |         |         |    |         | 4478552 |
   |         |         |         |         |    |         | 8.20060 |
   |         |         |         |         |    |         | 823.200 |
   |         |         |         |         |    |         | 6082322 |
   |         |         |         |         |    |         | 32322.9 |
   +---------+---------+---------+---------+----+---------+---------+
   |         |         | Study   | (000    | DA | 0008    | 2       |
   |         |         | Date    | 8,0020) |    |         | 0060823 |
   +---------+---------+---------+---------+----+---------+---------+
   |         |         | Content | (000    | DA | 0008    | 2       |
   |         |         | Date    | 8,0023) |    |         | 0060823 |
   +---------+---------+---------+---------+----+---------+---------+
   |         |         | Study   | (000    | TM | 0006    | 222400  |
   |         |         | Time    | 8,0030) |    |         |         |
   +---------+---------+---------+---------+----+---------+---------+
   |         |         | Content | (000    | TM | 0006    | 224352  |
   |         |         | Time    | 8,0033) |    |         |         |
   +---------+---------+---------+---------+----+---------+---------+
   |         |         | Ac      | (000    | SH | 0008    | 1       |
   |         |         | cession | 8,0050) |    |         | 0523475 |
   |         |         | Number  |         |    |         |         |
   +---------+---------+---------+---------+----+---------+---------+
   |         |         | Issuer  | (000    | SQ | f       |         |
   |         |         | of      | 8,0051) |    | fffffff |         |
   |         |         | Ac      |         |    |         |         |
   |         |         | cession |         |    |         |         |
   |         |         | Number  |         |    |         |         |
   |         |         | S       |         |    |         |         |
   |         |         | equence |         |    |         |         |
   +---------+---------+---------+---------+----+---------+---------+
   |         | %item   |         |         |    |         |         |
   +---------+---------+---------+---------+----+---------+---------+
   |         | >       | Local   | (004    | UT | 0008    | WUH-RIS |
   |         |         | Na      | 0,0032) |    |         |         |
   |         |         | mespace |         |    |         |         |
   |         |         | Entity  |         |    |         |         |
   |         |         | ID      |         |    |         |         |
   +---------+---------+---------+---------+----+---------+---------+
   |         | >       | Un      | (004    | UT | 0024    | 1.2.840 |
   |         |         | iversal | 0,0032) |    |         | .113619 |
   |         |         | Entity  |         |    |         | .2.62.9 |
   |         |         | ID      |         |    |         | 9404478 |
   |         |         |         |         |    |         | 5528.27 |
   +---------+---------+---------+---------+----+---------+---------+
   |         | >       | Un      | (004    | CS | 0004    | ISO     |
   |         |         | iversal | 0,0033) |    |         |         |
   |         |         | Entity  |         |    |         |         |
   |         |         | ID Type |         |    |         |         |
   +---------+---------+---------+---------+----+---------+---------+
   |         | %       |         |         |    |         |         |
   |         | enditem |         |         |    |         |         |
   +---------+---------+---------+---------+----+---------+---------+
   |         | %endseq |         |         |    |         |         |
   +---------+---------+---------+---------+----+---------+---------+
   |         |         | M       | (000    | CS | 0002    | SR      |
   |         |         | odality | 8,0060) |    |         |         |
   +---------+---------+---------+---------+----+---------+---------+
   |         |         | Manuf   | (000    | LO | 000a    | Di      |
   |         |         | acturer | 8,0070) |    |         | comWg20 |
   +---------+---------+---------+---------+----+---------+---------+
   |         |         | Re      | (000    | PN | 0010    | S       |
   |         |         | ferring | 8,0090) |    |         | mith^Jo |
   |         |         | Phys    |         |    |         | hn^^^MD |
   |         |         | ician's |         |    |         |         |
   |         |         | Name    |         |    |         |         |
   +---------+---------+---------+---------+----+---------+---------+
   |         |         | Pr      | (000    | SQ | f       |         |
   |         |         | ocedure | 8,1032) |    | fffffff |         |
   |         |         | Code    |         |    |         |         |
   |         |         | S       |         |    |         |         |
   |         |         | equence |         |    |         |         |
   +---------+---------+---------+---------+----+---------+---------+
   |         | %item   |         |         |    |         |         |
   +---------+---------+---------+---------+----+---------+---------+
   |         | >       | Code    | (000    | SH | 0006    | 11123   |
   |         |         | Value   | 8,0100) |    |         |         |
   +---------+---------+---------+---------+----+---------+---------+
   |         | >       | Coding  | (000    | SH | 0008    | 99WUHID |
   |         |         | Scheme  | 8,0102) |    |         |         |
   |         |         | Des     |         |    |         |         |
   |         |         | ignator |         |    |         |         |
   +---------+---------+---------+---------+----+---------+---------+
   |         | >       | Code    | (000    | LO | 000c    | X-Ray   |
   |         |         | Meaning | 8,0104) |    |         | Study   |
   +---------+---------+---------+---------+----+---------+---------+
   |         | %       |         |         |    |         |         |
   |         | enditem |         |         |    |         |         |
   +---------+---------+---------+---------+----+---------+---------+
   |         | %endseq |         |         |    |         |         |
   +---------+---------+---------+---------+----+---------+---------+
   |         |         | Ref     | (000    | SQ | f       |         |
   |         |         | erenced | 8,1111) |    | fffffff |         |
   |         |         | Pe      |         |    |         |         |
   |         |         | rformed |         |    |         |         |
   |         |         | Pr      |         |    |         |         |
   |         |         | ocedure |         |    |         |         |
   |         |         | Step    |         |    |         |         |
   |         |         | S       |         |    |         |         |
   |         |         | equence |         |    |         |         |
   +---------+---------+---------+---------+----+---------+---------+
   |         | %endseq |         |         |    |         |         |
   +---------+---------+---------+---------+----+---------+---------+
   |         |         | Pa      | (001    | PN | 0008    | D       |
   |         |         | tient's | 0,0010) |    |         | oe^John |
   |         |         | Name    |         |    |         |         |
   +---------+---------+---------+---------+----+---------+---------+
   |         |         | Patient | (001    | LO | 000a    | 000     |
   |         |         | ID      | 0,0020) |    |         | 0680029 |
   +---------+---------+---------+---------+----+---------+---------+
   |         |         | Issuer  | (001    | LO | 001a    | World   |
   |         |         | of      | 0,0021) |    |         | Uni     |
   |         |         | Patient |         |    |         | versity |
   |         |         | ID      |         |    |         | H       |
   |         |         |         |         |    |         | ospital |
   +---------+---------+---------+---------+----+---------+---------+
   |         |         | Issuer  | (001    | SQ | f       |         |
   |         |         | of      | 0,0024) |    | fffffff |         |
   |         |         | Patient |         |    |         |         |
   |         |         | ID      |         |    |         |         |
   |         |         | Qua     |         |    |         |         |
   |         |         | lifiers |         |    |         |         |
   |         |         | S       |         |    |         |         |
   |         |         | equence |         |    |         |         |
   +---------+---------+---------+---------+----+---------+---------+
   |         | %item   |         |         |    |         |         |
   +---------+---------+---------+---------+----+---------+---------+
   |         | >       | Un      | (004    | UT | 0024    | 1.2.840 |
   |         |         | iversal | 0,0032) |    |         | .113619 |
   |         |         | Entity  |         |    |         | .2.62.9 |
   |         |         | ID      |         |    |         | 9404478 |
   |         |         |         |         |    |         | 5528.10 |
   +---------+---------+---------+---------+----+---------+---------+
   |         | >       | Un      | (004    | CS | 0004    | ISO     |
   |         |         | iversal | 0,0033) |    |         |         |
   |         |         | Entity  |         |    |         |         |
   |         |         | ID Type |         |    |         |         |
   +---------+---------+---------+---------+----+---------+---------+
   |         | %       |         |         |    |         |         |
   |         | enditem |         |         |    |         |         |
   +---------+---------+---------+---------+----+---------+---------+
   |         | %endseq |         |         |    |         |         |
   +---------+---------+---------+---------+----+---------+---------+
   |         |         | Pa      | (001    | DA | 0008    | 1       |
   |         |         | tient's | 0,0030) |    |         | 9641128 |
   |         |         | Birth   |         |    |         |         |
   |         |         | Date    |         |    |         |         |
   +---------+---------+---------+---------+----+---------+---------+
   |         |         | Pa      | (001    | CS | 0002    | M       |
   |         |         | tient's | 0,0040) |    |         |         |
   |         |         | Sex     |         |    |         |         |
   +---------+---------+---------+---------+----+---------+---------+
   |         |         | Study   | (002    | UI | 002e    | 1.2     |
   |         |         | I       | 0,000d) |    |         | .840.11 |
   |         |         | nstance |         |    |         | 3619.2. |
   |         |         | UID     |         |    |         | 62.9940 |
   |         |         |         |         |    |         | 4478552 |
   |         |         |         |         |    |         | 8.11428 |
   |         |         |         |         |    |         | 9542805 |
   +---------+---------+---------+---------+----+---------+---------+
   |         |         | Series  | (002    | UI | 0036    | 1.2.    |
   |         |         | I       | 0,000e) |    |         | 840.113 |
   |         |         | nstance |         |    |         | 619.2.6 |
   |         |         | UID     |         |    |         | 2.99404 |
   |         |         |         |         |    |         | 4785528 |
   |         |         |         |         |    |         | .200608 |
   |         |         |         |         |    |         | 2322314 |
   |         |         |         |         |    |         | 2485052 |
   +---------+---------+---------+---------+----+---------+---------+
   |         |         | Study   | (002    | SH | 0008    | 1       |
   |         |         | ID      | 0,0010) |    |         | 0523475 |
   +---------+---------+---------+---------+----+---------+---------+
   |         |         | Series  | (002    | IS | 0004    | 560     |
   |         |         | Number  | 0,0011) |    |         |         |
   +---------+---------+---------+---------+----+---------+---------+
   |         |         | I       | (002    | IS | 0006    | 07851   |
   |         |         | nstance | 0,0013) |    |         |         |
   |         |         | Number  |         |    |         |         |
   +---------+---------+---------+---------+----+---------+---------+
   | 1       |         | Value   | (004    | CS | 000a    | CO      |
   |         |         | Type    | 0,a040) |    |         | NTAINER |
   +---------+---------+---------+---------+----+---------+---------+
   | 1       |         | Concept | (004    | SQ | f       |         |
   |         |         | Name    | 0,a043) |    | fffffff |         |
   |         |         | Code    |         |    |         |         |
   |         |         | S       |         |    |         |         |
   |         |         | equence |         |    |         |         |
   +---------+---------+---------+---------+----+---------+---------+
   | 1       | %item   |         |         |    |         |         |
   +---------+---------+---------+---------+----+---------+---------+
   | 1       | >       | Code    | (000    | SH | 0008    | 18782-3 |
   |         |         | Value   | 8,0100) |    |         |         |
   +---------+---------+---------+---------+----+---------+---------+
   | 1       | >       | Coding  | (000    | SH | 0002    | LN      |
   |         |         | Scheme  | 8,0102) |    |         |         |
   |         |         | Des     |         |    |         |         |
   |         |         | ignator |         |    |         |         |
   +---------+---------+---------+---------+----+---------+---------+
   | 1       | >       | Code    | (000    | LO | 000c    | X-Ray   |
   |         |         | Meaning | 8,0104) |    |         | Report  |
   +---------+---------+---------+---------+----+---------+---------+
   | 1       | %       |         |         |    |         |         |
   |         | enditem |         |         |    |         |         |
   +---------+---------+---------+---------+----+---------+---------+
   | 1       | %endseq |         |         |    |         |         |
   +---------+---------+---------+---------+----+---------+---------+
   | 1       |         | Con     | (004    | CS | 0008    | S       |
   |         |         | tinuity | 0,a050) |    |         | EPARATE |
   |         |         | Of      |         |    |         |         |
   |         |         | Content |         |    |         |         |
   +---------+---------+---------+---------+----+---------+---------+
   |         |         | Ve      | (004    | SQ | f       |         |
   |         |         | rifying | 0,a073) |    | fffffff |         |
   |         |         | O       |         |    |         |         |
   |         |         | bserver |         |    |         |         |
   |         |         | S       |         |    |         |         |
   |         |         | equence |         |    |         |         |
   +---------+---------+---------+---------+----+---------+---------+
   |         | %item   |         |         |    |         |         |
   +---------+---------+---------+---------+----+---------+---------+
   |         | >       | Ve      | (004    | LO | 001a    | World   |
   |         |         | rifying | 0,a027) |    |         | Uni     |
   |         |         | Organ   |         |    |         | versity |
   |         |         | ization |         |    |         | H       |
   |         |         |         |         |    |         | ospital |
   +---------+---------+---------+---------+----+---------+---------+
   |         | >       | Verif   | (004    | DT | 000e    | 2006082 |
   |         |         | ication | 0,a030) |    |         | 7141500 |
   |         |         | D       |         |    |         |         |
   |         |         | ateTime |         |    |         |         |
   +---------+---------+---------+---------+----+---------+---------+
   |         | >       | Ve      | (004    | PN | 0012    | Blit    |
   |         |         | rifying | 0,a075) |    |         | z^Richa |
   |         |         | O       |         |    |         | rd^^^MD |
   |         |         | bserver |         |    |         |         |
   |         |         | Name    |         |    |         |         |
   +---------+---------+---------+---------+----+---------+---------+
   |         | >       | Ve      | (004    | SQ | f       |         |
   |         |         | rifying | 0,a088) |    | fffffff |         |
   |         |         | O       |         |    |         |         |
   |         |         | bserver |         |    |         |         |
   |         |         | Identif |         |    |         |         |
   |         |         | ication |         |    |         |         |
   |         |         | Code    |         |    |         |         |
   |         |         | S       |         |    |         |         |
   |         |         | equence |         |    |         |         |
   +---------+---------+---------+---------+----+---------+---------+
   |         | %item   |         |         |    |         |         |
   +---------+---------+---------+---------+----+---------+---------+
   |         | >>      | Code    | (000    | SH | 0008    | 0       |
   |         |         | Value   | 8,0100) |    |         | 8150000 |
   +---------+---------+---------+---------+----+---------+---------+
   |         | >>      | Coding  | (000    | SH | 0008    | 99WUHID |
   |         |         | Scheme  | 8,0102) |    |         |         |
   |         |         | Des     |         |    |         |         |
   |         |         | ignator |         |    |         |         |
   +---------+---------+---------+---------+----+---------+---------+
   |         | >>      | Code    | (000    | LO | 0016    | Ve      |
   |         |         | Meaning | 8,0104) |    |         | rifying |
   |         |         |         |         |    |         | O       |
   |         |         |         |         |    |         | bserver |
   |         |         |         |         |    |         | ID      |
   +---------+---------+---------+---------+----+---------+---------+
   |         | %       |         |         |    |         |         |
   |         | enditem |         |         |    |         |         |
   +---------+---------+---------+---------+----+---------+---------+
   |         | %endseq |         |         |    |         |         |
   +---------+---------+---------+---------+----+---------+---------+
   |         | %       |         |         |    |         |         |
   |         | enditem |         |         |    |         |         |
   +---------+---------+---------+---------+----+---------+---------+
   |         | %endseq |         |         |    |         |         |
   +---------+---------+---------+---------+----+---------+---------+
   |         |         | Ref     | (004    | SQ | f       |         |
   |         |         | erenced | 0,a370) |    | fffffff |         |
   |         |         | Request |         |    |         |         |
   |         |         | S       |         |    |         |         |
   |         |         | equence |         |    |         |         |
   +---------+---------+---------+---------+----+---------+---------+
   |         | %item   |         |         |    |         |         |
   +---------+---------+---------+---------+----+---------+---------+
   |         | >       | Ac      | (000    | SH | 0008    | 1       |
   |         |         | cession | 8,0050) |    |         | 0523475 |
   |         |         | Number  |         |    |         |         |
   +---------+---------+---------+---------+----+---------+---------+
   |         | >       | Issuer  | (000    | SQ | f       |         |
   |         |         | of      | 8,0051) |    | fffffff |         |
   |         |         | Ac      |         |    |         |         |
   |         |         | cession |         |    |         |         |
   |         |         | Number  |         |    |         |         |
   |         |         | S       |         |    |         |         |
   |         |         | equence |         |    |         |         |
   +---------+---------+---------+---------+----+---------+---------+
   |         | %item   |         |         |    |         |         |
   +---------+---------+---------+---------+----+---------+---------+
   |         | >>      | Local   | (004    | UT | 0008    | WUH-RIS |
   |         |         | Na      | 0,0032) |    |         |         |
   |         |         | mespace |         |    |         |         |
   |         |         | Entity  |         |    |         |         |
   |         |         | ID      |         |    |         |         |
   +---------+---------+---------+---------+----+---------+---------+
   |         | >>      | Un      | (004    | UT | 0024    | 1.2.840 |
   |         |         | iversal | 0,0032) |    |         | .113619 |
   |         |         | Entity  |         |    |         | .2.62.9 |
   |         |         | ID      |         |    |         | 9404478 |
   |         |         |         |         |    |         | 5528.27 |
   +---------+---------+---------+---------+----+---------+---------+
   |         | >>      | Un      | (004    | CS | 0004    | ISO     |
   |         |         | iversal | 0,0033) |    |         |         |
   |         |         | Entity  |         |    |         |         |
   |         |         | ID Type |         |    |         |         |
   +---------+---------+---------+---------+----+---------+---------+
   |         | %       |         |         |    |         |         |
   |         | enditem |         |         |    |         |         |
   +---------+---------+---------+---------+----+---------+---------+
   |         | %endseq |         |         |    |         |         |
   +---------+---------+---------+---------+----+---------+---------+
   |         | >       | Ref     | (000    | SQ | f       |         |
   |         |         | erenced | 8,1110) |    | fffffff |         |
   |         |         | Study   |         |    |         |         |
   |         |         | S       |         |    |         |         |
   |         |         | equence |         |    |         |         |
   +---------+---------+---------+---------+----+---------+---------+
   |         | %item   |         |         |    |         |         |
   +---------+---------+---------+---------+----+---------+---------+
   |         | >>      | Ref     | (000    | UI | 001a    | 1.2.    |
   |         |         | erenced | 8,1150) |    |         | 840.100 |
   |         |         | SOP     |         |    |         | 08.5.1. |
   |         |         | Class   |         |    |         | 4.1.1.1 |
   |         |         | UID     |         |    |         |         |
   +---------+---------+---------+---------+----+---------+---------+
   |         | >>      | Ref     | (000    | UI | 003c    | 1.2     |
   |         |         | erenced | 8,1155) |    |         | .840.11 |
   |         |         | SOP     |         |    |         | 3619.2. |
   |         |         | I       |         |    |         | 62.9940 |
   |         |         | nstance |         |    |         | 4478552 |
   |         |         | UID     |         |    |         | 8.20060 |
   |         |         |         |         |    |         | 823.200 |
   |         |         |         |         |    |         | 6082322 |
   |         |         |         |         |    |         | 32322.3 |
   +---------+---------+---------+---------+----+---------+---------+
   |         | %       |         |         |    |         |         |
   |         | enditem |         |         |    |         |         |
   +---------+---------+---------+---------+----+---------+---------+
   |         | %endseq |         |         |    |         |         |
   +---------+---------+---------+---------+----+---------+---------+
   |         | >       | Study   | (002    | UI | 002e    | 1.2     |
   |         |         | I       | 0,000d) |    |         | .840.11 |
   |         |         | nstance |         |    |         | 3619.2. |
   |         |         | UID     |         |    |         | 62.9940 |
   |         |         |         |         |    |         | 4478552 |
   |         |         |         |         |    |         | 8.11428 |
   |         |         |         |         |    |         | 9542805 |
   +---------+---------+---------+---------+----+---------+---------+
   |         | >       | Re      | (003    | LO | 0020    | CHEST   |
   |         |         | quested | 2,1060) |    |         | TWO     |
   |         |         | Pr      |         |    |         | VIEWS,  |
   |         |         | ocedure |         |    |         | PA AND  |
   |         |         | Desc    |         |    |         | LATERAL |
   |         |         | ription |         |    |         |         |
   +---------+---------+---------+---------+----+---------+---------+
   |         | >       | Re      | (003    | SQ | f       |         |
   |         |         | quested | 2,1064) |    | fffffff |         |
   |         |         | Pr      |         |    |         |         |
   |         |         | ocedure |         |    |         |         |
   |         |         | Code    |         |    |         |         |
   |         |         | S       |         |    |         |         |
   |         |         | equence |         |    |         |         |
   +---------+---------+---------+---------+----+---------+---------+
   |         | %item   |         |         |    |         |         |
   +---------+---------+---------+---------+----+---------+---------+
   |         | >>      | Code    | (000    | SH | 0006    | 11123   |
   |         |         | Value   | 8,0100) |    |         |         |
   +---------+---------+---------+---------+----+---------+---------+
   |         | >>      | Coding  | (000    | SH | 0008    | 99WUHID |
   |         |         | Scheme  | 8,0102) |    |         |         |
   |         |         | Des     |         |    |         |         |
   |         |         | ignator |         |    |         |         |
   +---------+---------+---------+---------+----+---------+---------+
   |         | >>      | Code    | (000    | LO | 000c    | X-Ray   |
   |         |         | Meaning | 8,0104) |    |         | Study   |
   +---------+---------+---------+---------+----+---------+---------+
   |         | %       |         |         |    |         |         |
   |         | enditem |         |         |    |         |         |
   +---------+---------+---------+---------+----+---------+---------+
   |         | %endseq |         |         |    |         |         |
   +---------+---------+---------+---------+----+---------+---------+
   |         | >       | Order   | (004    | SQ | f       |         |
   |         |         | Placer  | 0,0026) |    | fffffff |         |
   |         |         | Ide     |         |    |         |         |
   |         |         | ntifier |         |    |         |         |
   |         |         | S       |         |    |         |         |
   |         |         | equence |         |    |         |         |
   +---------+---------+---------+---------+----+---------+---------+
   |         | %item   |         |         |    |         |         |
   +---------+---------+---------+---------+----+---------+---------+
   |         | >>      | Local   | (004    | UT | 0008    | W       |
   |         |         | Na      | 0,0032) |    |         | UH-CPOE |
   |         |         | mespace |         |    |         |         |
   |         |         | Entity  |         |    |         |         |
   |         |         | ID      |         |    |         |         |
   +---------+---------+---------+---------+----+---------+---------+
   |         | >>      | Un      | (004    | UT | 0024    | 1.2.840 |
   |         |         | iversal | 0,0032) |    |         | .113619 |
   |         |         | Entity  |         |    |         | .2.62.9 |
   |         |         | ID      |         |    |         | 9404478 |
   |         |         |         |         |    |         | 5528.29 |
   +---------+---------+---------+---------+----+---------+---------+
   |         | >>      | Un      | (004    | CS | 0004    | ISO     |
   |         |         | iversal | 0,0033) |    |         |         |
   |         |         | Entity  |         |    |         |         |
   |         |         | ID Type |         |    |         |         |
   +---------+---------+---------+---------+----+---------+---------+
   |         | %       |         |         |    |         |         |
   |         | enditem |         |         |    |         |         |
   +---------+---------+---------+---------+----+---------+---------+
   |         | %endseq |         |         |    |         |         |
   +---------+---------+---------+---------+----+---------+---------+
   |         | >       | Re      | (004    | SH | 0006    | 123453  |
   |         |         | quested | 0,1001) |    |         |         |
   |         |         | Pr      |         |    |         |         |
   |         |         | ocedure |         |    |         |         |
   |         |         | ID      |         |    |         |         |
   +---------+---------+---------+---------+----+---------+---------+
   |         | >       | Reason  | (004    | LO | 0014    | Su      |
   |         |         | for the | 0,1002) |    |         | spected |
   |         |         | Re      |         |    |         | lung    |
   |         |         | quested |         |    |         | tumor   |
   |         |         | Pr      |         |    |         |         |
   |         |         | ocedure |         |    |         |         |
   +---------+---------+---------+---------+----+---------+---------+
   |         | >       | Placer  | (004    | LO | 0006    | 123451  |
   |         |         | Order   | 0,2016) |    |         |         |
   |         |         | Number/ |         |    |         |         |
   |         |         | Imaging |         |    |         |         |
   |         |         | Service |         |    |         |         |
   |         |         | Request |         |    |         |         |
   +---------+---------+---------+---------+----+---------+---------+
   |         | %       |         |         |    |         |         |
   |         | enditem |         |         |    |         |         |
   +---------+---------+---------+---------+----+---------+---------+
   |         | %endseq |         |         |    |         |         |
   +---------+---------+---------+---------+----+---------+---------+
   |         |         | Pe      | (004    | SQ | f       |         |
   |         |         | rformed | 0,a372) |    | fffffff |         |
   |         |         | Pr      |         |    |         |         |
   |         |         | ocedure |         |    |         |         |
   |         |         | Code    |         |    |         |         |
   |         |         | S       |         |    |         |         |
   |         |         | equence |         |    |         |         |
   +---------+---------+---------+---------+----+---------+---------+
   |         | %item   |         |         |    |         |         |
   +---------+---------+---------+---------+----+---------+---------+
   |         | >       | Code    | (000    | SH | 0006    | 11123   |
   |         |         | Value   | 8,0100) |    |         |         |
   +---------+---------+---------+---------+----+---------+---------+
   |         | >       | Coding  | (000    | SH | 0008    | 99WUHID |
   |         |         | Scheme  | 8,0102) |    |         |         |
   |         |         | Des     |         |    |         |         |
   |         |         | ignator |         |    |         |         |
   +---------+---------+---------+---------+----+---------+---------+
   |         | >       | Code    | (000    | LO | 000c    | X-Ray   |
   |         |         | Meaning | 8,0104) |    |         | Study   |
   +---------+---------+---------+---------+----+---------+---------+
   |         | %       |         |         |    |         |         |
   |         | enditem |         |         |    |         |         |
   +---------+---------+---------+---------+----+---------+---------+
   |         | %endseq |         |         |    |         |         |
   +---------+---------+---------+---------+----+---------+---------+
   |         |         | Current | (004    | SQ | f       |         |
   |         |         | Re      | 0,a375) |    | fffffff |         |
   |         |         | quested |         |    |         |         |
   |         |         | Pr      |         |    |         |         |
   |         |         | ocedure |         |    |         |         |
   |         |         | E       |         |    |         |         |
   |         |         | vidence |         |    |         |         |
   |         |         | S       |         |    |         |         |
   |         |         | equence |         |    |         |         |
   +---------+---------+---------+---------+----+---------+---------+
   |         | %item   |         |         |    |         |         |
   +---------+---------+---------+---------+----+---------+---------+
   |         | >       | Ref     | (000    | SQ | f       |         |
   |         |         | erenced | 8,1115) |    | fffffff |         |
   |         |         | Series  |         |    |         |         |
   |         |         | S       |         |    |         |         |
   |         |         | equence |         |    |         |         |
   +---------+---------+---------+---------+----+---------+---------+
   |         | %item   |         |         |    |         |         |
   +---------+---------+---------+---------+----+---------+---------+
   |         | >>      | Ref     | (000    | SQ | f       |         |
   |         |         | erenced | 8,1199) |    | fffffff |         |
   |         |         | SOP     |         |    |         |         |
   |         |         | S       |         |    |         |         |
   |         |         | equence |         |    |         |         |
   +---------+---------+---------+---------+----+---------+---------+
   |         | %item   |         |         |    |         |         |
   +---------+---------+---------+---------+----+---------+---------+
   |         | >>>     | Ref     | (000    | UI | 001a    | 1.2.    |
   |         |         | erenced | 8,1150) |    |         | 840.100 |
   |         |         | SOP     |         |    |         | 08.5.1. |
   |         |         | Class   |         |    |         | 4.1.1.1 |
   |         |         | UID     |         |    |         |         |
   +---------+---------+---------+---------+----+---------+---------+
   |         | >>>     | Ref     | (000    | UI | 003c    | 1.2     |
   |         |         | erenced | 8,1155) |    |         | .840.11 |
   |         |         | SOP     |         |    |         | 3619.2. |
   |         |         | I       |         |    |         | 62.9940 |
   |         |         | nstance |         |    |         | 4478552 |
   |         |         | UID     |         |    |         | 8.20060 |
   |         |         |         |         |    |         | 823.200 |
   |         |         |         |         |    |         | 6082322 |
   |         |         |         |         |    |         | 32322.3 |
   +---------+---------+---------+---------+----+---------+---------+
   |         | %       |         |         |    |         |         |
   |         | enditem |         |         |    |         |         |
   +---------+---------+---------+---------+----+---------+---------+
   |         | %item   |         |         |    |         |         |
   +---------+---------+---------+---------+----+---------+---------+
   |         | >>>     | Ref     | (000    | UI | 001a    | 1.2.    |
   |         |         | erenced | 8,1150) |    |         | 840.100 |
   |         |         | SOP     |         |    |         | 08.5.1. |
   |         |         | Class   |         |    |         | 4.1.1.1 |
   |         |         | UID     |         |    |         |         |
   +---------+---------+---------+---------+----+---------+---------+
   |         | >>>     | Ref     | (000    | UI | 003c    | 1.2     |
   |         |         | erenced | 8,1155) |    |         | .840.11 |
   |         |         | SOP     |         |    |         | 3619.2. |
   |         |         | I       |         |    |         | 62.9940 |
   |         |         | nstance |         |    |         | 4478552 |
   |         |         | UID     |         |    |         | 8.20060 |
   |         |         |         |         |    |         | 823.200 |
   |         |         |         |         |    |         | 6082322 |
   |         |         |         |         |    |         | 31422.3 |
   +---------+---------+---------+---------+----+---------+---------+
   |         | %       |         |         |    |         |         |
   |         | enditem |         |         |    |         |         |
   +---------+---------+---------+---------+----+---------+---------+
   |         | %endseq |         |         |    |         |         |
   +---------+---------+---------+---------+----+---------+---------+
   |         | >>      | Series  | (002    | UI | 0036    | 1.2.    |
   |         |         | I       | 0,000e) |    |         | 840.113 |
   |         |         | nstance |         |    |         | 619.2.6 |
   |         |         | UID     |         |    |         | 2.99404 |
   |         |         |         |         |    |         | 4785528 |
   |         |         |         |         |    |         | .200608 |
   |         |         |         |         |    |         | 2322314 |
   |         |         |         |         |    |         | 2485051 |
   +---------+---------+---------+---------+----+---------+---------+
   |         | %       |         |         |    |         |         |
   |         | enditem |         |         |    |         |         |
   +---------+---------+---------+---------+----+---------+---------+
   |         | %endseq |         |         |    |         |         |
   +---------+---------+---------+---------+----+---------+---------+
   |         | >       | Study   | (002    | UI | 002e    | 1.2     |
   |         |         | I       | 0,000d) |    |         | .840.11 |
   |         |         | nstance |         |    |         | 3619.2. |
   |         |         | UID     |         |    |         | 62.9940 |
   |         |         |         |         |    |         | 4478552 |
   |         |         |         |         |    |         | 8.11428 |
   |         |         |         |         |    |         | 9542805 |
   +---------+---------+---------+---------+----+---------+---------+
   |         | %       |         |         |    |         |         |
   |         | enditem |         |         |    |         |         |
   +---------+---------+---------+---------+----+---------+---------+
   |         | %endseq |         |         |    |         |         |
   +---------+---------+---------+---------+----+---------+---------+
   |         |         | Com     | (004    | CS | 0008    | C       |
   |         |         | pletion | 0,a491) |    |         | OMPLETE |
   |         |         | Flag    |         |    |         |         |
   +---------+---------+---------+---------+----+---------+---------+
   |         |         | Verif   | (004    | CS | 0008    | V       |
   |         |         | ication | 0,a493) |    |         | ERIFIED |
   |         |         | Flag    |         |    |         |         |
   +---------+---------+---------+---------+----+---------+---------+
   | 1       |         | Content | (004    | SQ | f       |         |
   |         |         | S       | 0,a730) |    | fffffff |         |
   |         |         | equence |         |    |         |         |
   +---------+---------+---------+---------+----+---------+---------+
   | 1.1     | %item   |         |         |    |         |         |
   +---------+---------+---------+---------+----+---------+---------+
   | 1.1     | >       | Relat   | (004    | CS | 0010    | HAS     |
   |         |         | ionship | 0,a010) |    |         | CONCEPT |
   |         |         | Type    |         |    |         | MOD     |
   +---------+---------+---------+---------+----+---------+---------+
   | 1.1     | >       | Value   | (004    | CS | 0004    | CODE    |
   |         |         | Type    | 0,a040) |    |         |         |
   +---------+---------+---------+---------+----+---------+---------+
   | 1.1     | >       | Concept | (004    | SQ | f       |         |
   |         |         | Name    | 0,a043) |    | fffffff |         |
   |         |         | Code    |         |    |         |         |
   |         |         | S       |         |    |         |         |
   |         |         | equence |         |    |         |         |
   +---------+---------+---------+---------+----+---------+---------+
   | 1.1     | %item   |         |         |    |         |         |
   +---------+---------+---------+---------+----+---------+---------+
   | 1.1     | >>      | Code    | (000    | SH | 0006    | 122142  |
   |         |         | Value   | 8,0100) |    |         |         |
   +---------+---------+---------+---------+----+---------+---------+
   | 1.1     | >>      | Coding  | (000    | SH | 0004    | DCM     |
   |         |         | Scheme  | 8,0102) |    |         |         |
   |         |         | Des     |         |    |         |         |
   |         |         | ignator |         |    |         |         |
   +---------+---------+---------+---------+----+---------+---------+
   | 1.1     | >>      | Code    | (000    | LO | 0018    | Acqu    |
   |         |         | Meaning | 8,0104) |    |         | isition |
   |         |         |         |         |    |         | Device  |
   |         |         |         |         |    |         | Type    |
   +---------+---------+---------+---------+----+---------+---------+
   | 1.1     | %       |         |         |    |         |         |
   |         | enditem |         |         |    |         |         |
   +---------+---------+---------+---------+----+---------+---------+
   | 1.1     | %endseq |         |         |    |         |         |
   +---------+---------+---------+---------+----+---------+---------+
   | 1.1     | >       | Concept | (004    | SQ | f       |         |
   |         |         | Code    | 0,a168) |    | fffffff |         |
   |         |         | S       |         |    |         |         |
   |         |         | equence |         |    |         |         |
   +---------+---------+---------+---------+----+---------+---------+
   | 1.1     | %item   |         |         |    |         |         |
   +---------+---------+---------+---------+----+---------+---------+
   | 1.1     | >>      | Code    | (000    | SH | 0002    | XR      |
   |         |         | Value   | 8,0100) |    |         |         |
   +---------+---------+---------+---------+----+---------+---------+
   | 1.1     | >>      | Coding  | (000    | SH | 0004    | DCM     |
   |         |         | Scheme  | 8,0102) |    |         |         |
   |         |         | Des     |         |    |         |         |
   |         |         | ignator |         |    |         |         |
   +---------+---------+---------+---------+----+---------+---------+
   | 1.1     | >>      | Code    | (000    | LO | 0002    | XR      |
   |         |         | Meaning | 8,0104) |    |         |         |
   +---------+---------+---------+---------+----+---------+---------+
   | 1.1     | %       |         |         |    |         |         |
   |         | enditem |         |         |    |         |         |
   +---------+---------+---------+---------+----+---------+---------+
   | 1.1     | %endseq |         |         |    |         |         |
   +---------+---------+---------+---------+----+---------+---------+
   | 1.1     | %       |         |         |    |         |         |
   |         | enditem |         |         |    |         |         |
   +---------+---------+---------+---------+----+---------+---------+
   | 1.2     | %item   |         |         |    |         |         |
   +---------+---------+---------+---------+----+---------+---------+
   | 1.2     | >       | Relat   | (004    | CS | 0010    | HAS     |
   |         |         | ionship | 0,a010) |    |         | CONCEPT |
   |         |         | Type    |         |    |         | MOD     |
   +---------+---------+---------+---------+----+---------+---------+
   | 1.2     | >       | Value   | (004    | CS | 0004    | CODE    |
   |         |         | Type    | 0,a040) |    |         |         |
   +---------+---------+---------+---------+----+---------+---------+
   | 1.2     | >       | Concept | (004    | SQ | f       |         |
   |         |         | Name    | 0,a043) |    | fffffff |         |
   |         |         | Code    |         |    |         |         |
   |         |         | S       |         |    |         |         |
   |         |         | equence |         |    |         |         |
   +---------+---------+---------+---------+----+---------+---------+
   | 1.2     | %item   |         |         |    |         |         |
   +---------+---------+---------+---------+----+---------+---------+
   | 1.2     | >>      | Code    | (000    | SH | 0006    | 123014  |
   |         |         | Value   | 8,0100) |    |         |         |
   +---------+---------+---------+---------+----+---------+---------+
   | 1.2     | >>      | Coding  | (000    | SH | 0004    | DCM     |
   |         |         | Scheme  | 8,0102) |    |         |         |
   |         |         | Des     |         |    |         |         |
   |         |         | ignator |         |    |         |         |
   +---------+---------+---------+---------+----+---------+---------+
   | 1.2     | >>      | Code    | (000    | LO | 000e    | Target  |
   |         |         | Meaning | 8,0104) |    |         | Region  |
   +---------+---------+---------+---------+----+---------+---------+
   | 1.2     | %       |         |         |    |         |         |
   |         | enditem |         |         |    |         |         |
   +---------+---------+---------+---------+----+---------+---------+
   | 1.2     | %endseq |         |         |    |         |         |
   +---------+---------+---------+---------+----+---------+---------+
   | 1.2     | >       | Concept | (004    | SQ | f       |         |
   |         |         | Code    | 0,a168) |    | fffffff |         |
   |         |         | S       |         |    |         |         |
   |         |         | equence |         |    |         |         |
   +---------+---------+---------+---------+----+---------+---------+
   | 1.2     | %item   |         |         |    |         |         |
   +---------+---------+---------+---------+----+---------+---------+
   | 1.2     | >>      | Code    | (000    | SH | 0008    | 5       |
   |         |         | Value   | 8,0100) |    |         | 1185008 |
   +---------+---------+---------+---------+----+---------+---------+
   | 1.2     | >>      | Coding  | (000    | SH | 0004    | SCT     |
   |         |         | Scheme  | 8,0102) |    |         |         |
   |         |         | Des     |         |    |         |         |
   |         |         | ignator |         |    |         |         |
   +---------+---------+---------+---------+----+---------+---------+
   | 1.2     | >>      | Code    | (000    | LO | 0006    | Chest   |
   |         |         | Meaning | 8,0104) |    |         |         |
   +---------+---------+---------+---------+----+---------+---------+
   | 1.2     | %       |         |         |    |         |         |
   |         | enditem |         |         |    |         |         |
   +---------+---------+---------+---------+----+---------+---------+
   | 1.2     | %endseq |         |         |    |         |         |
   +---------+---------+---------+---------+----+---------+---------+
   | 1.2     | %       |         |         |    |         |         |
   |         | enditem |         |         |    |         |         |
   +---------+---------+---------+---------+----+---------+---------+
   | 1.3     | %item   |         |         |    |         |         |
   +---------+---------+---------+---------+----+---------+---------+
   | 1.3     | >       | Relat   | (004    | CS | 0010    | HAS     |
   |         |         | ionship | 0,a010) |    |         | CONCEPT |
   |         |         | Type    |         |    |         | MOD     |
   +---------+---------+---------+---------+----+---------+---------+
   | 1.3     | >       | Value   | (004    | CS | 0004    | CODE    |
   |         |         | Type    | 0,a040) |    |         |         |
   +---------+---------+---------+---------+----+---------+---------+
   | 1.3     | >       | Concept | (004    | SQ | f       |         |
   |         |         | Name    | 0,a043) |    | fffffff |         |
   |         |         | Code    |         |    |         |         |
   |         |         | S       |         |    |         |         |
   |         |         | equence |         |    |         |         |
   +---------+---------+---------+---------+----+---------+---------+
   | 1.3     | %item   |         |         |    |         |         |
   +---------+---------+---------+---------+----+---------+---------+
   | 1.3     | >>      | Code    | (000    | SH | 0006    | 121049  |
   |         |         | Value   | 8,0100) |    |         |         |
   +---------+---------+---------+---------+----+---------+---------+
   | 1.3     | >>      | Coding  | (000    | SH | 0004    | DCM     |
   |         |         | Scheme  | 8,0102) |    |         |         |
   |         |         | Des     |         |    |         |         |
   |         |         | ignator |         |    |         |         |
   +---------+---------+---------+---------+----+---------+---------+
   | 1.3     | >>      | Code    | (000    | LO | 0028    | L       |
   |         |         | Meaning | 8,0104) |    |         | anguage |
   |         |         |         |         |    |         | of      |
   |         |         |         |         |    |         | Content |
   |         |         |         |         |    |         | Item    |
   |         |         |         |         |    |         | and     |
   |         |         |         |         |    |         | Desc    |
   |         |         |         |         |    |         | endants |
   +---------+---------+---------+---------+----+---------+---------+
   | 1.3     | %       |         |         |    |         |         |
   |         | enditem |         |         |    |         |         |
   +---------+---------+---------+---------+----+---------+---------+
   | 1.3     | %endseq |         |         |    |         |         |
   +---------+---------+---------+---------+----+---------+---------+
   | 1.3     | >       | Concept | (004    | SQ | f       |         |
   |         |         | Code    | 0,a168) |    | fffffff |         |
   |         |         | S       |         |    |         |         |
   |         |         | equence |         |    |         |         |
   +---------+---------+---------+---------+----+---------+---------+
   | 1.3     | %item   |         |         |    |         |         |
   +---------+---------+---------+---------+----+---------+---------+
   | 1.3     | >>      | Code    | (000    | SH | 0006    | en-US   |
   |         |         | Value   | 8,0100) |    |         |         |
   +---------+---------+---------+---------+----+---------+---------+
   | 1.3     | >>      | Coding  | (000    | SH | 0008    | I       |
   |         |         | Scheme  | 8,0102) |    |         | SO639_1 |
   |         |         | Des     |         |    |         |         |
   |         |         | ignator |         |    |         |         |
   +---------+---------+---------+---------+----+---------+---------+
   | 1.3     | >>      | Code    | (000    | LO | 000e    | English |
   |         |         | Meaning | 8,0104) |    |         | (U.S.)  |
   +---------+---------+---------+---------+----+---------+---------+
   | 1.3     | %       |         |         |    |         |         |
   |         | enditem |         |         |    |         |         |
   +---------+---------+---------+---------+----+---------+---------+
   | 1.3     | %endseq |         |         |    |         |         |
   +---------+---------+---------+---------+----+---------+---------+
   | 1.3     | %       |         |         |    |         |         |
   |         | enditem |         |         |    |         |         |
   +---------+---------+---------+---------+----+---------+---------+
   | 1.4     | %item   |         |         |    |         |         |
   +---------+---------+---------+---------+----+---------+---------+
   | 1.4     | >       | Relat   | (004    | CS | 0010    | HAS     |
   |         |         | ionship | 0,a010) |    |         | CONCEPT |
   |         |         | Type    |         |    |         | MOD     |
   +---------+---------+---------+---------+----+---------+---------+
   | 1.4     | >       | Value   | (004    | CS | 0004    | TEXT    |
   |         |         | Type    | 0,a040) |    |         |         |
   +---------+---------+---------+---------+----+---------+---------+
   | 1.4     | >       | Concept | (004    | SQ | f       |         |
   |         |         | Name    | 0,a043) |    | fffffff |         |
   |         |         | Code    |         |    |         |         |
   |         |         | S       |         |    |         |         |
   |         |         | equence |         |    |         |         |
   +---------+---------+---------+---------+----+---------+---------+
   | 1.4     | %item   |         |         |    |         |         |
   +---------+---------+---------+---------+----+---------+---------+
   | 1.4     | >>      | Code    | (000    | SH | 0006    | 121050  |
   |         |         | Value   | 8,0100) |    |         |         |
   +---------+---------+---------+---------+----+---------+---------+
   | 1.4     | >>      | Coding  | (000    | SH | 0004    | DCM     |
   |         |         | Scheme  | 8,0102) |    |         |         |
   |         |         | Des     |         |    |         |         |
   |         |         | ignator |         |    |         |         |
   +---------+---------+---------+---------+----+---------+---------+
   | 1.4     | >>      | Code    | (000    | LO | 0022    | Equ     |
   |         |         | Meaning | 8,0104) |    |         | ivalent |
   |         |         |         |         |    |         | Meaning |
   |         |         |         |         |    |         | of      |
   |         |         |         |         |    |         | Concept |
   |         |         |         |         |    |         | Name    |
   +---------+---------+---------+---------+----+---------+---------+
   | 1.4     | %       |         |         |    |         |         |
   |         | enditem |         |         |    |         |         |
   +---------+---------+---------+---------+----+---------+---------+
   | 1.4     | %endseq |         |         |    |         |         |
   +---------+---------+---------+---------+----+---------+---------+
   | 1.4     | >       | Text    | (004    | UT | 001c    | Chest   |
   |         |         | Value   | 0,a160) |    |         | X-Ray,  |
   |         |         |         |         |    |         | PA and  |
   |         |         |         |         |    |         | LAT     |
   |         |         |         |         |    |         | View    |
   +---------+---------+---------+---------+----+---------+---------+
   | 1.4     | %       |         |         |    |         |         |
   |         | enditem |         |         |    |         |         |
   +---------+---------+---------+---------+----+---------+---------+
   | 1.5     | %item   |         |         |    |         |         |
   +---------+---------+---------+---------+----+---------+---------+
   | 1.5     | >       | Relat   | (004    | CS | 0010    | HAS OBS |
   |         |         | ionship | 0,a010) |    |         | CONTEXT |
   |         |         | Type    |         |    |         |         |
   +---------+---------+---------+---------+----+---------+---------+
   | 1.5     | >       | Value   | (004    | CS | 0004    | CODE    |
   |         |         | Type    | 0,a040) |    |         |         |
   +---------+---------+---------+---------+----+---------+---------+
   | 1.5     | >       | Concept | (004    | SQ | f       |         |
   |         |         | Name    | 0,a043) |    | fffffff |         |
   |         |         | Code    |         |    |         |         |
   |         |         | S       |         |    |         |         |
   |         |         | equence |         |    |         |         |
   +---------+---------+---------+---------+----+---------+---------+
   | 1.5     | %item   |         |         |    |         |         |
   +---------+---------+---------+---------+----+---------+---------+
   | 1.5     | >>      | Code    | (000    | SH | 0006    | 121005  |
   |         |         | Value   | 8,0100) |    |         |         |
   +---------+---------+---------+---------+----+---------+---------+
   | 1.5     | >>      | Coding  | (000    | SH | 0004    | DCM     |
   |         |         | Scheme  | 8,0102) |    |         |         |
   |         |         | Des     |         |    |         |         |
   |         |         | ignator |         |    |         |         |
   +---------+---------+---------+---------+----+---------+---------+
   | 1.5     | >>      | Code    | (000    | LO | 000e    | O       |
   |         |         | Meaning | 8,0104) |    |         | bserver |
   |         |         |         |         |    |         | Type    |
   +---------+---------+---------+---------+----+---------+---------+
   | 1.5     | %       |         |         |    |         |         |
   |         | enditem |         |         |    |         |         |
   +---------+---------+---------+---------+----+---------+---------+
   | 1.5     | %endseq |         |         |    |         |         |
   +---------+---------+---------+---------+----+---------+---------+
   | 1.5     | >       | Concept | (004    | SQ | f       |         |
   |         |         | Code    | 0,a168) |    | fffffff |         |
   |         |         | S       |         |    |         |         |
   |         |         | equence |         |    |         |         |
   +---------+---------+---------+---------+----+---------+---------+
   | 1.5     | %item   |         |         |    |         |         |
   +---------+---------+---------+---------+----+---------+---------+
   | 1.5     | >>      | Code    | (000    | SH | 0006    | 121006  |
   |         |         | Value   | 8,0100) |    |         |         |
   +---------+---------+---------+---------+----+---------+---------+
   | 1.5     | >>      | Coding  | (000    | SH | 0004    | DCM     |
   |         |         | Scheme  | 8,0102) |    |         |         |
   |         |         | Des     |         |    |         |         |
   |         |         | ignator |         |    |         |         |
   +---------+---------+---------+---------+----+---------+---------+
   | 1.5     | >>      | Code    | (000    | LO | 0006    | Person  |
   |         |         | Meaning | 8,0104) |    |         |         |
   +---------+---------+---------+---------+----+---------+---------+
   | 1.5     | %       |         |         |    |         |         |
   |         | enditem |         |         |    |         |         |
   +---------+---------+---------+---------+----+---------+---------+
   | 1.5     | %endseq |         |         |    |         |         |
   +---------+---------+---------+---------+----+---------+---------+
   | 1.5     | %       |         |         |    |         |         |
   |         | enditem |         |         |    |         |         |
   +---------+---------+---------+---------+----+---------+---------+
   | 1.6     | %item   |         |         |    |         |         |
   +---------+---------+---------+---------+----+---------+---------+
   | 1.6     | >       | Relat   | (004    | CS | 0010    | HAS OBS |
   |         |         | ionship | 0,a010) |    |         | CONTEXT |
   |         |         | Type    |         |    |         |         |
   +---------+---------+---------+---------+----+---------+---------+
   | 1.6     | >       | Value   | (004    | CS | 0006    | PNAME   |
   |         |         | Type    | 0,a040) |    |         |         |
   +---------+---------+---------+---------+----+---------+---------+
   | 1.6     | >       | Concept | (004    | SQ | f       |         |
   |         |         | Name    | 0,a043) |    | fffffff |         |
   |         |         | Code    |         |    |         |         |
   |         |         | S       |         |    |         |         |
   |         |         | equence |         |    |         |         |
   +---------+---------+---------+---------+----+---------+---------+
   | 1.6     | %item   |         |         |    |         |         |
   +---------+---------+---------+---------+----+---------+---------+
   | 1.6     | >>      | Code    | (000    | SH | 0006    | 121008  |
   |         |         | Value   | 8,0100) |    |         |         |
   +---------+---------+---------+---------+----+---------+---------+
   | 1.6     | >>      | Coding  | (000    | SH | 0004    | DCM     |
   |         |         | Scheme  | 8,0102) |    |         |         |
   |         |         | Des     |         |    |         |         |
   |         |         | ignator |         |    |         |         |
   +---------+---------+---------+---------+----+---------+---------+
   | 1.6     | >>      | Code    | (000    | LO | 0014    | Person  |
   |         |         | Meaning | 8,0104) |    |         | O       |
   |         |         |         |         |    |         | bserver |
   |         |         |         |         |    |         | Name    |
   +---------+---------+---------+---------+----+---------+---------+
   | 1.6     | %       |         |         |    |         |         |
   |         | enditem |         |         |    |         |         |
   +---------+---------+---------+---------+----+---------+---------+
   | 1.6     | %endseq |         |         |    |         |         |
   +---------+---------+---------+---------+----+---------+---------+
   | 1.6     | >       | Person  | (004    | PN | 0012    | Blit    |
   |         |         | Name    | 0,a123) |    |         | z^Richa |
   |         |         |         |         |    |         | rd^^^MD |
   +---------+---------+---------+---------+----+---------+---------+
   | 1.6     | %       |         |         |    |         |         |
   |         | enditem |         |         |    |         |         |
   +---------+---------+---------+---------+----+---------+---------+
   | 1.7     | %item   |         |         |    |         |         |
   +---------+---------+---------+---------+----+---------+---------+
   | 1.7     | >       | Relat   | (004    | CS | 0008    | C       |
   |         |         | ionship | 0,a010) |    |         | ONTAINS |
   |         |         | Type    |         |    |         |         |
   +---------+---------+---------+---------+----+---------+---------+
   | 1.7     | >       | Value   | (004    | CS | 000a    | CO      |
   |         |         | Type    | 0,a040) |    |         | NTAINER |
   +---------+---------+---------+---------+----+---------+---------+
   | 1.7     | >       | Concept | (004    | SQ | f       |         |
   |         |         | Name    | 0,a043) |    | fffffff |         |
   |         |         | Code    |         |    |         |         |
   |         |         | S       |         |    |         |         |
   |         |         | equence |         |    |         |         |
   +---------+---------+---------+---------+----+---------+---------+
   | 1.7     | %item   |         |         |    |         |         |
   +---------+---------+---------+---------+----+---------+---------+
   | 1.7     | >>      | Code    | (000    | SH | 0006    | 121060  |
   |         |         | Value   | 8,0100) |    |         |         |
   +---------+---------+---------+---------+----+---------+---------+
   | 1.7     | >>      | Coding  | (000    | SH | 0004    | DCM     |
   |         |         | Scheme  | 8,0102) |    |         |         |
   |         |         | Des     |         |    |         |         |
   |         |         | ignator |         |    |         |         |
   +---------+---------+---------+---------+----+---------+---------+
   | 1.7     | >>      | Code    | (000    | LO | 0008    | History |
   |         |         | Meaning | 8,0104) |    |         |         |
   +---------+---------+---------+---------+----+---------+---------+
   | 1.7     | %       |         |         |    |         |         |
   |         | enditem |         |         |    |         |         |
   +---------+---------+---------+---------+----+---------+---------+
   | 1.7     | %endseq |         |         |    |         |         |
   +---------+---------+---------+---------+----+---------+---------+
   | 1.7     | >       | Con     | (004    | CS | 0008    | S       |
   |         |         | tinuity | 0,a050) |    |         | EPARATE |
   |         |         | Of      |         |    |         |         |
   |         |         | Content |         |    |         |         |
   +---------+---------+---------+---------+----+---------+---------+
   | 1.7     | >       | Content | (004    | SQ | f       |         |
   |         |         | S       | 0,a730) |    | fffffff |         |
   |         |         | equence |         |    |         |         |
   +---------+---------+---------+---------+----+---------+---------+
   | 1.7.1   | %item   |         |         |    |         |         |
   +---------+---------+---------+---------+----+---------+---------+
   | 1.7.1   | >>      | Relat   | (004    | CS | 0008    | C       |
   |         |         | ionship | 0,a010) |    |         | ONTAINS |
   |         |         | Type    |         |    |         |         |
   +---------+---------+---------+---------+----+---------+---------+
   | 1.7.1   | >>      | Value   | (004    | CS | 0004    | TEXT    |
   |         |         | Type    | 0,a040) |    |         |         |
   +---------+---------+---------+---------+----+---------+---------+
   | 1.7.1   | >>      | Concept | (004    | SQ | f       |         |
   |         |         | Name    | 0,a043) |    | fffffff |         |
   |         |         | Code    |         |    |         |         |
   |         |         | S       |         |    |         |         |
   |         |         | equence |         |    |         |         |
   +---------+---------+---------+---------+----+---------+---------+
   | 1.7.1   | %item   |         |         |    |         |         |
   +---------+---------+---------+---------+----+---------+---------+
   | 1.7.1   | >>>     | Code    | (000    | SH | 0006    | 121060  |
   |         |         | Value   | 8,0100) |    |         |         |
   +---------+---------+---------+---------+----+---------+---------+
   | 1.7.1   | >>>     | Coding  | (000    | SH | 0004    | DCM     |
   |         |         | Scheme  | 8,0102) |    |         |         |
   |         |         | Des     |         |    |         |         |
   |         |         | ignator |         |    |         |         |
   +---------+---------+---------+---------+----+---------+---------+
   | 1.7.1   | >>>     | Code    | (000    | LO | 0008    | History |
   |         |         | Meaning | 8,0104) |    |         |         |
   +---------+---------+---------+---------+----+---------+---------+
   | 1.7.1   | %       |         |         |    |         |         |
   |         | enditem |         |         |    |         |         |
   +---------+---------+---------+---------+----+---------+---------+
   | 1.7.1   | %endseq |         |         |    |         |         |
   +---------+---------+---------+---------+----+---------+---------+
   | 1.7.1   | >>      | Text    | (004    | UT | 000c    | Sore    |
   |         |         | Value   | 0,a160) |    |         | throat. |
   +---------+---------+---------+---------+----+---------+---------+
   | 1.7.1   | %       |         |         |    |         |         |
   |         | enditem |         |         |    |         |         |
   +---------+---------+---------+---------+----+---------+---------+
   | 1.7     | %endseq |         |         |    |         |         |
   +---------+---------+---------+---------+----+---------+---------+
   | 1.7     | %       |         |         |    |         |         |
   |         | enditem |         |         |    |         |         |
   +---------+---------+---------+---------+----+---------+---------+
   | 1.8     | %item   |         |         |    |         |         |
   +---------+---------+---------+---------+----+---------+---------+
   | 1.8     | >       | Relat   | (004    | CS | 0008    | C       |
   |         |         | ionship | 0,a010) |    |         | ONTAINS |
   |         |         | Type    |         |    |         |         |
   +---------+---------+---------+---------+----+---------+---------+
   | 1.8     | >       | Value   | (004    | CS | 000a    | CO      |
   |         |         | Type    | 0,a040) |    |         | NTAINER |
   +---------+---------+---------+---------+----+---------+---------+
   | 1.8     | >       | Concept | (004    | SQ | f       |         |
   |         |         | Name    | 0,a043) |    | fffffff |         |
   |         |         | Code    |         |    |         |         |
   |         |         | S       |         |    |         |         |
   |         |         | equence |         |    |         |         |
   +---------+---------+---------+---------+----+---------+---------+
   | 1.8     | %item   |         |         |    |         |         |
   +---------+---------+---------+---------+----+---------+---------+
   | 1.8     | >>      | Code    | (000    | SH | 0006    | 121070  |
   |         |         | Value   | 8,0100) |    |         |         |
   +---------+---------+---------+---------+----+---------+---------+
   | 1.8     | >>      | Coding  | (000    | SH | 0004    | DCM     |
   |         |         | Scheme  | 8,0102) |    |         |         |
   |         |         | Des     |         |    |         |         |
   |         |         | ignator |         |    |         |         |
   +---------+---------+---------+---------+----+---------+---------+
   | 1.8     | >>      | Code    | (000    | LO | 0008    | F       |
   |         |         | Meaning | 8,0104) |    |         | indings |
   +---------+---------+---------+---------+----+---------+---------+
   | 1.8     | %       |         |         |    |         |         |
   |         | enditem |         |         |    |         |         |
   +---------+---------+---------+---------+----+---------+---------+
   | 1.8     | %endseq |         |         |    |         |         |
   +---------+---------+---------+---------+----+---------+---------+
   | 1.8     | >       | Con     | (004    | CS | 0008    | S       |
   |         |         | tinuity | 0,a050) |    |         | EPARATE |
   |         |         | Of      |         |    |         |         |
   |         |         | Content |         |    |         |         |
   +---------+---------+---------+---------+----+---------+---------+
   | 1.8     | >       | Content | (004    | SQ | f       |         |
   |         |         | S       | 0,a730) |    | fffffff |         |
   |         |         | equence |         |    |         |         |
   +---------+---------+---------+---------+----+---------+---------+
   | 1.8.1   | %item   |         |         |    |         |         |
   +---------+---------+---------+---------+----+---------+---------+
   | 1.8.1   | >>      | Relat   | (004    | CS | 0008    | C       |
   |         |         | ionship | 0,a010) |    |         | ONTAINS |
   |         |         | Type    |         |    |         |         |
   +---------+---------+---------+---------+----+---------+---------+
   | 1.8.1   | >>      | Value   | (004    | CS | 0004    | TEXT    |
   |         |         | Type    | 0,a040) |    |         |         |
   +---------+---------+---------+---------+----+---------+---------+
   | 1.8.1   | >>      | Concept | (004    | SQ | f       |         |
   |         |         | Name    | 0,a043) |    | fffffff |         |
   |         |         | Code    |         |    |         |         |
   |         |         | S       |         |    |         |         |
   |         |         | equence |         |    |         |         |
   +---------+---------+---------+---------+----+---------+---------+
   | 1.8.1   | %item   |         |         |    |         |         |
   +---------+---------+---------+---------+----+---------+---------+
   | 1.8.1   | >>>     | Code    | (000    | SH | 0006    | 121071  |
   |         |         | Value   | 8,0100) |    |         |         |
   +---------+---------+---------+---------+----+---------+---------+
   | 1.8.1   | >>>     | Coding  | (000    | SH | 0004    | DCM     |
   |         |         | Scheme  | 8,0102) |    |         |         |
   |         |         | Des     |         |    |         |         |
   |         |         | ignator |         |    |         |         |
   +---------+---------+---------+---------+----+---------+---------+
   | 1.8.1   | >>>     | Code    | (000    | LO | 0008    | Finding |
   |         |         | Meaning | 8,0104) |    |         |         |
   +---------+---------+---------+---------+----+---------+---------+
   | 1.8.1   | %       |         |         |    |         |         |
   |         | enditem |         |         |    |         |         |
   +---------+---------+---------+---------+----+---------+---------+
   | 1.8.1   | %endseq |         |         |    |         |         |
   +---------+---------+---------+---------+----+---------+---------+
   | 1.8.1   | >>      | Text    | (004    | UT | 01ae    | The     |
   |         |         | Value   | 0,a160) |    |         | car     |
   |         |         |         |         |    |         | diomedi |
   |         |         |         |         |    |         | astinum |
   |         |         |         |         |    |         | is      |
   |         |         |         |         |    |         | within  |
   |         |         |         |         |    |         | normal  |
   |         |         |         |         |    |         | limits. |
   |         |         |         |         |    |         | The     |
   |         |         |         |         |    |         | trachea |
   |         |         |         |         |    |         | is      |
   |         |         |         |         |    |         | m       |
   |         |         |         |         |    |         | idline. |
   |         |         |         |         |    |         | The     |
   |         |         |         |         |    |         | pre     |
   |         |         |         |         |    |         | viously |
   |         |         |         |         |    |         | de      |
   |         |         |         |         |    |         | scribed |
   |         |         |         |         |    |         | opacity |
   |         |         |         |         |    |         | at the  |
   |         |         |         |         |    |         | medial  |
   |         |         |         |         |    |         | right   |
   |         |         |         |         |    |         | lung    |
   |         |         |         |         |    |         | base    |
   |         |         |         |         |    |         | has     |
   |         |         |         |         |    |         | c       |
   |         |         |         |         |    |         | leared. |
   |         |         |         |         |    |         | There   |
   |         |         |         |         |    |         | are no  |
   |         |         |         |         |    |         | new     |
   |         |         |         |         |    |         | infil   |
   |         |         |         |         |    |         | trates. |
   |         |         |         |         |    |         | There   |
   |         |         |         |         |    |         | is a    |
   |         |         |         |         |    |         | new     |
   |         |         |         |         |    |         | round   |
   |         |         |         |         |    |         | density |
   |         |         |         |         |    |         | at the  |
   |         |         |         |         |    |         | left    |
   |         |         |         |         |    |         | hilus,  |
   |         |         |         |         |    |         | sup     |
   |         |         |         |         |    |         | eriorly |
   |         |         |         |         |    |         | (d      |
   |         |         |         |         |    |         | iameter |
   |         |         |         |         |    |         | about   |
   |         |         |         |         |    |         | 45mm).  |
   |         |         |         |         |    |         | A CT    |
   |         |         |         |         |    |         | scan is |
   |         |         |         |         |    |         | reco    |
   |         |         |         |         |    |         | mmended |
   |         |         |         |         |    |         | for     |
   |         |         |         |         |    |         | further |
   |         |         |         |         |    |         | eval    |
   |         |         |         |         |    |         | uation. |
   |         |         |         |         |    |         | The     |
   |         |         |         |         |    |         | pleural |
   |         |         |         |         |    |         | spaces  |
   |         |         |         |         |    |         | are     |
   |         |         |         |         |    |         | clear.  |
   |         |         |         |         |    |         | The     |
   |         |         |         |         |    |         | vis     |
   |         |         |         |         |    |         | ualized |
   |         |         |         |         |    |         | m       |
   |         |         |         |         |    |         | usculos |
   |         |         |         |         |    |         | keletal |
   |         |         |         |         |    |         | str     |
   |         |         |         |         |    |         | uctures |
   |         |         |         |         |    |         | and the |
   |         |         |         |         |    |         | upper   |
   |         |         |         |         |    |         | abdomen |
   |         |         |         |         |    |         | are     |
   |         |         |         |         |    |         | stable  |
   |         |         |         |         |    |         | and     |
   |         |         |         |         |    |         | unrema  |
   |         |         |         |         |    |         | rkable. |
   +---------+---------+---------+---------+----+---------+---------+
   | 1.8.1   | >>      | Content | (004    | SQ | f       |         |
   |         |         | S       | 0,a730) |    | fffffff |         |
   |         |         | equence |         |    |         |         |
   +---------+---------+---------+---------+----+---------+---------+
   | 1.8.1.1 | %item   |         |         |    |         |         |
   +---------+---------+---------+---------+----+---------+---------+
   | 1.8.1.1 | >>>     | Relat   | (004    | CS | 000e    | I       |
   |         |         | ionship | 0,a010) |    |         | NFERRED |
   |         |         | Type    |         |    |         | FROM    |
   +---------+---------+---------+---------+----+---------+---------+
   | 1.8.1.1 | >>>     | Obse    | (004    | DT | 000e    | 2006082 |
   |         |         | rvation | 0,a032) |    |         | 3223912 |
   |         |         | D       |         |    |         |         |
   |         |         | ateTime |         |    |         |         |
   +---------+---------+---------+---------+----+---------+---------+
   | 1.8.1.1 | >>>     | Value   | (004    | CS | 0004    | NUM     |
   |         |         | Type    | 0,a040) |    |         |         |
   +---------+---------+---------+---------+----+---------+---------+
   | 1.8.1.1 | >>>     | Concept | (004    | SQ | f       |         |
   |         |         | Name    | 0,a043) |    | fffffff |         |
   |         |         | Code    |         |    |         |         |
   |         |         | S       |         |    |         |         |
   |         |         | equence |         |    |         |         |
   +---------+---------+---------+---------+----+---------+---------+
   | 1.8.1.1 | %item   |         |         |    |         |         |
   +---------+---------+---------+---------+----+---------+---------+
   | 1.8.1.1 | >>>>    | Code    | (000    | SH | 0008    | 8       |
   |         |         | Value   | 8,0100) |    |         | 1827009 |
   +---------+---------+---------+---------+----+---------+---------+
   | 1.8.1.1 | >>>>    | Coding  | (000    | SH | 0004    | SCT     |
   |         |         | Scheme  | 8,0102) |    |         |         |
   |         |         | Des     |         |    |         |         |
   |         |         | ignator |         |    |         |         |
   +---------+---------+---------+---------+----+---------+---------+
   | 1.8.1.1 | >>>>    | Code    | (000    | LO | 0008    | D       |
   |         |         | Meaning | 8,0104) |    |         | iameter |
   +---------+---------+---------+---------+----+---------+---------+
   | 1.8.1.1 | %       |         |         |    |         |         |
   |         | enditem |         |         |    |         |         |
   +---------+---------+---------+---------+----+---------+---------+
   | 1.8.1.1 | %endseq |         |         |    |         |         |
   +---------+---------+---------+---------+----+---------+---------+
   | 1.8.1.1 | >>>     | M       | (004    | SQ | f       |         |
   |         |         | easured | 0,a300) |    | fffffff |         |
   |         |         | Value   |         |    |         |         |
   |         |         | S       |         |    |         |         |
   |         |         | equence |         |    |         |         |
   +---------+---------+---------+---------+----+---------+---------+
   | 1.8.1.1 | %item   |         |         |    |         |         |
   +---------+---------+---------+---------+----+---------+---------+
   | 1.8.1.1 | >>>>    | Meas    | (004    | SQ | f       |         |
   |         |         | urement | 0,08ea) |    | fffffff |         |
   |         |         | Units   |         |    |         |         |
   |         |         | Code    |         |    |         |         |
   |         |         | S       |         |    |         |         |
   |         |         | equence |         |    |         |         |
   +---------+---------+---------+---------+----+---------+---------+
   | 1.8.1.1 | %item   |         |         |    |         |         |
   +---------+---------+---------+---------+----+---------+---------+
   | 1.8.1.1 | >>>>>   | Code    | (000    | SH | 0002    | mm      |
   |         |         | Value   | 8,0100) |    |         |         |
   +---------+---------+---------+---------+----+---------+---------+
   | 1.8.1.1 | >>>>>   | Coding  | (000    | SH | 0004    | UCUM    |
   |         |         | Scheme  | 8,0102) |    |         |         |
   |         |         | Des     |         |    |         |         |
   |         |         | ignator |         |    |         |         |
   +---------+---------+---------+---------+----+---------+---------+
   | 1.8.1.1 | >>>>>   | Code    | (000    | LO | 0002    | mm      |
   |         |         | Meaning | 8,0104) |    |         |         |
   +---------+---------+---------+---------+----+---------+---------+
   | 1.8.1.1 | %       |         |         |    |         |         |
   |         | enditem |         |         |    |         |         |
   +---------+---------+---------+---------+----+---------+---------+
   | 1.8.1.1 | %endseq |         |         |    |         |         |
   +---------+---------+---------+---------+----+---------+---------+
   | 1.8.1.1 | >>>>    | Numeric | (004    | DS | 0002    | 45      |
   |         |         | Value   | 0,a30a) |    |         |         |
   +---------+---------+---------+---------+----+---------+---------+
   | 1.8.1.1 | %       |         |         |    |         |         |
   |         | enditem |         |         |    |         |         |
   +---------+---------+---------+---------+----+---------+---------+
   | 1.8.1.1 | %endseq |         |         |    |         |         |
   +---------+---------+---------+---------+----+---------+---------+
   | 1.8.1.1 | >>>     | Content | (004    | SQ | f       |         |
   |         |         | S       | 0,a730) |    | fffffff |         |
   |         |         | equence |         |    |         |         |
   +---------+---------+---------+---------+----+---------+---------+
   | 1.      | %item   |         |         |    |         |         |
   | 8.1.1.1 |         |         |         |    |         |         |
   +---------+---------+---------+---------+----+---------+---------+
   | 1.      | >>>>    | Ref     | (000    | SQ | f       |         |
   | 8.1.1.1 |         | erenced | 8,1199) |    | fffffff |         |
   |         |         | SOP     |         |    |         |         |
   |         |         | S       |         |    |         |         |
   |         |         | equence |         |    |         |         |
   +---------+---------+---------+---------+----+---------+---------+
   | 1.      | %item   |         |         |    |         |         |
   | 8.1.1.1 |         |         |         |    |         |         |
   +---------+---------+---------+---------+----+---------+---------+
   | 1.      | >>>>>   | Ref     | (000    | UI | 001a    | 1.2.    |
   | 8.1.1.1 |         | erenced | 8,1150) |    |         | 840.100 |
   |         |         | SOP     |         |    |         | 08.5.1. |
   |         |         | Class   |         |    |         | 4.1.1.1 |
   |         |         | UID     |         |    |         |         |
   +---------+---------+---------+---------+----+---------+---------+
   | 1.      | >>>>>   | Ref     | (000    | UI | 003c    | 1.2     |
   | 8.1.1.1 |         | erenced | 8,1155) |    |         | .840.11 |
   |         |         | SOP     |         |    |         | 3619.2. |
   |         |         | I       |         |    |         | 62.9940 |
   |         |         | nstance |         |    |         | 4478552 |
   |         |         | UID     |         |    |         | 8.20060 |
   |         |         |         |         |    |         | 823.200 |
   |         |         |         |         |    |         | 6082322 |
   |         |         |         |         |    |         | 32322.3 |
   +---------+---------+---------+---------+----+---------+---------+
   | 1.      | %       |         |         |    |         |         |
   | 8.1.1.1 | enditem |         |         |    |         |         |
   +---------+---------+---------+---------+----+---------+---------+
   | 1.      | %endseq |         |         |    |         |         |
   | 8.1.1.1 |         |         |         |    |         |         |
   +---------+---------+---------+---------+----+---------+---------+
   | 1.      | >>>>    | Relat   | (004    | CS | 000e    | I       |
   | 8.1.1.1 |         | ionship | 0,a010) |    |         | NFERRED |
   |         |         | Type    |         |    |         | FROM    |
   +---------+---------+---------+---------+----+---------+---------+
   | 1.      | >>>>    | Value   | (004    | CS | 0006    | IMAGE   |
   | 8.1.1.1 |         | Type    | 0,a040) |    |         |         |
   +---------+---------+---------+---------+----+---------+---------+
   | 1.      | >>>>    | Concept | (004    | SQ | f       |         |
   | 8.1.1.1 |         | Name    | 0,a043) |    | fffffff |         |
   |         |         | Code    |         |    |         |         |
   |         |         | S       |         |    |         |         |
   |         |         | equence |         |    |         |         |
   +---------+---------+---------+---------+----+---------+---------+
   | 1.      | %item   |         |         |    |         |         |
   | 8.1.1.1 |         |         |         |    |         |         |
   +---------+---------+---------+---------+----+---------+---------+
   | 1.      | >>>>>   | Code    | (000    | SH | 0006    | 121112  |
   | 8.1.1.1 |         | Value   | 8,0100) |    |         |         |
   +---------+---------+---------+---------+----+---------+---------+
   | 1.      | >>>>>   | Coding  | (000    | SH | 0004    | DCM     |
   | 8.1.1.1 |         | Scheme  | 8,0102) |    |         |         |
   |         |         | Des     |         |    |         |         |
   |         |         | ignator |         |    |         |         |
   +---------+---------+---------+---------+----+---------+---------+
   | 1.      | >>>>>   | Code    | (000    | LO | 0016    | Source  |
   | 8.1.1.1 |         | Meaning | 8,0104) |    |         | of      |
   |         |         |         |         |    |         | Meas    |
   |         |         |         |         |    |         | urement |
   +---------+---------+---------+---------+----+---------+---------+
   | 1.      | %       |         |         |    |         |         |
   | 8.1.1.1 | enditem |         |         |    |         |         |
   +---------+---------+---------+---------+----+---------+---------+
   | 1.      | %endseq |         |         |    |         |         |
   | 8.1.1.1 |         |         |         |    |         |         |
   +---------+---------+---------+---------+----+---------+---------+
   | 1.      | %       |         |         |    |         |         |
   | 8.1.1.1 | enditem |         |         |    |         |         |
   +---------+---------+---------+---------+----+---------+---------+
   | 1.8.1.1 | %endseq |         |         |    |         |         |
   +---------+---------+---------+---------+----+---------+---------+
   | 1.8.1.1 | %       |         |         |    |         |         |
   |         | enditem |         |         |    |         |         |
   +---------+---------+---------+---------+----+---------+---------+
   | 1.8.1   | %endseq |         |         |    |         |         |
   +---------+---------+---------+---------+----+---------+---------+
   | 1.8.1   | %       |         |         |    |         |         |
   |         | enditem |         |         |    |         |         |
   +---------+---------+---------+---------+----+---------+---------+
   | 1.8     | %endseq |         |         |    |         |         |
   +---------+---------+---------+---------+----+---------+---------+
   | 1.8     | %       |         |         |    |         |         |
   |         | enditem |         |         |    |         |         |
   +---------+---------+---------+---------+----+---------+---------+
   | 1.9     | %item   |         |         |    |         |         |
   +---------+---------+---------+---------+----+---------+---------+
   | 1.9     | >       | Relat   | (004    | CS | 0008    | C       |
   |         |         | ionship | 0,a010) |    |         | ONTAINS |
   |         |         | Type    |         |    |         |         |
   +---------+---------+---------+---------+----+---------+---------+
   | 1.9     | >       | Value   | (004    | CS | 000a    | CO      |
   |         |         | Type    | 0,a040) |    |         | NTAINER |
   +---------+---------+---------+---------+----+---------+---------+
   | 1.9     | >       | Concept | (004    | SQ | f       |         |
   |         |         | Name    | 0,a043) |    | fffffff |         |
   |         |         | Code    |         |    |         |         |
   |         |         | S       |         |    |         |         |
   |         |         | equence |         |    |         |         |
   +---------+---------+---------+---------+----+---------+---------+
   | 1.9     | %item   |         |         |    |         |         |
   +---------+---------+---------+---------+----+---------+---------+
   | 1.9     | >>      | Code    | (000    | SH | 0006    | 121072  |
   |         |         | Value   | 8,0100) |    |         |         |
   +---------+---------+---------+---------+----+---------+---------+
   | 1.9     | >>      | Coding  | (000    | SH | 0004    | DCM     |
   |         |         | Scheme  | 8,0102) |    |         |         |
   |         |         | Des     |         |    |         |         |
   |         |         | ignator |         |    |         |         |
   +---------+---------+---------+---------+----+---------+---------+
   | 1.9     | >>      | Code    | (000    | LO | 000c    | Impr    |
   |         |         | Meaning | 8,0104) |    |         | essions |
   +---------+---------+---------+---------+----+---------+---------+
   | 1.9     | %       |         |         |    |         |         |
   |         | enditem |         |         |    |         |         |
   +---------+---------+---------+---------+----+---------+---------+
   | 1.9     | %endseq |         |         |    |         |         |
   +---------+---------+---------+---------+----+---------+---------+
   | 1.9     | >       | Con     | (004    | CS | 0008    | S       |
   |         |         | tinuity | 0,a050) |    |         | EPARATE |
   |         |         | Of      |         |    |         |         |
   |         |         | Content |         |    |         |         |
   +---------+---------+---------+---------+----+---------+---------+
   | 1.9     | >       | Content | (004    | SQ | f       |         |
   |         |         | S       | 0,a730) |    | fffffff |         |
   |         |         | equence |         |    |         |         |
   +---------+---------+---------+---------+----+---------+---------+
   | 1.9.1   | %item   |         |         |    |         |         |
   +---------+---------+---------+---------+----+---------+---------+
   | 1.9.1   | >>      | Relat   | (004    | CS | 0008    | C       |
   |         |         | ionship | 0,a010) |    |         | ONTAINS |
   |         |         | Type    |         |    |         |         |
   +---------+---------+---------+---------+----+---------+---------+
   | 1.9.1   | >>      | Value   | (004    | CS | 0004    | TEXT    |
   |         |         | Type    | 0,a040) |    |         |         |
   +---------+---------+---------+---------+----+---------+---------+
   | 1.9.1   | >>      | Concept | (004    | SQ | f       |         |
   |         |         | Name    | 0,a043) |    | fffffff |         |
   |         |         | Code    |         |    |         |         |
   |         |         | S       |         |    |         |         |
   |         |         | equence |         |    |         |         |
   +---------+---------+---------+---------+----+---------+---------+
   | 1.9.1   | %item   |         |         |    |         |         |
   +---------+---------+---------+---------+----+---------+---------+
   | 1.9.1   | >>>     | Code    | (000    | SH | 0006    | 121073  |
   |         |         | Value   | 8,0100) |    |         |         |
   +---------+---------+---------+---------+----+---------+---------+
   | 1.9.1   | >>>     | Coding  | (000    | SH | 0004    | DCM     |
   |         |         | Scheme  | 8,0102) |    |         |         |
   |         |         | Des     |         |    |         |         |
   |         |         | ignator |         |    |         |         |
   +---------+---------+---------+---------+----+---------+---------+
   | 1.9.1   | >>>     | Code    | (000    | LO | 000a    | Imp     |
   |         |         | Meaning | 8,0104) |    |         | ression |
   +---------+---------+---------+---------+----+---------+---------+
   | 1.9.1   | %       |         |         |    |         |         |
   |         | enditem |         |         |    |         |         |
   +---------+---------+---------+---------+----+---------+---------+
   | 1.9.1   | %endseq |         |         |    |         |         |
   +---------+---------+---------+---------+----+---------+---------+
   | 1.9.1   | >>      | Text    | (004    | UT | 009c    | No      |
   |         |         | Value   | 0,a160) |    |         | acute   |
   |         |         |         |         |    |         | c       |
   |         |         |         |         |    |         | ardiopu |
   |         |         |         |         |    |         | lmonary |
   |         |         |         |         |    |         | p       |
   |         |         |         |         |    |         | rocess. |
   |         |         |         |         |    |         | Round   |
   |         |         |         |         |    |         | density |
   |         |         |         |         |    |         | in left |
   |         |         |         |         |    |         | s       |
   |         |         |         |         |    |         | uperior |
   |         |         |         |         |    |         | hilus,  |
   |         |         |         |         |    |         | further |
   |         |         |         |         |    |         | eva     |
   |         |         |         |         |    |         | luation |
   |         |         |         |         |    |         | with CT |
   |         |         |         |         |    |         | is      |
   |         |         |         |         |    |         | reco    |
   |         |         |         |         |    |         | mmended |
   |         |         |         |         |    |         | as      |
   |         |         |         |         |    |         | und     |
   |         |         |         |         |    |         | erlying |
   |         |         |         |         |    |         | mal     |
   |         |         |         |         |    |         | ignancy |
   |         |         |         |         |    |         | is not  |
   |         |         |         |         |    |         | ex      |
   |         |         |         |         |    |         | cluded. |
   +---------+---------+---------+---------+----+---------+---------+
   | 1.9.1   | %       |         |         |    |         |         |
   |         | enditem |         |         |    |         |         |
   +---------+---------+---------+---------+----+---------+---------+
   | 1.9     | %endseq |         |         |    |         |         |
   +---------+---------+---------+---------+----+---------+---------+
   | 1.9     | %       |         |         |    |         |         |
   |         | enditem |         |         |    |         |         |
   +---------+---------+---------+---------+----+---------+---------+
   | 1       | %endseq |         |         |    |         |         |
   +---------+---------+---------+---------+----+---------+---------+

.. _sect_C.5.2:

Transcoded HL7 CDA Release 2 Imaging Report
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

::

   <?xml version="1.0" encoding="utf-8"?>
   <?xml-stylesheet type="text/xsl" href="CDA-DIR.xsl"?>
   <ClinicalDocument xmlns="urn:hl7-org:v3"
           xmlns:voc="urn:hl7-org:v3/voc"
           xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
           xmlns:ps3-20="urn:dicom-org:ps3-20"
           xsi:schemaLocation="urn:hl7-org:v3 CDA.xsd">
       <realmCode code="UV"/>
       <typeId root="2.16.840.1.113883.1.3" extension="POCD_HD000040"/>
       <templateId root="1.2.840.10008.9.1"/>
       <templateId root="1.2.840.10008.9.20"/>
       <templateId root="1.2.840.10008.9.21"/>
       <templateId root="1.2.840.10008.9.22"/>
       <id root="1.2.840.113619.2.62.994044785528.12"extension="20060828170821659"/>
       <code code="18748-4" codeSystem="2.16.840.1.113883.6.1"
           codeSystemName="LOINC" displayName="Diagnostic Imaging Report"/>
       <title>Chest X-Ray, PA and LAT View</title>
       <effectiveTime value="20060828170821"/>
       <confidentialityCode code="N" codeSystem="2.16.840.1.113883.5.25"/>
       <languageCode code="en-US"/>
       <recordTarget>
           <patientRole>
               <id root="1.2.840.113619.2.62.994044785528.10" extension="0000680029"/>
               <addr nullFlavor="NI"/>
               <telecom nullFlavor="NI"/>
               <patient>
                   <name>
                       <given>John</given>
                       <family>Doe</family>
                   </name>
                   <administrativeGenderCode codeSystem="2.16.840.1.113883.5.1"code="M"/>
                   <birthTime value="19641128"/>
               </patient>
           </patientRole>
       </recordTarget>
       <author>
           <time value="20060823224352"/>
           <assignedAuthor>
               <id extension="121008" root="2.16.840.1.113883.19.5"/>
               <addr nullFlavor="NI"/>
               <telecom nullFlavor="NI"/>
               <assignedPerson>
                   <name>
                       <given>Richard</given>
                       <family>Blitz</family>
                       <suffix>MD</suffix>
                   </name>
               </assignedPerson>
           </assignedAuthor>
       </author>
       <custodian>
           <!-- custodian values have been added based on organizational policy (int his
            case they are not mapped from the SR sample document) -->
           <assignedCustodian>
               <representedCustodianOrganization>
                   <id root="2.16.840.1.113883.19.5"/>
                   <name>World University Hospital</name>
                   <telecom nullFlavor="NI"/>
                   <addr nullFlavor="NI"/>
               </representedCustodianOrganization>
           </assignedCustodian>
       </custodian>
       <!-- legal authenticator present in sample, document is VERIFIED -->
       <legalAuthenticator>
           <time value="20060827141500"/>
           <!-- Verification DateTime (0040,A030) -->
           <signatureCode code="S"/>
           <assignedEntity>
               <id extension="08150000" root="1.2.840.113619.2.62.994044785528.33"/>
               <addr nullFlavor="NI"/>
               <telecom nullFlavor="NI"/>
               <assignedPerson>
                   <name>
                       <given>Richard</given>
                       <family>Blitz</family>
                       <suffix>MD</suffix>
                   </name>
               </assignedPerson>
           </assignedEntity>
       </legalAuthenticator>
       <!-- Mapped from Referring Physician's Name (0008,0090) SR sample document -->
       <participant typeCode="REF">
           <associatedEntity classCode="PROV">
               <id nullFlavor="NI"/>
               <addr nullFlavor="NI"/>
               <telecom nullFlavor="NI"/>
               <associatedPerson>
                   <name>
                       <given>John</given>
                       <family>Smith</family>
                       <suffix>MD</suffix>
                   </name>
               </associatedPerson>
           </associatedEntity>
       </participant>
       <inFulfillmentOf>
           <order>
               <id extension="123451" root="1.2.840.113619.2.62.994044785528.29"/>
               <ps3-20:accessionNumber extension="10523475"root="1.2.840.113619.2.62.994044785528.27"/>
           </order>
       </inFulfillmentOf>
       <documentationOf>
           <serviceEvent classCode="ACT">
               <id root="1.2.840.113619.2.62.994044785528.114289542805"/>
               <!-- Study Instance UID -->
               <code code="11123" codeSystem="1.2.840.113619.2.62.5661"
                   codeSystemName="99WUHID" displayName="X-Ray Study"/>
               <translation code="XR" displayName="XR"
                   codeSystem="1.2.840.10008.2.16.4" codeSystemName="DCM"/>
               <translation code="51185008" displayName="Chest"
                   codeSystem="2.16.840.1.113883.6.96" codeSystemName="SNOMED CT"/>
               <!-- anatomy code mapped from old style SNOMED in SR to new -->
           </code>
       </code>
       <effectiveTime>
           <low value="20060823222400"/>
       </effectiveTime>
   </serviceEvent>
   </documentationOf>
   <!-- transformation of a DICOM SR -->
   <relatedDocument typeCode="XFRM">
       <parentDocument>
           <id root="1.2.840.113619.2.62.994044785528.20060823.200608232232322.9"/>
           <!-- SOP Instance UID (0008,0018) of SR sample document-->
       </parentDocument>
   </relatedDocument>
   <component>
       <structuredBody>
           <component>
               <!--**************** Clinical Information Section *****************-->
               <section>
                   <templateId root="1.2.840.10008.9.2"/>
                   <code code="55752-0" codeSystem="2.16.840.1.113883.6.1"codeSystemName="LOINC" displayName="Clinical Information"/>
                   <title>Clinical Information</title>
                   <component>
                       <!--**************** Procedure Indications Subsection *****************
                           Section text mapped from "Reason for the Requested Procedure" (0040,1002)
                           within the Referenced Request Sequence (0040,A370) of the SR header, under
                           the assumption that the header attribute value has been displayed to, and
                           accepted by, the legal authenticator.-->
                       <section>
                           <templateId root="2.16.840.1.113883.10.20.22.2.29"/>
                           <id root="1.2.840.10213.2.62.044785528.1142895426"/>
                           <code code="59768-2" codeSystem="2.16.840.1.113883.6.1"
                           codeSystemName="LOINC" displayName="Procedure Indications"/>
                           <title>Indications for Procedure</title>
                           <text>Suspected lung tumor</text>
                       </section>
                       <!--**************** End of Procedure Indications Subsection *****************-->
                   </component>
                   <component>
                       <!--**************** History Subsection *****************-->
                       <section>
                           <templateId root="2.16.840.1.113883.10.20.22.2.39"/>
                           <id root="1.2.840.10213.2.62.7044785528.114289875"/>
                           <code code="11329-0" codeSystem="2.16.840.1.113883.6.1"
                           codeSystemName="LOINC" displayName="History General"/>
                           <title>History</title>
                           <text>
                               <paragraph>
                                   <caption>History</caption>
                                   <content ID="Fndng1">Sore throat.</content>
                               </paragraph>
                           </text>
                           <entry>
                               <!-- History report element (TEXT) -->
                               <observation classCode="OBS" moodCode="EVN">
                                   <templateId root="2.16.840.1.113883.10.20.6.2.12"/>
                                   <code code="121060" codeSystem="1.2.840.10008.2.16.4"
                                       codeSystemName="DCM" displayName="History"/>
                                   <value xsi:type="ED">
                                       <reference value="#Fndng1"/>
                                   </value>
                               </observation>
                           </entry>
                       </section>
                       <!--**************** End of History Subsection *****************-->
                   </component>
                   <!--**************** End of Clinical Information Section *****************-->
               </component>
               <component>
                   <!--**************** Imaging Procedure Description Section *****************-->
                   <section classCode="DOCSECT" moodCode="EVN">
                       <templateId root="1.2.840.10008.9.3"/>
                       <id root="1.2.840.10213.2.62.9940434234785528.11428954534542805"/>
                       <code code="55111-9" codeSystem="2.16.840.1.113883.6.1"
                       codeSystemName="LOINC" displayName="Current Imaging Procedure Description"/>
                       <title>Imaging Procedure Description</title>
                       <text> </text>
                       <entry>
                           <procedure moodCode="EVN" classCode="PROC">
                               <templateId root="1.2.840.10008.9.14"/>
                               <id root="1.2.840.6544.33.9100653988998717.997527582345600170"/>
                               <code code="11123" displayName="X-Ray Study"
                               codeSystem="1.2.840.113619.2.62.5661" codeSystemName="99WUHID"/>
                               <effectiveTime value="20060823222400"/>
                               <methodCode code="XR" displayName="XR"
                               codeSystem="1.2.840.10008.2.16.4" codeSystemName="DCM"/>
                               <targetSiteCode code="51185008" displayName="Chest"
                               codeSystem="2.16.840.1.113883.6.96" codeSystemName="SNOMED CT"/>
                           </procedure>
                       </entry>
                       <component>
                           <!--**************** DICOM Object Catalog Sub-section *****************-->
                           <section classCode="DOCSECT" moodCode="EVN">
                               <templateId root="2.16.840.1.113883.10.20.6.1.1"/>
                               <code code="121181" codeSystem="1.2.840.10008.2.16.4"
                                   codeSystemName="DCM" displayName="DICOM Object Catalog"/>
                               <entry>
                                   <!--**************** Study *****************-->
                                   <act classCode="ACT" moodCode="EVN">
                                       <templateId root="2.16.840.1.113883.10.20.6.2.6"/>
                                       <id root="1.2.840.113619.2.62.994044785528.114289542805"/>
                                       <code code="113014" codeSystem="1.2.840.10008.2.16.4"
                                           codeSystemName="DCM" displayName="Study"/>
                                       <!--**************** Series (Parent SR Document) *****************-->
                                       <entryRelationship typeCode="COMP">
                                           <act classCode="ACT" moodCode="EVN">
                                               <id root="1.2.840.113619.2.62.994044785528.20060823222132232023"/>
                                               <code code="113015" codeSystem="1.2.840.10008.2.16.4"
                                                       codeSystemName="DCM" displayName="Series">
                                                   <qualifier>
                                                       <name code="121139" codeSystem="1.2.840.10008.2.16.4"
                                                           codeSystemName="DCM" displayName="Modality">
                                                       </name>
                                                       <value code="CR" codeSystem="1.2.840.10008.2.16.4"
                                                           codeSystemName="DCM" displayName="SR Document">
                                                       </value>
                                                   </qualifier>
                                               </code>
                                               <!--**************** SOP Instance UID *****************-->
                                               <!-- Reference to SR Document -->
                                               <entryRelationship typeCode="COMP">
                                                   <observation classCode="DGIMG" moodCode="EVN">
                                                       <templateId root="2.16.840.1.113883.10.20.6.2.8"/>
                                                       <id
                                                       root="1.2.840.113619.2.62.994044785528.20060823.200608242334312.3"/>
                                                       <code code="1.2.840.10008.5.1.4.1.1.88.22"codeSystem="1.2.840.10008.2.6.1"
                                                           codeSystemName="DCMUID"displayName="Enhanced SR">
                                                       </code>
                                                       <text mediaType="application/dicom">
                                                           <reference value="http://www.example.org/wado?requestType=WADO
                                                               &amp;studyUID=1.2.840.113619.2.62.994044785528.114289542805
                                                               &amp;seriesUID=1.2.840.113619.2.62.994044785528.20060823222132232023
                                                               &amp;objectUID=1.2.840.113619.2.62.994044785528.20060823.200608232232322.9
                                                               &amp;contentType=application/dicom"/>
                                                           <!--reference to image 1 (PA) -->
                                                       </text>
                                                       <effectiveTime value="20060823223232"/>
                                                   </observation>
                                               </entryRelationship>
                                           </act>
                                       </entryRelationship>
                                       <!--**************** Series (CR Images) *****************-->
                                       <entryRelationship typeCode="COMP">
                                           <act classCode="ACT"
                                               moodCode="EVN">
                                               <id root="1.2.840.113619.2.62.994044785528.20060823223142485051"/>
                                               <code code="113015" codeSystem="1.2.840.10008.2.16.4"
                                                       codeSystemName="DCM" displayName="Series">
                                                   <qualifier>
                                                       <name code="121139" codeSystem="1.2.840.10008.2.16.4"
                                                           codeSystemName="DCM" displayName="Modality">
                                                       </name>
                                                       <value code="CR" codeSystem="1.2.840.10008.2.16.4"
                                                           codeSystemName="DCM" displayName="Computed Radiography">
                                                       </value>
                                                   </qualifier>
                                               </code>
                                               <!--**************** SOP Instance UID *****************-->
                                               <!-- 2 References (chest PA and LAT) -->
                                               <entryRelationship typeCode="COMP">
                                                   <observation classCode="DGIMG" moodCode="EVN">
                                                       <templateId root="2.16.840.1.113883.10.20.6.2.8"/>
                                                       <id root="1.2.840.113619.2.62.994044785528.20060823.200608232232322.3"/>
                                                       <code code="1.2.840.10008.5.1.4.1.1.1"codeSystem="1.2.840.10008.2.6.1"
                                                           codeSystemName="DCMUID"displayName="Computed Radiography Image Storage">
                                                       </code>
                                                       <text mediaType="application/dicom">
                                                           <reference value="http://www.example.org/wado?requestType=WADO
                                                               &amp;studyUID=1.2.840.113619.2.62.994044785528.114289542805
                                                               &amp;seriesUID=1.2.840.113619.2.62.994044785528.20060823223142485051
                                                               &amp;objectUID=1.2.840.113619.2.62.994044785528.20060823.200608232232322.3
                                                               &amp;contentType=application/dicom"/>
                                                           <!--reference to image 1 (PA) -->
                                                       </text>
                                                       <effectiveTime value="20060823223232"/>
                                                   </observation>
                                               </entryRelationship>
                                               <entryRelationship typeCode="COMP">
                                                   <observation classCode="DGIMG" moodCode="EVN">
                                                       <templateId root="2.16.840.1.113883.10.20.6.2.8"/>
                                                       <id root="1.2.840.113619.2.62.994044785528.20060823.200608232231422.3"/>
                                                       <code code="1.2.840.10008.5.1.4.1.1.1"codeSystem="1.2.840.10008.2.6.1"
                                                           codeSystemName="DCMUID"displayName="Computed Radiography Image Storage">
                                                       </code>
                                                       <text
                                                           mediaType="application/dicom">
                                                           <reference value="http://www.example.org/wado?requestType=WADO
                                                           &amp;studyUID=1.2.840.113619.2.62.994044785528.114289542805
                                                           &amp;seriesUID=1.2.840.113619.2.62.994044785528.20060823223142485051
                                                           &amp;objectUID=1.2.840.113619.2.62.994044785528.20060823.200608232231422.3
                                                           &amp;contentType=application/dicom"/>
                                                           <!--reference to image 2 (LAT) -->
                                                       </text>
                                                       <effectiveTime value="20060823223142"/>
                                                   </observation>
                                               </entryRelationship>
                                           </act>
                                       </entryRelationship>
                                   </act>
                               </entry>
                           </section>
                           <!--**************** End of DICOM Object Catalog Subsection *****************-->
                       </component>
                   </section>
                   <!--**************** End of Imaging Procedure Description Section *****************-->
               </component>
               <component>
                   <!--**************** Findings Section  *****************-->
                   <section>
                       <templateId root="2.16.840.1.113883.10.20.6.1.2"/>
                       <id root="1.2.840.10213.2.62.9940434234785528.114289545000804445"/>
                       <code code="59776-5" codeSystem="2.16.840.1.113883.6.1"codeSystemName="LOINC" displayName="Findings"/>
                       <title>Findings</title>
                       <text>
                           <paragraph>
                               <caption>Finding</caption>
                               <content ID="Fndng2">The cardiomediastinum is within normal limits. The trachea is midline.
                               The previously described opacity at the medial right lung base has cleared. There are no new
                               infiltrates. There is a new round density at the left hilus,superiorly (diameter about 45mm).
                               A CT scan is recommended for further evaluation. The pleural spaces are clear. The visualized
                               musculoskeletal structures and the upper abdomen are stable and unremarkable.</content>
                           </paragraph>
                           <paragraph>
                               <caption>Diameter</caption>
                               <content ID="Diam2">45mm</content>
                           </paragraph>
                           <paragraph>
                               <caption>Source of Measurement</caption>
                               <content ID="SrceOfMeas2">
                                   <linkHtml
                                       href="http://www.example.org/wado?requestType=WADO
                                           &amp;studyUID=1.2.840.113619.2.62.994044785528.114289542805
                                           &amp;seriesUID=1.2.840.113619.2.62.994044785528.20060823223142485051
                                           &amp;objectUID=1.2.840.113619.2.62.994044785528.20060823.200608232232322.3
                                           &amp;contentType=application/dicom">Chest_PA</linkHtml>
                               </content>
                           </paragraph>
                       </text>
                       <entry>
                           <observation classCode="OBS" moodCode="EVN">
                               <!-- Text Observation -->
                               <templateId root="2.16.840.1.113883.10.20.6.2.12"/>
                               <code code="121071" codeSystem="1.2.840.10008.2.16.4"codeSystemName="DCM" displayName="Finding"/>
                               <value xsi:type="ED">
                                   <reference value="#Fndng2"/>
                               </value>
                               <!-- inferred from measurement -->
                               <entryRelationship typeCode="SPRT">
                                   <observation classCode="OBS" moodCode="EVN">
                                       <templateId root="2.16.840.1.113883.10.20.6.2.14"/>
                                       <code code="246120007" codeSystem="2.16.840.1.113883.6.96"codeSystemName="SNOMED"
                                           displayName="Nodule size">
                                           <originalText>
                                               <reference value="#Diam2"/>
                                           </originalText>
                                       </code>
                                       <!-- no DICOM attribute <statusCode code="completed"/> -->
                                       <effectiveTime value="20060823223912"/>
                                       <value xsi:type="PQ" value="45" unit="mm"/>
                                       <!-- inferred from image -->
                                       <entryRelationship typeCode="SUBJ">
                                           <observation classCode="DGIMG" moodCode="EVN">
                                               <templateId root="2.16.840.1.113883.10.20.6.2.8"/>
                                               <!-- (0008,1155) Referenced SOP Instance UID-->
                                               <id root="1.2.840.113619.2.62.994044785528.20060823.200608232232322.3"/>
                                               <!-- (0008,1150) Referenced SOP Class UID -->
                                               <code code="1.2.840.10008.5.1.4.1.1.1"codeSystem="1.2.840.10008.2.6.1"
                                                   codeSystemName="DCMUID"displayName="Computed Radiography Image Storage">
                                               </code>
                                               <text mediaType="application/dicom">
                                                   <!--reference to CR DICOM image (PA view) -->
                                                   <reference
                                                   value="http://www.example.org/wado?requestType=WADO
                                                       &amp;studyUID=1.2.840.113619.2.62.994044785528.114289542805
                                                       &amp;seriesUID=1.2.840.113619.2.62.994044785528.20060823223142485051
                                                       &amp;objectUID=1.2.840.113619.2.62.994044785528.20060823.200608232232322.3
                                                       &amp;contentType=application/dicom"/>
                                               </text>
                                               <effectiveTime value="20060823223232"/>
                                               <!-- Purpose of Reference -->
                                               <entryRelationship typeCode="RSON">
                                                   <observation classCode="OBS" moodCode="EVN">
                                                       <templateId root="2.16.840.1.113883.10.20.6.2.9"/>
                                                       <code code="ASSERTION"codeSystem="2.16.840.1.113883.5.4"/>
                                                       <value xsi:type="CD" code="121112"codeSystem="1.2.840.10008.2.16.4"
                                                               codeSystemName="DCM"displayName="Source of Measurement">
                                                           <originalText>
                                                               <reference value="#SrceOfMeas2"
                                                               />
                                                           </originalText>
                                                       </value>
                                                   </observation>
                                               </entryRelationship>
                                           </observation>
                                       </entryRelationship>
                                   </observation>
                               </entryRelationship>
                           </observation>
                       </entry>
                   </section>
                   <!--**************** End of Findings Section *****************-->
               </component>
               <component>
                   <!--**************** Impressions Section *****************-->
                   <section>
                       <templateId root="1.2.840.10008.9.5"/>
                       <id root="1.2.840.10213.2.62.9940434234785528.114289545345927752"/>
                       <code code="19005-8" codeSystem="2.16.840.1.113883.6.1"codeSystemName="LOINC" displayName="Impressions"/>
                       <title>Impressions</title>
                       <text>
                           <paragraph>
                               <caption>Impression</caption>
                               <content ID="Fndng3">No acute cardiopulmonary process. Round density in left superior hilus, further
                               evaluation with CT is recommended as underlying malignancy is not excluded.</content>
                           </paragraph>
                       </text>
                       <entry>
                           <!-- Impression report element (TEXT) -->
                           <observation classCode="OBS" moodCode="EVN">
                               <!-- Text Observation -->
                               <templateId root="2.16.840.1.113883.10.20.6.2.12"/>
                               <code code="121073" codeSystem="1.2.840.10008.2.16.4"codeSystemName="DCM" displayName="Impression"/>
                               <value xsi:type="ED">
                                   <reference value="#Fndng3"/>
                               </value>
                           </observation>
                       </entry>
                   </section>
                   <!--**************** End of Impressions
                    Section *****************-->
               </component>
           </structuredBody>
       </component>
   </ClinicalDocument>
