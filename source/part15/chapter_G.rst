.. _chapter_G:

Time Synchronization Profiles
=============================

.. _sect_G.1:

Basic Time Synchronization Profile
----------------------------------

The Basic Time Synchronization Profile defines services to synchronize
the clocks on multiple computers. It employs the Network Time Protocol
(NTP) services that have been used for this purpose by many other
disciplines. NTP permits synchronization to a local server that provides
a local time source, and synchronization to a variety of external time
services. The accuracy and precision controls are not explicitly part of
the protocol. They are determined in large part by the selection of
clock hardware and network topology.

An extensive discussion of implementation strategies for NTP can be
found at http://www.ntp.org.

The Basic Time Synchronization Profile applies to the actors DHCP
Client, DHCP Server, SNTP Client, NTP Client and NTP Server. The
mandatory and optional transactions are described in the table and
sections below.

.. table:: Basic Time Synchronization Profile

   =========== ================ =========== =======
   Actor       Transaction      Optionality Section
   =========== ================ =========== =======
   NTP Server  Maintain Time    M           G.1.2
   \           Find NTP Servers O           G.1.1
   NTP Client  Maintain Time    M           G.1.2
   \           Find NTP Servers O           G.1.1
   SNTP Client Maintain Time    M           G.1.2
   DHCP Server Find NTP Servers O           G.1.1
   DCHP Client Find NTP Servers M           G.1.1
   =========== ================ =========== =======

.. _sect_G.1.1:

Find NTP Servers
~~~~~~~~~~~~~~~~

The optional NTP protocol elements for NTP autoconfiguration and NTP
autodiscovery can significantly simplify installation. The NTP
specification for these is defined such that they are truly optional for
both client and server. In the event that a client cannot find an NTP
server automatically using these services, it can use the DHCP optional
information or manually configured information to find a server. Support
for these services is recommended but not mandatory.

This transaction exists primarily as a means of documenting whether
particular models of equipment support the automatic discovery. This
lets installation and operation plan their DHCP and equipment
installation procedures in advance.

.. _sect_G.1.1.1:

Scope
^^^^^

This applies to any client that needs the correct time, or that needs to
have its time stamps synchronized with those of another system. The
accuracy of synchronization is determined by details of the
configuration and implementation of the network and NTP servers at any
specific site.

Both the NTP and SNTP clients shall utilize the NTP server information
if it is provided by DHCP and NTP services have not been found using
autodiscovery. Manual configuration shall be provided as a backup.
Autodiscovery or DHCP are preferred.

.. _sect_G.1.1.2:

Use Case Roles
^^^^^^^^^^^^^^

DHCP Server
   Provides UTC offset, provides list of NTP servers

DHCP Client
   Receives UTC offset and list of NTP servers

NTP Client
   Maintains client clock

SNTP Client
   Maintains client clock

NTP Servers
   External time servers. These may have connections to other time
   servers, and may be synchronized with national time sources.

.. _sect_G.1.1.3:

Referenced Standards
^^^^^^^^^^^^^^^^^^^^

`biblioentry_title <#biblio_RFC_2030>`__ Simple Network Time Protocol
(SNTP) Version 4

`biblioentry_title <#biblio_RFC_5905>`__ Network Time Protocol Version
4: Protocol and Algorithms Specification

`biblioentry_title <#biblio_RFC_5906>`__ Network Time Protocol Version
4: Autokey Specification

`biblioentry_title <#biblio_RFC_8633>`__ Network Time Protocol Best
Current Practices

.. _sect_G.1.1.4:

Basic Course of Events.
^^^^^^^^^^^^^^^^^^^^^^^

The NTP Client uses a list of NTP Servers, which may be:

-  obtained through optional NTP discovery mechanisms (see
   `biblioentry_title <#biblio_RFC_5905>`__\ Section 3.1),

-  provided by a DHCP Server, see Annex F on DHCP, and/or

-  manually configured.

If the list is not empty, the client shall attempt to maintain time
synchronization with at least one of the NTP servers. The client
synchronization shall be in compliance with either
`biblioentry_title <#biblio_RFC_5905>`__ (NTP) or
`biblioentry_title <#biblio_RFC_2030>`__ (SNTP). If the list is empty,
the client may choose an alternative method of time synchronization.

SNTP provides much lower accuracy than NTP. If time synchronization of
better than 1s mean error is required, the client should use NTP.
`biblioentry_title <#biblio_RFC_5905>`__ and
`biblioentry_title <#biblio_RFC_8633>`__ discuss implementation and
accuracy considerations.

A DHCP server may provide to the DHCP Client a UTC offset between the
local time at the machine and UTC, which the client shall use for
converting between UTC and local time.

