.. _chapter_R:

Instance Availability Notification Service Class (Normative)
============================================================

.. _sect_R.1:

Overview
--------

.. _sect_R.1.1:

Scope
~~~~~

The Instance Availability Notification Service Class defines an
application-level class-of-service that allows one DICOM AE to notify
another DICOM AE of the presence and availability of SOP instances that
may be retrieved. The AE from which such SOP Instances can later be
retrieved may or may not be the SCU performing the notification.

.. note::

   An example of usage of this Service Class is for the receiver of the
   instances to provide notification of their arrival and availability
   for subsequent workflow steps to a different entity, such as a
   separate workflow manager.

The SCU implementation defines the conditions under which it provides
the notification. Certain SCUs may provide notification for arbitrary
sets of SOP Instances, while other SCUs may provide notification when
they determine that the instances associated with a Procedure Step or a
Requested Procedure are available. The SCU is required to document in
its Conformance Statement the nature of its notification decisions
(e.g., frequency of notifications, retrieve capabilities and latency,
etc.).

Once the SCU has provided notification about availability of the SOP
Instances, the SCP may use that information in directing further
workflow, such as in populating the Input Information Sequence when
forming a Unified Procedure Step. These types of policies are outside
the scope of this Standard, however, the SCP is required to document
these policies in its Conformance Statement.

The SCU of this Service Class is not required to assure that the study,
procedure step or any workflow-related entity is "complete"; indeed no
semantics other than the concept of "availability" is expressed or
implied by the use of this service.

.. note::

   1. The Performed Workitem Code Sequence (0040,4019) Attribute of a
      referenced GP-PPS instance may provide the specific description of
      the work item that triggered the Instance Availability
      Notification.

   2. The Instance Availability Notification is typically a service of
      the composite instance Storage SCP, since that application is
      responsible for making the instances available. The Instance
      Availability Notification allows that application to report the
      specific Retrieve AE Title, which may differ from the Storage
      Service AE Title, and may vary with different instance SOP
      Classes, or may vary over time.

.. _sect_R.2:

Conformance Overview
--------------------

The Instance Availability Notification Service Class consists of a
single SOP Class: the Instance Availability Notification SOP Class.

The SOP Class specifies Attributes, operations, and behavior applicable
to the SOP Class. The conformance requirements shall be specified in
terms of the Service Class Provider (SCP) and the Service Class User
(SCU).

The Instance Availability Notification Service Class uses the Instance
Availability Notification IOD as defined in and the N-CREATE DIMSE
Service specified in .

.. _sect_R.3:

Instance Availability Notification SOP Class
--------------------------------------------

.. _sect_R.3.1:

DIMSE Service Group
~~~~~~~~~~~~~~~~~~~

The DIMSE Services shown in `table_title <#table_R.3.1-1>`__ are
applicable to the Instance Availability Notification IOD under the
Instance Availability Notification SOP Class.

.. table:: DIMSE Service Group Applicable to Instance Availability
Notification

   ============================= =============
   DICOM Message Service Element Usage SCU/SCP
   ============================= =============
   N-CREATE                      M/M
   ============================= =============

The DIMSE Services and Protocols are specified in .

.. note::

   Though the terminology "notification" is used for this Service Class,
   the notification is in fact performed through Operations rather than
   Notifications.

.. _sect_R.3.2:

Operations
~~~~~~~~~~

The Application Entity that claims conformance to this SOP Class as an
SCU shall be permitted to invoke the following operations and the
Application Entity that claims conformance as an SCP shall be capable of
providing the following operations.

.. _sect_R.3.2.1:

N-CREATE Instance Availability Notification SOP Instance
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

This operation allows an SCU to create an instance of the Instance
Availability Notification SOP Class and to provide availability
information about Instances that are under the control of the SCU. This
operation shall be invoked through the DIMSE N-CREATE Service.

.. _sect_R.3.2.1.1:

Attributes
''''''''''

The Attribute list of the N-CREATE is defined as shown in
`table_title <#table_R.3.2-1>`__.

.. table:: Instance Availability Notification SOP Class N-CREATE
Attributes

   +--------------------------+-------------+--------------------------+
   | Attribute Name           | Tag         | Req. Type N-CREATE       |
   |                          |             | (SCU/SCP)                |
   +==========================+=============+==========================+
   | Specific Character Set   | (0008,0005) | 1C/1C                    |
   |                          |             |                          |
   |                          |             | (Required if an extended |
   |                          |             | or replacement character |
   |                          |             | set is used)             |
   +--------------------------+-------------+--------------------------+
   | *All other Attributes of | 3/3         |                          |
   | the*                     |             |                          |
   +--------------------------+-------------+--------------------------+
   | Referenced Performed     | (0008,1111) | 2/2                      |
   | Procedure Step Sequence  |             |                          |
   +--------------------------+-------------+--------------------------+
   | >Referenced SOP Class    | (0008,1150) | 1/1                      |
   | UID                      |             |                          |
   +--------------------------+-------------+--------------------------+
   | >Referenced SOP Instance | (0008,1155) | 1/1                      |
   | UID                      |             |                          |
   +--------------------------+-------------+--------------------------+
   | >Performed Workitem Code | (0040,4019) | 2/2                      |
   | Sequence                 |             |                          |
   +--------------------------+-------------+--------------------------+
   | *>>Include*\ `tabl       |             |                          |
   | e_title <#table_8-1a>`__ |             |                          |
   +--------------------------+-------------+--------------------------+
   | Study Instance UID       | (0020,000D) | 1/1                      |
   +--------------------------+-------------+--------------------------+
   | Referenced Series        | (0008,1115) | 1/1                      |
   | Sequence                 |             |                          |
   +--------------------------+-------------+--------------------------+
   | >Series Instance UID     | (0020,000E) | 1/1                      |
   +--------------------------+-------------+--------------------------+
   | >Referenced SOP Sequence | (0008,1199) | 1/1                      |
   +--------------------------+-------------+--------------------------+
   | >>Referenced SOP Class   | (0008,1150) | 1/1                      |
   | UID                      |             |                          |
   +--------------------------+-------------+--------------------------+
   | >>Reference SOP Instance | (0008,1155) | 1/1                      |
   | UID                      |             |                          |
   +--------------------------+-------------+--------------------------+
   | >>Instance Availability  | (0008,0056) | 1/1                      |
   +--------------------------+-------------+--------------------------+
   | >>Retrieve AE Title      | (0008,0054) | 1/1                      |
   +--------------------------+-------------+--------------------------+
   | >>Retrieve Location UID  | (0040,E011) | 3/3                      |
   +--------------------------+-------------+--------------------------+
   | >>Retrieve URI           | (0040,E010) | 3/3                      |
   +--------------------------+-------------+--------------------------+
   | >>Retrieve URL           | (0008,1190) | 3/3                      |
   +--------------------------+-------------+--------------------------+
   | >>Storage Media File-Set | (0088,0130) | 3/3                      |
   | ID                       |             |                          |
   +--------------------------+-------------+--------------------------+
   | >>Storage Media File-Set | (0088,0140) | 3/3                      |
   | UID                      |             |                          |
   +--------------------------+-------------+--------------------------+

.. _sect_R.3.2.1.2:

Service Class User
''''''''''''''''''

The SCU shall specify in the N-CREATE request primitive the SOP Class
and SOP Instance UIDs of the Instance Availability Notification SOP
Instance that is created and for which Attribute Values are to be
provided.

The SCU shall provide Attribute Values for the Instance Availability
Notification SOP Class Attributes as specified in
`table_title <#table_R.3.2-1>`__.

The use of additional optional Attributes by the SCU is forbidden.

.. note::

   The reason for forbidding optional Attributes is to prevent the use
   of Standard Extended SOP Classes that might add contextual
   information such as patient and procedure identifiers.

The encoding rules for Instance Availability Notification Attributes are
specified in the N-CREATE request primitive specification in .

There are no requirements on when N-CREATE requests are required to be
performed.

In particular, there are no requirements that notification about the
availability of the first instance of a Performed Procedure Step or
Study be provided upon its reception, nor that availability notification
be provided when an entire set of instances comprising a completed
Performed Procedure Step or Study are available, though these are
typical and common scenarios.

.. _sect_R.3.2.1.3:

Service Class Provider
''''''''''''''''''''''

The SCP shall return, via the N-CREATE response primitive, the N-CREATE
Response Status Code applicable to the associated request.

.. _sect_R.3.2.1.4:

Status Codes
''''''''''''

There are no specific status codes. See for response status codes.

.. _sect_R.3.3:

Instance Availability Notification SOP Class UID
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

The Instance Availability Notification SOP Class shall be uniquely
identified by the Instance Availability Notification SOP Class UID,
which shall have the value "1.2.840.10008.5.1.4.33".

.. _sect_R.3.4:

Conformance Requirements
~~~~~~~~~~~~~~~~~~~~~~~~

Implementations shall include within their Conformance Statement
information as described below.

An implementation may conform to this SOP Class as an SCU or as an SCP.
The Conformance Statement shall be in the format defined in .

.. _sect_R.3.4.1:

SCU Conformance
^^^^^^^^^^^^^^^

An implementation that is conformant to this SOP Class as an SCU shall
meet conformance requirements for the operations that it invokes.

.. _sect_R.3.4.1.1:

Operations
''''''''''

Any Attributes for which Attribute Values may be provided (using the
N-CREATE) by the SCU shall be enumerated in the SCU Conformance
Statement. The SCU Conformance Statement shall be formatted as defined
in .

An implementation that conforms to this SOP Class as an SCU shall
specify under which conditions during the performance of real-world
activities it will create the SOP Class Instance.

The SCU Conformance Statement shall specify what is meant by each
reported value of Instance Availability (0008,0056).

The SCU Conformance Statement shall describe the relationship between
the Instance Availability Notification and the Performed Procedure Step
SOP Classes, if the latter are supported.

.. _sect_R.3.4.2:

SCP Conformance
^^^^^^^^^^^^^^^

An implementation that is conformant to this SOP Class as an SCP shall
meet conformance requirements for the operations that it performs.

.. _sect_R.3.4.2.1:

Operations
''''''''''

The SCP Conformance Statement shall be formatted as defined in .

The SCP Conformance Statement shall provide information on the behavior
of the SCP (in terms of real world activities) for each reported value
of Instance Availability (0008,0056).

The SCP Conformance Statement shall describe the behavioral relationship
between the Instance Availability Notification and the Performed
Procedure Step SOP Classes, if the latter are supported.

