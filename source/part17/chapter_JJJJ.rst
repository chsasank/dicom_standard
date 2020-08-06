.. _chapter_JJJJ:

Multi-energy CT Imaging (Informative)
=====================================

.. _sect_JJJJ.1:

Domain of Application
---------------------

Multi-energy CT acquires pixel information which correlates to different
X-Ray spectra to enable differentiation, quantification and
classification of different types of tissues.

To detect the different X-Ray spectra, Multi-energy (ME) CT imaging uses
combinations of different Source(s) and Detector(s) technologies such as
current switching X-Ray tubes, spectral detectors, multi-layer
detectors, multi-source and detector pairs.

.. _sect_JJJJ.2:

Use Cases
---------

Multi-energy CT data can be reconstructed and processed in different
ways to serve a variety of purposes.

-  Differentiate materials that look similar on conventional CT images,
   e.g., to differentiate Iodine and Calcium in vascular structures or
   to differentiate vascular structures from adjacent bone.

-  Quantify base materials to accurately define tissues and organs. The
   intent is to quantify materials, and to extract regions and organs
   based on their composition.

-  Generate virtual non-contrast images from a contrast-enhanced image
   rather than having to scan the patient twice.

-  Reduce beam hardening artifacts.

-  Enhance the effect of contrast such as highlighting Iodine and soft
   tissue.

.. _sect_JJJJ.3:

Classification of Multi-energy Images
-------------------------------------

The following Multi-energy image types and families are addressed in
this supplement:

Standard CT Image (CT Image IOD, Enhanced CT Image IOD)
   Images created using ME techniques, for example, in case of the
   creation of conventional appearing CT images out of two energy
   spectra or images created with only one of the multiple energies
   acquired. No new image type definitions are needed but new optional
   Attributes are needed.

Objective Image Family
   Virtual Monoenergetic Image
      Each real-world value mapped pixel represents CT Hounsfield units
      and is analogous to a CT image created by a monoenergetic (of a
      specific keV value) X-Ray beam. In certain cases, the image
      impression (quality) will allow a better iodine representation and
      better metal artifact reduction. Monoenergetic images are
      sometimes colloquially referred to as monochromatic images.

   Effective Atomic Number Image
      Each real-world value mapped pixel represents Effective Atomic
      Number (aka. "Effective Z") of that pixel.

   Electron Density Image
      Each real-world value mapped pixel represents a number of
      electrons per unit volume (N) in units of 10\ :sup:`23`/ml or a
      relative electron density to water (N/N\ :sub:`Water`). Electron
      density is used commonly in radiotherapy.

Material Quantification Image Family
   These image types characterize the elemental composition of materials
   in the image. They provide material quantification using a physical
   scale. Pixel values can be in HU or in equivalent material
   concentration (e.g., mg/ml). The following image types belong to this
   family:

   Material-Specific Image
      Each real-world value mapped pixel value represents a property of
      a material such as attenuation, concentration or density.

   Material-Removed Image
      An image where the attenuation contribution of one or more
      materials has been removed. Each real-world value mapped pixel may
      be adjusted to represent the attenuation as if the pixel was
      filled with the remaining materials. For pixels that did not
      contain any of the removed material(s), the pixel values are
      unchanged. For example, in virtual-unenhanced (VUE) or
      virtual-non-contrast (VNC) image the attenuation contribution of
      the contrast material is removed from each pixel.

   Fractional Map Image
      Each real-world value mapped pixel represents the fraction of a
      specific material present in the pixel. Since Fractional Map
      Images are generated as a set, the sum of the real-world values
      for all the Fractional Map Images is 1 for each pixel.

   Value-Based Map Image
      Each real-world value mapped pixel represents a certain value for
      a specified material (the exact interpretation of the value range
      has to be defined by the user).

Material Visualization Image Family
   These image types allow visualizing material content, usually with
   colors (color maps, color overlays, blending, etc.).

   Material-Modified Image
      CT Image where pixel values have been modified to highlight a
      certain target material (either by partially suppressing the
      background or by enhancing the target material), or to partially
      suppress the target material. The image units are still HU, so
      they may be presented similarly to conventional CT Images. The
      values of some pixels in the Material-Modified Image are
      intentionally distorted for better visualization of certain
      materials (i.e. making tendon more visible). Thus, the image may
      not be used for quantification, unlike a Material-Removed Image,
      which can.

   Color Image
      Implementations of Material Visualization Images use existing
      DICOM objects (Blending Presentation State, Secondary Capture
      Image (used as fallback)).

.. _sect_JJJJ.4:

Presentation of Multi-energy Images by Legacy Display Systems
-------------------------------------------------------------

A legacy, naïve display system can receive a multi-energy (ME) image and
may not recognize it as ME image, but rather display the image as a
conventional CT image. This may potentially cause clinical
misinterpretation, for instance, in the following scenarios:

1. For virtual mono-energetic images (VMI, images similar to those
   obtained with mono-energetic x-ray beam, in keV), attenuation highly
   depends on the beam energy (keV), so CT pixel values in VMI images
   can be very different from those in conventional CT images. Without
   proper labeling of such images, including the specific keV value
   used, the reviewer can come to wrong conclusions.

2. HU-based Multi-energy images where CT pixel values have been modified
   for specific materials (suppressed, highlighted, etc.) look similar
   to conventional CT images. Without proper labeling of such images,
   including the identification of the affected materials and the way of
   modification, the reviewer can come to wrong conclusions.

3. In certain types of Multi-energy images (effective atomic number,
   electron density, material-specific image containing material
   concentration), CT pixel values do not represent HU values. Common
   ROI tools used on such an image will measure and display an average
   value. Since non-HU values are quite unusual in CT IOD images, there
   is a significant risk that a common naïve display will either omit
   the units of measurements (leaving user to assume the material or
   units), or (which is even worse) will display "HU" units instead.

4. In case of Virtual Non-Contrast images, the pixel values are modified
   (contrast is removed and pixel values may have been corrected for
   displacement of one material by another material). Since pixels are
   modified, there is a risk that the modification is incomplete or the
   replacement is not adequate.

.. _sect_JJJJ.5.:

Examples of Implementation
--------------------------

These are examples how the Attributes can be set for each image family
(`Classification of Multi-energy Images <#sect_JJJJ.3>`__).

The structure and content of a Multi-energy CT instance also depends on
the architecture of the acquisition device, e.g. multiple sources and
multiple detectors vs. switching source and single detector, etc. A
variety of architectures will be shown in the following examples, but an
example will not be shown for every architecture.

.. _sect_JJJJ.5.1:

Examples For Objective Image Family
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

.. _sect_JJJJ.5.1.1:

Example Multiple Physical Sources and Multiple Physical Detectors
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

This example shows an Effective Atomic Number image acquired on an
acquisition device with multiple physical sources and multiple physical
detectors.

.. table:: CT Image Module Attributes

   +--------------------------+-------------+--------------------------+
   | **Attribute Name**       | **Tag**     | **Values**               |
   +==========================+=============+==========================+
   | Image Type               | (0008,0008) | ORIGINAL\\               |
   |                          |             |                          |
   |                          |             | PRIMARY\\                |
   |                          |             |                          |
   |                          |             | AXIAL\\                  |
   |                          |             |                          |
   |                          |             | EFF_ATOMIC_NUM           |
   +--------------------------+-------------+--------------------------+
   | Multi-energy CT          | (0018,9361) | YES                      |
   | Acquisition              |             |                          |
   +--------------------------+-------------+--------------------------+
   | …                        |             |                          |
   +--------------------------+-------------+--------------------------+
   | Rescale Intercept        | (0028,1052) | -102.4                   |
   +--------------------------+-------------+--------------------------+
   | Rescale Slope            | (0028,1053) | 0.1                      |
   +--------------------------+-------------+--------------------------+
   | Rescale Type             | (0028,1054) | Z_EFF                    |
   +--------------------------+-------------+--------------------------+
   | …                        |             |                          |
   +--------------------------+-------------+--------------------------+
   | KVP                      | (0018,0060) | {null value because it   |
   |                          |             | is described below}      |
   +--------------------------+-------------+--------------------------+
   | …                        |             |                          |
   +--------------------------+-------------+--------------------------+
   | Distance Source to       | (0018,1110) | 1000                     |
   | Detector                 |             |                          |
   +--------------------------+-------------+--------------------------+
   | Distance Source to       | (0018,1111) | 500                      |
   | Patient                  |             |                          |
   +--------------------------+-------------+--------------------------+
   | Exposure Time            | (0018,1150) | 1000                     |
   +--------------------------+-------------+--------------------------+
   | Single Collimation Width | (0018,9306) | 0.6                      |
   +--------------------------+-------------+--------------------------+
   | Total Collimation Width  | (0018,9307) | 38,4                     |
   +--------------------------+-------------+--------------------------+
   | …                        |             |                          |
   +--------------------------+-------------+--------------------------+
   | *Include*                |             |                          |
   +--------------------------+-------------+--------------------------+

