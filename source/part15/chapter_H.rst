.. _chapter_H:

Application Configuration Management Profiles
=============================================

.. _sect_H.1:

Application Configuration Management Profile
--------------------------------------------

The Application Configuration Management Profile applies to the actors
LDAP Server, LDAP Client, and DNS Server. The mandatory and optional
transactions are described in the table and sections below.

.. table:: Application Configuration Management Profiles

   =========== ==================== =========== =======
   Actor       Transaction          Optionality Section
   =========== ==================== =========== =======
   LDAP Server Query LDAP Server    M           H.1.4.2
   \           Update LDAP Server   O           H.1.4.3
   \           Maintain LDAP Server M           H.1.4.4
   LDAP Client Find LDAP Server     M           H.1.4.1
   \           Query LDAP Server    M           H.1.4.2
   \           Update LDAP Server   O           H.1.4.3
   DNS Server  Find LDAP Server     M           H.1.4.1
   =========== ==================== =========== =======

.. _sect_H.1.1:

Data Model Component Objects
~~~~~~~~~~~~~~~~~~~~~~~~~~~~

The normative definition of the schema can be found in `LDAP Schema For
Objects and Attributes <#sect_H.1.3>`__. This section gives additional
informative descriptions of the objects and information defined in that
schema and makes normative statements regarding DICOM system behavior.

The Application Configuration Data Model has the following component
objects:

Device
   The description of the device

Network AE
   The description of the network application entity

Network Connection
   The description of the network interface

Transfer Capability
   The description of the SOP classes and syntaxes supported by a
   Network AE.

In addition there are a number of other objects used in the LDAP schema
(see `Application Configuration Data Model Hierarchy <#sect_H.1.2>`__
and `figure_title <#figure_H.1-2>`__) :

DICOM Configuration Root
   The root of DICOM Configuration Hierarchy

DICOM Devices Root
   The root of the DICOM Devices Hierarchy

DICOM Unique AE-Title Registry Root
   The root of the Unique DICOM AE-Title Registry

DICOM Unique AE Title
   A unique AE Title within the AE Title Registry

LDAP permits extensions to schema to support local needs (i.e., an
object may implement a single structural and multiple auxiliary LDAP
classes). DICOM does not mandate client support for such extensions.
Servers may support such extensions for local purposes. DICOM Clients
may accept or ignore extensions and shall not consider their presence an
error.

.. _sect_H.1.1.1:

Device
^^^^^^

The "device" is set of components organized to perform a task rather
than a specific physical instance. For simple devices there may be one
physical device corresponding to the Data Model device. But for complex
equipment there may be many physical parts to one "device".

The "device" is the collection of physical entities that supports a
collection of Application Entities. It is uniquely associated with these
entities and vice versa. It is also uniquely associated with the network
connections and vice versa. In a simple workstation with one CPU, power
connection, and network connection the "device" is the workstation.

An example of a complex device is a server built from a network of
multiple computers that have multiple network connections and
independent power connections. This would be one device with one
application entity and multiple network connections. Servers like this
are designed so that individual component computers can be replaced
without disturbing operations. The Application Configuration Data Model
does not describe any of this internal structure. It describes the
network connections and the network visible Application Entities. These
complex devices are usually designed for very high availability, but in
the unusual event of a system shutdown the "device" corresponds to all
the parts that get shut down.

.. table:: Attributes of Device Object

   +--------------------------+--------------+--------------------------+
   | Information Field        | Multiplicity | Description              |
   +==========================+==============+==========================+
   | Device Name              | 1            | A unique name (within    |
   |                          |              | the scope of the LDAP    |
   |                          |              | database) for this       |
   |                          |              | device. It is restricted |
   |                          |              | to legal LDAP names, and |
   |                          |              | not constrained by DICOM |
   |                          |              | AE Title limitations.    |
   +--------------------------+--------------+--------------------------+
   | Description              | 0..1         | Unconstrained text       |
   |                          |              | description of the       |
   |                          |              | device.                  |
   +--------------------------+--------------+--------------------------+
   | Manufacturer             | 0..1         | Should be the same as    |
   |                          |              | the value of             |
   |                          |              | Manufacturer (0008,0070) |
   |                          |              | in SOP instances created |
   |                          |              | by this device.          |
   +--------------------------+--------------+--------------------------+
   | Manufacturer Model Name  | 0..1         | Should be the same as    |
   |                          |              | the value of             |
   |                          |              | Manufacturer Model Name  |
   |                          |              | (0008,1090) in SOP       |
   |                          |              | instances created by     |
   |                          |              | this device.             |
   +--------------------------+--------------+--------------------------+
   | Software Version         | 0..N         | Should be the same as    |
   |                          |              | the values of Software   |
   |                          |              | Versions (0018,1020) in  |
   |                          |              | SOP instances created by |
   |                          |              | this device.             |
   +--------------------------+--------------+--------------------------+
   | Station Name             | 0..1         | Should be the same as    |
   |                          |              | the value of Station     |
   |                          |              | Name (0008,1010) in SOP  |
   |                          |              | instances created by     |
   |                          |              | this device.             |
   +--------------------------+--------------+--------------------------+
   | Device Serial Number     | 0..1         | Should be the same as    |
   |                          |              | the value of Device      |
   |                          |              | Serial Number            |
   |                          |              | (0018,1000) in SOP       |
   |                          |              | instances created by     |
   |                          |              | this device.             |
   +--------------------------+--------------+--------------------------+
   | Primary Device Type      | 0..N         | Represents the kind of   |
   |                          |              | device and is most       |
   |                          |              | applicable for           |
   |                          |              | acquisition modalities.  |
   |                          |              | Types should be selected |
   |                          |              | from the list of code    |
   |                          |              | values (0008,0100) for   |
   |                          |              | when applicable.         |
   +--------------------------+--------------+--------------------------+
   | Institution Name         | 0..N         | Should be the same as    |
   |                          |              | the value of Institution |
   |                          |              | Name (0008,0080) in SOP  |
   |                          |              | Instances created by     |
   |                          |              | this device.             |
   +--------------------------+--------------+--------------------------+
   | Institution Address      | 0..N         | Should be the same as    |
   |                          |              | the value of Institution |
   |                          |              | Address (0008,0081)      |
   |                          |              | attribute in SOP         |
   |                          |              | Instances created by     |
   |                          |              | this device.             |
   +--------------------------+--------------+--------------------------+
   | Institutional Department | 0..N         | Should be the same as    |
   | Name                     |              | the value of             |
   |                          |              | Institutional Department |
   |                          |              | Name (0008,1040) in SOP  |
   |                          |              | Instances created by     |
   |                          |              | this device.             |
   +--------------------------+--------------+--------------------------+
   | Institutional Department | 0..N         | Should be the same as    |
   | Type Code Sequence       |              | the value of             |
   |                          |              | Institutional Department |
   |                          |              | Type Code Sequence       |
   |                          |              | (0008,1041) in SOP       |
   |                          |              | Instances created by     |
   |                          |              | this device.             |
   +--------------------------+--------------+--------------------------+
   | Issuer of Patient ID     | 0..1         | Default value for the    |
   |                          |              | Issuer of Patient ID     |
   |                          |              | (0010,0021) for SOP      |
   |                          |              | Instances created by     |
   |                          |              | this device. May be      |
   |                          |              | overridden by the values |
   |                          |              | received in a worklist   |
   |                          |              | or other source.         |
   +--------------------------+--------------+--------------------------+
   | Related Device Reference | 0..N         | The DNs of related       |
   |                          |              | device descriptions      |
   |                          |              | outside the DICOM        |
   |                          |              | Configuration hierarchy. |
   |                          |              | Can be used to link the  |
   |                          |              | DICOM Device object to   |
   |                          |              | additional LDAP objects  |
   |                          |              | instantiated from other  |
   |                          |              | schema and used for      |
   |                          |              | separate administrative  |
   |                          |              | purposes.                |
   +--------------------------+--------------+--------------------------+
   | Authorized Node          | 0..N         | The DNs for the          |
   | Certificate Reference    |              | certificates of nodes    |
   |                          |              | that are authorized to   |
   |                          |              | connect to this device.  |
   |                          |              | The DNs need not be      |
   |                          |              | within the DICOM         |
   |                          |              | configuration hierarchy. |
   +--------------------------+--------------+--------------------------+
   | This Node Certificate    | 0..N         | The DNs of the public    |
   | Reference                |              | certificate(s) for this  |
   |                          |              | node. The DNs need not   |
   |                          |              | be within the DICOM      |
   |                          |              | configuration hierarchy. |
   +--------------------------+--------------+--------------------------+
   | Vendor Device Data       | 0..N         | Device specific vendor   |
   |                          |              | configuration            |
   |                          |              | information              |
   +--------------------------+--------------+--------------------------+
   | Installed                | 1            | Boolean to indicate      |
   |                          |              | whether this device is   |
   |                          |              | presently installed on   |
   |                          |              | the network. (This is    |
   |                          |              | useful for               |
   |                          |              | pre-configuration,       |
   |                          |              | mobile vans, and similar |
   |                          |              | situations.)             |
   +--------------------------+--------------+--------------------------+

The "Authorized Node Certificate Reference" is intended to allow the
LDAP server to provide the list of certificates for nodes that are
authorized to communicate with this device. These should be the public
certificates only. This list need not be complete. Other network peers
may be authorized by other mechanisms.

The "This Node Certificate Reference" is intended to allow the LDAP
server to provide the certificate(s) for this node. These may also be
handled independently of LDAP.

.. note::

   A device may have multiple Primary Device Type entries. It may be a
   multifunctional device, e.g., combined PET and CT. It may be a
   cascaded device, e.g., image capture and ultrasound.

