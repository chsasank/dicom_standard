.. _chapter_V:

Hanging Protocols (Informative)
===============================

The Hanging Protocol Composite IOD contains information about user
viewing preferences, related to image display station (workstation)
capabilities. The associated Service Classes support the storage
(C-STORE), query (C-FIND) and retrieve (C-MOVE and C-GET) of Hanging
Protocol Instances between servers and workstations. The goal is for
users to be able to conveniently define their preferred methods of
presentation and interaction for different types of viewing
circumstances once, and then to automatically layout image sets
according to the users' preferences on workstations of similar
capability.

The primary expectation is to facilitate the automatic and consistent
hanging of images according to definitions provided by the users, sites
or vendors of the workstations by providing the capability to:

-  Save defined Hanging Protocols

-  Search for Hanging Protocols by name, level (single user, user group,
   site, manufacturer), user identification code, modality, anatomy, and
   laterality.

-  Allow automatic hanging of image sets to occur for all studies on
   workstations with sufficiently compatible capabilities by matching
   against user or site defined Hanging Protocols. This includes
   supporting automatic hanging when the user reads from different
   locations, or on different but similar workstation types.

How relevant image sets (e.g., from the current and prior studies) are
obtained is not defined by the Hanging Protocol IOD or Service Classes.

Conformance with the DICOM Grayscale Standard Display Function and the
DICOM Softcopy Presentation States in conjunction with the Hanging
Protocol IOD allows the complete picture of what the users see, and how
they interact with it, to be defined, stored and reproduced as similarly
as possible, independent of workstation type. Further, it is anticipated
that implementers will make it easy for users to point to a graphical
representation of what they want (such as 4x1 versus 12x1 format with a
horizontal alternator scroll mechanism) and select it.

.. _sect_V.1:

Example Scenario
----------------

User A sits down at workstation X, with two 1024x1280 resolution screens
(`figure_title <#figure_V.1-1>`__) that recently has been installed and
hence has no user specific Hanging Protocols defined. The user brings up
the list of studies to be read and selects the first study, a chest CT,
together with the relevant prior studies. The workstation queries the
Hanging Protocol Query SCP for instances of the Hanging Protocol Storage
SOP Class. It finds none for this specific user, but matches a site
specific Hanging Protocol Instance, which was set up when the
workstation was installed at the site. It applies the site Hanging
Protocol Instance, and the user reads the current study in comparison to
the prior studies.

The user decides to customize the viewing style, and uses the viewing
application to define what type of Hanging Protocol is preferred (layout
style, interaction style) by pointing and clicking on graphical
representations of the choices. The user chooses a 3-column by 4-row
tiled presentation with a "vertical alternator" interaction, and a
default scroll amount of one row of images. The user places the current
study on the left screen, and the prior study on the right screen. The
user requests the application to save this Hanging Protocol, which
causes the new Hanging Protocol Instance to be stored to the Hanging
Protocol Storage SCP.

When the same user comes back the next day to read chest CT studies at
workstation X and a study is selected, the application queries the
Hanging Protocol Query SCP to determine which Hanging Protocol Instances
best match the scenario of this user on this workstation for this study.
The best match returned by the SCP in response to the query is with the
user ID matching his user ID, the study type matched to the study
type(s) of the image set selected for viewing, and the screen types
matching the workstation in use.

A list of matches is produced, with the Hanging Protocol Instance that
the user defined yesterday for chest CT matching the best, and the
current CT study is automatically displayed on the left screen with that
Hanging Protocol. Alternative next best matches are available to the
user via the application interface's pull-down menu list of all closely
matching Hanging Protocol Instances.

Because this Hanging Protocol defines an additional image set, the prior
year's chest CT study for the same patient is displayed next to the
current study, on the right screen.

The next week, the same user reads chest CTs at a different site in the
same enterprise on a similar type workstation, workstation Y, from a
different vendor. The workstation has a single 2048x2560 screen
(`figure_title <#figure_V.1-1>`__). This workstation queries the Hanging
Protocol Query SCP, and retrieves matching Hanging Protocol Instances,
choosing as the best match the Hanging Protocol Instance used on
workstation X before by user A. This Hanging Protocol is automatically
applied to display the chest CT study. The current chest CT study is
displayed on the left half of the 2048x2560 screen, and the prior chest
CT study is displayed on the right half of the screen, with 3 columns
and 8 rows each, maintaining the same vertical alternator layout. The
sequence of communications between the workstations and the SCP is
depicted in `figure_title <#figure_V.1-2>`__.

.. _sect_V.2:

Hanging Protocol Internal Process Model
---------------------------------------

The overall process flow of Hanging Protocols can be seen in
`figure_title <#figure_V.2-1>`__, and consists of three main steps:
selection, processing, and layout. The selection is defined in the . The
processing and layout are defined in the . The first process step, the
selection of sets of images that need to be available from DICOM image
objects, is defined by the Image Sets Sequence of the . This is a N:M
mapping, with multiple image sets potentially drawing from the same
image objects.

The second part of the process flow consists of the filtering,
reformatting, sorting, and presentation intent operations that map the
Image Sets into their final form, the Display Sets. This is defined in
the . This is a 1:M relationship, as multiple Display Sets may draw
their images from the same Image Set. The filtering operation allows for
selecting a subset of the Image Set and is defined by the Hanging
Protocol Display Module Filter Operations Sequence. Reformatting allows
operations such as multiplanar reformatting to resample images from a
volume (Reformatting Operation Type, Reformatting Thickness,
Reformatting Interval, Reformatting Operation Initial View Direction, 3D
Rendering Type). The Hanging Protocol Display Module Sorting Operations
Sequence allows for ordering of the images. Default presentation intent
(a subset of the Presentation State operations such as intensity window
default setting) is defined by the Hanging Protocol Display Module
presentation intent Attributes. The Display Sets are containers holding
the final sets of images after all operations have occurred. These sets
contain the images ready for rendering to locations on the screen(s).

The rendering of a Display Set to the screen is determined by the layout
information in the Image Boxes Sequence within a Display Sets Sequence
Item in the . A Display Set is mapped to a single Image Boxes Sequence.
This is generally a single Image Box (rectangular area on screen), but
may be an ordered set of image boxes. The mapping to an ordered set of
image boxes is a special case to allow the images to flow in an ordered
sequence through multiple locations on the screen (e.g., newspaper
columns). Display Environment Spatial Position specifies rectangular
locations on the screen where the images from the Display Sets will be
rendered. The type of interaction to be used is defined by the Image
Boxes Sequence Item Attributes. A vertically scrolling alternator could
be specified by having Image Box Layout Type equal TILED and Image Box
Scroll Direction equal VERTICAL.

An example of this processing is shown in
`figure_title <#figure_V.2-2>`__. The figure is based on the
Neurosurgery Planning Hanging Protocol Example contained in this Annex,
and corresponds to the display sets for Display Set Presentation Group
#1 (CT only display of current CT study).

.. _sect_V.3:

Chest X-Ray Hanging Protocol Example
------------------------------------

Goal: A Hanging Protocol for Chest X-ray, PA & Lateral (LL, RL) views,
current & prior, with the following layout:

The Hanging Protocol Definition does not specify a specific modality,
but rather a specific anatomy (Chest). The Image Sets Sequence provides
more detail, in that it specifies the modalities in addition to the
anatomy for each image set.

.. _sect_V.3.1:

Hanging Protocol Definition Module
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

-  Hanging Protocol Name: "Chest X-ray"

-  Hanging Protocol Description: "Current and Prior Chest PA and
   Lateral"

-  Hanging Protocol Level: "SITE"

-  Hanging Protocol Creator: "Senior Radiologist"

-  Hanging Protocol Creation DateTime: "20020823133455"

-  Hanging Protocol Definition Sequence:

   -  Item 1:

   -  Anatomic Region Sequence:

      -  Item 1: `(51185008, SCT,
         "Chest") <http://snomed.info/id/51185008>`__

   -  Laterality: *zero length*

   -  Procedure Code Sequence: *zero length*

   -  Reason for Requested Procedure Code Sequence: *zero length*

-  Number of Priors Referenced: 1

-  Image Sets Sequence:

   -  Item 1:

      -  Image Set Selector Sequence:

         -  Item 1:

            -  Image Set Selector Usage Flag: "NO_MATCH"

            -  Selector Attribute: (0008,2218) [Anatomic Region
               Sequence]

            -  Selector Attribute VR: "SQ"

            -  Selector Code Sequence Value:

               -  Item 1: `(51185008, SCT,
                  "Chest") <http://snomed.info/id/51185008>`__

            -  Selector Value Number: 1

         -  Item 2:

            -  Image Set Selector Usage Flag: "NO_MATCH"

            -  Selector Attribute: (0008,0060) [Modality]

            -  Selector Attribute VR: "CS"

            -  Selector CS Value: "CR\DX"

            -  Selector Value Number: 1

   -  Time Based Image Sets Sequence:

      -  Item 1:

         -  Image Set Number: 1

         -  Image Set Selector Category: "RELATIVE_TIME"

         -  Relative Time: 0\0

         -  Relative Time Units: "MINUTES"

         -  Image Set Label: "Current Chest X-ray"

      -  Item 2:

         -  Image Set Number: 2

         -  Image Set Selector Category: "ABSTRACT_PRIOR"

         -  Abstract Prior Value: 1\1

         -  Image Set Label: "Prior Chest X-ray"

-  Hanging Protocol User Identification Code Sequence: *zero length*

-  Hanging Protocol User Group Name: "ABC Hospital"

.. _sect_V.3.2:

Hanging Protocol Environment Module
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

-  Number of Screens: 2

-  Nominal Screen Definition Sequence:

   -  Item 1:

      -  Number of Vertical Pixels: 2560

      -  Number of Horizontal Pixels: 2048

      -  Display Environment Spatial Position: 0.0\1.0\0.5\0.0,
         representing (0,1), (0.5,0)

      -  Screen Minimum Grayscale Bit Depth: 8

      -  Application Maximum Repaint Time: 100

   -  Item 2:

      -  Number of Vertical Pixels: 2560

      -  Number of Horizontal Pixels: 2048

      -  Display Environment Spatial Position: 0.5\1.0\1.0\0.0,
         representing (0.5,1), (1,0)

      -  Screen Minimum Grayscale Bit Depth: 8

      -  Application Maximum Repaint Time: 100

.. _sect_V.3.3:

Hanging Protocol Display Module
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

