.. _chapter_F:

Procedure Step SOP Classes (Normative)
======================================

.. _sect_F.1:

Overview
--------

This Annex defines the Procedure Step SOP Classes.

.. note::

   This Annex formerly defined a Study Management Service Class that has
   been retired. See PS 3.4-2004.

.. _sect_F.1.1:

Scope
~~~~~

Retired. See PS 3.4-2004.

.. _sect_F.1.2:

Study Management Functional Model
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

Retired. See PS 3.4-2004.

.. _sect_F.1.3:

Study Management Information Model
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

Retired. See PS 3.4-2004.

.. _sect_F.1.4:

Study Management States
~~~~~~~~~~~~~~~~~~~~~~~

Retired. See PS 3.4-2004.

.. _sect_F.1.5:

Modality Performed Procedure Step Management States
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

The state information related to the Modality Performed Procedure Step
is specified by the Modality Performed Procedure Step IOD in the
Attribute Performed Procedure Step Status (0040,0252).

The Performed Procedure Step Object represents only the "performed"
segment of the real-world procedure step and not the "scheduled"
segment. The number of events is therefore limited; all events are
initiated by the modality. The state "DISCONTINUED" means canceled or
unsuccessfully terminated, which may happen when the performance of a
Procedure Step has been started but cannot be finished by the modality.
The modality shall convey this state change to the information system
(the SCP), to allow the information system to reschedule or cancel the
related Procedure Step. The state "COMPLETED" means that the acquisition
of Composite SOP Instances has been successfully completed and the SCU
has provided all required Attribute Values for the Performed Procedure
Step.

`table_title <#table_F.1-3>`__ describes the valid Modality Performed
Procedure Step states.

.. table:: Modality Performed Procedure Step States

   +--------------+------------------------------------------------------+
   | State        | Description                                          |
   +==============+======================================================+
   | In Progress  | Modality Performed Procedure Step created and        |
   |              | execution in progress                                |
   +--------------+------------------------------------------------------+
   | Discontinued | Execution of Modality Performed Procedure Step       |
   |              | canceled by modality                                 |
   +--------------+------------------------------------------------------+
   | Completed    | Modality Performed Procedure Step completed          |
   +--------------+------------------------------------------------------+

`table_title <#table_F.1-4>`__ defines the valid state transitions for
the Performed Procedure Steps. For each of the above defined states the
valid state resulting from the occurrence of events is specified. These
state transitions are managed by the Modality Performed Procedure Step
SOP Class.

.. table:: Modality Performed Procedure Step State Transition Diagram

   ===================================== ============
   \                                     States        
   ===================================== ============
   Performed Procedure Step Discontinued Discontinued  
   Performed Procedure Step Completed    Completed     
   ===================================== ============

.. _sect_F.1.6:

General Purpose Scheduled Procedure Step Management States (Retired)
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

Retired. See PS 3.4-2011.

.. _sect_F.1.7:

General Purpose Performed Procedure Step Management States (Retired)
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

Retired. See PS 3.4-2011.

.. _sect_F.2:

Conformance Overview
--------------------

The application-level services addressed by this Service Class
Definition are specified via the following distinct SOP Classes:

a. Modality Performed Procedure Step SOP Class

b. Modality Performed Procedure Step Notification SOP Class

c. Modality Performed Procedure Step Retrieve SOP Class

Each SOP Class operates on a subset of the Modality Performed Procedure
Step IOD and specifies the Attributes, operations, notifications, and
behavior applicable to the SOP Class. Conformance of Application
Entities shall be defined by selecting one or more of the Study and
Study Component Management SOP and Meta SOP Classes. For each SOP Class
conformance requirements shall be specified in terms of the Service
Class Provider (SCP) and the Service Class User (SCU).

.. _sect_F.2.1:

Association Negotiation
~~~~~~~~~~~~~~~~~~~~~~~

Association establishment is the first phase of any instance of
communication between peer DICOM AEs. The Association negotiation
procedure specified in shall be used to negotiate the supported SOP
Classes.

Support for the SCP/SCU Role Selection Negotiation is mandatory. The SOP
Class Extended Negotiation shall not be supported.

.. note::

   Event notification is a process that logically extends across
   multiple Associations. SCP implementations should support a local
   table of SCUs to which event notifications are to be sent.

.. _sect_F.3:

Detached Study Management SOP Class(Retired)
--------------------------------------------

Retired. See PS 3.4-2004.

.. _sect_F.4:

Study Component Management SOP Class(Retired)
---------------------------------------------

Retired. See PS 3.4-2004.

.. _sect_F.5:

Study Management Meta SOP Class(Retired)
----------------------------------------

Retired. See PS 3.4-2004.

.. _sect_F.6:

Specialized SOP Class Conformance(Retired)
------------------------------------------

Retired. See PS 3.4-2004.

.. _sect_F.7:

Modality Performed Procedure Step SOP Class
-------------------------------------------

.. _sect_F.7.1:

DIMSE Service Group
~~~~~~~~~~~~~~~~~~~

The DIMSE Services shown in `table_title <#table_F.7.1-1>`__ are
applicable to the Modality Performed Procedure Step IOD under the
Modality Performed Procedure Step SOP Class.

.. table:: DIMSE Service Group Applicable to Modality Performed
Procedure Step

   ============================= =============
   DICOM Message Service Element Usage SCU/SCP
   ============================= =============
   N-CREATE                      M/M
   N-SET                         M/M
   ============================= =============

The DIMSE Services and Protocols are specified in

.. _sect_F.7.2:

Operations
~~~~~~~~~~

The Application Entity that claims conformance to this SOP Class as an
SCU shall be permitted to invoke the following operations and the
Application Entity that claims conformance as an SCP shall be capable of
providing the following operations.

.. _sect_F.7.2.1:

Create Modality Performed Procedure Step SOP Instance
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

This operation allows an SCU to create an instance of the Modality
Performed Procedure Step SOP Class and provide information about a
specific real-world Performed Procedure Step that is under control of
the SCU. This operation shall be invoked through the DIMSE N-CREATE
Service.

.. note::

   The modality should inform the Information System as soon as possible
   that the performance of the Procedure Step has been started by
   sending the N-CREATE Service Request. This allows an SCP of the
   Modality Worklist SOP Class (if supported) to update the Modality
   Worklist. Some of the Attribute Values are already known at the
   beginning of the Procedure Step, they are required to be sent in the
   N-CREATE command. Other mandatory Attributes are known only at the
   end of the Performed Procedure Step, they are assigned a value in the
   N-SET command.

The same SOP Instance UID is shared by all three Modality Performed
Procedure Step SOP Classes. This means that the SOP Instance created and
set using the services of the Modality Performed Procedure Step SOP
Class can be retrieved using its SOP Instance UID within the service of
the Modality Performed Procedure Step Retrieve SOP Class. Changes in its
state can be notified by using its SOP Instance UID within the service
of the Modality Performed Procedure Step Notification SOP Class. The SOP
Class UID specified in the DIMSE N-CREATE and N-SET request primitives
shall be the UID of the Modality Performed Procedure Step SOP Class.

The Modality Performed Procedure Step SOP Instance UID shall not be used
to identify a SOP Instance of the Study Component Service Class.

.. _sect_F.7.2.1.1:

Modality Performed Procedure Step Subset Specification
''''''''''''''''''''''''''''''''''''''''''''''''''''''

The Application Entity that claims conformance to this SOP Class as an
SCU must provide all Required Attributes as specified in
`table_title <#table_F.7.2-1>`__. Optional Attributes maintained by the
SCP may be provided as well. The Application Entity that claims
conformance as an SCP to this SOP Class shall support the subset of the
Modality Performed Procedure Step Attributes specified in
`table_title <#table_F.7.2-1>`__.

.. table:: Modality Performed Procedure Step Enhanced Code Value Macro
with no N-SET

   +-------------+-------------+-------------+-------------+-------------+
   | Attribute   | Tag         | Req. Type   | Req. Type   | Requirement |
   | Name        |             | N-CREATE    | N-SET       | Type Final  |
   |             |             | (SCU/SCP)   | (SCU/SCP)   | State (see  |
   |             |             |             |             | Note 1)     |
   +=============+=============+=============+=============+=============+
   | *Include*\  |             |             |             |             |
   | `table_titl |             |             |             |             |
   | e <#table_F |             |             |             |             |
   | .7.2-1b>`__ |             |             |             |             |
   +-------------+-------------+-------------+-------------+-------------+
   | Equivalent  | (0008,0121) | 3/3         | Not allowed |             |
   | Code        |             |             |             |             |
   | Sequence    |             |             |             |             |
   +-------------+-------------+-------------+-------------+-------------+
   | *           |             |             |             |             |
   | >Include*\  |             |             |             |             |
   | `table_titl |             |             |             |             |
   | e <#table_F |             |             |             |             |
   | .7.2-1b>`__ |             |             |             |             |
   +-------------+-------------+-------------+-------------+-------------+

.. table:: Modality Performed Procedure Step Simple Code Value Macro
with no N-SET

   +-------------+-------------+-------------+-------------+-------------+
   | Attribute   | Tag         | Req. Type   | Req. Type   | Requirement |
   | Name        |             | N-CREATE    | N-SET       | Type Final  |
   |             |             | (SCU/SCP)   | (SCU/SCP)   | State (see  |
   |             |             |             |             | Note 1)     |
   +=============+=============+=============+=============+=============+
   | Code Value  | (0008,0100) | 1C/1C       | Not allowed |             |
   |             |             |             |             |             |
   |             |             | Shall be    |             |             |
   |             |             | present if  |             |             |
   |             |             | the code    |             |             |
   |             |             | value       |             |             |
   |             |             | length is   |             |             |
   |             |             | 16          |             |             |
   |             |             | characters  |             |             |
   |             |             | or less,    |             |             |
   |             |             | and the     |             |             |
   |             |             | code value  |             |             |
   |             |             | is not a    |             |             |
   |             |             | URN or URL. |             |             |
   +-------------+-------------+-------------+-------------+-------------+
   | Coding      | (0008,0102) | 1C/1C       | Not allowed |             |
   | Scheme      |             |             |             |             |
   | Designator  |             | Shall be    |             |             |
   |             |             | present if  |             |             |
   |             |             | Code Value  |             |             |
   |             |             | (0008,0100) |             |             |
   |             |             | or Long     |             |             |
   |             |             | Code Value  |             |             |
   |             |             | (0008,0119) |             |             |
   |             |             | is present. |             |             |
   |             |             | May be      |             |             |
   |             |             | present     |             |             |
   |             |             | otherwise.  |             |             |
   +-------------+-------------+-------------+-------------+-------------+
   | Coding      | (0008,0103) | 1C/1C       | Not allowed |             |
   | Scheme      |             |             |             |             |
   | Version     |             | Shall be    |             |             |
   |             |             | present if  |             |             |
   |             |             | the value   |             |             |
   |             |             | of Coding   |             |             |
   |             |             | Scheme      |             |             |
   |             |             | Designator  |             |             |
   |             |             | (0008,0102) |             |             |
   |             |             | is present  |             |             |
   |             |             | and is not  |             |             |
   |             |             | sufficient  |             |             |
   |             |             | to identify |             |             |
   |             |             | the Code    |             |             |
   |             |             | Value       |             |             |
   |             |             | (0008,0100) |             |             |
   |             |             | or Long     |             |             |
   |             |             | Code Value  |             |             |
   |             |             | (0008,0119) |             |             |
   |             |             | or URN Code |             |             |
   |             |             | Value       |             |             |
   |             |             | (0008,0120) |             |             |
   |             |             | una         |             |             |
   |             |             | mbiguously. |             |             |
   |             |             | Shall not   |             |             |
   |             |             | be present  |             |             |
   |             |             | if Coding   |             |             |
   |             |             | Scheme      |             |             |
   |             |             | Designator  |             |             |
   |             |             | (0008,0102) |             |             |
   |             |             | is absent.  |             |             |
   |             |             | May be      |             |             |
   |             |             | present     |             |             |
   |             |             | otherwise.  |             |             |
   +-------------+-------------+-------------+-------------+-------------+
   | Code        | (0008,0104) | 1/1         | Not allowed |             |
   | Meaning     |             |             |             |             |
   +-------------+-------------+-------------+-------------+-------------+
   | Long Code   | (0008,0119) | 1C/1C       | Not allowed |             |
   | Value       |             |             |             |             |
   |             |             | Shall be    |             |             |
   |             |             | present if  |             |             |
   |             |             | Code Value  |             |             |
   |             |             | (0008,0100) |             |             |
   |             |             | is not      |             |             |
   |             |             | present,    |             |             |
   |             |             | and the     |             |             |
   |             |             | code value  |             |             |
   |             |             | is not a    |             |             |
   |             |             | URN or URL. |             |             |
   +-------------+-------------+-------------+-------------+-------------+
   | URN Code    | (0008,0120) | 1C/1C       | Not allowed |             |
   | Value       |             |             |             |             |
   |             |             | Shall be    |             |             |
   |             |             | present if  |             |             |
   |             |             | Code Value  |             |             |
   |             |             | (0008,0100) |             |             |
   |             |             | is not      |             |             |
   |             |             | present,    |             |             |
   |             |             | and the     |             |             |
   |             |             | code value  |             |             |
   |             |             | is a URN or |             |             |
   |             |             | URL.        |             |             |
   +-------------+-------------+-------------+-------------+-------------+
   | Mapping     | (0008,0105) | 3/3         | Not allowed |             |
   | Resource    |             |             |             |             |
   +-------------+-------------+-------------+-------------+-------------+
   | Mapping     | (0008,0118) | 3/3         | Not allowed |             |
   | Resource    |             |             |             |             |
   | UID         |             |             |             |             |
   +-------------+-------------+-------------+-------------+-------------+
   | Context     | (0008,0118) | 3/3         | Not allowed |             |
   | Group       |             |             |             |             |
   | Version     |             |             |             |             |
   +-------------+-------------+-------------+-------------+-------------+
   | Context     | (0008,010B) | 3/3         | Not allowed |             |
   | Group       |             |             |             |             |
   | Extension   |             |             |             |             |
   | Flag        |             |             |             |             |
   +-------------+-------------+-------------+-------------+-------------+
   | Context     | (0008,0107) | 3/3         | Not allowed |             |
   | Group Local |             |             |             |             |
   | Version     |             |             |             |             |
   +-------------+-------------+-------------+-------------+-------------+
   | Context     | (0008,010D) | 3/3         | Not allowed |             |
   | Group       |             |             |             |             |
   | Extension   |             |             |             |             |
   | Creator UID |             |             |             |             |
   +-------------+-------------+-------------+-------------+-------------+

