.. _chapter_9:

DICOM Upper Layer Protocol for TCP/IP
=====================================

The DICOM Upper Layer Protocol specified in this section shall be used
in conjunction with the TCP/IP transport layers..

.. _sect_9.1:

Use of the Transport Service Provided By TCP
--------------------------------------------

.. _sect_9.1.1:

General
~~~~~~~

There is a one-to-one relationship between a TCP Transport Connection
and an Upper Layer Association. Therefore, the following rules apply:

a. Each Upper Layer Association shall be supported by one and only one
   TCP Transport Connection.

b. Each TCP Transport Connection shall support one and only one Upper
   Layer Association.

The Services provided by the TCP Transport Services are not formally
documented. This section, therefore, makes use of "commonly" used terms
in a number of TCP Programming Interface Implementations (e.g.,
Sockets). However, the following RFCs shall be required for TCP/IP
support. They specify the support needed for IPv4.

a. RFC793, Transmission Control Program - DARPA Internet Protocol
   Specification

b. RFC791, Internet Protocol - DARPA Internet Protocol Specification

c. RFC792, Internet Control Message Protocol - DARPA Internet Program
   Protocol Specification

d. RFC950, Internet Subnetting

In addition, devices that support IPv6 shall comply with:

a. RFC1881, IPv6 Address Allocation Management

b. RFC2460, Internet Protocol, Version 6 (IPv6) Specification

.. note::

   There are many other RFC's that may also apply to a particular
   implementation depending upon specific selections of hardware and
   software features.

For the establishment of a TCP connection, a TCP port shall be used to
serve as the transport selector. A DICOM UL entity is identified on a
given system on the network by a port number unique within the scope of
this system. Port numbers of remote DICOM UL entities (well known port
number or other numbers) shall be configurable on DICOM UL entities.

.. note::

   It is strongly recommended that systems supporting a single DICOM UL
   entity use as their port the "well known port" registered for the
   DICOM Upper Layer Protocol: port number 104 (decimal), if the
   operating system permits access to privileged ports (in the range 0
   to 1023), otherwise it is recommended that they use the "registered"
   port number 11112 (decimal). See
   "http://www.iana.org/assignments/port-numbers".

Application Entities may also choose to access the TCP Transport
Services via a Secure Transport Connection. The nature of this Secure
Transport Connection is specified through Security Profiles (see ).
Security Profiles select minimum mechanisms needed to support that
profile. Other mechanisms may also be used if agreed to during
establishment of the Secure Transport Connection.

.. note::

   1. DICOM does not specify how a secure transport connection is
      established, or the significance of any certificates exchanged
      during peer entity authentication. These issues are left up to the
      application, which is assumed to be following some security
      policy. Once the application has established a secure Transport
      Connection, then an Upper Layer Association can use that secure
      channel.

   2. There may be an interaction between PDU size and record size of
      the secure Transport Connection that impacts efficiency of
      transport.

   3. Registered ports for Secure Transport Connections are defined in .

.. _sect_9.1.2:

Opening a TCP Transport Connection
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

When an Association is to be established by a DICOM Upper Layer Entity,
a TRANSPORT CONNECT request primitive shall be issued to the TCP
Transport Service (Active Open). Once the TCP Transport Connection
Confirmation is received (Open Completed), an A-ASSOCIATE-RQ PDU shall
be sent/written on the now established transport connection.

When a DICOM Upper Layer Entity becomes activated (Association Idle
State), it shall wait for TCP Transport Connections in a passive mode by
initiating a "listen." When an incoming TCP Transport Connection
Indication is received from the network, it is accepted and a timer
ARTIM (Association Request/Reject/Release Timer) shall be set. Any
further exchange of PDUs (read/write) shall be performed as specified by
the Upper Layer State Machine (including ARTIM Timer expiration before
an A-ASSOCIATE-RQ PDU is received, see `DICOM Upper Layer Protocol for
TCP/IP State Machine <#sect_9.2>`__).

.. _sect_9.1.3:

Transferring Data On a TCP Connection
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

Data exchange of PDUs (read/write) on an established TCP Connection
shall follow the specifications of the DICOM Upper Layer Protocol State
Machine (see `DICOM Upper Layer Protocol for TCP/IP State
Machine <#sect_9.2>`__) and the DICOM Upper Layer PDU structure (see
`DICOM Upper Layer Protocol for TCP/IP Data Units
Structure <#sect_9.3>`__).

.. _sect_9.1.4:

Closing a TCP Transport Connection
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

TCP Transport Connections shall be closed using the "don't linger"
option.

A TCP Transport Connection is closed under a number of situations. These
are described in the DICOM Upper Layer Protocol State Machine. Some
typical cases are discussed below:

a. After an A-RELEASE-RQ has been sent and the A-RELEASE-RP PDU is
   received

b. When a Transport Connection has been established by the DICOM remote
   UL Entity and no A-ASSOCIATE-RQ is received before the ARTIM Timer
   expires

c. When an A-ABORT PDU has been received

d. When an A-ABORT PDU has been sent and the ARTIM Timer expires before
   the Transport Connection is closed

e. When a TCP connection is being disconnected by the Transport Service
   Provider (e.g., network failure)

f. When a TCP connection is being disconnected by the remote DICOM UL
   Entity

.. note::

   1. Except following the normal completion of an association reject,
      release or abort and in specific situations such as temporary lack
      of resources, an Upper Layer State Machine should not disconnect a
      TCP connection or reject its establishment. The appropriate
      behavior is to use the Association Reject or Abort services.

   2. The ARTIM Timer should not be used to oversee the Association
      Establishment or Release. Such a mechanism falls under the
      protocol definition of the layer above the DICOM Upper Layer
      (i.e., DICOM Application Entity, see ).

.. _sect_9.1.5:

ARTIM Timer
~~~~~~~~~~~

The value of the ARTIM Timer used to manage the Request, Reject, and
Release of associations on a DICOM UL entity shall be configurable to
address a wide range of network configurations.

.. _sect_9.2:

DICOM Upper Layer Protocol for TCP/IP State Machine
---------------------------------------------------

.. _sect_9.2.1:

Machine States Definition
~~~~~~~~~~~~~~~~~~~~~~~~~

.. table:: No Association

   ========= ==============
   **State** **Definition**
   ========= ==============
   Sta 1     Idle
   ========= ==============

.. table:: Association Establishment

   +-----------+---------------------------------------------------------+
   | **State** | **Definition**                                          |
   +===========+=========================================================+
   | Sta 2     | Transport connection open (Awaiting A-ASSOCIATE-RQ PDU) |
   +-----------+---------------------------------------------------------+
   | Sta 3     | Awaiting local A-ASSOCIATE response primitive (from     |
   |           | local user)                                             |
   +-----------+---------------------------------------------------------+
   | Sta 4     | Awaiting transport connection opening to complete (from |
   |           | local transport service)                                |
   +-----------+---------------------------------------------------------+
   | Sta 5     | Awaiting A-ASSOCIATE-AC or A-ASSOCIATE-RJ PDU           |
   +-----------+---------------------------------------------------------+

.. table:: Data Transfer

   ========= ===================================================
   **State** **Definition**
   ========= ===================================================
   Sta 6     Association established and ready for data transfer
   ========= ===================================================

.. table:: Association Release

   +-----------+---------------------------------------------------------+
   | **State** | **Definition**                                          |
   +===========+=========================================================+
   | Sta 7     | Awaiting A-RELEASE-RP PDU                               |
   +-----------+---------------------------------------------------------+
   | Sta 8     | Awaiting local A-RELEASE response primitive (from local |
   |           | user)                                                   |
   +-----------+---------------------------------------------------------+
   | Sta 9     | Release collision requestor side; awaiting A-RELEASE    |
   |           | response (from local user)                              |
   +-----------+---------------------------------------------------------+
   | Sta 10    | Release collision acceptor side; awaiting A-RELEASE-RP  |
   |           | PDU                                                     |
   +-----------+---------------------------------------------------------+
   | Sta 11    | Release collision requestor side; awaiting A-RELEASE-RP |
   |           | PDU                                                     |
   +-----------+---------------------------------------------------------+
   | Sta 12    | Release collision acceptor side; awaiting A-RELEASE     |
   |           | response primitive (from local user)                    |
   +-----------+---------------------------------------------------------+

.. table:: Waiting for Transport Connection Close

   +-----------+---------------------------------------------------------+
   | **State** | **Definition**                                          |
   +===========+=========================================================+
   | Sta 13    | Awaiting Transport Connection Close Indication          |
   |           | (Association no longer exists)                          |
   +-----------+---------------------------------------------------------+

.. _sect_9.2.2:

State Machine Actions Definition
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

