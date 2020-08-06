.. _chapter_5:

Conventions
===========

.. _sect_5.1:

Template Metadata
-----------------

Each template has a set of metadata, as specified in the HL7 Templates
Specification. The metadata is presented as a table, as shown in
`table_title <#table_5.1-1>`__.

.. table:: Template metadata table format

   +----------------------+----------------------------------------------+
   | **Template ID**      | OID (see `Template IDs and                   |
   |                      | Version <#sect_5.1.1>`__)                    |
   +----------------------+----------------------------------------------+
   | **Name**             |                                              |
   +----------------------+----------------------------------------------+
   | **Effective Date**   |                                              |
   +----------------------+----------------------------------------------+
   | **Version Label**    | (see `Template IDs and                       |
   |                      | Version <#sect_5.1.1>`__)                    |
   +----------------------+----------------------------------------------+
   | **Status**           | "draft", "active", "review" or "retired"     |
   +----------------------+----------------------------------------------+
   | **Description**      |                                              |
   +----------------------+----------------------------------------------+
   | **Classification**   | type of the template, e.g., CDA Section      |
   |                      | Level                                        |
   +----------------------+----------------------------------------------+
   | **Relationships**    | relationships to other templates or model    |
   |                      | artifacts                                    |
   +----------------------+----------------------------------------------+
   | **Context**          | "parent node", "sibling node" (see           |
   |                      | `Context <#sect_5.1.2>`__)                   |
   +----------------------+----------------------------------------------+
   | **Open/Closed**      | "open", "closed"(see `Open and Closed        |
   |                      | Templates <#sect_5.1.3>`__)                  |
   +----------------------+----------------------------------------------+
   | **Revision History** |                                              |
   +----------------------+----------------------------------------------+

.. _sect_5.1.1:

Template IDs and Version
~~~~~~~~~~~~~~~~~~~~~~~~

Template identifiers (templateId) are assigned for each document,
section, and entry level template. When valued in an instance, the
template identifier signals the imposition of a set of template-defined
constraints. The value of this attribute (e.g.,
@root="2.16.840.1.113883.10.20.22.4.8") provides a unique identifier for
the template in question.

A template may be further qualified by a version label. This label may
be used as the extension attribute of the templateID (e.g.,
@extension="20150309"). All versions of a template, regardless of the
version label, must be compatible; i.e., they may vary only by optional
content conformance requirements. Thus the version label is typically
not used as a conformance constraint.

Within this Standard, template versions are identified by the string
"DICOM" and the date of adoption (represented as YYYYMMDD), separated by
a hyphen (e.g., DICOM-20150523).

.. _sect_5.1.2:

Context
~~~~~~~

As described in the HL7 Template specification section 2.9.9.4, the
context identifies whether the template applies to the parent node in
which the templateID is an element, or applies to its sibling nodes in
the template table. These typically are applied respectively to
templates with a single parent element with child element structure, and
to templates with flat list of sibling elements (see `Value
Specification <#sect_5.2.8>`__).

.. _sect_5.1.3:

Open and Closed Templates
~~~~~~~~~~~~~~~~~~~~~~~~~

Each template is defined as being either "open" or "closed". In "open"
templates, all of the features of the CDA Specification are allowed
except as constrained by the templates. By contrast, a "closed" template
specifies everything that is allowed and nothing further may be
included.

.. _sect_5.2:

Template Table Structure
------------------------

Each template is specified in tabular form, as shown in
`table_title <#table_5.2-1>`__.

