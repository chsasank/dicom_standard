.. _chapter_7:

Configuration Profiles
======================

Configuration management support is implemented by means of protocols
defined in standards other than the DICOM Standard. These protocols are
described here in terms of actors, transactions, and profiles.

Actors are analogous to the Application Entities used within the DICOM
profile. An actor is a collection of hardware and software processes
that perform a particular role. When a device provides or uses a service
it will include an actor to handle the relevant network activity. DICOM
Configuration actors may co-exist with other Application Entities on a
device. Some DICOM Configuration actors exist as parts of general use IT
equipment. Like the Application Entity, specification of an Actor does
not imply anything about the details of the actual implementation.

The actor interactions are defined in terms of Transactions. Each
transaction is given a name. The transaction may in turn comprise a
variety of activity. All transactions are defined in terms of actors
that are communicating. The relationships between actors in a
transaction may be more complex than the simple SCU and SCP roles in
DICOM activities. When the transaction includes interactions with a
person, the transactions may be implemented by user interfaces,
removable media. and other mechanisms. The person is described in terms
of being an actor from the perspective of the transaction use case
model. More typically the transactions are a series of network
activities that perform a specific operation.

A transaction includes both mandatory and optional components. An Actor
that is implementing a transaction is required to implement all of the
mandatory components.

Some transactions include human actors in the transaction definition.
These actors are not defined as actors elsewhere, nor are they included
in profile descriptions. They exist to specify that some sort of
mechanism must be provided to permit these people to interact with the
computer actor. Other details of how that user interface is provided are
not specified by this Standard. For an example, see the definition of
the Configure DHCP transaction.

Conformance is further managed by means of Profiles. A Profile is
defined in terms of what transactions are required for an actor and what
transactions are optional. An implementation of a specific actor is
documented by specifying what optional transactions and transaction
components have been implemented. An implementation that omits any
required transactions or components cannot claim to be an implementation
of that Actor.

For example, in the Network Address Management Profile the DHCP Server
is required to perform the three Transactions to configure the DHCP
server, find and use DHCP servers, and maintain the DHCP leases. It may
also support the transaction to update the DNS server by means of DDNS
coordination.

A Profile includes definitions for more than one Actor. It specifies the
transactions for all of the actors that cooperate to perform a function.
For example, the Network Address Management Profile covers the DHCP
Server actor, the DHCP client Actor, and the DNS Server actor. There
must be at least one DHCP Server and one DHCP Client for the system to
be useful. The DNS Server itself is optional because the DHCP Server
need not implement the DDNS Coordination transaction. If the DNS Server
is part of the system, the DDNS coordination is required and the DHCP
Server will be expected to participate in the DDNS Coordination
transaction.

.. note::

   There may be a DNS server present on the same network as a DHCP
   Server, but if it is not providing the DNS Server actor from this
   profile it is not part of the DICOM Configuration activities.

The profiles, actors, and transactions are summarized in the following
sections. The detailed description of actor and transactions for each
specific profile are described in annexes for each profile. The
transactions are documented in terms of parameters and terms from their
original standards document, e.g., an RFC for Internet protocols. The
full details of the transaction are not described in the annex, only
particular details that are relevant to the DICOM application of that
transaction. The complete details for these external protocols are
documented in the relevant standards documents for the external
protocols. Compliance with the requirements of a particular profile
shall include compliance with these external protocol documents.

.. _sect_7.1:

Actors
------

**DHCP Server**

The DHCP Server is a computer/software feature that is provided with a
network configuration description, and that provides startup
configuration services in accordance with the DHCP protocol.

**DHCP Client**

The DHCP Client is a software feature that is used to obtain TCP/IP
parameters during the startup of a computer. It continues operation to
maintain validity of these parameters.

**DNS Server**

The DNS server is a computer/software feature that provides IP related
information in response to queries from clients utilizing the DNS
protocol. It is a part of a federated database facility that maintains
the current database relating machine names to IP address information.
The DNS server may also be isolated from the worldwide federated
database and provide only local DNS services.

**DNS Client**

The DNS client as a computer/software feature that utilizes the DNS
protocols to obtain IP information when given hostnames. The hostnames
may be in configuration files or other files instead of explicit IP
addresses. The hostnames are converted into IP addresses dynamically
when necessary. The DNS client uses a DNS server to provide the
necessary information.

**NTP Server**

The NTP server is a computer/software feature that provides time
services in accordance with the NTP or SNTP protocol.

**NTP Client**

The NTP client is software that obtains time information from an NTP
server and maintains the client time in synchronization with the time
signals from the NTP server.

**SNTP Client**

The SNTP client is software that obtains time information from an NTP
server and maintains the client time in approximate synchronization with
time signals from the NTP server. The SNTP client synchronization is not
maintained with the accuracy or precision that NTP provides.

**LDAP Server**

The LDAP server is a computer/ software feature that maintains an
internal database of various directory information. Some of this
directory information corresponds to DICOM Configuration schema. The
LDAP server provides network access to read and update the directory
information. The LDAP server provides a mechanism for external loading,
unloading, and backup of directory information. The LDAP server may be
part of a federated network of servers that provides a coordinated view
of a federated directory database in accordance with the rules of the
LDAP protocols.

**LDAP Client**

The LDAP client utilizes the LDAP protocol to make queries to an LDAP
server. The LDAP server maintains a database and responds to these
queries based on the contents of this database.

.. _sect_7.2:

Transactions
------------

The following transactions are used to provide communications between
actors in accordance with one or more of the DICOM Configuration
protocols.

**Configure DHCP Server**

This transaction changes the configuration on a DHCP server to reflect
additions, deletions, and changes to the IP parameters that have been
established for this network.

**Find and Use DHCP Server**

This transaction is a sequence of network messages that comply with the
rules of the DHCP protocol. It allows a DHCP client to find available
DHCP servers and select the server appropriate for that client. This
transaction obtains the mandatory IP parameter information from the DHCP
server and obtains additional optional parameters from the DHCP server.

**Configure Client**

The service staff uses this transaction to set the initial configuration
for a client.

**Maintain Lease**

This transaction deals with how the DHCP client should behave when its
IP lease is not renewed.

**DDNS Coordination**

This transaction documents whether the DHCP server is coordinating with
a DNS server so that access to the DHCP client can be maintained using
the hostname assigned to the DHCP client.

**Resolve Hostname**

This transaction obtains the IP address for a computer when given a
hostname.

**Maintain Time**

These transactions are the activities needed for an NTP or SNTP client
to maintain time synchronization with a master time service.

**Find NTP Server**

This transaction is the autodiscovery procedure defined for NTP. This
may use either a broadcast method or a DHCP supported method.

**Find LDAP Server**

In this transaction the DNS server is queried to obtain the IP address,
port, and name of the LDAP server.

**Query LDAP Server**

In this transaction the LDAP server is queried regarding contents of the
LDAP database.

**Client Update LDAP Server**

This transaction updates the configuration database using LDAP update
instructions from the client being configured.

**Maintain LDAP Server**

This transaction updates the configuration database using local services
of the LDAP server.

`figure_title <#figure_7-1>`__ shows the actors and their transactions.
The usual device will have an NTP Client, DHCP Client, and LDAP client
in addition to the other applications actors. The transactions
"Configure DHCP Server", "Configure Client", and "Maintain LDAP Server"
are not shown because these transactions are between a software actor
and a human actor. DICOM does not specify the means or user interface.
It only requires that certain capabilities be supported.

