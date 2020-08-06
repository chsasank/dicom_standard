.. _chapter_R:

Configuration Use Cases (Informative)
=====================================

The following use cases are the basis for the decisions made in defining
the Configuration Management Profiles specified in . Where possible
specific protocols that are commonly used in IT system management are
specifically identified.

.. _sect_R.1:

Install A New Machine
---------------------

When a new machine is added there need to be new entries made for:

a. TCP/IP parameters

b. DICOM Application Entity Related Parameters

The service staff effort needed for either of these should be minimal.
To the extent feasible these parameters should be generated and
installed automatically.

The need for some sort of ID is common to most of the use cases, so it
is assumed that each machine has sufficient non-volatile storage to at
least remember its own name for later use.

Updates may be made directly to the configuration databases or made via
the machine being configured. A common procedure for large networks is
for the initial network design to assign these parameters and create the
initial databases during the complete initial network design. Updates
can be made later as new devices are installed.

One step that specifically needs automation is the allocation of AE
Titles. These must be unique. Their assignment has been a problem with
manual procedures. Possibilities include:

a. Fully automatic allocation of AE Titles as requested. This interacts
   with the need for AE title stability in some use cases. The automatic
   process should permit AE Titles to be persistently associated with
   particular devices and application entities. The automatic process
   should permit the assignment of AE titles that comply with particular
   internal structuring rules.

b. Assisted manual allocation, where the service staff proposes AE
   Titles (perhaps based on examining the list of present AE Titles) and
   the system accepts them as unique or rejects them when non-unique.

These AE Titles can then be associated with the other application entity
related information. This complete set of information needs to be
provided for later uses.

The local setup may also involve searches for other AEs on the network.
For example, it is likely that a search will be made for archives and
printers. These searches might be by SOP class or device type. This is
related to vendor specific application setup procedures, which are
outside the scope of DICOM.

.. _sect_R.1.1:

Configure DHCP
~~~~~~~~~~~~~~

The network may have been designed in advance and the configuration
specified in advance. It should be possible to pre-configure the
configuration servers prior to other hardware installation. This should
not preclude later updates or later configuration at specific devices.

The DHCP servers have a database that is manually maintained defining
the relationship between machine parameters and IP parameters. This
defines:

a. Hardware MAC addresses that are to be allocated specific fixed IP
   information.

b. Client machine names that are to be allocated specific fixed IP
   information.

c. Hardware MAC addresses and address ranges that are to be allocated
   dynamically assigned IP addresses and IP information.

d. Client machine name patterns that are to be allocated dynamically
   assigned IP addresses and IP information.

The IP information that is provided will be a specific IP address
together with other information. The present recommendation is to
provide all of the following information when available.

The manual configuration of DHCP is often assisted by automated user
interface tools that are outside the scope of DICOM. Some people utilize
the DHCP database as a documentation tool for documenting the assignment
of IP addresses that are preset on equipment. This does not interfere
with DHCP operation and can make a gradual transition from equipment
presets to DHCP assignments easier. It also helps avoid accidental
re-use of IP addresses that are already manually assigned. However, DHCP
does not verify that these entries are in fact correct.

.. _sect_R.1.2:

Configure LDAP
~~~~~~~~~~~~~~

There are several ways that the LDAP configuration information can be
obtained.

a. A complete installation may be pre-designed and the full
   configuration loaded into the LDAP server, with the installation
   Attribute set to false. Then as systems are installed, they acquire
   their own configurations from the LDAP server. The site
   administration can set the installation Attribute to true when
   appropriate.

b. When the LDAP server permits network clients to update the
   configuration, they can be individually installed and configured.
   Then after each device is configured, that device uploads its own
   configuration to the LDAP server.

c. When the LDAP server does not permit network clients to update
   configurations, they can be individually installed and configured.
   Then, instead of uploading their own configuration, they create a
   standard format file with their configuration objects. This file is
   then manually added to the LDAP server (complying with local security
   procedures) and any conflicts resolved manually.

.. _sect_R.1.2.1:

Pre-configure
^^^^^^^^^^^^^

The network may have been designed in advance and the configuration
specified in advance. It should be possible to pre-configure the
configuration servers prior to other hardware installation. This should
not preclude later updates or later configuration at specific devices.

