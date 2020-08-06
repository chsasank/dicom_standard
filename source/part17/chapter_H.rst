.. _chapter_H:

Clinical Trial Identification Workflow Examples (Informative)
=============================================================

This Annex was formerly located in in the 2003 and earlier revisions of
the Standard.

The Clinical Trial Identification modules are optional. As such, there
are several points in the workflow of clinical trial or research data at
which the Clinical Trial Identification Attributes may be added to the
data. At the Clinical Trial Site, the Attributes may be added at the
scanner, a PACS system, a site workstation, or a workstation provided to
the site by a Clinical Trial Coordinating Center. If not added at the
site, the Clinical Trial Identification Attributes may be added to the
data after receipt by the Clinical Trial Coordinating Center. The
addition of clinical trial Attributes does not itself require changes to
the SOP Instance UID. However, the clinical trial or research protocol
or the process of de-identification may require such a change.

.. _sect_H.1:

Example Use-case
----------------

Images are obtained for the purpose of comparing patients treated with
placebo or the drug under test, then evaluated in a blinded manner by a
team of radiologists at the Clinical Trial Coordinating Center (CTCC).
The images are obtained at the clinical sites, collected by the CTCC, at
which time their identifying Attributes are removed and the Clinical
Trial Identification (CTI) module is added. The de-identified images
with the CTI information are then presented to the radiologists who make
quantitative and/or qualitative assessments. The assessments, and in
some cases the images, are returned to the sponsor for analysis, and
later are contributed to the submission to the regulating authority.

