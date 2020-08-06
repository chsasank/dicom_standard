.. _chapter_C:

Query/Retrieve Service Class (Normative)
========================================

.. _sect_C.1:

Overview
--------

.. _sect_C.1.1:

Scope
~~~~~

The Query/Retrieve Service Class defines an application-level
class-of-service that facilitates the simple management of Composite
Object Instances in a manner functionally similar to ACR-NEMA 300-1988.
The types of queries that are allowed are not complex. This Service
Class is not intended to provide a comprehensive generalized database
query mechanism such as SQL. Instead, the Query/Retrieve Service Class
is focused towards basic Composite Object Instance information queries
using a small set of common Key Attributes.

In addition, the Query/Retrieve Service Class provides the ability to
retrieve/transfer a well-identified set of Composite Object Instances.
The retrieve/transfer capability allows a DICOM AE to retrieve Composite
Object Instances from a remote DICOM AE or request the remote DICOM AE
to initiate a transfer of Composite Object Instances to another DICOM
AE.

.. note::

   Functional similarity to ACR-NEMA 300-1988 facilitates the migration
   to DICOM.

An Enhanced Multi-Frame Image Conversion Extended Negotiation option
allows the Query/Retrieve Service Class to access Classic single-frame
images that have been converted to Enhanced multi-frame images, or
vice-versa. This is achieved by providing alternative "views" of
studies, such that:

-  the default view provides the images in the form they were received,

-  a Classic single-frame "view" provides images as Classic single frame
   (that were received that way or have been converted from Enhanced
   multi-frame),

-  an Enhanced multi-frame "view" provides images as Enhanced
   multi-frame (that were received that way or have been converted to
   Enhanced multi-frame).

A query or retrieval above the IMAGE level does not show or return
duplicate information (two sets of images). The SCU may request the
default, enhanced multi-frame or Classic single frame view. For each
view, referential integrity is required to be consistent within the
scope of the Patient and that view; i.e., references to UIDs will be
converted in all Instances, not only within converted images.

.. note::

   1. The Classic single-frame view is not intended as an alternative to
      the Frame Level Retrieve SOP Classes defined in `Composite
      Instance Root Retrieve Service Class (Normative) <#chapter_Y>`__.
      Enhanced Image Storage SOP Classes and Frame Level Retrieve SOP
      Classes should be used together since they support a unified view
      of the relationships between instances through a common set of
      UIDs.

   2. In the Enhanced view, Instances that have no Enhanced equivalent
      will be returned in their original form but with referential
      integrity related changes.

.. _sect_C.1.2:

Conventions
~~~~~~~~~~~

The following conventions are used to define the types of keys used in
Query/Retrieve Information Models.

.. table:: Key Type Conventions for Query/Retrieve Information Models

   ====== ======================
   Symbol Description
   ====== ======================
   U      Unique Key Attribute
   R      Required Key Attribute
   O      Optional Key Attribute
   ====== ======================

.. _sect_C.1.3:

Query/Retrieve Information Model
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

In order to serve as an SCP of the Query/Retrieve Service Class, a DICOM
AE possesses information about the Attributes of a number of stored
Composite Object Instances. This information is organized into a well
defined Query/Retrieve Information Model. The Query/Retrieve Information
Model shall be a standard Query/Retrieve Information Model, as defined
in this Annex of the DICOM Standard.

Queries and Retrievals are implemented against well defined Information
Models. A specific SOP Class of the Query/Retrieve Service Class
consists of an Information Model Definition and a DIMSE-C Service Group.
In this Service Class, the Information Model plays a role similar to an
Information Object Definition (IOD) of most other DICOM Service Classes.

.. _sect_C.1.4:

Service Definition
~~~~~~~~~~~~~~~~~~

Two peer DICOM AEs implement a SOP Class of the Query/Retrieve Service
Class with one serving in the SCU role and one serving in the SCP role.
SOP Classes of the Query/Retrieve Service Class are implemented using
the DIMSE-C C-FIND, C-MOVE, and C-GET services as defined in .

Both a baseline and extended behavior is defined for the DIMSE-C C-FIND,
C-MOVE, and C-GET services. Baseline behavior specifies a minimum level
of conformance for all implementations to facilitate interoperability.
Extended behavior enhances the baseline behavior to provide additional
features that may be negotiated independently at Association
establishment time.

The following descriptions of the DIMSE-C C-FIND, C-MOVE, and C-GET
services provide a brief overview of the SCU/SCP semantics:

a. A C-FIND service conveys the following semantics:

   -  The SCU requests that the SCP perform a match of all the keys
      specified in the Identifier of the request, against the
      information it possesses, to the level (E.g. Patient, Study,
      Series, or Composite Object Instance) specified in the request.

      .. note::

         In this Annex, the term "Identifier" refers to the Identifier
         service parameter of the C-FIND, C-MOVE, or C-GET service as
         defined in .

   -  The SCP generates a C-FIND response for each match with an
      Identifier containing the values of all key fields and all known
      Attributes requested. All such responses will contain a status of
      Pending. A status of Pending indicates that the process of
      matching is not complete.

   -  When the process of matching is complete a C-FIND response is sent
      with a status of Success and no Identifier.

   -  A Refused or Failed response to a C-FIND request indicates that
      the SCP is unable to process the request.

   -  The SCU may cancel the C-FIND service by issuing a C-FIND-CANCEL
      request at any time during the processing of the C-FIND service.
      The SCP will interrupt all matching and return a status of
      Canceled.

b. A C-MOVE service conveys the following semantics:

   -  The SCU supplies Unique Key values to identify an entity at the
      level of the retrieval. The SCP of the C-MOVE initiates C-STORE
      sub-operations for the corresponding storage SOP Instances
      identified by Unique Key values. These C-STORE sub-operations
      occur on a different Association than the C-MOVE service. The SCP
      role of the Query/Retrieve SOP Class and the SCU role of the
      Storage SOP Class may be performed by different applications that
      may or may not reside on the same system. Initiation mechanism of
      C-STORE sub-operations is outside of the scope of DICOM Standard.

      .. note::

         This does not imply that they use the same AE Title. See
         `C-MOVE SCP Conformance <#sect_C.6.1.2.2.2>`__ and `C-MOVE SCP
         Conformance <#sect_C.6.2.2.2.2>`__ for the requirements to the
         C-MOVE SCP conformance.

   -  The SCP may optionally generate responses to the C-MOVE with
      status equal to Pending during the processing of the C-STORE
      sub-operations. These C-MOVE responses indicate the number of
      Remaining C-STORE sub-operations and the number of C-STORE
      sub-operations returning the status of Success, Warning, and
      Failed.

   -  When the number of Remaining C-STORE sub-operations reaches zero,
      the SCP generates a final response with a status equal to Success,
      Warning, Failed, or Refused. This response may indicate the number
      of C-STORE sub-operations returning the status of Success,
      Warning, and Failed. If the status of a C-STORE sub-operation was
      Failed a UID List will be returned.

   -  The SCU may cancel the C-MOVE service by issuing a C-MOVE-CANCEL
      request at any time during the processing of the C-MOVE. The SCP
      terminates all incomplete C-STORE sub-operations and returns a
      status of Canceled.

c. A C-GET service conveys the following semantics:

   -  The SCU supplies Unique Key values to identify an entity at the
      level of the retrieval. The SCP generates C-STORE sub-operations
      for the corresponding storage SOP Instances identified by the
      Unique Key values. These C-STORE sub-operations occur on the same
      Association as the C-GET service and the SCU/SCP roles will be
      reversed for the C-STORE.

   -  The SCP may optionally generate responses to the C-GET with status
      equal to Pending during the processing of the C-STORE
      sub-operations. These C-GET responses indicate the number of
      Remaining C-STORE sub-operations and the number of C-STORE
      sub-operations returning the status of Success, Warning, and
      Failed.

   -  When the number of Remaining C-STORE sub-operations reaches zero,
      the SCP generates a final response with a status equal to Success,
      Warning, Failed, or Refused. This response may indicate the number
      of C-STORE sub-operations returning the status of Success,
      Warning, and Failed. If the status of a C-STORE sub-operation was
      Failed a UID List will be returned.

   -  The SCU may cancel the C-GET service by issuing a C-GET-CANCEL
      request at any time during the processing of the C-GET. The SCP
      terminates all incomplete C-STORE sub-operations and returns a
      status of Canceled.

.. _sect_C.2:

Query/Retrieve Information Model Definition
-------------------------------------------

The Query/Retrieve Information Model is identified by the SOP Class
negotiated at Association establishment time. The SOP Class is composed
of both an Information Model and a DIMSE-C Service Group.

.. note::

   This SOP Class identifies the class of the Query/Retrieve Information
   Model (i.e., not the SOP Class of the stored SOP Instances for which
   the SCP has information).

Information Model Definitions for Standard SOP Classes of the
Query/Retrieve Service Class are defined in this Annex. A Query/Retrieve
Information Model Definition contains:

-  Entity-Relationship Model Definition

-  Key Attributes Definition

.. _sect_C.2.1:

Entity-Relationship Model Definition
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

For any Query/Retrieve Information Model, an Entity-Relationship Model
defines a hierarchy of entities, with Attributes defined for each level
in the hierarchy (e.g., Patient, Study, Series, Composite Object
Instance).

.. _sect_C.2.2:

Attributes Definition
~~~~~~~~~~~~~~~~~~~~~

Attributes shall be defined at each level in the Entity-Relationship
Model. An Identifier in a C-FIND, C-MOVE, or C-GET command shall contain
values to be matched against the Attributes of the Entities in a
Query/Retrieve Information Model. For any query, the set of entities for
which Attributes are returned, shall be determined by the set of Key
Attributes specified in the Identifier that have corresponding matches
on entities managed by the SCP associated with the query.

.. _sect_C.2.2.1:

Attribute Types
^^^^^^^^^^^^^^^

All Attributes of entities in a Query/Retrieve Information Model shall
be either a Unique Key, Required Key, or Optional Key. The term Key
Attributes refers to Unique, Required, and Optional Key Attributes.

.. _sect_C.2.2.1.1:

Unique Keys
'''''''''''

At each level in the Entity-Relationship Model, one Attribute shall be
defined as a Unique Key. A single value in a Unique Key Attribute shall
uniquely identify a single entity at a given level. That is, two
entities at the same level may not have the same Unique Key value.

C-FIND, C-MOVE, and C-GET SCPs shall support existence and matching of
all Unique Keys defined by a Query/Retrieve Information Model. All
entities managed by C-FIND, C-MOVE, and C-GET SCPs shall have a specific
non-zero length Unique Key value.

Unique Keys may be contained in the Identifier of a C-FIND request.
Unique Keys shall be contained in the Identifier of C-MOVE and C-GET
requests.

.. _sect_C.2.2.1.2:

Required Keys
'''''''''''''

At each level in the Entity-Relationship Model, a set of Attributes
shall be defined as Required Keys. Required Keys imply the SCP of a
C-FIND shall support matching based on a value contained in a Required
Key of the C-FIND request. Multiple entities may have the same value for
Required Keys. That is, a distinct value in a Required Key shall not
necessarily identify a single entity at the level of the key.

C-FIND SCPs shall support existence and matching of all Required Keys
defined by a Query/Retrieve Information Model. If a C-FIND SCP manages
an entity with a Required Key of zero length, the value is considered
unknown and all matching against the zero length Required Key shall be
considered a successful match.

Required Keys may be contained in the Identifier of a C-FIND request.
Required Keys shall not be contained in the Identifier of C-MOVE and
C-GET requests.

.. _sect_C.2.2.1.3:

Optional Keys
'''''''''''''

At each level in the Entity-Relationship Model, a set of Attributes
shall be defined as Optional Keys.

Optional Keys contained in the Identifier of a C-FIND request may have
three different types of behavior depending on support for existence
and/or matching by the C-FIND SCP. If the C-FIND SCP:

-  does not support the existence of the Optional Key, then the
   Attribute shall not be returned in C-FIND responses

-  supports the existence of the Optional Key but does not support
   matching on the Optional Key, then the Optional Key shall be
   processed in the same manner as a zero length Required Key. That is,
   the value specified to be matched for the Optional Key is ignored but
   a value may be returned by the SCP for this Optional Key.

-  supports the existence and matching of the Optional Key, then the
   Optional Key shall be processed in the same manner as a Required Key.

.. note::

   1. C-FIND SCU may not assume an Optional Key with non-zero length
      will be processed in the same manner as a Required Key. The
      Conformance Statement of the C-FIND SCP shall list the Optional
      Keys that are supported.

   2. Optional Keys are differentiated from Required Keys in that
      Optional Keys may or may not be supported for existence and/or
      matching by C-FIND SCPs. Whereas, Required Keys must always be
      supported by C-FIND SCPs.

Optional Keys may be contained in the Identifier of a C-FIND request.
Optional Keys shall not be contained in the Identifier of C-MOVE and
C-GET requests.

.. _sect_C.2.2.2:

Attribute Matching
^^^^^^^^^^^^^^^^^^

The following types of matching may be performed on Key Attributes in
the Query/Retrieve Service Class:

-  Single Value Matching

-  List of UID Matching

-  Universal Matching

-  Wild Card Matching

-  Range Matching

-  Sequence Matching

Matching requires special characters (i.e., "*","?","-", "=" and "\"),
which need not be part of the character repertoire for the VR of the Key
Attributes.

.. note::

   1. For example, the "-" character is not valid for the DA, DT and TM
      VRs but is used for Range Matching. The wild card characters "*"
      and "?" are not valid for the CS VR but are used for Wild Card
      Matching.

   2. When character sets other than the Default Character Repertoire
      are used, then the rules in apply, such as with respect to the use
      of the 05/12 "\" (BACKSLASH) (in ISO IR 6) or 05/12 "¥" (YEN SIGN)
      (in ISO IR 14).

The total length of the Key Attribute may exceed the length as specified
in the VR in . The Value Multiplicity (VM) may be larger than the VM
specified in for the Key Attribute, as defined for particular Matching
Type.

The Specific Character Set (0008,0005) Attribute may be present in the
Identifier but is never matched. Rather, it specifies how other
Attributes are encoded in the Request and Response Identifiers.

It may influence how matching of other Attributes is performed. If
Specific Character Set (0008,0005) is absent, then the Default Character
Repertoire shall be used. Specific Character Set (0008,0005) shall not
have a zero length value.

Specific Character Set (0008,0005) may have multiple values if escape
sequences are used to switch between character repertoires within
values.

If the SCP does not support the value(s) of Specific Character Set
(0008,0005) in the Request Identifier, then the manner in which matching
is performed is undefined and shall be specified in the conformance
statement.

.. note::

   1. If an SCU sends a Request Identifier with a single byte character
      set not supported by the SCP, then it is likely, but not required,
      that the SCP will treat unrecognized characters as wild cards and
      match only on characters in the default repertoire, and return a
      response in the default repertoire.

   2. Some Specific Character Set values are used with multi-component
      group person names (e.g., single-byte, ideographic and phonetic
      and phonetic component groups separated by an "=" (3DH)
      character), which may also affect the behavior of literal string
      matching.

The Timezone Offset From UTC (0008,0201) Attribute may be present in the
Identifier but is not matched if Timezone query adjustment is
negotiated. If Timezone query adjustment is negotiated, it specifies how
Attribute Values of VR of DT and TM (including related Attribute Values
of VR of DA, if present) are interpreted in the Request and Response
Identifiers if those values lack a specific time zone offset
specification.

.. _sect_C.2.2.2.1:

Single Value Matching
'''''''''''''''''''''

If the value specified for a Key Attribute in a request is non-zero
length and if it is not of VR SQ and:

a. of VR of AE, CS, LO, LT, PN, SH, ST, UC, UR or UT and contains no
   wild card characters, or

b. of VR of DA, TM or DT and contains a single value with no "-", or

c. of any other VR

then Single Value Matching shall be performed. Except for Attributes
with a PN VR, only entities with values that match exactly the value
specified in the request shall match. This matching is case-sensitive,
i.e., sensitive to the exact encoding of the key Attribute Value in
character sets where a letter may have multiple encodings (e.g., based
on its case, its position in a word, or whether it is accented).

.. _sect_C.2.2.2.1.1:

Attributes of VR of PN
                      

For Attributes with a PN VR (e.g., Patient Name (0010,0010)), an
application may perform literal matching that is either case-sensitive,
or that is insensitive to some or all aspects of case, position, accent,
or other character encoding variants.

.. note::

   For multi-component names, the component group delimiter "=" (3DH)
   may be present in the Key Attribute Value, but may give unexpected
   results if the SCP does not support matching on separate components
   but interprets the entire value literally as a single string. E.g.,
   "Wang^XiaoDong=王^小東" may or may not match "Wang^XiaoDong" or
   "王^小東"; Wild Card Matching without the component group delimiter,
   such as "*Wang^XiaoDong*" or "*王^小東 \*" may be necessary.

If extended negotiation of fuzzy semantic matching rather than literal
matching of PN VR is successful, not only may matching be insensitive to
case, position, accent, and character encoding (including combining
characters), but in addition other techniques such as phonetic matching
may be applied.

.. note::

   1. Matching of PN Attributes may be accent-insensitive, as specified
      in the conformance statement. Accent-insensitive matching would
      successfully match, for instance, a query character "SMALL LETTER
      a" (06/01 in the default ISO-IR 6) with

      -  "SMALL LETTER a WITH GRAVE ACCENT" (14/00 in ISO-IR 100),

      -  "SMALL LETTER a WITH TILDE" (14/03 in ISO-IR 100),

      -  "SMALL LETTER a WITH BREVE" (14/03 in ISO-IR 101), and

      -  "CAPITAL LETTER a WITH ACUTE ACCENT" (12/01 in ISO-IR 100) (if
         matching is also case-insensitive),

      but would not match 14/00 in ISO-IR 101, which is "SMALL LETTER r
      WITH ACUTE ACCENT". Matching to particular bit-combinations is
      specific to each supported character set (note the difference in
      meaning of 14/00), and should be described in the conformance
      statement.

   2. An SCU application may elect to perform additional filtering of
      the responses by applying the matching rules itself. In the event
      that both the SCU and SCP are applying the matching rules, this
      process will be successful as long as literal matching is
      performed by both, and any additional SCU filtering is insensitive
      to case, position, accent, or other character encoding variants.

However if fuzzy semantic matching of PN Attributes has been negotiated,
matching by the SCP may result in responses that are not obviously
related to the request, hence care should be taken if any additional
filtering of responses is performed by the SCU. For example, if phonetic
matching is performed, a query for "Swain" might well return "Swayne",
or if name component order insensitive matching is performed, a query
for "Smith^Mary" might well return "Mary^Smith" or "Mary Smith" or
"Smith, Mary". Fuzzy semantic matching may also take into account
separate single-byte, ideographic and phonetic name component groups.

.. _sect_C.2.2.2.1.2:

Attributes of VR of AE, CS, LO, LT, PN, SH, ST, UC, UR and UT
                                                             

The AE, LO, LT, PN, SH, ST, UC, UR and UT VRs allow the presence of wild
card characters "*" and "?". Wild card matching is also defined for CS
values. Single value matching against such characters is not supported.
See `Wild Card Matching <#sect_C.2.2.2.4>`__.

.. _sect_C.2.2.2.1.3:

Attributes of VR of DA, DT or TM
                                

If the Timezone Offset From UTC (0008,0201) Attribute is present in the
Identifier and Timezone query adjustment was negotiated, it shall be
used to adjust values of Attributes of VR of TM (and associated
Attributes of VR of DA, if present) from the local timezone to UTC. It
shall also adjust values of Attributes of VR of DT that do not specify a
timezone offset. The encoding and semantics of the Timezone Offset From
UTC (0008,0201) Attribute shall be as defined in the SOP Common Module
in .

The manner in which matching is performed is implementation dependent
and shall be specified in the conformance statement.

.. note::

   1. This definition implies that values of VR of TM, DA and DT are
      matched by their meaning, not as literal strings. For example:

      -  the DT "19980128103000.0000" matches "19980128103000"

      -  the DT "19980128103000" with no timezone offset matches
         "19980128073000" with timezone offset "-0300"

      -  the TM "2230" matches "223000"

   2. If an application is concerned about how Single Value Matching of
      dates and times is performed by another application, it may
      consider using Range Matching instead, which is always performed
      by meaning, with both values in the range the same.

   3. Exclusion of the "-" character for Single Value Matching implies
      that a Key Attribute with a VR of DT may not contain a negative
      offset from Universal Coordinated Time (UTC) if Single Value
      Matching is intended. Use of the "-" character in values of VR of
      TM, DA and DT indicates Range Matching.

   4. If an application is in a local time zone that has a negative
      offset then it cannot perform Single Value Matching using a local
      time notation. Instead, it can convert the Key Attribute Value to
      UTC and use an explicit suffix of "+0000".

.. _sect_C.2.2.2.2:

List of UID Matching
''''''''''''''''''''

