.. _chapter_XX:

Use Cases for Application Hosting
=================================

.. _sect_XX.1:

Agent-Specific Post Processing
------------------------------

Many metabolic/contrast agents require more than just simple imaging to
provide data for decision making. Rather than just detecting the
presence or absence of the metabolic/contrast agents, calculations based
on relative uptake rates, or decay rates, comparisons with previous or
neighboring data, fusion of data from multiple sources or time points,
etc. may be necessary to properly evaluate image data with these
metabolic/contrast agents. Often the nature of this processing is
closely related to the type of agent, the anatomy, and the disease
process being targeted. The processing may be so specific that the
general-purpose image processing features found on medical imaging
workstations are inadequate to properly perform the procedure. The
effective use of a particular agent for a particular procedure may
depend on having properly tuned, targeted post-processing. Both the
algorithms used, as well as the workflow in performing the analysis, may
be customized for performing procedures with a particular agent.

The stakeholders interested in developing such agent- and exam-specific
post-processing applications may have a vested interest in insuring that
such post-processing applications can run on a wide variety of systems.
The standard post-processing software API outlined in could simplify the
distribution of such agent-specific analysis applications. Rather than
creating multiple versions of the same application, each version
targeted to a particular medical imaging vendor's system, the
application developer need only create a single version of the
application, which would run on any system that implemented the standard
API.

Differences in physical characteristics, acquisition technique and
equipment, and user preference affect image quality and processing
requirements. By allowing the sharing of applications based on
device-independent (or conversely, device-specific) procedures, the
Hosted Application technology will reduce these differences to a
minimum.

.. _sect_XX.2:

Support For Multi-site Collaborative Research
---------------------------------------------

A common API for Application Hosting facilitates multi-site research.

**Site-specific problems**: The development of molecular imaging
applications can be accelerated with multiple site cooperation in the
validation of new algorithms and software. However, the run-time
environment and tools available at one site typically are not matched
identically at other sites, hampering the sharing of applications
between sites. Using the same tools allows them to share applications.
One cannot simply take an application written at one of these sites, and
make it run on the other site without major software work involving the
installation and configuration of multiple tool packages. Even after
installing the needed tools and libraries, software developed at one
site may be trying to access facilities that are unavailable at the
other site, for example, facilities to store, access, and organize the
image data. Often the data formats applications from one site are
expecting are incompatible with the data formats available at other
sites. Having a standard API could help minimize these data
incompatibilities.

**Gap between research and clinical environments**: The initial versions
of agent-specific applications are typically created in a research
environment, and are not easily accessible in the clinical environment.
The early experimental work generally is done by exporting the image
data out of the clinical environment to research workstations, and then
importing the results back into the clinical system once the analysis is
done. While exporting and importing the images may be sufficient for the
early research work, clinical acceptance of an application can be
significant enhanced if that application could run in the same clinical
environment where the images are collected, in order to better fit into
the clinical workflow.

The problem of mismatched run time environments becomes even more acute
when attempting to run the typical research application on a production
clinical workstation. Due to a variety of legal and commercial concerns,
vendors of the systems utilized in the clinical environment generally do
not support running unknown software, nor do most commercial vendors
have the time or resources to assist the hundreds of researchers who may
wish to port a particular application to that vendor's system. Even if
researchers manage to load an experimental program onto a clinical
system, the experimental program rarely has direct access to the data
stored on that clinical system, nor can it directly store results back
into the system's clinical database. Without a single standard
interface, users have to resort to the cumbersome and time-consuming
export and input routines to be able to run research programs on
clinical data. It is expected that the constrained environment that a
standard API provides would be simpler to validate, particularly if it
is universally deployed by multiple vendors, and could lessen the burden
on any individual system vendor.

.. _sect_XX.3:

Screening Applications
----------------------

Computer Aided Diagnosis and Decision Making (CAD) is becoming more
prevalent in radiology departments. Many classes of exams now routinely
go through a computer screening process prior to reading. One potential
barrier to more widespread use of CAD screening is that the various
vendors of CAD applications typically only allow their applications to
run on servers or workstations provided by those companies. A clinical
site that wishes to utilize, for example, mammo CAD from one vendor and
lung CAD from another often is forced to acquire two different servers
or workstations from the two different vendors.

The Hosted Application concept described in could be used to facilitate
the running of multiple CAD applications from multiple vendors on the
same computer system.

.. _sect_XX.4:

Modality-Specific Post Processing
---------------------------------

As medical imaging technology progresses, new modalities are added to
the Standard. For example, vessel wall detection in intravascular
ultrasound is often easier if the images are left in radial form.
Unfortunately, most DICOM workstations would not know how to deal with
images in such a strange format even though the workstation might
recognize that it is an image.

One possible solution is for a workstation to seek out an appropriate
Hosted Application for handling Modalities or SOP classes that it does
not recognize. This would allow for automatic handling of all image
types by a generic imaging platform. Similarly, SOP Classes, even
private SOP Classes, could be created that depend on particular Hosted
Applications to prepare data for display.

.. _sect_XX.5:

Measurement/Evidence Document Creation
--------------------------------------

Another natural use for such a standardized API is the creation of
exam-specific analysis and measurement programs for the creation of
Evidence Documents (Structured Reports). The standardized API would
allow the same analysis program to run on a variety of host systems,
reducing the amount of development needed to support multiple platforms.

.. _sect_XX.6:

CAD Rendering
-------------

Often the regulatory approval for CAD systems includes the method by
which the CAD marks are presented to the user. Providers of CAD systems
have used dedicated workstations for such display in the past in order
to insure that the CAD marks are presented as intended. If there were a
suitable standardized API for launching hosted applications, a Hosted
Application could handle the display of CAD results on any workstation
that supports that standardized API.

