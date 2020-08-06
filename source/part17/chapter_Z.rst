.. _chapter_Z:

X-Ray Isocenter Reference Transformations (Informative)
=======================================================

.. _sect_Z.1:

Introduction
------------

The Isocenter Reference System Attributes describe the 3D geometry of
the X-Ray equipment composed by the X-Ray positioner and the X-Ray
table.

These Attributes define three coordinate systems in the 3D space:

-  Isocenter coordinate system

-  Positioner coordinate system

-  Table coordinate system

The Isocenter Reference System Attributes describe the relationship
between the 3D coordinates of a point in the table coordinate system and
the 3D coordinates of such point in the positioner coordinate system
(both systems moving in the equipment), by using the Isocenter
coordinate system that is fixed in the equipment.

.. _sect_Z.2:

Positioner Coordinate System Transformations
--------------------------------------------

Any point of the Positioner coordinate system (P\ :sub:`Xp`,
P\ :sub:`Yp`, P\ :sub:`Zp`) can be expressed in the Isocenter coordinate
system (P\ :sub:`X`, P\ :sub:`Y`, P\ :sub:`Z`) by applying the following
transformation:

.. math::

    (P<subscript>X</subscript>, P<subscript>Y</subscript>, P<subscript>Z</subscript>)<superscript>T</superscript> = (R<subscript>2</subscript>
                       <superscript>.</superscript>R<subscript>1</subscript>)<superscript>T</superscript>
                       <superscript>.</superscript>(R<subscript>3</subscript>
                       <superscript>T</superscript>
                       <superscript>.</superscript>(P<subscript>Xp</subscript>, P<subscript>Yp</subscript>, P<subscript>Zp</subscript>)<superscript>T</superscript>) 

And inversely, any point of the Isocenter coordinate system (P\ **X**,
P\ **Y**, P\ **Z**) can be expressed in the Positioner coordinate system
(P\ **Xp**, P\ **Yp**, P\ **Zp**) by applying the following
transformation:

.. math::

   (P<subscript>Xp</subscript>, P<subscript>Yp</subscript>, P<subscript>Zp</subscript>)<superscript>T</superscript>= R<subscript>3</subscript>
                       <superscript>.</superscript>((R<subscript>2</subscript>
                       <superscript>.</superscript>R<subscript>1</subscript>)<superscript>.</superscript>(P<subscript>X</subscript>, P<subscript>Y</subscript>, P<subscript>Z</subscript>)<superscript>T</superscript>)

Where R\ :sub:`1`, R\ :sub:`2` and R\ :sub:`3` are defined as follows:

.. _sect_Z.3:

Table Coordinate System Transformations
---------------------------------------

Any point of the table coordinate system (P\ :sub:`Xt`, P\ :sub:`Yt`,
P\ :sub:`Zt`) (see `figure_title <#figure_Z-1>`__) can be expressed in
the Isocenter Reference coordinate system (P\ :sub:`X`, P\ :sub:`Y`,
P\ :sub:`Z`) by applying the following transformation:

.. math::

    (P<subscript>X</subscript>, P<subscript>Y</subscript>, P<subscript>Z</subscript>)<superscript>T</superscript>= (R<subscript>3</subscript>
                       <superscript>.</superscript>R<subscript>2</subscript>
                       <superscript>.</superscript>R<subscript>1</subscript>)<superscript>T</superscript>
                       <superscript>.</superscript>(P<subscript>Xt</subscript>, P<subscript>Yt</subscript>, P<subscript>Zt</subscript>)<superscript>T</superscript>+ (T<subscript>X</subscript>, T<subscript>Y</subscript>, T<subscript>Z</subscript>)<superscript>T</superscript>
                   

And inversely, any point of the Isocenter coordinate system
(P\ :sub:`X`, P\ :sub:`Y`, P\ :sub:`Z`) can be expressed in the table
coordinate system (P\ :sub:`Xt`, P\ :sub:`Yt`, P\ :sub:`Zt`) by applying
the following transformation:

.. math::

    (P<subscript>Xt</subscript>, P<subscript>Yt</subscript>, P<subscript>Zt</subscript>)<superscript>T</superscript>= (R<subscript>3</subscript>
                       <superscript>.</superscript>R<subscript>2</subscript>
                       <superscript>.</superscript>R<subscript>1</subscript>)<superscript>.</superscript>((P<subscript>X</subscript>, P<subscript>Y</subscript>, P<subscript>Z</subscript>)<superscript>T</superscript>- (T<subscript>X</subscript>, T<subscript>Y</subscript>, T<subscript>Z</subscript>)<superscript>T</superscript>) 

Where R\ :sub:`1`, R\ :sub:`2` and R\ :sub:`3` are defined as follows:

