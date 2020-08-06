.. _chapter_OOOO:

Encoding Perfusion Parameters for Parametric Maps and ROI Measurements (Informative)
====================================================================================

This Annex contains examples of how to encode perfusion models and
acquisition parameters within the Quantity Definition Sequence of
Parametric Maps and in ROIs in Measurement Report SR Documents.

Some measurements described as "relative" or "normalized" are calculated
by dividing the measurement in a region of interest by a corresponding
measurement from a reference region chosen for comparison purposes.

The approach suggested is to describe that a perfusion value is being
measured by using absolute or relative regional blood flow or volume
(generic) as the concept name of the numeric measurement, and to add
post-coordinated concept modifiers to describe:

-  the general anatomic location and type of finding that mirror common
   usage of terminology specific to the application

-  the size of any reference region used

-  a coded description of the location of any reference region in terms
   of:

   -  anatomic site (drawn from CID 7192 "Anatomical Structure
      Segmentation Property Types")

   -  laterality (drawn from or )

Also illustrated is how the (121050, DCM, "Equivalent Meaning of Concept
Name") can be used to communicate a single human readable textual
description for the entire concept.

The example used is from the oncology domain, but similar patterns can
be used for other applications, e.g., for stroke.

.. _sect_OOOO.1:

Encoding Relative Cerebral Tumor Blood Flow for Parametric Maps
---------------------------------------------------------------

This example shows how to use the to describe pixel values of blood flow
maps. It elaborates on the simple example provided in by adding coded
concepts that describe the location of the measurement and the location
and size of the reference region.

-  Real World Value Mapping Sequence (0040,9096)

   -  ...

   -  Real World Value Intercept (0040,9224) = "0"

   -  Real World Value Slope (0040,9225) = "1E-03"

   -  LUT Explanation (0028,3003) = "Relative Cerebral Tumor Blood Flow,
      relative to 150mm2 contralateral normal cerebellar gray matter"

   -  LUT Label (0040,9210) = "rCBF"

   -  Measurement Units Code Sequence (0040,08EA) = ({ratio}, UCUM,
      "ratio")

   -  Quantity Definition Sequence (0040,9220):

      -  CODE `(246205007, SCT,
         "Quantity") <http://snomed.info/id/246205007>`__ = (126397,
         DCM, "Relative Regional Blood Flow)

      -  CODE `(363698007, SCT, "Finding
         Site") <http://snomed.info/id/363698007>`__ = `(12738006, SCT,
         "Brain") <http://snomed.info/id/12738006>`__

      -  CODE (121071, DCM, "Finding") = `(108369006, SCT,
         "Neoplasm") <http://snomed.info/id/108369006>`__

      -  CODE `(C94970, NCIt, "Reference
         Region") <http://ncit.nci.nih.gov/ncitbrowser/ConceptReport.jsp?dictionary=NCI_Thesaurus&code=C94970>`__
         = `(25991003, SCT, "Cerebellar
         Cortex") <http://snomed.info/id/25991003>`__

         -  CODE `(272741003, SCT,
            "Laterality") <http://snomed.info/id/272741003>`__ =
            `(255209002, SCT,
            "Contralateral") <http://snomed.info/id/255209002>`__

         -  NUMERIC `(42798000, SCT,
            "Area") <http://snomed.info/id/42798000>`__ = 150 (mm2,
            UCUM, "mm2")

      -  TEXT (121050, DCM, "Equivalent Meaning of Concept Name") =
         "Relative cerebral tumor blood flow relative to 150mm2
         contralateral normal cerebellar gray matter"

In this usage, the text of the (121050, DCM, "Equivalent Meaning of
Concept Name") is redundant with the value of LUT Explanation
(0028,3003); either or both could be omitted.

The qualifiers of the quantity in this example, specifically the finding
and finding site, are intentionally more generic (i.e., brain and
neoplasm, respectively) than the more specific locations used in the SR
examples that follow (i.e., left temporal lobe and primary neoplasm),
since the purpose is to specify the type of the quantity, not encode an
entire report in the quantity definition.

The nesting of the indented modifiers in the example illustrates that
laterality and area are modifiers of the reference region (i.e., encoded
in the Content Item Modifier Sequence (0040,0441) of the Quantity
Definition Sequence (0040,9220)).

.. _sect_OOOO.2:

Encoding Relative Cerebral Tumor Blood Volume for ROIs in Measurement Report SR Documents
-----------------------------------------------------------------------------------------

This example shows how to describe the total relative cerebral blood
volume value of a region of interest that is a tumor in the left
temporal lobe. In this case the template used is TID 1419 ROI
Measurements within TID 1411 “Volumetric ROI Measurements” to separately
encode the ROI with the total relative CBV and the ROI for the reference
region with its size, with the relationship between them implicit in the
presence of a coded reference region.

For clarity, the enclosure of the content items within a Measurement
Group container and the accompanying tracking identifiers and spatial
information (coordinates and image and/or segmentation references) are
not shown here.

-  CODE (121071, DCM, "Finding") = `(86049000, SCT, "Neoplasm,
   Primary") <http://snomed.info/id/86049000>`__

-  NUM (126398, DCM, "Relative Regional Blood Volume) = 1.2 ({ratio},
   UCUM, "ratio")

   -  *HAS CONCEPT MOD* CODE `(363698007, SCT, "Finding
      Site") <http://snomed.info/id/363698007>`__ = `(78277001, SCT,
      "Temporal lobe") <http://snomed.info/id/78277001>`__

      -  *HAS CONCEPT MOD* CODE `(272741003, SCT,
         "Laterality") <http://snomed.info/id/272741003>`__ = `(7771000,
         SCT, "Left") <http://snomed.info/id/7771000>`__

   -  *HAS CONCEPT MOD* CODE (121401, DCM, "Derivation") = `(255619001,
      SCT, "Total") <http://snomed.info/id/255619001>`__

   -  *HAS CONCEPT MOD* TEXT (121050, DCM, "Equivalent Meaning of
      Concept Name") = "Total tumor blood volume relative to 150mm2
      contralateral normal cerebral white matter"

The reference region, its blood flow and size, would be specified as:

-  CODE (121071, DCM, "Finding") = `(C94970, NCIt, "Reference
   Region") <http://ncit.nci.nih.gov/ncitbrowser/ConceptReport.jsp?dictionary=NCI_Thesaurus&code=C94970>`__

-  NUM (126391, DCM, "Absolute Regional Blood Volume) = 34.6
   (ml/(100.ml), UCUM, "ml/(100.ml)")

   -  *HAS CONCEPT MOD* CODE `(363698007, SCT, "Finding
      Site") <http://snomed.info/id/363698007>`__ = `(68523003, SCT,
      "Cerebral White Matter") <http://snomed.info/id/68523003>`__

      -  *HAS CONCEPT MOD* CODE `(272741003, SCT,
         "Laterality") <http://snomed.info/id/272741003>`__ =
         `(255209002, SCT,
         "Contralateral") <http://snomed.info/id/255209002>`__

   -  *HAS CONCEPT MOD* CODE (121401, DCM, "Derivation") = `(255619001,
      SCT, "Total") <http://snomed.info/id/255619001>`__

-  NUM `(42798000, SCT, "Area") <http://snomed.info/id/42798000>`__ =
   150 (mm2, UCUM, "mm2")

Alternatively, if the absolute blood volume of the reference region is
not available, then its size can be specified alone, e.g.:

-  CODE (121071, DCM, "Finding") = `(C94970, NCIt, "Reference
   Region") <http://ncit.nci.nih.gov/ncitbrowser/ConceptReport.jsp?dictionary=NCI_Thesaurus&code=C94970>`__

-  NUM `(42798000, SCT, "Area") <http://snomed.info/id/42798000>`__ =
   150 (mm2, UCUM, "mm2")

   -  *HAS CONCEPT MOD* CODE `(363698007, SCT, "Finding
      Site") <http://snomed.info/id/363698007>`__ = `(68523003, SCT,
      "Cerebral White Matter") <http://snomed.info/id/68523003>`__

      -  *HAS CONCEPT MOD* CODE `(272741003, SCT,
         "Laterality") <http://snomed.info/id/272741003>`__ =
         `(255209002, SCT,
         "Contralateral") <http://snomed.info/id/255209002>`__

The use of a specific reference region may be made explicit if the
detailed information for both of the two source measurements, the
absolute CBV for the lesion and the reference region, is available, in
which case they could be encoded as their own instances of TID 1411
“Volumetric ROI Measurements”, and then the derived relative measurement
encoded using TID 1420 "Measurements Derived From Multiple ROI
Measurements", as follows:

-  NUM (126398, DCM, "Relative Regional Blood Volume) = 1.2 ({ratio},
   UCUM, "ratio")

   -  *R-INFERRED FROM* reference to measurement group content item of
      absolute measurement (Row 1 of TID 1411)

   -  *R-INFERRED FROM* reference to measurement group content item of
      reference region measurement (Row 1 of TID 1411)

.. _sect_OOOO.5:

Informative References
----------------------

This section lists useful references related to the taxonomy of
perfusion measurements.

.. _biblio_OOOO.5.1:

Perfusion Measurement Descriptions
----------------------------------

Wetzel 2002 Wetzel SG Cha S Johnson G et al 2002 224 3 797–803
http://dx.doi.org/10.1148/radiol.2243011014

Bjørnerud 2010 Bjørnerud A Emblem KE 2010 30 5 1066–78
http://dx.doi.org/10.1038/jcbfm.2010.4

Knutsson 2004 Knutsson L Ståhlberg F Wirestam R 2004 22 6 789–98
http://dx.doi.org/10.1016/j.mri.2003.12.002

Ziegelitz 2009 Ziegelitz D Starck G Mikkelsen IK et al 2009 62 1 56–65
http://dx.doi.org/10.1002/mrm.21975

Jain 2011 Jain R 2011 32 9 1570-1577 http://doi.org/10.3174/ajnr.A2263

Wintermark 2001 Wintermark M Thiran JP Maeder P et al 2001 22 5 905–14
http://www.ajnr.org/content/22/5/905