.. table:: Child Objects of Device Object

   +--------------------------+--------------+--------------------------+
   | Information Field        | Multiplicity | Description              |
   +==========================+==============+==========================+
   | Network Application      | 1..N         | The application entities |
   | Entity                   |              | available on this device |
   |                          |              | (see `Network            |
   |                          |              | Application              |
   |                          |              | En                       |
   |                          |              | tity <#sect_H.1.1.2>`__) |
   +--------------------------+--------------+--------------------------+
   | Network Connection       | 1..N         | The network connections  |
   |                          |              | for this device (see     |
   |                          |              | `Network                 |
   |                          |              | Connec                   |
   |                          |              | tion <#sect_H.1.1.3>`__) |
   +--------------------------+--------------+--------------------------+

.. _sect_H.1.1.2:

Network Application Entity
^^^^^^^^^^^^^^^^^^^^^^^^^^

A Network AE is an application entity that provides services on a
network. A Network AE will have the same functional capability
regardless of the particular network connection used. If there are
functional differences based on selected network connection, then these
are separate Network AEs. If there are functional differences based on
other internal structures, then these are separate Network AEs.

.. table:: Attributes of Network AE Object

   +--------------------------+--------------+--------------------------+
   | Information Field        | Multiplicity | Description              |
   +==========================+==============+==========================+
   | AE Title                 | 1            | Unique AE title for this |
   |                          |              | Network AE               |
   +--------------------------+--------------+--------------------------+
   | Description              | 0..1         | Unconstrained text       |
   |                          |              | description of the       |
   |                          |              | application entity.      |
   +--------------------------+--------------+--------------------------+
   | Vendor Data              | 0..N         | AE specific vendor       |
   |                          |              | configuration            |
   |                          |              | information              |
   +--------------------------+--------------+--------------------------+
   | Application Cluster      | 0..N         | Locally defined names    |
   |                          |              | for a subset of related  |
   |                          |              | applications. E.g.       |
   |                          |              | "neuroradiology".        |
   +--------------------------+--------------+--------------------------+
   | Preferred Called AE      | 0..N         | AE Title(s) that are     |
   | Title                    |              | preferred for initiating |
   |                          |              | associations.            |
   +--------------------------+--------------+--------------------------+
   | Preferred Calling AE     | 0..N         | AE Title(s) that are     |
   | Title                    |              | preferred for accepting  |
   |                          |              | associations.            |
   +--------------------------+--------------+--------------------------+
   | Association Acceptor     | 1            | A Boolean value. True if |
   |                          |              | the Network AE can       |
   |                          |              | accept associations,     |
   |                          |              | false otherwise.         |
   +--------------------------+--------------+--------------------------+
   | Association Initiator    | 1            | A Boolean value. True if |
   |                          |              | the Network AE can       |
   |                          |              | accept associations,     |
   |                          |              | false otherwise.         |
   +--------------------------+--------------+--------------------------+
   | Network Connection       | 1..N         | The DNs of the Network   |
   | Reference                |              | Connection objects for   |
   |                          |              | this AE                  |
   +--------------------------+--------------+--------------------------+
   | Supported Character Set  | 0..N         | The Character Set(s)     |
   |                          |              | supported by the Network |
   |                          |              | AE for Data Sets it      |
   |                          |              | receives. The value      |
   |                          |              | shall be selected from   |
   |                          |              | the Defined Terms for    |
   |                          |              | Specific Character Set   |
   |                          |              | (0008,0005) in . If no   |
   |                          |              | values are present, this |
   |                          |              | implies that the Network |
   |                          |              | AE supports only the     |
   |                          |              | default character        |
   |                          |              | repertoire(ISO IR 6).    |
   +--------------------------+--------------+--------------------------+
   | Installed                | 0..1         | A Boolean value. True if |
   |                          |              | the AE is installed on   |
   |                          |              | network. If not present, |
   |                          |              | information about the    |
   |                          |              | installed status of the  |
   |                          |              | AE is inherited from the |
   |                          |              | device                   |
   +--------------------------+--------------+--------------------------+

The "Application Cluster" concept provides the mechanism to define local
clusters of systems. The use cases for Configuration Management require
a "domain" capability for DICOM applications that would be independent
of the network topology and administrative domains that are used by DNS
and other TCP level protocols. The Application Cluster is multi-valued
to permit multiple clustering concepts for different purposes. It is
expected to be used as part of a query to limit the scope of the query.

The "Preferred Called AE Title" concept is intended to allow a site
administrator to define a limited default set of AEs that are preferred
for use as communication partners when initiating associations. This
capability is particularly useful for large centrally administered sites
to simplify the configuration possibilities and restrict the number of
configured AEs for specific workflow scenarios. For example, the set of
AEs might contain the AE Titles of assigned Printer, Archive, RIS and QA
Workstations so that the client device could adapt its configuration
preferences accordingly. The "Preferred Called AE Title" concept does
not prohibit association initiation to unlisted AEs. Associations to
unlisted AEs can be initiated if necessary.

The "Preferred Calling AE Title" concept is intended to allow a site
administrator to define a default set of AEs that are preferred when
accepting assocations. The "Preferred Calling AE Title" concept does not
prohibit accepting associations from unlisted AEs.

The "Network Connection Reference" is a link to a separate Network
Connection object. The referenced Network Connection object is a sibling
the AE object (i.e., both are children of the same Device object).

.. table:: Child Objects of Network AE Object

   +---------------------+--------------+-------------------------------+
   | Information Field   | Multiplicity | Description                   |
   +=====================+==============+===============================+
   | Transfer Capability | 1..N         | The Transfer Capabilities for |
   |                     |              | this Network AE. See          |
   |                     |              | `                             |
   |                     |              | Transactions <#sect_H.1.4>`__ |
   +---------------------+--------------+-------------------------------+

.. _sect_H.1.1.3:

Network Connection
^^^^^^^^^^^^^^^^^^

The "network connection" describes one TCP port on one network device.
This can be used for a TCP connection over which a DICOM association can
be negotiated with one or more Network AEs. It specifies the hostname
and TCP port number. A network connection may support multiple Network
AEs. The Network AE selection takes place during association negotiation
based on the called and calling AE-titles.

.. table:: Attributes of Network Connection Object

   +-------------------+--------------+---------------------------------+
   | Information Field | Multiplicity | Description                     |
   +===================+==============+=================================+
   | Common Name       | 0..1         | An arbitrary name for the       |
   |                   |              | Network Connections object. Can |
   |                   |              | be a meaningful name or any     |
   |                   |              | unique sequence of characters.  |
   |                   |              | Can be used as the RDN.         |
   |                   |              |                                 |
   |                   |              | .. note::                       |
   |                   |              |                                 |
   |                   |              |    The "cn" attribute type is a |
   |                   |              |    basic LDAP defined type and  |
   |                   |              |    is a synonym for Common      |
   |                   |              |    Name.                        |
   +-------------------+--------------+---------------------------------+
   | Hostname          | 1            | This is the DNS name for this   |
   |                   |              | particular connection. This is  |
   |                   |              | used to obtain the current IP   |
   |                   |              | address for connections.        |
   |                   |              | Hostname must be sufficiently   |
   |                   |              | qualified to be unambiguous for |
   |                   |              | any client DNS user.            |
   +-------------------+--------------+---------------------------------+
   | Port              | 0..1         | The TCP port that the AE is     |
   |                   |              | listening on. (This may be      |
   |                   |              | missing for a network           |
   |                   |              | connection that only initiates  |
   |                   |              | associations.)                  |
   +-------------------+--------------+---------------------------------+
   | TLS CipherSuite   | 0..N         | The TLS CipherSuites that are   |
   |                   |              | supported on this particular    |
   |                   |              | connection. TLS CipherSuites    |
   |                   |              | shall be described using an     |
   |                   |              | `biblioen                       |
   |                   |              | try_title <#biblio_RFC_2246>`__ |
   |                   |              | string representation (e.g.,    |
   |                   |              | "TLS_RSA_WITH_RC4_128_SHA")     |
   +-------------------+--------------+---------------------------------+
   | Installed         | 0..1         | A Boolean value. True if the    |
   |                   |              | Network Connection is installed |
   |                   |              | on the network. If not present, |
   |                   |              | information about the installed |
   |                   |              | status of the Network           |
   |                   |              | Connection is inherited from    |
   |                   |              | the device.                     |
   +-------------------+--------------+---------------------------------+

Inclusion of a TLS CipherSuite in a Network Connection capable of
accepting associations implies that the TLS protocol must be used to
successfully establish an association on the Network Connection.

A single Network AE may be available on multiple network connections.
This is often done at servers for availability or performance reasons.
For example, at a hospital where each floor is networked to a single hub
per floor, the major servers may have direct connections to each of the
hubs. This provides better performance and reliability. If the server
does not change behavior based on the particular physical network
connection, then it can be described as having Network AEs that are
available on all of these multiple network connections. A Network AE may
also be visible on multiple TCP ports on the same network hardware port,
with each TCP port represented as a separate network connection. This
would allow, e.g., a TLS-secured DICOM port and a classical un-secured
DICOM port to be supported by the same AE.

.. _sect_H.1.1.4:

Transfer Capabilities
^^^^^^^^^^^^^^^^^^^^^

Each Network AE object has one or more Transfer Capabilities. Each
transfer capability specifies the SOP class that the Network AE can
support, the mode that it can utilize (SCP or SCU), and the Transfer
Syntax(es) that it can utilize. A Network AE that supports the same SOP
class in both SCP and SCU modes will have two Transfer Capabilities
objects for that SOP class.

