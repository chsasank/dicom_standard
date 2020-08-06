.. _chapter_KKK:

Use-cases For Conversion of Classic Single Frame Images to Legacy Converted Enhanced Multi-frame Images (Informative)
=====================================================================================================================

.. _sect_KKK.1:

Introduction
------------

Traditionally, images from cross-sectional modalities like CT, MR and
PET have been stored with one reconstructed slice in a single frame
instance. Large studies with a large number of slices potentially pose a
problem for many existing implementations, both for efficient transfer
from the central store to the user's desktop for viewing or analysis,
and for bulk transfer between two stores (e.g., between a PACS and
another archive or a regional image repository).

There are two primary issues:

-  Transporting large numbers of slices as separate single instances
   (files) is potentially extremely inefficient due to the overhead
   associated with each transfer (such as C-STORE acknowledgment and
   database insertion).

-  Replicating the Attributes describing the entire
   patient/study/series/acquisition in every separate single instance is
   also potentially extremely inefficient, and though the size of the
   this information is trivial by comparison with the bulk data, the
   effort to repeatedly parse it and sort out what it means as a whole
   on the receiving end is not trivial.

The Enhanced family of modality-specific multi-frame IODs is intended to
address both these concerns, but there is a large installed base of
older equipment that does not yet support these, both on the sending and
receiving end, and a large archive of single frame instances.

An interim step, a legacy transition strategy for a mixed environment
containing older and newer modalities, PACS and workstations, is
described here. It is predicated on the ability to "convert" single
frame instances into new "enhanced multi-frame instances".

.. _sect_KKK.2:

Enhanced Legacy Converted Image Storage IODs
--------------------------------------------

The Enhanced family of modality-specific multi-frame IODs contain many
requirements that cannot be satisfied by the limited information
typically available in the older single frame objects. A family of
Multi-frame Secondary Capture IODs is available, but their use would
mean that a recipient could not depend on the presence of important
cross-sectional information like spacing, position and orientation.
Accordingly, a new family of modality-specific Legacy Converted Enhanced
Image Storage IODs has been defined that bridge the gap in conversion
complexity and usability between these two extremes.

.. _sect_KKK.3:

Heterogeneous Environment
-------------------------

`figure_title <#figure_KKK-1>`__ illustrates the approach to enabling a
heterogeneous environment with conversion from single to multi-frame
objects as appropriate. In this figure, modalities that generate single
or enhanced images peacefully co-exist with PACS or workstations that
support either or both.

The following use-cases are explicitly supported:

-  A PACS that accepts single frame images, and converts them to
   Multi-frame Images for its own internal use.

-  A PACS that accepts single frame images, and converts them to
   Multi-frame Images for externalization via DICOM services
   (Query/Retrieval) so that they can be used by external workstations
   (or other processing applications) that support Multi-frame Images.

-  A PACS that accepts Multi-frame Images from a modality, and converts
   them to single frame images for its own internal use.

-  A PACS that accepts true and/or legacy converted enhanced Multi-frame
   Images, and converts them to single frame images for externalization
   via DICOM services (Query/Retrieval) so that they can be used by
   external workstations (or other processing applications) that do not
   support Multi-frame Images.

-  A modality that can create true enhanced Multi-frame Images, as well
   as receive true (+/- legacy converted) enhanced Multi-frame Images.

-  Return of results from workstations in either single frame or true or
   legacy converted enhanced multi-frame form.

The amount of standard information is the same in single frame and
transitional legacy-converted Multi-frame Images, but greater in the
true enhanced Multi-frame Images, and this affects the level of
functionality obtainable within the PACS or with an external workstation
(without depending on private information).

Since the transitional legacy-converted and true enhanced Multi-frame
Images share a common structure and common functional group macros, this
scalability can be implemented incrementally.

It is NOT the expectation that modalities will generate Legacy Converted
Enhanced Image Storage SOP Instances; rather, they should create True
Enhanced Image Storage SOP Instances fully populated with the
appropriate Standard Attributes and codes.

.. _sect_KKK.4:

Compatibility With Modality Association Negotiation
---------------------------------------------------

This strategy is compatible with an approach commonly implemented on
acquisition modalities when deciding which SOP Class to use to encode
images.

Normally a modality will propose in the Association that images be
transferred using the SOP Class for which the IOD provides the richest
set of information (i.e., the True Enhanced Image Storage SOP Class),
and will choose the corresponding Abstract Syntax for C-STORE Operations
if the Association Acceptor accepts multiple choices of SOP Class.

Consider a modality that supports the appropriate modality-specific
Enhanced Image Storage SOP Class, but which is faced with the dilemma of
a PACS that does not. In this case, it will commonly "fall back" to
sending images the "old" way as single-frame SOP Class Instances, either
because it has been pre-configured that way by service personnel, or
because it discovers this limitation during Association Negotiation.
This strategy is also common amongst modalities for which there are
different choices of single frame SOP Class (e.g., DX versus CR versus
Secondary Capture, for Digital X-Rays). In some cases, this may be
implemented formally using the ability during Association Negotiation to
specify a Related General SOP Class ().

If the PACS is upgraded to include multi-frame conversion capability,
and no change is made in the configuration of the modality, or in the
SOP Classes accepted by the PACS, then in this scenario, the PACS can
potentially convert the single-frame instances into Legacy Converted
Enhanced instances. The net result is continuing sacrifice of
information compared to what the modality is actually capable of.

A better choice, since the PACS is now capable of handling Multi-frame
Images, is to also reconfigure it to also accept the "true" Enhanced
Image rather than just "transitional" Legacy Converted Enhanced Storage
SOP Classes. Since the two SOP Class families use the same structure and
common important Functional Groups, in all likelihood the PACS will be
able to use either class of objects, and in a future upgrade take
advantage of the additional information in the superior object (perhaps
for more complex processing or annotation or rendering). In any case,
storing the modality's best output in the archive will benefit future
re-use as priors and may enable greater functionality in external
workstations.

A special consideration is when prior images need to be displayed on the
modality before starting a new study (perhaps to setup a comparable
protocol or better understand the request). In this case, care needs to
be taken with respect to which images are accessible to the modality
(either pushed to it or retrieved by it), and the question of "round
trip fidelity" of conversion arises.

.. _sect_KKK.5:

Query and Retrieval
-------------------

The coexistence (either actually or logically) of two different
representations of the same information creates a potential challenge in
that the user must not be presented with both sets simultaneously.

A *naïve* conversion that added converted images to the study without an
ability to distinguish or "filter" them from view would not only be
confusing but would potentially result in twice as much data to
transfer.

Accordingly, the Query/Retrieve mechanism is extended with an optional
extended negotiation capability to specify which "view" of the
information is required by the SCU:

-  A "classic" view, which includes either original (as received)
   classic single frame images or enhanced Multi-frame Images converted
   to single frame.

-  An "enhanced" view, which includes either original (as received)
   enhanced Multi-frame Images, or classic single frame images converted
   to true or legacy converted enhanced multi-frame.

.. _sect_KKK.6:

Referential Integrity
---------------------

Often instances within a Study will cross-reference each other. For
example, a Presentation State or a Structured Report or an RT Structure
Set will reference the images to which they apply, cross-sectional
images may reference localizer images, and images that were acquired
with annotations may contain references to Presentation States encoding
those annotations.

Accordingly, when there are multiple "views" of the same study content
(classic or enhanced), the instances will have different SOP Instance
and Series Instance UIDs for converted content in each view. Hence any
references within an instance to a converted instance needs to be
updated as well. In doing such an update of references to UIDs,
instances that might not otherwise have needed to be converted do need
to be converted, and so on, until the entire set of instances within the
scope of the conversion for the view has referential integrity.

In practice, the only instances that do not need to be converted (and
assigned new UIDs) are those that contain no references and are not
classic or enhanced images to be converted.

Whether or not assignment of a converted instance to a new Series
triggers the need to convert all instances in that Series to the new
Series, even if they would not otherwise be converted, is not defined
(i.e., it is neither required nor prohibited, and hence a Series can be
"split" as a consequence of conversion).