.. table:: Multi-energy CT Image Attributes

   +--------------------------+-------------+-------------------------+
   | **Attribute Name**       | **Tag**     | **Values**              |
   +==========================+=============+=========================+
   | Multi-energy CT          | (0018,9362) |                         |
   | Acquisition Sequence     |             |                         |
   +--------------------------+-------------+-------------------------+
   | >Multi-energy            | (0018,937B) | Dual Source Dual Energy |
   | Acquisition Description  |             |                         |
   +--------------------------+-------------+-------------------------+
   | *                        |             |                         |
   | >Include*\ `table_title  |             |                         |
   | <#table_JJJJ.5.1.1-3>`__ |             |                         |
   +--------------------------+-------------+-------------------------+
   | *                        |             |                         |
   | >Include*\ `table_title  |             |                         |
   | <#table_JJJJ.5.1.1-4>`__ |             |                         |
   +--------------------------+-------------+-------------------------+
   | *                        |             |                         |
   | >Include*\ `table_title  |             |                         |
   | <#table_JJJJ.5.1.1-5>`__ |             |                         |
   +--------------------------+-------------+-------------------------+
   | *                        |             |                         |
   | >Include*\ `table_title  |             |                         |
   | <#table_JJJJ.5.1.1-6>`__ |             |                         |
   +--------------------------+-------------+-------------------------+
   | *                        |             |                         |
   | >Include*\ `table_title  |             |                         |
   | <#table_JJJJ.5.1.1-7>`__ |             |                         |
   +--------------------------+-------------+-------------------------+
   | *                        |             |                         |
   | >Include*\ `table_title  |             |                         |
   | <#table_JJJJ.5.1.1-8>`__ |             |                         |
   +--------------------------+-------------+-------------------------+
   | *                        |             |                         |
   | >Include*\ `table_title  |             |                         |
   | <#table_JJJJ.5.1.1-9>`__ |             |                         |
   +--------------------------+-------------+-------------------------+
   | Multi-energy CT          | (0018,9363) |                         |
   | Processing Sequence      |             |                         |
   +--------------------------+-------------+-------------------------+
   | *>                       |             |                         |
   | Include*\ `table_title < |             |                         |
   | #table_JJJJ.5.1.1-10>`__ |             |                         |
   +--------------------------+-------------+-------------------------+

.. table:: Multi-energy CT X-Ray Source Macro Attributes

   ===================================== =========== ===================
   **Attribute Name**                    **Tag**     **Values**
   ===================================== =========== ===================
   Multi-energy CT X-Ray Source Sequence (0018,9365) 
   ITEM 1                                            
   >X-Ray Source Index                   (0018,9366) 1
   >X-Ray Source ID                      (0018,9367) Tube A
   >Multi-energy Source Technique        (0018,9368) CONSTANT_SOURCE
   >Source Start DateTime                (0018,9369) 2018.05.01 13:22:03
   >Source End DateTime                  (0018,936A) 2018.05.01 13:22:20
   >Generator Power                      (0018,1170) 100
   ITEM 2                                            
   >X-Ray Source Index                   (0018,9366) 2
   >X-Ray Source ID                      (0018,9367) Tube B
   >Multi-energy Source Technique        (0018,9368) CONSTANT_SOURCE
   >Source Start DateTime                (0018,9369) 2018.05.01 13:22:03
   >Source End DateTime                  (0018,936A) 2018.05.01 13:22:20
   >Generator Power                      (0018,1170) 100
   ===================================== =========== ===================

.. table:: Multi-energy CT X-Ray Detector Macro Attributes

   ======================================= =========== ===========
   **Attribute Name**                      **Tag**     **Values**
   ======================================= =========== ===========
   Multi-energy CT X-Ray Detector Sequence (0018,936F) 
   ITEM 1                                              
   >X-Ray Detector Index                   (0018,9370) 1
   >X-Ray Detector ID                      (0018,9371) Detector A
   >Multi-energy Detector Type             (0018,9372) INTEGRATING
   >X-Ray Detector Label                   (0018,9373) High-Energy
   >Nominal Max Energy                     (0018,9374) 150
   >Nominal Min Energy                     (0018,9375) 35
   >Effective Bin Energy                   (0018,936E) 90
   ITEM 2                                              
   >X-Ray Detector Index                   (0018,9370) 2
   >X-Ray Detector ID                      (0018,9371) Detector B
   >Multi-energy Detector Type             (0018,9372) INTEGRATING
   >X-Ray Detector Label                   (0018,9373) Low-Energy
   >Nominal Max Energy                     (0018,9374) 100
   >Nominal Min Energy                     (0018,9375) 35
   >Effective Bin Energy                   (0018,936E) 60
   ======================================= =========== ===========

.. table:: Multi-energy CT Path Macro Attributes

   ============================= =========== ==========
   **Attribute Name**            **Tag**     **Values**
   ============================= =========== ==========
   Multi-energy CT Path Sequence (0018,9379) 
   ITEM 1                                    
   >Multi-energy CT Path Index   (0018,937A) 1
   >X-Ray Source Index           (0018,9366) 1
   >X-Ray Detector Index         (0018,9370) 1
   ITEM 2                                    
   >Multi-energy CT Path Index   (0018,937A) 2
   >X-Ray Source Index           (0018,9366) 2
   >X-Ray Detector Index         (0018,9370) 2
   ============================= =========== ==========

