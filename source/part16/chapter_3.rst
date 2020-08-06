.. _chapter_3:

Definitions
===========

For the purposes of this Standard the following definitions apply.

Baseline Context Group Identifier
   Identifier that specifies the suggested Context Group for a Code
   Sequence Attribute.

   See .

Baseline Template Identifier
   Identifier that specifies a Template suggested to be used in the
   creation of a set of Content Items.

Coding Scheme
   Dictionary (lexicons) of concepts (terms) with assigned codes and
   well defined meanings.

   .. note::

      Examples of coding schemes include SNOMED and LOINC.

Context Group
   A set of coded concepts defined by a Mapping Resource forming a set
   appropriate to use in a particular context.

Context Group Version
   Version of a Context Group.

Context ID
   Identifier of a Context Group.

Defined Context Group Identifier
   Identifier that specifies the Context Group for a Code Sequence
   Attribute that shall be used.

   See .

Defined Template Identifier
   Identifier that specifies a Template that shall be used in the
   creation of a set of Content Items.

DICOM Content Mapping Resource
   A Mapping Resource that defines Templates and Context Groups for use
   in DICOM IODs.

Extensible Context Group
   Context Group that may be extended by a particular application by
   inclusion of additional concepts.

   See .

Extensible Template
   A Template that may be extended by a particular application by
   inclusion of additional Content Items beyond those specified in the
   Template.

Mapping Resource
   A resource that defines context-dependent usage constraints (i.e.,
   Value Set or Relationship Type restrictions) for Attributes. A
   resource that specifies the mapping of the content of an external
   controlled terminology to the components of a message standard.

Non-Extensible Context Group
   Context Group whose defined set of concepts shall not be extended by
   an application.

   See .

Non-Extensible Template
   A Template that specifies the exact set of Content Items and
   corresponding Value Sets that shall be used and that shall not be
   extended by an application.

Relationship Type
   The association between two Concepts. Examples: "HAS PROPERTIES",
   "CONTAINS", "INFERRED FROM".

Root Template
   A Template whose first content item is a CONTAINER content item
   intended to be encoded in the top level Data Set of a SOP Instance.
   I.e., the "root node" of the "content tree".

Template
   A pattern that describes the Content Items, Value Types, Relationship
   Types and Value Sets that may be used in part of a Structured Report
   content tree, or in other Content Item constructs, such as
   Acquisition Context or Protocol Context. Analogous to a Module of an
   Information Object Definition.

Template ID
   Identifier of a Template.

Value Set
   The allowed values of a Code Sequence Attribute in a given context.
   Specified either as one or more individual values or by reference to
   a Context Group.

Code Sequence Attribute
   .

Imaging Agent
   A substance administered to improve the imaging of specific organs,
   tissues, diseases and physiological functions. Adapted from Wikipedia
   http://en.wikipedia.org/wiki/Imaging_agent.

   .. note::

      1. Imaging agents include iodinated X-Ray and gadolinium-based MR
         contrast agents.

      2. Saline flush is not an imaging agent but may be administered in
         conjunction with imaging agents.

      3. Air used as a negative contrast agent is an imaging agent.

Service-Object Pair Class
   .

Service-Object Pair Instance
   .

Data Set
   .

Monitor Units
   A unit of radiation output used to quantify a Meterset. See .