.. table:: Modality Performed Procedure Step Enhanced Code Value Macro
with N-SET, Mandatory Meaning

   +-------------+-------------+-------------+-------------+-------------+
   | Attribute   | Tag         | Req. Type   | Req. Type   | Requirement |
   | Name        |             | N-CREATE    | N-SET       | Type Final  |
   |             |             | (SCU/SCP)   | (SCU/SCP)   | State (see  |
   |             |             |             |             | Note 1)     |
   +=============+=============+=============+=============+=============+
   | *           |             |             |             |             |
   | >Include*\  |             |             |             |             |
   | `table_titl |             |             |             |             |
   | e <#table_F |             |             |             |             |
   | .7.2-1d>`__ |             |             |             |             |
   +-------------+-------------+-------------+-------------+-------------+
   | Equivalent  | (0008,0121) | 3/3         | 3/3         |             |
   | Code        |             |             |             |             |
   | Sequence    |             |             |             |             |
   +-------------+-------------+-------------+-------------+-------------+
   | *           |             |             |             |             |
   | >Include*\  |             |             |             |             |
   | `table_titl |             |             |             |             |
   | e <#table_F |             |             |             |             |
   | .7.2-1d>`__ |             |             |             |             |
   +-------------+-------------+-------------+-------------+-------------+

.. table:: Modality Performed Procedure Step Simple Code Value Macro
with N-SET, Mandatory Meaning

   +-------------+-------------+-------------+-------------+-------------+
   | Attribute   | Tag         | Req. Type   | Req. Type   | Requirement |
   | Name        |             | N-CREATE    | N-SET       | Type Final  |
   |             |             | (SCU/SCP)   | (SCU/SCP)   | State (see  |
   |             |             |             |             | Note 1)     |
   +=============+=============+=============+=============+=============+
   | Code Value  | (0008,0100) | 1C/1C       | 3/1C        |             |
   |             |             |             |             |             |
   |             |             | Shall be    | Shall be    |             |
   |             |             | present if  | present if  |             |
   |             |             | the code    | the code    |             |
   |             |             | value       | value       |             |
   |             |             | length is   | length is   |             |
   |             |             | 16          | 16          |             |
   |             |             | characters  | characters  |             |
   |             |             | or less,    | or less,    |             |
   |             |             | and the     | and the     |             |
   |             |             | code value  | code value  |             |
   |             |             | is not a    | is not a    |             |
   |             |             | URN or URL. | URN or URL. |             |
   +-------------+-------------+-------------+-------------+-------------+
   | Coding      | (0008,0102) | 1C/1C       | 1C/1C       |             |
   | Scheme      |             |             |             |             |
   | Designator  |             | Shall be    | Shall be    |             |
   |             |             | present if  | present if  |             |
   |             |             | Code Value  | Code Value  |             |
   |             |             | (0008,0100) | (0008,0100) |             |
   |             |             | or Long     | or Long     |             |
   |             |             | Code Value  | Code Value  |             |
   |             |             | (0008,0119) | (0008,0119) |             |
   |             |             | is present. | is present. |             |
   |             |             | May be      | May be      |             |
   |             |             | present     | present     |             |
   |             |             | otherwise.  | otherwise.  |             |
   +-------------+-------------+-------------+-------------+-------------+
   | Coding      | (0008,0103) | 1C/1C       | 1C/1C       |             |
   | Scheme      |             |             |             |             |
   | Version     |             | Shall be    | Shall be    |             |
   |             |             | present if  | present if  |             |
   |             |             | the value   | the value   |             |
   |             |             | of Coding   | of Coding   |             |
   |             |             | Scheme      | Scheme      |             |
   |             |             | Designator  | Designator  |             |
   |             |             | (0008,0102) | (0008,0102) |             |
   |             |             | is present  | is present  |             |
   |             |             | and is not  | and is not  |             |
   |             |             | sufficient  | sufficient  |             |
   |             |             | to identify | to identify |             |
   |             |             | the Code    | the Code    |             |
   |             |             | Value       | Value       |             |
   |             |             | (0008,0100) | (0008,0100) |             |
   |             |             | or Long     | or Long     |             |
   |             |             | Code Value  | Code Value  |             |
   |             |             | (0008,0119) | (0008,0119) |             |
   |             |             | or URN Code | or URN Code |             |
   |             |             | Value       | Value       |             |
   |             |             | (0008,0120) | (0008,0120) |             |
   |             |             | una         | una         |             |
   |             |             | mbiguously. | mbiguously. |             |
   |             |             | Shall not   | Shall not   |             |
   |             |             | be present  | be present  |             |
   |             |             | if Coding   | if Coding   |             |
   |             |             | Scheme      | Scheme      |             |
   |             |             | Designator  | Designator  |             |
   |             |             | (0008,0102) | (0008,0102) |             |
   |             |             | is absent.  | is absent.  |             |
   |             |             | May be      | May be      |             |
   |             |             | present     | present     |             |
   |             |             | otherwise.  | otherwise.  |             |
   +-------------+-------------+-------------+-------------+-------------+
   | Code        | (0008,0104) | 1/1         | 1/1         |             |
   | Meaning     |             |             |             |             |
   +-------------+-------------+-------------+-------------+-------------+
   | Long Code   | (0008,0119) | 1C/1C       | 3/1C        |             |
   | Value       |             |             |             |             |
   |             |             | Shall be    | Shall be    |             |
   |             |             | present if  | present if  |             |
   |             |             | Code Value  | Code Value  |             |
   |             |             | (0008,0100) | (0008,0100) |             |
   |             |             | is not      | is not      |             |
   |             |             | present,    | present,    |             |
   |             |             | and the     | and the     |             |
   |             |             | code value  | code value  |             |
   |             |             | is not a    | is not a    |             |
   |             |             | URN or URL. | URN or URL. |             |
   +-------------+-------------+-------------+-------------+-------------+
   | URN Code    | (0008,0120) | 1C/1C       | 3/1C        |             |
   | Value       |             |             |             |             |
   |             |             | Shall be    | Shall be    |             |
   |             |             | present if  | present if  |             |
   |             |             | Code Value  | Code Value  |             |
   |             |             | (0008,0100) | (0008,0100) |             |
   |             |             | is not      | is not      |             |
   |             |             | present,    | present,    |             |
   |             |             | and the     | and the     |             |
   |             |             | code value  | code value  |             |
   |             |             | is a URN or | is a URN or |             |
   |             |             | URL.        | URL.        |             |
   +-------------+-------------+-------------+-------------+-------------+
   | Mapping     | (0008,0105) | 3/3         | 3/3         |             |
   | Resource    |             |             |             |             |
   +-------------+-------------+-------------+-------------+-------------+
   | Mapping     | (0008,0118) | 3/3         | 3/3         |             |
   | Resource    |             |             |             |             |
   | UID         |             |             |             |             |
   +-------------+-------------+-------------+-------------+-------------+
   | Context     | (0008,0118) | 3/3         | 3/3         |             |
   | Group       |             |             |             |             |
   | Version     |             |             |             |             |
   +-------------+-------------+-------------+-------------+-------------+
   | Context     | (0008,010B) | 3/3         | 3/3         |             |
   | Group       |             |             |             |             |
   | Extension   |             |             |             |             |
   | Flag        |             |             |             |             |
   +-------------+-------------+-------------+-------------+-------------+
   | Context     | (0008,0107) | 3/3         | 3/3         |             |
   | Group Local |             |             |             |             |
   | Version     |             |             |             |             |
   +-------------+-------------+-------------+-------------+-------------+
   | Context     | (0008,010D) | 3/3         | 3/3         |             |
   | Group       |             |             |             |             |
   | Extension   |             |             |             |             |
   | Creator UID |             |             |             |             |
   +-------------+-------------+-------------+-------------+-------------+

.. table:: Modality Performed Procedure Step Enhanced Code Value Macro
with N-SET, Optional Meaning

   +-------------+-------------+-------------+-------------+-------------+
   | Attribute   | Tag         | Req. Type   | Req. Type   | Requirement |
   | Name        |             | N-CREATE    | N-SET       | Type Final  |
   |             |             | (SCU/SCP)   | (SCU/SCP)   | State (see  |
   |             |             |             |             | Note 1)     |
   +=============+=============+=============+=============+=============+
   | *           |             |             |             |             |
   | >Include*\  |             |             |             |             |
   | `table_titl |             |             |             |             |
   | e <#table_F |             |             |             |             |
   | .7.2-1f>`__ |             |             |             |             |
   +-------------+-------------+-------------+-------------+-------------+
   | Equivalent  | (0008,0121) | 3/3         | 3/3         |             |
   | Code        |             |             |             |             |
   | Sequence    |             |             |             |             |
   +-------------+-------------+-------------+-------------+-------------+
   | *           |             |             |             |             |
   | >Include*\  |             |             |             |             |
   | `table_titl |             |             |             |             |
   | e <#table_F |             |             |             |             |
   | .7.2-1f>`__ |             |             |             |             |
   +-------------+-------------+-------------+-------------+-------------+