.. table:: Attributes of Transfer Capability Object

   +-------------------+--------------+---------------------------------+
   | Information Field | Multiplicity | Description                     |
   +===================+==============+=================================+
   | Common Name       | 0..1         | An arbitrary name for the       |
   |                   |              | Transfer Capability object. Can |
   |                   |              | be a meaningful name or any     |
   |                   |              | unqiue sequence of characters.  |
   |                   |              | Can be used as the RDN.         |
   +-------------------+--------------+---------------------------------+
   | SOP Class         | 1            | SOP Class UID                   |
   +-------------------+--------------+---------------------------------+
   | Role              | 1            | Either "SCU" or "SCP"           |
   +-------------------+--------------+---------------------------------+
   | Transfer Syntax   | 1..N         | The transfer syntax(es) that    |
   |                   |              | may be requested as an SCU or   |
   |                   |              | that are offered as an SCP.     |
   +-------------------+--------------+---------------------------------+

.. _sect_H.1.1.5:

DICOM Configuration Root
^^^^^^^^^^^^^^^^^^^^^^^^

This structural object class represents the root of the DICOM
Configuration Hierarchy. Only a single object of this type should exist
within an organizational domain. Clients can search for an object of
this class to locate the root of the DICOM Configuration Hierarchy.

.. table:: Attributes of the DICOM Configuration Root Object

   +-------------------+--------------+---------------------------------+
   | Information Field | Multiplicity | Description                     |
   +===================+==============+=================================+
   | Common Name       | 1            | The Name for the Configuration  |
   |                   |              | Root. Should be used as the     |
   |                   |              | RDN. The name shall be "DICOM   |
   |                   |              | Configuration".                 |
   +-------------------+--------------+---------------------------------+
   | Description       | 0..1         | Unconstrained text description. |
   +-------------------+--------------+---------------------------------+

.. table:: Child Objects of DICOM Configuration Root Object

   +--------------------------+--------------+--------------------------+
   | Information Field        | Multiplicity | Description              |
   +==========================+==============+==========================+
   | Devices Root             | 1            | The root of the DICOM    |
   |                          |              | Devices Hierarchy        |
   +--------------------------+--------------+--------------------------+
   | Unique AE Titles         | 1            | The root of the Unique   |
   | Registry Root            |              | AE Titles Registry       |
   +--------------------------+--------------+--------------------------+

.. _sect_H.1.1.6:

Devices Root
^^^^^^^^^^^^

This structural object class represents the root of the DICOM Devices
Hierarchy. Only a single object of this type should exist as a child of
DICOM Configuration Root. Clients can search for an object of this class
to locate the root of the DICOM Devices Hierarchy.

.. table:: Attributes of the Devices Root Object

   +-------------------+--------------+---------------------------------+
   | Information Field | Multiplicity | Description                     |
   +===================+==============+=================================+
   | Common Name       | 1            | The Name for the Devices Root.  |
   |                   |              | Should be used as the RDN. The  |
   |                   |              | name shall be "Devices".        |
   +-------------------+--------------+---------------------------------+
   | Description       | 0..1         | Unconstrained text description. |
   +-------------------+--------------+---------------------------------+

.. table:: Child Objects of Devices Root Object

   +-------------------+--------------+---------------------------------+
   | Information Field | Multiplicity | Description                     |
   +===================+==============+=================================+
   | Device            | 0..N         | The individual devices          |
   |                   |              | installed within this           |
   |                   |              | organizational domain.          |
   +-------------------+--------------+---------------------------------+

.. _sect_H.1.1.7:

Unique AE Titles Registry Root
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

This structural object class represents the root of the Unique AE-Titles
Registry Hierarchy. Only a single object of this type should exist as a
child of the DICOM Configuration Root. Clients can search for an object
of this class to locate the root of the Unique AE Titles Registry.

.. table:: Attributes of the Unique AE Titles Registry Root Object

   +-------------------+--------------+---------------------------------+
   | Information Field | Multiplicity | Description                     |
   +===================+==============+=================================+
   | Common Name       | 1            | The Name for the Unique AE      |
   |                   |              | Titles Registry Root. Should be |
   |                   |              | used as the RDN. The name shall |
   |                   |              | be "Unique AE Titles Registry". |
   +-------------------+--------------+---------------------------------+
   | Description       | 0..1         | Unconstrained text description. |
   +-------------------+--------------+---------------------------------+

.. table:: Child Objects of Unique AE Titles Registry Root Object

   +-------------------+--------------+---------------------------------+
   | Information Field | Multiplicity | Description                     |
   +===================+==============+=================================+
   | Unique AE Title   | 0..N         | The unique AE Titles installed  |
   |                   |              | within this organizational      |
   |                   |              | domain (see `Unique AE          |
   |                   |              | Title <#sect_H.1.1.8>`__)       |
   +-------------------+--------------+---------------------------------+

.. _sect_H.1.1.8:

Unique AE Title
^^^^^^^^^^^^^^^

This structural object class represents a Unique Application Entity
Title. Objects of this type should only exist as children of the Unique
AE-Titles Registry Root. The sole purpose of this object class is to
enable allocation of unique AE Titles. All operational information
associated with an AE Title is maintained within a separate Network AE
object.

.. table:: Attributes of the Unique AE Title Object

   ================= ============ =====================
   Information Field Multiplicity Description
   ================= ============ =====================
   AE Title          1            The Unique AE Titles.
   ================= ============ =====================

.. _sect_H.1.2:

Application Configuration Data Model Hierarchy
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

The LDAP structure is built upon a hierarchy of named objects. This
hierarchy can vary from site to site. The DICOM configuration management
function needs to find its objects within this hierarchy in a
predictable manner. For this reason, three specific object classes are
defined for the three objects at the top of the DICOM hierarchy. These
three object classes must not be used in this tree relationship anywhere
else in the LDAP hierarchy.

The DICOM portion of the hierarchy shall begin at a root object of class
dicomConfigurationRoot with a Common Name of "DICOM Configuration".
Below this object shall be two other objects:

a. An object of class dicomDevicesRoot with a Common Name of "Devices".
   This is the root of the tree of objects that correspond to the
   Application Configuration Data Model structure of `Data Model
   Component Objects <#sect_H.1.1>`__.

b. An object of class dicomUniqueAETitlesRegistryRoot with a common name
   of "Unique AE Titles Registry". This is the root of a flat tree of
   objects. Each of these objects is named with one of the AE titles
   that are presently assigned. This is the mechanism for finding
   available AE titles.

The three object classes dicomConfigurationRoot, dicomDevicesRoot, and
dicomUniqueAETitleRegistryRoot are used by LDAP clients to establish the
local root of the DICOM configuration information within an LDAP
hierarchy that may be used for many other purposes.

.. note::

   During system startup it is likely that the DICOM configuration
   application will do an LDAP search for an entry of object class
   dicomConfigurationRoot and then confirm that it has the
   dicomDevicesRoot and dicomUniqueAETitlesRegistryRoot entries directly
   below it. When it finds this configuration, it can then save the full
   location within the local LDAP tree and use that as the root of the
   DICOM tree.

The objects underneath the dicomUniqueAETitlesRegistryRoot are used to
provide the uniqueness required for DICOM AE-titles. The
dicomUniqueAETitle objects have a single attribute representing a unique
AE Title. When a new AE-Title is required, a tentative new name is
selected. The new name is reserved by using the LDAP create facility to
create an object of class dicomUniqueAETitle with the new name under the
AE-Title object. If this name is already in use, the create will fail.
Otherwise, this reserves the name. LDAP queries can be used to obtain
the list of presently assigned AE-titles by obtaining the list of all
names under the dicomUniqueAETitlesRegistryRoot object.

.. note::

   1. LDAP uses a root and relative hierarchical naming system for
      objects. Every object name is fully unique within the full
      hierarchy. This means that the names of the objects beneath
      "Unique AE Titles Registry" will be unique. It also means that the
      full names of Network AEs and Connections will be within their
      hierarchy context. E.g., the DN for one of the Network AEs in
      `figure_title <#figure_H.1-2>`__ would be:

      -  dicomAETitle=CT_01, dicomDeviceName=Special Research CT,
         cn=Devices, cn=DICOM Configuration, o=Sometown Hospital

   2. In theory, multiple independent DICOM configuration hierarchies
      could exist within one organization. The LDAP servers in such a
      network should constrain local device accesses so that DICOM
      configuration clients have only one DICOM Configuration Hierarchy
      visible to each client.

   3. The merger of two organizations will require manual configuration
      management to merge DICOM Configuration hierarchies. There are
      likely to be conflicts in AE-titles, roles, and other conflicts.

.. _sect_H.1.3:

LDAP Schema For Objects and Attributes
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

The individual LDAP attribute information is summarized in the comments
at the beginning of the schema below. The formal definition of the
objects and the attributes is in the schema below. This schema may be
extended by defining an additional schema that defines auxiliary
classes, sub-classes derived from this schema, or both.

The formal LDAP schema for the Application Configuration Data Model and
the DICOM Configuration Hierarchy is:

::

   # 3 Attribute Type Definitions
   # 
   #    The following attribute types are defined in this document:
   # 
   #   Name                                    Syntax    Multiplicity
   #   --------------------------------        ------    ------------
   #   dicomDeviceName                         string    Single
   #   dicomDescription                        string    Single
   #   dicomManufacturer                       string    Single
   #   dicomManufacturerModelName              string    Single
   #   dicomSoftwareVersion                    string    Multiple
   #   dicomVendorData                         binary    Multiple
   #   dicomAETitle                            string    Single
   #   dicomNetworkConnectionReference         DN        Multiple
   #   dicomApplicationCluster                 string    Multiple
   #   dicomAssociationInitiator               bool      Single
   #   dicomAssociationAcceptor                bool      Single
   #   dicomHostname                           string    Single
   #   dicomPort                               integer   Single
   #   dicomSOPClass                           OID       Single
   #   dicomTransferRole                       string    Single
   #   dicomTransferSyntax                     OID       Multiple
   #   dicomPrimaryDeviceType                  string    Multiple
   #   dicomRelatedDeviceReference             DN        Multiple
   #   dicomPreferredCalledAETitle             string    Multiple
   #   dicomTLSCipherSuite                     string    Multiple
   #   dicomAuthorizedNodeCertificateReference DN        Multiple
   #   dicomThisNodeCertificateReference       DN        Multiple
   #   dicomInstalled                          bool      Single
   #   dicomStationName                        string    Single
   #   dicomDeviceSerialNumber                 string    Single
   #   dicomInstitutionName                    string    Multiple
   #   dicomInstitutionAddress                 string    Multiple
   #   dicomInstitutionDepartmentName          string    Multiple
   #   dicomIssuerOfPatientID                  string    Single
   #   dicomPreferredCallingAETitle            string    Multiple
   #   dicomSupportedCharacterSet              string    Multiple
   #   dicomInstitutionDepartmentType          string    Multiple
   #


   # 3.1 dicomDeviceName                     string    Single
   # 
   #    This attribute stores the unique name (within the scope of the LDAP database) 
   #    for a DICOM Device.
   #
   #    It is a single-valued attribute. 
   #    This attribute's syntax is 'Directory String'.
   #    Its case is not significant for equality and substring matches.
   # 
   attributetype ( 1.2.840.10008.15.0.3.1
       NAME 'dicomDeviceName'
       DESC 'The unique name for the device'
       EQUALITY caseIgnoreMatch
       SUBSTR caseIgnoreSubstringsMatch
       SYNTAX 1.3.6.1.4.1.1466.115.121.1.15
       SINGLE-VALUE )

   # 3.2 dicomDescription                    string    Single
   # 
   #    This attribute stores the (unconstrained) textual description for a DICOM entity.
   #
   #    It is a single-valued attribute. 
   #    This attribute's syntax is 'Directory String'.
   #    Its case is not significant for equality and substring matches.
   # 
   attributetype ( 1.2.840.10008.15.0.3.2
       NAME 'dicomDescription'
       DESC 'Textual description of the DICOM entity'
       EQUALITY caseIgnoreMatch
       SUBSTR caseIgnoreSubstringsMatch
       SYNTAX 1.3.6.1.4.1.1466.115.121.1.15
       SINGLE-VALUE )

   # 3.3 dicomManufacturer                   string    Single
   #
   #    This attribute stores the Manufacturer name for a DICOM Device.
   #    Should be identical to the value of the DICOM attribute Manufacturer (0008,0070) [VR=LO]
   #    contained in SOP Instances created by this device.
   #
   #    It is a single-valued attribute. 
   #    This attribute's syntax is 'Directory String'.
   #    Its case is not significant for equality and substring matches.
   #
   attributetype ( 1.2.840.10008.15.0.3.3
       NAME 'dicomManufacturer'
       DESC 'The device Manufacturer name'
       EQUALITY caseIgnoreMatch
       SUBSTR caseIgnoreSubstringsMatch
       SYNTAX 1.3.6.1.4.1.1466.115.121.1.15
       SINGLE-VALUE )

   # 3.4 dicomManufacturerModelName          string    Single
   #
   #    This attribute stores the Manufacturer Model Name for a DICOM Device.
   #    Should be identical to the value of the DICOM attribute Manufacturer 
   #    Model Name (0008,1090) [VR=LO]
   #    contained in SOP Instances created by this device.
   #
   #    It is a single-valued attribute. 
   #    This attribute's syntax is 'Directory String'.
   #    Its case is not significant for equality and substring matches.
   #
   attributetype ( 1.2.840.10008.15.0.3.4
       NAME 'dicomManufacturerModelName'
       DESC 'The device Manufacturer Model Name'
       EQUALITY caseIgnoreMatch
       SUBSTR caseIgnoreSubstringsMatch
       SYNTAX 1.3.6.1.4.1.1466.115.121.1.15
       SINGLE-VALUE )

   # 3.5 dicomSoftwareVersion                string    Multiple
   #
   #    This attribute stores the software version of the device and/or its subcomponents.
   #    Should be the same as the values of Software Versions (0018,1020) in 
   #    SOP instances created by this device.
   #
   #    It is a multi-valued attribute. 
   #    This attribute's syntax is 'Directory String'.
   #    Its case is not significant for equality and substring matches.
   #
   attributetype ( 1.2.840.10008.15.0.3.5
       NAME 'dicomSoftwareVersion'
       DESC 'The device software version. Should be the same as the values of Software
             Versions (0018,1020) in SOP instances created by this device.'
       EQUALITY caseIgnoreMatch
       SUBSTR caseIgnoreSubstringsMatch
       SYNTAX 1.3.6.1.4.1.1466.115.121.1.15 )

   # 3.6 dicomVendorData                     binary    Multiple
   #
   #    This attribute stores vendor specific configuration information.
   #
   #    It is a multi-valued attribute. 
   #    This attribute's syntax is 'Binary'.
   #    Neither equality nor substring matches are applicable to binary data.
   #
   attributetype ( 1.2.840.10008.15.0.3.6
       NAME 'dicomVendorData'
       DESC 'Arbitrary vendor-specific configuration information (binary data)'
       SYNTAX 1.3.6.1.4.1.1466.115.121.1.5 )

   # 3.7 dicomAETitle                        name      Single
   #
   #    This attribute stores an Application Entity (AE) title.
   #
   #    It is a single-valued attribute. 
   #    This attribute's syntax is 'IA5 String'.
   #    Its case is significant.
   #
   attributetype ( 1.2.840.10008.15.0.3.7
       NAME 'dicomAETitle'
       DESC 'Application Entity (AE) title'
       EQUALITY caseExactIA5Match
       SYNTAX 1.3.6.1.4.1.1466.115.121.1.26
       SINGLE-VALUE )

   # 3.8 dicomNetworkConnectionReference     DN        Multiple
   # 
   #    This attribute stores the DN of a dicomNetworkConnection object 
   #    used by an Application Entity.
   #
   #    It is a multi-valued attribute. 
   #    This attribute's syntax is 'Distinguished Name'.
   # 
   attributetype ( 1.2.840.10008.15.0.3.8
       NAME 'dicomNetworkConnectionReference'
       DESC 'The DN of a dicomNetworkConnection object used by an Application Entity'
       EQUALITY distinguishedNameMatch
       SYNTAX 1.3.6.1.4.1.1466.115.121.1.12 )

   # 3.9 dicomApplicationCluster             string    Multiple
   #
   #    This attribute stores an application cluster name for an Application 
   #    Entity (e.g., "Neuroradiology Research")
   #
   #    It is a multi-valued attribute. 
   #    This attribute's syntax is 'Directory String'.
   #    Its case is not significant for equality and substring matches.
   # 
   attributetype ( 1.2.840.10008.15.0.3.9
       NAME 'dicomApplicationCluster'
       DESC 'Application cluster name for an Application Entity (e.g., "Neuroradiology Research")'
       EQUALITY caseIgnoreMatch
       SUBSTR caseIgnoreSubstringsMatch
       SYNTAX 1.3.6.1.4.1.1466.115.121.1.15 )

   # 3.10 dicomAssociationInitiator          bool      Single
   #
   #    This attribute indicates if an Application Entity is capable of initiating 
   #    network associations.
   #
   #    It is a single-valued attribute. 
   #    This attribute's syntax is 'Boolean'.
   # 
   attributetype ( 1.2.840.10008.15.0.3.10
       NAME 'dicomAssociationInitiator'
       DESC 'Indicates if an Application Entity is capable of initiating network associations'
       EQUALITY booleanMatch 
       SYNTAX 1.3.6.1.4.1.1466.115.121.1.7
       SINGLE-VALUE )

   # 3.11 dicomAssociationAcceptor           bool      Single
   #
   #    This attribute indicates if an Application Entity is capable of accepting 
   #    network associations.
   #
   #    It is a single-valued attribute. 
   #    This attribute's syntax is 'Boolean'.
   # 
   attributetype ( 1.2.840.10008.15.0.3.11
       NAME 'dicomAssociationAcceptor'
       DESC 'Indicates if an Application Entity is capable of accepting network associations'
       EQUALITY booleanMatch 
       SYNTAX 1.3.6.1.4.1.1466.115.121.1.7
       SINGLE-VALUE )

   # 3.12 dicomHostname                      string    Single
   #
   #    This attribute stores a DNS hostname for a connection.
   #
   #    It is a single-valued attribute. 
   #    This attribute's syntax is 'Directory String'.
   #    Its case is not significant for equality and substring matches.
   #
   attributetype ( 1.2.840.10008.15.0.3.12
       NAME 'dicomHostname'
       DESC 'DNS hostname'
       EQUALITY caseIgnoreMatch
       SUBSTR caseIgnoreSubstringsMatch
       SYNTAX 1.3.6.1.4.1.1466.115.121.1.15
       SINGLE-VALUE )

   # 3.13 dicomPort                          integer   Single
   #
   #    This attribute stores a TCP port number for a connection.
   #
   #    It is a single-valued attribute. 
   #    This attribute's syntax is 'Integer'.
   #
   attributetype ( 1.2.840.10008.15.0.3.13
       NAME 'dicomPort'
       DESC 'TCP Port number'
       EQUALITY  integerMatch
       SYNTAX 1.3.6.1.4.1.1466.115.121.1.27
       SINGLE-VALUE )

   # 3.14 dicomSOPClass                      OID       Single
   #
   #    This attribute stores a SOP Class UID
   #
   #    It is a single-valued attribute. 
   #    This attribute's syntax is 'OID'.
   #
   attributetype ( 1.2.840.10008.15.0.3.14
       NAME 'dicomSOPClass'
       DESC 'A SOP Class UID'
       EQUALITY  objectIdentifierMatch
       SYNTAX 1.3.6.1.4.1.1466.115.121.1.38
       SINGLE-VALUE )

   # 3.15 dicomTransferRole                  String    Single
   #
   #    This attribute stores a transfer role (either "SCU" or "SCP").
   #
   #    It is a single-valued attribute. 
   #    This attribute's syntax is 'Directory String'.
   #    Its case is not significant for equality and substring matches.
   #
   attributetype ( 1.2.840.10008.15.0.3.15
       NAME 'dicomTransferRole'
       DESC 'Transfer role (either "SCU" or "SCP")'
       EQUALITY caseIgnoreMatch
       SUBSTR caseIgnoreSubstringsMatch
       SYNTAX 1.3.6.1.4.1.1466.115.121.1.15
       SINGLE-VALUE )

   # 3.16 dicomTransferSyntax                OID       Multiple
   #
   #    This attribute stores a Transfer Syntax UID
   #
   #    It is a multi-valued attribute. 
   #    This attribute's syntax is 'OID'.
   #
   attributetype ( 1.2.840.10008.15.0.3.16
       NAME 'dicomTransferSyntax'
       DESC 'A Transfer Syntax UID'
       EQUALITY  objectIdentifierMatch
       SYNTAX 1.3.6.1.4.1.1466.115.121.1.38 )

   # 3.17 dicomPrimaryDeviceType             string    Multiple
   #   
   #    This attribute stores the primary type for a DICOM Device. 
   #    Types should be selected from the list of code values (0008,0100) 
   #    for Context ID 30 in DICOM Part 16 when applicable. 
   #
   #    It is a multiple-valued attribute. 
   #    This attribute's syntax is 'IA5 String'.
   #    Its case is significant.
   #
   attributetype ( 1.2.840.10008.15.0.3.17
       NAME 'dicomPrimaryDeviceType'
       DESC 'The device Primary Device type'
       EQUALITY caseExactIA5Match
       SYNTAX 1.3.6.1.4.1.1466.115.121.1.26 )

   # 3.18 dicomRelatedDeviceReference        DN        Multiple
   #
   #    This attribute stores a reference to a related device description outside 
   #    the DICOM Configuration Hierachy. Can be used to link the DICOM Device object to 
   #    additional LDAP objects instantiated from other schema and used for 
   #    separate administrative purposes. 
   #
   #    This attribute's syntax is 'Distinguished Name'.
   #    It is a multiple-valued attribute. 
   #
   attributetype ( 1.2.840.10008.15.0.3.18
       NAME 'dicomRelatedDeviceReference'
       DESC 'The DN of a related device description outside the DICOM Configuration Hierachy'
       EQUALITY distinguishedNameMatch
       SYNTAX 1.3.6.1.4.1.1466.115.121.1.12 )

   # 3.19 dicomPreferredCalledAETitle        string    Multiple
   #
   #    AE Title(s) to which associations may be preferably initiated. 
   #
   #    It is a multiple-valued attribute. 
   #    This attribute's syntax is 'IA5 String'.
   #    Its case is significant.
   #
   attributetype ( 1.2.840.10008.15.0.3.19
       NAME 'dicomPreferredCalledAETitle'
       DESC 'AE Title(s) to which associations may be preferably initiated.'
       EQUALITY caseExactIA5Match
       SYNTAX 1.3.6.1.4.1.1466.115.121.1.26 )

   # 3.20 dicomTLSCipherSuite                string    Multiple
   #
   #    The attribute stores the supported TLS CipherSuites.
   #    TLS CipherSuites shall be described using a RFC-2246 string representation 
   #    (e.g., "TLS_RSA_WITH_RC4_128_SHA").
   #
   #    It is a multiple-valued attribute. 
   #    This attribute's syntax is 'IA5 String'.
   #    Its case is significant.
   # 
   attributetype ( 1.2.840.10008.15.0.3.20
       NAME 'dicomTLSCipherSuite'
       DESC 'The supported TLS CipherSuites'
       EQUALITY caseExactIA5Match
       SYNTAX 1.3.6.1.4.1.1466.115.121.1.26 )

   # 3.21  dicomAuthorizedNodeCertificateReference DN Multiple
   #
   #    This attribute stores a reference to a TLS public certificate for a DICOM
   #    node that is authorized to connect to this node. The certificate 
   #    is not necessarily stored within the DICOM Hierarchy
   #
   #    This attribute's syntax is 'Distinguished Name'.
   #    It is a multiple-valued attribute. 
   #
   attributetype ( 1.2.840.10008.15.0.3.21
       NAME 'dicomAuthorizedNodeCertificateReference'
       DESC 'The DN of a Certificate for a DICOM node that is authorized to connect to this node'
       EQUALITY distinguishedNameMatch
       SYNTAX 1.3.6.1.4.1.1466.115.121.1.12 )

   # 3.22 dicomThisNodeCertificateReference DN Multiple
   #
   #    This attribute stores a reference to a TLS public certificate for
   #    this node. It is not necessarily stored as part of
   #    the DICOM Configuration Hierachy.
   #
   #    This attribute's syntax is 'Distinguished Name'.
   #    It is a multiple-valued attribute. 
   #
   attributetype ( 1.2.840.10008.15.0.3.22
       NAME 'dicomThisNodeCertificateReference'
       DESC 'The DN of a related device description outside the DICOM Configuration Hierachy'
       EQUALITY distinguishedNameMatch
       SYNTAX 1.3.6.1.4.1.1466.115.121.1.12 )

   # 3.23 dicomInstalled                     bool      Single
   #
   #    This attribute indicates whether the object is presently installed.
   #
   #    It is a single-valued attribute. 
   #    This attribute's syntax is 'Boolean'.
   # 
   attributetype ( 1.2.840.10008.15.0.3.23
       NAME 'dicomInstalled'
       DESC 'Indicates if the DICOM object (device, Network AE, or Port) is presently installed'
       EQUALITY booleanMatch 
       SYNTAX 1.3.6.1.4.1.1466.115.121.1.7
       SINGLE-VALUE )

   # 3.24  dicomStationName                  string    Single
   #
   #    This attribute stores the station name of the device.
   #    Should be the same as the value of Station Name (0008,1010) in 
   #    SOP instances created by this device.
   #
   #    It is a single-valued attribute.
   #    This attribute's syntax is 'Directory String'.
   # 
   attributetype ( 1.2.840.10008.15.0.3.24
       NAME 'dicomStationName'
       DESC 'Station Name of the device. Should be the same as the value of Station
             Name (0008,1010) in SOP instances created by this device.'
       EQUALITY caseIgnoreMatch
       SUBSTR caseIgnoreSubstringsMatch
       SYNTAX 1.3.6.1.4.1.1466.115.121.1.15
       SINGLE-VALUE)

   # 3.25  dicomDeviceSerialNumber           string    Single
   #
   #    This attribute stores the serial number of the device.
   #    Should be the same as the value of Device Serial Number (0018,1000) 
   #    in SOP instances created by this device.
   #
   #    It is a single-valued attribute.
   #    This attribute's syntax is 'Directory String'.
   # 
   attributetype ( 1.2.840.10008.15.0.3.25
       NAME 'dicomDeviceSerialNumber'
       DESC 'Serial number of the device. Should be the same as the value of Device Serial
             Number (0018,1000) in SOP instances created by this device.'
       EQUALITY caseIgnoreMatch
       SUBSTR caseIgnoreSubstringsMatch
       SYNTAX 1.3.6.1.4.1.1466.115.121.1.15
       SINGLE-VALUE)

   # 3.26  dicomInstitutionName              string    Multiple
   #
   #    This attribute stores the institution name of the device.
   #    Should be the same as the value of Institution Name (0008,0080) 
   #    in SOP Instances created by this device.
   #
   #    It is a multi-valued attribute.
   #    This attribute's syntax is 'Directory String'.
   # 
   attributetype ( 1.2.840.10008.15.0.3.26
       NAME 'dicomInstitutionName'
       DESC 'Institution name of the device. Should be the same as the value of Institution
             Name (0008,0080) in SOP Instances created by this device.'
       EQUALITY caseIgnoreMatch
       SUBSTR caseIgnoreSubstringsMatch
       SYNTAX 1.3.6.1.4.1.1466.115.121.1.15 )

   # 3.27  dicomInstitutionAddress           string    Multiple
   #
   #    This attribute stores the institution address of the device.
   #    Should be the same as the value of Institution Address (0008,0081) 
   #    attribute in SOP Instances created by this device.
   #
   #    It is a multi-valued attribute.
   #    This attribute's syntax is 'Directory String'.
   # 
   attributetype ( 1.2.840.10008.15.0.3.27
       NAME 'dicomInstitutionAddress'
       DESC 'Institution address of the device. Should be the same as the value of Institution
             Address (0008,0081) attribute in SOP Instances created by this device.'
       EQUALITY caseIgnoreMatch
       SUBSTR caseIgnoreSubstringsMatch
       SYNTAX 1.3.6.1.4.1.1466.115.121.1.15 )

   # 3.28  dicomInstitutionDepartmentName    string   Multiple
   #
   #    This attribute stores the institution department name of the device. 
   #    Should be the same as the value of Institutional Department Name (0008,1040) 
   #    in SOP Instances created by this device.
   #
   #    It is a multi-valued attribute.
   #    This attribute's syntax is 'Directory String'.
   # 
   attributetype ( 1.2.840.10008.15.0.3.28
       NAME 'dicomInstitutionDepartmentName'
       DESC 'Institution department name of the device. Should be the same as the value of Institutional
             Department Name (0008,1040) in SOP Instances created by this device.'
       EQUALITY caseIgnoreMatch
       SUBSTR caseIgnoreSubstringsMatch
       SYNTAX 1.3.6.1.4.1.1466.115.121.1.15 )

   # 3.29  dicomIssuerOfPatientID            string    Single
   #
   #    This attribute stores the Default value for the Issuer of Patient ID (0010,0021) 
   #    for SOP Instances created by this device. May be overridden by the values 
   #    received in a worklist or other source.
   #
   #    It is a multi-valued attribute.
   #    This attribute's syntax is 'Directory String'.
   # 
   attributetype ( 1.2.840.10008.15.0.3.29
       NAME 'dicomIssuerOfPatientID'
       DESC 'Default value for the Issuer of Patient ID (0010,0021) for SOP Instances created by this device.
             May be overridden by the values received in a worklist or other source.'
       EQUALITY caseIgnoreMatch
       SUBSTR caseIgnoreSubstringsMatch
       SYNTAX 1.3.6.1.4.1.1466.115.121.1.15 )

   # 3.30  dicomPreferredCallingAETitle      string    Multiple
   #
   #    AE Title(s) to which associations may be preferably accepted. 
   #
   #    It is a multiple-valued attribute. 
   #    This attribute's syntax is 'IA5 String'.
   #    Its case is significant.
   #
   attributetype ( 1.2.840.10008.15.0.3.30
       NAME 'dicomPreferredCallingAETitle'
       DESC 'AE Title(s) to which associations may be preferably accepted.'
       EQUALITY caseExactIA5Match
       SYNTAX 1.3.6.1.4.1.1466.115.121.1.26 )

   # 3.31  dicomSupportedCharacterSet        string    Multiple
   #
   #    The Character Set(s) supported by the Network AE for Data Sets it receives. 
   #    Contains one of the Defined Terms for Specific Character Set (0008,0005). 
   #    If not present, this implies that the Network AE supports only the default 
   #    character repertoire (ISO IR 6). 
   #
   #    It is a multiple-valued attribute. 
   #    This attribute's syntax is 'IA5 String'.
   #    Its case is significant.
   #
   attributetype ( 1.2.840.10008.15.0.3.31
       NAME 'dicomSupportedCharacterSet'
       DESC 'The Character Set(s) supported by the Network AE for Data Sets it receives.'
       EQUALITY caseExactIA5Match
       SYNTAX 1.3.6.1.4.1.1466.115.121.1.26 )

   # 3.31 dicomInstitutionDepartmentType    string   Multiple
   #
   #    This attribute stores the institution department type of the device. 
   #    Should be the same as the value of Institutional Department Type Code 
   #    Sequence (0008,1041) in SOP Instances created by this device.
   #    Types should be selected from the list of code values (0008,0100) 
   #    for Context ID 7030 in DICOM Part 16 when applicable. 
   #
   #    It is a multi-valued attribute.
   #    This attribute's syntax is 'IA5 String'.
   # 
   attributetype ( 1.2.840.10008.15.0.3.31
    NAME 'dicomInstitutionDepartmentType'
    DESC 'Institution department type of the device. Should be the same as the value of Institutional
          Department Type Code Sequence (0008,1041) in SOP Instances created by this device.'
    EQUALITY caseIgnoreMatch
    SUBSTR caseIgnoreSubstringsMatch
    SYNTAX 1.3.6.1.4.1.1466.115.121.1.26 )

   # 4 Object Class Definitions
   # 
   #    The following object classes are defined in this document. All are
   #    structural classes.
   # 
   #   Name                            Description
   #   ---------------------------     --------------------------
   #   dicomConfigurationRoot          root of the DICOM Configuration Hierarchy
   #   dicomDevicesRoot                root of the DICOM Devices Hierarchy
   #   dicomUniqueAETitlesRegistryRoot root of the Unique DICOM AE-Titles Registry Hierarchy
   #   dicomDevice                     Devices
   #   dicomNetworkAE                  Network AE
   #   dicomNetworkConnection          Network Connections
   #   dicomUniqueAETitle              Unique AE Title
   #   dicomTransferCapability         Transfer Capability

   # 
   # 4.1 dicomConfigurationRoot
   #
   #    This structural object class represents the root of the DICOM Configuration Hierarchy. 
   #    Only a single object of this type should exist within an organizational domain.
   #    Clients can search for an object of this class to locate the root of the 
   #    DICOM Configuration Hierarchy.
   #
   objectclass ( 1.2.840.10008.15.0.4.1
       NAME 'dicomConfigurationRoot'
       DESC 'Root of the DICOM Configuration Hierarchy'
       SUP top
       STRUCTURAL
       MUST ( cn ) 
       MAY ( description ) )

   #
   # 4.2 dicomDevicesRoot          
   #
   #    This structural object class represents the root of the DICOM Devices Hierarchy. 
   #    Only a single object of this type should exist as a child of dicomConfigurationRoot.
   #
   objectclass ( 1.2.840.10008.15.0.4.2
       NAME 'dicomDevicesRoot'
       DESC 'Root of the DICOM Devices Hierarchy'
       SUP top
       STRUCTURAL
       MUST ( cn ) 
       MAY ( description ) )

   #
   # 4.3 dicomUniqueAETitlesRegistryRoot           
   #
   #    This structural object class represents the root of the Unique DICOM AE-Titles 
   #    Registry Hierarchy. 
   #    Only a single object of this type should exist as a child of dicomConfigurationRoot.
   #
   objectclass ( 1.2.840.10008.15.0.4.3
       NAME 'dicomUniqueAETitlesRegistryRoot'
       DESC 'Root of the Unique DICOM AE-Title Registry Hierarchy'
       SUP top
       STRUCTURAL
       MUST ( cn ) 
       MAY ( description ) )

   #
   # 4.4 dicomDevice
   #
   #    This structural object class represents a DICOM Device.
   #
   objectclass ( 1.2.840.10008.15.0.4.4
       NAME 'dicomDevice'
       DESC 'DICOM Device related information'
       SUP top
       STRUCTURAL
       MUST ( 
           dicomDeviceName $
           dicomInstalled ) 
       MAY  ( 
           dicomDescription $
           dicomManufacturer $
           dicomManufacturerModelName $
           dicomSoftwareVersion $
           dicomStationName $
           dicomDeviceSerialNumber $
           dicomInstitutionName $
           dicomInstitutionAddress $
           dicomInstitutionDepartmentName $
           dicomIssuerOfPatientID $
           dicomVendorData $
           dicomPrimaryDeviceType $
           dicomRelatedDeviceReference $
           dicomAuthorizedNodeCertificateReference $
           dicomThisNodeCertificateReference) )

   #
   # 4.5 dicomNetworkAE
   #
   #    This structural object class represents a Network Application Entity
   #
   objectclass ( 1.2.840.10008.15.0.4.5
       NAME 'dicomNetworkAE'
       DESC 'DICOM Network AE related information'
       SUP top
       STRUCTURAL
       MUST (
           dicomAETitle $ 
           dicomNetworkConnectionReference $
           dicomAssociationInitiator $
           dicomAssociationAcceptor )
       MAY ( 
           dicomDescription $
           dicomVendorData $
           dicomApplicationCluster $
           dicomPreferredCalledAETitle $
           dicomPreferredCallingAETitle $
           dicomSupportedCharacterSet $
           dicomInstalled ) )

   #
   # 4.6 dicomNetworkConnection
   #
   #    This structural object class represents a Network Connection
   #
   objectclass ( 1.2.840.10008.15.0.4.6
       NAME 'dicomNetworkConnection'
       DESC 'DICOM Network Connection information'
       SUP top
       STRUCTURAL
       MUST ( dicomHostname )
       MAY ( 
           cn $
           dicomPort $
           dicomTLSCipherSuite $
           dicomInstalled ) )

   #
   # 4.7 dicomUniqueAETitle
   #
   #    This structural object class represents a Unique Application Entity Title
   #
   objectclass ( 1.2.840.10008.15.0.4.7
       NAME 'dicomUniqueAETitle'
       DESC 'A Unique DICOM Application Entity title'
       SUP top
       STRUCTURAL
       MUST ( dicomAETitle ) )

   #
   # 4.8 dicomTransferCapability
   #
   #    This structural object class represents Transfer Capabilities for an Application Entity
   #
   objectclass ( 1.2.840.10008.15.0.4.8
       NAME 'dicomTransferCapability'
       DESC 'Transfer Capabilities for an Application Entity'
       SUP top
       STRUCTURAL
       MUST (
           dicomSOPClass $
           dicomTransferRole $
           dicomTransferSyntax)
       MAY (
           cn) )

     

