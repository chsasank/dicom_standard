.. _chapter_C:

Status Type Encoding (Normative)
================================

The following sections define the encoding for the Status Types
supported by the DIMSE services. The applicability and semantics for
each Status Type (i.e., Attribute list error, etc.) are defined in the
DIMSE Services. Each Status Type is categorized in a Status Class and
represents certain Status Meaning within the Status Class.

.. note::

   The Status (0000,0900) Command Element is required for all Status
   Types.

All Status Codes are assigned according to the following Status Class
convention:

======= ===================================================
Success 0000
Warning 0001 or Bxxx or 0107 or 0116
Failure Axxx or Cxxx or 01xx (except 0107 and 0116) or 02xx
Cancel  FE00
Pending FF00 and FF01
======= ===================================================

Status Codes with values 01xx and 02xx are reserved for assignment by
DICOM Standard. These Status codes have standard status meanings for
DIMSE Services that shall not be modified by a Service Class definition
or an implementation.

Status Codes with values Axxx, Bxxx, and Cxxx may be assigned by the
DICOM Standard or by an implementation according to the definition of a
Service Class in .

Implementations shall not use Status Codes with values not listed in the
table above.

.. _sect_C.1:

Success Status Class
--------------------

Statuses in this Status Class convey that the operation/notification
completed successfully.

.. _sect_C.1.1:

Success
~~~~~~~

+----------------+-------------+--------+--------+----------------+
| **Status       | **Tag**     | **VR** | **VM** | **Description  |
| Field**        |             |        |        | of Field**     |
+================+=============+========+========+================+
| Status         | (0000,0900) | US     | 1      | Confirmation   |
|                |             |        |        | status of the  |
|                |             |        |        | operation. The |
|                |             |        |        | value of this  |
|                |             |        |        | required field |
|                |             |        |        | shall be set   |
|                |             |        |        | to 0000H.      |
+----------------+-------------+--------+--------+----------------+

.. _sect_C.2:

Pending Status Class
--------------------

Statuses in this Status Class convey that the operation/notification is
continuing and additional Statuses are expected.

.. _sect_C.2.1:

Pending
~~~~~~~

+----------------+-------------+--------+--------+----------------+
| **Status       | **Tag**     | **VR** | **VM** | **Description  |
| Field**        |             |        |        | of Field**     |
+================+=============+========+========+================+
| Status         | (0000,0900) | US     | 1      | Confirmation   |
|                |             |        |        | status of the  |
|                |             |        |        | operation. The |
|                |             |        |        | value of this  |
|                |             |        |        | required field |
|                |             |        |        | is Service     |
|                |             |        |        | Class specific |
|                |             |        |        | and defined in |
|                |             |        |        | .              |
+----------------+-------------+--------+--------+----------------+

.. _sect_C.3:

Cancel Status Class
-------------------

Statuses in this Status Class convey that the operation/notification has
been canceled.

.. _sect_C.3.1:

Cancel
~~~~~~

+----------------+-------------+--------+--------+----------------+
| **Status       | **Tag**     | **VR** | **VM** | **Description  |
| Field**        |             |        |        | of Field**     |
+================+=============+========+========+================+
| Status         | (0000,0900) | US     | 1      | Confirmation   |
|                |             |        |        | status of the  |
|                |             |        |        | operation. The |
|                |             |        |        | value of this  |
|                |             |        |        | required field |
|                |             |        |        | shall be set   |
|                |             |        |        | to FE00H.      |
+----------------+-------------+--------+--------+----------------+

.. _sect_C.4:

Warning Status Class
--------------------

Statuses in this Status Class convey that the operation/notification has
completed but an error was detected. The semantics and behavior of these
Statuses are defined in .

.. _sect_C.4.1:

Warning
~~~~~~~

+----------------+-------------+--------+--------+----------------+
| **Status       | **Tag**     | **VR** | **VM** | **Description  |
| Field**        |             |        |        | of Field**     |
+================+=============+========+========+================+
| Status         | (0000,0900) | US     | 1      | Confirmation   |
|                |             |        |        | status of the  |
|                |             |        |        | operation. The |
|                |             |        |        | value of this  |
|                |             |        |        | required field |
|                |             |        |        | is Service     |
|                |             |        |        | Class specific |
|                |             |        |        | and defined in |
|                |             |        |        | .              |
+----------------+-------------+--------+--------+----------------+
| Offending      | (0000,0901) | AT     | 1-n    | This optional  |
| Element        |             |        |        | field contains |
|                |             |        |        | a list of the  |
|                |             |        |        | elements in    |
|                |             |        |        | which the      |
|                |             |        |        | error was      |
|                |             |        |        | detected.      |
+----------------+-------------+--------+--------+----------------+
| Error Comment  | (0000,0902) | LO     | 1      | This optional  |
|                |             |        |        | field contains |
|                |             |        |        | an             |
|                |             |        |        | applic         |
|                |             |        |        | ation-specific |
|                |             |        |        | text           |
|                |             |        |        | description of |
|                |             |        |        | the error      |
|                |             |        |        | detected.      |
+----------------+-------------+--------+--------+----------------+

.. _sect_C.4.2:

