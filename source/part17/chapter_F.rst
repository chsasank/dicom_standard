.. _chapter_F:

Chest CAD (Informative)
=======================

This Annex was formerly located in in the 2003 and earlier revisions of
the Standard.

.. _sect_F.1:

Chest CAD SR Content Tree Structure
-----------------------------------

The templates for the Chest CAD SR IOD are defined in . Relationships
defined in the Chest CAD SR IOD templates are by-value, unless otherwise
stated. Content items referenced from another SR object instance, such
as a prior Chest CAD SR, are inserted by-value in the new SR object
instance, with appropriate original source observation context. It is
necessary to update Rendering Intent, and referenced content item
identifiers for by-reference relationships, within content items
paraphrased from another source.

The Document Root, Image Library, CAD Processing and Findings Summary,
and Summaries of Detections and Analyses sub-trees together form the
content tree of the Chest CAD SR IOD. See `Mammography CAD
(Informative) <#chapter_E>`__ for additional explanation of the
Summaries of Detections and Analyses sub-trees.

The shaded area in `figure_title <#figure_F.1-2>`__ demarcates
information resulting from Detection, whereas the unshaded area is
information resulting from Analysis. This distinction is used in
determining whether to place algorithm identification information in the
Summary of Detections or Summary of Analyses sub-trees.

The identification of a lung nodule within a single image is considered
to be a Detection, which results in a Single Image Finding. The temporal
correlation of a lung nodule in two instances of the same view taken at
different times, resulting in a Composite Feature, is considered
Analysis.

Once a Single Image Finding or Composite Feature has been instantiated,
it may be referenced by any number of Composite Features higher in the
CAD Processing and Findings Summary sub-tree.

.. _sect_F.2:

Chest CAD SR Observation Context Encoding
-----------------------------------------

-  Any content item in the Content tree that has been inserted (i.e.,
   duplicated) from another SR object instance has a HAS OBS CONTEXT
   relationship to one or more content items that describe the context
   of the SR object instance from which it originated. This mechanism
   may be used to combine reports (e.g., Chest CAD SR 1, Chest CAD SR 2,
   Human).

-  By-reference relationships within Single Image Findings and Composite
   Features paraphrased from prior Chest CAD SR objects need to be
   updated to properly reference Image Library Entries carried from the
   prior object to their new positions in the present object.

The CAD Processing and Findings Summary section of the SR Document
Content tree of a Chest CAD SR IOD may contain a mixture of current and
prior single image findings and composite features. The content items
from current and prior contexts are target content items that have a
by-value INFERRED FROM relationship to a Composite Feature content item.
Content items that come from a context other than the Initial
Observation Context have a HAS OBS CONTEXT relationship to target
content items that describe the context of the source document.

In `figure_title <#figure_F.2-1>`__, Composite Feature and Single Image
Finding are current, and Single Image Finding (from Prior) is duplicated
from a prior document.

.. _sect_F.3:

Chest CAD SR Examples
---------------------

The following is a simple and non-comprehensive illustration of an
encoding of the Chest CAD SR IOD for chest computer aided detection
results. For brevity, some mandatory content items are not included,
such as several acquisition context content items for the images in the
Image Library.

.. _sect_F.3.1:

Example 1: Lung Nodule Detection With No Findings
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

A chest CAD device processes a typical screening chest case, i.e., there
is one image and no nodule findings. Chest CAD runs lung nodule
detection successfully and finds nothing.

The chest radiograph resembles:

The content tree structure would resemble:

+-----------+------------------------+------------------------+-----+
| Node      | Code Meaning of        | Code Meaning or        | TID |
|           | Concept Name           | Example Value          |     |
+===========+========================+========================+=====+
| 1         | Chest CAD Report       |                        |     |
+-----------+------------------------+------------------------+-----+
| 1.1       | Image Library          |                        |     |
+-----------+------------------------+------------------------+-----+
| 1.1.1     |                        | IMAGE 1                |     |
+-----------+------------------------+------------------------+-----+
| 1.1.1.1   | Image View             | Postero-anterior       |     |
+-----------+------------------------+------------------------+-----+
| 1.1.1.2   | Study Date             | 19980101               |     |
+-----------+------------------------+------------------------+-----+
| 1.2       | CAD Processing and     | All algorithms         |     |
|           | Findings Summary       | succeeded; without     |     |
|           |                        | findings               |     |
+-----------+------------------------+------------------------+-----+
| 1.3       | Summary of Detections  | Succeeded              |     |
+-----------+------------------------+------------------------+-----+
| 1.3.1     | Successful Detections  |                        |     |
+-----------+------------------------+------------------------+-----+
| 1.3.1.1   | Detection Performed    | Nodule                 |     |
+-----------+------------------------+------------------------+-----+
| 1.3.1.1.1 | Algorithm Name         | "Lung Nodule Detector" |     |
+-----------+------------------------+------------------------+-----+
| 1.3.1.1.2 | Algorithm Version      | "V1.3"                 |     |
+-----------+------------------------+------------------------+-----+
| 1.3.1.1.3 |                        | Reference to node      |     |
|           |                        | 1.1.1                  |     |
+-----------+------------------------+------------------------+-----+
| 1.4       | Summary of Analyses    | Not Attempted          |     |
+-----------+------------------------+------------------------+-----+

