.. _chapter_C:

Measuring the Accuracy With Which a Display System Matches the Grayscale Standard Display Function (Informative)
================================================================================================================

.. _sect_C.1:

General Considerations Regarding Conformance and Metrics
--------------------------------------------------------

To demonstrate conformance with the Grayscale Standard Display Function
is a much more complex task than, for example, validating the responses
of a totally digital system to DICOM messages.

Display systems ultimately produce analog output, either directly as
Luminances or indirectly as optical densities. For some Display Systems,
this analog output can be affected by various imperfections in addition
to whatever imperfections exist in the Display System's Display Function
that is to be validated. For example, there may be spatial
non-uniformities in the final presented image (e.g., arising from film,
printing, or processing non-uniformities in the case of a hardcopy
printer) that are measurable but are at low spatial frequencies that do
not ordinarily pose an image quality problem in diagnostic radiology.

It is worth noting that CRTs and light-boxes also introduce their own
spatial non-uniformities. These non-uniformities are outside the scope
of the Grayscale Standard Display Function and the measurement
procedures described here. But because of them, even a test image that
is perfectly presented in terms of the Grayscale Standard Display
Function will be less than perfectly perceived on a real CRT or a real
light-box.

Furthermore, the question "How close (to the Grayscale Standard Display
Function) is close enough?" is currently unanswered, since the answer
depends on psychophysical studies not yet done to determine what
difference in Display Function is "just noticeable" when two nearly
identical image presentations (e.g., two nearly identical films placed
on equivalent side-by-side light-boxes) are presented to an observer.

Furthermore, the evaluation of a given Display System could be based
either on visual tests (e.g., assessing the perceived contrast of many
low-contrast targets in one or more test images) or by quantitative
analysis based on measured data obtained from instruments (e.g.,
photometers or densitometers).

Even the quantitative approach could be addressed in different ways. One
could, for example, simply superimpose plots of measured and theoretical
analog output (i.e., Luminance or optical density) vs. P-Value, perhaps
along with "error bars" indicating the expected uncertainty
(non-repeatable variations) in the measured output. As a mathematically
more elegant alternative, all the measured data points could be used as
input to a statistical mathematical analysis that could attempt to
determine the underlying Display Function of the Display System,
yielding one or more quantitative values (metrics) that define how well
the Display System conforms with the Grayscale Standard Display
Function.

In what follows in this and the following annexes, an example of the
latter type of metric analysis is used, in which measured data is
analyzed using a "FIT" test that is intended to validate the shape of
the Characteristic Curve and a "LUM" test that is intended to show the
degree of scatter from the ideal Grayscale Standard Display Function.
This approach has been applied, for example, to quantitatively
demonstrate how improvements were successfully made to the Display
Function of certain Display Systems.

Before proceeding with the description of the methodology of this
specific metric approach, it should be noted that it is offered as one
possible approach, not necessarily as the most appropriate approach for
evaluating all Display Systems. In particular, the following notes
should be considered before selecting or interpreting results from any
particular metric approach.

1. There may be practical issues that limit the number of P-Values that
   can be meaningfully used in the analysis. For example, it may be
   practical to measure all 256 possible Luminances from a fixed
   position on the screen of an 8-bit video monitor, but it may be
   impractical to meaningfully measure all 4096 densities theoretically
   printable by a 12-bit film printer. One reason for the impracticality
   is the limited accuracy of densitometers (or even film digitizers). A
   second reason is that the film density measurements, unlike the CRT
   photometer measurements, are obtained from different locations on the
   display area, so any spatial non-uniformity that is present in the
   film affects the hardcopy measurement. Current hardcopy printers and
   densitometers both have absolute optical density accuracy limitations
   that are significantly worse than the change that would be caused by
   a change in just the least significant bit of a 12-bit P-Value. In
   general, selecting a larger number of P-Values allows, in principle,
   more localized aberrations from the Grayscale Standard Display
   Function to be "caught", but the signal-to-noise ratio (or
   significance) of each of these will be decreased.