-  Display Sets Sequence:

   -  Item 1:

      -  Display Set Number: 1

      -  Display Set Presentation Group: 1

      -  Image Set Number: 2

      -  Image Boxes Sequence:

         -  Item 1:

            -  Image Box Number: 1

            -  Display Environment Spatial Position: 0.0\1.0\0.25\0.0,
               representing (0,1), (0.25,0)

            -  Image Box Layout Type: "SINGLE"

      -  Filter Operations Sequence:

         -  o Item 1:

            -  Selector Attribute: (0018,5101) [View Position]

            -  Selector Attribute VR: "CS"

            -  Selector CS Value: "RL\LL"

            -  Selector Value Number: 1

            -  Filter-by Operator: "MEMBER_OF"

      -  Sorting Operations Sequence: *zero length*

      -  Display Set Patient Orientation: "A\F"

      -  Show Image True Size Flag: "NO"

      -  Show Graphic Annotation Flag: "NO"

   -  Item 2:

      -  Display Set Number: 2

      -  Display Set Presentation Group: 1

      -  Image Set Number: 2

      -  Image Boxes Sequence:

         -  Item 1:

            -  Image Box Number: 1

            -  Display Environment Spatial Position: 0.25\1.0\0.5\0.0,
               representing (0.25,1), (0.5,0)

            -  Image Box Layout Type: "SINGLE"

      -  Filter Operations Sequence:

         -  Item 1:

            -  Selector Attribute: (0018,5101) [View Position]

            -  Selector Attribute VR: "CS"

            -  Selector CS Value: "PA"

            -  Selector Value Number: 1

            -  Filter-by Operator: "MEMBER_OF"

      -  Sorting Operations Sequence: *zero length*

      -  Display Set Patient Orientation: "R\F"

      -  Show Image True Size Flag: "NO"

      -  Show Graphic Annotation Flag: "NO"

   -  Item 3:

      -  Display Set Number: 3

      -  Display Set Presentation Group: 1

      -  Image Set Number: 1

      -  Image Boxes Sequence:

         -  Item 1:

            -  Image Box Number: 1

            -  Display Environment Spatial Position: 0.5\1.0\0.75\1.0,
               representing (0.5,1), (0.75,0)

            -  Image Box Layout Type: "SINGLE"

      -  Filter Operations Sequence:

         -  Item 1:

            -  Selector Attribute: (0018,5101) [View Position]

            -  Selector Attribute VR: "CS"

            -  Selector CS Value: "PA"

            -  Selector Value Number: 1

            -  Filter-by Operator: "MEMBER_OF"

      -  Sorting Operations Sequence: *zero length*

      -  Display Set Patient Orientation: "R\F"

      -  Show Image True Size Flag: "NO"

      -  Show Graphic Annotation Flag: "NO"

   -  Item 4:

      -  Display Set Number: 4

      -  Display Set Presentation Group: 1

      -  Image Set Number: 1

      -  Image Boxes Sequence:

         -  Item 1:

            -  Image Box Number: 1

            -  Display Environment Spatial Position: 0.75\1.0\1.0\0.0,
               representing (0.75,1), (1,0)

            -  Image Box Layout Type: "SINGLE"

      -  Filter Operations Sequence:

         -  Item 1:

            -  Selector Attribute: (0018,5101) [View Position]

            -  Selector Attribute VR: "CS"

            -  Selector CS Value: "RL\LL"

            -  Selector Value Number: 1

            -  Filter-by Operator: "MEMBER_OF"

      -  Sorting Operations Sequence: *zero length*

      -  Display Set Patient Orientation: "A\F"

      -  Show Image True Size Flag: "NO"

      -  Show Graphic Annotation Flag: "NO"

-  Partial Data Display Handling: "MAINTAIN_LAYOUT"

.. _sect_V.4:

Neurosurgery Planning Hanging Protocol Example
----------------------------------------------

Goal: A Hanging Protocol for MR & CT of Head, for a neurosurgery plan.
1Kx1K screen on left shows orthogonal MPR slices through the acquisition
volume, and in one presentation group has a 3D interactive volume
rendering in the lower right quadrant. In all display sets the 1Kx1K
screen is split into 4 512x512 quadrants. The 2560x2048 screen has a 4
row by 3 column tiled display area. There are 4 temporal presentation
groups: CT\ :sub:`new`, MR, combined CT\ :sub:`new` and MR, combined
CT\ :sub:`new` and CT\ :sub:`old`.

Display Environment Spatial Position Attribute values for image boxes
are represented in terms of ratios in pixel space [(0/3072, 512/2560),
(512/3072,0/2560)] rather than (0.0,0.0), (1.0,1.0) space, for ease of
understanding the example.

.. _sect_V.4.1:

Hanging Protocol Definition Module
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

-  Hanging Protocol Name: "NeurosurgeryPlan"

-  Hanging Protocol Description: "Neurosurgery planning, requiring MR
   and CT of head"

-  Hanging Protocol Level: "SITE"

-  Hanging Protocol Creator: "Smith^Joseph"

-  Hanging Protocol Creation DateTime: "20020101104200"

-  Hanging Protocol Definition Sequence:

   -  Item 1:

      -  Modality: "MR"

      -  Anatomic Region Sequence:

         -  Item 1: `(69536005, SCT,
            "Head") <http://snomed.info/id/69536005>`__

      -  Laterality: *zero length*

      -  Procedure Code Sequence:

         -  Item 1: (98765, 99Local, 1.5, "NeuroSurgery Plan Local5")

      -  Reason for Requested Procedure Code Sequence:

         -  Item 1: (I67.1, I10, "Cerebral aneurysm")

   -  Item 2:

      -  Modality: "CT"

      -  Anatomic Region Sequence:

         -  Item 1: `(69536005, SCT,
            "Head") <http://snomed.info/id/69536005>`__

      -  Laterality: *zero length*

      -  Procedure Code Sequence:

         -  Item 1: (98765, 99Local, 1.5, "NeuroSurgery Plan Local5")

      -  Reason for Requested Procedure Code Sequence:

         -  Item 1: (I67.1, I10, "Cerebral aneurysm")

-  Number of Priors Referenced: 1

-  Image Sets Sequence:

   -  Item 1:

      -  Image Set Selector Sequence:

         -  o Item 1:

            -  Image Set Selector Usage Flag: "NO_MATCH"

            -  Selector Attribute: (0018,0015) [Body Part Examined]

            -  Selector Attribute VR: "CS"

            -  Selector CS Value: "HEAD"

            -  Selector Value Number: 1

         -  Item 2:

            -  Image Set Selector Usage Flag: "NO_MATCH"

            -  Selector Attribute: (0008,0060) [Modality]

            -  Selector Attribute VR: "CS"

            -  Selector CS Value: "MR"

            -  Selector Value Number: 1

      -  Time Based Image Sets Sequence:

         -  o Item 1:

            -  Image Set Number: 1

            -  Image Set Selector Category: "RELATIVE_TIME"

            -  Relative Time: 0\0

            -  Relative Time Units: "MINUTES"

            -  Image Set Label: "Current MR Head"

   -  Item 2:

      -  Image Set Selector Sequence:

         -  Item 1:

            -  Image Set Selector Usage Flag: "NO_MATCH"

            -  Selector Attribute: (0018,0015) [Body Part Examined]

            -  Selector Attribute VR: "CS"

            -  Selector CS Value: "HEAD"

            -  Selector Value Number: 1

         -  o Item 2:

            -  Image Set Selector Usage Flag: "NO_MATCH"

            -  Selector Attribute: (0008,0060) [Modality]

            -  Selector Attribute VR: "CS"

            -  Selector CS Value: "CT"

            -  Selector Value Number: 1

      -  Time Based Image Sets Sequence:

         -  Item 1:

            -  Image Set Number: 2

            -  Image Set Selector Category: "RELATIVE_TIME"

            -  Relative Time: 0\0

            -  Relative Time Units: "MINUTES"

            -  Image Set Label: "Current CT Head"

         -  Item 2:

            -  Image Set Number: 3

            -  Image Set Selector Category: "ABSTRACT_PRIOR"

            -  Abstract Prior Value: 1\1

            -  Image Set Label: "Prior CT Head"

-  Hanging Protocol User Identification Code Sequence: *zero length*

-  Hanging Protocol User Group Name: "ABC Hospital"

.. _sect_V.4.2:

Hanging Protocol Environment Module
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

-  Number of Screens: 2

-  Nominal Screen Definition Sequence:

   -  Item 1:

      -  Number of Vertical Pixels: 1024

      -  Number of Horizontal Pixels: 1024

      -  Display Environment Spatial Position: 0.0\0.28\0.33\0.0,
         representing (0.0, 0.28), (0.33, 0.0)

      -  Screen Minimum Color Bit Depth: 8

      -  Application Maximum Repaint Time: 70

   -  Item 2:

      -  Number of Vertical Pixels: 2560

      -  Number of Horizontal Pixels: 2048

      -  Display Environment Spatial Position 0.33\1.0\1.0\0.0,
         representing (0.33, 1.0), (1.0, 0.0)

      -  Screen Minimum Grayscale Bit Depth: 8

      -  Application Maximum Repaint Time: 10

.. _sect_V.4.3:

Hanging Protocol Display Module
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