.. table:: Template table format

   +-------+-------+-------+------+-------+-------+-------+-------+-------+
   | Bus   | Nest  | Ele   | Card | Elem  | Data  | Value | Value | Subsi |
   | iness | Level | ment/ |      | /Attr | Type  | Conf  |       | diary |
   | Name  |       | ​Attr |      | Conf  |       |       |       | Tem   |
   |       |       | ibute |      |       |       |       |       | plate |
   +=======+=======+=======+======+=======+=======+=======+=======+=======+
   | **Sco |       |       |      |       |       |       |       |       |
   | ping​ |       |       |      |       |       |       |       |       |
   | Busin |       |       |      |       |       |       |       |       |
   | ess​N |       |       |      |       |       |       |       |       |
   | ame** |       |       |      |       |       |       |       |       |
   +-------+-------+-------+------+-------+-------+-------+-------+-------+
   | E     |       |       |      |       |       |       |       |       |
   | lemen |       |       |      |       |       |       |       |       |
   | t​Bus |       |       |      |       |       |       |       |       |
   | iness |       |       |      |       |       |       |       |       |
   | ​Name |       |       |      |       |       |       |       |       |
   +-------+-------+-------+------+-------+-------+-------+-------+-------+
   | *     |       |       |      |       |       |       |       |       |
   | Refer |       |       |      |       |       |       |       |       |
   | enced |       |       |      |       |       |       |       |       |
   | ​Busi |       |       |      |       |       |       |       |       |
   | ness​ |       |       |      |       |       |       |       |       |
   | Name* |       |       |      |       |       |       |       |       |
   +-------+-------+-------+------+-------+-------+-------+-------+-------+

.. _sect_5.2.1:

Business Name
~~~~~~~~~~~~~

This Part uses Business Names to identify and map common data elements
from clinical imaging reports into the proper context-specific CDA/XML
structure.

A Business Name is assigned to each element or attribute that may have a
user-specified value assigned in the production of the clinical document
instance. Business Names are specified to facilitate the implementation
of production logic for clinical report authoring applications. The
benefit is that developers of clinical report authoring applications are
not required to have an in depth knowledge of CDA, the HL7 v3 R-MIM data
model, or the XML structures. The use of readable and intuitive Business
Names provides a method of direct access to insert data that is specific
to each clinical report instance.

.. note::

   Business Names are also described in the HL7 greenCDAModules for CCD
   specification, but that specification implies the use of a specific
   XML structure for production logic that is not required by this Part.
   The specification of production logic using Business Names is outside
   the scope of this Part.

Business Names are not specified for elements that are expected to
receive an automatically generated value, e.g., the id element for each
document, section, and entry.

As a convention, Business Names are represented in CamelCase
(alternating upper and lower case, no spaces, initial letter in upper
case) in the Business Name column of the template tables.

Business Names are hierarchically organized, and contextually scoped by
higher level Business Names.

-  Data element/attribute level Business Names are shown in normal font

-  Business Names that provide scoping for subsidiary Business Names are
   shown in bold font.

-  Referenced Business Names from included templates are shown in italic
   (see `Subsidiary Templates <#sect_5.2.9>`__)

-  As a convention, hierarchical relationship between Business Names is
   shown with the : character.

Scoping Business Names scope all attributes and elements subsidiary to
the element to which the name is assigned.

Examples:

-  The top level scoping Business Name for an Imaging Report is
   "ImagingReport", and it scopes all attributes and elements in the
   document, i.e., including and subsidiary to the <ClinicalDocument>
   XML element

-  The Business Name for the `Clinical Information <#sect_9.2>`__ report
   section is "ImagingReport:ClinicalInformation", and it scopes all
   attributes and elements including and subsidiary to the <section> XML
   element in template 1.2.840.10008.9.2

-  The Business Name for the text element of the `Clinical
   Information <#sect_9.2>`__ report section is
   "ImagingReport:ClinicalInformation:Text"

-  The Business Name for the text element of the
   `Impression <#sect_9.6>`__ section is "ImagingReport:Impression:Text"

Note that both `Clinical Information <#sect_9.2>`__ and
`Impression <#sect_9.6>`__ define a Business Name "Text", but these are
distinguished by their hierarchical location under the scoping Business
Names of their respective sections.

.. _sect_5.2.1.1:

Multiple Instantiations
^^^^^^^^^^^^^^^^^^^^^^^

