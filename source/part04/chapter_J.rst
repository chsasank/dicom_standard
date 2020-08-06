.. _chapter_J:

Storage Commitment Service Class (Normative)
============================================

.. _sect_J.1:

Overview
--------

.. _sect_J.1.1:

Scope
~~~~~

The mechanism currently defined in DICOM for network based storage of
SOP Instances, the Storage Service Class, allows a Service Class User
(SCU) to transmit images and other Composite SOP Instances to a Service
Class Provider (SCP). However, the Storage Service Class does not
specify that the SCP explicitly take responsibility for the safekeeping
of data into account. That is, there is no commitment that the SCP will
do more than accept the transmitted SOP Instances. In order to have
medical image management in addition to medical image communication,
there is a need for a Service Class within DICOM that ensures that there
is an explicitly defined commitment to store the SOP Instances.

The Storage Commitment Service Class defines an application-level
class-of-service that facilitates this commitment to storage. The
Storage Commitment Service Class enables an Application Entity (AE)
acting as an SCU to request another Application Entity (AE) acting as an
SCP to make the commitment for the safekeeping of the SOP Instances
(i.e., that the SOP Instances will be kept for an implementation
specific period of time and can be retrieved). The AE where such SOP
Instances can later be retrieved may be the SCP where storage commitment
was accepted or it may be distinct from that SCP.

The SCP implementation defines how it provides its commitment to
storage. Certain SCPs may commit to permanently store the SOP Instances
(e.g., an archive system) while other SCPs may commit to provide storage
of the SOP Instances for a limited amount of time. The SCP is required
to document in its Conformance Statement the nature of its commitment to
storage (e.g., duration of storage, retrieve capabilities and latency,
capacity).

The possession of a link to access pixel data shall not be sufficient
for the SCP to commit to storage. A copy of the entire pixel data is
required.

.. note::

   This situation may arise in the context of a JPIP Referenced Pixel
   Data Transfer Syntax.

Once the SCP has accepted the commitment to store the SOP Instances, the
SCU may decide that it is appropriate to delete its copies of the SOP
Instances. These types of policies are outside the scope of this
Standard, however, the SCU is required to document these policies in its
Conformance Statement.

.. _sect_J.1.2:

Models Overview
~~~~~~~~~~~~~~~

The request for storage commitment can be accomplished using the Push
Model.

The Push model expects an SCU to transmit SOP Instances to an SCP using
an appropriate mechanism outside the scope of this Service Class.
Storage commitment is then initiated by transmitting a Storage
Commitment Request containing references to a set of one or more SOP
Instances. Success or failure of storage commitment is subsequently
indicated via a notification from the SCP to the SCU.

.. note::

   1. A Pull Model was defined in earlier versions, but has been
      retired. See PS 3.4-2001.

   2. As indicated, the mechanisms used to transfer SOP Instances from
      an SCU to an SCP are outside the scope of this Service Class.
      However, typical mechanisms are found in the Storage Service
      Class, the Query/Retrieve Service Class, or Media Exchange.

.. _sect_J.2:

Conformance Overview
--------------------

The application-level services addressed by this Service Class are
specified via the Storage Commitment Push Model SOP Class.:

An SCP implementation of the Storage Commitment Service Class shall
support the Storage Commitment Push Model SOP Class.

The SOP Class specifies Attributes, operations, notifications, and
behavior applicable to the SOP Class. The conformance requirements shall
be specified in terms of the Service Class Provider (SCP) and the
Service Class User (SCU).

The Storage Commitment Service Class uses the Storage Commitment IOD as
defined in and the N-ACTION and N-EVENT-REPORT DIMSE Services specified
in .

.. _sect_J.2.1:

Association Negotiation
~~~~~~~~~~~~~~~~~~~~~~~

Association establishment is the first phase of any instance of
communication between peer DICOM AEs. The Association negotiation rules
as specified in shall be used to negotiate the supported SOP Classes.

Support for the SCP/SCU Role Selection Negotiation is mandatory. The SOP
Class Extended Negotiation shall not be supported.

An SCP implementation of the Storage Commitment Service Class shall
support the Storage Commitment Push Model SOP Class.

.. _sect_J.3:

Storage Commitment Push Model SOP Class
---------------------------------------