Attribute list error
~~~~~~~~~~~~~~~~~~~~

+----------------+-------------+--------+--------+----------------+
| **Status       | **Tag**     | **VR** | **VM** | **Description  |
| Field**        |             |        |        | of Field**     |
+================+=============+========+========+================+
| Affected SOP   | (0000,0002) | UI     | 1      | This optional  |
| Class UID      |             |        |        | field contains |
|                |             |        |        | the SOP Class  |
|                |             |        |        | UID for which  |
|                |             |        |        | Attributes     |
|                |             |        |        | were not       |
|                |             |        |        | recognized.    |
+----------------+-------------+--------+--------+----------------+
| Status         | (0000,0900) | US     | 1      | Confirmation   |
|                |             |        |        | status of the  |
|                |             |        |        | operation. The |
|                |             |        |        | value of this  |
|                |             |        |        | required field |
|                |             |        |        | shall be set   |
|                |             |        |        | to 0107H.      |
+----------------+-------------+--------+--------+----------------+
| Affected SOP   | (0000,1000) | UI     | 1      | This optional  |
| Instance UID   |             |        |        | field contains |
|                |             |        |        | the UID of the |
|                |             |        |        | SOP Instance   |
|                |             |        |        | for which      |
|                |             |        |        | Attributes     |
|                |             |        |        | were not       |
|                |             |        |        | recognized.    |
+----------------+-------------+--------+--------+----------------+
| Attribute      | (0000,1005) | AT     | 1-n    | This optional  |
| Identifier     |             |        |        | field contains |
| List           |             |        |        | an Attribute   |
|                |             |        |        | Tag for each   |
|                |             |        |        | Attribute that |
|                |             |        |        | was not        |
|                |             |        |        | recognized.    |
+----------------+-------------+--------+--------+----------------+

.. _sect_C.4.3:

Attribute Value out of range
~~~~~~~~~~~~~~~~~~~~~~~~~~~~

+----------------+-------------+--------+--------+----------------+
| **Status       | **Tag**     | **VR** | **VM** | **Description  |
| Field**        |             |        |        | of Field**     |
+================+=============+========+========+================+
| Status         | (0000,0900) | US     | 1      | Confirmation   |
|                |             |        |        | status of the  |
|                |             |        |        | operation. The |
|                |             |        |        | value of this  |
|                |             |        |        | required field |
|                |             |        |        | shall be set   |
|                |             |        |        | to 0116H.      |
+----------------+-------------+--------+--------+----------------+
| Modification   | (no tag)    | -      | -      | Optionally     |
| List/Attribute |             |        |        | contains the   |
| List           |             |        |        | application    |
|                |             |        |        | specific Data  |
|                |             |        |        | Set to only    |
|                |             |        |        | encode the     |
|                |             |        |        | invalid        |
|                |             |        |        | Attribute      |
|                |             |        |        | Values         |
|                |             |        |        | conveyed in    |
|                |             |        |        | the            |
|                |             |        |        | Modification   |
|                |             |        |        | List of the    |
|                |             |        |        | N-SET-RQ or    |
|                |             |        |        | the Attribute  |
|                |             |        |        | List of the    |
|                |             |        |        | N-CREATE-RQ.   |
+----------------+-------------+--------+--------+----------------+

.. _sect_C.5:

Failure Status Class
--------------------

Statuses in this Status Class convey that the operation/notification
failed and was not performed.

.. _sect_C.5.1:

Error: Cannot understand
~~~~~~~~~~~~~~~~~~~~~~~~

+----------------+-------------+--------+--------+----------------+
| **Status       | **Tag**     | **VR** | **VM** | **Description  |
| Field**        |             |        |        | of Field**     |
+================+=============+========+========+================+
| Status         | (0000,0900) | US     | 1      | Confirmation   |
|                |             |        |        | status of the  |
|                |             |        |        | operation. The |
|                |             |        |        | value of this  |
|                |             |        |        | required field |
|                |             |        |        | is Service     |
|                |             |        |        | Class specific |
|                |             |        |        | and defined in |
|                |             |        |        | .              |
+----------------+-------------+--------+--------+----------------+
| Offending      | (0000,0901) | AT     | 1-n    | This optional  |
| Element        |             |        |        | field contains |
|                |             |        |        | a list of the  |
|                |             |        |        | elements in    |
|                |             |        |        | which the      |
|                |             |        |        | error was      |
|                |             |        |        | detected.      |
+----------------+-------------+--------+--------+----------------+
| Error Comment  | (0000,0902) | LO     | 1      | This optional  |
|                |             |        |        | field contains |
|                |             |        |        | an             |
|                |             |        |        | applic         |
|                |             |        |        | ation-specific |
|                |             |        |        | text           |
|                |             |        |        | description of |
|                |             |        |        | the error      |
|                |             |        |        | detected.      |
+----------------+-------------+--------+--------+----------------+

.. _sect_C.5.2:

Error: Data Set does not match SOP Class
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

