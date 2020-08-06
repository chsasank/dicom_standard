.. _chapter_8:

Security Considerations
=======================

The metadata and ancillary streams usually contain Personally
Identifiable Information (PII). The video and audio streams might
contain protected information. The underlying SMPTE protocols do not
specify any security protections to ensure confidentiality, integrity,
or availability of the various data streams. DICOM does not specify any
additions to the SMPTE protocols to provide such protection.
Authorization and authentication of access to the DICOM-RTV Service is
handled by configuration. Authentication is not re-confirmed at
initiation of the underlying SMPTE protocols, and DICOM does not specify
any additions to the SMPTE protocols for access control, authorization,
or authentication.

The potential eavesdropping, replay, message insertion, deletion,
modification, man-in-the-middle and denial of service attacks have not
been analyzed. That analysis is up to the individual sites and
installations.

Individual sites and installations will also need to perform their own
assessments and selection of security mechanisms and add protections as
necessary. The data rates and strict timing requirements for the data
streams require careful analysis of any security mechanisms that are
added. There do exist security mechanisms that operate at and below the
IP level that can meet foreseen use cases, but there is insufficient
experience or evidence to justify DICOM making a recommendation.

