.. _chapter_Q:

Breast Imaging Report (Informative)
===================================

.. _sect_Q.1:

Breast Imaging Report Content Tree Structure
--------------------------------------------

The templates for the Breast Imaging Report are defined in .
Relationships defined in the Breast Imaging Report templates are
by-value. This template structure may be conveyed using the Enhanced SR
SOP Class or the Basic Text SR SOP Class.

As shown in `figure_title <#figure_Q.1-1>`__, the Breast Imaging Report
Narrative and Breast Imaging Report Supplementary Data sub-trees
together form the content tree of the Breast Imaging Report.

The Breast Imaging Procedure Reported sub-tree is a mandatory child of
the Supplementary Data content item, to describe all of the procedures
to which the report applies using coded terminology. It may also be used
as a sub-tree of sections within the Supplementary Data sub-tree, for
the instance in which a report covers more than one procedure, but
different sections of the Supplementary Data record the evidence of a
subset of the procedures.

An instance of the Breast Imaging Report Narrative sub-tree contains one
or more text-based report sections, with a name chosen from . Within a
report section, one or more observers may be identified. This sub-tree
is intended to contain the report text as it was created, presented to,
and signed off by the verifying observer. It is not intended to convey
the exact rendering of the report, such as formatting or visual
organization. Report text may reference one or more image or other
composite objects on which the interpretation was based.

An instance of the Breast Imaging Report Supplementary Data sub-tree
contains one or more of: Breast Imaging Procedure Reported, Breast
Composition Section, Breast Imaging Report Finding Section, Breast
Imaging Report Intervention Section, Overall Assessment. This sub-tree
is intended to contain the supporting evidence for the Breast Imaging
Report Narrative sub-tree, using coded terminology and numeric data.

The Breast Imaging Assessment sub-tree may be instantiated as the
content of an Overall Assessment section of a report (see
`figure_title <#figure_Q.1-4>`__), or as part of a Findings section of a
report (see ). Reports may provide an individual assessment for each
Finding, and then an overall assessment based on an aggregate of the
individual assessments.

.. _sect_Q.2:

Breast Imaging Report Examples
------------------------------

The following are simple illustrations of encoding Mammography procedure
based Breast Imaging Reports.

.. _sect_Q.2.1:

Example 1: Screening Mammogram With Negative Findings
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

A screening mammography case, i.e., there are typically four films and
no suspicious abnormalities. The result is a negative mammogram with
basic reporting. This example illustrates a report encoded as narrative
text only:

``Procedure reported``

``Film screen mammography, both breasts.``

``Reason for procedure``

``Screening``

``Findings``

``Comparison was made to exam from 11/14/2001. The breasts are heterogeneously dense. This may lower the sensitivity of mammography. No significant masses, calcifications, or other abnormalities are present. There is no significant change from the prior exam.``

``Impressions``

``BI-RADS® Category 1: Negative. Recommend normal interval follow-up in 12 months``

.. table:: Breast Image Report Content for Example 1

   +---------+-----------------------+-----------------------+---------+
   | Node    | Code Meaning of       | Code Meaning or       | TID/CID |
   |         | Concept Name          | Example Value         |         |
   +=========+=======================+=======================+=========+
   | 1       | Breast Imaging Report |                       |         |
   +---------+-----------------------+-----------------------+---------+
   | 1.1     | Language of Content   | English               |         |
   |         | Item and Descendants  |                       |         |
   +---------+-----------------------+-----------------------+---------+
   | 1.2     | Narrative Summary     |                       |         |
   +---------+-----------------------+-----------------------+---------+
   | 1.2.1   | Procedure reported    |                       |         |
   +---------+-----------------------+-----------------------+---------+
   | 1.2.1.1 | Procedure reported    | Film screen           |         |
   |         |                       | mammography, both     |         |
   |         |                       | breasts.              |         |
   +---------+-----------------------+-----------------------+---------+
   | 1.2.2   | Reason for procedure  |                       |         |
   +---------+-----------------------+-----------------------+---------+
   | 1.2.2.1 | Reason for procedure  | Screening             |         |
   +---------+-----------------------+-----------------------+---------+
   | 1.2.3   | Findings              |                       |         |
   +---------+-----------------------+-----------------------+---------+
   | 1.2.3.1 | Finding               | Comparison was made   |         |
   |         |                       | to exam from          |         |
   |         |                       | 11/14/2001. The       |         |
   |         |                       | breasts are           |         |
   |         |                       | heterogeneously       |         |
   |         |                       | dense. This may lower |         |
   |         |                       | the sensitivity of    |         |
   |         |                       | mammography. No       |         |
   |         |                       | significant masses,   |         |
   |         |                       | calcifications, or    |         |
   |         |                       | other abnormalities   |         |
   |         |                       | are present. There is |         |
   |         |                       | no significant change |         |
   |         |                       | from the prior exam.  |         |
   +---------+-----------------------+-----------------------+---------+
   | 1.2.4   | Impressions           |                       |         |
   +---------+-----------------------+-----------------------+---------+
   | 1.2.4.1 | Impression            | BI-RADS® Category 1:  |         |
   |         |                       | Negative. Recommend   |         |
   |         |                       | normal interval       |         |
   |         |                       | follow-up in 12       |         |
   |         |                       | months.               |         |
   +---------+-----------------------+-----------------------+---------+