+----------------+-------------+--------+--------+----------------+
| **Status       | **Tag**     | **VR** | **VM** | **Description  |
| Field**        |             |        |        | of Field**     |
+================+=============+========+========+================+
| Status         | (0000,0900) | US     | 1      | Confirmation   |
|                |             |        |        | status of the  |
|                |             |        |        | operation. The |
|                |             |        |        | value of this  |
|                |             |        |        | required field |
|                |             |        |        | is Service     |
|                |             |        |        | Class specific |
|                |             |        |        | and defined in |
|                |             |        |        | .              |
+----------------+-------------+--------+--------+----------------+
| Offending      | (0000,0901) | AT     | 1-n    | This optional  |
| Element        |             |        |        | field contains |
|                |             |        |        | a list of the  |
|                |             |        |        | elements in    |
|                |             |        |        | which the      |
|                |             |        |        | error was      |
|                |             |        |        | detected.      |
+----------------+-------------+--------+--------+----------------+
| Error Comment  | (0000,0902) | LO     | 1      | This optional  |
|                |             |        |        | field contains |
|                |             |        |        | an             |
|                |             |        |        | applic         |
|                |             |        |        | ation-specific |
|                |             |        |        | text           |
|                |             |        |        | description of |
|                |             |        |        | the error      |
|                |             |        |        | detected.      |
+----------------+-------------+--------+--------+----------------+

.. _sect_C.5.3:

Failed
~~~~~~

+----------------+-------------+--------+--------+----------------+
| **Status       | **Tag**     | **VR** | **VM** | **Description  |
| Field**        |             |        |        | of Field**     |
+================+=============+========+========+================+
| Status         | (0000,0900) | US     | 1      | Confirmation   |
|                |             |        |        | status of the  |
|                |             |        |        | operation. The |
|                |             |        |        | value of this  |
|                |             |        |        | required field |
|                |             |        |        | is Service     |
|                |             |        |        | Class specific |
|                |             |        |        | and defined in |
|                |             |        |        | .              |
+----------------+-------------+--------+--------+----------------+
| Offending      | (0000,0901) | AT     | 1-n    | This optional  |
| Element        |             |        |        | field contains |
|                |             |        |        | a list of the  |
|                |             |        |        | elements in    |
|                |             |        |        | which the      |
|                |             |        |        | error was      |
|                |             |        |        | detected.      |
+----------------+-------------+--------+--------+----------------+
| Error Comment  | (0000,0902) | LO     | 1      | This optional  |
|                |             |        |        | field contains |
|                |             |        |        | an             |
|                |             |        |        | applic         |
|                |             |        |        | ation-specific |
|                |             |        |        | text           |
|                |             |        |        | description of |
|                |             |        |        | the error      |
|                |             |        |        | detected.      |
+----------------+-------------+--------+--------+----------------+

.. _sect_C.5.4:

Refused: Move Destination unknown
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

+----------------+-------------+--------+--------+----------------+
| **Status       | **Tag**     | **VR** | **VM** | **Description  |
| Field**        |             |        |        | of Field**     |
+================+=============+========+========+================+
| Status         | (0000,0900) | US     | 1      | Confirmation   |
|                |             |        |        | status of the  |
|                |             |        |        | operation. The |
|                |             |        |        | value of this  |
|                |             |        |        | required field |
|                |             |        |        | is Service     |
|                |             |        |        | Class specific |
|                |             |        |        | and defined in |
|                |             |        |        | .              |
+----------------+-------------+--------+--------+----------------+
| Error Comment  | (0000,0902) | LO     | 1      | This optional  |
|                |             |        |        | field contains |
|                |             |        |        | an             |
|                |             |        |        | applic         |
|                |             |        |        | ation-specific |
|                |             |        |        | text           |
|                |             |        |        | description of |
|                |             |        |        | the error      |
|                |             |        |        | detected.      |
+----------------+-------------+--------+--------+----------------+

.. _sect_C.5.5:

Refused: Out of resources
~~~~~~~~~~~~~~~~~~~~~~~~~

+----------------+-------------+--------+--------+----------------+
| **Status       | **Tag**     | **VR** | **VM** | **Description  |
| Field**        |             |        |        | of Field**     |
+================+=============+========+========+================+
| Status         | (0000,0900) | US     | 1      | Confirmation   |
|                |             |        |        | status of the  |
|                |             |        |        | operation. The |
|                |             |        |        | value of this  |
|                |             |        |        | required field |
|                |             |        |        | is Service     |
|                |             |        |        | Class specific |
|                |             |        |        | and defined in |
|                |             |        |        | .              |
+----------------+-------------+--------+--------+----------------+
| Error Comment  | (0000,0902) | LO     | 1      | This optional  |
|                |             |        |        | field contains |
|                |             |        |        | an             |
|                |             |        |        | applic         |
|                |             |        |        | ation-specific |
|                |             |        |        | text           |
|                |             |        |        | description of |
|                |             |        |        | the error      |
|                |             |        |        | detected.      |
+----------------+-------------+--------+--------+----------------+

.. _sect_C.5.6:

Refused: SOP Class not supported
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

+----------------+-------------+--------+--------+----------------+
| **Status       | **Tag**     | **VR** | **VM** | **Description  |
| Field**        |             |        |        | of Field**     |
+================+=============+========+========+================+
| Status         | (0000,0900) | US     | 1      | Confirmation   |
|                |             |        |        | status of the  |
|                |             |        |        | operation. The |
|                |             |        |        | value of this  |
|                |             |        |        | required field |
|                |             |        |        | shall be set   |
|                |             |        |        | to 0122H.      |
+----------------+-------------+--------+--------+----------------+
| Error Comment  | (0000,0902) | LO     | 1      | This optional  |
|                |             |        |        | field contains |
|                |             |        |        | an             |
|                |             |        |        | applic         |
|                |             |        |        | ation-specific |
|                |             |        |        | text           |
|                |             |        |        | description of |
|                |             |        |        | the error      |
|                |             |        |        | detected.      |
+----------------+-------------+--------+--------+----------------+

.. _sect_C.5.7:

Class-Instance conflict
~~~~~~~~~~~~~~~~~~~~~~~

+----------------+-------------+--------+--------+----------------+
| **Status       | **Tag**     | **VR** | **VM** | **Description  |
| Field**        |             |        |        | of Field**     |
+================+=============+========+========+================+
| Affected SOP   | (0000,0002) | UI     | 1      | This optional  |
| Class UID      |             |        |        | field contains |
|                |             |        |        | the SOP Class  |
|                |             |        |        | UID for which  |
|                |             |        |        | the SOP        |
|                |             |        |        | Instance was   |
|                |             |        |        | not a member.  |
+----------------+-------------+--------+--------+----------------+
| Status         | (0000,0900) | US     | 1      | Confirmation   |
|                |             |        |        | status of the  |
|                |             |        |        | operation. The |
|                |             |        |        | value of this  |
|                |             |        |        | required field |
|                |             |        |        | shall be set   |
|                |             |        |        | to 0119H.      |
+----------------+-------------+--------+--------+----------------+
| Affected SOP   | (0000,1000) | UI     | 1      | This optional  |
| Instance UID   |             |        |        | field contains |
|                |             |        |        | the SOP        |
|                |             |        |        | Instance that  |
|                |             |        |        | was not a      |
|                |             |        |        | member of the  |
|                |             |        |        | specified SOP  |
|                |             |        |        | Class.         |
+----------------+-------------+--------+--------+----------------+

.. _sect_C.5.8:

Duplicate SOP Instance
~~~~~~~~~~~~~~~~~~~~~~

+----------------+-------------+--------+--------+----------------+
| **Status       | **Tag**     | **VR** | **VM** | **Description  |
| Field**        |             |        |        | of Field**     |
+================+=============+========+========+================+
| Status         | (0000,0900) | US     | 1      | Confirmation   |
|                |             |        |        | status of the  |
|                |             |        |        | operation. The |
|                |             |        |        | value of this  |
|                |             |        |        | required field |
|                |             |        |        | shall be set   |
|                |             |        |        | to 0111H.      |
+----------------+-------------+--------+--------+----------------+
| Affected SOP   | (0000,1000) | UI     | 1      | This optional  |
| Instance UID   |             |        |        | field contains |
|                |             |        |        | the SOP        |
|                |             |        |        | Instance UID   |
|                |             |        |        | that was       |
|                |             |        |        | already        |
|                |             |        |        | allocated to   |
|                |             |        |        | another SOP    |
|                |             |        |        | Instance.      |
+----------------+-------------+--------+--------+----------------+

.. _sect_C.5.9:

Duplicate invocation
~~~~~~~~~~~~~~~~~~~~

+----------------+-------------+--------+--------+----------------+
| **Status       | **Tag**     | **VR** | **VM** | **Description  |
| Field**        |             |        |        | of Field**     |
+================+=============+========+========+================+
| Status         | (0000,0900) | US     | 1      | Confirmation   |
|                |             |        |        | status of the  |
|                |             |        |        | operation. The |
|                |             |        |        | value of this  |
|                |             |        |        | required field |
|                |             |        |        | shall be set   |
|                |             |        |        | to 0210H.      |
+----------------+-------------+--------+--------+----------------+

.. _sect_C.5.10:

Invalid argument value
~~~~~~~~~~~~~~~~~~~~~~