-  Display Sets Sequence:

   -  

   -  Item 1:

      -  Display Set Number: 1

      -  Display Set Presentation Group: 1

      -  Image Set Number: 2

      -  Image Boxes Sequence:

         -  Item 1: [lower left quadrant of 1024x1024]

            -  Image Box Number: 1

            -  Display Environment Spatial Position: (0/3072, 512/2560),
               (512/3072,0/2560)

            -  Image Box Layout Type: "STACK"

      -  Filter Operations Sequence:

         -  Item 1:

            -  Filter-by Category: "IMAGE_PLANE"

            -  Selector Attribute VR: "CS"

            -  Selector CS Value: "TRANSVERSE"

            -  Filter-by Operator: "MEMBER_OF"

      -  Sorting Operations Sequence:

         -  Item 1:

            -  Sort-by Category: "ALONG_AXIS"

            -  Sorting Direction: "INCREASING"

      -  Reformatting Operation Type: "MPR"

      -  Reformatting Thickness: 5

      -  Reformatting Interval: 5

      -  Reformatting Operation Initial View Direction: "CORONAL"

      -  Display Set Patient Orientation: "L\F"

      -  VOI Type: BRAIN

      -  Display Set Presentation Group Description: "Current CT only"

   -  Item 2:

      -  Display Set Number: 2

      -  Display Set Presentation Group: 1

      -  Image Set Number: 2

      -  Image Boxes Sequence:

         -  Item 1: [upper left quadrant of 1024x1024]

            -  Image Box Number: 1

            -  Display Environment Spatial Position: (0/3072,
               1024/2560), (512/3072, 512/2560)

            -  Image Box Layout Type: "STACK"

      -  Filter Operations Sequence:

         -  Item 1:

            -  Filter-by Category: "IMAGE_PLANE"

            -  Selector Attribute VR: "CS"

            -  Selector CS Value: "TRANSVERSE"

            -  Filter-by Operator: "MEMBER_OF"

      -  Sorting Operations Sequence:

         -  Item 1:

            -  Sort-by Category: "ALONG_AXIS"

            -  Sorting Direction: "INCREASING"

      -  Reformatting Operation Type: "MPR"

      -  Reformatting Thickness: 5

      -  Reformatting Interval: 5

      -  Reformatting Operation Initial View Direction: "SAGITTAL"

      -  Display Set Patient Orientation: "P\F"

      -  VOI Type: BRAIN

   -  Item 3:

      -  Display Set Number: 3

      -  Display Set Presentation Group: 1

      -  Image Set Number: 2

      -  Image Boxes Sequence:

         -  Item 1: [upper right quadrant of 1024x1024]

            -  Image Box Number: 1

            -  Display Environment Spatial Position: (512/3072,
               1024/2560), (1024/3072, 512/2560)

            -  Image Box Layout Type: "STACK"

      -  Filter Operations Sequence:

         -  Item 1:

            -  Filter-by Category: "IMAGE_PLANE"

            -  Selector Attribute VR: "CS"

            -  Selector CS Value: "TRANSVERSE"

            -  Filter-by Operator: "MEMBER_OF"

      -  Sorting Operations Sequence:

         -  Item 1:

            -  Sort-by Category: "ALONG_AXIS"

            -  Sorting Direction: "INCREASING"

      -  Display Set Patient Orientation: "L\P"

      -  VOI Type: BRAIN

      -  Show Graphic Annotation Flag: "YES"

   -  Item 4:

      -  Display Set Number: 4

      -  Display Set Presentation Group: 1

      -  Image Set Number: 2

      -  Image Boxes Sequence:

         -  Item 1: [lower right quadrant of 1024x1024]

            -  Image Box Number: 1

            -  Display Environment Spatial Position: (512/3072,
               512/2560), (1024/3072, 0/2560)

            -  Image Box Layout Type: "PROCESSED"

      -  Filter Operations Sequence:

         -  Item 1:

            -  Selector Attribute: (0008,0008) [Image Type]

            -  Selector Attribute VR: "CS"

            -  Selector CS Value: "LOCALIZER "

            -  Selector Value Number: 3

            -  Filter-by Operator: "NOT_MEMBER_OF"

      -  Sorting Operations Sequence: *zero length*

      -  Reformatting Operation Type: "3D_RENDERING"

      -  Reformatting Operation Initial View Direction: "CORONAL"

      -  3D Rendering Type: "VOLUME"

      -  Display Set Patient Orientation: "X\F"

      -  Show Graphic Annotation Flag: "NO"

   -  Item 5:

      -  Display Set Number: 5

      -  Display Set Presentation Group: 1

      -  Image Set Number: 2

      -  Image Boxes Sequence:

         -  Item 1: [entire 2048x2560 space]

            -  Image Box Number: 1

            -  Display Environment Spatial Position: (1024/3072,
               2560/2560), (3072/3072, 0/2560)

            -  Image Box Layout Type: "TILED"

            -  Image Box Tile Horizontal Dimension: 3

            -  Image Box Tile Vertical Dimension: 4

            -  Image Box Scroll Direction: "VERTICAL"

            -  Image Box Small Scroll Type: "ROW_COLUMN"

            -  Image Box Small Scroll Amount: 1

            -  Image Box Large Scroll Type: "PAGE"

            -  Image Box Large Scroll Amount: 1

      -  Filter Operations Sequence:

         -  Item 1:

            -  Filter-by Category: "IMAGE_PLANE"

            -  Selector Attribute VR: "CS"

            -  Selector CS Value: "TRANSVERSE"

            -  Filter-by Operator: "MEMBER_OF"

      -  Sorting Operations Sequence:

         -  Item 1:

            -  Sort-by Category: "ALONG_AXIS"

            -  Sorting Direction: "INCREASING"

      -  Display Set Patient Orientation: "L\P"

      -  VOI Type: BRAIN

      -  Show Graphic Annotation Flag: "YES"

   -  

   -  Item 6:

      -  Display Set Number: 6

      -  Display Set Presentation Group: 2

      -  Image Set Number: 1

      -  Image Boxes Sequence:

         -  Item 1: [lower left quadrant of 1024x1024]

            -  Image Box Number: 1

            -  Display Environment Spatial Position: (0/3072, 512/2560),
               (512/3072,0/2560)

            -  Image Box Layout Type: "STACK"

      -  Filter Operations Sequence:

         -  Item 1:

            -  Filter-by Category: "IMAGE_PLANE"

            -  Selector Attribute VR: "CS"

            -  Selector CS Value: "TRANSVERSE"

            -  Filter-by Operator: "MEMBER_OF"

      -  Sorting Operations Sequence:

         -  Item 1:

            -  Sort-by Category: "ALONG_AXIS"

            -  Sorting Direction: "INCREASING"

      -  Reformatting Operation Type: "MPR"

      -  Reformatting Thickness: 5

      -  Reformatting Interval: 5

      -  Reformatting Operation Initial View Direction: "CORONAL"

      -  Display Set Patient Orientation: "P\F"

      -  Display Set Presentation Group Description: "MR only"

   -  Item 7:

      -  Display Set Number: 7

      -  Display Set Presentation Group: 2

      -  Image Set Number: 1

      -  Image Boxes Sequence:

         -  Item 1: [upper left quadrant of 1024x1024]

            -  Image Box Number: 1

            -  Display Environment Spatial Position: (0/3072,
               1024/2560), (512/3072, 512/2560)

            -  Image Box Layout Type: "STACK"

      -  Filter Operations Sequence:

         -  Item 1:

            -  Filter-by Category: "IMAGE_PLANE"

            -  Selector Attribute VR: "CS"

            -  Selector CS Value: "TRANSVERSE"

            -  Filter-by Operator: "MEMBER_OF"

      -  Sorting Operations Sequence:

         -  Item 1:

            -  Sort-by Category: "ALONG_AXIS"

            -  Sorting Direction: "INCREASING"

      -  Reformatting Operation Type: "MPR"

      -  Reformatting Thickness: 5

      -  Reformatting Interval: 5

      -  Reformatting Operation Initial View Direction: "SAGITTAL"

      -  Display Set Patient Orientation: "P\F"

   -  Item 8:

      -  Display Set Number: 8

      -  Display Set Presentation Group: 2

      -  Image Set Number: 1

      -  Image Boxes Sequence:

         -  Item 1: [upper right quadrant of 1024x1024]

            -  Image Box Number: 1

            -  Display Environment Spatial Position: (512/3072,
               1024/2560), (1024/3072, 512/2560)

            -  Image Box Layout Type: "STACK"

      -  Filter Operations Sequence:

         -  Item 1:

            -  Filter-by Category: "IMAGE_PLANE"

            -  Selector Attribute VR: "CS"

            -  Selector CS Value: "TRANSVERSE"

            -  Filter-by Operator: "MEMBER_OF"

      -  Sorting Operations Sequence:

         -  Item 1:

            -  Sort-by Category: "ALONG_AXIS"

            -  Sorting Direction: "INCREASING"

      -  Display Set Patient Orientation: "L\P"

   -  Item 9:

      -  Display Set Number: 9

      -  Display Set Presentation Group: 2

      -  Image Set Number: 1

      -  Image Boxes Sequence:

         -  Item 1: [lower right quadrant of 1024x1024]

            -  Image Box Number: 1

            -  Display Environment Spatial Position: (512/3072,
               512/2560), (1024/3072, 0/2560)

            -  Image Box Layout Type: "PROCESSED"

      -  Filter Operations Sequence: *zero length*

      -  Sorting Operations Sequence: *zero length*

      -  Reformatting Operation Type: "3D_RENDERING"

      -  Reformatting Operation Initial View Direction: "CORONAL"

      -  3D Rendering Type: "VOLUME"

      -  Display Set Patient Orientation: "X\F"

   -  Item 10:

      -  Display Set Number: 10

      -  Display Set Presentation Group: 2

      -  Image Set Number: 1

      -  Image Boxes Sequence:

         -  Item 1: [entire 2048x2560 space]

            -  Image Box Number: 1

            -  Display Environment Spatial Position: (1024/3072,
               2560/2560), (3072/3072, 0/2560)

            -  Image Box Layout Type: "TILED"

            -  Image Box Tile Horizontal Dimension: 3

            -  Image Box Tile Vertical Dimension: 4

            -  Image Box Scroll Direction: "VERTICAL"

            -  Image Box Small Scroll Type: "ROW_COLUMN"

            -  Image Box Small Scroll Amount: 1

            -  Image Box Large Scroll Type: "PAGE"

            -  Image Box Large Scroll Amount: 1

      -  Filter Operations Sequence:

         -  Item 1:

            -  Filter-by Category: "IMAGE_PLANE"

            -  Selector Attribute VR: "CS"

            -  Selector CS Value: "TRANSVERSE"

            -  Filter-by Operator: "MEMBER_OF"

      -  Sorting Operations Sequence:

         -  Item 1:

            -  Sort-by Category: "ALONG_AXIS"

            -  Sorting Direction: "INCREASING"

      -  Display Set Patient Orientation: "L\P"

   -  

   -  Item 11: [MR coronal]

      -  Display Set Number: 11

      -  Display Set Presentation Group: 3

      -  Image Set Number: 1

      -  Image Boxes Sequence:

         -  Item 1: [lower left quadrant of 1024x1024]

            -  Image Box Number: 1

            -  Display Environment Spatial Position: (0/3072, 512/2560),
               (512/3072,0/2560)

            -  Image Box Layout Type: "STACK"

      -  Filter Operations Sequence:

         -  Item 1:

            -  Filter-by Category: "IMAGE_PLANE"

            -  Selector Attribute VR: "CS"

            -  Selector CS Value: "TRANSVERSE"

            -  Filter-by Operator: "MEMBER_OF"

      -  Sorting Operations Sequence:

         -  Item 1:

            -  Sort-by Category: "ALONG_AXIS"

            -  Sorting Direction: "INCREASING"

      -  Reformatting Operation Type: "MPR"

      -  Reformatting Thickness: 5

      -  Reformatting Interval: 5

      -  Reformatting Operation Initial View Direction: "CORONAL"

      -  Display Set Patient Orientation: "L\F"

      -  Show Graphic Annotation Flag: "NO"

      -  Display Set Presentation Group Description: "MR & CT combined"

   -  Item 12: [CT coronal]

      -  Display Set Number: 12

      -  Display Set Presentation Group: 3

      -  Image Set Number: 2

      -  Image Boxes Sequence:

         -  Item 1: [upper left quadrant of 1024x1024]

            -  Image Box Number: 1

            -  Display Environment Spatial Position: (0/3072,
               1024/2560), (512/3072, 512/2560)

            -  Image Box Layout Type: "STACK"

      -  Filter Operations Sequence:

         -  Item 1:

            -  Filter-by Category: "IMAGE_PLANE"

            -  Selector Attribute VR: "CS"

            -  Selector CS Value: "TRANSVERSE"

            -  Filter-by Operator: "MEMBER_OF"

      -  Sorting Operations Sequence:

         -  Item 1:

            -  Sort-by Category: "ALONG_AXIS"

            -  Sorting Direction: "INCREASING"

      -  Reformatting Operation Type: "MPR"

      -  Reformatting Thickness: 5

      -  Reformatting Interval: 5

      -  Reformatting Operation Initial View Direction: "CORONAL"

      -  Display Set Patient Orientation: "L\F"

      -  VOI Type: BRAIN

      -  Show Graphic Annotation Flag: "NO"

   -  Item 13: [CT transverse]

      -  Display Set Number: 13

      -  Display Set Presentation Group: 3

      -  Image Set Number: 2

      -  Image Boxes Sequence:

         -  Item 1: [upper right quadrant of 1024x1024]

            -  Image Box Number: 1

            -  Display Environment Spatial Position: (512/3072,
               1024/2560), (1024/3072, 512/2560)

            -  Image Box Layout Type: "STACK"

      -  Filter Operations Sequence:

         -  Item 1:

            -  Filter-by Category: "IMAGE_PLANE"

            -  Selector Attribute VR: "CS"

            -  Selector CS Value: "TRANSVERSE"

            -  Filter-by Operator: "MEMBER_OF"

      -  Sorting Operations Sequence:

         -  Item 1:

            -  Sort-by Category: "ALONG_AXIS"

            -  Sorting Direction: "INCREASING"

      -  Display Set Patient Orientation: "L\P"

      -  VOI Type: BRAIN

      -  Show Graphic Annotation Flag: "YES"

   -  Item 14: [MR transverse]

      -  Display Set Number: 14

      -  Display Set Presentation Group: 3

      -  Image Set Number: 1

      -  Image Boxes Sequence:

         -  Item 1: [lower right quadrant of 1024x1024]

            -  Image Box Number: 1

            -  Display Environment Spatial Position: (512/3072,
               512/2560), (1024/3072, 0/2560)

            -  Image Box Layout Type: "STACK"

      -  Filter Operations Sequence:

         -  Item 1:

            -  Filter-by Category: "IMAGE_PLANE"

            -  Selector Attribute VR: "CS"

            -  Selector CS Value: "TRANSVERSE"

            -  Filter-by Operator: "MEMBER_OF"

      -  Sorting Operations Sequence:

         -  Item 1:

            -  Sort-by Category: "ALONG_AXIS"

            -  Sorting Direction: "INCREASING"

      -  Display Set Patient Orientation: "L\P"

      -  Show Graphic Annotation Flag: "NO"

   -  Item 15: [CT two part scrolled, rows 1 & 3]

      -  Display Set Number: 15

      -  Display Set Presentation Group: 3

      -  Image Set Number: 2

      -  Image Boxes Sequence:

         -  Item 1: [row 1 (top row) of 2048x2560 space]

            -  Image Box Number: 1

            -  Display Environment Spatial Position: (1024/3072,
               2048/2560), (3072/3072, 1536/2560)

            -  Image Box Layout Type: "TILED"

            -  Image Box Tile Horizontal Dimension: 3

            -  Image Box Tile Vertical Dimension: 1

            -  Image Box Scroll Direction: "HORIZONTAL"

            -  Image Box Small Scroll Type: "IMAGE"

            -  Image Box Small Scroll Amount: 1

            -  Image Box Large Scroll Type: "ROW_COLUMN"

            -  Image Box Large Scroll Amount: 1

         -  Item 2: [row 3 of 2048x2560 space]

            -  Image Box Number: 2

            -  Display Environment Spatial Position: (1024/3072,
               1024/2560), (3072/3072, 512/2560)

            -  Image Box Layout Type: "TILED"

            -  Image Box Tile Horizontal Dimension: 3

            -  Image Box Tile Vertical Dimension: 1

            -  Image Box Scroll Direction: "HORIZONTAL"

            -  Image Box Small Scroll Type: "IMAGE"

            -  Image Box Small Scroll Amount: 1

            -  Image Box Large Scroll Type: "ROW_COLUMN"

            -  Image Box Large Scroll Amount: 1

      -  Filter Operations Sequence:

         -  Item 1:

            -  Filter-by Category: "IMAGE_PLANE"

            -  Selector Attribute VR: "CS"

            -  Selector CS Value: "TRANSVERSE"

            -  Filter-by Operator: "MEMBER_OF"

      -  Sorting Operations Sequence:

         -  Item 1:

            -  Sort-by Category: "ALONG_AXIS"

            -  Sorting Direction: "INCREASING"

      -  Display Set Patient Orientation: "L\P"

      -  VOI Type: BRAIN

      -  Show Graphic Annotation Flag: "YES"

   -  Item 16: [MR two part scrolled, rows 2 & 4]

      -  Display Set Number: 16

      -  Display Set Presentation Group: 3

      -  Image Set Number: 1

      -  Image Boxes Sequence:

         -  Item 1: [row 2 of 2048x2560 space]

            -  Image Box Number: 1

            -  Display Environment Spatial Position: (1024/3072,
               1536/2560), (3072/3072, 1024/2560)

            -  Image Box Layout Type: "TILED"

            -  Image Box Tile Horizontal Dimension: 3

            -  Image Box Tile Vertical Dimension: 1

            -  Image Box Scroll Direction: "HORIZONTAL"

            -  Image Box Small Scroll Type: "IMAGE"

            -  Image Box Small Scroll Amount: 1

            -  Image Box Large Scroll Type: "ROW_COLUMN"

            -  Image Box Large Scroll Amount: 1

         -  Item 2: [row 4 (bottom row) of 2048x2560 space]

            -  Image Box Number: 2

            -  Display Environment Spatial Position: (1024/3072,
               512/2560), (3072/3072, 0/2560)

            -  Image Box Layout Type: "TILED"

            -  Image Box Tile Horizontal Dimension: 3

            -  Image Box Tile Vertical Dimension: 1

            -  Image Box Scroll Direction: "HORIZONTAL"

            -  Image Box Small Scroll Type: "IMAGE"

            -  Image Box Small Scroll Amount: 1

            -  Image Box Large Scroll Type: "ROW_COLUMN"

            -  Image Box Large Scroll Amount: 1

      -  Filter Operations Sequence:

         -  Item 1:

            -  Filter-by Category: "IMAGE_PLANE"

            -  Selector Attribute VR: "CS"

            -  Selector CS Value: "TRANSVERSE"

            -  Filter-by Operator: "MEMBER_OF"

      -  Sorting Operations Sequence:

         -  Item 1:

            -  Sort-by Category: "ALONG_AXIS"

            -  Sorting Direction: "INCREASING"

      -  Display Set Patient Orientation: "L\P"

      -  Show Graphic Annotation Flag: "NO"

   -  

   -  Item 17: [CT old coronal]

      -  Display Set Number: 17

      -  Display Set Presentation Group: 4

      -  Image Set Number: 3

      -  Image Boxes Sequence:

         -  Item 1: [lower left quadrant of 1024x1024]

            -  Image Box Number: 1

            -  Display Environment Spatial Position: (0/3072, 512/2560),
               (512/3072,0/2560)

            -  Image Box Layout Type: "STACK"

      -  Filter Operations Sequence:

         -  Item 1:

            -  Filter-by Category: "IMAGE_PLANE"

            -  Selector Attribute VR: "CS"

            -  Selector CS Value: "TRANSVERSE"

            -  Filter-by Operator: "MEMBER_OF"

      -  Sorting Operations Sequence:

         -  Item 1:

            -  Sort-by Category: "ALONG_AXIS"

            -  Sorting Direction: "INCREASING"

      -  Reformatting Operation Type: "MPR"

      -  Reformatting Thickness: 5

      -  Reformatting Interval: 5

      -  Reformatting Operation Initial View Direction: "CORONAL"

      -  Display Set Patient Orientation: "L\F"

      -  VOI Type: BRAIN

      -  Display Set Presentation Group Description: "CT old & CT new
         combined"

   -  Item 18: [CT new coronal]

      -  Display Set Number: 18

      -  Display Set Presentation Group: 4

      -  Image Set Number: 2

      -  Image Boxes Sequence:

         -  Item 1: [upper left quadrant of 1024x1024]

            -  Image Box Number: 1

            -  Display Environment Spatial Position: (0/3072,
               1024/2560), (512/3072, 512/2560)

            -  Image Box Layout Type: "STACK"

      -  Filter Operations Sequence:

         -  Item 1:

            -  Filter-by Category: "IMAGE_PLANE"

            -  Selector Attribute VR: "CS"

            -  Selector CS Value: "TRANSVERSE"

            -  Filter-by Operator: "MEMBER_OF"

      -  Sorting Operations Sequence:

         -  Item 1:

            -  Sort-by Category: "ALONG_AXIS"

            -  Sorting Direction: "INCREASING"

      -  Reformatting Operation Type: "MPR"

      -  Reformatting Thickness: 5

      -  Reformatting Interval: 5

      -  Reformatting Operation Initial View Direction: "CORONAL"

      -  Display Set Patient Orientation: "L\F"

      -  VOI Type: BRAIN

   -  Item 19: [CT new transverse]

      -  Display Set Number: 19

      -  Display Set Presentation Group: 4

      -  Image Set Number: 2

      -  Image Boxes Sequence:

         -  Item 1: [upper right quadrant of 1024x1024]

            -  Image Box Number: 1

            -  Display Environment Spatial Position: (512/3072,
               1024/2560), (1024/3072, 512/2560)

            -  Image Box Layout Type: "STACK"

      -  Filter Operations Sequence:

         -  Item 1:

            -  Filter-by Category: "IMAGE_PLANE"

            -  Selector Attribute VR: "CS"

            -  Selector CS Value: "TRANSVERSE"

            -  Filter-by Operator: "MEMBER_OF"

      -  Sorting Operations Sequence:

         -  Item 1:

            -  Sort-by Category: "ALONG_AXIS"

            -  Sorting Direction: "INCREASING"

      -  Display Set Patient Orientation: "L\P"

      -  VOI Type: BRAIN

      -  Show Graphic Annotation Flag: "YES"

   -  Item 20: [CT old transverse]

      -  Display Set Number: 20

      -  Display Set Presentation Group: 4

      -  Image Set Number: 3

      -  Image Boxes Sequence:

         -  Item 1: [lower right quadrant of 1024x1024]

            -  Image Box Number: 1

            -  Display Environment Spatial Position: (512/3072,
               512/2560), (1024/3072, 0/2560)

            -  Image Box Layout Type: "STACK"

      -  Filter Operations Sequence:

         -  Item 1:

            -  Filter-by Category: "IMAGE_PLANE"

            -  Selector Attribute VR: "CS"

            -  Selector CS Value: "TRANSVERSE"

            -  Filter-by Operator: "MEMBER_OF"

      -  Sorting Operations Sequence:

         -  Item 1:

            -  Sort-by Category: "ALONG_AXIS"

            -  Sorting Direction: "INCREASING"

      -  Display Set Patient Orientation: "L\P"

      -  VOI Type: BRAIN

      -  Show Graphic Annotation Flag: "YES"

   -  Item 21: [CT new two part scrolled, rows 1 & 3]

      -  Display Set Number: 21

      -  Display Set Presentation Group: 4

      -  Image Set Number: 2

      -  Image Boxes Sequence:

         -  Item 1: [row 1 (top row) of 2048x2560 space]

            -  Image Box Number: 1

            -  Display Environment Spatial Position: (1024/3072,
               2048/2560), (3072/3072, 1536/2560)

            -  Image Box Layout Type: "TILED"

            -  Image Box Tile Horizontal Dimension: 3

            -  Image Box Tile Vertical Dimension: 1

            -  Image Box Scroll Direction: "HORIZONTAL"

            -  Image Box Small Scroll Type: "IMAGE"

            -  Image Box Small Scroll Amount: 1

            -  Image Box Large Scroll Type: "ROW_COLUMN"

            -  Image Box Large Scroll Amount: 1

         -  Item 2: [row 3 of 2048x2560 space]

            -  Image Box Number: 2

            -  Display Environment Spatial Position: (1024/3072,
               1024/2560), (3072/3072, 512/2560)

            -  Image Box Layout Type: "TILED"

            -  Image Box Tile Horizontal Dimension: 3

            -  Image Box Tile Vertical Dimension: 1

            -  Image Box Scroll Direction: "HORIZONTAL"

            -  Image Box Small Scroll Type: "IMAGE"

            -  Image Box Small Scroll Amount: 1

            -  Image Box Large Scroll Type: "ROW_COLUMN"

            -  Image Box Large Scroll Amount: 1

      -  Filter Operations Sequence:

         -  Item 1:

            -  Filter-by Category: "IMAGE_PLANE"

            -  Selector Attribute VR: "CS"

            -  Selector CS Value: "TRANSVERSE"

            -  Filter-by Operator: "MEMBER_OF"

      -  Sorting Operations Sequence:

         -  Item 1:

            -  Sort-by Category: "ALONG_AXIS"

            -  Sorting Direction: "INCREASING"

      -  Display Set Patient Orientation: "L\P"

      -  VOI Type: BRAIN

      -  Show Graphic Annotation Flag: "YES"

   -  Item 22: [CT old two part scrolled, rows 2 & 4]

      -  Display Set Number: 22

      -  Display Set Presentation Group: 4

      -  Image Set Number: 3

      -  Image Boxes Sequence:

         -  Item 1: [row 2 of 2048x2560 space]

            -  Image Box Number: 1

            -  Display Environment Spatial Position: (1024/3072,
               1536/2560), (3072/3072, 1024/2560)

            -  Image Box Layout Type: "TILED"

            -  Image Box Tile Horizontal Dimension: 3

            -  Image Box Tile Vertical Dimension: 1

            -  Image Box Scroll Direction: "HORIZONTAL"

            -  Image Box Small Scroll Type: "IMAGE"

            -  Image Box Small Scroll Amount: 1

            -  Image Box Large Scroll Type: "ROW_COLUMN"

            -  Image Box Large Scroll Amount: 1

         -  Item 2: [row 4 (bottom row) of 2048x2560 space]

            -  Image Box Number: 2

            -  Display Environment Spatial Position: (1024/3072,
               512/2560), (3072/3072, 0/2560)

            -  Image Box Layout Type: "TILED"

            -  Image Box Tile Horizontal Dimension: 3

            -  Image Box Tile Vertical Dimension: 1

            -  Image Box Scroll Direction: "HORIZONTAL"

            -  Image Box Small Scroll Type: "IMAGE"

            -  Image Box Small Scroll Amount: 1

            -  Image Box Large Scroll Type: "ROW_COLUMN"

            -  Image Box Large Scroll Amount: 1

      -  Filter Operations Sequence:

         -  Item 1:

            -  Filter-by Category: "IMAGE_PLANE"

            -  Selector Attribute VR: "CS"

            -  Selector CS Value: "TRANSVERSE"

            -  Filter-by Operator: "MEMBER_OF"

      -  Sorting Operations Sequence:

         -  Item 1:

            -  Sort-by Category: "ALONG_AXIS"

            -  Sorting Direction: "INCREASING"

      -  Display Set Patient Orientation: "L\P"

      -  VOI Type: BRAIN

      -  Show Graphic Annotation Flag: "YES"

