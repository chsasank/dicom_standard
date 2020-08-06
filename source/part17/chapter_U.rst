.. _chapter_U:

Ophthalmology Use Cases (Informative)
=====================================

.. _sect_U.1:

Ophthalmic Photography Use Cases
--------------------------------

The following use cases are examples of how the DICOM Ophthalmology
Photography objects may be used. These use cases utilize the term
"picture" or "pictures" to avoid using the DICOM terminology of frame,
instance or image. In the use cases, the series means DICOM Series.

.. _sect_U.1.1:

Routine N-spot Exam
~~~~~~~~~~~~~~~~~~~

An N-spot retinal photography exam means that "N" predefined locations
on the retina are examined.

A routine N-spot retinal photography exam is ordered for both eyes.
There is nothing unusual observed during the exam, so N pictures are
taken of each retina. This healthcare facility also specifies that in an
N-spot exam a routine external picture is captured of both eyes, that
the current intraocular pressure (IOP) is measured, and that the current
refractive state is measured.

The resulting study contains:

a. 2N pictures of the retina and one external picture. Each retinal
   picture is labeled in the acquisition information to indicate its
   position in the local N-spot definition. The series is not labeled,
   each picture is labeled OS or OD as appropriate.

   .. note::

      DICOM uses L, R, and B in the Image Laterality Attribute
      (0020,0062). The actual encodings will be L, R, or B. Ophthalmic
      equipment can convert this to OS, OD, and OU before display.

b. In the acquisition information of every picture, the IOP and
   refractive state information is replicated.

c. Since there are no stereo pictures taken, there is no Stereometric
   Relationship IOD instance created.

The pictures may or may not be in the same Series.

.. _sect_U.1.2:

Routine N-spot Exam With Exceptions
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

A routine N-spot retinal photography exam is ordered for both eyes.
During the exam a lesion is observed in the right eye. The lesion spans
several spots, so an additional wide angle view is taken that captures
the complete lesion. Additional narrow angle views of the lesion are
captured in stereo. After completing the N-spot exam, several slit lamp
pictures are taken to further detail the lesion outline.

The resulting study contains:

a. 2N pictures of the retina and one external picture, one additional
   wide angle picture of the abnormal retina, 2M additional pictures for
   the stereo detail of the abnormal retina, and several slit lamp
   pictures of the abnormal eye. The different lenses and lighting
   parameters are documented in the acquisition information for each
   picture.

b. One instance of a Stereometric Relationship IOD, indicating which of
   the stereo detail pictures above should be used as stereo pairs.

The pictures may or may not be in the same Series.

.. _sect_U.1.3:

Routine Flourescein Exam
~~~~~~~~~~~~~~~~~~~~~~~~

A routine fluorescein exam is ordered for one eye. The procedure
includes:

a. Routine stereo N-spot pictures of both eyes, routine external
   picture, and current IOP.

b. Reference stereo picture of each eye using filtered lighting

c. Fluorescein injection

d. Capture of 20 stereo pairs with about 0.7 seconds between pictures in
   a pair and 3-5 seconds between pairs.

e. Stereo pair capture of each eye at increasing intervals for the next
   10 minutes, taking a total of 8 pairs for each eye.

The result is a study with:

a. The usual 2N+1 pictures from the N-spot exam

b. Four pictures taken with filtered lighting (documented in acquisition
   information) that constitute a stereo pair for each eye.

c. 40 pictures (20 pairs) for one eye of near term fluorescein. These
   include the acquisition information, lighting context, and time
   stamp.

d. 32 pictures (8 pairs for each eye) of long term fluorescein. These
   include acquisition information, lighting context, and time stamp.

e. One Stereometric Relationship IOD, indicating which of the above OP
   instances should be used as stereo pairs.

The pictures of a) through d) may or may not be in the same series.

.. _sect_U.1.4:

External Examination
~~~~~~~~~~~~~~~~~~~~

