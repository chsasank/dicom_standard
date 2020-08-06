.. _chapter_KK:

Use Cases For The Composite Instance Root Retrieval Classes (Informative)
=========================================================================

The use cases fall into five broad groups:

.. _sect_KK.1:

Clinical Review
---------------

.. _sect_KK.1.1:

Retrieval Based On Report References
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

A referring physician receives radiological diagnostic reports on CT or
MRI examinations. These reports contain references to specific images.
He chooses to review these specific images himself and/or show the
patient. The references in the report point to particular slices. If the
slices are individual images, then they may be obtained individually. If
the slices are part of an enhanced multi-frame CT/MR object, then
retrieval of the whole multi-frame object might take too long. The
Composite Instance Root Retrieve Service allows retrieval of only the
selected frames.

The source of the image and frame references in the report could be KOS,
CDA, SR, presentation states or other sources.

Selective retrieval can also be used to retrieve 2 or more arbitrary
frames, as may be used for digital subtraction (masking), and may be
used with any multi-frame objects, including multi-frame ultrasound, XR
etc.

Features of interest in many long "video" examinations (e.g., endoscopy)
are commonly referenced as times from the start of the examination. The
same benefits of reduced WAN bandwidth use could be obtained by
shortening the MPEG-2, MPEG-4 AVC/H.264, HEVC/H.265 or JPEG 2000 Part 2
Multi-component based stream prior to transmission.

.. _sect_KK.1.2:

Selective Retrieval Without References to Specific Slices
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

Retrieval using the Composite Instance Retrieve Without Bulk Data
Retrieve Service allows determination and retrieval of a suitable subset
of frames. This could for instance be used to retrieve only the slices
with particular imaging characteristics (e.g., T2 weighting from an
enhanced MR object).

.. _sect_KK.2:

Local Use - "Relevant Priors"
-----------------------------

.. _sect_KK.2.1:

Anatomic Sub-region
~~~~~~~~~~~~~~~~~~~

A multi-frame CT or MR may cover a larger area of anatomy than is
required for use as a relevant prior. How the SCU determines which
frames are relevant is outside the scope of the Standard.

.. _sect_KK.2.2:

Worklists
~~~~~~~~~

Relevant priors may be specified by instance and frame references in a
worklist and benefit from the same facilities.

.. _sect_KK.3:

Attribute Based Retrieval
-------------------------

There are times when it would be useful to retrieve from a Multi-frame
Image only those frames satisfying certain dimensionality criteria, such
as those CT slices fitting within a chosen volume. Initial retrieval of
the image using the Composite Instance Retrieve Without Bulk Data
Retrieve Service allows determination and retrieval of a suitable
sub-set of frames.

.. _sect_KK.4:

CAD & Data Mining Applications
------------------------------

Given the massively enhanced amount of dimensional information in the
new CT/MR objects, applications could be developed that would use this
for statistical purposes without needing to fetch the whole
(correspondingly large) pixel data. The Composite Instance Retrieve
Without Bulk Data Retrieve Service permits this.

.. _sect_KK.5:

Independent WADO Server
-----------------------

A hospital has a large PACS (that supports multi-frame objects) that
does not support WADO. The hospital installs a separate WADO server that
obtains images from the PACS using DICOM. WADO has the means to request
individual frames, supporting many of the above use cases.

