.. _chapter_S:

Legacy Transition For Configuration Management (Informative)
============================================================

There will usually be a period of time where a network will have some
applications that utilize the configuration management protocols
coexisting with applications that are only manually configured. The
transition issues arise when a legacy Association Requester interacts
with a managed Association Acceptor or when a managed Association
Requester interacts with a legacy Association Acceptor. Some of these
issues also arise when the Association Requester and Association
Acceptor support different configuration management profiles. These are
discussed below and some general recommendations made for techniques
that simplify the transition to a fully configuration managed network.

.. _sect_S.1:

Legacy Association Requester, Configuration Managed Association Acceptor
------------------------------------------------------------------------

The legacy Association Requester requires that the IP address of the
Association Acceptor not change dynamically because it lacks the ability
to utilize DNS to obtain the current IP address of the Association
Acceptor. The legacy Association Requester also requires that the AE
Title of the Association Acceptor be provided manually.

.. _sect_S.1.1:

DHCP Server
~~~~~~~~~~~

The DHCP server should be configurable with a database of hostname, IP,
and MAC address relationships. The DHCP server can be configured to
provide the same IP address every time that a particular machine
requests an IP address. This is a common requirement for Association
Acceptors that obtain IP addresses from DHCP. The Association Acceptor
may be identified by either the hardware MAC address or the hostname
requested by the Association Acceptor.

The IP address can be permanently assigned as a static IP address so
that legacy Association Requester can be configured to use that IP
address while managed Association Requester can utilize the DNS services
to obtain its IP address.

.. _sect_S.1.2:

DNS Server
~~~~~~~~~~

No specific actions are needed, although see below for the potential
that the DHCP server does not perform DDNS updates.

.. _sect_S.1.3:

LDAP Server
~~~~~~~~~~~

Although the managed Association Acceptor may obtain information from
the LDAP server, the legacy Association Requester will not. This means
that the legacy mechanisms for establishing EYE-Titles and related
information on the Association Requester will need to be coordinated
manually. Most LDAP products have suitable GUI mechanisms for examining
and updating the LDAP database. These are not specified by this
Standard.

An LDAP entry for the Association Requester should be manually created,
although this may be a very abbreviated entry. It is needed so that the
EYE-Title mechanisms can maintain unique AE Titles. There must be
entries created for each of the AEs on the legacy Association Requester.

The legacy Association Requester will need to be configured based on
manual examination of the LDAP information for the server and using the
legacy procedures for that Association Requester.

.. _sect_S.2:

Managed Association Requester, Legacy Association Acceptor
----------------------------------------------------------

.. _sect_S.2.1:

DHCP Server
~~~~~~~~~~~

The DHCP server may need to be configured with a pre-assigned IP address
for the Association Requester if the legacy Association Acceptor
restricts access by IP addresses. Otherwise no special actions are
needed.

.. _sect_S.2.2:

DNS Server
~~~~~~~~~~

The legacy Association Acceptor hostname and IP address should be
manually placed into the DNS database.

.. _sect_S.2.3:

LDAP Server
~~~~~~~~~~~

The LDAP server should be configured with a full description of the
legacy Association Acceptor, even though the Association Acceptor itself
cannot provide this information. This will need to be done manually,
most likely using GUI tools. The legacy Association Acceptor will need
to be manually configured to match the EYE-Titles and other
configuration information.

.. _sect_S.3:

No DDNS Support
---------------

In the event that the DHCP server or DNS server do not support or permit
DDNS updates, then the DNS server database will need to be manually
configured. Also, because these updates are not occurring, all of the
machines should have fixed pre-assigned IP addresses. This is not
strictly necessary for clients, since they will not have incoming DICOM
connections, but may be needed for other reasons. In practice
maintaining this file is very similar to the maintenance of the older
hostname files. There is still a significant administrative gain because
only the DNS and DHCP configuration files need to be maintained, instead
of maintaining files on each of the servers and clients

.. _sect_S.4:

Partially Managed Devices
-------------------------

It is likely that some devices will support only some of the system
management profiles. A typical example of such partial support is a node
that supports:

a. DHCP Client,

b. DNS Client, and

c. NTP Client

Configurations like this are common because many operating system
platforms provide complete tools for implementing these clients. The
support for LDAP Client requires application support and is often
released on a different cycle than the operating system support. These
devices will still have their DICOM application manually configured, but
will utilize the DHCP, DNS, and NTP services.

.. _sect_S.5:

Adding The First Managed Device to A Legacy Network
---------------------------------------------------

The addition of the first fully managed device to a legacy network
requires both server setup and device setup.

.. _sect_S.5.1:

New Servers Required
~~~~~~~~~~~~~~~~~~~~

The managed node requires that servers be installed or assigned to
provide the following actors:

a. DHCP Server

b. DNS Server

c. NTP Server

d. LDAP Server

These may be existing servers that need only administrative additions,
they may be existing hardware that has new software added, and these may
be one or multiple different systems. DHCP, DNS, and NTP services are
provided by a very wide variety of equipment.

.. _sect_S.5.2:

NTP
~~~

The NTP server location relative to this device should be reviewed to be
sure that it meets the timing requirements of the device. If it is an
NTP client with a time accuracy requirement of approximately 1 second,
almost any NTP server location will be acceptable. For SNTP clients and
devices with high time accuracy requirements, it is possible that an
additional NTP server or network topology adjustment may be needed.

If the NTP server is using secured time information, certificates or
passwords may need to be exchanged.

.. _sect_S.5.3:

Documenting Managed and Unmanaged Nodes (DHCP, DNS, and LDAP)
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

.. _sect_S.5.3.1:

DHCP Documentation
^^^^^^^^^^^^^^^^^^