.. table:: CT Exposure Macro Attributes

   ============================== =========== ==========
   **Attribute Name**             **Tag**     **Values**
   ============================== =========== ==========
   CT Exposure Sequence           (0018,9321) 
   ITEM 1                                     
   >Referenced X-Ray Source Index (0018,9377) 1
   >Exposure Time in ms           (0018,9328) 1000
   >X-Ray Tube Current in mA      (0018,9330) 500
   >Exposure in mAs               (0018,9332) 500
   >Exposure Modulation Type      (0018,9323) CD4D
   >CTDIvol                       (0018,9345) 5
   ITEM 2                                     
   >Referenced X-Ray Source Index (0018,9377) 2
   >Exposure Time in ms           (0018,9328) 1000
   >X-Ray Tube Current in mA      (0018,9330) 250
   >Exposure in mAs               (0018,9332) 250
   >Exposure Modulation Type      (0018,9323) CD4D
   >CTDIvol                       (0018,9345) 5
   ============================== =========== ==========

.. table:: CT X-Ray Details Sequence Macro Attributes

   ========================= =========== ===========
   **Attribute Name**        **Tag**     **Values**
   ========================= =========== ===========
   CT X-Ray Details Sequence (0018,9325) 
   ITEM 1                                
   >Referenced Path Index    (0018,9378) 1
   >KVP                      (0018,0060) 150
   >Focal Spot(s)            (0018,1190) 1.2
   >Filter Type              (0018,1160) WEDGE2
   >Filter Material          (0018,7050) MIXED
   ITEM 2                                
   >Referenced Path Index    (0018,9378) 2
   >KVP                      (0018,0060) 100
   >Focal Spot(s)            (0018,1190) 1.2
   >Filter Type              (0018,1160) WEDGE2+FLAT
   >Filter Material          (0018,7050) TIN
   ========================= =========== ===========

.. table:: CT Acquisition Details Macro Attributes

   =============================== =========== ==========
   **Attribute Name**              **Tag**     **Values**
   =============================== =========== ==========
   CT Acquisition Details Sequence (0018,9304) 
   ITEM 1                                      
   >Referenced Path Index          (0018,9378) 1
   >Rotation Direction             (0018,1140) CW
   >Revolution Time                (0018,9305) 0.5
   >Single Collimation Width       (0018,9306) 0.6
   >Total Collimation Width        (0018,9307) 38.4
   >Table Height                   (0018,1130) 88.5
   >Gantry/Detector Tilt           (0018,1120) 0
   >Data Collection Diameter       (0018,0090) 500
   ITEM 2                                      
   >Referenced Path Index          (0018,9378) 2
   >Rotation Direction             (0018,1140) CW
   >Revolution Time                (0018,9305) 0.5
   >Single Collimation Width       (0018,9306) 0.6
   >Total Collimation Width        (0018,9307) 38.4
   >Table Height                   (0018,1130) 88.5
   >Gantry/Detector Tilt           (0018,1120) 0
   >Data Collection Diameter       (0018,0090) 350
   =============================== =========== ==========

.. table:: CT Geometry Macro Attributes

   ========================================== =========== ==========
   **Attribute Name**                         **Tag**     **Values**
   ========================================== =========== ==========
   CT Geometry Sequence                       (0018,9312) 
   ITEM 1                                                 
   >Referenced Path Index                     (0018,9378) 1\2
   >Distance Source to Detector               (0018,1110) 1000
   >Distance Source to Data Collection Center (0018,9335) 500
   ========================================== =========== ==========

.. table:: Multi-energy CT Processing Attributes

   ========================= =========== =================
   Attribute Name            Tag         Values
   ========================= =========== =================
   Decomposition Method      (0018,937E) HYBRID
   Decomposition Description (0018,937F) iBHC + MAT DECOMP
   ========================= =========== =================

.. _sect_JJJJ.5.1.2:

Example Single Source Multi-layerdetector
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

This example shows a type Effective Atomic Number image acquired on an
acquisition device with a single source and multi-layer detector.

