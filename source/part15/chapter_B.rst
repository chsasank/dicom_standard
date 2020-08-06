.. _chapter_B:

Secure Transport Connection Profiles (Normative)
================================================

.. _sect_B.1:

Basic TLS Secure Transport Connection Profile
---------------------------------------------

Retired. See PS3.15 2018a.

.. _sect_B.2:

ISCL Secure Transport Connection Profile
----------------------------------------

Retired. See PS3.15 2018a.

.. _sect_B.3:

AES TLS Secure Transport Connection Profile
-------------------------------------------

Retired. See PS3.15 2018a.

.. note::

   Applications implementing the AES TLS Secure Transport Connection
   Profile will connect and interoperate with implementations of the BCP
   195 TLS Profile; see `BCP 195 TLS Secure Transport Connection
   Profile <#sect_B.9>`__.

.. _sect_B.4:

Basic User Identity Association Profile
---------------------------------------

An implementation that supports the Basic User Identity Association
profile shall accept the User Identity association negotiation sub-item,
for User-Identity-Type of 1 or 2. It need not verify the passcode. If a
positive response is requested, the implementation shall respond with
the association response sub-item.

The user identity from the Primary-field shall be used within the
implementation as the user identification. Such uses include recording
user identification in audit messages.

.. table:: Minimum Mechanisms for DICOM Association Negotiation Features
- Basic User Identity Association Profile

   ========================================= =================
   Supported Association Negotiation Feature Minimum Mechanism
   ========================================= =================
   User Identity                             Username
   ========================================= =================

.. _sect_B.5:

User Identity Plus Passcode Association Profile
-----------------------------------------------

An implementation that supports the User Identity plus Passcode
Association Profile shall send/accept the User Identity association
negotiation sub-item, for User-Identity-Type of 2. If a positive
response is requested, the association acceptor implementation shall
respond with the association response sub-item. The passcode information
shall be made available to internal or external authentication systems.
The user identity shall be authenticated by means of the passcode and
the authentication system. If the authentication fails, the association
shall be rejected.

The user identity from the Primary-field shall be used within the
implementation as the user identification. Such uses include recording
user identification in audit messages.

.. table:: User Identity Plus Passcode Association Profile - Minimum
Mechanisms for DICOM Association Negotiation Features

   ========================================= =====================
   Supported Association Negotiation Feature Minimum Mechanism
   ========================================= =====================
   User Identity                             Username and Passcode
   ========================================= =====================

.. _sect_B.6:

Kerberos Identity Negotiation Association Profile
-------------------------------------------------

An implementation that supports the Kerberos Identity Negotiation
Association Profile shall send/accept the User Identity association
negotiation sub-item, for User-Identity-Type of 3. If a positive
response is requested, the association acceptor implementation shall
respond with the association response sub-item containing a Kerberos
server ticket. The Kerberos server ticket information shall be made
available to internal or external Kerberos authentication systems. The
user identity shall be authenticated by means of the Kerberos
authentication system. If the authentication fails, the association
shall be rejected.

The user identity from the Primary-field shall be used within the
implementation as the user identification. Such uses include recording
user identification in audit messages.

.. table:: Kerberos Identity Negotiation Association Profile - Minimum
Mechanisms for DICOM Association Negotiation Features

   ========================================= =================
   Supported Association Negotiation Feature Minimum Mechanism
   ========================================= =================
   User Identity                             Kerberos
   ========================================= =================

.. _sect_B.7:

Generic SAML Assertion Identity Negotiation Association Profile
---------------------------------------------------------------

An implementation that supports the Generic SAML Assertion Identity
Negotiation Association Profile shall send/accept the User Identity
association negotiation sub-item, for User-Identity-Type of 4. If a
positive response is requested, the association acceptor implementation
shall respond with the association response sub-item containing a SAML
response. The SAML Assertion information shall be made available to
internal or external authentication systems. The user identity shall be
authenticated by means of an authentication system that employs SAML
Assertions. If the authentication fails, the association shall be
rejected.

The user identity from the Primary-field shall be used within the
implementation as the user identification. Such uses include recording
user identification in audit messages.

