.. _chapter_FF:

CT/MR Cardiovascular Analysis Report Templates (Informative)
============================================================

.. _sect_FF.2:

Template Structure
------------------

.. _sect_FF.3:

Report Example
--------------

The following is a simple, non-comprehensive illustration of a report
for a morphological examination with stenosis findings.

*``Cardiovascular Analysis Report - Vascular MRI``*

-  ``Observer: John Doe``

-  *``Procedure Description``*

   -  ``Abdominal aorta-iliac angiography procedure``

-  *``Vascular Morphological Analysis``*

   *``Anatomic Region = Abdominal Artery, Left``*

   -  **``Left Gastric Artery``**

      -  ``Findings:``

         -  ``Vessel Lumen Diameter: 2 mm``

         -  ``Vessel Lumen Cross Sectional Area: 3.4 mm2``

         -  ``Lesion Finding #1``

            -  ``Best illustration of finding``
               *``<hyperlink to Image with ROI highlighted>``*

            -  ``Associated Morphology: Stenosis``

            -  ``Stenosis type: Vasculitis``

            -  ``Shape: Eccentric``

            -  ``Minimum Vessel Lumen Diameter: 1 mm``

            -  ``Maximum Vessel Lumen Diameter: 1.5 mm``

            -  ``Mean Vessel Lumen Diameter: 1.2 mm``

            -  ``Minimum Vessel Lumen Cross-sectional Area: 1 mm2``

            -  ``Maximum Vessel Lumen Cross-sectional Area: 3 mm2``

            -  ``Stenotic Lesion Length: 5 mm``

            -  ``Minimum Lumen Area Stenosis: 45 %``

            -  ``Maximum Lumen Area Stenosis: 75 %``

            -  ``Mean Lumen Area Stenosis: 60%``