LDAP defines a standard file exchange format for transmitting LDAP
database subsets in an ASCII format. This file exchange format can be
created by a variety of network configuration tools. There are also
systems that use XML tools to create database subsets that can be loaded
into LDAP servers. It is out of scope to specify these tools in any
detail. The use case simply requires that such tools be available.

When the LDAP database is pre-configured using these tools, it is the
responsibility of the tools to ensure that the resulting database
entries have unique names. The unique name requirement is common to any
LDAP database and not just to DICOM AE Titles. Consequently, most tools
have mechanisms to ensure that the database updates that they create do
have unique names.

At an appropriate time, the installed Attribute is set on the device
objects in the LDAP configuration.

.. _sect_R.1.2.2:

Updating Configuration During Installation
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

The "unconfigured" device start up begins with use of the pre-configured
services from DHCP, DNS, and NTP. It then performs device configuration
and updates the LDAP database. This description assumes that the device
has been given permission to update the LDAP database directly.

a. DHCP is used to obtain IP related parameters. The DHCP request can
   indicate a desired machine name that DHCP can associate with a
   configuration saved at the DHCP server. DHCP does not guarantee that
   the desired machine name will be granted because it might already be
   in use, but this mechanism is often used to maintain specific machine
   configurations. The DHCP will also update the DNS server (using the
   DDNS mechanisms) with the assigned IP address and hostname
   information. Legacy note: A machine with pre-configured IP addresses,
   DNS servers, and NTP servers may skip this step. As an operational
   and documentation convenience, the DHCP server database may contain
   the description of this pre-configured machine.

b. The list of NTP servers is used to initiate the NTP process for
   obtaining and maintaining the correct time. This is an ongoing
   process that continues for the duration of device activity. See Time
   Synchronization below.

c. The list of DNS servers is used to obtain the address of the DNS
   servers at this site. Then the DNS servers are queried to get the
   list of LDAP servers. This utilizes a relatively new addition to the
   DNS capabilities that permit querying DNS to obtain servers within a
   domain that provide a particular service.

d. The LDAP servers are queried to find the server that provides DICOM
   configuration services, and then obtain a description for the device
   matching the assigned machine name. This description includes device
   specific configuration information and a list of Network AEs. For the
   unconfigured device there will be no configuration found.

   .. note::

      These first four steps are the same as a normal start up
      (described below).

e. Through a device specific process it determines its internal AE
   structure. During initial device installation it is likely that the
   LDAP database lacks information regarding the device. Using some
   vendor specific mechanism, e.g., service procedures, the device
   configuration is obtained. This device configuration includes all the
   information that will be stored in the LDAP database. The fields for
   "device name" and "AE Title" are tentative at this point.

f. Each of the Network AE objects is created by means of the LDAP object
   creation process. It is at this point that LDAP determines whether
   the AE Title is in fact unique among all AE Titles. If the title is
   unique, the creation succeeds. If there is a conflict, the creation
   fails and "name already in use" is given as a reasonless uses
   propose/create as an atomic operation for creating unique items. The
   LDAP approach permits unique titles that comply with algorithms for
   structured names, check digits, etc. DICOM does not require
   structured names, but they are a commonplace requirement for other
   LDAP users. It may take multiple attempts to find an unused name.
   This multiple probe behavior can be a problem if "unconfigured
   device" is a common occurrence and name collisions are common. Name
   collisions can be minimized at the expense of name structure by
   selecting names such as "AExxxxxxxxxxxxxx" where "xxxxxxxxxxxxxx" is
   a truly randomly selected number. The odds of collision are then
   exceedingly small, and a unique name will be found within one or two
   probes.

g. The device object is created. The device information is updated to
   reflect the actual AE titles of the AE objects. As with AE objects,
   there is the potential for device name collisions.

h. The network connection objects are created as subordinates to the
   device object.

i. The AE objects are updated to reflect the names of the network
   connection objects.

The "unconfigured device" now has a saved configuration. The LDAP
database reflects its present configuration.

In the following example, the new system needs two AE Titles. During its
installation another machine is also being installed and takes one of
the two AE Titles that the first machine expected to use. The new system
then claims another different EYE-title that does not conflict.

.. _sect_R.1.2.3:

Configure Client Then Update Server
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

Much of the initial start up is the same for restarting a configured
device and for configuring a client first and then updating the server.
The difference is two-fold.

