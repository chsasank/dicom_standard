.. _chapter_JJ:

Surface Mesh Representation (Informative)
=========================================

For a general introduction into the underlying principles used in the
see:

Foley & van Dam [et al], Computer Graphics: Principles and Practice,
Second Edition, Addison-Wesley, 1990.

.. _sect_JJ.1:

Multi-Dimensional Vectors
-------------------------

The dimensionality of the Vectors Macro () is not restricted to
accommodate broader use of this macro in the future. Usage beyond
3-dimensional Euclidean geometry is possible The Vectors Macro may be
used to represent any multi-dimensional numerical entity, like a set of
parameters that are assigned to a voxel in an image or a primitive in a
surface mesh.

Examples:

In electroanatomical mapping, one or more tracked catheters are used to
sample the electrophysiological parameters of the inner surface of the
heart. Using magnetic tracking information, a set of vertices is
generated according to the positions the catheter was moved to during
the examination. In addition to its 3D spatial position each vertex is
loaded with a 7D-Vector containing the time it was measured at, the
direction the catheter pointed to, the maximal potential measured in
that point, the duration of that potential and the point in time
(relative to the heart cycle) the potential was measured.

For biomechanical simulation the mechanical properties of a vertex or
voxel can be represented with a n-dimensional vector.

.. _sect_JJ.2:

Encoding Examples
-----------------

The following example demonstrates the usage of the Surface Mesh Module
for a tetrahedron.

