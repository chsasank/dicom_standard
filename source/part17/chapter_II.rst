.. _chapter_II:

Use of Product Characteristics Attributes in Composite SOP Instances (Informative)
==================================================================================

Bar coding or RFID tagging of contrast agents, drugs, and devices can
facilitate the provision of critical information to the imaging
modality, such as the active ingredient, concentration, etc. The Product
Characteristics Query SOP Class allows a modality to submit the product
bar code (or RFID tag) to an SCP to look up the product type, active
substance, size/quantity, or other parameters of the product.

This product information can be included in appropriate Attributes of
the Contrast/Bolus, Device, or Intervention Modules of the Composite SOP
Instances created by the modality. The product information then provides
key acquisition context data necessary for the proper interpretation of
the SOP Instances.

This annex provides informative information about mapping from the
Product Characteristics Module Attributes of the Product Characteristics
Query to the Attributes of Composite IODs included in several Modules.

Within this section, if no Product Characteristics Module source for the
Attribute value is provided, the modality would need to provide local
data entry or user selection from a pick list to fill in appropriate
values. Some values may need to be calculated based on user-performed
dilution of the product at the time of administration.

.. _sect_II.1:

Contrast/bolus Module
---------------------

.. table:: Contrast/Bolus Module Attribute Mapping

   +----------------------+----------------------+----------------------+
   | **Contrast/Bolus     | **Tag**              | **Product            |
   | Module Attribute     |                      | Characteristics      |
   | Name**               |                      | Module Source**      |
   +======================+======================+======================+
   | Contrast/Bolus Agent | (0018,0010)          | Product Name         |
   |                      |                      | (0044,0008)          |
   |                      |                      |                      |
   |                      |                      | .. note::            |
   |                      |                      |                      |
   |                      |                      |    If Product Name   |
   |                      |                      |    is multi-valued,  |
   |                      |                      |    use the first     |
   |                      |                      |    value.            |
   +----------------------+----------------------+----------------------+
   | Contrast/Bolus Agent | (0018,0012)          | --                   |
   | Sequence             |                      |                      |
   +----------------------+----------------------+----------------------+
   | *>Include*           | Product Type Code    |                      |
   |                      | Sequence (0044,0007) |                      |
   |                      | *>'Code Sequence     |                      |
   |                      | Macro'*              |                      |
   +----------------------+----------------------+----------------------+
   | Contrast/Bolus Route | (0018,1040)          |                      |
   +----------------------+----------------------+----------------------+
   | Contrast/Bolus       | (0018,0014)          |                      |
   | Administration Route |                      |                      |
   | Sequence             |                      |                      |
   +----------------------+----------------------+----------------------+
   | *>Include*           |                      |                      |
   +----------------------+----------------------+----------------------+
   | >Additional Drug     | (0018,002A)          |                      |
   | Sequence             |                      |                      |
   +----------------------+----------------------+----------------------+
   | *>Include*           |                      |                      |
   +----------------------+----------------------+----------------------+
   | Contrast/Bolus       | (0018,1041)          | *If contrast is      |
   | Volume               |                      | administered without |
   |                      |                      | dilution, and using  |
   |                      |                      | full contents of     |
   |                      |                      | dispensed product:*  |
   |                      |                      |                      |
   |                      |                      | Product Parameter    |
   |                      |                      | Sequence (0044,0013) |
   |                      |                      | > Numeric Value      |
   |                      |                      | (0040,A30A) where:   |
   |                      |                      |                      |
   |                      |                      | -  Product Parameter |
   |                      |                      |    Sequence >        |
   |                      |                      |    Concept Name Code |
   |                      |                      |    Sequence          |
   |                      |                      |    (0040,A043) value |
   |                      |                      |    is `(118565006,   |
   |                      |                      |    SCT,              |
   |                      |                      |    "Volum            |
   |                      |                      | e") <http://snomed.i |
   |                      |                      | nfo/id/118565006>`__ |
   |                      |                      |                      |
   |                      |                      | -  Product Parameter |
   |                      |                      |    Sequence >        |
   |                      |                      |    Measurement Units |
   |                      |                      |    Code Sequence     |
   |                      |                      |    (0040,08EA) is    |
   |                      |                      |    (ml, UCUM, "ml")  |
   +----------------------+----------------------+----------------------+
   | Contrast/Bolus Start | (0018,1042)          |                      |
   | Time                 |                      |                      |
   +----------------------+----------------------+----------------------+
   | Contrast/Bolus Stop  | (0018,1043)          |                      |
   | Time                 |                      |                      |
   +----------------------+----------------------+----------------------+
   | Contrast/Bolus Total | (0018,1044)          | *If contrast is      |
   | Dose                 |                      | administered using   |
   |                      |                      | full contents of     |
   |                      |                      | dispensed product:*  |
   |                      |                      |                      |
   |                      |                      | Product Parameter    |
   |                      |                      | Sequence (0044,0013) |
   |                      |                      | > Numeric Value      |
   |                      |                      | (0040,A30A), where:  |
   |                      |                      |                      |
   |                      |                      | -  Product Parameter |
   |                      |                      |    Sequence >        |
   |                      |                      |    Concept Name Code |
   |                      |                      |    Sequence          |
   |                      |                      |    (0040,A043) value |
   |                      |                      |    is `(118565006,   |
   |                      |                      |    SCT,              |
   |                      |                      |    "Volum            |
   |                      |                      | e") <http://snomed.i |
   |                      |                      | nfo/id/118565006>`__ |
   |                      |                      |                      |
   |                      |                      | -  Product Parameter |
   |                      |                      |    Sequence >        |
   |                      |                      |    Measurement Units |
   |                      |                      |    Code Sequence     |
   |                      |                      |    (0040,08EA) is    |
   |                      |                      |    (ml, UCUM, "ml")  |
   +----------------------+----------------------+----------------------+
   | Contrast Flow Rate   | (0018,1046)          |                      |
   +----------------------+----------------------+----------------------+
   | Contrast Flow        | (0018,1047)          |                      |
   | Duration             |                      |                      |
   +----------------------+----------------------+----------------------+
   | Contrast/Bolus       | (0018,1048)          | Product Parameter    |
   | Ingredient           |                      | Sequence (0044,0013) |
   |                      |                      | > Concept Code       |
   |                      |                      | Sequence (0040,A168) |
   |                      |                      | > Code Meaning       |
   |                      |                      | (0008,0104), where:  |
   |                      |                      |                      |
   |                      |                      | -  Product Parameter |
   |                      |                      |    Sequence >        |
   |                      |                      |    Concept Name Code |
   |                      |                      |    Sequence          |
   |                      |                      |    (0040,A043) value |
   |                      |                      |    is `(127489000,   |
   |                      |                      |    SCT, "Active      |
   |                      |                      |    Ingredien         |
   |                      |                      | t") <http://snomed.i |
   |                      |                      | nfo/id/127489000>`__ |
   |                      |                      |                      |
   |                      |                      | .. note::            |
   |                      |                      |                      |
   |                      |                      |    Contrast/Bolus    |
   |                      |                      |    Ingredient is a   |
   |                      |                      |    CS VR (16         |
   |                      |                      |    characters max,   |
   |                      |                      |    upper case), so a |
   |                      |                      |    conversion from   |
   |                      |                      |    the LO VR is      |
   |                      |                      |    required.         |
   +----------------------+----------------------+----------------------+
   | Contrast/Bolus       | (0018,1049)          | *If contrast is      |
   | Ingredient           |                      | administered without |
   | Concentration        |                      | dilution:*           |
   |                      |                      |                      |
   |                      |                      | Product Parameter    |
   |                      |                      | Sequence (0044,0013) |
   |                      |                      | > Numeric Value      |
   |                      |                      | (0040,A30A), where:  |
   |                      |                      |                      |
   |                      |                      | -  Product Parameter |
   |                      |                      |    Sequence >        |
   |                      |                      |    Concept Name Code |
   |                      |                      |    Sequence          |
   |                      |                      |    (0040,A043) value |
   |                      |                      |    is (121380, DCM,  |
   |                      |                      |    "Active           |
   |                      |                      |    Ingredient        |
   |                      |                      |    Undiluted         |
   |                      |                      |    Concentration")   |
   |                      |                      |                      |
   |                      |                      | -  Product Parameter |
   |                      |                      |    Sequence >        |
   |                      |                      |    Measurement Units |
   |                      |                      |    Code Sequence     |
   |                      |                      |    (0040,08EA) is    |
   |                      |                      |    (mg/ml, UCUM,     |
   |                      |                      |    "mg/ml")          |
   +----------------------+----------------------+----------------------+

.. _sect_II.2:

Enhanced Contrast/bolus Module
------------------------------

.. table:: Enhanced Contrast/Bolus Module Attribute Mapping

   +----------------------+----------------------+----------------------+
   | **Enhanced           | **Tag**              | **Product            |
   | Contrast/Bolus       |                      | Characteristics      |
   | Module Attribute     |                      | Module Source**      |
   | Name**               |                      |                      |
   +======================+======================+======================+
   | Contrast/Bolus Agent | (0018,0012)          | --                   |
   | Sequence             |                      |                      |
   +----------------------+----------------------+----------------------+
   | *>Include*           | Product Type Code    |                      |
   |                      | Sequence (0044,0007) |                      |
   |                      | > *'Code Sequence    |                      |
   |                      | Macro'*              |                      |
   +----------------------+----------------------+----------------------+
   | >Contrast/Bolus      | (0018,9337)          |                      |
   | Agent Number         |                      |                      |
   +----------------------+----------------------+----------------------+
   | >Contrast/Bolus      | (0018,0014)          |                      |
   | Administration Route |                      |                      |
   | Sequence             |                      |                      |
   +----------------------+----------------------+----------------------+
   | *>>Include*          |                      |                      |
   +----------------------+----------------------+----------------------+
   | >Contrast/Bolus      | (0018,9338)          | --                   |
   | Ingredient Code      |                      |                      |
   | Sequence             |                      |                      |
   +----------------------+----------------------+----------------------+
   | *>>Include*          | Product Parameter    |                      |
   |                      | Sequence (0044,0013) |                      |
   |                      | > Concept Code       |                      |
   |                      | Sequence             |                      |
   |                      | (0040,A168), where:  |                      |
   |                      |                      |                      |
   |                      | -  Product Parameter |                      |
   |                      |    Sequence >        |                      |
   |                      |    Concept Name Code |                      |
   |                      |    Sequence          |                      |
   |                      |    (0040,A043) value |                      |
   |                      |    is `(127489000,   |                      |
   |                      |    SCT, "Active      |                      |
   |                      |    Ingredien         |                      |
   |                      | t") <http://snomed.i |                      |
   |                      | nfo/id/127489000>`__ |                      |
   +----------------------+----------------------+----------------------+
   | >Contrast/Bolus      | (0018,1041)          | *If contrast is      |
   | Volume               |                      | administered without |
   |                      |                      | dilution, and using  |
   |                      |                      | full contents of     |
   |                      |                      | dispensed product:*  |
   |                      |                      |                      |
   |                      |                      | Product Parameter    |
   |                      |                      | Sequence (0044,0013) |
   |                      |                      | > Numeric Value      |
   |                      |                      | (0040,A30A), where:  |
   |                      |                      |                      |
   |                      |                      | -  Product Parameter |
   |                      |                      |    Sequence >        |
   |                      |                      |    Concept Name Code |
   |                      |                      |    Sequence          |
   |                      |                      |    (0040,A043) value |
   |                      |                      |    is `(118565006,   |
   |                      |                      |    SCT,              |
   |                      |                      |    "Volum            |
   |                      |                      | e") <http://snomed.i |
   |                      |                      | nfo/id/118565006>`__ |
   |                      |                      |                      |
   |                      |                      | -  Product Parameter |
   |                      |                      |    Sequence >        |
   |                      |                      |    Measurement Units |
   |                      |                      |    Code Sequence     |
   |                      |                      |    (0040,08EA) is    |
   |                      |                      |    (ml, UCUM, "ml")  |
   +----------------------+----------------------+----------------------+
   | >Contrast/Bolus      | (0018,1049)          | *If contrast is      |
   | Ingredient           |                      | administered without |
   | Concentration        |                      | dilution:*           |
   |                      |                      |                      |
   |                      |                      | Product Parameter    |
   |                      |                      | Sequence (0044,0013) |
   |                      |                      | > Numeric Value      |
   |                      |                      | (0040,A30A), where:  |
   |                      |                      |                      |
   |                      |                      | -  Product Parameter |
   |                      |                      |    Sequence >        |
   |                      |                      |    Concept Name Code |
   |                      |                      |    Sequence          |
   |                      |                      |    (0040,A043) value |
   |                      |                      |    is (121380, DCM,  |
   |                      |                      |    "Active           |
   |                      |                      |    Ingredient        |
   |                      |                      |    Undiluted         |
   |                      |                      |    Concentration")   |
   |                      |                      |                      |
   |                      |                      | -  Product Parameter |
   |                      |                      |    Sequence >        |
   |                      |                      |    Measurement Units |
   |                      |                      |    Code Sequence     |
   |                      |                      |    (0040,08EA) is    |
   |                      |                      |    (mg/ml, UCUM,     |
   |                      |                      |    "mg/ml")          |
   +----------------------+----------------------+----------------------+
   | >Contrast/Bolus      | (0018,9425)          | Product Parameter    |
   | Ingredient Opaque    |                      | Sequence (0044,0013) |
   |                      |                      | > Concept Code       |
   |                      |                      | Sequence (0040,A168) |
   |                      |                      | > Code Meaning       |
   |                      |                      | (0008,0104), where:  |
   |                      |                      |                      |
   |                      |                      | -  Product Parameter |
   |                      |                      |    Sequence >        |
   |                      |                      |    Concept Name Code |
   |                      |                      |    Sequence          |
   |                      |                      |    (0040,A043) value |
   |                      |                      |    is (121381, DCM,  |
   |                      |                      |    "Contrast/Bolus   |
   |                      |                      |    Ingredient        |
   |                      |                      |    Opaque") and      |
   |                      |                      |    mapped Code       |
   |                      |                      |    Meaning is "YES"  |
   |                      |                      |    or "NO".          |
   +----------------------+----------------------+----------------------+
   | >Contrast            | (0018,9340)          |                      |
   | Administration       |                      |                      |
   | Profile Sequence     |                      |                      |
   +----------------------+----------------------+----------------------+
   | >>Contrast/Bolus     | (0018,1041)          | *If contrast is      |
   | Volume               |                      | administered without |
   |                      |                      | dilution, and using  |
   |                      |                      | full contents of     |
   |                      |                      | dispensed product:*  |
   |                      |                      |                      |
   |                      |                      | Product Parameter    |
   |                      |                      | Sequence (0044,0013) |
   |                      |                      | > Numeric Value      |
   |                      |                      | (0040,A30A), where:  |
   |                      |                      |                      |
   |                      |                      | -  Product Parameter |
   |                      |                      |    Sequence >        |
   |                      |                      |    Concept Name Code |
   |                      |                      |    Sequence          |
   |                      |                      |    (0040,A043) value |
   |                      |                      |    is `(118565006,   |
   |                      |                      |    SCT,              |
   |                      |                      |    "Volum            |
   |                      |                      | e") <http://snomed.i |
   |                      |                      | nfo/id/118565006>`__ |
   |                      |                      |                      |
   |                      |                      | -  Product Parameter |
   |                      |                      |    Sequence >        |
   |                      |                      |    Measurement Units |
   |                      |                      |    Code Sequence     |
   |                      |                      |    (0040,08EA) is    |
   |                      |                      |    (ml, UCUM, "ml")  |
   +----------------------+----------------------+----------------------+
   | >>Contrast/Bolus     | (0018,1042)          |                      |
   | Start Time           |                      |                      |
   +----------------------+----------------------+----------------------+
   | >>Contrast/Bolus     | (0018,1043)          |                      |
   | Stop Time            |                      |                      |
   +----------------------+----------------------+----------------------+
   | >>Contrast Flow Rate | (0018,1046)          |                      |
   +----------------------+----------------------+----------------------+
   | >>Contrast Flow      | (0018,1047)          |                      |
   | Duration             |                      |                      |
   +----------------------+----------------------+----------------------+

.. _sect_II.3:

Device Module
-------------

.. table:: Device Module Attribute Mapping

   +----------------------+----------------------+----------------------+
   | **Device Module      | **Tag**              | **Product            |
   | Attribute Name**     |                      | Characteristics      |
   |                      |                      | Module Source**      |
   +======================+======================+======================+
   | Device Sequence      | (0050,0010)          | --                   |
   +----------------------+----------------------+----------------------+
   | *>Include*           | Product Type Code    |                      |
   |                      | Sequence (0044,0007) |                      |
   |                      | > *'Code Sequence    |                      |
   |                      | Macro'*              |                      |
   +----------------------+----------------------+----------------------+
   | >Device Length       | (0050,0014)          | Product Parameter    |
   |                      |                      | Sequence (0044,0013) |
   |                      |                      | > Numeric Value      |
   |                      |                      | (0040,A30A), where:  |
   |                      |                      |                      |
   |                      |                      | -  Product Parameter |
   |                      |                      |    Sequence >        |
   |                      |                      |    Concept Name Code |
   |                      |                      |    Sequence          |
   |                      |                      |    (0040,A043) value |
   |                      |                      |    is `(410668003,   |
   |                      |                      |    SCT,              |
   |                      |                      |    "Lengt            |
   |                      |                      | h") <http://snomed.i |
   |                      |                      | nfo/id/410668003>`__ |
   |                      |                      |                      |
   |                      |                      | -  Product Parameter |
   |                      |                      |    Sequence >        |
   |                      |                      |    Measurement Units |
   |                      |                      |    Code Sequence     |
   |                      |                      |    (0040,08EA) is    |
   |                      |                      |    (mm, UCUM, "mm")  |
   +----------------------+----------------------+----------------------+
   | >Device Diameter     | (0050,0016)          | Product Parameter    |
   |                      |                      | Sequence (0044,0013) |
   |                      |                      | > Numeric Value      |
   |                      |                      | (0040,A30A), where:  |
   |                      |                      |                      |
   |                      |                      | -  Product Parameter |
   |                      |                      |    Sequence >        |
   |                      |                      |    Concept Name Code |
   |                      |                      |    Sequence          |
   |                      |                      |    (0040,A043) value |
   |                      |                      |    is `(81827009,    |
   |                      |                      |    SCT,              |
   |                      |                      |    "Diamet           |
   |                      |                      | er") <http://snomed. |
   |                      |                      | info/id/81827009>`__ |
   +----------------------+----------------------+----------------------+
   | >Device Diameter     | (0050,0017)          | Product Parameter    |
   | Units                |                      | Sequence (0044,0013) |
   |                      |                      | > Measurement Units  |
   |                      |                      | Code Sequence        |
   |                      |                      | (0040,08EA) > Code   |
   |                      |                      | Meaning (0008,0104), |
   |                      |                      | where:               |
   |                      |                      |                      |
   |                      |                      | -  Product Parameter |
   |                      |                      |    Sequence >        |
   |                      |                      |    Concept Name Code |
   |                      |                      |    Sequence          |
   |                      |                      |    (0040,A043) value |
   |                      |                      |    is `(81827009,    |
   |                      |                      |    SCT,              |
   |                      |                      |    "Diamet           |
   |                      |                      | er") <http://snomed. |
   |                      |                      | info/id/81827009>`__ |
   |                      |                      |                      |
   |                      |                      | .. note::            |
   |                      |                      |                      |
   |                      |                      |    Device Diameter   |
   |                      |                      |    Units is a CS VR  |
   |                      |                      |    (16 characters    |
   |                      |                      |    max, upper case), |
   |                      |                      |    so a conversion   |
   |                      |                      |    from the LO VR is |
   |                      |                      |    required.         |
   +----------------------+----------------------+----------------------+
   | >Device Volume       | (0050,0018)          | Product Parameter    |
   |                      |                      | Sequence (0044,0013) |
   |                      |                      | > Numeric Value      |
   |                      |                      | (0040,A30A), where:  |
   |                      |                      |                      |
   |                      |                      | -  Product Parameter |
   |                      |                      |    Sequence >        |
   |                      |                      |    Concept Name Code |
   |                      |                      |    Sequence          |
   |                      |                      |    (0040,A043) value |
   |                      |                      |    is `(118565006,   |
   |                      |                      |    SCT,              |
   |                      |                      |    "Volum            |
   |                      |                      | e") <http://snomed.i |
   |                      |                      | nfo/id/118565006>`__ |
   |                      |                      |                      |
   |                      |                      | -  Product Parameter |
   |                      |                      |    Sequence >        |
   |                      |                      |    Measurement Units |
   |                      |                      |    Code Sequence     |
   |                      |                      |    (0040,08EA) is    |
   |                      |                      |    (ml, UCUM, "ml")  |
   +----------------------+----------------------+----------------------+
   | >Inter-Marker        | (0050,0019)          | Product Parameter    |
   | Distance             |                      | Sequence (0044,0013) |
   |                      |                      | > Numeric Value      |
   |                      |                      | (0040,A30A), where:  |
   |                      |                      |                      |
   |                      |                      | -  Product Parameter |
   |                      |                      |    Sequence >        |
   |                      |                      |    Concept Name Code |
   |                      |                      |    Sequence          |
   |                      |                      |    (0040,A043) value |
   |                      |                      |    is (121208, DCM,  |
   |                      |                      |    "Inter-Marker     |
   |                      |                      |    Distance")        |
   |                      |                      |                      |
   |                      |                      | -  Product Parameter |
   |                      |                      |    Sequence >        |
   |                      |                      |    Measurement Units |
   |                      |                      |    Code Sequence     |
   |                      |                      |    (0040,08EA) is    |
   |                      |                      |    (mm, UCUM, "mm")  |
   +----------------------+----------------------+----------------------+
   | >Device Description  | (0050,0020)          | Product Name         |
   |                      |                      | (0044,0008) and/or   |
   |                      |                      | Product Description  |
   |                      |                      | (0044,0009)          |
   +----------------------+----------------------+----------------------+

.. _sect_II.4:

Intervention Module
-------------------

.. table:: Intervention Module Attribute Mapping

   +----------------------+----------------------+----------------------+
   | **Intervention       | **Tag**              | **Product            |
   | Module Attribute     |                      | Characteristics      |
   | Name**               |                      | Module Source**      |
   +======================+======================+======================+
   | Intervention         | (0018,0036)          |                      |
   | Sequence             |                      |                      |
   +----------------------+----------------------+----------------------+
   | *>Include*           |                      |                      |
   +----------------------+----------------------+----------------------+
   | >Intervention Status | (0018,0038)          |                      |
   +----------------------+----------------------+----------------------+
   | >Intervention Drug   | (0018,0029)          | --                   |
   | Code Sequence        |                      |                      |
   +----------------------+----------------------+----------------------+
   | *>>Include*          | Product Type Code    |                      |
   |                      | Sequence (0044,0007) |                      |
   |                      | > *'Code Sequence    |                      |
   |                      | Macro'*              |                      |
   +----------------------+----------------------+----------------------+
   | >Intervention Drug   | (0018,0035)          |                      |
   | Start Time           |                      |                      |
   +----------------------+----------------------+----------------------+
   | >Intervention Drug   | (0018,0027)          |                      |
   | Stop Time            |                      |                      |
   +----------------------+----------------------+----------------------+
   | > Administration     | (0054,0302)          |                      |
   | Route Code Sequence  |                      |                      |
   +----------------------+----------------------+----------------------+
   | *>>Include*          |                      |                      |
   +----------------------+----------------------+----------------------+
   | >Intervention        | (0018,003A)          |                      |
   | Description          |                      |                      |
   +----------------------+----------------------+----------------------+

