.. _chapter_E:

Mammography CAD (Informative)
=============================

This Annex was formerly located in in the 2003 and earlier revisions of
the Standard.

.. _sect_E.1:

Mammography CAD SR Content Tree Structure
-----------------------------------------

The templates for the Mammography CAD SR IOD are defined in .
Relationships defined in the Mammography CAD SR IOD templates are
by-value, unless otherwise stated. Content items referenced from another
SR object instance, such as a prior Mammography CAD SR, are inserted
by-value in the new SR object instance, with appropriate original source
observation context. It is necessary to update Rendering Intent, and
referenced content item identifiers for by-reference relationships,
within content items paraphrased from another source.

The Document Root, Image Library, Summaries of Detections and Analyses,
and CAD Processing and Findings Summary sub-trees together form the
content tree of the Mammography CAD SR IOD. There are no constraints
regarding the 1-n multiplicity of the Individual
Impression/Recommendation or its underlying structure, other than the
and requirements in . Individual Impression/Recommendation containers
may be organized, for example per image, per finding or composite
feature, or some combination thereof.

The Summary of Detections and Summary of Analyses sub-trees identify the
algorithms used and the work done by the CAD device, and whether or not
each process was performed on one or more entire images or selected
regions of images. The findings of the detections and analyses are not
encoded in the summary sub-trees, but rather in the CAD Processing and
Findings Summary sub-tree. CAD processing may produce no findings, in
which case the sub-trees of the CAD Processing and Findings Summary
sub-tree are incompletely populated. This occurs in the following
situations:

a. All algorithms succeeded, but no findings resulted

b. Some algorithms succeeded, some failed, but no findings resulted

c. All algorithms failed

.. note::

   1. If the tree contains no Individual Impression/Recommendation nodes
      and all attempted detections and analyses succeeded then the
      mammography CAD device made no findings.

   2. Detections and Analyses that are not attempted are not listed in
      the Summary of Detections and Summary of Analyses trees.

   3. If the code value of the Summary of Detections or Summary of
      Analyses codes in is "Not Attempted" then no detail is provided as
      to which algorithms were not attempted.

The shaded area in `figure_title <#figure_E.1-3>`__ demarcates
information resulting from Detection, whereas the unshaded area is
information resulting from Analysis. This distinction is used in
determining whether to place algorithm identification information in the
Summary of Detections or Summary of Analyses sub-trees.

The clustering of calcifications within a single image is considered to
be a Detection process that results in a Single Image Finding. The
spatial correlation of a calcification cluster in two views, resulting
in a Composite Feature, is considered Analysis. The clustering of
calcifications in a single image is the only circumstance in which a
Single Image Finding can result from the combination of other Single
Image Findings, which must be Individual Calcifications.

Once a Single Image Finding or Composite Feature has been instantiated,
it may be referenced by any number of Composite Features higher in the
tree.

.. _sect_E.2:

Mammography CAD SR Observation Context Encoding
-----------------------------------------------

-  Any content item in the Content tree that has been inserted (i.e.,
   duplicated) from another SR object instance has a HAS OBS CONTEXT
   relationship to one or more content items that describe the context
   of the SR object instance from which it originated. This mechanism
   may be used to combine reports (e.g., Mammography CAD 1, Mammography
   CAD 2, Human).

-  By-reference relationships within Single Image Findings and Composite
   Features paraphrased from prior Mammography CAD SR objects need to be
   updated to properly reference Image Library Entries carried from the
   prior object to their new positions in the present object.

The Impression/Recommendation section of the SR Document Content tree of
a Mammography CAD SR IOD may contain a mixture of current and prior
single image findings and composite features. The content items from
current and prior contexts are target content items that have a by-value
INFERRED FROM relationship to a Composite Feature content item. Content
items that come from a context other than the Initial Observation
Context have a HAS OBS CONTEXT relationship to target content items that
describe the context of the source document.

In `figure_title <#figure_E.2-1>`__, Composite Feature and Single Image
Finding are current, and Single Image Finding (from Prior) is duplicated
from a prior document.

.. _sect_E.3:

Mammography CAD SR Examples
---------------------------

The following is a simple and non-comprehensive illustration of an
encoding of the Mammography CAD SR IOD for Mammography computer aided
detection results. For brevity, some Mandatory content items are not
included, such as several acquisition context content items for the
images in the Image Library.

.. _sect_E.3.1:

Example 1: Calcification and Mass Detection With No Findings
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

A mammography CAD device processes a typical screening mammography case,
i.e., there are four films and no cancer. Mammography CAD runs both
density and calcification detection successfully and finds nothing. The
mammograms resemble:

The content tree structure would resemble:

+-----------+------------------------+------------------------+-----+
| Node      | Code Meaning of        | Code Meaning or        | TID |
|           | Concept Name           | Example Value          |     |
+===========+========================+========================+=====+
| 1         | Mammography CAD Report |                        |     |
+-----------+------------------------+------------------------+-----+
| 1.1       | Image Library          |                        |     |
+-----------+------------------------+------------------------+-----+
| 1.1.1     |                        | IMAGE 1                |     |
+-----------+------------------------+------------------------+-----+
| 1.1.1.1   | Image Laterality       | Right                  |     |
+-----------+------------------------+------------------------+-----+
| 1.1.1.2   | Image View             | Cranio-caudal          |     |
+-----------+------------------------+------------------------+-----+
| 1.1.1.3   | Study Date             | 19980101               |     |
+-----------+------------------------+------------------------+-----+
| 1.1.2     |                        | IMAGE 2                |     |
+-----------+------------------------+------------------------+-----+
| 1.1.2.1   | Image Laterality       | Left                   |     |
+-----------+------------------------+------------------------+-----+
| 1.1.2.2   | Image View             | Cranio-caudal          |     |
+-----------+------------------------+------------------------+-----+
| 1.1.2.3   | Study Date             | 19980101               |     |
+-----------+------------------------+------------------------+-----+
| 1.1.3     |                        | IMAGE 3                |     |
+-----------+------------------------+------------------------+-----+
| 1.1.3.1   | Image Laterality       | Right                  |     |
+-----------+------------------------+------------------------+-----+
| 1.1.3.2   | Image View             | Medio-lateral oblique  |     |
+-----------+------------------------+------------------------+-----+
| 1.1.3.3   | Study Date             | 19980101               |     |
+-----------+------------------------+------------------------+-----+
| 1.1.4     |                        | IMAGE 4                |     |
+-----------+------------------------+------------------------+-----+
| 1.1.4.1   | Image Laterality       | Left                   |     |
+-----------+------------------------+------------------------+-----+
| 1.1.4.2   | Image View             | Medio-lateral oblique  |     |
+-----------+------------------------+------------------------+-----+
| 1.1.4.3   | Study Date             | 19980101               |     |
+-----------+------------------------+------------------------+-----+
| 1.2       | CAD Processing and     | All algorithms         |     |
|           | Findings Summary       | succeeded; without     |     |
|           |                        | findings               |     |
+-----------+------------------------+------------------------+-----+
| 1.3       | Summary of Detections  | Succeeded              |     |
+-----------+------------------------+------------------------+-----+
| 1.3.1     | Successful Detections  |                        |     |
+-----------+------------------------+------------------------+-----+
| 1.3.1.1   | Detection Performed    | Mammography breast     |     |
|           |                        | density                |     |
+-----------+------------------------+------------------------+-----+
| 1.3.1.1.1 | Algorithm Name         | "Density Detector"     |     |
+-----------+------------------------+------------------------+-----+
| 1.3.1.1.2 | Algorithm Version      | "V3.7"                 |     |
+-----------+------------------------+------------------------+-----+
| 1.3.1.1.3 |                        | Reference to node      |     |
|           |                        | 1.1.1                  |     |
+-----------+------------------------+------------------------+-----+
| 1.3.1.1.4 |                        | Reference to node      |     |
|           |                        | 1.1.2                  |     |
+-----------+------------------------+------------------------+-----+
| 1.3.1.1.5 |                        | Reference to node      |     |
|           |                        | 1.1.3                  |     |
+-----------+------------------------+------------------------+-----+
| 1.3.1.1.6 |                        | Reference to node      |     |
|           |                        | 1.1.4                  |     |
+-----------+------------------------+------------------------+-----+
| 1.3.1.2   | Detection Performed    | Individual             |     |
|           |                        | Calcification          |     |
+-----------+------------------------+------------------------+-----+
| 1.3.1.2.1 | Algorithm Name         | "Calc Detector"        |     |
+-----------+------------------------+------------------------+-----+
| 1.3.1.2.2 | Algorithm Version      | "V2.4"                 |     |
+-----------+------------------------+------------------------+-----+
| 1.3.1.2.3 |                        | Reference to node      |     |
|           |                        | 1.1.1                  |     |
+-----------+------------------------+------------------------+-----+
| 1.3.1.2.4 |                        | Reference to node      |     |
|           |                        | 1.1.2                  |     |
+-----------+------------------------+------------------------+-----+
| 1.3.1.2.5 |                        | Reference to node      |     |
|           |                        | 1.1.3                  |     |
+-----------+------------------------+------------------------+-----+
| 1.3.1.2.6 |                        | Reference to node      |     |
|           |                        | 1.1.4                  |     |
+-----------+------------------------+------------------------+-----+
| 1.4       | Summary of Analyses    | Not Attempted          |     |
+-----------+------------------------+------------------------+-----+

.. _sect_E.3.2:

Example 2: Calcification and Mass Detection With Findings
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

