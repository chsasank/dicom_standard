.. _chapter_ZZ:

Implant Template Description
============================

.. _sect_ZZ.1:

Implant Mating
--------------

In this section, the usage of mating features for assembly of implants
is declared.

.. _sect_ZZ.1.1:

Mating Features
~~~~~~~~~~~~~~~

These Attributes establish a Cartesian coordinate system relative to the
Frame of Reference of the implant. When two implants are assembled using
a pair of mating features, a rigid spatial registration can be
established, that transforms one Frame of Reference so that the mating
features align. The figure below gives a simple example in 2D how two
implants (symbolized by two rectangles) are matched according to a
mating feature pair. For each 2D and 3D template present, a set of
coordinates is assigned to each Mating Feature Sequence Item.

.. _sect_ZZ.1.2:

Mating Feature ID
~~~~~~~~~~~~~~~~~

It is recommended to give Mating Features that are somehow related, the
same Mating Feature ID (0068,63F0) in different implant templates. This
may help applications to switch between components while keeping
connections to other components. The Example in
`figure_title <#figure_ZZ.1-2>`__ shows that the first and the last hole
in the plates get the same Mating Feature ID in each Template.

.. _sect_ZZ.1.3:

Mating Feature Sets
~~~~~~~~~~~~~~~~~~~

The Mating Features are organized in sets of alternative features: Only
one feature of any set shall be used for assembly with other components
in one plan. This enables the definition of variants for one kind of
contact a component can make while ensuring consistent plans.

An example for Mating Feature Sets is shown in
`figure_title <#figure_ZZ.1-3>`__. A hip stem template shows a set of
five mating features, drawn as circles on the tip of its cone. Different
head components use different mating points, depending on the base
radius of the conic intake on the head.

.. _sect_ZZ.1.4:

Degrees of Freedom
~~~~~~~~~~~~~~~~~~

For each Item of the Mating Feature Sequence (0068,63E0), degrees of
freedom can be specified. A degree of freedom is defined by one axis,
and can be either rotational or translational. For each 2D and 3D
template present, the geometric specifications of the mating points can
be provided.

.. _sect_ZZ.1.5:

Implant Assembly Templates
~~~~~~~~~~~~~~~~~~~~~~~~~~

Instances of the Implant Assembly Template IOD are utilized to define
intended combinations of implant templates. An Implant Assembly Template
consists of a sequence of component type definitions (Component Type
Sequence (0076,0032)) that references Implant Template Instances and
assigns roles to the referenced implants. In the example in
`figure_title <#figure_ZZ.1-4>`__, the component types "Stems" and
"Heads" are defined. Four different stems and two different heads are
referenced. Both groups are flagged mandatory and exclusive, i.e., a
valid assembly requires exactly one representative of each group.

The Component Assembly Sequence (0076,0060) declares possible
connections between components referenced by the component groups. Each
sequence item refers to exactly two implant templates that are part of
at least one component group in the same Implant Assembly Template
Instance. An Component Assembly Sequence Item references one mating
feature in each of the templates according to which the assembly is
geometrically constrained. The double-pointed dashed lines represent the
Items of the Component Assembly Sequence in
`figure_title <#figure_ZZ.1-4>`__.

.. _sect_ZZ.2:

Planning Landmarks
------------------

Registration of implant templates with patient images according to
anatomical landmarks is one of the major features of implantation
planning. For that purpose, geometric features can be attached to
Implant Template Instances. Three kinds of landmarks are defined:
Points, lines, and planes. Each landmark consists of its geometric
definition, which is defined per template, and a description.

When registering an Implant Template to patient data like an Image or a
Surface Segmentation, the planning software should establish a spatial
transformation that matches to planning landmarks to corresponding
geometric features in the patient data.

.. _sect_ZZ.3:

Implant Registration and Mating Example
---------------------------------------

In this section, an example is presented that shows the usage of Implant
Templates together with an Implant Assembly Template to create an
Implantation Plan with patient images. The example is in 2D but can
easily be extended to 3D as well. The example looks at a simplified case
of hip reconstruction planning, using a monoblock stem component and a
monoblock cup component.

