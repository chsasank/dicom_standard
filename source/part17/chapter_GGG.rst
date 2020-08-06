.. _chapter_GGG:

Unified Worklist and Procedure Step - UPS (Informative)
=======================================================

.. _sect_GGG.1:

Introduction
------------

This section provides examples of different implementations and message
sequencing when using the Unified Worklist and Procedure Step SOP
Classes (UPS Push, UPS Pull, UPS Watch and UPS Event).

The examples are intended to provide a sense of how the UPS SOP Classes
can be used to support a variety of workflow use cases. For the detailed
specification of how the underlying DIMSE Services function, please
refer to . For the detailed specification of how the RESTful services
function, please refer to .

The Unified Worklist and Procedure Step Service Class combines the
information that is conveyed separately by the Modality Worklist and
Modality Performed Procedure Step into a single normalized object. This
object is created to represent the planned step and then updated to
reflect its progress from scheduled to complete and record details of
the procedure performed and the results created. Additionally, the
Unified Worklist supports subscription based notifications of progress
and completion.

The Unified Worklist and Modality Procedure Step Service Class does not
include support for complex internal task structures. It describes a
single task to be performed in terms of the task request and the task
results. Additional complexity is managed by the business logic.

The UPS SOP Classes define services so UPSs can be created, their status
managed, notifications sent and their Attributes set, queried, and
retrieved. DICOM intentionally leaves open the many combinations in
which these services can be implemented and applied to enact a variety
of approaches to workflow.

**Pull Workflow and Push Workflow**

Similar to previous SOP Classes like Modality Worklist, UPS allows a
performing system (using the UPS Pull SOP Class as a C-FIND SCU) to
query a worklist manager (the SCP) for relevant tasks and choose which
one to start working on. This is sometimes called "Pull Workflow" since
the performer pulls down the list and selects an item.

UPS adds the ability for a scheduling system (using the UPS Push SOP
Class as an N-CREATE SCU) to "push" a workitem onto the performing
system (here an SCP). In "Push Workflow" the scheduler makes the choice
of which system becomes responsible for the workitem.

Performing systems (again as an SCP) could also schedule/create their
own workitems, while allowing other systems (using the UPS Watch and UPS
Event SOP Classes as N-EVENT-REPORT SCUs and N-GET SCUs) to receive
notifications of the activities of the performer and examine the
results.

Push and Pull can also be combined in various ways. A high level
departmental scheduler could break down orders and push tasks onto the
acquisition worklist manager and reporting worklist manager from which
modalities and reporting workstations could pull their tasks. In another
scenario, a modality that has pulled an acquisition workitem off a
worklist, could push a follow-up task onto a workstation to perform 3D
processing or CAD on the results.

**Reliable Watchers and Deletion Locks**

Some UPS features (specifically the Deletion Lock - See ) were
introduced to support Reliable Watchers. By subscribing with a Deletion
Lock, an SCU wishing to be a reliable watcher can signal the SCP to
persist instances until the watcher has been able to retrieve final
state information and remove the lock.

This means that network latency, slight delays in processing threads, or
even the watcher being offline for a short time, will not prevent the
watcher from reliably collecting the final state details from UPS
instances it is interested in. This can be very important since the
watcher may be responsible for monitoring completion of those instances,
extracting details from them, and based on that and other internal
logic, creating subsequent UPS Instances and populating the input data
fields with information from the completed UPS. Without some form of
persistence guarantee, UPS instances could disappear immediately upon
entering a completed state.

Having established the Deletion Lock mechanism, it is possible that, due
to equipment or processing errors, there could be cases where locks are
not properly removed and some UPS instances might remain when they are
no longer needed. Most SCP implementations will likely provide a way for
such orphaned UPS instances to be removed under administrator control.

.. _sect_GGG.2:

Implementation Examples
-----------------------

The following sections describe ways UPS workflows could be used to
address some typical scenarios.

