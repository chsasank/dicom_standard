.. _chapter_8:

Protocol Overview
=================

.. _sect_8.1:

DIMSE Protocol
--------------

This Section provides an overview of the DIMSE protocol machine. The
DIMSE protocol machine defines the procedures and the encoding rules
necessary to construct Messages used to exchange command requests and
responses between peer DIMSE Service Users (e.g., two DICOM Application
Entities). The relationship between Messages and the different types of
service primitives is shown in `figure_title <#figure_7-1>`__.

The DIMSE protocol machine accepts DIMSE Service User request and
response service primitives and constructs Messages defined by the
procedures defined in 9.3 and 10.3. The DIMSE protocol machine accepts
Messages and passes them to the DIMSE Service User by the means of
indication and confirmation service primitives.

Procedures define the rules for the transfer of Messages that convey
command requests and responses. These rules define interpretation of the
various fields in the command part of the Message. They do not define
what an invoking DIMSE Service User should do with the information (the
Data Set part of the Message) it requested nor how a performing DIMSE
Service User should process the operation.

Messages may be fragmented. The fragmentation of Messages exchanged
between peer DICOM Application Entities and the P-DATA service used to
exchange these Message fragments are defined in `Usage of the P-DATA
Service By the DICOM Application Entity (Normative) <#chapter_F>`__.

.. note::

   These Message fragments are called Application Protocol Data Units
   (APDUs) by the OSI construct.

The invoking DIMSE Service User request primitive results in a Message
carrying a Command Request (with an optional associated Data Set). Each
Message induces an indication primitive to the performing DIMSE Service
User.

The performing DIMSE Service User response primitives result in a
Message carrying a Command Response (with an optional associated Data
Set). Each Message induces a confirmation primitive to the invoking
DIMSE Service User.

.. _sect_8.2:

Association Protocol
--------------------

The establishment of an Association involves two DIMSE Service Users,
one that is the Association-requester and one that is the
Association-acceptor. A DIMSE Service User may initiate an Association
establishment by using the A-ASSOCIATE service described in .

Included in the parameters of the A-ASSOCIATE service is the Application
Context that specifies, among other things, the rules required for the
coordination of initialization information corresponding to different
DICOM Application Entities. The Application Contexts permitted for DIMSE
are specified in `Application Context Usage (Normative) <#chapter_A>`__.

.. _sect_8.3:

Conformance
-----------

Implementers conform to the DIMSE protocol only by conformance to a SOP
class as defined in and . Implementers do not conform directly to the
DIMSE protocol, and are not required to include a statement about DIMSE
conformance in conformance statements except as required in .

