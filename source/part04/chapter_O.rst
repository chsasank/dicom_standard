.. _chapter_O:

Structured Reporting Storage SOP Classes (Normative)
====================================================

.. _sect_O.1:

Overview
--------

The Structured Reporting Storage SOP Classes extend the functionality of
the Storage Service class (defined in `Storage Service Class
(Normative) <#chapter_B>`__) to extend the SCP behavior and conformance
requirements.

.. _sect_O.2:

Structured Reporting Storage SOP Class SCU and SCP Behavior
-----------------------------------------------------------

.. _sect_O.2.1:

Behavior of an SCU
~~~~~~~~~~~~~~~~~~

.. _sect_O.2.1.1:

CAD SR SOP Classes
^^^^^^^^^^^^^^^^^^

Rendering Intent concept modifiers in the Mammography CAD SR, Chest CAD
SR and Colon CAD SR objects shall be consistent. Content items marked
"For Presentation" shall not be subordinate to content items marked "Not
for Presentation" or "Presentation Optional" in the content tree.
Similarly, content items marked "Presentation Optional" shall not be
subordinate to content items marked "Not for Presentation" in the
content tree.

Content items referenced from another SR object instance, such as a
prior Mammography CAD SR, Chest CAD SR or Colon CAD SR shall be inserted
by-value in the new SR object instance, with appropriate original source
observation context. It is necessary to update Rendering Intent, and
referenced content item identifiers for by-reference relationships,
within content items paraphrased from another source.

.. _sect_O.2.1.2:

Extensible SR SOP Class
^^^^^^^^^^^^^^^^^^^^^^^

The concept of extensibility implies that a recipient may encounter
Content Items, Value Types and Relationship Types that are unanticipated
and unsupported and hence potentially unrenderable.

An implementation shall identify in its Conformance Statement which
Content Items, Value Types and Relationship Types it creates.

.. _sect_O.2.2:

Behavior of an SCP
~~~~~~~~~~~~~~~~~~

An SCP intending to display or otherwise render a Structured Report
shall convey its full meaning in an unambiguous manner, except as
described in `Extensible SR SOP Class <#sect_O.2.2.2>`__.

.. note::

   "Full meaning" includes not just the Content Tree (i.e., the Items of
   the Content Sequence), but all Attributes of the Data Set that are
   necessary to properly interpret the Structured Report. This includes
   those Attributes that set the initial Observation Context for the
   Content Tree, i.e., the patient, procedure, and observer identifiers,
   and the Completion status and Verification status of the Structured
   Report.

An Icon Image in an IMAGE reference has no meaning, and is not required
to be rendered.

For a device, that is both an SCU and an SCP of these Storage SOP
Classes, in addition to the behavior for the Storage Service Class
specified in `Behavior of an SCP <#sect_B.2.2>`__, the following
additional requirements are specified for Structured Reporting Storage
SOP Classes:

-  an SCP of this SOP Class shall support Level 2 Conformance as defined
   in `Conformance as an SCP <#sect_B.4.1>`__.

.. note::

   This requirement means that all Type 1, Type 2, and Type 3 Attributes
   defined in the Information Object Definition associated with the SOP
   Class will be stored and may be accessed.

.. _sect_O.2.2.1:

CAD SR SOP Classes
^^^^^^^^^^^^^^^^^^

The Mammography CAD SR, Chest CAD SR and Colon CAD SR objects contain
data not only for presentation to the clinician, but also data solely
for use in subsequent mammography CAD analyses.

The SCU provides rendering guidelines via "Rendering Intent" concept
modifiers associated with "Individual Impression/Recommendation",
"Composite Feature" and "Single Image Finding" content items. The full
meaning of the SR is provided if all content items marked "Presentation
Required" are rendered down to the first instance of "Not for
Presentation" or "Presentation Optional" for each branch of the tree.
Use of the SCU's Conformance Statement is recommended if further
enhancement of the meaning of the SR can be accomplished by rendering
some or all of the data marked "Presentation Optional". Data marked "Not
for Presentation" should not be rendered by the SCP; it is embedded in
the SR content tree as input to subsequent CAD analysis work steps.

The SCP may further interpret whether or not to render a Single Image
Finding that has Rendering Intent "Presentation Optional" by
interpreting the value of the CAD Operating Point content item that is
subordinate to the Rendering Intent, if present. If the CAD Operating
Point content item is not present, then rendering of the Single Image
Finding may be based on recommendations in the creator's DICOM
Conformance Statement. For further information on the intended use of
CAD Operating Point see .

.. _sect_O.2.2.2:

Extensible SR SOP Class
^^^^^^^^^^^^^^^^^^^^^^^

The concept of extensibility implies that a recipient may encounter
Content Items, Value Types and Relationship Types that are unanticipated
and unsupported and hence potentially unrenderable.

An implementation shall identify in its Conformance Statement which
Content Items, Value Types and Relationship Types it supports.

Since it may not be possible to render the entire content in an
unambiguous manner because of unrecognized content, an SCP intending to
display or otherwise render an Extensible SR SOP Instance

-  shall convey a warning in the rendering to indicate that unsupported
   content is present and that this may affect the meaning of the
   rendering

-  shall identify in its Conformance Statement its behavior when
   encountering unsupported content

.. _sect_O.3:

Modification of SR Document Content
-----------------------------------

A device that is an SR Storage SOP Class SCU may modify information in a
SOP Instance that it has previously sent or received. When this SOP
Instance is modified and sent to an SCP, it shall be assigned a new SOP
Instance UID if any of the following conditions are met:

-  addition, removal or update of any Attribute within the SR Document
   General Module or SR Document Content Module;

