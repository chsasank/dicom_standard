.. _chapter_7:

Service Overview
================

The DICOM Message Service Element supports communication between peer
DIMSE Service Users. A DIMSE Service User acts in one of two roles:

a. invoking DIMSE Service User

b. performing DIMSE Service User

DIMSE Service Users make use of service primitives that are provided by
the DIMSE Service Provider. The DIMSE Service Provider is an abstraction
of the totality of those entities that provide DIMSE services to peer
DIMSE Service Users. A service primitive shall be one of the following
types:

a. request primitive

b. indication primitive

c. response primitive

d. confirmation primitive

These primitives (which are shown in `figure_title <#figure_7-1>`__) are
used as follows to successfully complete a DIMSE service:

-  The invoking DIMSE Service User issues a request primitive to the
   DIMSE Service Provider.

-  The DIMSE Service Provider receives the request primitive from the
   invoking DIMSE Service User and issues an indication primitive to the
   performing DIMSE Service User.

-  The performing DIMSE Service User receives the indication primitive
   from the DIMSE Service Provider and performs the requested service.

-  The performing DIMSE Service User issues a response primitive to the
   DIMSE Service Provider.

-  The DIMSE Service Provider receives the response primitive from the
   performing DIMSE Service User and issues a confirmation primitive to
   the invoking DIMSE Service User.

-  The invoking DIMSE Service User receives the confirmation primitive
   from the DIMSE Service Provider completing the DIMSE service.

.. _sect_7.1:

Service Types
-------------

DIMSE provides two types of information transfer services that are used
by DICOM Application Entities:

a. a notification service

b. an operation service

Notification services enable one DICOM Application Entity to notify
another about the occurrence of an event or change of state. The
definition of the notification and the consequent behavior of the
Application Entities is dependent upon the Service Class and Information
Object Definitions. See and .

Operation services enable one DICOM Application Entity to explicitly
request an operation to be performed upon a SOP Instance managed by
another DICOM Application Entity.

.. _sect_7.2:

DIMSE Service User Interaction
------------------------------

The DICOM Message Service Element receives notification and operation
requests and their related information from the DIMSE Service User. Two
DICOM Application Entities take the roles as peer DIMSE Service Users in
order to exchange notifications and operations.

A notification or operation is implemented as a request/response
interaction carried out within the context of an established application
Association. Typically, one DIMSE Service User requests that a
particular operation be performed (or notification be processed) and the
other DIMSE Service User attempts to perform the operation (or process
the notification) and then reports the outcome of the attempt.

When engaging in the operations or notifications, the DIMSE Service User
takes on one of two roles:

a. it performs operations (on SOP Instances for which it has
   responsibility) that were invoked by a peer DIMSE Service User. It
   may also emit change-of-state notifications for SOP Instances to one
   or more peer DIMSE Service Users. These notifications may be invoked
   as a result of operations initiated by other DIMSE Service Users.

b. it invokes the performance of an operation on a peer DIMSE Service
   User. It may also receive notifications from a peer DIMSE Service
   User.

These roles are depicted in `figure_title <#figure_7.2-1>`__.

.. note::

   1. Role a) (called the Agent role in ISO terminology) is used by an
      implementation that conforms to a DICOM Service Class as an SCP.

   2. Role b) (called the Manager role in ISO terminology) is used by an
      implementation that conforms to a DICOM Service Class as an SCU.

.. _sect_7.3:

Service Modes
-------------

Operations and notifications, on an Association, are used in one of the
following two modes:

a. synchronous

b. asynchronous

In the synchronous mode, the invoking DIMSE Service User, on an
established Association, requires a response from the performing DIMSE
Service User before invoking another operation or notification.

In the asynchronous mode, the invoking DIMSE Service User, on an
established Association, may continue to invoke further operations or
notifications to the performing DIMSE Service User without awaiting a
response. In the asynchronous mode, the performing DIMSE Service User
may respond to the operations or notifications in a different order than
they were received.

The mode selection (synchronous or asynchronous) is determined at
Association establishment time. The synchronous mode serves as the
default mode and shall be supported by all DIMSE Service Users. The
asynchronous mode is optional and the maximum number of outstanding
operations/notifications is negotiated during Association establishment.
This negotiation is accomplished by Application Association Information
as defined in `Association Negotiation (Normative) <#chapter_D>`__.

.. _sect_7.4:

Association Services
--------------------

The DICOM Message Service Element does not provide separate services for
the establishment and termination of application Associations. This
section provides an overview of how an Application Entity using the
DIMSE service uses the Association Services defined in .