The patient presents with a generic eye complaint. Visual examination
reveals a possible abrasion. The general appearance of the eyes is
documented with a wide angle shot, followed by several detailed pictures
of the ocular surface. A topical stain is applied to reveal details of
the surface lesion, followed by several additional pictures. Due to the
nature of the examination, no basic ophthalmic measurements were taken.

The result is a study with one or more series that contains:

a. One overall external picture of both eyes

b. Several close-up pictures of the injured eye

c. Several close-up pictures of the injured eye after topical stain.
   These pictures have the additional stain information conveyed in the
   acquisition information for these pictures.

.. _sect_U.1.5:

External Examination With Intention
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

The patient is suspected of a nervous system injury. A series of
external pictures are taken with the patient given instructions to
follow a light with his eyes. For each picture the location of the light
is indicated by the patient intent information, (e.g., above, below,
patient left, patient right).

The result is a study with one or more series that contains:

a. Individual pictures with each picture using the patient intent field
   to indicate the intended direction.

.. _sect_U.1.6:

External Examination With Drug Application
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

Patient is suspected of myaesthenia gravis. Both eyes are imaged in
normal situation. Then after Tensilon® (edrophonium chloride) injection
a series of pictures is taken. The time, amount, and method of Tensilon®
(edrophonium chloride) administration is captured in the acquisition
information. The time stamps of the pictures are used in conjunction
with the behavior of the eyelids to assess the state of the disease.

.. note::

   Tensilon® is a registered trademark of Roche Laboratories.

The result is a study with one or more series that contains:

a. Multiple reference pictures prior to test

b. Pictures with acquisition information to document drug administration
   time.

.. _sect_U.1.7:

Routine Stereo Camera Examination
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

A stereo optic disk examination is ordered for a patient with glaucoma.
For this examination, the IOP does not need to be measured. The
procedure includes:

1. Mydriasis using agent at time *t*

2. N stereo pictures (camera pictures right and left stereo picture
   simultaneously) of the optic disk region at the time *t+s*

The result is a study with:

a. N right and N left stereo pictures. These include acquisition
   information, lighting context, agent and time stamps.

   1. One Stereometric Relationship SOP Instance, indicating that the
      above OP images should be used as stereo pairs.

.. _sect_U.1.8:

Relative Image Position Definitions
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

Ophthalmic mapping usually occurs in the posterior region of the fundus,
typically in the macula or the optic disc. However, this or other
imaging may occur anywhere in the fundus. The mapping data has clinical
relevance only in the context of its location in the fundus, so this
must be appropriately defined. codes and the ocular fundus locations
they represent are defined by anatomical landmarks and are described
using conventional anatomic references, e.g., superior, inferior,
temporal, and nasal. `figure_title <#figure_U.1.8-1>`__ is a schematic
representation of the fundus of the left eye, and provides additional
clarification of the anatomic references used in the image location
definitions. A schematic of the right eye is omitted since it is
identical to the left eye, except horizontally reversed (Temporal→Nasal,
Nasal→Temporal).

The spatial precision of the following location definitions vary
depending upon their specific reference. Any location that is described
as "centered" is assumed to be positioned in the center of the
referenced anatomy. However, the center of the macula can be defined
visually with more precision than that of the disc or a lesion. The
locations without a "center" reference are approximations of the general
quadrant in which the image resides.

.. note::

   An image < 15° angular subtend in the same position should be
   considered Lesion Centered.

Following are general definitions used to understand the terminology
used in the code definitions.

-  Central zone - a circular region centered vertically on the macula
   and extending one disc diameter nasal to the nasal margin of the disc
   and four disc diameters temporal to the temporal margin of the disc.

-  Equator - the border between the mid-periphery and periphery of the
   retinal and corresponding to a circle approximately coincident with
   the ampulae of the vortex veins

-  Superior - any region that is located superiorly to a horizontal line
   bisecting the macula

-  Inferior - any region that is located inferiorly to a horizontal line
   bisecting the macula

-  Temporal - any region that is located temporally to a vertical line
   bisecting the macula

-  Nasal - any region that is located nasally to a vertical line
   bisecting the macula

