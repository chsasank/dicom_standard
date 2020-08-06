.. _chapter_YYY:

Preclinical Small Animal Imaging Acquisition Context (Informative)
==================================================================

.. _sect_YYY.1:

This Annex describes the use of Preclinical Small Animal Imaging
Acquisition Context.

.. _sect_YYY.1.1:

Example of housing and anesthesia for PET-CT
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

This Section contains examples for use cases involving imaging of a
single animal in a hybrid PET-CT system.

The basic use case involves an animal, which:

-  lives in an individually ventilated home cage with several other
   animals in the same cage

-  is (briefly) transported (in its home cage) with its cage mates to
   the imaging facility, without heating, with an appropriate lid

-  is removed from its home/transport cage for preparation for imaging,
   involving insertion of a tail vein cannula, performed on an
   electrically heated pad

-  is induced by (a) placement in an induction chamber with more
   concentrated volatile anesthetic, or (b) intraperitoneal injection of
   Ketamine mixture

-  is placed in a PET-CT compatible imaging sled/carrier/chamber for
   imaging (of one animal at a time), with anesthesia with Isoflurane
   and Oxygen as the carrier gas, and heated with an electric pad
   regulated by feedback from a rectal probe

-  is removed for recovery in a separate cage

The content tree structure (when induction is by a volatile anesthetic)
would resemble:

+--------------+----------------------+----------------------+-----+
| Node         | Code Meaning of      | Code Meaning or      | TID |
|              | Concept Name         | Example Value        |     |
+==============+======================+======================+=====+
| 1            | Preclinical Small    |                      |     |
|              | Animal Imaging       |                      |     |
|              | Acquisition Context  |                      |     |
+--------------+----------------------+----------------------+-----+
| 1.1          | Language of Content  | English              |     |
|              | Item and Descendants |                      |     |
+--------------+----------------------+----------------------+-----+
| 1.1.1        | Country of Language  | United States        |     |
+--------------+----------------------+----------------------+-----+
| 1.2          | Person Observer Name | Doe^Jane             |     |
+--------------+----------------------+----------------------+-----+
| 1.3          | Procedure Code       | PET/CT FDG imaging   |     |
|              |                      | of whole body        |     |
+--------------+----------------------+----------------------+-----+
| 1.4          | Biosafety conditions |                      |     |
+--------------+----------------------+----------------------+-----+
| 1.4.1        | Biosafety level      | Biosafety level 1    |     |
+--------------+----------------------+----------------------+-----+
| 1.5          | Animal handling      |                      |     |
|              | during specified     |                      |     |
|              | phase                |                      |     |
+--------------+----------------------+----------------------+-----+
| 1.5.1        | Phase of animal      | In home cage         |     |
|              | handling             |                      |     |
+--------------+----------------------+----------------------+-----+
| 1.5.2        | Animal housing       |                      |     |
+--------------+----------------------+----------------------+-----+
| 1.5.2.1      | Housing manufacturer | Acme Inc.            |     |
+--------------+----------------------+----------------------+-----+
| 1.5.2.2      | Housing rack product | Acmerack IVC Mouse   |     |
|              | name                 |                      |     |
+--------------+----------------------+----------------------+-----+
| 1.5.2.3      | Housing unit product | Acmecage Mouse       |     |
|              | name                 | Pre-Bedded Corn Cob  |     |
|              |                      | with Enrichment      |     |
+--------------+----------------------+----------------------+-----+
| 1.5.2.4      | Housing unit product | 12345                |     |
|              | code                 |                      |     |
+--------------+----------------------+----------------------+-----+
| 1.5.2.5      | Housing unit lid     | Acmecage IVC Mouse   |     |
|              | product name         | Single Filter        |     |
+--------------+----------------------+----------------------+-----+
| 1.5.2.6      | Housing unit lid     | 6789                 |     |
|              | product code         |                      |     |
+--------------+----------------------+----------------------+-----+
| 1.5.2.7      | Number of racks per  | 4 {racks}            |     |
|              | room                 |                      |     |
+--------------+----------------------+----------------------+-----+
| 1.5.2.8      | Number of housing    | 154 {housing units}  |     |
|              | units per rack       |                      |     |
+--------------+----------------------+----------------------+-----+
| 1.5.2.9      | Housing unit         | Row 4 Column 7       |     |
|              | location in rack     |                      |     |
+--------------+----------------------+----------------------+-----+
| 1.5.2.10     | Number of animals    | 5 {animals}          |     |
|              | within same housing  |                      |     |
|              | unit                 |                      |     |
+--------------+----------------------+----------------------+-----+
| 1.5.2.11     | Sex of animals       | Female               |     |
|              | within same housing  |                      |     |
|              | unit                 |                      |     |
+--------------+----------------------+----------------------+-----+
| 1.5.2.12     | Sex of handler       | Mixed sex            |     |
+--------------+----------------------+----------------------+-----+
| 1.5.2.13     | Total duration in    | 133 days             |     |
|              | housing              |                      |     |
+--------------+----------------------+----------------------+-----+
| 1.5.2.14     | Housing change       | 7 days               |     |
|              | interval             |                      |     |
+--------------+----------------------+----------------------+-----+
| 1.5.2.15     | Manual handling      | 24 hours             |     |
|              | interval             |                      |     |
+--------------+----------------------+----------------------+-----+
| 1.5.2.16     | Housing unit width   | 23.4 cm              |     |
+--------------+----------------------+----------------------+-----+
| 1.5.2.17     | Housing unit height  | 14.0 cm              |     |
+--------------+----------------------+----------------------+-----+
| 1.5.2.18     | Housing unit length  | 37.3 cm              |     |
+--------------+----------------------+----------------------+-----+
| 1.5.2.19     | Housing individually | Yes                  |     |
|              | ventilated           |                      |     |
+--------------+----------------------+----------------------+-----+
| 1.5.2.20     | Air changes          | 50 /hour             |     |
+--------------+----------------------+----------------------+-----+
| 1.5.2.21     | Environmental        | 22 C                 |     |
|              | temperature          |                      |     |
+--------------+----------------------+----------------------+-----+
| 1.5.2.22     | Housing humidity     | 50 %                 |     |
+--------------+----------------------+----------------------+-----+
| 1.5.2.23     | Housing unit reuse   | Unused               |     |
+--------------+----------------------+----------------------+-----+
| 1.5.2.24     | Bedding material     | Corn cob bedding     |     |
+--------------+----------------------+----------------------+-----+
| 1.5.2.25     | Bedding volume       | 450 ml               |     |
+--------------+----------------------+----------------------+-----+
| 1.5.2.26     | Enrichment material  | Acmerichment paper   |     |
|              |                      | twists               |     |
+--------------+----------------------+----------------------+-----+
| 1.5.2.27     | Exerciser device     | Acmewheel            |     |
+--------------+----------------------+----------------------+-----+
| 1.5.2.28     | Shelter type         | Red translucent      |     |
|              |                      | igloo                |     |
+--------------+----------------------+----------------------+-----+
| 1.5.2.29     | Shelter manufacturer | Acme Inc.            |     |
+--------------+----------------------+----------------------+-----+
| 1.5.2.30     | Shelter product name | Acmedome             |     |
+--------------+----------------------+----------------------+-----+
| 1.6          | Animal handling      |                      |     |
|              | during specified     |                      |     |
|              | phase                |                      |     |
+--------------+----------------------+----------------------+-----+
| 1.6.1        | Phase of animal      | During transport     |     |
|              | handling             |                      |     |
+--------------+----------------------+----------------------+-----+
| 1.6.2        | Animal housing       |                      |     |
+--------------+----------------------+----------------------+-----+
| 1.6.2.1      | Housing manufacturer | Acme Inc.            |     |
+--------------+----------------------+----------------------+-----+
| 1.6.2.2      | Housing unit product | Acmecage Mouse       |     |
|              | name                 | Pre-Bedded Corn Cob  |     |
|              |                      | with Enrichment      |     |
+--------------+----------------------+----------------------+-----+
| 1.6.2.3      | Housing unit product | 12345                |     |
|              | code                 |                      |     |
+--------------+----------------------+----------------------+-----+
| 1.6.2.4      | Housing unit lid     | Acmecage Mouse       |     |
|              | product name         | Transport            |     |
+--------------+----------------------+----------------------+-----+
| 1.6.2.5      | Housing unit lid     | 9872                 |     |
|              | product code         |                      |     |
+--------------+----------------------+----------------------+-----+
| 1.6.2.6      | Number of animals    | 5 {animals}          |     |
|              | within same housing  |                      |     |
|              | unit                 |                      |     |
+--------------+----------------------+----------------------+-----+
| 1.6.2.7      | Sex of animals       | Female               |     |
|              | within same housing  |                      |     |
|              | unit                 |                      |     |
+--------------+----------------------+----------------------+-----+
| 1.6.3        | Heating conditions   |                      |     |
+--------------+----------------------+----------------------+-----+
| 1.6.3.1      | Heating              | Unheated             |     |
+--------------+----------------------+----------------------+-----+
| 1.7          | Animal handling      |                      |     |
|              | during specified     |                      |     |
|              | phase                |                      |     |
+--------------+----------------------+----------------------+-----+
| 1.7.1        | Phase of animal      | Staging prior to     |     |
|              | handling             | imaging              |     |
+--------------+----------------------+----------------------+-----+
| 1.8          | Animal handling      |                      |     |
|              | during specified     |                      |     |
|              | phase                |                      |     |
+--------------+----------------------+----------------------+-----+
| 1.8.1        | Phase of animal      | Preparation for      |     |
|              | handling             | imaging              |     |
+--------------+----------------------+----------------------+-----+
| 1.8.2        | Animal housing       |                      |     |
+--------------+----------------------+----------------------+-----+
| 1.8.2.1      | Comment              | Animal exposed and   |     |
|              |                      | restrained whilst    |     |
|              |                      | cannulating tail     |     |
|              |                      | vein                 |     |
+--------------+----------------------+----------------------+-----+
| 1.8.3        | Heating conditions   |                      |     |
+--------------+----------------------+----------------------+-----+
| 1.8.3.1      | Heating              | Electric heating pad |     |
+--------------+----------------------+----------------------+-----+
| 1.8.3.2      | Feedback temperature | No                   |     |
|              | regulation           |                      |     |
+--------------+----------------------+----------------------+-----+
| 1.9          | Animal handling      |                      |     |
|              | during specified     |                      |     |
|              | phase                |                      |     |
+--------------+----------------------+----------------------+-----+
| 1.9.1        | Phase of animal      | Anesthesia induction |     |
|              | handling             |                      |     |
+--------------+----------------------+----------------------+-----+
| 1.9.2        | Animal housing       |                      |     |
+--------------+----------------------+----------------------+-----+
| 1.9.2.1      | Housing manufacturer | Acme Inc             |     |
+--------------+----------------------+----------------------+-----+
| 1.9.2.2      | Housing unit product | Gas Anesthesia       |     |
|              | name                 | Induction Chamber    |     |
|              |                      | Mouse                |     |
+--------------+----------------------+----------------------+-----+
| 1.9.2.3      | Housing unit product | 3487236              |     |
|              | code                 |                      |     |
+--------------+----------------------+----------------------+-----+
| 1.10         | Animal handling      |                      |     |
|              | during specified     |                      |     |
|              | phase                |                      |     |
+--------------+----------------------+----------------------+-----+
| 1.10.1       | Phase of animal      | Imaging procedure    |     |
|              | handling             |                      |     |
+--------------+----------------------+----------------------+-----+
| 1.10.2       | DateTime Started     | yyyymmddhhss         |     |
+--------------+----------------------+----------------------+-----+
| 1.10.3       | DateTime Ended       | yyyymmddhhss         |     |
+--------------+----------------------+----------------------+-----+
| 1.10.4       | Animal housing       |                      |     |
+--------------+----------------------+----------------------+-----+
| 1.10.4.1     | Housing manufacturer | Acme Inc             |     |
+--------------+----------------------+----------------------+-----+
| 1.10.4.2     | Housing unit product | Multimodal Mouse     |     |
|              | name                 | Chamber              |     |
+--------------+----------------------+----------------------+-----+
| 1.10.5       | Heating conditions   |                      |     |
+--------------+----------------------+----------------------+-----+
| 1.10.5.1     | Heating              | Electric heating pad |     |
+--------------+----------------------+----------------------+-----+
| 1.10.5.1     | Feedback temperature | Yes                  |     |
|              | regulation           |                      |     |
+--------------+----------------------+----------------------+-----+
| 1.10.5.2     | Temperature sensor   | Rectal temperature   |     |
|              | device component     |                      |     |
+--------------+----------------------+----------------------+-----+
| 1.10.5.3     | Equipment            | 37 C                 |     |
|              | Temperature          |                      |     |
+--------------+----------------------+----------------------+-----+
| 1.10.6       | Physiological        |                      |     |
|              | monitoring           |                      |     |
+--------------+----------------------+----------------------+-----+
| 1.10.6.1     | Electrocardiographic | Yes                  |     |
|              | monitoring           |                      |     |
+--------------+----------------------+----------------------+-----+
| 1.10.6.2     | Monitoring of        | No                   |     |
|              | respiration          |                      |     |
+--------------+----------------------+----------------------+-----+
| 1.11         | Animal handling      |                      |     |
|              | during specified     |                      |     |
|              | phase                |                      |     |
+--------------+----------------------+----------------------+-----+
| 1.11.1       | Phase of animal      | Anesthesia recovery  |     |
|              | handling             | period               |     |
+--------------+----------------------+----------------------+-----+
| 1.12         | Administration of    |                      |     |
|              | anesthesia           |                      |     |
+--------------+----------------------+----------------------+-----+
| 1.12.1       | Anesthesia Method    |                      |     |
|              | Set                  |                      |     |
+--------------+----------------------+----------------------+-----+
| 1.12.1.1     | Anesthesia Method    |                      |     |
+--------------+----------------------+----------------------+-----+
| 1.12.1.1.1   | Anesthesia Category  | General anesthesia   |     |
+--------------+----------------------+----------------------+-----+
| 1.12.1.1.2   | Anesthesia Start     | yyyymmddhhss         |     |
|              | Time                 |                      |     |
+--------------+----------------------+----------------------+-----+
| 1.12.1.1.3   | Anesthesia Finish    | yyyymmddhhss         |     |
|              | Time                 |                      |     |
+--------------+----------------------+----------------------+-----+
| 1.12.1.1.4   | Anesthesia Induction | By inhalation        |     |
+--------------+----------------------+----------------------+-----+
| 1.12.1.1.5   | Anesthesia           | Inhalation           |     |
|              | Maintenance          | anesthesia system    |     |
|              |                      | closed no            |     |
|              |                      | rebreathing primary  |     |
|              |                      | agent                |     |
+--------------+----------------------+----------------------+-----+
| 1.12.2       | Airway Management    |                      |     |
|              | Set                  |                      |     |
+--------------+----------------------+----------------------+-----+
| 1.12.2.1     | Airway Management    |                      |     |
+--------------+----------------------+----------------------+-----+
| 1.12.2.1.1   | Airway Management    | Nose cone            |     |
|              | Method               |                      |     |
+--------------+----------------------+----------------------+-----+
| 1.12.2.1.2   | Airway               | Continuous flow      |     |
|              | Sub-Management       | ventilation          |     |
|              | Method               |                      |     |
+--------------+----------------------+----------------------+-----+
| 1.12.3       | Medications Set      |                      |     |
+--------------+----------------------+----------------------+-----+
| 1.12.3.1     | Procedure Phase      | During procedure     |     |
+--------------+----------------------+----------------------+-----+
| 1.12.3.2     | Medication given     |                      |     |
+--------------+----------------------+----------------------+-----+
| 1.12.3.2.1   | Drug start           | yyyymmddhhss         |     |
+--------------+----------------------+----------------------+-----+
| 1.12.3.2.2   | Drug end             | yyyymmddhhss         |     |
+--------------+----------------------+----------------------+-----+
| 1.12.3.2.3   | Route of             | By inhalation        |     |
|              | administration       |                      |     |
+--------------+----------------------+----------------------+-----+
| 1.12.3.2.4   | Mixture              |                      |     |
+--------------+----------------------+----------------------+-----+
| 1.12.3.2.4.1 | Drug administered    | Isoflurane           |     |
+--------------+----------------------+----------------------+-----+
| 1.12.3.2.4.2 | Medication Type      | General anesthetic   |     |
+--------------+----------------------+----------------------+-----+
| 1.12.3.2.4.3 | Concentration        | 4 %                  |     |
+--------------+----------------------+----------------------+-----+
| 1.12.3.2.5   | Mixture              |                      |     |
+--------------+----------------------+----------------------+-----+
| 1.12.3.2.5.1 | Drug administered    | Oxygen gas           |     |
+--------------+----------------------+----------------------+-----+
| 1.12.3.2.5.2 | Medication Type      | Carrier gas          |     |
+--------------+----------------------+----------------------+-----+
| 1.12.3.2.5.3 | Concentration        | 100 %                |     |
+--------------+----------------------+----------------------+-----+
| 1.12.3.3     | Medication given     |                      |     |
+--------------+----------------------+----------------------+-----+
| 1.12.3.3.1   | Drug start           | yyyymmddhhss         |     |
+--------------+----------------------+----------------------+-----+
| 1.12.3.3.2   | Drug end             | yyyymmddhhss         |     |
+--------------+----------------------+----------------------+-----+
| 1.12.3.3.3   | Route of             | By inhalation        |     |
|              | administration       |                      |     |
+--------------+----------------------+----------------------+-----+
| 1.12.3.3.4   | Mixture              |                      |     |
+--------------+----------------------+----------------------+-----+
| 1.12.3.3.4.1 | Drug administered    | Isoflurane           |     |
+--------------+----------------------+----------------------+-----+
| 1.12.3.3.4.2 | Medication Type      | General anesthetic   |     |
+--------------+----------------------+----------------------+-----+
| 1.12.3.3.4.3 | Concentration        | 2 %                  |     |
+--------------+----------------------+----------------------+-----+
| 1.12.3.3.5   | Mixture              |                      |     |
+--------------+----------------------+----------------------+-----+
| 1.12.3.3.5.1 | Drug administered    | Oxygen gas           |     |
+--------------+----------------------+----------------------+-----+
| 1.12.3.3.5.2 | Medication Type      | Carrier gas          |     |
+--------------+----------------------+----------------------+-----+
| 1.12.3.3.5.3 | Concentration        | 100 %                |     |
+--------------+----------------------+----------------------+-----+