The Storage Commitment Push Model SOP Class is intended for those
Application Entities requiring storage commitment where the SCU
determines the time at which the SOP Instances are transmitted. The SCU
transmits the SOP Instances to the SCP using an appropriate mechanism.
The request for storage commitment is transmitted to the SCP together
with a list of references to one or more SOP Instances. Success or
failure of storage commitment is subsequently indicated by a
notification from the SCP to the SCU.

.. _sect_J.3.1:

DIMSE Service Group
~~~~~~~~~~~~~~~~~~~

The DIMSE-N Services applicable to the Storage Commitment Push Model SOP
Class are shown in `table_title <#table_J.3.1-1>`__.

.. table:: DIMSE Service Group Applicable to Storage Commitment Push
Model

   ============================= =============
   DICOM Message Service Element Usage SCU/SCP
   ============================= =============
   N-EVENT-REPORT                M/M
   N-ACTION                      M/M
   ============================= =============

The DIMSE-N Services and Protocol are specified in .

.. _sect_J.3.2:

Operations
~~~~~~~~~~

The DICOM AEs that claim conformance to this SOP Class as an SCU shall
invoke the N-ACTION operation. The DICOM AEs that claim conformance to
this SOP Class as an SCP shall support the N-ACTION operation.

.. _sect_J.3.2.1:

Storage Commitment Request
^^^^^^^^^^^^^^^^^^^^^^^^^^

The Storage Commitment Request operation allows an SCU to request an SCP
to commit to the safekeeping of a set of SOP Instances. This operation
shall be invoked through the N-ACTION primitive.

.. _sect_J.3.2.1.1:

Action Information
''''''''''''''''''

The DICOM AEs that claim conformance to this SOP Class as an SCU and/or
an SCP shall support the Action Types and Action Information as
specified in `table_title <#table_J.3-1>`__.

.. table:: Storage Commitment Request - Action Information

   +-------------+-------------+-------------+-------------+-------------+
   | Action Type | Action Type | Attribute   | Tag         | Requirement |
   | Name        | ID          | Name        |             | Type        |
   |             |             |             |             | SCU/SCP     |
   +=============+=============+=============+=============+=============+
   | Request     | 1           | Transaction | (0008,1195) | 1/1         |
   | Storage     |             | UID         |             |             |
   | Commitment  |             |             |             |             |
   +-------------+-------------+-------------+-------------+-------------+
   |             |             | Storage     | (0088,0130) | 3/3         |
   |             |             | Media       |             |             |
   |             |             | File-Set ID |             | See         |
   |             |             |             |             | `Storage    |
   |             |             |             |             | Media File  |
   |             |             |             |             | Set ID      |
   |             |             |             |             | A           |
   |             |             |             |             | ttributes < |
   |             |             |             |             | #sect_J.3.2 |
   |             |             |             |             | .1.1.1>`__. |
   +-------------+-------------+-------------+-------------+-------------+
   |             |             | Storage     | (0088,0140) | 3/3         |
   |             |             | Media       |             |             |
   |             |             | File-Set    |             | See         |
   |             |             | UID         |             | `Storage    |
   |             |             |             |             | Media File  |
   |             |             |             |             | Set ID      |
   |             |             |             |             | A           |
   |             |             |             |             | ttributes < |
   |             |             |             |             | #sect_J.3.2 |
   |             |             |             |             | .1.1.1>`__. |
   +-------------+-------------+-------------+-------------+-------------+
   |             |             | Referenced  | (0008,1199) | 1/1         |
   |             |             | SOP         |             |             |
   |             |             | Sequence    |             |             |
   +-------------+-------------+-------------+-------------+-------------+
   |             |             | >Referenced | (0008,1150) | 1/1         |
   |             |             | SOP Class   |             |             |
   |             |             | UID         |             |             |
   +-------------+-------------+-------------+-------------+-------------+
   |             |             | >Referenced | (0008,1155) | 1/1         |
   |             |             | SOP         |             |             |
   |             |             | Instance    |             | See `SOP    |
   |             |             | UID         |             | Instance    |
   |             |             |             |             | Reference < |
   |             |             |             |             | #sect_J.3.2 |
   |             |             |             |             | .1.1.3>`__. |
   +-------------+-------------+-------------+-------------+-------------+
   |             |             | >Storage    | (0088,0130) | 3/3         |
   |             |             | Media       |             |             |
   |             |             | File-Set ID |             | See         |
   |             |             |             |             | `Storage    |
   |             |             |             |             | Media File  |
   |             |             |             |             | Set ID      |
   |             |             |             |             | A           |
   |             |             |             |             | ttributes < |
   |             |             |             |             | #sect_J.3.2 |
   |             |             |             |             | .1.1.1>`__. |
   +-------------+-------------+-------------+-------------+-------------+
   |             |             | >Storage    | (0088,0140) | 3/3         |
   |             |             | Media       |             |             |
   |             |             | File-Set    |             | See         |
   |             |             | UID         |             | `Storage    |
   |             |             |             |             | Media File  |
   |             |             |             |             | Set ID      |
   |             |             |             |             | A           |
   |             |             |             |             | ttributes < |
   |             |             |             |             | #sect_J.3.2 |
   |             |             |             |             | .1.1.1>`__. |
   +-------------+-------------+-------------+-------------+-------------+