The AE Title uniqueness must be established manually, and the
configuration information saved at the client onto a file that can then
be provided to the LDAP server. There is a risk that the manually
assigned AE Title is not unique, but this can be managed and is easier
than the present entirely manual process for assigning AE Titles.

.. _sect_R.1.3:

Distributed Update Propagation
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

The larger enterprise networks require prompt database responses and
reliable responses during network disruptions. This implies the use of a
distributed or federated database. These have update propagation issues.
There is not a requirement for a complete and accurate view of the DICOM
network at all times. There is a requirement that local subsets of the
network maintain an accurate local view. E.g., each hospital in a large
hospital chain may tolerate occasional disconnections or problems in
viewing the network information in other hospitals in that chain, but
they require that their own internal network be reliably and accurately
described.

LDAP supports a variety of federation and distribution schemes. It
specifically states that it is designed and appropriate for federated
situations where distribution of updates between federated servers may
be slow. It is specifically designed for situations where database
updates are infrequent and database queries dominate.

.. _sect_R.2:

Legacy Compatibility
--------------------

Legacy devices utilize some internal method for obtaining the IP
addresses, port numbers, and AE Titles of the other devices. For legacy
compatibility, a managed node must be controlled so that the IP
addresses, port numbers, and AE Titles do not change. This affects DHCP
because it is DHCP that assigns IP addresses. The LDAP database design
must preserve port number and AE Title so that once the device is
configured these do not change.

DHCP was designed to deal with some common legacy issues:

a. Documenting legacy devices that do not utilize DHCP. Most DHCP
   servers can document a legacy device with a DHCP entry that describes
   the device. This avoids IP address conflicts. Since this is a manual
   process, there still remains the potential for errors. The DHCP
   server configuration is used to reserve the addresses and document
   how they are used. This documented entry approach is also used for
   complex multi-homed servers. These are often manually configured and
   kept with fixed configurations.

b. Specifying fixed IP addresses for DHCP clients. Many servers have
   clients that are not able to use DNS to obtain server IP addresses.
   These servers may also utilize DHCP for start up configuration. The
   DHCP servers must support the use of fixed IP allocations so that the
   servers are always assigned the same IP address. This avoids
   disrupting access by the server's legacy clients. This usage is quite
   common because it gives the IT administrators the centralized control
   that they need without disrupting operations. It is a frequent
   transitional stage for machines on networks that are transitioning to
   full DHCP operation.

There are two legacy-related issues with time configuration:

a. The NTP system operates in UTC. The device users probably want to
   operate in local time. This introduces additional internal software
   requirements to configure local time. DHCP will provide this
   information if that option is configured into the DHCP server.

b. Device clock setting must be documented correctly. Some systems set
   the battery-powered clock to local time; others use UTC. Incorrect
   settings will introduce very large time transient problems during
   start up. Eventually NTP clients do resolve the huge mismatch between
   battery clock and NTP clock, but the device may already be in medical
   use by the time this problem is resolved. The resulting time
   discontinuity can then pose problems. The magnitude of this problem
   depends on the particular NTP client implementation.

.. _sect_R.3:

Obtain Configuration of Other Devices
-------------------------------------

Managed devices can utilize the LDAP database during their own
installation to establish configuration parameters such as the AE Title
of destination devices. They may also utilize the LDAP database to
obtain this information at run time prior to association negotiation.

.. _sect_R.3.1:

Find AE When Given Device Type
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

The LDAP server supports simple relational queries. This query can be
phrased:

*Return devices where*

*DeviceType == <device type>*

Then, for each of those devices, query

*Return Network AE where*

*[ApplicationCluster == name]*

The result will be the Network AE entries that match those two criteria.
The first criteria selects the device type match. There are LDAP scoping
controls that determine whether the queries search the entire enterprise
or just this server. LDAP does not support complex queries,
transactions, constraints, nesting, etc. LDAP cannot provide the
hostnames for these Network AEs as part of a single query. Instead, the
returned Network AEs will include the names of the network connections
for each Network AE. Then the application would need to issue LDAP reads
using the DN of the NetworkConnection objects to obtain the hostnames.

.. _sect_R.4:

Device Start up
---------------

Normal start up of an already configured device will obtain IP
information and DICOM information from the servers.

The device start up sequence is:

a. DHCP is used to obtain IP related parameters. The DHCP request can
   indicate a desired machine name that DHCP can associate with a
   configuration saved at the DHCP server. DHCP does not guarantee that
   the desired machine name will be granted because it might already be
   in use, but this mechanism is often used to maintain specific machine
   configurations. The DHCP will also update the DNS server (using the
   DDNS mechanisms) with the assigned IP address and hostname
   information. Legacy note: A machine with pre-configured IP addresses,
   DNS servers, and NTP servers may skip this step. As an operational
   and documentation convenience, the DHCP server database may contain
   the description of this pre-configured machine.

b. The list of NTP servers is used to initiate the NTP process for
   obtaining and maintaining the correct time. This is an ongoing
   process that continues for the duration of device activity. See Time
   Synchronization below.

c. The list of DNS servers is used to obtain the list of LDAP servers.
   This utilizes a relatively new addition to the DNS capabilities that
   permit querying DNS to obtain servers within a domain that provide a
   particular service.

d. The "nearest" LDAP server is queried to obtain a description for the
   device matching the assigned machine name. This description includes
   device specific configuration information and a list of Network AEs.

   .. note::

      A partially managed node may reach this point and discover that
      there is no description for that device in the LDAP database.
      During installation (as described above) this may then proceed
      into device configuration. Partially managed devices may utilize
      an internal configuration mechanism.

e. The AE descriptions are obtained from the LDAP server. Key
   information in the AE description is the assigned AE Title. The AE
   descriptions probably include vendor unique information in either the
   vendor text field or vendor extensions to the AE object. The details
   of this information are vendor unique. DICOM is defining a mandatory
   minimum capability because this will be a common need for vendors
   that offer dynamically configurable devices. The AE description may
   be present even for devices that do not support dynamic
   configuration. If the device has been configured with an AE Title and
   description that is intended to be fixed, then a description should
   be present in the LDAP database. The device can confirm that the
   description matches its stored configuration. The presence of the AE
   Title in the description will prevent later network activities from
   inadvertently re-using the same AE Title for another purpose. The
   degree of configurability may also vary. Many simple devices may only
   permit dynamic configuration of the IP address and AE Title, with all
   other configuration requiring local service modifications.

f. The device performs whatever internal operations are involved to
   configure itself to match the device description and AE descriptions.

At this point, the device is ready for regular operation, the DNS
servers will correctly report its IP address when requested, and the
LDAP server has a correct description of the device, Network AEs, and
network connections.

.. _sect_R.5:

Shutdown
--------

.. _sect_R.5.1:

Shutdown
~~~~~~~~

The lease timeouts eventually release the IP address at DHCP, which can
then update DNS to indicate that the host is down. Clients that utilize
the hostname information in the LDAP database will initially experience
reports of connection failure; and then after DNS is updated, they will
get errors indicating the device is down when they attempt to use it.
Clients that use the IP entry directly will experience reports of
connection failure.

.. _sect_R.5.2:

Online/offline
~~~~~~~~~~~~~~

A device may be deliberately placed offline in the LDAP database to
indicate that it is unavailable and will remain unavailable for an
extended period of time. This may be utilized during system installation
so that pre-configured systems can be marked as offline until the system
installation is complete. It can also be used for systems that are down
for extended maintenance or upgrades. It may be useful for equipment
that is on mobile vans and only present for certain days.

For this purpose a separate Installed Attribute has been given to
devices, Network AEs, and Network Connections so that it can be manually
managed.

.. _sect_R.6:

Time Synchronization
--------------------

Medical device time requirements primarily deal with synchronization of
machines on a local network or campus. There are very few requirements
for accurate time (synchronized with an international reference clock).
DICOM time users are usually concerned with:

a. local time synchronization between machines

b. local time base stability. This means controlling the discontinuities
   in the local time and its first derivative. There is also an upper
   bound on time base stability errors that results from the
   synchronization error limits.

c. international time synchronization with the UTC master clocks

Other master clocks and time references (e.g., sidereal time) are not
relevant to medical users.

.. _sect_R.6.1:

High Accuracy Time Synchronization
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

High accuracy time synchronization is needed for devices like cardiology
equipment. The measurements taken on various different machines are
recorded with synchronization modules specifying the precise time base
for measurements such as waveforms and Multi-frame Images. These are
later used to synchronize data for analysis and display.

Typical requirements are:

**Local synchronization**

Synchronized to within approximately 10 millisecond. This corresponds to
a few percent of a typical heartbeat. Under some circumstances, the
requirements may be stricter than this.

