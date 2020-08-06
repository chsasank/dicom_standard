.. _chapter_9:

Section-level Templates
=======================

.. _sect_9.1:

General Requirements For Sections
---------------------------------

.. _sect_9.1.1:

Section Text
~~~~~~~~~~~~

+----------------------+----------------------------------------------+
| **Template ID**      | 1.2.840.10008.9.19                           |
+----------------------+----------------------------------------------+
| **Name**             | Section Text                                 |
+----------------------+----------------------------------------------+
| **Effective Date**   | 2015/03/24                                   |
+----------------------+----------------------------------------------+
| **Version Label**    | DICOM-20150324                               |
+----------------------+----------------------------------------------+
| **Status**           | Active                                       |
+----------------------+----------------------------------------------+
| **Description**      | This template specifies the common set of    |
|                      | narrative block markup that may be included  |
|                      | in a CDA imaging report section.             |
+----------------------+----------------------------------------------+
| **Classification**   | CDA Element Set                              |
+----------------------+----------------------------------------------+
| **Relationships**    | Included in all sections                     |
+----------------------+----------------------------------------------+
| **Context**          | parent node                                  |
+----------------------+----------------------------------------------+
| **Open/Closed**      | Open                                         |
+----------------------+----------------------------------------------+
| **Revision History** | DICOM-20150324: Initial version              |
+----------------------+----------------------------------------------+

+-------+-------+-------+-------+-------+-------+-------+-------+-------+
| **Bus | *     | **    | **C   | *     | *     | **    | **Va  | **    |
| iness | *Nest | Eleme | ard** | *Elem | *Data | Value | lue** | Subsi |
| N     | Le    | nt/​A |       | /Attr | T     | C     |       | diary |
| ame** | vel** | ttrib |       | C     | ype** | onf** |       | Templ |
|       |       | ute** |       | onf** |       |       |       | ate** |
+-------+-------+-------+-------+-------+-------+-------+-------+-------+
| Text  |       | text  | 1..1  | COND  | ED    |       |       |       |
+-------+-------+-------+-------+-------+-------+-------+-------+-------+
| **Co  | >     | co    | 0..\* | MAY   | ST    |       |       |       |
| ntent |       | ntent |       |       |       |       |       |       |
| [*]** |       |       |       |       |       |       |       |       |
+-------+-------+-------+-------+-------+-------+-------+-------+-------+
| *     | >@    | @ID   | 1..1  | SHALL | XML   |       | [See  |       |
| *\*** |       |       |       |       | ID    |       | `XML  |       |
|       |       |       |       |       |       |       | ID <# |       |
|       |       |       |       |       |       |       | sect_ |       |
|       |       |       |       |       |       |       | 5.3.4 |       |
|       |       |       |       |       |       |       | >`__] |       |
+-------+-------+-------+-------+-------+-------+-------+-------+-------+
| Style | >@    | @styl | 0..1  | MAY   | XML   |       |       |       |
|       |       | eCode |       |       | NMT   |       |       |       |
|       |       |       |       |       | OKENS |       |       |       |
+-------+-------+-------+-------+-------+-------+-------+-------+-------+
| Int​R | >     | link  | 0..\* | MAY   | ST    |       |       |       |
| ef[*] |       | ​Html |       |       |       |       |       |       |
+-------+-------+-------+-------+-------+-------+-------+-------+-------+
|       | >@    | @href | 1..1  | SHALL | ST    |       |       |       |
|       |       |       |       |       | (URL  |       |       |       |
|       |       |       |       |       | - XML |       |       |       |
|       |       |       |       |       | I     |       |       |       |
|       |       |       |       |       | DREF) |       |       |       |
+-------+-------+-------+-------+-------+-------+-------+-------+-------+
| **G   | >     | ren   | 0..\* | MAY   |       |       |       |       |
| raphi |       | der​M |       |       |       |       |       |       |
| c​Ref |       | ulti​ |       |       |       |       |       |       |
| [*]** |       | Media |       |       |       |       |       |       |
+-------+-------+-------+-------+-------+-------+-------+-------+-------+
|       | >@    | @r    | 1..1  | SHALL | XML   |       |       |       |
|       |       | efere |       |       | IDREF |       |       |       |
|       |       | ncedO |       |       |       |       |       |       |
|       |       | bject |       |       |       |       |       |       |
+-------+-------+-------+-------+-------+-------+-------+-------+-------+
| Ca    | >>    | ca    | 0..1  | MAY   | ST    |       |       |       |
| ption |       | ption |       |       |       |       |       |       |
+-------+-------+-------+-------+-------+-------+-------+-------+-------+
| **Ex  | >     | link  | 0..\* | MAY   | ST    |       |       |       |
| t​Ref |       | ​Html |       |       |       |       |       |       |
| [*]** |       |       |       |       |       |       |       |       |
+-------+-------+-------+-------+-------+-------+-------+-------+-------+
| URL   | >@    | @href | 1..1  | SHALL | ST    |       |       |       |
|       |       |       |       |       | (URL) |       |       |       |
+-------+-------+-------+-------+-------+-------+-------+-------+-------+
| *     | >     | para  | 0..\* | MAY   | ST    |       |       |       |
| *Para |       | graph |       |       |       |       |       |       |
| graph |       |       |       |       |       |       |       |       |
| (*)** |       |       |       |       |       |       |       |       |
+-------+-------+-------+-------+-------+-------+-------+-------+-------+
| Ca    | >>    | ca    | 0..1  | MAY   | ST    |       |       |       |
| ption |       | ption |       |       |       |       |       |       |
+-------+-------+-------+-------+-------+-------+-------+-------+-------+
| *     | >     | list  | 0..\* | MAY   | ST    |       |       |       |
| *List |       |       |       |       |       |       |       |       |
| (*)** |       |       |       |       |       |       |       |       |
+-------+-------+-------+-------+-------+-------+-------+-------+-------+
| *     | >@    | @ID   | 1..1  | SHALL | XML   |       | [See  |       |
| *\*** |       |       |       |       | ID    |       | `XML  |       |
|       |       |       |       |       |       |       | ID <# |       |
|       |       |       |       |       |       |       | sect_ |       |
|       |       |       |       |       |       |       | 5.3.4 |       |
|       |       |       |       |       |       |       | >`__] |       |
+-------+-------+-------+-------+-------+-------+-------+-------+-------+
| Or    | >@    | @lis  | 0..1  | MAY   | XML   | SHALL | or    |       |
| dered |       | tType |       |       | NMT   |       | dered |       |
|       |       |       |       |       | OKENS |       |       |       |
+-------+-------+-------+-------+-------+-------+-------+-------+-------+
| Ca    | >>    | ca    | 0..1  | MAY   | ST    |       |       |       |
| ption |       | ption |       |       |       |       |       |       |
+-------+-------+-------+-------+-------+-------+-------+-------+-------+
| It    | >>    | item  | 1..\* | SHALL | ST    |       |       |       |
| em(*) |       |       |       |       |       |       |       |       |
+-------+-------+-------+-------+-------+-------+-------+-------+-------+
| \*    | >>@   | @ID   | 1..1  | SHALL | XML   |       | [See  |       |
|       |       |       |       |       | ID    |       | `XML  |       |
|       |       |       |       |       |       |       | ID <# |       |
|       |       |       |       |       |       |       | sect_ |       |
|       |       |       |       |       |       |       | 5.3.4 |       |
|       |       |       |       |       |       |       | >`__] |       |
+-------+-------+-------+-------+-------+-------+-------+-------+-------+
| **    | >     | table | 1..1  | SHALL |       |       |       |       |
| Table |       |       |       |       |       |       |       |       |
| (*)** |       |       |       |       |       |       |       |       |
+-------+-------+-------+-------+-------+-------+-------+-------+-------+
| *     | >@    | @ID   | 1..1  | SHALL | XML   |       | [See  |       |
| *\*** |       |       |       |       | ID    |       | `XML  |       |
|       |       |       |       |       |       |       | ID <# |       |
|       |       |       |       |       |       |       | sect_ |       |
|       |       |       |       |       |       |       | 5.3.4 |       |
|       |       |       |       |       |       |       | >`__] |       |
+-------+-------+-------+-------+-------+-------+-------+-------+-------+
| Ca    | >>    | ca    | 0..1  | MAY   | ST    |       |       |       |
| ption |       | ption |       |       |       |       |       |       |
+-------+-------+-------+-------+-------+-------+-------+-------+-------+
|       | >>    | Tr    | 1..1  | SHALL |       |       |       |       |
+-------+-------+-------+-------+-------+-------+-------+-------+-------+
|       | >>@   | @styl | 1..1  | SHALL | CS    | SHALL | Bold  |       |
|       |       | eCode |       |       |       |       |       |       |
+-------+-------+-------+-------+-------+-------+-------+-------+-------+
| Colu  | >>>   | Th    | 1..\* | SHALL | ST    |       |       |       |
| mn​He |       |       |       |       |       |       |       |       |
| ad(*) |       |       |       |       |       |       |       |       |
+-------+-------+-------+-------+-------+-------+-------+-------+-------+
| **Row | >>    | Tr    | 1..\* | SHALL |       |       |       |       |
| [*]** |       |       |       |       |       |       |       |       |
+-------+-------+-------+-------+-------+-------+-------+-------+-------+
| *     | >>@   | @ID   | 1..1  | SHALL | XML   |       |       |       |
| *\*** |       |       |       |       | ID    |       |       |       |
+-------+-------+-------+-------+-------+-------+-------+-------+-------+
| Ce    | >>>   | Td    | 1..1  | SHALL | ST    |       |       |       |
| ll(*) |       |       |       |       |       |       |       |       |
+-------+-------+-------+-------+-------+-------+-------+-------+-------+

The text element within the section stores the narrative to be rendered,
as described in the CDA R2 specification, and is referred to as the CDA
narrative block.

COND: The text element SHALL be present if the section content is not
completely represented by subsections.

As noted in the CDA R2 specification, the document originator is
responsible for ensuring that the narrative block contains the complete,
human readable, attested content of the section. Structured entries
support computer processing and computation, and are not a replacement
for the attestable, human-readable content of the CDA narrative block.

Additional specification information for the CDA narrative block can be
found in the CDA R2 specification in sections 1.2.1, 1.2.3, 1.3, 1.3.1,
1.3.2, 4.3.4.2, and 6.

The narrative block allows a variety of markup. The markup that
implements various types of internal and external linkage is shown in
the table, and is included in the conformance specifications for each
section narrative block that invokes this template. The markup elements
may occur in any order and at any point within the narrative block text
as allowed by the CDA R2 specification.

.. _sect_9.1.1.1:

<content> Markup and Links From Entries
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

The CDA narrative block may contain the <content> markup element to wrap
a block of text so that it can be explicitly identified using its XML ID
attribute, and referenced from elsewhere in the document. Specifically,
structured entries may link to their equivalent narrative rendering in a
content block using the XML ID (see CDA R2 Specification, section
4.3.5.1).

Additionally, a content block may include a styleCode attribute to
suggest rendering (see CDA R2 Specification, section 4.3.5.11). For
example, Bold could also be used to highlight actionable findings in the
text of the `Findings <#sect_9.5>`__ and/or `Impression <#sect_9.6>`__
sections.

.. _sect_9.1.1.2:

<linkHtml> Markup and Internal References
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

The CDA narrative block MAY contain the <linkHtml> markup to provide a
link between narrative text in one section and a content block in
another section (see CDA R2 specification section 4.3.5.2). The XML ID
of the target content block is used in the linkHtml href attribute, with
a prefixed '#' to indicate the reference is in the current document.

For example, a linkHtml reference could be used to link an actionable
finding in the `Impression <#sect_9.6>`__ section to the specific,
detailed measurement evidencing a problem that was identified in the
text of the `Findings <#sect_9.5>`__ section.

.. _sect_9.1.1.3:

<renderMultiMedia> Markup and Graphical Content
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

The CDA narrative block MAY contain the <renderMultiMedia> markup
element to include graphical content, e.g., a coronary tree diagram or
myocardial wall motion "bulls-eye chart". The renderMultiMedia element
SHALL link to an observationMedia structured entry using the XML ID of
that entry (see CDA R2 Specification, section 4.3.5.6).

.. _sect_9.1.1.4:

<linkHtml> Markup and External References
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

The CDA narrative block MAY contain the <linkHtml> markup to provide a
link between narrative text and an external (non-attested) resource (see
CDA R2 specification section 4.3.5.2).