.. _sect_J.3.2.1.1.1:

Storage Media File Set ID Attributes
                                    

If present, the Storage Media File-Set ID (0088,0130) and Storage Media
File-Set UID (0088,0140) shall appear either outside the Referenced SOP
Sequence (0008,1199), or within one or more Items within that sequence,
but not both. If they appear outside of the sequence, then all of the
SOP Instances within the sequence shall be retrievable from the
specified Storage Media File-Set. If they appear within an Item of that
sequence, then the SOP Instance referenced to by that Item shall be
retrievable from the specified Storage Media File-Set.

.. _sect_J.3.2.1.1.2:

Referenced Performed Procedure Step Sequence Attribute (Retired)
                                                                

Referenced Performed Procedure Step Sequence (0008,1111) was included in
earlier versions, but its use here has been retired. See PS 3.4-2001, in
which the Attribute was formerly known as Referenced Study Component
Sequence.

.. note::

   This section formerly specified a means of referencing a Study
   Component that has been completed and semantics that the list of
   images in the commitment request represented a complete set. This
   section has been retired since the Modality Performed Procedure Step
   SOP Classes provide the same facility in a more appropriate service.

.. _sect_J.3.2.1.1.3:

SOP Instance Reference
                      

A SOP Instance may be referenced only once within the Referenced SOP
Sequence (0008,1199).

.. _sect_J.3.2.1.2:

Service Class User Behavior
'''''''''''''''''''''''''''

The SCU shall use the N-ACTION primitive to request the SCP the
safekeeping of a set of SOP Instances. The SOP Instances are referenced
in the Action Information as specified in
`table_title <#table_J.3-1>`__. The Action Type ID shall be set to 1
specifying the request for storage commitment.

The SCU shall supply the Transaction UID Attribute (0008,1195) to
uniquely identify each Storage Commitment Request. The value of the
Transaction UID Attribute will be included by the SCP in the Storage
Commitment Result (see `Storage Commitment Result <#sect_J.3.3.1>`__).
Use of the Transaction UID Attribute allows the SCU to match requests
and results that may occur over the same or different Associations.

The N-ACTION primitive shall contain the well-known Storage Commitment
Push Model SOP Instance UID (defined in `Storage Commitment Push Model
Reserved Identification <#sect_J.3.5>`__) in its Requested SOP Instance
UID parameter.

.. note::

   In the usage described here, there is no explicit creation of a SOP
   Instance upon which an N-ACTION primitive may operate. Instead, the
   N-ACTION primitive operates upon a constant well-known SOP Instance.
   This SOP Instance is conceptually created during start up of each
   Storage Commitment Service Class SCP Application.

Upon receipt of a successful N-ACTION Response Status Code from the SCP,
the SCU now knows that the SCP has received the N-ACTION request. Upon
receipt of any other N-ACTION Response Status Code from the SCP, the SCU
now knows that the SCP will not process the request and therefore will
not commit to the storage of the SOP Instances referenced by the Storage
Commitment Request. The actions taken by the SCU upon receiving the
status is beyond the scope of this Standard. Upon receipt of a failure
status, the Transaction UID is no longer active and shall not be reused
for other transactions.

At any time after receipt of the N-ACTION-Response, the SCU may release
the association on which it sent the N-ACTION-Request.

.. note::

   1. Failure of storage commitment will be signaled via the
      N-EVENT-REPORT primitive.

   2. In situations where the SOP Instance(s) are transferred via Media
      Interchange, the Storage Commitment Request may fail because the
      piece of Media containing the referenced SOP Instance(s) may not
      yet have been read. Attributes (0088,0130) File-Set ID and
      (0088,0140) File-Set UID may or may not be present in the case of
      Media Interchange. They may be provided to facilitate
      identification of the media containing the transferred SOP
      Instance(s) by the Storage Commitment SCP.

.. _sect_J.3.2.1.3:

Service Class Provider Behavior
'''''''''''''''''''''''''''''''

Upon receipt of the N-ACTION request, the SCP shall return, via the
N-ACTION response primitive, the N-ACTION Response Status Code
applicable to the associated request. A success status conveys that the
SCP has successfully received the request. A failure status conveys that
the SCP is not processing the request.

.. note::

   1. Failure of storage commitment will be signaled via the
      N-EVENT-REPORT primitive.

   2. When a Storage Commitment Request is received by an SCP it may
      immediately assess the list of references for which Storage
      Commitment is requested and return an N-EVENT-REPORT. In
      situations where the SOP Instance(s) are transferred via Media
      Interchange, the N-EVENT-REPORT may fail because the piece of
      Media containing the referenced SOP Instance(s) may not yet have
      been read. Attributes (0088,0130) File-Set ID and (0088,0140)
      File-Set UID may or may not be present in the case of Media
      Interchange. They may be used to facilitate identification of the
      media containing the transferred SOP Instance(s) by the Storage
      Commitment SCP.

.. _sect_J.3.2.1.4:

Status Codes
''''''''''''

No Service Class specific status values are defined for the N-ACTION
Service. See for general response status codes.

.. _sect_J.3.3:

Notifications
~~~~~~~~~~~~~

The DICOM AEs that claim conformance to this SOP Class as an SCP shall
invoke the N-EVENT-REPORT request. The DICOM AEs that claim conformance
to this SOP Class as an SCU shall be capable of receiving the
N-EVENT-REPORT request.

.. _sect_J.3.3.1:

Storage Commitment Result
^^^^^^^^^^^^^^^^^^^^^^^^^

The Storage Commitment Result notification allows an SCP to inform the
SCU whether or not it has accepted storage commitment responsibility for
the SOP Instances referenced by a Storage Commitment Request. This
notification is also used to convey error information (i.e., storage
commitment could not be achieved for one or more of the referenced SOP
Instances). This notification shall be invoked through the
N-EVENT-REPORT primitive.

.. _sect_J.3.3.1.1:

Event Information
'''''''''''''''''

The DICOM AEs that claim conformance to this SOP Class as an SCU and/or
an SCP shall support the Event Types and Event Information as specified
in `table_title <#table_J.3-2>`__.