.. table:: CT Image Module Attributes

   +--------------------------+-------------+--------------------------+
   | **Attribute Name**       | **Tag**     | **Values**               |
   +==========================+=============+==========================+
   | Image Type               | (0008,0008) | ORIGINAL\PRIM            |
   |                          |             | ARY\AXIAL\EFF_ATOMIC_NUM |
   +--------------------------+-------------+--------------------------+
   | Multi-energy CT          | (0018,9361) | YES                      |
   | Acquisition              |             |                          |
   +--------------------------+-------------+--------------------------+
   | …                        |             |                          |
   +--------------------------+-------------+--------------------------+
   | Rescale Intercept        | (0028,1052) | 0                        |
   +--------------------------+-------------+--------------------------+
   | Rescale Slope            | (0028,1053) | 1.3                      |
   +--------------------------+-------------+--------------------------+
   | Rescale Type             | (0028,1054) | 10^-2 Z_EFF              |
   +--------------------------+-------------+--------------------------+
   | …                        |             |                          |
   +--------------------------+-------------+--------------------------+
   | KVP                      | (0018,0060) | {null value because it   |
   |                          |             | is described below}      |
   +--------------------------+-------------+--------------------------+
   | …                        |             |                          |
   +--------------------------+-------------+--------------------------+
   | Scan Options             | (0018,0022) | AXIAL                    |
   +--------------------------+-------------+--------------------------+
   | Data Collection Diameter | (0018,0090) | 500                      |
   +--------------------------+-------------+--------------------------+
   | …                        |             |                          |
   +--------------------------+-------------+--------------------------+
   | Distance Source to       | (0018,1110) | 1040                     |
   | Detector                 |             |                          |
   +--------------------------+-------------+--------------------------+
   | Distance Source to       | (0018,1111) | 570                      |
   | Patient                  |             |                          |
   +--------------------------+-------------+--------------------------+
   | Exposure Time            | (0018,1150) | 750                      |
   +--------------------------+-------------+--------------------------+
   | X-Ray Tube Current       | (0018,1151) | 440                      |
   +--------------------------+-------------+--------------------------+
   | Exposure                 | (0018,1152) | 330                      |
   +--------------------------+-------------+--------------------------+
   | Single Collimation Width | (0018,9306) | 0.625                    |
   +--------------------------+-------------+--------------------------+
   | Total Collimation Width  | (0018,9307) | 20.0                     |
   +--------------------------+-------------+--------------------------+
   | …                        |             |                          |
   +--------------------------+-------------+--------------------------+
   | *Include*                |             |                          |
   +--------------------------+-------------+--------------------------+

.. table:: Multi-energy CT Image Attributes

   +----------------------------------------------------+-------------+------------+
   | **Attribute Name**                                 | **Tag**     | **Values** |
   +====================================================+=============+============+
   | Multi-energy CT Acquisition Sequence               | (0018,9362) |            |
   +----------------------------------------------------+-------------+------------+
   | >Multi-energy Acquisition Description              | (0018,937B) |            |
   +----------------------------------------------------+-------------+------------+
   | *>Include*\ `table_title <#table_JJJJ.5.1.2-3>`__  |             |            |
   +----------------------------------------------------+-------------+------------+
   | *>Include*\ `table_title <#table_JJJJ.5.1.2-4>`__  |             |            |
   +----------------------------------------------------+-------------+------------+
   | *>Include*\ `table_title <#table_JJJJ.5.1.2-5>`__  |             |            |
   +----------------------------------------------------+-------------+------------+
   | *>Include*\ `table_title <#table_JJJJ.5.1.2-6>`__  |             |            |
   +----------------------------------------------------+-------------+------------+
   | *>Include*\ `table_title <#table_JJJJ.5.1.2-7>`__  |             |            |
   +----------------------------------------------------+-------------+------------+
   | *>Include*\ `table_title <#table_JJJJ.5.1.2-8>`__  |             |            |
   +----------------------------------------------------+-------------+------------+
   | *>Include*\ `table_title <#table_JJJJ.5.1.2-9>`__  |             |            |
   +----------------------------------------------------+-------------+------------+
   | Multi-energy CT Processing Sequence                | (0018,9363) |            |
   +----------------------------------------------------+-------------+------------+
   | *>Include*\ `table_title <#table_JJJJ.5.1.2-10>`__ |             |            |
   +----------------------------------------------------+-------------+------------+

.. table:: Multi-energy CT X-Ray Source Macro Attributes

   ===================================== =========== ===================
   **Attribute Name**                    **Tag**     **Values**
   ===================================== =========== ===================
   Multi-energy CT X-Ray Source Sequence (0018,9365) 
   ITEM 1                                            
   >X-Ray Source Index                   (0018,9366) 1
   >X-Ray Source ID                      (0018,9367) Tube A
   >Multi-energy Source Technique        (0018,9368) CONSTANT_SOURCE
   >Source Start DateTime                (0018,9369) 2018.05.01 13:22:03
   >Source End DateTime                  (0018,936A) 2018.05.01 13:22:20
   ===================================== =========== ===================

.. table:: Multi-energy CT X-Ray Detector Macro Attributes

   ======================================= =========== ===========
   **Attribute Name**                      **Tag**     **Values**
   ======================================= =========== ===========
   Multi-energy CT X-Ray Detector Sequence (0018,936F) 
   ITEM 1                                              
   >X-Ray Detector Index                   (0018,9370) 1
   >X-Ray Detector ID                      (0018,9371) Detector A
   >Multi-energy Detector Type             (0018,9372) MULTILAYER
   >X-Ray Detector Label                   (0018,9373) High-Energy
   ITEM 2                                              
   >X-Ray Detector Index                   (0018,9370) 2
   >X-Ray Detector ID                      (0018,9371) Detector A
   >Multi-energy Detector Type             (0018,9372) MULTILAYER
   >X-Ray Detector Label                   (0018,9373) Low-Energy
   ======================================= =========== ===========