.. _sect_H.1.4:

Transactions
~~~~~~~~~~~~

.. _sect_H.1.4.1:

Find LDAP Server
^^^^^^^^^^^^^^^^

.. _sect_H.1.4.1.1:

Scope
'''''

The `biblioentry_title <#biblio_RFC_2782>`__ *A DNS RR for specifying
the location of services (DNS SRV)* specifies a mechanism for requesting
the names and rudimentary descriptions for machines that provide network
services. The DNS client requests the descriptions for all machines that
are registered as offering a particular service name. In this case the
service name requested will be "LDAP". The DNS server may respond with
multiple names for a single request.

.. _sect_H.1.4.1.2:

Use Case Roles
''''''''''''''

DNS Server
   Provides list of LDAP servers

LDAP Client
   Requests list of LDAP servers

.. _sect_H.1.4.1.3:

Referenced Standards
''''''''''''''''''''

`biblioentry_title <#biblio_RFC_2181>`__ Clarifications to the DNS
Specification

`biblioentry_title <#biblio_RFC_2219>`__ Use of DNS Aliases for Network
Services

`biblioentry_title <#biblio_RFC_2782>`__ A DNS RR for specifying the
location of services (DNS SRV)

other RFC's are included by reference from
`biblioentry_title <#biblio_RFC_2181>`__,
`biblioentry_title <#biblio_RFC_2219>`__, and
`biblioentry_title <#biblio_RFC_2782>`__.

.. _sect_H.1.4.1.4:

Interaction Diagram
'''''''''''''''''''

The DNS client shall request a list of all the LDAP servers available.
It will use the priority, capacity, and location information provided by
DNS to select a server (`biblioentry_title <#biblio_RFC_2782>`__
recommends the proper use of these parameters). It is possible that
there is no LDAP server, or that the DNS server does not support the SRV
RR request.

.. note::

   1. Multiple LDAP servers providing access to a common replicated LDAP
      database is a commonly supported configuration. This permits LDAP
      servers to be located where appropriate for best performance and
      fault tolerance. The DNS server response information provides
      guidance for selecting the most appropriate server.

   2. There may also be multiple LDAP servers providing different
      databases. In this situation the client may have to examine
      several servers to find the one that supports the DICOM
      configuration database. Similarly a single LDAP server may support
      multiple base DNs, and the client will need to check each of these
      DNs to determine which is the DICOM supporting tree.

.. _sect_H.1.4.1.5:

Alternative Paths
'''''''''''''''''

