.. _chapter_10:

DIMSE-N
=======

.. _sect_10.1:

Services
--------

The following sections describe the DIMSE-N Services. The behavior of
these services is also described in . The Affected SOP Class UID in the
DIMSE-N command need not match the SOP Class UID in the Presentation
Context negotiated for the association over which the DIMSE-N command
has been sent. specifies which combinations are valid.

.. _sect_10.1.1:

N-EVENT-REPORT Service
~~~~~~~~~~~~~~~~~~~~~~

The N-EVENT-REPORT service is used by a DIMSE Service User to report an
event to a peer DIMSE Service User. It is a confirmed service.

.. _sect_10.1.1.1:

N-EVENT-REPORT Parameters
^^^^^^^^^^^^^^^^^^^^^^^^^

`table_title <#table_10.1-1>`__ lists the parameters for this service.

.. table:: N-EVENT-REPORT Parameters

   ============================= =========== ============
   **DIMSE Parameter Name**      **Req/Ind** **Rsp/Conf**
   ============================= =========== ============
   Message ID                    M           -
   Message ID Being Responded To -           M
   Affected SOP Class UID        M           U(=)
   Affected SOP Instance UID     M           U(=)
   Event Type ID                 M           C(=)
   Event Information             U           -
   Event Reply                   -           C
   Status                        -           M
   ============================= =========== ============

.. _sect_10.1.1.1.1:

Message ID
''''''''''

This parameter identifies the operation. It is used to distinguish this
operation from other notifications or operations that the DIMSE Service
Provider may have in progress. No two identical values for the Message
ID (0000,0110) shall be used for outstanding operations or
notifications.

.. note::

   The Message ID (0000,0110) is recommended to be unique within the
   scope of an Association, to support debug procedures.

.. _sect_10.1.1.1.2:

Message ID Being Responded To
'''''''''''''''''''''''''''''

This parameter specifies the Message ID (0000,0110) of the notification
request/indication to which this response/confirmation applies.

.. _sect_10.1.1.1.3:

Affected SOP Class UID
''''''''''''''''''''''

For the request/indication, this parameter specifies the SOP Class of
the SOP Instance for the event. It may be included in the
response/confirmation. If included in the response/confirmation, this
parameter shall be equal to the value in the request/indication.

.. _sect_10.1.1.1.4:

Affected SOP Instance UID
'''''''''''''''''''''''''

For the request/indication, this parameter specifies the SOP Instance
for the event. It may be included in the response/confirmation. If
included in the response/confirmation, this parameter shall be equal
**to the**\ value in the request/indication.

.. _sect_10.1.1.1.5:

Event Type ID
'''''''''''''

This parameter specifies the type of event being reported. It may be
included in the success response/confirmation and shall be included if
the Event Reply parameter is included.

.. note::

   Service Class Specifications contained in defines any application
   usage of the Event Type ID parameter.

.. _sect_10.1.1.1.6:

Event Information
'''''''''''''''''

This application-specific parameter contains information that the
invoking DIMSE Service User is able to supply about the event.

.. note::

   Service Class Specifications contained in defines any application
   usage of the Event Information parameter.

.. _sect_10.1.1.1.7:

Event Reply
'''''''''''

This application-specific parameter contains the optional reply to the
event report. It may only be included in the success
response/confirmation.

.. note::

   Service Class Specifications contained in defines any application
   usage of the Event Reply parameter.

.. _sect_10.1.1.1.8:

Status
''''''

This parameter contains the error or success notification for the
operation. It shall be included by the performing DIMSE Service User in
any response/confirmation. The following types of status may occur (see
also `Status Type Encoding (Normative) <#chapter_C>`__):

-  Class-Instance conflict (0119H) - the specified SOP Instance is not a
   member of the specified SOP class.

-  Duplicate invocation (0210H) - the Message ID (0000,0110) specified
   is allocated to another notification or operation.

-  Invalid argument value (0115H) - the event information value
   specified was out of range or otherwise inappropriate.

-  Invalid SOP Instance (0117H) - the SOP Instance UID specified implied
   a violation of the UID construction rules.

-  Mistyped argument (0212H) - one of the parameters supplied has not
   been agreed for use on the Association between the DIMSE Service
   Users.

-  No such argument (0114H) - the event information specified was not
   recognized.

-  No such Event Type (0113H) - the event type specified was not
   recognized.

-  No such SOP Class (0118H) - the SOP Class was not recognized.

-  No such SOP Instance (0112H) - the SOP Instance was not recognized.

-  Processing Failure (0110H) - a general failure in processing the
   operation was encountered.

-  Resource Limitation (0213H) - the operation was not performed due to
   resource limitation.

-  Success (0000H) - successful notification.

-  Unrecognized operation (0211H) - the operation is not one of those
   agreed between the DIMSE Service Users.

.. _sect_10.1.1.2:

N-EVENT-REPORT Service Procedures
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

The following N-EVENT-REPORT procedures apply:

a. The invoking DIMSE Service User reports an event to the performing
   DIMSE Service User by issuing an N-EVENT-REPORT request primitive to
   the DIMSE Service Provider.

b. The DIMSE Service Provider issues an N-EVENT-REPORT indication
   primitive to the performing DIMSE Service User.

c. The performing DIMSE Service User reports acceptance or rejection of
   the N-EVENT-REPORT request primitive by issuing an N-EVENT-REPORT
   response primitive to the DIMSE Service Provider.

d. The DIMSE Service Provider issues an N-EVENT-REPORT confirmation
   primitive to the invoking DIMSE Service User, completing the
   N-EVENT-REPORT notification.

The performing DIMSE Service User may return an N-EVENT-REPORT response
primitive with the status of Failed or Refused before the entire
N-EVENT-REPORT indication (Data Set) has been completely transmitted by
the invoking DIMSE Service User. A N-EVENT-REPORT response primitive
with the status of Success or Warning shall not be returned until the
entire N-EVENT-REPORT indication has been received by the performing
DIMSE Service User.

.. note::

   Such an occurrence of a "Failed" response is often called an early
   failed response.

.. _sect_10.1.2:

N-GET Service
~~~~~~~~~~~~~

The N-GET service is used by a DIMSE Service User to retrieve Attribute
Values from a peer DIMSE Service User. It is a confirmed service.

.. _sect_10.1.2.1:

N-GET Parameters
^^^^^^^^^^^^^^^^

`table_title <#table_10.1-2>`__ lists the parameters for this service.

.. table:: N-GET Parameters

   ============================= =========== ============
   **DIMSE Parameter Name**      **Req/Ind** **Rsp/Conf**
   ============================= =========== ============
   Message ID                    M           -
   Message ID Being Responded To -           M
   Requested SOP Class UID       M           -
   Requested SOP Instance UID    M           -
   Attribute Identifier List     U           -
   Affected SOP Class UID        -           U
   Affected SOP Instance UID     -           U
   Attribute List                -           C
   Status                        -           M
   ============================= =========== ============

.. _sect_10.1.2.1.1:

Message ID
''''''''''

This parameter identifies the operation. It is used to distinguish this
operation from other notifications or operations that the DIMSE Service
Provider may have in progress. No two identical values for the Message
ID (0000,0110) shall be used for outstanding operations or
notifications.

.. note::

   The Message ID (0000,0110) is recommended to be unique within the
   scope of an Association, to support debug procedures.

.. _sect_10.1.2.1.2:

Message ID Being Responded To
'''''''''''''''''''''''''''''

This parameter specifies the Message ID (0000,0110) of the operation
request/indication to which this response/confirmation applies.

.. _sect_10.1.2.1.3:

Requested SOP Class UID
'''''''''''''''''''''''

This parameter specifies the SOP Class for which Attribute Values are to
be retrieved.

.. _sect_10.1.2.1.4:

Requested SOP Instance UID
''''''''''''''''''''''''''

This parameter specifies the SOP Instance for which Attribute Values are
to be retrieved.

.. _sect_10.1.2.1.5:

Attribute Identifier List
'''''''''''''''''''''''''

This parameter contains a set of Attribute identifiers for which the
Attribute Values are to be returned by the performing DIMSE Service
User. If this parameter is omitted, all Attribute identifiers are
assumed. The definitions of the Attributes are found in the
specification of the Information Object Definition in .

.. _sect_10.1.2.1.6:

Affected SOP Class UID
''''''''''''''''''''''

This parameter may be included in the response/confirmation. If included
in the response/confirmation, this parameter shall be equal to the
Requested SOP Class UID parameter value used in the request/indication.

.. _sect_10.1.2.1.7:

Affected SOP Instance UID
'''''''''''''''''''''''''

This parameter specifies the SOP Instance for which Attribute Values are
returned. It may be included in any response/confirmation and when
included shall be equal to the Requested SOP Instance UID (0000,1001)
parameter value used in the invocation.

.. _sect_10.1.2.1.8:

Attribute List
''''''''''''''

This parameter contains the set of Attribute identifiers and values that
are returned by the performing DIMSE Service User. It shall be included
in the success response/confirmation.

.. _sect_10.1.2.1.9:

Status
''''''

This parameter contains the error or success notification for the
operation. It shall be included by the performing DIMSE Service User in
any response/confirmation. The following types of status may occur (see
also `Status Type Encoding (Normative) <#chapter_C>`__):

-  Attribute list error (0107H) - one or more Attribute Values were not
   read because the specified Attribute was not recognized. The
   Attribute Values that could be read are returned.

-  Class-Instance conflict (0119H) - the specified SOP Instance is not a
   member of the specified SOP Class.

-  Duplicate invocation (0210H) - the Message ID (0000,0110) specified
   is allocated to another notification or operation.

-  Invalid SOP Instance (0117H) - the SOP Instance UID specified implied
   a violation of the UID construction rules.

-  Mistyped argument (0212H) - one of the parameters supplied has not
   been agreed for use on the Association between the DIMSE Service
   Users.

-  No such SOP Class (0118H) - the SOP Class was not recognized.

-  No such SOP Instance (0112H) - the SOP Instance was not recognized.

-  Processing Failure (0110H) - a general failure in processing the
   operation was encountered.

-  Resource Limitation (0213H) - the operation was not performed due to
   resource limitation.

-  Success (0000H) - successful operation.

-  Unrecognized operation (0211H) - the operation is not one of those
   agreed between the DIMSE Service Users.

-  Refused: Not authorized (0124H) - the DIMSE Service User was not
   authorized to invoke the operation

-  Warning (Status value is Service Class specific): not all optional
   attributes were returned by DIMSE Service User

-  Failed (Status value is Service Class specific): DIMSE Service User
   failed to complete the operation

.. _sect_10.1.2.2:

N-GET Service Procedures
^^^^^^^^^^^^^^^^^^^^^^^^

The following N-GET procedures apply;

a. The invoking DIMSE Service User requests the performing DIMSE Service
   User to retrieve Attribute Value(s) by issuing an N-GET request
   primitive to the DIMSE Service Provider.

b. The DIMSE Service Provider issues an N-GET indication primitive to
   the performing DIMSE Service User.

c. If the operation can be performed, then the performing DIMSE Service
   User retrieves the requested Attribute Value(s) and generates a
   response indicating acceptance of the N-GET request primitive by
   issuing an N-GET response primitive to the DIMSE Service Provider. In
   this case the following procedure does not apply.

d. If the operation cannot be performed, then the performing DIMSE
   Service User rejects the N-GET request by issuing an N-GET response
   primitive with the appropriate error code to the DIMSE Service
   Provider.

e. The DIMSE Service Provider issues an N-GET confirmation primitive to
   the invoking DIMSE Service User, completing the N-GET operation.

.. _sect_10.1.3:

N-SET Service
~~~~~~~~~~~~~

The N-SET service is used by a DIMSE Service User to request the
modification of Attribute Values from a peer DIMSE Service User. It is a
confirmed service.

.. _sect_10.1.3.1:

N-SET Parameters
^^^^^^^^^^^^^^^^

`table_title <#table_10.1-3>`__ lists the parameters for this service.

.. table:: N-SET Parameters

   ============================= =========== ============
   **DIMSE Parameter Name**      **Req/Ind** **Rsp/Conf**
   ============================= =========== ============
   Message ID                    M           -
   Message ID Being Responded To -           M
   Requested SOP Class UID       M           -
   Requested SOP Instance UID    M           -
   Modification List             M           -
   Attribute List                -           U
   Affected SOP Class UID        -           U
   Affected SOP Instance UID     -           U
   Status                        -           M
   ============================= =========== ============

.. _sect_10.1.3.1.1:

Message ID
''''''''''