.. _sect_F.3.2:

Example 2: Lung Nodule Detection With Findings and Anatomy/pathology Interpretation
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

A chest CAD device processes a screening chest case with one image, and
a lung nodule detected. The chest radiograph resembles:

The content tree structure in this example is complex. Structural
illustrations of portions of the content tree are placed within the
content tree table to show the relationships of data within the tree.
Some content items are duplicated (and shown in boldface) to facilitate
use of the diagrams.

The content tree structure would resemble:

+---------+-------------------------+-------------------------+-----+
| Node    | Code Meaning of Concept | Code Meaning or Example | TID |
|         | Name                    | Value                   |     |
+=========+=========================+=========================+=====+
| 1       | Chest CAD Report        |                         |     |
+---------+-------------------------+-------------------------+-----+
| **1.1** | Image Library           |                         |     |
+---------+-------------------------+-------------------------+-----+
| **1.2** | CAD Processing and      | All algorithms          |     |
|         | Findings Summary        | succeeded; with         |     |
|         |                         | findings                |     |
+---------+-------------------------+-------------------------+-----+
| **1.3** | Summary of Detections   | Succeeded               |     |
+---------+-------------------------+-------------------------+-----+
| 1.4     | Summary of Analyses     | Not Attempted           |     |
+---------+-------------------------+-------------------------+-----+

======= ============================ ============================= ===
Node    Code Meaning of Concept Name Code Meaning or Example Value TID
======= ============================ ============================= ===
1.1     Image Library                                              
1.1.1                                IMAGE 1                       
1.1.1.1 Image View                   Postero-anterior              
1.1.1.2 Study Date                   19990101                      
======= ============================ ============================= ===

+-------------+-----------------------+-----------------------+-----+
| Node        | Code Meaning of       | Code Meaning or       | TID |
|             | Concept Name          | Example Value         |     |
+=============+=======================+=======================+=====+
| 1.2         | CAD Processing and    | All algorithms        |     |
|             | Findings Summary      | succeeded; with       |     |
|             |                       | findings              |     |
+-------------+-----------------------+-----------------------+-----+
| 1.2.1       | Single Image Finding  | Abnormal Opacity      |     |
+-------------+-----------------------+-----------------------+-----+
| 1.2.1.1     | Single Image Finding  | Nodule                |     |
|             | Modifier              |                       |     |
+-------------+-----------------------+-----------------------+-----+
| 1.2.1.2     | Rendering Intent      | Presentation          |     |
|             |                       | Required:…            |     |
+-------------+-----------------------+-----------------------+-----+
| 1.2.1.3     | Algorithm Name        | "Lung Nodule          |     |
|             |                       | Detector"             |     |
+-------------+-----------------------+-----------------------+-----+
| 1.2.1.4     | Algorithm Version     | "V1.3"                |     |
+-------------+-----------------------+-----------------------+-----+
| 1.2.1.5     | Center                | POINT                 |     |
+-------------+-----------------------+-----------------------+-----+
| 1.2.1.5.1   |                       | Reference to Node     |     |
|             |                       | 1.1.1                 |     |
+-------------+-----------------------+-----------------------+-----+
| 1.2.1.6     | Outline               | POLYLINE              |     |
+-------------+-----------------------+-----------------------+-----+
| 1.2.1.6.1   |                       | Reference to Node     |     |
|             |                       | 1.1.1                 |     |
+-------------+-----------------------+-----------------------+-----+
| 1.2.1.7     | Diameter              | 2 cm                  |     |
+-------------+-----------------------+-----------------------+-----+
| 1.2.1.7.1   | Path                  | POLYLINE              |     |
+-------------+-----------------------+-----------------------+-----+
| 1.2.1.7.1.1 |                       | Reference to Node     |     |
|             |                       | 1.1.1                 |     |
+-------------+-----------------------+-----------------------+-----+

