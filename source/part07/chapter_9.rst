.. _chapter_9:

DIMSE-C
=======

.. _sect_9.1:

Services
--------

.. _sect_9.1.1:

C-STORE Service
~~~~~~~~~~~~~~~

The C-STORE service is used by a DIMSE Service User to store a composite
SOP Instance on a peer DIMSE Service User. It is a confirmed service.

.. _sect_9.1.1.1:

C-STORE Parameters
^^^^^^^^^^^^^^^^^^

`table_title <#table_9.1-1>`__ lists the parameters of this service.

.. table:: C-STORE Parameters

   ======================================== =========== ============
   **DIMSE-C Parameter Name**               **Req/Ind** **Rsp/Conf**
   ======================================== =========== ============
   Message ID                               M           U
   Message ID Being Responded To            -           M
   Affected SOP Class UID                   M           U(=)
   Affected SOP Instance UID                M           U(=)
   Priority                                 M           -
   Move Originator Application Entity Title U           -
   Move Originator Message ID               U           -
   Data Set                                 M           -
   Status                                   -           M
   ======================================== =========== ============

.. _sect_9.1.1.1.1:

Message ID
''''''''''

This parameter identifies the operation. It is used to distinguish this
operation from other notifications or operations that the DIMSE Service
Provider may have in progress. No two identical values for the Message
ID (0000,0110) shall be used for outstanding operations or
notifications.

.. note::

   1. Inclusion of this parameter in the confirmation was permitted in
      previous versions of this Standard but this mode of use is now
      retired. This parameter may be included in the confirmation but in
      such a case the invoking DIMSE Service User should not attach any
      semantic significance to this parameter.

   2. The Message ID (0000,0110) is recommended to be unique within the
      scope of an Association, to support debug procedures.

.. _sect_9.1.1.1.2:

Message ID Being Responded To
'''''''''''''''''''''''''''''

This parameter specifies the Message ID (0000,0110) of the operation
request/indication to which this response/confirmation applies.

.. _sect_9.1.1.1.3:

Affected SOP Class UID
''''''''''''''''''''''

For the request/indication, this parameter specifies the SOP Class for
the storage. It may be included in the response/confirmation. If
included in the response/confirmation, this parameter shall be equal to
the value in the request/indication.

.. _sect_9.1.1.1.4:

Affected SOP Instance UID
'''''''''''''''''''''''''

For the request/indication, this parameter specifies the SOP Instance to
be stored. It may be included in the response/confirmation. If included
in the response/confirmation, this parameter shall be equal to the value
in the request/indication.

.. _sect_9.1.1.1.5:

Priority
''''''''

This parameter specifies the priority of the C-STORE operation. It shall
be one of LOW, MEDIUM, or HIGH.

.. _sect_9.1.1.1.6:

Move Originator Application Entity Title
''''''''''''''''''''''''''''''''''''''''

This parameter specifies the DICOM AE Title of the DICOM AE that invoked
the C-MOVE operation from which this C-STORE sub-operation is being
performed.

.. _sect_9.1.1.1.7:

Move Originator Message ID
''''''''''''''''''''''''''

This parameter specifies the Message ID (0000,0110) of the C-MOVE
request/indication primitive from which this C-STORE sub-operation is
being performed.

.. _sect_9.1.1.1.8:

Data Set
''''''''

The Data Set accompanying the C-STORE primitive contains the Attributes
of the Composite SOP Instance to be stored.

.. _sect_9.1.1.1.9:

Status
''''''

This parameter contains the error or success notification for the
operation. It shall be included by the performing DIMSE Service User in
the response/confirmation. The following types of status may occur in a
response/confirmation (see also `Status Type Encoding
(Normative) <#chapter_C>`__):

a. Refused: Out of resources (Status value is Service Class specific) -
   This indicates that the peer DIMSE Service User was unable to store
   the composite SOP Instance because it was out of resources.

b. Refused: SOP Class not supported (0122H) - This indicates that the
   peer DIMSE Service User was unable to store the composite SOP
   Instance because the SOP Class is not supported,

c. Error: Cannot understand (Status value is Service Class specific) -
   This indicates that the peer DIMSE Service User was unable to store
   the composite SOP Instance because it Cannot understand certain Data
   Elements.

d. Error: Data Set does not match SOP Class (Status value is Service
   Class specific) - This indicates that the peer DIMSE Service User was
   unable to store the composite SOP Instance because the Data Set does
   not match the SOP Class.

e. Warning (Status value is Service Class specific) - This indicates
   that the peer DIMSE Service User was able to store the composite SOP
   Instance, but detected a probable error.

f. Success (0000H) - This indicates that the composite SOP Instance was
   successfully stored.

g. Duplicate invocation (0210H) - Indicates that the Message ID
   (0000,0110) specified is allocated to another notification or
   operation.

h. Invalid SOP Instance (0117H) - Indicates that the SOP Instance UID
   specified implied a violation of the UID construction rules.

i. Mistyped argument (0212H) - Indicates that one of the parameters
   supplied has not been agreed for use on the Association between the
   DIMSE Service Users.

j. Unrecognized operation (0211H) - Indicates that the operation is not
   one of those agreed between the DIMSE Service Users.

k. Refused: Not authorized (0124H) - Indicates that the peer DIMSE
   Service User was not authorized to store the composite SOP Instance.

.. _sect_9.1.1.2:

C-STORE Service Procedures
^^^^^^^^^^^^^^^^^^^^^^^^^^

The following C-STORE procedures apply:

a. The invoking DIMSE Service User requests that the performing DIMSE
   Service User store a composite SOP Instance by issuing a C-STORE
   request primitive to the DIMSE Service Provider.

b. The DIMSE Service Provider issues a C-STORE indication primitive to
   the performing DIMSE Service User.

c. The performing DIMSE Service User reports acceptance or rejection of
   the C-STORE request primitive by issuing a C-STORE response primitive
   to the DIMSE Service Provider,

d. The DIMSE Service Provider issues a C-STORE confirmation primitive to
   the invoking DIMSE Service User, completing the C-STORE operation.

The performing DIMSE Service User may return a C-STORE response
primitive with the status of Failed or Refused before the entire C-STORE
indication (Data Set) has been completely transmitted by the invoking
DIMSE Service User. A C-STORE response primitive with the status of
Success or Warning shall not be returned until the entire C-STORE
indication has been received by the performing DIMSE Service User.

.. note::

   Such an occurrence of a "Failed" response is often called an early
   failed response.

.. _sect_9.1.2:

C-FIND Service
~~~~~~~~~~~~~~

The C-FIND service is used by a DIMSE Service User to match a set of
Attributes against the Attributes of a set of composite SOP Instances
maintained by a peer DIMSE Service User. It is a confirmed service.

.. _sect_9.1.2.1:

C-FIND Parameters
^^^^^^^^^^^^^^^^^

See `table_title <#table_9.1-2>`__.

.. table:: C-FIND Parameters

   +-------------------------------+-------------+--------------+---------------------+
   | **DIMSE-C Parameter Name**    | **Req/Ind** | **Rsp/Conf** | **CnclReq/CnclInd** |
   +===============================+=============+==============+=====================+
   | Message ID                    | M           | U            | -                   |
   +-------------------------------+-------------+--------------+---------------------+
   | Message ID Being Responded To | -           | M            | M                   |
   +-------------------------------+-------------+--------------+---------------------+
   | Affected SOP Class UID        | M           | U(=)         | -                   |
   +-------------------------------+-------------+--------------+---------------------+
   | Priority                      | M           | -            | -                   |
   +-------------------------------+-------------+--------------+---------------------+
   | Identifier                    | M           | C            | -                   |
   +-------------------------------+-------------+--------------+---------------------+
   | Status                        | -           | M            | -                   |
   +-------------------------------+-------------+--------------+---------------------+

.. _sect_9.1.2.1.1:

Message ID
''''''''''

This parameter identifies the operation. It is used to distinguish this
operation from other notifications or operations that the DIMSE Service
Provider may have in progress. No two identical values for the Message
ID (0000,0110) shall be used for outstanding operations or
notifications.

.. note::

   1. Inclusion of this parameter in the confirmation was permitted in
      previous versions of this Standard but this mode of use is now
      retired. This parameter may be included in the confirmation but in
      such a case the invoking DIMSE Service User should not attach any
      semantic significance to this parameter.

   2. The Message ID (0000,0110) is recommended to be unique within the
      scope of an Association, to support debug procedures.

.. _sect_9.1.2.1.2:

Message ID Being Responded To
'''''''''''''''''''''''''''''

This parameter specifies the Message ID (0000,0110) of the
request/indication to which this response/confirmation applies.

.. _sect_9.1.2.1.3:

Affected SOP Class UID
''''''''''''''''''''''

For the request/indication, this parameter specifies the SOP Class of
the Information Model for the query. It may be included in the
response/confirmation. If included in the response/confirmation, this
parameter shall be equal to the value in the request/indication.

.. _sect_9.1.2.1.4:

Priority
''''''''

This parameter specifies the priority of the C-FIND operation. It shall
be one of LOW, MEDIUM, or HIGH.

.. _sect_9.1.2.1.5:

Identifier
''''''''''

In the request/indication, this is a list of Attributes to be matched
against the values of the Attributes in the instances of the composite
objects known to the performing DIMSE Service User.

In the response/confirmation, this is the same list of Attributes with
values of these Attributes in a particular composite SOP Instance that
matched. It shall be sent only when that Status (0000,0900) is equal to
Pending (not permitted for other statuses).

The list of Attributes and the rules for construction are specified in .

.. _sect_9.1.2.1.6:

Status
''''''

Indicates the status of the response. It may have any of the following
values (see also `Status Type Encoding (Normative) <#chapter_C>`__):

a. Success (0000H) - This indicates that processing of the matches is
   complete. It shall not contain a matching Identifier.

b. Pending (Status value is Service Class specific) - This indicates
   that processing of the matches is initiated or continuing. It shall
   contain a matching Identifier.

c. Refused: Out of resources (Status value is Service Class specific) -
   Indicates that processing of the C-FIND has been terminated because
   it was out of resources. This may be the initial response to the
   C-FIND, or may be sent after a number of pending C-FIND responses.
   This response shall not contain a matching Identifier.

d. Refused: SOP Class not supported (0122H) - Indicates that processing
   of the C-FIND has been terminated because the SOP Class was not
   supported. This response shall not contain a matching Identifier.

e. Cancel (FE00H) - Indicates that the processing of the C-FIND has been
   terminated due to a C-FIND Cancel indication primitive. The response
   shall not contain an Identifier.

f. Failed (Status value is Service Class specific) - Indicates that the
   C-FIND operation failed at the performing DIMSE Service User.

.. _sect_9.1.2.2:

C-FIND Service Procedures
^^^^^^^^^^^^^^^^^^^^^^^^^

The following C-FIND service procedures apply to the invoking
DIMSE-service user:

a. The invoking DIMSE Service User requests a performing DIMSE Service
   User to match an Identifier against the Attributes of all SOP
   Instances known to the performing DIMSE Service User by issuing a
   C-FIND request primitive to the DIMSE Service Provider. If the
   request is rejected by the DIMSE Service Provider, the following
   procedures do not apply.

b. At any time before receiving a C-FIND confirmation primitive with a
   status unequal to Pending, the invoking DIMSE Service User may
   request the performing DIMSE Service User to cancel the service by
   issuing a C-FIND cancel request primitive to the DIMSE Service
   Provider.

c. The invoking DIMSE Service User receives a C-FIND confirmation
   primitive for each unique match of the Identifier to a set of
   composite SOP Instance Attributes.

d. The invoking DIMSE Service User receives a final C-FIND confirmation
   primitive.

.. note::

   In the above procedures, (c) may precede (b).

The following C-FIND service procedures apply to the performing DIMSE
Service User:

a. When the performing DIMSE Service User receives a C-FIND indication
   from the DIMSE Service Provider, it matches the Identifier against
   the Attributes of known composite SOP Instances.

b. At any time following the C-FIND indication, the performing DIMSE
   Service User may receive a C-FIND cancel indication.

c. If the C-FIND cancel indication is received before the processing of
   the C-FIND indication has completed, then the C-FIND operation is
   aborted; otherwise the following procedure does not apply.

d. The performing DIMSE Service User issues a C-FIND response with a
   status of Canceled to the DIMSE Service Provider to indicate that the
   C-FIND has been canceled. The following procedures do not apply.

e. For each match, the performing DIMSE Service User issues a C-FIND
   response with the status set to Pending and a matching Identifier.

f. When the C-FIND operation completes (either in success or in
   failure), the performing DIMSE Service User issues a C-FIND response
   with the status set to either Refused, Failed, or Success to the
   DIMSE Service Provider.

The following C-FIND service procedures apply to the DIMSE Service
Provider:

a. When the DIMSE Service Provider receives a C-FIND request primitive
   from the invoking DIMSE Service User, it issues a C-FIND indication
   primitive to the performing DIMSE Service User.

b. When the DIMSE Service Provider receives a C-FIND cancel request
   primitive from the invoking DIMSE Service User, it issues a C-FIND
   cancel indication to the performing DIMSE Service User.

c. When the DIMSE Service Provider receives a C-FIND response primitive
   from the performing DIMSE Service User, it issues a C-FIND
   confirmation primitive to the invoking DIMSE Service User.

