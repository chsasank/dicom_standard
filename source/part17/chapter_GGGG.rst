.. _chapter_GGGG:

Patient Radiation Dose Structured Report Document (Informative)
===============================================================

This Annex contains examples of the use of Patient Radiation Dose
templates within Patient Radiation Dose Structured Report Documents.

.. _sect_GGGG.1:

Skin Dose Map Example
---------------------

The following example shows the report of the skin dose map calculated
from the dose delivered during an X-Ray interventional cardiology
procedure.

The calculation uses a Radiation Dose SR provided by a Single Plane
X-Ray Angiography equipment of the manufacturer "A". The Radiation Dose
SR is created during one procedure step, corresponding to the coronary
stenting of an adult male of 83 kg and 179 cm height.

The skin dose calculations are performed by an application on a
separated workstation of the manufacturer "B", operated by the medical
physicist, who is logged into the workstation at the time of the
creation of the Patient Radiation Dose Structured Report document.

The dose calculation application generates a Patient Radiation Dose
Structured Report document and a Secondary Capture Image containing an
image of the dose distribution over the deployed skin of the patient
model.

The dose calculation application uses the following settings and
assumptions:

-  RDSR Source Data:

   -  All the Irradiation Event UIDs are used in the calculation of the
      skin dose map.

-  Patient Model:

   -  The patient model is a combination of two elliptic cylinders to
      represent the chest and neck of the patient.

   -  The actual dimensions of the model are determined by the age,
      gender, height, and weight of the patient.

   -  In this example the exact height and weight of the patient are
      used to create the model. The resulting elliptic cylinder for the
      chest of the model is 31 cm in the AP dimension and 74 cm in the
      lateral dimension.

   -  The application creates internally a 3D voxelized model that is
      stored in a DICOM SOP Instance.

-  Patient Model Registration:

   -  The distance from the top of the patient's head to the head of the
      table (measured during the procedure) is known. The location of
      the patient head and table head are stored in a Spatial Fiducials
      SOP instance.

   -  The application uses fiducials to register the patient model with
      the data of the source Radiation Dose SR.

   -  A-priori knowledge of the distance from the table head to the
      system Isocenter at table zero position is calibrated offline.

   -  The table tilt, cradle, and rotation angles are ignored because
      the description of the acquisition geometry is incomplete in the
      Radiation Dose SR. Only table translations relative to the
      Isocenter are considered in the calculations.

-  Beam Attenuators:

   -  A-priori knowledge of the model of the table and mattress (i.e.,
      shape, dimensions, and absorption material) is calibrated offline,
      and it is referenced internally by the application. The model
      contains the same coordinate system as the one used in the
      equipment referenced in the Radiation Dose SR, so there is no need
      of another registration SOP instance.

   -  The X-Ray filter information from the source Radiation Dose SR is
      used by the application. There is no other a-priori knowledge of
      the X-Ray filtration.