========= ============================ ============================= ===
Node      Code Meaning of Concept Name Code Meaning or Example Value TID
========= ============================ ============================= ===
1.3       Summary of Detections        Succeeded                     
1.3.1     Successful Detections                                      
1.3.1.1   Detection Performed          Nodule                        
1.3.1.1.1 Algorithm Name               "Lung Nodule Detector"        
1.3.1.1.2 Algorithm Version            "V1.3"                        
1.3.1.1.3                              Reference to node 1.1.1       
========= ============================ ============================= ===

.. _sect_F.3.3:

Example 3: Lung Nodule Detection, Temporal Differencing With Findings
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

The patient in Example 2 returns for another chest radiograph. A more
comprehensive chest CAD device processes the current chest radiograph,
and analyses are performed that determine some temporally related
content items for Composite Features. Portions of the prior chest CAD
report (Example 2) are incorporated into this report. In the current
chest radiograph the lung nodule has increased in size.

Italicized entries (*xxx*) in the following table denote references to
or by-value inclusion of content tree items reused from the prior Chest
CAD SR instance (Example 2).

==== ============================ ============================= ===
Node Code Meaning of Concept Name Code Meaning or Example Value TID
==== ============================ ============================= ===
1    Chest CAD Report                                           
==== ============================ ============================= ===

While the Image Library contains references to content tree items reused
from the prior Chest CAD SR instance, the images are actually used in
the chest CAD analysis and are therefore not italicized as indicated
above.

======= ============================ ============================= ===
Node    Code Meaning of Concept Name Code Meaning or Example Value TID
======= ============================ ============================= ===
1.1     Image Library                                              
1.1.1                                IMAGE 1                       
1.1.1.1 Image View                   Postero-anterior              
1.1.1.2 Study Date                   20000101                      
1.1.2                                IMAGE 2                       
1.1.2.1 Image View                   Postero-anterior              
1.1.2.2 Study Date                   19990101                      
======= ============================ ============================= ===

The CAD processing and findings consist of one composite feature,
comprised of single image findings, one from each year. The temporal
relationship allows a quantitative temporal difference to be calculated:

+------------------+-------------------+-------------------+-----+
| Node             | Code Meaning of   | Code Meaning or   | TID |
|                  | Concept Name      | Example Value     |     |
+==================+===================+===================+=====+
| 1.2              | CAD Processing    | All algorithms    |     |
|                  | and Findings      | succeeded; with   |     |
|                  | Summary           | findings          |     |
+------------------+-------------------+-------------------+-----+
| 1.2.1            | Composite Feature | Abnormal Opacity  |     |
+------------------+-------------------+-------------------+-----+
| 1.2.1.1          | Composite Feature | Nodule            |     |
|                  | Modifier          |                   |     |
+------------------+-------------------+-------------------+-----+
| 1.2.1.2          | Rendering Intent  | Presentation      |     |
|                  |                   | Required: …       |     |
+------------------+-------------------+-------------------+-----+
| 1.2.1.3          | Algorithm Name    | "Nodule Change"   |     |
+------------------+-------------------+-------------------+-----+
| 1.2.1.4          | Algorithm Version | "V2.3"            |     |
+------------------+-------------------+-------------------+-----+
| 1.2.1.5          | Composite Type    | Target content    |     |
|                  |                   | items are related |     |
|                  |                   | temporally        |     |
+------------------+-------------------+-------------------+-----+
| 1.2.1.6          | Scope of Feature  | Feature detected  |     |
|                  |                   | on multiple       |     |
|                  |                   | images            |     |
+------------------+-------------------+-------------------+-----+
| 1.2.1.7          | Certainty of      | 85%               |     |
|                  | Feature           |                   |     |
+------------------+-------------------+-------------------+-----+
| 1.2.1.8          | Difference in     | 2 cm              |     |
|                  | size              |                   |     |
+------------------+-------------------+-------------------+-----+
| 1.2.1.8.1        |                   | Reference to Node |     |
|                  |                   | 1.2.1.9.8         |     |
+------------------+-------------------+-------------------+-----+
| 1.2.1.8.2        |                   | Reference to Node |     |
|                  |                   | *1.2.1.10.8*      |     |
+------------------+-------------------+-------------------+-----+
| 1.2.1.9          | Single Image      | Abnormal Opacity  |     |
|                  | Finding           |                   |     |
+------------------+-------------------+-------------------+-----+
| 1.2.1.9.1        | Single Image      | Nodule            |     |
|                  | Finding Modifier  |                   |     |
+------------------+-------------------+-------------------+-----+
| 1.2.1.9.2        | Rendering Intent  | Presentation      |     |
|                  |                   | Required: …       |     |
+------------------+-------------------+-------------------+-----+
| 1.2.1.9.3        | Tracking          | "Watchlist #1"    |     |
|                  | Identifier        |                   |     |
+------------------+-------------------+-------------------+-----+
| 1.2.1.9.4        | Algorithm Name    | "Lung Nodule      |     |
|                  |                   | Detector"         |     |
+------------------+-------------------+-------------------+-----+
| 1.2.1.9.5        | Algorithm Version | "V1.3"            |     |
+------------------+-------------------+-------------------+-----+
| 1.2.1.9.6        | Center            | POINT             |     |
+------------------+-------------------+-------------------+-----+
| 1.2.1.9.6.1      |                   | Reference to Node |     |
|                  |                   | 1.1.1             |     |
+------------------+-------------------+-------------------+-----+
| 1.2.1.9.7        | Outline           | POLYLINE          |     |
+------------------+-------------------+-------------------+-----+
| 1.2.1.9.7.1      |                   | Reference to Node |     |
|                  |                   | 1.1.1             |     |
+------------------+-------------------+-------------------+-----+
| 1.2.1.9.8        | Diameter          | 4 cm              |     |
+------------------+-------------------+-------------------+-----+
| 1.2.1.9.8.1      | Path              | POLYLINE          |     |
+------------------+-------------------+-------------------+-----+
| 1.2.1.9.8.1.1    |                   | Reference to Node |     |
|                  |                   | 1.1.1             |     |
+------------------+-------------------+-------------------+-----+
| *1.2.1.10*       | Single Image      | Abnormal Opacity  |     |
|                  | Finding           |                   |     |
+------------------+-------------------+-------------------+-----+
| *1.2.1.10.1*     | Single Image      | Nodule            |     |
|                  | Finding Modifier  |                   |     |
+------------------+-------------------+-------------------+-----+
| *1.2.1.10.2*     | Rendering Intent  | Presentation      |     |
|                  |                   | Required: …       |     |
+------------------+-------------------+-------------------+-----+
| *1.2.1.10.3*     | [Observation      |                   |     |
|                  | Context content   |                   |     |
|                  | items]            |                   |     |
+------------------+-------------------+-------------------+-----+
| *1.2.1.10.4*     | Algorithm Name    | "Lung Nodule      |     |
|                  |                   | Detector"         |     |
+------------------+-------------------+-------------------+-----+
| *1.2.1.10.5*     | Algorithm Version | "V1.3"            |     |
+------------------+-------------------+-------------------+-----+
| *1.2.1.10.6*     | Center            | POINT             |     |
+------------------+-------------------+-------------------+-----+
| *1.2.1.10.6.1*   |                   | Reference to Node |     |
|                  |                   | 1.1.2             |     |
+------------------+-------------------+-------------------+-----+
| *1.2.1.10.7*     | Outline           | POLYLINE          |     |
+------------------+-------------------+-------------------+-----+
| *1.2.1.10.7.1*   |                   | Reference to Node |     |
|                  |                   | 1.1.2             |     |
+------------------+-------------------+-------------------+-----+
| *1.2.1.10.8*     | Diameter          | 2 cm              |     |
+------------------+-------------------+-------------------+-----+
| *1.2.1.10.8.1*   | Path              | POLYLINE          |     |
+------------------+-------------------+-------------------+-----+
| *1.2.1.10.8.1.1* |                   | Reference to Node |     |
|                  |                   | 1.1.2             |     |
+------------------+-------------------+-------------------+-----+
| 1.3              | Summary of        | Succeeded         |     |
|                  | Detections        |                   |     |
+------------------+-------------------+-------------------+-----+
| 1.3.1            | Successful        |                   |     |
|                  | Detections        |                   |     |
+------------------+-------------------+-------------------+-----+
| 1.3.1.1          | Detection         | Nodule            |     |
|                  | Performed         |                   |     |
+------------------+-------------------+-------------------+-----+
| 1.3.1.1.1        | Algorithm Name    | "Lung Nodule      |     |
|                  |                   | Detector"         |     |
+------------------+-------------------+-------------------+-----+
| 1.3.1.1.2        | Algorithm Version | "V1.3"            |     |
+------------------+-------------------+-------------------+-----+
| 1.3.1.1.3        |                   | Reference to node |     |
|                  |                   | 1.1.1             |     |
+------------------+-------------------+-------------------+-----+
| 1.4              | Summary of        | Succeeded         |     |
|                  | Analyses          |                   |     |
+------------------+-------------------+-------------------+-----+
| 1.4.1            | Successful        |                   |     |
|                  | Analyses          |                   |     |
+------------------+-------------------+-------------------+-----+
| 1.4.1.1          | Analysis          | "Temporal         |     |
|                  | Performed         | correlation"      |     |
+------------------+-------------------+-------------------+-----+
| 1.4.1.1.1        | Algorithm Name    | "Nodule Change"   |     |
+------------------+-------------------+-------------------+-----+
| 1.4.1.1.2        | Algorithm Version | "V2.3"            |     |
+------------------+-------------------+-------------------+-----+
| 1.4.1.1.3        |                   | Reference to node |     |
|                  |                   | 1.1.1             |     |
+------------------+-------------------+-------------------+-----+
| 1.4.1.1.4        |                   | Reference to node |     |
|                  |                   | 1.1.2             |     |
+------------------+-------------------+-------------------+-----+

