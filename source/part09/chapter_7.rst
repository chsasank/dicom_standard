.. _chapter_7:

OSI Upper Layer Service for DICOM Application Entities
======================================================

This section provides a description of how to use the OSI Association
Control Service Element (ACSE) and OSI Presentation Layer to provide the
Upper Layer Service necessary to support the communication of DICOM
Application Entities. This Upper Layer Service is a fully conformant
subset of the services offered by the ACSE and the OSI Presentation
Layer.

The UL Services are listed in `table_title <#table_7-1>`__.

.. table:: Upper Layer Services

   =========== ==================
   SERVICE     TYPE
   =========== ==================
   A-ASSOCIATE Confirmed
   A-RELEASE   Confirmed
   A-ABORT     Non-Confirmed
   A-P-ABORT   Provider-initiated
   P-DATA      Non-Confirmed
   =========== ==================

In addition to the Upper Layer Service specification, this section
defines at the parameter level the use of each element of this Upper
Layer Service by DICOM Application Entities. The rules guiding the use
of this Upper Layer Service by the DICOM Application Entities are
addressed in .

.. _sect_7.1:

A-ASSOCIATE Service
-------------------

The establishment of an association between two AEs shall be performed
through ACSE A-ASSOCIATE request, indication, response and confirmation
primitives. The initiator of the service is hereafter called a requestor
and the service-user that receives the A-ASSOCIATE indication is
hereafter called the acceptor. It shall be a confirmed service.

.. note::

   The A-ASSOCIATE service supports the equivalent of a channel
   establishment in a point-to-point interface (see the retired PS3.9).

`figure_title <#figure_7-1>`__ illustrates the association establishment
between two AEs.

.. _sect_7.1.1:

A-ASSOCIATE Parameters
~~~~~~~~~~~~~~~~~~~~~~

`table_title <#table_7-2>`__ lists the parameters that shall be required
for the A-ASSOCIATE service used by DICOM Application Entities in this
Standard.

.. table:: Key A-ASSOCIATE Service Parameters

   +-----------------+---------+------------+----------+--------------+
   | A-ASSOCIATE     | Request | Indication | Response | Confirmation |
   | parameter name  |         |            |          |              |
   +=================+=========+============+==========+==============+
   | application     | M       | M(=)       | M        | M(=)         |
   | context name    |         |            |          |              |
   +-----------------+---------+------------+----------+--------------+
   | calling AE      | M       | M(=)       | M        | M(=)         |
   | title           |         |            |          |              |
   +-----------------+---------+------------+----------+--------------+
   | called AE title | M       | M(=)       | M        | M(=)         |
   +-----------------+---------+------------+----------+--------------+
   | user            | M       | M(=)       | M        | M(=)         |
   | information     |         |            |          |              |
   +-----------------+---------+------------+----------+--------------+
   | result          |         |            | M        | M(=)         |
   +-----------------+---------+------------+----------+--------------+
   | result source   |         |            |          | M            |
   +-----------------+---------+------------+----------+--------------+
   | diagnostic      |         |            | U        | C(=)         |
   +-----------------+---------+------------+----------+--------------+
   | calling         | M       | M(=)       |          |              |
   | presentation    |         |            |          |              |
   | address         |         |            |          |              |
   +-----------------+---------+------------+----------+--------------+
   | called          | M       | M(=)       |          |              |
   | presentation    |         |            |          |              |
   | address         |         |            |          |              |
   +-----------------+---------+------------+----------+--------------+
   | presentation    | M       | M(=)       |          |              |
   | context         |         |            |          |              |
   | definition list |         |            |          |              |
   +-----------------+---------+------------+----------+--------------+
   | presentation    |         |            | M        | M(=)         |
   | context         |         |            |          |              |
   | definition list |         |            |          |              |
   | result          |         |            |          |              |
   +-----------------+---------+------------+----------+--------------+

.. note::

   See Section 5 of this Part for table conventions.

`table_title <#table_7-3>`__ lists the parameters for the A-ASSOCIATE
service that shall contain fixed values or shall not be used by DICOM
Application Entities in this Standard.