Planning consists of 2 steps: Selection and placement of the best
fitting cup from the cups referenced by the Assembly Template based on
the dimension of the patient's hip is the first step. With that done, a
stem is selected that can be mated with the selected cup and has a neck
configuration that leads to an optimal outcome with regard to leg length
and other parameters. Therefore, the available stems are placed so that
the features align. The femoral planning landmarks are used to calculate
the displacement of the femur this configuration would result in. The
workflow is shown in the following set of figures.

In the first step, the planning landmarks marked with the green arrows
in `figure_title <#figure_ZZ.3-2>`__ are aligned with compliant
positions in the patient's x-ray.

In the second step, the femoral length axis is detected from the
patient's x-ray and the stem template is aligned accordingly using the
femoral axis landmark. The proximal and distal fixation boundary planes
are used to determine the insertion depth of the stem along that axis.

In the third step, the image is split into a femoral and a pelvic part
according to the proposed resection plane of the stem template. The
mating features are used to calculate the spatial relation between the
femoral and the pelvic component.

.. _sect_ZZ.3.1:

Degrees of Freedom
~~~~~~~~~~~~~~~~~~

The hip joint has several degrees of freedom, of course. The Implant
Template should contain this information in the Mating Features. In the
given 2D projections, the rotational freedom of the joint is expressed
by one single rotation around the axis of projection intersecting with
the printing space at the 2D coordinate of the Mating Feature.
Therefore, a Degree Of Freedom Sequence Item added to either the stem,
the cup, or both.

In planning, this information could be used to visualize the rotational
capacities of the joint after implantation.

.. note::

   Technically, the degree of freedom could also have been added to the
   cup or even (each with half the range of freedom) to both. But since
   we are used to seeing the femur's rotation with respect to the pelvis
   and not the other way around, it seemed natural to do it that way.

.. _sect_ZZ.4:

Encoding Example
----------------

The Templates used in the example can be encoded as follows:

.. table:: Attributes Used to Describe a Mono Stem Implant for Total Hip
Replacement

   +-------------------------+-------------------------+---------------+
   | **Attribute**           | **Value**               | **Comment**   |
   +=========================+=========================+===============+
   |                         |                         |               |
   +-------------------------+-------------------------+---------------+
   | SOP Class UID           | 1                       |               |
   |                         | .2.840.10008.5.1.4.43.1 |               |
   +-------------------------+-------------------------+---------------+
   | SOP Instance UID        | 1.2.3.4.5.6.7.0.1       |               |
   +-------------------------+-------------------------+---------------+
   | **Generic Implant       |                         |               |
   | Template Module**       |                         |               |
   +-------------------------+-------------------------+---------------+
   | Manufacturer            | ACME                    |               |
   +-------------------------+-------------------------+---------------+
   | Implant Name            | MONO_STEM               |               |
   +-------------------------+-------------------------+---------------+
   | Implant Size            | MEDIUM                  |               |
   +-------------------------+-------------------------+---------------+
   | Implant Part Number     | ACME_MST_M              |               |
   +-------------------------+-------------------------+---------------+
   | Effective DateTime      | 26.06.2009 12:00        |               |
   +-------------------------+-------------------------+---------------+
   | Implant Template        | 1                       |               |
   | Version                 |                         |               |
   +-------------------------+-------------------------+---------------+
   | Implant Template Type   | ORIGINAL                |               |
   +-------------------------+-------------------------+---------------+
   | Implant Target Anatomy  |                         |               |
   | Sequence                |                         |               |
   +-------------------------+-------------------------+---------------+
   | >Anatomic Region        |                         |               |
   | Sequence                |                         |               |
   +-------------------------+-------------------------+---------------+
   | >>Code Value            | 71341001                |               |
   +-------------------------+-------------------------+---------------+
   | >>Coding Scheme         | SCT                     |               |
   | Designator              |                         |               |
   +-------------------------+-------------------------+---------------+
   | >>Code Meaning          | Femur                   |               |
   +-------------------------+-------------------------+---------------+
   | Frame of Reference UID  | 1.2.3.4.5.6.7.1.1       |               |
   +-------------------------+-------------------------+---------------+
   | Overall Template        | 1.0                     |               |
   | Spatial Tolerance       |                         |               |
   +-------------------------+-------------------------+---------------+
   | HPGL Document Sequence  |                         |               |
   +-------------------------+-------------------------+---------------+
   | >HPGL Document ID       | 1                       |               |
   +-------------------------+-------------------------+---------------+
   | >View Orientation Code  |                         |               |
   | Sequence                |                         |               |
   +-------------------------+-------------------------+---------------+
   | >>Code Value            | 399348003               |               |
   +-------------------------+-------------------------+---------------+
   | >>Coding Scheme         | SCT                     |               |
   | Designator              |                         |               |
   +-------------------------+-------------------------+---------------+
   | >>Code Meaning          | Antero-Posterior        |               |
   +-------------------------+-------------------------+---------------+
   | >HPGL Document Scaling  | 1.0                     |               |
   +-------------------------+-------------------------+---------------+
   | >HPGL Document          | IN PA …                 | HPGL commands |
   +-------------------------+-------------------------+---------------+
   | >HPGL Contour Pen       | 2                       |               |
   | Number                  |                         |               |
   +-------------------------+-------------------------+---------------+
   | >HPGL Pen Sequence      |                         |               |
   +-------------------------+-------------------------+---------------+
   | >>HPGL Pen Number       | 2                       |               |
   +-------------------------+-------------------------+---------------+
   | >>HPGL Pen Label        | Contour                 |               |
   +-------------------------+-------------------------+---------------+
   | >>HPGL Pen Number       | 3                       |               |
   +-------------------------+-------------------------+---------------+
   | >>HPGL Pen Label        | Landmarks               |               |
   +-------------------------+-------------------------+---------------+
   | >>HPGL Pen Number       | 4                       |               |
   +-------------------------+-------------------------+---------------+
   | >>HPGL Pen Label        | Mating Features         |               |
   +-------------------------+-------------------------+---------------+
   | >Recommended Rotation   | 39.6/72.4               |               |
   | Point                   |                         |               |
   +-------------------------+-------------------------+---------------+
   | >Bounding Rectangle     | 14.2/5.7/46/78.8        |               |
   +-------------------------+-------------------------+---------------+
   | Material Code Sequence  |                         |               |
   +-------------------------+-------------------------+---------------+
   | >Code Value             | 256506002               |               |
   +-------------------------+-------------------------+---------------+
   | >Coding Scheme          | SCT                     |               |
   | Designator              |                         |               |
   +-------------------------+-------------------------+---------------+
   | >Code Meaning           | Stainless Steel         |               |
   |                         | Material                |               |
   +-------------------------+-------------------------+---------------+
   | Implant Type Code       |                         |               |
   | Sequence                |                         |               |
   +-------------------------+-------------------------+---------------+
   | >Code Value             | 112315                  |               |
   +-------------------------+-------------------------+---------------+
   | >Coding Scheme          | DCM                     |               |
   | Designator              |                         |               |
   +-------------------------+-------------------------+---------------+
   | >Code Meaning           | Monoblock Stem          |               |
   +-------------------------+-------------------------+---------------+
   | Fixation Method Code    |                         |               |
   | Sequence                |                         |               |
   +-------------------------+-------------------------+---------------+
   | >Code Value             | 304367000               |               |
   +-------------------------+-------------------------+---------------+
   | >Coding Scheme          | SCT                     |               |
   | Designator              |                         |               |
   +-------------------------+-------------------------+---------------+
   | >Code Meaning           | Uncemented Component    |               |
   |                         | Fixation                |               |
   +-------------------------+-------------------------+---------------+
   | Mating Feature Sets     |                         |               |
   | Sequence                |                         |               |
   +-------------------------+-------------------------+---------------+
   | >Mating Feature Set ID  | 1                       |               |
   +-------------------------+-------------------------+---------------+
   | >Mating Feature Set     | Head Rotation Point     |               |
   | Label                   |                         |               |
   +-------------------------+-------------------------+---------------+
   | >Mating Feature         |                         |               |
   | Sequence                |                         |               |
   +-------------------------+-------------------------+---------------+
   | >>Mating Feature ID     | 1                       |               |
   +-------------------------+-------------------------+---------------+
   | >>2D Mating Feature     |                         |               |
   | Coordinates Sequence    |                         |               |
   +-------------------------+-------------------------+---------------+
   | >>>Referenced HPGL      | 1                       |               |
   | Document ID             |                         |               |
   +-------------------------+-------------------------+---------------+
   | >>>2D Mating Point      | 39.6/72.4               |               |
   +-------------------------+-------------------------+---------------+
   | >>>2D Mating Axes       | 1/0/0/1                 |               |
   +-------------------------+-------------------------+---------------+
   | >>Mating Feature Degree |                         |               |
   | of Freedom Sequence     |                         |               |
   +-------------------------+-------------------------+---------------+
   | >>>Degree of Freedom ID | 1                       |               |
   +-------------------------+-------------------------+---------------+
   | >>>Degree of Freedom    | ROTATION                |               |
   | Type                    |                         |               |
   +-------------------------+-------------------------+---------------+
   | >>>2D Degree of Freedom |                         |               |
   | Sequence                |                         |               |
   +-------------------------+-------------------------+---------------+
   | >>>>Referenced HPGL     | 1                       |               |
   | Document ID             |                         |               |
   +-------------------------+-------------------------+---------------+
   | >>>>2D Degree Of        | 0/0/1                   |               |
   | Freedom Axis            |                         |               |
   +-------------------------+-------------------------+---------------+
   | >>>>Range of Freedom    | -15/15                  |               |
   +-------------------------+-------------------------+---------------+