Some templates may be invoked multiple times in a document instance; for
example, the `Quantity Measurement <#sect_10.5>`__ template is
instantiated for each numeric measurement in a report. Each
instantiation shall have an identifying string, unique within the
document, used as a discriminator between those multiple instantiations.
The Business Name for each element that may have multiple instantiations
has a suffix [*], indicating the use of a discriminator string. This
allows Business Name based production logic for authoring applications
to identify specific instances of an element.

::

   -- "Q21a" is the discriminator for the first measurement
   -- "Q21b" is the discriminator for the second measurement
   ImagingReport:Findings:QuantityMeasurement[Q21a]:MeasurementName = ("112058", "DCM", "Calcium score")
   ImagingReport:Findings:QuantityMeasurement[Q21a]:MeasurementValue = "8"
   ImagingReport:Findings:QuantityMeasurement[Q21a]:MeasurementUnits = "[arb'U]"
   ImagingReport:Findings:QuantityMeasurement[Q21b]:MeasurementName = ("408716009", "SNOMED", "Stenotic lesion length")
   ImagingReport:Findings:QuantityMeasurement[Q21b]:MeasurementValue = "14"
   ImagingReport:Findings:QuantityMeasurement[Q21b]:MeasurementUnits = "mm"

The discriminator string shall be conformant to XML Name production
requirements, as used for the XML ID attribute (see `XML
ID <#sect_5.3.4>`__ on the use of XML ID).

Some CDA elements may include an XML ID attribute. This attribute is
identified by '*' (asterisk) as its Business Name, and its value shall
be the discriminator string.

.. _sect_5.2.1.2:

Implicit Element Structure For Business Name
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

A Business Name may be associated with an element subsidiary to another
element that does not have an associated Business Name. In such a case,
when the element with the Business Name is instantiated in a document,
its entire parent element hierarchy must be instantiated, even if those
elements are identified as optional.

.. note::

   For example, in the `General Header <#sect_8.1>`__ template, if
   Recipient:Name is instantiated, the entire hierarchical structure of
   informationRecipient/intendedRecipient/informationRecipient/name must
   be instantiated to hold the name element content.

.. _sect_5.2.2:

Nesting Level
~~~~~~~~~~~~~

CDA documents are encoded using the Extensible Markup Language (XML),
and are marked up through hierarchically nested XML elements (tags). The
Nesting Level column of the template tables identifies the hierarchical
level of each element relative to the other elements in the table using
the character right angle bracket '>'. Multiple levels of nesting are
identified by multiple > characters.

XML elements may have attributes, encoded as "<name>=<value>" pairs
within the element tag. Such attributes are identified using the
character at sign '@'.

.. _sect_5.2.3:

Element/Attribute Names and XPath Notation
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

The name of each XML element and attribute used in a CDA document for
which specific constraints are applied is shown in the Element/Attribute
column of the template tables. Optional elements whose use is not
specified nor constrained are not shown.

Elements and attributes that use the default value specified in CDA
Specification are not shown. For example, the Section element has
default attributes classCode='DOCSECT' and moodCode='EVN'; these are not
listed in the templates. In accordance with the HL7 v3 specification,
attributes with default values need not be included in instances, and
their absence implies the default value.

XML Path Language (XPath) notation is used to identify the XML elements
and attributes within the CDA document instance to which various
constraints are applied. The implicit context of these expressions is
the root node of the document, and traversing the path to the root node
of the relevant template. This notation provides a mechanism that will
be familiar to developers for identifying parts of an XML document.

XPath syntax selects nodes from an XML document using a path containing
the context of the node(s). The path is constructed from node names and
attribute names (prefixed by a '@') and concatenated with a '/' symbol.

`example_title <#example_5.2.3-1>`__ is an example of a fragment of a
CDA document.

::

   <author>
       <assignedAuthor>
           ...
           <code codeSystem='2.16.840.1.113883.6.96' codeSystemName='SNOMED CT'
                   code='17561000' displayName='Cardiologist' />
               ...
           </assignedAuthor>
       </author>

`table_title <#table_5.2.3-1>`__ is an example of a fragment of a
template specification table.

