.. _chapter_EEEE:

Encoding Diffusion Model Parameters for Parametric Maps and ROI Measurements (Informative)
==========================================================================================

This Annex contains examples of how to encode diffusion models and
acquisition parameters within the Quantity Definition Sequence of
Parametric Maps and in ROIs in Measurement Report SR Documents.

The approach suggested is to describe that an ADC value is being
measured by using ADC (generic) as the concept name of the numeric
measurement, and to add post-coordinated concept modifiers to describe:

-  the model (e.g., mono-exponential, bi-exponential or other
   multi-compartment models) (drawn from )

-  the method of fitting the data points to that model (e.g., for
   mono-exponential models, log of ratio of two samples, linear
   least-squares for log-intensities of all b-values) (drawn from )

-  relevant numeric parameters, such as the b-values used during
   acquisition of the source images (drawn from )

The model and method of fitting are encoded separately since even though
the method of fitting is sometimes dependent on the model, the model may
be known but not the method of fitting, or there may be no code for the
method of fitting.

.. note::

   1. The generic concept of ADC, (113041, DCM, "Apparent Diffusion
      Coefficient"), is used, rather than the specific concept of
      ADC\ :sub:`m`, (113290, DCM, "Mono-exponential Apparent Diffusion
      Coefficient"), since the model is expressed in a post-coordinated
      manner. Most clinical users will not be concerned with which model
      was used, and so the ability to display and query for a single
      generic concept is preferred. However, model-specific
      pre-coordinated concepts for ADC are provided, as are concepts for
      other model parameters when a single ADC concept is inappropriate,
      e.g., for the fast and slow components of a bi-dimensional model.

   2. The generic concept of `(370129005, SCT, "Measurement
      Method") <http://snomed.info/id/370129005>`__ is used to describe
      the model, rather than being used to described the fitting method,
      since the model is the more important aspect of the measurement to
      distinguish. This pattern is consistent with historical precedent
      (e.g., in `Measurement Report SR Document Planar ROI on DCE-MR
      Tracer Kinetic Model Example <#sect_RRR.3>`__ the model (Extended
      Tofts) for DCE-MR measurements is described using the Measurement
      Method and the fitting method is not described).

Also illustrated is how the (121050, DCM, "Equivalent Meaning of Concept
Name") can be used to communicate a single human readable textual
description for the entire concept.

.. _sect_EEEE.1:

Encoding Diffusion Model Parameters for Parametric Maps
-------------------------------------------------------

This example shows how to use the to describe pixel values of an ADC
parametric map obtained from a pair of B0 and B1000 images fitting the
log ratio ot two samples to a mono-exponential function (single
compartment model). It elaborates on the simple example provided in by
adding coded concepts that describe the model, the method of fitting and
listing the b-values used.

-  Real World Value Mapping Sequence (0040,9096)

   -  ...

   -  Real World Value Intercept (0040,9224) = "0"

   -  Real World Value Slope (0040,9225) = "1E-06"

   -  LUT Explanation (0028,3003) = "ADC mm2/s mono-exponential log
      ratio B0 and B1000"

   -  LUT Label (0040,9210) = "ADC mm2/s"

   -  Measurement Units Code Sequence (0040,08EA) = (mm2/s, UCUM,
      "mm2/s")

   -  Quantity Definition Sequence (0040,9220):

      -  CODE `(246205007, SCT,
         "Quantity") <http://snomed.info/id/246205007>`__ = (113041,
         DCM, "Apparent Diffusion Coefficient")

      -  CODE `(370129005, SCT, "Measurement
         Method") <http://snomed.info/id/370125004>`__ = (113250, DCM,
         "Mono-exponential ADC model")

      -  CODE (113241, DCM, "Model fitting method") = (113260, DCM, "Log
         of ratio of two samples")

      -  NUMERIC (113240, DCM, "Source image diffusion b-value") = 0
         (s/mm2, UCUM, "s/mm2")

      -  NUMERIC (113240, DCM, "Source image diffusion b-value") = 1000
         (s/mm2, UCUM, "s/mm2")

      -  TEXT (121050, DCM, "Equivalent Meaning of Concept Name") = "ADC
         mono-exponential log ratio B0 and B1000"

In this usage, the text of the (121050, DCM, "Equivalent Meaning of
Concept Name") is redundant with the value of LUT Explanation
(0028,3003); either or both could be omitted.

The parameter describing a b-value of 0 is expected to be sent, and one
should not assume that a b-value of 0 is used if it is absent, since
some methods may use a low b-value (e.g., 50), which is not 0.

There is no consensus in the MR community or scientific literature as to
the appropriate units to use to report diffusion coefficient values to
the user, nor amongst the MR vendors as to how to encode them. In this
example, the units are specified as "s/mm2". If the diffusion
coefficient pixel values were encoded as integers with such a unit, they
could then be encoded with a Rescale Slope of 1E-06, given the typical
range of values encountered. Alternatively, the pixel values could be
encoded as floating point pixel data values with identity rescaling. Or,
if the units were specified "um2/s" (or "10-6.mm2/s", which is the same
thing), then integer pixels could be used with a Rescale Slope of 1.
Application software can of course rescale the values for display and
convert the units as appropriate to the user's preference, as long as
they are unambiguously encoded.

.. _sect_EEEE.2:

Encoding Diffusion Model Parameters for ROIs in Measurement Report SR Documents
-------------------------------------------------------------------------------

This example shows how to describe the mean ADC value of a region of
interest on a volume of ADC values obtained from a pair of B0 and B1000
images fitting the log ratio ot two samples to a mono-exponential
function (single compartment model). In this case the template used is .

-  NUM (113041, DCM, "Apparent Diffusion Coefficient") = 0.75E-3 (mm2/s,
   UCUM, "mm2/s")

   -  *HAS CONCEPT MOD* CODE `(370129005, SCT, "Measurement
      Method") <http://snomed.info/id/370125004>`__ = (113250, DCM,
      "Mono-exponential ADC model")

   -  *HAS CONCEPT MOD* CODE (113241, DCM, "Model fitting method") =
      (113260, DCM, "Log of ratio of two samples")

   -  *HAS CONCEPT MOD* CODE (121401, DCM, "Derivation") = `(373098007,
      SCT, "Mean") <http://snomed.info/id/373098007>`__

   -  *INFERRED FROM* NUM (113240, DCM, "Source image diffusion
      b-value") = 0 (s/mm2, UCUM, "s/mm2")

   -  *INFERRED FROM* NUM (113240, DCM, "Source image diffusion
      b-value") = 1000 (s/mm2, UCUM, "s/mm2")

   -  *HAS CONCEPT MOD* TEXT (121050, DCM, "Equivalent Meaning of
      Concept Name") = "Mean ADC mono-exponential log ratio B0 and
      B1000"

.. _sect_EEEE.3:

Relationship of Derived Diffusion Model Parametric Maps to Diffusion Weighted Source Images
-------------------------------------------------------------------------------------------

This example illustrates how to describe the manner in which an ADC
Parametric Map image was derived from B0 and B1000 images. The intent is
to provide links to the images, not to replicate all the information
that can be provided in the Quantity Definition Sequence.

This particular example illustrates the reference from an ADC Parametric
Map to a pair of Enhanced MR images, one for each b-value (or a pair of
subsets of frames of a single Enhanced MR image), but the same principle
is applicable when single frame IODs are used as source or derived
image.

-  Derivation Image Sequence (0008,9124)

   -  Derivation Description (0008,2111) = "Calculation of
      mono-exponential ADC from log of ratio of B0 and B1000 images"

   -  Derivation Code Sequence (0008,9215)

      -  (113041, DCM, "Apparent Diffusion Coefficient")

      -  (113250, DCM, "Mono-exponential ADC from log of ratio of two
         samples")

   -  Source Image Sequence (0008,2112)

      -  Item 1:

         -  Referenced SOP Class UID (0008,1150) of B0 image

         -  Referenced SOP Instance UID (0008,1155) of B0 image

         -  Referenced Frame Number (0008,1160) of B0 frames in image

         -  Purpose of Reference Code Sequence

            -  (121322, DCM, "Source image for image processing
               operation")

      -  Item 2:

         -  Referenced SOP Class UID (0008,1150) of B1000 image

         -  Referenced SOP Instance UID (0008,1155) of B1000 image

         -  Referenced Frame Number (0008,1160) of B1000 frames in image

         -  Purpose of Reference Code Sequence

            -  (121322, DCM, "Source image for image processing
               operation")

In this approach:

-  since multiple items are permitted in the Derivation Code Sequence
   (0008,9215), both the general concept (calculation of ADC) and the
   specific method have been listed; alternatively, just one or the
   other could be provided

-  a textual description has also be provided, which in this case
   provides more information than the structured content (i.e., about
   the b-values used)

-  a generic purpose of reference code has been used, since only a
   single code is permitted and there is no mechanism (other then
   creating pre-coordinated codes for every possible b-value) to convey
   which image (set) was acquired with which b-value; the more specific
   alternative of a coded concept for "source image for ADC calculation"
   would add no value over the concept already described in Derivation
   Code Sequence

-  the SOP Instance UID in the first and second items may be the same,
   but a different range of frames referenced, e.g., if all of the
   source frames (all of the b-values) are in the same instance, as is
   required by the IHE Diffusion (DIFF) profile
   (http://wiki.ihe.net/index.php/MR_Diffusion_Imaging); if all of the
   frames in a single source image are used, then only a single item is
   necessary and the Referenced Frame Number can be omitted.

-  all of the images have been listed in a single item of Derivation
   Image Sequence (0008,9124); alternatively, multiple items of
   Derivation Image Sequence (0008,9124) could be sent. one for each of
   the different b-values used; this would allow Derivation Description
   (0008,2111) to communicate which set contained which b-value, but
   there is no structured way to communicate such numeric parameters
   (other then creating pre-coordinated codes for every possible
   b-value)

.. _sect_EEEE.4:

Image and Frame of Derived Diffusion Model Parametric Maps
----------------------------------------------------------

This example illustrates how to encode the Image and Frame Type values
of an ADC Parametric Map image.

Parametric maps are of the enhanced multi-frame family, so they use the
standard roles of Image Flavor for Value 3 and Derived Pixel Contrast
for Value 4.

The specific requirement are defined in and .

Since this is a derived diffusion image that contains ADC value,
suitable values are:

-  Image Type (0008,0008) = "DERIVED\PRIMARY\DIFFUSION\ADC"

This usage is consistent with the requirements for Image and Frame Type
in the IHE Diffusion (DIFF) profile
(http://wiki.ihe.net/index.php/MR_Diffusion_Imaging).

.. _sect_EEEE.5:

Informative References
----------------------

This section lists useful references related to the taxonomy of ADC
calculation methods.

.. _biblio_EEEE.5.1:

ADC Method Descriptions
-----------------------

Burdette 1998 Burdette JH Elster AD Ricci PE 1998 22 5 792–4
http://journals.lww.com/jcat/pages/articleviewer.aspx?year=1998&issue=09000&article=00023&type=abstract

Barbieri 2016 Barbieri S Donati OF Froehlich JM Thoeny HC 2016 75 5
2175–84 http://dx.doi.org/10.1002/mrm.25765

Bennett 2003 Bennett KM Schmainda KM Bennett RT Rowe DB Lu H Hyde JS
2003 50 727–734 http://dx.doi.org/10.1002/mrm.10581

Gatidis 2016 Gatidis S Schmidt H Martirosian P Nikolaou K Schwenzer NF
2016 43 4 824–32 http://dx.doi.org/10.1002/jmri.25044

Graessner 2011 Graessner J 2011 84-87 Siemens Healthcare
http://clinical-mri.com/wp-content/uploads/software_hardware_updates/Graessner.pdf

Merisaari 2016 Merisaari H Movahedi P Perez IM Toivonen J Pesola M
Taimen P Boström PJ Pahikkala T Kiviniemi A Aronen HJ Jambor I 2016
http://dx.doi.org/10.1002/mrm.26169

Neil 1993 Neil JJ Bretthorst GL 1993 29 5 642–7
http://dx.doi.org/10.1002/mrm.1910290510

Oshio 2014 Oshio K Shinmoto H Mulkern RV 2014 13 191–195
http://dx.doi.org/10.2463/mrms.2014-0016

Toivonen 2015 Toivonen J Merisaari H Pesola M Taimen P Boström PJ
Pahikkala T Aronen HJ Jambor I 2015 74 4 1116–24
http://dx.doi.org/10.1002/mrm.25482

Yablonskiy 2003 Yablonskiy DA Bretthorst GL Ackerman JJH 2003 50 4 664–9
http://dx.doi.org/10.1002/mrm.10578