The scope of referential integrity required is defined to be the
Patient. Instances in one Study may be referenced from another (e.g., as
prior images).

.. _sect_KKK.7:

Persistence and Determinism
---------------------------

The rules for conversion specify that the SOP Instance and Series
Instance UIDs of converted images be changed, and that the same UIDs be
used each time that a query or retrieval is performed. The strict
separation of the two "views" of the same information, coupled with the
"determinism" that results in the same identification and organization
of each view every time, are required for stability across successive
operations.

Were this not to be the case, for example, the results of a query
(C-FIND) might be different from the results of a subsequent retrieval
(C-MOVE or C-GET), or for that matter, successive queries. Further,
references to specific instance UID in either view may be recorded in
external systems (e.g., in an EMR), hence it is important that these
remain stable and accessible.

This places a burden on the Q/R SCP to either retain a record of the
mapping of UIDs from one view to the other, or to use some deterministic
process that results in the same UIDs (one could envisage some hashing
scheme, for instance). How this is implemented is beyond the scope of
the Standard to define. The determinism requirement does not remove the
uniqueness requirement; in particular it is not appropriate to attempt
to derive new UIDs by adding a suffix to a UID generated by a different
application, for example.

There is no time limit placed on the determinism; it is expected to be
indefinite, at least within the control of the system. This is a factor
that should be taken into account both in the design of federated Q/R
SCPs that may integrate subsidiary SCPs that support this mechanism. It
should also be considered during migration to a new Q/R SCP, which
ideally should support the mechanism, and should support the same
mapping from one view to another as was provided by the Q/R SCP being
migrated. This may be non-trivial, since the algorithm for conversion
may be different between the two systems. It may be necessary to define
some persistent, standard, serialized mapping of one set of UIDs to the
other.

.. _sect_KKK.8:

Source References
-----------------

It is also useful to save references in converted SOP instances to their
source. Accordingly, converted instances are required to contain such
references, both for image conversions as well as for ancillary
instances that may be updated, such as Presentation States and
Structured Reports.

Obviously, the references to the source instances for the conversion are
excluded from conversion themselves. If the instances have been
converted on different systems, however, there is a possibility that the
source references will be "replaced" and a record of the "chain" of
multiple conversions will not be persisted.

There is no mechanism to define forward references in the source to the
converted instances, since that would imply changing the source
instances from their original form, and while this is acceptable within
the scope of the normal "coercion" that a Storage SCP is permitted to
perform, it is probably not sufficiently useful to justify the effort.
This does imply some asymmetry however, depending on the direction of
conversion (classic to enhanced or vice versa); only one set will
contain the references.

In performing round trip conversion, without access to the source
instances, the referenced source UIDs can be used as the UIDs for the
newly created converted instances.

.. _sect_KKK.9:

Uncertainty Principle
---------------------

When does a converted view come into existence? By definition, when it
is "observed". However, a practical question is when to start
conversion. A Study is never, theoretically, complete, yet the semantics
for conversion and consistency are defined at the Study level.

Another practical question is whether or not to make the received
instances available, even though the converted ones may not yet have
been created.

In the absence of the concept of "study completion" in DICOM, no firm
rules can be defined. However, in practice, most systems have an
internal "completion" concept, which may or may not be related to the
completion of the Performed Procedure Steps that are related to the sets
of instances in question, or may be established through some other
mechanism, such as operator intervention, possibly via a RIS message
(e.g., after QC checks are signed off as complete, or after a Study has
been declared as "ready to read").

A system may elect to "dynamically" begin conversion as instances arrive
and update the information in the conversion as new instances are
encountered, or it may wait until some state is established that allows
it to perform the conversion "statically". In either case, the
information in the converted view via the query/retrieval mechanisms
should be immutable once made available. I.e., once a conversion has
been "distributed", it would be desirable for the system to block
subsequent changes to the Study, except to the extent that there is a
need for correction and management of errors (in which case mechanisms
such as IHE Image Object Change Management (IOCM) may be appropriate).