.. table:: Template element and attribute example

   == ========== ================== =
   …  Nest Level Element/​Attribute …
   == ========== ================== =
   \             author             
   \  >          assigned​Author    
   …                                
   \  >>         code               
   \  >>@        @codeSystem        
   \  >>@        @codeSystemName    
   \  >>@        @code              
   \  >>@        @displayName       
   …                                
   == ========== ================== =

In `table_title <#table_5.2.3-1>`__, the code attribute of the code
element could be selected with the XPath
expressionauthor/assignedAuthor/code/@code.

.. _sect_5.2.4:

Cardinality
~~~~~~~~~~~

Each element/attribute has a cardinality indicator that specifies the
number of allowable occurrences within a template instance. The
cardinality indicators are interpreted with the following format "m…n"
where m represents the least and n the most:

-  0..1 zero or one

-  1..1 exactly one

-  1..\* at least one

-  0..\* zero or more

-  1..n at least one and not more than n

-  0..0 none [SHALL NOT]

.. _sect_5.2.5:

Element/Attribute Conformance
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

Each element/attribute has a conformance verb (keyword) in addition to
the cardinality constraint.

The keywords SHALL, SHOULD, MAY, SHOULD NOT, SHALL NOT, and NEED NOT in
this document are to be interpreted as described in ISO/IEC Directives,
Part 2, Annex H "Verbal forms for the expression of provisions":

-  SHALL: an absolute requirement

-  SHALL NOT: an absolute prohibition against inclusion

-  SHOULD/SHOULD NOT: a best practice or recommendation. There may be
   valid reasons to ignore a recommendation, but the full implications
   must be understood and carefully weighed before choosing to not
   adhere to the best practice.

-  MAY/NEED NOT: truly optional; can be included or omitted at the
   discretion of the content creator with no conformance implications

The keyword SHALL is associated with a minimum cardinality of at least
1; other keywords have a minimum cardinality of 0. If an element is
required by SHALL, but is not known (and would otherwise be omitted
without the SHALL requirement), it must be represented by a nullFlavor.
SHALL allows the use of nullFlavor unless the requirement is on an
attribute (nullFlavor does not apply to attributes), or the use of
nullFlavor is explicitly precluded (see `Value
Conformance <#sect_5.2.7>`__ and `Null Flavor <#sect_5.3.2>`__).

Within the template, the keyword COND (conditional) may be present. In
this case, the specification of the condition, and the conformance verbs
associated with the condition being true or false, are described below
the table in a paragraph flagged with the COND keyword.

In an open template, additional elements and attributes allowed by the
CDA Specification are not precluded by template constraints, unless
there are applicable SHALL NOT template specifications.

.. _sect_5.2.6:

Data Type
~~~~~~~~~

The data type associated with each element/attribute is specified, as
described in the CDA Specification and its referenced HL7v3 Data Types
Release 1. Elements that are simply tags with subsidiary content only of
nested elements, e.g., RIM class clone names, have the Data Type column
empty.

Many data types are non-primitive, and may include constituent component
elements and/or attributes. Such subsidiary components are not specified
in the templates unless specific constraints are to be applied to them.

.. _sect_5.2.7:

Value Conformance
~~~~~~~~~~~~~~~~~

The template table may constrain values or vocabularies to be used with
an element or attribute. Value constraints include a conformance verb
(SHALL, SHOULD, MAY, etc.) as defined in `Element/Attribute
Conformance <#sect_5.2.5>`__, and specified in the Value Conformance
column of the template tables.

Elements for which nullFlavor is forbidden are indicated with an
additional constraint keyword noNull.

Additionally, constraints specifying Value Sets include a coding
strength conformance CWE (Coded With Extensibility) or CNE (Coded with
No Extensibility), as defined in Core Principles and Properties of HL7
Version 3 Models, Release 1.

Further, Value Set constraints can be static, meaning that they are
bound to a specified version of a Value Set, or dynamic, meaning that
they are bound to the most current version of the Value Set. By default,
Value Sets have dynamic binding, unless explicitly specified with an
additional constraint keyword static.

.. _sect_5.2.8:

Value Specification
~~~~~~~~~~~~~~~~~~~

