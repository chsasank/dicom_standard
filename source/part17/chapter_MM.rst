.. _chapter_MM:

Considerations For Applications Creating New Images From Multi-frame Images
===========================================================================

.. _sect_MM.1:

Scope
-----

The purpose of this annex is to aid those developing SCPs of the
Composite Instance Root Retrieve Service Class. The behavior of the
application when making any of the changes discussed in this annex
should be documented in the conformance statement of the application.

.. _sect_MM.2:

Frame Extraction Issues
-----------------------

There are many different aspects to consider when extracting frames to
make a new object, to ensure that the new image remains a fully valid
SOP Instance, and the following is a non-exhaustive list of important
issues

.. _sect_MM.2.1:

Number of Frames
~~~~~~~~~~~~~~~~

The Number of Frames (0028,0008) Attribute will need to be updated.

.. _sect_MM.2.2:

Start and End Times
~~~~~~~~~~~~~~~~~~~

Any Attributes that refer to start and end times such as Acquisition
Time (0008,0032) and Content Time (0008,0033) must be updated to reflect
the new start time if the first frame is not the same as the original.
This is typically the case where the multi-frame object is a "video" and
where the first frame is not included. Likewise, Image Trigger Delay
(0018,1067) may need to be updated.

.. _sect_MM.2.3:

Time Interval versus Frame Increment Vector
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

The Frame Time (0018,1063) may need to be modified if frames in the new
image are not a simple contiguous sequence from the original, and if
they are irregular, then the Frame Time Vector (0018,1065) will need to
be used in its place, with a corresponding change to the Frame Increment
Pointer (0028,0009). This also needs careful consideration if
non-consecutive frames are requested from an image with non-linearly
spaced frames.

.. _sect_MM.2.4:

MPEG-2, MPEG-4 AVC/H.264 or HEVC/H.265
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

Identifying the location of the requested frames within an MPEG-2,
MPEG-4 AVC/H.264 or HEVC/H.265 data stream is non-trivial, but if
achieved, then little else other than changes to the starting times are
likely to be required for MPEG-2, MPEG-4 AVC/H.264 or HEVC/H.265 encoded
data, as the use-cases for such encoded data (e.g., endoscopy) are
unlikely to include explicit frame related data. See the note below
however for comments on "single-frame" results.

An application holding data in MPEG-2, MPEG-4 AVC/H.264 or HEVC/H.265
format is unlikely to be able to create a range with a frame increment
of greater than one (a calculated frame list with a 3\ :sup:`rd` value
greater than one), and if such a request is made, it might return a
status of AA02: Unable to extract Frames.

The approximation feature of the Time Range form of request is
especially suitable for data held in MPEG-2, MPEG-4 AVC/H.264 or
HEVC/H.265 form, as it allows the application to find the nearest
surrounding key frames, which greatly simplifies editing and improves
quality.

.. _sect_MM.2.5:

JPEG 2000 Part 2 Multi-Component Transform
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

Similar issues exist as for MPEG-2, MPEG-4 AVC/H.264 and HEVC/H.265 data
and similar solutions apply.

.. _sect_MM.2.6:

Functional Groups For Enhanced CT, MR, etc.
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

It is very important that functional groups for enhanced image objects
are properly re-created to reflect the reduced set of frames, as they
include important clinical information. The requirement in the Standard
that the resulting object be a valid SOP instance does make such
re-creations mandatory.

.. _sect_MM.2.7:

Nuclear Medicine Images
~~~~~~~~~~~~~~~~~~~~~~~

Images of the Nuclear Medicine SOP class are described by the Frame
Increment Pointer (0028,0009), which in turn references a number of
different "Vectors" as defined in Table "NM Multi-frame Module" in .
Like the Functional Groups above, these Vectors are required to contain
one value for each frame in the Image, and so their contents must be
modified to match the list of frames extracted, ensuring that the values
retained are those corresponding to the extracted frames.

.. _sect_MM.2.8:

A "Single Frame" Multi-frame Image
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

The requirement that the newly created image object generated in
response to a Frame level retrieve request must be the same as the SOP
class will frequently result in the need to create a single frame
instance of an object that is more commonly a multi-frame object, but
this should not cause any problems with the IOD rules, as all such
objects may quite legally have Number of Frames = 1.

However, a single frame may well cause problems for a transfer syntax
based on "video" such as those using MPEG-2, MPEG-4 AVC/H.264 or
HEVC/H.265, and therefore the SCU when negotiating a C-GET should
consider this problem, and include one or more transfer syntaxes
suitable for holding single or non-contiguous frames where such a
retrieval request is being made.

.. _sect_MM.3:

Frame Numbers
-------------

Frame numbers are indexes, not identifiers for frames. In every object,
the frame numbers always start at 1 and increment by 1, and therefore
they will not be the same after extraction into a new SOP Instance.

A SOP Instance may contain internal references to its own frames such as
mask frames. These may need to be corrected.

.. _sect_MM.4:

Consistency
-----------

There is no requirement in the Frame Level Retrieve Service for the SCP
to cache or otherwise retain any of the information it uses to create
the new SOP Instance, and therefore, an SCU submitting multiple requests
for the same information cannot expect to receive the "same" object with
the same Instance and Series UIDs each time. However, an SCP may choose
to cache such instances, and if returning an instance identical to one
previously created, then the same Instance and Series UIDs may be used.
The newly created object is however guaranteed to be a valid SOP
instance and an SCU may therefore choose to send such an instance to an
SCP using C-STORE, in which case it should be handled exactly as any
other Composite Instance of that SOP class.

.. _sect_MM.5:

Time Synchronization
--------------------

The time base for the new composite instance should be the same as for
the source image and should use the same time synchronization frame of
reference. This allows the object to retain synchronization to any
simultaneously acquired waveform data

.. _sect_MM.6:

Audio
-----

Where the original object is MPEG-2, MPEG-4 AVC/H.264 or HEVC/H.265 with
interleaved audio data in the MPEG-2 System, and where the retrieved
object is also MPEG-2, MPEG-4 AVC/H.264 or HEVC/H.265 encoded, then
audio could normally be preserved and maintain synchronization, but in
other cases, the audio may be lost.

.. _sect_MM.7:

Private Attributes
------------------

As with all modifications to existing SOP instances, an application
should remove any data that it cannot guarantee to make consistent with
the modifications it is making. Therefore, an application creating new
images from Multi-frame Images should remove any Private Attributes
about which it lacks sufficient information to allow safe and consistent
modification. This behavior should be documented in the conformance
statement.