+-----------------+-------------+-----------------+-----------------+
| **Name**        | **Tag**     | **Value**       | **Comment**     |
+=================+=============+=================+=================+
| Number of       | (0066,0001) | 1               |                 |
| Surfaces        |             |                 |                 |
+-----------------+-------------+-----------------+-----------------+
| Surface         | (0066,0002) |                 |                 |
| Sequence        |             |                 |                 |
+-----------------+-------------+-----------------+-----------------+
| >Surface Number | (0066,0003) | 1               |                 |
+-----------------+-------------+-----------------+-----------------+
| >Surface        | (0066,0004) | Test Surface    |                 |
| Comments        |             |                 |                 |
+-----------------+-------------+-----------------+-----------------+
| >Surface        | (0066,0009) | YES             |                 |
| Processing      |             |                 |                 |
+-----------------+-------------+-----------------+-----------------+
| >Surface        | (0066,000A) | 1.0             |                 |
| Processing      |             |                 |                 |
| Ratio           |             |                 |                 |
+-----------------+-------------+-----------------+-----------------+
| >Surface        | (0066,000B) | Moved Object    |                 |
| Processing      |             |                 |                 |
| Description     |             |                 |                 |
+-----------------+-------------+-----------------+-----------------+
| >Surface        | (0066,0035) |                 |                 |
| Processing      |             |                 |                 |
| Algorithm       |             |                 |                 |
| Identification  |             |                 |                 |
| Sequence        |             |                 |                 |
+-----------------+-------------+-----------------+-----------------+
| >>Algorithm     | (0066,002F) |                 |                 |
| Family Code     |             |                 |                 |
| Sequence        |             |                 |                 |
+-----------------+-------------+-----------------+-----------------+
| >>>Code Value   | (0008,0100) | 123109          |                 |
+-----------------+-------------+-----------------+-----------------+
| >>>Coding       | (0008,0102) | DCM             |                 |
| Scheme          |             |                 |                 |
| Designator      |             |                 |                 |
+-----------------+-------------+-----------------+-----------------+
| >>>Code Meaning | (0008,0104) | Manual          |                 |
|                 |             | Processing      |                 |
+-----------------+-------------+-----------------+-----------------+
| >>Algorithm     | (0066,0030) |                 |                 |
| Name Code       |             |                 |                 |
| Sequence        |             |                 |                 |
+-----------------+-------------+-----------------+-----------------+
| >>>Code Value   | (0008,0100) | AA01            |                 |
+-----------------+-------------+-----------------+-----------------+
| >>>Coding       | (0008,0102) | ICCAS           |                 |
| Scheme          |             |                 |                 |
| Designator      |             |                 |                 |
+-----------------+-------------+-----------------+-----------------+
| >>>Code Meaning | (0008,0104) | Interactive     |                 |
|                 |             | Shift           |                 |
+-----------------+-------------+-----------------+-----------------+
| >>Algorithm     | (0066,0036) | Interactive     |                 |
| Name            |             | Shift           |                 |
+-----------------+-------------+-----------------+-----------------+
| >>Algorithm     | (0066,0031) | "V1.0"          |                 |
| Version         |             |                 |                 |
+-----------------+-------------+-----------------+-----------------+
| >>Algorithm     | (0066,0032) | "x = 5 y = 1 z  |                 |
| Parameters      |             | = 0"            |                 |
+-----------------+-------------+-----------------+-----------------+
| >Recommended    | (0062,000C) | FFFFH           |                 |
| Display         |             |                 |                 |
| Grayscale Value |             |                 |                 |
+-----------------+-------------+-----------------+-----------------+
| >Recommended    | (0062,000D) | FFFF\8080\8080  |                 |
| Display CIELab  |             |                 |                 |
| Value           |             |                 |                 |
+-----------------+-------------+-----------------+-----------------+
| >Recommended    | (0066,000C) | 1.0             |                 |
| Presentation    |             |                 |                 |
| Opacity         |             |                 |                 |
+-----------------+-------------+-----------------+-----------------+
| >Recommended    | (0066,000D) | SURFACE         |                 |
| Presentation    |             |                 |                 |
| Type            |             |                 |                 |
+-----------------+-------------+-----------------+-----------------+
| >Finite Volume  | (0066,000E) | YES             |                 |
+-----------------+-------------+-----------------+-----------------+
| >Manifold       | (0066,0010) | YES             |                 |
+-----------------+-------------+-----------------+-----------------+
| >Surface Points | (0066,0011) |                 |                 |
| Sequence        |             |                 |                 |
+-----------------+-------------+-----------------+-----------------+
| >>Number Of     | (0066,0015) | 4               |                 |
| Surface Points  |             |                 |                 |
+-----------------+-------------+-----------------+-----------------+
| >>Point         | (0066,0016) | -5.\            | 4 triplets. The |
| Coordinates     |             | -3.727\-4.757\\ | points are      |
| Data            |             |                 | marked a,b,c,d  |
|                 |             | 5.\             | in              |
|                 |             | -3.707\-4.757\\ | `fig            |
|                 |             |                 | ure_title <#fig |
|                 |             | 0.              | ure_JJ.2-1>`__. |
|                 |             | \7.454\-4.757\\ |                 |
|                 |             |                 |                 |
|                 |             | 0.\0.\8.315     |                 |
+-----------------+-------------+-----------------+-----------------+
| >>Point         | (0066,0017) | 0.              |                 |
| Position        |             | 001\0.001\0.001 |                 |
| Accuracy        |             |                 |                 |
+-----------------+-------------+-----------------+-----------------+
| >>Mean Point    | (0066,0018) | 10.0            |                 |
| Distance        |             |                 |                 |
+-----------------+-------------+-----------------+-----------------+
| >>Maximum Point | (0066,0019) | 10.0            |                 |
| Distance        |             |                 |                 |
+-----------------+-------------+-----------------+-----------------+
| >>Points        | (0066,001A) | -5.\            | 2 triplets      |
| Bounding Box    |             | -3.727\-4.757\\ |                 |
| Coordinates     |             |                 |                 |
|                 |             | 5.\7.454\8.315  |                 |
+-----------------+-------------+-----------------+-----------------+
| >>Axis of       | (0066,001B) | 0.0\0.0\1.0     |                 |
| Rotation        |             |                 |                 |
+-----------------+-------------+-----------------+-----------------+
| >>Center of     | (0066,001C) | 0.0\0.0\0.0     |                 |
| Rotation        |             |                 |                 |
+-----------------+-------------+-----------------+-----------------+
| >Surface Points | (0066,0012) | <empty>         |                 |
| Normals         |             |                 |                 |
| Sequence        |             |                 |                 |
+-----------------+-------------+-----------------+-----------------+
| >Surface Mesh   | (0066,0013) |                 |                 |
| Primitives      |             |                 |                 |
| Sequence        |             |                 |                 |
+-----------------+-------------+-----------------+-----------------+
| >>Vertex Point  | (0066,0025) | <empty>         |                 |
| Index List      |             |                 |                 |
+-----------------+-------------+-----------------+-----------------+
| >>Edge Point    | (0066,0024) | <empty>         |                 |
| Index List      |             |                 |                 |
+-----------------+-------------+-----------------+-----------------+
| >>Triangle      | (0066,0023) | 1\3\2\1\        | The second      |
| Point Index     |             | 2\4\2\3\4\3\1\4 | triangle is the |
| List            |             |                 | one marked      |
|                 |             |                 | green in        |
|                 |             |                 | `fig            |
|                 |             |                 | ure_title <#fig |
|                 |             |                 | ure_JJ.2-1>`__. |
+-----------------+-------------+-----------------+-----------------+
| >>Triangle      | (0066,0026) | <empty>         |                 |
| Strip Sequence  |             |                 |                 |
+-----------------+-------------+-----------------+-----------------+
| >>Triangle Fan  | (0066,0027) | <empty>         |                 |
| Sequence        |             |                 |                 |
+-----------------+-------------+-----------------+-----------------+
| >>Line Sequence | (0066,0028) | <empty>         |                 |
+-----------------+-------------+-----------------+-----------------+
| >>Facet         | (0066,0034) | <empty>         |                 |
| Sequence        |             |                 |                 |
+-----------------+-------------+-----------------+-----------------+

.. note::

   When the actual values are binary a text string is shown.