+----------------+-------------+--------+--------+----------------+
| **Status       | **Tag**     | **VR** | **VM** | **Description  |
| Field**        |             |        |        | of Field**     |
+================+=============+========+========+================+
| Status         | (0000,0900) | US     | 1      | Confirmation   |
|                |             |        |        | status of the  |
|                |             |        |        | operation. The |
|                |             |        |        | value of this  |
|                |             |        |        | required field |
|                |             |        |        | shall be set   |
|                |             |        |        | to 0115H.      |
+----------------+-------------+--------+--------+----------------+
| Affected SOP   | (0000,0002) | UI     | 1      | This optional  |
| Class UID      |             |        |        | field contains |
|                |             |        |        | the SOP Class  |
|                |             |        |        | UID for which  |
|                |             |        |        | an argument    |
|                |             |        |        | value was in   |
|                |             |        |        | error.         |
+----------------+-------------+--------+--------+----------------+
| Affected SOP   | (0000,1000) | UI     | 1      | This optional  |
| Instance UID   |             |        |        | field contains |
|                |             |        |        | the ID of the  |
|                |             |        |        | SOP Instance   |
|                |             |        |        | for which an   |
|                |             |        |        | argument value |
|                |             |        |        | was in error.  |
+----------------+-------------+--------+--------+----------------+
| Event Type ID  | (0000,1002) | US     | 1      | This optional  |
|                |             |        |        | field contains |
|                |             |        |        | the UID of the |
|                |             |        |        | Event Type     |
|                |             |        |        | that was not   |
|                |             |        |        | recognized.    |
|                |             |        |        | Permitted only |
|                |             |        |        | in the         |
|                |             |        |        | N-EVENT-RSP.   |
+----------------+-------------+--------+--------+----------------+
| Event          | (no tag)    | -      | -      | Optionally     |
| Information    |             |        |        | contains the   |
|                |             |        |        | application    |
|                |             |        |        | specific Data  |
|                |             |        |        | Set to only    |
|                |             |        |        | encode the     |
|                |             |        |        | invalid        |
|                |             |        |        | argument       |
|                |             |        |        | values         |
|                |             |        |        | conveyed in    |
|                |             |        |        | the Event      |
|                |             |        |        | Information of |
|                |             |        |        | the request.   |
|                |             |        |        | Permitted only |
|                |             |        |        | in the         |
|                |             |        |        | N-EVE          |
|                |             |        |        | NT-REPORT-RSP. |
+----------------+-------------+--------+--------+----------------+
| Action Type ID | (0000,1008) | US     | 1      | This optional  |
|                |             |        |        | field contains |
|                |             |        |        | the ID of the  |
|                |             |        |        | Action Type    |
|                |             |        |        | that was not   |
|                |             |        |        | recognized.    |
|                |             |        |        | Permitted only |
|                |             |        |        | in the         |
|                |             |        |        | N-ACTION-RSP.  |
+----------------+-------------+--------+--------+----------------+
| Action         | (no tag)    | -      | -      | Optionally     |
| Information    |             |        |        | contains the   |
|                |             |        |        | application    |
|                |             |        |        | specific Data  |
|                |             |        |        | Set to only    |
|                |             |        |        | encode the     |
|                |             |        |        | invalid        |
|                |             |        |        | argument       |
|                |             |        |        | values         |
|                |             |        |        | conveyed in    |
|                |             |        |        | the            |
|                |             |        |        | N-ACTION-RQ.   |
|                |             |        |        | Permitted only |
|                |             |        |        | in the         |
|                |             |        |        | N-ACTION-RSP.  |
+----------------+-------------+--------+--------+----------------+

.. _sect_C.5.11:

Invalid Attribute Value
~~~~~~~~~~~~~~~~~~~~~~~

+----------------+-------------+--------+--------+----------------+
| **Status       | **Tag**     | **VR** | **VM** | **Description  |
| Field**        |             |        |        | of Field**     |
+================+=============+========+========+================+
| Status         | (0000,0900) | US     | 1      | Confirmation   |
|                |             |        |        | status of the  |
|                |             |        |        | operation. The |
|                |             |        |        | value of this  |
|                |             |        |        | required field |
|                |             |        |        | shall be set   |
|                |             |        |        | to 0106H.      |
+----------------+-------------+--------+--------+----------------+
| Modification   | (no tag)    | -      | -      | Optionally     |
| List/Attribute |             |        |        | contains the   |
| List           |             |        |        | application    |
|                |             |        |        | specific Data  |
|                |             |        |        | Set to only    |
|                |             |        |        | encode the     |
|                |             |        |        | invalid        |
|                |             |        |        | Attribute      |
|                |             |        |        | Values         |
|                |             |        |        | conveyed in    |
|                |             |        |        | the            |
|                |             |        |        | Modification   |
|                |             |        |        | List of the    |
|                |             |        |        | N-SET -RQ or   |
|                |             |        |        | the Attribute  |
|                |             |        |        | List of the    |
|                |             |        |        | N-CREATE-RQ.   |
+----------------+-------------+--------+--------+----------------+

.. _sect_C.5.12:

Invalid SOP Instance
~~~~~~~~~~~~~~~~~~~~

+----------------+-------------+--------+--------+----------------+
| **Status       | **Tag**     | **VR** | **VM** | **Description  |
| Field**        |             |        |        | of Field**     |
+================+=============+========+========+================+
| Status         | (0000,0900) | US     | 1      | Confirmation   |
|                |             |        |        | status of the  |
|                |             |        |        | operation. The |
|                |             |        |        | value of this  |
|                |             |        |        | required field |
|                |             |        |        | shall be set   |
|                |             |        |        | to 0117H.      |
+----------------+-------------+--------+--------+----------------+
| Affected SOP   | (0000,1000) | UI     | 1      | This optional  |
| Instance UID   |             |        |        | field contains |
|                |             |        |        | the SOP        |
|                |             |        |        | Instance UID   |
|                |             |        |        | that violated  |
|                |             |        |        | the UID        |
|                |             |        |        | construction   |
|                |             |        |        | rules.         |
+----------------+-------------+--------+--------+----------------+

