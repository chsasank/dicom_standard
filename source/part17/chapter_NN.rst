.. _chapter_NN:

Specimen Identification and Management
======================================

This annex explains the use of the Specimen Module for pathology or
laboratory specimen imaging.

.. _sect_NN.1:

Pathology Workflow
------------------

The concept of a specimen is deeply connected to analysis (lab)
workflow, the decisions made during analysis, and the "containers" used
within the workflow.

Typical anatomic pathology cases represent the analysis of (all) tissue
and/or non-biologic material (e.g., orthopedic hardware) removed in a
single collection procedure (e.g., surgical operation/event, biopsy,
scrape, aspiration etc.). A case is usually called an "Accession" and is
given a single accession number in the Laboratory Information System.

During an operation, the surgeon may label and send one or more discrete
collections of material (specimens) to pathology for analysis. By
sending discrete, labeled collections of tissue in separate containers,
the surgeon is requesting that each discrete labeled collection
(specimen) be analyzed and reported independently - as a separate "Part"
of the overall case. Therefore, each Part is an important, logical
component of the laboratory workflow. Within each Accession, each Part
is managed separately from the others and is identified uniquely in the
workflow and in the Laboratory Information System.

During the initial gross (or "eyeball") examination of a Part, the
pathologist may determine that some or all of the tissue in a Part
should be analyzed further (usually through histology). The pathologist
will place all or selected sub-samples of the material that makes up the
Part into labeled containers (cassettes). After some processing, all the
tissue in each cassette is embedded in a paraffin block (or epoxy resin
for electron microscopy); at the end of the process, the block is
physically attached to the cassette and has the same label. Therefore,
each "Block" is an important, logical component of the laboratory
workflow, which corresponds to physical material in a container for
handling, separating and identifying material managed in the workflow.
Within the workflow and Laboratory Information System, each Block is
identified uniquely and managed separately from all others.

From a Block, technicians can slice very thin sections. One or more of
these sections is placed on one or more slides. (Note, material from a
Part can also be placed directly on a slide bypassing the block). A
slide can be stained and then examined by the pathologists. Each
"Slide", therefore, is an important, logical component of the laboratory
workflow, which corresponds to physical material in a container for
handling, separating and identifying material managed in the workflow.
Within the workflow and within the Laboratory Information Systems, each
Slide is identified uniquely and managed separately from all others.

While "Parts" to "Blocks" to "Slides" is by far the most common workflow
in pathology, it is important to note that there can be numerous
variations on this basic theme. In particular, laser capture
microdissection and other slide sampling approaches for molecular
pathology are in increasing use. Such new workflows require a generic
approach in the Standard to identifying and managing specimen
identification and processing, not one limited only to "Parts",
"Blocks", and "Slides". Therefore, the Standard adopts a generic
approach of describing uniquely identified Specimens in Containers.

.. _sect_NN.2:

Basic Concepts and Definitions
------------------------------

.. _sect_NN.2.1:

Specimen
~~~~~~~~

A physical object (or a collection of objects) is a specimen when the
laboratory considers it a single discrete, uniquely identified unit that
is the subject of one or more steps in the laboratory (diagnostic)
workflow.

To say the same thing in a slightly different way: "Specimen" is defined
as a role played by a physical entity (one or more physical objects
considered as single unit) when the entity is identified uniquely by the
laboratory and is the direct subject of more steps in a laboratory
(diagnostic) workflow.

It is worthwhile to expand on this very basic, high level definition
because it contains implications that are important to the development
and implementation of the DICOM Specimen Module. In particular:

1. A single discrete physical object or a collection of several physical
   objects can act as a single specimen as long as the collection is
   considered a unit during the laboratory (diagnostic) process step
   involved. In other words, a specimen may include multiple physical
   pieces, as long as they are considered a single unit in the workflow.
   For example, when multiple fragments of tissue are placed in a
   cassette, most laboratories would consider that collection of
   fragments as one specimen (one "block").

2. A specimen must be identified. It must have an ID that identifies it
   as a unique subject in the laboratory workflow. An entity that does
   not have an identifier is not a specimen.