This parameter identifies the operation. It is used to distinguish this
operation from other notifications or operations that the DIMSE Service
Provider may have in progress. No two identical values for the Message
ID (0000,0110) shall be used for outstanding operations or
notifications.

.. note::

   The Message ID (0000,0110) is recommended to be unique within the
   scope of an Association, to support debug procedures.

.. _sect_10.1.3.1.2:

Message ID Being Responded To
'''''''''''''''''''''''''''''

This parameter specifies the Message ID (0000,0110) of the operation
request/indication to which this response/confirmation applies.

.. _sect_10.1.3.1.3:

Requested SOP Class UID
'''''''''''''''''''''''

This parameter specifies the SOP Class for which Attribute Values are to
be modified.

.. _sect_10.1.3.1.4:

Requested SOP Instance UID
''''''''''''''''''''''''''

This parameter specifies the SOP Instance for which Attribute Values are
to be modified.

.. _sect_10.1.3.1.5:

Modification List
'''''''''''''''''

This parameter contains the set of Attribute identifiers and values that
are to be used by the performing DIMSE Service User to replace the
current values of the Attributes specified.

.. _sect_10.1.3.1.6:

Attribute List
''''''''''''''

This parameter contains the set of Attribute identifiers and values that
were used by the performing DIMSE Service User to replace the values of
the Attributes specified. It may be included in the success
response/confirmation.

.. _sect_10.1.3.1.7:

Affected SOP Class UID
''''''''''''''''''''''

This parameter may be included in the response/confirmation. If included
in the response/confirmation, this parameter shall be equal to the
Requested SOP Class UID parameter value used in the request/indication.

.. _sect_10.1.3.1.8:

Affected SOP Instance UID
'''''''''''''''''''''''''

This parameter specifies the SOP Instance for which Attribute Values
were modified. It may be included in any response/confirmation and when
included shall be equal to the Requested SOP Instance UID (0000,1001)
parameter value used in the invocation.

.. _sect_10.1.3.1.9:

Status
''''''

This parameter contains the error or success notification for the
operation. It shall be included by the performing DIMSE Service User in
any response/confirmation. The following types of status may occur (see
also `Status Type Encoding (Normative) <#chapter_C>`__):

-  Class-Instance conflict (0119H) - the specified SOP Instance is not a
   member of the specified SOP Class.

-  Duplicate invocation (0210H) - the Message ID (0000,0110) specified
   is allocated to another notification or operation.

-  Invalid Attribute Value (0106H) - the Attribute Value specified was
   out of range or otherwise inappropriate.

-  Attribute Value out of range (0116H) - the Attribute Value specified
   was out of range or otherwise inappropriate. The Attribute Values
   that could be modified were modified.

-  Mistyped argument (0212H) - one of the parameters supplied has not
   been agreed for use on the Association between the DIMSE Service
   Users.

-  Invalid SOP Instance (0117H) - the SOP Instance UID specified implied
   a violation of the UID construction rules.

-  Missing Attribute Value (0121H) - a required Attribute Value was not
   supplied.

-  No such Attribute (0105H) - the Tag for the specified Attribute was
   not recognized.

-  Attribute list error (0107H) - one or more Attribute Values were not
   modified because the specified Attributes were not recognized. The
   Attribute Values that could be modified were modified.

-  No such SOP Class (0118H) - the SOP Class was not recognized.

-  No such SOP Instance (0112H) - the SOP Instance was not recognized.

-  Processing Failure (0110H) - a general failure in processing the
   operation was encountered.

-  Resource Limitation (0213H) - the operation was not performed due to
   resource limitation.

-  Success (0000H) - successful operation.

-  Unrecognized operation (0211H) - the operation is not one of those
   agreed between the DIMSE Service Users.

-  Refused: Not authorized (0124H) - the DIMSE Service User was not
   authorized to invoke the operation.

-  Failed (Status value is Service Class specific): the operation was
   not performed as certain conditions for operation were not met

-  Warning (Status value is Service Class specific): the operation was
   performed partially or with modified conditions

.. _sect_10.1.3.2:

N-SET Service Procedures
^^^^^^^^^^^^^^^^^^^^^^^^

The following N-SET procedures apply:

a. The invoking DIMSE Service User requests the performing DIMSE Service
   User to modify Attribute Value(s) by issuing an N-SET request
   primitive to the DIMSE Service Provider.

b. The DIMSE-service provider issues an N-SET indication primitive to
   the performing DIMSE Service User.

c. If the operation can be performed, then the performing DIMSE Service
   User modifies the requested Attribute Value(s) and generates a
   response indicating acceptance of the N-SET request primitive by
   issuing an N-SET response primitive to the DIMSE Service Provider. In
   this case the following procedure does not apply.

d. If the operation cannot be performed, then the performing DIMSE
   Service User rejects the N-SET request by issuing an N-SET response
   primitive with the appropriate error code to the DIMSE Service
   Provider.

e. The DIMSE Service Provider issues an N-SET confirmation primitive to
   the invoking DIMSE Service User, completing the N-SET operation.

The performing DIMSE Service User may return an N-SET response primitive
with the status of Failed or Refused before the entire N-SET indication
(Data Set) has been completely transmitted by the invoking DIMSE Service
User. A N-SET response primitive with the status of Success or Warning
shall not be returned until the entire N-SET indication has been
received by the performing DIMSE Service User.

.. note::

   Such an occurrence of a "Failed" response is often called an early
   failed response.

.. _sect_10.1.4:

N-ACTION Service
~~~~~~~~~~~~~~~~

The N-ACTION service is used by a DIMSE Service User to request an
action by a peer DIMSE Service User. It is a confirmed service.

.. _sect_10.1.4.1:

N-ACTION Parameters
^^^^^^^^^^^^^^^^^^^

`table_title <#table_10.1-4>`__ lists the parameters for this service.

.. table:: N-ACTION Parameters

   ============================= =========== ============
   **DIMSE Parameter Name**      **Req/Ind** **Rsp/Conf**
   ============================= =========== ============
   Message ID                    M           -
   Message ID Being Responded To -           M
   Requested SOP Class UID       M           -
   Requested SOP Instance UID    M           -
   Action Type ID                M           C(=)
   Action Information            U           -
   Affected SOP Class UID        -           U
   Affected SOP Instance UID     -           U
   Action Reply                  -           C
   Status                        -           M
   ============================= =========== ============

.. _sect_10.1.4.1.1:

Message ID
''''''''''

This parameter identifies the operation. It is used to distinguish this
operation from other notifications or operations that the DIMSE Service
Provider may have in progress. No two identical values for the Message
ID (0000,0110) shall be used for outstanding operations or
notifications.

.. note::

   The Message ID (0000,0110) is recommended to be unique within the
   scope of an Association, to support debug procedures.

.. _sect_10.1.4.1.2:

Message ID Being Responded To
'''''''''''''''''''''''''''''

This parameter specifies the Message ID (0000,0110) of the operation
request/indication to which this response/confirmation applies.

.. _sect_10.1.4.1.3:

Requested SOP Class UID
'''''''''''''''''''''''

This parameter specifies the SOP Class for which the action is to be
performed.

.. _sect_10.1.4.1.4:

Requested SOP Instance UID
''''''''''''''''''''''''''

This parameter specifies the SOP Instance on which the action is to be
performed.

.. _sect_10.1.4.1.5:

Action Type ID
''''''''''''''

This parameter specifies a particular action that is to be performed. It
may be included in the success response/confirmation and shall be
included if the action reply parameter is included.

.. note::

   Service Class Specifications contained in defines any application
   usage of the Action Type ID (0000,1008) parameter.

.. _sect_10.1.4.1.6:

Action Information
''''''''''''''''''

This parameter specifies extra application-specific information when
necessary to further define the nature, variations, or operands of the
action to be performed. The syntax and semantics of the parameter depend
upon the action requested. It may only be included in the
request/indication.

.. note::

   Service Class Specifications contained in defines any application
   usage of the Action Information parameter.

.. _sect_10.1.4.1.7:

Affected SOP Class UID
''''''''''''''''''''''

This parameter may be included in the response/confirmation. If included
in the response/confirmation, this parameter shall be equal to the
Requested SOP Class UID parameter value used in the request/indication.

.. _sect_10.1.4.1.8:

Affected SOP Instance UID
'''''''''''''''''''''''''

This parameter specifies the SOP Instance on which the action is to be
performed. It may be included in any response/confirmation and when
included shall be equal to the Requested SOP Instance UID (0000,1001)
parameter value used in the invocation.

