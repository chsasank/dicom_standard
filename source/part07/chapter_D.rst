.. _chapter_D:

Association Negotiation (Normative)
===================================

Association establishment is the first phase of any instance of
communication between peer DICOM AEs. The AEs use the Association
establishment to negotiate how data will be encoded and the type of data
to be exchanged. This Annex provides an overview of the negotiation
mechanisms plus a discussion of each concept, its objectives,
relationships, usage principles and specifications.

.. _sect_D.1:

Abstract Syntax
---------------

Abstract Syntaxes specify the Application Layer Data Elements and
Application Layer protocol control information (with associated
semantics) that are independent of the encoding technique used to
represent them.

Each Abstract Syntax shall be identified by an Abstract Syntax Name in
the form of a UID. DICOM AEs use the Abstract Syntax Name to identify
and negotiate which SOP Classes and related options are supported on a
specific Association. Abstract Syntax Names shall be defined in the
Service Class Definitions specified in . Each Abstract Syntax Name
defined shall have a value of either

-  a Service-Object Pair Class UID

-  a Meta Service-Object Pair Group UID

.. _sect_D.1.1:

Service-Object Pair Class UID
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

Each Service Class Definition defines one or more functionally-related
Service-Object Pair (SOP) Class definitions that specify well-defined
operations and/or notifications that may be performed between peer DICOM
Application Entities to provide an application-level service. Each SOP
Class, identified by a SOP Class UID, is defined by the union of one
Information Object Definition (IOD) and a specific set of one or more
DIMSE Services called the DIMSE Service Group (DSG) in that

-  The IOD defines the data structures

-  The DSG defines the operations and/or notifications that can be
   performed on this data structure.

Two SOP Classes defined by a single Service Class Definition may differ
by the IOD, the DSG or both. Two different IODs shall not, however, be
part of the same SOP Class. `figure_title <#figure_D.1-1>`__ shows the
relationships between Service Classes, IODs, DSGs and SOP Classes.

.. note::

   1. Two examples of Service Classes are the Storage and Study
      Management Service Classes. The Storage Service Class relates to
      image Information Object Definitions such as CT, MR etc. and the
      Study Management Service Class relates to the Study Information
      Object Definition.

   2. For readers familiar with OSI terminology, the concept of the
      Managed Object Class is the equivalent to the DICOM Service-Object
      Pair Class. The SOP Class specifies both the data (Attributes
      defined in the Information Object Definition) and the methods
      (Operations and Notifications (DSG) defined in the Service Class).

By setting the Abstract Syntax Name to a specific SOP Class UID value,
DICOM Application Entities may negotiate Service Class operations and/or
notifications for each defined SOP Class individually.

.. _sect_D.1.2:

Meta Service-Object Pair Group UID
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

Each Service Class Definition may optionally define one or more Meta
Service-Object Pair Classes each being identified by a Meta SOP Class
UID. Each Meta SOP Class represents the union of a set of SOP Classes
defined in the Service Class.

By setting the Abstract Syntax Name to a specific Meta SOP Class UID
value, DICOM Application Entities may negotiate Service Class operations
and/or notifications for a set of defined SOP Classes using a single
Abstract Syntax. `figure_title <#figure_D.1-2>`__ depicts this.

.. _sect_D.2:

Transfer Syntaxes
-----------------

Transfer Syntaxes define a set of encoding rules used to unambiguously
represent one or more Abstract Syntaxes. It allows communicating DICOM
AEs to negotiate the encoding techniques they are able to support (e.g.,
byte ordering, compression, etc.).

.. _sect_D.3:

Association Establishment
-------------------------

Association establishment is used to negotiate the type of data to be
exchanged and how the data will be encoded. DICOM AEs establish
Associations by using the ACSE A-ASSOCIATE Service as defined by Part 8
of the DICOM Standard. Three key parameters conveyed in the A-ASSOCIATE
Service are the Application Context, Presentation Context, and the User
Information Items. The following section discusses these negotiation
parameters.

Note: The A-ASSOCIATE Service is performed only once at Association
established time. The examples shown in this Section separate the
negotiation parameters for clarification purposes only. Readers should
remember that only one A-ASSOCIATE request is offered for each
Association and it contains all of the negotiation parameters.

.. _sect_D.3.1:

Application Context
~~~~~~~~~~~~~~~~~~~

An Application Context explicitly defines the set of Application Service
Elements, related options and any other information necessary for the
inter-working of DICOM AEs on an Association.

The Application Context provides the highest level of negotiation,
therefore, a very high level definition. Only one Application Context
shall be offered per Association. DICOM specifies a single Application
Context Name that defines the DICOM Application Context (applicable for
this Standard and potentially later versions).

.. note::

   For complete specification see `Application Context Usage
   (Normative) <#chapter_A>`__.

.. _sect_D.3.2:

Presentation Contexts Negotiation
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

A Presentation Context defines the presentation of the data on an
Association. It provides a lower level of negotiation and one or more
Presentation Contexts can be offered and accepted per Association.

A Presentation Context consists of three components, a Presentation
Context ID, an Abstract Syntax Name, and a list of one or more Transfer
Syntax Names.

Only one Abstract Syntax shall be offered per Presentation Context.
However, multiple Transfer Syntaxes may be offered per Presentation
Context, but only one shall be accepted.

For each SOP Class or Meta SOP Class a Presentation Context must be
negotiated such that this Presentation Context supports the associated
Abstract Syntax and a suitable Transfer Syntax. Presentation Contexts
will be identified within the scope of a specific Association by a
Presentation Context ID.

`figure_title <#figure_D.3-1>`__ provides an illustration of
Presentation Context Negotiation with the key points as follows:

a. the Association-requester may offer multiple Presentation Contexts
   per Association.

b. each Presentation Context supports one Abstract Syntax (related to a
   SOP Class or Meta SOP Class) and one or more Transfer Syntaxes.

c. the Association-acceptor may accept or reject each Presentation
   Context individually.

d. the Association-acceptor selects a suitable Transfer Syntax for each
   Presentation Context accepted.

.. _sect_D.3.3:

DICOM Application Association Information
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

Peer DICOM AEs negotiate, at Association establishment, a number of
features related to the DIMSE protocol by using the ACSE User
Information Item of the A-ASSOCIATE request. This Section discusses
these features.

When the Association is established between peer DIMSE Service Users the
Kernel Functional Unit shall be assumed; therefore, the Kernel
Functional Unit shall not be included in the A-ASSOCIATE User
Information item.

.. _sect_D.3.3.1:

Maximum Length Application PDU Notification
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

The Maximum Length notification allows communicating AEs to limit the
size of the data for each P-DATA indication. Each DICOM AE defines the
maximum PDU size it can receive on this Association. Therefore,
different maximum lengths can be specified for each direction of data
flow on an Association. This notification is required.
`figure_title <#figure_D.3-2>`__ illustrates the Maximum Length
notification.

.. note::

   For complete specification see .

.. _sect_D.3.3.2:

Implementation Identification Notification
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