.. table:: Storage Commitment Result - Event Information

   +-------------+-------------+-------------+-------------+-------------+
   | Event Type  | Event Type  | Attribute   | Tag         | Requirement |
   | Name        | ID          | Name        |             | Type        |
   |             |             |             |             | SCU/SCP     |
   +=============+=============+=============+=============+=============+
   | Storage     | 1           | Transaction | (0008,1195) | -/1         |
   | Commitment  |             | UID         |             |             |
   | Request     |             |             |             |             |
   | Successful  |             |             |             |             |
   +-------------+-------------+-------------+-------------+-------------+
   |             |             | Retrieve AE | (0008,0054) | -/3         |
   |             |             | Title       |             |             |
   |             |             |             |             | See         |
   |             |             |             |             | `Retrieve   |
   |             |             |             |             | AE Title    |
   |             |             |             |             | Attribute < |
   |             |             |             |             | #sect_J.3.3 |
   |             |             |             |             | .1.1.1>`__. |
   +-------------+-------------+-------------+-------------+-------------+
   |             |             | Storage     | (0088,0130) | -/3         |
   |             |             | Media       |             |             |
   |             |             | File-Set ID |             | See         |
   |             |             |             |             | `Storage    |
   |             |             |             |             | Media File  |
   |             |             |             |             | Set ID      |
   |             |             |             |             | A           |
   |             |             |             |             | ttributes < |
   |             |             |             |             | #sect_J.3.3 |
   |             |             |             |             | .1.1.2>`__. |
   +-------------+-------------+-------------+-------------+-------------+
   |             |             | Storage     | (0088,0140) | -/3         |
   |             |             | Media       |             |             |
   |             |             | File-Set    |             | See         |
   |             |             | UID         |             | `Storage    |
   |             |             |             |             | Media File  |
   |             |             |             |             | Set ID      |
   |             |             |             |             | A           |
   |             |             |             |             | ttributes < |
   |             |             |             |             | #sect_J.3.3 |
   |             |             |             |             | .1.1.2>`__. |
   +-------------+-------------+-------------+-------------+-------------+
   |             |             | Referenced  | (0008,1199) | -/1         |
   |             |             | SOP         |             |             |
   |             |             | Sequence    |             |             |
   +-------------+-------------+-------------+-------------+-------------+
   |             |             | >Referenced | (0008,1150) | -/1         |
   |             |             | SOP Class   |             |             |
   |             |             | UID         |             |             |
   +-------------+-------------+-------------+-------------+-------------+
   |             |             | >Referenced | (0008,1155) | -/1         |
   |             |             | SOP         |             |             |
   |             |             | Instance    |             |             |
   |             |             | UID         |             |             |
   +-------------+-------------+-------------+-------------+-------------+
   |             |             | >Retrieve   | (0008,0054) | -/3         |
   |             |             | AE Title    |             |             |
   |             |             |             |             | See         |
   |             |             |             |             | `Retrieve   |
   |             |             |             |             | AE Title    |
   |             |             |             |             | Attribute < |
   |             |             |             |             | #sect_J.3.3 |
   |             |             |             |             | .1.1.1>`__. |
   +-------------+-------------+-------------+-------------+-------------+
   |             |             | >Storage    | (0088,0130) | -/3         |
   |             |             | Media       |             |             |
   |             |             | File-Set ID |             | See         |
   |             |             |             |             | `Storage    |
   |             |             |             |             | Media File  |
   |             |             |             |             | Set ID      |
   |             |             |             |             | A           |
   |             |             |             |             | ttributes < |
   |             |             |             |             | #sect_J.3.3 |
   |             |             |             |             | .1.1.2>`__. |
   +-------------+-------------+-------------+-------------+-------------+
   |             |             | >Storage    | (0088,0140) | -/3         |
   |             |             | Media       |             |             |
   |             |             | File-Set    |             | See         |
   |             |             | UID         |             | `Storage    |
   |             |             |             |             | Media File  |
   |             |             |             |             | Set ID      |
   |             |             |             |             | A           |
   |             |             |             |             | ttributes < |
   |             |             |             |             | #sect_J.3.3 |
   |             |             |             |             | .1.1.2>`__. |
   +-------------+-------------+-------------+-------------+-------------+
   | Storage     | 2           | Transaction | (0008,1195) | -/1         |
   | Commitment  |             | UID         |             |             |
   | Request     |             |             |             |             |
   | Complete -  |             |             |             |             |
   | Failures    |             |             |             |             |
   | Exist       |             |             |             |             |
   +-------------+-------------+-------------+-------------+-------------+
   |             |             | Retrieve AE | (0008,0054) | -/3         |
   |             |             | Title       |             |             |
   |             |             |             |             | See         |
   |             |             |             |             | `Retrieve   |
   |             |             |             |             | AE Title    |
   |             |             |             |             | Attribute < |
   |             |             |             |             | #sect_J.3.3 |
   |             |             |             |             | .1.1.1>`__. |
   +-------------+-------------+-------------+-------------+-------------+
   |             |             | Storage     | (0088,0130) | -/3         |
   |             |             | Media       |             |             |
   |             |             | File-Set ID |             | See         |
   |             |             |             |             | `Storage    |
   |             |             |             |             | Media File  |
   |             |             |             |             | Set ID      |
   |             |             |             |             | A           |
   |             |             |             |             | ttributes < |
   |             |             |             |             | #sect_J.3.3 |
   |             |             |             |             | .1.1.2>`__. |
   +-------------+-------------+-------------+-------------+-------------+
   |             |             | Storage     | (0088,0140) | -/3         |
   |             |             | Media       |             |             |
   |             |             | File-Set    |             | See         |
   |             |             | UID         |             | `Storage    |
   |             |             |             |             | Media File  |
   |             |             |             |             | Set ID      |
   |             |             |             |             | A           |
   |             |             |             |             | ttributes < |
   |             |             |             |             | #sect_J.3.3 |
   |             |             |             |             | .1.1.2>`__. |
   +-------------+-------------+-------------+-------------+-------------+
   |             |             | Referenced  | (0008,1199) | -/1C        |
   |             |             | SOP         |             |             |
   |             |             | Sequence    |             | This        |
   |             |             |             |             | Attribute   |
   |             |             |             |             | shall be    |
   |             |             |             |             | provided if |
   |             |             |             |             | storage     |
   |             |             |             |             | commitment  |
   |             |             |             |             | for one or  |
   |             |             |             |             | more SOP    |
   |             |             |             |             | Instances   |
   |             |             |             |             | has been    |
   |             |             |             |             | successful  |
   +-------------+-------------+-------------+-------------+-------------+
   |             |             | >Referenced | (0008,1150) | -/1         |
   |             |             | SOP Class   |             |             |
   |             |             | UID         |             |             |
   +-------------+-------------+-------------+-------------+-------------+
   |             |             | >Referenced | (0008,1155) | -/1         |
   |             |             | SOP         |             |             |
   |             |             | Instance    |             |             |
   |             |             | UID         |             |             |
   +-------------+-------------+-------------+-------------+-------------+
   |             |             | >Retrieve   | (0008,0054) | -/3         |
   |             |             | AE Title    |             |             |
   |             |             |             |             | See         |
   |             |             |             |             | `Retrieve   |
   |             |             |             |             | AE Title    |
   |             |             |             |             | Attribute < |
   |             |             |             |             | #sect_J.3.3 |
   |             |             |             |             | .1.1.1>`__. |
   +-------------+-------------+-------------+-------------+-------------+
   |             |             | >Storage    | (0088,0130) | -/3         |
   |             |             | Media       |             |             |
   |             |             | File-Set ID |             | See         |
   |             |             |             |             | `Storage    |
   |             |             |             |             | Media File  |
   |             |             |             |             | Set ID      |
   |             |             |             |             | A           |
   |             |             |             |             | ttributes < |
   |             |             |             |             | #sect_J.3.3 |
   |             |             |             |             | .1.1.2>`__. |
   +-------------+-------------+-------------+-------------+-------------+
   |             |             | >Storage    | (0088,0140) | -/3         |
   |             |             | Media       |             |             |
   |             |             | File-Set    |             | See         |
   |             |             | UID         |             | `Storage    |
   |             |             |             |             | Media File  |
   |             |             |             |             | Set ID      |
   |             |             |             |             | A           |
   |             |             |             |             | ttributes < |
   |             |             |             |             | #sect_J.3.3 |
   |             |             |             |             | .1.1.2>`__. |
   +-------------+-------------+-------------+-------------+-------------+
   |             |             | Failed SOP  | (0008,1198) | -/1         |
   |             |             | Sequence    |             |             |
   +-------------+-------------+-------------+-------------+-------------+
   |             |             | >Referenced | (0008,1150) | -/1         |
   |             |             | SOP Class   |             |             |
   |             |             | UID         |             |             |
   +-------------+-------------+-------------+-------------+-------------+
   |             |             | >Referenced | (0008,1155) | -/1         |
   |             |             | SOP         |             |             |
   |             |             | Instance    |             |             |
   |             |             | UID         |             |             |
   +-------------+-------------+-------------+-------------+-------------+
   |             |             | >Failure    | (0008,1197) | -/1         |
   |             |             | Reason      |             |             |
   +-------------+-------------+-------------+-------------+-------------+