The performing DIMSE Service User may return a C-FIND response primitive
with the status of Failed or Refused before the entire C-FIND indication
(Data Set) has been completely transmitted by the invoking DIMSE Service
User. A C-FIND response primitive with the status of Success or Warning
shall not be returned until the entire C-FIND indication has been
received by the performing DIMSE Service User.

.. note::

   Such an occurrence of a "Failed" response is often called an early
   failed response.

.. _sect_9.1.3:

C-GET Service
~~~~~~~~~~~~~

The C-GET service is used by a DIMSE Service User to match a set of
Attributes against the Attributes of a set of composite SOP Instances
maintained by a peer DIMSE Service User, and retrieve all composite SOP
Instances that match. It triggers one or more C-STORE sub-operations on
the same Association. It is a confirmed service.

.. _sect_9.1.3.1:

C-GET Parameters
^^^^^^^^^^^^^^^^

See `table_title <#table_9.1-3>`__.

.. table:: C-GET Parameters

   +------------------+-------------+--------------+------------------+
   | **DIMSE-C        | **Req/Ind** | **Rsp/Conf** | **C              |
   | Parameter Name** |             |              | nclReq/CnclInd** |
   +==================+=============+==============+==================+
   | Message ID       | M           | U            | -                |
   +------------------+-------------+--------------+------------------+
   | Message ID Being | -           | M            | M                |
   | Responded To     |             |              |                  |
   +------------------+-------------+--------------+------------------+
   | Affected SOP     | M           | U(=)         | -                |
   | Class UID        |             |              |                  |
   +------------------+-------------+--------------+------------------+
   | Priority         | M           | -            | -                |
   +------------------+-------------+--------------+------------------+
   | Identifier       | M           | U            | -                |
   +------------------+-------------+--------------+------------------+
   | Status           | -           | M            | -                |
   +------------------+-------------+--------------+------------------+
   | Number of        | -           | C            | -                |
   | Remaining        |             |              |                  |
   | Sub-operations   |             |              |                  |
   +------------------+-------------+--------------+------------------+
   | Number of        | -           | C            | -                |
   | Completed        |             |              |                  |
   | Sub-operations   |             |              |                  |
   +------------------+-------------+--------------+------------------+
   | Number of Failed | -           | C            | -                |
   | Sub-operations   |             |              |                  |
   +------------------+-------------+--------------+------------------+
   | Number of        | -           | C            | -                |
   | Warning          |             |              |                  |
   | Sub-operations   |             |              |                  |
   +------------------+-------------+--------------+------------------+

.. _sect_9.1.3.1.1:

Message ID
''''''''''

This parameter identifies the operation. It is used to distinguish this
operation from other notifications or operations that the DIMSE Service
Provider may have in progress. No two identical values for the Message
ID (0000,0110) shall be used for outstanding operations or
notifications.

.. note::

   1. Inclusion of this parameter in the confirmation was permitted in
      previous versions of this Standard but this mode of use is now
      retired. This parameter may be included in the confirmation but in
      such a case the invoking DIMSE Service User should not attach any
      semantic significance to this parameter.

   2. The Message ID (0000,0110) is recommended to be unique within the
      scope of an Association, to support debug procedures.

.. _sect_9.1.3.1.2:

Message ID Being Responded To
'''''''''''''''''''''''''''''

This parameter specifies the Message ID (0000,0110) of the
request/indication to which this response/confirmation applies.

.. _sect_9.1.3.1.3:

Affected SOP Class UID
''''''''''''''''''''''

For the request/indication, this parameter specifies the SOP Class of
the Information Model for the retrieve. It may be included in the
response/confirmation. If included in the response/confirmation, this
parameter shall be equal to the value in the request/indication.

.. _sect_9.1.3.1.4:

Priority
''''''''

This parameter specifies the priority of the C-GET operation. It shall
be one of LOW, MEDIUM or HIGH. This priority shall also be the priority
used for all sub-operations.

.. _sect_9.1.3.1.5:

Identifier
''''''''''

In the request/indication, this is a list of Attributes to be matched
against the values of the Attributes of known composite SOP Instances of
the performing DIMSE Service User. The list of Attributes allowed and
the rules for the construction are specified in .

.. note::

   The Identifier is specified as U in the Response/Confirmation, but
   Services defined in that use this primitive may impose mandatory or
   conditional requirements on its presence.

In the response/confirmation, this is a list of Attributes that provide
status information about the C-GET operation. The list of Attributes
allowed and the rules that define the usage of the Identifier are
specified in .

.. _sect_9.1.3.1.6:

Status
''''''

Indicates the status of the response. It may have any of the following
values (see also `Status Type Encoding (Normative) <#chapter_C>`__):

a. Success (0000H) - This indicates that processing of the matches and
   all sub-operations are complete.

b. Pending (Status value is Service Class specific) - This indicates
   that processing of the matches and sub-operations is initiated or
   continuing.

c. Refused: Out of resources (Status value is Service Class specific) -
   Indicates that processing of the C-GET has been terminated because it
   was out of resources. This may be the initial response to the C-GET
   or may be sent after a number of Pending statuses.

d. Refused: SOP Class not supported (0122H) - Indicates that processing
   of the C-GET has been terminated because the SOP Class was not
   supported.

e. Cancel (FE00H) - Indicates that processing of the C-GET has been
   terminated due to a C-GET Cancel indication primitive.

f. Failed (Status value is Service Class specific) - Indicates that the
   C-GET operation failed at the performing DIMSE Service User.

g. Duplicate invocation (0210H) - Indicates that the Message ID
   (0000,0110) specified is allocated to another notification or
   operation.

h. Mistyped argument (0212H) - Indicates that one of the parameters
   supplied has not been agreed for use on the Association between the
   DIMSE Service Users.

i. Unrecognized operation (0211H) - Indicates that the operation is not
   one of those agreed between the DIMSE Service Users.

j. Refused: Not authorized (0124H) - Indicates that the peer DIMSE
   Service User was not authorized to invoke the C-FIND operation.

k. Warning (Status value is Service Class specific) - This indicates
   that the peer DIMSE Service User was able to perform sub-operations
   but detected a probable error with one or more of them.

.. _sect_9.1.3.1.7:

Number of Remaining Sub-Operations
''''''''''''''''''''''''''''''''''

This specifies the number of remaining C-STORE sub-operations to be
invoked by this C-GET operation. It may be included in any
response/confirmation and shall be included if the status is equal to
Pending.

.. _sect_9.1.3.1.8:

Number of Completed Sub-Operations
''''''''''''''''''''''''''''''''''

This specifies the number of C-STORE sub-operations invoked by this
C-GET operation that have completed successfully. It may be included in
any response/confirmation and shall be included if the status is equal
to Pending.

.. _sect_9.1.3.1.9:

Number of Failed Sub-Operations
'''''''''''''''''''''''''''''''

This specifies the number of C-STORE sub-operations invoked by this
C-GET operation that have failed. It may be included in any
response/confirmation and shall be included if the status is equal to
Pending.

.. _sect_9.1.3.1.10:

Number of Warning Sub-Operations
''''''''''''''''''''''''''''''''

This specifies the number of C-STORE sub-operation invoked by this C-GET
operation that generated Warning responses. It may be included in any
response/confirmation and shall be included if the status is equal to
Pending.

.. _sect_9.1.3.2:

C-GET Service Procedures
^^^^^^^^^^^^^^^^^^^^^^^^

The following C-GET service procedures apply to the invoking
DIMSE-service user:

a. The invoking DIMSE Service User requests a performing DIMSE Service
   User to match an Identifier against the Attributes of all SOP
   Instances known to the performing DIMSE Service User and generate a
   C-STORE sub-operation for each match. This request is made by issuing
   a C-GET request primitive to the DIMSE Service Provider. If the
   request is rejected by the DIMSE Service Provider, the following
   procedures do not apply.

b. At any time before receiving a C-GET confirmation primitive with
   status unequal to Pending, the invoking DIMSE Service User may
   request the performing DIMSE Service User to cancel the service by
   issuing a C-GET cancel request primitive to the DIMSE Service
   Provider.

c. The invoking DIMSE Service User may receive C-GET confirmation
   primitives with status of Pending during the processing of the C-GET
   operation.

d. The invoking DIMSE Service User receives a final C-GET confirmation
   primitive.

.. note::

   In the above procedures, (c) may precede (b).

The following C-GET service procedures apply to the performing DIMSE
Service User:

a. When the performing DIMSE Service User receives a C-GET indication
   from the DIMSE Service Provider it matches the Identifier against the
   Attributes of known composite SOP Instances and generates a C-STORE
   sub-operation for each match.

b. At any time following the C-GET indication, the performing DIMSE
   Service User may receive a C-GET cancel indication.

c. If the C-GET cancel indication is received before the processing of
   the C-GET indication has completed, then the C-GET operation is
   terminated; otherwise the following procedure does not apply.

d. The performing DIMSE Service User issues a C-GET response with a
   status of Canceled to the DIMSE Service Provider to indicate that the
   C-GET has been canceled. The following procedures do not apply.

e. For each match, the performing DIMSE Service User initiates a C-STORE
   sub-operation on the same Association as the C-GET. In this
   sub-operation, the C-GET performing DIMSE Service User becomes the
   C-STORE invoking DIMSE Service User. The C-STORE performing DIMSE
   Service User is the C-GET invoking DIMSE Service User.

f. During the processing of the C-GET operation, the performing DIMSE
   Service User may issue C-GET response primitives with a status of
   Pending.

g. When the C-GET operation completes (either in success or in failure),
   the performing DIMSE Service User issues a C-GET response with the
   status set to either refused, failed or success to the DIMSE Service
   Provider.

The following C-GET service procedures apply to the DIMSE Service
Provider:

a. When the DIMSE Service Provider receives a C-GET request primitive
   from the invoking DIMSE Service User, it issues a C-GET indication
   primitive to the performing DIMSE Service User.

b. When the DIMSE Service Provider receives a C-GET cancel request
   primitive from the invoking DIMSE Service User, it issues a C-GET
   cancel indication to the performing DIMSE Service User.

c. When the DIMSE Service Provider receives a C-GET response primitive
   from the performing DIMSE Service User, it issues a C-GET
   confirmation primitive to the invoking DIMSE Service User.

The performing DIMSE Service User may return a C-GET response primitive
with the status of Failed or Refused before the entire C-GET indication
(Data Set) has been completely transmitted by the invoking DIMSE Service
User. A C-GET response primitive with the status of Success or Warning
shall not be returned until the entire C-GET indication has been
received by the performing DIMSE Service User.

.. note::

   Such an occurrence of a "Failed" response is often called an early
   failed response.

.. _sect_9.1.4:

C-MOVE Service
~~~~~~~~~~~~~~

The C-MOVE service is used by a DIMSE Service User to match a set of
Attributes against the Attributes of a set of composite SOP Instances
maintained by a peer DIMSE Service User, and retrieve all composite SOP
Instances that match. It triggers one or more C-STORE sub-operations on
a separate Association. It is a confirmed service.

.. _sect_9.1.4.1:

C-MOVE Parameters
^^^^^^^^^^^^^^^^^

See `table_title <#table_9.1-4>`__.

.. table:: C-MOVE Parameters

   +------------------+-------------+--------------+------------------+
   | **DIMSE-C        | **Req/Ind** | **Rsp/Conf** | **C              |
   | Parameter Name** |             |              | nclReq/CnclInd** |
   +==================+=============+==============+==================+
   | Message ID       | M           | U            | -                |
   +------------------+-------------+--------------+------------------+
   | Message ID Being | -           | M            | M                |
   | Responded To     |             |              |                  |
   +------------------+-------------+--------------+------------------+
   | Affected SOP     | M           | U(=)         | -                |
   | Class UID        |             |              |                  |
   +------------------+-------------+--------------+------------------+
   | Priority         | M           | -            | -                |
   +------------------+-------------+--------------+------------------+
   | Move Destination | M           | -            | -                |
   +------------------+-------------+--------------+------------------+
   | Identifier       | M           | U            | -                |
   +------------------+-------------+--------------+------------------+
   | Status           | -           | M            | -                |
   +------------------+-------------+--------------+------------------+
   | Number of        | -           | C            | -                |
   | Remaining        |             |              |                  |
   | Sub-operations   |             |              |                  |
   +------------------+-------------+--------------+------------------+
   | Number of        | -           | C            | -                |
   | Completed        |             |              |                  |
   | Sub-operations   |             |              |                  |
   +------------------+-------------+--------------+------------------+
   | Number of Failed | -           | C            | -                |
   | Sub-operations   |             |              |                  |
   +------------------+-------------+--------------+------------------+
   | Number of        | -           | C            | -                |
   | Warning          |             |              |                  |
   | Sub-operations   |             |              |                  |
   +------------------+-------------+--------------+------------------+

.. _sect_9.1.4.1.1:

Message ID
''''''''''

This parameter identifies the operation. It is used to distinguish this
operation from other notifications or operations that the DIMSE Service
Provider may have in progress. No two identical values for the Message
ID (0000,0110) shall be used for outstanding operations or
notifications.

.. note::

   1. Inclusion of this parameter in the confirmation was permitted in
      previous versions of this Standard but this mode of use is now
      retired. This parameter may be included in the confirmation but in
      such a case the invoking DIMSE Service User should not attach any
      semantic significance to this parameter.

   2. The Message ID (0000,0110) is recommended to be unique within the
      scope of an Association, to support debug procedures.

.. _sect_9.1.4.1.2:

Message ID Being Responded To
'''''''''''''''''''''''''''''

This parameter specifies the Message ID (0000,0110) of the
request/indication to which this response/confirmation applies.

.. _sect_9.1.4.1.3:

Affected SOP Class UID
''''''''''''''''''''''

For the request/indication, this parameter specifies the SOP Class of
the Information Model for the retrieve. It may be included in the
response/confirmation. If included in the response/confirmation, this
parameter shall be equal to the value in the request/indication.

.. _sect_9.1.4.1.4:

Priority
''''''''

This parameter specifies the priority of the C-MOVE operation. It shall
be one of LOW, MEDIUM or HIGH . This priority shall also be the priority
used for all sub-operations.

.. _sect_9.1.4.1.5:

Move Destination
''''''''''''''''

This parameter specifies the DICOM AE Title of the destination DICOM AE
to which the C-STORE sub-operations are being performed.

.. _sect_9.1.4.1.6:

Identifier
''''''''''

In the request/indication, this is a list of Attributes to be matched
against the values of the Attributes of known composite SOP Instances of
the performing DIMSE Service User. The list of Attributes allowed and
the rules for the construction are in .

.. note::

   The Identifier is specified as U in the Response/Confirmation, but
   Services defined in that use this primitive may impose mandatory or
   conditional requirements on its presence.

In the response/confirmation, this is a list of Attributes that provide
status information about the C-MOVE operation. The list of Attributes
allowed and the rules that define the usage of the Identifier are
specified in .

.. _sect_9.1.4.1.7:

Status
''''''

Indicates the status of the response. It may have any of the following
values (see also `Status Type Encoding (Normative) <#chapter_C>`__):

a. Success (0000H) - This indicates that processing of the matches and
   all sub-operations are complete.

b. Pending (Status value is Service Class specific) - This indicates
   that procession of the matches and sub-operations is initiated or
   continuing.

c. Refused: Out of resources (Status value is Service Class specific) -
   Indicates that processing of the C-MOVE has been terminated because
   it was out of resources. This may be the initial response to the
   C-MOVE or may be sent after a number of Pending statuses.

d. Refused: SOP Class not supported (0122H) - Indicates that processing
   of the C-MOVE has been terminated because the SOP Class was not
   supported.

e. Refused: Move Destination unknown (Status value is Service Class
   specific) - Indicates that processing of the C-MOVE has been
   terminated because the Move destination was unknown.

f. Cancel (FE00H) - Indicates that processing of the C-MOVE has been
   terminated due to a C-MOVE Cancel indication primitive.

g. Failed (Status value is Service Class specific) - Indicates that the
   C-MOVE operation failed at the performing DIMSE Service User.

h. Duplicate invocation (0210H) - Indicates that the Message ID
   (0000,0110) specified is allocated to another notification or
   operation.

i. Mistyped argument (0212H) - Indicates that one of the parameters
   supplied has not been agreed for use on the Association between the
   DIMSE Service Users.

j. Unrecognized operation (0211H) - Indicates that the operation is not
   one of those agreed between the DIMSE Service Users.

k. Refused: Not authorized (0124H) - Indicates that the peer DIMSE
   Service User was not authorized to invoke the C-MOVE operation.

l. Warning (Status value is Service Class specific) - This indicates
   that the peer DIMSE Service User was able to perform sub-operations
   but detected a probable error with one or more of them.

.. _sect_9.1.4.1.8:

Number of Remaining Sub-Operations
''''''''''''''''''''''''''''''''''

This specifies the number of remaining C-STORE sub-operations to be
invoked by this C-MOVE operation. It may be included in any
response/confirmation and shall be included if the status is equal to
Pending.

.. _sect_9.1.4.1.9:

Number of Completed Sub-Operations
''''''''''''''''''''''''''''''''''

This specifies the number of C-STORE sub-operations invoked by this
C-MOVE operation that have completed successfully. It may be included in
any response/confirmation and shall be included if the status is equal
to Pending.

.. _sect_9.1.4.1.10:

Number of Failed Sub-Operations
'''''''''''''''''''''''''''''''

This specifies the number of C-STORE sub-operations invoked by this
C-MOVE operation that have failed. It may be included in any
response/confirmation and shall be included if the status is equal to
Pending.

.. _sect_9.1.4.1.11:

Number of Warning Sub-Operations
''''''''''''''''''''''''''''''''

This specifies the number of C-STORE sub-operation invoked by this
C-MOVE operation that generated Warning responses. It may be included in
any response/confirmation and shall be included if the status is equal
to Pending.

.. _sect_9.1.4.2:

C-MOVE Service Procedures
^^^^^^^^^^^^^^^^^^^^^^^^^

The following C-MOVE service procedures apply to the invoking
DIMSE-service user:

a. The invoking DIMSE Service User requests a performing DIMSE Service
   User to match an Identifier against the Attributes of all SOP
   Instances known to the performing DIMSE Service User and generate a
   C-STORE sub-operation for each match. This request is made by issuing
   a C-MOVE request primitive to the DIMSE Service Provider. If the
   request is rejected by the DIMSE Service Provider, the following
   procedures do not apply.

b. At any time before receiving a C-MOVE confirmation primitive with
   status unequal to Pending, the invoking DIMSE Service User may
   request the performing DIMSE Service User to cancel the service by
   issuing a C-MOVE cancel request primitive to the DIMSE Service
   Provider.

c. The invoking DIMSE Service User may receive C-MOVE confirmation
   primitives with status of Pending during the processing of the C-MOVE
   operation.

d. The invoking DIMSE Service User receives a final C-MOVE confirmation
   primitive.

.. note::

   in the above procedures, (c) may precede (b).

The following C-MOVE service procedures apply to the performing DIMSE
Service User:

a. When the performing DIMSE Service User receives a C-MOVE indication
   from the DIMSE Service Provider it matches the Identifier against the
   Attributes of known composite SOP Instances and generates a C-STORE
   sub-operation for each match.

b. At any time following the C-MOVE indication, the performing DIMSE
   Service User may receive a C-MOVE cancel indication.

c. If the C-MOVE cancel indication is received before the processing of
   the C-MOVE request has completed, then the C-MOVE operation is
   terminated; otherwise the following procedure does not apply.

d. The performing DIMSE Service User issues a C-MOVE response with a
   status of Canceled to the DIMSE Service Provider to indicate that the
   C-MOVE has been canceled. The following procedures do not apply.

e. For each matching composite SOP Instance, the C-MOVE performing DIMSE
   Service User initiates a C-STORE sub-operation on a different
   Association than the C-MOVE. In this sub-operation, the C-MOVE
   performing DIMSE Service User becomes the C-STORE invoking DIMSE
   Service User. The C-STORE performing DIMSE Service User may or may
   not be the C-MOVE invoking DIMSE Service User.

f. During the processing of the C-MOVE operation, the performing DIMSE
   Service User may issue C-MOVE response primitives with a status of
   Pending.

g. When the C-MOVE operation completes (either in success or in
   failure), the performing DIMSE Service User issues a C-MOVE response
   with the status set to either Refused, Failed, or Success to the
   DIMSE Service Provider.

The following C-MOVE service procedures apply to the DIMSE Service
Provider:

a. When the DIMSE Service Provider receives a C-MOVE request primitive
   from the invoking DIMSE Service User, it issues a C-MOVE indication
   primitive to the performing DIMSE Service User.

b. When the DIMSE Service Provider receives a C-MOVE cancel request
   primitive from the invoking DIMSE Service User, it issues a C-MOVE
   cancel indication to the performing DIMSE Service User.

c. When the DIMSE Service Provider receives a C-MOVE response primitive
   from the performing DIMSE Service User, it issues a C-MOVE
   confirmation primitive to the invoking DIMSE Service User.

The performing DIMSE Service User may return a C-MOVE response primitive
with the status of Failed or Refused before the entire C-MOVE indication
(Data Set) has been completely transmitted by the invoking DIMSE Service
User. A C-MOVE response primitive with the status of Success or Warning
shall not be returned until the entire C-MOVE indication has been
received by the performing DIMSE Service User.

.. note::

   1. Notes: Such an occurrence of a "Failed" response is often called
      an early failed response.

.. _sect_9.1.5:

C-ECHO Service
~~~~~~~~~~~~~~

The C-ECHO service is invoked by a DIMSE Service User to verify
end-to-end communications with a peer DIMSE Service User. It is a
confirmed service.

.. _sect_9.1.5.1:

C-ECHO Parameters
^^^^^^^^^^^^^^^^^

.. table:: C-ECHO Parameters

   ============================= =========== ============
   **DIMSE-C Parameter Name**    **Req/Ind** **Rsp/Conf**
   ============================= =========== ============
   Message ID                    M           U
   Message ID Being Responded To -           M
   Affected SOP Class UID        M           U(=)
   Status                        -           M
   ============================= =========== ============

.. _sect_9.1.5.1.1:

Message ID
''''''''''

This parameter identifies the operation. It is used to distinguish this
operation from other notifications or operations that the DIMSE Service
Provider may have in progress. No two identical values for the Message
ID (0000,0110) shall be used for outstanding operations or
notifications.

.. note::

   1. Inclusion of this parameter in the confirmation was permitted in
      previous versions of this Standard but this mode of use is now
      retired. This parameter may be included in the confirmation but in
      such a case the invoking DIMSE Service User should not attach any
      semantic significance to this parameter.

   2. The Message ID (0000,0110) is recommended to be unique within the
      scope of an Association, to support debug procedures.

.. _sect_9.1.5.1.2:

Message ID Being Responded To
'''''''''''''''''''''''''''''

This parameter specifies the Message ID (0000,0110) of the
request/indication to which this response/ confirmation applies.

.. _sect_9.1.5.1.3:

Affected SOP Class UID
''''''''''''''''''''''

For the request/indication, this parameter specifies the SOP Class of
the SOP Instance for the verification. It may be included in the
response/confirmation. If included in the response/confirmation, this
parameter shall be equal to the value in the request/indication.

.. _sect_9.1.5.1.4:

Status
''''''

Indicates the status of the response. It may have any of the following
values (see also `Status Type Encoding (Normative) <#chapter_C>`__):

a. Success (0000H)

b. Refused: SOP Class not supported (0122H) - Indicates that a different
   SOP Class than the Verification SOP Class was specified, which was
   not supported.

c. Duplicate invocation (0210H) - Indicates that the Message ID
   (0000,0110) specified is allocated to another notification or
   operation.

d. Mistyped argument (0212H) - Indicates that one of the parameters
   supplied has not been agreed for use on the Association between the
   DIMSE Service Users.

e. Unrecognized operation (0211H) - Indicates that a different SOP Class
   than the Verification SOP Class was specified, which does not
   recognize a C-ECHO operation.

.. _sect_9.1.5.2:

C-ECHO Service Procedures
^^^^^^^^^^^^^^^^^^^^^^^^^

The following C-ECHO procedures apply:

a. The invoking DIMSE Service User requests verification of
   communication to the performing DIMSE Service User by issuing a
   C-ECHO request primitive to the DIMSE Service Provider.

b. The DIMSE Service Provider issues a C-ECHO indication primitive to
   the performing DIMSE Service User.

c. The performing DIMSE Service User verifies communication by issuing a
   C-ECHO response primitive to the DIMSE Service Provider.

d. The DIMSE Service Provider issues a C-ECHO confirmation primitive to
   the invoking DIMSE Service User, completing the C-ECHO operation.

.. _sect_9.2:

Sequencing
----------

.. _sect_9.2.1:

Types of Services
~~~~~~~~~~~~~~~~~

All operation and notifications shall be confirmed services.

.. _sect_9.2.2:

Usage Restrictions
~~~~~~~~~~~~~~~~~~

These services may only be invoked within the context of an established
Association.

.. _sect_9.2.3:

Disrupted Procedures
~~~~~~~~~~~~~~~~~~~~

These services do not disrupt any other service procedure.

.. _sect_9.2.4:

Disrupting Procedures
~~~~~~~~~~~~~~~~~~~~~

These services are disrupted by the A-ABORT service procedure.

.. _sect_9.3:

Protocol
--------

This section specifies the protocol necessary to perform the set of
DIMSE-C operations. The Value Representations (VR) specified in the
following tables shall be encoded as defined in .

.. _sect_9.3.1:

C-STORE Protocol
~~~~~~~~~~~~~~~~

The information necessary for the C-STORE request and indication DIMSE-C
primitives are conveyed in the C-STORE-RQ Message. The information
necessary for the C-STORE response and confirmation DIMSE-C primitives
are conveyed in the C-STORE-RSP Message.

.. _sect_9.3.1.1:

C-STORE-RQ
^^^^^^^^^^

The C-STORE-RQ Message contains fields as defined in
`table_title <#table_9.3-1>`__. Each field shall conform to DICOM
encoding and Value Representation as defined in . Fields are required as
specified in the C-STORE service definition unless otherwise noted in
`table_title <#table_9.3-1>`__. Fields not specified in the C-STORE
service definition but present in `table_title <#table_9.3-1>`__ are
required by the DIMSE-C protocol.

