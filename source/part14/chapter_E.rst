.. _chapter_E:

Realizable JND Range of a Display Under Ambient Light (Informative)
===================================================================

*Dynamic range*\ is an often used measures of the information content
that can be presented by a Display System. However, there are many
definitions of dynamic range, and most such definitions do not take into
account real world conditions that affect the actual amount of
information that can be conveyed by a gray scale pixel. For example,
Poynton [E1] refers to the *contrast ratio*\ of a gray scale display
device as the ratio of display intensity between the brightest white and
the darkest black of the particular display device in question. However,
this definition of dynamic range applies to ideal viewing conditions.
Real world conditions such as veiling glare, noise, spatial frequency
content of the image, power supply saturation, and ambient lighting in a
cathode ray tube (CRT) based viewing situation can degrade the measured
dynamic range of the system significantly [E2, E3]. Because of all of
these variables dynamic range is an ill-defined concept for a Display
System.

.. note::

   *Veiling Glare* is the phenomenon wherein internal light reflections
   inside the CRT creates a "background lighting" thus reducing the
   contrast range of the CRT device.

The methods used to determine the degree to which the Display Function
of a Display System approximates the Grayscale Standard Display Function
can also be used to define two measures that might better characterize
the potential capabilities of a Display System to convey information
content. Two measures, the theoretically achievable JNDs and the
realized JNDs, are useful for comparing Display Systems [E4].

The number of theoretically achievable JNDs is simply the number of JNDs
predicted by the visual model given the Luminance Range of the Display
System used. The number of theoretically achievable JNDs of a Display
System may be found from `table_title <#table_B-1>`__ by counting the
number of JNDs in the table that fall between the measured minimum and
maximum Luminance of the Display System.

This number of JNDs may not actually be achievable due to resolution
limitations of other portions of the Display System, in particular, the
quantization resolution given by the finite number of bits per pixel
driving the Display System. For example, `table_title <#table_B-1>`__
may show that a particular Display System is capable of delivering 352
JNDs. However, if only 8 bits per pixel are presented to the Display
System, the number of JNDs achievable cannot exceed 2 :sup:`8`\ = 256
JNDs because of the quantizing effect. In actual fact, the number of
JNDs realized in a Display System will always be smaller than or equal
to the lower of the theoretically achievable JNDs and the quantization
limit. This is because some of the quantized values input to the display
may not line up with the input value required to achieve the next JND.

The more useful number of realized JNDs, describes how many JNDs are
actually achieved given the specifics of the Display System (i.e., the
number of gray levels of contrast resolution and the distribution of
Luminance values). This definition gives a measure of the information
that can actually be conveyed by the system to a human observer, in
essence, an informational dynamic range. This number is calculated
beginning at the minimum Luminance of the Display System, and then
stepping one JND in Luminance from the current Luminance value, and
choosing the smallest increment in DDL value that achieves a step at
least that large. Repeating this through all the available DDLs will
produce a sequence of steps, all at least 1 JND apart, and the length of
this sequence of steps is then the number of realizable JNDs of the
Display System.

The methods of PS3.14 cannot precisely duplicate all of the real world
sources of degradation in a Display System. However, this uniform method
of determining the realizable number of JNDs should give a measure of
the actual performance of a particular Display System that would be
experienced by a human observer when using the Display System in a real
world situation such as the viewing of radiological images in medicine.

**References**

[E1] Poynton, C. "Frequently Asked Questions about Gamma",Internet
ftp://ftp.inforamp.net/pub/users/poynton/doc/colour/gammaFAQ.pdf

[E2] Roehrig, H., Blume, H., Ji, T. and Browne, M.; "Performance Tests
and Quality Control of Cathode Ray Tube Displays"; J. Digital Imaging,
Vol. 3, No. 3, August 1990; pp. 134-145.

[E3] Gray, J.; "Use of the SMPTE Test Pattern in Picture Archiving and
Communication Systems"; J. Digital Imaging, Vol. 5, No. 1, February
1992; pp. 54-58.

[E4] Hemminger, B., Muller, K., "Performance Metric for evaluating
conformance of medical image displays with the ACR/NEMA display function
standard", SPIE Medical Imaging 1997, editor Yongmin Kim, vol 3031-25,
1997.
