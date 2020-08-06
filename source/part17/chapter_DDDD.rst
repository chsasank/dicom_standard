.. _chapter_DDDD:

Types of Echocardiography Measurement Specifications (Informative)
==================================================================

.. _sect_DDDD.1:

Overview
--------

Real-world quantities of clinical interest are exchanged in DICOM
Structured Reports. These real-world quantities are identified using
concept codes of three different types:

-  Standard measurements that are defined by professional organizations
   such as the American Society of Echocardiography (ASE), and codified
   by vocabulary standards such as the Logical Observation Identifiers
   Names and Codes (LOINC) or Systematized Nomenclature of Medicine -
   Clinical Terms (SNOMED-CT) standards.

-  Non-Standard measurements that are defined by a medical equipment
   vendor or clinical institution and codified using a private or
   standard Coding Scheme.

-  Adhoc measurements are those measurements that are generally acquired
   one time to quantify some atypical anatomy or pathology that may be
   observed during an exam. These measurements are not codified, but
   rather are described by the image itself and a label assigned at the
   time the measurement is taken.

This Annex discusses the requirements for identifying measurements in
such a manner that they are accurately acquired and correctly
interpreted by medical practitioners.

.. _sect_DDDD.2:

Specification of Standard Measurements
--------------------------------------

Clinical organizations publish recommendations for standardized
measurements that comprise a necessary and sufficient quantification of
particular anatomy and physiology useful in obtaining a clinical
diagnosis. For each measurement recommendation, the measurement
definition is specific enough so that any trained medical practitioner
would know exactly how to acquire the measurement and how to interpret
the measurement. Thus, there would be a 1:1 correspondence between the
intended measurement recommendation and the practitioner's understanding
of the intended measurement and the technique used to measure it
(anatomy and physiology, image view, cardiac/respiratory phase, and
position/orientation of measurement calipers). This is illustrated in
`figure_title <#figure_DDDD.2-1>`__.

The goal is for each recommended measurement to be fully specified such
that every medical practitioner making the measurement on a given
patient at a given time achieves the same result. However, if the
recommendation were to be unclear or ambiguous, different qualified
medical practitioners would achieve different results measuring the same
quantity on the same patient, as illustrated in
`figure_title <#figure_DDDD.2-2>`__.

There are a number of characteristics that should be included in a
measurement recommendation in order to ensure that all practitioners
making that measurement achieve the same results in making the
measurement. Some characteristics are:

-  Anatomy being measured, specified to appropriate level of detail