.. table:: Multi-energy CT Path Macro Attributes

   ============================= =========== ==========
   **Attribute Name**            **Tag**     **Values**
   ============================= =========== ==========
   Multi-energy CT Path Sequence (0018,9379) 
   ITEM 1                                    
   >Multi-energy CT Path Index   (0018,937A) 1
   >X-Ray Source Index           (0018,9366) 1
   >X-Ray Detector Index         (0018,9370) 1
   ITEM 2                                    
   >Multi-energy CT Path Index   (0018,937A) 2
   >X-Ray Source Index           (0018,9366) 1
   >X-Ray Detector Index         (0018,9370) 2
   ============================= =========== ==========

.. table:: CT Exposure Macro Attributes

   ============================== =========== ==========
   **Attribute Name**             **Tag**     **Values**
   ============================== =========== ==========
   CT Exposure Sequence           (0018,9321) 
   ITEM 1                                     
   >Referenced X-Ray Source Index (0018,9377) 1
   >Exposure Time in ms           (0018,9328) 750
   >X-Ray Tube Current in mA      (0018,9330) 440
   >Exposure in mAs               (0018,9332) 330
   >Exposure Modulation Type      (0018,9323) NONE
   >CTDIvol                       (0018,9345) 34.9
   ============================== =========== ==========

.. table:: CT X-Ray Details Sequence Macro Attributes

   ========================= =========== ==========
   **Attribute Name**        **Tag**     **Values**
   ========================= =========== ==========
   CT X-Ray Details Sequence (0018,9325) 
   ITEM 1                                
   >Referenced Path Index    (0018,9378) 1\2
   >KVP                      (0018,0060) 120
   >Focal Spot(s)            (0018,1190) 1.4
   >Filter Type              (0018,1160) NONE
   >Filter Material          (0018,7050) 
   ========================= =========== ==========

.. table:: CT Acquisition Details Macro Attributes

   =============================== =========== ==========
   **Attribute Name**              **Tag**     **Values**
   =============================== =========== ==========
   CT Acquisition Details Sequence (0018,9304) 
   ITEM 1                                      
   >Referenced Path Index          (0018,9378) 1
   >Rotation Direction             (0018,1140) CW
   >Revolution Time                (0018,9305) 0.75
   >Single Collimation Width       (0018,9306) 0.625
   >Total Collimation Width        (0018,9307) 20.0
   >Table Height                   (0018,1130) 88.5
   >Gantry/Detector Tilt           (0018,1120) 0
   >Data Collection Diameter       (0018,0090) 500
   =============================== =========== ==========

.. table:: CT Geometry Macro Attributes

   ========================================== =========== ==========
   **Attribute Name**                         **Tag**     **Values**
   ========================================== =========== ==========
   CT Geometry Sequence                       (0018,9312) 
   ITEM 1                                                 
   >Referenced Path Index                     (0018,9378) 1
   >Distance Source to Detector               (0018,1110) 1140
   >Distance Source to Data Collection Center (0018,9335) 570
   ========================================== =========== ==========

.. table:: Multi-energy CT Processing Attributes

   +--------------------------+-------------+--------------------------+
   | Attribute Name           | Tag         | Values                   |
   +==========================+=============+==========================+
   | Decomposition Method     | (0018,937E) | PROJECTION_BASED         |
   +--------------------------+-------------+--------------------------+
   | Decomposition            | (0018,937F) | Photo-Electric / Compton |
   | Description              |             | Scattering Decomposition |
   +--------------------------+-------------+--------------------------+

.. _sect_JJJJ.5.2:

Examples For Material Quantification Image Family:
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

.. _sect_JJJJ.5.2.1:

Example Switching Source Integrating Detector
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

This example shows a Material Specific image acquired on an acquisition
device with single switching sources and integrating detector.

.. table:: CT Image Module Attributes

   +--------------------------+-------------+--------------------------+
   | **Attribute Name**       | **Tag**     | **Values**               |
   +==========================+=============+==========================+
   | Image Type               | (0008,0008) | ORIGINAL\PR              |
   |                          |             | IMARY\AXIAL\MAT_SPECIFIC |
   +--------------------------+-------------+--------------------------+
   | Multi-energy CT          | (0018,9361) | YES                      |
   | Acquisition              |             |                          |
   +--------------------------+-------------+--------------------------+
   | …                        |             |                          |
   +--------------------------+-------------+--------------------------+
   | Rescale Intercept        | (0028,1052) | 0                        |
   +--------------------------+-------------+--------------------------+
   | Rescale Slope            | (0028,1053) | 1                        |
   +--------------------------+-------------+--------------------------+
   | Rescale Type             | (0028,1054) | 10^-2 MGML               |
   +--------------------------+-------------+--------------------------+
   | …                        |             |                          |
   +--------------------------+-------------+--------------------------+
   | KVP                      | (0018,0060) | {null value because it   |
   |                          |             | is described below}      |
   +--------------------------+-------------+--------------------------+
   | …                        |             |                          |
   +--------------------------+-------------+--------------------------+
   | Single Collimation Width | (0018,9306) | 0.625                    |
   +--------------------------+-------------+--------------------------+
   | Total Collimation Width  | (0018,9307) | 80.0                     |
   +--------------------------+-------------+--------------------------+
   | …                        |             |                          |
   +--------------------------+-------------+--------------------------+
   | *Include*                |             |                          |
   +--------------------------+-------------+--------------------------+