.. table:: Generic SAML Assertion Identity Negotiation Association
Profile - Minimum Mechanisms for DICOM Association Negotiation Features

   ========================================= =================
   Supported Association Negotiation Feature Minimum Mechanism
   ========================================= =================
   User Identity                             SAML Assertion
   ========================================= =================

.. _sect_B.8:

Secure Use of Email Transport
-----------------------------

When a DICOM File Set is sent over Email transport in compliance with
this profile the following rules shall be followed:

a. The File Set shall be an attachment to the email body.

b. The entire email (body, File Set attachment, and any other
   attachments) shall be encrypted using AES, in accordance with
   `biblioentry_title <#biblio_RFC_3851>`__ and
   `biblioentry_title <#biblio_RFC_3853>`__.

c. The email body and attachments may be compressed in accordance with
   `biblioentry_title <#biblio_RFC_3851>`__.

d. The email shall be digitally signed by the sender. The signing may be
   applied before or after encryption. This digital signature shall be
   interpreted to mean that the sender is attesting to his authorization
   to disclose the information in this email to the recipient.

The email signature is present to provide minimum sender information and
to confirm the integrity of the email transmission (body contents,
attachment, etc.). The email signature is separate from other signatures
that may be present in DICOM reports and objects contained in the File
set attached to the email. Those signatures are defined in terms of
clinical uses. Any clinical content attestations shall be encoded as
digital signatures in the DICOM SOP instances, not as the email
signature. The email may be composed by someone who cannot make clinical
attestations. Through the use of the email signature, the composer
attests that he or she is authorized to transmit the data to the
recipient.

.. note::

   1. This profile is separate from the underlying use of ZIP File or
      other File Set packaging over email.

   2. Where private information is being conveyed, most country
      regulations require the use of encryption or equivalent
      protections. This Profile meets the most common requirements of
      regulations, but there may be additional local requirements.
      Additional requirements may include mandatory statements in the
      email body and prohibitions on contents of the email body to
      protect patient privacy.

.. _sect_B.9:

BCP 195 TLS Secure Transport Connection Profile
-----------------------------------------------

An implementation that supports the
`biblioentry_title <#biblio_BCP_195>`__ TLS Profile shall utilize the
framework and negotiation mechanism specified by the Transport Layer
Security protocol. It shall comply with
`biblioentry_title <#biblio_BCP_195>`__ from the IETF.

.. note::

   1. `biblioentry_title <#biblio_BCP_195>`__ is currently also
      published as `biblioentry_title <#biblio_RFC_7525>`__. Both
      provide suggestions for proper use of TLS 1.2 and allow
      appropriate fallback rules.

   2. Existing implementations that are compliant with the DICOM AES TLS
      Secure Connection Profile are able to interoperate with this
      profile. This profile adds significant recommendations by the
      IETF, but does not make them mandatory. This is the IETF
      recommendation for upgrading an installed base.

   3. A device may support multiple different TLS profiles. DICOM does
      not specify how such devices are configured in the field or how
      different TLS profile-related rules are specified. The site will
      determine what configuration is appropriate.

   4. The DICOM profiles for TLS describe the capabilities of a product.
      Product configuration may permit selection of a particular profile
      and/or additional negotiation rules. The specific ciphersuite used
      is negotiated by the TLS implementation based on these rules.

TCP ports on which an implementation accepts TLS connections, or the
mechanism by which these port numbers are selected or configured, shall
be stated in the Conformance Statement. The TCP ports on which an
implementation accepts TLS connections for DICOMweb shall be different
from those on which an implementation accepts TLS connections for DIMSE.
The HTTP/HTTPS connection for DICOMweb can be shared with other
HTTP/HTTPS traffic.

.. note::

   It is recommended that systems supporting the BCP 195 TLS Profile use
   the registered port number "2762 dicom-tls" for the DICOM Upper Layer
   Protocol on TLS.

The Conformance Statement shall indicate what mechanisms the
implementation supports for Key Management. When an integrity check
fails, the connection shall be dropped per the TLS protocol, causing
both the sender and the receiver to issue an A-P-ABORT indication to the
upper layers with an implementation-specific provider reason. The
provider reason used shall be documented in the Conformance Statement.