.. _sect_F.3.4:

Example 4: Lung Nodule Detection in Chest Radiograph, Spatially Correlated With CT
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

The patient in Example 3 is called back for CT to confirm the Lung
Nodule found in Example 3. The patient undergoes CT of the Thorax and
the initial chest radiograph and CT slices are sent to a more
comprehensive CAD device for processing. Findings are detected and
analyses are performed that correlate findings from the two collections
of data. Portions of the prior CAD report (Example 3) are incorporated
into this report.

Italicized entries (*xxx*) in the following table denote references to
or by-value inclusion of content tree items reused from the prior Chest
CAD SR instance (Example 3).

+---------+-------------------------+-------------------------+-----+
| Node    | Code Meaning of Concept | Code Meaning of Example | TID |
|         | Name                    | Value                   |     |
+=========+=========================+=========================+=====+
| 1       | Chest CAD Report        |                         |     |
+---------+-------------------------+-------------------------+-----+
| 1.1     | Language of Content     | English                 |     |
|         | Item and Descendants    |                         |     |
+---------+-------------------------+-------------------------+-----+
| **1.2** | Image Library           |                         |     |
+---------+-------------------------+-------------------------+-----+
| **1.3** | CAD Processing and      | All algorithms          |     |
|         | Findings Summary        | succeeded; with         |     |
|         |                         | findings                |     |
+---------+-------------------------+-------------------------+-----+
| **1.4** | Summary of Detections   | Succeeded               |     |
+---------+-------------------------+-------------------------+-----+
| **1.5** | Summary of Analyses     | Succeeded               |     |
+---------+-------------------------+-------------------------+-----+

While the Image Library contains references to content tree items reused
from the prior Chest CAD SR instance, the images are actually used in
the CAD analysis and are therefore not italicized as indicated above.

======= ============================ ============================= ===
Node    Code Meaning of Concept Name Code Meaning of Example Value TID
======= ============================ ============================= ===
1.2     Image Library                                              
1.2.1                                IMAGE 1                       
1.2.1.1 Image View                   Postero-anterior              
1.2.1.2 Study Date                   20000101                      
======= ============================ ============================= ===

Most recent examination content:

+-----------+------------------------+------------------------+-----+
| Node      | Code Meaning of        | Code Meaning of        | TID |
|           | Concept Name           | Example Value          |     |
+===========+========================+========================+=====+
| 1.3       | CAD Processing and     | All algorithms         |     |
|           | Findings Summary       | succeeded; with        |     |
|           |                        | findings               |     |
+-----------+------------------------+------------------------+-----+
| **1.3.1** | Composite Feature      | Abnormal opacity       |     |
+-----------+------------------------+------------------------+-----+