.. table:: C-STORE-RQ Message Fields

   +----------------+-------------+--------+--------+----------------+
   | **Message      | **Tag**     | **VR** | **VM** | **Description  |
   | Field**        |             |        |        | of Field**     |
   +================+=============+========+========+================+
   | Command Group  | (0000,0000) | UL     | 1      | The even       |
   | Length         |             |        |        | number of      |
   |                |             |        |        | bytes from the |
   |                |             |        |        | end of the     |
   |                |             |        |        | value field to |
   |                |             |        |        | the beginning  |
   |                |             |        |        | of the next    |
   |                |             |        |        | group.         |
   +----------------+-------------+--------+--------+----------------+
   | Affected SOP   | (0000,0002) | UI     | 1      | SOP Class UID  |
   | Class UID      |             |        |        | of the SOP     |
   |                |             |        |        | Instance to be |
   |                |             |        |        | stored.        |
   +----------------+-------------+--------+--------+----------------+
   | Command Field  | (0000,0100) | US     | 1      | This field     |
   |                |             |        |        | distinguishes  |
   |                |             |        |        | the DIMSE-C    |
   |                |             |        |        | operation      |
   |                |             |        |        | conveyed by    |
   |                |             |        |        | this Message.  |
   |                |             |        |        | The value of   |
   |                |             |        |        | this field     |
   |                |             |        |        | shall be set   |
   |                |             |        |        | to 0001H for   |
   |                |             |        |        | the C-STORE-RQ |
   |                |             |        |        | Message.       |
   +----------------+-------------+--------+--------+----------------+
   | Message ID     | (0000,0110) | US     | 1      | Implement      |
   |                |             |        |        | ation-specific |
   |                |             |        |        | value. It      |
   |                |             |        |        | distinguishes  |
   |                |             |        |        | this Message   |
   |                |             |        |        | from other     |
   |                |             |        |        | Messages.      |
   +----------------+-------------+--------+--------+----------------+
   | Priority       | (0000,0700) | US     | 1      | The priority   |
   |                |             |        |        | shall be set   |
   |                |             |        |        | to one of the  |
   |                |             |        |        | following      |
   |                |             |        |        | values:        |
   |                |             |        |        |                |
   |                |             |        |        | LOW = 0002H    |
   |                |             |        |        |                |
   |                |             |        |        | MEDIUM = 0000H |
   |                |             |        |        |                |
   |                |             |        |        | HIGH = 0001H   |
   +----------------+-------------+--------+--------+----------------+
   | Command Data   | (0000,0800) | US     | 1      | This field     |
   | Set Type       |             |        |        | indicates that |
   |                |             |        |        | a Data Set is  |
   |                |             |        |        | present in the |
   |                |             |        |        | Message. It    |
   |                |             |        |        | shall be set   |
   |                |             |        |        | to any value   |
   |                |             |        |        | other than     |
   |                |             |        |        | 0101H (Null).  |
   +----------------+-------------+--------+--------+----------------+
   | Affected SOP   | (0000,1000) | UI     | 1      | Contains the   |
   | Instance UID   |             |        |        | UID of the SOP |
   |                |             |        |        | Instance to be |
   |                |             |        |        | stored.        |
   +----------------+-------------+--------+--------+----------------+
   | Move           | (0000,1030) | AE     | 1      | Contains the   |
   | Originator     |             |        |        | DICOM AE Title |
   | Application    |             |        |        | of the DICOM   |
   | Entity Title   |             |        |        | AE that        |
   |                |             |        |        | invoked the    |
   |                |             |        |        | C-MOVE         |
   |                |             |        |        | operation from |
   |                |             |        |        | which this     |
   |                |             |        |        | C-STORE        |
   |                |             |        |        | sub-operation  |
   |                |             |        |        | is being       |
   |                |             |        |        | performed.     |
   +----------------+-------------+--------+--------+----------------+
   | Move           | (0000,1031) | US     | 1      | Contains the   |
   | Originator     |             |        |        | Message ID     |
   | Message ID     |             |        |        | (0000,0110) of |
   |                |             |        |        | the C-MOVE-RQ  |
   |                |             |        |        | Message from   |
   |                |             |        |        | which this     |
   |                |             |        |        | C-STORE        |
   |                |             |        |        | sub-operations |
   |                |             |        |        | is being       |
   |                |             |        |        | performed.     |
   +----------------+-------------+--------+--------+----------------+
   | Data Set       | (no tag)    | -      | -      | Applic         |
   |                |             |        |        | ation-specific |
   |                |             |        |        | Data Set.      |
   +----------------+-------------+--------+--------+----------------+

.. note::

   The contents of Composite Information Object Definitions, encoded as
   a series of Data Elements, are defined in and

.. _sect_9.3.1.2:

C-STORE-RSP
^^^^^^^^^^^

The C-STORE-RSP Message contains fields as defined in
`table_title <#table_9.3-2>`__ and in `Status Type Encoding
(Normative) <#chapter_C>`__. Each field shall conform to DICOM encoding
and Value Representation as defined in of the DICOM Standard. Fields are
required as specified in the C-STORE service definition unless otherwise
noted in `table_title <#table_9.3-2>`__. Fields not specified in the
C-STORE service definition but present in `table_title <#table_9.3-2>`__
are required by the DIMSE-C protocol.

.. table:: C-STORE-RSP Message Fields

   +----------------+-------------+--------+--------+----------------+
   | **Message      | **Tag**     | **VR** | **VM** | **Description  |
   | Field**        |             |        |        | of Field**     |
   +================+=============+========+========+================+
   | Command Group  | (0000,0000) | UL     | 1      | The even       |
   | Length         |             |        |        | number of      |
   |                |             |        |        | bytes from the |
   |                |             |        |        | end of the     |
   |                |             |        |        | value field to |
   |                |             |        |        | the beginning  |
   |                |             |        |        | of the next    |
   |                |             |        |        | group.         |
   +----------------+-------------+--------+--------+----------------+
   | Affected SOP   | (0000,0002) | UI     | 1      | Contains the   |
   | Class UID      |             |        |        | SOP Class of   |
   |                |             |        |        | the SOP        |
   |                |             |        |        | Instance       |
   |                |             |        |        | stored.        |
   +----------------+-------------+--------+--------+----------------+
   | Command Field  | (0000,0100) | US     | 1      | This field     |
   |                |             |        |        | distinguishes  |
   |                |             |        |        | the DIMSE-C    |
   |                |             |        |        | operation      |
   |                |             |        |        | conveyed by    |
   |                |             |        |        | this Message.  |
   |                |             |        |        | The value of   |
   |                |             |        |        | this field     |
   |                |             |        |        | shall be set   |
   |                |             |        |        | to 8001H for   |
   |                |             |        |        | the            |
   |                |             |        |        | C-STORE-RSP    |
   |                |             |        |        | Message.       |
   +----------------+-------------+--------+--------+----------------+
   | Message ID     | (0000,0120) | US     | 1      | Shall be set   |
   | Being          |             |        |        | to the value   |
   | Responded To   |             |        |        | of the Message |
   |                |             |        |        | ID (0000,0110) |
   |                |             |        |        | field used in  |
   |                |             |        |        | associated     |
   |                |             |        |        | C-STORE-RQ     |
   |                |             |        |        | Message.       |
   +----------------+-------------+--------+--------+----------------+
   | Command Data   | (0000,0800) | US     | 1      | This field     |
   | Set Type       |             |        |        | indicates that |
   |                |             |        |        | no Data Set is |
   |                |             |        |        | present in the |
   |                |             |        |        | Message and    |
   |                |             |        |        | shall be set   |
   |                |             |        |        | to a value of  |
   |                |             |        |        | 0101H (Null).  |
   +----------------+-------------+--------+--------+----------------+
   | Status         | (0000,0900) | US     | 1      | The value of   |
   |                |             |        |        | this field     |
   |                |             |        |        | depends upon   |
   |                |             |        |        | the status     |
   |                |             |        |        | type. `Status  |
   |                |             |        |        | Type Encoding  |
   |                |             |        |        | (Normative) <  |
   |                |             |        |        | #chapter_C>`__ |
   |                |             |        |        | defines the    |
   |                |             |        |        | encoding of    |
   |                |             |        |        | the status     |
   |                |             |        |        | types defined  |
   |                |             |        |        | in the service |
   |                |             |        |        | definition.    |
   +----------------+-------------+--------+--------+----------------+
   | Affected SOP   | (0000,1000) | UI     | 1      | Contains the   |
   | Instance UID   |             |        |        | UID of the SOP |
   |                |             |        |        | Instance       |
   |                |             |        |        | stored.        |
   +----------------+-------------+--------+--------+----------------+

.. _sect_9.3.1.3:

C-STORE Protocol Procedures
^^^^^^^^^^^^^^^^^^^^^^^^^^^

The C-STORE procedures are initiated by the invoking DIMSE Service User
issuing a C-STORE request primitive. On receipt of the C-STORE request
primitive the DIMSE-C protocol machine shall:

-  construct a Message conveying the C-STORE-RQ

-  send the Message using the P-DATA request service (see 8.1)

On receipt of a Message conveying a C-STORE-RQ the DIMSE-C protocol
machine shall issue a C-STORE indication primitive to the performing
DIMSE Service User.

On receipt of the C-STORE response primitive, issued by the performing
DIMSE Service User, the DIMSE-C protocol machine shall:

-  construct a Message conveying the C-STORE-RSP

-  send the Message using the P-DATA request service (see 8.1)

On receipt of a Message conveying a C-STORE-RSP the DIMSE-C protocol
machine shall issue a C-STORE confirmation primitive to the invoking
DIMSE Service User, thus completing the C-STORE procedure.

The performing DIMSE Service User may return a C-STORE-RSP with the
status of Failed or Refused before the complete C-STORE-RQ request
Message has been completely transmitted by the invoking DIMSE Service
User (this is called an early failed response). Upon receipt of this
Failed or Refused C-STORE-RSP the invoking DIMSE Service User may
terminate the Message before it is completely sent (i.e., set the Last
Fragment bit to 1 in a Data PDV for this Message, see `Usage of the
P-DATA Service By the DICOM Application Entity
(Normative) <#chapter_F>`__). Following this, it may invoke another
operation or notification. It is a protocol violation for an invoking
DIMSE Service User to set the Last Fragment bit to 1 before a C-STORE-RQ
Message has been completely transmitted if it has not received a Failed
or Refused C-STORE-RSP to that request.

.. note::

   When an Association is operating in asynchronous mode, it is possible
   for an invoking DIMSE Service User to transmit several Messages
   before a response. Therefore, while sending a Message it may receive
   a response to a previously transmitted Message. In this case this
   response is not an early failed response because the related Message
   has already been sent.

.. _sect_9.3.2:

C-FIND Protocol
~~~~~~~~~~~~~~~

The information necessary for the C-FIND request and indication DIMSE-C
primitives are conveyed in the C-FIND-RQ Message. The information
necessary for the C-FIND response and confirmation DIMSE-C primitives
are conveyed in the C-FIND-RSP Message. The information necessary for
the C-FIND Cancel Request and Cancel Indication primitives are conveyed
in the C-CANCEL-FIND-RQ Message.

.. _sect_9.3.2.1:

C-FIND-RQ
^^^^^^^^^

The C-FIND-RQ Message contains fields as defined in
`table_title <#table_9.3-3>`__. Each field shall conform to DICOM
encoding and Value Representation as defined in . Fields are required as
specified in the C-FIND service definition unless otherwise noted in
`table_title <#table_9.3-3>`__. Fields not specified in the C-FIND
service definition but present in `table_title <#table_9.3-3>`__ are
required by the DIMSE-C protocol.