.. note::

   Implementers should take care to manage the risks of downgrading to
   less secure obsolescent protocols or cleartext protocols. See
   `biblioentry_title <#biblio_BCP_195>`__, Section 5.2 "Opportunistic
   Security".

.. _sect_B.10:

Non-Downgrading BCP 195 TLS Secure Transport Connection Profile
---------------------------------------------------------------

An implementation that supports the Non-Downgrading BCP 195 TLS Profile
shall utilize the framework and negotiation mechanism specified by the
Transport Layer Security protocol. It shall comply with
`biblioentry_title <#biblio_BCP_195>`__ from the IETF with the
additional restrictions enumerated below.

.. note::

   1. A device may support multiple different TLS profiles. DICOM does
      not specify how such devices are configured in the field or how
      different TLS profile-related rules are specified. The site will
      determine what configuration is appropriate.

   2. The DICOM profiles for TLS describe the capabilities of a product.
      Product configuration may permit selection of a particular profile
      and/or additional negotiation rules. The specific ciphersuite used
      is negotiated by the TLS implementation based on these rules.

The following additions are made to
`biblioentry_title <#biblio_BCP_195>`__ requirements. They change some
of the "should" recommendations in the RFC into requirements.

-  Implementations shall not negotiate TLS version 1.1
   `biblioentry_title <#biblio_RFC_4346>`__ or TLS version 1.0
   `biblioentry_title <#biblio_RFC_2246>`__

-  Implementations shall not negotiate DTLS version 1.0
   `biblioentry_title <#biblio_RFC_4347>`__

-  In cases where an application protocol allows implementations or
   deployments a choice between strict TLS configuration and dynamic
   upgrade from unencrypted to TLS-protected traffic (such as STARTTLS),
   clients and servers shall prefer strict TLS configuration.

-  Application protocols typically provide a way for the server to offer
   TLS during an initial protocol exchange, and sometimes also provide a
   way for the server to advertise support for TLS (e.g., through a flag
   indicating that TLS is required); unfortunately, these indications
   are sent before the communication channel is encrypted. A client
   shall attempt to negotiate TLS even if these indications are not
   communicated by the server.

-  The following cipher suites shall all be supported:

   -  TLS_DHE_RSA_WITH_AES_128_GCM_SHA256

   -  TLS_ECDHE_RSA_WITH_AES_128_GCM_SHA256

   -  TLS_DHE_RSA_WITH_AES_256_GCM_SHA384

   -  TLS_ECDHE_RSA_WITH_AES_256_GCM_SHA384

-  Additional cipher suites of similar or greater cryptographic strength
   may be supported.

TCP ports on which an implementation accepts TLS connections, or the
mechanism by which these port numbers are selected or configured, shall
be stated in the Conformance Statement. The TCP ports on which an
implementation accepts TLS connections for DICOMweb shall be different
from those on which an implementation accepts TLS connections for DIMSE.
The HTTP/HTTPS connection for DICOMweb can be shared with other
HTTP/HTTPS traffic.

The Conformance Statement shall also indicate what mechanisms the
implementation supports for Key Management.

.. note::

   It is recommended that systems supporting the Non-Downgrading BCP 195
   TLS Profile use the registered port number "2762 dicom-tls" for the
   DICOM Upper Layer Protocol on TLS. If both the Non-Downgrading BCP
   195 TLS Profile and the BCP 195 TLS Profile are supported, it is
   recommended that they use the well known port numbers on different IP
   addresses.

The Conformance Statement shall indicate what mechanisms the
implementation supports for Key Management.

When an integrity check fails, the connection shall be dropped per the
TLS protocol, causing both the sender and the receiver to issue an
A-P-ABORT indication to the upper layers with an implementation-specific
provider reason. The provider reason used shall be documented in the
Conformance Statement.

.. _sect_B.11:

Extended BCP 195 TLS Profile Secure Transport Connection Profile
----------------------------------------------------------------

An implementation that supports the Extended BCP 195 Profile shall
utilize the framework and negotiation mechanism specified by the
Transport Layer Security protocol. It shall comply with
`biblioentry_title <#biblio_BCP_195>`__ from the IETF with the
additional restrictions enumerated below.