The implementation identification notification allows implementations of
communicating AEs to identify each other at Association establishment
time. It is intended to provide respective (each network node knows the
other's implementation identity) and non-ambiguous identification in the
event of communication problems encountered between two nodes. This
negotiation is required.

Implementation identification relies on two pieces of information:

-  Implementation Class UID (required)

-  Implementation Version Name (optional)

The Implementation Class UID identifies in a unique manner a specific
class of implementation. Each node claiming conformance to this Standard
shall be assigned an Implementation Class UID to distinguish its
implementation environment from others. Such Implementation Class UIDs
shall be registered by the implementing organization per the policies
defined in . This Standard does not specify the policies associated with
assigning such a UID.

Different equipment of the same type or product line (but having
different serial numbers) shall use the same Implementation Class UID if
they share the same implementation environment (i.e., software).

The notification by Association requestors and acceptors of their
respective Implementation Class UID is required for all implementations
conforming to this Standard. `figure_title <#figure_D.3-3>`__
illustrates the Implementation Class UID notification.

In addition to the Implementation Class UID, an option is provided to
convey an Implementation Version Name of up to 16 characters.
`figure_title <#figure_D.3-4>`__ illustrates the Implementation Version
Name notification. This Standard does not specify the structure and
policies associated with such an Implementation Version Name. The
absence of the Implementation Version Name requires that the use of the
same Implementation Class UID by two nodes guarantees that these use the
same version of implementation.

.. note::

   As the UID shall not be parsed (their structure is not intended to
   convey any semantic significance beyond uniqueness), this optional
   Implementation Version Name provides an adequate mechanism to
   distinguish two versions of the same implementation (same
   Implementation Class UID).

.. _sect_D.3.3.2.1:

Implementation Class UID Sub-Item Structure (A-ASSOCIATE-RQ)
''''''''''''''''''''''''''''''''''''''''''''''''''''''''''''

The Implementation Class UID Sub-Item shall be made of a sequence of
mandatory fixed length fields followed by a variable field. Only one
Implementation Class UID Sub-Item shall be present in the User Data Item
of the A-ASSOCIATE-RQ. `table_title <#table_D.3-1>`__ shows the sequence
of the mandatory fields.

.. table:: Implementation Class UID Sub-Item Fields (A-ASSOCIATE-RQ)

   +----------------+-------------------------+-------------------------+
   | **Item Bytes** | **Field Name**          | **Description of        |
   |                |                         | Field**                 |
   +================+=========================+=========================+
   | 1              | Item-type               | 52H                     |
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
   |                |                         | I                       |
   |                |                         | mplementation-class-uid |
   |                |                         | field. It shall be      |
   |                |                         | encoded as an unsigned  |
   |                |                         | binary number.          |
   +----------------+-------------------------+-------------------------+
   | 5-xxx          | I                       | This variable field     |
   |                | mplementation-class-uid | shall contain the       |
   |                |                         | I                       |
   |                |                         | mplementation-class-uid |
   |                |                         | of the                  |
   |                |                         | Association-requester   |
   |                |                         | as defined in           |
   |                |                         | `Implementation         |
   |                |                         | Identification          |
   |                |                         | Notificat               |
   |                |                         | ion <#sect_D.3.3.2>`__. |
   |                |                         | The                     |
   |                |                         | I                       |
   |                |                         | mplementation-class-uid |
   |                |                         | field is structured as  |
   |                |                         | a UID as defined in .   |
   +----------------+-------------------------+-------------------------+

.. _sect_D.3.3.2.2:

Implementation Class UID Sub-Item Structure (A-ASSOCIATE-AC)
''''''''''''''''''''''''''''''''''''''''''''''''''''''''''''

The Implementation Class UID Sub-Item shall be made of a sequence of
mandatory fixed length fields followed by a variable field. Only one
Implementation Class UID Sub-Item shall be present in the User Data Item
of the A-ASSOCIATE-AC. `table_title <#table_D.3-2>`__ shows the sequence
of the mandatory fields.

.. table:: Implementation UID Sub-Item Fields (A-ASSOCIATE-AC)

   +----------------+-------------------------+-------------------------+
   | **Item Bytes** | **Field Name**          | **Description of        |
   |                |                         | Field**                 |
   +================+=========================+=========================+
   | 1              | Item-type               | 52H                     |
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
   |                |                         | I                       |
   |                |                         | mplementation-class-uid |
   |                |                         | field. It shall be      |
   |                |                         | encoded as an unsigned  |
   |                |                         | binary number.          |
   +----------------+-------------------------+-------------------------+
   | 5-xxx          | I                       | This variable field     |
   |                | mplementation-class-uid | shall contain the       |
   |                |                         | I                       |
   |                |                         | mplementation-class-uid |
   |                |                         | of the                  |
   |                |                         | Association-acceptor as |
   |                |                         | defined in              |
   |                |                         | `Implementation         |
   |                |                         | Identification          |
   |                |                         | Notificat               |
   |                |                         | ion <#sect_D.3.3.2>`__. |
   |                |                         | The                     |
   |                |                         | I                       |
   |                |                         | mplementation-class-uid |
   |                |                         | field is structured as  |
   |                |                         | a UID as defined in .   |
   +----------------+-------------------------+-------------------------+

.. _sect_D.3.3.2.3:

Implementation Version Name Structure (A-ASSOCIATE-RQ)
''''''''''''''''''''''''''''''''''''''''''''''''''''''

The Implementation Version Name Sub-Item shall be made of a sequence of
mandatory fixed length fields followed by a variable field. Only one
Implementation Version Name Sub-Item shall be present in the User Data
Item of the A-ASSOCIATE-RQ. `table_title <#table_D.3-3>`__ shows the
sequence of the mandatory fields.

.. table:: Implementation Version Name Sub-Item Fields (A-ASSOCIATE-RQ)

   +----------------+-------------------------+-------------------------+
   | **Item Bytes** | **Field Name**          | **Description of        |
   |                |                         | Field**                 |
   +================+=========================+=========================+
   | 1              | Item-type               | 55H                     |
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
   |                |                         | Impl                    |
   |                |                         | ementation-version-name |
   |                |                         | field. It shall be      |
   |                |                         | encoded as an unsigned  |
   |                |                         | binary number.          |
   +----------------+-------------------------+-------------------------+
   | 5-xxx          | Impl                    | This variable field     |
   |                | ementation-version-name | shall contain the       |
   |                |                         | Impl                    |
   |                |                         | ementation-version-name |
   |                |                         | of the                  |
   |                |                         | Association-requester   |
   |                |                         | as defined in           |
   |                |                         | `Implementation         |
   |                |                         | Identification          |
   |                |                         | Notificat               |
   |                |                         | ion <#sect_D.3.3.2>`__. |
   |                |                         | It shall be encoded as  |
   |                |                         | a string of 1 to 16 ISO |
   |                |                         | 646:1990 (basic G0 set) |
   |                |                         | characters.             |
   +----------------+-------------------------+-------------------------+

.. _sect_D.3.3.2.4:

Implementation Version Name Structure (A-ASSOCIATE-AC)
''''''''''''''''''''''''''''''''''''''''''''''''''''''

The Implementation Version Name Sub-Item shall be made of a sequence of
mandatory fixed length fields followed by a variable field. Only one
Implementation Version Name Sub-Item shall be present in the User Data
Item of the A-ASSOCIATE-AC. `table_title <#table_D.3-4>`__ shows the
sequence of the mandatory fields.

.. table:: Implementation Version Name Sub-Item Fields (A-ASSOCIATE-AC)

   +----------------+-------------------------+-------------------------+
   | **Item Bytes** | **Field Name**          | **Description of        |
   |                |                         | Field**                 |
   +================+=========================+=========================+
   | 1              | Item-type               | 55H                     |
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
   |                |                         | Impl                    |
   |                |                         | ementation-version-name |
   |                |                         | field. It shall be      |
   |                |                         | encoded as an unsigned  |
   |                |                         | binary number.          |
   +----------------+-------------------------+-------------------------+
   | 5-xxx          | Impl                    | This variable field     |
   |                | ementation-version-name | shall contain the       |
   |                |                         | Impl                    |
   |                |                         | ementation-version-name |
   |                |                         | of the                  |
   |                |                         | Association-acceptor as |
   |                |                         | defined in              |
   |                |                         | `Implementation         |
   |                |                         | Identification          |
   |                |                         | Notificat               |
   |                |                         | ion <#sect_D.3.3.2>`__. |
   |                |                         | It shall be encoded as  |
   |                |                         | a string of 1 to 16 ISO |
   |                |                         | 646:1990 (basic G0 set) |
   |                |                         | characters.             |
   +----------------+-------------------------+-------------------------+

.. _sect_D.3.3.3:

Asynchronous Operations (And Sub-Operations) Window Negotiation
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

The Asynchronous Operations Window is used to negotiate the maximum
number of outstanding operation or sub-operation requests (i.e., command
requests) for each direction. The synchronous operations mode is the
default mode and shall be supported by all DICOM AEs. This negotiation
is optional.

The Association-requester conveys in the A-ASSOCIATE request:

-  when negotiating the SCU role for operations, the maximum number of
   outstanding operations it may invoke asynchronously; when negotiating
   the SCP role for operations, the maximum number of outstanding
   sub-operations it may invoke asynchronously; when negotiating the SCP
   role for notifications, the maximum number of notifications it may
   invoke asynchronously

-  when negotiating the SCP role for operations, the maximum number of
   outstanding operations it may invoke asynchronously; when negotiating
   the SCU role for operations, the maximum number of outstanding
   sub-operations it may perform asynchronously; when negotiating the
   SCU role for notifications, the maximum number of notifications it
   may perform asynchronously when negotiating the SCP role

A value of zero indicates that the above parameters are unlimited. A
value of one indicates that there is no Asynchronous Operations support.
If the Asynchronous Operations Window is absent the default for the
above parameters shall be equal to one.

The Association-acceptor conveys in the A-ASSOCIATE response:

-  when negotiating the SCP role for operations, the maximum number of
   outstanding operations; when negotiating the SCU role for operations,
   the maximum number of sub-operations it allows the
   Association-requester to invoke asynchronously; when negotiating the
   SCU role for notifications, the maximum number of outstanding
   notifications it allows the Association-requester to invoke
   asynchronously when negotiating the SCU role. This number shall be
   equal or less than the number of outstanding notifications,
   operations and/or sub-operations the Association-requester offers to
   invoke (by the A-ASSOCIATE indication).

-  when negotiating the SCU role for operations, the maximum number of
   outstanding operations; when negotiating the SCP role for operations,
   the maximum number of sub-operations it allows the
   Association-requester to perform asynchronously; when negotiating the
   SCP role for notifications, the maximum number of outstanding
   notifications it allows the Association-requester to perform
   asynchronously. This number shall be equal or less than the number of
   outstanding notifications, operations and/or sub-operations the
   Association-requester offers to perform (by the A-ASSOCIATE
   indication).

A value of zero indicates that the above parameters are unlimited. If
the Asynchronous Operations Window is absent the default for the above
parameters shall be equal to one. Figures D.3-5 and D.3-6 illustrate
examples of Asynchronous Operations Window negotiation.

If this negotiation is not present in the A-ASSOCIATE indication it
shall be omitted in the A-ASSOCIATE response.

.. note::

   The case where the Association-requester offers the value of zero
   (which indicates unlimited operations), the Association-acceptor may
   return zero (agreeing to unlimited operations) or negotiate the
   parameter down by conveying a value other than zero.

.. _sect_D.3.3.3.1:

Asynchronous Operations Window Sub-Item Structure (A-ASSOCIATE-RQ)
''''''''''''''''''''''''''''''''''''''''''''''''''''''''''''''''''

The Asynchronous Operations Window Sub-Item shall be made of a sequence
of mandatory fixed length fields. This Sub-Item is optional and if
supported, only one Asynchronous Operations Window Sub-Item shall be
present in the User Data Item of the A-ASSOCIATE-RQ.
`table_title <#table_D.3-7>`__ shows the sequence of the mandatory
fields.

.. table:: Asynchronous Operations Window Sub-Item Fields
(A-ASSOCIATE-RQ)

   +----------------+-------------------------+-------------------------+
   | **Item Bytes** | **Field Name**          | **Description of        |
   |                |                         | Field**                 |
   +================+=========================+=========================+
   | 1              | Item-type               | 53H                     |
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
   |                |                         | Maximum-numb            |
   |                |                         | er-operations-performed |
   |                |                         | field. In the case of   |
   |                |                         | this Sub-Item, it shall |
   |                |                         | have the fixed value of |
   |                |                         | 00000004H encoded as an |
   |                |                         | unsigned binary number. |
   +----------------+-------------------------+-------------------------+
   | 5-6            | Maximum-nu              | This field shall        |
   |                | mber-operations-invoked | contain the             |
   |                |                         | Maximum-nu              |
   |                |                         | mber-operations-invoked |
   |                |                         | as defined for the      |
   |                |                         | Association-requester   |
   |                |                         | in `Asynchronous        |
   |                |                         | Operations (And         |
   |                |                         | Sub-Operations) Window  |
   |                |                         | Negotiat                |
   |                |                         | ion <#sect_D.3.3.3>`__. |
   |                |                         | It shall be encoded as  |
   |                |                         | an unsigned binary      |
   |                |                         | number.                 |
   +----------------+-------------------------+-------------------------+
   | 7-8            | Maximum-numb            | This field shall        |
   |                | er-operations-performed | contain the             |
   |                |                         | Maximum-numb            |
   |                |                         | er-operations-performed |
   |                |                         | as defined for the      |
   |                |                         | Association-requester   |
   |                |                         | in `Asynchronous        |
   |                |                         | Operations (And         |
   |                |                         | Sub-Operations) Window  |
   |                |                         | Negotiat                |
   |                |                         | ion <#sect_D.3.3.3>`__. |
   |                |                         | It shall be encoded as  |
   |                |                         | an unsigned binary      |
   |                |                         | number.                 |
   +----------------+-------------------------+-------------------------+

.. _sect_D.3.3.3.2:

Asynchronous Operations Window Sub-Item Structure (A-ASSOCIATE-AC)
''''''''''''''''''''''''''''''''''''''''''''''''''''''''''''''''''

The Asynchronous Operations Window Sub-Item shall be made of a sequence
of mandatory fixed length fields. This Sub-Item is optional and if
supported, only one Asynchronous Operations Window Sub-Item shall be
present in the User Data Item of the A-ASSOCIATE-AC.
`table_title <#table_D.3-8>`__ shows the sequence of the mandatory
fields.

.. table:: Asynchronous Operations Window Sub-Item Fields
(A-ASSOCIATE-AC)

   +----------------+-------------------------+-------------------------+
   | **Item Bytes** | **Field Name**          | **Description of        |
   |                |                         | Field**                 |
   +================+=========================+=========================+
   | 1              | Item-type               | 53H                     |
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
   |                |                         | Maximum-numb            |
   |                |                         | er-operations-performed |
   |                |                         | field. In the case of   |
   |                |                         | this Sub-Item, it shall |
   |                |                         | have the fixed value of |
   |                |                         | 00000004H encoded as an |
   |                |                         | unsigned binary number. |
   +----------------+-------------------------+-------------------------+
   | 5-6            | Maximum-nu              | This field shall        |
   |                | mber-operations-invoked | contain the             |
   |                |                         | Maximum-nu              |
   |                |                         | mber-operations-invoked |
   |                |                         | as defined for the      |
   |                |                         | Association-acceptor in |
   |                |                         | `Asynchronous           |
   |                |                         | Operations (And         |
   |                |                         | Sub-Operations) Window  |
   |                |                         | Negotia                 |
   |                |                         | tion <#sect_D.3.3.3>`__ |
   |                |                         | It shall be encoded as  |
   |                |                         | an unsigned binary      |
   |                |                         | number.                 |
   +----------------+-------------------------+-------------------------+
   | 7-8            | Maximum-numb            | This field shall        |
   |                | er-operations-performed | contain the             |
   |                |                         | Maximum-numb            |
   |                |                         | er-operations-performed |
   |                |                         | as defined for the      |
   |                |                         | Association-acceptor in |
   |                |                         | `Asynchronous           |
   |                |                         | Operations (And         |
   |                |                         | Sub-Operations) Window  |
   |                |                         | Negotiat                |
   |                |                         | ion <#sect_D.3.3.3>`__. |
   |                |                         | It shall be encoded as  |
   |                |                         | an unsigned binary      |
   |                |                         | number.                 |
   +----------------+-------------------------+-------------------------+

.. _sect_D.3.3.4:

SCP/SCU Role Selection Negotiation
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

The SCP/SCU Role Selection Negotiation allows peer AEs to negotiate the
roles in which they will serve for each SOP Class or Meta SOP Class
supported on the Association. This negotiation is optional.

The Association-requester, for each SOP Class UID or Meta SOP Class UID,
may use one SCP/SCU Role Selection item. The SOP Class or Meta SOP Class
shall be identified by its corresponding Abstract Syntax Name followed
by one of the three role values:

-  Association-requester is SCU only

-  Association-requester is SCP only

-  Association-requester is both SCU and SCP

If the SCP/SCU Role Selection item is absent the default role of the
Association-requester shall be SCU and the default role of the
Association-acceptor shall be SCP.

The Association-acceptor, for each SCP/SCU Role Selection item offered,
either accepts the Association-requester proposal by returning the same
value (1) or turns down the proposal by returning the value (0). The
Association-acceptor shall not return the value (1) if the
Association-requester has not proposed the role, i.e., it has sent a
value (0). The Association-requester shall ignore the response if it has
not proposed the role.

If the SCP/SCU Role Selection item is not returned by the
Association-acceptor then the role of the Association-requester shall be
SCU and the role of the Association-acceptor shall be SCP.
`figure_title <#figure_D.3-7>`__ illustrates the SCP/SCU Role Selection
Negotiation.

If the SCP/SCU Role Selection items do not exist in the A-ASSOCIATE
indication they shall be omitted in the A-ASSOCIATE response.

.. note::

   1. The choices made for the default roles are based on clarification
      made to previous versions of the Standard. Association-requesters
      that wish to offer Abstract Syntax Names using the SCP role must
      support this item. Association-acceptors that wish to accept
      Abstract Syntax Names using the SCU role must support this item.

   2. If an Association-requestor offers an SCP/SCU Role Selection item
      for an Abstract Syntax Name but the Association-acceptor does not
      return a SCP/SCU Role Selection item for the same Abstract Syntax
      Name then the proposed roles have not been accepted and the
      default roles apply (i.e., Association-requester is SCU and
      Association-acceptor is SCP).

.. note::

   1. DICOM AE "B" accepts DICOM AE "A"'s proposed role as an SCU for
      the Storage-MR SOP; therefore, DICOM AE "B" will perform in the
      SCP role. DICOM AE "B" turns down the SCP proposal from DICOM AE
      "A".

   2. Both DICOM AEs may be SCU and SCP for the Storage-CT SOP.

   3. DICOM AE "B" accepts DICOM AE "A"'s proposed role as an SCU for
      the Print-SOP; therefore, DICOM AE "B" will perform in the SCP
      role.

.. _sect_D.3.3.4.1:

SCP/SCU Role Selection Sub-Item Structure (A-ASSOCIATE-RQ)
''''''''''''''''''''''''''''''''''''''''''''''''''''''''''

The SCP/SCU Role Selection Sub-Item shall be made of a sequence of
mandatory fields. This Sub-Item is optional and if supported, one or
more SCP/SCU Role Selection Sub-Items may be present in the User Data
Item of the A-ASSOCIATE-RQ. The Association-requester may only offer one
SOP Class SCP/SCU Role Selection Sub-Item for each SOP Class UID or Meta
SOP Class that is present in the A-ASSOCIATE request.
`table_title <#table_D.3-9>`__ shows the sequence of the mandatory
fields.

.. table:: SCP/SCU Role Selection Sub-Item Fields (A-ASSOCIATE-RQ)

   +----------------+----------------+----------------------------------+
   | **Item Bytes** | **Field Name** | **Description of Field**         |
   +================+================+==================================+
   | 1              | Item-type      | 54H                              |
   +----------------+----------------+----------------------------------+
   | 2              | Reserved       | This reserved field shall be     |
   |                |                | sent with a value 00H but not    |
   |                |                | tested to this value when        |
   |                |                | received.                        |
   +----------------+----------------+----------------------------------+
   | 3-4            | Item-length    | This Item-length shall be the    |
   |                |                | number of bytes from the first   |
   |                |                | byte of the following field to   |
   |                |                | the last byte of the SCP Role    |
   |                |                | field. It shall be encoded as an |
   |                |                | unsigned binary number.          |
   +----------------+----------------+----------------------------------+
   | 5-6            | UID-length     | This UID-length shall be the     |
   |                |                | number of bytes from the first   |
   |                |                | byte of the following field to   |
   |                |                | the last byte of the             |
   |                |                | SOP-class-uid field. It shall be |
   |                |                | encoded as an unsigned binary    |
   |                |                | number.                          |
   +----------------+----------------+----------------------------------+
   | 7 -xxx         | SOP-class-uid  | This variable field shall        |
   |                |                | contain the SOP Class UID or     |
   |                |                | Meta SOP Class UID that may be   |
   |                |                | used to identify the             |
   |                |                | corresponding Abstract Syntax    |
   |                |                | for which this Sub-Item          |
   |                |                | pertains. It shall be encoded as |
   |                |                | a UID as defined in .            |
   +----------------+----------------+----------------------------------+
   | xxx            | SCU-role       | This byte field shall contain    |
   |                |                | the SCU-role as defined for the  |
   |                |                | Association-requester in         |
   |                |                | `SCP/SCU Role Selection          |
   |                |                | Negotiation <#sect_D.3.3.4>`__.  |
   |                |                | It shall be encoded as an        |
   |                |                | unsigned binary and shall use    |
   |                |                | one of the following values:     |
   |                |                |                                  |
   |                |                | 0 - non support of the SCU role  |
   |                |                |                                  |
   |                |                | 1 - support of the SCU role      |
   +----------------+----------------+----------------------------------+
   | xxx            | SCP-role       | This byte field shall contain    |
   |                |                | the SCP-role as defined for the  |
   |                |                | Association-requester in         |
   |                |                | `SCP/SCU Role Selection          |
   |                |                | Negotiation <#sect_D.3.3.4>`__.  |
   |                |                | It shall be encoded as an        |
   |                |                | unsigned binary and shall use    |
   |                |                | one of the following values:     |
   |                |                |                                  |
   |                |                | 0 - non support of the SCP role  |
   |                |                |                                  |
   |                |                | 1 - support of the SCP role.     |
   +----------------+----------------+----------------------------------+

.. _sect_D.3.3.4.2:

SCP/SCU Role Selection Sub-Item Structure (A-ASSOCIATE-AC)
''''''''''''''''''''''''''''''''''''''''''''''''''''''''''

The SCP/SCU Role Selection Sub-Item shall be made of a sequence of
mandatory fields. This Sub-Item is optional and if supported, one or
more SCP/SCU Role Selection Sub-Items may be present in the User Data
Item of the A-ASSOCIATE-AC. `table_title <#table_D.3-10>`__ shows the
sequence of the mandatory fields.

.. table:: SCP/SCU Role Selection Sub-Item Fields (A-ASSOCIATE-AC)

   +----------------+----------------+----------------------------------+
   | **Item Bytes** | **Field Name** | **Description of Field**         |
   +================+================+==================================+
   | 1              | Item-type      | 54H                              |
   +----------------+----------------+----------------------------------+
   | 2              | Reserved       | This reserved field shall be     |
   |                |                | sent with a value 00H but not    |
   |                |                | tested to this value when        |
   |                |                | received.                        |
   +----------------+----------------+----------------------------------+
   | 3-4            | Item-length    | This Item-length shall be the    |
   |                |                | number of bytes from the first   |
   |                |                | byte of the following field to   |
   |                |                | the last byte of the SCP Role    |
   |                |                | field. It shall be encoded as an |
   |                |                | unsigned binary number.          |
   +----------------+----------------+----------------------------------+
   | 5-6            | UID-length     | This UID-length shall be the     |
   |                |                | number of bytes from the first   |
   |                |                | byte of the following field to   |
   |                |                | the last byte of the             |
   |                |                | SOP-class-uid field. It shall be |
   |                |                | encoded as an unsigned binary    |
   |                |                | number.                          |
   +----------------+----------------+----------------------------------+
   | 7-xxx          | SOP-class-uid  | This variable field shall        |
   |                |                | contain the SOP Class UID or     |
   |                |                | Meta SOP Class UID that may be   |
   |                |                | used to identify the             |
   |                |                | corresponding Abstract Syntax    |
   |                |                | for which this Sub-Item          |
   |                |                | pertains. It shall be encoded as |
   |                |                | a UID as defined in .            |
   +----------------+----------------+----------------------------------+
   | xxx            | SCU-role       | This byte field shall contain    |
   |                |                | the SCU-role as defined in       |
   |                |                | `SCP/SCU Role Selection          |
   |                |                | Negotiation <#sect_D.3.3.4>`__.  |
   |                |                | It shall be encoded as an        |
   |                |                | unsigned binary and shall use    |
   |                |                | one of the following values:     |
   |                |                |                                  |
   |                |                | 0 - The Association-acceptor     |
   |                |                | rejects the                      |
   |                |                | Association-requester's proposal |
   |                |                | of the SCU role selection        |
   |                |                |                                  |
   |                |                | 1 - The Association-acceptor     |
   |                |                | accepts the                      |
   |                |                | Association-requester's proposal |
   |                |                | of the SCU role selection        |
   +----------------+----------------+----------------------------------+
   | xxx            | SCP-role       | This byte field shall contain    |
   |                |                | the SCP-role as defined for the  |
   |                |                | Association-acceptor in `SCP/SCU |
   |                |                | Role Selection                   |
   |                |                | Negotiation <#sect_D.3.3.4>`__.  |
   |                |                | It shall be encoded as an        |
   |                |                | unsigned binary and shall use    |
   |                |                | one of the following values:     |
   |                |                |                                  |
   |                |                | 0 - The Association-acceptor     |
   |                |                | rejects the                      |
   |                |                | Association-requester's proposal |
   |                |                | of the SCP role selection        |
   |                |                |                                  |
   |                |                | 1 - The Association-acceptor     |
   |                |                | accepts the                      |
   |                |                | Association-requester's proposal |
   |                |                | of the SCP role selection        |
   +----------------+----------------+----------------------------------+

.. _sect_D.3.3.5:

Service-Object Pair (SOP) Class Extended Negotiation
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

The SOP Class Extended Negotiation allows, at Association establishment,
peer DICOM AEs to exchange application information defined by specific
Service Class specifications. This is an optional feature that various
Service Classes may or may not choose to support.

Each Service Class specification is required to document, as part of its
SOP Class or Meta SOP Class, the application information it supports and
how this information is negotiated between SCUs and SCPs. Service Class
specifications shall specify, for both the SCU and SCP roles, the
following:

-  semantics of the application information (including the negotiation
   rules)

-  encoding of the application information

-  conditions for which the application information is mandatory and/or
   optional

-  default conditions of the application information

.. note::

   The use of the SOP Class Extended Negotiation is not limited to
   Service Classes defined by this Standard. It may also be used for
   privately defined Service Classes.

The Association-requester may only offer one SOP Class Extended
Negotiation Sub-Item for each SOP Class UID or Meta SOP Class that is
present in the A-ASSOCIATE request.

If the SOP Class Extended Negotiation Sub-Items do not exist in the
A-ASSOCIATE indication they shall be omitted in the A-ASSOCIATE
response.

.. _sect_D.3.3.5.1:

SOP Class Extended Negotiation Sub-Item Structure (A-ASSOCIATE-RQ)
''''''''''''''''''''''''''''''''''''''''''''''''''''''''''''''''''

The SOP Class Extended Negotiation Sub-Item shall be made of a sequence
of mandatory fields followed by the
Service-class-application-information field (specific for each Service
Class specification). This Sub-Item is required per the specific Service
Class specifications. Multiple SOP Class Extended Negotiation Sub-Items
may be present in the User Data Item of the A-ASSOCIATE-RQ, however,
only one Sub-Item per SOP Class UID shall be present.
`table_title <#table_D.3-11>`__ shows the sequence of mandatory fields.

.. table:: SOP Class Extended Negotiation Sub-Item Fields
(A-ASSOCIATE-RQ and A-ASSOCIATE-AC)

   +----------------+-------------------------+-------------------------+
   | **Item Bytes** | **Field Name**          | **Description of        |
   |                |                         | Field**                 |
   +================+=========================+=========================+
   | 1              | Item-type               | 56H                     |
   +----------------+-------------------------+-------------------------+
   | 2              | Reserved                | This reserved field     |
   |                |                         | shall be sent with a    |
   |                |                         | value 00H but not       |
   |                |                         | tested to this value    |
   |                |                         | when received.          |
   +----------------+-------------------------+-------------------------+
   | 3-4            | Item-Length             | This Item-length shall  |
   |                |                         | be the number of bytes  |
   |                |                         | from the first byte of  |
   |                |                         | the following field to  |
   |                |                         | the last byte of the    |
   |                |                         | Service-class-          |
   |                |                         | application-information |
   |                |                         | field. It shall be      |
   |                |                         | encoded as an unsigned  |
   |                |                         | binary number.          |
   +----------------+-------------------------+-------------------------+
   | 5-6            | SOP-class-uid-length    | The                     |
   |                |                         | SOP-class-uid-length    |
   |                |                         | shall be the number of  |
   |                |                         | bytes from the first    |
   |                |                         | byte of the following   |
   |                |                         | field to the last byte  |
   |                |                         | of the SOP-class-uid    |
   |                |                         | field. It shall be      |
   |                |                         | encoded as an unsigned  |
   |                |                         | binary number.          |
   +----------------+-------------------------+-------------------------+
   | 7-xxx          | SOP-class-uid           | The SOP Class or Meta   |
   |                |                         | SOP Class identifier    |
   |                |                         | encoded as a UID as     |
   |                |                         | defined in .            |
   +----------------+-------------------------+-------------------------+
   | xxx-xxx        | Service-class-          | This field shall        |
   |                | application-information | contain the application |
   |                |                         | information specific to |
   |                |                         | the Service Class       |
   |                |                         | specification           |
   |                |                         | identified by the       |
   |                |                         | SOP-class-uid. The      |
   |                |                         | semantics and value of  |
   |                |                         | this field is defined   |
   |                |                         | in the identified       |
   |                |                         | Service Class           |
   |                |                         | specification.          |
   +----------------+-------------------------+-------------------------+

.. _sect_D.3.3.5.2:

SOP Class Extended Negotiation Sub-Item Structure (A-ASSOCIATE-AC)
''''''''''''''''''''''''''''''''''''''''''''''''''''''''''''''''''

The SOP Class Extended Negotiation Sub-Item shall be made of a sequence
of mandatory fields followed by the
Service-class-application-information field (specific for each Service
Class specification). This Sub-Item is required per the specific Service
Class specifications. Multiple SOP Class Extended Negotiation Sub-Items
may be present in the User Data Item of the A-ASSOCIATE-AC, however,
only one Sub-Item per SOP Class UID shall be present.
`table_title <#table_D.3-11>`__ shows the sequence of mandatory fields.

.. _sect_D.3.3.6:

Service-Object Pair (SOP) Class Common Extended Negotiation
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

The SOP Class Common Extended Negotiation allows, at Association
establishment, peer DICOM AEs to exchange application information, the
form of which is generic, and not specific to individual Service
Classes, as compared to the information defined in D.3.3.5. This is an
optional feature that Association-requesters and Association-acceptors
may or may not choose to support.

The information included for each SOP Class for which a sub-item is
present consists of a Service Class UID and (optionally) a Related
General SOP Class UID.

The Service Class UID conveys the Service Class of the SOP Class.

.. note::

   Explicit conveyance of the Service Class may allow the selection of
   the proper format for the Service-class-application-information of
   the SOP Class Extended Negotiation Sub-Item.

The Related General SOP Class UID conveys zero or more Related General
SOP Class for the SOP Class.

.. note::

   1. Consider the example of negotiation of support for a Procedure Log
      Storage SOP Class. That SOP Class is of the Storage Service Class.
      The encoding of the IOD would be compatible with the more general
      Enhanced SR Storage SOP Class. Therefore, the following common
      extended negotiation sub-item could optionally be included:

      -  SOP Class UID: 1.2.840.10008.5.1.4.1.1.88.40 Procedure Log

      -  Service Class UID: 1.2.840.10008.4.2 Storage Service Class

      -  Related General SOP Class UID: 1.2.840.10008.5.1.4.1.1.88.22
         Enhanced SR

   2. The Related SOP Class may be absent, though the Service Class may
      still be included. For example, there may be a new image storage
      SOP Class without a Related SOP Class defined in , yet it is still
      useful to an Association-acceptor to be informed that the new SOP
      Class is of the Storage Service Class:

      -  SOP Class UID: 1.2.840.10008.5.1.4.1.1.7.1 MF Single Bit SC
         Image Storage

      -  Service Class UID: 1.2.840.10008.4.2 Storage Service Class

      -  Related General SOP Class UID: (none)

The Association-requester may only offer one SOP Class Common Extended
Negotiation Sub-Item for each SOP Class UID that is present in the
A-ASSOCIATE request.

No response is necessary, hence the SOP Class Common Extended
Negotiation Sub-Items shall be omitted in the A-ASSOCIATE response.

.. _sect_D.3.3.6.1:

SOP Class Common Extended Negotiation Sub-Item Structure (A-ASSOCIATE-RQ)
'''''''''''''''''''''''''''''''''''''''''''''''''''''''''''''''''''''''''

The SOP Class Common Extended Negotiation Sub-Item shall be made of a
sequence of mandatory fields, the last two of which may be zero-length.
Multiple SOP Class Common Extended Negotiation Sub-Items may be present
in the User Data Item of the A-ASSOCIATE-RQ, however, only one Sub-Item
per SOP Class UID shall be present. `table_title <#table_D.3-12>`__
shows the sequence of mandatory fields.

.. table:: SOP Class Common Extended Negotiation Sub-Item Fields
(A-ASSOCIATE-RQ)

   +----------------+-------------------------+-------------------------+
   | **Item Bytes** | **Field Name**          | **Description of        |
   |                |                         | Field**                 |
   +================+=========================+=========================+
   | 1              | Item-type               | 57H                     |
   +----------------+-------------------------+-------------------------+
   | 2              | Sub-Item-version        | This field indicates    |
   |                |                         | the version of the      |
   |                |                         | Sub-Item. Fields added  |
   |                |                         | to the Sub-Item         |
   |                |                         | definition in           |
   |                |                         | succeeding editions of  |
   |                |                         | the Standard will not   |
   |                |                         | affect the semantics of |
   |                |                         | previously defined      |
   |                |                         | fields. The version of  |
   |                |                         | the Sub-Item defined in |
   |                |                         | this edition of the     |
   |                |                         | Standard is 0.          |
   +----------------+-------------------------+-------------------------+
   | 3-4            | Item-Length             | This Item-length shall  |
   |                |                         | be the number of bytes  |
   |                |                         | from the first byte of  |
   |                |                         | the following field to  |
   |                |                         | the last byte of the    |
   |                |                         | Reserved field. It      |
   |                |                         | shall be encoded as an  |
   |                |                         | unsigned binary number. |
   +----------------+-------------------------+-------------------------+
   | 5-6            | SOP-class-uid-length    | The                     |
   |                |                         | SOP-class-uid-length    |
   |                |                         | shall be the number of  |
   |                |                         | bytes in the            |
   |                |                         | SOP-class-uid field. It |
   |                |                         | shall be encoded as an  |
   |                |                         | unsigned binary number. |
   +----------------+-------------------------+-------------------------+
   | 7-x            | SOP-class-uid           | The SOP Class           |
   |                |                         | identifier encoded as a |
   |                |                         | UID as defined in .     |
   +----------------+-------------------------+-------------------------+
   | (x+1) - (x+2)  | S                       | The                     |
   |                | ervice-class-uid-length | S                       |
   |                |                         | ervice-class-uid-length |
   |                |                         | shall be the number of  |
   |                |                         | bytes in the            |
   |                |                         | Service-class-uid       |
   |                |                         | field. It shall be      |
   |                |                         | encoded as an unsigned  |
   |                |                         | binary number.          |
   +----------------+-------------------------+-------------------------+
   | (x+3) - y      | Service-class-uid       | The Service Class       |
   |                |                         | identifier encoded as a |
   |                |                         | UID as defined in .     |
   +----------------+-------------------------+-------------------------+
   | (y+1) - (y+2)  | R                       | The                     |
   |                | elated-general-sop-clas | R                       |
   |                | s-identification-length | elated-general-sop-clas |
   |                |                         | s-identification-length |
   |                |                         | shall be the number of  |
   |                |                         | bytes in the            |
   |                |                         | Related-general-s       |
   |                |                         | op-class-identification |
   |                |                         | field. Shall be zero if |
   |                |                         | no Related General SOP  |
   |                |                         | Classes are identified. |
   +----------------+-------------------------+-------------------------+
   | (y+3) - z      | Related-general-s       | The                     |
   |                | op-class-identification | Related-general-s       |
   |                |                         | op-class-identification |
   |                |                         | is a sequence of pairs  |
   |                |                         | of length and UID       |
   |                |                         | sub-fields. Each pair   |
   |                |                         | of sub-fields shall be  |
   |                |                         | formatted in accordance |
   |                |                         | with                    |
   |                |                         | `table_t                |
   |                |                         | itle <#table_D.3-13>`__ |
   +----------------+-------------------------+-------------------------+
   | (z+1) - k      | Reserved                | Reserved for additional |
   |                |                         | fields of the sub-item. |
   |                |                         | Shall be zero-length    |
   |                |                         | for Version 0 of        |
   |                |                         | Sub-Item definition.    |
   +----------------+-------------------------+-------------------------+

.. table:: Related-General-SOP-Class-Identification Sub-Fields

   +-----------+---------------------------+---------------------------+
   | **Bytes** | **Sub-Field Name**        | **Description of          |
   |           |                           | Sub-Field**               |
   +===========+===========================+===========================+
   | 1-2       | Related-gen               | The                       |
   |           | eral-sop-class-uid-length | Related-gen               |
   |           |                           | eral-sop-class-uid-length |
   |           |                           | shall be the number of    |
   |           |                           | bytes in the              |
   |           |                           | Rela                      |
   |           |                           | ted-general-sop-class-uid |
   |           |                           | sub-field. It shall be    |
   |           |                           | encoded as an unsigned    |
   |           |                           | binary number.            |
   +-----------+---------------------------+---------------------------+
   | 3-n       | Rela                      | The Related General SOP   |
   |           | ted-general-sop-class-uid | Class identifier encoded  |
   |           |                           | as a UID as defined in .  |
   +-----------+---------------------------+---------------------------+

.. _sect_D.3.3.7:

User Identity Negotiation
^^^^^^^^^^^^^^^^^^^^^^^^^

The User Identity Negotiation is used to notify the association acceptor
of the user identity of the association requestor. It may also request
that the association acceptor respond with the server identity. This
negotiation is optional. If this sub-item is not present in the
A-ASSOCIATE request the A-ASSOCIATE response shall not contain a user
identity response sub-item.

The Association-requester conveys in the A-ASSOCIATE request:

-  the form of user identity being provided, either a username, username
   and passcode, a Kerberos service ticket, a SAML assertion, or a JSON
   Web Token (JWT).

-  an indication whether a positive server response is requested.

The Association-acceptor does not provide an A-ASSOCIATE response unless
a positive response is requested and user authentication succeeded. If a
positive response was requested, the A-ASSOCIATE response shall contain
a User Identity sub-item. If a Kerberos ticket is used the response
shall include a Kerberos server ticket.

Since a system may ignore request sub-items, the positive response must
be requested if the association requestor requires confirmation. If the
association acceptor does not support user identification it will accept
the association without making a positive response. The association
requestor can then decide whether to proceed.

The association acceptor may utilize the User Identity information
provided during the association negotiation to populate the user
information fields in DICOM audit trail messages. The association
acceptor may utilize the User Identity information provided during the
association negotiation to perform authorization controls during the
performance of other DIMSE transactions on the same association. The
user identity information may also be used to modify the performance of
DIMSE transactions for other purposes, such as workflow optimizations.

.. note::

   1. User identity authorization controls may be simple
      "allow/disallow" rules, or they can be more complex scoping rules.
      For example, a query could be constrained to apply only to return
      information about patients that are associated with the identified
      user. The issues surrounding authorization controls can become
      very complex. The User Identity SOP conveys user identity to
      support uses such as authorization controls and audit controls. It
      does not specify their behavior.

   2. The option to include a passcode along with the user identity
      enables a variety of non-Kerberos secure interfaces. Sending
      passwords in the clear is insecure, but there are single use
      password systems such as RFC-2289 and the various smart tokens
      that do not require protection. The password might also be
      protected by TLS or other mechanisms.

   3. For JSON Web Tokens (JWTs), RFC 7519 specifies minimal
      requirements for encryption, MAC and signature algorithms; others
      may be supported as described in the DICOM Conformance Statement.
      The encoded format in the Primary-field of the A-ASSOCIATE-RQ is
      the same as what might be included in an HTTP Authorization:
      Bearer header field per RFC 6750 when accessing a Protected
      Resource on a Resource Server, to facilitate bridging between and
      implementations.

.. _sect_D.3.3.7.1:

User Identity Sub-Item Structure (A-ASSOCIATE-RQ)
'''''''''''''''''''''''''''''''''''''''''''''''''

The User Identity Negotiation Sub-Item shall be made of a sequence of
mandatory fixed and variable length fields. This Sub-Item is optional
and if supported, only one User Identity Negotiation Sub-Item shall be
present in the User Data Item of the A-ASSOCIATE-RQ.
`table_title <#table_D.3-14>`__ shows the sequence of the mandatory
fields.

.. table:: User Identity Negotiation Sub-Item Fields (A-ASSOCIATE-RQ)

   +----------------+-------------------------+-------------------------+
   | **Item Bytes** | **Field Name**          | **Description of        |
   |                |                         | Field**                 |
   +================+=========================+=========================+
   | 1              | Item-type               | 58H                     |
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
   |                |                         | last field sent. It     |
   |                |                         | shall be encoded as an  |
   |                |                         | unsigned binary number. |
   +----------------+-------------------------+-------------------------+
   | 5              | User-Identity-Type      | Field value shall be in |
   |                |                         | the range 1 to 4 with   |
   |                |                         | the following meanings: |
   |                |                         |                         |
   |                |                         | 1 - Username as a       |
   |                |                         | string in UTF-8         |
   |                |                         |                         |
   |                |                         | 2 - Username as a       |
   |                |                         | string in UTF-8 and     |
   |                |                         | passcode                |
   |                |                         |                         |
   |                |                         | 3 - Kerberos Service    |
   |                |                         | ticket                  |
   |                |                         |                         |
   |                |                         | 4 - SAML Assertion      |
   |                |                         |                         |
   |                |                         | 5 - JSON Web Token      |
   |                |                         | (JWT)                   |
   |                |                         |                         |
   |                |                         | Other values are        |
   |                |                         | reserved for future     |
   |                |                         | standardization.        |
   +----------------+-------------------------+-------------------------+
   | 6              | Posi                    | Field value:            |
   |                | tive-response-requested |                         |
   |                |                         | 0 - no response         |
   |                |                         | requested               |
   |                |                         |                         |
   |                |                         | 1 - positive response   |
   |                |                         | requested               |
   +----------------+-------------------------+-------------------------+
   | 7-8            | Primary-field-length    | The                     |
   |                |                         | User-Identity-Length    |
   |                |                         | shall contain the       |
   |                |                         | length of the           |
   |                |                         | User-Identity value.    |
   +----------------+-------------------------+-------------------------+
   | 9-n            | Primary-field           | This field shall convey |
   |                |                         | the user identity,      |
   |                |                         | either the username as  |
   |                |                         | a series of characters, |
   |                |                         | or the Kerberos Service |
   |                |                         | ticket encoded in       |
   |                |                         | accordance with         |
   |                |                         | RFC-1510, or the JWT    |
   |                |                         | encoded in accordance   |
   |                |                         | with RFC 7519 using     |
   |                |                         | base64url encoded       |
   |                |                         | parts.                  |
   +----------------+-------------------------+-------------------------+
   | n+1-n+2        | Secondary-field-length  | This field shall be     |
   |                |                         | non-zero only if        |
   |                |                         | User-Identity-Type has  |
   |                |                         | the value 2. It shall   |
   |                |                         | contain the length of   |
   |                |                         | the secondary-field.    |
   +----------------+-------------------------+-------------------------+
   | n+3-m          | Secondary-field         | This field shall be     |
   |                |                         | present only if         |
   |                |                         | User-Identity-Type has  |
   |                |                         | the value 2. It shall   |
   |                |                         | contain the Passcode    |
   |                |                         | value.                  |
   +----------------+-------------------------+-------------------------+

.. _sect_D.3.3.7.2:

User Identity Sub-Item Structure (A-ASSOCIATE-AC)
'''''''''''''''''''''''''''''''''''''''''''''''''

The User Identity Sub-Item shall be made of a sequence of mandatory
fixed and variable length fields. This Sub-Item is optional and if
supported, only one User Identity Sub-Item shall be present in the User
Data Item of the A-ASSOCIATE-AC. `table_title <#table_D.3-15>`__ shows
the sequence of the mandatory fields.

.. table:: User Identity Negotiation Sub-Item Fields (A-ASSOCIATE-AC)

   +----------------+------------------------+-------------------------+
   | **Item Bytes** | **Field Name**         | **Description of        |
   |                |                        | Field**                 |
   +================+========================+=========================+
   | 1              | Item-type              | 59H                     |
   +----------------+------------------------+-------------------------+
   | 2              | Reserved               | This reserved field     |
   |                |                        | shall be sent with a    |
   |                |                        | value 00H but not       |
   |                |                        | tested to this value    |
   |                |                        | when received.          |
   +----------------+------------------------+-------------------------+
   | 3-4            | Item-length            | This Item-length shall  |
   |                |                        | be the number of bytes  |
   |                |                        | from the first byte of  |
   |                |                        | the following field to  |
   |                |                        | the last byte of the    |
   |                |                        | final field. It shall   |
   |                |                        | be encoded as an        |
   |                |                        | unsigned binary number. |
   +----------------+------------------------+-------------------------+
   | 5-6            | Server-response-length | This field shall        |
   |                |                        | contain the number of   |
   |                |                        | bytes in the            |
   |                |                        | Server-response. May be |
   |                |                        | zero.                   |
   +----------------+------------------------+-------------------------+
   | 7-n            | Server-response        | This field shall        |
   |                |                        | contain the Kerberos    |
   |                |                        | Server ticket, encoded  |
   |                |                        | in accordance with      |
   |                |                        | RFC-1510, if the        |
   |                |                        | User-Identity-Type      |
   |                |                        | value in the            |
   |                |                        | A-ASSOCIATE-RQ was 3.   |
   |                |                        | This field shall        |
   |                |                        | contain the SAML        |
   |                |                        | response if the         |
   |                |                        | User-Identity-Type      |
   |                |                        | value in the            |
   |                |                        | A-ASSOCIATE-RQ was 4.   |
   |                |                        | This field shall be     |
   |                |                        | zero length if the      |
   |                |                        | value of the            |
   |                |                        | User-Identity-Type in   |
   |                |                        | the A-ASSOCIATE-RQ was  |
   |                |                        | 1 or 2.                 |
   +----------------+------------------------+-------------------------+

If the Association-Requestor has requested a positive acknowledgment,
the Server-response shall be returned with the Kerberos Server ticket
when User-Identity-Type is Kerberos Service ticket (3).

.. _sect_D.3.3.7.3:

User Identity Rejection
'''''''''''''''''''''''

The association acceptor may utilize the username or username and
passcode information to determine whether the user is permitted to
establish an association. If the Kerberos mechanism is chosen, the
association acceptor shall utilize the Kerberos service ticket to
determine whether the user is permitted to establish an association.

If the association acceptor rejects the association because of an
authorization failure, the rejection shall be indicated to be
rejected-permanent (see ). The source shall be value (2) "DICOM UL
service provided (ACSE related function) ". The rejection is indicated
to be rejected-permanent because retries with the same user identity
fields will continue to be rejected. A different and valid username,
username and passcode, or Kerberos ticket must be provided.

This Standard does not define how the association acceptor performs
authentication or what rules apply to this authentication.