The template table may constrain values to a single fixed value, to a
Value Set from which the value is to be drawn, or to a named Concept
Domain. It may non-normatively reference a mapping from a DICOM SOP
Instance or an HL7 message.

The template table may contain elements without a value specification,
and without a Business Name. These are typically id elements. The
application creating the document instance shall fill these elements
with appropriate values.

.. _sect_5.2.8.1:

Coded Simple Value
^^^^^^^^^^^^^^^^^^

Values of Data Type CS (Coded Simple Value) have a fixed code system
defined in the CDA Specification, and are simple strings. The template
tables identify only the constraint on the code value, and do not
specify the fixed code system nor the code meaning (display name), which
are not encoded in the CDA instance.

.. _sect_5.2.8.2:

Concept Descriptor and Coded With Equivalents
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

Single values of Data Type CD (Concept Descriptor) or CE (Coded With
Equivalents) are specified in the template tables with the triplet
notation specified in :

-  (CodeValue, Coding Scheme Designator, "Code Meaning")

The Coding Scheme Designator is a simple human readable identifier of
the code system, and corresponds to the optional codeSystemName
attribute of the CD or CE element. The CDA Specification requires the
Code System OID to be encoded in the codeSystem attribute of the CD or
CE element. The corresponding OID for each Coding Scheme Designator is
provided in . The Code Meaning is encoded in the displayName attribute
of the CD or CE element.

.. _sect_5.2.8.3:

Value Set
^^^^^^^^^

Elements whose value may be drawn from a Value Set will have that Value
Set identified in the Value column introduced by the keyword ValueSet.

.. _sect_5.2.8.4:

Concept Domains
^^^^^^^^^^^^^^^

Concept Domains (see definition in `glossdiv_title <#sect_3.2>`__) are
used to provide a named category in a structural template that can be
bound to a specific value or value set by an invoking template, thus
specializing the structural template for a particular use case. Concept
Domain names are introduced by the keyword ConceptDomain in the Value
column. For example, the `Quantity Measurement <#sect_10.5>`__ template
Concept Domain "observationType" might be bound to a value set of fetal
ultrasound measurements in one invoking template, or to a value set of
cardiac CT measurements in another invoking template.

Concept Domain names are similar to element Business Names in that they
provide a public interface that is bound to specific values later in the
document specification and production process. Concept Domains do not
have a Value Conformance verb; the conformance verb is specified when
the Concept Domain is bound to a specific value or value set (see
`Vocabulary Binding and Constraints <#sect_5.2.9.1>`__).

.. _sect_5.2.8.5:

Mapping From DICOM SOP Instances and HL7v2 Messages
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

Elements whose value may be mapped from a DICOM SOP Instance or from an
HL7v2 message have the source attribute name and tag identified in the
Value column in italic font. Note that many of these values have their
origin in IT systems outside the imaging department, and there may be
alternate routes for these values to be accessed by the reporting
application, e.g., from an HL7 FHIR web service.

.. note::

   Due to differences in use of HL7v2 data elements, mappings should not
   be considered normative.

Data mapped from a specific Attribute in the interpreted DICOM image(s)
is identified by the Attribute Name and Tag, represented in the mapping
as:

-  *Attribute Name (gggg,eeee)*

Data mapped from Attributes within sequences is identified with the >
character:

-  *Sequence Attribute Name (ggg0,eee0) > Item Attribute Name
   (ggg1,eee1)*

Data mapped from an HL7v2 field in the order for the study is identified
by the Element Name and Segment Field identifier:

-  *Element Name seg-n*

The mapping of the value typically requires a transformation from the
DICOM Value Representation or the HL7v2 Data Type representation to the
CDA Data Type encoding. For example, transforming a DICOM Code Sequence
attribute or an HL7v2 CWE field to a CD or CE Data Type requires a look
up of the Coding Scheme OID.

.. _sect_5.2.9:

Subsidiary Templates
~~~~~~~~~~~~~~~~~~~~

A template may include subsidiary templates. Templates typically have
one of two styles, a single parent element with child element structure,
or a flat list of sibling elements.