.. _sect_J.3.3.1.1.1:

Retrieve AE Title Attribute
                           

If present, the Retrieve AE Title (0008,0054) shall appear either
outside the Referenced SOP Sequence (0008,1199), or within one or more
Items within that sequence, but not both. If they appear outside of the
sequence, then all of the SOP Instances within the sequence shall be
retrievable from the specified Retrieve AE Title. If they appear within
an Item of that sequence, then the SOP Instance referenced to by that
Item shall be retrievable from the specified Retrieve AE Title.

.. _sect_J.3.3.1.1.2:

Storage Media File Set ID Attributes
                                    

If present, the Storage Media File-Set ID (0088,0130) and Storage Media
File-Set UID (0088,0140) shall appear either outside the Referenced SOP
Sequence (0008,1199), or within one or more Items within that sequence,
but not both. If they appear outside of the sequence, then all of the
SOP Instances within the sequence shall be retrievable from the
specified Storage Media File-Set. If they appear within an Item of that
sequence, then the SOP Instance referenced to by that Item shall be
retrievable from the specified Storage Media File-Set.

.. _sect_J.3.3.1.2:

Service Class Provider Behavior
'''''''''''''''''''''''''''''''

If the SCP determines that it has successfully completed storage
commitment for all the SOP Instances referenced by a Storage Commitment
Request, the SCP shall issue an N-EVENT-REPORT with the Event Type ID
set to 1 (storage commitment request successful). This event shall
include references to the successfully stored SOP Instances. The SCP
shall store the referenced SOP Instances in accordance with Level 2 as
defined in the Storage Service Class (i.e., all Attributes, including
Private Attributes). The Storage Service Class is defined in . After the
N-EVENT-REPORT has been sent, the Transaction UID is no longer active
and shall not be reused for other transactions.