.. table:: Association Establishment Related Actions

   +------------+--------------------------------------------------------+
   | **Action** | **Definition**                                         |
   +============+========================================================+
   | AE-1       | Issue TRANSPORT CONNECT request primitive to local     |
   |            | transport service                                      |
   |            |                                                        |
   |            | Next state is Sta4                                     |
   +------------+--------------------------------------------------------+
   | AE-2       | Send A-ASSOCIATE-RQ-PDU                                |
   |            |                                                        |
   |            | Next state is Sta5                                     |
   +------------+--------------------------------------------------------+
   | AE-3       | Issue A-ASSOCIATE confirmation (accept) primitive      |
   |            |                                                        |
   |            | Next state is Sta6                                     |
   +------------+--------------------------------------------------------+
   | AE-4       | Issue A-ASSOCIATE confirmation (reject) primitive and  |
   |            | close transport connection                             |
   |            |                                                        |
   |            | Next state is Sta1                                     |
   +------------+--------------------------------------------------------+
   | AE-5       | Issue Transport connection response primitive; start   |
   |            | ARTIM timer                                            |
   |            |                                                        |
   |            | Next state is Sta2                                     |
   +------------+--------------------------------------------------------+
   | AE-6       | Stop ARTIM timer and if A-ASSOCIATE-RQ acceptable by   |
   |            | service-provider:                                      |
   |            |                                                        |
   |            | -  issue A-ASSOCIATE indication primitive              |
   |            |                                                        |
   |            |    Next state is Sta3                                  |
   |            |                                                        |
   |            | otherwise:                                             |
   |            |                                                        |
   |            | -  issue A-ASSOCIATE-RJ-PDU and start ARTIM timer      |
   |            |                                                        |
   |            |    Next state is Sta13                                 |
   +------------+--------------------------------------------------------+
   | AE-7       | Send A-ASSOCIATE-AC PDU                                |
   |            |                                                        |
   |            | Next state is Sta6                                     |
   +------------+--------------------------------------------------------+
   | AE-8       | Send A-ASSOCIATE-RJ PDU and start ARTIM timer          |
   |            |                                                        |
   |            | Next state is STA13                                    |
   +------------+--------------------------------------------------------+

.. table:: Data Transfer Related Actions

   ========= ================================
   **State** **Definition**
   ========= ================================
   DT-1      Send P-DATA-TF PDU
             
             Next state is Sta6
   DT-2      Send P-DATA indication primitive
             
             Next state is Sta6
   ========= ================================

.. table:: Association Release Related Actions

   +------------+--------------------------------------------------------+
   | **Action** | **Definition**                                         |
   +============+========================================================+
   | AR-1       | Send A-RELEASE-RQ PDU                                  |
   |            |                                                        |
   |            | Next state is Sta7                                     |
   +------------+--------------------------------------------------------+
   | AR-2       | Issue A-RELEASE indication primitive                   |
   |            |                                                        |
   |            | Next state is Sta8                                     |
   +------------+--------------------------------------------------------+
   | AR-3       | Issue A-RELEASE confirmation primitive, and close      |
   |            | transport connection                                   |
   |            |                                                        |
   |            | Next state is Sta1                                     |
   +------------+--------------------------------------------------------+
   | AR-4       | Issue A-RELEASE-RP PDU and start ARTIM timer           |
   |            |                                                        |
   |            | Next state is Sta13                                    |
   +------------+--------------------------------------------------------+
   | AR-5       | Stop ARTIM timer                                       |
   |            |                                                        |
   |            | Next state is Sta1                                     |
   +------------+--------------------------------------------------------+
   | AR-6       | Issue P-DATA indication                                |
   |            |                                                        |
   |            | Next state is Sta7                                     |
   +------------+--------------------------------------------------------+
   | AR-7       | Issue P-DATA-TF PDU                                    |
   |            |                                                        |
   |            | Next state is Sta8                                     |
   +------------+--------------------------------------------------------+
   | AR-8       | Issue A-RELEASE indication (release collision):        |
   |            |                                                        |
   |            | -  if association-requestor, next state is Sta9        |
   |            |                                                        |
   |            | -  if not, next state is Sta10                         |
   +------------+--------------------------------------------------------+
   | AR-9       | Send A-RELEASE-RP PDU                                  |
   |            |                                                        |
   |            | Next state is Sta11                                    |
   +------------+--------------------------------------------------------+
   | AR-10      | Issue A-RELEASE confirmation primitive                 |
   |            |                                                        |
   |            | Next state is Sta12                                    |
   +------------+--------------------------------------------------------+

.. table:: Association Abort Related Actions

   +------------+--------------------------------------------------------+
   | **Action** | **Definition**                                         |
   +============+========================================================+
   | AA-1       | Send A-ABORT PDU (service-user source) and start (or   |
   |            | restart if already started) ARTIM timer                |
   |            |                                                        |
   |            | Next state is Sta13                                    |
   +------------+--------------------------------------------------------+
   | AA-2       | Stop ARTIM timer if running. Close transport           |
   |            | connection                                             |
   |            |                                                        |
   |            | Next state is Sta1                                     |
   +------------+--------------------------------------------------------+
   | AA-3       | If (service-user inititated abort):                    |
   |            |                                                        |
   |            | -  issue A-ABORT indication and close transport        |
   |            |    connection                                          |
   |            |                                                        |
   |            | otherwise (service-provider inititated abort):         |
   |            |                                                        |
   |            | -  issue A-P-ABORT indication and close transport      |
   |            |    connection                                          |
   |            |                                                        |
   |            | Next state is Sta1                                     |
   +------------+--------------------------------------------------------+
   | AA-4       | Issue A-P-ABORT indication primitive                   |
   |            |                                                        |
   |            | Next state is Sta1                                     |
   +------------+--------------------------------------------------------+
   | AA-5       | Stop ARTIM timer                                       |
   |            |                                                        |
   |            | Next state is Sta1                                     |
   +------------+--------------------------------------------------------+
   | AA-6       | Ignore PDU                                             |
   |            |                                                        |
   |            | Next state is Sta13                                    |
   +------------+--------------------------------------------------------+
   | AA-7       | Send A-ABORT PDU                                       |
   |            |                                                        |
   |            | Next state is Sta13                                    |
   +------------+--------------------------------------------------------+
   | AA-8       | Send A-ABORT PDU (service-provider source-), issue an  |
   |            | A-P-ABORT indication, and start ARTIM timer            |
   |            |                                                        |
   |            | Next state is Sta13                                    |
   +------------+--------------------------------------------------------+

.. _sect_9.2.3:

DICOM Upper Layer Protocol for TCP/IP State Transition Table
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

The DICOM Upper Layer Protocol State transitions are specified in
`table_title <#table_9-10>`__. This table addresses both the normal and
error cases for the protocol operation. Both the called and the calling
aspects of an association are described in this table.