-  Mid-periphery - A circular zone of the retina extending from the
   central zone to the equator

-  Periphery - A zone of the retinal extending from the equator to the
   ora serrata.

-  Ora Serrata - the most anterior extent and termination of the retina

-  Lesion - any pathologic object of regard

`figure_title <#figure_U.1.8-1>`__ illustrates anatomical representation
of defined regions of the fundus of the left eye according to anatomical
markers. The right eye has the same representations but reversed
horizontally so that temporal and nasal are reversed with the macula
remaining temporal to the disc.

Modified after Welch Allyn:
http://www.welchallyn.com/wafor/students/Optometry-Students/BIO-Tutorial/BIO-Observation.htm.

.. _sect_U.2:

Typical Sequence of Events
--------------------------

The following shows the proposed sequence of events using individual
images that are captured for later stereo viewing, with the stereo
viewing relationships captured in the stereometric relationship
instance.

The instances captured are all time stamped so that the fluorescein
progress can be measured accurately. The acquisition and equipment
information captures the different setups that are in use:

a. Acquisition information A is the ordinary illumination and planned
   lenses for the examination.

b. Acquisition information B is the filtered illumination, filtered
   viewing, and lenses appropriate for the fluorescein examination.

c. Acquisition information C indicates no change to the equipment
   settings, but once the injection is made, the subsequent images
   include the drug, method, dose, and time of delivery.

.. _sect_U.3:

Ophthalmic Tomography Use Cases (Informative)
---------------------------------------------

Optical tomography uses the back scattering of light to provide
cross-sectional images of ocular structures. Visible (or near-visible)
light works well for imaging the eye because many important structures
are optically transparent (cornea, aqueous humor, lens, vitreous humor,
and retina - see `figure_title <#figure_U.3-1>`__).

To provide analogy to ultrasound imaging, the terms A-scan and B-scan
are used to describe optical tomography images. In this setting, an
A-scan is the image acquired by passing a single beam of light through
the structure of interest. An A-scan image represents the optical
reflectivity of the imaged tissue along the path of that beam - a
one-dimensional view through the structure. A B-scan is then created
from a collection of adjacent A-scan images - a two dimensional image.
It is also possible to combine multiple B-scans into a 3-dimensional
image of the tissue.

When using optical tomography in the eye it is desirable to have
information about the anatomic and physiologic state of the eye.
Measurements like the patient's refractive error and axial eye length
are frequently important for calculating magnification or minification
of images. The accommodative state and application of pupil dilating
medications are important when imaging the anterior segment of the eye
as they each cause shifts in the relative positions of ocular
structures. The use of dilating medications is also relevant when
imaging posterior segment structures because a small pupil can account
for poor image quality.

.. _sect_U.3.1:

Anterior Chamber Tomography
~~~~~~~~~~~~~~~~~~~~~~~~~~~

.. _sect_U.3.1.1:

Anterior Chamber Exam For Phakic Intraocular Lens Surgery Planning
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

Ophthalmic tomography may be used to plan placement of a phakic
intraocular lens (IOL). A phakic IOL is a synthetic lens placed in the
anterior segment of the eye in someone who still has their natural
crystalline lens (i.e., they are "phakic"). This procedure is done to
correct the patient's refractive error, typically a high degree of
myopia (near-sightedness). The exam will typically be performed on both
eyes, and each eye may be examined in a relaxed and accommodated state.
Refractive information for each eye is required to interpret the
tomographic study.

A study consists of one or more B-scans (see
`figure_title <#figure_U.3-2>`__) and one or more instances of
refractive state information. There may be a reference image of the eye
associated with each B-scan that shows the position of the scan on the
eye.

.. _sect_U.3.1.2:

Anterior Chamber Angle Exam
^^^^^^^^^^^^^^^^^^^^^^^^^^^

The anterior chamber angle is defined by the angle between the iris and
cornea where they meet the sclera. This anatomic feature is important in
people with narrow angles. Since the drainage of aqueous humor occurs in
the angle, a significantly narrow angle can impede outflow and result in
increased intraocular pressure. Chronically elevated intraocular
pressures can result in glaucoma. Ophthalmic tomography represents one
way of assessing the anterior chamber angle.