+--------------+----------------------+----------------------+-----+
| Node         | Code Meaning of      | Code Meaning of      | TID |
|              | Concept Name         | Example Value        |     |
+==============+======================+======================+=====+
| 1.3.1        | Composite Feature    | Abnormal opacity     |     |
+--------------+----------------------+----------------------+-----+
| 1.3.1.1      | Composite Feature    | Nodule               |     |
|              | Modifier             |                      |     |
+--------------+----------------------+----------------------+-----+
| 1.3.1.2      | Rendering Intent     | Presentation         |     |
|              |                      | Required: …          |     |
+--------------+----------------------+----------------------+-----+
| 1.3.1.3      | Tracking Identifier  | "Watchlist #1"       |     |
+--------------+----------------------+----------------------+-----+
| 1.3.1.4      | Algorithm Name       | "Chest/CT            |     |
|              |                      | Correlator"          |     |
+--------------+----------------------+----------------------+-----+
| 1.3.1.5      | Algorithm Version    | "V2.1"               |     |
+--------------+----------------------+----------------------+-----+
| 1.3.1.6      | Composite type       | Target content items |     |
|              |                      | are related          |     |
|              |                      | spatially            |     |
+--------------+----------------------+----------------------+-----+
| 1.3.1.7      | Scope of Feature     | Feature detected on  |     |
|              |                      | images from multiple |     |
|              |                      | modalities           |     |
+--------------+----------------------+----------------------+-----+
| 1.3.1.8      | Diameter             | 4 cm                 |     |
+--------------+----------------------+----------------------+-----+
| 1.3.1.8.1    | Path                 |                      |     |
+--------------+----------------------+----------------------+-----+
| 1.3.1.8.1.1  |                      | IMAGE 3 [CT slice    |     |
|              |                      | 104]                 |     |
+--------------+----------------------+----------------------+-----+
| 1.3.1.9      | Volume estimated     | 3.2 cm3              |     |
|              | from single 2D       |                      |     |
|              | region               |                      |     |
+--------------+----------------------+----------------------+-----+
| 1.3.1.9.1    | Perimeter Outline    |                      |     |
+--------------+----------------------+----------------------+-----+
| 1.3.1.9.1.1  |                      | IMAGE 3 [CT slice    |     |
|              |                      | 104]                 |     |
+--------------+----------------------+----------------------+-----+
| 1.3.1.10     | Size Descriptor      | Small                |     |
+--------------+----------------------+----------------------+-----+
| 1.3.1.11     | Border Shape         | Lobulated            |     |
+--------------+----------------------+----------------------+-----+
| 1.3.1.12     | Location in Chest    | Mid lobe             |     |
+--------------+----------------------+----------------------+-----+
| 1.3.1.13     | Laterality           | Right                |     |
+--------------+----------------------+----------------------+-----+
| **1.3.1.14** | Composite Feature    | Abnormal opacity     |     |
+--------------+----------------------+----------------------+-----+
| **1.3.1.15** | Single Image Finding | Abnormal opacity     |     |
+--------------+----------------------+----------------------+-----+

+-----------------+-------------------+-------------------+-----+
| Node            | Code Meaning of   | Code Meaning of   | TID |
|                 | Concept Name      | Example Value     |     |
+=================+===================+===================+=====+
| 1.3.1.14        | Composite Feature | Abnormal opacity  |     |
+-----------------+-------------------+-------------------+-----+
| 1.3.1.14.1      | Composite Feature | Nodule            |     |
|                 | Modifier          |                   |     |
+-----------------+-------------------+-------------------+-----+
| 1.3.1.14.2      | Rendering Intent  | Presentation      |     |
|                 |                   | Required: …       |     |
+-----------------+-------------------+-------------------+-----+
| 1.3.1.14.3      | Tracking          | "Nodule #1"       |     |
|                 | Identifier        |                   |     |
+-----------------+-------------------+-------------------+-----+
| 1.3.1.14.4      | Algorithm Name    | "Nodule Builder"  |     |
+-----------------+-------------------+-------------------+-----+
| 1.3.1.14.5      | Algorithm Version | "V1.4"            |     |
+-----------------+-------------------+-------------------+-----+
| 1.3.1.14.6      | Composite type    | Target content    |     |
|                 |                   | items are related |     |
|                 |                   | spatially         |     |
+-----------------+-------------------+-------------------+-----+
| 1.3.1.14.7      | Scope of Feature  | Feature detected  |     |
|                 |                   | on multiple       |     |
|                 |                   | images            |     |
+-----------------+-------------------+-------------------+-----+
| 1.3.1.14.8      | Diameter          | 4 cm              |     |
+-----------------+-------------------+-------------------+-----+
| 1.3.1.14.9      | Volume estimated  | 3.2 cm3           |     |
|                 | from single 2D    |                   |     |
|                 | region            |                   |     |
+-----------------+-------------------+-------------------+-----+
| **1.3.1.14.10** | Single Image      | Abnormal opacity  |     |
|                 | Finding           |                   |     |
+-----------------+-------------------+-------------------+-----+
| **1.3.1.14.11** | Single Image      | Abnormal opacity  |     |
|                 | Finding           |                   |     |
+-----------------+-------------------+-------------------+-----+
| **1.3.1.14.12** | Single Image      | Abnormal opacity  |     |
|                 | Finding           |                   |     |
+-----------------+-------------------+-------------------+-----+

