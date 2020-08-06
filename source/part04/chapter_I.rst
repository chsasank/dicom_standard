.. _chapter_I:

Media Storage Service Class (Normative)
=======================================

.. _sect_I.1:

Overview
--------

.. _sect_I.1.1:

Scope
~~~~~

The Media Storage Service Class defines an application-level
class-of-service that facilitates the simple transfer of images and
associated information between DICOM AEs by means of Storage Media. It
supports:

a. The Interchange of images and a wide range of associated information.

.. _sect_I.1.2:

Service Definition
~~~~~~~~~~~~~~~~~~

DICOM AEs support a SOP Class of the Media Storage Service Class by
performing one or more roles among the three roles FSC, FSR or FSU. SOP
Classes of the Media Storage Service Class use the Media Storage
Services (M-WRITE, M-READ, M-DELETE, M-INQUIRE FILE-SET and M-INQUIRE
FILE). These Services are defined in .

.. _sect_I.2:

Behavior
--------

This Section discusses the FSC, FSR and FSU behavior for SOP Classes of
the Media Storage Service Class.

.. _sect_I.2.1:

Behavior of an FSC
~~~~~~~~~~~~~~~~~~

The FSC shall be able to create a DICOMDIR File containing the Media
Storage Directory SOP Class for the created File-set and create zero or
more Files belonging to the File-set by invoking M-WRITE Operations with
SOP Instances that meet the requirements of the corresponding IOD. It is
the responsibility of the FSC to ensure that the M-WRITE results in the
creation of a correctly formatted DICOM File. The manner in which this
is achieved is beyond the scope of the DICOM Standard.

The FSC shall support the Media Storage Operation M-INQUIRE FILE-SET and
may optionally support the M-INQUIRE FILE.

.. _sect_I.2.2:

Behavior of an FSR
~~~~~~~~~~~~~~~~~~

The FSR shall be able to recognize a File-set and the corresponding
DICOMDIR containing the Media Storage Directory SOP Class. A valid
File-set may contain only a DICOMDIR and no other files. If a File-set
contains other files with stored SOP Instance, the FSR shall be capable
of invoking M-READ Operations to access the content of the Files of the
File-set. The manner in which this is achieved is beyond the scope of
the DICOM Standard.

The FSR shall support the Media Storage Operation M-INQUIRE FILE and may
optionally support the M-INQUIRE FILE-SET.

.. _sect_I.2.3:

Behavior of an FSU
~~~~~~~~~~~~~~~~~~

The FSU shall be able to recognize a File-set and the corresponding
DICOMDIR containing the Media Storage Directory SOP Class. A valid
File-set may contain only a DICOMDIR and no other files. If a File-set
contains other files with stored SOP Instances, the FSU shall be capable
of invoking M-READ Operations to access the content of the Files of the
File-set. The manner in which this is achieved is beyond the scope of
the DICOM Standard.

The FSU shall support the Media Storage Operation M-INQUIRE FILE and the
M-INQUIRE FILE-SET.

The FSU shall be able to create one or more new Files belonging to the
File-set by invoking M-WRITE Operations with SOP Instances that meet the
requirements of the corresponding IOD. It is the responsibility of the
FSU to ensure that the M-WRITE results in the creation of a correctly
formatted DICOM File. The manner in which this is achieved is beyond the
scope of the DICOM Standard. The FSU shall be able to update the
contents of the DICOMDIR File by using M-DELETE and or M-WRITE
Operations.

.. _sect_I.3:

Conformance
-----------

.. _sect_I.3.1:

Conformance as an FSC
~~~~~~~~~~~~~~~~~~~~~

An implementation that conforms to one of the SOP Classes of the Media
Storage Service Class:

a. shall meet the requirements specified in `Behavior of an
   FSC <#sect_I.2.1>`__;

b. shall meet the requirements specified in ;

c. shall perform M-WRITE Operations according to the SOP Class
   specification identified by the SOP Class UID in the Meta File
   Information;

d. shall support the Media Storage Directory SOP Class (stored in the
   DICOMDIR File).

.. _sect_I.3.2:

Conformance as an FSR
~~~~~~~~~~~~~~~~~~~~~

An implementation that conforms to one of the SOP Classes of the Media
Storage Service Class:

a. shall meet the requirements specified in `Behavior of an
   FSR <#sect_I.2.2>`__;

b. shall meet the requirements specified in ;

c. shall perform M-READ Operations according to the SOP Class
   specification identified by the SOP Class UID in the Meta File
   Information. M-READ of non-supported SOP Classes shall simply result
   in ignoring such stored Data Sets;

d. shall read DICOMDIR Files without a Directory Information Module or
   with a Directory Information Module including Directory Records of a
   Type not supported by the implementation.