The client may have a mechanism for manual default selection of the LDAP
server to be used if the DNS server does not provide an LDAP server
location.

.. _sect_H.1.4.2:

Query LDAP Server
^^^^^^^^^^^^^^^^^

.. _sect_H.1.4.2.1:

Scope
'''''

The `biblioentry_title <#biblio_RFC_2251>`__ "Lightweight Directory
Access Protocol (v3)" specifies a mechanism for making queries of a
database corresponding to an LDAP schema. The LDAP client can compose
requests in the LDAP query language, and the LDAP server will respond
with the results for a single request.

.. _sect_H.1.4.2.2:

Use Case Roles
''''''''''''''

LDAP Server
   Provides query response

LDAP Client
   Requests LDAP information

.. _sect_H.1.4.2.3:

Referenced Standards
''''''''''''''''''''

`biblioentry_title <#biblio_RFC_2251>`__ Lightweight Directory Access
Protocol (v3). LDAP support requires compliance with other RFC's invoked
by reference.

.. _sect_H.1.4.2.4:

Interaction Description
'''''''''''''''''''''''

The LDAP client may make a wide variety of queries and cascaded queries
using LDAP. The LDAP client and server shall support the Application
Configuration Data Model .

.. note::

   Multiple LDAP servers providing access to a common replicated LDAP
   database is a commonly supported configuration. This permits LDAP
   servers to be located where appropriate for best performance and
   fault tolerance. The replications rules chosen for the LDAP servers
   affect the visible data consistency. LDAP permits inconsistent views
   of the database during updates and replications.