.. table:: A-ASSOCIATE Service Parameter (Fixed or Not Used)

   +-----------------+---------+------------+----------+--------------+
   | A-ASSOCIATE     | Request | Indication | Response | Confirmation |
   | parameter name  |         |            |          |              |
   +=================+=========+============+==========+==============+
   | mode            | UF      | MF(=)      |          |              |
   +-----------------+---------+------------+----------+--------------+
   | responding AE   |         |            | MF       | MF(=)        |
   | title           |         |            |          |              |
   +-----------------+---------+------------+----------+--------------+
   | calling/ca      | NU      | NU         | NU       | NU           |
   | lled/responding |         |            |          |              |
   | AE qualifier    |         |            |          |              |
   +-----------------+---------+------------+----------+--------------+
   | calling/ca      | NU      | NU         | NU       | NU           |
   | lled/responding |         |            |          |              |
   | AP invoc-id     |         |            |          |              |
   +-----------------+---------+------------+----------+--------------+
   | calling/ca      | NU      | NU         | NU       | NU           |
   | lled/responding |         |            |          |              |
   | AE invoc-id     |         |            |          |              |
   +-----------------+---------+------------+----------+--------------+
   | responding      |         |            | MF       | MF(=)        |
   | presentation    |         |            |          |              |
   | address         |         |            |          |              |
   +-----------------+---------+------------+----------+--------------+
   | default context | NU      | NU         | NU       | NU           |
   | name/result     |         |            |          |              |
   +-----------------+---------+------------+----------+--------------+
   | presentation &  | UF      | UF(=)      | UF       | UF(=)        |
   | session         |         |            |          |              |
   | requirements    |         |            |          |              |
   +-----------------+---------+------------+----------+--------------+
   | other           | NU      | NU         | NU       | NU           |
   | parameters (see |         |            |          |              |
   | ISO 8822 &      |         |            |          |              |
   | 8649)           |         |            |          |              |
   +-----------------+---------+------------+----------+--------------+

.. _sect_7.1.1.1:

Mode (Fixed)
^^^^^^^^^^^^

This parameter allows the negotiation of the optional Mode OSI-ACSE
Service parameter. Only the default value of "normal" is used by DICOM
Application Entities. Therefore, this parameter shall always specify the
value "normal."

.. _sect_7.1.1.2:

Application Context Name
^^^^^^^^^^^^^^^^^^^^^^^^

This parameter identifies the application context proposed by the
requestor. The acceptor shall return either the same or a different
name. The returned name shall specify the application context to be used
for this association. Further discussion on Application Context Names
can be found in `Application Context Names
(Informative) <#chapter_A>`__.

An application context is an explicitly defined set of application
service elements, related options, and any other information necessary
for the interworking of application entities on an association.

.. note::

   The offer of an alternate application context by the acceptor
   provides a mechanism for limited negotiation. If the requestor cannot
   operate in the acceptor's application context, it shall issue an
   A-Abort request primitive. Application Context Names for the DICOM
   Application Entity as well as Application Context Names usage rules
   are defined in .

.. _sect_7.1.1.3:

Calling AE Title
^^^^^^^^^^^^^^^^

This parameter identifies the Application Entity (AE) that shall contain
the requestor of the A-ASSOCIATE service. It is based on the Source
DICOM Application Name. The relationship between DICOM Application Names
and AE titles is specified in `DICOM Addressing
(Normative) <#chapter_C>`__. The Calling AE title may or may not be the
same as the Initiator Address present in DICOM Messages exchanged over
the association.

.. note::

   It is the responsibility of the UL User that received the
   A-ASSOCIATE-RQ to verify whether the Calling AE Title is one of its
   known remote DICOM Application Names.

.. _sect_7.1.1.4:

Called AE Title
^^^^^^^^^^^^^^^

This parameter identifies the Application Entity that shall contain the
intended acceptor of the A-ASSOCIATE service. It is based on the
Destination DICOM Application Name. The relationship between DICOM
Application Name and AE titles is specified in `DICOM Addressing
(Normative) <#chapter_C>`__. The Called AE title may or may not be the
same as the Receiver Address present in DICOM Messages exchanged over
the association.

