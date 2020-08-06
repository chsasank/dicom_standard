.. _chapter_YY:

Compound and Combined Graphic Objects in Presentation States (Informative)
==========================================================================

Presentation States may contain Compound Graphics and combined graphic
objects. Two illustrative examples are given in this informative annex
to explain these two concepts.

First, an example of a Compound Graphic is given, an AXIS object, and
secondly an example of a combined graphic object is given, a distance
line.

The rendered appearance of the Compound Graphics (such as illustrated in
`figure_title <#figure_YY-1>`__) are recommendations and are not
mandatory. For example, the Compound Graphic 'AXIS' can look slightly
different on different viewing workstations.

.. _sect_YY.1:

An Example of The Compound Graphic 'axis'
-----------------------------------------

The AXIS from `figure_title <#figure_YY-1>`__ is defined in the
following Compound Graphic Sequence (0070,0209) (see the following
`table_title <#table_YY-1>`__). An AXIS object is typically used for
measurement purposes.

.. table:: Graphic Annotation Module Attributes

   ============================== =========== ===================
   **Attribute Name**             **Tag**     **Attribute Value**
   ============================== =========== ===================
   Graphic Annotation Sequence    (0070,0001) …
   …                                          
   >Compound Graphic Sequence     (0070,0209) 
   >>Compound Graphic Instance ID (0070,0226) 1
   >>Compound Graphic Units       (0070,0282) PIXEL
   >>Graphic Dimensions           (0070,0020) 2
   >>Number of Graphic Points     (0070,0021) 2
   >>Graphic Data                 (0070,0022) 10\10\150\10
   >>Compound Graphic Type        (0070,0294) AXIS
   >>Major Ticks Sequence         (0070,0287) 
   %item                                      
   >>>Tick Position               (0070,0288) 0
   >>>Tick Label                  (0070,0289) 20
   %enditem                                   
   %item                                      
   >>>Tick Position               (0070,0288) 0.25
   >>>Tick Label                  (0070,0289) 30
   %enditem                                   
   %item                                      
   >>>Tick Position               (0070,0288) 0.5
   >>>Tick Label                  (0070,0289) 40
   %enditem                                   
   %item                                      
   >>>Tick Position               (0070,0288) 0.75
   >>>Tick Label                  (0070,0289) 50
   %enditem                                   
   %item                                      
   >>>Tick Position               (0070,0288) 1.0
   >>>Tick Label                  (0070,0289) 60
   %enditem                                   
   %endseq                                    
   >>Tick Alignment               (0070,0274) CENTER
   >>Tick Label Alignment         (0070,0279) BOTTOM
   >>Show Tick Label              (0070,0278) Y
   ============================== =========== ===================

The following table shows the simple graphic objects for an axis. The
breakdown of the axis into simple graphics is up to the implementation.
The Compound Graphic Instance ID (0070,0226) is used to relate the
compound and the simple representation. To keep the example short only
the first major tick is shown.

