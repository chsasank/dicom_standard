.. _chapter_JJJ:

Optical Surface Scan
====================

.. _sect_JJJ.1:

General Information
-------------------

When supporting textures within one acquisition process, multiple series
are generated. There is one Series containing the Surfaces and another
containing the textures. References are used to link Instances in
different series together.

.. _sect_JJJ.2:

One Single Shot Without Texture Acquisition As Point Cloud
----------------------------------------------------------

Use cases: A single surface record of a patient is made, for example
teeth, nose, or breast. If third party software does the post-processing
only the point cloud needs to be stored.

The Surface Scan Point Cloud instance will be used because a point cloud
is stored. A study with a single series is created.

.. _sect_JJJ.3:

One Single Shot With Texture Acquisition As Mesh
------------------------------------------------

Use cases: A scanner device providing triangulated objects with
textures, e.g., for documentation of burns or virtual autopsy.

The Surface Scan Mesh instance will be used because a triangulated
object is stored. A study with two series will be created. One series
contains a Surface Mesh instance and the other series a VL Photographic
Image instance. The latter stores the texture, which is mapped on the
surface mesh and is linked to the Surface Scan Mesh instance via the UV
Mapping Sequence (0080,0008).

.. _sect_JJJ.4:

Storing Modified Point Cloud With Texture As Mesh
-------------------------------------------------

Use cases: The surface of a textured object has been modified, for
example artifacts have been manually removed after the study or surgery.
The new result is stored.

In the study of the origin Surface Scan Point Cloud instance a Surface
Scan Mesh instance is created in its own series containing the modified
mesh. The Referenced Surface Data Sequence (0080,0013) will be used to
reference the original instance. The mesh as well as the point cloud
points to the texture using the Referenced Surface Data Sequence
(0080,0012).

.. _sect_JJJ.5:

Multishot Without Texture As Point Clouds and Merged Mesh
---------------------------------------------------------

Use-case: Objects, which need to be scanned from multiple points of
view, such as the nose.

After the acquired point clouds have been merged by a post-processing
software application, the calculated surface mesh is stored in the same
study in a new series. The Referenced Surface Data Sequence (0080,0013)
points to all origin Surface Scan Point Cloud instances that have been
used for reconstruction. The Registration Method Code Sequence
(0080,0003) is used to indicate that multiple point clouds have been
merged.

.. _sect_JJJ.6:

Multishot With Two Texture Per Point Cloud
------------------------------------------

Use-case: In the application field of dental procedures some products
support switching between two different textures for the same surface.

In this case a number of VL Photographic Image instances are stored in
the same series.

The UV Mapping Sequence (0080,0008) is used to associate the VL
Photographic Image instances with the Surface Scan Point Cloud instance.
The Texture Label (0080,0009) is used to identify the textures of one
point cloud.

.. _sect_JJJ.7:

Using Colored Vertices Instead of Texture
-----------------------------------------

Use-case: A single surface record of a patient is made, for example
teeth, nose, or breast. If third party software does the post-processing
only the point cloud needs to be stored. Gray or color values can be
assigned to each point in the point cloud.

The point cloud is stored in a Surface Scan Point Cloud instance. A
study with a single series is created. One or both of the Attributes
Surface Point Presentation Value Data (0080,0006), or Surface Point
Color CIELab Value Data (0080,0007) may be used to assign gray or color
values to each point in the point cloud.

.. _sect_JJJ.8:

4D Surface Data Analysis
------------------------

Use-case: To replay a sequence of multiple 3D shots of different facial
expressions of a patient before facial surgeries such as facial
transplantation.

A time stamp for each shot is stored in the Acquisition DateTime
Attribute (0008,002A).

.. _sect_JJJ.9:

Referencing A Texture From Another Series
-----------------------------------------

Use-case: A texture from another series must be applied to a point
cloud.

The Referenced Instances And Access Macro is used within the Referenced
Textures Sequence (0080,0012) to reference a VL Photographic Image
instance from a different study.

