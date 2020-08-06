.. _chapter_B:

Creating a Privately Defined Unique Identifier (Informative)
============================================================

Privately defined Unique Identifiers (UIDs) are used in DICOM to
uniquely identify items such as Specialized or Private SOP Classes,
Image SOP Instances, Study SOP Instances, etc.

.. _sect_B.1:

Organizationally Derived UID
----------------------------

A UID may be formed using a registered root (see `DICOM Unique
Identifier Registration Process (Informative) <#chapter_C>`__) and an
organization specific suffix. The manner in which the suffix of such an
organizationally derived UID is defined is not constrained by the DICOM
Standard. Only the guarantee of its uniqueness by the defining
organization is required by DICOM.

The following example presents a particular choice made by a specific
organization in defining its suffix to guarantee uniqueness of a SOP
Instance UID.

::

     "1.2.840.xxxxx.3.152.235.2.12.187636473"
      \___________/ \______________________/
          root     .         suffix

In this example, the root is:

-  1 Identifies ISO

-  2 Identifies ANSI Member Body

-  840 Country code of a specific Member Body (U.S. for ANSI)

-  xxxxx Identifies a specific Organization.(assigned by ANSI)

In this example the first two components of the suffix relate to the
identification of the device:

-  3 Manufacturer defined device type

-  152 Manufacturer defined serial number

The remaining four components of the suffix relate to the identification
of the image:

-  235 Study number

-  2 Series number

-  12 Image number

-  187636473 Encoded date and time stamp of image acquisition

In this example, the organization has chosen these components to
guarantee uniqueness. Other organizations may choose an entirely
different series of components to uniquely identify its images. For
example it may have been perfectly valid to omit the Study Number,
Series Number and Image Number if the time stamp had a sufficient
precision to ensure that no two images might have the same date and time
stamp.

Because of the flexibility allowed by the DICOM Standard in creating
organizationally derived UIDs, implementations should not depend on any
assumed structure of UIDs and should not attempt to parse UIDs to
extract the semantics of some of its components.

.. _sect_B.2:

UUID Derived UID
----------------

`biblioentry_title <#biblio_ISOIEC9834-8>`__ /
`biblioentry_title <#biblio_ITU-T_X.667>`__ defines a method by which a
UID may be constructed from the root "2.25." followed by a decimal
representation of a Universally Unique Identifier (UUID). That decimal
representation treats the 128 bit UUID as an integer, and may thus be up
to 39 digits long (leading zeros must be suppressed).

A UUID derived UID may be appropriate for dynamically created UIDs, such
as SOP Instance UIDs, but is usually not appropriate for UIDs determined
during application software design, such as private SOP Class or
Transfer Syntax UIDs, or Implementation Class UIDs.

