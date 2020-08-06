.. _chapter_GG:

Non-Patient Object Storage Service Class
========================================

.. _sect_GG.1:

Overview
--------

.. _sect_GG.1.1:

Scope
~~~~~

The Non-Patient Object Storage Service Class defines an
application-level class-of-service that allows one DICOM AE to send a
SOP Instance of a non-patient-related information object to another
DICOM AE.

.. _sect_GG.1.2:

Service Definition
~~~~~~~~~~~~~~~~~~

The Non-Patient Object Storage Service Class includes several SOP
Classes, each using an IOD defined in (see `SOP
Classes <#sect_GG.3>`__). The Non-Patient Object Storage Service Class
uses the C-STORE DIMSE Service specified in . A successful completion of
the C-STORE has the following semantics:

-  Both the SCU and the SCP support the type of information to be
   stored.

-  The transferred information is stored in some medium.

-  For some time frame, the stored information may be accessed.

.. note::

   1. Support for the Non-Patient Object Storage Service Class does not
      imply support for any related Query/Retrieve Service Classes.

   2. The duration of the storage is also implementation dependent, but
      is described in the Conformance Statement of the SCP.

   3. The Non-Patient Object Storage Service Class is intended to be
      used in a variety of environments: e.g., for workstations to
      transfer SOP Instances to other workstations or archives, for
      archives to transfer SOP Instances to workstations, etc.

.. _sect_GG.2:

Association Negotiation
-----------------------

The Association negotiation rules as defined in apply to the SOP Classes
of this Service Class. No SOP Class specific application information
(extended negotiation) is used.

.. _sect_GG.3:

SOP Classes
-----------

The application-level services addressed by the Non-Patient Object
Storage Service Class definition are specified in the SOP Classes
specified in `table_title <#table_GG.3-1>`__.

.. table:: Standard SOP Classes

   +----------------------+----------------------+----------------------+
   | SOP Class Name       | SOP Class UID        | **IOD Specification  |
   |                      |                      | (defined in )**      |
   +======================+======================+======================+
   | Hanging Protocol     | 1.2.                 |                      |
   | Storage              | 840.10008.5.1.4.38.1 |                      |
   +----------------------+----------------------+----------------------+
   | Color Palette        | 1.2.                 |                      |
   | Storage              | 840.10008.5.1.4.39.1 |                      |
   +----------------------+----------------------+----------------------+
   | Generic Implant      | 1.2.                 |                      |
   | Template Storage     | 840.10008.5.1.4.43.1 |                      |
   +----------------------+----------------------+----------------------+
   | Implant Assembly     | 1.2.                 |                      |
   | Template Storage     | 840.10008.5.1.4.44.1 |                      |
   +----------------------+----------------------+----------------------+
   | Implant Template     | 1.2.                 |                      |
   | Group Storage        | 840.10008.5.1.4.45.1 |                      |
   +----------------------+----------------------+----------------------+
   | CT Defined Procedure | 1.2.840.1            |                      |
   | Protocol Storage     | 0008.5.1.4.1.1.200.1 |                      |
   +----------------------+----------------------+----------------------+
   | Protocol Approval    | 1.2.840.1            |                      |
   | Storage              | 0008.5.1.4.1.1.200.3 |                      |
   +----------------------+----------------------+----------------------+

.. _sect_GG.4:

Behavior
--------

This Section defines the SCU and SCP behavior for the Non-Patient Object
Storage Service. The C-STORE DIMSE-C Service shall be the mechanism used
to transfer SOP Instances between peer DICOM AEs as described in .

In addition to the behaviors specified in this section, there may be SOP
Class specific behavior requirements, as described in `Application
Behavior for Standard SOP Classes <#sect_GG.6>`__.

.. _sect_GG.4.1:

Service Class User
~~~~~~~~~~~~~~~~~~

A DICOM AE that claims conformance to any of the Non-Patient Object
Storage SOP Classes as an SCU shall be capable of sending a SOP Instance
that meets the requirements of the related IOD. The Service shall be
invoked by the SCU through the use of the DIMSE C-STORE request used in
conjunction with the SOP Class.

The SCU shall recognize the status of the C-STORE service and take
appropriate action based on the success or failure of the service. The
Non-Patient Object Storage Service places no further requirements on
what the SCU shall do other than that it shall distinguish between
successful and failed C-STORE responses. This behavior shall be
documented as part of the Conformance Statement.