A mammography CAD device processes a screening mammography case with
four films and a mass in the left breast. Mammography CAD runs both
density and calcification detection successfully. It finds two densities
in the LCC, one density in the LMLO, a cluster of two calcifications in
the RCC and a cluster of 20 calcifications in the RMLO. It performs two
clustering algorithms. One identifies individual calcifications and then
clusters them, and the second simply detects calcification clusters. It
performs mass correlation and combines one of the LCC densities and the
LMLO density into a mass; the other LCC density is flagged Not for
Presentation, therefore not intended for display to the end-user. The
mammograms resemble:

The content tree structure in this example is complex. Structural
illustrations of portions of the content tree are placed within the
content tree table to show the relationships of data within the tree.
Some content items are duplicated (and shown in boldface) to facilitate
use of the diagrams.

+---------+-------------------------+-------------------------+-----+
| Node    | Code Meaning of Concept | Code Meaning or Example | TID |
|         | Name                    | Value                   |     |
+=========+=========================+=========================+=====+
| 1       | Mammography CAD Report  |                         |     |
+---------+-------------------------+-------------------------+-----+
| **1.1** | Image Library           |                         |     |
+---------+-------------------------+-------------------------+-----+
| **1.2** | CAD Processing and      | All algorithms          |     |
|         | Findings Summary        | succeeded; with         |     |
|         |                         | findings                |     |
+---------+-------------------------+-------------------------+-----+
| **1.3** | Summary of Detections   | Succeeded               |     |
+---------+-------------------------+-------------------------+-----+
| **1.4** | Summary of Analyses     | Succeeded               |     |
+---------+-------------------------+-------------------------+-----+

======= ============================ ============================= ===
Node    Code Meaning of Concept Name Code Meaning or Example Value TID
======= ============================ ============================= ===
1.1     Image Library                                              
1.1.1                                IMAGE 1                       
1.1.1.1 Image Laterality             Right                         
1.1.1.2 Image View                   Cranio-caudal                 
1.1.1.3 Study Date                   19990101                      
1.1.2                                IMAGE 2                       
1.1.2.1 Image Laterality             Left                          
1.1.2.2 Image View                   Cranio-caudal                 
1.1.2.3 Study Date                   19990101                      
1.1.3                                IMAGE 3                       
1.1.3.1 Image Laterality             Right                         
1.1.3.2 Image View                   Medio-lateral oblique         
1.1.3.3 Study Date                   19990101                      
1.1.4                                IMAGE 4                       
1.1.4.1 Image Laterality             Left                          
1.1.4.2 Image View                   Medio-lateral oblique         
1.1.4.3 Study Date                   19990101                      
======= ============================ ============================= ===

+-----------+------------------------+------------------------+-----+
| Node      | Code Meaning of        | Code Meaning or        | TID |
|           | Concept Name           | Example Value          |     |
+===========+========================+========================+=====+
| 1.2       | CAD Processing and     | All algorithms         |     |
|           | Findings Summary       | succeeded; with        |     |
|           |                        | findings               |     |
+-----------+------------------------+------------------------+-----+
| **1.2.1** | Individual             |                        |     |
|           | Imp                    |                        |     |
|           | ression/Recommendation |                        |     |
+-----------+------------------------+------------------------+-----+
| **1.2.2** | Individual             |                        |     |
|           | Imp                    |                        |     |
|           | ression/Recommendation |                        |     |
+-----------+------------------------+------------------------+-----+
| **1.2.3** | Individual             |                        |     |
|           | Imp                    |                        |     |
|           | ression/Recommendation |                        |     |
+-----------+------------------------+------------------------+-----+
| **1.2.4** | Individual             |                        |     |
|           | Imp                    |                        |     |
|           | ression/Recommendation |                        |     |
+-----------+------------------------+------------------------+-----+

+-----------+------------------------+------------------------+-----+
| Node      | Code Meaning of        | Code Meaning or        | TID |
|           | Concept Name           | Example Value          |     |
+===========+========================+========================+=====+
| 1.2.1     | Individual             |                        |     |
|           | Imp                    |                        |     |
|           | ression/Recommendation |                        |     |
+-----------+------------------------+------------------------+-----+
| 1.2.1.1   | Rendering Intent       | Presentation Required  |     |
+-----------+------------------------+------------------------+-----+
| 1.2.1.2   | Composite Feature      | Mass                   |     |
+-----------+------------------------+------------------------+-----+
| 1.2.1.2.1 | Rendering Intent       | Presentation Required  |     |
+-----------+------------------------+------------------------+-----+
| 1.2.1.2.2 | Composite type         | Target content items   |     |
|           |                        | are related spatially  |     |
+-----------+------------------------+------------------------+-----+
| 1.2.1.2.3 | Scope of Feature       | Feature was detected   |     |
|           |                        | on multiple images     |     |
+-----------+------------------------+------------------------+-----+
| 1.2.1.2.4 | Algorithm Name         | "Mass Maker"           |     |
+-----------+------------------------+------------------------+-----+
| 1.2.1.2.5 | Algorithm Version      | "V1.9"                 |     |
+-----------+------------------------+------------------------+-----+
| 1.2.1.2.6 | Single Image Finding   | Mammography breast     |     |
|           |                        | density                |     |
+-----------+------------------------+------------------------+-----+
| 1.2.1.2.7 | Single Image Finding   | Mammography breast     |     |
|           |                        | density                |     |
+-----------+------------------------+------------------------+-----+

+---------------+----------------------+----------------------+-----+
| Node          | Code Meaning of      | Code Meaning or      | TID |
|               | Concept Name         | Example Value        |     |
+===============+======================+======================+=====+
| 1.2.1.2.6     | Single Image Finding | Mammography breast   |     |
|               |                      | density              |     |
+---------------+----------------------+----------------------+-----+
| 1.2.1.2.6.1   | Rendering Intent     | Presentation         |     |
|               |                      | Required             |     |
+---------------+----------------------+----------------------+-----+
| 1.2.1.2.6.2   | Algorithm Name       | "Density Detector"   |     |
+---------------+----------------------+----------------------+-----+
| 1.2.1.2.6.3   | Algorithm Version    | "V3.7"               |     |
+---------------+----------------------+----------------------+-----+
| 1.2.1.2.6.4   | Center               | POINT                |     |
+---------------+----------------------+----------------------+-----+
| 1.2.1.2.6.4.1 |                      | Reference to node    |     |
|               |                      | 1.1.2                |     |
+---------------+----------------------+----------------------+-----+
| 1.2.1.2.6.5   | Outline              | SCOORD               |     |
+---------------+----------------------+----------------------+-----+
| 1.2.1.2.6.5.1 |                      | Reference to node    |     |
|               |                      | 1.1.2                |     |
+---------------+----------------------+----------------------+-----+

+-----------------+-------------------+-------------------+-----+
| Node            | Code Meaning of   | Code Meaning or   | TID |
|                 | Concept Name      | Example Value     |     |
+=================+===================+===================+=====+
| 1.2.1.2.7       | Single Image      | Mammography       |     |
|                 | Finding           | breast density    |     |
+-----------------+-------------------+-------------------+-----+
| 1.2.1.2.7.1     | Rendering Intent  | Presentation      |     |
|                 |                   | Required          |     |
+-----------------+-------------------+-------------------+-----+
| 1.2.1.2.7.2     | Algorithm Name    | "Density          |     |
|                 |                   | Detector"         |     |
+-----------------+-------------------+-------------------+-----+
| 1.2.1.2.7.3     | Algorithm Version | "V3.7"            |     |
+-----------------+-------------------+-------------------+-----+
| 1.2.1.2.7.4     | Center            | POINT             |     |
+-----------------+-------------------+-------------------+-----+
| 1.2.1.2.7.4.1   |                   | Reference to node |     |
|                 |                   | 1.1.4             |     |
+-----------------+-------------------+-------------------+-----+
| 1.2.1.2.7.5     | Outline           | SCOORD            |     |
+-----------------+-------------------+-------------------+-----+
| 1.2.1.2.7.5.1   |                   | Reference to node |     |
|                 |                   | 1.1.4             |     |
+-----------------+-------------------+-------------------+-----+
| 1.2.1.2.7.6     | Area of Defined   | 1 cm\ :sup:`2`    |     |
|                 | Region            |                   |     |
+-----------------+-------------------+-------------------+-----+
| 1.2.1.2.7.6.1   | Area Outline      | SCOORD            |     |
+-----------------+-------------------+-------------------+-----+
| 1.2.1.2.7.6.1.1 |                   | Reference to node |     |
|                 |                   | 1.1.4             |     |
+-----------------+-------------------+-------------------+-----+

+-------------+-----------------------+-----------------------+-----+
| Node        | Code Meaning of       | Code Meaning or       | TID |
|             | Concept Name          | Example Value         |     |
+=============+=======================+=======================+=====+
| 1.2.2       | Individual            |                       |     |
|             | Impr                  |                       |     |
|             | ession/Recommendation |                       |     |
+-------------+-----------------------+-----------------------+-----+
| 1.2.2.1     | Rendering Intent      | Not for Presentation  |     |
+-------------+-----------------------+-----------------------+-----+
| 1.2.2.2     | Single Image Finding  | Mammography breast    |     |
|             |                       | density               |     |
+-------------+-----------------------+-----------------------+-----+
| 1.2.2.2.1   | Rendering Intent      | Not for Presentation  |     |
+-------------+-----------------------+-----------------------+-----+
| 1.2.2.2.2   | Algorithm Name        | "Density Detector"    |     |
+-------------+-----------------------+-----------------------+-----+
| 1.2.2.2.3   | Algorithm Version     | "V3.7"                |     |
+-------------+-----------------------+-----------------------+-----+
| 1.2.2.2.4   | Center                | POINT                 |     |
+-------------+-----------------------+-----------------------+-----+
| 1.2.2.2.4.1 |                       | Reference to node     |     |
|             |                       | 1.1.2                 |     |
+-------------+-----------------------+-----------------------+-----+
| 1.2.2.2.5   | Outline               | SCOORD                |     |
+-------------+-----------------------+-----------------------+-----+
| 1.2.2.2.5.1 |                       | Reference to node     |     |
|             |                       | 1.1.2                 |     |
+-------------+-----------------------+-----------------------+-----+