.. note::

   It is the responsibility of the UL User that received the
   A-ASSOCIATE-RQ to verify whether the Called AE Title is its (or one
   of its) DICOM Application Name(s).

.. _sect_7.1.1.5:

Responding AE Title (Fixed)
^^^^^^^^^^^^^^^^^^^^^^^^^^^

This parameter identifies the AE that shall contain the actual acceptor
of the A-ASSOCIATE service. In this Standard it shall always contain the
same value as the Called AE Title of the A-ASSOCIATE indication.

.. _sect_7.1.1.6:

User Information
^^^^^^^^^^^^^^^^

This parameter shall be used by the requestor and the acceptor of the
association to include DICOM Application Entity user information. Its
meaning shall depend on the application context that accompanies the
primitive. The usage of this parameter is specified in `Use and Format
of the A-ASSOCIATE User Information Parameter
(Normative) <#chapter_D>`__.

.. note::

   1. This parameter is used to carry initialization information for the
      DICOM Application Entities as defined in the application context
      specified by the value of the accompanying Application Context
      Name parameter.

   2. `Use and Format of the A-ASSOCIATE User Information Parameter
      (Normative) <#chapter_D>`__ specifies some user information
      sub-items, and references for the specification of additional
      sub-items. , in turn, references for the specification of
      Service-class-application-information used in some sub-items.

.. _sect_7.1.1.7:

Result
^^^^^^

This parameter shall be provided either by the acceptor of the
A-ASSOCIATE request, by the UL service-provider (ACSE related function),
or by the UL service-provider (Presentation related function). It shall
indicate the result of using the A-ASSOCIATE service. It shall take one
of the following symbolic values:

a. accepted;

b. rejected (permanent);

c. rejected (transient).

.. note::

   The rejected (permanent) implies that the association calling UL user
   (when returning such a result to an association request) does not
   need to "call later." A permanent situation exists that prevents the
   association establishment (e.g., remote DICOM Application Name
   unknown).

.. _sect_7.1.1.8:

Result Source
^^^^^^^^^^^^^

The value of the parameter is supplied by the UL service-provider. It
identifies the creating source of the Result parameter and the
Diagnostic parameter, if present. It shall take one of the following
symbolic values:

a. UL service-user;

b. UL service-provider (ACSE related function);c) UL service-provider
   (Presentation related function).

.. note::

   If the Result parameter has the value "accepted," the value of this
   parameter is "UL service-user."

.. _sect_7.1.1.9:

Diagnostic
^^^^^^^^^^

This parameter shall only be used if the Result parameter has the value
of "rejected (permanent) " or "rejected (transient)." It shall be used
to provide diagnostic information about the result of the A-ASSOCIATE
service.

If the Result Source parameter has the value "UL service-user," it shall
take one of the following symbolic values:

a. no-reason-given

b. application-context-name not supported

c. calling-AE-title not recognized

d. called-AE-title not recognized

e. calling-AE-qualifier not recognized (see note)

f. calling-AP-invocation-identifier not recognized (see note)

g. calling-AE-invocation-identifier not recognized (see note)

h. called-AE-qualifier not recognized (see note)

i. called-AP-invocation-identifier not recognized (see note)

j. called-AE-invocation-identifier not recognized (see note)

If the Result Source parameter has the value "UL service-provider" (ACSE
related function), it shall take one of the following symbolic values:

a. no-reason-given

b. no-common-UL version

If the result source has the value "UL service-provider" (Presentation
related function), it shall take the following symbolic values:

a. no-reason-given

b. temporary-congestion

c. local-limit-exceeded

d. called-(Presentation) -address-unknown

e. Presentation-protocol version not supported

f. no-(Presentation) Service Access Point (SAP) available

.. note::

   Even though some of the above symbolic values correspond to parameter
   errors not used in this Standard, they are included to allow the
   notification of errors resulting from the unauthorized use of these
   parameters.

