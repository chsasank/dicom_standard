.. _chapter_1:

Scope and Field of Application
==============================

This Part of the DICOM Standard specifies Security and System Management
Profiles to which implementations may claim conformance. Security and
System Management Profiles are defined by referencing externally
developed standard protocols, such as TLS, ISCL, DHCP, and LDAP, with
attention to their use in a system that uses DICOM Standard protocols
for information interchange.

.. _sect_1.1:

Security Policies and Mechanisms
--------------------------------

The DICOM Standard does not address issues of security policies, though
clearly adherence to appropriate security policies is necessary for any
level of security. The Standard only provides mechanisms that could be
used to implement security policies with regard to the interchange of
DICOM objects between Application Entities. For example, a security
policy may dictate some level of access control. This Standard does not
consider access control policies, but does provide the technological
means for the Application Entities involved to exchange sufficient
information to implement access control policies.

This Standard assumes that the Application Entities involved in a DICOM
interchange are implementing appropriate security policies, including,
but not limited to access control, audit trails, physical protection,
maintaining the confidentiality and integrity of data, and mechanisms to
identify users and their rights to access data. Essentially, each
Application Entity must insure that their own local environment is
secure before even attempting secure communications with other
Application Entities.

When Application Entities agree to interchange information via DICOM
through association negotiation, they are essentially agreeing to some
level of trust in the other Application Entities. Primarily Application
Entities trust that their communication partners will maintain the
confidentiality and integrity of data under their control. Of course
that level of trust may be dictated by local security and access control
policies.

Application Entities may not trust the communications channel by which
they communicate with other Application Entities. Thus, this Standard
provides mechanisms for Application Entities to securely authenticate
each other, to detect any tampering with or alteration of messages
exchanged, and to protect the confidentiality of those messages while
traversing the communications channel. Application Entities can
optionally utilize any of these mechanisms, depending on the level of
trust they place in the communications channel.

This Standard assumes that Application Entities can securely identify
local users of the Application Entity, and that user's roles or
licenses. Note that users may be persons, or may be abstract entities,
such as organizations or pieces of equipment. When Application Entities
agree to an exchange of information via DICOM, they may also exchange
information about the users of the Application Entity via the
Certificates exchanged in setting up the secure channel. The Application
Entity may then consider the information contained in the Certificates
about the users, whether local or remote, in implementing an access
control policy or in generating audit trails.

This Standard also assumes that Application Entities have means to
determine whether or not the "owners" (e.g., patient, institution) of
information have authorized particular users, or classes of users to
access information. This Standard further assumes that such
authorization might be considered in the access control provided by the
Application Entity. At this time, this Standard does not consider how
such authorization might be communicated between Application Entities,
though that may be a topic for consideration at some future date.

This Standard also assumes that an Application Entity using TLS has
secure access to or can securely obtain
`biblioentry_title <#biblio_ITU-T_X.509>`__ key Certificates for the
users of the application entity. In addition, this Standard assumes that
an Application Entity has the means to validate an
`biblioentry_title <#biblio_ITU-T_X.509>`__ certificate that it
receives. The validation mechanism may use locally administered
authorities, publicly available authorities, or some trusted third
party.

This Standard assumes that an Application Entity using ISCL has access
to an appropriate key management and distribution system (e.g.,
smartcards). The nature and use of such a key management and
distribution system is beyond the scope of DICOM, though it may be part
of the security policies used at particular sites.

.. _sect_1.2:

System Management Profiles
--------------------------

The System Management Profiles specified in this Part are designed to
support automation of the configuration management processes necessary
to operate a system that uses DICOM Standard protocols for information
interchange.

This Part assumes that the Application Entities may operate in a variety
of network environments of differing complexity. These environments may
range from a few units operating on an isolated network, to a
department-level network with some limited centralized network support
services, to an enterprise-level network with significant network
management services. Note that the System Management Profiles are
generally addressed to the implementation, not to Application Entities.
The same Profiles need to be supported by the different applications on
the network.