.. table:: Example #1 Report Encoding

   +----------------+------------------+------------------+---------+
   | **Nest**       | **Code Meaning   | **Code Meaning   | **TID** |
   |                | of Concept       | or Example       |         |
   |                | Name**           | Value**          |         |
   +================+==================+==================+=========+
   | 1              | CT/MR            |                  |         |
   |                | Cardiovascular   |                  |         |
   |                | Analysis Report  |                  |         |
   +----------------+------------------+------------------+---------+
   | 1.1            | Procedure        | Vascular MRI     |         |
   |                | Reported         |                  |         |
   +----------------+------------------+------------------+---------+
   | 1.2            | Observer Name    | John Doe         |         |
   +----------------+------------------+------------------+---------+
   | 1.3            | Language of      | English          |         |
   |                | Content Items    |                  |         |
   |                | and Descendents  |                  |         |
   +----------------+------------------+------------------+---------+
   | 1.4            | Procedure        |                  |         |
   |                | Summary          |                  |         |
   +----------------+------------------+------------------+---------+
   | 1.4.1          | Current          | Abdominal        |         |
   |                | Procedure        | aorta-iliac      |         |
   |                | Description      | angiography      |         |
   |                |                  | procedure        |         |
   +----------------+------------------+------------------+---------+
   | 1.5            | Findings         |                  |         |
   +----------------+------------------+------------------+---------+
   | 1.5.1          | Analysis         | Vascular         |         |
   |                | Performed        | Morphological    |         |
   |                |                  | Analysis         |         |
   +----------------+------------------+------------------+---------+
   | 1.5.2          | Artery of        |                  |         |
   |                | Abdomen          |                  |         |
   +----------------+------------------+------------------+---------+
   | 1.5.2.1        | Laterality       | Left             |         |
   +----------------+------------------+------------------+---------+
   | 1.5.2.2        | Findings         |                  |         |
   +----------------+------------------+------------------+---------+
   | 1.5.2.3.1      | Finding Site     | Gastric Artery   |         |
   +----------------+------------------+------------------+---------+
   | 1.5.2.3.2      | Vessel Lumen     | 2 mm             |         |
   |                | Diameter         |                  |         |
   +----------------+------------------+------------------+---------+
   | 1.5.2.3.3      | Vessel Lumen     | 3.4 mm2          |         |
   |                | Cross Sectional  |                  |         |
   |                | Area             |                  |         |
   +----------------+------------------+------------------+---------+
   | 1.5.2.3.4      | Lesion Finding   |                  |         |
   +----------------+------------------+------------------+---------+
   | 1.5.2.3.4.1    | Identifier       | 1                |         |
   +----------------+------------------+------------------+---------+
   | 1.5.2.3.4.2    | Best             | *<ROI            |         |
   |                | Illustration of  | specification>*  |         |
   |                | Findings         |                  |         |
   |                | (SCOORD)         |                  |         |
   +----------------+------------------+------------------+---------+
   | 1.5.2.3.4.2.1  |                  | *<Image          |         |
   |                |                  | reference>*      |         |
   +----------------+------------------+------------------+---------+
   | 1.5.2.3.4.3    | Associated       | Stenosis         |         |
   |                | Morphology       |                  |         |
   +----------------+------------------+------------------+---------+
   | 1.5.2.3.4.4    | Type             | Vasculitis       |         |
   +----------------+------------------+------------------+---------+
   | 1.5.2.3.4.5    | Shape            | Eccentric        |         |
   +----------------+------------------+------------------+---------+
   | 1.5.2.3.4.6    | Vessel Lumen     | 1 mm             |         |
   |                | Diameter         |                  |         |
   +----------------+------------------+------------------+---------+
   | 1.5.2.3.4.6.1  | Qualifier Value  | Minimum          |         |
   +----------------+------------------+------------------+---------+
   | 1.5.2.3.4.7    | Vessel Lumen     | 1.5 mm           |         |
   |                | Diameter         |                  |         |
   +----------------+------------------+------------------+---------+
   | 1.5.2.3.4.7.1  | Qualifier Value  | Maximum          |         |
   +----------------+------------------+------------------+---------+
   | 1.5.2.3.4.8    | Vessel Lumen     | 1.2 mm           |         |
   |                | Diameter         |                  |         |
   +----------------+------------------+------------------+---------+
   | 1.5.2.3.4.8.1  | Qualifier Value  | Mean             |         |
   +----------------+------------------+------------------+---------+
   | 1.5.2.3.4.9    | Vessel Lumen     | 1 mm2            |         |
   |                | Cross-sectional  |                  |         |
   |                | Area             |                  |         |
   +----------------+------------------+------------------+---------+
   | 1.5.2.3.4.9.1  | Qualifier Value  | Minimum          |         |
   +----------------+------------------+------------------+---------+
   | 1.5.2.3.4.10   | Vessel Lumen     | 3 mm2            |         |
   |                | Cross-sectional  |                  |         |
   |                | Area             |                  |         |
   +----------------+------------------+------------------+---------+
   | 1.5.2.3.4.10.1 | Qualifier Value  | Maximum          |         |
   +----------------+------------------+------------------+---------+
   | 1.5.2.3.3.11   | Stenotic Lesion  | 5 mm             |         |
   |                | Length           |                  |         |
   +----------------+------------------+------------------+---------+
   | 1.5.2.3.4.12   | Lumen Area       | 45 %             |         |
   |                | Stenosis         |                  |         |
   +----------------+------------------+------------------+---------+
   | 1.5.2.3.4.12.1 | Qualifier Value  | Minimum          |         |
   +----------------+------------------+------------------+---------+
   | 1.5.2.3.4.13   | Lumen Area       | 75 %             |         |
   |                | Stenosis         |                  |         |
   +----------------+------------------+------------------+---------+
   | 1.5.2.3.4.13.1 | Qualifier Value  | Maximum          |         |
   +----------------+------------------+------------------+---------+
   | 1.5.2.3.4.14   | Lumen Area       | 60 %             |         |
   |                | Stenosis         |                  |         |
   +----------------+------------------+------------------+---------+
   | 1.5.2.3.4.14.1 | Qualifier        | Mean             |         |
   +----------------+------------------+------------------+---------+