.. _sect_7.1.1.10:

Calling Presentation Address
^^^^^^^^^^^^^^^^^^^^^^^^^^^^

This parameter shall contain a structured destination address
unambiguous within the global network address structure. This shall be a
TCP/IP Address. See `DICOM Addressing (Normative) <#chapter_C>`__.

.. _sect_7.1.1.11:

Called Presentation Address
^^^^^^^^^^^^^^^^^^^^^^^^^^^

This parameter shall contain a structured destination address
unambiguous within the global network address structure. This shall be a
TCP/IP Address. See `DICOM Addressing (Normative) <#chapter_C>`__.

.. _sect_7.1.1.12:

Responding Presentation Address
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

In this Standard, a responding presentation address shall always contain
the same value as the called Presentation Address of the A-ASSOCIATE
indication. This parameter shall contain a structured destination
address unambiguous within the global network address structure.

.. _sect_7.1.1.13:

Presentation Context Definition List
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

This parameter used in an A-ASSOCIATE request or indication shall
consist of a list containing one or more presentation contexts. Each
item shall contain three components, a presentation context
identification, an Abstract Syntax Name, and a list of one or more
Transfer Syntax Names.

The presentation context identification components of this parameter
exist to distinguish presentation contexts in communication. Such an
identification of presentation context(s) applies only within the
context of a given association (i.e., different presentation contexts
may be identified by the same presentation context identification on
different associations). It is the association-requestor's
responsibility to assign an arbitrary, but unused identifier for each
proposed presentation context on a given association. There is no
restriction on the ordering of the presentation contexts in relation to
their identifiers.

.. note::

   A separate presentation context will be associated with each Abstract
   Syntax Name in each of the elements of the Presentation Context
   Definition List parameter. If the same Abstract Syntax Name occurs
   more than once, a separate and distinctly identified presentation
   context will be generated for each occurrence (as only one Transfer
   Syntax per presentation context can be accepted).

Abstract Syntaxes defined by this Standard and used by DICOM Application
Entites are defined in . Transfer Syntaxes defined by this Standard and
used by DICOM Application Entities are defined in . Further discussion
on Abstract Syntaxes and Transfer Syntaxes can be found in `Abstract and
Transfer Syntaxes (Informative) <#chapter_B>`__.

.. _sect_7.1.1.14:

Presentation Context Definition Result List
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

This parameter used in the A-ASSOCIATE Response and Confirmation
indicates the acceptance or rejection of each of the presentation
context definitions proposed in the presentation context definition list
parameter (`Presentation Context Definition List <#sect_7.1.1.13>`__).
The Presentation Context Definition Result List parameter shall take the
form of a list of result values. There is a one to one correspondence
between each one of these result values and each of the presentation
contexts proposed in the Presentation Context Definition List parameter.
Each result value represents either "acceptance," "user-rejection," or
"provider-rejection." The values of the results are assigned by the UL
user on the response service primitive. The result values may be sent in
any order.

.. note::

   The order of the results may be different than the order proposed.
   The order need not be sorted by identifier, and the Initiator may not
   assume or depend upon any particular order.

In this Standard only one Transfer Syntax per presentation context shall
be agreed to, even though more than one choice of Transfer Syntaxes may
have been offered in a specific presentation context of the Presentation
Context Definition list.

.. _sect_7.1.1.15:

Presentation Requirements (Fixed Value)
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

This parameter allows the negotiation of optional presentation
functional units beyond the Presentation Kernel. Only the Kernel
Functional Unit is used by DICOM Application Entities. Therefore, this
parameter shall always specify "Presentation Kernel."

.. _sect_7.1.1.16:

Session Requirements (Fixed Value)
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

This parameter allows the negotiation of optional session Functional
Units beyond the Session Kernel. Only the Kernel functional unit with
the Full Duplex Functional Unit shall be used by DICOM Application
Entities.

.. _sect_7.1.1.17:

Other Parameters
^^^^^^^^^^^^^^^^

