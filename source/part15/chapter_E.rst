.. _chapter_E:

Attribute Confidentiality Profiles
==================================

This Annex describes Profiles and Options to address the removal and
replacement of Attributes within a DICOM Dataset that may potentially
result in leakage of Individually Identifiable Information (III) about
the patient or other individuals or organizations involved in
acquisition.

Profiles are provided to address the balance between the removal of
information and the need to retain information so that the Datasets
remain useful for their intended purpose.

Options are used in addition to profiles to prevent a combinatorial
expansion of different Profiles.

.. _sect_E.1:

Application Level Confidentiality Profiles
------------------------------------------

Application Level Confidentiality Profiles address the following aspects
of security:

-  Data Confidentiality at the application layer.

Other aspects of security not addressed by these profiles, that may be
addressed elsewhere in the Standard include:

-  Confidentiality in other layers of the DICOM model;

-  Data Integrity.

These Profiles are targeted toward creating a special purpose,
de-identified version of an already-existing Data Set. It is not
intended to replace the original SOP Instance from which the
de-identified SOP Instance is created, nor is it intended to act as the
primary representation of clinical Data Sets in image archives. The
de-identified SOP Instances are useful, for example, in creating
teaching or research files, performing clinical trials, or submission to
registries where the identity of the patient and other individuals is
required to be protected. In some cases, it is also necessary to provide
a means of recovering identity by authorized personnel.

.. _sect_E.1.1:

De-identifier
~~~~~~~~~~~~~

An Application may claim conformance to an Application Level
Confidentiality Profile and Options as a de-identifier if it protects
and retains *all*\ Attributes as specified in the Profile and Options.
Protection in this context is defined as the following process:

1. The application may create one or more instances of the Encrypted
   Attributes Data Set and copy Attributes to be protected into the
   (single) item of the Modified Attributes Sequence (0400,0550) of one
   or more of the Encrypted Attributes Data Set instances.

   .. note::

      1. A complete reconstruction of the original Data Set may not be
         possible; however, Attributes (e.g., SOP Instance UID) in the
         Modified Attributes Sequence of an Encrypted Attributes Data
         Set may refer back to the original SOP Instance holding the
         original Data Set.

      2. It is not required that the Encrypted Attributes Data Set be
         created; indeed, there may be circumstances where the Dataset
         is expected to be archived long enough that any contemporary
         encryption technology may be inadequate to provide long term
         protection against unauthorized recovery of identification.

      3. Other mechanisms to assist in identity recovery or longitudinal
         consistency of replaced UIDs or dates and times are deprecated
         in favor of the Encrypted Attributes Data Set mechanism that is
         intended for this purpose. For example, if it is desired to
         include an encrypted hash of the Patient's Name, it should not
         be encoded in a separate private attribute implemented for that
         purpose, but should be included in the Encrypted Attributes
         Data Set and encoded using the standard mechanism. This allows
         for compatibility between different implementations and
         provides security based on the quality and control of the
         encryption keys. Note also, that unencrypted hashes are
         considerably less secure and should be avoided, since they are
         vulnerable to trivial dictionary based attacks.

2. Each Attribute to be protected shall then either be removed from the
   dataset, or have its value replaced by a different "replacement
   value" that does not allow identification of the patient.

   .. note::

      1. It is the responsibility of the de-identifier to ensure that
         this process does not negatively affect the integrity of the
         Information Object Definition, i. e. Dummy values may be
         necessary for Type 1 Attributes that are protected but may not
         be sent with zero length, and are to be stored or exchanged in
         encrypted form by applications that may not be aware of the
         security mechanism.

      2. The Standard does not mandate the use of any particular dummy
         value, and indeed it may have some meaning, for example in data
         that may be used for teaching purposes, where the real patient
         identifying information is encrypted for later retrieval, but a
         meaningful alternative form of identification is provided. For
         example, a dummy Patient's Name (0010,0010) may convey the type
         of pathology in a teaching case. It is the responsibility of
         the de-identifier software or human operator to ensure that the
         dummy values cannot be used to identify the patient.

      3. It is the responsibility of the de-identifier to ensure the
         consistency of dummy values for Attributes such as Study
         Instance UID (0020,000D) or Frame of Reference UID (0020,0052)
         if multiple related SOP Instances are protected. Indeed, all
         Attributes of every entity about the Instance level should
         remain consistent for all Instances protected, e.g., Patient ID
         for the Patient entity, Study ID for the Study entity, Series
         Number for the Series entity.

      4. Some profiles do not allow selective protection of parts of a
         Sequence of Items. If an Attribute to be protected is contained
         in a Sequence of Items, the complete Sequence of Items may need
         to be protected.

      5. The de-identifier should ensure that no identifying information
         that is burned in to the image pixel data either because the
         modality does not generate such burned in identification in the
         first place, or by removing it through the use of the Clean
         Pixel Data Option; see `Basic Application Level Confidentiality
         Options <#sect_E.3>`__. If non-pixel data graphics or overlays
         contain identification, the de-identifier is required to remove
         them, or clean them if the Clean Graphics option is supported.
         See `Clean Graphics Option <#sect_E.3.3>`__ The means by which
         burned in or graphic identifying information is located and
         removed is outside the scope of this Standard.

3. Each Attribute specified to be retained shall be retained. At the
   discretion of the de-identifier, Attributes may be added to the
   dataset to be protected.

   .. note::

      As an example, the Attribute Patient's Age (0010,1010) might be
      introduced as a replacement for Patient's Birth Date (0010,0030)
      if the patient's age is of importance, and the profile permits it.

4. If used, all instances of the Encrypted Attributes Data Set shall be
   encoded with a DICOM Transfer Syntax, encrypted, and stored in the
   dataset to be protected as an Item of the Encrypted Attributes
   Sequence (0400,0500). The encryption shall be done using RSA
   `biblioentry_title <#biblio_RFC_2313>`__ for the key transport of the
   content-encryption keys. A de-identifier conforming to this security
   profile may use either AES or Triple-DES for content-encryption. The
   AES key length may be any length allowed by the RFCs. The Triple-DES
   key length is 168 bits as defined by
   `biblioentry_title <#biblio_ANSIX9.52>`__. Encoding shall be
   performed according to the specifications for RSA Key Transport and
   Triple DES Content Encryption in
   `biblioentry_title <#biblio_RFC_3370>`__ and for AES Content
   Encryption in `biblioentry_title <#biblio_RFC_3565>`__.

   .. note::

      1. Each item of the Encrypted Attributes Sequence (0400,0500)
         consists of two Attributes, Encrypted Content Transfer Syntax
         UID (0400,0510) containing the UID of the Transfer Syntax that
         was used to encode the instance of the Encrypted Attributes
         Data Set, and Encrypted Content (0400,0520) containing the
         block of data resulting from the encryption of the Encrypted
         Attributes Data Set instance.

      2. RSA key transport of the content-encryption keys is specified
         as a requirement in the European Prestandard ENV 13608-2:
         Health Informatics - Security for healthcare communication -
         Part 2: Secure data objects.

5. No requirements on the size of the asymmetric key pairs used for RSA
   key transport are defined in this confidentiality scheme.
   Implementations claiming conformance to the Basic Application Level
   Confidentiality Profile as a de-identifier shall always protect
   (e.g., encrypt and replace) the SOP Instance UID (0008,0018)
   Attribute as well as all references to other SOP Instances, whether
   contained in the main dataset or embedded in an Item of a Sequence of
   Items, that could potentially be used by unauthorized entities to
   identify the patient.

   .. note::

      In the case of a SOP Instance UID embedded in an Item of a
      Sequence, this means that the enclosing Attribute in the top-level
      Data Set must be encrypted in its entirety.

6. The attribute Patient Identity Removed (0012,0062) shall be replaced
   or added to the dataset with a value of YES, and one or more codes
   from corresponding to the profile and options used shall be added to
   De-identification Method Code Sequence (0012,0064). A text string
   describing the method used may also be inserted in or added to
   De-identification Method (0012,0063), but is not required.

7. If the Dataset being de-identified is being stored within a DICOM
   File, then the File Meta Information including the 128 byte preamble,
   if present, shall be replaced with a description of the
   de-identifying application. Otherwise, there is a risk that identity
   information may leak through unmodified File Meta Information or
   preamble. See .

8. If the Dataset being de-identified is being communicated by DICOM
   Real-Time Video, then the File Meta Information including the 128
   byte preamble, if present, shall be replaced with a description of
   the de-identifying application. Otherwise, there is a risk that
   identity information may leak through unmodified File Meta
   Information or preamble. See .

The Attributes listed in `table_title <#table_E.1-1>`__ for each profile
are contained in Standard IODs, or may be contained in Standard Extended
IODs. An implementation claiming conformance to an Application Level
Confidentiality Profile as a de-identifier shall protect or retain all
instances of the Attributes listed in `table_title <#table_E.1-1>`__,
whether contained in the main dataset or embedded in an Item of a
Sequence of Items. The following action codes are used in the table:

-  D - replace with a non-zero length value that may be a dummy value
   and consistent with the VR

-  Z - replace with a zero length value, or a non-zero length value that
   may be a dummy value and consistent with the VR

-  X - remove

-  K - keep (unchanged for non-sequence attributes, cleaned for
   sequences)

-  C - clean, that is replace with values of similar meaning known not
   to contain identifying information and consistent with the VR

-  U - replace with a non-zero length UID that is internally consistent
   within a set of Instances

-  Z/D - Z unless D is required to maintain IOD conformance (Type 2
   versus Type 1)

-  X/Z - X unless Z is required to maintain IOD conformance (Type 3
   versus Type 2)

-  X/D - X unless D is required to maintain IOD conformance (Type 3
   versus Type 1)

-  X/Z/D - X unless Z or D is required to maintain IOD conformance (Type
   3 versus Type 2 versus Type 1)

-  X/Z/U\* - X unless Z or replacement of contained instance UIDs (U) is
   required to maintain IOD conformance (Type 3 versus Type 2 versus
   Type 1 sequences containing UID references)

These action codes are applicable to both Sequence and non-Sequence
attributes; in the case of Sequences, the action is applicable to the
Sequence and all of its contents. Cleaning a sequence ("C" action) may
entail either changing values of attributes within that Sequence when
the meaning of the Sequence within the context of its use in the IOD is
understood, or recursively applying the profile rules to each Dataset in
each Item of the Sequence. Keeping a Sequence ("K" action) requires
recursively applying the profile rules to each Dataset in each Item of
the Sequence (for example, in order to remap any UIDs contained within
that sequence).

A requirement for an Option, when implemented, overrides any requirement
for the underlying Profile.

.. note::

   1.  The Attributes listed in `table_title <#table_E.1-1>`__ may not
       be sufficient to guarantee confidentiality of patient identity.
       In particular, identifying information may be contained in
       Private Attributes, new Standard Attributes, Retired Standard
       Attributes and additional Standard Attributes not present in
       Standard Composite IODs (as defined in ) but used in Standard
       Extended SOP Classes. `table_title <#table_E.1-1>`__ indicates
       those Attributes that are used in Standard Composite IODs as well
       as those Attributes that are Retired. Also included in
       `table_title <#table_E.1-1>`__ are some Elements that are not
       normally found in a Dataset, but are used in Commands,
       Directories and Meta Information Headers, but that could be
       misused within Private Sequences. Textual Content Items of
       Structured Reports, textual annotations of Presentation States,
       Curves and Overlays are specifically addressed. It is the
       responsibility of the de-identifier to ensure that all
       identifying information is removed.

   2.  It should be noted that conformance to an Application Level
       Confidentiality Profile does not necessarily guarantee
       confidentiality. For example, if an attacker already has access
       to the original images, the Pixel Data could be matched, though
       the probability and impact of such a threat may be deemed to be
       negligible. If the Encrypted Attributes Sequence is used, it
       should be understood that any encryption scheme may be vulnerable
       to attack. Also, an organization's Security Policy and Key
       Management policy are recognized to have a much greater impact on
       the effectiveness of protection.

   3.  National and local regulations, which may vary, might require
       that additional attributes be de-identified, though the Profiles
       and Options have been designed to be sufficient to satisfy known
       regulations without compromising the usefulness of the
       de-identified instances for their intended purpose.

   4.  `table_title <#table_E.1-1>`__ is normative, but it is subject to
       extension as the DICOM Standard evolves and other similar
       Attributes are added to IODs. De-identifiers may take this
       extensibility into account, for example, by considering handling
       all dates and times on the basis of their Value Representation of
       DT, DA or TM, rather than just those date and time Attributes
       lists.

   5.  The Profiles and Options do not specify whether the design of a
       de-identifier should be to remove what is know to be a risk of
       identity leakage, or to retain only what is known to be safe. The
       former approach may fail when the Standard is extended, or when a
       vendor adds unanticipated standard or private attributes, whilst
       the latter requires an extensive, if not complete, comparison of
       each instance with the Information Object Definitions in to avoid
       discarding required or useful information.
       `table_title <#table_E.1-1>`__ defines the minimum actions
       required for conformance.

   6.  De-identification of Private SOP Classes is not defined.

   7.  The "C" (clean) action is specified not only for string VRs, but
       also for Code Sequences, since the use of private or local codes
       and non-standard code meanings may potentially cause identity
       leakage.

   8.  The Digital Signatures Sequences needs to be removed because it
       contains the certificate of the signer; theoretically the
       signature could be verified and the object re-signed by the
       de-identifier itself with its own certificate, but this is not
       required by the Standard.

   9.  In general, there are no CS VR Attributes in this table, since it
       is usually safe to assume that code strings do not contain
       identifying information.

   10. In general, there are no Code Sequence Attributes in this table,
       since it is usually safe to assume that coded sequence entries,
       including private codes, do not contain identifying information.
       Exceptions are codes for providers and staff.

   11. The Clean Pixel Data and Clean Recognizable Visual Features
       Options are not listed in this table, since they are defined by
       descriptions of operations on the Pixel Data itself. The Clean
       Pixel Data option may be applied to the Pixel Data within the
       Icon Image Sequence, or more likely the Icon Image Sequence may
       be recreated entirely once the Pixel Data of the main Dataset has
       been cleaned. The Icon Image Sequence is to be removed when its
       Pixel Data cannot be cleaned.

   12. The Original Attributes Sequence (0400,0561) (which in turn
       contains the Modified Attributes Sequence (0400,0550) ) generally
       needs to be removed, because it may contain unencrypted copies of
       other Attributes that may have been modified (e.g., coerced to
       use local identifiers and names during import of foreign images);
       an alternative approach would be to selectively modify its
       contents. This is distinct from the use of the Modified
       Attributes Sequence (0400,0550) within the Encrypted Attributes
       Sequence (0400,0500).

   13. `table_title <#table_E.1-1>`__ distinguishes Attributes that are
       in standard Composite IODs defined in from those that are not;
       some Attributes are defined in for other IODs, or have a specific
       usage other than in the top level Dataset of a Composite IOD, but
       are (mis-) used by implementers in instances as a Standard
       Extended SOP Class at other levels than as defined by the
       Standard. Any such Attributes encountered may be removed without
       compromising the conformance of the instance with the standard
       IOD. For example, Verifying Observer Sequence (0040,A073) is only
       defined in structured report IODs and hence is described in
       `table_title <#table_E.1-1>`__ as D since it is Type 1C; if
       encountered in an image instance, it should simply be removed
       (treated as X).