-  Partial Data Display Handling: "MAINTAIN_LAYOUT"

-  Synchronized Scrolling Sequence: [Link up (synchronize) the MR and CT
   tiled scroll panes in Display Sets 15 and 16, and the CT new and CT
   old tiled scroll panes in Display Sets 21 and 22]

   -  Item 1:

      -  Display Set Scrolling Group: 15\16

   -  Item 2:

      -  Display Set Scrolling Group: 21\22

.. _sect_V.5:

Hanging Protocol Query Example
------------------------------

The following is an example of a general C-FIND Request for the Hanging
Protocol Information Model - FIND SOP Class that is searching for all
Chest related Hanging Protocols for the purpose of reading projection
Chest X-ray. The user is at a workstation that has two 2Kx2.5K screens.

C-FIND Request:

+----------+----------+----------+--------+----------+----------+
| **N      | **Att    | **Tag**  | **VR** | **VL     | *        |
| esting** | ribute** |          |        | (hex)**  | *Value** |
+==========+==========+==========+========+==========+==========+
|          | Affected | (00      | UI     | 0018     | 1.2.840. |
|          | SOP      | 00,0002) |        |          | 10008.5. |
|          | Class    |          |        |          | 1.4.38.2 |
|          | UID      |          |        |          |          |
+----------+----------+----------+--------+----------+----------+
|          | Command  | (00      | US     | 0002     | 0020H    |
|          | Field    | 00,0100) |        |          | [C-      |
|          |          |          |        |          | FIND-RQ] |
+----------+----------+----------+--------+----------+----------+
|          | Message  | (00      | US     | 0002     | 0010H    |
|          | ID       | 00,0110) |        |          |          |
+----------+----------+----------+--------+----------+----------+
|          | Priority | (00      | US     | 0002     | 0000H    |
|          |          | 00,0700) |        |          | [MEDIUM] |
+----------+----------+----------+--------+----------+----------+
|          | Data Set | (00      | US     | 0002     | 0102H    |
|          | Type     | 00,0800) |        |          |          |
+----------+----------+----------+--------+----------+----------+
|          | SOP      | (00      | UI     | 0000     |          |
|          | Class    | 08,0016) |        |          |          |
|          | UID      |          |        |          |          |
+----------+----------+----------+--------+----------+----------+
|          | SOP      | (00      | UI     | 0000     |          |
|          | Instance | 08,0018) |        |          |          |
|          | UID      |          |        |          |          |
+----------+----------+----------+--------+----------+----------+
|          | Hanging  | (00      | SH     | 0000     |          |
|          | Protocol | 72,0002) |        |          |          |
|          | Name     |          |        |          |          |
+----------+----------+----------+--------+----------+----------+
|          | Hanging  | (00      | LO     | 0000     |          |
|          | Protocol | 72,0004) |        |          |          |
|          | Des      |          |        |          |          |
|          | cription |          |        |          |          |
+----------+----------+----------+--------+----------+----------+
|          | Hanging  | (00      | CS     | 0000     |          |
|          | Protocol | 72,0006) |        |          |          |
|          | Level    |          |        |          |          |
+----------+----------+----------+--------+----------+----------+
|          | Hanging  | (00      | LO     | 0000     |          |
|          | Protocol | 72,0008) |        |          |          |
|          | Creator  |          |        |          |          |
+----------+----------+----------+--------+----------+----------+
|          | Hanging  | (00      | DT     | 0000     |          |
|          | Protocol | 72,000A) |        |          |          |
|          | Creation |          |        |          |          |
|          | DateTime |          |        |          |          |
+----------+----------+----------+--------+----------+----------+
|          | Hanging  | (00      | SQ     | ffffffff |          |
|          | Protocol | 72,000C) |        |          |          |
|          | De       |          |        |          |          |
|          | finition |          |        |          |          |
|          | Sequence |          |        |          |          |
+----------+----------+----------+--------+----------+----------+
| %item    |          |          |        |          |          |
+----------+----------+----------+--------+----------+----------+
| >        | Modality | (00      | CS     | 0000     |          |
|          |          | 08,0060) |        |          |          |
+----------+----------+----------+--------+----------+----------+
| >        | Anatomic | (00      | SQ     | ffffffff |          |
|          | Region   | 08,2218) |        |          |          |
|          | Sequence |          |        |          |          |
+----------+----------+----------+--------+----------+----------+
| %item    |          |          |        |          |          |
+----------+----------+----------+--------+----------+----------+
| >>       | Code     | (00      | SH     | 0008     | 51185008 |
|          | Value    | 08,0100) |        |          |          |
+----------+----------+----------+--------+----------+----------+
| >>       | Coding   | (00      | SH     | 0004     | SCT      |
|          | Scheme   | 08,0102) |        |          |          |
|          | De       |          |        |          |          |
|          | signator |          |        |          |          |
+----------+----------+----------+--------+----------+----------+
| >>       | Code     | (00      | LO     | 0006     | Chest    |
|          | Meaning  | 08,0104) |        |          |          |
+----------+----------+----------+--------+----------+----------+
| %enditem |          |          |        |          |          |
+----------+----------+----------+--------+----------+----------+
| %endseq  |          |          |        |          |          |
+----------+----------+----------+--------+----------+----------+
| >        | P        | (00      | SQ     | 0000     |          |
|          | rocedure | 08,1032) |        |          |          |
|          | Code     |          |        |          |          |
|          | Sequence |          |        |          |          |
+----------+----------+----------+--------+----------+----------+
| >        | La       | (00      | CS     | 0000     |          |
|          | terality | 20,0060) |        |          |          |
+----------+----------+----------+--------+----------+----------+
| >        | Reason   | (00      | SQ     | 0000     |          |
|          | for      | 40,100A) |        |          |          |
|          | R        |          |        |          |          |
|          | equested |          |        |          |          |
|          | P        |          |        |          |          |
|          | rocedure |          |        |          |          |
|          | Code     |          |        |          |          |
|          | Sequence |          |        |          |          |
+----------+----------+----------+--------+----------+----------+
| %enditem |          |          |        |          |          |
+----------+----------+----------+--------+----------+----------+
| %endseq  |          |          |        |          |          |
+----------+----------+----------+--------+----------+----------+
|          | Hanging  | (00      | SQ     | 0000     |          |
|          | Protocol | 72,000E) |        |          |          |
|          | User     |          |        |          |          |
|          | Identi   |          |        |          |          |
|          | fication |          |        |          |          |
|          | Code     |          |        |          |          |
|          | Sequence |          |        |          |          |
+----------+----------+----------+--------+----------+----------+
|          | Number   | (00      | US     | 0000     |          |
|          | of       | 72,0014) |        |          |          |
|          | Priors   |          |        |          |          |
|          | Re       |          |        |          |          |
|          | ferenced |          |        |          |          |
+----------+----------+----------+--------+----------+----------+
|          | Number   | (00      | US     | 0000     |          |
|          | of       | 72,0100) |        |          |          |
|          | Screens  |          |        |          |          |
+----------+----------+----------+--------+----------+----------+
|          | Nominal  | (00      | SQ     | 0000     |          |
|          | Screen   | 72,0102) |        |          |          |
|          | De       |          |        |          |          |
|          | finition |          |        |          |          |
|          | Sequence |          |        |          |          |
+----------+----------+----------+--------+----------+----------+