The single parent element style is typical for the top level Document,
Section, and Entry templates, and the parent element is of the HL7 v3
RIM act class. Inclusion of such a template therefore involves an
actRelationship element; that actRelationship element is specified in
the invoking template.

The sibling elements style is typical for sets of elements and
attributes aggregated for editorial convenience.

Inclusion of a subsidiary template includes the name of included
template and its templateID, specified in the Subsidiary Template column
of the invoking template table.

For an included template of the single parent element style, the scoping
business name and top level element are provided in italics in the
invoking template table. This indicates this is data copied from the
specification in the included template for the reader's convenience.

.. _sect_5.2.9.1:

Vocabulary Binding and Constraints
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

A template inclusion may provide Concept Domain Vocabulary Binding or
other vocabulary constraints, e.g., limiting an element in the included
template to a specific value from its defined Value Set. These
vocabulary constraints are specified in tabular form, as shown in
`table_title <#table_5.2.9.1-1>`__. The table is included in the
additional requirements for the template, with a reference in the Value
column of the template entry invoking the subsidiary template. The Value
Conformance and Value specification columns are interpreted as in the
templates tables.

.. table:: Vocabulary Binding Table Format

   ========================= ========== =====
   Concept Domain or Element Value Conf Value
   ========================= ========== =====
   ...                       ...        ...
   ========================= ========== =====

.. _sect_5.2.10:

Additional Requirements
~~~~~~~~~~~~~~~~~~~~~~~

Each template may be accompanied by additional requirements and usage
explanations in narrative specification language.

.. _sect_5.3:

Encoding
--------

A full discussion of the representation of data types and vocabulary is
outside the scope of this document; for more information, see the HL7 V3
specifications on Abstract Data Types R1 and XML Data Types R1
referenced in the CDA Specification.

.. note::

   1. Many Data Types encode their values in attributes, rather than
      character data. For example, the URL Data Type encodes its value
      in the **value**\ attribute within the element tag, e.g.,
      <reference value="http://xyz.org">. Within this specification, the
      attribute(s) that hold the value are not identified, except where
      specific constraints apply.

   2. The Consolidated CDA specification includes extensive examples of
      valid and invalid encodings, which may be useful for implementers.

   3. The specification of a representation of Data Types for use in
      Business Name-based report production logic is outside the scope
      of this Standard.

.. _sect_5.3.1:

Translation Code Element
~~~~~~~~~~~~~~~~~~~~~~~~

HL7 Data Types CD (Concept Descriptor) and CE (Coded With Equivalents)
allow a translation code element, which allows the encoding of the same
concept in an alternate coding system. This supports the encoding of
both an originally entered (local) code, and a code specified for
cross-system interoperability.

This Part follows the convention used in the Consolidated CDA
Implementation Guide specification, which specifies the standard
interoperable code in the root, whether it is original or a translation.
The HL7v3 Data Types R1 standard included by CDA formally specifies the
original code (as initially entered in an information system
application) to be placed in the root.

.. note::

   This discrepancy is resolved in HL7v3 Data Types R2 to follow the
   convention used here, and the HL7 Structured Documents Working Group
   has approved the "pre-adoption" of the Data Types R2 approach in CDA
   implementations.

::

   <code code='206525008'
         displayName='neonatal necrotizing enterocolitis 'codeSystem='2.16.840.1.113883.6.96'
         codeSystemName='SNOMED CT'>
       <translation code='NEC-1'
         displayName='necrotizing enterocolitis'
         codeSystem='2.16.840.1.113883.19'/>
   </code>

.. _sect_5.3.2:

Null Flavor
~~~~~~~~~~~

Information technology solutions store and manage data, but sometimes
data are not available: an item may be unknown, not relevant, or not
computable or measurable. In HL7 v3, a flavor of null, or nullFlavor,
describes the reason for missing data.