.. _sect_GGG.2.1:

Typical SOP Class Implementations
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

The decision of which SOP Classes to implement in which systems will
revolve partly around where it makes the most sense for the business
logic to reside, what information each system would have access to, and
what kind of workflow is most effective for the users.

`table_title <#table_GGG.1-1>`__ shows a number of hypothetical systems
and the combination of SOP Classes they might implement. For example, a
typical worklist manager would support all four SOP Classes as an SCP. A
typical scheduling system might want to be a UPS Push SCU to submit work
items to the worklist manager, a UPS Watch SCU to subscribe for
notifications and get details of the results, and a UPS Event SCU to
receive the progress notifications. A simple "pull performer" might only
be a UPS Pull SCU, similar to modalities today.

Other examples are listed for:

-  "Minimal Scheduler", a requesting system that is not interested in
   monitoring progress or results.

-  "Watcher", a system interested in tracking the progress and/or
   results of Unified Procedure Steps.

-  "General Contractor", a system that accepts work items pushed to it,
   then uses internal business logic to subdivide/create work items that
   it pushes or makes available to systems that will actually perform
   the work.

-  "Push Performer", a system, for example a CAD system, that has work
   pushed to it, and provides status and results information to
   interested observers.

-  "Self-Scheduled Performer", which internally schedules it's own work,
   but supports notifications and N-GET so the details of the work can
   be made available to other departmental systems.

-  "Self-Scheduled Pull Performer", which pushes a workitem onto a
   worklist manager and then pulls it off to perform it. This allows it
   to work on "unscheduled" procedures without taking on the
   responsibility of being an SCP for notifications and events.

.. table:: SOP Classes for Typical Implementation Examples

   ============================= === === = = = = = =
   SOP Classes                   SCU SCP           
   ============================= === === = = = = = =
   Non-Performing SCUs                             
   Minimal Scheduler             X                 
   Typical Scheduler             X   X   X         
   Watcher                           X   X         
   Worklist SCPs                                   
   Worklist Manager                          X X X X
   General Contractor            X   X   X   X X X X
   Performing SCPs                                 
   Push Performer                            X X X 
   Self-Scheduled Performer                    X X 
   Performing SCUs                                 
   Pull Performer                          X       
   Self-Scheduled Pull Performer X         X       
   ============================= === === = = = = = =

A system that implements UPS Watch as an SCP will also need to implement
UPS Event as an SCP to be able to send Event Reports to the systems from
whom it accepts subscriptions.

.. _sect_GGG.2.2:

Typical Pull Workflow
~~~~~~~~~~~~~~~~~~~~~

This example shows how a typical pull workflow could be used to manage
the work of a 3D Lab. A group of 3D Workstations query a 3D Worklist
Manager for work items that they perform and report their progress. In
this example, the RIS would be a "Typical Scheduler", the 3D Workstation
is a "Pull Performer" as seen in `table_title <#table_GGG.1-1>`__ and
the PACS and Modality do not implement any UPS SOP Classes.

We will assume the RIS decides which studies require 3D views and puts
them on the worklist once the acquiring modality has reported it's MPPS
complete. The RIS identifies the required 3D views and lists the
necessary input objects in the UPS based on the image references
recorded in the MPPS.

Assume the RIS has subscribed globally for all UPS instances managed by
the 3D Worklist Manager.

.. _sect_GGG.2.3:

Reporting Workflow With "hand-off"
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

This example shows a reporting workflow with a "hand-off". Reporting
Workstations query a RIS for work items to interpret/report. In this
example, the RIS is a "Worklist Manager", the Reporting Workstation is
both a "Pull Performer" and a "Minimal Scheduler" as shown in
`table_title <#table_GGG.1-1>`__ and the PACS and Modality do not
implement any UPS SOP Classes. A reporting workstation claims Task X but
can't complete it and "puts it back on the worklist" by canceling Task X
and creating Task Y as a replacement, recording Task X as the Replaced
Procedure Step.