.. table:: C-FIND-RQ Message Fields

   +----------------+-------------+--------+--------+----------------+
   | **Message      | **Tag**     | **VR** | **VM** | **Description  |
   | Field**        |             |        |        | of Field**     |
   +================+=============+========+========+================+
   | Command Group  | (0000,0000) | UL     | 1      | The even       |
   | Length         |             |        |        | number of      |
   |                |             |        |        | bytes from the |
   |                |             |        |        | end of the     |
   |                |             |        |        | value field to |
   |                |             |        |        | the beginning  |
   |                |             |        |        | of the next    |
   |                |             |        |        | group.         |
   +----------------+-------------+--------+--------+----------------+
   | Affected SOP   | (0000,0002) | UI     | 1      | SOP Class UID  |
   | Class UID      |             |        |        | associated     |
   |                |             |        |        | with this      |
   |                |             |        |        | operation.     |
   +----------------+-------------+--------+--------+----------------+
   | Command Field  | (0000,0100) | US     | 1      | This field     |
   |                |             |        |        | distinguishes  |
   |                |             |        |        | the DIMSE-C    |
   |                |             |        |        | operation      |
   |                |             |        |        | conveyed by    |
   |                |             |        |        | this Message.  |
   |                |             |        |        | The value of   |
   |                |             |        |        | this field     |
   |                |             |        |        | shall be set   |
   |                |             |        |        | to 0020H for   |
   |                |             |        |        | the C-FIND-RQ  |
   |                |             |        |        | Message.       |
   +----------------+-------------+--------+--------+----------------+
   | Message ID     | (0000,0110) | US     | 1      | Implement      |
   |                |             |        |        | ation-specific |
   |                |             |        |        | value that     |
   |                |             |        |        | distinguishes  |
   |                |             |        |        | this Message   |
   |                |             |        |        | from other     |
   |                |             |        |        | Messages.      |
   +----------------+-------------+--------+--------+----------------+
   | Priority       | (0000,0700) | US     | 1      | The priority   |
   |                |             |        |        | shall be set   |
   |                |             |        |        | to one of the  |
   |                |             |        |        | following      |
   |                |             |        |        | values:        |
   |                |             |        |        |                |
   |                |             |        |        | LOW = 0002H    |
   |                |             |        |        |                |
   |                |             |        |        | MEDIUM = 0000H |
   |                |             |        |        |                |
   |                |             |        |        | HIGH = 0001H   |
   +----------------+-------------+--------+--------+----------------+
   | Command Data   | (0000,0800) | US     | 1      | This field     |
   | Set Type       |             |        |        | indicates that |
   |                |             |        |        | a Data Set is  |
   |                |             |        |        | present in the |
   |                |             |        |        | Message. It    |
   |                |             |        |        | shall be set   |
   |                |             |        |        | to any value   |
   |                |             |        |        | other than     |
   |                |             |        |        | 0101H (Null).  |
   +----------------+-------------+--------+--------+----------------+
   | Identifier     | (no tag)    | -      | -      | A Data Set     |
   |                |             |        |        | that encodes   |
   |                |             |        |        | the Identifier |
   |                |             |        |        | to be matched. |
   |                |             |        |        | See            |
   |                |             |        |        | `Iden          |
   |                |             |        |        | tifier <#sect_ |
   |                |             |        |        | 9.1.2.1.5>`__. |
   +----------------+-------------+--------+--------+----------------+

.. note::

   Implementations that require compatibility to previous versions of
   this Standard must set the Command Data Set Type (0000,0800) Field to
   0102H (Identifier).

.. _sect_9.3.2.2:

C-FIND-RSP
^^^^^^^^^^

The C-FIND-RSP Message contains fields as defined in
`table_title <#table_9.3-4>`__ and in `Status Type Encoding
(Normative) <#chapter_C>`__. Each field shall conform to DICOM encoding
and Value Representation as defined in . Fields are required as
specified in the C-FIND service definition unless otherwise noted in
`table_title <#table_9.3-4>`__. Fields not specified in the C-FIND
service definition but present in `table_title <#table_9.3-4>`__ are
required by the DIMSE-C protocol.

.. table:: C-FIND-RSP Message Fields

   +----------------+-------------+--------+--------+----------------+
   | **Message      | **Tag**     | **VR** | **VM** | **Description  |
   | Field**        |             |        |        | of Field**     |
   +================+=============+========+========+================+
   | Command Group  | (0000,0000) | UL     | 1      | The even       |
   | Length         |             |        |        | number of      |
   |                |             |        |        | bytes from the |
   |                |             |        |        | end of the     |
   |                |             |        |        | value field to |
   |                |             |        |        | the beginning  |
   |                |             |        |        | of the next    |
   |                |             |        |        | group.         |
   +----------------+-------------+--------+--------+----------------+
   | Affected SOP   | (0000,0002) | UI     | 1      | SOP Class UID  |
   | Class UID      |             |        |        | associated     |
   |                |             |        |        | with the       |
   |                |             |        |        | operation.     |
   +----------------+-------------+--------+--------+----------------+
   | Command Field  | (0000,0100) | US     | 1      | This field     |
   |                |             |        |        | distinguishes  |
   |                |             |        |        | the DIMSE-C    |
   |                |             |        |        | operation      |
   |                |             |        |        | conveyed by    |
   |                |             |        |        | this Message.  |
   |                |             |        |        | The value of   |
   |                |             |        |        | this field     |
   |                |             |        |        | shall be set   |
   |                |             |        |        | to 8020H for   |
   |                |             |        |        | the C-FIND-RSP |
   |                |             |        |        | Message.       |
   +----------------+-------------+--------+--------+----------------+
   | Message ID     | (0000,0120) | US     | 1      | Shall be set   |
   | Being          |             |        |        | to the value   |
   | Responded To   |             |        |        | of the Message |
   |                |             |        |        | ID (0000,0110) |
   |                |             |        |        | field used in  |
   |                |             |        |        | associated     |
   |                |             |        |        | C-FIND-RQ      |
   |                |             |        |        | Message.       |
   +----------------+-------------+--------+--------+----------------+
   | Command Data   | (0000,0800) | US     | 1      | This field     |
   | Set Type       |             |        |        | indicates if a |
   |                |             |        |        | Data Set is    |
   |                |             |        |        | present in the |
   |                |             |        |        | Message. This  |
   |                |             |        |        | field shall be |
   |                |             |        |        | set to the     |
   |                |             |        |        | value of 0101H |
   |                |             |        |        | (Null) if no   |
   |                |             |        |        | Data Set is    |
   |                |             |        |        | present; any   |
   |                |             |        |        | other value    |
   |                |             |        |        | indicates a    |
   |                |             |        |        | Data Set is    |
   |                |             |        |        | included in    |
   |                |             |        |        | the Message.   |
   +----------------+-------------+--------+--------+----------------+
   | Status         | (0000,0900) | US     | 1      | The value of   |
   |                |             |        |        | this field     |
   |                |             |        |        | depends upon   |
   |                |             |        |        | the status     |
   |                |             |        |        | type. `Status  |
   |                |             |        |        | Type Encoding  |
   |                |             |        |        | (Normative) <  |
   |                |             |        |        | #chapter_C>`__ |
   |                |             |        |        | defines the    |
   |                |             |        |        | encoding of    |
   |                |             |        |        | the status     |
   |                |             |        |        | types defined  |
   |                |             |        |        | in the service |
   |                |             |        |        | definition.    |
   +----------------+-------------+--------+--------+----------------+
   | Identifier     | (no tag)    | -      | -      | A Data Set     |
   |                |             |        |        | that encodes   |
   |                |             |        |        | the Identifier |
   |                |             |        |        | that was       |
   |                |             |        |        | matched. See   |
   |                |             |        |        | `Iden          |
   |                |             |        |        | tifier <#sect_ |
   |                |             |        |        | 9.1.2.1.5>`__. |
   +----------------+-------------+--------+--------+----------------+

.. _sect_9.3.2.3:

C-CANCEL-FIND-RQ
^^^^^^^^^^^^^^^^

The C-CANCEL-FIND-RQ Message contains fields as defined in
`table_title <#table_9.3-5>`__. Each field shall conform to DICOM
encoding and Value Representation as defined in . Fields are required as
specified in the C-FIND service definition unless otherwise noted in
`table_title <#table_9.3-5>`__. Fields not specified in the C-FIND
service definition but present in `table_title <#table_9.3-5>`__ are
required by the DIMSE-C protocol.

.. table:: C-CANCEL-FIND-RQ Message Fields

   +----------------+-------------+--------+--------+----------------+
   | **Message      | **Tag**     | **VR** | **VM** | **Description  |
   | Field**        |             |        |        | of Field**     |
   +================+=============+========+========+================+
   | Command Group  | (0000,0000) | UL     | 1      | The even       |
   | Length         |             |        |        | number of      |
   |                |             |        |        | bytes from the |
   |                |             |        |        | end of the     |
   |                |             |        |        | value field to |
   |                |             |        |        | the beginning  |
   |                |             |        |        | of the next    |
   |                |             |        |        | group.         |
   +----------------+-------------+--------+--------+----------------+
   | Command Field  | (0000,0100) | US     | 1      | This field     |
   |                |             |        |        | distinguishes  |
   |                |             |        |        | the DIMSE-C    |
   |                |             |        |        | operation      |
   |                |             |        |        | conveyed by    |
   |                |             |        |        | this Message.  |
   |                |             |        |        | The value of   |
   |                |             |        |        | this field     |
   |                |             |        |        | shall be set   |
   |                |             |        |        | to 0FFFH for   |
   |                |             |        |        | the            |
   |                |             |        |        | C-             |
   |                |             |        |        | CANCEL-FIND-RQ |
   |                |             |        |        | Message.       |
   +----------------+-------------+--------+--------+----------------+
   | Message ID     | (0000,0120) | US     | 1      | Shall be set   |
   | Being          |             |        |        | to the value   |
   | Responded To   |             |        |        | of the Message |
   |                |             |        |        | ID (0000,0110) |
   |                |             |        |        | field used in  |
   |                |             |        |        | associated     |
   |                |             |        |        | C-FIND-RQ      |
   |                |             |        |        | Message.       |
   +----------------+-------------+--------+--------+----------------+
   | Command Data   | (0000,0800) | US     | 1      | This field     |
   | Set Type       |             |        |        | indicates that |
   |                |             |        |        | no Data Set is |
   |                |             |        |        | present in the |
   |                |             |        |        | Message and    |
   |                |             |        |        | shall be set   |
   |                |             |        |        | to a value of  |
   |                |             |        |        | 0101H.         |
   +----------------+-------------+--------+--------+----------------+

.. _sect_9.3.2.4:

C-FIND Protocol Procedures
^^^^^^^^^^^^^^^^^^^^^^^^^^

The C-FIND procedures are initiated by the invoking DIMSE Service User
issuing a C-FIND request primitive. On receipt of the C-FIND request
primitive the DIMSE-C protocol machine shall:

-  construct a Message conveying the C-FIND-RQ

-  send the Message using the P-DATA request service (see 8.1)

On receipt of a Message conveying a C-FIND-RQ the DIMSE-C protocol
machine shall issue a C-FIND indication primitive to the performing
DIMSE Service User.

The DIMSE-C protocol machine shall:

-  accept zero or more C-FIND response primitives containing the status
   of Pending, issued by the performing DIMSE Service User, followed by
   a single C-FIND response primitive containing the final status

-  for each C-FIND response primitive containing the Pending status the
   DIMSE-C protocol machine shall:

   a. construct a Message conveying the (Pending) C-FIND-RSP

   b. send the Message using the P-DATA request service (see 8.1)

-  for the C-FIND response primitive containing the final status the
   DIMSE-C protocol machine shall:

   a. construct a Message conveying the (final) C-FIND-RSP

   b. end the Message using the P-DATA request service (see 8.1)

On receipt of a Message conveying a C-FIND-RSP the DIMSE-C protocol
machine shall:

-  if the Message indicates the status of Pending, issue a C-FIND
   confirmation primitive to the invoking DIMSE Service User with a
   Pending status

-  if the Message indicates a final status, issue a C-FIND confirmation
   primitive to the invoking DIMSE Service User with a final status,
   thus completing the C-FIND procedure

.. note::

   The C-FIND procedures can be canceled at any time by the invoking
   DIMSE Service User. This is accomplished by the invoking DIMSE
   Service User issuing a C-CANCEL request primitive.

The performing DIMSE Service User may return a C-FIND-RSP with the
status of Failed or Refused before the complete C-FIND-RQ request
Message has been completely transmitted by the invoking DIMSE Service
User (this is called an early failed response). Upon receipt of this
Failed or Refused C-FIND-RSP the invoking DIMSE Service User may
terminate the Message before it is completely sent (i.e., set the Last
Fragment bit to 1 in a Data PDV for this Message, see `Usage of the
P-DATA Service By the DICOM Application Entity
(Normative) <#chapter_F>`__). Following this, it may invoke another
operation or notification. It is a protocol violation for an invoking
DIMSE Service User to set the Last Fragment bit to 1 before a C-FIND-RQ
Message has been completely transmitted if it has not received a Failed
or Refused C-FIND-RSP to that request.

.. note::

   When an Association is operating in asynchronous mode, it is possible
   for an invoking DIMSE Service User to transmit several Messages
   before a response. Therefore, while sending a Message it may receive
   a response to a previously transmitted Message. In this case this
   response is not an early failed response because the related Message
   has already been sent.

.. _sect_9.3.3:

C-GET Protocol
~~~~~~~~~~~~~~

The information necessary for the C-GET request and indication DIMSE-C
primitives are conveyed in the C-GET-RQ Message. The information
necessary for the C-GET response and confirmation DIMSE-C primitives are
conveyed in the C-GET-RSP Message. The information necessary for the
C-GET Cancel Request and Cancel Indication primitives are conveyed in
the C-CANCEL-GET-RQ Message.

.. _sect_9.3.3.1:

C-GET-RQ
^^^^^^^^

The C-GET-RQ Message contains fields as defined in
`table_title <#table_9.3-6>`__. Each field shall conform to DICOM
encoding and Value Representation as defined in . Fields are required as
specified in the C-GET service definition unless otherwise noted in
`table_title <#table_9.3-6>`__. Fields not specified in the C-GET
service definition but present in `table_title <#table_9.3-6>`__ are
required by the DIMSE-C protocol.

.. table:: C-GET-RQ Message Fields

   +----------------+-------------+--------+--------+----------------+
   | **Message      | **Tag**     | **VR** | **VM** | **Description  |
   | Field**        |             |        |        | of Field**     |
   +================+=============+========+========+================+
   | Command Group  | (0000,0000) | UL     | 1      | The even       |
   | Length         |             |        |        | number of      |
   |                |             |        |        | bytes from the |
   |                |             |        |        | end of the     |
   |                |             |        |        | value field to |
   |                |             |        |        | the beginning  |
   |                |             |        |        | of the next    |
   |                |             |        |        | group.         |
   +----------------+-------------+--------+--------+----------------+
   | Affected SOP   | (0000,0002) | UI     | 1      | SOP Class UID  |
   | Class UID      |             |        |        | associated     |
   |                |             |        |        | with this      |
   |                |             |        |        | operation.     |
   +----------------+-------------+--------+--------+----------------+
   | Command Field  | (0000,0100) | US     | 1      | This field     |
   |                |             |        |        | distinguishes  |
   |                |             |        |        | the DIMSE-C    |
   |                |             |        |        | operation      |
   |                |             |        |        | conveyed by    |
   |                |             |        |        | this Message.  |
   |                |             |        |        | The value of   |
   |                |             |        |        | this field     |
   |                |             |        |        | shall be set   |
   |                |             |        |        | to 0010H for   |
   |                |             |        |        | the C-GET-RQ   |
   |                |             |        |        | Message.       |
   +----------------+-------------+--------+--------+----------------+
   | Message ID     | (0000,0110) | US     | 1      | Implement      |
   |                |             |        |        | ation-specific |
   |                |             |        |        | value that     |
   |                |             |        |        | distinguishes  |
   |                |             |        |        | this Message   |
   |                |             |        |        | from other     |
   |                |             |        |        | Messages.      |
   +----------------+-------------+--------+--------+----------------+
   | Priority       | (0000,0700) | US     | 1      | The priority   |
   |                |             |        |        | shall be set   |
   |                |             |        |        | to one of the  |
   |                |             |        |        | following      |
   |                |             |        |        | values:        |
   |                |             |        |        |                |
   |                |             |        |        | LOW = 0002H    |
   |                |             |        |        |                |
   |                |             |        |        | MEDIUM = 0000H |
   |                |             |        |        |                |
   |                |             |        |        | HIGH = 0001H   |
   +----------------+-------------+--------+--------+----------------+
   | Command Data   | (0000,0800) | US     | 1      | This field     |
   | Set Type       |             |        |        | indicates that |
   |                |             |        |        | a Data Set is  |
   |                |             |        |        | present in the |
   |                |             |        |        | Message. It    |
   |                |             |        |        | shall be set   |
   |                |             |        |        | to any value   |
   |                |             |        |        | other than     |
   |                |             |        |        | 0101H (Null).  |
   +----------------+-------------+--------+--------+----------------+
   | Identifier     | (no tag)    | -      | -      | A Data Set     |
   |                |             |        |        | that encodes   |
   |                |             |        |        | attributes     |
   |                |             |        |        | providing      |
   |                |             |        |        | status         |
   |                |             |        |        | information    |
   |                |             |        |        | about the      |
   |                |             |        |        | C-GET          |
   |                |             |        |        | operation. See |
   |                |             |        |        | `Iden          |
   |                |             |        |        | tifier <#sect_ |
   |                |             |        |        | 9.1.3.1.5>`__. |
   +----------------+-------------+--------+--------+----------------+

.. note::

   Implementations that require compatibility to previous versions of
   this Standard must set the Command Data Set Type (0000,0800) Field to
   0102H (Identifier).

.. _sect_9.3.3.2:

C-GET-RSP
^^^^^^^^^

The C-GET-RSP Message contains fields as defined in
`table_title <#table_9.3-7>`__ and in `Status Type Encoding
(Normative) <#chapter_C>`__. Each field shall conform to DICOM encoding
and Value Representation as defined in . Fields are required as
specified in the C-GET service definition unless otherwise noted in
`table_title <#table_9.3-7>`__. Fields not specified in the C-GET
service definition but present in `table_title <#table_9.3-7>`__ are
required by the DIMSE-C protocol.

.. table:: C-GET-RSP Message Fields

   +----------------+-------------+--------+--------+----------------+
   | **Message      | **Tag**     | **VR** | **VM** | **Description  |
   | Field**        |             |        |        | of Field**     |
   +================+=============+========+========+================+
   | Command Group  | (0000,0000) | UL     | 1      | The even       |
   | Length         |             |        |        | number of      |
   |                |             |        |        | bytes from the |
   |                |             |        |        | end of the     |
   |                |             |        |        | value field to |
   |                |             |        |        | the beginning  |
   |                |             |        |        | of the next    |
   |                |             |        |        | group.         |
   +----------------+-------------+--------+--------+----------------+
   | Affected SOP   | (0000,0002) | UI     | 1      | SOP Class UID  |
   | Class UID      |             |        |        | associated     |
   |                |             |        |        | with the       |
   |                |             |        |        | operation.     |
   +----------------+-------------+--------+--------+----------------+
   | Command Field  | (0000,0100) | US     | 1      | This field     |
   |                |             |        |        | distinguishes  |
   |                |             |        |        | the DIMSE-C    |
   |                |             |        |        | operation      |
   |                |             |        |        | conveyed by    |
   |                |             |        |        | this Message.  |
   |                |             |        |        | The value of   |
   |                |             |        |        | this field     |
   |                |             |        |        | shall be set   |
   |                |             |        |        | to 8010H for   |
   |                |             |        |        | the C-GET-RSP  |
   |                |             |        |        | Message.       |
   +----------------+-------------+--------+--------+----------------+
   | Message ID     | (0000,0120) | US     | 1      | Shall be set   |
   | Being          |             |        |        | to the value   |
   | Responded To   |             |        |        | of the Message |
   |                |             |        |        | ID (0000,0110) |
   |                |             |        |        | field used in  |
   |                |             |        |        | associated     |
   |                |             |        |        | C-GET-RQ       |
   |                |             |        |        | Message.       |
   +----------------+-------------+--------+--------+----------------+
   | Command Data   | (0000,0800) | US     | 1      | This field     |
   | Set Type       |             |        |        | indicates if a |
   |                |             |        |        | Data Set is    |
   |                |             |        |        | present in the |
   |                |             |        |        | Message. This  |
   |                |             |        |        | field shall be |
   |                |             |        |        | set to the     |
   |                |             |        |        | value of 0101H |
   |                |             |        |        | (Null) if no   |
   |                |             |        |        | Data Set is    |
   |                |             |        |        | present; any   |
   |                |             |        |        | other value    |
   |                |             |        |        | indicates a    |
   |                |             |        |        | Data Set is    |
   |                |             |        |        | included in    |
   |                |             |        |        | the Message.   |
   +----------------+-------------+--------+--------+----------------+
   | Status         | (0000,0900) | US     | 1      | The value of   |
   |                |             |        |        | this field     |
   |                |             |        |        | depends upon   |
   |                |             |        |        | the status     |
   |                |             |        |        | type. `Status  |
   |                |             |        |        | Type Encoding  |
   |                |             |        |        | (Normative) <  |
   |                |             |        |        | #chapter_C>`__ |
   |                |             |        |        | defines the    |
   |                |             |        |        | encoding of    |
   |                |             |        |        | the status     |
   |                |             |        |        | types defined  |
   |                |             |        |        | in the service |
   |                |             |        |        | definition.    |
   +----------------+-------------+--------+--------+----------------+
   | Number of      | (0000,1020) | US     | 1      | The number of  |
   | Remaining      |             |        |        | remaining      |
   | Sub-operations |             |        |        | C-STORE        |
   |                |             |        |        | sub-operations |
   |                |             |        |        | to be invoked  |
   |                |             |        |        | for this C-GET |
   |                |             |        |        | operation.     |
   +----------------+-------------+--------+--------+----------------+
   | Number of      | (0000,1021) | US     | 1      | The number of  |
   | Completed      |             |        |        | C-STORE        |
   | Sub-operations |             |        |        | sub-operations |
   |                |             |        |        | invoked by     |
   |                |             |        |        | this C-GET     |
   |                |             |        |        | operation that |
   |                |             |        |        | have completed |
   |                |             |        |        | successfully.  |
   +----------------+-------------+--------+--------+----------------+
   | Number of      | (0000,1022) | US     | 1      | The number of  |
   | Failed         |             |        |        | C-STORE        |
   | Sub-operations |             |        |        | sub-operations |
   |                |             |        |        | invoked by     |
   |                |             |        |        | this C-GET     |
   |                |             |        |        | operation that |
   |                |             |        |        | have failed.   |
   +----------------+-------------+--------+--------+----------------+
   | Number of      | (0000,1023) | US     | 1      | The number of  |
   | Warning        |             |        |        | C-STORE        |
   | Sub-operations |             |        |        | sub-operations |
   |                |             |        |        | invoked by     |
   |                |             |        |        | this C-GET     |
   |                |             |        |        | operation that |
   |                |             |        |        | generated      |
   |                |             |        |        | warning        |
   |                |             |        |        | responses.     |
   +----------------+-------------+--------+--------+----------------+
   | Identifier     | (no tag)    | -      | -      | A Data Set     |
   |                |             |        |        | that encodes   |
   |                |             |        |        | the Identifier |
   |                |             |        |        | that was       |
   |                |             |        |        | matched. See   |
   |                |             |        |        | `Iden          |
   |                |             |        |        | tifier <#sect_ |
   |                |             |        |        | 9.1.3.1.5>`__. |
   +----------------+-------------+--------+--------+----------------+

.. note::

   The list of Attributes allowed and the rules that define the usage of
   the Identifier are specified in .

.. _sect_9.3.3.3:

C-CANCEL-GET-RQ
^^^^^^^^^^^^^^^

The C-CANCEL-GET-RQ Message contains fields as defined in
`table_title <#table_9.3-8>`__. Each field shall conform to DICOM
encoding and Value Representation as defined in . Fields are required as
specified in the C-GET service definition unless otherwise noted in
`table_title <#table_9.3-8>`__. Fields not specified in the C-GET
service definition but present in `table_title <#table_9.3-8>`__ are
required by the DIMSE-C protocol.

.. table:: C-CANCEL-GET-RQ Message Fields

   +----------------+-------------+--------+--------+----------------+
   | **Message      | **Tag**     | **VR** | **VM** | **Description  |
   | Field**        |             |        |        | of Field**     |
   +================+=============+========+========+================+
   | Command Group  | (0000,0000) | UL     | 1      | The even       |
   | Length         |             |        |        | number of      |
   |                |             |        |        | bytes from the |
   |                |             |        |        | end of the     |
   |                |             |        |        | value field to |
   |                |             |        |        | the beginning  |
   |                |             |        |        | of the next    |
   |                |             |        |        | group.         |
   +----------------+-------------+--------+--------+----------------+
   | Command Field  | (0000,0100) | US     | 1      | This field     |
   |                |             |        |        | distinguishes  |
   |                |             |        |        | the DIMSE-C    |
   |                |             |        |        | operation      |
   |                |             |        |        | conveyed by    |
   |                |             |        |        | this Message.  |
   |                |             |        |        | The value of   |
   |                |             |        |        | this field     |
   |                |             |        |        | shall be set   |
   |                |             |        |        | to 0FFFH for   |
   |                |             |        |        | the            |
   |                |             |        |        | C              |
   |                |             |        |        | -CANCEL-GET-RQ |
   |                |             |        |        | Message.       |
   +----------------+-------------+--------+--------+----------------+
   | Message ID     | (0000,0120) | US     | 1      | Shall be set   |
   | Being          |             |        |        | to the value   |
   | Responded To   |             |        |        | of the Message |
   |                |             |        |        | ID (0000,0110) |
   |                |             |        |        | field used in  |
   |                |             |        |        | associated     |
   |                |             |        |        | C-GET-RQ       |
   |                |             |        |        | Message.       |
   +----------------+-------------+--------+--------+----------------+
   | Command Data   | (0000,0800) | US     | 1      | This field     |
   | Set Type       |             |        |        | indicates that |
   |                |             |        |        | no Data Set is |
   |                |             |        |        | present in the |
   |                |             |        |        | Message and    |
   |                |             |        |        | shall be set   |
   |                |             |        |        | to a value of  |
   |                |             |        |        | 0101H.         |
   +----------------+-------------+--------+--------+----------------+

.. _sect_9.3.3.4:

C-GET Protocol Procedures
^^^^^^^^^^^^^^^^^^^^^^^^^

The C-GET procedures are initiated by the invoking DIMSE Service User
issuing a C-GET request primitive. On receipt of the C-GET request
primitive the DIMSE-C protocol machine shall:

-  construct a Message conveying the C-GET-RQ

-  send the Message using the P-DATA request service (see 8.1).

On receipt of a Message conveying a C-GET-RQ the DIMSE-C protocol
machine shall issue a C-GET indication primitive to the performing DIMSE
Service User.

The DIMSE-C protocol machine shall:

-  accept zero or more C-GET response primitives containing the status
   of Pending, issued by the performing DIMSE Service User, followed by
   a single C-GET response primitive containing the final status

-  for each C-GET response primitive containing the Pending status the
   DIMSE-C protocol machine shall:

   a. construct a Message conveying the (Pending) C-GET-RSP

   b. send the Message using the P-DATA request service (see 8.1)

-  for the C-GET response primitive containing the final status the
   DIMSE-C protocol machine shall:

   a. construct a Message conveying the (final) C-GET-RSP

   b. send the Message using the P-DATA request service (see 8.1)