For example, if a patient arrives at an Emergency Department unconscious
and with no identification, a null flavor is used to represent the lack
of information. The patient's birth date could be represented with a
null flavor of "NAV", which is the code for "temporarily unavailable".
When the patient regains consciousness or a relative arrives, we expect
to be able to obtain the patient's birth date.

::

   <birthTime nullFlavor="NAV"/> <!--coding an unknown birthdate-->

Use null flavors for unknown, required, or optional attributes:

NI
   No information. This is the most general and default null flavor.

NA
   Not applicable. Known to have no proper value (e.g., last menstrual
   period for a male).

UNK
   Unknown. A proper value is applicable, but is not known.

ASKU
   Asked, but not known. Information was sought, but not found (e.g.,
   the patient was asked but did not know).

NAV
   Temporarily unavailable. The information is not available, but is
   expected to be available later.

NASK
   Not asked. The patient was not asked.

MSK
   Masked. There is information on this item available but it has not
   been provided by the sender due to security, privacy, or other
   reasons. There may be an alternate mechanism for gaining access to
   this information.

OTH
   Other. The actual value is not an element in the value domain of a
   variable. (e.g., concept not provided by required code system).

The above null flavors are commonly used in clinical documents. For the
full list and descriptions, see the nullFlavor vocabulary domain in the
HL7 v3 Vocabulary referenced by the CDA specification.

Any SHALL conformance requirement on an element may use nullFlavor,
unless nullFlavor is explicitly disallowed (as indicated by noNull, see
`Value Conformance <#sect_5.2.7>`__). SHOULD and MAY conformance
requirements may also use nullFlavor. nullFlavor does not apply to
conformance requirements on attributes.

The encoding of nullFlavor as an attribute of the data type element is
not shown in the templates, hence there is no business name associated
with the attribute.

.. note::

   Production logic based on Business Names needs to provide a mechanism
   for assignment of a value to the nullFlavor attribute as an
   alternative for a value for the element. Specification of such
   production logic is outside the scope of this Standard.

::

   <entry>
       <observation classCode="OBS" moodCode="EVN">
           <id nullFlavor="NI"/>
           <code nullFlavor="OTH">
               <originalText>New Grading system</originalText>
           </code>
           <statusCode code="completed"/>
           <effectiveTime nullFlavor="UNK"/>
           <value xsi:type="CD" nullFlavor="NAV">
               <originalText>Spiculated mass grade 5</originalText>
           </value>
       </observation>
   </entry>

.. _sect_5.3.3:

Unknown Information
~~~~~~~~~~~~~~~~~~~

If a document creator wants to state that a piece of information is
unknown, the following principles apply:

1. If the creator doesn't know an attribute of an act, that attribute
   can be null.

   ::

      <text>patient was given a medication but I do not know what it was</text>
      <entry>
          <substanceAdministration moodCode="EVN" classCode="SBADM">
              <consumable>
                  <manufacturedProduct>
                      <manufacturedLabeledDrug>
                          <code nullFlavor="NI"/>
                      </manufacturedLabeledDrug>
                  </manufacturedProduct>
              </consumable>
          </substanceAdministration>
      </entry>

2. If the creator doesn't know if an act occurred, the nullFlavor is on
   the act (detail could include specific allergy, drug, etc.).

   ::

      <text>I do not know whether or not patient received an anticoagulant drug</text>
      <entry></para>
          <substanceAdministration moodCode="EVN" classCode="SBADM" nullFlavor="NI">
              <consumable>
                  <manufacturedProduct>
                      <manufacturedLabeledDrug>
                          <code code="81839001" displayName="anticoagulant drug"
                              codeSystem="2.16.840.1.113883.6.96"
                              codeSystemName="SNOMED CT"/>
                      </manufacturedLabeledDrug>
                  </manufacturedProduct>
              </consumable>
          </substanceAdministration>
      </entry>