.. _sect_G.1.1.5:

Alternative Paths
^^^^^^^^^^^^^^^^^

If there is no UTC offset information from the DHCP or NTP server, then
the UTC offset will be obtained in a device specific manner (e.g.,
service, CMOS, internal battery clock).

.. _sect_G.1.1.6:

Assumptions
^^^^^^^^^^^

The local battery clock time is set to UTC, or the local operating
system has proper support to manage both battery clock time, NTP clock
time, and system clock time. The NTP time is always in UTC.

.. _sect_G.1.1.7:

Postconditions
^^^^^^^^^^^^^^

The client will remain synchronized with its selected time source. In an
environment with one or more NTP servers, this will be good time
synchronization. In the absence of NTP servers, the selected source will
be the internal client clock.

.. _sect_G.1.2:

Maintain Time
~~~~~~~~~~~~~

.. _sect_G.1.2.1:

Scope
^^^^^

This applies to any client that needs the correct time, or that needs to
have its time stamps synchronized with those of another system. The
accuracy of synchronization is determined by details of the
configuration and implementation of the network and NTP servers at any
specific site.

.. _sect_G.1.2.2:

Use Case Roles
^^^^^^^^^^^^^^

NTP/SNTP Client
   Maintains client clock

NTP Servers
   External time servers. These may have connections to other time
   servers, and may be synchronized with national time sources.

.. _sect_G.1.2.3:

Referenced Standards
^^^^^^^^^^^^^^^^^^^^

`biblioentry_title <#biblio_RFC_2030>`__ Simple Network Time Protocol
(SNTP) Version 4

`biblioentry_title <#biblio_RFC_2827>`__ Network Ingress Filtering:
Defeating Denial of Service Attacks which employ IP Source Address
Spoofing

`biblioentry_title <#biblio_RFC_5905>`__ Network Time Protocol Version
4: Protocol and Algorithms Specification

`biblioentry_title <#biblio_RFC_5906>`__ Network Time Protocol Version
4: Autokey Specification

`biblioentry_title <#biblio_RFC_8633>`__ Network Time Protocol Best
Current Practices

.. _sect_G.1.2.4:

Basic Course of Events.
^^^^^^^^^^^^^^^^^^^^^^^

The detail on Maintain Time transactions is described in
`biblioentry_title <#biblio_RFC_5905>`__ and
`biblioentry_title <#biblio_RFC_2030>`__. The most common and the
mandatory minimum mode for NTP operation uses a series of messages
between client and servers. The client sends requests to the servers,
which fill in time related fields in a response, and the client performs
optimal estimation of the present time based on that information. The
RFCs deal with issues of lost messages, estimation formulae, etc. Once
the clocks are in synchronization these message exchanges typically
stabilize at roughly 1000 second intervals.

The client machine uses the time estimate to maintain the internal
operating system clock. This clock is then used by applications that
need time information. This approach eliminates the application visible
difference between synchronized and unsynchronized time. The RFCs
provide guidance on proper implementations.

.. _sect_G.1.3:

NTP Security Considerations (Informative)
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

NTP security considerations (`biblioentry_title <#biblio_RFC_5905>`__
Section 8, `biblioentry_title <#biblio_RFC_5906>`__, and
`biblioentry_title <#biblio_RFC_8633>`__) may be applicable based on
site-specific environment and threat considerations. Locations with NTP
Servers should also consider `biblioentry_title <#biblio_RFC_2827>`__
and implementing access controls on the use of the server.

Security Policies and Procedures for NTP are maintained at
http://www.nwtime.org/security-policy/ as part of the Network Time
Foundation.

.. _sect_G.1.4:

NTP Implementation Considerations (Informative)
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

NTP compliant servers always support both NTP and SNTP clients. The
difference is one of synchronization accuracy, not communications
compatibility. Although in theory both NTP and SNTP clients could run at
the same time on the same system, this is not recommended. The SNTP
updates will simply degrade the time accuracy. When other time protocol
clients, such as IRIG, are also being used, these clients must be
coordinated with the NTP client to avoid synchronization problems.

These and other considerations, such as multiple clock types, accuracy
implications, and configuration alternatives, are documented at
http://www.ntp.org.

.. _sect_G.1.5:

Conformance
~~~~~~~~~~~

The Conformance Statement for the NTP Server and NTP Client shall state
whether secure transactions (`biblioentry_title <#biblio_RFC_5906>`__)
are supported.

The Conformance Statement for the NTP Server shall state whether it is
also an NTP Client.

The Conformance Statement for the NTP Client shall state how it manages
time when no NTP Server is available.

