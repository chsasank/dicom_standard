.. _chapter_H:

Print Management Service Class (Normative)
==========================================

.. _sect_H.1:

Scope
-----

The Print Management Service Class defines an application-level
class-of-service that facilitates the printing of images and image
related data on a hard copy medium.

.. note::

   The DICOM Print Management Service Class covers the general cases of
   printing medical images in standardized layouts. An application can
   obtain more flexible layout, annotation, and formatting either by
   direct manipulation of the pixel matrices used in DICOM Print
   Management, or by utilizing page descriptions written in a page
   description language (such as Postscript or PDF) that are
   communicated to the printing system using commonly available
   protocols. These other page descriptions languages are not
   communicated using DICOM protocols and their use is outside the scope
   of the DICOM Standard.

.. _sect_H.2:

Print Management Model
----------------------

.. _sect_H.2.1:

Print Management Data Flow Model
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

.. _sect_H.2.1.1:

Global Data Flow Model
^^^^^^^^^^^^^^^^^^^^^^

The Print Management Data Flow Model (`figure_title <#figure_H.2-1>`__)
consists of three main processes:

-  Film Session Management process

-  Print process

.. note::

   The Standard uses the word film as a general name for different types
   of hard copy media (e.g., photographic film, paper).

The Film Session Management process is responsible for acquiring all the
information that is required to print the film session. The film session
is the atomic work package of the Print Management Application and
contains one or more films related in a user defined way (e.g.,
belonging to the same exam, patient) that are originated from one host
(e.g., workstation, diagnostic modality) and that are printed on one
hard copy printer.

Each film consists of one or more images and zero or more film related
annotations. An annotation consists of one or more lines of text.

Each image consists of pixel data and zero or more overlay planes. The
user controls the look of the film by assigning values to print
parameters.

Print parameters are defined at film session, film, image and annotation
levels. The parameter level determines the scope of operation of the
print parameters (e.g., print parameters of the image level are valid
for the corresponding image).

The inputs of the Film Session Management process are:

-  set of images and image related data

-  presentation data that describes the visual look of the films

The output of the Film Session Management process is the Print Job,
which contains all the information to print the film session.

The Print process prints a set of films, based on the information in the
Print Job. The Print process is implementation specific and its
management is beyond the scope of the DICOM Standard.

.. _sect_H.2.1.2:

Grayscale Transformations
^^^^^^^^^^^^^^^^^^^^^^^^^

The Print Management Service Class supports two grayscale
transformations and spatial transformations that converts an original
image into a printed image.

The sequence of spatial transformations (e.g., magnification and merging
of annotation with images) and their relationships with the grayscale
transformations are implementation specific and fall beyond the scope of
the DICOM Standard.

The sequence of grayscale transformations is important for achieving
consistent image quality because of the non-orthogonal nature of the
different transformations. `figure_title <#figure_H.2-2>`__ describes
the sequence of grayscale transformations.

.. note::

   This section previously described Modality LUT and VOI LUT
   transformations in more detail. Since Referenced Print SOP Classes
   have been retired, these descriptions no longer apply to the Print
   Management Service Class. See PS 3.4-1998.

.. _sect_H.2.1.2.1:

Modality and User Specific Transformations
''''''''''''''''''''''''''''''''''''''''''

Examples of these transformations are Modality LUT, Mask Subtraction,
and VOI LUT.

The Modality LUT transforms manufacturer dependent pixel values into
pixel values that are meaningful for the modality and are manufacturer
independent.

The VOI LUT transforms the modality pixel values into pixel values that
are meaningful for the user or the application. For example it selects
of a range of pixel values to be optimized for display, such as soft
tissue or bone windows in a CT image.

.. _sect_H.2.1.2.2:

Polarity
''''''''

Polarity specifies whether minimum input pixel values shall be displayed
as black or white. If Polarity (2020,0020) is NORMAL then the pixels
will be displayed as specified by Photometric Interpretation; if
Polarity is REVERSE then the pixels will be displayed with the opposite
polarity as specified by Photometric Interpretation.

Polarity (2020,0020) is an Attribute of the Image Box IOD.

.. _sect_H.2.1.2.3:

Presentation LUT
''''''''''''''''

The Presentation LUT transforms the polarity pixel values into
Presentation Values (P-Values), which are meaningful for display of the
images. P-Values are approximately related to human perceptual response.
They are intended to facilitate consistent display with common input for
both hardcopy and softcopy display devices and be independent of the
specific class or characteristics of the display device. It is used to
realize image display tailored for specific modalities, applications,
and user preferences

In the Print Management Service Class, the Presentation LUT is part of
the Presentation LUT IOD.

Hardcopy devices convert P-Values into optical density for printing.
This conversion depends on desired image D-max and D-min. It also
depends on expected viewing conditions such as lightbox intensity for
transparency films. The conversion to printed density is specified in
the Presentation LUT SOP Class.

If the modality desires to natively specify P-Values as its output, it
can negotiate for support of the Presentation LUT, but specify a LUT
that is an identity function. The identity function informs the display
device that no further translation is necessary.

.. note::

   Performing this translation in the printer prevents potential loss of
   precision (detail) that would occur if this translation were to be
   performed on many of the existing 8-bit modalities.

.. _sect_H.2.2:

Print Management Service Class Structure
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

The Print Management Service Class Structure is shown in
`figure_title <#figure_H.2-3>`__.

The Print Management SCU and Print Management SCP are peer DICOM Print
Management Application Entities. The Application Entity of the Print
Management SCP corresponds with one or more hard copy printers. If the
SCP Application Entity corresponds with multiple printers then the SCP
Application Entity selects for each Print Job the printer where the
Print Job will be printed.

The Print Management SCU and Print Management SCP establish an
Association by using the Association Services of the OSI Upper Layer
Service. During Association establishment, the DICOM Print Management
Application Entities negotiate the supported SOP Classes. The
negotiation procedure is defined in `Association
Negotiation <#sect_H.5>`__.

`figure_title <#figure_H.2-4>`__ shows alternative configurations for
printing images and image related data from one host to multiple
printers.

-  Configuration 1: one SCU Application Entity corresponds with the host
   and one SCP Application Entity corresponds with multiple printers.
   The SCU has no control over the print parameters of each printer and
   over the print destination of the Print Job.

-  Configuration 2: one SCU Application Entity corresponds with the host
   and one Application Entity SCP corresponds with each printer. The SCU
   has explicit control over the print parameters of each printer and
   over the print destination of the Print Job. Each SCP Application
   Entity has one Association with the SCU Application Entity and is
   identified by its Application Entity title.

.. _sect_H.2.3:

Print Management SOP Classes
~~~~~~~~~~~~~~~~~~~~~~~~~~~~

The Print Management SCU controls the Print Process by manipulating the
Print Management SOP Classes by means of the DIMSE Services. The Print
Management SOP Classes are managed by the Print Management SCP.

The Print Management SOP Classes are classified as follows:

-  Content related SOP Classes: these SOP Classes are an abstraction of
   the contents of a film (e.g., pixel data, text string). The content
   related SOP Classes correspond with the Image related SOP Classes,
   which are described in `Print Management SOP Class
   Definitions <#sect_H.4>`__ of this Part.

-  Presentation related SOP Classes: these SOP Classes are an
   abstraction of the presentation of a film (e.g., layout information)
   and are defined by Normalized IODs and Normalized DIMSE-N Services.
   The presentation related SOP Classes are defined in `Print Management
   SOP Class Definitions <#sect_H.4>`__ of this Part.

-  Printer related SOP Classes: these SOP Classes are an abstraction of
   the printer configuration and status and are defined by Normalized
   IODs. The Printer SOP Class is defined in `Print Management SOP Class
   Definitions <#sect_H.4>`__ of this Part.

.. _sect_H.2.4:

Usage Specifications
~~~~~~~~~~~~~~~~~~~~

The building blocks of SOP Classes are Modules and DIMSE Services. The
Modules contain related Attributes, which are Mandatory(M) or Optional
(U). The usage may be different for the SCU and SCP. The usage is
specified as a pair of letters: the former indicating the SCU usage, the
latter indicating the SCP usage.

DIMSE Service Group may be Mandatory (M) or Optional (U) as specified in
Section 5.4 of this Part.

The meaning and behavior of the usage specification for Attributes for
the Print Management Service Class are:

M/M
   The SCU shall provide a value for the Attribute. If the SCU does not
   supply a value, the SCP shall return a Failure status ("Missing
   Attribute," code 0120H). The SCP shall support at least one value of
   the Attribute. If the SCP does not support the value specified by the
   SCU, it shall return a Failure status ("Invalid Attribute Value,"
   code 0106H).

-/M
   The SCU's usage of the Attribute is undefined. The SCP shall support
   at least one value of the Attribute.

U/M
   The SCU may provide a value for the Attribute. If the SCP does not
   support the value specified by the SCU, it shall return either a
   Failure status ("Invalid Attribute Value", code 0106H) or return a
   Warning status ("Attribute Value out of range", code 0116H). In the
   case of Warning status, the SCP will apply the default value as
   defined in the SCP Conformance Statement.

U/U
   The SCU may provide a value for the Attribute. If the SCP does not
   support the value specified by the SCU, but does support the
   Attribute, it shall return either a Failure status ("Invalid
   Attribute Value", code 0106H) or a Warning status ("Attribute Value
   out of range", code 0116H). In the case of Warning status, the SCP
   will apply the default value as defined in the SCP Conformance
   Statement.

   If the SCP does not support the Attribute specified by the SCU, it
   shall return either a Failure status ("No such Attribute", code
   0105H) or return a Warning status ("Attribute list error", code
   0107H). In the case of Warning status, the behavior of the SCP is
   defined in the SCP Conformance Statement.

If the usage type designation is modified by a "C" (e.g., MC/M) the
specification stated above shall be modified to include the requirement
that the Attribute shall be supported if the specified condition is met.

.. _sect_H.2.5:

Status Code Categories
~~~~~~~~~~~~~~~~~~~~~~

For every operation requested on a SOP Class of the print management
service class, a status code will be returned. These status codes are
grouped into success, warning or failure categories.

.. note::

   These status codes categories are defined in :

   -  Success - indicates that the SCP performed the requested operation
      as requested.

   -  Warning - indicates that the SCP has received the request and will
      process it. However, immediate processing of the request, or
      processing in the way specified by the SCU, may not be possible.
      The SCP expects to be able to complete the request without further
      action by the SCU across the DICOM interface. The exact behavior
      of the SCP is described in the Conformance Statement.

   -  Failure - indicates that the SCP is unable to perform the request.
      The request will not be processed unless it is repeated by the SCU
      at a later time. The exact behavior of the SCP is described in the
      Conformance Statement.

.. _sect_H.3:

Print Management Conformance
----------------------------

.. _sect_H.3.1:

Scope
~~~~~

Print Management conformance is defined in terms of supported Meta SOP
Classes, which correspond with the mandatory functionality, and of
supported optional SOP Classes, which correspond with additional
functionality.

A Meta SOP Class corresponds with a pre-defined group of SOP Classes.
The following Print Management Meta SOP Classes are defined:

-  Basic Grayscale Print Management Meta SOP Class

-  Basic Color Print Management Meta SOP Class

All SCUs and SCPs of the Print Management Service Class shall support at
least one of the Basic Print Management Meta SOP Classes.

In addition the other Meta SOP Classes or optional SOP Classes may be
supported.

The Meta SOP Class level negotiation is used to define a minimum set of
print functions; the SOP Class level negotiation is used to define
additional functions.

If multiple Meta SOP Classes and one or more optional SOP Classes are
negotiated, the SCP shall support all the optional SOP Classes in
conjunction with all the Meta SOP Classes.

At association setup, the negotiation process between the Print
Management SCU and SCP shall occur for

-  one or more of the Meta SOP Classes and zero or more of the optional
   SOP Classes specified in `List of Optional SOP
   Classes <#sect_H.3.3.2>`__; or

-  one or more of the Printer, Print Job, and Printer Configuration
   Retrieval SOP Classes.

.. note::

   It is possible for an SCP to support Associations for printing and to
   also support additional Associations for the sole purpose of
   exchanging status information about the printer.

.. _sect_H.3.2:

Print Management Meta SOP Classes
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

.. _sect_H.3.2.1:

Description
^^^^^^^^^^^

The Basic Print Management Meta SOP Classes correspond with the minimum
functionality that an implementation of the Print Management Service
Class shall support. The Basic Print Management Meta SOP Classes support
the following mandatory features:

-  preformatted grayscale images or preformatted color images;
   preformatted images are images where annotation, graphics, overlays
   are burned in

-  pre-defined film layouts (image display formats)

-  basic presentation parameters on film session, film box and image box
   level

-  basic device management

The optional SOP Classes described in `Optional SOP
Classes <#sect_H.3.3>`__ may be used with the Basic Print Management
Meta SOP Classes.

The following features are optional for SCUs and SCPs:

-  Film box annotation

-  Presentation LUT

.. _sect_H.3.2.2:

Meta SOP Class Definitions
^^^^^^^^^^^^^^^^^^^^^^^^^^

.. _sect_H.3.2.2.1:

Basic Grayscale Print Management Meta SOP Class
'''''''''''''''''''''''''''''''''''''''''''''''

The Meta SOP Class is defined by the following set of supported SOP
Classes.