+-------------+-----------------------+-----------------------+-----+
| Node        | Code Meaning of       | Code Meaning or       | TID |
|             | Concept Name          | Example Value         |     |
+=============+=======================+=======================+=====+
| 1.2.3       | Individual            |                       |     |
|             | Impr                  |                       |     |
|             | ession/Recommendation |                       |     |
+-------------+-----------------------+-----------------------+-----+
| 1.2.3.1     | Rendering Intent      | Presentation Required |     |
+-------------+-----------------------+-----------------------+-----+
| 1.2.3.2     | Single Image Finding  | Calcification Cluster |     |
+-------------+-----------------------+-----------------------+-----+
| 1.2.3.2.1   | Rendering Intent      | Presentation Required |     |
+-------------+-----------------------+-----------------------+-----+
| 1.2.3.2.2   | Algorithm Name        | "Calc Cluster         |     |
|             |                       | Detector"             |     |
+-------------+-----------------------+-----------------------+-----+
| 1.2.3.2.3   | Algorithm Version     | "V2.4"                |     |
+-------------+-----------------------+-----------------------+-----+
| 1.2.3.2.4   | Center                | POINT                 |     |
+-------------+-----------------------+-----------------------+-----+
| 1.2.3.2.4.1 |                       | Reference to node     |     |
|             |                       | 1.1.3                 |     |
+-------------+-----------------------+-----------------------+-----+
| 1.2.3.2.5   | Outline               | SCOORD                |     |
+-------------+-----------------------+-----------------------+-----+
| 1.2.3.2.5.1 |                       | Reference to node     |     |
|             |                       | 1.1.3                 |     |
+-------------+-----------------------+-----------------------+-----+
| 1.2.3.2.6   | Number of             | 20                    |     |
|             | Calcifications        |                       |     |
+-------------+-----------------------+-----------------------+-----+

+-------------+-----------------------+-----------------------+-----+
| Node        | Code Meaning of       | Code Meaning or       | TID |
|             | Concept Name          | Example Value         |     |
+=============+=======================+=======================+=====+
| 1.2.4       | Individual            |                       |     |
|             | Impr                  |                       |     |
|             | ession/Recommendation |                       |     |
+-------------+-----------------------+-----------------------+-----+
| 1.2.4.1     | Rendering Intent      | Presentation Required |     |
+-------------+-----------------------+-----------------------+-----+
| 1.2.4.2     | Single Image Finding  | Calcification Cluster |     |
+-------------+-----------------------+-----------------------+-----+
| 1.2.4.2.1   | Rendering Intent      | Presentation Required |     |
+-------------+-----------------------+-----------------------+-----+
| 1.2.4.2.2   | Algorithm Name        | "Calc Clustering"     |     |
+-------------+-----------------------+-----------------------+-----+
| 1.2.4.2.3   | Algorithm Version     | "V2.4"                |     |
+-------------+-----------------------+-----------------------+-----+
| 1.2.4.2.4   | Center                | POINT                 |     |
+-------------+-----------------------+-----------------------+-----+
| 1.2.4.2.4.1 |                       | Reference to node     |     |
|             |                       | 1.1.1                 |     |
+-------------+-----------------------+-----------------------+-----+
| 1.2.4.2.5   | Outline               | SCOORD                |     |
+-------------+-----------------------+-----------------------+-----+
| 1.2.4.2.5.1 |                       | Reference to node     |     |
|             |                       | 1.1.1                 |     |
+-------------+-----------------------+-----------------------+-----+
| 1.2.4.2.6   | Number of             | 2                     |     |
|             | Calcifications        |                       |     |
+-------------+-----------------------+-----------------------+-----+

+---------------+----------------------+----------------------+-----+
| Node          | Code Meaning of      | Code Meaning or      | TID |
|               | Concept Name         | Example Value        |     |
+===============+======================+======================+=====+
| 1.2.4.2.7     | Single Image Finding | Individual           |     |
|               |                      | Calcification        |     |
+---------------+----------------------+----------------------+-----+
| 1.2.4.2.7.1   | Rendering Intent     | Presentation         |     |
|               |                      | Optional             |     |
+---------------+----------------------+----------------------+-----+
| 1.2.4.2.7.2   | Algorithm Name       | "Calc Detector"      |     |
+---------------+----------------------+----------------------+-----+
| 1.2.4.2.7.3   | Algorithm Version    | "V2.4"               |     |
+---------------+----------------------+----------------------+-----+
| 1.2.4.2.7.4   | Center               | POINT                |     |
+---------------+----------------------+----------------------+-----+
| 1.2.4.2.7.4.1 |                      | Reference to node    |     |
|               |                      | 1.1.1                |     |
+---------------+----------------------+----------------------+-----+
| 1.2.4.2.7.5   | Outline              | SCOORD               |     |
+---------------+----------------------+----------------------+-----+
| 1.2.4.2.7.5.1 |                      | Reference to node    |     |
|               |                      | 1.1.1                |     |
+---------------+----------------------+----------------------+-----+

+---------------+----------------------+----------------------+-----+
| Node          | Code Meaning of      | Code Meaning or      | TID |
|               | Concept Name         | Example Value        |     |
+===============+======================+======================+=====+
| 1.2.4.2.8     | Single Image Finding | Individual           |     |
|               |                      | Calcification        |     |
+---------------+----------------------+----------------------+-----+
| 1.2.4.2.8.1   | Rendering Intent     | Presentation         |     |
|               |                      | Optional             |     |
+---------------+----------------------+----------------------+-----+
| 1.2.4.2.8.2   | Algorithm Name       | "Calc Detector"      |     |
+---------------+----------------------+----------------------+-----+
| 1.2.4.2.8.3   | Algorithm Version    | "V2.4"               |     |
+---------------+----------------------+----------------------+-----+
| 1.2.4.2.8.4   | Center               | POINT                |     |
+---------------+----------------------+----------------------+-----+
| 1.2.4.2.8.4.1 |                      | Reference to node    |     |
|               |                      | 1.1.1                |     |
+---------------+----------------------+----------------------+-----+
| 1.2.4.2.8.5   | Outline              | SCOORD               |     |
+---------------+----------------------+----------------------+-----+
| 1.2.4.2.8.5.1 |                      | Reference to node    |     |
|               |                      | 1.1.1                |     |
+---------------+----------------------+----------------------+-----+

========= ============================ ============================= ===
Node      Code Meaning of Concept Name Code Meaning or Example Value TID
========= ============================ ============================= ===
1.3       Summary of Detections        Succeeded                     
1.3.1     Successful Detections                                      
1.3.1.1   Detection Performed          Mammography breast density    
1.3.1.1.1 Algorithm Name               "Density Detector"            
1.3.1.1.2 Algorithm Version            "V3.7"                        
1.3.1.1.3                              Reference to node 1.1.1       
1.3.1.1.4                              Reference to node 1.1.2       
1.3.1.1.5                              Reference to node 1.1.3       
1.3.1.1.6                              Reference to node 1.1.4       
1.3.1.2   Detection Performed          Individual Calcification      
1.3.1.2.1 Algorithm Name               "Calc Detector"               
1.3.1.2.2 Algorithm Version            "V2.4"                        
1.3.1.2.3                              Reference to node 1.1.1       
1.3.1.2.4                              Reference to node 1.1.2       
1.3.1.2.5                              Reference to node 1.1.3       
1.3.1.2.6                              Reference to node 1.1.4       
1.3.1.3   Detection Performed          Calcification Cluster         
1.3.1.3.1 Algorithm Name               "Calc Clustering"             
1.3.1.3.2 Algorithm Version            "V2.4"                        
1.3.1.3.3                              Reference to node 1.1.1       
1.3.1.4   Detection Performed          Calcification Cluster         
1.3.1.4.1 Algorithm Name               "Calc Cluster Detector"       
1.3.1.4.2 Algorithm Version            "V2.4"                        
1.3.1.4.3                              Reference to node 1.1.1       
1.3.1.4.4                              Reference to node 1.1.2       
1.3.1.4.5                              Reference to node 1.1.3       
1.3.1.4.6                              Reference to node 1.1.4       
========= ============================ ============================= ===

========= ============================ ============================= ===
Node      Code Meaning of Concept Name Code Meaning or Example Value TID
========= ============================ ============================= ===
1.4       Summary of Analyses          Succeeded                     
1.4.1     Successful Analyses                                        
1.4.1.1   Analysis Performed           Mass Correlation              
1.4.1.1.1 Algorithm Name               "Mass Maker"                  
1.4.1.1.2 Algorithm Version            "V1.9"                        
1.4.1.1.3                              Reference to node 1.1.2       
1.4.1.1.4                              Reference to node 1.1.4       
========= ============================ ============================= ===

.. _sect_E.3.3:

Example 3: Calcification and Mass Detection, Temporal Differencing With Findings
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