-  modification of the Series Instance UID (0020,000E);

-  modification of the Study Instance UID (0020,000D).

.. _sect_O.4:

Conformance
-----------

In addition to the Conformance Statement requirements for the Storage
Service Class specified in `Conformance Statement
Requirements <#sect_B.4.3>`__, the following additional requirements are
specified for Structured Reporting Storage SOP Classes:

.. _sect_O.4.1:

Conformance Statement for an SCU
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

The following shall be documented in the Conformance Statement of any
implementation claiming conformance to the Structured Reporting Storage
SOP Classes as an SCU:

-  The Image or other composite object Storage SOP Classes that are also
   supported by the SCU and may be referenced by instances of Structured
   Reporting Storage SOP Class.

-  The range of Value Types and Relationship Types that are supported by
   the SCU.

-  The conditions under which a new SOP Instance UID is generated for an
   existing SR Document.

-  If the implementation provides Query/Retrieve of Structured Reporting
   SOP Instances as an SCU, whether it supports the Optional Keys
   Concept Name Code Sequence or Content Template Sequence.

.. note::

   The description of the Value Types and Relationship Types that are
   supported by the SCU is particularly important for the Extensible SR
   SOP Class.

.. _sect_O.4.1.1:

CAD SR SOP Classes
^^^^^^^^^^^^^^^^^^

The following shall be documented in the Conformance Statement of any
implementation claiming conformance to the Mammography CAD SR SOP Class
as an SCU:

-  Which types of detections and/or analyses the device is capable of
   performing:

   -  From detections listed in Context Group 6014 Mammography Single
      Image Finding

   -  From analyses listed in Context Group 6043 Types of Mammography
      CAD Analysis

The following shall be documented in the Conformance Statement of any
implementation claiming conformance to the Chest CAD SR SOP Class as an
SCU:

-  Which types of detections and/or analyses the device is capable of
   performing:

   -  From detections listed in Context ID 6101 Chest Finding or
      Feature, or Context ID 6102 Chest Finding or Feature Modifier

   -  From analyses listed in Context ID 6137 Types of CAD Analysis

The following shall be documented in the Conformance Statement of any
implementation claiming conformance to the Colon CAD SR SOP Class as an
SCU:

-  Which types of detections and/or analyses the device is capable of
   performing:

   -  From detections listed in Context ID 6201 Colon Finding or Feature

   -  From analyses listed in Context ID 6137 Types of CAD Analysis

The following shall be documented in the Conformance Statement of any
implementation claiming conformance to the Mammography CAD SR, Chest CAD
SR or Colon CAD SR SOP Classes as an SCU that creates instances:

-  Which optional content items are supported

-  Conditions under which content items are assigned Rendering Intent of
   "Presentation Optional", and whether a CAD Operating Point value will
   be included with each Single Image Finding that has Rendering Intent
   of "Presentation Optional"

-  Recommendations for the conditions under which content items with
   Rendering Intent of "Presentation Optional" should be rendered, based
   on CAD Operating Point or otherwise

-  Conditions under which content items are assigned Rendering Intent of
   "Not for Presentation"

.. _sect_O.4.1.2:

Ultrasound SR SOP Classes
^^^^^^^^^^^^^^^^^^^^^^^^^

The following shall be documented in the Conformance Statement of any SR
creator implementation claiming conformance to the Simplified Adult Echo
SR SOP Class as an SCU:

-  A list of all the measurement codes from supported by the device for
   use in .

-  A list of initial measurement codes supported by the device for use
   in Row 1 or 2 of .

   -  Optionally, a table of the post-coordinated modifer values
      associated with each measurement code.

-  A list of any extension codes added to , , , , .

.. _sect_O.4.2:

Conformance Statement for an SCP
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

The following shall be documented in the Conformance Statement of any
implementation claiming conformance to the Structured Reporting Storage
SOP Class as an SCP:

-  For an SCP of a Structured Reporting Storage SOP Class that is
   displaying or otherwise rendering the structured report contained in
   a SOP Instance of the Class, the general form in which the structured
   report related Attributes are rendered.

-  For an SCP of a Structured Reporting Storage SOP Class, the Image or
   other composite object Storage SOP Classes that are also supported by
   the SCP and may be referenced by instances of the Structured
   Reporting Storage SOP Class, and whether or not they will be
   displayed or otherwise rendered.

-  For an SCP of a Structured Reporting Storage SOP Class that is
   displaying or otherwise rendering an image or other composite object
   referred to by a SOP Instance of the Class, the manner in which the
   structured report related Attributes (such as spatial coordinates and
   referenced presentation states) are used to influence the display of
   the image or object.

-  If the implementation supports Query/Retrieve of Structured Reporting
   SOP Instances as an SCP, whether it supports the Optional Keys
   Concept Name Code Sequence or Content Template Sequence.

.. _sect_O.4.2.1:

CAD SR SOP Classes
^^^^^^^^^^^^^^^^^^

The following shall be documented in the Conformance Statement of any
implementation claiming conformance to the Mammography CAD SR, Chest CAD
SR or Colon CAD SR SOP Classes as an SCP:

-  Conditions under which the SCP will render content items with
   Rendering Intent concept modifier set to "Presentation Optional"

.. _sect_O.4.2.2:

Extensible SR SOP Class
^^^^^^^^^^^^^^^^^^^^^^^

The following shall be documented in the Conformance Statement of any
implementation claiming conformance to the Extensible SR SOP Class as an
SCP:

-  The behavior and warnings generated when encountering unsupported
   Content Items, Value Types and Relationship Types