.. table:: Modality Performed Procedure Step Simple Code Value Macro
with N-SET, Optional Meaning

   +-------------+-------------+-------------+-------------+-------------+
   | Attribute   | Tag         | Req. Type   | Req. Type   | Requirement |
   | Name        |             | N-CREATE    | N-SET       | Type Final  |
   |             |             | (SCU/SCP)   | (SCU/SCP)   | State (see  |
   |             |             |             |             | Note 1)     |
   +=============+=============+=============+=============+=============+
   | Code Value  | (0008,0100) | 1C/1C       | 3/1C        |             |
   |             |             |             |             |             |
   |             |             | Shall be    | Shall be    |             |
   |             |             | present if  | present if  |             |
   |             |             | the code    | the code    |             |
   |             |             | value       | value       |             |
   |             |             | length is   | length is   |             |
   |             |             | 16          | 16          |             |
   |             |             | characters  | characters  |             |
   |             |             | or less,    | or less,    |             |
   |             |             | and the     | and the     |             |
   |             |             | code value  | code value  |             |
   |             |             | is not a    | is not a    |             |
   |             |             | URN or URL. | URN or URL. |             |
   +-------------+-------------+-------------+-------------+-------------+
   | Coding      | (0008,0102) | 1C/1C       | 1C/1C       |             |
   | Scheme      |             |             |             |             |
   | Designator  |             | Shall be    | Shall be    |             |
   |             |             | present if  | present if  |             |
   |             |             | Code Value  | Code Value  |             |
   |             |             | (0008,0100) | (0008,0100) |             |
   |             |             | or Long     | or Long     |             |
   |             |             | Code Value  | Code Value  |             |
   |             |             | (0008,0119) | (0008,0119) |             |
   |             |             | is present. | is present. |             |
   |             |             | May be      | May be      |             |
   |             |             | present     | present     |             |
   |             |             | otherwise.  | otherwise.  |             |
   +-------------+-------------+-------------+-------------+-------------+
   | Coding      | (0008,0103) | 1C/1C       | 1C/1C       |             |
   | Scheme      |             |             |             |             |
   | Version     |             | Shall be    | Shall be    |             |
   |             |             | present if  | present if  |             |
   |             |             | the value   | the value   |             |
   |             |             | of Coding   | of Coding   |             |
   |             |             | Scheme      | Scheme      |             |
   |             |             | Designator  | Designator  |             |
   |             |             | (0008,0102) | (0008,0102) |             |
   |             |             | is present  | is present  |             |
   |             |             | and is not  | and is not  |             |
   |             |             | sufficient  | sufficient  |             |
   |             |             | to identify | to identify |             |
   |             |             | the Code    | the Code    |             |
   |             |             | Value       | Value       |             |
   |             |             | (0008,0100) | (0008,0100) |             |
   |             |             | or Long     | or Long     |             |
   |             |             | Code Value  | Code Value  |             |
   |             |             | (0008,0119) | (0008,0119) |             |
   |             |             | or URN Code | or URN Code |             |
   |             |             | Value       | Value       |             |
   |             |             | (0008,0120) | (0008,0120) |             |
   |             |             | una         | una         |             |
   |             |             | mbiguously. | mbiguously. |             |
   |             |             | Shall not   | Shall not   |             |
   |             |             | be present  | be present  |             |
   |             |             | if Coding   | if Coding   |             |
   |             |             | Scheme      | Scheme      |             |
   |             |             | Designator  | Designator  |             |
   |             |             | (0008,0102) | (0008,0102) |             |
   |             |             | is absent.  | is absent.  |             |
   |             |             | May be      | May be      |             |
   |             |             | present     | present     |             |
   |             |             | otherwise.  | otherwise.  |             |
   +-------------+-------------+-------------+-------------+-------------+
   | Code        | (0008,0104) | 3/3         | 3/3         |             |
   | Meaning     |             |             |             |             |
   +-------------+-------------+-------------+-------------+-------------+
   | Long Code   | (0008,0119) | 1C/1C       | 3/1C        |             |
   | Value       |             |             |             |             |
   |             |             | Shall be    | Shall be    |             |
   |             |             | present if  | present if  |             |
   |             |             | Code Value  | Code Value  |             |
   |             |             | (0008,0100) | (0008,0100) |             |
   |             |             | is not      | is not      |             |
   |             |             | present,    | present,    |             |
   |             |             | and the     | and the     |             |
   |             |             | code value  | code value  |             |
   |             |             | is not a    | is not a    |             |
   |             |             | URN or URL. | URN or URL. |             |
   +-------------+-------------+-------------+-------------+-------------+
   | URN Code    | (0008,0120) | 1C/1C       | 3/1C        |             |
   | Value       |             |             |             |             |
   |             |             | Shall be    | Shall be    |             |
   |             |             | present if  | present if  |             |
   |             |             | Code Value  | Code Value  |             |
   |             |             | (0008,0100) | (0008,0100) |             |
   |             |             | is not      | is not      |             |
   |             |             | present,    | present,    |             |
   |             |             | and the     | and the     |             |
   |             |             | code value  | code value  |             |
   |             |             | is a URN or | is a URN or |             |
   |             |             | URL.        | URL.        |             |
   +-------------+-------------+-------------+-------------+-------------+
   | Mapping     | (0008,0105) | 3/3         | 3/3         |             |
   | Resource    |             |             |             |             |
   +-------------+-------------+-------------+-------------+-------------+
   | Mapping     | (0008,0118) | 3/3         | 3/3         |             |
   | Resource    |             |             |             |             |
   | UID         |             |             |             |             |
   +-------------+-------------+-------------+-------------+-------------+
   | Context     | (0008,0118) | 3/3         | 3/3         |             |
   | Group       |             |             |             |             |
   | Version     |             |             |             |             |
   +-------------+-------------+-------------+-------------+-------------+
   | Context     | (0008,010B) | 3/3         | 3/3         |             |
   | Group       |             |             |             |             |
   | Extension   |             |             |             |             |
   | Flag        |             |             |             |             |
   +-------------+-------------+-------------+-------------+-------------+
   | Context     | (0008,0107) | 3/3         | 3/3         |             |
   | Group Local |             |             |             |             |
   | Version     |             |             |             |             |
   +-------------+-------------+-------------+-------------+-------------+
   | Context     | (0008,010D) | 3/3         | 3/3         |             |
   | Group       |             |             |             |             |
   | Extension   |             |             |             |             |
   | Creator UID |             |             |             |             |
   +-------------+-------------+-------------+-------------+-------------+

.. table:: Modality Performed Procedure Step SOP Class N-CREATE, N-SET
and Final State Attributes

   +-------------+-------------+-------------+-------------+-------------+
   | Attribute   | Tag         | Req. Type   | Req. Type   | Requirement |
   | Name        |             | N-CREATE    | N-SET       | Type Final  |
   |             |             | (SCU/SCP)   | (SCU/SCP)   | State (see  |
   |             |             |             |             | Note 1)     |
   +=============+=============+=============+=============+=============+
   | Specific    | (0008,0005) | 1C/1C       | 1C/1C       |             |
   | Character   |             |             |             |             |
   | Set         |             | (Required   | (Required   |             |
   |             |             | if an       | if an       |             |
   |             |             | extended or | extended or |             |
   |             |             | replacement | replacement |             |
   |             |             | character   | character   |             |
   |             |             | set is      | set is used |             |
   |             |             | used)       | in an       |             |
   |             |             |             | Attribute   |             |
   |             |             |             | that is     |             |
   |             |             |             | set)        |             |
   +-------------+-------------+-------------+-------------+-------------+
   | **Performed |             |             |             |             |
   | Procedure   |             |             |             |             |
   | Step        |             |             |             |             |
   | Rel         |             |             |             |             |
   | ationship** |             |             |             |             |
   +-------------+-------------+-------------+-------------+-------------+
   | Scheduled   | (0040,0270) | 1/1         | Not allowed |             |
   | Step        |             |             |             |             |
   | Attribute   |             |             |             |             |
   | Sequence    |             |             |             |             |
   +-------------+-------------+-------------+-------------+-------------+
   | >Study      | (0020,000D) | 1/1         | Not allowed |             |
   | Instance    |             |             |             |             |
   | UID         |             |             |             |             |
   +-------------+-------------+-------------+-------------+-------------+
   | >Referenced | (0008,1110) | 2/2         | Not allowed |             |
   | Study       |             |             |             |             |
   | Sequence    |             |             |             |             |
   +-------------+-------------+-------------+-------------+-------------+
   | >           | (0008,1150) | 1/1         | Not allowed |             |
   | >Referenced |             |             |             |             |
   | SOP Class   |             |             |             |             |
   | UID         |             |             |             |             |
   +-------------+-------------+-------------+-------------+-------------+
   | >           | (0008,1155) | 1/1         | Not allowed |             |
   | >Referenced |             |             |             |             |
   | SOP         |             |             |             |             |
   | Instance    |             |             |             |             |
   | UID         |             |             |             |             |
   +-------------+-------------+-------------+-------------+-------------+
   | >Accession  | (0008,0050) | 2/2         | Not allowed |             |
   | Number      |             |             |             |             |
   +-------------+-------------+-------------+-------------+-------------+
   | >Issuer of  | (0008,0051) | 3/3         | Not allowed |             |
   | Accession   |             |             |             |             |
   | Number      |             |             |             |             |
   | Sequence    |             |             |             |             |
   +-------------+-------------+-------------+-------------+-------------+
   | >>Local     | (0040,0031) | 1C/1C       | Not allowed |             |
   | Namespace   |             |             |             |             |
   | Entity ID   |             | Required if |             |             |
   |             |             | Universal   |             |             |
   |             |             | Entity ID   |             |             |
   |             |             | (0040,0032) |             |             |
   |             |             | is not      |             |             |
   |             |             | present;    |             |             |
   |             |             | may be      |             |             |
   |             |             | present     |             |             |
   |             |             | otherwise   |             |             |
   +-------------+-------------+-------------+-------------+-------------+
   | >>Universal | (0040,0032) | 1C/1C       | Not allowed |             |
   | Entity ID   |             |             |             |             |
   |             |             | Required if |             |             |
   |             |             | Local       |             |             |
   |             |             | Namespace   |             |             |
   |             |             | Entity ID   |             |             |
   |             |             | (0040,0031) |             |             |
   |             |             | is not      |             |             |
   |             |             | present;    |             |             |
   |             |             | may be      |             |             |
   |             |             | present     |             |             |
   |             |             | otherwise.  |             |             |
   +-------------+-------------+-------------+-------------+-------------+
   | >>Universal | (0040,0033) | 1C/1C       | Not allowed |             |
   | Entity ID   |             |             |             |             |
   | Type        |             | Required if |             |             |
   |             |             | Universal   |             |             |
   |             |             | Entity ID   |             |             |
   |             |             | (0040,0032) |             |             |
   |             |             | is present. |             |             |
   +-------------+-------------+-------------+-------------+-------------+
   | >Placer     | (0040,2016) | 3/3         | Not allowed |             |
   | Order       |             |             |             |             |
   | Num         |             |             |             |             |
   | ber/Imaging |             |             |             |             |
   | Service     |             |             |             |             |
   | Request     |             |             |             |             |
   +-------------+-------------+-------------+-------------+-------------+
   | >Order      | (0040,0026) | 3/3         | Not allowed |             |
   | Placer      |             |             |             |             |
   | Identifier  |             |             |             |             |
   | Sequence    |             |             |             |             |
   +-------------+-------------+-------------+-------------+-------------+
   | >>Local     | (0040,0031) | 1C/1C       | Not allowed |             |
   | Namespace   |             |             |             |             |
   | Entity ID   |             | Required if |             |             |
   |             |             | Universal   |             |             |
   |             |             | Entity ID   |             |             |
   |             |             | (0040,0032) |             |             |
   |             |             | is not      |             |             |
   |             |             | present;    |             |             |
   |             |             | may be      |             |             |
   |             |             | present     |             |             |
   |             |             | otherwise   |             |             |
   +-------------+-------------+-------------+-------------+-------------+
   | >>Universal | (0040,0032) | 1C/1C       | Not allowed |             |
   | Entity ID   |             |             |             |             |
   |             |             | Required if |             |             |
   |             |             | Local       |             |             |
   |             |             | Namespace   |             |             |
   |             |             | Entity ID   |             |             |
   |             |             | (0040,0031) |             |             |
   |             |             | is not      |             |             |
   |             |             | present;    |             |             |
   |             |             | may be      |             |             |
   |             |             | present     |             |             |
   |             |             | otherwise.. |             |             |
   +-------------+-------------+-------------+-------------+-------------+
   | >>Universal | (0040,0033) | 1C/1C       | Not allowed |             |
   | Entity ID   |             |             |             |             |
   | Type        |             | Required if |             |             |
   |             |             | Universal   |             |             |
   |             |             | Entity ID   |             |             |
   |             |             | (0040,0032) |             |             |
   |             |             | is present. |             |             |
   +-------------+-------------+-------------+-------------+-------------+
   | >Filler     | (0040,2017) | 3/3         | Not allowed |             |
   | Order       |             |             |             |             |
   | Num         |             |             |             |             |
   | ber/Imaging |             |             |             |             |
   | Service     |             |             |             |             |
   | Request     |             |             |             |             |
   +-------------+-------------+-------------+-------------+-------------+
   | >Order      | (0040,0027) | 3/3         | Not allowed |             |
   | Filler      |             |             |             |             |
   | Identifier  |             |             |             |             |
   | Sequence    |             |             |             |             |
   +-------------+-------------+-------------+-------------+-------------+
   | >>Local     | (0040,0031) | 1C/1C       | Not allowed |             |
   | Namespace   |             |             |             |             |
   | Entity ID   |             | Required if |             |             |
   |             |             | Universal   |             |             |
   |             |             | Entity ID   |             |             |
   |             |             | (0040,0032) |             |             |
   |             |             | is not      |             |             |
   |             |             | present;    |             |             |
   |             |             | may be      |             |             |
   |             |             | present     |             |             |
   |             |             | otherwise   |             |             |
   +-------------+-------------+-------------+-------------+-------------+
   | >>Universal | (0040,0032) | 1C/1C       | Not allowed |             |
   | Entity ID   |             |             |             |             |
   |             |             | Required if |             |             |
   |             |             | Local       |             |             |
   |             |             | Namespace   |             |             |
   |             |             | Entity ID   |             |             |
   |             |             | (0040,0031) |             |             |
   |             |             | is not      |             |             |
   |             |             | present;    |             |             |
   |             |             | may be      |             |             |
   |             |             | present     |             |             |
   |             |             | otherwise.. |             |             |
   +-------------+-------------+-------------+-------------+-------------+
   | >>Universal | (0040,0033) | 1C/1C       | Not allowed |             |
   | Entity ID   |             |             |             |             |
   | Type        |             | Required if |             |             |
   |             |             | Universal   |             |             |
   |             |             | Entity ID   |             |             |
   |             |             | (0040,0032) |             |             |
   |             |             | is present. |             |             |
   +-------------+-------------+-------------+-------------+-------------+
   | >Requested  | (0040,1001) | 2/2         | Not allowed |             |
   | Procedure   |             |             |             |             |
   | ID          |             |             |             |             |
   +-------------+-------------+-------------+-------------+-------------+
   | >Requested  | (0032,1064) | 3/3         | Not allowed |             |
   | Procedure   |             |             |             |             |
   | Code        |             |             |             |             |
   | Sequence    |             |             |             |             |
   +-------------+-------------+-------------+-------------+-------------+
   | *>          |             |             |             |             |
   | >Include*\  |             |             |             |             |
   | `table_titl |             |             |             |             |
   | e <#table_F |             |             |             |             |
   | .7.2-1a>`__ |             |             |             |             |
   +-------------+-------------+-------------+-------------+-------------+
   | >Requested  | (0032,1060) | 2/2         | Not allowed |             |
   | Procedure   |             |             |             |             |
   | Description |             |             |             |             |
   +-------------+-------------+-------------+-------------+-------------+
   | >Scheduled  | (0040,0009) | 2/2         | Not allowed |             |
   | Procedure   |             |             |             |             |
   | Step ID     |             |             |             |             |
   +-------------+-------------+-------------+-------------+-------------+
   | >Scheduled  | (0040,0007) | 2/2         | Not allowed |             |
   | Procedure   |             |             |             |             |
   | Step        |             |             |             |             |
   | Description |             |             |             |             |
   +-------------+-------------+-------------+-------------+-------------+
   | >Scheduled  | (0040,0008) | 2/2         | Not allowed |             |
   | Protocol    |             |             |             |             |
   | Code        |             |             |             |             |
   | Sequence    |             |             |             |             |
   +-------------+-------------+-------------+-------------+-------------+
   | *>          |             |             |             |             |
   | >Include*\  |             |             |             |             |
   | `table_titl |             |             |             |             |
   | e <#table_F |             |             |             |             |
   | .7.2-1a>`__ |             |             |             |             |
   +-------------+-------------+-------------+-------------+-------------+
   | Patient's   | (0010,0010) | 2/2         | Not allowed |             |
   | Name        |             |             |             |             |
   +-------------+-------------+-------------+-------------+-------------+
   | Patient ID  | (0010,0020) | 2/2         | Not allowed |             |
   +-------------+-------------+-------------+-------------+-------------+
   | Issuer of   | (0010,0021) | 3/3         | Not allowed |             |
   | Patient ID  |             |             |             |             |
   +-------------+-------------+-------------+-------------+-------------+
   | Issuer of   | (0010,0024) | 3/3         | Not allowed |             |
   | Patient ID  |             |             |             |             |
   | Qualifiers  |             |             |             |             |
   | Sequence    |             |             |             |             |
   +-------------+-------------+-------------+-------------+-------------+
   | >Universal  | (0040,0032) | 3/3         | Not allowed |             |
   | Entity ID   |             |             |             |             |
   +-------------+-------------+-------------+-------------+-------------+
   | >Universal  | (0040,0033) | 1C/1C       | Not allowed |             |
   | Entity ID   |             |             |             |             |
   | Type        |             | Required if |             |             |
   |             |             | Universal   |             |             |
   |             |             | Entity ID   |             |             |
   |             |             | (0040,0032) |             |             |
   |             |             | is present. |             |             |
   +-------------+-------------+-------------+-------------+-------------+
   | *>All other |             | 3/3         | Not allowed |             |
   | Attributes  |             |             |             |             |
   | of the      |             |             |             |             |
   | Issuer of   |             |             |             |             |
   | Patient ID  |             |             |             |             |
   | Qualifiers  |             |             |             |             |
   | Sequence*   |             |             |             |             |
   +-------------+-------------+-------------+-------------+-------------+
   | Other       | (0010,1002) | 3/3         | Not allowed |             |
   | Patient IDs |             |             |             |             |
   | Sequence    |             |             |             |             |
   +-------------+-------------+-------------+-------------+-------------+
   | >Patient ID | (0010,0020) | 3/3         | Not allowed |             |
   +-------------+-------------+-------------+-------------+-------------+
   | >Issuer of  | (0010,0021) | 3/3         | Not allowed |             |
   | Patient ID  |             |             |             |             |
   +-------------+-------------+-------------+-------------+-------------+
   | >Issuer of  | (0010,0024) | 3/3         | Not allowed |             |
   | Patient ID  |             |             |             |             |
   | Qualifiers  |             |             |             |             |
   | Sequence    |             |             |             |             |
   +-------------+-------------+-------------+-------------+-------------+
   | *>>All      |             | 3/3         | Not allowed |             |
   | other       |             |             |             |             |
   | Attributes  |             |             |             |             |
   | of the      |             |             |             |             |
   | Issuer of   |             |             |             |             |
   | Patient ID  |             |             |             |             |
   | Qualifiers  |             |             |             |             |
   | Sequence*   |             |             |             |             |
   +-------------+-------------+-------------+-------------+-------------+
   | >Type of    | (0010,0022) | 3/3         | Not allowed |             |
   | Patient ID  |             |             |             |             |
   +-------------+-------------+-------------+-------------+-------------+
   | Patient's   | (0010,0030) | 2/2         | Not allowed |             |
   | Birth Date  |             |             |             |             |
   +-------------+-------------+-------------+-------------+-------------+
   | Patient's   | (0010,0040) | 2/2         | Not allowed |             |
   | Sex         |             |             |             |             |
   +-------------+-------------+-------------+-------------+-------------+
   | Referenced  | (0008,1120) | 2/2         | Not allowed |             |
   | Patient     |             |             |             |             |
   | Sequence    |             |             |             |             |
   +-------------+-------------+-------------+-------------+-------------+
   | >Referenced | (0008,1150) | 1/1         | Not allowed |             |
   | SOP Class   |             |             |             |             |
   | UID         |             |             |             |             |
   +-------------+-------------+-------------+-------------+-------------+
   | >Referenced | (0008,1155) | 1/1         | Not allowed |             |
   | Instance    |             |             |             |             |
   | UID         |             |             |             |             |
   +-------------+-------------+-------------+-------------+-------------+
   | Admission   | (0038,0010) | 3/3         | Not Allowed |             |
   | ID          |             |             |             |             |
   +-------------+-------------+-------------+-------------+-------------+
   | Issuer of   | (0038,0014) | 3/3         | Not allowed |             |
   | Admission   |             |             |             |             |
   | ID Sequence |             |             |             |             |
   +-------------+-------------+-------------+-------------+-------------+
   | >Local      | (0040,0031) | 1C/1C       | Not allowed |             |
   | Namespace   |             |             |             |             |
   | Entity ID   |             | Required if |             |             |
   |             |             | Universal   |             |             |
   |             |             | Entity ID   |             |             |
   |             |             | (0040,0032) |             |             |
   |             |             | is not      |             |             |
   |             |             | present;    |             |             |
   |             |             | may be      |             |             |
   |             |             | present     |             |             |
   |             |             | otherwise   |             |             |
   +-------------+-------------+-------------+-------------+-------------+
   | >Universal  | (0040,0032) | 1C/1C       | Not allowed |             |
   | Entity ID   |             |             |             |             |
   |             |             | Required if |             |             |
   |             |             | Local       |             |             |
   |             |             | Namespace   |             |             |
   |             |             | Entity ID   |             |             |
   |             |             | (0040,0031) |             |             |
   |             |             | is not      |             |             |
   |             |             | present;    |             |             |
   |             |             | may be      |             |             |
   |             |             | present     |             |             |
   |             |             | otherwise.. |             |             |
   +-------------+-------------+-------------+-------------+-------------+
   | >Universal  | (0040,0033) | 1C/1C       | Not allowed |             |
   | Entity ID   |             |             |             |             |
   | Type        |             | Required if |             |             |
   |             |             | Universal   |             |             |
   |             |             | Entity ID   |             |             |
   |             |             | (0040,0032) |             |             |
   |             |             | is present. |             |             |
   +-------------+-------------+-------------+-------------+-------------+
   | Service     | (0038,0060) | 3/3         | Not allowed |             |
   | Episode ID  |             |             |             |             |
   +-------------+-------------+-------------+-------------+-------------+
   | Issuer of   | (0038,0064) | 3/3         | Not allowed |             |
   | Service     |             |             |             |             |
   | Episode ID  |             |             |             |             |
   | Sequence    |             |             |             |             |
   +-------------+-------------+-------------+-------------+-------------+
   | >Local      | (0040,0031) | 1C/1C       | Not allowed |             |
   | Namespace   |             |             |             |             |
   | Entity ID   |             | Required if |             |             |
   |             |             | Universal   |             |             |
   |             |             | Entity ID   |             |             |
   |             |             | (0040,0032) |             |             |
   |             |             | is not      |             |             |
   |             |             | present;    |             |             |
   |             |             | may be      |             |             |
   |             |             | present     |             |             |
   |             |             | otherwise   |             |             |
   +-------------+-------------+-------------+-------------+-------------+
   | >Universal  | (0040,0032) | 1C/1C       | Not allowed |             |
   | Entity ID   |             |             |             |             |
   |             |             | Required if |             |             |
   |             |             | Local       |             |             |
   |             |             | Namespace   |             |             |
   |             |             | Entity ID   |             |             |
   |             |             | (0040,0031) |             |             |
   |             |             | is not      |             |             |
   |             |             | present;    |             |             |
   |             |             | may be      |             |             |
   |             |             | present     |             |             |
   |             |             | otherwise.. |             |             |
   +-------------+-------------+-------------+-------------+-------------+
   | >Universal  | (0040,0033) | 1C/1C       | Not allowed |             |
   | Entity ID   |             |             |             |             |
   | Type        |             | Required if |             |             |
   |             |             | Universal   |             |             |
   |             |             | Entity ID   |             |             |
   |             |             | (0040,0032) |             |             |
   |             |             | is present. |             |             |
   +-------------+-------------+-------------+-------------+-------------+
   | Service     | (0038,0062) | 3/3         | Not allowed |             |
   | Episode     |             |             |             |             |
   | Description |             |             |             |             |
   +-------------+-------------+-------------+-------------+-------------+
   | **Performed |             |             |             |             |
   | Procedure   |             |             |             |             |
   | Step        |             |             |             |             |
   | In          |             |             |             |             |
   | formation** |             |             |             |             |
   +-------------+-------------+-------------+-------------+-------------+
   | Performed   | (0040,0253) | 1/1         | Not allowed |             |
   | Procedure   |             |             |             |             |
   | Step ID     |             |             |             |             |
   +-------------+-------------+-------------+-------------+-------------+
   | Performed   | (0040,0241) | 1/1         | Not allowed |             |
   | Station AE  |             |             |             |             |
   | Title       |             |             |             |             |
   +-------------+-------------+-------------+-------------+-------------+
   | Performed   | (0040,0242) | 2/2         | Not allowed |             |
   | Station     |             |             |             |             |
   | Name        |             |             |             |             |
   +-------------+-------------+-------------+-------------+-------------+
   | Performed   | (0040,0243) | 2/2         | Not allowed |             |
   | Location    |             |             |             |             |
   +-------------+-------------+-------------+-------------+-------------+
   | Performed   | (0040,0244) | 1/1         | Not allowed |             |
   | Procedure   |             |             |             |             |
   | Step Start  |             |             |             |             |
   | Date        |             |             |             |             |
   +-------------+-------------+-------------+-------------+-------------+
   | Performed   | (0040,0245) | 1/1         | Not allowed |             |
   | Procedure   |             |             |             |             |
   | Step Start  |             |             |             |             |
   | Time        |             |             |             |             |
   +-------------+-------------+-------------+-------------+-------------+
   | Performed   | (0040,0252) | 1/1         | 3/1         |             |
   | Procedure   |             |             |             |             |
   | Step Status |             |             |             |             |
   +-------------+-------------+-------------+-------------+-------------+
   | Performed   | (0040,0254) | 2/2         | 3/2         |             |
   | Procedure   |             |             |             |             |
   | Step        |             |             |             |             |
   | Description |             |             |             |             |
   +-------------+-------------+-------------+-------------+-------------+
   | Performed   | (0040,0255) | 2/2         | 3/2         |             |
   | Procedure   |             |             |             |             |
   | Type        |             |             |             |             |
   | Description |             |             |             |             |
   +-------------+-------------+-------------+-------------+-------------+
   | Procedure   | (0008,1032) | 2/2         | 3/2         |             |
   | Code        |             |             |             |             |
   | Sequence    |             |             |             |             |
   +-------------+-------------+-------------+-------------+-------------+
   | *           |             |             |             |             |
   | >Include*\  |             |             |             |             |
   | `table_titl |             |             |             |             |
   | e <#table_F |             |             |             |             |
   | .7.2-1e>`__ |             |             |             |             |
   +-------------+-------------+-------------+-------------+-------------+
   | Reason For  | (0040,1012) | 3/3         | 3/3         |             |
   | Performed   |             |             |             |             |
   | Procedure   |             |             |             |             |
   | Code        |             |             |             |             |
   | Sequence    |             |             |             |             |
   +-------------+-------------+-------------+-------------+-------------+
   | *           |             |             |             |             |
   | >Include*\  |             |             |             |             |
   | `table_titl |             |             |             |             |
   | e <#table_F |             |             |             |             |
   | .7.2-1c>`__ |             |             |             |             |
   +-------------+-------------+-------------+-------------+-------------+
   | Performed   | (0040,0250) | 2/2         | 3/1         | 1           |
   | Procedure   |             |             |             |             |
   | Step End    |             |             |             |             |
   | Date        |             |             |             |             |
   +-------------+-------------+-------------+-------------+-------------+
   | Performed   | (0040,0251) | 2/2         | 3/1         | 1           |
   | Procedure   |             |             |             |             |
   | Step End    |             |             |             |             |
   | Time        |             |             |             |             |
   +-------------+-------------+-------------+-------------+-------------+
   | Comments on | (0040,0280) | 3/3         | 3/3         |             |
   | the         |             |             |             |             |
   | Performed   |             |             |             |             |
   | Procedure   |             |             |             |             |
   | Step        |             |             |             |             |
   +-------------+-------------+-------------+-------------+-------------+
   | Performed   | (0040,0281) | 3/3         | 3/3         |             |
   | Procedure   |             |             |             |             |
   | Step        |             |             |             |             |
   | Disc        |             |             |             |             |
   | ontinuation |             |             |             |             |
   | Reason Code |             |             |             |             |
   | Sequence    |             |             |             |             |
   +-------------+-------------+-------------+-------------+-------------+
   | *           |             |             |             |             |
   | >Include*\  |             |             |             |             |
   | `table_titl |             |             |             |             |
   | e <#table_F |             |             |             |             |
   | .7.2-1c>`__ |             |             |             |             |
   +-------------+-------------+-------------+-------------+-------------+
   | **Image     |             |             |             |             |
   | Acquisition |             |             |             |             |
   | Results**   |             |             |             |             |
   +-------------+-------------+-------------+-------------+-------------+
   | Modality    | (0008,0060) | 1/1         | Not allowed |             |
   +-------------+-------------+-------------+-------------+-------------+
   | Study ID    | (0020,0010) | 2/2         | Not allowed |             |
   +-------------+-------------+-------------+-------------+-------------+
   | Performed   | (0040,0260) | 2/2         | 3/2         |             |
   | Protocol    |             |             |             |             |
   | Code        |             |             |             |             |
   | Sequence    |             |             |             |             |
   +-------------+-------------+-------------+-------------+-------------+
   | *           |             |             |             |             |
   | >Include*\  |             |             |             |             |
   | `table_titl |             |             |             |             |
   | e <#table_F |             |             |             |             |
   | .7.2-1e>`__ |             |             |             |             |
   +-------------+-------------+-------------+-------------+-------------+
   | Performed   | (0040,0340) | 2/2         | 3/1         | 1           |
   | Series      |             |             |             |             |
   | Sequence    |             |             |             | (see note   |
   |             |             |             |             | 2)          |
   +-------------+-------------+-------------+-------------+-------------+
   | >Performing | (0008,1050) | 2/2         | 2/2         | 2           |
   | Physician's |             |             |             |             |
   | Name        |             |             |             |             |
   +-------------+-------------+-------------+-------------+-------------+
   | >Protocol   | (0018,1030) | 1/1         | 1/1         | 1           |
   | Name        |             |             |             |             |
   +-------------+-------------+-------------+-------------+-------------+
   | >Operators' | (0008,1070) | 2/2         | 2/2         | 2           |
   | Name        |             |             |             |             |
   +-------------+-------------+-------------+-------------+-------------+
   | >Series     | (0020,000E) | 1/1         | 1/1         | 1           |
   | Instance    |             |             |             |             |
   | UID         |             |             |             |             |
   +-------------+-------------+-------------+-------------+-------------+
   | >Series     | (0008,103E) | 2/2         | 2/2         | 2           |
   | Description |             |             |             |             |
   +-------------+-------------+-------------+-------------+-------------+
   | >Retrieve   | (0008,0054) | 2/2         | 2/2         | 2           |
   | AE Title    |             |             |             |             |
   +-------------+-------------+-------------+-------------+-------------+
   | >Archive    | (0040,A494) | 3/3         | 3/3         |             |
   | Requested   |             |             |             |             |
   +-------------+-------------+-------------+-------------+-------------+
   | >Referenced | (0008,1140) | 2/2         | 2/2         | See         |
   | Image       |             |             |             | `Service    |
   | Sequence    |             |             |             | Class       |
   |             |             |             |             | Use         |
   |             |             |             |             | r <#sect_F. |
   |             |             |             |             | 7.2.2.2>`__ |
   +-------------+-------------+-------------+-------------+-------------+
   | >           | (0008,1150) | 1/1         | 1/1         |             |
   | >Referenced |             |             |             |             |
   | SOP Class   |             |             |             |             |
   | UID         |             |             |             |             |
   +-------------+-------------+-------------+-------------+-------------+
   | >           | (0008,1155) | 1/1         | 1/1         |             |
   | >Referenced |             |             |             |             |
   | SOP         |             |             |             |             |
   | Instance    |             |             |             |             |
   | UID         |             |             |             |             |
   +-------------+-------------+-------------+-------------+-------------+
   | >>Container | (0040,0512) | 3/3         | 3/3         |             |
   | Identifier  |             |             |             |             |
   +-------------+-------------+-------------+-------------+-------------+
   | >>Specimen  | (0040,0560) | 3/3         | 3/3         |             |
   | Description |             |             |             |             |
   | Sequence    |             |             |             |             |
   +-------------+-------------+-------------+-------------+-------------+
   | >>>Specimen | (0040,0551) | 1/1         | 1/1         |             |
   | Identifier  |             |             |             |             |
   +-------------+-------------+-------------+-------------+-------------+
   | >>>Specimen | (0040,0554) | 1/1         | 1/1         |             |
   | UID         |             |             |             |             |
   +-------------+-------------+-------------+-------------+-------------+
   | >Referenced | (0040,0220) | 2/2         | 2/2         | See         |
   | Non-Image   |             |             |             | `Service    |
   | Composite   |             |             |             | Class       |
   | SOP         |             |             |             | Use         |
   | Instance    |             |             |             | r <#sect_F. |
   | Sequence    |             |             |             | 7.2.2.2>`__ |
   +-------------+-------------+-------------+-------------+-------------+
   | >           | (0008,1150) | 1/1         | 1/1         |             |
   | >Referenced |             |             |             |             |
   | SOP Class   |             |             |             |             |
   | UID         |             |             |             |             |
   +-------------+-------------+-------------+-------------+-------------+
   | >           | (0008,1155) | 1/1         | 1/1         |             |
   | >Referenced |             |             |             |             |
   | SOP         |             |             |             |             |
   | Instance    |             |             |             |             |
   | UID         |             |             |             |             |
   +-------------+-------------+-------------+-------------+-------------+
   | *>All other |             | 3/3         | 3/3         |             |
   | Attributes  |             |             |             |             |
   | of the      |             |             |             |             |
   | Performed   |             |             |             |             |
   | Series      |             |             |             |             |
   | Sequence*   |             |             |             |             |
   +-------------+-------------+-------------+-------------+-------------+
   | *All other  |             | 3/3         | 3/3         |             |
   | Attributes  |             |             |             |             |
   | of the*     |             |             |             |             |
   +-------------+-------------+-------------+-------------+-------------+