The content tree structure when induction is by intra-peritoneal
injection might be different in the following way, in that the housing
during the induction phase does not involve a chamber, and the injected
agent is specified, as follows:

+--------------+----------------------+----------------------+-----+
| Node         | Code Meaning of      | Code Meaning or      | TID |
|              | Concept Name         | Example Value        |     |
+==============+======================+======================+=====+
| ...          | ...                  | ...                  | ... |
+--------------+----------------------+----------------------+-----+
| 1.9          | Animal handling      |                      |     |
|              | during specified     |                      |     |
|              | phase                |                      |     |
+--------------+----------------------+----------------------+-----+
| 1.9.1        | Phase of animal      | Anesthesia induction |     |
|              | handling             |                      |     |
+--------------+----------------------+----------------------+-----+
| 1.9.2        | Animal housing       |                      |     |
+--------------+----------------------+----------------------+-----+
| 1.9.2.1      | Comment              | Animal exposed       |     |
|              |                      | whilst inducing      |     |
|              |                      | anesthesia           |     |
+--------------+----------------------+----------------------+-----+
| ...          | ...                  | ...                  | ... |
+--------------+----------------------+----------------------+-----+
| 1.12         | Administration of    |                      |     |
|              | anesthesia           |                      |     |
+--------------+----------------------+----------------------+-----+
| 1.12.1       | Anesthesia Method    |                      |     |
|              | Set                  |                      |     |
+--------------+----------------------+----------------------+-----+
| 1.12.1.1     | Anesthesia Method    |                      |     |
+--------------+----------------------+----------------------+-----+
| 1.12.1.1.1   | Anesthesia Category  | General anesthesia   |     |
+--------------+----------------------+----------------------+-----+
| 1.12.1.1.2   | Anesthesia Start     | yyyymmddhhss         |     |
|              | Time                 |                      |     |
+--------------+----------------------+----------------------+-----+
| 1.12.1.1.3   | Anesthesia Finish    | yyyymmddhhss         |     |
|              | Time                 |                      |     |
+--------------+----------------------+----------------------+-----+
| 1.12.1.1.4   | Anesthesia Induction | Intraperitoneal      |     |
|              |                      | route                |     |
+--------------+----------------------+----------------------+-----+
| 1.12.1.1.5   | Anesthesia           | Inhalation           |     |
|              | Maintenance          | anesthesia, machine  |     |
|              |                      | system, closed, no   |     |
|              |                      | rebreathing of       |     |
|              |                      | primary agent        |     |
+--------------+----------------------+----------------------+-----+
| ...          | ...                  | ...                  | ... |
+--------------+----------------------+----------------------+-----+
| 1.12.3       | Medications Set      |                      |     |
+--------------+----------------------+----------------------+-----+
| 1.12.3.1     | Procedure Phase      | During procedure     |     |
+--------------+----------------------+----------------------+-----+
| 1.12.3.2     | Medication given     |                      |     |
+--------------+----------------------+----------------------+-----+
| 1.12.3.2.1   | Drug start           | yyyymmddhhss         |     |
+--------------+----------------------+----------------------+-----+
| 1.12.3.2.2   | Route of             | Intraperitoneal      |     |
|              | administration       | route                |     |
+--------------+----------------------+----------------------+-----+
| 1.12.3.2.3   | Mixture              |                      |     |
+--------------+----------------------+----------------------+-----+
| 1.12.3.2.3.1 | Drug administered    | Ketamine             |     |
+--------------+----------------------+----------------------+-----+
| 1.12.3.2.3.2 | Medication Type      | General anesthetic   |     |
+--------------+----------------------+----------------------+-----+
| 1.12.3.2.3.2 | Dosage               | nn mg                |     |
+--------------+----------------------+----------------------+-----+
| 1.12.3.2.4   | Mixture              |                      |     |
+--------------+----------------------+----------------------+-----+
| 1.12.3.2.4.1 | Drug administered    | Medetomidine         |     |
+--------------+----------------------+----------------------+-----+
| 1.12.3.2.4.2 | Medication Type      | General anesthetic   |     |
+--------------+----------------------+----------------------+-----+
| 1.12.3.2.4.2 | Dosage               | nn mg                |     |
+--------------+----------------------+----------------------+-----+
| ...          | ...                  | ...                  | ... |
+--------------+----------------------+----------------------+-----+