.. table:: SOP Classes of Basic Grayscale Print Management Meta SOP
Class

   +-------------------------+-------------------------+---------------+
   | SOP Class Name          | Reference               | Usage SCU/SCP |
   +=========================+=========================+===============+
   | Basic Film Session SOP  | `Basic Film Session SOP | M/M           |
   | Class                   | Class <#sect_H.4.1>`__  |               |
   +-------------------------+-------------------------+---------------+
   | Basic Film Box SOP      | `Basic Film Box SOP     | M/M           |
   | Class                   | Class <#sect_H.4.2>`__  |               |
   +-------------------------+-------------------------+---------------+
   | Basic Grayscale Image   | `Basic Grayscale Image  | M/M           |
   | Box SOP Class           | Box SOP                 |               |
   |                         | C                       |               |
   |                         | lass <#sect_H.4.3.1>`__ |               |
   +-------------------------+-------------------------+---------------+
   | Printer SOP Class       | `Printer SOP            | M/M           |
   |                         | Class <#sect_H.4.6>`__  |               |
   +-------------------------+-------------------------+---------------+

.. note::

   The image pixel data are part of the Basic Grayscale Image Box SOP
   Class

The meaning of the Usage SCU/SCP is described in `Usage
Specifications <#sect_H.2.4>`__.

The Basic Grayscale Print Management Meta SOP Class UID has the value
"1.2.840.10008.5.1.1.9".

.. _sect_H.3.2.2.2:

Basic Color Print Management Meta SOP Class
'''''''''''''''''''''''''''''''''''''''''''

The Meta SOP Class is defined by the following set of supported SOP
Classes.

.. table:: SOP Classes of Basic Color Print Management Meta SOP Class

   +-------------------------+-------------------------+---------------+
   | SOP Class Name          | Reference               | Usage SCU/SCP |
   +=========================+=========================+===============+
   | Basic Film Session SOP  | `Basic Film Session SOP | M/M           |
   | Class                   | Class <#sect_H.4.1>`__  |               |
   +-------------------------+-------------------------+---------------+
   | Basic Film Box SOP      | `Basic Film Box SOP     | M/M           |
   | Class                   | Class <#sect_H.4.2>`__  |               |
   +-------------------------+-------------------------+---------------+
   | Basic Color Image Box   | `Basic Color Image Box  | M/M           |
   | SOP Class               | SOP                     |               |
   |                         | C                       |               |
   |                         | lass <#sect_H.4.3.2>`__ |               |
   +-------------------------+-------------------------+---------------+
   | Printer SOP Class       | `Printer SOP            | M/M           |
   |                         | Class <#sect_H.4.6>`__  |               |
   +-------------------------+-------------------------+---------------+

.. note::

   The image pixel data are part of the Basic Color Image Box SOP Class

The meaning of the Usage SCU/SCP is described in `Usage
Specifications <#sect_H.2.4>`__.

The Basic Color Print Management Meta SOP Class UID has the value
"1.2.840.10008.5.1.1.18".

.. _sect_H.3.2.2.3:

Referenced Grayscale Print Management Meta SOP Class (Retired)
''''''''''''''''''''''''''''''''''''''''''''''''''''''''''''''

This section was previously defined in DICOM. It is now retired. See PS
3.4-1998.

.. _sect_H.3.2.2.4:

Referenced Color Print Management Meta SOP Class (Retired)
''''''''''''''''''''''''''''''''''''''''''''''''''''''''''

This section was previously defined in DICOM. It is now retired. See PS
3.4-1998.

.. _sect_H.3.2.2.5:

Pull Stored Print Management Meta SOP Class(Retired)
''''''''''''''''''''''''''''''''''''''''''''''''''''

This section was previously defined in DICOM. It is now retired. See PS
3.4-2004.

.. _sect_H.3.3:

Optional SOP Classes
~~~~~~~~~~~~~~~~~~~~

.. _sect_H.3.3.1:

Description
^^^^^^^^^^^

The optional SOP Classes address functionality beyond that of the Print
Management Meta SOP Classes. One or more optional SOP Classes may be
used in addition to the Print Management Meta SOP Classes.

The following functionality is supported by the optional SOP Classes:

-  annotation (text associated with a sheet of film)

-  tracking the printing of the print session

-  retrieval of printer configuration information

-  Presentation LUTs

Use of these optional SOP Classes allows an SCU to provide information
to be printed with or on an image without burning the information into
the image pixels. If these optional SOP Classes are not supported by
both the SCU and SCP, then only the information burnt in to the image
pixels before they are sent to the SCP will be printed. If the optional
SOP Classes are not supported, the SCU is responsible for burning all
expected text or graphics into the image pixels.

.. _sect_H.3.3.2:

List of Optional SOP Classes
^^^^^^^^^^^^^^^^^^^^^^^^^^^^

The following optional SOP Classes may be used in conjunction with the
Basic Print Management Meta SOP Classes specified in `Meta SOP Class
Definitions <#sect_H.3.2.2>`__.

.. table:: List of Optional SOP Classes for Basic Print Management Meta
SOP Classes

   +-------------------------+-------------------------+---------------+
   | SOP Class Name          | Reference               | Usage SCU/SCP |
   +=========================+=========================+===============+
   | Basic Annotation Box    | `Basic Annotation Box   | U/U           |
   | SOP Class               | SOP                     |               |
   |                         | Class <#sect_H.4.4>`__  |               |
   +-------------------------+-------------------------+---------------+
   | Print Job SOP Class     | `Print Job SOP          | U/U           |
   |                         | Class <#sect_H.4.5>`__  |               |
   +-------------------------+-------------------------+---------------+
   | Presentation LUT SOP    | `Presentation LUT SOP   | U/U           |
   | Class                   | Class <#sect_H.4.9>`__  |               |
   +-------------------------+-------------------------+---------------+
   | Printer Configuration   | `Printer Configuration  | U/U           |
   | Retrieval SOP Class     | Retrieval SOP           |               |
   |                         | Class <#sect_H.4.11>`__ |               |
   +-------------------------+-------------------------+---------------+

.. note::

   Negotiation of the Presentation LUT SOP Class does not imply any
   behavior in the SCP. Behavior is explicit when the Presentation LUT
   SOP Class is created and referenced at either the Film Session, Film
   Box, or Image Box levels.

.. _sect_H.3.4:

Conformance Statement
~~~~~~~~~~~~~~~~~~~~~

The implementation Conformance Statement of these SOP Classes shall
follow .

The SCU Conformance Statement shall specify the following items:

-  maximum number of supported Associations at the same time

-  list of supported SOP Classes and Meta SOP Classes

-  for each of the supported SOP and Meta SOP Classes:

-  list of supported optional SOP Class Attributes and DICOM Message
   Service Elements

-  for each supported Attribute (mandatory and optional Attribute), the
   valid range of values

The SCP Conformance Statement shall specify the following items:

-  maximum number of supported Associations at the same time

-  list of supported SOP Classes and Meta SOP Classes

-  minimum and maximum number of printable pixel matrix per supported
   film size

-  for each of the supported SOP Classes:

-  list of supported optional SOP Class Attributes and DICOM Message
   Service Elements

-  for each supported Attribute (mandatory and optional Attribute):

-  valid range of values

-  default value if no value is supplied by the SCU

-  status code (Failure or Warning) if SCU supplies a value that is out
   of range

-  for each supported DIMSE Service, the SCP behavior for all specific
   status codes

-  description of each supported custom Image Display Format (2010,0010)
   e.g., position and dimensions of each composing image box, numbering
   scheme of the image positions

-  description of each supported Annotation Display Format ID
   (2010,0030) e.g., position and dimensions of annotation box, font,
   number of characters

-  description of each supported configuration table (e.g.,
   identification, content)

-  if the SCP supports N-ACTION for the Film Session SOP Class then the
   SCP shall specify the maximum number of collated films

-  in the case of grayscale printers that print color images, the
   behavior of printing color images

-  if cropping of images is supported, the algorithm for removing rows
   and columns from the image

.. _sect_H.4:

Print Management SOP Class Definitions
--------------------------------------

.. _sect_H.4.1:

Basic Film Session SOP Class
~~~~~~~~~~~~~~~~~~~~~~~~~~~~

.. _sect_H.4.1.1:

IOD Description
^^^^^^^^^^^^^^^

The Basic Film Session IOD describes the presentation parameters that
are common for all the films of a film session (e.g., number of films,
film destination)

The Basic Film Session SOP Instance refers to one or more Basic Film Box
SOP Instances.

.. _sect_H.4.1.2:

DIMSE Service Group
^^^^^^^^^^^^^^^^^^^

The DIMSE Services applicable to the IOD are shown in
`table_title <#table_H.4-1>`__.

.. table:: DIMSE Service Group Applicable to Basic Film Session

   ============================= =============
   DICOM Message Service Element Usage SCU/SCP
   ============================= =============
   N-CREATE                      M/M
   N-SET                         U/M
   N-DELETE                      U/M
   N-ACTION                      U/U
   ============================= =============

The meaning of the Usage SCU/SCP is described in `Usage
Specifications <#sect_H.2.4>`__.

This Section describes the behavior of the DIMSE Services that are
specific for this IOD. The general behavior of the DIMSE Services is
specified in .

.. _sect_H.4.1.2.1:

N-CREATE
''''''''

The N-CREATE is used to create an instance of the Basic Film Session SOP
Class.

.. _sect_H.4.1.2.1.1:

Attributes
          

The Attribute list of the N-CREATE is defined as shown in
`table_title <#table_H.4-2>`__.

.. table:: N-CREATE Attribute List

   ====================== =========== =============
   Attribute Name         Tag         Usage SCU/SCP
   ====================== =========== =============
   Specific Character Set (0008,0005) U/U
   Number of Copies       (2000,0010) U/M
   Print Priority         (2000,0020) U/M
   Medium Type            (2000,0030) U/M
   Film Destination       (2000,0040) U/M
   Film Session Label     (2000,0050) U/U
   Memory Allocation      (2000,0060) U/U
   Owner ID               (2100,0160) U/U
   ====================== =========== =============

.. note::

   1. The memory allocation Attribute allows the SCU to reserve
      sufficient memory to store the "working" film session hierarchy as
      well the "copied" film session hierarchy in the Print Job in order
      to prevent deadlock situations.

   2. Owner ID (2100,0160) is a user option for the Basic Film Session.

The meaning of the Usage SCU/SCP is described in `Usage
Specifications <#sect_H.2.4>`__.

Within the film session, the allocated memory is consumed as SOP
Instances are created and is freed for reuse as SOP Instances are
deleted. All the allocated memory shall be released following
termination of the Association or deletion of the Film Session SOP
Instance.

.. _sect_H.4.1.2.1.2:

Status
      

`table_title <#table_H.4.1.2.1.2-1>`__ defines the specific status code
values that may be returned in a N-CREATE or N-SET response for this SOP
Class. See for additional response status codes of N-CREATE and N-SET
DIMSE Services.

.. table:: Status Values for Basic Film Session SOP Class

   ============== ================================= ===========
   Service Status Further Meaning                   Status Code
   ============== ================================= ===========
   Success        Film session successfully created 0000
   Warning        Memory allocation not supported   B600
   ============== ================================= ===========

.. note::

   The status code "0106H" (Invalid Attribute Value) indicates that the
   requested memory allocation can not be provided; the status code
   "0213H" (Resource limitation) indicates that the requested allocation
   can temporarily not be provided.

.. _sect_H.4.1.2.1.3:

Behavior
        

The SCU uses the N-CREATE to request the SCP to create a Basic Film
Session SOP Instance. The SCU shall initialize Attributes of the SOP
Class as specified in `Usage Specifications <#sect_H.2.4>`__.

The SCP shall create the SOP Instance and shall initialize Attributes of
the SOP Class as specified in `Usage Specifications <#sect_H.2.4>`__.

The SCP shall return the status code of the requested SOP Instance
creation. The meaning of success, warning, and failure status codes is
defined in `Status Code Categories <#sect_H.2.5>`__.

The Basic Film Session SOP Instances shall be created before the Film
Box SOP Instances are created.

At any time the SCU/SCP shall only support one Basic Film Session SOP
Instance on an Association.

.. note::

   Multiple film sessions may be handled by establishing multiple
   Associations.

Terminating the Association will effectively perform an N-DELETE on an
opened film session. See Note in `Behavior <#sect_H.4.1.2.3.2>`__.

.. _sect_H.4.1.2.2:

N-SET
'''''

The N-SET may be used to update an instance of the Basic Film Session
SOP Class.

.. _sect_H.4.1.2.2.1:

Attributes
          

All Attributes and usage in `table_title <#table_H.4-2>`__ apply to
N-SET.

.. _sect_H.4.1.2.2.2:

Status
      

The status values that are specific for this SOP Class are defined in
`Status <#sect_H.4.1.2.1.2>`__.

.. _sect_H.4.1.2.2.3:

Behavior
        

The SCU uses the N-SET to request the SCP to update a Basic Film Session
SOP Instance. The SCU shall specify the SOP Instance UID to be updated
and shall specify the list of Attributes for which the Attribute Values
are to be set.

The SCP shall set new values for the specified Attributes of the
specified SOP Instance.

The SCP shall return the status code of the requested SOP Instance
update. The meaning of success, warning, and failure status codes is
defined in `Status Code Categories <#sect_H.2.5>`__

.. _sect_H.4.1.2.3:

N-DELETE
''''''''

The N-DELETE is used to delete the complete Basic Film Session SOP
Instance hierarchy. As a result, all references to Image SOP Instances
within the film session are deleted.

The Basic Film Session SOP Instance hierarchy consists of one Basic Film
Session SOP Instance, one or more Basic Film Box SOP Instances, one or
more Image Box SOP Instances, zero or more Basic Annotation Box SOP
Instances, zero or more Presentation LUT SOP Instances, and zero or more
Basic Print Image Overlay Box SOP instances.

.. note::

   The Basic Film Session SOP Instance hierarchy can be visualized as a
   reversed tree with the Basic Film Session SOP Instance as the root
   and the Image Box SOP Instances as the leaves.

.. _sect_H.4.1.2.3.1:

Status
      

There are no specific status codes. See for response status codes.

.. _sect_H.4.1.2.3.2:

Behavior
        

The SCU uses the N-DELETE to request the SCP to delete the Basic Film
Session SOP Instance hierarchy. The SCU shall specify in the N-DELETE
request primitive of the SOP Instance UID of the Basic Film Session
(root).

The SCP shall delete the specified SOP Instance hierarchy.

The SCP shall not delete SOP Instances in the hierarchy as long as there
are outstanding references to these SOP Instances

.. note::

   It is beyond the scope of the Standard to specify when the SCP
   actually deletes SOP Instances with outstanding references.

The SCP shall return the status code of the requested SOP Instance
deletion. The meaning of success, warning, and failure status codes is
defined in `Status Code Categories <#sect_H.2.5>`__.

.. _sect_H.4.1.2.4:

N-ACTION
''''''''

The N-ACTION is used to print the film session; i.e., to print all the
films that belong to the film session.

If multiple copies of the film session have been requested, the SCP
shall collate the copies. This means that if two copies of four films
has been specified, the printed sequence is 12341234.

.. _sect_H.4.1.2.4.1:

Attributes
          

The arguments of the N-ACTION are defined in
`table_title <#table_H.4-3>`__.

The Action Reply argument is encoded as a DICOM Data Set. The Data Set
only contains the Attribute Referenced Print Job Sequence (2100,0500),
which includes the Referenced SOP Class UID (0008,1150) and the
Referenced SOP Instance UID (0008,1155).

If the SCP supports the Print Job SOP Class, the Action Reply argument
is contained in the N-ACTION response. Otherwise, the Action Reply is
not contained in the N-ACTION response.

.. table:: N-ACTION Arguments

   +-------------+-------------+-------------+-------------+-------------+
   | Action Type | Action Type | Attribute   | Tag         | Usage       |
   | Name        | ID          | Name        |             | SCU/SCP     |
   +=============+=============+=============+=============+=============+
   | Print       | 1           | Referenced  | (2100,0500) | -/MC        |
   |             |             | Print Job   |             |             |
   |             |             | Sequence    |             | Required if |
   |             |             |             |             | Print Job   |
   |             |             |             |             | SOP is      |
   |             |             |             |             | supported   |
   +-------------+-------------+-------------+-------------+-------------+
   |             |             | >Referenced | (0008,1150) | -/MC        |
   |             |             | SOP Class   |             |             |
   |             |             | UID         |             | Required if |
   |             |             |             |             | Referenced  |
   |             |             |             |             | Print Job   |
   |             |             |             |             | Sequence    |
   |             |             |             |             | (2100,0500) |
   |             |             |             |             | is present  |
   +-------------+-------------+-------------+-------------+-------------+
   |             |             | >Referenced | (0008,1155) | -/MC        |
   |             |             | SOP         |             |             |
   |             |             | Instance    |             | Required if |
   |             |             | UID         |             | Referenced  |
   |             |             |             |             | Print Job   |
   |             |             |             |             | Sequence    |
   |             |             |             |             | (2100,0500) |
   |             |             |             |             | is present  |
   +-------------+-------------+-------------+-------------+-------------+

.. _sect_H.4.1.2.4.2:

Status
      

`table_title <#table_H.4-4>`__\ defines the specific status code values
that may be returned in a N-ACTION response. See for additional response
status codes.

.. table:: SOP Class Status Values

   +--------------------------+--------------------------+-------------+
   | Service Status           | Further Meaning          | Status Code |
   +==========================+==========================+=============+
   | Success                  | Film belonging to the    | 0000        |
   |                          | film session are         |             |
   |                          | accepted for printing;   |             |
   |                          | if supported, the Print  |             |
   |                          | Job SOP Instance is      |             |
   |                          | created                  |             |
   +--------------------------+--------------------------+-------------+
   | Warning                  | Film session printing    | B601        |
   |                          | (collation) is not       |             |
   |                          | supported                |             |
   +--------------------------+--------------------------+-------------+
   | Film Session SOP         | B602                     |             |
   | Instance hierarchy does  |                          |             |
   | not contain Image Box    |                          |             |
   | SOP Instances (empty     |                          |             |
   | page)                    |                          |             |
   +--------------------------+--------------------------+-------------+
   | Image size is larger     | B604                     |             |
   | than image box size, the |                          |             |
   | image has been           |                          |             |
   | demagnified.             |                          |             |
   +--------------------------+--------------------------+-------------+
   | Image size is larger     | B609                     |             |
   | than the Image Box size. |                          |             |
   | The Image has been       |                          |             |
   | cropped to fit.          |                          |             |
   +--------------------------+--------------------------+-------------+
   | Image size or Combined   | B60A                     |             |
   | Print Image size is      |                          |             |
   | larger than the Image    |                          |             |
   | Box size. Image or       |                          |             |
   | Combined Print Image has |                          |             |
   | been decimated to fit.   |                          |             |
   +--------------------------+--------------------------+-------------+
   | Failure                  | Failed: Film Session SOP | C600        |
   |                          | Instance hierarchy does  |             |
   |                          | not contain Film Box SOP |             |
   |                          | Instances                |             |
   +--------------------------+--------------------------+-------------+
   | Failed: Unable to create | C601                     |             |
   | Print Job SOP Instance;  |                          |             |
   | print queue is full      |                          |             |
   +--------------------------+--------------------------+-------------+
   | Failed: Image size is    | C603                     |             |
   | larger than image box    |                          |             |
   | size                     |                          |             |
   +--------------------------+--------------------------+-------------+
   | Failed: Combined Print   | C613                     |             |
   | Image size is larger     |                          |             |
   | than the Image Box size  |                          |             |
   +--------------------------+--------------------------+-------------+

.. note::

   Previous versions of the DICOM Standard defined the status code of
   C604. This code was specified for the case of an image position
   collision. Since image position collision is not a possible state,
   the code has been retired.

.. _sect_H.4.1.2.4.3:

Behavior
        

The SCU uses the N-ACTION to request the SCP to print all the films
belonging to the identified film session.

The SCP shall make a copy of the "working" Basic Film Session SOP
Instance hierarchy, which contains all the information to control the
Print Process. Hence the SCU may further update the "working" SOP
Instance hierarchy without affecting the result of previous print
requests. The execution of the Print Process is monitored by the Print
Job SOP Instance (if supported by the SCP) and the Printer SOP Class.

If the SCP supports the Print Job SOP Class then the SCP shall create a
Print Job SOP Instance, which contains the copy of the "working" Basic
Film Session SOP Instance hierarchy and shall return the Print Job SOP
Class/Instance UID pair in the Attribute Referenced Print Job Sequence
of the Action Reply argument.

.. note::

   If the SCP supports the Print Job SOP Class, it creates a single
   Print Job for all the films of the film session.

The SCP shall return the status code of the requested operation. The
meaning of success, warning, and failure status codes is defined in
`Status Code Categories <#sect_H.2.5>`__.

The N-ACTION shall be issued only if the Basic Film Session SOP Instance
hierarchy contains at least one Film Box SOP Instance.

.. _sect_H.4.1.3:

SOP Class Definition and UID
^^^^^^^^^^^^^^^^^^^^^^^^^^^^

The Basic Film Session SOP Class UID shall have the value
"1.2.840.10008.5.1.1.1".

.. _sect_H.4.2:

Basic Film Box SOP Class
~~~~~~~~~~~~~~~~~~~~~~~~

.. _sect_H.4.2.1:

IOD Description
^^^^^^^^^^^^^^^

The Basic Film Box IOD is an abstraction of the presentation of one film
of the film session. The Basic Film Box IOD describes the presentation
parameters that are common for all images on a given sheet of film.

The Basic Film Box SOP Instance refers to one or more Image Box SOP
Instances, zero or more film related Annotation Box SOP Instances, and
zero or one Presentation LUT SOP Instance.

.. _sect_H.4.2.2:

DIMSE Service Group
^^^^^^^^^^^^^^^^^^^

`table_title <#table_H.4-5>`__ shows DIMSE Services applicable to the
IOD.

.. table:: DIMSE Service Group Applicable to Basic Film Box

   ============================= =============
   DICOM Message Service Element Usage SCU/SCP
   ============================= =============
   N-CREATE                      M/M
   N-ACTION                      M/M
   N-DELETE                      U/M
   N-SET                         U/U
   ============================= =============

The meaning of the Usage SCU/SCP is described in `Usage
Specifications <#sect_H.2.4>`__.

This Section describes the behavior of the DIMSE Services that are
specific for this IOD. The general behavior of the DIMSE Services is
specified in .

.. _sect_H.4.2.2.1:

N-CREATE
''''''''

The N-CREATE is used to create an instance of the Basic Film Box SOP
Class.

.. _sect_H.4.2.2.1.1:

Attributes
          

The Attribute list of the N-CREATE is shown in
`table_title <#table_H.4-6>`__.

.. table:: N-CREATE Attribute List

   +--------------------------+-------------+--------------------------+
   | Attribute Name           | Tag         | Usage SCU/SCP            |
   +==========================+=============+==========================+
   | Image Display Format     | (2010,0010) | M/M                      |
   +--------------------------+-------------+--------------------------+
   | Referenced Film Session  | (2010,0500) | M/M                      |
   | Sequence                 |             |                          |
   +--------------------------+-------------+--------------------------+
   | >Referenced SOP Class    | (0008,1150) | M/M                      |
   | UID                      |             |                          |
   +--------------------------+-------------+--------------------------+
   | >Referenced SOP Instance | (0008,1155) | M/M                      |
   | UID                      |             |                          |
   +--------------------------+-------------+--------------------------+
   | Referenced Image Box     | (2010,0510) | -/M                      |
   | Sequence                 |             |                          |
   +--------------------------+-------------+--------------------------+
   | >Referenced SOP Class    | (0008,1150) | -/M                      |
   | UID                      |             |                          |
   +--------------------------+-------------+--------------------------+
   | >Referenced SOP Instance | (0008,1155) | -/M                      |
   | UID                      |             |                          |
   +--------------------------+-------------+--------------------------+
   | Referenced Basic         | (2010,0520) | -/MC                     |
   | Annotation Box Sequence  |             |                          |
   |                          |             | (Required if optional    |
   |                          |             | Annotation SOP was       |
   |                          |             | negotiated)              |
   +--------------------------+-------------+--------------------------+
   | >Referenced SOP Class    | (0008,1150) | -/MC                     |
   | UID                      |             |                          |
   |                          |             | (Required if sequence is |
   |                          |             | present)                 |
   +--------------------------+-------------+--------------------------+
   | >Referenced SOP Instance | (0008,1155) | -/MC                     |
   | UID                      |             |                          |
   |                          |             | (Required if sequence is |
   |                          |             | present)                 |
   +--------------------------+-------------+--------------------------+
   | Film Orientation         | (2010,0040) | U/M                      |
   +--------------------------+-------------+--------------------------+
   | Film Size ID             | (2010,0050) | U/M                      |
   +--------------------------+-------------+--------------------------+
   | Magnification Type       | (2010,0060) | U/M                      |
   +--------------------------+-------------+--------------------------+
   | Max Density              | (2010,0130) | U/M                      |
   +--------------------------+-------------+--------------------------+
   | Configuration            | (2010,0150) | U/M                      |
   | Information              |             |                          |
   +--------------------------+-------------+--------------------------+
   | Referenced Presentation  | (2050,0500) | U/MC                     |
   | LUT Sequence             |             |                          |
   |                          |             | (Required if             |
   |                          |             | Presentation LUT is      |
   |                          |             | supported)               |
   +--------------------------+-------------+--------------------------+
   | >Referenced SOP Class    | (0008,1150) | U/MC                     |
   | UID                      |             |                          |
   |                          |             | (Required if sequence is |
   |                          |             | present)                 |
   +--------------------------+-------------+--------------------------+
   | >Referenced SOP Instance | (0008,1155) | U/MC                     |
   | UID                      |             |                          |
   |                          |             | (Required if sequence is |
   |                          |             | present)                 |
   +--------------------------+-------------+--------------------------+
   | Annotation Display       | (2010,0030) | U/U                      |
   | Format ID                |             |                          |
   +--------------------------+-------------+--------------------------+
   | Smoothing Type           | (2010,0080) | U/U                      |
   +--------------------------+-------------+--------------------------+
   | Border Density           | (2010,0100) | U/U                      |
   +--------------------------+-------------+--------------------------+
   | Empty Image Density      | (2010,0110) | U/U                      |
   +--------------------------+-------------+--------------------------+
   | Min Density              | (2010,0120) | U/U                      |
   +--------------------------+-------------+--------------------------+
   | Trim                     | (2010,0140) | U/U                      |
   +--------------------------+-------------+--------------------------+
   | Illumination             | (2010,015E) | U/MC                     |
   |                          |             |                          |
   |                          |             | (Required if             |
   |                          |             | Presentation LUT is      |
   |                          |             | supported)               |
   +--------------------------+-------------+--------------------------+
   | Reflected Ambient Light  | (2010,0160) | U/MC                     |
   |                          |             |                          |
   |                          |             | (Required if             |
   |                          |             | Presentation LUT is      |
   |                          |             | supported)               |
   +--------------------------+-------------+--------------------------+
   | Requested Resolution ID  | (2020,0050) | U/U                      |
   +--------------------------+-------------+--------------------------+
   | ICC Profile              | (0028,2000) | U/U                      |
   +--------------------------+-------------+--------------------------+

The meaning of the Usage SCU/SCP is described in `Usage
Specifications <#sect_H.2.4>`__.

If the Illumination (2010,015E) and Reflected Ambient Light (2010,0160)
values, respectively termed L0 and La, are not created, the following
default values are recommended for grayscale printing:

-  For transmissive film: L0 = 2000 cd/m\ :sup:`2`. La = 10
   cd/m\ :sup:`2`.

-  For reflective media: L0 = 150 cd/m\ :sup:`2`.

The ICC Profile (0028,2000) Attribute shall only be used to describe the
color space of images for color printing, i.e., in conjunction with the
Basic Color Image Box SOP Class. It shall not be used with the Basic
Grayscale Image Box SOP Class.

.. _sect_H.4.2.2.1.2:

Status
      

`table_title <#table_H.4.2.2.1.2-1>`__ defines the specific status code
values that may be returned in a N-CREATE or N-SET response for this SOP
Class. See for additional response status codes of N-CREATE and N-SET
DIMSE Services.

.. table:: Status Values for Basic Film Box SOP Class

   +----------------+-------------------------------------+-------------+
   | Service Status | Further Meaning                     | Status Code |
   +================+=====================================+=============+
   | Success        | Film Box successfully created       | 0000        |
   +----------------+-------------------------------------+-------------+
   | Warning        | Requested Min Density or Max        | B605        |
   |                | Density outside of printer's        |             |
   |                | operating range. The printer will   |             |
   |                | use its respective minimum or       |             |
   |                | maximum density value instead.      |             |
   +----------------+-------------------------------------+-------------+
   | Failure        | Failed: There is an existing Film   | C616        |
   |                | Box that has not been printed and   |             |
   |                | N-ACTION at the Film Session level  |             |
   |                | is not supported. A new Film Box    |             |
   |                | will not be created when a previous |             |
   |                | Film Box has not been printed.      |             |
   +----------------+-------------------------------------+-------------+

.. _sect_H.4.2.2.1.3:

Behavior
        

The SCU uses the N-CREATE to request the SCP to create a Basic Film Box
SOP Instance. The SCU shall initialize Attributes of the SOP Class as
specified in `Usage Specifications <#sect_H.2.4>`__.

The SCP shall create the SOP Instance and shall initialize Attributes of
the SOP Class as specified in `Usage Specifications <#sect_H.2.4>`__.

.. note::

   If there exists a Film Box SOP Instance that has not been printed and
   the SCP does not support N-ACTION on the Film Session, then the SCP
   should fail the N-CREATE of the new SOP Instance.

Upon the creation of the Basic Film Box SOP Instance, the SCP shall
append the SOP Class/Instance UID pair of the created Basic Film Box SOP
Instance to the Attribute Referenced Film Box Sequence (2000,0500) of
the parent Basic Film Session SOP Instance to link the Basic Film Box
SOP Instance to the Basic Film Session SOP Instance.

The SCP shall create Image Box SOP Instances of the appropriate Image
Box SOP Class for each image box as defined by the Attribute Image
Display Format (2010,0010). The SOP Class of the created Image Box SOP
Instance depends on the Meta SOP Class context. For example the
Grayscale Image Box SOP Class is related to the Basic Grayscale Print
Management Meta SOP Class. The Meta SOP Class context is conveyed by the
Presentation Context ID that corresponds with the Meta SOP Class and is
defined at Association setup.

The SCP shall append the SOP Class/Instance UID pair of the created
Image Box SOP Instance to the Referenced Image Box Sequence Attribute of
the parent Basic Film Box SOP Instance to link each Image Box SOP
Instance to the Basic Film Box SOP Instance. The SCP returns the list of
Image Box SOP Class/Instance UID pairs in the Attribute Referenced Image
Box Sequence (2010,0510) of the N-CREATE response message.

If supported, the SCP shall create Basic Annotation Box SOP Instances
for each Annotation Box defined by the Attribute Annotation Display
Format ID and shall append the SOP Class/Instance UID pair of the
created Basic Annotation Box SOP Instance to the Referenced Annotation
Box Sequence Attribute of the parent Basic Film Box SOP Instance to link
each Basic Annotation Box SOP Instance to the Basic Film Box SOP
Instance. The SCP returns the list of Basic Annotation Box SOP
Class/Instance UID pairs in the Attribute Referenced Annotation Box
Sequence of the N-CREATE response message. The Annotation Boxes shall
support the same character sets as the Basic Film Box.

The character set supported by the Film Box shall be the same as the
character set of the Basic Film Session.

The SCP shall return the status code of the requested SOP Instance
creation. The meaning of success, warning, and failure status codes is
defined in `Status Code Categories <#sect_H.2.5>`__.

.. _sect_H.4.2.2.2:

N-SET
'''''

