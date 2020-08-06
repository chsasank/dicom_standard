.. _chapter_6:

Purpose of An Application Profile
=================================

An Application Profile is a mechanism for selecting an appropriate set
of choices from the parts of DICOM for the support of a particular media
interchange application. Application Profiles for commonly used
interchange scenarios, such as inter-institutional exchange of X-Ray
cardiac angiographic examinations, or printing ultrasound studies from
recordable media, are meant to use the flexibility offered by DICOM
without resulting in so many media and format choices that interchange
is compromised.

Media interchange applications claim conformance to one or more Media
Storage Application Profiles. Two implementations that conform to
identical Application Profiles and support complementary File-set roles
(e.g., an FSC interchanging media with an FSR) are able to exchange SOP
Instances (pieces of DICOM information) on recorded media within the
context of those Application Profiles.

A DICOM Application Profile specifies:

a. which SOP Classes and options must be supported, including any
   required extensions, specializations, or privatizations

b. for each SOP Class, which Transfer Syntaxes may be used

c. what information should be included in the Basic Directory IOD

d. which Media Storage Service Class options may be utilized

e. which roles an application may take: File-set Creator, File-set
   Reader, and/or File-set Updater

f. which physical media and corresponding media formats must be
   supported

g. whether or not the DICOM Files in the File-set shall be Secure DICOM
   Files

h. which Media Storage Security Profile must be used for the creation of
   Secure DICOM Files

and any additional conformance requirements.

The result of making the necessary choices means that the Application
Profile can be thought of as a vertical path through the various parts
of DICOM that begins with choices of information to be exchanged and
ends at the physical medium. `figure_title <#figure_6-1>`__ shows the
relationship between the concepts used in an Application Profile and the
parts of DICOM.

An Application Profile is organized into the following major parts:

a. The name of the Application Profile, or the list of Application
   Profiles grouped in a related class

b. A description of the clinical context of the Application Profile

c. The definition of the Media Storage Service Class with the device
   Roles for the Application Profile and associated options

d. Informative section describing the operational requirements of the
   Application Profile

e. Specification of the SOP Classes and associated IODs supported and
   the Transfer Syntaxes to be used

f. The selection of Media Format and Physical Media to be used

g. If the Directory Information Module is used, the description of the
   minimum subset of the Information Model required

h. Other parameters that need to be specified to ensure interoperable
   media interchange

i. Security parameters that select the cryptographic techniques to be
   used with Secure Media Storage Application Profiles

The structure of DICOM and the design of the Application Profile
mechanism is such that extension to additional SOP Classes and new
exchange media is straightforward.