.. table:: Application Level Confidentiality Profile Attributes

   +-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+
   | *     | **    | **    | **In  | **    | *     | *     | *     | *     | *     | *     | *     | **    | **    | **    |
   | *Attr | Tag** | Retd. | Std.  | Basic | *Rtn. | *Rtn. | *Rtn. | *Rtn. | *Rtn. | *Rtn. | *Rtn. | Clean | Clean | Clean |
   | ibute |       | (from | Comp. | Pr    | Safe  | UIDs  | Dev.  | Inst. | Pat.  | Long. | Long. | Desc. | St    | G     |
   | N     |       | )**   | IOD   | of.** | Priv. | O     | Id.   | Id.   | C     | Full  | M     | O     | ruct. | raph. |
   | ame** |       |       | (from |       | O     | pt.** | O     | O     | hars. | Dates | odif. | pt.** | Cont. | O     |
   |       |       |       | )**   |       | pt.** |       | pt.** | pt.** | O     | O     | Dates |       | O     | pt.** |
   |       |       |       |       |       |       |       |       |       | pt.** | pt.** | O     |       | pt.** |       |
   |       |       |       |       |       |       |       |       |       |       |       | pt.** |       |       |       |
   +=======+=======+=======+=======+=======+=======+=======+=======+=======+=======+=======+=======+=======+=======+=======+
   | Acce  | (     | N     | Y     | Z     |       |       |       |       |       |       |       |       |       |       |
   | ssion | 0008, |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | N     | 0050) |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | umber |       |       |       |       |       |       |       |       |       |       |       |       |       |       |
   +-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+
   | A     | (     | Y     | N     | X     |       |       |       |       |       |       |       | C     |       |       |
   | cquis | 0018, |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | ition | 4000) |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | Com   |       |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | ments |       |       |       |       |       |       |       |       |       |       |       |       |       |       |
   +-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+
   | A     | (     | N     | Y     | X/Z   |       |       |       |       |       |       |       |       | C     |       |
   | cquis | 0040, |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | ition | 0555) |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | Co    |       |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | ntext |       |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | Seq   |       |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | uence |       |       |       |       |       |       |       |       |       |       |       |       |       |       |
   +-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+
   | A     | (     | N     | Y     | X/Z   |       |       |       |       |       | K     | C     |       |       |       |
   | cquis | 0008, |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | ition | 0022) |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | Date  |       |       |       |       |       |       |       |       |       |       |       |       |       |       |
   +-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+
   | A     | (     | N     | Y     | X/Z/D |       |       |       |       |       | K     | C     |       |       |       |
   | cquis | 0008, |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | ition | 002A) |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | Dat   |       |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | eTime |       |       |       |       |       |       |       |       |       |       |       |       |       |       |
   +-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+
   | A     | (     | N     | Y     | X/D   |       |       |       |       |       |       |       | C     |       |       |
   | cquis | 0018, |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | ition | 1400) |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | D     |       |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | evice |       |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | Proce |       |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | ssing |       |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | D     |       |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | escri |       |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | ption |       |       |       |       |       |       |       |       |       |       |       |       |       |       |
   +-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+
   | A     | (     | N     | Y     | X     |       |       |       |       |       |       |       | C     |       |       |
   | cquis | 0018, |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | ition | 9424) |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | Pro   |       |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | tocol |       |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | D     |       |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | escri |       |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | ption |       |       |       |       |       |       |       |       |       |       |       |       |       |       |
   +-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+
   | A     | (     | N     | Y     | X/Z   |       |       |       |       |       | K     | C     |       |       |       |
   | cquis | 0008, |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | ition | 0032) |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | Time  |       |       |       |       |       |       |       |       |       |       |       |       |       |       |
   +-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+
   | A     | (     | N     | N     | X     |       |       |       |       |       |       |       |       |       |       |
   | ctual | 0040, |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | Human | 4035) |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | Perfo |       |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | rmers |       |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | Seq   |       |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | uence |       |       |       |       |       |       |       |       |       |       |       |       |       |       |
   +-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+
   | Addit | (     | N     | Y     | X     |       |       |       |       |       |       |       | C     |       |       |
   | ional | 0010, |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | Pa    | 21B0) |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | tient |       |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | Hi    |       |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | story |       |       |       |       |       |       |       |       |       |       |       |       |       |       |
   +-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+
   | Ad    | (     | Y     | N     | X     |       |       |       |       |       |       |       |       |       |       |
   | dress | 0040, |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | (T    | A353) |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | rial) |       |       |       |       |       |       |       |       |       |       |       |       |       |       |
   +-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+
   | Admi  | (     | N     | Y     | X     |       |       |       |       |       |       |       |       |       |       |
   | ssion | 0038, |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | ID    | 0010) |       |       |       |       |       |       |       |       |       |       |       |       |       |
   +-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+
   | Admi  | (     | N     | N     | X     |       |       |       |       |       | K     | C     |       |       |       |
   | tting | 0038, |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | Date  | 0020) |       |       |       |       |       |       |       |       |       |       |       |       |       |
   +-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+
   | Admi  | (     | N     | Y     | X     |       |       |       |       |       |       |       | C     |       |       |
   | tting | 0008, |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | Diag  | 1084) |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | noses |       |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | Code  |       |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | Seq   |       |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | uence |       |       |       |       |       |       |       |       |       |       |       |       |       |       |
   +-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+
   | Admi  | (     | N     | Y     | X     |       |       |       |       |       |       |       | C     |       |       |
   | tting | 0008, |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | Diag  | 1080) |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | noses |       |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | D     |       |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | escri |       |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | ption |       |       |       |       |       |       |       |       |       |       |       |       |       |       |
   +-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+
   | Admi  | (     | N     | N     | X     |       |       |       |       |       | K     | C     |       |       |       |
   | tting | 0038, |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | Time  | 0021) |       |       |       |       |       |       |       |       |       |       |       |       |       |
   +-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+
   | Aff   | (     | N     | N     | X     |       | K     |       |       |       |       |       |       |       |       |
   | ected | 0000, |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | SOP   | 1000) |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | Ins   |       |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | tance |       |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | UID   |       |       |       |       |       |       |       |       |       |       |       |       |       |       |
   +-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+
   | Alle  | (     | N     | N     | X     |       |       |       |       | C     |       |       | C     |       |       |
   | rgies | 0010, |       |       |       |       |       |       |       |       |       |       |       |       |       |
   |       | 2110) |       |       |       |       |       |       |       |       |       |       |       |       |       |
   +-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+
   | Arbi  | (     | Y     | N     | X     |       |       |       |       |       |       |       |       |       |       |
   | trary | 4000, |       |       |       |       |       |       |       |       |       |       |       |       |       |
   |       | 0010) |       |       |       |       |       |       |       |       |       |       |       |       |       |
   +-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+
   | A     | (     | N     | Y     | X     |       |       |       |       |       |       |       |       |       |       |
   | uthor | 0040, |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | Obs   | A078) |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | erver |       |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | Seq   |       |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | uence |       |       |       |       |       |       |       |       |       |       |       |       |       |       |
   +-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+
   | Ba    | (     | N     | Y     | X/Z   |       |       |       |       |       |       |       |       |       |       |
   | rcode | 2200, |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | Value | 0005) |       |       |       |       |       |       |       |       |       |       |       |       |       |
   +-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+
   | Beam  | (     | N     | Y     | X     |       |       |       |       |       |       |       | C     |       |       |
   | D     | 300A, |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | escri | 00C3) |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | ption |       |       |       |       |       |       |       |       |       |       |       |       |       |       |
   +-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+
   | Bolus | (     | N     | Y     | X     |       |       |       |       |       |       |       | C     |       |       |
   | D     | 300A, |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | escri | 00DD) |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | ption |       |       |       |       |       |       |       |       |       |       |       |       |       |       |
   +-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+
   | B     | (     | N     | N     | X     |       |       |       |       |       |       |       |       |       |       |
   | ranch | 0010, |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | of    | 1081) |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | Se    |       |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | rvice |       |       |       |       |       |       |       |       |       |       |       |       |       |       |
   +-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+
   | C     | (     | N     | Y     | X     |       |       |       |       |       |       |       |       |       |       |
   | amera | 0016, |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | Owner | 004D) |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | Name  |       |       |       |       |       |       |       |       |       |       |       |       |       |       |
   +-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+
   | Cas   | (     | N     | Y     | X     |       |       | K     |       |       |       |       |       |       |       |
   | sette | 0018, |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | ID    | 1007) |       |       |       |       |       |       |       |       |       |       |       |       |       |
   +-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+
   | Cli   | (     | N     | Y     | Z     |       |       |       | K     |       |       |       |       |       |       |
   | nical | 0012, |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | Trial | 0060) |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | Co    |       |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | ordin |       |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | ating |       |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | C     |       |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | enter |       |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | Name  |       |       |       |       |       |       |       |       |       |       |       |       |       |       |
   +-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+
   | Cli   | (     | N     | Y     | X     |       |       |       |       |       |       |       |       |       |       |
   | nical | 0012, |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | Trial | 0082) |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | Pro   |       |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | tocol |       |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | E     |       |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | thics |       |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | Comm  |       |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | ittee |       |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | App   |       |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | roval |       |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | N     |       |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | umber |       |       |       |       |       |       |       |       |       |       |       |       |       |       |
   +-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+
   | Cli   | (     | N     | Y     | D     |       |       |       | K     |       |       |       |       |       |       |
   | nical | 0012, |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | Trial | 0081) |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | Pro   |       |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | tocol |       |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | E     |       |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | thics |       |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | Comm  |       |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | ittee |       |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | Name  |       |       |       |       |       |       |       |       |       |       |       |       |       |       |
   +-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+
   | Cli   | (     | N     | Y     | D     |       |       |       |       |       |       |       |       |       |       |
   | nical | 0012, |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | Trial | 0020) |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | Pro   |       |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | tocol |       |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | ID    |       |       |       |       |       |       |       |       |       |       |       |       |       |       |
   +-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+
   | Cli   | (     | N     | Y     | Z     |       |       |       |       |       |       |       |       |       |       |
   | nical | 0012, |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | Trial | 0021) |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | Pro   |       |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | tocol |       |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | Name  |       |       |       |       |       |       |       |       |       |       |       |       |       |       |
   +-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+
   | Cli   | (     | N     | Y     | X     |       |       |       |       |       |       |       | C     |       |       |
   | nical | 0012, |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | Trial | 0072) |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | S     |       |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | eries |       |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | D     |       |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | escri |       |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | ption |       |       |       |       |       |       |       |       |       |       |       |       |       |       |
   +-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+
   | Cli   | (     | N     | Y     | X     |       |       |       |       |       |       |       |       |       |       |
   | nical | 0012, |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | Trial | 0071) |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | S     |       |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | eries |       |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | ID    |       |       |       |       |       |       |       |       |       |       |       |       |       |       |
   +-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+
   | Cli   | (     | N     | Y     | Z     |       |       |       | K     |       |       |       |       |       |       |
   | nical | 0012, |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | Trial | 0030) |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | Site  |       |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | ID    |       |       |       |       |       |       |       |       |       |       |       |       |       |       |
   +-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+
   | Cli   | (     | N     | Y     | Z     |       |       |       | K     |       |       |       |       |       |       |
   | nical | 0012, |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | Trial | 0031) |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | Site  |       |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | Name  |       |       |       |       |       |       |       |       |       |       |       |       |       |       |
   +-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+
   | Cli   | (     | N     | Y     | D     |       |       |       |       |       |       |       |       |       |       |
   | nical | 0012, |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | Trial | 0010) |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | Sp    |       |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | onsor |       |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | Name  |       |       |       |       |       |       |       |       |       |       |       |       |       |       |
   +-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+
   | Cli   | (     | N     | Y     | D     |       |       |       |       |       |       |       |       |       |       |
   | nical | 0012, |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | Trial | 0040) |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | Su    |       |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | bject |       |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | ID    |       |       |       |       |       |       |       |       |       |       |       |       |       |       |
   +-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+
   | Cli   | (     | N     | Y     | D     |       |       |       |       |       |       |       |       |       |       |
   | nical | 0012, |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | Trial | 0042) |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | Su    |       |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | bject |       |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | Re    |       |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | ading |       |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | ID    |       |       |       |       |       |       |       |       |       |       |       |       |       |       |
   +-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+
   | Cli   | (     | N     | Y     | X     |       |       |       |       |       |       |       | C     |       |       |
   | nical | 0012, |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | Trial | 0051) |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | Time  |       |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | Point |       |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | D     |       |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | escri |       |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | ption |       |       |       |       |       |       |       |       |       |       |       |       |       |       |
   +-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+
   | Cli   | (     | N     | Y     | Z     |       |       |       |       |       |       |       |       |       |       |
   | nical | 0012, |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | Trial | 0050) |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | Time  |       |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | Point |       |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | ID    |       |       |       |       |       |       |       |       |       |       |       |       |       |       |
   +-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+
   | Com   | (     | N     | Y     | X     |       |       |       |       |       |       |       | C     |       |       |
   | ments | 0040, |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | on    | 0280) |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | the   |       |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | Perf  |       |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | ormed |       |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | Proc  |       |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | edure |       |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | Step  |       |       |       |       |       |       |       |       |       |       |       |       |       |       |
   +-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+
   | C     | (     | N     | Y     | X     |       |       |       |       |       |       |       | C     |       |       |
   | ompen | 300A, |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | sator | 02EB) |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | D     |       |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | escri |       |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | ption |       |       |       |       |       |       |       |       |       |       |       |       |       |       |
   +-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+
   | Con   | (     | N     | Y     | U     |       | K     |       |       |       |       |       |       |       |       |
   | caten | 0020, |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | ation | 9161) |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | UID   |       |       |       |       |       |       |       |       |       |       |       |       |       |       |
   +-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+
   | Conce | (     | N     | Y     | Z     |       |       |       |       |       |       |       | C     |       |       |
   | ptual | 3010, |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | V     | 000F) |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | olume |       |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | C     |       |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | ombin |       |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | ation |       |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | D     |       |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | escri |       |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | ption |       |       |       |       |       |       |       |       |       |       |       |       |       |       |
   +-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+
   | Conce | (     | N     | Y     | Z     |       |       |       |       |       |       |       | C     |       |       |
   | ptual | 3010, |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | V     | 0017) |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | olume |       |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | D     |       |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | escri |       |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | ption |       |       |       |       |       |       |       |       |       |       |       |       |       |       |
   +-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+
   | Conce | (     | N     | Y     | U     |       | K     |       |       |       |       |       |       |       |       |
   | ptual | 3010, |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | V     | 0006) |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | olume |       |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | UID   |       |       |       |       |       |       |       |       |       |       |       |       |       |       |
   +-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+
   | Confi | (     | N     | N     | X     |       |       |       |       |       |       |       |       |       |       |
   | denti | 0040, |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | ality | 3001) |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | Const |       |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | raint |       |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | on    |       |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | Pa    |       |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | tient |       |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | Data  |       |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | D     |       |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | escri |       |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | ption |       |       |       |       |       |       |       |       |       |       |       |       |       |       |
   +-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+
   | C     | (     | N     | Y     | U     |       | K     |       |       |       |       |       |       |       |       |
   | onsti | 3010, |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | tuent | 0013) |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | Conce |       |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | ptual |       |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | V     |       |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | olume |       |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | UID   |       |       |       |       |       |       |       |       |       |       |       |       |       |       |
   +-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+
   | Consu | (     | N     | Y     | Z     |       |       |       |       |       |       |       |       |       |       |
   | lting | 0008, |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | P     | 009C) |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | hysic |       |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | ian's |       |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | Name  |       |       |       |       |       |       |       |       |       |       |       |       |       |       |
   +-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+
   | Consu | (     | N     | Y     | X     |       |       |       |       |       |       |       |       |       |       |
   | lting | 0008, |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | Phys  | 009D) |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | ician |       |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | Iden  |       |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | tific |       |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | ation |       |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | Seq   |       |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | uence |       |       |       |       |       |       |       |       |       |       |       |       |       |       |
   +-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+
   | Cont  | (     | N     | Y     | X     |       |       |       |       |       |       |       |       |       |       |
   | ainer | 0050, |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | Comp  | 001B) |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | onent |       |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | ID    |       |       |       |       |       |       |       |       |       |       |       |       |       |       |
   +-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+
   | Cont  | (     | N     | Y     | X     |       |       |       |       |       |       |       | C     |       |       |
   | ainer | 0040, |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | D     | 051A) |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | escri |       |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | ption |       |       |       |       |       |       |       |       |       |       |       |       |       |       |
   +-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+
   | Cont  | (     | N     | Y     | D     |       |       |       |       |       |       |       |       |       |       |
   | ainer | 0040, |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | Ident | 0512) |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | ifier |       |       |       |       |       |       |       |       |       |       |       |       |       |       |
   +-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+
   | Co    | (     | N     | Y     | X     |       |       |       |       |       |       |       |       |       |       |
   | ntent | 0070, |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | Crea  | 0086) |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | tor's |       |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | Iden  |       |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | tific |       |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | ation |       |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | Code  |       |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | Seq   |       |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | uence |       |       |       |       |       |       |       |       |       |       |       |       |       |       |
   +-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+
   | Co    | (     | N     | Y     | Z/D   |       |       |       |       |       |       |       |       |       |       |
   | ntent | 0070, |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | Crea  | 0084) |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | tor's |       |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | Name  |       |       |       |       |       |       |       |       |       |       |       |       |       |       |
   +-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+
   | Co    | (     | N     | Y     | Z/D   |       |       |       |       |       | K     | C     |       |       |       |
   | ntent | 0008, |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | Date  | 0023) |       |       |       |       |       |       |       |       |       |       |       |       |       |
   +-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+
   | Co    | (     | N     | Y     | D     |       |       |       |       |       |       |       |       | C     |       |
   | ntent | 0040, |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | Seq   | A730) |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | uence |       |       |       |       |       |       |       |       |       |       |       |       |       |       |
   +-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+
   | Co    | (     | N     | Y     | Z/D   |       |       |       |       |       | K     | C     |       |       |       |
   | ntent | 0008, |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | Time  | 0033) |       |       |       |       |       |       |       |       |       |       |       |       |       |
   +-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+
   | Cont  | (     | N     | Y     | Z/D   |       |       |       |       |       |       |       | C     |       |       |
   | rast/ | 0018, |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | Bolus | 0010) |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | Agent |       |       |       |       |       |       |       |       |       |       |       |       |       |       |
   +-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+
   | Co    | (     | N     | Y     | X     |       |       |       |       |       |       |       | C     |       |       |
   | ntrib | 0018, |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | ution | A003) |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | D     |       |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | escri |       |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | ption |       |       |       |       |       |       |       |       |       |       |       |       |       |       |
   +-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+
   | Co    | (     | N     | N     | X     |       |       |       |       |       |       |       |       |       |       |
   | untry | 0010, |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | of    | 2150) |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | Resi  |       |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | dence |       |       |       |       |       |       |       |       |       |       |       |       |       |       |
   +-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+
   | Cu    | (     | Y     | N     | X     |       |       |       |       |       |       |       |       |       |       |
   | rrent | 0040, |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | Obs   | A307) |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | erver |       |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | (T    |       |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | rial) |       |       |       |       |       |       |       |       |       |       |       |       |       |       |
   +-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+
   | Cu    | (     | N     | N     | X     |       |       |       |       |       |       |       |       |       |       |
   | rrent | 0038, |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | Pa    | 0300) |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | tient |       |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | Loc   |       |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | ation |       |       |       |       |       |       |       |       |       |       |       |       |       |       |
   +-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+
   | Curve | (     | Y     | N     | X     |       |       |       |       |       |       |       |       |       | C     |
   | Data  | 50xx, |       |       |       |       |       |       |       |       |       |       |       |       |       |
   |       | xxxx) |       |       |       |       |       |       |       |       |       |       |       |       |       |
   +-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+
   | Curve | (     | Y     | Y     | X     |       |       |       |       |       | K     | C     |       |       |       |
   | Date  | 0008, |       |       |       |       |       |       |       |       |       |       |       |       |       |
   |       | 0025) |       |       |       |       |       |       |       |       |       |       |       |       |       |
   +-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+
   | Curve | (     | Y     | Y     | X     |       |       |       |       |       | K     | C     |       |       |       |
   | Time  | 0008, |       |       |       |       |       |       |       |       |       |       |       |       |       |
   |       | 0035) |       |       |       |       |       |       |       |       |       |       |       |       |       |
   +-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+
   | Cust  | (     | N     | Y     | X     |       |       |       |       |       |       |       |       |       |       |
   | odial | 0040, |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | Or    | A07C) |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | ganiz |       |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | ation |       |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | Seq   |       |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | uence |       |       |       |       |       |       |       |       |       |       |       |       |       |       |
   +-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+
   | Data  | (     | N     | Y     | X     |       |       |       |       |       |       |       |       |       |       |
   | Set   | FFFC, |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | Tra   | FFFC) |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | iling |       |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | Pa    |       |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | dding |       |       |       |       |       |       |       |       |       |       |       |       |       |       |
   +-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+
   | Dec   | (     | N     | Y     | X     |       |       |       |       |       |       |       | C     |       |       |
   | ompos | 0018, |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | ition | 937F) |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | D     |       |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | escri |       |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | ption |       |       |       |       |       |       |       |       |       |       |       |       |       |       |
   +-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+
   | Deriv | (     | N     | Y     | X     |       |       |       |       |       |       |       | C     |       |       |
   | ation | 0008, |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | D     | 2111) |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | escri |       |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | ption |       |       |       |       |       |       |       |       |       |       |       |       |       |       |
   +-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+
   | Det   | (     | N     | Y     | X/D   |       |       | K     |       |       |       |       |       |       |       |
   | ector | 0018, |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | ID    | 700A) |       |       |       |       |       |       |       |       |       |       |       |       |       |
   +-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+
   | D     | (     | N     | Y     | Z     |       |       |       |       |       |       |       |       |       |       |
   | evice | 3010, |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | Alte  | 001B) |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | rnate |       |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | Ident |       |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | ifier |       |       |       |       |       |       |       |       |       |       |       |       |       |       |
   +-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+
   | D     | (     | N     | Y     | X     |       |       | K     |       |       |       |       |       |       |       |
   | evice | 0050, |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | D     | 0020) |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | escri |       |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | ption |       |       |       |       |       |       |       |       |       |       |       |       |       |       |
   +-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+
   | D     | (     | N     | Y     | D     |       |       | K     |       |       |       |       |       |       |       |
   | evice | 3010, |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | Label | 002D) |       |       |       |       |       |       |       |       |       |       |       |       |       |
   +-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+
   | D     | (     | N     | Y     | X/Z/D |       |       | K     |       |       |       |       |       |       |       |
   | evice | 0018, |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | S     | 1000) |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | erial |       |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | N     |       |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | umber |       |       |       |       |       |       |       |       |       |       |       |       |       |       |
   +-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+
   | D     | (     | N     | Y     | X     |       |       |       |       |       |       |       | C     |       |       |
   | evice | 0016, |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | Se    | 004B) |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | tting |       |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | D     |       |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | escri |       |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | ption |       |       |       |       |       |       |       |       |       |       |       |       |       |       |
   +-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+
   | D     | (     | N     | Y     | U     |       | K     | K     |       |       |       |       |       |       |       |
   | evice | 0018, |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | UID   | 1002) |       |       |       |       |       |       |       |       |       |       |       |       |       |
   +-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+
   | Di    | (     | N     | Y     | X     |       |       |       |       |       |       |       |       |       |       |
   | gital | FFFA, |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | Signa | FFFA) |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | tures |       |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | Seq   |       |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | uence |       |       |       |       |       |       |       |       |       |       |       |       |       |       |
   +-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+
   | Di    | (     | N     | Y     | U     |       |       |       |       |       |       |       |       |       |       |
   | gital | 0400, |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | Sign  | 0100) |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | ature |       |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | UID   |       |       |       |       |       |       |       |       |       |       |       |       |       |       |
   +-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+
   | Dime  | (     | N     | Y     | U     |       | K     |       |       |       |       |       |       |       |       |
   | nsion | 0020, |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | Or    | 9164) |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | ganiz |       |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | ation |       |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | UID   |       |       |       |       |       |       |       |       |       |       |       |       |       |       |
   +-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+
   | Disc  | (     | Y     | N     | X     |       |       |       |       |       |       |       | C     |       |       |
   | harge | 0038, |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | Diag  | 0040) |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | nosis |       |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | D     |       |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | escri |       |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | ption |       |       |       |       |       |       |       |       |       |       |       |       |       |       |
   +-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+
   | Di    | (     | Y     | N     | X     |       |       |       |       |       |       |       |       |       |       |
   | strib | 4008, |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | ution | 011A) |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | Ad    |       |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | dress |       |       |       |       |       |       |       |       |       |       |       |       |       |       |
   +-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+
   | Di    | (     | Y     | N     | X     |       |       |       |       |       |       |       |       |       |       |
   | strib | 4008, |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | ution | 0119) |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | Name  |       |       |       |       |       |       |       |       |       |       |       |       |       |       |
   +-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+
   | Dose  | (     | N     | Y     | X     |       |       |       |       |       |       |       | C     |       |       |
   | Refe  | 300A, |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | rence | 0016) |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | D     |       |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | escri |       |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | ption |       |       |       |       |       |       |       |       |       |       |       |       |       |       |
   +-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+
   | Dose  | (     | N     | Y     | U     |       | K     |       |       |       |       |       |       |       |       |
   | Refe  | 300A, |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | rence | 0013) |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | UID   |       |       |       |       |       |       |       |       |       |       |       |       |       |       |
   +-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+
   | Dosim | (     | N     | Y     | U     |       | K     |       |       |       |       |       |       |       |       |
   | etric | 3010, |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | Obje  | 006E) |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | ctive |       |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | UID   |       |       |       |       |       |       |       |       |       |       |       |       |       |       |
   +-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+
   | End   | (     | N     | Y     | X/D   |       |       |       |       |       | K     | C     |       |       |       |
   | A     | 0018, |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | cquis | 9517) |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | ition |       |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | Dat   |       |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | eTime |       |       |       |       |       |       |       |       |       |       |       |       |       |       |
   +-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+
   | E     | (     | N     | Y     | X     |       |       |       |       |       |       |       | C     |       |       |
   | ntity | 3010, |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | D     | 0037) |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | escri |       |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | ption |       |       |       |       |       |       |       |       |       |       |       |       |       |       |
   +-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+
   | E     | (     | N     | Y     | D     |       |       |       |       |       |       |       | C     |       |       |
   | ntity | 3010, |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | Label | 0035) |       |       |       |       |       |       |       |       |       |       |       |       |       |
   +-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+
   | E     | (     | N     | Y     | D     |       |       |       |       |       |       |       | C     |       |       |
   | ntity | 3010, |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | Long  | 0038) |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | Label |       |       |       |       |       |       |       |       |       |       |       |       |       |       |
   +-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+
   | E     | (     | N     | Y     | X     |       |       |       |       |       |       |       | C     |       |       |
   | ntity | 3010, |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | Name  | 0036) |       |       |       |       |       |       |       |       |       |       |       |       |       |
   +-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+
   | Equi  | (     | N     | Y     | X     |       |       |       |       |       |       |       | C     |       |       |
   | pment | 300A, |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | Frame | 0676) |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | of    |       |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | Refe  |       |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | rence |       |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | D     |       |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | escri |       |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | ption |       |       |       |       |       |       |       |       |       |       |       |       |       |       |
   +-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+
   | E     | (     | N     | Y     | X     |       |       |       |       | K     |       |       |       |       |       |
   | thnic | 0010, |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | Group | 2160) |       |       |       |       |       |       |       |       |       |       |       |       |       |
   +-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+
   | Exp   | (     | N     | N     | X     |       |       |       |       |       | K     | C     |       |       |       |
   | ected | 0040, |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | Compl | 4011) |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | etion |       |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | Dat   |       |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | eTime |       |       |       |       |       |       |       |       |       |       |       |       |       |       |
   +-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+
   | F     | (     | N     | N     | U     |       | K     |       |       |       |       |       |       |       |       |
   | ailed | 0008, |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | SOP   | 0058) |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | Ins   |       |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | tance |       |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | UID   |       |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | List  |       |       |       |       |       |       |       |       |       |       |       |       |       |       |
   +-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+
   | Fid   | (     | N     | Y     | U     |       | K     |       |       |       |       |       |       |       |       |
   | ucial | 0070, |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | UID   | 031A) |       |       |       |       |       |       |       |       |       |       |       |       |       |
   +-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+
   | F     | (     | N     | Y     | Z     |       |       |       |       |       |       |       |       |       |       |
   | iller | 0040, |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | Order | 2017) |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | N     |       |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | umber |       |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | /     |       |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | Im    |       |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | aging |       |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | Se    |       |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | rvice |       |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | Re    |       |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | quest |       |       |       |       |       |       |       |       |       |       |       |       |       |       |
   +-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+
   | First | (     | N     | Y     | X/D   |       |       |       |       |       | K     | C     |       |       |       |
   | Trea  | 3008, |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | tment | 0054) |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | Date  |       |       |       |       |       |       |       |       |       |       |       |       |       |       |
   +-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+
   | Fix   | (     | N     | Y     | X     |       |       |       |       |       |       |       | C     |       |       |
   | ation | 300A, |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | D     | 0196) |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | evice |       |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | D     |       |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | escri |       |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | ption |       |       |       |       |       |       |       |       |       |       |       |       |       |       |
   +-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+
   | Flow  | (     | N     | Y     | D     |       |       |       |       |       |       |       |       |       |       |
   | Ident | 0034, |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | ifier | 0002) |       |       |       |       |       |       |       |       |       |       |       |       |       |
   +-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+
   | Flow  | (     | N     | Y     | D     |       |       |       |       |       |       |       |       |       |       |
   | Ident | 0034, |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | ifier | 0001) |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | Seq   |       |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | uence |       |       |       |       |       |       |       |       |       |       |       |       |       |       |
   +-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+
   | Fra   | (     | N     | Y     | Z     |       |       |       |       |       |       |       | C     |       |       |
   | ction | 3010, |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | ation | 007F) |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | Notes |       |       |       |       |       |       |       |       |       |       |       |       |       |       |
   +-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+
   | Fra   | (     | N     | Y     | X     |       |       |       |       |       |       |       | C     |       |       |
   | ction | 300A, |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | Group | 0072) |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | D     |       |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | escri |       |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | ption |       |       |       |       |       |       |       |       |       |       |       |       |       |       |
   +-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+
   | Frame | (     | N     | Y     | X     |       |       |       |       |       |       |       | C     |       |       |
   | Com   | 0020, |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | ments | 9158) |       |       |       |       |       |       |       |       |       |       |       |       |       |
   +-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+
   | Frame | (     | N     | Y     | U     |       | K     |       |       |       |       |       |       |       |       |
   | of    | 0020, |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | Refe  | 0052) |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | rence |       |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | UID   |       |       |       |       |       |       |       |       |       |       |       |       |       |       |
   +-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+
   | Frame | (     | N     | Y     | D     |       |       |       |       |       | K     | C     |       |       |       |
   | O     | 0034, |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | rigin | 0007) |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | Time  |       |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | stamp |       |       |       |       |       |       |       |       |       |       |       |       |       |       |
   +-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+
   | G     | (     | N     | Y     | X     |       |       | K     |       |       |       |       |       |       |       |
   | antry | 0018, |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | ID    | 1008) |       |       |       |       |       |       |       |       |       |       |       |       |       |
   +-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+
   | Gene  | (     | N     | Y     | X     |       |       | K     |       |       |       |       |       |       |       |
   | rator | 0018, |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | ID    | 1005) |       |       |       |       |       |       |       |       |       |       |       |       |       |
   +-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+
   | GPS   | (     | N     | Y     | X     |       |       |       |       |       |       |       |       |       |       |
   | Alti  | 0016, |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | tude​ | 0076) |       |       |       |       |       |       |       |       |       |       |       |       |       |
   +-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+
   | GPS   | (     | N     | Y     | X     |       |       |       |       |       |       |       |       |       |       |
   | Alti  | 0016, |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | tude​ | 0075) |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | Ref   |       |       |       |       |       |       |       |       |       |       |       |       |       |       |
   +-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+
   | GPS   | (     | N     | Y     | X     |       |       |       |       |       |       |       |       |       |       |
   | Area  | 0016, |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | ​I    | 008C) |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | nform |       |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | ation |       |       |       |       |       |       |       |       |       |       |       |       |       |       |
   +-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+
   | GPS   | (     | N     | Y     | X     |       |       |       |       |       | K     | C     |       |       |       |
   | Date​ | 0016, |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | Stamp | 008D) |       |       |       |       |       |       |       |       |       |       |       |       |       |
   +-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+
   | GPS   | (     | N     | Y     | X     |       |       |       |       |       |       |       |       |       |       |
   | Dest  | 0016, |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | ​Be   | 0088) |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | aring |       |       |       |       |       |       |       |       |       |       |       |       |       |       |
   +-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+
   | GPS   | (     | N     | Y     | X     |       |       |       |       |       |       |       |       |       |       |
   | Dest​ | 0016, |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | Be    | 0087) |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | aring |       |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | Ref   |       |       |       |       |       |       |       |       |       |       |       |       |       |       |
   +-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+
   | GPS   | (     | N     | Y     | X     |       |       |       |       |       |       |       |       |       |       |
   | Dest  | 0016, |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | ​Dis  | 008A) |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | tance |       |       |       |       |       |       |       |       |       |       |       |       |       |       |
   +-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+
   | GPS   | (     | N     | Y     | X     |       |       |       |       |       |       |       |       |       |       |
   | Dest  | 0016, |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | ​Dis  | 0089) |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | tance |       |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | Ref   |       |       |       |       |       |       |       |       |       |       |       |       |       |       |
   +-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+
   | GPS   | (     | N     | Y     | X     |       |       |       |       |       |       |       |       |       |       |
   | Dest​ | 0016, |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | Lat   | 0084) |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | itude |       |       |       |       |       |       |       |       |       |       |       |       |       |       |
   +-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+
   | GPS   | (     | N     | Y     | X     |       |       |       |       |       |       |       |       |       |       |
   | Dest​ | 0016, |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | Lat   | 0083) |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | itude |       |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | Ref   |       |       |       |       |       |       |       |       |       |       |       |       |       |       |
   +-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+
   | GPS   | (     | N     | Y     | X     |       |       |       |       |       |       |       |       |       |       |
   | Dest  | 0016, |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | ​Long | 0086) |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | itude |       |       |       |       |       |       |       |       |       |       |       |       |       |       |
   +-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+
   | GPS   | (     | N     | Y     | X     |       |       |       |       |       |       |       |       |       |       |
   | Dest  | 0016, |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | ​Long | 0085) |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | itude |       |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | Ref   |       |       |       |       |       |       |       |       |       |       |       |       |       |       |
   +-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+
   | GPS   | (     | N     | Y     | X     |       |       |       |       |       |       |       |       |       |       |
   | Di    | 0016, |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | ffere | 008E) |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | ntial |       |       |       |       |       |       |       |       |       |       |       |       |       |       |
   +-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+
   | GPS   | (     | N     | Y     | X     |       |       |       |       |       |       |       |       |       |       |
   | DOP   | 0016, |       |       |       |       |       |       |       |       |       |       |       |       |       |
   |       | 007B) |       |       |       |       |       |       |       |       |       |       |       |       |       |
   +-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+
   | GPS   | (     | N     | Y     | X     |       |       |       |       |       |       |       |       |       |       |
   | Img   | 0016, |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | ​Dire | 0081) |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | ction |       |       |       |       |       |       |       |       |       |       |       |       |       |       |
   +-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+
   | GPS   | (     | N     | Y     | X     |       |       |       |       |       |       |       |       |       |       |
   | Img​  | 0016, |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | Dire  | 0080) |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | ction |       |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | Ref   |       |       |       |       |       |       |       |       |       |       |       |       |       |       |
   +-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+
   | GPS   | (     | N     | Y     | X     |       |       |       |       |       |       |       |       |       |       |
   | Lati  | 0016, |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | tude​ | 0072) |       |       |       |       |       |       |       |       |       |       |       |       |       |
   +-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+
   | GPS   | (     | N     | Y     | X     |       |       |       |       |       |       |       |       |       |       |
   | Lati  | 0016, |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | tude​ | 0071) |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | Ref   |       |       |       |       |       |       |       |       |       |       |       |       |       |       |
   +-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+
   | GPS   | (     | N     | Y     | X     |       |       |       |       |       |       |       |       |       |       |
   | Long  | 0016, |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | itude | 0074) |       |       |       |       |       |       |       |       |       |       |       |       |       |
   +-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+
   | GPS   | (     | N     | Y     | X     |       |       |       |       |       |       |       |       |       |       |
   | Long  | 0016, |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | itude | 0073) |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | Ref   |       |       |       |       |       |       |       |       |       |       |       |       |       |       |
   +-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+
   | GPS   | (     | N     | Y     | X     |       |       |       |       |       |       |       |       |       |       |
   | Map​  | 0016, |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | Datum | 0082) |       |       |       |       |       |       |       |       |       |       |       |       |       |
   +-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+
   | GPS   | (     | N     | Y     | X     |       |       |       |       |       |       |       |       |       |       |
   | Me    | 0016, |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | asure | 007A) |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | ​Mode |       |       |       |       |       |       |       |       |       |       |       |       |       |       |
   +-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+
   | GPS   | (     | N     | Y     | X     |       |       |       |       |       |       |       |       |       |       |
   | P     | 0016, |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | roces | 008B) |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | sing​ |       |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | M     |       |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | ethod |       |       |       |       |       |       |       |       |       |       |       |       |       |       |
   +-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+
   | GPS   | (     | N     | Y     | X     |       |       |       |       |       |       |       |       |       |       |
   | Satel | 0016, |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | lites | 0078) |       |       |       |       |       |       |       |       |       |       |       |       |       |
   +-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+
   | GPS   | (     | N     | Y     | X     |       |       |       |       |       |       |       |       |       |       |
   | S     | 0016, |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | peed​ | 007D) |       |       |       |       |       |       |       |       |       |       |       |       |       |
   +-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+
   | GPS   | (     | N     | Y     | X     |       |       |       |       |       |       |       |       |       |       |
   | S     | 0016, |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | peed​ | 007C) |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | Ref   |       |       |       |       |       |       |       |       |       |       |       |       |       |       |
   +-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+
   | GPS   | (     | N     | Y     | X     |       |       |       |       |       |       |       |       |       |       |
   | S     | 0016, |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | tatus | 0079) |       |       |       |       |       |       |       |       |       |       |       |       |       |
   +-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+
   | GPS   | (     | N     | Y     | X     |       |       |       |       |       |       |       |       |       |       |
   | Time​ | 0016, |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | Stamp | 0077) |       |       |       |       |       |       |       |       |       |       |       |       |       |
   +-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+
   | GPS   | (     | N     | Y     | X     |       |       |       |       |       |       |       |       |       |       |
   | Track | 0016, |       |       |       |       |       |       |       |       |       |       |       |       |       |
   |       | 007F) |       |       |       |       |       |       |       |       |       |       |       |       |       |
   +-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+
   | GPS   | (     | N     | Y     | X     |       |       |       |       |       |       |       |       |       |       |
   | Track | 0016, |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | ​Ref  | 007E) |       |       |       |       |       |       |       |       |       |       |       |       |       |
   +-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+
   | GPS   | (     | N     | Y     | X     |       |       |       |       |       |       |       |       |       |       |
   | Ve    | 0016, |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | rsion | 0070) |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | ID    |       |       |       |       |       |       |       |       |       |       |       |       |       |       |
   +-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+
   | Gr    | (     | N     | Y     | D     |       |       |       |       |       |       |       |       |       | C     |
   | aphic | 0070, |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | Annot | 0001) |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | ation |       |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | Seq   |       |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | uence |       |       |       |       |       |       |       |       |       |       |       |       |       |       |
   +-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+
   | Human | (     | N     | N     | X     |       |       |       |       |       |       |       |       |       |       |
   | P     | 0040, |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | erfor | 4037) |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | mer's |       |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | Name  |       |       |       |       |       |       |       |       |       |       |       |       |       |       |
   +-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+
   | Human | (     | N     | N     | X     |       |       |       |       |       |       |       |       |       |       |
   | P     | 0040, |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | erfor | 4036) |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | mer's |       |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | Or    |       |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | ganiz |       |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | ation |       |       |       |       |       |       |       |       |       |       |       |       |       |       |
   +-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+
   | Icon  | (     | N     | Y     | X     |       |       |       |       |       |       |       |       |       |       |
   | Image | 0088, |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | Seq   | 0200) |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | uence |       |       |       |       |       |       |       |       |       |       |       |       |       |       |
   |       |       |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | (see  |       |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | Note  |       |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | 12)   |       |       |       |       |       |       |       |       |       |       |       |       |       |       |
   +-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+
   | I     | (     | Y     | N     | X     |       |       |       |       |       |       |       | C     |       |       |
   | denti | 0008, |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | fying | 4000) |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | Com   |       |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | ments |       |       |       |       |       |       |       |       |       |       |       |       |       |       |
   +-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+
   | Image | (     | N     | Y     | X     |       |       |       |       |       |       |       | C     |       |       |
   | Com   | 0020, |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | ments | 4000) |       |       |       |       |       |       |       |       |       |       |       |       |       |
   +-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+
   | Image | (     | Y     | N     | X     |       |       |       |       |       |       |       |       |       |       |
   | Pr    | 0028, |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | esent | 4000) |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | ation |       |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | Com   |       |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | ments |       |       |       |       |       |       |       |       |       |       |       |       |       |       |
   +-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+
   | Im    | (     | N     | N     | X     |       |       |       |       |       |       |       | C     |       |       |
   | aging | 0040, |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | Se    | 2400) |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | rvice |       |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | Re    |       |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | quest |       |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | Com   |       |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | ments |       |       |       |       |       |       |       |       |       |       |       |       |       |       |
   +-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+
   | Impe  | (     | N     | Y     | D     |       |       |       |       |       | K     | C     |       |       |       |
   | dance | 003A, |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | M     | 0314) |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | easur |       |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | ement |       |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | Dat   |       |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | eTime |       |       |       |       |       |       |       |       |       |       |       |       |       |       |
   +-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+
   | I     | (     | Y     | N     | X     |       |       |       |       |       |       |       | C     |       |       |
   | mpres | 4008, |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | sions | 0300) |       |       |       |       |       |       |       |       |       |       |       |       |       |
   +-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+
   | Ins   | (     | N     | Y     | X     |       |       |       |       |       | K     | C     |       |       |       |
   | tance | 0008, |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | Coe   | 0015) |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | rcion |       |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | Dat   |       |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | eTime |       |       |       |       |       |       |       |       |       |       |       |       |       |       |
   +-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+
   | Ins   | (     | N     | Y     | U     |       | K     |       |       |       |       |       |       |       |       |
   | tance | 0008, |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | Cr    | 0014) |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | eator |       |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | UID   |       |       |       |       |       |       |       |       |       |       |       |       |       |       |
   +-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+
   | Ins   | (     | N     | Y     | X     |       |       |       |       |       |       |       |       |       |       |
   | tance | 0400, |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | O     | 0600) |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | rigin |       |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | S     |       |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | tatus |       |       |       |       |       |       |       |       |       |       |       |       |       |       |
   +-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+
   | I     | (     | N     | Y     | X     |       |       |       | K     |       |       |       |       |       |       |
   | nstit | 0008, |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | ution | 0081) |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | Ad    |       |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | dress |       |       |       |       |       |       |       |       |       |       |       |       |       |       |
   +-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+
   | Ins   | (     | N     | Y     | X     |       |       |       | K     |       |       |       |       |       |       |
   | titut | 0008, |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | ional | 1040) |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | Depar |       |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | tment |       |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | Name  |       |       |       |       |       |       |       |       |       |       |       |       |       |       |
   +-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+
   | Ins   | (     | N     | Y     | X     |       |       |       | K     |       |       |       |       |       |       |
   | titut | 0008, |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | ional | 1041) |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | Depar |       |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | tment |       |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | Type  |       |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | Code  |       |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | Seq   |       |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | uence |       |       |       |       |       |       |       |       |       |       |       |       |       |       |
   +-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+
   | I     | (     | N     | Y     | X/Z/D |       |       |       | K     |       |       |       |       |       |       |
   | nstit | 0008, |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | ution | 0082) |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | Code  |       |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | Seq   |       |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | uence |       |       |       |       |       |       |       |       |       |       |       |       |       |       |
   +-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+
   | I     | (     | N     | Y     | X/Z/D |       |       |       | K     |       |       |       |       |       |       |
   | nstit | 0008, |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | ution | 0080) |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | Name  |       |       |       |       |       |       |       |       |       |       |       |       |       |       |
   +-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+
   | Insu  | (     | Y     | N     | X     |       |       |       |       |       |       |       |       |       |       |
   | rance | 0010, |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | Plan  | 1050) |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | Iden  |       |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | tific |       |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | ation |       |       |       |       |       |       |       |       |       |       |       |       |       |       |
   +-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+
   | Int   | (     | N     | Y     | X/D   |       |       |       |       |       | K     | C     |       |       |       |
   | ended | 3010, |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | Phase | 004D) |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | End   |       |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | Date  |       |       |       |       |       |       |       |       |       |       |       |       |       |       |
   +-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+
   | Int   | (     | N     | Y     | X/D   |       |       |       |       |       | K     | C     |       |       |       |
   | ended | 3010, |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | Phase | 004C) |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | Start |       |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | Date  |       |       |       |       |       |       |       |       |       |       |       |       |       |       |
   +-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+
   | Int   | (     | N     | N     | X     |       |       |       |       |       |       |       |       |       |       |
   | ended | 0040, |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | Recip | 1011) |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | ients |       |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | of    |       |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | Re    |       |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | sults |       |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | Iden  |       |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | tific |       |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | ation |       |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | Seq   |       |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | uence |       |       |       |       |       |       |       |       |       |       |       |       |       |       |
   +-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+
   | Inte  | (     | N     | Y     | D     |       |       |       |       |       | K     | C     |       |       |       |
   | rlock | 300A, |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | Dat   | 0741) |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | eTime |       |       |       |       |       |       |       |       |       |       |       |       |       |       |
   +-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+
   | Inte  | (     | N     | Y     | D     |       |       |       |       |       |       |       | C     |       |       |
   | rlock | 300A, |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | D     | 0742) |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | escri |       |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | ption |       |       |       |       |       |       |       |       |       |       |       |       |       |       |
   +-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+
   | Inte  | (     | N     | Y     | D     |       |       |       |       |       |       |       | C     |       |       |
   | rlock | 300A, |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | O     | 0783) |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | rigin |       |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | D     |       |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | escri |       |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | ption |       |       |       |       |       |       |       |       |       |       |       |       |       |       |
   +-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+
   | Inte  | (     | Y     | N     | X     |       |       |       |       |       |       |       |       |       |       |
   | rpret | 4008, |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | ation | 0111) |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | App   |       |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | rover |       |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | Seq   |       |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | uence |       |       |       |       |       |       |       |       |       |       |       |       |       |       |
   +-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+
   | Inte  | (     | Y     | N     | X     |       |       |       |       |       |       |       |       |       |       |
   | rpret | 4008, |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | ation | 010C) |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | A     |       |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | uthor |       |       |       |       |       |       |       |       |       |       |       |       |       |       |
   +-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+
   | Inte  | (     | Y     | N     | X     |       |       |       |       |       |       |       | C     |       |       |
   | rpret | 4008, |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | ation | 0115) |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | Diag  |       |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | nosis |       |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | D     |       |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | escri |       |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | ption |       |       |       |       |       |       |       |       |       |       |       |       |       |       |
   +-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+
   | Inte  | (     | Y     | N     | X     |       |       |       |       |       |       |       |       |       |       |
   | rpret | 4008, |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | ation | 0202) |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | ID    |       |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | I     |       |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | ssuer |       |       |       |       |       |       |       |       |       |       |       |       |       |       |
   +-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+
   | Inte  | (     | Y     | N     | X     |       |       |       |       |       |       |       |       |       |       |
   | rpret | 4008, |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | ation | 0102) |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | Rec   |       |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | order |       |       |       |       |       |       |       |       |       |       |       |       |       |       |
   +-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+
   | Inte  | (     | Y     | N     | X     |       |       |       |       |       |       |       | C     |       |       |
   | rpret | 4008, |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | ation | 010B) |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | Text  |       |       |       |       |       |       |       |       |       |       |       |       |       |       |
   +-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+
   | Inte  | (     | Y     | N     | X     |       |       |       |       |       |       |       |       |       |       |
   | rpret | 4008, |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | ation | 010A) |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | T     |       |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | ransc |       |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | riber |       |       |       |       |       |       |       |       |       |       |       |       |       |       |
   +-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+
   | I     | (     | N     | Y     | U     |       | K     |       |       |       |       |       |       |       |       |
   | rradi | 0008, |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | ation | 3010) |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | Event |       |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | UID   |       |       |       |       |       |       |       |       |       |       |       |       |       |       |
   +-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+
   | I     | (     | Y     | Y     | X     |       |       |       |       |       |       |       |       |       |       |
   | ssuer | 0038, |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | of    | 0011) |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | Admi  |       |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | ssion |       |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | ID    |       |       |       |       |       |       |       |       |       |       |       |       |       |       |
   +-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+
   | I     | (     | N     | Y     | X     |       |       |       |       |       |       |       |       |       |       |
   | ssuer | 0038, |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | of    | 0014) |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | Admi  |       |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | ssion |       |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | ID    |       |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | Seq   |       |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | uence |       |       |       |       |       |       |       |       |       |       |       |       |       |       |
   +-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+
   | I     | (     | N     | Y     | X     |       |       |       |       |       |       |       |       |       |       |
   | ssuer | 0010, |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | of    | 0021) |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | Pa    |       |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | tient |       |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | ID    |       |       |       |       |       |       |       |       |       |       |       |       |       |       |
   +-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+
   | I     | (     | Y     | Y     | X     |       |       |       |       |       |       |       |       |       |       |
   | ssuer | 0038, |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | of    | 0061) |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | Se    |       |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | rvice |       |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | Ep    |       |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | isode |       |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | ID    |       |       |       |       |       |       |       |       |       |       |       |       |       |       |
   +-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+
   | I     | (     | N     | Y     | X     |       |       |       |       |       |       |       |       |       |       |
   | ssuer | 0038, |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | of    | 0064) |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | Se    |       |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | rvice |       |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | Ep    |       |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | isode |       |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | ID    |       |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | Seq   |       |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | uence |       |       |       |       |       |       |       |       |       |       |       |       |       |       |
   +-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+
   | I     | (     | N     | Y     | Z     |       |       |       |       |       |       |       |       |       |       |
   | ssuer | 0040, |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | of    | 0513) |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | the   |       |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | Cont  |       |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | ainer |       |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | Ident |       |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | ifier |       |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | Seq   |       |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | uence |       |       |       |       |       |       |       |       |       |       |       |       |       |       |
   +-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+
   | I     | (     | N     | Y     | Z     |       |       |       |       |       |       |       |       |       |       |
   | ssuer | 0040, |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | of    | 0562) |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | the   |       |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | Spe   |       |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | cimen |       |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | Ident |       |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | ifier |       |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | Seq   |       |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | uence |       |       |       |       |       |       |       |       |       |       |       |       |       |       |
   +-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+
   | Label | (     | N     | Y     | X/Z   |       |       |       |       |       |       |       | C     |       |       |
   | Text  | 2200, |       |       |       |       |       |       |       |       |       |       |       |       |       |
   |       | 0002) |       |       |       |       |       |       |       |       |       |       |       |       |       |
   +-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+
   | Large | (     | Y     | N     | U     |       | K     |       |       |       |       |       |       |       |       |
   | Pa    | 0028, |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | lette | 1214) |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | Color |       |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | L     |       |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | ookup |       |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | Table |       |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | UID   |       |       |       |       |       |       |       |       |       |       |       |       |       |       |
   +-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+
   | Last  | (     | N     | N     | X     |       |       |       |       |       | K     | C     |       |       |       |
   | Mens  | 0010, |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | trual | 21D0) |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | Date  |       |       |       |       |       |       |       |       |       |       |       |       |       |       |
   +-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+
   | Lens  | (     | N     | Y     | X     |       |       | K     |       |       |       |       |       |       |       |
   | Make  | 0016, |       |       |       |       |       |       |       |       |       |       |       |       |       |
   |       | 004F) |       |       |       |       |       |       |       |       |       |       |       |       |       |
   +-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+
   | Lens  | (     | N     | Y     | X     |       |       | K     |       |       |       |       |       |       |       |
   | Model | 0016, |       |       |       |       |       |       |       |       |       |       |       |       |       |
   |       | 0050) |       |       |       |       |       |       |       |       |       |       |       |       |       |
   +-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+
   | Lens  | (     | N     | Y     | X     |       |       | K     |       |       |       |       |       |       |       |
   | S     | 0016, |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | erial | 0051) |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | N     |       |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | umber |       |       |       |       |       |       |       |       |       |       |       |       |       |       |
   +-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+
   | Lens  | (     | N     | Y     | X     |       |       | K     |       |       |       |       |       |       |       |
   | Spe   | 0016, |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | cific | 004E) |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | ation |       |       |       |       |       |       |       |       |       |       |       |       |       |       |
   +-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+
   | Long  | (     | N     | Y     | X     |       |       |       |       |       |       |       | C     |       |       |
   | D     | 0050, |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | evice | 0021) |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | D     |       |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | escri |       |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | ption |       |       |       |       |       |       |       |       |       |       |       |       |       |       |
   +-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+
   | MAC   | (     | N     | Y     | X     |       |       |       |       |       |       |       |       |       |       |
   |       | 0400, |       |       |       |       |       |       |       |       |       |       |       |       |       |
   |       | 0404) |       |       |       |       |       |       |       |       |       |       |       |       |       |
   +-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+
   | Maker | (     | N     | Y     | X     |       |       |       |       |       |       |       | C     |       |       |
   | Note  | 0016, |       |       |       |       |       |       |       |       |       |       |       |       |       |
   |       | 002B) |       |       |       |       |       |       |       |       |       |       |       |       |       |
   +-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+
   | Manu  | (     | N     | Y     | U     |       | K     | K     |       |       |       |       |       |       |       |
   | factu | 0018, |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | rer's | 100B) |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | D     |       |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | evice |       |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | Class |       |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | UID   |       |       |       |       |       |       |       |       |       |       |       |       |       |       |
   +-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+
   | Manu  | (     | N     | Y     | Z     |       |       | K     |       |       |       |       |       |       |       |
   | factu | 3010, |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | rer's | 0043) |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | D     |       |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | evice |       |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | Ident |       |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | ifier |       |       |       |       |       |       |       |       |       |       |       |       |       |       |
   +-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+
   | Media | (     | N     | N     | U     |       | K     |       |       |       |       |       |       |       |       |
   | St    | 0002, |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | orage | 0003) |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | SOP   |       |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | Ins   |       |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | tance |       |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | UID   |       |       |       |       |       |       |       |       |       |       |       |       |       |       |
   +-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+
   | Me    | (     | N     | N     | X     |       |       |       |       |       |       |       | C     |       |       |
   | dical | 0010, |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | A     | 2000) |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | lerts |       |       |       |       |       |       |       |       |       |       |       |       |       |       |
   +-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+
   | Me    | (     | Y     | N     | X     |       |       |       |       |       |       |       |       |       |       |
   | dical | 0010, |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | R     | 1090) |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | ecord |       |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | Lo    |       |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | cator |       |       |       |       |       |       |       |       |       |       |       |       |       |       |
   +-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+
   | Mil   | (     | N     | N     | X     |       |       |       |       |       |       |       |       |       |       |
   | itary | 0010, |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | Rank  | 1080) |       |       |       |       |       |       |       |       |       |       |       |       |       |
   +-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+
   | Mod   | (     | N     | N     | X     |       |       |       |       |       |       |       |       |       |       |
   | ified | 0400, |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | Attri | 0550) |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | butes |       |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | Seq   |       |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | uence |       |       |       |       |       |       |       |       |       |       |       |       |       |       |
   +-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+
   | Mod   | (     | Y     | N     | X     |       |       |       |       |       |       |       |       |       |       |
   | ified | 0020, |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | Image | 3406) |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | D     |       |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | escri |       |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | ption |       |       |       |       |       |       |       |       |       |       |       |       |       |       |
   +-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+
   | Modi  | (     | Y     | N     | X     |       |       |       |       |       |       |       |       |       |       |
   | fying | 0020, |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | D     | 3401) |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | evice |       |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | ID    |       |       |       |       |       |       |       |       |       |       |       |       |       |       |
   +-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+
   | Most  | (     | N     | Y     | X/D   |       |       |       |       |       | K     | C     |       |       |       |
   | R     | 3008, |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | ecent | 0056) |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | Trea  |       |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | tment |       |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | Date  |       |       |       |       |       |       |       |       |       |       |       |       |       |       |
   +-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+
   | Mu    | (     | N     | Y     | X     |       |       |       |       |       |       |       | C     |       |       |
   | lti-e | 0018, |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | nergy | 937B) |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | A     |       |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | cquis |       |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | ition |       |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | D     |       |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | escri |       |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | ption |       |       |       |       |       |       |       |       |       |       |       |       |       |       |
   +-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+
   | Mult  | (     | N     | Y     | U     |       | K     |       |       |       |       |       |       |       |       |
   | iplex | 003A, |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | Group | 0310) |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | UID   |       |       |       |       |       |       |       |       |       |       |       |       |       |       |
   +-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+
   | Name  | (     | N     | Y     | X     |       |       |       |       |       |       |       |       |       |       |
   | of    | 0008, |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | Ph    | 1060) |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | ysici |       |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | an(s) |       |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | Re    |       |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | ading |       |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | Study |       |       |       |       |       |       |       |       |       |       |       |       |       |       |
   +-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+
   | Names | (     | N     | N     | X     |       |       |       |       |       |       |       |       |       |       |
   | of    | 0040, |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | Int   | 1010) |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | ended |       |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | Recip |       |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | ients |       |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | of    |       |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | Re    |       |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | sults |       |       |       |       |       |       |       |       |       |       |       |       |       |       |
   +-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+
   | O     | (     | Y     | N     | X     |       |       |       |       |       | K     | C     |       |       |       |
   | bserv | 0040, |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | ation | A192) |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | Date  |       |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | (T    |       |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | rial) |       |       |       |       |       |       |       |       |       |       |       |       |       |       |
   +-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+
   | O     | (     | Y     | N     | U     |       | K     |       |       |       |       |       |       |       |       |
   | bserv | 0040, |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | ation | A402) |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | Su    |       |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | bject |       |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | UID   |       |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | (T    |       |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | rial) |       |       |       |       |       |       |       |       |       |       |       |       |       |       |
   +-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+
   | O     | (     | Y     | N     | X     |       |       |       |       |       | K     | C     |       |       |       |
   | bserv | 0040, |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | ation | A193) |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | Time  |       |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | (T    |       |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | rial) |       |       |       |       |       |       |       |       |       |       |       |       |       |       |
   +-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+
   | O     | (     | N     | Y     | U     |       | K     |       |       |       |       |       |       |       |       |
   | bserv | 0040, |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | ation | A171) |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | UID   |       |       |       |       |       |       |       |       |       |       |       |       |       |       |
   +-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+
   | Occup | (     | N     | Y     | X     |       |       |       |       |       |       |       | C     |       |       |
   | ation | 0010, |       |       |       |       |       |       |       |       |       |       |       |       |       |
   |       | 2180) |       |       |       |       |       |       |       |       |       |       |       |       |       |
   +-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+
   | Ope   | (     | N     | Y     | X/D   |       |       |       |       |       |       |       |       |       |       |
   | rator | 0008, |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | Iden  | 1072) |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | tific |       |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | ation |       |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | Seq   |       |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | uence |       |       |       |       |       |       |       |       |       |       |       |       |       |       |
   +-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+
   | Opera | (     | N     | Y     | X/Z/D |       |       |       |       |       |       |       |       |       |       |
   | tors' | 0008, |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | Name  | 1070) |       |       |       |       |       |       |       |       |       |       |       |       |       |
   +-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+
   | Order | (     | N     | N     | X     |       |       |       |       |       |       |       |       |       |       |
   | Cal   | 0040, |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | lback | 2010) |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | Phone |       |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | N     |       |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | umber |       |       |       |       |       |       |       |       |       |       |       |       |       |       |
   +-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+
   | Order | (     | N     | N     | X     |       |       |       |       |       |       |       |       |       |       |
   | Cal   | 0040, |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | lback | 2011) |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | Te    |       |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | lecom |       |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | I     |       |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | nform |       |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | ation |       |       |       |       |       |       |       |       |       |       |       |       |       |       |
   +-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+
   | Order | (     | N     | N     | X     |       |       |       |       |       |       |       |       |       |       |
   | En    | 0040, |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | tered | 2008) |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | By    |       |       |       |       |       |       |       |       |       |       |       |       |       |       |
   +-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+
   | Order | (     | N     | N     | X     |       |       |       |       |       |       |       |       |       |       |
   | Ente  | 0040, |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | rer's | 2009) |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | Loc   |       |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | ation |       |       |       |       |       |       |       |       |       |       |       |       |       |       |
   +-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+
   | Ori   | (     | N     | Y     | X     |       |       |       |       |       |       |       |       |       |       |
   | ginal | 0400, |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | Attri | 0561) |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | butes |       |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | Seq   |       |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | uence |       |       |       |       |       |       |       |       |       |       |       |       |       |       |
   +-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+
   | Other | (     | Y     | Y     | X     |       |       |       |       |       |       |       |       |       |       |
   | Pa    | 0010, |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | tient | 1000) |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | IDs   |       |       |       |       |       |       |       |       |       |       |       |       |       |       |
   +-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+
   | Other | (     | N     | Y     | X     |       |       |       |       |       |       |       |       |       |       |
   | Pa    | 0010, |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | tient | 1002) |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | IDs   |       |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | Seq   |       |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | uence |       |       |       |       |       |       |       |       |       |       |       |       |       |       |
   +-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+
   | Other | (     | N     | Y     | X     |       |       |       |       |       |       |       |       |       |       |
   | Pa    | 0010, |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | tient | 1001) |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | Names |       |       |       |       |       |       |       |       |       |       |       |       |       |       |
   +-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+
   | Ov    | (     | Y     | N     | X     |       |       |       |       |       |       |       |       |       | C     |
   | erlay | 60xx, |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | Com   | 4000) |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | ments |       |       |       |       |       |       |       |       |       |       |       |       |       |       |
   +-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+
   | Ov    | (     | N     | Y     | X     |       |       |       |       |       |       |       |       |       | C     |
   | erlay | 60xx, |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | Data  | 3000) |       |       |       |       |       |       |       |       |       |       |       |       |       |
   +-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+
   | Ov    | (     | Y     | Y     | X     |       |       |       |       |       | K     | C     |       |       |       |
   | erlay | 0008, |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | Date  | 0024) |       |       |       |       |       |       |       |       |       |       |       |       |       |
   +-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+
   | Ov    | (     | Y     | Y     | X     |       |       |       |       |       | K     | C     |       |       |       |
   | erlay | 0008, |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | Time  | 0034) |       |       |       |       |       |       |       |       |       |       |       |       |       |
   +-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+
   | Ove   | (     | N     | Y     | D     |       |       |       |       |       | K     | C     |       |       |       |
   | rride | 300A, |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | Dat   | 0760) |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | eTime |       |       |       |       |       |       |       |       |       |       |       |       |       |       |
   +-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+
   | Pa    | (     | N     | Y     | U     |       | K     |       |       |       |       |       |       |       |       |
   | lette | 0028, |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | Color | 1199) |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | L     |       |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | ookup |       |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | Table |       |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | UID   |       |       |       |       |       |       |       |       |       |       |       |       |       |       |
   +-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+
   | P     | (     | N     | Y     | X     |       |       |       |       |       |       |       |       |       |       |
   | artic | 0040, |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | ipant | A07A) |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | Seq   |       |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | uence |       |       |       |       |       |       |       |       |       |       |       |       |       |       |
   +-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+
   | Pati  | (     | N     | N     | X     |       |       |       |       |       |       |       |       |       |       |
   | ent's | 0010, |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | Ad    | 1040) |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | dress |       |       |       |       |       |       |       |       |       |       |       |       |       |       |
   +-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+
   | Pati  | (     | N     | Y     | X     |       |       |       |       | K     |       |       |       |       |       |
   | ent's | 0010, |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | Age   | 1010) |       |       |       |       |       |       |       |       |       |       |       |       |       |
   +-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+
   | Pati  | (     | N     | Y     | Z     |       |       |       |       |       |       |       |       |       |       |
   | ent's | 0010, |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | Birth | 0030) |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | Date  |       |       |       |       |       |       |       |       |       |       |       |       |       |       |
   +-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+
   | Pati  | (     | N     | N     | X     |       |       |       |       |       |       |       |       |       |       |
   | ent's | 0010, |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | Birth | 1005) |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | Name  |       |       |       |       |       |       |       |       |       |       |       |       |       |       |
   +-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+
   | Pati  | (     | N     | Y     | X     |       |       |       |       |       |       |       |       |       |       |
   | ent's | 0010, |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | Birth | 0032) |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | Time  |       |       |       |       |       |       |       |       |       |       |       |       |       |       |
   +-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+
   | Pati  | (     | N     | N     | X     |       |       |       |       |       |       |       |       |       |       |
   | ent's | 0038, |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | I     | 0400) |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | nstit |       |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | ution |       |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | Resi  |       |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | dence |       |       |       |       |       |       |       |       |       |       |       |       |       |       |
   +-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+
   | Pati  | (     | N     | Y     | X     |       |       |       |       |       |       |       |       |       |       |
   | ent's | 0010, |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | Insu  | 0050) |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | rance |       |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | Plan  |       |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | Code  |       |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | Seq   |       |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | uence |       |       |       |       |       |       |       |       |       |       |       |       |       |       |
   +-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+
   | Pati  | (     | N     | N     | X     |       |       |       |       |       |       |       |       |       |       |
   | ent's | 0010, |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | Mot   | 1060) |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | her's |       |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | Birth |       |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | Name  |       |       |       |       |       |       |       |       |       |       |       |       |       |       |
   +-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+
   | Pati  | (     | N     | Y     | Z     |       |       |       |       |       |       |       |       |       |       |
   | ent's | 0010, |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | Name  | 0010) |       |       |       |       |       |       |       |       |       |       |       |       |       |
   +-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+
   | Pati  | (     | N     | Y     | X     |       |       |       |       |       |       |       |       |       |       |
   | ent's | 0010, |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | Pr    | 0101) |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | imary |       |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | Lan   |       |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | guage |       |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | Code  |       |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | Seq   |       |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | uence |       |       |       |       |       |       |       |       |       |       |       |       |       |       |
   +-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+
   | Pati  | (     | N     | Y     | X     |       |       |       |       |       |       |       |       |       |       |
   | ent's | 0010, |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | Pr    | 0102) |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | imary |       |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | Lan   |       |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | guage |       |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | Mod   |       |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | ifier |       |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | Code  |       |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | Seq   |       |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | uence |       |       |       |       |       |       |       |       |       |       |       |       |       |       |
   +-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+
   | Pati  | (     | N     | N     | X     |       |       |       |       |       |       |       |       |       |       |
   | ent's | 0010, |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | Reli  | 21F0) |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | gious |       |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | Prefe |       |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | rence |       |       |       |       |       |       |       |       |       |       |       |       |       |       |
   +-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+
   | Pati  | (     | N     | Y     | Z     |       |       |       |       | K     |       |       |       |       |       |
   | ent's | 0010, |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | Sex   | 0040) |       |       |       |       |       |       |       |       |       |       |       |       |       |
   +-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+
   | Pati  | (     | N     | Y     | X/Z   |       |       |       |       | K     |       |       |       |       |       |
   | ent's | 0010, |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | Sex   | 2203) |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | Neu   |       |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | tered |       |       |       |       |       |       |       |       |       |       |       |       |       |       |
   +-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+
   | Pati  | (     | N     | Y     | X     |       |       |       |       | K     |       |       |       |       |       |
   | ent's | 0010, |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | Size  | 1020) |       |       |       |       |       |       |       |       |       |       |       |       |       |
   +-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+
   | Pati  | (     | N     | N     | X     |       |       |       |       |       |       |       |       |       |       |
   | ent's | 0010, |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | Te    | 2155) |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | lecom |       |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | I     |       |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | nform |       |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | ation |       |       |       |       |       |       |       |       |       |       |       |       |       |       |
   +-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+
   | Pati  | (     | N     | N     | X     |       |       |       |       |       |       |       |       |       |       |
   | ent's | 0010, |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | Tele  | 2154) |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | phone |       |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | Nu    |       |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | mbers |       |       |       |       |       |       |       |       |       |       |       |       |       |       |
   +-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+
   | Pati  | (     | N     | Y     | X     |       |       |       |       | K     |       |       |       |       |       |
   | ent's | 0010, |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | W     | 1030) |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | eight |       |       |       |       |       |       |       |       |       |       |       |       |       |       |
   +-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+
   | Pa    | (     | N     | Y     | X     |       |       |       |       |       |       |       | C     |       |       |
   | tient | 0010, |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | Com   | 4000) |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | ments |       |       |       |       |       |       |       |       |       |       |       |       |       |       |
   +-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+
   | Pa    | (     | N     | Y     | Z     |       |       |       |       |       |       |       |       |       |       |
   | tient | 0010, |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | ID    | 0020) |       |       |       |       |       |       |       |       |       |       |       |       |       |
   +-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+
   | Pa    | (     | N     | Y     | U     |       | K     |       |       |       |       |       |       |       |       |
   | tient | 300A, |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | Setup | 0650) |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | UID   |       |       |       |       |       |       |       |       |       |       |       |       |       |       |
   +-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+
   | Pa    | (     | N     | N     | X     |       |       |       |       | C     |       |       | C     |       |       |
   | tient | 0038, |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | State | 0500) |       |       |       |       |       |       |       |       |       |       |       |       |       |
   +-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+
   | Pa    | (     | N     | N     | X     |       |       |       |       |       |       |       |       |       |       |
   | tient | 0040, |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | Tran  | 1004) |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | sport |       |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | Ar    |       |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | range |       |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | ments |       |       |       |       |       |       |       |       |       |       |       |       |       |       |
   +-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+
   | Perf  | (     | N     | N     | X     |       |       |       |       |       |       |       |       |       |       |
   | ormed | 0040, |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | Loc   | 0243) |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | ation |       |       |       |       |       |       |       |       |       |       |       |       |       |       |
   +-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+
   | Perf  | (     | N     | Y     | X     |       |       |       |       |       |       |       | C     |       |       |
   | ormed | 0040, |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | Proc  | 0254) |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | edure |       |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | Step  |       |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | D     |       |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | escri |       |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | ption |       |       |       |       |       |       |       |       |       |       |       |       |       |       |
   +-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+
   | Perf  | (     | N     | Y     | X     |       |       |       |       |       | K     | C     |       |       |       |
   | ormed | 0040, |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | Proc  | 0250) |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | edure |       |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | Step  |       |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | End   |       |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | Date  |       |       |       |       |       |       |       |       |       |       |       |       |       |       |
   +-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+
   | Perf  | (     | N     | N     | X     |       |       |       |       |       | K     | C     |       |       |       |
   | ormed | 0040, |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | Proc  | 4051) |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | edure |       |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | Step  |       |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | End   |       |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | Dat   |       |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | eTime |       |       |       |       |       |       |       |       |       |       |       |       |       |       |
   +-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+
   | Perf  | (     | N     | Y     | X     |       |       |       |       |       | K     | C     |       |       |       |
   | ormed | 0040, |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | Proc  | 0251) |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | edure |       |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | Step  |       |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | End   |       |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | Time  |       |       |       |       |       |       |       |       |       |       |       |       |       |       |
   +-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+
   | Perf  | (     | N     | Y     | X     |       |       |       |       |       |       |       |       |       |       |
   | ormed | 0040, |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | Proc  | 0253) |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | edure |       |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | Step  |       |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | ID    |       |       |       |       |       |       |       |       |       |       |       |       |       |       |
   +-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+
   | Perf  | (     | N     | Y     | X     |       |       |       |       |       | K     | C     |       |       |       |
   | ormed | 0040, |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | Proc  | 0244) |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | edure |       |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | Step  |       |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | Start |       |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | Date  |       |       |       |       |       |       |       |       |       |       |       |       |       |       |
   +-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+
   | Perf  | (     | N     | N     | X     |       |       |       |       |       | K     | C     |       |       |       |
   | ormed | 0040, |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | Proc  | 4050) |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | edure |       |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | Step  |       |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | Start |       |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | Dat   |       |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | eTime |       |       |       |       |       |       |       |       |       |       |       |       |       |       |
   +-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+
   | Perf  | (     | N     | Y     | X     |       |       |       |       |       | K     | C     |       |       |       |
   | ormed | 0040, |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | Proc  | 0245) |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | edure |       |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | Step  |       |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | Start |       |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | Time  |       |       |       |       |       |       |       |       |       |       |       |       |       |       |
   +-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+
   | Perf  | (     | N     | N     | X     |       |       | K     |       |       |       |       |       |       |       |
   | ormed | 0040, |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | St    | 0241) |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | ation |       |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | AE    |       |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | Title |       |       |       |       |       |       |       |       |       |       |       |       |       |       |
   +-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+
   | Perf  | (     | N     | N     | X     |       |       | K     |       |       |       |       |       |       |       |
   | ormed | 0040, |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | St    | 4030) |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | ation |       |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | Geogr |       |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | aphic |       |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | Loc   |       |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | ation |       |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | Code  |       |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | Seq   |       |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | uence |       |       |       |       |       |       |       |       |       |       |       |       |       |       |
   +-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+
   | Perf  | (     | N     | N     | X     |       |       | K     |       |       |       |       |       |       |       |
   | ormed | 0040, |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | St    | 0242) |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | ation |       |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | Name  |       |       |       |       |       |       |       |       |       |       |       |       |       |       |
   +-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+
   | Perf  | (     | N     | N     | X     |       |       | K     |       |       |       |       |       |       |       |
   | ormed | 0040, |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | St    | 4028) |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | ation |       |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | Name  |       |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | Code  |       |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | Seq   |       |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | uence |       |       |       |       |       |       |       |       |       |       |       |       |       |       |
   +-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+
   | Perfo | (     | N     | Y     | X     |       |       |       |       |       |       |       |       |       |       |
   | rming | 0008, |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | P     | 1050) |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | hysic |       |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | ian's |       |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | Name  |       |       |       |       |       |       |       |       |       |       |       |       |       |       |
   +-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+
   | Perfo | (     | N     | Y     | X     |       |       |       |       |       |       |       |       |       |       |
   | rming | 0008, |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | Phys  | 1052) |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | ician |       |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | Iden  |       |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | tific |       |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | ation |       |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | Seq   |       |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | uence |       |       |       |       |       |       |       |       |       |       |       |       |       |       |
   +-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+
   | Per   | (     | N     | Y     | X     |       |       |       |       |       |       |       |       |       |       |
   | son's | 0040, |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | Ad    | 1102) |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | dress |       |       |       |       |       |       |       |       |       |       |       |       |       |       |
   +-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+
   | Per   | (     | N     | Y     | X     |       |       |       |       |       |       |       |       |       |       |
   | son's | 0040, |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | Te    | 1104) |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | lecom |       |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | I     |       |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | nform |       |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | ation |       |       |       |       |       |       |       |       |       |       |       |       |       |       |
   +-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+
   | Per   | (     | N     | Y     | X     |       |       |       |       |       |       |       |       |       |       |
   | son's | 0040, |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | Tele  | 1103) |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | phone |       |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | Nu    |       |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | mbers |       |       |       |       |       |       |       |       |       |       |       |       |       |       |
   +-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+
   | P     | (     | N     | Y     | D     |       |       |       |       |       |       |       |       |       |       |
   | erson | 0040, |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | Iden  | 1101) |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | tific |       |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | ation |       |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | Code  |       |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | Seq   |       |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | uence |       |       |       |       |       |       |       |       |       |       |       |       |       |       |
   +-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+
   | P     | (     | N     | Y     | D     |       |       |       |       |       |       |       |       |       |       |
   | erson | 0040, |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | Name  | A123) |       |       |       |       |       |       |       |       |       |       |       |       |       |
   +-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+
   | Ph    | (     | N     | Y     | X     |       |       |       |       |       |       |       |       |       |       |
   | ysici | 0008, |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | an(s) | 1048) |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | of    |       |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | R     |       |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | ecord |       |       |       |       |       |       |       |       |       |       |       |       |       |       |
   +-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+
   | Ph    | (     | N     | Y     | X     |       |       |       |       |       |       |       |       |       |       |
   | ysici | 0008, |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | an(s) | 1049) |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | of    |       |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | R     |       |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | ecord |       |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | Iden  |       |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | tific |       |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | ation |       |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | Seq   |       |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | uence |       |       |       |       |       |       |       |       |       |       |       |       |       |       |
   +-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+
   | Ph    | (     | N     | Y     | X     |       |       |       |       |       |       |       |       |       |       |
   | ysici | 0008, |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | an(s) | 1062) |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | Re    |       |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | ading |       |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | Study |       |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | Iden  |       |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | tific |       |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | ation |       |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | Seq   |       |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | uence |       |       |       |       |       |       |       |       |       |       |       |       |       |       |
   +-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+
   | Phys  | (     | Y     | N     | X     |       |       |       |       |       |       |       |       |       |       |
   | ician | 4008, |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | Appr  | 0114) |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | oving |       |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | Inte  |       |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | rpret |       |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | ation |       |       |       |       |       |       |       |       |       |       |       |       |       |       |
   +-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+
   | P     | (     | N     | Y     | Z     |       |       |       |       |       |       |       |       |       |       |
   | lacer | 0040, |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | Order | 2016) |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | N     |       |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | umber |       |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | /     |       |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | Im    |       |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | aging |       |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | Se    |       |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | rvice |       |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | Re    |       |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | quest |       |       |       |       |       |       |       |       |       |       |       |       |       |       |
   +-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+
   | Plate | (     | N     | Y     | X     |       |       | K     |       |       |       |       |       |       |       |
   | ID    | 0018, |       |       |       |       |       |       |       |       |       |       |       |       |       |
   |       | 1004) |       |       |       |       |       |       |       |       |       |       |       |       |       |
   +-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+
   | Preg  | (     | N     | N     | X     |       |       |       |       | K     |       |       |       |       |       |
   | nancy | 0010, |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | S     | 21C0) |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | tatus |       |       |       |       |       |       |       |       |       |       |       |       |       |       |
   +-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+
   | Pre-  | (     | N     | N     | X     |       |       |       |       | C     |       |       |       |       |       |
   | Medic | 0040, |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | ation | 0012) |       |       |       |       |       |       |       |       |       |       |       |       |       |
   +-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+
   | Pr    | (     | N     | Y     | X     |       |       |       |       |       |       |       | C     |       |       |
   | escri | 300A, |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | ption | 000E) |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | D     |       |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | escri |       |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | ption |       |       |       |       |       |       |       |       |       |       |       |       |       |       |
   +-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+
   | Pr    | (     | N     | Y     | Z     |       |       |       |       |       |       |       | C     |       |       |
   | escri | 3010, |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | ption | 007B) |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | Notes |       |       |       |       |       |       |       |       |       |       |       |       |       |       |
   +-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+
   | Pr    | (     | N     | Y     | Z     |       |       |       |       |       |       |       | C     |       |       |
   | escri | 3010, |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | ption | 0081) |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | Notes |       |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | Seq   |       |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | uence |       |       |       |       |       |       |       |       |       |       |       |       |       |       |
   +-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+
   | Pr    | (     | N     | Y     | U     |       | K     |       |       |       |       |       |       |       |       |
   | esent | 0070, |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | ation | 1101) |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | Di    |       |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | splay |       |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | Colle |       |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | ction |       |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | UID   |       |       |       |       |       |       |       |       |       |       |       |       |       |       |
   +-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+
   | Pr    | (     | N     | Y     | U     |       | K     |       |       |       |       |       |       |       |       |
   | esent | 0070, |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | ation | 1102) |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | Seq   |       |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | uence |       |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | Colle |       |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | ction |       |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | UID   |       |       |       |       |       |       |       |       |       |       |       |       |       |       |
   +-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+
   | Prior | (     | N     | Y     | X     |       |       |       |       |       |       |       | C     |       |       |
   | Trea  | 3010, |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | tment | 0061) |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | Dose  |       |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | D     |       |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | escri |       |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | ption |       |       |       |       |       |       |       |       |       |       |       |       |       |       |
   +-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+
   | *Pr   | *(    | N     | N     | X     | C     |       |       |       |       |       |       |       |       |       |
   | ivate | gggg, |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | a     | eeee) |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | ttrib | where |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | utes* | gggg  |       |       |       |       |       |       |       |       |       |       |       |       |       |
   |       | is    |       |       |       |       |       |       |       |       |       |       |       |       |       |
   |       | odd*  |       |       |       |       |       |       |       |       |       |       |       |       |       |
   +-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+
   | Proc  | (     | N     | N     | X     |       |       |       |       |       | K     | C     |       |       |       |
   | edure | 0040, |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | Step  | 4052) |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | Ca    |       |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | ncell |       |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | ation |       |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | Dat   |       |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | eTime |       |       |       |       |       |       |       |       |       |       |       |       |       |       |
   +-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+
   | Pro   | (     | N     | Y     | X/D   |       |       |       |       |       |       |       | C     |       |       |
   | tocol | 0018, |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | Name  | 1030) |       |       |       |       |       |       |       |       |       |       |       |       |       |
   +-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+
   | Radi  | (     | N     | Y     | D     |       |       |       |       |       |       |       | C     |       |       |
   | ation | 300A, |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | Dose  | 0619) |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | Iden  |       |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | tific |       |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | ation |       |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | Label |       |       |       |       |       |       |       |       |       |       |       |       |       |       |
   +-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+
   | Radi  | (     | N     | Y     | D     |       |       |       |       |       |       |       | C     |       |       |
   | ation | 300A, |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | Dose  | 0623) |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | In    |       |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | -Vivo |       |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | M     |       |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | easur |       |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | ement |       |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | Label |       |       |       |       |       |       |       |       |       |       |       |       |       |       |
   +-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+
   | Radi  | (     | N     | Y     | Z     |       |       |       |       |       |       |       | C     |       |       |
   | ation | 300A, |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | Gener | 067D) |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | ation |       |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | Mode  |       |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | D     |       |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | escri |       |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | ption |       |       |       |       |       |       |       |       |       |       |       |       |       |       |
   +-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+
   | Radi  | (     | N     | Y     | D     |       |       |       |       |       |       |       | C     |       |       |
   | ation | 300A, |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | Gener | 067C) |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | ation |       |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | Mode  |       |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | Label |       |       |       |       |       |       |       |       |       |       |       |       |       |       |
   +-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+
   | R     | (     | N     | Y     | X     |       |       |       |       |       |       |       | C     |       |       |
   | eason | 300C, |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | for   | 0113) |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | Omi   |       |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | ssion |       |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | D     |       |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | escri |       |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | ption |       |       |       |       |       |       |       |       |       |       |       |       |       |       |
   +-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+
   | R     | (     | N     | Y     | X     |       |       |       |       |       |       |       | C     |       |       |
   | eason | 0040, |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | for   | 100A) |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | Requ  |       |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | ested |       |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | Proc  |       |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | edure |       |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | Code  |       |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | Seq   |       |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | uence |       |       |       |       |       |       |       |       |       |       |       |       |       |       |
   +-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+
   | R     | (     | Y     | N     | X     |       |       |       |       |       |       |       | C     |       |       |
   | eason | 0032, |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | for   | 1030) |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | Study |       |       |       |       |       |       |       |       |       |       |       |       |       |       |
   +-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+
   | R     | (     | N     | Y     | Z     |       |       |       |       |       |       |       | C     |       |       |
   | eason | 3010, |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | for   | 005C) |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | S     |       |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | upers |       |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | eding |       |       |       |       |       |       |       |       |       |       |       |       |       |       |
   +-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+
   | R     | (     | Y     | N     | X     |       |       |       |       |       |       |       | C     |       |       |
   | eason | 0040, |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | for   | 2001) |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | the   |       |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | Im    |       |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | aging |       |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | Se    |       |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | rvice |       |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | Re    |       |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | quest |       |       |       |       |       |       |       |       |       |       |       |       |       |       |
   +-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+
   | R     | (     | N     | Y     | X     |       |       |       |       |       |       |       | C     |       |       |
   | eason | 0040, |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | for   | 1002) |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | the   |       |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | Requ  |       |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | ested |       |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | Proc  |       |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | edure |       |       |       |       |       |       |       |       |       |       |       |       |       |       |
   +-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+
   | R     | (     | N     | Y     | X     |       |       |       |       |       |       |       | C     |       |       |
   | eason | 0032, |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | for   | 1066) |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | Visit |       |       |       |       |       |       |       |       |       |       |       |       |       |       |
   +-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+
   | R     | (     | N     | Y     | X     |       |       |       |       |       |       |       | C     |       |       |
   | eason | 0032, |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | for   | 1067) |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | Visit |       |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | Code  |       |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | Seq   |       |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | uence |       |       |       |       |       |       |       |       |       |       |       |       |       |       |
   +-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+
   | Rec   | (     | N     | Y     | D     |       |       |       |       |       | K     | C     |       |       |       |
   | orded | 300A, |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | RT    | 073A) |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | Co    |       |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | ntrol |       |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | Point |       |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | Dat   |       |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | eTime |       |       |       |       |       |       |       |       |       |       |       |       |       |       |
   +-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+
   | Refer | (     | N     | Y     | U     |       | K     |       |       |       |       |       |       |       |       |
   | enced | 3010, |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | Conce | 000B) |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | ptual |       |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | V     |       |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | olume |       |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | UID   |       |       |       |       |       |       |       |       |       |       |       |       |       |       |
   +-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+
   | Refer | (     | N     | Y     | X     |       |       |       |       |       |       |       |       |       |       |
   | enced | 0400, |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | Di    | 0402) |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | gital |       |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | Sign  |       |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | ature |       |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | Seq   |       |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | uence |       |       |       |       |       |       |       |       |       |       |       |       |       |       |
   +-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+
   | Refer | (     | N     | Y     | U     |       | K     |       |       |       |       |       |       |       |       |
   | enced | 300A, |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | Dose  | 0083) |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | Refe  |       |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | rence |       |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | UID   |       |       |       |       |       |       |       |       |       |       |       |       |       |       |
   +-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+
   | Refer | (     | N     | Y     | U     |       | K     |       |       |       |       |       |       |       |       |
   | enced | 3010, |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | Dosim | 006F) |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | etric |       |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | Obje  |       |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | ctive |       |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | UID   |       |       |       |       |       |       |       |       |       |       |       |       |       |       |
   +-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+
   | Refer | (     | N     | Y     | U     |       | K     |       |       |       |       |       |       |       |       |
   | enced | 3010, |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | Fidu  | 0031) |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | cials |       |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | UID   |       |       |       |       |       |       |       |       |       |       |       |       |       |       |
   +-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+
   | Refer | (     | N     | Y     | U     |       | K     |       |       |       |       |       |       |       |       |
   | enced | 3006, |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | Frame | 0024) |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | of    |       |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | Refe  |       |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | rence |       |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | UID   |       |       |       |       |       |       |       |       |       |       |       |       |       |       |
   +-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+
   | Refer | (     | Y     | N     | U     |       | K     |       |       |       |       |       |       |       |       |
   | enced | 0040, |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | Ge    | 4023) |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | neral |       |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | Pu    |       |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | rpose |       |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | Sche  |       |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | duled |       |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | Proc  |       |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | edure |       |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | Step  |       |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | T     |       |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | ransa |       |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | ction |       |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | UID   |       |       |       |       |       |       |       |       |       |       |       |       |       |       |
   +-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+
   | Refer | (     | N     | Y     | X/    |       | K     |       |       |       |       |       |       |       |       |
   | enced | 0008, |       |       | Z/U\* |       |       |       |       |       |       |       |       |       |       |
   | Image | 1140) |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | Seq   |       |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | uence |       |       |       |       |       |       |       |       |       |       |       |       |       |       |
   +-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+
   | Refer | (     | Y     | N     | U     |       | K     |       |       |       |       |       |       |       |       |
   | enced | 0040, |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | O     | A172) |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | bserv |       |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | ation |       |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | UID   |       |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | (T    |       |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | rial) |       |       |       |       |       |       |       |       |       |       |       |       |       |       |
   +-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+
   | Refer | (     | N     | N     | X     |       |       |       |       |       |       |       |       |       |       |
   | enced | 0038, |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | Pa    | 0004) |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | tient |       |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | Alias |       |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | Seq   |       |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | uence |       |       |       |       |       |       |       |       |       |       |       |       |       |       |
   +-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+
   | Refer | (     | N     | Y     | X     |       |       |       |       |       |       |       |       |       |       |
   | enced | 0010, |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | Pa    | 1100) |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | tient |       |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | Photo |       |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | Seq   |       |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | uence |       |       |       |       |       |       |       |       |       |       |       |       |       |       |
   +-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+
   | Refer | (     | N     | Y     | X     |       | X     |       |       |       |       |       |       |       |       |
   | enced | 0008, |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | Pa    | 1120) |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | tient |       |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | Seq   |       |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | uence |       |       |       |       |       |       |       |       |       |       |       |       |       |       |
   +-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+
   | Refer | (     | N     | Y     | X/Z/D |       | K     |       |       |       |       |       |       |       |       |
   | enced | 0008, |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | Perf  | 1111) |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | ormed |       |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | Proc  |       |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | edure |       |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | Step  |       |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | Seq   |       |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | uence |       |       |       |       |       |       |       |       |       |       |       |       |       |       |
   +-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+
   | Refer | (     | N     | Y     | X     |       |       |       |       |       |       |       |       |       |       |
   | enced | 0400, |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | SOP   | 0403) |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | Ins   |       |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | tance |       |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | MAC   |       |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | Seq   |       |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | uence |       |       |       |       |       |       |       |       |       |       |       |       |       |       |
   +-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+
   | Refer | (     | N     | Y     | U     |       | K     |       |       |       |       |       |       |       |       |
   | enced | 0008, |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | SOP   | 1155) |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | Ins   |       |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | tance |       |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | UID   |       |       |       |       |       |       |       |       |       |       |       |       |       |       |
   +-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+
   | Refer | (     | N     | N     | U     |       | K     |       |       |       |       |       |       |       |       |
   | enced | 0004, |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | SOP   | 1511) |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | Ins   |       |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | tance |       |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | UID   |       |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | in    |       |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | File  |       |       |       |       |       |       |       |       |       |       |       |       |       |       |
   +-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+
   | Refer | (     | N     | Y     | X/Z   |       | K     |       |       |       |       |       |       |       |       |
   | enced | 0008, |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | Study | 1110) |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | Seq   |       |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | uence |       |       |       |       |       |       |       |       |       |       |       |       |       |       |
   +-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+
   | Refe  | (     | N     | N     | X     |       |       |       |       |       |       |       |       |       |       |
   | rring | 0008, |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | P     | 0092) |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | hysic |       |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | ian's |       |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | Ad    |       |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | dress |       |       |       |       |       |       |       |       |       |       |       |       |       |       |
   +-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+
   | Refe  | (     | N     | Y     | Z     |       |       |       |       |       |       |       |       |       |       |
   | rring | 0008, |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | P     | 0090) |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | hysic |       |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | ian's |       |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | Name  |       |       |       |       |       |       |       |       |       |       |       |       |       |       |
   +-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+
   | Refe  | (     | N     | N     | X     |       |       |       |       |       |       |       |       |       |       |
   | rring | 0008, |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | P     | 0094) |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | hysic |       |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | ian's |       |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | Tele  |       |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | phone |       |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | Nu    |       |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | mbers |       |       |       |       |       |       |       |       |       |       |       |       |       |       |
   +-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+
   | Refe  | (     | N     | Y     | X     |       |       |       |       |       |       |       |       |       |       |
   | rring | 0008, |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | Phys  | 0096) |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | ician |       |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | Iden  |       |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | tific |       |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | ation |       |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | Seq   |       |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | uence |       |       |       |       |       |       |       |       |       |       |       |       |       |       |
   +-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+
   | R     | (     | N     | N     | X     |       |       |       |       |       |       |       |       |       |       |
   | egion | 0010, |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | of    | 2152) |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | Resi  |       |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | dence |       |       |       |       |       |       |       |       |       |       |       |       |       |       |
   +-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+
   | Re    | (     | Y     | N     | U     |       | K     |       |       |       |       |       |       |       |       |
   | lated | 3006, |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | Frame | 00C2) |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | of    |       |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | Refe  |       |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | rence |       |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | UID   |       |       |       |       |       |       |       |       |       |       |       |       |       |       |
   +-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+
   | Re    | (     | N     | Y     | X     |       |       |       |       |       |       |       | C     |       |       |
   | quest | 0040, |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | Attri | 0275) |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | butes |       |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | Seq   |       |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | uence |       |       |       |       |       |       |       |       |       |       |       |       |       |       |
   +-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+
   | Requ  | (     | N     | N     | X     |       |       |       |       |       |       |       | C     |       |       |
   | ested | 0032, |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | Con   | 1070) |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | trast |       |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | Agent |       |       |       |       |       |       |       |       |       |       |       |       |       |       |
   +-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+
   | Requ  | (     | N     | N     | X     |       |       |       |       |       |       |       | C     |       |       |
   | ested | 0040, |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | Proc  | 1400) |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | edure |       |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | Com   |       |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | ments |       |       |       |       |       |       |       |       |       |       |       |       |       |       |
   +-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+
   | Requ  | (     | N     | Y     | X/Z   |       |       |       |       |       |       |       | C     |       |       |
   | ested | 0032, |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | Proc  | 1060) |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | edure |       |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | D     |       |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | escri |       |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | ption |       |       |       |       |       |       |       |       |       |       |       |       |       |       |
   +-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+
   | Requ  | (     | N     | N     | X     |       |       |       |       |       |       |       |       |       |       |
   | ested | 0040, |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | Proc  | 1001) |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | edure |       |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | ID    |       |       |       |       |       |       |       |       |       |       |       |       |       |       |
   +-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+
   | Requ  | (     | N     | N     | X     |       |       |       |       |       |       |       |       |       |       |
   | ested | 0040, |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | Proc  | 1005) |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | edure |       |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | Loc   |       |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | ation |       |       |       |       |       |       |       |       |       |       |       |       |       |       |
   +-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+
   | Requ  | (     | N     | N     | U     |       | K     |       |       |       |       |       |       |       |       |
   | ested | 0000, |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | SOP   | 1001) |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | Ins   |       |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | tance |       |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | UID   |       |       |       |       |       |       |       |       |       |       |       |       |       |       |
   +-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+
   | Reque | (     | N     | N     | X     |       |       |       |       |       |       |       |       |       |       |
   | sting | 0032, |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | Phys  | 1032) |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | ician |       |       |       |       |       |       |       |       |       |       |       |       |       |       |
   +-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+
   | Reque | (     | N     | N     | X     |       |       |       |       |       |       |       |       |       |       |
   | sting | 0032, |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | Se    | 1033) |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | rvice |       |       |       |       |       |       |       |       |       |       |       |       |       |       |
   +-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+
   | R     | (     | N     | Y     | X     |       |       |       |       |       |       |       | C     |       |       |
   | espir | 0018, |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | atory | 9185) |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | M     |       |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | otion |       |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | Co    |       |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | mpens |       |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | ation |       |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | Tech  |       |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | nique |       |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | D     |       |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | escri |       |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | ption |       |       |       |       |       |       |       |       |       |       |       |       |       |       |
   +-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+
   | R     | (     | N     | Y     | X     |       |       |       |       |       |       |       |       |       |       |
   | espon | 0010, |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | sible | 2299) |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | Or    |       |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | ganiz |       |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | ation |       |       |       |       |       |       |       |       |       |       |       |       |       |       |
   +-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+
   | R     | (     | N     | Y     | X     |       |       |       |       |       |       |       |       |       |       |
   | espon | 0010, |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | sible | 2297) |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | P     |       |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | erson |       |       |       |       |       |       |       |       |       |       |       |       |       |       |
   +-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+
   | Re    | (     | Y     | N     | X     |       |       |       |       |       |       |       | C     |       |       |
   | sults | 4008, |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | Com   | 4000) |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | ments |       |       |       |       |       |       |       |       |       |       |       |       |       |       |
   +-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+
   | Re    | (     | Y     | N     | X     |       |       |       |       |       |       |       |       |       |       |
   | sults | 4008, |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | Di    | 0118) |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | strib |       |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | ution |       |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | List  |       |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | Seq   |       |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | uence |       |       |       |       |       |       |       |       |       |       |       |       |       |       |
   +-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+
   | Re    | (     | Y     | N     | X     |       |       |       |       |       |       |       |       |       |       |
   | sults | 4008, |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | ID    | 0042) |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | I     |       |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | ssuer |       |       |       |       |       |       |       |       |       |       |       |       |       |       |
   +-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+
   | Rev   | (     | N     | Y     | X/Z   |       |       |       |       |       |       |       |       |       |       |
   | iewer | 300E, |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | Name  | 0008) |       |       |       |       |       |       |       |       |       |       |       |       |       |
   +-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+
   | RT    | (     | N     | Y     | Z     |       |       |       |       |       |       |       |       |       |       |
   | Acce  | 300A, |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | ssory | 0615) |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | D     |       |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | evice |       |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | Slot  |       |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | ID    |       |       |       |       |       |       |       |       |       |       |       |       |       |       |
   +-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+
   | RT    | (     | N     | Y     | Z     |       |       |       |       |       |       |       |       |       |       |
   | Acce  | 300A, |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | ssory | 0611) |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | H     |       |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | older |       |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | Slot  |       |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | ID    |       |       |       |       |       |       |       |       |       |       |       |       |       |       |
   +-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+
   | RT    | (     | N     | Y     | Z     |       |       |       |       |       |       |       | C     |       |       |
   | Phys  | 3010, |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | ician | 005A) |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | I     |       |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | ntent |       |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | Narr  |       |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | ative |       |       |       |       |       |       |       |       |       |       |       |       |       |       |
   +-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+
   | RT    | (     | N     | Y     | X/D   |       |       |       |       |       | K     | C     |       |       |       |
   | Plan  | 300A, |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | Date  | 0006) |       |       |       |       |       |       |       |       |       |       |       |       |       |
   +-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+
   | RT    | (     | N     | Y     | X     |       |       |       |       |       |       |       | C     |       |       |
   | Plan  | 300A, |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | D     | 0004) |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | escri |       |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | ption |       |       |       |       |       |       |       |       |       |       |       |       |       |       |
   +-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+
   | RT    | (     | N     | Y     | D     |       |       |       |       |       |       |       | C     |       |       |
   | Plan  | 300A, |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | Label | 0002) |       |       |       |       |       |       |       |       |       |       |       |       |       |
   +-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+
   | RT    | (     | N     | Y     | X     |       |       |       |       |       |       |       | C     |       |       |
   | Plan  | 300A, |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | Name  | 0003) |       |       |       |       |       |       |       |       |       |       |       |       |       |
   +-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+
   | RT    | (     | N     | Y     | X/D   |       |       |       |       |       | K     | C     |       |       |       |
   | Plan  | 300A, |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | Time  | 0007) |       |       |       |       |       |       |       |       |       |       |       |       |       |
   +-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+
   | RT    | (     | N     | Y     | D     |       |       |       |       |       |       |       | C     |       |       |
   | Pr    | 3010, |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | escri | 0054) |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | ption |       |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | Label |       |       |       |       |       |       |       |       |       |       |       |       |       |       |
   +-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+
   | RT    | (     | N     | Y     | D     |       |       |       |       |       |       |       | C     |       |       |
   | Tole  | 300A, |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | rance | 062A) |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | Set   |       |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | Label |       |       |       |       |       |       |       |       |       |       |       |       |       |       |
   +-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+
   | RT    | (     | N     | Y     | X/D   |       |       |       |       |       |       |       | C     |       |       |
   | Trea  | 3010, |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | tment | 0056) |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | App   |       |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | roach |       |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | Label |       |       |       |       |       |       |       |       |       |       |       |       |       |       |
   +-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+
   | RT    | (     | N     | Y     | U     |       | K     |       |       |       |       |       |       |       |       |
   | Trea  | 3010, |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | tment | 003B) |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | Phase |       |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | UID   |       |       |       |       |       |       |       |       |       |       |       |       |       |       |
   +-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+
   | Sche  | (     | N     | N     | X     |       |       |       |       |       |       |       |       |       |       |
   | duled | 0040, |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | Human | 4034) |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | Perfo |       |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | rmers |       |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | Seq   |       |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | uence |       |       |       |       |       |       |       |       |       |       |       |       |       |       |
   +-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+
   | Sche  | (     | Y     | N     | X     |       |       |       |       |       |       |       |       |       |       |
   | duled | 0038, |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | Pa    | 001E) |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | tient |       |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | I     |       |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | nstit |       |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | ution |       |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | Resi  |       |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | dence |       |       |       |       |       |       |       |       |       |       |       |       |       |       |
   +-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+
   | Sche  | (     | N     | N     | X     |       |       |       |       |       |       |       |       |       |       |
   | duled | 0040, |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | Perfo | 0006) |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | rming |       |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | P     |       |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | hysic |       |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | ian's |       |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | Name  |       |       |       |       |       |       |       |       |       |       |       |       |       |       |
   +-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+
   | Sche  | (     | N     | N     | X     |       |       |       |       |       |       |       |       |       |       |
   | duled | 0040, |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | Perfo | 000B) |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | rming |       |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | Phys  |       |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | ician |       |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | Iden  |       |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | tific |       |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | ation |       |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | Seq   |       |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | uence |       |       |       |       |       |       |       |       |       |       |       |       |       |       |
   +-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+
   | Sche  | (     | N     | Y     | X     |       |       |       |       |       |       |       | C     |       |       |
   | duled | 0040, |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | Proc  | 0007) |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | edure |       |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | Step  |       |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | D     |       |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | escri |       |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | ption |       |       |       |       |       |       |       |       |       |       |       |       |       |       |
   +-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+
   | Sche  | (     | N     | N     | X     |       |       |       |       |       | K     | C     |       |       |       |
   | duled | 0040, |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | Proc  | 0004) |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | edure |       |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | Step  |       |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | End   |       |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | Date  |       |       |       |       |       |       |       |       |       |       |       |       |       |       |
   +-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+
   | Sche  | (     | N     | N     | X     |       |       |       |       |       | K     | C     |       |       |       |
   | duled | 0040, |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | Proc  | 0005) |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | edure |       |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | Step  |       |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | End   |       |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | Time  |       |       |       |       |       |       |       |       |       |       |       |       |       |       |
   +-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+
   | Sche  | (     | N     | N     | X     |       |       |       |       |       | K     | C     |       |       |       |
   | duled | 0040, |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | Proc  | 4008) |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | edure |       |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | Step  |       |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | Expir |       |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | ation |       |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | Dat   |       |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | eTime |       |       |       |       |       |       |       |       |       |       |       |       |       |       |
   +-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+
   | Sche  | (     | N     | N     | X     |       |       | K     |       |       |       |       |       |       |       |
   | duled | 0040, |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | Proc  | 0011) |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | edure |       |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | Step  |       |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | Loc   |       |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | ation |       |       |       |       |       |       |       |       |       |       |       |       |       |       |
   +-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+
   | Sche  | (     | N     | N     | X     |       |       |       |       |       | K     | C     |       |       |       |
   | duled | 0040, |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | Proc  | 4010) |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | edure |       |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | Step  |       |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | Mo    |       |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | dific |       |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | ation |       |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | Dat   |       |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | eTime |       |       |       |       |       |       |       |       |       |       |       |       |       |       |
   +-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+
   | Sche  | (     | N     | N     | X     |       |       |       |       |       | K     | C     |       |       |       |
   | duled | 0040, |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | Proc  | 0002) |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | edure |       |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | Step  |       |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | Start |       |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | Date  |       |       |       |       |       |       |       |       |       |       |       |       |       |       |
   +-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+
   | Sche  | (     | N     | N     | X     |       |       |       |       |       | K     | C     |       |       |       |
   | duled | 0040, |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | Proc  | 4005) |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | edure |       |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | Step  |       |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | Start |       |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | Dat   |       |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | eTime |       |       |       |       |       |       |       |       |       |       |       |       |       |       |
   +-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+
   | Sche  | (     | N     | N     | X     |       |       |       |       |       | K     | C     |       |       |       |
   | duled | 0040, |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | Proc  | 0003) |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | edure |       |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | Step  |       |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | Start |       |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | Time  |       |       |       |       |       |       |       |       |       |       |       |       |       |       |
   +-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+
   | Sche  | (     | N     | N     | X     |       |       | K     |       |       |       |       |       |       |       |
   | duled | 0040, |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | St    | 0001) |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | ation |       |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | AE    |       |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | Title |       |       |       |       |       |       |       |       |       |       |       |       |       |       |
   +-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+
   | Sche  | (     | N     | N     | X     |       |       | K     |       |       |       |       |       |       |       |
   | duled | 0040, |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | St    | 4027) |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | ation |       |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | Geogr |       |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | aphic |       |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | Loc   |       |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | ation |       |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | Code  |       |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | Seq   |       |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | uence |       |       |       |       |       |       |       |       |       |       |       |       |       |       |
   +-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+
   | Sche  | (     | N     | N     | X     |       |       | K     |       |       |       |       |       |       |       |
   | duled | 0040, |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | St    | 0010) |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | ation |       |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | Name  |       |       |       |       |       |       |       |       |       |       |       |       |       |       |
   +-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+
   | Sche  | (     | N     | N     | X     |       |       | K     |       |       |       |       |       |       |       |
   | duled | 0040, |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | St    | 4025) |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | ation |       |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | Name  |       |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | Code  |       |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | Seq   |       |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | uence |       |       |       |       |       |       |       |       |       |       |       |       |       |       |
   +-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+
   | Sche  | (     | Y     | N     | X     |       |       | K     |       |       |       |       |       |       |       |
   | duled | 0032, |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | Study | 1020) |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | Loc   |       |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | ation |       |       |       |       |       |       |       |       |       |       |       |       |       |       |
   +-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+
   | Sche  | (     | Y     | N     | X     |       |       | K     |       |       |       |       |       |       |       |
   | duled | 0032, |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | Study | 1021) |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | Loc   |       |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | ation |       |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | AE    |       |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | Title |       |       |       |       |       |       |       |       |       |       |       |       |       |       |
   +-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+
   | S     | (     | N     | Y     | X/D   |       |       |       |       |       | K     | C     |       |       |       |
   | eries | 0008, |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | Date  | 0021) |       |       |       |       |       |       |       |       |       |       |       |       |       |
   +-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+
   | S     | (     | N     | Y     | X     |       |       |       |       |       |       |       | C     |       |       |
   | eries | 0008, |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | D     | 103E) |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | escri |       |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | ption |       |       |       |       |       |       |       |       |       |       |       |       |       |       |
   +-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+
   | S     | (     | N     | Y     | U     |       | K     |       |       |       |       |       |       |       |       |
   | eries | 0020, |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | Ins   | 000E) |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | tance |       |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | UID   |       |       |       |       |       |       |       |       |       |       |       |       |       |       |
   +-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+
   | S     | (     | N     | Y     | X/D   |       |       |       |       |       | K     | C     |       |       |       |
   | eries | 0008, |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | Time  | 0031) |       |       |       |       |       |       |       |       |       |       |       |       |       |
   +-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+
   | Se    | (     | N     | Y     | X     |       |       |       |       |       |       |       | C     |       |       |
   | rvice | 0038, |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | Ep    | 0062) |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | isode |       |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | D     |       |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | escri |       |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | ption |       |       |       |       |       |       |       |       |       |       |       |       |       |       |
   +-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+
   | Se    | (     | N     | Y     | X     |       |       |       |       |       |       |       |       |       |       |
   | rvice | 0038, |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | Ep    | 0060) |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | isode |       |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | ID    |       |       |       |       |       |       |       |       |       |       |       |       |       |       |
   +-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+
   | Setup | (     | N     | Y     | X     |       |       |       |       |       |       |       | C     |       |       |
   | Tech  | 300A, |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | nique | 01B2) |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | D     |       |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | escri |       |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | ption |       |       |       |       |       |       |       |       |       |       |       |       |       |       |
   +-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+
   | Shie  | (     | N     | Y     | X     |       |       |       |       |       |       |       | C     |       |       |
   | lding | 300A, |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | D     | 01A6) |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | evice |       |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | D     |       |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | escri |       |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | ption |       |       |       |       |       |       |       |       |       |       |       |       |       |       |
   +-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+
   | Slide | (     | Y     | N     | X     |       |       |       |       |       |       |       |       |       |       |
   | Ident | 0040, |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | ifier | 06FA) |       |       |       |       |       |       |       |       |       |       |       |       |       |
   +-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+
   | Sm    | (     | N     | N     | X     |       |       |       |       | K     |       |       |       |       |       |
   | oking | 0010, |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | S     | 21A0) |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | tatus |       |       |       |       |       |       |       |       |       |       |       |       |       |       |
   +-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+
   | SOP   | (     | N     | Y     | U     |       | K     |       |       |       |       |       |       |       |       |
   | Ins   | 0008, |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | tance | 0018) |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | UID   |       |       |       |       |       |       |       |       |       |       |       |       |       |       |
   +-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+
   | S     | (     | N     | Y     | U     |       | K     |       |       |       |       |       |       |       |       |
   | ource | 3010, |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | Conce | 0015) |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | ptual |       |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | V     |       |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | olume |       |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | UID   |       |       |       |       |       |       |       |       |       |       |       |       |       |       |
   +-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+
   | S     | (     | N     | Y     | D     |       |       |       |       |       | K     | C     |       |       |       |
   | ource | 0018, |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | End   | 936A) |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | Dat   |       |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | eTime |       |       |       |       |       |       |       |       |       |       |       |       |       |       |
   +-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+
   | S     | (     | N     | Y     | D     |       |       |       |       |       |       |       |       |       |       |
   | ource | 0034, |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | Ident | 0005) |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | ifier |       |       |       |       |       |       |       |       |       |       |       |       |       |       |
   +-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+
   | S     | (     | N     | Y     | X/    |       | K     |       |       |       |       |       |       |       |       |
   | ource | 0008, |       |       | Z/U\* |       |       |       |       |       |       |       |       |       |       |
   | Image | 2112) |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | Seq   |       |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | uence |       |       |       |       |       |       |       |       |       |       |       |       |       |       |
   +-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+
   | S     | (     | N     | Y     | X     |       |       | K     |       |       |       |       |       |       |       |
   | ource | 300A, |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | Ma    | 0216) |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | nufac |       |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | turer |       |       |       |       |       |       |       |       |       |       |       |       |       |       |
   +-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+
   | S     | (     | N     | Y     | X/Z   |       |       | K     |       |       |       |       |       |       |       |
   | ource | 3008, |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | S     | 0105) |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | erial |       |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | N     |       |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | umber |       |       |       |       |       |       |       |       |       |       |       |       |       |       |
   +-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+
   | S     | (     | N     | Y     | D     |       |       |       |       |       | K     | C     |       |       |       |
   | ource | 0018, |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | Start | 9369) |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | Dat   |       |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | eTime |       |       |       |       |       |       |       |       |       |       |       |       |       |       |
   +-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+
   | Sp    | (     | N     | N     | X     |       |       |       |       | C     |       |       |       |       |       |
   | ecial | 0038, |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | Needs | 0050) |       |       |       |       |       |       |       |       |       |       |       |       |       |
   +-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+
   | Spe   | (     | Y     | N     | X     |       |       |       |       |       |       |       |       |       |       |
   | cimen | 0040, |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | Acce  | 050A) |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | ssion |       |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | N     |       |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | umber |       |       |       |       |       |       |       |       |       |       |       |       |       |       |
   +-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+
   | Spe   | (     | N     | Y     | X     |       |       |       |       |       |       |       | C     |       |       |
   | cimen | 0040, |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | Det   | 0602) |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | ailed |       |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | D     |       |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | escri |       |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | ption |       |       |       |       |       |       |       |       |       |       |       |       |       |       |
   +-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+
   | Spe   | (     | N     | Y     | D     |       |       |       |       |       |       |       |       |       |       |
   | cimen | 0040, |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | Ident | 0551) |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | ifier |       |       |       |       |       |       |       |       |       |       |       |       |       |       |
   +-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+
   | Spe   | (     | N     | Y     | Z     |       |       |       |       |       |       |       |       | C     |       |
   | cimen | 0040, |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | P     | 0610) |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | repar |       |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | ation |       |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | Seq   |       |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | uence |       |       |       |       |       |       |       |       |       |       |       |       |       |       |
   +-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+
   | Spe   | (     | N     | Y     | X     |       |       |       |       |       |       |       | C     |       |       |
   | cimen | 0040, |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | Short | 0600) |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | D     |       |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | escri |       |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | ption |       |       |       |       |       |       |       |       |       |       |       |       |       |       |
   +-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+
   | Spe   | (     | N     | Y     | U     |       | K     |       |       |       |       |       |       |       |       |
   | cimen | 0040, |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | UID   | 0554) |       |       |       |       |       |       |       |       |       |       |       |       |       |
   +-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+
   | Start | (     | N     | Y     | X/D   |       |       |       |       |       | K     | C     |       |       |       |
   | A     | 0018, |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | cquis | 9516) |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | ition |       |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | Dat   |       |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | eTime |       |       |       |       |       |       |       |       |       |       |       |       |       |       |
   +-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+
   | St    | (     | N     | Y     | X/Z/D |       |       | K     |       |       |       |       |       |       |       |
   | ation | 0008, |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | Name  | 1010) |       |       |       |       |       |       |       |       |       |       |       |       |       |
   +-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+
   | St    | (     | N     | Y     | U     |       | K     |       |       |       |       |       |       |       |       |
   | orage | 0088, |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | Media | 0140) |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | Fil   |       |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | e-set |       |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | UID   |       |       |       |       |       |       |       |       |       |       |       |       |       |       |
   +-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+
   | Study | (     | Y     | N     | X     |       |       |       |       |       |       |       | C     |       |       |
   | Com   | 0032, |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | ments | 4000) |       |       |       |       |       |       |       |       |       |       |       |       |       |
   +-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+
   | Study | (     | N     | Y     | Z     |       |       |       |       |       | K     | C     |       |       |       |
   | Date  | 0008, |       |       |       |       |       |       |       |       |       |       |       |       |       |
   |       | 0020) |       |       |       |       |       |       |       |       |       |       |       |       |       |
   +-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+
   | Study | (     | N     | Y     | X     |       |       |       |       |       |       |       | C     |       |       |
   | D     | 0008, |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | escri | 1030) |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | ption |       |       |       |       |       |       |       |       |       |       |       |       |       |       |
   +-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+
   | Study | (     | N     | Y     | Z     |       |       |       |       |       |       |       |       |       |       |
   | ID    | 0020, |       |       |       |       |       |       |       |       |       |       |       |       |       |
   |       | 0010) |       |       |       |       |       |       |       |       |       |       |       |       |       |
   +-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+
   | Study | (     | Y     | N     | X     |       |       |       |       |       |       |       |       |       |       |
   | ID    | 0032, |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | I     | 0012) |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | ssuer |       |       |       |       |       |       |       |       |       |       |       |       |       |       |
   +-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+
   | Study | (     | N     | Y     | U     |       | K     |       |       |       |       |       |       |       |       |
   | Ins   | 0020, |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | tance | 000D) |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | UID   |       |       |       |       |       |       |       |       |       |       |       |       |       |       |
   +-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+
   | Study | (     | N     | Y     | Z     |       |       |       |       |       | K     | C     |       |       |       |
   | Time  | 0008, |       |       |       |       |       |       |       |       |       |       |       |       |       |
   |       | 0030) |       |       |       |       |       |       |       |       |       |       |       |       |       |
   +-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+
   | Synch | (     | N     | Y     | U     |       | K     |       |       |       |       |       |       |       |       |
   | roniz | 0020, |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | ation | 0200) |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | Frame |       |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | of    |       |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | Refe  |       |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | rence |       |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | UID   |       |       |       |       |       |       |       |       |       |       |       |       |       |       |
   +-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+
   | T     | (     | N     | Y     | U     |       | K     |       |       |       |       |       |       |       |       |
   | arget | 0018, |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | UID   | 2042) |       |       |       |       |       |       |       |       |       |       |       |       |       |
   +-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+
   | Tele  | (     | Y     | N     | X     |       |       |       |       |       |       |       |       |       |       |
   | phone | 0040, |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | N     | A354) |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | umber |       |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | (T    |       |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | rial) |       |       |       |       |       |       |       |       |       |       |       |       |       |       |
   +-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+
   | Tem   | (     | Y     | N     | U     |       | K     |       |       |       |       |       |       |       |       |
   | plate | 0040, |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | Exte  | DB0D) |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | nsion |       |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | Cr    |       |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | eator |       |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | UID   |       |       |       |       |       |       |       |       |       |       |       |       |       |       |
   +-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+
   | Tem   | (     | Y     | N     | U     |       | K     |       |       |       |       |       |       |       |       |
   | plate | 0040, |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | Exte  | DB0C) |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | nsion |       |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | Or    |       |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | ganiz |       |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | ation |       |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | UID   |       |       |       |       |       |       |       |       |       |       |       |       |       |       |
   +-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+
   | Text  | (     | Y     | N     | X     |       |       |       |       |       |       |       |       |       |       |
   | Com   | 4000, |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | ments | 4000) |       |       |       |       |       |       |       |       |       |       |       |       |       |
   +-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+
   | Text  | (     | N     | N     | X     |       |       |       |       |       |       |       |       |       |       |
   | S     | 2030, |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | tring | 0020) |       |       |       |       |       |       |       |       |       |       |       |       |       |
   +-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+
   | Tim   | (     | N     | Y     | X     |       |       |       |       |       | K     | C     |       |       |       |
   | ezone | 0008, |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | O     | 0201) |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | ffset |       |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | From  |       |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | UTC   |       |       |       |       |       |       |       |       |       |       |       |       |       |       |
   +-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+
   | Topic | (     | Y     | N     | X     |       |       |       |       |       |       |       |       |       |       |
   | A     | 0088, |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | uthor | 0910) |       |       |       |       |       |       |       |       |       |       |       |       |       |
   +-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+
   | Topic | (     | Y     | N     | X     |       |       |       |       |       |       |       |       |       |       |
   | Key   | 0088, |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | words | 0912) |       |       |       |       |       |       |       |       |       |       |       |       |       |
   +-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+
   | Topic | (     | Y     | N     | X     |       |       |       |       |       |       |       |       |       |       |
   | Su    | 0088, |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | bject | 0906) |       |       |       |       |       |       |       |       |       |       |       |       |       |
   +-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+
   | Topic | (     | Y     | N     | X     |       |       |       |       |       |       |       |       |       |       |
   | Title | 0088, |       |       |       |       |       |       |       |       |       |       |       |       |       |
   |       | 0904) |       |       |       |       |       |       |       |       |       |       |       |       |       |
   +-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+
   | Tra   | (     | N     | Y     | U     |       | K     |       |       |       |       |       |       |       |       |
   | cking | 0062, |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | UID   | 0021) |       |       |       |       |       |       |       |       |       |       |       |       |       |
   +-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+
   | T     | (     | N     | N     | U     |       | K     |       |       |       |       |       |       |       |       |
   | ransa | 0008, |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | ction | 1195) |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | UID   |       |       |       |       |       |       |       |       |       |       |       |       |       |       |
   +-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+
   | Trea  | (     | N     | Y     | X/D   |       |       |       |       |       | K     | C     |       |       |       |
   | tment | 3008, |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | Date  | 0250) |       |       |       |       |       |       |       |       |       |       |       |       |       |
   +-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+
   | Trea  | (     | N     | Y     | X     |       |       | K     |       |       |       |       |       |       |       |
   | tment | 300A, |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | Ma    | 00B2) |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | chine |       |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | Name  |       |       |       |       |       |       |       |       |       |       |       |       |       |       |
   +-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+
   | Trea  | (     | N     | Y     | D     |       |       |       |       |       |       |       | C     |       |       |
   | tment | 300A, |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | Pos   | 0608) |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | ition |       |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | Group |       |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | Label |       |       |       |       |       |       |       |       |       |       |       |       |       |       |
   +-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+
   | Trea  | (     | N     | Y     | U     |       | K     |       |       |       |       |       |       |       |       |
   | tment | 300A, |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | Pos   | 0609) |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | ition |       |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | Group |       |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | UID   |       |       |       |       |       |       |       |       |       |       |       |       |       |       |
   +-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+
   | Trea  | (     | N     | Y     | U     |       | K     |       |       |       |       |       |       |       |       |
   | tment | 300A, |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | Se    | 0700) |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | ssion |       |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | UID   |       |       |       |       |       |       |       |       |       |       |       |       |       |       |
   +-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+
   | Trea  | (     | N     | Y     | D     |       |       |       |       |       |       |       | C     |       |       |
   | tment | 3010, |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | Site  | 0077) |       |       |       |       |       |       |       |       |       |       |       |       |       |
   +-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+
   | Trea  | (     | N     | Y     | Z     |       |       |       |       |       |       |       | C     |       |       |
   | tment | 3010, |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | Tech  | 007A) |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | nique |       |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | Notes |       |       |       |       |       |       |       |       |       |       |       |       |       |       |
   +-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+
   | Trea  | (     | N     | Y     | X/D   |       |       |       |       |       | K     | C     |       |       |       |
   | tment | 3008, |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | Time  | 0251) |       |       |       |       |       |       |       |       |       |       |       |       |       |
   +-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+
   | Trea  | (     | N     | Y     | D     |       |       |       |       |       | K     | C     |       |       |       |
   | tment | 300A, |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | Tole  | 0736) |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | rance |       |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | Viol  |       |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | ation |       |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | Dat   |       |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | eTime |       |       |       |       |       |       |       |       |       |       |       |       |       |       |
   +-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+
   | Trea  | (     | N     | Y     | D     |       |       |       |       |       |       |       | C     |       |       |
   | tment | 300A, |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | Tole  | 0734) |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | rance |       |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | Viol  |       |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | ation |       |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | D     |       |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | escri |       |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | ption |       |       |       |       |       |       |       |       |       |       |       |       |       |       |
   +-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+
   | UDI   | (     | N     | Y     | X     |       |       | K     |       |       |       |       |       |       |       |
   | Seq   | 0018, |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | uence | 100A) |       |       |       |       |       |       |       |       |       |       |       |       |       |
   +-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+
   | UID   | (     | N     | Y     | U     |       |       |       |       |       |       |       |       |       |       |
   |       | 0040, |       |       |       |       |       |       |       |       |       |       |       |       |       |
   |       | A124) |       |       |       |       |       |       |       |       |       |       |       |       |       |
   +-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+
   | U     | (     | N     | Y     | X     |       |       | K     |       |       |       |       |       |       |       |
   | nique | 0018, |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | D     | 1009) |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | evice |       |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | Ident |       |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | ifier |       |       |       |       |       |       |       |       |       |       |       |       |       |       |
   +-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+
   | User  | (     | N     | Y     | D     |       |       |       |       |       |       |       | C     |       |       |
   | Co    | 3010, |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | ntent | 0033) |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | Label |       |       |       |       |       |       |       |       |       |       |       |       |       |       |
   +-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+
   | User  | (     | N     | Y     | D     |       |       |       |       |       |       |       | C     |       |       |
   | Co    | 3010, |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | ntent | 0034) |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | Long  |       |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | Label |       |       |       |       |       |       |       |       |       |       |       |       |       |       |
   +-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+
   | V     | (     | Y     | N     | X     |       |       |       |       |       |       |       |       |       |       |
   | erbal | 0040, |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | S     | A352) |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | ource |       |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | (T    |       |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | rial) |       |       |       |       |       |       |       |       |       |       |       |       |       |       |
   +-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+
   | V     | (     | Y     | N     | X     |       |       |       |       |       |       |       |       |       |       |
   | erbal | 0040, |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | S     | A358) |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | ource |       |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | Ident |       |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | ifier |       |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | Code  |       |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | Seq   |       |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | uence |       |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | (T    |       |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | rial) |       |       |       |       |       |       |       |       |       |       |       |       |       |       |
   +-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+
   | Veri  | (     | N     | Y     | Z     |       |       |       |       |       |       |       |       |       |       |
   | fying | 0040, |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | Obs   | A088) |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | erver |       |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | Iden  |       |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | tific |       |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | ation |       |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | Code  |       |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | Seq   |       |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | uence |       |       |       |       |       |       |       |       |       |       |       |       |       |       |
   +-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+
   | Veri  | (     | N     | Y     | D     |       |       |       |       |       |       |       |       |       |       |
   | fying | 0040, |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | Obs   | A075) |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | erver |       |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | Name  |       |       |       |       |       |       |       |       |       |       |       |       |       |       |
   +-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+
   | Veri  | (     | N     | Y     | D     |       |       |       |       |       |       |       |       |       |       |
   | fying | 0040, |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | Obs   | A073) |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | erver |       |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | Seq   |       |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | uence |       |       |       |       |       |       |       |       |       |       |       |       |       |       |
   +-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+
   | Veri  | (     | N     | Y     | D     |       |       |       |       |       |       |       |       |       |       |
   | fying | 0040, |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | Or    | A027) |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | ganiz |       |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | ation |       |       |       |       |       |       |       |       |       |       |       |       |       |       |
   +-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+
   | Visit | (     | N     | N     | X     |       |       |       |       |       |       |       | C     |       |       |
   | Com   | 0038, |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | ments | 4000) |       |       |       |       |       |       |       |       |       |       |       |       |       |
   +-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+
   | X-Ray | (     | N     | Y     | D     |       |       | K     |       |       |       |       |       |       |       |
   | Det   | 0018, |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | ector | 9371) |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | ID    |       |       |       |       |       |       |       |       |       |       |       |       |       |       |
   +-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+
   | X-Ray | (     | N     | Y     | X     |       |       | K     |       |       |       |       |       |       |       |
   | Det   | 0018, |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | ector | 9373) |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | Label |       |       |       |       |       |       |       |       |       |       |       |       |       |       |
   +-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+
   | X-Ray | (     | N     | Y     | D     |       |       | K     |       |       |       |       |       |       |       |
   | S     | 0018, |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | ource | 9367) |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | ID    |       |       |       |       |       |       |       |       |       |       |       |       |       |       |
   +-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+

.. _sect_E.1.2:

Re-identifier
~~~~~~~~~~~~~

An Application may claim conformance to an Application Level
Confidentiality Profile as a re-identifier if it is capable of removing
the protection from a protected SOP instance given that the recipient
keys required for the decryption of one or more of the Encrypted Content
(0400,0520) Attributes within the Encrypted Attributes Sequence
(0400,0500) of the SOP instance are available. Removal of protection in
this context is defined as the following process:

1. The application shall decrypt, using its recipient key, one instance
   of the Encrypted Content (0400,0520) Attribute within the Encrypted
   Attributes Sequence (0400,0500) and decode the resulting block of
   bytes into a DICOM dataset using the Transfer Syntax specified in the
   Encrypted Content Transfer Syntax UID (0400,0510). Re-identifiers
   claiming conformance to this profile shall be capable of decrypting
   the Encrypted Content using either AES or Triple-DES in all possible
   key lengths specified in this profile.

   .. note::

      If the application is able to decode more than one instance of the
      Encrypted Content (0400,0520) Attribute within the Encrypted
      Attributes Sequence (0400,0500), it is at the discretion of the
      application to choose any one of them.

2. The application shall move all Attributes contained in the single
   item of the Modified Attributes Sequence (0400,0550) of the decoded
   dataset into the main dataset, replacing "dummy value" Attributes
   that may be present in the main dataset.

   .. note::

      1. Re-identification does not imply a complete reconstruction of
         the original SOP Instance, since it is not required that all
         Attributes being protected be part of the Encrypted Attributes
         Data Set. If the original UIDs are part of the Encrypted
         Attributes Data Set, they might be usable to gain access to the
         original, unprotected SOP Instance.

      2. The presence of an encrypted Data Set that cannot be decrypted
         indicates that some or all of the attribute values in the
         message may not be real (they are dummies). Therefore, the
         recipient must not assume that any value in the message is
         diagnostically relevant.

3. The attribute Patient Identity Removed (0012,0062) shall be replaced
   or added to the dataset with a value of NO and De-identification
   Method (0012,0063) and De-identification Method Code Sequence
   (0012,0064) shall be removed.

.. _sect_E.1.3:

Conformance Requirements
~~~~~~~~~~~~~~~~~~~~~~~~

The Conformance Statement of an application that claims conformance to
an Application Level Confidentiality Profile shall describe:

-  which Attributes are removed during protection;

-  which Attributes are replaced by dummy values and how the dummy
   values are generated;

-  which Attributes are included in Encrypted Attributes Data Sets for
   later re-identification, and any pertinent details about how keys are
   selected for performing the encryption;

-  the scope across which the application is able to ensure referential
   integrity of replacement values for references such as SOP Instance
   UID, Frame of Reference UID, etc. if multiple SOP instances are
   protected (e.g., across multiple Studies, consistent replacement if
   the same Study processed more than once, etc.);

-  which Attributes and Attribute values are inserted during protection
   of a SOP instance;

-  which Transfer Syntaxes are supported for encoding/decoding of the
   Encrypted Attributes Data Set;

-  which Options are supported;

-  any additional restrictions (e. g. key sizes for public keys).

.. _sect_E.2:

Basic Application Level Confidentiality Profile
-----------------------------------------------

This profile is intended for use in clinical trials, and other scenarios
in which de-identification may be required, such as creation of teaching
files, other types of publication, as well as submission of images and
associated information to registries, such as oncology or radiation dose
registries.

This Basic Application Level Confidentiality Profile defines an
extremely conservative approach that removes all information related to:

-  the identity and demographic characteristics of the patient

-  the identity of any responsible parties or family members

-  the identity of any personnel involved in the procedure

-  the identity of the organizations involved in ordering or performing
   the procedure

-  additional information that could be used to match instances if given
   access to the originals, such as UIDs, dates and times

-  private attributes

when that information is present in the non-Pixel Data Attributes,
including graphics or overlays, as described in
`table_title <#table_E.1-1>`__.

.. note::

   Unless the Clean Pixel Data Option is also specified, this profile
   does not address information burned-in to the pixels.

The Attribute Longitudinal Temporal Information Modified (0028,0303)
shall be added to the Dataset with a value of "REMOVED" if none of the
Retain Longitudinal Temporal Information Options is applied.

.. _sect_E.3:

Basic Application Level Confidentiality Options
-----------------------------------------------

Various options are defined to be applicable to the Basic Application
Level Confidentiality Profile. Some of these options require removal of
additional information, and some of these options require retention of
information that would otherwise be removed.

The following options are defined that require removal of additional
information:

-  Clean Pixel Data Option

-  Clean Recognizable Visual Features Option

-  Clean Graphics Option

-  Clean Structured Content Option

-  Clean Descriptors Option

The following options are defined that require retention of information
that would otherwise be removed but that is needed for specific uses:

-  Retain Longitudinal Temporal Information with Full Dates Option

-  Retain Longitudinal Temporal Information with Modified Dates Option

-  Retain Patient Characteristics Option

-  Retain Device Identity Option

-  Retain Institution Identity Option

-  Retain UIDs

-  Retain Safe Private Option

.. _sect_E.3.1:

Clean Pixel Data Option
~~~~~~~~~~~~~~~~~~~~~~~

When this Option is specified in addition to an Application Level
Confidentiality Profile, any information burned in to the Pixel Data
(7FE0,0010) corresponding to the Attribute information specified to be
removed by the Profile and any other Options specified shall also be
removed, as described in `table_title <#table_E.1-1>`__.

This may require intervention of or approval by a human operator.

The Attribute Burned In Annotation (0028,0301) shall be added to the
Dataset with a value of "NO".

.. note::

   1. This capability is called out as a specific option, since it may
      be extremely burdensome in practice to implement and is
      unnecessary for the vast majority of modalities that do not burn
      in such annotation in the first place. For example, CT images do
      not normally contain such burned in annotation, whereas Ultrasound
      images routinely do.

   2. Though image processing and optical character recognition
      techniques can be used to detect the presence of and location of
      burned in text, and matching against known identifying information
      can be applied, deciding whether or not that text is identifying
      information or some other type of information may be non-trivial.
      Compliance with this option requires that identifying information
      is removed, regardless of how that is achieved. It is not required
      that information specified to be retained in the non-pixel data by
      other Options (e.g., physical characteristics, dates or
      descriptors) also be retained burned-in to the pixel data. Thus
      the most conservative approach of removing any and all burned in
      text would be compliant. This may involve sacrificing additional
      potentially useful information such as localizer posting and
      manual graphic annotations.

   3. The stored pixel values are to be changed (blacked out); it is not
      sufficient to superimpose an overlay or graphic annotation or
      shutter to obscure the pixel data values, since those may not be
      ignored by the receiving system.

   4. This option is intended to apply to the Pixel Data (7FE0,0010)
      Attribute that occurs in the top level Dataset of an Image Storage
      SOP Instance. The other standard use of Pixel Data (7FE0,0010) is
      within Icon Image Sequence (0088,0200), which is already described
      in `table_title <#table_E.1-1>`__ and the accompanying note as
      requiring removal. This option does not require the ability to
      manually or automatically process the pixel values of Pixel Data
      (7FE0,0010) occurring in any other location than the top level
      dataset, but it does not prohibit it. Pixel Data (7FE0,0010)
      occurring within private Attributes will be removed because such
      Attributes will not be known to be safe.

.. _sect_E.3.2:

Clean Recognizable Visual Features Option
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

When this Option is specified in addition to an Application Level
Confidentiality Profile, if there is sufficient visual information
within the Pixel Data of a set of instances to allow an individual to be
recognized from the instances themselves or a reconstruction of a set of
instances, then sufficient removal or distortion of the Pixel Data shall
be applied to prevent recognition.

This may require intervention of or approval by a human operator.

The Attribute Recognizable Visual Features (0028,0302) shall be added to
the Dataset with a value of "NO".

.. note::

   1. This capability is called out as a specific option, since it may
      be extremely burdensome in practice to implement and is
      unnecessary for the vast majority of anatomic sites and
      modalities.

   2. In the case of full-face photographs, the risk of visual
      identification is obvious, and numerous techniques are well
      established for de-identification, such as applying black
      rectangles over the eyes, etc.

   3. In the case of high-resolution cross-sectional imaging of the
      entire head and neck, it has been suggested that a 3D volume or
      surface rendering of the pixel data may be sufficient to allow
      identification (or matching against a constrained subset of
      individuals) under some circumstances.

   4. Application of this option may render the pixel data unusable for
      the purpose for which it has been collected, and hence its use may
      require a compromise between de-identification and utility based
      on obtaining appropriate ethical approval and informed consent.
      Consider for example, the case of dental images.

   5. Since the Referenced Patient Photo Sequence is removed as part of
      the Basic Profile, support of the Clean Recognizable Visual
      Features option does not add requirements for that attribute.

.. _sect_E.3.3:

Clean Graphics Option
~~~~~~~~~~~~~~~~~~~~~

Instances of various Standard and Standard Extended SOP Classes,
including Images, Presentation States and other Composite SOP Instances,
may contain identification information encoded as graphics, text
annotations or overlays. This does not include information contained in
Structured Report SOP Classes.

When this Option is specified in addition to an Application Level
Confidentiality Profile, any information encoded in graphics, text
annotations or overlays corresponding to the Attribute information
specified to be removed by the Profile and any other Options specified
shall also be removed, as described in `table_title <#table_E.1-1>`__.

This may require intervention of a human operator.

.. note::

   1. This capability is called out as a specific option, since it may
      be more practical to simply remove all such graphics, text
      annotations or overlays (as required by the profile without this
      option).

   2. As with burned-in pixel data annotation, deciding whether or not
      text is identifying information or some other type of information
      may be non-trivial. It is not required that information specified
      to be retained in the non-pixel data by other Options (e.g.,
      physical characteristics, dates or descriptors) also be retained
      in graphics, text annotations or overlays.

.. _sect_E.3.4:

Clean Structured Content Option
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

Instances of Structured Report SOP Classes may contain identifiable
information in a Content Sequence (0040,A730) encoded in Content Items.
Instances of other SOP Classes may contain structured content encoded in
a similar manner in the Acquisition Context Sequence (0040,0555) or
Specimen Preparation Sequence (0040,0610).

When this Option is specified in addition to an Application Level
Confidentiality Profile, any information encoded in SR Content Items or
Acquisition Context or Specimen Preparation Sequence Items corresponding
to the Attribute information specified to be removed by the Profile and
any other Options specified shall also be removed.

.. note::

   1. For example, the "observer" responsible for a diagnostic imaging
      report may be explicitly identified in Observation Content related
      Content Items in an SR.

   2. A de-identifier that does not implement this option creates
      significant risk when attempting to de-identity a Structured
      Report unless it is only used to de-identify instances that are
      known to have no identifying information in the Content Sequence.

   3. As this Standard and external coding schemes are maintained, the
      codes specified as Concept Name Codes may change. The previous
      codes are considered Retired but implementations may continue to
      send them and de-identifiers will be expected to be able to
      continue to recognize and de-identify Content Items with the
      Retired codes, including the Code Value and Coding Scheme
      Designator, even if the current Standard does not publish them.

      A notable example is the change throughout the Standard from using
      "SNOMED-RT style" code values with a Coding Scheme Designator of
      "SRT", "SNM3" or "99SDM", to the use of SNOMED CT numeric code
      values with a Coding Scheme Designator of "SCT". A mapping of
      retired to new SNOMED codes is found in PS3.16 Annex XXX.

.. table:: Application Level Confidentiality Profile Clean Structured
Content Option Content Item Concept Name Codes

   +-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+
   | *     | *     | **C   | **    | **    | **In  | **    | *     | *     | *     | *     | *     | *     | **    |
   | *Code | *Code | oding | Value | Retd. | Std.  | Basic | *Rtn. | *Rtn. | *Rtn. | *Rtn. | *Rtn. | *Rtn. | Clean |
   | Mean  | Va    | S     | T     | (from | Tpl.  | Pr    | UIDs  | Dev.  | Inst. | Pat.  | Long. | Long. | Desc. |
   | ing** | lue** | cheme | ype** | )**   | (from | of.** | O     | Id.   | Id.   | C     | Full  | M     | O     |
   |       |       | De    |       |       | )**   |       | pt.** | O     | O     | hars. | Dates | odif. | pt.** |
   |       |       | signa |       |       |       |       |       | pt.** | pt.** | O     | O     | Dates |       |
   |       |       | tor** |       |       |       |       |       |       |       | pt.** | pt.** | O     |       |
   |       |       |       |       |       |       |       |       |       |       |       |       | pt.** |       |
   +=======+=======+=======+=======+=======+=======+=======+=======+=======+=======+=======+=======+=======+=======+
   | Acce  | 1     | DCM   | TEXT  | N     | Y     | X     |       |       |       |       |       |       |       |
   | ssion | 21022 |       |       |       |       |       |       |       |       |       |       |       |       |
   | N     |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | umber |       |       |       |       |       |       |       |       |       |       |       |       |       |
   +-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+
   | Acq   | 1     | DCM   | IMAGE | N     | Y     | D     | K     |       |       |       |       |       |       |
   | uired | 13795 |       |       |       |       |       |       |       |       |       |       |       |       |
   | Image |       |       |       |       |       |       |       |       |       |       |       |       |       |
   +-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+
   | A     | 1     | DCM   | DATE  | N     | Y     | X     |       |       |       |       | K     | C     |       |
   | cquis | 26201 |       |       |       |       |       |       |       |       |       |       |       |       |
   | ition |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | Date  |       |       |       |       |       |       |       |       |       |       |       |       |       |
   +-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+
   | A     | 1     | DCM   | TEXT  | N     | Y     | X     |       |       |       |       |       |       | C     |
   | cquis | 25203 |       |       |       |       |       |       |       |       |       |       |       |       |
   | ition |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | Pro   |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | tocol |       |       |       |       |       |       |       |       |       |       |       |       |       |
   +-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+
   | A     | 1     | DCM   | TIME  | N     | Y     | X     |       |       |       |       | K     | C     |       |
   | cquis | 26202 |       |       |       |       |       |       |       |       |       |       |       |       |
   | ition |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | Time  |       |       |       |       |       |       |       |       |       |       |       |       |       |
   +-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+
   | Act   | C     | NCIt  | TEXT  | N     | Y     | X     |       |       |       |       |       |       | C     |
   | ivity | 67447 |       |       |       |       |       |       |       |       |       |       |       |       |
   | Se    |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | ssion |       |       |       |       |       |       |       |       |       |       |       |       |       |
   +-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+
   | Admi  | 4402  | SCT   | TEXT  | N     | Y     | D     |       |       |       |       |       |       | C     |
   | nistr | 52007 |       |       |       |       |       |       |       |       |       |       |       |       |
   | ation |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | of    |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | radi  |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | ophar |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | maceu |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | tical |       |       |       |       |       |       |       |       |       |       |       |       |       |
   +-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+
   | Admi  | 15    | NCDR  | DAT   | N     | Y     | X     |       |       |       |       | K     | C     |       |
   | ssion |       | [     | ETIME |       |       |       |       |       |       |       |       |       |       |
   | Dat   |       | 2.0b] |       |       |       |       |       |       |       |       |       |       |       |
   | eTime |       |       |       |       |       |       |       |       |       |       |       |       |       |
   +-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+
   | Ana   | 1     | DCM   | TEXT  | N     | Y     | X     |       |       |       |       |       |       | C     |
   | tomic | 12050 |       |       |       |       |       |       |       |       |       |       |       |       |
   | Ident |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | ifier |       |       |       |       |       |       |       |       |       |       |       |       |       |
   +-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+
   | Anest | 3981  | SCT   | DAT   | N     | Y     | X     |       |       |       |       | K     | C     |       |
   | hesia | 64008 |       | ETIME |       |       |       |       |       |       |       |       |       |       |
   | F     |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | inish |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | Time  |       |       |       |       |       |       |       |       |       |       |       |       |       |
   +-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+
   | Anest | 3983  | SCT   | DAT   | N     | Y     | X     |       |       |       |       | K     | C     |       |
   | hesia | 25003 |       | ETIME |       |       |       |       |       |       |       |       |       |       |
   | Start |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | Time  |       |       |       |       |       |       |       |       |       |       |       |       |       |
   +-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+
   | Best  | 1     | DCM   | IMAGE | N     | Y     | X     | K     |       |       |       |       |       |       |
   | il    | 21080 |       |       |       |       |       |       |       |       |       |       |       |       |
   | lustr |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | ation |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | of    |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | fi    |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | nding |       |       |       |       |       |       |       |       |       |       |       |       |       |
   +-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+
   | Best  | 1     | DCM   | WAV   | N     | Y     | X     | K     |       |       |       |       |       |       |
   | il    | 21080 |       | EFORM |       |       |       |       |       |       |       |       |       |       |
   | lustr |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | ation |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | of    |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | fi    |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | nding |       |       |       |       |       |       |       |       |       |       |       |       |       |
   +-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+
   | C     | 1     | DCM   | DAT   | N     | Y     | D     |       |       |       |       | K     | C     |       |
   | alibr | 13723 |       | ETIME |       |       |       |       |       |       |       |       |       |       |
   | ation |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | Dat   |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | eTime |       |       |       |       |       |       |       |       |       |       |       |       |       |
   +-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+
   | C     | 1     | DCM   | TEXT  | N     | Y     | X     |       |       |       |       |       |       | C     |
   | alibr | 13720 |       |       |       |       |       |       |       |       |       |       |       |       |
   | ation |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | Pro   |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | tocol |       |       |       |       |       |       |       |       |       |       |       |       |       |
   +-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+
   | C     | 1     | DCM   | TEXT  | N     | Y     | D     |       |       |       |       |       |       | C     |
   | alibr | 13724 |       |       |       |       |       |       |       |       |       |       |       |       |
   | ation |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | R     |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | espon |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | sible |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | Party |       |       |       |       |       |       |       |       |       |       |       |       |       |
   +-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+
   | Cathe | 76    | NCDR  | PNAME | N     | Y     | D     |       |       |       |       |       |       |       |
   | teriz |       | [     |       |       |       |       |       |       |       |       |       |       |       |
   | ation |       | 2.0b] |       |       |       |       |       |       |       |       |       |       |       |
   | Ope   |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | rator |       |       |       |       |       |       |       |       |       |       |       |       |       |
   +-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+
   | Cath  | 1     | DCM   | COMP  | N     | Y     | X     | K     |       |       |       |       |       |       |
   | Lab   | 21120 |       | OSITE |       |       |       |       |       |       |       |       |       |       |
   | Proc  |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | edure |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | Log   |       |       |       |       |       |       |       |       |       |       |       |       |       |
   +-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+
   | Cli   | 3715  | SCT   | COMP  | N     | Y     | X     | K     |       |       |       |       |       |       |
   | nical | 24004 |       | OSITE |       |       |       |       |       |       |       |       |       |       |
   | R     |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | eport |       |       |       |       |       |       |       |       |       |       |       |       |       |
   +-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+
   | Cli   | 3715  | SCT   | TEXT  | N     | Y     | X     |       |       |       |       |       |       | C     |
   | nical | 24004 |       |       |       |       |       |       |       |       |       |       |       |       |
   | R     |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | eport |       |       |       |       |       |       |       |       |       |       |       |       |       |
   +-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+
   | Co    | 1     | DCM   | TEXT  | N     | Y     | X     |       |       |       |       |       |       | C     |
   | mment | 21106 |       |       |       |       |       |       |       |       |       |       |       |       |
   +-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+
   | Co    | 1162  | SCT   | TEXT  | N     | Y     | X     |       |       |       |       |       |       | C     |
   | mplic | 24001 |       |       |       |       |       |       |       |       |       |       |       |       |
   | ation |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | of    |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | Proc  |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | edure |       |       |       |       |       |       |       |       |       |       |       |       |       |
   +-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+
   | Comp  | 1     | DCM   | TEXT  | N     | Y     | D     |       |       |       |       |       |       |       |
   | onent | 12347 |       |       |       |       |       |       |       |       |       |       |       |       |
   | ID    |       |       |       |       |       |       |       |       |       |       |       |       |       |
   +-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+
   | Concl | 1     | DCM   | TEXT  | N     | Y     | X     |       |       |       |       |       |       | C     |
   | usion | 21077 |       |       |       |       |       |       |       |       |       |       |       |       |
   +-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+
   | Co    | 1     | DCM   | DATE  | N     | Y     | X/D   |       |       |       |       | K     | C     |       |
   | ntent | 11018 |       |       |       |       |       |       |       |       |       |       |       |       |
   | Date  |       |       |       |       |       |       |       |       |       |       |       |       |       |
   +-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+
   | Co    | 1     | DCM   | TIME  | N     | Y     | X/D   |       |       |       |       | K     | C     |       |
   | ntent | 11019 |       |       |       |       |       |       |       |       |       |       |       |       |
   | Time  |       |       |       |       |       |       |       |       |       |       |       |       |       |
   +-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+
   | Cu    | 1     | DCM   | COMP  | N     | Y     | X     | K     |       |       |       |       |       |       |
   | rrent | 22073 |       | OSITE |       |       |       |       |       |       |       |       |       |       |
   | proc  |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | edure |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | evi   |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | dence |       |       |       |       |       |       |       |       |       |       |       |       |       |
   +-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+
   | Date  | 11    | LN    | DATE  | N     | Y     | X     |       |       |       |       | K     | C     |       |
   | of    | 955-2 |       |       |       |       |       |       |       |       |       |       |       |       |
   | last  |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | mens  |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | trual |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | p     |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | eriod |       |       |       |       |       |       |       |       |       |       |       |       |       |
   +-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+
   | Dat   | 1     | DCM   | DAT   | N     | Y     | X     |       |       |       |       | K     | C     |       |
   | eTime | 21431 |       | ETIME |       |       |       |       |       |       |       |       |       |       |
   | Co    |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | ncern |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | Noted |       |       |       |       |       |       |       |       |       |       |       |       |       |
   +-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+
   | Dat   | 1     | DCM   | DAT   | N     | Y     | X     |       |       |       |       | K     | C     |       |
   | eTime | 21432 |       | ETIME |       |       |       |       |       |       |       |       |       |       |
   | Co    |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | ncern |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | Res   |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | olved |       |       |       |       |       |       |       |       |       |       |       |       |       |
   +-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+
   | Dat   | 1     | DCM   | DAT   | N     | Y     | X     |       |       |       |       | K     | C     |       |
   | eTime | 11527 |       | ETIME |       |       |       |       |       |       |       |       |       |       |
   | Ended |       |       |       |       |       |       |       |       |       |       |       |       |       |
   +-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+
   | Dat   | 1     | DCM   | DAT   | N     | Y     | X     |       |       |       |       | K     | C     |       |
   | eTime | 22165 |       | ETIME |       |       |       |       |       |       |       |       |       |       |
   | of    |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | Death |       |       |       |       |       |       |       |       |       |       |       |       |       |
   +-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+
   | Dat   | 1     | DCM   | DAT   | N     | Y     | X     |       |       |       |       | K     | C     |       |
   | eTime | 22105 |       | ETIME |       |       |       |       |       |       |       |       |       |       |
   | of    |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | In    |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | terve |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | ntion |       |       |       |       |       |       |       |       |       |       |       |       |       |
   +-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+
   | Dat   | 1     | DCM   | DAT   | N     | Y     | X     |       |       |       |       | K     | C     |       |
   | eTime | 11536 |       | ETIME |       |       |       |       |       |       |       |       |       |       |
   | of    |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | last  |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | evalu |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | ation |       |       |       |       |       |       |       |       |       |       |       |       |       |
   +-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+
   | Dat   | 1     | DCM   | DAT   | N     | Y     | X     |       |       |       |       | K     | C     |       |
   | eTime | 11702 |       | ETIME |       |       |       |       |       |       |       |       |       |       |
   | of    |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | proce |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | ssing |       |       |       |       |       |       |       |       |       |       |       |       |       |
   +-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+
   | Dat   | 1     | DCM   | DAT   | N     | Y     | X     |       |       |       |       | K     | C     |       |
   | eTime | 21125 |       | ETIME |       |       |       |       |       |       |       |       |       |       |
   | of    |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | Reco  |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | rding |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | of    |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | Log   |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | Entry |       |       |       |       |       |       |       |       |       |       |       |       |       |
   +-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+
   | Dat   | 1     | DCM   | DAT   | N     | Y     | X     |       |       |       |       | K     | C     |       |
   | eTime | 11535 |       | ETIME |       |       |       |       |       |       |       |       |       |       |
   | pr    |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | oblem |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | obs   |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | erved |       |       |       |       |       |       |       |       |       |       |       |       |       |
   +-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+
   | Dat   | 1     | DCM   | DAT   | N     | Y     | X     |       |       |       |       | K     | C     |       |
   | eTime | 21433 |       | ETIME |       |       |       |       |       |       |       |       |       |       |
   | Pr    |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | oblem |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | Res   |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | olved |       |       |       |       |       |       |       |       |       |       |       |       |       |
   +-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+
   | Dat   | 1     | DCM   | DAT   | N     | Y     | X/D   |       |       |       |       | K     | C     |       |
   | eTime | 11526 |       | ETIME |       |       |       |       |       |       |       |       |       |       |
   | St    |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | arted |       |       |       |       |       |       |       |       |       |       |       |       |       |
   +-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+
   | D     | 1     | DCM   | TEXT  | N     | Y     | D     |       |       |       |       |       |       |       |
   | egree | 12363 |       |       |       |       |       |       |       |       |       |       |       |       |
   | of    |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | Fr    |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | eedom |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | ID    |       |       |       |       |       |       |       |       |       |       |       |       |       |
   +-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+
   | De    | 1     | DCM   | U     | N     | Y     | D     | K     |       |       |       |       |       |       |
   | rived | 12357 |       | IDREF |       |       |       |       |       |       |       |       |       |       |
   | Fid   |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | ucial |       |       |       |       |       |       |       |       |       |       |       |       |       |
   +-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+
   | De    | 1     | DCM   | COMP  | N     | Y     | X     | K     |       |       |       |       |       |       |
   | rived | 12373 |       | OSITE |       |       |       |       |       |       |       |       |       |       |
   | Pla   |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | nning |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | Data  |       |       |       |       |       |       |       |       |       |       |       |       |       |
   +-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+
   | De    | 1     | DCM   | COMP  | N     | Y     | X     | K     |       |       |       |       |       |       |
   | rived | 12372 |       | OSITE |       |       |       |       |       |       |       |       |       |       |
   | Pla   |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | nning |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | I     |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | mages |       |       |       |       |       |       |       |       |       |       |       |       |       |
   +-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+
   | D     | 1     | DCM   | TEXT  | N     | Y     | X     |       |       |       |       |       |       | C     |
   | escri | 11021 |       |       |       |       |       |       |       |       |       |       |       |       |
   | ption |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | of    |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | C     |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | hange |       |       |       |       |       |       |       |       |       |       |       |       |       |
   +-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+
   | D     | 1     | DCM   | TEXT  | N     | Y     | X     |       |       |       |       |       |       | C     |
   | escri | 21145 |       |       |       |       |       |       |       |       |       |       |       |       |
   | ption |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | of    |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | Mat   |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | erial |       |       |       |       |       |       |       |       |       |       |       |       |       |
   +-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+
   | D     | 1     | DCM   | TEXT  | N     | Y     | X     |       | K     |       |       |       |       |       |
   | evice | 20999 |       |       |       |       |       |       |       |       |       |       |       |       |
   | D     |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | escri |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | ption |       |       |       |       |       |       |       |       |       |       |       |       |       |
   +-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+
   | D     | 1     | DCM   | TEXT  | N     | Y     | X     |       | K     |       |       |       |       |       |
   | evice | 13877 |       |       |       |       |       |       |       |       |       |       |       |       |
   | Name  |       |       |       |       |       |       |       |       |       |       |       |       |       |
   +-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+
   | D     | 1     | DCM   | TEXT  | N     | Y     | X     |       | K     |       |       |       |       |       |
   | evice | 21013 |       |       |       |       |       |       |       |       |       |       |       |       |
   | Obs   |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | erver |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | Name  |       |       |       |       |       |       |       |       |       |       |       |       |       |
   +-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+
   | D     | 1     | DCM   | TEXT  | N     | Y     | X     |       |       | K     |       |       |       |       |
   | evice | 21017 |       |       |       |       |       |       |       |       |       |       |       |       |
   | Obs   |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | erver |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | Phy   |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | sical |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | Loc   |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | ation |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | D     |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | uring |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | O     |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | bserv |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | ation |       |       |       |       |       |       |       |       |       |       |       |       |       |
   +-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+
   | D     | 1     | DCM   | TEXT  | N     | Y     | X     |       | K     |       |       |       |       |       |
   | evice | 21016 |       |       |       |       |       |       |       |       |       |       |       |       |
   | Obs   |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | erver |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | S     |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | erial |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | N     |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | umber |       |       |       |       |       |       |       |       |       |       |       |       |       |
   +-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+
   | D     | 1     | DCM   | U     | N     | Y     | X/D   | K     | K     |       |       |       |       |       |
   | evice | 21012 |       | IDREF |       |       |       |       |       |       |       |       |       |       |
   | Obs   |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | erver |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | UID   |       |       |       |       |       |       |       |       |       |       |       |       |       |
   +-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+
   | D     | 1     | DCM   | TEXT  | N     | Y     | X/D   |       | K     |       |       |       |       |       |
   | evice | 13880 |       |       |       |       |       |       |       |       |       |       |       |       |
   | S     |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | erial |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | N     |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | umber |       |       |       |       |       |       |       |       |       |       |       |       |       |
   +-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+
   | D     | 1     | DCM   | TEXT  | N     | Y     | D     |       | K     |       |       |       |       |       |
   | evice | 21193 |       |       |       |       |       |       |       |       |       |       |       |       |
   | Su    |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | bject |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | Name  |       |       |       |       |       |       |       |       |       |       |       |       |       |
   +-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+
   | D     | 1     | DCM   | TEXT  | N     | Y     | X     |       |       | K     |       |       |       |       |
   | evice | 21197 |       |       |       |       |       |       |       |       |       |       |       |       |
   | Su    |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | bject |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | Phy   |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | sical |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | Loc   |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | ation |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | d     |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | uring |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | o     |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | bserv |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | ation |       |       |       |       |       |       |       |       |       |       |       |       |       |
   +-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+
   | D     | 1     | DCM   | TEXT  | N     | Y     | X     |       | K     |       |       |       |       |       |
   | evice | 21196 |       |       |       |       |       |       |       |       |       |       |       |       |
   | Su    |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | bject |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | S     |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | erial |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | N     |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | umber |       |       |       |       |       |       |       |       |       |       |       |       |       |
   +-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+
   | D     | 1     | DCM   | U     | N     | Y     | X     | K     | K     |       |       |       |       |       |
   | evice | 21198 |       | IDREF |       |       |       |       |       |       |       |       |       |       |
   | Su    |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | bject |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | UID   |       |       |       |       |       |       |       |       |       |       |       |       |       |
   +-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+
   | Disc  | 1     | DCM   | DAT   | N     | Y     | X     |       |       |       |       | K     | C     |       |
   | harge | 22163 |       | ETIME |       |       |       |       |       |       |       |       |       |       |
   | Dat   |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | eTime |       |       |       |       |       |       |       |       |       |       |       |       |       |
   +-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+
   | Dose  | 1     | DCM   | IMAGE | N     | Y     | X     | K     |       |       |       |       |       |       |
   | Image | 21342 |       |       |       |       |       |       |       |       |       |       |       |       |
   +-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+
   | Drug  | 1     | DCM   | TEXT  | N     | Y     | X/D   |       |       |       |       |       |       | C     |
   | ad    | 22083 |       |       |       |       |       |       |       |       |       |       |       |       |
   | minis |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | tered |       |       |       |       |       |       |       |       |       |       |       |       |       |
   +-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+
   | Drug  | 1     | DCM   | DAT   | N     | Y     | X     |       |       |       |       | K     | C     |       |
   | end   | 22082 |       | ETIME |       |       |       |       |       |       |       |       |       |       |
   +-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+
   | Drug  | 1     | DCM   | DAT   | N     | Y     | X     |       |       |       |       | K     | C     |       |
   | start | 22081 |       | ETIME |       |       |       |       |       |       |       |       |       |       |
   +-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+
   | ECG   | 2719  | SCT   | TEXT  | N     | Y     | X/D   |       |       |       |       |       |       | C     |
   | Fi    | 21002 |       |       |       |       |       |       |       |       |       |       |       |       |
   | nding |       |       |       |       |       |       |       |       |       |       |       |       |       |
   +-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+
   | EDD   | 11    | LN    | DATE  | N     | Y     | X     |       |       |       |       | K     | C     |       |
   |       | 778-8 |       |       |       |       |       |       |       |       |       |       |       |       |
   +-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+
   | End   | 1     | DCM   | DAT   | N     | Y     | D     |       |       |       |       | K     | C     |       |
   | of    | 13810 |       | ETIME |       |       |       |       |       |       |       |       |       |       |
   | X-Ray |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | I     |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | rradi |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | ation |       |       |       |       |       |       |       |       |       |       |       |       |       |
   +-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+
   | Equi  | 1     | DCM   | TEXT  | N     | Y     | X     |       | K     |       |       |       |       | C     |
   | pment | 21122 |       |       |       |       |       |       |       |       |       |       |       |       |
   | Iden  |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | tific |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | ation |       |       |       |       |       |       |       |       |       |       |       |       |       |
   +-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+
   | Event | 1     | DCM   | U     | N     | Y     | D     | K     |       |       |       |       |       |       |
   | UID   | 28429 |       | IDREF |       |       |       |       |       |       |       |       |       |       |
   | Used  |       |       |       |       |       |       |       |       |       |       |       |       |       |
   +-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+
   | F     | 1     | DCM   | PNAME | N     | Y     | X     |       |       |       |       |       |       |       |
   | ellow | 21088 |       |       |       |       |       |       |       |       |       |       |       |       |
   +-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+
   | Fetus | 11    | LN    | TEXT  | N     | Y     | D     |       |       |       |       |       |       |       |
   | ID    | 951-1 |       |       |       |       |       |       |       |       |       |       |       |       |
   +-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+
   | F     | 1     | DCM   | TEXT  | N     | Y     | X     |       |       |       |       |       |       |       |
   | iller | 21021 |       |       |       |       |       |       |       |       |       |       |       |       |
   | N     |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | umber |       |       |       |       |       |       |       |       |       |       |       |       |       |
   +-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+
   | Fi    | 1     | DCM   | TEXT  | N     | Y     | X/D   |       |       |       |       |       |       | C     |
   | nding | 21071 |       |       |       |       |       |       |       |       |       |       |       |       |
   +-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+
   | Fi    | 3636  | SCT   | TEXT  | N     | Y     | D     |       |       |       |       |       |       | C     |
   | nding | 98007 |       |       |       |       |       |       |       |       |       |       |       |       |
   | Site  |       |       |       |       |       |       |       |       |       |       |       |       |       |
   +-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+
   | Frame | 1     | DCM   | U     | N     | Y     | X/D   | K     |       |       |       |       |       |       |
   | of    | 12227 |       | IDREF |       |       |       |       |       |       |       |       |       |       |
   | Refe  |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | rence |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | UID   |       |       |       |       |       |       |       |       |       |       |       |       |       |
   +-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+
   | Gl    | 1     | DCM   | DATE  | N     | Y     | D     |       |       |       |       | K     | C     |       |
   | ucose | 27857 |       |       |       |       |       |       |       |       |       |       |       |       |
   | M     |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | easur |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | ement |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | Date  |       |       |       |       |       |       |       |       |       |       |       |       |       |
   +-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+
   | Gl    | 1     | DCM   | TIME  | N     | Y     | D     |       |       |       |       | K     | C     |       |
   | ucose | 27858 |       |       |       |       |       |       |       |       |       |       |       |       |
   | M     |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | easur |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | ement |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | Time  |       |       |       |       |       |       |       |       |       |       |       |       |       |
   +-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+
   | Hi    | 11    | LN    | TEXT  | N     | Y     | X     |       |       |       |       |       |       | C     |
   | story | 329-0 |       |       |       |       |       |       |       |       |       |       |       |       |
   +-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+
   | Iden  | 1     | DCM   | TEXT  | N     | Y     | D     |       | K     |       |       |       |       |       |
   | tific | 13832 |       |       |       |       |       |       |       |       |       |       |       |       |
   | ation |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | of    |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | the   |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | X-Ray |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | S     |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | ource |       |       |       |       |       |       |       |       |       |       |       |       |       |
   +-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+
   | Ident | 1     | DCM   | TEXT  | N     | Y     | X     |       |       |       |       |       |       |       |
   | ifier | 25010 |       |       |       |       |       |       |       |       |       |       |       |       |
   +-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+
   | Ident | 1     | DCM   | TEXT  | N     | Y     | X     |       |       |       |       |       |       |       |
   | ifier | 28775 |       |       |       |       |       |       |       |       |       |       |       |       |
   | w     |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | ithin |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | P     |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | erson |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | Obser |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | ver's |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | Role  |       |       |       |       |       |       |       |       |       |       |       |       |       |
   +-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+
   | I     | 1     | DCM   | IMAGE | N     | Y     | D     | K     |       |       |       |       |       |       |
   | denti | 12229 |       |       |       |       |       |       |       |       |       |       |       |       |
   | fying |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | Se    |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | gment |       |       |       |       |       |       |       |       |       |       |       |       |       |
   +-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+
   | Il    | 1     | DCM   | IMAGE | N     | Y     | X     | K     |       |       |       |       |       |       |
   | lustr | 25201 |       |       |       |       |       |       |       |       |       |       |       |       |
   | ation |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | of    |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | Fi    |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | nding |       |       |       |       |       |       |       |       |       |       |       |       |       |
   +-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+
   | Il    | 1     | DCM   | IMAGE | N     | Y     | X     | K     |       |       |       |       |       |       |
   | lustr | 21200 |       |       |       |       |       |       |       |       |       |       |       |       |
   | ation |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | of    |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | ROI   |       |       |       |       |       |       |       |       |       |       |       |       |       |
   +-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+
   | Image | 1     | DCM   | IMAGE | N     | Y     | D     | K     |       |       |       |       |       |       |
   | Acq   | 21138 |       |       |       |       |       |       |       |       |       |       |       |       |
   | uired |       |       |       |       |       |       |       |       |       |       |       |       |       |
   +-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+
   | Im    | 1     | DCM   | DAT   | N     | Y     | D     |       |       |       |       | K     | C     |       |
   | aging | 22712 |       | ETIME |       |       |       |       |       |       |       |       |       |       |
   | Start |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | Dat   |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | eTime |       |       |       |       |       |       |       |       |       |       |       |       |       |
   +-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+
   | Im    | 1     | DCM   | COMP  | N     | Y     | X     | K     |       |       |       |       |       |       |
   | plant | 12366 |       | OSITE |       |       |       |       |       |       |       |       |       |       |
   | Ass   |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | embly |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | Tem   |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | plate |       |       |       |       |       |       |       |       |       |       |       |       |       |
   +-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+
   | Impre | 1     | DCM   | TEXT  | N     | Y     | D     |       |       |       |       |       |       | C     |
   | ssion | 11033 |       |       |       |       |       |       |       |       |       |       |       |       |
   | D     |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | escri |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | ption |       |       |       |       |       |       |       |       |       |       |       |       |       |
   +-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+
   | I     | 18    | LN    | TEXT  | N     | Y     | D     |       |       |       |       |       |       | C     |
   | ndica | 785-6 |       |       |       |       |       |       |       |       |       |       |       |       |
   | tions |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | for   |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | Proc  |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | edure |       |       |       |       |       |       |       |       |       |       |       |       |       |
   +-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+
   | In    | 1     | DCM   | TEXT  | N     | Y     | D     |       |       |       |       |       |       |       |
   | terve | 21154 |       |       |       |       |       |       |       |       |       |       |       |       |
   | ntion |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | at    |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | tempt |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | ident |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | ifier |       |       |       |       |       |       |       |       |       |       |       |       |       |
   +-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+
   | I     | 1     | DCM   | PNAME | N     | Y     | D     |       |       |       |       |       |       |       |
   | rradi | 13850 |       |       |       |       |       |       |       |       |       |       |       |       |
   | ation |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | A     |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | uthor |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | izing |       |       |       |       |       |       |       |       |       |       |       |       |       |
   +-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+
   | I     | 1     | DCM   | TEXT  | N     | Y     | X     |       |       |       |       |       |       |       |
   | rradi | 13605 |       |       |       |       |       |       |       |       |       |       |       |       |
   | ation |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | Event |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | Label |       |       |       |       |       |       |       |       |       |       |       |       |       |
   +-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+
   | I     | 1     | DCM   | U     | N     | Y     | D     | K     |       |       |       |       |       |       |
   | rradi | 13769 |       | IDREF |       |       |       |       |       |       |       |       |       |       |
   | ation |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | Event |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | UID   |       |       |       |       |       |       |       |       |       |       |       |       |       |
   +-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+
   | I     | 1     | DCM   | TEXT  | N     | Y     | X     |       |       |       |       |       |       |       |
   | ssuer | 10190 |       |       |       |       |       |       |       |       |       |       |       |       |
   | of    |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | Ident |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | ifier |       |       |       |       |       |       |       |       |       |       |       |       |       |
   +-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+
   | I     | 1     | DCM   | TEXT  | N     | Y     | X     |       |       |       |       |       |       |       |
   | ssuer | 11706 |       |       |       |       |       |       |       |       |       |       |       |       |
   | of    |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | P     |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | arent |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | Spe   |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | cimen |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | Ident |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | ifier |       |       |       |       |       |       |       |       |       |       |       |       |       |
   +-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+
   | I     | 1     | DCM   | TEXT  | N     | Y     | X     |       |       |       |       |       |       |       |
   | ssuer | 11724 |       |       |       |       |       |       |       |       |       |       |       |       |
   | of    |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | Spe   |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | cimen |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | Ident |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | ifier |       |       |       |       |       |       |       |       |       |       |       |       |       |
   +-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+
   | Key   | 1     | DCM   | TEXT  | N     | Y     | X     |       |       |       |       |       |       | C     |
   | O     | 13012 |       |       |       |       |       |       |       |       |       |       |       |       |
   | bject |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | D     |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | escri |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | ption |       |       |       |       |       |       |       |       |       |       |       |       |       |
   +-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+
   | LV    | 18    | LN    | TEXT  | N     | Y     | X     |       |       |       |       |       |       | C     |
   | Wall  | 118-0 |       |       |       |       |       |       |       |       |       |       |       |       |
   | M     |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | otion |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | Segm  |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | ental |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | Fin   |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | dings |       |       |       |       |       |       |       |       |       |       |       |       |       |
   +-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+
   | Ma    | 1     | DCM   | COMP  | N     | Y     | D     | K     |       |       |       |       |       |       |
   | nufac | 12371 |       | OSITE |       |       |       |       |       |       |       |       |       |       |
   | turer |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | Im    |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | plant |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | Tem   |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | plate |       |       |       |       |       |       |       |       |       |       |       |       |       |
   +-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+
   | M     | 1     | DCM   | TEXT  | N     | Y     | D     |       |       |       |       |       |       |       |
   | ating | 12352 |       |       |       |       |       |       |       |       |       |       |       |       |
   | Fe    |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | ature |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | ID    |       |       |       |       |       |       |       |       |       |       |       |       |       |
   +-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+
   | M     | 1     | DCM   | TEXT  | N     | Y     | D     |       |       |       |       |       |       |       |
   | ating | 12351 |       |       |       |       |       |       |       |       |       |       |       |       |
   | Fe    |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | ature |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | Set   |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | ID    |       |       |       |       |       |       |       |       |       |       |       |       |       |
   +-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+
   | Medic | 1     | DCM   | TEXT  | N     | Y     | X     |       |       |       |       |       |       | C     |
   | ation | 11516 |       |       |       |       |       |       |       |       |       |       |       |       |
   | Type  |       |       |       |       |       |       |       |       |       |       |       |       |       |
   +-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+
   | M     | 1     | DCM   | PNAME | N     | Y     | X     |       |       |       |       |       |       |       |
   | other | 21036 |       |       |       |       |       |       |       |       |       |       |       |       |
   | of    |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | fetus |       |       |       |       |       |       |       |       |       |       |       |       |       |
   +-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+
   | Or    | 1     | DCM   | TEXT  | N     | Y     | X     |       |       | K     |       |       |       |       |
   | ganiz | 13873 |       |       |       |       |       |       |       |       |       |       |       |       |
   | ation |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | Name  |       |       |       |       |       |       |       |       |       |       |       |       |       |
   +-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+
   | Ori   | 1     | DCM   | COMP  | N     | Y     | D     | K     |       |       |       |       |       |       |
   | ginal | 11040 |       | OSITE |       |       |       |       |       |       |       |       |       |       |
   | S     |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | ource |       |       |       |       |       |       |       |       |       |       |       |       |       |
   +-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+
   | P     | 1     | DCM   | TEXT  | N     | Y     | D     |       |       |       |       |       |       |       |
   | arent | 11705 |       |       |       |       |       |       |       |       |       |       |       |       |
   | Spe   |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | cimen |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | Ident |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | ifier |       |       |       |       |       |       |       |       |       |       |       |       |       |
   +-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+
   | Pa    | 1     | DCM   | COMP  | N     | Y     | X     | K     |       |       |       |       |       |       |
   | tient | 12361 |       | OSITE |       |       |       |       |       |       |       |       |       |       |
   | Data  |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | Used  |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | D     |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | uring |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | Pla   |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | nning |       |       |       |       |       |       |       |       |       |       |       |       |       |
   +-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+
   | Pa    | 1     | DCM   | IMAGE | N     | Y     | X     | K     |       |       |       |       |       |       |
   | tient | 12354 |       |       |       |       |       |       |       |       |       |       |       |       |
   | Image |       |       |       |       |       |       |       |       |       |       |       |       |       |
   +-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+
   | Pa    | 1     | DCM   | TEXT  | N     | Y     | D     |       |       |       |       |       |       | C     |
   | tient | 13815 |       |       |       |       |       |       |       |       |       |       |       |       |
   | Model |       |       |       |       |       |       |       |       |       |       |       |       |       |
   +-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+
   | Pa    | 1     | DCM   | TEXT  | N     | Y     | X     |       |       |       |       |       |       | C     |
   | tient | 21110 |       |       |       |       |       |       |       |       |       |       |       |       |
   | Pr    |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | esent |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | ation |       |       |       |       |       |       |       |       |       |       |       |       |       |
   +-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+
   | Pa    | 1     | DCM   | COMP  | N     | Y     | X     | K     |       |       |       |       |       |       |
   | tient | 28425 |       | OSITE |       |       |       |       |       |       |       |       |       |       |
   | Radi  |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | ation |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | Dose  |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | Model |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | Data  |       |       |       |       |       |       |       |       |       |       |       |       |       |
   +-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+
   | Pa    | 1     | DCM   | IMAGE | N     | Y     | X     | K     |       |       |       |       |       |       |
   | tient | 28425 |       |       |       |       |       |       |       |       |       |       |       |       |
   | Radi  |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | ation |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | Dose  |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | Model |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | Data  |       |       |       |       |       |       |       |       |       |       |       |       |       |
   +-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+
   | Pa    | 1     | DCM   | U     | N     | Y     | X     | K     |       |       |       |       |       |       |
   | tient | 28425 |       | IDREF |       |       |       |       |       |       |       |       |       |       |
   | Radi  |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | ation |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | Dose  |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | Model |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | Data  |       |       |       |       |       |       |       |       |       |       |       |       |       |
   +-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+
   | Pa    | 1     | DCM   | TEXT  | N     | Y     | X     |       |       |       |       |       |       | C     |
   | tient | 28426 |       |       |       |       |       |       |       |       |       |       |       |       |
   | Radi  |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | ation |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | Dose  |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | Model |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | Refe  |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | rence |       |       |       |       |       |       |       |       |       |       |       |       |       |
   +-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+
   | Pa    | 1     | DCM   | TEXT  | N     | Y     | X     |       |       |       |       |       |       | C     |
   | tient | 09054 |       |       |       |       |       |       |       |       |       |       |       |       |
   | State |       |       |       |       |       |       |       |       |       |       |       |       |       |
   +-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+
   | Pa    | 1     | DCM   | TEXT  | N     | Y     | X     |       |       | K     |       |       |       |       |
   | tient | 22128 |       |       |       |       |       |       |       |       |       |       |       |       |
   | T     |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | ransf |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | erred |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | From  |       |       |       |       |       |       |       |       |       |       |       |       |       |
   +-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+
   | Perf  | 1     | DCM   | U     | N     | Y     | D     | K     |       |       |       |       |       |       |
   | ormed | 21126 |       | IDREF |       |       |       |       |       |       |       |       |       |       |
   | Proc  |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | edure |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | Step  |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | SOP   |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | Ins   |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | tance |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | UID   |       |       |       |       |       |       |       |       |       |       |       |       |       |
   +-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+
   | Perfo | 1     | DCM   | PNAME | N     | Y     | D     |       |       |       |       |       |       |       |
   | rming | 21114 |       |       |       |       |       |       |       |       |       |       |       |       |
   | Phys  |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | ician |       |       |       |       |       |       |       |       |       |       |       |       |       |
   +-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+
   | P     | 1     | DCM   | PNAME | N     | Y     | X     |       |       |       |       |       |       |       |
   | erson | 21152 |       |       |       |       |       |       |       |       |       |       |       |       |
   | adm   |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | inist |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | ering |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | dru   |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | g/con |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | trast |       |       |       |       |       |       |       |       |       |       |       |       |       |
   +-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+
   | P     | 1     | DCM   | TEXT  | N     | Y     | X     |       |       |       |       |       |       |       |
   | erson | 13871 |       |       |       |       |       |       |       |       |       |       |       |       |
   | ID    |       |       |       |       |       |       |       |       |       |       |       |       |       |
   +-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+
   | P     | 1     | DCM   | TEXT  | N     | Y     | X     |       |       |       |       |       |       |       |
   | erson | 13872 |       |       |       |       |       |       |       |       |       |       |       |       |
   | ID    |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | I     |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | ssuer |       |       |       |       |       |       |       |       |       |       |       |       |       |
   +-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+
   | P     | 1     | DCM   | PNAME | N     | Y     | D     |       |       |       |       |       |       |       |
   | erson | 13870 |       |       |       |       |       |       |       |       |       |       |       |       |
   | Name  |       |       |       |       |       |       |       |       |       |       |       |       |       |
   +-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+
   | P     | 1     | DCM   | TEXT  | N     | Y     | X     |       |       |       |       |       |       |       |
   | erson | 28774 |       |       |       |       |       |       |       |       |       |       |       |       |
   | Obser |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | ver's |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | Login |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | Name  |       |       |       |       |       |       |       |       |       |       |       |       |       |
   +-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+
   | P     | 1     | DCM   | TEXT  | N     | Y     | X     |       |       | K     |       |       |       |       |
   | erson | 21009 |       |       |       |       |       |       |       |       |       |       |       |       |
   | Obser |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | ver's |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | Or    |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | ganiz |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | ation |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | Name  |       |       |       |       |       |       |       |       |       |       |       |       |       |
   +-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+
   | P     | 1     | DCM   | PNAME | N     | Y     | D     |       |       |       |       |       |       |       |
   | erson | 21008 |       |       |       |       |       |       |       |       |       |       |       |       |
   | Obs   |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | erver |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | Name  |       |       |       |       |       |       |       |       |       |       |       |       |       |
   +-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+
   | Phys  | 1     | DCM   | TEXT  | N     | Y     | X     |       |       |       |       |       |       | C     |
   | ician | 21173 |       |       |       |       |       |       |       |       |       |       |       |       |
   | Note  |       |       |       |       |       |       |       |       |       |       |       |       |       |
   +-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+
   | P     | 1     | DCM   | TEXT  | N     | Y     | X     |       |       |       |       |       |       |       |
   | lacer | 21020 |       |       |       |       |       |       |       |       |       |       |       |       |
   | N     |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | umber |       |       |       |       |       |       |       |       |       |       |       |       |       |
   +-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+
   | Pr    | 1     | DCM   | TEXT  | N     | Y     | X     |       |       |       |       |       |       |       |
   | escri | 13516 |       |       |       |       |       |       |       |       |       |       |       |       |
   | ption |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | Ident |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | ifier |       |       |       |       |       |       |       |       |       |       |       |       |       |
   +-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+
   | Prior | 1     | DCM   | COMP  | N     | Y     | X     | K     |       |       |       |       |       |       |
   | r     | 22075 |       | OSITE |       |       |       |       |       |       |       |       |       |       |
   | eport |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | for   |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | cu    |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | rrent |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | pa    |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | tient |       |       |       |       |       |       |       |       |       |       |       |       |       |
   +-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+
   | Proc  | 1     | DCM   | TEXT  | N     | Y     | X/D   |       |       |       |       |       |       |       |
   | edure | 21124 |       |       |       |       |       |       |       |       |       |       |       |       |
   | A     |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | ction |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | ID    |       |       |       |       |       |       |       |       |       |       |       |       |       |
   +-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+
   | Proc  | 1     | DCM   | DAT   | N     | Y     | X/D   |       |       |       |       | K     | C     |       |
   | edure | 22146 |       | ETIME |       |       |       |       |       |       |       |       |       |       |
   | Dat   |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | eTime |       |       |       |       |       |       |       |       |       |       |       |       |       |
   +-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+
   | Proc  | 52    | NCDR  | DAT   | N     | Y     | D     |       |       |       |       | K     | C     |       |
   | edure |       | [     | ETIME |       |       |       |       |       |       |       |       |       |       |
   | Dat   |       | 2.0b] |       |       |       |       |       |       |       |       |       |       |       |
   | eTime |       |       |       |       |       |       |       |       |       |       |       |       |       |
   +-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+
   | Proc  | 1     | DCM   | TEXT  | N     | Y     | X/D   |       |       |       |       |       |       | C     |
   | edure | 21065 |       |       |       |       |       |       |       |       |       |       |       |       |
   | D     |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | escri |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | ption |       |       |       |       |       |       |       |       |       |       |       |       |       |
   +-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+
   | Proc  | 53    | NCDR  | TEXT  | N     | Y     | X     |       |       |       |       |       |       |       |
   | edure |       | [     |       |       |       |       |       |       |       |       |       |       |       |
   | N     |       | 2.0b] |       |       |       |       |       |       |       |       |       |       |       |
   | umber |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | in    |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | this  |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | admi  |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | ssion |       |       |       |       |       |       |       |       |       |       |       |       |       |
   +-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+
   | Proc  | 1     | DCM   | TEXT  | N     | Y     | X     |       |       |       |       |       |       | C     |
   | edure | 22177 |       |       |       |       |       |       |       |       |       |       |       |       |
   | R     |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | esult |       |       |       |       |       |       |       |       |       |       |       |       |       |
   +-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+
   | Proc  | 1     | DCM   | U     | N     | Y     | X     | K     |       |       |       |       |       |       |
   | edure | 21019 |       | IDREF |       |       |       |       |       |       |       |       |       |       |
   | Study |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | Comp  |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | onent |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | UID   |       |       |       |       |       |       |       |       |       |       |       |       |       |
   +-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+
   | Proc  | 1     | DCM   | U     | N     | Y     | X     | K     |       |       |       |       |       |       |
   | edure | 21018 |       | IDREF |       |       |       |       |       |       |       |       |       |       |
   | Study |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | Ins   |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | tance |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | UID   |       |       |       |       |       |       |       |       |       |       |       |       |       |
   +-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+
   | Proc  | 1     | DCM   | DAT   | N     | Y     | X     |       |       |       |       | K     | C     |       |
   | edure | 22701 |       | ETIME |       |       |       |       |       |       |       |       |       |       |
   | Time  |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | Base  |       |       |       |       |       |       |       |       |       |       |       |       |       |
   +-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+
   | Proce | 1     | DCM   | TEXT  | N     | Y     | X     |       |       |       |       |       |       | C     |
   | ssing | 11703 |       |       |       |       |       |       |       |       |       |       |       |       |
   | step  |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | d     |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | escri |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | ption |       |       |       |       |       |       |       |       |       |       |       |       |       |
   +-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+
   | Pro   | 1     | DCM   | TEXT  | N     | Y     | X     |       |       |       |       |       |       | C     |
   | tocol | 26071 |       |       |       |       |       |       |       |       |       |       |       |       |
   | Time  |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | Point |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | Ident |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | ifier |       |       |       |       |       |       |       |       |       |       |       |       |       |
   +-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+
   | Pulse | 1     | DCM   | TEXT  | N     | Y     | X     |       |       |       |       |       |       | C     |
   | Seq   | 28230 |       |       |       |       |       |       |       |       |       |       |       |       |
   | uence |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | Name  |       |       |       |       |       |       |       |       |       |       |       |       |       |
   +-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+
   | Q     | 1     | DCM   | COMP  | N     | Y     | D     | K     |       |       |       |       |       |       |
   | uoted | 21002 |       | OSITE |       |       |       |       |       |       |       |       |       |       |
   | S     |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | ource |       |       |       |       |       |       |       |       |       |       |       |       |       |
   +-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+
   | Radi  | 1     | DCM   | COMP  | N     | Y     | D     | K     |       |       |       |       |       |       |
   | ation | 28436 |       | OSITE |       |       |       |       |       |       |       |       |       |       |
   | Dose  |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | Comp  |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | osite |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | Param |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | eters |       |       |       |       |       |       |       |       |       |       |       |       |       |
   +-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+
   | Radi  | 1     | DCM   | TEXT  | N     | Y     | D     |       |       |       |       |       |       | C     |
   | ation | 28403 |       |       |       |       |       |       |       |       |       |       |       |       |
   | Dose  |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | Est   |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | imate |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | Name  |       |       |       |       |       |       |       |       |       |       |       |       |       |
   +-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+
   | Radi  | 1     | DCM   | COMP  | N     | Y     | D     | K     |       |       |       |       |       |       |
   | ation | 28414 |       | OSITE |       |       |       |       |       |       |       |       |       |       |
   | Dose  |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | Repr  |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | esent |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | ation |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | Data  |       |       |       |       |       |       |       |       |       |       |       |       |       |
   +-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+
   | Radi  | 1     | DCM   | IMAGE | N     | Y     | D     | K     |       |       |       |       |       |       |
   | ation | 28414 |       |       |       |       |       |       |       |       |       |       |       |       |
   | Dose  |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | Repr  |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | esent |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | ation |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | Data  |       |       |       |       |       |       |       |       |       |       |       |       |       |
   +-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+
   | Ra    | 1     | DCM   | TEXT  | N     | Y     | X     |       |       |       |       |       |       |       |
   | dionu | 13514 |       |       |       |       |       |       |       |       |       |       |       |       |
   | clide |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | Ident |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | ifier |       |       |       |       |       |       |       |       |       |       |       |       |       |
   +-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+
   | Radi  | 1     | DCM   | U     | N     | Y     | D     | K     |       |       |       |       |       |       |
   | ophar | 13503 |       | IDREF |       |       |       |       |       |       |       |       |       |       |
   | maceu |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | tical |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | Admi  |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | nistr |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | ation |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | Event |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | UID   |       |       |       |       |       |       |       |       |       |       |       |       |       |
   +-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+
   | Radi  | 1     | DCM   | TEXT  | N     | Y     | X     |       |       |       |       |       |       |       |
   | ophar | 13511 |       |       |       |       |       |       |       |       |       |       |       |       |
   | maceu |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | tical |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | Dis   |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | pense |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | Unit  |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | Ident |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | ifier |       |       |       |       |       |       |       |       |       |       |       |       |       |
   +-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+
   | Radi  | 1     | DCM   | TEXT  | N     | Y     | X     |       |       |       |       |       |       |       |
   | ophar | 13512 |       |       |       |       |       |       |       |       |       |       |       |       |
   | maceu |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | tical |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | Lot   |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | Ident |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | ifier |       |       |       |       |       |       |       |       |       |       |       |       |       |
   +-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+
   | Radi  | 1     | DCM   | DAT   | N     | Y     | X/D   |       |       |       |       | K     | C     |       |
   | ophar | 23003 |       | ETIME |       |       |       |       |       |       |       |       |       |       |
   | maceu |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | tical |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | Start |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | Dat   |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | eTime |       |       |       |       |       |       |       |       |       |       |       |       |       |
   +-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+
   | Radi  | 1     | DCM   | DAT   | N     | Y     | X     |       |       |       |       | K     | C     |       |
   | ophar | 23004 |       | ETIME |       |       |       |       |       |       |       |       |       |       |
   | maceu |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | tical |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | Stop  |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | Dat   |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | eTime |       |       |       |       |       |       |       |       |       |       |       |       |       |
   +-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+
   | Re    | 1     | DCM   | TEXT  | N     | Y     | X     |       |       |       |       |       |       |       |
   | agent | 13513 |       |       |       |       |       |       |       |       |       |       |       |       |
   | Vial  |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | Ident |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | ifier |       |       |       |       |       |       |       |       |       |       |       |       |       |
   +-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+
   | Real  | 1     | DCM   | COMP  | N     | Y     | X     | K     |       |       |       |       |       |       |
   | World | 26100 |       | OSITE |       |       |       |       |       |       |       |       |       |       |
   | Value |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | Map   |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | used  |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | for   |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | m     |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | easur |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | ement |       |       |       |       |       |       |       |       |       |       |       |       |       |
   +-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+
   | R     | 1     | DCM   | TEXT  | N     | Y     | X     |       |       |       |       |       |       | C     |
   | eason | 13907 |       |       |       |       |       |       |       |       |       |       |       |       |
   | for   |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | Proce |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | eding |       |       |       |       |       |       |       |       |       |       |       |       |       |
   +-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+
   | R     | 1     | DCM   | TEXT  | N     | Y     | X     |       |       |       |       |       |       | C     |
   | ecent | 13552 |       |       |       |       |       |       |       |       |       |       |       |       |
   | Phy   |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | sical |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | Act   |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | ivity |       |       |       |       |       |       |       |       |       |       |       |       |       |
   +-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+
   | Reco  | 1     | DCM   | TEXT  | N     | Y     | X     |       |       |       |       |       |       | C     |
   | mmend | 21075 |       |       |       |       |       |       |       |       |       |       |       |       |
   | ation |       |       |       |       |       |       |       |       |       |       |       |       |       |
   +-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+
   | R     | 1     | DCM   | DATE  | N     | Y     | X/D   |       |       |       |       | K     | C     |       |
   | ecomm | 11054 |       |       |       |       |       |       |       |       |       |       |       |       |
   | ended |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | Foll  |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | ow-up |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | Date  |       |       |       |       |       |       |       |       |       |       |       |       |       |
   +-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+
   | Refer | 1     | DCM   | IMAGE | N     | Y     | X/D   | K     |       |       |       |       |       |       |
   | enced | 21191 |       |       |       |       |       |       |       |       |       |       |       |       |
   | Se    |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | gment |       |       |       |       |       |       |       |       |       |       |       |       |       |
   +-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+
   | Refer | 1     | DCM   | IMAGE | N     | Y     | D     | K     |       |       |       |       |       |       |
   | enced | 21214 |       |       |       |       |       |       |       |       |       |       |       |       |
   | Se    |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | gment |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | ation |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | Frame |       |       |       |       |       |       |       |       |       |       |       |       |       |
   +-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+
   | Re    | 1     | DCM   | COMP  | N     | Y     | X     | K     |       |       |       |       |       |       |
   | lated | 12364 |       | OSITE |       |       |       |       |       |       |       |       |       |       |
   | Pa    |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | tient |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | Data  |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | Not   |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | Used  |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | D     |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | uring |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | Pla   |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | nning |       |       |       |       |       |       |       |       |       |       |       |       |       |
   +-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+
   | Room  | 1     | DCM   | TEXT  | N     | Y     | X     |       |       |       |       |       |       |       |
   | Iden  | 21121 |       |       |       |       |       |       |       |       |       |       |       |       |
   | tific |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | ation |       |       |       |       |       |       |       |       |       |       |       |       |       |
   +-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+
   | Sam   | 1     | DCM   | DAT   | N     | Y     | D     |       |       |       |       | K     | C     |       |
   | pling | 11469 |       | ETIME |       |       |       |       |       |       |       |       |       |       |
   | Dat   |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | eTime |       |       |       |       |       |       |       |       |       |       |       |       |       |
   +-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+
   | Sel   | 1     | DCM   | TEXT  | N     | Y     | D     |       |       |       |       |       |       | C     |
   | ected | 11058 |       |       |       |       |       |       |       |       |       |       |       |       |
   | R     |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | egion |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | D     |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | escri |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | ption |       |       |       |       |       |       |       |       |       |       |       |       |       |
   +-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+
   | S     | 1     | DCM   | U     | N     | Y     | D     | K     |       |       |       |       |       |       |
   | eries | 12002 |       | IDREF |       |       |       |       |       |       |       |       |       |       |
   | Ins   |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | tance |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | UID   |       |       |       |       |       |       |       |       |       |       |       |       |       |
   +-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+
   | S     | 1     | DCM   | U     | N     | Y     | D     | K     |       |       |       |       |       |       |
   | eries | 13985 |       | IDREF |       |       |       |       |       |       |       |       |       |       |
   | or    |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | Ins   |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | tance |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | used  |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | for   |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | Water |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | Equiv |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | alent |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | Dia   |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | meter |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | estim |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | ation |       |       |       |       |       |       |       |       |       |       |       |       |       |
   +-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+
   | Se    | 1     | DCM   | TEXT  | N     | Y     | X     |       |       | K     |       |       |       |       |
   | rvice | 21434 |       |       |       |       |       |       |       |       |       |       |       |       |
   | Del   |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | ivery |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | Loc   |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | ation |       |       |       |       |       |       |       |       |       |       |       |       |       |
   +-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+
   | Se    | 1     | DCM   | PNAME | N     | Y     | X     |       |       |       |       |       |       |       |
   | rvice | 21435 |       |       |       |       |       |       |       |       |       |       |       |       |
   | Perf  |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | ormer |       |       |       |       |       |       |       |       |       |       |       |       |       |
   +-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+
   | Se    | 1     | DCM   | TEXT  | N     | Y     | X     |       |       |       |       |       |       |       |
   | rvice | 21435 |       |       |       |       |       |       |       |       |       |       |       |       |
   | Perf  |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | ormer |       |       |       |       |       |       |       |       |       |       |       |       |       |
   +-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+
   | S     | 1604  | SCT   | TEXT  | N     | Y     | X     |       |       |       |       |       |       | C     |
   | ocial | 76009 |       |       |       |       |       |       |       |       |       |       |       |       |
   | Hi    |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | story |       |       |       |       |       |       |       |       |       |       |       |       |       |
   +-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+
   | S     | 1     | DCM   | IMAGE | N     | Y     | D     | K     |       |       |       |       |       |       |
   | ource | 21233 |       |       |       |       |       |       |       |       |       |       |       |       |
   | image |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | for   |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | se    |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | gment |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | ation |       |       |       |       |       |       |       |       |       |       |       |       |       |
   +-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+
   | S     | 1     | DCM   | IMAGE | N     | Y     | D     | K     |       |       |       |       |       |       |
   | ource | 21112 |       |       |       |       |       |       |       |       |       |       |       |       |
   | of    |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | M     |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | easur |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | ement |       |       |       |       |       |       |       |       |       |       |       |       |       |
   +-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+
   | S     | 1     | DCM   | WAV   | N     | Y     | X     | K     |       |       |       |       |       |       |
   | ource | 21112 |       | EFORM |       |       |       |       |       |       |       |       |       |       |
   | of    |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | M     |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | easur |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | ement |       |       |       |       |       |       |       |       |       |       |       |       |       |
   +-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+
   | S     | 1     | DCM   | U     | N     | Y     | D     | K     |       |       |       |       |       |       |
   | ource | 21232 |       | IDREF |       |       |       |       |       |       |       |       |       |       |
   | s     |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | eries |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | for   |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | se    |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | gment |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | ation |       |       |       |       |       |       |       |       |       |       |       |       |       |
   +-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+
   | Sp    | 1     | DCM   | COMP  | N     | Y     | X     | K     |       |       |       |       |       |       |
   | atial | 28447 |       | OSITE |       |       |       |       |       |       |       |       |       |       |
   | Fidu  |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | cials |       |       |       |       |       |       |       |       |       |       |       |       |       |
   +-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+
   | Sp    | 1     | DCM   | COMP  | N     | Y     | X     | K     |       |       |       |       |       |       |
   | atial | 12353 |       | OSITE |       |       |       |       |       |       |       |       |       |       |
   | Re    |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | gistr |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | ation |       |       |       |       |       |       |       |       |       |       |       |       |       |
   +-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+
   | Sp    | 1     | DCM   | COMP  | N     | Y     | D     | K     |       |       |       |       |       |       |
   | atial | 28444 |       | OSITE |       |       |       |       |       |       |       |       |       |       |
   | Re    |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | gistr |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | ation |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | Refe  |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | rence |       |       |       |       |       |       |       |       |       |       |       |       |       |
   +-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+
   | Spe   | 1     | DCM   | TEXT  | N     | Y     | X     |       |       |       |       |       |       |       |
   | cimen | 11700 |       |       |       |       |       |       |       |       |       |       |       |       |
   | Cont  |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | ainer |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | Ident |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | ifier |       |       |       |       |       |       |       |       |       |       |       |       |       |
   +-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+
   | Spe   | 1     | DCM   | TEXT  | N     | Y     | X     |       |       |       |       |       |       |       |
   | cimen | 21041 |       |       |       |       |       |       |       |       |       |       |       |       |
   | Ident |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | ifier |       |       |       |       |       |       |       |       |       |       |       |       |       |
   +-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+
   | Spe   | 1     | DCM   | U     | N     | Y     | X     | K     |       |       |       |       |       |       |
   | cimen | 21039 |       | IDREF |       |       |       |       |       |       |       |       |       |       |
   | UID   |       |       |       |       |       |       |       |       |       |       |       |       |       |
   +-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+
   | SR    | 1     | DCM   | COMP  | N     | Y     | D     | K     |       |       |       |       |       |       |
   | Ins   | 28416 |       | OSITE |       |       |       |       |       |       |       |       |       |       |
   | tance |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | Used  |       |       |       |       |       |       |       |       |       |       |       |       |       |
   +-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+
   | Start | 3982  | SCT   | DAT   | N     | Y     | D     |       |       |       |       | K     | C     |       |
   | Dat   | 01009 |       | ETIME |       |       |       |       |       |       |       |       |       |       |
   | eTime |       |       |       |       |       |       |       |       |       |       |       |       |       |
   +-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+
   | Start | 1     | DCM   | DAT   | N     | Y     | D     |       |       |       |       | K     | C     |       |
   | of    | 13809 |       | ETIME |       |       |       |       |       |       |       |       |       |       |
   | X-Ray |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | I     |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | rradi |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | ation |       |       |       |       |       |       |       |       |       |       |       |       |       |
   +-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+
   | St    | 1     | DCM   | TEXT  | N     | Y     | X     |       | K     |       |       |       |       |       |
   | ation | 10119 |       |       |       |       |       |       |       |       |       |       |       |       |
   | AE    |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | Title |       |       |       |       |       |       |       |       |       |       |       |       |       |
   +-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+
   | ST    | 1     | DCM   | DAT   | N     | Y     | X     |       |       |       |       | K     | C     |       |
   | Elev  | 22173 |       | ETIME |       |       |       |       |       |       |       |       |       |       |
   | ation |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | Onset |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | Dat   |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | eTime |       |       |       |       |       |       |       |       |       |       |       |       |       |
   +-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+
   | Stop  | 3978  | SCT   | DAT   | N     | Y     | D     |       |       |       |       | K     | C     |       |
   | Dat   | 98000 |       | ETIME |       |       |       |       |       |       |       |       |       |       |
   | eTime |       |       |       |       |       |       |       |       |       |       |       |       |       |
   +-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+
   | S     | 1     | DCM   | TEXT  | N     | Y     | X     |       |       |       |       |       |       | C     |
   | tress | 09056 |       |       |       |       |       |       |       |       |       |       |       |       |
   | Pro   |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | tocol |       |       |       |       |       |       |       |       |       |       |       |       |       |
   +-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+
   | Study | 1     | DCM   | DATE  | N     | Y     | X/D   |       |       |       |       | K     | C     |       |
   | Date  | 11060 |       |       |       |       |       |       |       |       |       |       |       |       |
   +-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+
   | Study | 1     | DCM   | U     | N     | Y     | D     | K     |       |       |       |       |       |       |
   | Ins   | 10180 |       | IDREF |       |       |       |       |       |       |       |       |       |       |
   | tance |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | UID   |       |       |       |       |       |       |       |       |       |       |       |       |       |
   +-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+
   | Study | 1     | DCM   | TIME  | N     | Y     | X/D   |       |       |       |       | K     | C     |       |
   | Time  | 11061 |       |       |       |       |       |       |       |       |       |       |       |       |
   +-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+
   | Su    | 1     | DCM   | NUM   | N     | Y     | X     |       |       |       | K     |       |       |       |
   | bject | 21033 |       |       |       |       |       |       |       |       |       |       |       |       |
   | Age   |       |       |       |       |       |       |       |       |       |       |       |       |       |
   +-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+
   | Su    | 1     | DCM   | DATE  | N     | Y     | X     |       |       |       |       |       |       |       |
   | bject | 21031 |       |       |       |       |       |       |       |       |       |       |       |       |
   | Birth |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | Date  |       |       |       |       |       |       |       |       |       |       |       |       |       |
   +-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+
   | Su    | 1     | DCM   | TEXT  | N     | Y     | X/D   |       |       |       |       |       |       |       |
   | bject | 21030 |       |       |       |       |       |       |       |       |       |       |       |       |
   | ID    |       |       |       |       |       |       |       |       |       |       |       |       |       |
   +-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+
   | Su    | 1     | DCM   | PNAME | N     | Y     | D     |       |       |       |       |       |       |       |
   | bject | 21029 |       |       |       |       |       |       |       |       |       |       |       |       |
   | Name  |       |       |       |       |       |       |       |       |       |       |       |       |       |
   +-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+
   | Su    | 1     | DCM   | CODE  | N     | Y     | X     |       |       |       | K     |       |       |       |
   | bject | 21032 |       |       |       |       |       |       |       |       |       |       |       |       |
   | Sex   |       |       |       |       |       |       |       |       |       |       |       |       |       |
   +-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+
   | Su    | 1     | DCM   | TEXT  | N     | Y     | X     |       |       |       |       |       |       | C     |
   | bject | 26070 |       |       |       |       |       |       |       |       |       |       |       |       |
   | Time  |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | Point |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | Ident |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | ifier |       |       |       |       |       |       |       |       |       |       |       |       |       |
   +-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+
   | Su    | 1     | DCM   | U     | N     | Y     | X     | K     |       |       |       |       |       |       |
   | bject | 21028 |       | IDREF |       |       |       |       |       |       |       |       |       |       |
   | UID   |       |       |       |       |       |       |       |       |       |       |       |       |       |
   +-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+
   | Su    | 1     | DCM   | TEXT  | N     | Y     | X     |       |       |       |       |       |       | C     |
   | mmary | 21111 |       |       |       |       |       |       |       |       |       |       |       |       |
   +-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+
   | Suppo | 1     | DCM   | COMP  | N     | Y     | X     | K     |       |       |       |       |       |       |
   | rting | 12359 |       | OSITE |       |       |       |       |       |       |       |       |       |       |
   | I     |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | nform |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | ation |       |       |       |       |       |       |       |       |       |       |       |       |       |
   +-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+
   | Time  | C23   | UMLS  | TEXT  | N     | Y     | X/D   |       |       |       |       |       |       | C     |
   | Point | 48792 |       |       |       |       |       |       |       |       |       |       |       |       |
   +-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+
   | Tra   | 1     | DCM   | U     | N     | Y     | D     | K     |       |       |       |       |       |       |
   | cking | 12040 |       | IDREF |       |       |       |       |       |       |       |       |       |       |
   | U     |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | nique |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | Ident |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | ifier |       |       |       |       |       |       |       |       |       |       |       |       |       |
   +-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+
   | U     | 74    | LN    | TEXT  | N     | Y     | X     |       | K     |       |       |       |       |       |
   | nique | 711-3 |       |       |       |       |       |       |       |       |       |       |       |       |
   | D     |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | evice |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | Ident |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | ifier |       |       |       |       |       |       |       |       |       |       |       |       |       |
   +-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+
   | U     | 1     | DCM   | CONT  | N     | Y     | X     |       | K     |       |       |       |       |       |
   | nique | 21000 |       | AINER |       |       |       |       |       |       |       |       |       |       |
   | D     |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | evice |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | I     |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | denti |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | fiers |       |       |       |       |       |       |       |       |       |       |       |       |       |
   +-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+
   | User  | 1     | DCM   | U     | N     | Y     | D     | K     |       |       |       |       |       |       |
   | Sel   | 12356 |       | IDREF |       |       |       |       |       |       |       |       |       |       |
   | ected |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | Fid   |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | ucial |       |       |       |       |       |       |       |       |       |       |       |       |       |
   +-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+
   | Wav   | 1     | DCM   | WAV   | N     | Y     | D     | K     |       |       |       |       |       |       |
   | eform | 21143 |       | EFORM |       |       |       |       |       |       |       |       |       |       |
   | Acq   |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | uired |       |       |       |       |       |       |       |       |       |       |       |       |       |
   +-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+
   | X-Ray | 1     | DCM   | COMP  | N     | Y     | X     | K     |       |       |       |       |       |       |
   | Atten | 28470 |       | OSITE |       |       |       |       |       |       |       |       |       |       |
   | uator |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | Model |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | Data  |       |       |       |       |       |       |       |       |       |       |       |       |       |
   +-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+
   | X-Ray | 1     | DCM   | IMAGE | N     | Y     | X     | K     |       |       |       |       |       |       |
   | Atten | 28470 |       |       |       |       |       |       |       |       |       |       |       |       |
   | uator |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | Model |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | Data  |       |       |       |       |       |       |       |       |       |       |       |       |       |
   +-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+
   | X-Ray | 1     | DCM   | U     | N     | Y     | X     | K     |       |       |       |       |       |       |
   | Atten | 28470 |       | IDREF |       |       |       |       |       |       |       |       |       |       |
   | uator |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | Model |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | Data  |       |       |       |       |       |       |       |       |       |       |       |       |       |
   +-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+
   | X-Ray | 1     | DCM   | COMP  | N     | Y     | X     | K     |       |       |       |       |       |       |
   | Radi  | 13701 |       | OSITE |       |       |       |       |       |       |       |       |       |       |
   | ation |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | Dose  |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | R     |       |       |       |       |       |       |       |       |       |       |       |       |       |
   | eport |       |       |       |       |       |       |       |       |       |       |       |       |       |
   +-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+

.. _sect_E.3.5:

Clean Descriptors Option
~~~~~~~~~~~~~~~~~~~~~~~~

Even though many Attributes are defined in the DICOM Standard for
specific purposes, such as to describe a Study or a Series, those that
contain plain text over which an operator has control may contain
unstructured information that includes identities.

When this Option is specified in addition to an Application Level
Confidentiality Profile, any information that is embedded in text or
string Attributes corresponding to the Attribute information specified
to be removed by the Profile and any other Options specified shall also
be removed, as described in `table_title <#table_E.1-1>`__.

.. note::

   1. For example, an operator may include a person's name or a
      patient's demographics or physical characteristics in the Study
      Description (0008,1030), perhaps because their modality user
      interface does not provide other fields or because other systems
      do not display them. E.g., the description might contain "CT chest
      abdomen pelvis - 55F Dr. Smith".

   2. One approach to cleaning such text strings without human
      intervention is to extract and retain only values known to be
      useful and safe and discard all others. For example, in the string
      "CT chest abdomen pelvis - 55F Dr. Smith" are found in Study
      Description (0008,1030), then it would be feasible to detect and
      retain "CT chest abdomen pelvis" and discard the remainder. In an
      international setting, this may require an extensive dictionary of
      words that are safe to retain, e.g., to detect "Buik" for abdomen
      in Dutch or "λεκάνη" for pelvis in Greek. Another possibility is
      to extract such information and attempt to code the information in
      other Attributes (if otherwise absent or empty) such as Anatomic
      Region Sequence (0008,2218). However, the possibility of string
      values being both identifying and descriptive in different uses
      needs to be considered, e.g., "Dr. Hand" or "M. Genou".

   3. `table_title <#table_E.1-1>`__ calls out specific Attributes known
      to be at risk, but an implementer may want to consider any
      attribute that could potential contain character data, though this
      Option does not require that this be done. For example, all SH,
      LO, ST, LT and UT Value Representations could perhaps be misused.
      Code strings, CS, are not generally at risk, but a check against
      known Defined Terms and Enumerated Values could be performed.
      Though extremely unusual, it is conceivable that even a DS or IS
      string could be misused, and a check could be made that only legal
      numeric characters were used. Any PN Attribute is obviously at
      risk. The OB VR is discussed in the Retain Safe Private Option.

   4. This Option specifies what needs to be removed, not what needs to
      be retained. Depending on the application, it may be desirable to
      retain some information, such as technique description, but
      discard other information, such as diagnosis, for example because
      it may bias the interpretation in a clinical trial. For example,
      one approach is to remove all description and comment attributes
      except Series Description (0008,103E), since this Attribute rarely
      contains identifying or diagnosis information yet is typically a
      reliable source of useful information about the acquisition
      technique populated automatically from modality device protocols,
      though it still could be cleaned as described in Note 2.

   5. It should be recognized that if any descriptor contains
      information about a particularly unusual procedure or condition,
      then in conjunction with other demographic information it might
      reduce the number of possible individuals that could be the
      imaging subject. However, this is to some extent true also if the
      condition or other unusual physical features are obvious from
      visual examination of the images themselves. E.g., how many
      conjoined twins born in a particular month in Philadelphia might
      there be?

The manner of cleaning shall be described in the Conformance Statement.

.. _sect_E.3.6:

Retain Longitudinal Temporal Information Options
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

Dates and times are recognized as having a potential for leakage of
identity because they constrain the number of possible individuals that
could be the imaging subject, though only if there is access to other
information about the individuals concerned to match it against.

However, there are applications that require dates and times to be
present to able to fulfill the objective. This is particularly true in
therapeutic clinical trials in which the objective is to measure change
in an outcome measure over time. Further, it is often necessary to
correlate information from images with information from other sources,
such as clinical and laboratory data, and dates and times need to be
consistent.

Two options are specified to address these requirements:

-  Retain Longitudinal Temporal Information With Full Dates Option

-  Retain Longitudinal Temporal Information With Modified Dates Option

When the Retain Longitudinal Temporal Information With Full Dates Option
is specified in addition to an Application Level Confidentiality
Profile, any dates and times present in the Attributes shall be
retained, as described in `table_title <#table_E.1-1>`__. The Attribute
Longitudinal Temporal Information Modified (0028,0303) shall be added to
the Dataset with a value of "UNMODIFIED".

When the Retain Longitudinal Temporal Information With Modified Dates
Option is specified in addition to an Application Level Confidentiality
Profile, any dates and times present in the Attributes listed in
`table_title <#table_E.1-1>`__ shall be modified. The modification of
the dates and times shall be performed in a manner that:

-  aggregates or transforms dates so as to reduce the possibility of
   matching for re-identification

-  preserves the gross longitudinal temporal relationships between
   images obtained on different dates to the extent necessary for the
   application

-  preserves the fine temporal relationships between images and
   real-world events to the extent necessary for analysis of the images
   for the application

The Attribute Longitudinal Temporal Information Modified (0028,0303)
shall be added to the Dataset with a value of "MODIFIED".

.. note::

   1. Aggregation of dates may be performed by various means such as
      setting all dates to the first day of the month, all months to the
      first month of the year, etc., depending on the precision required
      for the application.

   2. It is possible to modify all dates and times to dummy values by
      shifting them relative to an arbitrary event, and hence retain the
      precise longitudinal temporal relationships amongst a set of
      studies, when either de-identification of the entire set is
      performed at the same time, or some sort of mapping or database is
      kept to repeat this process on separate occasions. It may also be
      desirable to record the type of event and the temporal offset from
      that event, and Attributes are provided for that purpose; see
      Longitudinal Temporal Offset from Event (0012,0052) and
      Longitudinal Temporal Event Type (0012,0053) in the .

   3. Transformation of dates and times should be considered together,
      in order to address studies that span midnight.

   4. Any transformation of times should be performed in such a manner
      as to not disrupt computations needed for analysis, such as
      comparison of start of injection time to the acquisition time for
      PET SUV, or extraction of time-intensity values from dynamic
      contrast enhanced studies.

The manner of date modification shall be described in the Conformance
Statement.

.. _sect_E.3.7:

Retain Patient Characteristics Option
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

Physical characteristics of the patient, which are descriptive rather
than identifying information per se, are recognized as having a
potential for leakage of identity because they constrain the number of
possible individuals that could be the imaging subject, though only if
there is access to other information about the individuals concerned to
match it against.

However, there are applications that require such physical
characteristics in order to perform the computations necessary to
analyze the images to fulfill the objective. One such class of
applications is those that are related to metabolic measures, such as
computation of PET Standard Uptake Values (SUV) or DEXA or MRI measures
of body composition, which are based on body weight, body surface area
or lean body mass.

When this Option is specified in addition to an Application Level
Confidentiality Profile, information about age, sex, height and weight
and other characteristics present in the Attributes shall be retained,
as described in `table_title <#table_E.1-1>`__.

The manner of cleaning of retained attributes shall be described in the
Conformance Statement.

.. _sect_E.3.8:

Retain Device Identity Option
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

Information about the identity of the device that was used to perform
the acquisition is recognized as having a potential for leakage of
identity because it may constrain the number of possible individuals
that could be the imaging subject, though only if there is access to
other information about the individuals concerned to match it against.

However, there are applications that require such device information to
perform the analysis or interpretation. The type of correction for
spatial or other inhomogeneity may require knowledge of the specific
device serial number. Confirmation that specific devices that have been
previously qualified (e.g., with phantoms) may be required. Further,
there may be a need to maintain a record of the device used for
regulatory or registry purposes, yet the acquisition site may not
maintain an adequate electronic audit trail.

When this Option is specified in addition to an Application Level
Confidentiality Profile, information about the identity of the device in
the Attributes shall be retained, as described in
`table_title <#table_E.1-1>`__.

.. _sect_E.3.9:

Retain UIDs Option
~~~~~~~~~~~~~~~~~~

Though individuals do not have unique identifiers themselves, studies,
series, instances and other entities in the DICOM model are assigned
globally unique UIDs. Whilst these UIDs cannot be mapped directly to an
individual out of context, given access to the original images, or to a
database of the original images containing the UIDs, it would be
possible to recover the individual's identity.

However, there are applications that require the ability to maintain an
audit trail back to the original images and though there are other
mechanisms they may not scale well or be reliably implemented. This
Option is provided for use when it is judged that the risk of gaining
access to the original information via the UIDs is small relative to the
benefit of retaining them.

When this Option is specified in addition to an Application Level
Confidentiality Profile, UIDs shall be retained, as described in
`table_title <#table_E.1-1>`__.

.. note::

   1. A UID of a DICOM entity is not the same as a unique identifier of
      an individual, such as would be proscribed by some privacy
      regulations.

   2. UIDs are generated using a hierarchical scheme of "roots", which
      may be traceable by a knowledgeable person back to the original
      assignee of the root, typically the device manufacturer, but
      sometimes the organization using the device.

   3. When evaluating the risk of matching UIDs with the original images
      or PACS database, one should consider that even if the UIDs are
      changed, the pixel data itself presents a similar risk.
      Specifically, the pixel data of the de-identified image can be
      matched against the pixel data of the original image. Such
      matching can be greatly accelerated by comparing pre-computed hash
      values of the pixel data. Removal of burned-in identification may
      change the pixel data but then matching against a sub-region of
      the pixel data is almost certainly possible (e.g., the central
      region of an image). Even addition of noise to an image is not
      sufficient to prevent re-identification since statistical matching
      techniques can be used. Ultimately, if any useable pixel data is
      retained during de-identification, then re-identification is
      nearly always possible if one has access to the original images.
      Ergo, replacement of UIDs should not give rise to a false
      confidence that the images have been more thoroughly de-identified
      than if the UIDs are retained.

   4. Regardless of this option, implementers should take care not to
      remove UIDs that are structural and defined by the Standard as
      opposed to those that are instance-related. E.g., one would never
      remove or replace the SOP Class UID for de-identification
      purposes.

   5. The Implementation Class UID (0002,0012) is not included in the
      list of UID attributes to be retained, since it is part of the
      File Meta Information (see ), which is entirely replaced whenever
      a file is stored or modified during de-identification. See
      `De-identifier <#sect_E.1.1>`__.

   6. UIDs may have been generated using a date/time stamp mechanism to
      assist in uniqueness generation. Hence if the original UIDs are
      not replaced, they may assist identity recovery. That said, the
      presence of an apparent date/time stamp in a UID does not indicate
      that it is an original UID, since replacement UIDs may contain new
      date/time stamps related to when the instance was de-identified.
      Also, UUIDs may be time-based rather than name-based or
      random-number-based, so use of the mechanism does not necessarily
      avoid this issue.

.. _sect_E.3.10:

Retain Safe Private Option
~~~~~~~~~~~~~~~~~~~~~~~~~~

By definition, Private Attributes contain proprietary information, in
many cases the nature of which is known only to the vendor and not
publicly documented.

However, some Private Attributes may be necessary for the desired
application. For example, specific technique information such as CT
helical span pitch, or pixel value transformation, such as PET SUV
rescale factors, may only be available in Private Attributes since the
information is either not defined in Standard Attributes, or was added
to the DICOM Standard after the acquisition device was manufactured.

When this Option is specified in addition to an Application Level
Confidentiality Profile, Private Attributes that are known by the
de-identifier to be safe from identity leakage shall be retained,
together with the Private Creator IDs that are required to fully define
the retained Private Attributes; all other Private Attributes shall be
removed or processed in the element-specific manner recommended by
Deidentification Action (0008,0307), if present within Private Data
Element Characteristics Sequence (0008,0300) (see ).

Whether or not an Attribute is known to be safe may be determined by:

-  its presence in a block of Private Data Elements with a value of
   "SAFE" in Block Identifying Information Status (0008,0303) or
   individually listed in Nonidentifying Private Elements (gggg,0004)
   (within Private Data Element Characteristics Sequence (0008,0300);
   see )

-  its presence in `table_title <#table_E.3.10-1>`__

-  documentation in the Conformance Statement

-  some other means.

When this Option is not specified, all Private Attributes shall be
removed, as described in `table_title <#table_E.1-1>`__.

.. note::

   1. A sample list of Private Attributes thought to be safe is provided
      here. Vendors do not guarantee them to be safe, and do not commit
      to sending them in any particular software version (including
      future products).

      .. table:: Safe Private Attributes

         +----------------+----------------+--------+--------+----------------+
         | **Data         | **Private      | **VR** | **VM** | **Meaning**    |
         | Element**      | Creator**      |        |        |                |
         +================+================+========+========+================+
         | (7053,xx00)    | Philips PET    | DS     | 1      | SUV Factor -   |
         |                | Private Group  |        |        | Multiplying    |
         |                |                |        |        | stored pixel   |
         |                |                |        |        | values by      |
         |                |                |        |        | Rescale Slope  |
         |                |                |        |        | then this      |
         |                |                |        |        | factor results |
         |                |                |        |        | in SUVbw in    |
         |                |                |        |        | g/l            |
         +----------------+----------------+--------+--------+----------------+
         | (7053,xx09)    | Philips PET    | DS     | 1      | Activity       |
         |                | Private Group  |        |        | Concentration  |
         |                |                |        |        | Factor -       |
         |                |                |        |        | Multiplying    |
         |                |                |        |        | stored pixel   |
         |                |                |        |        | values by      |
         |                |                |        |        | Rescale Slope  |
         |                |                |        |        | then this      |
         |                |                |        |        | factor results |
         |                |                |        |        | in MBq/ml.     |
         +----------------+----------------+--------+--------+----------------+
         | (00E1,xx21)    | ELSCINT1       | DS     | 1      | DLP            |
         +----------------+----------------+--------+--------+----------------+
         | (00E1,xx50)    | ELSCINT1       | DS     | 1      | Acquisition    |
         |                |                |        |        | Duration       |
         +----------------+----------------+--------+--------+----------------+
         | (01E1,xx26)    | ELSCINT1       | CS     | 1      | Phantom Type   |
         +----------------+----------------+--------+--------+----------------+
         | (01F1,xx01)    | ELSCINT1       | CS     | 1      | Acquisition    |
         |                |                |        |        | Type           |
         +----------------+----------------+--------+--------+----------------+
         | (01F1,xx07)    | ELSCINT1       | DS     | 1      | Table Velocity |
         +----------------+----------------+--------+--------+----------------+
         | (01F1,xx26)    | ELSCINT1       | DS     | 1      | Pitch          |
         +----------------+----------------+--------+--------+----------------+
         | (01F1,xx27)    | ELSCINT1       | DS     | 1      | Rotation Time  |
         +----------------+----------------+--------+--------+----------------+
         | (0019,xx23)    | GEMS_ACQU_01   | DS     | 1      | Table Speed    |
         |                |                |        |        | [mm/rotation]  |
         +----------------+----------------+--------+--------+----------------+
         | (0019,xx24)    | GEMS_ACQU_01   | DS     | 1      | Mid Scan Time  |
         |                |                |        |        | [sec]          |
         +----------------+----------------+--------+--------+----------------+
         | (0019,xx27)    | GEMS_ACQU_01   | DS     | 1      | Rotation Speed |
         |                |                |        |        | (Gantry        |
         |                |                |        |        | Period)        |
         +----------------+----------------+--------+--------+----------------+
         | (0019,xx9E)    | GEMS_ACQU_01   | LO     | 1      | Internal Pulse |
         |                |                |        |        | Sequence Name  |
         +----------------+----------------+--------+--------+----------------+
         | (0043,xx27)    | GEMS_PARM_01   | SH     | 1      | Scan Pitch     |
         |                |                |        |        | Ratio in the   |
         |                |                |        |        | form "n.nnn:1" |
         +----------------+----------------+--------+--------+----------------+
         | (0045,xx01)    | GEMS_HELIOS_01 | SS     | 1      | Number of      |
         |                |                |        |        | Macro Rows in  |
         |                |                |        |        | Detector       |
         +----------------+----------------+--------+--------+----------------+
         | (0045,xx02)    | GEMS_HELIOS_01 | FL     | 1      | Macro width at |
         |                |                |        |        | ISO Center     |
         +----------------+----------------+--------+--------+----------------+
         | (0903,xx10)    | GEIIS PACS     | US     | 1      | Reject Image   |
         |                |                |        |        | Flag           |
         +----------------+----------------+--------+--------+----------------+
         | (0903,xx11)    | GEIIS PACS     | US     | 1      | Significant    |
         |                |                |        |        | Flag           |
         +----------------+----------------+--------+--------+----------------+
         | (0903,xx12)    | GEIIS PACS     | US     | 1      | Confidential   |
         |                |                |        |        | Flag           |
         +----------------+----------------+--------+--------+----------------+
         | (2001,xx03)    | Philips        | FL     | 1      | Diffusion      |
         |                | Imaging DD 001 |        |        | B-Factor       |
         +----------------+----------------+--------+--------+----------------+
         | (2001,xx04)    | Philips        | CS     | 1      | Diffusion      |
         |                | Imaging DD 001 |        |        | Direction      |
         +----------------+----------------+--------+--------+----------------+
         | (0019,xx0C)    | SIEMENS MR     | IS     | 1      | B Value        |
         |                | HEADER         |        |        |                |
         +----------------+----------------+--------+--------+----------------+
         | (0019,xx0D)    | SIEMENS MR     | CS     | 1      | Diffusion      |
         |                | HEADER         |        |        | Directionality |
         +----------------+----------------+--------+--------+----------------+
         | (0019,xx0E)    | SIEMENS MR     | FD     | 3      | Diffusion      |
         |                | HEADER         |        |        | Gradient       |
         |                |                |        |        | Direction      |
         +----------------+----------------+--------+--------+----------------+
         | (0019,xx27)    | SIEMENS MR     | FD     | 6      | B Matrix       |
         |                | HEADER         |        |        |                |
         +----------------+----------------+--------+--------+----------------+
         | (0043,xx39)    | GEMS_PARM_01   | IS     | 4      | 1\ :s          |
         |                |                |        |        | up:`st`\ value |
         |                |                |        |        | is B Value     |
         +----------------+----------------+--------+--------+----------------+
         | (0043,xx6F)    | GEMS_PARM_01   | DS     | 3-4    | Scanner Table  |
         |                |                |        |        | Entry +        |
         |                |                |        |        | Gradient Coil  |
         |                |                |        |        | Selected       |
         +----------------+----------------+--------+--------+----------------+
         | (0025,xx07)    | GEMS_SERS_01   | SL     | 1      | Images in      |
         |                |                |        |        | Series         |
         +----------------+----------------+--------+--------+----------------+
         | (7E01,xx01)    | HOLOGIC, Inc.  | LO     | 1      | Codec Version  |
         +----------------+----------------+--------+--------+----------------+
         | (7E01,xx02)    | HOLOGIC, Inc.  | SH     | 1      | Codec Content  |
         |                |                |        |        | Type           |
         +----------------+----------------+--------+--------+----------------+
         | (7E01,xx10)    | HOLOGIC, Inc.  | SQ     | 1      | High           |
         |                |                |        |        | Resolution     |
         |                |                |        |        | Data Sequence  |
         +----------------+----------------+--------+--------+----------------+
         | (7E01,xx11)    | HOLOGIC, Inc.  | SQ     | 1      | Low Resolution |
         |                |                |        |        | Data Sequence  |
         +----------------+----------------+--------+--------+----------------+
         | (7E01,xx12)    | HOLOGIC, Inc.  | OB     | 1      | Codec Content  |
         +----------------+----------------+--------+--------+----------------+
         | (0099,xx01)    | NQHeader       | UI     | 1      | Version        |
         +----------------+----------------+--------+--------+----------------+
         | (0099,xx02)    | NQHeader       | UI     | 1      | Analyzed       |
         |                |                |        |        | Series UID     |
         +----------------+----------------+--------+--------+----------------+
         | (0099,xx04)    | NQHeader       | SS     | 1      | Return Code    |
         +----------------+----------------+--------+--------+----------------+
         | (0099,xx05)    | NQHeader       | LT     | 1      | Return Message |
         +----------------+----------------+--------+--------+----------------+
         | (0099,xx10)    | NQHeader       | FL     | 1      | MI             |
         +----------------+----------------+--------+--------+----------------+
         | (0099,xx20)    | NQHeader       | SH     | 1      | Units          |
         +----------------+----------------+--------+--------+----------------+
         | (0099,xx21)    | NQHeader       | FL     | 1      | ICV            |
         +----------------+----------------+--------+--------+----------------+
         | (0199,xx01)    | NQLeft         | FL     | 1      | Left Cortical  |
         |                |                |        |        | White Matter   |
         +----------------+----------------+--------+--------+----------------+
         | (0199,xx02)    | NQLeft         | FL     | 1      | Left Cortical  |
         |                |                |        |        | Gray Matter    |
         +----------------+----------------+--------+--------+----------------+
         | (0199,xx03)    | NQLeft         | FL     | 1      | Left 3rd       |
         |                |                |        |        | Ventricle      |
         +----------------+----------------+--------+--------+----------------+
         | (0199,xx04)    | NQLeft         | FL     | 1      | Left 4th       |
         |                |                |        |        | Ventricle      |
         +----------------+----------------+--------+--------+----------------+
         | (0199,xx05)    | NQLeft         | FL     | 1      | Left 5th       |
         |                |                |        |        | Ventricle      |
         +----------------+----------------+--------+--------+----------------+
         | (0199,xx06)    | NQLeft         | FL     | 1      | Left Lateral   |
         |                |                |        |        | Ventricle      |
         +----------------+----------------+--------+--------+----------------+
         | (0199,xx07)    | NQLeft         | FL     | 1      | Left Inferior  |
         |                |                |        |        | Lateral        |
         |                |                |        |        | Ventricle      |
         +----------------+----------------+--------+--------+----------------+
         | (0199,xx08)    | NQLeft         | FL     | 1      | Left Inferior  |
         |                |                |        |        | CSF            |
         +----------------+----------------+--------+--------+----------------+
         | (0199,xx09)    | NQLeft         | FL     | 1      | Left           |
         |                |                |        |        | Cerebellar     |
         |                |                |        |        | White Matter   |
         +----------------+----------------+--------+--------+----------------+
         | (0199,xx0a)    | NQLeft         | FL     | 1      | Left           |
         |                |                |        |        | Cerebellar     |
         |                |                |        |        | Gray Matter    |
         +----------------+----------------+--------+--------+----------------+
         | (0199,xx0b)    | NQLeft         | FL     | 1      | Left           |
         |                |                |        |        | Hippocampus    |
         +----------------+----------------+--------+--------+----------------+
         | (0199,xx0c)    | NQLeft         | FL     | 1      | Left Amygdala  |
         +----------------+----------------+--------+--------+----------------+
         | (0199,xx0d)    | NQLeft         | FL     | 1      | Left Thalamus  |
         +----------------+----------------+--------+--------+----------------+
         | (0199,xx0e)    | NQLeft         | FL     | 1      | Left Caudate   |
         +----------------+----------------+--------+--------+----------------+
         | (0199,xx0f)    | NQLeft         | FL     | 1      | Left Putamen   |
         +----------------+----------------+--------+--------+----------------+
         | (0199,xx10)    | NQLeft         | FL     | 1      | Left Pallidum  |
         +----------------+----------------+--------+--------+----------------+
         | (0199,xx11)    | NQLeft         | FL     | 1      | Left Ventral   |
         |                |                |        |        | Diencephalon   |
         +----------------+----------------+--------+--------+----------------+
         | (0199,xx12)    | NQLeft         | FL     | 1      | Left Nucleus   |
         |                |                |        |        | Accumbens      |
         +----------------+----------------+--------+--------+----------------+
         | (0199,xx13)    | NQLeft         | FL     | 1      | Left Brain     |
         |                |                |        |        | Stem           |
         +----------------+----------------+--------+--------+----------------+
         | (0199,xx14)    | NQLeft         | FL     | 1      | Left Exterior  |
         |                |                |        |        | CSF            |
         +----------------+----------------+--------+--------+----------------+
         | (0199,xx15)    | NQLeft         | FL     | 1      | Left WM Hypo   |
         +----------------+----------------+--------+--------+----------------+
         | (0199,xx16)    | NQLeft         | FL     | 1      | Left Other     |
         +----------------+----------------+--------+--------+----------------+
         | (0299,xx01)    | NQRight        | FL     | 1      | Right Cortical |
         |                |                |        |        | White Matter   |
         +----------------+----------------+--------+--------+----------------+
         | (0299,xx02)    | NQRight        | FL     | 1      | Right Cortical |
         |                |                |        |        | Gray Matter    |
         +----------------+----------------+--------+--------+----------------+
         | (0299,xx03)    | NQRight        | FL     | 1      | Right 3rd      |
         |                |                |        |        | Ventricle      |
         +----------------+----------------+--------+--------+----------------+
         | (0299,xx04)    | NQRight        | FL     | 1      | Right 4th      |
         |                |                |        |        | Ventricle      |
         +----------------+----------------+--------+--------+----------------+
         | (0299,xx05)    | NQRight        | FL     | 1      | Right 5th      |
         |                |                |        |        | Ventricle      |
         +----------------+----------------+--------+--------+----------------+
         | (0299,xx06)    | NQRight        | FL     | 1      | Right Lateral  |
         |                |                |        |        | Ventricle      |
         +----------------+----------------+--------+--------+----------------+
         | (0299,xx07)    | NQRight        | FL     | 1      | Right Inferior |
         |                |                |        |        | Lateral        |
         |                |                |        |        | Ventricle      |
         +----------------+----------------+--------+--------+----------------+
         | (0299,xx08)    | NQRight        | FL     | 1      | Right Inferior |
         |                |                |        |        | CSF            |
         +----------------+----------------+--------+--------+----------------+
         | (0299,xx09)    | NQRight        | FL     | 1      | Right          |
         |                |                |        |        | Cerebellar     |
         |                |                |        |        | White Matter   |
         +----------------+----------------+--------+--------+----------------+
         | (0299,xx0a)    | NQRight        | FL     | 1      | Right          |
         |                |                |        |        | Cerebellar     |
         |                |                |        |        | Gray Matter    |
         +----------------+----------------+--------+--------+----------------+
         | (0299,xx0b)    | NQRight        | FL     | 1      | Right          |
         |                |                |        |        | Hippocampus    |
         +----------------+----------------+--------+--------+----------------+
         | (0299,xx0c)    | NQRight        | FL     | 1      | Right Amygdala |
         +----------------+----------------+--------+--------+----------------+
         | (0299,xx0d)    | NQRight        | FL     | 1      | Right Thalamus |
         +----------------+----------------+--------+--------+----------------+
         | (0299,xx0e)    | NQRight        | FL     | 1      | Right Caudate  |
         +----------------+----------------+--------+--------+----------------+
         | (0299,xx0f)    | NQRight        | FL     | 1      | Right Putamen  |
         +----------------+----------------+--------+--------+----------------+
         | (0299,xx10)    | NQRight        | FL     | 1      | Right Pallidum |
         +----------------+----------------+--------+--------+----------------+
         | (0299,xx11)    | NQRight        | FL     | 1      | Right Ventral  |
         |                |                |        |        | Diencephalon   |
         +----------------+----------------+--------+--------+----------------+
         | (0299,xx12)    | NQRight        | FL     | 1      | Right Nucleus  |
         |                |                |        |        | Accumbens      |
         +----------------+----------------+--------+--------+----------------+
         | (0299,xx13)    | NQRight        | FL     | 1      | Right Brain    |
         |                |                |        |        | Stem           |
         +----------------+----------------+--------+--------+----------------+
         | (0299,xx14)    | NQRight        | FL     | 1      | Right Exterior |
         |                |                |        |        | CSF            |
         +----------------+----------------+--------+--------+----------------+
         | (0299,xx15)    | NQRight        | FL     | 1      | Right WM Hypo  |
         +----------------+----------------+--------+--------+----------------+
         | (0299,xx16)    | NQRight        | FL     | 1      | Right Other    |
         +----------------+----------------+--------+--------+----------------+
         | (2005,xx0D)    | Philips MR     | FL     | 1      | Scale          |
         |                | Imaging DD 001 |        |        | Intercept      |
         +----------------+----------------+--------+--------+----------------+
         | (2005,xx0E)    | Philips MR     | FL     | 1      | Scale Slope    |
         |                | Imaging DD 001 |        |        |                |
         +----------------+----------------+--------+--------+----------------+
         | (0119,xx00)    | SIEMENS        | LO     | 1      | Acoustic Meta  |
         |                | Ultrasound     |        |        | Information    |
         |                | SC2000         |        |        | Version        |
         +----------------+----------------+--------+--------+----------------+
         | (0119,xx01)    | SIEMENS        | OB     | 1      | Common         |
         |                | Ultrasound     |        |        | Acoustic Meta  |
         |                | SC2000         |        |        | Information    |
         +----------------+----------------+--------+--------+----------------+
         | (0119,xx02)    | SIEMENS        | SQ     | 1      | Multi Stream   |
         |                | Ultrasound     |        |        | Sequence       |
         |                | SC2000         |        |        |                |
         +----------------+----------------+--------+--------+----------------+
         | (0119,xx03)    | SIEMENS        | SQ     | 1      | Acoustic Data  |
         |                | Ultrasound     |        |        | Sequence       |
         |                | SC2000         |        |        |                |
         +----------------+----------------+--------+--------+----------------+
         | (0119,xx04)    | SIEMENS        | OB     | 1      | Per            |
         |                | Ultrasound     |        |        | Transaction    |
         |                | SC2000         |        |        | Acoustic       |
         |                |                |        |        | Control        |
         |                |                |        |        | Information    |
         +----------------+----------------+--------+--------+----------------+
         | (0119,xx05)    | SIEMENS        | UL     | 1      | Acoustic Data  |
         |                | Ultrasound     |        |        | Offset         |
         |                | SC2000         |        |        |                |
         +----------------+----------------+--------+--------+----------------+
         | (0119,xx06)    | SIEMENS        | UL     | 1      | Acoustic Data  |
         |                | Ultrasound     |        |        | Length         |
         |                | SC2000         |        |        |                |
         +----------------+----------------+--------+--------+----------------+
         | (0119,xx07)    | SIEMENS        | UL     | 1      | Footer Offset  |
         |                | Ultrasound     |        |        |                |
         |                | SC2000         |        |        |                |
         +----------------+----------------+--------+--------+----------------+
         | (0119,xx08)    | SIEMENS        | UL     | 1      | Footer Length  |
         |                | Ultrasound     |        |        |                |
         |                | SC2000         |        |        |                |
         +----------------+----------------+--------+--------+----------------+
         | (0119,xx09)    | SIEMENS        | SS     | 1      | Acoustic       |
         |                | Ultrasound     |        |        | Stream Number  |
         |                | SC2000         |        |        |                |
         +----------------+----------------+--------+--------+----------------+
         | (0119,xx10)    | SIEMENS        | SH     | 1      | Acoustic       |
         |                | Ultrasound     |        |        | Stream Type    |
         |                | SC2000         |        |        |                |
         +----------------+----------------+--------+--------+----------------+
         | (0119,xx11)    | SIEMENS        |        | 1      | Stage Timer    |
         |                | Ultrasound     |        |        | Time           |
         |                | SC2000         |        |        |                |
         +----------------+----------------+--------+--------+----------------+
         | (0119,xx12)    | SIEMENS        |        | 1      | Stop Watch     |
         |                | Ultrasound     |        |        | Time           |
         |                | SC2000         |        |        |                |
         +----------------+----------------+--------+--------+----------------+
         | (0119,xx13)    | SIEMENS        | IS     | 1      | Volume Rate    |
         |                | Ultrasound     |        |        |                |
         |                | SC2000         |        |        |                |
         +----------------+----------------+--------+--------+----------------+
         | (0119,xx21)    | SIEMENS        | SH     | 1      |                |
         |                | Ultrasound     |        |        |                |
         |                | SC2000         |        |        |                |
         +----------------+----------------+--------+--------+----------------+
         | (0129,xx00)    | SIEMENS        | SQ     | 1      | MPR View       |
         |                | Ultrasound     |        |        | Sequence       |
         |                | SC2000         |        |        |                |
         +----------------+----------------+--------+--------+----------------+
         | (0129,xx02)    | SIEMENS        | UI     | 1      | Bookmark UID   |
         |                | Ultrasound     |        |        |                |
         |                | SC2000         |        |        |                |
         +----------------+----------------+--------+--------+----------------+
         | (0129,xx03)    | SIEMENS        |        | 1      | Plane Origin   |
         |                | Ultrasound     |        |        | Vector         |
         |                | SC2000         |        |        |                |
         +----------------+----------------+--------+--------+----------------+
         | (0129,xx04)    | SIEMENS        |        | 1      | Row Vector     |
         |                | Ultrasound     |        |        |                |
         |                | SC2000         |        |        |                |
         +----------------+----------------+--------+--------+----------------+
         | (0129,xx05)    | SIEMENS        |        | 1      | Column Vector  |
         |                | Ultrasound     |        |        |                |
         |                | SC2000         |        |        |                |
         +----------------+----------------+--------+--------+----------------+
         | (0129,xx06)    | SIEMENS        | SQ     | 1      | Visualization  |
         |                | Ultrasound     |        |        | Sequence       |
         |                | SC2000         |        |        |                |
         +----------------+----------------+--------+--------+----------------+
         | (0129,xx07)    | SIEMENS        | UI     | 1      | Bookmark UID   |
         |                | Ultrasound     |        |        |                |
         |                | SC2000         |        |        |                |
         +----------------+----------------+--------+--------+----------------+
         | (0129,xx08)    | SIEMENS        | OB     | 1      | Visualization  |
         |                | Ultrasound     |        |        | Information    |
         |                | SC2000         |        |        |                |
         +----------------+----------------+--------+--------+----------------+
         | (0129,xx09)    | SIEMENS        | SQ     | 1      | Application    |
         |                | Ultrasound     |        |        | State Sequence |
         |                | SC2000         |        |        |                |
         +----------------+----------------+--------+--------+----------------+
         | (0129,xx10)    | SIEMENS        | OB     | 1      | Application    |
         |                | Ultrasound     |        |        | State          |
         |                | SC2000         |        |        | Information    |
         +----------------+----------------+--------+--------+----------------+
         | (0129,xx11)    | SIEMENS        | SQ     | 1      | Referenced     |
         |                | Ultrasound     |        |        | Bookmark       |
         |                | SC2000         |        |        | Sequence       |
         +----------------+----------------+--------+--------+----------------+
         | (0129,xx12)    | SIEMENS        | UI     | 1      | Referenced     |
         |                | Ultrasound     |        |        | Bookmark UID   |
         |                | SC2000         |        |        |                |
         +----------------+----------------+--------+--------+----------------+
         | (0129,xx20)    | SIEMENS        | SQ     | 1      | Cine           |
         |                | Ultrasound     |        |        | Parameters     |
         |                | SC2000         |        |        | Sequence       |
         +----------------+----------------+--------+--------+----------------+
         | (0129,xx21)    | SIEMENS        | OB     | 1      | Cine           |
         |                | Ultrasound     |        |        | Parameters     |
         |                | SC2000         |        |        | Schema         |
         +----------------+----------------+--------+--------+----------------+
         | (0129,xx22)    | SIEMENS        | OB     | 1      | Values of Cine |
         |                | Ultrasound     |        |        | Parameters     |
         |                | SC2000         |        |        |                |
         +----------------+----------------+--------+--------+----------------+
         | (0129,xx29)    | SIEMENS        | OB     | 1      |                |
         |                | Ultrasound     |        |        |                |
         |                | SC2000         |        |        |                |
         +----------------+----------------+--------+--------+----------------+
         | (0129,xx30)    | SIEMENS        | CS     | 1      | Raw Data       |
         |                | Ultrasound     |        |        | Object Type    |
         |                | SC2000         |        |        |                |
         +----------------+----------------+--------+--------+----------------+
         | (0139,xx01)    | SIEMENS        | SL     | 1      | Physio Capture |
         |                | Ultrasound     |        |        | ROI            |
         |                | SC2000         |        |        |                |
         +----------------+----------------+--------+--------+----------------+
         | (0149,xx01)    | SIEMENS        | FD     | 1-n    | Vector of BROI |
         |                | Ultrasound     |        |        | Points         |
         |                | SC2000         |        |        |                |
         +----------------+----------------+--------+--------+----------------+
         | (0149,xx02)    | SIEMENS        | FD     | 1-n    | Start/End      |
         |                | Ultrasound     |        |        | Timestamps of  |
         |                | SC2000         |        |        | Strip Stream   |
         +----------------+----------------+--------+--------+----------------+
         | (0149,xx03)    | SIEMENS        | FD     | 1-n    | Timestamps of  |
         |                | Ultrasound     |        |        | Visible        |
         |                | SC2000         |        |        | R-waves        |
         +----------------+----------------+--------+--------+----------------+
         | (7FD1,xx01)    | SIEMENS        | OB     | 1      | Acoustic Image |
         |                | Ultrasound     |        |        | and Footer     |
         |                | SC2000         |        |        | Data           |
         +----------------+----------------+--------+--------+----------------+
         | (7FD1,xx09)    | SIEMENS        | UI     | 1      | Volume Version |
         |                | Ultrasound     |        |        | ID             |
         |                | SC2000         |        |        |                |
         +----------------+----------------+--------+--------+----------------+
         | (7FD1,xx10)    | SIEMENS        | OB     | 1      | Volume Payload |
         |                | Ultrasound     |        |        |                |
         |                | SC2000         |        |        |                |
         +----------------+----------------+--------+--------+----------------+
         | (7FD1,xx11)    | SIEMENS        | OB     | 1      | After Payload  |
         |                | Ultrasound     |        |        |                |
         |                | SC2000         |        |        |                |
         +----------------+----------------+--------+--------+----------------+
         | (7FD1,xx01)    | SIEMENS SYNGO  | OB     | 1      | Padding        |
         |                | ULTRA-SOUND    |        |        |                |
         |                | TOYON DATA     |        |        |                |
         |                | STREAMING      |        |        |                |
         +----------------+----------------+--------+--------+----------------+
         | (7FD1,xx09)    | SIEMENS SYNGO  | UI     | 1      | Version ID     |
         |                | ULTRA-SOUND    |        |        |                |
         |                | TOYON DATA     |        |        |                |
         |                | STREAMING      |        |        |                |
         +----------------+----------------+--------+--------+----------------+
         | (7FD1,xx10)    | SIEMENS SYNGO  | OB     | 1      | Volume Payload |
         |                | ULTRA-SOUND    |        |        |                |
         |                | TOYON DATA     |        |        |                |
         |                | STREAMING      |        |        |                |
         +----------------+----------------+--------+--------+----------------+
         | (7FD1,xx11)    | SIEMENS SYNGO  | OB     | 1      | After Payload  |
         |                | ULTRA-SOUND    |        |        |                |
         |                | TOYON DATA     |        |        |                |
         |                | STREAMING      |        |        |                |
         +----------------+----------------+--------+--------+----------------+

   2. One approach to retaining Private Attributes safely, either when
      the VR is encoded explicitly or known from a data dictionary (such
      as may be derived from published DICOM Conformance Statements or
      previously encountered instances, perhaps by adaptively extending
      the data dictionary as new explicit VR instances are received), is
      to retain those Attributes that are numeric only. For example, one
      might retain US, SS, UL, SS, FL and FD binary values, and IS and
      DS string values that contain only valid numeric characters. One
      might assume that other string Value Representations are unsafe in
      the absence of definite confirmation from the vendor to the
      contrary; code strings (CS) may be an exception. Bulk binary data
      in OB Value representations is particularly unsafe, and may often
      contain entire proprietary format headers in binary or text or XML
      form that includes the patient's name and other identifying
      information.

The safe private attributes that are retained shall be described in the
Conformance Statement.

.. _sect_E.3.11:

Retain Institution Identity Option
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

Information about the identity of the institution where the acquisition
was performed is recognized as having a potential for leakage of
identity because it may constrain the number of possible individuals
that could be the imaging subject, though only if there is access to
other information about the individuals concerned to match it against.

However, there are applications that require such institution
information to perform the analysis or interpretation. There may be a
need to maintain a record of the institution for regulatory or registry
purposes, yet the acquisition site may not maintain an adequate
electronic audit trail.

When this Option is specified in addition to an Application Level
Confidentiality Profile, information about the identity of the
institution in the Attributes shall be retained, as described in
`table_title <#table_E.1-1>`__.