.. _sect_C.5.13:

Missing Attribute
~~~~~~~~~~~~~~~~~

+----------------+-------------+--------+--------+----------------+
| **Status       | **Tag**     | **VR** | **VM** | **Description  |
| Field**        |             |        |        | of Field**     |
+================+=============+========+========+================+
| Status         | (0000,0900) | US     | 1      | Confirmation   |
|                |             |        |        | status of the  |
|                |             |        |        | operation. The |
|                |             |        |        | value of this  |
|                |             |        |        | required field |
|                |             |        |        | shall be set   |
|                |             |        |        | to 0120H.      |
+----------------+-------------+--------+--------+----------------+
| Attribute      | (0000,1005) | AT     | 1-n    | This optional  |
| Identifier     |             |        |        | field contains |
| List           |             |        |        | an Attribute   |
|                |             |        |        | Tag for each   |
|                |             |        |        | Attribute that |
|                |             |        |        | was not        |
|                |             |        |        | recognized.    |
+----------------+-------------+--------+--------+----------------+

.. _sect_C.5.14:

Missing Attribute Value
~~~~~~~~~~~~~~~~~~~~~~~

+----------------+-------------+--------+--------+----------------+
| **Status       | **Tag**     | **VR** | **VM** | **Description  |
| Field**        |             |        |        | of Field**     |
+================+=============+========+========+================+
| Status         | (0000,0900) | US     | 1      | Confirmation   |
|                |             |        |        | status of the  |
|                |             |        |        | operation. The |
|                |             |        |        | value of this  |
|                |             |        |        | required field |
|                |             |        |        | shall be set   |
|                |             |        |        | to 0121H.      |
+----------------+-------------+--------+--------+----------------+
| Modification   | (no tag)    | -      | -      | Optionally     |
| List/Attribute |             |        |        | contains the   |
| List           |             |        |        | application    |
|                |             |        |        | specific Data  |
|                |             |        |        | Set to only    |
|                |             |        |        | encode missing |
|                |             |        |        | Attribute      |
|                |             |        |        | Values         |
|                |             |        |        | conveyed       |
|                |             |        |        | Modification   |
|                |             |        |        | List of the    |
|                |             |        |        | N-SET -RQ or   |
|                |             |        |        | the Attribute  |
|                |             |        |        | List of the    |
|                |             |        |        | N-CREATE-RQ..  |
+----------------+-------------+--------+--------+----------------+

.. _sect_C.5.15:

Mistyped argument
~~~~~~~~~~~~~~~~~

+----------------+-------------+--------+--------+----------------+
| **Status       | **Tag**     | **VR** | **VM** | **Description  |
| Field**        |             |        |        | of Field**     |
+================+=============+========+========+================+
| Status         | (0000,0900) | US     | 1      | Confirmation   |
|                |             |        |        | status of the  |
|                |             |        |        | operation. The |
|                |             |        |        | value of this  |
|                |             |        |        | required field |
|                |             |        |        | shall be set   |
|                |             |        |        | to 0212H.      |
+----------------+-------------+--------+--------+----------------+

.. _sect_C.5.16:

No such argument
~~~~~~~~~~~~~~~~

+----------------+-------------+--------+--------+----------------+
| **Status       | **Tag**     | **VR** | **VM** | **Description  |
| Field**        |             |        |        | of Field**     |
+================+=============+========+========+================+
| Affected SOP   | (0000,0002) | UI     | 1      | This optional  |
| Class UID      |             |        |        | field shall    |
|                |             |        |        | optionally     |
|                |             |        |        | contain the    |
|                |             |        |        | SOP Class UID  |
|                |             |        |        | for which the  |
|                |             |        |        | argument does  |
|                |             |        |        | not exist.     |
+----------------+-------------+--------+--------+----------------+
| Status         | (0000,0900) | US     | 1      | Confirmation   |
|                |             |        |        | status of the  |
|                |             |        |        | operation. The |
|                |             |        |        | value of this  |
|                |             |        |        | required field |
|                |             |        |        | shall be set   |
|                |             |        |        | to 0114H.      |
+----------------+-------------+--------+--------+----------------+
| Event Type ID  | (0000,1002) | US     | 1      | This optional  |
|                |             |        |        | field contains |
|                |             |        |        | the ID of the  |
|                |             |        |        | Event Type for |
|                |             |        |        | which the      |
|                |             |        |        | argument does  |
|                |             |        |        | not exist.     |
|                |             |        |        | Permitted only |
|                |             |        |        | in the         |
|                |             |        |        | N-EVE          |
|                |             |        |        | NT-REPORT-RSP. |
+----------------+-------------+--------+--------+----------------+
| Action Type ID | (0000,1008) | US     | 1      | This optional  |
|                |             |        |        | field contains |
|                |             |        |        | the ID of the  |
|                |             |        |        | Action Type    |
|                |             |        |        | for which the  |
|                |             |        |        | argument does  |
|                |             |        |        | not exist.     |
|                |             |        |        | Permitted only |
|                |             |        |        | in the         |
|                |             |        |        | N-ACTION-RSP.  |
+----------------+-------------+--------+--------+----------------+