.. note::

   1. The requirement for the final state is that which applies at the
      time that the Performed Procedure Step Status (0040,0252) is N-SET
      to a value of COMPLETED or DISCONTINUED, as described in `Service
      Class User <#sect_F.7.2.2.2>`__. It is only described if it is
      different from the SCP requirement for the N-CREATE.

   2. The Performed Series Sequence (0040,0340) may not be empty (zero
      length) at the time that the Performed Procedure Step Status
      (0040,0252) is N-SET to a value of COMPLETED or DISCONTINUED. In
      other words a Series must exist for every Performed Procedure
      Step, though it may contain no Images or Non-Image Composite
      objects, if none were created, as described in `Service Class
      User <#sect_F.7.2.2.2>`__.

   3. Attributes (0040,1006) Placer Order Number/Procedure and
      (0040,1007) Filler Order Number/Procedure were previously defined
      in DICOM. They are now retired (see PS3.3-1998).

   4. Attributes (0040,2006) and (0040,2007) were previously defined in
      DICOM. They are now retired (see PS3.3-1998).

   5. Only Attributes that are specified in a SOP Instance at N-CREATE
      may later be updated through the N-SET. If an SCU wishes to use
      the PPS Discontinuation Reason Code Sequence (0040,0281), it must
      create that Attribute (zero-length) during MPPS N-CREATE.

   6. The Radiation Dose Module was previously defined in DICOM. This is
      now retired (see PS3.3-2017c).

.. _sect_F.7.2.1.2:

Service Class User
''''''''''''''''''

The SCU shall specify in the N-CREATE request primitive the Class and
Instance UIDs of the Modality Performed Procedure Step SOP Instance that
is created and for which Attribute Values are to be provided.

.. note::

   This requirement facilitates the inclusion of relevant Attributes in
   the Composite SOP Instances generated during the Performed Procedure
   Step.

The SCU shall provide Attribute Values for the Modality Performed
Procedure Step SOP Class Attributes as specified in
`table_title <#table_F.7.2-1>`__. Additionally, values may be provided
for optional Modality Performed Procedure Step IOD Attributes that are
supported by the SCP. The encoding rules for Modality Performed
Procedure Step Attributes are specified in the N-CREATE request
primitive specification in .

The SCU shall be capable of providing all required Attribute Values to
the SCP in the N-CREATE request primitive. The SCU may provide Attribute
Values for optional Attributes that are not maintained by the SCP. In
such case the SCU shall function properly regardless of whether the SCP
accepts values for those Attributes or not.

All Attributes shall be created before they can be set. Sequence
Attributes shall be created before they can be filled. Sequence Item
Attributes shall not be created at zero length.

.. note::

   Not all the Attributes that can be created can be set afterward (see
   `table_title <#table_F.7.2-1>`__).

The SCU shall only send the N-CREATE request primitive with the value
for the Attribute "Performed Procedure Step Status" (0040,0252) set to
"IN PROGRESS".

.. note::

   1. It is assumed but not required that the SCU (the modality)
      received the Study Instance UID within the scope of the Basic
      Worklist Management SOP Class.

   2. If the SCU has grouped multiple Requested Procedures into a single
      performed step the Study Instance UID (0020,000D) Attribute within
      the Scheduled Step Attributes Sequence (0040,0270) may be the
      Study Instance UID (0020,000D) for the study that contains all
      images and non-image composite instances created during
      performance of the current step. This value may be generated by
      the SCU and may be the same for all items of the sequence. In
      addition, the Referenced Study Sequence (0008,1110) may contain
      the Study Instance UIDs from the Requested Procedures being
      grouped. If Referenced Study Sequence (0008,1110) is present with
      an Item, the SOP Class UID of the Detached Study Management SOP
      Class (Retired) may be used in Referenced SOP Class UID
      (0008,1150).

   3. If the SCU does not have available Scheduled Procedure Step data
      applicable to the current step, the SCU may generate a value for
      the Study Instance UID (0020,000D) Attribute within the Scheduled
      Step Attributes Sequence (0040,0270). This value of the Study
      Instance UID (0020,000D) may be stored in all images and non-image
      composite SOP instances created during performance of this step.
      All other Attributes within the Scheduled Step Attribute Sequence
      (0040,0270) may be set to zero length for 2/2 requirement types or
      absent for 3/3 requirement types (see
      `table_title <#table_F.7.2-1>`__).

.. _sect_F.7.2.1.3:

Service Class Provider
''''''''''''''''''''''

The N-CREATE operation allows the SCU to provide to the SCP selected
Attribute Values for a specific Modality Performed Procedure Step SOP
Instance. This operation shall be invoked through the use of the DIMSE
N-CREATE Service used in conjunction with the appropriate Modality
Performed Procedure Step SOP Instance.

The SCP shall return, via the N-CREATE response primitive, the N-CREATE
Response Status Code applicable to the associated request.

The SCP shall accept N-CREATE request primitives only if the value of
the Attribute "Performed Procedure Step Status" (0040,0252) is "IN
PROGRESS". If the Performed Procedure Step Status Attribute has another
value, the SCP shall set the failure status code "Invalid Attribute
Value" (Code: 0106H) with an Attribute List.

.. note::

   The SCP may update the scheduling information on which the Modality
   Worklist is based, including the values of Study Date (0008,0020) and
   Study Time (0008,0030) using the earliest corresponding values of
   Performed Procedure Step Date (0040,0244) and Performed Procedure
   Step Time (0040,0245), in order to achieve consistency of Study level
   Attributes when multiple procedure steps are performed on different
   devices.

.. _sect_F.7.2.1.4:

Status Codes
''''''''''''

There are no specific status codes. See for response status codes.

.. _sect_F.7.2.2:

Set Modality Performed Procedure Step Information
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

This operation allows an SCU to set Attribute Values of an instance of
the Modality Performed Procedure Step SOP Class and provide information
about a specific real-world Modality Performed Procedure Step that is
under control of the SCU. This operation shall be invoked through the
DIMSE N-SET Service.

.. _sect_F.7.2.2.1:

Modality Performed Procedure Step IOD Subset Specification
''''''''''''''''''''''''''''''''''''''''''''''''''''''''''