The patient in Example 2 returns for another mammogram. A more
comprehensive mammography CAD device processes the current mammogram;
analyses are performed that determine some content items for Overall and
Individual Impression/Recommendations. Portions of the prior mammography
CAD report (Example 2) are incorporated into this report. In the current
mammogram the number of calcifications in the RCC has increased, and the
size of the mass in the left breast has increased from 1 to 4
cm\ :sup:`2`.

Italicized entries (*xxx*) in the following table denote references to
or by-value inclusion of content tree items reused from the prior
Mammography CAD SR instance (Example 2).

==== ============================ ============================= ===
Node Code Meaning of Concept Name Code Meaning or Example Value TID
==== ============================ ============================= ===
1    Mammography CAD Report                                     
==== ============================ ============================= ===

While the Image Library contains references to content tree items reused
from the prior Mammography CAD SR instance, the images are actually used
in the mammography CAD analysis and are therefore not italicized as
indicated above.

======= ============================ ============================= ===
Node    Code Meaning of Concept Name Code Meaning or Example Value TID
======= ============================ ============================= ===
1.1     Image Library                                              
1.1.1                                IMAGE 1                       
1.1.1.1 Image Laterality             Right                         
1.1.1.2 Image View                   Cranio-caudal                 
1.1.1.3 Study Date                   20000101                      
1.1.2                                IMAGE 2                       
1.1.2.1 Image Laterality             Left                          
1.1.2.2 Image View                   Cranio-caudal                 
1.1.2.3 Study Date                   20000101                      
1.1.3                                IMAGE 3                       
1.1.3.1 Image Laterality             Right                         
1.1.3.2 Image View                   Medio-lateral oblique         
1.1.3.3 Study Date                   20000101                      
1.1.4                                IMAGE 4                       
1.1.4.1 Image Laterality             Left                          
1.1.4.2 Image View                   Medio-lateral oblique         
1.1.4.3 Study Date                   20000101                      
1.1.5                                IMAGE 5                       
1.1.5.1 Image Laterality             Right                         
1.1.5.2 Image View                   Cranio-caudal                 
1.1.5.3 Study Date                   19990101                      
1.1.6                                IMAGE 6                       
1.1.6.1 Image Laterality             Left                          
1.1.6.2 Image View                   Cranio-caudal                 
1.1.6.3 Study Date                   19990101                      
1.1.7                                IMAGE 7                       
1.1.7.1 Image Laterality             Right                         
1.1.7.2 Image View                   Medio-lateral oblique         
1.1.7.3 Study Date                   19990101                      
1.1.8                                IMAGE 8                       
1.1.8.1 Image Laterality             Left                          
1.1.8.2 Image View                   Medio-lateral oblique         
1.1.8.3 Study Date                   19990101                      
======= ============================ ============================= ===

Current year content:

+-------------------+-------------------+-------------------+-----+
| Node              | Code Meaning of   | Code Meaning or   | TID |
|                   | Concept Name      | Example Value     |     |
+===================+===================+===================+=====+
| 1.2               | CAD Processing    | All algorithms    |     |
|                   | and Findings      | succeeded; with   |     |
|                   | Summary           | findings          |     |
+-------------------+-------------------+-------------------+-----+
| 1.2.1             | Assessment        | 4 - Suspicious    |     |
|                   | Category          | abnormality,      |     |
|                   |                   | biopsy should be  |     |
|                   |                   | considered        |     |
+-------------------+-------------------+-------------------+-----+
| 1.2.2             | Recommend         | 0 days            |     |
|                   | Follow-up         |                   |     |
|                   | Interval          |                   |     |
+-------------------+-------------------+-------------------+-----+
| 1.2.3             | Algorithm Name    | "Mammogram        |     |
|                   |                   | Analyzer"         |     |
+-------------------+-------------------+-------------------+-----+
| 1.2.4             | Algorithm Version | "V1.0"            |     |
+-------------------+-------------------+-------------------+-----+
| 1.2.5             | Individual        |                   |     |
|                   | Impressi          |                   |     |
|                   | on/Recommendation |                   |     |
+-------------------+-------------------+-------------------+-----+
| 1.2.5.1           | Rendering Intent  | Presentation      |     |
|                   |                   | Required          |     |
+-------------------+-------------------+-------------------+-----+
| 1.2.5.2           | Differential      | Increase in size  |     |
|                   | Dia               |                   |     |
|                   | gnosis/Impression |                   |     |
+-------------------+-------------------+-------------------+-----+
| 1.2.5.3           | Impression        | "Worrisome        |     |
|                   | Description       | increase in size" |     |
+-------------------+-------------------+-------------------+-----+
| 1.2.5.4           | Recommended       | Needle            |     |
|                   | Follow-up         | localization and  |     |
|                   |                   | biopsy            |     |
+-------------------+-------------------+-------------------+-----+
| 1.2.5.5           | Certainty of      | 84%               |     |
|                   | impression        |                   |     |
+-------------------+-------------------+-------------------+-----+
| 1.2.5.6           | Algorithm Name    | "Lesion Analyzer" |     |
+-------------------+-------------------+-------------------+-----+
| 1.2.5.7           | Algorithm Version | "V1.0"            |     |
+-------------------+-------------------+-------------------+-----+
| 1.2.5.8           | Composite Feature | Mass              |     |
+-------------------+-------------------+-------------------+-----+
| 1.2.5.8.1         | Rendering Intent  | Presentation      |     |
|                   |                   | Required          |     |
+-------------------+-------------------+-------------------+-----+
| 1.2.5.8.2         | Composite type    | Target content    |     |
|                   |                   | items are related |     |
|                   |                   | temporally        |     |
+-------------------+-------------------+-------------------+-----+
| 1.2.5.8.3         | Scope of Feature  | Feature was       |     |
|                   |                   | detected on       |     |
|                   |                   | multiple images   |     |
+-------------------+-------------------+-------------------+-----+
| 1.2.5.8.4         | Algorithm Name    | "Temporal Change" |     |
+-------------------+-------------------+-------------------+-----+
| 1.2.5.8.5         | Algorithm Version | "V0.1"            |     |
+-------------------+-------------------+-------------------+-----+
| 1.2.5.8.6         | Certainty of      | 91%               |     |
|                   | Feature           |                   |     |
+-------------------+-------------------+-------------------+-----+
| 1.2.5.8.7         | Probability of    | 84%               |     |
|                   | Cancer            |                   |     |
+-------------------+-------------------+-------------------+-----+
| 1.2.5.8.8         | Pathology         | Invasive lobular  |     |
|                   |                   | carcinoma         |     |
+-------------------+-------------------+-------------------+-----+
| 1.2.5.8.9         | Difference in     | 3 cm\ :sup:`2`    |     |
|                   | Size              |                   |     |
+-------------------+-------------------+-------------------+-----+
| 1.2.5.8.9.1       |                   | Reference to node |     |
|                   |                   | 1.2.5.8.13.7.6    |     |
+-------------------+-------------------+-------------------+-----+
| 1.2.5.8.9.2       |                   | Reference to node |     |
|                   |                   | *1.2.5.8.14.8.6*  |     |
+-------------------+-------------------+-------------------+-----+
| 1.2.5.8.10        | Lesion Density    | High density      |     |
+-------------------+-------------------+-------------------+-----+
| 1.2.5.8.11        | Shape             | Lobular           |     |
+-------------------+-------------------+-------------------+-----+
| 1.2.5.8.12        | Margins           | Microlobulated    |     |
+-------------------+-------------------+-------------------+-----+
| 1.2.5.8.13        | Composite Feature | Mass              |     |
+-------------------+-------------------+-------------------+-----+
| 1.2.5.8.13.1      | Rendering Intent  | Presentation      |     |
|                   |                   | Required          |     |
+-------------------+-------------------+-------------------+-----+
| 1.2.5.8.13.2      | Composite type    | Target content    |     |
|                   |                   | items are related |     |
|                   |                   | spatially         |     |
+-------------------+-------------------+-------------------+-----+
| 1.2.5.8.13.3      | Scope of Feature  | Feature was       |     |
|                   |                   | detected on       |     |
|                   |                   | multiple images   |     |
+-------------------+-------------------+-------------------+-----+
| 1.2.5.8.13.4      | Algorithm Name    | "Mass Maker"      |     |
+-------------------+-------------------+-------------------+-----+
| 1.2.5.8.13.5      | Algorithm Version | "V1.9"            |     |
+-------------------+-------------------+-------------------+-----+
| 1.2.5.8.13.6      | Single Image      | Mammography       |     |
|                   | Finding           | breast density    |     |
+-------------------+-------------------+-------------------+-----+
| 1.2.5.8.13.6.1    | Rendering Intent  | Presentation      |     |
|                   |                   | Required          |     |
+-------------------+-------------------+-------------------+-----+
| 1.2.5.8.13.6.2    | Algorithm Name    | "Density          |     |
|                   |                   | Detector"         |     |
+-------------------+-------------------+-------------------+-----+
| 1.2.5.8.13.6.3    | Algorithm Version | "V3.7"            |     |
+-------------------+-------------------+-------------------+-----+
| 1.2.5.8.13.6.4    | Center            | POINT             |     |
+-------------------+-------------------+-------------------+-----+
| 1.2.5.8.13.6.4.1  |                   | Reference to node |     |
|                   |                   | 1.1.2             |     |
+-------------------+-------------------+-------------------+-----+
| 1.2.5.8.13.6.5    | Outline           | SCOORD            |     |
+-------------------+-------------------+-------------------+-----+
| 1.2.5.8.13.6.5.1  |                   | Reference to node |     |
|                   |                   | 1.1.2             |     |
+-------------------+-------------------+-------------------+-----+
| 1.2.5.8.13.7      | Single Image      | Mammography       |     |
|                   | Finding           | breast density    |     |
+-------------------+-------------------+-------------------+-----+
| 1.2.5.8.13.7.1    | Rendering Intent  | Presentation      |     |
|                   |                   | Required          |     |
+-------------------+-------------------+-------------------+-----+
| 1.2.5.8.13.7.2    | Algorithm Name    | "Density          |     |
|                   |                   | Detector"         |     |
+-------------------+-------------------+-------------------+-----+
| 1.2.5.8.13.7.3    | Algorithm Version | "V3.7"            |     |
+-------------------+-------------------+-------------------+-----+
| 1.2.5.8.13.7.4    | Center            | POINT             |     |
+-------------------+-------------------+-------------------+-----+
| 1.2.5.8.13.7.4.1  |                   | Reference to node |     |
|                   |                   | 1.1.4             |     |
+-------------------+-------------------+-------------------+-----+
| 1.2.5.8.13.7.5    | Outline           | SCOORD            |     |
+-------------------+-------------------+-------------------+-----+
| 1.2.5.8.13.7.5.1  |                   | Reference to node |     |
|                   |                   | 1.1.4             |     |
+-------------------+-------------------+-------------------+-----+
| 1.2.5.8.13.7.6    | Area of Defined   | 4 cm\ :sup:`2`    |     |
|                   | Region            |                   |     |
+-------------------+-------------------+-------------------+-----+
| 1.2.5.8.13.7.6.1  | Area Outline      | SCOORD            |     |
+-------------------+-------------------+-------------------+-----+
| 1.2.5.8.13.7.6.   |                   | Reference to node |     |
| 1.1               |                   | 1.1.4             |     |
+-------------------+-------------------+-------------------+-----+

