.. _chapter_CC:

Unified Procedure Step Service and SOP Classes (Normative)
==========================================================

.. _sect_CC.1:

Overview
--------

This Annex defines the Service and SOP Classes associated with a Unified
Worklist and Procedure Step.

The Unified Procedure Step Service Class provides for management of
simple worklists, including creating new worklist items, querying the
worklist, and communicating progress and results.

A worklist is a list of Unified Procedure Step (UPS) instances. Each UPS
instance unifies the worklist details for a single requested procedure
step together with the result details of the corresponding performed
procedure step. There is a one to one relationship between the procedure
step request and the procedure step performed.

Unified Procedure Step instances may be used to represent a variety of
scheduled tasks such as: Image Processing, Quality Control, Computer
Aided Detection, Interpretation, Transcription, Report Verification, or
Printing.

The UPS instance can contain details of the requested task such as when
it is scheduled to be performed or Workitem Codes describing the
requested actions. The UPS may also contain details of the input
information the performer needs to do the task and the output the
performer produced, such as: Current Images, Prior Images, Reports,
Films, Presentation States, or Audio recordings.

The Unified Worklist and Procedure Step Service Class includes five SOP
Classes associated with UPS instances. The SOP Class UID for any UPS
Instance always specifies the UPS Push SOP Class. The separate SOP
Classes facilitate better negotiation and logical implementation groups
of functionalities.

The UPS Push SOP Class allows an SCU to instruct the SCP to create a new
UPS instance, effectively letting a system push a new work item onto the
SCP's worklist. It is important to note that the SCP could be a Worklist
Manager that maintains the worklist for other systems that will perform
the work, or the SCP could be a performing system itself that manages an
internal worklist.

The UPS Pull SOP Class allows an SCU to query a Worklist Manager (the
SCP) for matching UPS instances, and instruct the SCP to update the
status and contents of selected items (UPS instances). The SCU
effectively pulls work instructions from the worklist. As work
progresses, the SCU records details of the activities performed and the
results created in the UPS instance.

The UPS Query SOP Class allows an SCU to query a Worklist Manager (the
SCP), but does not otherwise interact with the UPS instances

The UPS Watch SOP Class allows an SCU to subscribe for status update
events and retrieve the details of work items (UPS instances) managed by
the SCP.

The UPS Event SOP Class allows an SCP to provide the actual status
update events for work items it manages to relevant (i.e., subscribed)
SCUs.

Each of these services has an equivalent HTTP operation defined by the
UPS-RS Worklist Service (see ).

While a Unified Worklist and Procedure Step Service Class SCP is not
required to support UPS-RS, an SCP may choose to support one or more of
the UPS-RS services as an Origin-Server. In this scenario, an SCP/Origin
Server shall follow the same internal behavior for all Workitems
irrespective of whether they originated with a DIMSE request or an HTTP
request. A DIMSE request and its equivalent HTTP request with the same
parameters shall yield the same response.

For example:

-  A Workitem instance created via DIMSE N-CREATE can be retrieved via
   HTTP requests and vice-versa

-  A Workitem instance created via DIMSE N-CREATE can be updated, have
   its state changed or be canceled via HTTP requests and vice-versa

-  A C-FIND request and an HTTP SearchForUPS request with the same
   parameters shall return the same set of results

-  An N-EVENT-REPORT SCU that also supports HTTP subscriptions will
   record whether a given subscriber uses DIMSE or WebSockets and send
   the appropriate form of notification to that subscriber

-  A change made to a Workitem instance will result in the same event
   notifications regardless of whether the change was requested via
   DIMSE or HTTP

-  A Global Subscription request or a Filtered Global Subscription
   request will subscribe an SCU (or User-Agent) to instances created
   both via DIMSE and via HTTP requests

-  A DIMSE event subscriber will receive notifications for relevant
   changes made via HTTP requests

-  An HTTP event subscriber will receive notifications for relevant
   changes made via DIMSE requests

The mapping between UPS DIMSE operations and UPS-RS services is defined
in .

.. _sect_CC.1.1:

Unified Procedure Step States
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

`figure_title <#figure_CC.1.1-1>`__, `table_title <#table_CC.1.1-1>`__
and `table_title <#table_CC.1.1-2>`__ specify how changes in the state
of a Unified Procedure Step shall be managed.

The following interactions represent an example sequence of events and
state transitions. Observe that the DIMSE Services described here
operate on the same IOD. The multiple UPS SOP Classes thus act in a
coordinated manner as specified in this Annex.

To create a UPS, an SCU uses an N-CREATE to push a UPS onto the SCP's
worklist. The SCP responds to such requests by creating a Unified
Procedure Step (UPS) with an initial state of SCHEDULED.

.. note::

   All UPS Instances are instances of the UPS Push SOP Class, although
   the other three SOP Classes (UPS Pull, UPS Watch and UPS Event) may
   also operate on the Instance.

To subscribe to receive N-EVENT-REPORTs for a UPS, or to unsubscribe to
stop receiving N-EVENT-REPORTS, an SCU uses an N-ACTION request. The SCU
may be the system that created the UPS as a Push SCU, or may be some
other system with a reason to track the progress and results of a
scheduled step.

To inform interested systems of the state of a UPS or the SCP itself, an
SCP issues N-EVENT-REPORTs to SCUs that have subscribed.

To find a UPS of interest, an SCU uses a C-FIND to query the SCP for
relevant UPS instances.

To "claim" and start work on a UPS, an SCU (which will be referred to
here as the "Performing SCU") uses an N-ACTION Change State request to
set the UPS state to IN PROGRESS and provide a transaction UID (which
will be referred to here as the Locking UID). For a SCHEDULED UPS, the
SCP responds by changing the UPS state to IN PROGRESS and recording the
transaction UID for future use. For a UPS with other status, the SCP
rejects the request.

The SCP does not permit the status of a SCHEDULED UPS to be set to
COMPLETED or CANCELED without first being set to IN PROGRESS.

To modify details of the performed procedure, the Performing SCU uses an
N-SET request to the SCP (providing the Locking UID for the UPS). N-SET
requests on an IN PROGRESS UPS where the Locking UID in the N-SET Data
Set does not match the Locking UID in the UPS are rejected by the SCP.

To modify the status of the procedure step, the Performing SCU uses an
N-ACTION Change State request to the SCP (providing the Locking UID for
the UPS). N-ACTION Change State requests where the Locking UID in the
N-ACTION Data Set does not match the Locking UID in the UPS are rejected
by the SCP.

The Locking UID effectively limits control of the state of an IN
PROGRESS UPS to only the SCP and the Performing SCU. The SCP does not
check whether IP addresses, AE-Titles, or parameters other than the
Locking UID match to determine if the SCU has permission.

When the Performing SCU completes work on the UPS, it N-SETs any values
necessary to meet the Final State requirements in
`table_title <#table_CC.2.5-3>`__, then uses an N-ACTION request
(providing the Locking UID for the UPS during both steps) for the SCP to
change the UPS state to COMPLETED.

When the Performing SCU abandons work on an incomplete UPS, it N-SETs
any values necessary to meet the Final State requirements in
`table_title <#table_CC.2.5-3>`__, then uses an N-ACTION request
(providing the Locking UID for the UPS) for the SCP to change the UPS
state to CANCELED.

To request cancellation of a UPS, non-performing SCUs use an N-ACTION
Request Cancel (see and for example cases).

-  If the UPS is still in the SCHEDULED state, the SCP first changes the
   UPS state to IN PROGRESS, and then to CANCELED, issuing the
   appropriate N-EVENT-REPORTS.

-  If the UPS is already IN PROGRESS and the SCP is itself performing
   the UPS, it may, at its own discretion, choose to cancel the UPS as
   described in the previous paragraph.

-  If the UPS is already IN PROGRESS and the SCP is not the performer,
   it does not change the UPS state to CANCELED, but rather responds by
   issuing an N-EVENT-REPORT of the cancellation request to all
   subscribed SCUs. If the Performing SCU is listening to
   N-EVENT-REPORTs it may, at its own discretion, choose to cancel the
   UPS as described above.

`table_title <#table_CC.1.1-1>`__ describes the valid UPS states

.. table:: Unified Procedure Step (UPS) States

   +-------------+-------------------------------------------------------+
   | State       | Description                                           |
   +=============+=======================================================+
   | SCHEDULED   | The UPS is scheduled to be performed.                 |
   +-------------+-------------------------------------------------------+
   | IN PROGRESS | The UPS has been claimed and a Locking UID has been   |
   |             | set. Performance of the UPS has likely started.       |
   +-------------+-------------------------------------------------------+
   | CANCELED    | The UPS has been permanently stopped before or during |
   |             | performance of the step. This may be due to voluntary |
   |             | or involuntary action by a human or machine. Any      |
   |             | further UPS-driven work required to complete the      |
   |             | scheduled task must be performed by scheduling        |
   |             | another (different) UPS.                              |
   +-------------+-------------------------------------------------------+
   | COMPLETED   | The UPS has been completed.                           |
   +-------------+-------------------------------------------------------+

COMPLETED and CANCELED are "Final States" that involve specific
requirements on the UPS as described in `UPS Final State
Requirements <#sect_CC.2.5.1.1>`__.

`table_title <#table_CC.1.1-2>`__ describes the valid state transitions
(a row in the table defines what should happen in response to a certain
event for each initial state). Details on how the Operations listed in
the table should be carried out are described in section `DIMSE Service
Groups <#sect_CC.2>`__.

.. table:: Unified Procedure Step State Transition Table

   +----------+----------+----------+----------+---------+---------+
   |          | States   |          |          |         |         |
   +==========+==========+==========+==========+=========+=========+
   | N-CREATE | Create   | error    | error    | error   | error   |
   | received | SOP      |          |          |         |         |
   | for this | Instance | 0111     | 0111     | 0111    | 0111    |
   | SOP      | with     |          |          |         |         |
   | Instance | empty    |          |          |         |         |
   | UID      | tra      |          |          |         |         |
   |          | nsaction |          |          |         |         |
   |          | UID,     |          |          |         |         |
   |          | Change   |          |          |         |         |
   |          | State to |          |          |         |         |
   |          | S        |          |          |         |         |
   |          | CHEDULED |          |          |         |         |
   +----------+----------+----------+----------+---------+---------+
   | N-ACTION | error    | Report   | error    | error   | error   |
   | to       |          | state    |          |         |         |
   | Change   | C307     | change,  | C302     | C300    | C300    |
   | State to |          | Record   |          |         |         |
   | IN       |          | tra      |          |         |         |
   | PROGRESS |          | nsaction |          |         |         |
   | with     |          | UID,     |          |         |         |
   | correct  |          | Change   |          |         |         |
   | tra      |          | State to |          |         |         |
   | nsaction |          | IN       |          |         |         |
   | UID      |          | PROGRESS |          |         |         |
   +----------+----------+----------+----------+---------+---------+
   | N-ACTION | error    | error    | error    | error   | error   |
   | to       |          |          |          |         |         |
   | Change   | C307     | C301     | C301     | C301    | C301    |
   | State to |          |          |          |         |         |
   | IN       |          |          |          |         |         |
   | PROGRESS |          |          |          |         |         |
   | without  |          |          |          |         |         |
   | correct  |          |          |          |         |         |
   | tra      |          |          |          |         |         |
   | nsaction |          |          |          |         |         |
   | UID      |          |          |          |         |         |
   +----------+----------+----------+----------+---------+---------+
   | N-ACTION | error    | error    | error    | error   | error   |
   | to       |          |          |          |         |         |
   | Change   | C307     | C303     | C303     | C303    | C303    |
   | State to |          |          |          |         |         |
   | S        |          |          |          |         |         |
   | CHEDULED |          |          |          |         |         |
   +----------+----------+----------+----------+---------+---------+
   | N-ACTION | error    | error    | If Final | warning | error   |
   | to       |          |          | State    |         |         |
   | Change   | C307     | C310     | Requ     | B306    | C300    |
   | State to |          |          | irements |         |         |
   | CO       |          |          | met,     |         |         |
   | MPLETED, |          |          | (Report  |         |         |
   | with     |          |          | state    |         |         |
   | correct  |          |          | change,  |         |         |
   | tra      |          |          | Change   |         |         |
   | nsaction |          |          | State to |         |         |
   | UID      |          |          | COM      |         |         |
   |          |          |          | PLETED); |         |         |
   |          |          |          | Else     |         |         |
   |          |          |          | C304     |         |         |
   +----------+----------+----------+----------+---------+---------+
   | N-ACTION | error    | error    | error    | error   | error   |
   | to       |          |          |          |         |         |
   | Change   | C307     | C301     | C301     | C301    | C301    |
   | State to |          |          |          |         |         |
   | CO       |          |          |          |         |         |
   | MPLETED, |          |          |          |         |         |
   | without  |          |          |          |         |         |
   | correct  |          |          |          |         |         |
   | tra      |          |          |          |         |         |
   | nsaction |          |          |          |         |         |
   | UID      |          |          |          |         |         |
   +----------+----------+----------+----------+---------+---------+
   | N-ACTION | error    | Report   | Report   | error   | warning |
   | to       |          | state    | that an  |         |         |
   | Request  | C307     | change   | App      | C311    | B304    |
   | Cancel   |          | to       | lication |         |         |
   |          |          | IN-P     | Entity   |         |         |
   |          |          | ROGRESS, | r        |         |         |
   |          |          | Report   | equested |         |         |
   |          |          | state    | a        |         |         |
   |          |          | change   | cancel.  |         |         |
   |          |          | to       |          |         |         |
   |          |          | C        |          |         |         |
   |          |          | ANCELED, |          |         |         |
   |          |          | Change   |          |         |         |
   |          |          | State to |          |         |         |
   |          |          | CANCELED |          |         |         |
   +----------+----------+----------+----------+---------+---------+
   | N-ACTION | error    | error    | If Final | error   | warning |
   | to       |          |          | State    |         |         |
   | Change   | C307     | C310     | Requ     | C300    | B304    |
   | State to |          |          | irements |         |         |
   | C        |          |          | met,     |         |         |
   | ANCELED, |          |          | (Report  |         |         |
   | with     |          |          | state    |         |         |
   | correct  |          |          | change,  |         |         |
   | tra      |          |          | Change   |         |         |
   | nsaction |          |          | State to |         |         |
   | UID      |          |          | CA       |         |         |
   |          |          |          | NCELED); |         |         |
   |          |          |          | Else     |         |         |
   |          |          |          | C304.    |         |         |
   +----------+----------+----------+----------+---------+---------+
   | N-ACTION | error    | error    | error    | error   | error   |
   | to       |          |          |          |         |         |
   | Change   | C307     | C301     | C301     | C301    | C301    |
   | State to |          |          |          |         |         |
   | C        |          |          |          |         |         |
   | ANCELED, |          |          |          |         |         |
   | without  |          |          |          |         |         |
   | correct  |          |          |          |         |         |
   | tra      |          |          |          |         |         |
   | nsaction |          |          |          |         |         |
   | UID      |          |          |          |         |         |
   +----------+----------+----------+----------+---------+---------+

.. _sect_CC.2:

DIMSE Service Groups
--------------------

The DIMSE Services shown in `table_title <#table_CC.2-1>`__,
`table_title <#table_CC.2-2>`__, `table_title <#table_CC.2-3>`__,
`table_title <#table_CC.2-4>`__ and `table_title <#table_CC.2-5>`__ are
applicable to the Unified Procedure Step (UPS) IOD under the UPS Push,
UPS Pull, UPS Watch, UPS Event and UPS Query SOP Classes respectively.

.. table:: DIMSE Service Group Applicable to UPS Push

   ============================= =============
   DICOM Message Service Element Usage SCU/SCP
   ============================= =============
   N-CREATE                      M/M
   N-ACTION - Request UPS Cancel U/M
   N-GET                         U/M
   ============================= =============

.. table:: DIMSE Service Group Applicable to UPS Pull

   ============================= =============
   DICOM Message Service Element Usage SCU/SCP
   ============================= =============
   C-FIND                        M/M
   N-GET                         M/M
   N-SET                         M/M
   N-ACTION - Change UPS State   M/M
   ============================= =============

.. table:: DIMSE Service Group Applicable to UPS Watch

   ============================= =======
   DICOM Message Service Element SCU/SCP
   ============================= =======
   N-ACTION - Un/Subscribe       M/M
   N-GET                         M/M
   C-FIND                        U/M
   N-ACTION - Request UPS Cancel U/M
   ============================= =======

.. table:: DIMSE Service Group Applicable to UPS Event

   ============================= =============
   DICOM Message Service Element Usage SCU/SCP
   ============================= =============
   N-EVENT-REPORT                M/M
   ============================= =============

.. table:: DIMSE Service Group Applicable to UPS Query

   ============================= =============
   DICOM Message Service Element Usage SCU/SCP
   ============================= =============
   C-FIND                        M/M
   ============================= =============

.. _sect_CC.2.1:

Change UPS State (N-ACTION)
~~~~~~~~~~~~~~~~~~~~~~~~~~~

This operation allows an SCU to ask the SCP to change the state of a
Unified Procedure Step (UPS) instance. This operation shall be invoked
by the SCU through the DIMSE N-ACTION Service.

.. _sect_CC.2.1.1:

Action Information
^^^^^^^^^^^^^^^^^^

DICOM AEs that claim conformance to the UPS Pull SOP Class as an SCU
and/or an SCP shall support the Action Types and Action Information as
specified in `table_title <#table_CC.2.1-1>`__.

.. table:: Change UPS State - Action Information

   +-------------+-------------+-------------+-------------+-------------+
   | Action Type | Action Type | Attribute   | Tag         | Requirement |
   | Name        | ID          | Name        |             | Type        |
   |             |             |             |             | SCU/SCP     |
   +=============+=============+=============+=============+=============+
   | Change UPS  | 1           | Procedure   | (0074,1000) | 1/1         |
   | State       |             | Step State  |             |             |
   +-------------+-------------+-------------+-------------+-------------+
   | Transaction | (0008,1195) | 1/1         |             |             |
   | UID         |             |             |             |             |
   +-------------+-------------+-------------+-------------+-------------+

.. _sect_CC.2.1.2:

Service Class User Behavior
^^^^^^^^^^^^^^^^^^^^^^^^^^^

An SCU uses N-ACTION to ask the SCP to change the state of a UPS
Instance as shown in `figure_title <#figure_CC.1.1-1>`__. Since all UPSs
are created as instances of the UPS Push SOP Class, the Requested SOP
Class UID (0000,0003) in the N-ACTION request shall be the UID of the
UPS Push SOP Class. See `Service Class and SOP Class
UIDs <#sect_CC.3.1>`__ for further details.

To take control of a SCHEDULED UPS, an SCU shall generate a Transaction
UID and submit a state change to IN PROGRESS including the Transaction
UID in the submission. The SCU shall record and use the Transaction UID
in future N-ACTION and N-SET requests for that UPS instance.

.. note::

   1. The performing SCU may wish to record the Transaction UID in
      non-volatile storage. This would allow the SCU to retain control
      over the UPS after recovering from a crash.

   2. If two SCUs try to take control of a UPS, the second SCU will get
      an error since the first SCU established the correct Transaction
      UID, so the Transaction UID provided by the second SCU is
      incorrect.

Upon completion of an IN PROGRESS UPS it controls, an SCU shall submit a
state change to COMPLETED and include the Transaction UID for the UPS
instance.

To cancel an IN PROGRESS UPS for which it has the Transaction UID, an
SCU shall submit a state change to CANCELED and include the Transaction
UID for the UPS instance.

.. note::

   1. Prior to submitting the state change to CANCELED, the performing
      SCU can N-SET the values of Reason For Cancellation, Procedure
      Step Discontinuation Reason Code Sequence, Contact Display Name or
      Contact URI to provide information to observing SCUs about the
      context of the cancellation.

   2. To request cancellation of an IN PROGRESS UPS for which it does
      not have the Transaction UID, an SCU uses the Request UPS Cancel
      action as described in `Request UPS Cancel
      (N-ACTION) <#sect_CC.2.2>`__, rather than a Change UPS State
      action.

Prior to submitting a state change to COMPLETED or CANCELED for a UPS
instance it controls, the SCU shall perform any N-SETs necessary for the
UPS to meet Final State requirements as described in section `UPS Final
State Requirements <#sect_CC.2.5.1.1>`__.

At any time after receipt of the N-ACTION-Response, the SCU may release
the association on which it sent the N-ACTION-Request.

.. _sect_CC.2.1.3:

Service Class Provider Behavior
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

The SCP shall perform the submitted state change for the identified UPS
instance by setting the Procedure Step State (0074,1000) to the
requested value, or shall report the appropriate failure response code.

Upon successfully changing the state of a UPS instance to IN PROGRESS,
the SCP shall record the Transaction UID provided by the SCU in the
Transaction UID (0008,1195) of the UPS instance.

Upon completion of the N-ACTION request, the SCP shall return, via the
N-ACTION response primitive, the N-ACTION Status Code applicable to the
associated request as shown in `table_title <#table_CC.2.1-2>`__.

The SCP shall only perform legal state changes as described in
`table_title <#table_CC.1.1-2>`__.

The SCP shall refuse requests to change the state of an IN PROGRESS UPS
unless the Transaction UID of the UPS instance is provided in the
request.

The SCP shall refuse requests to change the state of an IN PROGRESS UPS
to COMPLETED or CANCELED if the Final State requirements described in
`table_title <#table_CC.2.5-3>`__ have not been met.

After the state of the UPS instance has been changed to COMPLETED or
CANCELED, the SCP shall not delete the instance until all deletion locks
have been removed.

.. note::

   See `Service Class User Behavior <#sect_CC.2.3.2>`__ for a
   description of how SCUs place and remove deletion locks and see
   Reliable Watchers and Deletion Locks for further discussion.

The SCP may also modify the Procedure Step State (0074,1000) of a UPS
instance independently of an N-ACTION request, e.g., if the SCP is
performing the procedure step itself, or if it has been determined that
the performing SCU has been disabled.

.. note::

   If the SCP is not performing the procedure step, this should be done
   with caution.

Upon successfully changing the state of a UPS instance, the SCP shall
carry out the appropriate N-EVENT-REPORT behavior as described in
`Service Class Provider Behavior <#sect_CC.2.4.3>`__ if it supports the
UPS Event SOP Class as an SCP.

Bi-directional Authentication of machines/users/applications is possible
at association time (see and ). provides a "Refused: Refused: Not
authorized" error code. Further requiring or documenting authentication
and/or authorization features from the SCU or SCP is beyond the scope of
this SOP Class.

.. _sect_CC.2.1.4:

Status Codes
^^^^^^^^^^^^

`table_title <#table_CC.2.1-2>`__ defines the status code values that
might be returned in a N-ACTION response. General status code values and
fields related to status code values are defined for N-ACTION DIMSE
Service in .

.. table:: N-ACTION Response Status Values [for Change UPS State]

   +--------------------------+--------------------------+-------------+
   | Service Status           | Further Meaning          | Status Code |
   +==========================+==========================+=============+
   | Success                  | The requested state      | 0000        |
   |                          | change was performed     |             |
   +--------------------------+--------------------------+-------------+
   | Warning                  | The UPS is already in    | B304        |
   |                          | the requested state of   |             |
   |                          | CANCELED                 |             |
   +--------------------------+--------------------------+-------------+
   | The UPS is already in    | B306                     |             |
   | the requested state of   |                          |             |
   | COMPLETED                |                          |             |
   +--------------------------+--------------------------+-------------+
   | Failure                  | Failed: The UPS may no   | C300        |
   |                          | longer be updated        |             |
   +--------------------------+--------------------------+-------------+
   | Failed: The correct      | C301                     |             |
   | Transaction UID was not  |                          |             |
   | provided                 |                          |             |
   +--------------------------+--------------------------+-------------+
   | Failed: The UPS is       | C302                     |             |
   | already IN PROGRESS      |                          |             |
   +--------------------------+--------------------------+-------------+
   | Failed: The UPS may only | C303                     |             |
   | become SCHEDULED via     |                          |             |
   | N-CREATE, not N-SET or   |                          |             |
   | N-ACTION                 |                          |             |
   +--------------------------+--------------------------+-------------+
   | Failed: The UPS has not  | C304                     |             |
   | met final state          |                          |             |
   | requirements for the     |                          |             |
   | requested state change   |                          |             |
   +--------------------------+--------------------------+-------------+
   | Failed: Specified SOP    | C307                     |             |
   | Instance UID does not    |                          |             |
   | exist or is not a UPS    |                          |             |
   | Instance managed by this |                          |             |
   | SCP                      |                          |             |
   +--------------------------+--------------------------+-------------+
   | Failed: The UPS is not   | C310                     |             |
   | yet in the "IN PROGRESS" |                          |             |
   | state                    |                          |             |
   +--------------------------+--------------------------+-------------+

.. _sect_CC.2.2:

Request UPS Cancel (N-ACTION)
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

This operation allows an SCU that does not control a given Unified
Procedure Step (UPS) instance to request to the SCP that the instance be
canceled. This operation shall be invoked by the SCU through the DIMSE
N-ACTION Service.

.. _sect_CC.2.2.1:

Action Information
^^^^^^^^^^^^^^^^^^

DICOM AEs that claim conformance to the UPS Push SOP Class as an SCU or
an SCP shall support the Action Types and Action Information as
specified in `table_title <#table_CC.2.2-1>`__. DICOM AEs that claim
conformance to the UPS Watch SOP Class as an SCP or claim conformance to
the UPS Watch SOP Class as an SCU and choose to implement Request UPS
Cancel shall support the Action Types and Action Information as
specified in `table_title <#table_CC.2.2-1>`__.

.. table:: Request UPS Cancel - Action Information

   +-------------+-------------+-------------+-------------+-------------+
   | Action Type | Action Type | Attribute   | Tag         | Requirement |
   | Name        | ID          | Name        |             | Type        |
   |             |             |             |             | SCU/SCP     |
   +=============+=============+=============+=============+=============+
   | Request UPS | 2           | Reason For  | (0074,1238) | 3/1         |
   | Cancel      |             | C           |             |             |
   |             |             | ancellation |             |             |
   +-------------+-------------+-------------+-------------+-------------+
   | Procedure   | (0074,100e) | 3/1         |             |             |
   | Step        |             |             |             |             |
   | Disc        |             |             |             |             |
   | ontinuation |             |             |             |             |
   | Reason Code |             |             |             |             |
   | Sequence    |             |             |             |             |
   +-------------+-------------+-------------+-------------+-------------+
   | *>Includ    |             |             |             |             |
   | e*\ `table_ |             |             |             |             |
   | title <#tab |             |             |             |             |
   | le_8-1a>`__ |             |             |             |             |
   +-------------+-------------+-------------+-------------+-------------+
   | Contact URI | (0074,100a) | 3/1         |             |             |
   +-------------+-------------+-------------+-------------+-------------+
   | Contact     | (0074,100c) | 3/1         |             |             |
   | Display     |             |             |             |             |
   | Name        |             |             |             |             |
   +-------------+-------------+-------------+-------------+-------------+

.. _sect_CC.2.2.2:

Service Class User Behavior
^^^^^^^^^^^^^^^^^^^^^^^^^^^

An SCU uses N-ACTION to request to the SCP that the state of a UPS
Instance be changed to CANCELED as shown in
`figure_title <#figure_CC.1.1-1>`__. Since all UPSs are created as
instances of the UPS Push SOP Class, the Requested SOP Class UID
(0000,0003) in the N-ACTION request shall be the UID of the UPS Push SOP
Class. See `Service Class and SOP Class UIDs <#sect_CC.3.1>`__ for
further details.

The SCU may include a Reason For Cancellation and/or a proposed
Procedure Step Discontinuation Reason Code Sequence.

The SCU may also provide a Contact Display Name and/or a Contact URI for
the person with whom the cancel request may be discussed.

.. note::

   An N-ACTION Status Code indicating success means that the Request was
   accepted, not that the UPS has been canceled. The system performing
   the UPS is not obliged to honor the request to cancel and in some
   scenarios, may not even receive notification of the request. See
   `Report a Change in UPS Status (N-EVENT-REPORT) <#sect_CC.2.4>`__.

At any time after receipt of the N-ACTION-Response, the SCU may release
the association on which it sent the N-ACTION-Request.

To cancel an IN PROGRESS UPS that the SCU is itself performing, the SCU
shall instead use the Change UPS State action as described in `Change
UPS State (N-ACTION) <#sect_CC.2.1>`__.

.. _sect_CC.2.2.3:

Service Class Provider Behavior
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

The SCP shall send appropriate "UPS Cancel Requested" N-EVENT-REPORT
messages, as described in `Service Class Provider
Behavior <#sect_CC.2.4.3>`__ or shall report the appropriate failure
response code.

.. note::

   If provided, the Reason For Cancellation, a proposed Procedure Step
   Discontinuation Reason Code Sequence, a Contact Display Name and a
   Contact URI of someone responsible for the Cancel request might be
   useful in deciding to cancel the UPS or might be displayed to an
   operator so they can make contact for the purpose of clarifying or
   confirming the Cancel request. If the SCP is the performer and
   chooses to actually Cancel the UPS, it may at its own discretion set
   the Procedure Step Discontinuation Reason Code Sequence in the UPS
   instance based on the corresponding values provided.

If the Procedure Step State (0074,1000) of the UPS instance is still
SCHEDULED, the SCP shall change the Procedure Step State, as described
in `Service Class Provider Behavior <#sect_CC.2.1.3>`__, first to IN
PROGRESS and then to CANCELED, ensuring that the Final State
requirements, described in section `UPS Final State
Requirements <#sect_CC.2.5.1.1>`__, are met.

If the Procedure Step State (0074,1000) of the UPS instance is IN
PROGRESS, and the SCP is itself the performer of the UPS, the SCP may,
at its own discretion, choose to cancel the UPS as described in `Service
Class Provider Behavior <#sect_CC.2.1.3>`__.

If the SCP is the performer of the UPS and chooses not to cancel, or if
there is no possibility that the performing SCU will be informed of the
cancel request (e.g., the subscription list for the UPS is empty, or the
SCP has determined that the performing SCU has been disabled), the SCP
may return a failure.

Upon completion of the N-ACTION request, the SCP shall return, via the
N-ACTION response primitive, the N-ACTION Status Code applicable to the
associated request as shown in `table_title <#table_CC.2.2-2>`__.

Bi-directional Authentication of machines/users/applications is possible
at association time (see and ). provides a "Refused: Refused: Not
authorized" error code. Further requiring or documenting authentication
and/or authorization features from the SCU or SCP is beyond the scope of
this SOP Class.

.. _sect_CC.2.2.4:

Status Codes
^^^^^^^^^^^^

`table_title <#table_CC.2.2-2>`__ defines the status code values that
might be returned in a N-ACTION response. General status code values and
fields related to status code values are defined for N-ACTION DIMSE
Service in .

.. table:: N-ACTION Response Status Values [for Request UPS Cancel]

   +--------------------------+--------------------------+-------------+
   | Service Status           | Further Meaning          | Status Code |
   +==========================+==========================+=============+
   | Success                  | The cancel request is    | 0000        |
   |                          | acknowledged             |             |
   +--------------------------+--------------------------+-------------+
   | Warning                  | The UPS is already in    | B304        |
   |                          | the requested state of   |             |
   |                          | CANCELED                 |             |
   +--------------------------+--------------------------+-------------+
   | Failure                  | Failed: The UPS is       | C311        |
   |                          | already COMPLETED        |             |
   +--------------------------+--------------------------+-------------+
   | Failed: Performer        | C313                     |             |
   | chooses not to cancel    |                          |             |
   +--------------------------+--------------------------+-------------+
   | Failed: Specified SOP    | C307                     |             |
   | Instance UID does not    |                          |             |
   | exist or is not a UPS    |                          |             |
   | Instance managed by this |                          |             |
   | SCP                      |                          |             |
   +--------------------------+--------------------------+-------------+
   | Failed: The performer    | C312                     |             |
   | cannot be contacted      |                          |             |
   +--------------------------+--------------------------+-------------+

.. _sect_CC.2.3:

Subscribe/Unsubscribe to Receive UPS Event Reports (N-ACTION)
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

This operation allows an SCU to subscribe with an SCP in order to
receive N-EVENT-REPORTS of subsequent changes to the state of a UPS
instance, or to unsubscribe in order to no longer receive such
N-EVENT-REPORTs. This operation shall be invoked by the SCU through the
DIMSE N-ACTION Service.

.. _sect_CC.2.3.1:

Action Information
^^^^^^^^^^^^^^^^^^

DICOM AEs that claim conformance to the UPS Watch SOP Class as an SCU
and/or an SCP shall support the Action Types and Action Information as
specified in `table_title <#table_CC.2.3-1>`__.

.. table:: Subscribe/Unsubscribe to Receive UPS Event Reports - Action
Information

   +-------------+-------------+-------------+-------------+-------------+
   | Action Type | Action Type | Attribute   | Tag         | Requirement |
   | Name        | ID          | Name        |             | Type        |
   |             |             |             |             | SCU/SCP     |
   +=============+=============+=============+=============+=============+
   | Subscribe   | 3           | Receiving   | (0074,1234) | 1/1         |
   | to Receive  |             | AE          |             |             |
   | UPS Event   |             |             |             |             |
   | Reports     |             |             |             |             |
   +-------------+-------------+-------------+-------------+-------------+
   | Deletion    | (0074,1230) | 1/1         |             |             |
   | Lock        |             |             |             |             |
   +-------------+-------------+-------------+-------------+-------------+
   | Match Keys  | 1/1         |             |             |             |
   | (see        |             |             |             |             |
   | `Action     |             |             |             |             |
   | Informatio  |             |             |             |             |
   | n <#sect_CC |             |             |             |             |
   | .2.3.1>`__) |             |             |             |             |
   +-------------+-------------+-------------+-------------+-------------+
   | Unsubscribe | 4           | Receiving   | (0074,1234) | 1/1         |
   | from        |             | AE          |             |             |
   | Receiving   |             |             |             |             |
   | UPS Event   |             |             |             |             |
   | Reports     |             |             |             |             |
   +-------------+-------------+-------------+-------------+-------------+
   | Suspend     | 5           | Receiving   | (0074,1234) | 1/1         |
   | Global      |             | AE          |             |             |
   | S           |             |             |             |             |
   | ubscription |             |             |             |             |
   +-------------+-------------+-------------+-------------+-------------+

Each AE may be in one of three UPS Subscription States for each existing
UPS Instance: Not Subscribed, Subscribed with Deletion Lock, or
Subscribed w/o Deletion Lock. The UPS Subscription State determines
whether N-EVENT-REPORTs relating to a UPS Instance will be sent to the
AE.

Each AE may also be in one of three Global Subscription States for a
given SCP: No Global Subscription, Globally Subscribed with Deletion
Lock, Globally Subscribed w/o Deletion Lock. The Global Subscription
State mainly determines the initial UPS Subscription State for an AE and
new UPS Instances created by the SCP. Changes to the Global Subscription
State can also change the UPS Subscription State for existing UPS
Instances as described in `table_title <#table_CC.2.3-2>`__.

The three Subscription actions in `table_title <#table_CC.2.3-1>`__ are
used to manage the UPS Subscription State and Global Subscription State
of an AE.

`table_title <#table_CC.2.3-2>`__ describes the UPS Subscription State
transitions of an AE for a given UPS Instance. Each row in the table
defines what should happen in response to a Subscription Action, or a
UPS creation event, given the initial state. The table also shows when
an initial event message should be sent to the AE describing the
"Current UPS State".

.. note::

   In general, instance specific instructions take precedence over
   global instructions. The exception is the Unsubscribe Globally
   instruction, which removes all subscriptions, global and specific. To
   simply stop globally subscribing to new instances without removing
   specific subscriptions, use the Suspend Global Subscription message.

Most actions affect only the UPS Subscription State of a single UPS
Instance. However, Global actions potentially affect all existing UPS
Instances managed by the SCP and this is indicated in the following
table by "All". For example, in the "AE Subscribes Globally with Lock"
row, the content of the "Not Subscribed" cell means that in addition to
setting the Global Subscription State for the AE to "Global Subscription
with Lock", all existing UPS Instances whose UPS Subscription State for
the Receiving AE is "Not Subscribed" will each have their UPS
Subscription State changed to "Subscribed with Lock" and an event will
be sent to the Receiving AE for each Instance.