A few optional parameters defined in the OSI ACSE (ISO 8649) and OSI
Presentation Service (ISO 8822) Standards are not identified here. They
are not necessary for the communication of DICOM Application Entities
and shall not be used in this Standard.

.. _sect_7.1.2:

A-ASSOCIATE Service Procedure
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

**7.1.2.1** A DICOM Application Entity (which includes the Upper Layer
service-user) that desires to establish an association shall issue an
A-ASSOCIATE request primitive. The called AE is identified by parameters
of the request primitive. The requestor shall not issue any primitives
except an A-ABORT request primitive until it receives an A-ASSOCIATE
confirmation primitive.

**7.1.2.2** The Upper Layer (UL) service-provider shall issue an
A-ASSOCIATE indication primitive to the called AE.

**7.1.2.3** The called AE shall accept or reject the association by
sending an A-ASSOCIATE response primitive with an appropriate Result
parameter. The Upper layer service-provider shall issue an A-ASSOCIATE
confirmation primitive having the same Result parameter. The Result
Source parameter shall be assigned the symbolic value of "UL
service-user."

**7.1.2.4** If the acceptor accepts the association, the association is
available for use. Both AEs may now use any service provided by the
DICOM application context that is in effect (with the exception of
A-ASSOCIATE).

.. note::

   This implies that once the association has been established, DICOM
   Messages can be exchanged as defined in .

**7.1.2.5** If the called AE rejects the association, the association
shall not be established.

**7.1.2.6** The UL service-provider may not be capable of supporting the
requested association. In this situation, it shall return an A-ASSOCIATE
confirmation primitive to the requestor with an appropriate Result
parameter (rejected). The Result Source parameter shall be appropriately
assigned either the symbolic value of "UL service-provider (ACSE related
function) " or "UL service-provider (Presentation related function)."
The indication primitive shall not be issued. The association shall not
be established.

**7.1.2.7** Either an association-requestor or acceptor may disrupt the
A-ASSOCIATE service procedure by issuing an A-ABORT request primitive
(see `A-ABORT Service <#sect_7.3>`__). The remote AE receives an A-ABORT
indication primitive. The association shall not be established.

.. _sect_7.2:

A-RELEASE Service
-----------------

The graceful release of an association between two AEs shall be
performed through ACSE A-RELEASE request, indication, response, and
confirmation primitives. The initiator of the service is hereafter
called a requestor and the service-user that receives the A-RELEASE
indication is hereafter called the acceptor. It shall be a confirmed
service.

`figure_title <#figure_7-2>`__ illustrates the graceful release of an
association between two AEs.

.. _sect_7.2.1:

A-RELEASE Parameters
~~~~~~~~~~~~~~~~~~~~

`table_title <#table_7-4>`__ lists the parameters for the A-RELEASE
service that shall contain fixed values or shall not be used by DICOM
Application Entities in this Standard.

.. table:: A-RELEASE Service Parameters

   +-------------+-------------+-------------+-------------+-------------+
   | **A-RELEASE | **Request** | **I         | *           | **Con       |
   | parameter   |             | ndication** | *Response** | firmation** |
   | name**      |             |             |             |             |
   +=============+=============+=============+=============+=============+
   | reason      | UF          | UF(=)       | UF          | UF(=)       |
   +-------------+-------------+-------------+-------------+-------------+
   | user        | NU          | NU(=)       | NU          | NU(=)       |
   | information |             |             |             |             |
   +-------------+-------------+-------------+-------------+-------------+
   | result      |             |             | MF          | MF(=)       |
   +-------------+-------------+-------------+-------------+-------------+

.. _sect_7.2.1.1:

Reason (Fixed)
^^^^^^^^^^^^^^

When used on the request primitive, this parameter identifies the
general level of urgency of the request. This parameter shall always use
the value "normal" in this Standard.

.. _sect_7.2.1.2:

Result (Fixed)
^^^^^^^^^^^^^^

This parameter shall always take the value "affirmative" in this
Standard.

.. _sect_7.2.2:

A-RELEASE Service Procedure
~~~~~~~~~~~~~~~~~~~~~~~~~~~