The N-SET may be used to update the last created instance of the Basic
Film Box SOP Class.

.. _sect_H.4.2.2.2.1:

Attributes
          

The Attributes that may be updated are shown in
`table_title <#table_H.4-7>`__.

.. table:: N-SET Attributes

   +--------------------------+-------------+--------------------------+
   | Attribute Name           | Tag         | Usage SCU/SCP            |
   +==========================+=============+==========================+
   | Magnification Type       | (2010,0060) | U/M                      |
   +--------------------------+-------------+--------------------------+
   | Max Density              | (2010,0130) | U/M                      |
   +--------------------------+-------------+--------------------------+
   | Configuration            | (2010,0150) | U/M                      |
   | Information              |             |                          |
   +--------------------------+-------------+--------------------------+
   | Referenced Presentation  | (2050,0500) | U/MC                     |
   | LUT Sequence             |             |                          |
   |                          |             | (Required if             |
   |                          |             | Presentation LUT is      |
   |                          |             | supported)               |
   +--------------------------+-------------+--------------------------+
   | >Referenced SOP Class    | (0008,1150) | U/MC                     |
   | UID                      |             |                          |
   |                          |             | (Required if sequence is |
   |                          |             | present)                 |
   +--------------------------+-------------+--------------------------+
   | >Referenced SOP Instance | (0008,1155) | U/MC                     |
   | UID                      |             |                          |
   |                          |             | (Required if sequence is |
   |                          |             | present)                 |
   +--------------------------+-------------+--------------------------+
   | Smoothing Type           | (2010,0080) | U/U                      |
   +--------------------------+-------------+--------------------------+
   | Border Density           | (2010,0100) | U/U                      |
   +--------------------------+-------------+--------------------------+
   | Empty Image Density      | (2010,0110) | U/U                      |
   +--------------------------+-------------+--------------------------+
   | Min Density              | (2010,0120) | U/U                      |
   +--------------------------+-------------+--------------------------+
   | Trim                     | (2010,0140) | U/U                      |
   +--------------------------+-------------+--------------------------+
   | Illumination             | (2010,015E) | U/MC                     |
   |                          |             |                          |
   |                          |             | (Required if             |
   |                          |             | Presentation LUT is      |
   |                          |             | supported)               |
   +--------------------------+-------------+--------------------------+
   | Reflected Ambient Light  | (2010,0160) | U/MC                     |
   |                          |             |                          |
   |                          |             | (Required if             |
   |                          |             | Presentation LUT is      |
   |                          |             | supported)               |
   +--------------------------+-------------+--------------------------+
   | ICC Profile              | (0028,2000) | U/U                      |
   +--------------------------+-------------+--------------------------+

The meaning of the Usage SCU/SCP is described in `Usage
Specifications <#sect_H.2.4>`__.

.. _sect_H.4.2.2.2.2:

Status
      

The status values that are specific for this SOP Class are defined in
`Status <#sect_H.4.2.2.1.2>`__.

.. _sect_H.4.2.2.2.3:

Behavior
        

The SCU uses the N-SET to request the SCP to update a Basic Film Box SOP
Instance. The SCU shall only specify the SOP Instance UID of the last
created Basic Film Box SOP Instance in the N-SET request primitive, and
shall specify the list of Attributes for which the Attribute Values are
to be set.

The SCP shall set new values for the specified Attributes of the
specified SOP Instance.

The SCP shall return the status code of the requested SOP Instance
update. The meaning of success, warning, and failure status codes is
defined in `Status Code Categories <#sect_H.2.5>`__.

.. _sect_H.4.2.2.3:

N-DELETE
''''''''

The N-DELETE is used to delete the last created Basic Film Box SOP
Instance hierarchy. As a result all the information describing the last
film is deleted.

The Basic Film Box SOP Instance hierarchy consists of one Basic Film Box
SOP Instance, one or more Image Box SOP Instances, zero or more Basic
Annotation Box SOP Instances, zero or more Presentation LUT SOP
Instances, and zero or more Basic Print Image Overlay Box SOP instances.

.. note::

   There is no provision in the DICOM Standard to delete previously
   created Film Box SOP Instances.

.. _sect_H.4.2.2.3.1:

Behavior
        

The SCU uses the N-DELETE to request the SCP to delete the Basic Film
Box SOP Instance hierarchy. The SCU shall specify in the N-DELETE
request primitive the SOP Instance UID of the last created Basic Film
Box (root).

The SCP shall delete the specified SOP Instance hierarchy and shall
remove the UID of the deleted Basic Film Box SOP Instance from the list
of SOP Instance UIDs of the Film Box UIDs Attribute of the parent Basic
Film Session SOP Instance.

The SCP shall return the status code of the requested SOP Instance
hierarchy deletion. The meaning of success, warning, and failure status
codes is defined in `Status Code Categories <#sect_H.2.5>`__.

The SCP shall not delete SOP Instances in the hierarchy as long as there
are outstanding references to these SOP Instances

.. note::

   It is beyond the scope of the Standard to specify when the SCP
   actually deletes the Image SOP Instances with outstanding references.

.. _sect_H.4.2.2.3.2:

Status
      

There are no specific status codes. See for response status codes.

.. _sect_H.4.2.2.4:

N-ACTION
''''''''

The N-ACTION is used to print one or more copies of the last created
instance of the Film Box.

.. _sect_H.4.2.2.4.1:

Attributes
          

The arguments of the N-ACTION are defined as shown in
`table_title <#table_H.4-8>`__.

The Action Reply argument is encoded as a DICOM Data Set. The Data Set
only contains the Attribute Referenced Print Job Sequence (2100,0500),
which includes the Referenced SOP Class UID (0008,1150) and the
Referenced SOP Instance UID (0008,1155).

If the SCP supports the Print Job SOP Class, the Action Reply argument
is contained in the N-ACTION response. Otherwise, the Action Reply is
not contained in the N-ACTION response.

.. table:: N-ACTION Arguments

   +-------------+-------------+-------------+-------------+-------------+
   | Action Type | Action Type | Attribute   | Tag         | Usage       |
   | Name        | ID          | Name        |             | SCU/SCP     |
   +=============+=============+=============+=============+=============+
   | Print       | 1           | Referenced  | (2100,0500) | -/MC        |
   |             |             | Print Job   |             |             |
   |             |             | Sequence    |             | Required if |
   |             |             |             |             | Print Job   |
   |             |             |             |             | SOP is      |
   |             |             |             |             | supported   |
   +-------------+-------------+-------------+-------------+-------------+
   |             |             | >Referenced | (0008,1150) | -/MC        |
   |             |             | SOP Class   |             |             |
   |             |             | UID         |             | Required if |
   |             |             |             |             | Referenced  |
   |             |             |             |             | Print Job   |
   |             |             |             |             | Sequence    |
   |             |             |             |             | (2100,0500) |
   |             |             |             |             | is present  |
   +-------------+-------------+-------------+-------------+-------------+
   |             |             | >Referenced | (0008,1155) | -/MC        |
   |             |             | SOP         |             |             |
   |             |             | Instance    |             | Required if |
   |             |             | UID         |             | Referenced  |
   |             |             |             |             | Print Job   |
   |             |             |             |             | Sequence    |
   |             |             |             |             | (2100,0500) |
   |             |             |             |             | is present  |
   +-------------+-------------+-------------+-------------+-------------+

.. _sect_H.4.2.2.4.2:

Status
      

`table_title <#table_H.4-9>`__ defines the specific status code values
that may be returned in a N-ACTION response. See for additional response
status codes.