.. table:: UPS Subscription State Transition Table

   +-------------+-------------+-------------+-------------+-------------+
   |             | **States    |             |             |             |
   |             | (for a      |             |             |             |
   |             | specific    |             |             |             |
   |             | UPS and     |             |             |             |
   |             | AE)**       |             |             |             |
   +=============+=============+=============+=============+=============+
   | Events      | *null*      | Not         | Subscribed  | Subscribed  |
   |             |             | Subscribed  | with Lock   | w/o Lock    |
   +-------------+-------------+-------------+-------------+-------------+
   | A UPS is    | Go to Not   | *N/A*       | *N/A*       | *N/A*       |
   | Created     | Subscribed  |             |             |             |
   | when the AE |             |             |             |             |
   | Global      |             |             |             |             |
   | S           |             |             |             |             |
   | ubscription |             |             |             |             |
   | State is    |             |             |             |             |
   | "No Global  |             |             |             |             |
   | Su          |             |             |             |             |
   | bscription" |             |             |             |             |
   +-------------+-------------+-------------+-------------+-------------+
   | A UPS is    | Go to       | *N/A*       | *N/A*       | *N/A*       |
   | Created     | Subscribed  |             |             |             |
   | when the AE | with Lock;  |             |             |             |
   | Global      | Send        |             |             |             |
   | S           | initial     |             |             |             |
   | ubscription | event       |             |             |             |
   | State is    |             |             |             |             |
   | "Global     |             |             |             |             |
   | S           |             |             |             |             |
   | ubscription |             |             |             |             |
   | with Lock"  |             |             |             |             |
   +-------------+-------------+-------------+-------------+-------------+
   | A UPS is    | Go to       | *N/A*       | *N/A*       | *N/A*       |
   | Created     | Subscribed  |             |             |             |
   | when the AE | w/o Lock;   |             |             |             |
   | Global      | Send        |             |             |             |
   | S           | initial     |             |             |             |
   | ubscription | event       |             |             |             |
   | State is    |             |             |             |             |
   | "Global     |             |             |             |             |
   | S           |             |             |             |             |
   | ubscription |             |             |             |             |
   | w/o Lock"   |             |             |             |             |
   +-------------+-------------+-------------+-------------+-------------+
   | AE          | *N/A*       | *AE Global  | *AE Global  | *AE Global  |
   | Subscribes  |             | State is    | State is    | State is    |
   | Globally    |             | now "Global | now "Global | now "Global |
   | with Lock   |             | Sub. with   | Sub. with   | Sub. with   |
   |             |             | Lock";*     | Lock";*     | Lock";*     |
   |             |             |             |             |             |
   |             |             | All Go to   | No UPS      | No UPS      |
   |             |             | Subscribed  | state       | state       |
   |             |             | with Lock;  | change;     | change;     |
   |             |             | All Send    |             |             |
   |             |             | initial     |             |             |
   |             |             | event       |             |             |
   +-------------+-------------+-------------+-------------+-------------+
   | AE          | *N/A*       | *AE Global  | *AE Global  | *AE Global  |
   | Subscribes  |             | State is    | State is    | State is    |
   | Globally    |             | now "Global | now "Global | now "Global |
   | w/o Lock    |             | Sub. w/o    | Sub. w/o    | Sub. w/o    |
   |             |             | Lock"*;     | Lock";*     | Lock";*     |
   |             |             |             |             |             |
   |             |             | All Go to   | *No UPS     | No UPS      |
   |             |             | Subscribed  | state       | state       |
   |             |             | w/o Lock;   | change;*    | change;     |
   +-------------+-------------+-------------+-------------+-------------+
   | AE          | *N/A*       | Go to       | No UPS      | Go to       |
   | Subscribes  |             | Subscribed  | state       | Subscribed  |
   | to Specific |             | with Lock;  | change;     | with Lock;  |
   | UPS with    |             | Send        | Send        | Send        |
   | Lock        |             | initial     | initial     | initial     |
   |             |             | event       | event       | event       |
   +-------------+-------------+-------------+-------------+-------------+
   | AE          | *N/A*       | Go to       | Go to       | No UPS      |
   | Subscribes  |             | Subscribed  | Subscribed  | state       |
   | to Specific |             | w/o Lock;   | w/o Lock;   | change;     |
   | UPS without |             | Send        | Send        | Send        |
   | Lock        |             | initial     | initial     | initial     |
   |             |             | event       | event       | event       |
   +-------------+-------------+-------------+-------------+-------------+
   | AE          | *N/A*       | No UPS      | Go to Not   | Go to Not   |
   | U           |             | state       | Subscribed  | Subscribed  |
   | nsubscribes |             | change      |             |             |
   | from        |             |             |             |             |
   | Specific    |             |             |             |             |
   | UPS         |             |             |             |             |
   +-------------+-------------+-------------+-------------+-------------+
   | AE          | *N/A*       | *AE Global  | *AE Global  | *AE Global  |
   | U           |             | State is    | State is    | State is    |
   | nsubscribes |             | now "No     | now "No     | now "No     |
   | Globally    |             | Global      | Global      | Global      |
   |             |             | Subs        | Subs        | Subs        |
   |             |             | cription"*; | cription";* | cription";* |
   |             |             |             |             |             |
   |             |             | No UPS      | All Go to   | All Go to   |
   |             |             | state       | Not         | Not         |
   |             |             | change;     | Subscribed; | Subscribed; |
   +-------------+-------------+-------------+-------------+-------------+
   | AE Suspends | *N/A*       | *AE Global  | *AE Global  | *AE Global  |
   | Global      |             | State is    | State is    | State is    |
   | S           |             | now "No     | now "No     | now "No     |
   | ubscription |             | Global      | Global      | Global      |
   |             |             | Subs        | Subs        | Subs        |
   |             |             | cription";* | cription";* | cription";* |
   |             |             |             |             |             |
   |             |             | No UPS      | No UPS      | No UPS      |
   |             |             | state       | state       | state       |
   |             |             | change;     | change;     | change;     |
   +-------------+-------------+-------------+-------------+-------------+

See Reliable Watchers and Deletion Locks for further discussion of
deletion locks.

.. _sect_CC.2.3.2:

Service Class User Behavior
^^^^^^^^^^^^^^^^^^^^^^^^^^^

The SCU subscribing to track the progress and results of the scheduled
procedure step may be the system that created the UPS as an SCU of the
UPS Push SOP Class, or it may be some other interested observer.

An SCU shall use the N-ACTION primitive to request the SCP to subscribe
an AE (usually the requesting SCU) to receive event reports relating to
UPS instances managed by the SCP. Since all UPSs are created as
instances of the UPS Push SOP Class, the Requested SOP Class UID
(0000,0003) in the N-ACTION request shall be the UID of the UPS Push SOP
Class. See `Service Class and SOP Class UIDs <#sect_CC.3.1>`__ for
further details.

An SCU shall also use the N-ACTION primitive to request the SCP to
unsubscribe an AE to stop receiving event reports relating to UPS
instances managed by the SCP. Action Information is specified in
`table_title <#table_CC.2.3-1>`__. The SCU shall always provide the
AE-TITLE that is to receive (or stop receiving) the N-EVENT-REPORTs.

To subscribe for events relating to a single specific UPS instance
managed by the SCP, the SCU shall use Action Type ID 3 (Subscribe to
Receive UPS Event Reports) and provide the SOP Instance UID of the
specific UPS instance in the N-ACTION primitive request. The SCU shall
indicate a need for the UPS instance to persist after its state has
changed to COMPLETED or CANCELED by setting the value of the Deletion
Lock to TRUE. Otherwise the SCU shall set the value of the Deletion Lock
to FALSE.

To unsubscribe for events relating to a single specific UPS instance
managed by the SCP, the SCU shall use Action Type ID 4 (Unsubscribe from
Receiving UPS Event Reports) and provide the SOP Instance UID of the
specific UPS instance in the N-ACTION primitive request.

To subscribe for events relating to all current and subsequently created
UPS instances managed by the SCP, the SCU shall use Action Type ID 3
(Subscribe to Receive UPS Event Reports) and provide the well-known UID
1.2.840.10008.5.1.4.34.5 in the N-ACTION primitive request. The SCU
shall indicate a need for UPS instances to persist after their states
have changed to COMPLETED or CANCELED by setting the value of the
Deletion Lock to TRUE. Otherwise the SCU shall set the value of the
Deletion Lock to FALSE.

.. note::

   This "global subscription" is useful for SCUs that wish to monitor
   all activities without having to issue regular C-FINDs to identify
   new UPS instances.

To subscribe for events relating to a filtered subset of all current and
subsequently created UPS instances (Filtered Global Subscription)
managed by the SCP, the SCU shall use Action Type ID 3 (Subscribe to
Receive UPS Event Reports) and provide both the well-known UID
1.2.840.10008.5.1.4.34.5.1 and a set of Matching Keys and values in the
N-ACTION primitive request (see `Filtered Global
Subscription <#sect_CC.2.3.3.1>`__). The SCU shall indicate a need for
UPS instances to persist after their states have changed to COMPLETED or
CANCELED by setting the value of the Deletion Lock to TRUE. Otherwise
the SCU shall set the value of the Deletion Lock to FALSE.

.. note::

   The well-known UID for a Filtered Global Subscription is distinct
   from the Global Subscription well-known UID.

To unsubscribe for events relating to all current UPS instances managed
by the SCP and also stop being subscribed to subsequently created UPS
instances, the SCU shall use Action Type ID 4 (Unsubscribe from
Receiving UPS Event Reports) and provide the well-known UID
1.2.840.10008.5.1.4.34.5 in the N-ACTION primitive request.

.. note::

   This "global unsubscription" is useful for SCUs that wish to stop
   monitoring all activities and release all deletion locks (if any)
   placed for this subscriber.

To just stop being subscribed to subsequently created UPS instances, but
still continue to receive events for currently subscribed instances
managed by the SCP, the SCU shall use Action Type ID 5 (Suspend Global
Subscription) and provide the well-known UID 1.2.840.10008.5.1.4.34.5 in
the N-ACTION primitive request.

For each UPS instance on which the SCU has placed a deletion lock,
either explicitly on the specific instance or implicitly via a global
subscription with lock, the SCU shall remove the deletion lock once any
needed final state information for the instance has been obtained. The
deletion lock may be removed either by unsubscribing or by subscribing
with the value of the Deletion Lock set to FALSE.

.. note::

   The SCP will retain COMPLETED or CANCELED UPS Instances until all
   deletion locks have been released. Failure by SCUs to release the
   deletion lock may cause problems for the SCP. SCUs that do not have a
   significant need for the final state information, or who cannot
   dependably remove deletion locks should not use deletion locks.

The successful N-ACTION Response Status Code indicates that the SCP has
received the N-ACTION request and the Subscription State for the AE has
been successfully modified.

.. note::

   1. When subscribing to a specific instance, the SCU can also expect
      to receive an initial N-EVENT-REPORT containing the current state
      of the UPS instance. When subscribing globally with the Deletion
      Lock set to TRUE, the SCU can expect to receive initial
      N-EVENT-REPORTs for every instance currently managed by the SCP.
      Initial N-EVENT-REPORTs for newly created instances, received as a
      result of a global subscription, will appear as transitions to the
      SCHEDULED state.

   2. The UPS-RS User-Agent is responsible for opening the
      N-EVENT-REPORT communication channel (see ). The UPS-RS User-Agent
      is also responsible for re-establishing the N-EVENT-REPORT
      communication channel if it is disconnected. This differs from the
      DIMSE approach where the UPS SCP opens an Association for
      N-EVENT-REPORT messages as necessary.

A warning N-ACTION Response Status Code of "Deletion Lock not granted",
indicates that the AE subscription requested by the SCU was successful,
but the deletion lock has not been set.

A failure N-ACTION Response Status Code indicates that the subscription
state change requested will not be processed and no subscription states
have been changed. The action taken by the SCU upon receiving this
status is beyond the scope of this Standard.

At any time after receipt of the N-ACTION-Response, the SCU may release
the association on which it sent the N-ACTION-Request.

.. _sect_CC.2.3.3:

Service Class Provider Behavior
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

Upon receipt of the N-ACTION request, the SCP shall attempt to update
the Global Subscription State and/or UPS Subscription State of the
specified AE with respect to the specified SOP Instance UID as described
in `table_title <#table_CC.2.3-2>`__ and then return, via the N-ACTION
response primitive, the appropriate N-ACTION Response Status Code.

The SCP may optionally allow an Application Entity to subscribe globally
to a filtered set of UPS Instances. In this case, the Application Entity
will only be subscribed to existing and future UPS Instances that match
the search criteria specified by the Matching Keys of the N-ACTION
request (see `Filtered Global Subscription <#sect_CC.2.3.3.1>`__). If
the SCP does not support Filtered Global Subscription it will return a
Failure response with a Code of C307 (see
`table_title <#table_CC.2.3-3>`__).

A success status conveys that the Global Subscription State and/or UPS
Subscription State for the AE specified in Receiving AE (0074,1234) was
successfully modified by the SCP. The AE-TITLE in Receiving AE
(0074,1234) may be different than the AE-TITLE used by the SCU for the
association negotiation. The SCP shall use the AE-TITLE specified in
Receiving AE (0074,1234). This allows systems to subscribe other systems
they know would be interested in events for a certain UPS.

For all UPS instances managed by the SCP, the SCP shall send
N-EVENT-REPORTS (as described in `Service Class Provider
Behavior <#sect_CC.2.4.3>`__) to AEs that have a UPS Subscription State
of "Subscribed with Lock" or "Subscribed w/o Lock". If the SCP also
supports the HTTP CreateSubscription service as an Origin-Server, the
SCP shall also send HTTP SendEventReport messages (see ).

Upon successfully processing a subscription action, the SCP shall send
initial UPS State Report N-EVENT-REPORTs, as indicated in
`table_title <#table_CC.2.3-2>`__, providing the current status of the
UPS Instance to the Receiving AE.

The SCP may also refuse both specific and global Subscription requests
by returning a failure N-ACTION Response Status Code for "Refused:
Refused: Not authorized" if the refusal depends on permissions related
to the tasks or the requestor, or "Refused: SCP does not support Event
Reports" if the SCP does not support sending the events. The SCP must
document in its conformance statement if it might refuse Subscription
requests.

The SCP may remove existing Deletion Locks by changing the UPS
Subscription State for the AE from "Subscribed with Lock" to "Subscribed
w/o Lock" and/or by changing the Global Subscription State for an AE
from "Global Subscription with Lock" to "Global Subscription w/o Lock".
This is intended to allow the SCP to deal with SCU malfunctions. The SCP
must document in its conformance statement if it might remove a Deletion
Lock.

The SCP may also refuse the Deletion Lock portion of a specific or
global Subscription request. For example, a request to modify the UPS
Subscription State for the AE to "Subscribed with Lock" would instead
result in a UPS Subscription State of "Subscribed w/o Lock" and a
Warning status (see `table_title <#table_CC.2.3-3>`__) returned to the
requesting SCU. This is intended to deal with Security and related
policy restrictions. The SCP must document in its conformance statement
if it might refuse a Deletion Lock.

Bi-directional Authentication of machines/users/applications is possible
at association time (see and ). provides a "Refused: Refused: Not
authorized" error code. Further requiring or documenting authentication
and/or authorization features from the SCU or SCP is beyond the scope of
this SOP Class.

.. _sect_CC.2.3.3.1:

Filtered Global Subscription
''''''''''''''''''''''''''''

An SCP that supports Filtered Global Subscription shall create an
instance subscription for each UPS Instance that would match a C-FIND
request with the Matching Keys provided in the subscription request.

The SCP shall support the same matching logic used for C-FIND (see
`Service Class Provider Behavior <#sect_CC.2.8.3>`__).

.. _sect_CC.2.3.4:

Status Codes
^^^^^^^^^^^^

`table_title <#table_CC.2.3-3>`__ defines the status code values that
might be returned in a N-ACTION response. General status code values and
fields related to status code values are defined for N-ACTION DIMSE
Service in .

.. table:: N-ACTION Response Status Values [for Subscribe/Unsubscribe to
Receive UPS sEvent Reports]

   +--------------------------+--------------------------+-------------+
   | Service Status           | Further Meaning          | Status Code |
   +==========================+==========================+=============+
   | Success                  | The requested change of  | 0000        |
   |                          | subscription state was   |             |
   |                          | performed                |             |
   +--------------------------+--------------------------+-------------+
   | Warning                  | Deletion Lock not        | B301        |
   |                          | granted.                 |             |
   +--------------------------+--------------------------+-------------+
   | Failure                  | Failed: Specified SOP    | C307        |
   |                          | Instance UID does not    |             |
   |                          | exist or is not a UPS    |             |
   |                          | Instance managed by this |             |
   |                          | SCP                      |             |
   +--------------------------+--------------------------+-------------+
   | Failed: Receiving        | C308                     |             |
   | AE-TITLE is Unknown to   |                          |             |
   | this SCP                 |                          |             |
   +--------------------------+--------------------------+-------------+
   | Failed: Specified action | C314                     |             |
   | not appropriate for      |                          |             |
   | specified instance       |                          |             |
   +--------------------------+--------------------------+-------------+
   | Failed: SCP does not     | C315                     |             |
   | support Event Reports    |                          |             |
   +--------------------------+--------------------------+-------------+

.. _sect_CC.2.4:

Report a Change in UPS Status (N-EVENT-REPORT)
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

This operation allows an SCP to notify an SCU of a change in state of a
UPS instance or a change in state of the SCP itself. This operation
shall be invoked by the SCP through the DIMSE N-EVENT-REPORT Service.

.. _sect_CC.2.4.1:

Event Report Information
^^^^^^^^^^^^^^^^^^^^^^^^

DICOM AEs that claim conformance to the UPS Event SOP Class as an SCU
and/or an SCP shall support the Event Type IDs and Event Report
Attributes as specified in `table_title <#table_CC.2.4-1>`__.

.. table:: Report a Change in UPS Status - Event Report Information

   +-------------+-------------+-------------+-------------+-------------+
   | Event Type  | Event Type  | Attribute   | Tag         | Req. Type   |
   | Name        | ID          | Name        |             | SCU/SCP     |
   +=============+=============+=============+=============+=============+
   | UPS State   | 1           | Procedure   | (0074,1000) | -/1         |
   | Report      |             | Step State  |             |             |
   +-------------+-------------+-------------+-------------+-------------+
   | Input       | (0040,4041) | -/1         |             |             |
   | Readiness   |             |             |             |             |
   | State       |             |             |             |             |
   +-------------+-------------+-------------+-------------+-------------+
   | Reason For  | (0074,1238) | -/3         |             |             |
   | C           |             |             |             |             |
   | ancellation |             |             |             |             |
   +-------------+-------------+-------------+-------------+-------------+
   | Procedure   | (0074,100e) | -/3         |             |             |
   | Step        |             |             |             |             |
   | Disc        |             |             |             |             |
   | ontinuation |             |             |             |             |
   | Reason Code |             |             |             |             |
   | Sequence    |             |             |             |             |
   +-------------+-------------+-------------+-------------+-------------+
   | *>Includ    |             |             |             |             |
   | e*\ `table_ |             |             |             |             |
   | title <#tab |             |             |             |             |
   | le_8-3a>`__ |             |             |             |             |
   +-------------+-------------+-------------+-------------+-------------+
   | UPS Cancel  | 2           | Requesting  | (0074,1236) | -/1         |
   | Requested   |             | AE          |             |             |
   +-------------+-------------+-------------+-------------+-------------+
   | Reason For  | (0074,1238) | -/1C        |             |             |
   | C           |             |             |             |             |
   | ancellation |             | Required if |             |             |
   |             |             | provided in |             |             |
   |             |             | the         |             |             |
   |             |             | triggering  |             |             |
   |             |             | N-ACTION    |             |             |
   +-------------+-------------+-------------+-------------+-------------+
   | Procedure   | (0074,100e) | -/1C        |             |             |
   | Step        |             |             |             |             |
   | Disc        |             | Required if |             |             |
   | ontinuation |             | provided in |             |             |
   | Reason Code |             | the         |             |             |
   | Sequence    |             | triggering  |             |             |
   |             |             | N-ACTION    |             |             |
   +-------------+-------------+-------------+-------------+-------------+
   | *>Includ    |             |             |             |             |
   | e*\ `table_ |             |             |             |             |
   | title <#tab |             |             |             |             |
   | le_8-3a>`__ |             |             |             |             |
   +-------------+-------------+-------------+-------------+-------------+
   | Contact URI | (0074,100a) | -/1C        |             |             |
   |             |             |             |             |             |
   |             |             | Required if |             |             |
   |             |             | provided in |             |             |
   |             |             | the         |             |             |
   |             |             | triggering  |             |             |
   |             |             | N-ACTION    |             |             |
   +-------------+-------------+-------------+-------------+-------------+
   | Contact     | (0074,100c) | -/1C        |             |             |
   | Display     |             |             |             |             |
   | Name        |             | Required if |             |             |
   |             |             | provided in |             |             |
   |             |             | the         |             |             |
   |             |             | triggering  |             |             |
   |             |             | N-ACTION    |             |             |
   +-------------+-------------+-------------+-------------+-------------+
   | UPS         | 3           | Progress    | (0074,1002) | -/1         |
   | Progress    |             | Information |             |             |
   | Report      |             | Sequence    |             |             |
   +-------------+-------------+-------------+-------------+-------------+
   | >Procedure  | (0074,1004) | -/3         |             |             |
   | Step        |             |             |             |             |
   | Progress    |             |             |             |             |
   +-------------+-------------+-------------+-------------+-------------+
   | >Procedure  | (0074,1006) | -/3         |             |             |
   | Step        |             |             |             |             |
   | Progress    |             |             |             |             |
   | Description |             |             |             |             |
   +-------------+-------------+-------------+-------------+-------------+
   | >Procedure  | (0074,1007) | -/3         |             |             |
   | Step        |             |             |             |             |
   | Progress    |             |             |             |             |
   | Parameters  |             |             |             |             |
   | Sequence    |             |             |             |             |
   +-------------+-------------+-------------+-------------+-------------+
   | >Procedure  | (0074,1008) | -/3         |             |             |
   | Step        |             |             |             |             |
   | Com         |             |             |             |             |
   | munications |             |             |             |             |
   | URI         |             |             |             |             |
   | Sequence    |             |             |             |             |
   +-------------+-------------+-------------+-------------+-------------+
   | >>Contact   | (0074,100a) | -/1         |             |             |
   | URI         |             |             |             |             |
   +-------------+-------------+-------------+-------------+-------------+
   | >>Contact   | (0074,100c) | -/3         |             |             |
   | Display     |             |             |             |             |
   | Name        |             |             |             |             |
   +-------------+-------------+-------------+-------------+-------------+
   | SCP Status  | 4           | SCP Status  | (0074,1242) | -/1         |
   | Change      |             |             |             |             |
   +-------------+-------------+-------------+-------------+-------------+
   | S           | (0074,1244) | -/1         |             |             |
   | ubscription |             |             |             |             |
   | List Status |             |             |             |             |
   +-------------+-------------+-------------+-------------+-------------+
   | Unified     | (0074,1246) | -/1         |             |             |
   | Procedure   |             |             |             |             |
   | Step List   |             |             |             |             |
   | Status      |             |             |             |             |
   +-------------+-------------+-------------+-------------+-------------+
   | UPS         | 5           | Scheduled   | (0040,4025) | -/1C        |
   | Assigned    |             | Station     |             |             |
   |             |             | Name Code   |             | Required if |
   |             |             | Sequence    |             | populated   |
   |             |             |             |             | in the UPS  |
   |             |             |             |             | Instance    |
   +-------------+-------------+-------------+-------------+-------------+
   | *>Includ    |             |             |             |             |
   | e*\ `table_ |             |             |             |             |
   | title <#tab |             |             |             |             |
   | le_8-3a>`__ |             |             |             |             |
   +-------------+-------------+-------------+-------------+-------------+
   | Human       | (0040,4009) | -/1C        |             |             |
   | Performer   |             |             |             |             |
   | Code        |             | Required if |             |             |
   | Sequence    |             | populated   |             |             |
   |             |             | in the UPS  |             |             |
   |             |             | Instance    |             |             |
   +-------------+-------------+-------------+-------------+-------------+
   | *>Includ    |             |             |             |             |
   | e*\ `table_ |             |             |             |             |
   | title <#tab |             |             |             |             |
   | le_8-3a>`__ |             |             |             |             |
   +-------------+-------------+-------------+-------------+-------------+
   | Human       | (0040,4036) | -/1C        |             |             |
   | Performer's |             |             |             |             |
   | O           |             | Required if |             |             |
   | rganization |             | populated   |             |             |
   |             |             | in the UPS  |             |             |
   |             |             | Instance    |             |             |
   +-------------+-------------+-------------+-------------+-------------+

.. note::

   The meanings of the Progress Information Attribute Values in the
   context of a specific task are undefined, and the values may be
   obsolete when the UPS has moved to the COMPLETED or CANCELED state.

.. _sect_CC.2.4.2:

Service Class User Behavior
^^^^^^^^^^^^^^^^^^^^^^^^^^^

The SCU shall return, via the N-EVENT-REPORT response primitive, the
N-EVENT-REPORT Response Status Code applicable to the associated
request. See for general response status codes.

The SCU shall accept all Attributes included in any notification. No
requirements are placed on what the SCU will do as a result of receiving
this information.

.. note::

   An SCU may receive N-EVENT-REPORTs with an Event Type ID of 1 (UPS
   State Report) either due to a state change to the UPS, or in response
   to initial subscription to the UPS (possibly when the UPS is
   initially created). See `Service Class Provider
   Behavior <#sect_CC.2.3.3>`__.

If an SCU performing a UPS receives an N-EVENT-REPORT for that instance
with an Event Type ID of 2 (UPS Cancel Requested), then this SCU may, at
its own discretion, choose to cancel the UPS as described in `Service
Class User Behavior <#sect_CC.2.1.2>`__.

.. note::

   1. A UPS Cancel Requested notification includes the AE of the
      Requesting SCU, which could be useful to the performing SCU in
      deciding the significance/authority of the Cancel Request.

   2. The Reason For Cancellation, a proposed Procedure Step
      Discontinuation Reason Code Sequence, a Contact Display Name and a
      Contact URI of someone responsible for the Cancel Request may also
      be provided in the notification. Some performing SCUs might find
      this information useful in deciding to cancel the UPS or might
      provide the information to an operator so they can make contact
      for the purpose of clarifying or confirming the Cancel Request. If
      the performing SCU chooses to Cancel the UPS, it may at its own
      discretion set the Procedure Step Discontinuation Reason Code
      Sequence in the UPS instance based on the corresponding values
      provided.

If an SCU receives an N-EVENT-REPORT for an instance with an Event Type
ID of 5 (UPS Assigned) and the device or human specified in the
notification correspond to the SCU, then the UPS has been assigned to
that SCU.

An SCU that wishes to start/stop receiving N-EVENT-REPORTs about UPS
instances may subscribe/unsubscribe as described in `Service Class User
Behavior <#sect_CC.2.3.2>`__.

If an SCU receives an N-EVENT-REPORT with an Event Type ID of 4 (SCP
Status Change), it is not required to act on that information, however
the SCU may want to consider actions such as: re-subscribing if the
subscription list has been Cold Started, verifying (and recreating if
necessary) scheduled UPSs if the UPS list has been Cold Started, etc.

.. note::

   An SCU may receive SCP State Change Events from any SCP with which it
   is currently subscribed either globally or for any specific UPS.

.. _sect_CC.2.4.3:

Service Class Provider Behavior
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

The SCP shall specify in the N-EVENT-REPORT Request Primitive the Event
Type ID and the UID of the UPS Instance with which the event is
associated. Since all UPSs are created as instances of the UPS Push SOP
Class, the Affected SOP Class UID (0000,0002) in the N-EVENT-REPORT
request shall be the UID of the UPS Push SOP Class. See `Service Class
and SOP Class UIDs <#sect_CC.3.1>`__ for further details. The SCP shall
additionally include Attributes related to the event as defined in
`table_title <#table_CC.2.4-1>`__.

Each time the SCP completes a Subscribe to Receive UPS Event Reports
Action (see `Action Information <#sect_CC.2.3.1>`__) for a specific UPS
instance, the SCP shall send to the Receiving AE a UPS State Report
Event and provide the current value of the Procedure Step State
(0074,1000) and Input Readiness State (0040,4041) Attributes for the UPS
instance.

Each time the SCP completes a Subscribe to Receive UPS Event Reports
Action (see `Action Information <#sect_CC.2.3.1>`__) for the well-known
UID 1.2.840.10008.5.1.4.34.5 with the value of the Deletion Lock set to
TRUE (i.e., a Global Subscription with Lock), the SCP shall send to the
Receiving AE a UPS State Report Event for every UPS Instance managed by
the SCP and provide the current value of the Procedure Step State
(0074,1000) and Input Readiness State (0040,4041) Attributes.

Each time the SCP creates a new UPS instance, the SCP shall send a UPS
State Report Event, indicating a change of status to SCHEDULED and the
initial value of and Input Readiness State (0040,4041), to all AEs with
a Global Subscription State of "Global Subscription with Lock" or
"Global Subscription w/o Lock". (see `Subscribe/Unsubscribe to Receive
UPS Event Reports (N-ACTION) <#sect_CC.2.3>`__)

Each time the SCP creates a new UPS instance and either the Scheduled
Station Name Code Sequence (0040,4025) or the Scheduled Human Performers
Sequence (0040,4034) is populated, the SCP shall also send a UPS
Assigned Event, with the current contents of the Scheduled Station Name
Code Sequence (0040,4025) and the Scheduled Human Performers Sequence
(0040,4034), to all AEs with a Global Subscription State of "Global
Subscription with Lock" or "Global Subscription w/o Lock".

In the following text "Subscribed SCUs" means all AEs where the UPS
Subscription State of the UPS Instance in question is "Subscribed with
Lock" or "Subscribed w/o Lock" (see `Subscribe/Unsubscribe to Receive
UPS Event Reports (N-ACTION) <#sect_CC.2.3>`__). If the SCP also
supports the HTTP CreateSubscription service as an Origin-Server,
"Subscribed SCUs" also includes all CreateSubscription User-Agents where
the UPS Subscription State of the UPS Instance in question is
"Subscribed with Lock" or "Subscribed w/o Lock" (see ).

Each time the SCP changes the Procedure Step State (0074,1000) Attribute
for a UPS instance, the SCP shall send a UPS State Report Event to
subscribed SCUs.

Each time the SCP changes the Input Readiness State (0040,4041)
Attribute for a UPS instance, the SCP shall send a UPS State Report
Event to subscribed SCUs.

Each time the SCP receives an N-ACTION with an Action Type ID of 2
(Request UPS Cancel), the SCP shall send a UPS Cancel Requested Event to
subscribed SCUs. The SCP shall include the AE Title of the triggering
N-ACTION SCU in the Requesting AE Attribute. The SCP shall include the
Reason For Cancellation, Contact Display Name and Contact URI Attributes
if they were provided in the triggering N-ACTION.

Each time the SCP updates the Scheduled Station Name Code Sequence
(0040,4025) or the Scheduled Human Performers Sequence (0040,4034) for a
UPS instance, the SCP shall send a UPS Assigned Event, with the current
contents of the Scheduled Station Name Code Sequence (0040,4025) and the
Scheduled Human Performers Sequence (0040,4034), to subscribed SCUs.

Each time the SCP updates the Procedure Step Progress (0074,1004), the
Procedure Step Progress Description (0074,1006), or the contents of the
Procedure Step Communications URI Sequence (0074,1008) for a UPS
instance, the SCP shall send a UPS Progress Event, with the current
contents of the Progress Information Sequence (0074,1002), to subscribed
SCUs.

Each time the SCP is restarted, the SCP shall send an SCP Status Change
Event. The SCP, if it knows it is going down, may send an additional SCP
Status Change Event before it is shut down. Since the subscription lists
may be incomplete or missing in the event of a restart, the SCP shall
maintain a fallback list of AEs (for example as a configuration file, or
from an LDAP server). The SCP shall send the SCP Status Change Events
to:

-  all AEs on the fallback list and,

-  all AEs with a Global Subscription State of "Global Subscription with
   Lock" or "Global Subscription w/o Lock" and,

-  all AEs with a UPS Subscription State of "Subscribed with Lock" or
   "Subscribed w/o Lock" for any UPS Instance managed by the SCP

.. note::

   The SCP may choose to not send duplicate messages to an AE.

The value of SCP Status (0074,1242) shall be RESTARTED if the SCP is
sending this message due to being restarted and GOING DOWN if the SCP
will be shut down soon.

.. note::

   SCPs that report they are GOING DOWN might stop accepting new
   interactions from SCUs until after they have restarted.

When SCP Status (0074,1242) is RESTARTED, the value of Subscription List
Status (0074,1244) shall be WARM START if the SCP preserved the
Subscription List to the best of its knowledge, and COLD STARTED if the
SCP has not preserved the Subscription List.

When SCP Status (0074,1242) is RESTARTED, the value of Unified Procedure
Step List Status (0074,1246) shall be WARM START if the SCP preserved
the UPS List to the best of its knowledge, and COLD START if the SCP has
not preserved the UPS List.

If the SCP is unable to successfully complete an N-EVENT-REPORT to any
given SCU, the SCP has no obligation to queue or retry, and it should
not imply any effect on the subscription list or deletion locks.

.. _sect_CC.2.4.4:

Status Codes
^^^^^^^^^^^^

No Service Class specific status values are defined for the
N-EVENT-REPORT Service. See for general response status codes.

.. _sect_CC.2.5:

Create a Unified Procedure Step (N-CREATE)
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

This operation allows an SCU to instruct an SCP to create a Unified
Procedure Step. This operation shall be invoked by the SCU through the
DIMSE N-CREATE Service.

.. _sect_CC.2.5.1:

Unified Procedure Step Attribute Specification
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

An Application Entity that claims conformance to the UPS Push SOP Class
as an SCU shall provide all Required Attributes as specified in
`table_title <#table_CC.2.5-3>`__. Additional Attributes defined by the
UPS IOD may be provided as well.

An Application Entity that claims conformance to the UPS Push SOP Class
as an SCP shall support all required Attributes as specified in
`table_title <#table_CC.2.5-3>`__. Additional Attributes defined by the
UPS IOD may be supported as well.

.. _sect_CC.2.5.1.1:

UPS Final State Requirements
''''''''''''''''''''''''''''

COMPLETED and CANCELED are Final States for a UPS instance. The
Attributes and values of the UPS instance must meet certain requirements
before it may be placed in either of the Final States.

.. note::

   A UPS instance is in the SCHEDULED state when created. See `Unified
   Procedure Step States <#sect_CC.1.1>`__ for rules governing state
   transitions.

Attributes shall be valued as indicated by the Final State Codes in the
Final State Column of `table_title <#table_CC.2.5-3>`__ before the
Procedure Step State (0074,1000) may be set to COMPLETED or CANCELED
(i.e., Final State).

Performing systems are encouraged to ensure that the values for all
Attributes reasonably reflect what was done and the Final State of the
UPS. This may include blanking Attributes that are permitted to be empty
and for which no reasonable value can be determined. The UPS contents
should make it clear whether the step was completed, what work was done,
what results were produced and whether the results are usable. See for a
discussion of methods to convey things like partial completion.

.. note::

   The SCU may choose not to distribute, or otherwise make available,
   some or all instances created during the procedure step and
   referenced in the Output Information Sequence (0040,4033).

.. table:: Final State Codes

   +------------------+--------------------------------------------------+
   | Final State Code | Meaning                                          |
   +==================+==================================================+
   | R                | The UPS State shall not be set to COMPLETED or   |
   |                  | CANCELED if this Attribute does not have a       |
   |                  | value.                                           |
   +------------------+--------------------------------------------------+
   | RC               | The UPS State shall not be set to COMPLETED or   |
   |                  | CANCELED if the condition is met and this        |
   |                  | Attribute does not have a value.                 |
   +------------------+--------------------------------------------------+
   | P                | The UPS State shall not be set to COMPLETED if   |
   |                  | this Attribute does not have a value, but may be |
   |                  | set to CANCELED.                                 |
   +------------------+--------------------------------------------------+
   | X                | The UPS State shall not be set to CANCELED if    |
   |                  | this Attribute does not have a value, but may be |
   |                  | set to COMPLETED.                                |
   +------------------+--------------------------------------------------+
   | O                | The UPS State may be set to either COMPLETED or  |
   |                  | CANCELED if this Attribute does not have a       |
   |                  | value.                                           |
   +------------------+--------------------------------------------------+

.. _sect_CC.2.5.1.2:

UPS Macros
''''''''''

To reduce the size and complexity of `table_title <#table_CC.2.5-3>`__,
a macro notation is used.

For example, in `table_title <#table_CC.2.5-3>`__, a table entry
specifying "Include `table_title <#table_CC.2.5-2a>`__" should be
interpreted as including the following table of text as a substitution.
The nesting level for the sequence inclusion is indicated by the nesting
level on the reference to the macro. Where the matching key type
requirement is "*" it should be replaced with the matching key type
requirement of the sequence Attribute that incorporates this macro.

For code sequences that have requirements for N-CREATE, N-SET, N-GET, or
C-FIND behavior that differ from the Macro, the code sequence contents
are explicitly listed in the Table rather than specifying inclusion of
the Macro.

.. table:: UPS Code Sequence Macro

   +-------+-------+-------+-------+-------+-------+-------+-------+-------+
   | Attr  | Tag   | Req.  | Req.  | Final | Req.  | Match | R     | Remar |
   | ibute |       | Type  | Type  | State | Type  | Key   | eturn | k/Mat |
   | Name  |       | N-C   | N-SET |       | N-GET | Type  | Key   | ching |
   |       |       | REATE | (SCU  |       | (SCU  |       | Type  | Type  |
   |       |       | (SCU  | /SCP) |       | /SCP) |       |       |       |
   |       |       | /SCP) |       |       |       |       |       |       |
   +=======+=======+=======+=======+=======+=======+=======+=======+=======+
   | Code  | (     | 1C/1C | 1C/1C |       | -/1C  | \*    | 1C    | Code  |
   | Value | 0008, |       |       |       |       |       |       | Value |
   |       | 0100) |       |       |       |       |       |       | shall |
   |       |       |       |       |       |       |       |       | be    |
   |       |       |       |       |       |       |       |       | retr  |
   |       |       |       |       |       |       |       |       | ieved |
   |       |       |       |       |       |       |       |       | with  |
   |       |       |       |       |       |       |       |       | S     |
   |       |       |       |       |       |       |       |       | ingle |
   |       |       |       |       |       |       |       |       | Value |
   |       |       |       |       |       |       |       |       | Matc  |
   |       |       |       |       |       |       |       |       | hing. |
   |       |       |       |       |       |       |       |       |       |
   |       |       |       |       |       |       |       |       | Req   |
   |       |       |       |       |       |       |       |       | uired |
   |       |       |       |       |       |       |       |       | if    |
   |       |       |       |       |       |       |       |       | the   |
   |       |       |       |       |       |       |       |       | code  |
   |       |       |       |       |       |       |       |       | value |
   |       |       |       |       |       |       |       |       | l     |
   |       |       |       |       |       |       |       |       | ength |
   |       |       |       |       |       |       |       |       | is 16 |
   |       |       |       |       |       |       |       |       | chara |
   |       |       |       |       |       |       |       |       | cters |
   |       |       |       |       |       |       |       |       | or    |
   |       |       |       |       |       |       |       |       | less, |
   |       |       |       |       |       |       |       |       | and   |
   |       |       |       |       |       |       |       |       | the   |
   |       |       |       |       |       |       |       |       | code  |
   |       |       |       |       |       |       |       |       | value |
   |       |       |       |       |       |       |       |       | is    |
   |       |       |       |       |       |       |       |       | not a |
   |       |       |       |       |       |       |       |       | URN   |
   |       |       |       |       |       |       |       |       | or    |
   |       |       |       |       |       |       |       |       | URL.  |
   +-------+-------+-------+-------+-------+-------+-------+-------+-------+
   | C     | (     | 1C/1C | 1C/1C |       | -/1C  | \*    | 1C    | C     |
   | oding | 0008, |       |       |       |       |       |       | oding |
   | S     | 0102) |       |       |       |       |       |       | S     |
   | cheme |       |       |       |       |       |       |       | cheme |
   | Desig |       |       |       |       |       |       |       | Desig |
   | nator |       |       |       |       |       |       |       | nator |
   |       |       |       |       |       |       |       |       | shall |
   |       |       |       |       |       |       |       |       | be    |
   |       |       |       |       |       |       |       |       | retr  |
   |       |       |       |       |       |       |       |       | ieved |
   |       |       |       |       |       |       |       |       | with  |
   |       |       |       |       |       |       |       |       | S     |
   |       |       |       |       |       |       |       |       | ingle |
   |       |       |       |       |       |       |       |       | Value |
   |       |       |       |       |       |       |       |       | Matc  |
   |       |       |       |       |       |       |       |       | hing. |
   |       |       |       |       |       |       |       |       |       |
   |       |       |       |       |       |       |       |       | Shall |
   |       |       |       |       |       |       |       |       | be    |
   |       |       |       |       |       |       |       |       | pr    |
   |       |       |       |       |       |       |       |       | esent |
   |       |       |       |       |       |       |       |       | if    |
   |       |       |       |       |       |       |       |       | Code  |
   |       |       |       |       |       |       |       |       | Value |
   |       |       |       |       |       |       |       |       | (     |
   |       |       |       |       |       |       |       |       | 0008, |
   |       |       |       |       |       |       |       |       | 0100) |
   |       |       |       |       |       |       |       |       | or    |
   |       |       |       |       |       |       |       |       | Long  |
   |       |       |       |       |       |       |       |       | Code  |
   |       |       |       |       |       |       |       |       | Value |
   |       |       |       |       |       |       |       |       | (     |
   |       |       |       |       |       |       |       |       | 0008, |
   |       |       |       |       |       |       |       |       | 0119) |
   |       |       |       |       |       |       |       |       | is    |
   |       |       |       |       |       |       |       |       | pre   |
   |       |       |       |       |       |       |       |       | sent. |
   |       |       |       |       |       |       |       |       | May   |
   |       |       |       |       |       |       |       |       | be    |
   |       |       |       |       |       |       |       |       | pr    |
   |       |       |       |       |       |       |       |       | esent |
   |       |       |       |       |       |       |       |       | other |
   |       |       |       |       |       |       |       |       | wise. |
   +-------+-------+-------+-------+-------+-------+-------+-------+-------+
   | C     | (     | 1C/1C | 1C/1C |       | -/1C  | -     | 1C    | Req   |
   | oding | 0008, |       |       |       |       |       |       | uired |
   | S     | 0103) |       |       |       |       |       |       | if    |
   | cheme |       |       |       |       |       |       |       | the   |
   | Ve    |       |       |       |       |       |       |       | value |
   | rsion |       |       |       |       |       |       |       | of    |
   |       |       |       |       |       |       |       |       | C     |
   |       |       |       |       |       |       |       |       | oding |
   |       |       |       |       |       |       |       |       | S     |
   |       |       |       |       |       |       |       |       | cheme |
   |       |       |       |       |       |       |       |       | Desig |
   |       |       |       |       |       |       |       |       | nator |
   |       |       |       |       |       |       |       |       | (     |
   |       |       |       |       |       |       |       |       | 0008, |
   |       |       |       |       |       |       |       |       | 0102) |
   |       |       |       |       |       |       |       |       | is    |
   |       |       |       |       |       |       |       |       | not   |
   |       |       |       |       |       |       |       |       | suffi |
   |       |       |       |       |       |       |       |       | cient |
   |       |       |       |       |       |       |       |       | to    |
   |       |       |       |       |       |       |       |       | ide   |
   |       |       |       |       |       |       |       |       | ntify |
   |       |       |       |       |       |       |       |       | the   |
   |       |       |       |       |       |       |       |       | Code  |
   |       |       |       |       |       |       |       |       | Value |
   |       |       |       |       |       |       |       |       | (     |
   |       |       |       |       |       |       |       |       | 0008, |
   |       |       |       |       |       |       |       |       | 0100) |
   |       |       |       |       |       |       |       |       | unam  |
   |       |       |       |       |       |       |       |       | biguo |
   |       |       |       |       |       |       |       |       | usly. |
   |       |       |       |       |       |       |       |       |       |
   |       |       |       |       |       |       |       |       | Shall |
   |       |       |       |       |       |       |       |       | not   |
   |       |       |       |       |       |       |       |       | be    |
   |       |       |       |       |       |       |       |       | pr    |
   |       |       |       |       |       |       |       |       | esent |
   |       |       |       |       |       |       |       |       | if    |
   |       |       |       |       |       |       |       |       | C     |
   |       |       |       |       |       |       |       |       | oding |
   |       |       |       |       |       |       |       |       | S     |
   |       |       |       |       |       |       |       |       | cheme |
   |       |       |       |       |       |       |       |       | Desig |
   |       |       |       |       |       |       |       |       | nator |
   |       |       |       |       |       |       |       |       | (     |
   |       |       |       |       |       |       |       |       | 0008, |
   |       |       |       |       |       |       |       |       | 0102) |
   |       |       |       |       |       |       |       |       | is    |
   |       |       |       |       |       |       |       |       | ab    |
   |       |       |       |       |       |       |       |       | sent. |
   |       |       |       |       |       |       |       |       | May   |
   |       |       |       |       |       |       |       |       | be    |
   |       |       |       |       |       |       |       |       | pr    |
   |       |       |       |       |       |       |       |       | esent |
   |       |       |       |       |       |       |       |       | other |
   |       |       |       |       |       |       |       |       | wise. |
   +-------+-------+-------+-------+-------+-------+-------+-------+-------+
   | Code  | (     | 1/1   | 1/1   |       | -/1   | -     | 1     | Code  |
   | Me    | 0008, |       |       |       |       |       |       | Me    |
   | aning | 0104) |       |       |       |       |       |       | aning |
   |       |       |       |       |       |       |       |       | shall |
   |       |       |       |       |       |       |       |       | not   |
   |       |       |       |       |       |       |       |       | be    |
   |       |       |       |       |       |       |       |       | used  |
   |       |       |       |       |       |       |       |       | as    |
   |       |       |       |       |       |       |       |       | Mat   |
   |       |       |       |       |       |       |       |       | ching |
   |       |       |       |       |       |       |       |       | Key.  |
   +-------+-------+-------+-------+-------+-------+-------+-------+-------+
   | Long  | (     | 1C/1C | 1C/1C |       | -/1C  | \*    | 1C    | Long  |
   | Code  | 0008, |       |       |       |       |       |       | Code  |
   | Value | 0119) |       |       |       |       |       |       | Value |
   |       |       |       |       |       |       |       |       | shall |
   |       |       |       |       |       |       |       |       | be    |
   |       |       |       |       |       |       |       |       | retr  |
   |       |       |       |       |       |       |       |       | ieved |
   |       |       |       |       |       |       |       |       | with  |
   |       |       |       |       |       |       |       |       | S     |
   |       |       |       |       |       |       |       |       | ingle |
   |       |       |       |       |       |       |       |       | Value |
   |       |       |       |       |       |       |       |       | Matc  |
   |       |       |       |       |       |       |       |       | hing. |
   |       |       |       |       |       |       |       |       |       |
   |       |       |       |       |       |       |       |       | Shall |
   |       |       |       |       |       |       |       |       | be    |
   |       |       |       |       |       |       |       |       | pr    |
   |       |       |       |       |       |       |       |       | esent |
   |       |       |       |       |       |       |       |       | if    |
   |       |       |       |       |       |       |       |       | Code  |
   |       |       |       |       |       |       |       |       | Value |
   |       |       |       |       |       |       |       |       | (     |
   |       |       |       |       |       |       |       |       | 0008, |
   |       |       |       |       |       |       |       |       | 0100) |
   |       |       |       |       |       |       |       |       | is    |
   |       |       |       |       |       |       |       |       | not   |
   |       |       |       |       |       |       |       |       | pre   |
   |       |       |       |       |       |       |       |       | sent, |
   |       |       |       |       |       |       |       |       | and   |
   |       |       |       |       |       |       |       |       | the   |
   |       |       |       |       |       |       |       |       | code  |
   |       |       |       |       |       |       |       |       | value |
   |       |       |       |       |       |       |       |       | is    |
   |       |       |       |       |       |       |       |       | not a |
   |       |       |       |       |       |       |       |       | URN   |
   |       |       |       |       |       |       |       |       | or    |
   |       |       |       |       |       |       |       |       | URL.  |
   +-------+-------+-------+-------+-------+-------+-------+-------+-------+
   | URN   | (     | 1C/1C | 1C/1C |       | -/1C  | \*    | 1C    | Long  |
   | Code  | 0008, |       |       |       |       |       |       | Code  |
   | Value | 0120) |       |       |       |       |       |       | Value |
   |       |       |       |       |       |       |       |       | shall |
   |       |       |       |       |       |       |       |       | be    |
   |       |       |       |       |       |       |       |       | retr  |
   |       |       |       |       |       |       |       |       | ieved |
   |       |       |       |       |       |       |       |       | with  |
   |       |       |       |       |       |       |       |       | S     |
   |       |       |       |       |       |       |       |       | ingle |
   |       |       |       |       |       |       |       |       | Value |
   |       |       |       |       |       |       |       |       | Matc  |
   |       |       |       |       |       |       |       |       | hing. |
   |       |       |       |       |       |       |       |       |       |
   |       |       |       |       |       |       |       |       | Shall |
   |       |       |       |       |       |       |       |       | be    |
   |       |       |       |       |       |       |       |       | pr    |
   |       |       |       |       |       |       |       |       | esent |
   |       |       |       |       |       |       |       |       | if    |
   |       |       |       |       |       |       |       |       | Code  |
   |       |       |       |       |       |       |       |       | Value |
   |       |       |       |       |       |       |       |       | (     |
   |       |       |       |       |       |       |       |       | 0008, |
   |       |       |       |       |       |       |       |       | 0100) |
   |       |       |       |       |       |       |       |       | is    |
   |       |       |       |       |       |       |       |       | not   |
   |       |       |       |       |       |       |       |       | pre   |
   |       |       |       |       |       |       |       |       | sent, |
   |       |       |       |       |       |       |       |       | and   |
   |       |       |       |       |       |       |       |       | the   |
   |       |       |       |       |       |       |       |       | code  |
   |       |       |       |       |       |       |       |       | value |
   |       |       |       |       |       |       |       |       | is a  |
   |       |       |       |       |       |       |       |       | URN   |
   |       |       |       |       |       |       |       |       | or    |
   |       |       |       |       |       |       |       |       | URL.  |
   +-------+-------+-------+-------+-------+-------+-------+-------+-------+
   | Ma    | (     | 3/3   | 3/3   |       | -/3   | -     | 3     |       |
   | pping | 0008, |       |       |       |       |       |       |       |
   | Res   | 0105) |       |       |       |       |       |       |       |
   | ource |       |       |       |       |       |       |       |       |
   +-------+-------+-------+-------+-------+-------+-------+-------+-------+
   | Ma    | (     | 3/3   | 3/3   |       | -/3   | -     | 3     |       |
   | pping | 0008, |       |       |       |       |       |       |       |
   | Res   | 0118) |       |       |       |       |       |       |       |
   | ource |       |       |       |       |       |       |       |       |
   | UID   |       |       |       |       |       |       |       |       |
   +-------+-------+-------+-------+-------+-------+-------+-------+-------+
   | Co    | (     | 3/3   | 3/3   |       | -/3   | -     | 3     |       |
   | ntext | 0008, |       |       |       |       |       |       |       |
   | Group | 0106) |       |       |       |       |       |       |       |
   | Ve    |       |       |       |       |       |       |       |       |
   | rsion |       |       |       |       |       |       |       |       |
   +-------+-------+-------+-------+-------+-------+-------+-------+-------+
   | Co    | (     | 3/3   | 3/3   |       | -/3   | -     | 3     |       |
   | ntext | 0008, |       |       |       |       |       |       |       |
   | Group | 010B) |       |       |       |       |       |       |       |
   | Exte  |       |       |       |       |       |       |       |       |
   | nsion |       |       |       |       |       |       |       |       |
   | Flag  |       |       |       |       |       |       |       |       |
   +-------+-------+-------+-------+-------+-------+-------+-------+-------+
   | Co    | (     | 3/3   | 3/3   |       | -/3   | -     | 3     |       |
   | ntext | 0008, |       |       |       |       |       |       |       |
   | Group | 0107) |       |       |       |       |       |       |       |
   | Local |       |       |       |       |       |       |       |       |
   | Ve    |       |       |       |       |       |       |       |       |
   | rsion |       |       |       |       |       |       |       |       |
   +-------+-------+-------+-------+-------+-------+-------+-------+-------+
   | Co    | (     | 3/3   | 3/3   |       | -/3   | -     | 3     |       |
   | ntext | 0008, |       |       |       |       |       |       |       |
   | Group | 010D) |       |       |       |       |       |       |       |
   | Exte  |       |       |       |       |       |       |       |       |
   | nsion |       |       |       |       |       |       |       |       |
   | Cr    |       |       |       |       |       |       |       |       |
   | eator |       |       |       |       |       |       |       |       |
   | UID   |       |       |       |       |       |       |       |       |
   +-------+-------+-------+-------+-------+-------+-------+-------+-------+

.. table:: UPS Content Item Macro

   +-------+-------+-------+-------+-------+-------+-------+-------+-------+
   | Attr  | Tag   | Req.  | Req.  | Final | Req.  | Match | R     | Remar |
   | ibute |       | Type  | Type  | State | Type  | Key   | eturn | k/Mat |
   | Name  |       | N-C   | N-SET |       | N-GET | Type  | Key   | ching |
   |       |       | REATE | (SCU  |       | (SCU  |       | Type  | Type  |
   |       |       | (SCU  | /SCP) |       | /SCP) |       |       |       |
   |       |       | /SCP) |       |       |       |       |       |       |
   +=======+=======+=======+=======+=======+=======+=======+=======+=======+
   | Value | (     | 1/1   | 1/1   |       | -/1   | \*    | 1     | The   |
   | Type  | 0040, |       |       |       |       |       |       | type  |
   |       | A040) |       |       |       |       |       |       | of    |
   |       |       |       |       |       |       |       |       | the   |
   |       |       |       |       |       |       |       |       | value |
   |       |       |       |       |       |       |       |       | en    |
   |       |       |       |       |       |       |       |       | coded |
   |       |       |       |       |       |       |       |       | in    |
   |       |       |       |       |       |       |       |       | this  |
   |       |       |       |       |       |       |       |       | name- |
   |       |       |       |       |       |       |       |       | value |
   |       |       |       |       |       |       |       |       | Item. |
   |       |       |       |       |       |       |       |       |       |
   |       |       |       |       |       |       |       |       | DAT   |
   |       |       |       |       |       |       |       |       | ETIME |
   |       |       |       |       |       |       |       |       | DATE  |
   |       |       |       |       |       |       |       |       | TIME  |
   |       |       |       |       |       |       |       |       | PNAME |
   |       |       |       |       |       |       |       |       | U     |
   |       |       |       |       |       |       |       |       | IDREF |
   |       |       |       |       |       |       |       |       | TEXT  |
   |       |       |       |       |       |       |       |       | CODE  |
   |       |       |       |       |       |       |       |       | NU    |
   |       |       |       |       |       |       |       |       | MERIC |
   +-------+-------+-------+-------+-------+-------+-------+-------+-------+
   | Co    | (     | 1/1   | 1/1   |       | -/1   | \*    | 1     | Coded |
   | ncept | 0040, |       |       |       |       |       |       | co    |
   | Name  | A043) |       |       |       |       |       |       | ncept |
   | Code  |       |       |       |       |       |       |       | name  |
   | Seq   |       |       |       |       |       |       |       | of    |
   | uence |       |       |       |       |       |       |       | this  |
   |       |       |       |       |       |       |       |       | name- |
   |       |       |       |       |       |       |       |       | value |
   |       |       |       |       |       |       |       |       | Item. |
   +-------+-------+-------+-------+-------+-------+-------+-------+-------+
   | *     | *No   |       |       |       |       |       |       |       |
   | >Incl | Bas   |       |       |       |       |       |       |       |
   | ude*\ | eline |       |       |       |       |       |       |       |
   |  `tab | CID   |       |       |       |       |       |       |       |
   | le_ti | is    |       |       |       |       |       |       |       |
   | tle < | defi  |       |       |       |       |       |       |       |
   | #tabl | ned.* |       |       |       |       |       |       |       |
   | e_CC. |       |       |       |       |       |       |       |       |
   | 2.5-2 |       |       |       |       |       |       |       |       |
   | a>`__ |       |       |       |       |       |       |       |       |
   +-------+-------+-------+-------+-------+-------+-------+-------+-------+
   | Dat   | (     | 1C/1C | 1/1   |       | -/1   | \*    | 1C    | Dat   |
   | eTime | 0040, |       |       |       |       |       |       | etime |
   |       | A120) |       |       |       |       |       |       | value |
   |       |       |       |       |       |       |       |       | for   |
   |       |       |       |       |       |       |       |       | this  |
   |       |       |       |       |       |       |       |       | name- |
   |       |       |       |       |       |       |       |       | value |
   |       |       |       |       |       |       |       |       | Item. |
   |       |       |       |       |       |       |       |       |       |
   |       |       |       |       |       |       |       |       | Req   |
   |       |       |       |       |       |       |       |       | uired |
   |       |       |       |       |       |       |       |       | if    |
   |       |       |       |       |       |       |       |       | Value |
   |       |       |       |       |       |       |       |       | Type  |
   |       |       |       |       |       |       |       |       | (     |
   |       |       |       |       |       |       |       |       | 0040, |
   |       |       |       |       |       |       |       |       | A040) |
   |       |       |       |       |       |       |       |       | is    |
   |       |       |       |       |       |       |       |       | DATE  |
   |       |       |       |       |       |       |       |       | TIME. |
   +-------+-------+-------+-------+-------+-------+-------+-------+-------+
   | Date  | (     | 1C/1C | 1/1   |       | -/1   | \*    | 1C    | Date  |
   |       | 0040, |       |       |       |       |       |       | value |
   |       | A121) |       |       |       |       |       |       | for   |
   |       |       |       |       |       |       |       |       | this  |
   |       |       |       |       |       |       |       |       | name- |
   |       |       |       |       |       |       |       |       | value |
   |       |       |       |       |       |       |       |       | Item. |
   |       |       |       |       |       |       |       |       |       |
   |       |       |       |       |       |       |       |       | Req   |
   |       |       |       |       |       |       |       |       | uired |
   |       |       |       |       |       |       |       |       | if    |
   |       |       |       |       |       |       |       |       | Value |
   |       |       |       |       |       |       |       |       | Type  |
   |       |       |       |       |       |       |       |       | (     |
   |       |       |       |       |       |       |       |       | 0040, |
   |       |       |       |       |       |       |       |       | A040) |
   |       |       |       |       |       |       |       |       | is    |
   |       |       |       |       |       |       |       |       | DATE. |
   +-------+-------+-------+-------+-------+-------+-------+-------+-------+
   | Time  | (     | 1C/1C | 1/1   |       | -/1   | \*    | 1C    | Time  |
   |       | 0040, |       |       |       |       |       |       | value |
   |       | A122) |       |       |       |       |       |       | for   |
   |       |       |       |       |       |       |       |       | this  |
   |       |       |       |       |       |       |       |       | name- |
   |       |       |       |       |       |       |       |       | value |
   |       |       |       |       |       |       |       |       | Item. |
   |       |       |       |       |       |       |       |       |       |
   |       |       |       |       |       |       |       |       | Req   |
   |       |       |       |       |       |       |       |       | uired |
   |       |       |       |       |       |       |       |       | if    |
   |       |       |       |       |       |       |       |       | Value |
   |       |       |       |       |       |       |       |       | Type  |
   |       |       |       |       |       |       |       |       | (     |
   |       |       |       |       |       |       |       |       | 0040, |
   |       |       |       |       |       |       |       |       | A040) |
   |       |       |       |       |       |       |       |       | is    |
   |       |       |       |       |       |       |       |       | TIME. |
   +-------+-------+-------+-------+-------+-------+-------+-------+-------+
   | P     | (     | 1C/1C | 1/1   |       | -/1   | \*    | 1C    | P     |
   | erson | 0040, |       |       |       |       |       |       | erson |
   | Name  | A123) |       |       |       |       |       |       | name  |
   |       |       |       |       |       |       |       |       | value |
   |       |       |       |       |       |       |       |       | for   |
   |       |       |       |       |       |       |       |       | this  |
   |       |       |       |       |       |       |       |       | name- |
   |       |       |       |       |       |       |       |       | value |
   |       |       |       |       |       |       |       |       | Item. |
   |       |       |       |       |       |       |       |       |       |
   |       |       |       |       |       |       |       |       | Req   |
   |       |       |       |       |       |       |       |       | uired |
   |       |       |       |       |       |       |       |       | if    |
   |       |       |       |       |       |       |       |       | Value |
   |       |       |       |       |       |       |       |       | Type  |
   |       |       |       |       |       |       |       |       | (     |
   |       |       |       |       |       |       |       |       | 0040, |
   |       |       |       |       |       |       |       |       | A040) |
   |       |       |       |       |       |       |       |       | is    |
   |       |       |       |       |       |       |       |       | P     |
   |       |       |       |       |       |       |       |       | NAME. |
   +-------+-------+-------+-------+-------+-------+-------+-------+-------+
   | UID   | (     | 1C/1C | 1/1   |       | -/1   | \*    | 1C    | UID   |
   |       | 0040, |       |       |       |       |       |       | value |
   |       | A124) |       |       |       |       |       |       | for   |
   |       |       |       |       |       |       |       |       | this  |
   |       |       |       |       |       |       |       |       | name- |
   |       |       |       |       |       |       |       |       | value |
   |       |       |       |       |       |       |       |       | Item. |
   |       |       |       |       |       |       |       |       |       |
   |       |       |       |       |       |       |       |       | Req   |
   |       |       |       |       |       |       |       |       | uired |
   |       |       |       |       |       |       |       |       | if    |
   |       |       |       |       |       |       |       |       | Value |
   |       |       |       |       |       |       |       |       | Type  |
   |       |       |       |       |       |       |       |       | (     |
   |       |       |       |       |       |       |       |       | 0040, |
   |       |       |       |       |       |       |       |       | A040) |
   |       |       |       |       |       |       |       |       | is    |
   |       |       |       |       |       |       |       |       | UI    |
   |       |       |       |       |       |       |       |       | DREF. |
   +-------+-------+-------+-------+-------+-------+-------+-------+-------+
   | Text  | (     | 1C/1C | 1/1   |       | -/1   | \*    | 1C    | Text  |
   | Value | 0040, |       |       |       |       |       |       | value |
   |       | A160) |       |       |       |       |       |       | for   |
   |       |       |       |       |       |       |       |       | this  |
   |       |       |       |       |       |       |       |       | name- |
   |       |       |       |       |       |       |       |       | value |
   |       |       |       |       |       |       |       |       | Item. |
   |       |       |       |       |       |       |       |       |       |
   |       |       |       |       |       |       |       |       | Req   |
   |       |       |       |       |       |       |       |       | uired |
   |       |       |       |       |       |       |       |       | if    |
   |       |       |       |       |       |       |       |       | Value |
   |       |       |       |       |       |       |       |       | Type  |
   |       |       |       |       |       |       |       |       | (     |
   |       |       |       |       |       |       |       |       | 0040, |
   |       |       |       |       |       |       |       |       | A040) |
   |       |       |       |       |       |       |       |       | is    |
   |       |       |       |       |       |       |       |       | TEXT. |
   +-------+-------+-------+-------+-------+-------+-------+-------+-------+
   | Co    | (     | 1C/1C | 1/1   |       | -/1   | \*    | 1C    | Coded |
   | ncept | 0040, |       |       |       |       |       |       | co    |
   | Code  | A168) |       |       |       |       |       |       | ncept |
   | Seq   |       |       |       |       |       |       |       | value |
   | uence |       |       |       |       |       |       |       | of    |
   |       |       |       |       |       |       |       |       | this  |
   |       |       |       |       |       |       |       |       | name- |
   |       |       |       |       |       |       |       |       | value |
   |       |       |       |       |       |       |       |       | Item. |
   |       |       |       |       |       |       |       |       |       |
   |       |       |       |       |       |       |       |       | Req   |
   |       |       |       |       |       |       |       |       | uired |
   |       |       |       |       |       |       |       |       | if    |
   |       |       |       |       |       |       |       |       | Value |
   |       |       |       |       |       |       |       |       | Type  |
   |       |       |       |       |       |       |       |       | (     |
   |       |       |       |       |       |       |       |       | 0040, |
   |       |       |       |       |       |       |       |       | A040) |
   |       |       |       |       |       |       |       |       | is    |
   |       |       |       |       |       |       |       |       | CODE. |
   +-------+-------+-------+-------+-------+-------+-------+-------+-------+
   | *     | *No   |       |       |       |       |       |       |       |
   | >Incl | Bas   |       |       |       |       |       |       |       |
   | ude*\ | eline |       |       |       |       |       |       |       |
   |  `tab | CID   |       |       |       |       |       |       |       |
   | le_ti | is    |       |       |       |       |       |       |       |
   | tle < | defi  |       |       |       |       |       |       |       |
   | #tabl | ned.* |       |       |       |       |       |       |       |
   | e_CC. |       |       |       |       |       |       |       |       |
   | 2.5-2 |       |       |       |       |       |       |       |       |
   | a>`__ |       |       |       |       |       |       |       |       |
   +-------+-------+-------+-------+-------+-------+-------+-------+-------+
   | Nu    | (     | 1C/1C | 1/1   |       | -/1   | \*    | 1C    | Nu    |
   | meric | 0040, |       |       |       |       |       |       | meric |
   | Value | A30A) |       |       |       |       |       |       | value |
   |       |       |       |       |       |       |       |       | for   |
   |       |       |       |       |       |       |       |       | this  |
   |       |       |       |       |       |       |       |       | name- |
   |       |       |       |       |       |       |       |       | value |
   |       |       |       |       |       |       |       |       | Item. |
   |       |       |       |       |       |       |       |       |       |
   |       |       |       |       |       |       |       |       | Req   |
   |       |       |       |       |       |       |       |       | uired |
   |       |       |       |       |       |       |       |       | if    |
   |       |       |       |       |       |       |       |       | Value |
   |       |       |       |       |       |       |       |       | Type  |
   |       |       |       |       |       |       |       |       | (     |
   |       |       |       |       |       |       |       |       | 0040, |
   |       |       |       |       |       |       |       |       | A040) |
   |       |       |       |       |       |       |       |       | is    |
   |       |       |       |       |       |       |       |       | NUM   |
   |       |       |       |       |       |       |       |       | ERIC. |
   +-------+-------+-------+-------+-------+-------+-------+-------+-------+
   | M     | (     | 1C/1C | 1/1   |       | -/1   | \*    | 1C    | Units |
   | easur | 0040, |       |       |       |       |       |       | of    |
   | ement | 08EA) |       |       |       |       |       |       | m     |
   | Units |       |       |       |       |       |       |       | easur |
   | Code  |       |       |       |       |       |       |       | ement |
   | Seq   |       |       |       |       |       |       |       | for a |
   | uence |       |       |       |       |       |       |       | nu    |
   |       |       |       |       |       |       |       |       | meric |
   |       |       |       |       |       |       |       |       | value |
   |       |       |       |       |       |       |       |       | in    |
   |       |       |       |       |       |       |       |       | this  |
   |       |       |       |       |       |       |       |       | name- |
   |       |       |       |       |       |       |       |       | value |
   |       |       |       |       |       |       |       |       | Item. |
   |       |       |       |       |       |       |       |       |       |
   |       |       |       |       |       |       |       |       | Req   |
   |       |       |       |       |       |       |       |       | uired |
   |       |       |       |       |       |       |       |       | if    |
   |       |       |       |       |       |       |       |       | Value |
   |       |       |       |       |       |       |       |       | Type  |
   |       |       |       |       |       |       |       |       | (     |
   |       |       |       |       |       |       |       |       | 0040, |
   |       |       |       |       |       |       |       |       | A040) |
   |       |       |       |       |       |       |       |       | is    |
   |       |       |       |       |       |       |       |       | NUM   |
   |       |       |       |       |       |       |       |       | ERIC. |
   +-------+-------+-------+-------+-------+-------+-------+-------+-------+
   | *     | *Base |       |       |       |       |       |       |       |
   | >Incl | line* |       |       |       |       |       |       |       |
   | ude*\ |       |       |       |       |       |       |       |       |
   |  `tab |       |       |       |       |       |       |       |       |
   | le_ti |       |       |       |       |       |       |       |       |
   | tle < |       |       |       |       |       |       |       |       |
   | #tabl |       |       |       |       |       |       |       |       |
   | e_CC. |       |       |       |       |       |       |       |       |
   | 2.5-2 |       |       |       |       |       |       |       |       |
   | a>`__ |       |       |       |       |       |       |       |       |
   +-------+-------+-------+-------+-------+-------+-------+-------+-------+

.. table:: Referenced Instances and Access Macro

   +-------+-------+-------+-------+-------+-------+-------+-------+-------+
   | Attr  | Tag   | Req.  | Req.  | Final | Req.  | Match | R     | Remar |
   | ibute |       | Type  | Type  | State | Type  | Key   | eturn | k/Mat |
   | Name  |       | N-C   | N-SET |       | N-GET | Type  | Key   | ching |
   |       |       | REATE | (SCU  |       | (SCU  |       | Type  | Type  |
   |       |       | (SCU  | /SCP) |       | /SCP) |       |       |       |
   |       |       | /SCP) |       |       |       |       |       |       |
   +=======+=======+=======+=======+=======+=======+=======+=======+=======+
   | Type  | (     | 1/1   | 1/1   |       | -/1   | O     | 1     |       |
   | of    | 0040, |       |       |       |       |       |       |       |
   | Inst  | E020) |       |       |       |       |       |       |       |
   | ances |       |       |       |       |       |       |       |       |
   +-------+-------+-------+-------+-------+-------+-------+-------+-------+
   | Study | (     | 1C/1  | 1C/1  |       | -/1   | O     | 1C    | Req   |
   | Ins   | 0020, |       |       |       |       |       |       | uired |
   | tance | 000D) |       |       |       |       |       |       | if    |
   | UID   |       |       |       |       |       |       |       | Type  |
   |       |       |       |       |       |       |       |       | of    |
   |       |       |       |       |       |       |       |       | Inst  |
   |       |       |       |       |       |       |       |       | ances |
   |       |       |       |       |       |       |       |       | (     |
   |       |       |       |       |       |       |       |       | 0040, |
   |       |       |       |       |       |       |       |       | E020) |
   |       |       |       |       |       |       |       |       | is    |
   |       |       |       |       |       |       |       |       | DICOM |
   |       |       |       |       |       |       |       |       | and   |
   |       |       |       |       |       |       |       |       | the   |
   |       |       |       |       |       |       |       |       | I     |
   |       |       |       |       |       |       |       |       | nform |
   |       |       |       |       |       |       |       |       | ation |
   |       |       |       |       |       |       |       |       | Model |
   |       |       |       |       |       |       |       |       | of    |
   |       |       |       |       |       |       |       |       | the   |
   |       |       |       |       |       |       |       |       | refer |
   |       |       |       |       |       |       |       |       | enced |
   |       |       |       |       |       |       |       |       | ins   |
   |       |       |       |       |       |       |       |       | tance |
   |       |       |       |       |       |       |       |       | con   |
   |       |       |       |       |       |       |       |       | tains |
   |       |       |       |       |       |       |       |       | the   |
   |       |       |       |       |       |       |       |       | Study |
   |       |       |       |       |       |       |       |       | IE    |
   +-------+-------+-------+-------+-------+-------+-------+-------+-------+
   | S     | (     | 1C/1  | 1C/1  |       | -/1   | O     | 1C    | Req   |
   | eries | 0020, |       |       |       |       |       |       | uired |
   | Ins   | 000E) |       |       |       |       |       |       | if    |
   | tance |       |       |       |       |       |       |       | Type  |
   | UID   |       |       |       |       |       |       |       | of    |
   |       |       |       |       |       |       |       |       | Inst  |
   |       |       |       |       |       |       |       |       | ances |
   |       |       |       |       |       |       |       |       | (     |
   |       |       |       |       |       |       |       |       | 0040, |
   |       |       |       |       |       |       |       |       | E020) |
   |       |       |       |       |       |       |       |       | is    |
   |       |       |       |       |       |       |       |       | DICOM |
   |       |       |       |       |       |       |       |       | and   |
   |       |       |       |       |       |       |       |       | the   |
   |       |       |       |       |       |       |       |       | I     |
   |       |       |       |       |       |       |       |       | nform |
   |       |       |       |       |       |       |       |       | ation |
   |       |       |       |       |       |       |       |       | Model |
   |       |       |       |       |       |       |       |       | of    |
   |       |       |       |       |       |       |       |       | the   |
   |       |       |       |       |       |       |       |       | refer |
   |       |       |       |       |       |       |       |       | enced |
   |       |       |       |       |       |       |       |       | ins   |
   |       |       |       |       |       |       |       |       | tance |
   |       |       |       |       |       |       |       |       | con   |
   |       |       |       |       |       |       |       |       | tains |
   |       |       |       |       |       |       |       |       | the   |
   |       |       |       |       |       |       |       |       | S     |
   |       |       |       |       |       |       |       |       | eries |
   |       |       |       |       |       |       |       |       | IE    |
   +-------+-------+-------+-------+-------+-------+-------+-------+-------+
   | Refer | (     | 1/1   | 1/1   |       | -/1   | O     | 1     |       |
   | enced | 0008, |       |       |       |       |       |       |       |
   | SOP   | 1199) |       |       |       |       |       |       |       |
   | Seq   |       |       |       |       |       |       |       |       |
   | uence |       |       |       |       |       |       |       |       |
   +-------+-------+-------+-------+-------+-------+-------+-------+-------+
   | >     | (     | 1/1   | 1/1   |       | -/1   | O     | 1     |       |
   | Refer | 0008, |       |       |       |       |       |       |       |
   | enced | 1150) |       |       |       |       |       |       |       |
   | SOP   |       |       |       |       |       |       |       |       |
   | Class |       |       |       |       |       |       |       |       |
   | UID   |       |       |       |       |       |       |       |       |
   +-------+-------+-------+-------+-------+-------+-------+-------+-------+
   | >     | (     | 1/1   | 1/1   |       | -/1   | O     | 1     |       |
   | Refer | 0008, |       |       |       |       |       |       |       |
   | enced | 1155) |       |       |       |       |       |       |       |
   | SOP   |       |       |       |       |       |       |       |       |
   | Ins   |       |       |       |       |       |       |       |       |
   | tance |       |       |       |       |       |       |       |       |
   | UID   |       |       |       |       |       |       |       |       |
   +-------+-------+-------+-------+-------+-------+-------+-------+-------+
   | >HL7  | (     | 1C/1  | 1C/1  |       | -/1   | O     | 1C    | Req   |
   | Ins   | 0040, |       |       |       |       |       |       | uired |
   | tance | E001) |       |       |       |       |       |       | if    |
   | Ident |       |       |       |       |       |       |       | Type  |
   | ifier |       |       |       |       |       |       |       | of    |
   |       |       |       |       |       |       |       |       | Inst  |
   |       |       |       |       |       |       |       |       | ances |
   |       |       |       |       |       |       |       |       | (     |
   |       |       |       |       |       |       |       |       | 0040, |
   |       |       |       |       |       |       |       |       | E020) |
   |       |       |       |       |       |       |       |       | is    |
   |       |       |       |       |       |       |       |       | CDA.  |
   +-------+-------+-------+-------+-------+-------+-------+-------+-------+
   | >     | (     | 1C/1  | 1C/1  |       | -/2   | O     | 1C    | Req   |
   | Refer | 0008, |       |       |       |       |       |       | uired |
   | enced | 1160) |       |       |       |       |       |       | if    |
   | Frame |       |       |       |       |       |       |       | the   |
   | N     |       |       |       |       |       |       |       | Refer |
   | umber |       |       |       |       |       |       |       | enced |
   |       |       |       |       |       |       |       |       | SOP   |
   |       |       |       |       |       |       |       |       | Ins   |
   |       |       |       |       |       |       |       |       | tance |
   |       |       |       |       |       |       |       |       | is a  |
   |       |       |       |       |       |       |       |       | m     |
   |       |       |       |       |       |       |       |       | ulti- |
   |       |       |       |       |       |       |       |       | frame |
   |       |       |       |       |       |       |       |       | image |
   |       |       |       |       |       |       |       |       | and   |
   |       |       |       |       |       |       |       |       | the   |
   |       |       |       |       |       |       |       |       | refe  |
   |       |       |       |       |       |       |       |       | rence |
   |       |       |       |       |       |       |       |       | does  |
   |       |       |       |       |       |       |       |       | not   |
   |       |       |       |       |       |       |       |       | apply |
   |       |       |       |       |       |       |       |       | to    |
   |       |       |       |       |       |       |       |       | all   |
   |       |       |       |       |       |       |       |       | fr    |
   |       |       |       |       |       |       |       |       | ames, |
   |       |       |       |       |       |       |       |       | and   |
   |       |       |       |       |       |       |       |       | Refer |
   |       |       |       |       |       |       |       |       | enced |
   |       |       |       |       |       |       |       |       | Se    |
   |       |       |       |       |       |       |       |       | gment |
   |       |       |       |       |       |       |       |       | N     |
   |       |       |       |       |       |       |       |       | umber |
   |       |       |       |       |       |       |       |       | (     |
   |       |       |       |       |       |       |       |       | 0062, |
   |       |       |       |       |       |       |       |       | 000B) |
   |       |       |       |       |       |       |       |       | is    |
   |       |       |       |       |       |       |       |       | not   |
   |       |       |       |       |       |       |       |       | pre   |
   |       |       |       |       |       |       |       |       | sent. |
   +-------+-------+-------+-------+-------+-------+-------+-------+-------+
   | >     | (     | 1C/1  | 1C/1  |       | -/2   | O     | 1C    | Req   |
   | Refer | 0062, |       |       |       |       |       |       | uired |
   | enced | 000B) |       |       |       |       |       |       | if    |
   | Se    |       |       |       |       |       |       |       | the   |
   | gment |       |       |       |       |       |       |       | Refer |
   | N     |       |       |       |       |       |       |       | enced |
   | umber |       |       |       |       |       |       |       | SOP   |
   |       |       |       |       |       |       |       |       | Ins   |
   |       |       |       |       |       |       |       |       | tance |
   |       |       |       |       |       |       |       |       | is a  |
   |       |       |       |       |       |       |       |       | Se    |
   |       |       |       |       |       |       |       |       | gment |
   |       |       |       |       |       |       |       |       | ation |
   |       |       |       |       |       |       |       |       | and   |
   |       |       |       |       |       |       |       |       | the   |
   |       |       |       |       |       |       |       |       | refe  |
   |       |       |       |       |       |       |       |       | rence |
   |       |       |       |       |       |       |       |       | does  |
   |       |       |       |       |       |       |       |       | not   |
   |       |       |       |       |       |       |       |       | apply |
   |       |       |       |       |       |       |       |       | to    |
   |       |       |       |       |       |       |       |       | all   |
   |       |       |       |       |       |       |       |       | seg   |
   |       |       |       |       |       |       |       |       | ments |
   |       |       |       |       |       |       |       |       | and   |
   |       |       |       |       |       |       |       |       | Refer |
   |       |       |       |       |       |       |       |       | enced |
   |       |       |       |       |       |       |       |       | Frame |
   |       |       |       |       |       |       |       |       | N     |
   |       |       |       |       |       |       |       |       | umber |
   |       |       |       |       |       |       |       |       | (     |
   |       |       |       |       |       |       |       |       | 0008, |
   |       |       |       |       |       |       |       |       | 1160) |
   |       |       |       |       |       |       |       |       | is    |
   |       |       |       |       |       |       |       |       | not   |
   |       |       |       |       |       |       |       |       | pre   |
   |       |       |       |       |       |       |       |       | sent. |
   +-------+-------+-------+-------+-------+-------+-------+-------+-------+
   | DICOM | (     | 1C/1  | 1C/1  |       | -/1   | O     | 1C    | Req   |
   | Retr  | 0040, |       |       |       |       |       |       | uired |
   | ieval | E021) |       |       |       |       |       |       | if    |
   | Seq   |       |       |       |       |       |       |       | DICOM |
   | uence |       |       |       |       |       |       |       | Media |
   |       |       |       |       |       |       |       |       | Retr  |
   |       |       |       |       |       |       |       |       | ieval |
   |       |       |       |       |       |       |       |       | Seq   |
   |       |       |       |       |       |       |       |       | uence |
   |       |       |       |       |       |       |       |       | (0    |
   |       |       |       |       |       |       |       |       | 040,E |
   |       |       |       |       |       |       |       |       | 022), |
   |       |       |       |       |       |       |       |       | WADO  |
   |       |       |       |       |       |       |       |       | Retr  |
   |       |       |       |       |       |       |       |       | ieval |
   |       |       |       |       |       |       |       |       | Seq   |
   |       |       |       |       |       |       |       |       | uence |
   |       |       |       |       |       |       |       |       | (0    |
   |       |       |       |       |       |       |       |       | 040,E |
   |       |       |       |       |       |       |       |       | 023), |
   |       |       |       |       |       |       |       |       | WA    |
   |       |       |       |       |       |       |       |       | DO-RS |
   |       |       |       |       |       |       |       |       | Retr  |
   |       |       |       |       |       |       |       |       | ieval |
   |       |       |       |       |       |       |       |       | Seq   |
   |       |       |       |       |       |       |       |       | uence |
   |       |       |       |       |       |       |       |       | (     |
   |       |       |       |       |       |       |       |       | 0040, |
   |       |       |       |       |       |       |       |       | E025) |
   |       |       |       |       |       |       |       |       | and   |
   |       |       |       |       |       |       |       |       | XDS   |
   |       |       |       |       |       |       |       |       | Retr  |
   |       |       |       |       |       |       |       |       | ieval |
   |       |       |       |       |       |       |       |       | Seq   |
   |       |       |       |       |       |       |       |       | uence |
   |       |       |       |       |       |       |       |       | (     |
   |       |       |       |       |       |       |       |       | 0040, |
   |       |       |       |       |       |       |       |       | E024) |
   |       |       |       |       |       |       |       |       | are   |
   |       |       |       |       |       |       |       |       | not   |
   |       |       |       |       |       |       |       |       | pre   |
   |       |       |       |       |       |       |       |       | sent. |
   |       |       |       |       |       |       |       |       | May   |
   |       |       |       |       |       |       |       |       | be    |
   |       |       |       |       |       |       |       |       | pr    |
   |       |       |       |       |       |       |       |       | esent |
   |       |       |       |       |       |       |       |       | other |
   |       |       |       |       |       |       |       |       | wise. |
   +-------+-------+-------+-------+-------+-------+-------+-------+-------+
   | >Ret  | (     | 1/1   | 1/1   |       | -/1   | O     | 1     |       |
   | rieve | 0008, |       |       |       |       |       |       |       |
   | AE    | 0054) |       |       |       |       |       |       |       |
   | Title |       |       |       |       |       |       |       |       |
   +-------+-------+-------+-------+-------+-------+-------+-------+-------+
   | DICOM | (     | 1C/1  | 1C/1  |       | -/1   | O     | 1C    | Req   |
   | Media | 0040, |       |       |       |       |       |       | uired |
   | Retr  | E022) |       |       |       |       |       |       | if    |
   | ieval |       |       |       |       |       |       |       | DICOM |
   | Seq   |       |       |       |       |       |       |       | Retr  |
   | uence |       |       |       |       |       |       |       | ieval |
   |       |       |       |       |       |       |       |       | Seq   |
   |       |       |       |       |       |       |       |       | uence |
   |       |       |       |       |       |       |       |       | (0    |
   |       |       |       |       |       |       |       |       | 040,E |
   |       |       |       |       |       |       |       |       | 021), |
   |       |       |       |       |       |       |       |       | WADO  |
   |       |       |       |       |       |       |       |       | Retr  |
   |       |       |       |       |       |       |       |       | ieval |
   |       |       |       |       |       |       |       |       | Seq   |
   |       |       |       |       |       |       |       |       | uence |
   |       |       |       |       |       |       |       |       | (0    |
   |       |       |       |       |       |       |       |       | 040,E |
   |       |       |       |       |       |       |       |       | 023), |
   |       |       |       |       |       |       |       |       | WA    |
   |       |       |       |       |       |       |       |       | DO-RS |
   |       |       |       |       |       |       |       |       | Retr  |
   |       |       |       |       |       |       |       |       | ieval |
   |       |       |       |       |       |       |       |       | Seq   |
   |       |       |       |       |       |       |       |       | uence |
   |       |       |       |       |       |       |       |       | (     |
   |       |       |       |       |       |       |       |       | 0040, |
   |       |       |       |       |       |       |       |       | E025) |
   |       |       |       |       |       |       |       |       | and   |
   |       |       |       |       |       |       |       |       | XDS   |
   |       |       |       |       |       |       |       |       | Retr  |
   |       |       |       |       |       |       |       |       | ieval |
   |       |       |       |       |       |       |       |       | Seq   |
   |       |       |       |       |       |       |       |       | uence |
   |       |       |       |       |       |       |       |       | (     |
   |       |       |       |       |       |       |       |       | 0040, |
   |       |       |       |       |       |       |       |       | E024) |
   |       |       |       |       |       |       |       |       | are   |
   |       |       |       |       |       |       |       |       | not   |
   |       |       |       |       |       |       |       |       | pre   |
   |       |       |       |       |       |       |       |       | sent. |
   |       |       |       |       |       |       |       |       | May   |
   |       |       |       |       |       |       |       |       | be    |
   |       |       |       |       |       |       |       |       | pr    |
   |       |       |       |       |       |       |       |       | esent |
   |       |       |       |       |       |       |       |       | other |
   |       |       |       |       |       |       |       |       | wise. |
   +-------+-------+-------+-------+-------+-------+-------+-------+-------+
   | >St   | (     | 2/2   | 2/2   |       | -/2   | O     | 2     |       |
   | orage | 0088, |       |       |       |       |       |       |       |
   | Media | 0130) |       |       |       |       |       |       |       |
   | Fil   |       |       |       |       |       |       |       |       |
   | e-Set |       |       |       |       |       |       |       |       |
   | ID    |       |       |       |       |       |       |       |       |
   +-------+-------+-------+-------+-------+-------+-------+-------+-------+
   | >St   | (     | 1/1   | 1/1   |       | -/1   | O     | 1     |       |
   | orage | 0088, |       |       |       |       |       |       |       |
   | Media | 0140) |       |       |       |       |       |       |       |
   | Fil   |       |       |       |       |       |       |       |       |
   | e-Set |       |       |       |       |       |       |       |       |
   | UID   |       |       |       |       |       |       |       |       |
   +-------+-------+-------+-------+-------+-------+-------+-------+-------+
   | WADO  | (     | 1C/1  | 1C/1  |       | -/1   | O     | 1C    | Req   |
   | Retr  | 0040, |       |       |       |       |       |       | uired |
   | ieval | E023) |       |       |       |       |       |       | if    |
   | Seq   |       |       |       |       |       |       |       | DICOM |
   | uence |       |       |       |       |       |       |       | Retr  |
   |       |       |       |       |       |       |       |       | ieval |
   |       |       |       |       |       |       |       |       | Seq   |
   |       |       |       |       |       |       |       |       | uence |
   |       |       |       |       |       |       |       |       | (0    |
   |       |       |       |       |       |       |       |       | 040,E |
   |       |       |       |       |       |       |       |       | 021), |
   |       |       |       |       |       |       |       |       | DICOM |
   |       |       |       |       |       |       |       |       | Media |
   |       |       |       |       |       |       |       |       | Retr  |
   |       |       |       |       |       |       |       |       | ieval |
   |       |       |       |       |       |       |       |       | Seq   |
   |       |       |       |       |       |       |       |       | uence |
   |       |       |       |       |       |       |       |       | (0    |
   |       |       |       |       |       |       |       |       | 040,E |
   |       |       |       |       |       |       |       |       | 022), |
   |       |       |       |       |       |       |       |       | WA    |
   |       |       |       |       |       |       |       |       | DO-RS |
   |       |       |       |       |       |       |       |       | Retr  |
   |       |       |       |       |       |       |       |       | ieval |
   |       |       |       |       |       |       |       |       | Seq   |
   |       |       |       |       |       |       |       |       | uence |
   |       |       |       |       |       |       |       |       | (     |
   |       |       |       |       |       |       |       |       | 0040, |
   |       |       |       |       |       |       |       |       | E025) |
   |       |       |       |       |       |       |       |       | and   |
   |       |       |       |       |       |       |       |       | XDS   |
   |       |       |       |       |       |       |       |       | Retr  |
   |       |       |       |       |       |       |       |       | ieval |
   |       |       |       |       |       |       |       |       | Seq   |
   |       |       |       |       |       |       |       |       | uence |
   |       |       |       |       |       |       |       |       | (     |
   |       |       |       |       |       |       |       |       | 0040, |
   |       |       |       |       |       |       |       |       | E024) |
   |       |       |       |       |       |       |       |       | are   |
   |       |       |       |       |       |       |       |       | not   |
   |       |       |       |       |       |       |       |       | pre   |
   |       |       |       |       |       |       |       |       | sent. |
   |       |       |       |       |       |       |       |       | May   |
   |       |       |       |       |       |       |       |       | be    |
   |       |       |       |       |       |       |       |       | pr    |
   |       |       |       |       |       |       |       |       | esent |
   |       |       |       |       |       |       |       |       | other |
   |       |       |       |       |       |       |       |       | wise. |
   +-------+-------+-------+-------+-------+-------+-------+-------+-------+
   | >Ret  | (     | 1/1   | 1/1   |       | -/1   | O     | 1     |       |
   | rieve | 0040, |       |       |       |       |       |       |       |
   | URI   | E010) |       |       |       |       |       |       |       |
   +-------+-------+-------+-------+-------+-------+-------+-------+-------+
   | XDS   | (     | 1C    | 1C/1  |       | -/1   | O     | 1C    | Req   |
   | Retr  | 0040, |       |       |       |       |       |       | uired |
   | ieval | E024) |       |       |       |       |       |       | if    |
   | Seq   |       |       |       |       |       |       |       | DICOM |
   | uence |       |       |       |       |       |       |       | Retr  |
   |       |       |       |       |       |       |       |       | ieval |
   |       |       |       |       |       |       |       |       | Seq   |
   |       |       |       |       |       |       |       |       | uence |
   |       |       |       |       |       |       |       |       | (0    |
   |       |       |       |       |       |       |       |       | 040,E |
   |       |       |       |       |       |       |       |       | 021), |
   |       |       |       |       |       |       |       |       | DICOM |
   |       |       |       |       |       |       |       |       | Media |
   |       |       |       |       |       |       |       |       | Retr  |
   |       |       |       |       |       |       |       |       | ieval |
   |       |       |       |       |       |       |       |       | Seq   |
   |       |       |       |       |       |       |       |       | uence |
   |       |       |       |       |       |       |       |       | (0    |
   |       |       |       |       |       |       |       |       | 040,E |
   |       |       |       |       |       |       |       |       | 022), |
   |       |       |       |       |       |       |       |       | WA    |
   |       |       |       |       |       |       |       |       | DO-RS |
   |       |       |       |       |       |       |       |       | Retr  |
   |       |       |       |       |       |       |       |       | ieval |
   |       |       |       |       |       |       |       |       | Seq   |
   |       |       |       |       |       |       |       |       | uence |
   |       |       |       |       |       |       |       |       | (     |
   |       |       |       |       |       |       |       |       | 0040, |
   |       |       |       |       |       |       |       |       | E025) |
   |       |       |       |       |       |       |       |       | and   |
   |       |       |       |       |       |       |       |       | WADO  |
   |       |       |       |       |       |       |       |       | Retr  |
   |       |       |       |       |       |       |       |       | ieval |
   |       |       |       |       |       |       |       |       | Seq   |
   |       |       |       |       |       |       |       |       | uence |
   |       |       |       |       |       |       |       |       | (     |
   |       |       |       |       |       |       |       |       | 0040, |
   |       |       |       |       |       |       |       |       | E023) |
   |       |       |       |       |       |       |       |       | are   |
   |       |       |       |       |       |       |       |       | not   |
   |       |       |       |       |       |       |       |       | pre   |
   |       |       |       |       |       |       |       |       | sent. |
   |       |       |       |       |       |       |       |       | May   |
   |       |       |       |       |       |       |       |       | be    |
   |       |       |       |       |       |       |       |       | pr    |
   |       |       |       |       |       |       |       |       | esent |
   |       |       |       |       |       |       |       |       | other |
   |       |       |       |       |       |       |       |       | wise. |
   +-------+-------+-------+-------+-------+-------+-------+-------+-------+
   | >     | (     | 1/1   | 1/1   |       | -/1   | O     | 1     |       |
   | Repos | 0040, |       |       |       |       |       |       |       |
   | itory | E030) |       |       |       |       |       |       |       |
   | U     |       |       |       |       |       |       |       |       |
   | nique |       |       |       |       |       |       |       |       |
   | ID    |       |       |       |       |       |       |       |       |
   +-------+-------+-------+-------+-------+-------+-------+-------+-------+
   | >Home | (     | 3/2   | 3/2   |       | 3/2   | O     | 2     |       |
   | Comm  | 0040, |       |       |       |       |       |       |       |
   | unity | E031) |       |       |       |       |       |       |       |
   | ID    |       |       |       |       |       |       |       |       |
   +-------+-------+-------+-------+-------+-------+-------+-------+-------+
   | WA    | (     | 1C/1  | 1C/1  |       | -/1   | O     | 1C    | Req   |
   | DO-RS | 0040, |       |       |       |       |       |       | uired |
   | Retr  | E025) |       |       |       |       |       |       | if    |
   | ieval |       |       |       |       |       |       |       | DICOM |
   | Seq   |       |       |       |       |       |       |       | Retr  |
   | uence |       |       |       |       |       |       |       | ieval |
   |       |       |       |       |       |       |       |       | Seq   |
   |       |       |       |       |       |       |       |       | uence |
   |       |       |       |       |       |       |       |       | (0    |
   |       |       |       |       |       |       |       |       | 040,E |
   |       |       |       |       |       |       |       |       | 021), |
   |       |       |       |       |       |       |       |       | DICOM |
   |       |       |       |       |       |       |       |       | Media |
   |       |       |       |       |       |       |       |       | Retr  |
   |       |       |       |       |       |       |       |       | ieval |
   |       |       |       |       |       |       |       |       | Seq   |
   |       |       |       |       |       |       |       |       | uence |
   |       |       |       |       |       |       |       |       | (0    |
   |       |       |       |       |       |       |       |       | 040,E |
   |       |       |       |       |       |       |       |       | 022), |
   |       |       |       |       |       |       |       |       | WADO  |
   |       |       |       |       |       |       |       |       | Retr  |
   |       |       |       |       |       |       |       |       | ieval |
   |       |       |       |       |       |       |       |       | Seq   |
   |       |       |       |       |       |       |       |       | uence |
   |       |       |       |       |       |       |       |       | (0    |
   |       |       |       |       |       |       |       |       | 040,E |
   |       |       |       |       |       |       |       |       | 023), |
   |       |       |       |       |       |       |       |       | and   |
   |       |       |       |       |       |       |       |       | XDS   |
   |       |       |       |       |       |       |       |       | Retr  |
   |       |       |       |       |       |       |       |       | ieval |
   |       |       |       |       |       |       |       |       | Seq   |
   |       |       |       |       |       |       |       |       | uence |
   |       |       |       |       |       |       |       |       | (     |
   |       |       |       |       |       |       |       |       | 0040, |
   |       |       |       |       |       |       |       |       | E024) |
   |       |       |       |       |       |       |       |       | are   |
   |       |       |       |       |       |       |       |       | not   |
   |       |       |       |       |       |       |       |       | pre   |
   |       |       |       |       |       |       |       |       | sent. |
   |       |       |       |       |       |       |       |       | May   |
   |       |       |       |       |       |       |       |       | be    |
   |       |       |       |       |       |       |       |       | pr    |
   |       |       |       |       |       |       |       |       | esent |
   |       |       |       |       |       |       |       |       | other |
   |       |       |       |       |       |       |       |       | wise. |
   +-------+-------+-------+-------+-------+-------+-------+-------+-------+
   | >Ret  | (     | 1/1   | 1/1   |       | -/1   | O     | 1     | URL   |
   | rieve | 0008, |       |       |       |       |       |       | speci |
   | URL   | 1190) |       |       |       |       |       |       | fying |
   |       |       |       |       |       |       |       |       | the   |
   |       |       |       |       |       |       |       |       | loc   |
   |       |       |       |       |       |       |       |       | ation |
   |       |       |       |       |       |       |       |       | of    |
   |       |       |       |       |       |       |       |       | the   |
   |       |       |       |       |       |       |       |       | refer |
   |       |       |       |       |       |       |       |       | enced |
   |       |       |       |       |       |       |       |       | in    |
   |       |       |       |       |       |       |       |       | stanc |
   |       |       |       |       |       |       |       |       | e(s). |
   +-------+-------+-------+-------+-------+-------+-------+-------+-------+

.. table:: HL7V2 Hierarchic Designator Macro

   +-------+-------+-------+-------+-------+-------+-------+-------+-------+
   | Attr  | Tag   | Req.  | Req.  | Final | Req.  | Match | R     | Remar |
   | ibute |       | Type  | Type  | State | Type  | Key   | eturn | k/Mat |
   | Name  |       | N-C   | N-SET |       | N-GET | Type  | Key   | ching |
   |       |       | REATE | (SCU  |       | (SCU  |       | Type  | Type  |
   |       |       | (SCU  | /SCP) |       | /SCP) |       |       |       |
   |       |       | /SCP) |       |       |       |       |       |       |
   +=======+=======+=======+=======+=======+=======+=======+=======+=======+
   | Local | (     | 1C/1  | Not   |       | -/1   | \*    | 1C    | Cre   |
   | Name  | 0040, |       | Al    |       |       |       |       | ation |
   | space | 0031) |       | lowed |       |       |       |       | req   |
   | E     |       |       |       |       |       |       |       | uired |
   | ntity |       |       |       |       |       |       |       | if    |
   | ID    |       |       |       |       |       |       |       | Univ  |
   |       |       |       |       |       |       |       |       | ersal |
   |       |       |       |       |       |       |       |       | E     |
   |       |       |       |       |       |       |       |       | ntity |
   |       |       |       |       |       |       |       |       | ID    |
   |       |       |       |       |       |       |       |       | (     |
   |       |       |       |       |       |       |       |       | 0040, |
   |       |       |       |       |       |       |       |       | 0032) |
   |       |       |       |       |       |       |       |       | is    |
   |       |       |       |       |       |       |       |       | not   |
   |       |       |       |       |       |       |       |       | pre   |
   |       |       |       |       |       |       |       |       | sent; |
   |       |       |       |       |       |       |       |       | may   |
   |       |       |       |       |       |       |       |       | be    |
   |       |       |       |       |       |       |       |       | pr    |
   |       |       |       |       |       |       |       |       | esent |
   |       |       |       |       |       |       |       |       | other |
   |       |       |       |       |       |       |       |       | wise. |
   |       |       |       |       |       |       |       |       |       |
   |       |       |       |       |       |       |       |       | R     |
   |       |       |       |       |       |       |       |       | eturn |
   |       |       |       |       |       |       |       |       | Key   |
   |       |       |       |       |       |       |       |       | req   |
   |       |       |       |       |       |       |       |       | uired |
   |       |       |       |       |       |       |       |       | if    |
   |       |       |       |       |       |       |       |       | set.  |
   +-------+-------+-------+-------+-------+-------+-------+-------+-------+
   | Univ  | (     | 1C/1  | Not   |       | -/1   | \*    | 1C    | Cre   |
   | ersal | 0040, |       | Al    |       |       |       |       | ation |
   | E     | 0032) |       | lowed |       |       |       |       | req   |
   | ntity |       |       |       |       |       |       |       | uired |
   | ID    |       |       |       |       |       |       |       | if    |
   |       |       |       |       |       |       |       |       | Local |
   |       |       |       |       |       |       |       |       | Name  |
   |       |       |       |       |       |       |       |       | space |
   |       |       |       |       |       |       |       |       | E     |
   |       |       |       |       |       |       |       |       | ntity |
   |       |       |       |       |       |       |       |       | ID    |
   |       |       |       |       |       |       |       |       | (     |
   |       |       |       |       |       |       |       |       | 0040, |
   |       |       |       |       |       |       |       |       | 0031) |
   |       |       |       |       |       |       |       |       | is    |
   |       |       |       |       |       |       |       |       | not   |
   |       |       |       |       |       |       |       |       | pre   |
   |       |       |       |       |       |       |       |       | sent; |
   |       |       |       |       |       |       |       |       | may   |
   |       |       |       |       |       |       |       |       | be    |
   |       |       |       |       |       |       |       |       | pr    |
   |       |       |       |       |       |       |       |       | esent |
   |       |       |       |       |       |       |       |       | other |
   |       |       |       |       |       |       |       |       | wise. |
   |       |       |       |       |       |       |       |       |       |
   |       |       |       |       |       |       |       |       | R     |
   |       |       |       |       |       |       |       |       | eturn |
   |       |       |       |       |       |       |       |       | Key   |
   |       |       |       |       |       |       |       |       | req   |
   |       |       |       |       |       |       |       |       | uired |
   |       |       |       |       |       |       |       |       | if    |
   |       |       |       |       |       |       |       |       | set.  |
   +-------+-------+-------+-------+-------+-------+-------+-------+-------+
   | Univ  | (     | 1C/1  | Not   |       | -/1   | \*    | 1C    | Cre   |
   | ersal | 0040, |       | Al    |       |       |       |       | ation |
   | E     | 0033) |       | lowed |       |       |       |       | req   |
   | ntity |       |       |       |       |       |       |       | uired |
   | ID    |       |       |       |       |       |       |       | if    |
   | Type  |       |       |       |       |       |       |       | Univ  |
   |       |       |       |       |       |       |       |       | ersal |
   |       |       |       |       |       |       |       |       | E     |
   |       |       |       |       |       |       |       |       | ntity |
   |       |       |       |       |       |       |       |       | ID    |
   |       |       |       |       |       |       |       |       | (     |
   |       |       |       |       |       |       |       |       | 0040, |
   |       |       |       |       |       |       |       |       | 0032) |
   |       |       |       |       |       |       |       |       | is    |
   |       |       |       |       |       |       |       |       | pre   |
   |       |       |       |       |       |       |       |       | sent. |
   |       |       |       |       |       |       |       |       |       |
   |       |       |       |       |       |       |       |       | R     |
   |       |       |       |       |       |       |       |       | eturn |
   |       |       |       |       |       |       |       |       | Key   |
   |       |       |       |       |       |       |       |       | req   |
   |       |       |       |       |       |       |       |       | uired |
   |       |       |       |       |       |       |       |       | if    |
   |       |       |       |       |       |       |       |       | set.  |
   +-------+-------+-------+-------+-------+-------+-------+-------+-------+

.. table:: Issuer of Patient ID Macro

   +-------+-------+-------+-------+-------+-------+-------+-------+-------+
   | Attr  | Tag   | Req.  | Req.  | Final | Req.  | Match | R     | Remar |
   | ibute |       | Type  | Type  | State | Type  | Key   | eturn | k/Mat |
   | Name  |       | N-C   | N-SET |       | N-GET | Type  | Key   | ching |
   |       |       | REATE | (SCU  |       | (SCU  |       | Type  | Type  |
   |       |       | (SCU  | /SCP) |       | /SCP) |       |       |       |
   |       |       | /SCP) |       |       |       |       |       |       |
   +=======+=======+=======+=======+=======+=======+=======+=======+=======+
   | I     | (     | 2/2   | Not   | O     | 3/2   | R     | 2     |       |
   | ssuer | 0010, |       | al    |       |       |       |       |       |
   | of    | 0021) |       | lowed |       |       |       |       |       |
   | Pa    |       |       |       |       |       |       |       |       |
   | tient |       |       |       |       |       |       |       |       |
   | ID    |       |       |       |       |       |       |       |       |
   +-------+-------+-------+-------+-------+-------+-------+-------+-------+
   | I     | (     | 2/2   | Not   | O     | 3/2   | O     | 2     |       |
   | ssuer | 0010, |       | al    |       |       |       |       |       |
   | of    | 0024) |       | lowed |       |       |       |       |       |
   | Pa    |       |       |       |       |       |       |       |       |
   | tient |       |       |       |       |       |       |       |       |
   | ID    |       |       |       |       |       |       |       |       |
   | Quali |       |       |       |       |       |       |       |       |
   | fiers |       |       |       |       |       |       |       |       |
   | Seq   |       |       |       |       |       |       |       |       |
   | uence |       |       |       |       |       |       |       |       |
   +-------+-------+-------+-------+-------+-------+-------+-------+-------+
   | >Univ | (     | 2/2   | Not   | O     | 3/2   | O     | 2     |       |
   | ersal | 0040, |       | al    |       |       |       |       |       |
   | E     | 0032) |       | lowed |       |       |       |       |       |
   | ntity |       |       |       |       |       |       |       |       |
   | ID    |       |       |       |       |       |       |       |       |
   +-------+-------+-------+-------+-------+-------+-------+-------+-------+
   | >Univ | (     | 1C/1  | Not   | O     | 3/2   | O     | 1C    | Req   |
   | ersal | 0040, |       | al    |       |       |       |       | uired |
   | E     | 0033) |       | lowed |       |       |       |       | if    |
   | ntity |       |       |       |       |       |       |       | Univ  |
   | ID    |       |       |       |       |       |       |       | ersal |
   | Type  |       |       |       |       |       |       |       | E     |
   |       |       |       |       |       |       |       |       | ntity |
   |       |       |       |       |       |       |       |       | ID    |
   |       |       |       |       |       |       |       |       | (     |
   |       |       |       |       |       |       |       |       | 0040, |
   |       |       |       |       |       |       |       |       | 0032) |
   |       |       |       |       |       |       |       |       | is    |
   |       |       |       |       |       |       |       |       | pr    |
   |       |       |       |       |       |       |       |       | esent |
   |       |       |       |       |       |       |       |       | in    |
   |       |       |       |       |       |       |       |       | this  |
   |       |       |       |       |       |       |       |       | item  |
   |       |       |       |       |       |       |       |       | with  |
   |       |       |       |       |       |       |       |       | a     |
   |       |       |       |       |       |       |       |       | v     |
   |       |       |       |       |       |       |       |       | alue. |
   +-------+-------+-------+-------+-------+-------+-------+-------+-------+
   | >     | (     | 2/2   | Not   | O     | 3/2   | O     | 2     |       |
   | Ident | 0040, |       | al    |       |       |       |       |       |
   | ifier | 0035) |       | lowed |       |       |       |       |       |
   | Type  |       |       |       |       |       |       |       |       |
   | Code  |       |       |       |       |       |       |       |       |
   +-------+-------+-------+-------+-------+-------+-------+-------+-------+
   | >Assi | (     | 2/2   | Not   | O     | 3/2   | O     | 2     | The   |
   | gning | 0040, |       | al    |       |       |       |       | Attri |
   | Fac   | 0036) |       | lowed |       |       |       |       | butes |
   | ility |       |       |       |       |       |       |       | of    |
   | Seq   |       |       |       |       |       |       |       | the   |
   | uence |       |       |       |       |       |       |       | Assi  |
   |       |       |       |       |       |       |       |       | gning |
   |       |       |       |       |       |       |       |       | Fac   |
   |       |       |       |       |       |       |       |       | ility |
   |       |       |       |       |       |       |       |       | Seq   |
   |       |       |       |       |       |       |       |       | uence |
   |       |       |       |       |       |       |       |       | shall |
   |       |       |       |       |       |       |       |       | only  |
   |       |       |       |       |       |       |       |       | be    |
   |       |       |       |       |       |       |       |       | retr  |
   |       |       |       |       |       |       |       |       | ieved |
   |       |       |       |       |       |       |       |       | with  |
   |       |       |       |       |       |       |       |       | Seq   |
   |       |       |       |       |       |       |       |       | uence |
   |       |       |       |       |       |       |       |       | Matc  |
   |       |       |       |       |       |       |       |       | hing. |
   +-------+-------+-------+-------+-------+-------+-------+-------+-------+
   | *>    |       |       |       |       |       |       |       |       |
   | >Incl |       |       |       |       |       |       |       |       |
   | ude*\ |       |       |       |       |       |       |       |       |
   |  `tab |       |       |       |       |       |       |       |       |
   | le_ti |       |       |       |       |       |       |       |       |
   | tle < |       |       |       |       |       |       |       |       |
   | #tabl |       |       |       |       |       |       |       |       |
   | e_CC. |       |       |       |       |       |       |       |       |
   | 2.5-2 |       |       |       |       |       |       |       |       |
   | d>`__ |       |       |       |       |       |       |       |       |
   +-------+-------+-------+-------+-------+-------+-------+-------+-------+
   | >Assi | (     | 2/2   | Not   | O     | 3/2   | O     | 2     | The   |
   | gning | 0040, |       | al    |       |       |       |       | Attri |
   | Ju    | 0039) |       | lowed |       |       |       |       | butes |
   | risdi |       |       |       |       |       |       |       | of    |
   | ction |       |       |       |       |       |       |       | the   |
   | Code  |       |       |       |       |       |       |       | Assi  |
   | Seq   |       |       |       |       |       |       |       | gning |
   | uence |       |       |       |       |       |       |       | Ju    |
   |       |       |       |       |       |       |       |       | risdi |
   |       |       |       |       |       |       |       |       | ction |
   |       |       |       |       |       |       |       |       | Code  |
   |       |       |       |       |       |       |       |       | Seq   |
   |       |       |       |       |       |       |       |       | uence |
   |       |       |       |       |       |       |       |       | shall |
   |       |       |       |       |       |       |       |       | only  |
   |       |       |       |       |       |       |       |       | be    |
   |       |       |       |       |       |       |       |       | retr  |
   |       |       |       |       |       |       |       |       | ieved |
   |       |       |       |       |       |       |       |       | with  |
   |       |       |       |       |       |       |       |       | Seq   |
   |       |       |       |       |       |       |       |       | uence |
   |       |       |       |       |       |       |       |       | Matc  |
   |       |       |       |       |       |       |       |       | hing. |
   +-------+-------+-------+-------+-------+-------+-------+-------+-------+
   | *>    | *Bas  |       |       |       |       |       |       |       |
   | >Incl | eline |       |       |       |       |       |       |       |
   | ude*\ | for   |       |       |       |       |       |       |       |
   |  `tab | co    |       |       |       |       |       |       |       |
   | le_ti | untry |       |       |       |       |       |       |       |
   | tle < | co    |       |       |       |       |       |       |       |
   | #tabl | des.* |       |       |       |       |       |       |       |
   | e_CC. |       |       |       |       |       |       |       |       |
   | 2.5-2 |       |       |       |       |       |       |       |       |
   | a>`__ |       |       |       |       |       |       |       |       |
   +-------+-------+-------+-------+-------+-------+-------+-------+-------+
   | >Assi | (     | 2/2   | Not   | O     | 3/2   | O     | 2     | The   |
   | gning | 0040, |       | al    |       |       |       |       | Attri |
   | A     | 003A) |       | lowed |       |       |       |       | butes |
   | gency |       |       |       |       |       |       |       | of    |
   | or    |       |       |       |       |       |       |       | the   |
   | Depar |       |       |       |       |       |       |       | Assi  |
   | tment |       |       |       |       |       |       |       | gning |
   | Code  |       |       |       |       |       |       |       | A     |
   | Seq   |       |       |       |       |       |       |       | gency |
   | uence |       |       |       |       |       |       |       | or    |
   |       |       |       |       |       |       |       |       | Depar |
   |       |       |       |       |       |       |       |       | tment |
   |       |       |       |       |       |       |       |       | Code  |
   |       |       |       |       |       |       |       |       | Seq   |
   |       |       |       |       |       |       |       |       | uence |
   |       |       |       |       |       |       |       |       | shall |
   |       |       |       |       |       |       |       |       | only  |
   |       |       |       |       |       |       |       |       | be    |
   |       |       |       |       |       |       |       |       | retr  |
   |       |       |       |       |       |       |       |       | ieved |
   |       |       |       |       |       |       |       |       | with  |
   |       |       |       |       |       |       |       |       | Seq   |
   |       |       |       |       |       |       |       |       | uence |
   |       |       |       |       |       |       |       |       | Matc  |
   |       |       |       |       |       |       |       |       | hing. |
   +-------+-------+-------+-------+-------+-------+-------+-------+-------+
   | *>    | *No   |       |       |       |       |       |       |       |
   | >Incl | Bas   |       |       |       |       |       |       |       |
   | ude*\ | eline |       |       |       |       |       |       |       |
   |  `tab | CID.* |       |       |       |       |       |       |       |
   | le_ti |       |       |       |       |       |       |       |       |
   | tle < |       |       |       |       |       |       |       |       |
   | #tabl |       |       |       |       |       |       |       |       |
   | e_CC. |       |       |       |       |       |       |       |       |
   | 2.5-2 |       |       |       |       |       |       |       |       |
   | a>`__ |       |       |       |       |       |       |       |       |
   +-------+-------+-------+-------+-------+-------+-------+-------+-------+

.. table:: SOP Instance Reference Macro

   +-------+-------+-------+-------+-------+-------+-------+-------+-------+
   | Attr  | Tag   | Req.  | Req.  | Final | Req.  | Match | R     | Remar |
   | ibute |       | Type  | Type  | State | Type  | Key   | eturn | k/Mat |
   | Name  |       | N-C   | N-SET |       | N-GET | Type  | Key   | ching |
   |       |       | REATE | (SCU  |       | (SCU  |       | Type  | Type  |
   |       |       | (SCU  | /SCP) |       | /SCP) |       |       |       |
   |       |       | /SCP) |       |       |       |       |       |       |
   +=======+=======+=======+=======+=======+=======+=======+=======+=======+
   | Refer | (     | 1/1   | 1/1   |       | -/1   | \*    | 1     |       |
   | enced | 0008, |       |       |       |       |       |       |       |
   | SOP   | 1150) |       |       |       |       |       |       |       |
   | Class |       |       |       |       |       |       |       |       |
   | UID   |       |       |       |       |       |       |       |       |
   +-------+-------+-------+-------+-------+-------+-------+-------+-------+
   | Refer | (     | 1/1   | 1/1   |       | -/1   | \*    | 1     |       |
   | enced | 0008, |       |       |       |       |       |       |       |
   | SOP   | 1155) |       |       |       |       |       |       |       |
   | Ins   |       |       |       |       |       |       |       |       |
   | tance |       |       |       |       |       |       |       |       |
   | UID   |       |       |       |       |       |       |       |       |
   +-------+-------+-------+-------+-------+-------+-------+-------+-------+

.. table:: Storage Macro

   +-------+-------+-------+-------+-------+-------+-------+-------+-------+
   | Attr  | Tag   | Req.  | Req.  | Final | Req.  | Match | R     | Remar |
   | ibute |       | Type  | Type  | State | Type  | Key   | eturn | k/Mat |
   | Name  |       | N-C   | N-SET |       | N-GET | Type  | Key   | ching |
   |       |       | REATE | (SCU  |       | (SCU  |       | Type  | Type  |
   |       |       | (SCU  | /SCP) |       | /SCP) |       |       |       |
   |       |       | /SCP) |       |       |       |       |       |       |
   +=======+=======+=======+=======+=======+=======+=======+=======+=======+
   | Refer | (     | 1C/1  | 1C/1  |       | -/1   | O     | 1C    | Req   |
   | enced | 0008, |       |       |       |       |       |       | uired |
   | SOP   | 1150) |       |       |       |       |       |       | if    |
   | Class |       |       |       |       |       |       |       | the   |
   | UID   |       |       |       |       |       |       |       | st    |
   |       |       |       |       |       |       |       |       | orage |
   |       |       |       |       |       |       |       |       | re    |
   |       |       |       |       |       |       |       |       | quest |
   |       |       |       |       |       |       |       |       | only  |
   |       |       |       |       |       |       |       |       | ap    |
   |       |       |       |       |       |       |       |       | plies |
   |       |       |       |       |       |       |       |       | to a  |
   |       |       |       |       |       |       |       |       | spe   |
   |       |       |       |       |       |       |       |       | cific |
   |       |       |       |       |       |       |       |       | SOP   |
   |       |       |       |       |       |       |       |       | C     |
   |       |       |       |       |       |       |       |       | lass. |
   +-------+-------+-------+-------+-------+-------+-------+-------+-------+
   | DICOM | (     | 1C/1  | 1C/1  |       | -/1   | O     | 1C    | Req   |
   | St    | 0040, |       |       |       |       |       |       | uired |
   | orage | 4071) |       |       |       |       |       |       | if    |
   | Seq   |       |       |       |       |       |       |       | ST    |
   | uence |       |       |       |       |       |       |       | OW-RS |
   |       |       |       |       |       |       |       |       | St    |
   |       |       |       |       |       |       |       |       | orage |
   |       |       |       |       |       |       |       |       | Seq   |
   |       |       |       |       |       |       |       |       | uence |
   |       |       |       |       |       |       |       |       | (     |
   |       |       |       |       |       |       |       |       | 0040, |
   |       |       |       |       |       |       |       |       | 4072) |
   |       |       |       |       |       |       |       |       | and   |
   |       |       |       |       |       |       |       |       | XDS   |
   |       |       |       |       |       |       |       |       | St    |
   |       |       |       |       |       |       |       |       | orage |
   |       |       |       |       |       |       |       |       | Seq   |
   |       |       |       |       |       |       |       |       | uence |
   |       |       |       |       |       |       |       |       | (     |
   |       |       |       |       |       |       |       |       | 0040, |
   |       |       |       |       |       |       |       |       | 4074) |
   |       |       |       |       |       |       |       |       | are   |
   |       |       |       |       |       |       |       |       | not   |
   |       |       |       |       |       |       |       |       | pre   |
   |       |       |       |       |       |       |       |       | sent. |
   |       |       |       |       |       |       |       |       | May   |
   |       |       |       |       |       |       |       |       | be    |
   |       |       |       |       |       |       |       |       | pr    |
   |       |       |       |       |       |       |       |       | esent |
   |       |       |       |       |       |       |       |       | other |
   |       |       |       |       |       |       |       |       | wise. |
   +-------+-------+-------+-------+-------+-------+-------+-------+-------+
   | >D    | (     | 1/1   | 1/1   |       | -/1   | \*    | 1     |       |
   | estin | 0040, |       |       |       |       |       |       |       |
   | ation | 4071) |       |       |       |       |       |       |       |
   | AE    |       |       |       |       |       |       |       |       |
   +-------+-------+-------+-------+-------+-------+-------+-------+-------+
   | ST    | (     | 1C/1  | 1C/1  |       | -/1   | O     | 1C    | Req   |
   | OW-RS | 0040, |       |       |       |       |       |       | uired |
   | St    | 4072) |       |       |       |       |       |       | if    |
   | orage |       |       |       |       |       |       |       | DICOM |
   | Seq   |       |       |       |       |       |       |       | St    |
   | uence |       |       |       |       |       |       |       | orage |
   |       |       |       |       |       |       |       |       | Seq   |
   |       |       |       |       |       |       |       |       | uence |
   |       |       |       |       |       |       |       |       | (     |
   |       |       |       |       |       |       |       |       | 0040, |
   |       |       |       |       |       |       |       |       | 4071) |
   |       |       |       |       |       |       |       |       | and   |
   |       |       |       |       |       |       |       |       | XDS   |
   |       |       |       |       |       |       |       |       | St    |
   |       |       |       |       |       |       |       |       | orage |
   |       |       |       |       |       |       |       |       | Seq   |
   |       |       |       |       |       |       |       |       | uence |
   |       |       |       |       |       |       |       |       | (     |
   |       |       |       |       |       |       |       |       | 0040, |
   |       |       |       |       |       |       |       |       | 4074) |
   |       |       |       |       |       |       |       |       | are   |
   |       |       |       |       |       |       |       |       | not   |
   |       |       |       |       |       |       |       |       | pre   |
   |       |       |       |       |       |       |       |       | sent. |
   |       |       |       |       |       |       |       |       | May   |
   |       |       |       |       |       |       |       |       | be    |
   |       |       |       |       |       |       |       |       | pr    |
   |       |       |       |       |       |       |       |       | esent |
   |       |       |       |       |       |       |       |       | other |
   |       |       |       |       |       |       |       |       | wise. |
   +-------+-------+-------+-------+-------+-------+-------+-------+-------+
   | >St   | (     | 1/1   | 1/1   |       | -/1   | \*    | 1     |       |
   | orage | 0040, |       |       |       |       |       |       |       |
   | URL   | 4073) |       |       |       |       |       |       |       |
   +-------+-------+-------+-------+-------+-------+-------+-------+-------+
   | XDS   | (     | 1C/1  | 1C/1  |       | -/1   | O     | 1C    | Req   |
   | St    | 0040, |       |       |       |       |       |       | uired |
   | orage | 4074) |       |       |       |       |       |       | if    |
   | Seq   |       |       |       |       |       |       |       | DICOM |
   | uence |       |       |       |       |       |       |       | St    |
   |       |       |       |       |       |       |       |       | orage |
   |       |       |       |       |       |       |       |       | Seq   |
   |       |       |       |       |       |       |       |       | uence |
   |       |       |       |       |       |       |       |       | (     |
   |       |       |       |       |       |       |       |       | 0040, |
   |       |       |       |       |       |       |       |       | 4071) |
   |       |       |       |       |       |       |       |       | and   |
   |       |       |       |       |       |       |       |       | ST    |
   |       |       |       |       |       |       |       |       | OW-RS |
   |       |       |       |       |       |       |       |       | St    |
   |       |       |       |       |       |       |       |       | orage |
   |       |       |       |       |       |       |       |       | Seq   |
   |       |       |       |       |       |       |       |       | uence |
   |       |       |       |       |       |       |       |       | (     |
   |       |       |       |       |       |       |       |       | 0040, |
   |       |       |       |       |       |       |       |       | 4072) |
   |       |       |       |       |       |       |       |       | are   |
   |       |       |       |       |       |       |       |       | not   |
   |       |       |       |       |       |       |       |       | pre   |
   |       |       |       |       |       |       |       |       | sent. |
   |       |       |       |       |       |       |       |       | May   |
   |       |       |       |       |       |       |       |       | be    |
   |       |       |       |       |       |       |       |       | pr    |
   |       |       |       |       |       |       |       |       | esent |
   |       |       |       |       |       |       |       |       | other |
   |       |       |       |       |       |       |       |       | wise. |
   +-------+-------+-------+-------+-------+-------+-------+-------+-------+
   | >     | (     | 1/1   | 1/1   |       | -/1   | \*    | 1     |       |
   | Repos | 0040, |       |       |       |       |       |       |       |
   | itory | E030) |       |       |       |       |       |       |       |
   | U     |       |       |       |       |       |       |       |       |
   | nique |       |       |       |       |       |       |       |       |
   | ID    |       |       |       |       |       |       |       |       |
   +-------+-------+-------+-------+-------+-------+-------+-------+-------+
   | >Home | (     | 3/2   | 3/2   |       | 3/2   | \*    | 2     |       |
   | Comm  | 0040, |       |       |       |       |       |       |       |
   | unity | E031) |       |       |       |       |       |       |       |
   | ID    |       |       |       |       |       |       |       |       |
   +-------+-------+-------+-------+-------+-------+-------+-------+-------+

.. _sect_CC.2.5.1.3:

UPS Attribute Service Requirements
''''''''''''''''''''''''''''''''''

