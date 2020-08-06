.. _chapter_7:

Referencing The DICOM Standard
==============================

Under the procedures of the DICOM Standards Committee, the Standard is
in constant revision. Supplements and corrections to the Standard are
balloted and approved several times a year. Each change when approved as
Final Text immediately goes into effect. At intervals, all of the
approved Final Text changes are consolidated into a published edition of
the Standard, identified by year of publication, but such publication is
only a convenience to the user; the Standard is officially changed when
each change is approved.

Conformance to the DICOM Standard is through specified SOP Classes using
DIMSE messages (see ), Web Services (see ), media interchange (see and
), or the hosted application API (see ). Additional conformance claims
may be made to Profiles (see and ). Once such a unit of conformance is
specified in the Standard, all changes thereto are forward and backward
compatible (except in rare cases where the original specification was
non-interoperable, or conflicted with another standard). Conformance
requirements and conformance claims are therefore referenced to the name
and/or identifier of the feature, and never referenced to an edition of
the Standard. Generally, the only appropriate reference to a particular
edition of the Standard is to identify a retired feature (see
`Continuous Maintenance <#sect_1.4.2>`__).

The following citation form is preferred for general references to the
Standard, without specification of date of edition, when specific
conformance requirements are not invoked:

NEMA PS3 / ISO 12052, Digital Imaging and Communications in Medicine
(DICOM) Standard, National Electrical Manufacturers Association,
Rosslyn, VA, USA (available free at http://www.dicomstandard.org/)

The requirements of this section do not override the requirement to
provide a DICOM Conformance Statement as described in .

The following forms are preferred for references to units of conformance
to the Standard when they are made outside the context of a DICOM
Conformance Statement (e.g., in customer requirements):

-  “… conformant to the DICOM <name> SOP Class for network exchange [as
   a Service Class <User \| Provider>], as specified in DICOM : Service
   Class Specifications.”

-  “… conformant to the DICOM <name> SOP Class for media exchange [as a
   File Set <Creator \| Updater \| Reader>], as specified in DICOM :
   Service Class Specifications.”

-  “… conformant to the DICOM <name> Web Service [as <an Origin-server
   \| a User-agent>] [for the <name> SOP Class], as specified in DICOM :
   Web Services.”

-  “… conformant to DICOM Application Hosting [as a <Hosting System \|
   Hosted Application>] for the <name> SOP Class, as specified in DICOM
   : Application Hosting.”

-  “… conformant to the DICOM <identifier> Application Profile [as a
   File Set <Creator \| Updater \| Reader>] [for the <name> SOP Class],
   as specified in DICOM : Media Storage Application Profiles.”

-  “… conformant to the DICOM <name> Profile, as specified in DICOM :
   Security and System Management Profiles.”

.. note::

   1. Some Application Profiles and Web Services may fully specify the
      information objects exchanged, while others may require explicit
      specification of SOP Classes in the references.

   2. Examples:

      -  “The modality shall be conformant to the DICOM CT Image Storage
         and MR Image Storage SOP Classes for network exchange as a
         Service Class User, as specified in DICOM : Service Class
         Specifications.”

      -  “The workstation shall be conformant to the DICOM STD-XA1K-DVD
         Application Profile as a File Set Reader, as specified in DICOM
         : Media Storage Application Profiles.”

      -  “The PACS shall be conformant to the DICOM WADO-RS and STOW-RS
         Web Services as an Origin-server for the SOP Classes listed in
         Table X, as specified in DICOM : Web Services.”

   3. Such references are not permitted in lieu of a Conformance
      Statement for a product. For example, a product that reads or
      creates DICOM interchange media is required to have a Conformance
      Statement (as described in ) that enumerates the Media Application
      Profiles it implements. A statement in some other format, or a
      document that describes that a product supports recording of files
      of a particular SOP Class defined in , is not sufficient as an
      alternative to a Conformance Statement.

Reference may be made to other features of the Standard, but these shall
not be construed as DICOM conformance requirements (although they may be
conformance requirements for non-DICOM implementation guides or
regulations). Following are some examples:

-  “… SOP Instances in accordance with the <name> Information Object
   Definition, as specified in DICOM : Information Object Definitions.”

-  “… Structured Reporting SOP Instances using DICOM Template ID <number
   and name>, as specified in DICOM : Content Mapping Resource.”

-  “… HL7 CDA instances using Template ID <identifier and name>, as
   specified in DICOM : Imaging Reports using HL7 Clinical Document
   Architecture.”

-  “… using the <name> Transfer Syntax, as specified in DICOM : Data
   Structure and Semantics.”

.. note::

   For example, products producing or receiving SR documents must
   conform to a SOP Class, such as Enhanced SR; such products may also
   cite use of Template ID 5200 Echocardiography Procedure Report, but
   that is not a formal DICOM Conformance assertion. However, a
   non-DICOM implementation guide, such as the IHE Echocardiography
   Workflow Profile, may require use of that Template, and an
   implementation may describe its use of specific Templates in its
   Conformance Statement.

Since changes to the Standard shall not be cited prior to adoption as
Final Text, and since after adoption they are formally part of the
Standard, there should be no citations to supplements or correction
items for the purpose of describing conformance. Reference to such
change documents may be made for describing the historical development
of the DICOM Standard.