.. table:: DICOM Upper Layer Protocol State Transition Table

   +-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+
   | S     | No    | **A   | *     | **A   | *     |       |       |       |       |       |       |       |       |
   | TATES | assoc | ssoci | *Data | ssoci | *Wait |       |       |       |       |       |       |       |       |
   |       | \ :su | ation | trans | ation | for   |       |       |       |       |       |       |       |       |
   |       | p:`n` | estab | fer** | re    | Tp    |       |       |       |       |       |       |       |       |
   |       |       | lishm |       | lease | Cl    |       |       |       |       |       |       |       |       |
   |       |       | ent** |       | (n    | ose** |       |       |       |       |       |       |       |       |
   |       |       |       |       | ormal |       |       |       |       |       |       |       |       |       |
   |       |       |       |       | &     |       |       |       |       |       |       |       |       |       |
   |       |       |       |       | co    |       |       |       |       |       |       |       |       |       |
   |       |       |       |       | llisi |       |       |       |       |       |       |       |       |       |
   |       |       |       |       | on)** |       |       |       |       |       |       |       |       |       |
   +=======+=======+=======+=======+=======+=======+=======+=======+=======+=======+=======+=======+=======+=======+
   | A     | AE-1  |       |       |       |       |       |       |       |       |       |       |       |       |
   | -ASSO |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | CIATE | Sta4  |       |       |       |       |       |       |       |       |       |       |       |       |
   | Re    |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | quest |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | (     |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | local |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | user) |       |       |       |       |       |       |       |       |       |       |       |       |       |
   +-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+
   | Tran  |       |       |       | AE-2  |       |       |       |       |       |       |       |       |       |
   | sport |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | Conn. |       |       |       | Sta5  |       |       |       |       |       |       |       |       |       |
   | Co    |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | nfirm |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | \ :su |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | p:`n` |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | (     |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | local |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | tran  |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | sport |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | ser   |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | vice) |       |       |       |       |       |       |       |       |       |       |       |       |       |
   +-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+
   | A-AS  |       | AA-1  | AA-8  |       | AE-3  | AA-8  | AA-8  | AA-8  | AA-8  | AA-8  | AA-8  | AA-8  | AA-6  |
   | SOCIA |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | TE-AC |       | Sta13 | Sta13 |       | Sta6  | Sta13 | Sta13 | Sta13 | Sta13 | Sta13 | Sta13 | Sta13 | Sta13 |
   | PDU   |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | (rec  |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | eived |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | on    |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | tran  |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | sport |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | c     |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | onnec |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | tion) |       |       |       |       |       |       |       |       |       |       |       |       |       |
   +-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+
   | A-AS  |       | AA-1  | AA-8  |       | AE-4  | AA-8  | AA-8  | AA-8  | AA-8  | AA-8  | AA-8  | AA-8  | AA-6  |
   | SOCIA |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | TE-RJ |       | Sta13 | Sta13 |       | Sta1  | Sta13 | Sta13 | Sta13 | Sta13 | Sta13 | Sta13 | Sta13 | Sta13 |
   | PDU   |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | (rec  |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | eived |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | on    |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | tran  |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | sport |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | c     |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | onnec |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | tion) |       |       |       |       |       |       |       |       |       |       |       |       |       |
   +-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+
   | Tran  | AE-5  |       |       |       |       |       |       |       |       |       |       |       |       |
   | sport |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | Conne | Sta2  |       |       |       |       |       |       |       |       |       |       |       |       |
   | ction |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | Indic |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | ation |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | (     |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | local |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | tran  |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | sport |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | ser   |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | vice) |       |       |       |       |       |       |       |       |       |       |       |       |       |
   +-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+
   | A-AS  |       | AE-6  | AA-8  |       | AA-8  | AA-8  | AA-8  | AA-8  | AA-8  | AA-8  | AA-8  | AA-8  | AA-7  |
   | SOCIA |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | TE-RQ |       | Sta3  | Sta13 |       | Sta13 | Sta13 | Sta13 | Sta13 | Sta13 | Sta13 | Sta13 | Sta13 | Sta13 |
   | PDU   |       | or 13 |       |       |       |       |       |       |       |       |       |       |       |
   | (rec  |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | eived |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | on    |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | tran  |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | sport |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | c     |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | onnec |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | tion) |       |       |       |       |       |       |       |       |       |       |       |       |       |
   +-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+
   | A     |       |       | AE-7  |       |       |       |       |       |       |       |       |       |       |
   | -ASSO |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | CIATE |       |       | Sta6  |       |       |       |       |       |       |       |       |       |       |
   | res   |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | ponse |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | prim  |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | itive |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | (ac   |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | cept) |       |       |       |       |       |       |       |       |       |       |       |       |       |
   +-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+
   | A     |       |       | AE-8  |       |       |       |       |       |       |       |       |       |       |
   | -ASSO |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | CIATE |       |       | Sta13 |       |       |       |       |       |       |       |       |       |       |
   | res   |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | ponse |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | prim  |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | itive |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | (re   |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | ject) |       |       |       |       |       |       |       |       |       |       |       |       |       |
   +-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+
   | P     |       |       |       |       |       | DT-1  |       | AR-7  |       |       |       |       |       |
   | -DATA |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | re    |       |       |       |       |       | Sta6  |       | Sta8  |       |       |       |       |       |
   | quest |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | prim  |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | itive |       |       |       |       |       |       |       |       |       |       |       |       |       |
   +-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+
   | P-DA  |       | AA-1  | AA-8  |       | AA-8  | DT-2  | AR-6  | AA-8  | AA-8  | AA-8  | AA-8  | AA-8  | AA-6  |
   | TA-TF |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | PDU   |       | Sta13 | Sta13 |       | Sta13 | Sta6  | Sta7  | Sta13 | Sta13 | Sta13 | Sta13 | Sta13 | Sta13 |
   +-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+
   | A-RE  |       |       |       |       |       | AR-1  |       |       |       |       |       |       |       |
   | LEASE |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | Re    |       |       |       |       |       | Sta7  |       |       |       |       |       |       |       |
   | quest |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | prim  |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | itive |       |       |       |       |       |       |       |       |       |       |       |       |       |
   +-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+
   | A-    |       | AA-1  | AA-8  |       | AA-8  | AR-2  | AR-8  | AA-8  | AA-8  | AA-8  | AA-8  | AA-8  | AA-6  |
   | RELEA |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | SE-RQ |       | Sta13 | Sta13 |       | Sta13 | Sta8  | Sta9  | Sta13 | Sta13 | Sta13 | Sta13 | Sta13 | Sta13 |
   | PDU   |       |       |       |       |       |       | or 10 |       |       |       |       |       |       |
   | (rec  |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | eived |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | on    |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | open  |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | tran  |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | sport |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | c     |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | onnec |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | tion) |       |       |       |       |       |       |       |       |       |       |       |       |       |
   +-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+
   | A-    |       | AA-1  | AA-8  |       | AA-8  | AA-8  | AR-3  | AA-8  | AA-8  | AR-10 | AR-3  | AA-8  | AA-6  |
   | RELEA |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | SE-RP |       | Sta13 | Sta13 |       | Sta13 | Sta13 | Sta1  | Sta13 | Sta13 | Sta12 | Sta1  | Sta13 | Sta13 |
   | PDU   |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | (rec  |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | eived |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | on    |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | tran  |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | sport |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | c     |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | onnec |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | tion) |       |       |       |       |       |       |       |       |       |       |       |       |       |
   +-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+
   | A-RE  |       |       |       |       |       |       |       | AR-4  | AR-9  |       |       | AR-4  |       |
   | LEASE |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | Res   |       |       |       |       |       |       |       | Sta13 | Sta11 |       |       | Sta13 |       |
   | ponse |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | prim  |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | itive |       |       |       |       |       |       |       |       |       |       |       |       |       |
   +-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+
   | A-    |       |       | AA-1  | AA-2  | AA-1  | AA-1  | AA-1  | AA-1  | AA-1  | AA-1  | AA-1  | AA-1  |       |
   | ABORT |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | Re    |       |       | Sta13 | Sta1  | Sta13 | Sta13 | Sta13 | Sta13 | Sta13 | Sta13 | Sta13 | Sta13 |       |
   | quest |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | prim  |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | itive |       |       |       |       |       |       |       |       |       |       |       |       |       |
   +-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+
   | A-    |       | AA-2  | AA-3  |       | AA-3  | AA-3  | AA-3  | AA-3  | AA-3  | AA-3  | AA-3  | AA-3  | AA-2  |
   | ABORT |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | PDU   |       | Sta1  | Sta1  |       | Sta1  | Sta1  | Sta1  | Sta1  | Sta1  | Sta1  | Sta1  | Sta1  | Sta1  |
   | (rec  |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | eived |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | on    |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | open  |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | tran  |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | sport |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | c     |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | onnec |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | tion) |       |       |       |       |       |       |       |       |       |       |       |       |       |
   +-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+
   | Tran  |       | AA-5  | AA-4  | AA-4  | AA-4  | AA-4  | AA-4  | AA-4  | AA-4  | AA-4  | AA-4  | AA-4  | AR-5  |
   | sport |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | conne |       | Sta1  | Sta1  | Sta1  | Sta1  | Sta1  | Sta1  | Sta1  | Sta1  | Sta1  | Sta1  | Sta1  | Sta1  |
   | ction |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | c     |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | losed |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | indic |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | ation |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | (     |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | local |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | tran  |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | sport |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | ser   |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | vice) |       |       |       |       |       |       |       |       |       |       |       |       |       |
   +-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+
   | ARTIM |       | AA-2  |       |       |       |       |       |       |       |       |       |       | AA-2  |
   | timer |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | ex    |       | Sta1  |       |       |       |       |       |       |       |       |       |       | Sta1  |
   | pired |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | (A    |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | ssoci |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | ation |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | reje  |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | ct/re |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | lease |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | t     |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | imer) |       |       |       |       |       |       |       |       |       |       |       |       |       |
   +-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+
   | Un    |       | AA-1  | AA-8  |       | AA-8  | AA-8  | AA-8  | AA-8  | AA-8  | AA-8  | AA-8  | AA-8  | AA-7  |
   | recog |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | nized |       | Sta13 | Sta13 |       | Sta13 | Sta13 | Sta13 | Sta13 | Sta13 | Sta13 | Sta13 | Sta13 | Sta13 |
   | or    |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | in    |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | valid |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | PDU   |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | rec   |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | eived |       |       |       |       |       |       |       |       |       |       |       |       |       |
   +-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+

.. _sect_9.3:

DICOM Upper Layer Protocol for TCP/IP Data Units Structure
----------------------------------------------------------

.. _sect_9.3.1:

General
~~~~~~~

The Protocol Data Units (PDUs) are the message formats exchanged between
peer entities within a layer. A PDU shall consist of protocol control
information and user data. PDUs are constructed by mandatory fixed
fields followed by optional variable fields that contain one or more
items and/or sub-items.

Items of unrecognized types shall be ignored and skipped. Items shall
appear in an increasing order of their item types. Several instances of
the same item shall be acceptable or shall not as specified by each
item.

The DICOM UL protocol consists of seven Protocol Data Units:

a. A-ASSOCIATE-RQ PDU

b. A-ASSOCIATE-AC PDU

c. A-ASSOCIATE-RJ PDU

d. P-DATA-TF PDU

e. A-RELEASE-RQ PDU

f. A-RELEASE-RP PDU

g. A-ABORT PDU

The encoding of the DICOM UL PDUs is defined as follows (Big Endian byte
ordering) :

.. note::

   The Big Endian byte ordering has been chosen for consistency with the
   OSI and TCP/IP environment. This pertains to the DICOM UL PDU headers
   only. The encoding of the PDV message fragments is defined by the
   Transfer Syntax negotiated at association establishment.

a. Each PDU type shall consist of one or more bytes that when
   represented, are numbered sequentially, with byte 1 being the lowest
   byte number.

b. Each byte within the PDU shall consist of eight bits that, when
   represented, are numbered 7 to 0, where bit 0 is the low order bit.

c. When consecutive bytes are used to represent a string of characters,
   the lowest byte numbers represent the first character.

d. When consecutive bytes are used to represent a binary number, the
   lower byte number has the most significant value.

e. The lowest byte number is placed first in the transport service data
   flow.