.. _sect_Q.2.2:

Example 2: Screening Mammogram With Negative Findings
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

A screening mammography case, i.e., there are typically four films and
no suspicious abnormalities. The result is a negative mammogram with
basic reporting. This example illustrates a report encoded as narrative
text with minimal supplementary data, and follows BI-RADS® and MQSA:

``Procedure reported``

``Film screen mammography, both breasts.``

``Reason for procedure``

``Screening``

``Comparison to previous exams``

``Comparison was made to exam from 11/14/2001.``

``Breast composition``

``The breasts are heterogeneously dense. This may lower the sensitivity of mammography.``

``Findings``

``No significant masses, calcifications, or other abnormalities are present. There is no significant change from the prior exam.``

``Impressions``

``BI-RADS® Category 1: Negative. Recommend normal interval follow-up in 12 months.``

``Overall Assessment``

``Negative``

.. table:: Breast Imaging Report Content for Example 2

   +-----------+----------------------+----------------------+---------+
   | Node      | Code Meaning of      | Code Meaning or      | TID/CID |
   |           | Concept Name         | Example Value        |         |
   +===========+======================+======================+=========+
   | 1         | Breast Imaging       |                      |         |
   |           | Report               |                      |         |
   +-----------+----------------------+----------------------+---------+
   | 1.1       | Language of Content  | English              |         |
   |           | Item and Descendants |                      |         |
   +-----------+----------------------+----------------------+---------+
   | 1.2       | Narrative Summary    |                      |         |
   +-----------+----------------------+----------------------+---------+
   | 1.2.1     | Procedure reported   |                      |         |
   +-----------+----------------------+----------------------+---------+
   | 1.2.1.1   | Procedure reported   | Film screen          |         |
   |           |                      | mammography, both    |         |
   |           |                      | breasts.             |         |
   +-----------+----------------------+----------------------+---------+
   | 1.2.2     | Reason for procedure |                      |         |
   +-----------+----------------------+----------------------+---------+
   | 1.2.2.1   | Reason for procedure | Screening            |         |
   +-----------+----------------------+----------------------+---------+
   | 1.2.3     | Comparison to        |                      |         |
   |           | previous exams       |                      |         |
   +-----------+----------------------+----------------------+---------+
   | 1.2.3.1   | Comparison to        | Comparison was made  |         |
   |           | previous exams       | to exam from         |         |
   |           |                      | 11/14/2001.          |         |
   +-----------+----------------------+----------------------+---------+
   | 1.2.4     | Breast composition   |                      |         |
   +-----------+----------------------+----------------------+---------+
   | 1.2.4.1   | Breast composition   | The breasts are      |         |
   |           |                      | heterogeneously      |         |
   |           |                      | dense. This may      |         |
   |           |                      | lower the            |         |
   |           |                      | sensitivity of       |         |
   |           |                      | mammography.         |         |
   +-----------+----------------------+----------------------+---------+
   | 1.2.5     | Findings             |                      |         |
   +-----------+----------------------+----------------------+---------+
   | 1.2.5.1   | Finding              | No significant       |         |
   |           |                      | masses,              |         |
   |           |                      | calcifications, or   |         |
   |           |                      | other abnormalities  |         |
   |           |                      | are present. There   |         |
   |           |                      | is no significant    |         |
   |           |                      | change from the      |         |
   |           |                      | prior exam.          |         |
   +-----------+----------------------+----------------------+---------+
   | 1.2.6     | Impressions          |                      |         |
   +-----------+----------------------+----------------------+---------+
   | 1.2.6.1   | Impression           | BI-RADS® Category 1: |         |
   |           |                      | Negative. Recommend  |         |
   |           |                      | normal interval      |         |
   |           |                      | follow-up in 12      |         |
   |           |                      | months.              |         |
   +-----------+----------------------+----------------------+---------+
   | 1.2.7     | Overall Assessment   |                      |         |
   +-----------+----------------------+----------------------+---------+
   | 1.2.7.1   | Overall Assessment   | Negative             |         |
   +-----------+----------------------+----------------------+---------+
   | 1.3       | Supplementary Data   |                      |         |
   +-----------+----------------------+----------------------+---------+
   | 1.3.1     | Procedure reported   | Film Screen          |         |
   |           |                      | Mammography          |         |
   +-----------+----------------------+----------------------+---------+
   | 1.3.1.1   | Laterality           | Both breasts         |         |
   +-----------+----------------------+----------------------+---------+
   | 1.3.1.2   | Reason for procedure | Screening            |         |
   +-----------+----------------------+----------------------+---------+
   | 1.3.2     | Breast composition   |                      |         |
   +-----------+----------------------+----------------------+---------+
   | 1.3.2.1   | Breast composition   | Heterogeneously      |         |
   |           |                      | dense                |         |
   +-----------+----------------------+----------------------+---------+
   | 1.3.2.1.1 | Laterality           | Both breasts         |         |
   +-----------+----------------------+----------------------+---------+
   | 1.3.3     | Overall Assessment   |                      |         |
   +-----------+----------------------+----------------------+---------+
   | 1.3.3.1   | Assessment Category  | 1 - Negative         |         |
   +-----------+----------------------+----------------------+---------+
   | 1.3.3.2   | Recommended          | Normal interval      |         |
   |           | Follow-up            | follow-up            |         |
   +-----------+----------------------+----------------------+---------+

