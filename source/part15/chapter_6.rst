.. _chapter_6:

Security and System Management Profile Outlines
===============================================

An implementation may claim conformance to any of the Security and
System Management Profiles individually. It may also claim conformance
to more than one Security or System Management Profile. It shall
indicate in its Conformance Statement how it chooses which profiles to
use for any given transaction.

.. _sect_6.1:

Secure Use Profiles
-------------------

An implementation may claim conformance to one or more Secure Use
Profiles. Such profiles outline the use of attributes and other Security
Profiles in a specific fashion.

Secure Use Profiles are specified in `Secure Use Profiles
(Normative) <#chapter_A>`__.

.. _sect_6.2:

Secure Transport Connection Profiles
------------------------------------

An implementation may claim conformance to one or more Secure Transport
Connection Profiles.

A Secure Transport Connection Profile includes the following
information:

a. Description of the protocol framework and negotiation mechanisms

b. Description of the entity authentication an implementation shall
   support

   1. The identity of the entities being authenticated

   2. The mechanism by which entities are authenticated

   3. Any special considerations for audit log support

c. Description of the encryption mechanism an implementation shall
   support

   1. The method of distributing session keys

   2. The encryption protocol and relevant parameters

d. Description of the integrity check mechanism an implementation shall
   support

Secure Transport Connection Profiles are specified in `Secure Transport
Connection Profiles (Normative) <#chapter_B>`__.

.. _sect_6.3:

Digital Signature Profile
-------------------------

An implementation may claim conformance to one or more Digital Signature
Profiles.

A Digital Signature profile consists of the following information:

a. The role that the Digital Signature plays, including:

   1. Who or what entity the Digital Signature represents.

   2. A description of the purpose of the Digital Signature.

   3. The conditions under which the Digital Signature is included in
      the Data Set.

b. A list of Attributes that shall be included in the Digital Signature.

c. The mechanisms that shall be used to generate or verify the Digital
   Signature, including:

   1. The algorithm and relevant parameters that shall be used to create
      the MAC or hash code, including the Value to be used for the MAC
      Algorithm (0400,0015) Attribute.

   2. The encryption algorithm and relevant parameters that shall be
      used to encrypt the MAC or hash code in forming the Digital
      Signature.

   3. The certificate type or key distribution mechanism that shall be
      used, including the Value to be used for the Certificate Type
      (0400,0110) Attribute.

   4. Any requirements for the Certified Timestamp Type (0400,0305) and
      Certified Timestamp (0400,0310) Attributes.

d. Any special requirements for identifying the signatory.

e. The relationship with other Digital Signatures, if any.

f. Any other factors needed to create, verify, or interpret the Digital
   Signature

Digital Signature Profiles are specified in `Digital Signature Profiles
(Normative) <#chapter_C>`__.

.. _sect_6.4:

Media Storage Security Profiles
-------------------------------

An implementation may claim conformance to one or more Media Storage
Application Profiles, which in turn require conformance to one or more
Media Storage Security Profiles.

.. note::

   An implementation may not claim conformance to a Media Storage
   Security Profile without claiming conformance to a Media Storage
   Application Profile.

A Media Storage Security Profile includes the following specifications:

a. What aspects of security are addressed by the profile.

b. The restrictions on the types of DICOM Files that can be secured, if
   any.

c. How the DICOM Files will be encapsulated and secured.

Media Storage Security Profiles are specified in `Media Storage Security
Profiles (Normative) <#chapter_D>`__.

.. _sect_6.5:

Network Address Management Profiles
-----------------------------------

An implementation may claim conformance to one or more Network Address
Management Profiles. Such profiles outline the use of non-DICOM network
protocols to obtain the network addresses for the implementation.

Network Address Management Profiles are specified in `Network Address
Management Profiles <#chapter_F>`__.

.. _sect_6.6:

Time Synchronization Profiles
-----------------------------

An implementation may claim conformance to one or more Time
Synchronization Profiles. Such profiles outline the use of non-DICOM
protocols to set the current time for the implementation.

Time Synchronization Profiles are specified in `Time Synchronization
Profiles <#chapter_G>`__.

.. _sect_6.7:

Application Configuration Management Profiles
---------------------------------------------

An implementation may claim conformance to one or more Application
Configuration Management Profiles. Such profiles outline the use of
non-DICOM network protocols to obtain the descriptions, addresses and
capabilities of other devices with which the implementation may
communicate using the DICOM Protocol. They also specify the use of those
non-DICOM protocols for the implementation to publish or announce its
description, addresses and capabilities. They also specify how
implementation specific configuration information can be obtained by
devices.

Application Configuration Management Profiles are specified in
`Application Configuration Management Profiles <#chapter_H>`__.

.. _sect_6.8:

Audit Trail Profiles
--------------------

An implementation may claim conformance to one or more Audit Trail
Profiles. Such profiles outline the generation and transport of audit
messages for security and privacy policy enforcement.

Audit Trail Profiles are specified in `Secure Use Profiles
(Normative) <#chapter_A>`__.