2. If the measurement data for a particular Display System has
   significant "noise" (as indicated by limited repeatability in the
   data when multiple sets of measurements are taken), it may be
   desirable to apply a statistical analysis technique that goes beyond
   the "FIT" and "LUM" metric by explicitly utilizing the known standard
   deviations in the input data, along with the data itself, to prevent
   the fitting technique from over-reacting to noise. See, for example,
   the section "General Linear Least Squares" in Reference C1 and the
   chapter "Least-Squares Fit to a Polynomial" in Reference C2. If
   measurement noise is not explicitly taken into account in the
   analysis, the metric's returned root-mean-square error of the data
   points relative to the fit could be misleadingly high, since it would
   include the combined effect of errors due to incorrectness in the
   Display Function and errors due to measurement noise.

3. If possible, the sensitivity and specificity of the metric being
   considered should be checked against visual tests. For example, a
   digital test pattern with many low-contrast steps at many ambient
   Luminances could be printed on a "laboratory standard" Grayscale
   Standard Display Function printer and also printed on a printer being
   evaluated. The resultant films could then be placed side-by-side on
   light-boxes for comparison by a human observer. A good metric
   technique should detect as sensitively and repeatably as the human
   observer the existence of deviations (of any shape) from the
   Grayscale Standard Display Function. For example, if a Display System
   has a Characteristic Curve that, for even a very short interval of
   DDL values, is too contrasty, too flat, or (worse yet) non-monotonic,
   the metric should be able to detect and respond to that anomaly as
   strongly as the human observer does.

4. Finally, in addition to the experimentally encountered
   non-repeatabilities in the data from a Display System, there may be
   reason to consider additional possible causes of variations. For
   example, varying the ordering of P-Values in a test pattern
   (temporally for CRTs, spatially for printers) might affect the
   results. For printers, switching to different media might affect the
   results. A higher confidence can be placed in the results obtained
   from any metric if the results are stable in the presence of any or
   all such changes.

.. _sect_C.2:

Methodology
-----------

**Step (1)**

The Characteristic Curve of the test Display System should be determined
with as many measurements as practical (see `Emissive Display
Systems <#sect_D.1>`__, `Transparent Hardcopy Devices <#sect_D.2>`__,
and `Reflective Display Systems <#sect_D.3>`__). Using the Grayscale
Standard Display Function, the fractional number of JNDs are calculated
for each Luminance interval between equally spaced P-Value steps. The
JNDs/Luminance interval may be calculated directly, or iteratively. For
example, if only a few JNDs belong to every Luminance interval, a linear
interpolation may be performed. After transformation of the grayscale
response of the Display System, the Luminance Levels for every P-Value
are Li and the corresponding Standard Luminance Levels are Lj; dj
specifies the JNDs /Luminance-Interval on the Grayscale Standard Display
Function for the given number of P-Values. Then, the JNDs/Luminance
interval for the transformed Display Function are

.. math:: r = d<subscript>j</subscript>(L<subscript>i+1</subscript> - L<subscript>i</subscript>)(L<subscript>j+1</subscript> + L<subscript>j</subscript>) / ((L<subscript>i+1</subscript> + L<subscript>i</subscript>)(L<subscript>j+1</subscript> - L<subscript>j</subscript>))

Additionally, an iterative method can be used to calculate the number of
JNDs per Luminance interval, requiring only the Grayscale Standard
Display Function that defines a JND step in Luminance given a Luminance
value. This is done by simply counting the number of complete JND steps
in the Luminance interval, and then the remaining fractional step. Start
at the Luminance low end of the interval, and calculate from the
Grayscale Standard Display Function the Luminance step required for one
JND step. Then continue stepping from the low Luminance value to the
high Luminance value in single JND steps, until the Luminance value of
the upper end of the Luminance Range is passed. Calculate the fraction
portion of one JND that this last step represents. the total number of
completed integer JND steps plus the fractional portion of the last
uncompleted step is the fractional number of JND steps in the Luminance
interval.