Assume the RIS is picking up where example GGG.2.2 left off and was
waiting for the 3D view generation task to be complete before putting
the study on the reading worklist. The RIS identifies the necessary
input objects in the UPS based on the image references recorded in the
acquisition MPPS and the 3D UPS.

You could also imagine the 3D workstation is a Mammo CAD workstation. If
the first radiologist completed the report, the RIS could easily
schedule Task Y as the over-read by another radiologist.

For further discussion, refer to the `Other Examples <#sect_GGG.2.7>`__
material on Hand-offs, Fail-overs and Putting Tasks Back on the
Worklist.

.. _sect_GGG.2.4:

Third Party Cancel
~~~~~~~~~~~~~~~~~~

Cancel requests are always directed to the system managing the UPS
instance since it is the SCP. When the UPS is being managed by one
system (for example a Treatment Management System) and performed by a
second system (for example a Treatment Delivery System), a third party
would send the cancel request to the TMS and cancellation would take
place as shown below.

Performing SCUs are not *required* to react to cancel requests, or even
to listen for them, and in some situations would be unable to abort the
task represented by the UPS even if they were listening. In the diagram
below we assume the performing SCU is listening, willing, and able to
cancel the task.

If the User had sent the cancel request while the UPS was still in the
SCHEDULED state, the SCP (i.e., the TMS) could simply have canceled the
UPS internally. Since the UPS state was IN PROGRESS, it was necessary to
send the messages as shown. Note that since the TDS has no need for the
UPS instance to persist, it subscribed without setting a Deletion Lock,
and so it didn't need to bother unsubscribing later.

.. _sect_GGG.2.5:

Radiation Therapy Dose Calculation Push Workflow
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

In this example, users schedule tasks to a shared dose calculation
system and need to track progress. This example is intended as a
demonstration of UPS and should not be taken as prescriptive of RT
Therapy procedures.

Pushing the tasks avoids problems with a pull workflow such as the
server having to continually poll worklists on (a large number of)
possible clients; needing to configure the server to know about all the
clients; reporting results to a user who might be at several locations;
and associating the results with clients automatically. Also, when
performing machines each have unique capabilities, the scheduling must
target individual machines, and there can be advantages for integrating
the scheduling and performing activities like this.

Although not shown in the diagram, the User could have gone to a User
Terminal ("Watcher") and monitored the progress from there by doing a
C-FIND and selecting/subscribing to Task X.

In a second example, the User monitors progress from another User
Terminal ("Watcher") and decides to request cancellation after 3 beams.

.. _sect_GGG.2.6:

X-Ray Clinic Push Workflow
~~~~~~~~~~~~~~~~~~~~~~~~~~

In this example, arriving patients are admitted at the RIS and sent to a
specific X-Ray room for their exam.

The RIS is shown here subscribing globally for events from each Room.
Alternatively the RIS could subscribe individually to each Task right
after the N-CREATE is requested.

It is left open whether the patient demographics have been previously
registered and the patients scheduled on the RIS or whether they are
registered on the RIS when they arrive.

.. _sect_GGG.2.7:

Other Examples
~~~~~~~~~~~~~~

A wide variety of workflow methods are possible using the UPS SOP
Classes. In addition to those diagrammed in the previous sections, a few
more are briefly described here. These include examples of ways to
handle unscheduled tasks, grouped tasks, append cases, "event
forwarding", etc.

**Self-Scheduling Push & Pull: Unscheduled and Append Cases**

In radiation therapy a previously unscheduled ("emergency") procedure
may be performed on a Treatment Delivery System. Normally a TDS performs
scheduled procedures as a Performing SCU in a Typical Pull Workflow like
that shown in GGG.2.2. A TDS that might need to perform unscheduled
procedures could additionally implement UPS Push (as an SCU) and push
the "unscheduled" procedure to the departmental worklist server then
immediately set it IN PROGRESS as a UPS Pull SCU. The initial Push to
the departmental server allows the rest of the departmental workflow to
"sync up" normally to the new task on the schedule.

