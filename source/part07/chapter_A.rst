.. _chapter_A:

Application Context Usage (Normative)
=====================================

.. _sect_A.1:

Application Context Definition
------------------------------

An Application Context explicitly defines the set of application service
elements, related options and any other information necessary for the
inter working of Application Entities on an Association; in particular,
it specifies the DIMSE Protocol used by the Application Layer.

Two Application Entities establish an Association by agreeing on an
Application Context. The requester of an Association proposes an
Application Context Name and the acceptor returns either the same or a
different Application Context Name. The returned name specifies the
Application Context to be used for this Association. The offer of an
alternate Application Context by the acceptor provides a mechanism for
limited negotiation. If the requester cannot operate in the acceptor's
Application Context, it shall issue an A-Abort request primitive. Such a
negotiation will facilitate the introduction of new versions of the
DICOM Message Exchange Protocol in the future.

.. _sect_A.2:

DICOM Application Context Name Encoding and Registration
--------------------------------------------------------

The Application Context Name structure is based on the OSI Object
Identification (numeric form) as defined by ISO 8824. Specific rules are
defined in . Application Context Names are registered values as defined
by ISO 9834-1 to ensure global uniqueness. Application Context Names
shall be encoded as defined in .

.. _sect_A.2.1:

DICOM Registered Application Context Names
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

The organization responsible for the definition and registration of
DICOM Application Context Names is ACR-NEMA. ACR-NEMA guarantees
uniqueness for all DICOM Application Context Names. A choice of DICOM
registered Application Context Names related to a specific version of
DIMSE, as well as the associated negotiation rules, are defined in this
annex.

A single DICOM Application Context Name is defined for this version of
this Standard. This name is "1.2.840.10008.3.1.1.1"

.. _sect_A.2.2:

Privately Defined Application Context Names
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

Privately defined Application Context Names may also be used, but they
will not be registered by ACR-NEMA. Organizations that define private
Application Context Names are responsible to obtain their proper
registration as defined for OSI Object Identifiers. National Standards
Organizations representing a number of countries (e.g., UK, France,
Germany, Japan, USA, etc.) to the International Standards Organization
act as a registration authority as defined by ISO 9834-1.

.. note::

   For example, in the USA, ANSI assigns Organization Identifiers to any
   requesting organization. This identifier is made of a series of four
   numeric elements; 1 (identifies ISO), 2 (identifies the ISO member
   bodies branch), 840 (identifies ANSI as the ISO member body
   representing the USA), and xxxxxx (identifies a specific organization
   and is issued by ANSI). Such an identifier may be used by the
   identified organization as a root to which it may add a suffix made
   of one or more numeric elements. The identified organization accepts
   the responsibility to properly register these suffixes to ensure
   uniqueness.

Privately defined Application Context Names shall be encoded as defined
in . The Organization identifier "1.2.840.10008" is reserved for DICOM
and shall not be used for privately defined Application Context Names.

.. _sect_A.3:

Association Initialization for DICOM Application Entity
-------------------------------------------------------

The establishment of an Association involves two DICOM AEs, one that is
the Association-requester and one that is the Association-acceptor.

A DICOM AE shall initiate an Association establishment by using the
A-ASSOCIATE request service defined in . It shall provide the
Application Association Information as defined by `Association
Negotiation (Normative) <#chapter_D>`__.

.. _sect_A.4:

Operation/Notification for DICOM Application Entity
---------------------------------------------------

Operations and notifications are only used on an Association. They
result in Messages exchanged by using the P-DATA request service defined
in .

All operations and notifications invoked over an Association shall be
confirmed. The performing DICOM AE shall report the response of each
operation or notification over the same Association by means of which
the operation or notification was invoked. No recovery shall be
performed using multiple Associations.

Operations and notifications, on an Association, shall use one of the
following two modes:

-  synchronous, where the invoking DICOM AE, on a established
   Association, requires a response from the performing DICOM AE before
   invoking another operation or notification

-  asynchronous, where the invoking DICOM AE, on a established
   Association, may continue to invoke further operations or
   notifications to the performing DICOM AE without awaiting a response

.. note::

   The synchronous/asynchronous mode is defined within the scope of one
   Application Entity and not within the scope of the association
   between two Application Entities. The communication mode on the
   association may be bi-directional if agreed upon during association
   negotiation (i.e., both operation and notifications are
   simultaneously supported, etc.). Following is an example of
   synchronous mode, DICOM AE A may send an operation request to DICOM
   AE B and DICOM AE B may send a notification request to DICOM AE A
   before responding to the operation request from AE A. This is
   considered as synchronous mode because each AE has only one
   outstanding operation or notification.

The mode selected (synchronous or asynchronous) is determined at
Association establishment time. The synchronous mode serves as the
default mode and shall be supported by all DICOM AEs. The asynchronous
mode is optional and the maximum number of outstanding operations or
notifications is negotiated during Association establishment. This
negotiation is accomplished by the Asynchronous Operations Window
sub-item structure as defined in `Association Negotiation
(Normative) <#chapter_D>`__.

.. _sect_A.5:

Association Release for DICOM AE
--------------------------------

Only the DICOM AE Association-requester may initiate an orderly release
of the Association. This shall be accomplished by using the A-RELEASE
service defined in .

The DICOM AE Association-requester shall not release the Association
until all operations invoked have been confirmed.

.. _sect_A.6:

Association Abort for DICOM AE
------------------------------

Either DICOM AE may initiate an abrupt termination of an Association.
This shall be accomplished by using the A-ABORT service defined in .

Upon receiving or issuing the A-ABORT service primitive, the DICOM AE
Association-requester and DICOM AE Association-acceptor shall fail any
operation that is outstanding.

.. note::

   The Association services and presentation services defined in the
   Upper Layer Service in are a fully conformant subset of the services
   offered by the ACSE and the OSI Presentation Layer.

