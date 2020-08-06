.. _chapter_P:

Transforms and Mappings (Informative)
=====================================

The Affine Transform Matrix is of the following form.

This matrix requires the bottom row to be [0 0 0 1] to preserve the
homogeneous coordinates.

The matrix can be of type: RIGID, RIGID_SCALE and AFFINE. These
different types represent different conditions on the allowable values
for the matrix elements.

-  RIGID:

   This transform requires the matrix obey orthonormal transformation
   properties:

   for all combinations of j = 1,2,3 and k = 1,2,3 where δ = 1 for i = j
   and zero otherwise.

   The expansion into non-matrix equations is:

   -  M\ :sub:`11` M\ :sub:`11` + M\ :sub:`21` M\ :sub:`21` +
      M\ :sub:`31` M\ :sub:`31` = 1 where j = 1, k = 1

   -  M\ :sub:`11` M\ :sub:`12` + M\ :sub:`21` M\ :sub:`22` +
      M\ :sub:`31` M\ :sub:`32` = 0 where j = 1, k = 2

   -  M\ :sub:`11` M\ :sub:`13` + M\ :sub:`21` M\ :sub:`23` +
      M\ :sub:`31` M\ :sub:`33` = 0 where j = 1, k = 3

   -  M\ :sub:`12` M\ :sub:`11` + M\ :sub:`22` M\ :sub:`21` +
      M\ :sub:`32` M\ :sub:`31` = 0 where j = 2, k = 1

   -  M\ :sub:`12` M\ :sub:`12` + M\ :sub:`22` M\ :sub:`22` +
      M\ :sub:`32` M\ :sub:`32` = 1 where j = 2, k = 2

   -  M\ :sub:`12` M\ :sub:`13` + M\ :sub:`22` M\ :sub:`23` +
      M\ :sub:`32` M\ :sub:`33` = 0 where j = 2, k = 3

   -  M\ :sub:`13` M\ :sub:`11` + M\ :sub:`23` M\ :sub:`21` +
      M\ :sub:`33` M\ :sub:`31` = 0 where j = 3, k = 1

   -  M\ :sub:`13` M\ :sub:`12` + M\ :sub:`23` M\ :sub:`22` +
      M\ :sub:`33` M\ :sub:`32` = 0 where j = 3, k = 2

   -  M\ :sub:`13` M\ :sub:`13` + M\ :sub:`23` M\ :sub:`23` +
      M\ :sub:`33` M\ :sub:`33` = 1 where j = 3, k = 3

   The Frame of Reference Transformation Matrix :sup:`A`\ M\ :sub:`B`
   describes how to transform a point
   (B\ :sub:`x`,B\ :sub:`y`,B\ :sub:`z`) with respect to RCS\ :sub:`B`
   into (A\ :sub:`x`,A\ :sub:`y`,A\ :sub:`z`) with respect to
   RCS\ :sub:`A`.

   The matrix above consists of two parts: a rotation and translation as
   shown below;

   Rotation:

   Translation:

   The first column [M\ :sub:`11`,M\ :sub:`21`,M\ :sub:`31` ] are the
   direction cosines (projection) of the X-axis of RCS\ :sub:`B` with
   respect to RCS\ :sub:`A` *.* The second column
   [M\ :sub:`12`,M\ :sub:`22`,M\ :sub:`32`] are the direction cosines
   (projection) of the Y-axis of RCS\ :sub:`B` with respect to
   RCS\ :sub:`A.` The third column
   [M\ :sub:`13`,M\ :sub:`23`,M\ :sub:`33`] are the direction cosines
   (projection) of the Z-axis of RCS\ :sub:`B` with respect to
   RCS\ :sub:`A.` The fourth column
   [T\ :sub:`1`,T\ :sub:`2`,T\ :sub:`3`] is the origin of RCS\ :sub:`B`
   with respect to RCS\ :sub:`A`.

   There are three degrees of freedom representing rotation, and three
   degrees of freedom representing translation, giving a total of six
   degrees of freedom.

-  RIGID_SCALE

   The following constraint applies:

   for all combinations of j = 1,2,3 and k = 1,2,3 where δ = 1 for i=j
   and zero otherwise.

   The expansion into non-matrix equations is:

   -  M\ :sub:`11` M\ :sub:`11` + M\ :sub:`21` M\ :sub:`21` +
      M\ :sub:`31` M\ :sub:`31` = S\ :sub:`1` :sup:`2` where j = 1, k =
      1

   -  M\ :sub:`11` M\ :sub:`12` + M\ :sub:`21` M\ :sub:`22` +
      M\ :sub:`31` M\ :sub:`32` = 0 where j = 1, k = 2

   -  M\ :sub:`11` M\ :sub:`13` + M\ :sub:`21` M\ :sub:`23` +
      M\ :sub:`31` M\ :sub:`33` = 0 where j = 1, k = 3

   -  M\ :sub:`12` M\ :sub:`11` + M\ :sub:`22` M\ :sub:`21` +
      M\ :sub:`32` M\ :sub:`31` = 0 where j = 2, k = 1

   -  M\ :sub:`12` M\ :sub:`12` + M\ :sub:`22` M\ :sub:`22` +
      M\ :sub:`32` M\ :sub:`32` = S\ :sub:`2` :sup:`2` where j = 2, k =
      2

   -  M\ :sub:`12` M\ :sub:`13` + M\ :sub:`22` M\ :sub:`23` +
      M\ :sub:`32` M\ :sub:`33` = 0 where j = 2, k = 3

   -  M\ :sub:`13` M\ :sub:`11` + M\ :sub:`23` M\ :sub:`21` +
      M\ :sub:`33` M\ :sub:`31` = 0 where j = 3, k = 1

   -  M\ :sub:`13` M\ :sub:`12` + M\ :sub:`23` M\ :sub:`22` +
      M\ :sub:`33` M\ :sub:`32` = 0 where j = 3, k = 2

   -  M\ :sub:`13` M\ :sub:`13` + M\ :sub:`23` M\ :sub:`23` +
      M\ :sub:`33` M\ :sub:`33` = S\ :sub:`3` :sup:`2` where j = 3, k =
      3

   The above equations show a simple way of extracting the spatial
   scaling parameters Sj from a given matrix. The units of S\ :sub:`j`
   :sup:`2` is the RCS unit dimension of one millimeter.

   This type can be considered a simple extension of the type RIGID. The
   RIGID_SCALE is easily created by pre-multiplying a RIGID matrix by a
   diagonal scaling matrix as follows:

   where M\ :sub:`RBWS` is a matrix of type RIGID_SCALE and M\ :sub:`RB`
   is a matrix of type RIGID.

-  AFFINE:

   No constraints apply to this matrix, so it contains twelve degrees of
   freedom. This type of Frame of Reference Transformation Matrix allows
   shearing in addition to rotation, translation and scaling.

For a RIGID type of Frame of Reference Transformation Matrix, the
inverse is easily computed using the following formula (inverse of an
orthonormal matrix):

For RIGID_SCALE and AFFINE types of Registration Matrices, the inverse
cannot be calculated using the above equation, and must be calculated
using a conventional matrix inverse operation.