.. table:: Status Values

   +--------------------------+--------------------------+-------------+
   | Service Status           | Further Meaning          | Status Code |
   +==========================+==========================+=============+
   | Success                  | Film accepted for        | 0000        |
   |                          | printing; if supported,  |             |
   |                          | the Print Job SOP        |             |
   |                          | Instance is created      |             |
   +--------------------------+--------------------------+-------------+
   | Warning                  | Film Box SOP Instance    | B603        |
   |                          | hierarchy does not       |             |
   |                          | contain Image Box SOP    |             |
   |                          | Instances (empty page)   |             |
   +--------------------------+--------------------------+-------------+
   | Image size is larger     | B604                     |             |
   | than image box size, the |                          |             |
   | image has been           |                          |             |
   | demagnified.             |                          |             |
   +--------------------------+--------------------------+-------------+
   | Image size is larger     | B609                     |             |
   | than the Image Box size. |                          |             |
   | The Image has been       |                          |             |
   | cropped to fit.          |                          |             |
   +--------------------------+--------------------------+-------------+
   | Image size or Combined   | B60A                     |             |
   | Print Image size is      |                          |             |
   | larger than the Image    |                          |             |
   | Box size. Image or       |                          |             |
   | Combined Print Image has |                          |             |
   | been decimated to fit.   |                          |             |
   +--------------------------+--------------------------+-------------+
   | Failure                  | Failed: Unable to create | C602        |
   |                          | Print Job SOP Instance;  |             |
   |                          | print queue is full      |             |
   +--------------------------+--------------------------+-------------+
   | Failed: Image size is    | C603                     |             |
   | larger than image box    |                          |             |
   | size                     |                          |             |
   +--------------------------+--------------------------+-------------+
   | Failed: Combined Print   | C613                     |             |
   | Image size is larger     |                          |             |
   | than the Image Box size  |                          |             |
   +--------------------------+--------------------------+-------------+

.. note::

   Previous versions of the DICOM Standard defined the status code of
   C604. This code was specified for the case of an image position
   collision. Since image position collision is not a possible state,
   the code has been retired.

.. _sect_H.4.2.2.4.3:

Behavior
        

The SCU uses the N-ACTION to request the SCP to print one or more copies
of a single film of the film session. The SCU shall only specify the SOP
Instance UID of the last created Basic Film Box SOP Instance in the
N-ACTION request primitive.

The SCP shall make a copy of the "working" Basic Film Session SOP
Instance and the "working" Basic Film Box SOP Instance hierarchy, which
contains all the information to control the Print Process. Hence the SCU
may further update the "working" SOP Instances without affecting the
result of previous print requests. The execution of the Print Process is
monitored by the Print Job SOP Class (if supported by the SCP) and the
Printer SOP Class.

If the SCP supports the Print Job SOP Class then the SCP shall create a
Print Job SOP Instance, which contains the copy of the "working" Basic
Film Session SOP Instance hierarchy and shall return the Print Job SOP
Class/Instance UID pair in the Attribute Referenced Print Job Sequence
of the Action Reply argument.

The SCP shall return the status code of the requested operation. The
meaning of success, warning, and failure status codes is defined in
`Status Code Categories <#sect_H.2.5>`__.

.. _sect_H.4.2.3:

SOP Class Definition and UID
^^^^^^^^^^^^^^^^^^^^^^^^^^^^

The Basic Film Box SOP Class UID shall have the value
"1.2.840.10008.5.1.1.2".

.. _sect_H.4.3:

Image Box SOP Classes
~~~~~~~~~~~~~~~~~~~~~

.. _sect_H.4.3.1:

Basic Grayscale Image Box SOP Class
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

.. _sect_H.4.3.1.1:

IOD Description
'''''''''''''''

The Basic Image Box IOD is an abstraction of the presentation of an
image and image related data in the image area of a film. The Basic
Image Box IOD describes the presentation parameters and image pixel data
that apply to a single image of a sheet of film.

The Basic Grayscale Image Box SOP Instance is created by the SCP at the
time the Basic Film Box SOP Instance is created, based on the value of
the Basic Film Box Attribute Image Display Format (2010,0010).

The Basic Grayscale Image Box SOP Instance refers to zero or one Image
Overlay Box SOP Instance and zero or one Presentation LUT SOP Instance.

.. _sect_H.4.3.1.2:

DIMSE Service Group
'''''''''''''''''''

The DIMSE Services applicable to the IOD are shown below.

.. table:: DIMSE Service Group Applicable to Basic Grayscale Image Box

   ============================= =============
   DICOM Message Service Element Usage SCU/SCP
   ============================= =============
   N-SET                         M/M
   ============================= =============

The meaning of the Usage SCU/SCP is described in `Usage
Specifications <#sect_H.2.4>`__.

.. note::

   There is no N-CREATE because Instances of the Basic Grayscale Image
   Box SOP Class are created by the SCP as a result of the N-CREATE of
   the Film Box SOP Instance.

This Section describes the behavior of the DIMSE Services that are
specific for this IOD. The general behavior of the DIMSE Services is
specified in .

.. _sect_H.4.3.1.2.1:

N-SET
     

The N-SET may be used to update an instance of the Basic Grayscale Image
Box SOP Class.

.. _sect_H.4.3.1.2.1.1:

Attributes
          

The Attributes that may be updated are shown in
`table_title <#table_H.4-10>`__.

.. table:: N-SET Attributes

   +--------------------------+-------------+--------------------------+
   | Attribute Name           | Tag         | Usage SCU/SCP            |
   +==========================+=============+==========================+
   | Image Box Position       | (2020,0010) | M/M                      |
   +--------------------------+-------------+--------------------------+
   | Basic Grayscale Image    | (2020,0110) | M/M                      |
   | Sequence                 |             |                          |
   +--------------------------+-------------+--------------------------+
   | >Samples Per Pixel       | (0028,0002) | M/M                      |
   +--------------------------+-------------+--------------------------+
   | >Photometric             | (0028,0004) | M/M                      |
   | Interpretation           |             |                          |
   +--------------------------+-------------+--------------------------+
   | >Rows                    | (0028,0010) | M/M                      |
   +--------------------------+-------------+--------------------------+
   | >Columns                 | (0028,0011) | M/M                      |
   +--------------------------+-------------+--------------------------+
   | >Pixel Aspect Ratio      | (0028,0034) | MC/M                     |
   |                          |             |                          |
   |                          |             | (Required if the aspect  |
   |                          |             | ration is not 1\1)       |
   +--------------------------+-------------+--------------------------+
   | >Bits Allocated          | (0028,0100) | M/M                      |
   +--------------------------+-------------+--------------------------+
   | >Bits Stored             | (0028,0101) | M/M                      |
   +--------------------------+-------------+--------------------------+
   | >High Bit                | (0028,0102) | M/M                      |
   +--------------------------+-------------+--------------------------+
   | >Pixel Representation    | (0028,0103) | M/M                      |
   +--------------------------+-------------+--------------------------+
   | >Pixel Data              | (7FE0,0010) | M/M                      |
   +--------------------------+-------------+--------------------------+
   | Polarity                 | (2020,0020) | U/M                      |
   +--------------------------+-------------+--------------------------+
   | Magnification Type       | (2010,0060) | U/U                      |
   +--------------------------+-------------+--------------------------+
   | Smoothing Type           | (2010,0080) | U/U                      |
   +--------------------------+-------------+--------------------------+
   | Min Density              | (2010,0120) | U/U                      |
   +--------------------------+-------------+--------------------------+
   | Max Density              | (2010,0130) | U/U                      |
   +--------------------------+-------------+--------------------------+
   | Configuration            | (2010,0150) | U/U                      |
   | Information              |             |                          |
   +--------------------------+-------------+--------------------------+
   | Requested Image Size     | (2020,0030) | U/U                      |
   +--------------------------+-------------+--------------------------+
   | Requested Decimate/Crop  | (2020,0040) | U/U                      |
   | Behavior                 |             |                          |
   +--------------------------+-------------+--------------------------+
   | Referenced Presentation  | (2050,0500) | U/U                      |
   | LUT Sequence             |             |                          |
   +--------------------------+-------------+--------------------------+
   | >Referenced SOP Class    | (0008,1150) | U/U                      |
   | UID                      |             |                          |
   +--------------------------+-------------+--------------------------+
   | >Referenced SOP Instance | (0008,1155) | U/U                      |
   | UID                      |             |                          |
   +--------------------------+-------------+--------------------------+

The meaning of the Usage SCU/SCP is described in `Usage
Specifications <#sect_H.2.4>`__.

The values of Magnification Type (2010,0060) and Smoothing Type
(2010,0080) of a particular image box override the values of
Magnification Type and Smoothing Type of the film box.

Values for Referenced Presentation LUT Sequence override any
Presentation LUT that may have been set at the Basic Film Box. Values
for Min/Max Density override any Density values that may have been set
at the Basic Film Box.

.. _sect_H.4.3.1.2.1.2:

Status
      

`table_title <#table_H.4.3.1.2.1.2-1>`__ defines the specific status
code values that may be returned in a N-SET response. See for additional
response status codes.

.. table:: Status Values for Basic Grayscale Image Box SOP Class

   +--------------------------+--------------------------+-------------+
   | Service Status           | Further Meaning          | Status Code |
   +==========================+==========================+=============+
   | Success                  | Image successfully       | 0000        |
   |                          | stored in Image Box      |             |
   +--------------------------+--------------------------+-------------+
   | Warning                  | Image size larger than   | B604        |
   |                          | image box size, the      |             |
   |                          | image has been           |             |
   |                          | demagnified.             |             |
   +--------------------------+--------------------------+-------------+
   | Requested Min Density or | B605                     |             |
   | Max Density outside of   |                          |             |
   | printer's operating      |                          |             |
   | range. The printer will  |                          |             |
   | use its respective       |                          |             |
   | minimum or maximum       |                          |             |
   | density value instead.   |                          |             |
   +--------------------------+--------------------------+-------------+
   | Image size is larger     | B609                     |             |
   | than the Image Box size. |                          |             |
   | The Image has been       |                          |             |
   | cropped to fit.          |                          |             |
   +--------------------------+--------------------------+-------------+
   | Image size or Combined   | B60A                     |             |
   | Print Image size is      |                          |             |
   | larger than the Image    |                          |             |
   | Box size. The Image or   |                          |             |
   | Combined Print Image has |                          |             |
   | been decimated to fit.   |                          |             |
   +--------------------------+--------------------------+-------------+
   | Failure                  | Failed: Image size is    | C603        |
   |                          | larger than image box    |             |
   |                          | size                     |             |
   +--------------------------+--------------------------+-------------+
   | Failed: Insufficient     | C605                     |             |
   | memory in printer to     |                          |             |
   | store the image          |                          |             |
   +--------------------------+--------------------------+-------------+
   | Failed: Combined Print   | C613                     |             |
   | Image size is larger     |                          |             |
   | than the Image Box size  |                          |             |
   +--------------------------+--------------------------+-------------+

.. _sect_H.4.3.1.2.1.3:

Behavior
        

The SCU uses the N-SET to request the SCP to update a Basic Grayscale
Image Box SOP Instance. The SCU shall only specify the SOP Instance UID
of a Basic Grayscale Image Box belonging to the last created Film Box
SOP Instance and shall specify the list of Attributes for which the
Attribute Values are to be set.

To instruct the SCP to erase the image in the image position, the SCU
shall set a zero length and no value in the Attribute Basic Grayscale
Image Sequence (2020,0110).

The SCP shall set new values for the specified Attributes of the
specified SOP Instance.

.. note::

   The image in this N-SET supersedes any image previously set in the
   Image Box.

The SCP shall return the status code of the requested SOP Instance
update. The meaning of success, warning, and failure status codes is
defined in `Status Code Categories <#sect_H.2.5>`__.

If Requested Decimate/Crop Behavior (2020,0040) specifies DECIMATE,
Magnification Type (2010,0060) specifies NONE, and the image is too
large to fit the Image Box, the SCP shall fail the N-SET.

.. _sect_H.4.3.1.3:

SOP Class Definition and UID
''''''''''''''''''''''''''''

The Basic Grayscale Image Box SOP Class UID shall have the value
"1.2.840.10008.5.1.1.4".

.. _sect_H.4.3.2:

Basic Color Image Box SOP Class
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

.. _sect_H.4.3.2.1:

IOD Description
'''''''''''''''

The Basic Image Box IOD is an abstraction of the presentation of an
image and image related data in the image area of a film. The Basic
Image Box IOD describes the presentation parameters and image pixel data
that apply to a single image of a sheet of film.

The Basic Color Image Box SOP Instance is created by the SCP at the time
the Basic Film Box SOP Instance is created, based on the value of the
Basic Film Box Attribute Image Display Format (2010,0010).

The Basic Color Image Box SOP Instance refers to zero or one Image
Overlay Box SOP Instance.

.. _sect_H.4.3.2.2:

DIMSE Service Group
'''''''''''''''''''

The following DIMSE Services are applicable to the IOD.

.. table:: DIMSE Service Group Applicable to Basic Color Image Box

   ===================== =============
   DIMSE Service element Usage SCU/SCP
   ===================== =============
   N-SET                 M/M
   ===================== =============

The meaning of the Usage SCU/SCP is described in `Usage
Specifications <#sect_H.2.4>`__.

.. note::

   There is no N-CREATE because Instances of the Basic Color Image Box
   SOP Class are created by the SCP as a result of the N-CREATE of the
   Film Box SOP Instance.

This Section describes the behavior of the DIMSE Services that are
specific for this IOD. The general behavior of the DIMSE Services is
specified in .

.. _sect_H.4.3.2.2.1:

N-SET
     

The N-SET may be used to update an instance of the Basic Color Image Box
SOP Class.

.. _sect_H.4.3.2.2.1.1:

Attributes
          

The Attributes that may be updated are shown in
`table_title <#table_H.4-11>`__.

The meaning of the Usage SCU/SCP is described in `Usage
Specifications <#sect_H.2.4>`__.

The values of Magnification Type (2010,0060) and Smoothing Type
(2010,0080) of a particular image box override the values of
Magnification Type and Smoothing Type of the film box.

.. table:: N-SET Attributes

   +--------------------------+-------------+--------------------------+
   | Attribute Name           | Tag         | Usage SCU/SCP            |
   +==========================+=============+==========================+
   | Image Box Position       | (2020,0010) | M/M                      |
   +--------------------------+-------------+--------------------------+
   | Basic Color Image        | (2020,0111) | M/M                      |
   | Sequence                 |             |                          |
   +--------------------------+-------------+--------------------------+
   | >Samples Per Pixel       | (0028,0002) | M/M                      |
   +--------------------------+-------------+--------------------------+
   | >Photometric             | (0028,0004) | M/M                      |
   | Interpretation           |             |                          |
   +--------------------------+-------------+--------------------------+
   | >Planar Configuration    | (0028,0006) | M/M                      |
   +--------------------------+-------------+--------------------------+
   | >Rows                    | (0028,0010) | M/M                      |
   +--------------------------+-------------+--------------------------+
   | >Columns                 | (0028,0011) | M/M                      |
   +--------------------------+-------------+--------------------------+
   | >Pixel Aspect Ratio      | (0028,0034) | MC/M                     |
   |                          |             |                          |
   |                          |             | (Required if the aspect  |
   |                          |             | ration is not 1\1)       |
   +--------------------------+-------------+--------------------------+
   | >Bits Allocated          | (0028,0100) | M/M                      |
   +--------------------------+-------------+--------------------------+
   | >Bits Stored             | (0028,0101) | M/M                      |
   +--------------------------+-------------+--------------------------+
   | >High Bit                | (0028,0102) | M/M                      |
   +--------------------------+-------------+--------------------------+
   | >Pixel Representation    | (0028,0103) | M/M                      |
   +--------------------------+-------------+--------------------------+
   | >Pixel Data              | (7FE0,0010) | M/M                      |
   +--------------------------+-------------+--------------------------+
   | Polarity                 | (2020,0020) | U/M                      |
   +--------------------------+-------------+--------------------------+
   | Magnification Type       | (2010,0060) | U/U                      |
   +--------------------------+-------------+--------------------------+
   | Smoothing Type           | (2010,0080) | U/U                      |
   +--------------------------+-------------+--------------------------+
   | Requested Image Size     | (2020,0030) | U/U                      |
   +--------------------------+-------------+--------------------------+
   | Requested Decimate/Crop  | (2020,0040) | U/U                      |
   | Behavior                 |             |                          |
   +--------------------------+-------------+--------------------------+

.. _sect_H.4.3.2.2.1.2:

Status
      

`table_title <#table_H.4.3.1.2.1.2-1>`__ defines the specific status
code values that may be returned in a N-SET response. See for additional
response status codes.

.. table:: Status Values for Basic Color Image Box SOP Class

   +--------------------------+--------------------------+-------------+
   | Service Status           | Further Meaning          | Status Code |
   +==========================+==========================+=============+
   | Warning                  | Image size larger than   | B604        |
   |                          | image box size, the      |             |
   |                          | image has been           |             |
   |                          | demagnified.             |             |
   +--------------------------+--------------------------+-------------+
   | Image size is larger     | B609                     |             |
   | than the Image Box size. |                          |             |
   | The Image has been       |                          |             |
   | cropped to fit.          |                          |             |
   +--------------------------+--------------------------+-------------+
   | Image size or Combined   | B60A                     |             |
   | Print Image size is      |                          |             |
   | larger than the Image    |                          |             |
   | Box size. The Image or   |                          |             |
   | Combined Print Image has |                          |             |
   | been decimated to fit.   |                          |             |
   +--------------------------+--------------------------+-------------+
   | Failure                  | Failed: Image size is    | C603        |
   |                          | larger than image box    |             |
   |                          | size                     |             |
   +--------------------------+--------------------------+-------------+
   | Failed: Insufficient     | C605                     |             |
   | memory in printer to     |                          |             |
   | store the image          |                          |             |
   +--------------------------+--------------------------+-------------+
   | Failed: Combined Print   | C613                     |             |
   | Image size is larger     |                          |             |
   | than the Image Box size  |                          |             |
   +--------------------------+--------------------------+-------------+

.. _sect_H.4.3.2.2.1.3:

Behavior
        

The SCU uses the N-SET to request the SCP to update a Basic Color Image
Box SOP Instance. The SCU shall only specify the SOP Instance UID of a
Basic Color Image Box belonging to the last created Film Box SOP
Instance and shall specify the list of Attributes for which the
Attribute Values are to be set.

To instruct the SCP to erase the image in the image position, the SCU
shall set a zero length and no value in the Attribute Basic Color Image
Sequence (2020,0111).

The SCP shall set new values for the specified Attributes of the
specified SOP Instance.

.. note::

   The image in this N-SET supersedes any image previously set in the
   Image Box.

The SCP shall return the status code of the requested SOP Instance
update. The meaning of success, warning, and failure status codes is
defined in `Status Code Categories <#sect_H.2.5>`__.

If Requested Decimate/Crop Behavior (2020,0040) specifies DECIMATE,
Magnification Type (2010,0060) specifies NONE, and the image is too
large to fit the Image Box, the SCP shall fail the N-SET.

The color characteristics of the Pixel Data (7FE0,0010) in the Basic
Color Image Box may be described by an ICC Input Device Profile
specified in the Film Box, in which case the same profile shall apply to
all the Image Boxes in the same Film Box. See
`N-CREATE <#sect_H.4.2.2.1>`__ and `N-SET <#sect_H.4.2.2.2>`__.

.. _sect_H.4.3.2.3:

SOP Class Definition and UID
''''''''''''''''''''''''''''

The Basic Color Image Box SOP Class UID shall have the value
"1.2.840.10008.5.1.1.4.1".

.. _sect_H.4.3.3:

Referenced Image Box SOP Class (Retired)
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

This section was previously defined in DICOM. It is now retired. See PS
3.4-1998.

.. _sect_H.4.4:

Basic Annotation Box SOP Class
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

.. _sect_H.4.4.1:

IOD Description
^^^^^^^^^^^^^^^

The Basic Annotation Box IOD is an abstraction of the presentation of an
annotation (e.g., text string) on a film. The Basic Annotation Box IOD
describes the most used text related presentation parameters.

The Basic Annotation Box SOP Instance is created by the SCP at the time
the Basic Film Box SOP Instance is created, based on the value of the
Attribute Annotation Display Format ID (2010,0030) of the Basic Film
Box.

.. _sect_H.4.4.2:

DIMSE Service Group
^^^^^^^^^^^^^^^^^^^

The DIMSE Services that are applicable to the IOD are shown below.

.. table:: DIMSE Service Group Applicable to Basic Annotation Box

   ============================= =============
   DICOM Message Service Element Usage SCU/SCP
   ============================= =============
   N-SET                         U/M
   ============================= =============

The meaning of the Usage SCU/SCP is described in `Usage
Specifications <#sect_H.2.4>`__.

.. note::

   There is no N-CREATE because the Instances of the Basic Annotation
   Box SOP Class are created by the Film Box SOP Instance.

This Section describes the behavior of the DIMSE Services that are
specific for this IOD. The general behavior of the DIMSE Services is
specified in .

.. _sect_H.4.4.2.1:

N-SET
'''''

The N-SET is used to update the Basic Annotation Box SOP Instance.

.. _sect_H.4.4.2.1.1:

Attributes
          

The Attributes that may be updated are shown in
`table_title <#table_H.4-13>`__.

.. table:: N-SET Attributes

   =================== =========== =============
   Attribute Name      Tag         Usage SCU/SCP
   =================== =========== =============
   Annotation position (2030,0010) M/M
   Text String         (2030,0020) U/M
   =================== =========== =============

The meaning of the Usage SCU/SCP is described in `Usage
Specifications <#sect_H.2.4>`__.

.. _sect_H.4.4.2.1.2:

Status
      

There are no specific status codes. See for response status codes.

.. _sect_H.4.4.2.1.3:

Behavior
        

The SCU uses the N-SET to request the SCP to update a Basic Annotation
Box SOP Instance. The SCU shall only specify the SOP Instance UID of the
Basic Annotation Box belonging to the last created Film Box SOP Instance
in the N-SET request primitive, and shall specify the list of Attributes
for which the Attribute Values are to be set. The SCU may erase the text
string by setting a zero length value in the Attribute Text String
(2030,0020).

The SCP shall set new values for the specified Attributes of the
specified SOP Instance.

The SCP shall return the status code of the requested SOP Instance
update. The meaning of success, warning, and failure status codes is
defined in `Status Code Categories <#sect_H.2.5>`__.

.. _sect_H.4.4.3:

SOP Class Definition and UID
^^^^^^^^^^^^^^^^^^^^^^^^^^^^

The Basic Annotation Box SOP Class UID shall have the value
"1.2.840.10008.5.1.1.15".

.. _sect_H.4.5:

Print Job SOP Class
~~~~~~~~~~~~~~~~~~~

.. _sect_H.4.5.1:

IOD Description
^^^^^^^^^^^^^^^

The Print Job IOD is an abstraction of the Print Job transaction and is
the basic information entity to monitor the execution of the Print
Process. A Print Job contains one film or multiple films, all belonging
to the same film session.

The Print Job SOP Class is created by N-ACTION operation of the Film
Session SOP Class, Film Box SOP Class, or Pull Print Request SOP Class.
The Print Job SOP Instance is deleted after the films are printed or
after a failure condition.

.. _sect_H.4.5.2:

DIMSE Service Group
^^^^^^^^^^^^^^^^^^^

The DIMSE Services that are applicable to the IOD are shown below.

.. table:: DIMSE Service Group Applicable to Print Job

   ============================= =============
   DICOM Message Service Element Usage SCU/SCP
   ============================= =============
   N-EVENT-REPORT                M/M
   N-GET                         U/M
   ============================= =============

The meaning of the Usage SCU/SCP is described in `Usage
Specifications <#sect_H.2.4>`__.

This Section describes the behavior of the DIMSE Services that are
specific for this IOD. The general behavior of the DIMSE Services is
specified in .

.. _sect_H.4.5.2.1:

N-EVENT-REPORT
''''''''''''''

The N-EVENT-REPORT is used to report execution status changes to the SCU
in an asynchronous way.

.. _sect_H.4.5.2.1.1:

Attributes
          

The arguments of the N-EVENT-REPORT are defined as shown in
`table_title <#table_H.4-14>`__.

.. note::

   The encoding of Notification Event Information is defined in .

.. table:: Notification Event Information

   +-------------+-------------+-------------+-------------+-------------+
   | Event Type  | Event Type  | Attribute   | Tag         | Usage       |
   | Name        | ID          | Name        |             | SCU/SCP     |
   +=============+=============+=============+=============+=============+
   | Pending     | 1           | Execution   | (2100,0030) | U/M         |
   |             |             | Status Info |             |             |
   +-------------+-------------+-------------+-------------+-------------+
   |             |             | Film        | (2000,0050) | U/U         |
   |             |             | Session     |             |             |
   |             |             | Label       |             |             |
   +-------------+-------------+-------------+-------------+-------------+
   |             |             | Printer     | (2110,0030) | U/U         |
   |             |             | Name        |             |             |
   +-------------+-------------+-------------+-------------+-------------+
   | Printing    | 2           | Execution   | (2100,0030) | U/M         |
   |             |             | Status Info |             |             |
   +-------------+-------------+-------------+-------------+-------------+
   |             |             | Film        | (2000,0050) | U/U         |
   |             |             | Session     |             |             |
   |             |             | Label       |             |             |
   +-------------+-------------+-------------+-------------+-------------+
   |             |             | Printer     | (2110,0030) | U/U         |
   |             |             | Name        |             |             |
   +-------------+-------------+-------------+-------------+-------------+
   | Done        | 3           | Execution   | (2100,0030) | U/M         |
   |             |             | Status Info |             |             |
   +-------------+-------------+-------------+-------------+-------------+
   |             |             | Film        | (2000,0050) | U/U         |
   |             |             | Session     |             |             |
   |             |             | Label       |             |             |
   +-------------+-------------+-------------+-------------+-------------+
   |             |             | Printer     | (2110,0030) | U/U         |
   |             |             | Name        |             |             |
   +-------------+-------------+-------------+-------------+-------------+
   | Failure     | 4           | Execution   | (2100,0030) | U/M         |
   |             |             | Status Info |             |             |
   +-------------+-------------+-------------+-------------+-------------+
   |             |             | Film        | (2000,0050) | U/U         |
   |             |             | Session     |             |             |
   |             |             | Label       |             |             |
   +-------------+-------------+-------------+-------------+-------------+
   |             |             | Printer     | (2110,0030) | U/U         |
   |             |             | Name        |             |             |
   +-------------+-------------+-------------+-------------+-------------+

.. _sect_H.4.5.2.1.2:

Behavior
        

The SCP uses the N-EVENT-REPORT to inform the SCU about each execution
change. The SCP shall only use the N-EVENT-REPORT within the context of
the Association in which the Print Job SOP Instance was created.

.. note::

   If SCU wants to monitor the complete execution process of a Print
   Job, then the SCU should only release the Association after the
   receipt of the event type Done or Failure.

The SCU shall return the confirmation from the N-EVENT-REPORT operation.

If the Event Type Name = Failure or Pending then the error/pending
condition is stored in the Execution Status Info argument. The possible
values of the Execution Status Info argument are defined in `Execution
Status Information <#sect_H.4.5.3>`__.

If the Event Type Name = Failure or Done then the SCP shall delete the
Print Job SOP Instance after receiving a confirmation from the SCU.

.. _sect_H.4.5.2.1.3:

Status
      

There are no specific status codes. See for response status codes.

.. _sect_H.4.5.2.2:

N-GET
'''''