The following is an example of a set of C-FIND Responses for the Hanging
Protocol Information Model - FIND SOP Class, answering the C-FIND
Request listed above. There are a few matches for this general query.
The application needs to select the best choice among the matches, which
is the second response. The first response is for Chest CT, and the
third response does not match the user's workstation environment as well
as does the second.

C-FIND Response #1:

+----------+----------+----------+--------+----------+----------+
| **N      | **Att    | **Tag**  | **VR** | **VL     | *        |
| esting** | ribute** |          |        | (hex)**  | *Value** |
+==========+==========+==========+========+==========+==========+
|          | Affected | (00      | UI     | 0018     | 1.2.840. |
|          | SOP      | 00,0002) |        |          | 10008.5. |
|          | Class    |          |        |          | 1.4.38.2 |
|          | UID      |          |        |          |          |
+----------+----------+----------+--------+----------+----------+
|          | Command  | (00      | US     | 0002     | 8020H    |
|          | Field    | 00,0100) |        |          | [C-F     |
|          |          |          |        |          | IND-RSP] |
+----------+----------+----------+--------+----------+----------+
|          | Message  | (00      | US     | 0002     | 0010H    |
|          | ID Being | 00,0120) |        |          |          |
|          | R        |          |        |          |          |
|          | esponded |          |        |          |          |
|          | To       |          |        |          |          |
+----------+----------+----------+--------+----------+----------+
|          | Data Set | (00      | US     | 0002     | 0102H    |
|          | Type     | 00,0800) |        |          |          |
+----------+----------+----------+--------+----------+----------+
|          | Status   | (00      | US     | 0002     | FF00H    |
|          |          | 00,0900) |        |          | [        |
|          |          |          |        |          | Pending] |
+----------+----------+----------+--------+----------+----------+
|          | SOP      | (00      | UI     | 0018     | 1.2.840. |
|          | Class    | 08,0016) |        |          | 10008.5. |
|          | UID      |          |        |          | 1.4.38.1 |
+----------+----------+----------+--------+----------+----------+
|          | SOP      | (00      | UI     | 0024     | 1.2      |
|          | Instance | 08,0018) |        |          | .840.100 |
|          | UID      |          |        |          | 08.5.1.4 |
|          |          |          |        |          | .1.1.763 |
|          |          |          |        |          | 92.999.2 |
+----------+----------+----------+--------+----------+----------+
|          | Hanging  | (00      | SH     | 000a     | CT 1     |
|          | Protocol | 72,0002) |        |          | prior    |
|          | Name     |          |        |          |          |
+----------+----------+----------+--------+----------+----------+
|          | Hanging  | (00      | LO     | 0038     | Dual     |
|          | Protocol | 72,0004) |        |          | screen   |
|          | Des      |          |        |          | layout   |
|          | cription |          |        |          | for      |
|          |          |          |        |          | current  |
|          |          |          |        |          | and      |
|          |          |          |        |          | single   |
|          |          |          |        |          | prior    |
|          |          |          |        |          | chest CT |
+----------+----------+----------+--------+----------+----------+
|          | Hanging  | (00      | CS     | 000c     | SIN      |
|          | Protocol | 72,0006) |        |          | GLE_USER |
|          | Level    |          |        |          |          |
+----------+----------+----------+--------+----------+----------+
|          | Hanging  | (00      | LO     | 0008     | Dr. Chan |
|          | Protocol | 72,0008) |        |          |          |
|          | Creator  |          |        |          |          |
+----------+----------+----------+--------+----------+----------+
|          | Hanging  | (00      | DT     | 000c     | 2004     |
|          | Protocol | 72,000A) |        |          | 08210718 |
|          | Creation |          |        |          |          |
|          | DateTime |          |        |          |          |
+----------+----------+----------+--------+----------+----------+
|          | Hanging  | (00      | SQ     | ffffffff |          |
|          | Protocol | 72,000C) |        |          |          |
|          | De       |          |        |          |          |
|          | finition |          |        |          |          |
|          | Sequence |          |        |          |          |
+----------+----------+----------+--------+----------+----------+
| %item    |          |          |        |          |          |
+----------+----------+----------+--------+----------+----------+
| >        | Modality | (00      | CS     | 0002     | CT       |
|          |          | 08,0060) |        |          |          |
+----------+----------+----------+--------+----------+----------+
| >        | Anatomic | (00      | SQ     | ffffffff |          |
|          | Region   | 08,2218) |        |          |          |
|          | Sequence |          |        |          |          |
+----------+----------+----------+--------+----------+----------+
| %item    |          |          |        |          |          |
+----------+----------+----------+--------+----------+----------+
| >>       | Code     | (00      | SH     | 0008     | 51185008 |
|          | Value    | 08,0100) |        |          |          |
+----------+----------+----------+--------+----------+----------+
| >>       | Coding   | (00      | SH     | 0004     | SCT      |
|          | Scheme   | 08,0102) |        |          |          |
|          | De       |          |        |          |          |
|          | signator |          |        |          |          |
+----------+----------+----------+--------+----------+----------+
| >>       | Code     | (00      | LO     | 0006     | Chest    |
|          | Meaning  | 08,0104) |        |          |          |
+----------+----------+----------+--------+----------+----------+
| %enditem |          |          |        |          |          |
+----------+----------+----------+--------+----------+----------+
| %endseq  |          |          |        |          |          |
+----------+----------+----------+--------+----------+----------+
| >        | P        | (00      | SQ     | 0000     |          |
|          | rocedure | 08,1032) |        |          |          |
|          | Code     |          |        |          |          |
|          | Sequence |          |        |          |          |
+----------+----------+----------+--------+----------+----------+
| >        | La       | (00      | CS     | 0000     |          |
|          | terality | 20,0060) |        |          |          |
+----------+----------+----------+--------+----------+----------+
| >        | Reason   | (00      | SQ     | 0000     |          |
|          | for      | 40,100A) |        |          |          |
|          | R        |          |        |          |          |
|          | equested |          |        |          |          |
|          | P        |          |        |          |          |
|          | rocedure |          |        |          |          |
|          | Code     |          |        |          |          |
|          | Sequence |          |        |          |          |
+----------+----------+----------+--------+----------+----------+
| %enditem |          |          |        |          |          |
+----------+----------+----------+--------+----------+----------+
| %endseq  |          |          |        |          |          |
+----------+----------+----------+--------+----------+----------+
|          | Hanging  | (00      | SQ     | 0000     |          |
|          | Protocol | 72,000E) |        |          |          |
|          | User     |          |        |          |          |
|          | Identi   |          |        |          |          |
|          | fication |          |        |          |          |
|          | Code     |          |        |          |          |
|          | Sequence |          |        |          |          |
+----------+----------+----------+--------+----------+----------+
| %item    |          |          |        |          |          |
+----------+----------+----------+--------+----------+----------+
| >        | Code     | (00      | SH     | 000a     | 5        |
|          | Value    | 08,0100) |        |          | 8489749P |
+----------+----------+----------+--------+----------+----------+
| >        | Coding   | (00      | SH     | 0008     | HOSP_ID  |
|          | Scheme   | 08,0102) |        |          |          |
|          | De       |          |        |          |          |
|          | signator |          |        |          |          |
+----------+----------+----------+--------+----------+----------+
| >        | Code     | (00      | LO     | 000e     | Susan H. |
|          | Meaning  | 08,0104) |        |          | Chan     |
+----------+----------+----------+--------+----------+----------+
| %enditem |          |          |        |          |          |
+----------+----------+----------+--------+----------+----------+
| %endseq  |          |          |        |          |          |
+----------+----------+----------+--------+----------+----------+
|          | Number   | (00      | US     | 0002     | 1        |
|          | of       | 72,0014) |        |          |          |
|          | Priors   |          |        |          |          |
|          | Re       |          |        |          |          |
|          | ferenced |          |        |          |          |
+----------+----------+----------+--------+----------+----------+
|          | Number   | (00      | US     | 0002     | 2        |
|          | of       | 72,0100) |        |          |          |
|          | Screens  |          |        |          |          |
+----------+----------+----------+--------+----------+----------+
|          | Nominal  | (00      | SQ     | 0000     |          |
|          | Screen   | 72,0102) |        |          |          |
|          | De       |          |        |          |          |
|          | finition |          |        |          |          |
|          | Sequence |          |        |          |          |
+----------+----------+----------+--------+----------+----------+