.. _sect_GG.4.2:

Service Class Provider
~~~~~~~~~~~~~~~~~~~~~~

A DICOM AE that claims conformance to any of the Non-Patient Object
Storage SOP Classes as an SCP shall receive and store a SOP Instance
through the use of the DIMSE C-STORE service used in conjunction with
the specific SOP Class.

The SCP shall store and provide access to all Type 1, Type 2, and Type 3
Attributes defined in the IOD, as well as any Standard Extended
Attributes (including Private Attributes) included in the SOP Instance.
The SCP may, but is not required to validate that the Attributes of the
SOP Instance meet the requirements of the associated IOD.

The SCP shall not modify the values of any Attributes in the SOP
Instance without assigning a new SOP Instance UID, except that the SCP
may modify values of, or add, Type 3 and Private Attributes that do not
change the semantics or interpretation of the SOP Instance.

.. note::

   E.g., an SCP may add values to Alternate Content Description Sequence
   (0070,0087), to provide an additional description in another
   language.

The SCP shall return, via the C-STORE response primitive, the Response
Status Code applicable to the associated request. By performing this
service successfully, the SCP indicates that the SOP Instance has been
successfully stored. `table_title <#table_GG.4-1>`__ defines the
specific response status code values that might be returned in a C-STORE
response. General status code values and fields related to status code
values are defined for C-STORE DIMSE Service in .

.. table:: C-STORE Response Status Values

   +----------------+----------------+--------------+----------------+
   | Service Status | Further        | Status Codes | Related Fields |
   |                | Meaning        |              |                |
   +================+================+==============+================+
   | Failure        | Refused: Out   | A700         | (0000,0902)    |
   |                | of resources   |              |                |
   +----------------+----------------+--------------+----------------+
   | Error: Data    | A900           | (0000,0901)  |                |
   | Set does not   |                |              |                |
   | match SOP      |                | (0000,0902)  |                |
   | Class          |                |              |                |
   +----------------+----------------+--------------+----------------+
   | Error: Cannot  | C000           | (0000,0901)  |                |
   | understand     |                |              |                |
   |                |                | (0000,0902)  |                |
   +----------------+----------------+--------------+----------------+
   | Success        |                | 0000         | None           |
   +----------------+----------------+--------------+----------------+

.. note::

   Status Codes are returned in DIMSE response messages (see ). The code
   values stated in column "Status Codes" are returned in Status Command
   Element (0000,0900).

.. _sect_GG.5:

Conformance Statement Requirements
----------------------------------

An implementation may conform to any of the Non-Patient Object Storage
SOP Classes as an SCU, SCP or both. The Conformance Statement shall be
in the format defined in .

.. _sect_GG.5.1:

SCU Conformance Requirements
~~~~~~~~~~~~~~~~~~~~~~~~~~~~

An implementation that conforms to a SOP Class of the Non-Patient Object
Storage Service as an SCU shall state in its Conformance Statement:

-  Whether the implementation is a SOP Instance creator for the SOP
   Class.

   .. note::

      There may be SOP Class specific Conformance Statement requirements
      for creators of SOP Instances. See `Application Behavior for
      Standard SOP Classes <#sect_GG.6>`__.

-  The behavior of the SCU in the case of a success C-STORE response
   status.

-  The behavior of the SCU in each case of a failure C-STORE response
   status.

.. _sect_GG.5.2:

SCP Conformance Requirements
~~~~~~~~~~~~~~~~~~~~~~~~~~~~

An implementation that conforms to a SOP Class of the Non-Patient Object
Storage Service as an SCP shall state in its Conformance Statement:

-  The behavior of the SCP in the case of a successful C-STORE
   operation, including the access method for a stored SOP Instance, and
   the duration of the storage.

-  The meaning of each case of a failure C-STORE response status, as
   well as appropriate recovery action.

.. note::

   There may be SOP Class specific Conformance Statement requirements
   for applications that interpret the SOP Instances for display or
   further processing. See `Application Behavior for Standard SOP
   Classes <#sect_GG.6>`__.

.. _sect_GG.6:

Application Behavior for Standard SOP Classes
---------------------------------------------

This section specifies SOP Class specific behaviors for conformant
applications.

.. _sect_GG.6.1:

Hanging Protocol SOP Class
~~~~~~~~~~~~~~~~~~~~~~~~~~

.. _sect_GG.6.1.1:

Instance Creator
^^^^^^^^^^^^^^^^

An implementation that conforms to the Hanging Protocol Storage SOP
Class as an SCU and is a SOP Instance creator shall state in its
Conformance Statement:

-  The manner in which the values of the Hanging Protocol IOD Attributes
   are derived from displayed images, layouts, operator intervention or
   defaults.

-  Any Private Attributes that are used as the value of Selector
   Attribute (0072,0026) in the Image Set Selector Sequence, Filter
   Operations Sequence or Sorting Operations Sequence.

-  The optional Attributes that may be included in a Hanging Protocol
   SOP Instance.

.. _sect_GG.6.1.2:

Display Application
^^^^^^^^^^^^^^^^^^^

An implementation that conforms to the Hanging Protocol Storage SOP
Class as an SCP and interprets the contents of instances of the SOP
Class to control the display of images, shall apply all mandatory
Hanging Protocol and presentation intent Attributes to the sets of
displayed images. Such an implementation shall state in its Conformance
Statement:

-  The range of display environments that the application will support
   (e.g., number of screens, size of screens, overlapping image boxes).

-  The optional Attributes of the Hanging Protocol IOD that it is
   capable of interpreting and those that are not supported.

-  Description of application behavior when the value of Partial Data
   Display Handling (0072,0208) is ADAPT_LAYOUT or zero length.

-  Description of application behavior when the display environment of
   the Hanging Protocol Instance differs from the display environment of
   the application, with respect to preserving layout versus spatial
   resolution.

-  The Image Storage SOP Classes for which the Hanging Protocol Storage
   SOP Class is supported for display control.

.. _sect_GG.6.2:

Color Palette Storage SOP Class
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

.. _sect_GG.6.2.1:

Instance Creator
^^^^^^^^^^^^^^^^

An implementation that conforms to the Color Palette Storage SOP Class
as an SCU and is a SOP Instance creator shall state in its Conformance
Statement:

-  The optional Attributes that may be included in a Color Palette SOP
   Instance.

.. _sect_GG.6.2.2:

Display Application
^^^^^^^^^^^^^^^^^^^

An implementation that conforms to the Color Palette Storage SOP Class
as an SCP and interprets the contents of instances of the SOP Class to
affect the display of images, shall apply all mandatory Color Palette
and presentation intent Attributes to the applicable displayed images.

An implementation that conforms to the Color Palette Storage SOP Class
as an SCP and interprets the contents of instances of the SOP Class to
affect the display of images shall state in its Conformance Statement:

-  The optional Attributes of the Color Palette IOD that it is capable
   of interpreting and those that are not supported.

-  The Image Storage SOP Classes for which application of the Color
   Palette Storage SOP Class is supported

.. _sect_GG.6.3:

Template Storage SOP Classes
~~~~~~~~~~~~~~~~~~~~~~~~~~~~

An implementation that is a Generic Implant Template Storage, Implant
Assembly Template Storage, or Implant Template Group Storage SOP Class
SCU may modify information in a SOP Instance that it has previously sent
or received. When this SOP Instance is modified and sent to an SCP, it
shall be assigned a new SOP Instance UID if there is addition, removal
or update of any Attribute within:

-  Generic Implant Template Description Module

-  Generic Implant Template 2D Drawings Module

-  Generic Implant Template 3D Models Module

-  Generic Implant Template Mating Features Module

-  Generic Implant Template Planning Landmarks Module

-  Implant Assembly Template Module

-  Implant Template Group Module

-  Surface Mesh Module

Referential integrity between sets of related SOP instances shall be
maintained.

.. _sect_GG.6.4:

CT Defined Procedure Protocol Storage SOP Class
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

An implementation that conforms to the CT Defined Procedure Protocol
Storage SOP Class as an SCP shall not modify constraints for which the
value of the Modifiable Constraint Flag (0082,0038) is NO.

Modifying protocol constraints changes the semantics of a CT Defined
Procedure Protocol Storage SOP Instance.

.. _sect_GG.6.5:

Protocol Approval Storage SOP Class
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

Approvals are based on assertions. Receipt or generation of an assertion
will interact with organizational authentication and authorization
policies. For example, an approval may be received by mistake as part of
the transfer of a patient record.