**7.2.2.1** An UL service-user that desires to release the association
shall issue an A-RELEASE request primitive. This requestor shall not
issue any further primitives other than an A-ABORT request primitive
until it receives an A-RELEASE confirmation primitive.

.. note::

   Even though the requestor of the A-RELEASE service shall not issue
   any further primitive other than A-ABORT, it may receive P-DATA
   Indication primitives.

**7.2.2.2** The UL service-provider shall issue an A-RELEASE indication
primitive to the acceptor. The acceptor then shall not issue any UL
primitives other than an A-RELEASE response primitive, an A-ABORT
request primitive, or P-DATA Request primitive.

**7.2.2.3** To complete the A-RELEASE service, the acceptor shall reply
to the A-RELEASE indication primitive by issuing an A-RELEASE response
primitive. An accepting DICOM Application Entity shall always issue an
A-RELEASE response primitive with an "affirmative" result parameter
(i.e., accept the release).

**7.2.2.4** After an A-RELEASE response has been issued, the acceptor
shall not issue any further primitives for the association thereafter,
including P-DATA Requests.

**7.2.2.5** The UL service-provider shall issue an A-RELEASE
confirmation primitive always with an "affirmative" value for the Result
parameter.

**7.2.2.6** A requestor in either AE may disrupt the A-RELEASE service
procedure by issuing an A-ABORT request. When the acceptor receives an
A-ABORT indication, the association is released with the possible loss
of information in transit.

**7.2.2.7** An A-RELEASE service procedure collision results when
requestors in both AEs simultaneously issue an A-RELEASE service
primitive. In this situation, both UL service-users receive an
unexpected A-RELEASE indication primitive. The following sequence shall
occur to complete the normal release of the association:

a. The association-requestor shall issue an A-RELEASE response
   primitive.

b. The association-acceptor waits for an A-RELEASE confirmation
   primitive from its peer. When it receives one, it shall then issue an
   A-RELEASE response primitive.

c. The association-requestor receives an A-RELEASE confirmation
   primitive.

The association shall be released when both ACSE service-users have
received an A-RELEASE confirmation primitive.

.. _sect_7.3:

A-ABORT Service
---------------

The ACSE A-ABORT service shall be used by a requestor in either of the
AEs to cause the abnormal release of the association. It shall be a
non-confirmed service. However, because of the possibility of an A-ABORT
service procedure collision, the delivery of the indication primitive is
not guaranteed. Should such a collision occur, both AEs are aware that
the association has been terminated. The abort shall be performed
through A-ABORT request and A-ABORT indication primitives.

.. note::

   An A-ABORT request primitive used on an established association may
   result in the destruction of data in transit.

`figure_title <#figure_7-3>`__ illustrates aborting an established
association between two AE's.

.. _sect_7.3.1:

A-ABORT Parameters
~~~~~~~~~~~~~~~~~~

`table_title <#table_7-5>`__ lists the parameters for the A-ABORT
service. Only the first parameter shall be used by DICOM Application
Entities in this Standard.

.. table:: A-ABORT Service Parameters

   ========================== =========== ==============
   **A-ABORT Parameter Name** **Request** **Indication**
   ========================== =========== ==============
   abort source                           M
   user information           NU          NU(=)
   ========================== =========== ==============

.. _sect_7.3.1.1:

Abort Source
^^^^^^^^^^^^

This parameter indicates the initiating source of this abort. It shall
take one of the following symbolic values:

a. UL service-user

b. UL service-provider (ACSE related)

.. _sect_7.3.2:

A-ABORT Service Procedure
~~~~~~~~~~~~~~~~~~~~~~~~~

**7.3.2.1** When the A-ABORT service is used, the association shall be
released abnormally and simultaneous with the abnormal release of the
underlying connection.

**7.3.2.2** A UL service-user that desires to release the association
abnormally shall issue the A-ABORT request primitive. This requestor
shall not issue any further primitives for the association.