.. table:: Skin Dose Map Example

   +----------------+----------------+----------------+----------------+
   | **Node**       | **Code Meaning | **Code or      | **Comment**    |
   |                | of Concept     | Example        |                |
   |                | Name**         | Value**        |                |
   +================+================+================+================+
   | 1              | Patient        |                |                |
   |                | Radiation Dose |                |                |
   |                | Report         |                |                |
   +----------------+----------------+----------------+----------------+
   | 1.1            | Language of    | (En, IETF4646, |                |
   |                | Content Item   | "English")     |                |
   |                | and            |                |                |
   |                | Descendants    |                |                |
   +----------------+----------------+----------------+----------------+
   | 1.2            | Observer Type  | (121007, DCM,  |                |
   |                |                | "Device")      |                |
   +----------------+----------------+----------------+----------------+
   | 1.3            | Device         | 1              |                |
   |                | Observer UID   | .2.3.4.566.1.5 |                |
   +----------------+----------------+----------------+----------------+
   | 1.4            | Device         | MedPhys-01     |                |
   |                | Observer Name  |                |                |
   +----------------+----------------+----------------+----------------+
   | 1.5            | Device         | Manufacturer B |                |
   |                | Observer       |                |                |
   |                | Manufacturer   |                |                |
   +----------------+----------------+----------------+----------------+
   | 1.6            | Device         | Dose           |                |
   |                | Observer Model | Workstation v1 |                |
   |                | Name           |                |                |
   +----------------+----------------+----------------+----------------+
   | 1.7            | Observer Type  | (121006, DCM,  |                |
   |                |                | "Person")      |                |
   +----------------+----------------+----------------+----------------+
   | 1.8            | Person         | Do             |                |
   |                | Observer Name  | e^John^^Dr^PhD |                |
   +----------------+----------------+----------------+----------------+
   | 1.9            | Person         | `(C1708969,    |                |
   |                | Observer's     | UMLS, "Medical |                |
   |                | Role in the    | Ph             |                |
   |                | Organization   | ysicist") <htt |                |
   |                |                | ps://uts.nlm.n |                |
   |                |                | ih.gov/metathe |                |
   |                |                | saurus.html?cu |                |
   |                |                | i=C1708969>`__ |                |
   +----------------+----------------+----------------+----------------+
   | 1.10           | Radiation Dose |                |                |
   |                | Estimate       |                |                |
   +----------------+----------------+----------------+----------------+
   | 1.10.1         | Radiation Dose | Skin Dose Map  |                |
   |                | Estimate Name  |                |                |
   +----------------+----------------+----------------+----------------+
   | 1.10.2         | Comment        | Single Plane   |                |
   |                |                | XA             |                |
   +----------------+----------------+----------------+----------------+
   | 1.10.3         | Radiation Dose |                |                |
   |                | Estimate       |                |                |
   |                | Methodology    |                |                |
   +----------------+----------------+----------------+----------------+
   | 1.10.3.1       | SR Instance    |                | Radiation Dose |
   |                | Used           |                | SR #1          |
   +----------------+----------------+----------------+----------------+
   | 1.10.3.1.1     | SOP Class UID  | 1.2.840.1008.5 |                |
   |                |                | .1.4.1.1.88.67 |                |
   +----------------+----------------+----------------+----------------+
   | 1.10.3.1.2     | SOP Instance   | 1.             |                |
   |                | UID            | 2.3.4.566.77.1 |                |
   +----------------+----------------+----------------+----------------+
   | 1.10.3.1.3     | Spatial        |                | Spatial        |
   |                | Fiducials      |                | Fiducials      |
   +----------------+----------------+----------------+----------------+
   | 1.10.3.1.3.1   | SOP Class UID  | 1.2.840.       |                |
   |                |                | 1008.          |                |
   |                |                | 5.1.4.1.1.66.2 |                |
   +----------------+----------------+----------------+----------------+
   | 1.10.3.1.3.2   | SOP Instance   | 1.2.3          |                |
   |                | UID            | .4.44.222.33.1 |                |
   +----------------+----------------+----------------+----------------+
   | 1.10.3.2       | Patient        |                |                |
   |                | Radiation Dose |                |                |
   |                | Model          |                |                |
   +----------------+----------------+----------------+----------------+
   | 1.10.3.2.1     | Patient Model  | (128418, DCM,  |                |
   |                | Type           | "Simple Object |                |
   |                |                | Model")        |                |
   +----------------+----------------+----------------+----------------+
   | 1.10.3.2.2     | Radiation      | (128422, DCM,  |                |
   |                | Transport      | "Voxelized     |                |
   |                | Model Type     | Radiation      |                |
   |                |                | Transport      |                |
   |                |                | Model")        |                |
   +----------------+----------------+----------------+----------------+
   | 1.10.3.2.3     | Patient        |                | Parametric map |
   |                | Radiation Dose |                |                |
   |                | Model Data     |                |                |
   +----------------+----------------+----------------+----------------+
   | 1.10.3.1.3.1   | SOP Class UID  | 1.2.840.100    |                |
   |                |                | 8.5.1.4.1.1.30 |                |
   +----------------+----------------+----------------+----------------+
   | 1.10.3.1.3.2   | SOP Instance   | 1.             |                |
   |                | UID            | 2.3.43.44.55.1 |                |
   +----------------+----------------+----------------+----------------+
   | 1.10.3.2.4     | Patient        | DOI:1.2.3.4    |                |
   |                | Radiation Dose |                |                |
   |                | Model          |                |                |
   |                | Reference      |                |                |
   +----------------+----------------+----------------+----------------+
   | 1.10.3.2.5     | Comment        | Combined       |                |
   |                |                | Elliptic       |                |
   |                |                | Cylinders      |                |
   +----------------+----------------+----------------+----------------+
   | 1.10.3.2.6     | Patient Model  |                |                |
   |                | Demographics   |                |                |
   +----------------+----------------+----------------+----------------+
   | 1.10.3.2.6.1   | Model Minimum  | 18 (a, UCUM,   |                |
   |                | Age            | "year")        |                |
   +----------------+----------------+----------------+----------------+
   | 1.10.3.2.6.2   | Model Maximum  | 90 (a, UCUM,   |                |
   |                | Age            | "year")        |                |
   +----------------+----------------+----------------+----------------+
   | 1.10.3.2.6.3   | Model Patient  | (M, DCM,       |                |
   |                | Sex            | "Male")        |                |
   +----------------+----------------+----------------+----------------+
   | 1.10.3.2.6.4   | Model Minimum  | 83 (kg, UCUM,  |                |
   |                | Weight         | "kilogram")    |                |
   +----------------+----------------+----------------+----------------+
   | 1.10.3.2.6.5   | Model Maximum  | 83 (kg, UCUM,  |                |
   |                | Weight         | "kilogram")    |                |
   +----------------+----------------+----------------+----------------+
   | 1.10.3.2.6.6   | Model Minimum  | 179 (cm, UCUM, |                |
   |                | Height         | "Centimeter")  |                |
   +----------------+----------------+----------------+----------------+
   | 1.10.3.2.6.7   | Model Maximum  | 179 (cm, UCUM, |                |
   |                | Height         | "Centimeter")  |                |
   +----------------+----------------+----------------+----------------+
   | 1.10.3.2.7     | Patient Model  |                |                |
   |                | Registration   |                |                |
   +----------------+----------------+----------------+----------------+
   | 1.10.3.2.7.1   | Comment        | Distance from  |                |
   |                |                | the top of     |                |
   |                |                | patient's head |                |
   |                |                | to the head of |                |
   |                |                | the table = 10 |                |
   |                |                | cm             |                |
   +----------------+----------------+----------------+----------------+
   | 1.10.3.2.7.2   | Registration   | (125022, DCM,  |                |
   |                | Method         | "Fiducial      |                |
   |                |                | Alignment")    |                |
   +----------------+----------------+----------------+----------------+
   | 1.10.3.2.7.3   | Spatial        |                | Spatial        |
   |                | Registration   |                | Registration   |
   +----------------+----------------+----------------+----------------+
   | 1.10.3.1.3.1   | SOP Class UID  | 1.2.840.       |                |
   |                |                | 1008.          |                |
   |                |                | 5.1.4.1.1.66.1 |                |
   +----------------+----------------+----------------+----------------+
   | 1.10.3.1.3.2   | SOP Instance   | 1.2            |                |
   |                | UID            | .3.4.44.3.2.11 |                |
   +----------------+----------------+----------------+----------------+
   | 1.10.3.3       | X-Ray Beam     |                |                |
   |                | Attenuator     |                |                |
   +----------------+----------------+----------------+----------------+
   | 1.10.3.3.1     | Attenuator     | (128459, DCM,  |                |
   |                | Category       | "Table")       |                |
   +----------------+----------------+----------------+----------------+
   | 1.10.3.3.2     | Equivalent     | `(256501007,   |                |
   |                | Attenuator     | SCT, "Carbon   |                |
   |                | Material       | fi             |                |
   |                |                | ber") <http:// |                |
   |                |                | snomed.info/id |                |
   |                |                | /256501007>`__ |                |
   +----------------+----------------+----------------+----------------+
   | 1.10.3.3.3     | Equivalent     | 100 (mm, UCUM, |                |
   |                | Attenuator     | "Millimeter")  |                |
   |                | Thickness      |                |                |
   +----------------+----------------+----------------+----------------+
   | 1.10.3.3.4     | Attenuator     | X-Ray Table    |                |
   |                | Description    | with Mattress  |                |
   +----------------+----------------+----------------+----------------+
   | 1.10.3.3.5     | X-Ray Beam     |                |                |
   |                | Attenuator     |                |                |
   |                | Model          |                |                |
   +----------------+----------------+----------------+----------------+
   | 1.10.3.3.5.1   | Radiation      | (128421, DCM,  |                |
   |                | Transport      | "Geometric     |                |
   |                | Model Type     | Radiation      |                |
   |                |                | Transport      |                |
   |                |                | Model")        |                |
   +----------------+----------------+----------------+----------------+
   | 1.10.3.3.5.2   | X-Ray Beam     | DOI:1.4.2.3    |                |
   |                | Attenuator     |                |                |
   |                | Model          |                |                |
   |                | Reference      |                |                |
   +----------------+----------------+----------------+----------------+
   | 1.10.3.4       | Radiation Dose |                |                |
   |                | Estimate       |                |                |
   |                | Method         |                |                |
   +----------------+----------------+----------------+----------------+
   | 1.10.3.4.1     | Radiation Dose | (128480, DCM,  |                |
   |                | Estimate       | "Analytical    |                |
   |                | Method Type    | Algorithm")    |                |
   +----------------+----------------+----------------+----------------+
   | 1.10.3.4.2     | Radiation Dose |                |                |
   |                | Estimate       |                |                |
   |                | Parameters     |                |                |
   +----------------+----------------+----------------+----------------+
   | 1.10.3.4.2.1   | (128433, DCM,  | 1.06 ({ratio}, |                |
   |                | "Tissue Air    | UCUM, "ratio") |                |
   |                | Ratio")        |                |                |
   +----------------+----------------+----------------+----------------+
   | 1.10.3.4.2.1.1 | Radiation Dose | `(C70774,      |                |
   |                | Estimate       | NCIt, "Unit    |                |
   |                | Parameter Type | Conversion     |                |
   |                |                | Factor"        |                |
   |                |                | ) <https://nci |                |
   |                |                | t.nci.nih.gov/ |                |
   |                |                | ncitbrowser/Co |                |
   |                |                | nceptReport.js |                |
   |                |                | p?dictionary=N |                |
   |                |                | CI_Thesaurus&c |                |
   |                |                | ode=C70774>`__ |                |
   +----------------+----------------+----------------+----------------+
   | 1.10.3.4.2.2   | (128408, DCM,  | 31 (cm, UCUM,  |                |
   |                | "Patient AP    | "Centimeter")  |                |
   |                | Dimension")    |                |                |
   +----------------+----------------+----------------+----------------+
   | 1.10.3.4.2.2.1 | Radiation Dose | (121206, DCM,  |                |
   |                | Estimate       | "Distance")    |                |
   |                | Parameter Type |                |                |
   +----------------+----------------+----------------+----------------+
   | 1.10.3.4.2.3   | (128409, DCM,  | 74 (cm, UCUM,  |                |
   |                | "Patient       | "Centimeter")  |                |
   |                | Lateral        |                |                |
   |                | Dimension")    |                |                |
   +----------------+----------------+----------------+----------------+
   | 1.10.3.4.2.3.1 | Radiation Dose | (121206, DCM,  |                |
   |                | Estimate       | "Distance")    |                |
   |                | Parameter Type |                |                |
   +----------------+----------------+----------------+----------------+
   | 1.10.3.4.2.4   | (MyCode001,    | 0.010536 (/cm, |                |
   |                | 99MyScheme,    | UCUM,          |                |
   |                | "Linear        | "/Centimeter") |                |
   |                | attenuation    |                |                |
   |                | coefficient of |                |                |
   |                | the table and  |                |                |
   |                | mattress")     |                |                |
   +----------------+----------------+----------------+----------------+
   | 1.10.3.4.3     | Radiation Dose | DOI:4.2.13.4   |                |
   |                | Estimate       |                |                |
   |                | Method         |                |                |
   |                | Reference      |                |                |
   +----------------+----------------+----------------+----------------+
   | 1.10.4         | Radiation Dose |                |                |
   |                | Estimate       |                |                |
   |                | Representation |                |                |
   +----------------+----------------+----------------+----------------+
   | 1.10.4.1       | Distribution   | (128485, DCM,  |                |
   |                | Representation | "Skin Dose     |                |
   |                |                | Map")          |                |
   +----------------+----------------+----------------+----------------+
   | 1.10.4.2       | Radiation Dose |                |                |
   |                | Representation |                |                |
   |                | Data           |                |                |
   +----------------+----------------+----------------+----------------+
   | 1.10.4.2.1     | SOP Class UID  | 1.2.840.100    | Secondary      |
   |                |                | 08.5.1.4.1.1.7 | Capture        |
   +----------------+----------------+----------------+----------------+
   | 1.10.4.2.2     | SOP Instance   | 1.2.3.1.2.3.3  |                |
   |                | UID            |                |                |
   +----------------+----------------+----------------+----------------+
   | 1.10.4.3       | Organ          | `(181469002,   |                |
   |                |                | SCT,           |                |
   |                |                | "S             |                |
   |                |                | kin") <http:// |                |
   |                |                | snomed.info/id |                |
   |                |                | /181469002>`__ |                |
   +----------------+----------------+----------------+----------------+
   | 1.10.4.4       | Comment        | 2D map of the  |                |
   |                |                | dose on the    |                |
   |                |                | deployed skin  |                |
   +----------------+----------------+----------------+----------------+
   | 1.10.5         | Organ          |                |                |
   |                | Radiation Dose |                |                |
   |                | Information    |                |                |
   +----------------+----------------+----------------+----------------+
   | 1.10.5.1       | Organ          | `(181469002,   |                |
   |                |                | SCT,           |                |
   |                |                | "S             |                |
   |                |                | kin") <http:// |                |
   |                |                | snomed.info/id |                |
   |                |                | /181469002>`__ |                |
   +----------------+----------------+----------------+----------------+
   | 1.10.5.2       | Comment        | Skin in the    |                |
   |                |                | area of the    |                |
   |                |                | chest and neck |                |
   +----------------+----------------+----------------+----------------+
   | 1.10.5.3       | (DCM, 128531,  | 3000 (mGy,     |                |
   |                | "Maximum       | UCUM, "mGy")   |                |
   |                | Absorbed       |                |                |
   |                | Radiation      |                |                |
   |                | Dose")         |                |                |
   +----------------+----------------+----------------+----------------+
   | 1.10.5.3.1     | `(371884006,   | 750 (mGy,      |                |
   |                | SCT, "+/-,     | UCUM, "mGy")   |                |
   |                | range of       |                |                |
   |                | measurement    |                |                |
   |                | uncertai       |                |                |
   |                | nty") <http:// |                |                |
   |                | snomed.info/id |                |                |
   |                | /371884006>`__ |                |                |
   +----------------+----------------+----------------+----------------+
   | 1.11           | Comment        | Skin Dose Map  |                |
   |                |                | Report         |                |
   +----------------+----------------+----------------+----------------+

.. _sect_GGGG.2:

Dual-source CT Organ Radiation Dose Example
-------------------------------------------

The following example shows the report of the organ dose calculated for
a dual-source CT scan.

The calculation uses a Radiation Dose SR provided by a CT system that
has dual X-Ray tubes. The Radiation Dose SR is created during the
acquisition of Neck DE_CAROTID CT scan of an adult male of 75 kg and 165
cm height.

The dose calculations are performed on the CT system. The dose
calculation application generates a Patient Radiation Dose Structured
Report document and a Dose Point Cloud containing an image of the dose
distribution for the patient model.

The dose calculation application uses the following settings and
assumptions:

-  RDSR Source Data:

   -  The Irradiation Events associated with the CT Localizer Radiograph
      are excluded.

   -  The Irradiation Event UID from the helical CT series is used in
      the calculation of the organ dose.

-  Patient Model:

   -  The patient model is a stylized anthropomorphic model of the
      patient.

   -  Organs are represented by simple geometric shapes described by
      mathematical equations. The parameters of the equations describing
      the location, shape, and dimension of the organs are stored in a
      DICOM SOP Instance.

   -  In this example the gender and age of the patient are used to
      select the appropriate phantom from the existing phantom library.

-  Patient Model Registration:

   -  Image Content-based Alignment between the CT images Frame of
      Reference and the 3D stylized model Frame of Reference is used for
      registration.

-  Beam Attenuators:

   -  Additional Aluminum filtration is used in the methodology and the
      equivalent HVL for the scanner model used in the method is given.

.. table:: Dual-source CT Organ Radiation Dose Example

   +---------------+----------------+----------------+----------------+
   | **Node**      | **Code Meaning | **Code or      | **Comment**    |
   |               | of Concept     | Example        |                |
   |               | Name**         | Value**        |                |
   +===============+================+================+================+
   | 1             | Patient        |                |                |
   |               | Radiation Dose |                |                |
   |               | Report         |                |                |
   +---------------+----------------+----------------+----------------+
   | 1.1           | Language of    | (En, IETF4646, |                |
   |               | Content Item   | "English")     |                |
   |               | and            |                |                |
   |               | Descendants    |                |                |
   +---------------+----------------+----------------+----------------+
   | 1.1.1         | Country of     | (CA,           |                |
   |               | Language       | ISO3166_1,     |                |
   |               |                | "Canada")      |                |
   +---------------+----------------+----------------+----------------+
   | 1.2           | Observer Type  | (121007, DCM,  |                |
   |               |                | "Device")      |                |
   +---------------+----------------+----------------+----------------+
   | 1.3           | Device         | 2              |                |
   |               | Observer UID   | .13.4.5.2.33.5 |                |
   +---------------+----------------+----------------+----------------+
   | 1.4           | Device         | RUMC-213       |                |
   |               | Observer Name  |                |                |
   +---------------+----------------+----------------+----------------+
   | 1.5           | Device         | Manufacturer   |                |
   |               | Observer       | DEX            |                |
   |               | Manufacturer   |                |                |
   +---------------+----------------+----------------+----------------+
   | 1.6           | Device         | Scanner 4500   |                |
   |               | Observer Model |                |                |
   |               | Name           |                |                |
   +---------------+----------------+----------------+----------------+
   | 1.7           | Radiation Dose |                |                |
   |               | Estimate       |                |                |
   +---------------+----------------+----------------+----------------+
   | 1.7.1         | Radiation Dose | Dual-source    |                |
   |               | Estimate Name  | Neck           |                |
   |               |                | DE_CAROTID CT  |                |
   |               |                | scan Tube A&B  |                |
   +---------------+----------------+----------------+----------------+
   | 1.7.2         | Comment        | Tube A and B   |                |
   |               |                | combined       |                |
   +---------------+----------------+----------------+----------------+
   | 1.7.3         | Radiation Dose |                |                |
   |               | Estimation     |                |                |
   |               | Methodology    |                |                |
   +---------------+----------------+----------------+----------------+
   | 1.7.3.1       | SR Instance    |                |                |
   |               | Used           |                |                |
   +---------------+----------------+----------------+----------------+
   | 1.10.3.1      | SR Instance    |                | Radiation Dose |
   |               | Used           |                | SR             |
   +---------------+----------------+----------------+----------------+
   | 1.10.3.1.1    | SOP Class UID  | 1.2.840.1008.5 |                |
   |               |                | .1.4.1.1.88.67 |                |
   +---------------+----------------+----------------+----------------+
   | 1.10.3.1.2    | SOP Instance   | 1.             |                |
   |               | UID            | 2.3.4.566.77.1 |                |
   +---------------+----------------+----------------+----------------+
   | 1.7.3.1.1     | Event UID Used | 1              |                |
   |               |                | .3.12.2.xxxxxx |                |
   +---------------+----------------+----------------+----------------+
   | 1.7.3.2       | Patient        |                |                |
   |               | Radiation Dose |                |                |
   |               | Model          |                |                |
   +---------------+----------------+----------------+----------------+
   | 1.7.3.2.1     | Patient Model  | (128404, DCM,  |                |
   |               | Type           | "A             |                |
   |               |                | nthropomorphic |                |
   |               |                | Model")        |                |
   +---------------+----------------+----------------+----------------+
   | 1.7.3.2.2     | Radiation      | (128421, DCM,  |                |
   |               | Transport      | "Geometric     |                |
   |               | Model Type     | Radiation      |                |
   |               |                | Transport      |                |
   |               |                | Model")        |                |
   +---------------+----------------+----------------+----------------+
   | 1.7.3.2.3     | Patient        | < UID of       |                |
   |               | Radiation Dose | "Patient       |                |
   |               | Model Data     | Radiation Dose |                |
   |               |                | Model Data">   |                |
   +---------------+----------------+----------------+----------------+
   | 1.7.3.2.3     | Patient        |                | Parametric map |
   |               | Radiation Dose |                |                |
   |               | Model Data     |                |                |
   +---------------+----------------+----------------+----------------+
   | 1.7.3.2.3.1   | SOP Class UID  | 1.2.840.100    |                |
   |               |                | 8.5.1.4.1.1.30 |                |
   +---------------+----------------+----------------+----------------+
   | 1.7.3.2.3.2   | SOP Instance   | 1.2.5.4.6.677  |                |
   |               | UID            |                |                |
   +---------------+----------------+----------------+----------------+
   | 1.7.3.2.4     | Patient        | Cristy et al.  |                |
   |               | Radiation Dose | 1987           |                |
   |               | Model          |                |                |
   |               | Reference      |                |                |
   +---------------+----------------+----------------+----------------+
   | 1.7.3.2.5     | Patient Model  |                |                |
   |               | Demographics   |                |                |
   +---------------+----------------+----------------+----------------+
   | 1.7.3.2.5.1   | Model Minimum  | 18 (a, UCUM,   |                |
   |               | Age            | "year")        |                |
   +---------------+----------------+----------------+----------------+
   | 1.7.3.2.5.2   | Model Maximum  | 18 (a, UCUM,   |                |
   |               | Age            | "year")        |                |
   +---------------+----------------+----------------+----------------+
   | 1.7.3.2.5.3   | Model Patient  | (M, DCM,       |                |
   |               | Sex            | "Male")        |                |
   +---------------+----------------+----------------+----------------+
   | 1.7.3.2.5.4   | Model Minimum  | 75 (kg, UCUM,  |                |
   |               | Weight         | "kilogram")    |                |
   +---------------+----------------+----------------+----------------+
   | 1.7.3.2.5.5   | Model Maximum  | 75 (kg, UCUM,  |                |
   |               | Weight         | "kilogram")    |                |
   +---------------+----------------+----------------+----------------+
   | 1.7.3.2.5.6   | Model Minimum  | 165 (cm, UCUM, |                |
   |               | Height         | "Centimeter")  |                |
   +---------------+----------------+----------------+----------------+
   | 1.7.3.2.5.7   | Model Maximum  | 165 (cm, UCUM, |                |
   |               | Height         | "Centimeter")  |                |
   +---------------+----------------+----------------+----------------+
   | 1.7.3.2.6     | Patient Model  |                |                |
   |               | Registration   |                |                |
   +---------------+----------------+----------------+----------------+
   | 1.7.3.2.6.1   | Registration   | (125024, DCM,  |                |
   |               | Method         | "Image         |                |
   |               |                | Content-based  |                |
   |               |                | Alignment")    |                |
   +---------------+----------------+----------------+----------------+
   | 1.7.3.2.6.2   | Spatial        | <UID of        |                |
   |               | Registration   | "Spatial       |                |
   |               |                | Registration"> |                |
   +---------------+----------------+----------------+----------------+
   | 1.7.3.2.6.2.1 | SOP Class UID  | 1.2.840.       |                |
   |               |                | 1008.          |                |
   |               |                | 5.1.4.1.1.66.1 |                |
   +---------------+----------------+----------------+----------------+
   | 1.7.3.2.6.2.2 | SOP Instance   | 1.4            |                |
   |               | UID            | .9.87.11.223.5 |                |
   +---------------+----------------+----------------+----------------+
   | 1.7.3.3       | X-Ray Beam     |                |                |
   |               | Attenuator     |                |                |
   +---------------+----------------+----------------+----------------+
   | 1.7.3.3.1     | Attenuator     | (113771, DCM,  |                |
   |               | Category       | "X-Ray         |                |
   |               |                | Filters")      |                |
   +---------------+----------------+----------------+----------------+
   | 1.7.3.3.2     | Equivalent     | `(12503006,    |                |
   |               | Attenuator     | SCT,           |                |
   |               | Material       | "Alum          |                |
   |               |                | inum") <http:/ |                |
   |               |                | /snomed.info/i |                |
   |               |                | d/12503006>`__ |                |
   +---------------+----------------+----------------+----------------+
   | 1.7.3.3.3     | Equivalent     | 1.4 (mm, UCUM, |                |
   |               | Attenuator     | "Millimeter")  |                |
   |               | Thickness      |                |                |
   +---------------+----------------+----------------+----------------+
   | 1.7.3.3.4     | Attenuator     | Mean           |                |
   |               | Description    | equivalent     |                |
   |               |                | Aluminum       |                |
   |               |                | thickness of   |                |
   |               |                | bowtie filter  |                |
   +---------------+----------------+----------------+----------------+
   | 1.7.3.3.5     | X-Ray Beam     |                |                |
   |               | Attenuator     |                |                |
   |               | Model          |                |                |
   +---------------+----------------+----------------+----------------+
   | 1.7.3.3.5.1   | Radiation      | (128421, DCM,  |                |
   |               | Transport      | "Geometric     |                |
   |               | Model Type     | Radiation      |                |
   |               |                | Transport      |                |
   |               |                | Model")        |                |
   +---------------+----------------+----------------+----------------+
   | 1.7.3.4       | Radiation Dose |                |                |
   |               | Estimate       |                |                |
   |               | Method         |                |                |
   +---------------+----------------+----------------+----------------+
   | 1.7.3.4.1     | Radiation Dose | `(D009010,     |                |
   |               | Estimate       | MSH, "Monte    |                |
   |               | Method Type    | Carlo          |                |
   |               |                | ") <http://bio |                |
   |               |                | portal.bioonto |                |
   |               |                | logy.org/ontol |                |
   |               |                | ogies/MESH?p=c |                |
   |               |                | lasses&concept |                |
   |               |                | id=D009010>`__ |                |
   +---------------+----------------+----------------+----------------+
   | 1.7.3.4.2     | Radiation Dose |                |                |
   |               | Estimate       |                |                |
   |               | Parameters     |                |                |
   +---------------+----------------+----------------+----------------+
   | 1.7.3.4.2.1   | (111634, DCM,  | 8.5 (mm, UCUM, |                |
   |               | "Half Value    | "Millimeter")  |                |
   |               | Layer")        |                |                |
   +---------------+----------------+----------------+----------------+
   | 1.7.3.4.3     | Radiation Dose | Simulation     |                |
   |               | Estimate       | package XX     |                |
   |               | Method         | version YY     |                |
   |               | Reference      |                |                |
   +---------------+----------------+----------------+----------------+
   | 1.7.4         | Radiation Dose |                |                |
   |               | Estimate       |                |                |
   |               | Representation |                |                |
   +---------------+----------------+----------------+----------------+
   | 1.7.4.1       | Distribution   | (128496, DCM,  |                |
   |               | Representation | "Dose Point    |                |
   |               |                | Cloud")        |                |
   +---------------+----------------+----------------+----------------+
   | 1.7.4.2       | Radiation Dose |                |                |
   |               | Representation |                |                |
   |               | Data           |                |                |
   +---------------+----------------+----------------+----------------+
   | 1.7.3.2.3.1   | SOP Class UID  | 1.2.840.100    | Parametric Map |
   |               |                | 8.5.1.4.1.1.30 |                |
   +---------------+----------------+----------------+----------------+
   | 1.7.3.2.3.2   | SOP Instance   | 1              |                |
   |               | UID            | .87.2.3.4.11.3 |                |
   +---------------+----------------+----------------+----------------+
   | 1.7.4.3       | Organ          | `(38266002,    |                |
   |               |                | SCT, "Entire   |                |
   |               |                | Body") <http:/ |                |
   |               |                | /snomed.info/i |                |
   |               |                | d/38266002>`__ |                |
   +---------------+----------------+----------------+----------------+
   | 1.7.5         | Organ          |                |                |
   |               | Radiation Dose |                |                |
   |               | Information    |                |                |
   +---------------+----------------+----------------+----------------+
   | 1.7.5.1       | Organ          | `(39607008,    |                |
   |               |                | SCT,           |                |
   |               |                | "              |                |
   |               |                | Lung") <http:/ |                |
   |               |                | /snomed.info/i |                |
   |               |                | d/39607008>`__ |                |
   +---------------+----------------+----------------+----------------+
   | 1.7.5.1.1     | (DCM,128533,   | 9.6 (mGy,      |                |
   |               | "Mean Absorbed | UCUM, "mGy")   |                |
   |               | Radiation      |                |                |
   |               | Dose")         |                |                |
   +---------------+----------------+----------------+----------------+

