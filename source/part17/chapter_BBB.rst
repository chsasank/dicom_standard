.. _chapter_BBB:

Unified Procedure Step in Radiotherapy (Informative)
====================================================

.. _sect_BBB.1:

Purpose of this Annex
---------------------

This annex provides examples of message sequencing when using the
Unified Procedure Step SOP Classes in a radiotherapy context. This
section is not intended to provide an exhaustive set of use cases but
rather an informative example. There are other valid message sequences
that could be used to obtain an equivalent outcome and there are other
valid combinations of actors that could be involved in the workflow
management.

The current use cases assume that tasks are always scheduled by the
scheduler prior to being performed. It does not address the use case of
an emergency or otherwise unscheduled treatment, where the procedure
step will be created by a different device. However, Unified Procedure
Step does provide a convenient mechanism for doing this.

The use cases addressed in this annex are:

-  Treatment Delivery Normal Flow - Treatment Delivery System (TDS)
   performs the treatment delivery that was scheduled by the Treatment
   Management System (TMS). Both the "internal verification" and
   "external verification" flavors are modeled in these use cases.

-  Treatment Delivery - Override or Additional Information Required.
   Operating in the external verification mode, the Machine Parameter
   Verifier (MPV) detects an out-of-tolerance parameter of missing
   information, and requests the user to override the parameter or
   supply or correct the missing information. This use case addresses
   the situation where the 'verify' function is split from the TDS, but
   does not address verification of a subset of parameters by an
   external delivery accessory such as a patient positioner.

.. _sect_BBB.2:

Use Case Actors
---------------

The following actors are used in the use cases below:

User
   Human being controlling the delivery of the treatment.

Archive
   Stores SOP Instances (images, plans, structures, dose distributions,
   etc).

Treatment Management System (TMS)
   Manages worklists and tracks performance of procedures. This role is
   commonly filled by a Treatment Management System (Oncology
   Information System) in the Oncology Department. Acts as a UPS Pull
   SCP. The TMS has a user interface that may potentially be located in
   the treatment delivery control area. In addition, TMS terminals may
   be located throughout the institution.

Treatment Delivery System (TDS)
   Performs the treatment delivery specified by the worklist, updating a
   UPS, and stores treatment records and related SOP Instances such as
   verification images. Acts as a UPS Pull SCU. The TDS user interface
   is dedicated to the safe and effective delivery of the treatment, and
   is located in the treatment control area, typically just outside the
   radiation bunker.

Machine Parameter Verifier (MPV)
   Oversees and potentially inhibits delivery of the treatment. This
   role is commonly filled by a Treatment Management System in the
   Oncology Department, when the TDS is in the external verification
   mode. The MPV does not itself act as a UPS Pull SCU, but communicates
   directly with the TDS, which acts as a UPS Pull SCU. The MPV user
   interface may be shared with the TMS (in the treatment delivery
   control area), or could be located on a separate console.

.. _sect_BBB.3:

Use Cases
---------

.. _sect_BBB.3.1:

Treatment Delivery Normal Flow - Internal Verification
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

.. _sect_BBB.3.1.1:

Message Sequencing
^^^^^^^^^^^^^^^^^^

`figure_title <#figure_BBB.3.1.1-1>`__ illustrates a message sequence
example in the case where a treatment procedure delivery is requested
and performed by a delivery device that has internal verification
capability. In the example, no 'setup verification' is performed, i.e.,
the patient is assumed to be in the treatment position. Unified
Procedure Step (UPS) is used to request delivery of a session of
radiation therapy (commonly known as a "fraction") from a specialized
Application Entity (a "Treatment Delivery System"). That entity performs
the requested delivery, completing normally. Further examples could be
constructed for discontinued, emergency (unscheduled) and interrupted
treatment delivery use cases, but are not considered in this informative
section (see DICOM Part 17 for generic examples).