**Time base stability**

During the measurement period there should be no discontinuities greater
than a few milliseconds. The time base rate should be within 0.01% of
standard time rate.

**International Time Synchronization**

There are no special extra requirements. Note however that time base
stability conflicts with time synchronization when UTC time jumps (e.g.,
leap seconds).

.. _sect_R.6.2:

Ordinary Time Synchronization
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

Ordinary medical equipment uses time synchronization to perform
functions that were previously performed manually, e.g., record-keeping
and scheduling. These were typically done using watches and clocks, with
resultant stability and synchronization errors measured in seconds or
longer. The most stringent time synchronization requirements for
networked medical equipment derive from some of the security protocols
and their record keeping.

Ordinary requirements are:

**Local synchronization**

Synchronized to within approximately 500 milliseconds. Some security
systems have problems when the synchronization error exceeds 1 second.

**Time base stability**

Large drift errors may cause problems. Typical clock drift errors
approximately 1 second/day are unlikely to cause problems. Large
discontinuities are permissible if rare or during start up. Time may run
backwards, but only during rare large discontinuities.

**International Time Synchronization**

Some sites require synchronization to within a few seconds of UTC.
Others have no requirement.

.. _sect_R.6.3:

Background
~~~~~~~~~~

.. _sect_R.6.3.1:

Unsynchronized Time
^^^^^^^^^^^^^^^^^^^

The local system time of a computer is usually provided by two distinct
components.

a. There is a battery-powered clock that is used to establish an initial
   time estimate when the machine is turned on. These clocks are
   typically very inaccurate. Local and international synchronization
   errors are often 5-10 minutes. In some cases, the battery clock is
   incorrect by hours or days.

b. The ongoing system time is provided by a software function and a
   pulse source. The pulse source "ticks" at some rate between 1-1000Hz.
   It has a nominal tick rate that is used by the system software. For
   every tick the system software increments the current time estimate
   appropriately. E.g., for a system with a 100Hz tick, the system time
   increments 10ms each tick.

This lacks any external synchronization and is subject to substantial
initial error in the time estimate and to errors due to systematic and
random drift in the tick source. The tick sources are typically low cost
quartz crystal based, with a systematic error up to approximately
10\ :sup:`-5` in the actual versus nominal tick rate and with a
variation due to temperature, pressure, etc. up to approximately
10\ :sup:`-5`. This corresponds to drifts on the order of 10 seconds per
day.

.. _sect_R.6.3.2:

Network Synchronized Time
^^^^^^^^^^^^^^^^^^^^^^^^^

There is a well established Internet protocol (NTP) for maintaining time
synchronization that should be used by DICOM. It operates in several
ways.

The most common is for the computer to become an NTP client of one or
more NTP servers. As a client it uses occasional ping-pong NTP messages
to:

a. Estimate the network delays. These estimates are updated during each
   NTP update cycle.

b. Obtain a time estimate from the server. Each estimate includes the
   server's own statistical characteristics and accuracy assessment of
   the estimate.

c. Use the time estimates from the servers, the network delay estimates,
   and the time estimates from the local system clock, to obtain a new
   NTP time estimate. This typically uses modern statistical methods and
   filtering to perform optimal estimation.

d. Use the resulting time estimate to

   1. Adjust the system time, and

   2. Update drift and statistical characteristics of the local clock.

The local applications do not normally communicate with the NTP client
software. They normally continue to use the system clock services. The
NTP client software adjusts the system clock. The NTP standard defines a
nominal system clock service as having two adjustable parameters:

a. The clock frequency. In the example above, the nominal clock was
   100Hz, with a nominal increment of 10 milliseconds. Long term
   measurement may indicate that the actual clock is slightly faster and
   the NTP client can adjust the clock increment to be 9.98
   milliseconds.

b. The clock phase. This adjustment permits jump adjustments, and is the
   fixed time offset between the internal clock and the estimated UTC.

The experience with NTP in the field is that NTP clients on the same LAN
as their NTP server will maintain synchronization to within
approximately 100 microseconds. NTP clients on the North American
Internet and utilizing multiple NTP servers will maintain
synchronization to within approximately 10 milliseconds.