C-FIND Response #2:

+----------+----------+----------+--------+----------+----------+
| **N      | **Att    | **Tag**  | **VR** | **VL     | *        |
| esting** | ribute** |          |        | (hex)**  | *Value** |
+==========+==========+==========+========+==========+==========+
|          | Affected | (00      | UI     | 0018     | 1.2.840. |
|          | SOP      | 00,0002) |        |          | 10008.5. |
|          | Class    |          |        |          | 1.4.38.2 |
|          | UID      |          |        |          |          |
+----------+----------+----------+--------+----------+----------+
|          | Command  | (00      | US     | 0002     | 8020H    |
|          | Field    | 00,0100) |        |          | [C-F     |
|          |          |          |        |          | IND-RSP] |
+----------+----------+----------+--------+----------+----------+
|          | Message  | (00      | US     | 0002     | 0010H    |
|          | ID Being | 00,0120) |        |          |          |
|          | R        |          |        |          |          |
|          | esponded |          |        |          |          |
|          | To       |          |        |          |          |
+----------+----------+----------+--------+----------+----------+
|          | Data Set | (00      | US     | 0002     | 0102H    |
|          | Type     | 00,0800) |        |          |          |
+----------+----------+----------+--------+----------+----------+
|          | Status   | (00      | US     | 0002     | FF00H    |
|          |          | 00,0900) |        |          | [        |
|          |          |          |        |          | Pending] |
+----------+----------+----------+--------+----------+----------+
|          | SOP      | (00      | UI     | 0018     | 1.2.840. |
|          | Class    | 08,0016) |        |          | 10008.5. |
|          | UID      |          |        |          | 1.4.38.1 |
+----------+----------+----------+--------+----------+----------+
|          | SOP      | (00      | UI     | 0020     | 1.2.840. |
|          | Instance | 08,0018) |        |          | 123456.2 |
|          | UID      |          |        |          | 0030822. |
|          |          |          |        |          | 223344.1 |
+----------+----------+----------+--------+----------+----------+
|          | Hanging  | (00      | SH     | 000c     | Chest    |
|          | Protocol | 72,0002) |        |          | X-ray    |
|          | Name     |          |        |          |          |
+----------+----------+----------+--------+----------+----------+
|          | Hanging  | (00      | LO     | 0026     | Current  |
|          | Protocol | 72,0004) |        |          | and      |
|          | Des      |          |        |          | Prior    |
|          | cription |          |        |          | Chest PA |
|          |          |          |        |          | and      |
|          |          |          |        |          | Lateral  |
+----------+----------+----------+--------+----------+----------+
|          | Hanging  | (00      | CS     | 0004     | SITE     |
|          | Protocol | 72,0006) |        |          |          |
|          | Level    |          |        |          |          |
+----------+----------+----------+--------+----------+----------+
|          | Hanging  | (00      | LO     | 0012     | Senior   |
|          | Protocol | 72,0008) |        |          | Rad      |
|          | Creator  |          |        |          | iologist |
+----------+----------+----------+--------+----------+----------+
|          | Hanging  | (00      | DT     | 000e     | 200208   |
|          | Protocol | 72,000A) |        |          | 23133455 |
|          | Creation |          |        |          |          |
|          | DateTime |          |        |          |          |
+----------+----------+----------+--------+----------+----------+
|          | Hanging  | (00      | SQ     | ffffffff |          |
|          | Protocol | 72,000C) |        |          |          |
|          | De       |          |        |          |          |
|          | finition |          |        |          |          |
|          | Sequence |          |        |          |          |
+----------+----------+----------+--------+----------+----------+
| %item    |          |          |        |          |          |
+----------+----------+----------+--------+----------+----------+
| >        | Modality | (00      | CS     | 0000     |          |
|          |          | 08,0060) |        |          |          |
+----------+----------+----------+--------+----------+----------+
| >        | Anatomic | (00      | SQ     | ffffffff |          |
|          | Region   | 08,2218) |        |          |          |
|          | Sequence |          |        |          |          |
+----------+----------+----------+--------+----------+----------+
| %item    |          |          |        |          |          |
+----------+----------+----------+--------+----------+----------+
| >>       | Code     | (00      | SH     | 0008     | 51185008 |
|          | Value    | 08,0100) |        |          |          |
+----------+----------+----------+--------+----------+----------+
| >>       | Coding   | (00      | SH     | 0004     | SCT      |
|          | Scheme   | 08,0102) |        |          |          |
|          | De       |          |        |          |          |
|          | signator |          |        |          |          |
+----------+----------+----------+--------+----------+----------+
| >>       | Code     | (00      | LO     | 0006     | Chest    |
|          | Meaning  | 08,0104) |        |          |          |
+----------+----------+----------+--------+----------+----------+
| %enditem |          |          |        |          |          |
+----------+----------+----------+--------+----------+----------+
| %endseq  |          |          |        |          |          |
+----------+----------+----------+--------+----------+----------+
| >        | P        | (00      | SQ     | 0000     |          |
|          | rocedure | 08,1032) |        |          |          |
|          | Code     |          |        |          |          |
|          | Sequence |          |        |          |          |
+----------+----------+----------+--------+----------+----------+
| >        | La       | (00      | CS     | 0000     |          |
|          | terality | 20,0060) |        |          |          |
+----------+----------+----------+--------+----------+----------+
| >        | Reason   | (00      | SQ     | 0000     |          |
|          | for      | 40,100A) |        |          |          |
|          | R        |          |        |          |          |
|          | equested |          |        |          |          |
|          | P        |          |        |          |          |
|          | rocedure |          |        |          |          |
|          | Code     |          |        |          |          |
|          | Sequence |          |        |          |          |
+----------+----------+----------+--------+----------+----------+
| %enditem |          |          |        |          |          |
+----------+----------+----------+--------+----------+----------+
| %endseq  |          |          |        |          |          |
+----------+----------+----------+--------+----------+----------+
|          | Hanging  | (00      | SQ     | 0000     |          |
|          | Protocol | 72,000E) |        |          |          |
|          | User     |          |        |          |          |
|          | Identi   |          |        |          |          |
|          | fication |          |        |          |          |
|          | Code     |          |        |          |          |
|          | Sequence |          |        |          |          |
+----------+----------+----------+--------+----------+----------+
|          | Number   | (00      | US     | 0002     | 1        |
|          | of       | 72,0014) |        |          |          |
|          | Priors   |          |        |          |          |
|          | Re       |          |        |          |          |
|          | ferenced |          |        |          |          |
+----------+----------+----------+--------+----------+----------+
|          | Number   | (00      | US     | 0002     | 0002H    |
|          | of       | 72,0100) |        |          |          |
|          | Screens  |          |        |          |          |
+----------+----------+----------+--------+----------+----------+
|          | Nominal  | (00      | SQ     | ffffffff |          |
|          | Screen   | 72,0102) |        |          |          |
|          | De       |          |        |          |          |
|          | finition |          |        |          |          |
|          | Sequence |          |        |          |          |
+----------+----------+----------+--------+----------+----------+
| %item    |          |          |        |          |          |
+----------+----------+----------+--------+----------+----------+
| >        | Number   | (00      | US     | 0002     | 2560     |
|          | of       | 72,0104) |        |          |          |
|          | Vertical |          |        |          |          |
|          | Pixels   |          |        |          |          |
+----------+----------+----------+--------+----------+----------+
| >        | Number   | (00      | US     | 0002     | 2048     |
|          | of       | 72,0106) |        |          |          |
|          | Ho       |          |        |          |          |
|          | rizontal |          |        |          |          |
|          | Pixels   |          |        |          |          |
+----------+----------+----------+--------+----------+----------+
| >        | Display  | (00      | FD     | 0020     | 0.0\1.0  |
|          | Env      | 72,0108) |        |          | \0.5\0.0 |
|          | ironment |          |        |          |          |
|          | Spatial  |          |        |          |          |
|          | Position |          |        |          |          |
+----------+----------+----------+--------+----------+----------+
| >        | Screen   | (00      | US     | 0002     | 0008H    |
|          | Minimum  | 72,010A) |        |          |          |
|          | G        |          |        |          |          |
|          | rayscale |          |        |          |          |
|          | Bit      |          |        |          |          |
|          | Depth    |          |        |          |          |
+----------+----------+----------+--------+----------+----------+
| >        | App      | (00      | US     | 0002     | 0064H    |
|          | lication | 72,010E) |        |          |          |
|          | Maximum  |          |        |          |          |
|          | Repaint  |          |        |          |          |
|          | Time     |          |        |          |          |
+----------+----------+----------+--------+----------+----------+
| %enditem |          |          |        |          |          |
+----------+----------+----------+--------+----------+----------+
| %item    |          |          |        |          |          |
+----------+----------+----------+--------+----------+----------+
| >        | Number   | (00      | US     | 0002     | 2560     |
|          | of       | 72,0104) |        |          |          |
|          | Vertical |          |        |          |          |
|          | Pixels   |          |        |          |          |
+----------+----------+----------+--------+----------+----------+
| >        | Number   | (00      | US     | 0002     | 2048     |
|          | of       | 72,0106) |        |          |          |
|          | Ho       |          |        |          |          |
|          | rizontal |          |        |          |          |
|          | Pixels   |          |        |          |          |
+----------+----------+----------+--------+----------+----------+
| >        | Display  | (00      | FD     | 0020     | 0.5\1.0  |
|          | Env      | 72,0108) |        |          | \1.0\0.0 |
|          | ironment |          |        |          |          |
|          | Spatial  |          |        |          |          |
|          | Position |          |        |          |          |
+----------+----------+----------+--------+----------+----------+
| >        | Screen   | (00      | US     | 0002     | 0008H    |
|          | Minimum  | 72,010A) |        |          |          |
|          | G        |          |        |          |          |
|          | rayscale |          |        |          |          |
|          | Bit      |          |        |          |          |
|          | Depth    |          |        |          |          |
+----------+----------+----------+--------+----------+----------+
| >        | App      | (00      | US     | 0004     | 0064H    |
|          | lication | 72,010E) |        |          |          |
|          | Maximum  |          |        |          |          |
|          | Repaint  |          |        |          |          |
|          | Time     |          |        |          |          |
+----------+----------+----------+--------+----------+----------+
| %enditem |          |          |        |          |          |
+----------+----------+----------+--------+----------+----------+
| %endseq  |          |          |        |          |          |
+----------+----------+----------+--------+----------+----------+