.. _sect_YYY.1.2:

Example of exogenous substance administration to encode tumor cell line
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

Only the exogenous substance information is included in this example and
content describing animal handling, anesthesia information, etc. is
excluded for clarity. Indeed, given the optionality of the other
content, it would be possible to create an Acquisition Context SR
instance that describes only the exogenous substance information and
nothing else.

The content tree structure would resemble:

+-------------+-----------------------+-----------------------+-----+
| Node        | Code Meaning of       | Code Meaning or       | TID |
|             | Concept Name          | Example Value         |     |
+=============+=======================+=======================+=====+
| 1           | Preclinical Small     |                       |     |
|             | Animal Imaging        |                       |     |
|             | Acquisition Context   |                       |     |
+-------------+-----------------------+-----------------------+-----+
| 1.1         | Language of Content   | English               |     |
|             | Item and Descendants  |                       |     |
+-------------+-----------------------+-----------------------+-----+
| 1.1.2       | Country of Language   | United States         |     |
+-------------+-----------------------+-----------------------+-----+
| 1.2         | Person Observer Name  | Doe^Jane              |     |
+-------------+-----------------------+-----------------------+-----+
| ...         | ...                   | ...                   | ... |
+-------------+-----------------------+-----------------------+-----+
| 1.n         | Exogenous substance   |                       |     |
+-------------+-----------------------+-----------------------+-----+
| 1.n.1       | Tumor Graft           | Adenocarcinoma        |     |
+-------------+-----------------------+-----------------------+-----+
| 1.n.1.1     | Age Started           | 6 week                |     |
+-------------+-----------------------+-----------------------+-----+
| 1.n.1.2     | DateTime Started      | yyyymmddhhss          |     |
+-------------+-----------------------+-----------------------+-----+
| 1.n.1.3     | Brand Name            | MDA-MB-468            |     |
+-------------+-----------------------+-----------------------+-----+
| 1.n.1.4     | Dosage                | 10E6 {cells}          |     |
+-------------+-----------------------+-----------------------+-----+
| 1.n.1.5     | Relative dose         | Single event          |     |
|             | frequency             |                       |     |
+-------------+-----------------------+-----------------------+-----+
| 1.n.1.6     | Route of              | Subcutaneous route    |     |
|             | Administration        |                       |     |
+-------------+-----------------------+-----------------------+-----+
| 1.n.1.6.1   | Site of               | Flank                 |     |
+-------------+-----------------------+-----------------------+-----+
| 1.n.1.6.1.1 | Laterality            | Left                  |     |
+-------------+-----------------------+-----------------------+-----+
| 1.n.1.7     | Tissue of origin      | Breast                |     |
+-------------+-----------------------+-----------------------+-----+
| 1.n.1.8     | Taxonomic rank of     | homo sapiens          |     |
|             | origin                |                       |     |
+-------------+-----------------------+-----------------------+-----+