**7.3.2.3** The UL service-provider shall issue an A-ABORT indication
primitive to the acceptor. The UL service-provider shall assign the
value of "UL service-user" for the Abort Source parameter. The
association and the underlying connection have been released.

**7.3.2.4** The UL service-provider (ACSE related functions) may itself
cause the abnormal release of the association because of internal
errors. In this case, the UL service-provider shall issue A-ABORT
indication primitives to acceptors in both AEs. The UL service-provider
shall assign the value of "UL service-provider" to the Abort Source
parameter. The user information parameter shall not be used.

.. _sect_7.4:

A-P-ABORT Service
-----------------

The ACSE A-P-ABORT service shall be used by the UL service-provider to
signal the abnormal release of the association due to problems in
services at the Presentation Layer and below. This occurrence indicates
the possible loss of information in transit. A-P-ABORT is a
provider-initiated service.

`figure_title <#figure_7-4>`__ illustrates aborting an established
association by an UL service-provider.

.. _sect_7.4.1:

A-P-ABORT Parameter
~~~~~~~~~~~~~~~~~~~

`table_title <#table_7-6>`__ lists the parameter that shall be required
for the A-P-ABORT service.

.. table:: A-P-ABORT Service Parameters

   ======================== ==========
   A-P-ABORT Parameter Name Indication
   ======================== ==========
   provider reason          P
   ======================== ==========

The provider reason parameter shall be used to convey one of the
following reasons:

a. reason-not-specified

b. unrecognized-pdu

c. unexpected-pdu

d. unexpected-session-service primitive

e. unrecognized-pdu parameter

f. unexpected-pdu parameter

g. invalid-pdu-parameter value

.. note::

   In addition to these reasons, a locally defined list of reasons may
   be used to reflect errors that caused the abort and originated in the
   Session, Transport, Network, Data Link, and Physical layers. The
   generation and handling of such errors is internal to an
   implementation and, therefore, is outside the scope of this
   communications Standard.

.. _sect_7.4.2:

A-P-ABORT Service Procedure
~~~~~~~~~~~~~~~~~~~~~~~~~~~

When the UL service-provider detects an internal error, A-P-ABORT
indication primitives shall be issued to acceptors in both AEs. The
association shall be abnormally released. Requestors in both AEs shall
not issue any further primitives for the association.

.. _sect_7.5:

Sequencing Information
----------------------

Interactions among the specific service procedures, discussed in
`A-ASSOCIATE Service <#sect_7.1>`__, `A-RELEASE Service <#sect_7.2>`__,
`A-ABORT Service <#sect_7.3>`__ and `A-P-ABORT Service <#sect_7.4>`__
for the ACSE subset of the Upper Layer Service, are defined in clause 10
of ISO 8649 - The ACSE Service Definition.

.. _sect_7.6:

P-DATA Service
--------------

This Presentation P-DATA Service shall be used by either AE to cause the
exchange of application information (i.e., DICOM Messages). DICOM
Messages shall be exchanged as defined in . An association provides a
simultaneous bi-directional exchange of P-DATA request/indication
primitives.

`figure_title <#figure_7-5>`__ illustrates the transfer of data on an
established association between two AEs.

.. _sect_7.6.1:

P-DATA Parameters
~~~~~~~~~~~~~~~~~

`table_title <#table_7-7>`__ lists the parameter that shall be required
for the P-DATA service.

.. table:: P-DATA Service Parameter

   ============================ =========== ==============
   **P-DATA Parameter Name**    **Request** **Indication**
   ============================ =========== ==============
   presentation data value list M           M(=)
   ============================ =========== ==============

The Presentation Data Value List parameter shall contain one or more
Presentation Data Values (PDV). Each PDV shall consist of two
parameters: a Presentation Context ID and User Data values. The User
Data values are taken from the Abstract Syntax and encoded in the
Transfer Syntax identified by the Presentation Context ID. This
referenced Presentation Context ID identifies one of the presentation
contexts agreed to at association time. The User Data values format used
in each PDV by the DICOM Application Entities is specified in `Usage of
the P-DATA Service By the DICOM Application Entity
(Normative) <#chapter_E>`__.