.. _sect_Q.2.3:

Example 3: Diagnostic Mammogram - Unilateral
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

A diagnostic mammogram was prompted by a clinical finding. The result is
a probably benign finding with a short interval follow-up of the left
breast. This report provides the narrative text with more extensive
supplementary data.

``Procedure reported``

``Film screen mammography, left breast.``

``Reason for procedure``

``Non-bloody discharge left breast.``

``Breast composition``

``The breast is almost entirely fat.``

``Findings``

``Film screen mammograms were performed. There are heterogeneous calcifications regionally distributed in the 1 o'clock upper outer quadrant, anterior region of the left breast. There is an increase in the number of calcifications from the prior exam.``

``Impressions``

``BI-RADS® Category 3: Probably Benign Finding. Short interval follow-up of the left breast is recommended in 6 months.``

.. table:: Breast Imaging Report Content for Example 3

   +-------------+---------------------+---------------------+---------+
   | Node        | Code Meaning of     | Code Meaning or     | TID/CID |
   |             | Concept Name        | Example Value       |         |
   +=============+=====================+=====================+=========+
   | 1           | Breast Imaging      |                     |         |
   |             | Report              |                     |         |
   +-------------+---------------------+---------------------+---------+
   | 1.1         | Language of Content | English             |         |
   |             | Item and            |                     |         |
   |             | Descendants         |                     |         |
   +-------------+---------------------+---------------------+---------+
   | 1.2         | Narrative Summary   |                     |         |
   +-------------+---------------------+---------------------+---------+
   | 1.2.1       | Procedure reported  |                     |         |
   +-------------+---------------------+---------------------+---------+
   | 1.2.1.1     | Procedure reported  | Film screen         |         |
   |             |                     | mammography, left   |         |
   |             |                     | breast.             |         |
   +-------------+---------------------+---------------------+---------+
   | 1.2.2       | Reason for          |                     |         |
   |             | procedure           |                     |         |
   +-------------+---------------------+---------------------+---------+
   | 1.2.2.1     | Reason for          | Non-bloody          |         |
   |             | procedure           | discharge left      |         |
   |             |                     | breast.             |         |
   +-------------+---------------------+---------------------+---------+
   | 1.2.3       | Breast composition  |                     |         |
   +-------------+---------------------+---------------------+---------+
   | 1.2.3.1     | Breast composition  | The breast is       |         |
   |             |                     | almost entirely     |         |
   |             |                     | fat.                |         |
   +-------------+---------------------+---------------------+---------+
   | 1.2.4       | Findings            |                     |         |
   +-------------+---------------------+---------------------+---------+
   | 1.2.4.1     | Finding             | Film screen         |         |
   |             |                     | mammograms were     |         |
   |             |                     | performed. There    |         |
   |             |                     | are heterogeneous   |         |
   |             |                     | calcifications      |         |
   |             |                     | regionally          |         |
   |             |                     | distributed in the  |         |
   |             |                     | 1 o'clock upper     |         |
   |             |                     | outer quadrant,     |         |
   |             |                     | anterior region of  |         |
   |             |                     | the left breast.    |         |
   |             |                     | There is an         |         |
   |             |                     | increase in the     |         |
   |             |                     | number of           |         |
   |             |                     | calcifications from |         |
   |             |                     | the prior exam.     |         |
   +-------------+---------------------+---------------------+---------+
   | 1.2.5       | Impressions         |                     |         |
   +-------------+---------------------+---------------------+---------+
   | 1.2.5.1     | Impression          | BI-RADS® Category   |         |
   |             |                     | 3: Probably Benign  |         |
   |             |                     | Finding. Short      |         |
   |             |                     | interval follow-up  |         |
   |             |                     | of the left breast  |         |
   |             |                     | is recommended in 6 |         |
   |             |                     | months.             |         |
   +-------------+---------------------+---------------------+---------+
   | 1.3         | Supplementary Data  |                     |         |
   +-------------+---------------------+---------------------+---------+
   | 1.3.1       | Procedure reported  | Film Screen         |         |
   |             |                     | Mammography         |         |
   +-------------+---------------------+---------------------+---------+
   | 1.3.1.1     | Laterality          | Left breast         |         |
   +-------------+---------------------+---------------------+---------+
   | 1.3.1.2     | Reason for          | Clinical Finding    |         |
   |             | procedure           |                     |         |
   +-------------+---------------------+---------------------+---------+
   | 1.3.1.2.1   | Clinical Finding    | Non-bloody          |         |
   |             |                     | discharge           |         |
   +-------------+---------------------+---------------------+---------+
   | 1.3.1.2.1.1 | Laterality          | Left breast         |         |
   +-------------+---------------------+---------------------+---------+
   | 1.3.2       | Breast composition  |                     |         |
   +-------------+---------------------+---------------------+---------+
   | 1.3.2.1     | Breast composition  | Almost entirely fat |         |
   +-------------+---------------------+---------------------+---------+
   | 1.3.2.1.1   | Laterality          | Left breast         |         |
   +-------------+---------------------+---------------------+---------+
   | 1.3.3       | Findings            |                     |         |
   +-------------+---------------------+---------------------+---------+
   | 1.3.3.1     | Finding             | Calcification of    |         |
   |             |                     | breast              |         |
   +-------------+---------------------+---------------------+---------+
   | 1.3.3.1.1   | Assessment Category | 3 - Probably Benign |         |
   |             |                     | Finding - short     |         |
   |             |                     | interval follow-up  |         |
   +-------------+---------------------+---------------------+---------+
   | 1.3.3.1.2   | Recommended         | Follow-up at short  |         |
   |             | Follow-up           | interval (1-11      |         |
   |             |                     | months)             |         |
   +-------------+---------------------+---------------------+---------+
   | 1.3.3.1.2.1 | Laterality          | Left breast         |         |
   +-------------+---------------------+---------------------+---------+
   | 1.3.3.1.2.2 | Recommended         | 6 months            |         |
   |             | Follow-up Interval  |                     |         |
   +-------------+---------------------+---------------------+---------+
   | 1.3.3.1.3   | Clockface or region | 1 o'clock position  |         |
   +-------------+---------------------+---------------------+---------+
   | 1.3.3.1.4   | Quadrant location   | Upper outer         |         |
   |             |                     | quadrant of breast  |         |
   +-------------+---------------------+---------------------+---------+
   | 1.3.3.1.5   | Depth               | Anterior            |         |
   +-------------+---------------------+---------------------+---------+
   | 1.3.3.1.6   | Calcification Type  | Heterogeneous       |         |
   |             |                     | calcification       |         |
   +-------------+---------------------+---------------------+---------+
   | 1.3.3.1.7   | Calcification       | Regional            |         |
   |             | Distribution        | calcification       |         |
   |             |                     | distribution        |         |
   +-------------+---------------------+---------------------+---------+
   | 1.3.3.1.8   | Change since last   | Increase in number  |         |
   |             | mammogram           | of calcifications   |         |
   +-------------+---------------------+---------------------+---------+

