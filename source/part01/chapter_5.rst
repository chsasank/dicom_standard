.. _chapter_5:

The DICOM Communication Model
=============================

The DICOM Standard facilitates interoperability of devices claiming
conformance. In particular, it:

-  Addresses the semantics of Commands and associated data. For devices
   to interact, there must be standards on how devices are expected to
   react to Commands and associated data, not just the information that
   is to be moved between devices.

-  Addresses the semantics of file services, file formats and
   information directories necessary for off-line communication.

-  Is explicit in defining the conformance requirements of
   implementations of the Standard. In particular, a conformance
   statement must specify enough information to determine the functions
   for which interoperability can be expected with another device
   claiming conformance.

-  Facilitates operation in a networked environment.

-  Is structured to accommodate the introduction of new services, thus
   facilitating support for future medical imaging applications.

-  Makes use of existing international standards wherever applicable,
   and itself conforms to established documentation guidelines for
   international standards.

`figure_title <#figure_5-1>`__ presents the general communication model
of the Standard, which spans both network (on-line) and media storage
interchange (off-line) communication. Applications may utilize any of
the following transport mechanisms:

-  the DICOM Message Service and Upper Layer Service, which provides
   independence from specific physical networking communication support
   and protocols such as TCP/IP.

-  the DICOM Web Service API and HTTP Service, which allows use of
   common hypertext and associated protocols for transport of DICOM
   services

-  the Basic DICOM File Service, which provides access to Storage Media
   independently from specific media storage formats and file structures

-  the DICOM-RTV and RTP Service, which allows use of real-time
   transmission for transport of DICOM services.