.. _sect_YYY.1.3:

Informative References
~~~~~~~~~~~~~~~~~~~~~~

.. _biblio_YYY.1.3.1:

Method Descriptions
-------------------

Stout et al 2013 Stout D Berr SS LeBlanc A Kalen JD Osborne D Price J
Schiffer W Kuntner C Wall J 2013 12 7 1-15
http://journals.sagepub.com/doi/pdf/10.2310/7290.2013.00055

David et al 2013a David JM Chatziioannou AF Taschereau R Wang H Stout DB
2013 63 5 386–91 http://www.ncbi.nlm.nih.gov/pmc/articles/PMC3796748/

David et al 2013b David JM Knowles S Lamkin DM Stout DB 2013 52 6 738–44
http://www.ncbi.nlm.nih.gov/pmc/articles/PMC3838608/

Rosenbaum et al 2009 Rosenbaum MD 2009 48 6 763–73
http://www.ncbi.nlm.nih.gov/pmc/articles/PMC2786931/

Fueger et al 2006 Fueger BJ 2006 47 6 999–1006
http://jnm.snmjournals.org/content/47/6/999

Dandekar et al 2007 Dandekar M 2007 48 4 602–7 10.2967/jnumed.106.036608
http://jnm.snmjournals.org/content/48/4/602

Lee et al 2005 Lee KH 2005 46 9 1531–36
http://jnm.snmjournals.org/content/46/9/1531

Balcombe et al 2004 Balcombe JP 2004 43 6 42–51

Van der Meer et al 2004 Van der Meer E 2004 38 4 376–83
http://www.animalexperiments.info/resources/Studies/Animal-impacts/Stress.-Balcombe-et-al-2004./Stress-Balcombe-et-al-2004.pdf

Tabata et al 1998 Tabata H 1998 32 2 143–48 10.1258/002367798780599983
http://lan.sagepub.com/content/32/2/143