There are advantages to documenting the unmanaged nodes in the DHCP
database. This is not critical for operations, but it helps avoid
administrative errors. Most DHCP servers support the definition of
pre-allocated static IP addresses. The unmanaged nodes can be documented
by including entries for static IP addresses for the unmanaged nodes.
These nodes will not be using the DHCP server initially, but having
their entries in the DHCP database helps reduce errors and simplifies
gradual transitions. The DHCP database can be used to document the
manually assigned IP addresses in a way that avoids unintentional
duplication.

The managed node must be documented in the DHCP database. The NTP and
DNS server locations must be specified.

If this device is an association acceptor it probably should be assigned
a fixed IP address. Many legacy devices cannot operate properly when
communicating with devices that have dynamically assigned IP addresses.
The legacy device does not utilize the DNS system, so the DDNS updates
that maintain the changing IP address are not available. So most managed
nodes that are association acceptors must be assigned a static IP
address. The DHCP system still provides the IP address to the device
during the boot process, but it is configured to always provide the same
IP address every time. The legacy systems are configured to use that IP
address.

.. _sect_S.5.3.2:

DNS Documentation
^^^^^^^^^^^^^^^^^

Most DNS servers have a database for hostname to IP relationships that
is similar to the DHCP database. The unmanaged devices that will be used
by the managed node must have entries in this database so that machine
IP addresses can be found. It is often convenient to document all of the
hostnames and IP addresses for the network into the DNS database. This
is a fairly routine administrative task and can be done for the entire
network and maintained manually as devices are added, moved, or removed.
There are many administrative tools that expect DNS information about
all network devices, and this makes that information available.

If DDNS updates are being used, the manually maintained portion of the
DNS database must be adjusted to avoid conflicts.

There must be DNS entries provided for every device that will be used by
the managed node.

.. _sect_S.5.3.3:

LDAP Documentation
^^^^^^^^^^^^^^^^^^

The LDAP database should be configured to include device descriptions
for this managed device, and there should be descriptions for the other
devices that this device will communicate with. The first portion is
used by this device during its start up configuration process. The
second portion is used by this device to find the services that it will
use.

The basic structural components of the DICOM information must be present
on the LDAP server so that this device can find the DICOM root and its
own entry. It is a good idea to fully populate the AE Title registry so
that as managed devices are added there are no AE Title conflicts.

.. _sect_S.5.3.4:

Descriptions of Other Devices
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

This device needs to be able to find the association acceptors (usually
SCPs) that it will use during normal operation. These may need to be
manually configured into the LDAP server. Their descriptions can be
highly incomplete if these other devices are not managed devices. Only
enough information is needed to meet the needs of this device. If this
device is manually configured and makes no LDAP queries to find
services, then none of the other device descriptions are needed.

There are some advantages to manually maintaining the LDAP database for
unmanaged devices. This can document the manually assigned AE Titles.
The service and network connection information can be very useful during
network planning and troubleshooting. The database can also be useful
during service operations on unmanaged devices as a documentation aid.
The decision whether to use the LDAP database as a documentation aid
often depends upon the features provided with the LDAP server. If it has
good tools for manually updating the LDAP database and good tools for
querying and reporting, it is often a good investment to create a
manually maintained LDAP database.

.. _sect_S.5.4:

Description of This Device
~~~~~~~~~~~~~~~~~~~~~~~~~~

This device needs its own LDAP entry. This is used during the system
start up process. The LDAP server updates must be performed.

.. _sect_S.6:

Switching A Node From Unmanaged to Managed in A Mixed Network
-------------------------------------------------------------

During the transition period devices will be switched from unmanaged to
managed. This may be done in stages, with the LDAP client transition
being done at a different time than the DHCP, DNS, and NTP client. This
section describes a switch that changes a device from completely
unmanaged to a fully managed device. The device itself may be completely
replaced or simply have a software upgrade. Details of how the device is
switched are not important.

.. _sect_S.6.1:

DHCP and DNS
~~~~~~~~~~~~

If the device was documented as part of an initial full network
documentation process, the entries in the DHCP and DNS databases need to
be checked. If the entry is missing, wrong, or incomplete, it must be
corrected in the DHCP and DNS databases. If the entries are correct,
then no changes are needed to those servers. The device can simply start
using the servers. The only synchronization requirement is that the DHCP
and DNS servers be updated before the device, so these can be scheduled
as convenient.

If the device is going to be dynamically assigned an IP address by the
DHCP server, then the DNS server database should be updated to reflect
that DDNS is now going to be used for this device. This update should
not be made ahead of time. It should be made when the device is updated.

.. _sect_S.6.2:

NTP
~~~

The NTP server location relative to this device should be reviewed to be
sure that it meets the timing requirements of the device. If it is an
NTP client with a time accuracy requirement of approximately 1 second,
almost any NTP server location will be acceptable. For SNTP clients and
devices with high time accuracy requirements, it is possible that an
additional NTP server or network topology adjustment may be needed.

If the NTP server is using secured time information, certificates or
passwords may need to be exchanged.

.. _sect_S.6.3:

Association Acceptors On This Node
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

The association acceptors may be able to simply utilize the
configuration information from the LDAP database, but it is likely that
further configuration will be needed. Unmanaged nodes probably have only
a minimal configuration in the database.

.. _sect_S.6.4:

Association Requesters On Legacy Nodes
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

These will probably remain unchanged. The IP address must be
pre-allocated if there are legacy nodes that cannot support DHCP.

.. _sect_S.6.5:

Association Requesters On Managed Nodes
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

If the previous configuration had already been described in the LDAP
database, the managed nodes can continue to use the LDAP database. The
updated and more detailed entry describing the now managed association
acceptor will be used.