.. table:: Graphic Annotation Module Attributes

   +-----------------+-------------+-----------------+-----------------+
   | **Attribute     | **Tag**     | **Attribute     | **Comment**     |
   | Name**          |             | Value**         |                 |
   +=================+=============+=================+=================+
   | Graphic         | (0070,0001) | …               |                 |
   | Annotation      |             |                 |                 |
   | Sequence        |             |                 |                 |
   +-----------------+-------------+-----------------+-----------------+
   | …               |             |                 |                 |
   +-----------------+-------------+-----------------+-----------------+
   | >Text Object    | (0070,0008) |                 | Tick Labels     |
   | Sequence        |             |                 |                 |
   +-----------------+-------------+-----------------+-----------------+
   | >>Anchor Point  | (0070,0004) | PIXEL           | First Tick      |
   | Annotation      |             |                 | Label           |
   | Units           |             |                 |                 |
   +-----------------+-------------+-----------------+-----------------+
   | >>Anchor Point  | (0070,0014) | 8/22            |                 |
   +-----------------+-------------+-----------------+-----------------+
   | >>Anchor Point  | (0070,0015) | N               |                 |
   | Visibility      |             |                 |                 |
   +-----------------+-------------+-----------------+-----------------+
   | >>Unformatted   | (0070,0006) | 20              |                 |
   | Text Value      |             |                 |                 |
   +-----------------+-------------+-----------------+-----------------+
   | >>Compound      | (0070,0226) | 1               |                 |
   | Graphic         |             |                 |                 |
   | Instance ID     |             |                 |                 |
   +-----------------+-------------+-----------------+-----------------+
   | …               |             |                 |                 |
   +-----------------+-------------+-----------------+-----------------+
   | >Graphic Object | (0070,0009) |                 | Primary Axis    |
   | Sequence        |             |                 | Line            |
   +-----------------+-------------+-----------------+-----------------+
   | >>Graphic       | (0070,0005) | PIXEL           |                 |
   | Annotation      |             |                 |                 |
   | Units           |             |                 |                 |
   +-----------------+-------------+-----------------+-----------------+
   | >>Graphic       | (0070,0020) | 2               |                 |
   | Dimensions      |             |                 |                 |
   +-----------------+-------------+-----------------+-----------------+
   | >>Number of     | (0070,0021) | 2               |                 |
   | Graphic Points  |             |                 |                 |
   +-----------------+-------------+-----------------+-----------------+
   | >>Graphic Data  | (0070,0022) | 10\10\150\10    |                 |
   +-----------------+-------------+-----------------+-----------------+
   | >>Graphic Type  | (0070,0023) | POLYLINE        |                 |
   +-----------------+-------------+-----------------+-----------------+
   | >>Compound      | (0070,0226) | 1               |                 |
   | Graphic         |             |                 |                 |
   | Instance ID     |             |                 |                 |
   +-----------------+-------------+-----------------+-----------------+
   | …               |             |                 |                 |
   +-----------------+-------------+-----------------+-----------------+
   | >>Graphic       | (0070,0005) | PIXEL           | First Major     |
   | Annotation      |             |                 | Tick            |
   | Units           |             |                 |                 |
   +-----------------+-------------+-----------------+-----------------+
   | >>Graphic       | (0070,0020) | 2               |                 |
   | Dimensions      |             |                 |                 |
   +-----------------+-------------+-----------------+-----------------+
   | >>Number of     | (0070,0021) | 2               |                 |
   | Graphic Points  |             |                 |                 |
   +-----------------+-------------+-----------------+-----------------+
   | >>Graphic Data  | (0070,0022) | 10\5\10\15      |                 |
   +-----------------+-------------+-----------------+-----------------+
   | >>Graphic Type  | (0070,0023) | POLYLINE        |                 |
   +-----------------+-------------+-----------------+-----------------+
   | >>Compound      | (0070,0226) | 1               |                 |
   | Graphic         |             |                 |                 |
   | Instance ID     |             |                 |                 |
   +-----------------+-------------+-----------------+-----------------+
   | …               |             |                 |                 |
   +-----------------+-------------+-----------------+-----------------+

.. _sect_YY.2:

An Example of Distance Line Defined As A Combined Graphic Object
----------------------------------------------------------------

Now, a distance line is defined as a combined graphic object, i.e.,
grouping a text object with a polyline graphic object (see
`figure_title <#figure_YY-2>`__). Distance lines are typically used for
measurements and for computing the grayscale values along this line to
build up a profile curve.

This simple example is intended to show how the Graphic Group ID
(0070,0295) is used for grouping of graphic annotations.

.. table:: Graphic Group Module

   ========================== =========== ===================
   **Attribute Name**         **Tag**     **Attribute Value**
   ========================== =========== ===================
   Graphic Group Sequence     (0070,0234) 
   >Graphic Group ID          (0070,0295) 1
   >Graphic Group Label       (0070,0207) DistanceLine
   >Graphic Group Description (0070,0208) Measurement Tool
   ========================== =========== ===================

.. table:: Graphic Annotation Module Attributes

   =============================== =========== ===================
   **Attribute Name**              **Tag**     **Attribute Value**
   =============================== =========== ===================
   Graphic Annotation Sequence     (0070,0001) …
   …                                           
   >Text Object Sequence           (0070,0008) 
   >>Anchor Point Annotation Units (0070,0004) PIXEL
   >>Anchor Point                  (0070,0014) 70/20
   >>Anchor Point Visibility       (0070,0015) N
   >>Unformatted Text Value        (0070,0006) 52.20 mm
   >>Graphic Group ID              (0070,0295) 1
   …                                           
   >Compound Object Sequence       (0070,0009) 
   >>Graphic Annotation Units      (0070,0005) PIXEL
   >>Graphic Dimensions            (0070,0020) 2
   >>Number of Graphic Points      (0070,0021) 2
   >>Graphic Data                  (0070,0022) 10\10\150\10
   >>Graphic Type                  (0070,0023) POLYLINE
   >>Graphic Group ID              (0070,0295) 1
   =============================== =========== ===================