The Application Entity that claims conformance to this SOP Class as an
SCU may choose to modify a subset of the Attributes maintained by the
SCP. The Application Entity that claims conformance as an SCP to this
SOP Class shall support the subset of the Modality Performed Procedure
Step Attributes specified in `table_title <#table_F.7.2-1>`__.

The character set used for Attribute Values updated using the N-SET
shall be the same as that specified by the N-CREATE Request Primitive.

.. _sect_F.7.2.2.2:

Service Class User
''''''''''''''''''

The SCU shall specify in the N-SET request primitive the UID of the
Modality Performed Procedure Step SOP Instance for which it wants to set
Attribute Values.

The SCU shall be permitted to set Attribute Values for any Modality
Performed Procedure Step SOP Class Attribute specified in
`table_title <#table_F.7.2-1>`__. The SCU shall specify the list of
Modality Performed Procedure Step SOP Class Attributes for which it
wants to set the Attribute Values. The SCU shall provide, with one or
more N-SET request primitives, the Attribute Values specified in
`table_title <#table_F.7.2-1>`__. The encoding rules for Modality
Performed Procedure Step Attributes are specified in the N-SET request
primitive specification in . The SCU shall only set Attribute Values
that are already created with an N-CREATE request.

The SCU shall not send N-SET request primitives for a Modality Performed
Procedure Step SOP Instance after a N-SET request primitive with a value
for the Attribute "Performed Procedure Step Status" (0040,0252) is
"COMPLETED" or "DISCONTINUED" has been sent.

If Sequences are included in a N-SET command, all Items of a Sequence
are to be included in the command and not only the Items to be updated.

Once the Modality Performed Procedure Step Status (0040,0252) has been
set to "COMPLETED" or "DISCONTINUED" the SCU shall no longer modify the
Modality Performed Procedure Step SOP Instance, and shall not create new
Composite SOP Instances as part of the same Modality Performed Procedure
Step SOP Instance.

.. note::

   A Modality that wishes to continue or resume creating Composite SOP
   Instances may create a new Modality Performed Procedure Step.

Before or when Modality Performed Procedure Step Status (0040,0252) is
set to "COMPLETED" or "DISCONTINUED" the SCU shall have created or set
all the Attributes according to the requirements in the Final State
column of `table_title <#table_F.7.2-1>`__.

Before or when Modality Performed Procedure Step Status (0040,0252) is
set to "COMPLETED" or "DISCONTINUED" the SCU shall have sent to the SCP
a list of all Image SOP Instances and all Non-Image Composite SOP
Instances created during the Procedure Step in Referenced Image Sequence
(0008,1140) and Referenced Non-Image Composite SOP Instance Sequence
(0040,0220) respectively.

.. note::

   1. The intent is that a completed or discontinued Modality Performed
      Procedure Step entity will contain a complete list of all the
      Images and Non-Image Composite SOP Instances that were created.

   2. The distinction between the list of images and non-images is
      present for historic reasons only, and has no semantic
      significance.

The Modality Performed Procedure Step Status (0040,0252) shall not be
set to "COMPLETED" or "DISCONTINUED" if the list contains neither Image
references nor Non-Image Composite SOP Instance references, unless no
such Instances were created.

.. _sect_F.7.2.2.3:

Service Class Provider
''''''''''''''''''''''

The N-SET operation allows the SCU to request that the SCP update
selected Attribute Values for a specific Modality Performed Procedure
Step SOP Instance. This operation shall be invoked through the use of
the DIMSE N-SET Service used in conjunction with the appropriate
Modality Performed Procedure Step SOP Instance. The N-SET value for
Specific Character Set (0008,0005) does not replace the previous value.
The SCP shall appropriately modify its internal representation so that
subsequent operations reflect the combination of the character sets in
use by the Attributes in this N-SET and those used by Attributes that
have not been modified.

.. note::

   The SCP may need to convert the text for instance to the Unicode
   character set. If the SCP is not able to perform a necessary
   conversion it may return the Invalid Attribute Value error code
   (0106H).

The SCP shall return, via the N-SET response primitive, the N-SET
Response Status Code applicable to the associated request. Contingent on
the N-SET Response Status, the SCP shall update the Referenced Performed
Procedure Step Attributes.

The SCP shall accept N-SET request primitives only if the value of the
already existing Attribute "Performed Procedure Step Status" (0040,0252)
is "IN PROGRESS". If the already existing Performed Procedure Step
Status Attribute has another value, the SCP shall set the failure status
code "Processing failure" (Code: 0110H) with a Specific Error Comment
(see `Status Codes <#sect_F.7.2.2.4>`__).

The SCP may itself modify any Attributes of the Modality Performed
Procedure Step SOP Instance only after the "Performed Procedure Step
Status" (0040,0252) has been set to "COMPLETED" or "DISCONTINUED".

.. note::

   1. Such coercion of Attributes by the SCP may be necessary to
      correct, for example, patient identification information or
      incorrectly selected scheduling information. Such an operation is
      not permitted to the SCU by the requirements described in
      `table_title <#table_F.7.2-1>`__, which might create a new
      Modality Performed Procedure Step SOP Instance to achieve the same
      objective.

   2. Under exceptional circumstances, it may be necessary for the SCP
      to itself set the Performed Procedure Step Status (0040,0252) to
      COMPLETED or DISCONTINUED, for example if the Modality has failed.
      When the Modality recovers, subsequent N-SETs may fail.

.. _sect_F.7.2.2.4:

Status Codes
''''''''''''

There are no specific status codes. The specific Error Comment and Error
ID that may be returned with a status code of Processsing Failure in a
N-SET-RSP are defined in `table_title <#table_F.7.2-2>`__. See for
additional response status codes.

.. table:: N-SET Status

   +-------------+-------------+-------------+-------------+-------------+
   | Service     | Further     | Status Code | Error       | Error ID    |
   | Status      | Meaning     |             | Comment     | (0000,0903) |
   |             |             |             | (0000,0902) |             |
   +=============+=============+=============+=============+=============+
   | Failure     | Processing  | 0110        | Performed   | A710        |
   |             | Failure     |             | Procedure   |             |
   |             |             |             | Step Object |             |
   |             |             |             | may no      |             |
   |             |             |             | longer be   |             |
   |             |             |             | updated     |             |
   +-------------+-------------+-------------+-------------+-------------+

.. _sect_F.7.3:

Modality Performed Procedure Step SOP Class UID
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

The Modality Performed Procedure Step SOP Class shall be uniquely
identified by the Modality Performed Procedure Step SOP Class UID that
shall have the value "1.2.840.10008.3.1.2.3.3".

.. _sect_F.7.4:

Conformance Requirements
~~~~~~~~~~~~~~~~~~~~~~~~

Implementations providing conformance to the Modality Performed
Procedure Step SOP Class shall be conformant as described in the
following sections and shall include within their Conformance Statement
information as described below.

An implementation may conform to this SOP Class as an SCU or as an SCP.
The Conformance Statement shall be in the format defined in .

.. _sect_F.7.4.1:

SCU Conformance
^^^^^^^^^^^^^^^

An implementation that is conformant to this SOP Class as an SCU shall
meet conformance requirements for the operations that it invokes.

.. _sect_F.7.4.1.1:

Operations
''''''''''

Any Attributes for which Attribute Values may be provided (using the
N-CREATE Service) by the SCU shall be enumerated in the Conformance
Statement.

Any Attributes for which Attribute Values may be provided (using the
N-SET Service) by the SCU shall be enumerated in the Conformance
Statement.

An implementation that conforms to this SOP Class as an SCU shall
specify under which conditions during the performance of the real-world
Performed Procedure Step it will create the SOP Class Instance and under
which conditions it will set the status value to COMPLETED and
DISCONTINUED.

An implementation that conforms to this SOP Class as an SCU shall
specify what strategy it applies to group Storage SOP Class Instances
referenced in a Performed Procedure Step.

.. note::

   For example, whether or not Radiation Dose SR instances are sent
   within the same Performed Procedure Step as the images to which it
   applies, or a different Performed Procedure Step. See the discussion
   of the MPPS in the DICOM real-world model in .

.. _sect_F.7.4.2:

SCP Conformance
^^^^^^^^^^^^^^^

An implementation that is conformant to this SOP Class as an SCP shall
meet conformance requirements for the operations that it performs.

.. _sect_F.7.4.2.1:

Operations
''''''''''

Any Attributes for which Attribute Values may be provided (using the
N-CREATE Service) by the SCU shall be enumerated in the Conformance
Statement.

Any Attributes for which Attribute Values may be updated (using the
N-SET Service) by the SCU shall be enumerated in the Conformance
Statement.

The Conformance Statement shall also provide information on the behavior
of the SCP at the following occurrences:

-  The creation of a new Instance of the Modality Performed Procedure
   Step SOP Class with the status "IN PROGRESS". The result of that
   process on the scheduling information and on the Attributes values of
   the Modality Worklist SOP Class shall be specified.

-  The update of the Attribute "Performed Procedure Step Status", i.e.,
   the change from the state "IN PROGRESS" to "DISCONTINUED" or to
   "COMPLETED".

-  Which Attributes the SCP may coerce after the state has been set to
   "IN PROGRESS" or "DISCONTINUED" or to "COMPLETED".

-  For how long the Modality Performed Procedure Step SOP Instance will
   persist on the SCP.

.. _sect_F.8:

Modality Performed Procedure Step Retrieve SOP Class
----------------------------------------------------

.. _sect_F.8.1:

DIMSE Service Group
~~~~~~~~~~~~~~~~~~~

The DIMSE Services shown in `table_title <#table_F.8.1-1>`__ are
applicable to the Modality Performed Procedure Step IOD under the
Modality Performed Procedure Step Retrieve SOP Class.

.. table:: DIMSE Service Group Applicable to Modality Performed
Procedure Step Retrieve

   ============================= =============
   DICOM Message Service Element Usage SCU/SCP
   ============================= =============
   N-GET                         M/M
   ============================= =============

The DIMSE Services and Protocols are specified in . If the Modality
Performed Procedure Step Object is no longer available the Request
Primitive will be answered with a Failure Status message "No such Object
Instance".

.. _sect_F.8.2:

Operations
~~~~~~~~~~

The Application Entity that claims conformance to this SOP Class as an
SCU shall be permitted to invoke the following operations and the
Application Entity that claims conformance as an SCP shall be capable of
providing the following operations.

.. _sect_F.8.2.1:

Get Performed Procedure Step Information
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

This operation allows an SCU to get information about a specific
real-world Performed Procedure Step that is represented as a Modality
Performed Procedure Step Retrieve SOP Instance by a Modality Performed
Procedure Step Retrieve SCP. The operation is performed on a Modality
Performed Procedure Step IOD. This operation shall be invoked through
the DIMSE N-GET Service used in conjunction with the appropriate
Modality Performed Procedure Step Retrieve SOP Instance.

The same SOP Instance UID is shared by all three Modality Performed
Procedure Step SOP Classes. This means that the SOP Instance created and
set using the services of the Modality Performed Procedure Step SOP
Class can be retrieved using its SOP Instance UID within the service of
the Modality Performed Procedure Step Retrieve SOP Class. Changes in its
state can be notified by using its SOP Instance UID within the service
of the Modality Performed Procedure Step Notification SOP Class. The SOP
Class UID specified in the DIMSE N-GET request primitive shall be the
UID of the Modality Performed Procedure Step Retrieve SOP Class.

The Modality Performed Procedure Retrieve Step SOP Instance UID shall
not be used to identify a SOP Instance of the Study Component Service
Class.

.. note::

   An Application Entity may support the SCU role of the Modality
   Performed Procedure Step Retrieve SOP Class in order to obtain
   information about Performed Procedure Steps created by other
   Application Entities.

.. _sect_F.8.2.1.1:

Modality Performed Procedure Step Retrieve IOD Subset Specifications
''''''''''''''''''''''''''''''''''''''''''''''''''''''''''''''''''''

The Application Entity that claims conformance to this SOP Class as an
SCU may choose to interpret the Attribute Values maintained by the SCP
that the SCU receives via the operation of this SOP Class. The
Application Entity that claims conformance as an SCP to this Modality
Performed Procedure Step Retrieve SOP Class shall support the subset of
the Modality Performed Procedure Step Retrieve Attributes specified in
`table_title <#table_F.8.2-1>`__.

.. table:: Modality Performed Procedure Step Retrieve SOP Class N-GET
Attributes

   +--------------------------+-------------+--------------------------+
   | Attribute Name           | Tag         | Requirement Type         |
   |                          |             | (SCU/SCP)                |
   +==========================+=============+==========================+
   | Specific Character Set   | (0008,0005) | 3/1C                     |
   |                          |             |                          |
   |                          |             | (Required if an extended |
   |                          |             | or replacement character |
   |                          |             | set is used)             |
   +--------------------------+-------------+--------------------------+
   | **Performed Procedure    |             |                          |
   | Step Relationship**      |             |                          |
   +--------------------------+-------------+--------------------------+
   | Scheduled Step           | (0040,0270) | 3/1                      |
   | Attributes Sequence      |             |                          |
   +--------------------------+-------------+--------------------------+
   | >Study Instance UID      | (0020,000D) | -/1                      |
   +--------------------------+-------------+--------------------------+
   | >Referenced Study        | (0008,1110) | -/2                      |
   | Sequence                 |             |                          |
   +--------------------------+-------------+--------------------------+
   | >>Referenced SOP Class   | (0008,1150) | -/1                      |
   | UID                      |             |                          |
   +--------------------------+-------------+--------------------------+
   | >>Referenced SOP         | (0008,1155) | -/1                      |
   | Instance UID             |             |                          |
   +--------------------------+-------------+--------------------------+
   | >Accession Number        | (0008,0050) | -/2                      |
   +--------------------------+-------------+--------------------------+
   | >Issuer of Accession     | (0008,0051) | -/3                      |
   | Number Sequence          |             |                          |
   +--------------------------+-------------+--------------------------+
   | >>Local Namespace Entity | (0040,0031) | -/3                      |
   | ID                       |             |                          |
   +--------------------------+-------------+--------------------------+
   | >>Universal Entity ID    | (0040,0032) | -/3                      |
   +--------------------------+-------------+--------------------------+
   | >>Universal Entity ID    | (0040,0033) | -/3                      |
   | Type                     |             |                          |
   +--------------------------+-------------+--------------------------+
   | >Placer Order            | (0040,2016) | -/3                      |
   | Number/Imaging Service   |             |                          |
   | Request                  |             |                          |
   +--------------------------+-------------+--------------------------+
   | >Order Placer Identifier | (0040,0026) | -/3                      |
   | Sequence                 |             |                          |
   +--------------------------+-------------+--------------------------+
   | >>Local Namespace Entity | (0040,0031) | -/3                      |
   | ID                       |             |                          |
   +--------------------------+-------------+--------------------------+
   | >>Universal Entity ID    | (0040,0032) | -/3                      |
   +--------------------------+-------------+--------------------------+
   | >>Universal Entity ID    | (0040,0033) | -/3                      |
   | Type                     |             |                          |
   +--------------------------+-------------+--------------------------+
   | >Filler Order            | (0040,2017) | -/3                      |
   | Number/Imaging Service   |             |                          |
   | Request                  |             |                          |
   +--------------------------+-------------+--------------------------+
   | >Order Filler Identifier | (0040,0027) | -/3                      |
   | Sequence                 |             |                          |
   +--------------------------+-------------+--------------------------+
   | >>Local Namespace Entity | (0040,0031) | -/3                      |
   | ID                       |             |                          |
   +--------------------------+-------------+--------------------------+
   | >>Universal Entity ID    | (0040,0032) | -/3                      |
   +--------------------------+-------------+--------------------------+
   | >>Universal Entity ID    | (0040,0033) | -/3                      |
   | Type                     |             |                          |
   +--------------------------+-------------+--------------------------+
   | >Requested Procedure     | (0032,1064) | -/3                      |
   | Code Sequence            |             |                          |
   +--------------------------+-------------+--------------------------+
   | *>>Include*\ `tabl       |             |                          |
   | e_title <#table_8-3a>`__ |             |                          |
   +--------------------------+-------------+--------------------------+
   | >Requested Procedure     | (0032,1060) | -/2                      |
   | Description              |             |                          |
   +--------------------------+-------------+--------------------------+
   | >Requested Procedure ID  | (0040,1001) | -/2                      |
   +--------------------------+-------------+--------------------------+
   | >Scheduled Procedure     | (0040,0009) | -/2                      |
   | Step ID                  |             |                          |
   +--------------------------+-------------+--------------------------+
   | >Scheduled Procedure     | (0040,0007) | -/2                      |
   | Step Description         |             |                          |
   +--------------------------+-------------+--------------------------+
   | >Scheduled Protocol Code | (0040,0008) | -/2                      |
   | Sequence                 |             |                          |
   +--------------------------+-------------+--------------------------+
   | *>>Include*\ `tabl       |             |                          |
   | e_title <#table_8-5a>`__ |             |                          |
   +--------------------------+-------------+--------------------------+
   | Patient's Name           | (0010,0010) | 3/2                      |
   +--------------------------+-------------+--------------------------+
   | Patient ID               | (0010,0020) | 3/2                      |
   +--------------------------+-------------+--------------------------+
   | Issuer of Patient ID     | (0010,0021) | 3/3                      |
   +--------------------------+-------------+--------------------------+
   | Issuer of Patient ID     | (0010,0024) | 3/3                      |
   | Qualifiers Sequence      |             |                          |
   +--------------------------+-------------+--------------------------+
   | >Universal Entity ID     | (0040,0032) | 3/3                      |
   +--------------------------+-------------+--------------------------+
   | >Universal Entity ID     | (0040,0033) | 1C/1C                    |
   | Type                     |             |                          |
   |                          |             | Required if Universal    |
   |                          |             | Entity ID (0040,0032) is |
   |                          |             | present.                 |
   +--------------------------+-------------+--------------------------+
   | *>All other Attributes   |             | 3/3                      |
   | of the Issuer of Patient |             |                          |
   | ID Qualifiers Sequence*  |             |                          |
   +--------------------------+-------------+--------------------------+
   | >Patient ID              | (0010,0020) | 3/3                      |
   +--------------------------+-------------+--------------------------+
   | >Issuer of Patient ID    | (0010,0021) | 3/3                      |
   +--------------------------+-------------+--------------------------+
   | >Issuer of Patient ID    | (0010,0024) | 3/3                      |
   | Qualifiers Sequence      |             |                          |
   +--------------------------+-------------+--------------------------+
   | *>>All other Attributes  |             | 3/3                      |
   | of the Issuer of Patient |             |                          |
   | ID Qualifiers Sequence*  |             |                          |
   +--------------------------+-------------+--------------------------+
   | Patient's Birth Date     | (0010,0032) | 3/2                      |
   +--------------------------+-------------+--------------------------+
   | Patient's Sex            | (0010,0040) | 3/2                      |
   +--------------------------+-------------+--------------------------+
   | Referenced Patient       | (0008,1120) | 3/2                      |
   | Sequence                 |             |                          |
   +--------------------------+-------------+--------------------------+
   | >Referenced SOP Class    | (0008,1150) | -/1                      |
   | UID                      |             |                          |
   +--------------------------+-------------+--------------------------+
   | >Referenced Instance UID | (0008,1155) | -/1                      |
   +--------------------------+-------------+--------------------------+
   | Admission ID             | (0038,0010) | 3/3                      |
   +--------------------------+-------------+--------------------------+
   | Issuer of Admission ID   | (0038,0014) | 3/3                      |
   | Sequence                 |             |                          |
   +--------------------------+-------------+--------------------------+
   | >Local Namespace Entity  | (0040,0031) | -/3                      |
   | ID                       |             |                          |
   +--------------------------+-------------+--------------------------+
   | >Universal Entity ID     | (0040,0032) | -/3                      |
   +--------------------------+-------------+--------------------------+
   | >Universal Entity ID     | (0040,0033) | -/3                      |
   | Type                     |             |                          |
   +--------------------------+-------------+--------------------------+
   | Service Episode ID       | (0038,0060) | 3/3                      |
   +--------------------------+-------------+--------------------------+
   | Issuer of Service        | (0038,0064) | 3/3                      |
   | Episode ID Sequence      |             |                          |
   +--------------------------+-------------+--------------------------+
   | >Local Namespace Entity  | (0040,0031) | -/3                      |
   | ID                       |             |                          |
   +--------------------------+-------------+--------------------------+
   | >Universal Entity ID     | (0040,0032) | -/3                      |
   +--------------------------+-------------+--------------------------+
   | >Universal Entity ID     | (0040,0033) | -/3                      |
   | Type                     |             |                          |
   +--------------------------+-------------+--------------------------+
   | Service Episode          | (0038,0062) | 3/3                      |
   | Description              |             |                          |
   +--------------------------+-------------+--------------------------+
   | **Performed Procedure    |             |                          |
   | Step Information**       |             |                          |
   +--------------------------+-------------+--------------------------+
   | Performed Station AE     | (0040,0241) | 3/1                      |
   | Title                    |             |                          |
   +--------------------------+-------------+--------------------------+
   | Performed Station Name   | (0040,0242) | 3/2                      |
   +--------------------------+-------------+--------------------------+
   | Performed Location       | (0040,0243) | 3/2                      |
   +--------------------------+-------------+--------------------------+
   | Performed Procedure Step | (0040,0244) | 3/1                      |
   | Start Date               |             |                          |
   +--------------------------+-------------+--------------------------+
   | Performed Procedure Step | (0040,0245) | 3/1                      |
   | Start Time               |             |                          |
   +--------------------------+-------------+--------------------------+
   | Performed Procedure Step | (0040,0253) | 3/1                      |
   | ID                       |             |                          |
   +--------------------------+-------------+--------------------------+
   | Performed Procedure Step | (0040,0252) | 3/1                      |
   | Status                   |             |                          |
   +--------------------------+-------------+--------------------------+
   | Performed Procedure Step | (0040,0250) | 3/2                      |
   | End Date                 |             |                          |
   +--------------------------+-------------+--------------------------+
   | Performed Procedure Step | (0040,0251) | 3/2                      |
   | End Time                 |             |                          |
   +--------------------------+-------------+--------------------------+
   | Performed Procedure Step | (0040,0254) | 3/2                      |
   | Description              |             |                          |
   +--------------------------+-------------+--------------------------+
   | Performed Procedure Type | (0040,0255) | 3/2                      |
   | Description              |             |                          |
   +--------------------------+-------------+--------------------------+
   | Procedure Code Sequence  | (0008,1032) | 3/2                      |
   +--------------------------+-------------+--------------------------+
   | *>Include*\ `tabl        |             |                          |
   | e_title <#table_8-5a>`__ |             |                          |
   +--------------------------+-------------+--------------------------+
   | Comments on the          | (0040,0280) | 3/3                      |
   | Performed Procedure Step |             |                          |
   +--------------------------+-------------+--------------------------+
   | Performed Procedure Step | (0040,0281) | 3/2                      |
   | Discontinuation Reason   |             |                          |
   | Code Sequence            |             |                          |
   +--------------------------+-------------+--------------------------+
   | *>Include*\ `tabl        |             |                          |
   | e_title <#table_8-5a>`__ |             |                          |
   +--------------------------+-------------+--------------------------+
   | **Image Acquisition      |             |                          |
   | Results**                |             |                          |
   +--------------------------+-------------+--------------------------+
   | Performed Series         | (0040,0340) | 3/2                      |
   | Sequence                 |             |                          |
   +--------------------------+-------------+--------------------------+
   | >Performing Physician's  | (0008,1050) | -/2                      |
   | Name                     |             |                          |
   +--------------------------+-------------+--------------------------+
   | >Protocol Name           | (0018,1030) | -/1                      |
   +--------------------------+-------------+--------------------------+
   | >Operators' Name         | (0008,1070) | -/2                      |
   +--------------------------+-------------+--------------------------+
   | >Series Instance UID     | (0020,000E) | -/1                      |
   +--------------------------+-------------+--------------------------+
   | >Series Description      | (0008,103E) | -/2                      |
   +--------------------------+-------------+--------------------------+
   | >Retrieve AE Title       | (0008,0054) | -/2                      |
   +--------------------------+-------------+--------------------------+
   | >Referenced Image        | (0008,1140) | -/2                      |
   | Sequence                 |             |                          |
   +--------------------------+-------------+--------------------------+
   | >>Referenced SOP Class   | (0008,1150) | -/1                      |
   | UID                      |             |                          |
   +--------------------------+-------------+--------------------------+
   | >>Referenced SOP         | (0008,1155) | -/1                      |
   | Instance UID             |             |                          |
   +--------------------------+-------------+--------------------------+
   | >Referenced Non-Image    | (0040,0220) | -/2                      |
   | Composite SOP Instance   |             |                          |
   | Sequence                 |             |                          |
   +--------------------------+-------------+--------------------------+
   | >>Referenced SOP Class   | (0008,1150) | -/1                      |
   | UID                      |             |                          |
   +--------------------------+-------------+--------------------------+
   | >>Referenced SOP         | (0008,1155) | -/1                      |
   | Instance UID             |             |                          |
   +--------------------------+-------------+--------------------------+
   | *>All other Attributes   |             | -/3                      |
   | of the Performed Series  |             |                          |
   | Sequence*                |             |                          |
   +--------------------------+-------------+--------------------------+
   | Modality                 | (0008,0060) | 3/1                      |
   +--------------------------+-------------+--------------------------+
   | Study ID                 | (0020,0010) | 3/2                      |
   +--------------------------+-------------+--------------------------+
   | Performed Protocol Code  | (0040,0260) | 3/2                      |
   | Sequence                 |             |                          |
   +--------------------------+-------------+--------------------------+
   | *>Include*\ `tabl        |             |                          |
   | e_title <#table_8-5a>`__ |             |                          |
   +--------------------------+-------------+--------------------------+
   | *All other Attributes of |             | 3/3                      |
   | the*                     |             |                          |
   +--------------------------+-------------+--------------------------+

.. note::

   1. Attributes (0040,1006) Placer Order Number/Procedure and
      (0040,1007) Filler Order Number/Procedure were previously defined
      in DICOM. They are now retired (see PS3.3-1998).

   2. Attributes (0040,2006) and (0040,2007) were previously defined in
      DICOM. They are now retired (see PS3.3-1998).

   3. The Radiation Dose Module was previously defined in DICOM. This is
      now retired (see PS3.3-2017c).

.. _sect_F.8.2.1.2:

Service Class User
''''''''''''''''''

The SCU uses the N-GET Service Element to request the SCP to get a
Modality Performed Procedure Step Retrieve SOP Instance. The SCU shall
specify in the N-GET request primitive the UID of the SOP Instance to be
retrieved, which is a UID of a Modality Performed Procedure Step SOP
Instance. The SCU shall be permitted to request that Attribute Values be
returned for any Modality Performed Procedure Step Retrieve SOP Class
Attribute specified in `table_title <#table_F.8.2-1>`__. Additionally
values may be requested for optional Modality Performed Procedure Step
IOD Attributes.

The SCU shall specify the list of Modality Performed Procedure Step
Retrieve SOP Class Attributes for which values are to be returned. The
encoding rules for Modality Performed Procedure Step Attributes are
specified in the N-GET request primitive specification in .

In an N-GET operation, the values of Attributes that are defined within
a Sequence of Items shall not be requested by an SCU.

The SCU shall be capable of receiving all requested Attribute Values
provided by the SCP in response to the N-GET indication primitive. The
SCU may request Attribute Values for optional Attributes that are not
maintained by the SCP. In such a case, the SCU shall function properly
regardless of whether the SCP returns values for those Attributes or
not. This Service Class Specification places no requirements on what the
SCU shall do as a result of receiving this information.

.. note::

   In order to accurately interpret the character set used for the
   Attribute Values returned, it is recommended that the Attribute Value
   for the Specific Character Set (0008,0005) be requested in the N-GET
   request primitive.

.. _sect_F.8.2.1.3:

Service Class Provider
''''''''''''''''''''''