.. _sect_10.1.4.1.9:

Action Reply
''''''''''''

This parameter contains the application-specific reply to the action. It
may be included in the success response/confirmation.

.. note::

   Service Class Specifications contained in defines any application
   usage of the Action Reply parameter.

.. _sect_10.1.4.1.10:

Status
''''''

This parameter contains the error or success notification for the
operation. It shall be included by the performing DIMSE Service User in
any response/confirmation. The following type of status may occur (see
also `Status Type Encoding (Normative) <#chapter_C>`__):

-  Class-Instance conflict (0119H) - the specified SOP Instance is not a
   member of the specified SOP Class.

-  Duplicate invocation (0210H) - the Message ID (0000,0110) specified
   is allocated to another notification or operation.

-  Invalid argument value (0115H) - the action information value
   specified was out of range or otherwise inappropriate.

-  Invalid SOP Instance (0117H) - the SOP Instance UID specified implied
   a violation of the UID construction rules.

-  Mistyped argument (0212H) - one of the parameters supplied has not
   been agreed for use on the Association between the DIMSE Service
   Users.

-  No such Action (0123H) - the action type specified was not supported.

-  No such argument (0114H) - the action information specified was not
   supported.

-  No such SOP Class (0118H) - the SOP Class was not recognized.

-  No such SOP Instance (0112H) - the SOP Instance was not recognized.

-  Processing Failure (0110H) - a general failure in processing the
   operation was encountered.

-  Resource Limitation (0213H) - the operation was not performed due to
   resource limitation.

-  Success (0000H) - successful operation.

-  Unrecognized operation (0211H) - the operation is not one of those
   agreed between the DIMSE Service Users.

-  Refused: Not authorized (0124H) - the DIMSE Service User was not
   authorized to invoke the operation.

-  Failed (Status value is Service Class specific): the operation was
   not performed as certain conditions for operation were not met

-  Warning (Status value is Service Class specific): the operation was
   performed partially or with modified conditions

.. _sect_10.1.4.2:

N-ACTION Service Procedures
^^^^^^^^^^^^^^^^^^^^^^^^^^^

The following N-ACTION procedures apply:

a. The invoking DIMSE Service User requests the performing DIMSE Service
   User to perform an action on a managed SOP Instance by issuing an
   N-ACTION request primitive to the DIMSE Service Provider.

b. The DIMSE-service provider issues an N-ACTION indication primitive to
   the performing DIMSE Service User.

c. If the operation can be performed, the performing DIMSE Service User
   applies the action to the specified SOP Instance and generates a
   response indicating acceptance of the N-ACTION request primitive by
   issuing an N-ACTION response primitive to the DIMSE Service Provider.
   In this case the following procedure does not apply. The Action Reply
   may be included in a successful response.

d. If the operation cannot be performed, then the performing DIMSE
   Service User rejects the N-ACTION request by issuing an N-ACTION
   response primitive with the appropriate error code to the DIMSE
   Service Provider.

e. The DIMSE Service Provider issues an N-ACTION confirmation primitive
   to the invoking DIMSE Service User, completing the N-ACTION
   operation.

The performing DIMSE Service User may return an N-ACTION response
primitive with the status of Failed or Refused before the entire
N-ACTION indication (Data Set) has been completely transmitted by the
invoking DIMSE Service User. A N-ACTION response primitive with the
status of Success or Warning shall not be returned until the entire
N-ACTION indication has been received by the performing DIMSE Service
User.

.. note::

   Such an occurrence of a "Failed" response is often called an early
   failed response.

.. _sect_10.1.5:

N-CREATE Service
~~~~~~~~~~~~~~~~

The N-CREATE service is used by a DIMSE Service User to request a peer
DIMSE Service User to create a new managed SOP Instance, complete with
its identification and the values of its associated Attributes, and
simultaneously to register its identification. It is a confirmed
service.

.. _sect_10.1.5.1:

N-CREATE Parameters
^^^^^^^^^^^^^^^^^^^

`table_title <#table_10.1-5>`__ lists the parameters for this service.

.. table:: N-CREATE Parameters

   ============================= =========== ============
   **DIMSE Parameter Name**      **Req/Ind** **Rsp/Conf**
   ============================= =========== ============
   Message ID                    M           -
   Message ID Being Responded To -           M
   Affected SOP Class UID        M           U(=)
   Affected SOP Instance UID     U           C
   Attribute List                U           U
   Status                        -           M
   ============================= =========== ============

.. _sect_10.1.5.1.1:

Message ID
''''''''''

This parameter identifies the operation. It is used to distinguish this
operation from other notifications or operations that the DIMSE Service
Provider may have in progress. No two identical values for the Message
ID (0000,0110) shall be used for outstanding operations or
notifications.

.. note::

   The Message ID (0000,0110) is recommended to be unique within the
   scope of an Association, to support debug procedures.

.. _sect_10.1.5.1.2:

Message ID Being Responded To
'''''''''''''''''''''''''''''

This parameter specifies the Message ID (0000,0110) of the operation
request/indication to which this response/confirmation applies.

.. _sect_10.1.5.1.3:

Affected SOP Class UID
''''''''''''''''''''''

For the request/indication, this parameter specifies the SOP Class of
the new SOP Instance that is to be created by the performing DIMSE
Service User. The performing DIMSE Service User assigns to the new SOP
Instance, a set of Attribute Values as specified by the definition of
its SOP Class. For the response/confirmation, this parameter specifies
the SOP class of the SOP Instance that was created. It may be included
in the response/confirmation. If included in the response/confirmation,
this parameter shall be equal to the value in the request/indication.

.. _sect_10.1.5.1.4:

Affected SOP Instance UID
'''''''''''''''''''''''''

For the request/indication, this parameter specifies the SOP Instance
that is used by the performing DIMSE Service User. If the SOP Instance
UID is not supplied by the invoking DIMSE Service User, then the
performing DIMSE Service User assigns a value to this identification of
instance. For the response/confirmation, this parameter may only be
included in the success response/confirmation and shall be included if
it is not supplied by the invoking DIMSE Service User.

.. _sect_10.1.5.1.5:

Attribute List
''''''''''''''

When this parameter is supplied by the invoking DIMSE Service User, it
contains a set of Attribute identifiers and values that the performing
DIMSE Service User is to assign to the new managed SOP Instance. When
returned by the performing DIMSE Service User in the success
response/confirmation, this parameter contains the complete list of all
Attribute identifiers and values that were assigned to the new managed
SOP Instance.

.. _sect_10.1.5.1.6:

Status
''''''

This parameter contains the error or success notification for the
operation. It shall be included by the performing DIMSE Service User in
any response/confirmation. The following type of status may occur (see
also `Status Type Encoding (Normative) <#chapter_C>`__):

-  Duplicate invocation (0210H) - the Message ID (0000,0110) specified
   is allocated to another notification or operation.

-  Duplicate SOP Instance (0111H) - the new managed SOP Instance Value
   supplied by the invoking DIMSE Service User was already registered
   for a managed SOP Instance of the specified SOP Class.

-  Invalid Attribute Value (0106H) - the Attribute Value specified was
   out of range or otherwise inappropriate.

-  Attribute Value out of range (0116H) - the Attribute Value specified
   was out of range or otherwise inappropriate. The SCP will apply a
   default value or will not include the attribute in the created
   instance.

-  Invalid SOP Instance (0117H) - the SOP Instance UID specified implied
   a violation of the UID construction rules.

-  Missing Attribute (0120H) - a required Attribute was not supplied.

-  Missing Attribute Value (0121H) - a required Attribute Value was not
   supplied and a default value was not available.

-  Mistyped argument (0212H) - one of the parameters supplied has not
   been agreed for use on the Association between the DIMSE Service
   Users.

-  No such Attribute (0105H) - the Tag for the specified Attribute was
   not recognized.

-  Attribute list error (0107H) -one or more specified Attributes were
   not recognized and not included in the created instance.

-  No such SOP Class (0118H) - the SOP Class was not recognized.

-  Processing Failure (0110H) - a general failure in processing the
   operation was encountered.

-  Resource Limitation (0213H) - the operation was not performed due to
   resource limitation.

-  Success (0000H) - successful operation.

-  Unrecognized operation (0211H) - the operation is not one of those
   agreed between the DIMSE Service Users.

-  Refused: Not authorized (0124H) - the DIMSE Service User was not
   authorized to invoke the operation.

-  Failed (Status value is Service Class specific): no instance was
   created by the DIMSE Service User

-  Warning (Status value is Service Class specific): the DIMSE Service
   User created an Instance but did not perform all specified operations

.. _sect_10.1.5.2:

N-CREATE Service Procedures
^^^^^^^^^^^^^^^^^^^^^^^^^^^

The following N-CREATE procedures apply:

a. The invoking DIMSE Service User requests the creation and
   registration of a new managed SOP Instance by issuing an N-CREATE
   request primitive to the DIMSE Service Provider.

b. The DIMSE-service provider issues an N-CREATE indication primitive to
   the performing DIMSE Service User.

c. If the operation can be performed, the performing DIMSE Service User
   creates and registers the new managed SOP Instance and generates a
   response indicating acceptance of the N-CREATE request primitive by
   issuing an N-CREATE response primitive to the DIMSE Service Provider.
   In this case the following procedure does not apply.

d. If the operation cannot be performed, then the performing DIMSE
   Service User rejects the N-CREATE request by issuing an N-CREATE
   response primitive with the appropriate error code to the DIMSE
   Service Provider.

e. The DIMSE Service Provider issues an N-CREATE confirmation primitive
   to the invoking DIMSE Service User, completing the N-CREATE
   operation.

The performing DIMSE Service User may return an N-CREATE response
primitive with the status of Failed or Refused before the entire
N-CREATE indication (Data Set) has been completely transmitted by the
invoking DIMSE Service User. A N-CREATE response primitive with the
status of Success or Warning shall not be returned until the entire
N-CREATE indication has been received by the performing DIMSE Service
User.

.. note::

   Such an occurrence of a "Failed" response is often called an early
   failed response.

.. _sect_10.1.6:

N-DELETE Service
~~~~~~~~~~~~~~~~

The N-DELETE service is used by an invoking DIMSE Service User to
request a peer DIMSE Service User to delete a managed SOP Instance and
to de-register its identification. It is a confirmed service.

.. _sect_10.1.6.1:

N-DELETE Parameters
^^^^^^^^^^^^^^^^^^^

`table_title <#table_10.1-6>`__ lists the parameters for this service.

.. table:: N-DELETE Parameters

   ============================= =========== ============
   **DIMSE Parameter Name**      **Req/Ind** **Rsp/Conf**
   ============================= =========== ============
   Message ID                    M           -
   Message ID Being Responded To -           M
   Requested SOP Class UID       M           -
   Requested SOP Instance UID    M           -
   Affected SOP Class UID        -           U
   Affected SOP Instance UID     -           U
   Status                        -           M
   ============================= =========== ============

.. _sect_10.1.6.1.1:

Message ID
''''''''''