Plot the number of JNDs per Luminance interval (vertical axis) versus
the index of the Luminance interval (horizontal axis). This curve is
referred to as the *Luminance intervals vs JNDs*\ curve. An example of a
plot of Luminance intervals vs JNDs is shown in figure C-1. The plot is
matched very well by a horizontal line when a linear regression is
applied.

The JNDs/Luminance interval data are evaluated by two statistical
measures [C4]. The first assesses the global match of the test Display
Function with the Grayscale Standard Display Function. The second
measure locally analyses the approximation of the Grayscale Standard
Display Function to the test Display Function.

**Step (2)**

Two related measures of a regression analysis are applied after normal
multiple linear regression assumptions are verified for the data
[C3].The first measure, named the *FIT*\ test, attempts to match the
Luminance-Intervals-vs-JNDs curve of the test Luminance distribution
with different order polynomial fits. The Grayscale Standard Display
Function is characterized by exactly one JND per Luminance interval over
the entire Luminance Range. Therefore, ideally, the data of
JNDs/Luminance intervals vs index of the Luminance interval are best fit
by a horizontal line of a constant number of JNDs/Luminance interval,
indicating that both the local and global means of JNDs/Luminance
interval are constant over the given Luminance Range. If the curve is
better matched by a higher-order curve, the distribution is not closely
approximating the Grayscale Standard Display Function. The regression
analysis should test comparisons through third-order curves.

The second measure, the Luminance uniformity metric (LUM), analyzes
whether the size of Luminance steps are uniform in perceptual size
(i.e., JNDs) across the Luminance Range. This is measured by the Root
Mean Square Error (RMSE) of the curve fit by a horizontal line of the
JNDs/Luminance interval. The smaller the RMSE of the JNDs/Luminance
interval, the more closely the test Display Function approximates the
Grayscale Standard Display Function on a microscopic scale.

Both the FIT and LUM measures can be conveniently calculated on standard
statistical packages.

Assuming the test Luminance distribution passes the FIT test, then the
measure of quality of the distribution is determined by the single
quantitative measurement (LUM) of the standard deviation of the
JNDs/Luminance interval from their mean. Clinical practice is expected
to determine the tolerances for the FIT and LUM values.

An important factor in reaching a close approximation of a test Display
Function to the Grayscale Standard Display Function is the number of
discrete output levels of the Display System. For instance, the LUM
measure can be improved by using only a subset of the available DDLs
while maintaining the full available output digitization resolution at
the cost of decreasing contrast resolution.

While the LUM is influenced by the choice of the number of discrete
output gray levels in the Grayscale Standard Display Function, the
appropriate number of output levels is determined by the clinical
application, including possible gray scale image processing that may
occur independently of the Grayscale Standard Display Function
standardization. Thus, PS3.14 does not prescribe a certain number of
gray levels of output. However, in general, the larger the number of
distinguishable gray levels available, the higher the possible image
quality because the contrast resolution is increased. It is recommended
that the number of necessary output driving levels for the transformed
Display Function be determined prior to standardization of the Display
System (based on clinical applications of the Display System), so that
this information can be used when calculating the transformation in
order to avoid using gray scale distributions with fewer output levels
than needed.

.. _sect_C.3:

References
----------

[C1] Press, William H, et al., Numerical Recipes in C, Cambridge
University Press, 1988, Section "General Linear Least Squares"

[C2] Bevington, Phillip R., Data Reduction and Error Analysis for the
Physical Sciences, McGraw-Hill, 1969, the chapter "Least-Squares Fit to
a Polynomial" .

[C3] Kleinbaum DG, Kupper LL, Muller KE, Applied Regression Analysis and
Other Multivariable Methods, Duxbury Press, 2nd Edition, pp 45-49, 1987.

[C4] Hemminger, B., Muller, K., "Performance Metric for evaluating
conformance of medical image displays with the ACR/NEMA display function
standard", SPIE Medical Imaging 1997, editor Yongmin Kim, vol 3031-25,
1997.