Included content from prior mammography CAD report (see Example 2,
starting with node 1.2.1.2)

+-------------------+-------------------+-------------------+-----+
| Node              | Code Meaning of   | Code Meaning or   | TID |
|                   | Concept Name      | Example Value     |     |
+===================+===================+===================+=====+
| *1.2.5.8.14*      | Composite Feature | Mass              |     |
+-------------------+-------------------+-------------------+-----+
| *1.2.5.8.14.1*    | Rendering Intent  | Presentation      |     |
|                   |                   | Required          |     |
+-------------------+-------------------+-------------------+-----+
| *1.2.5.8.14.2*    | Composite type    | Target content    |     |
|                   |                   | items are related |     |
|                   |                   | spatially         |     |
+-------------------+-------------------+-------------------+-----+
| *1.2.5.8.14.3*    | Scope of Feature  | Feature was       |     |
|                   |                   | detected on       |     |
|                   |                   | multiple images   |     |
+-------------------+-------------------+-------------------+-----+
| *1.2.5.8.14.4*    | Algorithm Name    | "Mass Maker"      |     |
+-------------------+-------------------+-------------------+-----+
| *1.2.5.8.14.5*    | Algorithm Version | "V1.9"            |     |
+-------------------+-------------------+-------------------+-----+
| *1.2.5.8.14.6*    | [Observation      |                   |     |
|                   | Context content   |                   |     |
|                   | items]            |                   |     |
+-------------------+-------------------+-------------------+-----+
| *1.2.5.8.14.7*    | Single Image      | Mammography       |     |
|                   | Finding           | breast density    |     |
+-------------------+-------------------+-------------------+-----+
| *1.2.5.8.14.7.1*  | Rendering Intent  | Presentation      |     |
|                   |                   | Required          |     |
+-------------------+-------------------+-------------------+-----+
| *1.2.5.8.14.7.2*  | Algorithm Name    | "Density          |     |
|                   |                   | Detector"         |     |
+-------------------+-------------------+-------------------+-----+
| *1.2.5.8.14.7.3*  | Algorithm Version | "V3.7"            |     |
+-------------------+-------------------+-------------------+-----+
| *1.2.5.8.14.7.4*  | Center            | POINT             |     |
+-------------------+-------------------+-------------------+-----+
| *                 |                   | Reference to node |     |
| 1.2.5.8.14.7.4.1* |                   | 1.1.6             |     |
+-------------------+-------------------+-------------------+-----+
| *1.2.5.8.14.7.5*  | Outline           | SCOORD            |     |
+-------------------+-------------------+-------------------+-----+
| *                 |                   | Reference to node |     |
| 1.2.5.8.14.7.5.1* |                   | 1.1.6             |     |
+-------------------+-------------------+-------------------+-----+
| *1.2.5.8.14.8*    | Single Image      | Mammography       |     |
|                   | Finding           | breast density    |     |
+-------------------+-------------------+-------------------+-----+
| *1.2.5.8.14.8.1*  | Rendering Intent  | Presentation      |     |
|                   |                   | Required          |     |
+-------------------+-------------------+-------------------+-----+
| *1.2.5.8.14.8.2*  | Algorithm Name    | "Density          |     |
|                   |                   | Detector"         |     |
+-------------------+-------------------+-------------------+-----+
| *1.2.5.8.14.8.3*  | Algorithm Version | "V3.7"            |     |
+-------------------+-------------------+-------------------+-----+
| *1.2.5.8.14.8.4*  | Center            | POINT             |     |
+-------------------+-------------------+-------------------+-----+
| *                 |                   | Reference to node |     |
| 1.2.5.8.14.8.4.1* |                   | 1.1.8             |     |
+-------------------+-------------------+-------------------+-----+
| *1.2.5.8.14.8.5*  | Outline           | SCOORD            |     |
+-------------------+-------------------+-------------------+-----+
| *                 |                   | Reference to node |     |
| 1.2.5.8.14.8.5.1* |                   | 1.1.8             |     |
+-------------------+-------------------+-------------------+-----+
| *1.2.5.8.14.8.6*  | Area of Defined   | 1 cm\ :sup:`2`    |     |
|                   | Region            |                   |     |
+-------------------+-------------------+-------------------+-----+
| *                 | Area Outline      | SCOORD            |     |
| 1.2.5.8.14.8.6.1* |                   |                   |     |
+-------------------+-------------------+-------------------+-----+
| *1.               |                   | Reference to node |     |
| 2.5.8.14.8.6.1.1* |                   | 1.1.8             |     |
+-------------------+-------------------+-------------------+-----+

More current year content:

+-------------------+-------------------+-------------------+-----+
| Node              | Code Meaning of   | Code Meaning or   | TID |
|                   | Concept Name      | Example Value     |     |
+===================+===================+===================+=====+
| 1.2.6             | Individual        |                   |     |
|                   | Impressi          |                   |     |
|                   | on/Recommendation |                   |     |
+-------------------+-------------------+-------------------+-----+
| 1.2.6.1           | Rendering Intent  | Not for           |     |
|                   |                   | Presentation      |     |
+-------------------+-------------------+-------------------+-----+
| 1.2.6.2           | Single Image      | Mammography       |     |
|                   | Finding           | breast density    |     |
+-------------------+-------------------+-------------------+-----+
| 1.2.6.2.1         | Rendering Intent  | Not for           |     |
|                   |                   | Presentation      |     |
+-------------------+-------------------+-------------------+-----+
| 1.2.6.2.2         | Algorithm Name    | "Density          |     |
|                   |                   | Detector"         |     |
+-------------------+-------------------+-------------------+-----+
| 1.2.6.2.3         | Algorithm Version | "V3.7"            |     |
+-------------------+-------------------+-------------------+-----+
| 1.2.6.2.4         | Center            | POINT             |     |
+-------------------+-------------------+-------------------+-----+
| 1.2.6.2.4.1       |                   | Reference to node |     |
|                   |                   | 1.1.2             |     |
+-------------------+-------------------+-------------------+-----+
| 1.2.6.2.5         | Outline           | SCOORD            |     |
+-------------------+-------------------+-------------------+-----+
| 1.2.6.2.5.1       |                   | Reference to node |     |
|                   |                   | 1.1.2             |     |
+-------------------+-------------------+-------------------+-----+
| 1.2.7             | Individual        | INDIVIDUAL        |     |
|                   | Impressi          |                   |     |
|                   | on/Recommendation |                   |     |
+-------------------+-------------------+-------------------+-----+
| 1.2.7.1           | Rendering Intent  | Presentation      |     |
|                   |                   | Required          |     |
+-------------------+-------------------+-------------------+-----+
| 1.2.7.2           | Single Image      | Calcification     |     |
|                   | Finding           | Cluster           |     |
+-------------------+-------------------+-------------------+-----+
| 1.2.7.2.1         | Rendering Intent  | Presentation      |     |
|                   |                   | Required          |     |
+-------------------+-------------------+-------------------+-----+
| 1.2.7.2.2         | Algorithm Name    | "Calc Cluster     |     |
|                   |                   | Detector"         |     |
+-------------------+-------------------+-------------------+-----+
| 1.2.7.2.3         | Algorithm Version | "V2.4"            |     |
+-------------------+-------------------+-------------------+-----+
| 1.2.7.2.4         | Center            | POINT             |     |
+-------------------+-------------------+-------------------+-----+
| 1.2.7.2.4.1       |                   | Reference to node |     |
|                   |                   | 1.1.3             |     |
+-------------------+-------------------+-------------------+-----+
| 1.2.7.2.5         | Outline           | SCOORD            |     |
+-------------------+-------------------+-------------------+-----+
| 1.2.7.2.5.1       |                   | Reference to node |     |
|                   |                   | 1.1.3             |     |
+-------------------+-------------------+-------------------+-----+
| 1.2.7.2.6         | Number of         | 20                |     |
|                   | Calcifications    |                   |     |
+-------------------+-------------------+-------------------+-----+
| 1.2.8             | Individual        |                   |     |
|                   | Impressi          |                   |     |
|                   | on/Recommendation |                   |     |
+-------------------+-------------------+-------------------+-----+
| 1.2.8.1           | Rendering Intent  | Presentation      |     |
|                   |                   | Required          |     |
+-------------------+-------------------+-------------------+-----+
| 1.2.8.2           | Differential      | Increase in       |     |
|                   | Dia               | number of         |     |
|                   | gnosis/Impression | calcifications    |     |
+-------------------+-------------------+-------------------+-----+
| 1.2.8.3           | Impression        | "Calcification    |     |
|                   | Description       | cluster has       |     |
|                   |                   | increased in      |     |
|                   |                   | size"             |     |
+-------------------+-------------------+-------------------+-----+
| 1.2.8.4           | Recommended       | Magnification     |     |
|                   | Follow-up         | views             |     |
+-------------------+-------------------+-------------------+-----+
| 1.2.8.5           | Certainty of      | 100%              |     |
|                   | impression        |                   |     |
+-------------------+-------------------+-------------------+-----+
| 1.2.8.6           | Algorithm Name    | "Lesion Analyzer" |     |
+-------------------+-------------------+-------------------+-----+
| 1.2.8.7           | Algorithm Version | "V1.0"            |     |
+-------------------+-------------------+-------------------+-----+
| 1.2.8.8           | Composite Feature | Calcification     |     |
|                   |                   | Cluster           |     |
+-------------------+-------------------+-------------------+-----+
| 1.2.8.8.1         | Rendering Intent  | Presentation      |     |
|                   |                   | Required          |     |
+-------------------+-------------------+-------------------+-----+
| 1.2.8.8.2         | Composite type    | Target content    |     |
|                   |                   | items are related |     |
|                   |                   | temporally        |     |
+-------------------+-------------------+-------------------+-----+
| 1.2.8.8.3         | Scope of Feature  | Feature was       |     |
|                   |                   | detected on       |     |
|                   |                   | multiple images   |     |
+-------------------+-------------------+-------------------+-----+
| 1.2.8.8.4         | Algorithm Name    | "Lesion Analyzer" |     |
+-------------------+-------------------+-------------------+-----+
| 1.2.8.8.5         | Algorithm Version | "V1.0"            |     |
+-------------------+-------------------+-------------------+-----+
| 1.2.8.8.6         | Certainty of      | 99%               |     |
|                   | Feature           |                   |     |
+-------------------+-------------------+-------------------+-----+
| 1.2.8.8.7         | Probability of    | 54%               |     |
|                   | Cancer            |                   |     |
+-------------------+-------------------+-------------------+-----+
| 1.2.8.8.8         | Pathology         | Intraductal       |     |
|                   |                   | carcinoma, low    |     |
|                   |                   | grade             |     |
+-------------------+-------------------+-------------------+-----+
| 1.2.8.8.9         | Difference in     | 4                 |     |
|                   | Number of         |                   |     |
|                   | calcifications    |                   |     |
+-------------------+-------------------+-------------------+-----+
| 1.2.8.8.9.1       |                   | Reference to node |     |
|                   |                   | 1.2.8.8.12.6      |     |
+-------------------+-------------------+-------------------+-----+
| 1.2.8.8.9.2       |                   | Reference to node |     |
|                   |                   | *1.2.8.8.13.6*    |     |
+-------------------+-------------------+-------------------+-----+
| 1.2.8.8.10        | Calcification     | Fine, linear,     |     |
|                   | type              | branching         |     |
|                   |                   | (casting)         |     |
+-------------------+-------------------+-------------------+-----+
| 1.2.8.8.11        | Calcification     | Grouped or        |     |
|                   | distribution      | clustered         |     |
+-------------------+-------------------+-------------------+-----+
| 1.2.8.8.12        | Single Image      | Calcification     |     |
|                   | Finding           | Cluster           |     |
+-------------------+-------------------+-------------------+-----+
| 1.2.8.8.12.1      | Rendering Intent  | Presentation      |     |
|                   |                   | Required          |     |
+-------------------+-------------------+-------------------+-----+
| 1.2.8.8.12.2      | Algorithm Name    | "Calc Clustering" |     |
+-------------------+-------------------+-------------------+-----+
| 1.2.8.8.12.3      | Algorithm Version | "V2.4"            |     |
+-------------------+-------------------+-------------------+-----+
| 1.2.8.8.12.4      | Center            | POINT             |     |
+-------------------+-------------------+-------------------+-----+
| 1.2.8.8.12.4.1    |                   | Reference to node |     |
|                   |                   | 1.1.1             |     |
+-------------------+-------------------+-------------------+-----+
| 1.2.8.8.12.5      | Outline           | SCOORD            |     |
+-------------------+-------------------+-------------------+-----+
| 1.2.8.8.12.5.1    |                   | Reference to node |     |
|                   |                   | 1.1.1             |     |
+-------------------+-------------------+-------------------+-----+
| 1.2.8.8.12.6      | Number of         | 6                 |     |
|                   | Calcifications    |                   |     |
+-------------------+-------------------+-------------------+-----+
| 1.2.8.8.12.7      | Single Image      | Individual        |     |
|                   | Finding           | Calcification     |     |
+-------------------+-------------------+-------------------+-----+
| 1.2.8.8.12.7.1    | Rendering Intent  | Presentation      |     |
|                   |                   | Optional          |     |
+-------------------+-------------------+-------------------+-----+
| 1.2.8.8.12.7.2    | Algorithm Name    | "Calc Detector"   |     |
+-------------------+-------------------+-------------------+-----+
| 1.2.8.8.12.7.3    | Algorithm Version | "V2.4"            |     |
+-------------------+-------------------+-------------------+-----+
| 1.2.8.8.12.7.4    | Center            | POINT             |     |
+-------------------+-------------------+-------------------+-----+
| 1.2.8.8.12.7.4.1  |                   | Reference to node |     |
|                   |                   | 1.1.1             |     |
+-------------------+-------------------+-------------------+-----+
| 1.2.8.8.12.7.5    | Outline           | SCOORD            |     |
+-------------------+-------------------+-------------------+-----+
| 1.2.8.8.12.7.5.1  |                   | Reference to node |     |
|                   |                   | 1.1.1             |     |
+-------------------+-------------------+-------------------+-----+
| 1.2.8.8.12.8      | Single Image      | Individual        |     |
|                   | Finding           | Calcification     |     |
+-------------------+-------------------+-------------------+-----+
| 1.2.8.8.12.8.1    | Rendering Intent  | Presentation      |     |
|                   |                   | Optional          |     |
+-------------------+-------------------+-------------------+-----+
| 1.2.8.8.12.8.2    | Algorithm Name    | "Calc Detector"   |     |
+-------------------+-------------------+-------------------+-----+
| 1.2.8.8.12.8.3    | Algorithm Version | "V2.4"            |     |
+-------------------+-------------------+-------------------+-----+
| 1.2.8.8.12.8.4    | Center            | POINT             |     |
+-------------------+-------------------+-------------------+-----+
| 1.2.8.8.12.8.4.1  |                   | Reference to node |     |
|                   |                   | 1.1.1             |     |
+-------------------+-------------------+-------------------+-----+
| 1.2.8.8.12.8.5    | Outline           | SCOORD            |     |
+-------------------+-------------------+-------------------+-----+
| 1.2.8.8.12.8.5.1  |                   | Reference to node |     |
|                   |                   | 1.1.1             |     |
+-------------------+-------------------+-------------------+-----+
| 1.2.8.8.12.9      | Single Image      | Individual        |     |
|                   | Finding           | Calcification     |     |
+-------------------+-------------------+-------------------+-----+
| 1.2.8.8.12.9.1    | Rendering Intent  | Presentation      |     |
|                   |                   | Optional          |     |
+-------------------+-------------------+-------------------+-----+
| 1.2.8.8.12.9.2    | Algorithm Name    | "Calc Detector"   |     |
+-------------------+-------------------+-------------------+-----+
| 1.2.8.8.12.9.3    | Algorithm Version | "V2.4"            |     |
+-------------------+-------------------+-------------------+-----+
| 1.2.8.8.12.9.4    | Center            | POINT             |     |
+-------------------+-------------------+-------------------+-----+
| 1.2.8.8.12.9.4.1  |                   | Reference to node |     |
|                   |                   | 1.1.1             |     |
+-------------------+-------------------+-------------------+-----+
| 1.2.8.8.12.9.5    | Outline           | SCOORD            |     |
+-------------------+-------------------+-------------------+-----+
| 1.2.8.8.12.9.5.1  |                   | Reference to node |     |
|                   |                   | 1.1.1             |     |
+-------------------+-------------------+-------------------+-----+
| 1.2.8.8.12.10     | Single Image      | Individual        |     |
|                   | Finding           | Calcification     |     |
+-------------------+-------------------+-------------------+-----+
| 1.2.8.8.12.10.1   | Rendering Intent  | Presentation      |     |
|                   |                   | Optional          |     |
+-------------------+-------------------+-------------------+-----+
| 1.2.8.8.12.10.2   | Algorithm Name    | "Calc Detector"   |     |
+-------------------+-------------------+-------------------+-----+
| 1.2.8.8.12.10.3   | Algorithm Version | "V2.4"            |     |
+-------------------+-------------------+-------------------+-----+
| 1.2.8.8.12.10.4   | Center            | POINT             |     |
+-------------------+-------------------+-------------------+-----+
| 1.2.8.8.12.10.4.1 |                   | Reference to node |     |
|                   |                   | 1.1.1             |     |
+-------------------+-------------------+-------------------+-----+
| 1.2.8.8.12.10.5   | Outline           | SCOORD            |     |
+-------------------+-------------------+-------------------+-----+
| 1.2.8.8.12.10.5.1 |                   | Reference to node |     |
|                   |                   | 1.1.1             |     |
+-------------------+-------------------+-------------------+-----+
| 1.2.8.8.12.11     | Single Image      | Individual        |     |
|                   | Finding           | Calcification     |     |
+-------------------+-------------------+-------------------+-----+
| 1.2.8.8.12.11.1   | Rendering Intent  | Presentation      |     |
|                   |                   | Optional          |     |
+-------------------+-------------------+-------------------+-----+
| 1.2.8.8.12.11.2   | Algorithm Name    | "Calc Detector"   |     |
+-------------------+-------------------+-------------------+-----+
| 1.2.8.8.12.11.3   | Algorithm Version | "V2.4"            |     |
+-------------------+-------------------+-------------------+-----+
| 1.2.8.8.12.11.4   | Center            | POINT             |     |
+-------------------+-------------------+-------------------+-----+
| 1.2.8.8.12.11.4.1 |                   | Reference to node |     |
|                   |                   | 1.1.1             |     |
+-------------------+-------------------+-------------------+-----+
| 1.2.8.8.12.11.5   | Outline           | SCOORD            |     |
+-------------------+-------------------+-------------------+-----+
| 1.2.8.8.12.11.5.1 |                   | Reference to node |     |
|                   |                   | 1.1.1             |     |
+-------------------+-------------------+-------------------+-----+
| 1.2.8.8.12.12     | Single Image      | Individual        |     |
|                   | Finding           | Calcification     |     |
+-------------------+-------------------+-------------------+-----+
| 1.2.8.8.12.12.1   | Rendering Intent  | Presentation      |     |
|                   |                   | Optional          |     |
+-------------------+-------------------+-------------------+-----+
| 1.2.8.8.12.12.2   | Algorithm Name    | "Calc Detector"   |     |
+-------------------+-------------------+-------------------+-----+
| 1.2.8.8.12.12.3   | Algorithm Version | "V2.4"            |     |
+-------------------+-------------------+-------------------+-----+
| 1.2.8.8.12.12.4   | Center            | POINT             |     |
+-------------------+-------------------+-------------------+-----+
| 1.2.8.8.12.12.4.1 |                   | Reference to node |     |
|                   |                   | 1.1.1             |     |
+-------------------+-------------------+-------------------+-----+
| 1.2.8.8.12.12.5   | Outline           | SCOORD            |     |
+-------------------+-------------------+-------------------+-----+
| 1.2.8.8.12.12.5.1 |                   | Reference to node |     |
|                   |                   | 1.1.1             |     |
+-------------------+-------------------+-------------------+-----+

