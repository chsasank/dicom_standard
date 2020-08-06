.. _chapter_C:

DICOM Addressing (Normative)
============================

.. _sect_C.1:

DICOM Application Entity Titles
-------------------------------

A DICOM Application Entity Title uniquely identifies a service or
application on a specific system in the network. Application Entity
Titles are independent of network topology so a device may be physically
moved while its corresponding Application Entity Title may remain the
same. See for the encoding of DICOM Application Entity Titles.

.. note::

   DICOM Application Entity Title was called Logical Address in the
   ACR-NEMA Standard.

DICOM Application Entity Titles are used in three instances of
communication:

a. to identify the Called/Calling Application Entities. They are used to
   establish an association and to ensure that the association is
   established with the expected application.

b. to identify the originator and intended destination of DICOM Retrieve
   Services (see ). They are conveyed in DICOM Commands with messages of
   the DIMSE C-MOVE and C-STORE Services exchanged over an established
   association.

c. to identify the location of a Retrieve Service SCP for one or more
   SOP Instances. They are conveyed in DICOM DataSets of various
   services.

.. _sect_C.2:

Naming and Addressing Usage Rules
---------------------------------

DICOM Application Entity Titles are used in the Called/Calling
Application Entity Title fields of the Upper Layer Service, in the Move
Destination and Move Originator Application Entity Title data elements
in the DICOM Message Command Set, and in various Attributes of the DICOM
Message Data Set.

.. note::

   1. A single Application Entity Title can be associated with multiple
      network addresses assigned to a single system (e.g., multi-homed
      host).

   2. A single Application Entity Title can be associated with multiple
      TCP Ports using the same or different IP Addresses.

   3. A single network access point (IP Address and TCP Port) can
      support multiple Application Entity Titles.

A DICOM system on a network may support several application processes
identified by different DICOM Application Entity Titles.

Upon receiving an association request, the Called Application Entity
Title shall be validated so an association can be rejected when the
corresponding local application does not exist.

