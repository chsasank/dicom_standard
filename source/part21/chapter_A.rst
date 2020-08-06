.. _chapter_A:

Transformation Between AIM and DICOM SR
=======================================

.. _sect_A.1:

Scope and Field of Application
------------------------------

NCI AIM objects that are constrained to specific use cases can be
transformed to DICOM SR documents that are based on .

NCI AIM specifies a generic model for encoding structured information
about medical images. The AIM model and its XML encoding are version
specific. The version transformed in this document is Version 4
`biblioentry_title <#biblio_AIM_Model_Extending>`__. Though AIM
instances can be generated according to application-specific templates
[ref. AIM template builder], such templates are too use-case specific to
be detailed in the transformation described in this Part. Rather, common
patterns of use implemented by well known implementations (ref. CC, ref
ePAD) have been abstracted and are mapped as described in this document.

DICOM SR specifies a generic model for encoding structured information
about DICOM instances. DICOM specifies a basic DICOM SR report template
for quantitative measurements and categorical statements for single
identifiable patient subjects including regions of interest defined by
spatial coordinates or segmentations.

.. _sect_A.2:

Use Cases
---------

The basic use case for the transformation from AIM to DICOM SR is
exchange of quantitative and categorical information about DICOM images
and regions of interest in DICOM images.

AIM and DICOM SR instances both contain references to DICOM images, and
both make use of references to other types of DICOM instances such as
segmentations. The flow of information between systems that might make
use of a conversion between AIM and DICOM SR instances is considered in
`figure_title <#figure_A.2-1>`__.

Various different transformation scenarios should be considered:

a. Transformation of a complete AIM instance to a complete DICOM SR
   Measurement Report. The receiver optionally selects relevant parts of
   the transformed document for further processing or static or
   interactive visualization by the user.

b. Transformation of a subset of a AIM instance to a DICOM SR
   Measurement Report. This subset comprises the relevant information
   for a specific use-case.

c. Transformation of multiple related AIM instances to a single DICOM SR
   Measurement Report. The selected related AIM instances comprise the
   relevant information for a specific use-case.

This Part of the Standard does not mandate any particular transformation
scenario. Transformations of various compatible components of AIM and
DICOM SR are described, allowing each of these scenarios to be
implemented as appropriate. This Part of the Standard enables a
deterministic transformation of the first scenario (complete mapping of
an AIM instance to DICOM).

The primary use-case for the transformation is that of:

-  taking an existing AIM instance containing one or more annotations,
   converting it into DICOM SR, storing it in a DICOM storage system,
   possibly displaying it with a DICOM SR aware application,
   transforming it back into an AIM instance after retrieval from the
   DICOM storage system, and reusing it in an AIM-aware application

An important secondary use-case is transformation of annotation
information in different formats into a single format for data
aggregation (e.g., "analytics", "data mining", "big data", "machine
learning", and "deep learning"). The conversion described here is
intended to allow preservation of semantics sufficient for such
purposes, regardless of the source format.

It should be understood that DICOM SR created by transforming an AIM
object will not necessarily be identical in structure and content to a
DICOM SR that might have been created *de novo* by a similar
application. For instance, there are various encoding choices that an
application implementer may make, especially with respect to the degree
of post-coordination of ROI and measurement descriptions, which might
result in different structures. It may not be possible to transform a
DICOM SR TID 1500 instance into AIM and retain all of its content.
Post-coordinated concepts, such as measurement and derivation methods,
may be preserved by using multiple CalculationEntity/typeCode entries or
by pre-coordinating into a single concept during the transformation.

Multiple regions of interest, or multiple measurements and categorical
statements about a single region of interest, or about the same real
world entity (e.g., lesion) identified with different regions of
interest (e.g., at different time points or with different modalities),
may be encoded in single or multiple AIM or DICOM SR instances. Whether
or not a source AIM or DICOM SR implementation encodes more than one
region of interest (and their accompanying measurements and categorical
statements) in a single instance or in separate instances, and whether
the conversion from one form to the other "bundles" multiple instances
into a single instance, or "unbundles" a single instance into multiple
instances, is not prescribed. The AIM 4.2 model allows for the encoding
of multiple marked up regions and multiple measurements in a single
annotation instance, and unlike earlier AIM model versions provides
mechanisms for identifying which markup is associated with which
measurement using AIM statements; otherwise it is necessary to assume
that all markup applies to all measurements and vice versa.

For example, for RECIST measurements that involve the long and short
axis of a lesion, it is not only possible to encode in AIM (and map to
TID 1500) the boundaries of and the area measurements derived from a
planar volumetric ROI, it is also possible to encode the endpoints of
the measured axes of the pair of linear measurements and their derived
values.

.. _sect_A.3:

Structure of DICOM SR Documents
-------------------------------

DICOM SR documents can be thought of as consisting of a document header
and a document body. The header metadata Attribute values are grouped
into Modules such as "Patient", "General Study" in .

The SR Document Content Module () contains the Attributes for the root
Content Item, which includes the coded report title. The Content Tree
(structured content) of the document body is contained in the nested
Content Sequence Items of that Module. "Container" Content Items are
part of the Content Sequence. They are structural elements of the SR
document body structure. Content items are DICOM SR document nodes
within the Content Tree that are connected through "by-value"
relationships (for Enhanced SR IODs). The transformations defined in
this Part do not support the use of "by-reference" relationships between
Content Items.

.. _sect_A.3.1:

Header
~~~~~~

The Modules used in a DICOM SR are defined by the Information Object
Definition (IOD). A particular DICOM SR template may be encoded using a
variety of DICOM SR IODs, depending on the features supported by the
template and used by a particular instance. Each SR IOD constrains the
Value Types and Relationship Types that are permitted. The Enhanced SR
IOD is sufficient to encode TID 1500 instances unless 3D
patient-relative coordinates (rather than 2D image-relative coordinates
or segmentations) are used to define regions of interest on images, in
which case use of the Comprehensive 3D SR IOD or Extensible SR IOD would
be required.

`table_title <#table_A.3.1-1>`__ summarizes the Modules common to the SR
IODs that can encode the as specified in .

.. table:: Transformation of DICOM SR IOD Modules

   +-------------+-------------+-----------+-------------+-------------+
   | IE          | Module      | Reference | Usage       | Tra         |
   |             |             |           |             | nsformation |
   +=============+=============+===========+=============+=============+
   | Patient     | Patient     |           | M           | `Mapping of |
   |             |             |           |             | DICOM       |
   |             |             |           |             | Patient     |
   |             |             |           |             | Modul       |
   |             |             |           |             | e <#sect_A. |
   |             |             |           |             | 6.1.1.1>`__ |
   +-------------+-------------+-----------+-------------+-------------+
   | Clinical    |             | U         | `Mapping of |             |
   | Trial       |             |           | DICOM       |             |
   | Subject     |             |           | Clinical    |             |
   |             |             |           | Trial       |             |
   |             |             |           | Subject     |             |
   |             |             |           | Modul       |             |
   |             |             |           | e <#sect_A. |             |
   |             |             |           | 6.1.1.2>`__ |             |
   +-------------+-------------+-----------+-------------+-------------+
   | Study       | General     |           | M           | `Mapping of |
   |             | Study       |           |             | DICOM       |
   |             |             |           |             | General     |
   |             |             |           |             | Study       |
   |             |             |           |             | Modul       |
   |             |             |           |             | e <#sect_A. |
   |             |             |           |             | 6.1.1.3>`__ |
   +-------------+-------------+-----------+-------------+-------------+
   | Patient     |             | U         | `Mapping of |             |
   | Study       |             |           | DICOM       |             |
   |             |             |           | Patient     |             |
   |             |             |           | Study       |             |
   |             |             |           | Modul       |             |
   |             |             |           | e <#sect_A. |             |
   |             |             |           | 6.1.1.4>`__ |             |
   +-------------+-------------+-----------+-------------+-------------+
   | Clinical    |             | U         | `Mapping of |             |
   | Trial Study |             |           | DICOM       |             |
   |             |             |           | Clinical    |             |
   |             |             |           | Trial Study |             |
   |             |             |           | Modul       |             |
   |             |             |           | e <#sect_A. |             |
   |             |             |           | 6.1.1.5>`__ |             |
   +-------------+-------------+-----------+-------------+-------------+
   | Series      | SR Document |           | M           | `Mapping of |
   |             | Series      |           |             | DICOM SR    |
   |             |             |           |             | Document    |
   |             |             |           |             | Series      |
   |             |             |           |             | Modul       |
   |             |             |           |             | e <#sect_A. |
   |             |             |           |             | 6.1.1.6>`__ |
   +-------------+-------------+-----------+-------------+-------------+
   | Clinical    |             | U         | `Mapping of |             |
   | Trial       |             |           | DICOM       |             |
   | Series      |             |           | Clinical    |             |
   |             |             |           | Trial       |             |
   |             |             |           | Series      |             |
   |             |             |           | Modul       |             |
   |             |             |           | e <#sect_A. |             |
   |             |             |           | 6.1.1.7>`__ |             |
   +-------------+-------------+-----------+-------------+-------------+
   | Equipment   | General     |           | M           | `Mapping of |
   |             | Equipment   |           |             | DICOM       |
   |             |             |           |             | General     |
   |             |             |           |             | Equipment   |
   |             |             |           |             | Modul       |
   |             |             |           |             | e <#sect_A. |
   |             |             |           |             | 6.1.1.8>`__ |
   +-------------+-------------+-----------+-------------+-------------+
   | Document    | SR Document |           | M           | `Mapping of |
   |             | General     |           |             | DICOM SR    |
   |             |             |           |             | Document    |
   |             |             |           |             | General     |
   |             |             |           |             | Modul       |
   |             |             |           |             | e <#sect_A. |
   |             |             |           |             | 6.1.1.9>`__ |
   +-------------+-------------+-----------+-------------+-------------+
   | SR Document |             | M         | `Mapping of |             |
   | Content     |             |           | DICOM SR    |             |
   |             |             |           | Document    |             |
   |             |             |           | Content     |             |
   |             |             |           | Module      |             |
   |             |             |           |  <#sect_A.6 |             |
   |             |             |           | .1.1.10>`__ |             |
   +-------------+-------------+-----------+-------------+-------------+
   | SOP Common  |             | M         | `Mapping of |             |
   |             |             |           | DICOM SOP   |             |
   |             |             |           | Common      |             |
   |             |             |           | Module      |             |
   |             |             |           |  <#sect_A.6 |             |
   |             |             |           | .1.1.11>`__ |             |
   +-------------+-------------+-----------+-------------+-------------+

**Patient Module**

The Patient Module specifies the Attributes of the Patient that describe
and identify the Patient who is the subject of a Study. This Module
contains Attributes of the patient that are needed for interpretation of
the Image and are common for all studies performed on the patient.

**Clinical Trial Subject Module**

The Clinical Trial Subject Module contains Attributes that identify a
Patient as a clinical trial Subject.

**General Study Module**

The General Study Module specifies the Attributes that describe and
identify the Study performed upon the Patient.

**Patient Study Module**

The Patient Study Module defines the Attributes that provide information
about the Patient at the time the Study was performed.

**Clinical Trial Study Module**

The Clinical Trial Study Module contains Attributes that identify a
Study in the context of a clinical trial.

**SR Document Series Module**

The SR Document Series Module defines the Attributes of the SR Document
Series. A Series of SR Documents may contain any number of SR Documents.

**Clinical Trial Series Module**

The Clinical Trial Series Module contains Attributes that identify a
Series in the context of a clinical trial.

**General Equipment Module**

The General Equipment Module specifies the Attributes that identify and
describe the piece of equipment that produced a Series of Composite
Instances.

**SR Document General Module**

The SR Document General Module defines the general Attributes of an SR
Document Instance. These Attributes identify the SR Document and provide
context for the entire document.

**SOP Common Module**

The SOP Common Module defines the Attributes that are required for
proper functioning and identification of the associated SOP Instances.

**SR Document Content Module**

The Attributes in this Module convey the content of an SR Document. It
specifies the root Content Item and the Content Tree (refer to
`figure_title <#figure_A.3-1>`__).

.. _sect_A.3.2:

Document Body
~~~~~~~~~~~~~

The document body is the information that is stored in the DICOM SR
Content Tree. The Content Tree is encoded in the SR Document Content
Module.

.. _sect_A.3.2.1:

DICOM SR "Measurement Report" Template Structure
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

is the top-level template of the DICOM SR Measurement Report (). It
includes sub-templates as shown in `figure_title <#figure_A.3.2.1-1>`__.

.. note::

   1. The use of TID 1001 Observation Context within TID 1000 Quotation
      is not shown because it is not relevant to the mapping use cases.

   2. The use of TID 311 Measurement Statistical Properties and TID 312
      Normal Range Properties within TID 310 Measurement Properties is
      not shown because it is not relevant to the mapping use cases.

   3. The use of TID 1410 Planar ROI Measurements, TID 1411 Volumetric
      ROI Measurements, and TID 310 Measurement Properties within TID
      1420 is not shown because it is not relevant to the mapping use
      cases.

.. _sect_A.3.2.2:

Mapping Considerations
^^^^^^^^^^^^^^^^^^^^^^

The goal of this document is to specify a mapping between constrained
AIM v4 instances and DICOM SR documents. The following limitations apply
to AIM instances that are mapped to DICOM SR Measurement Reports:

-  Subject Context: The DICOM SR TID 1500 Measurement Report is
   restricted to cover exactly one patient subject; the mapping of
   subject context of fetuses, specimens or devices as subjects is out
   of scope. Small or large animal identifiers and descriptors (beyond
   reuse of the normal patient identifiers) are not specifically
   addressed since no such identifiers are present in the AIM model
   (e.g., multiple animals imaged as one, and strain descriptions are
   out of scope).

-  The mapping of DICOM SR clinical trial header data (Clinical Trial
   Subject Module, Clinical Trial Study Module, Clinical Trial Series
   Module) is not described since no such identifiers are present in the
   AIM model.

-  The transformation of de-identified objects is not specifically
   addressed in this mapping, since AIM does not address encoding of the
   history of de-identification explicitly. I.e., identifiers will be
   converted unchanged and whether they have been de-identified will not
   be explicitly signaled.

-  A subset of spatial coordinate types are mapped, to the extent that
   both AIM and DICOM SR support the same graphic concepts.

.. _sect_A.3.2.3:

DICOM Composite Object References
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

The hierarchical Attributes describing DICOM composite object references
are used whenever DICOM composite objects are referenced in the Content
Tree and are also described in the Image Library templates and the
Current Requested Procedure Evidence Sequence (0040,A375) or Pertinent
Other Evidence Sequence (0040,A385). Information on relevant DICOM
objects referenced within the AIM instance are included in the AIM
DicomImageReferenceEntity class.

.. _sect_A.4:

Structure of AIM Version 4 Instances
------------------------------------

AIM instances are encoded in XML according to a schema generated from
the AIM Model `biblioentry_title <#biblio_AIM_Model_v4_2>`__, which is
defined in UML. `figure_title <#figure_A.4-1>`__ is a simplified view
rather than the entire model, showing only those UML classes and
attributes relevant to the transformations described in this Part.

.. _sect_A.5:

AIM v4 Structure
----------------

Version 4 of AIM makes use of `biblioentry_title <#biblio_ISO_21090>`__
data types. See `Overview of Data Types <#sect_A.8>`__.

.. _sect_A.6:

AIM v4 to DICOM TID 1500 Mapping
--------------------------------

The transformation is described in one direction, by enumerating the
structures in the target (DICOM SR TID 1500) and describing where in the
source (AIM v4) the corresponding information may be obtained. The
information is tabulated in a manner that can be implemented as an
automated "pull" conversion of an AIM instance into a DICOM SR instance,
such as might be described using a transformation language such as XSLT.
The transformation is intended to be reversible, i.e., by inverting the
target and the source, even though round-trip full fidelity will not be
achieved in some cases. Gaps that exist in the information required in
the target to create a compliant object, which need to be filled by
information from an out of band source or generated *de novo*, are
highlighted. Information in the source that is not "pulled" into the
DICOM encoding will be lost; these omissions are deemed to be harmless
from the perspective of the relevant use cases.

The tabular representations make use of the following conventions in
order to simplify the automatic extraction and use as a formal syntax to
drive implementations:

-  DICOM Attributes are represented by keywords defined in , rather than
   specifying the data element group and element tags.

-  DICOM Attributes that are nested within sequences are shown as a path
   from the top level Data Set separated by a ">" symbol.

-  AIM classes, attributes and associations are represented using their
   XPath representation as encoded in XML instances.

-  DICOM Code Sequence Attributes are mapped from AIM CD data type
   attributes without fully enumerating the corresponding subordinate
   DICOM Attributes and XML elements and attributes.

-  Other DICOM Sequences are listed, without a mapping on the same row,
   but with the following rows describing the individual DICOM
   Attributes nested within that Sequence.

-  All source and target paths are fully qualified relative to the root
   of the instance in order to make the transformation reversible. I.e.,
   it would be possible to describe some transformations using the
   descendant-or-self axis XSLT operator ("//") if the source were
   unambiguous but that would not specify the location reversibly as a
   target. Accordingly, some of the explicit paths are quite long.

-  The requirement type for DICOM Attributes is as defined in PS3.3 for
   Attributes in Modules and Attribute Macros, except that if the
   containing Module in the IOD is not required, e.g., is U rather than
   M, then a mandatory (Type 1 or 2) Attribute in a user optional (type
   U) Module is shown as optional (Type 3).

-  The data type and cardinality are specified for both the source and
   the target, to highlight potential mismatches that may occur during
   transformation. For nested elements and attributes, the multiplicity
   is expressed as the combination of the multiplicity along the entire
   path. For example, the aim:name attribute has a multiplicity of 1:1
   in an aim:Person class but is associated with the
   aim:Image​AnnotationClass with a multiplicity of 1 -> 0:1, so the
   multiplicity is indicated as 0:1, not 1:1, since that is the net
   effect. The DICOM multiplicity is either the VM for the data element
   or the number of Sequence Items if the data element is a Sequence.

   The XML representation of the AIM UML collapses some associations and
   classes such that they are encoded as a single element, and this is
   reflected in the mapping paths. For example, the aim:Person class has
   an aim:person association from the aim:Image​AnnotationCollection
   class, so the path to the aim:name attribute is expressed as
   /Image​AnnotationCollection/​person/​name, as it appears in the XML
   instance.

-  Data type transformations are assumed and are not described further
   unless there is a specific requirement. For example, conversion from
   DICOM DA, TM and DT VR Attributes to AIM TS Data Type values is
   implicit, including extraction/​population of the appropriate
   sub-fields (i.e., only the date portion of a TS is used when creating
   a DICOM DA value).

-  If value sets are defined for both AIM and DICOM, then value mappings
   are described. In some cases, explicit value sets are not defined.
   For example, aim:Person/​sex has no explicitly defined value set but
   maps to DICOM PatientSex, which does; so if AIM implementations use
   the DICOM values, and the values are copied, then the transformation
   without value mapping will be successful, but not otherwise.

-  When a mapping is defined but no transformation source is available
   but a value is required, a Generated Value is indicated, which may be
   a fixed constant (e.g., a Modality value of "SR"), an indication that
   an empty (zero length) value or sequence is required, or an
   indication that a new value of the appropriate VR needs to be
   generated (e.g., a new UID for a UI VR, a new integer for an IS VR,
   etc.). The need to generate new values will not produce a
   deterministic result without a memory of previous conversions.

-  Optional content in the target that has no defined source is not
   described (e.g., DICOM SeriesDescription in the General Series Module
   has no correlate in AIM, though it would be useful to populate with a
   generated value).

-  When the same DICOM Attribute is described in two different Modules,
   the more specialized (restrictive) use is described in the mapping
   tables. E.g., InstanceNumber is Type 3 in the SOP Common Module but
   Type 1 in the SR Document General Module, so it is only described in
   the latter.

-  Capitalization and punctuation of DICOM keywords and AIM class,
   attribute and association names are significant.

.. _sect_A.6.1:

Mapping of Constrained AIM v4
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

.. _sect_A.6.1.1:

Header
^^^^^^

General Remarks on the mapping of DICOM header Module Attributes:

**SR Document General Module**

-  Mapped AIM objects are considered "unverified", so there is no
   requirement to record the identity of the Verifying Observer; if the
   "recording" observer identity is required (aim:user class attributes)
   it may be mapped to Author Observer Sequence (0040,A078) in the SR
   Document General Module (and entries in Observation Context in the
   Content Tree are not needed).

-  Attributes of the Predecessor Documents Sequence (0040,A360) and
   Identical Documents Sequence (0040,A525) are not described in this
   transformation since they are relevant only in the context of a
   managed DICOM SR document environment and have no correlate in AIM.

-  Attributes of the Current Requested Procedure Evidence Sequence
   (0040,A375) and Pertinent Other Evidence Sequence (0040,A385) are
   described in the transformation and provide the information described
   in the Hierarchical SOP Instance Reference Macro used to match
   composite instance references with their Study and Series context;
   the AIM DicomImageReferenceEntity class performs a similar function.

-  Attributes of the Equivalent Document Sequence (0040,A090) are not
   described in the transformation since they are relevant only in the
   context of the original DICOM SR document.

   The name space of the AIM elements is elided, and is implied to be
   "gme://caCORE.caCORE/4.4/edu.northwestern.radiology.AIM".

**SOP Common Module**

-  Timezone Offset From UTC (0008,0201) shall be considered for
   Attributes of the DICOM SR document that are based on the DA or TM
   data type (). AIM date and time attributes may or may not contain
   explicit timezone information that may be extracted to populate
   Timezone Offset From UTC (0008,0201).

-  The Specific Character Set (0008,0005) is required (Type 1C), if the
   Basic Graphic Set is expanded or replaced. This is the basis for
   mapping DICOM character sets to AIM XML Unicode (<?xml version="1.0"
   encoding="UTF-8"?>).

   .. note::

      Ambiguities exist for mapping individual characters to Unicode
      (e.g., for Japanese characters). Resolution of those issues is
      beyond the scope of this document. Please refer to `Overview of
      Data Types <#sect_A.8>`__ for further details on data types and
      character sets.

.. _sect_A.6.1.1.1:

Mapping of DICOM Patient Module
'''''''''''''''''''''''''''''''

.. table:: Mapping of DICOM Patient Module

   +-------+-------+-------+-------+-------+-------+-------+-------+-------+
   | DICOM | DICOM | DICOM | DICOM | Gene  | AIM   | AIM   | AIM   | Co    |
   | Attr  | VR    | VM    | Usage | rated | El    | Data  | Mu    | mment |
   | ibute |       |       | Type  | Value | ement | Type  | ltipl |       |
   |       |       |       |       |       | or    |       | icity |       |
   |       |       |       |       |       | Attr  |       |       |       |
   |       |       |       |       |       | ibute |       |       |       |
   +=======+=======+=======+=======+=======+=======+=======+=======+=======+
   | P     | PN    | 1     | 2     |       | Image | ST    | 0..1  |       |
   | atien |       |       |       |       | ​Anno |       |       |       |
   | tName |       |       |       |       | tatio |       |       |       |
   |       |       |       |       |       | n​​Co |       |       |       |
   |       |       |       |       |       | llect |       |       |       |
   |       |       |       |       |       | ion/​ |       |       |       |
   |       |       |       |       |       | perso |       |       |       |
   |       |       |       |       |       | n/​na |       |       |       |
   |       |       |       |       |       | me/​@ |       |       |       |
   |       |       |       |       |       | value |       |       |       |
   +-------+-------+-------+-------+-------+-------+-------+-------+-------+
   | Pati  | LO    | 1     | 2     |       | Ima   | ST    | 0..1  |       |
   | entID |       |       |       |       | ge​An |       |       |       |
   |       |       |       |       |       | notat |       |       |       |
   |       |       |       |       |       | ion​​ |       |       |       |
   |       |       |       |       |       | Colle |       |       |       |
   |       |       |       |       |       | ction |       |       |       |
   |       |       |       |       |       | /​per |       |       |       |
   |       |       |       |       |       | son/​ |       |       |       |
   |       |       |       |       |       | id/​@ |       |       |       |
   |       |       |       |       |       | value |       |       |       |
   +-------+-------+-------+-------+-------+-------+-------+-------+-------+
   | P     | DA    | 1     | 2     |       | Image | TS    | 0..1  |       |
   | atien |       |       |       |       | ​Anno |       |       |       |
   | tBirt |       |       |       |       | tatio |       |       |       |
   | hDate |       |       |       |       | n​​Co |       |       |       |
   |       |       |       |       |       | llect |       |       |       |
   |       |       |       |       |       | ion/​ |       |       |       |
   |       |       |       |       |       | perso |       |       |       |
   |       |       |       |       |       | n/​bi |       |       |       |
   |       |       |       |       |       | rthDa |       |       |       |
   |       |       |       |       |       | te/​@ |       |       |       |
   |       |       |       |       |       | value |       |       |       |
   +-------+-------+-------+-------+-------+-------+-------+-------+-------+
   | Patie | CS    | 1     | 2     |       | Imag  | ST    | 0..1  |       |
   | ntSex |       |       |       |       | e​Ann |       |       |       |
   |       |       |       |       |       | otati |       |       |       |
   |       |       |       |       |       | on​​C |       |       |       |
   |       |       |       |       |       | ollec |       |       |       |
   |       |       |       |       |       | tion/ |       |       |       |
   |       |       |       |       |       | ​pers |       |       |       |
   |       |       |       |       |       | on/​s |       |       |       |
   |       |       |       |       |       | ex/​@ |       |       |       |
   |       |       |       |       |       | value |       |       |       |
   +-------+-------+-------+-------+-------+-------+-------+-------+-------+
   | E     | SH    | 1     | 3     |       | Im    | ST    | 0..1  |       |
   | thnic |       |       |       |       | age​A |       |       |       |
   | Group |       |       |       |       | nnota |       |       |       |
   |       |       |       |       |       | tion​ |       |       |       |
   |       |       |       |       |       | ​Coll |       |       |       |
   |       |       |       |       |       | ectio |       |       |       |
   |       |       |       |       |       | n/​pe |       |       |       |
   |       |       |       |       |       | rson/ |       |       |       |
   |       |       |       |       |       | ​ethn |       |       |       |
   |       |       |       |       |       | icGro |       |       |       |
   |       |       |       |       |       | up/​@ |       |       |       |
   |       |       |       |       |       | value |       |       |       |
   +-------+-------+-------+-------+-------+-------+-------+-------+-------+
   | Sourc | SQ    | 1     | 3     |       | I     | ST    | 0..1  |       |
   | e​Pat |       |       |       |       | mage​ |       |       |       |
   | ient​ |       |       |       |       | Annot |       |       |       |
   | Group |       |       |       |       | ation |       |       |       |
   | ​Iden |       |       |       |       | ​​Col |       |       |       |
   | tific |       |       |       |       | lecti |       |       |       |
   | ation |       |       |       |       | on/​p |       |       |       |
   | ​Sequ |       |       |       |       | erson |       |       |       |
   | ence> |       |       |       |       | /​sou |       |       |       |
   | Patie |       |       |       |       | rce​P |       |       |       |
   | nt​ID |       |       |       |       | atien |       |       |       |
   |       |       |       |       |       | t​Gro |       |       |       |
   |       |       |       |       |       | up​Id |       |       |       |
   +-------+-------+-------+-------+-------+-------+-------+-------+-------+

.. note::

   If the annotation concerns a small animal that has been imaged as
   part of a group of animals in the same image, then the PatientID and
   other Attributes of this Module will be those of that individual
   animal, not the group. The AIM 4.2 model can optionally identify the
   group of animals imaged at the same time that corresponds to the
   DICOM SourcePatientGroupIdentificationSequence.

.. _sect_A.6.1.1.2:

Mapping of DICOM Clinical Trial Subject Module
''''''''''''''''''''''''''''''''''''''''''''''

No mapping of the DICOM Clinical Trial Subject Module is described since
no corresponding content is present in the AIM model.

.. _sect_A.6.1.1.3:

Mapping of DICOM General Study Module
'''''''''''''''''''''''''''''''''''''

The AIM 4.2 model provides optional Study identification information. If
available, this information shall be used during transformation from AIM
to SR, otherwise either a new Study may be generated, or the SR instance
derived from the AIM object could be placed in (one of) the Study(ies)
referenced by the AIM instance, assuming there are any, which produces a
predictable transformation.

If there is more than one DICOM Study referenced by the AIM object and
explicit Study identification information
(Image​Annotation​​Collection/​study​Instance​Uid) is absent, duplicates
of the converted AIM SR instance may be placed in each of the referenced
studies (with different SOP Instance UIDs), in which case the
IdenticalDocumentsSequence is required in the SR Document General
Module; see .

.. table:: Mapping of DICOM General Study Module

   +-------+-------+-------+-------+-------+-------+-------+-------+-------+
   | DICOM | DICOM | DICOM | DICOM | Gene  | AIM   | Data  | Mu    | Co    |
   | Attr  | VR    | VM    | Usage | rated | El    | Type  | ltipl | mment |
   | ibute |       |       | Type  | Value | ement |       | icity |       |
   |       |       |       |       |       | or    |       |       |       |
   |       |       |       |       |       | Attr  |       |       |       |
   |       |       |       |       |       | ibute |       |       |       |
   +=======+=======+=======+=======+=======+=======+=======+=======+=======+
   | S     | UI    | 1     | 1     | New   | Image | II    | 0..1  |       |
   | tudyI |       |       |       | or    | ​Anno |       |       |       |
   | nstan |       |       |       | de    | tatio |       |       |       |
   | ceUID |       |       |       | rived | n​​Co |       |       |       |
   |       |       |       |       | from  | llect |       |       |       |
   |       |       |       |       | refer | ion/​ |       |       |       |
   |       |       |       |       | enced | study |       |       |       |
   |       |       |       |       | image | ​Inst |       |       |       |
   |       |       |       |       | if    | ance​ |       |       |       |
   |       |       |       |       | not   | Uid/​ |       |       |       |
   |       |       |       |       | in    | @root |       |       |       |
   |       |       |       |       | s     |       |       |       |       |
   |       |       |       |       | ource |       |       |       |       |
   +-------+-------+-------+-------+-------+-------+-------+-------+-------+
   | Stud  | UI    | 1     | 2     | Empty | Ima   | TS    | 0..1  |       |
   | yDate |       |       |       | if    | ge​An |       |       |       |
   |       |       |       |       | not   | notat |       |       |       |
   |       |       |       |       | in    | ion​​ |       |       |       |
   |       |       |       |       | s     | Colle |       |       |       |
   |       |       |       |       | ource | ction |       |       |       |
   |       |       |       |       |       | /​ima |       |       |       |
   |       |       |       |       |       | ge​An |       |       |       |
   |       |       |       |       |       | notat |       |       |       |
   |       |       |       |       |       | ions/ |       |       |       |
   |       |       |       |       |       | ​Imag |       |       |       |
   |       |       |       |       |       | e​Ann |       |       |       |
   |       |       |       |       |       | otati |       |       |       |
   |       |       |       |       |       | on[1] |       |       |       |
   |       |       |       |       |       | /​ima |       |       |       |
   |       |       |       |       |       | ge​Re |       |       |       |
   |       |       |       |       |       | feren |       |       |       |
   |       |       |       |       |       | ce​En |       |       |       |
   |       |       |       |       |       | tity​ |       |       |       |
   |       |       |       |       |       | ​Coll |       |       |       |
   |       |       |       |       |       | ectio |       |       |       |
   |       |       |       |       |       | n/​Im |       |       |       |
   |       |       |       |       |       | ageRe |       |       |       |
   |       |       |       |       |       | feren |       |       |       |
   |       |       |       |       |       | ceEnt |       |       |       |
   |       |       |       |       |       | ity[1 |       |       |       |
   |       |       |       |       |       | ]/​im |       |       |       |
   |       |       |       |       |       | ageSt |       |       |       |
   |       |       |       |       |       | udy[1 |       |       |       |
   |       |       |       |       |       | ]/​st |       |       |       |
   |       |       |       |       |       | artDa |       |       |       |
   |       |       |       |       |       | te/​@ |       |       |       |
   |       |       |       |       |       | value |       |       |       |
   +-------+-------+-------+-------+-------+-------+-------+-------+-------+
   | Stud  | UI    | 1     | 2     | Empty | Ima   | TS    | 0..1  |       |
   | yTime |       |       |       | if    | ge​An |       |       |       |
   |       |       |       |       | not   | notat |       |       |       |
   |       |       |       |       | in    | ion​​ |       |       |       |
   |       |       |       |       | s     | Colle |       |       |       |
   |       |       |       |       | ource | ction |       |       |       |
   |       |       |       |       |       | /​ima |       |       |       |
   |       |       |       |       |       | ge​An |       |       |       |
   |       |       |       |       |       | notat |       |       |       |
   |       |       |       |       |       | ions/ |       |       |       |
   |       |       |       |       |       | ​Imag |       |       |       |
   |       |       |       |       |       | e​Ann |       |       |       |
   |       |       |       |       |       | otati |       |       |       |
   |       |       |       |       |       | on[1] |       |       |       |
   |       |       |       |       |       | /​ima |       |       |       |
   |       |       |       |       |       | ge​Re |       |       |       |
   |       |       |       |       |       | feren |       |       |       |
   |       |       |       |       |       | ce​En |       |       |       |
   |       |       |       |       |       | tity​ |       |       |       |
   |       |       |       |       |       | ​Coll |       |       |       |
   |       |       |       |       |       | ectio |       |       |       |
   |       |       |       |       |       | n/​Im |       |       |       |
   |       |       |       |       |       | ageRe |       |       |       |
   |       |       |       |       |       | feren |       |       |       |
   |       |       |       |       |       | ceEnt |       |       |       |
   |       |       |       |       |       | ity[1 |       |       |       |
   |       |       |       |       |       | ]/​im |       |       |       |
   |       |       |       |       |       | ageSt |       |       |       |
   |       |       |       |       |       | udy[1 |       |       |       |
   |       |       |       |       |       | ]/​st |       |       |       |
   |       |       |       |       |       | artTi |       |       |       |
   |       |       |       |       |       | me/​@ |       |       |       |
   |       |       |       |       |       | value |       |       |       |
   +-------+-------+-------+-------+-------+-------+-------+-------+-------+
   | Refe  | PN    | 1     | 2     | Empty |       |       |       | Not   |
   | rring |       |       |       |       |       |       |       | in    |
   | ​Phys |       |       |       |       |       |       |       | AIM.  |
   | ician |       |       |       |       |       |       |       |       |
   | ​Name |       |       |       |       |       |       |       |       |
   +-------+-------+-------+-------+-------+-------+-------+-------+-------+
   | Stu   | SH    | 1     | 2     | Empty |       |       |       | Not   |
   | dy​ID |       |       |       |       |       |       |       | in    |
   |       |       |       |       |       |       |       |       | AIM.  |
   +-------+-------+-------+-------+-------+-------+-------+-------+-------+
   | A     | SH    | 1     | 2     | Empty |       |       |       | Imag  |
   | ccess |       |       |       | if    |       |       |       | e​Ann |
   | ion​N |       |       |       | not   |       |       |       | otati |
   | umber |       |       |       | in    |       |       |       | on​​C |
   |       |       |       |       | s     |       |       |       | ollec |
   |       |       |       |       | ource |       |       |       | tion/ |
   |       |       |       |       |       |       |       |       | acces |
   |       |       |       |       |       |       |       |       | sion​ |
   |       |       |       |       |       |       |       |       | Numbe |
   |       |       |       |       |       |       |       |       | r/​@v |
   |       |       |       |       |       |       |       |       | alue. |
   +-------+-------+-------+-------+-------+-------+-------+-------+-------+

.. _sect_A.6.1.1.4:

Mapping of DICOM Patient Study Module
'''''''''''''''''''''''''''''''''''''

No mapping of the DICOM Patient Study Module is described since no
corresponding content is present in the AIM model.

.. _sect_A.6.1.1.5:

Mapping of DICOM Clinical Trial Study Module
''''''''''''''''''''''''''''''''''''''''''''

No mapping of the DICOM Clinical Trial Study Module is described since
no corresponding content is present in the AIM model.

.. _sect_A.6.1.1.6:

Mapping of DICOM SR Document Series Module
''''''''''''''''''''''''''''''''''''''''''

The AIM 4.2 model optionally supports the concept that an annotation
itself is part of a Series. If available, this information shall be
used, otherwise a new Series shall be generated since a converted
instance cannot be made part of a referenced image Series, if any,
because of the rule that all instances of a Series are generated on the
same Equipment.

.. table:: Mapping of DICOM SR Document Series Module

   +-------+-------+-------+-------+-------+-------+-------+-------+-------+
   | DICOM | DICOM | DICOM | DICOM | Gene  | AIM   | AIM   | AIM   | Co    |
   | Attr  | VR    | VM    | Usage | rated | El    | Data  | Mu    | mment |
   | ibute |       |       | Type  | Value | ement | Type  | ltipl |       |
   |       |       |       |       |       | or    |       | icity |       |
   |       |       |       |       |       | Attr  |       |       |       |
   |       |       |       |       |       | ibute |       |       |       |
   +=======+=======+=======+=======+=======+=======+=======+=======+=======+
   | Mod   | CS    | 1     | 1     | "SR"  |       |       |       |       |
   | ality |       |       |       |       |       |       |       |       |
   +-------+-------+-------+-------+-------+-------+-------+-------+-------+
   | Seri  | UI    | 1     | 1     | New   | I     | II    | 0..1  | Using |
   | es​In |       |       |       | if    | mage​ |       |       | a     |
   | stanc |       |       |       | not   | Annot |       |       | gene  |
   | e​UID |       |       |       | in    | ation |       |       | rated |
   |       |       |       |       | so    | ​​Col |       |       | value |
   |       |       |       |       | urce. | lecti |       |       | means |
   |       |       |       |       |       | on/​s |       |       | that  |
   |       |       |       |       |       | eries |       |       | mul   |
   |       |       |       |       |       | ​Inst |       |       | tiple |
   |       |       |       |       |       | ance​ |       |       | r     |
   |       |       |       |       |       | Uid/​ |       |       | ound- |
   |       |       |       |       |       | @root |       |       | trips |
   |       |       |       |       |       |       |       |       | may   |
   |       |       |       |       |       |       |       |       | pr    |
   |       |       |       |       |       |       |       |       | oduce |
   |       |       |       |       |       |       |       |       | diff  |
   |       |       |       |       |       |       |       |       | erent |
   |       |       |       |       |       |       |       |       | va    |
   |       |       |       |       |       |       |       |       | lues. |
   |       |       |       |       |       |       |       |       |       |
   |       |       |       |       |       |       |       |       | When  |
   |       |       |       |       |       |       |       |       | ma    |
   |       |       |       |       |       |       |       |       | pping |
   |       |       |       |       |       |       |       |       | mul   |
   |       |       |       |       |       |       |       |       | tiple |
   |       |       |       |       |       |       |       |       | AIM   |
   |       |       |       |       |       |       |       |       | inst  |
   |       |       |       |       |       |       |       |       | ances |
   |       |       |       |       |       |       |       |       | re    |
   |       |       |       |       |       |       |       |       | lated |
   |       |       |       |       |       |       |       |       | to    |
   |       |       |       |       |       |       |       |       | the   |
   |       |       |       |       |       |       |       |       | same  |
   |       |       |       |       |       |       |       |       | s     |
   |       |       |       |       |       |       |       |       | tudy, |
   |       |       |       |       |       |       |       |       | if    |
   |       |       |       |       |       |       |       |       | the   |
   |       |       |       |       |       |       |       |       | same  |
   |       |       |       |       |       |       |       |       | Se    |
   |       |       |       |       |       |       |       |       | riesI |
   |       |       |       |       |       |       |       |       | nstan |
   |       |       |       |       |       |       |       |       | ceUID |
   |       |       |       |       |       |       |       |       | is    |
   |       |       |       |       |       |       |       |       | used  |
   |       |       |       |       |       |       |       |       | they  |
   |       |       |       |       |       |       |       |       | will  |
   |       |       |       |       |       |       |       |       | a     |
   |       |       |       |       |       |       |       |       | ppear |
   |       |       |       |       |       |       |       |       | in    |
   |       |       |       |       |       |       |       |       | the   |
   |       |       |       |       |       |       |       |       | same  |
   |       |       |       |       |       |       |       |       | Se    |
   |       |       |       |       |       |       |       |       | ries. |
   +-------+-------+-------+-------+-------+-------+-------+-------+-------+
   | Ser   | IS    | 1     | 1     | 7291  |       |       |       | A     |
   | ies​N |       |       |       |       |       |       |       | well- |
   | umber |       |       |       |       |       |       |       | known |
   |       |       |       |       |       |       |       |       | value |
   |       |       |       |       |       |       |       |       | means |
   |       |       |       |       |       |       |       |       | that  |
   |       |       |       |       |       |       |       |       | mul   |
   |       |       |       |       |       |       |       |       | tiple |
   |       |       |       |       |       |       |       |       | r     |
   |       |       |       |       |       |       |       |       | ound- |
   |       |       |       |       |       |       |       |       | trips |
   |       |       |       |       |       |       |       |       | will  |
   |       |       |       |       |       |       |       |       | use   |
   |       |       |       |       |       |       |       |       | the   |
   |       |       |       |       |       |       |       |       | same  |
   |       |       |       |       |       |       |       |       | v     |
   |       |       |       |       |       |       |       |       | alue. |
   +-------+-------+-------+-------+-------+-------+-------+-------+-------+
   | Refe  | SQ    | 1     | 2     | Empty |       |       |       |       |
   | rence |       |       |       |       |       |       |       |       |
   | d​Per |       |       |       |       |       |       |       |       |
   | forme |       |       |       |       |       |       |       |       |
   | d​Pro |       |       |       |       |       |       |       |       |
   | cedur |       |       |       |       |       |       |       |       |
   | e​Ste |       |       |       |       |       |       |       |       |
   | p​Seq |       |       |       |       |       |       |       |       |
   | uence |       |       |       |       |       |       |       |       |
   +-------+-------+-------+-------+-------+-------+-------+-------+-------+

.. _sect_A.6.1.1.7:

Mapping of DICOM Clinical Trial Series Module
'''''''''''''''''''''''''''''''''''''''''''''

No mapping of the DICOM Clinical Trial Series Module is described since
no corresponding content is present in the AIM model.

.. _sect_A.6.1.1.8:

Mapping of DICOM General Equipment Module
'''''''''''''''''''''''''''''''''''''''''

.. table:: Mapping of DICOM General Equipment Module

   +-------+-------+-------+-------+-------+-------+-------+-------+-------+
   | DICOM | DICOM | DICOM | DICOM | Gene  | AIM   | AIM   | AIM   | Co    |
   | Attr  | VR    | VM    | Usage | rated | El    | Data  | Mu    | mment |
   | ibute |       |       | Type  | Value | ement | Type  | ltipl |       |
   |       |       |       |       |       | or    |       | icity |       |
   |       |       |       |       |       | Attr  |       |       |       |
   |       |       |       |       |       | ibute |       |       |       |
   +=======+=======+=======+=======+=======+=======+=======+=======+=======+
   | Ma    | LO    | 1     | 2     |       | I     | ST    | 0..1  |       |
   | nufac |       |       |       |       | mage​ |       |       |       |
   | turer |       |       |       |       | Annot |       |       |       |
   |       |       |       |       |       | ation |       |       |       |
   |       |       |       |       |       | ​​Col |       |       |       |
   |       |       |       |       |       | lecti |       |       |       |
   |       |       |       |       |       | on/​e |       |       |       |
   |       |       |       |       |       | quipm |       |       |       |
   |       |       |       |       |       | ent/​ |       |       |       |
   |       |       |       |       |       | manuf |       |       |       |
   |       |       |       |       |       | actur |       |       |       |
   |       |       |       |       |       | er/​@ |       |       |       |
   |       |       |       |       |       | value |       |       |       |
   +-------+-------+-------+-------+-------+-------+-------+-------+-------+
   | M     | LO    | 1     | 3     |       | Image | ST    | 0..1  |       |
   | anufa |       |       |       |       | ​Anno |       |       |       |
   | cture |       |       |       |       | tatio |       |       |       |
   | rMode |       |       |       |       | n​​Co |       |       |       |
   | lName |       |       |       |       | llect |       |       |       |
   |       |       |       |       |       | ion/​ |       |       |       |
   |       |       |       |       |       | equip |       |       |       |
   |       |       |       |       |       | ment/ |       |       |       |
   |       |       |       |       |       | ​manu |       |       |       |
   |       |       |       |       |       | factu |       |       |       |
   |       |       |       |       |       | rerMo |       |       |       |
   |       |       |       |       |       | delNa |       |       |       |
   |       |       |       |       |       | me/​@ |       |       |       |
   |       |       |       |       |       | value |       |       |       |
   +-------+-------+-------+-------+-------+-------+-------+-------+-------+
   | S     | LO    | 1-n   | 3     |       | Imag  | ST    | 0..1  |       |
   | oftwa |       |       |       |       | e​Ann |       |       |       |
   | reVer |       |       |       |       | otati |       |       |       |
   | sions |       |       |       |       | on​​C |       |       |       |
   |       |       |       |       |       | ollec |       |       |       |
   |       |       |       |       |       | tion/ |       |       |       |
   |       |       |       |       |       | ​equi |       |       |       |
   |       |       |       |       |       | pment |       |       |       |
   |       |       |       |       |       | /​sof |       |       |       |
   |       |       |       |       |       | tware |       |       |       |
   |       |       |       |       |       | Versi |       |       |       |
   |       |       |       |       |       | on/​@ |       |       |       |
   |       |       |       |       |       | value |       |       |       |
   +-------+-------+-------+-------+-------+-------+-------+-------+-------+

.. _sect_A.6.1.1.9:

Mapping of DICOM SR Document General Module
'''''''''''''''''''''''''''''''''''''''''''

.. table:: Mapping of DICOM SR Document General Module

   +-------+-------+-------+-------+-------+-------+-------+-------+-------+
   | DICOM | DICOM | DICOM | DICOM | Gene  | AIM   | Data  | Mu    | Co    |
   | Attr  | VR    | VM    | Usage | rated | El    | Type  | ltipl | mment |
   | ibute |       |       | Type  | Value | ement |       | icity |       |
   |       |       |       |       |       | or    |       |       |       |
   |       |       |       |       |       | Attr  |       |       |       |
   |       |       |       |       |       | ibute |       |       |       |
   +=======+=======+=======+=======+=======+=======+=======+=======+=======+
   | Inst  | IS    | 1     | 1     | New   |       |       |       |       |
   | anceN |       |       |       |       |       |       |       |       |
   | umber |       |       |       |       |       |       |       |       |
   +-------+-------+-------+-------+-------+-------+-------+-------+-------+
   | Comp  | CS    | 1     | 1     | "COMP |       |       |       |       |
   | letio |       |       |       | LETE" |       |       |       |       |
   | nFlag |       |       |       |       |       |       |       |       |
   +-------+-------+-------+-------+-------+-------+-------+-------+-------+
   | V     | CS    | 1     | 1     | "U    |       |       |       | Se    |
   | erifi |       |       |       | NVERI |       |       |       | nding |
   | catio |       |       |       | FIED" |       |       |       | a     |
   | nFlag |       |       |       |       |       |       |       | value |
   |       |       |       |       |       |       |       |       | of    |
   |       |       |       |       |       |       |       |       | "VERI |
   |       |       |       |       |       |       |       |       | FIED" |
   |       |       |       |       |       |       |       |       | would |
   |       |       |       |       |       |       |       |       | tr    |
   |       |       |       |       |       |       |       |       | igger |
   |       |       |       |       |       |       |       |       | the   |
   |       |       |       |       |       |       |       |       | need  |
   |       |       |       |       |       |       |       |       | to    |
   |       |       |       |       |       |       |       |       | send  |
   |       |       |       |       |       |       |       |       | the   |
   |       |       |       |       |       |       |       |       | Veri  |
   |       |       |       |       |       |       |       |       | fying |
   |       |       |       |       |       |       |       |       | Obs   |
   |       |       |       |       |       |       |       |       | erver |
   |       |       |       |       |       |       |       |       | Sequ  |
   |       |       |       |       |       |       |       |       | ence, |
   |       |       |       |       |       |       |       |       | which |
   |       |       |       |       |       |       |       |       | is    |
   |       |       |       |       |       |       |       |       | not   |
   |       |       |       |       |       |       |       |       | desc  |
   |       |       |       |       |       |       |       |       | ribed |
   |       |       |       |       |       |       |       |       | in    |
   |       |       |       |       |       |       |       |       | this  |
   |       |       |       |       |       |       |       |       | map   |
   |       |       |       |       |       |       |       |       | ping. |
   +-------+-------+-------+-------+-------+-------+-------+-------+-------+
   | C     | DA    | 1     | 1     |       | I     | TS    | 1..1  |       |
   | onten |       |       |       |       | mage​ |       |       |       |
   | tDate |       |       |       |       | Annot |       |       |       |
   |       |       |       |       |       | ation |       |       |       |
   |       |       |       |       |       | ​​Col |       |       |       |
   |       |       |       |       |       | lecti |       |       |       |
   |       |       |       |       |       | on/​d |       |       |       |
   |       |       |       |       |       | ateTi |       |       |       |
   |       |       |       |       |       | me/​@ |       |       |       |
   |       |       |       |       |       | value |       |       |       |
   +-------+-------+-------+-------+-------+-------+-------+-------+-------+
   | C     | TM    | 1     | 1     |       | I     | TS    | 1..1  |       |
   | onten |       |       |       |       | mage​ |       |       |       |
   | tTime |       |       |       |       | Annot |       |       |       |
   |       |       |       |       |       | ation |       |       |       |
   |       |       |       |       |       | ​​Col |       |       |       |
   |       |       |       |       |       | lecti |       |       |       |
   |       |       |       |       |       | on/​d |       |       |       |
   |       |       |       |       |       | ateTi |       |       |       |
   |       |       |       |       |       | me/​@ |       |       |       |
   |       |       |       |       |       | value |       |       |       |
   +-------+-------+-------+-------+-------+-------+-------+-------+-------+
   | Auth  | SQ    | 1-n   | 3     |       |       |       |       | Don't |
   | or​Ob |       |       |       |       |       |       |       | send  |
   | serve |       |       |       |       |       |       |       | seq   |
   | r​Seq |       |       |       |       |       |       |       | uence |
   | uence |       |       |       |       |       |       |       | at    |
   |       |       |       |       |       |       |       |       | all   |
   |       |       |       |       |       |       |       |       | if    |
   |       |       |       |       |       |       |       |       | obs   |
   |       |       |       |       |       |       |       |       | erver |
   |       |       |       |       |       |       |       |       | is a  |
   |       |       |       |       |       |       |       |       | d     |
   |       |       |       |       |       |       |       |       | evice |
   |       |       |       |       |       |       |       |       | r     |
   |       |       |       |       |       |       |       |       | ather |
   |       |       |       |       |       |       |       |       | than  |
   |       |       |       |       |       |       |       |       | a     |
   |       |       |       |       |       |       |       |       | human |
   |       |       |       |       |       |       |       |       | since |
   |       |       |       |       |       |       |       |       | the   |
   |       |       |       |       |       |       |       |       | d     |
   |       |       |       |       |       |       |       |       | evice |
   |       |       |       |       |       |       |       |       | is    |
   |       |       |       |       |       |       |       |       | desc  |
   |       |       |       |       |       |       |       |       | ribed |
   |       |       |       |       |       |       |       |       | in    |
   |       |       |       |       |       |       |       |       | the   |
   |       |       |       |       |       |       |       |       | Ge    |
   |       |       |       |       |       |       |       |       | neral |
   |       |       |       |       |       |       |       |       | Equi  |
   |       |       |       |       |       |       |       |       | pment |
   |       |       |       |       |       |       |       |       | Mo    |
   |       |       |       |       |       |       |       |       | dule. |
   +-------+-------+-------+-------+-------+-------+-------+-------+-------+
   | Auth  | CS    | 1     | 1     | PSN   |       |       |       | DICOM |
   | or​Ob |       |       |       |       |       |       |       | a     |
   | serve |       |       |       |       |       |       |       | llows |
   | r​Seq |       |       |       |       |       |       |       | PSN   |
   | uence |       |       |       |       |       |       |       | or    |
   | >     |       |       |       |       |       |       |       | DEV.  |
   | Obs   |       |       |       |       |       |       |       |       |
   | erver |       |       |       |       |       |       |       |       |
   | ​Type |       |       |       |       |       |       |       |       |
   +-------+-------+-------+-------+-------+-------+-------+-------+-------+
   | Auth  | PN    | 1     | 1C    |       | Imag  | ST    | 1..1  | If    |
   | or​Ob |       |       |       |       | e​Ann |       |       | PSN.  |
   | serve |       |       |       |       | otati |       |       |       |
   | r​Seq |       |       |       |       | on​​C |       |       |       |
   | uence |       |       |       |       | ollec |       |       |       |
   | >     |       |       |       |       | tion/ |       |       |       |
   | P     |       |       |       |       | ​user |       |       |       |
   | erson |       |       |       |       | /​​na |       |       |       |
   | ​Name |       |       |       |       | me/​@ |       |       |       |
   |       |       |       |       |       | value |       |       |       |
   +-------+-------+-------+-------+-------+-------+-------+-------+-------+
   | Auth  | SQ    | 1     | 2C    | Empty |       |       |       | If    |
   | or​Ob |       |       |       |       |       |       |       | PSN.  |
   | serve |       |       |       |       |       |       |       |       |
   | r​Seq |       |       |       |       |       |       |       | Not   |
   | uence |       |       |       |       |       |       |       | in    |
   | >     |       |       |       |       |       |       |       | AIM.  |
   | Perso |       |       |       |       |       |       |       |       |
   | n​Ide |       |       |       |       |       |       |       |       |
   | ntifi |       |       |       |       |       |       |       |       |
   | catio |       |       |       |       |       |       |       |       |
   | n​Cod |       |       |       |       |       |       |       |       |
   | e​Seq |       |       |       |       |       |       |       |       |
   | uence |       |       |       |       |       |       |       |       |
   +-------+-------+-------+-------+-------+-------+-------+-------+-------+
   | Auth  | SQ    | 1     | 2     | Empty |       |       |       | Not   |
   | or​Ob |       |       |       |       |       |       |       | in    |
   | serve |       |       |       |       |       |       |       | AIM.  |
   | r​Seq |       |       |       |       |       |       |       |       |
   | uence |       |       |       |       |       |       |       |       |
   | >     |       |       |       |       |       |       |       |       |
   | I     |       |       |       |       |       |       |       |       |
   | nstit |       |       |       |       |       |       |       |       |
   | ution |       |       |       |       |       |       |       |       |
   | ​Name |       |       |       |       |       |       |       |       |
   +-------+-------+-------+-------+-------+-------+-------+-------+-------+
   | Auth  | SQ    | 1     | 2     | Empty |       |       |       | Not   |
   | or​Ob |       |       |       |       |       |       |       | in    |
   | serve |       |       |       |       |       |       |       | AIM.  |
   | r​Seq |       |       |       |       |       |       |       |       |
   | uence |       |       |       |       |       |       |       |       |
   | >     |       |       |       |       |       |       |       |       |
   | Insti |       |       |       |       |       |       |       |       |
   | tutio |       |       |       |       |       |       |       |       |
   | n​Cod |       |       |       |       |       |       |       |       |
   | e​Seq |       |       |       |       |       |       |       |       |
   | uence |       |       |       |       |       |       |       |       |
   +-------+-------+-------+-------+-------+-------+-------+-------+-------+
   | Iden  | SQ    | 1     | 1C    | UIDs  |       |       |       | Req   |
   | tical |       |       |       | of    |       |       |       | uired |
   | ​Docu |       |       |       | other |       |       |       | if    |
   | ments |       |       |       | iden  |       |       |       | this  |
   | ​​Seq |       |       |       | tical |       |       |       | doc   |
   | uence |       |       |       | conv  |       |       |       | ument |
   |       |       |       |       | erted |       |       |       | is    |
   |       |       |       |       | insta |       |       |       | s     |
   |       |       |       |       | nces. |       |       |       | tored |
   |       |       |       |       |       |       |       |       | with  |
   |       |       |       |       |       |       |       |       | diff  |
   |       |       |       |       |       |       |       |       | erent |
   |       |       |       |       |       |       |       |       | SOP   |
   |       |       |       |       |       |       |       |       | Ins   |
   |       |       |       |       |       |       |       |       | tance |
   |       |       |       |       |       |       |       |       | UIDs  |
   |       |       |       |       |       |       |       |       | in    |
   |       |       |       |       |       |       |       |       | one   |
   |       |       |       |       |       |       |       |       | or    |
   |       |       |       |       |       |       |       |       | more  |
   |       |       |       |       |       |       |       |       | other |
   |       |       |       |       |       |       |       |       | St    |
   |       |       |       |       |       |       |       |       | udies |
   +-------+-------+-------+-------+-------+-------+-------+-------+-------+
   | Curre | SQ    | 1     | 1     |       |       |       |       |       |
   | nt​Re |       |       |       |       |       |       |       |       |
   | quest |       |       |       |       |       |       |       |       |
   | ed​Pr |       |       |       |       |       |       |       |       |
   | ocedu |       |       |       |       |       |       |       |       |
   | re​Ev |       |       |       |       |       |       |       |       |
   | idenc |       |       |       |       |       |       |       |       |
   | e​Seq |       |       |       |       |       |       |       |       |
   | uence |       |       |       |       |       |       |       |       |
   +-------+-------+-------+-------+-------+-------+-------+-------+-------+
   | Cur   | UI    | 1     | 1     |       | Im    | II,   | 1..1, |       |
   | rent​ |       |       |       |       | age​A | II    | 0..1  |       |
   | Reque |       |       |       |       | nnota |       |       |       |
   | sted​ |       |       |       |       | tion​ |       |       |       |
   | Proce |       |       |       |       | ​Coll |       |       |       |
   | dure​ |       |       |       |       | ectio |       |       |       |
   | Evide |       |       |       |       | n/​im |       |       |       |
   | nce​S |       |       |       |       | age​A |       |       |       |
   | equen |       |       |       |       | nnota |       |       |       |
   | ce>​S |       |       |       |       | tions |       |       |       |
   | tudyI |       |       |       |       | /​ima |       |       |       |
   | nstan |       |       |       |       | ge​Re |       |       |       |
   | ceUID |       |       |       |       | feren |       |       |       |
   |       |       |       |       |       | ce​En |       |       |       |
   |       |       |       |       |       | tity​ |       |       |       |
   |       |       |       |       |       | ​Coll |       |       |       |
   |       |       |       |       |       | ectio |       |       |       |
   |       |       |       |       |       | n/​Im |       |       |       |
   |       |       |       |       |       | ageRe |       |       |       |
   |       |       |       |       |       | feren |       |       |       |
   |       |       |       |       |       | ceEnt |       |       |       |
   |       |       |       |       |       | ity/​ |       |       |       |
   |       |       |       |       |       | image |       |       |       |
   |       |       |       |       |       | Study |       |       |       |
   |       |       |       |       |       | /​ins |       |       |       |
   |       |       |       |       |       | tance |       |       |       |
   |       |       |       |       |       | Uid/​ |       |       |       |
   |       |       |       |       |       | @root |       |       |       |
   |       |       |       |       |       |       |       |       |       |
   |       |       |       |       |       | Ima   |       |       |       |
   |       |       |       |       |       | ge​An |       |       |       |
   |       |       |       |       |       | notat |       |       |       |
   |       |       |       |       |       | ion​​ |       |       |       |
   |       |       |       |       |       | Colle |       |       |       |
   |       |       |       |       |       | ction |       |       |       |
   |       |       |       |       |       | /​ima |       |       |       |
   |       |       |       |       |       | ge​An |       |       |       |
   |       |       |       |       |       | notat |       |       |       |
   |       |       |       |       |       | ions/ |       |       |       |
   |       |       |       |       |       | ​Imag |       |       |       |
   |       |       |       |       |       | e​Ann |       |       |       |
   |       |       |       |       |       | otati |       |       |       |
   |       |       |       |       |       | on/​​ |       |       |       |
   |       |       |       |       |       | segme |       |       |       |
   |       |       |       |       |       | ntati |       |       |       |
   |       |       |       |       |       | on​En |       |       |       |
   |       |       |       |       |       | tity​ |       |       |       |
   |       |       |       |       |       | Colle |       |       |       |
   |       |       |       |       |       | ction |       |       |       |
   |       |       |       |       |       | /​Seg |       |       |       |
   |       |       |       |       |       | menta |       |       |       |
   |       |       |       |       |       | tionE |       |       |       |
   |       |       |       |       |       | ntity |       |       |       |
   |       |       |       |       |       | /​stu |       |       |       |
   |       |       |       |       |       | dyIns |       |       |       |
   |       |       |       |       |       | tance |       |       |       |
   |       |       |       |       |       | Uid/​ |       |       |       |
   |       |       |       |       |       | @root |       |       |       |
   +-------+-------+-------+-------+-------+-------+-------+-------+-------+
   | C     | SQ    | 1     | 1     |       |       |       |       |       |
   | urren |       |       |       |       |       |       |       |       |
   | t​Req |       |       |       |       |       |       |       |       |
   | ueste |       |       |       |       |       |       |       |       |
   | d​Pro |       |       |       |       |       |       |       |       |
   | cedur |       |       |       |       |       |       |       |       |
   | e​Evi |       |       |       |       |       |       |       |       |
   | dence |       |       |       |       |       |       |       |       |
   | ​Sequ |       |       |       |       |       |       |       |       |
   | ence> |       |       |       |       |       |       |       |       |
   | ​Refe |       |       |       |       |       |       |       |       |
   | rence |       |       |       |       |       |       |       |       |
   | dSeri |       |       |       |       |       |       |       |       |
   | esSeq |       |       |       |       |       |       |       |       |
   | uence |       |       |       |       |       |       |       |       |
   +-------+-------+-------+-------+-------+-------+-------+-------+-------+
   | Curre | UI    | 1     | 1     |       | Image | II,   | 1..1, |       |
   | nt​Re |       |       |       |       | ​Anno | II    | 0..1  |       |
   | quest |       |       |       |       | tatio |       |       |       |
   | ed​Pr |       |       |       |       | n​​Co |       |       |       |
   | ocedu |       |       |       |       | llect |       |       |       |
   | re​Ev |       |       |       |       | ion/​ |       |       |       |
   | idenc |       |       |       |       | image |       |       |       |
   | e​Seq |       |       |       |       | ​Anno |       |       |       |
   | uence |       |       |       |       | tatio |       |       |       |
   | >​Ref |       |       |       |       | ns/​i |       |       |       |
   | erenc |       |       |       |       | mage​ |       |       |       |
   | edSer |       |       |       |       | Refer |       |       |       |
   | iesSe |       |       |       |       | ence​ |       |       |       |
   | quenc |       |       |       |       | Entit |       |       |       |
   | e>​Se |       |       |       |       | y​​Co |       |       |       |
   | riesI |       |       |       |       | llect |       |       |       |
   | nstan |       |       |       |       | ion/​ |       |       |       |
   | ceUID |       |       |       |       | Image |       |       |       |
   |       |       |       |       |       | Refer |       |       |       |
   |       |       |       |       |       | enceE |       |       |       |
   |       |       |       |       |       | ntity |       |       |       |
   |       |       |       |       |       | /​ima |       |       |       |
   |       |       |       |       |       | geStu |       |       |       |
   |       |       |       |       |       | dy/​i |       |       |       |
   |       |       |       |       |       | mageS |       |       |       |
   |       |       |       |       |       | eries |       |       |       |
   |       |       |       |       |       | /​ins |       |       |       |
   |       |       |       |       |       | tance |       |       |       |
   |       |       |       |       |       | Uid/​ |       |       |       |
   |       |       |       |       |       | @root |       |       |       |
   |       |       |       |       |       |       |       |       |       |
   |       |       |       |       |       | Imag  |       |       |       |
   |       |       |       |       |       | e​Ann |       |       |       |
   |       |       |       |       |       | otati |       |       |       |
   |       |       |       |       |       | on​​C |       |       |       |
   |       |       |       |       |       | ollec |       |       |       |
   |       |       |       |       |       | tion/ |       |       |       |
   |       |       |       |       |       | ​imag |       |       |       |
   |       |       |       |       |       | e​Ann |       |       |       |
   |       |       |       |       |       | otati |       |       |       |
   |       |       |       |       |       | ons/​ |       |       |       |
   |       |       |       |       |       | Image |       |       |       |
   |       |       |       |       |       | ​Anno |       |       |       |
   |       |       |       |       |       | tatio |       |       |       |
   |       |       |       |       |       | n/​​s |       |       |       |
   |       |       |       |       |       | egmen |       |       |       |
   |       |       |       |       |       | tatio |       |       |       |
   |       |       |       |       |       | n​Ent |       |       |       |
   |       |       |       |       |       | ity​C |       |       |       |
   |       |       |       |       |       | ollec |       |       |       |
   |       |       |       |       |       | tion/ |       |       |       |
   |       |       |       |       |       | ​Segm |       |       |       |
   |       |       |       |       |       | entat |       |       |       |
   |       |       |       |       |       | ionEn |       |       |       |
   |       |       |       |       |       | tity/ |       |       |       |
   |       |       |       |       |       | ​seri |       |       |       |
   |       |       |       |       |       | esIns |       |       |       |
   |       |       |       |       |       | tance |       |       |       |
   |       |       |       |       |       | Uid/​ |       |       |       |
   |       |       |       |       |       | @root |       |       |       |
   +-------+-------+-------+-------+-------+-------+-------+-------+-------+
   | Curr  | SQ    | 1     | 1     |       |       |       |       |       |
   | ent​R |       |       |       |       |       |       |       |       |
   | eques |       |       |       |       |       |       |       |       |
   | ted​P |       |       |       |       |       |       |       |       |
   | roced |       |       |       |       |       |       |       |       |
   | ure​E |       |       |       |       |       |       |       |       |
   | viden |       |       |       |       |       |       |       |       |
   | ce​Se |       |       |       |       |       |       |       |       |
   | quenc |       |       |       |       |       |       |       |       |
   | e>​Re |       |       |       |       |       |       |       |       |
   | feren |       |       |       |       |       |       |       |       |
   | cedSe |       |       |       |       |       |       |       |       |
   | riesS |       |       |       |       |       |       |       |       |
   | equen |       |       |       |       |       |       |       |       |
   | ce>​R |       |       |       |       |       |       |       |       |
   | efere |       |       |       |       |       |       |       |       |
   | ncedS |       |       |       |       |       |       |       |       |
   | OPSeq |       |       |       |       |       |       |       |       |
   | uence |       |       |       |       |       |       |       |       |
   +-------+-------+-------+-------+-------+-------+-------+-------+-------+
   | Cu    | UI    | 1     | 1     |       | Image | II,   | 1..1, | If    |
   | rrent |       |       |       |       | ​Anno | II    | 0..1  | the   |
   | ​Requ |       |       |       |       | tatio |       |       | s     |
   | ested |       |       |       |       | n​​Co |       |       | tudyI |
   | ​Proc |       |       |       |       | llect |       |       | nstan |
   | edure |       |       |       |       | ion/​ |       |       | ceUid |
   | ​Evid |       |       |       |       | image |       |       | or    |
   | ence​ |       |       |       |       | ​Anno |       |       | se    |
   | Seque |       |       |       |       | tatio |       |       | riesI |
   | nce>​ |       |       |       |       | ns/​i |       |       | nstan |
   | Refer |       |       |       |       | mage​ |       |       | ceUid |
   | enced |       |       |       |       | Refer |       |       | of a  |
   | Serie |       |       |       |       | ence​ |       |       | Seg   |
   | sSequ |       |       |       |       | Entit |       |       | menta |
   | ence> |       |       |       |       | y​​Co |       |       | tionE |
   | ​Refe |       |       |       |       | llect |       |       | ntity |
   | rence |       |       |       |       | ion/​ |       |       | are   |
   | dSOPS |       |       |       |       | Image |       |       | ab    |
   | equen |       |       |       |       | Refer |       |       | sent, |
   | ce>​R |       |       |       |       | enceE |       |       | this  |
   | efere |       |       |       |       | ntity |       |       | refe  |
   | ncedS |       |       |       |       | /​ima |       |       | rence |
   | OPCla |       |       |       |       | geStu |       |       | c     |
   | ssUID |       |       |       |       | dy/​i |       |       | annot |
   |       |       |       |       |       | mageS |       |       | be    |
   |       |       |       |       |       | eries |       |       | inc   |
   |       |       |       |       |       | /​ima |       |       | luded |
   |       |       |       |       |       | ge​Co |       |       | for   |
   |       |       |       |       |       | llect |       |       | that  |
   |       |       |       |       |       | ion/​ |       |       | inst  |
   |       |       |       |       |       | Image |       |       | ance. |
   |       |       |       |       |       | /​sop |       |       |       |
   |       |       |       |       |       | Class |       |       |       |
   |       |       |       |       |       | Uid/​ |       |       |       |
   |       |       |       |       |       | @root |       |       |       |
   |       |       |       |       |       |       |       |       |       |
   |       |       |       |       |       | Ima   |       |       |       |
   |       |       |       |       |       | ge​An |       |       |       |
   |       |       |       |       |       | notat |       |       |       |
   |       |       |       |       |       | ion​​ |       |       |       |
   |       |       |       |       |       | Colle |       |       |       |
   |       |       |       |       |       | ction |       |       |       |
   |       |       |       |       |       | /​ima |       |       |       |
   |       |       |       |       |       | ge​An |       |       |       |
   |       |       |       |       |       | notat |       |       |       |
   |       |       |       |       |       | ions/ |       |       |       |
   |       |       |       |       |       | ​Imag |       |       |       |
   |       |       |       |       |       | e​Ann |       |       |       |
   |       |       |       |       |       | otati |       |       |       |
   |       |       |       |       |       | on/​​ |       |       |       |
   |       |       |       |       |       | segme |       |       |       |
   |       |       |       |       |       | ntati |       |       |       |
   |       |       |       |       |       | on​En |       |       |       |
   |       |       |       |       |       | tity​ |       |       |       |
   |       |       |       |       |       | Colle |       |       |       |
   |       |       |       |       |       | ction |       |       |       |
   |       |       |       |       |       | /​Seg |       |       |       |
   |       |       |       |       |       | menta |       |       |       |
   |       |       |       |       |       | tionE |       |       |       |
   |       |       |       |       |       | ntity |       |       |       |
   |       |       |       |       |       | /​sop |       |       |       |
   |       |       |       |       |       | Class |       |       |       |
   |       |       |       |       |       | Uid/​ |       |       |       |
   |       |       |       |       |       | @root |       |       |       |
   +-------+-------+-------+-------+-------+-------+-------+-------+-------+
   | Curre | UI    | 1     | 1     |       | Ima   | II,   | 1..1, | If    |
   | nt​Re |       |       |       |       | ge​An | II    | 0..1  | the   |
   | quest |       |       |       |       | notat |       |       | s     |
   | ed​Pr |       |       |       |       | ion​​ |       |       | tudyI |
   | ocedu |       |       |       |       | Colle |       |       | nstan |
   | re​Ev |       |       |       |       | ction |       |       | ceUid |
   | idenc |       |       |       |       | /​ima |       |       | or    |
   | e​Seq |       |       |       |       | ge​An |       |       | se    |
   | uence |       |       |       |       | notat |       |       | riesI |
   | >​Ref |       |       |       |       | ions/ |       |       | nstan |
   | erenc |       |       |       |       | ​imag |       |       | ceUid |
   | edSer |       |       |       |       | e​Ref |       |       | of a  |
   | iesSe |       |       |       |       | erenc |       |       | Seg   |
   | quenc |       |       |       |       | e​Ent |       |       | menta |
   | e>​Re |       |       |       |       | ity​​ |       |       | tionE |
   | feren |       |       |       |       | Colle |       |       | ntity |
   | cedSO |       |       |       |       | ction |       |       | are   |
   | PSequ |       |       |       |       | /​Ima |       |       | ab    |
   | ence> |       |       |       |       | geRef |       |       | sent, |
   | ​Refe |       |       |       |       | erenc |       |       | this  |
   | rence |       |       |       |       | eEnti |       |       | refe  |
   | dSOPI |       |       |       |       | ty/​i |       |       | rence |
   | nstan |       |       |       |       | mageS |       |       | c     |
   | ceUID |       |       |       |       | tudy/ |       |       | annot |
   |       |       |       |       |       | ​imag |       |       | be    |
   |       |       |       |       |       | eSeri |       |       | inc   |
   |       |       |       |       |       | es/​i |       |       | luded |
   |       |       |       |       |       | mage​ |       |       | for   |
   |       |       |       |       |       | Colle |       |       | that  |
   |       |       |       |       |       | ction |       |       | inst  |
   |       |       |       |       |       | /​Ima |       |       | ance. |
   |       |       |       |       |       | ge/​s |       |       |       |
   |       |       |       |       |       | opIns |       |       |       |
   |       |       |       |       |       | tance |       |       |       |
   |       |       |       |       |       | Uid/​ |       |       |       |
   |       |       |       |       |       | @root |       |       |       |
   |       |       |       |       |       |       |       |       |       |
   |       |       |       |       |       | I     |       |       |       |
   |       |       |       |       |       | mage​ |       |       |       |
   |       |       |       |       |       | Annot |       |       |       |
   |       |       |       |       |       | ation |       |       |       |
   |       |       |       |       |       | ​​Col |       |       |       |
   |       |       |       |       |       | lecti |       |       |       |
   |       |       |       |       |       | on/​i |       |       |       |
   |       |       |       |       |       | mage​ |       |       |       |
   |       |       |       |       |       | Annot |       |       |       |
   |       |       |       |       |       | ation |       |       |       |
   |       |       |       |       |       | s/​Im |       |       |       |
   |       |       |       |       |       | age​A |       |       |       |
   |       |       |       |       |       | nnota |       |       |       |
   |       |       |       |       |       | tion/ |       |       |       |
   |       |       |       |       |       | ​​seg |       |       |       |
   |       |       |       |       |       | menta |       |       |       |
   |       |       |       |       |       | tion​ |       |       |       |
   |       |       |       |       |       | Entit |       |       |       |
   |       |       |       |       |       | y​Col |       |       |       |
   |       |       |       |       |       | lecti |       |       |       |
   |       |       |       |       |       | on/​S |       |       |       |
   |       |       |       |       |       | egmen |       |       |       |
   |       |       |       |       |       | tatio |       |       |       |
   |       |       |       |       |       | nEnti |       |       |       |
   |       |       |       |       |       | ty/​s |       |       |       |
   |       |       |       |       |       | opIns |       |       |       |
   |       |       |       |       |       | tance |       |       |       |
   |       |       |       |       |       | Uid/​ |       |       |       |
   |       |       |       |       |       | @root |       |       |       |
   +-------+-------+-------+-------+-------+-------+-------+-------+-------+
   | Per   | SQ    | 1     | 2     | Empty |       |       |       | Not   |
   | forme |       |       |       |       |       |       |       | in    |
   | d​Pro |       |       |       |       |       |       |       | AIM.  |
   | cedur |       |       |       |       |       |       |       |       |
   | e​Cod |       |       |       |       |       |       |       |       |
   | e​Seq |       |       |       |       |       |       |       |       |
   | uence |       |       |       |       |       |       |       |       |
   +-------+-------+-------+-------+-------+-------+-------+-------+-------+

.. _sect_A.6.1.1.10:

Mapping of DICOM SR Document Content Module
'''''''''''''''''''''''''''''''''''''''''''

All the Attributes in the SR Document Content Module are transformed by
processing the DICOM SR Content Tree, and accordingly are not described
in the same tabular manner as the "header" Attributes, since the mapping
depends on the DICOM SR template structure. The Attributes common to
each Content Item of the Content Tree are:

-  ValueType

-  ConceptNameCodeSequence

-  ObservationUID

-  ContentSequence

Each child Content Item with a "by-value" relationship with its parent
also contains:

-  RelationshipType

The additional required Attributes in each Content Item depend on the
ValueType:

-  TEXT - Text​Value

-  DATETIME - Date​Time

-  DATE - Date

-  TIME - Time

-  PNAME - Person​Name

-  UIDREF - UID

-  NUM - Measured​Value​Sequence, Measured​Value​Sequence>Numeric​Value,
   Measured​Value​Sequence>Measurement​Units​Code​Sequence

-  CODE - ConceptCodeSequence

-  COMPOSITE - Referenced​SOP​Sequence,
   Referenced​SOP​Sequence>Referenced​SOP​Class​UID,
   Referenced​SOP​Sequence>Referenced​SOP​Instance​UID

-  IMAGE - Referenced​SOP​Sequence,
   Referenced​SOP​Sequence>Referenced​SOP​Class​UID,
   Referenced​SOP​Sequence>Referenced​SO​PInstance​UID,
   Referenced​SOP​Sequence>Referenced​Frame​Number,
   Referenced​SOP​Sequence>Referenced​Segment​Number

-  SCOORD - Graphic​Data, Graphic​Type

-  SCOORD3D - Referenced​Frame​Of​Reference​UID, Graphic​Data,
   Graphic​Type

-  CONTAINER - Continuity​Of​Content, Content​Template​Sequence,
   Content​Template​Sequence>Mapping​Resource,
   Content​Template​Sequence>Template​Identifier

Observation​UID is required for the following Content Items in order to
propagate the aim:unique​Identifer information:

-  IMAGE - for (121191, DCM, "Referenced Segment") Content Item
   corresponding to aim:Segmentation​Entity

-  CONTAINER - for (126200, DCM, "Image Library Group") Content Item
   corresponding to aim:Image​Reference​Entity

-  CONTAINER - for (125007, DCM, "Measurement Group") Content Item
   corresponding to aim:Image​Annotation

-  NUM - for any Content Item corresponding to aim:Calculation​Entity

-  SCOORD - for any Content Item corresponding to aim:MarkupEntity

Observation​DateTime is required for the following Content Items in
order to propagate the aim:dateTime information:

-  CONTAINER - for (125007, DCM, "Measurement Group") Content Item
   corresponding to aim:Image​Annotation

.. _sect_A.6.1.1.11:

Mapping of DICOM SOP Common Module
''''''''''''''''''''''''''''''''''

.. table:: Mapping of DICOM SOP Common Module

   +-------+-------+-------+-------+-------+-------+-------+-------+-------+
   | DICOM | DICOM | DICOM | DICOM | Gene  | AIM   | AIM   | AIM   | Co    |
   | Attr  | VR    | VM    | Usage | rated | El    | Data  | Mu    | mment |
   | ibute |       |       | Type  | Value | ement | Type  | ltipl |       |
   |       |       |       |       |       | or    |       | icity |       |
   |       |       |       |       |       | Attr  |       |       |       |
   |       |       |       |       |       | ibute |       |       |       |
   +=======+=======+=======+=======+=======+=======+=======+=======+=======+
   | S     | UI    | 1     | 1     | "1.   |       |       |       | The   |
   | OPCla |       |       |       | 2.840 |       |       |       | fixed |
   | ssUID |       |       |       | .1000 |       |       |       | value |
   |       |       |       |       | 8.​5. |       |       |       | is    |
   |       |       |       |       | ​1.​4 |       |       |       | the   |
   |       |       |       |       | .​1.​ |       |       |       | SOP   |
   |       |       |       |       | 1.​88 |       |       |       | Class |
   |       |       |       |       | .​22" |       |       |       | UID   |
   |       |       |       |       |       |       |       |       | of    |
   |       |       |       |       |       |       |       |       | the   |
   |       |       |       |       |       |       |       |       | Enh   |
   |       |       |       |       |       |       |       |       | anced |
   |       |       |       |       |       |       |       |       | SR    |
   |       |       |       |       |       |       |       |       | St    |
   |       |       |       |       |       |       |       |       | orage |
   |       |       |       |       |       |       |       |       | SOP   |
   |       |       |       |       |       |       |       |       | C     |
   |       |       |       |       |       |       |       |       | lass, |
   |       |       |       |       |       |       |       |       | which |
   |       |       |       |       |       |       |       |       | is    |
   |       |       |       |       |       |       |       |       | suffi |
   |       |       |       |       |       |       |       |       | cient |
   |       |       |       |       |       |       |       |       | u     |
   |       |       |       |       |       |       |       |       | nless |
   |       |       |       |       |       |       |       |       | SCO   |
   |       |       |       |       |       |       |       |       | ORD3D |
   |       |       |       |       |       |       |       |       | are   |
   |       |       |       |       |       |       |       |       | used, |
   |       |       |       |       |       |       |       |       | in    |
   |       |       |       |       |       |       |       |       | which |
   |       |       |       |       |       |       |       |       | case  |
   |       |       |       |       |       |       |       |       | the   |
   |       |       |       |       |       |       |       |       | Com   |
   |       |       |       |       |       |       |       |       | prehe |
   |       |       |       |       |       |       |       |       | nsive |
   |       |       |       |       |       |       |       |       | 3D SR |
   |       |       |       |       |       |       |       |       | St    |
   |       |       |       |       |       |       |       |       | orage |
   |       |       |       |       |       |       |       |       | SOP   |
   |       |       |       |       |       |       |       |       | Class |
   |       |       |       |       |       |       |       |       | is    |
   |       |       |       |       |       |       |       |       | requ  |
   |       |       |       |       |       |       |       |       | ired, |
   |       |       |       |       |       |       |       |       | which |
   |       |       |       |       |       |       |       |       | has a |
   |       |       |       |       |       |       |       |       | UID   |
   |       |       |       |       |       |       |       |       | of    |
   |       |       |       |       |       |       |       |       | "1.2  |
   |       |       |       |       |       |       |       |       | .840. |
   |       |       |       |       |       |       |       |       | 10008 |
   |       |       |       |       |       |       |       |       | .​5.​ |
   |       |       |       |       |       |       |       |       | 1.​4. |
   |       |       |       |       |       |       |       |       | ​1.​1 |
   |       |       |       |       |       |       |       |       | .​88. |
   |       |       |       |       |       |       |       |       | ​34". |
   +-------+-------+-------+-------+-------+-------+-------+-------+-------+
   | SOPI  | UI    | 1     | 1     | Gene  | Im    | II    | 1..1  |       |
   | nstan |       |       |       | rated | age​A |       |       |       |
   | ceUID |       |       |       | if    | nnota |       |       |       |
   |       |       |       |       | more  | tion​ |       |       |       |
   |       |       |       |       | than  | ​Coll |       |       |       |
   |       |       |       |       | one   | ectio |       |       |       |
   |       |       |       |       | conv  | n>uni |       |       |       |
   |       |       |       |       | erted | queId |       |       |       |
   |       |       |       |       | ins   | entif |       |       |       |
   |       |       |       |       | tance | ier/​ |       |       |       |
   |       |       |       |       | in    | @root |       |       |       |
   |       |       |       |       | sep   |       |       |       |       |
   |       |       |       |       | arate |       |       |       |       |
   |       |       |       |       | stu   |       |       |       |       |
   |       |       |       |       | dies. |       |       |       |       |
   +-------+-------+-------+-------+-------+-------+-------+-------+-------+
   | Speci | CS    | 1     | 1     | "I    |       |       |       | The   |
   | ficCh |       |       |       | SO_IR |       |       |       | fixed |
   | aract |       |       |       | 192"  |       |       |       | gene  |
   | erSet |       |       |       |       |       |       |       | rated |
   |       |       |       |       |       |       |       |       | value |
   |       |       |       |       |       |       |       |       | c     |
   |       |       |       |       |       |       |       |       | orres |
   |       |       |       |       |       |       |       |       | ponds |
   |       |       |       |       |       |       |       |       | to    |
   |       |       |       |       |       |       |       |       | the   |
   |       |       |       |       |       |       |       |       | n     |
   |       |       |       |       |       |       |       |       | ormal |
   |       |       |       |       |       |       |       |       | UTF-8 |
   |       |       |       |       |       |       |       |       | spec  |
   |       |       |       |       |       |       |       |       | ified |
   |       |       |       |       |       |       |       |       | in    |
   |       |       |       |       |       |       |       |       | the   |
   |       |       |       |       |       |       |       |       | XM    |
   |       |       |       |       |       |       |       |       | LDecl |
   |       |       |       |       |       |       |       |       | of    |
   |       |       |       |       |       |       |       |       | the   |
   |       |       |       |       |       |       |       |       | XML   |
   |       |       |       |       |       |       |       |       | p     |
   |       |       |       |       |       |       |       |       | rolog |
   |       |       |       |       |       |       |       |       | `bibl |
   |       |       |       |       |       |       |       |       | ioent |
   |       |       |       |       |       |       |       |       | ry_ti |
   |       |       |       |       |       |       |       |       | tle < |
   |       |       |       |       |       |       |       |       | #bibl |
   |       |       |       |       |       |       |       |       | io_XM |
   |       |       |       |       |       |       |       |       | L>`__ |
   |       |       |       |       |       |       |       |       | in    |
   |       |       |       |       |       |       |       |       | the   |
   |       |       |       |       |       |       |       |       | AIM   |
   |       |       |       |       |       |       |       |       | inst  |
   |       |       |       |       |       |       |       |       | ance. |
   |       |       |       |       |       |       |       |       | Other |
   |       |       |       |       |       |       |       |       | v     |
   |       |       |       |       |       |       |       |       | alues |
   |       |       |       |       |       |       |       |       | may   |
   |       |       |       |       |       |       |       |       | be    |
   |       |       |       |       |       |       |       |       | used  |
   |       |       |       |       |       |       |       |       | if    |
   |       |       |       |       |       |       |       |       | they  |
   |       |       |       |       |       |       |       |       | are   |
   |       |       |       |       |       |       |       |       | suffi |
   |       |       |       |       |       |       |       |       | cient |
   |       |       |       |       |       |       |       |       | to    |
   |       |       |       |       |       |       |       |       | des   |
   |       |       |       |       |       |       |       |       | cribe |
   |       |       |       |       |       |       |       |       | all   |
   |       |       |       |       |       |       |       |       | the   |
   |       |       |       |       |       |       |       |       | en    |
   |       |       |       |       |       |       |       |       | coded |
   |       |       |       |       |       |       |       |       | chara |
   |       |       |       |       |       |       |       |       | cters |
   |       |       |       |       |       |       |       |       | in    |
   |       |       |       |       |       |       |       |       | the   |
   |       |       |       |       |       |       |       |       | t     |
   |       |       |       |       |       |       |       |       | ransf |
   |       |       |       |       |       |       |       |       | ormed |
   |       |       |       |       |       |       |       |       | inst  |
   |       |       |       |       |       |       |       |       | ance. |
   |       |       |       |       |       |       |       |       | E.g., |
   |       |       |       |       |       |       |       |       | it    |
   |       |       |       |       |       |       |       |       | may   |
   |       |       |       |       |       |       |       |       | be    |
   |       |       |       |       |       |       |       |       | om    |
   |       |       |       |       |       |       |       |       | itted |
   |       |       |       |       |       |       |       |       | ent   |
   |       |       |       |       |       |       |       |       | irely |
   |       |       |       |       |       |       |       |       | if    |
   |       |       |       |       |       |       |       |       | all   |
   |       |       |       |       |       |       |       |       | the   |
   |       |       |       |       |       |       |       |       | chara |
   |       |       |       |       |       |       |       |       | cters |
   |       |       |       |       |       |       |       |       | are   |
   |       |       |       |       |       |       |       |       | US-A  |
   |       |       |       |       |       |       |       |       | SCII. |
   +-------+-------+-------+-------+-------+-------+-------+-------+-------+

.. _sect_A.6.1.2:

Content Tree
^^^^^^^^^^^^

.. _sect_Mapping_TID_1500:

Mapping of Measurement Report
'''''''''''''''''''''''''''''

This section describes the mapping of .

.. table:: Mapping of Measurement Report

   +-------+-------+-------+-------+-------+-------+-------+-------+-------+
   | DICOM | DICOM | DICOM | DICOM | Gene  | AIM   | AIM   | AIM   | Co    |
   | SR    | VT    | VM    | Usage | rated | El    | Data  | Mu    | mment |
   | Path  |       |       | Type  | Value | ement | Type  | ltipl |       |
   |       |       |       |       |       | or    |       | icity |       |
   |       |       |       |       |       | Attr  |       |       |       |
   |       |       |       |       |       | ibute |       |       |       |
   +=======+=======+=======+=======+=======+=======+=======+=======+=======+
   | (12   | CONT  | 1     | M     |       |       |       |       | The   |
   | 6000, | AINER |       |       |       |       |       |       | fixed |
   | DCM,  |       |       |       |       |       |       |       | Co    |
   | "Im   |       |       |       |       |       |       |       | ncept |
   | aging |       |       |       |       |       |       |       | Name  |
   | M     |       |       |       |       |       |       |       | code  |
   | easur |       |       |       |       |       |       |       | is an |
   | ement |       |       |       |       |       |       |       | a     |
   | Rep   |       |       |       |       |       |       |       | pprop |
   | ort") |       |       |       |       |       |       |       | riate |
   |       |       |       |       |       |       |       |       | c     |
   |       |       |       |       |       |       |       |       | hoice |
   |       |       |       |       |       |       |       |       | sel   |
   |       |       |       |       |       |       |       |       | ected |
   |       |       |       |       |       |       |       |       | from  |
   |       |       |       |       |       |       |       |       | in    |
   |       |       |       |       |       |       |       |       | the   |
   |       |       |       |       |       |       |       |       | ab    |
   |       |       |       |       |       |       |       |       | sence |
   |       |       |       |       |       |       |       |       | of a  |
   |       |       |       |       |       |       |       |       | "doc  |
   |       |       |       |       |       |       |       |       | ument |
   |       |       |       |       |       |       |       |       | t     |
   |       |       |       |       |       |       |       |       | itle" |
   |       |       |       |       |       |       |       |       | co    |
   |       |       |       |       |       |       |       |       | ncept |
   |       |       |       |       |       |       |       |       | in    |
   |       |       |       |       |       |       |       |       | AIM.  |
   |       |       |       |       |       |       |       |       |       |
   |       |       |       |       |       |       |       |       | If    |
   |       |       |       |       |       |       |       |       | out   |
   |       |       |       |       |       |       |       |       | of    |
   |       |       |       |       |       |       |       |       | band  |
   |       |       |       |       |       |       |       |       | i     |
   |       |       |       |       |       |       |       |       | nform |
   |       |       |       |       |       |       |       |       | ation |
   |       |       |       |       |       |       |       |       | is    |
   |       |       |       |       |       |       |       |       | avail |
   |       |       |       |       |       |       |       |       | able, |
   |       |       |       |       |       |       |       |       | a     |
   |       |       |       |       |       |       |       |       | more  |
   |       |       |       |       |       |       |       |       | a     |
   |       |       |       |       |       |       |       |       | pprop |
   |       |       |       |       |       |       |       |       | riate |
   |       |       |       |       |       |       |       |       | code  |
   |       |       |       |       |       |       |       |       | can   |
   |       |       |       |       |       |       |       |       | be    |
   |       |       |       |       |       |       |       |       | used. |
   +-------+-------+-------+-------+-------+-------+-------+-------+-------+
   | (12   | IN    | 1     | M     | `Ma   |       |       |       |       |
   | 6000, | CLUDE |       |       | pping |       |       |       |       |
   | DCM,  |       |       |       | of    |       |       |       |       |
   | "Im   |       |       |       | Lan   |       |       |       |       |
   | aging |       |       |       | guage |       |       |       |       |
   | M     |       |       |       | of    |       |       |       |       |
   | easur |       |       |       | Co    |       |       |       |       |
   | ement |       |       |       | ntent |       |       |       |       |
   | Rep   |       |       |       | Item  |       |       |       |       |
   | ort") |       |       |       | and   |       |       |       |       |
   | >     |       |       |       | Desc  |       |       |       |       |
   |       |       |       |       | endan |       |       |       |       |
   |       |       |       |       | ts <# |       |       |       |       |
   |       |       |       |       | sect_ |       |       |       |       |
   |       |       |       |       | Mappi |       |       |       |       |
   |       |       |       |       | ng_TI |       |       |       |       |
   |       |       |       |       | D_120 |       |       |       |       |
   |       |       |       |       | 4>`__ |       |       |       |       |
   +-------+-------+-------+-------+-------+-------+-------+-------+-------+
   | (12   | IN    | 1     | M     | `Ma   |       |       |       |       |
   | 6000, | CLUDE |       |       | pping |       |       |       |       |
   | DCM,  |       |       |       | of    |       |       |       |       |
   | "Im   |       |       |       | O     |       |       |       |       |
   | aging |       |       |       | bserv |       |       |       |       |
   | M     |       |       |       | ation |       |       |       |       |
   | easur |       |       |       | Conte |       |       |       |       |
   | ement |       |       |       | xt <# |       |       |       |       |
   | Rep   |       |       |       | sect_ |       |       |       |       |
   | ort") |       |       |       | Mappi |       |       |       |       |
   | >     |       |       |       | ng_TI |       |       |       |       |
   |       |       |       |       | D_100 |       |       |       |       |
   |       |       |       |       | 1>`__ |       |       |       |       |
   +-------+-------+-------+-------+-------+-------+-------+-------+-------+
   | (12   | CODE  | 1-n   | M     | `(    |       |       |       | The   |
   | 6000, |       |       |       | 36367 |       |       |       | fixed |
   | DCM,  |       |       |       | 9005, |       |       |       | ge    |
   | "Im   |       |       |       | SCT,  |       |       |       | neric |
   | aging |       |       |       | "Im   |       |       |       | code  |
   | M     |       |       |       | aging |       |       |       | value |
   | easur |       |       |       | pro   |       |       |       | is    |
   | ement |       |       |       | cedur |       |       |       | sugg  |
   | Rep   |       |       |       | e") < |       |       |       | ested |
   | ort") |       |       |       | http: |       |       |       | in    |
   | >     |       |       |       | //sno |       |       |       | lieu  |
   | (12   |       |       |       | med.i |       |       |       | of    |
   | 1058, |       |       |       | nfo/i |       |       |       | AIM   |
   | DCM,  |       |       |       | d/363 |       |       |       | conta |
   | "Proc |       |       |       | 67900 |       |       |       | ining |
   | edure |       |       |       | 5>`__ |       |       |       | any   |
   | repor |       |       |       |       |       |       |       | i     |
   | ted") |       |       |       |       |       |       |       | nform |
   |       |       |       |       |       |       |       |       | ation |
   |       |       |       |       |       |       |       |       | about |
   |       |       |       |       |       |       |       |       | the   |
   |       |       |       |       |       |       |       |       | im    |
   |       |       |       |       |       |       |       |       | aging |
   |       |       |       |       |       |       |       |       | proce |
   |       |       |       |       |       |       |       |       | dure, |
   |       |       |       |       |       |       |       |       | so    |
   |       |       |       |       |       |       |       |       | more  |
   |       |       |       |       |       |       |       |       | spe   |
   |       |       |       |       |       |       |       |       | cific |
   |       |       |       |       |       |       |       |       | proc  |
   |       |       |       |       |       |       |       |       | edure |
   |       |       |       |       |       |       |       |       | codes |
   |       |       |       |       |       |       |       |       | such  |
   |       |       |       |       |       |       |       |       | as    |
   |       |       |       |       |       |       |       |       | those |
   |       |       |       |       |       |       |       |       | from  |
   |       |       |       |       |       |       |       |       | c     |
   |       |       |       |       |       |       |       |       | annot |
   |       |       |       |       |       |       |       |       | be    |
   |       |       |       |       |       |       |       |       | used. |
   |       |       |       |       |       |       |       |       |       |
   |       |       |       |       |       |       |       |       | If    |
   |       |       |       |       |       |       |       |       | out   |
   |       |       |       |       |       |       |       |       | of    |
   |       |       |       |       |       |       |       |       | band  |
   |       |       |       |       |       |       |       |       | i     |
   |       |       |       |       |       |       |       |       | nform |
   |       |       |       |       |       |       |       |       | ation |
   |       |       |       |       |       |       |       |       | is    |
   |       |       |       |       |       |       |       |       | avail |
   |       |       |       |       |       |       |       |       | able, |
   |       |       |       |       |       |       |       |       | a     |
   |       |       |       |       |       |       |       |       | more  |
   |       |       |       |       |       |       |       |       | a     |
   |       |       |       |       |       |       |       |       | pprop |
   |       |       |       |       |       |       |       |       | riate |
   |       |       |       |       |       |       |       |       | code  |
   |       |       |       |       |       |       |       |       | can   |
   |       |       |       |       |       |       |       |       | be    |
   |       |       |       |       |       |       |       |       | used. |
   +-------+-------+-------+-------+-------+-------+-------+-------+-------+
   | (12   | IN    | 1     | M     | `Ma   |       |       |       |       |
   | 6000, | CLUDE |       |       | pping |       |       |       |       |
   | DCM,  |       |       |       | of    |       |       |       |       |
   | "Im   |       |       |       | Image |       |       |       |       |
   | aging |       |       |       | Libra |       |       |       |       |
   | M     |       |       |       | ry <# |       |       |       |       |
   | easur |       |       |       | sect_ |       |       |       |       |
   | ement |       |       |       | Mappi |       |       |       |       |
   | Rep   |       |       |       | ng_TI |       |       |       |       |
   | ort") |       |       |       | D_160 |       |       |       |       |
   | >     |       |       |       | 0>`__ |       |       |       |       |
   +-------+-------+-------+-------+-------+-------+-------+-------+-------+
   | (12   | CONT  | 1     | C     |       |       |       |       | IFF   |
   | 6000, | AINER |       |       |       |       |       |       | me    |
   | DCM,  |       |       |       |       |       |       |       | asure |
   | "Im   |       |       |       |       |       |       |       | ments |
   | aging |       |       |       |       |       |       |       | are   |
   | M     |       |       |       |       |       |       |       | pr    |
   | easur |       |       |       |       |       |       |       | esent |
   | ement |       |       |       |       |       |       |       | in    |
   | Rep   |       |       |       |       |       |       |       | the   |
   | ort") |       |       |       |       |       |       |       | s     |
   | >     |       |       |       |       |       |       |       | ource |
   | (12   |       |       |       |       |       |       |       | AIM   |
   | 6010, |       |       |       |       |       |       |       | o     |
   | DCM,  |       |       |       |       |       |       |       | bject |
   | "Im   |       |       |       |       |       |       |       |       |
   | aging |       |       |       |       |       |       |       |       |
   | Meas  |       |       |       |       |       |       |       |       |
   | ureme |       |       |       |       |       |       |       |       |
   | nts") |       |       |       |       |       |       |       |       |
   +-------+-------+-------+-------+-------+-------+-------+-------+-------+
   | (12   | IN    | 1-n   | U     | `Ma   |       |       |       |       |
   | 6000, | CLUDE |       |       | pping |       |       |       |       |
   | DCM,  |       |       |       | of    |       |       |       |       |
   | "Im   |       |       |       | P     |       |       |       |       |
   | aging |       |       |       | lanar |       |       |       |       |
   | M     |       |       |       | ROI   |       |       |       |       |
   | easur |       |       |       | Measu |       |       |       |       |
   | ement |       |       |       | remen |       |       |       |       |
   | Rep   |       |       |       | ts <# |       |       |       |       |
   | ort") |       |       |       | sect_ |       |       |       |       |
   | >     |       |       |       | Mappi |       |       |       |       |
   | (12   |       |       |       | ng_TI |       |       |       |       |
   | 6010, |       |       |       | D_141 |       |       |       |       |
   | DCM,  |       |       |       | 0>`__ |       |       |       |       |
   | "Im   |       |       |       |       |       |       |       |       |
   | aging |       |       |       |       |       |       |       |       |
   | Meas  |       |       |       |       |       |       |       |       |
   | ureme |       |       |       |       |       |       |       |       |
   | nts") |       |       |       |       |       |       |       |       |
   | >     |       |       |       |       |       |       |       |       |
   +-------+-------+-------+-------+-------+-------+-------+-------+-------+
   | (12   | IN    | 1-n   | U     | `Ma   |       |       |       |       |
   | 6000, | CLUDE |       |       | pping |       |       |       |       |
   | DCM,  |       |       |       | of    |       |       |       |       |
   | "Im   |       |       |       | Volum |       |       |       |       |
   | aging |       |       |       | etric |       |       |       |       |
   | M     |       |       |       | ROI   |       |       |       |       |
   | easur |       |       |       | Measu |       |       |       |       |
   | ement |       |       |       | remen |       |       |       |       |
   | Rep   |       |       |       | ts <# |       |       |       |       |
   | ort") |       |       |       | sect_ |       |       |       |       |
   | >     |       |       |       | Mappi |       |       |       |       |
   | (12   |       |       |       | ng_TI |       |       |       |       |
   | 6010, |       |       |       | D_141 |       |       |       |       |
   | DCM,  |       |       |       | 1>`__ |       |       |       |       |
   | "Im   |       |       |       |       |       |       |       |       |
   | aging |       |       |       |       |       |       |       |       |
   | Meas  |       |       |       |       |       |       |       |       |
   | ureme |       |       |       |       |       |       |       |       |
   | nts") |       |       |       |       |       |       |       |       |
   | >     |       |       |       |       |       |       |       |       |
   +-------+-------+-------+-------+-------+-------+-------+-------+-------+
   | (12   | IN    | 1-n   | U     | `Ma   |       |       |       |       |
   | 6000, | CLUDE |       |       | pping |       |       |       |       |
   | DCM,  |       |       |       | of    |       |       |       |       |
   | "Im   |       |       |       | M     |       |       |       |       |
   | aging |       |       |       | easur |       |       |       |       |
   | M     |       |       |       | ement |       |       |       |       |
   | easur |       |       |       | Gro   |       |       |       |       |
   | ement |       |       |       | up <# |       |       |       |       |
   | Rep   |       |       |       | sect_ |       |       |       |       |
   | ort") |       |       |       | Mappi |       |       |       |       |
   | >     |       |       |       | ng_TI |       |       |       |       |
   | (12   |       |       |       | D_150 |       |       |       |       |
   | 6010, |       |       |       | 1>`__ |       |       |       |       |
   | DCM,  |       |       |       |       |       |       |       |       |
   | "Im   |       |       |       |       |       |       |       |       |
   | aging |       |       |       |       |       |       |       |       |
   | Meas  |       |       |       |       |       |       |       |       |
   | ureme |       |       |       |       |       |       |       |       |
   | nts") |       |       |       |       |       |       |       |       |
   | >     |       |       |       |       |       |       |       |       |
   +-------+-------+-------+-------+-------+-------+-------+-------+-------+
   | (12   | CONT  | 1     | C     |       |       |       |       | Not   |
   | 6000, | AINER |       |       |       |       |       |       | appli |
   | DCM,  |       |       |       |       |       |       |       | cable |
   | "Im   |       |       |       |       |       |       |       | to    |
   | aging |       |       |       |       |       |       |       | cu    |
   | M     |       |       |       |       |       |       |       | rrent |
   | easur |       |       |       |       |       |       |       | use   |
   | ement |       |       |       |       |       |       |       | cases |
   | Rep   |       |       |       |       |       |       |       |       |
   | ort") |       |       |       |       |       |       |       |       |
   | >     |       |       |       |       |       |       |       |       |
   | (12   |       |       |       |       |       |       |       |       |
   | 6011, |       |       |       |       |       |       |       |       |
   | DCM,  |       |       |       |       |       |       |       |       |
   | "De   |       |       |       |       |       |       |       |       |
   | rived |       |       |       |       |       |       |       |       |
   | Im    |       |       |       |       |       |       |       |       |
   | aging |       |       |       |       |       |       |       |       |
   | Meas  |       |       |       |       |       |       |       |       |
   | ureme |       |       |       |       |       |       |       |       |
   | nts") |       |       |       |       |       |       |       |       |
   +-------+-------+-------+-------+-------+-------+-------+-------+-------+
   | (12   | IN    | 1-n   | U     | `Ma   |       |       |       |       |
   | 6000, | CLUDE |       |       | pping |       |       |       |       |
   | DCM,  |       |       |       | of    |       |       |       |       |
   | "Im   |       |       |       | Me    |       |       |       |       |
   | aging |       |       |       | asure |       |       |       |       |
   | M     |       |       |       | ments |       |       |       |       |
   | easur |       |       |       | De    |       |       |       |       |
   | ement |       |       |       | rived |       |       |       |       |
   | Rep   |       |       |       | From  |       |       |       |       |
   | ort") |       |       |       | Mul   |       |       |       |       |
   | >     |       |       |       | tiple |       |       |       |       |
   | (12   |       |       |       | ROI   |       |       |       |       |
   | 6011, |       |       |       | Measu |       |       |       |       |
   | DCM,  |       |       |       | remen |       |       |       |       |
   | "De   |       |       |       | ts <# |       |       |       |       |
   | rived |       |       |       | sect_ |       |       |       |       |
   | Im    |       |       |       | Mappi |       |       |       |       |
   | aging |       |       |       | ng_TI |       |       |       |       |
   | Meas  |       |       |       | D_142 |       |       |       |       |
   | ureme |       |       |       | 0>`__ |       |       |       |       |
   | nts") |       |       |       |       |       |       |       |       |
   | >     |       |       |       |       |       |       |       |       |
   +-------+-------+-------+-------+-------+-------+-------+-------+-------+
   | (12   | CONT  | 1     | C     |       |       |       |       | IFF   |
   | 6000, | AINER |       |       |       |       |       |       | I     |
   | DCM,  |       |       |       |       |       |       |       | magin |
   | "Im   |       |       |       |       |       |       |       | g​Obs |
   | aging |       |       |       |       |       |       |       | ervat |
   | M     |       |       |       |       |       |       |       | ion​E |
   | easur |       |       |       |       |       |       |       | ntity |
   | ement |       |       |       |       |       |       |       | ele   |
   | Rep   |       |       |       |       |       |       |       | ments |
   | ort") |       |       |       |       |       |       |       | are   |
   | >     |       |       |       |       |       |       |       | pr    |
   | `     |       |       |       |       |       |       |       | esent |
   | (C003 |       |       |       |       |       |       |       | in    |
   | 4375, |       |       |       |       |       |       |       | the   |
   | UMLS, |       |       |       |       |       |       |       | s     |
   | "Q    |       |       |       |       |       |       |       | ource |
   | ualit |       |       |       |       |       |       |       | AIM   |
   | ative |       |       |       |       |       |       |       | o     |
   | Eval  |       |       |       |       |       |       |       | bject |
   | uatio |       |       |       |       |       |       |       |       |
   | ns")  |       |       |       |       |       |       |       |       |
   | <http |       |       |       |       |       |       |       |       |
   | s://u |       |       |       |       |       |       |       |       |
   | ts.nl |       |       |       |       |       |       |       |       |
   | m.nih |       |       |       |       |       |       |       |       |
   | .gov/ |       |       |       |       |       |       |       |       |
   | metat |       |       |       |       |       |       |       |       |
   | hesau |       |       |       |       |       |       |       |       |
   | rus.h |       |       |       |       |       |       |       |       |
   | tml?c |       |       |       |       |       |       |       |       |
   | ui=C0 |       |       |       |       |       |       |       |       |
   | 03437 |       |       |       |       |       |       |       |       |
   | 5>`__ |       |       |       |       |       |       |       |       |
   +-------+-------+-------+-------+-------+-------+-------+-------+-------+
   | (12   | CODE  | 1-n   | U     |       | NAME  | CD,   | 1,    | The   |
   | 6000, |       |       |       |       | =     | CD    | 0..1  | co    |
   | DCM,  |       |       |       |       | Ima   |       |       | ncept |
   | "Im   |       |       |       |       | ge​An |       |       | name  |
   | aging |       |       |       |       | notat |       |       | may   |
   | M     |       |       |       |       | ion​​ |       |       | be    |
   | easur |       |       |       |       | Colle |       |       | en    |
   | ement |       |       |       |       | ction |       |       | coded |
   | Rep   |       |       |       |       | /​ima |       |       | as a  |
   | ort") |       |       |       |       | ge​An |       |       | spe   |
   | >     |       |       |       |       | notat |       |       | cific |
   | `     |       |       |       |       | ions/ |       |       | que   |
   | (C003 |       |       |       |       | ​Imag |       |       | stion |
   | 4375, |       |       |       |       | e​Ann |       |       | ​Type |
   | UMLS, |       |       |       |       | otati |       |       | ​Code |
   | "Q    |       |       |       |       | on/​i |       |       | for   |
   | ualit |       |       |       |       | magin |       |       | the   |
   | ative |       |       |       |       | g​Obs |       |       | Imagi |
   | Eval  |       |       |       |       | ervat |       |       | ng​Ob |
   | uatio |       |       |       |       | ion​E |       |       | serva |
   | ns")  |       |       |       |       | ntity |       |       | tion​ |
   | <http |       |       |       |       | ​Coll |       |       | Chara |
   | s://u |       |       |       |       | ectio |       |       | cteri |
   | ts.nl |       |       |       |       | n/​Im |       |       | stic​ |
   | m.nih |       |       |       |       | aging |       |       | or    |
   | .gov/ |       |       |       |       | ​Obse |       |       | inhe  |
   | metat |       |       |       |       | rvati |       |       | rited |
   | hesau |       |       |       |       | on​En |       |       | from  |
   | rus.h |       |       |       |       | tity​ |       |       | the   |
   | tml?c |       |       |       |       | /​ima |       |       | type  |
   | ui=C0 |       |       |       |       | ging​ |       |       | ​Code |
   | 03437 |       |       |       |       | Obser |       |       | of    |
   | 5>`__ |       |       |       |       | vatio |       |       | the   |
   | >     |       |       |       |       | n​Cha |       |       | p     |
   | CODE  |       |       |       |       | racte |       |       | arent |
   |       |       |       |       |       | risti |       |       | Im    |
   |       |       |       |       |       | c​Col |       |       | aging |
   |       |       |       |       |       | lecti |       |       | ​Obse |
   |       |       |       |       |       | on​/​ |       |       | rvati |
   |       |       |       |       |       | Imagi |       |       | on​En |
   |       |       |       |       |       | ng​Ob |       |       | tity. |
   |       |       |       |       |       | serva |       |       |       |
   |       |       |       |       |       | tion​ |       |       |       |
   |       |       |       |       |       | Chara |       |       |       |
   |       |       |       |       |       | cteri |       |       |       |
   |       |       |       |       |       | stic​ |       |       |       |
   |       |       |       |       |       | ​/​qu |       |       |       |
   |       |       |       |       |       | estio |       |       |       |
   |       |       |       |       |       | nType |       |       |       |
   |       |       |       |       |       | ​Code |       |       |       |
   |       |       |       |       |       |       |       |       |       |
   |       |       |       |       |       | or    |       |       |       |
   |       |       |       |       |       | NAME  |       |       |       |
   |       |       |       |       |       | =     |       |       |       |
   |       |       |       |       |       | Ima   |       |       |       |
   |       |       |       |       |       | ge​An |       |       |       |
   |       |       |       |       |       | notat |       |       |       |
   |       |       |       |       |       | ion​​ |       |       |       |
   |       |       |       |       |       | Colle |       |       |       |
   |       |       |       |       |       | ction |       |       |       |
   |       |       |       |       |       | /​ima |       |       |       |
   |       |       |       |       |       | ge​An |       |       |       |
   |       |       |       |       |       | notat |       |       |       |
   |       |       |       |       |       | ions/ |       |       |       |
   |       |       |       |       |       | ​Imag |       |       |       |
   |       |       |       |       |       | e​Ann |       |       |       |
   |       |       |       |       |       | otati |       |       |       |
   |       |       |       |       |       | on/​i |       |       |       |
   |       |       |       |       |       | magin |       |       |       |
   |       |       |       |       |       | g​Obs |       |       |       |
   |       |       |       |       |       | ervat |       |       |       |
   |       |       |       |       |       | ion​E |       |       |       |
   |       |       |       |       |       | ntity |       |       |       |
   |       |       |       |       |       | ​Coll |       |       |       |
   |       |       |       |       |       | ectio |       |       |       |
   |       |       |       |       |       | n/​Im |       |       |       |
   |       |       |       |       |       | aging |       |       |       |
   |       |       |       |       |       | ​Obse |       |       |       |
   |       |       |       |       |       | rvati |       |       |       |
   |       |       |       |       |       | on​En |       |       |       |
   |       |       |       |       |       | tity​ |       |       |       |
   |       |       |       |       |       | /type |       |       |       |
   |       |       |       |       |       | ​Code |       |       |       |
   |       |       |       |       |       |       |       |       |       |
   |       |       |       |       |       | VALUE |       |       |       |
   |       |       |       |       |       | =     |       |       |       |
   |       |       |       |       |       | Image |       |       |       |
   |       |       |       |       |       | ​Anno |       |       |       |
   |       |       |       |       |       | tatio |       |       |       |
   |       |       |       |       |       | n​​Co |       |       |       |
   |       |       |       |       |       | llect |       |       |       |
   |       |       |       |       |       | ion/​ |       |       |       |
   |       |       |       |       |       | image |       |       |       |
   |       |       |       |       |       | ​Anno |       |       |       |
   |       |       |       |       |       | tatio |       |       |       |
   |       |       |       |       |       | ns/​I |       |       |       |
   |       |       |       |       |       | mage​ |       |       |       |
   |       |       |       |       |       | Annot |       |       |       |
   |       |       |       |       |       | ation |       |       |       |
   |       |       |       |       |       | /​ima |       |       |       |
   |       |       |       |       |       | ging​ |       |       |       |
   |       |       |       |       |       | Obser |       |       |       |
   |       |       |       |       |       | vatio |       |       |       |
   |       |       |       |       |       | n​Ent |       |       |       |
   |       |       |       |       |       | ity​C |       |       |       |
   |       |       |       |       |       | ollec |       |       |       |
   |       |       |       |       |       | tion/ |       |       |       |
   |       |       |       |       |       | Imagi |       |       |       |
   |       |       |       |       |       | ng​Ob |       |       |       |
   |       |       |       |       |       | serva |       |       |       |
   |       |       |       |       |       | tion​ |       |       |       |
   |       |       |       |       |       | Entit |       |       |       |
   |       |       |       |       |       | y/ima |       |       |       |
   |       |       |       |       |       | ging​ |       |       |       |
   |       |       |       |       |       | Obser |       |       |       |
   |       |       |       |       |       | vatio |       |       |       |
   |       |       |       |       |       | n​Cha |       |       |       |
   |       |       |       |       |       | racte |       |       |       |
   |       |       |       |       |       | risti |       |       |       |
   |       |       |       |       |       | c​Col |       |       |       |
   |       |       |       |       |       | lecti |       |       |       |
   |       |       |       |       |       | on​/​ |       |       |       |
   |       |       |       |       |       | Imagi |       |       |       |
   |       |       |       |       |       | ng​Ob |       |       |       |
   |       |       |       |       |       | serva |       |       |       |
   |       |       |       |       |       | tion​ |       |       |       |
   |       |       |       |       |       | Chara |       |       |       |
   |       |       |       |       |       | cteri |       |       |       |
   |       |       |       |       |       | stic​ |       |       |       |
   |       |       |       |       |       | /type |       |       |       |
   |       |       |       |       |       | ​Code |       |       |       |
   +-------+-------+-------+-------+-------+-------+-------+-------+-------+
   | (12   | TEXT  | 1-n   | U     |       |       |       |       | Not   |
   | 6000, |       |       |       |       |       |       |       | used  |
   | DCM,  |       |       |       |       |       |       |       | in    |
   | "Im   |       |       |       |       |       |       |       | AIM   |
   | aging |       |       |       |       |       |       |       |       |
   | M     |       |       |       |       |       |       |       |       |
   | easur |       |       |       |       |       |       |       |       |
   | ement |       |       |       |       |       |       |       |       |
   | Rep   |       |       |       |       |       |       |       |       |
   | ort") |       |       |       |       |       |       |       |       |
   | >     |       |       |       |       |       |       |       |       |
   | `     |       |       |       |       |       |       |       |       |
   | (C003 |       |       |       |       |       |       |       |       |
   | 4375, |       |       |       |       |       |       |       |       |
   | UMLS, |       |       |       |       |       |       |       |       |
   | "Q    |       |       |       |       |       |       |       |       |
   | ualit |       |       |       |       |       |       |       |       |
   | ative |       |       |       |       |       |       |       |       |
   | Eval  |       |       |       |       |       |       |       |       |
   | uatio |       |       |       |       |       |       |       |       |
   | ns")  |       |       |       |       |       |       |       |       |
   | <http |       |       |       |       |       |       |       |       |
   | s://u |       |       |       |       |       |       |       |       |
   | ts.nl |       |       |       |       |       |       |       |       |
   | m.nih |       |       |       |       |       |       |       |       |
   | .gov/ |       |       |       |       |       |       |       |       |
   | metat |       |       |       |       |       |       |       |       |
   | hesau |       |       |       |       |       |       |       |       |
   | rus.h |       |       |       |       |       |       |       |       |
   | tml?c |       |       |       |       |       |       |       |       |
   | ui=C0 |       |       |       |       |       |       |       |       |
   | 03437 |       |       |       |       |       |       |       |       |
   | 5>`__ |       |       |       |       |       |       |       |       |
   | >     |       |       |       |       |       |       |       |       |
   | TEXT  |       |       |       |       |       |       |       |       |
   +-------+-------+-------+-------+-------+-------+-------+-------+-------+

.. _sect_Mapping_TID_1501:

Mapping of Measurement Group
''''''''''''''''''''''''''''

This section describes the mapping of .

.. table:: Mapping of Measurement Group

   +-------+-------+-------+-------+-------+-------+-------+-------+-------+
   | DICOM | DICOM | DICOM | DICOM | Gene  | AIM   | AIM   | AIM   | Co    |
   | SR    | VT    | VM    | Usage | rated | El    | Data  | Mu    | mment |
   | Path  |       |       | Type  | Value | ement | Type  | ltipl |       |
   |       |       |       |       |       | or    |       | icity |       |
   |       |       |       |       |       | Attr  |       |       |       |
   |       |       |       |       |       | ibute |       |       |       |
   +=======+=======+=======+=======+=======+=======+=======+=======+=======+
   | (12   | CONT  | 1     | M     |       | Image |       |       | The   |
   | 6000, | AINER |       |       |       | ​Anno |       |       | value |
   | DCM,  |       |       |       |       | tatio |       |       | of    |
   | "Im   |       |       |       |       | n​​Co |       |       | ai    |
   | aging |       |       |       |       | llect |       |       | m:uni |
   | M     |       |       |       |       | ion/​ |       |       | que​I |
   | easur |       |       |       |       | image |       |       | denti |
   | ement |       |       |       |       | ​Anno |       |       | fier/ |
   | Rep   |       |       |       |       | tatio |       |       | @root |
   | ort") |       |       |       |       | ns/​I |       |       | is    |
   | >     |       |       |       |       | mage​ |       |       | m     |
   | (12   |       |       |       |       | Annot |       |       | apped |
   | 6010, |       |       |       |       | ation |       |       | to    |
   | DCM,  |       |       |       |       |       |       |       | the   |
   | "Im   |       |       |       |       |       |       |       | Obser |
   | aging |       |       |       |       |       |       |       | vatio |
   | Meas  |       |       |       |       |       |       |       | n​UID |
   | ureme |       |       |       |       |       |       |       | Attr  |
   | nts") |       |       |       |       |       |       |       | ibute |
   | >     |       |       |       |       |       |       |       | of    |
   | (12   |       |       |       |       |       |       |       | the   |
   | 5007, |       |       |       |       |       |       |       | CONTA |
   | DCM,  |       |       |       |       |       |       |       | INER. |
   | "M    |       |       |       |       |       |       |       |       |
   | easur |       |       |       |       |       |       |       | The   |
   | ement |       |       |       |       |       |       |       | value |
   | Gr    |       |       |       |       |       |       |       | of    |
   | oup") |       |       |       |       |       |       |       | aim:  |
   |       |       |       |       |       |       |       |       | date​ |
   |       |       |       |       |       |       |       |       | Time/ |
   |       |       |       |       |       |       |       |       | @root |
   |       |       |       |       |       |       |       |       | is    |
   |       |       |       |       |       |       |       |       | m     |
   |       |       |       |       |       |       |       |       | apped |
   |       |       |       |       |       |       |       |       | to    |
   |       |       |       |       |       |       |       |       | the   |
   |       |       |       |       |       |       |       |       | O     |
   |       |       |       |       |       |       |       |       | bserv |
   |       |       |       |       |       |       |       |       | ation |
   |       |       |       |       |       |       |       |       | ​Date |
   |       |       |       |       |       |       |       |       | ​Time |
   |       |       |       |       |       |       |       |       | ​Attr |
   |       |       |       |       |       |       |       |       | ibute |
   |       |       |       |       |       |       |       |       | of    |
   |       |       |       |       |       |       |       |       | the   |
   |       |       |       |       |       |       |       |       | CONTA |
   |       |       |       |       |       |       |       |       | INER. |
   +-------+-------+-------+-------+-------+-------+-------+-------+-------+
   | (12   | TEXT  | 1     | U     |       |       |       |       | Not   |
   | 6000, |       |       |       |       |       |       |       | pr    |
   | DCM,  |       |       |       |       |       |       |       | esent |
   | "Im   |       |       |       |       |       |       |       | in    |
   | aging |       |       |       |       |       |       |       | AIM.  |
   | M     |       |       |       |       |       |       |       |       |
   | easur |       |       |       |       |       |       |       | Ident |
   | ement |       |       |       |       |       |       |       | ifies |
   | Rep   |       |       |       |       |       |       |       | the   |
   | ort") |       |       |       |       |       |       |       | se    |
   | >     |       |       |       |       |       |       |       | ssion |
   | (12   |       |       |       |       |       |       |       | d     |
   | 6010, |       |       |       |       |       |       |       | uring |
   | DCM,  |       |       |       |       |       |       |       | which |
   | "Im   |       |       |       |       |       |       |       | the   |
   | aging |       |       |       |       |       |       |       | me    |
   | Meas  |       |       |       |       |       |       |       | asure |
   | ureme |       |       |       |       |       |       |       | ments |
   | nts") |       |       |       |       |       |       |       | were  |
   | >     |       |       |       |       |       |       |       | made. |
   | (12   |       |       |       |       |       |       |       | The   |
   | 5007, |       |       |       |       |       |       |       | NCI   |
   | DCM,  |       |       |       |       |       |       |       | Thes  |
   | "M    |       |       |       |       |       |       |       | aurus |
   | easur |       |       |       |       |       |       |       | defin |
   | ement |       |       |       |       |       |       |       | ition |
   | Gr    |       |       |       |       |       |       |       | is    |
   | oup") |       |       |       |       |       |       |       | "     |
   | >     |       |       |       |       |       |       |       | time, |
   | (C6   |       |       |       |       |       |       |       | pe    |
   | 7447, |       |       |       |       |       |       |       | riod, |
   | NCIt, |       |       |       |       |       |       |       | or    |
   | "Act  |       |       |       |       |       |       |       | term  |
   | ivity |       |       |       |       |       |       |       | de    |
   | Sess  |       |       |       |       |       |       |       | voted |
   | ion") |       |       |       |       |       |       |       | to    |
   |       |       |       |       |       |       |       |       | some  |
   |       |       |       |       |       |       |       |       | activ |
   |       |       |       |       |       |       |       |       | ity". |
   +-------+-------+-------+-------+-------+-------+-------+-------+-------+
   | (12   | TEXT  | 1     | M     |       | Imag  | ST    | 1     |       |
   | 6000, |       |       |       |       | e​Ann |       |       |       |
   | DCM,  |       |       |       |       | otati |       |       |       |
   | "Im   |       |       |       |       | on​​C |       |       |       |
   | aging |       |       |       |       | ollec |       |       |       |
   | M     |       |       |       |       | tion/ |       |       |       |
   | easur |       |       |       |       | ​imag |       |       |       |
   | ement |       |       |       |       | e​Ann |       |       |       |
   | Rep   |       |       |       |       | otati |       |       |       |
   | ort") |       |       |       |       | ons/​ |       |       |       |
   | >     |       |       |       |       | Image |       |       |       |
   | (12   |       |       |       |       | ​Anno |       |       |       |
   | 6010, |       |       |       |       | tatio |       |       |       |
   | DCM,  |       |       |       |       | n/​na |       |       |       |
   | "Im   |       |       |       |       | me/​@ |       |       |       |
   | aging |       |       |       |       | value |       |       |       |
   | Meas  |       |       |       |       |       |       |       |       |
   | ureme |       |       |       |       |       |       |       |       |
   | nts") |       |       |       |       |       |       |       |       |
   | >     |       |       |       |       |       |       |       |       |
   | (12   |       |       |       |       |       |       |       |       |
   | 5007, |       |       |       |       |       |       |       |       |
   | DCM,  |       |       |       |       |       |       |       |       |
   | "M    |       |       |       |       |       |       |       |       |
   | easur |       |       |       |       |       |       |       |       |
   | ement |       |       |       |       |       |       |       |       |
   | Gr    |       |       |       |       |       |       |       |       |
   | oup") |       |       |       |       |       |       |       |       |
   | >     |       |       |       |       |       |       |       |       |
   | (11   |       |       |       |       |       |       |       |       |
   | 2039, |       |       |       |       |       |       |       |       |
   | DCM,  |       |       |       |       |       |       |       |       |
   | "Tra  |       |       |       |       |       |       |       |       |
   | cking |       |       |       |       |       |       |       |       |
   | Id    |       |       |       |       |       |       |       |       |
   | entif |       |       |       |       |       |       |       |       |
   | ier") |       |       |       |       |       |       |       |       |
   +-------+-------+-------+-------+-------+-------+-------+-------+-------+
   | (12   | U     | 1     | M     |       | Imag  | II    | 1     | If    |
   | 6000, | IDREF |       |       |       | e​Ann |       |       | t     |
   | DCM,  |       |       |       |       | otati |       |       | racki |
   | "Im   |       |       |       |       | on​​C |       |       | ng​Un |
   | aging |       |       |       |       | ollec |       |       | ique​ |
   | M     |       |       |       |       | tion/ |       |       | Ident |
   | easur |       |       |       |       | ​imag |       |       | ifier |
   | ement |       |       |       |       | e​Ann |       |       | is    |
   | Rep   |       |       |       |       | otati |       |       | ab    |
   | ort") |       |       |       |       | ons/​ |       |       | sent, |
   | >     |       |       |       |       | Image |       |       | then  |
   | (12   |       |       |       |       | ​Anno |       |       | Imag  |
   | 6010, |       |       |       |       | tatio |       |       | e​Ann |
   | DCM,  |       |       |       |       | n/​tr |       |       | otati |
   | "Im   |       |       |       |       | ackin |       |       | on/​u |
   | aging |       |       |       |       | g​Uni |       |       | nique |
   | Meas  |       |       |       |       | queId |       |       | Ident |
   | ureme |       |       |       |       | entif |       |       | ifier |
   | nts") |       |       |       |       | ier/​ |       |       | may   |
   | >     |       |       |       |       | @root |       |       | be    |
   | (12   |       |       |       |       |       |       |       | used  |
   | 5007, |       |       |       |       |       |       |       | as a  |
   | DCM,  |       |       |       |       |       |       |       | proxy |
   | "M    |       |       |       |       |       |       |       | for   |
   | easur |       |       |       |       |       |       |       | Tra   |
   | ement |       |       |       |       |       |       |       | cking |
   | Gr    |       |       |       |       |       |       |       | U     |
   | oup") |       |       |       |       |       |       |       | nique |
   | >     |       |       |       |       |       |       |       | I     |
   | (11   |       |       |       |       |       |       |       | denti |
   | 2040, |       |       |       |       |       |       |       | fier, |
   | DCM,  |       |       |       |       |       |       |       | but   |
   | "Tra  |       |       |       |       |       |       |       | this  |
   | cking |       |       |       |       |       |       |       | does  |
   | U     |       |       |       |       |       |       |       | not   |
   | nique |       |       |       |       |       |       |       | allow |
   | Id    |       |       |       |       |       |       |       | lo    |
   | entif |       |       |       |       |       |       |       | ngitu |
   | ier") |       |       |       |       |       |       |       | dinal |
   |       |       |       |       |       |       |       |       | iden  |
   |       |       |       |       |       |       |       |       | tific |
   |       |       |       |       |       |       |       |       | ation |
   |       |       |       |       |       |       |       |       | of    |
   |       |       |       |       |       |       |       |       | the   |
   |       |       |       |       |       |       |       |       | same  |
   |       |       |       |       |       |       |       |       | l     |
   |       |       |       |       |       |       |       |       | esion |
   |       |       |       |       |       |       |       |       | be    |
   |       |       |       |       |       |       |       |       | cause |
   |       |       |       |       |       |       |       |       | Imag  |
   |       |       |       |       |       |       |       |       | e​Ann |
   |       |       |       |       |       |       |       |       | otati |
   |       |       |       |       |       |       |       |       | on/​u |
   |       |       |       |       |       |       |       |       | nique |
   |       |       |       |       |       |       |       |       | Ident |
   |       |       |       |       |       |       |       |       | ifier |
   |       |       |       |       |       |       |       |       | must  |
   |       |       |       |       |       |       |       |       | be    |
   |       |       |       |       |       |       |       |       | u     |
   |       |       |       |       |       |       |       |       | nique |
   |       |       |       |       |       |       |       |       | to    |
   |       |       |       |       |       |       |       |       | each  |
   |       |       |       |       |       |       |       |       | AIM   |
   |       |       |       |       |       |       |       |       | annot |
   |       |       |       |       |       |       |       |       | ation |
   |       |       |       |       |       |       |       |       | file, |
   |       |       |       |       |       |       |       |       | in    |
   |       |       |       |       |       |       |       |       | which |
   |       |       |       |       |       |       |       |       | case  |
   |       |       |       |       |       |       |       |       | only  |
   |       |       |       |       |       |       |       |       | Im    |
   |       |       |       |       |       |       |       |       | age​A |
   |       |       |       |       |       |       |       |       | nnota |
   |       |       |       |       |       |       |       |       | tion/ |
   |       |       |       |       |       |       |       |       | ​name |
   |       |       |       |       |       |       |       |       | can   |
   |       |       |       |       |       |       |       |       | be    |
   |       |       |       |       |       |       |       |       | used  |
   |       |       |       |       |       |       |       |       | to    |
   |       |       |       |       |       |       |       |       | reco  |
   |       |       |       |       |       |       |       |       | gnize |
   |       |       |       |       |       |       |       |       | co    |
   |       |       |       |       |       |       |       |       | mmona |
   |       |       |       |       |       |       |       |       | lity. |
   +-------+-------+-------+-------+-------+-------+-------+-------+-------+
   | (12   | CODE  | 1     | U     |       | Image | CD    | 1..n  | Only  |
   | 6000, |       |       |       |       | ​Anno |       |       | a     |
   | DCM,  |       |       |       |       | tatio |       |       | s     |
   | "Im   |       |       |       |       | n​​Co |       |       | ingle |
   | aging |       |       |       |       | llect |       |       | ai    |
   | M     |       |       |       |       | ion/​ |       |       | m:typ |
   | easur |       |       |       |       | image |       |       | eCode |
   | ement |       |       |       |       | ​Anno |       |       | value |
   | Rep   |       |       |       |       | tatio |       |       | can   |
   | ort") |       |       |       |       | ns/​I |       |       | be    |
   | >     |       |       |       |       | mage​ |       |       | ma    |
   | (12   |       |       |       |       | Annot |       |       | pped. |
   | 6010, |       |       |       |       | ation |       |       |       |
   | DCM,  |       |       |       |       | /​typ |       |       |       |
   | "Im   |       |       |       |       | eCode |       |       |       |
   | aging |       |       |       |       |       |       |       |       |
   | Meas  |       |       |       |       |       |       |       |       |
   | ureme |       |       |       |       |       |       |       |       |
   | nts") |       |       |       |       |       |       |       |       |
   | >     |       |       |       |       |       |       |       |       |
   | (12   |       |       |       |       |       |       |       |       |
   | 5007, |       |       |       |       |       |       |       |       |
   | DCM,  |       |       |       |       |       |       |       |       |
   | "M    |       |       |       |       |       |       |       |       |
   | easur |       |       |       |       |       |       |       |       |
   | ement |       |       |       |       |       |       |       |       |
   | Gr    |       |       |       |       |       |       |       |       |
   | oup") |       |       |       |       |       |       |       |       |
   | >     |       |       |       |       |       |       |       |       |
   | (12   |       |       |       |       |       |       |       |       |
   | 1071, |       |       |       |       |       |       |       |       |
   | DCM,  |       |       |       |       |       |       |       |       |
   | "Find |       |       |       |       |       |       |       |       |
   | ing") |       |       |       |       |       |       |       |       |
   +-------+-------+-------+-------+-------+-------+-------+-------+-------+
   | (12   | IN    | 1     | U     | `Ma   | Not   |       |       |       |
   | 6000, | CLUDE |       |       | pping | used  |       |       |       |
   | DCM,  |       |       |       | of    | in    |       |       |       |
   | "Im   |       |       |       | Time  | AIM.  |       |       |       |
   | aging |       |       |       | Point |       |       |       |       |
   | M     |       |       |       | Conte |       |       |       |       |
   | easur |       |       |       | xt <# |       |       |       |       |
   | ement |       |       |       | sect_ |       |       |       |       |
   | Rep   |       |       |       | Mappi |       |       |       |       |
   | ort") |       |       |       | ng_TI |       |       |       |       |
   | >     |       |       |       | D_150 |       |       |       |       |
   | (12   |       |       |       | 2>`__ |       |       |       |       |
   | 6010, |       |       |       |       |       |       |       |       |
   | DCM,  |       |       |       |       |       |       |       |       |
   | "Im   |       |       |       |       |       |       |       |       |
   | aging |       |       |       |       |       |       |       |       |
   | Meas  |       |       |       |       |       |       |       |       |
   | ureme |       |       |       |       |       |       |       |       |
   | nts") |       |       |       |       |       |       |       |       |
   | >     |       |       |       |       |       |       |       |       |
   | (12   |       |       |       |       |       |       |       |       |
   | 5007, |       |       |       |       |       |       |       |       |
   | DCM,  |       |       |       |       |       |       |       |       |
   | "M    |       |       |       |       |       |       |       |       |
   | easur |       |       |       |       |       |       |       |       |
   | ement |       |       |       |       |       |       |       |       |
   | Gr    |       |       |       |       |       |       |       |       |
   | oup") |       |       |       |       |       |       |       |       |
   | >     |       |       |       |       |       |       |       |       |
   +-------+-------+-------+-------+-------+-------+-------+-------+-------+
   | (12   | CODE  | 1     | U     |       |       |       |       | Not   |
   | 6000, |       |       |       |       |       |       |       | used  |
   | DCM,  |       |       |       |       |       |       |       | in    |
   | "Im   |       |       |       |       |       |       |       | AIM   |
   | aging |       |       |       |       |       |       |       | at    |
   | M     |       |       |       |       |       |       |       | this  |
   | easur |       |       |       |       |       |       |       | l     |
   | ement |       |       |       |       |       |       |       | evel. |
   | Rep   |       |       |       |       |       |       |       |       |
   | ort") |       |       |       |       |       |       |       |       |
   | >     |       |       |       |       |       |       |       |       |
   | (12   |       |       |       |       |       |       |       |       |
   | 6010, |       |       |       |       |       |       |       |       |
   | DCM,  |       |       |       |       |       |       |       |       |
   | "Im   |       |       |       |       |       |       |       |       |
   | aging |       |       |       |       |       |       |       |       |
   | Meas  |       |       |       |       |       |       |       |       |
   | ureme |       |       |       |       |       |       |       |       |
   | nts") |       |       |       |       |       |       |       |       |
   | >     |       |       |       |       |       |       |       |       |
   | (12   |       |       |       |       |       |       |       |       |
   | 5007, |       |       |       |       |       |       |       |       |
   | DCM,  |       |       |       |       |       |       |       |       |
   | "M    |       |       |       |       |       |       |       |       |
   | easur |       |       |       |       |       |       |       |       |
   | ement |       |       |       |       |       |       |       |       |
   | Gr    |       |       |       |       |       |       |       |       |
   | oup") |       |       |       |       |       |       |       |       |
   | >     |       |       |       |       |       |       |       |       |
   | `(    |       |       |       |       |       |       |       |       |
   | 37012 |       |       |       |       |       |       |       |       |
   | 9005, |       |       |       |       |       |       |       |       |
   | SCT,  |       |       |       |       |       |       |       |       |
   | "M    |       |       |       |       |       |       |       |       |
   | easur |       |       |       |       |       |       |       |       |
   | ement |       |       |       |       |       |       |       |       |
   | Metho |       |       |       |       |       |       |       |       |
   | d") < |       |       |       |       |       |       |       |       |
   | http: |       |       |       |       |       |       |       |       |
   | //sno |       |       |       |       |       |       |       |       |
   | med.i |       |       |       |       |       |       |       |       |
   | nfo/i |       |       |       |       |       |       |       |       |
   | d/370 |       |       |       |       |       |       |       |       |
   | 12900 |       |       |       |       |       |       |       |       |
   | 5>`__ |       |       |       |       |       |       |       |       |
   +-------+-------+-------+-------+-------+-------+-------+-------+-------+
   | (12   | CODE  | 1-n   | U     |       | Ima   | CD    | 1..n  | If a  |
   | 6000, |       |       |       |       | ge​An |       |       | p     |
   | DCM,  |       |       |       |       | notat |       |       | aired |
   | "Im   |       |       |       |       | ion​​ |       |       | stru  |
   | aging |       |       |       |       | Colle |       |       | cture |
   | M     |       |       |       |       | ction |       |       | in    |
   | easur |       |       |       |       | /​ima |       |       | AIM,  |
   | ement |       |       |       |       | ge​An |       |       | this  |
   | Rep   |       |       |       |       | notat |       |       | entry |
   | ort") |       |       |       |       | ions/ |       |       | will  |
   | >     |       |       |       |       | ​Imag |       |       | pre-  |
   | (12   |       |       |       |       | e​Ann |       |       | coord |
   | 6010, |       |       |       |       | otati |       |       | inate |
   | DCM,  |       |       |       |       | on/​i |       |       | the   |
   | "Im   |       |       |       |       | magin |       |       | later |
   | aging |       |       |       |       | gPhys |       |       | ality |
   | Meas  |       |       |       |       | ical​ |       |       | with  |
   | ureme |       |       |       |       | Entit |       |       | the   |
   | nts") |       |       |       |       | y​Col |       |       | site. |
   | >     |       |       |       |       | lecti |       |       |       |
   | (12   |       |       |       |       | on/​I |       |       |       |
   | 5007, |       |       |       |       | magin |       |       |       |
   | DCM,  |       |       |       |       | gPhys |       |       |       |
   | "M    |       |       |       |       | icalE |       |       |       |
   | easur |       |       |       |       | ntity |       |       |       |
   | ement |       |       |       |       | [labe |       |       |       |
   | Gr    |       |       |       |       | l/​@v |       |       |       |
   | oup") |       |       |       |       | alue= |       |       |       |
   | >     |       |       |       |       | 'Loca |       |       |       |
   | `(    |       |       |       |       | tion' |       |       |       |
   | 36369 |       |       |       |       | or    |       |       |       |
   | 8007, |       |       |       |       | label |       |       |       |
   | SCT,  |       |       |       |       | /​@va |       |       |       |
   | "Fi   |       |       |       |       | lue=' |       |       |       |
   | nding |       |       |       |       | Lobar |       |       |       |
   | Sit   |       |       |       |       | Loca  |       |       |       |
   | e") < |       |       |       |       | tion' |       |       |       |
   | http: |       |       |       |       | or    |       |       |       |
   | //sno |       |       |       |       | labe  |       |       |       |
   | med.i |       |       |       |       | l/​@v |       |       |       |
   | nfo/i |       |       |       |       | alue= |       |       |       |
   | d/363 |       |       |       |       | 'Segm |       |       |       |
   | 69800 |       |       |       |       | ental |       |       |       |
   | 7>`__ |       |       |       |       | Loca  |       |       |       |
   |       |       |       |       |       | tion' |       |       |       |
   |       |       |       |       |       | or    |       |       |       |
   |       |       |       |       |       | label |       |       |       |
   |       |       |       |       |       | /​@va |       |       |       |
   |       |       |       |       |       | lue=' |       |       |       |
   |       |       |       |       |       | Organ |       |       |       |
   |       |       |       |       |       | Type' |       |       |       |
   |       |       |       |       |       | ]/typ |       |       |       |
   |       |       |       |       |       | eCode |       |       |       |
   +-------+-------+-------+-------+-------+-------+-------+-------+-------+
   | (12   | CODE  | 1     | U     |       |       |       |       | Not   |
   | 6000, |       |       |       |       |       |       |       | used  |
   | DCM,  |       |       |       |       |       |       |       | in    |
   | "Im   |       |       |       |       |       |       |       | AIM.  |
   | aging |       |       |       |       |       |       |       |       |
   | M     |       |       |       |       |       |       |       |       |
   | easur |       |       |       |       |       |       |       |       |
   | ement |       |       |       |       |       |       |       |       |
   | Rep   |       |       |       |       |       |       |       |       |
   | ort") |       |       |       |       |       |       |       |       |
   | >     |       |       |       |       |       |       |       |       |
   | (12   |       |       |       |       |       |       |       |       |
   | 6010, |       |       |       |       |       |       |       |       |
   | DCM,  |       |       |       |       |       |       |       |       |
   | "Im   |       |       |       |       |       |       |       |       |
   | aging |       |       |       |       |       |       |       |       |
   | Meas  |       |       |       |       |       |       |       |       |
   | ureme |       |       |       |       |       |       |       |       |
   | nts") |       |       |       |       |       |       |       |       |
   | >     |       |       |       |       |       |       |       |       |
   | (12   |       |       |       |       |       |       |       |       |
   | 5007, |       |       |       |       |       |       |       |       |
   | DCM,  |       |       |       |       |       |       |       |       |
   | "M    |       |       |       |       |       |       |       |       |
   | easur |       |       |       |       |       |       |       |       |
   | ement |       |       |       |       |       |       |       |       |
   | Gr    |       |       |       |       |       |       |       |       |
   | oup") |       |       |       |       |       |       |       |       |
   | >     |       |       |       |       |       |       |       |       |
   | `(    |       |       |       |       |       |       |       |       |
   | 36369 |       |       |       |       |       |       |       |       |
   | 8007, |       |       |       |       |       |       |       |       |
   | SCT,  |       |       |       |       |       |       |       |       |
   | "Fi   |       |       |       |       |       |       |       |       |
   | nding |       |       |       |       |       |       |       |       |
   | Sit   |       |       |       |       |       |       |       |       |
   | e") < |       |       |       |       |       |       |       |       |
   | http: |       |       |       |       |       |       |       |       |
   | //sno |       |       |       |       |       |       |       |       |
   | med.i |       |       |       |       |       |       |       |       |
   | nfo/i |       |       |       |       |       |       |       |       |
   | d/363 |       |       |       |       |       |       |       |       |
   | 69800 |       |       |       |       |       |       |       |       |
   | 7>`__ |       |       |       |       |       |       |       |       |
   | >     |       |       |       |       |       |       |       |       |
   | `(    |       |       |       |       |       |       |       |       |
   | 27274 |       |       |       |       |       |       |       |       |
   | 1003, |       |       |       |       |       |       |       |       |
   | SCT,  |       |       |       |       |       |       |       |       |
   | "Late |       |       |       |       |       |       |       |       |
   | ralit |       |       |       |       |       |       |       |       |
   | y") < |       |       |       |       |       |       |       |       |
   | http: |       |       |       |       |       |       |       |       |
   | //sno |       |       |       |       |       |       |       |       |
   | med.i |       |       |       |       |       |       |       |       |
   | nfo/i |       |       |       |       |       |       |       |       |
   | d/272 |       |       |       |       |       |       |       |       |
   | 74100 |       |       |       |       |       |       |       |       |
   | 3>`__ |       |       |       |       |       |       |       |       |
   +-------+-------+-------+-------+-------+-------+-------+-------+-------+
   | (12   | CODE  | 1     | U     |       |       |       |       | Not   |
   | 6000, |       |       |       |       |       |       |       | used  |
   | DCM,  |       |       |       |       |       |       |       | since |
   | "Im   |       |       |       |       |       |       |       | AIM   |
   | aging |       |       |       |       |       |       |       | does  |
   | M     |       |       |       |       |       |       |       | not   |
   | easur |       |       |       |       |       |       |       | have  |
   | ement |       |       |       |       |       |       |       | a     |
   | Rep   |       |       |       |       |       |       |       | mech  |
   | ort") |       |       |       |       |       |       |       | anism |
   | >     |       |       |       |       |       |       |       | for   |
   | (12   |       |       |       |       |       |       |       | po    |
   | 6010, |       |       |       |       |       |       |       | st-co |
   | DCM,  |       |       |       |       |       |       |       | ordin |
   | "Im   |       |       |       |       |       |       |       | ating |
   | aging |       |       |       |       |       |       |       | the   |
   | Meas  |       |       |       |       |       |       |       | loca  |
   | ureme |       |       |       |       |       |       |       | tion. |
   | nts") |       |       |       |       |       |       |       |       |
   | >     |       |       |       |       |       |       |       |       |
   | (12   |       |       |       |       |       |       |       |       |
   | 5007, |       |       |       |       |       |       |       |       |
   | DCM,  |       |       |       |       |       |       |       |       |
   | "M    |       |       |       |       |       |       |       |       |
   | easur |       |       |       |       |       |       |       |       |
   | ement |       |       |       |       |       |       |       |       |
   | Gr    |       |       |       |       |       |       |       |       |
   | oup") |       |       |       |       |       |       |       |       |
   | >     |       |       |       |       |       |       |       |       |
   | `(    |       |       |       |       |       |       |       |       |
   | 36369 |       |       |       |       |       |       |       |       |
   | 8007, |       |       |       |       |       |       |       |       |
   | SCT,  |       |       |       |       |       |       |       |       |
   | "Fi   |       |       |       |       |       |       |       |       |
   | nding |       |       |       |       |       |       |       |       |
   | Sit   |       |       |       |       |       |       |       |       |
   | e") < |       |       |       |       |       |       |       |       |
   | http: |       |       |       |       |       |       |       |       |
   | //sno |       |       |       |       |       |       |       |       |
   | med.i |       |       |       |       |       |       |       |       |
   | nfo/i |       |       |       |       |       |       |       |       |
   | d/363 |       |       |       |       |       |       |       |       |
   | 69800 |       |       |       |       |       |       |       |       |
   | 7>`__ |       |       |       |       |       |       |       |       |
   | >     |       |       |       |       |       |       |       |       |
   | `(    |       |       |       |       |       |       |       |       |
   | 10623 |       |       |       |       |       |       |       |       |
   | 3006, |       |       |       |       |       |       |       |       |
   | SCT,  |       |       |       |       |       |       |       |       |
   | "Top  |       |       |       |       |       |       |       |       |
   | ograp |       |       |       |       |       |       |       |       |
   | hical |       |       |       |       |       |       |       |       |
   | mo    |       |       |       |       |       |       |       |       |
   | difie |       |       |       |       |       |       |       |       |
   | r") < |       |       |       |       |       |       |       |       |
   | http: |       |       |       |       |       |       |       |       |
   | //sno |       |       |       |       |       |       |       |       |
   | med.i |       |       |       |       |       |       |       |       |
   | nfo/i |       |       |       |       |       |       |       |       |
   | d/106 |       |       |       |       |       |       |       |       |
   | 23300 |       |       |       |       |       |       |       |       |
   | 6>`__ |       |       |       |       |       |       |       |       |
   +-------+-------+-------+-------+-------+-------+-------+-------+-------+
   | (12   | COMP  | 1     | U     |       |       |       |       | Not   |
   | 6000, | OSITE |       |       |       |       |       |       | used  |
   | DCM,  |       |       |       |       |       |       |       | in    |
   | "Im   |       |       |       |       |       |       |       | AIM.  |
   | aging |       |       |       |       |       |       |       |       |
   | M     |       |       |       |       |       |       |       |       |
   | easur |       |       |       |       |       |       |       |       |
   | ement |       |       |       |       |       |       |       |       |
   | Rep   |       |       |       |       |       |       |       |       |
   | ort") |       |       |       |       |       |       |       |       |
   | >     |       |       |       |       |       |       |       |       |
   | (12   |       |       |       |       |       |       |       |       |
   | 6010, |       |       |       |       |       |       |       |       |
   | DCM,  |       |       |       |       |       |       |       |       |
   | "Im   |       |       |       |       |       |       |       |       |
   | aging |       |       |       |       |       |       |       |       |
   | Meas  |       |       |       |       |       |       |       |       |
   | ureme |       |       |       |       |       |       |       |       |
   | nts") |       |       |       |       |       |       |       |       |
   | >     |       |       |       |       |       |       |       |       |
   | (12   |       |       |       |       |       |       |       |       |
   | 5007, |       |       |       |       |       |       |       |       |
   | DCM,  |       |       |       |       |       |       |       |       |
   | "M    |       |       |       |       |       |       |       |       |
   | easur |       |       |       |       |       |       |       |       |
   | ement |       |       |       |       |       |       |       |       |
   | Gr    |       |       |       |       |       |       |       |       |
   | oup") |       |       |       |       |       |       |       |       |
   | >     |       |       |       |       |       |       |       |       |
   | (12   |       |       |       |       |       |       |       |       |
   | 6100, |       |       |       |       |       |       |       |       |
   | DCM,  |       |       |       |       |       |       |       |       |
   | "Real |       |       |       |       |       |       |       |       |
   | World |       |       |       |       |       |       |       |       |
   | Value |       |       |       |       |       |       |       |       |
   | Map   |       |       |       |       |       |       |       |       |
   | used  |       |       |       |       |       |       |       |       |
   | for   |       |       |       |       |       |       |       |       |
   | mea   |       |       |       |       |       |       |       |       |
   | surem |       |       |       |       |       |       |       |       |
   | ent") |       |       |       |       |       |       |       |       |
   +-------+-------+-------+-------+-------+-------+-------+-------+-------+
   | (12   | IN    | 1-n   | M     | `Ma   |       |       |       |       |
   | 6000, | CLUDE |       |       | pping |       |       |       |       |
   | DCM,  |       |       |       | of    |       |       |       |       |
   | "Im   |       |       |       | Mea   |       |       |       |       |
   | aging |       |       |       | surem |       |       |       |       |
   | M     |       |       |       | ent < |       |       |       |       |
   | easur |       |       |       | #sect |       |       |       |       |
   | ement |       |       |       | _Mapp |       |       |       |       |
   | Rep   |       |       |       | ing_T |       |       |       |       |
   | ort") |       |       |       | ID_30 |       |       |       |       |
   | >     |       |       |       | 0>`__ |       |       |       |       |
   | (12   |       |       |       |       |       |       |       |       |
   | 6010, |       |       |       |       |       |       |       |       |
   | DCM,  |       |       |       |       |       |       |       |       |
   | "Im   |       |       |       |       |       |       |       |       |
   | aging |       |       |       |       |       |       |       |       |
   | Meas  |       |       |       |       |       |       |       |       |
   | ureme |       |       |       |       |       |       |       |       |
   | nts") |       |       |       |       |       |       |       |       |
   | >     |       |       |       |       |       |       |       |       |
   | (12   |       |       |       |       |       |       |       |       |
   | 5007, |       |       |       |       |       |       |       |       |
   | DCM,  |       |       |       |       |       |       |       |       |
   | "M    |       |       |       |       |       |       |       |       |
   | easur |       |       |       |       |       |       |       |       |
   | ement |       |       |       |       |       |       |       |       |
   | Gr    |       |       |       |       |       |       |       |       |
   | oup") |       |       |       |       |       |       |       |       |
   | >     |       |       |       |       |       |       |       |       |
   +-------+-------+-------+-------+-------+-------+-------+-------+-------+
   | (12   | CODE  | 1-n   | U     |       |       |       |       | Not   |
   | 6000, |       |       |       |       |       |       |       | used  |
   | DCM,  |       |       |       |       |       |       |       | in    |
   | "Im   |       |       |       |       |       |       |       | AIM.  |
   | aging |       |       |       |       |       |       |       |       |
   | M     |       |       |       |       |       |       |       |       |
   | easur |       |       |       |       |       |       |       |       |
   | ement |       |       |       |       |       |       |       |       |
   | Rep   |       |       |       |       |       |       |       |       |
   | ort") |       |       |       |       |       |       |       |       |
   | >     |       |       |       |       |       |       |       |       |
   | (12   |       |       |       |       |       |       |       |       |
   | 6010, |       |       |       |       |       |       |       |       |
   | DCM,  |       |       |       |       |       |       |       |       |
   | "Im   |       |       |       |       |       |       |       |       |
   | aging |       |       |       |       |       |       |       |       |
   | Meas  |       |       |       |       |       |       |       |       |
   | ureme |       |       |       |       |       |       |       |       |
   | nts") |       |       |       |       |       |       |       |       |
   | >     |       |       |       |       |       |       |       |       |
   | (12   |       |       |       |       |       |       |       |       |
   | 5007, |       |       |       |       |       |       |       |       |
   | DCM,  |       |       |       |       |       |       |       |       |
   | "M    |       |       |       |       |       |       |       |       |
   | easur |       |       |       |       |       |       |       |       |
   | ement |       |       |       |       |       |       |       |       |
   | Gr    |       |       |       |       |       |       |       |       |
   | oup") |       |       |       |       |       |       |       |       |
   | >     |       |       |       |       |       |       |       |       |
   | $Qu   |       |       |       |       |       |       |       |       |
   | alita |       |       |       |       |       |       |       |       |
   | tiveE |       |       |       |       |       |       |       |       |
   | valua |       |       |       |       |       |       |       |       |
   | tions |       |       |       |       |       |       |       |       |
   +-------+-------+-------+-------+-------+-------+-------+-------+-------+
   | (12   | TEXT  | 1-n   | U     |       | Im    |       |       | The   |
   | 6000, |       |       |       |       | age​A |       |       | para  |
   | DCM,  |       |       |       |       | nnota |       |       | meter |
   | "Im   |       |       |       |       | tion​ |       |       | $Qua  |
   | aging |       |       |       |       | ​Coll |       |       | litat |
   | M     |       |       |       |       | ectio |       |       | ive​E |
   | easur |       |       |       |       | n/​im |       |       | valua |
   | ement |       |       |       |       | age​A |       |       | tions |
   | Rep   |       |       |       |       | nnota |       |       | is    |
   | ort") |       |       |       |       | tions |       |       | not   |
   | >     |       |       |       |       | /​Ima |       |       | used  |
   | (12   |       |       |       |       | ge​An |       |       | in    |
   | 6010, |       |       |       |       | notat |       |       | AIM,  |
   | DCM,  |       |       |       |       | ion/​ |       |       | but   |
   | "Im   |       |       |       |       | comme |       |       | this  |
   | aging |       |       |       |       | nt/​@ |       |       | TEXT  |
   | Meas  |       |       |       |       | value |       |       | co    |
   | ureme |       |       |       |       |       |       |       | ntent |
   | nts") |       |       |       |       |       |       |       | item  |
   | >     |       |       |       |       |       |       |       | is    |
   | (12   |       |       |       |       |       |       |       | used  |
   | 5007, |       |       |       |       |       |       |       | to    |
   | DCM,  |       |       |       |       |       |       |       | map   |
   | "M    |       |       |       |       |       |       |       | the   |
   | easur |       |       |       |       |       |       |       | AIM   |
   | ement |       |       |       |       |       |       |       | co    |
   | Gr    |       |       |       |       |       |       |       | mment |
   | oup") |       |       |       |       |       |       |       | as if |
   | >     |       |       |       |       |       |       |       | it    |
   | (12   |       |       |       |       |       |       |       | were  |
   | 1106, |       |       |       |       |       |       |       | a     |
   | DCM,  |       |       |       |       |       |       |       | Q     |
   | "Comm |       |       |       |       |       |       |       | ualit |
   | ent") |       |       |       |       |       |       |       | ative |
   |       |       |       |       |       |       |       |       | E     |
   |       |       |       |       |       |       |       |       | valua |
   |       |       |       |       |       |       |       |       | tion. |
   +-------+-------+-------+-------+-------+-------+-------+-------+-------+

.. _sect_Mapping_TID_1502:

Mapping of Time Point Context
'''''''''''''''''''''''''''''

This section describes the mapping of .

.. table:: Mapping of Time Point Context

   +-------+-------+-------+-------+-------+-------+-------+-------+-------+
   | DICOM | DICOM | DICOM | DICOM | Gene  | AIM   | AIM   | AIM   | Co    |
   | SR    | VT    | VM    | Usage | rated | El    | Data  | Mu    | mment |
   | Path  |       |       | Type  | Value | ement | Type  | ltipl |       |
   |       |       |       |       |       | or    |       | icity |       |
   |       |       |       |       |       | Attr  |       |       |       |
   |       |       |       |       |       | ibute |       |       |       |
   +=======+=======+=======+=======+=======+=======+=======+=======+=======+
   | (12   | TEXT  | 1     | U     |       |       |       |       | Not   |
   | 6000, |       |       |       |       |       |       |       | used  |
   | DCM,  |       |       |       |       |       |       |       | in    |
   | "Im   |       |       |       |       |       |       |       | AIM.  |
   | aging |       |       |       |       |       |       |       |       |
   | M     |       |       |       |       |       |       |       |       |
   | easur |       |       |       |       |       |       |       |       |
   | ement |       |       |       |       |       |       |       |       |
   | Rep   |       |       |       |       |       |       |       |       |
   | ort") |       |       |       |       |       |       |       |       |
   | >     |       |       |       |       |       |       |       |       |
   | (12   |       |       |       |       |       |       |       |       |
   | 6010, |       |       |       |       |       |       |       |       |
   | DCM,  |       |       |       |       |       |       |       |       |
   | "Im   |       |       |       |       |       |       |       |       |
   | aging |       |       |       |       |       |       |       |       |
   | Meas  |       |       |       |       |       |       |       |       |
   | ureme |       |       |       |       |       |       |       |       |
   | nts") |       |       |       |       |       |       |       |       |
   | >     |       |       |       |       |       |       |       |       |
   | (12   |       |       |       |       |       |       |       |       |
   | 5007, |       |       |       |       |       |       |       |       |
   | DCM,  |       |       |       |       |       |       |       |       |
   | "M    |       |       |       |       |       |       |       |       |
   | easur |       |       |       |       |       |       |       |       |
   | ement |       |       |       |       |       |       |       |       |
   | Gr    |       |       |       |       |       |       |       |       |
   | oup") |       |       |       |       |       |       |       |       |
   | >     |       |       |       |       |       |       |       |       |
   | (12   |       |       |       |       |       |       |       |       |
   | 6070, |       |       |       |       |       |       |       |       |
   | DCM,  |       |       |       |       |       |       |       |       |
   | "Su   |       |       |       |       |       |       |       |       |
   | bject |       |       |       |       |       |       |       |       |
   | Time  |       |       |       |       |       |       |       |       |
   | Point |       |       |       |       |       |       |       |       |
   | Id    |       |       |       |       |       |       |       |       |
   | entif |       |       |       |       |       |       |       |       |
   | ier") |       |       |       |       |       |       |       |       |
   +-------+-------+-------+-------+-------+-------+-------+-------+-------+
   | (12   | TEXT  | 1     | U     |       |       |       |       | Not   |
   | 6000, |       |       |       |       |       |       |       | used  |
   | DCM,  |       |       |       |       |       |       |       | in    |
   | "Im   |       |       |       |       |       |       |       | AIM.  |
   | aging |       |       |       |       |       |       |       |       |
   | M     |       |       |       |       |       |       |       |       |
   | easur |       |       |       |       |       |       |       |       |
   | ement |       |       |       |       |       |       |       |       |
   | Rep   |       |       |       |       |       |       |       |       |
   | ort") |       |       |       |       |       |       |       |       |
   | >     |       |       |       |       |       |       |       |       |
   | (12   |       |       |       |       |       |       |       |       |
   | 6010, |       |       |       |       |       |       |       |       |
   | DCM,  |       |       |       |       |       |       |       |       |
   | "Im   |       |       |       |       |       |       |       |       |
   | aging |       |       |       |       |       |       |       |       |
   | Meas  |       |       |       |       |       |       |       |       |
   | ureme |       |       |       |       |       |       |       |       |
   | nts") |       |       |       |       |       |       |       |       |
   | >     |       |       |       |       |       |       |       |       |
   | (12   |       |       |       |       |       |       |       |       |
   | 5007, |       |       |       |       |       |       |       |       |
   | DCM,  |       |       |       |       |       |       |       |       |
   | "M    |       |       |       |       |       |       |       |       |
   | easur |       |       |       |       |       |       |       |       |
   | ement |       |       |       |       |       |       |       |       |
   | Gr    |       |       |       |       |       |       |       |       |
   | oup") |       |       |       |       |       |       |       |       |
   | >     |       |       |       |       |       |       |       |       |
   | (12   |       |       |       |       |       |       |       |       |
   | 6071, |       |       |       |       |       |       |       |       |
   | DCM,  |       |       |       |       |       |       |       |       |
   | "Pro  |       |       |       |       |       |       |       |       |
   | tocol |       |       |       |       |       |       |       |       |
   | Time  |       |       |       |       |       |       |       |       |
   | Point |       |       |       |       |       |       |       |       |
   | Id    |       |       |       |       |       |       |       |       |
   | entif |       |       |       |       |       |       |       |       |
   | ier") |       |       |       |       |       |       |       |       |
   +-------+-------+-------+-------+-------+-------+-------+-------+-------+
   | (12   | TEXT  | 1     | M     |       |       |       |       | Not   |
   | 6000, |       |       |       |       |       |       |       | used  |
   | DCM,  |       |       |       |       |       |       |       | in    |
   | "Im   |       |       |       |       |       |       |       | AIM.  |
   | aging |       |       |       |       |       |       |       |       |
   | M     |       |       |       |       |       |       |       |       |
   | easur |       |       |       |       |       |       |       |       |
   | ement |       |       |       |       |       |       |       |       |
   | Rep   |       |       |       |       |       |       |       |       |
   | ort") |       |       |       |       |       |       |       |       |
   | >     |       |       |       |       |       |       |       |       |
   | (12   |       |       |       |       |       |       |       |       |
   | 6010, |       |       |       |       |       |       |       |       |
   | DCM,  |       |       |       |       |       |       |       |       |
   | "Im   |       |       |       |       |       |       |       |       |
   | aging |       |       |       |       |       |       |       |       |
   | Meas  |       |       |       |       |       |       |       |       |
   | ureme |       |       |       |       |       |       |       |       |
   | nts") |       |       |       |       |       |       |       |       |
   | >     |       |       |       |       |       |       |       |       |
   | (12   |       |       |       |       |       |       |       |       |
   | 5007, |       |       |       |       |       |       |       |       |
   | DCM,  |       |       |       |       |       |       |       |       |
   | "M    |       |       |       |       |       |       |       |       |
   | easur |       |       |       |       |       |       |       |       |
   | ement |       |       |       |       |       |       |       |       |
   | Gr    |       |       |       |       |       |       |       |       |
   | oup") |       |       |       |       |       |       |       |       |
   | >     |       |       |       |       |       |       |       |       |
   | `     |       |       |       |       |       |       |       |       |
   | (C234 |       |       |       |       |       |       |       |       |
   | 8792, |       |       |       |       |       |       |       |       |
   | UMLS, |       |       |       |       |       |       |       |       |
   | "Time |       |       |       |       |       |       |       |       |
   | Poi   |       |       |       |       |       |       |       |       |
   | nt")  |       |       |       |       |       |       |       |       |
   | <http |       |       |       |       |       |       |       |       |
   | s://u |       |       |       |       |       |       |       |       |
   | ts.nl |       |       |       |       |       |       |       |       |
   | m.nih |       |       |       |       |       |       |       |       |
   | .gov/ |       |       |       |       |       |       |       |       |
   | metat |       |       |       |       |       |       |       |       |
   | hesau |       |       |       |       |       |       |       |       |
   | rus.h |       |       |       |       |       |       |       |       |
   | tml?c |       |       |       |       |       |       |       |       |
   | ui=C2 |       |       |       |       |       |       |       |       |
   | 34879 |       |       |       |       |       |       |       |       |
   | 2>`__ |       |       |       |       |       |       |       |       |
   +-------+-------+-------+-------+-------+-------+-------+-------+-------+
   | (12   | CODE  | 1-n   | U     |       |       |       |       | B     |
   | 6000, |       |       |       |       |       |       |       |       |
   | DCM,  |       |       |       |       |       |       |       | Not   |
   | "Im   |       |       |       |       |       |       |       | used  |
   | aging |       |       |       |       |       |       |       | in    |
   | M     |       |       |       |       |       |       |       | AIM.  |
   | easur |       |       |       |       |       |       |       |       |
   | ement |       |       |       |       |       |       |       |       |
   | Rep   |       |       |       |       |       |       |       |       |
   | ort") |       |       |       |       |       |       |       |       |
   | >     |       |       |       |       |       |       |       |       |
   | (12   |       |       |       |       |       |       |       |       |
   | 6010, |       |       |       |       |       |       |       |       |
   | DCM,  |       |       |       |       |       |       |       |       |
   | "Im   |       |       |       |       |       |       |       |       |
   | aging |       |       |       |       |       |       |       |       |
   | Meas  |       |       |       |       |       |       |       |       |
   | ureme |       |       |       |       |       |       |       |       |
   | nts") |       |       |       |       |       |       |       |       |
   | >     |       |       |       |       |       |       |       |       |
   | (12   |       |       |       |       |       |       |       |       |
   | 5007, |       |       |       |       |       |       |       |       |
   | DCM,  |       |       |       |       |       |       |       |       |
   | "M    |       |       |       |       |       |       |       |       |
   | easur |       |       |       |       |       |       |       |       |
   | ement |       |       |       |       |       |       |       |       |
   | Gr    |       |       |       |       |       |       |       |       |
   | oup") |       |       |       |       |       |       |       |       |
   | >     |       |       |       |       |       |       |       |       |
   | (12   |       |       |       |       |       |       |       |       |
   | 6072, |       |       |       |       |       |       |       |       |
   | DCM,  |       |       |       |       |       |       |       |       |
   | "Time |       |       |       |       |       |       |       |       |
   | Point |       |       |       |       |       |       |       |       |
   | T     |       |       |       |       |       |       |       |       |
   | ype") |       |       |       |       |       |       |       |       |
   +-------+-------+-------+-------+-------+-------+-------+-------+-------+
   | (12   | NUM   | 1     | U     |       |       |       |       | Not   |
   | 6000, |       |       |       |       |       |       |       | used  |
   | DCM,  |       |       |       |       |       |       |       | in    |
   | "Im   |       |       |       |       |       |       |       | AIM.  |
   | aging |       |       |       |       |       |       |       |       |
   | M     |       |       |       |       |       |       |       |       |
   | easur |       |       |       |       |       |       |       |       |
   | ement |       |       |       |       |       |       |       |       |
   | Rep   |       |       |       |       |       |       |       |       |
   | ort") |       |       |       |       |       |       |       |       |
   | >     |       |       |       |       |       |       |       |       |
   | (12   |       |       |       |       |       |       |       |       |
   | 6010, |       |       |       |       |       |       |       |       |
   | DCM,  |       |       |       |       |       |       |       |       |
   | "Im   |       |       |       |       |       |       |       |       |
   | aging |       |       |       |       |       |       |       |       |
   | Meas  |       |       |       |       |       |       |       |       |
   | ureme |       |       |       |       |       |       |       |       |
   | nts") |       |       |       |       |       |       |       |       |
   | >     |       |       |       |       |       |       |       |       |
   | (12   |       |       |       |       |       |       |       |       |
   | 5007, |       |       |       |       |       |       |       |       |
   | DCM,  |       |       |       |       |       |       |       |       |
   | "M    |       |       |       |       |       |       |       |       |
   | easur |       |       |       |       |       |       |       |       |
   | ement |       |       |       |       |       |       |       |       |
   | Gr    |       |       |       |       |       |       |       |       |
   | oup") |       |       |       |       |       |       |       |       |
   | >     |       |       |       |       |       |       |       |       |
   | (12   |       |       |       |       |       |       |       |       |
   | 6073, |       |       |       |       |       |       |       |       |
   | DCM,  |       |       |       |       |       |       |       |       |
   | "Time |       |       |       |       |       |       |       |       |
   | Point |       |       |       |       |       |       |       |       |
   | Or    |       |       |       |       |       |       |       |       |
   | der") |       |       |       |       |       |       |       |       |
   +-------+-------+-------+-------+-------+-------+-------+-------+-------+
   | (12   | NUM   | 1     | U     |       |       |       |       | Not   |
   | 6000, |       |       |       |       |       |       |       | used  |
   | DCM,  |       |       |       |       |       |       |       | in    |
   | "Im   |       |       |       |       |       |       |       | AIM.  |
   | aging |       |       |       |       |       |       |       |       |
   | M     |       |       |       |       |       |       |       |       |
   | easur |       |       |       |       |       |       |       |       |
   | ement |       |       |       |       |       |       |       |       |
   | Rep   |       |       |       |       |       |       |       |       |
   | ort") |       |       |       |       |       |       |       |       |
   | >     |       |       |       |       |       |       |       |       |
   | (12   |       |       |       |       |       |       |       |       |
   | 6010, |       |       |       |       |       |       |       |       |
   | DCM,  |       |       |       |       |       |       |       |       |
   | "Im   |       |       |       |       |       |       |       |       |
   | aging |       |       |       |       |       |       |       |       |
   | Meas  |       |       |       |       |       |       |       |       |
   | ureme |       |       |       |       |       |       |       |       |
   | nts") |       |       |       |       |       |       |       |       |
   | >     |       |       |       |       |       |       |       |       |
   | (12   |       |       |       |       |       |       |       |       |
   | 5007, |       |       |       |       |       |       |       |       |
   | DCM,  |       |       |       |       |       |       |       |       |
   | "M    |       |       |       |       |       |       |       |       |
   | easur |       |       |       |       |       |       |       |       |
   | ement |       |       |       |       |       |       |       |       |
   | Gr    |       |       |       |       |       |       |       |       |
   | oup") |       |       |       |       |       |       |       |       |
   | >     |       |       |       |       |       |       |       |       |
   | (12   |       |       |       |       |       |       |       |       |
   | 8740, |       |       |       |       |       |       |       |       |
   | DCM,  |       |       |       |       |       |       |       |       |
   | "Lo   |       |       |       |       |       |       |       |       |
   | ngitu |       |       |       |       |       |       |       |       |
   | dinal |       |       |       |       |       |       |       |       |
   | Tem   |       |       |       |       |       |       |       |       |
   | poral |       |       |       |       |       |       |       |       |
   | O     |       |       |       |       |       |       |       |       |
   | ffset |       |       |       |       |       |       |       |       |
   | from  |       |       |       |       |       |       |       |       |
   | Ev    |       |       |       |       |       |       |       |       |
   | ent") |       |       |       |       |       |       |       |       |
   +-------+-------+-------+-------+-------+-------+-------+-------+-------+
   | (12   | CODE  | 1     | U     |       |       |       |       | Not   |
   | 6000, |       |       |       |       |       |       |       | used  |
   | DCM,  |       |       |       |       |       |       |       | in    |
   | "Im   |       |       |       |       |       |       |       | AIM.  |
   | aging |       |       |       |       |       |       |       |       |
   | M     |       |       |       |       |       |       |       |       |
   | easur |       |       |       |       |       |       |       |       |
   | ement |       |       |       |       |       |       |       |       |
   | Rep   |       |       |       |       |       |       |       |       |
   | ort") |       |       |       |       |       |       |       |       |
   | >     |       |       |       |       |       |       |       |       |
   | (12   |       |       |       |       |       |       |       |       |
   | 6010, |       |       |       |       |       |       |       |       |
   | DCM,  |       |       |       |       |       |       |       |       |
   | "Im   |       |       |       |       |       |       |       |       |
   | aging |       |       |       |       |       |       |       |       |
   | Meas  |       |       |       |       |       |       |       |       |
   | ureme |       |       |       |       |       |       |       |       |
   | nts") |       |       |       |       |       |       |       |       |
   | >     |       |       |       |       |       |       |       |       |
   | (12   |       |       |       |       |       |       |       |       |
   | 5007, |       |       |       |       |       |       |       |       |
   | DCM,  |       |       |       |       |       |       |       |       |
   | "M    |       |       |       |       |       |       |       |       |
   | easur |       |       |       |       |       |       |       |       |
   | ement |       |       |       |       |       |       |       |       |
   | Gr    |       |       |       |       |       |       |       |       |
   | oup") |       |       |       |       |       |       |       |       |
   | >     |       |       |       |       |       |       |       |       |
   | (12   |       |       |       |       |       |       |       |       |
   | 8740, |       |       |       |       |       |       |       |       |
   | DCM,  |       |       |       |       |       |       |       |       |
   | "Lo   |       |       |       |       |       |       |       |       |
   | ngitu |       |       |       |       |       |       |       |       |
   | dinal |       |       |       |       |       |       |       |       |
   | Tem   |       |       |       |       |       |       |       |       |
   | poral |       |       |       |       |       |       |       |       |
   | O     |       |       |       |       |       |       |       |       |
   | ffset |       |       |       |       |       |       |       |       |
   | from  |       |       |       |       |       |       |       |       |
   | Ev    |       |       |       |       |       |       |       |       |
   | ent") |       |       |       |       |       |       |       |       |
   | >     |       |       |       |       |       |       |       |       |
   | (12   |       |       |       |       |       |       |       |       |
   | 8741, |       |       |       |       |       |       |       |       |
   | DCM,  |       |       |       |       |       |       |       |       |
   | "Lo   |       |       |       |       |       |       |       |       |
   | ngitu |       |       |       |       |       |       |       |       |
   | dinal |       |       |       |       |       |       |       |       |
   | Tem   |       |       |       |       |       |       |       |       |
   | poral |       |       |       |       |       |       |       |       |
   | Event |       |       |       |       |       |       |       |       |
   | T     |       |       |       |       |       |       |       |       |
   | ype") |       |       |       |       |       |       |       |       |
   +-------+-------+-------+-------+-------+-------+-------+-------+-------+

.. _sect_Mapping_TID_1410:

Mapping of Planar ROI Measurements
''''''''''''''''''''''''''''''''''

This section describes the mapping of .

.. table:: Mapping of Planar ROI Measurements

   +-------+-------+-------+-------+-------+-------+-------+-------+-------+
   | DICOM | DICOM | DICOM | DICOM | Gene  | AIM   | AIM   | AIM   | Co    |
   | SR    | VT    | VM    | Usage | rated | El    | Data  | Mu    | mment |
   | Path  |       |       | Type  | Value | ement | Type  | ltipl |       |
   |       |       |       |       |       | or    |       | icity |       |
   |       |       |       |       |       | Attr  |       |       |       |
   |       |       |       |       |       | ibute |       |       |       |
   +=======+=======+=======+=======+=======+=======+=======+=======+=======+
   | (12   | CONT  | 1     | M     |       | Image |       |       | The   |
   | 6000, | AINER |       |       |       | ​Anno |       |       | value |
   | DCM,  |       |       |       |       | tatio |       |       | of    |
   | "Im   |       |       |       |       | n​​Co |       |       | ai    |
   | aging |       |       |       |       | llect |       |       | m:uni |
   | M     |       |       |       |       | ion/​ |       |       | que​I |
   | easur |       |       |       |       | image |       |       | denti |
   | ement |       |       |       |       | ​Anno |       |       | fier/ |
   | Rep   |       |       |       |       | tatio |       |       | @root |
   | ort") |       |       |       |       | ns/​I |       |       | is    |
   | >     |       |       |       |       | mage​ |       |       | m     |
   | (12   |       |       |       |       | Annot |       |       | apped |
   | 6010, |       |       |       |       | ation |       |       | to    |
   | DCM,  |       |       |       |       |       |       |       | the   |
   | "Im   |       |       |       |       |       |       |       | Obser |
   | aging |       |       |       |       |       |       |       | vatio |
   | Meas  |       |       |       |       |       |       |       | n​UID |
   | ureme |       |       |       |       |       |       |       | Attr  |
   | nts") |       |       |       |       |       |       |       | ibute |
   | >     |       |       |       |       |       |       |       | of    |
   | (12   |       |       |       |       |       |       |       | the   |
   | 5007, |       |       |       |       |       |       |       | CONTA |
   | DCM,  |       |       |       |       |       |       |       | INER. |
   | "M    |       |       |       |       |       |       |       |       |
   | easur |       |       |       |       |       |       |       | The   |
   | ement |       |       |       |       |       |       |       | value |
   | Gr    |       |       |       |       |       |       |       | of    |
   | oup") |       |       |       |       |       |       |       | aim:  |
   |       |       |       |       |       |       |       |       | date​ |
   |       |       |       |       |       |       |       |       | Time/ |
   |       |       |       |       |       |       |       |       | @root |
   |       |       |       |       |       |       |       |       | is    |
   |       |       |       |       |       |       |       |       | m     |
   |       |       |       |       |       |       |       |       | apped |
   |       |       |       |       |       |       |       |       | to    |
   |       |       |       |       |       |       |       |       | the   |
   |       |       |       |       |       |       |       |       | O     |
   |       |       |       |       |       |       |       |       | bserv |
   |       |       |       |       |       |       |       |       | ation |
   |       |       |       |       |       |       |       |       | ​Date |
   |       |       |       |       |       |       |       |       | ​Time |
   |       |       |       |       |       |       |       |       | ​Attr |
   |       |       |       |       |       |       |       |       | ibute |
   |       |       |       |       |       |       |       |       | of    |
   |       |       |       |       |       |       |       |       | the   |
   |       |       |       |       |       |       |       |       | CONTA |
   |       |       |       |       |       |       |       |       | INER. |
   +-------+-------+-------+-------+-------+-------+-------+-------+-------+
   | (12   | TEXT  | 1     | U     |       |       |       |       | Not   |
   | 6000, |       |       |       |       |       |       |       | pr    |
   | DCM,  |       |       |       |       |       |       |       | esent |
   | "Im   |       |       |       |       |       |       |       | in    |
   | aging |       |       |       |       |       |       |       | AIM.  |
   | M     |       |       |       |       |       |       |       |       |
   | easur |       |       |       |       |       |       |       | Ident |
   | ement |       |       |       |       |       |       |       | ifies |
   | Rep   |       |       |       |       |       |       |       | the   |
   | ort") |       |       |       |       |       |       |       | se    |
   | >     |       |       |       |       |       |       |       | ssion |
   | (12   |       |       |       |       |       |       |       | d     |
   | 6010, |       |       |       |       |       |       |       | uring |
   | DCM,  |       |       |       |       |       |       |       | which |
   | "Im   |       |       |       |       |       |       |       | the   |
   | aging |       |       |       |       |       |       |       | me    |
   | Meas  |       |       |       |       |       |       |       | asure |
   | ureme |       |       |       |       |       |       |       | ments |
   | nts") |       |       |       |       |       |       |       | were  |
   | >     |       |       |       |       |       |       |       | made. |
   | (12   |       |       |       |       |       |       |       | The   |
   | 5007, |       |       |       |       |       |       |       | NCI   |
   | DCM,  |       |       |       |       |       |       |       | Thes  |
   | "M    |       |       |       |       |       |       |       | aurus |
   | easur |       |       |       |       |       |       |       | defin |
   | ement |       |       |       |       |       |       |       | ition |
   | Gr    |       |       |       |       |       |       |       | is    |
   | oup") |       |       |       |       |       |       |       | "     |
   | >     |       |       |       |       |       |       |       | time, |
   | (C6   |       |       |       |       |       |       |       | pe    |
   | 7447, |       |       |       |       |       |       |       | riod, |
   | NCIt, |       |       |       |       |       |       |       | or    |
   | "Act  |       |       |       |       |       |       |       | term  |
   | ivity |       |       |       |       |       |       |       | de    |
   | Sess  |       |       |       |       |       |       |       | voted |
   | ion") |       |       |       |       |       |       |       | to    |
   |       |       |       |       |       |       |       |       | some  |
   |       |       |       |       |       |       |       |       | activ |
   |       |       |       |       |       |       |       |       | ity". |
   +-------+-------+-------+-------+-------+-------+-------+-------+-------+
   | (12   | TEXT  | 1     | M     |       | Imag  | ST    | 1     |       |
   | 6000, |       |       |       |       | e​Ann |       |       |       |
   | DCM,  |       |       |       |       | otati |       |       |       |
   | "Im   |       |       |       |       | on​​C |       |       |       |
   | aging |       |       |       |       | ollec |       |       |       |
   | M     |       |       |       |       | tion/ |       |       |       |
   | easur |       |       |       |       | ​imag |       |       |       |
   | ement |       |       |       |       | e​Ann |       |       |       |
   | Rep   |       |       |       |       | otati |       |       |       |
   | ort") |       |       |       |       | ons/​ |       |       |       |
   | >     |       |       |       |       | Image |       |       |       |
   | (12   |       |       |       |       | ​Anno |       |       |       |
   | 6010, |       |       |       |       | tatio |       |       |       |
   | DCM,  |       |       |       |       | n/​na |       |       |       |
   | "Im   |       |       |       |       | me/​@ |       |       |       |
   | aging |       |       |       |       | value |       |       |       |
   | Meas  |       |       |       |       |       |       |       |       |
   | ureme |       |       |       |       |       |       |       |       |
   | nts") |       |       |       |       |       |       |       |       |
   | >     |       |       |       |       |       |       |       |       |
   | (12   |       |       |       |       |       |       |       |       |
   | 5007, |       |       |       |       |       |       |       |       |
   | DCM,  |       |       |       |       |       |       |       |       |
   | "M    |       |       |       |       |       |       |       |       |
   | easur |       |       |       |       |       |       |       |       |
   | ement |       |       |       |       |       |       |       |       |
   | Gr    |       |       |       |       |       |       |       |       |
   | oup") |       |       |       |       |       |       |       |       |
   | >     |       |       |       |       |       |       |       |       |
   | (11   |       |       |       |       |       |       |       |       |
   | 2039, |       |       |       |       |       |       |       |       |
   | DCM,  |       |       |       |       |       |       |       |       |
   | "Tra  |       |       |       |       |       |       |       |       |
   | cking |       |       |       |       |       |       |       |       |
   | Id    |       |       |       |       |       |       |       |       |
   | entif |       |       |       |       |       |       |       |       |
   | ier") |       |       |       |       |       |       |       |       |
   +-------+-------+-------+-------+-------+-------+-------+-------+-------+
   | (12   | U     | 1     | M     |       | Imag  | II    | 1     | If    |
   | 6000, | IDREF |       |       |       | e​Ann |       |       | t     |
   | DCM,  |       |       |       |       | otati |       |       | racki |
   | "Im   |       |       |       |       | on​​C |       |       | ng​Un |
   | aging |       |       |       |       | ollec |       |       | ique​ |
   | M     |       |       |       |       | tion/ |       |       | Ident |
   | easur |       |       |       |       | ​imag |       |       | ifier |
   | ement |       |       |       |       | e​Ann |       |       | is    |
   | Rep   |       |       |       |       | otati |       |       | ab    |
   | ort") |       |       |       |       | ons/​ |       |       | sent, |
   | >     |       |       |       |       | Image |       |       | then  |
   | (12   |       |       |       |       | ​Anno |       |       | Imag  |
   | 6010, |       |       |       |       | tatio |       |       | e​Ann |
   | DCM,  |       |       |       |       | n/​tr |       |       | otati |
   | "Im   |       |       |       |       | ackin |       |       | on/​u |
   | aging |       |       |       |       | g​Uni |       |       | nique |
   | Meas  |       |       |       |       | queId |       |       | Ident |
   | ureme |       |       |       |       | entif |       |       | ifier |
   | nts") |       |       |       |       | ier/​ |       |       | may   |
   | >     |       |       |       |       | @root |       |       | be    |
   | (12   |       |       |       |       |       |       |       | used  |
   | 5007, |       |       |       |       |       |       |       | as a  |
   | DCM,  |       |       |       |       |       |       |       | proxy |
   | "M    |       |       |       |       |       |       |       | for   |
   | easur |       |       |       |       |       |       |       | Tra   |
   | ement |       |       |       |       |       |       |       | cking |
   | Gr    |       |       |       |       |       |       |       | U     |
   | oup") |       |       |       |       |       |       |       | nique |
   | >     |       |       |       |       |       |       |       | I     |
   | (11   |       |       |       |       |       |       |       | denti |
   | 2040, |       |       |       |       |       |       |       | fier, |
   | DCM,  |       |       |       |       |       |       |       | but   |
   | "Tra  |       |       |       |       |       |       |       | this  |
   | cking |       |       |       |       |       |       |       | does  |
   | U     |       |       |       |       |       |       |       | not   |
   | nique |       |       |       |       |       |       |       | allow |
   | Id    |       |       |       |       |       |       |       | lo    |
   | entif |       |       |       |       |       |       |       | ngitu |
   | ier") |       |       |       |       |       |       |       | dinal |
   |       |       |       |       |       |       |       |       | iden  |
   |       |       |       |       |       |       |       |       | tific |
   |       |       |       |       |       |       |       |       | ation |
   |       |       |       |       |       |       |       |       | of    |
   |       |       |       |       |       |       |       |       | the   |
   |       |       |       |       |       |       |       |       | same  |
   |       |       |       |       |       |       |       |       | l     |
   |       |       |       |       |       |       |       |       | esion |
   |       |       |       |       |       |       |       |       | be    |
   |       |       |       |       |       |       |       |       | cause |
   |       |       |       |       |       |       |       |       | Imag  |
   |       |       |       |       |       |       |       |       | e​Ann |
   |       |       |       |       |       |       |       |       | otati |
   |       |       |       |       |       |       |       |       | on/​u |
   |       |       |       |       |       |       |       |       | nique |
   |       |       |       |       |       |       |       |       | Ident |
   |       |       |       |       |       |       |       |       | ifier |
   |       |       |       |       |       |       |       |       | must  |
   |       |       |       |       |       |       |       |       | be    |
   |       |       |       |       |       |       |       |       | u     |
   |       |       |       |       |       |       |       |       | nique |
   |       |       |       |       |       |       |       |       | to    |
   |       |       |       |       |       |       |       |       | each  |
   |       |       |       |       |       |       |       |       | AIM   |
   |       |       |       |       |       |       |       |       | annot |
   |       |       |       |       |       |       |       |       | ation |
   |       |       |       |       |       |       |       |       | file, |
   |       |       |       |       |       |       |       |       | in    |
   |       |       |       |       |       |       |       |       | which |
   |       |       |       |       |       |       |       |       | case  |
   |       |       |       |       |       |       |       |       | only  |
   |       |       |       |       |       |       |       |       | Im    |
   |       |       |       |       |       |       |       |       | age​A |
   |       |       |       |       |       |       |       |       | nnota |
   |       |       |       |       |       |       |       |       | tion/ |
   |       |       |       |       |       |       |       |       | ​name |
   |       |       |       |       |       |       |       |       | can   |
   |       |       |       |       |       |       |       |       | be    |
   |       |       |       |       |       |       |       |       | used  |
   |       |       |       |       |       |       |       |       | to    |
   |       |       |       |       |       |       |       |       | reco  |
   |       |       |       |       |       |       |       |       | gnize |
   |       |       |       |       |       |       |       |       | co    |
   |       |       |       |       |       |       |       |       | mmona |
   |       |       |       |       |       |       |       |       | lity. |
   +-------+-------+-------+-------+-------+-------+-------+-------+-------+
   | (12   | CODE  | 1     | U     |       | Image | CD    | 1..n  | Only  |
   | 6000, |       |       |       |       | ​Anno |       |       | a     |
   | DCM,  |       |       |       |       | tatio |       |       | s     |
   | "Im   |       |       |       |       | n​​Co |       |       | ingle |
   | aging |       |       |       |       | llect |       |       | ai    |
   | M     |       |       |       |       | ion/​ |       |       | m:typ |
   | easur |       |       |       |       | image |       |       | eCode |
   | ement |       |       |       |       | ​Anno |       |       | value |
   | Rep   |       |       |       |       | tatio |       |       | can   |
   | ort") |       |       |       |       | ns/​I |       |       | be    |
   | >     |       |       |       |       | mage​ |       |       | ma    |
   | (12   |       |       |       |       | Annot |       |       | pped. |
   | 6010, |       |       |       |       | ation |       |       |       |
   | DCM,  |       |       |       |       | /​typ |       |       |       |
   | "Im   |       |       |       |       | eCode |       |       |       |
   | aging |       |       |       |       |       |       |       |       |
   | Meas  |       |       |       |       |       |       |       |       |
   | ureme |       |       |       |       |       |       |       |       |
   | nts") |       |       |       |       |       |       |       |       |
   | >     |       |       |       |       |       |       |       |       |
   | (12   |       |       |       |       |       |       |       |       |
   | 5007, |       |       |       |       |       |       |       |       |
   | DCM,  |       |       |       |       |       |       |       |       |
   | "M    |       |       |       |       |       |       |       |       |
   | easur |       |       |       |       |       |       |       |       |
   | ement |       |       |       |       |       |       |       |       |
   | Gr    |       |       |       |       |       |       |       |       |
   | oup") |       |       |       |       |       |       |       |       |
   | >     |       |       |       |       |       |       |       |       |
   | (12   |       |       |       |       |       |       |       |       |
   | 1071, |       |       |       |       |       |       |       |       |
   | DCM,  |       |       |       |       |       |       |       |       |
   | "Find |       |       |       |       |       |       |       |       |
   | ing") |       |       |       |       |       |       |       |       |
   +-------+-------+-------+-------+-------+-------+-------+-------+-------+
   | (12   | IN    | 1     | U     | `Ma   | Not   |       |       |       |
   | 6000, | CLUDE |       |       | pping | used  |       |       |       |
   | DCM,  |       |       |       | of    | in    |       |       |       |
   | "Im   |       |       |       | Time  | AIM.  |       |       |       |
   | aging |       |       |       | Point |       |       |       |       |
   | M     |       |       |       | Conte |       |       |       |       |
   | easur |       |       |       | xt <# |       |       |       |       |
   | ement |       |       |       | sect_ |       |       |       |       |
   | Rep   |       |       |       | Mappi |       |       |       |       |
   | ort") |       |       |       | ng_TI |       |       |       |       |
   | >     |       |       |       | D_150 |       |       |       |       |
   | (12   |       |       |       | 2>`__ |       |       |       |       |
   | 6010, |       |       |       |       |       |       |       |       |
   | DCM,  |       |       |       |       |       |       |       |       |
   | "Im   |       |       |       |       |       |       |       |       |
   | aging |       |       |       |       |       |       |       |       |
   | Meas  |       |       |       |       |       |       |       |       |
   | ureme |       |       |       |       |       |       |       |       |
   | nts") |       |       |       |       |       |       |       |       |
   | >     |       |       |       |       |       |       |       |       |
   | (12   |       |       |       |       |       |       |       |       |
   | 5007, |       |       |       |       |       |       |       |       |
   | DCM,  |       |       |       |       |       |       |       |       |
   | "M    |       |       |       |       |       |       |       |       |
   | easur |       |       |       |       |       |       |       |       |
   | ement |       |       |       |       |       |       |       |       |
   | Gr    |       |       |       |       |       |       |       |       |
   | oup") |       |       |       |       |       |       |       |       |
   | >     |       |       |       |       |       |       |       |       |
   +-------+-------+-------+-------+-------+-------+-------+-------+-------+
   | (12   | S     | 1     | MC    |       | Im    |       |       | A     |
   | 6000, | COORD |       |       |       | age​A |       |       | Gr    |
   | DCM,  |       |       |       |       | nnota |       |       | aphic |
   | "Im   |       |       |       |       | tion​ |       |       | Type  |
   | aging |       |       |       |       | ​Coll |       |       | of    |
   | M     |       |       |       |       | ectio |       |       | MULTI |
   | easur |       |       |       |       | n/​im |       |       | POINT |
   | ement |       |       |       |       | age​A |       |       | is    |
   | Rep   |       |       |       |       | nnota |       |       | not   |
   | ort") |       |       |       |       | tions |       |       | perm  |
   | >     |       |       |       |       | /​Ima |       |       | itted |
   | (12   |       |       |       |       | ge​An |       |       | in    |
   | 6010, |       |       |       |       | notat |       |       | the   |
   | DCM,  |       |       |       |       | ion/​ |       |       | DICOM |
   | "Im   |       |       |       |       | ​mark |       |       | temp  |
   | aging |       |       |       |       | up​En |       |       | late. |
   | Meas  |       |       |       |       | tity​ |       |       |       |
   | ureme |       |       |       |       | Colle |       |       | One   |
   | nts") |       |       |       |       | ction |       |       | or    |
   | >     |       |       |       |       | /​Mar |       |       | more  |
   | (12   |       |       |       |       | kupEn |       |       | Ma    |
   | 5007, |       |       |       |       | tity/ |       |       | rkupE |
   | DCM,  |       |       |       |       | ​twoD |       |       | ntity |
   | "M    |       |       |       |       | imens |       |       | inst  |
   | easur |       |       |       |       | ion​S |       |       | ances |
   | ement |       |       |       |       | patia |       |       | w     |
   | Gr    |       |       |       |       | lCoor |       |       | ithin |
   | oup") |       |       |       |       | dinat |       |       | an    |
   | >     |       |       |       |       | e​​Co |       |       | I     |
   | (11   |       |       |       |       | llect |       |       | mage​ |
   | 1030, |       |       |       |       | ion/​ |       |       | Annot |
   | DCM,  |       |       |       |       | TwoDi |       |       | ation |
   | "     |       |       |       |       | mensi |       |       | ins   |
   | Image |       |       |       |       | on​Sp |       |       | tance |
   | Reg   |       |       |       |       | atial |       |       | may   |
   | ion") |       |       |       |       | Coord |       |       | be    |
   |       |       |       |       |       | inate |       |       | c     |
   |       |       |       |       |       |       |       |       | onstr |
   |       |       |       |       |       |       |       |       | ained |
   |       |       |       |       |       |       |       |       | to be |
   |       |       |       |       |       |       |       |       | assoc |
   |       |       |       |       |       |       |       |       | iated |
   |       |       |       |       |       |       |       |       | with  |
   |       |       |       |       |       |       |       |       | parti |
   |       |       |       |       |       |       |       |       | cular |
   |       |       |       |       |       |       |       |       | NUM   |
   |       |       |       |       |       |       |       |       | meas  |
   |       |       |       |       |       |       |       |       | ureme |
   |       |       |       |       |       |       |       |       | nt(s) |
   |       |       |       |       |       |       |       |       | in    |
   |       |       |       |       |       |       |       |       | the   |
   |       |       |       |       |       |       |       |       | inc   |
   |       |       |       |       |       |       |       |       | luded |
   |       |       |       |       |       |       |       |       | TID   |
   |       |       |       |       |       |       |       |       | 1419  |
   |       |       |       |       |       |       |       |       | by a  |
   |       |       |       |       |       |       |       |       | Calc  |
   |       |       |       |       |       |       |       |       | ulati |
   |       |       |       |       |       |       |       |       | on​En |
   |       |       |       |       |       |       |       |       | tity​ |
   |       |       |       |       |       |       |       |       | Refer |
   |       |       |       |       |       |       |       |       | ences |
   |       |       |       |       |       |       |       |       | ​Mark |
   |       |       |       |       |       |       |       |       | up​En |
   |       |       |       |       |       |       |       |       | tity​ |
   |       |       |       |       |       |       |       |       | State |
   |       |       |       |       |       |       |       |       | ment. |
   +-------+-------+-------+-------+-------+-------+-------+-------+-------+
   | (12   | IMAGE | 1     | M     |       | Ima   | II,   | 1,    | The   |
   | 6000, |       |       |       |       | ge​An | INT   | 0..1  | Refer |
   | DCM,  |       |       |       |       | notat |       |       | enced |
   | "Im   |       |       |       |       | ion​​ |       |       | SOP   |
   | aging |       |       |       |       | Colle |       |       | Class |
   | M     |       |       |       |       | ction |       |       | UID   |
   | easur |       |       |       |       | /​ima |       |       | is    |
   | ement |       |       |       |       | ge​An |       |       | obt   |
   | Rep   |       |       |       |       | notat |       |       | ained |
   | ort") |       |       |       |       | ions/ |       |       | from  |
   | >     |       |       |       |       | ​Imag |       |       | ima   |
   | (12   |       |       |       |       | e​Ann |       |       | geRef |
   | 6010, |       |       |       |       | otati |       |       | erenc |
   | DCM,  |       |       |       |       | on/​​ |       |       | e​Ent |
   | "Im   |       |       |       |       | marku |       |       | ity​C |
   | aging |       |       |       |       | p​Ent |       |       | ollec |
   | Meas  |       |       |       |       | ity​C |       |       | tion; |
   | ureme |       |       |       |       | ollec |       |       | see   |
   | nts") |       |       |       |       | tion/ |       |       | `tabl |
   | >     |       |       |       |       | ​Mark |       |       | e_tit |
   | (12   |       |       |       |       | upEnt |       |       | le <# |
   | 5007, |       |       |       |       | ity/​ |       |       | table |
   | DCM,  |       |       |       |       | image |       |       | _A.8- |
   | "M    |       |       |       |       | Refer |       |       | 5>`__ |
   | easur |       |       |       |       | enceU |       |       |       |
   | ement |       |       |       |       | id/​@ |       |       |       |
   | Gr    |       |       |       |       | root, |       |       |       |
   | oup") |       |       |       |       | refe  |       |       |       |
   | >     |       |       |       |       | rence |       |       |       |
   | (11   |       |       |       |       | dFram |       |       |       |
   | 1030, |       |       |       |       | eNumb |       |       |       |
   | DCM,  |       |       |       |       | er/​@ |       |       |       |
   | "     |       |       |       |       | value |       |       |       |
   | Image |       |       |       |       |       |       |       |       |
   | Reg   |       |       |       |       |       |       |       |       |
   | ion") |       |       |       |       |       |       |       |       |
   | >     |       |       |       |       |       |       |       |       |
   | IMAGE |       |       |       |       |       |       |       |       |
   +-------+-------+-------+-------+-------+-------+-------+-------+-------+
   | (12   | IMAGE | 1     | MC    |       | Ima   |       |       | Refe  |
   | 6000, |       |       |       |       | ge​An |       |       | rence |
   | DCM,  |       |       |       |       | notat |       |       | shall |
   | "Im   |       |       |       |       | ion​​ |       |       | be to |
   | aging |       |       |       |       | Colle |       |       | a     |
   | M     |       |       |       |       | ction |       |       | Se    |
   | easur |       |       |       |       | /​ima |       |       | gment |
   | ement |       |       |       |       | ge​An |       |       | ation |
   | Rep   |       |       |       |       | notat |       |       | I     |
   | ort") |       |       |       |       | ions/ |       |       | mage, |
   | >     |       |       |       |       | ​Imag |       |       | with  |
   | (12   |       |       |       |       | e​Ann |       |       | a     |
   | 6010, |       |       |       |       | otati |       |       | s     |
   | DCM,  |       |       |       |       | on/​​ |       |       | ingle |
   | "Im   |       |       |       |       | segme |       |       | value |
   | aging |       |       |       |       | ntati |       |       | spec  |
   | Meas  |       |       |       |       | on​En |       |       | ified |
   | ureme |       |       |       |       | tity​ |       |       | in    |
   | nts") |       |       |       |       | Colle |       |       | Refer |
   | >     |       |       |       |       | ction |       |       | enced |
   | (12   |       |       |       |       | /​Seg |       |       | Frame |
   | 5007, |       |       |       |       | menta |       |       | Nu    |
   | DCM,  |       |       |       |       | tionE |       |       | mber, |
   | "M    |       |       |       |       | ntity |       |       | and   |
   | easur |       |       |       |       |       |       |       | with  |
   | ement |       |       |       |       |       |       |       | a     |
   | Gr    |       |       |       |       |       |       |       | s     |
   | oup") |       |       |       |       |       |       |       | ingle |
   | >     |       |       |       |       |       |       |       | value |
   | (12   |       |       |       |       |       |       |       | spec  |
   | 1214, |       |       |       |       |       |       |       | ified |
   | DCM,  |       |       |       |       |       |       |       | in    |
   | "     |       |       |       |       |       |       |       | Refer |
   | Refer |       |       |       |       |       |       |       | enced |
   | enced |       |       |       |       |       |       |       | Se    |
   | Se    |       |       |       |       |       |       |       | gment |
   | gment |       |       |       |       |       |       |       | Nu    |
   | ation |       |       |       |       |       |       |       | mber. |
   | Fr    |       |       |       |       |       |       |       |       |
   | ame") |       |       |       |       |       |       |       | The   |
   |       |       |       |       |       |       |       |       | value |
   |       |       |       |       |       |       |       |       | of    |
   |       |       |       |       |       |       |       |       | ai    |
   |       |       |       |       |       |       |       |       | m:uni |
   |       |       |       |       |       |       |       |       | que​I |
   |       |       |       |       |       |       |       |       | denti |
   |       |       |       |       |       |       |       |       | fier/ |
   |       |       |       |       |       |       |       |       | @root |
   |       |       |       |       |       |       |       |       | is    |
   |       |       |       |       |       |       |       |       | m     |
   |       |       |       |       |       |       |       |       | apped |
   |       |       |       |       |       |       |       |       | to    |
   |       |       |       |       |       |       |       |       | the   |
   |       |       |       |       |       |       |       |       | Obser |
   |       |       |       |       |       |       |       |       | vatio |
   |       |       |       |       |       |       |       |       | n​UID |
   |       |       |       |       |       |       |       |       | Attr  |
   |       |       |       |       |       |       |       |       | ibute |
   |       |       |       |       |       |       |       |       | of    |
   |       |       |       |       |       |       |       |       | the   |
   |       |       |       |       |       |       |       |       | I     |
   |       |       |       |       |       |       |       |       | MAGE. |
   |       |       |       |       |       |       |       |       |       |
   |       |       |       |       |       |       |       |       | One   |
   |       |       |       |       |       |       |       |       | or    |
   |       |       |       |       |       |       |       |       | more  |
   |       |       |       |       |       |       |       |       | Se    |
   |       |       |       |       |       |       |       |       | gment |
   |       |       |       |       |       |       |       |       | ation |
   |       |       |       |       |       |       |       |       | refer |
   |       |       |       |       |       |       |       |       | ences |
   |       |       |       |       |       |       |       |       | w     |
   |       |       |       |       |       |       |       |       | ithin |
   |       |       |       |       |       |       |       |       | an    |
   |       |       |       |       |       |       |       |       | I     |
   |       |       |       |       |       |       |       |       | mage​ |
   |       |       |       |       |       |       |       |       | Annot |
   |       |       |       |       |       |       |       |       | ation |
   |       |       |       |       |       |       |       |       | ins   |
   |       |       |       |       |       |       |       |       | tance |
   |       |       |       |       |       |       |       |       | may   |
   |       |       |       |       |       |       |       |       | be    |
   |       |       |       |       |       |       |       |       | c     |
   |       |       |       |       |       |       |       |       | onstr |
   |       |       |       |       |       |       |       |       | ained |
   |       |       |       |       |       |       |       |       | to be |
   |       |       |       |       |       |       |       |       | assoc |
   |       |       |       |       |       |       |       |       | iated |
   |       |       |       |       |       |       |       |       | with  |
   |       |       |       |       |       |       |       |       | parti |
   |       |       |       |       |       |       |       |       | cular |
   |       |       |       |       |       |       |       |       | NUM   |
   |       |       |       |       |       |       |       |       | meas  |
   |       |       |       |       |       |       |       |       | ureme |
   |       |       |       |       |       |       |       |       | nt(s) |
   |       |       |       |       |       |       |       |       | in    |
   |       |       |       |       |       |       |       |       | the   |
   |       |       |       |       |       |       |       |       | inc   |
   |       |       |       |       |       |       |       |       | luded |
   |       |       |       |       |       |       |       |       | TID   |
   |       |       |       |       |       |       |       |       | 1419  |
   |       |       |       |       |       |       |       |       | by a  |
   |       |       |       |       |       |       |       |       | Calcu |
   |       |       |       |       |       |       |       |       | latio |
   |       |       |       |       |       |       |       |       | n​Ent |
   |       |       |       |       |       |       |       |       | ity​R |
   |       |       |       |       |       |       |       |       | efere |
   |       |       |       |       |       |       |       |       | nces​ |
   |       |       |       |       |       |       |       |       | Segme |
   |       |       |       |       |       |       |       |       | ntati |
   |       |       |       |       |       |       |       |       | on​En |
   |       |       |       |       |       |       |       |       | tity​ |
   |       |       |       |       |       |       |       |       | State |
   |       |       |       |       |       |       |       |       | ment. |
   +-------+-------+-------+-------+-------+-------+-------+-------+-------+
   | (12   | IMAGE | 1     | MC    |       | I     |       |       |       |
   | 6000, |       |       |       |       | mage​ |       |       |       |
   | DCM,  |       |       |       |       | Annot |       |       |       |
   | "Im   |       |       |       |       | ation |       |       |       |
   | aging |       |       |       |       | ​​Col |       |       |       |
   | M     |       |       |       |       | lecti |       |       |       |
   | easur |       |       |       |       | on/​i |       |       |       |
   | ement |       |       |       |       | mage​ |       |       |       |
   | Rep   |       |       |       |       | Annot |       |       |       |
   | ort") |       |       |       |       | ation |       |       |       |
   | >     |       |       |       |       | s/​Im |       |       |       |
   | (12   |       |       |       |       | age​A |       |       |       |
   | 6010, |       |       |       |       | nnota |       |       |       |
   | DCM,  |       |       |       |       | tion/ |       |       |       |
   | "Im   |       |       |       |       | ​​seg |       |       |       |
   | aging |       |       |       |       | menta |       |       |       |
   | Meas  |       |       |       |       | tion​ |       |       |       |
   | ureme |       |       |       |       | Entit |       |       |       |
   | nts") |       |       |       |       | y​Col |       |       |       |
   | >     |       |       |       |       | lecti |       |       |       |
   | (12   |       |       |       |       | on/​S |       |       |       |
   | 5007, |       |       |       |       | egmen |       |       |       |
   | DCM,  |       |       |       |       | tatio |       |       |       |
   | "M    |       |       |       |       | nEnti |       |       |       |
   | easur |       |       |       |       | ty/​r |       |       |       |
   | ement |       |       |       |       | efere |       |       |       |
   | Gr    |       |       |       |       | ncedS |       |       |       |
   | oup") |       |       |       |       | opIns |       |       |       |
   | >     |       |       |       |       | tance |       |       |       |
   | (12   |       |       |       |       | Uid/​ |       |       |       |
   | 1233, |       |       |       |       | @root |       |       |       |
   | DCM,  |       |       |       |       |       |       |       |       |
   | "S    |       |       |       |       |       |       |       |       |
   | ource |       |       |       |       |       |       |       |       |
   | image |       |       |       |       |       |       |       |       |
   | for   |       |       |       |       |       |       |       |       |
   | segm  |       |       |       |       |       |       |       |       |
   | entat |       |       |       |       |       |       |       |       |
   | ion") |       |       |       |       |       |       |       |       |
   +-------+-------+-------+-------+-------+-------+-------+-------+-------+
   | (12   | IMAGE | 1     | U     |       |       |       |       | Not   |
   | 6000, |       |       |       |       |       |       |       | used  |
   | DCM,  |       |       |       |       |       |       |       | in    |
   | "Im   |       |       |       |       |       |       |       | AIM.  |
   | aging |       |       |       |       |       |       |       |       |
   | M     |       |       |       |       |       |       |       |       |
   | easur |       |       |       |       |       |       |       |       |
   | ement |       |       |       |       |       |       |       |       |
   | Rep   |       |       |       |       |       |       |       |       |
   | ort") |       |       |       |       |       |       |       |       |
   | >     |       |       |       |       |       |       |       |       |
   | (12   |       |       |       |       |       |       |       |       |
   | 6010, |       |       |       |       |       |       |       |       |
   | DCM,  |       |       |       |       |       |       |       |       |
   | "Im   |       |       |       |       |       |       |       |       |
   | aging |       |       |       |       |       |       |       |       |
   | Meas  |       |       |       |       |       |       |       |       |
   | ureme |       |       |       |       |       |       |       |       |
   | nts") |       |       |       |       |       |       |       |       |
   | >     |       |       |       |       |       |       |       |       |
   | (12   |       |       |       |       |       |       |       |       |
   | 5007, |       |       |       |       |       |       |       |       |
   | DCM,  |       |       |       |       |       |       |       |       |
   | "M    |       |       |       |       |       |       |       |       |
   | easur |       |       |       |       |       |       |       |       |
   | ement |       |       |       |       |       |       |       |       |
   | Gr    |       |       |       |       |       |       |       |       |
   | oup") |       |       |       |       |       |       |       |       |
   | >     |       |       |       |       |       |       |       |       |
   | (12   |       |       |       |       |       |       |       |       |
   | 1200, |       |       |       |       |       |       |       |       |
   | DCM,  |       |       |       |       |       |       |       |       |
   | "Il   |       |       |       |       |       |       |       |       |
   | lustr |       |       |       |       |       |       |       |       |
   | ation |       |       |       |       |       |       |       |       |
   | of    |       |       |       |       |       |       |       |       |
   | ROI") |       |       |       |       |       |       |       |       |
   +-------+-------+-------+-------+-------+-------+-------+-------+-------+
   | (12   | COMP  | 1     | U     |       |       |       |       | Not   |
   | 6000, | OSITE |       |       |       |       |       |       | used  |
   | DCM,  |       |       |       |       |       |       |       | in    |
   | "Im   |       |       |       |       |       |       |       | AIM.  |
   | aging |       |       |       |       |       |       |       |       |
   | M     |       |       |       |       |       |       |       |       |
   | easur |       |       |       |       |       |       |       |       |
   | ement |       |       |       |       |       |       |       |       |
   | Rep   |       |       |       |       |       |       |       |       |
   | ort") |       |       |       |       |       |       |       |       |
   | >     |       |       |       |       |       |       |       |       |
   | (12   |       |       |       |       |       |       |       |       |
   | 6010, |       |       |       |       |       |       |       |       |
   | DCM,  |       |       |       |       |       |       |       |       |
   | "Im   |       |       |       |       |       |       |       |       |
   | aging |       |       |       |       |       |       |       |       |
   | Meas  |       |       |       |       |       |       |       |       |
   | ureme |       |       |       |       |       |       |       |       |
   | nts") |       |       |       |       |       |       |       |       |
   | >     |       |       |       |       |       |       |       |       |
   | (12   |       |       |       |       |       |       |       |       |
   | 5007, |       |       |       |       |       |       |       |       |
   | DCM,  |       |       |       |       |       |       |       |       |
   | "M    |       |       |       |       |       |       |       |       |
   | easur |       |       |       |       |       |       |       |       |
   | ement |       |       |       |       |       |       |       |       |
   | Gr    |       |       |       |       |       |       |       |       |
   | oup") |       |       |       |       |       |       |       |       |
   | >     |       |       |       |       |       |       |       |       |
   | (12   |       |       |       |       |       |       |       |       |
   | 6100, |       |       |       |       |       |       |       |       |
   | DCM,  |       |       |       |       |       |       |       |       |
   | "Real |       |       |       |       |       |       |       |       |
   | World |       |       |       |       |       |       |       |       |
   | Value |       |       |       |       |       |       |       |       |
   | Map   |       |       |       |       |       |       |       |       |
   | used  |       |       |       |       |       |       |       |       |
   | for   |       |       |       |       |       |       |       |       |
   | mea   |       |       |       |       |       |       |       |       |
   | surem |       |       |       |       |       |       |       |       |
   | ent") |       |       |       |       |       |       |       |       |
   +-------+-------+-------+-------+-------+-------+-------+-------+-------+
   | (12   | IN    | 1     | M     | `Ma   |       |       |       |       |
   | 6000, | CLUDE |       |       | pping |       |       |       |       |
   | DCM,  |       |       |       | of    |       |       |       |       |
   | "Im   |       |       |       | ROI   |       |       |       |       |
   | aging |       |       |       | Measu |       |       |       |       |
   | M     |       |       |       | remen |       |       |       |       |
   | easur |       |       |       | ts <# |       |       |       |       |
   | ement |       |       |       | sect_ |       |       |       |       |
   | Rep   |       |       |       | Mappi |       |       |       |       |
   | ort") |       |       |       | ng_TI |       |       |       |       |
   | >     |       |       |       | D_141 |       |       |       |       |
   | (12   |       |       |       | 9>`__ |       |       |       |       |
   | 6010, |       |       |       |       |       |       |       |       |
   | DCM,  |       |       |       |       |       |       |       |       |
   | "Im   |       |       |       |       |       |       |       |       |
   | aging |       |       |       |       |       |       |       |       |
   | Meas  |       |       |       |       |       |       |       |       |
   | ureme |       |       |       |       |       |       |       |       |
   | nts") |       |       |       |       |       |       |       |       |
   | >     |       |       |       |       |       |       |       |       |
   | (12   |       |       |       |       |       |       |       |       |
   | 5007, |       |       |       |       |       |       |       |       |
   | DCM,  |       |       |       |       |       |       |       |       |
   | "M    |       |       |       |       |       |       |       |       |
   | easur |       |       |       |       |       |       |       |       |
   | ement |       |       |       |       |       |       |       |       |
   | Gr    |       |       |       |       |       |       |       |       |
   | oup") |       |       |       |       |       |       |       |       |
   | >     |       |       |       |       |       |       |       |       |
   +-------+-------+-------+-------+-------+-------+-------+-------+-------+
   | (12   | CODE  | 1-n   | U     |       |       |       |       | Not   |
   | 6000, |       |       |       |       |       |       |       | used  |
   | DCM,  |       |       |       |       |       |       |       | in    |
   | "Im   |       |       |       |       |       |       |       | AIM.  |
   | aging |       |       |       |       |       |       |       |       |
   | M     |       |       |       |       |       |       |       |       |
   | easur |       |       |       |       |       |       |       |       |
   | ement |       |       |       |       |       |       |       |       |
   | Rep   |       |       |       |       |       |       |       |       |
   | ort") |       |       |       |       |       |       |       |       |
   | >     |       |       |       |       |       |       |       |       |
   | (12   |       |       |       |       |       |       |       |       |
   | 6010, |       |       |       |       |       |       |       |       |
   | DCM,  |       |       |       |       |       |       |       |       |
   | "Im   |       |       |       |       |       |       |       |       |
   | aging |       |       |       |       |       |       |       |       |
   | Meas  |       |       |       |       |       |       |       |       |
   | ureme |       |       |       |       |       |       |       |       |
   | nts") |       |       |       |       |       |       |       |       |
   | >     |       |       |       |       |       |       |       |       |
   | (12   |       |       |       |       |       |       |       |       |
   | 5007, |       |       |       |       |       |       |       |       |
   | DCM,  |       |       |       |       |       |       |       |       |
   | "M    |       |       |       |       |       |       |       |       |
   | easur |       |       |       |       |       |       |       |       |
   | ement |       |       |       |       |       |       |       |       |
   | Gr    |       |       |       |       |       |       |       |       |
   | oup") |       |       |       |       |       |       |       |       |
   | >     |       |       |       |       |       |       |       |       |
   | $Qu   |       |       |       |       |       |       |       |       |
   | alita |       |       |       |       |       |       |       |       |
   | tiveE |       |       |       |       |       |       |       |       |
   | valua |       |       |       |       |       |       |       |       |
   | tions |       |       |       |       |       |       |       |       |
   +-------+-------+-------+-------+-------+-------+-------+-------+-------+
   | (12   | TEXT  | 1-n   | U     |       | Im    |       |       | The   |
   | 6000, |       |       |       |       | age​A |       |       | para  |
   | DCM,  |       |       |       |       | nnota |       |       | meter |
   | "Im   |       |       |       |       | tion​ |       |       | $Qua  |
   | aging |       |       |       |       | ​Coll |       |       | litat |
   | M     |       |       |       |       | ectio |       |       | ive​E |
   | easur |       |       |       |       | n/​im |       |       | valua |
   | ement |       |       |       |       | age​A |       |       | tions |
   | Rep   |       |       |       |       | nnota |       |       | is    |
   | ort") |       |       |       |       | tions |       |       | not   |
   | >     |       |       |       |       | /​Ima |       |       | used  |
   | (12   |       |       |       |       | ge​An |       |       | in    |
   | 6010, |       |       |       |       | notat |       |       | AIM,  |
   | DCM,  |       |       |       |       | ion/​ |       |       | but   |
   | "Im   |       |       |       |       | comme |       |       | this  |
   | aging |       |       |       |       | nt/​@ |       |       | TEXT  |
   | Meas  |       |       |       |       | value |       |       | co    |
   | ureme |       |       |       |       |       |       |       | ntent |
   | nts") |       |       |       |       |       |       |       | item  |
   | >     |       |       |       |       |       |       |       | is    |
   | (12   |       |       |       |       |       |       |       | used  |
   | 5007, |       |       |       |       |       |       |       | to    |
   | DCM,  |       |       |       |       |       |       |       | map   |
   | "M    |       |       |       |       |       |       |       | the   |
   | easur |       |       |       |       |       |       |       | AIM   |
   | ement |       |       |       |       |       |       |       | co    |
   | Gr    |       |       |       |       |       |       |       | mment |
   | oup") |       |       |       |       |       |       |       | as if |
   | >     |       |       |       |       |       |       |       | it    |
   | (12   |       |       |       |       |       |       |       | were  |
   | 1106, |       |       |       |       |       |       |       | a     |
   | DCM,  |       |       |       |       |       |       |       | Q     |
   | "Comm |       |       |       |       |       |       |       | ualit |
   | ent") |       |       |       |       |       |       |       | ative |
   |       |       |       |       |       |       |       |       | Evalu |
   |       |       |       |       |       |       |       |       | ation |
   +-------+-------+-------+-------+-------+-------+-------+-------+-------+

.. _sect_Mapping_TID_1411:

Mapping of Volumetric ROI Measurements
''''''''''''''''''''''''''''''''''''''

This section describes the mapping of .

.. table:: Mapping of Volumetric ROI Measurements

   +-------+-------+-------+-------+-------+-------+-------+-------+-------+
   | DICOM | DICOM | DICOM | DICOM | Gene  | AIM   | AIM   | AIM   | Co    |
   | SR    | VT    | VM    | Usage | rated | El    | Data  | Mu    | mment |
   | Path  |       |       | Type  | Value | ement | Type  | ltipl |       |
   |       |       |       |       |       | or    |       | icity |       |
   |       |       |       |       |       | Attr  |       |       |       |
   |       |       |       |       |       | ibute |       |       |       |
   +=======+=======+=======+=======+=======+=======+=======+=======+=======+
   | (12   | CONT  | 1     | M     |       | Image |       |       | The   |
   | 6000, | AINER |       |       |       | ​Anno |       |       | value |
   | DCM,  |       |       |       |       | tatio |       |       | of    |
   | "Im   |       |       |       |       | n​​Co |       |       | ai    |
   | aging |       |       |       |       | llect |       |       | m:uni |
   | M     |       |       |       |       | ion/​ |       |       | que​I |
   | easur |       |       |       |       | image |       |       | denti |
   | ement |       |       |       |       | ​Anno |       |       | fier/ |
   | Rep   |       |       |       |       | tatio |       |       | @root |
   | ort") |       |       |       |       | ns/​I |       |       | is    |
   | >     |       |       |       |       | mage​ |       |       | m     |
   | (12   |       |       |       |       | Annot |       |       | apped |
   | 6010, |       |       |       |       | ation |       |       | to    |
   | DCM,  |       |       |       |       |       |       |       | the   |
   | "Im   |       |       |       |       |       |       |       | Obser |
   | aging |       |       |       |       |       |       |       | vatio |
   | Meas  |       |       |       |       |       |       |       | n​UID |
   | ureme |       |       |       |       |       |       |       | Attr  |
   | nts") |       |       |       |       |       |       |       | ibute |
   | >     |       |       |       |       |       |       |       | of    |
   | (12   |       |       |       |       |       |       |       | the   |
   | 5007, |       |       |       |       |       |       |       | CONTA |
   | DCM,  |       |       |       |       |       |       |       | INER. |
   | "M    |       |       |       |       |       |       |       |       |
   | easur |       |       |       |       |       |       |       | The   |
   | ement |       |       |       |       |       |       |       | value |
   | Gr    |       |       |       |       |       |       |       | of    |
   | oup") |       |       |       |       |       |       |       | aim:  |
   |       |       |       |       |       |       |       |       | date​ |
   |       |       |       |       |       |       |       |       | Time/ |
   |       |       |       |       |       |       |       |       | @root |
   |       |       |       |       |       |       |       |       | is    |
   |       |       |       |       |       |       |       |       | m     |
   |       |       |       |       |       |       |       |       | apped |
   |       |       |       |       |       |       |       |       | to    |
   |       |       |       |       |       |       |       |       | the   |
   |       |       |       |       |       |       |       |       | O     |
   |       |       |       |       |       |       |       |       | bserv |
   |       |       |       |       |       |       |       |       | ation |
   |       |       |       |       |       |       |       |       | ​Date |
   |       |       |       |       |       |       |       |       | ​Time |
   |       |       |       |       |       |       |       |       | ​Attr |
   |       |       |       |       |       |       |       |       | ibute |
   |       |       |       |       |       |       |       |       | of    |
   |       |       |       |       |       |       |       |       | the   |
   |       |       |       |       |       |       |       |       | CONTA |
   |       |       |       |       |       |       |       |       | INER. |
   +-------+-------+-------+-------+-------+-------+-------+-------+-------+
   | (12   | TEXT  | 1     | U     |       |       |       |       | Not   |
   | 6000, |       |       |       |       |       |       |       | pr    |
   | DCM,  |       |       |       |       |       |       |       | esent |
   | "Im   |       |       |       |       |       |       |       | in    |
   | aging |       |       |       |       |       |       |       | AIM.  |
   | M     |       |       |       |       |       |       |       |       |
   | easur |       |       |       |       |       |       |       | Ident |
   | ement |       |       |       |       |       |       |       | ifies |
   | Rep   |       |       |       |       |       |       |       | the   |
   | ort") |       |       |       |       |       |       |       | se    |
   | >     |       |       |       |       |       |       |       | ssion |
   | (12   |       |       |       |       |       |       |       | d     |
   | 6010, |       |       |       |       |       |       |       | uring |
   | DCM,  |       |       |       |       |       |       |       | which |
   | "Im   |       |       |       |       |       |       |       | the   |
   | aging |       |       |       |       |       |       |       | me    |
   | Meas  |       |       |       |       |       |       |       | asure |
   | ureme |       |       |       |       |       |       |       | ments |
   | nts") |       |       |       |       |       |       |       | were  |
   | >     |       |       |       |       |       |       |       | made. |
   | (12   |       |       |       |       |       |       |       | The   |
   | 5007, |       |       |       |       |       |       |       | NCI   |
   | DCM,  |       |       |       |       |       |       |       | Thes  |
   | "M    |       |       |       |       |       |       |       | aurus |
   | easur |       |       |       |       |       |       |       | defin |
   | ement |       |       |       |       |       |       |       | ition |
   | Gr    |       |       |       |       |       |       |       | is    |
   | oup") |       |       |       |       |       |       |       | "     |
   | >     |       |       |       |       |       |       |       | time, |
   | (C6   |       |       |       |       |       |       |       | pe    |
   | 7447, |       |       |       |       |       |       |       | riod, |
   | NCIt, |       |       |       |       |       |       |       | or    |
   | "Act  |       |       |       |       |       |       |       | term  |
   | ivity |       |       |       |       |       |       |       | de    |
   | Sess  |       |       |       |       |       |       |       | voted |
   | ion") |       |       |       |       |       |       |       | to    |
   |       |       |       |       |       |       |       |       | some  |
   |       |       |       |       |       |       |       |       | activ |
   |       |       |       |       |       |       |       |       | ity". |
   +-------+-------+-------+-------+-------+-------+-------+-------+-------+
   | (12   | TEXT  | 1     | M     |       | Imag  | ST    | 1     |       |
   | 6000, |       |       |       |       | e​Ann |       |       |       |
   | DCM,  |       |       |       |       | otati |       |       |       |
   | "Im   |       |       |       |       | on​​C |       |       |       |
   | aging |       |       |       |       | ollec |       |       |       |
   | M     |       |       |       |       | tion/ |       |       |       |
   | easur |       |       |       |       | ​imag |       |       |       |
   | ement |       |       |       |       | e​Ann |       |       |       |
   | Rep   |       |       |       |       | otati |       |       |       |
   | ort") |       |       |       |       | ons/​ |       |       |       |
   | >     |       |       |       |       | Image |       |       |       |
   | (12   |       |       |       |       | ​Anno |       |       |       |
   | 6010, |       |       |       |       | tatio |       |       |       |
   | DCM,  |       |       |       |       | n/​na |       |       |       |
   | "Im   |       |       |       |       | me/​@ |       |       |       |
   | aging |       |       |       |       | value |       |       |       |
   | Meas  |       |       |       |       |       |       |       |       |
   | ureme |       |       |       |       |       |       |       |       |
   | nts") |       |       |       |       |       |       |       |       |
   | >     |       |       |       |       |       |       |       |       |
   | (12   |       |       |       |       |       |       |       |       |
   | 5007, |       |       |       |       |       |       |       |       |
   | DCM,  |       |       |       |       |       |       |       |       |
   | "M    |       |       |       |       |       |       |       |       |
   | easur |       |       |       |       |       |       |       |       |
   | ement |       |       |       |       |       |       |       |       |
   | Gr    |       |       |       |       |       |       |       |       |
   | oup") |       |       |       |       |       |       |       |       |
   | >     |       |       |       |       |       |       |       |       |
   | (11   |       |       |       |       |       |       |       |       |
   | 2039, |       |       |       |       |       |       |       |       |
   | DCM,  |       |       |       |       |       |       |       |       |
   | "Tra  |       |       |       |       |       |       |       |       |
   | cking |       |       |       |       |       |       |       |       |
   | Id    |       |       |       |       |       |       |       |       |
   | entif |       |       |       |       |       |       |       |       |
   | ier") |       |       |       |       |       |       |       |       |
   +-------+-------+-------+-------+-------+-------+-------+-------+-------+
   | (12   | U     | 1     | M     |       | Imag  | II    | 1     | If    |
   | 6000, | IDREF |       |       |       | e​Ann |       |       | t     |
   | DCM,  |       |       |       |       | otati |       |       | racki |
   | "Im   |       |       |       |       | on​​C |       |       | ng​Un |
   | aging |       |       |       |       | ollec |       |       | ique​ |
   | M     |       |       |       |       | tion/ |       |       | Ident |
   | easur |       |       |       |       | ​imag |       |       | ifier |
   | ement |       |       |       |       | e​Ann |       |       | is    |
   | Rep   |       |       |       |       | otati |       |       | ab    |
   | ort") |       |       |       |       | ons/​ |       |       | sent, |
   | >     |       |       |       |       | Image |       |       | then  |
   | (12   |       |       |       |       | ​Anno |       |       | Imag  |
   | 6010, |       |       |       |       | tatio |       |       | e​Ann |
   | DCM,  |       |       |       |       | n/​tr |       |       | otati |
   | "Im   |       |       |       |       | ackin |       |       | on/​u |
   | aging |       |       |       |       | g​Uni |       |       | nique |
   | Meas  |       |       |       |       | queId |       |       | Ident |
   | ureme |       |       |       |       | entif |       |       | ifier |
   | nts") |       |       |       |       | ier/​ |       |       | may   |
   | >     |       |       |       |       | @root |       |       | be    |
   | (12   |       |       |       |       |       |       |       | used  |
   | 5007, |       |       |       |       |       |       |       | as a  |
   | DCM,  |       |       |       |       |       |       |       | proxy |
   | "M    |       |       |       |       |       |       |       | for   |
   | easur |       |       |       |       |       |       |       | Tra   |
   | ement |       |       |       |       |       |       |       | cking |
   | Gr    |       |       |       |       |       |       |       | U     |
   | oup") |       |       |       |       |       |       |       | nique |
   | >     |       |       |       |       |       |       |       | I     |
   | (11   |       |       |       |       |       |       |       | denti |
   | 2040, |       |       |       |       |       |       |       | fier, |
   | DCM,  |       |       |       |       |       |       |       | but   |
   | "Tra  |       |       |       |       |       |       |       | this  |
   | cking |       |       |       |       |       |       |       | does  |
   | U     |       |       |       |       |       |       |       | not   |
   | nique |       |       |       |       |       |       |       | allow |
   | Id    |       |       |       |       |       |       |       | lo    |
   | entif |       |       |       |       |       |       |       | ngitu |
   | ier") |       |       |       |       |       |       |       | dinal |
   |       |       |       |       |       |       |       |       | iden  |
   |       |       |       |       |       |       |       |       | tific |
   |       |       |       |       |       |       |       |       | ation |
   |       |       |       |       |       |       |       |       | of    |
   |       |       |       |       |       |       |       |       | the   |
   |       |       |       |       |       |       |       |       | same  |
   |       |       |       |       |       |       |       |       | l     |
   |       |       |       |       |       |       |       |       | esion |
   |       |       |       |       |       |       |       |       | be    |
   |       |       |       |       |       |       |       |       | cause |
   |       |       |       |       |       |       |       |       | Imag  |
   |       |       |       |       |       |       |       |       | e​Ann |
   |       |       |       |       |       |       |       |       | otati |
   |       |       |       |       |       |       |       |       | on/​u |
   |       |       |       |       |       |       |       |       | nique |
   |       |       |       |       |       |       |       |       | Ident |
   |       |       |       |       |       |       |       |       | ifier |
   |       |       |       |       |       |       |       |       | must  |
   |       |       |       |       |       |       |       |       | be    |
   |       |       |       |       |       |       |       |       | u     |
   |       |       |       |       |       |       |       |       | nique |
   |       |       |       |       |       |       |       |       | to    |
   |       |       |       |       |       |       |       |       | each  |
   |       |       |       |       |       |       |       |       | AIM   |
   |       |       |       |       |       |       |       |       | annot |
   |       |       |       |       |       |       |       |       | ation |
   |       |       |       |       |       |       |       |       | file, |
   |       |       |       |       |       |       |       |       | in    |
   |       |       |       |       |       |       |       |       | which |
   |       |       |       |       |       |       |       |       | case  |
   |       |       |       |       |       |       |       |       | only  |
   |       |       |       |       |       |       |       |       | Im    |
   |       |       |       |       |       |       |       |       | age​A |
   |       |       |       |       |       |       |       |       | nnota |
   |       |       |       |       |       |       |       |       | tion/ |
   |       |       |       |       |       |       |       |       | ​name |
   |       |       |       |       |       |       |       |       | can   |
   |       |       |       |       |       |       |       |       | be    |
   |       |       |       |       |       |       |       |       | used  |
   |       |       |       |       |       |       |       |       | to    |
   |       |       |       |       |       |       |       |       | reco  |
   |       |       |       |       |       |       |       |       | gnize |
   |       |       |       |       |       |       |       |       | co    |
   |       |       |       |       |       |       |       |       | mmona |
   |       |       |       |       |       |       |       |       | lity. |
   +-------+-------+-------+-------+-------+-------+-------+-------+-------+
   | (12   | CODE  | 1     | U     |       | Image | CD    | 1..n  | Only  |
   | 6000, |       |       |       |       | ​Anno |       |       | a     |
   | DCM,  |       |       |       |       | tatio |       |       | s     |
   | "Im   |       |       |       |       | n​​Co |       |       | ingle |
   | aging |       |       |       |       | llect |       |       | ai    |
   | M     |       |       |       |       | ion/​ |       |       | m:typ |
   | easur |       |       |       |       | image |       |       | eCode |
   | ement |       |       |       |       | ​Anno |       |       | value |
   | Rep   |       |       |       |       | tatio |       |       | can   |
   | ort") |       |       |       |       | ns/​I |       |       | be    |
   | >     |       |       |       |       | mage​ |       |       | ma    |
   | (12   |       |       |       |       | Annot |       |       | pped. |
   | 6010, |       |       |       |       | ation |       |       |       |
   | DCM,  |       |       |       |       | /​typ |       |       |       |
   | "Im   |       |       |       |       | eCode |       |       |       |
   | aging |       |       |       |       |       |       |       |       |
   | Meas  |       |       |       |       |       |       |       |       |
   | ureme |       |       |       |       |       |       |       |       |
   | nts") |       |       |       |       |       |       |       |       |
   | >     |       |       |       |       |       |       |       |       |
   | (12   |       |       |       |       |       |       |       |       |
   | 5007, |       |       |       |       |       |       |       |       |
   | DCM,  |       |       |       |       |       |       |       |       |
   | "M    |       |       |       |       |       |       |       |       |
   | easur |       |       |       |       |       |       |       |       |
   | ement |       |       |       |       |       |       |       |       |
   | Gr    |       |       |       |       |       |       |       |       |
   | oup") |       |       |       |       |       |       |       |       |
   | >     |       |       |       |       |       |       |       |       |
   | (12   |       |       |       |       |       |       |       |       |
   | 1071, |       |       |       |       |       |       |       |       |
   | DCM,  |       |       |       |       |       |       |       |       |
   | "Find |       |       |       |       |       |       |       |       |
   | ing") |       |       |       |       |       |       |       |       |
   +-------+-------+-------+-------+-------+-------+-------+-------+-------+
   | (12   | IN    | 1     | U     | `Ma   | Not   |       |       |       |
   | 6000, | CLUDE |       |       | pping | used  |       |       |       |
   | DCM,  |       |       |       | of    | in    |       |       |       |
   | "Im   |       |       |       | Time  | AIM.  |       |       |       |
   | aging |       |       |       | Point |       |       |       |       |
   | M     |       |       |       | Conte |       |       |       |       |
   | easur |       |       |       | xt <# |       |       |       |       |
   | ement |       |       |       | sect_ |       |       |       |       |
   | Rep   |       |       |       | Mappi |       |       |       |       |
   | ort") |       |       |       | ng_TI |       |       |       |       |
   | >     |       |       |       | D_150 |       |       |       |       |
   | (12   |       |       |       | 2>`__ |       |       |       |       |
   | 6010, |       |       |       |       |       |       |       |       |
   | DCM,  |       |       |       |       |       |       |       |       |
   | "Im   |       |       |       |       |       |       |       |       |
   | aging |       |       |       |       |       |       |       |       |
   | Meas  |       |       |       |       |       |       |       |       |
   | ureme |       |       |       |       |       |       |       |       |
   | nts") |       |       |       |       |       |       |       |       |
   | >     |       |       |       |       |       |       |       |       |
   | (12   |       |       |       |       |       |       |       |       |
   | 5007, |       |       |       |       |       |       |       |       |
   | DCM,  |       |       |       |       |       |       |       |       |
   | "M    |       |       |       |       |       |       |       |       |
   | easur |       |       |       |       |       |       |       |       |
   | ement |       |       |       |       |       |       |       |       |
   | Gr    |       |       |       |       |       |       |       |       |
   | oup") |       |       |       |       |       |       |       |       |
   | >     |       |       |       |       |       |       |       |       |
   +-------+-------+-------+-------+-------+-------+-------+-------+-------+
   | (12   | S     | 1-n   | MC    |       | Im    | REAL  | 1..n  | A     |
   | 6000, | COORD |       |       |       | age​A |       |       | Gr    |
   | DCM,  |       |       |       |       | nnota |       |       | aphic |
   | "Im   |       |       |       |       | tion​ |       |       | Type  |
   | aging |       |       |       |       | ​Coll |       |       | of    |
   | M     |       |       |       |       | ectio |       |       | MULTI |
   | easur |       |       |       |       | n/​im |       |       | POINT |
   | ement |       |       |       |       | age​A |       |       | is    |
   | Rep   |       |       |       |       | nnota |       |       | not   |
   | ort") |       |       |       |       | tions |       |       | perm  |
   | >     |       |       |       |       | /​Ima |       |       | itted |
   | (12   |       |       |       |       | ge​An |       |       | in    |
   | 6010, |       |       |       |       | notat |       |       | the   |
   | DCM,  |       |       |       |       | ion/​ |       |       | DICOM |
   | "Im   |       |       |       |       | ​mark |       |       | temp  |
   | aging |       |       |       |       | up​En |       |       | late. |
   | Meas  |       |       |       |       | tity​ |       |       |       |
   | ureme |       |       |       |       | Colle |       |       | The   |
   | nts") |       |       |       |       | ction |       |       | value |
   | >     |       |       |       |       | /​Mar |       |       | of    |
   | (12   |       |       |       |       | kupEn |       |       | aim:  |
   | 5007, |       |       |       |       | tity/ |       |       | ​Mark |
   | DCM,  |       |       |       |       | ​twoD |       |       | up​En |
   | "M    |       |       |       |       | imens |       |       | tity/ |
   | easur |       |       |       |       | ion​S |       |       | ​aim: |
   | ement |       |       |       |       | patia |       |       | ​uniq |
   | Gr    |       |       |       |       | lCoor |       |       | ue​Id |
   | oup") |       |       |       |       | dinat |       |       | entif |
   | >     |       |       |       |       | e​​Co |       |       | ier/​ |
   | (11   |       |       |       |       | llect |       |       | @root |
   | 1030, |       |       |       |       | ion/​ |       |       | is    |
   | DCM,  |       |       |       |       | TwoDi |       |       | m     |
   | "     |       |       |       |       | mensi |       |       | apped |
   | Image |       |       |       |       | on​Sp |       |       | to    |
   | Reg   |       |       |       |       | atial |       |       | the   |
   | ion") |       |       |       |       | Coord |       |       | Obser |
   |       |       |       |       |       | inate |       |       | vatio |
   |       |       |       |       |       |       |       |       | n​UID |
   |       |       |       |       |       |       |       |       | Attr  |
   |       |       |       |       |       |       |       |       | ibute |
   |       |       |       |       |       |       |       |       | of    |
   |       |       |       |       |       |       |       |       | the   |
   |       |       |       |       |       |       |       |       | SC    |
   |       |       |       |       |       |       |       |       | OORD. |
   |       |       |       |       |       |       |       |       |       |
   |       |       |       |       |       |       |       |       | One   |
   |       |       |       |       |       |       |       |       | or    |
   |       |       |       |       |       |       |       |       | more  |
   |       |       |       |       |       |       |       |       | Ma    |
   |       |       |       |       |       |       |       |       | rkupE |
   |       |       |       |       |       |       |       |       | ntity |
   |       |       |       |       |       |       |       |       | inst  |
   |       |       |       |       |       |       |       |       | ances |
   |       |       |       |       |       |       |       |       | w     |
   |       |       |       |       |       |       |       |       | ithin |
   |       |       |       |       |       |       |       |       | an    |
   |       |       |       |       |       |       |       |       | I     |
   |       |       |       |       |       |       |       |       | mage​ |
   |       |       |       |       |       |       |       |       | Annot |
   |       |       |       |       |       |       |       |       | ation |
   |       |       |       |       |       |       |       |       | ins   |
   |       |       |       |       |       |       |       |       | tance |
   |       |       |       |       |       |       |       |       | may   |
   |       |       |       |       |       |       |       |       | be    |
   |       |       |       |       |       |       |       |       | c     |
   |       |       |       |       |       |       |       |       | onstr |
   |       |       |       |       |       |       |       |       | ained |
   |       |       |       |       |       |       |       |       | to be |
   |       |       |       |       |       |       |       |       | assoc |
   |       |       |       |       |       |       |       |       | iated |
   |       |       |       |       |       |       |       |       | with  |
   |       |       |       |       |       |       |       |       | parti |
   |       |       |       |       |       |       |       |       | cular |
   |       |       |       |       |       |       |       |       | NUM   |
   |       |       |       |       |       |       |       |       | meas  |
   |       |       |       |       |       |       |       |       | ureme |
   |       |       |       |       |       |       |       |       | nt(s) |
   |       |       |       |       |       |       |       |       | in    |
   |       |       |       |       |       |       |       |       | the   |
   |       |       |       |       |       |       |       |       | inc   |
   |       |       |       |       |       |       |       |       | luded |
   |       |       |       |       |       |       |       |       | TID   |
   |       |       |       |       |       |       |       |       | 1419  |
   |       |       |       |       |       |       |       |       | by a  |
   |       |       |       |       |       |       |       |       | Calc  |
   |       |       |       |       |       |       |       |       | ulati |
   |       |       |       |       |       |       |       |       | on​En |
   |       |       |       |       |       |       |       |       | tity​ |
   |       |       |       |       |       |       |       |       | Refer |
   |       |       |       |       |       |       |       |       | ences |
   |       |       |       |       |       |       |       |       | ​Mark |
   |       |       |       |       |       |       |       |       | up​En |
   |       |       |       |       |       |       |       |       | tity​ |
   |       |       |       |       |       |       |       |       | State |
   |       |       |       |       |       |       |       |       | ment. |
   +-------+-------+-------+-------+-------+-------+-------+-------+-------+
   | (12   | IMAGE | 1     | M     |       | Ima   | II,   | 1,    | The   |
   | 6000, |       |       |       |       | ge​An | INT   | 0..1  | Refer |
   | DCM,  |       |       |       |       | notat |       |       | enced |
   | "Im   |       |       |       |       | ion​​ |       |       | SOP   |
   | aging |       |       |       |       | Colle |       |       | Class |
   | M     |       |       |       |       | ction |       |       | UID   |
   | easur |       |       |       |       | /​ima |       |       | is    |
   | ement |       |       |       |       | ge​An |       |       | obt   |
   | Rep   |       |       |       |       | notat |       |       | ained |
   | ort") |       |       |       |       | ions/ |       |       | from  |
   | >     |       |       |       |       | ​Imag |       |       | ima   |
   | (12   |       |       |       |       | e​Ann |       |       | geRef |
   | 6010, |       |       |       |       | otati |       |       | erenc |
   | DCM,  |       |       |       |       | on/​​ |       |       | e​Ent |
   | "Im   |       |       |       |       | marku |       |       | ity​C |
   | aging |       |       |       |       | p​Ent |       |       | ollec |
   | Meas  |       |       |       |       | ity​C |       |       | tion; |
   | ureme |       |       |       |       | ollec |       |       | see   |
   | nts") |       |       |       |       | tion/ |       |       | `tabl |
   | >     |       |       |       |       | ​Mark |       |       | e_tit |
   | (12   |       |       |       |       | upEnt |       |       | le <# |
   | 5007, |       |       |       |       | ity/​ |       |       | table |
   | DCM,  |       |       |       |       | image |       |       | _A.8- |
   | "M    |       |       |       |       | Refer |       |       | 5>`__ |
   | easur |       |       |       |       | enceU |       |       |       |
   | ement |       |       |       |       | id/​@ |       |       |       |
   | Gr    |       |       |       |       | root, |       |       |       |
   | oup") |       |       |       |       | refe  |       |       |       |
   | >     |       |       |       |       | rence |       |       |       |
   | (11   |       |       |       |       | dFram |       |       |       |
   | 1030, |       |       |       |       | eNumb |       |       |       |
   | DCM,  |       |       |       |       | er/​@ |       |       |       |
   | "     |       |       |       |       | value |       |       |       |
   | Image |       |       |       |       |       |       |       |       |
   | Reg   |       |       |       |       |       |       |       |       |
   | ion") |       |       |       |       |       |       |       |       |
   | >     |       |       |       |       |       |       |       |       |
   | IMAGE |       |       |       |       |       |       |       |       |
   +-------+-------+-------+-------+-------+-------+-------+-------+-------+
   | (12   | IMAGE | 1     | MC    |       | Ima   | INT   | 0..1  | Refe  |
   | 6000, |       |       |       |       | ge​An |       |       | rence |
   | DCM,  |       |       |       |       | notat |       |       | shall |
   | "Im   |       |       |       |       | ion​​ |       |       | be to |
   | aging |       |       |       |       | Colle |       |       | a     |
   | M     |       |       |       |       | ction |       |       | Se    |
   | easur |       |       |       |       | /​ima |       |       | gment |
   | ement |       |       |       |       | ge​An |       |       | ation |
   | Rep   |       |       |       |       | notat |       |       | Image |
   | ort") |       |       |       |       | ions/ |       |       | or    |
   | >     |       |       |       |       | ​Imag |       |       | Su    |
   | (12   |       |       |       |       | e​Ann |       |       | rface |
   | 6010, |       |       |       |       | otati |       |       | Se    |
   | DCM,  |       |       |       |       | on/​​ |       |       | gment |
   | "Im   |       |       |       |       | segme |       |       | ation |
   | aging |       |       |       |       | ntati |       |       | ob    |
   | Meas  |       |       |       |       | on​En |       |       | ject, |
   | ureme |       |       |       |       | tity​ |       |       | with  |
   | nts") |       |       |       |       | Colle |       |       | a     |
   | >     |       |       |       |       | ction |       |       | s     |
   | (12   |       |       |       |       | /​Seg |       |       | ingle |
   | 5007, |       |       |       |       | menta |       |       | value |
   | DCM,  |       |       |       |       | tionE |       |       | spec  |
   | "M    |       |       |       |       | ntity |       |       | ified |
   | easur |       |       |       |       |       |       |       | in    |
   | ement |       |       |       |       |       |       |       | Refer |
   | Gr    |       |       |       |       |       |       |       | enced |
   | oup") |       |       |       |       |       |       |       | Se    |
   | >     |       |       |       |       |       |       |       | gment |
   | (12   |       |       |       |       |       |       |       | Nu    |
   | 1191, |       |       |       |       |       |       |       | mber. |
   | DCM,  |       |       |       |       |       |       |       |       |
   | "     |       |       |       |       |       |       |       | One   |
   | Refer |       |       |       |       |       |       |       | or    |
   | enced |       |       |       |       |       |       |       | more  |
   | Segm  |       |       |       |       |       |       |       | Se    |
   | ent") |       |       |       |       |       |       |       | gment |
   |       |       |       |       |       |       |       |       | ation |
   |       |       |       |       |       |       |       |       | refer |
   |       |       |       |       |       |       |       |       | ences |
   |       |       |       |       |       |       |       |       | w     |
   |       |       |       |       |       |       |       |       | ithin |
   |       |       |       |       |       |       |       |       | an    |
   |       |       |       |       |       |       |       |       | I     |
   |       |       |       |       |       |       |       |       | mage​ |
   |       |       |       |       |       |       |       |       | Annot |
   |       |       |       |       |       |       |       |       | ation |
   |       |       |       |       |       |       |       |       | ins   |
   |       |       |       |       |       |       |       |       | tance |
   |       |       |       |       |       |       |       |       | may   |
   |       |       |       |       |       |       |       |       | be    |
   |       |       |       |       |       |       |       |       | c     |
   |       |       |       |       |       |       |       |       | onstr |
   |       |       |       |       |       |       |       |       | ained |
   |       |       |       |       |       |       |       |       | to be |
   |       |       |       |       |       |       |       |       | assoc |
   |       |       |       |       |       |       |       |       | iated |
   |       |       |       |       |       |       |       |       | with  |
   |       |       |       |       |       |       |       |       | parti |
   |       |       |       |       |       |       |       |       | cular |
   |       |       |       |       |       |       |       |       | NUM   |
   |       |       |       |       |       |       |       |       | meas  |
   |       |       |       |       |       |       |       |       | ureme |
   |       |       |       |       |       |       |       |       | nt(s) |
   |       |       |       |       |       |       |       |       | in    |
   |       |       |       |       |       |       |       |       | the   |
   |       |       |       |       |       |       |       |       | inc   |
   |       |       |       |       |       |       |       |       | luded |
   |       |       |       |       |       |       |       |       | TID   |
   |       |       |       |       |       |       |       |       | 1419  |
   |       |       |       |       |       |       |       |       | by a  |
   |       |       |       |       |       |       |       |       | Calc  |
   |       |       |       |       |       |       |       |       | ulati |
   |       |       |       |       |       |       |       |       | on​En |
   |       |       |       |       |       |       |       |       | tity​ |
   |       |       |       |       |       |       |       |       | Refer |
   |       |       |       |       |       |       |       |       | ences |
   |       |       |       |       |       |       |       |       | ​Segm |
   |       |       |       |       |       |       |       |       | entat |
   |       |       |       |       |       |       |       |       | ion​E |
   |       |       |       |       |       |       |       |       | ntity |
   |       |       |       |       |       |       |       |       | ​Stat |
   |       |       |       |       |       |       |       |       | ement |
   +-------+-------+-------+-------+-------+-------+-------+-------+-------+
   | (12   | SCO   | 1     | MC    |       |       |       |       | Not   |
   | 6000, | ORD3D |       |       |       |       |       |       | used  |
   | DCM,  |       |       |       |       |       |       |       | in    |
   | "Im   |       |       |       |       |       |       |       | AIM.  |
   | aging |       |       |       |       |       |       |       |       |
   | M     |       |       |       |       |       |       |       |       |
   | easur |       |       |       |       |       |       |       |       |
   | ement |       |       |       |       |       |       |       |       |
   | Rep   |       |       |       |       |       |       |       |       |
   | ort") |       |       |       |       |       |       |       |       |
   | >     |       |       |       |       |       |       |       |       |
   | (12   |       |       |       |       |       |       |       |       |
   | 6010, |       |       |       |       |       |       |       |       |
   | DCM,  |       |       |       |       |       |       |       |       |
   | "Im   |       |       |       |       |       |       |       |       |
   | aging |       |       |       |       |       |       |       |       |
   | Meas  |       |       |       |       |       |       |       |       |
   | ureme |       |       |       |       |       |       |       |       |
   | nts") |       |       |       |       |       |       |       |       |
   | >     |       |       |       |       |       |       |       |       |
   | (12   |       |       |       |       |       |       |       |       |
   | 5007, |       |       |       |       |       |       |       |       |
   | DCM,  |       |       |       |       |       |       |       |       |
   | "M    |       |       |       |       |       |       |       |       |
   | easur |       |       |       |       |       |       |       |       |
   | ement |       |       |       |       |       |       |       |       |
   | Gr    |       |       |       |       |       |       |       |       |
   | oup") |       |       |       |       |       |       |       |       |
   | >     |       |       |       |       |       |       |       |       |
   | (12   |       |       |       |       |       |       |       |       |
   | 1231, |       |       |       |       |       |       |       |       |
   | DCM,  |       |       |       |       |       |       |       |       |
   | "V    |       |       |       |       |       |       |       |       |
   | olume |       |       |       |       |       |       |       |       |
   | Surf  |       |       |       |       |       |       |       |       |
   | ace") |       |       |       |       |       |       |       |       |
   +-------+-------+-------+-------+-------+-------+-------+-------+-------+
   | (12   | IMAGE | 1-n   | MC    |       | I     |       |       |       |
   | 6000, |       |       |       |       | mage​ |       |       |       |
   | DCM,  |       |       |       |       | Annot |       |       |       |
   | "Im   |       |       |       |       | ation |       |       |       |
   | aging |       |       |       |       | ​​Col |       |       |       |
   | M     |       |       |       |       | lecti |       |       |       |
   | easur |       |       |       |       | on/​i |       |       |       |
   | ement |       |       |       |       | mage​ |       |       |       |
   | Rep   |       |       |       |       | Annot |       |       |       |
   | ort") |       |       |       |       | ation |       |       |       |
   | >     |       |       |       |       | s/​Im |       |       |       |
   | (12   |       |       |       |       | age​A |       |       |       |
   | 6010, |       |       |       |       | nnota |       |       |       |
   | DCM,  |       |       |       |       | tion/ |       |       |       |
   | "Im   |       |       |       |       | ​​seg |       |       |       |
   | aging |       |       |       |       | menta |       |       |       |
   | Meas  |       |       |       |       | tion​ |       |       |       |
   | ureme |       |       |       |       | Entit |       |       |       |
   | nts") |       |       |       |       | y​Col |       |       |       |
   | >     |       |       |       |       | lecti |       |       |       |
   | (12   |       |       |       |       | on/​S |       |       |       |
   | 5007, |       |       |       |       | egmen |       |       |       |
   | DCM,  |       |       |       |       | tatio |       |       |       |
   | "M    |       |       |       |       | nEnti |       |       |       |
   | easur |       |       |       |       | ty/​r |       |       |       |
   | ement |       |       |       |       | efere |       |       |       |
   | Gr    |       |       |       |       | ncedS |       |       |       |
   | oup") |       |       |       |       | opIns |       |       |       |
   | >     |       |       |       |       | tance |       |       |       |
   | (12   |       |       |       |       | Uid/​ |       |       |       |
   | 1233, |       |       |       |       | @root |       |       |       |
   | DCM,  |       |       |       |       |       |       |       |       |
   | "S    |       |       |       |       |       |       |       |       |
   | ource |       |       |       |       |       |       |       |       |
   | image |       |       |       |       |       |       |       |       |
   | for   |       |       |       |       |       |       |       |       |
   | segm  |       |       |       |       |       |       |       |       |
   | entat |       |       |       |       |       |       |       |       |
   | ion") |       |       |       |       |       |       |       |       |
   +-------+-------+-------+-------+-------+-------+-------+-------+-------+
   | (12   | U     | 1     | MC    |       |       |       |       | Not   |
   | 6000, | IDREF |       |       |       |       |       |       | used  |
   | DCM,  |       |       |       |       |       |       |       | in    |
   | "Im   |       |       |       |       |       |       |       | AIM   |
   | aging |       |       |       |       |       |       |       |       |
   | M     |       |       |       |       |       |       |       |       |
   | easur |       |       |       |       |       |       |       |       |
   | ement |       |       |       |       |       |       |       |       |
   | Rep   |       |       |       |       |       |       |       |       |
   | ort") |       |       |       |       |       |       |       |       |
   | >     |       |       |       |       |       |       |       |       |
   | (12   |       |       |       |       |       |       |       |       |
   | 6010, |       |       |       |       |       |       |       |       |
   | DCM,  |       |       |       |       |       |       |       |       |
   | "Im   |       |       |       |       |       |       |       |       |
   | aging |       |       |       |       |       |       |       |       |
   | Meas  |       |       |       |       |       |       |       |       |
   | ureme |       |       |       |       |       |       |       |       |
   | nts") |       |       |       |       |       |       |       |       |
   | >     |       |       |       |       |       |       |       |       |
   | (12   |       |       |       |       |       |       |       |       |
   | 5007, |       |       |       |       |       |       |       |       |
   | DCM,  |       |       |       |       |       |       |       |       |
   | "M    |       |       |       |       |       |       |       |       |
   | easur |       |       |       |       |       |       |       |       |
   | ement |       |       |       |       |       |       |       |       |
   | Gr    |       |       |       |       |       |       |       |       |
   | oup") |       |       |       |       |       |       |       |       |
   | >     |       |       |       |       |       |       |       |       |
   | (12   |       |       |       |       |       |       |       |       |
   | 1232, |       |       |       |       |       |       |       |       |
   | DCM,  |       |       |       |       |       |       |       |       |
   | "S    |       |       |       |       |       |       |       |       |
   | ource |       |       |       |       |       |       |       |       |
   | s     |       |       |       |       |       |       |       |       |
   | eries |       |       |       |       |       |       |       |       |
   | for   |       |       |       |       |       |       |       |       |
   | segm  |       |       |       |       |       |       |       |       |
   | entat |       |       |       |       |       |       |       |       |
   | ion") |       |       |       |       |       |       |       |       |
   +-------+-------+-------+-------+-------+-------+-------+-------+-------+
   | (12   | IMAGE | 1-n   | U     |       |       |       |       | Not   |
   | 6000, |       |       |       |       |       |       |       | used  |
   | DCM,  |       |       |       |       |       |       |       | in    |
   | "Im   |       |       |       |       |       |       |       | AIM.  |
   | aging |       |       |       |       |       |       |       |       |
   | M     |       |       |       |       |       |       |       |       |
   | easur |       |       |       |       |       |       |       |       |
   | ement |       |       |       |       |       |       |       |       |
   | Rep   |       |       |       |       |       |       |       |       |
   | ort") |       |       |       |       |       |       |       |       |
   | >     |       |       |       |       |       |       |       |       |
   | (12   |       |       |       |       |       |       |       |       |
   | 6010, |       |       |       |       |       |       |       |       |
   | DCM,  |       |       |       |       |       |       |       |       |
   | "Im   |       |       |       |       |       |       |       |       |
   | aging |       |       |       |       |       |       |       |       |
   | Meas  |       |       |       |       |       |       |       |       |
   | ureme |       |       |       |       |       |       |       |       |
   | nts") |       |       |       |       |       |       |       |       |
   | >     |       |       |       |       |       |       |       |       |
   | (12   |       |       |       |       |       |       |       |       |
   | 5007, |       |       |       |       |       |       |       |       |
   | DCM,  |       |       |       |       |       |       |       |       |
   | "M    |       |       |       |       |       |       |       |       |
   | easur |       |       |       |       |       |       |       |       |
   | ement |       |       |       |       |       |       |       |       |
   | Gr    |       |       |       |       |       |       |       |       |
   | oup") |       |       |       |       |       |       |       |       |
   | >     |       |       |       |       |       |       |       |       |
   | (12   |       |       |       |       |       |       |       |       |
   | 1200, |       |       |       |       |       |       |       |       |
   | DCM,  |       |       |       |       |       |       |       |       |
   | "Il   |       |       |       |       |       |       |       |       |
   | lustr |       |       |       |       |       |       |       |       |
   | ation |       |       |       |       |       |       |       |       |
   | of    |       |       |       |       |       |       |       |       |
   | ROI") |       |       |       |       |       |       |       |       |
   +-------+-------+-------+-------+-------+-------+-------+-------+-------+
   | (12   | COMP  | 1     | U     |       |       |       |       | Not   |
   | 6000, | OSITE |       |       |       |       |       |       | used  |
   | DCM,  |       |       |       |       |       |       |       | in    |
   | "Im   |       |       |       |       |       |       |       | AIM.  |
   | aging |       |       |       |       |       |       |       |       |
   | M     |       |       |       |       |       |       |       |       |
   | easur |       |       |       |       |       |       |       |       |
   | ement |       |       |       |       |       |       |       |       |
   | Rep   |       |       |       |       |       |       |       |       |
   | ort") |       |       |       |       |       |       |       |       |
   | >     |       |       |       |       |       |       |       |       |
   | (12   |       |       |       |       |       |       |       |       |
   | 6010, |       |       |       |       |       |       |       |       |
   | DCM,  |       |       |       |       |       |       |       |       |
   | "Im   |       |       |       |       |       |       |       |       |
   | aging |       |       |       |       |       |       |       |       |
   | Meas  |       |       |       |       |       |       |       |       |
   | ureme |       |       |       |       |       |       |       |       |
   | nts") |       |       |       |       |       |       |       |       |
   | >     |       |       |       |       |       |       |       |       |
   | (12   |       |       |       |       |       |       |       |       |
   | 5007, |       |       |       |       |       |       |       |       |
   | DCM,  |       |       |       |       |       |       |       |       |
   | "M    |       |       |       |       |       |       |       |       |
   | easur |       |       |       |       |       |       |       |       |
   | ement |       |       |       |       |       |       |       |       |
   | Gr    |       |       |       |       |       |       |       |       |
   | oup") |       |       |       |       |       |       |       |       |
   | >     |       |       |       |       |       |       |       |       |
   | (12   |       |       |       |       |       |       |       |       |
   | 6100, |       |       |       |       |       |       |       |       |
   | DCM,  |       |       |       |       |       |       |       |       |
   | "Real |       |       |       |       |       |       |       |       |
   | World |       |       |       |       |       |       |       |       |
   | Value |       |       |       |       |       |       |       |       |
   | Map   |       |       |       |       |       |       |       |       |
   | used  |       |       |       |       |       |       |       |       |
   | for   |       |       |       |       |       |       |       |       |
   | mea   |       |       |       |       |       |       |       |       |
   | surem |       |       |       |       |       |       |       |       |
   | ent") |       |       |       |       |       |       |       |       |
   +-------+-------+-------+-------+-------+-------+-------+-------+-------+
   | (12   | IN    | 1     | M     | `Ma   |       |       |       |       |
   | 6000, | CLUDE |       |       | pping |       |       |       |       |
   | DCM,  |       |       |       | of    |       |       |       |       |
   | "Im   |       |       |       | ROI   |       |       |       |       |
   | aging |       |       |       | Measu |       |       |       |       |
   | M     |       |       |       | remen |       |       |       |       |
   | easur |       |       |       | ts <# |       |       |       |       |
   | ement |       |       |       | sect_ |       |       |       |       |
   | Rep   |       |       |       | Mappi |       |       |       |       |
   | ort") |       |       |       | ng_TI |       |       |       |       |
   | >     |       |       |       | D_141 |       |       |       |       |
   | (12   |       |       |       | 9>`__ |       |       |       |       |
   | 6010, |       |       |       |       |       |       |       |       |
   | DCM,  |       |       |       |       |       |       |       |       |
   | "Im   |       |       |       |       |       |       |       |       |
   | aging |       |       |       |       |       |       |       |       |
   | Meas  |       |       |       |       |       |       |       |       |
   | ureme |       |       |       |       |       |       |       |       |
   | nts") |       |       |       |       |       |       |       |       |
   | >     |       |       |       |       |       |       |       |       |
   | (12   |       |       |       |       |       |       |       |       |
   | 5007, |       |       |       |       |       |       |       |       |
   | DCM,  |       |       |       |       |       |       |       |       |
   | "M    |       |       |       |       |       |       |       |       |
   | easur |       |       |       |       |       |       |       |       |
   | ement |       |       |       |       |       |       |       |       |
   | Gr    |       |       |       |       |       |       |       |       |
   | oup") |       |       |       |       |       |       |       |       |
   | >     |       |       |       |       |       |       |       |       |
   +-------+-------+-------+-------+-------+-------+-------+-------+-------+
   | (12   | CODE  | 1-n   | U     |       | Image | CD,   | 1,    |       |
   | 6000, |       |       |       |       | ​Anno | CD    | 0..1  |       |
   | DCM,  |       |       |       |       | tatio |       |       |       |
   | "Im   |       |       |       |       | n​​Co |       |       |       |
   | aging |       |       |       |       | llect |       |       |       |
   | M     |       |       |       |       | ion/​ |       |       |       |
   | easur |       |       |       |       | image |       |       |       |
   | ement |       |       |       |       | ​Anno |       |       |       |
   | Rep   |       |       |       |       | tatio |       |       |       |
   | ort") |       |       |       |       | ns/​I |       |       |       |
   | >     |       |       |       |       | mage​ |       |       |       |
   | (12   |       |       |       |       | Annot |       |       |       |
   | 6010, |       |       |       |       | ation |       |       |       |
   | DCM,  |       |       |       |       | /​ima |       |       |       |
   | "Im   |       |       |       |       | ging​ |       |       |       |
   | aging |       |       |       |       | Obser |       |       |       |
   | Meas  |       |       |       |       | vatio |       |       |       |
   | ureme |       |       |       |       | n​Ent |       |       |       |
   | nts") |       |       |       |       | ity​C |       |       |       |
   | >     |       |       |       |       | ollec |       |       |       |
   | (12   |       |       |       |       | tion/ |       |       |       |
   | 5007, |       |       |       |       | ​Imag |       |       |       |
   | DCM,  |       |       |       |       | ing​O |       |       |       |
   | "M    |       |       |       |       | bserv |       |       |       |
   | easur |       |       |       |       | ation |       |       |       |
   | ement |       |       |       |       | ​Enti |       |       |       |
   | Gr    |       |       |       |       | ty/​i |       |       |       |
   | oup") |       |       |       |       | magin |       |       |       |
   | >     |       |       |       |       | g​Obs |       |       |       |
   | $Qu   |       |       |       |       | ervat |       |       |       |
   | alita |       |       |       |       | ion​C |       |       |       |
   | tiveE |       |       |       |       | harac |       |       |       |
   | valua |       |       |       |       | teris |       |       |       |
   | tions |       |       |       |       | tic​C |       |       |       |
   |       |       |       |       |       | ollec |       |       |       |
   |       |       |       |       |       | tion/ |       |       |       |
   |       |       |       |       |       | ​Imag |       |       |       |
   |       |       |       |       |       | ing​O |       |       |       |
   |       |       |       |       |       | bserv |       |       |       |
   |       |       |       |       |       | ation |       |       |       |
   |       |       |       |       |       | ​Char |       |       |       |
   |       |       |       |       |       | acter |       |       |       |
   |       |       |       |       |       | istic |       |       |       |
   |       |       |       |       |       | ​/​qu |       |       |       |
   |       |       |       |       |       | estio |       |       |       |
   |       |       |       |       |       | nType |       |       |       |
   |       |       |       |       |       | ​Code |       |       |       |
   |       |       |       |       |       | ,type |       |       |       |
   |       |       |       |       |       | ​Code |       |       |       |
   +-------+-------+-------+-------+-------+-------+-------+-------+-------+
   | (12   | TEXT  | 1-n   | U     |       | Im    |       |       | The   |
   | 6000, |       |       |       |       | age​A |       |       | para  |
   | DCM,  |       |       |       |       | nnota |       |       | meter |
   | "Im   |       |       |       |       | tion​ |       |       | $Qua  |
   | aging |       |       |       |       | ​Coll |       |       | litat |
   | M     |       |       |       |       | ectio |       |       | ive​E |
   | easur |       |       |       |       | n/​im |       |       | valua |
   | ement |       |       |       |       | age​A |       |       | tions |
   | Rep   |       |       |       |       | nnota |       |       | is    |
   | ort") |       |       |       |       | tions |       |       | not   |
   | >     |       |       |       |       | /​Ima |       |       | used  |
   | (12   |       |       |       |       | ge​An |       |       | in    |
   | 6010, |       |       |       |       | notat |       |       | AIM,  |
   | DCM,  |       |       |       |       | ion/​ |       |       | but   |
   | "Im   |       |       |       |       | comme |       |       | this  |
   | aging |       |       |       |       | nt/​@ |       |       | TEXT  |
   | Meas  |       |       |       |       | value |       |       | co    |
   | ureme |       |       |       |       |       |       |       | ntent |
   | nts") |       |       |       |       |       |       |       | item  |
   | >     |       |       |       |       |       |       |       | is    |
   | (12   |       |       |       |       |       |       |       | used  |
   | 5007, |       |       |       |       |       |       |       | to    |
   | DCM,  |       |       |       |       |       |       |       | map   |
   | "M    |       |       |       |       |       |       |       | the   |
   | easur |       |       |       |       |       |       |       | AIM   |
   | ement |       |       |       |       |       |       |       | co    |
   | Gr    |       |       |       |       |       |       |       | mment |
   | oup") |       |       |       |       |       |       |       | as if |
   | >     |       |       |       |       |       |       |       | it    |
   | (12   |       |       |       |       |       |       |       | were  |
   | 1106, |       |       |       |       |       |       |       | a     |
   | DCM,  |       |       |       |       |       |       |       | Q     |
   | "Comm |       |       |       |       |       |       |       | ualit |
   | ent") |       |       |       |       |       |       |       | ative |
   |       |       |       |       |       |       |       |       | E     |
   |       |       |       |       |       |       |       |       | valua |
   |       |       |       |       |       |       |       |       | tion. |
   +-------+-------+-------+-------+-------+-------+-------+-------+-------+

.. _sect_Mapping_TID_1419:

Mapping of ROI Measurements
'''''''''''''''''''''''''''

This section describes the mapping of .

.. table:: Mapping of ROI Measurements

   +-------+-------+-------+-------+-------+-------+-------+-------+-------+
   | DICOM | DICOM | DICOM | DICOM | Gene  | AIM   | AIM   | AIM   | Co    |
   | SR    | VT    | VM    | Usage | rated | El    | Data  | Mu    | mment |
   | Path  |       |       | Type  | Value | ement | Type  | ltipl |       |
   |       |       |       |       |       | or    |       | icity |       |
   |       |       |       |       |       | Attr  |       |       |       |
   |       |       |       |       |       | ibute |       |       |       |
   +=======+=======+=======+=======+=======+=======+=======+=======+=======+
   | (12   | CODE  | 1     | U     |       |       |       |       | Not   |
   | 6000, |       |       |       |       |       |       |       | en    |
   | DCM,  |       |       |       |       |       |       |       | coded |
   | "Im   |       |       |       |       |       |       |       | in    |
   | aging |       |       |       |       |       |       |       | AIM   |
   | M     |       |       |       |       |       |       |       | at    |
   | easur |       |       |       |       |       |       |       | this  |
   | ement |       |       |       |       |       |       |       | l     |
   | Rep   |       |       |       |       |       |       |       | evel. |
   | ort") |       |       |       |       |       |       |       |       |
   | >     |       |       |       |       |       |       |       |       |
   | (12   |       |       |       |       |       |       |       |       |
   | 6010, |       |       |       |       |       |       |       |       |
   | DCM,  |       |       |       |       |       |       |       |       |
   | "Im   |       |       |       |       |       |       |       |       |
   | aging |       |       |       |       |       |       |       |       |
   | Meas  |       |       |       |       |       |       |       |       |
   | ureme |       |       |       |       |       |       |       |       |
   | nts") |       |       |       |       |       |       |       |       |
   | >     |       |       |       |       |       |       |       |       |
   | (12   |       |       |       |       |       |       |       |       |
   | 5007, |       |       |       |       |       |       |       |       |
   | DCM,  |       |       |       |       |       |       |       |       |
   | "M    |       |       |       |       |       |       |       |       |
   | easur |       |       |       |       |       |       |       |       |
   | ement |       |       |       |       |       |       |       |       |
   | Gr    |       |       |       |       |       |       |       |       |
   | oup") |       |       |       |       |       |       |       |       |
   | >     |       |       |       |       |       |       |       |       |
   | `(    |       |       |       |       |       |       |       |       |
   | 37012 |       |       |       |       |       |       |       |       |
   | 9005, |       |       |       |       |       |       |       |       |
   | SCT,  |       |       |       |       |       |       |       |       |
   | "M    |       |       |       |       |       |       |       |       |
   | easur |       |       |       |       |       |       |       |       |
   | ement |       |       |       |       |       |       |       |       |
   | Metho |       |       |       |       |       |       |       |       |
   | d") < |       |       |       |       |       |       |       |       |
   | http: |       |       |       |       |       |       |       |       |
   | //sno |       |       |       |       |       |       |       |       |
   | med.i |       |       |       |       |       |       |       |       |
   | nfo/i |       |       |       |       |       |       |       |       |
   | d/370 |       |       |       |       |       |       |       |       |
   | 12900 |       |       |       |       |       |       |       |       |
   | 5>`__ |       |       |       |       |       |       |       |       |
   +-------+-------+-------+-------+-------+-------+-------+-------+-------+
   | (12   | CODE  | 1-n   | U     |       | Imag  | CD    | 1..n  | The   |
   | 6000, |       |       |       |       | e​Ann |       |       | fi    |
   | DCM,  |       |       |       |       | otati |       |       | nding |
   | "Im   |       |       |       |       | on​​C |       |       | site  |
   | aging |       |       |       |       | ollec |       |       | is    |
   | M     |       |       |       |       | tion/ |       |       | fac   |
   | easur |       |       |       |       | ​imag |       |       | tored |
   | ement |       |       |       |       | e​Ann |       |       | out   |
   | Rep   |       |       |       |       | otati |       |       | since |
   | ort") |       |       |       |       | ons/​ |       |       | it is |
   | >     |       |       |       |       | Image |       |       | c     |
   | (12   |       |       |       |       | ​Anno |       |       | ommon |
   | 6010, |       |       |       |       | tatio |       |       | to    |
   | DCM,  |       |       |       |       | n/​im |       |       | all   |
   | "Im   |       |       |       |       | aging |       |       | me    |
   | aging |       |       |       |       | Physi |       |       | asure |
   | Meas  |       |       |       |       | cal​E |       |       | ments |
   | ureme |       |       |       |       | ntity |       |       | in    |
   | nts") |       |       |       |       | ​Coll |       |       | this  |
   | >     |       |       |       |       | ectio |       |       | g     |
   | (12   |       |       |       |       | n/​Im |       |       | roup. |
   | 5007, |       |       |       |       | aging |       |       |       |
   | DCM,  |       |       |       |       | Physi |       |       | If a  |
   | "M    |       |       |       |       | calEn |       |       | p     |
   | easur |       |       |       |       | tity​ |       |       | aired |
   | ement |       |       |       |       | [labe |       |       | stru  |
   | Gr    |       |       |       |       | l/​@v |       |       | cture |
   | oup") |       |       |       |       | alue= |       |       | in    |
   | >     |       |       |       |       | 'Loca |       |       | AIM,  |
   | `(    |       |       |       |       | tion' |       |       | this  |
   | 36369 |       |       |       |       | or    |       |       | entry |
   | 8007, |       |       |       |       | label |       |       | will  |
   | SCT,  |       |       |       |       | /​@va |       |       | pre-  |
   | "Fi   |       |       |       |       | lue=' |       |       | coord |
   | nding |       |       |       |       | Lobar |       |       | inate |
   | Sit   |       |       |       |       | Loca  |       |       | the   |
   | e") < |       |       |       |       | tion' |       |       | later |
   | http: |       |       |       |       | or    |       |       | ality |
   | //sno |       |       |       |       | labe  |       |       | with  |
   | med.i |       |       |       |       | l/​@v |       |       | the   |
   | nfo/i |       |       |       |       | alue= |       |       | site. |
   | d/363 |       |       |       |       | 'Segm |       |       |       |
   | 69800 |       |       |       |       | ental |       |       |       |
   | 7>`__ |       |       |       |       | Loca  |       |       |       |
   |       |       |       |       |       | tion' |       |       |       |
   |       |       |       |       |       | or    |       |       |       |
   |       |       |       |       |       | label |       |       |       |
   |       |       |       |       |       | /​@va |       |       |       |
   |       |       |       |       |       | lue=' |       |       |       |
   |       |       |       |       |       | Organ |       |       |       |
   |       |       |       |       |       | Type' |       |       |       |
   |       |       |       |       |       | ]/typ |       |       |       |
   |       |       |       |       |       | eCode |       |       |       |
   +-------+-------+-------+-------+-------+-------+-------+-------+-------+
   | (12   | CODE  | 1     | U     |       |       |       |       | Not   |
   | 6000, |       |       |       |       |       |       |       | used  |
   | DCM,  |       |       |       |       |       |       |       | since |
   | "Im   |       |       |       |       |       |       |       | AIM   |
   | aging |       |       |       |       |       |       |       | does  |
   | M     |       |       |       |       |       |       |       | not   |
   | easur |       |       |       |       |       |       |       | have  |
   | ement |       |       |       |       |       |       |       | a     |
   | Rep   |       |       |       |       |       |       |       | mech  |
   | ort") |       |       |       |       |       |       |       | anism |
   | >     |       |       |       |       |       |       |       | for   |
   | (12   |       |       |       |       |       |       |       | po    |
   | 6010, |       |       |       |       |       |       |       | st-co |
   | DCM,  |       |       |       |       |       |       |       | ordin |
   | "Im   |       |       |       |       |       |       |       | ating |
   | aging |       |       |       |       |       |       |       | the   |
   | Meas  |       |       |       |       |       |       |       | loca  |
   | ureme |       |       |       |       |       |       |       | tion. |
   | nts") |       |       |       |       |       |       |       |       |
   | >     |       |       |       |       |       |       |       |       |
   | (12   |       |       |       |       |       |       |       |       |
   | 5007, |       |       |       |       |       |       |       |       |
   | DCM,  |       |       |       |       |       |       |       |       |
   | "M    |       |       |       |       |       |       |       |       |
   | easur |       |       |       |       |       |       |       |       |
   | ement |       |       |       |       |       |       |       |       |
   | Gr    |       |       |       |       |       |       |       |       |
   | oup") |       |       |       |       |       |       |       |       |
   | >     |       |       |       |       |       |       |       |       |
   | `(    |       |       |       |       |       |       |       |       |
   | 36369 |       |       |       |       |       |       |       |       |
   | 8007, |       |       |       |       |       |       |       |       |
   | SCT,  |       |       |       |       |       |       |       |       |
   | "Fi   |       |       |       |       |       |       |       |       |
   | nding |       |       |       |       |       |       |       |       |
   | Sit   |       |       |       |       |       |       |       |       |
   | e") < |       |       |       |       |       |       |       |       |
   | http: |       |       |       |       |       |       |       |       |
   | //sno |       |       |       |       |       |       |       |       |
   | med.i |       |       |       |       |       |       |       |       |
   | nfo/i |       |       |       |       |       |       |       |       |
   | d/363 |       |       |       |       |       |       |       |       |
   | 69800 |       |       |       |       |       |       |       |       |
   | 7>`__ |       |       |       |       |       |       |       |       |
   | >     |       |       |       |       |       |       |       |       |
   | `(    |       |       |       |       |       |       |       |       |
   | 27274 |       |       |       |       |       |       |       |       |
   | 1003, |       |       |       |       |       |       |       |       |
   | SCT,  |       |       |       |       |       |       |       |       |
   | "Late |       |       |       |       |       |       |       |       |
   | ralit |       |       |       |       |       |       |       |       |
   | y") < |       |       |       |       |       |       |       |       |
   | http: |       |       |       |       |       |       |       |       |
   | //sno |       |       |       |       |       |       |       |       |
   | med.i |       |       |       |       |       |       |       |       |
   | nfo/i |       |       |       |       |       |       |       |       |
   | d/272 |       |       |       |       |       |       |       |       |
   | 74100 |       |       |       |       |       |       |       |       |
   | 3>`__ |       |       |       |       |       |       |       |       |
   +-------+-------+-------+-------+-------+-------+-------+-------+-------+
   | (12   | CODE  | 1     | U     |       |       |       |       | Not   |
   | 6000, |       |       |       |       |       |       |       | used  |
   | DCM,  |       |       |       |       |       |       |       | since |
   | "Im   |       |       |       |       |       |       |       | AIM   |
   | aging |       |       |       |       |       |       |       | does  |
   | M     |       |       |       |       |       |       |       | not   |
   | easur |       |       |       |       |       |       |       | have  |
   | ement |       |       |       |       |       |       |       | a     |
   | Rep   |       |       |       |       |       |       |       | mech  |
   | ort") |       |       |       |       |       |       |       | anism |
   | >     |       |       |       |       |       |       |       | for   |
   | (12   |       |       |       |       |       |       |       | po    |
   | 6010, |       |       |       |       |       |       |       | st-co |
   | DCM,  |       |       |       |       |       |       |       | ordin |
   | "Im   |       |       |       |       |       |       |       | ating |
   | aging |       |       |       |       |       |       |       | the   |
   | Meas  |       |       |       |       |       |       |       | loca  |
   | ureme |       |       |       |       |       |       |       | tion. |
   | nts") |       |       |       |       |       |       |       |       |
   | >     |       |       |       |       |       |       |       |       |
   | (12   |       |       |       |       |       |       |       |       |
   | 5007, |       |       |       |       |       |       |       |       |
   | DCM,  |       |       |       |       |       |       |       |       |
   | "M    |       |       |       |       |       |       |       |       |
   | easur |       |       |       |       |       |       |       |       |
   | ement |       |       |       |       |       |       |       |       |
   | Gr    |       |       |       |       |       |       |       |       |
   | oup") |       |       |       |       |       |       |       |       |
   | >     |       |       |       |       |       |       |       |       |
   | `(    |       |       |       |       |       |       |       |       |
   | 36369 |       |       |       |       |       |       |       |       |
   | 8007, |       |       |       |       |       |       |       |       |
   | SCT,  |       |       |       |       |       |       |       |       |
   | "Fi   |       |       |       |       |       |       |       |       |
   | nding |       |       |       |       |       |       |       |       |
   | Sit   |       |       |       |       |       |       |       |       |
   | e") < |       |       |       |       |       |       |       |       |
   | http: |       |       |       |       |       |       |       |       |
   | //sno |       |       |       |       |       |       |       |       |
   | med.i |       |       |       |       |       |       |       |       |
   | nfo/i |       |       |       |       |       |       |       |       |
   | d/363 |       |       |       |       |       |       |       |       |
   | 69800 |       |       |       |       |       |       |       |       |
   | 7>`__ |       |       |       |       |       |       |       |       |
   | >     |       |       |       |       |       |       |       |       |
   | `(    |       |       |       |       |       |       |       |       |
   | 10623 |       |       |       |       |       |       |       |       |
   | 3006, |       |       |       |       |       |       |       |       |
   | SCT,  |       |       |       |       |       |       |       |       |
   | "Top  |       |       |       |       |       |       |       |       |
   | ograp |       |       |       |       |       |       |       |       |
   | hical |       |       |       |       |       |       |       |       |
   | mo    |       |       |       |       |       |       |       |       |
   | difie |       |       |       |       |       |       |       |       |
   | r") < |       |       |       |       |       |       |       |       |
   | http: |       |       |       |       |       |       |       |       |
   | //sno |       |       |       |       |       |       |       |       |
   | med.i |       |       |       |       |       |       |       |       |
   | nfo/i |       |       |       |       |       |       |       |       |
   | d/106 |       |       |       |       |       |       |       |       |
   | 23300 |       |       |       |       |       |       |       |       |
   | 6>`__ |       |       |       |       |       |       |       |       |
   +-------+-------+-------+-------+-------+-------+-------+-------+-------+
   | (12   | NUM   | 1-n   | M     |       | NAME  | CD,   | 1..n, | The   |
   | 6000, |       |       |       |       | =     | ST,   | 0..n, | first |
   | DCM,  |       |       |       |       | Ima   | CD    | 1     | typ   |
   | "Im   |       |       |       |       | ge​An |       |       | eCode |
   | aging |       |       |       |       | notat |       |       | entry |
   | M     |       |       |       |       | ion​​ |       |       | is    |
   | easur |       |       |       |       | Colle |       |       | as    |
   | ement |       |       |       |       | ction |       |       | sumed |
   | Rep   |       |       |       |       | /​ima |       |       | to be |
   | ort") |       |       |       |       | ge​An |       |       | the   |
   | >     |       |       |       |       | notat |       |       | pr    |
   | (12   |       |       |       |       | ions/ |       |       | imary |
   | 6010, |       |       |       |       | ​Imag |       |       | con   |
   | DCM,  |       |       |       |       | e​Ann |       |       | cept. |
   | "Im   |       |       |       |       | otati |       |       | Other |
   | aging |       |       |       |       | on/​c |       |       | typ   |
   | Meas  |       |       |       |       | alcul |       |       | eCode |
   | ureme |       |       |       |       | ation |       |       | en    |
   | nts") |       |       |       |       | ​Enti |       |       | tries |
   | >     |       |       |       |       | ty​Co |       |       | may   |
   | (12   |       |       |       |       | llect |       |       | be    |
   | 5007, |       |       |       |       | ion/​ |       |       | consi |
   | DCM,  |       |       |       |       | Calcu |       |       | dered |
   | "M    |       |       |       |       | latio |       |       | as    |
   | easur |       |       |       |       | nEnti |       |       | modif |
   | ement |       |       |       |       | ty/​t |       |       | iers. |
   | Gr    |       |       |       |       | ypeCo |       |       |       |
   | oup") |       |       |       |       | de[1] |       |       | Value |
   | >     |       |       |       |       |       |       |       | may   |
   | $M    |       |       |       |       | VALUE |       |       | be    |
   | easur |       |       |       |       | =     |       |       | found |
   | ement |       |       |       |       | Imag  |       |       | in    |
   |       |       |       |       |       | e​Ann |       |       | e     |
   |       |       |       |       |       | otati |       |       | ither |
   |       |       |       |       |       | on​​C |       |       | C     |
   |       |       |       |       |       | ollec |       |       | ompac |
   |       |       |       |       |       | tion/ |       |       | t​Cal |
   |       |       |       |       |       | ​imag |       |       | culat |
   |       |       |       |       |       | e​Ann |       |       | ion​R |
   |       |       |       |       |       | otati |       |       | esult |
   |       |       |       |       |       | ons/​ |       |       | (     |
   |       |       |       |       |       | Image |       |       | i.e., |
   |       |       |       |       |       | ​Anno |       |       | value |
   |       |       |       |       |       | tatio |       |       | child |
   |       |       |       |       |       | n/​ca |       |       | of    |
   |       |       |       |       |       | lcula |       |       | Cal   |
   |       |       |       |       |       | tion​ |       |       | culat |
   |       |       |       |       |       | Entit |       |       | ionRe |
   |       |       |       |       |       | y​Col |       |       | sult) |
   |       |       |       |       |       | lecti |       |       | or    |
   |       |       |       |       |       | on/​C |       |       | first |
   |       |       |       |       |       | alcul |       |       | value |
   |       |       |       |       |       | ation |       |       | of    |
   |       |       |       |       |       | Entit |       |       | Ex    |
   |       |       |       |       |       | y/​ca |       |       | tende |
   |       |       |       |       |       | lcula |       |       | d​Cal |
   |       |       |       |       |       | tionR |       |       | culat |
   |       |       |       |       |       | esult |       |       | ion​R |
   |       |       |       |       |       | ​Coll |       |       | esult |
   |       |       |       |       |       | ectio |       |       | (     |
   |       |       |       |       |       | n/​Ca |       |       | i.e., |
   |       |       |       |       |       | lcula |       |       | n     |
   |       |       |       |       |       | tionR |       |       | ested |
   |       |       |       |       |       | esult |       |       | w     |
   |       |       |       |       |       | /​​@v |       |       | ithin |
   |       |       |       |       |       | alue, |       |       | c     |
   |       |       |       |       |       | c     |       |       | alcul |
   |       |       |       |       |       | alcul |       |       | ation |
   |       |       |       |       |       | ation |       |       | ​Resu |
   |       |       |       |       |       | Data​ |       |       | lt​Co |
   |       |       |       |       |       | Colle |       |       | llect |
   |       |       |       |       |       | ction |       |       | ion). |
   |       |       |       |       |       | /​Cal |       |       |       |
   |       |       |       |       |       | culat |       |       | Only  |
   |       |       |       |       |       | ionDa |       |       | ma    |
   |       |       |       |       |       | ta/​@ |       |       | pping |
   |       |       |       |       |       | value |       |       | of a  |
   |       |       |       |       |       |       |       |       | s     |
   |       |       |       |       |       | UNITS |       |       | ingle |
   |       |       |       |       |       | =     |       |       | value |
   |       |       |       |       |       | Imag  |       |       | from  |
   |       |       |       |       |       | e​Ann |       |       | Ex    |
   |       |       |       |       |       | otati |       |       | tende |
   |       |       |       |       |       | on​​C |       |       | d​Cal |
   |       |       |       |       |       | ollec |       |       | culat |
   |       |       |       |       |       | tion/ |       |       | ion​R |
   |       |       |       |       |       | ​imag |       |       | esult |
   |       |       |       |       |       | e​Ann |       |       | is    |
   |       |       |       |       |       | otati |       |       | suppo |
   |       |       |       |       |       | ons/​ |       |       | rted. |
   |       |       |       |       |       | Image |       |       |       |
   |       |       |       |       |       | ​Anno |       |       | If no |
   |       |       |       |       |       | tatio |       |       | m     |
   |       |       |       |       |       | n/​ca |       |       | easur |
   |       |       |       |       |       | lcula |       |       | ement |
   |       |       |       |       |       | tion​ |       |       | is    |
   |       |       |       |       |       | Entit |       |       | pr    |
   |       |       |       |       |       | y​Col |       |       | esent |
   |       |       |       |       |       | lecti |       |       | in    |
   |       |       |       |       |       | on/​C |       |       | AIM   |
   |       |       |       |       |       | alcul |       |       | (     |
   |       |       |       |       |       | ation |       |       | 0..n) |
   |       |       |       |       |       | Entit |       |       | then  |
   |       |       |       |       |       | y/​ca |       |       | do    |
   |       |       |       |       |       | lcula |       |       | not   |
   |       |       |       |       |       | tionR |       |       | in    |
   |       |       |       |       |       | esult |       |       | clude |
   |       |       |       |       |       | ​Coll |       |       | the   |
   |       |       |       |       |       | ectio |       |       | tem   |
   |       |       |       |       |       | n/​Ca |       |       | plate |
   |       |       |       |       |       | lcula |       |       | in    |
   |       |       |       |       |       | tionR |       |       | the   |
   |       |       |       |       |       | esult |       |       | first |
   |       |       |       |       |       | /​uni |       |       | p     |
   |       |       |       |       |       | tOfMe |       |       | lace. |
   |       |       |       |       |       | asure |       |       |       |
   |       |       |       |       |       |       |       |       | The   |
   |       |       |       |       |       |       |       |       | value |
   |       |       |       |       |       |       |       |       | of    |
   |       |       |       |       |       |       |       |       | ai    |
   |       |       |       |       |       |       |       |       | m:uni |
   |       |       |       |       |       |       |       |       | que​I |
   |       |       |       |       |       |       |       |       | denti |
   |       |       |       |       |       |       |       |       | fier/ |
   |       |       |       |       |       |       |       |       | @root |
   |       |       |       |       |       |       |       |       | is    |
   |       |       |       |       |       |       |       |       | m     |
   |       |       |       |       |       |       |       |       | apped |
   |       |       |       |       |       |       |       |       | to    |
   |       |       |       |       |       |       |       |       | the   |
   |       |       |       |       |       |       |       |       | Obser |
   |       |       |       |       |       |       |       |       | vatio |
   |       |       |       |       |       |       |       |       | n​UID |
   |       |       |       |       |       |       |       |       | Attr  |
   |       |       |       |       |       |       |       |       | ibute |
   |       |       |       |       |       |       |       |       | of    |
   |       |       |       |       |       |       |       |       | the   |
   |       |       |       |       |       |       |       |       | NUM   |
   |       |       |       |       |       |       |       |       | Co    |
   |       |       |       |       |       |       |       |       | ntent |
   |       |       |       |       |       |       |       |       | Item. |
   +-------+-------+-------+-------+-------+-------+-------+-------+-------+
   | (12   | CODE  | 1-n   | U     |       | Im    | CD    | 1..n  | The   |
   | 6000, |       |       |       |       | age​A |       |       | first |
   | DCM,  |       |       |       |       | nnota |       |       | typ   |
   | "Im   |       |       |       |       | tion​ |       |       | eCode |
   | aging |       |       |       |       | ​Coll |       |       | entry |
   | M     |       |       |       |       | ectio |       |       | is    |
   | easur |       |       |       |       | n/​im |       |       | as    |
   | ement |       |       |       |       | age​A |       |       | sumed |
   | Rep   |       |       |       |       | nnota |       |       | to be |
   | ort") |       |       |       |       | tions |       |       | the   |
   | >     |       |       |       |       | /​Ima |       |       | pr    |
   | (12   |       |       |       |       | ge​An |       |       | imary |
   | 6010, |       |       |       |       | notat |       |       | con   |
   | DCM,  |       |       |       |       | ion/​ |       |       | cept. |
   | "Im   |       |       |       |       | calcu |       |       | This  |
   | aging |       |       |       |       | latio |       |       | row   |
   | Meas  |       |       |       |       | n​Ent |       |       | can   |
   | ureme |       |       |       |       | ity​C |       |       | be    |
   | nts") |       |       |       |       | ollec |       |       | used  |
   | >     |       |       |       |       | tion/ |       |       | if    |
   | (12   |       |       |       |       | ​Calc |       |       | succe |
   | 5007, |       |       |       |       | ulati |       |       | ssive |
   | DCM,  |       |       |       |       | onEnt |       |       | typ   |
   | "M    |       |       |       |       | ity/​ |       |       | eCode |
   | easur |       |       |       |       | typeC |       |       | en    |
   | ement |       |       |       |       | ode​[ |       |       | tries |
   | Gr    |       |       |       |       | posit |       |       | are   |
   | oup") |       |       |       |       | ion() |       |       | r     |
   | >     |       |       |       |       | != 1] |       |       | ecogn |
   | $M    |       |       |       |       |       |       |       | ized, |
   | easur |       |       |       |       |       |       |       | and   |
   | ement |       |       |       |       |       |       |       | not a |
   | >     |       |       |       |       |       |       |       | m     |
   | $Mo   |       |       |       |       |       |       |       | ethod |
   | dType |       |       |       |       |       |       |       | or    |
   |       |       |       |       |       |       |       |       | d     |
   |       |       |       |       |       |       |       |       | eriva |
   |       |       |       |       |       |       |       |       | tion, |
   |       |       |       |       |       |       |       |       | and a |
   |       |       |       |       |       |       |       |       | name- |
   |       |       |       |       |       |       |       |       | value |
   |       |       |       |       |       |       |       |       | pair  |
   |       |       |       |       |       |       |       |       | can   |
   |       |       |       |       |       |       |       |       | be    |
   |       |       |       |       |       |       |       |       | c     |
   |       |       |       |       |       |       |       |       | onstr |
   |       |       |       |       |       |       |       |       | ucted |
   |       |       |       |       |       |       |       |       | from  |
   |       |       |       |       |       |       |       |       | the   |
   |       |       |       |       |       |       |       |       | typ   |
   |       |       |       |       |       |       |       |       | eCode |
   |       |       |       |       |       |       |       |       | entry |
   |       |       |       |       |       |       |       |       | (     |
   |       |       |       |       |       |       |       |       | which |
   |       |       |       |       |       |       |       |       | is a  |
   |       |       |       |       |       |       |       |       | s     |
   |       |       |       |       |       |       |       |       | ingle |
   |       |       |       |       |       |       |       |       | c     |
   |       |       |       |       |       |       |       |       | ode). |
   +-------+-------+-------+-------+-------+-------+-------+-------+-------+
   | (12   | CODE  | 1     | U     |       | Im    | CD    | 1..n  | The   |
   | 6000, |       |       |       |       | age​A |       |       | first |
   | DCM,  |       |       |       |       | nnota |       |       | typ   |
   | "Im   |       |       |       |       | tion​ |       |       | eCode |
   | aging |       |       |       |       | ​Coll |       |       | entry |
   | M     |       |       |       |       | ectio |       |       | is    |
   | easur |       |       |       |       | n/​im |       |       | as    |
   | ement |       |       |       |       | age​A |       |       | sumed |
   | Rep   |       |       |       |       | nnota |       |       | to be |
   | ort") |       |       |       |       | tions |       |       | the   |
   | >     |       |       |       |       | /​Ima |       |       | pr    |
   | (12   |       |       |       |       | ge​An |       |       | imary |
   | 6010, |       |       |       |       | notat |       |       | con   |
   | DCM,  |       |       |       |       | ion/​ |       |       | cept. |
   | "Im   |       |       |       |       | calcu |       |       | Other |
   | aging |       |       |       |       | latio |       |       | typ   |
   | Meas  |       |       |       |       | n​Ent |       |       | eCode |
   | ureme |       |       |       |       | ity​C |       |       | en    |
   | nts") |       |       |       |       | ollec |       |       | tries |
   | >     |       |       |       |       | tion/ |       |       | may   |
   | (12   |       |       |       |       | ​Calc |       |       | be    |
   | 5007, |       |       |       |       | ulati |       |       | consi |
   | DCM,  |       |       |       |       | onEnt |       |       | dered |
   | "M    |       |       |       |       | ity/​ |       |       | as    |
   | easur |       |       |       |       | typeC |       |       | modif |
   | ement |       |       |       |       | ode​[ |       |       | iers, |
   | Gr    |       |       |       |       | posit |       |       | but   |
   | oup") |       |       |       |       | ion() |       |       | there |
   | >     |       |       |       |       | != 1] |       |       | is no |
   | $M    |       |       |       |       |       |       |       | sta   |
   | easur |       |       |       |       |       |       |       | ndard |
   | ement |       |       |       |       |       |       |       | o     |
   | >     |       |       |       |       |       |       |       | rder, |
   | `(    |       |       |       |       |       |       |       | so    |
   | 37012 |       |       |       |       |       |       |       | r     |
   | 9005, |       |       |       |       |       |       |       | ecogn |
   | SCT,  |       |       |       |       |       |       |       | ition |
   | "M    |       |       |       |       |       |       |       | as a  |
   | easur |       |       |       |       |       |       |       | "me   |
   | ement |       |       |       |       |       |       |       | thod" |
   | Metho |       |       |       |       |       |       |       | de    |
   | d") < |       |       |       |       |       |       |       | pends |
   | http: |       |       |       |       |       |       |       | on    |
   | //sno |       |       |       |       |       |       |       | r     |
   | med.i |       |       |       |       |       |       |       | ecogn |
   | nfo/i |       |       |       |       |       |       |       | ition |
   | d/370 |       |       |       |       |       |       |       | of    |
   | 12900 |       |       |       |       |       |       |       | spe   |
   | 5>`__ |       |       |       |       |       |       |       | cific |
   |       |       |       |       |       |       |       |       | c     |
   |       |       |       |       |       |       |       |       | odes. |
   +-------+-------+-------+-------+-------+-------+-------+-------+-------+
   | (12   | CODE  | 1     | U     |       | Im    | CD    | 1..n  | The   |
   | 6000, |       |       |       |       | age​A |       |       | first |
   | DCM,  |       |       |       |       | nnota |       |       | typ   |
   | "Im   |       |       |       |       | tion​ |       |       | eCode |
   | aging |       |       |       |       | ​Coll |       |       | entry |
   | M     |       |       |       |       | ectio |       |       | is    |
   | easur |       |       |       |       | n/​im |       |       | as    |
   | ement |       |       |       |       | age​A |       |       | sumed |
   | Rep   |       |       |       |       | nnota |       |       | to be |
   | ort") |       |       |       |       | tions |       |       | the   |
   | >     |       |       |       |       | /​Ima |       |       | pr    |
   | (12   |       |       |       |       | ge​An |       |       | imary |
   | 6010, |       |       |       |       | notat |       |       | con   |
   | DCM,  |       |       |       |       | ion/​ |       |       | cept. |
   | "Im   |       |       |       |       | calcu |       |       | Other |
   | aging |       |       |       |       | latio |       |       | typ   |
   | Meas  |       |       |       |       | n​Ent |       |       | eCode |
   | ureme |       |       |       |       | ity​C |       |       | en    |
   | nts") |       |       |       |       | ollec |       |       | tries |
   | >     |       |       |       |       | tion/ |       |       | may   |
   | (12   |       |       |       |       | ​Calc |       |       | be    |
   | 5007, |       |       |       |       | ulati |       |       | consi |
   | DCM,  |       |       |       |       | onEnt |       |       | dered |
   | "M    |       |       |       |       | ity/​ |       |       | as    |
   | easur |       |       |       |       | typeC |       |       | modif |
   | ement |       |       |       |       | ode​[ |       |       | iers, |
   | Gr    |       |       |       |       | posit |       |       | but   |
   | oup") |       |       |       |       | ion() |       |       | there |
   | >     |       |       |       |       | != 1] |       |       | is no |
   | $M    |       |       |       |       |       |       |       | sta   |
   | easur |       |       |       |       |       |       |       | ndard |
   | ement |       |       |       |       |       |       |       | o     |
   | >     |       |       |       |       |       |       |       | rder, |
   | (12   |       |       |       |       |       |       |       | so    |
   | 1401, |       |       |       |       |       |       |       | r     |
   | DCM,  |       |       |       |       |       |       |       | ecogn |
   | "De   |       |       |       |       |       |       |       | ition |
   | rivat |       |       |       |       |       |       |       | as a  |
   | ion") |       |       |       |       |       |       |       | "d    |
   |       |       |       |       |       |       |       |       | eriva |
   |       |       |       |       |       |       |       |       | tion" |
   |       |       |       |       |       |       |       |       | de    |
   |       |       |       |       |       |       |       |       | pends |
   |       |       |       |       |       |       |       |       | on    |
   |       |       |       |       |       |       |       |       | r     |
   |       |       |       |       |       |       |       |       | ecogn |
   |       |       |       |       |       |       |       |       | ition |
   |       |       |       |       |       |       |       |       | of    |
   |       |       |       |       |       |       |       |       | spe   |
   |       |       |       |       |       |       |       |       | cific |
   |       |       |       |       |       |       |       |       | c     |
   |       |       |       |       |       |       |       |       | odes. |
   +-------+-------+-------+-------+-------+-------+-------+-------+-------+
   | (12   | CODE  | 1-n   | U     |       |       |       |       | Not   |
   | 6000, |       |       |       |       |       |       |       | used, |
   | DCM,  |       |       |       |       |       |       |       | since |
   | "Im   |       |       |       |       |       |       |       | is    |
   | aging |       |       |       |       |       |       |       | sent  |
   | M     |       |       |       |       |       |       |       | at    |
   | easur |       |       |       |       |       |       |       | m     |
   | ement |       |       |       |       |       |       |       | easur |
   | Rep   |       |       |       |       |       |       |       | ement |
   | ort") |       |       |       |       |       |       |       | group |
   | >     |       |       |       |       |       |       |       | level |
   | (12   |       |       |       |       |       |       |       | since |
   | 6010, |       |       |       |       |       |       |       | c     |
   | DCM,  |       |       |       |       |       |       |       | ommon |
   | "Im   |       |       |       |       |       |       |       | to    |
   | aging |       |       |       |       |       |       |       | all   |
   | Meas  |       |       |       |       |       |       |       | me    |
   | ureme |       |       |       |       |       |       |       | asure |
   | nts") |       |       |       |       |       |       |       | ments |
   | >     |       |       |       |       |       |       |       | in    |
   | (12   |       |       |       |       |       |       |       | a     |
   | 5007, |       |       |       |       |       |       |       | nnota |
   | DCM,  |       |       |       |       |       |       |       | tion. |
   | "M    |       |       |       |       |       |       |       |       |
   | easur |       |       |       |       |       |       |       | If a  |
   | ement |       |       |       |       |       |       |       | p     |
   | Gr    |       |       |       |       |       |       |       | aired |
   | oup") |       |       |       |       |       |       |       | stru  |
   | >     |       |       |       |       |       |       |       | cture |
   | $M    |       |       |       |       |       |       |       | in    |
   | easur |       |       |       |       |       |       |       | AIM,  |
   | ement |       |       |       |       |       |       |       | this  |
   | >     |       |       |       |       |       |       |       | entry |
   | `(    |       |       |       |       |       |       |       | will  |
   | 36369 |       |       |       |       |       |       |       | pre-  |
   | 8007, |       |       |       |       |       |       |       | coord |
   | SCT,  |       |       |       |       |       |       |       | inate |
   | "Fi   |       |       |       |       |       |       |       | the   |
   | nding |       |       |       |       |       |       |       | later |
   | Sit   |       |       |       |       |       |       |       | ality |
   | e") < |       |       |       |       |       |       |       | with  |
   | http: |       |       |       |       |       |       |       | the   |
   | //sno |       |       |       |       |       |       |       | site. |
   | med.i |       |       |       |       |       |       |       |       |
   | nfo/i |       |       |       |       |       |       |       |       |
   | d/363 |       |       |       |       |       |       |       |       |
   | 69800 |       |       |       |       |       |       |       |       |
   | 7>`__ |       |       |       |       |       |       |       |       |
   +-------+-------+-------+-------+-------+-------+-------+-------+-------+
   | (12   | CODE  | 1     | U     |       |       |       |       |       |
   | 6000, |       |       |       |       |       |       |       |       |
   | DCM,  |       |       |       |       |       |       |       |       |
   | "Im   |       |       |       |       |       |       |       |       |
   | aging |       |       |       |       |       |       |       |       |
   | M     |       |       |       |       |       |       |       |       |
   | easur |       |       |       |       |       |       |       |       |
   | ement |       |       |       |       |       |       |       |       |
   | Rep   |       |       |       |       |       |       |       |       |
   | ort") |       |       |       |       |       |       |       |       |
   | >     |       |       |       |       |       |       |       |       |
   | (12   |       |       |       |       |       |       |       |       |
   | 6010, |       |       |       |       |       |       |       |       |
   | DCM,  |       |       |       |       |       |       |       |       |
   | "Im   |       |       |       |       |       |       |       |       |
   | aging |       |       |       |       |       |       |       |       |
   | Meas  |       |       |       |       |       |       |       |       |
   | ureme |       |       |       |       |       |       |       |       |
   | nts") |       |       |       |       |       |       |       |       |
   | >     |       |       |       |       |       |       |       |       |
   | (12   |       |       |       |       |       |       |       |       |
   | 5007, |       |       |       |       |       |       |       |       |
   | DCM,  |       |       |       |       |       |       |       |       |
   | "M    |       |       |       |       |       |       |       |       |
   | easur |       |       |       |       |       |       |       |       |
   | ement |       |       |       |       |       |       |       |       |
   | Gr    |       |       |       |       |       |       |       |       |
   | oup") |       |       |       |       |       |       |       |       |
   | >     |       |       |       |       |       |       |       |       |
   | $M    |       |       |       |       |       |       |       |       |
   | easur |       |       |       |       |       |       |       |       |
   | ement |       |       |       |       |       |       |       |       |
   | >     |       |       |       |       |       |       |       |       |
   | `(    |       |       |       |       |       |       |       |       |
   | 36369 |       |       |       |       |       |       |       |       |
   | 8007, |       |       |       |       |       |       |       |       |
   | SCT,  |       |       |       |       |       |       |       |       |
   | "Fi   |       |       |       |       |       |       |       |       |
   | nding |       |       |       |       |       |       |       |       |
   | Sit   |       |       |       |       |       |       |       |       |
   | e") < |       |       |       |       |       |       |       |       |
   | http: |       |       |       |       |       |       |       |       |
   | //sno |       |       |       |       |       |       |       |       |
   | med.i |       |       |       |       |       |       |       |       |
   | nfo/i |       |       |       |       |       |       |       |       |
   | d/363 |       |       |       |       |       |       |       |       |
   | 69800 |       |       |       |       |       |       |       |       |
   | 7>`__ |       |       |       |       |       |       |       |       |
   | >     |       |       |       |       |       |       |       |       |
   | `(    |       |       |       |       |       |       |       |       |
   | 27274 |       |       |       |       |       |       |       |       |
   | 1003, |       |       |       |       |       |       |       |       |
   | SCT,  |       |       |       |       |       |       |       |       |
   | "Late |       |       |       |       |       |       |       |       |
   | ralit |       |       |       |       |       |       |       |       |
   | y") < |       |       |       |       |       |       |       |       |
   | http: |       |       |       |       |       |       |       |       |
   | //sno |       |       |       |       |       |       |       |       |
   | med.i |       |       |       |       |       |       |       |       |
   | nfo/i |       |       |       |       |       |       |       |       |
   | d/272 |       |       |       |       |       |       |       |       |
   | 74100 |       |       |       |       |       |       |       |       |
   | 3>`__ |       |       |       |       |       |       |       |       |
   +-------+-------+-------+-------+-------+-------+-------+-------+-------+
   | (12   | CODE  | 1     | U     |       |       |       |       | Not   |
   | 6000, |       |       |       |       |       |       |       | used  |
   | DCM,  |       |       |       |       |       |       |       | since |
   | "Im   |       |       |       |       |       |       |       | AIM   |
   | aging |       |       |       |       |       |       |       | does  |
   | M     |       |       |       |       |       |       |       | not   |
   | easur |       |       |       |       |       |       |       | have  |
   | ement |       |       |       |       |       |       |       | a     |
   | Rep   |       |       |       |       |       |       |       | mech  |
   | ort") |       |       |       |       |       |       |       | anism |
   | >     |       |       |       |       |       |       |       | for   |
   | (12   |       |       |       |       |       |       |       | po    |
   | 6010, |       |       |       |       |       |       |       | st-co |
   | DCM,  |       |       |       |       |       |       |       | ordin |
   | "Im   |       |       |       |       |       |       |       | ating |
   | aging |       |       |       |       |       |       |       | the   |
   | Meas  |       |       |       |       |       |       |       | loca  |
   | ureme |       |       |       |       |       |       |       | tion. |
   | nts") |       |       |       |       |       |       |       |       |
   | >     |       |       |       |       |       |       |       |       |
   | (12   |       |       |       |       |       |       |       |       |
   | 5007, |       |       |       |       |       |       |       |       |
   | DCM,  |       |       |       |       |       |       |       |       |
   | "M    |       |       |       |       |       |       |       |       |
   | easur |       |       |       |       |       |       |       |       |
   | ement |       |       |       |       |       |       |       |       |
   | Gr    |       |       |       |       |       |       |       |       |
   | oup") |       |       |       |       |       |       |       |       |
   | >     |       |       |       |       |       |       |       |       |
   | $M    |       |       |       |       |       |       |       |       |
   | easur |       |       |       |       |       |       |       |       |
   | ement |       |       |       |       |       |       |       |       |
   | >     |       |       |       |       |       |       |       |       |
   | `(    |       |       |       |       |       |       |       |       |
   | 36369 |       |       |       |       |       |       |       |       |
   | 8007, |       |       |       |       |       |       |       |       |
   | SCT,  |       |       |       |       |       |       |       |       |
   | "Fi   |       |       |       |       |       |       |       |       |
   | nding |       |       |       |       |       |       |       |       |
   | Sit   |       |       |       |       |       |       |       |       |
   | e") < |       |       |       |       |       |       |       |       |
   | http: |       |       |       |       |       |       |       |       |
   | //sno |       |       |       |       |       |       |       |       |
   | med.i |       |       |       |       |       |       |       |       |
   | nfo/i |       |       |       |       |       |       |       |       |
   | d/363 |       |       |       |       |       |       |       |       |
   | 69800 |       |       |       |       |       |       |       |       |
   | 7>`__ |       |       |       |       |       |       |       |       |
   | >     |       |       |       |       |       |       |       |       |
   | `(    |       |       |       |       |       |       |       |       |
   | 10623 |       |       |       |       |       |       |       |       |
   | 3006, |       |       |       |       |       |       |       |       |
   | SCT,  |       |       |       |       |       |       |       |       |
   | "Top  |       |       |       |       |       |       |       |       |
   | ograp |       |       |       |       |       |       |       |       |
   | hical |       |       |       |       |       |       |       |       |
   | mo    |       |       |       |       |       |       |       |       |
   | difie |       |       |       |       |       |       |       |       |
   | r") < |       |       |       |       |       |       |       |       |
   | http: |       |       |       |       |       |       |       |       |
   | //sno |       |       |       |       |       |       |       |       |
   | med.i |       |       |       |       |       |       |       |       |
   | nfo/i |       |       |       |       |       |       |       |       |
   | d/106 |       |       |       |       |       |       |       |       |
   | 23300 |       |       |       |       |       |       |       |       |
   | 6>`__ |       |       |       |       |       |       |       |       |
   +-------+-------+-------+-------+-------+-------+-------+-------+-------+
   | (12   | IN    | 1     | U     |       | S     |       |       |       |
   | 6000, | CLUDE |       |       |       | tatis |       |       |       |
   | DCM,  |       |       |       |       | tical |       |       |       |
   | "Im   |       |       |       |       | and   |       |       |       |
   | aging |       |       |       |       | n     |       |       |       |
   | M     |       |       |       |       | ormal |       |       |       |
   | easur |       |       |       |       | range |       |       |       |
   | ement |       |       |       |       | prope |       |       |       |
   | Rep   |       |       |       |       | rties |       |       |       |
   | ort") |       |       |       |       | are   |       |       |       |
   | >     |       |       |       |       | not   |       |       |       |
   | (12   |       |       |       |       | used  |       |       |       |
   | 6010, |       |       |       |       | in    |       |       |       |
   | DCM,  |       |       |       |       | AIM   |       |       |       |
   | "Im   |       |       |       |       | use   |       |       |       |
   | aging |       |       |       |       | cases |       |       |       |
   | Meas  |       |       |       |       | for   |       |       |       |
   | ureme |       |       |       |       | this  |       |       |       |
   | nts") |       |       |       |       | map   |       |       |       |
   | >     |       |       |       |       | ping. |       |       |       |
   | (12   |       |       |       |       |       |       |       |       |
   | 5007, |       |       |       |       |       |       |       |       |
   | DCM,  |       |       |       |       |       |       |       |       |
   | "M    |       |       |       |       |       |       |       |       |
   | easur |       |       |       |       |       |       |       |       |
   | ement |       |       |       |       |       |       |       |       |
   | Gr    |       |       |       |       |       |       |       |       |
   | oup") |       |       |       |       |       |       |       |       |
   | >     |       |       |       |       |       |       |       |       |
   | $M    |       |       |       |       |       |       |       |       |
   | easur |       |       |       |       |       |       |       |       |
   | ement |       |       |       |       |       |       |       |       |
   | >     |       |       |       |       |       |       |       |       |
   +-------+-------+-------+-------+-------+-------+-------+-------+-------+
   | (12   | NUM   | 1-n   | UC    |       |       |       |       | Not   |
   | 6000, |       |       |       |       |       |       |       | used  |
   | DCM,  |       |       |       |       |       |       |       | in    |
   | "Im   |       |       |       |       |       |       |       | AIM   |
   | aging |       |       |       |       |       |       |       |       |
   | M     |       |       |       |       |       |       |       |       |
   | easur |       |       |       |       |       |       |       |       |
   | ement |       |       |       |       |       |       |       |       |
   | Rep   |       |       |       |       |       |       |       |       |
   | ort") |       |       |       |       |       |       |       |       |
   | >     |       |       |       |       |       |       |       |       |
   | (12   |       |       |       |       |       |       |       |       |
   | 6010, |       |       |       |       |       |       |       |       |
   | DCM,  |       |       |       |       |       |       |       |       |
   | "Im   |       |       |       |       |       |       |       |       |
   | aging |       |       |       |       |       |       |       |       |
   | Meas  |       |       |       |       |       |       |       |       |
   | ureme |       |       |       |       |       |       |       |       |
   | nts") |       |       |       |       |       |       |       |       |
   | >     |       |       |       |       |       |       |       |       |
   | (12   |       |       |       |       |       |       |       |       |
   | 5007, |       |       |       |       |       |       |       |       |
   | DCM,  |       |       |       |       |       |       |       |       |
   | "M    |       |       |       |       |       |       |       |       |
   | easur |       |       |       |       |       |       |       |       |
   | ement |       |       |       |       |       |       |       |       |
   | Gr    |       |       |       |       |       |       |       |       |
   | oup") |       |       |       |       |       |       |       |       |
   | >     |       |       |       |       |       |       |       |       |
   | $M    |       |       |       |       |       |       |       |       |
   | easur |       |       |       |       |       |       |       |       |
   | ement |       |       |       |       |       |       |       |       |
   | >     |       |       |       |       |       |       |       |       |
   | $Deri |       |       |       |       |       |       |       |       |
   | vatio |       |       |       |       |       |       |       |       |
   | nPara |       |       |       |       |       |       |       |       |
   | meter |       |       |       |       |       |       |       |       |
   +-------+-------+-------+-------+-------+-------+-------+-------+-------+
   | (12   | NUM   | 1-n   | UC    |       |       |       |       | Not   |
   | 6000, |       |       |       |       |       |       |       | used  |
   | DCM,  |       |       |       |       |       |       |       | in    |
   | "Im   |       |       |       |       |       |       |       | AIM   |
   | aging |       |       |       |       |       |       |       |       |
   | M     |       |       |       |       |       |       |       |       |
   | easur |       |       |       |       |       |       |       |       |
   | ement |       |       |       |       |       |       |       |       |
   | Rep   |       |       |       |       |       |       |       |       |
   | ort") |       |       |       |       |       |       |       |       |
   | >     |       |       |       |       |       |       |       |       |
   | (12   |       |       |       |       |       |       |       |       |
   | 6010, |       |       |       |       |       |       |       |       |
   | DCM,  |       |       |       |       |       |       |       |       |
   | "Im   |       |       |       |       |       |       |       |       |
   | aging |       |       |       |       |       |       |       |       |
   | Meas  |       |       |       |       |       |       |       |       |
   | ureme |       |       |       |       |       |       |       |       |
   | nts") |       |       |       |       |       |       |       |       |
   | >     |       |       |       |       |       |       |       |       |
   | (12   |       |       |       |       |       |       |       |       |
   | 5007, |       |       |       |       |       |       |       |       |
   | DCM,  |       |       |       |       |       |       |       |       |
   | "M    |       |       |       |       |       |       |       |       |
   | easur |       |       |       |       |       |       |       |       |
   | ement |       |       |       |       |       |       |       |       |
   | Gr    |       |       |       |       |       |       |       |       |
   | oup") |       |       |       |       |       |       |       |       |
   | >     |       |       |       |       |       |       |       |       |
   | $M    |       |       |       |       |       |       |       |       |
   | easur |       |       |       |       |       |       |       |       |
   | ement |       |       |       |       |       |       |       |       |
   | >     |       |       |       |       |       |       |       |       |
   | $Deri |       |       |       |       |       |       |       |       |
   | vatio |       |       |       |       |       |       |       |       |
   | nPara |       |       |       |       |       |       |       |       |
   | meter |       |       |       |       |       |       |       |       |
   +-------+-------+-------+-------+-------+-------+-------+-------+-------+
   | (12   | IN    | 1     | UC    |       | Not   |       |       |       |
   | 6000, | CLUDE |       |       |       | used  |       |       |       |
   | DCM,  |       |       |       |       | in    |       |       |       |
   | "Im   |       |       |       |       | AIM   |       |       |       |
   | aging |       |       |       |       |       |       |       |       |
   | M     |       |       |       |       |       |       |       |       |
   | easur |       |       |       |       |       |       |       |       |
   | ement |       |       |       |       |       |       |       |       |
   | Rep   |       |       |       |       |       |       |       |       |
   | ort") |       |       |       |       |       |       |       |       |
   | >     |       |       |       |       |       |       |       |       |
   | (12   |       |       |       |       |       |       |       |       |
   | 6010, |       |       |       |       |       |       |       |       |
   | DCM,  |       |       |       |       |       |       |       |       |
   | "Im   |       |       |       |       |       |       |       |       |
   | aging |       |       |       |       |       |       |       |       |
   | Meas  |       |       |       |       |       |       |       |       |
   | ureme |       |       |       |       |       |       |       |       |
   | nts") |       |       |       |       |       |       |       |       |
   | >     |       |       |       |       |       |       |       |       |
   | (12   |       |       |       |       |       |       |       |       |
   | 5007, |       |       |       |       |       |       |       |       |
   | DCM,  |       |       |       |       |       |       |       |       |
   | "M    |       |       |       |       |       |       |       |       |
   | easur |       |       |       |       |       |       |       |       |
   | ement |       |       |       |       |       |       |       |       |
   | Gr    |       |       |       |       |       |       |       |       |
   | oup") |       |       |       |       |       |       |       |       |
   | >     |       |       |       |       |       |       |       |       |
   | $M    |       |       |       |       |       |       |       |       |
   | easur |       |       |       |       |       |       |       |       |
   | ement |       |       |       |       |       |       |       |       |
   | >     |       |       |       |       |       |       |       |       |
   +-------+-------+-------+-------+-------+-------+-------+-------+-------+
   | (12   | TEXT  | 1     | UC    |       |       |       |       | Not   |
   | 6000, |       |       |       |       |       |       |       | used  |
   | DCM,  |       |       |       |       |       |       |       | in    |
   | "Im   |       |       |       |       |       |       |       | AIM   |
   | aging |       |       |       |       |       |       |       |       |
   | M     |       |       |       |       |       |       |       |       |
   | easur |       |       |       |       |       |       |       |       |
   | ement |       |       |       |       |       |       |       |       |
   | Rep   |       |       |       |       |       |       |       |       |
   | ort") |       |       |       |       |       |       |       |       |
   | >     |       |       |       |       |       |       |       |       |
   | (12   |       |       |       |       |       |       |       |       |
   | 6010, |       |       |       |       |       |       |       |       |
   | DCM,  |       |       |       |       |       |       |       |       |
   | "Im   |       |       |       |       |       |       |       |       |
   | aging |       |       |       |       |       |       |       |       |
   | Meas  |       |       |       |       |       |       |       |       |
   | ureme |       |       |       |       |       |       |       |       |
   | nts") |       |       |       |       |       |       |       |       |
   | >     |       |       |       |       |       |       |       |       |
   | (12   |       |       |       |       |       |       |       |       |
   | 5007, |       |       |       |       |       |       |       |       |
   | DCM,  |       |       |       |       |       |       |       |       |
   | "M    |       |       |       |       |       |       |       |       |
   | easur |       |       |       |       |       |       |       |       |
   | ement |       |       |       |       |       |       |       |       |
   | Gr    |       |       |       |       |       |       |       |       |
   | oup") |       |       |       |       |       |       |       |       |
   | >     |       |       |       |       |       |       |       |       |
   | $M    |       |       |       |       |       |       |       |       |
   | easur |       |       |       |       |       |       |       |       |
   | ement |       |       |       |       |       |       |       |       |
   | >     |       |       |       |       |       |       |       |       |
   | TEXT  |       |       |       |       |       |       |       |       |
   +-------+-------+-------+-------+-------+-------+-------+-------+-------+
   | (12   | IN    | 1     | U     |       | Quota |       |       |       |
   | 6000, | CLUDE |       |       |       | tions |       |       |       |
   | DCM,  |       |       |       |       | are   |       |       |       |
   | "Im   |       |       |       |       | not   |       |       |       |
   | aging |       |       |       |       | used  |       |       |       |
   | M     |       |       |       |       | in    |       |       |       |
   | easur |       |       |       |       | AIM.  |       |       |       |
   | ement |       |       |       |       |       |       |       |       |
   | Rep   |       |       |       |       |       |       |       |       |
   | ort") |       |       |       |       |       |       |       |       |
   | >     |       |       |       |       |       |       |       |       |
   | (12   |       |       |       |       |       |       |       |       |
   | 6010, |       |       |       |       |       |       |       |       |
   | DCM,  |       |       |       |       |       |       |       |       |
   | "Im   |       |       |       |       |       |       |       |       |
   | aging |       |       |       |       |       |       |       |       |
   | Meas  |       |       |       |       |       |       |       |       |
   | ureme |       |       |       |       |       |       |       |       |
   | nts") |       |       |       |       |       |       |       |       |
   | >     |       |       |       |       |       |       |       |       |
   | (12   |       |       |       |       |       |       |       |       |
   | 5007, |       |       |       |       |       |       |       |       |
   | DCM,  |       |       |       |       |       |       |       |       |
   | "M    |       |       |       |       |       |       |       |       |
   | easur |       |       |       |       |       |       |       |       |
   | ement |       |       |       |       |       |       |       |       |
   | Gr    |       |       |       |       |       |       |       |       |
   | oup") |       |       |       |       |       |       |       |       |
   | >     |       |       |       |       |       |       |       |       |
   | $M    |       |       |       |       |       |       |       |       |
   | easur |       |       |       |       |       |       |       |       |
   | ement |       |       |       |       |       |       |       |       |
   | >     |       |       |       |       |       |       |       |       |
   +-------+-------+-------+-------+-------+-------+-------+-------+-------+
   | (12   | TEXT  | 1     | U     |       |       |       |       | Not   |
   | 6000, |       |       |       |       |       |       |       | used  |
   | DCM,  |       |       |       |       |       |       |       | in    |
   | "Im   |       |       |       |       |       |       |       | AIM.  |
   | aging |       |       |       |       |       |       |       |       |
   | M     |       |       |       |       |       |       |       |       |
   | easur |       |       |       |       |       |       |       |       |
   | ement |       |       |       |       |       |       |       |       |
   | Rep   |       |       |       |       |       |       |       |       |
   | ort") |       |       |       |       |       |       |       |       |
   | >     |       |       |       |       |       |       |       |       |
   | (12   |       |       |       |       |       |       |       |       |
   | 6010, |       |       |       |       |       |       |       |       |
   | DCM,  |       |       |       |       |       |       |       |       |
   | "Im   |       |       |       |       |       |       |       |       |
   | aging |       |       |       |       |       |       |       |       |
   | Meas  |       |       |       |       |       |       |       |       |
   | ureme |       |       |       |       |       |       |       |       |
   | nts") |       |       |       |       |       |       |       |       |
   | >     |       |       |       |       |       |       |       |       |
   | (12   |       |       |       |       |       |       |       |       |
   | 5007, |       |       |       |       |       |       |       |       |
   | DCM,  |       |       |       |       |       |       |       |       |
   | "M    |       |       |       |       |       |       |       |       |
   | easur |       |       |       |       |       |       |       |       |
   | ement |       |       |       |       |       |       |       |       |
   | Gr    |       |       |       |       |       |       |       |       |
   | oup") |       |       |       |       |       |       |       |       |
   | >     |       |       |       |       |       |       |       |       |
   | $M    |       |       |       |       |       |       |       |       |
   | easur |       |       |       |       |       |       |       |       |
   | ement |       |       |       |       |       |       |       |       |
   | >     |       |       |       |       |       |       |       |       |
   | (12   |       |       |       |       |       |       |       |       |
   | 1050, |       |       |       |       |       |       |       |       |
   | DCM,  |       |       |       |       |       |       |       |       |
   | "     |       |       |       |       |       |       |       |       |
   | Equiv |       |       |       |       |       |       |       |       |
   | alent |       |       |       |       |       |       |       |       |
   | Me    |       |       |       |       |       |       |       |       |
   | aning |       |       |       |       |       |       |       |       |
   | of    |       |       |       |       |       |       |       |       |
   | Co    |       |       |       |       |       |       |       |       |
   | ncept |       |       |       |       |       |       |       |       |
   | N     |       |       |       |       |       |       |       |       |
   | ame") |       |       |       |       |       |       |       |       |
   +-------+-------+-------+-------+-------+-------+-------+-------+-------+
   | (12   | COMP  | 1     | U     |       |       |       |       | Not   |
   | 6000, | OSITE |       |       |       |       |       |       | used  |
   | DCM,  |       |       |       |       |       |       |       | in    |
   | "Im   |       |       |       |       |       |       |       | AIM.  |
   | aging |       |       |       |       |       |       |       |       |
   | M     |       |       |       |       |       |       |       |       |
   | easur |       |       |       |       |       |       |       |       |
   | ement |       |       |       |       |       |       |       |       |
   | Rep   |       |       |       |       |       |       |       |       |
   | ort") |       |       |       |       |       |       |       |       |
   | >     |       |       |       |       |       |       |       |       |
   | (12   |       |       |       |       |       |       |       |       |
   | 6010, |       |       |       |       |       |       |       |       |
   | DCM,  |       |       |       |       |       |       |       |       |
   | "Im   |       |       |       |       |       |       |       |       |
   | aging |       |       |       |       |       |       |       |       |
   | Meas  |       |       |       |       |       |       |       |       |
   | ureme |       |       |       |       |       |       |       |       |
   | nts") |       |       |       |       |       |       |       |       |
   | >     |       |       |       |       |       |       |       |       |
   | (12   |       |       |       |       |       |       |       |       |
   | 5007, |       |       |       |       |       |       |       |       |
   | DCM,  |       |       |       |       |       |       |       |       |
   | "M    |       |       |       |       |       |       |       |       |
   | easur |       |       |       |       |       |       |       |       |
   | ement |       |       |       |       |       |       |       |       |
   | Gr    |       |       |       |       |       |       |       |       |
   | oup") |       |       |       |       |       |       |       |       |
   | >     |       |       |       |       |       |       |       |       |
   | $M    |       |       |       |       |       |       |       |       |
   | easur |       |       |       |       |       |       |       |       |
   | ement |       |       |       |       |       |       |       |       |
   | >     |       |       |       |       |       |       |       |       |
   | (12   |       |       |       |       |       |       |       |       |
   | 6100, |       |       |       |       |       |       |       |       |
   | DCM,  |       |       |       |       |       |       |       |       |
   | "Real |       |       |       |       |       |       |       |       |
   | World |       |       |       |       |       |       |       |       |
   | Value |       |       |       |       |       |       |       |       |
   | Map   |       |       |       |       |       |       |       |       |
   | used  |       |       |       |       |       |       |       |       |
   | for   |       |       |       |       |       |       |       |       |
   | mea   |       |       |       |       |       |       |       |       |
   | surem |       |       |       |       |       |       |       |       |
   | ent") |       |       |       |       |       |       |       |       |
   +-------+-------+-------+-------+-------+-------+-------+-------+-------+
   | (12   | IN    | 1     | U     | `Ma   |       |       |       |       |
   | 6000, | CLUDE |       |       | pping |       |       |       |       |
   | DCM,  |       |       |       | of    |       |       |       |       |
   | "Im   |       |       |       | Algo  |       |       |       |       |
   | aging |       |       |       | rithm |       |       |       |       |
   | M     |       |       |       | Id    |       |       |       |       |
   | easur |       |       |       | entif |       |       |       |       |
   | ement |       |       |       | icati |       |       |       |       |
   | Rep   |       |       |       | on <# |       |       |       |       |
   | ort") |       |       |       | sect_ |       |       |       |       |
   | >     |       |       |       | Mappi |       |       |       |       |
   | (12   |       |       |       | ng_TI |       |       |       |       |
   | 6010, |       |       |       | D_401 |       |       |       |       |
   | DCM,  |       |       |       | 9>`__ |       |       |       |       |
   | "Im   |       |       |       |       |       |       |       |       |
   | aging |       |       |       |       |       |       |       |       |
   | Meas  |       |       |       |       |       |       |       |       |
   | ureme |       |       |       |       |       |       |       |       |
   | nts") |       |       |       |       |       |       |       |       |
   | >     |       |       |       |       |       |       |       |       |
   | (12   |       |       |       |       |       |       |       |       |
   | 5007, |       |       |       |       |       |       |       |       |
   | DCM,  |       |       |       |       |       |       |       |       |
   | "M    |       |       |       |       |       |       |       |       |
   | easur |       |       |       |       |       |       |       |       |
   | ement |       |       |       |       |       |       |       |       |
   | Gr    |       |       |       |       |       |       |       |       |
   | oup") |       |       |       |       |       |       |       |       |
   | >     |       |       |       |       |       |       |       |       |
   | $M    |       |       |       |       |       |       |       |       |
   | easur |       |       |       |       |       |       |       |       |
   | ement |       |       |       |       |       |       |       |       |
   | >     |       |       |       |       |       |       |       |       |
   +-------+-------+-------+-------+-------+-------+-------+-------+-------+

.. _sect_Mapping_TID_1420:

Mapping of Measurements Derived From Multiple ROI Measurements
''''''''''''''''''''''''''''''''''''''''''''''''''''''''''''''

This section describes the mapping of .

.. table:: Mapping of Measurements Derived From Multiple ROI
Measurements

   +-------+-------+-------+-------+-------+-------+-------+-------+-------+
   | DICOM | DICOM | DICOM | DICOM | Gene  | AIM   | AIM   | AIM   | Co    |
   | SR    | VT    | VM    | Usage | rated | El    | Data  | Mu    | mment |
   | Path  |       |       | Type  | Value | ement | Type  | ltipl |       |
   |       |       |       |       |       | or    |       | icity |       |
   |       |       |       |       |       | Attr  |       |       |       |
   |       |       |       |       |       | ibute |       |       |       |
   +=======+=======+=======+=======+=======+=======+=======+=======+=======+
   | (12   | NUM   | 1-n   | M     |       |       |       |       |       |
   | 6000, |       |       |       |       |       |       |       |       |
   | DCM,  |       |       |       |       |       |       |       |       |
   | "Im   |       |       |       |       |       |       |       |       |
   | aging |       |       |       |       |       |       |       |       |
   | M     |       |       |       |       |       |       |       |       |
   | easur |       |       |       |       |       |       |       |       |
   | ement |       |       |       |       |       |       |       |       |
   | Rep   |       |       |       |       |       |       |       |       |
   | ort") |       |       |       |       |       |       |       |       |
   | >     |       |       |       |       |       |       |       |       |
   | (12   |       |       |       |       |       |       |       |       |
   | 6011, |       |       |       |       |       |       |       |       |
   | DCM,  |       |       |       |       |       |       |       |       |
   | "De   |       |       |       |       |       |       |       |       |
   | rived |       |       |       |       |       |       |       |       |
   | Im    |       |       |       |       |       |       |       |       |
   | aging |       |       |       |       |       |       |       |       |
   | Meas  |       |       |       |       |       |       |       |       |
   | ureme |       |       |       |       |       |       |       |       |
   | nts") |       |       |       |       |       |       |       |       |
   | > NUM |       |       |       |       |       |       |       |       |
   +-------+-------+-------+-------+-------+-------+-------+-------+-------+
   | (12   | IN    | 1-n   | MC    | `Ma   |       |       |       |       |
   | 6000, | CLUDE |       |       | pping |       |       |       |       |
   | DCM,  |       |       |       | of    |       |       |       |       |
   | "Im   |       |       |       | P     |       |       |       |       |
   | aging |       |       |       | lanar |       |       |       |       |
   | M     |       |       |       | ROI   |       |       |       |       |
   | easur |       |       |       | Measu |       |       |       |       |
   | ement |       |       |       | remen |       |       |       |       |
   | Rep   |       |       |       | ts <# |       |       |       |       |
   | ort") |       |       |       | sect_ |       |       |       |       |
   | >     |       |       |       | Mappi |       |       |       |       |
   | (12   |       |       |       | ng_TI |       |       |       |       |
   | 6011, |       |       |       | D_141 |       |       |       |       |
   | DCM,  |       |       |       | 0>`__ |       |       |       |       |
   | "De   |       |       |       |       |       |       |       |       |
   | rived |       |       |       |       |       |       |       |       |
   | Im    |       |       |       |       |       |       |       |       |
   | aging |       |       |       |       |       |       |       |       |
   | Meas  |       |       |       |       |       |       |       |       |
   | ureme |       |       |       |       |       |       |       |       |
   | nts") |       |       |       |       |       |       |       |       |
   | > NUM |       |       |       |       |       |       |       |       |
   | >     |       |       |       |       |       |       |       |       |
   +-------+-------+-------+-------+-------+-------+-------+-------+-------+
   | (12   | IN    | 1-n   | MC    | `Ma   |       |       |       |       |
   | 6000, | CLUDE |       |       | pping |       |       |       |       |
   | DCM,  |       |       |       | of    |       |       |       |       |
   | "Im   |       |       |       | Volum |       |       |       |       |
   | aging |       |       |       | etric |       |       |       |       |
   | M     |       |       |       | ROI   |       |       |       |       |
   | easur |       |       |       | Measu |       |       |       |       |
   | ement |       |       |       | remen |       |       |       |       |
   | Rep   |       |       |       | ts <# |       |       |       |       |
   | ort") |       |       |       | sect_ |       |       |       |       |
   | >     |       |       |       | Mappi |       |       |       |       |
   | (12   |       |       |       | ng_TI |       |       |       |       |
   | 6011, |       |       |       | D_141 |       |       |       |       |
   | DCM,  |       |       |       | 1>`__ |       |       |       |       |
   | "De   |       |       |       |       |       |       |       |       |
   | rived |       |       |       |       |       |       |       |       |
   | Im    |       |       |       |       |       |       |       |       |
   | aging |       |       |       |       |       |       |       |       |
   | Meas  |       |       |       |       |       |       |       |       |
   | ureme |       |       |       |       |       |       |       |       |
   | nts") |       |       |       |       |       |       |       |       |
   | > NUM |       |       |       |       |       |       |       |       |
   | >     |       |       |       |       |       |       |       |       |
   +-------+-------+-------+-------+-------+-------+-------+-------+-------+
   | (12   | IN    | 1     | U     |       | S     |       |       |       |
   | 6000, | CLUDE |       |       |       | tatis |       |       |       |
   | DCM,  |       |       |       |       | tical |       |       |       |
   | "Im   |       |       |       |       | and   |       |       |       |
   | aging |       |       |       |       | n     |       |       |       |
   | M     |       |       |       |       | ormal |       |       |       |
   | easur |       |       |       |       | range |       |       |       |
   | ement |       |       |       |       | prope |       |       |       |
   | Rep   |       |       |       |       | rties |       |       |       |
   | ort") |       |       |       |       | are   |       |       |       |
   | >     |       |       |       |       | not   |       |       |       |
   | (12   |       |       |       |       | used  |       |       |       |
   | 6011, |       |       |       |       | in    |       |       |       |
   | DCM,  |       |       |       |       | AIM   |       |       |       |
   | "De   |       |       |       |       | use   |       |       |       |
   | rived |       |       |       |       | cases |       |       |       |
   | Im    |       |       |       |       | for   |       |       |       |
   | aging |       |       |       |       | this  |       |       |       |
   | Meas  |       |       |       |       | map   |       |       |       |
   | ureme |       |       |       |       | ping. |       |       |       |
   | nts") |       |       |       |       |       |       |       |       |
   | > NUM |       |       |       |       |       |       |       |       |
   | >     |       |       |       |       |       |       |       |       |
   +-------+-------+-------+-------+-------+-------+-------+-------+-------+

.. _sect_Mapping_TID_300:

Mapping of Measurement
''''''''''''''''''''''

This section describes the mapping of .

.. table:: Mapping of Measurement

   +-------+-------+-------+-------+-------+-------+-------+-------+-------+
   | DICOM | DICOM | DICOM | DICOM | Gene  | AIM   | AIM   | AIM   | Co    |
   | SR    | VT    | VM    | Usage | rated | El    | Data  | Mu    | mment |
   | Path  |       |       | Type  | Value | ement | Type  | ltipl |       |
   |       |       |       |       |       | or    |       | icity |       |
   |       |       |       |       |       | Attr  |       |       |       |
   |       |       |       |       |       | ibute |       |       |       |
   +=======+=======+=======+=======+=======+=======+=======+=======+=======+
   | (12   | NUM   | 1     | M     |       | NAME  | CD,   | 1..n, | The   |
   | 6000, |       |       |       |       | =     | ST,   | 0..n, | first |
   | DCM,  |       |       |       |       | Ima   | CD    | 1     | typ   |
   | "Im   |       |       |       |       | ge​An |       |       | eCode |
   | aging |       |       |       |       | notat |       |       | entry |
   | M     |       |       |       |       | ion​​ |       |       | is    |
   | easur |       |       |       |       | Colle |       |       | as    |
   | ement |       |       |       |       | ction |       |       | sumed |
   | Rep   |       |       |       |       | /​ima |       |       | to be |
   | ort") |       |       |       |       | ge​An |       |       | the   |
   | >     |       |       |       |       | notat |       |       | pr    |
   | (12   |       |       |       |       | ions/ |       |       | imary |
   | 6010, |       |       |       |       | ​Imag |       |       | con   |
   | DCM,  |       |       |       |       | e​Ann |       |       | cept. |
   | "Im   |       |       |       |       | otati |       |       | Other |
   | aging |       |       |       |       | on/​c |       |       | typ   |
   | Meas  |       |       |       |       | alcul |       |       | eCode |
   | ureme |       |       |       |       | ation |       |       | en    |
   | nts") |       |       |       |       | ​Enti |       |       | tries |
   | >     |       |       |       |       | ty​Co |       |       | may   |
   | (12   |       |       |       |       | llect |       |       | be    |
   | 5007, |       |       |       |       | ion/​ |       |       | consi |
   | DCM,  |       |       |       |       | Calcu |       |       | dered |
   | "M    |       |       |       |       | latio |       |       | as    |
   | easur |       |       |       |       | nEnti |       |       | modif |
   | ement |       |       |       |       | ty/​t |       |       | iers. |
   | Gr    |       |       |       |       | ypeCo |       |       |       |
   | oup") |       |       |       |       | de[1] |       |       | Value |
   | >     |       |       |       |       |       |       |       | may   |
   | $M    |       |       |       |       | VALUE |       |       | be    |
   | easur |       |       |       |       | =     |       |       | found |
   | ement |       |       |       |       | Imag  |       |       | in    |
   |       |       |       |       |       | e​Ann |       |       | e     |
   |       |       |       |       |       | otati |       |       | ither |
   |       |       |       |       |       | on​​C |       |       | C     |
   |       |       |       |       |       | ollec |       |       | ompac |
   |       |       |       |       |       | tion/ |       |       | t​Cal |
   |       |       |       |       |       | ​imag |       |       | culat |
   |       |       |       |       |       | e​Ann |       |       | ion​R |
   |       |       |       |       |       | otati |       |       | esult |
   |       |       |       |       |       | ons/​ |       |       | (     |
   |       |       |       |       |       | Image |       |       | i.e., |
   |       |       |       |       |       | ​Anno |       |       | value |
   |       |       |       |       |       | tatio |       |       | child |
   |       |       |       |       |       | n/​ca |       |       | of    |
   |       |       |       |       |       | lcula |       |       | Cal   |
   |       |       |       |       |       | tion​ |       |       | culat |
   |       |       |       |       |       | Entit |       |       | ionRe |
   |       |       |       |       |       | y​Col |       |       | sult) |
   |       |       |       |       |       | lecti |       |       | or    |
   |       |       |       |       |       | on/​C |       |       | first |
   |       |       |       |       |       | alcul |       |       | value |
   |       |       |       |       |       | ation |       |       | of    |
   |       |       |       |       |       | Entit |       |       | Ex    |
   |       |       |       |       |       | y/​ca |       |       | tende |
   |       |       |       |       |       | lcula |       |       | d​Cal |
   |       |       |       |       |       | tionR |       |       | culat |
   |       |       |       |       |       | esult |       |       | ion​R |
   |       |       |       |       |       | ​Coll |       |       | esult |
   |       |       |       |       |       | ectio |       |       | (     |
   |       |       |       |       |       | n/​Ca |       |       | i.e., |
   |       |       |       |       |       | lcula |       |       | n     |
   |       |       |       |       |       | tionR |       |       | ested |
   |       |       |       |       |       | esult |       |       | w     |
   |       |       |       |       |       | /​​@v |       |       | ithin |
   |       |       |       |       |       | alue, |       |       | c     |
   |       |       |       |       |       | c     |       |       | alcul |
   |       |       |       |       |       | alcul |       |       | ation |
   |       |       |       |       |       | ation |       |       | ​Resu |
   |       |       |       |       |       | Data​ |       |       | lt​Co |
   |       |       |       |       |       | Colle |       |       | llect |
   |       |       |       |       |       | ction |       |       | ion). |
   |       |       |       |       |       | /​Cal |       |       |       |
   |       |       |       |       |       | culat |       |       | Only  |
   |       |       |       |       |       | ionDa |       |       | ma    |
   |       |       |       |       |       | ta/​@ |       |       | pping |
   |       |       |       |       |       | value |       |       | of a  |
   |       |       |       |       |       |       |       |       | s     |
   |       |       |       |       |       | UNITS |       |       | ingle |
   |       |       |       |       |       | =     |       |       | value |
   |       |       |       |       |       | Imag  |       |       | from  |
   |       |       |       |       |       | e​Ann |       |       | Ex    |
   |       |       |       |       |       | otati |       |       | tende |
   |       |       |       |       |       | on​​C |       |       | d​Cal |
   |       |       |       |       |       | ollec |       |       | culat |
   |       |       |       |       |       | tion/ |       |       | ion​R |
   |       |       |       |       |       | ​imag |       |       | esult |
   |       |       |       |       |       | e​Ann |       |       | is    |
   |       |       |       |       |       | otati |       |       | suppo |
   |       |       |       |       |       | ons/​ |       |       | rted. |
   |       |       |       |       |       | Image |       |       |       |
   |       |       |       |       |       | ​Anno |       |       | The   |
   |       |       |       |       |       | tatio |       |       | value |
   |       |       |       |       |       | n/​ca |       |       | of    |
   |       |       |       |       |       | lcula |       |       | ai    |
   |       |       |       |       |       | tion​ |       |       | m:uni |
   |       |       |       |       |       | Entit |       |       | que​I |
   |       |       |       |       |       | y​Col |       |       | denti |
   |       |       |       |       |       | lecti |       |       | fier/ |
   |       |       |       |       |       | on/​C |       |       | @root |
   |       |       |       |       |       | alcul |       |       | is    |
   |       |       |       |       |       | ation |       |       | m     |
   |       |       |       |       |       | Entit |       |       | apped |
   |       |       |       |       |       | y/​ca |       |       | to    |
   |       |       |       |       |       | lcula |       |       | the   |
   |       |       |       |       |       | tionR |       |       | Obser |
   |       |       |       |       |       | esult |       |       | vatio |
   |       |       |       |       |       | ​Coll |       |       | n​UID |
   |       |       |       |       |       | ectio |       |       | Attr  |
   |       |       |       |       |       | n/​Ca |       |       | ibute |
   |       |       |       |       |       | lcula |       |       | of    |
   |       |       |       |       |       | tionR |       |       | the   |
   |       |       |       |       |       | esult |       |       | NUM   |
   |       |       |       |       |       | /​uni |       |       | Co    |
   |       |       |       |       |       | tOfMe |       |       | ntent |
   |       |       |       |       |       | asure |       |       | Item. |
   +-------+-------+-------+-------+-------+-------+-------+-------+-------+
   | (12   | CODE  | 1-n   | U     |       | Im    | CD    | 1..n  | The   |
   | 6000, |       |       |       |       | age​A |       |       | first |
   | DCM,  |       |       |       |       | nnota |       |       | typ   |
   | "Im   |       |       |       |       | tion​ |       |       | eCode |
   | aging |       |       |       |       | ​Coll |       |       | entry |
   | M     |       |       |       |       | ectio |       |       | is    |
   | easur |       |       |       |       | n/​im |       |       | as    |
   | ement |       |       |       |       | age​A |       |       | sumed |
   | Rep   |       |       |       |       | nnota |       |       | to be |
   | ort") |       |       |       |       | tions |       |       | the   |
   | >     |       |       |       |       | /​Ima |       |       | pr    |
   | (12   |       |       |       |       | ge​An |       |       | imary |
   | 6010, |       |       |       |       | notat |       |       | con   |
   | DCM,  |       |       |       |       | ion/​ |       |       | cept. |
   | "Im   |       |       |       |       | calcu |       |       | This  |
   | aging |       |       |       |       | latio |       |       | row   |
   | Meas  |       |       |       |       | n​Ent |       |       | can   |
   | ureme |       |       |       |       | ity​C |       |       | be    |
   | nts") |       |       |       |       | ollec |       |       | used  |
   | >     |       |       |       |       | tion/ |       |       | if    |
   | (12   |       |       |       |       | ​Calc |       |       | succe |
   | 5007, |       |       |       |       | ulati |       |       | ssive |
   | DCM,  |       |       |       |       | onEnt |       |       | typ   |
   | "M    |       |       |       |       | ity/​ |       |       | eCode |
   | easur |       |       |       |       | typeC |       |       | en    |
   | ement |       |       |       |       | ode​[ |       |       | tries |
   | Gr    |       |       |       |       | posit |       |       | are   |
   | oup") |       |       |       |       | ion() |       |       | r     |
   | >     |       |       |       |       | != 1] |       |       | ecogn |
   | $M    |       |       |       |       |       |       |       | ized, |
   | easur |       |       |       |       |       |       |       | and   |
   | ement |       |       |       |       |       |       |       | not a |
   | >     |       |       |       |       |       |       |       | m     |
   | $Mo   |       |       |       |       |       |       |       | ethod |
   | dType |       |       |       |       |       |       |       | or    |
   |       |       |       |       |       |       |       |       | d     |
   |       |       |       |       |       |       |       |       | eriva |
   |       |       |       |       |       |       |       |       | tion, |
   |       |       |       |       |       |       |       |       | and a |
   |       |       |       |       |       |       |       |       | name- |
   |       |       |       |       |       |       |       |       | value |
   |       |       |       |       |       |       |       |       | pair  |
   |       |       |       |       |       |       |       |       | can   |
   |       |       |       |       |       |       |       |       | be    |
   |       |       |       |       |       |       |       |       | c     |
   |       |       |       |       |       |       |       |       | onstr |
   |       |       |       |       |       |       |       |       | ucted |
   |       |       |       |       |       |       |       |       | from  |
   |       |       |       |       |       |       |       |       | the   |
   |       |       |       |       |       |       |       |       | typ   |
   |       |       |       |       |       |       |       |       | eCode |
   |       |       |       |       |       |       |       |       | entry |
   |       |       |       |       |       |       |       |       | (     |
   |       |       |       |       |       |       |       |       | which |
   |       |       |       |       |       |       |       |       | is a  |
   |       |       |       |       |       |       |       |       | s     |
   |       |       |       |       |       |       |       |       | ingle |
   |       |       |       |       |       |       |       |       | c     |
   |       |       |       |       |       |       |       |       | ode). |
   +-------+-------+-------+-------+-------+-------+-------+-------+-------+
   | (12   | CODE  | 1     | U     |       | Im    | CD    | 1..n  | The   |
   | 6000, |       |       |       |       | age​A |       |       | first |
   | DCM,  |       |       |       |       | nnota |       |       | typ   |
   | "Im   |       |       |       |       | tion​ |       |       | eCode |
   | aging |       |       |       |       | ​Coll |       |       | entry |
   | M     |       |       |       |       | ectio |       |       | is    |
   | easur |       |       |       |       | n/​im |       |       | as    |
   | ement |       |       |       |       | age​A |       |       | sumed |
   | Rep   |       |       |       |       | nnota |       |       | to be |
   | ort") |       |       |       |       | tions |       |       | the   |
   | >     |       |       |       |       | /​Ima |       |       | pr    |
   | (12   |       |       |       |       | ge​An |       |       | imary |
   | 6010, |       |       |       |       | notat |       |       | con   |
   | DCM,  |       |       |       |       | ion/​ |       |       | cept. |
   | "Im   |       |       |       |       | calcu |       |       | Other |
   | aging |       |       |       |       | latio |       |       | typ   |
   | Meas  |       |       |       |       | n​Ent |       |       | eCode |
   | ureme |       |       |       |       | ity​C |       |       | en    |
   | nts") |       |       |       |       | ollec |       |       | tries |
   | >     |       |       |       |       | tion/ |       |       | may   |
   | (12   |       |       |       |       | ​Calc |       |       | be    |
   | 5007, |       |       |       |       | ulati |       |       | consi |
   | DCM,  |       |       |       |       | onEnt |       |       | dered |
   | "M    |       |       |       |       | ity/​ |       |       | as    |
   | easur |       |       |       |       | typeC |       |       | modif |
   | ement |       |       |       |       | ode​[ |       |       | iers, |
   | Gr    |       |       |       |       | posit |       |       | but   |
   | oup") |       |       |       |       | ion() |       |       | there |
   | >     |       |       |       |       | != 1] |       |       | is no |
   | $M    |       |       |       |       |       |       |       | sta   |
   | easur |       |       |       |       |       |       |       | ndard |
   | ement |       |       |       |       |       |       |       | o     |
   | >     |       |       |       |       |       |       |       | rder, |
   | `(    |       |       |       |       |       |       |       | so    |
   | 37012 |       |       |       |       |       |       |       | r     |
   | 9005, |       |       |       |       |       |       |       | ecogn |
   | SCT,  |       |       |       |       |       |       |       | ition |
   | "M    |       |       |       |       |       |       |       | as a  |
   | easur |       |       |       |       |       |       |       | "me   |
   | ement |       |       |       |       |       |       |       | thod" |
   | Metho |       |       |       |       |       |       |       | de    |
   | d") < |       |       |       |       |       |       |       | pends |
   | http: |       |       |       |       |       |       |       | on    |
   | //sno |       |       |       |       |       |       |       | r     |
   | med.i |       |       |       |       |       |       |       | ecogn |
   | nfo/i |       |       |       |       |       |       |       | ition |
   | d/370 |       |       |       |       |       |       |       | of    |
   | 12900 |       |       |       |       |       |       |       | spe   |
   | 5>`__ |       |       |       |       |       |       |       | cific |
   |       |       |       |       |       |       |       |       | c     |
   |       |       |       |       |       |       |       |       | odes. |
   +-------+-------+-------+-------+-------+-------+-------+-------+-------+
   | (12   | CODE  | 1     | U     |       | Im    | CD    | 1..n  | The   |
   | 6000, |       |       |       |       | age​A |       |       | first |
   | DCM,  |       |       |       |       | nnota |       |       | typ   |
   | "Im   |       |       |       |       | tion​ |       |       | eCode |
   | aging |       |       |       |       | ​Coll |       |       | entry |
   | M     |       |       |       |       | ectio |       |       | is    |
   | easur |       |       |       |       | n/​im |       |       | as    |
   | ement |       |       |       |       | age​A |       |       | sumed |
   | Rep   |       |       |       |       | nnota |       |       | to be |
   | ort") |       |       |       |       | tions |       |       | the   |
   | >     |       |       |       |       | /​Ima |       |       | pr    |
   | (12   |       |       |       |       | ge​An |       |       | imary |
   | 6010, |       |       |       |       | notat |       |       | con   |
   | DCM,  |       |       |       |       | ion/​ |       |       | cept. |
   | "Im   |       |       |       |       | calcu |       |       | Other |
   | aging |       |       |       |       | latio |       |       | typ   |
   | Meas  |       |       |       |       | n​Ent |       |       | eCode |
   | ureme |       |       |       |       | ity​C |       |       | en    |
   | nts") |       |       |       |       | ollec |       |       | tries |
   | >     |       |       |       |       | tion/ |       |       | may   |
   | (12   |       |       |       |       | ​Calc |       |       | be    |
   | 5007, |       |       |       |       | ulati |       |       | consi |
   | DCM,  |       |       |       |       | onEnt |       |       | dered |
   | "M    |       |       |       |       | ity/​ |       |       | as    |
   | easur |       |       |       |       | typeC |       |       | modif |
   | ement |       |       |       |       | ode​[ |       |       | iers, |
   | Gr    |       |       |       |       | posit |       |       | but   |
   | oup") |       |       |       |       | ion() |       |       | there |
   | >     |       |       |       |       | != 1] |       |       | is no |
   | $M    |       |       |       |       |       |       |       | sta   |
   | easur |       |       |       |       |       |       |       | ndard |
   | ement |       |       |       |       |       |       |       | o     |
   | >     |       |       |       |       |       |       |       | rder, |
   | (12   |       |       |       |       |       |       |       | so    |
   | 1401, |       |       |       |       |       |       |       | r     |
   | DCM,  |       |       |       |       |       |       |       | ecogn |
   | "De   |       |       |       |       |       |       |       | ition |
   | rivat |       |       |       |       |       |       |       | as a  |
   | ion") |       |       |       |       |       |       |       | "d    |
   |       |       |       |       |       |       |       |       | eriva |
   |       |       |       |       |       |       |       |       | tion" |
   |       |       |       |       |       |       |       |       | de    |
   |       |       |       |       |       |       |       |       | pends |
   |       |       |       |       |       |       |       |       | on    |
   |       |       |       |       |       |       |       |       | r     |
   |       |       |       |       |       |       |       |       | ecogn |
   |       |       |       |       |       |       |       |       | ition |
   |       |       |       |       |       |       |       |       | of    |
   |       |       |       |       |       |       |       |       | spe   |
   |       |       |       |       |       |       |       |       | cific |
   |       |       |       |       |       |       |       |       | c     |
   |       |       |       |       |       |       |       |       | odes. |
   +-------+-------+-------+-------+-------+-------+-------+-------+-------+
   | (12   | CODE  | 1-n   | U     |       |       |       |       | Not   |
   | 6000, |       |       |       |       |       |       |       | used  |
   | DCM,  |       |       |       |       |       |       |       | in    |
   | "Im   |       |       |       |       |       |       |       | AIM,  |
   | aging |       |       |       |       |       |       |       | since |
   | M     |       |       |       |       |       |       |       | it is |
   | easur |       |       |       |       |       |       |       | sent  |
   | ement |       |       |       |       |       |       |       | at    |
   | Rep   |       |       |       |       |       |       |       | m     |
   | ort") |       |       |       |       |       |       |       | easur |
   | >     |       |       |       |       |       |       |       | ement |
   | (12   |       |       |       |       |       |       |       | group |
   | 6010, |       |       |       |       |       |       |       | level |
   | DCM,  |       |       |       |       |       |       |       | be    |
   | "Im   |       |       |       |       |       |       |       | cause |
   | aging |       |       |       |       |       |       |       | it is |
   | Meas  |       |       |       |       |       |       |       | c     |
   | ureme |       |       |       |       |       |       |       | ommon |
   | nts") |       |       |       |       |       |       |       | to    |
   | >     |       |       |       |       |       |       |       | all   |
   | (12   |       |       |       |       |       |       |       | me    |
   | 5007, |       |       |       |       |       |       |       | asure |
   | DCM,  |       |       |       |       |       |       |       | ments |
   | "M    |       |       |       |       |       |       |       | in    |
   | easur |       |       |       |       |       |       |       | a     |
   | ement |       |       |       |       |       |       |       | nnota |
   | Gr    |       |       |       |       |       |       |       | tion. |
   | oup") |       |       |       |       |       |       |       |       |
   | >     |       |       |       |       |       |       |       |       |
   | $M    |       |       |       |       |       |       |       |       |
   | easur |       |       |       |       |       |       |       |       |
   | ement |       |       |       |       |       |       |       |       |
   | >     |       |       |       |       |       |       |       |       |
   | `(    |       |       |       |       |       |       |       |       |
   | 36369 |       |       |       |       |       |       |       |       |
   | 8007, |       |       |       |       |       |       |       |       |
   | SCT,  |       |       |       |       |       |       |       |       |
   | "Fi   |       |       |       |       |       |       |       |       |
   | nding |       |       |       |       |       |       |       |       |
   | Sit   |       |       |       |       |       |       |       |       |
   | e") < |       |       |       |       |       |       |       |       |
   | http: |       |       |       |       |       |       |       |       |
   | //sno |       |       |       |       |       |       |       |       |
   | med.i |       |       |       |       |       |       |       |       |
   | nfo/i |       |       |       |       |       |       |       |       |
   | d/363 |       |       |       |       |       |       |       |       |
   | 69800 |       |       |       |       |       |       |       |       |
   | 7>`__ |       |       |       |       |       |       |       |       |
   +-------+-------+-------+-------+-------+-------+-------+-------+-------+
   | (12   | CODE  | 1     | U     |       |       |       |       | Not   |
   | 6000, |       |       |       |       |       |       |       | used  |
   | DCM,  |       |       |       |       |       |       |       | in    |
   | "Im   |       |       |       |       |       |       |       | AIM.  |
   | aging |       |       |       |       |       |       |       |       |
   | M     |       |       |       |       |       |       |       |       |
   | easur |       |       |       |       |       |       |       |       |
   | ement |       |       |       |       |       |       |       |       |
   | Rep   |       |       |       |       |       |       |       |       |
   | ort") |       |       |       |       |       |       |       |       |
   | >     |       |       |       |       |       |       |       |       |
   | (12   |       |       |       |       |       |       |       |       |
   | 6010, |       |       |       |       |       |       |       |       |
   | DCM,  |       |       |       |       |       |       |       |       |
   | "Im   |       |       |       |       |       |       |       |       |
   | aging |       |       |       |       |       |       |       |       |
   | Meas  |       |       |       |       |       |       |       |       |
   | ureme |       |       |       |       |       |       |       |       |
   | nts") |       |       |       |       |       |       |       |       |
   | >     |       |       |       |       |       |       |       |       |
   | (12   |       |       |       |       |       |       |       |       |
   | 5007, |       |       |       |       |       |       |       |       |
   | DCM,  |       |       |       |       |       |       |       |       |
   | "M    |       |       |       |       |       |       |       |       |
   | easur |       |       |       |       |       |       |       |       |
   | ement |       |       |       |       |       |       |       |       |
   | Gr    |       |       |       |       |       |       |       |       |
   | oup") |       |       |       |       |       |       |       |       |
   | >     |       |       |       |       |       |       |       |       |
   | $M    |       |       |       |       |       |       |       |       |
   | easur |       |       |       |       |       |       |       |       |
   | ement |       |       |       |       |       |       |       |       |
   | >     |       |       |       |       |       |       |       |       |
   | `(    |       |       |       |       |       |       |       |       |
   | 36369 |       |       |       |       |       |       |       |       |
   | 8007, |       |       |       |       |       |       |       |       |
   | SCT,  |       |       |       |       |       |       |       |       |
   | "Fi   |       |       |       |       |       |       |       |       |
   | nding |       |       |       |       |       |       |       |       |
   | Sit   |       |       |       |       |       |       |       |       |
   | e") < |       |       |       |       |       |       |       |       |
   | http: |       |       |       |       |       |       |       |       |
   | //sno |       |       |       |       |       |       |       |       |
   | med.i |       |       |       |       |       |       |       |       |
   | nfo/i |       |       |       |       |       |       |       |       |
   | d/363 |       |       |       |       |       |       |       |       |
   | 69800 |       |       |       |       |       |       |       |       |
   | 7>`__ |       |       |       |       |       |       |       |       |
   | >     |       |       |       |       |       |       |       |       |
   | `(    |       |       |       |       |       |       |       |       |
   | 27274 |       |       |       |       |       |       |       |       |
   | 1003, |       |       |       |       |       |       |       |       |
   | SCT,  |       |       |       |       |       |       |       |       |
   | "Late |       |       |       |       |       |       |       |       |
   | ralit |       |       |       |       |       |       |       |       |
   | y") < |       |       |       |       |       |       |       |       |
   | http: |       |       |       |       |       |       |       |       |
   | //sno |       |       |       |       |       |       |       |       |
   | med.i |       |       |       |       |       |       |       |       |
   | nfo/i |       |       |       |       |       |       |       |       |
   | d/272 |       |       |       |       |       |       |       |       |
   | 74100 |       |       |       |       |       |       |       |       |
   | 3>`__ |       |       |       |       |       |       |       |       |
   +-------+-------+-------+-------+-------+-------+-------+-------+-------+
   | (12   | CODE  | 1     | U     |       | $Tar  |       |       | Not   |
   | 6000, |       |       |       |       | getSi |       |       | used  |
   | DCM,  |       |       |       |       | teMod |       |       | since |
   | "Im   |       |       |       |       |       |       |       | AIM   |
   | aging |       |       |       |       |       |       |       | does  |
   | M     |       |       |       |       |       |       |       | not   |
   | easur |       |       |       |       |       |       |       | have  |
   | ement |       |       |       |       |       |       |       | a     |
   | Rep   |       |       |       |       |       |       |       | mech  |
   | ort") |       |       |       |       |       |       |       | anism |
   | >     |       |       |       |       |       |       |       | for   |
   | (12   |       |       |       |       |       |       |       | po    |
   | 6010, |       |       |       |       |       |       |       | st-co |
   | DCM,  |       |       |       |       |       |       |       | ordin |
   | "Im   |       |       |       |       |       |       |       | ating |
   | aging |       |       |       |       |       |       |       | the   |
   | Meas  |       |       |       |       |       |       |       | loca  |
   | ureme |       |       |       |       |       |       |       | tion. |
   | nts") |       |       |       |       |       |       |       |       |
   | >     |       |       |       |       |       |       |       |       |
   | (12   |       |       |       |       |       |       |       |       |
   | 5007, |       |       |       |       |       |       |       |       |
   | DCM,  |       |       |       |       |       |       |       |       |
   | "M    |       |       |       |       |       |       |       |       |
   | easur |       |       |       |       |       |       |       |       |
   | ement |       |       |       |       |       |       |       |       |
   | Gr    |       |       |       |       |       |       |       |       |
   | oup") |       |       |       |       |       |       |       |       |
   | >     |       |       |       |       |       |       |       |       |
   | $M    |       |       |       |       |       |       |       |       |
   | easur |       |       |       |       |       |       |       |       |
   | ement |       |       |       |       |       |       |       |       |
   | >     |       |       |       |       |       |       |       |       |
   | `(    |       |       |       |       |       |       |       |       |
   | 36369 |       |       |       |       |       |       |       |       |
   | 8007, |       |       |       |       |       |       |       |       |
   | SCT,  |       |       |       |       |       |       |       |       |
   | "Fi   |       |       |       |       |       |       |       |       |
   | nding |       |       |       |       |       |       |       |       |
   | Sit   |       |       |       |       |       |       |       |       |
   | e") < |       |       |       |       |       |       |       |       |
   | http: |       |       |       |       |       |       |       |       |
   | //sno |       |       |       |       |       |       |       |       |
   | med.i |       |       |       |       |       |       |       |       |
   | nfo/i |       |       |       |       |       |       |       |       |
   | d/363 |       |       |       |       |       |       |       |       |
   | 69800 |       |       |       |       |       |       |       |       |
   | 7>`__ |       |       |       |       |       |       |       |       |
   | >     |       |       |       |       |       |       |       |       |
   | `(    |       |       |       |       |       |       |       |       |
   | 10623 |       |       |       |       |       |       |       |       |
   | 3006, |       |       |       |       |       |       |       |       |
   | SCT,  |       |       |       |       |       |       |       |       |
   | "Top  |       |       |       |       |       |       |       |       |
   | ograp |       |       |       |       |       |       |       |       |
   | hical |       |       |       |       |       |       |       |       |
   | mo    |       |       |       |       |       |       |       |       |
   | difie |       |       |       |       |       |       |       |       |
   | r") < |       |       |       |       |       |       |       |       |
   | http: |       |       |       |       |       |       |       |       |
   | //sno |       |       |       |       |       |       |       |       |
   | med.i |       |       |       |       |       |       |       |       |
   | nfo/i |       |       |       |       |       |       |       |       |
   | d/106 |       |       |       |       |       |       |       |       |
   | 23300 |       |       |       |       |       |       |       |       |
   | 6>`__ |       |       |       |       |       |       |       |       |
   +-------+-------+-------+-------+-------+-------+-------+-------+-------+
   | (12   | IN    | 1     | U     |       | S     |       |       |       |
   | 6000, | CLUDE |       |       |       | tatis |       |       |       |
   | DCM,  |       |       |       |       | tical |       |       |       |
   | "Im   |       |       |       |       | and   |       |       |       |
   | aging |       |       |       |       | n     |       |       |       |
   | M     |       |       |       |       | ormal |       |       |       |
   | easur |       |       |       |       | range |       |       |       |
   | ement |       |       |       |       | prope |       |       |       |
   | Rep   |       |       |       |       | rties |       |       |       |
   | ort") |       |       |       |       | are   |       |       |       |
   | >     |       |       |       |       | not   |       |       |       |
   | (12   |       |       |       |       | used  |       |       |       |
   | 6010, |       |       |       |       | in    |       |       |       |
   | DCM,  |       |       |       |       | AIM   |       |       |       |
   | "Im   |       |       |       |       | use   |       |       |       |
   | aging |       |       |       |       | cases |       |       |       |
   | Meas  |       |       |       |       | for   |       |       |       |
   | ureme |       |       |       |       | this  |       |       |       |
   | nts") |       |       |       |       | map   |       |       |       |
   | >     |       |       |       |       | ping. |       |       |       |
   | (12   |       |       |       |       |       |       |       |       |
   | 5007, |       |       |       |       |       |       |       |       |
   | DCM,  |       |       |       |       |       |       |       |       |
   | "M    |       |       |       |       |       |       |       |       |
   | easur |       |       |       |       |       |       |       |       |
   | ement |       |       |       |       |       |       |       |       |
   | Gr    |       |       |       |       |       |       |       |       |
   | oup") |       |       |       |       |       |       |       |       |
   | >     |       |       |       |       |       |       |       |       |
   | $M    |       |       |       |       |       |       |       |       |
   | easur |       |       |       |       |       |       |       |       |
   | ement |       |       |       |       |       |       |       |       |
   | >     |       |       |       |       |       |       |       |       |
   +-------+-------+-------+-------+-------+-------+-------+-------+-------+
   | (12   | NUM   | 1-n   | UC    |       |       |       |       | Not   |
   | 6000, |       |       |       |       |       |       |       | used  |
   | DCM,  |       |       |       |       |       |       |       | in    |
   | "Im   |       |       |       |       |       |       |       | AIM   |
   | aging |       |       |       |       |       |       |       | for   |
   | M     |       |       |       |       |       |       |       | our   |
   | easur |       |       |       |       |       |       |       | use   |
   | ement |       |       |       |       |       |       |       | c     |
   | Rep   |       |       |       |       |       |       |       | ases. |
   | ort") |       |       |       |       |       |       |       |       |
   | >     |       |       |       |       |       |       |       |       |
   | (12   |       |       |       |       |       |       |       |       |
   | 6010, |       |       |       |       |       |       |       |       |
   | DCM,  |       |       |       |       |       |       |       |       |
   | "Im   |       |       |       |       |       |       |       |       |
   | aging |       |       |       |       |       |       |       |       |
   | Meas  |       |       |       |       |       |       |       |       |
   | ureme |       |       |       |       |       |       |       |       |
   | nts") |       |       |       |       |       |       |       |       |
   | >     |       |       |       |       |       |       |       |       |
   | (12   |       |       |       |       |       |       |       |       |
   | 5007, |       |       |       |       |       |       |       |       |
   | DCM,  |       |       |       |       |       |       |       |       |
   | "M    |       |       |       |       |       |       |       |       |
   | easur |       |       |       |       |       |       |       |       |
   | ement |       |       |       |       |       |       |       |       |
   | Gr    |       |       |       |       |       |       |       |       |
   | oup") |       |       |       |       |       |       |       |       |
   | >     |       |       |       |       |       |       |       |       |
   | $M    |       |       |       |       |       |       |       |       |
   | easur |       |       |       |       |       |       |       |       |
   | ement |       |       |       |       |       |       |       |       |
   | >     |       |       |       |       |       |       |       |       |
   | $Deri |       |       |       |       |       |       |       |       |
   | vatio |       |       |       |       |       |       |       |       |
   | nPara |       |       |       |       |       |       |       |       |
   | meter |       |       |       |       |       |       |       |       |
   +-------+-------+-------+-------+-------+-------+-------+-------+-------+
   | (12   | NUM   | 1-n   | UC    |       |       |       |       | Not   |
   | 6000, |       |       |       |       |       |       |       | used  |
   | DCM,  |       |       |       |       |       |       |       | in    |
   | "Im   |       |       |       |       |       |       |       | AIM   |
   | aging |       |       |       |       |       |       |       | for   |
   | M     |       |       |       |       |       |       |       | our   |
   | easur |       |       |       |       |       |       |       | use   |
   | ement |       |       |       |       |       |       |       | c     |
   | Rep   |       |       |       |       |       |       |       | ases. |
   | ort") |       |       |       |       |       |       |       |       |
   | >     |       |       |       |       |       |       |       |       |
   | (12   |       |       |       |       |       |       |       |       |
   | 6010, |       |       |       |       |       |       |       |       |
   | DCM,  |       |       |       |       |       |       |       |       |
   | "Im   |       |       |       |       |       |       |       |       |
   | aging |       |       |       |       |       |       |       |       |
   | Meas  |       |       |       |       |       |       |       |       |
   | ureme |       |       |       |       |       |       |       |       |
   | nts") |       |       |       |       |       |       |       |       |
   | >     |       |       |       |       |       |       |       |       |
   | (12   |       |       |       |       |       |       |       |       |
   | 5007, |       |       |       |       |       |       |       |       |
   | DCM,  |       |       |       |       |       |       |       |       |
   | "M    |       |       |       |       |       |       |       |       |
   | easur |       |       |       |       |       |       |       |       |
   | ement |       |       |       |       |       |       |       |       |
   | Gr    |       |       |       |       |       |       |       |       |
   | oup") |       |       |       |       |       |       |       |       |
   | >     |       |       |       |       |       |       |       |       |
   | $M    |       |       |       |       |       |       |       |       |
   | easur |       |       |       |       |       |       |       |       |
   | ement |       |       |       |       |       |       |       |       |
   | >     |       |       |       |       |       |       |       |       |
   | $Deri |       |       |       |       |       |       |       |       |
   | vatio |       |       |       |       |       |       |       |       |
   | nPara |       |       |       |       |       |       |       |       |
   | meter |       |       |       |       |       |       |       |       |
   +-------+-------+-------+-------+-------+-------+-------+-------+-------+
   | (12   | IN    | 1     | UC    |       | B     |       |       |       |
   | 6000, | CLUDE |       |       |       | eyond |       |       |       |
   | DCM,  |       |       |       |       | the   |       |       |       |
   | "Im   |       |       |       |       | scope |       |       |       |
   | aging |       |       |       |       | of    |       |       |       |
   | M     |       |       |       |       | our   |       |       |       |
   | easur |       |       |       |       | use   |       |       |       |
   | ement |       |       |       |       | cases |       |       |       |
   | Rep   |       |       |       |       | to    |       |       |       |
   | ort") |       |       |       |       | map.  |       |       |       |
   | >     |       |       |       |       |       |       |       |       |
   | (12   |       |       |       |       |       |       |       |       |
   | 6010, |       |       |       |       |       |       |       |       |
   | DCM,  |       |       |       |       |       |       |       |       |
   | "Im   |       |       |       |       |       |       |       |       |
   | aging |       |       |       |       |       |       |       |       |
   | Meas  |       |       |       |       |       |       |       |       |
   | ureme |       |       |       |       |       |       |       |       |
   | nts") |       |       |       |       |       |       |       |       |
   | >     |       |       |       |       |       |       |       |       |
   | (12   |       |       |       |       |       |       |       |       |
   | 5007, |       |       |       |       |       |       |       |       |
   | DCM,  |       |       |       |       |       |       |       |       |
   | "M    |       |       |       |       |       |       |       |       |
   | easur |       |       |       |       |       |       |       |       |
   | ement |       |       |       |       |       |       |       |       |
   | Gr    |       |       |       |       |       |       |       |       |
   | oup") |       |       |       |       |       |       |       |       |
   | >     |       |       |       |       |       |       |       |       |
   | $M    |       |       |       |       |       |       |       |       |
   | easur |       |       |       |       |       |       |       |       |
   | ement |       |       |       |       |       |       |       |       |
   | >     |       |       |       |       |       |       |       |       |
   +-------+-------+-------+-------+-------+-------+-------+-------+-------+
   | (12   | TEXT  | 1     | UC    |       |       |       |       | B     |
   | 6000, |       |       |       |       |       |       |       | eyond |
   | DCM,  |       |       |       |       |       |       |       | the   |
   | "Im   |       |       |       |       |       |       |       | scope |
   | aging |       |       |       |       |       |       |       | of    |
   | M     |       |       |       |       |       |       |       | our   |
   | easur |       |       |       |       |       |       |       | use   |
   | ement |       |       |       |       |       |       |       | cases |
   | Rep   |       |       |       |       |       |       |       | to    |
   | ort") |       |       |       |       |       |       |       | map.  |
   | >     |       |       |       |       |       |       |       |       |
   | (12   |       |       |       |       |       |       |       |       |
   | 6010, |       |       |       |       |       |       |       |       |
   | DCM,  |       |       |       |       |       |       |       |       |
   | "Im   |       |       |       |       |       |       |       |       |
   | aging |       |       |       |       |       |       |       |       |
   | Meas  |       |       |       |       |       |       |       |       |
   | ureme |       |       |       |       |       |       |       |       |
   | nts") |       |       |       |       |       |       |       |       |
   | >     |       |       |       |       |       |       |       |       |
   | (12   |       |       |       |       |       |       |       |       |
   | 5007, |       |       |       |       |       |       |       |       |
   | DCM,  |       |       |       |       |       |       |       |       |
   | "M    |       |       |       |       |       |       |       |       |
   | easur |       |       |       |       |       |       |       |       |
   | ement |       |       |       |       |       |       |       |       |
   | Gr    |       |       |       |       |       |       |       |       |
   | oup") |       |       |       |       |       |       |       |       |
   | >     |       |       |       |       |       |       |       |       |
   | $M    |       |       |       |       |       |       |       |       |
   | easur |       |       |       |       |       |       |       |       |
   | ement |       |       |       |       |       |       |       |       |
   | >     |       |       |       |       |       |       |       |       |
   | TEXT  |       |       |       |       |       |       |       |       |
   +-------+-------+-------+-------+-------+-------+-------+-------+-------+
   | (12   | IN    | 1-n   | U     | `Ma   |       |       |       |       |
   | 6000, | CLUDE |       |       | pping |       |       |       |       |
   | DCM,  |       |       |       | of    |       |       |       |       |
   | "Im   |       |       |       | Image |       |       |       |       |
   | aging |       |       |       | or    |       |       |       |       |
   | M     |       |       |       | Sp    |       |       |       |       |
   | easur |       |       |       | atial |       |       |       |       |
   | ement |       |       |       | Coo   |       |       |       |       |
   | Rep   |       |       |       | rdina |       |       |       |       |
   | ort") |       |       |       | tes < |       |       |       |       |
   | >     |       |       |       | #sect |       |       |       |       |
   | (12   |       |       |       | _Mapp |       |       |       |       |
   | 6010, |       |       |       | ing_T |       |       |       |       |
   | DCM,  |       |       |       | ID_32 |       |       |       |       |
   | "Im   |       |       |       | 0>`__ |       |       |       |       |
   | aging |       |       |       |       |       |       |       |       |
   | Meas  |       |       |       |       |       |       |       |       |
   | ureme |       |       |       |       |       |       |       |       |
   | nts") |       |       |       |       |       |       |       |       |
   | >     |       |       |       |       |       |       |       |       |
   | (12   |       |       |       |       |       |       |       |       |
   | 5007, |       |       |       |       |       |       |       |       |
   | DCM,  |       |       |       |       |       |       |       |       |
   | "M    |       |       |       |       |       |       |       |       |
   | easur |       |       |       |       |       |       |       |       |
   | ement |       |       |       |       |       |       |       |       |
   | Gr    |       |       |       |       |       |       |       |       |
   | oup") |       |       |       |       |       |       |       |       |
   | >     |       |       |       |       |       |       |       |       |
   | $M    |       |       |       |       |       |       |       |       |
   | easur |       |       |       |       |       |       |       |       |
   | ement |       |       |       |       |       |       |       |       |
   | >     |       |       |       |       |       |       |       |       |
   | $Im   |       |       |       |       |       |       |       |       |
   | agePu |       |       |       |       |       |       |       |       |
   | rpose |       |       |       |       |       |       |       |       |
   +-------+-------+-------+-------+-------+-------+-------+-------+-------+
   | (12   | IN    | 1-n   | U     |       | Not   |       |       |       |
   | 6000, | CLUDE |       |       |       | used  |       |       |       |
   | DCM,  |       |       |       |       | in    |       |       |       |
   | "Im   |       |       |       |       | our   |       |       |       |
   | aging |       |       |       |       | AIM   |       |       |       |
   | M     |       |       |       |       | use   |       |       |       |
   | easur |       |       |       |       | c     |       |       |       |
   | ement |       |       |       |       | ases. |       |       |       |
   | Rep   |       |       |       |       |       |       |       |       |
   | ort") |       |       |       |       |       |       |       |       |
   | >     |       |       |       |       |       |       |       |       |
   | (12   |       |       |       |       |       |       |       |       |
   | 6010, |       |       |       |       |       |       |       |       |
   | DCM,  |       |       |       |       |       |       |       |       |
   | "Im   |       |       |       |       |       |       |       |       |
   | aging |       |       |       |       |       |       |       |       |
   | Meas  |       |       |       |       |       |       |       |       |
   | ureme |       |       |       |       |       |       |       |       |
   | nts") |       |       |       |       |       |       |       |       |
   | >     |       |       |       |       |       |       |       |       |
   | (12   |       |       |       |       |       |       |       |       |
   | 5007, |       |       |       |       |       |       |       |       |
   | DCM,  |       |       |       |       |       |       |       |       |
   | "M    |       |       |       |       |       |       |       |       |
   | easur |       |       |       |       |       |       |       |       |
   | ement |       |       |       |       |       |       |       |       |
   | Gr    |       |       |       |       |       |       |       |       |
   | oup") |       |       |       |       |       |       |       |       |
   | >     |       |       |       |       |       |       |       |       |
   | $M    |       |       |       |       |       |       |       |       |
   | easur |       |       |       |       |       |       |       |       |
   | ement |       |       |       |       |       |       |       |       |
   | >     |       |       |       |       |       |       |       |       |
   | $W    |       |       |       |       |       |       |       |       |
   | avePu |       |       |       |       |       |       |       |       |
   | rpose |       |       |       |       |       |       |       |       |
   +-------+-------+-------+-------+-------+-------+-------+-------+-------+
   | (12   | IN    | 1     | U     |       | Not   |       |       |       |
   | 6000, | CLUDE |       |       |       | used  |       |       |       |
   | DCM,  |       |       |       |       | in    |       |       |       |
   | "Im   |       |       |       |       | our   |       |       |       |
   | aging |       |       |       |       | AIM   |       |       |       |
   | M     |       |       |       |       | use   |       |       |       |
   | easur |       |       |       |       | c     |       |       |       |
   | ement |       |       |       |       | ases. |       |       |       |
   | Rep   |       |       |       |       |       |       |       |       |
   | ort") |       |       |       |       |       |       |       |       |
   | >     |       |       |       |       |       |       |       |       |
   | (12   |       |       |       |       |       |       |       |       |
   | 6010, |       |       |       |       |       |       |       |       |
   | DCM,  |       |       |       |       |       |       |       |       |
   | "Im   |       |       |       |       |       |       |       |       |
   | aging |       |       |       |       |       |       |       |       |
   | Meas  |       |       |       |       |       |       |       |       |
   | ureme |       |       |       |       |       |       |       |       |
   | nts") |       |       |       |       |       |       |       |       |
   | >     |       |       |       |       |       |       |       |       |
   | (12   |       |       |       |       |       |       |       |       |
   | 5007, |       |       |       |       |       |       |       |       |
   | DCM,  |       |       |       |       |       |       |       |       |
   | "M    |       |       |       |       |       |       |       |       |
   | easur |       |       |       |       |       |       |       |       |
   | ement |       |       |       |       |       |       |       |       |
   | Gr    |       |       |       |       |       |       |       |       |
   | oup") |       |       |       |       |       |       |       |       |
   | >     |       |       |       |       |       |       |       |       |
   | $M    |       |       |       |       |       |       |       |       |
   | easur |       |       |       |       |       |       |       |       |
   | ement |       |       |       |       |       |       |       |       |
   | >     |       |       |       |       |       |       |       |       |
   +-------+-------+-------+-------+-------+-------+-------+-------+-------+
   | (12   | TEXT  | 1     | U     |       |       |       |       | Not   |
   | 6000, |       |       |       |       |       |       |       | used  |
   | DCM,  |       |       |       |       |       |       |       | in    |
   | "Im   |       |       |       |       |       |       |       | AIM   |
   | aging |       |       |       |       |       |       |       |       |
   | M     |       |       |       |       |       |       |       |       |
   | easur |       |       |       |       |       |       |       |       |
   | ement |       |       |       |       |       |       |       |       |
   | Rep   |       |       |       |       |       |       |       |       |
   | ort") |       |       |       |       |       |       |       |       |
   | >     |       |       |       |       |       |       |       |       |
   | (12   |       |       |       |       |       |       |       |       |
   | 6010, |       |       |       |       |       |       |       |       |
   | DCM,  |       |       |       |       |       |       |       |       |
   | "Im   |       |       |       |       |       |       |       |       |
   | aging |       |       |       |       |       |       |       |       |
   | Meas  |       |       |       |       |       |       |       |       |
   | ureme |       |       |       |       |       |       |       |       |
   | nts") |       |       |       |       |       |       |       |       |
   | >     |       |       |       |       |       |       |       |       |
   | (12   |       |       |       |       |       |       |       |       |
   | 5007, |       |       |       |       |       |       |       |       |
   | DCM,  |       |       |       |       |       |       |       |       |
   | "M    |       |       |       |       |       |       |       |       |
   | easur |       |       |       |       |       |       |       |       |
   | ement |       |       |       |       |       |       |       |       |
   | Gr    |       |       |       |       |       |       |       |       |
   | oup") |       |       |       |       |       |       |       |       |
   | >     |       |       |       |       |       |       |       |       |
   | $M    |       |       |       |       |       |       |       |       |
   | easur |       |       |       |       |       |       |       |       |
   | ement |       |       |       |       |       |       |       |       |
   | >     |       |       |       |       |       |       |       |       |
   | (12   |       |       |       |       |       |       |       |       |
   | 1050, |       |       |       |       |       |       |       |       |
   | DCM,  |       |       |       |       |       |       |       |       |
   | "     |       |       |       |       |       |       |       |       |
   | Equiv |       |       |       |       |       |       |       |       |
   | alent |       |       |       |       |       |       |       |       |
   | Me    |       |       |       |       |       |       |       |       |
   | aning |       |       |       |       |       |       |       |       |
   | of    |       |       |       |       |       |       |       |       |
   | Co    |       |       |       |       |       |       |       |       |
   | ncept |       |       |       |       |       |       |       |       |
   | N     |       |       |       |       |       |       |       |       |
   | ame") |       |       |       |       |       |       |       |       |
   +-------+-------+-------+-------+-------+-------+-------+-------+-------+
   | (12   | IN    | 1     | U     | `Ma   | Not   |       |       |       |
   | 6000, | CLUDE |       |       | pping | m     |       |       |       |
   | DCM,  |       |       |       | of    | apped |       |       |       |
   | "Im   |       |       |       | Tra   | at    |       |       |       |
   | aging |       |       |       | cking | this  |       |       |       |
   | M     |       |       |       | Ide   | level |       |       |       |
   | easur |       |       |       | ntifi | for   |       |       |       |
   | ement |       |       |       | er <# | TID   |       |       |       |
   | Rep   |       |       |       | sect_ | 1500, |       |       |       |
   | ort") |       |       |       | Mappi | but   |       |       |       |
   | >     |       |       |       | ng_TI | r     |       |       |       |
   | (12   |       |       |       | D_410 | ather |       |       |       |
   | 6010, |       |       |       | 8>`__ | at    |       |       |       |
   | DCM,  |       |       |       |       | the   |       |       |       |
   | "Im   |       |       |       |       | M     |       |       |       |
   | aging |       |       |       |       | easur |       |       |       |
   | Meas  |       |       |       |       | ement |       |       |       |
   | ureme |       |       |       |       | Group |       |       |       |
   | nts") |       |       |       |       | level |       |       |       |
   | >     |       |       |       |       | in    |       |       |       |
   | (12   |       |       |       |       | TID   |       |       |       |
   | 5007, |       |       |       |       | 1501. |       |       |       |
   | DCM,  |       |       |       |       |       |       |       |       |
   | "M    |       |       |       |       |       |       |       |       |
   | easur |       |       |       |       |       |       |       |       |
   | ement |       |       |       |       |       |       |       |       |
   | Gr    |       |       |       |       |       |       |       |       |
   | oup") |       |       |       |       |       |       |       |       |
   | >     |       |       |       |       |       |       |       |       |
   | $M    |       |       |       |       |       |       |       |       |
   | easur |       |       |       |       |       |       |       |       |
   | ement |       |       |       |       |       |       |       |       |
   | >     |       |       |       |       |       |       |       |       |
   +-------+-------+-------+-------+-------+-------+-------+-------+-------+
   | (12   | COMP  | 1     | U     |       |       |       |       | Not   |
   | 6000, | OSITE |       |       |       |       |       |       | used  |
   | DCM,  |       |       |       |       |       |       |       | in    |
   | "Im   |       |       |       |       |       |       |       | AIM.  |
   | aging |       |       |       |       |       |       |       |       |
   | M     |       |       |       |       |       |       |       |       |
   | easur |       |       |       |       |       |       |       |       |
   | ement |       |       |       |       |       |       |       |       |
   | Rep   |       |       |       |       |       |       |       |       |
   | ort") |       |       |       |       |       |       |       |       |
   | >     |       |       |       |       |       |       |       |       |
   | (12   |       |       |       |       |       |       |       |       |
   | 6010, |       |       |       |       |       |       |       |       |
   | DCM,  |       |       |       |       |       |       |       |       |
   | "Im   |       |       |       |       |       |       |       |       |
   | aging |       |       |       |       |       |       |       |       |
   | Meas  |       |       |       |       |       |       |       |       |
   | ureme |       |       |       |       |       |       |       |       |
   | nts") |       |       |       |       |       |       |       |       |
   | >     |       |       |       |       |       |       |       |       |
   | (12   |       |       |       |       |       |       |       |       |
   | 5007, |       |       |       |       |       |       |       |       |
   | DCM,  |       |       |       |       |       |       |       |       |
   | "M    |       |       |       |       |       |       |       |       |
   | easur |       |       |       |       |       |       |       |       |
   | ement |       |       |       |       |       |       |       |       |
   | Gr    |       |       |       |       |       |       |       |       |
   | oup") |       |       |       |       |       |       |       |       |
   | >     |       |       |       |       |       |       |       |       |
   | $M    |       |       |       |       |       |       |       |       |
   | easur |       |       |       |       |       |       |       |       |
   | ement |       |       |       |       |       |       |       |       |
   | >     |       |       |       |       |       |       |       |       |
   | (12   |       |       |       |       |       |       |       |       |
   | 6100, |       |       |       |       |       |       |       |       |
   | DCM,  |       |       |       |       |       |       |       |       |
   | "Real |       |       |       |       |       |       |       |       |
   | World |       |       |       |       |       |       |       |       |
   | Value |       |       |       |       |       |       |       |       |
   | Map   |       |       |       |       |       |       |       |       |
   | used  |       |       |       |       |       |       |       |       |
   | for   |       |       |       |       |       |       |       |       |
   | mea   |       |       |       |       |       |       |       |       |
   | surem |       |       |       |       |       |       |       |       |
   | ent") |       |       |       |       |       |       |       |       |
   +-------+-------+-------+-------+-------+-------+-------+-------+-------+
   | (12   | IN    | 1     | U     | `Ma   |       |       |       |       |
   | 6000, | CLUDE |       |       | pping |       |       |       |       |
   | DCM,  |       |       |       | of    |       |       |       |       |
   | "Im   |       |       |       | Algo  |       |       |       |       |
   | aging |       |       |       | rithm |       |       |       |       |
   | M     |       |       |       | Id    |       |       |       |       |
   | easur |       |       |       | entif |       |       |       |       |
   | ement |       |       |       | icati |       |       |       |       |
   | Rep   |       |       |       | on <# |       |       |       |       |
   | ort") |       |       |       | sect_ |       |       |       |       |
   | >     |       |       |       | Mappi |       |       |       |       |
   | (12   |       |       |       | ng_TI |       |       |       |       |
   | 6010, |       |       |       | D_401 |       |       |       |       |
   | DCM,  |       |       |       | 9>`__ |       |       |       |       |
   | "Im   |       |       |       |       |       |       |       |       |
   | aging |       |       |       |       |       |       |       |       |
   | Meas  |       |       |       |       |       |       |       |       |
   | ureme |       |       |       |       |       |       |       |       |
   | nts") |       |       |       |       |       |       |       |       |
   | >     |       |       |       |       |       |       |       |       |
   | (12   |       |       |       |       |       |       |       |       |
   | 5007, |       |       |       |       |       |       |       |       |
   | DCM,  |       |       |       |       |       |       |       |       |
   | "M    |       |       |       |       |       |       |       |       |
   | easur |       |       |       |       |       |       |       |       |
   | ement |       |       |       |       |       |       |       |       |
   | Gr    |       |       |       |       |       |       |       |       |
   | oup") |       |       |       |       |       |       |       |       |
   | >     |       |       |       |       |       |       |       |       |
   | $M    |       |       |       |       |       |       |       |       |
   | easur |       |       |       |       |       |       |       |       |
   | ement |       |       |       |       |       |       |       |       |
   | >     |       |       |       |       |       |       |       |       |
   +-------+-------+-------+-------+-------+-------+-------+-------+-------+

.. _sect_Mapping_TID_320:

Mapping of Image or Spatial Coordinates
'''''''''''''''''''''''''''''''''''''''

This section describes the mapping of .

.. table:: Mapping of Image or Spatial Coordinates

   +-------+-------+-------+-------+-------+-------+-------+-------+-------+
   | DICOM | DICOM | DICOM | DICOM | Gene  | AIM   | AIM   | AIM   | Co    |
   | SR    | VT    | VM    | Usage | rated | El    | Data  | Mu    | mment |
   | Path  |       |       | Type  | Value | ement | Type  | ltipl |       |
   |       |       |       |       |       | or    |       | icity |       |
   |       |       |       |       |       | Attr  |       |       |       |
   |       |       |       |       |       | ibute |       |       |       |
   +=======+=======+=======+=======+=======+=======+=======+=======+=======+
   | (12   | IMAGE | 1     | MC    |       | Ima   | II,   | 1,    | An    |
   | 6000, |       |       |       |       | ge​An | INT   | 0..1  | e     |
   | DCM,  |       |       |       |       | notat |       |       | ntire |
   | "Im   |       |       |       |       | ion​​ |       |       | image |
   | aging |       |       |       |       | Colle |       |       | refe  |
   | M     |       |       |       |       | ction |       |       | rence |
   | easur |       |       |       |       | /​ima |       |       | wi    |
   | ement |       |       |       |       | ge​An |       |       | thout |
   | Rep   |       |       |       |       | notat |       |       | sp    |
   | ort") |       |       |       |       | ions/ |       |       | atial |
   | >     |       |       |       |       | ​Imag |       |       | c     |
   | (12   |       |       |       |       | e​Ann |       |       | oordi |
   | 6010, |       |       |       |       | otati |       |       | nates |
   | DCM,  |       |       |       |       | on/​​ |       |       |       |
   | "Im   |       |       |       |       | marku |       |       | The   |
   | aging |       |       |       |       | p​Ent |       |       | Refer |
   | Meas  |       |       |       |       | ity​C |       |       | enced |
   | ureme |       |       |       |       | ollec |       |       | SOP   |
   | nts") |       |       |       |       | tion/ |       |       | Class |
   | >     |       |       |       |       | ​Mark |       |       | UID   |
   | (12   |       |       |       |       | upEnt |       |       | is    |
   | 5007, |       |       |       |       | ity/​ |       |       | obt   |
   | DCM,  |       |       |       |       | image |       |       | ained |
   | "M    |       |       |       |       | Refer |       |       | from  |
   | easur |       |       |       |       | enceU |       |       | ima   |
   | ement |       |       |       |       | id/​@ |       |       | geRef |
   | Gr    |       |       |       |       | root, |       |       | erenc |
   | oup") |       |       |       |       | refe  |       |       | e​Ent |
   | >     |       |       |       |       | rence |       |       | ity​C |
   | $Pu   |       |       |       |       | dFram |       |       | ollec |
   | rpose |       |       |       |       | eNumb |       |       | tion; |
   |       |       |       |       |       | er/​@ |       |       | see   |
   |       |       |       |       |       | value |       |       | `tabl |
   |       |       |       |       |       |       |       |       | e_tit |
   |       |       |       |       |       |       |       |       | le <# |
   |       |       |       |       |       |       |       |       | table |
   |       |       |       |       |       |       |       |       | _A.8- |
   |       |       |       |       |       |       |       |       | 5>`__ |
   |       |       |       |       |       |       |       |       |       |
   |       |       |       |       |       |       |       |       | Only  |
   |       |       |       |       |       |       |       |       | the   |
   |       |       |       |       |       |       |       |       | by-   |
   |       |       |       |       |       |       |       |       | value |
   |       |       |       |       |       |       |       |       | (SEL  |
   |       |       |       |       |       |       |       |       | ECTED |
   |       |       |       |       |       |       |       |       | FROM) |
   |       |       |       |       |       |       |       |       | re    |
   |       |       |       |       |       |       |       |       | latio |
   |       |       |       |       |       |       |       |       | nship |
   |       |       |       |       |       |       |       |       | is    |
   |       |       |       |       |       |       |       |       | used, |
   |       |       |       |       |       |       |       |       | not   |
   |       |       |       |       |       |       |       |       | the   |
   |       |       |       |       |       |       |       |       | by    |
   |       |       |       |       |       |       |       |       | -refe |
   |       |       |       |       |       |       |       |       | rence |
   |       |       |       |       |       |       |       |       | (     |
   |       |       |       |       |       |       |       |       | R-SEL |
   |       |       |       |       |       |       |       |       | ECTED |
   |       |       |       |       |       |       |       |       | FROM) |
   |       |       |       |       |       |       |       |       | rel   |
   |       |       |       |       |       |       |       |       | ation |
   |       |       |       |       |       |       |       |       | ship. |
   +-------+-------+-------+-------+-------+-------+-------+-------+-------+
   | (12   | S     | 1     | MC    |       | Im    | REAL  | 1..n  | A     |
   | 6000, | COORD |       |       |       | age​A |       |       | refe  |
   | DCM,  |       |       |       |       | nnota |       |       | rence |
   | "Im   |       |       |       |       | tion​ |       |       | to    |
   | aging |       |       |       |       | ​Coll |       |       | c     |
   | M     |       |       |       |       | ectio |       |       | oordi |
   | easur |       |       |       |       | n/​im |       |       | nates |
   | ement |       |       |       |       | age​A |       |       | on an |
   | Rep   |       |       |       |       | nnota |       |       | i     |
   | ort") |       |       |       |       | tions |       |       | mage. |
   | >     |       |       |       |       | /​Ima |       |       |       |
   | (12   |       |       |       |       | ge​An |       |       | The   |
   | 6010, |       |       |       |       | notat |       |       | value |
   | DCM,  |       |       |       |       | ion/​ |       |       | of    |
   | "Im   |       |       |       |       | ​mark |       |       | aim:  |
   | aging |       |       |       |       | up​En |       |       | ​Mark |
   | Meas  |       |       |       |       | tity​ |       |       | up​En |
   | ureme |       |       |       |       | Colle |       |       | tity/ |
   | nts") |       |       |       |       | ction |       |       | ​aim: |
   | >     |       |       |       |       | /​Mar |       |       | ​uniq |
   | (12   |       |       |       |       | kupEn |       |       | ue​Id |
   | 5007, |       |       |       |       | tity/ |       |       | entif |
   | DCM,  |       |       |       |       | ​twoD |       |       | ier/​ |
   | "M    |       |       |       |       | imens |       |       | @root |
   | easur |       |       |       |       | ion​S |       |       | is    |
   | ement |       |       |       |       | patia |       |       | m     |
   | Gr    |       |       |       |       | lCoor |       |       | apped |
   | oup") |       |       |       |       | dinat |       |       | to    |
   | >     |       |       |       |       | e​​Co |       |       | the   |
   | $Pu   |       |       |       |       | llect |       |       | Obser |
   | rpose |       |       |       |       | ion/​ |       |       | vatio |
   |       |       |       |       |       | TwoDi |       |       | n​UID |
   |       |       |       |       |       | mensi |       |       | Attr  |
   |       |       |       |       |       | on​Sp |       |       | ibute |
   |       |       |       |       |       | atial |       |       | of    |
   |       |       |       |       |       | Coord |       |       | the   |
   |       |       |       |       |       | inate |       |       | SC    |
   |       |       |       |       |       |       |       |       | OORD. |
   |       |       |       |       |       |       |       |       |       |
   |       |       |       |       |       |       |       |       | One   |
   |       |       |       |       |       |       |       |       | or    |
   |       |       |       |       |       |       |       |       | more  |
   |       |       |       |       |       |       |       |       | Ma    |
   |       |       |       |       |       |       |       |       | rkupE |
   |       |       |       |       |       |       |       |       | ntity |
   |       |       |       |       |       |       |       |       | inst  |
   |       |       |       |       |       |       |       |       | ances |
   |       |       |       |       |       |       |       |       | w     |
   |       |       |       |       |       |       |       |       | ithin |
   |       |       |       |       |       |       |       |       | an    |
   |       |       |       |       |       |       |       |       | I     |
   |       |       |       |       |       |       |       |       | mage​ |
   |       |       |       |       |       |       |       |       | Annot |
   |       |       |       |       |       |       |       |       | ation |
   |       |       |       |       |       |       |       |       | ins   |
   |       |       |       |       |       |       |       |       | tance |
   |       |       |       |       |       |       |       |       | may   |
   |       |       |       |       |       |       |       |       | be    |
   |       |       |       |       |       |       |       |       | c     |
   |       |       |       |       |       |       |       |       | onstr |
   |       |       |       |       |       |       |       |       | ained |
   |       |       |       |       |       |       |       |       | to be |
   |       |       |       |       |       |       |       |       | assoc |
   |       |       |       |       |       |       |       |       | iated |
   |       |       |       |       |       |       |       |       | with  |
   |       |       |       |       |       |       |       |       | parti |
   |       |       |       |       |       |       |       |       | cular |
   |       |       |       |       |       |       |       |       | NUM   |
   |       |       |       |       |       |       |       |       | meas  |
   |       |       |       |       |       |       |       |       | ureme |
   |       |       |       |       |       |       |       |       | nt(s) |
   |       |       |       |       |       |       |       |       | in    |
   |       |       |       |       |       |       |       |       | the   |
   |       |       |       |       |       |       |       |       | inc   |
   |       |       |       |       |       |       |       |       | luded |
   |       |       |       |       |       |       |       |       | TID   |
   |       |       |       |       |       |       |       |       | 1419  |
   |       |       |       |       |       |       |       |       | by a  |
   |       |       |       |       |       |       |       |       | Calc  |
   |       |       |       |       |       |       |       |       | ulati |
   |       |       |       |       |       |       |       |       | on​En |
   |       |       |       |       |       |       |       |       | tity​ |
   |       |       |       |       |       |       |       |       | Refer |
   |       |       |       |       |       |       |       |       | ences |
   |       |       |       |       |       |       |       |       | ​Mark |
   |       |       |       |       |       |       |       |       | up​En |
   |       |       |       |       |       |       |       |       | tity​ |
   |       |       |       |       |       |       |       |       | State |
   |       |       |       |       |       |       |       |       | ment. |
   +-------+-------+-------+-------+-------+-------+-------+-------+-------+
   | (12   | IMAGE | 1     | M     |       | Ima   | II,   | 1,    | The   |
   | 6000, |       |       |       |       | ge​An | INT   | 0..1  | Refer |
   | DCM,  |       |       |       |       | notat |       |       | enced |
   | "Im   |       |       |       |       | ion​​ |       |       | SOP   |
   | aging |       |       |       |       | Colle |       |       | Class |
   | M     |       |       |       |       | ction |       |       | UID   |
   | easur |       |       |       |       | /​ima |       |       | is    |
   | ement |       |       |       |       | ge​An |       |       | obt   |
   | Rep   |       |       |       |       | notat |       |       | ained |
   | ort") |       |       |       |       | ions/ |       |       | from  |
   | >     |       |       |       |       | ​Imag |       |       | ima   |
   | (12   |       |       |       |       | e​Ann |       |       | geRef |
   | 6010, |       |       |       |       | otati |       |       | erenc |
   | DCM,  |       |       |       |       | on/​​ |       |       | e​Ent |
   | "Im   |       |       |       |       | marku |       |       | ity​C |
   | aging |       |       |       |       | p​Ent |       |       | ollec |
   | Meas  |       |       |       |       | ity​C |       |       | tion; |
   | ureme |       |       |       |       | ollec |       |       | see   |
   | nts") |       |       |       |       | tion/ |       |       | `tabl |
   | >     |       |       |       |       | ​Mark |       |       | e_tit |
   | (12   |       |       |       |       | upEnt |       |       | le <# |
   | 5007, |       |       |       |       | ity/​ |       |       | table |
   | DCM,  |       |       |       |       | image |       |       | _A.8- |
   | "M    |       |       |       |       | Refer |       |       | 5>`__ |
   | easur |       |       |       |       | enceU |       |       |       |
   | ement |       |       |       |       | id/​@ |       |       | Only  |
   | Gr    |       |       |       |       | root, |       |       | the   |
   | oup") |       |       |       |       | refe  |       |       | by-   |
   | >     |       |       |       |       | rence |       |       | value |
   | $Pu   |       |       |       |       | dFram |       |       | (SEL  |
   | rpose |       |       |       |       | eNumb |       |       | ECTED |
   | >     |       |       |       |       | er/​@ |       |       | FROM) |
   | IMAGE |       |       |       |       | value |       |       | re    |
   |       |       |       |       |       |       |       |       | latio |
   |       |       |       |       |       |       |       |       | nship |
   |       |       |       |       |       |       |       |       | is    |
   |       |       |       |       |       |       |       |       | used, |
   |       |       |       |       |       |       |       |       | not   |
   |       |       |       |       |       |       |       |       | the   |
   |       |       |       |       |       |       |       |       | by    |
   |       |       |       |       |       |       |       |       | -refe |
   |       |       |       |       |       |       |       |       | rence |
   |       |       |       |       |       |       |       |       | (     |
   |       |       |       |       |       |       |       |       | R-SEL |
   |       |       |       |       |       |       |       |       | ECTED |
   |       |       |       |       |       |       |       |       | FROM) |
   |       |       |       |       |       |       |       |       | rel   |
   |       |       |       |       |       |       |       |       | ation |
   |       |       |       |       |       |       |       |       | ship. |
   +-------+-------+-------+-------+-------+-------+-------+-------+-------+

.. _sect_Mapping_TID_4019:

Mapping of Algorithm Identification
'''''''''''''''''''''''''''''''''''

This section describes the mapping of PS3.16 .

.. table:: Mapping of Algorithm Identification

   +-------+-------+-------+-------+-------+-------+-------+-------+-------+
   | DICOM | DICOM | DICOM | DICOM | Gene  | AIM   | AIM   | AIM   | Co    |
   | SR    | VT    | VM    | Usage | rated | El    | Data  | Mu    | mment |
   | Path  |       |       | Type  | Value | ement | Type  | ltipl |       |
   |       |       |       |       |       | or    |       | icity |       |
   |       |       |       |       |       | Attr  |       |       |       |
   |       |       |       |       |       | ibute |       |       |       |
   +=======+=======+=======+=======+=======+=======+=======+=======+=======+
   | (12   | TEXT  | 1     | U     |       | Image | ST    | 1     | The   |
   | 6000, |       |       |       |       | ​Anno |       |       | type  |
   | DCM,  |       |       |       |       | tatio |       |       | attr  |
   | "Im   |       |       |       |       | n​​Co |       |       | ibute |
   | aging |       |       |       |       | llect |       |       | (CD   |
   | M     |       |       |       |       | ion/​ |       |       | 1..n) |
   | easur |       |       |       |       | image |       |       | is    |
   | ement |       |       |       |       | ​Anno |       |       | not   |
   | Rep   |       |       |       |       | tatio |       |       | supp  |
   | ort") |       |       |       |       | ns/​I |       |       | orted |
   | >     |       |       |       |       | mage​ |       |       | by    |
   | (12   |       |       |       |       | Annot |       |       | CID   |
   | 6010, |       |       |       |       | ation |       |       | 4019  |
   | DCM,  |       |       |       |       | /​cal |       |       |       |
   | "Im   |       |       |       |       | culat |       |       |       |
   | aging |       |       |       |       | ion​E |       |       |       |
   | Meas  |       |       |       |       | ntity |       |       |       |
   | ureme |       |       |       |       | ​Coll |       |       |       |
   | nts") |       |       |       |       | ectio |       |       |       |
   | >     |       |       |       |       | n/​Ca |       |       |       |
   | (12   |       |       |       |       | lcula |       |       |       |
   | 5007, |       |       |       |       | tionE |       |       |       |
   | DCM,  |       |       |       |       | ntity |       |       |       |
   | "M    |       |       |       |       | /​alg |       |       |       |
   | easur |       |       |       |       | orith |       |       |       |
   | ement |       |       |       |       | m/​na |       |       |       |
   | Gr    |       |       |       |       | me/​@ |       |       |       |
   | oup") |       |       |       |       | value |       |       |       |
   | >     |       |       |       |       |       |       |       |       |
   | $M    |       |       |       |       |       |       |       |       |
   | easur |       |       |       |       |       |       |       |       |
   | ement |       |       |       |       |       |       |       |       |
   | >     |       |       |       |       |       |       |       |       |
   | (11   |       |       |       |       |       |       |       |       |
   | 1001, |       |       |       |       |       |       |       |       |
   | DCM,  |       |       |       |       |       |       |       |       |
   | "Algo |       |       |       |       |       |       |       |       |
   | rithm |       |       |       |       |       |       |       |       |
   | N     |       |       |       |       |       |       |       |       |
   | ame") |       |       |       |       |       |       |       |       |
   +-------+-------+-------+-------+-------+-------+-------+-------+-------+
   | (12   | TEXT  | 1     | U     |       | Ima   | ST    | 0..1  |       |
   | 6000, |       |       |       |       | ge​An |       |       |       |
   | DCM,  |       |       |       |       | notat |       |       |       |
   | "Im   |       |       |       |       | ion​​ |       |       |       |
   | aging |       |       |       |       | Colle |       |       |       |
   | M     |       |       |       |       | ction |       |       |       |
   | easur |       |       |       |       | /​ima |       |       |       |
   | ement |       |       |       |       | ge​An |       |       |       |
   | Rep   |       |       |       |       | notat |       |       |       |
   | ort") |       |       |       |       | ions/ |       |       |       |
   | >     |       |       |       |       | ​Imag |       |       |       |
   | (12   |       |       |       |       | e​Ann |       |       |       |
   | 6010, |       |       |       |       | otati |       |       |       |
   | DCM,  |       |       |       |       | on/​c |       |       |       |
   | "Im   |       |       |       |       | alcul |       |       |       |
   | aging |       |       |       |       | ation |       |       |       |
   | Meas  |       |       |       |       | ​Enti |       |       |       |
   | ureme |       |       |       |       | ty​Co |       |       |       |
   | nts") |       |       |       |       | llect |       |       |       |
   | >     |       |       |       |       | ion/​ |       |       |       |
   | (12   |       |       |       |       | Calcu |       |       |       |
   | 5007, |       |       |       |       | latio |       |       |       |
   | DCM,  |       |       |       |       | nEnti |       |       |       |
   | "M    |       |       |       |       | ty/​a |       |       |       |
   | easur |       |       |       |       | lgori |       |       |       |
   | ement |       |       |       |       | thm/​ |       |       |       |
   | Gr    |       |       |       |       | versi |       |       |       |
   | oup") |       |       |       |       | on/​@ |       |       |       |
   | >     |       |       |       |       | value |       |       |       |
   | $M    |       |       |       |       |       |       |       |       |
   | easur |       |       |       |       |       |       |       |       |
   | ement |       |       |       |       |       |       |       |       |
   | >     |       |       |       |       |       |       |       |       |
   | (11   |       |       |       |       |       |       |       |       |
   | 1003, |       |       |       |       |       |       |       |       |
   | DCM,  |       |       |       |       |       |       |       |       |
   | "Algo |       |       |       |       |       |       |       |       |
   | rithm |       |       |       |       |       |       |       |       |
   | Vers  |       |       |       |       |       |       |       |       |
   | ion") |       |       |       |       |       |       |       |       |
   +-------+-------+-------+-------+-------+-------+-------+-------+-------+
   | (12   | TEXT  | 1-n   | U     |       | I     | CD,   | 0..n  | Sep   |
   | 6000, |       |       |       |       | mage​ | ST,ST |       | arate |
   | DCM,  |       |       |       |       | Annot |       |       | ma    |
   | "Im   |       |       |       |       | ation |       |       | pping |
   | aging |       |       |       |       | ​​Col |       |       | of    |
   | M     |       |       |       |       | lecti |       |       | data  |
   | easur |       |       |       |       | on/​i |       |       | Type, |
   | ement |       |       |       |       | mage​ |       |       | name  |
   | Rep   |       |       |       |       | Annot |       |       | and   |
   | ort") |       |       |       |       | ation |       |       | value |
   | >     |       |       |       |       | s/​Im |       |       | attri |
   | (12   |       |       |       |       | age​A |       |       | butes |
   | 6010, |       |       |       |       | nnota |       |       | is    |
   | DCM,  |       |       |       |       | tion/ |       |       | not   |
   | "Im   |       |       |       |       | ​calc |       |       | supp  |
   | aging |       |       |       |       | ulati |       |       | orted |
   | Meas  |       |       |       |       | on​En |       |       | by    |
   | ureme |       |       |       |       | tity​ |       |       | CID   |
   | nts") |       |       |       |       | Colle |       |       | 4019  |
   | >     |       |       |       |       | ction |       |       |       |
   | (12   |       |       |       |       | /​Cal |       |       |       |
   | 5007, |       |       |       |       | culat |       |       |       |
   | DCM,  |       |       |       |       | ionEn |       |       |       |
   | "M    |       |       |       |       | tity/ |       |       |       |
   | easur |       |       |       |       | ​algo |       |       |       |
   | ement |       |       |       |       | rithm |       |       |       |
   | Gr    |       |       |       |       | /​par |       |       |       |
   | oup") |       |       |       |       | amete |       |       |       |
   | >     |       |       |       |       | r/​@d |       |       |       |
   | $M    |       |       |       |       | ataTy |       |       |       |
   | easur |       |       |       |       | pe,@n |       |       |       |
   | ement |       |       |       |       | ame,@ |       |       |       |
   | >     |       |       |       |       | value |       |       |       |
   | (11   |       |       |       |       |       |       |       |       |
   | 1002, |       |       |       |       |       |       |       |       |
   | DCM,  |       |       |       |       |       |       |       |       |
   | "Algo |       |       |       |       |       |       |       |       |
   | rithm |       |       |       |       |       |       |       |       |
   | Pa    |       |       |       |       |       |       |       |       |
   | ramet |       |       |       |       |       |       |       |       |
   | ers") |       |       |       |       |       |       |       |       |
   +-------+-------+-------+-------+-------+-------+-------+-------+-------+
   |       |       |       |       |       | Im    | CD    | 1..n  | No    |
   |       |       |       |       |       | age​A |       |       | cor   |
   |       |       |       |       |       | nnota |       |       | respo |
   |       |       |       |       |       | tion​ |       |       | nding |
   |       |       |       |       |       | ​Coll |       |       | ma    |
   |       |       |       |       |       | ectio |       |       | pping |
   |       |       |       |       |       | n/​im |       |       | in    |
   |       |       |       |       |       | age​A |       |       | DICOM |
   |       |       |       |       |       | nnota |       |       | SR    |
   |       |       |       |       |       | tions |       |       | tem   |
   |       |       |       |       |       | /​Ima |       |       | plate |
   |       |       |       |       |       | ge​An |       |       | at    |
   |       |       |       |       |       | notat |       |       | this  |
   |       |       |       |       |       | ion/​ |       |       | time. |
   |       |       |       |       |       | calcu |       |       |       |
   |       |       |       |       |       | latio |       |       |       |
   |       |       |       |       |       | n​Ent |       |       |       |
   |       |       |       |       |       | ity​C |       |       |       |
   |       |       |       |       |       | ollec |       |       |       |
   |       |       |       |       |       | tion/ |       |       |       |
   |       |       |       |       |       | ​Calc |       |       |       |
   |       |       |       |       |       | ulati |       |       |       |
   |       |       |       |       |       | onEnt |       |       |       |
   |       |       |       |       |       | ity/​ |       |       |       |
   |       |       |       |       |       | algor |       |       |       |
   |       |       |       |       |       | ithm/ |       |       |       |
   |       |       |       |       |       | ​type |       |       |       |
   +-------+-------+-------+-------+-------+-------+-------+-------+-------+

.. _sect_Mapping_TID_4108:

Mapping of Tracking Identifier
''''''''''''''''''''''''''''''

This section describes the mapping of .

For the purpose of this mapping, this template is not used to track
individual measurements; rather, the corresponding content items defined
in `Mapping of Measurement Group <#sect_Mapping_TID_1501>`__ are mapped
at the Measurement Group level instead.

.. table:: Mapping of Tracking Identifier

   +-------+-------+-------+-------+-------+-------+-------+-------+-------+
   | DICOM | DICOM | DICOM | DICOM | Gene  | AIM   | AIM   | AIM   | Co    |
   | SR    | VT    | VM    | Usage | rated | El    | Data  | Mu    | mment |
   | Path  |       |       | Type  | Value | ement | Type  | ltipl |       |
   |       |       |       |       |       | or    |       | icity |       |
   |       |       |       |       |       | Attr  |       |       |       |
   |       |       |       |       |       | ibute |       |       |       |
   +=======+=======+=======+=======+=======+=======+=======+=======+=======+
   | (12   | TEXT  | 1     | U     |       |       |       |       | MC    |
   | 6000, |       |       |       |       |       |       |       | but U |
   | DCM,  |       |       |       |       |       |       |       | in    |
   | "Im   |       |       |       |       |       |       |       | p     |
   | aging |       |       |       |       |       |       |       | arent |
   | M     |       |       |       |       |       |       |       | TID   |
   | easur |       |       |       |       |       |       |       | 300.  |
   | ement |       |       |       |       |       |       |       |       |
   | Rep   |       |       |       |       |       |       |       | Not   |
   | ort") |       |       |       |       |       |       |       | m     |
   | >     |       |       |       |       |       |       |       | apped |
   | (12   |       |       |       |       |       |       |       | at    |
   | 6010, |       |       |       |       |       |       |       | this  |
   | DCM,  |       |       |       |       |       |       |       | level |
   | "Im   |       |       |       |       |       |       |       | for   |
   | aging |       |       |       |       |       |       |       | TID   |
   | Meas  |       |       |       |       |       |       |       | 1500, |
   | ureme |       |       |       |       |       |       |       | but   |
   | nts") |       |       |       |       |       |       |       | r     |
   | >     |       |       |       |       |       |       |       | ather |
   | (12   |       |       |       |       |       |       |       | at    |
   | 5007, |       |       |       |       |       |       |       | the   |
   | DCM,  |       |       |       |       |       |       |       | M     |
   | "M    |       |       |       |       |       |       |       | easur |
   | easur |       |       |       |       |       |       |       | ement |
   | ement |       |       |       |       |       |       |       | Group |
   | Gr    |       |       |       |       |       |       |       | level |
   | oup") |       |       |       |       |       |       |       | in    |
   | >     |       |       |       |       |       |       |       | TID   |
   | $M    |       |       |       |       |       |       |       | 1501. |
   | easur |       |       |       |       |       |       |       |       |
   | ement |       |       |       |       |       |       |       |       |
   | >     |       |       |       |       |       |       |       |       |
   | (11   |       |       |       |       |       |       |       |       |
   | 2039, |       |       |       |       |       |       |       |       |
   | DCM,  |       |       |       |       |       |       |       |       |
   | "Tra  |       |       |       |       |       |       |       |       |
   | cking |       |       |       |       |       |       |       |       |
   | Id    |       |       |       |       |       |       |       |       |
   | entif |       |       |       |       |       |       |       |       |
   | ier") |       |       |       |       |       |       |       |       |
   +-------+-------+-------+-------+-------+-------+-------+-------+-------+
   | (12   | U     | 1     | U     |       |       |       |       | MC    |
   | 6000, | IDREF |       |       |       |       |       |       | but U |
   | DCM,  |       |       |       |       |       |       |       | in    |
   | "Im   |       |       |       |       |       |       |       | p     |
   | aging |       |       |       |       |       |       |       | arent |
   | M     |       |       |       |       |       |       |       | TID   |
   | easur |       |       |       |       |       |       |       | 300.  |
   | ement |       |       |       |       |       |       |       |       |
   | Rep   |       |       |       |       |       |       |       | Not   |
   | ort") |       |       |       |       |       |       |       | m     |
   | >     |       |       |       |       |       |       |       | apped |
   | (12   |       |       |       |       |       |       |       | at    |
   | 6010, |       |       |       |       |       |       |       | this  |
   | DCM,  |       |       |       |       |       |       |       | level |
   | "Im   |       |       |       |       |       |       |       | for   |
   | aging |       |       |       |       |       |       |       | TID   |
   | Meas  |       |       |       |       |       |       |       | 1500, |
   | ureme |       |       |       |       |       |       |       | but   |
   | nts") |       |       |       |       |       |       |       | r     |
   | >     |       |       |       |       |       |       |       | ather |
   | (12   |       |       |       |       |       |       |       | at    |
   | 5007, |       |       |       |       |       |       |       | the   |
   | DCM,  |       |       |       |       |       |       |       | M     |
   | "M    |       |       |       |       |       |       |       | easur |
   | easur |       |       |       |       |       |       |       | ement |
   | ement |       |       |       |       |       |       |       | Group |
   | Gr    |       |       |       |       |       |       |       | level |
   | oup") |       |       |       |       |       |       |       | in    |
   | >     |       |       |       |       |       |       |       | TID   |
   | $M    |       |       |       |       |       |       |       | 1501. |
   | easur |       |       |       |       |       |       |       |       |
   | ement |       |       |       |       |       |       |       |       |
   | >     |       |       |       |       |       |       |       |       |
   | (11   |       |       |       |       |       |       |       |       |
   | 2040, |       |       |       |       |       |       |       |       |
   | DCM,  |       |       |       |       |       |       |       |       |
   | "Tra  |       |       |       |       |       |       |       |       |
   | cking |       |       |       |       |       |       |       |       |
   | U     |       |       |       |       |       |       |       |       |
   | nique |       |       |       |       |       |       |       |       |
   | Id    |       |       |       |       |       |       |       |       |
   | entif |       |       |       |       |       |       |       |       |
   | ier") |       |       |       |       |       |       |       |       |
   +-------+-------+-------+-------+-------+-------+-------+-------+-------+

.. _sect_Mapping_TID_1204:

Mapping of Language of Content Item and Descendants
'''''''''''''''''''''''''''''''''''''''''''''''''''

This section describes the mapping of .

.. table:: Mapping of Language of Content Item and Descendants

   +-------+-------+-------+-------+-------+-------+-------+-------+-------+
   | DICOM | DICOM | DICOM | DICOM | Gene  | AIM   | AIM   | AIM   | Co    |
   | SR    | VT    | VM    | Usage | rated | El    | Data  | Mu    | mment |
   | Path  |       |       | Type  | Value | ement | Type  | ltipl |       |
   |       |       |       |       |       | or    |       | icity |       |
   |       |       |       |       |       | Attr  |       |       |       |
   |       |       |       |       |       | ibute |       |       |       |
   +=======+=======+=======+=======+=======+=======+=======+=======+=======+
   | (12   | CODE  | 1     | M     | (en   |       |       |       | Not   |
   | 6000, |       |       |       | g,RFC |       |       |       | used  |
   | DCM,  |       |       |       | 5646, |       |       |       | in    |
   | "Im   |       |       |       | "Engl |       |       |       | AIM;  |
   | aging |       |       |       | ish") |       |       |       | disc  |
   | M     |       |       |       |       |       |       |       | arded |
   | easur |       |       |       |       |       |       |       | if    |
   | ement |       |       |       |       |       |       |       | pr    |
   | Rep   |       |       |       |       |       |       |       | esent |
   | ort") |       |       |       |       |       |       |       | in    |
   | >     |       |       |       |       |       |       |       | DICOM |
   | (12   |       |       |       |       |       |       |       | SR.   |
   | 1049, |       |       |       |       |       |       |       |       |
   | DCM,  |       |       |       |       |       |       |       |       |
   | "Lan  |       |       |       |       |       |       |       |       |
   | guage |       |       |       |       |       |       |       |       |
   | of    |       |       |       |       |       |       |       |       |
   | Co    |       |       |       |       |       |       |       |       |
   | ntent |       |       |       |       |       |       |       |       |
   | Item  |       |       |       |       |       |       |       |       |
   | and   |       |       |       |       |       |       |       |       |
   | Des   |       |       |       |       |       |       |       |       |
   | cenda |       |       |       |       |       |       |       |       |
   | nts") |       |       |       |       |       |       |       |       |
   +-------+-------+-------+-------+-------+-------+-------+-------+-------+
   | (12   | CODE  | 1     | U     | (     |       |       |       | Not   |
   | 6000, |       |       |       | US,IS |       |       |       | used  |
   | DCM,  |       |       |       | O3166 |       |       |       | in    |
   | "Im   |       |       |       | _1,"U |       |       |       | AIM;  |
   | aging |       |       |       | nited |       |       |       | disc  |
   | M     |       |       |       | Sta   |       |       |       | arded |
   | easur |       |       |       | tes") |       |       |       | if    |
   | ement |       |       |       |       |       |       |       | pr    |
   | Rep   |       |       |       |       |       |       |       | esent |
   | ort") |       |       |       |       |       |       |       | in    |
   | >     |       |       |       |       |       |       |       | DICOM |
   | (12   |       |       |       |       |       |       |       | SR.   |
   | 1049, |       |       |       |       |       |       |       |       |
   | DCM,  |       |       |       |       |       |       |       |       |
   | "Lan  |       |       |       |       |       |       |       |       |
   | guage |       |       |       |       |       |       |       |       |
   | of    |       |       |       |       |       |       |       |       |
   | Co    |       |       |       |       |       |       |       |       |
   | ntent |       |       |       |       |       |       |       |       |
   | Item  |       |       |       |       |       |       |       |       |
   | and   |       |       |       |       |       |       |       |       |
   | Des   |       |       |       |       |       |       |       |       |
   | cenda |       |       |       |       |       |       |       |       |
   | nts") |       |       |       |       |       |       |       |       |
   | >     |       |       |       |       |       |       |       |       |
   | (12   |       |       |       |       |       |       |       |       |
   | 1046, |       |       |       |       |       |       |       |       |
   | DCM,  |       |       |       |       |       |       |       |       |
   | "Co   |       |       |       |       |       |       |       |       |
   | untry |       |       |       |       |       |       |       |       |
   | of    |       |       |       |       |       |       |       |       |
   | Langu |       |       |       |       |       |       |       |       |
   | age") |       |       |       |       |       |       |       |       |
   +-------+-------+-------+-------+-------+-------+-------+-------+-------+

.. _sect_Mapping_TID_1001:

Mapping of Observation Context
''''''''''''''''''''''''''''''

This section describes the mapping of .

.. table:: Mapping of Observation Context

   +----------+----------+----------+----------+----------+----------+
   | DICOM SR | DICOM VT | DICOM VM | DICOM    | G        | AIM      |
   | Path     |          |          | Usage    | enerated | Element  |
   |          |          |          | Type     | Value    | or       |
   |          |          |          |          |          | A        |
   |          |          |          |          |          | ttribute |
   +==========+==========+==========+==========+==========+==========+
   | (126000, | INCLUDE  | 1-n      | MC       | `Mapping | Only     |
   | DCM,     |          |          |          | of       | required |
   | "Imaging |          |          |          | Observer | for AIM  |
   | Mea      |          |          |          | Con      | if       |
   | surement |          |          |          | text <#s | At       |
   | Report") |          |          |          | ect_Mapp | tributes |
   | >        |          |          |          | ing_TID_ | of the   |
   |          |          |          |          | 1002>`__ | Author   |
   |          |          |          |          |          | Observer |
   |          |          |          |          |          | Sequence |
   |          |          |          |          |          | (00      |
   |          |          |          |          |          | 40,A078) |
   |          |          |          |          |          | are      |
   |          |          |          |          |          | insu     |
   |          |          |          |          |          | fficient |
   |          |          |          |          |          | to       |
   |          |          |          |          |          | describe |
   |          |          |          |          |          | the      |
   |          |          |          |          |          | person   |
   |          |          |          |          |          | o        |
   |          |          |          |          |          | bserver; |
   |          |          |          |          |          | not used |
   |          |          |          |          |          | for a    |
   |          |          |          |          |          | device   |
   |          |          |          |          |          | o        |
   |          |          |          |          |          | bserver. |
   +----------+----------+----------+----------+----------+----------+
   | (126000, | INCLUDE  | 1        | MC       | TID 1005 | Not used |
   | DCM,     |          |          |          | "P       | in AIM   |
   | "Imaging |          |          |          | rocedure | since    |
   | Mea      |          |          |          | Context" | r        |
   | surement |          |          |          |          | edundant |
   | Report") |          |          |          |          | with     |
   | >        |          |          |          |          | header   |
   |          |          |          |          |          | info     |
   |          |          |          |          |          | rmation; |
   |          |          |          |          |          | d        |
   |          |          |          |          |          | iscarded |
   |          |          |          |          |          | if       |
   |          |          |          |          |          | present  |
   |          |          |          |          |          | in DICOM |
   |          |          |          |          |          | SR.      |
   +----------+----------+----------+----------+----------+----------+
   | (126000, | INCLUDE  | 1        | MC       | TID 1006 | Not used |
   | DCM,     |          |          |          | "Subject | in AIM   |
   | "Imaging |          |          |          | Context" | since    |
   | Mea      |          |          |          |          | r        |
   | surement |          |          |          |          | edundant |
   | Report") |          |          |          |          | with     |
   | >        |          |          |          |          | header   |
   |          |          |          |          |          | info     |
   |          |          |          |          |          | rmation; |
   |          |          |          |          |          | d        |
   |          |          |          |          |          | iscarded |
   |          |          |          |          |          | if       |
   |          |          |          |          |          | present  |
   |          |          |          |          |          | in DICOM |
   |          |          |          |          |          | SR.      |
   +----------+----------+----------+----------+----------+----------+

.. _sect_Mapping_TID_1002:

Mapping of Observer Context
'''''''''''''''''''''''''''

This section describes the mapping of .

.. table:: Mapping of Observer Context

   +-------+-------+-------+-------+-------+-------+-------+-------+-------+
   | DICOM | DICOM | DICOM | DICOM | Gene  | AIM   | AIM   | AIM   | Co    |
   | SR    | VT    | VM    | Usage | rated | El    | Data  | Mu    | mment |
   | Path  |       |       | Type  | Value | ement | Type  | ltipl |       |
   |       |       |       |       |       | or    |       | icity |       |
   |       |       |       |       |       | Attr  |       |       |       |
   |       |       |       |       |       | ibute |       |       |       |
   +=======+=======+=======+=======+=======+=======+=======+=======+=======+
   | (12   | CODE  | 1     | MC    |       |       |       |       | Since |
   | 6000, |       |       |       |       |       |       |       | this  |
   | DCM,  |       |       |       |       |       |       |       | tem   |
   | "Im   |       |       |       |       |       |       |       | plate |
   | aging |       |       |       |       |       |       |       | is    |
   | M     |       |       |       |       |       |       |       | only  |
   | easur |       |       |       |       |       |       |       | used  |
   | ement |       |       |       |       |       |       |       | for   |
   | Rep   |       |       |       |       |       |       |       | AIM   |
   | ort") |       |       |       |       |       |       |       | for   |
   | >     |       |       |       |       |       |       |       | p     |
   | (12   |       |       |       |       |       |       |       | erson |
   | 1005, |       |       |       |       |       |       |       | obser |
   | DCM,  |       |       |       |       |       |       |       | vers, |
   | "Obs  |       |       |       |       |       |       |       | which |
   | erver |       |       |       |       |       |       |       | is    |
   | T     |       |       |       |       |       |       |       | the   |
   | ype") |       |       |       |       |       |       |       | def   |
   |       |       |       |       |       |       |       |       | ault, |
   |       |       |       |       |       |       |       |       | it    |
   |       |       |       |       |       |       |       |       | may   |
   |       |       |       |       |       |       |       |       | be    |
   |       |       |       |       |       |       |       |       | om    |
   |       |       |       |       |       |       |       |       | itted |
   |       |       |       |       |       |       |       |       | or    |
   |       |       |       |       |       |       |       |       | expli |
   |       |       |       |       |       |       |       |       | citly |
   |       |       |       |       |       |       |       |       | sent  |
   |       |       |       |       |       |       |       |       | as    |
   |       |       |       |       |       |       |       |       | (12   |
   |       |       |       |       |       |       |       |       | 1006, |
   |       |       |       |       |       |       |       |       | DCM,  |
   |       |       |       |       |       |       |       |       | "Pers |
   |       |       |       |       |       |       |       |       | on"); |
   |       |       |       |       |       |       |       |       | see   |
   |       |       |       |       |       |       |       |       | also  |
   +-------+-------+-------+-------+-------+-------+-------+-------+-------+
   | (12   | IN    | 1     | MC    | `Ma   | IFF   |       |       |       |
   | 6000, | CLUDE |       |       | pping | Row 1 |       |       |       |
   | DCM,  |       |       |       | of    | value |       |       |       |
   | "Im   |       |       |       | P     | =     |       |       |       |
   | aging |       |       |       | erson | (12   |       |       |       |
   | M     |       |       |       | Obs   | 1006, |       |       |       |
   | easur |       |       |       | erver | DCM,  |       |       |       |
   | ement |       |       |       | I     | "Per  |       |       |       |
   | Rep   |       |       |       | denti | son") |       |       |       |
   | ort") |       |       |       | fying | or    |       |       |       |
   | >     |       |       |       | Att   | Row 1 |       |       |       |
   |       |       |       |       | ribut | is    |       |       |       |
   |       |       |       |       | es <# | a     |       |       |       |
   |       |       |       |       | sect_ | bsent |       |       |       |
   |       |       |       |       | Mappi |       |       |       |       |
   |       |       |       |       | ng_TI |       |       |       |       |
   |       |       |       |       | D_100 |       |       |       |       |
   |       |       |       |       | 3>`__ |       |       |       |       |
   +-------+-------+-------+-------+-------+-------+-------+-------+-------+
   | (12   | IN    | 1     | MC    | TID   | Not   |       |       |       |
   | 6000, | CLUDE |       |       | 1004  | used  |       |       |       |
   | DCM,  |       |       |       | "D    | in    |       |       |       |
   | "Im   |       |       |       | evice | AIM;  |       |       |       |
   | aging |       |       |       | Obs   | IFF   |       |       |       |
   | M     |       |       |       | erver | Row 1 |       |       |       |
   | easur |       |       |       | I     | value |       |       |       |
   | ement |       |       |       | denti | =     |       |       |       |
   | Rep   |       |       |       | fying | (12   |       |       |       |
   | ort") |       |       |       | A     | 1007, |       |       |       |
   | >     |       |       |       | ttrib | DCM,  |       |       |       |
   |       |       |       |       | utes" | "Dev  |       |       |       |
   |       |       |       |       |       | ice") |       |       |       |
   +-------+-------+-------+-------+-------+-------+-------+-------+-------+

.. _sect_Mapping_TID_1003:

Mapping of Person Observer Identifying Attributes
'''''''''''''''''''''''''''''''''''''''''''''''''

This section describes the mapping of .

.. table:: Mapping of Person Observer Identifying Attributes

   +-------+-------+-------+-------+-------+-------+-------+-------+-------+
   | DICOM | DICOM | DICOM | DICOM | Gene  | AIM   | AIM   | AIM   | Co    |
   | SR    | VT    | VM    | Usage | rated | El    | Data  | Mu    | mment |
   | Path  |       |       | Type  | Value | ement | Type  | ltipl |       |
   |       |       |       |       |       | or    |       | icity |       |
   |       |       |       |       |       | Attr  |       |       |       |
   |       |       |       |       |       | ibute |       |       |       |
   +=======+=======+=======+=======+=======+=======+=======+=======+=======+
   | (12   | PNAME | 1     | M     |       | Ima   | ST    | 1..1  |       |
   | 6000, |       |       |       |       | ge​An |       |       |       |
   | DCM,  |       |       |       |       | notat |       |       |       |
   | "Im   |       |       |       |       | ion​​ |       |       |       |
   | aging |       |       |       |       | Colle |       |       |       |
   | M     |       |       |       |       | ction |       |       |       |
   | easur |       |       |       |       | /​use |       |       |       |
   | ement |       |       |       |       | r/​na |       |       |       |
   | Rep   |       |       |       |       | me/​@ |       |       |       |
   | ort") |       |       |       |       | value |       |       |       |
   | >     |       |       |       |       |       |       |       |       |
   | (12   |       |       |       |       |       |       |       |       |
   | 1008, |       |       |       |       |       |       |       |       |
   | DCM,  |       |       |       |       |       |       |       |       |
   | "P    |       |       |       |       |       |       |       |       |
   | erson |       |       |       |       |       |       |       |       |
   | Obs   |       |       |       |       |       |       |       |       |
   | erver |       |       |       |       |       |       |       |       |
   | N     |       |       |       |       |       |       |       |       |
   | ame") |       |       |       |       |       |       |       |       |
   +-------+-------+-------+-------+-------+-------+-------+-------+-------+
   | (12   | PNAME | 1     | M     |       | Ima   | ST    | 1..1  |       |
   | 6000, |       |       |       |       | ge​An |       |       |       |
   | DCM,  |       |       |       |       | notat |       |       |       |
   | "Im   |       |       |       |       | ion​​ |       |       |       |
   | aging |       |       |       |       | Colle |       |       |       |
   | M     |       |       |       |       | ction |       |       |       |
   | easur |       |       |       |       | /​use |       |       |       |
   | ement |       |       |       |       | r/​lo |       |       |       |
   | Rep   |       |       |       |       | ginNa |       |       |       |
   | ort") |       |       |       |       | me/​@ |       |       |       |
   | >     |       |       |       |       | value |       |       |       |
   | (12   |       |       |       |       |       |       |       |       |
   | 8774, |       |       |       |       |       |       |       |       |
   | DCM,  |       |       |       |       |       |       |       |       |
   | "P    |       |       |       |       |       |       |       |       |
   | erson |       |       |       |       |       |       |       |       |
   | Obser |       |       |       |       |       |       |       |       |
   | ver's |       |       |       |       |       |       |       |       |
   | Login |       |       |       |       |       |       |       |       |
   | N     |       |       |       |       |       |       |       |       |
   | ame") |       |       |       |       |       |       |       |       |
   +-------+-------+-------+-------+-------+-------+-------+-------+-------+
   | (12   | TEXT  | 1     | U     |       |       |       |       | Not   |
   | 6000, |       |       |       |       |       |       |       | used  |
   | DCM,  |       |       |       |       |       |       |       | in    |
   | "Im   |       |       |       |       |       |       |       | AIM.  |
   | aging |       |       |       |       |       |       |       |       |
   | M     |       |       |       |       |       |       |       |       |
   | easur |       |       |       |       |       |       |       |       |
   | ement |       |       |       |       |       |       |       |       |
   | Rep   |       |       |       |       |       |       |       |       |
   | ort") |       |       |       |       |       |       |       |       |
   | >     |       |       |       |       |       |       |       |       |
   | (12   |       |       |       |       |       |       |       |       |
   | 1009, |       |       |       |       |       |       |       |       |
   | DCM,  |       |       |       |       |       |       |       |       |
   | "P    |       |       |       |       |       |       |       |       |
   | erson |       |       |       |       |       |       |       |       |
   | Obser |       |       |       |       |       |       |       |       |
   | ver's |       |       |       |       |       |       |       |       |
   | Or    |       |       |       |       |       |       |       |       |
   | ganiz |       |       |       |       |       |       |       |       |
   | ation |       |       |       |       |       |       |       |       |
   | N     |       |       |       |       |       |       |       |       |
   | ame") |       |       |       |       |       |       |       |       |
   +-------+-------+-------+-------+-------+-------+-------+-------+-------+
   | (12   | CODE  | 1     | U     |       |       |       |       | Not   |
   | 6000, |       |       |       |       |       |       |       | used  |
   | DCM,  |       |       |       |       |       |       |       | in    |
   | "Im   |       |       |       |       |       |       |       | AIM.  |
   | aging |       |       |       |       |       |       |       |       |
   | M     |       |       |       |       |       |       |       |       |
   | easur |       |       |       |       |       |       |       |       |
   | ement |       |       |       |       |       |       |       |       |
   | Rep   |       |       |       |       |       |       |       |       |
   | ort") |       |       |       |       |       |       |       |       |
   | >     |       |       |       |       |       |       |       |       |
   | (12   |       |       |       |       |       |       |       |       |
   | 1010, |       |       |       |       |       |       |       |       |
   | DCM,  |       |       |       |       |       |       |       |       |
   | "P    |       |       |       |       |       |       |       |       |
   | erson |       |       |       |       |       |       |       |       |
   | Obser |       |       |       |       |       |       |       |       |
   | ver's |       |       |       |       |       |       |       |       |
   | Role  |       |       |       |       |       |       |       |       |
   | in    |       |       |       |       |       |       |       |       |
   | the   |       |       |       |       |       |       |       |       |
   | Orga  |       |       |       |       |       |       |       |       |
   | nizat |       |       |       |       |       |       |       |       |
   | ion") |       |       |       |       |       |       |       |       |
   +-------+-------+-------+-------+-------+-------+-------+-------+-------+
   | (12   | CODE  | 1     | U     |       | Image | ST    | 0..1  | B     |
   | 6000, |       |       |       |       | ​Anno |       |       |       |
   | DCM,  |       |       |       |       | tatio |       |       | V     |
   | "Im   |       |       |       |       | n​​Co |       |       | alues |
   | aging |       |       |       |       | llect |       |       | m     |
   | M     |       |       |       |       | ion/​ |       |       | apped |
   | easur |       |       |       |       | user/ |       |       | are   |
   | ement |       |       |       |       | ​role |       |       | am    |
   | Rep   |       |       |       |       | InTri |       |       | ended |
   | ort") |       |       |       |       | al/​@ |       |       | in CP |
   | >     |       |       |       |       | value |       |       | 1734. |
   | (12   |       |       |       |       |       |       |       |       |
   | 1011, |       |       |       |       |       |       |       | AIM   |
   | DCM,  |       |       |       |       |       |       |       | does  |
   | "P    |       |       |       |       |       |       |       | not   |
   | erson |       |       |       |       |       |       |       | d     |
   | Obser |       |       |       |       |       |       |       | efine |
   | ver's |       |       |       |       |       |       |       | a     |
   | Role  |       |       |       |       |       |       |       | value |
   | in    |       |       |       |       |       |       |       | set   |
   | this  |       |       |       |       |       |       |       | for   |
   | P     |       |       |       |       |       |       |       | the   |
   | roced |       |       |       |       |       |       |       | r     |
   | ure") |       |       |       |       |       |       |       | oles, |
   |       |       |       |       |       |       |       |       | so no |
   |       |       |       |       |       |       |       |       | sta   |
   |       |       |       |       |       |       |       |       | ndard |
   |       |       |       |       |       |       |       |       | ma    |
   |       |       |       |       |       |       |       |       | pping |
   |       |       |       |       |       |       |       |       | to    |
   |       |       |       |       |       |       |       |       | the   |
   |       |       |       |       |       |       |       |       | DICOM |
   |       |       |       |       |       |       |       |       | codes |
   |       |       |       |       |       |       |       |       | is    |
   |       |       |       |       |       |       |       |       | def   |
   |       |       |       |       |       |       |       |       | ined. |
   +-------+-------+-------+-------+-------+-------+-------+-------+-------+
   | (12   | TEXT  | 1     | U     |       | Image | INT   | 0..1  | DICOM |
   | 6000, |       |       |       |       | ​Anno |       |       | a     |
   | DCM,  |       |       |       |       | tatio |       |       | llows |
   | "Im   |       |       |       |       | n​​Co |       |       | for   |
   | aging |       |       |       |       | llect |       |       | alp   |
   | M     |       |       |       |       | ion/​ |       |       | hanum |
   | easur |       |       |       |       | user/ |       |       | eric, |
   | ement |       |       |       |       | ​numb |       |       | wh    |
   | Rep   |       |       |       |       | erWit |       |       | ereas |
   | ort") |       |       |       |       | hinRo |       |       | AIM   |
   | >     |       |       |       |       | leOfC |       |       | is    |
   | (12   |       |       |       |       | linic |       |       | INT   |
   | 1011, |       |       |       |       | alTri |       |       | only. |
   | DCM,  |       |       |       |       | al/​@ |       |       |       |
   | "P    |       |       |       |       | value |       |       |       |
   | erson |       |       |       |       |       |       |       |       |
   | Obser |       |       |       |       |       |       |       |       |
   | ver's |       |       |       |       |       |       |       |       |
   | Role  |       |       |       |       |       |       |       |       |
   | in    |       |       |       |       |       |       |       |       |
   | this  |       |       |       |       |       |       |       |       |
   | P     |       |       |       |       |       |       |       |       |
   | roced |       |       |       |       |       |       |       |       |
   | ure") |       |       |       |       |       |       |       |       |
   | >     |       |       |       |       |       |       |       |       |
   | (12   |       |       |       |       |       |       |       |       |
   | 8775, |       |       |       |       |       |       |       |       |
   | DCM,  |       |       |       |       |       |       |       |       |
   | "     |       |       |       |       |       |       |       |       |
   | Ident |       |       |       |       |       |       |       |       |
   | ifier |       |       |       |       |       |       |       |       |
   | w     |       |       |       |       |       |       |       |       |
   | ithin |       |       |       |       |       |       |       |       |
   | P     |       |       |       |       |       |       |       |       |
   | erson |       |       |       |       |       |       |       |       |
   | Obser |       |       |       |       |       |       |       |       |
   | ver's |       |       |       |       |       |       |       |       |
   | R     |       |       |       |       |       |       |       |       |
   | ole") |       |       |       |       |       |       |       |       |
   +-------+-------+-------+-------+-------+-------+-------+-------+-------+

.. _sect_Mapping_TID_1600:

Mapping of Image Library
''''''''''''''''''''''''

This section describes the mapping of .

.. table:: Mapping of Image Library

   +-------+-------+-------+-------+-------+-------+-------+-------+-------+
   | DICOM | DICOM | DICOM | DICOM | Gene  | AIM   | AIM   | AIM   | Co    |
   | SR    | VT    | VM    | Usage | rated | El    | Data  | Mu    | mment |
   | Path  |       |       | Type  | Value | ement | Type  | ltipl |       |
   |       |       |       |       |       | or    |       | icity |       |
   |       |       |       |       |       | Attr  |       |       |       |
   |       |       |       |       |       | ibute |       |       |       |
   +=======+=======+=======+=======+=======+=======+=======+=======+=======+
   | (12   | CONT  | 1     | M     |       |       |       |       |       |
   | 6000, | AINER |       |       |       |       |       |       |       |
   | DCM,  |       |       |       |       |       |       |       |       |
   | "Im   |       |       |       |       |       |       |       |       |
   | aging |       |       |       |       |       |       |       |       |
   | M     |       |       |       |       |       |       |       |       |
   | easur |       |       |       |       |       |       |       |       |
   | ement |       |       |       |       |       |       |       |       |
   | Rep   |       |       |       |       |       |       |       |       |
   | ort") |       |       |       |       |       |       |       |       |
   | >     |       |       |       |       |       |       |       |       |
   | (11   |       |       |       |       |       |       |       |       |
   | 1028, |       |       |       |       |       |       |       |       |
   | DCM,  |       |       |       |       |       |       |       |       |
   | "     |       |       |       |       |       |       |       |       |
   | Image |       |       |       |       |       |       |       |       |
   | Libr  |       |       |       |       |       |       |       |       |
   | ary") |       |       |       |       |       |       |       |       |
   +-------+-------+-------+-------+-------+-------+-------+-------+-------+
   | (12   | CONT  | 1-n   | U     |       | /Ima  |       |       | The   |
   | 6000, | AINER |       |       |       | ge​An |       |       | value |
   | DCM,  |       |       |       |       | notat |       |       | of    |
   | "Im   |       |       |       |       | ion​C |       |       | ai    |
   | aging |       |       |       |       | ollec |       |       | m:uni |
   | M     |       |       |       |       | tion/ |       |       | que​I |
   | easur |       |       |       |       | ​imag |       |       | denti |
   | ement |       |       |       |       | e​Ann |       |       | fier/ |
   | Rep   |       |       |       |       | otati |       |       | @root |
   | ort") |       |       |       |       | ons/​ |       |       | is    |
   | >     |       |       |       |       | Image |       |       | m     |
   | (11   |       |       |       |       | ​Anno |       |       | apped |
   | 1028, |       |       |       |       | tatio |       |       | to    |
   | DCM,  |       |       |       |       | n/​im |       |       | the   |
   | "     |       |       |       |       | ageRe |       |       | Obser |
   | Image |       |       |       |       | feren |       |       | vatio |
   | Libr  |       |       |       |       | ceEnt |       |       | n​UID |
   | ary") |       |       |       |       | ityCo |       |       | Attr  |
   | >     |       |       |       |       | llect |       |       | ibute |
   | (12   |       |       |       |       | ion/​ |       |       | of    |
   | 6200, |       |       |       |       | Image |       |       | the   |
   | DCM,  |       |       |       |       | Refer |       |       | CONTA |
   | "     |       |       |       |       | enceE |       |       | INER. |
   | Image |       |       |       |       | ntity |       |       |       |
   | Li    |       |       |       |       |       |       |       |       |
   | brary |       |       |       |       |       |       |       |       |
   | Gr    |       |       |       |       |       |       |       |       |
   | oup") |       |       |       |       |       |       |       |       |
   +-------+-------+-------+-------+-------+-------+-------+-------+-------+
   | (12   | IN    | 1     | U     | `Ma   |       |       |       |       |
   | 6000, | CLUDE |       |       | pping |       |       |       |       |
   | DCM,  |       |       |       | of    |       |       |       |       |
   | "Im   |       |       |       | Image |       |       |       |       |
   | aging |       |       |       | Li    |       |       |       |       |
   | M     |       |       |       | brary |       |       |       |       |
   | easur |       |       |       | Entry |       |       |       |       |
   | ement |       |       |       | Desc  |       |       |       |       |
   | Rep   |       |       |       | ripto |       |       |       |       |
   | ort") |       |       |       | rs <# |       |       |       |       |
   | >     |       |       |       | sect_ |       |       |       |       |
   | (11   |       |       |       | Mappi |       |       |       |       |
   | 1028, |       |       |       | ng_TI |       |       |       |       |
   | DCM,  |       |       |       | D_160 |       |       |       |       |
   | "     |       |       |       | 2>`__ |       |       |       |       |
   | Image |       |       |       |       |       |       |       |       |
   | Libr  |       |       |       |       |       |       |       |       |
   | ary") |       |       |       |       |       |       |       |       |
   | >     |       |       |       |       |       |       |       |       |
   | (12   |       |       |       |       |       |       |       |       |
   | 6200, |       |       |       |       |       |       |       |       |
   | DCM,  |       |       |       |       |       |       |       |       |
   | "     |       |       |       |       |       |       |       |       |
   | Image |       |       |       |       |       |       |       |       |
   | Li    |       |       |       |       |       |       |       |       |
   | brary |       |       |       |       |       |       |       |       |
   | Gr    |       |       |       |       |       |       |       |       |
   | oup") |       |       |       |       |       |       |       |       |
   | >     |       |       |       |       |       |       |       |       |
   +-------+-------+-------+-------+-------+-------+-------+-------+-------+
   | (12   | IN    | 1-n   | U     | `Ma   |       |       |       |       |
   | 6000, | CLUDE |       |       | pping |       |       |       |       |
   | DCM,  |       |       |       | of    |       |       |       |       |
   | "Im   |       |       |       | Image |       |       |       |       |
   | aging |       |       |       | Li    |       |       |       |       |
   | M     |       |       |       | brary |       |       |       |       |
   | easur |       |       |       | Ent   |       |       |       |       |
   | ement |       |       |       | ry <# |       |       |       |       |
   | Rep   |       |       |       | sect_ |       |       |       |       |
   | ort") |       |       |       | Mappi |       |       |       |       |
   | >     |       |       |       | ng_TI |       |       |       |       |
   | (11   |       |       |       | D_160 |       |       |       |       |
   | 1028, |       |       |       | 1>`__ |       |       |       |       |
   | DCM,  |       |       |       |       |       |       |       |       |
   | "     |       |       |       |       |       |       |       |       |
   | Image |       |       |       |       |       |       |       |       |
   | Libr  |       |       |       |       |       |       |       |       |
   | ary") |       |       |       |       |       |       |       |       |
   | >     |       |       |       |       |       |       |       |       |
   | (12   |       |       |       |       |       |       |       |       |
   | 6200, |       |       |       |       |       |       |       |       |
   | DCM,  |       |       |       |       |       |       |       |       |
   | "     |       |       |       |       |       |       |       |       |
   | Image |       |       |       |       |       |       |       |       |
   | Li    |       |       |       |       |       |       |       |       |
   | brary |       |       |       |       |       |       |       |       |
   | Gr    |       |       |       |       |       |       |       |       |
   | oup") |       |       |       |       |       |       |       |       |
   | >     |       |       |       |       |       |       |       |       |
   +-------+-------+-------+-------+-------+-------+-------+-------+-------+

.. _sect_Mapping_TID_1601:

Mapping of Image Library Entry
''''''''''''''''''''''''''''''

This section describes the mapping of .

.. table:: Mapping of Image Library Entry

   +-------+-------+-------+-------+-------+-------+-------+-------+-------+
   | DICOM | DICOM | DICOM | DICOM | Gene  | AIM   | AIM   | AIM   | Co    |
   | SR    | VT    | VM    | Usage | rated | El    | Data  | Mu    | mment |
   | Path  |       |       | Type  | Value | ement | Type  | ltipl |       |
   |       |       |       |       |       | or    |       | icity |       |
   |       |       |       |       |       | Attr  |       |       |       |
   |       |       |       |       |       | ibute |       |       |       |
   +=======+=======+=======+=======+=======+=======+=======+=======+=======+
   | (12   | IMAGE | 1     | M     |       | /Ima  | II,   | 1, 1  |       |
   | 6000, |       |       |       |       | ge​An | II    |       |       |
   | DCM,  |       |       |       |       | notat |       |       |       |
   | "Im   |       |       |       |       | ion​C |       |       |       |
   | aging |       |       |       |       | ollec |       |       |       |
   | M     |       |       |       |       | tion/ |       |       |       |
   | easur |       |       |       |       | ​imag |       |       |       |
   | ement |       |       |       |       | e​Ann |       |       |       |
   | Rep   |       |       |       |       | otati |       |       |       |
   | ort") |       |       |       |       | ons/​ |       |       |       |
   | >     |       |       |       |       | Image |       |       |       |
   | (11   |       |       |       |       | ​Anno |       |       |       |
   | 1028, |       |       |       |       | tatio |       |       |       |
   | DCM,  |       |       |       |       | n/​im |       |       |       |
   | "     |       |       |       |       | ageRe |       |       |       |
   | Image |       |       |       |       | feren |       |       |       |
   | Libr  |       |       |       |       | ceEnt |       |       |       |
   | ary") |       |       |       |       | ityCo |       |       |       |
   | >     |       |       |       |       | llect |       |       |       |
   | (12   |       |       |       |       | ion/​ |       |       |       |
   | 6200, |       |       |       |       | Image |       |       |       |
   | DCM,  |       |       |       |       | Refer |       |       |       |
   | "     |       |       |       |       | enceE |       |       |       |
   | Image |       |       |       |       | ntity |       |       |       |
   | Li    |       |       |       |       | /​ima |       |       |       |
   | brary |       |       |       |       | geStu |       |       |       |
   | Gr    |       |       |       |       | dy/​i |       |       |       |
   | oup") |       |       |       |       | mageS |       |       |       |
   | >     |       |       |       |       | eries |       |       |       |
   | IMAGE |       |       |       |       | /​ima |       |       |       |
   |       |       |       |       |       | ge​Co |       |       |       |
   |       |       |       |       |       | llect |       |       |       |
   |       |       |       |       |       | ion/​ |       |       |       |
   |       |       |       |       |       | Image |       |       |       |
   |       |       |       |       |       | /​sop |       |       |       |
   |       |       |       |       |       | Insta |       |       |       |
   |       |       |       |       |       | nceUi |       |       |       |
   |       |       |       |       |       | d/​@r |       |       |       |
   |       |       |       |       |       | oot​, |       |       |       |
   |       |       |       |       |       | sopC  |       |       |       |
   |       |       |       |       |       | lassU |       |       |       |
   |       |       |       |       |       | id/​@ |       |       |       |
   |       |       |       |       |       | root​ |       |       |       |
   +-------+-------+-------+-------+-------+-------+-------+-------+-------+
   | (12   | IN    | 1     | U     | `Ma   |       |       |       |       |
   | 6000, | CLUDE |       |       | pping |       |       |       |       |
   | DCM,  |       |       |       | of    |       |       |       |       |
   | "Im   |       |       |       | Image |       |       |       |       |
   | aging |       |       |       | Li    |       |       |       |       |
   | M     |       |       |       | brary |       |       |       |       |
   | easur |       |       |       | Entry |       |       |       |       |
   | ement |       |       |       | Desc  |       |       |       |       |
   | Rep   |       |       |       | ripto |       |       |       |       |
   | ort") |       |       |       | rs <# |       |       |       |       |
   | >     |       |       |       | sect_ |       |       |       |       |
   | (11   |       |       |       | Mappi |       |       |       |       |
   | 1028, |       |       |       | ng_TI |       |       |       |       |
   | DCM,  |       |       |       | D_160 |       |       |       |       |
   | "     |       |       |       | 2>`__ |       |       |       |       |
   | Image |       |       |       |       |       |       |       |       |
   | Libr  |       |       |       |       |       |       |       |       |
   | ary") |       |       |       |       |       |       |       |       |
   | >     |       |       |       |       |       |       |       |       |
   | (12   |       |       |       |       |       |       |       |       |
   | 6200, |       |       |       |       |       |       |       |       |
   | DCM,  |       |       |       |       |       |       |       |       |
   | "     |       |       |       |       |       |       |       |       |
   | Image |       |       |       |       |       |       |       |       |
   | Li    |       |       |       |       |       |       |       |       |
   | brary |       |       |       |       |       |       |       |       |
   | Gr    |       |       |       |       |       |       |       |       |
   | oup") |       |       |       |       |       |       |       |       |
   | >     |       |       |       |       |       |       |       |       |
   | IMAGE |       |       |       |       |       |       |       |       |
   | >     |       |       |       |       |       |       |       |       |
   +-------+-------+-------+-------+-------+-------+-------+-------+-------+

.. _sect_Mapping_TID_1602:

Mapping of Image Library Entry Descriptors
''''''''''''''''''''''''''''''''''''''''''

This section describes the mapping of .

.. table:: Mapping of Image Library Entry Descriptors

   +-------+-------+-------+-------+-------+-------+-------+-------+-------+
   | DICOM | DICOM | DICOM | DICOM | Gene  | AIM   | AIM   | AIM   | Co    |
   | SR    | VT    | VM    | Usage | rated | El    | Data  | Mu    | mment |
   | Path  |       |       | Type  | Value | ement | Type  | ltipl |       |
   |       |       |       |       |       | or    |       | icity |       |
   |       |       |       |       |       | Attr  |       |       |       |
   |       |       |       |       |       | ibute |       |       |       |
   +=======+=======+=======+=======+=======+=======+=======+=======+=======+
   | (12   | CODE  | 1     | U     |       | /     | CD    | 1..1  | AIM   |
   | 6000, |       |       |       |       | Image |       |       | does  |
   | DCM,  |       |       |       |       | ​Anno |       |       | not   |
   | "Im   |       |       |       |       | tatio |       |       | for   |
   | aging |       |       |       |       | n​Col |       |       | mally |
   | M     |       |       |       |       | lecti |       |       | d     |
   | easur |       |       |       |       | on/​i |       |       | efine |
   | ement |       |       |       |       | mage​ |       |       | a     |
   | Rep   |       |       |       |       | Annot |       |       | value |
   | ort") |       |       |       |       | ation |       |       | set   |
   | >     |       |       |       |       | s/​Im |       |       | but   |
   | (11   |       |       |       |       | age​A |       |       | c     |
   | 1028, |       |       |       |       | nnota |       |       | ommon |
   | DCM,  |       |       |       |       | tion/ |       |       | usage |
   | "     |       |       |       |       | ​imag |       |       | is    |
   | Image |       |       |       |       | eRefe |       |       | the   |
   | Libr  |       |       |       |       | rence |       |       | set   |
   | ary") |       |       |       |       | Entit |       |       | of    |
   | >     |       |       |       |       | yColl |       |       | code  |
   | (12   |       |       |       |       | ectio |       |       | st    |
   | 6200, |       |       |       |       | n/​Im |       |       | rings |
   | DCM,  |       |       |       |       | ageRe |       |       | de    |
   | "     |       |       |       |       | feren |       |       | fined |
   | Image |       |       |       |       | ceEnt |       |       | for   |
   | Li    |       |       |       |       | ity/​ |       |       | the   |
   | brary |       |       |       |       | image |       |       | image |
   | Gr    |       |       |       |       | Study |       |       | Mod   |
   | oup") |       |       |       |       | /​ima |       |       | ality |
   | >     |       |       |       |       | geSer |       |       | Attri |
   | (12   |       |       |       |       | ies/​ |       |       | bute, |
   | 1139, |       |       |       |       | modal |       |       | and   |
   | DCM,  |       |       |       |       | ity/​ |       |       | these |
   | "     |       |       |       |       | @code |       |       | have  |
   | Modal |       |       |       |       |       |       |       | a 1:1 |
   | ity") |       |       |       |       |       |       |       | corr  |
   |       |       |       |       |       |       |       |       | espon |
   |       |       |       |       |       |       |       |       | dence |
   |       |       |       |       |       |       |       |       | with  |
   |       |       |       |       |       |       |       |       | the   |
   |       |       |       |       |       |       |       |       | code  |
   |       |       |       |       |       |       |       |       | v     |
   |       |       |       |       |       |       |       |       | alues |
   |       |       |       |       |       |       |       |       | of .  |
   +-------+-------+-------+-------+-------+-------+-------+-------+-------+
   | (12   | CODE  | 1     | U     |       |       |       |       | Not   |
   | 6000, |       |       |       |       |       |       |       | used  |
   | DCM,  |       |       |       |       |       |       |       | in    |
   | "Im   |       |       |       |       |       |       |       | AIM;  |
   | aging |       |       |       |       |       |       |       | disc  |
   | M     |       |       |       |       |       |       |       | arded |
   | easur |       |       |       |       |       |       |       | if    |
   | ement |       |       |       |       |       |       |       | pr    |
   | Rep   |       |       |       |       |       |       |       | esent |
   | ort") |       |       |       |       |       |       |       | in    |
   | >     |       |       |       |       |       |       |       | DICOM |
   | (11   |       |       |       |       |       |       |       | SR.   |
   | 1028, |       |       |       |       |       |       |       |       |
   | DCM,  |       |       |       |       |       |       |       |       |
   | "     |       |       |       |       |       |       |       |       |
   | Image |       |       |       |       |       |       |       |       |
   | Libr  |       |       |       |       |       |       |       |       |
   | ary") |       |       |       |       |       |       |       |       |
   | >     |       |       |       |       |       |       |       |       |
   | (12   |       |       |       |       |       |       |       |       |
   | 6200, |       |       |       |       |       |       |       |       |
   | DCM,  |       |       |       |       |       |       |       |       |
   | "     |       |       |       |       |       |       |       |       |
   | Image |       |       |       |       |       |       |       |       |
   | Li    |       |       |       |       |       |       |       |       |
   | brary |       |       |       |       |       |       |       |       |
   | Gr    |       |       |       |       |       |       |       |       |
   | oup") |       |       |       |       |       |       |       |       |
   | >     |       |       |       |       |       |       |       |       |
   | (12   |       |       |       |       |       |       |       |       |
   | 3014, |       |       |       |       |       |       |       |       |
   | DCM,  |       |       |       |       |       |       |       |       |
   | "T    |       |       |       |       |       |       |       |       |
   | arget |       |       |       |       |       |       |       |       |
   | Reg   |       |       |       |       |       |       |       |       |
   | ion") |       |       |       |       |       |       |       |       |
   +-------+-------+-------+-------+-------+-------+-------+-------+-------+
   | (12   | CODE  | 1     | U     |       |       |       |       | Not   |
   | 6000, |       |       |       |       |       |       |       | used  |
   | DCM,  |       |       |       |       |       |       |       | in    |
   | "Im   |       |       |       |       |       |       |       | AIM;  |
   | aging |       |       |       |       |       |       |       | disc  |
   | M     |       |       |       |       |       |       |       | arded |
   | easur |       |       |       |       |       |       |       | if    |
   | ement |       |       |       |       |       |       |       | pr    |
   | Rep   |       |       |       |       |       |       |       | esent |
   | ort") |       |       |       |       |       |       |       | in    |
   | >     |       |       |       |       |       |       |       | DICOM |
   | (11   |       |       |       |       |       |       |       | SR.   |
   | 1028, |       |       |       |       |       |       |       |       |
   | DCM,  |       |       |       |       |       |       |       |       |
   | "     |       |       |       |       |       |       |       |       |
   | Image |       |       |       |       |       |       |       |       |
   | Libr  |       |       |       |       |       |       |       |       |
   | ary") |       |       |       |       |       |       |       |       |
   | >     |       |       |       |       |       |       |       |       |
   | (12   |       |       |       |       |       |       |       |       |
   | 6200, |       |       |       |       |       |       |       |       |
   | DCM,  |       |       |       |       |       |       |       |       |
   | "     |       |       |       |       |       |       |       |       |
   | Image |       |       |       |       |       |       |       |       |
   | Li    |       |       |       |       |       |       |       |       |
   | brary |       |       |       |       |       |       |       |       |
   | Gr    |       |       |       |       |       |       |       |       |
   | oup") |       |       |       |       |       |       |       |       |
   | >     |       |       |       |       |       |       |       |       |
   | (11   |       |       |       |       |       |       |       |       |
   | 1027, |       |       |       |       |       |       |       |       |
   | DCM,  |       |       |       |       |       |       |       |       |
   | "     |       |       |       |       |       |       |       |       |
   | Image |       |       |       |       |       |       |       |       |
   | La    |       |       |       |       |       |       |       |       |
   | teral |       |       |       |       |       |       |       |       |
   | ity") |       |       |       |       |       |       |       |       |
   +-------+-------+-------+-------+-------+-------+-------+-------+-------+
   | 12    | TEXT  | 1     | U     |       | /Im   | ST    | 0..1  |       |
   | 6000, |       |       |       |       | age​A |       |       |       |
   | DCM,  |       |       |       |       | nnota |       |       |       |
   | "Im   |       |       |       |       | tion​ |       |       |       |
   | aging |       |       |       |       | Colle |       |       |       |
   | M     |       |       |       |       | ction |       |       |       |
   | easur |       |       |       |       | /​ima |       |       |       |
   | ement |       |       |       |       | ge​An |       |       |       |
   | Rep   |       |       |       |       | notat |       |       |       |
   | ort") |       |       |       |       | ions/ |       |       |       |
   | >     |       |       |       |       | ​Imag |       |       |       |
   | (11   |       |       |       |       | e​Ann |       |       |       |
   | 1028, |       |       |       |       | otati |       |       |       |
   | DCM,  |       |       |       |       | on/​i |       |       |       |
   | "     |       |       |       |       | mage​ |       |       |       |
   | Image |       |       |       |       | Refer |       |       |       |
   | Libr  |       |       |       |       | ence​ |       |       |       |
   | ary") |       |       |       |       | Entit |       |       |       |
   | >     |       |       |       |       | y​Col |       |       |       |
   | (12   |       |       |       |       | lecti |       |       |       |
   | 6200, |       |       |       |       | on/​I |       |       |       |
   | DCM,  |       |       |       |       | mage​ |       |       |       |
   | "     |       |       |       |       | Refer |       |       |       |
   | Image |       |       |       |       | ence​ |       |       |       |
   | Li    |       |       |       |       | Entit |       |       |       |
   | brary |       |       |       |       | y/​im |       |       |       |
   | Gr    |       |       |       |       | age​S |       |       |       |
   | oup") |       |       |       |       | tudy/ |       |       |       |
   | >(12  |       |       |       |       | ​acce |       |       |       |
   | 1022, |       |       |       |       | ssion |       |       |       |
   | DCM,  |       |       |       |       | ​Numb |       |       |       |
   | "Acce |       |       |       |       | er/​@ |       |       |       |
   | ssion |       |       |       |       | value |       |       |       |
   | Num   |       |       |       |       |       |       |       |       |
   | ber") |       |       |       |       |       |       |       |       |
   +-------+-------+-------+-------+-------+-------+-------+-------+-------+
   | (12   | DATE  | 1     | U     |       | /Imag | TS    | 1..1  |       |
   | 6000, |       |       |       |       | e​Ann |       |       |       |
   | DCM,  |       |       |       |       | otati |       |       |       |
   | "Im   |       |       |       |       | on​Co |       |       |       |
   | aging |       |       |       |       | llect |       |       |       |
   | M     |       |       |       |       | ion/​ |       |       |       |
   | easur |       |       |       |       | image |       |       |       |
   | ement |       |       |       |       | ​Anno |       |       |       |
   | Rep   |       |       |       |       | tatio |       |       |       |
   | ort") |       |       |       |       | ns/​I |       |       |       |
   | >     |       |       |       |       | mage​ |       |       |       |
   | (11   |       |       |       |       | Annot |       |       |       |
   | 1028, |       |       |       |       | ation |       |       |       |
   | DCM,  |       |       |       |       | /​ima |       |       |       |
   | "     |       |       |       |       | geRef |       |       |       |
   | Image |       |       |       |       | erenc |       |       |       |
   | Libr  |       |       |       |       | eEnti |       |       |       |
   | ary") |       |       |       |       | tyCol |       |       |       |
   | >     |       |       |       |       | lecti |       |       |       |
   | (12   |       |       |       |       | on/​I |       |       |       |
   | 6200, |       |       |       |       | mageR |       |       |       |
   | DCM,  |       |       |       |       | efere |       |       |       |
   | "     |       |       |       |       | nceEn |       |       |       |
   | Image |       |       |       |       | tity/ |       |       |       |
   | Li    |       |       |       |       | ​imag |       |       |       |
   | brary |       |       |       |       | eStud |       |       |       |
   | Gr    |       |       |       |       | y/​st |       |       |       |
   | oup") |       |       |       |       | artDa |       |       |       |
   | >     |       |       |       |       | te/​@ |       |       |       |
   | (11   |       |       |       |       | value |       |       |       |
   | 1060, |       |       |       |       |       |       |       |       |
   | DCM,  |       |       |       |       |       |       |       |       |
   | "     |       |       |       |       |       |       |       |       |
   | Study |       |       |       |       |       |       |       |       |
   | D     |       |       |       |       |       |       |       |       |
   | ate") |       |       |       |       |       |       |       |       |
   +-------+-------+-------+-------+-------+-------+-------+-------+-------+
   | (12   | TIME  | 1     | U     |       | /Imag | TS    | 1..1  |       |
   | 6000, |       |       |       |       | e​Ann |       |       |       |
   | DCM,  |       |       |       |       | otati |       |       |       |
   | "Im   |       |       |       |       | on​Co |       |       |       |
   | aging |       |       |       |       | llect |       |       |       |
   | M     |       |       |       |       | ion/​ |       |       |       |
   | easur |       |       |       |       | image |       |       |       |
   | ement |       |       |       |       | ​Anno |       |       |       |
   | Rep   |       |       |       |       | tatio |       |       |       |
   | ort") |       |       |       |       | ns/​I |       |       |       |
   | >     |       |       |       |       | mage​ |       |       |       |
   | (11   |       |       |       |       | Annot |       |       |       |
   | 1028, |       |       |       |       | ation |       |       |       |
   | DCM,  |       |       |       |       | /​ima |       |       |       |
   | "     |       |       |       |       | geRef |       |       |       |
   | Image |       |       |       |       | erenc |       |       |       |
   | Libr  |       |       |       |       | eEnti |       |       |       |
   | ary") |       |       |       |       | tyCol |       |       |       |
   | >     |       |       |       |       | lecti |       |       |       |
   | (12   |       |       |       |       | on/​I |       |       |       |
   | 6200, |       |       |       |       | mageR |       |       |       |
   | DCM,  |       |       |       |       | efere |       |       |       |
   | "     |       |       |       |       | nceEn |       |       |       |
   | Image |       |       |       |       | tity/ |       |       |       |
   | Li    |       |       |       |       | ​imag |       |       |       |
   | brary |       |       |       |       | eStud |       |       |       |
   | Gr    |       |       |       |       | y/​st |       |       |       |
   | oup") |       |       |       |       | artTi |       |       |       |
   | >     |       |       |       |       | me/​@ |       |       |       |
   | (11   |       |       |       |       | value |       |       |       |
   | 1061, |       |       |       |       |       |       |       |       |
   | DCM,  |       |       |       |       |       |       |       |       |
   | "     |       |       |       |       |       |       |       |       |
   | Study |       |       |       |       |       |       |       |       |
   | T     |       |       |       |       |       |       |       |       |
   | ime") |       |       |       |       |       |       |       |       |
   +-------+-------+-------+-------+-------+-------+-------+-------+-------+
   | (12   | DATE  | 1     | U     |       |       |       |       | Not   |
   | 6000, |       |       |       |       |       |       |       | used  |
   | DCM,  |       |       |       |       |       |       |       | in    |
   | "Im   |       |       |       |       |       |       |       | AIM;  |
   | aging |       |       |       |       |       |       |       | disc  |
   | M     |       |       |       |       |       |       |       | arded |
   | easur |       |       |       |       |       |       |       | if    |
   | ement |       |       |       |       |       |       |       | pr    |
   | Rep   |       |       |       |       |       |       |       | esent |
   | ort") |       |       |       |       |       |       |       | in    |
   | >     |       |       |       |       |       |       |       | DICOM |
   | (11   |       |       |       |       |       |       |       | SR.   |
   | 1028, |       |       |       |       |       |       |       |       |
   | DCM,  |       |       |       |       |       |       |       |       |
   | "     |       |       |       |       |       |       |       |       |
   | Image |       |       |       |       |       |       |       |       |
   | Libr  |       |       |       |       |       |       |       |       |
   | ary") |       |       |       |       |       |       |       |       |
   | >     |       |       |       |       |       |       |       |       |
   | (12   |       |       |       |       |       |       |       |       |
   | 6200, |       |       |       |       |       |       |       |       |
   | DCM,  |       |       |       |       |       |       |       |       |
   | "     |       |       |       |       |       |       |       |       |
   | Image |       |       |       |       |       |       |       |       |
   | Li    |       |       |       |       |       |       |       |       |
   | brary |       |       |       |       |       |       |       |       |
   | Gr    |       |       |       |       |       |       |       |       |
   | oup") |       |       |       |       |       |       |       |       |
   | >     |       |       |       |       |       |       |       |       |
   | (11   |       |       |       |       |       |       |       |       |
   | 1018, |       |       |       |       |       |       |       |       |
   | DCM,  |       |       |       |       |       |       |       |       |
   | "Co   |       |       |       |       |       |       |       |       |
   | ntent |       |       |       |       |       |       |       |       |
   | D     |       |       |       |       |       |       |       |       |
   | ate") |       |       |       |       |       |       |       |       |
   +-------+-------+-------+-------+-------+-------+-------+-------+-------+
   | (12   | TIME  | 1     | U     |       |       |       |       | Not   |
   | 6000, |       |       |       |       |       |       |       | used  |
   | DCM,  |       |       |       |       |       |       |       | in    |
   | "Im   |       |       |       |       |       |       |       | AIM;  |
   | aging |       |       |       |       |       |       |       | disc  |
   | M     |       |       |       |       |       |       |       | arded |
   | easur |       |       |       |       |       |       |       | if    |
   | ement |       |       |       |       |       |       |       | pr    |
   | Rep   |       |       |       |       |       |       |       | esent |
   | ort") |       |       |       |       |       |       |       | in    |
   | >     |       |       |       |       |       |       |       | DICOM |
   | (11   |       |       |       |       |       |       |       | SR.   |
   | 1028, |       |       |       |       |       |       |       |       |
   | DCM,  |       |       |       |       |       |       |       |       |
   | "     |       |       |       |       |       |       |       |       |
   | Image |       |       |       |       |       |       |       |       |
   | Libr  |       |       |       |       |       |       |       |       |
   | ary") |       |       |       |       |       |       |       |       |
   | >     |       |       |       |       |       |       |       |       |
   | (12   |       |       |       |       |       |       |       |       |
   | 6200, |       |       |       |       |       |       |       |       |
   | DCM,  |       |       |       |       |       |       |       |       |
   | "     |       |       |       |       |       |       |       |       |
   | Image |       |       |       |       |       |       |       |       |
   | Li    |       |       |       |       |       |       |       |       |
   | brary |       |       |       |       |       |       |       |       |
   | Gr    |       |       |       |       |       |       |       |       |
   | oup") |       |       |       |       |       |       |       |       |
   | >     |       |       |       |       |       |       |       |       |
   | (11   |       |       |       |       |       |       |       |       |
   | 1019, |       |       |       |       |       |       |       |       |
   | DCM,  |       |       |       |       |       |       |       |       |
   | "Co   |       |       |       |       |       |       |       |       |
   | ntent |       |       |       |       |       |       |       |       |
   | T     |       |       |       |       |       |       |       |       |
   | ime") |       |       |       |       |       |       |       |       |
   +-------+-------+-------+-------+-------+-------+-------+-------+-------+
   | (12   | DATE  | 1     | U     |       |       |       |       | Not   |
   | 6000, |       |       |       |       |       |       |       | used  |
   | DCM,  |       |       |       |       |       |       |       | in    |
   | "Im   |       |       |       |       |       |       |       | AIM;  |
   | aging |       |       |       |       |       |       |       | disc  |
   | M     |       |       |       |       |       |       |       | arded |
   | easur |       |       |       |       |       |       |       | if    |
   | ement |       |       |       |       |       |       |       | pr    |
   | Rep   |       |       |       |       |       |       |       | esent |
   | ort") |       |       |       |       |       |       |       | in    |
   | >     |       |       |       |       |       |       |       | DICOM |
   | (11   |       |       |       |       |       |       |       | SR.   |
   | 1028, |       |       |       |       |       |       |       |       |
   | DCM,  |       |       |       |       |       |       |       |       |
   | "     |       |       |       |       |       |       |       |       |
   | Image |       |       |       |       |       |       |       |       |
   | Libr  |       |       |       |       |       |       |       |       |
   | ary") |       |       |       |       |       |       |       |       |
   | >     |       |       |       |       |       |       |       |       |
   | (12   |       |       |       |       |       |       |       |       |
   | 6200, |       |       |       |       |       |       |       |       |
   | DCM,  |       |       |       |       |       |       |       |       |
   | "     |       |       |       |       |       |       |       |       |
   | Image |       |       |       |       |       |       |       |       |
   | Li    |       |       |       |       |       |       |       |       |
   | brary |       |       |       |       |       |       |       |       |
   | Gr    |       |       |       |       |       |       |       |       |
   | oup") |       |       |       |       |       |       |       |       |
   | >     |       |       |       |       |       |       |       |       |
   | (12   |       |       |       |       |       |       |       |       |
   | 6201, |       |       |       |       |       |       |       |       |
   | DCM,  |       |       |       |       |       |       |       |       |
   | "A    |       |       |       |       |       |       |       |       |
   | cquis |       |       |       |       |       |       |       |       |
   | ition |       |       |       |       |       |       |       |       |
   | D     |       |       |       |       |       |       |       |       |
   | ate") |       |       |       |       |       |       |       |       |
   +-------+-------+-------+-------+-------+-------+-------+-------+-------+
   | (12   | TIME  | 1     | U     |       |       |       |       | Not   |
   | 6000, |       |       |       |       |       |       |       | used  |
   | DCM,  |       |       |       |       |       |       |       | in    |
   | "Im   |       |       |       |       |       |       |       | AIM;  |
   | aging |       |       |       |       |       |       |       | disc  |
   | M     |       |       |       |       |       |       |       | arded |
   | easur |       |       |       |       |       |       |       | if    |
   | ement |       |       |       |       |       |       |       | pr    |
   | Rep   |       |       |       |       |       |       |       | esent |
   | ort") |       |       |       |       |       |       |       | in    |
   | >     |       |       |       |       |       |       |       | DICOM |
   | (11   |       |       |       |       |       |       |       | SR.   |
   | 1028, |       |       |       |       |       |       |       |       |
   | DCM,  |       |       |       |       |       |       |       |       |
   | "     |       |       |       |       |       |       |       |       |
   | Image |       |       |       |       |       |       |       |       |
   | Libr  |       |       |       |       |       |       |       |       |
   | ary") |       |       |       |       |       |       |       |       |
   | >     |       |       |       |       |       |       |       |       |
   | (12   |       |       |       |       |       |       |       |       |
   | 6200, |       |       |       |       |       |       |       |       |
   | DCM,  |       |       |       |       |       |       |       |       |
   | "     |       |       |       |       |       |       |       |       |
   | Image |       |       |       |       |       |       |       |       |
   | Li    |       |       |       |       |       |       |       |       |
   | brary |       |       |       |       |       |       |       |       |
   | Gr    |       |       |       |       |       |       |       |       |
   | oup") |       |       |       |       |       |       |       |       |
   | >     |       |       |       |       |       |       |       |       |
   | (12   |       |       |       |       |       |       |       |       |
   | 6202, |       |       |       |       |       |       |       |       |
   | DCM,  |       |       |       |       |       |       |       |       |
   | "A    |       |       |       |       |       |       |       |       |
   | cquis |       |       |       |       |       |       |       |       |
   | ition |       |       |       |       |       |       |       |       |
   | T     |       |       |       |       |       |       |       |       |
   | ime") |       |       |       |       |       |       |       |       |
   +-------+-------+-------+-------+-------+-------+-------+-------+-------+
   | (12   | U     | 1     | U     |       |       |       |       | Not   |
   | 6000, | IDREF |       |       |       |       |       |       | used  |
   | DCM,  |       |       |       |       |       |       |       | in    |
   | "Im   |       |       |       |       |       |       |       | AIM;  |
   | aging |       |       |       |       |       |       |       | disc  |
   | M     |       |       |       |       |       |       |       | arded |
   | easur |       |       |       |       |       |       |       | if    |
   | ement |       |       |       |       |       |       |       | pr    |
   | Rep   |       |       |       |       |       |       |       | esent |
   | ort") |       |       |       |       |       |       |       | in    |
   | >     |       |       |       |       |       |       |       | DICOM |
   | (11   |       |       |       |       |       |       |       | SR.   |
   | 1028, |       |       |       |       |       |       |       |       |
   | DCM,  |       |       |       |       |       |       |       |       |
   | "     |       |       |       |       |       |       |       |       |
   | Image |       |       |       |       |       |       |       |       |
   | Libr  |       |       |       |       |       |       |       |       |
   | ary") |       |       |       |       |       |       |       |       |
   | >     |       |       |       |       |       |       |       |       |
   | (12   |       |       |       |       |       |       |       |       |
   | 6200, |       |       |       |       |       |       |       |       |
   | DCM,  |       |       |       |       |       |       |       |       |
   | "     |       |       |       |       |       |       |       |       |
   | Image |       |       |       |       |       |       |       |       |
   | Li    |       |       |       |       |       |       |       |       |
   | brary |       |       |       |       |       |       |       |       |
   | Gr    |       |       |       |       |       |       |       |       |
   | oup") |       |       |       |       |       |       |       |       |
   | >     |       |       |       |       |       |       |       |       |
   | (11   |       |       |       |       |       |       |       |       |
   | 2227, |       |       |       |       |       |       |       |       |
   | DCM,  |       |       |       |       |       |       |       |       |
   | "     |       |       |       |       |       |       |       |       |
   | Frame |       |       |       |       |       |       |       |       |
   | of    |       |       |       |       |       |       |       |       |
   | Refe  |       |       |       |       |       |       |       |       |
   | rence |       |       |       |       |       |       |       |       |
   | UID") |       |       |       |       |       |       |       |       |
   +-------+-------+-------+-------+-------+-------+-------+-------+-------+
   | (12   | NUM   | 1     | U     |       |       |       |       | Not   |
   | 6000, |       |       |       |       |       |       |       | used  |
   | DCM,  |       |       |       |       |       |       |       | in    |
   | "Im   |       |       |       |       |       |       |       | AIM;  |
   | aging |       |       |       |       |       |       |       | disc  |
   | M     |       |       |       |       |       |       |       | arded |
   | easur |       |       |       |       |       |       |       | if    |
   | ement |       |       |       |       |       |       |       | pr    |
   | Rep   |       |       |       |       |       |       |       | esent |
   | ort") |       |       |       |       |       |       |       | in    |
   | >     |       |       |       |       |       |       |       | DICOM |
   | (11   |       |       |       |       |       |       |       | SR.   |
   | 1028, |       |       |       |       |       |       |       |       |
   | DCM,  |       |       |       |       |       |       |       |       |
   | "     |       |       |       |       |       |       |       |       |
   | Image |       |       |       |       |       |       |       |       |
   | Libr  |       |       |       |       |       |       |       |       |
   | ary") |       |       |       |       |       |       |       |       |
   | >     |       |       |       |       |       |       |       |       |
   | (12   |       |       |       |       |       |       |       |       |
   | 6200, |       |       |       |       |       |       |       |       |
   | DCM,  |       |       |       |       |       |       |       |       |
   | "     |       |       |       |       |       |       |       |       |
   | Image |       |       |       |       |       |       |       |       |
   | Li    |       |       |       |       |       |       |       |       |
   | brary |       |       |       |       |       |       |       |       |
   | Gr    |       |       |       |       |       |       |       |       |
   | oup") |       |       |       |       |       |       |       |       |
   | >     |       |       |       |       |       |       |       |       |
   | (11   |       |       |       |       |       |       |       |       |
   | 0910, |       |       |       |       |       |       |       |       |
   | DCM,  |       |       |       |       |       |       |       |       |
   | "     |       |       |       |       |       |       |       |       |
   | Pixel |       |       |       |       |       |       |       |       |
   | Data  |       |       |       |       |       |       |       |       |
   | R     |       |       |       |       |       |       |       |       |
   | ows") |       |       |       |       |       |       |       |       |
   +-------+-------+-------+-------+-------+-------+-------+-------+-------+
   | (12   | NUM   | 1     | U     |       |       |       |       | Not   |
   | 6000, |       |       |       |       |       |       |       | used  |
   | DCM,  |       |       |       |       |       |       |       | in    |
   | "Im   |       |       |       |       |       |       |       | AIM;  |
   | aging |       |       |       |       |       |       |       | disc  |
   | M     |       |       |       |       |       |       |       | arded |
   | easur |       |       |       |       |       |       |       | if    |
   | ement |       |       |       |       |       |       |       | pr    |
   | Rep   |       |       |       |       |       |       |       | esent |
   | ort") |       |       |       |       |       |       |       | in    |
   | >     |       |       |       |       |       |       |       | DICOM |
   | (11   |       |       |       |       |       |       |       | SR.   |
   | 1028, |       |       |       |       |       |       |       |       |
   | DCM,  |       |       |       |       |       |       |       |       |
   | "     |       |       |       |       |       |       |       |       |
   | Image |       |       |       |       |       |       |       |       |
   | Libr  |       |       |       |       |       |       |       |       |
   | ary") |       |       |       |       |       |       |       |       |
   | >     |       |       |       |       |       |       |       |       |
   | (12   |       |       |       |       |       |       |       |       |
   | 6200, |       |       |       |       |       |       |       |       |
   | DCM,  |       |       |       |       |       |       |       |       |
   | "     |       |       |       |       |       |       |       |       |
   | Image |       |       |       |       |       |       |       |       |
   | Li    |       |       |       |       |       |       |       |       |
   | brary |       |       |       |       |       |       |       |       |
   | Gr    |       |       |       |       |       |       |       |       |
   | oup") |       |       |       |       |       |       |       |       |
   | >     |       |       |       |       |       |       |       |       |
   | (11   |       |       |       |       |       |       |       |       |
   | 0911, |       |       |       |       |       |       |       |       |
   | DCM,  |       |       |       |       |       |       |       |       |
   | "     |       |       |       |       |       |       |       |       |
   | Pixel |       |       |       |       |       |       |       |       |
   | Data  |       |       |       |       |       |       |       |       |
   | Colu  |       |       |       |       |       |       |       |       |
   | mns") |       |       |       |       |       |       |       |       |
   +-------+-------+-------+-------+-------+-------+-------+-------+-------+
   | (12   | IN    | 1     | U     | TID   | Not   |       |       |       |
   | 6000, | CLUDE |       |       | 1603  | used  |       |       |       |
   | DCM,  |       |       |       | "     | in    |       |       |       |
   | "Im   |       |       |       | Image | AIM;  |       |       |       |
   | aging |       |       |       | Li    | disc  |       |       |       |
   | M     |       |       |       | brary | arded |       |       |       |
   | easur |       |       |       | Entry | if    |       |       |       |
   | ement |       |       |       | D     | pr    |       |       |       |
   | Rep   |       |       |       | escri | esent |       |       |       |
   | ort") |       |       |       | ptors | in    |       |       |       |
   | >     |       |       |       | for   | DICOM |       |       |       |
   | (11   |       |       |       | Proje | SR.   |       |       |       |
   | 1028, |       |       |       | ction |       |       |       |       |
   | DCM,  |       |       |       | Ra    |       |       |       |       |
   | "     |       |       |       | diogr |       |       |       |       |
   | Image |       |       |       | aphy" |       |       |       |       |
   | Libr  |       |       |       |       |       |       |       |       |
   | ary") |       |       |       |       |       |       |       |       |
   | >     |       |       |       |       |       |       |       |       |
   | (12   |       |       |       |       |       |       |       |       |
   | 6200, |       |       |       |       |       |       |       |       |
   | DCM,  |       |       |       |       |       |       |       |       |
   | "     |       |       |       |       |       |       |       |       |
   | Image |       |       |       |       |       |       |       |       |
   | Li    |       |       |       |       |       |       |       |       |
   | brary |       |       |       |       |       |       |       |       |
   | Gr    |       |       |       |       |       |       |       |       |
   | oup") |       |       |       |       |       |       |       |       |
   | >     |       |       |       |       |       |       |       |       |
   +-------+-------+-------+-------+-------+-------+-------+-------+-------+
   | (12   | IN    | 1     | U     | TID   | Not   |       |       |       |
   | 6000, | CLUDE |       |       | 1604  | used  |       |       |       |
   | DCM,  |       |       |       | "     | in    |       |       |       |
   | "Im   |       |       |       | Image | AIM;  |       |       |       |
   | aging |       |       |       | Li    | disc  |       |       |       |
   | M     |       |       |       | brary | arded |       |       |       |
   | easur |       |       |       | Entry | if    |       |       |       |
   | ement |       |       |       | D     | pr    |       |       |       |
   | Rep   |       |       |       | escri | esent |       |       |       |
   | ort") |       |       |       | ptors | in    |       |       |       |
   | >     |       |       |       | for   | DICOM |       |       |       |
   | (11   |       |       |       | Cross | SR.   |       |       |       |
   | 1028, |       |       |       | -Sect |       |       |       |       |
   | DCM,  |       |       |       | ional |       |       |       |       |
   | "     |       |       |       | M     |       |       |       |       |
   | Image |       |       |       | odali |       |       |       |       |
   | Libr  |       |       |       | ties" |       |       |       |       |
   | ary") |       |       |       |       |       |       |       |       |
   | >     |       |       |       |       |       |       |       |       |
   | (12   |       |       |       |       |       |       |       |       |
   | 6200, |       |       |       |       |       |       |       |       |
   | DCM,  |       |       |       |       |       |       |       |       |
   | "     |       |       |       |       |       |       |       |       |
   | Image |       |       |       |       |       |       |       |       |
   | Li    |       |       |       |       |       |       |       |       |
   | brary |       |       |       |       |       |       |       |       |
   | Gr    |       |       |       |       |       |       |       |       |
   | oup") |       |       |       |       |       |       |       |       |
   | >     |       |       |       |       |       |       |       |       |
   +-------+-------+-------+-------+-------+-------+-------+-------+-------+
   | (12   | IN    | 1     | U     | TID   | Not   |       |       |       |
   | 6000, | CLUDE |       |       | 1605  | used  |       |       |       |
   | DCM,  |       |       |       | "     | in    |       |       |       |
   | "Im   |       |       |       | Image | AIM;  |       |       |       |
   | aging |       |       |       | Li    | disc  |       |       |       |
   | M     |       |       |       | brary | arded |       |       |       |
   | easur |       |       |       | Entry | if    |       |       |       |
   | ement |       |       |       | D     | pr    |       |       |       |
   | Rep   |       |       |       | escri | esent |       |       |       |
   | ort") |       |       |       | ptors | in    |       |       |       |
   | >     |       |       |       | for   | DICOM |       |       |       |
   | (11   |       |       |       | CT"   | SR.   |       |       |       |
   | 1028, |       |       |       |       |       |       |       |       |
   | DCM,  |       |       |       |       |       |       |       |       |
   | "     |       |       |       |       |       |       |       |       |
   | Image |       |       |       |       |       |       |       |       |
   | Libr  |       |       |       |       |       |       |       |       |
   | ary") |       |       |       |       |       |       |       |       |
   | >     |       |       |       |       |       |       |       |       |
   | (12   |       |       |       |       |       |       |       |       |
   | 6200, |       |       |       |       |       |       |       |       |
   | DCM,  |       |       |       |       |       |       |       |       |
   | "     |       |       |       |       |       |       |       |       |
   | Image |       |       |       |       |       |       |       |       |
   | Li    |       |       |       |       |       |       |       |       |
   | brary |       |       |       |       |       |       |       |       |
   | Gr    |       |       |       |       |       |       |       |       |
   | oup") |       |       |       |       |       |       |       |       |
   | >     |       |       |       |       |       |       |       |       |
   +-------+-------+-------+-------+-------+-------+-------+-------+-------+
   | (12   | IN    | 1     | U     | TID   | Not   |       |       |       |
   | 6000, | CLUDE |       |       | 1606  | used  |       |       |       |
   | DCM,  |       |       |       | "     | in    |       |       |       |
   | "Im   |       |       |       | Image | AIM;  |       |       |       |
   | aging |       |       |       | Li    | disc  |       |       |       |
   | M     |       |       |       | brary | arded |       |       |       |
   | easur |       |       |       | Entry | if    |       |       |       |
   | ement |       |       |       | D     | pr    |       |       |       |
   | Rep   |       |       |       | escri | esent |       |       |       |
   | ort") |       |       |       | ptors | in    |       |       |       |
   | >     |       |       |       | for   | DICOM |       |       |       |
   | (11   |       |       |       | MR"   | SR.   |       |       |       |
   | 1028, |       |       |       |       |       |       |       |       |
   | DCM,  |       |       |       |       |       |       |       |       |
   | "     |       |       |       |       |       |       |       |       |
   | Image |       |       |       |       |       |       |       |       |
   | Libr  |       |       |       |       |       |       |       |       |
   | ary") |       |       |       |       |       |       |       |       |
   | >     |       |       |       |       |       |       |       |       |
   | (12   |       |       |       |       |       |       |       |       |
   | 6200, |       |       |       |       |       |       |       |       |
   | DCM,  |       |       |       |       |       |       |       |       |
   | "     |       |       |       |       |       |       |       |       |
   | Image |       |       |       |       |       |       |       |       |
   | Li    |       |       |       |       |       |       |       |       |
   | brary |       |       |       |       |       |       |       |       |
   | Gr    |       |       |       |       |       |       |       |       |
   | oup") |       |       |       |       |       |       |       |       |
   | >     |       |       |       |       |       |       |       |       |
   +-------+-------+-------+-------+-------+-------+-------+-------+-------+
   | (12   | IN    | 1     | U     | TID   | Not   |       |       |       |
   | 6000, | CLUDE |       |       | 1607  | used  |       |       |       |
   | DCM,  |       |       |       | "     | in    |       |       |       |
   | "Im   |       |       |       | Image | AIM;  |       |       |       |
   | aging |       |       |       | Li    | disc  |       |       |       |
   | M     |       |       |       | brary | arded |       |       |       |
   | easur |       |       |       | Entry | if    |       |       |       |
   | ement |       |       |       | D     | pr    |       |       |       |
   | Rep   |       |       |       | escri | esent |       |       |       |
   | ort") |       |       |       | ptors | in    |       |       |       |
   | >     |       |       |       | for   | DICOM |       |       |       |
   | (11   |       |       |       | PET"  | SR.   |       |       |       |
   | 1028, |       |       |       |       |       |       |       |       |
   | DCM,  |       |       |       |       |       |       |       |       |
   | "     |       |       |       |       |       |       |       |       |
   | Image |       |       |       |       |       |       |       |       |
   | Libr  |       |       |       |       |       |       |       |       |
   | ary") |       |       |       |       |       |       |       |       |
   | >     |       |       |       |       |       |       |       |       |
   | (12   |       |       |       |       |       |       |       |       |
   | 6200, |       |       |       |       |       |       |       |       |
   | DCM,  |       |       |       |       |       |       |       |       |
   | "     |       |       |       |       |       |       |       |       |
   | Image |       |       |       |       |       |       |       |       |
   | Li    |       |       |       |       |       |       |       |       |
   | brary |       |       |       |       |       |       |       |       |
   | Gr    |       |       |       |       |       |       |       |       |
   | oup") |       |       |       |       |       |       |       |       |
   | >     |       |       |       |       |       |       |       |       |
   +-------+-------+-------+-------+-------+-------+-------+-------+-------+

.. _sect_A.7:

Sample Documents
----------------

This section describes a sample AIM v4.2 instance and the same content
transformed into a DICOM SR TID 1500 instance.

.. _sect_A.7.1:

Source AIM v4 Instance
~~~~~~~~~~~~~~~~~~~~~~

::

   <?xml version="1.0" encoding="UTF-8"?>
   <ImageAnnotationCollection xmlns="gme://caCORE.caCORE/4.4/edu.northwestern.radiology.AIM" xmlns:rdf="http://www.w3.org/1999/02/22-rdf-syntax-ns#" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" aimVersion="AIMv4_2" xsi:schemaLocation="gme://caCORE.caCORE/4.4/edu.northwestern.radiology.AIM AIM_v4.2_rv2_XML.xsd">
       <uniqueIdentifier root="2.25.224793923339609181243139195858254344686"/>
       <studyInstanceUid root="2.25.80159168229010751652502576830057032194"/>
       <seriesInstanceUid root="2.25.323817225444021135415209334192751441320"/>
       <accessionNumber value="AN5678AIM"/>
       <dateTime value="20170201180043"/>
       <user>
           <name value="Doe^Jane"/>
           <loginName value="jdoe"/>
           <roleInTrial/>
       </user>
       <equipment>
           <manufacturerName value="Acme Medical Systems"/>
           <manufacturerModelName value=""/>
           <softwareVersion value="36.00"/>
       </equipment>
       <person>
           <name value="CM-1-111-000000"/>
           <id value="293761767066931586407385203810190772174"/>
           <birthDate value="19600101000000"/>
           <sex value="M"/>
           <ethnicGroup/>
       </person>
       <imageAnnotations>
           <ImageAnnotation>
               <uniqueIdentifier root="2.25.56002466128627498886935079903172938041"/>
               <typeCode code="52988006" codeSystemName="SCT">
                   <iso:displayName xmlns:iso="uri:iso.org:21090" value="Lesion"/>
               </typeCode>
               <dateTime value="20170201180043"/>
               <name value="Lesion1"/>
               <comment value="PT / WB NAC P600 / 0"/>
               <trackingUniqueIdentifier root="2.25.165294254063588909770717555738008800301"/>
               <calculationEntityCollection>
                   <CalculationEntity>
                       <uniqueIdentifier root="2.25.51420968257530981243824658943871973198"/>
                       <typeCode code="126401" codeSystemName="DCM">
                           <iso:displayName xmlns:iso="uri:iso.org:21090" value="SUVbw"/>
                       </typeCode>
                       <typeCode code="255605001" codeSystemName="SCT">
                           <iso:displayName xmlns:iso="uri:iso.org:21090" value="Minimum"/>
                       </typeCode>
                       <description value="SUVbw Minimum"/>
                       <mathML/>
                       <calculationResultCollection>
                           <CalculationResult type="Scalar" xsi:type="CompactCalculationResult">
                               <unitOfMeasure value="g/ml{SUVbw}"/>
                               <dataType code="C48870" codeSystemName="NCI">
                                   <iso:displayName xmlns:iso="uri:iso.org:21090" value="Double"/>
                               </dataType>
                               <dimensionCollection>
                                   <Dimension>
                                       <index value="0"/>
                                       <size value="1"/>
                                       <label value="Minimum"/>
                                   </Dimension>
                               </dimensionCollection>
                               <value value="1.98024"/>
                           </CalculationResult>
                       </calculationResultCollection>
                       
                   </CalculationEntity>
                   <CalculationEntity>
                       <uniqueIdentifier root="2.25.205292243885258032428819330909580896146"/>
                       <typeCode code="126401" codeSystemName="DCM">
                           <iso:displayName xmlns:iso="uri:iso.org:21090" value="SUVbw"/>
                       </typeCode>
                       <typeCode code="56851009" codeSystemName="SCT">
                           <iso:displayName xmlns:iso="uri:iso.org:21090" value="Maximum"/>
                       </typeCode>
                       <description value="SUVbw Maximum"/>
                       <mathML/>
                       <calculationResultCollection>
                           <CalculationResult type="Scalar" xsi:type="CompactCalculationResult">
                               <unitOfMeasure value="g/ml{SUVbw}"/>
                               <dataType code="C48870" codeSystemName="NCI">
                                   <iso:displayName xmlns:iso="uri:iso.org:21090" value="Double"/>
                               </dataType>
                               <dimensionCollection>
                                   <Dimension>
                                       <index value="0"/>
                                       <size value="1"/>
                                       <label value="Maximum"/>
                                   </Dimension>
                               </dimensionCollection>
                               <value value="5.68816"/>
                           </CalculationResult>
                       </calculationResultCollection>
                       
                   </CalculationEntity>
                   <CalculationEntity>
                       <uniqueIdentifier root="2.25.70160252080234577167847509948368893276"/>
                       <typeCode code="126401" codeSystemName="DCM">
                           <iso:displayName xmlns:iso="uri:iso.org:21090" value="SUVbw"/>
                       </typeCode>
                       <typeCode code="373098007" codeSystemName="SCT">
                           <iso:displayName xmlns:iso="uri:iso.org:21090" value="Mean"/>
                       </typeCode>
                       <description value="SUVbw Mean"/>
                       <mathML/>
                       <calculationResultCollection>
                           <CalculationResult type="Scalar" xsi:type="CompactCalculationResult">
                               <unitOfMeasure value="g/ml{SUVbw}"/>
                               <dataType code="C48870" codeSystemName="NCI">
                                   <iso:displayName xmlns:iso="uri:iso.org:21090" value="Double"/>
                               </dataType>
                               <dimensionCollection>
                                   <Dimension>
                                       <index value="0"/>
                                       <size value="1"/>
                                       <label value="Mean"/>
                                   </Dimension>
                               </dimensionCollection>
                               <value value="2.329186593407"/>
                           </CalculationResult>
                       </calculationResultCollection>
                       
                   </CalculationEntity>
                   <CalculationEntity>
                       <uniqueIdentifier root="2.25.140657026119469861895824082767088344984"/>
                       <typeCode code="126401" codeSystemName="DCM">
                           <iso:displayName xmlns:iso="uri:iso.org:21090" value="SUVbw"/>
                       </typeCode>
                       <typeCode code="386136009" codeSystemName="SCT">
                           <iso:displayName xmlns:iso="uri:iso.org:21090" value="Standard Deviation"/>
                       </typeCode>
                       <description value="SUVbw Standard Deviation"/>
                       <mathML/>
                       <calculationResultCollection>
                           <CalculationResult type="Scalar" xsi:type="CompactCalculationResult">
                               <unitOfMeasure value="g/ml{SUVbw}"/>
                               <dataType code="C48870" codeSystemName="NCI">
                                   <iso:displayName xmlns:iso="uri:iso.org:21090" value="Double"/>
                               </dataType>
                               <dimensionCollection>
                                   <Dimension>
                                       <index value="0"/>
                                       <size value="1"/>
                                       <label value="Standard Deviation"/>
                                   </Dimension>
                               </dimensionCollection>
                               <value value="1.8828952323684"/>
                           </CalculationResult>
                       </calculationResultCollection>
                       
                   </CalculationEntity>
               </calculationEntityCollection>
               <segmentationEntityCollection>
                   <SegmentationEntity xsi:type="DicomSegmentationEntity">
                       <uniqueIdentifier root="2.25.318310842062810077214341266367812728264"/>
                       <sopInstanceUid root="2.25.134884066033959077306435705240550195701"/>
                       <studyInstanceUid root="2.25.19202292006231006756726546749423641172"/>
                       <seriesInstanceUid root="2.25.225493840038502954753967211679094249480"/>
                       <sopClassUid root="1.2.840.10008.5.1.4.1.1.66.4"/>
                       <referencedSopInstanceUid root="2.25.319214308104243787945491694789635628411"/>
                       <segmentNumber value="1"/>
                   </SegmentationEntity>
               </segmentationEntityCollection>
               <imageReferenceEntityCollection>
                   <ImageReferenceEntity xsi:type="DicomImageReferenceEntity">
                       <uniqueIdentifier root="2.25.239108061065263370785162033783811931375"/>
                       <imageStudy>
                           <instanceUid root="2.25.52186905385055707830834793159643714079"/>
                           <startDate value="20170113"/>
                           <startTime value="070844"/>
                           <accessionNumber value="AN1234IMG"/>
                           <imageSeries>
                               <instanceUid root="2.25.263500776851326986665835510707132143772"/>
                               <modality code="PT" codeSystemName="DCM">
                                   <iso:displayName xmlns:iso="uri:iso.org:21090" value="Positron emission tomography"/>
                               </modality>
                               <imageCollection>
                                   <Image>
                                       <sopClassUid root="1.2.840.10008.5.1.4.1.1.128"/>
                                       <sopInstanceUid root="2.25.319214308104243787945491694789635628411"/>
                                   </Image>
                               </imageCollection>
                           </imageSeries>
                       </imageStudy>
                   </ImageReferenceEntity>
               </imageReferenceEntityCollection>
           </ImageAnnotation>
       </imageAnnotations>
   </ImageAnnotationCollection>

.. _sect_A.7.2:

Target DICOM SR "Measurement Report" (TID 1500)
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

A compact representation of the semantic content of the transformed
DICOM SR tree is shown here:

::

   1: : CONTAINER: (126000,DCM,"Imaging Measurement Report")  [SEPARATE] (DCMR,1500)
       >1.1: HAS CONCEPT MOD: CODE: (121049,DCM,"Language of Content Item and Descendants")  = (eng,RFC5646,"English")
           >>1.1.1: HAS CONCEPT MOD: CODE: (121046,DCM,"Country of Language")  = (US,ISO3166_1,"United States")
       >1.2: HAS OBS CONTEXT: PNAME: (121008,DCM,"Person Observer Name")  = "Doe^Jane"
       >1.3: HAS OBS CONTEXT: TEXT: (128774,DCM,"Person Observer's Login Name")  = "jdoe"
       >1.4: HAS CONCEPT MOD: CODE: (121058,DCM,"Procedure reported")  = (44136-0,LN,"PET unspecified body region")
       >1.5: CONTAINS: CONTAINER: (111028,DCM,"Image Library")  [SEPARATE]
           >>1.5.1: CONTAINS: CONTAINER: (126200,DCM,"Image Library Group")  [SEPARATE] (,2.25.239108061065263370785162033783811931375)
               >>>1.5.1.1: CONTAINS: IMAGE:  = (1.2.840.10008.5.1.4.1.1.128,2.25.319214308104243787945491694789635628411)
                   >>>>1.5.1.1.1: HAS ACQ CONTEXT: CODE: (121139,DCM,"Modality")  = (PT,DCM,"Positron emission tomography")
                   >>>>1.5.1.1.2: HAS ACQ CONTEXT: TEXT: (121022,DCM,"Accession Number")  = "AN1234IMG"
                   >>>>1.5.1.1.3: HAS ACQ CONTEXT: DATE: (111060,DCM,"Study Date")  = "20170113"
                   >>>>1.5.1.1.4: HAS ACQ CONTEXT: TIME: (111061,DCM,"Study Time")  = "070844"
       >1.6: CONTAINS: CONTAINER: (126010,DCM,"Imaging Measurements")  [SEPARATE]
           >>1.6.1: CONTAINS: CONTAINER: (125007,DCM,"Measurement Group")  [SEPARATE] (20170201180043,2.25.56002466128627498886935079903172938041)
               >>>1.6.1.1: HAS OBS CONTEXT: TEXT: (112039,DCM,"Tracking Identifier")  = "Lesion1"
               >>>1.6.1.2: HAS OBS CONTEXT: UIDREF: (112040,DCM,"Tracking Unique Identifier")  = "2.25.165294254063588909770717555738008800301"
               >>>1.6.1.3: CONTAINS: CODE: (121071,DCM,"Finding")  = (52988006,SCT,"Lesion")
               >>>1.6.1.4: CONTAINS: IMAGE: (121191,DCM,"Referenced Segment")  = (1.2.840.10008.5.1.4.1.1.66.4,2.25.134884066033959077306435705240550195701) [Segment 1] (,2.25.318310842062810077214341266367812728264)
               >>>1.6.1.5: CONTAINS: IMAGE: (121233,DCM,"Source image for segmentation")  = (1.2.840.10008.5.1.4.1.1.128,2.25.319214308104243787945491694789635628411)
               >>>1.6.1.6: CONTAINS: NUM: (126401,DCM,"SUVbw")  = 1.98024 (g/ml{SUVbw},UCUM,"g/ml{SUVbw}") (,2.25.51420968257530981243824658943871973198)
                   >>>>1.6.1.6.1: HAS CONCEPT MOD: CODE: (121401,DCM,"Derivation")  = (255605001,SCT,"Minimum")
               >>>1.6.1.7: CONTAINS: NUM: (126401,DCM,"SUVbw")  = 5.68816 (g/ml{SUVbw},UCUM,"g/ml{SUVbw}") (,2.25.205292243885258032428819330909580896146)
                   >>>>1.6.1.7.1: HAS CONCEPT MOD: CODE: (121401,DCM,"Derivation")  = (56851009,SCT,"Maximum")
               >>>1.6.1.8: CONTAINS: NUM: (126401,DCM,"SUVbw")  = 2.329186593407 (g/ml{SUVbw},UCUM,"g/ml{SUVbw}") (,2.25.70160252080234577167847509948368893276)
                   >>>>1.6.1.8.1: HAS CONCEPT MOD: CODE: (121401,DCM,"Derivation")  = (373098007,SCT,"Mean")
               >>>1.6.1.9: CONTAINS: NUM: (126401,DCM,"SUVbw")  = 1.8828952323684 (g/ml{SUVbw},UCUM,"g/ml{SUVbw}") (,2.25.140657026119469861895824082767088344984)
                   >>>>1.6.1.9.1: HAS CONCEPT MOD: CODE: (121401,DCM,"Derivation")  = (386136009,SCT,"Standard Deviation")
               >>>1.6.1.10: CONTAINS: TEXT: (121106,DCM,"Comment")  = "PT / WB NAC P600 / 0"

The AIM sample transformed into SR illustrated at the Attribute encoding
level shown in `table_title <#table_A.7.2-1>`__ includes information on
the SR document body tree depth (column 1: SR Tree Depth), nesting level
for nested artifacts such as sequences and sequence items (column 2:
Nesting), DICOM Attribute names (column 3: Attribute), DICOM tag (column
4: Tag), the DICOM Attribute value representation (Column 5: VR as
specified in ), the hexadecimal value of value length (column 6: VL
(hex)) and the sample document Attribute values (column 7: Value).

.. table:: Transformed SR document encoding at the Attribute level

   +---------+---------+---------+---------+----+---------+---------+
   | SR Tree | Nesting | At      | Tag     | VR | VL      | Value   |
   | Depth   |         | tribute |         |    | (hex)   |         |
   +=========+=========+=========+=========+====+=========+=========+
   |         |         | File    | (000    | UL | 0004    | 0x0     |
   |         |         | Meta    | 2,0000) |    |         | 00000ba |
   |         |         | Info    |         |    |         |         |
   |         |         | rmation |         |    |         |         |
   |         |         | Group   |         |    |         |         |
   |         |         | Length  |         |    |         |         |
   +---------+---------+---------+---------+----+---------+---------+
   |         |         | File    | (000    | OB | 0002    | 0x      |
   |         |         | Meta    | 2,0001) |    |         | 00,0x01 |
   |         |         | Info    |         |    |         |         |
   |         |         | rmation |         |    |         |         |
   |         |         | Version |         |    |         |         |
   +---------+---------+---------+---------+----+---------+---------+
   |         |         | Media   | (000    | UI | 001e    | 1       |
   |         |         | Storage | 2,0002) |    |         | .2.840. |
   |         |         | SOP     |         |    |         | 10008.5 |
   |         |         | Class   |         |    |         | .1.4.1. |
   |         |         | UID     |         |    |         | 1.88.22 |
   +---------+---------+---------+---------+----+---------+---------+
   |         |         | Media   | (000    | UI | 002c    | 2.      |
   |         |         | Storage | 2,0003) |    |         | 25.2247 |
   |         |         | SOP     |         |    |         | 9392333 |
   |         |         | I       |         |    |         | 9609181 |
   |         |         | nstance |         |    |         | 2431391 |
   |         |         | UID     |         |    |         | 9585825 |
   |         |         |         |         |    |         | 4344686 |
   +---------+---------+---------+---------+----+---------+---------+
   |         |         | T       | (000    | UI | 0014    | 1.2.8   |
   |         |         | ransfer | 2,0010) |    |         | 40.1000 |
   |         |         | Syntax  |         |    |         | 8.1.2.1 |
   |         |         | UID     |         |    |         |         |
   +---------+---------+---------+---------+----+---------+---------+
   |         |         | Impleme | (000    | UI | 0016    | 1.3.6.1 |
   |         |         | ntation | 2,0012) |    |         | .4.1.59 |
   |         |         | Class   |         |    |         | 62.99.2 |
   |         |         | UID     |         |    |         |         |
   +---------+---------+---------+---------+----+---------+---------+
   |         |         | Impleme | (000    | SH | 0010    | P       |
   |         |         | ntation | 2,0013) |    |         | IXELMED |
   |         |         | Version |         |    |         | JAVA001 |
   |         |         | Name    |         |    |         |         |
   +---------+---------+---------+---------+----+---------+---------+
   |         |         | SOP     | (000    | UI | 001e    | 1       |
   |         |         | Class   | 8,0016) |    |         | .2.840. |
   |         |         | UID     |         |    |         | 10008.5 |
   |         |         |         |         |    |         | .1.4.1. |
   |         |         |         |         |    |         | 1.88.22 |
   +---------+---------+---------+---------+----+---------+---------+
   |         |         | SOP     | (000    | UI | 002c    | 2.      |
   |         |         | I       | 8,0018) |    |         | 25.2247 |
   |         |         | nstance |         |    |         | 9392333 |
   |         |         | UID     |         |    |         | 9609181 |
   |         |         |         |         |    |         | 2431391 |
   |         |         |         |         |    |         | 9585825 |
   |         |         |         |         |    |         | 4344686 |
   +---------+---------+---------+---------+----+---------+---------+
   |         |         | Study   | (000    | DA | 0000    |         |
   |         |         | Date    | 8,0020) |    |         |         |
   +---------+---------+---------+---------+----+---------+---------+
   |         |         | Content | (000    | DA | 0008    | 2       |
   |         |         | Date    | 8,0023) |    |         | 0170201 |
   +---------+---------+---------+---------+----+---------+---------+
   |         |         | Study   | (000    | TM | 0000    |         |
   |         |         | Time    | 8,0030) |    |         |         |
   +---------+---------+---------+---------+----+---------+---------+
   |         |         | Content | (000    | TM | 0006    | 180043  |
   |         |         | Time    | 8,0033) |    |         |         |
   +---------+---------+---------+---------+----+---------+---------+
   |         |         | Ac      | (000    | SH | 000a    | AN      |
   |         |         | cession | 8,0050) |    |         | 5678AIM |
   |         |         | Number  |         |    |         |         |
   +---------+---------+---------+---------+----+---------+---------+
   |         |         | M       | (000    | CS | 0002    | SR      |
   |         |         | odality | 8,0060) |    |         |         |
   +---------+---------+---------+---------+----+---------+---------+
   |         |         | Manuf   | (000    | LO | 0014    | Acme    |
   |         |         | acturer | 8,0070) |    |         | Medical |
   |         |         |         |         |    |         | Systems |
   +---------+---------+---------+---------+----+---------+---------+
   |         |         | Re      | (000    | PN | 0000    |         |
   |         |         | ferring | 8,0090) |    |         |         |
   |         |         | Phys    |         |    |         |         |
   |         |         | ician's |         |    |         |         |
   |         |         | Name    |         |    |         |         |
   +---------+---------+---------+---------+----+---------+---------+
   |         |         | Manufac | (000    | LO | 0000    |         |
   |         |         | turer's | 8,1090) |    |         |         |
   |         |         | Model   |         |    |         |         |
   |         |         | Name    |         |    |         |         |
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
   |         |         | Pa      | (001    | PN | 0010    | C       |
   |         |         | tient's | 0,0010) |    |         | M-1-111 |
   |         |         | Name    |         |    |         | -000000 |
   +---------+---------+---------+---------+----+---------+---------+
   |         |         | Patient | (001    | LO | 0028    | 2937    |
   |         |         | ID      | 0,0020) |    |         | 6176706 |
   |         |         |         |         |    |         | 6931586 |
   |         |         |         |         |    |         | 4073852 |
   |         |         |         |         |    |         | 0381019 |
   |         |         |         |         |    |         | 0772174 |
   +---------+---------+---------+---------+----+---------+---------+
   |         |         | Pa      | (001    | DA | 0008    | 1       |
   |         |         | tient's | 0,0030) |    |         | 9601000 |
   |         |         | Birth   |         |    |         |         |
   |         |         | Date    |         |    |         |         |
   +---------+---------+---------+---------+----+---------+---------+
   |         |         | Pa      | (001    | CS | 0002    | M       |
   |         |         | tient's | 0,0040) |    |         |         |
   |         |         | Sex     |         |    |         |         |
   +---------+---------+---------+---------+----+---------+---------+
   |         |         | Ethnic  | (001    | SH | 0000    |         |
   |         |         | Group   | 0,2160) |    |         |         |
   +---------+---------+---------+---------+----+---------+---------+
   |         |         | S       | (001    | LO | 0006    | 36.00   |
   |         |         | oftware | 8,1020) |    |         |         |
   |         |         | V       |         |    |         |         |
   |         |         | ersions |         |    |         |         |
   +---------+---------+---------+---------+----+---------+---------+
   |         |         | Study   | (002    | UI | 002c    | 2       |
   |         |         | I       | 0,000d) |    |         | .25.801 |
   |         |         | nstance |         |    |         | 5916822 |
   |         |         | UID     |         |    |         | 9010751 |
   |         |         |         |         |    |         | 6525025 |
   |         |         |         |         |    |         | 7683005 |
   |         |         |         |         |    |         | 7032194 |
   +---------+---------+---------+---------+----+---------+---------+
   |         |         | Series  | (002    | UI | 002c    | 2.      |
   |         |         | I       | 0,000e) |    |         | 25.3238 |
   |         |         | nstance |         |    |         | 1722544 |
   |         |         | UID     |         |    |         | 4021135 |
   |         |         |         |         |    |         | 4152093 |
   |         |         |         |         |    |         | 3419275 |
   |         |         |         |         |    |         | 1441320 |
   +---------+---------+---------+---------+----+---------+---------+
   |         |         | Study   | (002    | SH | 0000    |         |
   |         |         | ID      | 0,0010) |    |         |         |
   +---------+---------+---------+---------+----+---------+---------+
   |         |         | Series  | (002    | IS | 0004    | 7291    |
   |         |         | Number  | 0,0011) |    |         |         |
   +---------+---------+---------+---------+----+---------+---------+
   |         |         | I       | (002    | IS | 0002    | 1       |
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
   |         | %item   |         |         |    |         |         |
   +---------+---------+---------+---------+----+---------+---------+
   |         | >       | Code    | (000    | SH | 0006    | 126000  |
   |         |         | Value   | 8,0100) |    |         |         |
   +---------+---------+---------+---------+----+---------+---------+
   |         | >       | Coding  | (000    | SH | 0004    | DCM     |
   |         |         | Scheme  | 8,0102) |    |         |         |
   |         |         | Des     |         |    |         |         |
   |         |         | ignator |         |    |         |         |
   +---------+---------+---------+---------+----+---------+---------+
   |         | >       | Code    | (000    | LO | 001a    | Imaging |
   |         |         | Meaning | 8,0104) |    |         | Meas    |
   |         |         |         |         |    |         | urement |
   |         |         |         |         |    |         | Report  |
   +---------+---------+---------+---------+----+---------+---------+
   |         | %       |         |         |    |         |         |
   |         | enditem |         |         |    |         |         |
   +---------+---------+---------+---------+----+---------+---------+
   |         | %endseq |         |         |    |         |         |
   +---------+---------+---------+---------+----+---------+---------+
   | 1       |         | Con     | (004    | CS | 0008    | S       |
   |         |         | tinuity | 0,a050) |    |         | EPARATE |
   |         |         | Of      |         |    |         |         |
   |         |         | Content |         |    |         |         |
   +---------+---------+---------+---------+----+---------+---------+
   |         |         | Author  | (004    | SQ | f       |         |
   |         |         | O       | 0,a078) |    | fffffff |         |
   |         |         | bserver |         |    |         |         |
   |         |         | S       |         |    |         |         |
   |         |         | equence |         |    |         |         |
   +---------+---------+---------+---------+----+---------+---------+
   |         | %item   |         |         |    |         |         |
   +---------+---------+---------+---------+----+---------+---------+
   |         | >       | Inst    | (000    | LO | 0000    |         |
   |         |         | itution | 8,0080) |    |         |         |
   |         |         | Name    |         |    |         |         |
   +---------+---------+---------+---------+----+---------+---------+
   |         | >       | Inst    | (000    | SQ | f       |         |
   |         |         | itution | 8,0082) |    | fffffff |         |
   |         |         | Code    |         |    |         |         |
   |         |         | S       |         |    |         |         |
   |         |         | equence |         |    |         |         |
   +---------+---------+---------+---------+----+---------+---------+
   |         | %endseq |         |         |    |         |         |
   +---------+---------+---------+---------+----+---------+---------+
   |         | >       | Person  | (004    | SQ | f       |         |
   |         |         | Identif | 0,1101) |    | fffffff |         |
   |         |         | ication |         |    |         |         |
   |         |         | Code    |         |    |         |         |
   |         |         | S       |         |    |         |         |
   |         |         | equence |         |    |         |         |
   +---------+---------+---------+---------+----+---------+---------+
   |         | %endseq |         |         |    |         |         |
   +---------+---------+---------+---------+----+---------+---------+
   |         | >       | O       | (004    | CS | 0004    | PSN     |
   |         |         | bserver | 0,a084) |    |         |         |
   |         |         | Type    |         |    |         |         |
   +---------+---------+---------+---------+----+---------+---------+
   |         | >       | Person  | (004    | PN | 0008    | D       |
   |         |         | Name    | 0,a123) |    |         | oe^Jane |
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
   |         | >>>     | Ref     | (000    | UI | 001c    | 1.2.84  |
   |         |         | erenced | 8,1150) |    |         | 0.10008 |
   |         |         | SOP     |         |    |         | .5.1.4. |
   |         |         | Class   |         |    |         | 1.1.128 |
   |         |         | UID     |         |    |         |         |
   +---------+---------+---------+---------+----+---------+---------+
   |         | >>>     | Ref     | (000    | UI | 002c    | 2.      |
   |         |         | erenced | 8,1155) |    |         | 25.3192 |
   |         |         | SOP     |         |    |         | 1430810 |
   |         |         | I       |         |    |         | 4243787 |
   |         |         | nstance |         |    |         | 9454916 |
   |         |         | UID     |         |    |         | 9478963 |
   |         |         |         |         |    |         | 5628411 |
   +---------+---------+---------+---------+----+---------+---------+
   |         | %       |         |         |    |         |         |
   |         | enditem |         |         |    |         |         |
   +---------+---------+---------+---------+----+---------+---------+
   |         | %endseq |         |         |    |         |         |
   +---------+---------+---------+---------+----+---------+---------+
   |         | >>      | Series  | (002    | UI | 002c    | 2.      |
   |         |         | I       | 0,000e) |    |         | 25.2635 |
   |         |         | nstance |         |    |         | 0077685 |
   |         |         | UID     |         |    |         | 1326986 |
   |         |         |         |         |    |         | 6658355 |
   |         |         |         |         |    |         | 1070713 |
   |         |         |         |         |    |         | 2143772 |
   +---------+---------+---------+---------+----+---------+---------+
   |         | %       |         |         |    |         |         |
   |         | enditem |         |         |    |         |         |
   +---------+---------+---------+---------+----+---------+---------+
   |         | %endseq |         |         |    |         |         |
   +---------+---------+---------+---------+----+---------+---------+
   |         | >       | Study   | (002    | UI | 002c    | 2       |
   |         |         | I       | 0,000d) |    |         | .25.521 |
   |         |         | nstance |         |    |         | 8690538 |
   |         |         | UID     |         |    |         | 5055707 |
   |         |         |         |         |    |         | 8308347 |
   |         |         |         |         |    |         | 9315964 |
   |         |         |         |         |    |         | 3714079 |
   +---------+---------+---------+---------+----+---------+---------+
   |         | %       |         |         |    |         |         |
   |         | enditem |         |         |    |         |         |
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
   |         | >>>     | Ref     | (000    | UI | 001c    | 1.2.840 |
   |         |         | erenced | 8,1150) |    |         | .10008. |
   |         |         | SOP     |         |    |         | 5.1.4.1 |
   |         |         | Class   |         |    |         | .1.66.4 |
   |         |         | UID     |         |    |         |         |
   +---------+---------+---------+---------+----+---------+---------+
   |         | >>>     | Ref     | (000    | UI | 002c    | 2.      |
   |         |         | erenced | 8,1155) |    |         | 25.1348 |
   |         |         | SOP     |         |    |         | 8406603 |
   |         |         | I       |         |    |         | 3959077 |
   |         |         | nstance |         |    |         | 3064357 |
   |         |         | UID     |         |    |         | 0524055 |
   |         |         |         |         |    |         | 0195701 |
   +---------+---------+---------+---------+----+---------+---------+
   |         | %       |         |         |    |         |         |
   |         | enditem |         |         |    |         |         |
   +---------+---------+---------+---------+----+---------+---------+
   |         | %endseq |         |         |    |         |         |
   +---------+---------+---------+---------+----+---------+---------+
   |         | >>      | Series  | (002    | UI | 002c    | 2.      |
   |         |         | I       | 0,000e) |    |         | 25.2254 |
   |         |         | nstance |         |    |         | 9384003 |
   |         |         | UID     |         |    |         | 8502954 |
   |         |         |         |         |    |         | 7539672 |
   |         |         |         |         |    |         | 1167909 |
   |         |         |         |         |    |         | 4249480 |
   +---------+---------+---------+---------+----+---------+---------+
   |         | %       |         |         |    |         |         |
   |         | enditem |         |         |    |         |         |
   +---------+---------+---------+---------+----+---------+---------+
   |         | %endseq |         |         |    |         |         |
   +---------+---------+---------+---------+----+---------+---------+
   |         | >       | Study   | (002    | UI | 002c    | 2       |
   |         |         | I       | 0,000d) |    |         | .25.192 |
   |         |         | nstance |         |    |         | 0229200 |
   |         |         | UID     |         |    |         | 6231006 |
   |         |         |         |         |    |         | 7567265 |
   |         |         |         |         |    |         | 4674942 |
   |         |         |         |         |    |         | 3641172 |
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
   |         |         | Verif   | (004    | CS | 000a    | UNV     |
   |         |         | ication | 0,a493) |    |         | ERIFIED |
   |         |         | Flag    |         |    |         |         |
   +---------+---------+---------+---------+----+---------+---------+
   |         |         | Content | (004    | SQ | f       |         |
   |         |         | T       | 0,a504) |    | fffffff |         |
   |         |         | emplate |         |    |         |         |
   |         |         | S       |         |    |         |         |
   |         |         | equence |         |    |         |         |
   +---------+---------+---------+---------+----+---------+---------+
   |         | %item   |         |         |    |         |         |
   +---------+---------+---------+---------+----+---------+---------+
   |         | >       | Mapping | (000    | CS | 0004    | DCMR    |
   |         |         | R       | 8,0105) |    |         |         |
   |         |         | esource |         |    |         |         |
   +---------+---------+---------+---------+----+---------+---------+
   |         | >       | T       | (004    | CS | 0004    | 1500    |
   |         |         | emplate | 0,db00) |    |         |         |
   |         |         | Ide     |         |    |         |         |
   |         |         | ntifier |         |    |         |         |
   +---------+---------+---------+---------+----+---------+---------+
   |         | %       |         |         |    |         |         |
   |         | enditem |         |         |    |         |         |
   +---------+---------+---------+---------+----+---------+---------+
   |         | %endseq |         |         |    |         |         |
   +---------+---------+---------+---------+----+---------+---------+
   | 1       |         | Content | (004    | SQ | f       |         |
   |         |         | S       | 0,a730) |    | fffffff |         |
   |         |         | equence |         |    |         |         |
   +---------+---------+---------+---------+----+---------+---------+
   |         | %item   |         |         |    |         |         |
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
   |         | %item   |         |         |    |         |         |
   +---------+---------+---------+---------+----+---------+---------+
   | 1.1     | >>      | Code    | (000    | SH | 0006    | 121049  |
   |         |         | Value   | 8,0100) |    |         |         |
   +---------+---------+---------+---------+----+---------+---------+
   | 1.1     | >>      | Coding  | (000    | SH | 0004    | DCM     |
   |         |         | Scheme  | 8,0102) |    |         |         |
   |         |         | Des     |         |    |         |         |
   |         |         | ignator |         |    |         |         |
   +---------+---------+---------+---------+----+---------+---------+
   | 1.1     | >>      | Code    | (000    | LO | 0028    | L       |
   |         |         | Meaning | 8,0104) |    |         | anguage |
   |         |         |         |         |    |         | of      |
   |         |         |         |         |    |         | Content |
   |         |         |         |         |    |         | Item    |
   |         |         |         |         |    |         | and     |
   |         |         |         |         |    |         | Desc    |
   |         |         |         |         |    |         | endants |
   +---------+---------+---------+---------+----+---------+---------+
   |         | %       |         |         |    |         |         |
   |         | enditem |         |         |    |         |         |
   +---------+---------+---------+---------+----+---------+---------+
   |         | %endseq |         |         |    |         |         |
   +---------+---------+---------+---------+----+---------+---------+
   | 1.1     | >       | Concept | (004    | SQ | f       |         |
   |         |         | Code    | 0,a168) |    | fffffff |         |
   |         |         | S       |         |    |         |         |
   |         |         | equence |         |    |         |         |
   +---------+---------+---------+---------+----+---------+---------+
   |         | %item   |         |         |    |         |         |
   +---------+---------+---------+---------+----+---------+---------+
   | 1.1     | >>      | Code    | (000    | SH | 0004    | eng     |
   |         |         | Value   | 8,0100) |    |         |         |
   +---------+---------+---------+---------+----+---------+---------+
   | 1.1     | >>      | Coding  | (000    | SH | 0008    | RFC5646 |
   |         |         | Scheme  | 8,0102) |    |         |         |
   |         |         | Des     |         |    |         |         |
   |         |         | ignator |         |    |         |         |
   +---------+---------+---------+---------+----+---------+---------+
   | 1.1     | >>      | Code    | (000    | LO | 0008    | English |
   |         |         | Meaning | 8,0104) |    |         |         |
   +---------+---------+---------+---------+----+---------+---------+
   |         | %       |         |         |    |         |         |
   |         | enditem |         |         |    |         |         |
   +---------+---------+---------+---------+----+---------+---------+
   |         | %endseq |         |         |    |         |         |
   +---------+---------+---------+---------+----+---------+---------+
   | 1.1     | >       | Content | (004    | SQ | f       |         |
   |         |         | S       | 0,a730) |    | fffffff |         |
   |         |         | equence |         |    |         |         |
   +---------+---------+---------+---------+----+---------+---------+
   |         | %item   |         |         |    |         |         |
   +---------+---------+---------+---------+----+---------+---------+
   | 1.1.1   | >>      | Relat   | (004    | CS | 0010    | HAS     |
   |         |         | ionship | 0,a010) |    |         | CONCEPT |
   |         |         | Type    |         |    |         | MOD     |
   +---------+---------+---------+---------+----+---------+---------+
   | 1.1.1   | >>      | Value   | (004    | CS | 0004    | CODE    |
   |         |         | Type    | 0,a040) |    |         |         |
   +---------+---------+---------+---------+----+---------+---------+
   | 1.1.1   | >>      | Concept | (004    | SQ | f       |         |
   |         |         | Name    | 0,a043) |    | fffffff |         |
   |         |         | Code    |         |    |         |         |
   |         |         | S       |         |    |         |         |
   |         |         | equence |         |    |         |         |
   +---------+---------+---------+---------+----+---------+---------+
   |         | %item   |         |         |    |         |         |
   +---------+---------+---------+---------+----+---------+---------+
   | 1.1.1   | >>>     | Code    | (000    | SH | 0006    | 121046  |
   |         |         | Value   | 8,0100) |    |         |         |
   +---------+---------+---------+---------+----+---------+---------+
   | 1.1.1   | >>>     | Coding  | (000    | SH | 0004    | DCM     |
   |         |         | Scheme  | 8,0102) |    |         |         |
   |         |         | Des     |         |    |         |         |
   |         |         | ignator |         |    |         |         |
   +---------+---------+---------+---------+----+---------+---------+
   | 1.1.1   | >>>     | Code    | (000    | LO | 0014    | Country |
   |         |         | Meaning | 8,0104) |    |         | of      |
   |         |         |         |         |    |         | L       |
   |         |         |         |         |    |         | anguage |
   +---------+---------+---------+---------+----+---------+---------+
   |         | %       |         |         |    |         |         |
   |         | enditem |         |         |    |         |         |
   +---------+---------+---------+---------+----+---------+---------+
   |         | %endseq |         |         |    |         |         |
   +---------+---------+---------+---------+----+---------+---------+
   | 1.1.1   | >>      | Concept | (004    | SQ | f       |         |
   |         |         | Code    | 0,a168) |    | fffffff |         |
   |         |         | S       |         |    |         |         |
   |         |         | equence |         |    |         |         |
   +---------+---------+---------+---------+----+---------+---------+
   |         | %item   |         |         |    |         |         |
   +---------+---------+---------+---------+----+---------+---------+
   | 1.1.1   | >>>     | Code    | (000    | SH | 0002    | US      |
   |         |         | Value   | 8,0100) |    |         |         |
   +---------+---------+---------+---------+----+---------+---------+
   | 1.1.1   | >>>     | Coding  | (000    | SH | 000a    | IS      |
   |         |         | Scheme  | 8,0102) |    |         | O3166_1 |
   |         |         | Des     |         |    |         |         |
   |         |         | ignator |         |    |         |         |
   +---------+---------+---------+---------+----+---------+---------+
   | 1.1.1   | >>>     | Code    | (000    | LO | 000e    | United  |
   |         |         | Meaning | 8,0104) |    |         | States  |
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
   |         | %       |         |         |    |         |         |
   |         | enditem |         |         |    |         |         |
   +---------+---------+---------+---------+----+---------+---------+
   |         | %item   |         |         |    |         |         |
   +---------+---------+---------+---------+----+---------+---------+
   | 1.2     | >       | Relat   | (004    | CS | 0010    | HAS OBS |
   |         |         | ionship | 0,a010) |    |         | CONTEXT |
   |         |         | Type    |         |    |         |         |
   +---------+---------+---------+---------+----+---------+---------+
   | 1.2     | >       | Value   | (004    | CS | 0006    | PNAME   |
   |         |         | Type    | 0,a040) |    |         |         |
   +---------+---------+---------+---------+----+---------+---------+
   | 1.2     | >       | Concept | (004    | SQ | f       |         |
   |         |         | Name    | 0,a043) |    | fffffff |         |
   |         |         | Code    |         |    |         |         |
   |         |         | S       |         |    |         |         |
   |         |         | equence |         |    |         |         |
   +---------+---------+---------+---------+----+---------+---------+
   |         | %item   |         |         |    |         |         |
   +---------+---------+---------+---------+----+---------+---------+
   | 1.2     | >>      | Code    | (000    | SH | 0006    | 121008  |
   |         |         | Value   | 8,0100) |    |         |         |
   +---------+---------+---------+---------+----+---------+---------+
   | 1.2     | >>      | Coding  | (000    | SH | 0004    | DCM     |
   |         |         | Scheme  | 8,0102) |    |         |         |
   |         |         | Des     |         |    |         |         |
   |         |         | ignator |         |    |         |         |
   +---------+---------+---------+---------+----+---------+---------+
   | 1.2     | >>      | Code    | (000    | LO | 0014    | Person  |
   |         |         | Meaning | 8,0104) |    |         | O       |
   |         |         |         |         |    |         | bserver |
   |         |         |         |         |    |         | Name    |
   +---------+---------+---------+---------+----+---------+---------+
   |         | %       |         |         |    |         |         |
   |         | enditem |         |         |    |         |         |
   +---------+---------+---------+---------+----+---------+---------+
   |         | %endseq |         |         |    |         |         |
   +---------+---------+---------+---------+----+---------+---------+
   | 1.2     | >       | Person  | (004    | PN | 0008    | D       |
   |         |         | Name    | 0,a123) |    |         | oe^Jane |
   +---------+---------+---------+---------+----+---------+---------+
   |         | %       |         |         |    |         |         |
   |         | enditem |         |         |    |         |         |
   +---------+---------+---------+---------+----+---------+---------+
   |         | %item   |         |         |    |         |         |
   +---------+---------+---------+---------+----+---------+---------+
   | 1.3     | >       | Relat   | (004    | CS | 0010    | HAS OBS |
   |         |         | ionship | 0,a010) |    |         | CONTEXT |
   |         |         | Type    |         |    |         |         |
   +---------+---------+---------+---------+----+---------+---------+
   | 1.3     | >       | Value   | (004    | CS | 0004    | TEXT    |
   |         |         | Type    | 0,a040) |    |         |         |
   +---------+---------+---------+---------+----+---------+---------+
   | 1.3     | >       | Concept | (004    | SQ | f       |         |
   |         |         | Name    | 0,a043) |    | fffffff |         |
   |         |         | Code    |         |    |         |         |
   |         |         | S       |         |    |         |         |
   |         |         | equence |         |    |         |         |
   +---------+---------+---------+---------+----+---------+---------+
   |         | %item   |         |         |    |         |         |
   +---------+---------+---------+---------+----+---------+---------+
   | 1.3     | >>      | Code    | (000    | SH | 0006    | 128774  |
   |         |         | Value   | 8,0100) |    |         |         |
   +---------+---------+---------+---------+----+---------+---------+
   | 1.3     | >>      | Coding  | (000    | SH | 0004    | DCM     |
   |         |         | Scheme  | 8,0102) |    |         |         |
   |         |         | Des     |         |    |         |         |
   |         |         | ignator |         |    |         |         |
   +---------+---------+---------+---------+----+---------+---------+
   | 1.3     | >>      | Code    | (000    | LO | 001c    | Person  |
   |         |         | Meaning | 8,0104) |    |         | Obs     |
   |         |         |         |         |    |         | erver's |
   |         |         |         |         |    |         | Login   |
   |         |         |         |         |    |         | Name    |
   +---------+---------+---------+---------+----+---------+---------+
   |         | %       |         |         |    |         |         |
   |         | enditem |         |         |    |         |         |
   +---------+---------+---------+---------+----+---------+---------+
   |         | %endseq |         |         |    |         |         |
   +---------+---------+---------+---------+----+---------+---------+
   | 1.3     | >       | Text    | (004    | UT | 0004    | jdoe    |
   |         |         | Value   | 0,a160) |    |         |         |
   +---------+---------+---------+---------+----+---------+---------+
   |         | %       |         |         |    |         |         |
   |         | enditem |         |         |    |         |         |
   +---------+---------+---------+---------+----+---------+---------+
   |         | %item   |         |         |    |         |         |
   +---------+---------+---------+---------+----+---------+---------+
   | 1.4     | >       | Relat   | (004    | CS | 0010    | HAS     |
   |         |         | ionship | 0,a010) |    |         | CONCEPT |
   |         |         | Type    |         |    |         | MOD     |
   +---------+---------+---------+---------+----+---------+---------+
   | 1.4     | >       | Value   | (004    | CS | 0004    | CODE    |
   |         |         | Type    | 0,a040) |    |         |         |
   +---------+---------+---------+---------+----+---------+---------+
   | 1.4     | >       | Concept | (004    | SQ | f       |         |
   |         |         | Name    | 0,a043) |    | fffffff |         |
   |         |         | Code    |         |    |         |         |
   |         |         | S       |         |    |         |         |
   |         |         | equence |         |    |         |         |
   +---------+---------+---------+---------+----+---------+---------+
   |         | %item   |         |         |    |         |         |
   +---------+---------+---------+---------+----+---------+---------+
   | 1.4     | >>      | Code    | (000    | SH | 0006    | 121058  |
   |         |         | Value   | 8,0100) |    |         |         |
   +---------+---------+---------+---------+----+---------+---------+
   | 1.4     | >>      | Coding  | (000    | SH | 0004    | DCM     |
   |         |         | Scheme  | 8,0102) |    |         |         |
   |         |         | Des     |         |    |         |         |
   |         |         | ignator |         |    |         |         |
   +---------+---------+---------+---------+----+---------+---------+
   | 1.4     | >>      | Code    | (000    | LO | 0012    | Pr      |
   |         |         | Meaning | 8,0104) |    |         | ocedure |
   |         |         |         |         |    |         | r       |
   |         |         |         |         |    |         | eported |
   +---------+---------+---------+---------+----+---------+---------+
   |         | %       |         |         |    |         |         |
   |         | enditem |         |         |    |         |         |
   +---------+---------+---------+---------+----+---------+---------+
   |         | %endseq |         |         |    |         |         |
   +---------+---------+---------+---------+----+---------+---------+
   | 1.4     | >       | Concept | (004    | SQ | f       |         |
   |         |         | Code    | 0,a168) |    | fffffff |         |
   |         |         | S       |         |    |         |         |
   |         |         | equence |         |    |         |         |
   +---------+---------+---------+---------+----+---------+---------+
   |         | %item   |         |         |    |         |         |
   +---------+---------+---------+---------+----+---------+---------+
   | 1.4     | >>      | Code    | (000    | SH | 0008    | 44136-0 |
   |         |         | Value   | 8,0100) |    |         |         |
   +---------+---------+---------+---------+----+---------+---------+
   | 1.4     | >>      | Coding  | (000    | SH | 0002    | LN      |
   |         |         | Scheme  | 8,0102) |    |         |         |
   |         |         | Des     |         |    |         |         |
   |         |         | ignator |         |    |         |         |
   +---------+---------+---------+---------+----+---------+---------+
   | 1.4     | >>      | Code    | (000    | LO | 001c    | PET     |
   |         |         | Meaning | 8,0104) |    |         | unsp    |
   |         |         |         |         |    |         | ecified |
   |         |         |         |         |    |         | body    |
   |         |         |         |         |    |         | region  |
   +---------+---------+---------+---------+----+---------+---------+
   |         | %       |         |         |    |         |         |
   |         | enditem |         |         |    |         |         |
   +---------+---------+---------+---------+----+---------+---------+
   |         | %endseq |         |         |    |         |         |
   +---------+---------+---------+---------+----+---------+---------+
   |         | %       |         |         |    |         |         |
   |         | enditem |         |         |    |         |         |
   +---------+---------+---------+---------+----+---------+---------+
   |         | %item   |         |         |    |         |         |
   +---------+---------+---------+---------+----+---------+---------+
   | 1.5     | >       | Relat   | (004    | CS | 0008    | C       |
   |         |         | ionship | 0,a010) |    |         | ONTAINS |
   |         |         | Type    |         |    |         |         |
   +---------+---------+---------+---------+----+---------+---------+
   | 1.5     | >       | Value   | (004    | CS | 000a    | CO      |
   |         |         | Type    | 0,a040) |    |         | NTAINER |
   +---------+---------+---------+---------+----+---------+---------+
   | 1.5     | >       | Concept | (004    | SQ | f       |         |
   |         |         | Name    | 0,a043) |    | fffffff |         |
   |         |         | Code    |         |    |         |         |
   |         |         | S       |         |    |         |         |
   |         |         | equence |         |    |         |         |
   +---------+---------+---------+---------+----+---------+---------+
   |         | %item   |         |         |    |         |         |
   +---------+---------+---------+---------+----+---------+---------+
   | 1.5     | >>      | Code    | (000    | SH | 0006    | 111028  |
   |         |         | Value   | 8,0100) |    |         |         |
   +---------+---------+---------+---------+----+---------+---------+
   | 1.5     | >>      | Coding  | (000    | SH | 0004    | DCM     |
   |         |         | Scheme  | 8,0102) |    |         |         |
   |         |         | Des     |         |    |         |         |
   |         |         | ignator |         |    |         |         |
   +---------+---------+---------+---------+----+---------+---------+
   | 1.5     | >>      | Code    | (000    | LO | 000e    | Image   |
   |         |         | Meaning | 8,0104) |    |         | Library |
   +---------+---------+---------+---------+----+---------+---------+
   |         | %       |         |         |    |         |         |
   |         | enditem |         |         |    |         |         |
   +---------+---------+---------+---------+----+---------+---------+
   |         | %endseq |         |         |    |         |         |
   +---------+---------+---------+---------+----+---------+---------+
   | 1.5     | >       | Con     | (004    | CS | 0008    | S       |
   |         |         | tinuity | 0,a050) |    |         | EPARATE |
   |         |         | Of      |         |    |         |         |
   |         |         | Content |         |    |         |         |
   +---------+---------+---------+---------+----+---------+---------+
   | 1.5     | >       | Content | (004    | SQ | f       |         |
   |         |         | S       | 0,a730) |    | fffffff |         |
   |         |         | equence |         |    |         |         |
   +---------+---------+---------+---------+----+---------+---------+
   |         | %item   |         |         |    |         |         |
   +---------+---------+---------+---------+----+---------+---------+
   | 1.5.1   | >>      | Relat   | (004    | CS | 0008    | C       |
   |         |         | ionship | 0,a010) |    |         | ONTAINS |
   |         |         | Type    |         |    |         |         |
   +---------+---------+---------+---------+----+---------+---------+
   | 1.5.1   | >>      | Value   | (004    | CS | 000a    | CO      |
   |         |         | Type    | 0,a040) |    |         | NTAINER |
   +---------+---------+---------+---------+----+---------+---------+
   | 1.5.1   | >>      | Concept | (004    | SQ | f       |         |
   |         |         | Name    | 0,a043) |    | fffffff |         |
   |         |         | Code    |         |    |         |         |
   |         |         | S       |         |    |         |         |
   |         |         | equence |         |    |         |         |
   +---------+---------+---------+---------+----+---------+---------+
   |         | %item   |         |         |    |         |         |
   +---------+---------+---------+---------+----+---------+---------+
   | 1.5.1   | >>>     | Code    | (000    | SH | 0006    | 126200  |
   |         |         | Value   | 8,0100) |    |         |         |
   +---------+---------+---------+---------+----+---------+---------+
   | 1.5.1   | >>>     | Coding  | (000    | SH | 0004    | DCM     |
   |         |         | Scheme  | 8,0102) |    |         |         |
   |         |         | Des     |         |    |         |         |
   |         |         | ignator |         |    |         |         |
   +---------+---------+---------+---------+----+---------+---------+
   | 1.5.1   | >>>     | Code    | (000    | LO | 0014    | Image   |
   |         |         | Meaning | 8,0104) |    |         | Library |
   |         |         |         |         |    |         | Group   |
   +---------+---------+---------+---------+----+---------+---------+
   |         | %       |         |         |    |         |         |
   |         | enditem |         |         |    |         |         |
   +---------+---------+---------+---------+----+---------+---------+
   |         | %endseq |         |         |    |         |         |
   +---------+---------+---------+---------+----+---------+---------+
   | 1.5.1   | >>      | Con     | (004    | CS | 0008    | S       |
   |         |         | tinuity | 0,a050) |    |         | EPARATE |
   |         |         | Of      |         |    |         |         |
   |         |         | Content |         |    |         |         |
   +---------+---------+---------+---------+----+---------+---------+
   | 1.5.1   | >>      | Obse    | (004    | UI | 002c    | 2.      |
   |         |         | rvation | 0,a171) |    |         | 25.2391 |
   |         |         | UID     |         |    |         | 0806106 |
   |         |         |         |         |    |         | 5263370 |
   |         |         |         |         |    |         | 7851620 |
   |         |         |         |         |    |         | 3378381 |
   |         |         |         |         |    |         | 1931375 |
   +---------+---------+---------+---------+----+---------+---------+
   | 1.5.1   | >>      | Content | (004    | SQ | f       |         |
   |         |         | S       | 0,a730) |    | fffffff |         |
   |         |         | equence |         |    |         |         |
   +---------+---------+---------+---------+----+---------+---------+
   |         | %item   |         |         |    |         |         |
   +---------+---------+---------+---------+----+---------+---------+
   | 1.5.1.1 | >>>     | Ref     | (000    | SQ | f       |         |
   |         |         | erenced | 8,1199) |    | fffffff |         |
   |         |         | SOP     |         |    |         |         |
   |         |         | S       |         |    |         |         |
   |         |         | equence |         |    |         |         |
   +---------+---------+---------+---------+----+---------+---------+
   |         | %item   |         |         |    |         |         |
   +---------+---------+---------+---------+----+---------+---------+
   | 1.5.1.1 | >>>>    | Ref     | (000    | UI | 001c    | 1.2.84  |
   |         |         | erenced | 8,1150) |    |         | 0.10008 |
   |         |         | SOP     |         |    |         | .5.1.4. |
   |         |         | Class   |         |    |         | 1.1.128 |
   |         |         | UID     |         |    |         |         |
   +---------+---------+---------+---------+----+---------+---------+
   | 1.5.1.1 | >>>>    | Ref     | (000    | UI | 002c    | 2.      |
   |         |         | erenced | 8,1155) |    |         | 25.3192 |
   |         |         | SOP     |         |    |         | 1430810 |
   |         |         | I       |         |    |         | 4243787 |
   |         |         | nstance |         |    |         | 9454916 |
   |         |         | UID     |         |    |         | 9478963 |
   |         |         |         |         |    |         | 5628411 |
   +---------+---------+---------+---------+----+---------+---------+
   |         | %       |         |         |    |         |         |
   |         | enditem |         |         |    |         |         |
   +---------+---------+---------+---------+----+---------+---------+
   |         | %endseq |         |         |    |         |         |
   +---------+---------+---------+---------+----+---------+---------+
   | 1.5.1.1 | >>>     | Relat   | (004    | CS | 0008    | C       |
   |         |         | ionship | 0,a010) |    |         | ONTAINS |
   |         |         | Type    |         |    |         |         |
   +---------+---------+---------+---------+----+---------+---------+
   | 1.5.1.1 | >>>     | Value   | (004    | CS | 0006    | IMAGE   |
   |         |         | Type    | 0,a040) |    |         |         |
   +---------+---------+---------+---------+----+---------+---------+
   | 1.5.1.1 | >>>     | Content | (004    | SQ | f       |         |
   |         |         | S       | 0,a730) |    | fffffff |         |
   |         |         | equence |         |    |         |         |
   +---------+---------+---------+---------+----+---------+---------+
   |         | %item   |         |         |    |         |         |
   +---------+---------+---------+---------+----+---------+---------+
   | 1.      | >>>>    | Relat   | (004    | CS | 0010    | HAS ACQ |
   | 5.1.1.1 |         | ionship | 0,a010) |    |         | CONTEXT |
   |         |         | Type    |         |    |         |         |
   +---------+---------+---------+---------+----+---------+---------+
   | 1.      | >>>>    | Value   | (004    | CS | 0004    | CODE    |
   | 5.1.1.1 |         | Type    | 0,a040) |    |         |         |
   +---------+---------+---------+---------+----+---------+---------+
   | 1.      | >>>>    | Concept | (004    | SQ | f       |         |
   | 5.1.1.1 |         | Name    | 0,a043) |    | fffffff |         |
   |         |         | Code    |         |    |         |         |
   |         |         | S       |         |    |         |         |
   |         |         | equence |         |    |         |         |
   +---------+---------+---------+---------+----+---------+---------+
   |         | %item   |         |         |    |         |         |
   +---------+---------+---------+---------+----+---------+---------+
   | 1.      | >>>>>   | Code    | (000    | SH | 0006    | 121139  |
   | 5.1.1.1 |         | Value   | 8,0100) |    |         |         |
   +---------+---------+---------+---------+----+---------+---------+
   | 1.      | >>>>>   | Coding  | (000    | SH | 0004    | DCM     |
   | 5.1.1.1 |         | Scheme  | 8,0102) |    |         |         |
   |         |         | Des     |         |    |         |         |
   |         |         | ignator |         |    |         |         |
   +---------+---------+---------+---------+----+---------+---------+
   | 1.      | >>>>>   | Code    | (000    | LO | 0008    | M       |
   | 5.1.1.1 |         | Meaning | 8,0104) |    |         | odality |
   +---------+---------+---------+---------+----+---------+---------+
   |         | %       |         |         |    |         |         |
   |         | enditem |         |         |    |         |         |
   +---------+---------+---------+---------+----+---------+---------+
   |         | %endseq |         |         |    |         |         |
   +---------+---------+---------+---------+----+---------+---------+
   | 1.      | >>>>    | Concept | (004    | SQ | f       |         |
   | 5.1.1.1 |         | Code    | 0,a168) |    | fffffff |         |
   |         |         | S       |         |    |         |         |
   |         |         | equence |         |    |         |         |
   +---------+---------+---------+---------+----+---------+---------+
   |         | %item   |         |         |    |         |         |
   +---------+---------+---------+---------+----+---------+---------+
   | 1.      | >>>>>   | Code    | (000    | SH | 0002    | PT      |
   | 5.1.1.1 |         | Value   | 8,0100) |    |         |         |
   +---------+---------+---------+---------+----+---------+---------+
   | 1.      | >>>>>   | Coding  | (000    | SH | 0004    | DCM     |
   | 5.1.1.1 |         | Scheme  | 8,0102) |    |         |         |
   |         |         | Des     |         |    |         |         |
   |         |         | ignator |         |    |         |         |
   +---------+---------+---------+---------+----+---------+---------+
   | 1.      | >>>>>   | Code    | (000    | LO | 001c    | P       |
   | 5.1.1.1 |         | Meaning | 8,0104) |    |         | ositron |
   |         |         |         |         |    |         | e       |
   |         |         |         |         |    |         | mission |
   |         |         |         |         |    |         | tom     |
   |         |         |         |         |    |         | ography |
   +---------+---------+---------+---------+----+---------+---------+
   |         | %       |         |         |    |         |         |
   |         | enditem |         |         |    |         |         |
   +---------+---------+---------+---------+----+---------+---------+
   |         | %endseq |         |         |    |         |         |
   +---------+---------+---------+---------+----+---------+---------+
   |         | %       |         |         |    |         |         |
   |         | enditem |         |         |    |         |         |
   +---------+---------+---------+---------+----+---------+---------+
   |         | %item   |         |         |    |         |         |
   +---------+---------+---------+---------+----+---------+---------+
   | 1.      | >>>>    | Relat   | (004    | CS | 0010    | HAS ACQ |
   | 5.1.1.2 |         | ionship | 0,a010) |    |         | CONTEXT |
   |         |         | Type    |         |    |         |         |
   +---------+---------+---------+---------+----+---------+---------+
   | 1.      | >>>>    | Value   | (004    | CS | 0004    | TEXT    |
   | 5.1.1.2 |         | Type    | 0,a040) |    |         |         |
   +---------+---------+---------+---------+----+---------+---------+
   | 1.      | >>>>    | Concept | (004    | SQ | f       |         |
   | 5.1.1.2 |         | Name    | 0,a043) |    | fffffff |         |
   |         |         | Code    |         |    |         |         |
   |         |         | S       |         |    |         |         |
   |         |         | equence |         |    |         |         |
   +---------+---------+---------+---------+----+---------+---------+
   |         | %item   |         |         |    |         |         |
   +---------+---------+---------+---------+----+---------+---------+
   | 1.      | >>>>>   | Code    | (000    | SH | 0006    | 121022  |
   | 5.1.1.2 |         | Value   | 8,0100) |    |         |         |
   +---------+---------+---------+---------+----+---------+---------+
   | 1.      | >>>>>   | Coding  | (000    | SH | 0004    | DCM     |
   | 5.1.1.2 |         | Scheme  | 8,0102) |    |         |         |
   |         |         | Des     |         |    |         |         |
   |         |         | ignator |         |    |         |         |
   +---------+---------+---------+---------+----+---------+---------+
   | 1.      | >>>>>   | Code    | (000    | LO | 0010    | Ac      |
   | 5.1.1.2 |         | Meaning | 8,0104) |    |         | cession |
   |         |         |         |         |    |         | Number  |
   +---------+---------+---------+---------+----+---------+---------+
   |         | %       |         |         |    |         |         |
   |         | enditem |         |         |    |         |         |
   +---------+---------+---------+---------+----+---------+---------+
   |         | %endseq |         |         |    |         |         |
   +---------+---------+---------+---------+----+---------+---------+
   | 1.      | >>>>    | Text    | (004    | UT | 000a    | AN      |
   | 5.1.1.2 |         | Value   | 0,a160) |    |         | 1234IMG |
   +---------+---------+---------+---------+----+---------+---------+
   |         | %       |         |         |    |         |         |
   |         | enditem |         |         |    |         |         |
   +---------+---------+---------+---------+----+---------+---------+
   |         | %item   |         |         |    |         |         |
   +---------+---------+---------+---------+----+---------+---------+
   | 1.      | >>>>    | Relat   | (004    | CS | 0010    | HAS ACQ |
   | 5.1.1.3 |         | ionship | 0,a010) |    |         | CONTEXT |
   |         |         | Type    |         |    |         |         |
   +---------+---------+---------+---------+----+---------+---------+
   | 1.      | >>>>    | Value   | (004    | CS | 0004    | DATE    |
   | 5.1.1.3 |         | Type    | 0,a040) |    |         |         |
   +---------+---------+---------+---------+----+---------+---------+
   | 1.      | >>>>    | Concept | (004    | SQ | f       |         |
   | 5.1.1.3 |         | Name    | 0,a043) |    | fffffff |         |
   |         |         | Code    |         |    |         |         |
   |         |         | S       |         |    |         |         |
   |         |         | equence |         |    |         |         |
   +---------+---------+---------+---------+----+---------+---------+
   |         | %item   |         |         |    |         |         |
   +---------+---------+---------+---------+----+---------+---------+
   | 1.      | >>>>>   | Code    | (000    | SH | 0006    | 111060  |
   | 5.1.1.3 |         | Value   | 8,0100) |    |         |         |
   +---------+---------+---------+---------+----+---------+---------+
   | 1.      | >>>>>   | Coding  | (000    | SH | 0004    | DCM     |
   | 5.1.1.3 |         | Scheme  | 8,0102) |    |         |         |
   |         |         | Des     |         |    |         |         |
   |         |         | ignator |         |    |         |         |
   +---------+---------+---------+---------+----+---------+---------+
   | 1.      | >>>>>   | Code    | (000    | LO | 000a    | Study   |
   | 5.1.1.3 |         | Meaning | 8,0104) |    |         | Date    |
   +---------+---------+---------+---------+----+---------+---------+
   |         | %       |         |         |    |         |         |
   |         | enditem |         |         |    |         |         |
   +---------+---------+---------+---------+----+---------+---------+
   |         | %endseq |         |         |    |         |         |
   +---------+---------+---------+---------+----+---------+---------+
   | 1.      | >>>>    | Date    | (004    | DA | 0008    | 2       |
   | 5.1.1.3 |         |         | 0,a121) |    |         | 0170113 |
   +---------+---------+---------+---------+----+---------+---------+
   |         | %       |         |         |    |         |         |
   |         | enditem |         |         |    |         |         |
   +---------+---------+---------+---------+----+---------+---------+
   |         | %item   |         |         |    |         |         |
   +---------+---------+---------+---------+----+---------+---------+
   | 1.      | >>>>    | Relat   | (004    | CS | 0010    | HAS ACQ |
   | 5.1.1.4 |         | ionship | 0,a010) |    |         | CONTEXT |
   |         |         | Type    |         |    |         |         |
   +---------+---------+---------+---------+----+---------+---------+
   | 1.      | >>>>    | Value   | (004    | CS | 0004    | TIME    |
   | 5.1.1.4 |         | Type    | 0,a040) |    |         |         |
   +---------+---------+---------+---------+----+---------+---------+
   | 1.      | >>>>    | Concept | (004    | SQ | f       |         |
   | 5.1.1.4 |         | Name    | 0,a043) |    | fffffff |         |
   |         |         | Code    |         |    |         |         |
   |         |         | S       |         |    |         |         |
   |         |         | equence |         |    |         |         |
   +---------+---------+---------+---------+----+---------+---------+
   |         | %item   |         |         |    |         |         |
   +---------+---------+---------+---------+----+---------+---------+
   | 1.      | >>>>>   | Code    | (000    | SH | 0006    | 111061  |
   | 5.1.1.4 |         | Value   | 8,0100) |    |         |         |
   +---------+---------+---------+---------+----+---------+---------+
   | 1.      | >>>>>   | Coding  | (000    | SH | 0004    | DCM     |
   | 5.1.1.4 |         | Scheme  | 8,0102) |    |         |         |
   |         |         | Des     |         |    |         |         |
   |         |         | ignator |         |    |         |         |
   +---------+---------+---------+---------+----+---------+---------+
   | 1.      | >>>>>   | Code    | (000    | LO | 000a    | Study   |
   | 5.1.1.4 |         | Meaning | 8,0104) |    |         | Time    |
   +---------+---------+---------+---------+----+---------+---------+
   |         | %       |         |         |    |         |         |
   |         | enditem |         |         |    |         |         |
   +---------+---------+---------+---------+----+---------+---------+
   |         | %endseq |         |         |    |         |         |
   +---------+---------+---------+---------+----+---------+---------+
   | 1.      | >>>>    | Time    | (004    | TM | 0006    | 070844  |
   | 5.1.1.4 |         |         | 0,a122) |    |         |         |
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
   |         | %       |         |         |    |         |         |
   |         | enditem |         |         |    |         |         |
   +---------+---------+---------+---------+----+---------+---------+
   |         | %endseq |         |         |    |         |         |
   +---------+---------+---------+---------+----+---------+---------+
   |         | %       |         |         |    |         |         |
   |         | enditem |         |         |    |         |         |
   +---------+---------+---------+---------+----+---------+---------+
   |         | %item   |         |         |    |         |         |
   +---------+---------+---------+---------+----+---------+---------+
   | 1.6     | >       | Relat   | (004    | CS | 0008    | C       |
   |         |         | ionship | 0,a010) |    |         | ONTAINS |
   |         |         | Type    |         |    |         |         |
   +---------+---------+---------+---------+----+---------+---------+
   | 1.6     | >       | Value   | (004    | CS | 000a    | CO      |
   |         |         | Type    | 0,a040) |    |         | NTAINER |
   +---------+---------+---------+---------+----+---------+---------+
   | 1.6     | >       | Concept | (004    | SQ | f       |         |
   |         |         | Name    | 0,a043) |    | fffffff |         |
   |         |         | Code    |         |    |         |         |
   |         |         | S       |         |    |         |         |
   |         |         | equence |         |    |         |         |
   +---------+---------+---------+---------+----+---------+---------+
   |         | %item   |         |         |    |         |         |
   +---------+---------+---------+---------+----+---------+---------+
   | 1.6     | >>      | Code    | (000    | SH | 0006    | 126010  |
   |         |         | Value   | 8,0100) |    |         |         |
   +---------+---------+---------+---------+----+---------+---------+
   | 1.6     | >>      | Coding  | (000    | SH | 0004    | DCM     |
   |         |         | Scheme  | 8,0102) |    |         |         |
   |         |         | Des     |         |    |         |         |
   |         |         | ignator |         |    |         |         |
   +---------+---------+---------+---------+----+---------+---------+
   | 1.6     | >>      | Code    | (000    | LO | 0014    | Imaging |
   |         |         | Meaning | 8,0104) |    |         | Measu   |
   |         |         |         |         |    |         | rements |
   +---------+---------+---------+---------+----+---------+---------+
   |         | %       |         |         |    |         |         |
   |         | enditem |         |         |    |         |         |
   +---------+---------+---------+---------+----+---------+---------+
   |         | %endseq |         |         |    |         |         |
   +---------+---------+---------+---------+----+---------+---------+
   | 1.6     | >       | Con     | (004    | CS | 0008    | S       |
   |         |         | tinuity | 0,a050) |    |         | EPARATE |
   |         |         | Of      |         |    |         |         |
   |         |         | Content |         |    |         |         |
   +---------+---------+---------+---------+----+---------+---------+
   | 1.6     | >       | Content | (004    | SQ | f       |         |
   |         |         | S       | 0,a730) |    | fffffff |         |
   |         |         | equence |         |    |         |         |
   +---------+---------+---------+---------+----+---------+---------+
   |         | %item   |         |         |    |         |         |
   +---------+---------+---------+---------+----+---------+---------+
   | 1.6.1   | >>      | Relat   | (004    | CS | 0008    | C       |
   |         |         | ionship | 0,a010) |    |         | ONTAINS |
   |         |         | Type    |         |    |         |         |
   +---------+---------+---------+---------+----+---------+---------+
   | 1.6.1   | >>      | Obse    | (004    | DT | 000e    | 2017020 |
   |         |         | rvation | 0,a032) |    |         | 1180043 |
   |         |         | D       |         |    |         |         |
   |         |         | ateTime |         |    |         |         |
   +---------+---------+---------+---------+----+---------+---------+
   | 1.6.1   | >>      | Value   | (004    | CS | 000a    | CO      |
   |         |         | Type    | 0,a040) |    |         | NTAINER |
   +---------+---------+---------+---------+----+---------+---------+
   | 1.6.1   | >>      | Concept | (004    | SQ | f       |         |
   |         |         | Name    | 0,a043) |    | fffffff |         |
   |         |         | Code    |         |    |         |         |
   |         |         | S       |         |    |         |         |
   |         |         | equence |         |    |         |         |
   +---------+---------+---------+---------+----+---------+---------+
   |         | %item   |         |         |    |         |         |
   +---------+---------+---------+---------+----+---------+---------+
   | 1.6.1   | >>>     | Code    | (000    | SH | 0006    | 125007  |
   |         |         | Value   | 8,0100) |    |         |         |
   +---------+---------+---------+---------+----+---------+---------+
   | 1.6.1   | >>>     | Coding  | (000    | SH | 0004    | DCM     |
   |         |         | Scheme  | 8,0102) |    |         |         |
   |         |         | Des     |         |    |         |         |
   |         |         | ignator |         |    |         |         |
   +---------+---------+---------+---------+----+---------+---------+
   | 1.6.1   | >>>     | Code    | (000    | LO | 0012    | Meas    |
   |         |         | Meaning | 8,0104) |    |         | urement |
   |         |         |         |         |    |         | Group   |
   +---------+---------+---------+---------+----+---------+---------+
   |         | %       |         |         |    |         |         |
   |         | enditem |         |         |    |         |         |
   +---------+---------+---------+---------+----+---------+---------+
   |         | %endseq |         |         |    |         |         |
   +---------+---------+---------+---------+----+---------+---------+
   | 1.6.1   | >>      | Con     | (004    | CS | 0008    | S       |
   |         |         | tinuity | 0,a050) |    |         | EPARATE |
   |         |         | Of      |         |    |         |         |
   |         |         | Content |         |    |         |         |
   +---------+---------+---------+---------+----+---------+---------+
   | 1.6.1   | >>      | Obse    | (004    | UI | 002c    | 2       |
   |         |         | rvation | 0,a171) |    |         | .25.560 |
   |         |         | UID     |         |    |         | 0246612 |
   |         |         |         |         |    |         | 8627498 |
   |         |         |         |         |    |         | 8869350 |
   |         |         |         |         |    |         | 7990317 |
   |         |         |         |         |    |         | 2938041 |
   +---------+---------+---------+---------+----+---------+---------+
   | 1.6.1   | >>      | Content | (004    | SQ | f       |         |
   |         |         | S       | 0,a730) |    | fffffff |         |
   |         |         | equence |         |    |         |         |
   +---------+---------+---------+---------+----+---------+---------+
   |         | %item   |         |         |    |         |         |
   +---------+---------+---------+---------+----+---------+---------+
   | 1.6.1.1 | >>>     | Relat   | (004    | CS | 0010    | HAS OBS |
   |         |         | ionship | 0,a010) |    |         | CONTEXT |
   |         |         | Type    |         |    |         |         |
   +---------+---------+---------+---------+----+---------+---------+
   | 1.6.1.1 | >>>     | Value   | (004    | CS | 0004    | TEXT    |
   |         |         | Type    | 0,a040) |    |         |         |
   +---------+---------+---------+---------+----+---------+---------+
   | 1.6.1.1 | >>>     | Concept | (004    | SQ | f       |         |
   |         |         | Name    | 0,a043) |    | fffffff |         |
   |         |         | Code    |         |    |         |         |
   |         |         | S       |         |    |         |         |
   |         |         | equence |         |    |         |         |
   +---------+---------+---------+---------+----+---------+---------+
   |         | %item   |         |         |    |         |         |
   +---------+---------+---------+---------+----+---------+---------+
   | 1.6.1.1 | >>>>    | Code    | (000    | SH | 0006    | 112039  |
   |         |         | Value   | 8,0100) |    |         |         |
   +---------+---------+---------+---------+----+---------+---------+
   | 1.6.1.1 | >>>>    | Coding  | (000    | SH | 0004    | DCM     |
   |         |         | Scheme  | 8,0102) |    |         |         |
   |         |         | Des     |         |    |         |         |
   |         |         | ignator |         |    |         |         |
   +---------+---------+---------+---------+----+---------+---------+
   | 1.6.1.1 | >>>>    | Code    | (000    | LO | 0014    | T       |
   |         |         | Meaning | 8,0104) |    |         | racking |
   |         |         |         |         |    |         | Ide     |
   |         |         |         |         |    |         | ntifier |
   +---------+---------+---------+---------+----+---------+---------+
   |         | %       |         |         |    |         |         |
   |         | enditem |         |         |    |         |         |
   +---------+---------+---------+---------+----+---------+---------+
   |         | %endseq |         |         |    |         |         |
   +---------+---------+---------+---------+----+---------+---------+
   | 1.6.1.1 | >>>     | Text    | (004    | UT | 0008    | Lesion1 |
   |         |         | Value   | 0,a160) |    |         |         |
   +---------+---------+---------+---------+----+---------+---------+
   |         | %       |         |         |    |         |         |
   |         | enditem |         |         |    |         |         |
   +---------+---------+---------+---------+----+---------+---------+
   |         | %item   |         |         |    |         |         |
   +---------+---------+---------+---------+----+---------+---------+
   | 1.6.1.2 | >>>     | Relat   | (004    | CS | 0010    | HAS OBS |
   |         |         | ionship | 0,a010) |    |         | CONTEXT |
   |         |         | Type    |         |    |         |         |
   +---------+---------+---------+---------+----+---------+---------+
   | 1.6.1.2 | >>>     | Value   | (004    | CS | 0006    | UIDREF  |
   |         |         | Type    | 0,a040) |    |         |         |
   +---------+---------+---------+---------+----+---------+---------+
   | 1.6.1.2 | >>>     | Concept | (004    | SQ | f       |         |
   |         |         | Name    | 0,a043) |    | fffffff |         |
   |         |         | Code    |         |    |         |         |
   |         |         | S       |         |    |         |         |
   |         |         | equence |         |    |         |         |
   +---------+---------+---------+---------+----+---------+---------+
   |         | %item   |         |         |    |         |         |
   +---------+---------+---------+---------+----+---------+---------+
   | 1.6.1.2 | >>>>    | Code    | (000    | SH | 0006    | 112040  |
   |         |         | Value   | 8,0100) |    |         |         |
   +---------+---------+---------+---------+----+---------+---------+
   | 1.6.1.2 | >>>>    | Coding  | (000    | SH | 0004    | DCM     |
   |         |         | Scheme  | 8,0102) |    |         |         |
   |         |         | Des     |         |    |         |         |
   |         |         | ignator |         |    |         |         |
   +---------+---------+---------+---------+----+---------+---------+
   | 1.6.1.2 | >>>>    | Code    | (000    | LO | 001a    | T       |
   |         |         | Meaning | 8,0104) |    |         | racking |
   |         |         |         |         |    |         | Unique  |
   |         |         |         |         |    |         | Ide     |
   |         |         |         |         |    |         | ntifier |
   +---------+---------+---------+---------+----+---------+---------+
   |         | %       |         |         |    |         |         |
   |         | enditem |         |         |    |         |         |
   +---------+---------+---------+---------+----+---------+---------+
   |         | %endseq |         |         |    |         |         |
   +---------+---------+---------+---------+----+---------+---------+
   | 1.6.1.2 | >>>     | UID     | (004    | UI | 002c    | 2.      |
   |         |         |         | 0,a124) |    |         | 25.1652 |
   |         |         |         |         |    |         | 9425406 |
   |         |         |         |         |    |         | 3588909 |
   |         |         |         |         |    |         | 7707175 |
   |         |         |         |         |    |         | 5573800 |
   |         |         |         |         |    |         | 8800301 |
   +---------+---------+---------+---------+----+---------+---------+
   |         | %       |         |         |    |         |         |
   |         | enditem |         |         |    |         |         |
   +---------+---------+---------+---------+----+---------+---------+
   |         | %item   |         |         |    |         |         |
   +---------+---------+---------+---------+----+---------+---------+
   | 1.6.1.3 | >>>     | Relat   | (004    | CS | 0008    | C       |
   |         |         | ionship | 0,a010) |    |         | ONTAINS |
   |         |         | Type    |         |    |         |         |
   +---------+---------+---------+---------+----+---------+---------+
   | 1.6.1.3 | >>>     | Value   | (004    | CS | 0004    | CODE    |
   |         |         | Type    | 0,a040) |    |         |         |
   +---------+---------+---------+---------+----+---------+---------+
   | 1.6.1.3 | >>>     | Concept | (004    | SQ | f       |         |
   |         |         | Name    | 0,a043) |    | fffffff |         |
   |         |         | Code    |         |    |         |         |
   |         |         | S       |         |    |         |         |
   |         |         | equence |         |    |         |         |
   +---------+---------+---------+---------+----+---------+---------+
   |         | %item   |         |         |    |         |         |
   +---------+---------+---------+---------+----+---------+---------+
   | 1.6.1.3 | >>>>    | Code    | (000    | SH | 0006    | 121071  |
   |         |         | Value   | 8,0100) |    |         |         |
   +---------+---------+---------+---------+----+---------+---------+
   | 1.6.1.3 | >>>>    | Coding  | (000    | SH | 0004    | DCM     |
   |         |         | Scheme  | 8,0102) |    |         |         |
   |         |         | Des     |         |    |         |         |
   |         |         | ignator |         |    |         |         |
   +---------+---------+---------+---------+----+---------+---------+
   | 1.6.1.3 | >>>>    | Code    | (000    | LO | 0008    | Finding |
   |         |         | Meaning | 8,0104) |    |         |         |
   +---------+---------+---------+---------+----+---------+---------+
   |         | %       |         |         |    |         |         |
   |         | enditem |         |         |    |         |         |
   +---------+---------+---------+---------+----+---------+---------+
   |         | %endseq |         |         |    |         |         |
   +---------+---------+---------+---------+----+---------+---------+
   | 1.6.1.3 | >>>     | Concept | (004    | SQ | f       |         |
   |         |         | Code    | 0,a168) |    | fffffff |         |
   |         |         | S       |         |    |         |         |
   |         |         | equence |         |    |         |         |
   +---------+---------+---------+---------+----+---------+---------+
   |         | %item   |         |         |    |         |         |
   +---------+---------+---------+---------+----+---------+---------+
   | 1.6.1.3 | >>>>    | Code    | (000    | SH | 0008    | 5       |
   |         |         | Value   | 8,0100) |    |         | 2988006 |
   +---------+---------+---------+---------+----+---------+---------+
   | 1.6.1.3 | >>>>    | Coding  | (000    | SH | 0004    | SCT     |
   |         |         | Scheme  | 8,0102) |    |         |         |
   |         |         | Des     |         |    |         |         |
   |         |         | ignator |         |    |         |         |
   +---------+---------+---------+---------+----+---------+---------+
   | 1.6.1.3 | >>>>    | Code    | (000    | LO | 0006    | Lesion  |
   |         |         | Meaning | 8,0104) |    |         |         |
   +---------+---------+---------+---------+----+---------+---------+
   |         | %       |         |         |    |         |         |
   |         | enditem |         |         |    |         |         |
   +---------+---------+---------+---------+----+---------+---------+
   |         | %endseq |         |         |    |         |         |
   +---------+---------+---------+---------+----+---------+---------+
   |         | %       |         |         |    |         |         |
   |         | enditem |         |         |    |         |         |
   +---------+---------+---------+---------+----+---------+---------+
   |         | %item   |         |         |    |         |         |
   +---------+---------+---------+---------+----+---------+---------+
   | 1.6.1.4 | >>>     | Ref     | (000    | SQ | f       |         |
   |         |         | erenced | 8,1199) |    | fffffff |         |
   |         |         | SOP     |         |    |         |         |
   |         |         | S       |         |    |         |         |
   |         |         | equence |         |    |         |         |
   +---------+---------+---------+---------+----+---------+---------+
   |         | %item   |         |         |    |         |         |
   +---------+---------+---------+---------+----+---------+---------+
   | 1.6.1.4 | >>>>    | Ref     | (000    | UI | 001c    | 1.2.840 |
   |         |         | erenced | 8,1150) |    |         | .10008. |
   |         |         | SOP     |         |    |         | 5.1.4.1 |
   |         |         | Class   |         |    |         | .1.66.4 |
   |         |         | UID     |         |    |         |         |
   +---------+---------+---------+---------+----+---------+---------+
   | 1.6.1.4 | >>>>    | Ref     | (000    | UI | 002c    | 2.      |
   |         |         | erenced | 8,1155) |    |         | 25.1348 |
   |         |         | SOP     |         |    |         | 8406603 |
   |         |         | I       |         |    |         | 3959077 |
   |         |         | nstance |         |    |         | 3064357 |
   |         |         | UID     |         |    |         | 0524055 |
   |         |         |         |         |    |         | 0195701 |
   +---------+---------+---------+---------+----+---------+---------+
   | 1.6.1.4 | >>>>    | Ref     | (006    | US | 0002    | 0x0001  |
   |         |         | erenced | 2,000b) |    |         |         |
   |         |         | Segment |         |    |         |         |
   |         |         | Number  |         |    |         |         |
   +---------+---------+---------+---------+----+---------+---------+
   |         | %       |         |         |    |         |         |
   |         | enditem |         |         |    |         |         |
   +---------+---------+---------+---------+----+---------+---------+
   |         | %endseq |         |         |    |         |         |
   +---------+---------+---------+---------+----+---------+---------+
   | 1.6.1.4 | >>>     | Relat   | (004    | CS | 0008    | C       |
   |         |         | ionship | 0,a010) |    |         | ONTAINS |
   |         |         | Type    |         |    |         |         |
   +---------+---------+---------+---------+----+---------+---------+
   | 1.6.1.4 | >>>     | Value   | (004    | CS | 0006    | IMAGE   |
   |         |         | Type    | 0,a040) |    |         |         |
   +---------+---------+---------+---------+----+---------+---------+
   | 1.6.1.4 | >>>     | Concept | (004    | SQ | f       |         |
   |         |         | Name    | 0,a043) |    | fffffff |         |
   |         |         | Code    |         |    |         |         |
   |         |         | S       |         |    |         |         |
   |         |         | equence |         |    |         |         |
   +---------+---------+---------+---------+----+---------+---------+
   |         | %item   |         |         |    |         |         |
   +---------+---------+---------+---------+----+---------+---------+
   | 1.6.1.4 | >>>>    | Code    | (000    | SH | 0006    | 121191  |
   |         |         | Value   | 8,0100) |    |         |         |
   +---------+---------+---------+---------+----+---------+---------+
   | 1.6.1.4 | >>>>    | Coding  | (000    | SH | 0004    | DCM     |
   |         |         | Scheme  | 8,0102) |    |         |         |
   |         |         | Des     |         |    |         |         |
   |         |         | ignator |         |    |         |         |
   +---------+---------+---------+---------+----+---------+---------+
   | 1.6.1.4 | >>>>    | Code    | (000    | LO | 0012    | Ref     |
   |         |         | Meaning | 8,0104) |    |         | erenced |
   |         |         |         |         |    |         | Segment |
   +---------+---------+---------+---------+----+---------+---------+
   |         | %       |         |         |    |         |         |
   |         | enditem |         |         |    |         |         |
   +---------+---------+---------+---------+----+---------+---------+
   |         | %endseq |         |         |    |         |         |
   +---------+---------+---------+---------+----+---------+---------+
   | 1.6.1.4 | >>>     | Obse    | (004    | UI | 002c    | 2.      |
   |         |         | rvation | 0,a171) |    |         | 25.3183 |
   |         |         | UID     |         |    |         | 1084206 |
   |         |         |         |         |    |         | 2810077 |
   |         |         |         |         |    |         | 2143412 |
   |         |         |         |         |    |         | 6636781 |
   |         |         |         |         |    |         | 2728264 |
   +---------+---------+---------+---------+----+---------+---------+
   |         | %       |         |         |    |         |         |
   |         | enditem |         |         |    |         |         |
   +---------+---------+---------+---------+----+---------+---------+
   |         | %item   |         |         |    |         |         |
   +---------+---------+---------+---------+----+---------+---------+
   | 1.6.1.5 | >>>     | Ref     | (000    | SQ | f       |         |
   |         |         | erenced | 8,1199) |    | fffffff |         |
   |         |         | SOP     |         |    |         |         |
   |         |         | S       |         |    |         |         |
   |         |         | equence |         |    |         |         |
   +---------+---------+---------+---------+----+---------+---------+
   |         | %item   |         |         |    |         |         |
   +---------+---------+---------+---------+----+---------+---------+
   | 1.6.1.5 | >>>>    | Ref     | (000    | UI | 001c    | 1.2.84  |
   |         |         | erenced | 8,1150) |    |         | 0.10008 |
   |         |         | SOP     |         |    |         | .5.1.4. |
   |         |         | Class   |         |    |         | 1.1.128 |
   |         |         | UID     |         |    |         |         |
   +---------+---------+---------+---------+----+---------+---------+
   | 1.6.1.5 | >>>>    | Ref     | (000    | UI | 002c    | 2.      |
   |         |         | erenced | 8,1155) |    |         | 25.3192 |
   |         |         | SOP     |         |    |         | 1430810 |
   |         |         | I       |         |    |         | 4243787 |
   |         |         | nstance |         |    |         | 9454916 |
   |         |         | UID     |         |    |         | 9478963 |
   |         |         |         |         |    |         | 5628411 |
   +---------+---------+---------+---------+----+---------+---------+
   |         | %       |         |         |    |         |         |
   |         | enditem |         |         |    |         |         |
   +---------+---------+---------+---------+----+---------+---------+
   |         | %endseq |         |         |    |         |         |
   +---------+---------+---------+---------+----+---------+---------+
   | 1.6.1.5 | >>>     | Relat   | (004    | CS | 0008    | C       |
   |         |         | ionship | 0,a010) |    |         | ONTAINS |
   |         |         | Type    |         |    |         |         |
   +---------+---------+---------+---------+----+---------+---------+
   | 1.6.1.5 | >>>     | Value   | (004    | CS | 0006    | IMAGE   |
   |         |         | Type    | 0,a040) |    |         |         |
   +---------+---------+---------+---------+----+---------+---------+
   | 1.6.1.5 | >>>     | Concept | (004    | SQ | f       |         |
   |         |         | Name    | 0,a043) |    | fffffff |         |
   |         |         | Code    |         |    |         |         |
   |         |         | S       |         |    |         |         |
   |         |         | equence |         |    |         |         |
   +---------+---------+---------+---------+----+---------+---------+
   |         | %item   |         |         |    |         |         |
   +---------+---------+---------+---------+----+---------+---------+
   | 1.6.1.5 | >>>>    | Code    | (000    | SH | 0006    | 121233  |
   |         |         | Value   | 8,0100) |    |         |         |
   +---------+---------+---------+---------+----+---------+---------+
   | 1.6.1.5 | >>>>    | Coding  | (000    | SH | 0004    | DCM     |
   |         |         | Scheme  | 8,0102) |    |         |         |
   |         |         | Des     |         |    |         |         |
   |         |         | ignator |         |    |         |         |
   +---------+---------+---------+---------+----+---------+---------+
   | 1.6.1.5 | >>>>    | Code    | (000    | LO | 001e    | Source  |
   |         |         | Meaning | 8,0104) |    |         | image   |
   |         |         |         |         |    |         | for     |
   |         |         |         |         |    |         | segme   |
   |         |         |         |         |    |         | ntation |
   +---------+---------+---------+---------+----+---------+---------+
   |         | %       |         |         |    |         |         |
   |         | enditem |         |         |    |         |         |
   +---------+---------+---------+---------+----+---------+---------+
   |         | %endseq |         |         |    |         |         |
   +---------+---------+---------+---------+----+---------+---------+
   |         | %       |         |         |    |         |         |
   |         | enditem |         |         |    |         |         |
   +---------+---------+---------+---------+----+---------+---------+
   |         | %item   |         |         |    |         |         |
   +---------+---------+---------+---------+----+---------+---------+
   | 1.6.1.6 | >>>     | Relat   | (004    | CS | 0008    | C       |
   |         |         | ionship | 0,a010) |    |         | ONTAINS |
   |         |         | Type    |         |    |         |         |
   +---------+---------+---------+---------+----+---------+---------+
   | 1.6.1.6 | >>>     | Value   | (004    | CS | 0004    | NUM     |
   |         |         | Type    | 0,a040) |    |         |         |
   +---------+---------+---------+---------+----+---------+---------+
   | 1.6.1.6 | >>>     | Concept | (004    | SQ | f       |         |
   |         |         | Name    | 0,a043) |    | fffffff |         |
   |         |         | Code    |         |    |         |         |
   |         |         | S       |         |    |         |         |
   |         |         | equence |         |    |         |         |
   +---------+---------+---------+---------+----+---------+---------+
   |         | %item   |         |         |    |         |         |
   +---------+---------+---------+---------+----+---------+---------+
   | 1.6.1.6 | >>>>    | Code    | (000    | SH | 0006    | 126401  |
   |         |         | Value   | 8,0100) |    |         |         |
   +---------+---------+---------+---------+----+---------+---------+
   | 1.6.1.6 | >>>>    | Coding  | (000    | SH | 0004    | DCM     |
   |         |         | Scheme  | 8,0102) |    |         |         |
   |         |         | Des     |         |    |         |         |
   |         |         | ignator |         |    |         |         |
   +---------+---------+---------+---------+----+---------+---------+
   | 1.6.1.6 | >>>>    | Code    | (000    | LO | 0006    | SUVbw   |
   |         |         | Meaning | 8,0104) |    |         |         |
   +---------+---------+---------+---------+----+---------+---------+
   |         | %       |         |         |    |         |         |
   |         | enditem |         |         |    |         |         |
   +---------+---------+---------+---------+----+---------+---------+
   |         | %endseq |         |         |    |         |         |
   +---------+---------+---------+---------+----+---------+---------+
   | 1.6.1.6 | >>>     | Obse    | (004    | UI | 002c    | 2       |
   |         |         | rvation | 0,a171) |    |         | .25.514 |
   |         |         | UID     |         |    |         | 2096825 |
   |         |         |         |         |    |         | 7530981 |
   |         |         |         |         |    |         | 2438246 |
   |         |         |         |         |    |         | 5894387 |
   |         |         |         |         |    |         | 1973198 |
   +---------+---------+---------+---------+----+---------+---------+
   | 1.6.1.6 | >>>     | M       | (004    | SQ | f       |         |
   |         |         | easured | 0,a300) |    | fffffff |         |
   |         |         | Value   |         |    |         |         |
   |         |         | S       |         |    |         |         |
   |         |         | equence |         |    |         |         |
   +---------+---------+---------+---------+----+---------+---------+
   |         | %item   |         |         |    |         |         |
   +---------+---------+---------+---------+----+---------+---------+
   | 1.6.1.6 | >>>>    | Meas    | (004    | SQ | f       |         |
   |         |         | urement | 0,08ea) |    | fffffff |         |
   |         |         | Units   |         |    |         |         |
   |         |         | Code    |         |    |         |         |
   |         |         | S       |         |    |         |         |
   |         |         | equence |         |    |         |         |
   +---------+---------+---------+---------+----+---------+---------+
   |         | %item   |         |         |    |         |         |
   +---------+---------+---------+---------+----+---------+---------+
   | 1.6.1.6 | >>>>>   | Code    | (000    | SH | 000c    | g/ml    |
   |         |         | Value   | 8,0100) |    |         | {SUVbw} |
   +---------+---------+---------+---------+----+---------+---------+
   | 1.6.1.6 | >>>>>   | Coding  | (000    | SH | 0004    | UCUM    |
   |         |         | Scheme  | 8,0102) |    |         |         |
   |         |         | Des     |         |    |         |         |
   |         |         | ignator |         |    |         |         |
   +---------+---------+---------+---------+----+---------+---------+
   | 1.6.1.6 | >>>>>   | Code    | (000    | LO | 000c    | g/ml    |
   |         |         | Meaning | 8,0104) |    |         | {SUVbw} |
   +---------+---------+---------+---------+----+---------+---------+
   |         | %       |         |         |    |         |         |
   |         | enditem |         |         |    |         |         |
   +---------+---------+---------+---------+----+---------+---------+
   |         | %endseq |         |         |    |         |         |
   +---------+---------+---------+---------+----+---------+---------+
   | 1.6.1.6 | >>>>    | Numeric | (004    | DS | 0008    | 1.98024 |
   |         |         | Value   | 0,a30a) |    |         |         |
   +---------+---------+---------+---------+----+---------+---------+
   |         | %       |         |         |    |         |         |
   |         | enditem |         |         |    |         |         |
   +---------+---------+---------+---------+----+---------+---------+
   |         | %endseq |         |         |    |         |         |
   +---------+---------+---------+---------+----+---------+---------+
   | 1.6.1.6 | >>>     | Content | (004    | SQ | f       |         |
   |         |         | S       | 0,a730) |    | fffffff |         |
   |         |         | equence |         |    |         |         |
   +---------+---------+---------+---------+----+---------+---------+
   |         | %item   |         |         |    |         |         |
   +---------+---------+---------+---------+----+---------+---------+
   | 1.      | >>>>    | Relat   | (004    | CS | 0010    | HAS     |
   | 6.1.6.1 |         | ionship | 0,a010) |    |         | CONCEPT |
   |         |         | Type    |         |    |         | MOD     |
   +---------+---------+---------+---------+----+---------+---------+
   | 1.      | >>>>    | Value   | (004    | CS | 0004    | CODE    |
   | 6.1.6.1 |         | Type    | 0,a040) |    |         |         |
   +---------+---------+---------+---------+----+---------+---------+
   | 1.      | >>>>    | Concept | (004    | SQ | f       |         |
   | 6.1.6.1 |         | Name    | 0,a043) |    | fffffff |         |
   |         |         | Code    |         |    |         |         |
   |         |         | S       |         |    |         |         |
   |         |         | equence |         |    |         |         |
   +---------+---------+---------+---------+----+---------+---------+
   |         | %item   |         |         |    |         |         |
   +---------+---------+---------+---------+----+---------+---------+
   | 1.      | >>>>>   | Code    | (000    | SH | 0006    | 121401  |
   | 6.1.6.1 |         | Value   | 8,0100) |    |         |         |
   +---------+---------+---------+---------+----+---------+---------+
   | 1.      | >>>>>   | Coding  | (000    | SH | 0004    | DCM     |
   | 6.1.6.1 |         | Scheme  | 8,0102) |    |         |         |
   |         |         | Des     |         |    |         |         |
   |         |         | ignator |         |    |         |         |
   +---------+---------+---------+---------+----+---------+---------+
   | 1.      | >>>>>   | Code    | (000    | LO | 000a    | Der     |
   | 6.1.6.1 |         | Meaning | 8,0104) |    |         | ivation |
   +---------+---------+---------+---------+----+---------+---------+
   |         | %       |         |         |    |         |         |
   |         | enditem |         |         |    |         |         |
   +---------+---------+---------+---------+----+---------+---------+
   |         | %endseq |         |         |    |         |         |
   +---------+---------+---------+---------+----+---------+---------+
   | 1.      | >>>>    | Concept | (004    | SQ | f       |         |
   | 6.1.6.1 |         | Code    | 0,a168) |    | fffffff |         |
   |         |         | S       |         |    |         |         |
   |         |         | equence |         |    |         |         |
   +---------+---------+---------+---------+----+---------+---------+
   |         | %item   |         |         |    |         |         |
   +---------+---------+---------+---------+----+---------+---------+
   | 1.      | >>>>>   | Code    | (000    | SH | 000a    | 25      |
   | 6.1.6.1 |         | Value   | 8,0100) |    |         | 5605001 |
   +---------+---------+---------+---------+----+---------+---------+
   | 1.      | >>>>>   | Coding  | (000    | SH | 0004    | SCT     |
   | 6.1.6.1 |         | Scheme  | 8,0102) |    |         |         |
   |         |         | Des     |         |    |         |         |
   |         |         | ignator |         |    |         |         |
   +---------+---------+---------+---------+----+---------+---------+
   | 1.      | >>>>>   | Code    | (000    | LO | 0008    | Minimum |
   | 6.1.6.1 |         | Meaning | 8,0104) |    |         |         |
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
   |         | %       |         |         |    |         |         |
   |         | enditem |         |         |    |         |         |
   +---------+---------+---------+---------+----+---------+---------+
   |         | %item   |         |         |    |         |         |
   +---------+---------+---------+---------+----+---------+---------+
   | 1.6.1.7 | >>>     | Relat   | (004    | CS | 0008    | C       |
   |         |         | ionship | 0,a010) |    |         | ONTAINS |
   |         |         | Type    |         |    |         |         |
   +---------+---------+---------+---------+----+---------+---------+
   | 1.6.1.7 | >>>     | Value   | (004    | CS | 0004    | NUM     |
   |         |         | Type    | 0,a040) |    |         |         |
   +---------+---------+---------+---------+----+---------+---------+
   | 1.6.1.7 | >>>     | Concept | (004    | SQ | f       |         |
   |         |         | Name    | 0,a043) |    | fffffff |         |
   |         |         | Code    |         |    |         |         |
   |         |         | S       |         |    |         |         |
   |         |         | equence |         |    |         |         |
   +---------+---------+---------+---------+----+---------+---------+
   |         | %item   |         |         |    |         |         |
   +---------+---------+---------+---------+----+---------+---------+
   | 1.6.1.7 | >>>>    | Code    | (000    | SH | 0006    | 126401  |
   |         |         | Value   | 8,0100) |    |         |         |
   +---------+---------+---------+---------+----+---------+---------+
   | 1.6.1.7 | >>>>    | Coding  | (000    | SH | 0004    | DCM     |
   |         |         | Scheme  | 8,0102) |    |         |         |
   |         |         | Des     |         |    |         |         |
   |         |         | ignator |         |    |         |         |
   +---------+---------+---------+---------+----+---------+---------+
   | 1.6.1.7 | >>>>    | Code    | (000    | LO | 0006    | SUVbw   |
   |         |         | Meaning | 8,0104) |    |         |         |
   +---------+---------+---------+---------+----+---------+---------+
   |         | %       |         |         |    |         |         |
   |         | enditem |         |         |    |         |         |
   +---------+---------+---------+---------+----+---------+---------+
   |         | %endseq |         |         |    |         |         |
   +---------+---------+---------+---------+----+---------+---------+
   | 1.6.1.7 | >>>     | Obse    | (004    | UI | 002c    | 2.      |
   |         |         | rvation | 0,a171) |    |         | 25.2052 |
   |         |         | UID     |         |    |         | 9224388 |
   |         |         |         |         |    |         | 5258032 |
   |         |         |         |         |    |         | 4288193 |
   |         |         |         |         |    |         | 3090958 |
   |         |         |         |         |    |         | 0896146 |
   +---------+---------+---------+---------+----+---------+---------+
   | 1.6.1.7 | >>>     | M       | (004    | SQ | f       |         |
   |         |         | easured | 0,a300) |    | fffffff |         |
   |         |         | Value   |         |    |         |         |
   |         |         | S       |         |    |         |         |
   |         |         | equence |         |    |         |         |
   +---------+---------+---------+---------+----+---------+---------+
   |         | %item   |         |         |    |         |         |
   +---------+---------+---------+---------+----+---------+---------+
   | 1.6.1.7 | >>>>    | Meas    | (004    | SQ | f       |         |
   |         |         | urement | 0,08ea) |    | fffffff |         |
   |         |         | Units   |         |    |         |         |
   |         |         | Code    |         |    |         |         |
   |         |         | S       |         |    |         |         |
   |         |         | equence |         |    |         |         |
   +---------+---------+---------+---------+----+---------+---------+
   |         | %item   |         |         |    |         |         |
   +---------+---------+---------+---------+----+---------+---------+
   | 1.6.1.7 | >>>>>   | Code    | (000    | SH | 000c    | g/ml    |
   |         |         | Value   | 8,0100) |    |         | {SUVbw} |
   +---------+---------+---------+---------+----+---------+---------+
   | 1.6.1.7 | >>>>>   | Coding  | (000    | SH | 0004    | UCUM    |
   |         |         | Scheme  | 8,0102) |    |         |         |
   |         |         | Des     |         |    |         |         |
   |         |         | ignator |         |    |         |         |
   +---------+---------+---------+---------+----+---------+---------+
   | 1.6.1.7 | >>>>>   | Code    | (000    | LO | 000c    | g/ml    |
   |         |         | Meaning | 8,0104) |    |         | {SUVbw} |
   +---------+---------+---------+---------+----+---------+---------+
   |         | %       |         |         |    |         |         |
   |         | enditem |         |         |    |         |         |
   +---------+---------+---------+---------+----+---------+---------+
   |         | %endseq |         |         |    |         |         |
   +---------+---------+---------+---------+----+---------+---------+
   | 1.6.1.7 | >>>>    | Numeric | (004    | DS | 0008    | 5.68816 |
   |         |         | Value   | 0,a30a) |    |         |         |
   +---------+---------+---------+---------+----+---------+---------+
   |         | %       |         |         |    |         |         |
   |         | enditem |         |         |    |         |         |
   +---------+---------+---------+---------+----+---------+---------+
   |         | %endseq |         |         |    |         |         |
   +---------+---------+---------+---------+----+---------+---------+
   | 1.6.1.7 | >>>     | Content | (004    | SQ | f       |         |
   |         |         | S       | 0,a730) |    | fffffff |         |
   |         |         | equence |         |    |         |         |
   +---------+---------+---------+---------+----+---------+---------+
   |         | %item   |         |         |    |         |         |
   +---------+---------+---------+---------+----+---------+---------+
   | 1.      | >>>>    | Relat   | (004    | CS | 0010    | HAS     |
   | 6.1.7.1 |         | ionship | 0,a010) |    |         | CONCEPT |
   |         |         | Type    |         |    |         | MOD     |
   +---------+---------+---------+---------+----+---------+---------+
   | 1.      | >>>>    | Value   | (004    | CS | 0004    | CODE    |
   | 6.1.7.1 |         | Type    | 0,a040) |    |         |         |
   +---------+---------+---------+---------+----+---------+---------+
   | 1.      | >>>>    | Concept | (004    | SQ | f       |         |
   | 6.1.7.1 |         | Name    | 0,a043) |    | fffffff |         |
   |         |         | Code    |         |    |         |         |
   |         |         | S       |         |    |         |         |
   |         |         | equence |         |    |         |         |
   +---------+---------+---------+---------+----+---------+---------+
   |         | %item   |         |         |    |         |         |
   +---------+---------+---------+---------+----+---------+---------+
   | 1.      | >>>>>   | Code    | (000    | SH | 0006    | 121401  |
   | 6.1.7.1 |         | Value   | 8,0100) |    |         |         |
   +---------+---------+---------+---------+----+---------+---------+
   | 1.      | >>>>>   | Coding  | (000    | SH | 0004    | DCM     |
   | 6.1.7.1 |         | Scheme  | 8,0102) |    |         |         |
   |         |         | Des     |         |    |         |         |
   |         |         | ignator |         |    |         |         |
   +---------+---------+---------+---------+----+---------+---------+
   | 1.      | >>>>>   | Code    | (000    | LO | 000a    | Der     |
   | 6.1.7.1 |         | Meaning | 8,0104) |    |         | ivation |
   +---------+---------+---------+---------+----+---------+---------+
   |         | %       |         |         |    |         |         |
   |         | enditem |         |         |    |         |         |
   +---------+---------+---------+---------+----+---------+---------+
   |         | %endseq |         |         |    |         |         |
   +---------+---------+---------+---------+----+---------+---------+
   | 1.      | >>>>    | Concept | (004    | SQ | f       |         |
   | 6.1.7.1 |         | Code    | 0,a168) |    | fffffff |         |
   |         |         | S       |         |    |         |         |
   |         |         | equence |         |    |         |         |
   +---------+---------+---------+---------+----+---------+---------+
   |         | %item   |         |         |    |         |         |
   +---------+---------+---------+---------+----+---------+---------+
   | 1.      | >>>>>   | Code    | (000    | SH | 0008    | 5       |
   | 6.1.7.1 |         | Value   | 8,0100) |    |         | 6851009 |
   +---------+---------+---------+---------+----+---------+---------+
   | 1.      | >>>>>   | Coding  | (000    | SH | 0004    | SCT     |
   | 6.1.7.1 |         | Scheme  | 8,0102) |    |         |         |
   |         |         | Des     |         |    |         |         |
   |         |         | ignator |         |    |         |         |
   +---------+---------+---------+---------+----+---------+---------+
   | 1.      | >>>>>   | Code    | (000    | LO | 0008    | Maximum |
   | 6.1.7.1 |         | Meaning | 8,0104) |    |         |         |
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
   |         | %       |         |         |    |         |         |
   |         | enditem |         |         |    |         |         |
   +---------+---------+---------+---------+----+---------+---------+
   |         | %item   |         |         |    |         |         |
   +---------+---------+---------+---------+----+---------+---------+
   | 1.6.1.8 | >>>     | Relat   | (004    | CS | 0008    | C       |
   |         |         | ionship | 0,a010) |    |         | ONTAINS |
   |         |         | Type    |         |    |         |         |
   +---------+---------+---------+---------+----+---------+---------+
   | 1.6.1.8 | >>>     | Value   | (004    | CS | 0004    | NUM     |
   |         |         | Type    | 0,a040) |    |         |         |
   +---------+---------+---------+---------+----+---------+---------+
   | 1.6.1.8 | >>>     | Concept | (004    | SQ | f       |         |
   |         |         | Name    | 0,a043) |    | fffffff |         |
   |         |         | Code    |         |    |         |         |
   |         |         | S       |         |    |         |         |
   |         |         | equence |         |    |         |         |
   +---------+---------+---------+---------+----+---------+---------+
   |         | %item   |         |         |    |         |         |
   +---------+---------+---------+---------+----+---------+---------+
   | 1.6.1.8 | >>>>    | Code    | (000    | SH | 0006    | 126401  |
   |         |         | Value   | 8,0100) |    |         |         |
   +---------+---------+---------+---------+----+---------+---------+
   | 1.6.1.8 | >>>>    | Coding  | (000    | SH | 0004    | DCM     |
   |         |         | Scheme  | 8,0102) |    |         |         |
   |         |         | Des     |         |    |         |         |
   |         |         | ignator |         |    |         |         |
   +---------+---------+---------+---------+----+---------+---------+
   | 1.6.1.8 | >>>>    | Code    | (000    | LO | 0006    | SUVbw   |
   |         |         | Meaning | 8,0104) |    |         |         |
   +---------+---------+---------+---------+----+---------+---------+
   |         | %       |         |         |    |         |         |
   |         | enditem |         |         |    |         |         |
   +---------+---------+---------+---------+----+---------+---------+
   |         | %endseq |         |         |    |         |         |
   +---------+---------+---------+---------+----+---------+---------+
   | 1.6.1.8 | >>>     | Obse    | (004    | UI | 002c    | 2       |
   |         |         | rvation | 0,a171) |    |         | .25.701 |
   |         |         | UID     |         |    |         | 6025208 |
   |         |         |         |         |    |         | 0234577 |
   |         |         |         |         |    |         | 1678475 |
   |         |         |         |         |    |         | 0994836 |
   |         |         |         |         |    |         | 8893276 |
   +---------+---------+---------+---------+----+---------+---------+
   | 1.6.1.8 | >>>     | M       | (004    | SQ | f       |         |
   |         |         | easured | 0,a300) |    | fffffff |         |
   |         |         | Value   |         |    |         |         |
   |         |         | S       |         |    |         |         |
   |         |         | equence |         |    |         |         |
   +---------+---------+---------+---------+----+---------+---------+
   |         | %item   |         |         |    |         |         |
   +---------+---------+---------+---------+----+---------+---------+
   | 1.6.1.8 | >>>>    | Meas    | (004    | SQ | f       |         |
   |         |         | urement | 0,08ea) |    | fffffff |         |
   |         |         | Units   |         |    |         |         |
   |         |         | Code    |         |    |         |         |
   |         |         | S       |         |    |         |         |
   |         |         | equence |         |    |         |         |
   +---------+---------+---------+---------+----+---------+---------+
   |         | %item   |         |         |    |         |         |
   +---------+---------+---------+---------+----+---------+---------+
   | 1.6.1.8 | >>>>>   | Code    | (000    | SH | 000c    | g/ml    |
   |         |         | Value   | 8,0100) |    |         | {SUVbw} |
   +---------+---------+---------+---------+----+---------+---------+
   | 1.6.1.8 | >>>>>   | Coding  | (000    | SH | 0004    | UCUM    |
   |         |         | Scheme  | 8,0102) |    |         |         |
   |         |         | Des     |         |    |         |         |
   |         |         | ignator |         |    |         |         |
   +---------+---------+---------+---------+----+---------+---------+
   | 1.6.1.8 | >>>>>   | Code    | (000    | LO | 000c    | g/ml    |
   |         |         | Meaning | 8,0104) |    |         | {SUVbw} |
   +---------+---------+---------+---------+----+---------+---------+
   |         | %       |         |         |    |         |         |
   |         | enditem |         |         |    |         |         |
   +---------+---------+---------+---------+----+---------+---------+
   |         | %endseq |         |         |    |         |         |
   +---------+---------+---------+---------+----+---------+---------+
   | 1.6.1.8 | >>>>    | Numeric | (004    | DS | 000e    | 2.32918 |
   |         |         | Value   | 0,a30a) |    |         | 6593407 |
   +---------+---------+---------+---------+----+---------+---------+
   |         | %       |         |         |    |         |         |
   |         | enditem |         |         |    |         |         |
   +---------+---------+---------+---------+----+---------+---------+
   |         | %endseq |         |         |    |         |         |
   +---------+---------+---------+---------+----+---------+---------+
   | 1.6.1.8 | >>>     | Content | (004    | SQ | f       |         |
   |         |         | S       | 0,a730) |    | fffffff |         |
   |         |         | equence |         |    |         |         |
   +---------+---------+---------+---------+----+---------+---------+
   |         | %item   |         |         |    |         |         |
   +---------+---------+---------+---------+----+---------+---------+
   | 1.      | >>>>    | Relat   | (004    | CS | 0010    | HAS     |
   | 6.1.8.1 |         | ionship | 0,a010) |    |         | CONCEPT |
   |         |         | Type    |         |    |         | MOD     |
   +---------+---------+---------+---------+----+---------+---------+
   | 1.      | >>>>    | Value   | (004    | CS | 0004    | CODE    |
   | 6.1.8.1 |         | Type    | 0,a040) |    |         |         |
   +---------+---------+---------+---------+----+---------+---------+
   | 1.      | >>>>    | Concept | (004    | SQ | f       |         |
   | 6.1.8.1 |         | Name    | 0,a043) |    | fffffff |         |
   |         |         | Code    |         |    |         |         |
   |         |         | S       |         |    |         |         |
   |         |         | equence |         |    |         |         |
   +---------+---------+---------+---------+----+---------+---------+
   |         | %item   |         |         |    |         |         |
   +---------+---------+---------+---------+----+---------+---------+
   | 1.      | >>>>>   | Code    | (000    | SH | 0006    | 121401  |
   | 6.1.8.1 |         | Value   | 8,0100) |    |         |         |
   +---------+---------+---------+---------+----+---------+---------+
   | 1.      | >>>>>   | Coding  | (000    | SH | 0004    | DCM     |
   | 6.1.8.1 |         | Scheme  | 8,0102) |    |         |         |
   |         |         | Des     |         |    |         |         |
   |         |         | ignator |         |    |         |         |
   +---------+---------+---------+---------+----+---------+---------+
   | 1.      | >>>>>   | Code    | (000    | LO | 000a    | Der     |
   | 6.1.8.1 |         | Meaning | 8,0104) |    |         | ivation |
   +---------+---------+---------+---------+----+---------+---------+
   |         | %       |         |         |    |         |         |
   |         | enditem |         |         |    |         |         |
   +---------+---------+---------+---------+----+---------+---------+
   |         | %endseq |         |         |    |         |         |
   +---------+---------+---------+---------+----+---------+---------+
   | 1.      | >>>>    | Concept | (004    | SQ | f       |         |
   | 6.1.8.1 |         | Code    | 0,a168) |    | fffffff |         |
   |         |         | S       |         |    |         |         |
   |         |         | equence |         |    |         |         |
   +---------+---------+---------+---------+----+---------+---------+
   |         | %item   |         |         |    |         |         |
   +---------+---------+---------+---------+----+---------+---------+
   | 1.      | >>>>>   | Code    | (000    | SH | 000a    | 37      |
   | 6.1.8.1 |         | Value   | 8,0100) |    |         | 3098007 |
   +---------+---------+---------+---------+----+---------+---------+
   | 1.      | >>>>>   | Coding  | (000    | SH | 0004    | SCT     |
   | 6.1.8.1 |         | Scheme  | 8,0102) |    |         |         |
   |         |         | Des     |         |    |         |         |
   |         |         | ignator |         |    |         |         |
   +---------+---------+---------+---------+----+---------+---------+
   | 1.      | >>>>>   | Code    | (000    | LO | 0004    | Mean    |
   | 6.1.8.1 |         | Meaning | 8,0104) |    |         |         |
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
   |         | %       |         |         |    |         |         |
   |         | enditem |         |         |    |         |         |
   +---------+---------+---------+---------+----+---------+---------+
   |         | %item   |         |         |    |         |         |
   +---------+---------+---------+---------+----+---------+---------+
   | 1.6.1.9 | >>>     | Relat   | (004    | CS | 0008    | C       |
   |         |         | ionship | 0,a010) |    |         | ONTAINS |
   |         |         | Type    |         |    |         |         |
   +---------+---------+---------+---------+----+---------+---------+
   | 1.6.1.9 | >>>     | Value   | (004    | CS | 0004    | NUM     |
   |         |         | Type    | 0,a040) |    |         |         |
   +---------+---------+---------+---------+----+---------+---------+
   | 1.6.1.9 | >>>     | Concept | (004    | SQ | f       |         |
   |         |         | Name    | 0,a043) |    | fffffff |         |
   |         |         | Code    |         |    |         |         |
   |         |         | S       |         |    |         |         |
   |         |         | equence |         |    |         |         |
   +---------+---------+---------+---------+----+---------+---------+
   |         | %item   |         |         |    |         |         |
   +---------+---------+---------+---------+----+---------+---------+
   | 1.6.1.9 | >>>>    | Code    | (000    | SH | 0006    | 126401  |
   |         |         | Value   | 8,0100) |    |         |         |
   +---------+---------+---------+---------+----+---------+---------+
   | 1.6.1.9 | >>>>    | Coding  | (000    | SH | 0004    | DCM     |
   |         |         | Scheme  | 8,0102) |    |         |         |
   |         |         | Des     |         |    |         |         |
   |         |         | ignator |         |    |         |         |
   +---------+---------+---------+---------+----+---------+---------+
   | 1.6.1.9 | >>>>    | Code    | (000    | LO | 0006    | SUVbw   |
   |         |         | Meaning | 8,0104) |    |         |         |
   +---------+---------+---------+---------+----+---------+---------+
   |         | %       |         |         |    |         |         |
   |         | enditem |         |         |    |         |         |
   +---------+---------+---------+---------+----+---------+---------+
   |         | %endseq |         |         |    |         |         |
   +---------+---------+---------+---------+----+---------+---------+
   | 1.6.1.9 | >>>     | Obse    | (004    | UI | 002c    | 2.      |
   |         |         | rvation | 0,a171) |    |         | 25.1406 |
   |         |         | UID     |         |    |         | 5702611 |
   |         |         |         |         |    |         | 9469861 |
   |         |         |         |         |    |         | 8958240 |
   |         |         |         |         |    |         | 8276708 |
   |         |         |         |         |    |         | 8344984 |
   +---------+---------+---------+---------+----+---------+---------+
   | 1.6.1.9 | >>>     | M       | (004    | SQ | f       |         |
   |         |         | easured | 0,a300) |    | fffffff |         |
   |         |         | Value   |         |    |         |         |
   |         |         | S       |         |    |         |         |
   |         |         | equence |         |    |         |         |
   +---------+---------+---------+---------+----+---------+---------+
   |         | %item   |         |         |    |         |         |
   +---------+---------+---------+---------+----+---------+---------+
   | 1.6.1.9 | >>>>    | Meas    | (004    | SQ | f       |         |
   |         |         | urement | 0,08ea) |    | fffffff |         |
   |         |         | Units   |         |    |         |         |
   |         |         | Code    |         |    |         |         |
   |         |         | S       |         |    |         |         |
   |         |         | equence |         |    |         |         |
   +---------+---------+---------+---------+----+---------+---------+
   |         | %item   |         |         |    |         |         |
   +---------+---------+---------+---------+----+---------+---------+
   | 1.6.1.9 | >>>>>   | Code    | (000    | SH | 000c    | g/ml    |
   |         |         | Value   | 8,0100) |    |         | {SUVbw} |
   +---------+---------+---------+---------+----+---------+---------+
   | 1.6.1.9 | >>>>>   | Coding  | (000    | SH | 0004    | UCUM    |
   |         |         | Scheme  | 8,0102) |    |         |         |
   |         |         | Des     |         |    |         |         |
   |         |         | ignator |         |    |         |         |
   +---------+---------+---------+---------+----+---------+---------+
   | 1.6.1.9 | >>>>>   | Code    | (000    | LO | 000c    | g/ml    |
   |         |         | Meaning | 8,0104) |    |         | {SUVbw} |
   +---------+---------+---------+---------+----+---------+---------+
   |         | %       |         |         |    |         |         |
   |         | enditem |         |         |    |         |         |
   +---------+---------+---------+---------+----+---------+---------+
   |         | %endseq |         |         |    |         |         |
   +---------+---------+---------+---------+----+---------+---------+
   | 1.6.1.9 | >>>>    | Numeric | (004    | DS | 0010    | 1       |
   |         |         | Value   | 0,a30a) |    |         | .882895 |
   |         |         |         |         |    |         | 2323684 |
   +---------+---------+---------+---------+----+---------+---------+
   |         | %       |         |         |    |         |         |
   |         | enditem |         |         |    |         |         |
   +---------+---------+---------+---------+----+---------+---------+
   |         | %endseq |         |         |    |         |         |
   +---------+---------+---------+---------+----+---------+---------+
   | 1.6.1.9 | >>>     | Content | (004    | SQ | f       |         |
   |         |         | S       | 0,a730) |    | fffffff |         |
   |         |         | equence |         |    |         |         |
   +---------+---------+---------+---------+----+---------+---------+
   |         | %item   |         |         |    |         |         |
   +---------+---------+---------+---------+----+---------+---------+
   | 1.      | >>>>    | Relat   | (004    | CS | 0010    | HAS     |
   | 6.1.9.1 |         | ionship | 0,a010) |    |         | CONCEPT |
   |         |         | Type    |         |    |         | MOD     |
   +---------+---------+---------+---------+----+---------+---------+
   | 1.      | >>>>    | Value   | (004    | CS | 0004    | CODE    |
   | 6.1.9.1 |         | Type    | 0,a040) |    |         |         |
   +---------+---------+---------+---------+----+---------+---------+
   | 1.      | >>>>    | Concept | (004    | SQ | f       |         |
   | 6.1.9.1 |         | Name    | 0,a043) |    | fffffff |         |
   |         |         | Code    |         |    |         |         |
   |         |         | S       |         |    |         |         |
   |         |         | equence |         |    |         |         |
   +---------+---------+---------+---------+----+---------+---------+
   |         | %item   |         |         |    |         |         |
   +---------+---------+---------+---------+----+---------+---------+
   | 1.      | >>>>>   | Code    | (000    | SH | 0006    | 121401  |
   | 6.1.9.1 |         | Value   | 8,0100) |    |         |         |
   +---------+---------+---------+---------+----+---------+---------+
   | 1.      | >>>>>   | Coding  | (000    | SH | 0004    | DCM     |
   | 6.1.9.1 |         | Scheme  | 8,0102) |    |         |         |
   |         |         | Des     |         |    |         |         |
   |         |         | ignator |         |    |         |         |
   +---------+---------+---------+---------+----+---------+---------+
   | 1.      | >>>>>   | Code    | (000    | LO | 000a    | Der     |
   | 6.1.9.1 |         | Meaning | 8,0104) |    |         | ivation |
   +---------+---------+---------+---------+----+---------+---------+
   |         | %       |         |         |    |         |         |
   |         | enditem |         |         |    |         |         |
   +---------+---------+---------+---------+----+---------+---------+
   |         | %endseq |         |         |    |         |         |
   +---------+---------+---------+---------+----+---------+---------+
   | 1.      | >>>>    | Concept | (004    | SQ | f       |         |
   | 6.1.9.1 |         | Code    | 0,a168) |    | fffffff |         |
   |         |         | S       |         |    |         |         |
   |         |         | equence |         |    |         |         |
   +---------+---------+---------+---------+----+---------+---------+
   |         | %item   |         |         |    |         |         |
   +---------+---------+---------+---------+----+---------+---------+
   | 1.      | >>>>>   | Code    | (000    | SH | 000a    | 38      |
   | 6.1.9.1 |         | Value   | 8,0100) |    |         | 6136009 |
   +---------+---------+---------+---------+----+---------+---------+
   | 1.      | >>>>>   | Coding  | (000    | SH | 0004    | SCT     |
   | 6.1.9.1 |         | Scheme  | 8,0102) |    |         |         |
   |         |         | Des     |         |    |         |         |
   |         |         | ignator |         |    |         |         |
   +---------+---------+---------+---------+----+---------+---------+
   | 1.      | >>>>>   | Code    | (000    | LO | 0012    | S       |
   | 6.1.9.1 |         | Meaning | 8,0104) |    |         | tandard |
   |         |         |         |         |    |         | De      |
   |         |         |         |         |    |         | viation |
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
   |         | %       |         |         |    |         |         |
   |         | enditem |         |         |    |         |         |
   +---------+---------+---------+---------+----+---------+---------+
   |         | %item   |         |         |    |         |         |
   +---------+---------+---------+---------+----+---------+---------+
   | 1       | >>>     | Relat   | (004    | CS | 0008    | C       |
   | .6.1.10 |         | ionship | 0,a010) |    |         | ONTAINS |
   |         |         | Type    |         |    |         |         |
   +---------+---------+---------+---------+----+---------+---------+
   | 1       | >>>     | Value   | (004    | CS | 0004    | TEXT    |
   | .6.1.10 |         | Type    | 0,a040) |    |         |         |
   +---------+---------+---------+---------+----+---------+---------+
   | 1       | >>>     | Concept | (004    | SQ | f       |         |
   | .6.1.10 |         | Name    | 0,a043) |    | fffffff |         |
   |         |         | Code    |         |    |         |         |
   |         |         | S       |         |    |         |         |
   |         |         | equence |         |    |         |         |
   +---------+---------+---------+---------+----+---------+---------+
   |         | %item   |         |         |    |         |         |
   +---------+---------+---------+---------+----+---------+---------+
   | 1       | >>>>    | Code    | (000    | SH | 0006    | 121106  |
   | .6.1.10 |         | Value   | 8,0100) |    |         |         |
   +---------+---------+---------+---------+----+---------+---------+
   | 1       | >>>>    | Coding  | (000    | SH | 0004    | DCM     |
   | .6.1.10 |         | Scheme  | 8,0102) |    |         |         |
   |         |         | Des     |         |    |         |         |
   |         |         | ignator |         |    |         |         |
   +---------+---------+---------+---------+----+---------+---------+
   | 1       | >>>>    | Code    | (000    | LO | 0008    | Comment |
   | .6.1.10 |         | Meaning | 8,0104) |    |         |         |
   +---------+---------+---------+---------+----+---------+---------+
   |         | %       |         |         |    |         |         |
   |         | enditem |         |         |    |         |         |
   +---------+---------+---------+---------+----+---------+---------+
   |         | %endseq |         |         |    |         |         |
   +---------+---------+---------+---------+----+---------+---------+
   | 1       | >>>     | Text    | (004    | UT | 0014    | PT / WB |
   | .6.1.10 |         | Value   | 0,a160) |    |         | NAC     |
   |         |         |         |         |    |         | P600 /  |
   |         |         |         |         |    |         | 0       |
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
   |         | %       |         |         |    |         |         |
   |         | enditem |         |         |    |         |         |
   +---------+---------+---------+---------+----+---------+---------+
   |         | %endseq |         |         |    |         |         |
   +---------+---------+---------+---------+----+---------+---------+

.. _sect_A.8:

Overview of Data Types
----------------------

DICOM data types are specified in PS3.5 of the Standard ().

The AIM V4 data types are a subset of
`biblioentry_title <#biblio_ISO_21090>`__, which are in turn based on
`biblioentry_title <#biblio_HL7V3DTR1>`__. The AIM V4 data types used
are documented in `biblioentry_title <#biblio_AIMV3V4Changes>`__ and
`biblioentry_title <#biblio_AIM_Model_Extending>`__.

While a complete comparison of DICOM and
`biblioentry_title <#biblio_ISO_21090>`__ data types, cardinality and
optionality is beyond the scope of this mapping guide, some hints are
given on topics that are relevant for transforming AIM instances and
DICOM SR Measurement Reports.

The AIM V4 model uses the data types as specified in
`table_title <#table_A.8-2>`__ from
`biblioentry_title <#biblio_ISO_21090>`__, of which only a subset are
encountered in use cases described by this mapping. In XML encoded AIM
instances, the data type is not explicitly encoded, though it is defined
in the UML model.

.. table:: ISO 21090 Data Types used in AIM V4

   +----------------------+----------------------------------------------+
   | ISO 21090 Data Types | Description                                  |
   +======================+==============================================+
   | BL                   | Boolean (two-valued logic). A BL value can   |
   |                      | be either true or false, or may have a       |
   |                      | nullFlavor.                                  |
   +----------------------+----------------------------------------------+
   | CD                   | Concept Descriptor. A reference to a concept |
   |                      | defined in an external code system,          |
   |                      | terminology or ontology, or an expression in |
   |                      | some syntax defined by the referenced code   |
   |                      | system.                                      |
   +----------------------+----------------------------------------------+
   | II                   | Instance Identifier. An identifier that      |
   |                      | uniquely identifies a thing or object.       |
   |                      | Instance identifiers are usually defined     |
   |                      | based on ISO object identifiers.             |
   +----------------------+----------------------------------------------+
   | INT                  | Integer. No arbitrary limit is imposed on    |
   |                      | the range of integer numbers.                |
   +----------------------+----------------------------------------------+
   | REAL                 | Fractional numbers. The typical              |
   |                      | representation is decimal.                   |
   +----------------------+----------------------------------------------+
   | ST                   | Character string. Shall have at least one    |
   |                      | character or else have a nullFlavor.         |
   +----------------------+----------------------------------------------+
   | TS                   | Point in time. A quantity specifying a point |
   |                      | on the axis of natural time. Most often      |
   |                      | represented as a calendar expression.        |
   +----------------------+----------------------------------------------+

Additional data type mapping considerations include:

a. Optionality and nullFlavor

   If the original AIM instance does not include values that are
   required or mandatory in DICOM SR TID 1500, fixed values are
   specified since empty values are not permitted in DICOM SR TEXT and
   CODE entries and omitting the Content Item would violate the template
   constraints. All nullFlavor values are treated as empty, except for
   numeric values.

b. Character Sets

   DICOM provides information on the interpretation of text data types
   by specifying a default character set (ISO-IR 6) and "Specific
   Character Set" (0008,0005) values that are used if the Basic Graphic
   Set is expanded or replaced. For AIM, the XML declaration attribute
   "encoding" (overall document) and the attribute "charset" (for ST
   data type values) may be used to provide information on character
   sets. See the description of Specific Character Set in `Mapping of
   DICOM SOP Common Module <#sect_A.6.1.1.11>`__.

c. Character strings

   In general, ST text value attributes in AIM XML elements are mapped
   to DICOM Text Value (0040,A160) of value type TEXT (with a VR of
   Unlimited Text (UT)) in the SR Content Tree. No maximum length is
   specified for AIM elements and attributes.

   Some text value attributes in AIM XML elements are mapped to
   Attributes in the DICOM header, and DICOM length limits may apply to
   character strings such as Long String (LO), e.g., Patient ID.

d. Identifiers

   Unique identifiers in AIM V4 are encoded as the root attribute of an
   XML element (aim:uniqueIdentifier/​@root), which has an II data type,
   and are mapped to the DICOM UI VR, which is limited to 64 bytes.

e. Codes

   Codes in AIM V4 are encoded as attributes of the aim:typeCode XML
   element and are mapped as specified in `table_title <#table_A.8-2>`__
   below for the `biblioentry_title <#biblio_ISO_21090>`__ code data
   type (CD). The code and codeSystemName attributes are encountered as
   attributes of the aim:typeCode XML element, but the displayName is
   the value attribute of a child element,
   aim:typeCode/​iso:displayName/​@value. Note that codeSystem (Coding
   Scheme UID) is usually not sent, even though it is required by
   `biblioentry_title <#biblio_ISO_21090>`__. DICOM also supports other
   Attributes for encoding code values that exceed 16 characters in
   length.

   .. table:: Mapping between DICOM Basic Code Attributes and AIM ISO
   21090 Code Data Types (CD)

      +----------------+----------------+----------------+----------------+
      | DICOM          | AIM Element    |                |                |
      | Attribute and  | and Attribute  |                |                |
      | VR             | and ISO 21090  |                |                |
      |                | Data Type      |                |                |
      +================+================+================+================+
      | Code Value     | SH             | aim:t          | CD.c           |
      | (0008,0100)    |                | ypeCode/​@code | haracterstring |
      +----------------+----------------+----------------+----------------+
      | Coding Scheme  | UI             | aim:typeCod    | CD.c           |
      | UID            |                | e/​@codeSystem | haracterstring |
      | (0008,0x010C)  |                |                |                |
      +----------------+----------------+----------------+----------------+
      | Coding Scheme  | SH             | a              | CD.c           |
      | Designator     |                | im:typeCode/​@ | haracterstring |
      | (0008,0102)    |                | codeSystemName |                |
      +----------------+----------------+----------------+----------------+
      | Coding Scheme  | SH             | aim:           | CD.c           |
      | Version        |                | typeCode/​@cod | haracterstring |
      | (0008,0103)    |                | eSystemVersion |                |
      +----------------+----------------+----------------+----------------+
      | Code Meaning   | LO             | aim:typeC      | CD.ST          |
      | (0008,0104)    |                | ode/​iso:displ |                |
      |                |                | ayName/​@value |                |
      +----------------+----------------+----------------+----------------+

f. Date and Time

   -  The AIM V4 XML element aim:dateTime/​@value attribute corresponds
      to the ISO 21090 TS data type, and is mapped to the DICOM DateTime
      (DT) VR, or the combination of separate Date (DA) and Time (TM)
      Attributes.

   -  DICOM DT matches TS except for the number of decimal places of
      fractional seconds (6 for DT versus 4 for TS).

   -  DICOM DA matches the TS part YYYYMMDD (Y=Year, M=Month, D=Day),
      except that TS may be missing DD or MMDD.

   -  DICOM TM matches the TS part HHMMSS.UUUUUU (H=Hour, M=Minute,
      S=Second, U=Fractional Second) except for the number of decimal
      places of fractional seconds (6 for DT versus 4 for TS).

   -  If available, the DICOM Timezone Offset From UTC (0008,0201) used
      for DA or TM data types may be populated using time zone offset
      values from the ISO 21090 TS value.

   -  ISO TS allows for separators; these need to be removed for
      conversion to DT, DA and TM.

g. Person Names

   -  DICOM Person Name (PN) shall be mapped from
      `biblioentry_title <#biblio_ISO_21090>`__ data type Person Name
      (PN) as described in `table_title <#table_A.8-3>`__.

      .. table:: Mapping between DICOM Person Name (PN) ans ISO 21090
      Data Type Person Name (PN)

         ====================== ========================================
         DICOM Person Name (PN) ISO 21090 Data Type: Person Name (PN)
         ====================== ========================================
         <family_name_complex>  Family Part type
         <given_name_complex>   Given Part type
         <middle_name>          Given Part type - order of parts matters
         <name_suffix>          Suffix Part type
         <name_prefix>          Prefix Part type
         ====================== ========================================

   -  `biblioentry_title <#biblio_ISO_21090>`__ PN may contain multiple
      given names. DICOM PN Middle Name shall be mapped to
      `biblioentry_title <#biblio_ISO_21090>`__ PN Given Name Part type.

      John Robert Morrison, Ph.D. "Morrison^John Robert^^^Ph.D." [One
      family name; two given names; no middle name; no prefix; one
      suffix] can be represented as a
      `biblioentry_title <#biblio_ISO_21090>`__ Person Name (PN) in the
      following way:

      ::

         <name>
                 <given>John</given>
                 <given>Robert</given>
                 <family>Morrison</family>
                 <suffix>Ph.D.</suffix>
             </name>

   -  The following `biblioentry_title <#biblio_ISO_21090>`__ PN use
      codes may be used to represent multi-part DICOM person names: ABC
      (Alphabetic), IDE (Ideographic), SYL (Phonetic).

      ::

         <name use="ABC">
                 <family>KIMURA</family>
                 <given>MICHIO</given>
             </name>
             <name use='IDE'>
                 <family>木村</family>
                 <given>道男</given>
             </name>
             <name use="SYL">
                 <family>きむら</family>
                 <given>みちお</given>
             </name>

h. Numeric Measurements

   DICOM Numeric Measurement value types shall be mapped from the
   `biblioentry_title <#biblio_ISO_21090>`__ data types as specified in
   `table_title <#table_A.8-4>`__.

   .. table:: Mapping between DICOM Numeric Measurement Value Types and
   ISO 21090 Data Types

      +--------------------+--------------------+--------------------+----+
      | DICOM , and :      | AIM Path and ISO   |                    |    |
      | Numeric            | 21090 Data Type    |                    |    |
      | Measurement (NUM)  |                    |                    |    |
      | Value Type         |                    |                    |    |
      +====================+====================+====================+====+
      | Measured Value     | Code Sequence      | CalculationE       | CD |
      | Sequence           | Macro              | ntity/​typeCode[1] |    |
      | (0040,A300) >      |                    |                    |    |
      | Concept Name Code  |                    |                    |    |
      | Sequence           |                    |                    |    |
      | (0040,A043)        |                    |                    |    |
      +--------------------+--------------------+--------------------+----+
      | Measured Value     | DS                 | Ca                 | ST |
      | Sequence           |                    | lculationEntity/​c |    |
      | (0040,A300) >      |                    | alculationResultCo |    |
      | Numeric Value      |                    | llection/​Calculat |    |
      | (0040,A30A)        |                    | ionResult/​​@value |    |
      |                    |                    |                    |    |
      |                    |                    | Calculatio         |    |
      |                    |                    | nEntity/​calculati |    |
      |                    |                    | onResultCollection |    |
      |                    |                    | /​CalculationResul |    |
      |                    |                    | t/​​calculationDat |    |
      |                    |                    | aCollection/​Calcu |    |
      |                    |                    | lationData/​@value |    |
      +--------------------+--------------------+--------------------+----+
      | Measured Value     | Code Sequence      | Calculat           | ST |
      | Sequence           | Macro              | ionEntity/​calcula |    |
      | (0040,A300) >      |                    | tionResultCollecti |    |
      | Measurement Units  |                    | on/​CalculationRes |    |
      | Code Sequence      |                    | ult/​unitOfMeasure |    |
      | (0040,08EA)        |                    |                    |    |
      +--------------------+--------------------+--------------------+----+
      | Numeric Value      | Code Sequence      | Calculati          | ST |
      | Qualifier Code     | Macro              | onEntity/​calculat |    |
      | Sequence           |                    | ionResultCollectio |    |
      | (0040,A301)        |                    | n/​CalculationResu |    |
      |                    |                    | lt/​calculationDat |    |
      |                    |                    | aCollection/​Calcu |    |
      |                    |                    | lationData/​@value |    |
      +--------------------+--------------------+--------------------+----+

   The `biblioentry_title <#biblio_ISO_21090>`__ PQ data type is not
   used in AIM.

   The Concept Name of the measurement is usually pre-coordinated in a
   single CalculationEntity/​typeCode entry. If there is more than one
   CalculationEntity/​typeCode, the first is assumed to be the primary
   concept and the others may be modifiers that, if recognized as such,
   may be mapped to method and derivation, or if otherwise recognized
   and name-value pair of concepts can be constructed can be encoded as
   generic modifiers, but otherwise have to be ignored.

   The Numeric Value may be found as the single value of a
   CompactCalculationResult (i.e., value child of CalculationResult) or
   the first value of an ExtendedCalculationResult (i.e., nested within
   calculationResultCollection). This can give rise to a difference in
   representation in a round trip conversion.

   Units of measurement shall be converted from a text string (ST) to a
   Coded Sequence entry using the UCUM Code Values and "UCUM" as the
   Coding Scheme Designator (in AIM, CalculationResult/​unitOfMeasure is
   defined as "A string representation of UCUM unit for the value of the
   calculation").

   The AIM CalculationData/​@value shall be assumed to be in the US
   English locale (i.e., periods are used as the decimal point, not
   commas, etc.).

   The length of the AIM CalculationData/​@value ST is not limited, but
   the DICOM DS value representation is limited to 16 characters. Values
   of CalculationData/​@value that are too long shall be truncated or
   rounded to fit in an implementation-dependent manner.

   The CalculationResult/​dataType (e.g., Double, Integer) is not
   encoded in the DICOM mapping, since all DICOM SR numeric values are
   encoded as a Decimal String (DS), so in a round trip from AIM to
   DICOM and back to AIM will not be recovered (i.e., will always be
   encoded as Double). For the use cases for this mapping, it is likely
   that all measurements will be Double anyway.

   DICOM allows the Measured Value Sequence (0040,A300) to be sent zero
   length (empty) if there is no value. In such cases the Numeric Value
   Qualifier Code Sequence (0040,A301) may be used in DICOM to send a
   code indicating why, either because of an invalid floating point
   result (e.g., (114000, DCM, "Not a number") corresponding to
   `biblioentry_title <#biblio_IEEE754>`__ NaN), or for more general
   reasons (e.g., (114006, DCM, "Measurement failure")). See .
   `table_title <#table_A.8-4>`__ indicates that a non-numeric
   CalculationData/@value may be mapped to Numeric Value Qualifier Code
   Sequence (0040,A301). Various possible mappings of AIM string values
   to a subset of DICOM codes corresponding to
   `biblioentry_title <#biblio_IEEE754>`__ are defined in
   `table_title <#table_A.8-5>`__. These are based on the:

   -  Java Double.toString(double) definition (see
      https://docs.oracle.com/javase/8/docs/api/java/lang/Double.html#toString-double-)

   -  `biblioentry_title <#biblio_XSD_DataTypes>`__

   -  `biblioentry_title <#biblio_ISO_21090>`__

   No similar standard C or C++ mapping is known to exist (e.g., for
   libc dtostr() or sprintf()). Other languages offer some flexibility
   (e.g., Python supports case insensitive variants of "NaN" and
   "Infinity", the latter with or without a sign; see
   http://docs.python.org/3/library/functions.html#float). For
   JavaScript, see
   https://tc39.github.io/ecma262/#sec-tostring-applied-to-the-number-type,
   https://tc39.github.io/ecma262/#sec-parsefloat-string and
   https://tc39.github.io/ecma262/#sec-number.parsefloat. The table
   describes a subset of possible values, the mapping may not be exact
   (e.g., the definitions of NaN may differ), the mapping is ambiguous
   (since AIM does not define which string source to use), and the
   mapping of other values is undefined.

   .. table:: Mapping between DICOM Numeric Value Qualifier Code
   Sequence and AIM ST

      +-------------------+-------------+------------+-------------------+
      | DICOM Code        | Java String | XML Schema | ISO 21090 Null    |
      |                   |             |            | Flavor            |
      +===================+=============+============+===================+
      | (114000, DCM,     | NaN         | NaN        |                   |
      | "Not a number")   |             |            |                   |
      +-------------------+-------------+------------+-------------------+
      | (114001, DCM,     | -Infinity   | -INF       | NINF              |
      | "Negative         |             |            |                   |
      | Infinity")        |             |            |                   |
      +-------------------+-------------+------------+-------------------+
      | (114002, DCM,     | Infinity    | INF        | PINF              |
      | "Positive         |             |            |                   |
      | Infinity")        |             |            |                   |
      +-------------------+-------------+------------+-------------------+

i. Image and segmentation references

   DICOM image references may be mapped as specified in
   `table_title <#table_A.8-6>`__.

   .. table:: DICOM Image references to AIM Path

      +-------------------+-------------------+-------------------+-----+
      | DICOM , and :     | AIM Path and ISO  |                   |     |
      | Image Reference   | 21090 Data Type   |                   |     |
      | (IMAGE) Value     |                   |                   |     |
      | Type              |                   |                   |     |
      +===================+===================+===================+=====+
      | Referenced SOP    | UI                | /Image​Annotatio  | II  |
      | Sequence >        |                   | n​Collection/​ima |     |
      | Referenced SOP    |                   | ge​Annotations/​I |     |
      | Class UID         |                   | mage​Annotation/​ |     |
      |                   |                   | imageReferenceEnt |     |
      |                   |                   | ityCollection/​Im |     |
      |                   |                   | ageReferenceEntit |     |
      |                   |                   | y/​imageStudy/​im |     |
      |                   |                   | ageSeries/​imageC |     |
      |                   |                   | ollection/​Image[ |     |
      |                   |                   | sopInstanceUid/​@ |     |
      |                   |                   | root=​imageRefere |     |
      |                   |                   | nceUid/​@root]/​s |     |
      |                   |                   | opClassUid/​@root |     |
      +-------------------+-------------------+-------------------+-----+
      | Referenced SOP    | UI                | imageRe           | II  |
      | Sequence >        |                   | ferenceUid/​@root |     |
      | Referenced SOP    |                   |                   |     |
      | Instance UID      |                   |                   |     |
      +-------------------+-------------------+-------------------+-----+
      | Referenced SOP    | IS                | referencedFr      | INT |
      | Sequence >        |                   | ameNumber/​@value |     |
      | Referenced Frame  |                   |                   |     |
      | Number            |                   |                   |     |
      +-------------------+-------------------+-------------------+-----+

   An image reference in the AIM tree locally consists of the SOP
   Instance UID only, without SOP Class, which is described elsewhere in
   the tree in the imageReferenceEntityCollection (which, similar to the
   DICOM Current Requested Procedure Evidence Sequence or Pertinent
   Other Evidence Sequence, also contains the Study and Series level
   information). Hence the use of the predicate
   "sopInstanceUid/​@root=$sopInstanceUID" in the path in the table.

   The AIM version 4.2 model includes an optional AccessionNumber in the
   imageStudy class used in the imageReferenceEntityCollection. This may
   be preserved in a DICOM SR instance in the ImageLibrary.

   DICOM segmentation references may be mapped as specified in
   `table_title <#table_A.8-7>`__.

   .. table:: DICOM Segmentation references to AIM Path

      +-------------------+-------------------+-------------------+-----+
      | DICOM , and :     | AIM Path and ISO  |                   |     |
      | Image Reference   | 21090 Data Type   |                   |     |
      | (IMAGE) Value     |                   |                   |     |
      | Type              |                   |                   |     |
      +===================+===================+===================+=====+
      | Referenced SOP    | UI                | Segm              | II  |
      | Sequence >        |                   | entationEntity/​s |     |
      | Referenced SOP    |                   | opClassUid/​@root |     |
      | Class UID         |                   |                   |     |
      +-------------------+-------------------+-------------------+-----+
      | Referenced SOP    | UI                | ​Segment          | II  |
      | Sequence >        |                   | ationEntity/​sopI |     |
      | Referenced SOP    |                   | nstanceUid/​@root |     |
      | Instance UID      |                   |                   |     |
      +-------------------+-------------------+-------------------+-----+
      | Referenced SOP    | US                | Segment           | INT |
      | Sequence >        |                   | ationEntity/​segm |     |
      | Referenced        |                   | entNumber/​@value |     |
      | Segment Number    |                   |                   |     |
      +-------------------+-------------------+-------------------+-----+

   The SOP Class UID is included locally in the AIM tree with the
   reference, rather than being factored out into the
   imageReferenceEntityCollection, in which it is not present.

   Ideally, all segmentation references would be included in either
   Current Requested Procedure Evidence Sequence or Pertinent Other
   Evidence Sequence as appropriate. There is optional information in
   the AIM 4.2 model to identify the Study and Series, but if the Study
   and Series Instance UIDs are absent, they cannot be assumed to be
   those of any related images.

   The reference to the original image that was segmented or a
   representative image on which the segmentation may be displayed,
   which may be present in
   SegmentationEntity/​referencedSopInstanceUid/​@root, may be encoded
   in a separate Content Item if supported by the template (e.g., TID
   1410, TID 1411) in (121233, DCM, "Source image for segmentation").