There are low cost devices with only limited time synchronization needs.
NTP has been updated to include SNTP for these devices. SNTP eliminates
the estimation of network delays and eliminates the statistical methods
for optimal time estimation. It assumes that the network delays are nil
and that each NTP server time estimate received is completely accurate.
This reduces the development and hardware costs for these devices. The
computer processing costs for NTP are insignificant for a PC, but may be
burdensome for very small devices. The SNTP synchronization errors are
only a few milliseconds in a LAN environment. They are very topology
sensitive and errors may become huge in a WAN environment.

Most NTP servers are in turn NTP clients to multiple superior servers
and peers. NTP is designed to accommodate a hierarchy of server/clients
that distributes time information from a few international standard
clocks out through layers of servers.

.. _sect_R.6.3.3:

External Clocks
^^^^^^^^^^^^^^^

The NTP implementations anticipate the use of three major kinds of
external clock sources:

**External NTP servers**

Many ISPs and government agencies offer access to NTP servers that are
in turn synchronized with the international standard clocks. This access
is usually offered on a restricted basis.

**External clock broadcasts**

The US, Canada, Germany, and others offer radio broadcasts of time
signals that may be used by local receivers attached to an NTP server.
The US and Russia broadcast time signals from satellites, e.g., GPS.
Some mobile telephone services broadcast time signals. These signals are
synchronized with the international standard clocks. GPS time signals
are popular worldwide time sources. Their primary problem is
difficulties with proper antenna location and receiver cost. Most of the
popular low cost consumer GPS systems save money by sacrificing the
clock accuracy.

**External pulse sources**

For extremely high accuracy synchronization, atomic clocks can be
attached to NTP servers. These clocks do not provide a time estimate,
but they provide a pulse signal that is known to be extremely accurate.
The optimal estimation logic can use this in combination with other
external sources to achieve sub microsecond synchronization to a
reference clock even when the devices are separated by the earth's
diameter.

The details regarding selecting an external clock source and appropriate
use of the clock source are outside the scope of the NTP protocol. They
are often discussed and documented in conjunction with the NTP protocol
and many such interfaces are included in the reference implementation of
NTP.

.. _sect_R.6.4:

SNTP Restrictions
~~~~~~~~~~~~~~~~~

In theory, servers can be SNTP servers and NTP servers can be SNTP
clients of other servers. This is very strongly discouraged. The SNTP
errors can be substantial, and the clients of a server using SNTP will
not have the statistical information needed to assess the magnitude of
these errors. It is feasible for SNTP clients to use NTP servers. The
SNTP protocol packets are identical to the NTP protocol packets. SNTP
differs in that some of the statistical information fields are filled
with nominal SNTP values instead of having actual measured values.

.. _sect_R.6.5:

Implementation Considerations
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

There are several public reference implementations of NTP server and
client software available. These are in widespread use and have been
ported to many platforms (including Unix, Windows, and Macintosh). There
are also proprietary and built-in NTP services for some platforms (e.g.,
Windows 2000). The public reference implementations include sample
interfaces to many kinds of external clock sources.

There are significant performance considerations in the selection of
locations for servers and clients. Devices that need high accuracy
synchronization should probably be all on the same LAN together with an
NTP server on that LAN.

Real time operating system (RTOS) implementations may have greater
difficulties. The reference NTP implementations have been ported to
several RTOSs. There were difficulties with the implementations of the
internal system clock on the RTOS. The dual frequency/phase adjustment
requirements may require the clock functions to be rewritten. The
reference implementations also require access to a separate high
resolution interval timer (with sub microsecond accuracy and precision).
This is a standard CPU feature for modern workstation processors, but
may be missing on low end processors.

An RTOS implementation with only ordinary synchronization requirements
might choose to write their own SNTP only implementation rather than use
the reference NTP implementation. The SNTP client is very simple. It may
be based on the reference implementation or written from scratch. The
operating system support needed for accurate adjustment is optional for
SNTP clients. The only requirement is the time base stability
requirement, which usually implies the ability to specify fractional
seconds when setting the time.

The conflict between the user desire to use local time and the NTP use
of UTC must be resolved in the device. DHCP offers the ability to obtain
the offset between local time and UTC dynamically, provided the DHCP
server supports this option. There remain issues such as service
procedures, start up in the absence of DHCP, etc.

The differences between local time, UTC, summer time, etc. are a common
source of confusion and errors setting the battery clock. The NTP
algorithms will eventually resolve these errors, but the final
convergence on correct time may be significantly delayed. The device
might be ready for medical use before these errors are resolved.