If it is determined that storage commitment could not be achieved for
one or more referenced SOP Instances, the SCP shall issue an
N-EVENT-REPORT with the Event Type ID set to 2 (storage commitment
request complete - failure exists) conveying that the SCP does not
commit to store all SOP Instances. This event shall include references
to the failed SOP Instances together with references to those SOP
Instances that have been successfully stored. For each failed SOP
Instance the reason for failure shall be described by the Failure Reason
Attribute. After the N-EVENT-REPORT has been sent, the Transaction UID
is no longer active and shall not be reused for other transactions.

The complete set of SOP Instances referenced by the Referenced SOP
Sequence (0008,1199) Attribute, in the initiating N-ACTION, shall be
present in both Event Types either in the Referenced SOP Sequence
(0008,1199) or in the Failed SOP Sequence (0008,1198).

The N-EVENT-REPORT shall include the same Transaction UID Attribute
(0008,1195) value as contained in the initiating N-ACTION.

An SCP shall be capable of issuing the N-EVENT-REPORT on a different
association than the one on which the N-ACTION operation was performed.

.. note::

   1. The SCP may attempt to issue the N-EVENT-REPORT on the same
      Association, but this operation may fail because the SCU is free
      to release at any time the Association on which it sent the
      N-ACTION-Request. As DICOM defaults the association requestor to
      the SCU role, the SCP (i.e., the association requester) negotiates
      an SCP role using the SCU/SCP Role Selection Negotiation (see ).

   2. When responding on a different Association, the SCP must use the
      same AE Title as it used on the original Association, because the
      DICOM Standard defines a Service between two peer applications,
      each identified by an AE Title. Thus the SCP should be
      consistently identified for all Associations in the particular
      instance of the Storage Commitment Service.

   3. The optional Attributes Retrieve AE Title (0008,0054), Storage
      Media File-Set ID (0088,0130) and Storage Media File-Set UID
      (0088,0140) within the Event Information allows an SCP to indicate
      the location where it has stored SOP Instances for safekeeping.
      For example, the SCP could relay SOP Instances to a third
      Application Entity using this Service Class, in which case it can
      use the Retrieve AE Title Attribute to indicate the real location
      of the data. Another example is if the SCP stores data on media,
      it can indicate this using the Storage Media File-Set ID and UID
      Attributes.

.. _sect_J.3.3.1.3:

Service Class User Behavior
'''''''''''''''''''''''''''

An SCU shall be capable of receiving an N-EVENT-REPORT on a different
association than the one on which the N-ACTION operation was performed.

.. note::

   To receive this N-EVENT-REPORT, the SCU accepts an association where
   the SCP role is proposed by the Storage Commitment SCP acting as an
   association requestor.

The SCU shall return, via the N-EVENT-REPORT response primitive, the
N-EVENT-REPORT Response Status Code applicable to the associated
request. The actions taken by the SCU upon receiving the N-EVENT-REPORT
are beyond the scope of this Standard but are stated in its Conformance
Statement.

.. note::

   In the case where the SCP indicates that it cannot achieve storage
   commitment for some SOP Instances, the SCU might, for example,
   re-send the failed SOP Instances to the SCP (via the Storage Service
   Class) and then re-transmit the N-ACTION request. However, this
   behavior is beyond the scope of this Standard.

.. _sect_J.3.3.1.4:

Status Codes
''''''''''''

No Service Class specific status values are defined for the
N-EVENT-REPORT Service. See for general response status codes.

.. note::

   This Section refers to status codes returned by the N-EVENT-REPORT
   response primitive. The Failure Reason Attribute returned in the
   Storage Commitment Result - Event Information (see ) are described in
   the Storage Commitment IOD.

.. _sect_J.3.4:

Storage Commitment Push Model SOP Class UID
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

The Storage Commitment Push Model SOP Class shall be uniquely identified
by the Storage Commitment Push Model SOP Class UID, which shall have the
value "1.2.840.10008.1.20.1".

.. _sect_J.3.5:

Storage Commitment Push Model Reserved Identification
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

The well-known UID of the Storage Commitment Push Model SOP Instance
shall have the value "1.2.840.10008.1.20.1.1".

.. _sect_J.3.6:

Conformance Requirements
~~~~~~~~~~~~~~~~~~~~~~~~

Implementations claiming Standard SOP Class Conformance to the Storage
Commitment Push Model SOP Class shall be conformant as described in this
Section and shall include within their Conformance Statement information
as described in this Section and sub-Sections.

An implementation may claim conformance to this SOP Class as an SCU, SCP
or both. The Conformance Statement shall be in the format defined in .

.. _sect_J.3.6.1:

SCU Conformance
^^^^^^^^^^^^^^^

An implementation that is conformant to this SOP Class as an SCU shall
meet conformance requirements for

-  the operations and actions that it invokes

-  the notifications that it receives.

The mechanisms used by the SCU to transfer SOP Instances to the SCP
shall be documented.

.. _sect_J.3.6.1.1:

Operations
''''''''''