A modality choosing to append some additional images after the original
UPS was completed could use a similar method. Since the original UPS can
no longer be modified, the modality could push a new UPS instance to the
Worklist Manager and then immediately set it IN PROGRESS. Many of the
Attribute values in the new UPS would be the same as the original UPS.

Note that for a Pull Performer that wants to handle unscheduled cases,
this Push & Pull approach is pretty simple to implement. Becoming a UPS
Push SCU just requires N-CREATE and N-ACTION (Request Cancel) that are
quite similar to the N-SET and N-ACTION it already supports as a UPS
Pull SCU.

The alternative would be implementing both UPS Watch and UPS Event as an
SCP, which would be more work. Further, potential listeners would have
to be aware of and monitor the performing system to track the
unscheduled steps, instead of just monitoring the departmental Pull SCP.

**Self-Scheduling Performer**

An example of an alternative method for handling unscheduled procedures
is a CAD workstation that decides for itself to perform processing on a
study. By implementing UPS Watch as an SCP and UPS Event as an SCP, the
workstation can create UPS instances internally and departmental systems
such as the RIS can subscribe globally to the workstation to monitor its
activities.

The workstation might create the UPS tasks in response to having data
pushed to it, or potentially the workstation could itself also be a
Watch and Event SCU and subscribe globally to relevant modality or PACS
systems and watch for appropriate studies.

**Push Daisy Chain**

Sometimes the performer of the current task is in the best position to
decide what the next task should be.

An alternative to centralized task management is daisy-chaining where
each system pushes the next task to the next performer upon completion
of the current task. Using a workflow similar to the X-Ray Clinic
example in GGG.6, a modality could push a task to a CAD workstation to
process the images created by the modality. The task would specify the
necessary images and perhaps parameters relevant to the acquisition
technique. The RIS could subscribe globally with the CAD workstation to
track events. Another example of push daisy chain would be for the task
completed at each step in a reporting process to be followed by
scheduling the next logical task.

**Hand-offs, Fail-overs and Putting Tasks Back on the Worklist**

Sometimes the performer of the current task, after setting it to IN
PROGRESS, may determine it cannot complete the task and would like the
task performed by another system. It is not permitted to move the task
backwards to the SCHEDULED state.

One approach is for the performer to cancel the old UPS and schedule a
new UPS to be pulled off the worklist by another system or by itself at
some point in the future. The new UPS would be populated with details
from the original. The details of the new UPS, such as the Input
Information Sequence (0040,4021), the Scheduled Workitem Code Sequence
(0040,4018), and the Scheduled Processing Parameters Sequence
(0074,1210), might be revised to reflect any work already completed in
the old UPS. By including the "Discontinued Procedure Step rescheduled"
code in the Procedure Step Discontinuation Reason Code Sequence
(0074,100e) of the old UPS, the performer can allow watchers and other
systems monitoring the task to know that there is a replacement for the
old canceled UPS. By referencing the UID of the old UPS in the Replaced
Procedure Step Sequence (0074,1224) of the new UPS, the performer can
allow watchers and other systems to find the new UPS that replaced the
old. A proactive SCP might even subscribe watchers of the old UPS to the
new UPS that replaces it.

Alternatively, if the performer does not have the capability to create a
new UPS, it could include the "Discontinued Procedure Step rescheduling
recommended" code in the Procedure Step Discontinuation Reason Code
Sequence (0074,100e). A very smart scheduling system could observe the
cancellation reason and create the new replacement UPS as described
above on behalf of the performer.

Another approach is for the performer to "sub-contract" to another
system by pushing a new UPS onto that system and marking the original
UPS complete after the sub-contractor finishes.