B-scans are obtained of the anterior segment including the cornea and
iris. Scans may be taken at multiple angles in each eye (see
`figure_title <#figure_U.3-2>`__). A reference image may be acquired at
the time of each B-scan(s). Accommodative and refractive state
information are also important for interpretation of the resulting
tomographic information.

Note in the Figure the ability to characterize the narrow angle between
the iris and peripheral cornea.

.. _sect_U.3.1.4:

Corneal Exam
^^^^^^^^^^^^

As a transparent structure located at the front of the eye, the cornea
is ideally suited to optical tomography. There are multiple disease
states including glaucoma and corneal edema where the thickness of the
cornea is relevant and tomography can provide this information using one
or more B-scans taken at different angles relative to an axis through
the center of the cornea.

Tomography is also useful for defining the curvature of the cornea.
Accurate measurements of the anterior and posterior curvatures are
important in diseases like keratoconus (where the cornea "bulges"
abnormally) and in the correction of refractive error via surgery or
contact lenses. Measurements of corneal curvature can be derived from
multiple B-scans taken at different angles through the center of the
cornea.

In both cases, a photograph of the imaged structure may be associated
with each B-scan image.

.. _sect_U.3.2:

Posterior Segment Tomography
~~~~~~~~~~~~~~~~~~~~~~~~~~~~

.. _sect_U.3.2.1:

Retinal Nerve Fiber Layer Exam
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

The Retinal Nerve Fiber Layer (RNFL) is made up of the axons of the
ganglion cells of the retina. These axons exit the eye as the optic
nerve carrying visual signals to the brain. RNFL thinning is a sign of
glaucoma and other optic nerve diseases.

An ophthalmic tomography study contains one or more circular scans,
perhaps at varying distances from the optic nerve. Each circular scan
can be "unfolded" and treated as a B-scan used to assess the thickness
of the nerve fiber layer (see `figure_title <#figure_U.3-3>`__). A
fundus image that shows the scan location on the retina may be
associated with each B-scan. To detect a loss of retinal nerve fiber
cells the exam might be repeated one or multiple times over some period
of time. The change in thickness of the nerve fiber tissue or a trend
(serial plot of thickness data) might be used to support the diagnosis.

In the Figure, the pseudo-colored image on the left shows the various
layers of the retina in cross section with the nerve fiber layer between
the two white lines. The location of the scan is indicated by the bright
circle in the photograph on the right.

.. _sect_U.3.2.2:

Macular Exam
^^^^^^^^^^^^

The macula is located roughly in the center of the retina, temporal to
the optic nerve. It is a small and highly sensitive part of the retina
responsible for detailed central vision. Many common ophthalmic diseases
affect the macula, frequently impacting the thickness of different
layers in the macula. A series of scans through the macula can be used
to assess those layers (see `figure_title <#figure_U.3-4>`__).

A study may contain a series of B-scans. A fundus image showing the scan
location(s) on the retina may be associated with one or more B-scans. In
the Figure, the corresponding fundus photograph is in the upper left.

.. _sect_U.3.2.3:

Angiographic Exams
^^^^^^^^^^^^^^^^^^

Some color retinal imaging studies are done to determine vascular
caliber of retinal vessels, which can vary throughout the cardiac cycle.
Images are captured while connected to an ECG machine or a cardiac pulse
monitor allowing image acquisition to be synchronized to the cardiac
cycle.

Angiography is a procedure that requires a dye to be injected into the
patient for the purpose of enhancing the imaging of vascular structures
in the eye. A standard step in this procedure is imaging the eye at
specified intervals to detect the pooling of small amounts of dye and/or
blood in the retina. For a doctor or technician to properly interpret
angiography images it is important to know how much time had elapsed
between the dye being injected in the patient (time 0) and the image
frame being taken. It is known that such dyes can have an affect on OPT
tomographic images as well (and it may be possible to use such dyes to
enhance vascular structure in the OPT images), therefore time
synchronization will be applied to the creation of the OPT images as
well as any associated OP images