.. table:: Multi-energy CT Image Attributes

   +--------------------------+-------------+------------------------+
   | **Attribute Name**       | **Tag**     | **Values**             |
   +==========================+=============+========================+
   | Multi-energy CT          | (0018,9362) |                        |
   | Acquisition Sequence     |             |                        |
   +--------------------------+-------------+------------------------+
   | >Multi-energy            | (0018,937B) | KV Switching Technique |
   | Acquisition Description  |             |                        |
   +--------------------------+-------------+------------------------+
   | *                        |             |                        |
   | >Include*\ `table_title  |             |                        |
   | <#table_JJJJ.5.2.1-3>`__ |             |                        |
   +--------------------------+-------------+------------------------+
   | *                        |             |                        |
   | >Include*\ `table_title  |             |                        |
   | <#table_JJJJ.5.2.1-4>`__ |             |                        |
   +--------------------------+-------------+------------------------+
   | *                        |             |                        |
   | >Include*\ `table_title  |             |                        |
   | <#table_JJJJ.5.2.1-5>`__ |             |                        |
   +--------------------------+-------------+------------------------+
   | *                        |             |                        |
   | >Include*\ `table_title  |             |                        |
   | <#table_JJJJ.5.2.1-6>`__ |             |                        |
   +--------------------------+-------------+------------------------+
   | *                        |             |                        |
   | >Include*\ `table_title  |             |                        |
   | <#table_JJJJ.5.2.1-7>`__ |             |                        |
   +--------------------------+-------------+------------------------+
   | *                        |             |                        |
   | >Include*\ `table_title  |             |                        |
   | <#table_JJJJ.5.2.1-8>`__ |             |                        |
   +--------------------------+-------------+------------------------+
   | *                        |             |                        |
   | >Include*\ `table_title  |             |                        |
   | <#table_JJJJ.5.2.1-9>`__ |             |                        |
   +--------------------------+-------------+------------------------+
   | Multi-energy CT          | (0018,9363) |                        |
   | Processing Sequence      |             |                        |
   +--------------------------+-------------+------------------------+
   | *>                       |             |                        |
   | Include*\ `table_title < |             |                        |
   | #table_JJJJ.5.2.1-10>`__ |             |                        |
   +--------------------------+-------------+------------------------+

.. table:: Multi-energy CT X-Ray Source Macro Attributes

   ===================================== =========== ===================
   **Attribute Name**                    **Tag**     **Values**
   ===================================== =========== ===================
   Multi-energy CT X-Ray Source Sequence (0018,9365) 
   ITEM 1                                            
   >X-Ray Source Index                   (0018,9366) 1
   >X-Ray Source ID                      (0018,9367) Tube A
   >Multi-energy Source Technique        (0018,9368) SWITCHING_SOURCE
   >Source Start DateTime                (0018,9369) 2018.05.01 13:22:03
   >Source End DateTime                  (0018,936A) 2018.05.01 13:22:20
   >Switching Phase Number               (0018,936B) 1
   >Switching Phase Nominal Duration     (0018,936C) 100
   >Switching Phase Transition Duration  (0018,936D) 10
   >Generator Power                      (0018,1170) 120
   ITEM 2                                            
   >X-Ray Source Index                   (0018,9366) 2
   >X-Ray Source ID                      (0018,9367) Tube A
   >Multi-energy Source Technique        (0018,9368) SWITCHING_SOURCE
   >Source Start DateTime                (0018,9369) 2018.05.01 13:22:03
   >Source End DateTime                  (0018,936A) 2018.05.01 13:22:20
   >Switching Phase Number               (0018,936B) 2
   >Switching Phase Nominal Duration     (0018,936C) 100
   >Switching Phase Transition Duration  (0018,936D) 10
   >Generator Power                      (0018,1170) 100
   ===================================== =========== ===================