The N-GET is used to retrieve an instance of the Print Job SOP Class.

.. _sect_H.4.5.2.2.1:

Attributes
          

The Attributes that may be retrieved are shown in
`table_title <#table_H.4-15>`__.

.. table:: N-GET Attributes

   ===================== =========== =============
   Attribute Name        Tag         Usage SCU/SCP
   ===================== =========== =============
   Execution Status      (2100,0020) U/M
   Execution Status Info (2100,0030) U/M
   Print Priority        (2000,0020) U/M
   Creation Date         (2100,0040) U/U
   Creation Time         (2100,0050) U/U
   Printer Name          (2110,0030) U/U
   Originator            (2100,0070) U/U
   ===================== =========== =============

The meaning of the Usage SCU/SCP is described in `Usage
Specifications <#sect_H.2.4>`__.

.. _sect_H.4.5.2.2.2:

Behavior
        

The SCU uses the N-GET to request the SCP to get a Print Job SOP
Instance. The SCU shall specify in the N-GET request primitive the UID
of the SOP Instance to be retrieved.

The SCP shall return the values for the specified Attributes of the
specified SOP Instance.

The SCP shall return the status code of the requested SOP Instance
retrieval. The meaning of success, warning, and failure status codes is
defined in `Status Code Categories <#sect_H.2.5>`__.

.. _sect_H.4.5.2.2.3:

Status
      

There are no specific status codes. See for response status codes.

.. _sect_H.4.5.3:

Execution Status Information
^^^^^^^^^^^^^^^^^^^^^^^^^^^^

Status Information is defined in . Implementation specific warning and
error codes shall be defined in the Conformance Statement.

.. _sect_H.4.5.4:

SOP Class Definition and UID
^^^^^^^^^^^^^^^^^^^^^^^^^^^^

The Print Job SOP Class UID shall have the value
"1.2.840.10008.5.1.1.14".

.. _sect_H.4.6:

Printer SOP Class
~~~~~~~~~~~~~~~~~

.. _sect_H.4.6.1:

IOD Description
^^^^^^^^^^^^^^^

The Printer IOD is an abstraction of the hard copy printer and is the
basic Information Entity to monitor the status of the printer.

The Printer SOP Instance is created by the SCP during start-up of the
hard copy printer and has a well-known SOP Instance UID.

.. _sect_H.4.6.2:

DIMSE Service Group
^^^^^^^^^^^^^^^^^^^

The DIMSE Services that are applicable to the IOD are shown below.

.. table:: DIMSE Service Group Applicable to Printer

   ============================= =============
   DICOM Message Service Element Usage SCU/SCP
   ============================= =============
   N-EVENT-REPORT                M/M
   N-GET                         U/M
   ============================= =============

The meaning of the Usage SCU/SCP is described in `Usage
Specifications <#sect_H.2.4>`__.

This Section describes the behavior of the DIMSE Services that are
specific for this IOD. The general behavior of the DIMSE Services is
specified in .

.. _sect_H.4.6.2.1:

N-EVENT-REPORT
''''''''''''''

The N-EVENT-REPORT is used to report the changes of the printer status
in an asynchronous way.

.. _sect_H.4.6.2.1.1:

Attributes
          

The arguments of the N-EVENT-REPORT are defined as shown in
`table_title <#table_H.4-16>`__.

.. note::

   The encoding of Notification Event Information is defined in .

.. table:: Notification Event Information

   +-----------------+---------------+---------------------+-------------+---------------+
   | Event Type Name | Event Type ID | Attribute Name      | Tag         | Usage SCU/SCP |
   +=================+===============+=====================+=============+===============+
   | Normal          | 1             |                     |             |               |
   +-----------------+---------------+---------------------+-------------+---------------+
   | Warning         | 2             | Printer Status Info | (2110,0020) | U/M           |
   +-----------------+---------------+---------------------+-------------+---------------+
   |                 |               | Film Destination    | (2000,0040) | U/U           |
   +-----------------+---------------+---------------------+-------------+---------------+
   |                 |               | Printer Name        | (2110,0030) | U/U           |
   +-----------------+---------------+---------------------+-------------+---------------+
   | Failure         | 3             | Printer Status Info | (2110,0020) | U/M           |
   +-----------------+---------------+---------------------+-------------+---------------+
   |                 |               | Film Destination    | (2000,0040) | U/U           |
   +-----------------+---------------+---------------------+-------------+---------------+
   |                 |               | Printer Name        | (2110,0030) | U/U           |
   +-----------------+---------------+---------------------+-------------+---------------+

.. _sect_H.4.6.2.1.2:

Behavior
        

The SCP shall use the N-EVENT-REPORT to inform the SCU about each
execution change. The SCP shall send the events to all SCUs with which
the SCP has an Association that is using the printer for which the
status changes.

The SCU shall return the confirmation of the N-EVENT-REPORT operation.

If the Event Type Name = Warning or Failure then the warning/failure
condition is stored in the Printer Status Info argument. The possible
values the Printer Status Info argument are defined in `Printer Status
Information <#sect_H.4.6.3>`__.

.. _sect_H.4.6.2.1.3:

Status
      

There are no specific status codes. See for response status codes.

.. _sect_H.4.6.2.2:

N-GET
'''''

The N-GET is used to retrieve an instance of the Printer SOP Class.

.. _sect_H.4.6.2.2.1:

Attributes
          

The Attributes that may be retrieved are shown in
`table_title <#table_H.4-17>`__.

.. table:: N-GET Attributes

   ======================= =========== =============
   Attribute Name          Tag         Usage SCU/SCP
   ======================= =========== =============
   Printer Status          (2110,0010) U/M
   Printer Status Info     (2110,0020) U/M
   Printer Name            (2110,0030) U/U
   Manufacturer            (0008,0070) U/U
   Manufacturer Model Name (0008,1090) U/U
   Device Serial Number    (0018,1000) U/U
   Software Versions       (0018,1020) U/U
   Date Last Calibration   (0018,1200) U/U
   Last Calibration        (0018,1201) U/U
   ======================= =========== =============

The meaning of the Usage SCU/SCP is described in `Usage
Specifications <#sect_H.2.4>`__.

.. _sect_H.4.6.2.2.2:

Behavior
        

The SCU uses the N-GET to request the SCP to get a Printer SOP Instance.
The SCU shall specify in the N-GET request primitive the UID of the SOP
Instance to be retrieved.

The SCP shall return the values for the specified Attributes of the
specified SOP Instance.

The SCP shall return the status code of the requested SOP Instance
retrieval. The meaning of success, warning, and failure status codes is
defined in `Status Code Categories <#sect_H.2.5>`__.

.. _sect_H.4.6.2.2.3:

Status
      

There are no specific status codes. See for response status codes.

.. _sect_H.4.6.3:

Printer Status Information
^^^^^^^^^^^^^^^^^^^^^^^^^^

Status Information is defined in . Implementation specific warning and
error codes shall be defined in the Conformance Statement.

.. _sect_H.4.6.4:

SOP Class Definition and UID
^^^^^^^^^^^^^^^^^^^^^^^^^^^^

The Printer SOP Class UID shall have the value "1.2.840.10008.5.1.1.16".

.. _sect_H.4.6.5:

Reserved Identifications
^^^^^^^^^^^^^^^^^^^^^^^^

The well-known UID of the Printer SOP Instance shall have the value
"1.2.840.10008.5.1.1.17".

.. _sect_H.4.7:

VOI LUT Box SOP Class(Retired)
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

This section was previously defined in DICOM. It is now retired. See PS
3.4-1998.

.. _sect_H.4.8:

Image Overlay Box SOP Class(Retired)
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

This section was previously defined in DICOM. It is now retired. See PS
3.4-1998.

.. _sect_H.4.9:

Presentation LUT SOP Class
~~~~~~~~~~~~~~~~~~~~~~~~~~

.. _sect_H.4.9.1:

Information Object Description
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

The Presentation LUT Information Object is an abstraction of a
Presentation LUT (see `Global Data Flow Model <#sect_H.2.1.1>`__). The
objective of the Presentation LUT is to realize image display tailored
for specific modalities, applications, and user preferences. It is used
to prepare image pixel data for display on devices that conform to the
Grayscale Standard Display Function defined in .

.. note::

   The density range to be printed, Min Density to Max Density, is
   specified at either the Film Box or the Image Box. As follows from
   the definition for Min Density and Max Density in , if the requested
   minimum density is lower than the minimum printer density, or the
   requested maximum density is greater than the maximum printer
   density, the printer will use its minimum or maximum density,
   respectively, when computing the standard response.

The output of the Presentation LUT is Presentation Values (P-Values).
P-Values are approximately related to human perceptual response. They
are intended to facilitate common input for both hardcopy and softcopy
display devices. P-Values are intended to be independent of the specific
class or characteristics of the display device.

The Presentation LUT is not intended to alter the appearance of the
pixel values, as specified as specified by the Photometric
Interpretation (0028,0004) and Polarity (2020,0020).

The Basic Film Box Information Object, the Basic Image Box Information
Object and the Referenced Image Box Object reference the Presentation
LUT.

If the Configuration Information Attribute (2010,0150) of the Basic Film
Box IOD contains information similar to the Presentation LUT, then the
Presentation LUT Attributes shall take precedence.

.. _sect_H.4.9.1.1:

Mapping of P-Values to Optical Density
''''''''''''''''''''''''''''''''''''''

The mathematical definition of the Grayscale Standard Display Function
and mapping of P-Values to optical density for reflective and
transmissive printers is contained in .

.. _sect_H.4.9.2:

DIMSE Service Group
^^^^^^^^^^^^^^^^^^^

The following DIMSE Services are applicable to the association related
Presentation LUT Information Object:

.. table:: DIMSE Service Group Applicable to Presentation LUT

   ============================= =============
   DICOM Message Service Element Usage SCU/SCP
   ============================= =============
   N-CREATE                      M/M
   N-DELETE                      U/M
   ============================= =============

The meaning of the Usage SCU/SCP is described in section `Usage
Specifications <#sect_H.2.4>`__.

This section describes the behavior of the DIMSE Services, which are
specific for this Information Object. The general behavior of the DIMSE
services is specified in .

.. _sect_H.4.9.2.1:

N-CREATE
''''''''

The N-CREATE Service Element is used to create an instance of the
Presentation LUT SOP Class.

.. _sect_H.4.9.2.1.1:

Attributes
          

The Attribute list of the N-CREATE Service Element is defined as shown
in `table_title <#table_H.4-23>`__.

.. table:: N-CREATE Attribute List

   +--------------------------+-------------+--------------------------+
   | Attribute Name           | Tag         | Usage SCU/SCP            |
   +==========================+=============+==========================+
   | Presentation LUT         | (2050,0010) | MC/M                     |
   | Sequence                 |             |                          |
   |                          |             | (Required if             |
   |                          |             | Presentation LUT Shape   |
   |                          |             | (2050,0020) is not       |
   |                          |             | present. Not allowed     |
   |                          |             | otherwise.)              |
   +--------------------------+-------------+--------------------------+
   | >LUT Descriptor          | (0028,3002) | MC/M                     |
   |                          |             |                          |
   |                          |             | (Required if sequence is |
   |                          |             | present).                |
   |                          |             |                          |
   |                          |             | See `LUT                 |
   |                          |             | Descriptor <             |
   |                          |             | #sect_H.4.9.2.1.1.1>`__. |
   +--------------------------+-------------+--------------------------+
   | >LUT Explanation         | (0028,3003) | U/U                      |
   +--------------------------+-------------+--------------------------+
   | >LUT Data                | (0028,3006) | MC/M                     |
   |                          |             |                          |
   |                          |             | (Required if sequence is |
   |                          |             | present)                 |
   +--------------------------+-------------+--------------------------+
   | Presentation LUT Shape   | (2050,0020) | MC/M                     |
   |                          |             |                          |
   |                          |             | (Required if             |
   |                          |             | Presentation LUT         |
   |                          |             | Sequence (2050,0010) is  |
   |                          |             | not present. Not allowed |
   |                          |             | otherwise.)              |
   |                          |             |                          |
   |                          |             | SCPs shall support the   |
   |                          |             | Enumerated Values        |
   |                          |             | IDENTITY and LIN OD      |
   +--------------------------+-------------+--------------------------+

.. _sect_H.4.9.2.1.1.1:

LUT Descriptor
              

The first value (number of entries in the LUT) shall be equal to:

-  256 if Bits Stored = 8,

-  4096 if Bits Stored = 12.

The second value shall be equal to 0.

The third value (number of bits for each LUT entry) shall be 10-16.

See the definition in for further explanation.

.. _sect_H.4.9.2.1.2:

Status
      

`table_title <#table_H.4.9.2.1.2-1>`__ defines the specific status code
values that may be returned in a N-CREATE response. See for additional
response status codes

.. table:: Status Values for Presentation LUT SOP Class

   +----------------+-------------------------------------+-------------+
   | Service Status | Further Meaning                     | Status Code |
   +================+=====================================+=============+
   | Success        | Presentation LUT successfully       | 0000        |
   |                | created                             |             |
   +----------------+-------------------------------------+-------------+
   | Warning        | Requested Min Density or Max        | B605        |
   |                | Density outside of printer's        |             |
   |                | operating range. The printer will   |             |
   |                | use its respective minimum or       |             |
   |                | maximum density value instead.      |             |
   +----------------+-------------------------------------+-------------+

.. _sect_H.4.9.2.1.3:

Behavior
        

The SCU uses the N-CREATE Service Element to request the SCP to create a
Presentation LUT SOP Instance. The SCU shall initialize Attributes of
the SOP Class as specified in section `Usage
Specifications <#sect_H.2.4>`__.

The SCU shall create the Presentation LUT prior to referencing it from
the Film Box or the Image Box.

The Presentation LUT persists in the SCP as long as the Association in
which it was created is open or an explicit N-DELETE is issued by the
SCU.

The SCP shall return the status code of the requested SOP Instance
creation. The meaning of success, warning, and failure status codes is
defined in `Status Code Categories <#sect_H.2.5>`__.

The SCP shall use the Grayscale Standard Display Function as specified
in to convert the output of the Presentation LUT to density for
printing. If the SCU specifies values for Illumination (2010,015E)
and/or Reflected Ambient Light (2010,0160), these values shall be used
instead of the default or configured values of the SCP. If these values
are not supplied, the SCP shall use its default or configured values.
(see `Attributes <#sect_H.4.2.2.1.1>`__ for suggested defaults).

.. _sect_H.4.9.2.2:

N-DELETE
''''''''

The N-DELETE Service Element is used to delete the Presentation LUT SOP
Instance.

.. _sect_H.4.9.2.2.1:

Status
      

There are no specific status codes. See for response status codes.

.. _sect_H.4.9.2.2.2:

Behavior
        

The SCU uses the N-DELETE Service Element to request the SCP to delete
the Presentation LUT SOP Instance. The SCU shall specify the
Presentation LUT SOP Instance UID.

The SCP shall not delete a Presentation LUT SOP Instance as long as
there are outstanding references to it. Otherwise, it shall delete the
specified Presentation LUT SOP Instance. The N-DELETE of a Presentation
LUT will prevent the SCU from further referencing it. The SCU shall not
reference a previously deleted Presentation LUT. The SCP shall return
the status code of the requested Presentation LUT SOP Instance deletion.
The meaning of success, warning, and failure status codes is defined in
`Status Code Categories <#sect_H.2.5>`__.

.. _sect_H.4.9.2.4:

SOP Class Definition and UID
''''''''''''''''''''''''''''