3. If the sender wants to state 'no known', a negationInd can be used on
   the corresponding act (substanceAdministration, Procedure, etc.)

   ::

      <text>No known medications</text>
      <entry>
          <substanceAdministration moodCode="EVN" classCode="SBADM" negationInd="true">
              <consumable>
                  <manufacturedProduct>
                      <manufacturedLabeledDrug>
                          <code code="410942007" displayName="drug or medication"
                              codeSystem="2.16.840.1.113883.6.96"
                              codeSystemName="SNOMED CT"/>
                      </manufacturedLabeledDrug>
                  </manufacturedProduct>
              </consumable>
          </substanceAdministration>
      </entry>

Other CDA implementation guides recommended using specific codes to
assert no known content, for example SNOMED CT 160244002 "No known
allergies" or 160245001 "No current problems or disability". Specific
codes are still allowed; however, use of negationInd is an alternative,
and the specific approach for each use will be specified in the
associated template.

.. _sect_5.3.4:

XML ID
~~~~~~

The XML Specification allows a markup tag to have an attribute of type
ID, whose value is unique within the document, that allows reference to
that markup. The CDA schema defines such attributes with attribute name
ID.

.. note::

   1. Thus the attribute named ID is of XML attribute type ID. This must
      further be distinguished from the element named id of HL7v3 Data
      Type UID that is part of most RIM classes. The attribute name is
      always upper case, the element name is always lower case.

   2. The actual CDA schema specification uses the XML Schema Datatypes
      definition of XML ID (xs:ID). Readers may also be familiar with
      the xml:id specification, which is not formally used by CDA as it
      was published after the CDA specification.

In the CDA R2 Specification, the XML ID attribute capability is applied
to the Section and observationMedia elements, and to various types of
narrative block markup, and is used to provide linkage between
structured entries and the corresponding narrative text (see `Section
Text <#sect_9.1.1>`__).

.. _sect_5.4:

Extension and Namespace
-----------------------

In accordance with CDA R2 (and HL7 v3 XML) extensibility rules, as
described in CDA R2 Section 1.4, "locally-defined" XML markup may be
specified where there is a need to communicate information for which
there is no suitable representation in CDA R2. These extensions are
described in the context of the templates where they are used. All such
extensions use HL7 v3 Data Types used by CDA R2.

.. note::

   The HL7 Structured Documents Working Group coordinates markup
   extensions that have been defined for implementation guides published
   by HL7, IHE, DICOM, and other organizations. See
   http://wiki.hl7.org/index.php?title=CDA_R2_Extensions

The namespace for extensions defined in this Standard is
"urn:dicom-org:ps3-20", which is aliased in this Standard as "ps3-20".
Extensions defined in this Standard are:

-  ps3-20:accessionNumber - The accessionNumber extension allows for the
   clear identification of the imaging department identifier for a
   service request (order). While this identifier could be conveyed as
   another id for the inFulfillmentOf/Order element, there is no
   reliable way in that context to distinguish it from the Placer Order
   Number. As this is a primary management identifier in departmental
   workflows, a distinct local markup is defined. This extension uses
   the II Data Type.

The namespace for extensions defined by HL7 is "urn:hl7-org:sdtc". which
is aliased in this Standard as "sdtc". HL7 defined extensions used in
this Standard are:

-  sdtc:signatureText - Provides a location for a textual or multimedia
   depiction of the signature by which the participant endorses and
   accepts responsibility for his or her participation in the Act as
   specified in the Participation.typeCode. Details of the element
   content are described in the HL7 CDA Digital Signature Standard. This
   extension uses the ED Data Type.

.. _sect_5.5:

Serialization Order of Elements
-------------------------------

The CDA schema requires elements to be encoded in a specified order,
which may be different than the order in which they are described in the
templates. The serialization of elements shall be in accordance with the
HL7 CDA Hierarchical Description. In particular, attention must be paid
to the serialization order of elements defined in sibling templates (see
`Context <#sect_5.1.2>`__).

.. note::

   For example, the various header templates are siblings, specifying
   sets of elements at the same hierarchical level. These elements of
   different templates must be encoded in their appropriate serialized
   order in the object instance - all templateID elements from the
   document template and all header templates first, followed by the
   elements of the clinicalDocument class in their prescribed order,
   followed by the participations in their prescribed order, followed by
   act relationships in their prescribed order.