.. table:: Attributes Used to Describe a Mono Cup Implant for Total Hip
Replacement

   +-------------------------+-------------------------+---------------+
   | **Attribute**           | **Value**               | **Comment**   |
   +=========================+=========================+===============+
   |                         |                         |               |
   +-------------------------+-------------------------+---------------+
   | SOP Class UID           | 1                       |               |
   |                         | .2.840.10008.5.1.4.43.1 |               |
   +-------------------------+-------------------------+---------------+
   | SOP Instance UID        | 1.2.3.4.5.6.7.0.2       |               |
   +-------------------------+-------------------------+---------------+
   | **Generic Implant       |                         |               |
   | Template Module**       |                         |               |
   +-------------------------+-------------------------+---------------+
   | Manufacturer            | ACME                    |               |
   +-------------------------+-------------------------+---------------+
   | Implant Name            | MONO_CUP                |               |
   +-------------------------+-------------------------+---------------+
   | Implant Size            | MEDIUM                  |               |
   +-------------------------+-------------------------+---------------+
   | Implant Part Number     | ACME_MCP_M              |               |
   +-------------------------+-------------------------+---------------+
   | Effective DateTime      | 26.06.2009 12:00        |               |
   +-------------------------+-------------------------+---------------+
   | Implant Template        | 1                       |               |
   | Version                 |                         |               |
   +-------------------------+-------------------------+---------------+
   | Implant Template Type   | ORIGINAL                |               |
   +-------------------------+-------------------------+---------------+
   | Implant Target Anatomy  |                         |               |
   | Sequence                |                         |               |
   +-------------------------+-------------------------+---------------+
   | >Anatomic Region        |                         |               |
   | Sequence                |                         |               |
   +-------------------------+-------------------------+---------------+
   | >>Code Value            | 24136001                |               |
   +-------------------------+-------------------------+---------------+
   | >>Coding Scheme         | SCT                     |               |
   | Designator              |                         |               |
   +-------------------------+-------------------------+---------------+
   | >>Code Meaning          | Hip Joint               |               |
   +-------------------------+-------------------------+---------------+
   | Frame of Reference UID  | 1.2.3.4.5.6.7.1.2       |               |
   +-------------------------+-------------------------+---------------+
   | Overall Template        | 1.0                     |               |
   | Spatial Tolerance       |                         |               |
   +-------------------------+-------------------------+---------------+
   | HPGL Document Sequence  |                         |               |
   +-------------------------+-------------------------+---------------+
   | >HPGL Document ID       | 1                       |               |
   +-------------------------+-------------------------+---------------+
   | >View Orientation Code  |                         |               |
   | Sequence                |                         |               |
   +-------------------------+-------------------------+---------------+
   | >>Code Value            | 399321004               |               |
   +-------------------------+-------------------------+---------------+
   | >>Coding Scheme         | SCT                     |               |
   | Designator              |                         |               |
   +-------------------------+-------------------------+---------------+
   | >>Code Meaning          | Anterior Projection     |               |
   +-------------------------+-------------------------+---------------+
   | >HPGL Document Scaling  | 1                       |               |
   +-------------------------+-------------------------+---------------+
   | >HPGL Document          | IN PA …                 | HPGL commands |
   +-------------------------+-------------------------+---------------+
   | >HPGL Contour Pen       | 2                       |               |
   | Number                  |                         |               |
   +-------------------------+-------------------------+---------------+
   | >HPGL Pen Sequence      |                         |               |
   +-------------------------+-------------------------+---------------+
   | >>HPGL Pen Number       | 2                       |               |
   +-------------------------+-------------------------+---------------+
   | >>HPGL Pen Label        | Contour                 |               |
   +-------------------------+-------------------------+---------------+
   | >>HPGL Pen Number       | 3                       |               |
   +-------------------------+-------------------------+---------------+
   | >>HPGL Pen Label        | Landmarks               |               |
   +-------------------------+-------------------------+---------------+
   | >>HPGL Pen Number       | 4                       |               |
   +-------------------------+-------------------------+---------------+
   | >>HPGL Pen Label        | Mating Features         |               |
   +-------------------------+-------------------------+---------------+
   | >Recommended Rotation   | 12.9/0                  |               |
   | Point                   |                         |               |
   +-------------------------+-------------------------+---------------+
   | >Bounding Rectangle     | 0/0/25.8/12.9           |               |
   +-------------------------+-------------------------+---------------+
   | Material Code Sequence  |                         |               |
   +-------------------------+-------------------------+---------------+
   | >Code Value             | 256506002               |               |
   +-------------------------+-------------------------+---------------+
   | >Coding Scheme          | SCT                     |               |
   | Designator              |                         |               |
   +-------------------------+-------------------------+---------------+
   | >Code Meaning           | Stainless Steel         |               |
   |                         | Material                |               |
   +-------------------------+-------------------------+---------------+
   | Implant Type Code       |                         |               |
   | Sequence                |                         |               |
   +-------------------------+-------------------------+---------------+
   | >Code Value             | 112307                  |               |
   +-------------------------+-------------------------+---------------+
   | >Coding Scheme          | DCM                     |               |
   | Designator              |                         |               |
   +-------------------------+-------------------------+---------------+
   | >Code Meaning           | Acetabular Cup          |               |
   |                         | Monoblock               |               |
   +-------------------------+-------------------------+---------------+
   | Fixation Method Code    |                         |               |
   | Sequence                |                         |               |
   +-------------------------+-------------------------+---------------+
   | >Code Value             | 304367000               |               |
   +-------------------------+-------------------------+---------------+
   | >Coding Scheme          | SCT                     |               |
   | Designator              |                         |               |
   +-------------------------+-------------------------+---------------+
   | >Code Meaning           | Uncemented Component    |               |
   |                         | Fixation                |               |
   +-------------------------+-------------------------+---------------+
   | Mating Feature Sets     |                         |               |
   | Sequence                |                         |               |
   +-------------------------+-------------------------+---------------+
   | >Mating Feature Set ID  | 1                       |               |
   +-------------------------+-------------------------+---------------+
   | >Mating Feature Set     | Hip Joint Mating        |               |
   | Label                   | Feature                 |               |
   +-------------------------+-------------------------+---------------+
   | >Mating Feature         |                         |               |
   | Sequence                |                         |               |
   +-------------------------+-------------------------+---------------+
   | >>Mating Feature ID     | 1                       |               |
   +-------------------------+-------------------------+---------------+
   | >>2D Mating Feature     |                         |               |
   | Coordinates Sequence    |                         |               |
   +-------------------------+-------------------------+---------------+
   | >>>Referenced HPGL      | 1                       |               |
   | Document ID             |                         |               |
   +-------------------------+-------------------------+---------------+
   | >>>2D Mating Point      | 12.9/0                  |               |
   +-------------------------+-------------------------+---------------+
   | >>>2D Mating Axes       | 0                       |               |
   |                         | .707/0.707/-0.707/0.707 |               |
   +-------------------------+-------------------------+---------------+