A List of UIDs is encoded by using the value multiplicity operator,
backslash ("\"), as a delimiter between UIDs. Each item in the list
shall contain a single UID value. Each UID in the list contained in the
Identifier of the request may generate a match.

.. note::

   A list of single values is encoded exactly as a VR of UI and a VM of
   Multiple (see ).

.. _sect_C.2.2.2.3:

Universal Matching
''''''''''''''''''

If the value specified for a Key Attribute in a request is zero length,
then all entities shall match this Attribute. An Attribute that contains
a Universal Match specification in a C-FIND request provides a mechanism
to request the selected Attribute Value be returned in corresponding
C-FIND responses.

.. _sect_C.2.2.2.4:

Wild Card Matching
''''''''''''''''''

If the Attribute is of VR of AE, CS, LO, LT, PN, SH, ST, UC, UR, UT and
the value specified in the request contains any occurrence of an "*" or
a "?", then "*" shall match any sequence of characters (including a zero
length value) and "?" shall match any single character. This matching is
case sensitive, except for Attributes with a PN VR (e.g., Patient Name
(0010,0010)).

For Attributes with a PN VR, including the case of extended negotiation
of fuzzy semantic matching, Wild Card Matching is implementation
dependent and shall be specified in the conformance statement.

.. note::

   1. Wild card matching on a value of "*" is equivalent to Universal
      Matching.

   2. The Wild Card Matching method specified by DICOM might not be
      supported by some non-DICOM multi-byte character text processors.

   3. For multi-component group names, the component group delimiter "="
      (3DH) may be present in the Key Attribute Value, but may give
      unexpected results if the SCP does not support matching on
      separate components but interprets the entire value literally.
      E.g., "*=*" or "*=*=*" may or may not return all strings, and
      hence is not equivalent to "*", nor to Universal Matching.

   4. Attributes with VR of AE, LO, PN, SH and UC may contain wild card
      characters "*" and "?". Attempts to match on a string explicitly
      containing "*" or "?" will be treated as Wild Card Matching and
      thus may return multiple results rather than a single one. There
      is no mechanism for Single Value Matching on values that contain
      characters "*" and "?" for these VRs - such queries will always be
      treated as queries with Wild Card Matching.

   5. Attributes with VR of ST, LT and UT are intended for conveying
      narrative text and may contain wild card characters "*" and "?".
      Attempts to match on a string explicitly containing "*" or "?"
      will be treated as Wild Card Matching and thus may return multiple
      results rather than a single one. There is no mechanism for Single
      Value Matching on values that contain characters "*" and "?" for
      these VRs - such queries will always be treated as queries with
      Wild Card Matching.

   6. Attributes with VR of UR may contain wild card characters "*" and
      "?" as delimiters. These characters are reserved according to
      `biblioentry_title <#biblio_RFC_3986>`__ Section 2. Attempts to
      match on a string explicitly containing "*" or "?" will be treated
      as Wild Card Matching and thus may return multiple results rather
      than a single one. There is no mechanism for Single Value Matching
      on values that contain characters "*" and "?" for these VRs - such
      queries will always be treated as queries with Wild Card Matching.

.. _sect_C.2.2.2.5:

Range Matching
''''''''''''''

.. _sect_C.2.2.2.5.1:

Range Matching of Attributes of VR of DA
                                        

In the absence of extended negotiation, then:

a. A string of the form "<date1> - <date2>", where <date1> is less or
   equal to <date2>, shall match all occurrences of dates that fall
   between <date1> and <date2> inclusive

b. A string of the form "- <date1>" shall match all occurrences of dates
   prior to and including <date1>

c. A string of the form "<date1> -" shall match all occurrences of
   <date1> and subsequent dates

.. _sect_C.2.2.2.5.2:

Range Matching of Attributes of VR of TM
                                        

All comparison specified in the following shall be based on a direct
comparison of times within a day. "Prior" includes all times starting
from midnight of the same day to the specified time. "Subsequent"
includes all times starting with the specified time until any time prior
to midnight of the following day. Range matching crossing midnight is
not supported.

No offset from Universal Coordinated Time is permitted in the TM VR
values. If Timezone Offset From UTC (0008,0201) is present in the query
identifier, the specified time values and the definition of midnight are
in the specified timezone.

In the absence of extended negotiation, then:

a. A string of the form "<time1> - <time2>", where <time1> is less or
   equal to <time2>, shall match all occurrences of times that fall
   between <time1> and <time2> inclusive

b. A string of the form "- <time1>" shall match all occurrences of times
   prior to and including <time1>

c. A string of the form "<time1> -" shall match all occurrences of
   <time1> and subsequent times

.. _sect_C.2.2.2.5.3:

Range Matching of Attributes of VR of DT
                                        

a. A string of the form "<datetime1> - <datetime2>", where <datetime1>
   is less or equal to <datetime2>, shall match all moments in time that
   fall between <datetime1> and <datetime2> inclusive

b. A string of the form "- <datetime1>" shall match all moments in time
   prior to and including <datetime1>

c. A string of the form "<datetime1> -" shall match all moments in time
   subsequent to and including <datetime1>

d. The offset from Universal Coordinated Time, if present in the Value
   of the Attribute, shall be taken into account for the purposes of the
   match.

.. _sect_C.2.2.2.5.4:

Range Matching General Rules
                            

If extended negotiation of combined datetime matching is successful,
then a pair of Attributes that are of VR DA and TM, both of which
specify the same form of Range Matching, shall have the concatenated
string values of each Range Matching component matched as if they were a
single Attribute of VR DT.

.. note::

   For example, a Study Date of "20060705-20060707" and a Study Time of
   "1000-1800" will match the time period of July 5, 10am until July 7,
   6pm, rather than the three time periods of 10am until 6pm on each of
   July 5, July 6 and July 7, as would be the case without extended
   negotiation.

Regardless of other extended negotiation, an application may use the
value of Timezone Offset From UTC (0008,0201) to adjust values of
Attributes of VR TM and DT from the local timezone to UTC for matching.
See `Single Value Matching <#sect_C.2.2.2.1>`__.

.. note::

   If extended negotiation of combined datetime matching is successful,
   the timezone offset may effect a change in date if the local time and
   UTC are on different sides of midnight.

Range matching is not defined for types of Attributes other than dates
and times.

.. _sect_C.2.2.2.6:

Sequence Matching
'''''''''''''''''

If a Key Attribute in the Identifier of a C-FIND request needs to be
matched against an Attribute structured as a Sequence of Items (VR of
SQ), the Key Attribute shall be structured as a Sequence of Items with a
single Item. This Item may contain zero or more Item Key Attributes.
Each Item Key Attribute matching shall be performed on an Item by Item
basis. The types of matching defined in `Attribute
Matching <#sect_C.2.2.2>`__ shall be used: Single Value Matching, List
of UID Matching, Universal Matching, Wild Card Matching, Range Matching
and Sequence Matching (recursive Sequence matching).

If all the Item Key Attributes match, for at least one of the Items of
the Attribute against which the match is performed, a successful match
is generated. A sequence of matching Items containing only the requested
Attributes is returned in the corresponding C-FIND responses.

If the Key Attribute in the Identifier of a C-FIND request contains no
Key Item Attribute (zero-length Item Tag), then all entities shall match
this Attribute. This provides a Universal Matching like mechanism to
request that the selected Key Attribute Value (the entire Sequence of
Items) be returned in corresponding C-FIND responses.

.. _sect_C.2.2.3:

Matching Multiple Values
^^^^^^^^^^^^^^^^^^^^^^^^

When matching an Attribute that has a value multiplicity of greater than
one, if any of the values match, then all values shall be returned.

.. _sect_C.3:

Standard Query/Retrieve Information Models
------------------------------------------

Three standard Query/Retrieve Information Models are defined in this
Annex. Each Query/Retrieve Information Model is associated with a number
of SOP Classes. The following three hierarchical Query/Retrieve
Information Models are defined:

-  Patient Root

-  Study Root

-  Patient/Study Only

.. _sect_C.3.1:

Patient Root Query/Retrieve Information Model
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

The Patient Root Query/Retrieve Information Model is based upon a four
level hierarchy:

-  Patient

-  Study

-  Series

-  Composite Object Instance

The patient level is the top level and contains Attributes associated
with the Patient Information Entity (IE) of the Composite IODs as
defined in . Patients IEs are modality independent.

The study level is below the patient level and contains Attributes
associated with the Study IE of the Composite IODs as defined in . A
study belongs to a single patient. A single patient may have multiple
studies. Study IEs are modality independent.

The series level is below the study level and contains Attributes
associated with the Series, Frame of Reference and Equipment IEs of the
Composite IODs as defined in . A series belongs to a single study. A
single study may have multiple series. Series IEs are modality
dependent. To accommodate this modality dependence, the set of Optional
Keys at the series level includes all Attributes defined at the series
level from any Composite IOD defined in .

The lowest level is the Composite Object Instance level and contains
Attributes associated with the Composite object IE of the Composite IODs
as defined in . A Composite Object Instance belongs to a single series.
A single series may contain multiple Composite Object Instances. Most
composite object IEs are modality dependent. To accommodate this
potential modality dependence, the set of Optional Keys at the Composite
Object Instance level includes all Attributes defined at the Composite
Object Instance level from any Composite IOD defined in .

.. _sect_C.3.2:

Study Root Query/Retrieve Information Model
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

The Study Root Query/Retrieve Information Model is identical to the
Patient Root Query/Retrieve Information Model except the top level is
the study level. Attributes of patients are considered to be Attributes
of studies.

.. _sect_C.3.3:

Patient/Study Only Query/Retrieve Information Model
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

Retired. See PS 3.4-2004.

.. _sect_C.3.4:

Additional Query/Retrieve Attributes
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

Some optional Attributes that may be used in Query/Retrieve Information
Models that are not Attributes of an Information Object Definition and,
therefore, are not defined in . These Attributes are defined in
`table_title <#table_C.3-1>`__.

.. table:: Additional Query/Retrieve Attributes

   +--------------------------+-------------+--------------------------+
   | Attribute Name           | Tag         | Attribute Description    |
   +==========================+=============+==========================+
   | Number of Patient        | (0020,1200) | The number of studies    |
   | Related Studies          |             | that match the Patient   |
   |                          |             | level Query/Retrieve     |
   |                          |             | search criteria          |
   +--------------------------+-------------+--------------------------+
   | Number of Patient        | (0020,1202) | The number of series     |
   | Related Series           |             | that match the Patient   |
   |                          |             | level Query/Retrieve     |
   |                          |             | search criteria          |
   +--------------------------+-------------+--------------------------+
   | Number of Patient        | (0020,1204) | The number of Composite  |
   | Related Instances        |             | Object Instances that    |
   |                          |             | match the Patient level  |
   |                          |             | Query/Retrieve search    |
   |                          |             | criteria                 |
   +--------------------------+-------------+--------------------------+
   | Number of Study Related  | (0020,1206) | The number of series     |
   | Series                   |             | that match the Study     |
   |                          |             | level Query/Retrieve     |
   |                          |             | search criteria          |
   +--------------------------+-------------+--------------------------+
   | Number of Series Related | (0020,1209) | The number of Composite  |
   | Instances                |             | Object Instances in a    |
   |                          |             | Series that match the    |
   |                          |             | Series level             |
   |                          |             | Query/Retrieve search    |
   |                          |             | criteria                 |
   +--------------------------+-------------+--------------------------+
   | Number of Study Related  | (0020,1208) | The number of Composite  |
   | Instances                |             | Object Instances that    |
   |                          |             | match the Study level    |
   |                          |             | Query/Retrieve search    |
   |                          |             | criteria                 |
   +--------------------------+-------------+--------------------------+
   | Modalities in Study      | (0008,0061) | All of the distinct      |
   |                          |             | values used for Modality |
   |                          |             | (0008,0060) in the       |
   |                          |             | Series of the Study.     |
   +--------------------------+-------------+--------------------------+
   | SOP Classes in Study     | (0008,0062) | The SOP Classes          |
   |                          |             | contained in the Study.  |
   +--------------------------+-------------+--------------------------+
   | Anatomic Regions in      | (0008,0063) | The anatomic regions of  |
   | Study Code Sequence      |             | interest in this Study   |
   |                          |             | (i.e., external anatomy, |
   |                          |             | surface anatomy, or      |
   |                          |             | general region of the    |
   |                          |             | body).                   |
   |                          |             |                          |
   |                          |             | One or more Items are    |
   |                          |             | permitted in this        |
   |                          |             | Sequence.                |
   |                          |             |                          |
   |                          |             | .. note::                |
   |                          |             |                          |
   |                          |             |    If the Instances in   |
   |                          |             |    the Study contain     |
   |                          |             |    Anatomic Region       |
   |                          |             |    Sequence (0008,2218), |
   |                          |             |    then the Items of     |
   |                          |             |    this Sequence may be  |
   |                          |             |    the union of the      |
   |                          |             |    codes in the          |
   |                          |             |    Instances.            |
   |                          |             |    Alternatively,        |
   |                          |             |    multiple (usually     |
   |                          |             |    contiguous) anatomic  |
   |                          |             |    regions might be      |
   |                          |             |    combined into a       |
   |                          |             |    single code. E.g.,    |
   |                          |             |    `(51185008, SCT,      |
   |                          |             |    "Chest") <http://snom |
   |                          |             | ed.info/id/51185008>`__, |
   |                          |             |    `(113345001, SCT,     |
   |                          |             |                          |
   |                          |             |  "Abdomen") <http://snom |
   |                          |             | ed.info/id/113345001>`__ |
   |                          |             |    and `(12921003, SCT,  |
   |                          |             |    "Pelvis") <http://sno |
   |                          |             | med.info/id/12921003>`__ |
   |                          |             |    might be combined     |
   |                          |             |    into `(416775004,     |
   |                          |             |    SCT, "Chest, Abdomen  |
   |                          |             |    and                   |
   |                          |             |                          |
   |                          |             |   Pelvis") <http://snome |
   |                          |             | d.info/id/416775004>`__. |
   |                          |             |                          |
   |                          |             |    If Instances in the   |
   |                          |             |    Study do not contain  |
   |                          |             |    Anatomic Region       |
   |                          |             |    Sequence (0008,2218)  |
   |                          |             |    but do contain Body   |
   |                          |             |    Part Examined         |
   |                          |             |    (0018,0015), then     |
   |                          |             |    codes equivalent to   |
   |                          |             |    recognized values of  |
   |                          |             |    Body Part Examined    |
   |                          |             |    (0018,0015) may be    |
   |                          |             |    used. See for         |
   |                          |             |    standard equivalent   |
   |                          |             |    values. E.g., if an   |
   |                          |             |    Instance contained    |
   |                          |             |    Body Part Examined    |
   |                          |             |    (0018,0015) with a    |
   |                          |             |    value of "CHEST",     |
   |                          |             |    then this Sequence    |
   |                          |             |    might contain         |
   |                          |             |    `(51185008, SCT,      |
   |                          |             |    "Chest") <http://snom |
   |                          |             | ed.info/id/51185008>`__. |
   +--------------------------+-------------+--------------------------+
   | Alternate Representation | (0008,3001) | A Sequence of Items,     |
   | Sequence                 |             | each identifying an      |
   |                          |             | alternate encoding of an |
   |                          |             | image that matches the   |
   |                          |             | Instance level           |
   |                          |             | Query/Retrieve search    |
   |                          |             | criteria (see `Alternate |
   |                          |             | Representation           |
   |                          |             | Sequence                 |
   |                          |             |  <#sect_C.6.1.1.5.1>`__) |
   +--------------------------+-------------+--------------------------+
   | Available Transfer       | (0008,3002) | Describes one or more    |
   | Syntax UID               |             | Transfer Syntaxes that   |
   |                          |             | the SCP can assure will  |
   |                          |             | be supported for         |
   |                          |             | retrieval of the SOP     |
   |                          |             | Instance (see `Available |
   |                          |             | SOP Transfer Syntax      |
   |                          |             | UID                      |
   |                          |             | <#sect_C.6.1.1.5.2>`__). |
   +--------------------------+-------------+--------------------------+

If the SCP manages images in multiple alternate encodings, only one of
the alternate encodings of an image is included in the number of object
instances.

.. _sect_C.3.5:

New Instance Creation for Enhanced Multi-Frame Image Conversion
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

When Query/Retrieve View (0008,0053) is present with a value of
"CLASSIC" or "ENHANCED" in a C-FIND, C-MOVE or C-GET Request Identifier,
then the Information Model against which the query or retrieval is
performed and any SOP Instances that are retrieved shall be returned,
constructed or converted according to the requirements in this section.

There are no requirements with respect to when such instances are
actually created or persisted, only that they be available on request.
I.e., they may be created in advance (cached) or they may be created
dynamically as required, as long as the process is deterministic in the
sense that the same Attributes will be populated with the same values on
successive queries and retrievals (including UIDs).

.. note::

   1. The UID generation process is required to be deterministic but it
      is important to remember that appending a suffix to an existing
      UID is not a valid approach to generating a new UID, unless the
      converter is the producer (owner of the root) of the original UID
      and knows that this is safe and the result will be unique.

   2. The cross-references between original and converted instances
      contain sufficient information to recover UIDs in the alternative
      form.

All instances for a Patient known to the SCP shall be converted as
necessary to maintain referential integrity and to avoid information
loss.

.. note::

   1. It is not permitted to fail to include a subset of instances
      within this scope, for example, the presentation states or key
      object selection documents, in the "ENHANCED" view, in order to
      avoid the effort of creating new instances with updated references
      required to maintain referential integrity. In other words, the
      total "information content" of any view will be no less than that
      of the default view.

   2. This does not mean that all instances need to be converted, since
      if they contain no such references, they can be left alone and
      included in the view. For example, a Classic single slice CT
      localizer image with no references can remain unchanged in the
      view as a CT Image Storage SOP Class with its existing SOP
      Instance UID and SOP Class and in its existing Series, and be
      referenced from converted instances, such as the axial images
      prescribed from it. An SCU cannot make any assumptions about what
      will or will not be converted, or in what order.

   3. It is understood that the requirements of this section are
      applicable to a single SCP; it is not possible to require all SCPs
      that perform conversion to perform it the same way, or create the
      same UIDs, etc.

In addition to the general requirements in this section, specific
requirements apply to the following types of instance created:

-  Enhanced (true or legacy converted) multi-frame images that are
   created from Classic single frame images

-  Classic single frame images that are created from Enhanced (true or
   legacy converted) multi-frame images

-  Instances that contain references to the SOP Instance UIDs or Series
   Instance UIDs corresponding to either the converted single frame
   images, or other instances with such references

The general requirements are that:

-  The new Composite Instance shall have a new SOP Instance UID.

-  The new Composite Instance shall be a valid SOP Instance (i.e., will
   comply with the IOD, Module and Attribute requirements for the
   Storage SOP Class).

-  The new Composite Instance shall contain the Contributing Equipment
   Sequence (0018,A001). If the source Composite Instances already
   contain the Contributing Equipment Sequence with a consistent set of
   Item values (excluding Contribution DateTime (0018,A002)), then a new
   Item shall be appended to the copy of the sequence in the new
   Composite Instance; if the source Composite Instance does not contain
   the Contributing Equipment Sequence or the Item values (excluding
   Contribution DateTime (0018,A002)) differ between source instances,
   then Contributing Equipment Sequence shall be created, containing one
   new Item. In either case, the new Item shall describe the equipment
   that is creating the new Composite Instance, and the Purpose of
   Reference Code Sequence (0040,A170) within the Item shall be (109106,
   DCM, "Enhanced Multi-frame Conversion Equipment") and the
   Contribution Description (0018,A003) shall be "Legacy Enhanced Image
   created from Classic Images", "Classic Image created from Enhanced
   Image", or "Updated UID references during Legacy Enhanced Classic
   conversion" as appropriate.

-  The new Composite Instance shall have the same Patient and Study
   level information as the source Instance, including the same Study
   Instance UID.

-  The new Composite Instance shall have the same spatial and temporal
   Frame of Reference information as the source instance, if present
   (e.g., the Frame of Reference UID shall be the same).

-  The new Composite Instance shall be placed in a new Series (together
   with other new Composite Instances that share the same, new Series
   level information), with a new Series Instance UID. The Series Date
   (0008,0021) and Series Time (0008,0031) of all the Instances in the
   new Series shall be the earliest of the values in the source
   Composite Instances, if present.

   .. note::

      1. The new Series Date and Time shall NOT be that of when the
         conversion was performed, but shall reflect the values in the
         source images.

      2. There is no standard requirement or mechanism defined to change
         or preserve other Series level Attributes, such as Series
         Number or Series Description. This is left to the discretion of
         the implementer, particularly in cases where instances from
         different Series are merged.

-  The new Composite Instance shall have the same Items and Values of
   Request Attributes Sequence (0040,0275) as the source Composite
   Instances, if Request Attributes Sequence (0040,0275) is present in
   any of the source Composite Instances.

-  If the new Composite Instance contains references to another entity
   for the same Patient (including, but not limited to, references to
   SOP Instances, Series, Studies or Frames of Reference), and the
   target of those references is also converted, then the references
   shall be changed to refer to the converted entity.

   .. note::

      1. For example, if the source instance refers to an instance in a
         Series, and the referenced instance is also converted, and
         hence placed in a new Series, then both the SOP Instance UID
         and the Series Reference UID in the hierarchical reference to
         the instance will need to be updated, as will the SOP Class UID
         of the referenced instance, if that has changed, as it likely
         will have.

      2. The overall intent is to maintain referential integrity within
         the converted set of instances, within the scope of the same
         Patient. Since it is likely that most if not all non-image
         instances for a patient will reference images that will be
         converted, this means that most if not all non-image instances
         will also have to be "converted", for the purpose of updating
         such references. This referential integrity is required
         regardless of whether the initial request is for a subset of
         instances for the patient only, or not.

      3. The UIDs referenced in Conversion Source Attributes Sequence
         (0020,9172) are not converted, since by definition, these
         reference instances in the "other" view; they should not exist
         in the source, but will be inserted (or be replaced, if
         previously converted) during conversion.

The specific requirements for the conversion of single frame images to
Enhanced Multi-frame images are:

-  The SOP Class of the new Composite Instance shall be the appropriate
   modality-specific Enhanced Image Storage SOP Class that is intended
   for de novo creation by an acquisition or post-processing device,
   unless the source images do not contain sufficient information to
   populate mandatory Attributes with standard Enumerated Values and
   Defined Terms or Coded Sequence Item values, in which case the
   appropriate modality-specific Legacy Converted Enhanced Image Storage
   SOP Class shall be used. The appropriate SOP Classes are defined in
   `table_title <#table_C.3.5-1>`__.

   .. note::

      1. For example, if the source images to be converted are of the CT
         Image Storage SOP Class, then the preferred new SOP Class is
         the Enhanced CT Image Storage SOP Class, but if this is not
         possible, the Legacy Converted Enhanced CT Image Storage SOP
         Class is used.

      2. It is not intended that images from different modalities be
         combined in the same new Composite Instance. For example, it is
         not expected that CT and PET images would be combined in the
         same Instance, since the technique Attributes and the pixel
         data characteristics are quite distinct.

      3. It is expected that as many single frame images will be
         combined into a single multi-frame image as is sensible, given
         the constrains on what Attributes must be identical as defined
         in this section, and depending on the type of images and the
         size of the resulting object. Different implementations may
         make different choices in this respect. For example, an
         application might choose to combine only images in the same
         Series, or with the same slice spacing, or the same values for
         Image Type, or with the same Image Orientation (Patient).

-  The new Composite Instance shall not be contained in a Concatenation.
   This means that it shall not contain a Concatenation UID (0020,9161)
   Attribute or other Concatenation Attributes. If the existing
   Composite Instance contains such Attributes, they shall not be
   included in the new Composite Instance.

-  The new Composite Instance contains only one set of Attributes for
   the Image Pixel Module, hence the contents of the Image Pixel Module
   shall either be identical in all source images, or the Pixel Data for
   each frame shall be converted as necessary to match the Image Pixel
   Module of the new Composite Instance.

   .. note::

      1. In particular this means that the values of Rows, Columns, Bits
         Stored, Bits Allocated, High Bit, Pixel Representation, Samples
         per Pixel, Photometric Interpretation and Planar Configuration
         applicable to all of the frames needs to be the same. In
         special cases, such as where Bits Stored is less than Bits
         Allocated but varies per frame, it may be safe to use the
         largest value for all the frames and ensure that any unused
         high bits are appropriately masked before encoding. It is not
         expected that source images with different numbers of Rows and
         Columns will be combined (by padding the periphery of images
         smaller than the largest); quite apart from not being the
         intended use case, this has the potential to greatly expand the
         size of the instance, and might also require adjustment of the
         Image Position (Patient) values.

      2. Special attention should be given to the Pixel Padding Value
         and associated Attributes, in case these vary per frame in the
         source images, in which case the Pixel Data for some frames may
         need to be modified to be consistent with all the other frames.

      3. It is possible to change the Image Pixel Module Attributes
         related to compressed Transfer Syntaxes (including lossy or
         irreversible compression) during conversion.

-  All mandatory Attributes of all mandatory Modules and Functional
   Group Macros of the SOP Class of the new Composite Instance shall be
   populated as required by the IOD. In this context, "mandatory" means
   either required or conditional where the condition is satisfied.

   .. note::

      For example, if the source images to be converted are of the CT
      Image Storage SOP Class, and the new Composite Instance is of the
      Legacy Converted Enhanced CT Image Storage SOP Class, then it is
      required that the Pixel Measures Functional Group be populated
      from Pixel Spacing, that the Plane Position (Patient) Functional
      Group be populated from Image Position (Patient), etc. In
      addition, if Body Part Examined is present in the source images
      with a standard value, then the condition for the inclusion of the
      Frame Anatomy Functional Group is satisfied, and the value therein
      needs to be converted to the appropriate Anatomic Region Sequence
      code.

-  All optional Attributes, Modules and Functional Group Macros for
   which corresponding information is present in the source images in
   Standard Attributes shall also be populated.

-  All Attributes of the Overlay Module shall be removed and converted
   into a Grayscale or Color Softcopy Presentation State (depending on
   the value of Photometric Interpretation); if the Overlay uses high
   bits in the Pixel Data (7FE0,0010) these shall be extracted and
   encoded in Overlay Data (60xx,3000) in the Presentation State and
   shall be set to zero in the Pixel Data (7FE0,0010) Attribute in the
   converted image.

   .. note::

      The extraction of Overlays from multiple frames may lead to a
      proliferation of GSPS Instances (one per converted frame), unless
      the converter recognizes commonality in the binary values of
      overlay bit planes and factors it out into fewer GSPS objects that
      each apply to multiple frames.

-  All Attributes of the Curve Module (retired, but formerly defined in
   DICOM) shall be removed; they may be converted into a Grayscale or
   Color Softcopy Presentation State (depending on the value of
   Photometric Interpretation) or a Waveform as appropriate, but this is
   not required.

-  All Attributes of the Graphic Annotation Sequence (0070,0001) (not
   defined in Classic image IODs, but sometimes used in a Standard
   Extended SOP Class) shall be removed; they may be converted into a
   Grayscale or Color Softcopy Presentation State (depending on the
   value of Photometric Interpretation), but this is not required.

-  All remaining Attributes in the source images (i.e., those that have
   not been used to populate mandatory or optional Attributes in Modules
   and Functional Groups), including Private Attributes, shall be copied
   into the top-level Data Set or the Unassigned Shared Converted
   Attributes Sequence (0020,9170) if they are present in all of the
   source images for the new Composite Instance, have the same number of
   values, and have the same values, otherwise they shall be copied into
   the Unassigned Per-Frame Converted Attributes Sequence (0020,9171).

   .. note::

      The semantics of Private Attributes, or Standard Attributes used
      in a Standard Extended SOP Class, might not be maintained, being
      unknown to the converting application; for example, referential
      integrity of UIDs in Private Attributes might not be updated.

-  The new Composite Instance shall contain references to the source
   Instances from which it was converted, encoded in the Conversion
   Source Reference Functional Group Macro.

The specific requirements for the conversion of Enhanced Multi-frame
images to Classic single frame images are:

-  The SOP Class of the new Composite Instance shall be the appropriate
   modality-specific (Classic) Image Storage SOP Class that is intended
   for de novo creation by an acquisition or post-processing device.

   .. note::

      For example, if the source images to be converted are of the
      Enhanced CT Image Storage SOP Class or the Legacy Converted
      Enhanced CT Image Storage SOP Class, then the new SOP Class is the
      CT Image Storage SOP Class.

-  All mandatory Attributes of the IOD of the SOP Class of the new
   Composite Instance shall be populated. In this context, "mandatory"
   means either required or conditional where the condition is
   satisfied.

   .. note::

      For example, if the source images to be converted are of the
      Legacy Converted Enhanced CT Image Storage SOP Class, and the new
      Composite Instance is of the CT Image Storage SOP Class, then it
      is required that Pixel Spacing be populated from the Pixel
      Measures Functional Group, that Image Position (Patient) be
      populated from the Plane Position (Patient) Functional Group, etc.

-  All optional Attributes in Modules of the IOD for which corresponding
   information is present in the source images shall also be populated.

-  All remaining Attributes in the source images (i.e., those that have
   not been used to populate mandatory or optional Attributes in
   Modules), including Private Attributes, shall be copied from the
   top-level Data Set and the Shared Functional Group Macro and the
   corresponding Item of the Per-Frame Functional Group Macro into the
   top-level Data Set of the new Composite Instance, including those in
   the Unassigned Shared Converted Attributes Sequence (0020,9170) and
   the corresponding Item of the Unassigned Per-Frame Converted
   Attributes Sequence (0020,9171) (which will result in a Standard
   Extended SOP Class).

   .. note::

      1. Identifying Attributes, such as Series Number or Series
         Description, will be present in the Unassigned functional
         groups, and UIDs will be present in the Conversion Source
         Attributes Sequence, allowing, for example, the original Series
         organization to be recovered, whether or not a single Series
         was previously converted into a single Legacy Converted
         instance or it was split or merged with other Series.

      2. The integrity of the set of Private Attributes recovered in
         this manner cannot be guaranteed to result in the correct
         function of any applications that depend on them, but the
         expectation is that this will be no better or worse than the
         impact of storing instances with private Attributes on any
         Storage SCP that may or may not reorganize and/or selectively
         preserve Private Attributes.

-  The new Composite Instance shall contain references to the source
   Instances from which it was converted, encoded in the Conversion
   Source Attributes Sequence (0020,9172) in the SOP Common Module.

The specific requirements for the conversion of other instances are:

-  The new Composite Instance shall be an instance of the same SOP Class
   as the source Composite Instance.

-  The new Composite Instance shall contain references to the source
   Instances from which it was converted, encoded in the Conversion
   Source Attributes Sequence (0020,9172) in the SOP Common Module.

.. table:: Modality-Specific SOP Class Conversions

   +-------------------+-----------------------+-----------------------+
   | Classic           | True Enhanced         | Legacy Converted      |
   |                   |                       | Enhanced              |
   +===================+=======================+=======================+
   | CT Image Storage  | Enhanced CT Image     | Legacy Converted      |
   |                   | Storage               | Enhanced CT Image     |
   |                   |                       | Storage               |
   +-------------------+-----------------------+-----------------------+
   | MR Image Storage  | Enhanced MR Image     | Legacy Converted      |
   |                   | Storage               | Enhanced MR Image     |
   |                   |                       | Storage               |
   +-------------------+-----------------------+-----------------------+
   | PET Image Storage | Enhanced PET Image    | Legacy Converted      |
   |                   | Storage               | Enhanced PET Image    |
   |                   |                       | Storage               |
   +-------------------+-----------------------+-----------------------+

.. _sect_C.4:

DIMSE-C Service Groups
----------------------

Three DIMSE-C Services are used in the construction of SOP Classes of
the Query/Retrieve Service Class. The following DIMSE-C operations are
used:

-  C-FIND

-  C-MOVE

-  C-GET

.. _sect_C.4.1:

C-FIND Operation
~~~~~~~~~~~~~~~~

SCPs of some SOP Classes of the Query/Retrieve Service Class may be
capable of processing queries using the C-FIND operation as described in
. The C-FIND operation is the mechanism by which queries are performed.
Matches against the keys present in the Identifier are returned in
C-FIND responses.

.. _sect_C.4.1.1:

C-FIND Service Parameters
^^^^^^^^^^^^^^^^^^^^^^^^^

.. _sect_C.4.1.1.1:

SOP Class UID
'''''''''''''

The SOP Class UID identifies the Query/Retrieve Information Model
against which the C-FIND is to be performed. Support for the SOP Class
UID is implied by the Abstract Syntax UID of the Presentation Context
used by this C-FIND operation.

.. _sect_C.4.1.1.2:

Priority
''''''''

The Priority Attribute defines the requested priority of the C-FIND
operation with respect to other DIMSE operations being performed by the
same SCP.

Processing of priority requests is not required of SCPs. Whether or not
an SCP supports priority processing and the meaning of the different
priority levels shall be stated in the Conformance Statement of the SCP.

.. _sect_C.4.1.1.3:

Identifier
''''''''''

Both the C-FIND request and response contain an Identifier encoded as a
Data Set (see ).

.. note::

   The definition of a Data Set in specifically excludes the range of
   groups below group 0008, and this includes in particular Meta
   Information Header elements such as Transfer Syntax UID (0002,0010).
   The C-FIND request and identifier do not support a mechanism for
   ascertaining the manner in which an SCP might have encoded a stored
   image whether it be by requesting Transfer Syntax UID (0002,0010) or
   by any other mechanism.

.. _sect_C.4.1.1.3.1:

Request Identifier Structure
                            

An Identifier in a C-FIND request shall contain:

-  Key Attributes values to be matched against the values of storage SOP
   Instances managed by the SCP.

-  Query/Retrieve Level (0008,0052), which defines the level of the
   query.

-  Conditionally, the Attribute Query/Retrieve View (0008,0053). This
   Attribute may be included if Enhanced Multi-Frame Image Conversion
   has been accepted during Association Extended Negotiation. It shall
   not be included otherwise.

-  Conditionally, the Attribute Specific Character Set (0008,0005). This
   Attribute shall be included if expanded or replacement character sets
   may be used in any of the Attributes in the Request Identifier. It
   shall not be included otherwise.

-  Conditionally, the Attribute Timezone Offset From UTC (0008,0201).
   This Attribute shall be included if Key Attributes of time are to be
   interpreted explicitly in the designated local time zone. It shall
   not be present otherwise, i.e., it shall not be sent with a
   zero-length value.

The Key Attributes and values allowable for the level of the query shall
be defined in the SOP Class definition for the Query/Retrieve
Information Model.

.. _sect_C.4.1.1.3.2:

Response Identifier Structure
                             

The C-FIND response shall not contain Attributes that were not in the
request or specified in this section.

An Identifier in a C-FIND response shall contain:

-  Key Attributes with values corresponding to Key Attributes contained
   in the Identifier of the request.

   .. note::

      1. All Required Keys in the Request Identifier, as well as all
         Optional Keys in the Request Identifier that are supported by
         the SCP, will therefore be present in the Response Identifier.

      2. Required Keys and supported Optional Keys in the Response
         Identifier will have zero length if the SCP has no value to
         send; i.e., there is no requirement that the SCP have a value
         for these, or create a dummy value.

      3. The requirement that unsupported Optional Keys present in the
         Request Identifier not be included in the Response Identifier
         is specified in `Optional Keys <#sect_C.2.2.1.3>`__.

      4. Private Attributes present in the Request Identifier may be
         ignored by the SCP if unrecognized (as defined for a ), hence
         may or may not be present in the Response Identifier.

-  Query/Retrieve Level (0008,0052), which defines the level of the
   query. The Query/Retrieve level shall be equal to the level specified
   in the request.

-  Conditionally, the Attribute Specific Character Set (0008,0005). This
   Attribute shall be included if expanded or replacement character sets
   may be used in any of the Attributes in the Response Identifier. It
   shall not be included otherwise. The C-FIND SCP is not required to
   return responses in the Specific Character Set requested by the SCU
   if that character set is not supported by the SCP. The SCP may return
   responses with a different Specific Character Set.

-  Conditionally, the Attribute Timezone Offset From UTC (0008,0201).
   This Attribute shall be included if any Attributes of time in the
   Response Identifier are to be interpreted explicitly in the
   designated local time zone. It shall not be present otherwise, i.e.,
   it shall not be sent with a zero-length value.

The C-FIND SCP is required to support either or both the Retrieve AE
Title Data Element or the Storage Media File-Set ID/Storage Media File
Set UID Data Elements. An Identifier in a C-FIND response shall contain:

-  Storage Media File-Set ID (0088,0130), which defines a user or
   implementation specific human readable Identifier that identifies the
   Storage Media on which the Composite Object Instance(s); reside. This
   element pertains to the set of Composite Object Instances available
   at the Query/Retrieve Level specified in the Identifier of the C-FIND
   request (e.g., Patient, Study, Series, Composite Object Instance).
   This Attribute shall be present if the Retrieve AE Title Data Element
   is not present. A null value (Data Element length of 0) is valid for
   all levels except the lowest level in the Information Model as
   defined by the SOP Class.

-  Storage Media File-Set UID (0088,0140), which uniquely identifies the
   Storage Media on which the Composite Object Instance(s) reside. This
   element pertains to the set of Composite Object Instances available
   at the Query/Retrieve Level specified in the Identifier of the C-FIND
   request (e.g., Patient, Study, Series, Composite Object Instance).
   This Attribute shall be present if the Retrieve AE Title Data Element
   is not present. A null value (Data Element length of 0) is valid for
   all levels except the lowest level in the Information Model as
   defined by the SOP Class.

   .. note::

      The File-Set concepts are used in .

-  Retrieve AE Title (0008,0054), which defines a list of DICOM
   Application Entity Title(s) that identify the location from which the
   Composite Object Instance(s) may be retrieved on the network. This
   element pertains to the set of Composite Object Instances available
   at the Query/Retrieve Level specified in the Identifier of the C-FIND
   request (e.g., Patient, Study, Series, Composite Object Instance).
   This Attribute shall be present if the Storage Media File-Set ID and
   Storage Media File-Set UID elements are not present. The Application
   Entity named in this field shall support either the C-GET or C-MOVE
   SOP Class of the Query/Retrieve Service Class. A null value (Data
   Element length of 0) is valid for all levels except the lowest level
   in the Information Model as defined by the SOP Class.

   .. note::

      1. For example, a DICOM AE with the AE Title of "A" performs a
         C-FIND request to a DICOM AE with the AE Title of "B" with the
         Query/Retrieve level set to "STUDY". DICOM AE "B" determines
         that the Composite Object Instances for each matching study may
         be retrieved by itself and sets the Data Element Retrieve AE
         Title to "B".

      2. File-Sets may not be defined at every Query/Retrieve Level. If
         the SCP supports the File-Set ID/File-Set UID option but does
         not define these Attributes at the Query/Retrieve Level
         specified in the C-FIND request it may return these Data
         Elements with a length of 0 to signify that the value is
         unknown. An SCU should reissue a C-FIND at a Query/Retrieve
         Level lower in the hierarchy.

      3. The fact that the value of the Key Attribute is unknown to the
         SCP of the Query/Retrieve Service Class does not imply that it
         is not present in the underlying Information Object. Thus, a
         subsequent retrieval may cause a Storage of a SOP Instance that
         contains the value of the Attribute.

The C-FIND SCP may also, but is not required to, support the Instance
Availability (0008,0056) Data Element. This Data Element shall not be
included in a C-FIND request. An Identifier in a C-FIND response may
contain:

-  Instance Availability (0008,0056), which defines how rapidly
   Composite Object Instance(s); become available for transmission after
   a C-MOVE or C-GET retrieval request. This element pertains to the set
   of Composite Object Instances available at the Query/Retrieve Level
   specified in the Identifier of the C-FIND request (e.g., Patient,
   Study, Series, Composite Object Instance). When some composite
   instances are less rapidly available than others, the availability of
   the least rapidly available shall be returned. If this Data Element
   is not returned, the availability is unknown or unspecified. A null
   value (Data Element length of 0) is not permitted. The Enumerated
   Values for this Data Element are:

   -  "ONLINE", which means the instances are immediately available,

   -  "NEARLINE", which means the instances need to be retrieved from
      relatively slow media such as optical disk or tape, or require
      conversion that takes time,

   -  "OFFLINE", which means the instances need to be retrieved by
      manual intervention,

   -  "UNAVAILABLE", which means the instances cannot be retrieved. Note
      that SOP Instances that are unavailable may have an alternate
      representation that is available (see section `Alternate
      Representation Sequence <#sect_C.6.1.1.5.1>`__).

.. _sect_C.4.1.1.4:

Status
''''''

`table_title <#table_C.4-1>`__ defines the specific status code values
that might be returned in a C-FIND response. General status code values
and fields related to status code values are defined for C-FIND DIMSE
Service in .

.. table:: C-FIND Response Status Values

   +----------------+----------------+--------------+----------------+
   | Service Status | Further        | Status Codes | Related Fields |
   |                | Meaning        |              |                |
   +================+================+==============+================+
   | Failure        | Refused: Out   | A700         | (0000,0902)    |
   |                | of resources   |              |                |
   +----------------+----------------+--------------+----------------+
   | Error: Data    | A900           | (0000,0901)  |                |
   | Set does not   |                |              |                |
   | match SOP      |                | (0000,0902)  |                |
   | Class          |                |              |                |
   +----------------+----------------+--------------+----------------+
   | Failed: Unable | Cxxx           | (0000,0901)  |                |
   | to process     |                |              |                |
   |                |                | (0000,0902)  |                |
   +----------------+----------------+--------------+----------------+
   | Cancel         | Matching       | FE00         | None           |
   |                | terminated due |              |                |
   |                | to Cancel      |              |                |
   |                | request        |              |                |
   +----------------+----------------+--------------+----------------+
   | Success        | Matching is    | 0000         | None           |
   |                | complete - No  |              |                |
   |                | final          |              |                |
   |                | Identifier is  |              |                |
   |                | supplied.      |              |                |
   +----------------+----------------+--------------+----------------+
   | Pending        | Matches are    | FF00         | Identifier     |
   |                | continuing -   |              |                |
   |                | Current Match  |              |                |
   |                | is supplied    |              |                |
   |                | and any        |              |                |
   |                | Optional Keys  |              |                |
   |                | were supported |              |                |
   |                | in the same    |              |                |
   |                | manner as      |              |                |
   |                | Required Keys. |              |                |
   +----------------+----------------+--------------+----------------+
   | Matches are    | FF01           | Identifier   |                |
   | continuing -   |                |              |                |
   | Warning that   |                |              |                |
   | one or more    |                |              |                |
   | Optional Keys  |                |              |                |
   | were not       |                |              |                |
   | supported for  |                |              |                |
   | existence      |                |              |                |
   | and/or         |                |              |                |
   | matching for   |                |              |                |
   | this           |                |              |                |
   | Identifier.    |                |              |                |
   +----------------+----------------+--------------+----------------+

Some Failure Status Codes are implementation specific.

An SCP implementation shall assign specific failure status codes by
replacing each 'x' symbol with a hexadecimal digit in the range from 0
to F. An SCP implementation wishing to differentiate between causes of
“Failed: Unable to process” Failure Meaning shall assign those causes
specific Status Code Values within valid range specified in
`table_title <#table_C.4-1>`__.

An SCU implementation shall recognize any Failure Status Code within the
value range specified in `table_title <#table_C.4-1>`__ as an indicator
of the Failure Meaning stated in the table. There is no requirement for
an SCU implementation to differentiate between specific Status Codes
within the valid range.

.. _sect_C.4.1.2:

C-FIND SCU Behavior
^^^^^^^^^^^^^^^^^^^

This Section discusses both the baseline and extended behavior of the
C-FIND SCU.

.. _sect_C.4.1.2.1:

Baseline Behavior of SCU
''''''''''''''''''''''''

All C-FIND SCUs shall be capable of generating query requests that meet
the requirements of the Hierarchical Search.

The Identifier contained in a C-FIND request shall contain a single
value in the Unique Key Attribute for each level above the
Query/Retrieve level. No Required or Optional Keys shall be specified
that are associated with levels above the Query/Retrieve level.

The Unique Key Attribute associated with the Query/Retrieve level shall
be contained in the C-FIND request and may specify Single Value
Matching, Universal Value Matching, or List of UID Matching. In
addition, Required and Optional Keys associated with the Query/Retrieve
level may be contained in the Identifier.

An SCU conveys the following semantics using the C-FIND request:

-  The SCU requests that the SCP perform a match of all keys specified
   in the Identifier of the request against the information it possesses
   down to the Query/Retrieve level specified in the request.

   .. note::

      1. The SCU may not assume the SCP supports any Optional Keys.
         Hence, Optional Keys serve only to reduce network related
         overhead when they are supported by the SCP.

      2. The SCU must be prepared to filter C-FIND responses when the
         SCP fails to support an Optional Key specified in the C-FIND
         request.

-  The SCU shall interpret Pending responses to convey the Attributes of
   a match of an Entity at the level of the query.

-  The SCU shall interpret a response with a status equal to Success,
   Failed or Refused to convey the end of Pending responses.

-  The SCU shall interpret a Refused or Failed response to a C-FIND
   request as an indication that the SCP is unable to process the
   request.

-  The SCU may cancel the C-FIND service by issuing a C-FIND-CANCEL
   request at any time during the processing of the C-FIND. The SCU
   shall recognize a status of Canceled to indicate that the
   C-FIND-CANCEL was successful.

.. _sect_C.4.1.2.2:

Extended Behavior of SCU
''''''''''''''''''''''''

Extended SCU behavior shall be negotiated at Association establishment
time. If an option within the extended behavior is not agreed upon in
the negotiation, then only baseline SCU behavior shall be performed with
respect to that option. Extended SCU behavior includes all baseline
behavior with the following option:

-  Relational-queries

-  Enhanced Multi-Frame Image Conversion

More than one option may be agreed upon.

.. _sect_C.4.1.2.2.1:

Relational-Queries
                  

The C-FIND Service with relational-queries allows any combination of
keys at any level in the hierarchy. The Unique Key Attribute associated
with the Query/Retrieve level shall be contained in the C-FIND request
and may specify Single Value Matching, Universal Value Matching, or List
of UID Matching. Support for relational-queries removes the baseline
restriction that a Unique Key shall be specified for all levels above
the Query/Retrieve level in the C-FIND request.

.. _sect_C.4.1.2.2.2:

Enhanced Multi-Frame Image Conversion
                                     

The C-FIND Service with Enhanced Multi-Frame Image Conversion allows for
selection of the default or an alternative view of the instances
represented by the Information Model.

Support for Enhanced Multi-Frame Image Conversion allows the SCU to
specify the Query/Retrieve View (0008,0053) in the Request Identifier
with a value of either "CLASSIC" or "ENHANCED".

If Query/Retrieve View (0008,0053) is not present in the Request
Identifier, then the SCU requests that the SCP perform a match of all
keys specified in the Identifier of the request against the information
about the instances that it possesses, as received.

If Query/Retrieve View (0008,0053) is present with a value of "CLASSIC",
then the SCU requests that the SCP perform a match of all keys specified
in the Identifier of the request against the information about Classic
single frame Instances (converted from Enhanced multi-frame Instances if
required), as well as any instances that were converted to preserve
referential integrity, and any that did not need to be converted.

If Query/Retrieve View (0008,0053) is present with a value of
"ENHANCED", then the SCU requests that the SCP perform a match of all
keys specified in the Identifier of the request against the information
about Enhanced multi-frame Instances (converted from Classic single
frame Instances if required), as well as any instances that were
converted to preserve referential integrity, and any that did not need
to be converted.

.. note::

   1. The SCU may assume that no duplicate information will be returned.
      For example, if an entire series of single frame instances can be
      converted to a separate series of converted instances, a STUDY
      level C-FIND will not return both series.

   2. The Query Information Model is unchanged, and the same unique,
      required and optional keys are equally applicable to both views,
      except that the values for the SERIES and IMAGE level queries will
      be different and will depend on the converted instance content.

   3. Unconverted instances, such as for other modalities like
      Ultrasound, will appear identical regardless of view.

   4. Implementations may apply performance optimizations, such as
      pre-computing or caching the potential information against which
      CLASSIC and ENHANCED queries may be performed, in order to
      minimize significant delays between the query request and response
      caused by converting "on demand", but SCUs may need to consider
      the potential for a delayed response when configuring timeouts,
      etc.

.. _sect_C.4.1.3:

C-FIND SCP Behavior
^^^^^^^^^^^^^^^^^^^

This Section discusses both the baseline and extended behavior of the
C-FIND SCP.

.. _sect_C.4.1.3.1:

Baseline Behavior of SCP
''''''''''''''''''''''''

All C-FIND SCPs shall be capable of processing queries that meet the
requirements of the Hierarchical Search.

An SCP conveys the following semantics with a C-FIND response:

-  The SCP is requested to perform a match of all the keys specified in
   the Identifier of the request, against the information it possesses,
   to the level specified in the request. Attribute matching is
   performed using the key values specified in the Identifier of the
   C-FIND request as defined in `Query/Retrieve Information Model
   Definition <#sect_C.2>`__.

-  The SCP generates a C-FIND response for each match using the
   Hierarchical Search method. All such responses shall contain an
   Identifier whose Attributes contain values from a single match. All
   such responses shall contain a status of Pending.

-  When all matches have been sent, the SCP generates a C-FIND response
   that contains a status of Success. A status of Success shall indicate
   that a response has been sent for each match known to the SCP.

   .. note::

      When there are no matches, then no responses with a status of
      Pending are sent, only a single response with a status of Success.

-  The SCP shall generate a response with a status of Refused or Failed
   if it is unable to process the request. A Refused or Failed response
   shall contain no Identifier.

-  If the SCP receives C-FIND-CANCEL indication before it has completed
   the processing of the matches it shall interrupt the matching process
   and return a status of Canceled.

-  If the SCP manages images in multiple alternate encodings (see
   `Alternate Representation Sequence <#sect_C.6.1.1.5.1>`__), only one
   of the alternate encodings of an image shall be included in the set
   of matches for a C-FIND request at the Instance level.

   .. note::

      For query of images with alternate encodings, the SCP may select
      the appropriately encoded Instance for the request response based
      on identity of the SCU or other factors.

.. _sect_C.4.1.3.1.1:

Hierarchical Search Method
                          

Starting at the top level in the Query/Retrieve Information Model,
continuing until the level specified in the C-FIND request is reached,
the following procedures are used to generate matches:

a. If the current level is the level specified in the C-FIND request,
   then the key match strings contained in the Identifier of the C-FIND
   request are matched against the values of the Key Attributes for each
   entity at the current level. For each entity for which the Attributes
   match all of the specified match strings, construct an Identifier.
   This Identifier shall contain all of the Unique Keys at higher levels
   and all of the values of the Attributes for this entity that match
   those in the C-FIND request. Return a response for each such
   Identifier. If there are no matching keys, then there are no matches,
   return a response with a status equal to Success and with no
   Identifier.

b. Otherwise, if the current level is not the level specified in the
   C-FIND request and there is an entity matching the Unique Key
   Attribute Value for this level specified in the C-FIND request,
   perform this procedure at the next level down in the hierarchy.

c. Otherwise there are no matches; return a response with a status equal
   to Success.

   .. note::

      The above description specifies a recursive procedure. It may
      recur upon itself multiple times as it goes down the hierarchical
      levels, but at each level it recurs only once.

.. _sect_C.4.1.3.2:

Extended Behavior of SCP
''''''''''''''''''''''''

Extended SCP behavior shall be negotiated at Association establishment
time. If an option within the extended behavior is not agreed upon in
the negotiation, then only baseline SCP behavior shall be performed with
respect to that option. Extended SCP behavior includes all baseline
behavior with the following option:

-  Relational-queries

-  Enhanced Multi-Frame Image Conversion

More than one option may be agreed upon.

.. _sect_C.4.1.3.2.1:

Relational-Queries
                  

The C-FIND Service with relational-queries allows any combination of
keys at any level in the hierarchy. At the lowest level, a query using
the relational-queries shall contain the Unique Key for that level with
either a Single Value Match, a Wild Card Match, or a Universal Match.
Support for relational-queries removes the baseline restriction that a
Unique Key shall be specified for all levels above the Query/Retrieve
level in the C-FIND request.

The C-FIND SCP shall perform matching based on all keys specified in the
C-FIND request regardless of the Query/Retrieve level.

.. _sect_C.4.1.3.2.2:

Relational Search Method
                        

A query using the relational method may contain any combination of keys
at any level in the hierarchy. Starting at the top level in the
Query/Retrieve Information Model, continuing until the Query/Retrieve
level specified in the C-FIND request is reached, the following
procedures are used to generate matches:

a. The key match strings contained in the Identifier of the C-FIND
   request are matched against the values of the Key Attributes for each
   entity at the current level.

b. If no Key Attribute is specified at the current level and the current
   level is not the level specified in the C-FIND request, the match
   shall be performed as if a wild card were specified for the Unique
   Key Attribute for the current level (i.e., all entities at the
   current level shall match).

c. If the current level is the level specified in the C-FIND request,
   then for each matching entity (a matching entity is one for which the
   Attributes match all of the specified match strings in the Key
   Attributes), construct an Identifier. This Identifier shall contain
   all of the Attributes generated by this procedure at higher levels on
   this recursion path and all of the values of the Key Attributes for
   this entity that match those in the C-FIND request.

d. Otherwise, if the current level is not the level specified in the
   C-FIND request, then for each matching entity construct a list of
   Attributes containing all of the matching Key Attributes and all
   Attributes that were prepared at the previous level for this entity.
   Then perform this procedure at the next level down in the hierarchy
   for each matching entity.

e. Otherwise, if there are no matches, return a response with status
   equal to Success and no Identifier.

.. note::

   1. The above description specifies a recursive procedure. It may
      recur upon itself multiple times as it goes down the hierarchical
      levels, and at each level, it may recur multiple times (one for
      each matching entity). This may result in a large number of
      Identifiers being generated.

   2. It is not required that the above defined procedure be used to
      generate matches. It is expected that implementations will
      incorporate different algorithms for performing searches of the
      databases. For a given query, the set of matches shall be
      equivalent to that which would be generated by the above
      procedure.

.. _sect_C.4.1.3.2.3:

Enhanced Multi-Frame Image Conversion
                                     

If Query/Retrieve View (0008,0053) is not present in the Request
Identifier, then the SCP shall perform a match of all keys specified in
the Identifier of the request against the information about the
instances that it possesses, as received.

If Query/Retrieve View (0008,0053) is present with a value of "CLASSIC",
then the SCP shall perform a match of all keys specified in the
Identifier of the request against the information about Classic single
frame Instances (converted from Enhanced multi-frame Instances if
required), as well as any instances that were converted to preserve
referential integrity, and any that did not need to be converted.

If Query/Retrieve View (0008,0053) is present with a value of
"ENHANCED", then the SCP shall perform a match of all keys specified in
the Identifier of the request against the information about Enhanced
multi-frame Instances (converted from Classic single frame Instances if
required), as well as any instances that were converted to preserve
referential integrity, and any that did not need to be converted.

.. note::

   1. The SCP will not return information that is duplicated. For
      example, if an entire series of single frame instances can be
      converted to a separate series of converted instances, a STUDY
      level C-FIND will not return both series.

   2. The Query Information Model is unchanged, and the same unique,
      required and optional keys are equally applicable to both views,
      except that the values for the SERIES and IMAGE level queries will
      be different and will depend on the converted instance content.

   3. Unconverted instances, such as for other modalities like
      Ultrasound, will appear identical regardless of view.

.. _sect_C.4.2:

C-MOVE Operation
~~~~~~~~~~~~~~~~

SCUs of some SOP Classes of the Query/Retrieve Service Class may
generate retrievals using the C-MOVE operation as described in . The
C-MOVE operation allows an application entity to instruct another
application entity to transfer stored SOP Instances to another
application entity using the C-STORE operation. Support for the C-MOVE
service shall be agreed upon at Association establishment time by both
the SCU and SCP of the C-MOVE in order for a C-MOVE operation to occur
over the Association. The C-STORE sub-operations shall always be
accomplished over an Association different from the Association that
accomplishes the C-MOVE operation. Hence, the SCP of the Query/Retrieve
Service Class serves as the SCU of the Storage Service Class.

.. note::

   The application entity that receives the stored SOP Instances may or
   may not be the originator of the C-MOVE operation.

A C-MOVE request may be performed to any level of the Query/Retrieve
Information Model. However, the transfer of stored SOP Instances may not
be performed at this level. The level at which the transfer is performed
depends upon the SOP Class (see `SOP Class Definitions <#sect_C.6>`__).

.. _sect_C.4.2.1:

C-MOVE Service Parameters
^^^^^^^^^^^^^^^^^^^^^^^^^

.. _sect_C.4.2.1.1:

SOP Class UID
'''''''''''''

The SOP Class UID identifies the Query/Retrieve Information Model
against which the C-MOVE is to be performed. Support for the SOP Class
UID is implied by the Abstract Syntax UID of the Presentation Context
used by this C-MOVE operation.

.. _sect_C.4.2.1.2:

Priority
''''''''

The Priority Attribute defines the requested priority of the C-MOVE
operation and corresponding C-STORE sub-operations with respect to other
DIMSE operations being performed by the same SCP.

Processing of priority requests is not required of SCPs. Whether or not
an SCP supports priority processing, and the meaning of the different
priority levels shall be stated in the Conformance Statement of the SCP.
The same priority shall be used for all C-STORE sub-operations.

.. _sect_C.4.2.1.3:

Move Destination
''''''''''''''''

Move Destination specifies the Application Entity Title of the receiver
of the C-STORE sub-operations.

.. _sect_C.4.2.1.4:

Identifier
''''''''''

The C-MOVE request shall contain an Identifier. The C-MOVE response
shall conditionally contain an Identifier as required in `Response
Identifier Structure <#sect_C.4.2.1.4.2>`__.

.. note::

   The Identifier is specified as U in the definition of the C-MOVE
   primitive in but is specialized for use with this service.

.. _sect_C.4.2.1.4.1:

Request Identifier Structure
                            

An Identifier in a C-MOVE request shall contain:

-  Query/Retrieve Level (0008,0052), which defines the level of the
   retrieval

-  Unique Key Attributes, which may include Patient ID (0010,0020),
   Study Instance UIDs (0020,000D), Series Instance UIDs (0020,000E),
   and the SOP Instance UIDs (0008,0018)

-  Conditionally, the Attribute Query/Retrieve View (0008,0053). This
   Attribute may be included if Enhanced Multi-Frame Image Conversion
   has been accepted during Association Extended Negotiation. It shall
   not be included otherwise.

Specific Character Set (0008,0005) shall be present if Patient ID
(0010,0020) is using a character set other than the Default Character
Repertoire.

The Unique Keys at each level of the hierarchy and the values allowable
for the level of the retrieval shall be defined in the SOP Class
definition for the Query/Retrieve Information Model.

.. note::

   1. In the non-Relational behavior, more than one entity may be
      retrieved if the Query/Retrieve Level is IMAGE, SERIES or STUDY,
      using List of UID matching, but only Single Value Matching value
      may be specified for Patient ID (0010,0020).

   2. The issuer of the Patient ID (0010,0020) is implicit; there is no
      provision to send the Issuer of Patient ID (0010,0021). When there
      is a possibility of ambiguity of the Patient ID (0010,0020) value,
      a STUDY level retrieval should be used instead of a PATIENT level
      retrieval.

.. _sect_C.4.2.1.4.2:

Response Identifier Structure
                             

The Failed SOP Instance UID List (0008,0058) specifies a list of UIDs of
the C-STORE sub-operation SOP Instances for which this C-MOVE operation
has failed. An Identifier in a C-MOVE response shall conditionally
contain the Failed SOP Instance UID List (0008,0058) based on the C-MOVE
response status value. If no C-STORE sub-operation failed, Failed SOP
Instance UID List (0008,0058) is absent and therefore no Data Set shall
be sent in the C-MOVE response.

Specific Character Set (0008,0005) shall not be present.

The Identifier in a C-MOVE response with a status of:

-  Canceled, Failure, Refused, or Warning shall contain the Failed SOP
   Instance UID List Attribute

-  Pending shall not contain the Failed SOP Instance UID List Attribute
   (no Data Set)

.. _sect_C.4.2.1.5:

Status
''''''

`table_title <#table_C.4-2>`__ defines the specific status code values
that might be returned in a C-MOVE response. General status code values
and fields related to status code values are defined for C-MOVE DIMSE
Service in .

.. table:: C-MOVE Response Status Values

   +----------------+----------------+--------------+----------------+
   | Service Status | Further        | Status Codes | Related Fields |
   |                | Meaning        |              |                |
   +================+================+==============+================+
   | Failure        | Refused: Out   | A701         | (0000,0902)    |
   |                | of resources - |              |                |
   |                | Unable to      |              |                |
   |                | calculate      |              |                |
   |                | number of      |              |                |
   |                | matches        |              |                |
   +----------------+----------------+--------------+----------------+
   | Refused: Out   | A702           | (0000,1021)  |                |
   | of resources - |                |              |                |
   | Unable to      |                | (0000,1022)  |                |
   | perform        |                |              |                |
   | sub-operations |                | (0000,1023)  |                |
   +----------------+----------------+--------------+----------------+
   | Refused: Move  | A801           | (0000,0902)  |                |
   | Destination    |                |              |                |
   | unknown        |                |              |                |
   +----------------+----------------+--------------+----------------+
   | Error: Data    | A900           | (0000,0901)  |                |
   | Set does not   |                |              |                |
   | match SOP      |                | (0000,0902)  |                |
   | Class          |                |              |                |
   +----------------+----------------+--------------+----------------+
   | Failed: Unable | Cxxx           | (0000,0901)  |                |
   | to Process     |                |              |                |
   |                |                | (0000,0902)  |                |
   +----------------+----------------+--------------+----------------+
   | Cancel         | Sub-operations | FE00         | (0000,1020)    |
   |                | terminated due |              |                |
   |                | to Cancel      |              | (0000,1021)    |
   |                | Indication     |              |                |
   |                |                |              | (0000,1022)    |
   |                |                |              |                |
   |                |                |              | (0000,1023)    |
   +----------------+----------------+--------------+----------------+
   | Warning        | Sub-operations | B000         | (0000,1021)    |
   |                | Complete - One |              |                |
   |                | or more        |              | (0000,1022)    |
   |                | Failures       |              |                |
   |                |                |              | (0000,1023)    |
   +----------------+----------------+--------------+----------------+
   | Success        | Sub-operations | 0000         | (0000,1021)    |
   |                | Complete - No  |              |                |
   |                | Failures       |              | (0000,1022)    |
   |                |                |              |                |
   |                |                |              | (0000,1023)    |
   +----------------+----------------+--------------+----------------+
   | Pending        | Sub-operations | FF00         | (0000,1020)    |
   |                | are continuing |              |                |
   |                |                |              | (0000,1021)    |
   |                |                |              |                |
   |                |                |              | (0000,1022)    |
   |                |                |              |                |
   |                |                |              | (0000,1023)    |
   +----------------+----------------+--------------+----------------+

Some Failure Status Codes are implementation specific.

An SCP implementation shall assign specific failure status codes by
replacing each 'x' symbol with a hexadecimal digit in the range from 0
to F. An SCP implementation wishing to differentiate between causes of
"Failed: Unable to process" Failure Meaning shall assign those causes
specific Status Code Values within valid range specified in
`table_title <#table_C.4-2>`__.

An SCU implementation shall recognize any Failure Status Code within the
value range specified in `table_title <#table_C.4-2>`__ as an indicator
of the Failure Meaning stated in the table. There is no requirement for
an SCU implementation to differentiate between specific Status Codes
within the valid range.

.. _sect_C.4.2.1.6:

Number of Remaining Sub-Operations
''''''''''''''''''''''''''''''''''

Inclusion of the Number of Remaining Sub-operations is conditional based
upon the status in the C-MOVE response. The Number of Remaining
Sub-operations specifies the number of Remaining C-STORE sub-operations
necessary to complete the C-MOVE operation.

A C-MOVE response with a status of:

-  Pending shall contain the Number of Remaining Sub-operations
   Attribute

-  Canceled may contain the Number of Remaining Sub-operations Attribute

-  Warning, Failure, or Success shall not contain the Number of
   Remaining Sub-operations Attribute

.. _sect_C.4.2.1.7:

Number of Completed Sub-Operations
''''''''''''''''''''''''''''''''''

Inclusion of the Number of Completed Sub-operations is conditional based
upon the status in the C-MOVE response. The Number of Completed
sub-operations specifies the number of C-STORE sub-operations generated
by the requested transfer that have completed successfully.

A C-MOVE response with a status of:

-  Pending shall contain the Number of Completed Sub-operations
   Attribute

-  Canceled, Warning, Failure, or Success may contain the Number of
   Completed Sub-operations Attribute

.. _sect_C.4.2.1.8:

Number of Failed Sub-Operations
'''''''''''''''''''''''''''''''

Inclusion of the Number of Failed Sub-operations is conditional based
upon the status in the C-MOVE response. The Number of Failed
sub-operations specifies the number of C-STORE sub-operations generated
by the requested transfer that have Failed.

A C-MOVE response with a status of:

-  Pending shall contain the Number of Failed Sub-operations Attribute

-  Canceled, Warning, Failure, or Success may contain the Number of
   Failed Sub-operations Attribute

.. _sect_C.4.2.1.9:

Number of Warning Sub-Operations
''''''''''''''''''''''''''''''''

Inclusion of the Number of Warning Sub-operations is conditional based
upon the status in the C-MOVE response. The Number of Warning
sub-operations specifies the number of C-STORE sub-operations generated
by the requested transfer that had a status of warning.

A C-MOVE response with a status of:

-  Pending shall contain the Number of Warnings Sub-operations Attribute

-  Canceled, Warning, Failure, or Success may contain the Number of
   Warning Sub-operations Attribute

.. _sect_C.4.2.2:

C-MOVE SCU Behavior
^^^^^^^^^^^^^^^^^^^

This Section discusses both the baseline and extended behavior of the
C-MOVE SCU.

.. _sect_C.4.2.2.1:

Baseline Behavior of SCU
''''''''''''''''''''''''

An SCU conveys the following semantics with a C-MOVE request:

-  The SCU shall supply a single value in the Unique Key Attribute for
   each level above the Query/Retrieve level. For the level of retrieve,
   the SCU shall supply a single value for one unique key if the level
   of retrieve is above the STUDY level and shall supply one UID, or a
   list of UIDs if a retrieval of several items is desired and the
   retrieve level is STUDY, SERIES or IMAGE. The SCU shall also supply a
   move destination. The move destination shall be the DICOM Application
   Entity Title of a DICOM Application Entity capable of serving as the
   SCP of the Storage Service Class.

-  The SCU shall interpret responses to the C-MOVE with status equal to
   Pending during the processing of the C-STORE sub-operations. These
   responses shall indicate the number of Remaining, Completed, Failed,
   and Warning C-STORE sub-operations.

-  The SCU shall interpret responses with a status equal to Success,
   Warning, Failure, or Refused as final responses. The final response
   shall indicate the number of Successful C-STORE sub-operations and
   the number of Failed C-STORE sub-operations resulting from the C-MOVE
   operation. The SCU shall interpret a status of:

   -  Success to indicate that all sub-operations were successfully
      completed

   -  Warning to indicate one or more sub-operations were successfully
      completed and one or more sub-operations were unsuccessful or had
      a status of warning, or all sub-operations had a status of warning

   -  Failure or Refused to indicate all sub-operations were
      unsuccessful.

-  The SCU may cancel the C-MOVE service by issuing a C-MOVE-CANCEL
   request at any time during the processing of the C-MOVE. The SCU
   shall interpret a C-MOVE response with a status of Canceled to
   indicate the transfer was canceled. The C-MOVE response with a status
   of Canceled shall contain the number of Completed, Failed, and
   Warning C-STORE sub-operations. If present, the Remaining
   sub-operations count shall contain the number of C-STORE
   sub-operations that were not initiated due to the C-MOVE-CANCEL
   request.

.. _sect_C.4.2.2.2:

Extended Behavior of SCU
''''''''''''''''''''''''

Extended SCU behavior shall be negotiated at Association establishment
time. If an option within the extended behavior is not agreed upon in
the negotiation, then only baseline SCU behavior shall be performed with
respect to that option. Extended SCU behavior includes all baseline
behavior with the following option:

-  Relational-retrieve

-  Enhanced Multi-Frame Image Conversion

More than one option may be agreed upon.

.. _sect_C.4.2.2.2.1:

Relational-Retrieve
                   

The C-MOVE Service with relational-retrieve removes the restriction that
the SCU supply Unique Key values for levels above the Query/Retrieve
level to identify an entity at the level of the retrieval. Hence, the
Identifier of a C-MOVE request may transfer:

-  all Composite Object Instances related to a study by only providing a
   Study Instance UID (0020,000D)

-  all Composite Object Instances related to a series by only providing
   a Series Instance UID (0020,000E)

-  individual Composite Object Instances by only providing a list of SOP
   Instance UIDs (0008,0018)

.. _sect_C.4.2.2.2.2:

Enhanced Multi-Frame Image Conversion
                                     

The C-MOVE Service with Enhanced Multi-Frame Image Conversion allows for
selection of the default or an alternative view of the instances
represented by the Information Model, and hence the retrieval of either
the legacy or the converted images, together with any unconverted
instances, all of which are required to be processed to maintain
referential integrity within the scope of the Patient.

Support for Enhanced Multi-Frame Image Conversion allows the SCU to
specify the Attribute Query/Retrieve View (0008,0053) in the Request
Identifier with a value of either "CLASSIC" or "ENHANCED".

If Query/Retrieve View (0008,0053) is not present in the Request
Identifier, then the SCU requests that the SCP provide all the requested
instances it possesses, as received.

If Query/Retrieve View (0008,0053) is present with a value of "CLASSIC",
then the SCU requests that the SCP provide all the Classic single frame
Instances (converted from Enhanced multi-frame Instances if required),
as well as any instances that were converted to preserve referential
integrity, and any that did not need to be converted.

If Query/Retrieve View (0008,0053) is present with a value of
"ENHANCED", then the SCU requests that the SCP provide all the Enhanced
multi-frame Instances (converted from Classic single frame Instances if
required), as well as any instances that were converted to preserve
referential integrity, and any that did not need to be converted.

.. note::

   1. The SCU may assume that no duplicate information will be provided.
      For example, if an entire series of single frame instances can be
      converted to a separate series of converted instances, a STUDY
      level C-MOVE will not provide both series.

   2. The Query Information Model is unchanged, and the same unique keys
      are equally applicable to both views, except that the values for
      the SERIES and IMAGE level queries will be different and will
      depend on the converted instance content.

   3. The Query/Retrieve View is still required in an IMAGE or SERIES
      level request identifier, even though the requested unique key(s)
      are unambiguous, and the view is in a sense "redundant", because
      the conversion that created the requested instances may not have
      been executed yet. It is not permitted to specify a view that is
      inconsistent with the requested unique key(s).

.. _sect_C.4.2.3:

C-MOVE SCP Behavior
^^^^^^^^^^^^^^^^^^^

This section discusses both the baseline and extended behavior of the
C-MOVE SCP.

.. _sect_C.4.2.3.1:

Baseline Behavior of SCP
''''''''''''''''''''''''

An SCP conveys the following semantics with a C-MOVE response:

-  The SCP shall identify a set of Entities at the level of the transfer
   based upon the values in the Unique Keys in the Identifier of the
   C-MOVE request. The SCP shall initiate C-STORE sub-operations for the
   corresponding storage SOP Instances. These C-STORE sub-operations
   shall occur on a different Association (that may already exist) from
   the C-MOVE operation. The SCP of the Query/Retrieve Service Class
   shall serve as an SCU of the Storage Service Class.

-  The SCP shall either reuse an established and compatible Association
   or establish a new Association for the C-STORE sub-operations. The
   SCP shall initiate C-STORE sub-operations over that Association for
   all stored SOP Instances related to the Patient ID, List of Study
   Instance UIDs, List of Series Instance UIDs, or List of SOP Instance
   UIDs depending on the Query/Retrieve level specified in the C-MOVE
   request. A sub-operation is considered Failed if the SCP is unable to
   negotiate an appropriate presentation context for a given stored SOP
   Instance.

-  Optionally, the SCP may generate responses to the C-MOVE with status
   equal to Pending during the processing of the C-STORE sub-operations.
   These responses shall indicate the Remaining, Completed, Failed, and
   Warning C-STORE sub-operations.

-  When the number of Remaining sub-operations reaches zero, the SCP
   shall generate a final response with a status equal to Success,
   Warning, Failure, or Refused. This response shall indicate the number
   of Completed sub-operations, the number of Failed sub-operations, and
   the number of sub-operations with Warning Status. The status
   contained in the C-MOVE response shall contain:

   -  Success if all sub-operations were successfully completed

   -  Warning if one or more sub-operations were successfully completed
      and one or more sub-operations were unsuccessful or had a warning
      status

   -  Warning if all sub-operations had a warning status

   -  Failure or Refused if all sub-operations were unsuccessful

-  The SCP may receive a C-MOVE-CANCEL request at any time during the
   processing of the C-MOVE. The SCP shall interrupt all C-STORE
   sub-operation processing and return a status of Canceled in the
   C-MOVE response. The C-MOVE response with a status of Canceled shall
   contain the number of Completed, Failed, and Warning C-STORE
   sub-operations. If present, the Remaining sub-operations count shall
   contain the number of C-STORE sub-operations that were not initiated
   due to the C-MOVE-CANCEL request.

-  If the SCP manages images in multiple alternate encodings (see
   `Alternate Representation Sequence <#sect_C.6.1.1.5.1>`__), only one
   of the alternate encodings of an image shall be included in the set
   of object instances retrieved by a C-MOVE request at the Patient,
   Study, or Series level.

   .. note::

      For retrieval of images with alternate encodings using a C-MOVE
      request at the Patient, Study, or Series level, the SCP may select
      the appropriately encoded Instance for the retrieval based on
      identity of the SCU, transfer syntaxes accepted in the C-STORE
      Association Negotiation, or other factors.

.. note::

   If the association on which the C-MOVE operation was issued is
   abnormally terminated, then it will not be possible to issue any
   further pending responses nor a final response, nor will
   C-MOVE-CANCEL requests be received. The behavior of the C-MOVE SCP
   acting as a C-STORE SCU is undefined in this condition. Specifically,
   whether or not any uncompleted C-STORE sub-operations continue is
   undefined.

.. _sect_C.4.2.3.2:

Extended Behavior of SCP
''''''''''''''''''''''''

Extended SCP behavior shall be negotiated at Association establishment
time. If an option within the extended behavior is not agreed upon in
the negotiation, then only baseline SCP behavior shall be performed with
respect to that option. Extended SCP behavior includes all baseline
behavior with the following option:

-  Relational-retrieve

-  Enhanced Multi-Frame Image Conversion

More than one option may be agreed upon.

.. _sect_C.4.2.3.2.1:

Relational-Retrieve
                   

The C-MOVE Service with relational-retrieve removes the restriction that
the SCU supply Unique Key values for levels above the Query/Retrieve
level to help identify an entity at the level of the retrieval. Hence,
the Identifier of a C-MOVE request may specify the transfer of:

-  all Composite Object Instances related to a study by only providing a
   Study Instance UID (0020,000D)

-  all Composite Object Instances related to a series by only providing
   a Series Instance UID (0020,000E)

-  individual Composite Object Instances by only providing a list of SOP
   Instance UIDs (0008,0018)

.. _sect_C.4.2.3.2.2:

Enhanced Multi-Frame Image Conversion
                                     

If Query/Retrieve View (0008,0053) is not present in the Request
Identifier, then the SCP shall identify a set of Entities at the level
of the transfer based upon the values in the Unique Keys in the
Identifier of the C-MOVE request that correspond to the instances it
possesses, as received, and shall initiate C-STORE sub-operations for
all the corresponding storage SOP Instances.

If Query/Retrieve View (0008,0053) is present with a value of "CLASSIC",
then the SCP shall identify a set of Entities at the level of the
transfer based upon the values in the Unique Keys in the Identifier of
the C-MOVE request that correspond to the Classic single frame Instances
(converted from Enhanced multi-frame Instances if required), as well as
any instances that were converted to preserve referential integrity, and
any that did not need to be converted, and shall initiate C-STORE
sub-operations for all the corresponding storage SOP Instances.

If Query/Retrieve View (0008,0053) is present with a value of
"ENHANCED", then the SCP shall identify a set of Entities at the level
of the transfer based upon the values in the Unique Keys in the
Identifier of the C-MOVE request that correspond to the Enhanced
multi-frame Instances (converted from Classic single frame Instances if
required), as well as any instances that were converted to preserve
referential integrity, and any that did not need to be converted, and
shall initiate C-STORE sub-operations for all the corresponding storage
SOP Instances.

.. note::

   1. The SCP will not send information that is duplicated to the
      C-STORE SCP. For example, if an entire series of single frame
      instances can be converted to a separate series of converted
      instances, a STUDY level C-MOVE will not send both series.

   2. The C-STORE SCP will need to support the necessary SOP Classes for
      converted instances, otherwise the C-STORE sub-operations will
      fail in the normal manner and this will be reflected in the C-MOVE
      responses.

   3. The Query Information Model is unchanged, and the same unique,
      required and optional keys are equally applicable to both views,
      except that the values for the SERIES and IMAGE level queries will
      be different and will depend on the converted instance content.

   4. The Query/Retrieve View is still required in an IMAGE or SERIES
      level request identifier, even though the requested unique key(s)
      are unambiguous.

.. _sect_C.4.3:

C-GET Operation
~~~~~~~~~~~~~~~

SCUs of some SOP Classes of the Query/Retrieve Service Class may
generate retrievals using the C-GET operation as described in . The
C-GET operation allows an application entity to instruct another
application entity to transfer stored SOP Instances to the initiating
application entity using the C-STORE operation. Support for the C-GET
service shall be agreed upon at Association establishment time by both
the SCU and SCP of the C-GET in order for a C-GET operation to occur
over the Association. The C-STORE Sub-operations shall be accomplished
on the same Association as the C-GET operation. Hence, the SCP of the
Query/Retrieve Service Class serves as the SCU of the Storage Service
Class.

.. note::

   The application entity that receives the stored SOP Instances is
   always the originator of the C-GET operation.

A C-GET request may be performed to any level of the Query/Retrieve
Information Model. However, the transfer of stored SOP Instances may not
be performed at this level. The level at which the transfer is performed
depends upon the SOP Class.

.. _sect_C.4.3.1:

C-GET Service Parameters
^^^^^^^^^^^^^^^^^^^^^^^^

.. _sect_C.4.3.1.1:

SOP Class UID
'''''''''''''

The SOP Class UID identifies the Query/Retrieve Information Model
against which the C-GET is to be performed. Support for the SOP Class
UID is implied by the Abstract Syntax UID of the Presentation Context
used by this C-GET operation.

.. _sect_C.4.3.1.2:

Priority
''''''''

The Priority Attribute defines the requested priority of the C-GET
operation and corresponding C-STORE sub-operations with respect to other
DIMSE operations being performed by the same SCP.

Processing of priority requests is not required of SCPs. Whether or not
an SCP supports priority processing, and the meaning of the different
priority levels shall be stated in the Conformance Statement of the SCP.
The same priority shall be used for all C-STORE sub-operations.

.. _sect_C.4.3.1.3:

Identifier
''''''''''

The C-GET request shall contain an Identifier. The C-GET response shall
conditionally contain an Identifier as required in `Response Identifier
Structure <#sect_C.4.3.1.3.2>`__.

.. note::

   The Identifier is specified as U in the definition of the C-GET
   primitive in but is specialized for use with this service.

.. _sect_C.4.3.1.3.1:

Request Identifier Structure
                            

An Identifier in a C-GET request shall contain:

-  Query/Retrieve Level (0008,0052), which defines the level of the
   retrieval

-  Unique Key Attributes, which may include Patient ID (0010,0020),
   Study Instance UIDs (0020,000D) Series Instance UIDs (0020,000E), and
   SOP Instance UIDs (0008,0018)

-  Conditionally, the Attribute Query/Retrieve View (0008,0053). This
   Attribute may be included if Enhanced Multi-Frame Image Conversion
   has been accepted during Association Extended Negotiation. It shall
   not be included otherwise.

Specific Character Set (0008,0005) shall be present if Patient ID
(0010,0020) is using a character set other than the Default Character
Repertoire.

The Unique Keys at each level of the hierarchy and the values allowable
for the level of the retrieval shall be defined in the SOP Class
definition for the Query/Retrieve Information Model.

.. note::

   1. In the non-Relational behavior, more than one entity may be
      retrieved if the Query/Retrieve Level is IMAGE, SERIES or STUDY,
      using List of UID matching, but only Single Value Matching value
      may be specified for Patient ID (0010,0020).

   2. The issuer of the Patient ID (0010,0020) is implicit; there is no
      provision to send the Issuer of Patient ID (0010,0021). When there
      is a possibility of ambiguity of the Patient ID (0010,0020) value,
      a STUDY level retrieval should be used instead of a PATIENT level
      retrieval.

.. _sect_C.4.3.1.3.2:

Response Identifier Structure
                             

The Failed SOP Instance UID List (0008,0058) specifies a list of UIDs of
the C-STORE sub-operation SOP Instances for which this C-GET operation
has failed. An Identifier in a C-GET response shall conditionally
contain the Failed SOP Instance UID List (0008,0058) based on the C-GET
response. If no C-STORE sub-operation failed, Failed SOP Instance UID
List (0008,0058) is absent and therefore no Data Set shall be sent in
the C-GET response.

Specific Character Set (0008,0005) shall not be present.

The Identifier in a C-GET response with a status of:

-  Canceled, Failure, Refused, or Warning shall contain the Failed SOP
   Instance UID List Attribute

-  Pending shall not contain the Failed SOP Instance UID List Attribute
   (no Data Set)

.. _sect_C.4.3.1.4:

Status
''''''

`table_title <#table_C.4-3>`__ defines the specific status code values
that might be returned in a C-GET response. General status code values
and fields related to status code values are defined for C-GET DIMSE
Service in .

.. table:: C-GET Response Status Values

   +----------------+----------------+--------------+----------------+
   | Service Status | Further        | Status Codes | Related Fields |
   |                | Meaning        |              |                |
   +================+================+==============+================+
   | Failure        | Refused: Out   | A701         | (0000,0902)    |
   |                | of resources - |              |                |
   |                | Unable to      |              |                |
   |                | calculate      |              |                |
   |                | number of      |              |                |
   |                | matches        |              |                |
   +----------------+----------------+--------------+----------------+
   | Refused: Out   | A702           | (0000,1021)  |                |
   | of resources - |                |              |                |
   | Unable to      |                | (0000,1022)  |                |
   | perform        |                |              |                |
   | sub-operations |                | (0000,1023)  |                |
   +----------------+----------------+--------------+----------------+
   | Error: Data    | A900           | (0000,0901)  |                |
   | Set does not   |                |              |                |
   | match SOP      |                | (0000,0902)  |                |
   | Class          |                |              |                |
   +----------------+----------------+--------------+----------------+
   | Failed: Unable | Cxxx           | (0000,0901)  |                |
   | to process     |                |              |                |
   |                |                | (0000,0902)  |                |
   +----------------+----------------+--------------+----------------+
   | Cancel         | Sub-operations | FE00         | (0000,1020)    |
   |                | terminated due |              |                |
   |                | to Cancel      |              | (0000,1021)    |
   |                | Indication     |              |                |
   |                |                |              | (0000,1022)    |
   |                |                |              |                |
   |                |                |              | (0000,1023)    |
   +----------------+----------------+--------------+----------------+
   | Warning        | Sub-operations | B000         | (0000,1021)    |
   |                | Complete - One |              |                |
   |                | or more        |              | (0000,1022)    |
   |                | Failures or    |              |                |
   |                | Warnings       |              | (0000,1023)    |
   +----------------+----------------+--------------+----------------+
   | Success        | Sub-operations | 0000         | (0000,1021)    |
   |                | Complete - No  |              |                |
   |                | Failures or    |              | (0000,1022)    |
   |                | Warnings       |              |                |
   |                |                |              | (0000,1023)    |
   +----------------+----------------+--------------+----------------+
   | Pending        | Sub-operations | FF00         | (0000,1020)    |
   |                | are continuing |              |                |
   |                |                |              | (0000,1021)    |
   |                |                |              |                |
   |                |                |              | (0000,1022)    |
   |                |                |              |                |
   |                |                |              | (0000,1023)    |
   +----------------+----------------+--------------+----------------+

Some Failure Status Codes are implementation specific.

An SCP implementation shall assign specific failure status codes by
replacing each 'x' symbol with a hexadecimal digit in the range from 0
to F. An SCP implementation wishing to differentiate between causes of
“Failed: Unable to process” Failure Meaning shall assign those causes
specific Status Code Values within valid range specified in
`table_title <#table_C.4-3>`__.

An SCU implementation shall recognize any Failure Status Code within the
value range specified in `table_title <#table_C.4-3>`__ as an indicator
of the Failure Meaning stated in the table. There is no requirement for
an SCU implementation to differentiate between specific Status Codes
within the valid range.

.. _sect_C.4.3.1.5:

Number of Remaining Sub-Operations
''''''''''''''''''''''''''''''''''

Inclusion of the Number of Remaining Sub-operations is conditional based
upon the status in the C-GET response. The Number of Remaining
Sub-operations specifies the number of Remaining C-STORE sub-operations
necessary to complete the C-GET operation.

A C-GET response with a status of:

-  Pending shall contain the Number of Remaining Sub-operations
   Attribute

-  Canceled may contain the Number of Remaining Sub-operations Attribute

-  Warning, Failure, or Success shall not contain the Number of
   Remaining Sub-operations Attribute.

.. _sect_C.4.3.1.6:

Number of Completed Sub-Operations
''''''''''''''''''''''''''''''''''

Inclusion of the Number of Completed Sub-operations is conditional based
upon the status in the C-GET response. The Number of Completed
Sub-operations specifies the number of C-STORE sub-operations generated
by the requested transfer that have completed successfully.

A C-GET response with a status of:

-  Pending shall contain the Number of Completed Sub-operations
   Attribute

-  Canceled, Warning, Failure, or Success may contain the Number of
   Completed Sub-operations Attribute

.. _sect_C.4.3.1.7:

Number of Failed Sub-Operations
'''''''''''''''''''''''''''''''

Inclusion of the Number of Failed Sub-operations is conditional based
upon the status in the C-GET response. The Number of Failed
Sub-operations specifies the number of C-STORE sub-operations generated
by the requested transfer that have Failed.

A C-GET response with a status of:

-  Pending shall contain the Number of Failed Sub-operations Attribute

-  Canceled, Warning, Failure, or Success may contain the Number of
   Failed Sub-operations Attribute

.. _sect_C.4.3.1.8:

Number of Warning Sub-Operations
''''''''''''''''''''''''''''''''

Inclusion of the Number of Warning Sub-operations is conditional based
upon the status in the C-GET response. The Number of Warning
Sub-operations specifies the number of C-STORE sub-operations generated
by the requested transfer that had a status of Warning.

A C-GET response with a status of:

-  Pending shall contain the Number of Warning Sub-operations Attribute

-  Canceled, Warning, Failure, or Success may contain the Number of
   Warning Sub-operations Attribute

.. _sect_C.4.3.2:

C-GET SCU Behavior
^^^^^^^^^^^^^^^^^^

This Section discusses both the baseline and extended behavior of the
C-GET SCU.

.. _sect_C.4.3.2.1:

Baseline Behavior of SCU
''''''''''''''''''''''''

An SCU conveys the following semantics with a C-GET request:

-  The SCU shall have proposed sufficient presentation contexts at
   Association establishment time to accommodate expected C-STORE
   sub-operations that shall occur over the same Association. The SCU of
   the Query/Retrieve Service Class shall serve as the SCP of the
   Storage Service Class.

-  The SCU shall supply a single value in the Unique Key Attribute for
   each level above the Query/Retrieve level. For the level of retrieve,
   the SCU shall supply a single value for one unique key if the level
   of the retrieve is above the STUDY level and shall supply one UID, or
   a list of UIDs if a retrieval of several items is desired and the
   retrieve level is STUDY, SERIES or IMAGE.

-  The SCU shall interpret C-GET responses with status equal to Pending
   during the processing of the C-STORE sub-operations. These responses
   shall indicate the number of Remaining, Completed, Failed, Warning
   C-STORE sub-operations.

-  The SCU shall interpret a C-GET response with a status equal to
   Success, Warning, Failure, or Refused as a final response. The final
   response shall indicate the number of Completed sub-operations and
   the number of Failed C-STORE sub-operations resulting from the C-GET
   operation. The SCU shall interpret a status of:

   -  Success to indicate that all sub-operations were successfully
      completed

   -  Warning to indicate one or more sub-operations were successfully
      completed and one or more unsuccessful or all sub-operations had a
      status of warning

   -  Failure or Refused to indicate all sub-operations were
      unsuccessful

-  The SCU may cancel the C-GET operation by issuing a C-GET-CANCEL
   request at any time during the processing of the C-GET request. A
   C-GET response with a status of Canceled shall indicate to the SCU
   that the retrieve was canceled. Optionally, the C-GET response with a
   status of Canceled shall indicate the number of Completed, Failed,
   and Warning C-STORE sub-operations. If present, the Remaining
   sub-operations count shall contain the number of C-STORE
   sub-operations that were not initiated due to the C-GET-CANCEL
   request.

.. _sect_C.4.3.2.2:

Extended Behavior of SCU
''''''''''''''''''''''''

Extended SCU behavior shall be negotiated at Association establishment
time. If an option within the extended behavior is not agreed upon in
the negotiation, then only baseline SCU behavior shall be supported with
respect to that option. Extended SCU behavior includes all baseline
behavior with the following option:

-  Relational-retrieve

-  Enhanced Multi-Frame Image Conversion

More than one option may be agreed upon.

.. _sect_C.4.3.2.2.1:

Relational-Retrieve
                   

The C-GET Service with relational-retrieve removes the restriction that
the SCU supply Unique Key values for levels above the Query/Retrieve
level to help identify an entity at the level of the retrieval. Hence,
the Identifier of a C-GET request may retrieve:

-  all Composite Object Instances related to a study by providing a
   Study Instance UID (0020,000D)

-  all Composite Object Instances related to a series by providing a
   Series Instance UID (0020,000E)

-  individual Composite Object Instances by providing a list of SOP
   Instance UIDs (0008,0018)

.. _sect_C.4.3.2.2.2:

Enhanced Multi-Frame Image Conversion
                                     

The C-GET Service with Enhanced Multi-Frame Image Conversion allows for
selection of the default or an alternative view of the instances
represented by the Information Model, and hence the retrieval of either
the legacy or the converted images, together with any unconverted
instances, all of which are required to be processed to maintain
referential integrity within the scope of the Patient.

Support for Enhanced Multi-Frame Image Conversion allows the SCU to
specify the Attribute Query/Retrieve View (0008,0053) in the Request
Identifier with a value of either "CLASSIC" or "ENHANCED".

If Query/Retrieve View (0008,0053) is not present in the Request
Identifier, then the SCU requests that the SCP retrieve all the
requested instances it possesses, as received.

If Query/Retrieve View (0008,0053) is present with a value of "CLASSIC",
then the SCU requests that the SCP retrieve all the Classic single frame
Instances (converted from Enhanced multi-frame Instances if required),
as well as any instances that were converted to preserve referential
integrity, and any that did not need to be converted.

If Query/Retrieve View (0008,0053) is present with a value of
"ENHANCED", then the SCU requests that the SCP retrieve all the Enhanced
multi-frame Instances (converted from Classic single frame Instances if
required), as well as any instances that were converted to preserve
referential integrity, and any that did not need to be converted.

.. note::

   1. The C-GET SCU acting as a C-STORE SCP may assume that no duplicate
      information will be provided. For example, if an entire series of
      single frame instances can be converted to a separate series of
      converted instances, a STUDY level C-GET will not return both
      series.

   2. The C-GET SCU acting as a C-STORE SCP will need to support the
      necessary SOP Classes for converted instances, otherwise the
      C-STORE sub-operations will fail in the normal manner and this
      will be reflected in the C-GET responses.

   3. The Query Information Model is unchanged, and the same unique,
      required and optional keys are equally applicable to both views,
      except that the values for the SERIES and IMAGE level queries will
      be different and will depend on the converted instance content.

   4. The Query/Retrieve View is still required in an IMAGE or SERIES
      level request identifier, even though the requested unique key (s)
      are unambiguous, and the view is in a sense "redundant", because
      the conversion that created the requested instances may not have
      been executed yet. It is not permitted to specify a view that is
      inconsistent with the requested unique key(s).

.. _sect_C.4.3.3:

C-GET SCP Behavior
^^^^^^^^^^^^^^^^^^

This Section discusses both the baseline and extended behavior of the
C-GET SCP.

.. _sect_C.4.3.3.1:

Baseline Behavior of SCP
''''''''''''''''''''''''

An SCP conveys the following semantics with a C-GET response:

-  The SCP shall identify a set of Entities at the level of the
   retrieval based upon the values in the Unique Keys in the Identifier
   of the C-GET request. The SCP shall initiate C-STORE sub-operations
   for the corresponding storage SOP Instances. The SCP of the
   Query/Retrieve Service Class shall serve as an SCU of the Storage
   Service Class.

-  The SCP shall initiate C-STORE sub-operations over the same
   Association for all stored SOP Instances related to the Patient ID,
   List of Study Instance UIDs, List of Series Instance UIDs, or List of
   SOP Instance UIDs depending on the Query/Retrieve level specified in
   the C-GET request

-  A sub-operation is considered Failed if the SCP is unable to initiate
   a C-STORE sub-operation because the Query/Retrieve SCU did not offer
   an appropriate presentation context for a given stored SOP Instance.

-  Optionally, the SCP may generate responses to the C-GET with status
   equal to Pending during the processing of the C-STORE sub-operations.
   These responses shall indicate the number of Remaining, Completed,
   Failure, and Warning C-STORE sub-operations.

-  When the number of Remaining sub-operations reaches zero, the SCP
   shall generate a final response with a status equal to Success,
   Warning, Failed, or Refused. The status contained in the C-GET
   response shall contain:

   -  Success if all sub-operations were successfully completed

   -  Warning if one or more sub-operations were successfully completed
      and one or more sub-operations were unsuccessful or had a status
      of warning

   -  Warning if all sub-operations had a status of Warning

   -  Failure or Refused if all sub-operations were unsuccessful

-  The SCP may receive a C-GET-CANCEL request at any time during the
   processing of the C-GET request. The SCP shall interrupt all C-STORE
   sub-operation processing and return a status of Canceled in the C-GET
   response. The C-GET response with a status of Canceled shall contain
   the number of Completed, Failed, and Warning C-STORE sub-operations.
   If present, the Remaining sub-operations count shall contain the
   number of C-STORE sub-operations that were not initiated due to the
   C-GET-CANCEL request.

-  If the SCP manages images in multiple alternate encodings (see
   `Alternate Representation Sequence <#sect_C.6.1.1.5.1>`__), only one
   of the alternate encodings of an image shall be included in the set
   of object instances retrieved by a C-GET request at the Patient,
   Study, or Series level.

   .. note::

      For retrieval of images with alternate encodings using a C-GET
      request at the Patient, Study, or Series level, the SCP may select
      the appropriately encoded Instance for the retrieval based on
      identity of the SCU, transfer syntaxes accepted in the C-STORE
      Association Negotiation, or other factors.

.. _sect_C.4.3.3.2:

Extended Behavior of SCP
''''''''''''''''''''''''

Extended SCP behavior shall be negotiated at Association establishment
time. If an option within the extended behavior is not agreed upon in
the negotiation, then only baseline SCP behavior shall be performed with
respect to that option. Extended SCP behavior includes all baseline
behavior with the following option:

-  Relational-retrieve

-  Enhanced Multi-Frame Image Conversion

More than one option may be agreed upon.

.. _sect_C.4.3.3.2.1:

Relational-Retrieve
                   

The C-GET Service with relational-retrieve removes the restriction that
the SCU supply Unique Key values for levels above the Query/Retrieve
level to help identify an entity at the level of the retrieval. Hence,
the Identifier of a C-GET request may retrieve:

-  all Composite Object Instances related to a study by providing a
   Study Instance UID

-  all Composite Object Instances related to a series by providing a
   Series Instance UID

-  individual Composite Object Instances by providing a list of SOP
   Instance UIDs

.. _sect_C.4.3.3.2.2:

Enhanced Multi-Frame Image Conversion
                                     

If Query/Retrieve View (0008,0053) is not present in the Request
Identifier, then the SCP shall identify a set of Entities at the level
of the transfer based upon the values in the Unique Keys in the
Identifier of the C-GET request that correspond to the instances it
possesses, as received, and shall initiate C-STORE sub-operations for
all the corresponding storage SOP Instances.

If Query/Retrieve View (0008,0053) is present with a value of "CLASSIC",
then the SCP shall identify a set of Entities at the level of the
transfer based upon the values in the Unique Keys in the Identifier of
the C-GET request that correspond to the Classic single frame Instances
(converted from Enhanced multi-frame Instances if required), as well as
any instances that were converted to preserve referential integrity, and
any that did not need to be converted, and shall initiate C-STORE
sub-operations for all the corresponding storage SOP Instances.

If Query/Retrieve View (0008,0053) is present with a value of
"ENHANCED", then the SCP shall identify a set of Entities at the level
of the transfer based upon the values in the Unique Keys in the
Identifier of the C-GET request that correspond to the Enhanced
multi-frame Instances (converted from Classic single frame Instances if
required), as well as any instances that were converted to preserve
referential integrity, and any that did not need to be converted, and
shall initiate C-STORE sub-operations for all the corresponding storage
SOP Instances.

.. note::

   1. The C-GET SCP acting as a C-STORE SCU will not send information
      that is duplicated to the C-GET SCU acting as a C-STORE SCP. For
      example, if an entire series of single frame instances can be
      converted to a separate series of converted instances, a STUDY
      level C-GET will not send both series.

   2. The Query Information Model is unchanged, and the same unique,
      required and optional keys are equally applicable to both views,
      except that the values for the SERIES and IMAGE level queries will
      be different and will depend on the converted instance content.

   3. The Query/Retrieve View is still required in an IMAGE or SERIES
      level request identifier, even though the requested unique key(s)
      are unambiguous.

.. _sect_C.5:

Association Negotiation
-----------------------

Association establishment is the first phase of any instance of
communication between peer DICOM AEs. AEs supporting DICOM
Query/Retrieve SOP Classes utilize Association establishment negotiation
by defining the use of Application Association Information. See for an
overview of Association negotiation.

SOP Classes of the Query/Retrieve Service Class, which include query
services based on the C-FIND operation, may use SOP Class Extended
Negotiation Sub-Item to negotiate options such as Relational-queries and
Enhanced Multi-Frame Image Conversion.

SOP Classes of the Query/Retrieve Service Class, which include retrieval
services based on the C-MOVE and C-GET operations, may use the SOP Class
Extended Negotiation Sub-Item to negotiate relational-retrieval and
Enhanced Multi-Frame Image Conversion.

SOP Classes of the Query/Retrieve Service Class, which include retrieval
services based on the C-GET operation, use the SCP/SCU Role Selection
Sub-Item to identify the SOP Classes that may be used for retrieval.

.. _sect_C.5.1:

Association Negotiation for C-FIND SOP Classes
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

The following negotiation rules apply to DICOM SOP Classes and
Specialized DICOM SOP Classes of the Query/Retrieve Service Class that
include the C-FIND operation.

The Association-requester (query SCU role) shall convey in the
A-ASSOCIATE request:

-  one Abstract Syntax, in a Presentation Context, for each query based
   SOP Class supported

-  optionally, one SOP Class Extended Negotiation Sub-Item, for each
   query based SOP Class

The Association-acceptor (query SCP role) of an A-ASSOCIATE request
shall accept:

-  one Abstract Syntax, in a Presentation Context, for each query based
   SOP Class supported

-  optionally, one SOP Class Extended Negotiation Sub-Item, for each
   query based SOP Class

.. _sect_C.5.1.1:

SOP Class Extended Negotiation
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

The SOP Class Extended Negotiation allows, at Association establishment,
peer DICOM AEs to exchange application Association information defined
by specific SOP Classes. This is achieved by defining the
Service-class-application-information field. The
Service-class-application-information field is used to define support
for relational-queries, combined date time matching, fuzzy semantic
matching of person names, timezone query adjustment and Enhanced
Multi-Frame Image Conversion.

This negotiation is optional. If absent, the default conditions shall
be:

-  no relational-query support

-  separate (independent) Range Matching of date and time Attributes

-  literal matching of person names with case sensitivity unspecified

-  timezone query adjustment unspecified

-  no Enhanced Multi-Frame Image Conversion support

The Association-requester, for each SOP Class, may use one SOP Class
Extended Negotiation Sub-Item. The SOP Class is identified by the
corresponding Abstract Syntax Name (as defined by ) followed by the
Service-class-application-information field. This field defines one or
more sub-fields:

-  relational-query support by the Association-requester

-  combined date and time Range Matching by the Association-requester

-  literal or fuzzy semantic matching of person names by the
   Association-requester

-  timezone query adjustment by the Association-requester

-  Enhanced Multi-Frame Image Conversion support by the
   Association-requester

The Association-acceptor shall return a single byte field (single
sub-field) if offered a single byte field (single sub-field) by the
Association-requester. The Association-acceptor may return either a
single byte field (single sub-field) or a multiple byte field if offered
a multiple byte field by the Association-requester. A one byte response
to a multiple byte request means that the missing sub-fields shall be
treated as 0 values.

.. note::

   The restriction to return only a single byte field if that was all
   that was offered is because the original DICOM Standard only
   contained one byte and older systems may not be expecting more.

The Association-acceptor, for each sub-field of the SOP Class Extended
Negotiation Sub-Item offered, either accepts the Association-requester
proposal by returning the same value (1) or turns down the proposal by
returning the value (0).

If the SOP Class Extended Negotiation Sub-Item is not returned by the
Association-acceptor then relational-queries are not supported over the
Association (default condition).

If the SOP Class Extended Negotiation Sub-Items do not exist in the
A-ASSOCIATE indication they shall be omitted in the A-ASSOCIATE
response.

.. _sect_C.5.1.1.1:

SOP Class Extended Negotiation Sub-Item Structure (A-ASSOCIATE-RQ)
''''''''''''''''''''''''''''''''''''''''''''''''''''''''''''''''''

The SOP Class Extended Negotiation Sub-Item consists of a sequence of
mandatory fields as defined by . `table_title <#table_C.5-1>`__ defines
the Service-class-application-information field for DICOM Query/Retrieve
SOP Classes and Specialized DICOM Query/Retrieve SOP Classes that
include the C-FIND operation. This field may be either one or more bytes
in length (i.e., item bytes 2, 3, 4 and 5 are optional).

.. table:: SOP Class Extended Negotiation Sub-Item
(Service-Class-Application-Information Field) - A-ASSOCIATE-RQ

   +------------+---------------------------+---------------------------+
   | Item Bytes | Field Name                | Description of Field      |
   +============+===========================+===========================+
   | 1          | Relational-queries        | This byte field defines   |
   |            |                           | relational-query support  |
   |            |                           | by the                    |
   |            |                           | Association-requester. It |
   |            |                           | shall be encoded as an    |
   |            |                           | unsigned binary integer   |
   |            |                           | and shall use one of the  |
   |            |                           | following values          |
   |            |                           |                           |
   |            |                           | 0 - relational queries    |
   |            |                           | not supported             |
   |            |                           |                           |
   |            |                           | 1 - relational queries    |
   |            |                           | supported                 |
   +------------+---------------------------+---------------------------+
   | 2          | Date-time matching        | This byte field defines   |
   |            |                           | whether or not combined   |
   |            |                           | date and time Attribute   |
   |            |                           | Range Matching is         |
   |            |                           | requested by the          |
   |            |                           | Association-requester. It |
   |            |                           | shall be encoded as an    |
   |            |                           | unsigned binary integer   |
   |            |                           | and shall use one of the  |
   |            |                           | following values          |
   |            |                           |                           |
   |            |                           | 0 - combined matching not |
   |            |                           | requested                 |
   |            |                           |                           |
   |            |                           | 1 - combined matching     |
   |            |                           | requested                 |
   +------------+---------------------------+---------------------------+
   | 3          | Fuzzy semantic matching   | This byte field defines   |
   |            | of person names           | whether or not fuzzy      |
   |            |                           | semantic person name      |
   |            |                           | Attribute matching is     |
   |            |                           | requested by the          |
   |            |                           | Association-requester. It |
   |            |                           | shall be encoded as an    |
   |            |                           | unsigned binary integer   |
   |            |                           | and shall use one of the  |
   |            |                           | following values          |
   |            |                           |                           |
   |            |                           | 0 - fuzzy semantic        |
   |            |                           | matching not requested    |
   |            |                           |                           |
   |            |                           | 1 - fuzzy semantic        |
   |            |                           | matching requested        |
   +------------+---------------------------+---------------------------+
   | 4          | Timezone query adjustment | This byte field defines   |
   |            |                           | whether or not the        |
   |            |                           | Attribute Timezone Offset |
   |            |                           | From UTC (0008,0201)      |
   |            |                           | shall be used to adjust   |
   |            |                           | the query meaning for     |
   |            |                           | time and datetime fields  |
   |            |                           | in queries. It shall be   |
   |            |                           | encoded as an unsigned    |
   |            |                           | binary integer and shall  |
   |            |                           | use one of the following  |
   |            |                           | values                    |
   |            |                           |                           |
   |            |                           | 0 - Timezone query        |
   |            |                           | adjustment not requested  |
   |            |                           |                           |
   |            |                           | 1 - Timezone query        |
   |            |                           | adjustment requested      |
   +------------+---------------------------+---------------------------+
   | 5          | Enhanced Multi-Frame      | This byte field defines   |
   |            | Image Conversion          | whether or not the        |
   |            |                           | Attribute Query/Retrieve  |
   |            |                           | View (0008,0053) shall be |
   |            |                           | used to adjust the view   |
   |            |                           | returned in queries to    |
   |            |                           | consider conversion to or |
   |            |                           | from Enhanced Multi-Frame |
   |            |                           | Images. It shall be       |
   |            |                           | encoded as an unsigned    |
   |            |                           | binary integer and shall  |
   |            |                           | use one of the following  |
   |            |                           | values                    |
   |            |                           |                           |
   |            |                           | 0 - Query/Retrieve View   |
   |            |                           | not supported             |
   |            |                           |                           |
   |            |                           | 1 - Query/Retrieve View   |
   |            |                           | supported                 |
   +------------+---------------------------+---------------------------+

.. _sect_C.5.1.1.2:

SOP Class Extended Negotiation Sub-Item Structure (A-ASSOCIATE-AC)
''''''''''''''''''''''''''''''''''''''''''''''''''''''''''''''''''

The SOP Class Extended Negotiation Sub-Item is made of a sequence of
mandatory fields as defined by . `table_title <#table_C.5-2>`__ defines
the Service-class-application-information field for DICOM Query/Retrieve
SOP Classes and Specialized DICOM Query/Retrieve SOP Classes that
include the C-FIND operation. This field may be either one or more bytes
in length (i.e., item bytes 2, 3, 4 and 5 are optional).

.. table:: SOP Class Extended Negotiation Sub-Item
(Service-Class-Application-Information Field) - A-ASSOCIATE-AC

   +------------+---------------------------+---------------------------+
   | Item Bytes | Field Name                | Description of Field      |
   +============+===========================+===========================+
   | 1          | Relational-queries        | This byte field defines   |
   |            |                           | relational-query support  |
   |            |                           | for the                   |
   |            |                           | Association-acceptor. It  |
   |            |                           | shall be encoded as an    |
   |            |                           | unsigned binary integer   |
   |            |                           | and shall use one of the  |
   |            |                           | following values          |
   |            |                           |                           |
   |            |                           | 0 - relational-queries    |
   |            |                           | not supported             |
   |            |                           |                           |
   |            |                           | 1 - relational-queries    |
   |            |                           | supported                 |
   +------------+---------------------------+---------------------------+
   | 2          | Date-time matching        | This byte field defines   |
   |            |                           | whether or not combined   |
   |            |                           | date and time Attribute   |
   |            |                           | Range Matching will be    |
   |            |                           | performed by the          |
   |            |                           | Association-acceptor. It  |
   |            |                           | shall be encoded as an    |
   |            |                           | unsigned binary integer   |
   |            |                           | and shall use one of the  |
   |            |                           | following values          |
   |            |                           |                           |
   |            |                           | 0 - combined matching not |
   |            |                           | performed                 |
   |            |                           |                           |
   |            |                           | 1 - combined matching     |
   |            |                           | performed                 |
   +------------+---------------------------+---------------------------+
   | 3          | Fuzzy semantic matching   | This byte field defines   |
   |            | of person names           | whether or not fuzzy      |
   |            |                           | semantic person name      |
   |            |                           | Attribute matching will   |
   |            |                           | be performed by the       |
   |            |                           | Association-acceptor. It  |
   |            |                           | shall be encoded as an    |
   |            |                           | unsigned binary integer   |
   |            |                           | and shall use one of the  |
   |            |                           | following values          |
   |            |                           |                           |
   |            |                           | 0 - fuzzy semantic        |
   |            |                           | matching not performed    |
   |            |                           |                           |
   |            |                           | 1 - fuzzy semantic        |
   |            |                           | matching performed        |
   +------------+---------------------------+---------------------------+
   | 4          | Timezone query adjustment | This byte field defines   |
   |            |                           | whether or not the        |
   |            |                           | Attribute Timezone Offset |
   |            |                           | From UTC (0008,0201)      |
   |            |                           | shall be used to adjust   |
   |            |                           | the query meaning for     |
   |            |                           | time and datetime fields  |
   |            |                           | in queries. It shall be   |
   |            |                           | encoded as an unsigned    |
   |            |                           | binary integer and shall  |
   |            |                           | use one of the following  |
   |            |                           | values                    |
   |            |                           |                           |
   |            |                           | 0 - Timezone adjustment   |
   |            |                           | of queries not performed  |
   |            |                           |                           |
   |            |                           | 1 - Timezone adjustment   |
   |            |                           | of queries performed      |
   +------------+---------------------------+---------------------------+
   | 5          | Enhanced Multi-Frame      | This byte field defines   |
   |            | Image Conversion          | whether or not the        |
   |            |                           | Attribute Query/Retrieve  |
   |            |                           | View (0008,0053) shall be |
   |            |                           | used to adjust the view   |
   |            |                           | returned in queries to    |
   |            |                           | consider conversion to or |
   |            |                           | from Enhanced Multi-Frame |
   |            |                           | Images. It shall be       |
   |            |                           | encoded as an unsigned    |
   |            |                           | binary integer and shall  |
   |            |                           | use one of the following  |
   |            |                           | values                    |
   |            |                           |                           |
   |            |                           | 0 - Query/Retrieve View   |
   |            |                           | not supported             |
   |            |                           |                           |
   |            |                           | 1 - Query/Retrieve View   |
   |            |                           | supported                 |
   +------------+---------------------------+---------------------------+

.. _sect_C.5.2:

Association Negotiation for C-MOVE SOP Classes
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

The following negotiation rules apply to DICOM SOP Classes and
Specialized DICOM SOP Classes of the Query/Retrieve Service Class that
include the C-MOVE operation.

The Association-requester (retrieval SCU role) shall convey in the
A-ASSOCIATE request:

-  one Abstract Syntax, in a Presentation Context, for each retrieval
   based SOP Class supported

-  optionally, one SOP Class Extended Negotiation Sub-Item, for each
   retrieval based SOP Class

The Association-acceptor (retrieval SCP role) of an A-ASSOCIATE request
shall accept:

-  one Abstract Syntax, in a Presentation Context, for each retrieval
   based SOP Class supported

-  optionally, one SOP Class Extended Negotiation Sub-Item, for each
   retrieval based SOP Class

.. _sect_C.5.2.1:

SOP Class Extended Negotiation
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

The SOP Class Extended Negotiation allows, at Association establishment,
peer DICOM AEs to exchange application Association information defined
by specific SOP Classes. This is achieved by defining the
Service-class-application-information field. The
Service-class-application-information field is used to define support
for relational-retrievals.

This negotiation is optional. If absent, the default condition shall be:

-  no relational-retrieval support

-  no Enhanced Multi-Frame Image Conversion support

The Association-requester, for each SOP Class, may use one SOP Class
Extended Negotiation Sub-Item. The SOP Class is identified by the
corresponding Abstract Syntax Name (as defined by ) followed by the
Service-class-application-information field. This field defines:

-  relational-retrieval support by the Association-requester

-  Enhanced Multi-Frame Image Conversion support by the
   Association-requester

The Association-acceptor shall return a single byte field (single
sub-field) if offered a single byte field (single sub-field) by the
Association-requester. The Association-acceptor may return either a
single byte field (single sub-field) or a multiple byte field if offered
a multiple byte field by the Association-requester. A one byte response
to a multiple byte request means that the missing sub-fields shall be
treated as 0 values.

.. note::

   The restriction to return only a single byte field if that was all
   that was offered is because the original DICOM Standard only
   contained one byte and older systems may not be expecting more.

The Association-acceptor, for each SOP Class Extended Negotiation
Sub-Item offered, either accepts the Association-requester proposal by
returning the same value (1) or turns down the proposal by returning the
value (0).

If the SOP Class Extended Negotiation Sub-Item is not returned by the
Association-acceptor then relational-retrievals and Enhanced Multi-Frame
Image Conversion are not supported (default condition).

If the SOP Class Extended Negotiation Sub-Items do not exist in the
A-ASSOCIATE indication they shall be omitted in the A-ASSOCIATE
response.

.. _sect_C.5.2.1.1:

SOP Class Extended Negotiation Sub-Item Structure (A-ASSOCIATE-RQ)
''''''''''''''''''''''''''''''''''''''''''''''''''''''''''''''''''

The SOP Class Extended Negotiation Sub-Item consists of a sequence of
mandatory fields as defined by . `table_title <#table_C.5-3>`__ defines
the Service-class-application-information field for DICOM Query/Retrieve
SOP Classes and Specialized DICOM Query/Retrieve SOP Classes that
include the C-MOVE and C-GET operations.

.. table:: SOP Class Extended Negotiation Sub-Item
(Service-Class-Application-Information Field) - A-ASSOCIATE-RQ

   +------------+---------------------------+---------------------------+
   | Item Bytes | Field Name                | Description of Field      |
   +============+===========================+===========================+
   | 1          | Relational-retrieval      | This byte field defines   |
   |            |                           | relational-retrieval      |
   |            |                           | support by the            |
   |            |                           | Association-requester. It |
   |            |                           | shall be encoded as an    |
   |            |                           | unsigned binary integer   |
   |            |                           | and shall use one of the  |
   |            |                           | following values          |
   |            |                           |                           |
   |            |                           | 0 - relational-retrieval  |
   |            |                           | not supported             |
   |            |                           |                           |
   |            |                           | 1 - relational-retrieval  |
   |            |                           | supported                 |
   +------------+---------------------------+---------------------------+
   | 2          | Enhanced Multi-Frame      | This byte field defines   |
   |            | Image Conversion          | whether or not the        |
   |            |                           | Attribute Query/Retrieve  |
   |            |                           | View (0008,0053) shall be |
   |            |                           | used to adjust the view   |
   |            |                           | returned in queries to    |
   |            |                           | consider conversion to or |
   |            |                           | from Enhanced Multi-Frame |
   |            |                           | Images. It shall be       |
   |            |                           | encoded as an unsigned    |
   |            |                           | binary integer and shall  |
   |            |                           | use one of the following  |
   |            |                           | values                    |
   |            |                           |                           |
   |            |                           | 0 - Query/Retrieve View   |
   |            |                           | not supported             |
   |            |                           |                           |
   |            |                           | 1 - Query/Retrieve View   |
   |            |                           | supported                 |
   +------------+---------------------------+---------------------------+

.. _sect_C.5.2.1.2:

SOP Class Extended Negotiation Sub-Item Structure (A-ASSOCIATE-AC)
''''''''''''''''''''''''''''''''''''''''''''''''''''''''''''''''''

The SOP Class Extended Negotiation Sub-Item consists of a sequence of
mandatory fields as defined by . `table_title <#table_C.5-4>`__ defines
the Service-class-application-information field for DICOM Query/Retrieve
SOP Classes and Specialized DICOM Query/Retrieve SOP Classes that
include the C-MOVE and C-GET operations.

.. table:: SOP Class Extended Negotiation Sub-Item
(Service-Class-Application-Information Field) - A-ASSOCIATE-AC

   +------------+---------------------------+---------------------------+
   | Item Bytes | Field Name                | Description of Field      |
   +============+===========================+===========================+
   | 1          | Relational-retrieval      | This byte field defines   |
   |            |                           | relational-retrieval      |
   |            |                           | support for the           |
   |            |                           | Association-acceptor. It  |
   |            |                           | shall be encoded as an    |
   |            |                           | unsigned binary integer   |
   |            |                           | and shall use one of the  |
   |            |                           | following values          |
   |            |                           |                           |
   |            |                           | 0 - relational-retrievals |
   |            |                           | not supported             |
   |            |                           |                           |
   |            |                           | 1 - relational-retrievals |
   |            |                           | supported                 |
   +------------+---------------------------+---------------------------+
   | 2          | Enhanced Multi-Frame      | This byte field defines   |
   |            | Image Conversion          | whether or not the        |
   |            |                           | Attribute Query/Retrieve  |
   |            |                           | View (0008,0053) shall be |
   |            |                           | used to adjust the view   |
   |            |                           | returned in queries to    |
   |            |                           | consider conversion to or |
   |            |                           | from Enhanced Multi-Frame |
   |            |                           | Images. It shall be       |
   |            |                           | encoded as an unsigned    |
   |            |                           | binary integer and shall  |
   |            |                           | use one of the following  |
   |            |                           | values                    |
   |            |                           |                           |
   |            |                           | 0 - Query/Retrieve View   |
   |            |                           | not supported             |
   |            |                           |                           |
   |            |                           | 1 - Query/Retrieve View   |
   |            |                           | supported                 |
   +------------+---------------------------+---------------------------+

.. _sect_C.5.3:

Association Negotiation for C-GET SOP Classes
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

When an SCP performs the C-GET operation it induces a C-STORE operation
for the purpose of transmitting composite SOP Instances for Storage.
This induced C-STORE operation (called a sub-operation) requires a
switch from the C-GET Presentation Context to a Presentation Context
that supports the specific C-STORE sub-operation.

The following negotiation rules apply to retrieval based DICOM
Query/Retrieve SOP Classes and Specialized DICOM Query/Retrieve SOP
Classes that include the C-GET operation.

The Association-requester (retrieve SCU role) in the A-ASSOCIATE request
shall convey:

a. C-GET operation support with:

   -  one Abstract Syntax, in a Presentation Context, for each SOP Class
      supported

   -  and optionally, one SOP Class Extended Negotiation Sub-Item, for
      each retrieval based SOP Class

b. Induced Storage sub-operation support where the SOP Class (in the
   retrieval SCU role) is acting as a Storage SOP Class in the SCP Role.
   See `figure_title <#figure_C.5-1>`__. For each supported Storage SOP
   Class, the A-ASSOCIATE request contains:

   -  one Abstract Syntax in a Presentation Context

   -  one SCP/SCU Role Selection Negotiation Sub-Item with the SCP-role
      field set to indicate support of the SCP role. The SCP/SCU Role
      Selection Negotiation shall be used as defined in .

.. note::

   This negotiation does not place any requirements on the SCU-flag of
   the SCP/SCU Role Selection Negotiation Sub-Item. It may be set if the
   Association-requester supports the Storage Service Class in the SCU
   role.

The Association-acceptor (retrieve SCP role) in the A-ASSOCIATE response
shall convey:

a. C-GET operation support with:

   -  one Abstract Syntax, in a Presentation Context, for each SOP Class
      supported

b. Induced Storage sub-operation support where the SOP Class (using the
   retrieval SCP role) is acting as a Storage SOP Class in the SCU Role.
   See `figure_title <#figure_C.5-1>`__. For each supported Storage SOP
   Class, the A-ASSOCIATE response contains both:

   -  one Abstract Syntax, in a Presentation Context

   -  one SCP/SCU Role Selection Negotiation Sub-Item with the SCP-role
      field set to indicate the acceptance of the
      Association-requester's support of the SCP role. The SCP/SCU Role
      Selection Negotiation shall be used as defined in .

.. note::

   The negotiation does not place any requirements on the SCU-flag of
   the SCP/SCU Role Selection Negotiation Sub-Item. It may be set if the
   Association-acceptor accepts the Storage SCP role.
   `figure_title <#figure_C.5-2>`__ illustrates an example of the
   retrieve (C-GET) negotiation.

`figure_title <#figure_C.5-2>`__ illustrates an example of the retrieve
(C-GET) negotiation.

.. _sect_C.5.3.1:

SOP Class Extended Negotiation
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

The SOP Class Extended Negotiation allows, at Association establishment,
peer DICOM AEs to exchange application Association information defined
by specific SOP Classes.

This is achieved by defining the Service-class-application-information
field. The Service-class-application-information field is used to define
support for relational-retrievals and alternative views for Enhanced
Multi-Frame Image Conversion.

Extended negotiation for SOP Classes based on the retrieval services
that include C-GET operations is identical to the negotiation defined
for C-MOVE, which is defined in `SOP Class Extended
Negotiation <#sect_C.5.2.1>`__ of this Annex.

Extended negotiation for the SOP Classes of the Storage Service Class
(for the C-STORE sub-operation) is defined in `Storage Service Class
(Normative) <#chapter_B>`__.

.. _sect_C.6:

SOP Class Definitions
---------------------

.. _sect_C.6.1:

Patient Root SOP Class Group
~~~~~~~~~~~~~~~~~~~~~~~~~~~~

In the Patient Root Query/Retrieve Information Model, the information is
arranged into four levels that correspond to one of the four values in
element (0008,0052) shown in `table_title <#table_C.6.1-1>`__.

.. table:: Query/Retrieve Level Values for Patient Root

   ===================================== ====================
   Query/Retrieve Level                  Value in (0008,0052)
   ===================================== ====================
   Patient Information                   PATIENT
   Study Information                     STUDY
   Series Information                    SERIES
   Composite Object Instance Information IMAGE
   ===================================== ====================

.. note::

   The use of the word "Images" rather than "Composite Object Instances"
   is historical to allow backward compatibility with previous editions
   of the standard. It should not be taken to mean that Composite Object
   Instances of other than image type are not included at the level
   indicated by the value IMAGE.

.. _sect_C.6.1.1:

Patient Root Query/Retrieve Information Model
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

.. _sect_C.6.1.1.1:

E/R Model
'''''''''

The Patient Root Query/Retrieve Information Model may be represented by
the entity relationship diagram shown in
`figure_title <#figure_C.6-1>`__.

.. _sect_C.6.1.1.2:

Patient Level
'''''''''''''

`table_title <#table_C.6-1>`__ defines the Attributes at the Patient
Query/Retrieve level of the Patient Root Query/Retrieve Information
Model.

.. note::

   1. A description of the Attributes of this Information Model is
      contained in `Standard Query/Retrieve Information
      Models <#sect_C.3>`__ of this Part.

   2. Although the Patient ID may not be globally unique, the Study
      Instance UID is globally unique ensuring that no two studies may
      be misidentified. The scope of uniqueness of the Patient ID may be
      specified using the Issuer of Patient ID (0010,0021).

   3. Previously, Other Patient IDs (0010,1000) was included in this
      table. This Attribute have been retired. See PS3.4 2017a.

.. table:: Patient Level Attributes for the Patient Root Query/Retrieve
Information Model

   ======================================= =========== ====
   Attribute Name                          Tag         Type
   ======================================= =========== ====
   Patient's Name                          (0010,0010) R
   Patient ID                              (0010,0020) U
   Issuer of Patient ID                    (0010,0021) O
   Referenced Patient Sequence             (0008,1120) O
   >Referenced SOP Class UID               (0008,1150) O
   >Referenced SOP Instance UID            (0008,1155) O
   Patient's Birth Date                    (0010,0030) O
   Patient's Birth Time                    (0010,0032) O
   Patient's Sex                           (0010,0040) O
   Other Patient IDs Sequence              (0010,1002) O
   Other Patient Names                     (0010,1001) O
   Ethnic Group                            (0010,2160) O
   Patient Comments                        (0010,4000) O
   Number of Patient Related Studies       (0020,1200) O
   Number of Patient Related Series        (0020,1202) O
   Number of Patient Related Instances     (0020,1204) O
   *All other Attributes at Patient Level*             O
   ======================================= =========== ====

.. _sect_C.6.1.1.3:

Study Level
'''''''''''

`table_title <#table_C.6-2>`__ defines the keys at the Study Information
level of the Patient Root Query/Retrieve Information Model.

.. note::

   1. A description of the Attributes of this Information Model is
      contained in `Standard Query/Retrieve Information
      Models <#sect_C.3>`__ of this Part.

   2. Although the Patient ID may not be globally unique, the Study
      Instance UID is globally unique ensuring that no two studies may
      be misidentified. The scope of uniqueness of the Patient ID may be
      specified using the Issuer of Patient ID (0010,0021).

.. table:: Enhanced Code Value Keys Macro with Optional Keys

   =========================================== =========== ================
   Attribute Name                              Tag         Requirement Type
   =========================================== =========== ================
   *Include*\ `table_title <#table_C.6-2b>`__              
   Equivalent Code Sequence                    (0008,0121) O
   *>Include*\ `table_title <#table_C.6-2b>`__             
   =========================================== =========== ================

.. table:: Basic Code Value Keys Macro with Optional Keys

   +--------------------------+-------------+--------------------------+
   | Attribute Name           | Tag         | Requirement Type         |
   +==========================+=============+==========================+
   | Code Value               | (0008,0100) | OC - May be present only |
   |                          |             | if the code value length |
   |                          |             | is 16 characters or      |
   |                          |             | less, and the code value |
   |                          |             | is not a URN or URL.     |
   +--------------------------+-------------+--------------------------+
   | Coding Scheme Designator | (0008,0102) | O                        |
   +--------------------------+-------------+--------------------------+
   | Coding Scheme Version    | (0008,0103) | O                        |
   +--------------------------+-------------+--------------------------+
   | Code Meaning             | (0008,0104) | O                        |
   +--------------------------+-------------+--------------------------+
   | Long Code Value          | (0008,0119) | OC - May be present only |
   |                          |             | if Code Value            |
   |                          |             | (0008,0100) is not       |
   |                          |             | present, and the code    |
   |                          |             | value is not a URN or    |
   |                          |             | URL.                     |
   +--------------------------+-------------+--------------------------+
   | URN Code Value           | (0008,0120) | OC - May be present only |
   |                          |             | if Code Value            |
   |                          |             | (0008,0100) is not       |
   |                          |             | present, and the code    |
   |                          |             | value is a URN or URL.   |
   +--------------------------+-------------+--------------------------+
   | Context Identifier       | (0008,010e) | O                        |
   +--------------------------+-------------+--------------------------+
   | Context UID              | (0008,0117) | O                        |
   +--------------------------+-------------+--------------------------+
   | Mapping Resource         | (0008,0105) | O                        |
   +--------------------------+-------------+--------------------------+
   | Mapping Resource UID     | (0008,0118) | O                        |
   +--------------------------+-------------+--------------------------+
   | Context Group Version    | (0008,0118) | O                        |
   +--------------------------+-------------+--------------------------+
   | Context Group Extension  | (0008,010B) | O                        |
   | Flag                     |             |                          |
   +--------------------------+-------------+--------------------------+
   | Context Group Local      | (0008,0107) | O                        |
   | Version                  |             |                          |
   +--------------------------+-------------+--------------------------+
   | Context Group Extension  | (0008,010D) | O                        |
   | Creator UID              |             |                          |
   +--------------------------+-------------+--------------------------+

.. table:: Study Level Keys for the Patient Root Query/Retrieve
Information Model

   =========================================== =========== ====
   Attribute Name                              Tag         Type
   =========================================== =========== ====
   Study Date                                  (0008,0020) R
   Study Time                                  (0008,0030) R
   Accession Number                            (0008,0050) R
   Study ID                                    (0020,0010) R
   Study Instance UID                          (0020,000D) U
   Modalities in Study                         (0008,0061) O
   SOP Classes in Study                        (0008,0062) O
   Anatomic Regions in Study Code Sequence     (0008,0063) O
   *>Include*\ `table_title <#table_C.6-2a>`__             
   Referring Physician's Name                  (0008,0090) O
   Study Description                           (0008,1030) O
   Procedure Code Sequence                     (0008,1032) O
   *>Include*\ `table_title <#table_C.6-2a>`__             
   Name of Physician(s) Reading Study          (0008,1060) O
   Admitting Diagnoses Description             (0008,1080) O
   Referenced Study Sequence                   (0008,1110) O
   >Referenced SOP Class UID                   (0008,1150) O
   >Referenced SOP Instance UID                (0008,1155) O
   Patient's Age                               (0010,1010) O
   Patient's Size                              (0010,1020) O
   Patient's Weight                            (0010,1030) O
   Occupation                                  (0010,2180) O
   Additional Patient History                  (0010,21B0) O
   Other Study Numbers                         (0020,1070) O
   Number of Study Related Series              (0020,1206) O
   Number of Study Related Instances           (0020,1208) O
   *All other Attributes at Study Level*                   O
   =========================================== =========== ====

.. _sect_C.6.1.1.4:

Series Level
''''''''''''

`table_title <#table_C.6-3>`__ defines the keys at the Series
Information level of the Patient Root Query/Retrieve Information Model.

.. table:: Series Level Attributes for the Patient Root Query/Retrieve
Information Model

   ====================================== =========== ====
   Attribute Name                         Tag         Type
   ====================================== =========== ====
   Modality                               (0008,0060) R
   Series Number                          (0020,0011) R
   Series Instance UID                    (0020,000E) U
   Number of Series Related Instances     (0020,1209) O
   *All Other Attributes at Series Level*             O
   ====================================== =========== ====

.. note::

   The Attribute Number of Series Related Instances is an optional key.
   It is, however recognized as a broadly needed key and return
   Attribute, which SCPs are strongly encouraged to support.

.. _sect_C.6.1.1.5:

Composite Object Instance Level
'''''''''''''''''''''''''''''''

`table_title <#table_C.6-4>`__ defines the keys at the Composite Object
Instance Information level of the Patient Root Query/Retrieve
Information Model.

.. table:: Composite Object Instance Level Keys for the Patient Root
Query/Retrieve Information Model

   +-----------------------------------------------------------+-------------+------+
   | Attribute Name                                            | Tag         | Type |
   +===========================================================+=============+======+
   | Instance Number                                           | (0020,0013) | R    |
   +-----------------------------------------------------------+-------------+------+
   | SOP Instance UID                                          | (0008,0018) | U    |
   +-----------------------------------------------------------+-------------+------+
   | SOP Class UID                                             | (0008,0016) | O    |
   +-----------------------------------------------------------+-------------+------+
   | Available Transfer Syntax UID                             | (0008,3002) | O    |
   +-----------------------------------------------------------+-------------+------+
   | Alternate Representation Sequence                         | (0008,3001) | O    |
   +-----------------------------------------------------------+-------------+------+
   | >Series Instance UID                                      | (0020,000E) | O    |
   +-----------------------------------------------------------+-------------+------+
   | >SOP Class UID                                            | (0008,1150) | O    |
   +-----------------------------------------------------------+-------------+------+
   | >SOP Instance UID                                         | (0008,1155) | O    |
   +-----------------------------------------------------------+-------------+------+
   | >Purpose of Reference Code Sequence                       | (0040,A170) | O    |
   +-----------------------------------------------------------+-------------+------+
   | *>>Include*\ `table_title <#table_C.6-2a>`__              |             |      |
   +-----------------------------------------------------------+-------------+------+
   | Related General SOP Class UID                             | (0008,001A) | O    |
   +-----------------------------------------------------------+-------------+------+
   | Concept Name Code Sequence                                | (0040,A043) | O    |
   +-----------------------------------------------------------+-------------+------+
   | *>Include*\ `table_title <#table_C.6-2a>`__               |             |      |
   +-----------------------------------------------------------+-------------+------+
   | Content Template Sequence                                 | (0040,A504) | O    |
   +-----------------------------------------------------------+-------------+------+
   | >Template Identifier                                      | (0040,DB00) | O    |
   +-----------------------------------------------------------+-------------+------+
   | >Mapping Resource                                         | (0008,0105) | O    |
   +-----------------------------------------------------------+-------------+------+
   | Container Identifier                                      | (0040,0512) | O    |
   +-----------------------------------------------------------+-------------+------+
   | Specimen Description Sequence                             | (0040,0560) | O    |
   +-----------------------------------------------------------+-------------+------+
   | >Specimen Identifier                                      | (0040,0551) | O    |
   +-----------------------------------------------------------+-------------+------+
   | >Specimen UID                                             | (0040,0554) | O    |
   +-----------------------------------------------------------+-------------+------+
   | *All Other Attributes at Composite Object Instance Level* |             | O    |
   +-----------------------------------------------------------+-------------+------+

.. note::

   1. SOP Class UID (0008,0016) is an optional key, but it is strongly
      recommended that it always be returned by all SCPs, if matching is
      requested.

   2. The Concept Name Code Sequence (0040,A043) and Content Template
      Sequence (0040,A504) are optional keys that are useful for
      identifying instances of various Structured Reporting Storage SOP
      Classes. It is strongly recommended that these keys be supported
      by the SCP for query against such instances.

.. _sect_C.6.1.1.5.1:

Alternate Representation Sequence
                                 

The Alternate Representation Sequence (0008,3001) encodes a reference to
an alternate encoding of the composite image identified in the Query
response item. This alternate encoding may utilize a different SOP Class
or have different image quality characteristics, but it shall be the
same image.

.. note::

   The Alternate Representation Sequence (0008,3001) allows the query
   response about an original image to reference a lossy compressed
   version, and vice versa.

An image may be lossy compressed, e.g., for long-term archive purposes,
and its SOP Instance UID changed. An application processing a SOP
Instance that references the original image UID, e.g., a Structured
Report, may query the C-FIND SCP for the image. The SCP returns a
reference to an accessible version of the image even if the original SOP
Instance is no longer available.

The Alternate Representation Sequence (0008,3001), if present in a Query
Request Identifier, shall be zero-length, or shall contain a single
zero-length Item. That is, only Universal Matching is defined for this
Attribute.

The Alternate Representation Sequence (0008,3001), if present in the
Query Response Identifier, may include zero or more Items. Each
Alternate Representation Sequence Item in the Query Response Identifier
shall include

-  the Series Instance UID (0020,000E) if the alternately encoded image
   is in a different Series.

-  the SOP Class UID (0008,0016) and SOP Instance UID (0008,0018) of the
   alternately encoded image.

-  the Purpose of Reference Code Sequence (0040,A170), which shall
   describe the nature of the alternate encoding of the image. The
   Purpose of Reference Code Sequence (0040,A170) shall include only one
   Item. The Baseline Context Group for this Code Sequence is CID 7205.

.. _sect_C.6.1.1.5.2:

Available SOP Transfer Syntax UID
                                 

The Available Transfer Syntax UID (0008,3002) describes one or more
Transfer Syntaxes that the SCP can assure will be supported for
retrieval of the SOP Instance. This may, but is not required to, include
the Transfer Syntax in which the SCP has stored the instance. For all
Transfer Syntaxes listed, no loss shall be involved in transcoding from
whatever is stored.

The Attribute is multi-valued, and if more than one value is present,
then the SCU may interpret those Transfer Syntaxes listed earlier as
being preferred by the SCP over those listed later. E.g., the order
might reflect the amount of effort required to convert from the stored
form, and the first listed might be the stored form.

There is no requirement to include every Transfer Syntax in which the
instance may be retrieved without loss. E.g., the Default Transfer
Syntax as specified in , if it is applicable, might be omitted if it is
not the Transfer Syntax in which the instance happens to be stored.

.. note::

   The value of this Attribute may be useful, for example, to determine
   if the the instance is stored in a lossy Transfer Syntax that is not
   supported by the SCU, and for which decompression or conversion into
   a different compressed form would involve loss and be inappropriate,
   and require use of an Alternate Representation.

.. _sect_C.6.1.1.6:

Scope of the C-GET and C-MOVE Commands and Sub-Operations
'''''''''''''''''''''''''''''''''''''''''''''''''''''''''

A C-MOVE or C-GET request may be performed to any level of the
Query/Retrieve Model. However, the transfer of Stored SOP Instances
shall always take place at the Composite Object Instance level. A C-MOVE
or C-GET where the Query/Retrieve level is the:

-  PATIENT level indicates that all Composite Object Instances related
   to a Patient shall be transferred.

-  STUDY level indicates that all Composite Object Instances related to
   a Study shall be transferred.

-  SERIES level indicates that all Composite Object Instances related to
   a Series shall be transferred.

-  IMAGE level indicates that selected individual Composite Object
   Instances shall be transferred.

.. note::

   In the Baseline behavior, more than one entity may be retrieved if
   the Query/Retrieve Level is IMAGE, SERIES or STUDY, using List of UID
   matching, but only Single Value Matching value may be specified for
   Patient ID (0010,0020).

.. _sect_C.6.1.2:

Conformance Requirements
^^^^^^^^^^^^^^^^^^^^^^^^

An implementation may conform to one of the SOP Classes of the Patient
Root SOP Class Group as an SCU, SCP or both. The Conformance Statement
shall be in the format defined in .

.. _sect_C.6.1.2.1:

SCU Conformance
'''''''''''''''

.. _sect_C.6.1.2.1.1:

C-FIND SCU Conformance
                      

An implementation that conforms to one of the SOP Classes of the Patient
Root SOP Class Group shall support queries against the Query/Retrieve
Information Model described in `Patient Root Query/Retrieve Information
Model <#sect_C.6.1.1>`__ using the baseline C-FIND SCU Behavior
described in `C-FIND SCU Behavior <#sect_C.4.1.2>`__.

An implementation that conforms to one of the SOP Classes of the Patient
Root SOP Class Group as an SCU shall state in its Conformance Statement
whether it supports Optional Keys. If it supports Optional Keys, then it
shall list the Optional Keys that it supports.

An implementation that conforms to one of the SOP Classes of the Patient
Root SOP Class Group as an SCU shall state in its Conformance Statement
whether it may generate Relational-queries. If it supports
Relational-queries, then it shall also support extended negotiation of
relational-queries.

An implementation that conforms to one of the SOP Classes of the Patient
Root SOP Class Group as an SCU shall state in its Conformance Statement
whether or not it supports extended negotiation of combined date-time
matching and/or fuzzy semantic matching of person names.

An implementation that conforms to one of the SOP Classes of the Patient
Root SOP Class Group as an SCU shall state in its Conformance Statement
how it makes use of Specific Character Set (0008,0005) and Timezone
Offset From UTC (0008,0201) when encoding queries and interpreting
responses.

.. _sect_C.6.1.2.1.2:

C-MOVE SCU Conformance
                      

An implementation that conforms to one of the SOP Classes of the Patient
Root SOP Class Group as an SCU shall support transfers against the
Query/Retrieve Information Model described in `Patient Root
Query/Retrieve Information Model <#sect_C.6.1.1>`__ using the C-MOVE SCU
Behavior described in `C-MOVE SCU Behavior <#sect_C.4.2.2>`__.

.. _sect_C.6.1.2.1.3:

C-GET SCU Conformance
                     

An implementation that conforms to one of the SOP Classes of the Patient
Root SOP Class Group as an SCU shall support retrievals against the
Query/Retrieve Information Model described in `Patient Root
Query/Retrieve Information Model <#sect_C.6.1.1>`__ using the C-GET SCU
Behavior described in `C-GET SCU Behavior <#sect_C.4.3.2>`__.

An implementation that conforms to one of the SOP Classes of the Patient
Root SOP Class Group as an SCU, which generates retrievals using the
C-GET operation, shall state in its Conformance Statement the Storage
Service Class SOP Classes under which it shall support the C-STORE
sub-operations generated by the C-GET.

.. _sect_C.6.1.2.2:

SCP Conformance
'''''''''''''''

.. _sect_C.6.1.2.2.1:

C-FIND SCP Conformance
                      

An implementation that conforms to one of the SOP Classes of the Patient
Root SOP Class Group shall support queries against the Query/Retrieve
Information Model described in `Patient Root Query/Retrieve Information
Model <#sect_C.6.1.1>`__ using the C-FIND SCP Behavior described in
`C-FIND SCP Behavior <#sect_C.4.1.3>`__.

An implementation that conforms to one of the SOP Classes of the Patient
Root SOP Class Group as an SCP shall state in its Conformance Statement
whether it supports Optional Keys. If it supports Optional Keys, then it
shall list the Optional Keys that it supports.

An implementation that conforms to one of the SOP Classes of the Patient
Root SOP Class Group as an SCP shall state in its Conformance Statement
whether it supports Relational-queries. If it supports
Relational-queries, then it shall also support extended negotiation of
relational-queries.

An implementation that conforms to one of the SOP Classes of the Patient
Root SOP Class Group as an SCP shall state in its Conformance Statement
whether or not it supports extended negotiation of combined date-time
matching and/or fuzzy semantic matching of person names. If fuzzy
semantic matching of person names is supported, then the mechanism for
fuzzy semantic matching shall be specified.

An implementation that conforms to one of the SOP Classes of the Patient
Root SOP Class Group as an SCP shall state in its Conformance Statement
whether it supports case-insensitive matching for PN VR Attributes and
list Attributes for which this applies.

An implementation that conforms to one of the SOP Classes of the Patient
Root SOP Class Group as an SCP shall state in its Conformance Statement
how it makes use of Specific Character Set (0008,0005) and Timezone
Offset From UTC (0008,0201) when interpreting queries, performing
matching and encoding responses.

.. _sect_C.6.1.2.2.2:

C-MOVE SCP Conformance
                      

An implementation that conforms to one of the SOP Classes of the Patient
Root SOP Class Group as an SCP shall support transfers against the
Query/Retrieve Information Model described in `Patient Root
Query/Retrieve Information Model <#sect_C.6.1.1>`__ using the C-MOVE SCP
Behavior described in `C-MOVE SCP Behavior <#sect_C.4.2.3>`__.

An implementation that conforms to one of the SOP Classes of the Patient
Root SOP Class Group as an SCP, which generates transfers using the
C-MOVE operation shall state in its Conformance Statement the Storage
Service Class SOP Classes under which it shall support the C-STORE
sub-operations generated by the C-MOVE.

.. _sect_C.6.1.2.2.3:

C-GET SCP Conformance
                     

An implementation that conforms to one of the SOP Classes of the Patient
Root SOP Class Group as an SCP shall support retrievals against the
Query/Retrieve Information Model described in `Patient Root
Query/Retrieve Information Model <#sect_C.6.1.1>`__ using the C-GET SCP
Behavior described in `C-GET SCP Behavior <#sect_C.4.3.3>`__.

An implementation that conforms to one of the SOP Classes of the Patient
Root SOP Class Group as an SCP, which generates retrievals using the
C-GET operation, shall state in its Conformance Statement the Storage
Service Class SOP Classes under which it shall support the C-STORE
sub-operations generated by the C-GET.

.. _sect_C.6.1.3:

SOP Classes
^^^^^^^^^^^

The SOP Classes in the Patient Root Query SOP Class Group of the
Query/Retrieve Service Class identify the Patient Root Query/Retrieve
Information Model, and the DIMSE-C operations supported. The Standard
SOP Classes are listed in `table_title <#table_C.6.1.3-1>`__.

.. table:: SOP Classes for Patient Root Query/Retrieve

   +---------------------------------------+-----------------------------+
   | SOP Class Name                        | SOP Class UID               |
   +=======================================+=============================+
   | Patient Root Query/Retrieve           | 1.2.840.10008.5.1.4.1.2.1.1 |
   | Information Model - FIND              |                             |
   +---------------------------------------+-----------------------------+
   | Patient Root Query/Retrieve           | 1.2.840.10008.5.1.4.1.2.1.2 |
   | Information Model - MOVE              |                             |
   +---------------------------------------+-----------------------------+
   | Patient Root Query/Retrieve           | 1.2.840.10008.5.1.4.1.2.1.3 |
   | Information Model - GET               |                             |
   +---------------------------------------+-----------------------------+

.. _sect_C.6.2:

Study Root SOP Class Group
~~~~~~~~~~~~~~~~~~~~~~~~~~

In the Study Root Query/Retrieve Information Model, the information is
arranged into three levels that correspond to one of the three values in
element (0008,0052) shown in `table_title <#table_C.6.2-1>`__.

.. table:: Query/Retrieve Level Values for Study Root

   ===================================== ====================
   Query/Retrieve Level                  Value in (0008,0052)
   ===================================== ====================
   Study Information                     STUDY
   Series Information                    SERIES
   Composite Object Instance Information IMAGE
   ===================================== ====================

.. note::

   The use of the word "Images" rather than "Composite Object Instances"
   is historical to allow backward compatibility with previous editions
   of the Standard. It should not be taken to mean that Composite Object
   Instances of other than image type are not included at the level
   indicated by the value IMAGE.

.. _sect_C.6.2.1:

Study Root Query/Retrieve Information Model
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

.. _sect_C.6.2.1.1:

E/R Model
'''''''''

The Study Root Query/Retrieve Information Model may be represented by
the entity relationship diagram shown in
`figure_title <#figure_C.6-2>`__.

.. _sect_C.6.2.1.2:

Study Level
'''''''''''

`table_title <#table_C.6-5>`__ defines the keys at the Study Information
level of the Study Root Query/Retrieve Information Model.

.. note::

   1. A description of the Attributes of this Information Model is
      contained in `Standard Query/Retrieve Information
      Models <#sect_C.3>`__.

   2. Although the Patient ID may not be globally unique, the Study
      Instance UID is globally unique ensuring that no two studies may
      be misidentified. The scope of uniqueness of the Patient ID may be
      specified using the Issuer of Patient ID (0010,0021).

   3. Previously, Other Patient IDs (0010,1000) was included in this
      table. This Attribute have been retired. See PS3.4 2017a.

.. table:: Study Level Keys for the Study Root Query/Retrieve
Information Model

   =========================================== =========== ====
   Attribute Name                              Tag         Type
   =========================================== =========== ====
   Study Date                                  (0008,0020) R
   Study Time                                  (0008,0030) R
   Accession Number                            (0008,0050) R
   Patient's Name                              (0010,0010) R
   Patient ID                                  (0010,0020) R
   Study ID                                    (0020,0010) R
   Study Instance UID                          (0020,000D) U
   Modalities in Study                         (0008,0061) O
   SOP Classes in Study                        (0008,0062) O
   Anatomic Regions in Study Code Sequence     (0008,0063) O
   *>Include*\ `table_title <#table_C.6-2a>`__             
   Referring Physician's Name                  (0008,0090) O
   Study Description                           (0008,1030) O
   Procedure Code Sequence                     (0008,1032) O
   *>Include*\ `table_title <#table_C.6-2a>`__             
   Name of Physician(s) Reading Study          (0008,1060) O
   Admitting Diagnoses Description             (0008,1080) O
   Referenced Study Sequence                   (0008,1110) O
   >Referenced SOP Class UID                   (0008,1150) O
   >Referenced SOP Instance UID                (0008,1155) O
   Referenced Patient Sequence                 (0008,1120) O
   >Referenced SOP Class UID                   (0008,1150) O
   >Referenced SOP Instance UID                (0008,1155) O
   Issuer of Patient ID                        (0010,0021) O
   Patient's Birth Date                        (0010,0030) O
   Patient's Birth Time                        (0010,0032) O
   Patient's Sex                               (0010,0040) O
   Other Patient IDs Sequence                  (0010,1002) O
   Other Patient Names                         (0010,1001) O
   Patient's Age                               (0010,1010) O
   Patient's Size                              (0010,1020) O
   Patient's Weight                            (0010,1030) O
   Ethnic Group                                (0010,2160) O
   Occupation                                  (0010,2180) O
   Additional Patient History                  (0010,21B0) O
   Patient Comments                            (0010,4000) O
   Other Study Numbers                         (0020,1070) O
   Number of Study Related Series              (0020,1206) O
   Number of Study Related Instances           (0020,1208) O
   *All other Attributes at Study Level*                   O
   =========================================== =========== ====

.. note::

   The use of the word "Images" rather than "Composite Object Instances"
   is historical, and should not be taken to mean that Composite Object
   Instances of other than image type are not included in the number.

.. _sect_C.6.2.1.3:

Series Level
''''''''''''

Attributes for the Series Level of the Study Root Query/Retrieve
Information Model are the same as the Attributes for the Series Level of
the Patient Root Query/Retrieve Information Model described in `Series
Level <#sect_C.6.1.1.4>`__.

.. _sect_C.6.2.1.4:

Composite Object Instance Level
'''''''''''''''''''''''''''''''

Attributes for the Composite Object Instance Level of the Study Root
Query/Retrieve Information Model are the same as the Attributes for the
Composite Object Instance Level of the Patient Root Query/Retrieve
Information Model described in `Composite Object Instance
Level <#sect_C.6.1.1.5>`__.

.. _sect_C.6.2.1.5:

Scope of the Get and Move Commands and Sub-Operations
'''''''''''''''''''''''''''''''''''''''''''''''''''''

A C-MOVE or C-GET request may be performed to any level of the
Query/Retrieve Model. However, the transfer of Stored SOP Instances
shall always take place at the Composite Object Instance level. A C-MOVE
or C-GET where the Query/Retrieve level is the:

-  STUDY level indicates that all Composite Object Instances related to
   a Study shall be transferred

-  SERIES level indicates that all Composite Object Instances related to
   a Series shall be transferred

-  IMAGE level indicates that selected individual Composite Object
   Instances shall be transferred

.. note::

   In the Baseline behavior, more than one entity may be retrieved if
   the Query/Retrieve Level is IMAGE, SERIES or STUDY, using List of UID
   matching,

.. _sect_C.6.2.2:

Conformance Requirements
^^^^^^^^^^^^^^^^^^^^^^^^

An implementation may conform to one of the SOP Classes of the Study
Hierarchy SOP Class Group as an SCU, SCP or both. The Conformance
Statement shall be in the format defined in .

.. _sect_C.6.2.2.1:

SCU Conformance
'''''''''''''''

.. _sect_C.6.2.2.1.1:

C-FIND SCU Conformance
                      

An implementation that conforms to one of the SOP Classes of the Study
Root SOP Class Group shall support queries against the Query/Retrieve
Information Model described in `Study Root Query/Retrieve Information
Model <#sect_C.6.2.1>`__ using the C-FIND SCU behavior described in
`C-FIND SCU Behavior <#sect_C.4.1.2>`__.

An implementation that conforms to one of the SOP Classes of the Study
Root SOP Class Group as an SCU shall state in its Conformance Statement
whether it supports Optional Keys. If it supports Optional Keys, then it
shall list the Optional Keys that it supports.

An implementation that conforms to one of the SOP Classes of the Study
Root SOP Class Group as an SCU shall be capable of generating queries
using the Hierarchical Search. It shall not generate queries using
Relational-queries unless the Relational-queries option has been
successfully negotiated.

An implementation that conforms to one of the SOP Classes of the Study
Root SOP Class Group as an SCU shall state in its Conformance Statement
whether it may generate Relational-queries. If it supports Relational
Search, then it shall also support extended negotiation of
relational-queries.

An implementation that conforms to one of the SOP Classes of the Study
Root SOP Class Group as an SCU shall state in its Conformance Statement
whether or not it supports extended negotiation of combined date-time
matching and/or fuzzy semantic matching of person names.

An implementation that conforms to one of the SOP Classes of the Study
Root SOP Class Group as an SCU shall state in its Conformance Statement
how it makes use of Specific Character Set (0008,0005) and Timezone
Offset From UTC (0008,0201) when encoding queries and interpreting
responses.

.. _sect_C.6.2.2.1.2:

C-MOVE SCU Conformance
                      

An implementation that conforms to one of the SOP Classes of the Study
Root SOP Class Group as an SCU shall support transfers against the
Query/Retrieve Information Model described in `Study Root Query/Retrieve
Information Model <#sect_C.6.2.1>`__ using the C-MOVE SCU Behavior
described in `C-MOVE SCU Behavior <#sect_C.4.2.2>`__.

.. _sect_C.6.2.2.1.3:

C-GET SCU Conformance
                     

An implementation that conforms to one of the SOP Classes of the Study
Root SOP Class Group as an SCU shall support retrievals against the
Query/Retrieve Information Model described in `Study Root Query/Retrieve
Information Model <#sect_C.6.2.1>`__ using the C-GET SCU Behavior
described in `C-GET SCU Behavior <#sect_C.4.3.2>`__.

An implementation that conforms to one of the SOP Classes of the Study
Root SOP Class Group as an SCU, which generates retrievals using the
C-GET operation shall state in its Conformance Statement the Storage
Service Class SOP Classes under which it shall support the C-STORE
sub-operations generated by the C-GET.

.. _sect_C.6.2.2.2:

SCP Conformance
'''''''''''''''

.. _sect_C.6.2.2.2.1:

C-FIND SCP Conformance
                      

An implementation that conforms to one of the SOP Classes of the Study
Root SOP Class Group shall support queries against the Query/Retrieve
Information Model described in `Study Root Query/Retrieve Information
Model <#sect_C.6.2.1>`__ using the C-FIND SCP behavior described in
`C-FIND SCP Behavior <#sect_C.4.1.3>`__.

An implementation that conforms to one of the SOP Classes of the Study
Root SOP Class Group as an SCP shall state in its Conformance Statement
whether it supports Optional Keys. If it supports Optional Keys, then it
shall list the Optional Keys that it supports.

An implementation that conforms to one of the SOP Classes of the Study
Root SOP Class Group as an SCP shall state in its Conformance Statement
whether it supports Relational Search. If it supports Relational Search,
then it shall also support extended negotiation of relational-queries.

An implementation that conforms to one of the SOP Classes of the Study
Root SOP Class Group as an SCP shall state in its Conformance Statement
whether or not it supports extended negotiation of combined date-time
matching and/or fuzzy semantic matching of person names. If fuzzy
semantic matching of person names is supported, then the mechanism for
fuzzy semantic matching shall be specified.

An implementation that conforms to one of the SOP Classes of the Study
Root SOP Class Group as an SCP shall state in its Conformance Statement
whether it supports case-insensitive matching for PN VR Attributes and
list Attributes for which this applies.

An implementation that conforms to one of the SOP Classes of the Study
Root SOP Class Group as an SCP shall state in its Conformance Statement
how it makes use of Specific Character Set (0008,0005) and Timezone
Offset From UTC (0008,0201) when interpreting queries, performing
matching and encoding responses.

.. _sect_C.6.2.2.2.2:

C-MOVE SCP Conformance
                      

An implementation that conforms to one of the SOP Classes of the Study
Root SOP Class Group as an SCP shall support transfers against the
Query/Retrieve Information Model described in `Study Root Query/Retrieve
Information Model <#sect_C.6.2.1>`__ using the C-MOVE SCP Behavior
described in `C-MOVE SCP Behavior <#sect_C.4.2.3>`__.

An implementation that conforms to one of the SOP Classes of the Study
Root SOP Class Group as an SCP, which generates transfers using the
C-MOVE operation shall state in its Conformance Statement the Storage
Service Class SOP Classes under which it shall support the C-STORE
sub-operations generated by the C-MOVE.

.. _sect_C.6.2.2.2.3:

C-GET SCP Conformance
                     

An implementation that conforms to one of the SOP Classes of the Study
Root SOP Class Group as an SCP shall support retrievals against the
Query/Retrieve Information Model described in `Study Root Query/Retrieve
Information Model <#sect_C.6.2.1>`__ using the C-GET SCP Behavior
described in `C-GET SCP Behavior <#sect_C.4.3.3>`__.

An implementation that conforms to one of the SOP Classes of the Study
Root SOP Class Group as an SCP, which generates retrievals using the
C-GET operation shall state in its Conformance Statement the Storage
Service Class SOP Classes under which it shall support the C-STORE
sub-operations generated by the C-GET.

.. _sect_C.6.2.3:

SOP Classes
^^^^^^^^^^^

The SOP Classes in the Study Root SOP Class Group of the Query/Retrieve
Service Class identify the Study Root Query/Retrieve Information Model,
and the DIMSE-C operations supported. The Standard SOP Classes are
listed in `table_title <#table_C.6.2.3-1>`__.

.. table:: SOP Classes for Study Root Query/Retrieve

   +---------------------------------------+-----------------------------+
   | SOP Class Name                        | SOP Class UID               |
   +=======================================+=============================+
   | Study Root Query/Retrieve Information | 1.2.840.10008.5.1.4.1.2.2.1 |
   | Model - FIND                          |                             |
   +---------------------------------------+-----------------------------+
   | Study Root Query/Retrieve Information | 1.2.840.10008.5.1.4.1.2.2.2 |
   | Model - MOVE                          |                             |
   +---------------------------------------+-----------------------------+
   | Study Root Query/Retrieve Information | 1.2.840.10008.5.1.4.1.2.2.3 |
   | Model - GET                           |                             |
   +---------------------------------------+-----------------------------+

.. _sect_C.6.3:

Patient/Study Only SOP Class Group
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

Retired. See PS 3.4-2004.

