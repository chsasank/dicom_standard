.. _chapter_H:

Capabilities Description
========================

A Capabilities Description is a WADL Document. See
`biblioentry_title <#biblio_WADL>`__.

The Capabilities Description resource follows directly and unambiguously
from the RESTful resources defined in `Studies Service and
Resources <#chapter_10>`__, `Worklist Service and
Resources <#chapter_11>`__ and `Non-Patient Instance Service and
Resources <#chapter_12>`__.

The WADL document shall contain one top-level "application" element.

The "application" element shall contain one "resources" element whose
"base" attribute value is the base URL for the service. This may be a
combination of protocol (either http or https), host, port, and
application.

Additionally, the WADL content shall include a "resource" element for
the Target Resource specified in the request describing all methods and
child resources for the specified resource and each of its children.

The full resource tree and the methods defined for each resource are
described in `table_title <#table_H-1>`__.

.. note::

   The Retrieve Capabilities Transaction is excluded from
   `table_title <#table_H-1>`__ because that transaction is used to
   retrieve this document and WADL is not self-describing.

.. table:: Resources and Methods

   +----------------+----------------+----------------+----------------+
   | Service        | Resource       | Transactions   | Reference      |
   +================+================+================+================+
   | Studies (see   |                |                |                |
   | `Resource      |                |                |                |
   | Des            |                |                |                |
   | criptions <#se |                |                |                |
   | ct_10.1.1>`__) |                |                |                |
   +----------------+----------------+----------------+----------------+
   |                | studies        | Search for     | `Search        |
   |                |                | Studies        | Transaction <  |
   |                |                |                | #sect_10.6>`__ |
   |                |                | Store          |                |
   |                |                | Instances      | `Store         |
   |                |                |                | Transaction <  |
   |                |                |                | #sect_10.5>`__ |
   +----------------+----------------+----------------+----------------+
   | {              | Retrieve Study | `Retrieve      |                |
   | StudyInstance} |                | Transaction <  |                |
   |                | Store Study    | #sect_10.4>`__ |                |
   |                | Instances      |                |                |
   |                |                | `Store         |                |
   |                |                | Transaction <  |                |
   |                |                | #sect_10.5>`__ |                |
   +----------------+----------------+----------------+----------------+
   | metadata       | Retrieve Study | `Retrieve      |                |
   |                | Metadata       | Transaction <  |                |
   |                |                | #sect_10.4>`__ |                |
   +----------------+----------------+----------------+----------------+
   | series         | Search for     | `Search        |                |
   |                | Study Series   | Transaction <  |                |
   |                |                | #sect_10.6>`__ |                |
   +----------------+----------------+----------------+----------------+
   | {S             | Retrieve       | `Retrieve      |                |
   | eriesInstance} | Series         | Transaction <  |                |
   |                |                | #sect_10.4>`__ |                |
   +----------------+----------------+----------------+----------------+
   | metadata       | Retrieve       | `Retrieve      |                |
   |                | Series         | Transaction <  |                |
   |                | Metadata       | #sect_10.4>`__ |                |
   +----------------+----------------+----------------+----------------+
   | instances      | Search for     | `Retrieve      |                |
   |                | Study Series   | Transaction <  |                |
   |                | Instances      | #sect_10.4>`__ |                |
   +----------------+----------------+----------------+----------------+
   | {SOPInstance}  | Retrieve       | `Retrieve      |                |
   |                | Instance       | Transaction <  |                |
   |                |                | #sect_10.4>`__ |                |
   +----------------+----------------+----------------+----------------+
   | metadata       | Retrieve       | `Retrieve      |                |
   |                | Instance       | Transaction <  |                |
   |                | Metadata       | #sect_10.4>`__ |                |
   +----------------+----------------+----------------+----------------+
   | frames         | N/A            | N/A            |                |
   +----------------+----------------+----------------+----------------+
   | {framelist}    | Retrieve       | `Retrieve      |                |
   |                | Frames         | Transaction <  |                |
   |                |                | #sect_10.4>`__ |                |
   +----------------+----------------+----------------+----------------+
   | instances      | Search for     | `Search        |                |
   |                | Study          | Transaction <  |                |
   |                | Instances      | #sect_10.6>`__ |                |
   +----------------+----------------+----------------+----------------+
   | series         | Search for     | `Search        |                |
   |                | Series         | Transaction <  |                |
   |                |                | #sect_10.6>`__ |                |
   +----------------+----------------+----------------+----------------+
   | {S             | N/A            | N/A            |                |
   | eriesInstance} |                |                |                |
   +----------------+----------------+----------------+----------------+
   | {instances}    | Search for     | `Search        |                |
   |                | Instances      | Transaction <  |                |
   |                |                | #sect_10.6>`__ |                |
   +----------------+----------------+----------------+----------------+
   | instances      | Search for     | `Search        |                |
   |                | Instances      | Transaction <  |                |
   |                |                | #sect_10.6>`__ |                |
   +----------------+----------------+----------------+----------------+
   | {Bulk          | Retrieve       | `Retrieve      |                |
   | DataReference} | Bulkdata       | Transaction <  |                |
   |                |                | #sect_10.4>`__ |                |
   +----------------+----------------+----------------+----------------+
   | Worklist (see  |                |                |                |
   | `Resource      |                |                |                |
   | De             |                |                |                |
   | scription <#se |                |                |                |
   | ct_11.1.1>`__) |                |                |                |
   +----------------+----------------+----------------+----------------+
   |                | workitems      | Search for     | `Search        |
   |                |                | Workitem       | Transaction <  |
   |                |                |                | #sect_11.9>`__ |
   |                |                | Create         |                |
   |                |                | Workitem       | `Create        |
   |                |                |                | Workitem       |
   |                |                |                | Transaction <  |
   |                |                |                | #sect_11.4>`__ |
   +----------------+----------------+----------------+----------------+
   | {Workitem}     | Retrieve       | `Create        |                |
   |                | Workitem       | Workitem       |                |
   |                |                | Transaction <  |                |
   |                | Update         | #sect_11.4>`__ |                |
   |                | Workitem       |                |                |
   |                |                | `Update        |                |
   |                |                | Workitem       |                |
   |                |                | Transaction <  |                |
   |                |                | #sect_11.6>`__ |                |
   +----------------+----------------+----------------+----------------+
   | state          | Change         | `Change        |                |
   |                | Workitem State | Workitem       |                |
   |                |                | State <        |                |
   |                |                | #sect_11.7>`__ |                |
   +----------------+----------------+----------------+----------------+
   | cancelrequest  | Request        | `Request       |                |
   |                | Workitem       | Cancellation < |                |
   |                | Cancellation   | #sect_11.8>`__ |                |
   +----------------+----------------+----------------+----------------+
   | subscribers    | N/A            | N/A            |                |
   +----------------+----------------+----------------+----------------+
   | {AETitle}      | Subscribe      | `Subscribe     |                |
   |                |                | Transaction <# |                |
   |                | Unsubscribe    | sect_11.10>`__ |                |
   |                |                |                |                |
   |                |                | `Unsubscribe   |                |
   |                |                | Transaction <# |                |
   |                |                | sect_11.11>`__ |                |
   +----------------+----------------+----------------+----------------+
   | 1.2.840.10     | N/A            | N/A            |                |
   | 008.5.1.4.34.5 |                |                |                |
   +----------------+----------------+----------------+----------------+
   | subscribers    | N/A            | N/A            |                |
   +----------------+----------------+----------------+----------------+
   | {AETitle}      | Subscribe      | `Subscribe     |                |
   |                |                | Transaction <# |                |
   |                | Unsubscribe    | sect_11.10>`__ |                |
   |                |                |                |                |
   |                |                | `Unsubscribe   |                |
   |                |                | Transaction <# |                |
   |                |                | sect_11.11>`__ |                |
   +----------------+----------------+----------------+----------------+
   | suspend        | Unsubscribe    | `Unsubscribe   |                |
   |                |                | Transaction <# |                |
   |                |                | sect_11.11>`__ |                |
   +----------------+----------------+----------------+----------------+
   | 1.2.840.1000   | N/A            | N/A            |                |
   | 8.5.1.4.34.5.1 |                |                |                |
   +----------------+----------------+----------------+----------------+
   | subscribers    | N/A            | N/A            |                |
   +----------------+----------------+----------------+----------------+
   | {AETitle}      | Subscribe      | `Subscribe     |                |
   |                |                | Transaction <# |                |
   |                | Unsubscribe    | sect_11.10>`__ |                |
   |                |                |                |                |
   |                |                | `Unsubscribe   |                |
   |                |                | Transaction <# |                |
   |                |                | sect_11.11>`__ |                |
   +----------------+----------------+----------------+----------------+
   | suspend        | Suspend        | `Unsubscribe   |                |
   |                | Worklist       | Transaction <# |                |
   |                | Subscription   | sect_11.11>`__ |                |
   +----------------+----------------+----------------+----------------+
   | Non-Patient    |                |                |                |
   | Instances (see |                |                |                |
   | `Resource      |                |                |                |
   | Des            |                |                |                |
   | criptions <#se |                |                |                |
   | ct_12.1.1>`__) |                |                |                |
   +----------------+----------------+----------------+----------------+
   |                | color-palettes | N/A            | N/A            |
   +----------------+----------------+----------------+----------------+
   | {uid}          | Retrieve       | `Retrieve      |                |
   |                |                | Transaction <  |                |
   |                | Store          | #sect_12.4>`__ |                |
   |                |                |                |                |
   |                | Search         | `Store         |                |
   |                |                | Transaction <  |                |
   |                |                | #sect_12.5>`__ |                |
   |                |                |                |                |
   |                |                | `Search        |                |
   |                |                | Transaction <  |                |
   |                |                | #sect_12.6>`__ |                |
   +----------------+----------------+----------------+----------------+
   | defined-proc   | N/A            | N/A            |                |
   | edure-protocol |                |                |                |
   +----------------+----------------+----------------+----------------+
   | {uid}          | Retrieve       | `Retrieve      |                |
   |                |                | Transaction <  |                |
   |                | Store          | #sect_12.4>`__ |                |
   |                |                |                |                |
   |                | Search         | `Store         |                |
   |                |                | Transaction <  |                |
   |                |                | #sect_12.5>`__ |                |
   |                |                |                |                |
   |                |                | `Search        |                |
   |                |                | Transaction <  |                |
   |                |                | #sect_12.6>`__ |                |
   +----------------+----------------+----------------+----------------+
   | ha             | N/A            | N/A            |                |
   | nging-protocol |                |                |                |
   +----------------+----------------+----------------+----------------+
   | {uid}          | Retrieve       | `Retrieve      |                |
   |                |                | Transaction <  |                |
   |                | Store          | #sect_12.4>`__ |                |
   |                |                |                |                |
   |                | Search         | `Store         |                |
   |                |                | Transaction <  |                |
   |                |                | #sect_12.5>`__ |                |
   |                |                |                |                |
   |                |                | `Search        |                |
   |                |                | Transaction <  |                |
   |                |                | #sect_12.6>`__ |                |
   +----------------+----------------+----------------+----------------+
   | imp            | N/A            | N/A            |                |
   | lant-templates |                |                |                |
   +----------------+----------------+----------------+----------------+
   | {uid}          | Retrieve       | `Retrieve      |                |
   |                |                | Transaction <  |                |
   |                | Store          | #sect_12.4>`__ |                |
   |                |                |                |                |
   |                | Search         | `Store         |                |
   |                |                | Transaction <  |                |
   |                |                | #sect_12.5>`__ |                |
   |                |                |                |                |
   |                |                | `Search        |                |
   |                |                | Transaction <  |                |
   |                |                | #sect_12.6>`__ |                |
   +----------------+----------------+----------------+----------------+

