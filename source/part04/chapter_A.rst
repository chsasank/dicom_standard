.. _chapter_A:

Verification Service Class (Normative)
======================================

.. _sect_A.1:

Overview
--------

.. _sect_A.1.1:

Scope
~~~~~

The Verification Service Class defines a service that verifies
application level communication between peer DICOM AEs. This
verification is accomplished on an established Association using the
C-ECHO DIMSE-C service.

.. _sect_A.2:

SCU/SCP Behavior
----------------

A DICOM AE, supporting the Verification SOP Class SCU role, requests
verification of communication to a remote DICOM AE. This request is
performed using the C-ECHO request primitive. The remote DICOM AE,
supporting the Verification SOP Class SCP role, issues an C-ECHO
response primitive. Upon receipt of the C-ECHO confirmation, the SCU
determines that verification is complete. See for the specification of
the C-ECHO primitives.

.. _sect_A.3:

DIMSE-C Service Group
---------------------

The C-ECHO DIMSE-C service shall be the mechanism used to verify
communications between peer DICOM AEs. The C-ECHO service and protocol
parameters shall be required as defined in .

.. _sect_A.4:

Verification SOP Class
----------------------

The Verification SOP Class consists of the C-ECHO DIMSE-C service. No
associated Information Object Definition is defined. The SOP Class UID
shall be "1.2.840.10008.1.1".

No Specialized SOP Classes and/or Meta SOP Classes shall be defined for
the Verification SOP Class.

.. _sect_A.5:

Association Negotiation
-----------------------

Association establishment is the first phase of any instance of
communication between peer DICOM AEs. The following negotiation rules
apply to DICOM AEs that support the Verification SOP Class

-  The Association-requester (verification SCU role) in the A-ASSOCIATE
   request shall convey an Abstract Syntax, in a Presentation Context,
   for the Verification SOP Class. The Abstract Syntax Name shall be
   equivalent to the Verification SOP Class UID.

-  The Association-acceptor (verification SCP role) in the A-ASSOCIATE
   response shall accept the Abstract Syntax, in a Presentation Context,
   for the supported Verification SOP Class.

No Application Association Information specific to the Verification SOP
Class shall be used.

.. _sect_A.6:

Conformance
-----------

.. _sect_A.6.1:

Conformance Supporting the SCU Role
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

Implementations that conform to the Verification SOP Class SCU role
shall meet the:

-  C-ECHO service requirements as defined by the DIMSE Service Group,
   `DIMSE-C Service Group <#sect_A.3>`__

-  Association negotiation rules as defined in `Association
   Negotiation <#sect_A.5>`__

.. _sect_A.6.2:

Conformance Supporting the SCP Role
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

Implementations that conform to the Verification SOP Class SCP role
shall meet the:

-  C-ECHO operation rules as defined by the DIMSE Service Group,
   `DIMSE-C Service Group <#sect_A.3>`__

-  Association negotiation rules as defined in `Association
   Negotiation <#sect_A.5>`__

.. _sect_A.6.3:

Conformance Statement
~~~~~~~~~~~~~~~~~~~~~

An implementation may conform to the Verification SOP Class as an SCU,
SCP, or both. The Conformance Statement shall be in the format defined
in .