+-----------------+-------------------+-------------------+-----+
| Node            | Code Meaning of   | Code Meaning of   | TID |
|                 | Concept Name      | Example Value     |     |
+=================+===================+===================+=====+
| 1.3.1.14.10     | Single Image      | Abnormal opacity  |     |
|                 | Finding           |                   |     |
+-----------------+-------------------+-------------------+-----+
| 1.3.1.14.10.1   | Single Image      | Nodule            |     |
|                 | Finding Modifier  |                   |     |
+-----------------+-------------------+-------------------+-----+
| 1.3.1.14.10.2   | Rendering Intent  | Presentation      |     |
|                 |                   | Required: …       |     |
+-----------------+-------------------+-------------------+-----+
| 1.3.1.14.10.3   | Tracking          | "Detection #1"    |     |
|                 | Identifier        |                   |     |
+-----------------+-------------------+-------------------+-----+
| 1.3.1.14.10.4   | Algorithm Name    | "CT Nodule        |     |
|                 |                   | Detector"         |     |
+-----------------+-------------------+-------------------+-----+
| 1.3.1.14.10.5   | Algorithm Version | "V2.5"            |     |
+-----------------+-------------------+-------------------+-----+
| 1.3.1.14.10.6   | Center            | POINT             |     |
+-----------------+-------------------+-------------------+-----+
| 1.3.1.14.10.6.1 |                   | IMAGE 2 [CT slice |     |
|                 |                   | 103]              |     |
+-----------------+-------------------+-------------------+-----+
| 1.3.1.14.10.7   | Outline           | POLYLINE          |     |
+-----------------+-------------------+-------------------+-----+
| 1.3.1.14.10.7.1 |                   | IMAGE 2 [CT slice |     |
|                 |                   | 103]              |     |
+-----------------+-------------------+-------------------+-----+

+-----------------+-------------------+-------------------+-----+
| Node            | Code Meaning of   | Code Meaning of   | TID |
|                 | Concept Name      | Example Value     |     |
+=================+===================+===================+=====+
| 1.3.1.14.11     | Single Image      | Abnormal opacity  |     |
|                 | Finding           |                   |     |
+-----------------+-------------------+-------------------+-----+
| 1.3.1.14.11.1   | Single Image      | Nodule            |     |
|                 | Finding Modifier  |                   |     |
+-----------------+-------------------+-------------------+-----+
| 1.3.1.14.11.2   | Rendering Intent  | Presentation      |     |
|                 |                   | Required: …       |     |
+-----------------+-------------------+-------------------+-----+
| 1.3.1.14.11.3   | Tracking          | "Detection #2"    |     |
|                 | Identifier        |                   |     |
+-----------------+-------------------+-------------------+-----+
| 1.3.1.14.11.4   | Algorithm Name    | "CT Nodule        |     |
|                 |                   | Detector"         |     |
+-----------------+-------------------+-------------------+-----+
| 1.3.1.14.11.5   | Algorithm Version | "V2.5"            |     |
+-----------------+-------------------+-------------------+-----+
| 1.3.1.14.11.6   | Center            | POINT             |     |
+-----------------+-------------------+-------------------+-----+
| 1.3.1.14.11.6.1 |                   | IMAGE 3 [CT slice |     |
|                 |                   | 104]              |     |
+-----------------+-------------------+-------------------+-----+
| 1.3.1.14.11.7   | Outline           | POLYLINE          |     |
+-----------------+-------------------+-------------------+-----+
| 1.3.1.14.11.7.1 |                   | IMAGE 3 [CT slice |     |
|                 |                   | 104]              |     |
+-----------------+-------------------+-------------------+-----+

+-----------------+-------------------+-------------------+-----+
| Node            | Code Meaning of   | Code Meaning of   | TID |
|                 | Concept Name      | Example Value     |     |
+=================+===================+===================+=====+
| 1.3.1.14.12     | Single Image      | Abnormal opacity  |     |
|                 | Finding           |                   |     |
+-----------------+-------------------+-------------------+-----+
| 1.3.1.14.12.1   | Single Image      | Nodule            |     |
|                 | Finding Modifier  |                   |     |
+-----------------+-------------------+-------------------+-----+
| 1.3.1.14.12.2   | Rendering Intent  | Presentation      |     |
|                 |                   | Required: …       |     |
+-----------------+-------------------+-------------------+-----+
| 1.3.1.14.12.3   | Tracking          | "Detection #3"    |     |
|                 | Identifier        |                   |     |
+-----------------+-------------------+-------------------+-----+
| 1.3.1.14.12.4   | Algorithm Name    | "CT Nodule        |     |
|                 |                   | Detector"         |     |
+-----------------+-------------------+-------------------+-----+
| 1.3.1.14.12.5   | Algorithm Version | "V2.5"            |     |
+-----------------+-------------------+-------------------+-----+
| 1.3.1.14.12.6   | Center            | POINT             |     |
+-----------------+-------------------+-------------------+-----+
| 1.3.1.14.12.6.1 |                   | IMAGE 4 [CT slice |     |
|                 |                   | 105]              |     |
+-----------------+-------------------+-------------------+-----+
| 1.3.1.14.12.7   | Outline           | POLYLINE          |     |
+-----------------+-------------------+-------------------+-----+
| 1.3.1.14.12.7.1 |                   | IMAGE 4 [CT slice |     |
|                 |                   | 105]              |     |
+-----------------+-------------------+-------------------+-----+