f. An overview of the PDUs is shown in `figure_title <#figure_9-1>`__
   and `figure_title <#figure_9-2>`__. The detailed structure of each
   PDU is specified in the following sections.

.. note::

   A number of parameters defined in the UL Service are not reflected in
   these PDUs (e.g., service parameters, fixed values, values not used
   by DICOM Application Entities.)

.. _sect_9.3.2:

A-ASSOCIATE-RQ PDU Structure
~~~~~~~~~~~~~~~~~~~~~~~~~~~~

An A-ASSOCIATE-RQ PDU shall be made of a sequence of mandatory fields
followed by a variable length field. `table_title <#table_9-11>`__ shows
the sequence of the mandatory fields.

The variable field shall consist of one Application Context Item, one or
more Presentation Context Items, and one User Information Item.
Sub-Items shall exist for the Presentation Context and User Information
Items.

.. table:: ASSOCIATE-RQ PDU Fields

   +---------------+------------------+---------------------------------+
   | **PDU bytes** | **Field name**   | **Description of field**        |
   +===============+==================+=================================+
   | 1             | PDU-type         | 01H                             |
   +---------------+------------------+---------------------------------+
   | 2             | Reserved         | This reserved field shall be    |
   |               |                  | sent with a value 00H but not   |
   |               |                  | tested to this value when       |
   |               |                  | received.                       |
   +---------------+------------------+---------------------------------+
   | 3-6           | PDU-length       | This PDU-length shall be the    |
   |               |                  | number of bytes from the first  |
   |               |                  | byte of the following field to  |
   |               |                  | the last byte of the variable   |
   |               |                  | field. It shall be encoded as   |
   |               |                  | an unsigned binary number       |
   +---------------+------------------+---------------------------------+
   | 7-8           | Protocol-version | This two byte field shall use   |
   |               |                  | one bit to identify each        |
   |               |                  | version of the DICOM UL         |
   |               |                  | protocol supported by the       |
   |               |                  | calling end-system. This is     |
   |               |                  | Version 1 and shall be          |
   |               |                  | identified with bit 0 set. A    |
   |               |                  | receiver of this PDU            |
   |               |                  | implementing only this version  |
   |               |                  | of the DICOM UL protocol shall  |
   |               |                  | only test that bit 0 is set.    |
   +---------------+------------------+---------------------------------+
   | 9-10          | Reserved         | This reserved field shall be    |
   |               |                  | sent with a value 0000H but not |
   |               |                  | tested to this value when       |
   |               |                  | received.                       |
   +---------------+------------------+---------------------------------+
   | 11-26         | Called-AE-title  | Destination DICOM Application   |
   |               |                  | Name. It shall be encoded as 16 |
   |               |                  | characters as defined by the    |
   |               |                  | ISO 646:1990-Basic G0 Set with  |
   |               |                  | leading and trailing spaces     |
   |               |                  | (20H) being non-significant.    |
   |               |                  | The value made of 16 spaces     |
   |               |                  | (20H) meaning "no Application   |
   |               |                  | Name specified" shall not be    |
   |               |                  | used. For a complete            |
   |               |                  | description of the use of this  |
   |               |                  | field, see `Called AE           |
   |               |                  | Title <#sect_7.1.1.4>`__.       |
   +---------------+------------------+---------------------------------+
   | 27-42         | Calling-AE-title | Source DICOM Application Name.  |
   |               |                  | It shall be encoded as 16       |
   |               |                  | characters as defined by the    |
   |               |                  | ISO 646:1990-Basic G0 Set with  |
   |               |                  | leading and trailing spaces     |
   |               |                  | (20H) being non-significant.    |
   |               |                  | The value made of 16 spaces     |
   |               |                  | (20H) meaning "no Application   |
   |               |                  | Name specified" shall not be    |
   |               |                  | used. For a complete            |
   |               |                  | description of the use of this  |
   |               |                  | field, see `Calling AE          |
   |               |                  | Title <#sect_7.1.1.3>`__.       |
   +---------------+------------------+---------------------------------+
   | 43-74         | Reserved         | This reserved field shall be    |
   |               |                  | sent with a value 00H for all   |
   |               |                  | bytes but not tested to this    |
   |               |                  | value when received             |
   +---------------+------------------+---------------------------------+
   | 75-xxx        | Variable items   | This variable field shall       |
   |               |                  | contain the following items:    |
   |               |                  | one Application Context Item,   |
   |               |                  | one or more Presentation        |
   |               |                  | Context Items and one User      |
   |               |                  | Information Item. For a         |
   |               |                  | complete description of the use |
   |               |                  | of these items see `Application |
   |               |                  | Context                         |
   |               |                  | Name <#sect_7.1.1.2>`__,        |
   |               |                  | `Presentation Context           |
   |               |                  | Definition                      |
   |               |                  | List <#sect_7.1.1.13>`__, and   |
   |               |                  | `User                           |
   |               |                  | Information <#sect_7.1.1.6>`__. |
   +---------------+------------------+---------------------------------+

.. _sect_9.3.2.1:

Application Context Item Structure
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

An Application Context Item shall be made of a sequence of mandatory
fields followed by a variable length field.
`table_title <#table_9-12>`__ shows the sequence of the mandatory
fields.

.. table:: Application Context Item Fields

   +----------------+-------------------------+-------------------------+
   | **Item bytes** | **Field name**          | **Description of        |
   |                |                         | field**                 |
   +================+=========================+=========================+
   | 1              | Item-type               | 10H                     |
   +----------------+-------------------------+-------------------------+
   | 2              | Reserved                | This reserved field     |
   |                |                         | shall be sent with a    |
   |                |                         | value 00H but not       |
   |                |                         | tested to this value    |
   |                |                         | when received.          |
   +----------------+-------------------------+-------------------------+
   | 3-4            | Item-length             | This Item-length shall  |
   |                |                         | be the number of bytes  |
   |                |                         | from the first byte of  |
   |                |                         | the following field to  |
   |                |                         | the last byte of the    |
   |                |                         | A                       |
   |                |                         | pplication-context-name |
   |                |                         | field. It shall be      |
   |                |                         | encoded as an unsigned  |
   |                |                         | binary number.          |
   +----------------+-------------------------+-------------------------+
   | 5-xxx          | A                       | A valid                 |
   |                | pplication-context-name | A                       |
   |                |                         | pplication-context-name |
   |                |                         | shall be encoded as     |
   |                |                         | defined in `DICOM UL    |
   |                |                         | Encoding Rules for      |
   |                |                         | Application Contexts,   |
   |                |                         | Abstract Syntaxes,      |
   |                |                         | Transfer Syntaxes       |
   |                |                         | (Norm                   |
   |                |                         | ative) <#chapter_F>`__. |
   |                |                         | For a description of    |
   |                |                         | the use of this field   |
   |                |                         | see `Application        |
   |                |                         | Context                 |
   |                |                         | N                       |
   |                |                         | ame <#sect_7.1.1.2>`__. |
   |                |                         | Ap                      |
   |                |                         | plication-context-names |
   |                |                         | are structured as UIDs  |
   |                |                         | as defined in (see      |
   |                |                         | `Application Context    |
   |                |                         | Names                   |
   |                |                         | (Infor                  |
   |                |                         | mative) <#chapter_A>`__ |
   |                |                         | for an overview of this |
   |                |                         | concept). DICOM         |
   |                |                         | Ap                      |
   |                |                         | plication-context-names |
   |                |                         | are registered in .     |
   +----------------+-------------------------+-------------------------+

.. _sect_9.3.2.2:

Presentation Context Item Structure
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

The Presentation Context Item shall be made of a sequence of mandatory
fixed length fields followed by a variable field.
`table_title <#table_9-13>`__ shows the sequence of the mandatory
fields.

The variable field shall consist of one Abstract Syntax Sub-Item
followed by one or more Transfer Syntax Sub-Items.

