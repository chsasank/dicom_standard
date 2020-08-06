.. _chapter_MMMM:

Performed Imaging Agent Administration Structured Report (Informative)
======================================================================

This Annex describes the use of Imaging Agent Administration Structured
Report objects.

.. _sect_MMMM.1:

Performed Imaging Agent Administration Structured Report
--------------------------------------------------------

This Section contains examples for use cases involving contrast imaging
of a single patient in CT system.

In the basic use case:

-  Patient was scheduled by RIS system with a study UID and accession
   number.

-  An Injection procedure for the study was described by an IAASR plan
   object.

-  Patient suffers from insufficient renal function, so intravenous
   (i.v.) contrast agents were dissolved to achieve necessary volumes.

-  Before i.v. contrast was administered a 10 mg Prednisone injection
   was given to the patient.

-  After connecting the patient to the injection system, a patency test
   injection was done. (The injection system does not record detailed
   graph information of this.)

-  "Keep vein open" was activated at a rate of 1 ml per minute.

-  The Requested Procedure was a CT abdominal study with both i.v. and
   oral contrast administration.

   -  Oral contrast media OralContrastofin was diluted to 25:1000 as
      given in the drug usage description. 1000 ml of oral contrast
      media was given 2 hours in advance of the procedure. (Preparation
      of 1000 ml solution uses 24.4 ml contrast and 975.6 ml water)

   -  Test bolus and Imaging injection phase was done at 3 ml/s and were
      followed by a 30 ml flush at the same flow rate.

   -  Before the diagnostic injection, a test bolus of 10 ml undiluted
      ContrastStuff 370 contrast was given, in order to determine scan
      delay time for the diagnostic injection.

   -  Finally 88 ml i.v. contrast media ContrastStuff 370 (corresponding
      to 0.5 g iodine / kg body weight for a 65 kg person) was given
      during imaging. Due to the high viscosity of the contrast and
      renal insufficiency of the patient, ContrastStuff 370 was diluted
      1:1 with 88 ml flush on the fly during injection.

The content tree structure would resemble:

+---------------+----------------+----------------+----------------+
| **Node**      | **Code Meaning | **Code Meaning | **Reference to |
|               | of Concept     | or Example     | TID/ CID/      |
|               | Name**         | Value**        | Comments**     |
+===============+================+================+================+
| 1             | Performed      |                |                |
|               | Imaging Agent  |                |                |
|               | Administration |                |                |
+---------------+----------------+----------------+----------------+
| 1.1           | Language of    | English        |                |
|               | Content Item   |                |                |
|               | and            |                |                |
|               | Descendants    |                |                |
+---------------+----------------+----------------+----------------+
| 1.1.1         | Country of     | United States  |                |
|               | Language       |                |                |
+---------------+----------------+----------------+----------------+
| 1.2           | Observer Type  | Person         |                |
+---------------+----------------+----------------+----------------+
| 1.3           | Person         | Doe^Jane       |                |
|               | Observer Name  |                |                |
+---------------+----------------+----------------+----------------+
| 1.4           | Observer Type  | Device         | Since Observer |
|               |                |                | Type is Device |
+---------------+----------------+----------------+----------------+
| 1.5           | Device         | 1.2.           |                |
|               | Observer UID   | 3.4.47110815.1 |                |
+---------------+----------------+----------------+----------------+
| 1.6           | Device         | Injector       |                |
|               | Observer       | Corporation    |                |
|               | Manufacturer   |                |                |
+---------------+----------------+----------------+----------------+
| 1.7           | Device         | XYZ INJECTOR   |                |
|               | Observer Model |                |                |
|               | Name           |                |                |
+---------------+----------------+----------------+----------------+
| 1.8           | Device         | 1234567890     |                |
|               | Observer       |                |                |
|               | Serial Number  |                |                |
+---------------+----------------+----------------+----------------+
| 1.9           | Station AE     | XYZINJAET      |                |
|               | Title          |                |                |
+---------------+----------------+----------------+----------------+
| 1.10          | Procedure      | 1.2.           | Defaults to    |
|               | Study Instance | 3.4.47110815.2 | Study Instance |
|               | UID            |                | UID            |
|               |                |                | (0020,000D) of |
|               |                |                | General Study  |
|               |                |                | Module         |
+---------------+----------------+----------------+----------------+
| 1.11          | Accession      | 123456789      | Defaults to    |
|               | Number         |                | (0008,0050)    |
+---------------+----------------+----------------+----------------+
| 1.12          | Medication     |                |                |
|               | given          |                |                |
+---------------+----------------+----------------+----------------+
| 1.12.1        | Route of       | (47625008,     |                |
|               | administration | SCT,           |                |
|               |                | "Intravenous   |                |
|               |                | route")        |                |
+---------------+----------------+----------------+----------------+
| 1.12.2        | Mixture        |                |                |
+---------------+----------------+----------------+----------------+
| 1.12.2.1      | Drug           | Prednisone     | row 7          |
|               | administered   |                |                |
+---------------+----------------+----------------+----------------+
| 1.12.2..2     | Medication     | (130259, DCM,  |                |
|               | Type           | "Contrast      |                |
|               |                | Reaction       |                |
|               |                | Prophylactic   |                |
|               |                | Agent")        |                |
+---------------+----------------+----------------+----------------+
| 1.12.2.3      | Dosage         | 2 ml           | (Units)        |
+---------------+----------------+----------------+----------------+
| 1.12.2.4      | Concentration  | 5 mg/ml        | (Units)        |
+---------------+----------------+----------------+----------------+
| 1.13          | Patient        |                |                |
|               | C              |                |                |
|               | haracteristics |                |                |
+---------------+----------------+----------------+----------------+
| 1.13.1        | Patient State  | (414417004,    |                |
|               |                | SCT, "History  |                |
|               |                | of renal       |                |
|               |                | failure")      |                |
+---------------+----------------+----------------+----------------+
| 1.13.2        | Subject Age    | 25             | UNITS=EV (a,   |
|               |                |                | UCUM, "year")  |
+---------------+----------------+----------------+----------------+
| 1.13.3        | Subject Sex    | (M, DCM,       |                |
|               |                | "Male")        |                |
+---------------+----------------+----------------+----------------+
| 1.13.4        | Patient Height | 175            | UNITS=EV (cm,  |
|               |                |                | UCUM, "cm")    |
+---------------+----------------+----------------+----------------+
| 1.13.5        | Patient Weight | 65             | UNITS=EV (kg,  |
|               |                |                | UCUM, "kg")    |
+---------------+----------------+----------------+----------------+
| 1.13.6        | Body Mass      | 21.23          | UNITS=EV       |
|               | Index          |                | (kg/m2, UCUM,  |
|               |                |                | "kg/m2")       |
+---------------+----------------+----------------+----------------+
| 1.13.6.1      | Equation       | (122265, DCM,  |                |
|               |                | "BMI=Wt/Ht^2") |                |
+---------------+----------------+----------------+----------------+
| 1.13.7        | Serum          | 2.7            | UNITS=DT       |
|               | Creatinine     |                | (mg/dl, UCUM,  |
|               |                |                | "mg/dl")       |
+---------------+----------------+----------------+----------------+
| 1.13.8        | Glomerular     | 38             | UNITS=DT       |
|               | Filtration     |                | (ml            |
|               | Rate           |                | /min{1.73_m2}, |
|               |                |                | UCUM,          |
|               |                |                | "m             |
|               |                |                | l/min/1.73m2") |
+---------------+----------------+----------------+----------------+
| 1.13.8.1      | Measurement    | (113570, DCM,  |                |
|               | Method         | "              |                |
|               |                | Cockroft-Gault |                |
|               |                | Formula        |                |
|               |                | estimation of  |                |
|               |                | GFR")          |                |
+---------------+----------------+----------------+----------------+
| 1.13.8.2      | Equivalent     | (33914-3, LN,  |                |
|               | meaning of     | "Glomerular    |                |
|               | concept name   | Filtration     |                |
|               |                | Rate (MDRD)")  |                |
+---------------+----------------+----------------+----------------+
| 1.14          | Imaging Agent  |                |                |
|               | Information    |                |                |
+---------------+----------------+----------------+----------------+
| 1.14.1        | Imaging Agent  | INJECTOR_      |                |
|               | Identifier     | CONTRAST_AGENT |                |
+---------------+----------------+----------------+----------------+
| 1.14.2        | Imaging Agent  | (373066001,    |                |
|               | Warmed         | SCT, "Yes")    |                |
+---------------+----------------+----------------+----------------+
| 1.14.3        | Imaging Agent  |                |                |
|               | Component      |                |                |
|               | Usage          |                |                |
+---------------+----------------+----------------+----------------+
| 1.14.3.1      | Imaging Agent  |                |                |
|               | Component      |                |                |
+---------------+----------------+----------------+----------------+
| 1.14.3.1.1    | Drug           | (353903006,    |                |
|               | administered   | SCT,           |                |
|               |                | "Iopromide")   |                |
+---------------+----------------+----------------+----------------+
| 1.14.3.1.2    | Active         | (44588005,     |                |
|               | Ingredient     | SCT, "Iodine") |                |
+---------------+----------------+----------------+----------------+
| 1.14.3.1.3    | Concentration  | 370            | UNITS = EV     |
|               |                |                | (mg/ml,        |
|               |                |                | "UCUM",        |
|               |                |                | "mg/ml")       |
+---------------+----------------+----------------+----------------+
| 1.14.3.1.4    | Osmolality at  | 770            | UNITS=EV       |
|               | 37C            |                | (mosm/kg,      |
|               |                |                | UCUM,          |
|               |                |                | "mosm/kg")     |
+---------------+----------------+----------------+----------------+
| 1.14.3.1.5    | Viscosity at   | 10             | UNITS = EV     |
|               | 37C            |                | (cP, "UCUM",   |
|               |                |                | "centi Poise") |
+---------------+----------------+----------------+----------------+
| 1.14.3.1.6    | Unit of        | (68276009,     |                |
|               | Presentation   | SCT, "Bottle") |                |
+---------------+----------------+----------------+----------------+
| 1.14.3.1.7    | Imaging Agent  | 500            | UNITS=EV (ml,  |
|               | Volume Per     |                | UCUM, "ml")    |
|               | Unit of        |                |                |
|               | Presentation   |                |                |
+---------------+----------------+----------------+----------------+
| 1.14.3.1.8    | Medical        | 20190301       |                |
|               | Product        |                |                |
|               | Expiration     |                |                |
|               | Date           |                |                |
+---------------+----------------+----------------+----------------+
| 1.14.3.1.9    | Manufacturer   | ContrastMed    |                |
|               | Name           | Corp           |                |
+---------------+----------------+----------------+----------------+
| 1.14.3.1.10   | Brand Name     | ContrastStuff  |                |
|               |                | 370            |                |
+---------------+----------------+----------------+----------------+
| 1.14.3.1.11   | Barcode Value  | -07363935      | PZN number     |
+---------------+----------------+----------------+----------------+
| 1.14.3.1.12   | Lot Identifier | 4B17010        |                |
+---------------+----------------+----------------+----------------+
| 1.14.3.2      | Component      | 97.84          | UNITS=EV (ml,  |
|               | Volume         |                | UCUM, "ml")    |
+---------------+----------------+----------------+----------------+
| 1.15          | Imaging Agent  |                |                |
|               | Information    |                |                |
+---------------+----------------+----------------+----------------+
| 1.15.1        | Imaging Agent  | INJECT         |                |
|               | Identifier     | OR_FLUSH_AGENT |                |
+---------------+----------------+----------------+----------------+
| 1.15.2        | Imaging Agent  | (373066001,    |                |
|               | Warmed         | SCT, "Yes")    |                |
+---------------+----------------+----------------+----------------+
| 1.15.3        | Imaging Agent  |                |                |
|               | Component      |                |                |
|               | Usage          |                |                |
+---------------+----------------+----------------+----------------+
| 1.15.3.1      | Imaging Agent  |                |                |
|               | Component      |                |                |
+---------------+----------------+----------------+----------------+
| 1.15.3.1.1    | Drug           | (262003004,    |                |
|               | administered   | SCT, "Saline") |                |
+---------------+----------------+----------------+----------------+
| 1.15.3.1.2    | Unit of        | (68276009,     |                |
|               | Presentation   | SCT, "Bottle") |                |
+---------------+----------------+----------------+----------------+
| 1.15.3.1.3    | Imaging Agent  | 500            | UNITS=EV (ml,  |
|               | Volume Per     |                | UCUM, "ml")    |
|               | Unit of        |                |                |
|               | Presentation   |                |                |
+---------------+----------------+----------------+----------------+
| 1.15.3.1.4    | Manufacturer   | Saline Water   |                |
|               | Name           | Corp           |                |
+---------------+----------------+----------------+----------------+
| 1.15.3.1.5    | Brand Name     | Isotonic       |                |
|               |                | N              |                |
|               |                | atriumchloride |                |
|               |                | Solution       |                |
+---------------+----------------+----------------+----------------+
| 1.15.3.1.6    | Barcode Value  | -00854309      | PZN number     |
+---------------+----------------+----------------+----------------+
| 1.15.3.1.7    | Lot Identifier | 13CQ4857       |                |
+---------------+----------------+----------------+----------------+
| 1.15.3.2      | Component      | 200            | UNITS=EV (ml,  |
|               | Volume         |                | UCUM, "ml")    |
+---------------+----------------+----------------+----------------+
| 1.16          | Imaging Agent  |                |                |
|               | Information    |                |                |
+---------------+----------------+----------------+----------------+
| 1.16.1        | Imaging Agent  | ORAL_          |                |
|               | Identifier     | CONTRAST_AGENT |                |
+---------------+----------------+----------------+----------------+
| 1.16.2        | Imaging Agent  | (373067005,    |                |
|               | Warmed         | SCT, "No")     |                |
+---------------+----------------+----------------+----------------+
| 1.16.3        | Imaging Agent  |                |                |
|               | Component      |                |                |
|               | Usage          |                |                |
+---------------+----------------+----------------+----------------+
| 1.16.3.1      | Imaging Agent  |                |                |
|               | Component      |                |                |
+---------------+----------------+----------------+----------------+
| 1.16.3.1.1    | Drug           | (47192000,     |                |
|               | administered   | SCT,           |                |
|               |                | "Meglumine     |                |
|               |                | diatrizoate")  |                |
+---------------+----------------+----------------+----------------+
| 1.16.3.1.2    | Active         | (44588005,     |                |
|               | Ingredient     | SCT, "Iodine") |                |
+---------------+----------------+----------------+----------------+
| 1.16.3.1.3    | Concentration  | 370            | UNITS = EV     |
|               |                |                | (mg/ml,        |
|               |                |                | "UCUM",        |
|               |                |                | "mg/ml")       |
+---------------+----------------+----------------+----------------+
| 1.16.3.1.4    | Viscosity at   | 8.9            | UNITS = EV     |
|               | 37C            |                | (cP, "UCUM",   |
|               |                |                | "centiPoise")  |
+---------------+----------------+----------------+----------------+
| 1.16.3.1.5    | Unit of        | (68276009,     |                |
|               | Presentation   | SCT, "Bottle") |                |
+---------------+----------------+----------------+----------------+
| 1.16.3.1.6    | Imaging Agent  | 100            | UNITS=EV (ml,  |
|               | Volume Per     |                | UCUM, "ml")    |
|               | Unit of        |                |                |
|               | Presentation   |                |                |
+---------------+----------------+----------------+----------------+
| 1.16.3.1.7    | Manufacturer   | ContrastMed    |                |
|               | Name           | Corp           |                |
+---------------+----------------+----------------+----------------+
| 1.16.3.1.8    | Brand Name     | Or             |                |
|               |                | alContrastofin |                |
+---------------+----------------+----------------+----------------+
| 1.16.3.1.9    | Barcode Value  | -00408497      | PZN number     |
+---------------+----------------+----------------+----------------+
| 1.16.3.1.10   | Lot Identifier | 6X14325        |                |
+---------------+----------------+----------------+----------------+
| 1.16.3.2      | Component      | 24.4           | UNITS=EV (ml,  |
|               | Volume         |                | UCUM, "ml")    |
+---------------+----------------+----------------+----------------+
| 1.16.4        | Imaging Agent  |                |                |
|               | Component      |                |                |
|               | Usage          |                |                |
+---------------+----------------+----------------+----------------+
| 1.16.4.1      | Imaging Agent  |                |                |
|               | Component      |                |                |
+---------------+----------------+----------------+----------------+
| 1.16.4.1.1    | Drug           | (11713004,     |                |
|               | administered   | SCT, "Water")  |                |
+---------------+----------------+----------------+----------------+
| 1.16.4.1.2    | Unit of        | (68276009,     |                |
|               | Presentation   | SCT, "Bottle") |                |
+---------------+----------------+----------------+----------------+
| 1.16.4.1.3    | Imaging Agent  | 1000           | UNITS=EV (ml,  |
|               | Volume Per     |                | UCUM, "ml")    |
|               | Unit of        |                |                |
|               | Presentation   |                |                |
+---------------+----------------+----------------+----------------+
| 1.16.4.1.4    | Manufacturer   | Fresh Water    |                |
|               | Name           | Corp           |                |
+---------------+----------------+----------------+----------------+
| 1.16.4.1.5    | Brand Name     | BestWaterEver  |                |
+---------------+----------------+----------------+----------------+
| 1.16.4.1.6    | Barcode Value  | -4801694       | PZN number     |
+---------------+----------------+----------------+----------------+
| 1.16.4.2      | Component      | 975.6          | UNITS=EV (ml,  |
|               | Volume         |                | UCUM, "ml")    |
+---------------+----------------+----------------+----------------+
| 1.17          | Summary        | Administered   |                |
|               |                | 1000 ml of     |                |
|               |                | Oral           |                |
|               |                | Contrastofin   |                |
|               |                | via oral route |                |
|               |                | and 88ml of    |                |
|               |                | ContrastStuff  |                |
|               |                | 370 via        |                |
|               |                | intravenous    |                |
|               |                | route in Left  |                |
|               |                | Arm Vein.      |                |
+---------------+----------------+----------------+----------------+
| 1.18          | Imaging Agent  |                |                |
|               | Administration |                |                |
|               | Consumable     |                |                |
+---------------+----------------+----------------+----------------+
| 1.18.1        | Imaging Agent  | (467354001,    |                |
|               | Administration | SCT, "Contrast |                |
|               | Consumable     | medium         |                |
|               | Type           | injection      |                |
|               |                | system         |                |
|               |                | manifold kit") |                |
+---------------+----------------+----------------+----------------+
| 1.18.2        | Quantity of    | 1              |                |
|               | Material       |                |                |
+---------------+----------------+----------------+----------------+
| 1.18.2.1      | Consumable is  | (373066001,    |                |
|               | New            | SCT, "Yes")    |                |
+---------------+----------------+----------------+----------------+
| 1.18.3        | Billing Code   | 317627C        |                |
+---------------+----------------+----------------+----------------+
| 1.18.4        | Medical        | 20221031       |                |
|               | Product        |                |                |
|               | Expiration     |                |                |
|               | Date           |                |                |
+---------------+----------------+----------------+----------------+
| 1.18.5        | Manufacturer   | Injector Corp  |                |
|               | Name           |                |                |
+---------------+----------------+----------------+----------------+
| 1.18.6        | Barcode Value  | (01)           |                |
|               |                | 14250299       |                |
|               |                | 676272(19)1311 |                |
|               |                | 1501(17)181000 |                |
+---------------+----------------+----------------+----------------+
| 1.18.7        | Lot Identifier | 13111501       |                |
+---------------+----------------+----------------+----------------+
| 1.19          | Imaging Agent  |                |                |
|               | Administration |                |                |
|               | Consumable     |                |                |
+---------------+----------------+----------------+----------------+
| 1.19.1        | Imaging Agent  | (79068005,     |                |
|               | Administration | SCT, "Needle") |                |
|               | Consumable     |                |                |
|               | Type           |                |                |
+---------------+----------------+----------------+----------------+
| 1.19.2        | Quantity of    | 1              |                |
|               | Material       |                |                |
+---------------+----------------+----------------+----------------+
| 1.19.2.1      | Consumable is  | (373066001,    |                |
|               | New            | SCT, "Yes")    |                |
+---------------+----------------+----------------+----------------+
| 1.19.3        | Billing Code   | 206342         |                |
+---------------+----------------+----------------+----------------+
| 1.19.4        | Medical        | 20181130       |                |
|               | Product        |                |                |
|               | Expiration     |                |                |
|               | Date           |                |                |
+---------------+----------------+----------------+----------------+
| 1.19.5        | Manufacturer   | Dr. Poke Inc.  |                |
|               | Name           |                |                |
+---------------+----------------+----------------+----------------+
| 1.19.6        | Brand Name     | Sterile        |                |
|               |                | Standard,      |                |
|               |                | Green          |                |
+---------------+----------------+----------------+----------------+
| 1.20          | Imaging Agent  |                |                |
|               | Administration |                |                |
|               | Consumable     |                |                |
+---------------+----------------+----------------+----------------+
| 1.20.1        | Imaging Agent  | (68276009,     |                |
|               | Administration | SCT, "Bottle") |                |
|               | Consumable     |                |                |
|               | Type           |                |                |
+---------------+----------------+----------------+----------------+
| 1.20.2        | Quantity of    | 1              |                |
|               | Material       |                |                |
+---------------+----------------+----------------+----------------+
| 1.20.2.1      | Consumable is  | (373066001,    |                |
|               | New            | SCT, "Yes")    |                |
+---------------+----------------+----------------+----------------+
| 1.20.3        | Billing Code   | 47110815       |                |
+---------------+----------------+----------------+----------------+
| 1.20.4        | Medical        | 20191001       |                |
|               | Product        |                |                |
|               | Expiration     |                |                |
|               | Date           |                |                |
+---------------+----------------+----------------+----------------+
| 1.21          | Imaging Agent  |                |                |
|               | Administration |                |                |
|               | Steps          |                |                |
+---------------+----------------+----------------+----------------+
| 1.21.1        | Imaging Agent  | Abdomen        |                |
|               | Administration | intestinal and |                |
|               | Steps Name     | vessel         |                |
|               |                | contrast       |                |
|               |                | processing     |                |
+---------------+----------------+----------------+----------------+
| 1.21.2        | Imaging Agent  | This contrast  |                |
|               | Administration | processing is  |                |
|               | Steps          | given by an    |                |
|               | Description    | oral           |                |
|               |                | administration |                |
|               |                | of first 2     |                |
|               |                | hours in       |                |
|               |                | advance of the |                |
|               |                | procedure.     |                |
|               |                | I.v.           |                |
|               |                | administration |                |
|               |                | is done with a |                |
|               |                | pre-inject to  |                |
|               |                | determine scan |                |
|               |                | delay time.    |                |
|               |                | Patent test    |                |
|               |                | injection      |                |
|               |                | applies as a   |                |
|               |                | default        |                |
|               |                | procedure.     |                |
+---------------+----------------+----------------+----------------+
| 1.21.3        | Imaging Agent  |                |                |
|               | Administration |                |                |
|               | Step           |                |                |
+---------------+----------------+----------------+----------------+
| 1.21.3.1.     | Imaging Agent  | ORAL_STEP_1    |                |
|               | Administration |                |                |
|               | Step           |                |                |
|               | Identifier     |                |                |
+---------------+----------------+----------------+----------------+
| 1.21.3.2      | Imaging Agent  | 1.2.           | Since "Root    |
|               | Administration | 3.4.47110815.3 | Concept Name   |
|               | Performed Step |                | Code Sequence" |
|               | UID            |                | is "Performed  |
|               |                |                | Imaging Agent  |
|               |                |                | A              |
|               |                |                | dministration" |
+---------------+----------------+----------------+----------------+
| 1.21.3.3      | Administration | (130174, DCM,  |                |
|               | Mode           | "Manual        |                |
|               |                | Ad             |                |
|               |                | ministration") |                |
+---------------+----------------+----------------+----------------+
| 1.21.3.4      | Person Role in | (121025, DCM,  | Since          |
|               | Organization   | "Patient")     | "              |
|               |                |                | Administration |
|               |                |                | Mode" is       |
|               |                |                | "Manual        |
|               |                |                | Ad             |
|               |                |                | ministration", |
|               |                |                | condition      |
|               |                |                | holds          |
|               |                |                | (self-a        |
|               |                |                | dministration) |
+---------------+----------------+----------------+----------------+
| 1.21.3.5      | Administration | (130249, DCM,  |                |
|               | Step Type      | "Diagnostic    |                |
|               |                | Ad             |                |
|               |                | ministration") |                |
+---------------+----------------+----------------+----------------+
| 1.21.3.6      | Scan Delay     | 7200           | UNITS = EV (s, |
|               |                |                | UCUM, "s")     |
+---------------+----------------+----------------+----------------+
| 1.21.3.7      | Route of       | (26643006,     |                |
|               | Administration | SCT, "Oral     |                |
|               |                | route")        |                |
+---------------+----------------+----------------+----------------+
| 1.21.3.8      | Imaging Agent  |                |                |
|               | Administration |                |                |
|               | Phase          |                |                |
+---------------+----------------+----------------+----------------+
| 1.21.3.8.1    | Imaging Agent  | ORAL_PHASE     |                |
|               | Administration |                |                |
|               | Phase          |                |                |
|               | Identifier     |                |                |
+---------------+----------------+----------------+----------------+
| 1.21.3.8.2    | Imaging Agent  | 1.2.           | Since "Root    |
|               | Administration | 3.4.47110815.4 | Concept Name   |
|               | Performed      |                | Code Sequence" |
|               | Phase UID      |                | is "Performed  |
|               |                |                | Imaging Agent  |
|               |                |                | A              |
|               |                |                | dministration" |
+---------------+----------------+----------------+----------------+
| 1.21.3.8.3    | Imaging Agent  |                |                |
|               | Administration |                |                |
|               | Activity       |                |                |
+---------------+----------------+----------------+----------------+
| 1.21.3.8.3.1  | Referenced     | ORAL_          | Value of       |
|               | Imaging Agent  | CONTRAST_AGENT | 1.16.1         |
|               | Identifier     |                |                |
+---------------+----------------+----------------+----------------+
| 1.21.3.8.3.2  | Volume         | 1000           | UNITS = EV     |
|               | Administered   |                | (ml, UCUM,     |
|               |                |                | "ml")          |
|               |                |                |                |
|               |                |                | Same value as  |
|               |                |                | 1.21.3.8.4     |
+---------------+----------------+----------------+----------------+
| 1.21.3.8.3.3  | DateTime       | 20181012101531 | Since root     |
|               | Started        |                | Concept Name   |
|               |                |                | is "Performed  |
|               |                |                | Imaging Agent  |
|               |                |                | A              |
|               |                |                | dministration" |
+---------------+----------------+----------------+----------------+
| 1.21.3.8.3.4  | Duration       | 2700           | UNITS = EV (s, |
|               |                |                | UCUM, "s")     |
|               |                |                |                |
|               |                |                | Since root     |
|               |                |                | Concept Name   |
|               |                |                | is "Performed  |
|               |                |                | Imaging Agent  |
|               |                |                | A              |
|               |                |                | dministration" |
+---------------+----------------+----------------+----------------+
| 1.21.3.8.4    | Total Phase    | 1000           | UNITS = EV     |
|               | Volume         |                | (ml, UCUM,     |
|               | Administered   |                | "ml")          |
|               |                |                |                |
|               |                |                | Same value as  |
|               |                |                | 1.21.3.8.3.2   |
+---------------+----------------+----------------+----------------+
| 1.21.3.8.5    | DateTime       | 20181012101531 | Since "Root    |
|               | Started        |                | Concept Name   |
|               |                |                | Code Sequence" |
|               |                |                | is "Performed  |
|               |                |                | Imaging Agent  |
|               |                |                | A              |
|               |                |                | dministration" |
+---------------+----------------+----------------+----------------+
| 1.21.3.8.6    | Duration       | 2700           | UNITS = EV (s, |
|               |                |                | UCUM, "s")     |
|               |                |                |                |
|               |                |                | Since "Root    |
|               |                |                | Concept Name   |
|               |                |                | Code Sequence" |
|               |                |                | is "Performed  |
|               |                |                | Imaging Agent  |
|               |                |                | A              |
|               |                |                | dministration" |
+---------------+----------------+----------------+----------------+
| 1.21.4        | Imaging Agent  |                |                |
|               | Administration |                |                |
|               | Step           |                |                |
+---------------+----------------+----------------+----------------+
| 1.21.4.1      | Imaging Agent  | EXTRAVASATI    |                |
|               | Administration | ON_TEST_STEP_2 |                |
|               | Step           |                |                |
|               | Identifier     |                |                |
+---------------+----------------+----------------+----------------+
| 1.21.4.2      | Imaging Agent  | 1.2.           | Since "Root    |
|               | Administration | 3.4.47110815.5 | Concept Name   |
|               | Performed Step |                | Code Sequence" |
|               | UID            |                | is "Performed  |
|               |                |                | Imaging Agent  |
|               |                |                | A              |
|               |                |                | dministration" |
+---------------+----------------+----------------+----------------+
| 1.21.4.3      | Administration | (130173, DCM,  |                |
|               | Mode           | "Automated     |                |
|               |                | Ad             |                |
|               |                | ministration") |                |
+---------------+----------------+----------------+----------------+
| 1.21.4.4      | Administration | (130247, DCM,  |                |
|               | Step Type      | "Patency Test  |                |
|               |                | Injection")    |                |
+---------------+----------------+----------------+----------------+
| 1.21.4.5      | Route of       | (47625008,     |                |
|               | Administration | SCT,           |                |
|               |                | "Intravenous   |                |
|               |                | route")        |                |
+---------------+----------------+----------------+----------------+
| 1.21.4.5.1    | Site of        | (261459001,    | Since "Route   |
|               |                | SCT, "Via arm  | of             |
|               |                | vein")         | A              |
|               |                |                | dministration" |
|               |                |                | is             |
|               |                |                | "Intravenous   |
|               |                |                | route"         |
+---------------+----------------+----------------+----------------+
| 1.21.4.5.1.1  | Laterality     | (7771000, SCT, | Since "Site    |
|               |                | "Left")        | of" is "Via    |
|               |                |                | arm vein"      |
+---------------+----------------+----------------+----------------+
| 1.21.4.6      | Imaging Agent  |                |                |
|               | Administration |                |                |
|               | Phase          |                |                |
+---------------+----------------+----------------+----------------+
| 1.21.4.6.1    | Imaging Agent  | EXTRAVASAT     |                |
|               | Administration | ION_TEST_PHASE |                |
|               | Phase          |                |                |
|               | Identifier     |                |                |
+---------------+----------------+----------------+----------------+
| 1.21.4.6.2    | Imaging Agent  | 1.2.           | Since "Root    |
|               | Administration | 3.4.47110815.6 | Concept Name   |
|               | Performed      |                | Code Sequence" |
|               | Phase UID      |                | is "Performed  |
|               |                |                | Imaging Agent  |
|               |                |                | A              |
|               |                |                | dministration" |
+---------------+----------------+----------------+----------------+
| 1.21.4.6.3    | Imaging Agent  | (130171, DCM,  | Since 1.21.4.3 |
|               | Administration | "Automatic     | (              |
|               | Phase Type     | with Manual    | Administration |
|               |                | Inject Phase") | Mode) is       |
|               |                |                | "Automated     |
|               |                |                | A              |
|               |                |                | dministration" |
+---------------+----------------+----------------+----------------+
| 1.21.4.6.4    | Imaging Agent  |                |                |
|               | Administration |                |                |
|               | Activity       |                |                |
+---------------+----------------+----------------+----------------+
| 1.21.4.6.4.1  | Referenced     | INJECT         | Value of       |
|               | Imaging Agent  | OR_FLUSH_AGENT | 1.15.1         |
|               | Identifier     |                |                |
+---------------+----------------+----------------+----------------+
| 1.21.4.6.4.2  | Volume         | 30             | UNITS = EV     |
|               | Administered   |                | (ml, UCUM,     |
|               |                |                | "ml")          |
|               |                |                |                |
|               |                |                | Same value as  |
|               |                |                | 1.21.4.6.5 and |
|               |                |                | 1.21.4.9.1     |
+---------------+----------------+----------------+----------------+
| 1.21.4.6.4.3  | Starting Flow  | 3              | UNITS = EV     |
|               | Rate of        |                | (ml/s, UCUM    |
|               | administration |                | "ml/s")        |
+---------------+----------------+----------------+----------------+
| 1.21.4.6.4.4  | Peak Flow Rate | 3              | UNITS = EV     |
|               | in Phase       |                | (ml/s, UCUM    |
|               | Activity       |                | "ml/s")        |
|               |                |                |                |
|               |                |                | Since 1.21.4.3 |
|               |                |                | (              |
|               |                |                | Administration |
|               |                |                | Mode) is       |
|               |                |                | "Automated     |
|               |                |                | A              |
|               |                |                | dministration" |
|               |                |                | and "Root      |
|               |                |                | Concept Name   |
|               |                |                | Code Sequence" |
|               |                |                | is "Performed  |
|               |                |                | Imaging Agent  |
|               |                |                | A              |
|               |                |                | dministration" |
+---------------+----------------+----------------+----------------+
| 1.21.4.6.4.5  | Peak Pressure  | 2.5            | UNITS = EV     |
|               | in Phase       |                | (kPa, UCUM     |
|               | Activity       |                | "kPa")         |
|               |                |                |                |
|               |                |                | Since 1.21.4.3 |
|               |                |                | (              |
|               |                |                | Administration |
|               |                |                | Mode) is       |
|               |                |                | "Automated     |
|               |                |                | A              |
|               |                |                | dministration" |
|               |                |                | and "Root      |
|               |                |                | Concept Name   |
|               |                |                | Code Sequence" |
|               |                |                | is "Performed  |
|               |                |                | Imaging Agent  |
|               |                |                | A              |
|               |                |                | dministration" |
+---------------+----------------+----------------+----------------+
| 1.21.4.6.4.6  | Initial Volume | 197            | UNITS = EV     |
|               | of Imaging     |                | (ml, UCUM,     |
|               | Agent in       |                | "ml")          |
|               | Container      |                |                |
|               |                |                | Since "Root    |
|               |                |                | Concept Name   |
|               |                |                | Code Sequence" |
|               |                |                | is "Performed  |
|               |                |                | Imaging Agent  |
|               |                |                | A              |
|               |                |                | dministration" |
+---------------+----------------+----------------+----------------+
| 1.21.4.6.4.7  | Residual       | 167            | UNITS = EV     |
|               | Volume of      |                | (ml, UCUM,     |
|               | Imaging Agent  |                | "ml")          |
|               | in Container   |                |                |
|               |                |                | Since "Root    |
|               |                |                | Concept Name   |
|               |                |                | Code Sequence" |
|               |                |                | is "Performed  |
|               |                |                | Imaging Agent  |
|               |                |                | A              |
|               |                |                | dministration" |
+---------------+----------------+----------------+----------------+
| 1.21.4.6.4.8  | DateTime       | 20181012121537 | Since root     |
|               | Started        |                | Concept Name   |
|               |                |                | is "Performed  |
|               |                |                | Imaging Agent  |
|               |                |                | A              |
|               |                |                | dministration" |
+---------------+----------------+----------------+----------------+
| 1.21.4.6.4.9  | Duration       | 10             | UNITS = EV (s, |
|               |                |                | UCUM, "s")     |
|               |                |                |                |
|               |                |                | Since root     |
|               |                |                | Concept Name   |
|               |                |                | is "Performed  |
|               |                |                | Imaging Agent  |
|               |                |                | A              |
|               |                |                | dministration" |
+---------------+----------------+----------------+----------------+
| 1.21.4.6.5    | Total Phase    | 30             | UNITS = EV     |
|               | Volume         |                | (ml, UCUM,     |
|               | Administered   |                | "ml")          |
|               |                |                |                |
|               |                |                | In this case   |
|               |                |                | the same value |
|               |                |                | as             |
|               |                |                | 1.21.4.6.4.2   |
|               |                |                | and 1.21.4.9.1 |
+---------------+----------------+----------------+----------------+
| 1.21.4.6.6    | DateTime       | 20181012121537 | Since root     |
|               | Started        |                | Concept Name   |
|               |                |                | Code Sequence  |
|               |                |                | is "Performed  |
|               |                |                | Imaging Agent  |
|               |                |                | A              |
|               |                |                | dministration" |
+---------------+----------------+----------------+----------------+
| 1.21.4.6.7    | Duration       | 10             | UNITS = EV (s, |
|               |                |                | UCUM, "s")     |
|               |                |                |                |
|               |                |                | Since root     |
|               |                |                | Concept Name   |
|               |                |                | Code Sequence  |
|               |                |                | is "Performed  |
|               |                |                | Imaging Agent  |
|               |                |                | Ad             |
|               |                |                | ministration") |
+---------------+----------------+----------------+----------------+
| 1.21.4.7      | Number of      | 2              |                |
|               | Injector Heads |                |                |
+---------------+----------------+----------------+----------------+
| 1.21.4.8      | Programmable   | (373066001,    |                |
|               | Device         | SCT, "Yes")    |                |
+---------------+----------------+----------------+----------------+
| 1.21.4.9      | Manually       |                | Since 1.21.4.3 |
|               | triggered      |                | (              |
|               | injection      |                | Administration |
|               | information    |                | Mode) is       |
|               |                |                | "Automated     |
|               |                |                | A              |
|               |                |                | dministration" |
|               |                |                | and root       |
|               |                |                | Concept Name   |
|               |                |                | Code Sequence  |
|               |                |                | is "Performed  |
|               |                |                | Imaging Agent  |
|               |                |                | A              |
|               |                |                | dministration" |
+---------------+----------------+----------------+----------------+
| 1.21.4.9.1    | Total Step     | 30             | UNITS = EV     |
|               | Volume         |                | (ml, UCUM,     |
|               | Administered   |                | "ml")          |
|               |                |                |                |
|               |                |                | In this case   |
|               |                |                | the same value |
|               |                |                | as             |
|               |                |                | 1.21.4.6.4.2   |
|               |                |                | and 1.21.4.6.5 |
+---------------+----------------+----------------+----------------+
| 1.21.4.9.2    | Total number   | 1              |                |
|               | of manually    |                |                |
|               | triggered      |                |                |
|               | injections     |                |                |
+---------------+----------------+----------------+----------------+
| 1.21.5        | Imaging Agent  |                |                |
|               | Administration |                |                |
|               | Step           |                |                |
+---------------+----------------+----------------+----------------+
| 1.21.5.1      | Imaging Agent  | DELAY_E        |                |
|               | Administration | STIMATE_STEP_3 |                |
|               | Step           |                |                |
|               | Identifier     |                |                |
+---------------+----------------+----------------+----------------+
| 1.21.5.2      | Imaging Agent  | 1.2.           | Since "Root    |
|               | Administration | 3.4.47110815.7 | Concept Name   |
|               | Performed Step |                | Code Sequence" |
|               | UID            |                | is "Performed  |
|               |                |                | Imaging Agent  |
|               |                |                | A              |
|               |                |                | dministration" |
+---------------+----------------+----------------+----------------+
| 1.21.5.3      | Administration | (130173, DCM,  |                |
|               | Mode           | "Automated     |                |
|               |                | Ad             |                |
|               |                | ministration") |                |
+---------------+----------------+----------------+----------------+
| 1.21.5.4      | Administration | (130248, DCM,  |                |
|               | Step Type      | "Transit Time  |                |
|               |                | Test           |                |
|               |                | Injection")    |                |
+---------------+----------------+----------------+----------------+
| 1.21.5.5      | Pressure Limit | 15             | UNITS = EV     |
|               |                |                | (kPa, UCUM     |
|               |                |                | "kPa")         |
|               |                |                |                |
|               |                |                | Since 1.21.5.3 |
|               |                |                | is "Automated  |
|               |                |                | A              |
|               |                |                | dministration" |
+---------------+----------------+----------------+----------------+
| 1.21.5.6      | Route of       | (47625008,     |                |
|               | Administration | SCT,           |                |
|               |                | "Intravenous   |                |
|               |                | route")        |                |
+---------------+----------------+----------------+----------------+
| 1.21.5.6.1    | Site of        | (261459001,    | Since "Route   |
|               |                | SCT, "Via arm  | of             |
|               |                | vein")         | A              |
|               |                |                | dministration" |
|               |                |                | is             |
|               |                |                | "Intravenous   |
|               |                |                | route"         |
+---------------+----------------+----------------+----------------+
| 1.21.5.6.1.1  | Laterality     | (7771000, SCT, | Since "Site    |
|               |                | "Left")        | of" is "Via    |
|               |                |                | arm vein"      |
+---------------+----------------+----------------+----------------+
| 1.21.5.7      | Imaging Agent  |                |                |
|               | Administration |                |                |
|               | Phase          |                |                |
+---------------+----------------+----------------+----------------+
| 1.21.5.7.1    | Imaging Agent  | DELAY_ES       |                |
|               | Administration | TIMATE_PHASE_1 |                |
|               | Phase          |                |                |
|               | Identifier     |                |                |
+---------------+----------------+----------------+----------------+
| 1.21.5.7.2    | Imaging Agent  | 1.2.           | Since "Root    |
|               | Administration | 3.4.47110815.8 | Concept Name   |
|               | Performed      |                | Code Sequence" |
|               | Phase UID      |                | is "Performed  |
|               |                |                | Imaging Agent  |
|               |                |                | A              |
|               |                |                | dministration" |
+---------------+----------------+----------------+----------------+
| 1.21.5.7.3    | Imaging Agent  | (130168, DCM,  | Since 1.21.5.3 |
|               | Administration | "Automatic     | is "Automated  |
|               | Phase Type     | Administration | A              |
|               |                | Phase")        | dministration" |
+---------------+----------------+----------------+----------------+
| 1.21.5.7.4    | Imaging Agent  |                |                |
|               | Administration |                |                |
|               | Activity       |                |                |
+---------------+----------------+----------------+----------------+
| 1.21.5.7.4.1  | Referenced     | INJECTOR_      | Value of       |
|               | Imaging Agent  | CONTRAST_AGENT | 1.14.1         |
|               | Identifier     |                |                |
+---------------+----------------+----------------+----------------+
| 1.21.5.7.4.2  | Volume         | 10             | UNITS = EV     |
|               | Administered   |                | (ml, UCUM,     |
|               |                |                | "ml")          |
|               |                |                |                |
|               |                |                | Same value as  |
|               |                |                | 1.21.5.7.5     |
+---------------+----------------+----------------+----------------+
| 1.21.5.7.4.3  | Starting Flow  | 3              | UNITS = EV     |
|               | Rate of        |                | (ml/s, UCUM    |
|               | administration |                | "ml/s")        |
+---------------+----------------+----------------+----------------+
| 1.21.5.7.4.4  | Peak Flow Rate | 3              | UNITS = EV     |
|               | in Phase       |                | (ml/s, UCUM    |
|               | Activity       |                | "ml/s")        |
|               |                |                |                |
|               |                |                | Since 1.21.5.3 |
|               |                |                | is "Automated  |
|               |                |                | A              |
|               |                |                | dministration" |
|               |                |                | and "Root      |
|               |                |                | Concept Name   |
|               |                |                | Code Sequence" |
|               |                |                | is "Performed  |
|               |                |                | Imaging Agent  |
|               |                |                | A              |
|               |                |                | dministration" |
+---------------+----------------+----------------+----------------+
| 1.21.5.7.4.5  | Peak Pressure  | 2              | UNITS = EV     |
|               | in Phase       |                | (kPa, UCUM     |
|               | Activity       |                | "kPa")         |
|               |                |                |                |
|               |                |                | Since 1.21.5.3 |
|               |                |                | is "Automated  |
|               |                |                | A              |
|               |                |                | dministration" |
|               |                |                | and "Root      |
|               |                |                | Concept Name   |
|               |                |                | Code Sequence" |
|               |                |                | is "Performed  |
|               |                |                | Imaging Agent  |
|               |                |                | A              |
|               |                |                | dministration" |
+---------------+----------------+----------------+----------------+
| 1.21.5.7.4.6  | Initial Volume | 195            | UNITS = EV     |
|               | of Imaging     |                | (ml, UCUM,     |
|               | Agent in       |                |                |
|               | Container      |                | "ml")          |
|               |                |                |                |
|               |                |                | Since "Root    |
|               |                |                | Concept Name   |
|               |                |                | Code Sequence" |
|               |                |                | is "Performed  |
|               |                |                | Imaging Agent  |
|               |                |                | A              |
|               |                |                | dministration" |
+---------------+----------------+----------------+----------------+
| 1.21.5.7.4.7  | Residual       | 185            | UNITS = EV     |
|               | Volume of      |                | (ml, UCUM,     |
|               | Imaging Agent  |                | "ml")          |
|               | in Container   |                |                |
|               |                |                | Since "Root    |
|               |                |                | Concept Name   |
|               |                |                | Code Sequence" |
|               |                |                | is "Performed  |
|               |                |                | Imaging Agent  |
|               |                |                | A              |
|               |                |                | dministration" |
+---------------+----------------+----------------+----------------+
| 1.21.5.7.4.8  | DateTime       | 20181012121637 | Since root     |
|               | Started        |                | Concept Name   |
|               |                |                | is "Performed  |
|               |                |                | Imaging Agent  |
|               |                |                | A              |
|               |                |                | dministration" |
+---------------+----------------+----------------+----------------+
| 1.21.5.7.4.9  | Duration       | 3.3            | UNITS = EV (s, |
|               |                |                | UCUM, "s")     |
|               |                |                |                |
|               |                |                | Since root     |
|               |                |                | Concept Name   |
|               |                |                | is "Performed  |
|               |                |                | Imaging Agent  |
|               |                |                | A              |
|               |                |                | dministration" |
+---------------+----------------+----------------+----------------+
| 1.21.5.7.5    | Total Phase    | 10             | UNITS = EV     |
|               | Volume         |                | (ml, UCUM,     |
|               | Administered   |                | "ml")          |
|               |                |                |                |
|               |                |                | Same value as  |
|               |                |                | 1.21.5.7.4.2   |
+---------------+----------------+----------------+----------------+
| 1.21.5.7.6    | DateTime       | 20181012121637 | Since root     |
|               | Started        |                | Concept Name   |
|               |                |                | Code Sequence  |
|               |                |                | is "Performed  |
|               |                |                | Imaging Agent  |
|               |                |                | A              |
|               |                |                | dministration" |
+---------------+----------------+----------------+----------------+
| 1.21.5.7.7    | Duration       | 3.3            | UNITS = EV (s, |
|               |                |                | UCUM, "s")     |
|               |                |                |                |
|               |                |                | Since root     |
|               |                |                | Concept Name   |
|               |                |                | Code Sequence  |
|               |                |                | is "Performed  |
|               |                |                | Imaging Agent  |
|               |                |                | Ad             |
|               |                |                | ministration") |
+---------------+----------------+----------------+----------------+
| 1.21.5.8      | Imaging Agent  |                |                |
|               | Administration |                |                |
|               | Phase          |                |                |
+---------------+----------------+----------------+----------------+
| 1.21.5.8.1    | Imaging Agent  | DELAY_ES       |                |
|               | Administration | TIMATE_PHASE_2 |                |
|               | Phase          |                |                |
|               | Identifier     |                |                |
+---------------+----------------+----------------+----------------+
| 1.21.5.8.2    | Imaging Agent  | 1.2.           | Since "Root    |
|               | Administration | 3.4.47110815.9 | Concept Name   |
|               | Performed      |                | Code Sequence" |
|               | Phase UID      |                | is "Performed  |
|               |                |                | Imaging Agent  |
|               |                |                | A              |
|               |                |                | dministration" |
+---------------+----------------+----------------+----------------+
| 1.21.5.8.3    | Imaging Agent  | (130168, DCM,  | Since 1.21.5.3 |
|               | Administration | "Automatic     | is "Automated  |
|               | Phase Type     | Administration | A              |
|               |                | Phase")        | dministration" |
+---------------+----------------+----------------+----------------+
| 1.21.5.8.4    | Imaging Agent  |                |                |
|               | Administration |                |                |
|               | Activity       |                |                |
+---------------+----------------+----------------+----------------+
| 1.21.5.8.4.1  | Referenced     | INJECT         | Value of       |
|               | Imaging Agent  | OR_FLUSH_AGENT | 1.15.1         |
|               | Identifier     |                |                |
+---------------+----------------+----------------+----------------+
| 1.21.5.8.4.2  | Volume         | 30             | UNITS = EV     |
|               | Administered   |                | (ml, UCUM,     |
|               |                |                | "ml")          |
|               |                |                |                |
|               |                |                | Same value as  |
|               |                |                | 1.21.5.9.5     |
+---------------+----------------+----------------+----------------+
| 1.21.5.8.4.3  | Starting Flow  | 3              | UNITS = EV     |
|               | Rate of        |                | (ml/s, UCUM    |
|               | administration |                | "ml/s")        |
+---------------+----------------+----------------+----------------+
| 1.21.5.8.4.4  | Peak Flow Rate | 3              | UNITS = EV     |
|               | in Phase       |                | (ml/s, UCUM    |
|               | Activity       |                | "ml/s")        |
|               |                |                |                |
|               |                |                | Since 1.21.5.3 |
|               |                |                | is "Automated  |
|               |                |                | A              |
|               |                |                | dministration" |
|               |                |                | and "Root      |
|               |                |                | Concept Name   |
|               |                |                | Code Sequence" |
|               |                |                | is "Performed  |
|               |                |                | Imaging Agent  |
|               |                |                | A              |
|               |                |                | dministration" |
+---------------+----------------+----------------+----------------+
| 1.21.5.8.4.5  | Peak Pressure  | 5              | UNITS = EV     |
|               | in Phase       |                | (kPa, UCUM     |
|               | Activity       |                | "kPa")         |
|               |                |                |                |
|               |                |                | Since 1.21.5.3 |
|               |                |                | is "Automated  |
|               |                |                | A              |
|               |                |                | dministration" |
|               |                |                | and "Root      |
|               |                |                | Concept Name   |
|               |                |                | Code Sequence" |
|               |                |                | is "Performed  |
|               |                |                | Imaging Agent  |
|               |                |                | A              |
|               |                |                | dministration" |
+---------------+----------------+----------------+----------------+
| 1.21.5.8.4.6  | Initial Volume | 166            | UNITS = EV     |
|               | of Imaging     |                | (ml, UCUM,     |
|               | Agent in       |                | "ml")          |
|               | Container      |                |                |
|               |                |                | Since "Root    |
|               |                |                | Concept Name   |
|               |                |                | Code Sequence" |
|               |                |                | is "Performed  |
|               |                |                | Imaging Agent  |
|               |                |                | A              |
|               |                |                | dministration" |
+---------------+----------------+----------------+----------------+
| 1.21.5.8.4.7  | Residual       | 136            | UNITS = EV     |
|               | Volume of      |                | (ml, UCUM,     |
|               | Imaging Agent  |                | "ml")          |
|               | in Container   |                |                |
|               |                |                | Since "Root    |
|               |                |                | Concept Name   |
|               |                |                | Code Sequence" |
|               |                |                | is "Performed  |
|               |                |                | Imaging Agent  |
|               |                |                | A              |
|               |                |                | dministration" |
+---------------+----------------+----------------+----------------+
| 1.21.5.8.4.8  | DateTime       | 20             | Since root     |
|               | Started        | 181012121640.3 | Concept Name   |
|               |                |                | is "Performed  |
|               |                |                | Imaging Agent  |
|               |                |                | A              |
|               |                |                | dministration" |
+---------------+----------------+----------------+----------------+
| 1.21.5.8.4.9  | Duration       | 10             | UNITS = EV (s, |
|               |                |                | UCUM, "s")     |
|               |                |                |                |
|               |                |                | Since root     |
|               |                |                | Concept Name   |
|               |                |                | is "Performed  |
|               |                |                | Imaging Agent  |
|               |                |                | A              |
|               |                |                | dministration" |
+---------------+----------------+----------------+----------------+
| 1.21.5.8.5    | Total Phase    | 30             | UNITS = EV     |
|               | Volume         |                | (ml, UCUM,     |
|               | Administered   |                | "ml")          |
|               |                |                |                |
|               |                |                | Same value as  |
|               |                |                | 1.21.5.9.4.2   |
+---------------+----------------+----------------+----------------+
| 1.21.5.8.6    | DateTime       | 20             | Since root     |
|               | Started        | 181012121640.3 | Concept Name   |
|               |                |                | Code Sequence  |
|               |                |                | is "Performed  |
|               |                |                | Imaging Agent  |
|               |                |                | A              |
|               |                |                | dministration" |
+---------------+----------------+----------------+----------------+
| 1.21.5.8.7    | Duration       | 10             | UNITS = EV (s, |
|               |                |                | UCUM, "s")     |
|               |                |                |                |
|               |                |                | Since root     |
|               |                |                | Concept Name   |
|               |                |                | Code Sequence  |
|               |                |                | is "Performed  |
|               |                |                | Imaging Agent  |
|               |                |                | Ad             |
|               |                |                | ministration") |
+---------------+----------------+----------------+----------------+
| 1.21.5.9      | Imaging Agent  |                |                |
|               | Administration |                |                |
|               | Graph          |                |                |
+---------------+----------------+----------------+----------------+
| 1.21.5.9.1    | Referenced     | INJECTOR_      |                |
|               | Imaging Agent  | CONTRAST_AGENT |                |
|               | Identifier     |                |                |
+---------------+----------------+----------------+----------------+
| 1.21.5.9.2    | Flow Rate vs   |                | Concept name   |
|               | time           |                | is parameter   |
|               |                |                | $M             |
|               |                |                | easurmentGraph |
+---------------+----------------+----------------+----------------+
| 1.21.5.9.2.1  | X-Concept      | (130194, DCM,  | Parameter      |
|               |                | "Time after    | $X-Concept     |
|               |                | the start of   |                |
|               |                | injection")    |                |
+---------------+----------------+----------------+----------------+
| 1.21.5.9.2.2  | Y-Concept      | (122094, DCM,  | Parameter      |
|               |                | "Rate of       | $Y-Concept     |
|               |                | ad             |                |
|               |                | ministration") |                |
+---------------+----------------+----------------+----------------+
| 1.21.5.9.2.3  | Flow Rate vs   | IMAGE =        |                |
|               | time           | 1.2.3.         |                |
|               |                | 4.5.6.7.8.9.10 |                |
+---------------+----------------+----------------+----------------+
| 1.21.5.9.3    | Pressure vs    |                | Concept name   |
|               | time           |                | is parameter   |
|               |                |                | $Me            |
|               |                |                | asurementGraph |
|               |                |                | of             |
+---------------+----------------+----------------+----------------+
| 1.21.5.9.3.1  | X-Concept      | (130194, DCM,  | Parameter      |
|               |                | "Time after    | $X-Concept of  |
|               |                | the start of   |                |
|               |                | injection")    |                |
+---------------+----------------+----------------+----------------+
| 1.21.5.9.3.2  | Y-Concept      | (279046003,    | Parameter      |
|               |                | SCT,           | $Y-Concept of  |
|               |                | "Pressure")    |                |
+---------------+----------------+----------------+----------------+
| 1.21.5.9.3.3  | Pressure vs    | IMAGE =        | All graphs are |
|               | time           | 1.2.3.         | in the same    |
|               |                | 4.5.6.7.8.9.10 | image in this  |
|               |                |                | example.       |
+---------------+----------------+----------------+----------------+
| 1.21.5.10     | Imaging Agent  |                |                |
|               | Administration |                |                |
|               | Graph          |                |                |
+---------------+----------------+----------------+----------------+
| 1.21.5.10.1   | Referenced     | INJECT         |                |
|               | Imaging Agent  | OR_FLUSH_AGENT |                |
|               | Identifier     |                |                |
+---------------+----------------+----------------+----------------+
| 1.21.5.10.2   | Flow Rate vs   |                | Concept name   |
|               | time           |                | is parameter   |
|               |                |                | $Me            |
|               |                |                | asurementGraph |
|               |                |                | of             |
+---------------+----------------+----------------+----------------+
| 1.21.5.10.2.1 | X-Concept      | (130194, DCM,  | Parameter      |
|               |                | "Time after    | $X-Concept     |
|               |                | the start of   |                |
|               |                | injection")    |                |
+---------------+----------------+----------------+----------------+
| 1.21.5.10.2.2 | Y-Concept      | (122094, DCM,  | Parameter      |
|               |                | "Rate of       | $Y-Concept     |
|               |                | ad             |                |
|               |                | ministration") |                |
+---------------+----------------+----------------+----------------+
| 1.21.5.10.2.3 | Flow Rate vs   | IMAGE =        |                |
|               | time           | 1.2.3.         |                |
|               |                | 4.5.6.7.8.9.10 |                |
+---------------+----------------+----------------+----------------+
| 1.21.5.10.3   | Pressure vs    |                | Concept name   |
|               | time           |                | is parameter   |
|               |                |                | $Me            |
|               |                |                | asurementGraph |
|               |                |                | of             |
+---------------+----------------+----------------+----------------+
| 1.21.5.10.3.1 | X-Concept      | (130194, DCM,  | Parameter      |
|               |                | "Time after    | $X-Concept of  |
|               |                | the start of   |                |
|               |                | injection")    |                |
+---------------+----------------+----------------+----------------+
| 1.21.5.10.3.2 | Y-Concept      | (279046003,    | Parameter      |
|               |                | SCT,           | $Y-Concept of  |
|               |                | "Pressure")    |                |
+---------------+----------------+----------------+----------------+
| 1.21.5.10.3.3 | Pressure vs    | IMAGE =        |                |
|               | time           | 1.2.3.         |                |
|               |                | 4.5.6.7.8.9.10 |                |
+---------------+----------------+----------------+----------------+
| 1.21.5.11     | Number of      | 2              |                |
|               | Injector Heads |                |                |
+---------------+----------------+----------------+----------------+
| 1.21.5.12     | Programmable   | (373066001,    |                |
|               | Device         | SCT, "Yes")    |                |
+---------------+----------------+----------------+----------------+
| 1.21.6        | Imaging Agent  |                |                |
|               | Administration |                |                |
|               | Step           |                |                |
+---------------+----------------+----------------+----------------+
| 1.21.6.1      | Imaging Agent  | DIA            |                |
|               | Administration | GNOSTIC_STEP_4 |                |
|               | Step           |                |                |
|               | Identifier     |                |                |
+---------------+----------------+----------------+----------------+
| 1.21.6.2      | Imaging Agent  | 1.2.3          | Since "Root    |
|               | Administration | .4.47110815.10 | Concept Name   |
|               | Performed Step |                | Code Sequence" |
|               | UID            |                | is "Performed  |
|               |                |                | Imaging Agent  |
|               |                |                | A              |
|               |                |                | dministration" |
+---------------+----------------+----------------+----------------+
| 1.21.6.3      | Administration | (130173, DCM,  |                |
|               | Mode           | "Automated     |                |
|               |                | Ad             |                |
|               |                | ministration") |                |
+---------------+----------------+----------------+----------------+
| 1.21.6.4      | Administration | (130249, DCM,  |                |
|               | Step Type      | "Diagnostic    |                |
|               |                | Ad             |                |
|               |                | ministration") |                |
+---------------+----------------+----------------+----------------+
| 1.21.6.5      | Scan Delay     | 12             | UNITS = EV (s, |
|               |                |                | UCUM, "s")     |
+---------------+----------------+----------------+----------------+
| 1.21.6.6      | Pressure Limit | 15             | UNITS = EV     |
|               |                |                | (kPa, UCUM     |
|               |                |                | "kPa")         |
|               |                |                |                |
|               |                |                | Since 1.21.6.3 |
|               |                |                | is "Automated  |
|               |                |                | A              |
|               |                |                | dministration" |
+---------------+----------------+----------------+----------------+
| 1.21.6.7      | Route of       | (47625008,     |                |
|               | Administration | SCT,           |                |
|               |                | "Intravenous   |                |
|               |                | route")        |                |
+---------------+----------------+----------------+----------------+
| 1.21.6.7.1    | Site of        | (261459001,    | Since "Route   |
|               |                | SCT, "Via arm  | of             |
|               |                | vein")         | A              |
|               |                |                | dministration" |
|               |                |                | is             |
|               |                |                | "Intravenous   |
|               |                |                | route"         |
+---------------+----------------+----------------+----------------+
| 1.21.6.7.1.1  | Laterality     | (7771000, SCT, | Since "Site    |
|               |                | "Left")        | of" is "Via    |
|               |                |                | arm vein"      |
+---------------+----------------+----------------+----------------+
| 1.21.6.8      | Imaging Agent  |                |                |
|               | Administration |                |                |
|               | Phase          |                |                |
+---------------+----------------+----------------+----------------+
| 1.21.6.8.1    | Imaging Agent  | DIAGNOSTIC_INJ |                |
|               | Administration | ECTION_PHASE_1 |                |
|               | Phase          |                |                |
|               | Identifier     |                |                |
+---------------+----------------+----------------+----------------+
| 1.21.6.8.2    | Imaging Agent  | 1.2.3          | Since "Root    |
|               | Administration | .4.47110815.11 | Concept Name   |
|               | Performed      |                | Code Sequence" |
|               | Phase UID      |                | is "Performed  |
|               |                |                | Imaging Agent  |
|               |                |                | A              |
|               |                |                | dministration" |
+---------------+----------------+----------------+----------------+
| 1.21.6.8.3    | Imaging Agent  | (130168, DCM,  | Since 1.21.6.3 |
|               | Administration | "Automatic     | is "Automated  |
|               | Phase Type     | Administration | A              |
|               |                | Phase")        | dministration" |
+---------------+----------------+----------------+----------------+
| 1.21.6.8.4    | Imaging Agent  |                |                |
|               | Administration |                |                |
|               | Activity       |                |                |
+---------------+----------------+----------------+----------------+
| 1.21.6.8.4.1  | Referenced     | INJECTOR_      | Value of       |
|               | Imaging Agent  | CONTRAST_AGENT | 1.14.1         |
|               | Identifier     |                |                |
+---------------+----------------+----------------+----------------+
| 1.21.6.8.4.2  | Volume         | 88             | UNITS = EV     |
|               | Administered   |                | (ml, UCUM,     |
|               |                |                | "ml")          |
|               |                |                |                |
|               |                |                | See 1.21.6.8.6 |
|               |                |                | (Phase Volume) |
|               |                |                | also           |
+---------------+----------------+----------------+----------------+
| 1.21.6.8.4.3  | Starting Flow  | 1.5            | UNITS = EV     |
|               | Rate of        |                | (ml/s, UCUM    |
|               | administration |                | "ml/s")        |
+---------------+----------------+----------------+----------------+
| 1.21.6.8.4.4  | Peak Flow Rate | 1.5            | UNITS = EV     |
|               | in Phase       |                | (ml/s, UCUM    |
|               | Activity       |                | "ml/s")        |
|               |                |                |                |
|               |                |                | Since 1.21.6.3 |
|               |                |                | is "Automated  |
|               |                |                | A              |
|               |                |                | dministration" |
|               |                |                | and "Root      |
|               |                |                | Concept Name   |
|               |                |                | Code Sequence" |
|               |                |                | is "Performed  |
|               |                |                | Imaging Agent  |
|               |                |                | A              |
|               |                |                | dministration" |
+---------------+----------------+----------------+----------------+
| 1.21.6.8.4.5  | Peak Pressure  | 5              | UNITS = EV     |
|               | in Phase       |                | (kPa, UCUM     |
|               | Activity       |                | "kPa")         |
|               |                |                |                |
|               |                |                | Since 1.21.6.3 |
|               |                |                | is "Automated  |
|               |                |                | A              |
|               |                |                | dministration" |
|               |                |                | and "Root      |
|               |                |                | Concept Name   |
|               |                |                | Code Sequence" |
|               |                |                | is "Performed  |
|               |                |                | Imaging Agent  |
|               |                |                | A              |
|               |                |                | dministration" |
+---------------+----------------+----------------+----------------+
| 1.21.6.8.4.6  | Initial Volume | 185            | UNITS = EV     |
|               | of Imaging     |                | (ml, UCUM,     |
|               | Agent in       |                | "ml")          |
|               | Container      |                |                |
|               |                |                | Since "Root    |
|               |                |                | Concept Name   |
|               |                |                | Code Sequence" |
|               |                |                | is "Performed  |
|               |                |                | Imaging Agent  |
|               |                |                | A              |
|               |                |                | dministration" |
+---------------+----------------+----------------+----------------+
| 1.21.6.8.4.7  | Residual       | 97             | UNITS = EV     |
|               | Volume of      |                | (ml, UCUM,     |
|               | Imaging Agent  |                | "ml")          |
|               | in Container   |                |                |
|               |                |                | Since "Root    |
|               |                |                | Concept Name   |
|               |                |                | Code Sequence" |
|               |                |                | is "Performed  |
|               |                |                | Imaging Agent  |
|               |                |                | A              |
|               |                |                | dministration" |
+---------------+----------------+----------------+----------------+
| 1.21.6.8.4.8  | DateTime       | 20181012121900 | Since root     |
|               | Started        |                | Concept Name   |
|               |                |                | is "Performed  |
|               |                |                | Imaging Agent  |
|               |                |                | A              |
|               |                |                | dministration" |
+---------------+----------------+----------------+----------------+
| 1.21.6.8.4.9  | Duration       | 58.6           | UNITS = EV (s, |
|               |                |                | UCUM, "s")     |
|               |                |                |                |
|               |                |                | Since root     |
|               |                |                | Concept Name   |
|               |                |                | is "Performed  |
|               |                |                | Imaging Agent  |
|               |                |                | A              |
|               |                |                | dministration" |
+---------------+----------------+----------------+----------------+
| 1.21.6.8.5    | Imaging Agent  |                |                |
|               | Administration |                |                |
|               | Activity       |                |                |
+---------------+----------------+----------------+----------------+
| 1.21.6.8.5.1  | Referenced     | INJECT         | Value of       |
|               | Imaging Agent  | OR_FLUSH_AGENT | 1.15.1         |
|               | Identifier     |                |                |
+---------------+----------------+----------------+----------------+
| 1.21.6.8.5.2  | Volume         | 88             | UNITS = EV     |
|               | Administered   |                | (ml, UCUM,     |
|               |                |                | "ml")          |
|               |                |                |                |
|               |                |                | See 1.21.6.8.6 |
|               |                |                | (Phase Volume) |
|               |                |                | also           |
+---------------+----------------+----------------+----------------+
| 1.21.6.8.5.3  | Starting Flow  | 1.5            | UNITS = EV     |
|               | Rate of        |                | (ml/s, UCUM    |
|               | administration |                | "ml/s")        |
+---------------+----------------+----------------+----------------+
| 1.21.6.8.5.4  | Peak Flow Rate | 1.5            | UNITS = EV     |
|               | in Phase       |                | (ml/s, UCUM    |
|               | Activity       |                | "ml/s")        |
|               |                |                |                |
|               |                |                | Since 1.21.6.3 |
|               |                |                | is "Automated  |
|               |                |                | A              |
|               |                |                | dministration" |
|               |                |                | and "Root      |
|               |                |                | Concept Name   |
|               |                |                | Code Sequence" |
|               |                |                | is "Performed  |
|               |                |                | Imaging Agent  |
|               |                |                | A              |
|               |                |                | dministration" |
+---------------+----------------+----------------+----------------+
| 1.21.6.8.5.5  | Peak Pressure  | 5              | UNITS = EV     |
|               | in Phase       |                | (kPa, UCUM     |
|               | Activity       |                | "kPa")         |
|               |                |                |                |
|               |                |                | Since 1.21.6.3 |
|               |                |                | is "Automated  |
|               |                |                | A              |
|               |                |                | dministration" |
|               |                |                | and "Root      |
|               |                |                | Concept Name   |
|               |                |                | Code Sequence" |
|               |                |                | is "Performed  |
|               |                |                | Imaging Agent  |
|               |                |                | A              |
|               |                |                | dministration" |
+---------------+----------------+----------------+----------------+
| 1.21.6.8.5.6  | Initial Volume | 134            | UNITS = EV     |
|               | of Imaging     |                | (ml, UCUM,     |
|               | Agent in       |                | "ml")          |
|               | Container      |                |                |
|               |                |                | Value results  |
|               |                |                | from 136ml -   |
|               |                |                | 2ml KVO within |
|               |                |                | 1 min 10 sec   |
|               |                |                | until now      |
|               |                |                |                |
|               |                |                | Since "Root    |
|               |                |                | Concept Name   |
|               |                |                | Code Sequence" |
|               |                |                | is "Performed  |
|               |                |                | Imaging Agent  |
|               |                |                | A              |
|               |                |                | dministration" |
+---------------+----------------+----------------+----------------+
| 1.21.6.8.5.7  | Residual       | 46             | UNITS = EV     |
|               | Volume of      |                | (ml, UCUM,     |
|               | Imaging Agent  |                | "ml")          |
|               | in Container   |                |                |
|               |                |                | Since "Root    |
|               |                |                | Concept Name   |
|               |                |                | Code Sequence" |
|               |                |                | is "Performed  |
|               |                |                | Imaging Agent  |
|               |                |                | A              |
|               |                |                | dministration" |
+---------------+----------------+----------------+----------------+
| 1.21.6.8.5.8  | DateTime       | 20181012121900 | Since root     |
|               | Started        |                | Concept Name   |
|               |                |                | is "Performed  |
|               |                |                | Imaging Agent  |
|               |                |                | A              |
|               |                |                | dministration" |
+---------------+----------------+----------------+----------------+
| 1.21.6.8.5.9  | Duration       | 58.6           | UNITS = EV (s, |
|               |                |                | UCUM, "s")     |
|               |                |                |                |
|               |                |                | Since root     |
|               |                |                | Concept Name   |
|               |                |                | is "Performed  |
|               |                |                | Imaging Agent  |
|               |                |                | A              |
|               |                |                | dministration" |
+---------------+----------------+----------------+----------------+
| 1.21.6.8.6    | Total Phase    | 176            | UNITS = EV     |
|               | Volume         |                | (ml, UCUM,     |
|               | Administered   |                | "ml")          |
|               |                |                |                |
|               |                |                | Sum of         |
|               |                |                | 1.21.6.8.4.2   |
|               |                |                | and            |
|               |                |                | 1.21.6.8.5.2   |
+---------------+----------------+----------------+----------------+
| 1.21.6.8.7    | DateTime       | 20181012121900 | Since root     |
|               | Started        |                | Concept Name   |
|               |                |                | Code Sequence  |
|               |                |                | is "Performed  |
|               |                |                | Imaging Agent  |
|               |                |                | A              |
|               |                |                | dministration" |
+---------------+----------------+----------------+----------------+
| 1.21.6.8.8    | Duration       | 58.56          | UNITS = EV (s, |
|               |                |                | UCUM, "s")     |
|               |                |                |                |
|               |                |                | Since root     |
|               |                |                | Concept Name   |
|               |                |                | Code Sequence  |
|               |                |                | is "Performed  |
|               |                |                | Imaging Agent  |
|               |                |                | Ad             |
|               |                |                | ministration") |
+---------------+----------------+----------------+----------------+
| 1.21.6.9      | Imaging Agent  |                |                |
|               | Administration |                |                |
|               | Phase          |                |                |
+---------------+----------------+----------------+----------------+
| 1.21.6.9.1    | Imaging Agent  | DIAGNOSTIC_INJ |                |
|               | Administration | ECTION_PHASE_2 |                |
|               | Phase          |                |                |
|               | Identifier     |                |                |
+---------------+----------------+----------------+----------------+
| 1.21.6.9.2    | Imaging Agent  | 1.2.3          | Since "Root    |
|               | Administration | .4.47110815.12 | Concept Name   |
|               | Performed      |                | Code Sequence" |
|               | Phase UID      |                | is "Performed  |
|               |                |                | Imaging Agent  |
|               |                |                | A              |
|               |                |                | dministration" |
+---------------+----------------+----------------+----------------+
| 1.21.6.9.3    | Imaging Agent  | (130168, DCM,  | Since 1.21.6.3 |
|               | Administration | "Automatic     | is "Automated  |
|               | Phase Type     | Administration | A              |
|               |                | Phase")        | dministration" |
+---------------+----------------+----------------+----------------+
| 1.21.6.9.4    | Imaging Agent  |                |                |
|               | Administration |                |                |
|               | Activity       |                |                |
+---------------+----------------+----------------+----------------+
| 1.21.6.9.4.1  | Referenced     | INJECT         | Value of       |
|               | Imaging Agent  | OR_FLUSH_AGENT | 1.15.1         |
|               | Identifier     |                |                |
+---------------+----------------+----------------+----------------+
| 1.21.6.9.4.2  | Volume         | 30             | UNITS = EV     |
|               | Administered   |                | (ml, UCUM,     |
|               |                |                | "ml")          |
|               |                |                |                |
|               |                |                | Same value as  |
|               |                |                | 1.21.6.9.5     |
+---------------+----------------+----------------+----------------+
| 1.21.6.9.4.3  | Starting Flow  | 3              | UNITS = EV     |
|               | Rate of        |                | (ml/s, UCUM    |
|               | administration |                | "ml/s")        |
+---------------+----------------+----------------+----------------+
| 1.21.6.9.4.4  | Peak Flow Rate | 3              | UNITS = EV     |
|               | in Phase       |                | (ml/s, UCUM    |
|               | Activity       |                | "ml/s")        |
|               |                |                |                |
|               |                |                | Since 1.21.6.3 |
|               |                |                | is "Automated  |
|               |                |                | A              |
|               |                |                | dministration" |
|               |                |                | and "Root      |
|               |                |                | Concept Name   |
|               |                |                | Code Sequence" |
|               |                |                | is "Performed  |
|               |                |                | Imaging Agent  |
|               |                |                | A              |
|               |                |                | dministration" |
+---------------+----------------+----------------+----------------+
| 1.21.6.9.4.5  | Peak Pressure  | 5              | UNITS = EV     |
|               | in Phase       |                | (kPa, UCUM     |
|               | Activity       |                | "kPa")         |
|               |                |                |                |
|               |                |                | Since 1.21.6.3 |
|               |                |                | is "Automated  |
|               |                |                | A              |
|               |                |                | dministration" |
|               |                |                | and "Root      |
|               |                |                | Concept Name   |
|               |                |                | Code Sequence" |
|               |                |                | is "Performed  |
|               |                |                | Imaging Agent  |
|               |                |                | A              |
|               |                |                | dministration" |
+---------------+----------------+----------------+----------------+
| 1.21.6.9.4.6  | Initial Volume | 46             | UNITS = EV     |
|               | of Imaging     |                | (ml, UCUM,     |
|               | Agent in       |                | "ml")          |
|               | Container      |                |                |
|               |                |                | Since "Root    |
|               |                |                | Concept Name   |
|               |                |                | Code Sequence" |
|               |                |                | is "Performed  |
|               |                |                | Imaging Agent  |
|               |                |                | A              |
|               |                |                | dministration" |
+---------------+----------------+----------------+----------------+
| 1.21.6.9.4.7  | Residual       | 16             | UNITS = EV     |
|               | Volume of      |                | (ml, UCUM,     |
|               | Imaging Agent  |                | "ml")          |
|               | in Container   |                |                |
|               |                |                | Since "Root    |
|               |                |                | Concept Name   |
|               |                |                | Code Sequence" |
|               |                |                | is "Performed  |
|               |                |                | Imaging Agent  |
|               |                |                | A              |
|               |                |                | dministration" |
+---------------+----------------+----------------+----------------+
| 1.21.6.9.4.8  | DateTime       | 201            | Since root     |
|               | Started        | 81012121958.56 | Concept Name   |
|               |                |                | is "Performed  |
|               |                |                | Imaging Agent  |
|               |                |                | A              |
|               |                |                | dministration" |
+---------------+----------------+----------------+----------------+
| 1.21.6.9.4.9  | Duration       | 10             | UNITS = EV (s, |
|               |                |                | UCUM, "s")     |
|               |                |                |                |
|               |                |                | Since root     |
|               |                |                | Concept Name   |
|               |                |                | is "Performed  |
|               |                |                | Imaging Agent  |
|               |                |                | A              |
|               |                |                | dministration" |
+---------------+----------------+----------------+----------------+
| 1.21.6.9.5    | Total Phase    | 30             | UNITS = EV     |
|               | Volume         |                | (ml, UCUM,     |
|               | Administered   |                | "ml")          |
|               |                |                |                |
|               |                |                | Same value as  |
|               |                |                | 1.21.6.9.4.2   |
+---------------+----------------+----------------+----------------+
| 1.21.6.9.6    | DateTime       | 201            | Since root     |
|               | Started        | 81012121958.56 | Concept Name   |
|               |                |                | Code Sequence  |
|               |                |                | is "Performed  |
|               |                |                | Imaging Agent  |
|               |                |                | A              |
|               |                |                | dministration" |
+---------------+----------------+----------------+----------------+
| 1.21.6.9.7    | Duration       | 10             | UNITS = EV (s, |
|               |                |                | UCUM, "s")     |
|               |                |                |                |
|               |                |                | Since root     |
|               |                |                | Concept Name   |
|               |                |                | Code Sequence  |
|               |                |                | is "Performed  |
|               |                |                | Imaging Agent  |
|               |                |                | Ad             |
|               |                |                | ministration") |
+---------------+----------------+----------------+----------------+
| 1.21.6.10     | Imaging Agent  |                |                |
|               | Administration |                |                |
|               | Graph          |                |                |
+---------------+----------------+----------------+----------------+
| 1.21.6.10.1   | Referenced     | INJECTOR_      |                |
|               | Imaging Agent  | CONTRAST_AGENT |                |
|               | Identifier     |                |                |
+---------------+----------------+----------------+----------------+
| 1.21.6.10.2   | Flow Rate vs   |                | Concept name   |
|               | time           |                | is parameter   |
|               |                |                | $Me            |
|               |                |                | asurementGraph |
+---------------+----------------+----------------+----------------+
| 1.21.6.10.2.1 | X-Concept      | (130194, DCM,  | Parameter      |
|               |                | "Time after    | $X-Concept     |
|               |                | the start of   |                |
|               |                | injection")    |                |
+---------------+----------------+----------------+----------------+
| 1.21.6.10.2.2 | Y-Concept      | (122094, DCM,  | Parameter      |
|               |                | "Rate of       | $Y-Concept     |
|               |                | ad             |                |
|               |                | ministration") |                |
+---------------+----------------+----------------+----------------+
| 1.21.6.10.2.3 | Flow Rate vs   | IMAGE =        |                |
|               | time           | 1.2.3.         |                |
|               |                | 4.5.6.7.8.9.11 |                |
+---------------+----------------+----------------+----------------+
| 1.21.6.10.3   | Pressure vs    |                | Named by       |
|               | time           |                | parameter      |
|               |                |                | $Me            |
|               |                |                | asurementGraph |
+---------------+----------------+----------------+----------------+
| 1.21.6.10.3.1 | X-Concept      | (130194, DCM,  | Parameter      |
|               |                | "Time after    | $X-Concept     |
|               |                | the start of   |                |
|               |                | injection")    |                |
+---------------+----------------+----------------+----------------+
| 1.21.6.10.3.2 | Y-Concept      | (279046003,    | Parameter      |
|               |                | SCT,           | $Y-Concept     |
|               |                | "Pressure")    |                |
+---------------+----------------+----------------+----------------+
| 1.21.6.10.3.3 | Pressure vs    | IMAGE =        |                |
|               | time           | 1.2.3.         |                |
|               |                | 4.5.6.7.8.9.11 |                |
+---------------+----------------+----------------+----------------+
| 1.21.6.11     | Imaging Agent  |                |                |
|               | Administration |                |                |
|               | Graph          |                |                |
+---------------+----------------+----------------+----------------+
| 1.21.6.11.1   | Referenced     | INJECT         |                |
|               | Imaging Agent  | OR_FLUSH_AGENT |                |
|               | Identifier     |                |                |
+---------------+----------------+----------------+----------------+
| 1.21.6.11.2   | Flow Rate vs   |                | Concept name   |
|               | time           |                | is parameter   |
|               |                |                | $Me            |
|               |                |                | asurementGraph |
+---------------+----------------+----------------+----------------+
| 1.21.6.11.2.1 | X-Concept      | (130194, DCM,  | Parameter      |
|               |                | "Time after    |                |
|               |                | the start of   |                |
|               |                | injection")    |                |
+---------------+----------------+----------------+----------------+
| 1.21.6.11.2.2 | Y-Concept      | (122094, DCM,  | Parameter      |
|               |                | "Rate of       | $Y-Concept     |
|               |                | ad             |                |
|               |                | ministration") |                |
+---------------+----------------+----------------+----------------+
| 1.21.6.11.2.3 | Flow Rate vs   | IMAGE =        |                |
|               | time           | 1.2.3.         |                |
|               |                | 4.5.6.7.8.9.11 |                |
+---------------+----------------+----------------+----------------+
| 1.21.6.11.3   | Pressure vs    |                | Named by       |
|               | time           |                | parameter      |
|               |                |                | $Me            |
|               |                |                | asurementGraph |
+---------------+----------------+----------------+----------------+
| 1.21.6.11.3.1 | X-Concept      | (130194, DCM,  | Parameter      |
|               |                | "Time after    | $X-Concept     |
|               |                | the start of   |                |
|               |                | injection")    |                |
+---------------+----------------+----------------+----------------+
| 1.21.6.11.3.2 | Y-Concept      | (279046003,    | Parameter      |
|               |                | SCT,           | $Y-Concept     |
|               |                | "Pressure")    |                |
+---------------+----------------+----------------+----------------+
| 1.21.6.11.3.3 | Pressure vs    | IMAGE =        |                |
|               | time           | 1.2.3.         |                |
|               |                | 4.5.6.7.8.9.11 |                |
+---------------+----------------+----------------+----------------+
| 1.21.6.12     | Number of      | 2              |                |
|               | Injector Heads |                |                |
+---------------+----------------+----------------+----------------+
| 1.21.6.13     | Programmable   | (373066001,    |                |
|               | Device         | SCT, "Yes")    |                |
+---------------+----------------+----------------+----------------+
| 1.22          | Planned        | 1.2.3          | SInce this     |
|               | Imaging Agent  | .4.47110815.13 | administration |
|               | Administration |                | was based on a |
|               | SOP Instance   |                | Imaging        |
|               |                |                | Administration |
|               |                |                | Plan           |
+---------------+----------------+----------------+----------------+
| 1.23          | Imaging Agent  | (255594003,    |                |
|               | Administration | SCT,           |                |
|               | Completion     | "Complete")    |                |
|               | Status         |                |                |
+---------------+----------------+----------------+----------------+
| 1.24          | Imaging Agent  |                |                |
|               | Administration |                |                |
|               | Adverse Events |                |                |
+---------------+----------------+----------------+----------------+
| 1.24.1        | Administration | (373067005,    |                |
|               | discontinued   | SCT, "No")     |                |
+---------------+----------------+----------------+----------------+
| 1.24.2        | Adverse Event  | (415690000,    |                |
|               |                | SCT,           |                |
|               |                | "Sweating")    |                |
+---------------+----------------+----------------+----------------+
| 1.24.2.1      | Severity       | (255604002,    |                |
|               |                | SCT, "Mild")   |                |
+---------------+----------------+----------------+----------------+
| 1.24.2.2      | Relative Time  | (307153007,    |                |
|               |                | SCT, "Before   |                |
|               |                | Procedure")    |                |
+---------------+----------------+----------------+----------------+
| 1.24.2.3      | Adverse Event  | 20181012121500 |                |
|               | Detection      |                |                |
|               | DateTime       |                |                |
+---------------+----------------+----------------+----------------+
| 1.24.2.4      | Referenced     | 1.2.           | Same value as  |
|               | Imaging Agent  | 3.4.47110815.5 | 1.21.4.2       |
|               | Administration |                |                |
|               | Step UID       |                |                |
+---------------+----------------+----------------+----------------+
| 1.24.2.5      | Referenced     | 1.2.           | Same value as  |
|               | Imaging Agent  | 3.4.47110815.6 |                |
|               | Administration |                | 1.21.4.6.2     |
|               | Phase UID      |                |                |
+---------------+----------------+----------------+----------------+
| 1.24.2.6      | Comment        | Patient was    |                |
|               |                | afraid of      |                |
|               |                | procedure      |                |
+---------------+----------------+----------------+----------------+
| 1.24.3        | Adverse Event  | (95384003,     |                |
|               |                | SCT,           |                |
|               |                | "Injection     |                |
|               |                | Site           |                |
|               |                | E              |                |
|               |                | xtravasation") |                |
+---------------+----------------+----------------+----------------+
| 1.24.3.1      | Relative Time  | (303110006,    |                |
|               |                | SCT, "After    |                |
|               |                | Procedure")    |                |
+---------------+----------------+----------------+----------------+
| 1.24.3.2      | Adverse Event  | 20181012122100 |                |
|               | Detection      |                |                |
|               | DateTime       |                |                |
+---------------+----------------+----------------+----------------+
| 1.24.3.3      | Estimated      | 2              | UNITS = EV     |
|               | Extravasation  |                | (ml, UCUM,     |
|               | Volume         |                | "ml")          |
|               |                |                |                |
|               |                |                | Since 1.17.3   |
|               |                |                | is "Injection  |
|               |                |                | Site           |
|               |                |                | Extravasation" |
+---------------+----------------+----------------+----------------+
| 1.24.3.4      | Referenced     | 1.2.3          | Same value as  |
|               | Imaging Agent  | .4.47110815.10 |                |
|               | Administration |                | 1.21.6.2       |
|               | Step UID       |                |                |
+---------------+----------------+----------------+----------------+
| 1.24.3.5      | Referenced     | 1.2.3          | Same value as  |
|               | Imaging Agent  | .4.47110815.12 |                |
|               | Administration |                | 1.21.6.9.2     |
|               | Phase UID      |                |                |
+---------------+----------------+----------------+----------------+
| 1.24.3.6      | Comment        | Detected       |                |
|               |                | extravasation  |                |
|               |                | when removing  |                |
|               |                | needle         |                |
+---------------+----------------+----------------+----------------+
| 1.25          | Imaging Agent  |                |                |
|               | Administration |                |                |
|               | Injector       |                |                |
|               | Events         |                |                |
+---------------+----------------+----------------+----------------+
| 1.25.1        | Administration | (373067005,    |                |
|               | discontinued   | SCT, "No")     |                |
+---------------+----------------+----------------+----------------+
| 1.25.2        | Imaging Agent  | (130161, DCM,  |                |
|               | Administration | "Keep vein     |                |
|               | Injector Event | open started") |                |
|               | Type           |                |                |
+---------------+----------------+----------------+----------------+
| 1.25.2.1      | Injector Event | 20181012121628 |                |
|               | Detection      |                |                |
|               | DateTime       |                |                |
+---------------+----------------+----------------+----------------+
| 1.25.2.2      | Referenced     | INJECT         |                |
|               | Imaging Agent  | OR_FLUSH_AGENT |                |
|               | Identifier     |                |                |
+---------------+----------------+----------------+----------------+
| 1.25.3        | Imaging Agent  | (130162, DCM,  |                |
|               | Administration | "Keep vein     |                |
|               | Injector Event | open ended")   |                |
|               | Type           |                |                |
+---------------+----------------+----------------+----------------+
| 1.25.3.1      | Injector Event | 20181012121958 |                |
|               | Detection      |                |                |
|               | DateTime       |                |                |
+---------------+----------------+----------------+----------------+
| 1.25.3.2      | Referenced     | INJECT         |                |
|               | Imaging Agent  | OR_FLUSH_AGENT |                |
|               | Identifier     |                |                |
+---------------+----------------+----------------+----------------+
| 1.26          | Total Keep     | 3              | UNITS = EV     |
|               | Vein Open      |                | (ml, UCUM,     |
|               | Volume         |                | "ml")          |
|               | Administered   |                |                |
+---------------+----------------+----------------+----------------+