.. note::

   1. A device may support multiple different TLS profiles. DICOM does
      not specify how such devices are configured in the field or how
      different TLS profile-related rules are specified. The site will
      determine what configuration is appropriate.

   2. The DICOM profiles for TLS describe the capabilities of a product.
      Product configuration may permit selection of a particular profile
      and/or additional negotiation rules. The specific ciphersuite used
      is negotiated by the TLS implementation based on these rules.

The following additions are made to
`biblioentry_title <#biblio_BCP_195>`__ requirements. They change some
of the "should" recommendations in the RFC into requirements.

-  Implementations shall not negotiate TLS version 1.1
   `biblioentry_title <#biblio_RFC_4346>`__ or TLS version 1.0
   `biblioentry_title <#biblio_RFC_2246>`__

-  Implementations shall not negotiate DTLS version 1.0
   `biblioentry_title <#biblio_RFC_4347>`__

-  In cases where an application protocol allows implementations or
   deployments a choice between strict TLS configuration and dynamic
   upgrade from unencrypted to TLS-protected traffic (such as STARTTLS),
   clients and servers shall prefer strict TLS configuration.

-  Application protocols typically provide a way for the server to offer
   TLS during an initial protocol exchange, and sometimes also provide a
   way for the server to advertise support for TLS (e.g., through a flag
   indicating that TLS is required); unfortunately, these indications
   are sent before the communication channel is encrypted. A client
   shall attempt to negotiate TLS even if these indications are not
   communicated by the server.

-  The following cipher suites shall all be supported:

   -  TLS_DHE_RSA_WITH_AES_128_GCM_SHA256

   -  TLS_ECDHE_RSA_WITH_AES_128_GCM_SHA256

   -  TLS_DHE_RSA_WITH_AES_256_GCM_SHA384

   -  TLS_ECDHE_RSA_WITH_AES_256_GCM_SHA384

-  One or more of the following cipher suites should be supported:

   -  TLS_DHE_RSA_WITH_CAMELLIA_256_GCM_SHA384 (0xC0, 0x7D)

   -  TLS_DHE_RSA_WITH_CAMELLIA_128_GCM_SHA256 (0xC0,0x7C)

   -  TLS_ECDHE_ECDSA_WITH_AES_256_GCM_SHA384 (0xC0,0x2C)

   -  TLS_ECDHE_ECDSA_WITH_CAMELLIA_256_GCM_SHA384 (0xC0,0x87)

   -  TLS_ECDHE_RSA_WITH_CAMELLIA_256_GCM_SHA384 (0xC0,0x8B)

   -  TLS_ECDHE_ECDSA_WITH_AES_128_GCM_SHA256 (0xC0,0x2B)

   -  TLS_ECDHE_ECDSA_WITH_CAMELLIA_128_GCM_SHA256 (0xC0,0x86)

   -  TLS_ECDHE_RSA_WITH_CAMELLIA_128_GCM_SHA256 (0xC0,0x8A)

-  No other cipher suites shall be used.

-  When DHE is used by key exchange, the key length shall be 2048 bits
   or more.

-  When ECDHE is used by key exchange, the key length shall be 256 bits
   or more.

TCP ports on which an implementation accepts TLS connections, or the
mechanism by which these port numbers are selected or configured, shall
be stated in the Conformance Statement. The TCP ports on which an
implementation accepts TLS connections for DICOMweb shall be different
from those on which an implementation accepts TLS connections for DIMSE.
The HTTPS connection for DICOMweb can be shared with other HTTP/HTTPS
traffic.

.. note::

   It is recommended that systems supporting the Extended BCP 195 TLS
   Profile use the registered port number "2762 dicom-tls" for the DICOM
   Upper Layer Protocol on TLS.

The Conformance Statement shall indicate what mechanisms the
implementation supports for Key Management.

When an integrity check fails, the connection shall be dropped per the
TLS protocol, causing both the sender and the receiver to issue an
A-P-ABORT indication to the upper layers with an implementation-specific
provider reason. The provider reason used shall be documented in the
Conformance Statement.