The SCU shall document in the SCU Operations Statement the actions and
behavior that cause the SCU to generate an N-ACTION primitive (Storage
Commitment Request).

The SCU shall specify the SOP Class UIDs for which it may request
storage commitment.

The SCU shall specify the duration of applicability of the Transaction
UID. This may be specified as a time limit or a policy that defines the
end of a transaction (e.g., how long will the SCU wait for a
N-EVENT-REPORT).

The SCU shall specify if it supports the optional Storage Media File-Set
ID & UID Attributes in the N-ACTION. If these Attributes are supported,
the SCU shall also specify which Storage Media Application Profiles are
supported.

The SCU Operations Statement shall be formatted as defined in

.. _sect_J.3.6.1.2:

Notifications.
''''''''''''''

The SCU shall document in the SCU Notifications Statement the behavior
and actions taken by the SCU upon receiving an N-EVENT-REPORT primitive
(Storage Commitment Result).

The SCU shall specify the behavior and actions performed when a success
status is received (i.e., if and when local SOP Instances copies are
deleted).

The SCU shall specify the behavior and actions performed when a failure
status is received (i.e., recovery mechanisms, etc.).

The SCU Notifications Statement shall be formatted as defined in

.. _sect_J.3.6.2:

SCP Conformance.
^^^^^^^^^^^^^^^^

An implementation that is conformant to this SOP Class as an SCP shall
meet conformance requirements for

-  the operations and actions that it performs

-  the notifications that it generates.

.. _sect_J.3.6.2.1:

Operations
''''''''''

The SCP shall document in the SCP Operations Statement the behavior and
actions of the SCP upon receiving the N-ACTION primitive (Storage
Commitment Request).

The SCP shall specify parameters indicating the level of storage
commitment, such as:

-  under what conditions the SCP would delete SOP Instances

-  persistence of storage

-  capacity

-  volatility

-  other pertinent information

The SCP shall specify the mechanisms and characteristics of retrieval of
stored SOP Instances, such as:

-  supported query/retrieve services

-  latency

-  other pertinent information

The SCP shall specify if it supports the optional Storage Media File-Set
ID & UID Attributes in the N-ACTION. If these Attributes are supported,
the SCP shall also specify which Storage Media Application Profiles are
supported.

The SCP Operations Statement shall be formatted as defined in

.. _sect_J.3.6.2.2:

Notifications
'''''''''''''

The SCP shall document in the SCP Notifications Statement the behavior
and actions that cause the SCP to generate an N-EVENT-REPORT primitive
(Storage Commitment Result).

The SCP shall specify if it supports the optional Storage Media File-Set
ID & UID Attributes in the N-EVENT-REPORT and describe the policies for
how the Media is used. The SCP shall also specify which Storage Media
Application Profiles are supported.

The SCP shall specify if it supports the optional Retrieve AE Title
(0008,0054) Attribute in the N-EVENT-REPORT and describe the policies
for how it is used.

The SCP Notifications Statement shall be formatted as defined in

.. _sect_J.4:

Storage Commitment Pull Model SOP Class(Retired)
------------------------------------------------

A Pull Model was defined in earlier versions, but has been retired. See
PS 3.4-2001.

.. _sect_J.5:

Storage Commitment Examples (Informative)
-----------------------------------------

Moved to

