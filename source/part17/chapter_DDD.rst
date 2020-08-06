.. _chapter_DDD:

Visual Field Static Perimetry Use Cases (Informative)
=====================================================

.. _sect_DDD.1:

Introduction
------------

Automated visual fields are the most commonly used method to assess the
function of the visual system. This is accomplished by sequentially
presenting visual stimuli to the patient and then requiring the patient
press a button if he/she perceives a stimulus. The stimuli are presented
at a variety of points within the area expected to be visible to the
patient and each of those points is tested with multiple stimuli of
varying intensity. The result of this is a spatial map indicating how
well the patient can see throughout his/her visual field.

.. _sect_DDD.2:

Use Cases
---------

.. _sect_DDD.2.1:

Evaluation For Glaucoma
~~~~~~~~~~~~~~~~~~~~~~~

The diagnosis and management of Glaucoma, a disease of the optic nerve,
is the primary use of visual field testing. In this regard, automated
visual fields are used to assess quantitatively the function of the
optic nerve with the intent of detecting defects caused by glaucoma.

The first step in analyzing a visual field report is to confirm that it
came from the correct patient. Demographic information including the
patient's name, gender, date of birth, and perhaps medical record number
are therefore essential data to collect. The patient's age is also
important in the analysis of the visual field (see below) as optic nerve
function changes with age. Finally, it is important to document the
patient's refractive error as this needs to be corrected properly for
the test to be valid.

Second, the clinician needs to assess the reliability of the test. This
can be determined in a number of ways. One of these is by monitoring
patient fixation during the test. To be meaningful, a visual field test
assumes that the subject was looking at a fixed point throughout the
test and was responding to stimuli in the periphery. Currently available
techniques for monitoring this fixation include blind spot mapping,
pupil tracking, and observation by the technician conducting the test.
Blind spot mapping starts by identifying the small region of the visual
field corresponding to the optic nerve head. Since the patient cannot
detect stimuli in this area, any positive response to a stimulus placed
there later in the test indicates that the patient has lost fixation and
the blind spot has "moved". Both pupil tracking and direct observation
by the technician are now easily carried out using a camera focused on
the patient's eye.

Another means of assessing the reliability of the test is to count both
false positive and false negative responses. False positives occur when
the subject presses the button either in response to no stimulus or in
response to a stimulus with intensity significantly below one they had
not detected previously. False negatives are recorded when the patient
fails to respond to stimulus significantly more intense than one they
had previously seen. Taken together, fixation losses, false positives,
and false negatives provide an indication of the quality of the test.

The next phase of visual field interpretation is to assess for the
presence of disease. The first aspect of the visual field data used here
are the raw sensitivity values. These are usually expressed as a
function of the amount of attenuation that could be applied to the
maximum possible stimulus such that the patient could still see it when
displayed. Since a value is available at each point tested in the visual
field, these values can be represented either as raw values or as a
graphical map.

Because the raw intensity values can be affected by a number of factors
including age and other non-optic nerve problems including refractive
error or any opacity along the visual axis (cornea, lens, vitreous), it
is helpful to also evaluate some corrected values. One set of corrected
intensity values is usually some indication of the difference of each
tested point from its expected value based on patient age. Another set
of corrected intensity values, referred to as "Pattern deviation or
"Corrected comparison" are normalized for age and also have a value
subtracted from the deviation at each test point, which is estimated to
be due to diffuse visual field loss This latter set is useful for focal
rather than diffuse defects in visual function. In the case of glaucoma
and most other optic nerve disease, clinicians are more interested in
focal defects so this second set of normalized data is useful.

For all normalized visual field sensitivity data, it is useful to know
how a particular value compares to a group of normal patients. Vendors
of automated visual field machines therefore go to great lengths to
collect data on such "normal" subjects to allow subsequent analysis.
Furthermore, the various sets of values mentioned above can be
summarized further using calculations like a mean and standard
deviation. These values give some idea about the average amount of field
loss (mean) and the focality of that loss (standard deviation).

A final step in the clinical assessment of a visual field test is to
review any disease-specific tests that are performed on the data. One
such test is the Glaucoma Hemifield Test, which has been designed to
identify field loss consistent with glaucoma. These tests are frequently
vendor-specific.

.. _sect_DDD.2.2:

Neurological Disease
~~~~~~~~~~~~~~~~~~~~

In addition to primary diseases of the optic nerve, like glaucoma,
visual fields are useful for assessing damage to the visual pathway
occurring between the optic chiasm and occipital cortex. There is the
same need for demographic information, for assessment of reliability,
and for the various raw and normalized sensitivity values. At this time,
there are no well-established automated tests for the presence of
neurological defects.

.. _sect_DDD.2.3:

Diffuse and Local Defect
~~~~~~~~~~~~~~~~~~~~~~~~

.. _sect_DDD.2.3.1:

Diffuse Defect
^^^^^^^^^^^^^^

The Diffuse Defect is an estimate of the portion of a patient's visual
field loss that is diffuse, or spread evenly across all portions of the
visual field, in dB. In this graphical display, deviation from the
average normal value for each test point is ranked on the x axis from 1
to 59, with 59 being the test point that has the greatest deviation from
normal. Deviations from normal at each test point are represented on the
y axis, in dB. The patient's actual test point deviations are
represented by the thin blue line. Age corrected normal values are
represented by the light blue band. The patient's deviation from normal
at the test point ranked 25% among his or her own deviations is then
estimated to be his or her diffuse visual field loss, represented by the
dark blue band. This provides a graphical estimate of the remaining
visual field loss for this patient, which is then presumed to consist of
local visual field defects, which are more significant in management of
glaucoma than diffuse defects.

.. _sect_DDD.2.4.2:

Local Defect
^^^^^^^^^^^^

The Local Defect is an estimate of the portion of a patient's visual
field loss that is local, or not spread evenly across all portions of
the visual field. The x and y axis in this graphical display have the
same meaning as in the diffuse defect. In this graphical display the top
line/blue band represent age corrected normal values. This line is
shifted downward by the amount estimated to be due to diffuse visual
field loss for this patient, according to the calculation in
`figure_title <#figure_DDD.2-7>`__ (Diffuse Defect). The difference
between the patient's test value at each point in the ranking on the
horizontal axis and the point on the lower curve at the 50% point is
represented by the dark blue section of the graph. This accentuates the
degree of local visual field defect, which is more significant in
management of glaucoma than diffuse defects. The Local Defect is an
index that highly correlates with square root of the loss variance (sLV)
but is less susceptible to false positives. In addition to the usage in
white/white perimetry it is especially helpful as early identifier for
abnormal results in perimetry methods with higher inter subject
variability such as blue/yellow (SWAP) or flicker perimetry. An example
of Local Defect is shown in `figure_title <#figure_DDD.2-8>`__ and is
expressed in dark blue in dB and is normalized to be comparable between
different test patterns.