During the Association establishment phase, a DIMSE Service User shall
exchange initialization information using parameters of the A-ASSOCIATE
Upper Layer Service (see `figure_title <#figure_7.4-1>`__) that include:

-  Application context

-  Presentation and session requirements

-  DIMSE-specific user information

-  Application Association Information

The A-RELEASE and A-ABORT Services defined in shall be used for the
termination of an Association.

.. note::

   The rules defining how the Association Services are used by a DIMSE
   Service User are defined in `Association Negotiation
   (Normative) <#chapter_D>`__.

.. _sect_7.4.1:

Association Establishment
~~~~~~~~~~~~~~~~~~~~~~~~~

The A-ASSOCIATE Service is invoked by a DIMSE Service User to establish
an Association with a peer DIMSE Service User. Association establishment
is always the first phase of DICOM Message Exchange.

The initiating DIMSE Service User and the responding DIMSE Service User
shall include Application Association Information on the request and
response primitive respectively. The meaning of this parameter is
Application Context specific. For more information on the use of the
Application Association Information, see `Association Negotiation
(Normative) <#chapter_D>`__.

.. _sect_7.4.2:

Association Release
~~~~~~~~~~~~~~~~~~~

The A-RELEASE Service is invoked by a DIMSE Service User to request the
orderly termination of an Association between peer DIMSE Service Users.
This Part of the Standard does not specify any use of the parameters of
the A-RELEASE service.

The A-ABORT Service is invoked by a DIMSE Service User to request the
abrupt termination of the Association between peer DIMSE Service Users.
The A-ABORT invoking DIMSE Service User shall include (within the
A-ABORT user information field) the Abort Source parameter. The Abort
Source parameter indicates the initiating source of the abort. It takes
one of the following symbolic values:

-  DIMSE Service Provider

-  DIMSE Service User

Reference for more information on the A-RELEASE and A-ABORT services.

.. _sect_7.5:

DIMSE Services
--------------

Because the manner in which operations applied to Composite SOP
Instances differ from operations and notifications applied to Normalized
SOP Instances, two groups of DIMSE services are defined:

-  DIMSE-N: those services applicable to Normalized SOP Instances

-  DIMSE-C: those services applicable to Composite SOP Instances

.. table:: DIMSE Services

   ============== ========= ============
   **Name**       **Group** **Type**
   ============== ========= ============
   C-STORE        DIMSE-C   operation
   C-GET          DIMSE-C   operation
   C-MOVE         DIMSE-C   operation
   C-FIND         DIMSE-C   operation
   C-ECHO         DIMSE-C   operation
   N-EVENT-REPORT DIMSE-N   notification
   N-GET          DIMSE-N   operation
   N-SET          DIMSE-N   operation
   N-ACTION       DIMSE-N   operation
   N-CREATE       DIMSE-N   operation
   N-DELETE       DIMSE-N   operation
   ============== ========= ============

.. note::

   Use of the Dialog command, supported in previous versions of this
   Standard, has been retired.

.. _sect_7.5.1:

DIMSE-C Services
~~~~~~~~~~~~~~~~

The DIMSE-C services allow a DICOM Application Entity to explicitly
request an operation by another DICOM Application Entity on Composite
SOP Instances. The operations allowed are intended to be effectively
compatible with those provided by previous versions of this Standard.
DIMSE-C provides only operation services.

.. _sect_7.5.1.1:

Operation Services
^^^^^^^^^^^^^^^^^^

DIMSE-C provides the following operation services that are all confirmed
services and as such a response is expected:

a. The C-STORE service is invoked by a DIMSE Service User to request the
   storage of Composite SOP Instance information by a peer DIMSE Service
   User.

b. The C-FIND service is invoked by a DIMSE Service User to match a
   series of Attribute strings against the Attributes of the set of SOP
   Instances managed by a peer DIMSE Service User. The C-FIND service
   returns for each match a list of requested Attributes and their
   values.

c. The C-GET service is invoked by a DIMSE Service User to fetch the
   information for one or more Composite SOP Instances from a peer DIMSE
   Service User, based upon the Attributes supplied by the invoking
   DIMSE Service User.

d. The C-MOVE service is invoked by a DIMSE Service User to move the
   information for one or more Composite SOP Instances from a peer DIMSE
   Service User, to a third party DIMSE Service User, based upon the
   Attributes supplied by the invoking DIMSE Service User

e. The C-ECHO service is invoked by a DIMSE Service User to verify
   end-to-end communications with a peer DIMSE Service User.