C-FIND Response #3:

+----------+----------+----------+--------+----------+----------+
| **N      | **Att    | **Tag**  | **VR** | **VL     | *        |
| esting** | ribute** |          |        | (hex)**  | *Value** |
+==========+==========+==========+========+==========+==========+
|          | Affected | (00      | UI     | 0018     | 1.2.840. |
|          | SOP      | 00,0002) |        |          | 10008.5. |
|          | Class    |          |        |          | 1.4.38.2 |
|          | UID      |          |        |          |          |
+----------+----------+----------+--------+----------+----------+
|          | Command  | (00      | US     | 0002     | 8020H    |
|          | Field    | 00,0100) |        |          | [C-F     |
|          |          |          |        |          | IND-RSP] |
+----------+----------+----------+--------+----------+----------+
|          | Message  | (00      | US     | 0002     | 0010H    |
|          | ID Being | 00,0120) |        |          |          |
|          | R        |          |        |          |          |
|          | esponded |          |        |          |          |
|          | To       |          |        |          |          |
+----------+----------+----------+--------+----------+----------+
|          | Data Set | (00      | US     | 0002     | 0102H    |
|          | Type     | 00,0800) |        |          |          |
+----------+----------+----------+--------+----------+----------+
|          | Status   | (00      | US     | 0002     | FF00H    |
|          |          | 00,0900) |        |          | [        |
|          |          |          |        |          | Pending] |
+----------+----------+----------+--------+----------+----------+
|          | SOP      | (00      | UI     | 0018     | 1.2.840. |
|          | Class    | 08,0016) |        |          | 10008.5. |
|          | UID      |          |        |          | 1.4.38.1 |
+----------+----------+----------+--------+----------+----------+
|          | SOP      | (00      | UI     | 002a     | 1.       |
|          | Instance | 08,0018) |        |          | 2.840.11 |
|          | UID      |          |        |          | 3986.2.6 |
|          |          |          |        |          | 64566.21 |
|          |          |          |        |          | 121125.8 |
|          |          |          |        |          | 5669.967 |
+----------+----------+----------+--------+----------+----------+
|          | Hanging  | (00      | SH     | 0010     | Chest    |
|          | Protocol | 72,0002) |        |          | X-       |
|          | Name     |          |        |          | ray_LGon |
+----------+----------+----------+--------+----------+----------+
|          | Hanging  | (00      | LO     | 003e     | Prior    |
|          | Protocol | 72,0004) |        |          | and      |
|          | Des      |          |        |          | Current  |
|          | cription |          |        |          | Lateral  |
|          |          |          |        |          | of Chest |
|          |          |          |        |          | X-ray    |
|          |          |          |        |          | for two  |
|          |          |          |        |          | screen   |
|          |          |          |        |          | system   |
+----------+----------+----------+--------+----------+----------+
|          | Hanging  | (00      | CS     | 000c     | SIN      |
|          | Protocol | 72,0006) |        |          | GLE_USER |
|          | Level    |          |        |          |          |
+----------+----------+----------+--------+----------+----------+
|          | Hanging  | (00      | LO     | 0012     | Dr. Leia |
|          | Protocol | 72,0008) |        |          | Gonzales |
|          | Creator  |          |        |          |          |
+----------+----------+----------+--------+----------+----------+
|          | Hanging  | (00      | DT     | 000e     | 200308   |
|          | Protocol | 72,000A) |        |          | 22101100 |
|          | Creation |          |        |          |          |
|          | DateTime |          |        |          |          |
+----------+----------+----------+--------+----------+----------+
|          | Hanging  | (00      | SQ     | ffffffff |          |
|          | Protocol | 72,000C) |        |          |          |
|          | De       |          |        |          |          |
|          | finition |          |        |          |          |
|          | Sequence |          |        |          |          |
+----------+----------+----------+--------+----------+----------+
| %item    |          |          |        |          |          |
+----------+----------+----------+--------+----------+----------+
| >        | Modality | (00      | CS     | 0002     | DX       |
|          |          | 08,0060) |        |          |          |
+----------+----------+----------+--------+----------+----------+
| >        | Anatomic | (00      | SQ     | ffffffff |          |
|          | Region   | 08,2218) |        |          |          |
|          | Sequence |          |        |          |          |
+----------+----------+----------+--------+----------+----------+
| %item    |          |          |        |          |          |
+----------+----------+----------+--------+----------+----------+
| >>       | Code     | (00      | SH     | 0008     | 51185008 |
|          | Value    | 08,0100) |        |          |          |
+----------+----------+----------+--------+----------+----------+
| >>       | Coding   | (00      | SH     | 0004     | SCT      |
|          | Scheme   | 08,0102) |        |          |          |
|          | De       |          |        |          |          |
|          | signator |          |        |          |          |
+----------+----------+----------+--------+----------+----------+
| >>       | Code     | (00      | LO     | 0006     | Chest    |
|          | Meaning  | 08,0104) |        |          |          |
+----------+----------+----------+--------+----------+----------+
| %enditem |          |          |        |          |          |
+----------+----------+----------+--------+----------+----------+
| %endseq  |          |          |        |          |          |
+----------+----------+----------+--------+----------+----------+
| >        | P        | (00      | SQ     | 0000     |          |
|          | rocedure | 08,1032) |        |          |          |
|          | Code     |          |        |          |          |
|          | Sequence |          |        |          |          |
+----------+----------+----------+--------+----------+----------+
| >        | La       | (00      | CS     | 0000     |          |
|          | terality | 20,0060) |        |          |          |
+----------+----------+----------+--------+----------+----------+
| >        | Reason   | (00      | SQ     | 0000     |          |
|          | for      | 40,100A) |        |          |          |
|          | R        |          |        |          |          |
|          | equested |          |        |          |          |
|          | P        |          |        |          |          |
|          | rocedure |          |        |          |          |
|          | Code     |          |        |          |          |
|          | Sequence |          |        |          |          |
+----------+----------+----------+--------+----------+----------+
| %enditem |          |          |        |          |          |
+----------+----------+----------+--------+----------+----------+
| %endseq  |          |          |        |          |          |
+----------+----------+----------+--------+----------+----------+
|          | Hanging  | (00      | SQ     | 0000     |          |
|          | Protocol | 72,000E) |        |          |          |
|          | User     |          |        |          |          |
|          | Identi   |          |        |          |          |
|          | fication |          |        |          |          |
|          | Code     |          |        |          |          |
|          | Sequence |          |        |          |          |
+----------+----------+----------+--------+----------+----------+
| %item    |          |          |        |          |          |
+----------+----------+----------+--------+----------+----------+
| >        | Code     | (00      | SH     | 0004     | Lgon     |
|          | Value    | 08,0100) |        |          |          |
+----------+----------+----------+--------+----------+----------+
| >        | Coding   | (00      | SH     | 0008     | 99Local  |
|          | Scheme   | 08,0102) |        |          |          |
|          | De       |          |        |          |          |
|          | signator |          |        |          |          |
+----------+----------+----------+--------+----------+----------+
| >        | Coding   | (00      | SH     | 0004     | v40a     |
|          | Scheme   | 08,0103) |        |          |          |
|          | Version  |          |        |          |          |
+----------+----------+----------+--------+----------+----------+
| >        | Code     | (00      | LO     | 000c     | log-in   |
|          | Meaning  | 08,0104) |        |          | name     |
+----------+----------+----------+--------+----------+----------+
| %enditem |          |          |        |          |          |
+----------+----------+----------+--------+----------+----------+
| %endseq  |          |          |        |          |          |
+----------+----------+----------+--------+----------+----------+
|          | Number   | (00      | US     | 0002     | 1        |
|          | of       | 72,0014) |        |          |          |
|          | Priors   |          |        |          |          |
|          | Re       |          |        |          |          |
|          | ferenced |          |        |          |          |
+----------+----------+----------+--------+----------+----------+
|          | Number   | (00      | US     | 0002     | 0002H    |
|          | of       | 72,0100) |        |          |          |
|          | Screens  |          |        |          |          |
+----------+----------+----------+--------+----------+----------+
|          | Nominal  | (00      | SQ     | ffffffff |          |
|          | Screen   | 72,0102) |        |          |          |
|          | De       |          |        |          |          |
|          | finition |          |        |          |          |
|          | Sequence |          |        |          |          |
+----------+----------+----------+--------+----------+----------+
| %item    |          |          |        |          |          |
+----------+----------+----------+--------+----------+----------+
| >        | Number   | (00      | US     | 0002     | 1280     |
|          | of       | 72,0104) |        |          |          |
|          | Vertical |          |        |          |          |
|          | Pixels   |          |        |          |          |
+----------+----------+----------+--------+----------+----------+
| >        | Number   | (00      | US     | 0002     | 1024     |
|          | of       | 72,0106) |        |          |          |
|          | Ho       |          |        |          |          |
|          | rizontal |          |        |          |          |
|          | Pixels   |          |        |          |          |
+----------+----------+----------+--------+----------+----------+
| >        | Display  | (00      | FD     | 0020     | 0.0\1.0  |
|          | Env      | 72,0108) |        |          | \0.5\0.0 |
|          | ironment |          |        |          |          |
|          | Spatial  |          |        |          |          |
|          | Position |          |        |          |          |
+----------+----------+----------+--------+----------+----------+
| >        | Screen   | (00      | US     | 0002     | 0008H    |
|          | Minimum  | 72,010A) |        |          |          |
|          | G        |          |        |          |          |
|          | rayscale |          |        |          |          |
|          | Bit      |          |        |          |          |
|          | Depth    |          |        |          |          |
+----------+----------+----------+--------+----------+----------+
| >        | App      | (00      | US     | 0004     | 0064H    |
|          | lication | 72,010E) |        |          |          |
|          | Maximum  |          |        |          |          |
|          | Repaint  |          |        |          |          |
|          | Time     |          |        |          |          |
+----------+----------+----------+--------+----------+----------+
| %enditem |          |          |        |          |          |
+----------+----------+----------+--------+----------+----------+
| %item    |          |          |        |          |          |
+----------+----------+----------+--------+----------+----------+
| >        | Number   | (00      | US     | 0002     | 1280     |
|          | of       | 72,0104) |        |          |          |
|          | Vertical |          |        |          |          |
|          | Pixels   |          |        |          |          |
+----------+----------+----------+--------+----------+----------+
| >        | Number   | (00      | US     | 0002     | 1024     |
|          | of       | 72,0106) |        |          |          |
|          | Ho       |          |        |          |          |
|          | rizontal |          |        |          |          |
|          | Pixels   |          |        |          |          |
+----------+----------+----------+--------+----------+----------+
| >        | Display  | (00      | FD     | 0020     | 0.5\1.0  |
|          | Env      | 72,0108) |        |          | \1.0\0.0 |
|          | ironment |          |        |          |          |
|          | Spatial  |          |        |          |          |
|          | Position |          |        |          |          |
+----------+----------+----------+--------+----------+----------+
| >        | Screen   | (00      | US     | 0002     | 0008H    |
|          | Minimum  | 72,010A) |        |          |          |
|          | G        |          |        |          |          |
|          | rayscale |          |        |          |          |
|          | Bit      |          |        |          |          |
|          | Depth    |          |        |          |          |
+----------+----------+----------+--------+----------+----------+
| >        | App      | (00      | US     | 0004     | 0064H    |
|          | lication | 72,010E) |        |          |          |
|          | Maximum  |          |        |          |          |
|          | Repaint  |          |        |          |          |
|          | Time     |          |        |          |          |
+----------+----------+----------+--------+----------+----------+
| %enditem |          |          |        |          |          |
+----------+----------+----------+--------+----------+----------+
| %endseq  |          |          |        |          |          |
+----------+----------+----------+--------+----------+----------+