The N-GET operation allows the SCU to request from the SCP selected
Attribute Values for a specific Modality Performed Procedure Step SOP
Instance via a Modality Performed Procedure Step Retrieve SOP Instance.
This operation shall be invoked through the use of the DIMSE N-GET
Service used in conjunction with the appropriate Modality Performed
Procedure Step Retrieve SOP Instance that equals the Modality Performed
Procedure SOP Instance. The SCP shall retrieve the selected Attribute
Values from the indicated Modality Performed Procedure Step SOP
Instance.

The SCP shall return, via the N-GET response primitive, the N-GET
Response Status Code applicable to the associated request. A Failure
Code shall indicate that the SCP has not retrieved the SOP Instance.
Contingent on the N-GET Response Status, the SCP shall return, via the
N-GET response primitive, Attribute Values for all requested Attributes
maintained by the SCP.

.. _sect_F.8.2.1.4:

Status Codes
''''''''''''

`table_title <#table_F.8.2-2>`__ defines the specific status code values
that might be returned in a N-GET response. See for additional response
status codes.

.. table:: Response Status

   +----------------+-------------------------------------------------+-------------+
   | Service Status | Further Meaning                                 | Status Code |
   +================+=================================================+=============+
   | Warning        | Requested optional Attributes are not supported | 0001        |
   +----------------+-------------------------------------------------+-------------+

.. _sect_F.8.3:

Modality Performed Procedure Step Retrieve SOP Class UID
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

The Modality Performed Procedure Step Retrieve SOP Class shall be
uniquely identified by the Modality Performed Procedure Step Retrieve
SOP Class UID that shall have the value "1.2.840.10008.3.1.2.3.4".

.. _sect_F.8.4:

Conformance Requirements
~~~~~~~~~~~~~~~~~~~~~~~~

Implementations providing conformance to the Modality Performed
Procedure Step Retrieve SOP Class shall be conformant as described in
the following sections and shall include within their Conformance
Statement information as described below.

An implementation may conform to this SOP Class as an SCU or as an SCP.
The Conformance Statement shall be in the format defined in .

.. _sect_F.8.4.1:

SCU Conformance
^^^^^^^^^^^^^^^

An implementation that is conformant to this SOP Class as an SCU shall
meet conformance requirements for the operations that it invokes.

.. _sect_F.8.4.1.1:

Operations
''''''''''

Any Attributes for which Attribute Values may be requested (using the
N-GET Service) by the SCU shall be enumerated in the SCU Operations
Statement. The SCU Operations Statement shall be formatted as defined in
.

.. _sect_F.8.4.2:

SCP Conformance
^^^^^^^^^^^^^^^

An implementation that is conformant to this SOP Class as an SCP shall
meet conformance requirements for the operations that it performs.

.. _sect_F.8.4.2.1:

Operations
''''''''''

Any Attributes for which Attribute Values may be requested (using the
N-GET Service) by the SCU shall be enumerated in the SCP Operations
Statement. The SCP Operations Statement shall be formatted as defined in
.

.. _sect_F.9:

Modality Performed Procedure Step Notification SOP Class
--------------------------------------------------------

The Modality Performed Procedure Step Notification SOP Class is intended
for those Application Entities requiring notifications of Modality
Performed Procedure Step's changes in state.

An Application Entity may choose to take some actions based upon a
notification or request for information but is in no way required to do
so.

.. note::

   1. For example, in one configuration, an IS could be responsible for
      maintaining data related to performed procedure steps. A PACS
      reviewing workstation may need to display the images for any study
      viewed. In order for the PACS to link the images to the study, a
      PACS may receive a notification whenever a procedure step has been
      performed. In such a configuration the IS is the SCP and the PACS
      is the SCU. When the PACS receives this notification, it may link
      the images and the performed procedure step to the study within
      its internal database or may choose to take no action.

   2. The terms IS and PACS used in the previous example are provided
      for clarification purposes only. This document does not define nor
      constrain the purpose or role of any IS, PACS or acquisition
      Application Entity conforming to this Service Class Specification.

.. _sect_F.9.1:

DIMSE Service Group
~~~~~~~~~~~~~~~~~~~

`table_title <#table_F.9.1-1>`__ shows the DIMSE-N Services applicable
to the Modality Performed Procedure Step IOD under the Modality
Performed Procedure Step Notification SOP Class.

The DIMSE-N Services and Protocol are specified in .

.. table:: DIMSE Service Group Applicable to Modality Performed
Procedure Step Notification

   ============================= =============
   DICOM Message Service Element Usage SCU/SCP
   ============================= =============
   N-EVENT-REPORT                M/M
   ============================= =============

.. _sect_F.9.2:

Notifications
~~~~~~~~~~~~~

The Application Entity that claims conformance as an SCU to this SOP
Class shall be permitted to receive the following notification. The
Application Entity that claims conformance as an SCP to this SOP Class
shall be capable of providing the notifications defined in
`table_title <#table_F.9.2-1>`__.

.. table:: Performed Procedure Step Notification Event Information

   +---------------+---------------+---------------+-----+---------------+
   | Event Type    | Event Type ID | Attribute     | Tag | Req. Type     |
   | Name          |               | Name          |     | SCU/SCP       |
   +===============+===============+===============+=====+===============+
   | Performed     | 1             |               |     |               |
   | Procedure     |               |               |     |               |
   | Step In       |               |               |     |               |
   | Progress      |               |               |     |               |
   +---------------+---------------+---------------+-----+---------------+
   | Performed     | 2             |               |     |               |
   | Procedure     |               |               |     |               |
   | Step          |               |               |     |               |
   | Completed     |               |               |     |               |
   +---------------+---------------+---------------+-----+---------------+
   | Performed     | 3             |               |     |               |
   | Procedure     |               |               |     |               |
   | Step          |               |               |     |               |
   | Discontinued  |               |               |     |               |
   +---------------+---------------+---------------+-----+---------------+
   | Performed     | 4             |               |     | An Update     |
   | Procedure     |               |               |     | event shall   |
   | Step Updated  |               |               |     | not be used   |
   |               |               |               |     | to notify     |
   |               |               |               |     | changes in    |
   |               |               |               |     | Performed     |
   |               |               |               |     | Procedure     |
   |               |               |               |     | Step Status   |
   |               |               |               |     | (0040,0252).  |
   +---------------+---------------+---------------+-----+---------------+
   | Performed     | 5             |               |     |               |
   | Procedure     |               |               |     |               |
   | Step Deleted  |               |               |     |               |
   +---------------+---------------+---------------+-----+---------------+

.. note::

   The Notification Event Information contains no Attributes, beyond
   those defined in . An SCU receiving a Notification and requiring
   further information may also be an SCU of the Modality Performed
   Procedure Step Retrieval SOP Class and may use the Affected SOP
   Instance UID (0000,1000) to perform an N-GET of the Modality
   Performed Procedure Step SOP Instance.

.. _sect_F.9.2.1:

Receive Modality Performed Procedure Step Event Notification
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

This notification allows an SCU to receive from the SCP an unsolicited
notification of a change in a Modality Performed Procedure Step SOP
Instance. These notifications shall be invoked by the SCP through the
use of the DIMSE N-EVENT-REPORT Service used in conjunction with the
related Modality Performed Procedure Step SOP Instance.

The SCU shall return, via the N-EVENT-REPORT response primitive, the
N-EVENT-REPORT Response Status Code applicable to the associated
request. The SCU shall accept all Attributes included in any
notification. This Service Class Specification places no requirements on
what the SCU shall do as a result of receiving this information.

The same SOP Instance UID is shared by all three Modality Performed
Procedure Step SOP Classes. This means that the SOP Instance created and
set using the services of the Modality Performed Procedure Step SOP
Class can be retrieved using its SOP Instance UID within the service of
the Modality Performed Procedure Step Retrieve SOP Class. Changes in its
state can be notified by using its SOP Instance UID within the request
primitive of the Modality Performed Procedure Step Notification SOP
Class.

The Modality Performed Procedure Step Notification SOP Instance UID
shall not be used to identify a SOP Instance of the Study Component
Service Class.

.. _sect_F.9.2.2:

Provide Modality Performed Procedure Step Event Notification
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

These notifications allow an SCU to receive from the SCP an unsolicited
notification of a change in the state of a real-world performed
procedure step. This notification shall be invoked by the SCP through
the use of the DIMSE N-EVENT-REPORT Service used in conjunction with the
related Modality Performed Procedure Step SOP Instance.

The SCP shall specify in the N-EVENT-REPORT request primitive the UID of
the Modality Performed Procedure Step SOP Instance with which the event
is associated and the Event Type ID. The Affected SOP Class UID
specified in the DIMSE N-EVENT-REPORT request primitive shall be the UID
of the Modality Performed Procedure Step Notification SOP Class.

.. note::

   The encoding of Notification Event Information is defined in .

.. _sect_F.9.2.3:

Status Codes
^^^^^^^^^^^^

There are no specific status codes. See for response status codes.

.. _sect_F.9.3:

Modality Performed Procedure Step Notification SOP Class UID
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

The Modality Performed Procedure Step Notification SOP Class shall be
uniquely identified by the Modality Performed Procedure Step
Notification SOP Class UID that shall have the value
"1.2.840.10008.3.1.2.3.5".

.. _sect_F.9.4:

Conformance Requirements
~~~~~~~~~~~~~~~~~~~~~~~~

Implementations providing Standard SOP Class Conformance to the Modality
Performed Procedure Step Notification SOP Class shall be conformant as
described in the following sections and shall include within their
Conformance Statement information as described in the following
sections.

An implementation may conform to this SOP Class as an SCU, SCP or both.
The Conformance Statement shall be in the format defined in .

.. _sect_F.9.4.1:

SCU Conformance
^^^^^^^^^^^^^^^

An implementation that is conformant to this SOP Class as an SCU shall
meet conformance requirements for the:

-  notifications that it receives

.. _sect_F.9.4.1.1:

Notifications
'''''''''''''

All standard event types for which notifications may be requested by the
SCU shall be enumerated in the SCU Notifications Statement. The SCU
Notifications Statement shall include an enumerated list of the event
types supported:

-  Performed Procedure Step In Progress

-  Performed Procedure Step Completed

-  Performed Procedure Step Discontinued

-  Performed Procedure Step Updated

-  Performed Procedure Step Deleted

.. _sect_F.9.4.2:

SCP Conformance
^^^^^^^^^^^^^^^

An implementation that is conformant to this SOP Class as an SCP shall
meet conformance requirements for:

-  notifications that it invokes

.. _sect_F.9.4.2.1:

Notifications
'''''''''''''

Any optional Attributes that may be included in Standard notifications
to the SCU shall be enumerated in the SCP Notifications Statement. The
SCP Notifications Statement shall be formatted as defined in . Following
this statement shall be the list of event types and optional Attributes.

.. _sect_F.10:

General Purpose Scheduled Procedure Step SOP Class (Retired)
------------------------------------------------------------

Retired. See PS3.4-2011.

.. _sect_F.11:

General Purpose Performed Procedure Step SOP Class (Retired)
------------------------------------------------------------

Retired. See PS3.4-2011.