The Presentation LUT SOP Class UID is "1.2.840.10008.5.1.1.23".

.. _sect_H.4.10:

Pull Print Request SOP Class(Retired)
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

This section was previously defined in DICOM. It is now retired. See PS
3.4-2004.

.. _sect_H.4.11:

Printer Configuration Retrieval SOP Class
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

.. _sect_H.4.11.1:

IOD Description
^^^^^^^^^^^^^^^

The Printer Configuration IOD is an abstraction of the hard copy printer
and is the basic Information Entity to retrieve key imaging
characteristics of the printer

The Printer Configuration Retrieval SOP Instance is created by the SCP
during start-up of the hard copy printer and has a well-known SOP
Instance UID.

.. _sect_H.4.11.2:

DIMSE Service Group
^^^^^^^^^^^^^^^^^^^

The DIMSE Services that are applicable to the IOD are shown in
`table_title <#table_H.4.11.2-1>`__.

.. table:: DIMSE Service Group Applicable to Printer Configuration
Retrieval

   ============================= =============
   DICOM Message Service Element Usage SCU/SCP
   ============================= =============
   N-GET                         M/M
   ============================= =============

The meaning of the Usage SCU/SCP is described in `Usage
Specifications <#sect_H.2.4>`__.

This Section describes the behavior of the DIMSE Service that are
specific for this IOD. The general behavior of the DIMSE Services is
specified in .

.. _sect_H.4.11.2.2:

N-GET
'''''

The N-GET is used to retrieve an instance of the Printer Configuration
Retrieval SOP Class.

.. _sect_H.4.11.2.2.1:

Attributes
          

The Attributes that are retrieved are shown in
`table_title <#table_H.4-26>`__.

.. table:: N-GET Attributes

   +--------------------------+-------------+--------------------------+
   | Attribute Name           | Tag         | Usage SCU/SCP            |
   +==========================+=============+==========================+
   | Printer Configuration    | (2000,001E) | U/M                      |
   | Sequence                 |             |                          |
   +--------------------------+-------------+--------------------------+
   | >SOP Classes Supported   | (0008,115A) | -/M                      |
   +--------------------------+-------------+--------------------------+
   | >Maximum Memory          | (2000,0061) | -/M                      |
   | Allocation               |             |                          |
   +--------------------------+-------------+--------------------------+
   | >Memory Bit Depth        | (2000,00A0) | -/M                      |
   +--------------------------+-------------+--------------------------+
   | >Printing Bit Depth      | (2000,00A1) | -/M                      |
   +--------------------------+-------------+--------------------------+
   | >Media Installed         | (2000,00A2) | -/M                      |
   | Sequence                 |             |                          |
   +--------------------------+-------------+--------------------------+
   | >>Item Number            | (0020,0019) | -/M                      |
   +--------------------------+-------------+--------------------------+
   | >>Medium Type            | (2000,0030) | -/M                      |
   +--------------------------+-------------+--------------------------+
   | >>Film Size ID           | (2010,0050) | -/M                      |
   +--------------------------+-------------+--------------------------+
   | >>Min Density            | (2010,0120) | -/MC                     |
   |                          |             |                          |
   |                          |             | Required if Sequence is  |
   |                          |             | Present and Min Density  |
   |                          |             | is known                 |
   +--------------------------+-------------+--------------------------+
   | >>Max Density            | (2010,0130) | -/M                      |
   +--------------------------+-------------+--------------------------+
   | >Other Media Available   | (2000,00A4) | -/M                      |
   | Sequence                 |             |                          |
   +--------------------------+-------------+--------------------------+
   | >>Medium Type            | (2000,0030) | -/M                      |
   +--------------------------+-------------+--------------------------+
   | >>Film Size ID           | (2010,0050) | -/M                      |
   +--------------------------+-------------+--------------------------+
   | >>Min Density            | (2010,0120) | -/MC                     |
   |                          |             |                          |
   |                          |             | Required if Sequence is  |
   |                          |             | Present and Min Density  |
   |                          |             | is known                 |
   +--------------------------+-------------+--------------------------+
   | >>Max Density            | (2010,0130) | -/M                      |
   +--------------------------+-------------+--------------------------+
   | >Supported Image Display | (2000,00A8) | -/M                      |
   | Formats Sequence         |             |                          |
   +--------------------------+-------------+--------------------------+
   | >>Rows                   | (0028,0010) | -/MC                     |
   |                          |             |                          |
   |                          |             | Required if all Image    |
   |                          |             | Boxes in the Display     |
   |                          |             | Format have the same     |
   |                          |             | number of rows and       |
   |                          |             | columns                  |
   +--------------------------+-------------+--------------------------+
   | >>Columns                | (0028,0011) | -/MC                     |
   |                          |             |                          |
   |                          |             | Required if all Image    |
   |                          |             | Boxes in the Display     |
   |                          |             | Format have the same     |
   |                          |             | number of rows and       |
   |                          |             | columns                  |
   +--------------------------+-------------+--------------------------+
   | >>Image Display Format   | (2010,0010) | -/M                      |
   +--------------------------+-------------+--------------------------+
   | >>Film Orientation       | (2010,0040) | -/M                      |
   +--------------------------+-------------+--------------------------+
   | >>Film Size ID           | (2010,0050) | -/M                      |
   +--------------------------+-------------+--------------------------+
   | >>Printer Resolution ID  | (2010,0052) | -/M                      |
   +--------------------------+-------------+--------------------------+
   | >>Printer Pixel Spacing  | (2010,0376) | -/M                      |
   +--------------------------+-------------+--------------------------+
   | >>Requested Image Size   | (2020,00A0) | -/M                      |
   | Flag                     |             |                          |
   +--------------------------+-------------+--------------------------+
   | >Default Printer         | (2010,0054) | -/M                      |
   | Resolution ID            |             |                          |
   +--------------------------+-------------+--------------------------+
   | >Default Magnification   | (2010,00A6) | -/M                      |
   | Type                     |             |                          |
   +--------------------------+-------------+--------------------------+
   | >Other Magnification     | (2010,00A7) | -/M                      |
   | Types Available          |             |                          |
   +--------------------------+-------------+--------------------------+
   | >Default Smoothing Type  | (2010,00A8) | -/M                      |
   +--------------------------+-------------+--------------------------+
   | >Other Smoothing Types   | (2010,00A9) | -/M                      |
   | Available                |             |                          |
   +--------------------------+-------------+--------------------------+
   | >Configuration           | (2010,0152) | -/M                      |
   | Information Description  |             |                          |
   +--------------------------+-------------+--------------------------+
   | >Maximum Collated Films  | (2010,0154) | -/M                      |
   +--------------------------+-------------+--------------------------+
   | >Decimate/Crop Result    | (2020,00A2) | -/M                      |
   +--------------------------+-------------+--------------------------+
   | >Manufacturer            | (0008,0070) | -/M                      |
   +--------------------------+-------------+--------------------------+
   | >Manufacturer Model Name | (0008,1090) | -/M                      |
   +--------------------------+-------------+--------------------------+
   | >Printer Name            | (2110,0030) | -/M                      |
   +--------------------------+-------------+--------------------------+

The meaning of the Usage SCU/SCP is described in `Usage
Specifications <#sect_H.2.4>`__.

.. _sect_H.4.11.2.2.2:

Behavior
        

The SCU uses the N-GET to request the SCP to get a Printer Configuration
Retrieval SOP Instance. The SCU shall specify in the N-GET request
primitive the UID of the SOP Instance to be retrieved.

The SCP shall return the values for the specified Attributes of the
specified SOP Instance.

The SCP shall return the status code of the requested SOP Instance
retrieval.

A Failure status code shall indicate that the SCP has not retrieved the
SOP Instance.

.. _sect_H.4.11.2.2.3:

Status
      

There are no specific status codes. See for response status codes.

.. _sect_H.4.11.3:

SOP Class Definition and UID
^^^^^^^^^^^^^^^^^^^^^^^^^^^^

The Printer Configuration Retrieval SOP Class UID is
"1.2.840.10008.5.1.1.16.376".

.. _sect_H.4.11.4:

Reserved Identifications
^^^^^^^^^^^^^^^^^^^^^^^^

The well-known UID of the Printer Configuration Retrieval SOP Instance
is "1.2.840.10008.5.1.1.17.376".

.. _sect_H.4.12:

Basic Print Image Overlay Box SOP Class(Retired)
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

This section was previously defined in DICOM. It is now retired. See PS
3.4-2004.

.. _sect_H.5:

Association Negotiation
-----------------------

Association establishment is the first phase of any instance of
communication between peer DICOM AEs. The Association negotiation
procedure is used to negotiate the supported SOP Classes or Meta SOP
Classes. specifies the Association procedures.

The negotiation procedure is used to negotiate the supported Meta SOP
Classes and the supported optional SOP Classes. The SCU and SCP shall
support at least one Meta SOP Class UID (e.g., Basic Grayscale Print
Management Meta SOP Class) and may support additional optional SOP
Classes.

The Print Management Service Class does not support extended
negotiation.

The SCU shall specify in the A-ASSOCIATE request one Abstract Syntax, in
a Presentation Context, for each supported SOP Class or Meta SOP Class.

If the Association is released or aborted then all the SOP Instances
except the Print Job SOP Instance and the Printer SOP Instance are
deleted.

.. note::

   Pending Print Jobs will still be printed after the release or
   abortion of the Association.

.. _sect_H.6:

Example of Print Management SCU Session (Informative)
-----------------------------------------------------

.. _sect_H.6.1:

Simple Example
~~~~~~~~~~~~~~

Moved to .

.. _sect_H.6.2:

Advanced Example(Retired)
~~~~~~~~~~~~~~~~~~~~~~~~~

This section was previously defined in DICOM. It is now retired. See PS
3.4-1998.

.. _sect_H.7:

Example of the Pull Print Request Meta SOP Class (Informative)
--------------------------------------------------------------

This section was previously defined in DICOM. It is now retired. See PS
3.4-2004.

.. _sect_H.8:

Overlay Examples (Informative)
------------------------------

This section was previously defined in DICOM. It is now retired. See PS
3.4-2004.

