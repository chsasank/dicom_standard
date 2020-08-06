.. _chapter_Foreword:

Foreword
========

This DICOM Standard was developed according to the procedures of the
DICOM Standards Committee.

While other parts of the DICOM Standard specify how digital image data
can be moved from system to system, it does not specify how the pixel
values should be interpreted or displayed. PS3.14 specifies a function
that relates pixel values to displayed Luminance levels.

A digital signal from an image can be measured, characterized,
transmitted, and reproduced objectively and accurately. However, the
visual interpretation of that signal is dependent on the varied
characteristics of the systems displaying that image. Currently, images
produced by the same signal may have completely different visual
appearance, information, and characteristics on different display
devices.

In medical imaging, it is important that there be a visual consistency
in how a given digital image appears, whether viewed, for example, on
the display monitor of a workstation or as a film on a light-box. In the
absence of any standard that regulates how these images are to be
visually presented on any device, a digital image that has good
diagnostic value when viewed on one device could look very different and
have greatly reduced diagnostic value when viewed on another device.
Accordingly, PS3.14 was developed to provide an objective, quantitative
mechanism for mapping digital image values into a given range of
Luminance. An application that knows this relationship between digital
values and display Luminance can produce better visual consistency in
how that image appears on diverse display devices. The relationship that
PS3.14 defines between digital image values and displayed Luminance is
based upon measurements and models of human perception over a wide range
of Luminance, not upon the characteristics of any one image presentation
device or of any one imaging modality. It is also not dependent upon
user preferences, which can be more properly handled by other constructs
such as the DICOM Presentation Lookup Table.

The DICOM Standard is structured as a multi-part document using the
guidelines established in
`biblioentry_title <#biblio_ISODirectives2>`__.

DICOM® is the registered trademark of the National Electrical
Manufacturers Association for its standards publications relating to
digital communications of medical information, all rights reserved.

HL7® and CDA® are the registered trademarks of Health Level Seven
International, all rights reserved.

SNOMED®, SNOMED Clinical Terms®, SNOMED CT® are the registered
trademarks of the International Health Terminology Standards Development
*Organisation* (IHTSDO), all rights reserved.

LOINC® is the registered trademark of Regenstrief Institute, Inc, all
rights reserved.