In this example the Treatment Delivery System conforms to the UPS Pull
SOP Class as an SCU, and the Treatment Management System conforms to the
UPS Pull SOP Class as an SCP. In alternative implementations requiring
on-the-fly scheduling and notification, other UPS SOP classes could be
implemented.

Italic text in `figure_title <#figure_BBB.3.1.1-1>`__ denotes messages
that will typically be conveyed by means other than DICOM services.

.. _sect_BBB.3.1.2:

Transactions and Message Flow
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

This section describes in detail the interactions illustrated in
`figure_title <#figure_BBB.3.1.1-1>`__.

1.  'List Procedures for Delivery' on TDS console.

    The User uses a control on the user interface of the TDS to indicate
    that he or she wishes to see the list of patients available for
    treatment.

2.  Query UPS.

    The TDS queries the TMS for Unified Procedure Steps (UPSs) matching
    its search criteria. For example, all worklist items with a Unified
    Procedure Step Status of "SCHEDULED", and Input Readiness State
    (0040,4041) of "READY". This is conveyed using the C-FIND request
    primitive of the UPS Pull SOP Class.

3.  Receive 0-n UPS.

    The TDS receives the set of Unified Procedure Steps (UPSs) resulting
    from the Query UPS message. The Receive UPS is conveyed via one or
    more C-FIND response primitives of the UPS Pull SOP Class. Each
    response (with status pending) contains the requested Attributes of
    a single Unified Procedure Step (UPS).

    The TMS returns a list of one or more UPSs based on its own
    knowledge of the planned tasks for the querying device. Two
    real-world scenarios are common in this step:

    -  There is no TMS Console located in the treatment area, and
       selection of the delivery to be performed has not been made. In
       this case, the TMS returns a list of potentially many UPSs (for
       different patients), and the User picks from the list the UPS
       that they wish to deliver.

    -  The User has direct access to the TMS in the treatment area, and
       has already selected the delivery to be performed on the console
       of the TMS, located in the treatment room area. In this case, a
       single UPS is returned. The TDS may either display the single
       item for confirmation, or proceed directly to loading the patient
       details.

    A returned set of UPSs may have more than one UPS addressing a given
    treatment delivery. For example, in the case where a patient
    position verification is required prior to delivery, there might be
    a UPS with Requested Procedure Code Sequence item having a Code
    Value of 121708 ("RT Patient Position Acquisition, CT MV"), another
    UPS with a Code Value of 121714 ("RT Patient Position Registration,
    3D CT general"), another UPS with a Code Value of 121722 ("RT
    Patient Position Adjustment"),and a fourth UPS whose Requested
    Procedure Code Sequence item would have a Code Value of 121726 ("RT
    Treatment With Internal Verification").

4.  'Select Procedure' on TDS console

    The User selects one of the scheduled procedures specified on the
    TDS console. If exactly one UPS was returned from the UPS query
    described above, then this step can be omitted.

5.  Get UPS Details and Retrieve Archive Objects

    The TDS may request the details of one or more procedure steps. This
    is conveyed using the N-GET primitive of the UPS Pull SOP Class, and
    is required when not all necessary information can be obtained from
    the query response alone.

    The TDS then retrieves the required SOP Classes from the Input
    Information Sequence of the returned UPS query response. In response
    to a C-MOVE Request on those objects (5a), the Archive then
    transmits to the TDS the SOP Instances to be used as input
    information during the task. These SOP Instances might include an RT
    Plan SOP Instance, and verification images (CT Image or RT Image).
    They might also include RT Beams Treatment Record SOP Instances if
    the Archive is used to store these SOP Instances rather than the
    TMS. The TDS knows of the existence and whereabouts of these SOP
    Instances by virtue of the fully-specified locations in the N-GET
    response.

    Although the TDS could set the UPS to 'IN PROGRESS' prior to
    retrieving the archive instances, this example shows the archive
    instances being retrieved prior to the UPS being 'locked' with the
    N-ACTION step. This avoids the UPS being set 'IN PROGRESS' if the
    required instances are not available, and therefore avoids the need
    to schedule another (different) procedure step in this case, as
    required by the Unified Procedure Step State Diagram State Diagram
    (). However, some object instances dynamically created to service
    performing of the UPS step should be supplied after setting the UPS
    'IN PROGRESS' (see Step 7).

6.  Change UPS State to IN PROGRESS

    The TDS sets the UPS (which is managed by the TMS) to have the
    Unified Procedure Step Status of 'IN PROGRESS' upon starting work on
    the item. The SOP Instance UID of the UPS will normally have been
    obtained in the worklist item. This is conveyed using the N-ACTION
    primitive of the UPS Pull SOP Class with an action type "UPS Status
    Change". This message allows the TMS to update its worklist and
    permits other Performing Devices to detect that the UPS is already
    being worked on.

    The UPS is updated in this step before the required dynamic SOP
    Instances are obtained from the TMS (see Step 7). In radiation
    therapy, it is desirable to signal as early as possible that a
    patient is about to undergo treatment, to allow the TMS to begin
    other activities related to the patient delivery. If the TMS
    implements the UPS Watch SOP Class, other systems will be able to
    subscribe for notifications regarding the progress of the procedure
    step.

7.  Retrieve TMS Objects

    In response to a C-MOVE Request, the TMS transmits to the TDS the RT
    Beams Delivery Instruction and possibly RT Treatment Summary Record
    SOP Instances to be used as input information during the task. These
    SOP Instances may be created "on-the-fly" by the TMS (since it was
    the TMS itself that transmitted the UIDs in the UPS). The RT
    Treatment Summary SOP Instance may be required by the TDS to
    determine the delivery context, although the UPS does specify a
    completion delivery (following a previous delivery interruption). RT
    Beams Treatment Record instances might also be retrieved from the
    TMS in this step if the TMS is used to manage these SOP Instances
    rather than the Archive.

8.  'Start Treatment Session' on TDS console

    The User uses a control on the user interface of the TDS to indicate
    that he or she wishes to commence the treatment delivery session. A
    Treatment Session may involve fulfillment of more than one UPS, in
    which case Steps 4-13 may be repeated.

9.  Set UPS Progress and Beam Number, Verify, and Deliver Radiation

    For each beam, the TDS updates the UPS on the TMS just prior to
    starting the radiation delivery sequencing. This is conveyed using
    the N-SET primitive of the UPS Pull SOP Class.

    The completion percentage of the entire UPS is indicated in the
    Unified Procedure Step Progress Attribute. The algorithm used to
    calculate this completion percentage is not specified here, but
    should be appropriate for user interface display.

    The Referenced Beam Number of the beam about to be delivered is
    specified by encoding it as a string value in the Procedure Step
    Progress Description (0074,1006).

    The TDS then performs internal verifications to determine that the
    machine is ready to deliver the radiation, and then delivers the
    therapeutic radiation for the specified beam. In the current use
    case, it is assumed that the radiation completes normally,
    delivering the entire scheduled fraction. Other use cases, such as
    voluntary interruption by the User, or interruption by the TDS, will
    be described elsewhere.

    If there is more than one beam to be delivered, the verification,
    UPS update, and radiation delivery is repeated once per beam.

    This example does not specify whether or not treatment should be
    interrupted or terminated if a UPS update operation fails. The
    successful transmittal of updates is not intended as a gating
    requirement for continuation of the delivery, but could be used as
    such if the TDS considers that interrupting treatment is clinically
    appropriate at that moment of occurrence.

10. Set UPS to Indicate Radiation Complete

    The TDS may then update the UPS Progress Information Sequence upon
    completion of the final beam (although this is not required), and
    set any other Attributes of interest to the SCP. This is conveyed
    using the N-SET primitive of the UPS Pull SOP Class.

11. Store Results

    The TDS stores any generated results to the Archive. This would
    typically be achieved using the Storage and/or Storage Commitment
    Service Classes and may contain one or more RT Beams Treatment
    Records or RT Treatment Summary Records, RT Images (portal
    verification images), CT Images (3D verification images), RT Dose
    (reconstructed or measured data), or other relevant Composite SOP
    Instances. References to the results and their storage locations are
    associated with the UPS in the Set UPS to Final State message
    (below). The RT Beams Treatment Record instances might be stored to
    the TMS instead, if the TMS is used to manage these SOP Instances
    rather than the Archive.

    The required SOP Instances are stored to the Archive in this step
    before the UPS is status is set to COMPLETED. In radiation therapy,
    it is desirable to ensure that the entire procedure is complete,
    including storage of important patient data, before indicating that
    the step completed successfully. For some systems, such as those
    using Storage Commitment, this may not be possible, in which case
    another service such as Instance Availability Notification (not
    shown here) would have to be used to notify the TMS of SOP Instance
    availability. For the purpose of this example, it is assumed that
    the storage commitment response occurs in a short time frame.

12. Set UPS Attributes to Meet Final State Requirements

    The TDS then updates the UPS with any further Attributes required to
    conform to the UPS final state requirements. Also, references to the
    results SOP Instances stored in Step 11 are supplied in the Output
    Information Sequence. This is conveyed using the N-SET primitive of
    the UPS Pull SOP Class.

13. Change UPS State to COMPLETED

    The TDS changes the Unified Procedure Step Status of the UPS to
    COMPLETED upon completion of the scheduled step and storage or
    results. This is conveyed using the N-ACTION primitive of the UPS
    Pull SOP Class with an action type "UPS Status Change". This message
    informs the TMS that the UPS is now complete.

14. Indicate 'Treatment Session Completed' on TDS Console

    The TDS then signals to the User via the TDS user interface that the
    requested procedure has completed successfully, and all generated
    SOP Instances have been stored.

.. _sect_BBB.3.2:

Treatment Delivery Normal Flow - External Verification
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

.. _sect_BBB.3.2.1:

Message Sequencing
^^^^^^^^^^^^^^^^^^

`figure_title <#figure_BBB.3.2.1-1>`__ illustrates a message sequence
example in the case where a treatment procedure delivery is requested
and performed by a conventional delivery device requiring an *external*
verification capability.

In the case where external verification is requested (i.e., where the
UPS Requested Procedure Code Sequence item has a value of "RT Treatment
With External Verification"), the information contained in the UPS and
potentially other required delivery data must be communicated to the
Machine Parameter Verifier (MPV). In many real-world situations the
Oncology Information System fulfills both the role of the TMS and the
MPV, hence this communication is internal to the device and not
standardized. If separate physical devices perform the two roles, the
communication may also be non-standard, since these two devices must be
very closely coupled.

Elements in bold indicate the additional messages required when the
Machine Parameter Verifier is charged with validating the beam
parameters for each beam, prior to radiation being administered. These
checks can be initiated by the User on a beam-by-beam basis ('manual
sequencing', shown with the optional 'Deliver Beam x' messages), or can
be performed by the Machine Parameter Verifier without intervention
('automatic sequencing'). The TDS would typically store an RT Treatment
Record SOP Instance after each beam.

This example illustrates the case where photon or electron beams are
being delivered. If ion beams are to be delivered, instances of the RT
Conventional Machine Verification IOD will be replaced with instances of
the RT Ion Machine Verification IOD.

Delivery of individual beams can be explicitly requested by the User (as
shown in this example), or sequenced automatically by the TDS.

.. _sect_BBB.3.2.2:

Transactions and Message Flow
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

This section describes in detail the additional interactions illustrated
in `figure_title <#figure_BBB.3.2.1-1>`__.

After the TDS has retrieved the necessary treatment SOP Instances (Step
7), the following step is performed:

7a. Communicate UPS and Required Delivery Data to MPV

The MPV must receive information about the procedure to be performed,
and any other data required in order to carry out its role. This
communication typically occurs outside the DICOM Standard, since the TMS
and MPV are tightly coupled (and may be the same physical device). In
cases where standardized network communication of these parameters is
required, this could be achieved using DICOM storage of RT Plan and RT
Delivery Instruction SOP Instances, or alternatively by use of the UPS
Push SOP Class.

After the User has initiated the treatment session on the TDS console
(Step 8), the following steps are then performed:

8a. 'Deliver Beam x' on TDS console

In some implementations, parameter verification for each beam may be
initiated manually by the User (as shown in this example). In other
approaches, the TDS may initiate these verifications automatically.

8b. Create RT Conventional Machine Verification Instance

The TDS creates a new RT Conventional Machine Verification instance on
the MPV prior to beam parameter verification of the first beam to be
delivered. This is conveyed using the N-CREATE primitive of the RT
Conventional Machine Verification SOP Class.

After the TDS has signaled the UPS current Referenced Beam Number and
completion percentage for a given beam (9), the following sequence of
steps is performed:

9a. Set 'Beam x' RT Conventional Machine Verification Instance

The TDS sets the RT Conventional Machine Verification SOP Instance to
transfer the necessary verification parameters. This is conveyed using
the N-SET primitive of the RT Conventional Machine Verification SOP
Class. The Referenced Beam Number (300C,0006) Attribute is used to
specify the beam to be delivered. It is the responsibility of the SCU to
keep track of the verification parameters such that the complete list of
required Attributes can be specified within the top-level sequence
items.

9b. Initiate Verification

The TDS sets the RT Conventional Machine Verification SOP Instance to
indicate that the TDS is ready for external verification to occur. This
is conveyed using the N-ACTION primitive of the RT Conventional Machine
Verification SOP Class.

9c. Verify Machine Parameters

The MPV then attempts to verify the treatment parameters for 'Beam x'.
The MPV sends one or more N-EVENT-REPORT signals to the TDS during the
verification process. The permissible event types for these signals in
this context are 'Pending' (zero or more times, not shown in this use
case), and 'Done' when the verification is complete (successful or
otherwise).

9d. Get RT Conventional Machine Verification (optional step)

The TDS may then request Attributes of the RT Conventional Machine
Verification instance. This is conveyed using the N-GET primitive of the
RT Conventional Machine Verification SOP Class. If verification has
occurred normally and the N-EVENT-REPORT contained a Treatment
Verification Status of VERIFIED (this use case), then this step is not
necessary unless the TDS wishes to record additional parameters
associated with the verification process.

The TDS then delivers the therapeutic radiation. In the current use
case, it is assumed that the radiation completes normally, delivering
the entire scheduled fraction. Other use cases, such as voluntary
interruption by the User, or interruption by the TDS or MPV, are not
described here. If the delivery requires an override of additional
information, a different message flow occurs. This is illustrated in the
use case described in the next section.

9e. Store 'Beam x' RT Beams Treatment Record to Archive

The TDS stores an RT Beams Treatment Record to the Archive (or
potentially the TMS as described in `Transactions and Message
Flow <#sect_BBB.3.1.2>`__ Transactions and Message Flow). The RT Beams
Treatment Record is therefore not stored in Step 11 for the external
verification case (since it has already been stored in the step on a
per-beam basis).

For each subsequent beam in the sequence of beams being delivered, steps
8a (optional), 9, 9a, 9b, 9c, 9d (optional), and 9e are then repeated,
i.e., N-SET, N-ACTION, and N-GET operations are performed on the same
instance of the RT Conventional Machine Verification SOP Class, which
persists throughout the beam session.

9f. Delete RT Conventional Machine Verification Instance

When all beams have been processed, the TDS deletes the RT Conventional
Machine Verification SOP Instance to indicate to the MPV that
verification is no longer required. This is conveyed using the N-DELETE
primitive of the RT Conventional Machine Verification SOP Class.

.. _sect_BBB.3.3:

Treatment-delivery With External Verification - Override Or Additional Info Required
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

.. _sect_BBB.3.3.1:

Message Sequencing
^^^^^^^^^^^^^^^^^^

`figure_title <#figure_BBB.3.3.1-1>`__ illustrates a message sequence
example for the external verification model in the case where the
Machine Parameter Verifier (MPV) either detects that an override is
required, or requires additional information (such as a bar code) before
authorizing treatment.

The steps in this use case replace Steps 8a to 9f in Use Case BBB.3.2,
for the case where only a single beam is delivered.

.. _sect_BBB.3.3.2:

Transactions and Message Flow
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

This section describes in detail the interactions illustrated in
`figure_title <#figure_BBB.3.3.1-1>`__.

1.  'Deliver Beam x' on TDS console (optional step)

    See use case `Treatment Delivery Normal Flow - External
    Verification <#sect_BBB.3.2>`__.

2.  Create RT Conventional Machine Verification Instance

    See use case `Treatment Delivery Normal Flow - External
    Verification <#sect_BBB.3.2>`__.

3.  Set 'Beam x' RT Conventional Machine Verification Instance

    See use case `Treatment Delivery Normal Flow - External
    Verification <#sect_BBB.3.2>`__.

4.  Initiate Machine Verification

    See use case `Treatment Delivery Normal Flow - External
    Verification <#sect_BBB.3.2>`__.

5.  Verify Machine Parameters

    The MPV then attempts to verify the treatment parameters for 'Beam
    x'. The MPV determines that one or more treatment parameters are
    out-of-tolerance, or that information such as a bar code is missing.
    It sends an N-EVENT-REPORT signal to the TDS with an Event Type of
    Done and an RT Machine Verification Status of NOT_VERIFIED. The MPV
    also shows the reason for the override/information request on its
    display (5a).

6.  Supply Override Instruction or Bar Code

    The User observes on the MPV console that an override or missing
    information is required, and supplies the override approval or
    missing information to the MPV via its user interface, or equivalent
    proxy.

7.  Initiate Machine Verification

    The TDS performs another N-ACTION on the RT Conventional Machine
    Verification SOP Instance to indicate that the TDS is once again
    ready for treatment verification. See use case `Treatment Delivery
    Normal Flow - External Verification <#sect_BBB.3.2>`__. This may be
    initiated by the user (as shown in this example), or may be
    initiated automatically by the TDS using a polling approach.

8.  Re-verify Machine Parameters

    The MPV verifies the treatment parameters, and determines that all
    parameters are now within tolerance and all required information is
    supplied. It sends an N-EVENT-REPORT signal to the TDS with an Event
    Type of Done and an RT Machine Verification Status of VERIFIED_OVR.

    .. note::

       If another verification failure occurs, the override cycle can be
       repeated as many times as necessary.

9.  Get RT Conventional Machine Verification (optional step)

    See use case `Treatment Delivery Normal Flow - External
    Verification <#sect_BBB.3.2>`__. If an N-GET is requested, the
    parameters that were overridden are available in Overridden
    Parameters Sequence (0074,104A).

    The TDS then delivers the therapeutic radiation.

10. Store 'Beam x' RT Beams Treatment Record to Archive

    See use case `Treatment Delivery Normal Flow - External
    Verification <#sect_BBB.3.2>`__. Overridden parameters are
    ultimately captured in the treatment record.

11. Delete RT Conventional Machine Verification Instance

    See use case `Treatment Delivery Normal Flow - External
    Verification <#sect_BBB.3.2>`__.

.. _sect_BBB.3.4:

Treatment-delivery With External Verification - Machine Adjustment Required
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

.. _sect_BBB.3.4.1:

Message Sequencing
^^^^^^^^^^^^^^^^^^

`figure_title <#figure_BBB.3.4.1-1>`__ illustrates a message sequence
example for the external verification model in the case where the
Machine Parameter Verifier (MPV) detects that one or more machine
adjustments are required before authorizing treatment, and the TDS has
been configured to retrieve the failure information and make the
required adjustments.

The steps in this use case replace Steps 8a to 9f in Use Case BBB.3.2,
for the case where only a single beam is delivered.

.. _sect_BBB.3.4.2:

Transactions and Message Flow
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

This section describe in detail the interactions illustrated in
`figure_title <#figure_BBB.3.4.1-1>`__.

1.  'Deliver Beam x' on TDS console (optional step)

    See use case `Treatment Delivery Normal Flow - External
    Verification <#sect_BBB.3.2>`__.

2.  Create RT Conventional Machine Verification Instance

    See use case `Treatment Delivery Normal Flow - External
    Verification <#sect_BBB.3.2>`__.

3.  Set 'Beam x' RT Conventional Machine Verification Instance

    See use case `Treatment Delivery Normal Flow - External
    Verification <#sect_BBB.3.2>`__.

4.  Initiate Machine Verification

    See use case `Treatment Delivery Normal Flow - External
    Verification <#sect_BBB.3.2>`__.

5.  Verify Machine Parameters

    The MPV then attempts to verify the treatment parameters for 'Beam
    x'. The MPV determines that one or more treatment parameters are
    out-of-tolerance. It sends an N-EVENT-REPORT signal to the TDS with
    an Event Type of Done and an RT Machine Verification Status of
    NOT_VERIFIED. It may also display the verification status and
    information to the user (5a).

6.  Get RT Conventional Machine Verification

    The TDS then requests the failed verification parameters of the
    verification process. This is conveyed using the N-GET primitive of
    the RT Conventional Machine Verification SOP Class. The MPV replies
    with an N-GET-RESPONSE having a Treatment Verification Status of
    NOT_VERIFIED. The reason(s) for the failure is encoded in the Failed
    Parameters Sequence (0074,1048) Attribute of the response.

7.  Request machine adjustment

    As illustrated in this example, some implementations may require
    that the User observes the failed verification parameters on the MPV
    console and manually request the required machine adjustment. In
    this case the User makes the request to the TDS via its user
    interface. In other implementations the TDS makes the adjustments
    automatically and request verification without User intervention.

8.  Adjust TDS and Set 'Beam x' RT Conventional Machine Verification
    Instance

    The TDS adjusts one or more of its parameters as requested, then
    sets the RT Conventional Machine Verification SOP Instance to
    indicate that the TDS is once again ready for treatment delivery.
    This is conveyed using the N-SET primitive of the RT Conventional
    Machine Verification SOP Class. The N-SET command provides values
    for all applicable parameters (not just those that have been
    modified) since if one or more parameters within a top-level
    sequence is supplied, then all the applicable parameters within that
    sequence must also be supplied (otherwise DICOM requires their
    values to be cleared).

9.  Initiate Machine Verification

    The TDS performs another N-ACTION on the RT Conventional Machine
    Verification SOP Instance to request that the MPV re-perform
    treatment verification. See use case `Treatment Delivery Normal Flow
    - External Verification <#sect_BBB.3.2>`__.

    As an optional step, the MPV may notify the TDS that the
    verification is in process at any time, by sending an N-EVENT-REPORT
    signal to the TDS with an Event Type of Pending (9a).

10. Re-verify Machine Parameters

    The MPV verifies the treatment parameters, and determines that the
    required adjustments have been made, i.e., all parameters are now
    within tolerance. It sends an N-EVENT-REPORT signal to the TDS with
    an Event Type of Done and an RT Conventional Machine Verification
    Status of VERIFIED.

    .. note::

       If another verification failure occurs, the override cycle can be
       repeated as many times as necessary.

11. Get RT Conventional Machine Verification (optional step)

    See use case `Treatment Delivery Normal Flow - External
    Verification <#sect_BBB.3.2>`__.

    The TDS then delivers the therapeutic radiation.

12. Store 'Beam x' RT Beams Treatment Record to Archive

    See use case `Treatment Delivery Normal Flow - External
    Verification <#sect_BBB.3.2>`__.

13. Delete RT Conventional Machine Verification Instance

    See use case `Treatment Delivery Normal Flow - External
    Verification <#sect_BBB.3.2>`__.