.. table:: Attributes Used to Describe The Assembly of Cup and Stem

   +------------------------+------------------------+-----------------+
   | **Attribute**          | **Value**              | **Comment**     |
   +========================+========================+=================+
   |                        |                        |                 |
   +------------------------+------------------------+-----------------+
   | SOP Class UID          | 1.                     |                 |
   |                        | 2.840.10008.5.1.4.44.1 |                 |
   +------------------------+------------------------+-----------------+
   | SOP Instance UID       | 1.2.3.4.5.6.7.0.3      |                 |
   +------------------------+------------------------+-----------------+
   | **Implant Assembly     |                        |                 |
   | Template Module**      |                        |                 |
   +------------------------+------------------------+-----------------+
   | Implant Assembly       | Acme Hip Assembly      |                 |
   | Template Name          |                        |                 |
   +------------------------+------------------------+-----------------+
   | Implant Assembly       | ACME                   |                 |
   | Template Issuer        |                        |                 |
   +------------------------+------------------------+-----------------+
   | Effective DateTime     | 26.06.2009 12:00       |                 |
   +------------------------+------------------------+-----------------+
   | Implant Assembly       | 1                      |                 |
   | Template Version       |                        |                 |
   +------------------------+------------------------+-----------------+
   | Implant Assembly       | ORIGINAL               |                 |
   | Template Type          |                        |                 |
   +------------------------+------------------------+-----------------+
   | Implant Assembly       |                        |                 |
   | Template Target        |                        |                 |
   | Anatomy Sequence       |                        |                 |
   +------------------------+------------------------+-----------------+
   | >Anatomic Region       |                        |                 |
   | Sequence               |                        |                 |
   +------------------------+------------------------+-----------------+
   | >>Code Value           | 24136001               |                 |
   +------------------------+------------------------+-----------------+
   | >>Coding Scheme        | SCT                    |                 |
   | Designator             |                        |                 |
   +------------------------+------------------------+-----------------+
   | >>Code Meaning         | Hip Joint              |                 |
   +------------------------+------------------------+-----------------+
   | Procedure Type Code    |                        |                 |
   | Sequence               |                        |                 |
   +------------------------+------------------------+-----------------+
   | >Code Value            | 119614000              |                 |
   +------------------------+------------------------+-----------------+
   | >Coding Scheme         | SCT                    |                 |
   | Designator             |                        |                 |
   +------------------------+------------------------+-----------------+
   | >Code Meaning          | Hip Joint              |                 |
   |                        | Reconstruction         |                 |
   +------------------------+------------------------+-----------------+
   | Component Types        |                        |                 |
   | Sequence               |                        |                 |
   +------------------------+------------------------+-----------------+
   | >Component Type Code   |                        | Sequence Item 1 |
   | Sequence               |                        |                 |
   +------------------------+------------------------+-----------------+
   | >>Code Value           | 112310                 |                 |
   +------------------------+------------------------+-----------------+
   | >>Coding Scheme        | DCM                    |                 |
   | Designator             |                        |                 |
   +------------------------+------------------------+-----------------+
   | >>Code Meaning         | Femoral Stem           |                 |
   +------------------------+------------------------+-----------------+
   | >Exclusive Component   | YES                    |                 |
   | Type                   |                        |                 |
   +------------------------+------------------------+-----------------+
   | >Mandatory Component   | YES                    |                 |
   | Type                   |                        |                 |
   +------------------------+------------------------+-----------------+
   | >Component Sequence    |                        |                 |
   +------------------------+------------------------+-----------------+
   | >>Referenced SOP Class | 1.                     |                 |
   | UID                    | 2.840.10008.5.1.4.43.1 |                 |
   +------------------------+------------------------+-----------------+
   | >>Referenced SOP       | 1.2.3.4.5.6.7.0.1      |                 |
   | Instance UID           |                        |                 |
   +------------------------+------------------------+-----------------+
   | >>Component ID         | 1                      |                 |
   +------------------------+------------------------+-----------------+
   | >Component Type Code   |                        | Sequence Item 2 |
   | Sequence               |                        |                 |
   +------------------------+------------------------+-----------------+
   | >>Code Value           | 112305                 |                 |
   +------------------------+------------------------+-----------------+
   | >>Coding Scheme        | DCM                    |                 |
   | Designator             |                        |                 |
   +------------------------+------------------------+-----------------+
   | >>Code Meaning         | Acetabular Cup Shell   |                 |
   +------------------------+------------------------+-----------------+
   | >Exclusive Component   | YES                    |                 |
   | Type                   |                        |                 |
   +------------------------+------------------------+-----------------+
   | >Mandatory Component   | YES                    |                 |
   | Type                   |                        |                 |
   +------------------------+------------------------+-----------------+
   | >Component Sequence    |                        |                 |
   +------------------------+------------------------+-----------------+
   | >>Referenced SOP Class | 1.                     |                 |
   | UID                    | 2.840.10008.5.1.4.43.1 |                 |
   +------------------------+------------------------+-----------------+
   | >>Referenced SOP       | 1.2.3.4.5.6.7.0.2      |                 |
   | Instance UID           |                        |                 |
   +------------------------+------------------------+-----------------+
   | >>Component ID         | 2                      |                 |
   +------------------------+------------------------+-----------------+
   | Component Assembly     |                        |                 |
   | Sequence               |                        |                 |
   +------------------------+------------------------+-----------------+
   | >Component 1           | 1                      | The stem        |
   | Referenced ID          |                        |                 |
   +------------------------+------------------------+-----------------+
   | >Component 1           | 1                      |                 |
   | Referenced Mating      |                        |                 |
   | Feature Set ID         |                        |                 |
   +------------------------+------------------------+-----------------+
   | > Component 1          | 1                      |                 |
   | Referenced Mating      |                        |                 |
   | Feature ID             |                        |                 |
   +------------------------+------------------------+-----------------+
   | >Component 2           | 2                      | The cup         |
   | Referenced ID          |                        |                 |
   +------------------------+------------------------+-----------------+
   | > Component 2          | 1                      |                 |
   | Referenced Mating      |                        |                 |
   | Feature Set ID         |                        |                 |
   +------------------------+------------------------+-----------------+
   | > Component 2          | 1                      |                 |
   | Referenced Mating      |                        |                 |
   | Feature ID             |                        |                 |
   +------------------------+------------------------+-----------------+

