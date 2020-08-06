.. _chapter_WW:

Audit Messages (Informative)
============================

This annex holds examples of audit messaging, as described by the Audit
Trail Message Format Secure Use Profile in .

.. _sect_WW.1:

Message Example
---------------

An example of one of the DICOM Instances Transferred messages is shown
in `example_title <#example_WW.1-1>`__.

::

   <?xml version="1.0" encoding="UTF-8"?>
   <AuditMessage
       xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" 
         xsi:noNamespaceSchemaLocation="D:\data\DICOM\security\audit-message.rnc">
     <EventIdentification
         EventActionCode="C"
         EventDateTime="2001-12-17T09:30:47"
         EventOutcomeIndicator="0">
       <EventID code="110104"
         codeSystemName="DCM"
         displayName="DICOM Instances Transferred"/>
     </EventIdentification>
     
     <ActiveParticipant
         UserID="123"
         AlternativeUserID="AETITLE=AEFOO"
         UserIsRequestor="false" 
             NetworkAccessPointID="192.168.1.2"
             NetworkAccessPointTypeCode="2">
       <RoleIDCode
           code="110153"
           codeSystemName="DCM"
           displayName="Source Role ID"/>
     </ActiveParticipant>
     
     <ActiveParticipant
         UserID="67562"
         AlternativeUserID="AETITLE=AEPACS"
         UserIsRequestor="false" 
             NetworkAccessPointID="192.168.1.5"
             NetworkAccessPointTypeCode="2">
       <RoleIDCode
           code="110152"
           codeSystemName="DCM"
           displayName="Destination Role ID"/>
     </ActiveParticipant>
     
     <ActiveParticipant
         UserID="smitty@readingroom.hospital.org"
             AlternativeUserID="smith@nema"
             UserName="Dr. Smith" 
             UserIsRequestor="true"
             NetworkAccessPointID="192.168.1.2"
             NetworkAccessPointTypeCode="2">
       <RoleIDCode
           code="110153"
           codeSystemName="DCM"
           displayName="Source Role ID"/>
     </ActiveParticipant>
     
     <AuditSourceIdentification
         AuditEnterpriseSiteID="Hospital"
         AuditSourceID="ReadingRoom">
       <AuditSourceTypeCode code="1"/>
     </AuditSourceIdentification>
     
     <ParticipantObjectIdentification
         ParticipantObjectID="1.2.840.10008.2.3.4.5.6.7.78.8" 
               ParticipantObjectTypeCode="2"
               ParticipantObjectTypeCodeRole="3" 
               ParticipantObjectDataLifeCycle="1">
       <ParticipantObjectIDTypeCode
           code="110180"
           codeSystemName="DCM"
           displayName="Study Instance UID"/>
       <ParticipantObjectDescription>
         <MPPS UID="1.2.840.10008.1.2.3.4.5"/>
         <Accession Number="12341234" />
         <SOPClass UID="1.2.840.10008.5.1.4.1.1.2" NumberOfInstances="1500"/>
         <SOPClass UID="1.2.840.10008.5.1.4.1.1.11.1" NumberOfInstances="3"/>
       </ParticipantObjectDescription>
     </ParticipantObjectIdentification>
     
     <ParticipantObjectIdentification
         ParticipantObjectID="ptid12345"
         ParticipantObjectTypeCode="1"
             ParticipantObjectTypeCodeRole="1">
       <ParticipantObjectIDTypeCode code="2"/>
       <ParticipantObjectName>John Doe</ParticipantObjectName>
     </ParticipantObjectIdentification>
   </AuditMessage>

The message describes a study transfer initiated at the request of Dr.
Smith on the system at the IP address 192.168.1.2 to a system at IP
address 192.168.1.5. The study contains 1500 CT SOP Instances and 3 GSPS
SOP Instances. The audit report came from the audit source
"ReadingRoom".

.. _sect_WW.2:

Workflow Example
----------------

The following is an example of audit trail message use in a hypothetical
workflow. It is not intended to be all-inclusive, nor does it cover all
possible scenarios for audit trail message use. There are many
alternatives that can be utilized by the system designer, or that could
be configured by the local site security administrator to fit security
policies.

As this example scenario begins, an imaging workstation boots up. During
its start up process, a DICOM-enabled viewing application is launched by
the start up sequence. This triggers an Application Activity message
with the Event Type Code of (110120, DCM, "Application Start").

After start up, a curious, but unauthorized visitor attempts to utilize
the reviewing application. Since the reviewing application cannot verify
the identity of this visitor, the attempt fails, and the reviewing
application generates a User Authentication message, recording the fact
that this visitor attempted to enter the application, but failed.

Later, an authorized user accesses the reviewing application. Upon
successfully identifying the user, the reviewing application generates a
User Authentication message indicating a successful login to the
application.

The user, in order to locate the data of a particular examination,
issues a query, which the reviewing application directs to a DICOM
archive. The details of this query are recorded by the archive
application in a Query message.

The reviewing application, in delivering the results of the query to the
user, displays certain patient related information. The reviewing
application records this fact by sending a Patient Record message that
is defined by some other standard. Audit logs will contain messages
specified by a variety of different standards. The MSG-ID field is used
to aid the recognition of the defining standard or proprietary source
documentation for a particular message.

From the query results, the user selects a set of images to review. The
reviewing application requests the images from the archive, and records
this fact in a Begin Transferring Instances message.

The archive application locates the images, sends them back to the
reviewing application, and records this fact in an Instances Transferred
message.

The reviewing application displays the images to the user, recording
this fact via an Instances Accessed message.

During the reviewing process, the use looks up details of the procedure
from the hospital information system. The reviewing application performs
this lookup using HL7 messaging, and records this fact in a Procedure
Record message.

The user decides that a follow-up examination is needed, and generates a
new order via HL7 messaging to the hospital information system. The
reviewing application records this in an Order Record message.

The user decides that a second opinion is desirable, and selects certain
images to send to a colleague in an e-mail message. The reviewing
application records the fact that it packaged and sent images via e-mail
in an Export message.

