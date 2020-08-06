.. _chapter_LL:

Example SCU Use of The Composite Instance Root Retrieval Classes (Informative)
==============================================================================

.. _sect_LL.1:

Retrieval of Entire Composite Instances
---------------------------------------

There are many modules in DICOM that use the Image SOP Instance
Reference Macro (), which includes the SOP Instance UID and SOP class
UID, but not the Series Instance UID and Study Instance UID. Using the
Composite Instance Root Retrieval Classes however, retrieval of such
instances is simple, as a direct retrieval may be requested, including
only the SOP Instance UID in the Identifier of the C-GET request.

.. _sect_LL.2:

Retrieval of Selected Frame Composite Instances From Multi-frame Objects
------------------------------------------------------------------------

Where the frames to be retrieved and viewed are known in advance, -
e.g., when they are referenced by an Image Reference Macro in a
structured report, then they may be retrieved directly using either of
the Composite Instance Root Retrieval Classes.

.. _sect_LL.3:

Retrieval of Selected Frame Composite Instances From MPEG-2, MPEG-4 AVC/H.264 or HEVC/H.265 Video
-------------------------------------------------------------------------------------------------

If the image has been stored in MPEG-2, MPEG-4 AVC/H.264 or HEVC/H.265
format, and if the SCU has knowledge independent of DICOM as to which
section of a "video" is required for viewing (e.g., perhaps notes from
an endoscopy) then the SCU can perform the following steps:

1. Use known configuration information to identify the available
   transfer syntaxes.

2. If MPEG-2, MPEG-4 AVC/H.264, HEVC/H.265 or JPEG 2000 Part 2
   Multi-component transfer syntaxes are available, then issue a request
   to retrieve the required section.

   The data received may be slightly longer than that requested,
   depending on the position of key frames in the data.

3. If only other transfer syntaxes are available, then the SCU may need
   to retrieve most of the object using Composite Instance Retrieve
   Without Bulk Data Retrieve Service to find the frame rate or frame
   time vector, and then calculate a list of frames to retrieve as in
   the previous sections.