-  Reference points (e.g., "OFD is measurement in the same plane as BPD
   from the outer table of the proximal skull with the cranial bones
   perpendicular to the US beam to the inner table of the distal skull")

-  Type of measurement (distance, area, volume, velocity, time, VTI,
   etc.)

-  Sampling method (average of several samples, peak value of several
   samples, etc.)

-  Image view in which the measurement is made

-  Cardiac and/or respiratory phase

The measurement definition should specify these characteristics in order
that the definition is clear and unambiguous. Since the characteristics
are published by the professional society as part of the Standard
measurement definition document are incorporated in the codes that are
added to LOINC, a pre-coordinated measurement code is sufficient to
specify the measurement in a structured report.

Because of the detail in the definition of each standard measurement, it
is sufficient to represent such measurements with a pre-coordinated
measurement code and a minimum of circumstantial modifiers. This
approach is being followed by , for example.

.. _sect_DDDD.3:

Specification of Non-standard Measurements
------------------------------------------

Non-Standard Measurements are defined by a particular vendor or clinical
institution, and are not necessarily understood by users of other
vendors' equipment or practitioners in other clinical institutions. A
system producing such measurements cannot expect a consuming application
to implicitly understand the measurement and its characteristics.
Further, such measurements may not be fully understood by the medical
practitioners who are acquiring the measurements, so there is some risk
that the measurement acquired may not match the real-world quantity
intended by the measurement definition, as illustrated by
`figure_title <#figure_DDDD.3-1>`__.

It is important for all non-standard measurement definitions to include
all the characteristics of the measurement as would have been specified
for Standard (baseline) measurement definitions, such as:

-  Anatomy being measured, specified to appropriate level of detail

-  Reference points (e.g., "OFD is measurement in the same plane as BPD
   from the outer table of the proximal skull with the cranial bones
   perpendicular to the US beam to the inner table of the distal skull")

-  Type of measurement (distance, area, volume, velocity, time, VTI,
   etc.)

-  Sampling method (average of several samples, peak value of several
   samples, etc.)

-  Image view in which the measurement is made

-  Cardiac and/or respiratory phase

Fully specifying the characteristics of such measurements is important
for several reasons:

1. Ensuring medical practitioners correctly measure the intended
   real-world quantity

2. Aiding receiving applications in correctly interpreting the
   non-standard measurement and mapping the non-standard measurement to
   the most appropriate internally-supported measurement.

3. Aid in determining whether non-standard measurements from different
   sources are in fact equivalent measurements and could thus be
   described by a common measurement definition.

Each of these reasons is elaborated upon in the sections to follow. This
is the justification for representing such non-standard measurements
using both post-coordinated concepts and a pre-coordinated concept code
for the measurement, such as is done in .

.. _sect_DDDD.3.1:

Acquiring the Intended Real-World Quantity
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

A medical practitioner can be expected to correctly acquire the
real-world quantity intended by the non-standard measurement definition
only if it is completely specified. This includes explicitly specifying
all the essential clinical characteristics as are described for Standard
measurements. While the resultant measurement value can be described by
a pre-coordinated concept code, the characteristics of the intended
real-world quantity must be defined and known.

.. _sect_DDDD.3.2:

Interpreting the Non-Standard Measurement
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

The characteristics of the real-world measurement measured by the
acquisition system and user are conveyed in the mandatory
post-coordinated descriptors recorded alongside the measurement value.

The presence of such post-coordinated descriptors aids the consumer
application in

1. Mapping the non-standard measurement to a corresponding
   internally-supported measurement. The full details provided by
   including the post-coordinated descriptors greatly simplifies the
   task of determining measurement equivalence.

2. Organizing the display of the non-standard measurement values in a
   report. It is clinically useful to structure written reports in a
   hierarchical manner by displaying all measurements that pertain to
   the same anatomical structure or physiological condition together.

3. Interpreting similar anatomical measurements differently depending on
   such characteristics as acquisition image mode (e.g., 2D vs. M-mode
   image). Since the clinical interpretation may depend on this
   information, it should be explicitly included along with the
   measurement concept code/code meaning.

4. Analyzing accumulated report data (trending, data mining, and big
   data analytics)

.. note::

   Some of these benefits are reduced if the context groups specified
   for each post-coordinated descriptor are extended with custom codes.
   A user should take great care when considering the extension of the
   standard context groups to minimize the proliferation of modifier
   codes.

The first time that a consumer application encounters a new
post-coordinated measurement, it will need to evaluate it based on the
values of the post-coordinated descriptors. To help the consumer
application with subsequent encounters with the same type of
measurement, the acquisition system can consistently populate the
Concept Name of the measurement with a code that corresponds to the
collection of post-coordinated descriptor values; effectively a
non-standard, but stable, pre-coordinated measurement code. (See , Row
1)

The presence of the pre-coordinated code in addition to the
post-coordinated descriptors allows subsequent receipt of the same
measurement to utilize the mapping that was performed as described above
and treat the measurement as an effectively pre-coordinated measurement.

If the acquisition system is aware of other pre-coordinated codes (e.g.,
those used by other vendor carts) that are also equivalent to the
collection of post-coordinated descriptor values for a given
measurement, those pre-coordinated codes may be listed as (121050, DCM,
"Equivalent Meaning of Concept Name"). These "known mappings" provided
by the acquisition system can also be useful for consumer applications
trying to recognize or map measurements.

.. _sect_DDDD.3.3:

Determining Equivalence of Measurements from Different Sources
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

It is customary for individual vendors to provide tools to acquire
measurements that aren't currently defined in a Standard measurement
template. In the normal evolution of the Standard, standard measurement
sets are periodically updated to reflect the state of medical practice.
Often, individual vendors and/or clinical users are first to implement
the acquisition of new measurements.

Some measurements may be defined and used within a particular clinical
institution. For maximum interoperability, if there exists a Standard or
vendor-defined measurement concept code for that measurement, the
Standard or vendor-defined concept code should be used instead of
creating a custom measurement code unique to that institution.

Determining whether two or more different measurement definitions
pertain to the same real-world quantity is a non-trivial task. It
requires clinical experts to carefully examine alternative measurement
definitions to determine if two or more definitions are equivalent. This
task is greatly simplified if the distinct characteristics of the
non-standard measurement are explicitly stated and conveyed. If two
measurements differ in one or more critical characteristics then it can
be concluded that the two measurement definitions describe different
real-world quantities. Only those measurements that share all the
critical clinical characteristics need to be carefully examined by
clinical experts to see if they are equivalent.

It may be determined that two measurements that share all specified
clinical characteristics are actually distinct real-world quantities. If
this occurs, it may be an indication that not all relevant clinical
characteristics have been isolated and codified. In this case, the
convention for defining the measurement should be extended to include
the unspecified clinical characteristic.

.. _sect_DDDD.4:

Specification of Adhoc (One-Time) Measurements
----------------------------------------------

In the case of a measurement that is only being performed once, there is
little value in incurring the overhead to specify all measurement
characteristics and assign a code to the measurement as it will never be
used again. Rather, the descriptive text associated with the measurement
may provide sufficient clinical context. Association of the measurement
with the source image (and/or particular points in the source image) can
often provide additional relevant context so it is recommended to
provide image coordinate references in the Structured Report (See ).

If a user finds that the same quantity is being measured repeatedly as
an adhoc measurement, a non-standard measurement definition should be
created for the measurement as described in `Specification of
Non-standard Measurements <#sect_DDDD.3>`__.