.. note::

   The C-GET indication primitive initiates a sub-operation identical to
   the C-STORE operation. However, for the C-STORE sub-operation the
   DIMSE Service Users switch their invoking and performing roles (i.e.,
   the invoking DIMSE Service User becomes the performing DIMSE Service
   User, etc.).

On receipt of a Message conveying a C-GET-RSP the DIMSE-C protocol
machine shall:

-  if the Message indicates the status of Pending, issue a C-GET
   confirmation primitive to the invoking DIMSE Service User with a
   Pending status

-  if the Message indicates a final status, issue a C-GET confirmation
   primitive to the invoking DIMSE Service User with a final status,
   thus completing the C-GET procedure

.. note::

   The C-GET procedures can be canceled at any time by the invoking
   DIMSE Service User. This is accomplished by the invoking DIMSE
   Service User issuing a C-CANCEL request primitive.

The performing DIMSE Service User may return a C-GET-RSP with the status
of Failed or Refused before the complete C-GET-RQ request Message has
been completely transmitted by the invoking DIMSE Service User (this is
called an early failed response). Upon receipt of this Failed or Refused
C-GET-RSP the invoking DIMSE Service User may terminate the Message
before it is completely sent (i.e., set the Last Fragment bit to 1 in a
Data PDV for this Message, see `Usage of the P-DATA Service By the DICOM
Application Entity (Normative) <#chapter_F>`__). Following this, it may
invoke another operation or notification. It is a protocol violation for
an invoking DIMSE Service User to set the Last Fragment bit to 1 before
a C-GET-RQ Message has been completely transmitted if it has not
received a Failed or Refused C-GET-RSP to that request.

.. note::

   When an Association is operating in asynchronous mode, it is possible
   for an invoking DIMSE Service User to transmit several Messages
   before a response. Therefore, while sending a Message it may receive
   a response to a previously transmitted Message. In this case this
   response is not an early failed response because the related Message
   has already been sent.

.. _sect_9.3.4:

C-MOVE Protocol
~~~~~~~~~~~~~~~

The information necessary for the C-MOVE request and indication DIMSE-C
primitives are conveyed in the C-MOVE-RQ Message. The information
necessary for the C-MOVE response and confirmation DIMSE-C primitives
are conveyed in the C-MOVE-RSP Message. The information necessary for
the C-MOVE Cancel request and Cancel indication primitives are conveyed
in the C-CANCEL-MOVE-RQ Message.

.. _sect_9.3.4.1:

C-MOVE-RQ
^^^^^^^^^

The C-MOVE-RQ Message contains fields as defined in
`table_title <#table_9.3-9>`__. Each field shall conform to DICOM
encoding and Value Representation as defined in . Fields are required as
specified in the C-MOVE service definition unless otherwise noted in
`table_title <#table_9.3-9>`__. Fields not specified in the C-GET-MOVE
service definition but present in `table_title <#table_9.3-9>`__ are
required by the DIMSE-C protocol.

.. table:: C-MOVE-RQ Message Fields

   +----------------+-------------+--------+--------+----------------+
   | **Message      | **Tag**     | **VR** | **VM** | **Description  |
   | Field**        |             |        |        | of Field**     |
   +================+=============+========+========+================+
   | Command Group  | (0000,0000) | UL     | 1      | The even       |
   | Length         |             |        |        | number of      |
   |                |             |        |        | bytes from the |
   |                |             |        |        | end of the     |
   |                |             |        |        | value field to |
   |                |             |        |        | the beginning  |
   |                |             |        |        | of the next    |
   |                |             |        |        | group.         |
   +----------------+-------------+--------+--------+----------------+
   | Affected SOP   | (0000,0002) | UI     | 1      | SOP Class UID  |
   | Class UID      |             |        |        | associated     |
   |                |             |        |        | with this      |
   |                |             |        |        | operation.     |
   +----------------+-------------+--------+--------+----------------+
   | Command Field  | (0000,0100) | US     | 1      | This field     |
   |                |             |        |        | distinguishes  |
   |                |             |        |        | the DIMSE-C    |
   |                |             |        |        | operation      |
   |                |             |        |        | conveyed by    |
   |                |             |        |        | this Message.  |
   |                |             |        |        | The value of   |
   |                |             |        |        | this field     |
   |                |             |        |        | shall be set   |
   |                |             |        |        | to 0021H for   |
   |                |             |        |        | the C-MOVE-RQ  |
   |                |             |        |        | Message.       |
   +----------------+-------------+--------+--------+----------------+
   | Message ID     | (0000,0110) | US     | 1      | Implement      |
   |                |             |        |        | ation-specific |
   |                |             |        |        | value that     |
   |                |             |        |        | distinguishes  |
   |                |             |        |        | this Message   |
   |                |             |        |        | from other     |
   |                |             |        |        | Messages.      |
   +----------------+-------------+--------+--------+----------------+
   | Priority       | (0000,0700) | US     | 1      | The priority   |
   |                |             |        |        | shall be set   |
   |                |             |        |        | to one of the  |
   |                |             |        |        | following      |
   |                |             |        |        | values:        |
   |                |             |        |        |                |
   |                |             |        |        | LOW = 0002H    |
   |                |             |        |        |                |
   |                |             |        |        | MEDIUM = 0000H |
   |                |             |        |        |                |
   |                |             |        |        | HIGH = 0001H   |
   +----------------+-------------+--------+--------+----------------+
   | Command Data   | (0000,0800) | US     | 1      | This field     |
   | Set Type       |             |        |        | indicates that |
   |                |             |        |        | a Data Set is  |
   |                |             |        |        | present in the |
   |                |             |        |        | Message. It    |
   |                |             |        |        | shall be set   |
   |                |             |        |        | to any value   |
   |                |             |        |        | other than     |
   |                |             |        |        | 0101H (Null).  |
   +----------------+-------------+--------+--------+----------------+
   | Move           | (0000,0600) | AE     | 1      | Shall be set   |
   | Destination    |             |        |        | to the DICOM   |
   |                |             |        |        | AE Title of    |
   |                |             |        |        | the            |
   |                |             |        |        | destination    |
   |                |             |        |        | DICOM AE to    |
   |                |             |        |        | which the      |
   |                |             |        |        | C-STORE        |
   |                |             |        |        | sub-operations |
   |                |             |        |        | are being      |
   |                |             |        |        | performed.     |
   +----------------+-------------+--------+--------+----------------+
   | Identifier     | (no tag)    | -      | -      | A Data Set     |
   |                |             |        |        | that encodes   |
   |                |             |        |        | the Identifier |
   |                |             |        |        | to be matched. |
   |                |             |        |        | See            |
   |                |             |        |        | `Iden          |
   |                |             |        |        | tifier <#sect_ |
   |                |             |        |        | 9.1.4.1.6>`__. |
   +----------------+-------------+--------+--------+----------------+

.. note::

   Implementations that require compatibility to previous versions of
   this Standard must set the Command Data Set Type (0000,0800) Field to
   0102H (Identifier).

.. _sect_9.3.4.2:

C-MOVE-RSP
^^^^^^^^^^

The C-MOVE-RSP Message contains fields as defined in
`table_title <#table_9.3-10>`__ and in `Status Type Encoding
(Normative) <#chapter_C>`__. Each field shall conform to DICOM encoding
and Value Representation as defined in . Fields are required as
specified in the C-MOVE service definition unless otherwise noted in
`table_title <#table_9.3-10>`__. Fields not specified in the C-MOVE
service definition but present in `table_title <#table_9.3-10>`__ are
required by the DIMSE-C protocol.

.. table:: C-MOVE-RSP Message Fields

   +----------------+-------------+--------+--------+----------------+
   | **Message      | **Tag**     | **VR** | **VM** | **Description  |
   | Field**        |             |        |        | of Field**     |
   +================+=============+========+========+================+
   | Command Group  | (0000,0000) | UL     | 1      | The even       |
   | Length         |             |        |        | number of      |
   |                |             |        |        | bytes from the |
   |                |             |        |        | end of the     |
   |                |             |        |        | value field to |
   |                |             |        |        | the beginning  |
   |                |             |        |        | of the next    |
   |                |             |        |        | group.         |
   +----------------+-------------+--------+--------+----------------+
   | Affected SOP   | (0000,0002) | UI     | 1      | SOP Class UID  |
   | Class UID      |             |        |        | associated     |
   |                |             |        |        | with the       |
   |                |             |        |        | operation.     |
   +----------------+-------------+--------+--------+----------------+
   | Command Field  | (0000,0100) | US     | 1      | This field     |
   |                |             |        |        | distinguishes  |
   |                |             |        |        | the DIMSE-C    |
   |                |             |        |        | operation      |
   |                |             |        |        | conveyed by    |
   |                |             |        |        | this Message.  |
   |                |             |        |        | The value of   |
   |                |             |        |        | this field     |
   |                |             |        |        | shall be set   |
   |                |             |        |        | to 8021H for   |
   |                |             |        |        | the C-MOVE-RSP |
   |                |             |        |        | Message.       |
   +----------------+-------------+--------+--------+----------------+
   | Message ID     | (0000,0120) | US     | 1      | Shall be set   |
   | Being          |             |        |        | to the value   |
   | Responded To   |             |        |        | of the Message |
   |                |             |        |        | ID (0000,0110) |
   |                |             |        |        | field used in  |
   |                |             |        |        | associated     |
   |                |             |        |        | C-MOVE         |
   |                |             |        |        | Message.       |
   +----------------+-------------+--------+--------+----------------+
   | Command Data   | (0000,0800) | US     | 1      | This field     |
   | Set Type       |             |        |        | indicates if a |
   |                |             |        |        | Data Set is    |
   |                |             |        |        | present in the |
   |                |             |        |        | Message. This  |
   |                |             |        |        | field shall be |
   |                |             |        |        | set to the     |
   |                |             |        |        | value of 0101H |
   |                |             |        |        | (Null) if no   |
   |                |             |        |        | Data Set is    |
   |                |             |        |        | present; any   |
   |                |             |        |        | other value    |
   |                |             |        |        | indicates a    |
   |                |             |        |        | Data Set is    |
   |                |             |        |        | included in    |
   |                |             |        |        | the Message.   |
   +----------------+-------------+--------+--------+----------------+
   | Status         | (0000,0900) | US     | 1      | The value of   |
   |                |             |        |        | this field     |
   |                |             |        |        | depends upon   |
   |                |             |        |        | the status     |
   |                |             |        |        | type. `Status  |
   |                |             |        |        | Type Encoding  |
   |                |             |        |        | (Normative) <  |
   |                |             |        |        | #chapter_C>`__ |
   |                |             |        |        | defines the    |
   |                |             |        |        | encoding of    |
   |                |             |        |        | the status     |
   |                |             |        |        | types defined  |
   |                |             |        |        | in the service |
   |                |             |        |        | definition.    |
   +----------------+-------------+--------+--------+----------------+
   | Number of      | (0000,1020) | US     | 1      | The number of  |
   | Remaining      |             |        |        | remaining      |
   | Sub-operations |             |        |        | sub-operations |
   |                |             |        |        | to be invoked  |
   |                |             |        |        | for this       |
   |                |             |        |        | C-MOVE         |
   |                |             |        |        | operation.     |
   +----------------+-------------+--------+--------+----------------+
   | Number of      | (0000,1021) | US     | 1      | The number of  |
   | Completed      |             |        |        | C-STORE        |
   | Sub-operations |             |        |        | sub-operations |
   |                |             |        |        | invoked by     |
   |                |             |        |        | this C-MOVE    |
   |                |             |        |        | operation that |
   |                |             |        |        | have completed |
   |                |             |        |        | successfully.  |
   +----------------+-------------+--------+--------+----------------+
   | Number of      | (0000,1022) | US     | 1      | The number of  |
   | Failed         |             |        |        | C-STORE        |
   | Sub-operations |             |        |        | sub-operations |
   |                |             |        |        | invoked by     |
   |                |             |        |        | this C-MOVE    |
   |                |             |        |        | operation that |
   |                |             |        |        | have failed.   |
   +----------------+-------------+--------+--------+----------------+
   | Number of      | (0000,1023) | US     | 1      | The number of  |
   | Warning        |             |        |        | C-STORE        |
   | Sub-operations |             |        |        | sub-operations |
   |                |             |        |        | invoked by     |
   |                |             |        |        | this C-MOVE    |
   |                |             |        |        | operation that |
   |                |             |        |        | generated      |
   |                |             |        |        | warning        |
   |                |             |        |        | responses.     |
   +----------------+-------------+--------+--------+----------------+
   | Identifier     | (no tag)    | -      | -      | A Data Set     |
   |                |             |        |        | that encodes   |
   |                |             |        |        | attributes     |
   |                |             |        |        | providing      |
   |                |             |        |        | status         |
   |                |             |        |        | information    |
   |                |             |        |        | about the      |
   |                |             |        |        | C-MOVE         |
   |                |             |        |        | operation. See |
   |                |             |        |        | `Iden          |
   |                |             |        |        | tifier <#sect_ |
   |                |             |        |        | 9.1.4.1.6>`__. |
   +----------------+-------------+--------+--------+----------------+

.. _sect_9.3.4.3:

C-CANCEL-MOVE-RQ
^^^^^^^^^^^^^^^^

The C-CANCEL-MOVE-RQ Message contains fields as defined in
`table_title <#table_9.3-11>`__. Each field shall conform to DICOM
encoding and Value Representation as defined in . Fields are required as
specified in the C-MOVE service definition unless otherwise noted in
`table_title <#table_9.3-11>`__. Fields not specified in the C-MOVE
service definition but present in `table_title <#table_9.3-11>`__ are
required by the DIMSE-C protocol.

.. table:: C-CANCEL-MOVE-RQ Message Fields

   +----------------+-------------+--------+--------+----------------+
   | **Message      | **Tag**     | **VR** | **VM** | **Description  |
   | Field**        |             |        |        | of Field**     |
   +================+=============+========+========+================+
   | Command Group  | (0000,0000) | UL     | 1      | The even       |
   | Length         |             |        |        | number of      |
   |                |             |        |        | bytes from the |
   |                |             |        |        | end of the     |
   |                |             |        |        | value field to |
   |                |             |        |        | the beginning  |
   |                |             |        |        | of the next    |
   |                |             |        |        | group.         |
   +----------------+-------------+--------+--------+----------------+
   | Command Field  | (0000,0100) | US     | 1      | This field     |
   |                |             |        |        | distinguishes  |
   |                |             |        |        | the DIMSE-C    |
   |                |             |        |        | operation      |
   |                |             |        |        | conveyed by    |
   |                |             |        |        | this Message.  |
   |                |             |        |        | The value of   |
   |                |             |        |        | this field     |
   |                |             |        |        | shall be set   |
   |                |             |        |        | to 0FFFH for   |
   |                |             |        |        | the            |
   |                |             |        |        | C-             |
   |                |             |        |        | CANCEL-MOVE-RQ |
   |                |             |        |        | Message.       |
   +----------------+-------------+--------+--------+----------------+
   | Message ID     | (0000,0120) | US     | 1      | Shall be set   |
   | Being          |             |        |        | to the value   |
   | Responded To   |             |        |        | of the Message |
   |                |             |        |        | ID (0000,0110) |
   |                |             |        |        | field used in  |
   |                |             |        |        | associated     |
   |                |             |        |        | C-MOVE-RQ      |
   |                |             |        |        | Message.       |
   +----------------+-------------+--------+--------+----------------+
   | Command Data   | (0000,0800) | US     | 1      | This field     |
   | Set Type       |             |        |        | indicates that |
   |                |             |        |        | no Data Set is |
   |                |             |        |        | present in the |
   |                |             |        |        | Message and    |
   |                |             |        |        | shall be set   |
   |                |             |        |        | to a value of  |
   |                |             |        |        | 0101H.         |
   +----------------+-------------+--------+--------+----------------+

.. _sect_9.3.4.4:

C-MOVE Protocol Procedures
^^^^^^^^^^^^^^^^^^^^^^^^^^

The C-MOVE procedures are initiated by the invoking DIMSE Service User
issuing a C-MOVE request primitive. On receipt of the C-MOVE request
primitive the DIMSE-C protocol machine shall:

-  construct a Message conveying the C-MOVE-RQ

-  send the Message using the P-DATA request service (see 8.1)

On receipt of a Message conveying a C-MOVE-RQ the DIMSE-C protocol
machine shall issue a C-MOVE indication primitive to the performing
DIMSE Service User.

The DIMSE-C protocol machine shall:

-  accept zero or more C-MOVE response primitives containing the status
   of Pending, issued by the performing DIMSE Service User, followed by
   a single C-MOVE response primitive containing the final status

-  for each C-MOVE response primitive containing the Pending status the
   DIMSE-C protocol machine shall:

   a. construct a Message conveying the (Pending) C-MOVE-RSP

   b. send the Message using the P-DATA request service (see 8.1)

-  for the C-MOVE response primitive containing the final status the
   DIMSE-C protocol machine shall:

   a. construct a Message conveying the (final) C-MOVE-RSP

   b. send the Message using the P-DATA request service (see 8.1)

.. note::

   The C-MOVE indication primitive initiates a sub-operation identical
   to the C-STORE operation.

On receipt of a Message conveying a C-MOVE-RSP the DIMSE-C protocol
machine shall:

-  if the Message indicates the status of Pending, issue a C-MOVE
   confirmation primitive to the invoking DIMSE Service User with a
   Pending status;

-  if the Message indicates a final status, issue a C-MOVE confirmation
   primitive to the invoking DIMSE Service User with a final status,
   thus completing the C-MOVE procedure

.. note::

   The C-MOVE procedures can be canceled at any time by the invoking
   DIMSE Service User. This shall be accomplished by the invoking DIMSE
   Service User issuing a C-CANCEL request primitive.

The performing DIMSE Service User may return a C-MOVE-RSP with the
status of Failed or Refused before the complete C-MOVE-RQ request
Message has been completely transmitted by the invoking DIMSE Service
User (this is called an early failed response). Upon receipt of this
Failed or Refused C-MOVE-RSP the invoking DIMSE Service User may
terminate the Message before it is completely sent (i.e., set the Last
Fragment bit to 1 in a Data PDV for this Message, see `Usage of the
P-DATA Service By the DICOM Application Entity
(Normative) <#chapter_F>`__). Following this, it may invoke another
operation or notification. It is a protocol violation for an invoking
DIMSE Service User to set the Last Fragment bit to 1 before a C-MOVE-RQ
Message has been completely transmitted if it has not received a Failed
or Refused C-MOVE-RSP to that request.

.. note::

   When an Association is operating in asynchronous mode, it is possible
   for an invoking DIMSE Service User to transmit several Messages
   before a response. Therefore, while sending a Message it may receive
   a response to a previously transmitted Message. In this case this
   response is not an early failed response because the related Message
   has already been sent.

.. _sect_9.3.5:

C-ECHO Protocol
~~~~~~~~~~~~~~~

The information necessary for the C-ECHO request and indication DIMSE-C
primitives are conveyed in the C-ECHO-RQ Message. The information
necessary for the C-ECHO response and confirmation DIMSE-C primitives
are conveyed in the C-ECHO-RSP Message.

.. _sect_9.3.5.1:

C-ECHO-RQ
^^^^^^^^^

The C-ECHO-RQ Message contains fields as defined in
`table_title <#table_9.3-12>`__. Each field shall conform to DICOM
encoding and Value Representation as defined in . Fields are required as
specified in the C-ECHO service definition unless otherwise noted in
`table_title <#table_9.3-12>`__. Fields not specified in the C-ECHO
service definition but present in `table_title <#table_9.3-12>`__ are
required by the DIMSE-C protocol.

.. table:: C-ECHO-RQ Message Fields

   +----------------+-------------+--------+--------+----------------+
   | **Message      | **Tag**     | **VR** | **VM** | **Description  |
   | Field**        |             |        |        | of Field**     |
   +================+=============+========+========+================+
   | Command Group  | (0000,0000) | UL     | 1      | The even       |
   | Length         |             |        |        | number of      |
   |                |             |        |        | bytes from the |
   |                |             |        |        | end of the     |
   |                |             |        |        | value field to |
   |                |             |        |        | the beginning  |
   |                |             |        |        | of the next    |
   |                |             |        |        | group.         |
   +----------------+-------------+--------+--------+----------------+
   | Affected SOP   | (0000,0002) | UI     | 1      | SOP Class UID  |
   | Class UID      |             |        |        | associated     |
   |                |             |        |        | with this      |
   |                |             |        |        | operation.     |
   +----------------+-------------+--------+--------+----------------+
   | Command Field  | (0000,0100) | US     | 1      | This field     |
   |                |             |        |        | distinguishes  |
   |                |             |        |        | the DIMSE-C    |
   |                |             |        |        | operation      |
   |                |             |        |        | conveyed by    |
   |                |             |        |        | this Message.  |
   |                |             |        |        | The value of   |
   |                |             |        |        | this field     |
   |                |             |        |        | shall be set   |
   |                |             |        |        | to 0030H for   |
   |                |             |        |        | the C-ECHO-RQ  |
   |                |             |        |        | Message.       |
   +----------------+-------------+--------+--------+----------------+
   | Message ID     | (0000,0110) | US     | 1      | Implement      |
   |                |             |        |        | ation-specific |
   |                |             |        |        | value that     |
   |                |             |        |        | distinguishes  |
   |                |             |        |        | this Message   |
   |                |             |        |        | from other     |
   |                |             |        |        | Messages.      |
   +----------------+-------------+--------+--------+----------------+
   | Command Data   | (0000,0800) | US     | 1      | This field     |
   | Set Type       |             |        |        | indicates that |
   |                |             |        |        | no Data Set is |
   |                |             |        |        | present in the |
   |                |             |        |        | Message and    |
   |                |             |        |        | shall be set   |
   |                |             |        |        | to a value of  |
   |                |             |        |        | 0101H.         |
   +----------------+-------------+--------+--------+----------------+

.. _sect_9.3.5.2:

C-ECHO-RSP
^^^^^^^^^^

The C-ECHO-RSP Message contains fields as defined in
`table_title <#table_9.3-13>`__ and in `Status Type Encoding
(Normative) <#chapter_C>`__. Each field shall conform to DICOM encoding
and Value Representation as defined in . Fields are required as
specified in the C-ECHO service definition unless otherwise noted in
`table_title <#table_9.3-13>`__. Fields not specified in the C-ECHO
service definition but present in `table_title <#table_9.3-13>`__ are
required by the DIMSE-C protocol.

.. table:: C-ECHO-RSP Message Fields

   +----------------+-------------+--------+--------+----------------+
   | **Message      | **Tag**     | **VR** | **VM** | **Description  |
   | Field**        |             |        |        | of Field**     |
   +================+=============+========+========+================+
   | Command Group  | (0000,0000) | UL     | 1      | The even       |
   | Length         |             |        |        | number of      |
   |                |             |        |        | bytes from the |
   |                |             |        |        | end of the     |
   |                |             |        |        | value field to |
   |                |             |        |        | the beginning  |
   |                |             |        |        | of the next    |
   |                |             |        |        | group.         |
   +----------------+-------------+--------+--------+----------------+
   | Affected SOP   | (0000,0002) | UI     | 1      | SOP Class UID  |
   | Class UID      |             |        |        | associated     |
   |                |             |        |        | with the       |
   |                |             |        |        | operation.     |
   +----------------+-------------+--------+--------+----------------+
   | Command Field  | (0000,0100) | US     | 1      | This field     |
   |                |             |        |        | distinguishes  |
   |                |             |        |        | the DIMSE-C    |
   |                |             |        |        | operation      |
   |                |             |        |        | conveyed by    |
   |                |             |        |        | this Message.  |
   |                |             |        |        | The value of   |
   |                |             |        |        | this field     |
   |                |             |        |        | shall be set   |
   |                |             |        |        | to 8030H for   |
   |                |             |        |        | the C-ECHO-RSP |
   |                |             |        |        | Message.       |
   +----------------+-------------+--------+--------+----------------+
   | Message ID     | (0000,0120) | US     | 1      | Shall be set   |
   | Being          |             |        |        | to the value   |
   | Responded To   |             |        |        | of the Message |
   |                |             |        |        | ID (0000,0110) |
   |                |             |        |        | field used in  |
   |                |             |        |        | associated     |
   |                |             |        |        | C-ECHO-RQ      |
   |                |             |        |        | Message.       |
   +----------------+-------------+--------+--------+----------------+
   | Command Data   | (0000,0800) | US     | 1      | This field     |
   | Set Type       |             |        |        | indicates that |
   |                |             |        |        | no Data Set is |
   |                |             |        |        | present in the |
   |                |             |        |        | Message and    |
   |                |             |        |        | shall be set   |
   |                |             |        |        | to a value of  |
   |                |             |        |        | 0101H.         |
   +----------------+-------------+--------+--------+----------------+
   | Status         | (0000,0900) | US     | 1      | Indicates the  |
   |                |             |        |        | status of the  |
   |                |             |        |        | response. It   |
   |                |             |        |        | shall have a   |
   |                |             |        |        | value of       |
   |                |             |        |        | Success.       |
   +----------------+-------------+--------+--------+----------------+

.. _sect_9.3.5.3:

C-ECHO Protocol Procedures
^^^^^^^^^^^^^^^^^^^^^^^^^^

The C-ECHO procedures are initiated by the invoking DIMSE Service User
issuing a C-ECHO request primitive. On receipt of the C-ECHO request
primitive the DIMSE-C protocol machine shall:

-  construct a Message conveying the C-ECHO-RQ

-  send the Message using the P-DATA request service (see 8.1)

On receipt of a Message conveying a C-ECHO-RQ the DIMSE-C protocol
machine shall issue a C-ECHO indication primitive to the performing
DIMSE Service User.

On receipt of a C-ECHO response primitive, issued by the performing
DIMSE Service User, the DIMSE-C protocol machine shall:

-  construct a Message conveying the C-ECHO-RSP

-  send the Message using the P-DATA request service (see 8.1)

On receipt of a Message conveying a C-ECHO-RSP the DIMSE protocol
machine shall issue a C-ECHO confirmation primitive to the invoking
DIMSE Service User, thus completing the C-ECHO procedure.