C-FIND Response #4:

+----------+----------+----------+--------+----------+----------+
| **N      | **Att    | **Tag**  | **VR** | **VL     | *        |
| esting** | ribute** |          |        | (hex)**  | *Value** |
+==========+==========+==========+========+==========+==========+
|          | Affected | (00      | UI     | 0018     | 1        |
|          | SOP      | 00,0002) |        |          | .2.840.1 |
|          | Class    |          |        |          | 0008.5.1 |
|          | UID      |          |        |          | .4.38.2. |
+----------+----------+----------+--------+----------+----------+
|          | Command  | (00      | US     | 0002     | 8020H    |
|          | Field    | 00,0100) |        |          | [C-F     |
|          |          |          |        |          | IND-RSP] |
+----------+----------+----------+--------+----------+----------+
|          | Message  | (00      | US     | 0002     | 0010H    |
|          | ID Being | 00,0120) |        |          |          |
|          | R        |          |        |          |          |
|          | esponded |          |        |          |          |
|          | To       |          |        |          |          |
+----------+----------+----------+--------+----------+----------+
|          | Data Set | (00      | US     | 0002     | 0101H    |
|          | Type     | 00,0800) |        |          |          |
+----------+----------+----------+--------+----------+----------+
|          | Status   | (00      | US     | 0002     | 0000H    |
|          |          | 00,0900) |        |          | [        |
|          |          |          |        |          | Success] |
+----------+----------+----------+--------+----------+----------+

.. _sect_V.6:

Display Set Patient Orientation Example
---------------------------------------

For Display Set Patient Orientation (0072,0700) with value "A\F", the
application interpreting the Hanging Protocol will arrange sagittal
images oriented with the patient's anterior toward the right side of the
image box, and the patient's foot will be toward the bottom of the image
box. An incoming sagittal MRI image as shown in
`figure_title <#figure_V.6-1>`__ will require a horizontal flip before
display in the image box.