This parameter identifies the operation. It is used to distinguish this
operation from other notifications or operations that the DIMSE Service
Provider may have in progress. No two identical values for the Message
ID (0000,0110) shall be used for outstanding operations or
notifications.

.. note::

   The Message ID (0000,0110) is recommended to be unique within the
   scope of an Association, to support debug procedures.

.. _sect_10.1.6.1.2:

Message ID Being Responded To
'''''''''''''''''''''''''''''

This parameter specifies the Message ID (0000,0110) of the operation
request/indication to which this response/confirmation applies.

.. _sect_10.1.6.1.3:

Requested SOP Class UID
'''''''''''''''''''''''

This parameter specifies the SOP Class that is to be deleted.

.. _sect_10.1.6.1.4:

Requested SOP Instance UID
''''''''''''''''''''''''''

This parameter specifies the SOP Instance that is to be deleted.

.. _sect_10.1.6.1.5:

Affected SOP Class UID
''''''''''''''''''''''

This parameter may be included in the response/confirmation. If included
in the response/confirmation, this parameter shall be equal to the
parameter value used in the request/indication.

.. _sect_10.1.6.1.6:

Affected SOP Instance UID
'''''''''''''''''''''''''

This parameter specifies the SOP Instance that was deleted. It may be
included in any response/confirmation and when included shall be equal
to the Requested SOP Instance UID (0000,1001) parameter value used in
the invocation.

.. _sect_10.1.6.1.7:

Status
''''''

This parameter contains the error or success notification for the
operation. It shall be included by the performing DIMSE Service User in
any response/confirmation. The following types of status may occur (see
also `Status Type Encoding (Normative) <#chapter_C>`__):

-  Class-Instance conflict (0119H) - the specified SOP Instance is not a
   member of the specified SOP Class

-  Duplicate invocation (0210H) - the Message ID (0000,0110) specified
   is allocated to another notification or operation

-  Invalid SOP Instance (0117H) - the SOP Instance UID specified implied
   a violation of the UID construction rules

-  Mistyped argument (0212H) - one of the parameters supplied has not
   been agreed for use on the Association between the DIMSE Service
   Users

-  No such SOP Class (0118H) - the SOP Class was not recognized

-  No such SOP Instance (0112H) - the SOP Instance was not recognized

-  Processing Failure (0110H) - a general failure in processing the
   operation was encountered

-  Resource Limitation (0213H) - the operation was not performed due to
   resource limitation

-  Success (0000H) - successful operation

-  Unrecognized operation (0211H) - the operation is not one of those
   agreed between the DIMSE Service Users

-  Refused: Not authorized (0124H) - the DIMSE Service User was not
   authorized to invoke the operation.

.. _sect_10.1.6.2:

N-DELETE Service Procedures
^^^^^^^^^^^^^^^^^^^^^^^^^^^

The following N-DELETE procedures apply:

a. The invoking DIMSE Service User requests the performing DIMSE Service
   User to delete a managed SOP Instance by issuing an N-DELETE request
   primitive to the DIMSE Service Provider.

b. The DIMSE-service provider issues an N-DELETE indication primitive to
   the performing DIMSE Service User.

c. If the operation can be performed, the performing DIMSE Service User
   deletes the specified managed SOP Instance and generates a response
   indicating acceptance of the N-DELETE request primitive by issuing an
   N-DELETE response primitive to the DIMSE Service Provider. In this
   case the following procedure does not apply.

d. If the operation cannot be performed, then the performing DIMSE
   Service User rejects the N-DELETE request by issuing an N-DELETE
   response primitive with the appropriate error code to the DIMSE
   Service Provider.

e. The DIMSE Service Provider issues an N-DELETE confirmation primitive
   to the invoking DIMSE Service User, completing the N-DELETE
   operation.

.. _sect_10.2:

Sequencing
----------

.. _sect_10.2.1:

Types of Services
~~~~~~~~~~~~~~~~~

All operation and notifications shall be confirmed services.

.. _sect_10.2.2:

Usage Restrictions
~~~~~~~~~~~~~~~~~~

These services may only be invoked within the context of an established
Association.

.. _sect_10.2.3:

Disrupted Procedures
~~~~~~~~~~~~~~~~~~~~

These services do not disrupt any other service procedure.

.. _sect_10.2.4:

Disrupting Procedures
~~~~~~~~~~~~~~~~~~~~~

These services are disrupted by the A-ABORT service procedure.

.. _sect_10.3:

Protocol
--------

This section specifies the protocol necessary to perform the set of
DIMSE-N operations and notifications. The Value Representations (VR)
specified in the following tables shall be encoded as defined in .

.. _sect_10.3.1:

N-EVENT-REPORT Protocol
~~~~~~~~~~~~~~~~~~~~~~~

The information necessary for the N-EVENT-REPORT request and indication
DIMSE-N primitives are conveyed in the N-EVENT-REPORT-RQ Message. The
information necessary for the N-EVENT-REPORT response and confirmation
DIMSE-N primitives are conveyed in the N-EVENT-REPORT-RSP Message.

.. _sect_10.3.1.1:

N-EVENT-REPORT-RQ
^^^^^^^^^^^^^^^^^

The N-EVENT-REPORT-RQ Message contains fields as defined in
`table_title <#table_10.3-1>`__. Each field shall conform to DICOM
encoding and Value Representation as defined in . Fields are required as
specified in the N-EVENT-REPORT service definition unless otherwise
noted in `table_title <#table_10.3-1>`__. Fields not specified in the
N-EVENT-REPORT service definition but present in
`table_title <#table_10.3-1>`__ are required by the DIMSE-N protocol.

.. table:: N-EVENT-REPORT-RQ Message Fields

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
   |                |             |        |        | Instance for   |
   |                |             |        |        | which this     |
   |                |             |        |        | event          |
   |                |             |        |        | occurred.      |
   +----------------+-------------+--------+--------+----------------+
   | Command Field  | (0000,0100) | US     | 1      | This field     |
   |                |             |        |        | distinguishes  |
   |                |             |        |        | the DIMSE-N    |
   |                |             |        |        | notification   |
   |                |             |        |        | conveyed by    |
   |                |             |        |        | this Message.  |
   |                |             |        |        | The value of   |
   |                |             |        |        | this field     |
   |                |             |        |        | shall be set   |
   |                |             |        |        | to 0100H for   |
   |                |             |        |        | the            |
   |                |             |        |        | N-E            |
   |                |             |        |        | VENT-REPORT-RQ |
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
   | Set Type       |             |        |        | indicates if a |
   |                |             |        |        | Data Set is    |
   |                |             |        |        | present in the |
   |                |             |        |        | Message. This  |
   |                |             |        |        | field shall be |
   |                |             |        |        | set to the     |
   |                |             |        |        | value of 0101H |
   |                |             |        |        | if no Data Set |
   |                |             |        |        | is present;    |
   |                |             |        |        | any other      |
   |                |             |        |        | value          |
   |                |             |        |        | indicates a    |
   |                |             |        |        | Data Set is    |
   |                |             |        |        | included in    |
   |                |             |        |        | the Message.   |
   +----------------+-------------+--------+--------+----------------+
   | Affected SOP   | (0000,1000) | UI     | 1      | Contains the   |
   | Instance UID   |             |        |        | UID of the SOP |
   |                |             |        |        | Instance for   |
   |                |             |        |        | which this     |
   |                |             |        |        | event          |
   |                |             |        |        | occurred.      |
   +----------------+-------------+--------+--------+----------------+
   | Event Type ID  | (0000,1002) | US     | 1      | Values for     |
   |                |             |        |        | this field are |
   |                |             |        |        | applica        |
   |                |             |        |        | tion-specific. |
   +----------------+-------------+--------+--------+----------------+
   | Event          | (no tag)    | -      | -      | Applic         |
   | Information    |             |        |        | ation-specific |
   |                |             |        |        | Data Set       |
   |                |             |        |        | containing     |
   |                |             |        |        | additional     |
   |                |             |        |        | information    |
   |                |             |        |        | related to the |
   |                |             |        |        | operation.     |
   +----------------+-------------+--------+--------+----------------+

.. note::

   1. Service Class Specifications contained in defines the values
      needed for the Event Type ID parameter.

   2. Service Class Specifications contained in defines the Data Set
      needed for the Event Information parameter.

.. _sect_10.3.1.2:

N-EVENT-REPORT-RSP
^^^^^^^^^^^^^^^^^^

The N-EVENT-REPORT-RSP Message contains fields as defined in
`table_title <#table_10.3-2>`__ and `Status Type Encoding
(Normative) <#chapter_C>`__. Each field shall conform to DICOM encoding
and Value Representation as defined in . Fields are required as
specified in the N-EVENT-REPORT service definition unless otherwise
noted in `table_title <#table_10.3-2>`__. Fields not specified in the
N-EVENT-REPORT service definition but present in
`table_title <#table_10.3-2>`__ are required by the DIMSE-N protocol.

.. table:: N-EVENT-REPORT-RSP Message Fields

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
   |                |             |        |        | Instance for   |
   |                |             |        |        | which this     |
   |                |             |        |        | event          |
   |                |             |        |        | occurred.      |
   +----------------+-------------+--------+--------+----------------+
   | Command Field  | (0000,0100) | US     | 1      | This field     |
   |                |             |        |        | distinguishes  |
   |                |             |        |        | the DIMSE-N    |
   |                |             |        |        | operation      |
   |                |             |        |        | conveyed by    |
   |                |             |        |        | this Message.  |
   |                |             |        |        | The value of   |
   |                |             |        |        | this field     |
   |                |             |        |        | shall be set   |
   |                |             |        |        | to 8100H for   |
   |                |             |        |        | the            |
   |                |             |        |        | N-EV           |
   |                |             |        |        | ENT-REPORT-RSP |
   |                |             |        |        | Message.       |
   +----------------+-------------+--------+--------+----------------+
   | Message ID     | (0000,0120) | US     | 1      | Shall be set   |
   | Being          |             |        |        | to the value   |
   | Responded To   |             |        |        | of the Message |
   |                |             |        |        | ID (0000,0110) |
   |                |             |        |        | field used in  |
   |                |             |        |        | associated     |
   |                |             |        |        | N-E            |
   |                |             |        |        | VENT-REPORT-RQ |
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
   |                |             |        |        | if no Data Set |
   |                |             |        |        | is present;    |
   |                |             |        |        | any other      |
   |                |             |        |        | value          |
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
   | Affected SOP   | (0000,1000) | UI     | 1      | Contains the   |
   | Instance UID   |             |        |        | UID of the SOP |
   |                |             |        |        | Instance for   |
   |                |             |        |        | which this     |
   |                |             |        |        | event          |
   |                |             |        |        | occurred.      |
   +----------------+-------------+--------+--------+----------------+
   | Event Type ID  | (0000,1002) | US     | 1      | Values for     |
   |                |             |        |        | this field are |
   |                |             |        |        | applica        |
   |                |             |        |        | tion-specific. |
   +----------------+-------------+--------+--------+----------------+
   | Event Reply    | (no tag)    | -      | -      | Applic         |
   |                |             |        |        | ation-specific |
   |                |             |        |        | Data Set       |
   |                |             |        |        | containing     |
   |                |             |        |        | additional     |
   |                |             |        |        | information    |
   |                |             |        |        | related to the |
   |                |             |        |        | operation.     |
   +----------------+-------------+--------+--------+----------------+

.. note::

   1. Service Class Specifications contained in defines the values
      needed for the Event Type ID parameter.

   2. Service Class Specifications contained in defines the Data Set
      needed for the Event Reply parameter related to each defined Event
      Type ID.

.. _sect_10.3.1.3:

N-EVENT-REPORT Protocol Procedures
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

The N-EVENT-REPORT reporting procedures are initiated by the invoking
DIMSE Service User issuing an N-EVENT-REPORT request primitive. On
receipt of the N-EVENT-REPORT request primitive the DIMSE-N protocol
machine shall:

-  construct a Message conveying the N-EVENT-REPORT-RQ

-  send the Message using the P-DATA request service (see 8.1)

On receipt of a Message conveying an N-EVENT-REPORT-RQ the DIMSE-N
protocol machine shall issue an N-EVENT-REPORT indication primitive to
the performing DIMSE Service User.

On receipt of the N-EVENT-REPORT response primitive issued by the
performing DIMSE Service User **,**\ the DIMSE-N protocol machine shall:

-  construct a Message conveying the N-EVENT-REPORT-RSP

-  send the Message using the P-DATA request service (see `DIMSE
   Protocol <#sect_8.1>`__)

On receipt of a Message conveying an N-EVENT-REPORT-RSP the DIMSE-N
protocol machine shall issue an N-EVENT-REPORT confirmation primitive to
the invoking DIMSE Service User, thus completing the notification
procedure.

The performing DIMSE Service User may return an N-EVENT-REPORT-RSP with
the status of Failed or Refused before the complete N-EVENT-REPORT-RQ
request Message has been completely transmitted by the invoking DIMSE
Service User (this is called an early failed response). Upon receipt of
this Failed or Refused N-EVENT-REPORT-RSP the invoking DIMSE Service
User may terminate the Message before it is completely sent (i.e., set
the Last Fragment bit to 1 in a Data PDV for this Message, see `Usage of
the P-DATA Service By the DICOM Application Entity
(Normative) <#chapter_F>`__). Following this, it may invoke another
operation or notification. It is a protocol violation for an invoking
DIMSE Service User to set the Last Fragment bit to 1 before an
N-EVENT-REPORT-RQ Message has been completely transmitted if it has not
received a Failed or Refused N-EVENT-REPORT-RSP to that request.

.. note::

   When an Association is operating in asynchronous mode, it is possible
   for an invoking DIMSE Service User to transmit several Messages
   before a response. Therefore, while sending a Message it may receive
   a response to a previously transmitted Message. In this case this
   response is not an early failed response because the related Message
   has already been sent.

.. _sect_10.3.2:

N-GET Protocol
~~~~~~~~~~~~~~

The information necessary for the N-GET request and indication DIMSE-N
primitives are conveyed in the N-GET-RQ Message. The information
necessary for the N-GET response and confirmation DIMSE-N primitives are
conveyed in the N-GET-RSP Message.

.. _sect_10.3.2.1:

N-GET-RQ
^^^^^^^^

The N-GET-RQ Message contains fields as defined in
`table_title <#table_10.3-3>`__. Each field shall conform to DICOM
encoding and Value Representation as defined in . Fields are required as
specified in the N-GET service definition unless otherwise noted in
`table_title <#table_10.3-3>`__. Fields not specified in the N-GET
service definition but present in `table_title <#table_10.3-3>`__ are
required by the DIMSE-N protocol.

.. table:: N-GET-RQ Message Fields

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
   | Requested SOP  | (0000,0003) | UI     | 1      | SOP Class UID  |
   | Class UID      |             |        |        | of the SOP     |
   |                |             |        |        | Instance for   |
   |                |             |        |        | which          |
   |                |             |        |        | Attribute      |
   |                |             |        |        | Values are to  |
   |                |             |        |        | be retrieved.  |
   +----------------+-------------+--------+--------+----------------+
   | Command Field  | (0000,0100) | US     | 1      | This field     |
   |                |             |        |        | distinguishes  |
   |                |             |        |        | the DIMSE-N    |
   |                |             |        |        | operation      |
   |                |             |        |        | conveyed by    |
   |                |             |        |        | this Message.  |
   |                |             |        |        | The value of   |
   |                |             |        |        | this field     |
   |                |             |        |        | shall be set   |
   |                |             |        |        | to 0110H for   |
   |                |             |        |        | the N-GET-RQ   |
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
   |                |             |        |        | no Data Set    |
   |                |             |        |        | shall be       |
   |                |             |        |        | present in the |
   |                |             |        |        | Message. This  |
   |                |             |        |        | field shall be |
   |                |             |        |        | set to the     |
   |                |             |        |        | value of       |
   |                |             |        |        | 0101H).        |
   +----------------+-------------+--------+--------+----------------+
   | Requested SOP  | (0000,1001) | UI     | 1      | Contains the   |
   | Instance UID   |             |        |        | UID of the SOP |
   |                |             |        |        | Instance for   |
   |                |             |        |        | which          |
   |                |             |        |        | Attribute      |
   |                |             |        |        | Values are to  |
   |                |             |        |        | be retrieved.  |
   +----------------+-------------+--------+--------+----------------+
   | Attribute      | (0000,1005) | AT     | 1-n    | This field     |
   | Identifier     |             |        |        | contains an    |
   | List           |             |        |        | Attribute Tag  |
   |                |             |        |        | for each of    |
   |                |             |        |        | the n          |
   |                |             |        |        | Attributes     |
   |                |             |        |        | applicable to  |
   |                |             |        |        | the N-GET      |
   |                |             |        |        | operation.     |
   +----------------+-------------+--------+--------+----------------+

.. _sect_10.3.2.2:

N-GET-RSP
^^^^^^^^^

The N-GET-RSP Message contains fields as defined in
`table_title <#table_10.3-4>`__ and `Status Type Encoding
(Normative) <#chapter_C>`__. Each field shall conform to DICOM encoding
and Value Representation as defined in . Fields are required as
specified in the N-GET service definition unless otherwise noted in
`table_title <#table_10.3-4>`__. Fields not specified in the N-GET
service definition but present in `table_title <#table_10.3-4>`__ are
required by the DIMSE-N protocol.

.. table:: N-GET-RSP Message Fields

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
   |                |             |        |        | Instance for   |
   |                |             |        |        | which          |
   |                |             |        |        | Attribute      |
   |                |             |        |        | Values are     |
   |                |             |        |        | returned.      |
   +----------------+-------------+--------+--------+----------------+
   | Command Field  | (0000,0100) | US     | 1      | This field     |
   |                |             |        |        | distinguishes  |
   |                |             |        |        | the DIMSE-N    |
   |                |             |        |        | operation      |
   |                |             |        |        | conveyed by    |
   |                |             |        |        | this Message.  |
   |                |             |        |        | The value of   |
   |                |             |        |        | this field     |
   |                |             |        |        | shall be set   |
   |                |             |        |        | to 8110H for   |
   |                |             |        |        | the N-GET-RSP  |
   |                |             |        |        | Message.       |
   +----------------+-------------+--------+--------+----------------+
   | Message ID     | (0000,0120) | US     | 1      | Shall be set   |
   | Being          |             |        |        | to the value   |
   | Responded To   |             |        |        | of the Message |
   |                |             |        |        | ID (0000,0110) |
   |                |             |        |        | field used in  |
   |                |             |        |        | associated     |
   |                |             |        |        | N-GET-RQ       |
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
   |                |             |        |        | if no Data Set |
   |                |             |        |        | is present;    |
   |                |             |        |        | any other      |
   |                |             |        |        | value          |
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
   | Affected SOP   | (0000,1000) | UI     | 1      | Contains the   |
   | Instance UID   |             |        |        | UID of the SOP |
   |                |             |        |        | Instance for   |
   |                |             |        |        | which          |
   |                |             |        |        | Attribute      |
   |                |             |        |        | Values are     |
   |                |             |        |        | returned.      |
   +----------------+-------------+--------+--------+----------------+
   | Attribute List | (no tag)    | -      | -      | T his field is |
   |                |             |        |        | encoded as a   |
   |                |             |        |        | Data Set. One  |
   |                |             |        |        | Data Element   |
   |                |             |        |        | is encoded for |
   |                |             |        |        | each Attribute |
   |                |             |        |        | Value          |
   |                |             |        |        | returned.      |
   +----------------+-------------+--------+--------+----------------+

.. note::

   The permitted contents of Attribute List, encoded as a series of Data
   Elements, are defined in the Information Object Definition () and
   Service Class Specifications ().

.. _sect_10.3.2.3:

N-GET Protocol Procedures
^^^^^^^^^^^^^^^^^^^^^^^^^

The N-GET procedures are initiated by the invoking DIMSE Service User
issuing an N-GET request primitive. On receipt of the N-GET request
primitive the DIMSE-N protocol machine shall:

-  construct a Message conveying the N-GET-RQ

-  send the Message using the P-DATA request service (see 8.1)

On receipt of a Message conveying an N-GET-RQ the DIMSE-N protocol
machine shall issue an N-GET indication primitive to the performing
DIMSE Service User.

On receipt of the N-GET response primitive, issued by the performing
DIMSE Service User, the DIMSE-N protocol machine shall:

-  construct a Message conveying the N-GET-RSP

-  send the Message using the P-DATA request service (see 8.1)

On receipt of a Message conveying an N-GET-RSP the DIMSE-N protocol
machine shall issue an N-GET confirmation primitive to the invoking
DIMSE Service User, thus completing the N-GET procedure.

.. _sect_10.3.3:

N-SET Protocol
~~~~~~~~~~~~~~

The information necessary for the N-SET request and indication DIMSE-N
primitives are conveyed in the N-SET-RQ Message. The information
necessary for the N-SET response and confirmation DIMSE-N primitives are
conveyed in the N-SET-RSP Message. Fields not specified in the N-SET
service definition but present in `table_title <#table_10.3-3>`__ are
required by the DIMSE-N protocol.

.. _sect_10.3.3.1:

N-SET-RQ
^^^^^^^^

The N-SET-RQ Message contains fields as defined in
`table_title <#table_10.3-5>`__. Each field shall conform to DICOM
encoding and Value Representation as defined in . Fields are required as
specified in the N-SET service definition unless otherwise noted in
`table_title <#table_10.3-5>`__. Fields not specified in the N-SET
service definition but present in `table_title <#table_10.3-5>`__ are
required by the DIMSE-N protocol.

.. table:: N-SET-RQ Message Fields

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
   | Requested SOP  | (0000,0003) | UI     | 1      | SOP Class UID  |
   | Class UID      |             |        |        | of the SOP     |
   |                |             |        |        | Instance for   |
   |                |             |        |        | which          |
   |                |             |        |        | Attribute      |
   |                |             |        |        | Values are to  |
   |                |             |        |        | be modified.   |
   +----------------+-------------+--------+--------+----------------+
   | Command Field  | (0000,0100) | US     | 1      | This field     |
   |                |             |        |        | distinguishes  |
   |                |             |        |        | the DIMSE-N    |
   |                |             |        |        | operation      |
   |                |             |        |        | conveyed by    |
   |                |             |        |        | this Message.  |
   |                |             |        |        | The value of   |
   |                |             |        |        | this field     |
   |                |             |        |        | shall be set   |
   |                |             |        |        | to 0120H for   |
   |                |             |        |        | the N-SET-RQ   |
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
   |                |             |        |        | a Data Set is  |
   |                |             |        |        | present in the |
   |                |             |        |        | Message. It    |
   |                |             |        |        | shall be set   |
   |                |             |        |        | to any value   |
   |                |             |        |        | other than     |
   |                |             |        |        | 0101H (Null).  |
   +----------------+-------------+--------+--------+----------------+
   | Requested SOP  | (0000,1001) | UI     | 1      | Contains the   |
   | Instance UID   |             |        |        | UID of the SOP |
   |                |             |        |        | Instance for   |
   |                |             |        |        | which          |
   |                |             |        |        | Attribute      |
   |                |             |        |        | Values are to  |
   |                |             |        |        | be modified.   |
   +----------------+-------------+--------+--------+----------------+
   | Modification   | (no tag)    | -      | -      | This field is  |
   | List           |             |        |        | encoded as a   |
   |                |             |        |        | Data Set. One  |
   |                |             |        |        | Data Element   |
   |                |             |        |        | is encoded for |
   |                |             |        |        | each Attribute |
   |                |             |        |        | and Attribute  |
   |                |             |        |        | Value          |
   |                |             |        |        | applicable to  |
   |                |             |        |        | the operation. |
   +----------------+-------------+--------+--------+----------------+

.. note::

   The permitted contents of Modification List, encoded as a series of
   Data Elements, are defined in the Information Object Definition ()
   and Service Class Specifications ().

.. _sect_10.3.3.2:

N-SET-RSP
^^^^^^^^^

The N-SET-RSP Message contains all fields as defined in
`table_title <#table_10.3-6>`__ and in `Status Type Encoding
(Normative) <#chapter_C>`__. Each field shall conform to DICOM encoding
and Value Representation as defined in . Fields are required as
specified in the N-SET service definition unless otherwise noted. Fields
not specified in the N-SET service definition but present in
`table_title <#table_10.3-6>`__ are required by the DIMSE-N protocol.

.. table:: N-SET-RSP Message Fields

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
   |                |             |        |        | Instance for   |
   |                |             |        |        | which          |
   |                |             |        |        | Attribute      |
   |                |             |        |        | Values were    |
   |                |             |        |        | modified.      |
   +----------------+-------------+--------+--------+----------------+
   | Command Field  | (0000,0100) | US     | 1      | This field     |
   |                |             |        |        | distinguishes  |
   |                |             |        |        | the DIMSE-N    |
   |                |             |        |        | operation      |
   |                |             |        |        | conveyed by    |
   |                |             |        |        | this Message.  |
   |                |             |        |        | The value of   |
   |                |             |        |        | this field     |
   |                |             |        |        | shall be set   |
   |                |             |        |        | to 8120H for   |
   |                |             |        |        | the N-SET-RSP  |
   |                |             |        |        | Message.       |
   +----------------+-------------+--------+--------+----------------+
   | Message ID     | (0000,0120) | US     | 1      | Shall be set   |
   | Being          |             |        |        | to the value   |
   | Responded To   |             |        |        | of the Message |
   |                |             |        |        | ID (0000,0110) |
   |                |             |        |        | field used in  |
   |                |             |        |        | associated     |
   |                |             |        |        | N-SET-RQ       |
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
   |                |             |        |        | if no Data Set |
   |                |             |        |        | is present;    |
   |                |             |        |        | any other      |
   |                |             |        |        | value          |
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
   | Affected SOP   | (0000,1000) | UI     | 1      | Contains the   |
   | Instance UID   |             |        |        | UID of the SOP |
   |                |             |        |        | Instance for   |
   |                |             |        |        | which          |
   |                |             |        |        | Attribute      |
   |                |             |        |        | Values were    |
   |                |             |        |        | modified.      |
   +----------------+-------------+--------+--------+----------------+
   | Attribute List | (no tag)    | -      | -      | This field is  |
   |                |             |        |        | encoded as a   |
   |                |             |        |        | Data Set. One  |
   |                |             |        |        | Data Element   |
   |                |             |        |        | is encoded for |
   |                |             |        |        | each Attribute |
   |                |             |        |        | and Attribute  |
   |                |             |        |        | Value          |
   |                |             |        |        | applicable to  |
   |                |             |        |        | the operation. |
   +----------------+-------------+--------+--------+----------------+

.. note::

   The permitted contents of Attribute List, encoded as a series of Data
   Elements, are defined in the Information Object Definition () and
   Service Class Specifications ().

.. _sect_10.3.3.3:

N-SET Protocol Procedures
^^^^^^^^^^^^^^^^^^^^^^^^^

The N-SET procedures are initiated by the invoking DIMSE Service User
issuing an N-SET request primitive. On receipt of the N-SET request
primitive the DIMSE-N protocol machine shall:

-  construct a Message conveying the N-SET-RQ

-  send the Message using the P-DATA request service (see 8.1)

On receipt of a Message conveying an N-SET-RQ the DIMSE-N protocol
machine shall issue an N-SET indication primitive to the performing
DIMSE Service User.

On receipt of the N-SET response primitive, issued by the performing
DIMSE Service User, the DIMSE-N protocol machine shall:

-  construct a Message conveying the N-SET-RSP

-  send the Message using the P-DATA request service (see 8.1)

On receipt of a Message conveying an N-SET-RSP the DIMSE-N protocol
machine shall issue an N-SET confirmation primitive to the invoking
DIMSE Service User, thus completing the N-SET procedure.

The performing DIMSE Service User may return an N-SET-RSP with the
status of Failed or Refused before the complete N-SET-RQ request Message
has been completely transmitted by the invoking DIMSE Service User (this
is called an early failed response). Upon receipt of this Failed or
Refused N-SET-RSP the invoking DIMSE Service User may terminate the
Message before it is completely sent (i.e., set the Last Fragment bit to
1 in a Data PDV for this Message, see `Usage of the P-DATA Service By
the DICOM Application Entity (Normative) <#chapter_F>`__). Following
this, it may invoke another operation or notification. It is a protocol
violation for an invoking DIMSE Service User to set the Last Fragment
bit to 1 before an N-SET-RQ Message has been completely transmitted if
it has not received a Failed or Refused N-SET-RSP to that request.

.. note::

   When an Association is operating in asynchronous mode, it is possible
   for an invoking DIMSE Service User to transmit several Messages
   before a response. Therefore, while sending a Message it may receive
   a response to a previously transmitted Message. In this case this
   response is not an early failed response because the related Message
   has already been sent.

.. _sect_10.3.4:

N-ACTION Protocol
~~~~~~~~~~~~~~~~~

The information necessary for the N-ACTION request and indication
DIMSE-N primitives are conveyed in the N-ACTION-RQ Message. The
information necessary for the N-ACTION response and confirmation DIMSE-N
primitives are conveyed in the N-ACTION-RSP Message.

.. _sect_10.3.4.1:

N-ACTION-RQ
^^^^^^^^^^^

The N-ACTION-RQ Message contains fields as defined in
`table_title <#table_10.3-7>`__. Each field shall conform to DICOM
encoding and Value Representation as defined in . Fields are required as
specified in the N-ACTION service definition unless otherwise noted in
`table_title <#table_10.3-7>`__. Fields not specified in the N-ACTION
service definition but present in `table_title <#table_10.3-7>`__ are
required by the DIMSE-N protocol.

.. table:: N-ACTION-RQ Message Fields

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
   | Requested SOP  | (0000,0003) | UI     | 1      | SOP Class UID  |
   | Class UID      |             |        |        | of the SOP     |
   |                |             |        |        | Instance for   |
   |                |             |        |        | which the      |
   |                |             |        |        | action is to   |
   |                |             |        |        | be performed.  |
   +----------------+-------------+--------+--------+----------------+
   | Command Field  | (0000,0100) | US     | 1      | This field     |
   |                |             |        |        | distinguishes  |
   |                |             |        |        | the DIMSE-N    |
   |                |             |        |        | operation      |
   |                |             |        |        | conveyed by    |
   |                |             |        |        | this Message.  |
   |                |             |        |        | The value of   |
   |                |             |        |        | this field     |
   |                |             |        |        | shall be set   |
   |                |             |        |        | to 0130H for   |
   |                |             |        |        | the            |
   |                |             |        |        | N-ACTION-RQ    |
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
   | Set Type       |             |        |        | indicates if a |
   |                |             |        |        | Data Set is    |
   |                |             |        |        | present in the |
   |                |             |        |        | Message. This  |
   |                |             |        |        | field shall be |
   |                |             |        |        | set to the     |
   |                |             |        |        | value of 0101H |
   |                |             |        |        | if no Data Set |
   |                |             |        |        | is present;    |
   |                |             |        |        | any other      |
   |                |             |        |        | value          |
   |                |             |        |        | indicates a    |
   |                |             |        |        | Data Set is    |
   |                |             |        |        | included in    |
   |                |             |        |        | the Message.   |
   +----------------+-------------+--------+--------+----------------+
   | Requested SOP  | (0000,1001) | UI     | 1      | Contains the   |
   | Instance UID   |             |        |        | UID of the SOP |
   |                |             |        |        | Instance for   |
   |                |             |        |        | which the      |
   |                |             |        |        | action is to   |
   |                |             |        |        | be performed.  |
   +----------------+-------------+--------+--------+----------------+
   | Action Type ID | (0000,1008) | US     | 1      | Values for     |
   |                |             |        |        | this field are |
   |                |             |        |        | applica        |
   |                |             |        |        | tion-specific. |
   +----------------+-------------+--------+--------+----------------+
   | Action         | (no tag)    | -      | -      | Applic         |
   | Information    |             |        |        | ation-specific |
   |                |             |        |        | Data Set       |
   |                |             |        |        | containing     |
   |                |             |        |        | additional     |
   |                |             |        |        | information    |
   |                |             |        |        | related to the |
   |                |             |        |        | operation.     |
   +----------------+-------------+--------+--------+----------------+

.. note::

   1. Service Class Specifications contained in define the values needed
      for the Action Type ID (0000,1008) parameter.

   2. Service Class Specifications contained in define the Data Set
      needed for the Action Information parameter.

.. _sect_10.3.4.2:

N-ACTION-RSP
^^^^^^^^^^^^

The N-ACTION-RSP Message contains fields as defined in
`table_title <#table_10.3-8>`__ and `Status Type Encoding
(Normative) <#chapter_C>`__. Each field shall conform to DICOM encoding
and Value Representation as defined in . Fields are required as
specified in the N-ACTION service definition unless otherwise noted in
`table_title <#table_10.3-8>`__. Fields not specified in the N-ACTION
service definition but present in `table_title <#table_10.3-8>`__ are
required by the DIMSE-N protocol.

.. table:: N-ACTION-RSP Message Fields

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
   |                |             |        |        | Instance for   |
   |                |             |        |        | which the      |
   |                |             |        |        | action was     |
   |                |             |        |        | performed.     |
   +----------------+-------------+--------+--------+----------------+
   | Command Field  | (0000,0100) | US     | 1      | This field     |
   |                |             |        |        | distinguishes  |
   |                |             |        |        | the DIMSE-N    |
   |                |             |        |        | operation      |
   |                |             |        |        | conveyed by    |
   |                |             |        |        | this Message.  |
   |                |             |        |        | The value of   |
   |                |             |        |        | this field     |
   |                |             |        |        | shall be set   |
   |                |             |        |        | to 8130H for   |
   |                |             |        |        | the            |
   |                |             |        |        | N-ACTION-RSP   |
   |                |             |        |        | Message.       |
   +----------------+-------------+--------+--------+----------------+
   | Message ID     | (0000,0120) | US     | 1      | Shall be set   |
   | Being          |             |        |        | to the value   |
   | Responded To   |             |        |        | of the Message |
   |                |             |        |        | ID (0000,0110) |
   |                |             |        |        | field used in  |
   |                |             |        |        | associated     |
   |                |             |        |        | N-ACTION-RQ    |
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
   |                |             |        |        | if no Data Set |
   |                |             |        |        | is present;    |
   |                |             |        |        | any other      |
   |                |             |        |        | value          |
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
   | Affected SOP   | (0000,1000) | UI     | 1      | Contains the   |
   | Instance UID   |             |        |        | UID of the SOP |
   |                |             |        |        | Instance for   |
   |                |             |        |        | which the      |
   |                |             |        |        | action was     |
   |                |             |        |        | performed.     |
   +----------------+-------------+--------+--------+----------------+
   | Action Type ID | (0000,1008) | US     | 1      | Values for     |
   |                |             |        |        | this field are |
   |                |             |        |        | applica        |
   |                |             |        |        | tion-specific. |
   +----------------+-------------+--------+--------+----------------+
   | Action Reply   | (no tag)    | -      | -      | Applic         |
   |                |             |        |        | ation-specific |
   |                |             |        |        | Data Set       |
   |                |             |        |        | containing     |
   |                |             |        |        | additional     |
   |                |             |        |        | information    |
   |                |             |        |        | related to the |
   |                |             |        |        | operation.     |
   +----------------+-------------+--------+--------+----------------+

.. note::

   1. Service Class Specifications contained in define the values needed
      for the Action Type ID (0000,1008) parameter.

   2. Service Class Specifications contained in define the Data Set
      needed for the Action Reply parameter related to each defined
      Action Type ID.

   3. Service Class Specifications contained in define the encoding of
      the Action Reply parameter.

.. _sect_10.3.4.3:

N-ACTION Protocol Procedures
^^^^^^^^^^^^^^^^^^^^^^^^^^^^

The N-ACTION procedures are initiated by the invoking DIMSE Service User
issuing an N-ACTION request primitive. On receipt of the N-ACTION
request primitive the DIMSE-N protocol machine shall:

-  construct a Message conveying the N-ACTION-RQ

-  send the Message using the P-DATA request service (see 8.1)

On receipt of a Message conveying an N-ACTION-RQ the DIMSE-N protocol
machine shall issue an N-ACTION indication primitive to the performing
DIMSE Service User.

On receipt of the N-ACTION response primitive, issued by the performing
DIMSE Service User, the DIMSE-N protocol machine shall:

-  construct a Message conveying the N-ACTION-RSP

-  send the Message using the P-DATA request service (see 8.1)

On receipt of a Message conveying an N-ACTION-RSP the DIMSE-N protocol
machine shall issue an N-ACTION confirmation primitive to the invoking
DIMSE Service User, thus completing the N-ACTION procedure.

The performing DIMSE Service User may return an N-ACTION-RSP with the
status of Failed or Refused before the complete N-ACTION-RQ request
Message has been completely transmitted by the invoking DIMSE Service
User (this is called an early failed response). Upon receipt of this
Failed or Refused N-ACTION-RSP the invoking DIMSE Service User may
terminate the Message before it is completely sent (i.e., set the Last
Fragment bit to 1 in a Data PDV for this Message, see `Usage of the
P-DATA Service By the DICOM Application Entity
(Normative) <#chapter_F>`__). Following this, it may invoke another
operation or notification. It is a protocol violation for an invoking
DIMSE Service User to set the Last Fragment bit to 1 before an
N-ACTION-RQ Message has been completely transmitted if it has not
received a Failed or Refused N-ACTION-RSP to that request.

.. note::

   When an Association is operating in asynchronous mode, it is possible
   for an invoking DIMSE Service User to transmit several Messages
   before a response. Therefore, while sending a Message it may receive
   a response to a previously transmitted Message. In this case this
   response is not an early failed response because the related Message
   has already been sent.

.. _sect_10.3.5:

N-CREATE Protocol
~~~~~~~~~~~~~~~~~

The information necessary for the N-CREATE request and indication
DIMSE-N primitives are conveyed in the N-CREATE-RQ Message. The
information necessary for the N-CREATE response and confirmation DIMSE-N
primitives are conveyed in the N-CREATE-RSP Message.

.. _sect_10.3.5.1:

N-CREATE-RQ
^^^^^^^^^^^

The N-CREATE-RQ Message contains fields as defined in
`table_title <#table_10.3-9>`__. Each field shall conform to DICOM
encoding and Value Representation as defined in . Fields are required as
specified in the N-CREATE service definition unless otherwise noted in
`table_title <#table_10.3-9>`__. Fields not specified in the N-CREATE
service definition but present in `table_title <#table_10.3-9>`__ are
required by the DIMSE-N protocol.

.. table:: N-CREATE-RQ Message Fields

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
   |                |             |        |        | created.       |
   +----------------+-------------+--------+--------+----------------+
   | Command Field  | (0000,0100) | US     | 1      | This field     |
   |                |             |        |        | distinguishes  |
   |                |             |        |        | the DIMSE-N    |
   |                |             |        |        | operation      |
   |                |             |        |        | conveyed by    |
   |                |             |        |        | this Message.  |
   |                |             |        |        | The value of   |
   |                |             |        |        | this field     |
   |                |             |        |        | shall be set   |
   |                |             |        |        | to 0140H for   |
   |                |             |        |        | the            |
   |                |             |        |        | N-CREATE-RQ    |
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
   |                |             |        |        | if a Data Set  |
   |                |             |        |        | is present in  |
   |                |             |        |        | the Message.   |
   |                |             |        |        | This field     |
   |                |             |        |        | shall be set   |
   |                |             |        |        | to the value   |
   |                |             |        |        | of 0101H if no |
   |                |             |        |        | Data Set is    |
   |                |             |        |        | present; any   |
   |                |             |        |        | other value    |
   |                |             |        |        | indicates a    |
   |                |             |        |        | Data Set is    |
   |                |             |        |        | included in    |
   |                |             |        |        | the Message.   |
   +----------------+-------------+--------+--------+----------------+
   | Affected SOP   | (0000,1000) | UI     | 1      | Contains the   |
   | Instance UID   |             |        |        | UID of the SOP |
   |                |             |        |        | Instance to be |
   |                |             |        |        | created.       |
   +----------------+-------------+--------+--------+----------------+
   | Attribute List | (no tag)    | -      | -      | This field is  |
   |                |             |        |        | encoded as a   |
   |                |             |        |        | Data Set. One  |
   |                |             |        |        | Data Element   |
   |                |             |        |        | is encoded for |
   |                |             |        |        | each Attribute |
   |                |             |        |        | and Attribute  |
   |                |             |        |        | Value          |
   |                |             |        |        | applicable to  |
   |                |             |        |        | the operation. |
   +----------------+-------------+--------+--------+----------------+

.. note::

   The permitted contents of Attribute List, encoded as a series of Data
   Elements, are defined in the Information Object Definition () and
   Service Class Specifications ().

.. _sect_10.3.5.2:

N-CREATE-RSP
^^^^^^^^^^^^

The N-CREATE-RSP Message contains fields as defined in
`table_title <#table_10.3-10>`__ and `Status Type Encoding
(Normative) <#chapter_C>`__. Each field shall conform to DICOM encoding
and Value Representation as defined in . Fields are required as
specified in the N-CREATE service definition unless otherwise noted in
Table10.3-10. Fields not specified in the N-CREATE service definition
but present in `table_title <#table_10.3-10>`__ are required by the
DIMSE-N protocol.

.. table:: N-CREATE-RSP Message Fields

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
   |                |             |        |        | Instance that  |
   |                |             |        |        | was created.   |
   +----------------+-------------+--------+--------+----------------+
   | Command Field  | (0000,0100) | US     | 1      | This field     |
   |                |             |        |        | distinguishes  |
   |                |             |        |        | the DIMSE-N    |
   |                |             |        |        | operation      |
   |                |             |        |        | conveyed by    |
   |                |             |        |        | this Message.  |
   |                |             |        |        | The value of   |
   |                |             |        |        | this field     |
   |                |             |        |        | shall be set   |
   |                |             |        |        | to 8140H for   |
   |                |             |        |        | the            |
   |                |             |        |        | N-CREATE-RSP   |
   |                |             |        |        | Message.       |
   +----------------+-------------+--------+--------+----------------+
   | Message ID     | (0000,0120) | US     | 1      | Shall be set   |
   | Being          |             |        |        | to the value   |
   | Responded To   |             |        |        | of the Message |
   |                |             |        |        | ID (0000,0110) |
   |                |             |        |        | field used in  |
   |                |             |        |        | associated     |
   |                |             |        |        | N-CREATE-RQ    |
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
   |                |             |        |        | if no Data Set |
   |                |             |        |        | is present;    |
   |                |             |        |        | any other      |
   |                |             |        |        | value          |
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
   | Affected SOP   | (0000,1000) | UI     | 1      | Contains the   |
   | Instance UID   |             |        |        | UID of the SOP |
   |                |             |        |        | Instance that  |
   |                |             |        |        | was created.   |
   +----------------+-------------+--------+--------+----------------+
   | Attribute List | (no tag)    | -      | -      | This field is  |
   |                |             |        |        | encoded as a   |
   |                |             |        |        | Data Set. One  |
   |                |             |        |        | Data Element   |
   |                |             |        |        | is encoded for |
   |                |             |        |        | each Attribute |
   |                |             |        |        | and Attribute  |
   |                |             |        |        | Value          |
   |                |             |        |        | applicable to  |
   |                |             |        |        | the operation. |
   +----------------+-------------+--------+--------+----------------+

.. note::

   The permitted contents of Attribute List, encoded as a series of Data
   Elements, are defined in the Information Object Definition () and
   Service Class Specifications ().

.. _sect_10.3.5.3:

N-CREATE Protocol Procedures
^^^^^^^^^^^^^^^^^^^^^^^^^^^^

The N-CREATE procedures are initiated by the invoking DIMSE Service User
issuing an N-CREATE request primitive. On receipt of the N-CREATE
request primitive the DIMSE-N protocol machine shall:

-  construct a Message conveying the N-CREATE-RQ

-  send the Message using the P-DATA request service (see 8.1)

On receipt of a Message conveying an N-CREATE-RQ the DIMSE-N protocol
machine shall issue an N-CREATE indication primitive to the performing
DIMSE Service User.

On receipt of the N-CREATE response primitive, issued by the performing
DIMSE Service User, the DIMSE-N protocol machine shall:

-  construct a Message conveying the N-CREATE-RSP

-  send the Message using the P-DATA request service (see 8.1)

On receipt of a Message conveying an N-CREATE-RSP the DIMSE-N protocol
machine shall issue an N-CREATE confirmation primitive to the invoking
DIMSE Service User, thus completing the N-CREATE procedure.

The performing DIMSE Service User may return an N-CREATE-RSP with the
status of Failed or Refused before the complete N-CREATE-RQ request
Message has been completely transmitted by the invoking DIMSE Service
User (this is called an early failed response). Upon receipt of this
Failed or Refused N-CREATE-RSP the invoking DIMSE Service User may
terminate the Message before it is completely sent (i.e., set the Last
Fragment bit to 1 in a Data PDV for this Message, see `Usage of the
P-DATA Service By the DICOM Application Entity
(Normative) <#chapter_F>`__). Following this, it may invoke another
operation or notification. It is a protocol violation for an invoking
DIMSE Service User to set the Last Fragment bit to 1 before an
N-CREATE-RQ Message has been completely transmitted if it has not
received a Failed or Refused N-CREATE-RSP to that request.

.. note::

   When an Association is operating in asynchronous mode, it is possible
   for an invoking DIMSE Service User to transmit several Messages
   before a response. Therefore, while sending a Message it may receive
   a response to a previously transmitted Message. In this case this
   response is not an early failed response because the related Message
   has already been sent.

.. _sect_10.3.6:

N-DELETE Protocol
~~~~~~~~~~~~~~~~~

The information necessary for the N-DELETE request and indication
DIMSE-N primitives are conveyed in the N-DELETE-RQ Message. The
information necessary for the N-DELETE response and confirmation DIMSE-N
primitives are conveyed in the N-DELETE-RSP Message.

.. _sect_10.3.6.1:

N-DELETE-RQ
^^^^^^^^^^^

The N-DELETE-RQ Message contains fields as defined in
`table_title <#table_10.3-11>`__. Each field shall conform to DICOM
encoding and Value Representation as defined in . Fields are required as
specified in the N-DELETE service definition unless otherwise noted in
`table_title <#table_10.3-11>`__. Fields not specified in the N-DELETE
service definition but present in `table_title <#table_10.3-11>`__ are
required by the DIMSE-N protocol.

.. table:: N-DELETE-RQ Message Fields

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
   | Requested SOP  | (0000,0003) | UI     | 1      | SOP Class UID  |
   | Class UID      |             |        |        | of the SOP     |
   |                |             |        |        | Instance to be |
   |                |             |        |        | deleted.       |
   +----------------+-------------+--------+--------+----------------+
   | Command Field  | (0000,0100) | US     | 1      | This field     |
   |                |             |        |        | distinguishes  |
   |                |             |        |        | the DIMSE-N    |
   |                |             |        |        | operation      |
   |                |             |        |        | conveyed by    |
   |                |             |        |        | this Message.  |
   |                |             |        |        | The value of   |
   |                |             |        |        | this field     |
   |                |             |        |        | shall be set   |
   |                |             |        |        | to 0150H for   |
   |                |             |        |        | the            |
   |                |             |        |        | N-DELETE-RQ    |
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
   |                |             |        |        | Message. It    |
   |                |             |        |        | shall be set   |
   |                |             |        |        | to the value   |
   |                |             |        |        | of 0101H.      |
   +----------------+-------------+--------+--------+----------------+
   | Requested SOP  | (0000,1001) | UI     | 1      | Contains the   |
   | Instance UID   |             |        |        | UID of the SOP |
   |                |             |        |        | Instance to be |
   |                |             |        |        | deleted.       |
   +----------------+-------------+--------+--------+----------------+

.. _sect_10.3.6.2:

N-DELETE-RSP
^^^^^^^^^^^^

The N-DELETE-RSP Message contains fields as defined in
`table_title <#table_10.3-12>`__ and `Status Type Encoding
(Normative) <#chapter_C>`__. Each field shall conform to DICOM encoding
and Value Representation as defined in . Fields are required as
specified in the N-DELETE service definition unless otherwise noted in
`table_title <#table_10.3-12>`__. Fields not specified in the N-DELETE
service definition but present in `table_title <#table_10.3-12>`__ are
required by the DIMSE-N protocol.

.. table:: N-DELETE-RSP Message Fields

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
   |                |             |        |        | Instance that  |
   |                |             |        |        | was deleted.   |
   +----------------+-------------+--------+--------+----------------+
   | Command Field  | (0000,0100) | US     | 1      | This field     |
   |                |             |        |        | distinguishes  |
   |                |             |        |        | the DIMSE-N    |
   |                |             |        |        | operation      |
   |                |             |        |        | conveyed by    |
   |                |             |        |        | this Message.  |
   |                |             |        |        | The value of   |
   |                |             |        |        | this field     |
   |                |             |        |        | shall be set   |
   |                |             |        |        | to 8150H for   |
   |                |             |        |        | the            |
   |                |             |        |        | N-DELETE-RSP   |
   |                |             |        |        | Message.       |
   +----------------+-------------+--------+--------+----------------+
   | Message ID     | (0000,0120) | US     | 1      | Shall be set   |
   | Being          |             |        |        | to the value   |
   | Responded To   |             |        |        | of the Message |
   |                |             |        |        | ID (0000,0110) |
   |                |             |        |        | field used in  |
   |                |             |        |        | associated     |
   |                |             |        |        | N-DELETE-RQ    |
   |                |             |        |        | Message.       |
   +----------------+-------------+--------+--------+----------------+
   | Command Data   | (0000,0800) | US     | 1      | This field     |
   | Set Type       |             |        |        | indicates that |
   |                |             |        |        | no Data Set is |
   |                |             |        |        | present in the |
   |                |             |        |        | Message. This  |
   |                |             |        |        | field shall be |
   |                |             |        |        | set to the     |
   |                |             |        |        | value of       |
   |                |             |        |        | 0101H).        |
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
   |                |             |        |        | Instance that  |
   |                |             |        |        | was deleted.   |
   +----------------+-------------+--------+--------+----------------+

.. _sect_10.3.6.3:

N-DELETE Protocol Procedures
^^^^^^^^^^^^^^^^^^^^^^^^^^^^

The N-DELETE procedures are initiated by the invoking DIMSE Service User
issuing an N-DELETE request primitive. On receipt of the N-DELETE
request primitive the DIMSE-N protocol machine shall:

-  construct a Message conveying the N-DELETE-RQ

-  end the Message using the P-DATA request service (see 8.1)

On receipt of a Message conveying an N-DELETE-RQ the DIMSE-N protocol
machine shall issue an N-DELETE indication primitive to the performing
DIMSE Service User.

On receipt of the N-DELETE response primitive, issued by the performing
DIMSE Service User, the DIMSE-N protocol machine shall:

-  construct a Message conveying the N-DELETE-RSP

-  send the Message using the P-DATA request service (see 8.1)

On receipt of a Message conveying an N-DELETE-RSP the DIMSE-N protocol
machine shall issue an N-DELETE confirmation primitive to the invoking
DIMSE Service User, thus completing the N-DELETE procedure.