.. _sect_H.1.4.3:

Update LDAP Server
^^^^^^^^^^^^^^^^^^

.. _sect_H.1.4.3.1:

Scope
'''''

The `biblioentry_title <#biblio_RFC_2251>`__ "Lightweight Directory
Access Protocol (v3)" specifies a mechanism for making updates to a
database corresponding to an LDAP schema. The LDAP client can compose
updates in the LDAP query language, and the LDAP server will respond
with the results for a single request. Update requests may be refused
for security reasons.

.. _sect_H.1.4.3.2:

Use Case Roles
''''''''''''''

LDAP Server
   Maintains database

LDAP Client
   Updates LDAP information

.. _sect_H.1.4.3.3:

Referenced Standards
''''''''''''''''''''

`biblioentry_title <#biblio_RFC_2251>`__ Lightweight Directory Access
Protocol (v3). LDAP support requires compliance with other RFC's invoked
by reference.

.. _sect_H.1.4.3.4:

Interaction Description
'''''''''''''''''''''''

The LDAP client may make a request to update the LDAP database. The LDAP
client shall support the data model described above. The LDAP server may
choose to refuse the update request for security reasons. If the LDAP
server permits update requests, is shall support the data model
described above.

.. note::

   Multiple LDAP servers providing access to a common replicated LDAP
   database is a commonly supported configuration. This permits LDAP
   servers to be located where appropriate for best performance and
   fault tolerance. Inappropriate selection of replication rules in the
   configuration of the LDAP server will result in failure for AE-title
   uniqueness when creating the AE-titles objects.

.. _sect_H.1.4.3.5:

Special Update For Network AE Creation
''''''''''''''''''''''''''''''''''''''

The creation of a new Network AE requires special action. The following
steps shall be followed:

a. A tentative AE title shall be selected. Various algorithms are
   possible, ranging from generating a random name to starting with a
   preset name template and incrementing a counter field. The client may
   query the Unique AE Titles Registry sub-tree to obtain the complete
   list of names that are presently in use as part of this process.

b. A new Unique AE Title object shall be created in the Unique AE Titles
   Registry portion of the hierarchy with the tentative name. The LDAP
   server enforces uniqueness of names at any specific point in the
   hierarchy.

c. If the new object creation was successful, this shall be the AE Title
   used for the new Network AE.

d. If the new object creation fails due to non-unique name, return to a)
   and select another name.

.. _sect_H.1.4.4:

Maintain LDAP Server
^^^^^^^^^^^^^^^^^^^^

The LDAP server shall support a separate manual or automated means of
maintaining the LDAP database contents. The LDAP server shall support
the `biblioentry_title <#biblio_RFC_2849>`__ file format mechanism for
updating the LDAP database. The LDAP Client or service installation
tools shall provide `biblioentry_title <#biblio_RFC_2849>`__ formatted
files to update LDAP server databases manually. The LDAP server may
refuse client network updates for security reasons. If this is the case,
then the maintenance process will be used to maintain the LDAP database.

The manual update procedures are not specified other than the
requirement above that at least the minimal LDAP information exchange
file format from `biblioentry_title <#biblio_RFC_2849>`__ be supported.
The exact mechanisms for transferring this information remain vendor and
site specific. In some situations, for example the creation of
AE-titles, a purely manual update mechanism may be easier than
exchanging files.

The conformance statement shall document the mechanisms available for
transferring this information. Typical mechanisms include:

a. floppy disk

b. CD-R

c. SSH

d. Secure FTP

e. FTP

f. email

g. HTTPS

.. note::

   1. There are many automated and semi-automatic tools for maintaining
      LDAP databases. Many LDAP servers provide GUI interfaces and
      updating tools. The specifics of these tools are outside the scope
      of DICOM. The LDAP `biblioentry_title <#biblio_RFC_2849>`__
      requires at least a minimal data exchange capability. There are
      also XML based tools for creating and maintaining these files.

   2. This mechanism may also be highly effective for preparing a new
      network installation by means of a single pre-planned network
      configuration setup rather than individual machine updates.

.. _sect_H.1.5:

LDAP Security Considerations (Informative)
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

.. _sect_H.1.5.1:

Threat Assessment
^^^^^^^^^^^^^^^^^

The threat and value for the LDAP based configuration mechanisms fall
into categories:

a. AE-uniqueness mechanism

b. Finding (and updating) Network AE descriptions

c. Finding (and updating) device descriptions

These each pose different vulnerabilities to attack. These are:

a. Active Attacks

   1. The AE-title uniqueness mechanism could be attacked by creating
      vast numbers of spurious AE-titles. This could be a Denial of
      Service (DoS) attack on the LDAP server. It has a low probability
      of interfering with DICOM operations.

   2. The Network AE information could be maliciously updated. This
      would interfere with DICOM operations by interfering with finding
      the proper server. It could direct connections to malicious nodes,
      although the use of TLS authentication for DICOM connections would
      detect such misdirection. When TLS authentication is in place this
      becomes a DoS attack.

   3. The device descriptions could be maliciously modified. This would
      interfere with proper device operation.

b. Passive Attacks

   1. There is no apparent value to an attacker in obtaining the current
      list of AE-titles. This does not indicate where these AE-titles
      are deployed or on what equipment.

   2. The Network AE information and device descriptions might be of
      value in determining the location of vulnerable systems. If it is
      known that a particular model of equipment from a particular
      vendor is vulnerable to a specific attack, then the Network AE
      Information can be used to find that equipment.

.. _sect_H.1.5.2:

Available LDAP Security Mechanisms
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

The security mechanisms for LDAP are highly variable in actual
implementations. They are a mixture of administrative restrictions and
protocol implementations. The widely available options for security
methods are:

a. Anonymous access, where there is no restriction on performing this
   function over the network.

b. Basic, where there is a username and password exchange prior to
   granting access to this function. The exchange is vulnerable to
   snooping, spoofing, and man in the middle attacks.

c. TLS, where there is an SSL/TLS exchange during connection
   establishment.

d. Manual, where no network access is permitted and the function must be
   performed manually at the server, or semi-automatically at the
   server. The semi-automatic means permit the use of independently
   exchanged files (e.g., via floppy) together with manual commands at
   the server.

The categories of functions that may be independently controlled are:

a. Read related, to read, query, or otherwise obtain a portion of the
   LDAP directory tree

b. Update related, to modify previously existing objects in the
   directory tree

c. Create, to create new objects in the directory tree.

Finally, these rules may be applied differently to different subtrees
within the overall LDAP structure. The specific details of Access
Control Lists (ACLs), functional controls, etc. vary somewhat between
different LDAP implementations.