The angiographic acquisition is instantiated as a multi-frame OPT Image.
The variable time increments between frames of the image are captured in
the Frame Time Vector of the OPT Multi-frame Module. For multiple sets
of images, e.g., sets of retinal scan images, the Slice Location Vector
will be used in addition to the Frame Time Vector. For 5 sets of 6 scans
there will be 30 frames in the Multi-frame Image. The first 6 values in
the Frame Time Vector will give the time from injection to the first set
of scans, the second 6 will contain the time interval for the second set
of 6 scans, and so on, for a total of 5 time intervals.

Another example of an angiographic study with related sets of images is
a sequence of SLO/OCT/"ICG filtered" image triples (or SLO/OCT image
pairs) that are time-stamped relative to a user-defined event. This
user-defined event usually corresponds to the inject time of ICG
(indocyanine green) into the patients blood stream. The resultant images
form an angiography study where the patient's blood flow can be observed
with the "ICG filtered" images and can be correlated with the
pathologies observed in the SLO and OCT images that are spatially
related to the ICG image with a pixel-to-pixel correspondence on the X-Y
plane.

.. _sect_U.3.2.4:

3D Reconstruction Exam
^^^^^^^^^^^^^^^^^^^^^^

The prognosis of some pathologies can be aided by a 3D visualization of
the affected areas of the eye. For example, in certain cases the density
of cystic formations or the amount of drusen present can be hard to
ascertain from a series of unrelated two-dimensional longitudinal images
of the eye. However, some OCT machines are capable of taking a sequence
of spatially related two-dimensional images in a suitably short period
of time. These images can either be oriented longitudinally
(perpendicular to the retina) or transversely (near-parallel to the
retina). Once such a sequence has been captured, it then becomes
possible for the examined volume of data to be reconstructed for an
interactive 3D inspection by a user of the system (see
`figure_title <#figure_U.3-5>`__). It is also possible for measurements,
including volumes, to be calculated based on the 3D data.

A reference image is often combined with the OCT data to provide a means
of registering the 3D OCT data-set with a location on the surface of the
retina (see `figure_title <#figure_U.3-6>`__ and
`figure_title <#figure_U.3-7>`__).

.. _sect_U.3.2.5:

Transverse Imaging
^^^^^^^^^^^^^^^^^^

While the majority of ophthalmic tomography imaging consists of sets of
longitudinal images (also known as B scans or line scans), transverse
images (also known as coronal or "en face" images) can also provide
useful information in determining the full extent of the volume affected
by pathology.

Longitudinal images are oriented in a manner that is perpendicular to
the structure being examined, while transverse images are oriented in an
"en face" or near parallel fashion through the structure being examined.

Transverse images can be obtained from a directly as a single scan (as
shown in `figure_title <#figure_U.3-8>`__ and
`figure_title <#figure_U.3-9>`__) or they can also be reconstructed from
3D data (as shown in `figure_title <#figure_U.3-10>`__ and
`figure_title <#figure_U.3-11>`__). A sequence of transverse images can
also be combined to form 3D data.

`figure_title <#figure_U.3-8>`__, `figure_title <#figure_U.3-9>`__,
`figure_title <#figure_U.3-10>`__ and `figure_title <#figure_U.3-11>`__
are all images of the same pathology in the same eye, but the two
different orientations provide complementary information about the size
and shape of the pathology being examined. For example, when examining
macular holes, determining the amount of surrounding cystic formation is
important aid in the following treatment. Determining the extent of such
cystic formation is much more easily ascertained using transverse images
rather than longitudinal images. Transverse images are also very useful
in locating micro-pathologies such as covered macular holes, which may
be overlooked using conventional longitudinal imaging.

In `figure_title <#figure_U.3-10>`__, the blue green and pink lines show
the correspondence of the three images. In
`figure_title <#figure_U.3-11>`__, the Transverse image is highlighted
in yellow.