3. Specimens are sampled and processed during a laboratory's
   (diagnostic) workflow. Sampling can create new (child) specimens.
   These child specimens are full specimens in their own right (they
   have unique identifiers and are direct subjects in one or more steps
   in the laboratory's (diagnostic) workflow. This property of specimens
   (that can be created from existing specimens by sampling) extends a
   common definition of specimen, which limits the word to the original
   object received for examination (e.g., from surgery).

4. However, child specimens can and do carry some Attributes from
   ancestors. For example, a tissue section cut from a formalin fixed
   block remains formalin fixed, and a tissue section cut from a block
   dissected from the proximal margin of a colon resection is still made
   up of tissue from the proximal margin. A description of a specimen
   therefore, may require description of its parent specimens.

5. A specimen is defined by decisions in the laboratory workflow. For
   example, in a typical laboratory, multiple tissue sections cut from a
   single block and placed on the same slide are considered a single
   specimen (as single unit identified by the slide number). However, if
   the histotechnologists had placed each tissue section on its own
   slide (and given each slide a unique number), each tissue section
   would be a specimen in its own right .

.. _sect_NN.2.2:

Containers
~~~~~~~~~~

Specimen containers (or just "containers") play an important role in
laboratory (diagnostic) processes. In most, but not all, process steps,
specimens are held in containers, and a container often carries its
specimen's ID. Sometimes the container becomes intimately involved with
the specimen (e.g., a paraffin block), and in some situations (such as
examining tissue under the microscope) the container (the slide and
coverslip) become part of the optical path.

Containers have identifiers that are important in laboratory operations
and in some imaging processes (such as whole slide imaging). The DICOM
Specimen Module distinguishes the Container ID and the Specimen ID,
making them different data elements. In many laboratories where there is
one specimen per container, the value of the specimen ID and container
ID will be same. However, there are use cases in which there are more
than one specimen in a container. In those situations, the value of the
container ID and the specimen IDs will be different (see `Relationship
Between Specimens and Containers <#sect_NN.3.5>`__).

Containers are often made up of components. For example, a "slide" is
container that is made up of the glass slide, the coverslip and the
"glue" the binds them together. The Module allows each component to be
described in detail.

.. _sect_NN.3:

Specimen Module
---------------

.. _sect_NN.3.1:

Scope
~~~~~

The Specimen Module (see ) defines formal DICOM Attributes for the
identification and description of laboratory specimens when said
specimens are the subject of a DICOM image. The Module is focused on the
specimen and laboratory Attributes necessary to understand and interpret
the image. These include:

1. Attributes that identify (specify) the specimen (within a given
   institution and across institutions).

2. Attributes that identify and describe the container in which the
   specimen resides. Containers are intimately associated with specimens
   in laboratory processes, often "carry" a specimen's identity, and
   sometimes are intimately part of the imaging process, as when a glass
   slide and coverslip are in the optical path in microscope imaging.

3. Attributes that describe specimen collection, sampling and
   processing. Knowing how a specimen was collected, sampled, processed
   and stained is vital in interpreting an image of a specimen. One can
   make a strong case that those laboratory steps are part of the
   imaging process.

4. Attributes that describe the specimen or its ancestors (see
   `Specimen <#sect_NN.2.1>`__) when these descriptions help with the
   interpretation of the image.

Attributes that convey diagnostic opinions or interpretations are not
within the scope of the Specimen Module. The DICOM Specimen Module does
not seek to replace or mirror the pathologist's report.

.. _sect_NN.3.2:

Relationship With The Laboratory Information System
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

The Laboratory Information System (LIS) is critical to management of
workflow and processes in the pathology lab. It is ultimately the source
of the identifiers applied to specimens and containers, and is
responsible for recording the processes that were applied to specimens.

An important purpose of the Specimen Module is to store specimen
information necessary to understand and interpret an image within the
image information object, as images may be displayed in contexts where
the Laboratory Information System is not available. Implementation of
the Specimen Module therefore requires close, dynamic integration
between the LIS and imaging systems in the laboratory workflow.

It is expected that the Laboratory Information Systems will participate
in the population of the Specimen Module by passing the appropriate
information to a DICOM compliant imaging system in the Modality
Worklist, or by processing the image objects itself and populating the
Specimen Module Attributes.

The nature of the LIS processing for imaging in the workflow will vary
by product implementation. For example, an image of a gross specimen may
be taken before a gross description is transcribed. A LIS might provide
short term storage for images and update the description Attributes in
the module after a particular event (such as sign out). The DICOM
Standard is silent on such implementation issues, and only discusses the
Attributes defined for the information objects exchanged between
systems.

.. _sect_NN.3.3:

Case Level Information and The Accession Number
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

A pathology "case" is a unit of work resulting in a report with
associated codified, billable acts. Case Level Attributes are generally
outside the scope of the Specimen Module. However, a case is equivalent
to a DICOM Requested Procedure, for which Attributes are specified in
the DICOM Study level modules.

DICOM has existing methods to handle most "case level" issues, including
accepting cases referred for other institutions, clinical history,
status codes, etc. These methods are considered sufficient to support
DICOM imaging in Pathology.

The concept of an "Accession Number" in Pathology has been determined to
be sufficiently equivalent to an "Accession Number" in Radiology that
the DICOM data element "Accession Number" at the Study level at the
DICOM information model may be used for the Pathology Accession Number
with essentially the existing definition.

It is understood that the value of the laboratory accession number is
often incorporated as part of a Specimen ID. However, there is no
presumption that this is always true, and the Specimen ID should not be
parsed to determine an accession number. The accession number will
always be sent in its own discrete Attribute.

.. _sect_NN.3.4:

Laboratory Workflows and Specimen Types
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

While created with anatomic pathology in mind, the DICOM Specimen Module
is designed to support specimen identification, collection, sampling and
processing Attributes for a wide range of laboratory workflows. The
Module is designed in a general way so not to limit the nature, scope,
scale or complexity of laboratory (diagnostic) workflow that may
generate DICOM images.

To provide specificity on the general process, the Module provides
extendable lists of Container Types, Container Component Types, Specimen
Types, Specimen Collection Types, Specimen Process Types and Staining
Types. It is expected that the value sets for these "types" can be
specialized to describe a wide range of laboratory procedures.

In typical anatomic pathology practice, and in Laboratory Information
Systems, there are conventionally three identified levels of specimen
preparation - part, block, and slide. These terms are actually
conflations of the concepts of specimen and container. Not all
processing can be described by only these three levels.

A part is the uniquely identified tissue or material collected from the
patient and delivered to the pathology department for examination.
Examples of parts would include a lung resection, colon biopsy at 20 cm,
colon biopsy at 30 cm, peripheral blood sample, cervical cells obtained
via scraping or brush, etc. A part can be delivered in a wide range of
containers, usually labeled with the patients name, medical record
number, and a short description of the specimen such as "colon biopsy at
20 cm". At accession, the lab creates a part identifier and writes it on
the container. The container therefore conveys the part's identifier in
the lab.

A block is a uniquely identified container, typically a cassette,
containing one or more pieces of tissue dissected from the part (tissue
dice). The tissue pieces may be considered, by some laboratories, as
separate specimens. However in most labs, all the tissue pieces in a
block are considered a single specimen.

A slide is a uniquely identified container, typically a glass microscope
slide, containing tissue or other material. Common slide preparations
include:

-  "Tissue sections" created from tissue embedded in blocks. (1 slide
   typically contains one or more tissue sections coming from one block)

-  "Touch preps" prepared by placing a slide into contact with
   unprocessed tissue.

-  "Liquid preparations" are a thin layer of cells created from a
   suspension.

.. _sect_NN.3.5:

Relationship Between Specimens and Containers
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

Virtually all specimens in a clinical laboratory are associated with a
container, and specimens and containers are both important in imaging
(see "Definitions", above). In most clinical laboratory situations there
is a one to one relationship between specimens and containers. In fact,
pathologists and LIS systems routinely consider a specimen and its
container as single entity; e.g., the slide (a container) and the tissue
sections (the specimen) are considered a single unit.

However, there are legitimate use cases in which a laboratory may place
two or more specimens in the same container (see `Specimen
Identification Examples <#sect_NN.4>`__ for examples). Therefore, the
DICOM Specimen Module distinguishes between a Specimen ID and a
Container ID. However, in situations where there is only one specimen
per container, the value of the Specimen ID and Container ID may be the
same (as assigned by the LIS).

Some Laboratory Information System may, in fact, not support multiple
specimens in a container, i.e., they manage only a single identifier
used for the combination of specimen and container. This is not contrary
to the DICOM Standard; images produced under such a system will simply
always assert that there is only one specimen in each container.
However, a pathology image display application that shows images from a
variety of sources must be able to distinguish between container and
specimen IDs, and handle the 1:N relationship.

In allowing for one container to have multiple specimens, the Specimen
Module asserts that it is the Container, not the Specimen, that is the
unique target of the image. In other words, one Container ID is required
in the Specimen Module, and multiple Specimen IDs are allowed in the
Specimen Sequence. See `figure_title <#figure_NN.3-1>`__.

If there is more than one specimen in a container, there must be a
mechanism to identify and locate each specimen. When there is more than
one specimen in a container, the Module allows various approaches to
specify their locations. The Specimen Localization Content Item Sequence
(0040,0620), through its associated , allows the specimen to be
localized by a distance in three dimensions from a reference point on
the container, by a textual description of a location or physical
Attribute such as a colored ink, or by its location as shown in a
referenced image of the container. The referenced image may use an
overlay, burned-in annotation, or an associated Presentation State SOP
Instance to specify the location of the specimen.

.. _sect_NN.3.6:

Relationship Between Specimens and Images
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

Because the Module supports one container with multiple specimens, the
Module can be used with an image of:

-  A single specimen associated with a container

-  One or more specimens out of several in the same container

-  All specimens in the same container

However the Module is not designed for use with an image of:

-  Multiple specimens that are not associated with the same container,
   e.g., two gross specimens (two Parts) on a photography table, each
   with a little plastic label with their specimen number.

-  Multiple containers that hold specimens (e.g., eight cassettes
   containing breast tissue being X-Rayed for calcium).

Such images may be included in the Study, but would not use the Specimen
Module; they would, for instance, be general Visible Light Photographic
images. Note, however, that the LIS might identify a "virtual container"
that contains such multiple real containers, and manage that virtual
container in the laboratory workflow.

.. _sect_NN.4:

Specimen Identification Examples
--------------------------------

.. _sect_NN.4.1:

One Specimen Per Container
~~~~~~~~~~~~~~~~~~~~~~~~~~

In normal clinical practice, when there is one specimen per container,
the value of the specimen identifier and the value of the container
identifier will be the same. In `figure_title <#figure_NN.4-1>`__, each
slide is prepared from a single tissue sample from a single block
(cassette).

.. _sect_NN.4.2:

Multiple Items From Same Block
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

`figure_title <#figure_NN.4-2>`__ shows more than one tissue item on the
same slide coming from the same block (but cut from different levels).
The laboratory information system considers two tissue sections (on the
same slide) to be separate specimens.

Two Specimen IDs will be assigned, different from the Container (Slide)
ID. The specimens may be localized, for example, by descriptive text
"Left" and "Right".

If the slide is imaged, a single image with more than one specimen may
be created. In this case, both specimens must be identified in the
Specimen Sequence of the Specimen Module. If only one specimen is
imaged, only its Specimen ID must be included in the Specimen Sequence;
however, both IDs may be included (e.g., if the image acquisition system
cannot determine which specimens in/on the container are in the field of
view).

.. _sect_NN.4.3:

Items From Different Parts in The Same Block
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

`figure_title <#figure_NN.4-3>`__ shows processing where more than one
tissue item is embedded in the same block within the same Cassette, but
coming from different clinical specimens (parts). This may represent
different lymph nodes embedded into one cassette, or different tissue
dice coming from different parts in a frozen section examination, or
tissue from the proximal margin and from the distal margin, and both
were placed in the same cassette. Because the laboratory wanted to
maintain the sample as separate specimens (to maintain their identity),
the LIS gave them different IDs and the tissue from Part A was inked
blue and the tissue from Part B was inked red.

The specimen IDs must be different from each other and from the
container (cassette) ID. The specimens may be localized, for example, by
descriptive text "Red" and "Blue" for Visual Coding of Specimen.

If a section is made from the block, each tissue section will include
fragments from two specimens (red and blue). The slide (container) ID
will be different from the section id (which will be different form each
other).

If the slide is imaged, a single image with more than one specimen may
be created but the different specimens must be identified and
unambiguously localized within the container.

.. _sect_NN.4.4:

Items From Different Parts On The Same Slide
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

`figure_title <#figure_NN.4-4>`__ shows the result of two tissue
collections placed on the same slide by the surgeon. E.g., in
gynecological smears the different directions of smears might represent
different parts (portio, cervix).

The specimen IDs must be different from each other and from the
container (slide) ID. The specimens may be localized, for example, by
descriptive text "Short direction smear" and "Long direction smear".

.. _sect_NN.4.5:

Tissue Micro Array
~~~~~~~~~~~~~~~~~~

Slides created from a TMA block have small fragments of many different
tissues coming from different patients, all of which may be processed at
the same time, under the same conditions by a desired technique. These
are typically utilized in research. See
`figure_title <#figure_NN.4-5>`__. Tissue items (spots) on the TMA slide
come from different tissue items (cores) in TMA blocks (from different
donor blocks, different parts and different patients).

Each Specimen (spot) must have its own ID. The specimens may be
localized, for example, by X-Y coordinates, or by a textual column-row
identifier for the spot (e.g., "E3" for fifth column, third row).

If the TMA slide is imaged as a whole, e.g., at low resolution as an
index, it must be given a "pseudo-patient" identifier (since it does not
relate to a single patient). Images created for each spot should be
assigned to the real patients.

.. _sect_NN.5:

Structure of The Specimen Module
--------------------------------

The Specimen Module content is specified as a Macro as an editorial
convention to facilitate its use in both Composite IODs and in the
Modality Worklist Information Model.

The Module has two main sections. The first deals with the specimen
container. The second deals with the specimens within that container.
Because more than one specimen may reside in single container, the
specimen section is set up as a sequence.

The Container section is divided two "sub-sections":

-  One deals with the Specimen Container ID and the Container Type. Note
   that the "Container Identifier" is a required field.

-  One deals with Container Components. Because there may be more than
   one component, this section is set up as a sequence.

The Specimen Description Sequence contains five "sub-sections"

-  One deals with the Specimen ID

-  One deals with descriptions of the specimen

-  One deals with preparation of the specimen and its ancestor specimens
   (including sampling, processing and staining). Because of its
   importance in interpreting slide images, staining is distinguished
   from other processing. Specimen preparation is set up as sequence of
   process steps (multiple steps are possible); each step is in turn a
   sequence of content items (Attributes using coded vocabularies). This
   is the most complex part of the module.

-  One deals with the original anatomic location of the specimen in the
   patient.

-  One deals with specimen localization within a container. This is used
   to identify specimens when there is more than one in a container. It
   is set up as sequence.

.. _sect_NN.6:

Examples of Specimen Module Use
-------------------------------

This section includes examples of the use of the Specimen Module. Each
example has two tables.

The first table contains the majority of the container and specimen
elements of the Specimen Module. The second includes the Specimen
Preparation Sequence (which documents the sampling, processing and
staining steps).

In the first table, invocations of Macros have been expanded to their
constituent Attributes. The Table does not include Type 3 (optional)
Attributes that are not used for the example case.

The second table shows the Items of the Specimen Preparation Sequence
and its subsidiary Specimen Preparation Step Content Item Sequence. That
latter sequence itself has subsidiary Code Sequence Items, but these are
shown in the canonical DICOM "triplet" format (see ), e.g., `(44714003,
SCT, "Left Upper Lobe of Lung") <http://snomed.info/id/44714003>`__. In
the table, inclusions of subsidiary templates have been expanded to
their constituent Content Items. The Table does not include Type U
(optional) Content Items that are not used for the example case.

Values in the colored columns of the two tables actually appear in the
image object.

.. _sect_NN.6.1:

Gross Specimen
~~~~~~~~~~~~~~

This is an example of how the Specimen Module can be populated for a
gross specimen (a lung lobe resection received from surgery). The
associated image would be a gross image taken in gross room.

.. table:: Specimen Module for Gross Specimen

   +-------------+-------------+-------------+-------------+-------------+
   | **Attribute | **Tag**     | **Attribute | **Example   | *           |
   | Name**      |             | De          | Value**     | *Comments** |
   |             |             | scription** |             |             |
   +=============+=============+=============+=============+=============+
   | Container   | (0040,0512) | The         | S07-100 A   | Note that   |
   | Identifier  |             | identifier  |             | the         |
   |             |             | for the     |             | container   |
   |             |             | container   |             | ID is       |
   |             |             | that        |             | required,   |
   |             |             | contains    |             | even though |
   |             |             | the         |             | the         |
   |             |             | specimen(s) |             | container   |
   |             |             | being       |             | itself does |
   |             |             | imaged.     |             | not figure  |
   |             |             |             |             | in the      |
   |             |             |             |             | image.      |
   +-------------+-------------+-------------+-------------+-------------+
   | Issuer of   | (0040,0513) | O           |             |             |
   | the         |             | rganization |             |             |
   | Container   |             | that        |             |             |
   | Identifier  |             | assigned    |             |             |
   | Sequence    |             | the         |             |             |
   |             |             | Container   |             |             |
   |             |             | Identifier  |             |             |
   +-------------+-------------+-------------+-------------+-------------+
   | >Local      | (0040,0031) | Identifies  | Case        |             |
   | Namespace   |             | an entity   | Medical     |             |
   | Entity ID   |             | within the  | Center      |             |
   |             |             | local       |             |             |
   |             |             | namespace   |             |             |
   |             |             | or domain.  |             |             |
   +-------------+-------------+-------------+-------------+-------------+
   | Container   | (0040,0518) | Type of     |             | This would  |
   | Type Code   |             | container   |             | likely be a |
   | Sequence    |             | that        |             | default     |
   |             |             | contains    |             | container   |
   |             |             | the         |             | value for   |
   |             |             | specimen(s) |             | all gross   |
   |             |             | being       |             | specimens.  |
   |             |             | imaged.     |             | The LIS     |
   |             |             | Zero or one |             | does not    |
   |             |             | items shall |             | keep        |
   |             |             | be          |             | information |
   |             |             | permitted   |             | on the      |
   |             |             | in this     |             | gross       |
   |             |             | sequence    |             | container   |
   |             |             |             |             | type, so    |
   |             |             |             |             | this is an  |
   |             |             |             |             | empty       |
   |             |             |             |             | sequence.   |
   +-------------+-------------+-------------+-------------+-------------+
   | Specimen    | (0040,0560) | Sequence of |             |             |
   | Description |             | identifiers |             |             |
   | Sequence    |             | and         |             |             |
   |             |             | detailed    |             |             |
   |             |             | description |             |             |
   |             |             | of the      |             |             |
   |             |             | specimen(s) |             |             |
   |             |             | being       |             |             |
   |             |             | imaged. One |             |             |
   |             |             | or more     |             |             |
   |             |             | Items shall |             |             |
   |             |             | be included |             |             |
   |             |             | in this     |             |             |
   |             |             | Sequence.   |             |             |
   +-------------+-------------+-------------+-------------+-------------+
   | >Specimen   | (0040,0551) | A           | S07-100 A   | Specimen    |
   | Identifier  |             | d           |             | and         |
   |             |             | epartmental |             | Container   |
   |             |             | information |             | have same   |
   |             |             | system      |             | ID          |
   |             |             | identifier  |             |             |
   |             |             | for the     |             |             |
   |             |             | Specimen.   |             |             |
   +-------------+-------------+-------------+-------------+-------------+
   | >Issuer of  | (0040,0562) | The name or |             |             |
   | the         |             | code for    |             |             |
   | Specimen    |             | the         |             |             |
   | Identifier  |             | institution |             |             |
   | Sequence    |             | that has    |             |             |
   |             |             | assigned    |             |             |
   |             |             | the         |             |             |
   |             |             | Specimen    |             |             |
   |             |             | Identifier. |             |             |
   +-------------+-------------+-------------+-------------+-------------+
   | >> Local    | (0040,0031) | Identifies  | Case        |             |
   | Namespace   |             | an entity   | Medical     |             |
   | Entity ID   |             | within the  | Center      |             |
   |             |             | local       |             |             |
   |             |             | namespace   |             |             |
   |             |             | or domain.  |             |             |
   +-------------+-------------+-------------+-------------+-------------+
   | >Specimen   | (0040,0554) | Unique      | 1           |             |
   | UID         |             | Identifier  | .2.840.9979 |             |
   |             |             | for         | 0.986.33.16 |             |
   |             |             | Specimen    | 77.1.1.17.1 |             |
   +-------------+-------------+-------------+-------------+-------------+
   | >Specimen   | (0040,0600) | Short       | Part A:     | The LIS     |
   | Short       |             | textual     | LEFT UPPER  | "Specimen   |
   | Description |             | specimen    | LOBE        | Received"   |
   |             |             | description |             | field is    |
   |             |             |             |             | mapped to   |
   |             |             |             |             | this DICOM  |
   |             |             |             |             | field       |
   +-------------+-------------+-------------+-------------+-------------+
   | >Specimen   | (0040,0602) | Detailed    | A: Received | This is a   |
   | Detailed    |             | textual     | fresh for   | mapping     |
   | Description |             | specimen    | int         | from the    |
   |             |             | description | raoperative | LIS "Gross  |
   |             |             |             | co          | D           |
   |             |             |             | nsultation, | escription" |
   |             |             |             | labeled     | field. Note |
   |             |             |             | with the    | that in     |
   |             |             |             | patient's   | Case        |
   |             |             |             | name,       | S07-100     |
   |             |             |             | number and  | there were  |
   |             |             |             | "left upper | six parts.  |
   |             |             |             | lobe," is a | This means  |
   |             |             |             | pink-tan,   | the LIS     |
   |             |             |             | w           | gross       |
   |             |             |             | edge-shaped | description |
   |             |             |             | segment of  | field will  |
   |             |             |             | soft        | have six    |
   |             |             |             | tissue, 6.9 | sections (A |
   |             |             |             | x 4.2 x 1.0 | - F). We    |
   |             |             |             | cm. The     | would have  |
   |             |             |             | pleural     | to parse    |
   |             |             |             | surface is  | the gross   |
   |             |             |             | pink-tan    | description |
   |             |             |             | and         | field into  |
   |             |             |             | glistening  | those parts |
   |             |             |             | with a      | (A-F) and   |
   |             |             |             | stapled     | then only   |
   |             |             |             | line        | incorporate |
   |             |             |             | measuring   | section "A" |
   |             |             |             | 12.0 cm. in | into this   |
   |             |             |             | length. The | Attribute.  |
   |             |             |             | pleural     | NOTE: One   |
   |             |             |             | surface     | could       |
   |             |             |             | shows a 0.5 | consider    |
   |             |             |             | cm. area of | listing all |
   |             |             |             | puckering.  | the Blocks  |
   |             |             |             | The pleural | associated  |
   |             |             |             | surface is  | with Part   |
   |             |             |             | inked       | A. It would |
   |             |             |             | black. The  | be easy to  |
   |             |             |             | cut surface | do and      |
   |             |             |             | reveals a   | might give  |
   |             |             |             | 1.2 x 1.1   | useful      |
   |             |             |             | cm,         | i           |
   |             |             |             | white-gray, | nformation. |
   |             |             |             | irregular   |             |
   |             |             |             | mass        |             |
   |             |             |             | abutting    |             |
   |             |             |             | the pleural |             |
   |             |             |             | surface and |             |
   |             |             |             | deep to the |             |
   |             |             |             | puckered    |             |
   |             |             |             | area. The   |             |
   |             |             |             | remainder   |             |
   |             |             |             | of the cut  |             |
   |             |             |             | surface is  |             |
   |             |             |             | red-brown   |             |
   |             |             |             | and         |             |
   |             |             |             | congested.  |             |
   |             |             |             | No other    |             |
   |             |             |             | lesions are |             |
   |             |             |             | identified. |             |
   |             |             |             | Rep         |             |
   |             |             |             | resentative |             |
   |             |             |             | sections    |             |
   |             |             |             | are         |             |
   |             |             |             | submitted.  |             |
   +-------------+-------------+-------------+-------------+-------------+
   | >Specimen   | (0040,0610) | Sequence of | (see        |             |
   | Preparation |             | Items       | `table_tit  |             |
   | Sequence    |             | identifying | le <#table_ |             |
   |             |             | the process | NN.6-2>`__) |             |
   |             |             | steps used  |             |             |
   |             |             | to prepare  |             |             |
   |             |             | the         |             |             |
   |             |             | specimen    |             |             |
   |             |             | for image   |             |             |
   |             |             | a           |             |             |
   |             |             | cquisition. |             |             |
   |             |             | One or more |             |             |
   |             |             | Items may   |             |             |
   |             |             | be present. |             |             |
   |             |             | This        |             |             |
   |             |             | Sequence    |             |             |
   |             |             | includes    |             |             |
   |             |             | description |             |             |
   |             |             | of the      |             |             |
   |             |             | specimen    |             |             |
   |             |             | sampling    |             |             |
   |             |             | step from a |             |             |
   |             |             | parent      |             |             |
   |             |             | specimen,   |             |             |
   |             |             | potentially |             |             |
   |             |             | back to the |             |             |
   |             |             | original    |             |             |
   |             |             | part        |             |             |
   |             |             | collection. |             |             |
   +-------------+-------------+-------------+-------------+-------------+
   | >>Specimen  | (0040,0612) | Sequence of |             |             |
   | Preparation |             | Content     |             |             |
   | Step        |             | Items       |             |             |
   | Content     |             | identifying |             |             |
   | Item        |             | the         |             |             |
   | Sequence    |             | processes   |             |             |
   |             |             | used in one |             |             |
   |             |             | preparation |             |             |
   |             |             | step to     |             |             |
   |             |             | prepare the |             |             |
   |             |             | specimen    |             |             |
   |             |             | for image   |             |             |
   |             |             | a           |             |             |
   |             |             | cquisition. |             |             |
   |             |             | One or more |             |             |
   |             |             | Items may   |             |             |
   |             |             | be present. |             |             |
   +-------------+-------------+-------------+-------------+-------------+
   | >Primary    | (0008,2228) | Original    |             |             |
   | Anatomic    |             | anatomic    |             |             |
   | Structure   |             | location in |             |             |
   | Sequence    |             | patient of  |             |             |
   |             |             | specimen.   |             |             |
   |             |             | This        |             |             |
   |             |             | location    |             |             |
   |             |             | may be      |             |             |
   |             |             | inherited   |             |             |
   |             |             | from the    |             |             |
   |             |             | parent      |             |             |
   |             |             | specimen,   |             |             |
   |             |             | or further  |             |             |
   |             |             | refined by  |             |             |
   |             |             | modifiers   |             |             |
   |             |             | depending   |             |             |
   |             |             | on the      |             |             |
   |             |             | sampling    |             |             |
   |             |             | procedure   |             |             |
   |             |             | for this    |             |             |
   |             |             | specimen.   |             |             |
   +-------------+-------------+-------------+-------------+-------------+
   | >>Code      | (0008,0100) |             | 44714003    | This is a   |
   | Value       |             |             |             | code        |
   |             |             |             |             | sequence    |
   |             |             |             |             | item        |
   +-------------+-------------+-------------+-------------+-------------+
   | >>Coding    | (0008,0102) |             | SCT         |             |
   | Scheme      |             |             |             |             |
   | Designator  |             |             |             |             |
   +-------------+-------------+-------------+-------------+-------------+
   | >>Code      | (0008,0104) |             | Left Upper  |             |
   | Meaning     |             |             | Lobe of     |             |
   |             |             |             | Lung        |             |
   +-------------+-------------+-------------+-------------+-------------+

.. table:: Specimen Preparation Sequence for Gross Specimen

   +---------+---------+---------+---------+---------+---------+---------+
   | **S     | **S     | **T     | **Value | **      | **      | **Com   |
   | pecimen | pecimen | emplate | Type    | Concept | Example | ments** |
   | Prep    | Prep.   | / Row** | (0040,  | Name    | Value** |         |
   | aration | Step    |         | A040)** | Code    |         |         |
   | S       | Content |         |         | S       |         |         |
   | equence | Item    |         |         | equence |         |         |
   | - Item  | S       |         |         | (0040,  |         |         |
   | #**     | equence |         |         | A043)** |         |         |
   |         | - Item  |         |         |         |         |         |
   |         | #**     |         |         |         |         |         |
   +=========+=========+=========+=========+=========+=========+=========+
   | 1       | 1       | 8001 /  | TEXT    | (       | S07-100 | Col     |
   |         |         | 1       |         | 121041, | A       | lection |
   |         |         |         |         | DCM,    |         | in OR   |
   |         |         |         |         | "S      |         |         |
   |         |         |         |         | pecimen |         |         |
   |         |         |         |         | Ident   |         |         |
   |         |         |         |         | ifier") |         |         |
   +---------+---------+---------+---------+---------+---------+---------+
   | 2       | 8001 /  | TEXT    | (       | Case    |         |         |
   |         | 2       |         | 111724, | Medical |         |         |
   |         |         |         | DCM,    | Center  |         |         |
   |         |         |         | "Issuer |         |         |         |
   |         |         |         | of      |         |         |         |
   |         |         |         | S       |         |         |         |
   |         |         |         | pecimen |         |         |         |
   |         |         |         | Ident   |         |         |         |
   |         |         |         | ifier") |         |         |         |
   +---------+---------+---------+---------+---------+---------+---------+
   | 1       | 8001 /  | CODE    | (       | `(17    |         |         |
   |         | 3       |         | 111701, | 636008, |         |         |
   |         |         |         | DCM,    | SCT,    |         |         |
   |         |         |         | "Pro    | "S      |         |         |
   |         |         |         | cessing | pecimen |         |         |
   |         |         |         | type")  | collec  |         |         |
   |         |         |         |         | tion")  |         |         |
   |         |         |         |         | <http:/ |         |         |
   |         |         |         |         | /snomed |         |         |
   |         |         |         |         | .info/i |         |         |
   |         |         |         |         | d/17636 |         |         |
   |         |         |         |         | 008>`__ |         |         |
   +---------+---------+---------+---------+---------+---------+---------+
   | 2       | 8001 /  | D       | (       | 20070   |         |         |
   |         | 4       | ATETIME | 111702, | 3230827 |         |         |
   |         |         |         | DCM,    |         |         |         |
   |         |         |         | "D      |         |         |         |
   |         |         |         | ateTime |         |         |         |
   |         |         |         | of      |         |         |         |
   |         |         |         | proce   |         |         |         |
   |         |         |         | ssing") |         |         |         |
   +---------+---------+---------+---------+---------+---------+---------+
   | 3       | 8001 /  | TEXT    | (       | Taken   |         |         |
   |         | 5       |         | 111703, |         |         |         |
   |         |         |         | DCM,    |         |         |         |
   |         |         |         | "Pro    |         |         |         |
   |         |         |         | cessing |         |         |         |
   |         |         |         | step    |         |         |         |
   |         |         |         | descri  |         |         |         |
   |         |         |         | ption") |         |         |         |
   +---------+---------+---------+---------+---------+---------+---------+
   | 4       | 8001 /  | CODE    | (       | `(65    |         |         |
   |         | 8       |         | 111704, | 801008, |         |         |
   |         |         |         | DCM,    | SCT,    |         |         |
   |         | 8002 /  |         | "S      | "Exci   |         |         |
   |         | 1       |         | ampling | sion")  |         |         |
   |         |         |         | M       | <http:/ |         |         |
   |         |         |         | ethod") | /snomed |         |         |
   |         |         |         |         | .info/i |         |         |
   |         |         |         |         | d/65801 |         |         |
   |         |         |         |         | 008>`__ |         |         |
   +---------+---------+---------+---------+---------+---------+---------+
   | 2       | 1       | 8001 /  | TEXT    | (       | S07-100 | S       |
   |         |         | 1       |         | 121041, | A       | pecimen |
   |         |         |         |         | DCM,    |         | r       |
   |         |         |         |         | "S      |         | eceived |
   |         |         |         |         | pecimen |         | in      |
   |         |         |         |         | Ident   |         | Pa      |
   |         |         |         |         | ifier") |         | thology |
   |         |         |         |         |         |         | dep     |
   |         |         |         |         |         |         | artment |
   +---------+---------+---------+---------+---------+---------+---------+
   | 2       | 8001 /  | TEXT    | (       | Case    |         |         |
   |         | 2       |         | 111724, | Medical |         |         |
   |         |         |         | DCM,    | Center  |         |         |
   |         |         |         | "Issuer |         |         |         |
   |         |         |         | of      |         |         |         |
   |         |         |         | S       |         |         |         |
   |         |         |         | pecimen |         |         |         |
   |         |         |         | Ident   |         |         |         |
   |         |         |         | ifier") |         |         |         |
   +---------+---------+---------+---------+---------+---------+---------+
   | 1       | 8001 /  | CODE    | (       | `(428   |         |         |
   |         | 3       |         | 111701, | 995007, |         |         |
   |         |         |         | DCM,    | SCT,    |         |         |
   |         |         |         | "Pro    | "S      |         |         |
   |         |         |         | cessing | pecimen |         |         |
   |         |         |         | type")  | Receiv  |         |         |
   |         |         |         |         | ing") < |         |         |
   |         |         |         |         | http:// |         |         |
   |         |         |         |         | snomed. |         |         |
   |         |         |         |         | info/id |         |         |
   |         |         |         |         | /428995 |         |         |
   |         |         |         |         | 007>`__ |         |         |
   +---------+---------+---------+---------+---------+---------+---------+
   | 2       | 8001 /  | D       | (       | 20070   |         |         |
   |         | 4       | ATETIME | 111702, | 3230943 |         |         |
   |         |         |         | DCM,    |         |         |         |
   |         |         |         | "D      |         |         |         |
   |         |         |         | ateTime |         |         |         |
   |         |         |         | of      |         |         |         |
   |         |         |         | proce   |         |         |         |
   |         |         |         | ssing") |         |         |         |
   +---------+---------+---------+---------+---------+---------+---------+

.. _sect_NN.6.2:

Slide
~~~~~

This is an example of how the Specimen Module can be populated for a
slide (from a lung lobe resection received from surgery). The associated
image would be a whole slide image.

.. table:: Specimen Module for a Slide

   +-------------+-------------+-------------+-------------+-------------+
   | **Attribute | **Tag**     | **Attribute | **Example   | *           |
   | Name**      |             | De          | Value**     | *Comments** |
   |             |             | scription** |             |             |
   +=============+=============+=============+=============+=============+
   | Container   | (0040,0512) | The         | S07-100 A 5 |             |
   | Identifier  |             | identifier  | 1           |             |
   |             |             | for the     |             |             |
   |             |             | container   |             |             |
   |             |             | that        |             |             |
   |             |             | contains    |             |             |
   |             |             | the         |             |             |
   |             |             | specimen(s) |             |             |
   |             |             | being       |             |             |
   |             |             | imaged.     |             |             |
   +-------------+-------------+-------------+-------------+-------------+
   | Issuer of   | (0040,0513) | O           |             |             |
   | the         |             | rganization |             |             |
   | Container   |             | that        |             |             |
   | Identifier  |             | assigned    |             |             |
   | Sequence    |             | the         |             |             |
   |             |             | Container   |             |             |
   |             |             | Identifier  |             |             |
   +-------------+-------------+-------------+-------------+-------------+
   | >Local      | (0040,0031) | Identifies  | Case        |             |
   | Namespace   |             | an entity   | Medical     |             |
   | Entity ID   |             | within the  | Center      |             |
   |             |             | local       |             |             |
   |             |             | namespace   |             |             |
   |             |             | or domain.  |             |             |
   +-------------+-------------+-------------+-------------+-------------+
   | Container   | (0040,0518) | Type of     |             | This would  |
   | Type Code   |             | container   |             | likely be a |
   | Sequence    |             | that        |             | default     |
   |             |             | contains    |             | container   |
   |             |             | the         |             | value for   |
   |             |             | specimen(s) |             | all slide   |
   |             |             | being       |             | specimens.  |
   |             |             | imaged.     |             |             |
   |             |             | Only a      |             |             |
   |             |             | single item |             |             |
   |             |             | shall be    |             |             |
   |             |             | permitted   |             |             |
   |             |             | in this     |             |             |
   |             |             | sequence    |             |             |
   +-------------+-------------+-------------+-------------+-------------+
   | >Code Value | (0008,0100) |             | 258661006   | This is a   |
   |             |             |             |             | code        |
   |             |             |             |             | sequence    |
   |             |             |             |             | item        |
   +-------------+-------------+-------------+-------------+-------------+
   | >Coding     | (0008,0102) |             | SCT         |             |
   | Scheme      |             |             |             |             |
   | Designator  |             |             |             |             |
   +-------------+-------------+-------------+-------------+-------------+
   | >Code       | (0008,0104) |             | Slide       |             |
   | Meaning     |             |             |             |             |
   +-------------+-------------+-------------+-------------+-------------+
   | Container   | (0040,0520) | Description |             |             |
   | Component   |             | of one or   |             |             |
   | Sequence    |             | more        |             |             |
   |             |             | components  |             |             |
   |             |             | of the      |             |             |
   |             |             | container   |             |             |
   |             |             | (e.g.,      |             |             |
   |             |             | description |             |             |
   |             |             | of the      |             |             |
   |             |             | slide and   |             |             |
   |             |             | of the      |             |             |
   |             |             | coverslip). |             |             |
   |             |             | One or more |             |             |
   |             |             | Items may   |             |             |
   |             |             | be included |             |             |
   |             |             | in this     |             |             |
   |             |             | Sequence.   |             |             |
   +-------------+-------------+-------------+-------------+-------------+
   | >Container  | (0050,0012) | Type of     |             |             |
   | Component   |             | container   |             |             |
   | Type Code   |             | component.  |             |             |
   | Sequence    |             | One Item    |             |             |
   |             |             | shall be    |             |             |
   |             |             | included in |             |             |
   |             |             | this        |             |             |
   |             |             | Sequence.   |             |             |
   +-------------+-------------+-------------+-------------+-------------+
   | >>Code      | (0008,0100) |             | 433472003   | This is a   |
   | Value       |             |             |             | code        |
   |             |             |             |             | sequence    |
   |             |             |             |             | item        |
   +-------------+-------------+-------------+-------------+-------------+
   | >>Coding    | (0008,0102) |             | SCT         |             |
   | Scheme      |             |             |             |             |
   | Designator  |             |             |             |             |
   +-------------+-------------+-------------+-------------+-------------+
   | >>Code      | (0008,0104) |             | Microscope  |             |
   | Meaning     |             |             | slide       |             |
   |             |             |             | coverslip   |             |
   +-------------+-------------+-------------+-------------+-------------+
   | >Container  | (0050,001A) | Material of | GLASS       |             |
   | Component   |             | container   |             |             |
   | Material    |             | component.  |             |             |
   +-------------+-------------+-------------+-------------+-------------+
   | Specimen    | (0040,0560) | Sequence of |             |             |
   | Description |             | identifiers |             |             |
   | Sequence    |             | and         |             |             |
   |             |             | detailed    |             |             |
   |             |             | description |             |             |
   |             |             | of the      |             |             |
   |             |             | specimen(s) |             |             |
   |             |             | being       |             |             |
   |             |             | imaged. One |             |             |
   |             |             | or more     |             |             |
   |             |             | Items shall |             |             |
   |             |             | be included |             |             |
   |             |             | in this     |             |             |
   |             |             | Sequence.   |             |             |
   +-------------+-------------+-------------+-------------+-------------+
   | >Specimen   | (0040,0551) | A           | S07-100 A 5 | Specimen    |
   | Identifier  |             | d           | 1           | and         |
   |             |             | epartmental |             | Container   |
   |             |             | information |             | have same   |
   |             |             | system      |             | ID          |
   |             |             | identifier  |             |             |
   |             |             | for the     |             |             |
   |             |             | Specimen.   |             |             |
   +-------------+-------------+-------------+-------------+-------------+
   | >Issuer of  | (0040,0562) | The name or |             |             |
   | the         |             | code for    |             |             |
   | Specimen    |             | the         |             |             |
   | Identifier  |             | institution |             |             |
   | Sequence    |             | that has    |             |             |
   |             |             | assigned    |             |             |
   |             |             | the         |             |             |
   |             |             | Specimen    |             |             |
   |             |             | Identifier. |             |             |
   +-------------+-------------+-------------+-------------+-------------+
   | >>Local     | (0040,0031) | Identifies  | Case        |             |
   | Namespace   |             | an entity   | Medical     |             |
   | Entity ID   |             | within the  | Center      |             |
   |             |             | local       |             |             |
   |             |             | namespace   |             |             |
   |             |             | or domain.  |             |             |
   +-------------+-------------+-------------+-------------+-------------+
   | >Specimen   | (0040,0554) | Unique      | 1           |             |
   | UID         |             | Identifier  | .2.840.9979 |             |
   |             |             | for         | 0.986.33.16 |             |
   |             |             | Specimen    | 77.1.1.19.5 |             |
   +-------------+-------------+-------------+-------------+-------------+
   | >Specimen   | (0040,0600) | Short       | Part A:     | This        |
   | Short       |             | textual     | LEFT UPPER  | Attribute   |
   | Description |             | specimen    | LOBE, Block | c           |
   |             |             | description | 5: Mass (2  | oncatenates |
   |             |             |             | pc), Slide  | four LIS    |
   |             |             |             | 1: H&E      | fields: 1.  |
   |             |             |             |             | Specimen    |
   |             |             |             |             | Received,   |
   |             |             |             |             | 2. Cassette |
   |             |             |             |             | Summary, 3. |
   |             |             |             |             | Number of   |
   |             |             |             |             | Pieces in   |
   |             |             |             |             | Block, 4.   |
   |             |             |             |             | Staining.   |
   |             |             |             |             | This does   |
   |             |             |             |             | not always  |
   |             |             |             |             | work this   |
   |             |             |             |             | nicely.     |
   |             |             |             |             | Often one   |
   |             |             |             |             | or more of  |
   |             |             |             |             | fields is   |
   |             |             |             |             | empty or    |
   |             |             |             |             | confusing.  |
   |             |             |             |             |             |
   |             |             |             |             | .. note::   |
   |             |             |             |             |             |
   |             |             |             |             |    This     |
   |             |             |             |             |    field is |
   |             |             |             |             |    limited  |
   |             |             |             |             |    to 64    |
   |             |             |             |             |             |
   |             |             |             |             |  characters |
   +-------------+-------------+-------------+-------------+-------------+
   | >Specimen   | (0040,0602) | Detailed    | A: Received | This is a   |
   | Detailed    |             | textual     | fresh for   | mapping     |
   | Description |             | specimen    | int         | from the    |
   |             |             | description | raoperative | LIS Gross   |
   |             |             |             | co          | Description |
   |             |             |             | nsultation, | Field and   |
   |             |             |             | labeled     | the Block   |
   |             |             |             | with the    | Summary.    |
   |             |             |             | patient's   | Note that   |
   |             |             |             | name,       | in Case     |
   |             |             |             | number and  | S07-100,    |
   |             |             |             | "left upper | there were  |
   |             |             |             | lobe," is a | six parts.  |
   |             |             |             | pink-tan,   | This means  |
   |             |             |             | w           | the LIS     |
   |             |             |             | edge-shaped | gross       |
   |             |             |             | segment of  | description |
   |             |             |             | soft        | field will  |
   |             |             |             | tissue, 6.9 | have six    |
   |             |             |             | x 4.2 x 1.0 | sections (A |
   |             |             |             | cm. The     | - F). We    |
   |             |             |             | pleural     | would have  |
   |             |             |             | surface is  | to parse    |
   |             |             |             | pink-tan    | the gross   |
   |             |             |             | and         | description |
   |             |             |             | glistening  | field into  |
   |             |             |             | with a      | those parts |
   |             |             |             | stapled     | (A-F) and   |
   |             |             |             | line        | then only   |
   |             |             |             | measuring   | incorporate |
   |             |             |             | 12.0 cm. in | section "A" |
   |             |             |             | length. The | into this   |
   |             |             |             | pleural     | Attribute.  |
   |             |             |             | surface     | The same    |
   |             |             |             | shows a 0.5 | would be    |
   |             |             |             | cm. area of | true of the |
   |             |             |             | puckering.  | Blocks.     |
   |             |             |             | The pleural |             |
   |             |             |             | surface is  | .. note::   |
   |             |             |             | inked       |             |
   |             |             |             | black. The  |    One      |
   |             |             |             | cut surface |    could    |
   |             |             |             | reveals a   |    consider |
   |             |             |             | 1.2 x 1.1   |    listing  |
   |             |             |             | cm,         |    all the  |
   |             |             |             | white-gray, |    Blocks   |
   |             |             |             | irregular   |             |
   |             |             |             | mass        |  associated |
   |             |             |             | abutting    |    with     |
   |             |             |             | the pleural |    Part A.  |
   |             |             |             | surface and |    It would |
   |             |             |             | deep to the |    be easy  |
   |             |             |             | puckered    |    to do    |
   |             |             |             | area. The   |    and      |
   |             |             |             | remainder   |    might    |
   |             |             |             | of the cut  |    give     |
   |             |             |             | surface is  |    useful   |
   |             |             |             | red-brown   |    i        |
   |             |             |             | and         | nformation. |
   |             |             |             | congested.  |             |
   |             |             |             | No other    |             |
   |             |             |             | lesions are |             |
   |             |             |             | identified. |             |
   |             |             |             | Rep         |             |
   |             |             |             | resentative |             |
   |             |             |             | sections    |             |
   |             |             |             | are         |             |
   |             |             |             | submitted.  |             |
   |             |             |             |             |             |
   |             |             |             | Block 5:    |             |
   |             |             |             | "Mass" (2   |             |
   |             |             |             | pieces)     |             |
   +-------------+-------------+-------------+-------------+-------------+
   | >Specimen   | (0040,0610) | Sequence of | (see        |             |
   | Preparation |             | Items       | `table_tit  |             |
   | Sequence    |             | identifying | le <#table_ |             |
   |             |             | the process | NN.6-4>`__) |             |
   |             |             | steps used  |             |             |
   |             |             | to prepare  |             |             |
   |             |             | the         |             |             |
   |             |             | specimen    |             |             |
   |             |             | for image   |             |             |
   |             |             | a           |             |             |
   |             |             | cquisition. |             |             |
   |             |             | One or more |             |             |
   |             |             | Items may   |             |             |
   |             |             | be present. |             |             |
   |             |             | This        |             |             |
   |             |             | Sequence    |             |             |
   |             |             | includes    |             |             |
   |             |             | description |             |             |
   |             |             | of the      |             |             |
   |             |             | specimen    |             |             |
   |             |             | sampling    |             |             |
   |             |             | step from a |             |             |
   |             |             | parent      |             |             |
   |             |             | specimen,   |             |             |
   |             |             | potentially |             |             |
   |             |             | back to the |             |             |
   |             |             | original    |             |             |
   |             |             | part        |             |             |
   |             |             | collection. |             |             |
   +-------------+-------------+-------------+-------------+-------------+
   | >>Specimen  | (0040,0612) | Sequence of |             |             |
   | Preparation |             | Content     |             |             |
   | Step        |             | Items       |             |             |
   | Content     |             | identifying |             |             |
   | Item        |             | the         |             |             |
   | Sequence    |             | processes   |             |             |
   |             |             | used in one |             |             |
   |             |             | preparation |             |             |
   |             |             | step to     |             |             |
   |             |             | prepare the |             |             |
   |             |             | specimen    |             |             |
   |             |             | for image   |             |             |
   |             |             | a           |             |             |
   |             |             | cquisition. |             |             |
   |             |             | One or more |             |             |
   |             |             | Items may   |             |             |
   |             |             | be present. |             |             |
   +-------------+-------------+-------------+-------------+-------------+
   | >Primary    | (0008,2228) | Original    |             |             |
   | Anatomic    |             | anatomic    |             |             |
   | Structure   |             | location in |             |             |
   | Sequence    |             | patient of  |             |             |
   |             |             | specimen.   |             |             |
   |             |             | This        |             |             |
   |             |             | location    |             |             |
   |             |             | may be      |             |             |
   |             |             | inherited   |             |             |
   |             |             | from the    |             |             |
   |             |             | parent      |             |             |
   |             |             | specimen,   |             |             |
   |             |             | or further  |             |             |
   |             |             | refined by  |             |             |
   |             |             | modifiers   |             |             |
   |             |             | depending   |             |             |
   |             |             | on the      |             |             |
   |             |             | sampling    |             |             |
   |             |             | procedure   |             |             |
   |             |             | for this    |             |             |
   |             |             | specimen.   |             |             |
   +-------------+-------------+-------------+-------------+-------------+
   | >>Code      | (0008,0100) |             | 44714003    | This is a   |
   | Value       |             |             |             | code        |
   |             |             |             |             | sequence    |
   |             |             |             |             | item        |
   +-------------+-------------+-------------+-------------+-------------+
   | >>Coding    | (0008,0102) |             | SCT         |             |
   | Scheme      |             |             |             |             |
   | Designator  |             |             |             |             |
   +-------------+-------------+-------------+-------------+-------------+
   | >>Code      | (0008,0104) |             | Left Upper  |             |
   | Meaning     |             |             | Lobe of     |             |
   |             |             |             | Lung        |             |
   +-------------+-------------+-------------+-------------+-------------+

The example Specimen Preparation Sequence first describes the most
recent processing of the slide (staining), then goes back to show its
provenance. Notice that there is no sampling process for the slide
described here; the LIS did not record the step of slicing of blocks
into slides.

.. table:: Specimen Preparation Sequence for Slide

   +---------+---------+---------+---------+---------+---------+---------+
   | **S     | **S     | **T     | **Value | **      | **      | **Com   |
   | pecimen | pecimen | emplate | Type    | Concept | Example | ments** |
   | Prep    | Prep.   | / Row** | (0040,  | Name    | Value** |         |
   | aration | Step    |         | A040)** | Code    |         |         |
   | S       | Content |         |         | S       |         |         |
   | equence | Item    |         |         | equence |         |         |
   | - Item  | S       |         |         | (0040,  |         |         |
   | #**     | equence |         |         | A043)** |         |         |
   |         | - Item  |         |         |         |         |         |
   |         | #**     |         |         |         |         |         |
   +=========+=========+=========+=========+=========+=========+=========+
   | 1       | 1       | 8001 /  | TEXT    | (       | S07-100 | Part    |
   |         |         | 1       |         | 121041, | A       | Col     |
   |         |         |         |         | DCM,    |         | lection |
   |         |         |         |         | "S      |         | in OR.  |
   |         |         |         |         | pecimen |         |         |
   |         |         |         |         | Ident   |         |         |
   |         |         |         |         | ifier") |         |         |
   +---------+---------+---------+---------+---------+---------+---------+
   | 2       | 8001 /  | TEXT    | (       | Case    |         |         |
   |         | 2       |         | 111724, | Medical |         |         |
   |         |         |         | DCM,    | Center  |         |         |
   |         |         |         | "Issuer |         |         |         |
   |         |         |         | of      |         |         |         |
   |         |         |         | S       |         |         |         |
   |         |         |         | pecimen |         |         |         |
   |         |         |         | Ident   |         |         |         |
   |         |         |         | ifier") |         |         |         |
   +---------+---------+---------+---------+---------+---------+---------+
   | 3       | 8001 /  | CODE    | (       | `(17    |         |         |
   |         | 3       |         | 111701, | 636008, |         |         |
   |         |         |         | DCM,    | SCT,    |         |         |
   |         |         |         | "Pro    | "S      |         |         |
   |         |         |         | cessing | pecimen |         |         |
   |         |         |         | type")  | collec  |         |         |
   |         |         |         |         | tion")  |         |         |
   |         |         |         |         | <http:/ |         |         |
   |         |         |         |         | /snomed |         |         |
   |         |         |         |         | .info/i |         |         |
   |         |         |         |         | d/17636 |         |         |
   |         |         |         |         | 008>`__ |         |         |
   +---------+---------+---------+---------+---------+---------+---------+
   | 4       | 8001 /  | D       | (       | 20070   |         |         |
   |         | 4       | ATETIME | 111702, | 3230827 |         |         |
   |         |         |         | DCM,    |         |         |         |
   |         |         |         | "D      |         |         |         |
   |         |         |         | ateTime |         |         |         |
   |         |         |         | of      |         |         |         |
   |         |         |         | proce   |         |         |         |
   |         |         |         | ssing") |         |         |         |
   +---------+---------+---------+---------+---------+---------+---------+
   | 5       | 8001 /  | TEXT    | (       | Taken   |         |         |
   |         | 5       |         | 111703, |         |         |         |
   |         |         |         | DCM,    |         |         |         |
   |         |         |         | "Pro    |         |         |         |
   |         |         |         | cessing |         |         |         |
   |         |         |         | step    |         |         |         |
   |         |         |         | descri  |         |         |         |
   |         |         |         | ption") |         |         |         |
   +---------+---------+---------+---------+---------+---------+---------+
   | 6       | 8001 /  | CODE    | (       | `(65    |         |         |
   |         | 8       |         | 111704, | 801008, |         |         |
   |         |         |         | DCM,    | SCT,    |         |         |
   |         | 8002 /  |         | "S      | "Exci   |         |         |
   |         | 1       |         | ampling | sion")  |         |         |
   |         |         |         | M       | <http:/ |         |         |
   |         |         |         | ethod") | /snomed |         |         |
   |         |         |         |         | .info/i |         |         |
   |         |         |         |         | d/65801 |         |         |
   |         |         |         |         | 008>`__ |         |         |
   +---------+---------+---------+---------+---------+---------+---------+
   | 2       | 1       | 8001 /  | TEXT    | (       | S07-100 | S       |
   |         |         | 1       |         | 121041, | A       | pecimen |
   |         |         |         |         | DCM,    |         | r       |
   |         |         |         |         | "S      |         | eceived |
   |         |         |         |         | pecimen |         | in      |
   |         |         |         |         | Ident   |         | Pa      |
   |         |         |         |         | ifier") |         | thology |
   |         |         |         |         |         |         | dep     |
   |         |         |         |         |         |         | artment |
   +---------+---------+---------+---------+---------+---------+---------+
   | 2       | 8001 /  | TEXT    | (       | Case    |         |         |
   |         | 2       |         | 111724, | Medical |         |         |
   |         |         |         | DCM,    | Center  |         |         |
   |         |         |         | "Issuer |         |         |         |
   |         |         |         | of      |         |         |         |
   |         |         |         | S       |         |         |         |
   |         |         |         | pecimen |         |         |         |
   |         |         |         | Ident   |         |         |         |
   |         |         |         | ifier") |         |         |         |
   +---------+---------+---------+---------+---------+---------+---------+
   | 3       | 8001 /  | CODE    | (       | `(428   |         |         |
   |         | 3       |         | 111701, | 995007, |         |         |
   |         |         |         | DCM,    | SCT,    |         |         |
   |         |         |         | "Pro    | "S      |         |         |
   |         |         |         | cessing | pecimen |         |         |
   |         |         |         | type")  | Receiv  |         |         |
   |         |         |         |         | ing") < |         |         |
   |         |         |         |         | http:// |         |         |
   |         |         |         |         | snomed. |         |         |
   |         |         |         |         | info/id |         |         |
   |         |         |         |         | /428995 |         |         |
   |         |         |         |         | 007>`__ |         |         |
   +---------+---------+---------+---------+---------+---------+---------+
   | 4       | 8001 /  | D       | (       | 20070   |         |         |
   |         | 4       | ATETIME | 111702, | 3230943 |         |         |
   |         |         |         | DCM,    |         |         |         |
   |         |         |         | "D      |         |         |         |
   |         |         |         | ateTime |         |         |         |
   |         |         |         | of      |         |         |         |
   |         |         |         | proce   |         |         |         |
   |         |         |         | ssing") |         |         |         |
   +---------+---------+---------+---------+---------+---------+---------+
   | 3       | 1       | 8001 /  | TEXT    | (       | S07-100 | S       |
   |         |         | 1       |         | 121041, | A 5     | ampling |
   |         |         |         |         | DCM,    |         | to      |
   |         |         |         |         | "S      |         | block   |
   |         |         |         |         | pecimen |         |         |
   |         |         |         |         | Ident   |         |         |
   |         |         |         |         | ifier") |         |         |
   +---------+---------+---------+---------+---------+---------+---------+
   | 2       | 8001 /  | TEXT    | (       | Case    |         |         |
   |         | 2       |         | 111724, | Medical |         |         |
   |         |         |         | DCM,    | Center  |         |         |
   |         |         |         | "Issuer |         |         |         |
   |         |         |         | of      |         |         |         |
   |         |         |         | S       |         |         |         |
   |         |         |         | pecimen |         |         |         |
   |         |         |         | Ident   |         |         |         |
   |         |         |         | ifier") |         |         |         |
   +---------+---------+---------+---------+---------+---------+---------+
   | 3       | 8001 /  | CODE    | (       | `(433   |         |         |
   |         | 3       |         | 111701, | 465004, |         |         |
   |         |         |         | DCM,    | SCT,    |         |         |
   |         |         |         | "Pro    | "S      |         |         |
   |         |         |         | cessing | ampling |         |         |
   |         |         |         | type")  | of      |         |         |
   |         |         |         |         | tissue  |         |         |
   |         |         |         |         | speci   |         |         |
   |         |         |         |         | men") < |         |         |
   |         |         |         |         | http:// |         |         |
   |         |         |         |         | snomed. |         |         |
   |         |         |         |         | info/id |         |         |
   |         |         |         |         | /433465 |         |         |
   |         |         |         |         | 004>`__ |         |         |
   +---------+---------+---------+---------+---------+---------+---------+
   | 4       | 8001 /  | TEXT    | (       | Block   |         |         |
   |         | 5       |         | 111703, | C       |         |         |
   |         |         |         | DCM,    | reation |         |         |
   |         |         |         | "Pro    |         |         |         |
   |         |         |         | cessing |         |         |         |
   |         |         |         | step    |         |         |         |
   |         |         |         | descri  |         |         |         |
   |         |         |         | ption") |         |         |         |
   +---------+---------+---------+---------+---------+---------+---------+
   | 5       | 8001 /  | CODE    | (       | `(122   |         |         |
   |         | 8       |         | 111704, | 459003, |         |         |
   |         |         |         | DCM,    | SCT,    |         |         |
   |         | 8002 /  |         | "S      | "       |         |         |
   |         | 1       |         | ampling | Dissect |         |         |
   |         |         |         | M       | ion") < |         |         |
   |         |         |         | ethod") | http:// |         |         |
   |         |         |         |         | snomed. |         |         |
   |         |         |         |         | info/id |         |         |
   |         |         |         |         | /122459 |         |         |
   |         |         |         |         | 003>`__ |         |         |
   +---------+---------+---------+---------+---------+---------+---------+
   | 6       | 8001 /  | TEXT    | (       | S07-100 |         |         |
   |         | 8       |         | 111705, | A       |         |         |
   |         |         |         | DCM,    |         |         |         |
   |         | 8002 /  |         | "Parent |         |         |         |
   |         | 2       |         | S       |         |         |         |
   |         |         |         | pecimen |         |         |         |
   |         |         |         | Ident   |         |         |         |
   |         |         |         | ifier") |         |         |         |
   +---------+---------+---------+---------+---------+---------+---------+
   | 7       | 8001 /  | TEXT    | (       | Case    |         |         |
   |         | 8       |         | 111706, | Medical |         |         |
   |         |         |         | DCM,    | Center  |         |         |
   |         | 8002 /  |         | "Issuer |         |         |         |
   |         | 3       |         | of      |         |         |         |
   |         |         |         | Parent  |         |         |         |
   |         |         |         | S       |         |         |         |
   |         |         |         | pecimen |         |         |         |
   |         |         |         | Ident   |         |         |         |
   |         |         |         | ifier") |         |         |         |
   +---------+---------+---------+---------+---------+---------+---------+
   | 8       | 8001 /  | CODE    | (       | `(38    |         |         |
   |         | 8       |         | 111707, | 866009, |         |         |
   |         |         |         | DCM,    | SCT,    |         |         |
   |         | 8002 /  |         | "Parent | "A      |         |         |
   |         | 4       |         | s       | natomic |         |         |
   |         |         |         | pecimen | part")  |         |         |
   |         |         |         | type")  | <http:/ |         |         |
   |         |         |         |         | /snomed |         |         |
   |         |         |         |         | .info/i |         |         |
   |         |         |         |         | d/38866 |         |         |
   |         |         |         |         | 009>`__ |         |         |
   +---------+---------+---------+---------+---------+---------+---------+
   | 9       | 8001 /  | TEXT    | (       | Mass    | This is |         |
   |         | 8       |         | 111709, |         | coming  |         |
   |         |         |         | DCM,    |         | from    |         |
   |         | 8002 /  |         | "L      |         | the     |         |
   |         | 6       |         | ocation |         | summary |         |
   |         |         |         | of      |         | of      |         |
   |         |         |         | s       |         | blocks  |         |
   |         |         |         | ampling |         | field   |         |
   |         |         |         | site")  |         | in the  |         |
   |         |         |         |         |         | LIS     |         |
   +---------+---------+---------+---------+---------+---------+---------+
   | 4       | 1       | 8001 /  | TEXT    | (       | S07-100 | Block   |
   |         |         | 1       |         | 121041, | A 5     | Pro     |
   |         |         |         |         | DCM,    |         | cessing |
   |         |         |         |         | "S      |         |         |
   |         |         |         |         | pecimen |         |         |
   |         |         |         |         | Ident   |         |         |
   |         |         |         |         | ifier") |         |         |
   +---------+---------+---------+---------+---------+---------+---------+
   | 2       | 8001 /  | TEXT    | (       | Case    |         |         |
   |         | 2       |         | 111724, | Medical |         |         |
   |         |         |         | DCM,    | Center  |         |         |
   |         |         |         | "Issuer |         |         |         |
   |         |         |         | of      |         |         |         |
   |         |         |         | S       |         |         |         |
   |         |         |         | pecimen |         |         |         |
   |         |         |         | Ident   |         |         |         |
   |         |         |         | ifier") |         |         |         |
   +---------+---------+---------+---------+---------+---------+---------+
   | 3       | 8001 /  | CODE    | (       | `(9     |         |         |
   |         | 3       |         | 111701, | 265001, |         |         |
   |         |         |         | DCM,    | SCT,    |         |         |
   |         |         |         | "Pro    | "S      |         |         |
   |         |         |         | cessing | pecimen |         |         |
   |         |         |         | type")  | Proce   |         |         |
   |         |         |         |         | ssing") |         |         |
   |         |         |         |         |  <http: |         |         |
   |         |         |         |         | //snome |         |         |
   |         |         |         |         | d.info/ |         |         |
   |         |         |         |         | id/9265 |         |         |
   |         |         |         |         | 001>`__ |         |         |
   +---------+---------+---------+---------+---------+---------+---------+
   | 4       | 8001 /  | D       | (       | 20070   |         |         |
   |         | 4       | ATETIME | 111702, | 3231900 |         |         |
   |         |         |         | DCM,    |         |         |         |
   |         |         |         | "D      |         |         |         |
   |         |         |         | ateTime |         |         |         |
   |         |         |         | of      |         |         |         |
   |         |         |         | proce   |         |         |         |
   |         |         |         | ssing") |         |         |         |
   +---------+---------+---------+---------+---------+---------+---------+
   | 5       | 8001 /  | TEXT    | (       | S       |         |         |
   |         | 5       |         | 111703, | tandard |         |         |
   |         |         |         | DCM,    | Block   |         |         |
   |         |         |         | "Pro    | Pro     |         |         |
   |         |         |         | cessing | cessing |         |         |
   |         |         |         | step    | (Fo     |         |         |
   |         |         |         | descri  | rmalin) |         |         |
   |         |         |         | ption") |         |         |         |
   +---------+---------+---------+---------+---------+---------+---------+
   | 6       | 8001 /  | CODE    | `(430   | `(111   |         |         |
   |         | 10      |         | 864009, | 095003, |         |         |
   |         |         |         | SCT,    | SCT,    |         |         |
   |         |         |         | "Tissue | "Forma  |         |         |
   |         |         |         | Fixat   | lin") < |         |         |
   |         |         |         | ive") < | http:// |         |         |
   |         |         |         | http:// | snomed. |         |         |
   |         |         |         | snomed. | info/id |         |         |
   |         |         |         | info/id | /111095 |         |         |
   |         |         |         | /430864 | 003>`__ |         |         |
   |         |         |         | 009>`__ |         |         |         |
   +---------+---------+---------+---------+---------+---------+---------+
   | 5       | 1       | 8001 /  | TEXT    | (       | S07-100 | Block   |
   |         |         | 1       |         | 121041, | A 5     | em      |
   |         |         |         |         | DCM,    |         | bedding |
   |         |         |         |         | "S      |         |         |
   |         |         |         |         | pecimen |         |         |
   |         |         |         |         | Ident   |         |         |
   |         |         |         |         | ifier") |         |         |
   +---------+---------+---------+---------+---------+---------+---------+
   | 2       | 8001 /  | TEXT    | (       | Case    |         |         |
   |         | 2       |         | 111724, | Medical |         |         |
   |         |         |         | DCM,    | Center  |         |         |
   |         |         |         | "Issuer |         |         |         |
   |         |         |         | of      |         |         |         |
   |         |         |         | S       |         |         |         |
   |         |         |         | pecimen |         |         |         |
   |         |         |         | Ident   |         |         |         |
   |         |         |         | ifier") |         |         |         |
   +---------+---------+---------+---------+---------+---------+---------+
   | 3       | 8001 /  | CODE    | (       | `(9     |         |         |
   |         | 3       |         | 111701, | 265001, |         |         |
   |         |         |         | DCM,    | SCT,    |         |         |
   |         |         |         | "Pro    | "S      |         |         |
   |         |         |         | cessing | pecimen |         |         |
   |         |         |         | type")  | Proce   |         |         |
   |         |         |         |         | ssing") |         |         |
   |         |         |         |         |  <http: |         |         |
   |         |         |         |         | //snome |         |         |
   |         |         |         |         | d.info/ |         |         |
   |         |         |         |         | id/9265 |         |         |
   |         |         |         |         | 001>`__ |         |         |
   +---------+---------+---------+---------+---------+---------+---------+
   | 4       | 8001 /  | D       | (       | 20070   |         |         |
   |         | 4       | ATETIME | 111702, | 3240500 |         |         |
   |         |         |         | DCM,    |         |         |         |
   |         |         |         | "D      |         |         |         |
   |         |         |         | ateTime |         |         |         |
   |         |         |         | of      |         |         |         |
   |         |         |         | proce   |         |         |         |
   |         |         |         | ssing") |         |         |         |
   +---------+---------+---------+---------+---------+---------+---------+
   | 5       | 8001 /  | TEXT    | (       | Em      |         |         |
   |         | 5       |         | 111703, | bedding |         |         |
   |         |         |         | DCM,    | (pa     |         |         |
   |         |         |         | "Pro    | raffin) |         |         |
   |         |         |         | cessing |         |         |         |
   |         |         |         | step    |         |         |         |
   |         |         |         | descri  |         |         |         |
   |         |         |         | ption") |         |         |         |
   +---------+---------+---------+---------+---------+---------+---------+
   | 6       | 8001 /  | CODE    | `(430   | `(255   |         |         |
   |         | 11      |         | 863003, | 667006, |         |         |
   |         |         |         | SCT,    | SCT,    |         |         |
   |         |         |         | "Em     | "Paraf  |         |         |
   |         |         |         | bedding | fin") < |         |         |
   |         |         |         | med     | http:// |         |         |
   |         |         |         | ium") < | snomed. |         |         |
   |         |         |         | http:// | info/id |         |         |
   |         |         |         | snomed. | /255667 |         |         |
   |         |         |         | info/id | 006>`__ |         |         |
   |         |         |         | /430863 |         |         |         |
   |         |         |         | 003>`__ |         |         |         |
   +---------+---------+---------+---------+---------+---------+---------+
   | 6       | 1       | 8001 /  | TEXT    | (       | S07-100 | Slide   |
   |         |         | 1       |         | 121041, | A 5 1   | S       |
   |         |         |         |         | DCM,    |         | taining |
   |         |         |         |         | "S      |         |         |
   |         |         |         |         | pecimen |         |         |
   |         |         |         |         | Ident   |         |         |
   |         |         |         |         | ifier") |         |         |
   +---------+---------+---------+---------+---------+---------+---------+
   | 2       | 8001 /  | CODE    | (       | `(127   |         |         |
   |         | 3       |         | 111701, | 790008, |         |         |
   |         |         |         | DCM,    | SCT,    |         |         |
   |         |         |         | "Pro    | "Stain  |         |         |
   |         |         |         | cessing | ing") < |         |         |
   |         |         |         | type")  | http:// |         |         |
   |         |         |         |         | snomed. |         |         |
   |         |         |         |         | info/id |         |         |
   |         |         |         |         | /127790 |         |         |
   |         |         |         |         | 008>`__ |         |         |
   +---------+---------+---------+---------+---------+---------+---------+
   | 3       | 8001 /  | D       | (       | 20070   |         |         |
   |         | 4       | ATETIME | 111702, | 3240700 |         |         |
   |         |         |         | DCM,    |         |         |         |
   |         |         |         | "D      |         |         |         |
   |         |         |         | ateTime |         |         |         |
   |         |         |         | of      |         |         |         |
   |         |         |         | proce   |         |         |         |
   |         |         |         | ssing") |         |         |         |
   +---------+---------+---------+---------+---------+---------+---------+
   | 4       | 8001 /  | TEXT    | `(424   | H&E (1) |         |         |
   |         | 9       |         | 361007, |         |         |         |
   |         |         |         | SCT,    |         |         |         |
   |         | 8003 /  |         | "Using  |         |         |         |
   |         | 2       |         | substa  |         |         |         |
   |         |         |         | nce") < |         |         |         |
   |         |         |         | http:// |         |         |         |
   |         |         |         | snomed. |         |         |         |
   |         |         |         | info/id |         |         |         |
   |         |         |         | /424361 |         |         |         |
   |         |         |         | 007>`__ |         |         |         |
   +---------+---------+---------+---------+---------+---------+---------+

.. _sect_NN.7:

Specimen Data in Pathology Imaging Workflow Management
------------------------------------------------------

Workflow management in the DICOM imaging environment utilizes the
Modality Worklist (MWL) and Modality Performed Procedure Step (MPPS)
services. Within the pathology department, these services support both
human controlled imaging (e.g., gross specimen photography), as well as
automated slide scanning modalities.

While this section provides an overview of the DICOM services for
managing workflow, the reader is referred to the IHE Anatomic Pathology
Domain Technical Framework for specific use cases and profiles for
pathology imaging workflow management.

.. _sect_NN.7.1:

Modality Worklist
~~~~~~~~~~~~~~~~~

The contents of the Specimen Module may be conveyed in the Scheduled
Specimen Sequence of the Modality Worklist query. This feature allows an
imaging system (Modality Worklist SCU) to query for work items by
Container ID. The worklist server (SCP) of the laboratory information
system can then return all the necessary information for creating a
DICOM specimen-related image. This information includes patient identity
and the complete slide processing history (including stain applied). It
may be used for imaging set-up and/or inclusion in the Image SOP
Instance.

.. _sect_NN.7.1.1:

MWL for Whole Slide Imaging
^^^^^^^^^^^^^^^^^^^^^^^^^^^

In addition to the Specimen Module Attributes, the set up of an
automated whole slide scanner requires the acquisition parameters such
as scan resolution, number of Z-planes, fluorescence wavelengths, etc. A
managed set of such parameters is called a Protocol (see ), and the MWL
response may contain a Protocol Code to control scanning set up.
Additional set-up parameters can be passed as Content Items in the
associated Protocol Context Sequence; this might be important when the
reading pathologist requests a rescan of the slide with slightly
different settings.

.. _sect_NN.7.2:

Modality Performed Procedure Step
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

When scanning is initiated, the scanner reports the procedure step in a
Modality Performed Procedure Step (MPPS) transaction.

Upon completion (or cancellation) of an image acquisition, the modality
reports the work completed in an update to the MPPS. The MPPS can convey
both the Container ID and the image UIDs, so that the workflow manager
(laboratory information system) is advised of the image UIDs associated
with each imaged specimen.