.. _sect_ZZ.5:

Implant Template Versions and Derivation
----------------------------------------

The Generic Implant Module contains several Attributes to express the
relations between different versions of implant templates. These
Attributes are

+-------------+--------------------------+--------------------------+
| (0022,1097) | Implant Part Number      | Number (or               |
|             |                          | alphanumerical code)     |
|             |                          | assigned by the          |
|             |                          | manufacturer of an       |
|             |                          | implant to one           |
|             |                          | particular release of    |
|             |                          | one particular part.     |
|             |                          | Whenever changes on the  |
|             |                          | implant design are made, |
|             |                          | a new implant part       |
|             |                          | number is assigned.      |
+-------------+--------------------------+--------------------------+
| (0068,6226) | Effective DateTime       | Date and time from which |
|             |                          | on an Implant Template   |
|             |                          | Instance is valid.       |
+-------------+--------------------------+--------------------------+
| (0068,6221) | Implant Template Version | Number assigned by the   |
|             |                          | creator of an ORIGINAL   |
|             |                          | Implant Template         |
|             |                          | Instance. When an        |
|             |                          | implant manufacturer     |
|             |                          | issues a new version of  |
|             |                          | an implant template      |
|             |                          | without doing changes on |
|             |                          | the implant itself, it   |
|             |                          | issues a new instance    |
|             |                          | with the same part       |
|             |                          | number but a different   |
|             |                          | template version.        |
+-------------+--------------------------+--------------------------+
| (0068,6222) | Replaced Implant         | When a manufacturer      |
|             | Template Sequence        | issues a new version of  |
|             |                          | an Implant Template, the |
|             |                          | instance contains a      |
|             |                          | reference to it direct   |
|             |                          | predecessor.             |
+-------------+--------------------------+--------------------------+
| (0068,6223) | Implant Type             | When a software vendor,  |
|             |                          | user or other entity     |
|             |                          | creates a "proprietary"  |
|             |                          | version of an Implant    |
|             |                          | Template by adding       |
|             |                          | Attributes, the          |
|             |                          | resulting Instance is    |
|             |                          | labeled DERIVED.         |
+-------------+--------------------------+--------------------------+
| (0068,6225) | Original Implant         | When an Instance is      |
|             | Template                 | DERIVED, it contains a   |
|             |                          | reference to the         |
|             |                          | ORIGINAL instance it was |
|             |                          | derived from (directly   |
|             |                          | or with several derived  |
|             |                          | versions in between).    |
+-------------+--------------------------+--------------------------+
| (0068,6224) | Derivation Implant       | When an Implant Template |
|             | Template Sequence        | Instance is derived from |
|             |                          | another instance, it     |
|             |                          | contains a reference to  |
|             |                          | the Implant Template     |
|             |                          | Instance it was directly |
|             |                          | derived from.            |
+-------------+--------------------------+--------------------------+

