.. _chapter_CC:

Storage Commitment (Informative)
================================

.. _sect_CC.1:

Storage Commitment Examples (Informative)
-----------------------------------------

This Section and its sub-sections contain examples of ways in which the
Storage Commitment Service Class could be used. This is not meant to be
an exhaustive set of scenarios but rather a set of examples.

.. _sect_CC.1.1:

Push Model Example
~~~~~~~~~~~~~~~~~~

`figure_title <#figure_CC.1-1>`__ is an example of the use of the
Storage Commitment Push Model SOP Class.

Node A (an SCU) uses the services of the Storage Service Class to
transmit one or more SOP Instances to Node B (1). Node A then issues an
N-ACTION to Node B (an SCP) containing a list of references to SOP
Instances, requesting that the SCP take responsibility for storage
commitment of the SOP Instances (2). If the SCP has determined that all
SOP Instances exist and that it has successfully completed storage
commitment for the set of SOP Instances, it issues an N-EVENT-REPORT
with the status successful (3) and a list of the stored SOP Instances.
Node A now knows that Node B has accepted the commitment to store the
SOP Instances. Node A might decide that it is now appropriate for it to
delete its copies of the SOP Instances. The N-EVENT-REPORT may or may
not occur on the same Association as the N-ACTION.

If the SCP determines that committed storage can for some reason not be
provided for one or more SOP Instances referenced by the N-ACTION
request, then instead of reporting success it would issue an
N-EVENT-REPORT with a status of completed - failures exists. With the
EVENT-REPORT it would include a list of the SOP Instances that were
successfully stored and also a list of the SOP Instances for which
storage failed.

.. _sect_CC.1.2:

Pull Model Example (Retired)
~~~~~~~~~~~~~~~~~~~~~~~~~~~~

A Pull Model was defined in earlier versions, but has been retired. See
PS3.4-2001.

.. _sect_CC.1.3:

Remote Storage of Data by The SCP
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

`figure_title <#figure_CC.1-3>`__ explains the use of the Retrieve AE
Title. Using the push model a set of SOP Instances will be transferred
from the SCU to the SCP. The SCP may decide to store the data locally
or, alternatively, may decide to store the data at a remote location.
This example illustrates how to handle the latter case.

Node A, an SCU of the Storage Commitment Push Model SOP Class, informs
Node B, an SCP of the corresponding SOP Class, of its wish for storage
commitment by issuing an N-ACTION containing a list of references to SOP
Instances (1). The SOP Instances will already have been transferred from
Node A to Node B (Push Model) (2). If the SCP has determined that
storage commitment has been achieved for all SOP Instances at Node C
specified in the original Storage Commitment Request (from Node A), it
issues an N-EVENT-REPORT (3) like in the previous examples. However, to
inform the SCU about the address of the location at which the data will
be stored, the SCP includes in the N-EVENT-REPORT the Application Entity
Title of Node C.

The Retrieve AE Title can be included in the N-EVENT-REPORT at two
different levels. If all the SOP Instances in question were stored at
Node C, a single Retrieve AE Title could be used for the whole
collection of data. However, the SCP could also choose not to store all
the SOP Instances at the same location. In this case the Retrieve AE
Title Attribute must be provided at the level of each single SOP
Instance in the Referenced SOP Instance Sequence.

This example also applies to the situation where the SCP decides to
store the SOP Instances on Storage Media. Instead of providing the
Retrieve AE Title, the SCP will then provide a pair of Storage Media
File-Set ID and UID.

.. _sect_CC.1.4:

Storage Commitment in Conjunction With Use of Storage Media
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

`figure_title <#figure_CC.1-4>`__ is an example of how to use the Push
Model with Storage Media to perform the actual transfer of the SOP
Instances.

Node A (an SCU) starts out by transferring the SOP Instances for which
committed storage is required to Node B (an SCP) by off-line means on
some kind of Storage Media (1). When the data is believed to have
arrived at Node B, Node A can issue an N-ACTION to Node B containing a
list of references to the SOP Instances contained on the Storage Media,
requesting that the SCP perform storage commitment of these SOP
Instances (2). If the SCP has determined that all the referenced SOP
Instances exist (they may already have been loaded into the system or
they may still reside on the Storage Media) and that it has successfully
completed storage commitment for the SOP Instances, it issues an
N-EVENT-REPORT with the status successful (3) and a list of the stored
SOP Instances like in the previous examples.

If the Storage Media has not yet arrived or if the SCP determines that
committed storage can for some other reason not be provided for one or
more SOP Instances referenced by the N-ACTION request it would issue an
N-EVENT-REPORT with a status of completed - failures exists. With the
EVENT-REPORT it would include a list of the SOP Instances that were
successfully stored and also a list of the SOP Instances for which
storage failed. The SCP is not required to wait for the Storage Media to
arrive (however it may chose to wait) but is free to reject the Storage
Commitment request immediately. If so, the SCU may decide to reissue
another N-ACTION at a later point in time.