.. _sect_H.1.5.3:

Recommendations (Informative)
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

The LDAP server should be able to specify different restrictions for the
AE-Title list and for the remainder of the configuration information. To
facilitate interoperability, `table_title <#table_H.1-15>`__ defines
several patterns for access control. They correspond to different
assessments of risk for a network environment.

.. table:: LDAP Security Patterns

   +---------+---------+---------+---------+---------+---------+---------+
   |         | **TLS** | **TLS-M | **      | **      | **Anon  | **Anon  |
   |         |         | anual** | Basic** | Basic-M | ymous** | ymous-M |
   |         |         |         |         | anual** |         | anual** |
   +=========+=========+=========+=========+=========+=========+=========+
   | **Read  | Ano     | Ano     | Ano     | Ano     | An      | An      |
   | AE-     | nymous, | nymous, | nymous, | nymous, | onymous | onymous |
   | title** | TLS     | TLS     | Basic   | Basic   |         |         |
   +---------+---------+---------+---------+---------+---------+---------+
   | *       | TLS     | Manual  | Basic   | Manual  | An      | Manual  |
   | *Create |         |         |         |         | onymous |         |
   | AE-     |         |         |         |         |         |         |
   | Title** |         |         |         |         |         |         |
   +---------+---------+---------+---------+---------+---------+---------+
   | **Read  | TLS     | TLS     | Basic   | Basic   | An      | An      |
   | C       |         |         |         |         | onymous | onymous |
   | onfig** |         |         |         |         |         |         |
   +---------+---------+---------+---------+---------+---------+---------+
   | *       | TLS     | Manual  | Basic   | Manual  | An      | Manual  |
   | *Update |         |         |         |         | onymous |         |
   | C       |         |         |         |         |         |         |
   | onfig** |         |         |         |         |         |         |
   +---------+---------+---------+---------+---------+---------+---------+
   | *       | TLS     | Manual  | Basic   | Manual  | An      | Manual  |
   | *Create |         |         |         |         | onymous |         |
   | C       |         |         |         |         |         |         |
   | onfig** |         |         |         |         |         |         |
   +---------+---------+---------+---------+---------+---------+---------+

TLS
   This pattern provides SSL/TLS authentication and encryption between
   client and server. It requires additional setup during installation
   because the TLS certificate information needs to be installed onto
   the client machines and server. Once the certificates are installed
   the clients may then perform full updating operations.

TLS-Manual
   This pattern provides SSL/TLS controls for read access to information
   and require manual intervention to perform update and creation
   functions.

Basic
   This pattern utilizes the LDAP basic security to gain access to the
   LDAP database. It requires the installation of a password during
   client setup. It does not provide encryption protection. Once the
   password is installed, the client can then perform updates.

Basic-Manual
   This pattern utilizes basic security protection for read access to
   the configuration information and requires manual intervention to
   perform update and creation functions.

Anonymous
   This pattern permits full read/update access to all machines on the
   network.

Anonymous-Manual
   This pattern permits full read access to all machines on the network,
   but requires manual intervention to perform update and creation.

A client or server implementation may be capable of being configured to
support multiple patterns. This should be documented in the conformance
claim. The specific configuration in use at a specific site can then be
determined at installation time.

.. _sect_H.1.6:

Implementation Considerations (Informative)
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

The LDAP database can be used as a documentation tool. Documenting the
configuration for both managed and legacy machines makes upgrading
easier and reduces the error rate for manually configured legacy
equipment.

There are various possible implementation strategies for clients
performing lookups within the LDAP database. For example, before
initiating a DICOM association to a specific AE, a client implementation
could either:

a. Query the LDAP database to obtain hostname and port for the specific
   AE Title immediately prior to initiating a DICOM association.

b. Maintain a local cache of AE Title, hostname and port information and
   only query the LDAP database if the specific AE Title is not found in
   the local cache.

The advantages of maintaining a local cache include performance (by
avoiding frequent lookups) and reliability (should the LDAP server be
temporarily unavailable). The disadvantage of a cache is that it can
become outdated over time. Client implementations should provide
appropriate mechanisms to purge locally cached information.

Client caches may cause confusion during updates. Manual steps may be
needed to trigger immediate updates. LDAP database replication also may
introduce delays and inconsistencies. Database replication may also
require manual intervention to force updates to occur immediately.

One strategy to reduce client cache problems is to re-acquire new DNS
and LDAP information after any network association information. Often
the first symptom of stale cache information is association failures due
to the use of obsolete configuration information.

Some LDAP servers do not support a "modify DN" operation. For example,
in the case of renaming a device on such a server, a tree copy operation
may be needed to create a new object tree using the new name, followed
by removal of the old object tree. After such a rename the device may
need to search using other attributes when finding its own configuration
information, e.g., the device serial number.

.. _sect_H.1.7:

Conformance
~~~~~~~~~~~

The Conformance Statement for an LDAP Client or LDAP Server
implementation shall specify the security pattern(s) that it supports.

.. _sect_H.2:

DNS Service Discovery
---------------------

.. _sect_H.2.1:

Scope
~~~~~

Service discovery mechanisms provide a means for devices to announce
their presence and seek information about the existence of other
services on the network. Many of these mechanisms are DNS-based.

The exact use of such protocols as DNS Service Discovery (DNS-SD),
Multi-cast DNS (mDNS) and DNS Dynamic Updates is defined in RFC's
referenced by DICOM. This section standardizes the name to be used in
DNS SRV records for such purposes, and the DNS TXT records that encode
accompanying parameters.

Security issues associated with self-discovery are out of scope. See
`DNS Security Considerations (Informative) <#sect_F.1.1.4>`__ for the
informative discussion on DNS Security issues.

.. _sect_H.2.2:

Use Case Roles
~~~~~~~~~~~~~~

DNS Server
   Provides list of DICOM Association Acceptors

DNS Client
   Requests list of DICOM Association Acceptors

.. _sect_H.2.3:

Referenced Standards
~~~~~~~~~~~~~~~~~~~~

`biblioentry_title <#biblio_RFC_2136>`__ DNS Dynamic Updates

`biblioentry_title <#biblio_RFC_2181>`__ Clarifications to the DNS
Specification

`biblioentry_title <#biblio_RFC_2219>`__ Use of DNS Aliases for Network
Services

`biblioentry_title <#biblio_RFC_2782>`__ A DNS RR for specifying the
location of services (DNS SRV)

`biblioentry_title <#biblio_RFC_6762>`__ Multicast DNS

`biblioentry_title <#biblio_RFC_6763>`__ DNS-Based Service Discovery

`biblioentry_title <#biblio_RFC_8553>`__ DNS AttrLeaf Changes

`biblioentry_title <#biblio_DNSSD>`__ DNS Self-Discovery

The name to be used in the DNS SRV to advertise DICOM Association
Acceptors, regardless of the SOP Class(es) supported, shall be

-  "dicom" for unsecured DICOM communication

-  "dicom-tls" for the Basic TLS Secure Transport Connection Profile

-  "dicom-iscl" for ISCL Transport Connection Profile

-  "dicomweb" for DICOM web services over unsecured http

-  "dicomweb-tls" for DICOM web services over https

.. note::

   These choices are consistent with the names registered with IANA to
   define the mapping of IP ports to services, which is conventional for
   this usage. The choice "dicom" is used rather than the "acr-nema"
   alternative for clarity. There is no implied port choice by the usage
   in the DNS SRV Service Type, since the port is explicitly conveyed.

The DNS TXT record may contain the following parameters:

-  AET= *<application entity title>*, where the value *<application
   entity title>*\ is to be used as the Called Application Entity Title
   when initiating Associations to the device

-  PrimaryDeviceType= *<primary device type>*, where the value *<primary
   device type>*\ is as defined `table_title <#table_H.1-2>`__
   Attributes of Device Object

-  DICOMWebPath= *<service>*, where the value *<service>* is the *path*
   component of the DICOM Web Service root as defined in

In the absence of a DNS TXT record, or the AET parameter of the DNS TXT
record, then the Instance Name preceding the Service Type in the DNS SRV
record used for DICOM service discovery shall be the AET.

.. note::

   Further parameters are not specified, for example to indicate the SOP
   Classes supported or other information, since the size of DNS records
   encoded as UDP datagrams is strictly limited, and furthermore, the
   envisaged multicast usage encourages the exchange of the minimal
   information necessary. The existing DICOM association negotiation
   mechanism can be used to explore the SOP Classes offered once the IP
   address, port number and AET are known. The primary device type is
   supplied because it is useful to indicate to users the type of
   device, which is not conveyed during association establishment.

.. _sect_H.2.4:

Examples
~~~~~~~~

Example SRV record:

-  \_dicomweb-tls._tcp. examplehospital.org 86400 IN SRV 10 60 443
   dicomweb.examplehospital.org.

Example TXT record:

-  dicomweb.examplehospital.org IN TXT "DICOMWebPath=apps/dicom-rs"

The above examples would combine to define a DICOM web service root of:

-  "https://dicomweb.examplehospital.org:443/apps/dicom-rs"

.. _sect_H.2.5:

Conformance
~~~~~~~~~~~

An implementation that supports this profile shall state in its
Conformance Statement whether it supports reading (DNS Client) or
writing DNS (DNS Server) records.

An implementation that supports this profile shall state in its
Conformance Statement whether it supports DNSSEC
`biblioentry_title <#biblio_RFC_4033>`__
`biblioentry_title <#biblio_RFC_4034>`__
`biblioentry_title <#biblio_RFC_4035>`__ for the interactions described
in this profile, in which case either the options supported shall be
stated or a reference provided to the DNSSEC support for this product.