Different versions of Implant Templates reflect the changes a
manufacturer is doing on the Implant Templates he issues. The Implant
Templates that are issued by a manufacturer (or a third party who is
acting on behalf of the manufacturer) are always ORIGINAL. Software
vendors, PACS integrators, or other stakeholders will add information to
such templates for different purposes. The Instances that are generated
by this process is called derivation and the resulting instances are
labeled DERIVED. Implantation Plans, i.e., electronic documents
describing the result of implantation planning, are specified in an
instance of the Implantation Plan SR Document. There, the implants that
are relevant for one plan are included by reference. When such plans are
exchanged between systems or organizations it is likely that the
receiving party has access to other versions of templates as the sending
party has. In order to maintain readability of exchanged plans, the
following is required:

-  All necessary information about an implant that is relevant to
   display and understand a plan is present in the ORIGINAL Implant
   Templates that were issued by a manufacturer. This is assured by
   these Attributes being Type 1 in the IOD.

-  When deriving Instances, information may only be added but not
   removed from the ORIGINAL Instance. This information may be encoded
   in standard or private Tags.

-  Derived Instances contain the information about the source Instances
   they were derived from. All Instances contain a reference to the
   ORIGINAL Instance they were derived from. If an application receives
   a plan that references an implant it does not have in its database,
   it will find the UID of the ORIGINAL Instance in the plan, too. It
   can query its database for an instance that was derived from that
   Instance and thereby find an Instance it can use to present the plan.

`figure_title <#figure_ZZ.5-1>`__ shows an example of the relationships
between two versions of a manufacturer's Implant Template and several
different Implant Templates derived by software vendors from these
versions.