.. _sect_C.5.17:

No such Attribute
~~~~~~~~~~~~~~~~~

+----------------+-------------+--------+--------+----------------+
| **Status       | **Tag**     | **VR** | **VM** | **Description  |
| Field**        |             |        |        | of Field**     |
+================+=============+========+========+================+
| Status         | (0000,0900) | US     | 1      | Confirmation   |
|                |             |        |        | status of the  |
|                |             |        |        | operation. The |
|                |             |        |        | value of this  |
|                |             |        |        | required field |
|                |             |        |        | shall be set   |
|                |             |        |        | to 0105H.      |
+----------------+-------------+--------+--------+----------------+
| Attribute      | (0000,1005) | AT     | 1-n    | This optional  |
| Identifier     |             |        |        | field contains |
| List           |             |        |        | an Attribute   |
|                |             |        |        | Tag for each   |
|                |             |        |        | Attribute that |
|                |             |        |        | was not        |
|                |             |        |        | recognized.    |
+----------------+-------------+--------+--------+----------------+

.. _sect_C.5.18:

No such Event Type
~~~~~~~~~~~~~~~~~~

+----------------+-------------+--------+--------+----------------+
| **Status       | **Tag**     | **VR** | **VM** | **Description  |
| Field**        |             |        |        | of Field**     |
+================+=============+========+========+================+
| Affected SOP   | (0000,0002) | UI     | 1      | This optional  |
| Class UID      |             |        |        | field contains |
|                |             |        |        | the SOP Class  |
|                |             |        |        | UID for which  |
|                |             |        |        | the event type |
|                |             |        |        | does not       |
|                |             |        |        | exist.         |
+----------------+-------------+--------+--------+----------------+
| Status         | (0000,0900) | US     | 1      | Confirmation   |
|                |             |        |        | status of the  |
|                |             |        |        | operation. The |
|                |             |        |        | value of this  |
|                |             |        |        | required field |
|                |             |        |        | shall be set   |
|                |             |        |        | to 0113H.      |
+----------------+-------------+--------+--------+----------------+
| Event Type ID  | (0000,1002) | US     | 1      | This optional  |
|                |             |        |        | field contains |
|                |             |        |        | the ID of the  |
|                |             |        |        | Event Type     |
|                |             |        |        | that does not  |
|                |             |        |        | exist.         |
+----------------+-------------+--------+--------+----------------+

.. _sect_C.5.19:

No such SOP Instance
~~~~~~~~~~~~~~~~~~~~

+----------------+-------------+--------+--------+----------------+
| **Status       | **Tag**     | **VR** | **VM** | **Description  |
| Field**        |             |        |        | of Field**     |
+================+=============+========+========+================+
| Status         | (0000,0900) | US     | 1      | Confirmation   |
|                |             |        |        | status of the  |
|                |             |        |        | operation. The |
|                |             |        |        | value of this  |
|                |             |        |        | required field |
|                |             |        |        | shall be set   |
|                |             |        |        | to 0112H.      |
+----------------+-------------+--------+--------+----------------+
| Affected SOP   | (0000,1000) | UI     | 1      | This optional  |
| Instance UID   |             |        |        | field contains |
|                |             |        |        | the SOP        |
|                |             |        |        | Instance UID   |
|                |             |        |        | that did not   |
|                |             |        |        | exist.         |
+----------------+-------------+--------+--------+----------------+

.. _sect_C.5.20:

No such SOP Class
~~~~~~~~~~~~~~~~~

+----------------+-------------+--------+--------+----------------+
| **Status       | **Tag**     | **VR** | **VM** | **Description  |
| Field**        |             |        |        | of Field**     |
+================+=============+========+========+================+
| Affected SOP   | (0000,0002) | UI     | 1      | This optional  |
| Class UID      |             |        |        | field contains |
|                |             |        |        | the SOP Class  |
|                |             |        |        | UID that does  |
|                |             |        |        | not exist.     |
+----------------+-------------+--------+--------+----------------+
| Status         | (0000,0900) | US     | 1      | Confirmation   |
|                |             |        |        | status of the  |
|                |             |        |        | operation. The |
|                |             |        |        | value of this  |
|                |             |        |        | required field |
|                |             |        |        | shall be set   |
|                |             |        |        | to 0118H.      |
+----------------+-------------+--------+--------+----------------+

.. _sect_C.5.21:

Processing Failure
~~~~~~~~~~~~~~~~~~