This table combines the Attribute requirements for multiple DIMSE
services (N-CREATE, N-SET, N-GET, C-FIND) to facilitate consistency
between the requirements.

See PS3.4 for the meaning of the requirement codes used in the N-CREATE,
N-SET, N-GET and Return Key columns in the following table.

See `Conventions <#sect_C.1.2>`__ for the meaning of the requirement
codes used in the Match Key column in the following table.

See `table_title <#table_CC.2.5-1>`__ for the meaning of the requirement
codes used in the Final State column of the following table.

.. table:: UPS SOP Class N-CREATE/N-SET/N-GET/C-FIND Attributes

   +-------+-------+-------+-------+-------+-------+-------+-------+-------+
   | Attr  | Tag   | Req.  | Req.  | Final | Req.  | Match | R     | Remar |
   | ibute |       | Type  | Type  | State | Type  | Key   | eturn | k/Mat |
   | Name  |       | N-C   | N-SET |       | N-GET | Type  | Key   | ching |
   |       |       | REATE | (SCU  |       | (SCU  |       | Type  | Type  |
   |       |       | (SCU  | /SCP) |       | /SCP) |       |       |       |
   |       |       | /SCP) |       |       |       |       |       |       |
   +=======+=======+=======+=======+=======+=======+=======+=======+=======+
   | T     | (     | 2/2   | (see  | O     | Not   | -     | -     | C     |
   | ransa | 0008, |       | `Se   |       | al    |       |       | annot |
   | ction | 1195) | Shall | rvice |       | lowed |       |       | be    |
   | UID   |       | be    | Class |       |       |       |       | que   |
   |       |       | empty | Pro   |       |       |       |       | ried. |
   |       |       |       | vider |       |       |       |       |       |
   |       |       |       | Beha  |       |       |       |       |       |
   |       |       |       | vior  |       |       |       |       |       |
   |       |       |       | <#sec |       |       |       |       |       |
   |       |       |       | t_CC. |       |       |       |       |       |
   |       |       |       | 2.6.3 |       |       |       |       |       |
   |       |       |       | >`__) |       |       |       |       |       |
   +-------+-------+-------+-------+-------+-------+-------+-------+-------+
   | **SOP |       |       |       |       |       |       |       |       |
   | C     |       |       |       |       |       |       |       |       |
   | ommon |       |       |       |       |       |       |       |       |
   | Mod   |       |       |       |       |       |       |       |       |
   | ule** |       |       |       |       |       |       |       |       |
   +-------+-------+-------+-------+-------+-------+-------+-------+-------+
   | Spe   | (     | 1C/1C | 1C/1C | RC    | 3/1   | -     | 1C    | Req   |
   | cific | 0008, |       |       |       |       |       |       | uired |
   | Char  | 0005) |       |       |       |       |       |       | if    |
   | acter |       |       |       |       |       |       |       | ext   |
   | Set   |       |       |       |       |       |       |       | ended |
   |       |       |       |       |       |       |       |       | or    |
   |       |       |       |       |       |       |       |       | r     |
   |       |       |       |       |       |       |       |       | eplac |
   |       |       |       |       |       |       |       |       | ement |
   |       |       |       |       |       |       |       |       | char  |
   |       |       |       |       |       |       |       |       | acter |
   |       |       |       |       |       |       |       |       | set   |
   |       |       |       |       |       |       |       |       | is    |
   |       |       |       |       |       |       |       |       | used  |
   +-------+-------+-------+-------+-------+-------+-------+-------+-------+
   | SOP   | (     | See   | Not   | R     | Not   | O     | 1     | Uni   |
   | Class | 0008, | `UPS  | al    |       | al    |       |       | quely |
   | UID   | 0016) | SOP   | lowed |       | lowed |       |       | ident |
   |       |       | Class |       |       |       |       |       | ifies |
   |       |       | UI    |       |       |       |       |       | the   |
   |       |       | D <#s |       |       |       |       |       | SOP   |
   |       |       | ect_C |       |       |       |       |       | Class |
   |       |       | C.2.5 |       |       |       |       |       | of    |
   |       |       | .1.3. |       |       |       |       |       | the   |
   |       |       | 1>`__ |       |       |       |       |       | Un    |
   |       |       |       |       |       |       |       |       | ified |
   |       |       |       |       |       |       |       |       | Proc  |
   |       |       |       |       |       |       |       |       | edure |
   |       |       |       |       |       |       |       |       | Step. |
   |       |       |       |       |       |       |       |       |       |
   |       |       |       |       |       |       |       |       | See   |
   |       |       |       |       |       |       |       |       | `Se   |
   |       |       |       |       |       |       |       |       | rvice |
   |       |       |       |       |       |       |       |       | Class |
   |       |       |       |       |       |       |       |       | and   |
   |       |       |       |       |       |       |       |       | SOP   |
   |       |       |       |       |       |       |       |       | Class |
   |       |       |       |       |       |       |       |       | UI    |
   |       |       |       |       |       |       |       |       | Ds <# |
   |       |       |       |       |       |       |       |       | sect_ |
   |       |       |       |       |       |       |       |       | CC.3. |
   |       |       |       |       |       |       |       |       | 1>`__ |
   |       |       |       |       |       |       |       |       | for   |
   |       |       |       |       |       |       |       |       | fu    |
   |       |       |       |       |       |       |       |       | rther |
   |       |       |       |       |       |       |       |       | ex    |
   |       |       |       |       |       |       |       |       | plana |
   |       |       |       |       |       |       |       |       | tion. |
   +-------+-------+-------+-------+-------+-------+-------+-------+-------+
   | SOP   | (     | Not   | Not   | R     | Not   | U     | 1     | Uni   |
   | Ins   | 0008, | all   | all   |       | all   |       |       | quely |
   | tance | 0018) | owed. | owed. |       | owed. |       |       | ident |
   | UID   |       |       |       |       |       |       |       | ifies |
   |       |       | SOP   | SOP   |       | SOP   |       |       | the   |
   |       |       | Ins   | Ins   |       | Ins   |       |       | SOP   |
   |       |       | tance | tance |       | tance |       |       | Ins   |
   |       |       | is    | is    |       | is    |       |       | tance |
   |       |       | con   | con   |       | con   |       |       | of    |
   |       |       | veyed | veyed |       | veyed |       |       | the   |
   |       |       | in    | in    |       | in    |       |       | UPS.  |
   |       |       | the   | the   |       | the   |       |       |       |
   |       |       | Aff   | Requ  |       | Requ  |       |       | SOP   |
   |       |       | ected | ested |       | ested |       |       | Ins   |
   |       |       | SOP   | SOP   |       | SOP   |       |       | tance |
   |       |       | Ins   | Ins   |       | Ins   |       |       | UID   |
   |       |       | tance | tance |       | tance |       |       | shall |
   |       |       | UID   | UID   |       | UID   |       |       | be    |
   |       |       | (     | (     |       | (     |       |       | retr  |
   |       |       | 0000, | 0000, |       | 0000, |       |       | ieved |
   |       |       | 1000) | 1001) |       | 1001) |       |       | with  |
   |       |       |       |       |       |       |       |       | S     |
   |       |       |       |       |       |       |       |       | ingle |
   |       |       |       |       |       |       |       |       | Value |
   |       |       |       |       |       |       |       |       | Matc  |
   |       |       |       |       |       |       |       |       | hing. |
   +-------+-------+-------+-------+-------+-------+-------+-------+-------+
   | *All  |       | 3/3   | 3/3   | O     | 3/3   | -     | -     |       |
   | other |       |       |       |       |       |       |       |       |
   | Attri |       |       |       |       |       |       |       |       |
   | butes |       |       |       |       |       |       |       |       |
   | of    |       |       |       |       |       |       |       |       |
   | the*  |       |       |       |       |       |       |       |       |
   +-------+-------+-------+-------+-------+-------+-------+-------+-------+
   | **Un  |       |       |       |       |       |       |       |       |
   | ified |       |       |       |       |       |       |       |       |
   | Proc  |       |       |       |       |       |       |       |       |
   | edure |       |       |       |       |       |       |       |       |
   | Step  |       |       |       |       |       |       |       |       |
   | Sche  |       |       |       |       |       |       |       |       |
   | duled |       |       |       |       |       |       |       |       |
   | Proc  |       |       |       |       |       |       |       |       |
   | edure |       |       |       |       |       |       |       |       |
   | I     |       |       |       |       |       |       |       |       |
   | nform |       |       |       |       |       |       |       |       |
   | ation |       |       |       |       |       |       |       |       |
   | Mod   |       |       |       |       |       |       |       |       |
   | ule** |       |       |       |       |       |       |       |       |
   +-------+-------+-------+-------+-------+-------+-------+-------+-------+
   | Sche  | (     | 1/1   | 3/1   | R     | 3/1   | R     | 1     | Sche  |
   | duled | 0074, |       |       |       |       |       |       | duled |
   | Proc  | 1200) |       |       |       |       |       |       | Proc  |
   | edure |       |       |       |       |       |       |       | edure |
   | Step  |       |       |       |       |       |       |       | Step  |
   | Pri   |       |       |       |       |       |       |       | Pri   |
   | ority |       |       |       |       |       |       |       | ority |
   |       |       |       |       |       |       |       |       | shall |
   |       |       |       |       |       |       |       |       | be    |
   |       |       |       |       |       |       |       |       | retr  |
   |       |       |       |       |       |       |       |       | ieved |
   |       |       |       |       |       |       |       |       | with  |
   |       |       |       |       |       |       |       |       | S     |
   |       |       |       |       |       |       |       |       | ingle |
   |       |       |       |       |       |       |       |       | Value |
   |       |       |       |       |       |       |       |       | Matc  |
   |       |       |       |       |       |       |       |       | hing. |
   +-------+-------+-------+-------+-------+-------+-------+-------+-------+
   | Sche  | (     | -/1   | -/1   | R     | 3/1   | O     | 3     | Sche  |
   | duled | 0040, |       |       |       |       |       |       | duled |
   | Proc  | 4010) | SCP   | SCP   |       |       |       |       | Proc  |
   | edure |       | shall | shall |       |       |       |       | edure |
   | Step  |       | use   | use   |       |       |       |       | Step  |
   | Mo    |       | time  | time  |       |       |       |       | Mo    |
   | dific |       | of    | of    |       |       |       |       | dific |
   | ation |       | C     | SET   |       |       |       |       | ation |
   | Dat   |       | REATE |       |       |       |       |       | Dat   |
   | eTime |       |       |       |       |       |       |       | eTime |
   |       |       |       |       |       |       |       |       | shall |
   |       |       |       |       |       |       |       |       | be    |
   |       |       |       |       |       |       |       |       | retr  |
   |       |       |       |       |       |       |       |       | ieved |
   |       |       |       |       |       |       |       |       | with  |
   |       |       |       |       |       |       |       |       | S     |
   |       |       |       |       |       |       |       |       | ingle |
   |       |       |       |       |       |       |       |       | Value |
   |       |       |       |       |       |       |       |       | Mat   |
   |       |       |       |       |       |       |       |       | ching |
   |       |       |       |       |       |       |       |       | or    |
   |       |       |       |       |       |       |       |       | Range |
   |       |       |       |       |       |       |       |       | Matc  |
   |       |       |       |       |       |       |       |       | hing. |
   +-------+-------+-------+-------+-------+-------+-------+-------+-------+
   | Proc  | (     | 1/1   | 3/1   | O     | 3/1   | R     | 1     |       |
   | edure | 0074, |       |       |       |       |       |       |       |
   | Step  | 1204) |       |       |       |       |       |       |       |
   | Label |       |       |       |       |       |       |       |       |
   +-------+-------+-------+-------+-------+-------+-------+-------+-------+
   | Wor   | (     | 2/1   | 3/1   | O     | 3/1   | R     | 1     |       |
   | klist | 0074, |       |       |       |       |       |       |       |
   | Label | 1202) | If a  |       |       |       |       |       |       |
   |       |       | value |       |       |       |       |       |       |
   |       |       | is    |       |       |       |       |       |       |
   |       |       | not   |       |       |       |       |       |       |
   |       |       | pro   |       |       |       |       |       |       |
   |       |       | vided |       |       |       |       |       |       |
   |       |       | by    |       |       |       |       |       |       |
   |       |       | the   |       |       |       |       |       |       |
   |       |       | SCU,  |       |       |       |       |       |       |
   |       |       | the   |       |       |       |       |       |       |
   |       |       | SCP   |       |       |       |       |       |       |
   |       |       | shall |       |       |       |       |       |       |
   |       |       | fill  |       |       |       |       |       |       |
   |       |       | in    |       |       |       |       |       |       |
   |       |       | the   |       |       |       |       |       |       |
   |       |       | Wor   |       |       |       |       |       |       |
   |       |       | klist |       |       |       |       |       |       |
   |       |       | L     |       |       |       |       |       |       |
   |       |       | abel, |       |       |       |       |       |       |
   |       |       | e.g., |       |       |       |       |       |       |
   |       |       | using |       |       |       |       |       |       |
   |       |       | a     |       |       |       |       |       |       |
   |       |       | de    |       |       |       |       |       |       |
   |       |       | fault |       |       |       |       |       |       |
   |       |       | value |       |       |       |       |       |       |
   |       |       | or by |       |       |       |       |       |       |
   |       |       | assi  |       |       |       |       |       |       |
   |       |       | gning |       |       |       |       |       |       |
   |       |       | the   |       |       |       |       |       |       |
   |       |       | UPS   |       |       |       |       |       |       |
   |       |       | ins   |       |       |       |       |       |       |
   |       |       | tance |       |       |       |       |       |       |
   |       |       | to a  |       |       |       |       |       |       |
   |       |       | lo    |       |       |       |       |       |       |
   |       |       | gical |       |       |       |       |       |       |
   |       |       | work  |       |       |       |       |       |       |
   |       |       | list. |       |       |       |       |       |       |
   +-------+-------+-------+-------+-------+-------+-------+-------+-------+
   | Sche  | (     | 2/2   | 3/2   | O     | 3/2   | -     | 2     |       |
   | duled | 0074, |       |       |       |       |       |       |       |
   | Proce | 1210) |       |       |       |       |       |       |       |
   | ssing |       |       |       |       |       |       |       |       |
   | Param |       |       |       |       |       |       |       |       |
   | eters |       |       |       |       |       |       |       |       |
   | Seq   |       |       |       |       |       |       |       |       |
   | uence |       |       |       |       |       |       |       |       |
   +-------+-------+-------+-------+-------+-------+-------+-------+-------+
   | *     |       |       |       |       |       |       |       |       |
   | >Incl |       |       |       |       |       |       |       |       |
   | ude*\ |       |       |       |       |       |       |       |       |
   |  `tab |       |       |       |       |       |       |       |       |
   | le_ti |       |       |       |       |       |       |       |       |
   | tle < |       |       |       |       |       |       |       |       |
   | #tabl |       |       |       |       |       |       |       |       |
   | e_CC. |       |       |       |       |       |       |       |       |
   | 2.5-2 |       |       |       |       |       |       |       |       |
   | b>`__ |       |       |       |       |       |       |       |       |
   +-------+-------+-------+-------+-------+-------+-------+-------+-------+
   | Sche  | (     | 2/2   | 3/2   | O     | 3/2   | R     | 2     | The   |
   | duled | 0040, |       |       |       |       |       |       | Attri |
   | St    | 4025) |       |       |       |       |       |       | butes |
   | ation |       |       |       |       |       |       |       | of    |
   | Name  |       |       |       |       |       |       |       | the   |
   | Code  |       |       |       |       |       |       |       | Sche  |
   | Seq   |       |       |       |       |       |       |       | duled |
   | uence |       |       |       |       |       |       |       | St    |
   |       |       |       |       |       |       |       |       | ation |
   |       |       |       |       |       |       |       |       | Name  |
   |       |       |       |       |       |       |       |       | Code  |
   |       |       |       |       |       |       |       |       | Seq   |
   |       |       |       |       |       |       |       |       | uence |
   |       |       |       |       |       |       |       |       | shall |
   |       |       |       |       |       |       |       |       | only  |
   |       |       |       |       |       |       |       |       | be    |
   |       |       |       |       |       |       |       |       | retr  |
   |       |       |       |       |       |       |       |       | ieved |
   |       |       |       |       |       |       |       |       | with  |
   |       |       |       |       |       |       |       |       | Seq   |
   |       |       |       |       |       |       |       |       | uence |
   |       |       |       |       |       |       |       |       | Matc  |
   |       |       |       |       |       |       |       |       | hing. |
   |       |       |       |       |       |       |       |       |       |
   |       |       |       |       |       |       |       |       | .. n  |
   |       |       |       |       |       |       |       |       | ote:: |
   |       |       |       |       |       |       |       |       |       |
   |       |       |       |       |       |       |       |       |    In |
   |       |       |       |       |       |       |       |       |       |
   |       |       |       |       |       |       |       |       |  Push |
   |       |       |       |       |       |       |       |       |       |
   |       |       |       |       |       |       |       |       |  Scen |
   |       |       |       |       |       |       |       |       | ario, |
   |       |       |       |       |       |       |       |       |       |
   |       |       |       |       |       |       |       |       |   the |
   |       |       |       |       |       |       |       |       |       |
   |       |       |       |       |       |       |       |       |   SCP |
   |       |       |       |       |       |       |       |       | -Perf |
   |       |       |       |       |       |       |       |       | ormer |
   |       |       |       |       |       |       |       |       |       |
   |       |       |       |       |       |       |       |       |   has |
   |       |       |       |       |       |       |       |       |    to |
   |       |       |       |       |       |       |       |       |    c  |
   |       |       |       |       |       |       |       |       | reate |
   |       |       |       |       |       |       |       |       |       |
   |       |       |       |       |       |       |       |       | empty |
   |       |       |       |       |       |       |       |       |       |
   |       |       |       |       |       |       |       |       |   but |
   |       |       |       |       |       |       |       |       |       |
   |       |       |       |       |       |       |       |       | could |
   |       |       |       |       |       |       |       |       |       |
   |       |       |       |       |       |       |       |       |  self |
   |       |       |       |       |       |       |       |       |       |
   |       |       |       |       |       |       |       |       |  fill |
   |       |       |       |       |       |       |       |       |    l  |
   |       |       |       |       |       |       |       |       | ater. |
   +-------+-------+-------+-------+-------+-------+-------+-------+-------+
   | *     |       |       |       |       |       |       |       |       |
   | >Incl |       |       |       |       |       |       |       |       |
   | ude*\ |       |       |       |       |       |       |       |       |
   |  `tab |       |       |       |       |       |       |       |       |
   | le_ti |       |       |       |       |       |       |       |       |
   | tle < |       |       |       |       |       |       |       |       |
   | #tabl |       |       |       |       |       |       |       |       |
   | e_CC. |       |       |       |       |       |       |       |       |
   | 2.5-2 |       |       |       |       |       |       |       |       |
   | a>`__ |       |       |       |       |       |       |       |       |
   +-------+-------+-------+-------+-------+-------+-------+-------+-------+
   | Sche  | (     | 2/2   | 3/2   | O     | 3/2   | R     | 2     | The   |
   | duled | 0040, |       |       |       |       |       |       | Attri |
   | St    | 4026) |       |       |       |       |       |       | butes |
   | ation |       |       |       |       |       |       |       | of    |
   | Class |       |       |       |       |       |       |       | the   |
   | Code  |       |       |       |       |       |       |       | Sche  |
   | Seq   |       |       |       |       |       |       |       | duled |
   | uence |       |       |       |       |       |       |       | St    |
   |       |       |       |       |       |       |       |       | ation |
   |       |       |       |       |       |       |       |       | Class |
   |       |       |       |       |       |       |       |       | Code  |
   |       |       |       |       |       |       |       |       | Seq   |
   |       |       |       |       |       |       |       |       | uence |
   |       |       |       |       |       |       |       |       | shall |
   |       |       |       |       |       |       |       |       | only  |
   |       |       |       |       |       |       |       |       | be    |
   |       |       |       |       |       |       |       |       | retr  |
   |       |       |       |       |       |       |       |       | ieved |
   |       |       |       |       |       |       |       |       | with  |
   |       |       |       |       |       |       |       |       | Seq   |
   |       |       |       |       |       |       |       |       | uence |
   |       |       |       |       |       |       |       |       | Matc  |
   |       |       |       |       |       |       |       |       | hing. |
   +-------+-------+-------+-------+-------+-------+-------+-------+-------+
   | *     |       |       |       |       |       |       |       |       |
   | >Incl |       |       |       |       |       |       |       |       |
   | ude*\ |       |       |       |       |       |       |       |       |
   |  `tab |       |       |       |       |       |       |       |       |
   | le_ti |       |       |       |       |       |       |       |       |
   | tle < |       |       |       |       |       |       |       |       |
   | #tabl |       |       |       |       |       |       |       |       |
   | e_CC. |       |       |       |       |       |       |       |       |
   | 2.5-2 |       |       |       |       |       |       |       |       |
   | a>`__ |       |       |       |       |       |       |       |       |
   +-------+-------+-------+-------+-------+-------+-------+-------+-------+
   | Sche  | (     | 2/2   | 3/2   | O     | 3/2   | R     | 2     | The   |
   | duled | 0040, |       |       |       |       |       |       | Attri |
   | St    | 4027) |       |       |       |       |       |       | butes |
   | ation |       |       |       |       |       |       |       | of    |
   | Geogr |       |       |       |       |       |       |       | the   |
   | aphic |       |       |       |       |       |       |       | Sche  |
   | Loc   |       |       |       |       |       |       |       | duled |
   | ation |       |       |       |       |       |       |       | St    |
   | Code  |       |       |       |       |       |       |       | ation |
   | Seq   |       |       |       |       |       |       |       | Geogr |
   | uence |       |       |       |       |       |       |       | aphic |
   |       |       |       |       |       |       |       |       | Loc   |
   |       |       |       |       |       |       |       |       | ation |
   |       |       |       |       |       |       |       |       | Code  |
   |       |       |       |       |       |       |       |       | Seq   |
   |       |       |       |       |       |       |       |       | uence |
   |       |       |       |       |       |       |       |       | shall |
   |       |       |       |       |       |       |       |       | only  |
   |       |       |       |       |       |       |       |       | be    |
   |       |       |       |       |       |       |       |       | retr  |
   |       |       |       |       |       |       |       |       | ieved |
   |       |       |       |       |       |       |       |       | with  |
   |       |       |       |       |       |       |       |       | Seq   |
   |       |       |       |       |       |       |       |       | uence |
   |       |       |       |       |       |       |       |       | Matc  |
   |       |       |       |       |       |       |       |       | hing. |
   +-------+-------+-------+-------+-------+-------+-------+-------+-------+
   | *     |       |       |       |       |       |       |       |       |
   | >Incl |       |       |       |       |       |       |       |       |
   | ude*\ |       |       |       |       |       |       |       |       |
   |  `tab |       |       |       |       |       |       |       |       |
   | le_ti |       |       |       |       |       |       |       |       |
   | tle < |       |       |       |       |       |       |       |       |
   | #tabl |       |       |       |       |       |       |       |       |
   | e_CC. |       |       |       |       |       |       |       |       |
   | 2.5-2 |       |       |       |       |       |       |       |       |
   | a>`__ |       |       |       |       |       |       |       |       |
   +-------+-------+-------+-------+-------+-------+-------+-------+-------+
   | Sche  | (     | 2C/2C | 3/2   | O     | 3/2   | R     | 2     | The   |
   | duled | 0040, |       |       |       |       |       |       | Attri |
   | Human | 4034) |       |       |       |       |       |       | butes |
   | Perfo |       |       |       |       |       |       |       | of    |
   | rmers |       |       |       |       |       |       |       | the   |
   | Seq   |       |       |       |       |       |       |       | Sche  |
   | uence |       |       |       |       |       |       |       | duled |
   |       |       |       |       |       |       |       |       | Human |
   |       |       |       |       |       |       |       |       | Perfo |
   |       |       |       |       |       |       |       |       | rmers |
   |       |       |       |       |       |       |       |       | Seq   |
   |       |       |       |       |       |       |       |       | uence |
   |       |       |       |       |       |       |       |       | shall |
   |       |       |       |       |       |       |       |       | only  |
   |       |       |       |       |       |       |       |       | be    |
   |       |       |       |       |       |       |       |       | retr  |
   |       |       |       |       |       |       |       |       | ieved |
   |       |       |       |       |       |       |       |       | with  |
   |       |       |       |       |       |       |       |       | Seq   |
   |       |       |       |       |       |       |       |       | uence |
   |       |       |       |       |       |       |       |       | Matc  |
   |       |       |       |       |       |       |       |       | hing. |
   |       |       |       |       |       |       |       |       |       |
   |       |       |       |       |       |       |       |       | Req   |
   |       |       |       |       |       |       |       |       | uired |
   |       |       |       |       |       |       |       |       | if a  |
   |       |       |       |       |       |       |       |       | Human |
   |       |       |       |       |       |       |       |       | Perf  |
   |       |       |       |       |       |       |       |       | ormer |
   |       |       |       |       |       |       |       |       | is    |
   |       |       |       |       |       |       |       |       | speci |
   |       |       |       |       |       |       |       |       | fied. |
   +-------+-------+-------+-------+-------+-------+-------+-------+-------+
   | >     | (     | 1/1   | 1/1   | O     | -/1   | R     | 1     | The   |
   | Human | 0040, |       |       |       |       |       |       | Attri |
   | Perf  | 4009) |       |       |       |       |       |       | butes |
   | ormer |       |       |       |       |       |       |       | of    |
   | Code  |       |       |       |       |       |       |       | the   |
   | Seq   |       |       |       |       |       |       |       | Sche  |
   | uence |       |       |       |       |       |       |       | duled |
   |       |       |       |       |       |       |       |       | Human |
   |       |       |       |       |       |       |       |       | Perfo |
   |       |       |       |       |       |       |       |       | rmers |
   |       |       |       |       |       |       |       |       | Code  |
   |       |       |       |       |       |       |       |       | Seq   |
   |       |       |       |       |       |       |       |       | uence |
   |       |       |       |       |       |       |       |       | shall |
   |       |       |       |       |       |       |       |       | only  |
   |       |       |       |       |       |       |       |       | be    |
   |       |       |       |       |       |       |       |       | retr  |
   |       |       |       |       |       |       |       |       | ieved |
   |       |       |       |       |       |       |       |       | with  |
   |       |       |       |       |       |       |       |       | Seq   |
   |       |       |       |       |       |       |       |       | uence |
   |       |       |       |       |       |       |       |       | Matc  |
   |       |       |       |       |       |       |       |       | hing. |
   +-------+-------+-------+-------+-------+-------+-------+-------+-------+
   | *>    |       |       |       |       |       |       |       |       |
   | >Incl |       |       |       |       |       |       |       |       |
   | ude*\ |       |       |       |       |       |       |       |       |
   |  `tab |       |       |       |       |       |       |       |       |
   | le_ti |       |       |       |       |       |       |       |       |
   | tle < |       |       |       |       |       |       |       |       |
   | #tabl |       |       |       |       |       |       |       |       |
   | e_CC. |       |       |       |       |       |       |       |       |
   | 2.5-2 |       |       |       |       |       |       |       |       |
   | a>`__ |       |       |       |       |       |       |       |       |
   +-------+-------+-------+-------+-------+-------+-------+-------+-------+
   | >     | (     | 1/1   | 1/1   | O     | -/1   | O     | 3     |       |
   | Human | 0040, |       |       |       |       |       |       |       |
   | P     | 4037) |       |       |       |       |       |       |       |
   | erfor |       |       |       |       |       |       |       |       |
   | mer's |       |       |       |       |       |       |       |       |
   | Name  |       |       |       |       |       |       |       |       |
   +-------+-------+-------+-------+-------+-------+-------+-------+-------+
   | >     | (     | 1/1   | 1/1   | O     | -/1   | O     | 3     |       |
   | Human | 0040, |       |       |       |       |       |       |       |
   | P     | 4036) |       |       |       |       |       |       |       |
   | erfor |       |       |       |       |       |       |       |       |
   | mer's |       |       |       |       |       |       |       |       |
   | Or    |       |       |       |       |       |       |       |       |
   | ganiz |       |       |       |       |       |       |       |       |
   | ation |       |       |       |       |       |       |       |       |
   +-------+-------+-------+-------+-------+-------+-------+-------+-------+
   | Sche  | (     | 1/1   | 3/1   | R     | 3/1   | R     | 1     | Sche  |
   | duled | 0040, |       |       |       |       |       |       | duled |
   | Proc  | 4005) |       |       |       |       |       |       | Proc  |
   | edure |       |       |       |       |       |       |       | edure |
   | Step  |       |       |       |       |       |       |       | Step  |
   | Start |       |       |       |       |       |       |       | Start |
   | Dat   |       |       |       |       |       |       |       | Dat   |
   | eTime |       |       |       |       |       |       |       | eTime |
   |       |       |       |       |       |       |       |       | shall |
   |       |       |       |       |       |       |       |       | be    |
   |       |       |       |       |       |       |       |       | retr  |
   |       |       |       |       |       |       |       |       | ieved |
   |       |       |       |       |       |       |       |       | with  |
   |       |       |       |       |       |       |       |       | S     |
   |       |       |       |       |       |       |       |       | ingle |
   |       |       |       |       |       |       |       |       | Value |
   |       |       |       |       |       |       |       |       | Mat   |
   |       |       |       |       |       |       |       |       | ching |
   |       |       |       |       |       |       |       |       | or    |
   |       |       |       |       |       |       |       |       | Range |
   |       |       |       |       |       |       |       |       | Matc  |
   |       |       |       |       |       |       |       |       | hing. |
   +-------+-------+-------+-------+-------+-------+-------+-------+-------+
   | Exp   | (     | 3/1   | 3/1   | O     | 3/1   | R     | 3     | Exp   |
   | ected | 0040, |       |       |       |       |       |       | ected |
   | Compl | 4011) |       |       |       |       |       |       | Compl |
   | etion |       |       |       |       |       |       |       | etion |
   | Dat   |       |       |       |       |       |       |       | Dat   |
   | eTime |       |       |       |       |       |       |       | eTime |
   |       |       |       |       |       |       |       |       | shall |
   |       |       |       |       |       |       |       |       | be    |
   |       |       |       |       |       |       |       |       | retr  |
   |       |       |       |       |       |       |       |       | ieved |
   |       |       |       |       |       |       |       |       | with  |
   |       |       |       |       |       |       |       |       | S     |
   |       |       |       |       |       |       |       |       | ingle |
   |       |       |       |       |       |       |       |       | Value |
   |       |       |       |       |       |       |       |       | Mat   |
   |       |       |       |       |       |       |       |       | ching |
   |       |       |       |       |       |       |       |       | or    |
   |       |       |       |       |       |       |       |       | Range |
   |       |       |       |       |       |       |       |       | Matc  |
   |       |       |       |       |       |       |       |       | hing. |
   +-------+-------+-------+-------+-------+-------+-------+-------+-------+
   | Sche  | (     | 3/3   | 3/3   | O     | 3/3   | O     | 3     | Sche  |
   | duled | 0040, |       |       |       |       |       |       | duled |
   | Proc  | 4008) |       |       |       |       |       |       | Proc  |
   | edure |       |       |       |       |       |       |       | edure |
   | Step  |       |       |       |       |       |       |       | Step  |
   | Expir |       |       |       |       |       |       |       | Expir |
   | ation |       |       |       |       |       |       |       | ation |
   | Dat   |       |       |       |       |       |       |       | Dat   |
   | eTime |       |       |       |       |       |       |       | eTime |
   |       |       |       |       |       |       |       |       | shall |
   |       |       |       |       |       |       |       |       | be    |
   |       |       |       |       |       |       |       |       | retr  |
   |       |       |       |       |       |       |       |       | ieved |
   |       |       |       |       |       |       |       |       | with  |
   |       |       |       |       |       |       |       |       | S     |
   |       |       |       |       |       |       |       |       | ingle |
   |       |       |       |       |       |       |       |       | Value |
   |       |       |       |       |       |       |       |       | Mat   |
   |       |       |       |       |       |       |       |       | ching |
   |       |       |       |       |       |       |       |       | or    |
   |       |       |       |       |       |       |       |       | Range |
   |       |       |       |       |       |       |       |       | Matc  |
   |       |       |       |       |       |       |       |       | hing. |
   +-------+-------+-------+-------+-------+-------+-------+-------+-------+
   | Sche  | (     | 2/2   | 3/1   | O     | 3/1   | R     | 2     | The   |
   | duled | 0040, |       |       |       |       |       |       | Attri |
   | Wor   | 4018) |       |       |       |       |       |       | butes |
   | kitem |       |       |       |       |       |       |       | of    |
   | Code  |       |       |       |       |       |       |       | the   |
   | Seq   |       |       |       |       |       |       |       | Sche  |
   | uence |       |       |       |       |       |       |       | duled |
   |       |       |       |       |       |       |       |       | Wor   |
   |       |       |       |       |       |       |       |       | kitem |
   |       |       |       |       |       |       |       |       | Code  |
   |       |       |       |       |       |       |       |       | Seq   |
   |       |       |       |       |       |       |       |       | uence |
   |       |       |       |       |       |       |       |       | shall |
   |       |       |       |       |       |       |       |       | only  |
   |       |       |       |       |       |       |       |       | be    |
   |       |       |       |       |       |       |       |       | retr  |
   |       |       |       |       |       |       |       |       | ieved |
   |       |       |       |       |       |       |       |       | with  |
   |       |       |       |       |       |       |       |       | Seq   |
   |       |       |       |       |       |       |       |       | uence |
   |       |       |       |       |       |       |       |       | Matc  |
   |       |       |       |       |       |       |       |       | hing. |
   +-------+-------+-------+-------+-------+-------+-------+-------+-------+
   | *     |       |       |       |       |       |       |       |       |
   | >Incl |       |       |       |       |       |       |       |       |
   | ude*\ |       |       |       |       |       |       |       |       |
   |  `tab |       |       |       |       |       |       |       |       |
   | le_ti |       |       |       |       |       |       |       |       |
   | tle < |       |       |       |       |       |       |       |       |
   | #tabl |       |       |       |       |       |       |       |       |
   | e_CC. |       |       |       |       |       |       |       |       |
   | 2.5-2 |       |       |       |       |       |       |       |       |
   | a>`__ |       |       |       |       |       |       |       |       |
   +-------+-------+-------+-------+-------+-------+-------+-------+-------+
   | Com   | (     | 2/2   | 3/1   | O     | 3/1   | O     | 3     |       |
   | ments | 0040, |       |       |       |       |       |       |       |
   | on    | 0400) |       |       |       |       |       |       |       |
   | the   |       |       |       |       |       |       |       |       |
   | Sche  |       |       |       |       |       |       |       |       |
   | duled |       |       |       |       |       |       |       |       |
   | Proc  |       |       |       |       |       |       |       |       |
   | edure |       |       |       |       |       |       |       |       |
   | Step  |       |       |       |       |       |       |       |       |
   +-------+-------+-------+-------+-------+-------+-------+-------+-------+
   | Input | (     | 1/1   | 3/1   | R     | 3/1   | R     | 1     | Input |
   | Read  | 0040, |       |       |       |       |       |       | Read  |
   | iness | 4041) |       |       |       |       |       |       | iness |
   | State |       |       |       |       |       |       |       | State |
   |       |       |       |       |       |       |       |       | shall |
   |       |       |       |       |       |       |       |       | be    |
   |       |       |       |       |       |       |       |       | retr  |
   |       |       |       |       |       |       |       |       | ieved |
   |       |       |       |       |       |       |       |       | with  |
   |       |       |       |       |       |       |       |       | S     |
   |       |       |       |       |       |       |       |       | ingle |
   |       |       |       |       |       |       |       |       | Value |
   |       |       |       |       |       |       |       |       | Matc  |
   |       |       |       |       |       |       |       |       | hing. |
   +-------+-------+-------+-------+-------+-------+-------+-------+-------+
   | Input | (     | 2/2   | 3/2   | O     | 3/2   | O     | 2     | The   |
   | I     | 0040, |       |       |       |       |       |       | Attri |
   | nform | 4021) |       |       |       |       |       |       | butes |
   | ation |       |       |       |       |       |       |       | of    |
   | Seq   |       |       |       |       |       |       |       | the   |
   | uence |       |       |       |       |       |       |       | Input |
   |       |       |       |       |       |       |       |       | I     |
   |       |       |       |       |       |       |       |       | nform |
   |       |       |       |       |       |       |       |       | ation |
   |       |       |       |       |       |       |       |       | Seq   |
   |       |       |       |       |       |       |       |       | uence |
   |       |       |       |       |       |       |       |       | shall |
   |       |       |       |       |       |       |       |       | only  |
   |       |       |       |       |       |       |       |       | be    |
   |       |       |       |       |       |       |       |       | retr  |
   |       |       |       |       |       |       |       |       | ieved |
   |       |       |       |       |       |       |       |       | with  |
   |       |       |       |       |       |       |       |       | Seq   |
   |       |       |       |       |       |       |       |       | uence |
   |       |       |       |       |       |       |       |       | Matc  |
   |       |       |       |       |       |       |       |       | hing. |
   +-------+-------+-------+-------+-------+-------+-------+-------+-------+
   | *     |       |       |       |       |       |       |       |       |
   | >Incl |       |       |       |       |       |       |       |       |
   | ude*\ |       |       |       |       |       |       |       |       |
   |  `tab |       |       |       |       |       |       |       |       |
   | le_ti |       |       |       |       |       |       |       |       |
   | tle < |       |       |       |       |       |       |       |       |
   | #tabl |       |       |       |       |       |       |       |       |
   | e_CC. |       |       |       |       |       |       |       |       |
   | 2.5-2 |       |       |       |       |       |       |       |       |
   | c>`__ |       |       |       |       |       |       |       |       |
   +-------+-------+-------+-------+-------+-------+-------+-------+-------+
   | Study | (     | 1C/2  | 3/2   | O     | 3/2   | O     | 2     | Req   |
   | Ins   | 0020, |       |       |       |       |       |       | uired |
   | tance | 000D) |       |       |       |       |       |       | if    |
   | UID   |       |       |       |       |       |       |       | the   |
   |       |       |       |       |       |       |       |       | Wor   |
   |       |       |       |       |       |       |       |       | kitem |
   |       |       |       |       |       |       |       |       | is    |
   |       |       |       |       |       |       |       |       | exp   |
   |       |       |       |       |       |       |       |       | ected |
   |       |       |       |       |       |       |       |       | to    |
   |       |       |       |       |       |       |       |       | r     |
   |       |       |       |       |       |       |       |       | esult |
   |       |       |       |       |       |       |       |       | in    |
   |       |       |       |       |       |       |       |       | the   |
   |       |       |       |       |       |       |       |       | cre   |
   |       |       |       |       |       |       |       |       | ation |
   |       |       |       |       |       |       |       |       | of    |
   |       |       |       |       |       |       |       |       | any   |
   |       |       |       |       |       |       |       |       | DICOM |
   |       |       |       |       |       |       |       |       | Comp  |
   |       |       |       |       |       |       |       |       | osite |
   |       |       |       |       |       |       |       |       | Inst  |
   |       |       |       |       |       |       |       |       | ances |
   |       |       |       |       |       |       |       |       | whose |
   |       |       |       |       |       |       |       |       | IOD   |
   |       |       |       |       |       |       |       |       | con   |
   |       |       |       |       |       |       |       |       | tains |
   |       |       |       |       |       |       |       |       | the   |
   |       |       |       |       |       |       |       |       | Study |
   |       |       |       |       |       |       |       |       | IE.   |
   |       |       |       |       |       |       |       |       |       |
   |       |       |       |       |       |       |       |       | There |
   |       |       |       |       |       |       |       |       | may   |
   |       |       |       |       |       |       |       |       | be    |
   |       |       |       |       |       |       |       |       | situa |
   |       |       |       |       |       |       |       |       | tions |
   |       |       |       |       |       |       |       |       | where |
   |       |       |       |       |       |       |       |       | the   |
   |       |       |       |       |       |       |       |       | perf  |
   |       |       |       |       |       |       |       |       | ormer |
   |       |       |       |       |       |       |       |       | does  |
   |       |       |       |       |       |       |       |       | not   |
   |       |       |       |       |       |       |       |       | use   |
   |       |       |       |       |       |       |       |       | the   |
   |       |       |       |       |       |       |       |       | Study |
   |       |       |       |       |       |       |       |       | Ins   |
   |       |       |       |       |       |       |       |       | tance |
   |       |       |       |       |       |       |       |       | UID   |
   |       |       |       |       |       |       |       |       | sugg  |
   |       |       |       |       |       |       |       |       | ested |
   |       |       |       |       |       |       |       |       | by    |
   |       |       |       |       |       |       |       |       | the   |
   |       |       |       |       |       |       |       |       | Sched |
   |       |       |       |       |       |       |       |       | uler. |
   +-------+-------+-------+-------+-------+-------+-------+-------+-------+
   | O     | (     | 3/3   | 3/3   | O     | 3/3   | O     | 3     | The   |
   | utput | 0040, |       |       |       |       |       |       | Attri |
   | D     | 4070) |       |       |       |       |       |       | butes |
   | estin |       |       |       |       |       |       |       | of    |
   | ation |       |       |       |       |       |       |       | the   |
   | Seq   |       |       |       |       |       |       |       | O     |
   | uence |       |       |       |       |       |       |       | utput |
   |       |       |       |       |       |       |       |       | D     |
   |       |       |       |       |       |       |       |       | estin |
   |       |       |       |       |       |       |       |       | ation |
   |       |       |       |       |       |       |       |       | Seq   |
   |       |       |       |       |       |       |       |       | uence |
   |       |       |       |       |       |       |       |       | shall |
   |       |       |       |       |       |       |       |       | only  |
   |       |       |       |       |       |       |       |       | be    |
   |       |       |       |       |       |       |       |       | retr  |
   |       |       |       |       |       |       |       |       | ieved |
   |       |       |       |       |       |       |       |       | with  |
   |       |       |       |       |       |       |       |       | Seq   |
   |       |       |       |       |       |       |       |       | uence |
   |       |       |       |       |       |       |       |       | Matc  |
   |       |       |       |       |       |       |       |       | hing. |
   +-------+-------+-------+-------+-------+-------+-------+-------+-------+
   | *     |       |       |       |       |       |       |       |       |
   | >Incl |       |       |       |       |       |       |       |       |
   | ude*\ |       |       |       |       |       |       |       |       |
   |  `tab |       |       |       |       |       |       |       |       |
   | le_ti |       |       |       |       |       |       |       |       |
   | tle < |       |       |       |       |       |       |       |       |
   | #tabl |       |       |       |       |       |       |       |       |
   | e_CC. |       |       |       |       |       |       |       |       |
   | 2.5-2 |       |       |       |       |       |       |       |       |
   | g>`__ |       |       |       |       |       |       |       |       |
   +-------+-------+-------+-------+-------+-------+-------+-------+-------+
   | *All  |       | 3/3   | 3/3   | O     | 3/3   | -     | -     |       |
   | other |       |       |       |       |       |       |       |       |
   | Attri |       |       |       |       |       |       |       |       |
   | butes |       |       |       |       |       |       |       |       |
   | of    |       |       |       |       |       |       |       |       |
   | the*  |       |       |       |       |       |       |       |       |
   +-------+-------+-------+-------+-------+-------+-------+-------+-------+
   | **Un  |       |       |       |       |       |       |       |       |
   | ified |       |       |       |       |       |       |       |       |
   | Proc  |       |       |       |       |       |       |       |       |
   | edure |       |       |       |       |       |       |       |       |
   | Step  |       |       |       |       |       |       |       |       |
   | Re    |       |       |       |       |       |       |       |       |
   | latio |       |       |       |       |       |       |       |       |
   | nship |       |       |       |       |       |       |       |       |
   | Mod   |       |       |       |       |       |       |       |       |
   | ule** |       |       |       |       |       |       |       |       |
   +-------+-------+-------+-------+-------+-------+-------+-------+-------+
   | Pati  | (     | 2/2   | Not   | O     | 3/2   | R     | 2     |       |
   | ent's | 0010, |       | al    |       |       |       |       |       |
   | Name  | 0010) |       | lowed |       |       |       |       |       |
   +-------+-------+-------+-------+-------+-------+-------+-------+-------+
   | Pa    | (     | 1C/2  | Not   | O     | 3/2   | R     | 2     | Req   |
   | tient | 0010, |       | al    |       |       |       |       | uired |
   | ID    | 0020) |       | lowed |       |       |       |       | if    |
   |       |       |       |       |       |       |       |       | the   |
   |       |       |       |       |       |       |       |       | su    |
   |       |       |       |       |       |       |       |       | bject |
   |       |       |       |       |       |       |       |       | of    |
   |       |       |       |       |       |       |       |       | the   |
   |       |       |       |       |       |       |       |       | wor   |
   |       |       |       |       |       |       |       |       | kitem |
   |       |       |       |       |       |       |       |       | req   |
   |       |       |       |       |       |       |       |       | uires |
   |       |       |       |       |       |       |       |       | iden  |
   |       |       |       |       |       |       |       |       | tific |
   |       |       |       |       |       |       |       |       | ation |
   |       |       |       |       |       |       |       |       | or if |
   |       |       |       |       |       |       |       |       | the   |
   |       |       |       |       |       |       |       |       | wor   |
   |       |       |       |       |       |       |       |       | kitem |
   |       |       |       |       |       |       |       |       | is    |
   |       |       |       |       |       |       |       |       | exp   |
   |       |       |       |       |       |       |       |       | ected |
   |       |       |       |       |       |       |       |       | to    |
   |       |       |       |       |       |       |       |       | r     |
   |       |       |       |       |       |       |       |       | esult |
   |       |       |       |       |       |       |       |       | in    |
   |       |       |       |       |       |       |       |       | the   |
   |       |       |       |       |       |       |       |       | cre   |
   |       |       |       |       |       |       |       |       | ation |
   |       |       |       |       |       |       |       |       | of    |
   |       |       |       |       |       |       |       |       | ob    |
   |       |       |       |       |       |       |       |       | jects |
   |       |       |       |       |       |       |       |       | that  |
   |       |       |       |       |       |       |       |       | ide   |
   |       |       |       |       |       |       |       |       | ntify |
   |       |       |       |       |       |       |       |       | the   |
   |       |       |       |       |       |       |       |       | sub   |
   |       |       |       |       |       |       |       |       | ject. |
   |       |       |       |       |       |       |       |       |       |
   |       |       |       |       |       |       |       |       | See   |
   +-------+-------+-------+-------+-------+-------+-------+-------+-------+
   | *Incl |       |       |       |       |       |       |       |       |
   | ude*\ |       |       |       |       |       |       |       |       |
   |  `tab |       |       |       |       |       |       |       |       |
   | le_ti |       |       |       |       |       |       |       |       |
   | tle < |       |       |       |       |       |       |       |       |
   | #tabl |       |       |       |       |       |       |       |       |
   | e_CC. |       |       |       |       |       |       |       |       |
   | 2.5-2 |       |       |       |       |       |       |       |       |
   | e>`__ |       |       |       |       |       |       |       |       |
   +-------+-------+-------+-------+-------+-------+-------+-------+-------+
   | Other | (     | 2/2   | 3/3   | O     | 3/2   | O     | 2     |       |
   | Pa    | 0010, |       |       |       |       |       |       |       |
   | tient | 1002) |       |       |       |       |       |       |       |
   | IDs   |       |       |       |       |       |       |       |       |
   | Seq   |       |       |       |       |       |       |       |       |
   | uence |       |       |       |       |       |       |       |       |
   +-------+-------+-------+-------+-------+-------+-------+-------+-------+
   | >Pa   | (     | 1/1   | 1/1   | O     | -/1   | O     | 1     |       |
   | tient | 0010, |       |       |       |       |       |       |       |
   | ID    | 0020) |       |       |       |       |       |       |       |
   +-------+-------+-------+-------+-------+-------+-------+-------+-------+
   | *     |       |       |       |       |       |       |       |       |
   | >Incl |       |       |       |       |       |       |       |       |
   | ude*\ |       |       |       |       |       |       |       |       |
   |  `tab |       |       |       |       |       |       |       |       |
   | le_ti |       |       |       |       |       |       |       |       |
   | tle < |       |       |       |       |       |       |       |       |
   | #tabl |       |       |       |       |       |       |       |       |
   | e_CC. |       |       |       |       |       |       |       |       |
   | 2.5-2 |       |       |       |       |       |       |       |       |
   | e>`__ |       |       |       |       |       |       |       |       |
   +-------+-------+-------+-------+-------+-------+-------+-------+-------+
   | >Type | (     | 3/3   | 3/3   | O     | 3/3   | O     | 3     |       |
   | of    | 0010, |       |       |       |       |       |       |       |
   | Pa    | 0022) |       |       |       |       |       |       |       |
   | tient |       |       |       |       |       |       |       |       |
   | ID    |       |       |       |       |       |       |       |       |
   +-------+-------+-------+-------+-------+-------+-------+-------+-------+
   | Pati  | (     | 2/2   | Not   | O     | 3/2   | R     | 2     |       |
   | ent's | 0010, |       | al    |       |       |       |       |       |
   | Birth | 0030) |       | lowed |       |       |       |       |       |
   | Date  |       |       |       |       |       |       |       |       |
   +-------+-------+-------+-------+-------+-------+-------+-------+-------+
   | Pati  | (     | 2/2   | Not   | O     | 3/2   | R     | 2     |       |
   | ent's | 0010, |       | al    |       |       |       |       |       |
   | Sex   | 0040) |       | lowed |       |       |       |       |       |
   +-------+-------+-------+-------+-------+-------+-------+-------+-------+
   | Refer | (     | 3/3   | 3/3   | O     | 3/3   | -     | 3     |       |
   | enced | 0010, |       |       |       |       |       |       |       |
   | Pa    | 1100) |       |       |       |       |       |       |       |
   | tient |       |       |       |       |       |       |       |       |
   | Photo |       |       |       |       |       |       |       |       |
   | Seq   |       |       |       |       |       |       |       |       |
   | uence |       |       |       |       |       |       |       |       |
   +-------+-------+-------+-------+-------+-------+-------+-------+-------+
   | *     |       |       |       |       |       |       |       |       |
   | >Incl |       |       |       |       |       |       |       |       |
   | ude*\ |       |       |       |       |       |       |       |       |
   |  `tab |       |       |       |       |       |       |       |       |
   | le_ti |       |       |       |       |       |       |       |       |
   | tle < |       |       |       |       |       |       |       |       |
   | #tabl |       |       |       |       |       |       |       |       |
   | e_CC. |       |       |       |       |       |       |       |       |
   | 2.5-2 |       |       |       |       |       |       |       |       |
   | c>`__ |       |       |       |       |       |       |       |       |
   +-------+-------+-------+-------+-------+-------+-------+-------+-------+
   | Admi  | (     | 2/2   | Not   | O     | 3/2   | R     | 2     |       |
   | ssion | 0038, |       | al    |       |       |       |       |       |
   | ID    | 0010) |       | lowed |       |       |       |       |       |
   +-------+-------+-------+-------+-------+-------+-------+-------+-------+
   | I     | (     | 2/2   | Not   | O     | 3/2   | R     | 2     |       |
   | ssuer | 0038, |       | al    |       |       |       |       |       |
   | of    | 0014) |       | lowed |       |       |       |       |       |
   | Admi  |       |       |       |       |       |       |       |       |
   | ssion |       |       |       |       |       |       |       |       |
   | ID    |       |       |       |       |       |       |       |       |
   | Seq   |       |       |       |       |       |       |       |       |
   | uence |       |       |       |       |       |       |       |       |
   +-------+-------+-------+-------+-------+-------+-------+-------+-------+
   | *     |       |       |       |       |       |       |       |       |
   | >Incl |       |       |       |       |       |       |       |       |
   | ude*\ |       |       |       |       |       |       |       |       |
   |  `tab |       |       |       |       |       |       |       |       |
   | le_ti |       |       |       |       |       |       |       |       |
   | tle < |       |       |       |       |       |       |       |       |
   | #tabl |       |       |       |       |       |       |       |       |
   | e_CC. |       |       |       |       |       |       |       |       |
   | 2.5-2 |       |       |       |       |       |       |       |       |
   | d>`__ |       |       |       |       |       |       |       |       |
   +-------+-------+-------+-------+-------+-------+-------+-------+-------+
   | Admi  | (     | 2/2   | Not   | O     | 3/2   | O     | 2     |       |
   | tting | 0008, |       | al    |       |       |       |       |       |
   | Diag  | 1080) |       | lowed |       |       |       |       |       |
   | noses |       |       |       |       |       |       |       |       |
   | D     |       |       |       |       |       |       |       |       |
   | escri |       |       |       |       |       |       |       |       |
   | ption |       |       |       |       |       |       |       |       |
   +-------+-------+-------+-------+-------+-------+-------+-------+-------+
   | Admi  | (     | 2/2   | Not   | O     | 3/2   | O     | 2     | The   |
   | tting | 0008, |       | al    |       |       |       |       | Attri |
   | Diag  | 1084) |       | lowed |       |       |       |       | butes |
   | noses |       |       |       |       |       |       |       | of    |
   | Code  |       |       |       |       |       |       |       | the   |
   | Seq   |       |       |       |       |       |       |       | Admi  |
   | uence |       |       |       |       |       |       |       | tting |
   |       |       |       |       |       |       |       |       | Diag  |
   |       |       |       |       |       |       |       |       | noses |
   |       |       |       |       |       |       |       |       | Code  |
   |       |       |       |       |       |       |       |       | Seq   |
   |       |       |       |       |       |       |       |       | uence |
   |       |       |       |       |       |       |       |       | shall |
   |       |       |       |       |       |       |       |       | only  |
   |       |       |       |       |       |       |       |       | be    |
   |       |       |       |       |       |       |       |       | retr  |
   |       |       |       |       |       |       |       |       | ieved |
   |       |       |       |       |       |       |       |       | with  |
   |       |       |       |       |       |       |       |       | Seq   |
   |       |       |       |       |       |       |       |       | uence |
   |       |       |       |       |       |       |       |       | Matc  |
   |       |       |       |       |       |       |       |       | hing. |
   +-------+-------+-------+-------+-------+-------+-------+-------+-------+
   | *     |       |       |       |       |       |       |       |       |
   | >Incl |       |       |       |       |       |       |       |       |
   | ude*\ |       |       |       |       |       |       |       |       |
   |  `tab |       |       |       |       |       |       |       |       |
   | le_ti |       |       |       |       |       |       |       |       |
   | tle < |       |       |       |       |       |       |       |       |
   | #tabl |       |       |       |       |       |       |       |       |
   | e_CC. |       |       |       |       |       |       |       |       |
   | 2.5-2 |       |       |       |       |       |       |       |       |
   | a>`__ |       |       |       |       |       |       |       |       |
   | \ *.* |       |       |       |       |       |       |       |       |
   +-------+-------+-------+-------+-------+-------+-------+-------+-------+
   | Refer | (     | 2/2   | Not   | O     | 3/2   | R     | 2     | Could |
   | enced | 0040, |       | al    |       |       |       |       | be    |
   | Re    | A370) |       | lowed |       |       |       |       | "cha  |
   | quest |       |       |       |       |       |       |       | nged" |
   | Seq   |       |       |       |       |       |       |       | while |
   | uence |       |       |       |       |       |       |       | SCHE  |
   |       |       |       |       |       |       |       |       | DULED |
   |       |       |       |       |       |       |       |       | by    |
   |       |       |       |       |       |       |       |       | canc  |
   |       |       |       |       |       |       |       |       | eling |
   |       |       |       |       |       |       |       |       | and   |
   |       |       |       |       |       |       |       |       | r     |
   |       |       |       |       |       |       |       |       | e-cre |
   |       |       |       |       |       |       |       |       | ating |
   |       |       |       |       |       |       |       |       | with  |
   |       |       |       |       |       |       |       |       | the   |
   |       |       |       |       |       |       |       |       | "cor  |
   |       |       |       |       |       |       |       |       | rect" |
   |       |       |       |       |       |       |       |       | va    |
   |       |       |       |       |       |       |       |       | lues. |
   +-------+-------+-------+-------+-------+-------+-------+-------+-------+
   | >     | (     | 1/1   | Not   | O     | -/1   | O     | 1     |       |
   | Study | 0020, |       | al    |       |       |       |       |       |
   | Ins   | 000D) |       | lowed |       |       |       |       |       |
   | tance |       |       |       |       |       |       |       |       |
   | UID   |       |       |       |       |       |       |       |       |
   +-------+-------+-------+-------+-------+-------+-------+-------+-------+
   | >Acce | (     | 2/2   | Not   | O     | -/2   | R     | 2     |       |
   | ssion | 0008, |       | al    |       |       |       |       |       |
   | N     | 0050) |       | lowed |       |       |       |       |       |
   | umber |       |       |       |       |       |       |       |       |
   +-------+-------+-------+-------+-------+-------+-------+-------+-------+
   | >I    | (     | 2/2   | Not   | O     | -/2   | R     | 2     | The   |
   | ssuer | 0008, |       | al    |       |       |       |       | I     |
   | of    | 0051) |       | lowed |       |       |       |       | ssuer |
   | Acce  |       |       |       |       |       |       |       | of    |
   | ssion |       |       |       |       |       |       |       | Acce  |
   | N     |       |       |       |       |       |       |       | ssion |
   | umber |       |       |       |       |       |       |       | N     |
   | Seq   |       |       |       |       |       |       |       | umber |
   | uence |       |       |       |       |       |       |       | Seq   |
   |       |       |       |       |       |       |       |       | uence |
   |       |       |       |       |       |       |       |       | shall |
   |       |       |       |       |       |       |       |       | only  |
   |       |       |       |       |       |       |       |       | be    |
   |       |       |       |       |       |       |       |       | retr  |
   |       |       |       |       |       |       |       |       | ieved |
   |       |       |       |       |       |       |       |       | with  |
   |       |       |       |       |       |       |       |       | Seq   |
   |       |       |       |       |       |       |       |       | uence |
   |       |       |       |       |       |       |       |       | Matc  |
   |       |       |       |       |       |       |       |       | hing. |
   +-------+-------+-------+-------+-------+-------+-------+-------+-------+
   | *>    |       |       |       |       |       |       |       |       |
   | >Incl |       |       |       |       |       |       |       |       |
   | ude*\ |       |       |       |       |       |       |       |       |
   |  `tab |       |       |       |       |       |       |       |       |
   | le_ti |       |       |       |       |       |       |       |       |
   | tle < |       |       |       |       |       |       |       |       |
   | #tabl |       |       |       |       |       |       |       |       |
   | e_CC. |       |       |       |       |       |       |       |       |
   | 2.5-2 |       |       |       |       |       |       |       |       |
   | d>`__ |       |       |       |       |       |       |       |       |
   +-------+-------+-------+-------+-------+-------+-------+-------+-------+
   | >P    | (     | 3/1   | Not   | O     | -/1   | O     | 1C    | Req   |
   | lacer | 0040, |       | al    |       |       |       |       | uired |
   | Order | 2016) |       | lowed |       |       |       |       | if    |
   | Numb  |       |       |       |       |       |       |       | set.  |
   | er/Im |       |       |       |       |       |       |       |       |
   | aging |       |       |       |       |       |       |       |       |
   | Se    |       |       |       |       |       |       |       |       |
   | rvice |       |       |       |       |       |       |       |       |
   | Re    |       |       |       |       |       |       |       |       |
   | quest |       |       |       |       |       |       |       |       |
   +-------+-------+-------+-------+-------+-------+-------+-------+-------+
   | >     | (     | 2/2   | Not   | O     | -/2   | O     | 2     | The   |
   | Order | 0040, |       | al    |       |       |       |       | Order |
   | P     | 0026) |       | lowed |       |       |       |       | P     |
   | lacer |       |       |       |       |       |       |       | lacer |
   | Ident |       |       |       |       |       |       |       | Ident |
   | ifier |       |       |       |       |       |       |       | ifier |
   | Seq   |       |       |       |       |       |       |       | Seq   |
   | uence |       |       |       |       |       |       |       | uence |
   |       |       |       |       |       |       |       |       | shall |
   |       |       |       |       |       |       |       |       | only  |
   |       |       |       |       |       |       |       |       | be    |
   |       |       |       |       |       |       |       |       | retr  |
   |       |       |       |       |       |       |       |       | ieved |
   |       |       |       |       |       |       |       |       | with  |
   |       |       |       |       |       |       |       |       | Seq   |
   |       |       |       |       |       |       |       |       | uence |
   |       |       |       |       |       |       |       |       | Matc  |
   |       |       |       |       |       |       |       |       | hing. |
   +-------+-------+-------+-------+-------+-------+-------+-------+-------+
   | *>    |       |       |       |       |       |       |       |       |
   | >Incl |       |       |       |       |       |       |       |       |
   | ude*\ |       |       |       |       |       |       |       |       |
   |  `tab |       |       |       |       |       |       |       |       |
   | le_ti |       |       |       |       |       |       |       |       |
   | tle < |       |       |       |       |       |       |       |       |
   | #tabl |       |       |       |       |       |       |       |       |
   | e_CC. |       |       |       |       |       |       |       |       |
   | 2.5-2 |       |       |       |       |       |       |       |       |
   | d>`__ |       |       |       |       |       |       |       |       |
   +-------+-------+-------+-------+-------+-------+-------+-------+-------+
   | >F    | (     | 3/1   | Not   | O     | -/1   | O     | 1C    | Req   |
   | iller | 0040, |       | al    |       |       |       |       | uired |
   | Order | 2017) |       | lowed |       |       |       |       | if    |
   | Numb  |       |       |       |       |       |       |       | set.  |
   | er/Im |       |       |       |       |       |       |       |       |
   | aging |       |       |       |       |       |       |       |       |
   | Se    |       |       |       |       |       |       |       |       |
   | rvice |       |       |       |       |       |       |       |       |
   | Re    |       |       |       |       |       |       |       |       |
   | quest |       |       |       |       |       |       |       |       |
   +-------+-------+-------+-------+-------+-------+-------+-------+-------+
   | >     | (     | 2/2   | Not   | O     | -/2   | O     | 2     | The   |
   | Order | 0040, |       | al    |       |       |       |       | Order |
   | F     | 0027) |       | lowed |       |       |       |       | F     |
   | iller |       |       |       |       |       |       |       | iller |
   | Ident |       |       |       |       |       |       |       | Ident |
   | ifier |       |       |       |       |       |       |       | ifier |
   | Seq   |       |       |       |       |       |       |       | Seq   |
   | uence |       |       |       |       |       |       |       | uence |
   |       |       |       |       |       |       |       |       | shall |
   |       |       |       |       |       |       |       |       | only  |
   |       |       |       |       |       |       |       |       | be    |
   |       |       |       |       |       |       |       |       | retr  |
   |       |       |       |       |       |       |       |       | ieved |
   |       |       |       |       |       |       |       |       | with  |
   |       |       |       |       |       |       |       |       | Seq   |
   |       |       |       |       |       |       |       |       | uence |
   |       |       |       |       |       |       |       |       | Matc  |
   |       |       |       |       |       |       |       |       | hing. |
   +-------+-------+-------+-------+-------+-------+-------+-------+-------+
   | *>    |       |       |       |       |       |       |       |       |
   | >Incl |       |       |       |       |       |       |       |       |
   | ude*\ |       |       |       |       |       |       |       |       |
   |  `tab |       |       |       |       |       |       |       |       |
   | le_ti |       |       |       |       |       |       |       |       |
   | tle < |       |       |       |       |       |       |       |       |
   | #tabl |       |       |       |       |       |       |       |       |
   | e_CC. |       |       |       |       |       |       |       |       |
   | 2.5-2 |       |       |       |       |       |       |       |       |
   | d>`__ |       |       |       |       |       |       |       |       |
   +-------+-------+-------+-------+-------+-------+-------+-------+-------+
   | >Requ | (     | 2/2   | Not   | O     | -/2   | R     | 2     |       |
   | ested | 0040, |       | al    |       |       |       |       |       |
   | Proc  | 1001) |       | lowed |       |       |       |       |       |
   | edure |       |       |       |       |       |       |       |       |
   | ID    |       |       |       |       |       |       |       |       |
   +-------+-------+-------+-------+-------+-------+-------+-------+-------+
   | >Requ | (     | 2/2   | Not   | O     | -/2   | O     | 2     |       |
   | ested | 0032, |       | al    |       |       |       |       |       |
   | Proc  | 1060) |       | lowed |       |       |       |       |       |
   | edure |       |       |       |       |       |       |       |       |
   | D     |       |       |       |       |       |       |       |       |
   | escri |       |       |       |       |       |       |       |       |
   | ption |       |       |       |       |       |       |       |       |
   +-------+-------+-------+-------+-------+-------+-------+-------+-------+
   | >Requ | (     | 2/2   | Not   | O     | -/2   | O     | 2     |       |
   | ested | 0032, |       | al    |       |       |       |       |       |
   | Proc  | 1064) |       | lowed |       |       |       |       |       |
   | edure |       |       |       |       |       |       |       |       |
   | Code  |       |       |       |       |       |       |       |       |
   | Seq   |       |       |       |       |       |       |       |       |
   | uence |       |       |       |       |       |       |       |       |
   +-------+-------+-------+-------+-------+-------+-------+-------+-------+
   | *>    |       |       |       |       |       |       |       |       |
   | >Incl |       |       |       |       |       |       |       |       |
   | ude*\ |       |       |       |       |       |       |       |       |
   |  `tab |       |       |       |       |       |       |       |       |
   | le_ti |       |       |       |       |       |       |       |       |
   | tle < |       |       |       |       |       |       |       |       |
   | #tabl |       |       |       |       |       |       |       |       |
   | e_CC. |       |       |       |       |       |       |       |       |
   | 2.5-2 |       |       |       |       |       |       |       |       |
   | a>`__ |       |       |       |       |       |       |       |       |
   +-------+-------+-------+-------+-------+-------+-------+-------+-------+
   | >R    | (     | 3/3   | 3/3   | O     | -/3   | O     | 3     |       |
   | eason | 0040, |       |       |       |       |       |       |       |
   | for   | 1002) |       |       |       |       |       |       |       |
   | the   |       |       |       |       |       |       |       |       |
   | Requ  |       |       |       |       |       |       |       |       |
   | ested |       |       |       |       |       |       |       |       |
   | Proc  |       |       |       |       |       |       |       |       |
   | edure |       |       |       |       |       |       |       |       |
   +-------+-------+-------+-------+-------+-------+-------+-------+-------+
   | >R    | (     | 3/3   | 3/3   | O     | -/3   | O     | 3     |       |
   | eason | 0040, |       |       |       |       |       |       |       |
   | for   | 100A) |       |       |       |       |       |       |       |
   | Requ  |       |       |       |       |       |       |       |       |
   | ested |       |       |       |       |       |       |       |       |
   | Proc  |       |       |       |       |       |       |       |       |
   | edure |       |       |       |       |       |       |       |       |
   | Code  |       |       |       |       |       |       |       |       |
   | Seq   |       |       |       |       |       |       |       |       |
   | uence |       |       |       |       |       |       |       |       |
   +-------+-------+-------+-------+-------+-------+-------+-------+-------+
   | *>    |       |       |       |       |       |       |       |       |
   | >Incl |       |       |       |       |       |       |       |       |
   | ude*\ |       |       |       |       |       |       |       |       |
   |  `tab |       |       |       |       |       |       |       |       |
   | le_ti |       |       |       |       |       |       |       |       |
   | tle < |       |       |       |       |       |       |       |       |
   | #tabl |       |       |       |       |       |       |       |       |
   | e_CC. |       |       |       |       |       |       |       |       |
   | 2.5-2 |       |       |       |       |       |       |       |       |
   | a>`__ |       |       |       |       |       |       |       |       |
   +-------+-------+-------+-------+-------+-------+-------+-------+-------+
   | >Requ | (     | 3/3   | 3/3   | O     | -/3   | O     | 1C    | Req   |
   | ested | 0040, |       |       |       |       |       |       | uired |
   | Proc  | 1400) |       |       |       |       |       |       | if    |
   | edure |       |       |       |       |       |       |       | set.  |
   | Com   |       |       |       |       |       |       |       |       |
   | ments |       |       |       |       |       |       |       |       |
   +-------+-------+-------+-------+-------+-------+-------+-------+-------+
   | >     | (     | 3/3   | 3/3   | O     | -/3   | O     | 3     |       |
   | Confi | 0040, |       |       |       |       |       |       |       |
   | denti | 1008) |       |       |       |       |       |       |       |
   | ality |       |       |       |       |       |       |       |       |
   | Code  |       |       |       |       |       |       |       |       |
   +-------+-------+-------+-------+-------+-------+-------+-------+-------+
   | >     | (     | 3/3   | 3/3   | O     | -/3   | O     | 3     |       |
   | Names | 0040, |       |       |       |       |       |       |       |
   | of    | 1010) |       |       |       |       |       |       |       |
   | Int   |       |       |       |       |       |       |       |       |
   | ended |       |       |       |       |       |       |       |       |
   | Recip |       |       |       |       |       |       |       |       |
   | ients |       |       |       |       |       |       |       |       |
   | of    |       |       |       |       |       |       |       |       |
   | Re    |       |       |       |       |       |       |       |       |
   | sults |       |       |       |       |       |       |       |       |
   +-------+-------+-------+-------+-------+-------+-------+-------+-------+
   | >Im   | (     | 3/3   | 3/3   | O     | -/3   | O     | 3     |       |
   | aging | 0040, |       |       |       |       |       |       |       |
   | Se    | 2400) |       |       |       |       |       |       |       |
   | rvice |       |       |       |       |       |       |       |       |
   | Re    |       |       |       |       |       |       |       |       |
   | quest |       |       |       |       |       |       |       |       |
   | Com   |       |       |       |       |       |       |       |       |
   | ments |       |       |       |       |       |       |       |       |
   +-------+-------+-------+-------+-------+-------+-------+-------+-------+
   | >     | (     | 3/3   | 3/3   | O     | -/3   | O     | 3     |       |
   | Reque | 0032, |       |       |       |       |       |       |       |
   | sting | 1032) |       |       |       |       |       |       |       |
   | Phys  |       |       |       |       |       |       |       |       |
   | ician |       |       |       |       |       |       |       |       |
   +-------+-------+-------+-------+-------+-------+-------+-------+-------+
   | >     | (     | 3/1   | 3/1   | O     | -/3   | R     | 3     |       |
   | Reque | 0032, |       |       |       |       |       |       |       |
   | sting | 1033) |       |       |       |       |       |       |       |
   | Se    |       |       |       |       |       |       |       |       |
   | rvice |       |       |       |       |       |       |       |       |
   +-------+-------+-------+-------+-------+-------+-------+-------+-------+
   | >     | (     | 3/3   | 3/3   | O     | -/3   | O     | 3     |       |
   | Reque | 0032, |       |       |       |       |       |       |       |
   | sting | 1034) |       |       |       |       |       |       |       |
   | Se    |       |       |       |       |       |       |       |       |
   | rvice |       |       |       |       |       |       |       |       |
   | Code  |       |       |       |       |       |       |       |       |
   | Seq   |       |       |       |       |       |       |       |       |
   | uence |       |       |       |       |       |       |       |       |
   +-------+-------+-------+-------+-------+-------+-------+-------+-------+
   | *>    |       |       |       |       |       |       |       |       |
   | >Incl |       |       |       |       |       |       |       |       |
   | ude*\ |       |       |       |       |       |       |       |       |
   |  `tab |       |       |       |       |       |       |       |       |
   | le_ti |       |       |       |       |       |       |       |       |
   | tle < |       |       |       |       |       |       |       |       |
   | #tabl |       |       |       |       |       |       |       |       |
   | e_CC. |       |       |       |       |       |       |       |       |
   | 2.5-2 |       |       |       |       |       |       |       |       |
   | a>`__ |       |       |       |       |       |       |       |       |
   +-------+-------+-------+-------+-------+-------+-------+-------+-------+
   | >     | (     | 3/3   | 3/3   | O     | -/3   | O     | 3     |       |
   | Issue | 0040, |       |       |       |       |       |       |       |
   | Date  | 2004) |       |       |       |       |       |       |       |
   | of    |       |       |       |       |       |       |       |       |
   | Im    |       |       |       |       |       |       |       |       |
   | aging |       |       |       |       |       |       |       |       |
   | Se    |       |       |       |       |       |       |       |       |
   | rvice |       |       |       |       |       |       |       |       |
   | Re    |       |       |       |       |       |       |       |       |
   | quest |       |       |       |       |       |       |       |       |
   +-------+-------+-------+-------+-------+-------+-------+-------+-------+
   | >     | (     | 3/3   | 3/3   | O     | -/3   | O     | 3     |       |
   | Issue | 0040, |       |       |       |       |       |       |       |
   | Time  | 2005) |       |       |       |       |       |       |       |
   | of    |       |       |       |       |       |       |       |       |
   | Im    |       |       |       |       |       |       |       |       |
   | aging |       |       |       |       |       |       |       |       |
   | Se    |       |       |       |       |       |       |       |       |
   | rvice |       |       |       |       |       |       |       |       |
   | Re    |       |       |       |       |       |       |       |       |
   | quest |       |       |       |       |       |       |       |       |
   +-------+-------+-------+-------+-------+-------+-------+-------+-------+
   | >Refe | (     | 3/3   | 3/3   | O     | -/3   | O     | 3     |       |
   | rring | 0008, |       |       |       |       |       |       |       |
   | P     | 0090) |       |       |       |       |       |       |       |
   | hysic |       |       |       |       |       |       |       |       |
   | ian's |       |       |       |       |       |       |       |       |
   | Name  |       |       |       |       |       |       |       |       |
   +-------+-------+-------+-------+-------+-------+-------+-------+-------+
   | Rep   | (     | 1C/1C | Not   | O     | 3/2   | R     | 3     | Req   |
   | laced | 0074, |       | al    |       |       |       |       | uired |
   | Proc  | 1224) |       | lowed |       |       |       |       | if    |
   | edure |       |       |       |       |       |       |       | the   |
   | Step  |       |       |       |       |       |       |       | UPS   |
   | Seq   |       |       |       |       |       |       |       | rep   |
   | uence |       |       |       |       |       |       |       | laces |
   |       |       |       |       |       |       |       |       | an    |
   |       |       |       |       |       |       |       |       | other |
   |       |       |       |       |       |       |       |       | Proc  |
   |       |       |       |       |       |       |       |       | edure |
   |       |       |       |       |       |       |       |       | Step. |
   +-------+-------+-------+-------+-------+-------+-------+-------+-------+
   | *     |       |       |       |       |       |       |       |       |
   | >Incl |       |       |       |       |       |       |       |       |
   | ude*\ |       |       |       |       |       |       |       |       |
   |  `tab |       |       |       |       |       |       |       |       |
   | le_ti |       |       |       |       |       |       |       |       |
   | tle < |       |       |       |       |       |       |       |       |
   | #tabl |       |       |       |       |       |       |       |       |
   | e_CC. |       |       |       |       |       |       |       |       |
   | 2.5-2 |       |       |       |       |       |       |       |       |
   | f>`__ |       |       |       |       |       |       |       |       |
   +-------+-------+-------+-------+-------+-------+-------+-------+-------+
   | *All  |       | 3/3   | 3/3   | O     | 3/3   | -     | -     |       |
   | other |       |       |       |       |       |       |       |       |
   | Attri |       |       |       |       |       |       |       |       |
   | butes |       |       |       |       |       |       |       |       |
   | of    |       |       |       |       |       |       |       |       |
   | the   |       |       |       |       |       |       |       |       |
   | Un    |       |       |       |       |       |       |       |       |
   | ified |       |       |       |       |       |       |       |       |
   | Proc  |       |       |       |       |       |       |       |       |
   | edure |       |       |       |       |       |       |       |       |
   | Step  |       |       |       |       |       |       |       |       |
   | Re    |       |       |       |       |       |       |       |       |
   | latio |       |       |       |       |       |       |       |       |
   | nship |       |       |       |       |       |       |       |       |
   | Mo    |       |       |       |       |       |       |       |       |
   | dule* |       |       |       |       |       |       |       |       |
   +-------+-------+-------+-------+-------+-------+-------+-------+-------+
   | **Pa  |       |       |       |       |       |       |       |       |
   | tient |       |       |       |       |       |       |       |       |
   | D     |       |       |       |       |       |       |       |       |
   | emogr |       |       |       |       |       |       |       |       |
   | aphic |       |       |       |       |       |       |       |       |
   | Mod   |       |       |       |       |       |       |       |       |
   | ule** |       |       |       |       |       |       |       |       |
   +-------+-------+-------+-------+-------+-------+-------+-------+-------+
   | *All  |       | 3/3   | 3/3   | O     | 3/3   | -     | -     |       |
   | Attri |       |       |       |       |       |       |       |       |
   | butes |       |       |       |       |       |       |       |       |
   | of    |       |       |       |       |       |       |       |       |
   | the*  |       |       |       |       |       |       |       |       |
   +-------+-------+-------+-------+-------+-------+-------+-------+-------+
   | **Pa  |       |       |       |       |       |       |       |       |
   | tient |       |       |       |       |       |       |       |       |
   | Me    |       |       |       |       |       |       |       |       |
   | dical |       |       |       |       |       |       |       |       |
   | Mod   |       |       |       |       |       |       |       |       |
   | ule** |       |       |       |       |       |       |       |       |
   +-------+-------+-------+-------+-------+-------+-------+-------+-------+
   | Me    | (     | 3/2   | 3/2   | O     | 3/2   | O     | 2C    | Req   |
   | dical | 0010, |       |       |       |       |       |       | uired |
   | A     | 2000) |       |       |       |       |       |       | if    |
   | lerts |       |       |       |       |       |       |       | pre   |
   |       |       |       |       |       |       |       |       | sent. |
   +-------+-------+-------+-------+-------+-------+-------+-------+-------+
   | Preg  | (     | 3/2   | 3/2   | O     | 3/2   | O     | 2C    | Req   |
   | nancy | 0010, |       |       |       |       |       |       | uired |
   | S     | 21C0) |       |       |       |       |       |       | if    |
   | tatus |       |       |       |       |       |       |       | pre   |
   |       |       |       |       |       |       |       |       | sent. |
   +-------+-------+-------+-------+-------+-------+-------+-------+-------+
   | Sp    | (     | 3/2   | 3/2   | O     | 3/2   | O     | 2C    | Req   |
   | ecial | 0038, |       |       |       |       |       |       | uired |
   | Needs | 0050) |       |       |       |       |       |       | if    |
   |       |       |       |       |       |       |       |       | pre   |
   |       |       |       |       |       |       |       |       | sent. |
   +-------+-------+-------+-------+-------+-------+-------+-------+-------+
   | *All  |       | 3/3   | 3/3   | O     | 3/3   | O     | 3     |       |
   | other |       |       |       |       |       |       |       |       |
   | Attri |       |       |       |       |       |       |       |       |
   | butes |       |       |       |       |       |       |       |       |
   | of    |       |       |       |       |       |       |       |       |
   | the*  |       |       |       |       |       |       |       |       |
   +-------+-------+-------+-------+-------+-------+-------+-------+-------+
   | **    |       |       |       |       |       |       |       |       |
   | Visit |       |       |       |       |       |       |       |       |
   | Iden  |       |       |       |       |       |       |       |       |
   | tific |       |       |       |       |       |       |       |       |
   | ation |       |       |       |       |       |       |       |       |
   | Mod   |       |       |       |       |       |       |       |       |
   | ule** |       |       |       |       |       |       |       |       |
   +-------+-------+-------+-------+-------+-------+-------+-------+-------+
   | *All  |       | 3/3   | 3/3   | O     | 3/3   | -     | -     |       |
   | Attri |       |       |       |       |       |       |       |       |
   | butes |       |       |       |       |       |       |       |       |
   | of    |       |       |       |       |       |       |       |       |
   | the*  |       |       |       |       |       |       |       |       |
   +-------+-------+-------+-------+-------+-------+-------+-------+-------+
   | **    |       |       |       |       |       |       |       |       |
   | Visit |       |       |       |       |       |       |       |       |
   | S     |       |       |       |       |       |       |       |       |
   | tatus |       |       |       |       |       |       |       |       |
   | Mod   |       |       |       |       |       |       |       |       |
   | ule** |       |       |       |       |       |       |       |       |
   +-------+-------+-------+-------+-------+-------+-------+-------+-------+
   | *All  |       | 3/3   | 3/3   | O     | 3/3   | -     | -     |       |
   | Attri |       |       |       |       |       |       |       |       |
   | butes |       |       |       |       |       |       |       |       |
   | of    |       |       |       |       |       |       |       |       |
   | the*  |       |       |       |       |       |       |       |       |
   +-------+-------+-------+-------+-------+-------+-------+-------+-------+
   | **    |       |       |       |       |       |       |       |       |
   | Visit |       |       |       |       |       |       |       |       |
   | Admi  |       |       |       |       |       |       |       |       |
   | ssion |       |       |       |       |       |       |       |       |
   | Mod   |       |       |       |       |       |       |       |       |
   | ule** |       |       |       |       |       |       |       |       |
   +-------+-------+-------+-------+-------+-------+-------+-------+-------+
   | *All  |       | 3/3   | 3/3   | O     | 3/3   | -     | -     |       |
   | Attri |       |       |       |       |       |       |       |       |
   | butes |       |       |       |       |       |       |       |       |
   | of    |       |       |       |       |       |       |       |       |
   | the*  |       |       |       |       |       |       |       |       |
   +-------+-------+-------+-------+-------+-------+-------+-------+-------+
   | **Un  |       |       |       |       |       |       |       |       |
   | ified |       |       |       |       |       |       |       |       |
   | Proc  |       |       |       |       |       |       |       |       |
   | edure |       |       |       |       |       |       |       |       |
   | Step  |       |       |       |       |       |       |       |       |
   | Pro   |       |       |       |       |       |       |       |       |
   | gress |       |       |       |       |       |       |       |       |
   | I     |       |       |       |       |       |       |       |       |
   | nform |       |       |       |       |       |       |       |       |
   | ation |       |       |       |       |       |       |       |       |
   | Mod   |       |       |       |       |       |       |       |       |
   | ule** |       |       |       |       |       |       |       |       |
   +-------+-------+-------+-------+-------+-------+-------+-------+-------+
   | Proc  | (     | 1/1   | Not   | R     | 3/1   | R     | 1     | Proc  |
   | edure | 0074, |       | All   |       |       |       |       | edure |
   | Step  | 1000) | Shall | owed. |       |       |       |       | Step  |
   | State |       | be    |       |       |       |       |       | State |
   |       |       | cr    | Use   |       |       |       |       | shall |
   |       |       | eated | N-A   |       |       |       |       | be    |
   |       |       | with  | CTION |       |       |       |       | retr  |
   |       |       | a     |       |       |       |       |       | ieved |
   |       |       | value |       |       |       |       |       | with  |
   |       |       | of    |       |       |       |       |       | S     |
   |       |       | "     |       |       |       |       |       | ingle |
   |       |       | SCHED |       |       |       |       |       | Value |
   |       |       | ULED" |       |       |       |       |       | Mat   |
   |       |       |       |       |       |       |       |       | ching |
   +-------+-------+-------+-------+-------+-------+-------+-------+-------+
   | Pro   | (     | 2/2   | 3/2   | X     | 3/2   |       | 2     |       |
   | gress | 0074, |       |       |       |       |       |       |       |
   | I     | 1002) | Shall |       |       |       |       |       |       |
   | nform |       | be    |       |       |       |       |       |       |
   | ation |       | empty |       |       |       |       |       |       |
   | Seq   |       |       |       |       |       |       |       |       |
   | uence |       |       |       |       |       |       |       |       |
   +-------+-------+-------+-------+-------+-------+-------+-------+-------+
   | >Proc | (     | Not   | 3/1   | O     | -/1   | -     | -     |       |
   | edure | 0074, | Al    |       |       |       |       |       |       |
   | Step  | 1004) | lowed |       |       |       |       |       |       |
   | Pro   |       |       |       |       |       |       |       |       |
   | gress |       |       |       |       |       |       |       |       |
   +-------+-------+-------+-------+-------+-------+-------+-------+-------+
   | >Proc | (     | Not   | 3/1   | O     | -/1   | -     | -     |       |
   | edure | 0074, | Al    |       |       |       |       |       |       |
   | Step  | 1006) | lowed |       |       |       |       |       |       |
   | Pro   |       |       |       |       |       |       |       |       |
   | gress |       |       |       |       |       |       |       |       |
   | D     |       |       |       |       |       |       |       |       |
   | escri |       |       |       |       |       |       |       |       |
   | ption |       |       |       |       |       |       |       |       |
   +-------+-------+-------+-------+-------+-------+-------+-------+-------+
   | >Proc | (     | Not   | 3/3   | O     | -/3   |       |       |       |
   | edure | 0074, | Al    |       |       |       |       |       |       |
   | Step  | 1007) | lowed |       |       |       |       |       |       |
   | Pro   |       |       |       |       |       |       |       |       |
   | gress |       |       |       |       |       |       |       |       |
   | Param |       |       |       |       |       |       |       |       |
   | eters |       |       |       |       |       |       |       |       |
   | Seq   |       |       |       |       |       |       |       |       |
   | uence |       |       |       |       |       |       |       |       |
   +-------+-------+-------+-------+-------+-------+-------+-------+-------+
   | *>    |       |       |       |       |       |       |       |       |
   | >Incl |       |       |       |       |       |       |       |       |
   | ude*\ |       |       |       |       |       |       |       |       |
   |  `tab |       |       |       |       |       |       |       |       |
   | le_ti |       |       |       |       |       |       |       |       |
   | tle < |       |       |       |       |       |       |       |       |
   | #tabl |       |       |       |       |       |       |       |       |
   | e_CC. |       |       |       |       |       |       |       |       |
   | 2.5-2 |       |       |       |       |       |       |       |       |
   | b>`__ |       |       |       |       |       |       |       |       |
   +-------+-------+-------+-------+-------+-------+-------+-------+-------+
   | >>Co  | (     | Not   | 3/3   | O     | -/3   |       |       |       |
   | ntent | 0040, | Al    |       |       |       |       |       |       |
   | Item  | 0441) | lowed |       |       |       |       |       |       |
   | Mod   |       |       |       |       |       |       |       |       |
   | ifier |       |       |       |       |       |       |       |       |
   | Seq   |       |       |       |       |       |       |       |       |
   | uence |       |       |       |       |       |       |       |       |
   +-------+-------+-------+-------+-------+-------+-------+-------+-------+
   | *>>   |       |       |       |       |       |       |       |       |
   | >Incl |       |       |       |       |       |       |       |       |
   | ude*\ |       |       |       |       |       |       |       |       |
   |  `tab |       |       |       |       |       |       |       |       |
   | le_ti |       |       |       |       |       |       |       |       |
   | tle < |       |       |       |       |       |       |       |       |
   | #tabl |       |       |       |       |       |       |       |       |
   | e_CC. |       |       |       |       |       |       |       |       |
   | 2.5-2 |       |       |       |       |       |       |       |       |
   | b>`__ |       |       |       |       |       |       |       |       |
   +-------+-------+-------+-------+-------+-------+-------+-------+-------+
   | >Proc | (     | Not   | 3/1   | O     | -/1   | -     | -     |       |
   | edure | 0074, | Al    |       |       |       |       |       |       |
   | Step  | 1008) | lowed |       |       |       |       |       |       |
   | Comm  |       |       |       |       |       |       |       |       |
   | unica |       |       |       |       |       |       |       |       |
   | tions |       |       |       |       |       |       |       |       |
   | URI   |       |       |       |       |       |       |       |       |
   | Seq   |       |       |       |       |       |       |       |       |
   | uence |       |       |       |       |       |       |       |       |
   +-------+-------+-------+-------+-------+-------+-------+-------+-------+
   | >>Co  | (     | Not   | 1/1   | O     | -/1   | -     | -     |       |
   | ntact | 0074, | Al    |       |       |       |       |       |       |
   | URI   | 100a) | lowed |       |       |       |       |       |       |
   +-------+-------+-------+-------+-------+-------+-------+-------+-------+
   | >>Co  | (     | Not   | 3/1   | O     | -/1   | -     | -     |       |
   | ntact | 0074, | Al    |       |       |       |       |       |       |
   | Di    | 100c) | lowed |       |       |       |       |       |       |
   | splay |       |       |       |       |       |       |       |       |
   | Name  |       |       |       |       |       |       |       |       |
   +-------+-------+-------+-------+-------+-------+-------+-------+-------+
   | >Proc | (     | Not   | 3/1   | X     | -/1   | -     | -     | If    |
   | edure | 0040, | Al    |       |       |       |       |       | cha   |
   | Step  | 4052) | lowed |       |       |       |       |       | nging |
   | Ca    |       |       |       |       |       |       |       | the   |
   | ncell |       |       |       |       |       |       |       | UPS   |
   | ation |       |       |       |       |       |       |       | State |
   | Dat   |       |       |       |       |       |       |       | (     |
   | eTime |       |       |       |       |       |       |       | 0074, |
   |       |       |       |       |       |       |       |       | 1000) |
   |       |       |       |       |       |       |       |       | to    |
   |       |       |       |       |       |       |       |       | CAN   |
   |       |       |       |       |       |       |       |       | CELED |
   |       |       |       |       |       |       |       |       | and   |
   |       |       |       |       |       |       |       |       | this  |
   |       |       |       |       |       |       |       |       | Attr  |
   |       |       |       |       |       |       |       |       | ibute |
   |       |       |       |       |       |       |       |       | has   |
   |       |       |       |       |       |       |       |       | no    |
   |       |       |       |       |       |       |       |       | v     |
   |       |       |       |       |       |       |       |       | alue, |
   |       |       |       |       |       |       |       |       | the   |
   |       |       |       |       |       |       |       |       | SCP   |
   |       |       |       |       |       |       |       |       | shall |
   |       |       |       |       |       |       |       |       | fill  |
   |       |       |       |       |       |       |       |       | it    |
   |       |       |       |       |       |       |       |       | with  |
   |       |       |       |       |       |       |       |       | the   |
   |       |       |       |       |       |       |       |       | cu    |
   |       |       |       |       |       |       |       |       | rrent |
   |       |       |       |       |       |       |       |       | date  |
   |       |       |       |       |       |       |       |       | time. |
   +-------+-------+-------+-------+-------+-------+-------+-------+-------+
   | >R    | (     | Not   | 3/1   | O     | -/1   | -     | -     |       |
   | eason | 0074, | Al    |       |       |       |       |       |       |
   | For   | 1238) | lowed |       |       |       |       |       |       |
   | Ca    |       |       |       |       |       |       |       |       |
   | ncell |       |       |       |       |       |       |       |       |
   | ation |       |       |       |       |       |       |       |       |
   +-------+-------+-------+-------+-------+-------+-------+-------+-------+
   | >Proc | (     | Not   | 3/1   | X     | -/1   |       |       |       |
   | edure | 0074, | Al    |       |       |       |       |       |       |
   | Step  | 100e) | lowed |       |       |       |       |       |       |
   | Disco |       |       |       |       |       |       |       |       |
   | ntinu |       |       |       |       |       |       |       |       |
   | ation |       |       |       |       |       |       |       |       |
   | R     |       |       |       |       |       |       |       |       |
   | eason |       |       |       |       |       |       |       |       |
   | Code  |       |       |       |       |       |       |       |       |
   | Seq   |       |       |       |       |       |       |       |       |
   | uence |       |       |       |       |       |       |       |       |
   +-------+-------+-------+-------+-------+-------+-------+-------+-------+
   | *>    |       |       |       |       |       |       |       |       |
   | >Incl |       |       |       |       |       |       |       |       |
   | ude*\ |       |       |       |       |       |       |       |       |
   |  `tab |       |       |       |       |       |       |       |       |
   | le_ti |       |       |       |       |       |       |       |       |
   | tle < |       |       |       |       |       |       |       |       |
   | #tabl |       |       |       |       |       |       |       |       |
   | e_CC. |       |       |       |       |       |       |       |       |
   | 2.5-2 |       |       |       |       |       |       |       |       |
   | a>`__ |       |       |       |       |       |       |       |       |
   +-------+-------+-------+-------+-------+-------+-------+-------+-------+
   | **Un  |       |       |       |       |       |       |       |       |
   | ified |       |       |       |       |       |       |       |       |
   | Proc  |       |       |       |       |       |       |       |       |
   | edure |       |       |       |       |       |       |       |       |
   | Step  |       |       |       |       |       |       |       |       |
   | Perf  |       |       |       |       |       |       |       |       |
   | ormed |       |       |       |       |       |       |       |       |
   | Proc  |       |       |       |       |       |       |       |       |
   | edure |       |       |       |       |       |       |       |       |
   | I     |       |       |       |       |       |       |       |       |
   | nform |       |       |       |       |       |       |       |       |
   | ation |       |       |       |       |       |       |       |       |
   | Mod   |       |       |       |       |       |       |       |       |
   | ule** |       |       |       |       |       |       |       |       |
   +-------+-------+-------+-------+-------+-------+-------+-------+-------+
   | Un    | (     | 2/2   | 3/2   | P     | 3/2   | -     | -     | See   |
   | ified | 0074, |       |       |       |       |       |       | `Un   |
   | Proc  | 1216) | Shall |       |       |       |       |       | ified |
   | edure |       | be    |       |       |       |       |       | Proc  |
   | Step  |       | cr    |       |       |       |       |       | edure |
   | Perf  |       | eated |       |       |       |       |       | Step  |
   | ormed |       | empty |       |       |       |       |       | Perf  |
   | Proc  |       |       |       |       |       |       |       | ormed |
   | edure |       |       |       |       |       |       |       | Proc  |
   | Seq   |       |       |       |       |       |       |       | edure |
   | uence |       |       |       |       |       |       |       | Seq   |
   |       |       |       |       |       |       |       |       | uence |
   |       |       |       |       |       |       |       |       |  <#se |
   |       |       |       |       |       |       |       |       | ct_CC |
   |       |       |       |       |       |       |       |       | .2.5. |
   |       |       |       |       |       |       |       |       | 1.3.2 |
   |       |       |       |       |       |       |       |       | >`__. |
   +-------+-------+-------+-------+-------+-------+-------+-------+-------+
   | >A    | (     | Not   | 3/1   | RC    | -/1   | O     | 1C    | Shall |
   | ctual | 0040, | Al    |       |       |       |       |       | be    |
   | Human | 4035) | lowed |       |       |       |       |       | pro   |
   | Perfo |       |       |       |       |       |       |       | vided |
   | rmers |       |       |       |       |       |       |       | if    |
   | Seq   |       |       |       |       |       |       |       | k     |
   | uence |       |       |       |       |       |       |       | nown. |
   |       |       |       |       |       |       |       |       |       |
   |       |       |       |       |       |       |       |       | R     |
   |       |       |       |       |       |       |       |       | eturn |
   |       |       |       |       |       |       |       |       | Key   |
   |       |       |       |       |       |       |       |       | req   |
   |       |       |       |       |       |       |       |       | uired |
   |       |       |       |       |       |       |       |       | if    |
   |       |       |       |       |       |       |       |       | set.  |
   |       |       |       |       |       |       |       |       |       |
   |       |       |       |       |       |       |       |       | The   |
   |       |       |       |       |       |       |       |       | Attri |
   |       |       |       |       |       |       |       |       | butes |
   |       |       |       |       |       |       |       |       | of    |
   |       |       |       |       |       |       |       |       | the   |
   |       |       |       |       |       |       |       |       | A     |
   |       |       |       |       |       |       |       |       | ctual |
   |       |       |       |       |       |       |       |       | Human |
   |       |       |       |       |       |       |       |       | Perfo |
   |       |       |       |       |       |       |       |       | rmers |
   |       |       |       |       |       |       |       |       | Seq   |
   |       |       |       |       |       |       |       |       | uence |
   |       |       |       |       |       |       |       |       | shall |
   |       |       |       |       |       |       |       |       | only  |
   |       |       |       |       |       |       |       |       | be    |
   |       |       |       |       |       |       |       |       | retr  |
   |       |       |       |       |       |       |       |       | ieved |
   |       |       |       |       |       |       |       |       | with  |
   |       |       |       |       |       |       |       |       | Seq   |
   |       |       |       |       |       |       |       |       | uence |
   |       |       |       |       |       |       |       |       | Matc  |
   |       |       |       |       |       |       |       |       | hing. |
   +-------+-------+-------+-------+-------+-------+-------+-------+-------+
   | >>    | (     | Not   | 3/1   | RC    | -/1   | -     | -     | Shall |
   | Human | 0040, | Al    |       |       |       |       |       | be    |
   | Perf  | 4009) | lowed |       |       |       |       |       | pro   |
   | ormer |       |       |       |       |       |       |       | vided |
   | Code  |       |       |       |       |       |       |       | if    |
   | Seq   |       |       |       |       |       |       |       | k     |
   | uence |       |       |       |       |       |       |       | nown. |
   +-------+-------+-------+-------+-------+-------+-------+-------+-------+
   | *>>   |       |       |       |       |       |       |       |       |
   | >Incl |       |       |       |       |       |       |       |       |
   | ude*\ |       |       |       |       |       |       |       |       |
   |  `tab |       |       |       |       |       |       |       |       |
   | le_ti |       |       |       |       |       |       |       |       |
   | tle < |       |       |       |       |       |       |       |       |
   | #tabl |       |       |       |       |       |       |       |       |
   | e_CC. |       |       |       |       |       |       |       |       |
   | 2.5-2 |       |       |       |       |       |       |       |       |
   | a>`__ |       |       |       |       |       |       |       |       |
   +-------+-------+-------+-------+-------+-------+-------+-------+-------+
   | >>    | (     | Not   | 3/1   | RC    | -/1   | -     | -     | Shall |
   | Human | 0040, | Al    |       |       |       |       |       | be    |
   | P     | 4037) | lowed |       |       |       |       |       | pro   |
   | erfor |       |       |       |       |       |       |       | vided |
   | mer's |       |       |       |       |       |       |       | if    |
   | Name  |       |       |       |       |       |       |       | known |
   +-------+-------+-------+-------+-------+-------+-------+-------+-------+
   | >>    | (     | Not   | 3/1   | O     | -/1   | -     | -     |       |
   | Human | 0040, | Al    |       |       |       |       |       |       |
   | P     | 4036) | lowed |       |       |       |       |       |       |
   | erfor |       |       |       |       |       |       |       |       |
   | mer's |       |       |       |       |       |       |       |       |
   | Or    |       |       |       |       |       |       |       |       |
   | ganiz |       |       |       |       |       |       |       |       |
   | ation |       |       |       |       |       |       |       |       |
   +-------+-------+-------+-------+-------+-------+-------+-------+-------+
   | >Perf | (     | Not   | 3/2   | P     | -/2   | O     | 3     |       |
   | ormed | 0040, | Al    |       |       |       |       |       |       |
   | St    | 4028) | lowed |       |       |       |       |       |       |
   | ation |       |       |       |       |       |       |       |       |
   | Name  |       |       |       |       |       |       |       |       |
   | Code  |       |       |       |       |       |       |       |       |
   | Seq   |       |       |       |       |       |       |       |       |
   | uence |       |       |       |       |       |       |       |       |
   +-------+-------+-------+-------+-------+-------+-------+-------+-------+
   | *>    |       |       |       |       |       |       |       |       |
   | >Incl |       |       |       |       |       |       |       |       |
   | ude*\ |       |       |       |       |       |       |       |       |
   |  `tab |       |       |       |       |       |       |       |       |
   | le_ti |       |       |       |       |       |       |       |       |
   | tle < |       |       |       |       |       |       |       |       |
   | #tabl |       |       |       |       |       |       |       |       |
   | e_CC. |       |       |       |       |       |       |       |       |
   | 2.5-2 |       |       |       |       |       |       |       |       |
   | a>`__ |       |       |       |       |       |       |       |       |
   +-------+-------+-------+-------+-------+-------+-------+-------+-------+
   | >Perf | (     | Not   | 3/2   | O     | -/2   | -     | -     |       |
   | ormed | 0040, | Al    |       |       |       |       |       |       |
   | St    | 4029) | lowed |       |       |       |       |       |       |
   | ation |       |       |       |       |       |       |       |       |
   | Class |       |       |       |       |       |       |       |       |
   | Code  |       |       |       |       |       |       |       |       |
   | Seq   |       |       |       |       |       |       |       |       |
   | uence |       |       |       |       |       |       |       |       |
   +-------+-------+-------+-------+-------+-------+-------+-------+-------+
   | *>    |       |       |       |       |       |       |       |       |
   | >Incl |       |       |       |       |       |       |       |       |
   | ude*\ |       |       |       |       |       |       |       |       |
   |  `tab |       |       |       |       |       |       |       |       |
   | le_ti |       |       |       |       |       |       |       |       |
   | tle < |       |       |       |       |       |       |       |       |
   | #tabl |       |       |       |       |       |       |       |       |
   | e_CC. |       |       |       |       |       |       |       |       |
   | 2.5-2 |       |       |       |       |       |       |       |       |
   | a>`__ |       |       |       |       |       |       |       |       |
   +-------+-------+-------+-------+-------+-------+-------+-------+-------+
   | >Perf | (     | Not   | 3/2   | O     | -/2   | -     | -     |       |
   | ormed | 0040, | Al    |       |       |       |       |       |       |
   | St    | 4030) | lowed |       |       |       |       |       |       |
   | ation |       |       |       |       |       |       |       |       |
   | Geogr |       |       |       |       |       |       |       |       |
   | aphic |       |       |       |       |       |       |       |       |
   | Loc   |       |       |       |       |       |       |       |       |
   | ation |       |       |       |       |       |       |       |       |
   | Code  |       |       |       |       |       |       |       |       |
   | Seq   |       |       |       |       |       |       |       |       |
   | uence |       |       |       |       |       |       |       |       |
   +-------+-------+-------+-------+-------+-------+-------+-------+-------+
   | *>    |       |       |       |       |       |       |       |       |
   | >Incl |       |       |       |       |       |       |       |       |
   | ude*\ |       |       |       |       |       |       |       |       |
   |  `tab |       |       |       |       |       |       |       |       |
   | le_ti |       |       |       |       |       |       |       |       |
   | tle < |       |       |       |       |       |       |       |       |
   | #tabl |       |       |       |       |       |       |       |       |
   | e_CC. |       |       |       |       |       |       |       |       |
   | 2.5-2 |       |       |       |       |       |       |       |       |
   | a>`__ |       |       |       |       |       |       |       |       |
   +-------+-------+-------+-------+-------+-------+-------+-------+-------+
   | >Perf | (     | Not   | 3/1   | P     | -/1   | -     | -     |       |
   | ormed | 0040, | Al    |       |       |       |       |       |       |
   | Proc  | 4050) | lowed |       |       |       |       |       |       |
   | edure |       |       |       |       |       |       |       |       |
   | Step  |       |       |       |       |       |       |       |       |
   | Start |       |       |       |       |       |       |       |       |
   | Dat   |       |       |       |       |       |       |       |       |
   | eTime |       |       |       |       |       |       |       |       |
   +-------+-------+-------+-------+-------+-------+-------+-------+-------+
   | >Perf | (     | Not   | 3/1   | O     | -/1   | -     | -     |       |
   | ormed | 0040, | Al    |       |       |       |       |       |       |
   | Proc  | 0254) | lowed |       |       |       |       |       |       |
   | edure |       |       |       |       |       |       |       |       |
   | Step  |       |       |       |       |       |       |       |       |
   | D     |       |       |       |       |       |       |       |       |
   | escri |       |       |       |       |       |       |       |       |
   | ption |       |       |       |       |       |       |       |       |
   +-------+-------+-------+-------+-------+-------+-------+-------+-------+
   | >Com  | (     | Not   | 3/1   | O     | -/1   | -     | -     |       |
   | ments | 0040, | Al    |       |       |       |       |       |       |
   | on    | 0280) | lowed |       |       |       |       |       |       |
   | the   |       |       |       |       |       |       |       |       |
   | Perf  |       |       |       |       |       |       |       |       |
   | ormed |       |       |       |       |       |       |       |       |
   | Proc  |       |       |       |       |       |       |       |       |
   | edure |       |       |       |       |       |       |       |       |
   | Step  |       |       |       |       |       |       |       |       |
   +-------+-------+-------+-------+-------+-------+-------+-------+-------+
   | >Perf | (     | Not   | 3/1   | P     | -/1   | -     | -     |       |
   | ormed | 0040, | Al    |       |       |       |       |       |       |
   | Wor   | 4019) | lowed |       |       |       |       |       |       |
   | kitem |       |       |       |       |       |       |       |       |
   | Code  |       |       |       |       |       |       |       |       |
   | Seq   |       |       |       |       |       |       |       |       |
   | uence |       |       |       |       |       |       |       |       |
   +-------+-------+-------+-------+-------+-------+-------+-------+-------+
   | *>    |       |       |       |       |       |       |       |       |
   | >Incl |       |       |       |       |       |       |       |       |
   | ude*\ |       |       |       |       |       |       |       |       |
   |  `tab |       |       |       |       |       |       |       |       |
   | le_ti |       |       |       |       |       |       |       |       |
   | tle < |       |       |       |       |       |       |       |       |
   | #tabl |       |       |       |       |       |       |       |       |
   | e_CC. |       |       |       |       |       |       |       |       |
   | 2.5-2 |       |       |       |       |       |       |       |       |
   | a>`__ |       |       |       |       |       |       |       |       |
   +-------+-------+-------+-------+-------+-------+-------+-------+-------+
   | >Perf | (     | Not   | 3/1   | O     | -/1   | -     | -     |       |
   | ormed | 0074, | Al    |       |       |       |       |       |       |
   | Proce | 1212) | lowed |       |       |       |       |       |       |
   | ssing |       |       |       |       |       |       |       |       |
   | Param |       |       |       |       |       |       |       |       |
   | eters |       |       |       |       |       |       |       |       |
   | Seq   |       |       |       |       |       |       |       |       |
   | uence |       |       |       |       |       |       |       |       |
   +-------+-------+-------+-------+-------+-------+-------+-------+-------+
   | *>    |       |       |       |       |       |       |       |       |
   | >Incl |       |       |       |       |       |       |       |       |
   | ude*\ |       |       |       |       |       |       |       |       |
   |  `tab |       |       |       |       |       |       |       |       |
   | le_ti |       |       |       |       |       |       |       |       |
   | tle < |       |       |       |       |       |       |       |       |
   | #tabl |       |       |       |       |       |       |       |       |
   | e_CC. |       |       |       |       |       |       |       |       |
   | 2.5-2 |       |       |       |       |       |       |       |       |
   | b>`__ |       |       |       |       |       |       |       |       |
   +-------+-------+-------+-------+-------+-------+-------+-------+-------+
   | >Perf | (     | Not   | 3/1   | P     | -/1   | O     | 1C    | Req   |
   | ormed | 0040, | Al    |       |       |       |       |       | uired |
   | Proc  | 4051) | lowed |       |       |       |       |       | if    |
   | edure |       |       |       |       |       |       |       | set.  |
   | Step  |       |       |       |       |       |       |       |       |
   | End   |       |       |       |       |       |       |       |       |
   | Dat   |       |       |       |       |       |       |       |       |
   | eTime |       |       |       |       |       |       |       |       |
   +-------+-------+-------+-------+-------+-------+-------+-------+-------+
   | >O    | (     | Not   | 2/2   | P     | -/2   | -     | -     | If    |
   | utput | 0040, | Al    |       |       |       |       |       | there |
   | I     | 4033) | lowed |       |       |       |       |       | are   |
   | nform |       |       |       |       |       |       |       | no    |
   | ation |       |       |       |       |       |       |       | rel   |
   | Seq   |       |       |       |       |       |       |       | evant |
   | uence |       |       |       |       |       |       |       | o     |
   |       |       |       |       |       |       |       |       | utput |
   |       |       |       |       |       |       |       |       | obj   |
   |       |       |       |       |       |       |       |       | ects, |
   |       |       |       |       |       |       |       |       | then  |
   |       |       |       |       |       |       |       |       | this  |
   |       |       |       |       |       |       |       |       | seq   |
   |       |       |       |       |       |       |       |       | uence |
   |       |       |       |       |       |       |       |       | may   |
   |       |       |       |       |       |       |       |       | have  |
   |       |       |       |       |       |       |       |       | no    |
   |       |       |       |       |       |       |       |       | i     |
   |       |       |       |       |       |       |       |       | tems. |
   +-------+-------+-------+-------+-------+-------+-------+-------+-------+
   | *     |       |       |       |       |       |       |       |       |
   | >Incl |       |       |       |       |       |       |       |       |
   | ude*\ |       |       |       |       |       |       |       |       |
   |  `tab |       |       |       |       |       |       |       |       |
   | le_ti |       |       |       |       |       |       |       |       |
   | tle < |       |       |       |       |       |       |       |       |
   | #tabl |       |       |       |       |       |       |       |       |
   | e_CC. |       |       |       |       |       |       |       |       |
   | 2.5-2 |       |       |       |       |       |       |       |       |
   | c>`__ |       |       |       |       |       |       |       |       |
   +-------+-------+-------+-------+-------+-------+-------+-------+-------+

.. _sect_CC.2.5.1.3.1:

UPS SOP Class UID
                 

The SOP Class UID shall be set to 1.2.840.10008.5.1.4.34.6.1 by SCP

.. _sect_CC.2.5.1.3.2:

Unified Procedure Step Performed Procedure Sequence
                                                   

The Attributes of the UPS Performed Procedure Sequence shall only be
retrieved with Sequence Matching.

.. note::

   Since this Attribute may be created empty and has a Final State
   requirement of X, a UPS in the SCHEDULED state may be canceled with
   two N-ACTIONS (IN PROGRESS then CANCELED) and no N-SETs.

.. _sect_CC.2.5.2:

Service Class User Behavior
^^^^^^^^^^^^^^^^^^^^^^^^^^^

An SCU uses N-CREATE to request the SCP schedule a new UPS.

The SCU shall specify in the N-CREATE request primitive the UPS Push SOP
Class UID and the SOP Instance UID for the UPS that is to be created and
for which Attribute Values are to be provided. See `Service Class and
SOP Class UIDs <#sect_CC.3.1>`__ for further discussion of UPS SOP Class
UIDs.

The SCU shall provide Attribute Values in the N-CREATE request primitive
for all required UPS Attributes as specified in
`table_title <#table_CC.2.5-3>`__. Additionally, values may be provided
for optional Attributes as specified in
`table_title <#table_CC.2.5-3>`__.

The SCU shall specify a value of "SCHEDULED" for the Attribute Procedure
Step State (0074,1000) in the N-CREATE request primitive.

.. _sect_CC.2.5.3:

Service Class Provider Behavior
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

The SCP shall create and maintain UPS instances as instructed by
creation requests and as specified by `table_title <#table_CC.2.5-3>`__.

The SCP shall return, via the N-CREATE response primitive, the N-CREATE
Response Status Code applicable to the associated request.

The SCP shall accept creation requests only if the value of the
Procedure Step State (0074,1000) Attribute is "SCHEDULED". If the
Procedure Step State Attribute has another value, the SCP shall fail the
request.

The SCP may modify Attributes of a UPS instance, e.g., to correct
invalid Attribute Values. A description of the modifications the SCP may
perform shall be documented in the conformance statement of the SCP.

The SCP may also create and maintain UPS instances without receiving a
UPS instance N-CREATE request, e.g., based on internal logic, operator
inputs or HL7 messages. The contents of the instance created by the SCP
must still comply with the N-CREATE requirements in
`table_title <#table_CC.2.5-3>`__.

Upon creating a new UPS Instance, the SCP shall update UPS Subscription
Status of the Instance for each AE with a Global Subscription as
described in `Subscribe/Unsubscribe to Receive UPS Event Reports
(N-ACTION) <#sect_CC.2.3>`__. Optionally, the SCP may create a UPS
Subscription for the N-CREATE SCU AE; such behavior shall be documented
in the Conformance Statement.

Upon creating a new UPS Instance, the SCP shall send UPS State Reports
(if it supports the UPS Event SOP Class) as described in `Service Class
Provider Behavior <#sect_CC.2.4.3>`__ regardless of whether the creation
was based on an N-CREATE or on internal logic.

Bi-directional Authentication of machines/users/applications is possible
at association time (see and ). provides a "Refused: Refused: Not
authorized" error code. There are no specific requirements to perform
authorization.

.. _sect_CC.2.5.4:

Status Codes
^^^^^^^^^^^^

`table_title <#table_CC.2.5-4>`__ defines the status code values that
might be returned in a N-CREATE response. General status code values and
fields related to status code values are defined for N-CREATE DIMSE
Service in .

.. table:: N-CREATE Response Status Values [for Create a Unified
Procedure Step]

   +----------------+-------------------------------------+-------------+
   | Service Status | Further Meaning                     | Status Code |
   +================+=====================================+=============+
   | Success        | The UPS was created as requested    | 0000        |
   +----------------+-------------------------------------+-------------+
   | Warning        | The UPS was created with            | B300        |
   |                | modifications                       |             |
   +----------------+-------------------------------------+-------------+
   | Failure        | Failed: The provided value of UPS   | C309        |
   |                | State was not "SCHEDULED".          |             |
   +----------------+-------------------------------------+-------------+

.. _sect_CC.2.6:

Set Unified Procedure Step Information (N-SET)
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

This operation allows an SCU to set Attribute Values of a UPS Instance
and provide information about a specific real-world UPS that is under
control of the SCU. This operation shall be invoked by the SCU through
the DIMSE N-SET Service.

.. _sect_CC.2.6.1:

Unified Procedure Step IOD Subset Specification
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

The Application Entity that claims conformance to the UPS Pull SOP Class
as an SCU may choose to modify a subset of the Attributes maintained by
the SCP. The Application Entity that claims conformance as an SCP to the
UPS Pull SOP Class shall support Attributes specified in
`table_title <#table_CC.2.5-3>`__

.. _sect_CC.2.6.2:

Service Class User Behavior
^^^^^^^^^^^^^^^^^^^^^^^^^^^

The SCU shall specify in the N-SET request primitive the UID of the UPS
Instance for which it wants to set Attribute Values. Since all UPSs are
created as instances of the UPS Push SOP Class, the Requested SOP Class
UID in the N-SET request shall be the UID of the UPS Push SOP Class. See
`Service Class and SOP Class UIDs <#sect_CC.3.1>`__ for further details.

To N-SET a UPS instance currently in the SCHEDULED state, the
Transaction UID Attribute shall not be present in the request. For a UPS
instance in the IN PROGRESS state, the SCU shall provide the current
Transaction UID (0008,1195) as an Attribute.

The SCU shall be permitted to set Attribute Values as specified in
`table_title <#table_CC.2.5-3>`__. The SCU shall specify the list of
Attributes for which it wants to set the Attribute Values. The SCU shall
provide, with one or more N-SET request primitives, the Attribute Values
specified in `table_title <#table_CC.2.5-3>`__.

When modifying a sequence, the SCU shall include in the N-SET request
all Items in the sequence, not just the Items to be modified.

N-SET requests shall be atomic (indivisible) and idempotent (repeat
executions have no additional effect). Since it is possible for an N-GET
to occur between two N-SET requests, any given N-SET shall leave the UPS
instance in an internally consistent state (i.e., when multiple
Attributes need updating as a group, do this as multiple Attributes in a
single N-SET request, not as multiple N-SET requests)

The SCU shall not set the value of the Procedure Step State (0074,1000)
Attribute using N-SET. Procedure Step State is managed using N-ACTION as
described in `Change UPS State (N-ACTION) <#sect_CC.2.1>`__

The SCU shall create or set all Attributes to meet Final State
requirements prior to using N-ACTION to set the value of Procedure Step
State (0074,1000) to "COMPLETED" or "CANCELED". See `UPS Final State
Requirements <#sect_CC.2.5.1.1>`__ for further details.

Once the Procedure Step State (0074,1000) has been set to "COMPLETED" or
"CANCELED" the SCU shall no longer modify the UPS SOP Instance.

.. note::

   The SCU can only set Attribute Values that have already been created
   with an N-CREATE request.

.. _sect_CC.2.6.3:

Service Class Provider Behavior
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

The SOP Class UID of the specified UPS instance will always be the UPS
Push SOP Class UID, which might not match the UPS SOP Class negotiated
with the SCU. See `Service Class and SOP Class UIDs <#sect_CC.3.1>`__
for further details.

The SCP shall support the Attribute changes to the UPS instance
specified by the SCU in the set request as specified in
`table_title <#table_CC.2.5-3>`__.

The SCP shall refuse set requests on an IN PROGRESS UPS and not modify
the UPS if the set request does not include the Transaction UID
(0008,1195) Attribute with the same value as currently recorded in the
UPS instance.

The SCP shall refuse set requests on a COMPLETED or CANCELED UPS.

The SCP shall use the Specific Character Set (0008,0005) value to
appropriately modify its internal representation so that subsequent
operations reflect the combination of the character sets in use by the
Attributes in this request and those used by Attributes that have not
been modified.

The SCP shall return, via the N-SET response primitive, the N-SET
Response Status Code applicable to the associated request as specified
in `Status Codes <#sect_CC.2.6.4>`__.

The SCP may itself modify any Attributes of a UPS instance independently
of an N-SET request, e.g., if the SCP is performing the procedure step
itself, if it has been determined that the performing SCU has been
disabled, or if it is necessary to correct Attribute Values after
completion of the procedure in order to carry out reconciliation of the
data. A description of the coercions the SCP may perform shall be
documented in the conformance statement of the SCP.

Bi-directional Authentication of machines/users/applications is possible
at association time (see and ). provides a "Refused: Refused: Not
authorized" error code. There are no specific requirements to perform
authorization.

.. _sect_CC.2.6.4:

Status Codes
^^^^^^^^^^^^

`table_title <#table_CC.2.6-1>`__ defines the status code values that
might be returned in a N-SET response. General status code values and
fields related to status code values are defined for N-SET DIMSE Service
in .

.. table:: N-SET Response Status Values [for Set Unified Procedure Step
Information]

   +--------------------------+--------------------------+-------------+
   | Service Status           | Further Meaning          | Status Code |
   +==========================+==========================+=============+
   | Success                  | The requested            | 0000        |
   |                          | modification of the      |             |
   |                          | Attribute Values is      |             |
   |                          | performed                |             |
   +--------------------------+--------------------------+-------------+
   | Warning                  | Requested optional       | 0001        |
   |                          | Attributes are not       |             |
   |                          | supported.               |             |
   +--------------------------+--------------------------+-------------+
   | Coerced invalid values   | B305                     |             |
   | to valid values          |                          |             |
   +--------------------------+--------------------------+-------------+
   | Failure                  | Failed: The UPS is not   | C310        |
   |                          | in the "IN PROGRESS"     |             |
   |                          | state                    |             |
   +--------------------------+--------------------------+-------------+
   | Failed: The correct      | C301                     |             |
   | Transaction UID was not  |                          |             |
   | provided                 |                          |             |
   +--------------------------+--------------------------+-------------+
   | Failed: The UPS may no   | C300                     |             |
   | longer be updated        |                          |             |
   +--------------------------+--------------------------+-------------+
   | Failed: Specified SOP    | C307                     |             |
   | Instance UID does not    |                          |             |
   | exist or is not a UPS    |                          |             |
   | Instance managed by this |                          |             |
   | SCP                      |                          |             |
   +--------------------------+--------------------------+-------------+

.. _sect_CC.2.7:

Get Unified Procedure Step Information (N-GET)
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

This operation allows an SCU to get information from an SCP about a
specific real-world Procedure Step that is represented as a Unified
Procedure Step Instance. This operation shall be invoked by the SCU
through the DIMSE N-GET Service.

.. _sect_CC.2.7.1:

Unified Procedure Step IOD Subset Specification
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

The Application Entity that claims conformance to the UPS Pull or UPS
Watch SOP Classes as an SCU may choose to retrieve a subset of the
Attribute Values maintained by the SCP. The Application Entity that
claims conformance as an SCP to these SOP Classes shall support the
Attributes specified in `table_title <#table_CC.2.5-3>`__.

.. _sect_CC.2.7.2:

Service Class User Behavior
^^^^^^^^^^^^^^^^^^^^^^^^^^^

The SCU uses the N-GET to request the SCP to provide Attributes and
values of a Unified Procedure Step Instance. Since all UPSs are created
as instances of the UPS Push SOP Class, the Affected SOP Class UID
(0000,0002) in the N-GET request shall be the UID of the UPS Push SOP
Class. See `Service Class and SOP Class UIDs <#sect_CC.3.1>`__ for
further details.

The SCU shall specify in the N-GET Service Element the UID of the SOP
Instance from which Attributes are to be retrieved.

The SCU shall specify the list of Unified Procedure Step Attributes for
which values are to be returned. The SCU shall not specify Attributes
that are defined within a Sequence, but rather specify the sequence
itself to be retrieved in its entirety.

The SCU shall not request the value of the Transaction UID (0008,1195)
Attribute.

The SCU may request Attribute Values for optional Attributes that are
not maintained by the SCP. In such a case, the SCU shall function
properly regardless of whether the SCP returns values for those
Attributes or not. This Service Class Specification places no
requirements on what the SCU shall do as a result of receiving this
information.

.. note::

   In order to accurately interpret the character set used for the
   Attribute Values returned, it is recommended that the Attribute Value
   for the Specific Character Set (0008,0005) be requested in the N-GET
   request primitive.

The SCU shall be permitted to request and shall be capable of receiving
values for any Attribute as specified in
`table_title <#table_CC.2.5-3>`__. Additionally, values may be requested
for optional Attributes.

The SCU shall be capable of receiving all requested Attribute Values
provided by the SCP in response to the N-GET indication primitive.

.. note::

   If the SCU or the user will need access to the final state Attributes
   it is the responsibility of the SCU to Subscribe (see `Request UPS
   Cancel (N-ACTION) <#sect_CC.2.2>`__) in order to receive State Change
   Events and then N-GET the necessary Attributes promptly upon
   notification of a state change to COMPLETED or CANCELED. If the SCU
   sets the Deletion Lock when subscribing, a COMPLETED or CANCELED
   instance will continue to persist on the SCP, using resources. It is
   important that the SCU remove the lock (e.g., by unsubscribing) after
   doing the N-GET on the COMPLETED or CANCELED instance.

.. _sect_CC.2.7.3:

Service Class Provider Behavior
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

The SOP Class UID of the specified UPS instance will always be the UPS
Push SOP Class UID, which might not match the UPS SOP Classes negotiated
with the SCU. See `Service Class and SOP Class UIDs <#sect_CC.3.1>`__
for further details.

The SCP shall return, via the N-GET response primitive, the selected
Attribute Values from the indicated Unified Procedure Step Instance to
the SCU.

.. note::

   The requirement for the SCP to respond to N-GET requests for UPS
   Instances that have moved to the COMPLETED or CANCELED state is
   limited. See `Service Class Provider Behavior <#sect_CC.2.1.3>`__
   Service Class Provider Behavior.

The SCP shall not return the Transaction UID (0008,1195) Attribute. This
is necessary to preserve this Attribute's role as an access lock.

The SCP shall return, via the N-GET response primitive, the N-GET
Response Status Code applicable to the associated request. A Failure
Code shall indicate that the SCP has not retrieved the SOP Instance.

Bi-directional Authentication of machines/users/applications is possible
at association time (see and ). provides a "Refused: Refused: Not
authorized" error code. Further requiring or documenting authentication
and/or authorization features from the SCU or SCP is beyond the scope of
this SOP Class.

.. _sect_CC.2.7.4:

Status Codes
^^^^^^^^^^^^

`table_title <#table_CC.2.7-1>`__ defines the status code values that
might be returned in a N-GET response. General status code values and
fields related to status code values are defined for N-GET DIMSE Service
in .

.. table:: N-GET Response Status Values [for Get Unified Procedure Step
Information]

   +----------------+-------------------------------------+-------------+
   | Service Status | Further Meaning                     | Status Code |
   +================+=====================================+=============+
   | Warning        | Requested optional Attributes are   | 0001        |
   |                | not supported                       |             |
   +----------------+-------------------------------------+-------------+
   | Failure        | Failed: Specified SOP Instance UID  | C307        |
   |                | does not exist or is not a UPS      |             |
   |                | Instance managed by this SCP        |             |
   +----------------+-------------------------------------+-------------+

.. _sect_CC.2.8:

Search for Unified Procedure Step (C-FIND)
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

This operation allows an SCU to locate and get information about Unified
Procedure Step instances of interest that are managed by an SCP. This
operation shall be invoked by the SCU through the DIMSE C-FIND Service.
The SCP processes such queries, matches UPS instances it manages against
the keys present in the Identifier and returns C-FIND responses.

The SCU might be searching for UPS instance with the intention of
starting work on one of them or perhaps with the intention of
subscribing to monitor the progress of an instance.

.. _sect_CC.2.8.1:

Operation
^^^^^^^^^

.. _sect_CC.2.8.1.1:

E/R Model
'''''''''

In response to a given C-FIND request, the SCP might send several C-FIND
responses, (i.e., one C-FIND response per matching worklist item). Each
worklist item describes a single task and its related information.

The Unified Procedure Step Query Information Model is represented by the
Entity Relationship diagram shown in
`figure_title <#figure_CC.2.8-1>`__.

There is only one Information Entity in the model, which is the Unified
Procedure Step. The Attributes of a Unified Procedure Step can be found
in `table_title <#table_CC.2.5-3>`__.

.. _sect_CC.2.8.1.2:

C-FIND Service Parameters
'''''''''''''''''''''''''

.. _sect_CC.2.8.1.2.1:

SOP Class UID
             

The Affected SOP Class UID of the C-FIND DIMSE request shall always be
the UPS SOP Class negotiated for the Presentation Context under which
the service is requested. This will always be the UPS Pull SOP Class,
the UPS Watch SOP Class, or the UPS Query SOP Class. See `Service Class
and SOP Class UIDs <#sect_CC.3.1>`__ for further details.

The C-FIND is performed against the Unified Procedure Step Information
Model shown in `figure_title <#figure_CC.2.8-1>`__.

.. _sect_CC.2.8.1.2.2:

Priority
        

The Priority Attribute defines the requested priority of the C-FIND
operation with respect to other DIMSE operations being performed by the
same SCP.

Processing of priority requests is not required of SCPs. Whether or not
an SCP supports priority processing and the meaning of the different
priority levels shall be stated in the Conformance Statement of the SCP.

.. _sect_CC.2.8.1.3:

Identifier
''''''''''

Both the C-FIND request and response contain an Identifier encoded as a
Data Set (see ).

.. _sect_CC.2.8.1.3.1:

Request Identifier Structure
                            

An Identifier in a C-FIND request shall contain:

-  Key Attributes values to be matched against the values of Attributes
   specified in the SOP Class identified by the Affected SOP Class UID.

-  Conditionally, the Attribute Specific Character Set (0008,0005). This
   Attribute shall be included if expanded or replacement character sets
   may be used in any of the Attributes in the Request Identifier. It
   shall not be included otherwise.

-  Conditionally, the Attribute Timezone Offset From UTC (0008,0201).
   This Attribute shall be included if Key Attributes of time are to be
   interpreted explicitly in the designated local time zone. It shall
   not be present otherwise, i.e., it shall not be sent with a
   zero-length value.

.. note::

   This means that Specific Character Set (0008,0005) is included if the
   SCU supports expanded or replacement character sets in the context of
   this service. It will not be included if expanded or replacement
   character sets are not supported by the SCU.

The Key Attributes and values allowable for the query shall be defined
in the SOP Class definition corresponding to the Affected SOP Class UID
for the corresponding Unified Worklist And Procedure Step Information
Model.

.. _sect_CC.2.8.1.3.2:

Response Identifier Structure
                             

The C-FIND response shall not contain Attributes that were not in the
request or specified in this section.

An Identifier in a C-FIND response shall contain:

-  Key Attributes with values corresponding to Key Attributes contained
   in the Identifier of the request (Key Attributes as defined in
   `table_title <#table_CC.2.5-3>`__.)

-  Conditionally, the Attribute Specific Character Set (0008,0005). This
   Attribute shall be included if expanded or replacement character sets
   may be used in any of the Attributes in the Response Identifier. It
   shall not be included otherwise. The C-FIND SCP is not required to
   return responses in the Specific Character Set requested by the SCU
   if that character set is not supported by the SCP. The SCP may return
   responses with a different Specific Character Set.

-  Conditionally, the Attribute Timezone Offset From UTC (0008,0201).
   This Attribute shall be included if any Attributes of time in the
   Response Identifier are to be interpreted explicitly in the
   designated local time zone. It shall not be present otherwise, i.e.,
   it shall not be sent with a zero-length value.

.. note::

   This means that Specific Character Set (0008,0005) is included if the
   SCP supports expanded or replacement character sets in the context of
   this service. It will not be included if expanded or replacement
   character sets are not supported by the SCP.

.. _sect_CC.2.8.2:

Service Class User Behavior
^^^^^^^^^^^^^^^^^^^^^^^^^^^

All C-FIND SCUs shall be capable of generating query requests that meet
the requirements of the "Worklist" Search Method (see `Worklist Search
Method <#sect_CC.2.8.3.1>`__).

Required Keys and Optional Keys, identified in
`table_title <#table_CC.2.5-3>`__, associated with the Query may be
contained in the Identifier.

An SCU conveys the following semantics using the C-FIND requests and
responses:

-  The SCU requests that the SCP perform a match of all keys specified
   in the Identifier of the request against the information it possesses
   of the Query specified in the request.

-  The SCU shall interpret Pending responses to convey the Attributes of
   a match of an item.

-  The SCU shall interpret a response with a status equal to Success,
   Failure, or Cancel to convey the end of Pending responses.

-  The SCU shall interpret a Failure response to a C-FIND request as an
   indication that the SCP is unable to process the request.

-  The SCU may cancel the C-FIND service by issuing a C-FIND-CANCEL
   request at any time during the processing of the C-FIND. The SCU
   shall recognize a status of Cancel to indicate that the C-FIND-CANCEL
   was successful.

.. _sect_CC.2.8.3:

Service Class Provider Behavior
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

All C-FIND SCPs shall be capable of processing queries that meet the
requirements of the "Worklist" Search (see `Worklist Search
Method <#sect_CC.2.8.3.1>`__). This does not imply that an SCP that
supports the UPS Watch SOP Class or the UPS Query SOP Class must also be
an SCP of the UPS Pull SOP Class.

The SCP shall support Attribute matching as described in `Attribute
Matching <#sect_C.2.2.2>`__.

An SCP conveys the following semantics using the C-FIND requests and
responses:

-  The SCP is requested to perform a match of all the keys specified in
   the Identifier of the request, against the information it possesses.
   Attribute matching is performed using the key values specified in the
   Identifier of the C-FIND request as defined in
   `table_title <#table_CC.2.5-3>`__.

-  The SCP generates a C-FIND response for each match using the
   "Worklist" Search method. All such responses shall contain an
   Identifier whose Attributes contain values from a single match. All
   such responses shall contain a status of Pending.

-  When all matches have been sent, the SCP generates a C-FIND response
   that contains a status of Success. A status of Success shall indicate
   that a response has been sent for each match known to the SCP.

.. note::

   1. No Identifier is contained in a response with a status of Success.
      For a complete definition, see .

   2. When there are no matches, then no responses with a status of
      Pending are sent, only a single response with a status of Success.

-  The SCP shall generate a response with a status of Failure if it is
   unable to process the request. A Failure response shall contain no
   Identifier.

-  If the SCP receives C-FIND-CANCEL indication before it has completed
   the processing of the matches it shall interrupt the matching process
   and return a status of Cancel.

Bi-directional Authentication of machines/users/applications is possible
at association time (see and ). provides a "Refused: Refused: Not
authorized" error code. Further requiring or documenting authentication
and/or authorization features from the SCU or SCP is beyond the scope of
this SOP Class.

.. _sect_CC.2.8.3.1:

Worklist Search Method
''''''''''''''''''''''

The following steps are used to generate match responses.

-  Match the key match Attributes contained in the Identifier of the
   C-FIND request against the values of the Key Attributes for each
   worklist entity.

-  If there are no matching keys, then there are no matches, return a
   response with a status equal to Success and with no Identifier.

-  Otherwise,

   -  For each entity for which the Attributes match all of the
      specified matching key Attributes, construct an Identifier. This
      Identifier shall contain all of the values of the Attributes for
      this entity that correspond to the return keys specified in the
      C-FIND request.

   -  Return a response for each remaining Identifier.

`table_title <#table_CC.2.5-3>`__ defines the Attributes of the Unified
Procedure Step Information Model, the requirements for key matching, and
the requirements for return keys.

.. _sect_CC.2.8.4:

Status Codes
^^^^^^^^^^^^

`table_title <#table_CC.2.8-2>`__ defines the status code values that
might be returned in a C-FIND response. General status code values and
fields related to status code values are defined for C-FIND DIMSE
Service in .

.. table:: C-FIND Response Status Values [for Search for Unified
Procedure Step]

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
   | Refused: SOP   | 0122           |              |                |
   | Class not      |                |              |                |
   | supported      |                |              |                |
   +----------------+----------------+--------------+----------------+
   | Failed: Unable | Cxxx           | (0000,0901)  |                |
   | to process     |                |              |                |
   |                |                | (0000,0902)  |                |
   +----------------+----------------+--------------+----------------+
   | Cancel         | Matching       | FE00         | None           |
   |                | terminated due |              |                |
   |                | to Cancel      |              |                |
   |                | request        |              |                |
   +----------------+----------------+--------------+----------------+
   | Success        | Matching is    | 0000         | None           |
   |                | complete - No  |              |                |
   |                | final          |              |                |
   |                | Identifier is  |              |                |
   |                | supplied.      |              |                |
   +----------------+----------------+--------------+----------------+
   | Pending        | Matches are    | FF00         | Identifier     |
   |                | continuing -   |              |                |
   |                | Current Match  |              |                |
   |                | is supplied    |              |                |
   |                | and any        |              |                |
   |                | Optional Keys  |              |                |
   |                | were supported |              |                |
   |                | in the same    |              |                |
   |                | manner as      |              |                |
   |                | Required Keys. |              |                |
   +----------------+----------------+--------------+----------------+
   | Matches are    | FF01           | Identifier   |                |
   | continuing -   |                |              |                |
   | Warning that   |                |              |                |
   | one or more    |                |              |                |
   | Optional Keys  |                |              |                |
   | were not       |                |              |                |
   | supported for  |                |              |                |
   | existence for  |                |              |                |
   | this           |                |              |                |
   | Identifier.    |                |              |                |
   +----------------+----------------+--------------+----------------+

.. note::

   Status Codes are returned in DIMSE response messages (see ). The code
   values stated in column "Status Codes" are returned in Status Command
   Element (0000,0900).

Some Failure Status Codes are implementation specific.

An SCP implementation shall assign specific failure status codes by
replacing each 'x' symbol with a hexadecimal digit in the range from 0
to F. An SCP implementation wishing to differentiate between causes of
“Failed: Unable to process” Failure Meaning shall assign those causes
specific Status Code Values within valid range specified in
`table_title <#table_CC.2.8-2>`__.

An SCU implementation shall recognize any Failure Status Code within the
value range specified in `table_title <#table_CC.2.8-2>`__ as an
indicator of the Failure Meaning stated in the table. There is no
requirement for an SCU implementation to differentiate between specific
Status Codes within the valid range.

.. _sect_CC.3:

UPS SOP Classes
---------------

There are five UPS SOP Classes associated with the Unified Procedure
Step IOD. Each SOP Class supports different interactions with a UPS
Instance (also referred to as a worklist item).

The UPS Push SOP Class allows SCU systems to:

-  create (push) a new worklist item (i.e., instance) onto a worklist

-  submit a cancellation request for a worklist item

The UPS Pull SOP Class allows SCU systems to:

-  query a worklist for matching items

-  take responsibility for performing a worklist item

-  add/modify progress/status/result details for the worklist item

-  finalize a controlled worklist item as Completed or Canceled.

The UPS Watch SOP Class allows SCU systems to:

-  query for worklist items of interest

-  subscribe/unsubscribe for event notifications of changes to a given
   worklist item

-  subscribe/unsubscribe for event notifications of all worklist items

-  get details for a given worklist item

-  submit a cancellation request for a given worklist item

The UPS Event SOP Class allows SCU systems to:

-  receive event notifications of changes to a worklist item

The UPS Query SOP Class allows SCU systems to:

-  query a worklist for matching items

The DICOM AEs that claim conformance to one or more of these SOP Classes
shall support all services listed as "M" in the corresponding
`table_title <#table_CC.2-1>`__, `table_title <#table_CC.2-2>`__,
`table_title <#table_CC.2-3>`__, `table_title <#table_CC.2-4>`__ and
`table_title <#table_CC.2-5>`__.

.. _sect_CC.3.1:

Service Class and SOP Class UIDs
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

All UPS Instances shall be created with the value of SOP Class UID set
to "1.2.840.10008.5.1.4.34.6.1" (i.e., that of the UPS Push SOP Class).

.. note::

   UPS Instances are all based on the Unified Procedure Step IOD and are
   all created either internally by the SCP, or in response to an
   N-CREATE issued as part of the UPS Push SOP Class.

Once created, UPS instances may be operated on by DIMSE services from
any of the four UPS SOP Classes defined in the Unified Worklist and
Procedure Step Service Class.

During association negotiation, the Abstract Syntax UID shall be the
implemented SOP Class as shown in the following list:

-  1.2.840.10008.5.1.4.34.6.1 (UPS Push SOP Class)

-  1.2.840.10008.5.1.4.34.6.2 (UPS Watch SOP Class)

-  1.2.840.10008.5.1.4.34.6.3 (UPS Pull SOP Class)

-  1.2.840.10008.5.1.4.34.6.4 (UPS Event SOP Class)

-  1.2.840.10008.5.1.4.34.6.5 (UPS Query SOP Class)

.. _sect_CC.3.1.1:

DIMSE Implications for UPS (Informative)
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

A SOP Instance may be created with one SOP Class UID (UPS Push) and
later DIMSE Services may refer to it over an association negotiated for
a different SOP Class UID. Further details on this can be found in .

For DIMSE-N Services, the Affected SOP Class UID (0000,0002) or
Requested SOP Class UID (0000,0003), when present, will be the UID of
the UPS Push SOP Class regardless of the negotiated Abstract Syntax UID.
The SCU and SCP will not reject DIMSE-N messages on the basis of the
Affected/Requested SOP Class UID being that of the UPS Push SOP Class,
rather than one of the other four SOP Class UIDs as listed in the
Abstract Syntax UID during association negotiation. The SCU and SCP may
reject the DIMSE-N messages if the instance is not a UPS Push SOP Class
Instance.

For DIMSE-C Services (C-FIND), the Affected SOP Class UID will always
match the negotiated Abstract Syntax UID for the Presentation Context
under which the request is made. This will be UPS Watch, UPS Pull or UPS
Query. All of these SOP Classes represent the UPS Information Model
described in `Operation <#sect_CC.2.8.1>`__.

For example, in a typical "Pull Workflow" message exchange, the C-FIND
query from a "performing SCU" would use the UPS Pull SOP Class UID for
both the negotiated Abstract Syntax UID and the Affected SOP Class UID
(0000,0002), however the SOP Class UID (0008,0016) of the C-FIND
responses themselves will be set to the UPS Push SOP Class UID by the
SCP. All the subsequent N-ACTION, N-SET, and N-GET messages, would then
use the UPS Pull SOP Class UID for the negotiated Abstract Syntax UID,
and the UPS Push SOP Class UID for the Affected SOP Class UID
(0000,0002).

.. _sect_CC.3.1.2:

Global Instance Subscription UID
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

The well-known UID for subscribing/unsubscribing to events for all UPS
Instances managed by an SCP shall have the value
"1.2.840.10008.5.1.4.34.5".

.. _sect_CC.3.2:

Association Negotiation
~~~~~~~~~~~~~~~~~~~~~~~

Association establishment is the first phase of any instance of
communication between peer DICOM AEs. The Association negotiation
procedure specified in shall be used to negotiate the supported SOP
Classes.

See the Association Negotiation definition for the Basic Worklist
Management Service Class (`Association Negotiation <#sect_K.5>`__).

.. _sect_CC.4:

Conformance Requirements
------------------------

Implementations providing conformance to any of the UPS SOP Classes (UPS
Pull, UPS Push, UPS Watch, UPS Event and UPS Query) shall be conformant
as described in the following sections and shall include within their
Conformance Statement information as described below.

An implementation may conform to any of the UPS SOP Classes as an SCU or
as an SCP. The Conformance Statement shall be in the format defined in .

.. _sect_CC.4.1:

SCU Conformance
~~~~~~~~~~~~~~~

An implementation, which is conformant to any of the UPS SOP Classes as
an SCU, shall meet conformance requirements for the operations that it
invokes.

.. _sect_CC.4.1.1:

Operations
^^^^^^^^^^

The SCU Conformance Statement shall be formatted as defined in .

An implementation, that conforms to any of the UPS Push, UPS Pull or UPS
Watch SOP Classes as an SCU, shall specify under which conditions it
will request the modification of the value of the Procedure Step State
(0074,1000) Attribute to "IN PROGRESS", "COMPLETED", and "CANCELED".

An implementation that conforms to the UPS Pull, UPS Watch or UPS Query
SOP Classes as an SCU shall state in its Conformance Statement

-  Whether it requests matching on Optional Matching Key Attributes for
   C-FIND.

-  Whether it requests Type 3 Return Key Attributes. If it requests Type
   3 Return Key Attributes, then it shall list these Optional Return Key
   Attributes.

-  Whether or not it supports extended negotiation of fuzzy semantic
   matching of person names for C-FIND.

-  How it makes use of Specific Character Set (0008,0005) and Timezone
   Offset From UTC (0008,0201) when encoding queries and interpreting
   responses for C-FIND.

-  What access mechanisms the SCP is capable of using for retrieving
   input data and/or making output data available. (see for details on
   the different Retrieval Sequences).

.. _sect_CC.4.2:

SCP Conformance
~~~~~~~~~~~~~~~

An implementation that is conformant to any of the UPS SOP Classes as an
SCP shall meet conformance requirements for the operations that it
performs.

.. _sect_CC.4.2.1:

Operations
^^^^^^^^^^

The SCP Conformance Statement shall be formatted as defined in .

The SCP Conformance Statement shall provide information on the behavior
of the SCP at the following occurrences:

-  The creation of a new Instance of the UPS Push SOP Class with the
   status "SCHEDULED". The result of that process on the scheduling
   information and on the Attribute Values of the Unified Procedure Step
   shall be specified. Any automatic UPS Subscription created in
   response to the Instance creation shall be specified.

-  The conditions for the update of the Attribute "Procedure Step State"
   (0074,1000), i.e., the change to the state "IN PROGRESS" or to
   "CANCELED" or to "COMPLETED".

-  Which Attributes the SCP may update after the state has been set to
   "IN PROGRESS" or "CANCELED" or "COMPLETED".

-  For how long the UPS Instance will persist on the SCP, and how long
   it will be available for N-GETs once its state has been set to
   "COMPLETED" or "CANCELED".

-  Whether the SCP supports priority for C-FIND. If the SCP supports
   priority for C-FIND, then the meaning of the different priority
   levels shall be specified.

-  Whether the SCP supports case-insensitive matching for PN VR
   Attributes for C-FIND. If the SCP supports case-insensitive matching
   of PN VR Attributes, then the Attributes for which this applies shall
   be specified.

-  Whether the SCP supports extended negotiation of fuzzy semantic
   matching of person names for C-FIND. If the SCP supports extended
   negotiation of fuzzy semantic matching of person names, then the
   mechanism for fuzzy semantic matching shall be specified.

-  How the SCP makes use of Specific Character Set (0008,0005) and
   Timezone Offset From UTC (0008,0201) when interpreting C-FIND
   queries, performing matching and encoding responses.

-  What rules the SCP may use to perform additional filtering during a
   C-FIND (e.g., limiting returns based on the requesting user and the
   confidentiality settings of the workitems, or limiting the return to
   a single item already selected on the SCP) and under what conditions
   those rules are invoked.

-  Whether the SCP might refuse Subscription requests and/or Deletion
   Locks and for what reasons.

-  What access mechanisms the SCP is capable of using for retrieving
   input data and/or making output data available. (see for details on
   the different Retrieval Sequences).