Yet another approach would be for the performer to deliver the Locking
UID (by some unspecified mechanism) to another system allowing the new
system to continue the work on the existing UPS. Coordination and
reconciliation would be very important since the new system would need
to review the current contents of the UPS, understand the current state,
update the performing system information, etc.

.. _sect_GGG.3:

Other Features
--------------

.. _sect_GGG.3.1:

What Was Scheduled Vs. What Was Performed
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

The performing system for a UPS instance determines what details to put
in the Attributes of the Performed Procedure Information Module. It is
possible that the procedure performed may differ in some details from
the procedure scheduled. It is up to the performing system to decide how
much the performed procedure can differ from the scheduled procedure
before it is considered a different procedure, or how much must be
performed before the procedure is considered complete.

In the case of cancellation, it is possible that some details of the
situation may be indeterminable. Beyond meeting the Final State
requirements, accurately reflecting in the CANCELED UPS instance the
actual state of the task (e.g., reflecting partial work completed and/or
any cleanup performed during cancellation), is at the discretion of the
performing system.

In general it is expected that:

-  An SCU that completes a UPS differently than described in the
   scheduled details, but accomplishes the intended goal, would record
   the details as performed in the existing UPS and set it to COMPLETED.
   Interested systems may choose to N-GET the Performed Codes from the
   UPS and confirm whether they match the Scheduled Codes.

-  An SCU that completes part of the work described in a UPS, but does
   not accomplish the intended goal, would set the Performed Protocol
   Codes to reflect what work was fully or partially completed, set the
   Output Sequence to reflect the created objects and set the UPS state
   to CANCELED since the goal was not completed.

-  An SCU that completes a step with a different intent and scope in
   place of a scheduled UPS would cancel the original scheduled UPS,
   listing no work output products, and schedule a new UPS describing
   what was actually done, and reference the original UPS that it
   replaces in the Replaced Procedure Step Sequence to facilitate
   monitoring systems "closing the loop".

-  An SCU that completes multiple steps, scheduled as separate UPS
   instances (e.g., a dictation & a transcription & a verification), as
   a block would individually report each of them as completed.

-  An SCU that completes additional unscheduled work in the course of
   completing a scheduled UPS would either report additional procedure
   codes in the completed UPS, or create one or more new UPS instances
   to record the unscheduled work.

.. _sect_GGG.3.2:

Complex Procedure Steps
~~~~~~~~~~~~~~~~~~~~~~~

There are cases where it may be useful to schedule a complex procedure
that is essentially a grouping of multiple workitems. Placing multiple
workitem codes in the Scheduled Workitem Code Sequence is not permitted
(partly due to the additional complexities that would result related to
sequencing, dependency, partial completion, etc.)

One approach is to schedule separate UPS instances for each of the
component workitems and to identify the related UPS instances based on
their use of a common Study UID or Order Number.

Another approach is for the site to define a single workitem code that
means a pre-defined combination of what would otherwise be separate
workitems, along with describing the necessary sequencing, dependencies,
etc.

.. _sect_GGG.3.3:

Gift Subscriptions
~~~~~~~~~~~~~~~~~~

The UPS Subscription allows the Receiving AE Title to be different than
the AE Title of the SCU of the N-ACTION request. This allows an SCU to
sign up someone else who would be interested for a subscription. For
example, a reporting workflow manager could subscribe the RIS to UPSs
the reporting workflow manager creates for radiology studies, and
subscribe the CIS to UPSs it creates for cardiology studies. Or a RIS
could subscribe the MPPS broker or the order tracking system to the high
level UPS instances and save them from having independent business logic
to determine which ones are significant.

This can provide an alternative to systems using global subscriptions to
stay on top of things. It also has the benefit of providing a way to
avoid having to "forward" events. All interested SCUs get their events
directly from the SCP. Instead of SCU A forwarding relevant events to
SCU B, SCU A can simply subscribe SCU B to the relevant events.