.. _sect_I.3.3:

Conformance as an FSU
~~~~~~~~~~~~~~~~~~~~~

An implementation that conforms to one of the SOP Classes of the Media
Storage Service Class:

a. shall meet the requirements specified in `Behavior of an
   FSU <#sect_I.2.3>`__;

b. shall meet the requirements specified in ;

c. shall perform M-READ Operations according to the SOP Class
   specification identified by the SOP Class UID in the Meta File
   Information. M-READ of unsupported SOP Classes shall simply result in
   ignoring such stored Data Sets;

d. shall perform M-WRITE Operations according to the SOP Class
   specification identified by the SOP Class UID in the Meta File
   Information;

e. shall support the Media Storage Directory SOP Class (stored in the
   DICOMDIR File). Directories containing a Directory Information Module
   shall be updated by an FSU. Directories containing no Directory
   Information Module shall not be updated by an FSU;

f. shall read DICOMDIR Files without a Directory Information Module or
   with a Directory Information Module including Directory Records of a
   Type not supported by the implementation.

.. _sect_I.3.4:

Conformance Statement Requirements
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

An implementation of the Media Storage Service Class may support one or
more Roles as specified in `table_title <#table_I.3-1>`__. In addition,
the implementation may conform to one or more of the SOP Classes of the
Media Storage Service Class defined in `Media Storage SOP
Classes <#sect_I.4>`__. The Conformance Statement shall be in the format
defined by .

.. table:: Allowed Combinations of Roles

   +-----------------------+---------+---------+-----------------------+
   | Roles                 | FSR     | FSC     | FSU                   |
   +=======================+=========+=========+=======================+
   | With a Directory      | Allowed | Allowed | Allowed Directory     |
   | Information Module    |         |         | shall be updated      |
   +-----------------------+---------+---------+-----------------------+
   | With no Directory     | Allowed | Allowed | Allowed Directory     |
   | Information Module    |         |         | shall not be updated  |
   +-----------------------+---------+---------+-----------------------+

The following aspects shall be documented in the Conformance Statement
of any implementation claiming conformance to one of the Media Storage
SOP Classes:

-  the subset of the Basic Directory Information Object Model supported;

-  When the Directory Information Module is created or updated
   (Directory Information Module supported), the optional standard keys
   that may be included in Directory Records shall be documented.
   Private Keys and Private Records may also be documented;

.. _sect_I.3.5:

Standard Extended, Specialized, and Private Conformance
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

In addition to Standard Media Storage SOP Classes, implementations may
support Standard Extended, Specialized and/or Private SOP Classes as
defined by .

For all three types of SOP Classes, implementations shall be permitted
to conform as an FSC, FSR, both or as an FSU. The Conformance Statement
shall be in the format defined in .

.. _sect_I.4:

Media Storage SOP Classes
-------------------------

The SOP Classes in the Media Storage Service Class identify the
Composite IODs to be stored. The IODs of the following SOP Classes can
be stored:

-  all IODs of the SOP Classes specified for the DIMSE C-STORE based
   Storage Service Class identified in `table_title <#table_B.5-1>`__

-  all IODs of the SOP Classes specified for the DIMSE C-STORE based
   Non-Patient Object Storage Service Class identified in
   `table_title <#table_GG.3-1>`__

-  the IOD of the media directory SOP Class identified in
   `table_title <#table_I.4-1>`__

.. table:: Media Storage Standard SOP Classes

   +----------------------+----------------------+----------------------+
   | SOP Class Name       | SOP Class UID        | **IOD Specification  |
   |                      |                      | (defined in )**      |
   +======================+======================+======================+
   | Media Storage        | 1.2.840.10008.1.3.10 |                      |
   | Directory Storage    |                      |                      |
   +----------------------+----------------------+----------------------+

.. note::

   1. Except for the Media Storage Directory SOP Class, all the SOP
      Classes in the Media Storage Service Class are assigned the same
      UID Value as the corresponding network communication SOP Classes.
      This was done to simplify UID assignment. Although these SOP
      Classes are based on different Services, the context of their
      usage should unambiguously distinguish a SOP Class used for Media
      Storage from a network communication SOP Class.

   2. The storage of Normalized Print SOP Instances on media was
      previously defined in DICOM. They have been retired. See PS
      3.4-1998.

   3. The storage of Detached and Standalone SOP Instances on media was
      previously defined in DICOM. They have been retired. See PS
      3.4-2004

.. _sect_I.4.1:

Specialization for Standard SOP Classes (Retired)
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

See `Specialization for Standard SOP Classes <#sect_B.5.1>`__.

.. _sect_I.5:

Retired Standard SOP Classes
----------------------------

See `Retired Standard SOP Classes <#sect_B.6>`__.