+------------------+-------------------+-------------------+-----+
| Node             | Code Meaning of   | Code Meaning of   | TID |
|                  | Concept Name      | Example Value     |     |
+==================+===================+===================+=====+
| *1.3.1.15*       | Single Image      | Abnormal opacity  |     |
|                  | Finding           |                   |     |
+------------------+-------------------+-------------------+-----+
| *1.3.1.15.1*     | Single Image      | Nodule            |     |
|                  | Finding Modifier  |                   |     |
+------------------+-------------------+-------------------+-----+
| *1.3.1.15.2*     | Rendering Intent  | Presentation      |     |
|                  |                   | Required: …       |     |
+------------------+-------------------+-------------------+-----+
| *1.3.1.15.3*     | Tracking          | "Watchlist #1"    |     |
|                  | Identifier        |                   |     |
+------------------+-------------------+-------------------+-----+
| *1.3.1.15.4*     | [Observation      |                   |     |
|                  | Context content   |                   |     |
|                  | items]            |                   |     |
+------------------+-------------------+-------------------+-----+
| *1.3.1.15.5*     | Algorithm Name    | "Lung Nodule      |     |
|                  |                   | Detector"         |     |
+------------------+-------------------+-------------------+-----+
| *1.3.1.15.6*     | Algorithm Version | "V1.3"            |     |
+------------------+-------------------+-------------------+-----+
| *1.3.1.15.7*     | Center            | POINT             |     |
+------------------+-------------------+-------------------+-----+
| *1.3.1.15.7.1*   |                   | Reference to node |     |
|                  |                   | 1.2.1             |     |
+------------------+-------------------+-------------------+-----+
| *1.3.1.15.8*     | Outline           | POLYLINE          |     |
+------------------+-------------------+-------------------+-----+
| *1.3.1.15.8.1*   |                   | Reference to node |     |
|                  |                   | 1.2.1             |     |
+------------------+-------------------+-------------------+-----+
| *1.3.1.15.9*     | Diameter          | 4 cm              |     |
+------------------+-------------------+-------------------+-----+
| *1.3.1.15.9.1*   | Path              | POLYLINE          |     |
+------------------+-------------------+-------------------+-----+
| *1.3.1.15.9.1.1* |                   | Reference to Node |     |
|                  |                   | 1.2.1             |     |
+------------------+-------------------+-------------------+-----+

========= ============================ ============================= ===
Node      Code Meaning of Concept Name Code Meaning of Example Value TID
========= ============================ ============================= ===
1.4       Summary of Detections        Succeeded                     
1.4.1     Successful Detections                                      
1.4.1.1   Detection Performed          Nodule                        
1.4.1.1.1 Algorithm Name               "CT Nodule Detector"          
1.4.1.1.2 Algorithm Version            "V2.5"                        
1.4.1.1.3                              IMAGE 2 [CT slice 103]        
1.4.1.1.4                              IMAGE 3 [CT slice 104]        
1.4.1.1.5                              IMAGE 4 [CT slice 105]        
1.5       Summary of Analyses          Succeeded                     
1.5.1     Successful Analyses                                        
1.5.1.1   Analysis Performed           "Spatial colocation analysis" 
1.5.1.1.1 Algorithm Name               "Chest/CT Correlator"         
1.5.1.1.2 Algorithm Version            "V2.1"                        
1.5.1.1.3                              Reference to node 1.2.1       
1.5.1.1.4                              IMAGE 2 [CT slice 103]        
1.5.1.1.5                              IMAGE 3 [CT slice 104]        
1.5.1.1.6                              IMAGE 4 [CT slice 105]        
1.5.1.2   Analysis Performed           "Spatial colocation analysis" 
1.5.1.2.1 Algorithm Name               "Nodule Builder"              
1.5.1.2.2 Algorithm Version            "V1.4"                        
1.5.1.2.3                              IMAGE 2 [CT slice 103]        
1.5.1.2.4                              IMAGE 3 [CT slice 104]        
1.5.1.2.5                              IMAGE 4 [CT slice 105]        
========= ============================ ============================= ===