.. table:: Presentation Context Item Fields

   +----------------+-------------------------+-------------------------+
   | **Item bytes** | **Field name**          | **Description of        |
   |                |                         | field**                 |
   +================+=========================+=========================+
   | 1              | Item-type               | 20H                     |
   +----------------+-------------------------+-------------------------+
   | 2              | Reserved                | This reserved field     |
   |                |                         | shall be sent with a    |
   |                |                         | value 00H but not       |
   |                |                         | tested to this value    |
   |                |                         | when received.          |
   +----------------+-------------------------+-------------------------+
   | 3-4            | Item-length             | This Item-length shall  |
   |                |                         | be the number of bytes  |
   |                |                         | from the first byte of  |
   |                |                         | the following field to  |
   |                |                         | the last byte of the    |
   |                |                         | last Transfer Syntax    |
   |                |                         | Item. It shall be       |
   |                |                         | encoded as an unsigned  |
   |                |                         | binary number.          |
   +----------------+-------------------------+-------------------------+
   | 5              | Presentation-context-ID | Presentation-context-ID |
   |                |                         | values shall be odd     |
   |                |                         | integers between 1 and  |
   |                |                         | 255, encoded as an      |
   |                |                         | unsigned binary number. |
   |                |                         | For a complete          |
   |                |                         | description of the use  |
   |                |                         | of this field see       |
   |                |                         | `Presentation Context   |
   |                |                         | Definition              |
   |                |                         | Li                      |
   |                |                         | st <#sect_7.1.1.13>`__. |
   +----------------+-------------------------+-------------------------+
   | 6              | Reserved                | This reserved field     |
   |                |                         | shall be sent with a    |
   |                |                         | value 00H but not       |
   |                |                         | tested to this value    |
   |                |                         | when received.          |
   +----------------+-------------------------+-------------------------+
   | 7              | Reserved                | This reserved field     |
   |                |                         | shall be sent with a    |
   |                |                         | value 00H but not       |
   |                |                         | tested to this value    |
   |                |                         | when received.          |
   +----------------+-------------------------+-------------------------+
   | 8              | Reserved                | This reserved field     |
   |                |                         | shall be sent with a    |
   |                |                         | value 00H but not       |
   |                |                         | tested to this value    |
   |                |                         | when received.          |
   +----------------+-------------------------+-------------------------+
   | 9-xxx          | Abstract/Transfer       | This variable field     |
   |                | Syntax Sub-Items        | shall contain the       |
   |                |                         | following sub-items:    |
   |                |                         | one Abstract Syntax and |
   |                |                         | one or more Transfer    |
   |                |                         | Syntax(es). For a       |
   |                |                         | complete description of |
   |                |                         | the use and encoding of |
   |                |                         | these sub-items see     |
   |                |                         | `Abstract Syntax        |
   |                |                         | Sub-Item                |
   |                |                         | Structu                 |
   |                |                         | re <#sect_9.3.2.2.1>`__ |
   |                |                         | and `Transfer Syntax    |
   |                |                         | Sub-Item                |
   |                |                         | Structur                |
   |                |                         | e <#sect_9.3.2.2.2>`__. |
   +----------------+-------------------------+-------------------------+

.. _sect_9.3.2.2.1:

Abstract Syntax Sub-Item Structure
''''''''''''''''''''''''''''''''''

The Abstract Syntax Sub-Item shall be made of a sequence of mandatory
fixed length fields followed by a variable field.
`table_title <#table_9-14>`__ shows the sequence of the mandatory
fields.

.. table:: Abstract Syntax Sub-Item Fields

   +----------------+----------------------+-------------------------+
   | **Item bytes** | **Field name**       | **Description of        |
   |                |                      | field**                 |
   +================+======================+=========================+
   | 1              | Item-type            | 30H                     |
   +----------------+----------------------+-------------------------+
   | 2              | Reserved             | This reserved field     |
   |                |                      | shall be sent with a    |
   |                |                      | value 00H but not       |
   |                |                      | tested to this value    |
   |                |                      | when received.          |
   +----------------+----------------------+-------------------------+
   | 3-4            | Item-length          | This Item-length shall  |
   |                |                      | be the number of bytes  |
   |                |                      | from the first byte of  |
   |                |                      | the following field to  |
   |                |                      | the last byte of the    |
   |                |                      | Abstract-syntax-name    |
   |                |                      | field. It shall be      |
   |                |                      | encoded as an unsigned  |
   |                |                      | binary number.          |
   +----------------+----------------------+-------------------------+
   | 5-xxx          | Abstract-syntax-name | This variable field     |
   |                |                      | shall contain the       |
   |                |                      | Abstract-syntax-name    |
   |                |                      | related to the proposed |
   |                |                      | presentation context. A |
   |                |                      | valid                   |
   |                |                      | Abstract-syntax-name    |
   |                |                      | shall be encoded as     |
   |                |                      | defined in `DICOM UL    |
   |                |                      | Encoding Rules for      |
   |                |                      | Application Contexts,   |
   |                |                      | Abstract Syntaxes,      |
   |                |                      | Transfer Syntaxes       |
   |                |                      | (Norm                   |
   |                |                      | ative) <#chapter_F>`__. |
   |                |                      | For a description of    |
   |                |                      | the use of this field   |
   |                |                      | see `Presentation       |
   |                |                      | Context Definition      |
   |                |                      | Li                      |
   |                |                      | st <#sect_7.1.1.13>`__. |
   |                |                      | Abstract-syntax-names   |
   |                |                      | are structured as UIDs  |
   |                |                      | as defined in (see      |
   |                |                      | `Abstract and Transfer  |
   |                |                      | Syntaxes                |
   |                |                      | (Infor                  |
   |                |                      | mative) <#chapter_B>`__ |
   |                |                      | for an overview of this |
   |                |                      | concept). DICOM         |
   |                |                      | Abstract-syntax-names   |
   |                |                      | are registered in .     |
   +----------------+----------------------+-------------------------+

.. _sect_9.3.2.2.2:

Transfer Syntax Sub-Item Structure
''''''''''''''''''''''''''''''''''

The Transfer Syntax Sub-Item shall be made of a sequence of mandatory
fixed length fields followed by a variable field.
`table_title <#table_9-15>`__ shows the sequence of the mandatory
fields.

.. table:: Transfer Syntax Sub-Item Fields

   +----------------+-------------------------+-------------------------+
   | **Item bytes** | **Field name**          | **Description of        |
   |                |                         | field**                 |
   +================+=========================+=========================+
   | 1              | Item-type               | 40H                     |
   +----------------+-------------------------+-------------------------+
   | 2              | Reserved                | This reserved field     |
   |                |                         | shall be sent with a    |
   |                |                         | value 00H but not       |
   |                |                         | tested to this value    |
   |                |                         | when received.          |
   +----------------+-------------------------+-------------------------+
   | 3-4            | Item-length             | This Item-length shall  |
   |                |                         | be the number of bytes  |
   |                |                         | from the first byte of  |
   |                |                         | the following field to  |
   |                |                         | the last byte of the    |
   |                |                         | Transfer-syntax-name    |
   |                |                         | field(s). It shall be   |
   |                |                         | encoded as an unsigned  |
   |                |                         | binary numbers          |
   +----------------+-------------------------+-------------------------+
   | 5-xxx          | Transfer-syntax-name(s) | This variable field     |
   |                |                         | shall contain the       |
   |                |                         | Transfer-syntax-name    |
   |                |                         | proposed for this       |
   |                |                         | presentation context. A |
   |                |                         | valid                   |
   |                |                         | Transfer-syntax-name    |
   |                |                         | shall be encoded as     |
   |                |                         | defined in `DICOM UL    |
   |                |                         | Encoding Rules for      |
   |                |                         | Application Contexts,   |
   |                |                         | Abstract Syntaxes,      |
   |                |                         | Transfer Syntaxes       |
   |                |                         | (Norm                   |
   |                |                         | ative) <#chapter_F>`__. |
   |                |                         | For a description of    |
   |                |                         | the use of this field   |
   |                |                         | see `Presentation       |
   |                |                         | Context Definition      |
   |                |                         | Li                      |
   |                |                         | st <#sect_7.1.1.13>`__. |
   |                |                         | Transfer-syntax-names   |
   |                |                         | are structured as UIDs  |
   |                |                         | as defined in (see      |
   |                |                         | `Abstract and Transfer  |
   |                |                         | Syntaxes                |
   |                |                         | (Infor                  |
   |                |                         | mative) <#chapter_B>`__ |
   |                |                         | for an overview of this |
   |                |                         | concept). DICOM         |
   |                |                         | Transfer-syntax-names   |
   |                |                         | are registered in .     |
   +----------------+-------------------------+-------------------------+

.. _sect_9.3.2.3:

User Information Item Structure
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

The User Information Item shall be made of a sequence of mandatory fixed
length fields followed by a variable field.
`table_title <#table_9-16>`__ shows the sequence of the mandatory
fields.

The variable field shall consist of one or more User-Data Sub-Items.

.. note::

   The User-Data Sub-Items may be present in any order within the
   User-Information Item. No significance should be placed on the order
   of User-Data Sub-Items within the User Information Item. Sending
   applications should be aware that some older applications might
   expect Sub-Items to be encoded in ascending order of Item-type within
   the enclosing Item.

.. table:: User Information Item Fields

   +----------------+----------------+----------------------------------+
   | **Item bytes** | **Field name** | **Description of field**         |
   +================+================+==================================+
   | 1              | Item-type      | 50H                              |
   +----------------+----------------+----------------------------------+
   | 2              | Reserved       | This reserved field shall be     |
   |                |                | sent with a value 00H but not    |
   |                |                | tested to this value when        |
   |                |                | received.                        |
   +----------------+----------------+----------------------------------+
   | 3-4            | Item-length    | This Item-length shall be the    |
   |                |                | number of bytes from the first   |
   |                |                | byte of the following field to   |
   |                |                | the last byte of the User-data   |
   |                |                | field(s). It shall be encoded as |
   |                |                | an unsigned binary number.       |
   +----------------+----------------+----------------------------------+
   | 5-xxx          | User-data      | This variable field shall        |
   |                |                | contain User-data sub-items as   |
   |                |                | defined by the DICOM Application |
   |                |                | Entity. The structure and        |
   |                |                | content of these sub-items is    |
   |                |                | defined in `Use and Format of    |
   |                |                | the A-ASSOCIATE User Information |
   |                |                | Parameter                        |
   |                |                | (Normative) <#chapter_D>`__.     |
   +----------------+----------------+----------------------------------+

.. _sect_9.3.3:

A-ASSOCIATE-AC PDU Structure
~~~~~~~~~~~~~~~~~~~~~~~~~~~~

An A-ASSOCIATE-AC PDU shall be made of a sequence of mandatory fields
followed by a variable length field. `table_title <#table_9-17>`__ shows
the sequence of the mandatory fields.