Included content from prior mammography CAD report (see Example 2,
starting with node 1.2.4.2)

+-------------------+-------------------+-------------------+-----+
| Node              | Code Meaning of   | Code Meaning or   | TID |
|                   | Concept Name      | Example Value     |     |
+===================+===================+===================+=====+
| *1.2.8.8.13*      | Single Image      | Calcification     |     |
|                   | Finding           | Cluster           |     |
+-------------------+-------------------+-------------------+-----+
| *1.2.8.8.13.1*    | Rendering Intent  | Presentation      |     |
|                   |                   | Required          |     |
+-------------------+-------------------+-------------------+-----+
| *1.2.8.8.13.2*    | Algorithm Name    | "Calc Clustering" |     |
+-------------------+-------------------+-------------------+-----+
| *1.2.8.8.13.3*    | Algorithm Version | "V2.4"            |     |
+-------------------+-------------------+-------------------+-----+
| *1.2.8.8.13.4*    | Center            | POINT             |     |
+-------------------+-------------------+-------------------+-----+
| *1.2.8.8.13.4.1*  |                   | Reference to node |     |
|                   |                   | 1.1.5             |     |
+-------------------+-------------------+-------------------+-----+
| *1.2.8.8.13.5*    | Outline           | SCOORD            |     |
+-------------------+-------------------+-------------------+-----+
| *1.2.8.8.13.5.1*  |                   | Reference to node |     |
|                   |                   | 1.1.5             |     |
+-------------------+-------------------+-------------------+-----+
| *1.2.8.8.13.6*    | Number of         | 2                 |     |
|                   | Calcifications    |                   |     |
+-------------------+-------------------+-------------------+-----+
| *1.2.8.8.13.7*    | [Observation      |                   |     |
|                   | Context content   |                   |     |
|                   | items]            |                   |     |
+-------------------+-------------------+-------------------+-----+
| *1.2.8.8.13.8*    | Single Image      | Individual        |     |
|                   | Finding           | Calcification     |     |
+-------------------+-------------------+-------------------+-----+
| *1.2.8.8.13.8.1*  | Rendering Intent  | Presentation      |     |
|                   |                   | Optional          |     |
+-------------------+-------------------+-------------------+-----+
| *1.2.8.8.13.8.2*  | Algorithm Name    | "Calc Detector"   |     |
+-------------------+-------------------+-------------------+-----+
| *1.2.8.8.13.8.3*  | Algorithm Version | "V2.4"            |     |
+-------------------+-------------------+-------------------+-----+
| *1.2.8.8.13.8.4*  | Center            | POINT             |     |
+-------------------+-------------------+-------------------+-----+
| *                 |                   | Reference to node |     |
| 1.2.8.8.13.8.4.1* |                   | 1.1.5             |     |
+-------------------+-------------------+-------------------+-----+
| *1.2.8.8.13.8.5*  | Outline           | SCOORD            |     |
+-------------------+-------------------+-------------------+-----+
| *                 |                   | Reference to node |     |
| 1.2.8.8.13.8.5.1* |                   | 1.1.5             |     |
+-------------------+-------------------+-------------------+-----+
| *1.2.8.8.13.9*    | Single Image      | Individual        |     |
|                   | Finding           | Calcification     |     |
+-------------------+-------------------+-------------------+-----+
| *1.2.8.8.13.9.1*  | Rendering Intent  | Presentation      |     |
|                   |                   | Optional          |     |
+-------------------+-------------------+-------------------+-----+
| *1.2.8.8.13.9.2*  | Algorithm Name    | "Calc Detector"   |     |
+-------------------+-------------------+-------------------+-----+
| *1.2.8.8.13.9.3*  | Algorithm Version | "V2.4"            |     |
+-------------------+-------------------+-------------------+-----+
| *1.2.8.8.13.9.4*  | Center            | POINT             |     |
+-------------------+-------------------+-------------------+-----+
| *                 |                   | Reference to node |     |
| 1.2.8.8.13.9.4.1* |                   | 1.1.5             |     |
+-------------------+-------------------+-------------------+-----+
| *1.2.8.8.13.9.4*  | Outline           | SCOORD            |     |
+-------------------+-------------------+-------------------+-----+
| *                 |                   | Reference to node |     |
| 1.2.8.8.13.9.4.1* |                   | 1.1.5             |     |
+-------------------+-------------------+-------------------+-----+

More current year content:

+-----------+------------------------+------------------------+-----+
| Node      | Code Meaning of        | Code Meaning or        | TID |
|           | Concept Name           | Example Value          |     |
+===========+========================+========================+=====+
| 1.3       | Summary of Detections  | Succeeded              |     |
+-----------+------------------------+------------------------+-----+
| 1.3.1     | Successful Detections  |                        |     |
+-----------+------------------------+------------------------+-----+
| 1.3.1.1   | Detection Performed    | Mammography breast     |     |
|           |                        | density                |     |
+-----------+------------------------+------------------------+-----+
| 1.3.1.1.1 | Algorithm Name         | "Density Detector"     |     |
+-----------+------------------------+------------------------+-----+
| 1.3.1.1.2 | Algorithm Version      | "V3.7"                 |     |
+-----------+------------------------+------------------------+-----+
| 1.3.1.1.3 |                        | Reference to node      |     |
|           |                        | 1.1.1                  |     |
+-----------+------------------------+------------------------+-----+
| 1.3.1.1.4 |                        | Reference to node      |     |
|           |                        | 1.1.2                  |     |
+-----------+------------------------+------------------------+-----+
| 1.3.1.1.5 |                        | Reference to node      |     |
|           |                        | 1.1.3                  |     |
+-----------+------------------------+------------------------+-----+
| 1.3.1.1.6 |                        | Reference to node      |     |
|           |                        | 1.1.4                  |     |
+-----------+------------------------+------------------------+-----+
| 1.3.1.2   | Detection Performed    | Individual             |     |
|           |                        | Calcification          |     |
+-----------+------------------------+------------------------+-----+
| 1.3.1.2.1 | Algorithm Name         | "Calc Detector"        |     |
+-----------+------------------------+------------------------+-----+
| 1.3.1.2.2 | Algorithm Version      | "V2.4"                 |     |
+-----------+------------------------+------------------------+-----+
| 1.3.1.2.3 |                        | Reference to node      |     |
|           |                        | 1.1.1                  |     |
+-----------+------------------------+------------------------+-----+
| 1.3.1.2.4 |                        | Reference to node      |     |
|           |                        | 1.1.2                  |     |
+-----------+------------------------+------------------------+-----+
| 1.3.1.2.5 |                        | Reference to node      |     |
|           |                        | 1.1.3                  |     |
+-----------+------------------------+------------------------+-----+
| 1.3.1.2.6 |                        | Reference to node      |     |
|           |                        | 1.1.4                  |     |
+-----------+------------------------+------------------------+-----+
| 1.3.1.3   | Detection Performed    | Calcification Cluster  |     |
+-----------+------------------------+------------------------+-----+
| 1.3.1.3.1 | Algorithm Name         | "Calc Clustering"      |     |
+-----------+------------------------+------------------------+-----+
| 1.3.1.3.2 | Algorithm Version      | "V2.4"                 |     |
+-----------+------------------------+------------------------+-----+
| 1.3.1.3.3 |                        | Reference to node      |     |
|           |                        | 1.1.1                  |     |
+-----------+------------------------+------------------------+-----+
| 1.3.1.4   | Detection Performed    | Calcification Cluster  |     |
+-----------+------------------------+------------------------+-----+
| 1.3.1.4.1 | Algorithm Name         | "Calc Cluster          |     |
|           |                        | Detector"              |     |
+-----------+------------------------+------------------------+-----+
| 1.3.1.4.2 | Algorithm Version      | "V2.4"                 |     |
+-----------+------------------------+------------------------+-----+
| 1.3.1.4.3 |                        | Reference to node      |     |
|           |                        | 1.1.1                  |     |
+-----------+------------------------+------------------------+-----+
| 1.3.1.4.4 |                        | Reference to node      |     |
|           |                        | 1.1.2                  |     |
+-----------+------------------------+------------------------+-----+
| 1.3.1.4.5 |                        | Reference to node      |     |
|           |                        | 1.1.3                  |     |
+-----------+------------------------+------------------------+-----+
| 1.3.1.4.6 |                        | Reference to node      |     |
|           |                        | 1.1.4                  |     |
+-----------+------------------------+------------------------+-----+
| 1.4       | Summary of Analyses    | Succeeded              |     |
+-----------+------------------------+------------------------+-----+
| 1.4.1     | Successful Analyses    |                        |     |
+-----------+------------------------+------------------------+-----+
| 1.4.1.1   | Analysis Performed     | Mass Correlation       |     |
+-----------+------------------------+------------------------+-----+
| 1.4.1.1.1 | Algorithm Name         | "Mass Maker"           |     |
+-----------+------------------------+------------------------+-----+
| 1.4.1.1.2 | Algorithm Version      | "V1.9"                 |     |
+-----------+------------------------+------------------------+-----+
| 1.4.1.1.3 |                        | Reference to node      |     |
|           |                        | 1.1.2                  |     |
+-----------+------------------------+------------------------+-----+
| 1.4.1.1.4 |                        | Reference to node      |     |
|           |                        | 1.1.4                  |     |
+-----------+------------------------+------------------------+-----+
| 1.4.1.2   | Analysis Performed     | Temporal Correlation   |     |
+-----------+------------------------+------------------------+-----+
| 1.4.1.2.1 | Algorithm Name         | "Temporal Change"      |     |
+-----------+------------------------+------------------------+-----+
| 1.4.1.2.2 | Algorithm Version      | "V0.1"                 |     |
+-----------+------------------------+------------------------+-----+
| 1.4.1.2.3 |                        | Reference to node      |     |
|           |                        | 1.1.2                  |     |
+-----------+------------------------+------------------------+-----+
| 1.4.1.2.4 |                        | Reference to node      |     |
|           |                        | 1.1.4                  |     |
+-----------+------------------------+------------------------+-----+
| 1.4.1.2.5 |                        | Reference to node      |     |
|           |                        | 1.1.6                  |     |
+-----------+------------------------+------------------------+-----+
| 1.4.1.2.6 |                        | Reference to node      |     |
|           |                        | 1.1.8                  |     |
+-----------+------------------------+------------------------+-----+
| 1.4.1.3   | Analysis Performed     | Individual Impression  |     |
|           |                        | / Recommendation       |     |
|           |                        | Analysis               |     |
+-----------+------------------------+------------------------+-----+
| 1.4.1.3.1 | Algorithm Name         | "Lesion Analyzer"      |     |
+-----------+------------------------+------------------------+-----+
| 1.4.1.3.2 | Algorithm Version      | "V1.0"                 |     |
+-----------+------------------------+------------------------+-----+
| 1.4.1.3.3 |                        | Reference to node      |     |
|           |                        | 1.1.2                  |     |
+-----------+------------------------+------------------------+-----+
| 1.4.1.3.4 |                        | Reference to node      |     |
|           |                        | 1.1.4                  |     |
+-----------+------------------------+------------------------+-----+
| 1.4.1.3.5 |                        | Reference to node      |     |
|           |                        | 1.1.6                  |     |
+-----------+------------------------+------------------------+-----+
| 1.4.1.3.6 |                        | Reference to node      |     |
|           |                        | 1.1.8                  |     |
+-----------+------------------------+------------------------+-----+
| 1.4.1.4   | Analysis Performed     | Overall Impression /   |     |
|           |                        | Recommendation         |     |
|           |                        | Analysis               |     |
+-----------+------------------------+------------------------+-----+
| 1.4.1.4.1 | Algorithm Name         | "Mammogram Analyzer"   |     |
+-----------+------------------------+------------------------+-----+
| 1.4.1.4.2 | Algorithm Version      | "V1.0"                 |     |
+-----------+------------------------+------------------------+-----+
| 1.4.1.4.3 |                        | Reference to node      |     |
|           |                        | 1.1.2                  |     |
+-----------+------------------------+------------------------+-----+
| 1.4.1.4.4 |                        | Reference to node      |     |
|           |                        | 1.1.4                  |     |
+-----------+------------------------+------------------------+-----+
| 1.4.1.4.5 |                        | Reference to node      |     |
|           |                        | 1.1.6                  |     |
+-----------+------------------------+------------------------+-----+
| 1.4.1.4.6 |                        | Reference to node      |     |
|           |                        | 1.1.8                  |     |
+-----------+------------------------+------------------------+-----+

.. _sect_E.4:

CAD Operating Point
-------------------

Computer-aided detection algorithms often compute an internal "CAD
score" for each Single Image Finding detected by the algorithm. In some
implementations the algorithms then group the findings into "bins" as a
function of their CAD score. The number of bins is a function of the
algorithm and the manufacturer's implementation, and must be one or
more. The bins allow an application that is displaying CAD marks to
provide a number of operating points on the Free-response
Receiver-Operating Characteristic (FROC) curve for the algorithm, as
illustrated in `figure_title <#figure_E.4-1>`__.

This is accomplished by displaying all CAD marks of Rendering Intent
"Presentation Required" or "Presentation Optional" according to the
following rules:

-  if the display application's Operating Point is 0, only marks with a
   Rendering Intent = "Presentation Required" are displayed

-  if the display application's Operating Point is 1, then marks with a
   Rendering Intent = "Presentation Required" and marks with a Rendering
   Intent = "Presentation Optional" with a CAD Operating Point = 1 are
   displayed

-  if the display application's Operating Point is n, then marks with a
   Rendering Intent = "Presentation Required" and marks with a Rendering
   Intent = "Presentation Optional" with a CAD Operating Point <= n are
   displayed

.. _sect_E.5:

Mammography CAD SR and For Processing / For Presentation Images
---------------------------------------------------------------

If a Mammography CAD SR Instance references Digital Mammography X-ray
Image Storage - For Processing Instances, but a review workstation has
access only to Digital Mammography X-Ray Image Storage - For
Presentation Instances, the following steps are recommended in order to
display such Mammography CAD SR content with Digital Mammography X-Ray
Image - For Presentation Instances.

-  In most scenarios, the Mammography CAD SR Instance is assigned to the
   same DICOM Patient and Study as the corresponding Digital Mammography
   "For Processing" and "For Presentation" image Instances.

-  If a workstation has a Mammography CAD SR Instance, but does not have
   images for the same DICOM Patient and Study, the workstation may use
   the Patient and Study Attributes of the Mammography CAD SR Instance
   in order to Query/Retrieve the Digital Mammography "For Presentation"
   images for that Patient and Study.

-  Once a workstation has the Mammography CAD SR Instance and Digital
   Mammography "For Presentation" image Instances for the Patient and
   Study, the Source Image Sequence (0008,2112) Attribute of each
   Digital Mammography "For Presentation" Instance will reference the
   corresponding Digital Mammography "For Processing" Instance. The
   workstation can match the referenced Digital Mammography "For
   Processing" Instance to a Digital Mammography "For Processing"
   Instance referenced in the Mammography CAD SR.

-  The workstation should check for Spatial Locations Preserved
   (0028,135A) in the Source Image Sequence of each Digital Mammography
   "For Presentation" image Instance, to determine whether it is
   spatially equivalent to the corresponding Digital Mammography "For
   Processing" image Instance.

-  If the value of Spatial Locations Preserved (0028,135A) is YES, then
   the CAD results should be displayed.

-  If the value of Spatial Locations Preserved (0028,135A) is NO, then
   the CAD results should not be displayed.

-  If Spatial Locations Preserved (0028,135A) is not present, whether or
   not the images are spatially equivalent is not known. If the
   workstation chooses to proceed with attempting to display CAD
   results, then compare the Image Library (see ) content item values of
   the Mammography CAD SR Instance to the associated Attribute values in
   the corresponding Digital Mammography "For Presentation" image
   Instance. The content items (111044, DCM, "Patient Orientation Row"),
   (111043, DCM, "Patient Orientation Column"), (111026, DCM,
   "Horizontal Pixel Spacing"), and (111066, DCM, "Vertical Pixel
   Spacing") may be used for this purpose. If the values do not match,
   the workstation needs to adjust the coordinates of the findings in
   the Mammography CAD SR content to match the spatial characteristics
   of the Digital Mammography "For Presentation" image Instance.