.. table:: Multi-energy CT X-Ray Detector Macro Attributes

   ======================================= =========== ===========
   **Attribute Name**                      **Tag**     **Values**
   ======================================= =========== ===========
   Multi-energy CT X-Ray Detector Sequence (0018,936F) 
   ITEM 1                                              
   >X-Ray Detector Index                   (0018,9370) 1
   >X-Ray Detector ID                      (0018,9371) Detector A
   >Multi-energy Detector Type             (0018,9372) INTEGRATING
   ======================================= =========== ===========

.. table:: Multi-energy CT Path Macro Attributes

   ============================= =========== ==========
   **Attribute Name**            **Tag**     **Values**
   ============================= =========== ==========
   Multi-energy CT Path Sequence (0018,9379) 
   ITEM 1                                    
   >Multi-energy CT Path Index   (0018,937A) 1
   >X-Ray Source Index           (0018,9366) 1
   >X-Ray Detector Index         (0018,9370) 1
   ITEM 2                                    
   >Multi-energy CT Path Index   (0018,937A) 2
   >X-Ray Source Index           (0018,9366) 2
   >X-Ray Detector Index         (0018,9370) 1
   ============================= =========== ==========

.. table:: CT Exposure Macro Attributes

   ============================== =========== ==========
   **Attribute Name**             **Tag**     **Values**
   ============================== =========== ==========
   CT Exposure Sequence           (0018,9321) 
   ITEM 1                                     
   >Referenced X-Ray Source Index (0018,9377) 1\2
   >Exposure Time in ms           (0018,9328) 500
   >X-Ray Tube Current in mA      (0018,9330) 300
   >Exposure in mAs               (0018,9332) 150
   >Exposure Modulation Type      (0018,9323) NONE
   >CTDIvol                       (0018,9345) 10
   ============================== =========== ==========

.. table:: CT X-Ray Details Sequence Macro Attributes

   ========================= =========== ==========
   **Attribute Name**        **Tag**     **Values**
   ========================= =========== ==========
   CT X-Ray Details Sequence (0018,9325) 
   ITEM 1                                
   >Referenced Path Index    (0018,9378) 1
   >KVP                      (0018,0060) 80
   >Focal Spot(s)            (0018,1190) 0.5\0.5
   >Filter Type              (0018,1160) NONE
   ITEM 2                                
   >Referenced Path Index    (0018,9378) 2
   >KVP                      (0018,0060) 140
   >Focal Spot(s)            (0018,1190) 0.5\0.5
   >Filter Type              (0018,1160) NONE
   ========================= =========== ==========

.. table:: CT Acquisition Details Macro Attributes

   =============================== =========== ==========
   **Attribute Name**              **Tag**     **Values**
   =============================== =========== ==========
   CT Acquisition Details Sequence (0018,9304) 
   ITEM 1                                      
   >Referenced Path Index          (0018,9378) 1\2
   >Rotation Direction             (0018,1140) CW
   >Revolution Time                (0018,9305) 0.5
   >Single Collimation Width       (0018,9306) 0.625
   >Total Collimation Width        (0018,9307) 80.0
   >Table Height                   (0018,1130) 88.5
   >Gantry/Detector Tilt           (0018,1120) 0
   >Data Collection Diameter       (0018,0090) 500
   =============================== =========== ==========

.. table:: CT Geometry Macro Attributes

   ========================================== =========== ==========
   **Attribute Name**                         **Tag**     **Values**
   ========================================== =========== ==========
   CT Geometry Sequence                       (0018,9312) 
   ITEM 1                                                 
   >Referenced Path Index                     (0018,9378) 1\2
   >Distance Source to Detector               (0018,1110) 1140
   >Distance Source to Data Collection Center (0018,9335) 570
   ========================================== =========== ==========

.. table:: Multi-energy CT Processing Attributes

   +------------------------+------------------------+------------------+
   | Attribute Name         | Tag                    | Values           |
   +========================+========================+==================+
   | Decomposition Method   | (0018,937E)            | PROJECTION_BASED |
   +------------------------+------------------------+------------------+
   | Decomposition Material | (0018,9381)            |                  |
   | Sequence               |                        |                  |
   +------------------------+------------------------+------------------+
   | ITEM 1                 |                        |                  |
   +------------------------+------------------------+------------------+
   | >Material Code         | (0018,937D)            |                  |
   | Sequence               |                        |                  |
   +------------------------+------------------------+------------------+
   | *>>Include*            | `(11713004, SCT,       |                  |
   |                        | "Water") <http://snome |                  |
   |                        | d.info/id/11713004>`__ |                  |
   +------------------------+------------------------+------------------+
   | ITEM 2                 |                        |                  |
   +------------------------+------------------------+------------------+
   | >Material Code         | (0018,937D)            |                  |
   | Sequence               |                        |                  |
   +------------------------+------------------------+------------------+
   | *>>Include*            | `(44588005, SCT,       |                  |
   |                        | "                      |                  |
   |                        | Iodine") <http://snome |                  |
   |                        | d.info/id/44588005>`__ |                  |
   +------------------------+------------------------+------------------+