The variable field consist of one Application Context Item, one or more
Presentation Context Items, and one User Information Item. Sub-Items
shall exist for the Presentation Context and User Information Items.

.. table:: ASSOCIATE-AC PDU Fields

   +---------------+------------------+---------------------------------+
   | **PDU bytes** | **Field name**   | **Description of field**        |
   +===============+==================+=================================+
   | 1             | PDU-type         | 02H                             |
   +---------------+------------------+---------------------------------+
   | 2             | Reserved         | This reserved field shall be    |
   |               |                  | sent with a value 00H but not   |
   |               |                  | tested to this value when       |
   |               |                  | received.                       |
   +---------------+------------------+---------------------------------+
   | 3-6           | PDU-length       | This PDU-length shall be the    |
   |               |                  | number of bytes from the first  |
   |               |                  | byte of the following field to  |
   |               |                  | the last byte of the variable   |
   |               |                  | field. It shall be encoded as   |
   |               |                  | an unsigned binary number.      |
   +---------------+------------------+---------------------------------+
   | 7-8           | Protocol-version | This two byte field shall use   |
   |               |                  | one bit to identify each        |
   |               |                  | version of the DICOM UL         |
   |               |                  | protocol supported by the       |
   |               |                  | calling end-system. This is     |
   |               |                  | Version 1 and shall be          |
   |               |                  | identified with bit 0 set. A    |
   |               |                  | receiver of this PDU            |
   |               |                  | implementing only this version  |
   |               |                  | of the DICOM UL protocol shall  |
   |               |                  | only test that bit 0 is set.    |
   +---------------+------------------+---------------------------------+
   | 9-10          | Reserved         | This reserved field shall be    |
   |               |                  | sent with a value 0000H but not |
   |               |                  | tested to this value when       |
   |               |                  | received.                       |
   +---------------+------------------+---------------------------------+
   | 11-26         | Reserved         | This reserved field shall be    |
   |               |                  | sent with a value identical to  |
   |               |                  | the value received in the same  |
   |               |                  | field of the A-ASSOCIATE-RQ     |
   |               |                  | PDU, but its value shall not be |
   |               |                  | tested when received.           |
   +---------------+------------------+---------------------------------+
   | 27-42         | Reserved         | This reserved field shall be    |
   |               |                  | sent with a value identical to  |
   |               |                  | the value received in the same  |
   |               |                  | field of the A-ASSOCIATE-RQ     |
   |               |                  | PDU, but its value shall not be |
   |               |                  | tested when received.           |
   +---------------+------------------+---------------------------------+
   | 43-74         | Reserved         | This reserved field shall be    |
   |               |                  | sent with a value identical to  |
   |               |                  | the value received in the same  |
   |               |                  | field of the A-ASSOCIATE-RQ     |
   |               |                  | PDU, but its value shall not be |
   |               |                  | tested when received.           |
   +---------------+------------------+---------------------------------+
   | 75-xxx        | Variable items   | This variable field shall       |
   |               |                  | contain the following items:    |
   |               |                  | one Application Context Item,   |
   |               |                  | one or more Presentation        |
   |               |                  | Context Item(s) and one User    |
   |               |                  | Information Item. For a         |
   |               |                  | complete description of these   |
   |               |                  | items see `Application Context  |
   |               |                  | Name <#sect_7.1.1.2>`__,        |
   |               |                  | `Presentation Context           |
   |               |                  | Definition Result               |
   |               |                  | List <#sect_7.1.1.14>`__, and   |
   |               |                  | `User                           |
   |               |                  | Information <#sect_7.1.1.6>`__. |
   +---------------+------------------+---------------------------------+

.. _sect_9.3.3.1:

Application Context Item Structure
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

An Application Context Item shall be made of a sequence of mandatory
fields followed by a variable length field.
`table_title <#table_9-12>`__ shows the sequence of mandatory fields.

.. _sect_9.3.3.2:

Presentation Context Item Structure
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

The Presentation Context Item shall be made of a sequence of mandatory
fixed length fields followed by a variable field.
`table_title <#table_9-18>`__ shows the sequence of the mandatory
fields.

The variable field shall consist of one Transfer Syntax Sub-Item.

.. table:: Presentation Context Item Fields

   +----------------+-------------------------+-------------------------+
   | **Item bytes** | **Field name**          | **Description of        |
   |                |                         | field**                 |
   +================+=========================+=========================+
   | 1              | Item-type               | 21H                     |
   +----------------+-------------------------+-------------------------+
   | 2              | Reserved                | This reserved field     |
   |                |                         | shall be sent with a    |
   |                |                         | value 00H but not       |
   |                |                         | tested to this value    |
   |                |                         | when received.          |
   +----------------+-------------------------+-------------------------+
   | 3-4            | Item-length             | This Item-length shall  |
   |                |                         | be the number of bytes  |
   |                |                         | from the first byte of  |
   |                |                         | the following field to  |
   |                |                         | the last byte of the    |
   |                |                         | Transfer Syntax         |
   |                |                         | Sub-Item. It shall be   |
   |                |                         | encoded as an unsigned  |
   |                |                         | binary number.          |
   +----------------+-------------------------+-------------------------+
   | 5              | Presentation-context-ID | Presentation-context-ID |
   |                |                         | values shall be odd     |
   |                |                         | integers between 1 and  |
   |                |                         | 255, encoded as an      |
   |                |                         | unsigned binary number. |
   |                |                         | For a complete          |
   |                |                         | description of the use  |
   |                |                         | of this field see       |
   |                |                         | `Presentation Context   |
   |                |                         | Definition              |
   |                |                         | Li                      |
   |                |                         | st <#sect_7.1.1.13>`__. |
   +----------------+-------------------------+-------------------------+
   | 6              | Reserved                | This reserved field     |
   |                |                         | shall be sent with a    |
   |                |                         | value 00H but not       |
   |                |                         | tested to this value    |
   |                |                         | when received.          |
   +----------------+-------------------------+-------------------------+
   | 7              | Result/Reason           | This Result/Reason      |
   |                |                         | field shall contain an  |
   |                |                         | integer value encoded   |
   |                |                         | as an unsigned binary   |
   |                |                         | number. One of the      |
   |                |                         | following values shall  |
   |                |                         | be used:                |
   |                |                         |                         |
   |                |                         | 0 - acceptance          |
   |                |                         |                         |
   |                |                         | 1 - user-rejection      |
   |                |                         |                         |
   |                |                         | 2 - no-reason (provider |
   |                |                         | rejection)              |
   |                |                         |                         |
   |                |                         | 3 -                     |
   |                |                         | abstra                  |
   |                |                         | ct-syntax-not-supported |
   |                |                         | (provider rejection)    |
   |                |                         |                         |
   |                |                         | 4 -                     |
   |                |                         | transfer                |
   |                |                         | -syntaxes-not-supported |
   |                |                         | (provider rejection)    |
   +----------------+-------------------------+-------------------------+
   | 8              | Reserved                | This reserved field     |
   |                |                         | shall be sent with a    |
   |                |                         | value 00H but not       |
   |                |                         | tested to this value    |
   |                |                         | when received.          |
   +----------------+-------------------------+-------------------------+
   | 9-xxx          | Transfer syntax         | This variable field     |
   |                | sub-item                | shall contain one       |
   |                |                         | Transfer Syntax         |
   |                |                         | Sub-Item. When the      |
   |                |                         | Result/Reason field has |
   |                |                         | a value other than      |
   |                |                         | acceptance (0), this    |
   |                |                         | field shall not be      |
   |                |                         | significant and its     |
   |                |                         | value shall not be      |
   |                |                         | tested when received.   |
   |                |                         | For a complete          |
   |                |                         | description of the use  |
   |                |                         | and encoding of this    |
   |                |                         | item see `Transfer      |
   |                |                         | Syntax Sub-Item         |
   |                |                         | Structur                |
   |                |                         | e <#sect_9.3.3.2.1>`__. |
   +----------------+-------------------------+-------------------------+

.. _sect_9.3.3.2.1:

Transfer Syntax Sub-Item Structure
''''''''''''''''''''''''''''''''''

The Transfer Syntax Sub-Item shall be made of a sequence of mandatory
fixed length fields followed by a variable field.
`table_title <#table_9-19>`__ shows the sequence of the mandatory
fields.

.. table:: Transfer Syntax Sub-Item Fields

   +----------------+----------------------+-------------------------+
   | **Item bytes** | **Field name**       | **Description of        |
   |                |                      | field**                 |
   +================+======================+=========================+
   | 1              | Item-type            | 40H                     |
   +----------------+----------------------+-------------------------+
   | 2              | Reserved             | This reserved field     |
   |                |                      | shall be sent with a    |
   |                |                      | value 00H but not       |
   |                |                      | tested to this value    |
   |                |                      | when received.          |
   +----------------+----------------------+-------------------------+
   | 3-4            | Item-length          | This Item-length shall  |
   |                |                      | be the number of bytes  |
   |                |                      | from the first byte of  |
   |                |                      | the following field to  |
   |                |                      | the last byte of the    |
   |                |                      | Transfer-syntax-name    |
   |                |                      | field. It shall be      |
   |                |                      | encoded as an unsigned  |
   |                |                      | binary number.          |
   +----------------+----------------------+-------------------------+
   | 5-xxx          | Transfer-syntax-name | This variable field     |
   |                |                      | shall contain the       |
   |                |                      | Transfer-syntax-name    |
   |                |                      | proposed for this       |
   |                |                      | presentation context. A |
   |                |                      | valid                   |
   |                |                      | Transfer-syntax-name    |
   |                |                      | shall be encoded as     |
   |                |                      | defined in `DICOM UL    |
   |                |                      | Encoding Rules for      |
   |                |                      | Application Contexts,   |
   |                |                      | Abstract Syntaxes,      |
   |                |                      | Transfer Syntaxes       |
   |                |                      | (Norm                   |
   |                |                      | ative) <#chapter_F>`__. |
   |                |                      | For a description of    |
   |                |                      | the use of this field   |
   |                |                      | see `Presentation       |
   |                |                      | Context Definition      |
   |                |                      | Result                  |
   |                |                      | Li                      |
   |                |                      | st <#sect_7.1.1.14>`__. |
   |                |                      | Transfer-syntax-names   |
   |                |                      | are structured as UIDs  |
   |                |                      | as defined in (see      |
   |                |                      | `Abstract and Transfer  |
   |                |                      | Syntaxes                |
   |                |                      | (Infor                  |
   |                |                      | mative) <#chapter_B>`__ |
   |                |                      | for an overview of this |
   |                |                      | concept). DICOM         |
   |                |                      | Transfer-syntax-names   |
   |                |                      | are registered in .     |
   +----------------+----------------------+-------------------------+

.. _sect_9.3.3.3:

User Information Item Structure
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

The User Information Item shall be made of a sequence of mandatory
length fields followed by a variable field.
`table_title <#table_9-20>`__ shows the sequence of the mandatory
fields.

The variable field shall consist of one or more User-Data Sub-Items.

.. note::

   The User-Data Sub-Items may be present in any order within the
   User-Information Item. No significance should be placed on the order
   of User-Data Sub-Items within the User Information Item. Sending
   applications should be aware that some older applications might
   expect Sub-Items to be encoded in ascending order of Item-type within
   the enclosing Item.

.. table:: User Information Item Fields

   +----------------+----------------+----------------------------------+
   | **Item bytes** | **Field name** | **Description of field**         |
   +================+================+==================================+
   | 1              | Item-type      | 50H                              |
   +----------------+----------------+----------------------------------+
   | 2              | Reserved       | This reserved field shall be     |
   |                |                | sent with a value 00H but not    |
   |                |                | tested to this value when        |
   |                |                | received.                        |
   +----------------+----------------+----------------------------------+
   | 3-4            | Item-length    | This Item-length shall be the    |
   |                |                | number of bytes from the first   |
   |                |                | byte of the following field to   |
   |                |                | the last byte of the             |
   |                |                | User-data-information field(s).  |
   |                |                | It shall be encoded as an        |
   |                |                | unsigned binary number.          |
   +----------------+----------------+----------------------------------+
   | 5-xxx          | User-data      | This variable field shall        |
   |                |                | contain User-data sub-items as   |
   |                |                | defined by the DICOM Application |
   |                |                | Entity. The structure and        |
   |                |                | content of these sub-items is    |
   |                |                | defined in `Use and Format of    |
   |                |                | the A-ASSOCIATE User Information |
   |                |                | Parameter                        |
   |                |                | (Normative) <#chapter_D>`__.     |
   +----------------+----------------+----------------------------------+

.. _sect_9.3.4:

A-ASSOCIATE-RJ PDU Structure
~~~~~~~~~~~~~~~~~~~~~~~~~~~~

An A-ASSOCIATE-RJ PDU shall be made of a sequence of mandatory fields.
`table_title <#table_9-21>`__ shows the sequence of the mandatory
fields.

.. table:: ASSOCIATE-RJ PDU Fields

   +---------------+----------------+-----------------------------------+
   | **PDU bytes** | **Field name** | **Description of field**          |
   +===============+================+===================================+
   | 1             | PDU-type       | 03H                               |
   +---------------+----------------+-----------------------------------+
   | 2             | Reserved       | This reserved field shall be sent |
   |               |                | with a value 00H but not tested   |
   |               |                | to this value when received.      |
   +---------------+----------------+-----------------------------------+
   | 3-6           | PDU-length     | This PDU-length shall be the      |
   |               |                | number of bytes from the first    |
   |               |                | byte of the following field to    |
   |               |                | the last byte of the Reason/Diag. |
   |               |                | field. In the case of this PDU,   |
   |               |                | it shall have the fixed value of  |
   |               |                | 00000004H encoded as an unsigned  |
   |               |                | binary number.                    |
   +---------------+----------------+-----------------------------------+
   | 7             | Reserved       | This reserved field shall be sent |
   |               |                | with a value 00H but not tested   |
   |               |                | to this value when received.      |
   +---------------+----------------+-----------------------------------+
   | 8             | Result         | This Result field shall contain   |
   |               |                | an integer value encoded as an    |
   |               |                | unsigned binary number. One of    |
   |               |                | the following values shall be     |
   |               |                | used:                             |
   |               |                |                                   |
   |               |                | 1 - rejected-permanent            |
   |               |                |                                   |
   |               |                | 2 - rejected-transient            |
   +---------------+----------------+-----------------------------------+
   | 9             | Source         | This Source field shall contain   |
   |               |                | an integer value encoded as an    |
   |               |                | unsigned binary number. One of    |
   |               |                | the following values shall be     |
   |               |                | used:                             |
   |               |                |                                   |
   |               |                | 1 - DICOM UL service-user         |
   |               |                |                                   |
   |               |                | 2 - DICOM UL service-provider     |
   |               |                | (ACSE related function)           |
   |               |                |                                   |
   |               |                | 3 - DICOM UL service-provider     |
   |               |                | (Presentation related function)   |
   +---------------+----------------+-----------------------------------+
   | 10            | Reason/Diag.   | This field shall contain an       |
   |               |                | integer value encoded as an       |
   |               |                | unsigned binary number. If the    |
   |               |                | Source field has the value (1)    |
   |               |                | "DICOM UL service-user", it shall |
   |               |                | take one of the following:        |
   |               |                |                                   |
   |               |                | 1 - no-reason-given               |
   |               |                |                                   |
   |               |                | 2 -                               |
   |               |                | appli                             |
   |               |                | cation-context-name-not-supported |
   |               |                |                                   |
   |               |                | 3 -                               |
   |               |                | calling-AE-title-not-recognized   |
   |               |                |                                   |
   |               |                | 4-6 - reserved                    |
   |               |                |                                   |
   |               |                | 7 -                               |
   |               |                | called-AE-title-not-recognized    |
   |               |                |                                   |
   |               |                | 8-10 - reserved                   |
   |               |                |                                   |
   |               |                | If the Source field has the value |
   |               |                | (2) "DICOM UL service provided    |
   |               |                | (ACSE related function)", it      |
   |               |                | shall take one of the following:  |
   |               |                |                                   |
   |               |                | 1 - no-reason-given               |
   |               |                |                                   |
   |               |                | 2 -                               |
   |               |                | protocol-version-not-supported    |
   |               |                |                                   |
   |               |                | If the Source field has the value |
   |               |                | (3) "DICOM UL service provided    |
   |               |                | (Presentation related function)", |
   |               |                | it shall take one of the          |
   |               |                | following:                        |
   |               |                |                                   |
   |               |                | 0 - reserved                      |
   |               |                |                                   |
   |               |                | 1 - temporary-congestio           |
   |               |                |                                   |
   |               |                | 2 - local-limit-exceeded          |
   |               |                |                                   |
   |               |                | 3-7 - reserved                    |
   |               |                |                                   |
   |               |                | .. note::                         |
   |               |                |                                   |
   |               |                |    The reserved fields are used   |
   |               |                |    to preserve symmetry with OSI  |
   |               |                |    ACSE/Presentation Services and |
   |               |                |    Protocols.                     |
   +---------------+----------------+-----------------------------------+

.. _sect_9.3.5:

P-DATA-TF PDU Structure
~~~~~~~~~~~~~~~~~~~~~~~

A P-DATA-TF PDU shall be made of a sequence of mandatory fixed length
fields followed by a variable length field.
`table_title <#table_9-22>`__ shows the sequence of the mandatory
fields.

The variable data field shall contain one or more
Presentation-Data-Value Items.

.. table:: P-DATA-TF PDU Fields

   +---------------+-------------------------+-------------------------+
   | **PDU bytes** | **Field name**          | **Description of        |
   |               |                         | field**                 |
   +===============+=========================+=========================+
   | 1             | PDU-type                | 04H                     |
   +---------------+-------------------------+-------------------------+
   | 2             | Reserved                | This reserved field     |
   |               |                         | shall be sent with a    |
   |               |                         | value 00H but not       |
   |               |                         | tested to this value    |
   |               |                         | when received.          |
   +---------------+-------------------------+-------------------------+
   | 3-6           | PDU-length              | This PDU-length shall   |
   |               |                         | be the number of bytes  |
   |               |                         | from the first byte of  |
   |               |                         | the following field to  |
   |               |                         | the last byte of the    |
   |               |                         | variable field. It      |
   |               |                         | shall be encoded as an  |
   |               |                         | unsigned binary number. |
   +---------------+-------------------------+-------------------------+
   | 7-xxx         | Presentation-data-value | This variable data      |
   |               | Item(s)                 | field shall contain one |
   |               |                         | or more                 |
   |               |                         | Presentation-data-value |
   |               |                         | Items(s). For a         |
   |               |                         | complete description of |
   |               |                         | the use of this field   |
   |               |                         | see `Presentation Data  |
   |               |                         | Value Item              |
   |               |                         | Struc                   |
   |               |                         | ture <#sect_9.3.5.1>`__ |
   +---------------+-------------------------+-------------------------+

.. _sect_9.3.5.1:

Presentation Data Value Item Structure
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

The Presentation Data Value Item shall be made of a sequence of
mandatory fixed length fields followed by one variable length field.
`table_title <#table_9-23>`__ shows the sequence of the fields.

The variable field shall consist of one Presentation-Data-Value.

.. table:: Presentation-Data-Value Item Fields

   +----------------+-------------------------+-------------------------+
   | **Item bytes** | **Field name**          | **Description of        |
   |                |                         | field**                 |
   +================+=========================+=========================+
   | 1-4            | Item-length             | This Item-length shall  |
   |                |                         | be the number of bytes  |
   |                |                         | from the first byte of  |
   |                |                         | the following field to  |
   |                |                         | the last byte of the    |
   |                |                         | Presentation-data-value |
   |                |                         | field. It shall be      |
   |                |                         | encoded as an unsigned  |
   |                |                         | binary number.          |
   +----------------+-------------------------+-------------------------+
   | 5              | Presentation-context-ID | Presentation-context-ID |
   |                |                         | values shall be odd     |
   |                |                         | integers between 1 and  |
   |                |                         | 255, encoded as an      |
   |                |                         | unsigned binary number. |
   |                |                         | For a complete          |
   |                |                         | description of the use  |
   |                |                         | of this field see       |
   |                |                         | `Presentation Context   |
   |                |                         | Definition              |
   |                |                         | Li                      |
   |                |                         | st <#sect_7.1.1.13>`__. |
   +----------------+-------------------------+-------------------------+
   | 6-xxx          | Presentation-data-value | This                    |
   |                |                         | Presentation-data-value |
   |                |                         | field shall contain     |
   |                |                         | DICOM message           |
   |                |                         | information (command    |
   |                |                         | and/or Data Set) with a |
   |                |                         | message control header. |
   |                |                         | For a complete          |
   |                |                         | description of the use  |
   |                |                         | of this field see       |
   |                |                         | `Usage of the P-DATA    |
   |                |                         | Service By the DICOM    |
   |                |                         | Application Entity      |
   |                |                         | (Norm                   |
   |                |                         | ative) <#chapter_E>`__. |
   +----------------+-------------------------+-------------------------+

.. _sect_9.3.6:

A-RELEASE-RQ PDU Structure
~~~~~~~~~~~~~~~~~~~~~~~~~~

An A-RELEASE-RQ PDU shall be made of a sequence of mandatory fields.
`table_title <#table_9-24>`__ shows the sequence of the fields.

.. table:: A-RELEASE-RQ PDU Fields

   +---------------+----------------+-----------------------------------+
   | **PDU bytes** | **Field name** | **Description of field**          |
   +===============+================+===================================+
   | 1             | PDU-type       | 05H                               |
   +---------------+----------------+-----------------------------------+
   | 2             | Reserved       | This reserved field shall be sent |
   |               |                | with a value 00H but not tested   |
   |               |                | to this value when received.      |
   +---------------+----------------+-----------------------------------+
   | 3-6           | PDU-length     | This PDU-length shall be the      |
   |               |                | number of bytes from the first    |
   |               |                | byte of the following field to    |
   |               |                | the last byte of the Reserved     |
   |               |                | field. In the case of this PDU,   |
   |               |                | it shall have the fixed value of  |
   |               |                | 00000004H encoded as an unsigned  |
   |               |                | binary number.                    |
   +---------------+----------------+-----------------------------------+
   | 7-10          | Reserved       | This reserved field shall be sent |
   |               |                | with a value 00000000H but not    |
   |               |                | tested to this value when         |
   |               |                | received.                         |
   +---------------+----------------+-----------------------------------+

.. _sect_9.3.7:

A-RELEASE-RP PDU Structure
~~~~~~~~~~~~~~~~~~~~~~~~~~

An A-RELEASE-RP PDU shall be made of a sequence of mandatory fields.
`table_title <#table_9-25>`__ shows the sequence of the fields.

.. table:: A-RELEASE-RP PDU Fields

   +---------------+----------------+-----------------------------------+
   | **PDU bytes** | **Field name** | **Description of field**          |
   +===============+================+===================================+
   | 1             | PDU-type       | 06H                               |
   +---------------+----------------+-----------------------------------+
   | 2             | Reserved       | This reserved field shall be sent |
   |               |                | with a value 00H but not tested   |
   |               |                | to this value when received.      |
   +---------------+----------------+-----------------------------------+
   | 3-6           | PDU-length     | This PDU-length shall be the      |
   |               |                | number of bytes from the first    |
   |               |                | byte of the following field to    |
   |               |                | the last byte of the Reserved     |
   |               |                | field. In the case of this PDU,   |
   |               |                | it shall have the fixed value of  |
   |               |                | 00000004H encoded as an unsigned  |
   |               |                | binary number.                    |
   +---------------+----------------+-----------------------------------+
   | 7-10          | Reserved       | This reserved field shall be sent |
   |               |                | with a value 00000000H but not    |
   |               |                | tested to this value when         |
   |               |                | received.                         |
   +---------------+----------------+-----------------------------------+

.. _sect_9.3.8:

A-ABORT PDU Structure
~~~~~~~~~~~~~~~~~~~~~

An A-ABORT PDU shall be made of a sequence of mandatory fields.
`table_title <#table_9-26>`__ shows the sequence of the fields.

The A-ABORT PDU shall support both the A-ABORT Service (user initiated)
and the A-P-ABORT Service (provider initiated).

.. table:: A-ABORT PDU Fields

   +---------------+----------------+-----------------------------------+
   | **PDU bytes** | **Field name** | **Description of field**          |
   +===============+================+===================================+
   | 1             | PDU-type       | 07H                               |
   +---------------+----------------+-----------------------------------+
   | 2             | Reserved       | This reserved field shall be sent |
   |               |                | with a value 00H but not tested   |
   |               |                | to this value when received.      |
   +---------------+----------------+-----------------------------------+
   | 3-6           | PDU-length     | This PDU-length shall be the      |
   |               |                | number of bytes from the first    |
   |               |                | byte of the following field to    |
   |               |                | the last byte of the Reserved     |
   |               |                | field. In the case of this PDU,   |
   |               |                | it shall have the fixed value of  |
   |               |                | 00000004H encoded as an unsigned  |
   |               |                | binary number.                    |
   +---------------+----------------+-----------------------------------+
   | 7             | Reserved       | This reserved field shall be sent |
   |               |                | with a value 00H but not tested   |
   |               |                | to this value when received.      |
   +---------------+----------------+-----------------------------------+
   | 8             | Reserved       | This reserved field shall be sent |
   |               |                | with a value 00H but not tested   |
   |               |                | to this value when received.      |
   +---------------+----------------+-----------------------------------+
   | 9             | Source         | This Source field shall contain   |
   |               |                | an integer value encoded as an    |
   |               |                | unsigned binary number. One of    |
   |               |                | the following values shall be     |
   |               |                | used:                             |
   |               |                |                                   |
   |               |                | 0 - DICOM UL service-user         |
   |               |                | (initiated abort)                 |
   |               |                |                                   |
   |               |                | 1 - reserved                      |
   |               |                |                                   |
   |               |                | 2 - DICOM UL service-provider     |
   |               |                | (initiated abort)                 |
   +---------------+----------------+-----------------------------------+
   | 10            | Reason/Diag.,  | This field shall contain an       |
   |               |                | integer value encoded as an       |
   |               |                | unsigned binary number. If the    |
   |               |                | Source field has the value (2)    |
   |               |                | "DICOM UL service-provider", it   |
   |               |                | shall take one of the following:  |
   |               |                |                                   |
   |               |                | 0 - reason-not-specified1 -       |
   |               |                | unrecognized-PDU                  |
   |               |                |                                   |
   |               |                | 2 - unexpected-PDU                |
   |               |                |                                   |
   |               |                | 3 - reserved                      |
   |               |                |                                   |
   |               |                | 4 - unrecognized-PDU parameter    |
   |               |                |                                   |
   |               |                | 5 - unexpected-PDU parameter      |
   |               |                |                                   |
   |               |                | 6 - invalid-PDU-parameter value   |
   |               |                |                                   |
   |               |                | If the Source field has the value |
   |               |                | (0) "DICOM UL service-user", this |
   |               |                | reason field shall not be         |
   |               |                | significant. It shall be sent     |
   |               |                | with a value 00H but not tested   |
   |               |                | to this value when received.      |
   |               |                |                                   |
   |               |                | .. note::                         |
   |               |                |                                   |
   |               |                |    The reserved fields are used   |
   |               |                |    to preserve symmetry with OSI  |
   |               |                |    ACSE/Presentation Services and |
   |               |                |    Protocol.                      |
   +---------------+----------------+-----------------------------------+