.. note::

   For radiology reports, this capability may be used to tag concepts in
   the narrative block to concepts defined in the RadLex terminology
   (http://www.radlex.org), developed by the Radiological Society of
   North America. The RadLex coded vocabulary is a useful tool for
   indexing report content for data mining purposes. It is not intended
   to be a complete grammar for expression of clinical statements, but
   rather a lexicon for tagging concepts of interest.

Within the report section narrative blocks, RadLex codes may be included
using the <linkHtml> element and a URI pointing to the RadLex resource.
<linkHtml> elements may be embedded in the text at the location of the
concept (within the scope of a content tag), or may be provided in a
list at the end of the narrative block.

::

   <section>
       ...
       <text>
           ...
           <content ID="find1">There is focal opacity
               <linkHtml href="http://www.radlex.org/RID/RID28530"/>
               at the right lung
               <linkHtml href="http://www.radlex.org/RID/RID1302"/>
               base most likely representing right lower lobe atelectasis
               <linkHtml href="http://www.radlex.org/RID/RID28493"/>.
           </content>
           <content ID="find2">The mediastinum ...</content>
       </text>
       ...
   </section>

::

   <section>
       <title>Findings</title>
       <text>
           <content ID="find1">Pleura normal... </content>
           <linkHtml href="http://www.radlex.org/RID/RID1362"/>
       </text>
   </section>

.. _sect_9.1.1.5:

<linkHtml> Markup and Image References
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

The text elements (and their children) MAY contain Web Access to DICOM
Persistent Object (WADO) references to DICOM objects by including a
linkHtml element where @href is a valid WADO URL. The text content of
linkHtml MAY be either the visible text of the hyperlink, or a
descriptor or identifier of the image.

The linkHtml may be associated with a <renderMultiMedia> markup element
to specify a (limited resolution) copy of the image to be rendered in
the narrative (e.g., a thumbnail); the renderMultiMedia element SHALL
link to an observationMedia structured entry using the XML ID of that
entry. As CDA does not allow use of an image as the linkHtml displayable
hyper-linked content, the linkHtml should immediately follow the
renderMultiMedia for the thumbnail.

::

   <text>
       ...
       <paragraph>
           <caption>Source of Measurement</caption>
           <renderMultiMedia referencedObject="#thumb1"/>
           <linkHtml href="http://www.example.org/wado?requestType=WADO
               &amp;studyUID=1.2.840.113619.2.62.994044785528.114289542805
               &amp;seriesUID=1.2.840.113619.2.62.994044785528.20060823223142485051
               &amp;objectUID=1.2.840.113619.2.62.994044785528.20060823.200608232232322.3
               &amp;contentType=application/dicom">Chest_PA</linkHtml>
       </paragraph>
       ...
   </text>

.. _sect_9.1.1.6:

list
^^^^

This template specifies a structure and Business Names for list markup
in the narrative text, as described in the CDA Specification section
4.3.5.8. Inclusion of the listType="ordered" attribute specifies a
numbered list of items.

Each list is identified by an XML ID attribute, and each list item also
is identified by an XML ID attribute.

The list items contain human readable displayable text using any of the
narrative text structures permitted in section/text, including internal,
external, or image references, or graphics. Processable structured data
may be encoded in `Coded Observation <#sect_10.1>`__ or `Quantity
Measurement <#sect_10.5>`__ entries in the *section*. Such observation
entries SHOULD be linked to the corresponding item through the ID
attribute of the item (see `text/reference and Related Narrative Block
Markup <#sect_10.1.2>`__ and `text/reference and Related Narrative Block
Markup <#sect_10.5.1>`__).

.. _sect_9.1.1.7:

table
^^^^^

This template specifies a structure and Business Names for table markup
in the narrative text, as described in the CDA Specification section
4.3.5.9, typically used for a table of measurements. The table may be of
arbitrary size.

.. note::

   See Travis, A., et al., "Preferences for Structured Reporting of
   Measurement Data", *JAcadRadiology* 21:6
   DOI:10.1016/j.acra.2014.02.008

Each table is identified by an XML ID attribute, and each table row also
is identified by an XML ID attribute.

The table cells contain human readable displayable text using any of the
narrative text structures permitted in section/text, including internal,
external, or image references, or graphics. Processable structured data
may be encoded in `Coded Observation <#sect_10.1>`__ or `Quantity
Measurement <#sect_10.5>`__ entries in the *section*. Such observation
entries SHOULD be linked to the corresponding row through the ID
attribute of the row (see `text/reference and Related Narrative Block
Markup <#sect_10.1.2>`__ and `text/reference and Related Narrative Block
Markup <#sect_10.5.1>`__).

As displayed

.. table:: Cardiac Measurements

   =================================== ====== =======
   Measurement name                    Value  Flag
   =================================== ====== =======
   Left ventricular ejection fraction  40 %   **LOW**
   Left ventricle end diastolic volume 120 ml 
   Left ventricle end systolic volume  72 ml  
   =================================== ====== =======

As encoded in CDA instance

::

   <text>
       <table ID="T-C">
           <caption>Cardiac Measurements</caption>
           <tr styleCode="Bold">
               <th>Measurement name</th>
               <th>Value</th>
               <th>Flag</th>
           </tr>
           <tr ID="Q1">
               <td>Left ventricular ejection fraction</td>
               <td>40 %</td>
               <td styleCode="Bold">LOW</td>
           </tr>
           <tr ID="Q2">
               <td>Left ventricle end diastolic volume</td>
               <td>120 ml</td>
           </tr>
           <tr ID="Q3">
               <td>Left ventricle end systolic volume</td>
               <td>72 ml</td>
           </tr>
       </table>
   </text>
   <entry>
       <observation classCode="OBS" moodCode="EVN">
           <templateId root="2.16.840.1.113883.10.20.6.2.14"/>
           <id root="1.2.840.10213.2.62.7044234.11652014"/>
           <code code="10230-1" codeSystem="2.16.840.1.113883.6.1"
               codeSystemName="LOINC" displayName="LVEF" />
           <text><reference value="#Q1"/></text>
           <statusCode code="completed"/>
           <effectiveTime value="20140913223912"/>
           <value xsi:type="PQ" unit="%" value="40" />
           <interpretationCode code="L" codeSystem="2.16.840.1.113883.6.83"
               codeSystemName="ObservationInterpretation" displayName="Low" />
       </observation>
   </entry>
   <entry>
       <observation classCode="OBS" moodCode="EVN">
           <templateId root="2.16.840.1.113883.10.20.6.2.14"/>
           <id root="1.2.840.10213.2.62.7044234.11652014"/>
           <code code="8821-1" codeSystem="2.16.840.1.113883.6.1"
               codeSystemName="LOINC" displayName="LVEDV" />
           <text><reference value="#Q2"/></text>
           <statusCode code="completed"/>
           <effectiveTime value="20140913223912"/>
           <value xsi:type="PQ" unit="ml" value="120" />
       </observation>
   </entry>
   <entry>
       <observation classCode="OBS" moodCode="EVN">
           <templateId root="2.16.840.1.113883.10.20.6.2.14"/>
           <id root="1.2.840.10213.2.62.7044234.11652014"/>
           <code code="8823-7" codeSystem="2.16.840.1.113883.6.1"
               codeSystemName="LOINC" displayName="LVESV" />
           <text><reference value="#Q3"/></text>
           <statusCode code="completed"/>
           <effectiveTime value="20140913223912"/>
           <value xsi:type="PQ" unit="ml" value="72" />
       </observation>
   </entry>

As displayed

.. table:: Current Lesion Sizes with Comparison to Exam on 2014/11/16

   +-----+---------------+---------------+-------------+---------------+
   | Ref | Measurement   | Current Value | Prior Value | Image         |
   |     | name          |               |             | Reference     |
   +=====+===============+===============+=============+===============+
   | L1  | Left          | 12 x 8        | 15 x 10     | Ser:3, Img:67 |
   |     | periaortic    |               |             |               |
   |     | lymph node    |               |             |               |
   |     | size (mm)     |               |             |               |
   +-----+---------------+---------------+-------------+---------------+
   | L2  | Segment 2     | 6 x 8         | 10 x 9      | Ser:3, Img:79 |
   |     | left lobe     |               |             |               |
   |     | lesion size   |               |             |               |
   |     | (mm)          |               |             |               |
   +-----+---------------+---------------+-------------+---------------+
   | L3  | Left common   | 12 x 3        | 16 x 5      | Ser:3,        |
   |     | iliac lymph   |               |             | Img:139       |
   |     | node size     |               |             |               |
   |     | (mm)          |               |             |               |
   +-----+---------------+---------------+-------------+---------------+

As encoded in CDA instance

::

   <text>
       <table ID="Table2">
           <caption>Current Lesion Sizes with Comparison to Exam on 2014/11/16</caption>
           <tr styleCode="Bold">
               <td>Ref</td>
               <td>Measurement name</td>
               <td>Current Value</td>
               <td>Prior Value</td>
               <td>Image Reference</td>
           </tr>
           <tr ID="lesRow1">
               <td>L1</td>
               <td>Left periaortic lymph node size (mm) </td>
               <td>12 x 8</td>
               <td>15 x 10</td>
               <td><linkHtml href="http://wado.pacs.guh.org/..." >Ser:3, Img:67</linkHtml></td>
           </tr>
           ...
       </table>
   </text>

.. _sect_9.1.2:

General Section Entries
~~~~~~~~~~~~~~~~~~~~~~~

+----------------------+----------------------------------------------+
| **Template ID**      | 1.2.840.10008.9.23                           |
+----------------------+----------------------------------------------+
| **Name**             | General Section Entries                      |
+----------------------+----------------------------------------------+
| **Effective Date**   | 2015/03/24                                   |
+----------------------+----------------------------------------------+
| **Version Label**    | DICOM-20150324                               |
+----------------------+----------------------------------------------+
| **Status**           | Active                                       |
+----------------------+----------------------------------------------+
| **Description**      | This template specifies the common set of    |
|                      | structured entries that may be included in a |
|                      | CDA imaging report section, and an author    |
|                      | participation for the section.               |
+----------------------+----------------------------------------------+
| **Classification**   | CDA Element Set                              |
+----------------------+----------------------------------------------+
| **Relationships**    | Included in `Findings <#sect_9.5>`__ section |
|                      | and its sub-sections, `Clinical              |
|                      | Information <#sect_9.2>`__ and other         |
|                      | sections                                     |
+----------------------+----------------------------------------------+
| **Context**          | sibling node                                 |
+----------------------+----------------------------------------------+
| **Open/Closed**      | open                                         |
+----------------------+----------------------------------------------+
| **Revision History** | DICOM-20150324: Initial version              |
+----------------------+----------------------------------------------+

+-------+-------+-------+-------+-------+-------+-------+-------+-------+
| **Bus | *     | **    | **C   | *     | *     | **    | **Va  | **    |
| iness | *Nest | Eleme | ard** | *Elem | *Data | Value | lue** | Subsi |
| N     | Le    | nt/​A |       | /Attr | T     | C     |       | diary |
| ame** | vel** | ttrib |       | C     | ype** | onf** |       | Templ |
|       |       | ute** |       | onf** |       |       |       | ate** |
+-------+-------+-------+-------+-------+-------+-------+-------+-------+
| C     |       | t     | 0..1  | MAY   | II    |       |       |       |
| onten |       | empla |       |       |       |       |       |       |
| t​Tem |       | te​Id |       |       |       |       |       |       |
| plate |       |       |       |       |       |       |       |       |
+-------+-------+-------+-------+-------+-------+-------+-------+-------+
|       |       | a     | 0..\* | MAY   |       |       |       |       |
|       |       | uthor |       |       |       |       |       |       |
+-------+-------+-------+-------+-------+-------+-------+-------+-------+
| Auth  | >     | time  | 1..1  | SHALL | TS    |       |       |       |
| oring |       |       |       |       |       |       |       |       |
| ​Time |       |       |       |       |       |       |       |       |
+-------+-------+-------+-------+-------+-------+-------+-------+-------+
|       | >     | assig | 1..1  | SHALL |       |       |       |       |
|       |       | ned​A |       |       |       |       |       |       |
|       |       | uthor |       |       |       |       |       |       |
+-------+-------+-------+-------+-------+-------+-------+-------+-------+
| Auth  | >>    | id    | 1.\*  | SHALL | II    |       |       |       |
| or​ID |       |       |       |       |       |       |       |       |
+-------+-------+-------+-------+-------+-------+-------+-------+-------+
|       | >>    | assig | 1..1  | COND  |       |       |       |       |
|       |       | ned​P |       |       |       |       |       |       |
|       |       | erson |       |       |       |       |       |       |
+-------+-------+-------+-------+-------+-------+-------+-------+-------+
| A     | >>>   | name  | 1..1  | SHALL | PN    |       |       |       |
| uthor |       |       |       |       |       |       |       |       |
| ​Name |       |       |       |       |       |       |       |       |
+-------+-------+-------+-------+-------+-------+-------+-------+-------+
|       | >>    | assig | 1..1  | COND  |       |       |       |       |
|       |       | ned​A |       |       |       |       |       |       |
|       |       | uthor |       |       |       |       |       |       |
|       |       | ing​D |       |       |       |       |       |       |
|       |       | evice |       |       |       |       |       |       |
+-------+-------+-------+-------+-------+-------+-------+-------+-------+
| Auth  | >>>   | man   | 0..1  | S     | ST    |       |       |       |
| or​De |       | ufact |       | HOULD |       |       |       |       |
| vice​ |       | urer​ |       |       |       |       |       |       |
| Model |       | Model |       |       |       |       |       |       |
|       |       | ​Name |       |       |       |       |       |       |
+-------+-------+-------+-------+-------+-------+-------+-------+-------+
| Autho | >>>   | sof   | 0..1  | S     | ST    |       |       |       |
| r​Sof |       | tware |       | HOULD |       |       |       |       |
| tware |       | ​Name |       |       |       |       |       |       |
+-------+-------+-------+-------+-------+-------+-------+-------+-------+
|       | >>    | repr  | 0..1  | MAY   |       |       |       |       |
|       |       | esent |       |       |       |       |       |       |
|       |       | ed​Or |       |       |       |       |       |       |
|       |       | ganiz |       |       |       |       |       |       |
|       |       | ation |       |       |       |       |       |       |
+-------+-------+-------+-------+-------+-------+-------+-------+-------+
| Auth  | >>>   | name  | 0..1  | S     | ON    |       |       |       |
| or​Or |       |       |       | HOULD |       |       |       |       |
| ganiz |       |       |       |       |       |       |       |       |
| ation |       |       |       |       |       |       |       |       |
+-------+-------+-------+-------+-------+-------+-------+-------+-------+
|       |       | entry | 0..\* | MAY   |       |       |       |       |
+-------+-------+-------+-------+-------+-------+-------+-------+-------+
| *C    | >     | *ob   | 1..1  | SHALL |       |       |       | `     |
| oded​ |       | serva |       |       |       |       |       | Coded |
| Obser |       | tion* |       |       |       |       |       | Ob    |
| vatio |       |       |       |       |       |       |       | serva |
| n[*]* |       |       |       |       |       |       |       | tion  |
|       |       |       |       |       |       |       |       | <#sec |
|       |       |       |       |       |       |       |       | t_10. |
|       |       |       |       |       |       |       |       | 1>`__ |
|       |       |       |       |       |       |       |       | 2     |
|       |       |       |       |       |       |       |       | .16.8 |
|       |       |       |       |       |       |       |       | 40.1. |
|       |       |       |       |       |       |       |       | 11388 |
|       |       |       |       |       |       |       |       | 3.​10 |
|       |       |       |       |       |       |       |       | .20.6 |
|       |       |       |       |       |       |       |       | .2.13 |
+-------+-------+-------+-------+-------+-------+-------+-------+-------+
|       |       | entry | 0..\* | MAY   |       |       |       |       |
+-------+-------+-------+-------+-------+-------+-------+-------+-------+
| *Quan | >     | *ob   | 1..1  | SHALL |       |       |       | `Qua  |
| tity​ |       | serva |       |       |       |       |       | ntity |
| Measu |       | tion* |       |       |       |       |       | Me    |
| remen |       |       |       |       |       |       |       | asure |
| t[*]* |       |       |       |       |       |       |       | ment  |
|       |       |       |       |       |       |       |       | <#sec |
|       |       |       |       |       |       |       |       | t_10. |
|       |       |       |       |       |       |       |       | 5>`__ |
|       |       |       |       |       |       |       |       | 2     |
|       |       |       |       |       |       |       |       | .16.8 |
|       |       |       |       |       |       |       |       | 40.1. |
|       |       |       |       |       |       |       |       | 11388 |
|       |       |       |       |       |       |       |       | 3.​10 |
|       |       |       |       |       |       |       |       | .20.6 |
|       |       |       |       |       |       |       |       | .2.14 |
+-------+-------+-------+-------+-------+-------+-------+-------+-------+
|       |       | entry | 0..\* | MAY   |       |       |       |       |
+-------+-------+-------+-------+-------+-------+-------+-------+-------+
| *G    | >     | *obs  | 1..1  | SHALL |       |       |       | `ob   |
| raphi |       | ervat |       |       |       |       |       | serva |
| c[*]* |       | ion​M |       |       |       |       |       | tionM |
|       |       | edia* |       |       |       |       |       | edia  |
|       |       |       |       |       |       |       |       | <#sec |
|       |       |       |       |       |       |       |       | t_10. |
|       |       |       |       |       |       |       |       | 3>`__ |
|       |       |       |       |       |       |       |       | 1.3   |
|       |       |       |       |       |       |       |       | .6.1. |
|       |       |       |       |       |       |       |       | 4.1.1 |
|       |       |       |       |       |       |       |       | 9376. |
|       |       |       |       |       |       |       |       | ​1.4. |
|       |       |       |       |       |       |       |       | 1.4.7 |
+-------+-------+-------+-------+-------+-------+-------+-------+-------+
|       |       | entry | 0..\* | MAY   |       |       |       |       |
+-------+-------+-------+-------+-------+-------+-------+-------+-------+
| *     | >     | *ob   | 1..1  | SHALL |       |       |       | `SOP  |
| SOPIn |       | serva |       |       |       |       |       | Ins   |
| stanc |       | tion* |       |       |       |       |       | tance |
| e[*]* |       |       |       |       |       |       |       | Ob    |
|       |       |       |       |       |       |       |       | serva |
|       |       |       |       |       |       |       |       | tion  |
|       |       |       |       |       |       |       |       | <#sec |
|       |       |       |       |       |       |       |       | t_10. |
|       |       |       |       |       |       |       |       | 8>`__ |
|       |       |       |       |       |       |       |       | 1.2   |
|       |       |       |       |       |       |       |       | .840. |
|       |       |       |       |       |       |       |       | 10008 |
|       |       |       |       |       |       |       |       | .9.18 |
+-------+-------+-------+-------+-------+-------+-------+-------+-------+
|       |       | entry | 0..\* | MAY   |       |       |       |       |
+-------+-------+-------+-------+-------+-------+-------+-------+-------+
|       | >     | reg   | 0..0  | SHALL |       |       |       |       |
|       |       | ion​O |       | NOT   |       |       |       |       |
|       |       | f​Int |       |       |       |       |       |       |
|       |       | erest |       |       |       |       |       |       |
+-------+-------+-------+-------+-------+-------+-------+-------+-------+

Note that there is no business name associated with this template.
Rather, this template is an editorial convenience for template
specification, and the Business Names for the elements of this template
are logically part of the Business Name scope of the invoking template.

Also, the ID of this template is not represented in a templateID
element. Rather, the templateID of the invoking template implicitly
includes the elements specified by this template.

.. _sect_9.1.2.1:

templateId
^^^^^^^^^^

This templateId may be used to identify the template(s) used to
generate/constrain the content of the section. This is in addition to
the templateId of the section level template, and typically represents
clinical sub-specialty requirements. See `Template IDs and
Version <#sect_5.1.1>`__ on the structure and use of the templateId.

.. _sect_9.1.2.2:

author
^^^^^^

The author participation allows the recording of an author for a
section, equivalent to the . Either a person or a device may be
identified as the author for a section or subsection.

COND: Either the assignedPerson or assignedAuthoringDevice element SHALL
be present.

::

   <author>
       <assignedAuthor>
           <id extension="121008" root="2.16.840.1.113883.19.5"/>
           <assignedPerson>
               <name>
                   <given>John</given>
                   <family>Blitz</family>
                   <suffix>MD</suffix>
               </name>
           </assignedPerson>
       </assignedAuthor>
   </author>

.. _sect_9.1.2.3:

section/entry
^^^^^^^^^^^^^

A section may contain CDA entries that represent clinical statements in
coded form (using the `Coded Observation <#sect_10.1>`__ template),
numeric measurements (using the `Quantity Measurement <#sect_10.5>`__
template), images to be displayed in the narrative block (using the
`observationMedia <#sect_10.3>`__ template, and invoked from a
renderMultiMedia element), or references to external images or annotated
images (using the `SOP Instance Observation <#sect_10.8>`__ template).

These entries may appear in any order.

.. _sect_9.1.2.4:

regionOfInterest
^^^^^^^^^^^^^^^^

Section templates defined in this Implementation guide SHALL NOT use the
CDA Region of Interest Overlay entry (classCode="ROIOVL"). If it is
desired to show images with graphical annotations, the annotations
SHOULD be encoded in DICOM Presentation State objects that reference the
image. Report applications that display referenced images and annotation
may retrieve a rendered image using a WADO reference in accordance with
PS3.18, including the image and Presentation State, or other DICOM
retrieval and rendering methods. This approach avoids the risks of
errors in registering a CDA region of interest annotation with DICOM
images, and places all image rendering within the scope of the DICOM
Standard, including the full range of 2D and 3D presentations defined in
DICOM.

.. _sect_9.2:

Clinical Information
--------------------

+----------------------+----------------------------------------------+
| **Template ID**      | 1.2.840.10008.9.2                            |
+----------------------+----------------------------------------------+
| **Name**             | Clinical Information                         |
+----------------------+----------------------------------------------+
| **Effective Date**   | 2015/03/24                                   |
+----------------------+----------------------------------------------+
| **Version Label**    | DICOM-20150324                               |
+----------------------+----------------------------------------------+
| **Status**           | Active                                       |
+----------------------+----------------------------------------------+
| **Description**      | Clinical details about the case such as      |
|                      | presenting signs and symptoms, past clinical |
|                      | history, the overall condition of the        |
|                      | patient, etc.                                |
+----------------------+----------------------------------------------+
| **Classification**   | CDA Section Level                            |
+----------------------+----------------------------------------------+
| **Relationships**    | Included in `Imaging Report <#sect_7.1>`__   |
+----------------------+----------------------------------------------+
| **Context**          | parent node                                  |
+----------------------+----------------------------------------------+
| **Open/Closed**      | Open                                         |
+----------------------+----------------------------------------------+
| **Revision History** | DICOM-20150324: Initial version              |
+----------------------+----------------------------------------------+

+-------+-------+-------+------+-------+-------+-------+-------+-------+
| Bus   | Nest  | Ele   | Card | Elem  | Data  | Value | Value | Subsi |
| iness | Level | ment/ |      | /Attr | Type  | Conf  |       | diary |
| Name  |       | ​Attr |      | Conf  |       |       |       | Tem   |
|       |       | ibute |      |       |       |       |       | plate |
+=======+=======+=======+======+=======+=======+=======+=======+=======+
| **Cl  |       | se    | 1..1 | SHALL |       |       |       |       |
| inica |       | ction |      |       |       |       |       |       |
| l​Inf |       |       |      |       |       |       |       |       |
| ormat |       |       |      |       |       |       |       |       |
| ion** |       |       |      |       |       |       |       |       |
+-------+-------+-------+------+-------+-------+-------+-------+-------+
|       | >     | t     | 1..1 | SHALL | II    |       |       |       |
|       |       | empla |      |       |       |       |       |       |
|       |       | te​Id |      |       |       |       |       |       |
+-------+-------+-------+------+-------+-------+-------+-------+-------+
|       | >@    | @root | 1..1 | SHALL | UID   | SHALL | 1.    |       |
|       |       |       |      |       |       |       | 2.840 |       |
|       |       |       |      |       |       |       | .1000 |       |
|       |       |       |      |       |       |       | 8.9.2 |       |
+-------+-------+-------+------+-------+-------+-------+-------+-------+
|       | >     | id    | 1..1 | SHALL | II    |       |       |       |
+-------+-------+-------+------+-------+-------+-------+-------+-------+
|       | >     | code  | 1..1 | SHALL | CD    | SHALL | `(557 |       |
|       |       |       |      |       |       |       | 52-0, |       |
|       |       |       |      |       |       |       | L     |       |
|       |       |       |      |       |       |       | OINC, |       |
|       |       |       |      |       |       |       | "Cli  |       |
|       |       |       |      |       |       |       | nical |       |
|       |       |       |      |       |       |       | Info  |       |
|       |       |       |      |       |       |       | rmati |       |
|       |       |       |      |       |       |       | on")  |       |
|       |       |       |      |       |       |       | <http |       |
|       |       |       |      |       |       |       | ://lo |       |
|       |       |       |      |       |       |       | inc.o |       |
|       |       |       |      |       |       |       | rg/55 |       |
|       |       |       |      |       |       |       | 752-0 |       |
|       |       |       |      |       |       |       | />`__ |       |
+-------+-------+-------+------+-------+-------+-------+-------+-------+
| Title | >     | title | 1..1 | SHALL | ST    |       |       |       |
+-------+-------+-------+------+-------+-------+-------+-------+-------+
| *     | *>*   | *     | 1..1 | COND  | ED    |       |       | `Se   |
| Text* |       | text* |      |       |       |       |       | ction |
|       |       |       |      |       |       |       |       | T     |
|       |       |       |      |       |       |       |       | ext < |
|       |       |       |      |       |       |       |       | #sect |
|       |       |       |      |       |       |       |       | _9.1. |
|       |       |       |      |       |       |       |       | 1>`__ |
|       |       |       |      |       |       |       |       | 1.2   |
|       |       |       |      |       |       |       |       | .840. |
|       |       |       |      |       |       |       |       | 10008 |
|       |       |       |      |       |       |       |       | .9.19 |
+-------+-------+-------+------+-------+-------+-------+-------+-------+
|       | >     | comp  | 0..1 | MAY   |       |       |       |       |
|       |       | onent |      |       |       |       |       |       |
+-------+-------+-------+------+-------+-------+-------+-------+-------+
| *Req  | >>    | *sec  | 1..1 | SHALL |       |       |       | `Requ |
| uest* |       | tion* |      |       |       |       |       | est < |
|       |       |       |      |       |       |       |       | #sect |
|       |       |       |      |       |       |       |       | _9.8. |
|       |       |       |      |       |       |       |       | 1>`__ |
|       |       |       |      |       |       |       |       | 1.    |
|       |       |       |      |       |       |       |       | 2.840 |
|       |       |       |      |       |       |       |       | .1000 |
|       |       |       |      |       |       |       |       | 8.9.7 |
+-------+-------+-------+------+-------+-------+-------+-------+-------+
|       | >     | comp  | 0..1 | MAY   |       |       |       |       |
|       |       | onent |      |       |       |       |       |       |
+-------+-------+-------+------+-------+-------+-------+-------+-------+
| *Pr   | >>    | *sec  | 1..1 | SHALL |       |       |       | `Proc |
| ocedu |       | tion* |      |       |       |       |       | edure |
| re​In |       |       |      |       |       |       |       | Ind   |
| dicat |       |       |      |       |       |       |       | icati |
| ions* |       |       |      |       |       |       |       | ons < |
|       |       |       |      |       |       |       |       | #sect |
|       |       |       |      |       |       |       |       | _9.8. |
|       |       |       |      |       |       |       |       | 2>`__ |
|       |       |       |      |       |       |       |       | 1.2   |
|       |       |       |      |       |       |       |       | .840. |
|       |       |       |      |       |       |       |       | 10008 |
|       |       |       |      |       |       |       |       | .9.22 |
+-------+-------+-------+------+-------+-------+-------+-------+-------+
|       | >     | comp  | 0..1 | MAY   |       |       |       |       |
|       |       | onent |      |       |       |       |       |       |
+-------+-------+-------+------+-------+-------+-------+-------+-------+
| *His  | >>    | *sec  | 1..1 | SHALL |       |       |       | `Me   |
| tory* |       | tion* |      |       |       |       |       | dical |
|       |       |       |      |       |       |       |       | (Gen  |
|       |       |       |      |       |       |       |       | eral) |
|       |       |       |      |       |       |       |       | Hist  |
|       |       |       |      |       |       |       |       | ory < |
|       |       |       |      |       |       |       |       | #sect |
|       |       |       |      |       |       |       |       | _9.8. |
|       |       |       |      |       |       |       |       | 3>`__ |
|       |       |       |      |       |       |       |       | 2.    |
|       |       |       |      |       |       |       |       | 16.84 |
|       |       |       |      |       |       |       |       | 0.1.1 |
|       |       |       |      |       |       |       |       | 13883 |
|       |       |       |      |       |       |       |       | .​10. |
|       |       |       |      |       |       |       |       | 20.22 |
|       |       |       |      |       |       |       |       | .2.39 |
+-------+-------+-------+------+-------+-------+-------+-------+-------+
|       | >     |       | 0..1 | MAY   |       |       |       | `Ge   |
|       |       |       |      |       |       |       |       | neral |
|       |       |       |      |       |       |       |       | Se    |
|       |       |       |      |       |       |       |       | ction |
|       |       |       |      |       |       |       |       | Entr  |
|       |       |       |      |       |       |       |       | ies < |
|       |       |       |      |       |       |       |       | #sect |
|       |       |       |      |       |       |       |       | _9.1. |
|       |       |       |      |       |       |       |       | 2>`__ |
|       |       |       |      |       |       |       |       | 1.2   |
|       |       |       |      |       |       |       |       | .840. |
|       |       |       |      |       |       |       |       | 10008 |
|       |       |       |      |       |       |       |       | .9.23 |
+-------+-------+-------+------+-------+-------+-------+-------+-------+

::

   <section classCode="DOCSECT" moodCode="EVN">
       <templateId root="1.2.840.10008.9.2"/>
       <id root="1.2.840.10213.2.62.994044785528.114289542805"/>
       <code code="55752-0" codeSystem="2.16.840.1.113883.6.1"
           codeSystemName="LOINC" displayName="Clinical Information"/>
       <title>Clinical Information</title>
       <text>The patient was referred for evaluation of suspected pulmonary embolism.</text>
       <!---see examples for other sections/entries -->
   </section>

.. _sect_9.3:

Imaging Procedure Description
-----------------------------

+----------------------+----------------------------------------------+
| **Template ID**      | 1.2.840.10008.9.3                            |
+----------------------+----------------------------------------------+
| **Name**             | Imaging Procedure Description                |
+----------------------+----------------------------------------------+
| **Effective Date**   | 2015/03/24                                   |
+----------------------+----------------------------------------------+
| **Version Label**    | DICOM-20150324                               |
+----------------------+----------------------------------------------+
| **Status**           | Active                                       |
+----------------------+----------------------------------------------+
| **Description**      | The Imaging Procedure Description section    |
|                      | records the technical details of the         |
|                      | procedure and may include information about  |
|                      | protocol, imaging device, contrast,          |
|                      | radiation dose, medications administered     |
|                      | (sedation, stress agents), etc.              |
+----------------------+----------------------------------------------+
| **Classification**   | CDA Section Level                            |
+----------------------+----------------------------------------------+
| **Relationships**    | Included in `Imaging Report <#sect_7.1>`__   |
+----------------------+----------------------------------------------+
| **Context**          | parent node                                  |
+----------------------+----------------------------------------------+
| **Open/Closed**      | Open                                         |
+----------------------+----------------------------------------------+
| **Revision History** | DICOM-20150324: Initial version              |
+----------------------+----------------------------------------------+

+-------+-------+-------+-------+-------+-------+-------+-------+-------+
| Bus   | Nest  | Ele   | Card  | Elem  | Data  | Value | Value | Subsi |
| iness | Level | ment/ |       | /Attr | Type  | Conf  |       | diary |
| Name  |       | ​Attr |       | Conf  |       |       |       | Tem   |
|       |       | ibute |       |       |       |       |       | plate |
+=======+=======+=======+=======+=======+=======+=======+=======+=======+
| **Pro |       | se    | 1..1  | SHALL |       |       |       |       |
| cedur |       | ction |       |       |       |       |       |       |
| e​Des |       |       |       |       |       |       |       |       |
| cript |       |       |       |       |       |       |       |       |
| ion** |       |       |       |       |       |       |       |       |
+-------+-------+-------+-------+-------+-------+-------+-------+-------+
|       | >     | t     | 1..1  | SHALL | II    |       |       |       |
|       |       | empla |       |       |       |       |       |       |
|       |       | te​Id |       |       |       |       |       |       |
+-------+-------+-------+-------+-------+-------+-------+-------+-------+
|       | >@    | @root | 1..1  | SHALL | UID   | SHALL | 1.    |       |
|       |       |       |       |       |       |       | 2.840 |       |
|       |       |       |       |       |       |       | .1000 |       |
|       |       |       |       |       |       |       | 8.9.3 |       |
+-------+-------+-------+-------+-------+-------+-------+-------+-------+
|       | >     | id    | 1..1  | SHALL | II    |       |       |       |
+-------+-------+-------+-------+-------+-------+-------+-------+-------+
|       | >     | code  | 1..1  | SHALL | CD    | SHALL | `(551 |       |
|       |       |       |       |       |       |       | 11-9, |       |
|       |       |       |       |       |       |       | L     |       |
|       |       |       |       |       |       |       | OINC, |       |
|       |       |       |       |       |       |       | "Cu   |       |
|       |       |       |       |       |       |       | rrent |       |
|       |       |       |       |       |       |       | Im    |       |
|       |       |       |       |       |       |       | aging |       |
|       |       |       |       |       |       |       | Proc  |       |
|       |       |       |       |       |       |       | edure |       |
|       |       |       |       |       |       |       | Desc  |       |
|       |       |       |       |       |       |       | ripti |       |
|       |       |       |       |       |       |       | on")  |       |
|       |       |       |       |       |       |       | <http |       |
|       |       |       |       |       |       |       | ://lo |       |
|       |       |       |       |       |       |       | inc.o |       |
|       |       |       |       |       |       |       | rg/55 |       |
|       |       |       |       |       |       |       | 111-9 |       |
|       |       |       |       |       |       |       | />`__ |       |
+-------+-------+-------+-------+-------+-------+-------+-------+-------+
| Title | >     | title | 1..1  | SHALL | ST    |       |       |       |
+-------+-------+-------+-------+-------+-------+-------+-------+-------+
| *     | *>*   | *     | 1..1  | COND  | ED    |       |       | `Se   |
| Text* |       | text* |       |       |       |       |       | ction |
|       |       |       |       |       |       |       |       | T     |
|       |       |       |       |       |       |       |       | ext < |
|       |       |       |       |       |       |       |       | #sect |
|       |       |       |       |       |       |       |       | _9.1. |
|       |       |       |       |       |       |       |       | 1>`__ |
|       |       |       |       |       |       |       |       | 1.2   |
|       |       |       |       |       |       |       |       | .840. |
|       |       |       |       |       |       |       |       | 10008 |
|       |       |       |       |       |       |       |       | .9.19 |
+-------+-------+-------+-------+-------+-------+-------+-------+-------+
|       | >     | entry | 1..1  | SHALL |       |       |       |       |
+-------+-------+-------+-------+-------+-------+-------+-------+-------+
| *     | >>    | *     | 1..1  | SHALL |       |       |       | `Proc |
| Proce |       | proce |       |       |       |       |       | edure |
| dure​ |       | dure* |       |       |       |       |       | Techn |
| Techn |       |       |       |       |       |       |       | ique  |
| ique* |       |       |       |       |       |       |       | <#sec |
|       |       |       |       |       |       |       |       | t_10. |
|       |       |       |       |       |       |       |       | 4>`__ |
|       |       |       |       |       |       |       |       | 1.2   |
|       |       |       |       |       |       |       |       | .840. |
|       |       |       |       |       |       |       |       | 10008 |
|       |       |       |       |       |       |       |       | .9.14 |
+-------+-------+-------+-------+-------+-------+-------+-------+-------+
|       | >     | entry | 0..\* | MAY   |       |       |       |       |
+-------+-------+-------+-------+-------+-------+-------+-------+-------+
| *     | >>    | *     | 1..1  | SHALL |       |       |       | `     |
| Proce |       | subst |       |       |       |       |       | Proce |
| dural |       | ance​ |       |       |       |       |       | dural |
| ​Medi |       | Admin |       |       |       |       |       | M     |
| catio |       | istra |       |       |       |       |       | edica |
| n[*]* |       | tion* |       |       |       |       |       | tion  |
|       |       |       |       |       |       |       |       | <#sec |
|       |       |       |       |       |       |       |       | t_10. |
|       |       |       |       |       |       |       |       | 2>`__ |
|       |       |       |       |       |       |       |       | 1.2   |
|       |       |       |       |       |       |       |       | .840. |
|       |       |       |       |       |       |       |       | 10008 |
|       |       |       |       |       |       |       |       | .9.13 |
+-------+-------+-------+-------+-------+-------+-------+-------+-------+
|       | >     | comp  | 0..1  | MAY   |       |       |       |       |
|       |       | onent |       |       |       |       |       |       |
+-------+-------+-------+-------+-------+-------+-------+-------+-------+
| *Comp | >>    | *sec  | 1..1  | SHALL |       |       |       | `     |
| licat |       | tion* |       |       |       |       |       | Compl |
| ions* |       |       |       |       |       |       |       | icati |
|       |       |       |       |       |       |       |       | ons < |
|       |       |       |       |       |       |       |       | #sect |
|       |       |       |       |       |       |       |       | _9.8. |
|       |       |       |       |       |       |       |       | 4>`__ |
|       |       |       |       |       |       |       |       | 2.    |
|       |       |       |       |       |       |       |       | 16.84 |
|       |       |       |       |       |       |       |       | 0.1.1 |
|       |       |       |       |       |       |       |       | 13883 |
|       |       |       |       |       |       |       |       | .​10. |
|       |       |       |       |       |       |       |       | 20.22 |
|       |       |       |       |       |       |       |       | .2.37 |
+-------+-------+-------+-------+-------+-------+-------+-------+-------+
|       | >     | comp  | 0..1  | COND  |       |       |       |       |
|       |       | onent |       |       |       |       |       |       |
+-------+-------+-------+-------+-------+-------+-------+-------+-------+
| *Radi | >>    | *sec  | 1..1  | SHALL |       |       |       | `Radi |
| ation |       | tion* |       |       |       |       |       | ation |
| ​Expo |       |       |       |       |       |       |       | Exp   |
| sure* |       |       |       |       |       |       |       | osure |
|       |       |       |       |       |       |       |       | and   |
|       |       |       |       |       |       |       |       | Prote |
|       |       |       |       |       |       |       |       | ction |
|       |       |       |       |       |       |       |       | Inf   |
|       |       |       |       |       |       |       |       | ormat |
|       |       |       |       |       |       |       |       | ion < |
|       |       |       |       |       |       |       |       | #sect |
|       |       |       |       |       |       |       |       | _9.8. |
|       |       |       |       |       |       |       |       | 5>`__ |
|       |       |       |       |       |       |       |       | 1.    |
|       |       |       |       |       |       |       |       | 2.840 |
|       |       |       |       |       |       |       |       | .1000 |
|       |       |       |       |       |       |       |       | 8.9.8 |
+-------+-------+-------+-------+-------+-------+-------+-------+-------+
|       | >     | comp  | 1..1  | SHALL |       |       |       |       |
|       |       | onent |       |       |       |       |       |       |
+-------+-------+-------+-------+-------+-------+-------+-------+-------+
| *     | >>    | *sec  | 1..1  | SHALL |       |       |       | `     |
| DICOM |       | tion* |       |       |       |       |       | DICOM |
| Objec |       |       |       |       |       |       |       | O     |
| t​Cat |       |       |       |       |       |       |       | bject |
| alog* |       |       |       |       |       |       |       | Cata  |
|       |       |       |       |       |       |       |       | log < |
|       |       |       |       |       |       |       |       | #sect |
|       |       |       |       |       |       |       |       | _9.8. |
|       |       |       |       |       |       |       |       | 7>`__ |
|       |       |       |       |       |       |       |       | 2.16. |
|       |       |       |       |       |       |       |       | 840.1 |
|       |       |       |       |       |       |       |       | .1138 |
|       |       |       |       |       |       |       |       | 83.​1 |
|       |       |       |       |       |       |       |       | 0.20. |
|       |       |       |       |       |       |       |       | 6.1.1 |
+-------+-------+-------+-------+-------+-------+-------+-------+-------+
|       | >     | entry | 0..1  | MAY   |       |       |       |       |
+-------+-------+-------+-------+-------+-------+-------+-------+-------+
| *Imag | >>    | *ob   | 1..1  | SHALL |       |       |       | `     |
| e​Qua |       | serva |       |       |       |       |       | Image |
| lity* |       | tion* |       |       |       |       |       | Qua   |
|       |       |       |       |       |       |       |       | lity  |
|       |       |       |       |       |       |       |       | <#sec |
|       |       |       |       |       |       |       |       | t_10. |
|       |       |       |       |       |       |       |       | 9>`__ |
|       |       |       |       |       |       |       |       | 1.2   |
|       |       |       |       |       |       |       |       | .840. |
|       |       |       |       |       |       |       |       | 10008 |
|       |       |       |       |       |       |       |       | .9.15 |
+-------+-------+-------+-------+-------+-------+-------+-------+-------+

::

   <section classCode="DOCSECT" moodCode="EVN">
       <templateId root="1.2.840.10008.9.3"/>
       <id root="1.2.840.10213.2.62.9940434234785528.11428954534542805"/>
       <code code="55111-9" codeSystem="2.16.840.1.113883.6.1"
           codeSystemName="LOINC" displayName="Current Imaging Procedure Description"/>
       <title>Imaging Procedure Description</title>
       <text>A CT study was acquired with 2.5 mm images of the abdomen and pelvis with 140 ml of... </text>
       <!-- See Procedure Technique template example - required here -->
       <!-- See DICOM Imaging Catalog template example - required here -->
       <!---see examples for other sections/entries -->
   </section>

.. _sect_9.3.1:

component/section Radiation Exposure and Protection Information
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

COND: If the documented service utilizes ionizing radiation, a
`Radiation Exposure and Protection Information <#sect_9.8.5>`__ section
MAY be present.

.. _sect_9.4:

Comparison Study
----------------

+----------------------+----------------------------------------------+
| **Template​ID**      | 1.2.840.10008.9.4                            |
+----------------------+----------------------------------------------+
| **Name**             | Comparison Study                             |
+----------------------+----------------------------------------------+
| **Effective Date**   | 2015/03/24                                   |
+----------------------+----------------------------------------------+
| **Version Label**    | DICOM-20150324                               |
+----------------------+----------------------------------------------+
| **Status**           | Active                                       |
+----------------------+----------------------------------------------+
| **Description**      | Documentation of a prior Imaging Procedure   |
|                      | to which the current images were compared    |
+----------------------+----------------------------------------------+
| **Classification**   | CDA Section Level                            |
+----------------------+----------------------------------------------+
| **Relationships**    | Included in `Imaging Report <#sect_7.1>`__   |
+----------------------+----------------------------------------------+
| **Context**          | parent node                                  |
+----------------------+----------------------------------------------+
| **Open/Closed**      | Open                                         |
+----------------------+----------------------------------------------+
| **Revision History** | DICOM-20150324: Initial version              |
+----------------------+----------------------------------------------+

+-------+-------+-------+-------+-------+-------+-------+-------+-------+
| Bus   | Nest  | Ele   | Card  | Elem  | Data  | Value | Value | Subsi |
| iness | Level | ment/ |       | /Attr | Type  | Conf  |       | diary |
| Name  |       | ​Attr |       | Conf  |       |       |       | Tem   |
|       |       | ibute |       |       |       |       |       | plate |
+=======+=======+=======+=======+=======+=======+=======+=======+=======+
| **Com |       | se    | 1..1  | SHALL |       |       |       |       |
| paris |       | ction |       |       |       |       |       |       |
| on​St |       |       |       |       |       |       |       |       |
| udy** |       |       |       |       |       |       |       |       |
+-------+-------+-------+-------+-------+-------+-------+-------+-------+
|       | >     | t     | 1..1  | SHALL | II    |       |       |       |
|       |       | empla |       |       |       |       |       |       |
|       |       | te​Id |       |       |       |       |       |       |
+-------+-------+-------+-------+-------+-------+-------+-------+-------+
|       | >@    | @root | 1..1  | SHALL | UID   | SHALL | 1.    |       |
|       |       |       |       |       |       |       | 2.840 |       |
|       |       |       |       |       |       |       | .1000 |       |
|       |       |       |       |       |       |       | 8.9.4 |       |
+-------+-------+-------+-------+-------+-------+-------+-------+-------+
|       | >     | id    | 1..\* | SHALL | II    |       |       |       |
+-------+-------+-------+-------+-------+-------+-------+-------+-------+
|       | >     | code  | 1..1  | SHALL | CD    | SHALL | `(188 |       |
|       |       |       |       |       |       |       | 34-2, |       |
|       |       |       |       |       |       |       | L     |       |
|       |       |       |       |       |       |       | OINC, |       |
|       |       |       |       |       |       |       | "Radi |       |
|       |       |       |       |       |       |       | ology |       |
|       |       |       |       |       |       |       | Compa |       |
|       |       |       |       |       |       |       | rison |       |
|       |       |       |       |       |       |       | stu   |       |
|       |       |       |       |       |       |       | dy")  |       |
|       |       |       |       |       |       |       | <http |       |
|       |       |       |       |       |       |       | ://lo |       |
|       |       |       |       |       |       |       | inc.o |       |
|       |       |       |       |       |       |       | rg/18 |       |
|       |       |       |       |       |       |       | 834-2 |       |
|       |       |       |       |       |       |       | />`__ |       |
+-------+-------+-------+-------+-------+-------+-------+-------+-------+
| Title | >     | title | 1..1  | SHALL | ST    |       |       |       |
+-------+-------+-------+-------+-------+-------+-------+-------+-------+
| *     | *>*   | *     | 1..1  | COND  | ED    |       |       | `Se   |
| Text* |       | text* |       |       |       |       |       | ction |
|       |       |       |       |       |       |       |       | T     |
|       |       |       |       |       |       |       |       | ext < |
|       |       |       |       |       |       |       |       | #sect |
|       |       |       |       |       |       |       |       | _9.1. |
|       |       |       |       |       |       |       |       | 1>`__ |
|       |       |       |       |       |       |       |       | 1.2   |
|       |       |       |       |       |       |       |       | .840. |
|       |       |       |       |       |       |       |       | 10008 |
|       |       |       |       |       |       |       |       | .9.19 |
+-------+-------+-------+-------+-------+-------+-------+-------+-------+
|       | >     | entry | 0..\* | MAY   |       |       |       |       |
+-------+-------+-------+-------+-------+-------+-------+-------+-------+
| *     | >>    | *     | 1..1  | SHALL |       |       |       | `Proc |
| Proce |       | proce |       |       |       |       |       | edure |
| dure​ |       | dure* |       |       |       |       |       | Techn |
| Techn |       |       |       |       |       |       |       | ique  |
| ique* |       |       |       |       |       |       |       | <#sec |
|       |       |       |       |       |       |       |       | t_10. |
|       |       |       |       |       |       |       |       | 4>`__ |
|       |       |       |       |       |       |       |       | 1.2   |
|       |       |       |       |       |       |       |       | .840. |
|       |       |       |       |       |       |       |       | 10008 |
|       |       |       |       |       |       |       |       | .9.14 |
+-------+-------+-------+-------+-------+-------+-------+-------+-------+
|       | >     | entry | 0..\* | MAY   |       |       |       |       |
+-------+-------+-------+-------+-------+-------+-------+-------+-------+
| *Stud | >>    | *act* | 1..1  | SHALL |       |       |       | `     |
| y[*]* |       |       |       |       |       |       |       | Study |
|       |       |       |       |       |       |       |       | Act   |
|       |       |       |       |       |       |       |       | <#sec |
|       |       |       |       |       |       |       |       | t_10. |
|       |       |       |       |       |       |       |       | 6>`__ |
|       |       |       |       |       |       |       |       | 1.2   |
|       |       |       |       |       |       |       |       | .840. |
|       |       |       |       |       |       |       |       | 10008 |
|       |       |       |       |       |       |       |       | .9.16 |
+-------+-------+-------+-------+-------+-------+-------+-------+-------+
|       | >     |       | 0..1  | MAY   |       |       |       | `Ge   |
|       |       |       |       |       |       |       |       | neral |
|       |       |       |       |       |       |       |       | Se    |
|       |       |       |       |       |       |       |       | ction |
|       |       |       |       |       |       |       |       | Entr  |
|       |       |       |       |       |       |       |       | ies < |
|       |       |       |       |       |       |       |       | #sect |
|       |       |       |       |       |       |       |       | _9.1. |
|       |       |       |       |       |       |       |       | 2>`__ |
|       |       |       |       |       |       |       |       | 1.2   |
|       |       |       |       |       |       |       |       | .840. |
|       |       |       |       |       |       |       |       | 10008 |
|       |       |       |       |       |       |       |       | .9.23 |
+-------+-------+-------+-------+-------+-------+-------+-------+-------+

::

   <section classCode="DOCSECT" moodCode="EVN">
       <templateId root="1.2.840.10008.9.4"/>
       <id root="1.2.840.10213.2.62.994056444785528.1142893564536542805"/>
       <code code="18834-2" codeSystem="2.16.840.1.113883.6.1"
           codeSystemName="LOINC" displayName="Radiology Comparison Study"/>
       <title>Comparison Study</title>
       <text>A prior CT with contrast performed on May 7, 2012, showed that ...</text>
       <! ---see examples for other sections/entries />
   </section>

.. _sect_9.5:

Findings
--------

+----------------------+----------------------------------------------+
| **Template ID**      | 2.16.840.1.113883.​10.20.6.1.2               |
+----------------------+----------------------------------------------+
| **Name**             | Findings                                     |
+----------------------+----------------------------------------------+
| **Effective Date**   | 2015/03/24                                   |
+----------------------+----------------------------------------------+
| **Version Label**    | DICOM-20150324                               |
+----------------------+----------------------------------------------+
| **Status**           | Active                                       |
+----------------------+----------------------------------------------+
| **Description**      | Records clinically significant observations  |
|                      | confirmed or discovered during the           |
|                      | procedure.                                   |
+----------------------+----------------------------------------------+
| **Classification**   | CDA Section Level                            |
+----------------------+----------------------------------------------+
| **Relationships**    | Included in `Imaging Report <#sect_7.1>`__   |
+----------------------+----------------------------------------------+
| **Context**          | parent node                                  |
+----------------------+----------------------------------------------+
| **Open/Closed**      | Open                                         |
+----------------------+----------------------------------------------+
| **Revision History** | From Consolidated CDA r1.1                   |
|                      |                                              |
|                      | DICOM-20150324: Added optional subsections   |
|                      | and entries                                  |
+----------------------+----------------------------------------------+

+-------+-------+-------+-------+-------+-------+-------+-------+-------+
| Bus   | Nest  | Ele   | Card  | Elem  | Data  | Value | Value | Subsi |
| iness | Level | ment/ |       | /Attr | Type  | Conf  |       | diary |
| Name  |       | ​Attr |       | Conf  |       |       |       | Tem   |
|       |       | ibute |       |       |       |       |       | plate |
+=======+=======+=======+=======+=======+=======+=======+=======+=======+
| **    |       | se    |       |       |       |       |       |       |
| Findi |       | ction |       |       |       |       |       |       |
| ngs** |       |       |       |       |       |       |       |       |
+-------+-------+-------+-------+-------+-------+-------+-------+-------+
|       | >     | t     | 1..1  | SHALL | II    |       |       |       |
|       |       | empla |       |       |       |       |       |       |
|       |       | te​Id |       |       |       |       |       |       |
+-------+-------+-------+-------+-------+-------+-------+-------+-------+
|       | >@    | @root | 1..1  | SHALL | UID   | SHALL | 2.16. |       |
|       |       |       |       |       |       |       | 840.1 |       |
|       |       |       |       |       |       |       | .1138 |       |
|       |       |       |       |       |       |       | 83.​1 |       |
|       |       |       |       |       |       |       | 0.20. |       |
|       |       |       |       |       |       |       | 6.1.2 |       |
+-------+-------+-------+-------+-------+-------+-------+-------+-------+
|       | >     | id    | 1..\* | SHALL | II    |       |       |       |
+-------+-------+-------+-------+-------+-------+-------+-------+-------+
|       | >     | code  | 1..1  | SHALL | CD    | SHALL | `(597 |       |
|       |       |       |       |       |       |       | 76-5, |       |
|       |       |       |       |       |       |       | L     |       |
|       |       |       |       |       |       |       | OINC, |       |
|       |       |       |       |       |       |       | "Proc |       |
|       |       |       |       |       |       |       | edure |       |
|       |       |       |       |       |       |       | F     |       |
|       |       |       |       |       |       |       | indin |       |
|       |       |       |       |       |       |       | gs")  |       |
|       |       |       |       |       |       |       | <http |       |
|       |       |       |       |       |       |       | ://lo |       |
|       |       |       |       |       |       |       | inc.o |       |
|       |       |       |       |       |       |       | rg/59 |       |
|       |       |       |       |       |       |       | 776-5 |       |
|       |       |       |       |       |       |       | />`__ |       |
+-------+-------+-------+-------+-------+-------+-------+-------+-------+
| Title | >     | title | 1..1  | SHALL | ST    |       |       |       |
+-------+-------+-------+-------+-------+-------+-------+-------+-------+
| *     | *>*   | *     | 1..1  | COND  | ED    |       |       | `Se   |
| Text* |       | text* |       |       |       |       |       | ction |
|       |       |       |       |       |       |       |       | T     |
|       |       |       |       |       |       |       |       | ext < |
|       |       |       |       |       |       |       |       | #sect |
|       |       |       |       |       |       |       |       | _9.1. |
|       |       |       |       |       |       |       |       | 1>`__ |
|       |       |       |       |       |       |       |       | 1.2   |
|       |       |       |       |       |       |       |       | .840. |
|       |       |       |       |       |       |       |       | 10008 |
|       |       |       |       |       |       |       |       | .9.19 |
+-------+-------+-------+-------+-------+-------+-------+-------+-------+
|       | >     | comp  | 0..\* | MAY   |       |       |       |       |
|       |       | onent |       |       |       |       |       |       |
+-------+-------+-------+-------+-------+-------+-------+-------+-------+
| *Fet  | >>    | *sec  | 1..1  | SHALL |       |       |       | `     |
| us​Fi |       | tion* |       |       |       |       |       | Fetus |
| nding |       |       |       |       |       |       |       | Findi |
| s[*]* |       |       |       |       |       |       |       | ngs < |
|       |       |       |       |       |       |       |       | #sect |
|       |       |       |       |       |       |       |       | _9.8. |
|       |       |       |       |       |       |       |       | 8>`__ |
|       |       |       |       |       |       |       |       | 1.    |
|       |       |       |       |       |       |       |       | 2.840 |
|       |       |       |       |       |       |       |       | .1000 |
|       |       |       |       |       |       |       |       | 8.9.9 |
+-------+-------+-------+-------+-------+-------+-------+-------+-------+
|       | >     | comp  | 0..\* | MAY   |       |       |       |       |
|       |       | onent |       |       |       |       |       |       |
+-------+-------+-------+-------+-------+-------+-------+-------+-------+
| *Subs | >>    | *sec  | 1..1  | SHALL |       |       |       | `La   |
| ectio |       | tion* |       |       |       |       |       | beled |
| n[*]* |       |       |       |       |       |       |       | Su    |
|       |       |       |       |       |       |       |       | bsect |
|       |       |       |       |       |       |       |       | ion < |
|       |       |       |       |       |       |       |       | #sect |
|       |       |       |       |       |       |       |       | _9.8. |
|       |       |       |       |       |       |       |       | 9>`__ |
|       |       |       |       |       |       |       |       | 1.2   |
|       |       |       |       |       |       |       |       | .840. |
|       |       |       |       |       |       |       |       | 10008 |
|       |       |       |       |       |       |       |       | .9.10 |
+-------+-------+-------+-------+-------+-------+-------+-------+-------+
|       | >     |       | 0..1  | MAY   |       |       |       | `Ge   |
|       |       |       |       |       |       |       |       | neral |
|       |       |       |       |       |       |       |       | Se    |
|       |       |       |       |       |       |       |       | ction |
|       |       |       |       |       |       |       |       | Entr  |
|       |       |       |       |       |       |       |       | ies < |
|       |       |       |       |       |       |       |       | #sect |
|       |       |       |       |       |       |       |       | _9.1. |
|       |       |       |       |       |       |       |       | 2>`__ |
|       |       |       |       |       |       |       |       | 1.2   |
|       |       |       |       |       |       |       |       | .840. |
|       |       |       |       |       |       |       |       | 10008 |
|       |       |       |       |       |       |       |       | .9.23 |
+-------+-------+-------+-------+-------+-------+-------+-------+-------+

.. _sect_9.5.1:

text
~~~~

If entries are present, the section/text SHALL represent faithfully all
such statements and MAY contain additional text.

The narrative text associated with an actionable finding SHOULD be
highlighted using styleCode Bold. See `<content> Markup and Links From
Entries <#sect_9.1.1.1>`__.

Actionable findings that require a specific follow-up action or
procedure SHOULD be referenced from a recommendation in the
`Recommendation <#sect_9.8.11>`__ section.

Communication of actionable findings SHOULD be documented in the
`Communication of Actionable Findings <#sect_9.8.10>`__ section.

::

   <section classCode="DOCSECT" moodCode="EVN">
       <templateId root="2.16.840.1.113883.10.20.6.1.2"/>
       <id root="1.2.840.10213.2.62.941494044785528.114289542452452805"/>
       <code code="59776-5" codeSystem="2.16.840.1.113883.6.1"
           codeSystemName="LOINC" displayName="Procedure Findings"/>
       <title>Findings</title>
       <text>
           <paragraph>
               <caption>Finding</caption>
               <content ID="Fndng2">The cardiomediastinum is... </content>
           </paragraph>
           <paragraph>
               <caption>Diameter</caption>
               <content ID="Diam2">45mm</content>
           </paragraph>
           ...
       </text>
       <entry>
           <templateId root="2.16.840.1.113883.10.20.6.2.12"/>
           ...
       </entry>
       <!-- see examples for other sections/entries -->
   </section>

.. _sect_9.6:

Impression
----------

+----------------------+----------------------------------------------+
| **Template ID**      | 1.2.840.10008.9.5                            |
+----------------------+----------------------------------------------+
| **Name**             | Impression                                   |
+----------------------+----------------------------------------------+
| **Effective Date**   | 2015/03/24                                   |
+----------------------+----------------------------------------------+
| **Version Label**    | DICOM-20150324                               |
+----------------------+----------------------------------------------+
| **Status**           | Active                                       |
+----------------------+----------------------------------------------+
| **Description**      | The most important diagnoses or other        |
|                      | clinical conclusions that can be made from   |
|                      | the imaging observations and other clinical  |
|                      | information are recorded here. This section  |
|                      | may include recommendations for additional   |
|                      | imaging tests or other actions, as well as   |
|                      | global assessments, such as BI-RADS          |
|                      | Categories or the equivalent.                |
+----------------------+----------------------------------------------+
| **Classification**   | CDA Section Level                            |
+----------------------+----------------------------------------------+
| **Relationships**    | Included in `Imaging Report <#sect_7.1>`__   |
+----------------------+----------------------------------------------+
| **Context**          | parent node                                  |
+----------------------+----------------------------------------------+
| **Open/Closed**      | Open                                         |
+----------------------+----------------------------------------------+
| **Revision History** | DICOM-20150324: Initial version              |
+----------------------+----------------------------------------------+

+-------+-------+-------+-------+-------+-------+-------+-------+-------+
| Bus   | Nest  | Ele   | Card  | Elem  | Data  | Value | Value | Subsi |
| iness | Level | ment/ |       | /Attr | Type  | Conf  |       | diary |
| Name  |       | ​Attr |       | Conf  |       |       |       | Tem   |
|       |       | ibute |       |       |       |       |       | plate |
+=======+=======+=======+=======+=======+=======+=======+=======+=======+
| **Im  |       | se    | 1..1  | SHALL |       |       |       |       |
| press |       | ction |       |       |       |       |       |       |
| ion** |       |       |       |       |       |       |       |       |
+-------+-------+-------+-------+-------+-------+-------+-------+-------+
|       | >     | t     | 1..1  | SHALL | II    |       |       |       |
|       |       | empla |       |       |       |       |       |       |
|       |       | te​Id |       |       |       |       |       |       |
+-------+-------+-------+-------+-------+-------+-------+-------+-------+
|       | >@    | @root | 1..1  | SHALL | UID   | SHALL | 1.    |       |
|       |       |       |       |       |       |       | 2.840 |       |
|       |       |       |       |       |       |       | .1000 |       |
|       |       |       |       |       |       |       | 8.9.5 |       |
+-------+-------+-------+-------+-------+-------+-------+-------+-------+
|       | >     | id    | 1..\* | SHALL | II    |       |       |       |
+-------+-------+-------+-------+-------+-------+-------+-------+-------+
|       | >     | code  | 1..1  | SHALL | CD    | SHALL | `(190 |       |
|       |       |       |       |       |       |       | 05-8, |       |
|       |       |       |       |       |       |       | L     |       |
|       |       |       |       |       |       |       | OINC, |       |
|       |       |       |       |       |       |       | "Impr |       |
|       |       |       |       |       |       |       | essio |       |
|       |       |       |       |       |       |       | ns")  |       |
|       |       |       |       |       |       |       | <http |       |
|       |       |       |       |       |       |       | ://lo |       |
|       |       |       |       |       |       |       | inc.o |       |
|       |       |       |       |       |       |       | rg/19 |       |
|       |       |       |       |       |       |       | 005-8 |       |
|       |       |       |       |       |       |       | />`__ |       |
+-------+-------+-------+-------+-------+-------+-------+-------+-------+
| Title | >     | title | 1..1  | SHALL | ST    |       |       |       |
+-------+-------+-------+-------+-------+-------+-------+-------+-------+
| *     | *>*   | *     | 1..1  | COND  | ED    |       |       | `Se   |
| Text* |       | text* |       |       |       |       |       | ction |
|       |       |       |       |       |       |       |       | T     |
|       |       |       |       |       |       |       |       | ext < |
|       |       |       |       |       |       |       |       | #sect |
|       |       |       |       |       |       |       |       | _9.1. |
|       |       |       |       |       |       |       |       | 1>`__ |
|       |       |       |       |       |       |       |       | 1.2   |
|       |       |       |       |       |       |       |       | .840. |
|       |       |       |       |       |       |       |       | 10008 |
|       |       |       |       |       |       |       |       | .9.19 |
+-------+-------+-------+-------+-------+-------+-------+-------+-------+
|       | >     | comp  | 0..1  | MAY   |       |       |       |       |
|       |       | onent |       |       |       |       |       |       |
+-------+-------+-------+-------+-------+-------+-------+-------+-------+
| *Co   | >>    | *sec  | 1..1  | SHALL |       |       |       | `Com  |
| mmuni |       | tion* |       |       |       |       |       | munic |
| catio |       |       |       |       |       |       |       | ation |
| n​Of​ |       |       |       |       |       |       |       | of    |
| Actio |       |       |       |       |       |       |       | Actio |
| nable |       |       |       |       |       |       |       | nable |
| ​Find |       |       |       |       |       |       |       | F     |
| ings* |       |       |       |       |       |       |       | indin |
|       |       |       |       |       |       |       |       | gs <# |
|       |       |       |       |       |       |       |       | sect_ |
|       |       |       |       |       |       |       |       | 9.8.1 |
|       |       |       |       |       |       |       |       | 0>`__ |
|       |       |       |       |       |       |       |       | 1.2   |
|       |       |       |       |       |       |       |       | .840. |
|       |       |       |       |       |       |       |       | 10008 |
|       |       |       |       |       |       |       |       | .9.11 |
+-------+-------+-------+-------+-------+-------+-------+-------+-------+
|       | >     | comp  | 0..1  | MAY   |       |       |       |       |
|       |       | onent |       |       |       |       |       |       |
+-------+-------+-------+-------+-------+-------+-------+-------+-------+
| *K    | >>    | *sec  | 1..1  | SHALL |       |       |       | `Key  |
| ey​Im |       | tion* |       |       |       |       |       | Ima   |
| ages* |       |       |       |       |       |       |       | ges < |
|       |       |       |       |       |       |       |       | #sect |
|       |       |       |       |       |       |       |       | _9.8. |
|       |       |       |       |       |       |       |       | 6>`__ |
|       |       |       |       |       |       |       |       | 1.3.  |
|       |       |       |       |       |       |       |       | 6.1.4 |
|       |       |       |       |       |       |       |       | .1.19 |
|       |       |       |       |       |       |       |       | 376.​ |
|       |       |       |       |       |       |       |       | 1.4.1 |
|       |       |       |       |       |       |       |       | .2.14 |
+-------+-------+-------+-------+-------+-------+-------+-------+-------+
|       | >     | comp  | 0..\* | MAY   |       |       |       |       |
|       |       | onent |       |       |       |       |       |       |
+-------+-------+-------+-------+-------+-------+-------+-------+-------+
| *     | >>    | *sec  | 1..1  | SHALL |       |       |       | `Re   |
| Recom |       | tion* |       |       |       |       |       | comme |
| menda |       |       |       |       |       |       |       | ndati |
| tion* |       |       |       |       |       |       |       | on <# |
|       |       |       |       |       |       |       |       | sect_ |
|       |       |       |       |       |       |       |       | 9.8.1 |
|       |       |       |       |       |       |       |       | 1>`__ |
|       |       |       |       |       |       |       |       | 1.2   |
|       |       |       |       |       |       |       |       | .840. |
|       |       |       |       |       |       |       |       | 10008 |
|       |       |       |       |       |       |       |       | .9.12 |
+-------+-------+-------+-------+-------+-------+-------+-------+-------+
|       | >     | entry | 0..\* | MAY   |       |       |       |       |
+-------+-------+-------+-------+-------+-------+-------+-------+-------+
| *Cod  | >>    | *ob   | 1..1  | SHALL | CD    |       |       | `     |
| ed​Ob |       | serva |       |       |       |       |       | Coded |
| serva |       | tion* |       |       |       |       |       | Ob    |
| tion* |       |       |       |       |       |       |       | serva |
|       |       |       |       |       |       |       |       | tion  |
|       |       |       |       |       |       |       |       | <#sec |
|       |       |       |       |       |       |       |       | t_10. |
|       |       |       |       |       |       |       |       | 1>`__ |
|       |       |       |       |       |       |       |       | 2     |
|       |       |       |       |       |       |       |       | .16.8 |
|       |       |       |       |       |       |       |       | 40.1. |
|       |       |       |       |       |       |       |       | 11388 |
|       |       |       |       |       |       |       |       | 3.​10 |
|       |       |       |       |       |       |       |       | .20.6 |
|       |       |       |       |       |       |       |       | .2.13 |
+-------+-------+-------+-------+-------+-------+-------+-------+-------+

::

   <section classCode="DOCSECT" moodCode="EVN">
       <templateId root="2.16.840.1.113883.10.20.22.2.27"/>
       <id root="1.2.840.10213.2.62.994948294044785528.11422458954285205"/>
       <code code="19005-8"
           codeSystem="2.16.840.1.113883.6.1"
           codeSystemName="LOINC"
           displayName="Impressions"/>
       <title>Impression</title>
       <text>This exam identified ...</text>
       <!-- other sections and entries here -->
   </section>

.. _sect_9.7:

Addendum
--------

+----------------------+----------------------------------------------+
| **Template ID**      | 1.2.840.10008.9.6                            |
+----------------------+----------------------------------------------+
| **Name**             | Addendum                                     |
+----------------------+----------------------------------------------+
| **Effective Date**   | 2015/03/24                                   |
+----------------------+----------------------------------------------+
| **Version Label**    | DICOM-20150324                               |
+----------------------+----------------------------------------------+
| **Status**           | Active                                       |
+----------------------+----------------------------------------------+
| **Description**      | Addendum section for imaging report includes |
|                      | supplemental information added to the        |
|                      | original document contents..                 |
+----------------------+----------------------------------------------+
| **Classification**   | CDA Section Level                            |
+----------------------+----------------------------------------------+
| **Relationships**    | Included in `Imaging Report <#sect_7.1>`__   |
+----------------------+----------------------------------------------+
| **Context**          | parent node                                  |
+----------------------+----------------------------------------------+
| **Open/Closed**      | Open                                         |
+----------------------+----------------------------------------------+
| **Revision History** | DICOM-20150324: Initial version              |
+----------------------+----------------------------------------------+

+-------+-------+-------+-------+-------+-------+-------+-------+-------+
| Bus   | Nest  | Ele   | Card  | Elem  | Data  | Value | Value | Subsi |
| iness | Level | ment/ |       | /Attr | Type  | Conf  |       | diary |
| Name  |       | ​Attr |       | Conf  |       |       |       | Tem   |
|       |       | ibute |       |       |       |       |       | plate |
+=======+=======+=======+=======+=======+=======+=======+=======+=======+
| **Add |       | se    | 1..1  | SHALL |       |       |       |       |
| endum |       | ction |       |       |       |       |       |       |
| [*]** |       |       |       |       |       |       |       |       |
+-------+-------+-------+-------+-------+-------+-------+-------+-------+
|       | >     | t     | 1..1  | SHALL | II    |       |       |       |
|       |       | empla |       |       |       |       |       |       |
|       |       | te​Id |       |       |       |       |       |       |
+-------+-------+-------+-------+-------+-------+-------+-------+-------+
|       | >@    | @root | 1..1  | SHALL | UID   | SHALL | 1.    |       |
|       |       |       |       |       |       |       | 2.840 |       |
|       |       |       |       |       |       |       | .1000 |       |
|       |       |       |       |       |       |       | 8.9.6 |       |
+-------+-------+-------+-------+-------+-------+-------+-------+-------+
|       | >     | id    | 1..\* | SHALL | II    |       |       |       |
+-------+-------+-------+-------+-------+-------+-------+-------+-------+
|       | >     | code  | 1..1  | SHALL | CD    | SHALL | `(551 |       |
|       |       |       |       |       |       |       | 07-7, |       |
|       |       |       |       |       |       |       | L     |       |
|       |       |       |       |       |       |       | OINC, |       |
|       |       |       |       |       |       |       | "A    |       |
|       |       |       |       |       |       |       | ddend |       |
|       |       |       |       |       |       |       | um")  |       |
|       |       |       |       |       |       |       | <http |       |
|       |       |       |       |       |       |       | ://lo |       |
|       |       |       |       |       |       |       | inc.o |       |
|       |       |       |       |       |       |       | rg/55 |       |
|       |       |       |       |       |       |       | 107-7 |       |
|       |       |       |       |       |       |       | />`__ |       |
+-------+-------+-------+-------+-------+-------+-------+-------+-------+
| Title | >     | title | 1..1  | SHALL | ST    |       |       |       |
+-------+-------+-------+-------+-------+-------+-------+-------+-------+
| *     | *>*   | *     | 1..1  | COND  | ED    |       |       | `Se   |
| Text* |       | text* |       |       |       |       |       | ction |
|       |       |       |       |       |       |       |       | T     |
|       |       |       |       |       |       |       |       | ext < |
|       |       |       |       |       |       |       |       | #sect |
|       |       |       |       |       |       |       |       | _9.1. |
|       |       |       |       |       |       |       |       | 1>`__ |
|       |       |       |       |       |       |       |       | 1.2   |
|       |       |       |       |       |       |       |       | .840. |
|       |       |       |       |       |       |       |       | 10008 |
|       |       |       |       |       |       |       |       | .9.19 |
+-------+-------+-------+-------+-------+-------+-------+-------+-------+
|       | >     | a     | 1..1  | SHALL |       |       |       |       |
|       |       | uthor |       |       |       |       |       |       |
+-------+-------+-------+-------+-------+-------+-------+-------+-------+
| Time  | >>    | time  | 1..1  | SHALL | TS    |       |       |       |
+-------+-------+-------+-------+-------+-------+-------+-------+-------+
|       | >>    | assig | 1..1  | SHALL |       |       |       |       |
|       |       | ned​A |       |       |       |       |       |       |
|       |       | uthor |       |       |       |       |       |       |
+-------+-------+-------+-------+-------+-------+-------+-------+-------+
| Auth  | >>>   | id    | 1..\* | SHALL | II    |       |       |       |
| or​ID |       |       |       |       |       |       |       |       |
+-------+-------+-------+-------+-------+-------+-------+-------+-------+
|       | >>>>  | assig | 1..1  | SHALL |       |       |       |       |
|       |       | ned​P |       |       |       |       |       |       |
|       |       | erson |       |       |       |       |       |       |
+-------+-------+-------+-------+-------+-------+-------+-------+-------+
| A     | >>>>> | name  | 1..1  | SHALL | PN    |       |       |       |
| uthor |       |       |       |       |       |       |       |       |
| ​Name |       |       |       |       |       |       |       |       |
+-------+-------+-------+-------+-------+-------+-------+-------+-------+
|       | >     | comp  | 0..1  | MAY   |       |       |       |       |
|       |       | onent |       |       |       |       |       |       |
+-------+-------+-------+-------+-------+-------+-------+-------+-------+
| *Co   | >>    | *sec  | 1..1  | SHALL |       |       |       | `Com  |
| mmuni |       | tion* |       |       |       |       |       | munic |
| catio |       |       |       |       |       |       |       | ation |
| n​Of​ |       |       |       |       |       |       |       | of    |
| Actio |       |       |       |       |       |       |       | Actio |
| nable |       |       |       |       |       |       |       | nable |
| ​Find |       |       |       |       |       |       |       | F     |
| ings* |       |       |       |       |       |       |       | indin |
|       |       |       |       |       |       |       |       | gs <# |
|       |       |       |       |       |       |       |       | sect_ |
|       |       |       |       |       |       |       |       | 9.8.1 |
|       |       |       |       |       |       |       |       | 0>`__ |
|       |       |       |       |       |       |       |       | 1.2   |
|       |       |       |       |       |       |       |       | .840. |
|       |       |       |       |       |       |       |       | 10008 |
|       |       |       |       |       |       |       |       | .9.11 |
+-------+-------+-------+-------+-------+-------+-------+-------+-------+
|       | >     |       | 0..1  | MAY   |       |       |       | `Ge   |
|       |       |       |       |       |       |       |       | neral |
|       |       |       |       |       |       |       |       | Se    |
|       |       |       |       |       |       |       |       | ction |
|       |       |       |       |       |       |       |       | Entr  |
|       |       |       |       |       |       |       |       | ies < |
|       |       |       |       |       |       |       |       | #sect |
|       |       |       |       |       |       |       |       | _9.1. |
|       |       |       |       |       |       |       |       | 2>`__ |
|       |       |       |       |       |       |       |       | 1.2   |
|       |       |       |       |       |       |       |       | .840. |
|       |       |       |       |       |       |       |       | 10008 |
|       |       |       |       |       |       |       |       | .9.23 |
+-------+-------+-------+-------+-------+-------+-------+-------+-------+

.. _sect_9.7.1:

author
~~~~~~

Note that the Author identified in the document header is the author of
the original report, as that participation sets the default authoring
context for the report. The Author participation in this section shall
be present, and identifies the author of the addendum, even if the same
as the author of the original report.

.. _sect_9.7.2:

component/section - Communication of Actionable Findings
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

It is possible for an imaging report to be legally signed
(authenticated) prior to the Actionable Findings being properly
communicated. In this event, an addendum to the imaging report is often
created to document the communication of the actionable findings. This
can be included in the section/text of the `Addendum <#sect_9.7>`__, or
using the `Communication of Actionable Findings <#sect_9.8.10>`__
subsection.

::

   <section classCode="DOCSECT" moodCode="EVN" ID="Adndm">
       <templateId root="1.2.840.10008.9.6"/>
       <id root="1.2.840.10213.2.62.7906994044785528.1142895428068506"/>
       <code code="55107-7" codeSystem="2.16.840.1.113883.6.1"
           codeSystemName="LOINC" displayName=" Addendum"/>
       <title>Addendum</title>
       <text>The supplemental information added to the original document...</text>
       <author>
           <time value="20140605143000+0500"/>
           <assignedAuthor>
               <id extension="23454345" root="2.16.840.1.113883.19.5"/>
               <assignedPerson>
               <name><given>Henry</given> <family>Radiologist</family></name>
               </assignedPerson>
           </assignedAuthor>
       </author>
   </section>

.. _sect_9.8:

Sub-sections
------------

.. _sect_9.8.1:

Request
~~~~~~~

+----------------------+----------------------------------------------+
| **Template ID**      | 1.2.840.10008.9.7                            |
+----------------------+----------------------------------------------+
| **Name**             | Request                                      |
+----------------------+----------------------------------------------+
| **Effective Date**   | 2015/03/24                                   |
+----------------------+----------------------------------------------+
| **Version Label**    | DICOM-20150324                               |
+----------------------+----------------------------------------------+
| **Status**           | Active                                       |
+----------------------+----------------------------------------------+
| **Description**      | Information about the requested imaging      |
|                      | studies and associated tests. It may include |
|                      | information on the reason for the request,   |
|                      | and on any validation of the request by      |
|                      | clinical decision support against relevant   |
|                      | appropriateness criteria.                    |
+----------------------+----------------------------------------------+
| **Classification**   | CDA Section Level                            |
+----------------------+----------------------------------------------+
| **Relationships**    | Included in `Clinical                        |
|                      | Information <#sect_9.2>`__                   |
+----------------------+----------------------------------------------+
| **Context**          | parent node                                  |
+----------------------+----------------------------------------------+
| **Open/Closed**      | Open                                         |
+----------------------+----------------------------------------------+
| **Revision History** | DICOM-20150324: Initial version              |
+----------------------+----------------------------------------------+

+-------+-------+-------+-------+-------+-------+-------+-------+-------+
| **Bus | *     | **    | **C   | *     | *     | **    | **Va  | **    |
| iness | *Nest | Eleme | ard** | *Elem | *Data | Value | lue** | Subsi |
| N     | Le    | nt/​A |       | /Attr | T     | C     |       | diary |
| ame** | vel** | ttrib |       | C     | ype** | onf** |       | Templ |
|       |       | ute** |       | onf** |       |       |       | ate** |
+-------+-------+-------+-------+-------+-------+-------+-------+-------+
| *     |       | se    | 1..1  | SHALL |       |       |       |       |
| *Requ |       | ction |       |       |       |       |       |       |
| est** |       |       |       |       |       |       |       |       |
+-------+-------+-------+-------+-------+-------+-------+-------+-------+
|       | >     | t     | 1..1  | SHALL | II    |       |       |       |
|       |       | empla |       |       |       |       |       |       |
|       |       | te​Id |       |       |       |       |       |       |
+-------+-------+-------+-------+-------+-------+-------+-------+-------+
|       | >@    | @root | 1..1  | SHALL | UID   | SHALL | 1.    |       |
|       |       |       |       |       |       |       | 2.840 |       |
|       |       |       |       |       |       |       | .1000 |       |
|       |       |       |       |       |       |       | 8.9.7 |       |
+-------+-------+-------+-------+-------+-------+-------+-------+-------+
|       | >     | id    | 1..\* | SHALL | II    |       |       |       |
+-------+-------+-------+-------+-------+-------+-------+-------+-------+
|       | >     | code  | 1..1  | SHALL | CD    | SHALL | `(551 |       |
|       |       |       |       |       |       |       | 15-0, |       |
|       |       |       |       |       |       |       | L     |       |
|       |       |       |       |       |       |       | OINC, |       |
|       |       |       |       |       |       |       | "     |       |
|       |       |       |       |       |       |       | Reque |       |
|       |       |       |       |       |       |       | st")  |       |
|       |       |       |       |       |       |       | <http |       |
|       |       |       |       |       |       |       | ://lo |       |
|       |       |       |       |       |       |       | inc.o |       |
|       |       |       |       |       |       |       | rg/55 |       |
|       |       |       |       |       |       |       | 115-0 |       |
|       |       |       |       |       |       |       | />`__ |       |
+-------+-------+-------+-------+-------+-------+-------+-------+-------+
| Title | >     | title | 1..1  | SHALL | ST    |       |       |       |
+-------+-------+-------+-------+-------+-------+-------+-------+-------+
| *     | *>*   | *     | 1..1  | COND  | ED    |       |       | `Se   |
| Text* |       | text* |       |       |       |       |       | ction |
|       |       |       |       |       |       |       |       | T     |
|       |       |       |       |       |       |       |       | ext < |
|       |       |       |       |       |       |       |       | #sect |
|       |       |       |       |       |       |       |       | _9.1. |
|       |       |       |       |       |       |       |       | 1>`__ |
|       |       |       |       |       |       |       |       | 1.2   |
|       |       |       |       |       |       |       |       | .840. |
|       |       |       |       |       |       |       |       | 10008 |
|       |       |       |       |       |       |       |       | .9.19 |
+-------+-------+-------+-------+-------+-------+-------+-------+-------+
| CD    | >>    | co    | 0..\* | MAY   | ST    |       |       |       |
| SReco |       | ntent |       |       |       |       |       |       |
| rd​Te |       |       |       |       |       |       |       |       |
| xt[*] |       |       |       |       |       |       |       |       |
+-------+-------+-------+-------+-------+-------+-------+-------+-------+
| \*    | >>@   | @ID   | 1..1  | SHALL | XML   |       |       |       |
|       |       |       |       |       | ID    |       |       |       |
+-------+-------+-------+-------+-------+-------+-------+-------+-------+
|       | >     |       | 0..1  | MAY   |       |       |       | `Ge   |
|       |       |       |       |       |       |       |       | neral |
|       |       |       |       |       |       |       |       | Se    |
|       |       |       |       |       |       |       |       | ction |
|       |       |       |       |       |       |       |       | Entr  |
|       |       |       |       |       |       |       |       | ies < |
|       |       |       |       |       |       |       |       | #sect |
|       |       |       |       |       |       |       |       | _9.1. |
|       |       |       |       |       |       |       |       | 2>`__ |
|       |       |       |       |       |       |       |       | 1.2   |
|       |       |       |       |       |       |       |       | .840. |
|       |       |       |       |       |       |       |       | 10008 |
|       |       |       |       |       |       |       |       | .9.23 |
+-------+-------+-------+-------+-------+-------+-------+-------+-------+

.. _sect_9.8.1.1:

text/content and @ID – CDS Record
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

The Request section narrative text block MAY include content blocks
recording clinical decision support assessments of the request with
respect to the indications, patient characteristics, and relevant
guidelines. Each such text/content SHALL include an XML ID attribute
that serves as the business name discriminator associated with an
instantiation of the element. Even if only one content block is
instantiated, the ID attribute shall be present.

::

   <section classCode="DOCSECT" moodCode="EVN">
       <templateId root="1.2.840.10008.9.7" />
       <id root="1.2.840.10213.2.62.7906994785528.114289506"/>
       <code code="55115-0"
           codeSystem="2.16.840.1.113883.6.1"
           codeSystemName="LOINC"
           displayName="Request" />
       <title>Request</title>
       <text>PTA (Iliac Angioplasty) for treatment of symptomatic
           atherosclerotic disease in both iliac arteries.
           <content ID="CDS001">Procedure ordered by Pat Smith, MD, NPI:8740944987.
           Classified APPROPRIATE by RadCDS based on ACR Select criteria
           at 2015-07-21 10:52:31 CDT</content>
       </text>
   </section>

.. _sect_9.8.2:

Procedure Indications
~~~~~~~~~~~~~~~~~~~~~

+----------------------+----------------------------------------------+
| **Template ID**      | 2.16.840.1.113883.​10.20.22.2.29             |
+----------------------+----------------------------------------------+
| **Name**             | Procedure Indications                        |
+----------------------+----------------------------------------------+
| **Effective Date**   | 2012-07                                      |
+----------------------+----------------------------------------------+
| **Version Label**    | DICOM-20150324                               |
+----------------------+----------------------------------------------+
| **Status**           | Active                                       |
+----------------------+----------------------------------------------+
| **Description**      | Records details about the reason for the     |
|                      | procedure. This section may include the      |
|                      | pre-procedure diagnosis or diagnoses as well |
|                      | as one or more symptoms that contribute to   |
|                      | the reason the procedure is being performed. |
+----------------------+----------------------------------------------+
| **Classification**   | CDA Section Level                            |
+----------------------+----------------------------------------------+
| **Relationships**    | Included in `Clinical                        |
|                      | Information <#sect_9.2>`__                   |
+----------------------+----------------------------------------------+
| **Context**          | parent node                                  |
+----------------------+----------------------------------------------+
| **Open/Closed**      | Open                                         |
+----------------------+----------------------------------------------+
| **Revision History** | From Consolidated CDA r1.1                   |
|                      |                                              |
|                      | DICOM-20150324: adapted to use optional      |
|                      | Coded Observation entry rather than optional |
|                      | Indication entry                             |
+----------------------+----------------------------------------------+

+-------+-------+-------+-------+-------+-------+-------+-------+-------+
| **Bus | *     | **    | **C   | *     | *     | **    | **Va  | **    |
| iness | *Nest | Eleme | ard** | *Elem | *Data | Value | lue** | Subsi |
| N     | Le    | nt/​A |       | /Attr | T     | C     |       | diary |
| ame** | vel** | ttrib |       | C     | ype** | onf** |       | Templ |
|       |       | ute** |       | onf** |       |       |       | ate** |
+-------+-------+-------+-------+-------+-------+-------+-------+-------+
| **Pro |       | se    | 1..1  | SHALL |       |       |       |       |
| cedur |       | ction |       |       |       |       |       |       |
| e​Ind |       |       |       |       |       |       |       |       |
| icati |       |       |       |       |       |       |       |       |
| ons** |       |       |       |       |       |       |       |       |
+-------+-------+-------+-------+-------+-------+-------+-------+-------+
|       | >     | t     | 1..1  | SHALL | II    |       |       |       |
|       |       | empla |       |       |       |       |       |       |
|       |       | te​Id |       |       |       |       |       |       |
+-------+-------+-------+-------+-------+-------+-------+-------+-------+
|       | >@    | @root | 1..1  | SHALL | UID   | SHALL | 2.    |       |
|       |       |       |       |       |       |       | 16.84 |       |
|       |       |       |       |       |       |       | 0.1.1 |       |
|       |       |       |       |       |       |       | 13883 |       |
|       |       |       |       |       |       |       | .​10. |       |
|       |       |       |       |       |       |       | 20.22 |       |
|       |       |       |       |       |       |       | .2.29 |       |
+-------+-------+-------+-------+-------+-------+-------+-------+-------+
|       | >     | id    | 1..\* | SHALL | II    |       |       |       |
+-------+-------+-------+-------+-------+-------+-------+-------+-------+
|       | >     | code  | 1..1  | SHALL | CD    | SHALL | `(597 |       |
|       |       |       |       |       |       |       | 68-2, |       |
|       |       |       |       |       |       |       | L     |       |
|       |       |       |       |       |       |       | OINC, |       |
|       |       |       |       |       |       |       | "Proc |       |
|       |       |       |       |       |       |       | edure |       |
|       |       |       |       |       |       |       | Indi  |       |
|       |       |       |       |       |       |       | catio |       |
|       |       |       |       |       |       |       | ns")  |       |
|       |       |       |       |       |       |       | <http |       |
|       |       |       |       |       |       |       | ://lo |       |
|       |       |       |       |       |       |       | inc.o |       |
|       |       |       |       |       |       |       | rg/59 |       |
|       |       |       |       |       |       |       | 768-2 |       |
|       |       |       |       |       |       |       | />`__ |       |
+-------+-------+-------+-------+-------+-------+-------+-------+-------+
| Title | >     | title | 1..1  | SHALL | ST    |       |       |       |
+-------+-------+-------+-------+-------+-------+-------+-------+-------+
| *     | *>*   | *     | 1..1  | COND  | ED    |       |       | `Se   |
| Text* |       | text* |       |       |       |       |       | ction |
|       |       |       |       |       |       |       |       | T     |
|       |       |       |       |       |       |       |       | ext < |
|       |       |       |       |       |       |       |       | #sect |
|       |       |       |       |       |       |       |       | _9.1. |
|       |       |       |       |       |       |       |       | 1>`__ |
|       |       |       |       |       |       |       |       | 1.2   |
|       |       |       |       |       |       |       |       | .840. |
|       |       |       |       |       |       |       |       | 10008 |
|       |       |       |       |       |       |       |       | .9.19 |
+-------+-------+-------+-------+-------+-------+-------+-------+-------+
|       | >     | entry | 0..\* | MAY   |       |       |       |       |
+-------+-------+-------+-------+-------+-------+-------+-------+-------+
| *C    | >>    | *ob   | 1..1  | SHALL |       |       | See   | `     |
| oded​ |       | serva |       |       |       |       | `e    | Coded |
| Obser |       | tion* |       |       |       |       | ntry/ | Ob    |
| vatio |       |       |       |       |       |       | obser | serva |
| n[*]* |       |       |       |       |       |       | vatio | tion  |
|       |       |       |       |       |       |       | n <#s | <#sec |
|       |       |       |       |       |       |       | ect_9 | t_10. |
|       |       |       |       |       |       |       | .8.2. | 1>`__ |
|       |       |       |       |       |       |       | 1>`__ | 2     |
|       |       |       |       |       |       |       |       | .16.8 |
|       |       |       |       |       |       |       |       | 40.1. |
|       |       |       |       |       |       |       |       | 11388 |
|       |       |       |       |       |       |       |       | 3.​10 |
|       |       |       |       |       |       |       |       | .20.6 |
|       |       |       |       |       |       |       |       | .2.13 |
+-------+-------+-------+-------+-------+-------+-------+-------+-------+

.. _sect_9.8.2.1:

entry/observation
^^^^^^^^^^^^^^^^^

The binding to the Coded Observation concept domains is:

+---------------------------+------------+---------------------------+
| Concept Domain or Element | Value Conf | Value                     |
+===========================+============+===========================+
| Observation​Type          | SHOULD     | (432678004, SNOMED,       |
|                           |            | "Indication for           |
|                           |            | procedure")               |
+---------------------------+------------+---------------------------+
| Other concept domains     |            | unspecified               |
+---------------------------+------------+---------------------------+

.. note::

   In Consolidated CDA r1.1 the binding to the observationType is to
   Value Set Problem Type (2.16.840.1.113883.3.88.12.3221.7.2) with
   conformance SHOULD. Values from that Value Set are acceptable here as
   well.

::

   <section classCode="DOCSECT" moodCode="EVN">
       <templateId root="2.16.840.1.113883.10.20.22.2.29"/>
       <id root="1.2.840.10213.2.62.044785528.1142895426"/>
       <code code="59768-2"
           codeSystem="2.16.840.1.113883.6.1"
           codeSystemName="LOINC"
           displayName="Procedure Indications"/>
       <title>Procedure Indications</title>
       <text>The procedure is performed as a follow-up for abnormal screening result.</text>
   </section>

.. _sect_9.8.3:

Medical (General) History
~~~~~~~~~~~~~~~~~~~~~~~~~

+----------------------+----------------------------------------------+
| **Template ID**      | 2.16.840.1.113883.​10.20.22.2.39             |
+----------------------+----------------------------------------------+
| **Name**             | Medical (General) History                    |
+----------------------+----------------------------------------------+
| **Effective Date**   | 2012-07                                      |
+----------------------+----------------------------------------------+
| **Version Label**    | DICOM-20150324                               |
+----------------------+----------------------------------------------+
| **Status**           | Active                                       |
+----------------------+----------------------------------------------+
| **Description**      | History general describes all aspects of     |
|                      | medical history of the patient even if not   |
|                      | pertinent to the current procedure, and may  |
|                      | include chief complaint, past medical        |
|                      | history, social history, family history,     |
|                      | surgical or procedure history, medication    |
|                      | history, and other history information. The  |
|                      | history may be limited to information        |
|                      | pertinent to the current procedure or may be |
|                      | more comprehensive. It may also be reported  |
|                      | as a collection of random clinical           |
|                      | statements or it may be reported             |
|                      | categorically. Categorical report formats    |
|                      | may be divided into multiple subsections,    |
|                      | including Past Medical History and Social    |
|                      | History.                                     |
+----------------------+----------------------------------------------+
| **Classification**   | CDA Section Level                            |
+----------------------+----------------------------------------------+
| **Relationships**    | Included in `Clinical                        |
|                      | Information <#sect_9.2>`__                   |
+----------------------+----------------------------------------------+
| **Context**          | parent node                                  |
+----------------------+----------------------------------------------+
| **Open/Closed**      | Open                                         |
+----------------------+----------------------------------------------+
| **Revision History** | From Consolidated CDA r1.1                   |
|                      |                                              |
|                      | DICOM-20150324: Addition of optional         |
|                      | entries; C-CDA templateID retained           |
+----------------------+----------------------------------------------+

+-------+-------+-------+-------+-------+-------+-------+-------+-------+
| **Bus | *     | **    | **C   | *     | *     | **    | **Va  | **    |
| iness | *Nest | Eleme | ard** | *Elem | *Data | Value | lue** | Subsi |
| N     | Le    | nt/​A |       | /Attr | T     | C     |       | diary |
| ame** | vel** | ttrib |       | C     | ype** | onf** |       | Templ |
|       |       | ute** |       | onf** |       |       |       | ate** |
+-------+-------+-------+-------+-------+-------+-------+-------+-------+
| *     |       | se    | 1..1  | SHALL |       |       |       |       |
| *Hist |       | ction |       |       |       |       |       |       |
| ory** |       |       |       |       |       |       |       |       |
+-------+-------+-------+-------+-------+-------+-------+-------+-------+
|       | >     | t     | 1..1  | SHALL | II    |       |       |       |
|       |       | empla |       |       |       |       |       |       |
|       |       | te​Id |       |       |       |       |       |       |
+-------+-------+-------+-------+-------+-------+-------+-------+-------+
|       | >@    | @root | 1..1  | SHALL | UID   | SHALL | 2.    |       |
|       |       |       |       |       |       |       | 16.84 |       |
|       |       |       |       |       |       |       | 0.1.1 |       |
|       |       |       |       |       |       |       | 13883 |       |
|       |       |       |       |       |       |       | .​10. |       |
|       |       |       |       |       |       |       | 20.22 |       |
|       |       |       |       |       |       |       | .2.39 |       |
+-------+-------+-------+-------+-------+-------+-------+-------+-------+
|       | >     | id    | 1..\* | SHALL | II    |       |       |       |
+-------+-------+-------+-------+-------+-------+-------+-------+-------+
|       | >     | code  | 1..1  | SHALL | CD    | SHALL | `(113 |       |
|       |       |       |       |       |       |       | 29-0, |       |
|       |       |       |       |       |       |       | L     |       |
|       |       |       |       |       |       |       | OINC, |       |
|       |       |       |       |       |       |       | "Hi   |       |
|       |       |       |       |       |       |       | story |       |
|       |       |       |       |       |       |       | Gener |       |
|       |       |       |       |       |       |       | al")  |       |
|       |       |       |       |       |       |       | <http |       |
|       |       |       |       |       |       |       | ://lo |       |
|       |       |       |       |       |       |       | inc.o |       |
|       |       |       |       |       |       |       | rg/11 |       |
|       |       |       |       |       |       |       | 329-0 |       |
|       |       |       |       |       |       |       | />`__ |       |
+-------+-------+-------+-------+-------+-------+-------+-------+-------+
| Title | >     | title | 1..1  | SHALL | ST    |       |       |       |
+-------+-------+-------+-------+-------+-------+-------+-------+-------+
| *     | *>*   | *     | 1..1  | COND  | ED    |       |       | `Se   |
| Text* |       | text* |       |       |       |       |       | ction |
|       |       |       |       |       |       |       |       | T     |
|       |       |       |       |       |       |       |       | ext < |
|       |       |       |       |       |       |       |       | #sect |
|       |       |       |       |       |       |       |       | _9.1. |
|       |       |       |       |       |       |       |       | 1>`__ |
|       |       |       |       |       |       |       |       | 1.2   |
|       |       |       |       |       |       |       |       | .840. |
|       |       |       |       |       |       |       |       | 10008 |
|       |       |       |       |       |       |       |       | .9.19 |
+-------+-------+-------+-------+-------+-------+-------+-------+-------+
|       | >     |       | 0..1  | MAY   |       |       |       | `Ge   |
|       |       |       |       |       |       |       |       | neral |
|       |       |       |       |       |       |       |       | Se    |
|       |       |       |       |       |       |       |       | ction |
|       |       |       |       |       |       |       |       | Entr  |
|       |       |       |       |       |       |       |       | ies < |
|       |       |       |       |       |       |       |       | #sect |
|       |       |       |       |       |       |       |       | _9.1. |
|       |       |       |       |       |       |       |       | 2>`__ |
|       |       |       |       |       |       |       |       | 1.2   |
|       |       |       |       |       |       |       |       | .840. |
|       |       |       |       |       |       |       |       | 10008 |
|       |       |       |       |       |       |       |       | .9.23 |
+-------+-------+-------+-------+-------+-------+-------+-------+-------+

.. _sect_9.8.3.1:

section/text
^^^^^^^^^^^^

In the context of an Imaging Report, the section/text should document
any contraindications to contrast administration or other procedure
techniques that affected the selection or performance of the protocol.

::

   <section classCode="DOCSECT" moodCode="EVN">
       <templateId root="2.16.840.1.113883.10.20.22.2.39"/>
       <id root="1.2.840.10213.2.62.7044785528.114289875"/>
       <code code="11329-0"
           codeSystem="2.16.840.1.113883.6.1"
           codeSystemName="LOINC"
           displayName="History General"/>
       <title>Relevant Medical History</title>
       <text>
           <list>
               <item>Patient reported adverse reaction to iodine.</item>
               <item>Patient is smoker (1 pack daily).</item>
           </list>
       </text>
   </section>

.. _sect_9.8.4:

Complications
~~~~~~~~~~~~~

+----------------------+----------------------------------------------+
| **Template ID**      | 2.16.840.1.113883.​10.20.22.2.37             |
+----------------------+----------------------------------------------+
| **Name**             | Complications                                |
+----------------------+----------------------------------------------+
| **Effective Date**   | 2012-07                                      |
+----------------------+----------------------------------------------+
| **Version Label**    | DICOM-20150324                               |
+----------------------+----------------------------------------------+
| **Status**           | Active                                       |
+----------------------+----------------------------------------------+
| **Description**      | The Complications section records problems   |
|                      | that occurred during the procedure or other  |
|                      | activity. The complications may have been    |
|                      | known risks or unanticipated problems.       |
+----------------------+----------------------------------------------+
| **Classification**   | CDA Section Level                            |
+----------------------+----------------------------------------------+
| **Relationships**    | Included in `Imaging Procedure               |
|                      | Description <#sect_9.3>`__                   |
+----------------------+----------------------------------------------+
| **Context**          | parent node                                  |
+----------------------+----------------------------------------------+
| **Open/Closed**      | Open                                         |
+----------------------+----------------------------------------------+
| **Revision History** | From Consolidated CDA r1.1                   |
|                      |                                              |
|                      | DICOM-20150324: Addition of optional entries |
+----------------------+----------------------------------------------+

+-------+-------+-------+-------+-------+-------+-------+-------+-------+
| **Bus | *     | **    | **C   | *     | *     | **    | **Va  | **    |
| iness | *Nest | Eleme | ard** | *Elem | *Data | Value | lue** | Subsi |
| N     | Le    | nt/​A |       | /Attr | T     | C     |       | diary |
| ame** | vel** | ttrib |       | C     | ype** | onf** |       | Templ |
|       |       | ute** |       | onf** |       |       |       | ate** |
+-------+-------+-------+-------+-------+-------+-------+-------+-------+
| **    |       | se    | 1..1  | SHALL |       |       |       |       |
| Compl |       | ction |       |       |       |       |       |       |
| icati |       |       |       |       |       |       |       |       |
| ons** |       |       |       |       |       |       |       |       |
+-------+-------+-------+-------+-------+-------+-------+-------+-------+
|       | >     | t     | 1..1  | SHALL | II    |       |       |       |
|       |       | empla |       |       |       |       |       |       |
|       |       | te​Id |       |       |       |       |       |       |
+-------+-------+-------+-------+-------+-------+-------+-------+-------+
|       | >@    | @root | 1..1  | SHALL | UID   | SHALL | 2.    |       |
|       |       |       |       |       |       |       | 16.84 |       |
|       |       |       |       |       |       |       | 0.1.1 |       |
|       |       |       |       |       |       |       | 13883 |       |
|       |       |       |       |       |       |       | .​10. |       |
|       |       |       |       |       |       |       | 20.22 |       |
|       |       |       |       |       |       |       | .2.37 |       |
+-------+-------+-------+-------+-------+-------+-------+-------+-------+
|       | >     | id    | 1..\* | SHALL | II    |       |       |       |
+-------+-------+-------+-------+-------+-------+-------+-------+-------+
|       | >     | code  | 1..1  | SHALL | CD    | SHALL | `(551 |       |
|       |       |       |       |       |       |       | 09-3, |       |
|       |       |       |       |       |       |       | L     |       |
|       |       |       |       |       |       |       | OINC, |       |
|       |       |       |       |       |       |       | "C    |       |
|       |       |       |       |       |       |       | ompli |       |
|       |       |       |       |       |       |       | catio |       |
|       |       |       |       |       |       |       | ns")  |       |
|       |       |       |       |       |       |       | <http |       |
|       |       |       |       |       |       |       | ://lo |       |
|       |       |       |       |       |       |       | inc.o |       |
|       |       |       |       |       |       |       | rg/55 |       |
|       |       |       |       |       |       |       | 109-3 |       |
|       |       |       |       |       |       |       | />`__ |       |
+-------+-------+-------+-------+-------+-------+-------+-------+-------+
| Title | >     | title | 1..1  | SHALL | ST    |       |       |       |
+-------+-------+-------+-------+-------+-------+-------+-------+-------+
| *     | *>*   | *     | 1..1  | COND  | ED    |       |       | `Se   |
| Text* |       | text* |       |       |       |       |       | ction |
|       |       |       |       |       |       |       |       | T     |
|       |       |       |       |       |       |       |       | ext < |
|       |       |       |       |       |       |       |       | #sect |
|       |       |       |       |       |       |       |       | _9.1. |
|       |       |       |       |       |       |       |       | 1>`__ |
|       |       |       |       |       |       |       |       | 1.2   |
|       |       |       |       |       |       |       |       | .840. |
|       |       |       |       |       |       |       |       | 10008 |
|       |       |       |       |       |       |       |       | .9.19 |
+-------+-------+-------+-------+-------+-------+-------+-------+-------+
|       | >     | entry | 0..\* | MAY   |       |       |       |       |
+-------+-------+-------+-------+-------+-------+-------+-------+-------+
| *C    | >>    | *ob   |       |       |       |       |       | `     |
| oded​ |       | serva |       |       |       |       |       | Coded |
| Obser |       | tion* |       |       |       |       |       | Ob    |
| vatio |       |       |       |       |       |       |       | serva |
| n[*]* |       |       |       |       |       |       |       | tion  |
|       |       |       |       |       |       |       |       | <#sec |
|       |       |       |       |       |       |       |       | t_10. |
|       |       |       |       |       |       |       |       | 1>`__ |
|       |       |       |       |       |       |       |       | 2     |
|       |       |       |       |       |       |       |       | .16.8 |
|       |       |       |       |       |       |       |       | 40.1. |
|       |       |       |       |       |       |       |       | 11388 |
|       |       |       |       |       |       |       |       | 3.​10 |
|       |       |       |       |       |       |       |       | .20.6 |
|       |       |       |       |       |       |       |       | .2.13 |
+-------+-------+-------+-------+-------+-------+-------+-------+-------+

::

   <section classCode="DOCSECT" moodCode="EVN">
       <templateId root="2.16.840.1.113883.10.20.22.2.37"/>
       <id root="1.2.840.10213.2.62.70444786655528.11428987524546666"/>
       <code code="55109-3"
           codeSystem="2.16.840.1.113883.6.1"
           codeSystemName="LOINC"
           displayName="Complications"/>
       <title>Complications</title>
       <text>Immediately following IV contrast injection, the patient reporting itching "all over".
           Dr. Smith examined the patient and found multiple urticaria. The patient denied difficulty
           breathing or swallowing. The patient was given Benadryl 50 mg PO and was followed for
           30 minutes, during which time the symptoms subsided.</text>
       <entry>
           <observation classCode="OBS" moodCode="EVN">
               <templateId root="2.16.840.1.113883.10.20.6.2.13"/>
               <!-- Coded Observation -->
               ...
           </observation>
       </entry>
   </section>

.. _sect_9.8.5:

Radiation Exposure and Protection Information
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

+----------------------+----------------------------------------------+
| **Template ID**      | 1.2.840.10008.9.8                            |
+----------------------+----------------------------------------------+
| **Name**             | Radiation Exposure and Protection            |
|                      | Information                                  |
+----------------------+----------------------------------------------+
| **Effective Date**   | 2015/03/24                                   |
+----------------------+----------------------------------------------+
| **Version Label**    | DICOM-20150324                               |
+----------------------+----------------------------------------------+
| **Status**           | Active                                       |
+----------------------+----------------------------------------------+
| **Description**      | Contains information related to the          |
|                      | radiation exposure and protection of the     |
|                      | patient, as may be required by national or   |
|                      | local legal requirements or standards.       |
+----------------------+----------------------------------------------+
| **Classification**   | CDA Section and Entry Level                  |
+----------------------+----------------------------------------------+
| **Relationships**    | Included in `Imaging Procedure               |
|                      | Description <#sect_9.3>`__                   |
+----------------------+----------------------------------------------+
| **Context**          | parent node                                  |
+----------------------+----------------------------------------------+
| **Open/Closed**      | Open                                         |
+----------------------+----------------------------------------------+
| **Revision History** | DICOM-20150324: Initial version              |
+----------------------+----------------------------------------------+

+-------+-------+-------+-------+-------+-------+-------+-------+-------+
| **Bus | *     | **    | **C   | *     | *     | **    | **Va  | **    |
| iness | *Nest | Eleme | ard** | *Elem | *Data | Value | lue** | Subsi |
| N     | Le    | nt/​A |       | /Attr | T     | C     |       | diary |
| ame** | vel** | ttrib |       | C     | ype** | onf** |       | Templ |
|       |       | ute** |       | onf** |       |       |       | ate** |
+-------+-------+-------+-------+-------+-------+-------+-------+-------+
| **    |       | se    | 1..1  | SHALL |       |       |       |       |
| Radia |       | ction |       |       |       |       |       |       |
| tion​ |       |       |       |       |       |       |       |       |
| Expos |       |       |       |       |       |       |       |       |
| ure** |       |       |       |       |       |       |       |       |
+-------+-------+-------+-------+-------+-------+-------+-------+-------+
|       | >     | t     | 1..1  | SHALL | II    |       |       |       |
|       |       | empla |       |       |       |       |       |       |
|       |       | te​Id |       |       |       |       |       |       |
+-------+-------+-------+-------+-------+-------+-------+-------+-------+
|       | >>@   | @root | 1..1  | SHALL | UID   | SHALL | 1.    |       |
|       |       |       |       |       |       |       | 2.840 |       |
|       |       |       |       |       |       |       | .1000 |       |
|       |       |       |       |       |       |       | 8.9.8 |       |
+-------+-------+-------+-------+-------+-------+-------+-------+-------+
|       | >     | code  | 1..1  | SHALL | CD    | SHALL | `(735 |       |
|       |       |       |       |       |       |       | 69-6, |       |
|       |       |       |       |       |       |       | L     |       |
|       |       |       |       |       |       |       | OINC, |       |
|       |       |       |       |       |       |       | "Radi |       |
|       |       |       |       |       |       |       | ation |       |
|       |       |       |       |       |       |       | exp   |       |
|       |       |       |       |       |       |       | osure |       |
|       |       |       |       |       |       |       | and   |       |
|       |       |       |       |       |       |       | prote |       |
|       |       |       |       |       |       |       | ction |       |
|       |       |       |       |       |       |       | info  |       |
|       |       |       |       |       |       |       | rmati |       |
|       |       |       |       |       |       |       | on")  |       |
|       |       |       |       |       |       |       | <http |       |
|       |       |       |       |       |       |       | ://lo |       |
|       |       |       |       |       |       |       | inc.o |       |
|       |       |       |       |       |       |       | rg/73 |       |
|       |       |       |       |       |       |       | 569-6 |       |
|       |       |       |       |       |       |       | />`__ |       |
+-------+-------+-------+-------+-------+-------+-------+-------+-------+
|       | >     | id    | 1..1  | SHALL | II    |       |       |       |
+-------+-------+-------+-------+-------+-------+-------+-------+-------+
| Title | >     | title | 1..1  | SHALL | ST    |       |       |       |
+-------+-------+-------+-------+-------+-------+-------+-------+-------+
| *     | *>*   | *     | 1..1  | SHALL | ED    |       |       | `Se   |
| Text* |       | text* |       |       |       |       |       | ction |
|       |       |       |       |       |       |       |       | T     |
|       |       |       |       |       |       |       |       | ext < |
|       |       |       |       |       |       |       |       | #sect |
|       |       |       |       |       |       |       |       | _9.1. |
|       |       |       |       |       |       |       |       | 1>`__ |
|       |       |       |       |       |       |       |       | 1.2   |
|       |       |       |       |       |       |       |       | .840. |
|       |       |       |       |       |       |       |       | 10008 |
|       |       |       |       |       |       |       |       | .9.19 |
+-------+-------+-------+-------+-------+-------+-------+-------+-------+
|       | >     | entry | 0..1  | COND  |       |       |       |       |
+-------+-------+-------+-------+-------+-------+-------+-------+-------+
|       | >>    | proc  | 1..1  | SHALL |       |       |       |       |
|       |       | edure |       |       |       |       |       |       |
+-------+-------+-------+-------+-------+-------+-------+-------+-------+
|       | >>@   | @clas | 1..1  | SHALL | CS    | SHALL | PROC  |       |
|       |       | sCode |       |       |       |       |       |       |
+-------+-------+-------+-------+-------+-------+-------+-------+-------+
|       | >>@   | @moo  | 1..1  | SHALL | CS    | SHALL | EVN   |       |
|       |       | dCode |       |       |       |       |       |       |
+-------+-------+-------+-------+-------+-------+-------+-------+-------+
|       | >>>   | code  | 1..1  | SHALL | CD    | SHALL | (12   |       |
|       |       |       |       |       |       |       | 1290, |       |
|       |       |       |       |       |       |       | DCM,  |       |
|       |       |       |       |       |       |       | "Pa   |       |
|       |       |       |       |       |       |       | tient |       |
|       |       |       |       |       |       |       | exp   |       |
|       |       |       |       |       |       |       | osure |       |
|       |       |       |       |       |       |       | to    |       |
|       |       |       |       |       |       |       | ion   |       |
|       |       |       |       |       |       |       | izing |       |
|       |       |       |       |       |       |       | r     |       |
|       |       |       |       |       |       |       | adiat |       |
|       |       |       |       |       |       |       | ion") |       |
+-------+-------+-------+-------+-------+-------+-------+-------+-------+
|       | >>>   | p     | 1..1  | SHALL |       |       |       |       |
|       |       | artic |       |       |       |       |       |       |
|       |       | ipant |       |       |       |       |       |       |
+-------+-------+-------+-------+-------+-------+-------+-------+-------+
|       | >>@   | @typ  | 1..1  | SHALL | CS    | SHALL | RESP  |       |
|       |       | eCode |       |       |       |       |       |       |
+-------+-------+-------+-------+-------+-------+-------+-------+-------+
|       | >>>   | p     | 1..1  | SHALL |       |       |       |       |
|       |       | artic |       |       |       |       |       |       |
|       |       | ipant |       |       |       |       |       |       |
|       |       | ​Role |       |       |       |       |       |       |
+-------+-------+-------+-------+-------+-------+-------+-------+-------+
| I     | >>>>  | id    | 1..1  | SHALL | II    |       |       |       |
| rradi |       |       |       |       |       |       |       |       |
| ation |       |       |       |       |       |       |       |       |
| ​Auth |       |       |       |       |       |       |       |       |
| orizi |       |       |       |       |       |       |       |       |
| ng​ID |       |       |       |       |       |       |       |       |
+-------+-------+-------+-------+-------+-------+-------+-------+-------+
|       | >>>>  | fun   | 1..1  | SHALL | CE    | SHALL | (11   |       |
|       |       | ction |       |       |       |       | 3850, |       |
|       |       | ​Code |       |       |       |       | DCM,  |       |
|       |       |       |       |       |       |       | "I    |       |
|       |       |       |       |       |       |       | rradi |       |
|       |       |       |       |       |       |       | ation |       |
|       |       |       |       |       |       |       | Aut   |       |
|       |       |       |       |       |       |       | horiz |       |
|       |       |       |       |       |       |       | ing") |       |
+-------+-------+-------+-------+-------+-------+-------+-------+-------+
|       | >>>>  | play  | 1..1  | SHALL |       |       |       |       |
|       |       | ing​E |       |       |       |       |       |       |
|       |       | ntity |       |       |       |       |       |       |
+-------+-------+-------+-------+-------+-------+-------+-------+-------+
| Irr   | >>>>> | name  | 1..1  | SHALL | PN    |       |       |       |
| adiat |       |       |       |       |       |       |       |       |
| ion​A |       |       |       |       |       |       |       |       |
| uthor |       |       |       |       |       |       |       |       |
| izing |       |       |       |       |       |       |       |       |
| ​Name |       |       |       |       |       |       |       |       |
+-------+-------+-------+-------+-------+-------+-------+-------+-------+
|       | >     | entry | 0..\* | MAY   |       |       |       |       |
+-------+-------+-------+-------+-------+-------+-------+-------+-------+
| *     | >>    | *ob   | 1..1  | SHALL |       |       |       | `SOP  |
| SOPIn |       | serva |       |       |       |       |       | Ins   |
| stanc |       | tion* |       |       |       |       |       | tance |
| e[*]* |       |       |       |       |       |       |       | Ob    |
|       |       |       |       |       |       |       |       | serva |
|       |       |       |       |       |       |       |       | tion  |
|       |       |       |       |       |       |       |       | <#sec |
|       |       |       |       |       |       |       |       | t_10. |
|       |       |       |       |       |       |       |       | 8>`__ |
|       |       |       |       |       |       |       |       | 1.2   |
|       |       |       |       |       |       |       |       | .840. |
|       |       |       |       |       |       |       |       | 10008 |
|       |       |       |       |       |       |       |       | .9.18 |
+-------+-------+-------+-------+-------+-------+-------+-------+-------+
|       | >     | entry | 1..1  | COND  |       |       |       |       |
+-------+-------+-------+-------+-------+-------+-------+-------+-------+
| *     | >>    | *ob   | 1..1  | SHALL |       |       | [See  | `     |
| Coded |       | serva |       |       |       |       | `en   | Coded |
| ​Obse |       | tion* |       |       |       |       | try/o | Ob    |
| rvati |       |       |       |       |       |       | bserv | serva |
| on​[p |       |       |       |       |       |       | ation | tion  |
| regna |       |       |       |       |       |       | Preg  | <#sec |
| ncy]* |       |       |       |       |       |       | nancy | t_10. |
|       |       |       |       |       |       |       |  <#se | 1>`__ |
|       |       |       |       |       |       |       | ct_9. | 2     |
|       |       |       |       |       |       |       | 8.5.4 | .16.8 |
|       |       |       |       |       |       |       | >`__] | 40.1. |
|       |       |       |       |       |       |       |       | 11388 |
|       |       |       |       |       |       |       |       | 3.​10 |
|       |       |       |       |       |       |       |       | .20.6 |
|       |       |       |       |       |       |       |       | .2.13 |
+-------+-------+-------+-------+-------+-------+-------+-------+-------+
|       | >     | entry | 0..1  | MAY   |       |       |       |       |
+-------+-------+-------+-------+-------+-------+-------+-------+-------+
| *C    | >>    | *ob   | 1..1  | SHALL |       |       | [See  | `     |
| oded​ |       | serva |       |       |       |       | `en   | Coded |
| Obser |       | tion* |       |       |       |       | try/o | Ob    |
| vatio |       |       |       |       |       |       | bserv | serva |
| n​[in |       |       |       |       |       |       | ation | tion  |
| dicat |       |       |       |       |       |       | Indic | <#sec |
| ion]* |       |       |       |       |       |       | ation | t_10. |
|       |       |       |       |       |       |       |  <#se | 1>`__ |
|       |       |       |       |       |       |       | ct_9. | 2     |
|       |       |       |       |       |       |       | 8.5.5 | .16.8 |
|       |       |       |       |       |       |       | >`__] | 40.1. |
|       |       |       |       |       |       |       |       | 11388 |
|       |       |       |       |       |       |       |       | 3.​10 |
|       |       |       |       |       |       |       |       | .20.6 |
|       |       |       |       |       |       |       |       | .2.13 |
+-------+-------+-------+-------+-------+-------+-------+-------+-------+
|       | >     | entry | 0..\* | MAY   |       |       |       |       |
+-------+-------+-------+-------+-------+-------+-------+-------+-------+
| *Quan | >>    | *ob   | 1..1  |       |       |       | [See  | `Qua  |
| tity​ |       | serva |       |       |       |       | `en   | ntity |
| Measu |       | tion* |       |       |       |       | try/o | Me    |
| remen |       |       |       |       |       |       | bserv | asure |
| t[*]* |       |       |       |       |       |       | ation | ment  |
|       |       |       |       |       |       |       | Dose  | <#sec |
|       |       |       |       |       |       |       | Me    | t_10. |
|       |       |       |       |       |       |       | asure | 5>`__ |
|       |       |       |       |       |       |       | ments | 2     |
|       |       |       |       |       |       |       |  <#se | .16.8 |
|       |       |       |       |       |       |       | ct_9. | 40.1. |
|       |       |       |       |       |       |       | 8.5.6 | 11388 |
|       |       |       |       |       |       |       | >`__] | 3.​10 |
|       |       |       |       |       |       |       |       | .20.6 |
|       |       |       |       |       |       |       |       | .2.14 |
+-------+-------+-------+-------+-------+-------+-------+-------+-------+
|       | >     | entry | 0..1  | MAY   |       |       |       |       |
+-------+-------+-------+-------+-------+-------+-------+-------+-------+
|       | >>    | subs  |       |       |       |       |       |       |
|       |       | tance |       |       |       |       |       |       |
|       |       | ​Admi |       |       |       |       |       |       |
|       |       | nistr |       |       |       |       |       |       |
|       |       | ation |       |       |       |       |       |       |
+-------+-------+-------+-------+-------+-------+-------+-------+-------+
|       | >>@   | @clas | 1..1  | SHALL |       | SHALL | SBADM |       |
|       |       | sCode |       |       |       |       |       |       |
+-------+-------+-------+-------+-------+-------+-------+-------+-------+
|       | >>@   | @moo  | 1..1  | SHALL |       | SHALL | EVN   |       |
|       |       | dCode |       |       |       |       |       |       |
+-------+-------+-------+-------+-------+-------+-------+-------+-------+
|       | >>>   | code  | 1..1  |       |       | SHALL | (     |       |
|       |       |       |       |       |       |       | 44025 |       |
|       |       |       |       |       |       |       | 2007, |       |
|       |       |       |       |       |       |       | SN    |       |
|       |       |       |       |       |       |       | OMED, |       |
|       |       |       |       |       |       |       | "Admi |       |
|       |       |       |       |       |       |       | nistr |       |
|       |       |       |       |       |       |       | ation |       |
|       |       |       |       |       |       |       | of    |       |
|       |       |       |       |       |       |       | r     |       |
|       |       |       |       |       |       |       | adiop |       |
|       |       |       |       |       |       |       | harma |       |
|       |       |       |       |       |       |       | ceuti |       |
|       |       |       |       |       |       |       | cal") |       |
+-------+-------+-------+-------+-------+-------+-------+-------+-------+
| Rad   | >>>   | dos   | 0..1  | S     | PQ    |       |       |       |
| ioact |       | e​Qua |       | HOULD |       |       |       |       |
| ivity |       | ntity |       |       |       |       |       |       |
| ​Dose |       |       |       |       |       |       |       |       |
+-------+-------+-------+-------+-------+-------+-------+-------+-------+
|       | >>>   | consu | 1..1  | SHALL |       |       |       |       |
|       |       | mable |       |       |       |       |       |       |
+-------+-------+-------+-------+-------+-------+-------+-------+-------+
|       | >>>>  | manuf | 1..1  | SHALL |       |       |       |       |
|       |       | actur |       |       |       |       |       |       |
|       |       | ed​Pr |       |       |       |       |       |       |
|       |       | oduct |       |       |       |       |       |       |
+-------+-------+-------+-------+-------+-------+-------+-------+-------+
|       | >>>>> | mat   | 1..1  | SHALL |       |       |       |       |
|       |       | erial |       |       |       |       |       |       |
+-------+-------+-------+-------+-------+-------+-------+-------+-------+
| Radio | >     | code  | 1..1  | SHALL | CE    | S     | Val   |       |
| ​phar | >>>>> |       |       |       |       | HOULD | ueSet |       |
| maceu |       |       |       |       |       |       | , or  |       |
| tical |       |       |       |       |       | CWE   |       |       |
+-------+-------+-------+-------+-------+-------+-------+-------+-------+
| Free​ | >>    | ori   | 0..1  | S     | ED    |       |       |       |
| Text​ | >>>>> | ginal |       | HOULD |       |       |       |       |
| Radio |       | Text  |       |       |       |       |       |       |
| ​phar |       |       |       |       |       |       |       |       |
| maceu |       |       |       |       |       |       |       |       |
| tical |       |       |       |       |       |       |       |       |
+-------+-------+-------+-------+-------+-------+-------+-------+-------+

.. _sect_9.8.5.1:

text
^^^^

The section text SHALL contain information related to the radiation
exposure and protection of the patient, as is required by state/national
legal requirements or standards, for example:

-  information on the indications for the procedure

-  the name of the "Irradiation Authorizing" person who is the clinician
   responsible for determining that the irradiating procedure was
   appropriate for the indications.

-  summary information on radiation exposure if ionizing is applied in
   the context of the current procedure (detailed specification of
   exposure is out of the scope of this textual summary).

-  information on the radioactive substance administered if radioactive
   substance is administered in the context of the current procedure.

.. note::

   Compare to .

.. _sect_9.8.5.2:

entry/procedure Patient Exposure
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

COND: If modality is CT, MG, NM, PT, XR, XA, or XF, the section SHOULD
contain a procedure entry for the exposure of the patient to ionizing
radiation.

This entry SHALL have a participant, the irradiation authorizing person
who is the clinician responsible for determining that the irradiating
procedure was appropriate for the indications.

.. note::

   This may be the same person as the performing physician identified in
   the header.

.. _sect_9.8.5.3:

entry/observation SOP Instance
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

The section may include reference to one or more DICOM Dose Report SOP
Instances that provides a detailed record of exposure.

.. _sect_9.8.5.4:

entry/observation Pregnancy
^^^^^^^^^^^^^^^^^^^^^^^^^^^

COND: A coded observation entry SHALL be present if the patient is
female and child-bearing age.

The binding to the Coded Observation concept domains is:

+---------------------------+------------+---------------------------+
| Concept Domain or Element | Value Conf | Value                     |
+===========================+============+===========================+
| Observation​Type          | SHALL      | (364320009, SNOMED,       |
|                           |            | "Pregnancy observable")   |
+---------------------------+------------+---------------------------+
| Observation​Value         | SHALL CNE  | Value​Set                 |
+---------------------------+------------+---------------------------+
| Other concept domains     |            | unspecified               |
+---------------------------+------------+---------------------------+

.. _sect_9.8.5.5:

entry/observation Indication
^^^^^^^^^^^^^^^^^^^^^^^^^^^^

An indication for procedure recorded in this section should be
consistent with any indications identified in the `Clinical
Information <#sect_9.2>`__ and/or `Procedure
Indications <#sect_9.8.2>`__ section. It is included here for
conformance with regulatory requirements in some jurisdictions for the
indications to be specified in the context of the radiation exposure
information.

The binding to the Coded Observation concept domains is:

+---------------------------+------------+---------------------------+
| Concept Domain or Element | Value Conf | Value                     |
+===========================+============+===========================+
| Observation​Type          | SHALL      | (432678004, SNOMED,       |
|                           |            | "Indication for           |
|                           |            | procedure")               |
+---------------------------+------------+---------------------------+
| Other concept domains     |            | unspecified               |
+---------------------------+------------+---------------------------+

.. _sect_9.8.5.6:

entry/observation Dose Measurements
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

The section may include multiple dose measurements. The binding to the
Quantity Measurement concept domains is:

========================= ========== ===========
Concept Domain or Element Value Conf Value
========================= ========== ===========
Observation​Type          SHALL CWE  Value​Set
Other concept domains                unspecified
========================= ========== ===========

::

   <section classCode="DOCSECT" moodCode="EVN">
       <templateId root="1.2.840.10008.9.8" />
       <id root="1.2.840.10213.2.62.704478559484.11428372623"/>
       <code code="73569-6"
           codeSystem="2.16.840.1.113883.6.1"
           codeSystemName="LOINC"
           displayName="Radiation Exposure And Protection Information"/>
       <title> Radiation Exposure and Protection Information</title>
       <text>A dosage of... </text>
       <entry>
           <procedure classCode="PROC" moodCode="EVN">
               <code code="121290"
                   codeSystem="2.16.840.1.113883.6.1"
                   codeSystemName="DCM"
                   displayName="Patient exposure to ionizing radiation"/>
               <participant typeCode="RESP">
                   <participantRole>
                       <id root="2.16.840.1.113883.4.6" extension="980003719"/>
                       <code code="113850"
                           codeSystem="2.16.840.1.113883.6.1"
                           codeSystemName="DCM"
                           displayName="Irradiation Authorizing"/>
                       <playingEntity>
                           <name>
                               <given>Martha</given>
                               <family>Radiologist</family>
                           </name>
                       </playingEntity>
                   </participantRole>
               </participant>
           </procedure>
       </entry>
       <entry>
           <observation classCode="OBS" moodCode="EVN" ID="pregnancy">
               <templateId root="2.16.840.1.113883.10.20.6.2.13"/>
               <id root="1.2.840.10213.2.62.7044779.114265201"/>
               <code code="364320009"
                   codeSystem="2.16.840.1.113883.6.96"
                   codeSystemName="SNOMED CT"
                   displayName="Pregnancy observable"/>
               <statusCode code="completed"/>
               <value xsi:type="CD" code="60001007"
                   codeSystem="2.16.840.1.113883.6.96"
                   codeSystemName="SNOMED CT"
                   displayName="not pregnant"/>
               <effectiveTime value="20140914171504+0500"/>
           </observation>
       </entry>
   </section>

.. _sect_9.8.6:

Key Images
~~~~~~~~~~

+----------------------+----------------------------------------------+
| **ID**               | 1.3.6.1.4.1.19376.​1.4.1.2.14                |
+----------------------+----------------------------------------------+
| **Name**             | Key Images                                   |
+----------------------+----------------------------------------------+
| **Effective Date**   | 2011-07                                      |
+----------------------+----------------------------------------------+
| **Version Label**    | DICOM-20150324                               |
+----------------------+----------------------------------------------+
| **Status**           | Active                                       |
+----------------------+----------------------------------------------+
| **Description**      | The Key Images section contains narrative    |
|                      | description of and references to DICOM Image |
|                      | Information Objects that illustrate the      |
|                      | findings of the procedure reported.          |
+----------------------+----------------------------------------------+
| **Classification**   | CDA Section Level                            |
+----------------------+----------------------------------------------+
| **Relationships**    | Included in `Impression <#sect_9.6>`__       |
+----------------------+----------------------------------------------+
| **Context**          | parent node                                  |
+----------------------+----------------------------------------------+
| **Open/Closed**      | Open                                         |
+----------------------+----------------------------------------------+
| **Revision History** | From IHE Cardiac Imaging Report Content      |
|                      |                                              |
|                      | DICOM-20150324: Addition of optional inline  |
|                      | image (observationMedia)                     |
+----------------------+----------------------------------------------+

+-------+-------+-------+-------+-------+-------+-------+-------+-------+
| **Bus | *     | **    | **C   | *     | *     | **    | **Va  | **    |
| iness | *Nest | Eleme | ard** | *Elem | *Data | Value | lue** | Subsi |
| N     | Le    | nt/​A |       | /Attr | T     | C     |       | diary |
| ame** | vel** | ttrib |       | C     | ype** | onf** |       | Templ |
|       |       | ute** |       | onf** |       |       |       | ate** |
+-------+-------+-------+-------+-------+-------+-------+-------+-------+
| **Ke  |       | se    | 1..1  | SHALL |       |       |       |       |
| y​Ima |       | ction |       |       |       |       |       |       |
| ges** |       |       |       |       |       |       |       |       |
+-------+-------+-------+-------+-------+-------+-------+-------+-------+
|       | >     | t     | 1..1  | SHALL | II    |       |       |       |
|       |       | empla |       |       |       |       |       |       |
|       |       | te​Id |       |       |       |       |       |       |
+-------+-------+-------+-------+-------+-------+-------+-------+-------+
|       | >@    | @root | 1..1  | SHALL | UID   | SHALL | 1.3.  |       |
|       |       |       |       |       |       |       | 6.1.4 |       |
|       |       |       |       |       |       |       | .1.19 |       |
|       |       |       |       |       |       |       | 376.​ |       |
|       |       |       |       |       |       |       | 1.4.1 |       |
|       |       |       |       |       |       |       | .2.14 |       |
+-------+-------+-------+-------+-------+-------+-------+-------+-------+
|       | >     | id    | 1..\* | SHALL | II    |       |       |       |
+-------+-------+-------+-------+-------+-------+-------+-------+-------+
|       | >     | code  | 1..1  | SHALL | CD    | SHALL | `(551 |       |
|       |       |       |       |       |       |       | 13-5, |       |
|       |       |       |       |       |       |       | L     |       |
|       |       |       |       |       |       |       | OINC, |       |
|       |       |       |       |       |       |       | "Key  |       |
|       |       |       |       |       |       |       | Imag  |       |
|       |       |       |       |       |       |       | es")  |       |
|       |       |       |       |       |       |       | <http |       |
|       |       |       |       |       |       |       | ://lo |       |
|       |       |       |       |       |       |       | inc.o |       |
|       |       |       |       |       |       |       | rg/55 |       |
|       |       |       |       |       |       |       | 113-5 |       |
|       |       |       |       |       |       |       | />`__ |       |
+-------+-------+-------+-------+-------+-------+-------+-------+-------+
| Title | >     | title | 1..1  | SHALL | ST    |       |       |       |
+-------+-------+-------+-------+-------+-------+-------+-------+-------+
| *     | *>*   | *     | 1..1  | COND  | ED    |       |       | `Se   |
| Text* |       | text* |       |       |       |       |       | ction |
|       |       |       |       |       |       |       |       | T     |
|       |       |       |       |       |       |       |       | ext < |
|       |       |       |       |       |       |       |       | #sect |
|       |       |       |       |       |       |       |       | _9.1. |
|       |       |       |       |       |       |       |       | 1>`__ |
|       |       |       |       |       |       |       |       | 1.2   |
|       |       |       |       |       |       |       |       | .840. |
|       |       |       |       |       |       |       |       | 10008 |
|       |       |       |       |       |       |       |       | .9.19 |
+-------+-------+-------+-------+-------+-------+-------+-------+-------+
|       | >     | entry | 0..\* | S     |       |       |       |       |
|       |       |       |       | HOULD |       |       |       |       |
+-------+-------+-------+-------+-------+-------+-------+-------+-------+
| *     | *>>*  | *ob   | 1..1  | SHALL |       |       |       |       |
| SOPIn |       | serva |       |       |       |       |       |       |
| stanc |       | tion* |       |       |       |       |       |       |
| e[*]* |       |       |       |       |       |       |       |       |
+-------+-------+-------+-------+-------+-------+-------+-------+-------+
|       | >     | entry | 0..\* | MAY   |       |       |       |       |
+-------+-------+-------+-------+-------+-------+-------+-------+-------+
| *G    | *>>*  | *obs  | 1..1  | SHALL |       |       |       | `ob   |
| raphi |       | ervat |       |       |       |       |       | serva |
| c[*]* |       | ion​M |       |       |       |       |       | tionM |
|       |       | edia* |       |       |       |       |       | edia  |
|       |       |       |       |       |       |       |       | <#sec |
|       |       |       |       |       |       |       |       | t_10. |
|       |       |       |       |       |       |       |       | 3>`__ |
|       |       |       |       |       |       |       |       | 1.3   |
|       |       |       |       |       |       |       |       | .6.1. |
|       |       |       |       |       |       |       |       | 4.1.1 |
|       |       |       |       |       |       |       |       | 9376. |
|       |       |       |       |       |       |       |       | ​1.4. |
|       |       |       |       |       |       |       |       | 1.4.7 |
+-------+-------+-------+-------+-------+-------+-------+-------+-------+

.. _sect_9.8.6.1:

Section/text
^^^^^^^^^^^^

The Key Images section text SHALL contain image references using
linkHtml elements, where @href is a valid Web Access to DICOM Persistent
Object (WADO) URL. See `<linkHtml> Markup and Image
References <#sect_9.1.1.5>`__. The text content of linkHtml should be
either visible text of the hyperlink, or a descriptor or identifier of
the image; it may be associated with a (limited resolution) copy of the
image (see `observationMedia <#sect_9.8.6.3>`__).

.. _sect_9.8.6.2:

SOP Instance Observation
^^^^^^^^^^^^^^^^^^^^^^^^

The Key Images section SHOULD include `SOP Instance
Observation <#sect_10.8>`__ entries equivalent to the linkHtml image
references.

.. _sect_9.8.6.3:

observationMedia
^^^^^^^^^^^^^^^^

The Key Images section MAY include observationMedia entries with in-line
encoded copies of the referenced images, linked into the narrative block
using the renderMultiMedia markup. See `<renderMultiMedia> Markup and
Graphical Content <#sect_9.1.1.3>`__. These in-line encoded images may
have limited resolution and lossy compression as appropriate for
inclusion in a report.

::

   <section classCode="DOCSECT" moodCode="EVN">>
       <templateId root="1.3.6.1.4.1.19376.1.4.1.2.14" />
       <id root="1.2.840.10213.2.62.704478559484.11428372623" />
       <code code="55113-5"
           codeSystem="2.16.840.1.113883.6.1"
           codeSystemName="LOINC"
           displayName="Key Images"/>
       <title>Key Images</title>
       <text>Maximum extent of tumor is shown in
           <linkHtml href="http://www.example.org/wado?requestType=WADO&amp;...">image 1</linkHtml>
           <renderMultiMedia referencedObject="refimag1"/>
       </text>
       <entry>
           <!-- SOP Instance reference -->
           <observation classCode=DGIMG moodCode=EVN ID="SOP1-2"/>
       </entry>
       <entry>
           <!-- inline rendered image -->
           <observationMedia ID="refimag1">
               <value representation=B64 mediaType="image/jpeg">
                   Bgd3fsET4g...
               </value>
           </observationMedia>
       </entry>
   </section>

.. _sect_9.8.7:

DICOM Object Catalog
~~~~~~~~~~~~~~~~~~~~

+----------------------+----------------------------------------------+
| **Template ID**      | 2.16.840.1.113883.​10.20.6.1.1               |
+----------------------+----------------------------------------------+
| **Name**             | DICOM Object Catalog Section                 |
+----------------------+----------------------------------------------+
| **Effective Date**   | 2012-07                                      |
+----------------------+----------------------------------------------+
| **Version Label**    | CCDA-1.1                                     |
+----------------------+----------------------------------------------+
| **Status**           | Active                                       |
+----------------------+----------------------------------------------+
| **Description**      | DICOM Object Catalog lists all referenced    |
|                      | objects and their parent Series and Studies, |
|                      | plus other DICOM attributes required for     |
|                      | retrieving the objects. The DICOM Object     |
|                      | Catalog section is not intended for viewing  |
|                      | and may contain empty section text.          |
+----------------------+----------------------------------------------+
| **Classification**   | CDA Section Level                            |
+----------------------+----------------------------------------------+
| **Relationships**    | Included in `Imaging Procedure               |
|                      | Description <#sect_9.3>`__                   |
+----------------------+----------------------------------------------+
| **Context**          | parent node                                  |
+----------------------+----------------------------------------------+
| **Open/Closed**      | Open                                         |
+----------------------+----------------------------------------------+
| **Revision History** | From Consolidated CDA r1.1                   |
+----------------------+----------------------------------------------+

+-------+-------+-------+-------+-------+-------+-------+-------+-------+
| **Bus | *     | **    | **C   | *     | *     | **    | **Va  | **    |
| iness | *Nest | Eleme | ard** | *Elem | *Data | Value | lue** | Subsi |
| N     | Le    | nt/​A |       | /Attr | T     | C     |       | diary |
| ame** | vel** | ttrib |       | C     | ype** | onf** |       | Templ |
|       |       | ute** |       | onf** |       |       |       | ate** |
+-------+-------+-------+-------+-------+-------+-------+-------+-------+
| *     |       | se    | 1..1  | SHALL |       |       |       |       |
| *DICO |       | ction |       |       |       |       |       |       |
| MCata |       |       |       |       |       |       |       |       |
| log** |       |       |       |       |       |       |       |       |
+-------+-------+-------+-------+-------+-------+-------+-------+-------+
|       | >     | t     | 1..1  | SHALL | II    |       |       |       |
|       |       | empla |       |       |       |       |       |       |
|       |       | te​Id |       |       |       |       |       |       |
+-------+-------+-------+-------+-------+-------+-------+-------+-------+
|       | >@    | @root | 1..1  | SHALL | UID   | SHALL | 2.16. |       |
|       |       |       |       |       |       |       | 840.1 |       |
|       |       |       |       |       |       |       | .1138 |       |
|       |       |       |       |       |       |       | 83.​1 |       |
|       |       |       |       |       |       |       | 0.20. |       |
|       |       |       |       |       |       |       | 6.1.1 |       |
+-------+-------+-------+-------+-------+-------+-------+-------+-------+
|       | >     | id    | 1..\* | SHALL | II    |       |       |       |
+-------+-------+-------+-------+-------+-------+-------+-------+-------+
|       | >     | code  | 1..1  | SHALL | CD    | SHALL | (12   |       |
|       |       |       |       |       |       |       | 1181, |       |
|       |       |       |       |       |       |       | DCM,  |       |
|       |       |       |       |       |       |       | "     |       |
|       |       |       |       |       |       |       | Dicom |       |
|       |       |       |       |       |       |       | O     |       |
|       |       |       |       |       |       |       | bject |       |
|       |       |       |       |       |       |       | Cata  |       |
|       |       |       |       |       |       |       | log") |       |
+-------+-------+-------+-------+-------+-------+-------+-------+-------+
| Title | >     | title | 1..1  | SHALL | ST    |       |       |       |
+-------+-------+-------+-------+-------+-------+-------+-------+-------+
| *     | *>*   | *     | 1..1  | SHALL | ED    |       |       | `Se   |
| Text* |       | text* |       |       |       |       |       | ction |
|       |       |       |       |       |       |       |       | T     |
|       |       |       |       |       |       |       |       | ext < |
|       |       |       |       |       |       |       |       | #sect |
|       |       |       |       |       |       |       |       | _9.1. |
|       |       |       |       |       |       |       |       | 1>`__ |
|       |       |       |       |       |       |       |       | 1.2   |
|       |       |       |       |       |       |       |       | .840. |
|       |       |       |       |       |       |       |       | 10008 |
|       |       |       |       |       |       |       |       | .9.19 |
+-------+-------+-------+-------+-------+-------+-------+-------+-------+
|       | >     | entry | 0..\* | S     |       |       |       |       |
|       |       |       |       | HOULD |       |       |       |       |
+-------+-------+-------+-------+-------+-------+-------+-------+-------+
| *Stud | >>    | *act* | 1..1  | SHALL |       |       |       | `     |
| y[*]* |       |       |       |       |       |       |       | Study |
|       |       |       |       |       |       |       |       | Act   |
|       |       |       |       |       |       |       |       | <#sec |
|       |       |       |       |       |       |       |       | t_10. |
|       |       |       |       |       |       |       |       | 6>`__ |
|       |       |       |       |       |       |       |       | 2.16. |
|       |       |       |       |       |       |       |       | 840.1 |
|       |       |       |       |       |       |       |       | .1138 |
|       |       |       |       |       |       |       |       | 83.​1 |
|       |       |       |       |       |       |       |       | 0.20. |
|       |       |       |       |       |       |       |       | 6.2.6 |
+-------+-------+-------+-------+-------+-------+-------+-------+-------+

::

   <section classCode="DOCSECT" moodCode="EVN">
       <templateId root="2.16.840.1.113883.10.20.6.1.1"/>
       <id root="1.2.840.10213.2.62.70447834679.11429737"/>
       <code code="121181"
           codeSystem="1.2.840.10008.2.16.4"
           codeSystemName="DCM"
           displayName="DICOM Object Catalog"/>
       <entry>
           <!-- **** Study Act **** -->
           <act classCode="ACT" moodCode="EVN">
               <templateId root="2.16.840.1.113883.10.20.6.2.6"/>
               <id root="1.2.840.113619.2.62.994044785528.114289542805"/>
               <code code="113014" codeSystem="1.2.840.10008.2.16.4"
                   codeSystemName="DCM" displayName="Study"/>
               <!-- **** Series Act ****-->
               <entryRelationship typeCode="COMP">
                   <act classCode="ACT" moodCode="EVN">
                       <id root="1.2.840.113619.2.62.994044785528.20060823223142485051"/>
                       <code code="113015" codeSystem="1.2.840.10008.2.16.4"
                           codeSystemName="DCM" displayName="Series">
                           ...
                       </code>
                       <!-- **** SOP Instance UID *** -->
                       <!-- 2 References -->
                       <entryRelationship typeCode="COMP">
                           <observation classCode="DGIMG" moodCode="EVN">
                               <templateId root="2.16.840.1.113883.10.20.6.2.8"/>
                               ...
                           </observation>
                       </entryRelationship>
                       <entryRelationship typeCode="COMP">
                           <observation classCode="DGIMG" moodCode="EVN">
                               <templateId root="2.16.840.1.113883.10.20.6.2.8"/>
                               ...
                           </observation>
                       </entryRelationship>
                   </act>
               </entryRelationship>
           </act>
       </entry>

.. _sect_9.8.8:

Fetus Findings
~~~~~~~~~~~~~~

+----------------------+----------------------------------------------+
| **Template ID**      | 1.2.840.10008.9.9                            |
+----------------------+----------------------------------------------+
| **Name**             | Fetus Findings                               |
+----------------------+----------------------------------------------+
| **Effective Date**   | 2015/03/24                                   |
+----------------------+----------------------------------------------+
| **Version Label**    | DICOM-20150324                               |
+----------------------+----------------------------------------------+
| **Status**           | Active                                       |
+----------------------+----------------------------------------------+
| **Description**      | Records observations related to a fetus      |
|                      | confirmed or discovered during an imaging    |
|                      | procedure.                                   |
+----------------------+----------------------------------------------+
| **Classification**   | CDA Section Level                            |
+----------------------+----------------------------------------------+
| **Relationships**    | Included in `Findings <#sect_9.5>`__         |
+----------------------+----------------------------------------------+
| **Context**          | parent node                                  |
+----------------------+----------------------------------------------+
| **Open/Closed**      | Open                                         |
+----------------------+----------------------------------------------+
| **Revision History** | DICOM-20150324: Initial version              |
+----------------------+----------------------------------------------+

+-------+-------+-------+-------+-------+-------+-------+-------+-------+
| **Bus | *     | **    | **C   | *     | *     | **    | **Va  | **    |
| iness | *Nest | Eleme | ard** | *Elem | *Data | Value | lue** | Subsi |
| N     | Le    | nt/​A |       | /Attr | T     | C     |       | diary |
| ame** | vel** | ttrib |       | C     | ype** | onf** |       | Templ |
|       |       | ute** |       | onf** |       |       |       | ate** |
+-------+-------+-------+-------+-------+-------+-------+-------+-------+
| *     |       | se    | 1..1  | SHALL |       |       |       |       |
| *Fetu |       | ction |       |       |       |       |       |       |
| s​Fin |       |       |       |       |       |       |       |       |
| dings |       |       |       |       |       |       |       |       |
| [*]** |       |       |       |       |       |       |       |       |
+-------+-------+-------+-------+-------+-------+-------+-------+-------+
|       | >     | t     | 1..1  | SHALL | II    |       |       |       |
|       |       | empla |       |       |       |       |       |       |
|       |       | te​Id |       |       |       |       |       |       |
+-------+-------+-------+-------+-------+-------+-------+-------+-------+
|       | >@    | @root | 1..1  | SHALL | UID   | SHALL | 1.    |       |
|       |       |       |       |       |       |       | 2.840 |       |
|       |       |       |       |       |       |       | .1000 |       |
|       |       |       |       |       |       |       | 8.9.9 |       |
+-------+-------+-------+-------+-------+-------+-------+-------+-------+
|       | >     | id    | 1..\* | SHALL | II    |       |       |       |
+-------+-------+-------+-------+-------+-------+-------+-------+-------+
|       | >     | code  | 1..1  | SHALL | CD    | SHALL | `(765 |       |
|       |       |       |       |       |       |       | 14-9, |       |
|       |       |       |       |       |       |       | L     |       |
|       |       |       |       |       |       |       | OINC, |       |
|       |       |       |       |       |       |       | "     |       |
|       |       |       |       |       |       |       | Fetal |       |
|       |       |       |       |       |       |       | Study |       |
|       |       |       |       |       |       |       | obse  |       |
|       |       |       |       |       |       |       | rvati |       |
|       |       |       |       |       |       |       | on")  |       |
|       |       |       |       |       |       |       | <http |       |
|       |       |       |       |       |       |       | ://lo |       |
|       |       |       |       |       |       |       | inc.o |       |
|       |       |       |       |       |       |       | rg/76 |       |
|       |       |       |       |       |       |       | 514-9 |       |
|       |       |       |       |       |       |       | />`__ |       |
+-------+-------+-------+-------+-------+-------+-------+-------+-------+
| Title | >     | title | 1..1  | SHALL | ST    |       |       |       |
+-------+-------+-------+-------+-------+-------+-------+-------+-------+
| *     | *>*   | *     | 1..1  | COND  | ED    |       |       | `Se   |
| Text* |       | text* |       |       |       |       |       | ction |
|       |       |       |       |       |       |       |       | T     |
|       |       |       |       |       |       |       |       | ext < |
|       |       |       |       |       |       |       |       | #sect |
|       |       |       |       |       |       |       |       | _9.1. |
|       |       |       |       |       |       |       |       | 1>`__ |
|       |       |       |       |       |       |       |       | 1.2   |
|       |       |       |       |       |       |       |       | .840. |
|       |       |       |       |       |       |       |       | 10008 |
|       |       |       |       |       |       |       |       | .9.19 |
+-------+-------+-------+-------+-------+-------+-------+-------+-------+
|       | >     | su    | 1..1  | SHALL |       |       |       |       |
|       |       | bject |       |       |       |       |       |       |
+-------+-------+-------+-------+-------+-------+-------+-------+-------+
|       | >>    | relat | 1..1  | SHALL |       |       |       |       |
|       |       | ed​Su |       |       |       |       |       |       |
|       |       | bject |       |       |       |       |       |       |
+-------+-------+-------+-------+-------+-------+-------+-------+-------+
|       | >>>   | code  | 1..1  | SHALL | CE    | SHALL | (12   |       |
|       |       |       |       |       |       |       | 1026, |       |
|       |       |       |       |       |       |       | DCM,  |       |
|       |       |       |       |       |       |       | "Fe   |       |
|       |       |       |       |       |       |       | tus") |       |
+-------+-------+-------+-------+-------+-------+-------+-------+-------+
|       | >>>   | su    | 1..1  | SHALL |       |       |       |       |
|       |       | bject |       |       |       |       |       |       |
+-------+-------+-------+-------+-------+-------+-------+-------+-------+
| Fet   | >>>>  | name  | 1..1  | SHALL | PN    |       |       |       |
| us​ID |       |       |       |       |       |       |       |       |
+-------+-------+-------+-------+-------+-------+-------+-------+-------+
|       | >     | comp  | 0..\* | MAY   |       |       |       |       |
|       |       | onent |       |       |       |       |       |       |
+-------+-------+-------+-------+-------+-------+-------+-------+-------+
| *Subs | >>    | *sec  | 1..1  | SHALL |       |       |       | `La   |
| ectio |       | tion* |       |       |       |       |       | beled |
| n[*]* |       |       |       |       |       |       |       | Su    |
|       |       |       |       |       |       |       |       | bsect |
|       |       |       |       |       |       |       |       | ion < |
|       |       |       |       |       |       |       |       | #sect |
|       |       |       |       |       |       |       |       | _9.8. |
|       |       |       |       |       |       |       |       | 9>`__ |
|       |       |       |       |       |       |       |       | 1.2   |
|       |       |       |       |       |       |       |       | .840. |
|       |       |       |       |       |       |       |       | 10008 |
|       |       |       |       |       |       |       |       | .9.10 |
+-------+-------+-------+-------+-------+-------+-------+-------+-------+
|       | >     |       | 0.1   | MAY   |       |       |       | `Ge   |
|       |       |       |       |       |       |       |       | neral |
|       |       |       |       |       |       |       |       | Se    |
|       |       |       |       |       |       |       |       | ction |
|       |       |       |       |       |       |       |       | Entr  |
|       |       |       |       |       |       |       |       | ies < |
|       |       |       |       |       |       |       |       | #sect |
|       |       |       |       |       |       |       |       | _9.1. |
|       |       |       |       |       |       |       |       | 2>`__ |
|       |       |       |       |       |       |       |       | 1.2   |
|       |       |       |       |       |       |       |       | .840. |
|       |       |       |       |       |       |       |       | 10008 |
|       |       |       |       |       |       |       |       | .9.23 |
+-------+-------+-------+-------+-------+-------+-------+-------+-------+

For reports on mothers and their fetus(es), information on a mother is
mapped to recordTarget/PatientRole/Patient in the CDA header.
Information on the fetus is mapped to
subject/relatedSubject/SubjectPerson at the CDA section level. Both
context information on the mother and fetus must be included in the
document if observations on fetus(es) are contained in the document.

.. _sect_9.8.8.1:

name - FetusID
^^^^^^^^^^^^^^

The subject/relatedSubject/subject/name element is used to store the
fetus ID, typically a pseudonym such as "fetus A". This shall be present
even if only one fetus is identified in the document.

::

   <section classCode="DOCSECT" moodCode="EVN">
       <templateId root="2.16.840.1.113883.10.20.22.2.27" />
       <id root="1.2.840.10213.2.62.70447834679.11429737"/>
       <code code="76514-9" codeSystem="2.16.840.1.113883.6.1"
           codeSystemName="LOINC" displayName="Fetal Study observation" />
       <title>Fetus #1</title>
       <text>Estimated gestational age of 27 weeks... </text>
       <relatedSubject>
           <code code="121026" codeSystem="1.2.840.10008.2.16.4" displayName="Fetus"/>
           <subject>
               <name>Fetus 1</name>
           </subject>
       </relatedSubject>
   </section>

.. _sect_9.8.9:

Labeled Subsection
~~~~~~~~~~~~~~~~~~

+----------------------+----------------------------------------------+
| **Template ID**      | 1.2.840.10008.9.10                           |
+----------------------+----------------------------------------------+
| **Name**             | Labeled Subsection                           |
+----------------------+----------------------------------------------+
| **Effective Date**   | 2015/03/24                                   |
+----------------------+----------------------------------------------+
| **Version Label**    | DICOM-20150324                               |
+----------------------+----------------------------------------------+
| **Status**           | Active                                       |
+----------------------+----------------------------------------------+
| **Description**      | Narrative or coded subsection that allows    |
|                      | organization of content for a labeled topic  |
|                      | (a particular organ or anatomic feature, a   |
|                      | lesion, a tumor, etc.). The section.code     |
|                      | shall be absent, but the section.title shall |
|                      | be present.                                  |
+----------------------+----------------------------------------------+
| **Classification**   | CDA Section Level                            |
+----------------------+----------------------------------------------+
| **Relationships**    | Included in `Findings <#sect_9.5>`__         |
+----------------------+----------------------------------------------+
| **Context**          | parent node                                  |
+----------------------+----------------------------------------------+
| **Open/Closed**      | Open                                         |
+----------------------+----------------------------------------------+
| **Revision History** | DICOM-20150324: Initial version              |
+----------------------+----------------------------------------------+

+-------+-------+-------+-------+-------+-------+-------+-------+-------+
| **Bus | *     | **    | **C   | *     | *     | **    | **Va  | **    |
| iness | *Nest | Eleme | ard** | *Elem | *Data | Value | lue** | Subsi |
| N     | Le    | nt/​A |       | /Attr | T     | C     |       | diary |
| ame** | vel** | ttrib |       | C     | ype** | onf** |       | Templ |
|       |       | ute** |       | onf** |       |       |       | ate** |
+-------+-------+-------+-------+-------+-------+-------+-------+-------+
| **    |       | se    | 1..1  | SHALL |       |       |       |       |
| Subse |       | ction |       |       |       |       |       |       |
| ction |       |       |       |       |       |       |       |       |
| [*]** |       |       |       |       |       |       |       |       |
+-------+-------+-------+-------+-------+-------+-------+-------+-------+
|       | >     | t     | 1..1  | SHALL | II    |       |       |       |
|       |       | empla |       |       |       |       |       |       |
|       |       | te​Id |       |       |       |       |       |       |
+-------+-------+-------+-------+-------+-------+-------+-------+-------+
|       | >@    | @root | 1..1  | SHALL | UID   | SHALL | 1.2   |       |
|       |       |       |       |       |       |       | .840. |       |
|       |       |       |       |       |       |       | 10008 |       |
|       |       |       |       |       |       |       | .9.10 |       |
+-------+-------+-------+-------+-------+-------+-------+-------+-------+
|       | >     | id    | 1..\* | SHALL | II    |       |       |       |
+-------+-------+-------+-------+-------+-------+-------+-------+-------+
|       | >     | code  | 0..0  | SHALL |       |       |       |       |
|       |       |       |       | NOT   |       |       |       |       |
+-------+-------+-------+-------+-------+-------+-------+-------+-------+
| Title | >     | title | 1..1  | SHALL | ST    |       | [See  |       |
|       |       |       |       |       |       |       | `     |       |
|       |       |       |       | no    |       |       | title |       |
|       |       |       |       | ​Null |       |       |  <#se |       |
|       |       |       |       |       |       |       | ct_9. |       |
|       |       |       |       |       |       |       | 8.9.1 |       |
|       |       |       |       |       |       |       | >`__] |       |
+-------+-------+-------+-------+-------+-------+-------+-------+-------+
| *     | *>*   | *     | 1..1  | COND  | ED    |       |       | `Se   |
| Text* |       | text* |       |       |       |       |       | ction |
|       |       |       |       |       |       |       |       | T     |
|       |       |       |       |       |       |       |       | ext < |
|       |       |       |       |       |       |       |       | #sect |
|       |       |       |       |       |       |       |       | _9.1. |
|       |       |       |       |       |       |       |       | 1>`__ |
|       |       |       |       |       |       |       |       | 1.2   |
|       |       |       |       |       |       |       |       | .840. |
|       |       |       |       |       |       |       |       | 10008 |
|       |       |       |       |       |       |       |       | .9.19 |
+-------+-------+-------+-------+-------+-------+-------+-------+-------+
|       | >     | comp  | 0..\* | MAY   |       |       |       |       |
|       |       | onent |       |       |       |       |       |       |
+-------+-------+-------+-------+-------+-------+-------+-------+-------+
| *Subs | >>    | *sec  | 1..1  | SHALL |       |       |       | `La   |
| ectio |       | tion* |       |       |       |       |       | beled |
| n[*]* |       |       |       |       |       |       |       | Su    |
|       |       |       |       |       |       |       |       | bsect |
|       |       |       |       |       |       |       |       | ion < |
|       |       |       |       |       |       |       |       | #sect |
|       |       |       |       |       |       |       |       | _9.8. |
|       |       |       |       |       |       |       |       | 9>`__ |
|       |       |       |       |       |       |       |       | 1.2   |
|       |       |       |       |       |       |       |       | .840. |
|       |       |       |       |       |       |       |       | 10008 |
|       |       |       |       |       |       |       |       | .9.10 |
+-------+-------+-------+-------+-------+-------+-------+-------+-------+
|       | >     |       | 0..1  | MAY   |       |       |       | `Ge   |
|       |       |       |       |       |       |       |       | neral |
|       |       |       |       |       |       |       |       | Se    |
|       |       |       |       |       |       |       |       | ction |
|       |       |       |       |       |       |       |       | Entr  |
|       |       |       |       |       |       |       |       | ies < |
|       |       |       |       |       |       |       |       | #sect |
|       |       |       |       |       |       |       |       | _9.1. |
|       |       |       |       |       |       |       |       | 2>`__ |
|       |       |       |       |       |       |       |       | 1.2   |
|       |       |       |       |       |       |       |       | .840. |
|       |       |       |       |       |       |       |       | 10008 |
|       |       |       |       |       |       |       |       | .9.23 |
+-------+-------+-------+-------+-------+-------+-------+-------+-------+

.. _sect_9.8.9.1:

title
^^^^^

The title element is used to identify the topic (specific organ or
anatomic feature, abnormality, lesion, etc.) as the subject of the
sub-section findings in the human readable document. As there is no
section.code, this is the required mechanism to represent the section
purpose as free text.

.. _sect_9.8.9.2:

component/section Labeled Subsection
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

This template invokes itself recursively to allow arbitrarily deep
nested subsections.

::

   <section classCode="DOCSECT" moodCode="EVN">
       <templateId root="1.2.840.10008.9.10" />
       <id root="1.2.840.10213.2.62.7044794679.114296787"/>
       <title>Liver</title>
       <text>No evidence of cirrhosis, nodular regeneration, or ... </text>
   </section>

.. _sect_9.8.10:

Communication of Actionable Findings
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

+----------------------+----------------------------------------------+
| **Template ID**      | 1.2.840.10008.9.11                           |
+----------------------+----------------------------------------------+
| **Name**             | Communication of Actionable Findings         |
+----------------------+----------------------------------------------+
| **Effective Date**   | 2015/03/24                                   |
+----------------------+----------------------------------------------+
| **Version Label**    | DICOM-20150324                               |
+----------------------+----------------------------------------------+
| **Status**           | Active                                       |
+----------------------+----------------------------------------------+
| **Description**      | A section that documents the notification of |
|                      | an actionable finding to a provider or other |
|                      | person responsible for patient care. The     |
|                      | documentation in narrative text, and         |
|                      | optionally in a coded entry, includes by     |
|                      | whom, to whom, and at what date/time.        |
|                      |                                              |
|                      | Specific findings, including actionable      |
|                      | (aka. critical) findings documented in text  |
|                      | or as coded entries, are typically found in  |
|                      | the `Findings <#sect_9.5>`__. The actionable |
|                      | findings may be duplicated in the            |
|                      | `Impression <#sect_9.6>`__ in either text or |
|                      | as coded entries. The actionable findings    |
|                      | may be new (critical) or a change to a       |
|                      | previous report/diagnosis (discrepant).      |
+----------------------+----------------------------------------------+
| **Classification**   | CDA Section and Entry Level                  |
+----------------------+----------------------------------------------+
| **Relationships**    | Included in `Impression <#sect_9.6>`__ and   |
|                      | `Addendum <#sect_9.7>`__                     |
+----------------------+----------------------------------------------+
| **Context**          | parent node                                  |
+----------------------+----------------------------------------------+
| **Open/Closed**      | Open                                         |
+----------------------+----------------------------------------------+
| **Revision History** | DICOM-20150324: Initial version              |
+----------------------+----------------------------------------------+

+-------+-------+-------+-------+-------+-------+-------+-------+-------+
| **Bus | *     | **    | **C   | *     | *     | **    | **Va  | **    |
| iness | *Nest | Eleme | ard** | *Elem | *Data | Value | lue** | Subsi |
| N     | Le    | nt/​A |       | /Attr | T     | C     |       | diary |
| ame** | vel** | ttrib |       | C     | ype** | onf** |       | Templ |
|       |       | ute** |       | onf** |       |       |       | ate** |
+-------+-------+-------+-------+-------+-------+-------+-------+-------+
| **A   |       | se    | 1..1  | SHALL |       |       |       |       |
| ction |       | ction |       |       |       |       |       |       |
| able​ |       |       |       |       |       |       |       |       |
| Findi |       |       |       |       |       |       |       |       |
| ngs** |       |       |       |       |       |       |       |       |
+-------+-------+-------+-------+-------+-------+-------+-------+-------+
|       | >     | t     | 1..1  | SHALL | II    |       |       |       |
|       |       | empla |       |       |       |       |       |       |
|       |       | te​Id |       |       |       |       |       |       |
+-------+-------+-------+-------+-------+-------+-------+-------+-------+
|       | >@    | @root | 1..1  | SHALL | UID   | SHALL | 1.2   |       |
|       |       |       |       |       |       |       | .840. |       |
|       |       |       |       |       |       |       | 10008 |       |
|       |       |       |       |       |       |       | .9.11 |       |
+-------+-------+-------+-------+-------+-------+-------+-------+-------+
|       | >     | id    | 1..\* | SHALL | II    |       |       |       |
+-------+-------+-------+-------+-------+-------+-------+-------+-------+
|       | >     | code  | 1..1  | SHALL | CD    | SHALL | `(735 |       |
|       |       |       |       |       |       |       | 68-8, |       |
|       |       |       |       |       |       |       | L     |       |
|       |       |       |       |       |       |       | OINC, |       |
|       |       |       |       |       |       |       | "Com  |       |
|       |       |       |       |       |       |       | munic |       |
|       |       |       |       |       |       |       | ation |       |
|       |       |       |       |       |       |       | of    |       |
|       |       |       |       |       |       |       | Cri   |       |
|       |       |       |       |       |       |       | tical |       |
|       |       |       |       |       |       |       | Resul |       |
|       |       |       |       |       |       |       | ts")  |       |
|       |       |       |       |       |       |       | <http |       |
|       |       |       |       |       |       |       | ://lo |       |
|       |       |       |       |       |       |       | inc.o |       |
|       |       |       |       |       |       |       | rg/73 |       |
|       |       |       |       |       |       |       | 568-8 |       |
|       |       |       |       |       |       |       | />`__ |       |
+-------+-------+-------+-------+-------+-------+-------+-------+-------+
| Title | >     | title | 1..1  | SHALL | ST    |       |       |       |
+-------+-------+-------+-------+-------+-------+-------+-------+-------+
|       | >     | text  | 1..1  | SHALL | ED    |       |       |       |
+-------+-------+-------+-------+-------+-------+-------+-------+-------+
| **Co  | >>    | co    | 0..\* | SHALL | ST    |       | [See  |       |
| ntent |       | ntent |       |       |       |       | `     |       |
| [*]** |       |       |       |       |       |       | secti |       |
|       |       |       |       |       |       |       | on/te |       |
|       |       |       |       |       |       |       | xt/co |       |
|       |       |       |       |       |       |       | ntent |       |
|       |       |       |       |       |       |       | -     |       |
|       |       |       |       |       |       |       | narra |       |
|       |       |       |       |       |       |       | tive  |       |
|       |       |       |       |       |       |       | <#sec |       |
|       |       |       |       |       |       |       | t_9.8 |       |
|       |       |       |       |       |       |       | .10.1 |       |
|       |       |       |       |       |       |       | >`__] |       |
+-------+-------+-------+-------+-------+-------+-------+-------+-------+
| *     | >>@   | @ID   | 1..1  | SHALL | XML   |       |       |       |
| *\*** |       |       |       |       | ID    |       |       |       |
+-------+-------+-------+-------+-------+-------+-------+-------+-------+
| F     | >>>   | link  | 0..\* | MAY   | ST    |       |       |       |
| indin |       | ​Html |       |       |       |       |       |       |
| g​Ref |       |       |       |       |       |       |       |       |
+-------+-------+-------+-------+-------+-------+-------+-------+-------+
| F     | >>>@  | @href | 1..1  | SHALL | URL   |       | *#f   |       |
| indin |       |       |       |       | (XML  |       | indin |       |
| g​URI |       |       |       |       | I     |       | gRef* |       |
|       |       |       |       |       | DREF) |       |       |       |
+-------+-------+-------+-------+-------+-------+-------+-------+-------+
|       | >     | entry | 0..\* | S     |       |       |       |       |
|       |       |       |       | HOULD |       |       |       |       |
+-------+-------+-------+-------+-------+-------+-------+-------+-------+
| **Com | >>    | act   | 1..1  | SHALL |       | SHALL |       |       |
| munic |       |       |       |       |       |       |       |       |
| ation |       |       |       |       |       |       |       |       |
| [*]** |       |       |       |       |       |       |       |       |
+-------+-------+-------+-------+-------+-------+-------+-------+-------+
|       | >>@   | @clas | 1..1  | SHALL | CS    | SHALL | ACT   |       |
|       |       | sCode |       |       |       |       |       |       |
+-------+-------+-------+-------+-------+-------+-------+-------+-------+
|       | >>@   | @moo  | 1..1  | SHALL | CS    | SHALL | EVN   |       |
|       |       | dCode |       |       |       |       |       |       |
+-------+-------+-------+-------+-------+-------+-------+-------+-------+
| *     | >>@   | @ID   | 1..1  | SHALL | XML   |       |       |       |
| *\*** |       |       |       |       | ID    |       |       |       |
+-------+-------+-------+-------+-------+-------+-------+-------+-------+
|       | >>>   | code  | 1..1  | SHALL | CD    | SHALL | (12   |       |
|       |       |       |       |       |       |       | 1291, |       |
|       |       |       |       |       |       |       | DCM,  |       |
|       |       |       |       |       |       |       | "Re   |       |
|       |       |       |       |       |       |       | sults |       |
|       |       |       |       |       |       |       | comm  |       |
|       |       |       |       |       |       |       | unica |       |
|       |       |       |       |       |       |       | ted") |       |
+-------+-------+-------+-------+-------+-------+-------+-------+-------+
| Comm  | >>>   | effe  | 1..1  | SHALL | TS    |       |       |       |
| ​Time |       | ctive |       |       |       |       |       |       |
|       |       | ​Time |       |       |       |       |       |       |
+-------+-------+-------+-------+-------+-------+-------+-------+-------+
|       | >>>   | text  | 1..1  | SHALL | ED    |       |       |       |
+-------+-------+-------+-------+-------+-------+-------+-------+-------+
| Ref   | >>>>  | refe  | 1..1  | SHALL | URL   |       | #     |       |
|       |       | rence |       |       | (XML  |       | *co   |       |
|       |       |       |       |       | I     |       | ntent |       |
|       |       |       |       |       | DREF) |       | ​Ref* |       |
+-------+-------+-------+-------+-------+-------+-------+-------+-------+
|       | >>>   | perf  | 1..1  | SHALL |       |       |       |       |
|       |       | ormer |       |       |       |       |       |       |
+-------+-------+-------+-------+-------+-------+-------+-------+-------+
|       | >>>>  | assig | 1..1  | SHALL |       |       |       |       |
|       |       | ned​E |       |       |       |       |       |       |
|       |       | ntity |       |       |       |       |       |       |
+-------+-------+-------+-------+-------+-------+-------+-------+-------+
|       | >>>>> | assi  | 1..1  | SHALL |       |       |       |       |
|       |       | gnedP |       |       |       |       |       |       |
|       |       | erson |       |       |       |       |       |       |
+-------+-------+-------+-------+-------+-------+-------+-------+-------+
| Repo  | >     | name  | 1..1  | SHALL | PN    |       |       |       |
| rting | >>>>> |       |       |       |       |       |       |       |
| ​Phys |       |       |       |       |       |       |       |       |
| ician |       |       |       |       |       |       |       |       |
| ​Name |       |       |       |       |       |       |       |       |
+-------+-------+-------+-------+-------+-------+-------+-------+-------+
|       | >>>   | p     | 1..1  | SHALL |       |       |       |       |
|       |       | artic |       |       |       |       |       |       |
|       |       | ipant |       |       |       |       |       |       |
+-------+-------+-------+-------+-------+-------+-------+-------+-------+
|       | >>>@  | @typ  | 1..1  | SHALL | CS    | SHALL | NOT   |       |
|       |       | eCode |       |       |       |       |       |       |
+-------+-------+-------+-------+-------+-------+-------+-------+-------+
|       | >>>>  | p     | 1..1  | SHALL |       |       |       |       |
|       |       | artic |       |       |       |       |       |       |
|       |       | ipant |       |       |       |       |       |       |
|       |       | ​Role |       |       |       |       |       |       |
+-------+-------+-------+-------+-------+-------+-------+-------+-------+
| Not   | >>>>> | te    | 1..1  | SHALL | TEL   |       |       |       |
| ifica |       | lecom |       |       |       |       |       |       |
| tion​ |       |       |       |       |       |       |       |       |
| Conta |       |       |       |       |       |       |       |       |
| ct​Te |       |       |       |       |       |       |       |       |
| lecom |       |       |       |       |       |       |       |       |
+-------+-------+-------+-------+-------+-------+-------+-------+-------+
|       | >>>>> | play  | 1..1  | SHALL |       |       |       |       |
|       |       | ing​E |       |       |       |       |       |       |
|       |       | ntity |       |       |       |       |       |       |
+-------+-------+-------+-------+-------+-------+-------+-------+-------+
| Notif | >     | name  | 1..1  | SHALL | PN    |       |       |       |
| icati | >>>>> |       |       |       |       |       |       |       |
| on​Co |       |       |       |       |       |       |       |       |
| ntact |       |       |       |       |       |       |       |       |
| ​Name |       |       |       |       |       |       |       |       |
+-------+-------+-------+-------+-------+-------+-------+-------+-------+

.. _sect_9.8.10.1:

section/text/content - narrative
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

Each documented act of communication of actionable findings SHALL be
included as narrative in a section/text/content element, labeled with an
XML ID (see `<content> Markup and Links From
Entries <#sect_9.1.1.1>`__).

.. note::

   The following text content for such a block is specified in the RSNA
   Radiology Reporting Templates, Template 297: Communication of
   Actionable Finding (http://radreport.org/txt-mrrt/0000297):

   method [discussed directly \| discussed by telephone \| described in
   message]

   by [person]

   to [person]

   on [<date>] at [<time>]

The documentation may also provide a linkHtml reference to the
actionable finding narrative elsewhere in the report, e.g., in the
`Findings <#sect_9.5>`__ or `Complications <#sect_9.8.4>`__ section (see
`<linkHtml> Markup and Internal References <#sect_9.1.1.2>`__).

.. _sect_9.8.10.2:

entry/act
^^^^^^^^^

A structured entry representation of the act of communication MAY be
included in the section. This entry does not necessarily represent the
entirety of the act as described in the narrative text, e.g., the
communication method and actual content of the communication is not
represented, nor whether the receiver acknowledged the communication
("read-back"). The act/text/reference element SHALL include an XML IDREF
value pointing to the associated narrative content block.

.. _sect_9.8.10.3:

entry/act/effectiveTime
^^^^^^^^^^^^^^^^^^^^^^^

The entry/act/effectiveTime element represents the date and time that
actionable findings were communicated. The time that the findings were
first observed is recorded in the effectiveTime element of the original
observation, as linked through the section/text/content/linkHtml
element.

.. _sect_9.8.10.4:

entry/act/participant
^^^^^^^^^^^^^^^^^^^^^

The entry/act/participant element represents the notified party
(@typecode = "NOT"). This could be the patient.

::

   <section classCode="DOCSECT" moodCode="EVN">
       <templateId root="1.2.840.10008.9.11"/>
       <id root="1.2.840.10213.2.62.7044794679.114296787"/>
       <code code="73568-8"
           codeSystem="2.16.840.1.113883.6.1"
           codeSystemName="LOINC"
           displayName="Communication of Critical Results"/>
       <title>Communication of Actionable Results</title>
       <text>
           <content ID=CR1>Dr. Smith was phoned at 262-966-0120 at 3:14pm on
           Wednesday, June 4, 2014, and the 4mm lung nodule was discussed directly
           with Dr. Smith to explain the follow-up recommendation of ...</content>
       </text>
       <entry>
           <act classCode="ACT" moodCode="EVN">
               <code code="121291"
                   codeSystem="1.2.840.10008.2.16.4"
                   codeSystemName="DCM"
                   displayName="Results Communicated"/>
               <text>
                   <reference value="#CR1"/>
               </text>
               <effectiveTime value="20140604221400-0700"/>
               <performer>
                   <assignedEntity>
                       <id root="1.2.840.10213.2.62.7044794679.114298686"/>
                       <assignedPerson>
                           <name>Jane Doctor</name>
                       </assignedPerson>
                   </assignedEntity>
               </performer>
               <participant typeCode="NOT">
                   <participantRole>
                       <telecom value="tel:262-966-0120"/>
                       <playingEntity>
                           <name>Dr. Smith</name>
                       </playingEntity>
                   </participantRole>
               </participant>
           </act>
       </entry>
   </section>

.. _sect_9.8.11:

Recommendation
~~~~~~~~~~~~~~

+----------------------+----------------------------------------------+
| **Template ID**      | 1.2.840.10008.9.12                           |
+----------------------+----------------------------------------------+
| **Name**             | Recommendation                               |
+----------------------+----------------------------------------------+
| **Effective Date**   | 2015/03/24                                   |
+----------------------+----------------------------------------------+
| **Version Label**    | DICOM-20150324                               |
+----------------------+----------------------------------------------+
| **Status**           | Active                                       |
+----------------------+----------------------------------------------+
| **Description**      | This section provides a separate section to  |
|                      | describe the study interpreter's             |
|                      | recommendations for follow-up studies or     |
|                      | procedures.                                  |
+----------------------+----------------------------------------------+
| **Classification**   | CDA Section Level                            |
+----------------------+----------------------------------------------+
| **Relationships**    | Included in `Impression <#sect_9.6>`__       |
+----------------------+----------------------------------------------+
| **Context**          | parent node                                  |
+----------------------+----------------------------------------------+
| **Open/Closed**      | Open                                         |
+----------------------+----------------------------------------------+
| **Revision History** | DICOM-20150324: Initial version              |
+----------------------+----------------------------------------------+

+-------+-------+-------+-------+-------+-------+-------+-------+-------+
| **Bus | *     | **    | **C   | *     | *     | **    | **Va  | **    |
| iness | *Nest | Eleme | ard** | *Elem | *Data | Value | lue** | Subsi |
| N     | Le    | nt/​A |       | /Attr | T     | C     |       | diary |
| ame** | vel** | ttrib |       | C     | ype** | onf** |       | Templ |
|       |       | ute** |       | onf** |       |       |       | ate** |
+-------+-------+-------+-------+-------+-------+-------+-------+-------+
| **R   |       | se    |       |       |       |       |       |       |
| ecomm |       | ction |       |       |       |       |       |       |
| endat |       |       |       |       |       |       |       |       |
| ion** |       |       |       |       |       |       |       |       |
+-------+-------+-------+-------+-------+-------+-------+-------+-------+
|       | >     | t     | 1..1  | SHALL | II    |       |       |       |
|       |       | empla |       |       |       |       |       |       |
|       |       | te​Id |       |       |       |       |       |       |
+-------+-------+-------+-------+-------+-------+-------+-------+-------+
|       | >@    | @root | 1..1  | SHALL | UID   | SHALL | 1.2   |       |
|       |       |       |       |       |       |       | .840. |       |
|       |       |       |       |       |       |       | 10008 |       |
|       |       |       |       |       |       |       | .9.12 |       |
+-------+-------+-------+-------+-------+-------+-------+-------+-------+
|       | >     | id    | 1..\* | SHALL | II    |       |       |       |
+-------+-------+-------+-------+-------+-------+-------+-------+-------+
|       | >     | code  | 1..1  | SHALL | CD    | SHALL | `(187 |       |
|       |       |       |       |       |       |       | 83-1, |       |
|       |       |       |       |       |       |       | L     |       |
|       |       |       |       |       |       |       | OINC, |       |
|       |       |       |       |       |       |       | "     |       |
|       |       |       |       |       |       |       | Study |       |
|       |       |       |       |       |       |       | re    |       |
|       |       |       |       |       |       |       | comme |       |
|       |       |       |       |       |       |       | ndati |       |
|       |       |       |       |       |       |       | on")  |       |
|       |       |       |       |       |       |       | <http |       |
|       |       |       |       |       |       |       | ://lo |       |
|       |       |       |       |       |       |       | inc.o |       |
|       |       |       |       |       |       |       | rg/18 |       |
|       |       |       |       |       |       |       | 783-1 |       |
|       |       |       |       |       |       |       | />`__ |       |
+-------+-------+-------+-------+-------+-------+-------+-------+-------+
| Title | >     | title | 0..1  | MAY   | ST    |       |       |       |
+-------+-------+-------+-------+-------+-------+-------+-------+-------+
| Text  | >     | text  | 0..1  | SHALL | ED    |       |       |       |
+-------+-------+-------+-------+-------+-------+-------+-------+-------+
| **Co  | >>    | co    | 0..\* | SHALL | ST    |       | [See  |       |
| ntent |       | ntent |       |       |       |       | `tex  |       |
| [*]** |       |       |       |       |       |       | t/con |       |
|       |       |       |       |       |       |       | tent  |       |
|       |       |       |       |       |       |       | <#sec |       |
|       |       |       |       |       |       |       | t_9.8 |       |
|       |       |       |       |       |       |       | .11.1 |       |
|       |       |       |       |       |       |       | >`__] |       |
+-------+-------+-------+-------+-------+-------+-------+-------+-------+
| *     | >>@   | @ID   | 1..1  | SHALL | XML   |       |       |       |
| *\*** |       |       |       |       | ID    |       |       |       |
+-------+-------+-------+-------+-------+-------+-------+-------+-------+
| Gui   | >>>   | link  | 0..1  | MAY   | ST    |       |       |       |
| delin |       | ​Html |       |       |       |       |       |       |
| e​Ref |       |       |       |       |       |       |       |       |
+-------+-------+-------+-------+-------+-------+-------+-------+-------+
| Gui   | >>>@  | @href | 1..1  | SHALL | URI   |       |       |       |
| delin |       |       |       |       |       |       |       |       |
| e​URI |       |       |       |       |       |       |       |       |
+-------+-------+-------+-------+-------+-------+-------+-------+-------+
|       | >     | entry | 0..\* | S     |       |       |       |       |
|       |       |       |       | HOULD |       |       |       |       |
+-------+-------+-------+-------+-------+-------+-------+-------+-------+
| **Fol | >>    | proc  | 1..1  | SHALL |       |       |       |       |
| lowup |       | edure |       |       |       |       |       |       |
| ​Proc |       |       |       |       |       |       |       |       |
| edure |       |       |       |       |       |       |       |       |
| [*]** |       |       |       |       |       |       |       |       |
+-------+-------+-------+-------+-------+-------+-------+-------+-------+
|       | >>@   | @clas | 1..1  | SHALL | CS    | SHALL | PROC  |       |
|       |       | sCode |       |       |       |       |       |       |
+-------+-------+-------+-------+-------+-------+-------+-------+-------+
|       | >>@   | @moo  | 1..1  | SHALL | CS    | SHALL | PRP   |       |
|       |       | dCode |       |       |       |       |       |       |
+-------+-------+-------+-------+-------+-------+-------+-------+-------+
| Proc  | >>>   | code  | 1..1  | SHALL | CD    |       | Conc  |       |
| edure |       |       |       |       |       |       | ept​D |       |
| ​Code |       |       |       |       |       |       | omain |       |
|       |       |       |       |       |       |       | R     |       |
|       |       |       |       |       |       |       | ecomm |       |
|       |       |       |       |       |       |       | ended |       |
|       |       |       |       |       |       |       | Foll  |       |
|       |       |       |       |       |       |       | ow-up |       |
+-------+-------+-------+-------+-------+-------+-------+-------+-------+
| When  | >>>   | effe  | 1..1  | S     | IVL   |       |       |       |
|       |       | ctive |       | HOULD | <TS>  |       |       |       |
|       |       | ​Time |       |       |       |       |       |       |
+-------+-------+-------+-------+-------+-------+-------+-------+-------+
|       | >>>   | text  | 1..1  | SHALL | ED    |       |       |       |
+-------+-------+-------+-------+-------+-------+-------+-------+-------+
| Ref   | >>>>  | refe  | 1..1  | SHALL | URL   |       | #     |       |
|       |       | rence |       |       | (XML  |       | *co   |       |
|       |       |       |       |       | I     |       | ntent |       |
|       |       |       |       |       | DREF) |       | ​Ref* |       |
+-------+-------+-------+-------+-------+-------+-------+-------+-------+

.. _sect_9.8.11.1:

text/content
^^^^^^^^^^^^

Each documented recommendation SHALL be included as narrative in a
content element, labeled with an XML ID (see `<content> Markup and Links
From Entries <#sect_9.1.1.1>`__). The content element NEED NOT be top
level markup within the section/text element; it MAY be wrapped in
another allowed narrative block markup, such as paragraph, list/item, or
table/row/cell.

If the recommendation is based on a clinical guideline, a reference to
that guideline MAY be included in a linkHtml element.

Each recommendation SHOULD have a corresponding structured entry.

.. _sect_9.8.11.2:

entry/procedure
^^^^^^^^^^^^^^^

The Recommendation section SHOULD include entries for recommended
follow-up actions or procedures.

.. note::

   While this entry may be a trigger for a tracking system for ensuring
   follow up on recommendations, the imaging study report only conveys
   the interpreting physician's recommendations.

.. _sect_9.8.11.3:

entry/procedure/code
^^^^^^^^^^^^^^^^^^^^

Vocabulary binding for Concept Domain Recommended Follow-up may be
further profiled in sub-specialty guidelines.

.. note::

   An example would be Value Set , incorporating concepts from ACR
   BI-RADS :sup:`®`.

.. _sect_9.8.11.4:

entry/procedure/effectiveTime
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

The HL7v3 IVL <TS> Data Type used for effectiveTime requires the
specification of absolute dates, rather than a date relative to the date
of the report.

.. note::

   Thus the concept "follow-up within one year" needs to be encoded as a
   IVL <TS> with an effectiveTime/high element value one year after the
   date of the report.

.. _sect_9.8.11.5:

entry/procedure/text/reference
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

The procedure entry SHALL include a text/reference element, whose value
attribute SHALL begin with a '#' and SHALL point to its corresponding
narrative content block. See `<content> Markup and Links From
Entries <#sect_9.1.1.1>`__.

::

   <section classCode="DOCSECT" moodCode="EVN">
       <templateId root="1.2.840.10008.9.12" />
       <id root="1.2.840.10213.2.62.7044779.114265201"/>
       <code code="18783-1" codeSystem="2.16.840.1.113883.6.1"
           codeSystemName="LOINC" displayName="Study Recommendation"/>
       <title>Radiology Recommendation</title>
       <text>
           <content ID="rec01">Biopsy should be considered. Follow-up at 3 month interval.
           </content>
           <linkHtml href="http://pubs.rsna.org/doi/abs/10.1148/radiol.2372041887"/>
       </text>
       <entry>
           <procedure ID="RadRec1" classCode="PROC" moodCode="PRP"/>
           <!-- local coding scheme -->
           <code code="9191919" codeSystem="2.16.840.1.56789.6.1"
               codeSystemName="My Hospital Coding System"
               displayName="3 month follow-up"/>
           <text><reference value="#rec01"/></text>
           <effectiveTime value="20141213"/>
       </entry>
   </section>