.. _sect_Q.2.4:

Example 4: Diagnostic Mammogram and Ultrasound - Unilateral
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

Following a screening mammogram, the patient was asked to return for
additional imaging and an ultrasound on the breast, for further
evaluation of a mammographic mass. This example demonstrates a report on
multiple breast imaging procedures. This report provides the narrative
text with some supplementary data.

``Procedure reported``

``Film screen mammography, left breast; Ultrasound procedure, left breast.``

``Reason for procedure``

``Additional evaluation requested at current screening.``

``Comparison to previous exams``

``Comparison was made to exam from 11/14/2001.``

``Findings``

``Film Screen Mammography: A lobular mass with obscured margins is present measuring 7mm in the upper outer quadrant.``

``Findings``

``Ultrasound demonstrates a simple cyst.``

``Impressions``

``BI-RADS® Category 2: Benign, no evidence of malignancy. Normal interval follow-up of both breasts is recommended in 12 months.``

``Overall Assessment``

``Benign``

.. table:: Breast Imaging Report Content for Example 4

   +-----------+----------------------+----------------------+---------+
   | Node      | Code Meaning of      | Code Meaning or      | TID/CID |
   |           | Concept Name         | Example Value        |         |
   +===========+======================+======================+=========+
   | 1         | Breast Imaging       |                      |         |
   |           | Report               |                      |         |
   +-----------+----------------------+----------------------+---------+
   | 1.1       | Language of Content  | English              |         |
   |           | Item and Descendants |                      |         |
   +-----------+----------------------+----------------------+---------+
   | 1.2       | Narrative Summary    |                      |         |
   +-----------+----------------------+----------------------+---------+
   | 1.2.1     | Procedure reported   |                      |         |
   +-----------+----------------------+----------------------+---------+
   | 1.2.1.1   | Procedure reported   | Film screen          |         |
   |           |                      | mammography, left    |         |
   |           |                      | breast; Ultrasound   |         |
   |           |                      | procedure, left      |         |
   |           |                      | breast.              |         |
   +-----------+----------------------+----------------------+---------+
   | 1.2.2     | Reason for procedure |                      |         |
   +-----------+----------------------+----------------------+---------+
   | 1.2.2.1   | Reason for procedure | Additional           |         |
   |           |                      | evaluation requested |         |
   |           |                      | at current           |         |
   |           |                      | screening.           |         |
   +-----------+----------------------+----------------------+---------+
   | 1.2.3     | Comparison to        |                      |         |
   |           | previous exams       |                      |         |
   +-----------+----------------------+----------------------+---------+
   | 1.2.3.1   | Comparison to        | Comparison was made  |         |
   |           | previous exams       | to exam from         |         |
   |           |                      | 11/14/2001.          |         |
   +-----------+----------------------+----------------------+---------+
   | 1.2.4     | Findings             |                      |         |
   +-----------+----------------------+----------------------+---------+
   | 1.2.4.1   | Finding              | Film Screen          |         |
   |           |                      | Mammography: A       |         |
   |           |                      | lobular mass with    |         |
   |           |                      | obscured margins is  |         |
   |           |                      | present measuring    |         |
   |           |                      | 7mm in the upper     |         |
   |           |                      | outer quadrant.      |         |
   +-----------+----------------------+----------------------+---------+
   | 1.2.5     | Findings             |                      |         |
   +-----------+----------------------+----------------------+---------+
   | 1.2.5.1   | Finding              | Ultrasound           |         |
   |           |                      | demonstrates a       |         |
   |           |                      | simple cyst.         |         |
   +-----------+----------------------+----------------------+---------+
   | 1.2.6     | Impressions          |                      |         |
   +-----------+----------------------+----------------------+---------+
   | 1.2.6.1   | Impression           | BI-RADS® Category 2: |         |
   |           |                      | Benign, no evidence  |         |
   |           |                      | of malignancy.       |         |
   |           |                      | Normal interval      |         |
   |           |                      | follow-up of both    |         |
   |           |                      | breasts is           |         |
   |           |                      | recommended in 12    |         |
   |           |                      | months.              |         |
   +-----------+----------------------+----------------------+---------+
   | 1.2.7     | Overall Assessment   |                      |         |
   +-----------+----------------------+----------------------+---------+
   | 1.2.7.1   | Overall Assessment   | Benign               |         |
   +-----------+----------------------+----------------------+---------+
   | 1.3       | Supplementary Data   |                      |         |
   +-----------+----------------------+----------------------+---------+
   | 1.3.1     | Procedure reported   | Film Screen          |         |
   |           |                      | Mammography          |         |
   +-----------+----------------------+----------------------+---------+
   | 1.3.1.1   | Laterality           | Left breast          |         |
   +-----------+----------------------+----------------------+---------+
   | 1.3.1.2   | Reason for procedure | Additional           |         |
   |           |                      | evaluation requested |         |
   |           |                      | at current screening |         |
   +-----------+----------------------+----------------------+---------+
   | 1.3.2     | Procedure reported   | Ultrasound procedure |         |
   +-----------+----------------------+----------------------+---------+
   | 1.3.2.1   | Laterality           | Left breast          |         |
   +-----------+----------------------+----------------------+---------+
   | 1.3.2.2   | Reason for procedure | Additional           |         |
   |           |                      | evaluation requested |         |
   |           |                      | at current screening |         |
   +-----------+----------------------+----------------------+---------+
   | 1.3.3     | Findings             |                      |         |
   +-----------+----------------------+----------------------+---------+
   | 1.3.3.1   | Procedure reported   | Film Screen          |         |
   |           |                      | Mammography          |         |
   +-----------+----------------------+----------------------+---------+
   | 1.3.3.1.1 | Laterality           | Left breast          |         |
   +-----------+----------------------+----------------------+---------+
   | 1.3.3.1.2 | Reason for procedure | Additional           |         |
   |           |                      | evaluation requested |         |
   |           |                      | at current screening |         |
   +-----------+----------------------+----------------------+---------+
   | 1.3.3.2   | Finding              | Mammographic breast  |         |
   |           |                      | mass                 |         |
   +-----------+----------------------+----------------------+---------+
   | 1.3.3.2.1 | Quadrant location    | Upper outer quadrant |         |
   |           |                      | of breast            |         |
   +-----------+----------------------+----------------------+---------+
   | 1.3.3.2.2 | Diameter             | 7 mm                 |         |
   +-----------+----------------------+----------------------+---------+
   | 1.3.3.2.3 | Shape                | Lobular              |         |
   +-----------+----------------------+----------------------+---------+
   | 1.3.3.2.4 | Margins              | Obscured lesion      |         |
   +-----------+----------------------+----------------------+---------+
   | 1.3.4     | Findings             |                      |         |
   +-----------+----------------------+----------------------+---------+
   | 1.3.4.1   | Procedure reported   | Ultrasound procedure |         |
   +-----------+----------------------+----------------------+---------+
   | 1.3.4.1.1 | Laterality           | Left breast          |         |
   +-----------+----------------------+----------------------+---------+
   | 1.3.4.1.2 | Reason for procedure | Additional           |         |
   |           |                      | evaluation requested |         |
   |           |                      | at current screening |         |
   +-----------+----------------------+----------------------+---------+
   | 1.3.4.2   | Finding              | Simple cyst of       |         |
   |           |                      | breast               |         |
   +-----------+----------------------+----------------------+---------+
   | 1.3.5     | Overall Assessment   |                      |         |
   +-----------+----------------------+----------------------+---------+
   | 1.3.5.1   | Assessment Category  | 2 - Benign Finding   |         |
   +-----------+----------------------+----------------------+---------+