+----------------+-------------+--------+--------+----------------+
| **Status       | **Tag**     | **VR** | **VM** | **Description  |
| Field**        |             |        |        | of Field**     |
+================+=============+========+========+================+
| Affected SOP   | (0000,0002) | UI     | 1      | This optional  |
| Class UID      |             |        |        | field contains |
|                |             |        |        | the SOP Class  |
|                |             |        |        | UID on which   |
|                |             |        |        | the processing |
|                |             |        |        | failure        |
|                |             |        |        | occurred.      |
+----------------+-------------+--------+--------+----------------+
| Status         | (0000,0900) | US     | 1      | Confirmation   |
|                |             |        |        | status of the  |
|                |             |        |        | operation. The |
|                |             |        |        | value of this  |
|                |             |        |        | required field |
|                |             |        |        | shall be set   |
|                |             |        |        | to 0110H.      |
+----------------+-------------+--------+--------+----------------+
| Error Comment  | (0000,0902) | LO     | 1      | This optional  |
|                |             |        |        | field contains |
|                |             |        |        | an             |
|                |             |        |        | applic         |
|                |             |        |        | ation-specific |
|                |             |        |        | text           |
|                |             |        |        | description of |
|                |             |        |        | the error      |
|                |             |        |        | detected.      |
+----------------+-------------+--------+--------+----------------+
| Error ID       | (0000,0903) | US     | 1      | This optional  |
|                |             |        |        | field contains |
|                |             |        |        | an             |
|                |             |        |        | applic         |
|                |             |        |        | ation-specific |
|                |             |        |        | error code.    |
+----------------+-------------+--------+--------+----------------+
| Affected SOP   | (0000,1000) | UI     | 1      | This optional  |
| Instance UID   |             |        |        | field shall    |
|                |             |        |        | optionally     |
|                |             |        |        | contain the    |
|                |             |        |        | UID of the SOP |
|                |             |        |        | Instance on    |
|                |             |        |        | which the      |
|                |             |        |        | processing     |
|                |             |        |        | failure        |
|                |             |        |        | occurred.      |
+----------------+-------------+--------+--------+----------------+

.. _sect_C.5.22:

Resource Limitation
~~~~~~~~~~~~~~~~~~~

+----------------+-------------+--------+--------+----------------+
| **Status       | **Tag**     | **VR** | **VM** | **Description  |
| Field**        |             |        |        | of Field**     |
+================+=============+========+========+================+
| Status         | (0000,0900) | US     | 1      | Confirmation   |
|                |             |        |        | status of the  |
|                |             |        |        | operation. The |
|                |             |        |        | value of this  |
|                |             |        |        | required field |
|                |             |        |        | shall be set   |
|                |             |        |        | to 0213H.      |
+----------------+-------------+--------+--------+----------------+

.. _sect_C.5.23:

Unrecognized operation
~~~~~~~~~~~~~~~~~~~~~~

+----------------+-------------+--------+--------+----------------+
| **Status       | **Tag**     | **VR** | **VM** | **Description  |
| Field**        |             |        |        | of Field**     |
+================+=============+========+========+================+
| Status         | (0000,0900) | US     | 1      | Confirmation   |
|                |             |        |        | status of the  |
|                |             |        |        | operation. The |
|                |             |        |        | value of this  |
|                |             |        |        | required field |
|                |             |        |        | shall be set   |
|                |             |        |        | to 0211H.      |
+----------------+-------------+--------+--------+----------------+

.. _sect_C.5.24:

No such Action Type
~~~~~~~~~~~~~~~~~~~

+----------------+-------------+--------+--------+----------------+
| **Status       | **Tag**     | **VR** | **VM** | **Description  |
| Field**        |             |        |        | of Field**     |
+================+=============+========+========+================+
| Affected SOP   | (0000,0002) | UI     | 1      | This optional  |
| Class UID      |             |        |        | field contains |
|                |             |        |        | the SOP Class  |
|                |             |        |        | UID for which  |
|                |             |        |        | the action     |
|                |             |        |        | type does not  |
|                |             |        |        | exist.         |
+----------------+-------------+--------+--------+----------------+
| Status         | (0000,0900) | US     | 1      | Confirmation   |
|                |             |        |        | status of the  |
|                |             |        |        | operation. The |
|                |             |        |        | value of this  |
|                |             |        |        | required field |
|                |             |        |        | shall be set   |
|                |             |        |        | to 0123H.      |
+----------------+-------------+--------+--------+----------------+
| Action Type ID | (0000,1008) | US     | 1      | This optional  |
|                |             |        |        | field contains |
|                |             |        |        | the ID of the  |
|                |             |        |        | Action Type    |
|                |             |        |        | that does not  |
|                |             |        |        | exist.         |
+----------------+-------------+--------+--------+----------------+

.. _sect_C.5.25:

Refused: Not authorized
~~~~~~~~~~~~~~~~~~~~~~~

+----------------+-------------+--------+--------+----------------+
| **Status       | **Tag**     | **VR** | **VM** | **Description  |
| Field**        |             |        |        | of Field**     |
+================+=============+========+========+================+
| Status         | (0000,0900) | US     | 1      | Confirmation   |
|                |             |        |        | status of the  |
|                |             |        |        | operation. The |
|                |             |        |        | value of this  |
|                |             |        |        | required field |
|                |             |        |        | shall be set   |
|                |             |        |        | to 0124H.      |
+----------------+-------------+--------+--------+----------------+
| Error Comment  | (0000,0902) | LO     | 1      | This optional  |
|                |             |        |        | field contains |
|                |             |        |        | an             |
|                |             |        |        | applic         |
|                |             |        |        | ation-specific |
|                |             |        |        | text           |
|                |             |        |        | description of |
|                |             |        |        | the error      |
|                |             |        |        | detected.      |
+----------------+-------------+--------+--------+----------------+