.. note::

   1. The major differences between a C-GET and a C-MOVE operation are
      that the:

      a. C-STORE sub-operations resulting from a C-GET are performed on
         the same Association as the C-GET. With a C-MOVE, the resulting
         C-STORE sub-operations are performed on a separate Association.

      b. C-MOVE operation supports C-STORE sub-operations being
         performed with an Application Entity that is not the one that
         initiated the C-MOVE (third party move).

   2. In the case where an Application Entity wishes to request that it
      receives one or more images for storage, it may use either a C-GET
      operation or a C-MOVE to itself. It is expected that in most
      environments the C-MOVE is a simpler solution despite the fact
      that two Associations are required. The use of the C-GET service
      may not be widely implemented. It may be implemented in special
      cases where a system does not support multiple Associations. It
      was left in this version of the Standard for backward
      compatibility with previous versions of the Standard.

.. _sect_7.5.2:

DIMSE-N Services
~~~~~~~~~~~~~~~~

The DIMSE-N services provide both notification and operation services
applicable to Normalized SOP Instances.

.. _sect_7.5.2.1:

Notification Service
^^^^^^^^^^^^^^^^^^^^

DIMSE-N provides a single Notification Service, the N-EVENT-REPORT. The
N-EVENT-REPORT service is invoked by a DIMSE Service User to report an
event about a SOP Instance to a peer DIMSE Service User. This service is
a confirmed service and a response is expected.

.. _sect_7.5.2.2:

Operation Services
^^^^^^^^^^^^^^^^^^

DIMSE-N provides the following operation services that are all confirmed
services and as such a response is expected:

a. The N-GET service is invoked by a DIMSE Service User to request the
   retrieval of information from a peer DIMSE Service User.

b. The N-SET service is invoked by a DIMSE Service User to request the
   modification of information by a peer DIMSE Service User.

c. The N-ACTION service is invoked by a DIMSE Service User to request a
   peer DIMSE Service User to perform an action.

d. The N-CREATE service is invoked by a DIMSE Service User to request a
   peer DIMSE Service User to create an instance of a SOP Class.

e. The N-DELETE service is invoked by a DIMSE Service User to request a
   peer DIMSE Service User to delete an instance of a SOP Class.

.. _sect_7.5.3:

DIMSE Procedures
~~~~~~~~~~~~~~~~

All DIMSE operations and notifications are confirmed services. The
performing DIMSE Service User shall report the response of each
operation or notification over the same Association on which the
operation or notification was invoked.

Each DIMSE service is accomplished through the use of one or more
service primitives. How the peer DIMSE Service Users utilize and react
to the service primitives are defined by the service procedures.

.. _sect_7.5.3.1:

Sub-Operations
^^^^^^^^^^^^^^

Some DIMSE services are atomic in that the service is performed by one
operation or notification. In such a case the DIMSE service primitives
are used by peer DIMSE Service Users to invoke and perform the operation
or notification.

Other DIMSE services require the use of one or more sub-operations to
perform the service. In such cases DIMSE service primitives are used by
peer DIMSE Service Users to invoke and perform each sub-operation. How
and when the sub-operation service primitives are used is defined by the
procedures for the DIMSE service.

.. _sect_7.5.3.2:

Multiple Responses
^^^^^^^^^^^^^^^^^^

Each DIMSE service requires one or more response primitives as a result
of the invocation of the service. How and when the multiple response
primitives are used is defined by the procedures for the DIMSE service.
Whether multiple responses are returned is conditional upon the
information included in the request primitive by the DIMSE Service User.

.. _sect_7.5.3.3:

Cancellation
^^^^^^^^^^^^

Certain DIMSE services permit the cancellation of the service through
the use of service primitives. This allows an invoking DIMSE Service
User to request termination of a DIMSE service after completion of the
request service primitive but prior to completion of the confirm service
primitive.

`table_title <#table_7.5-2>`__ lists each DIMSE service and its related
procedure information. The complete specifications for the service
procedures are defined in Sections 9 and 10 for DIMSE-C and DIMSE-N
respectively.

.. table:: DIMSE Services and Procedures

   ============== ================== ====================== ==========
   **Name**       **Sub-Operations** **Multiple Responses** **Cancel**
   ============== ================== ====================== ==========
   C-STORE        -                  -                      -
   C-GET          M                  C                      M
   C-MOVE         M                  C                      M
   C-FIND         -                  C                      M
   C-ECHO         -                  -                      -
   N-EVENT-REPORT -                  -                      -
   N-GET          -                  -                      -
   N-SET          -                  -                      -
   N-ACTION       -                  -                      -
   N-CREATE       -                  -                      -
   N-DELETE       -                  -                      -
   ============== ================== ====================== ==========

