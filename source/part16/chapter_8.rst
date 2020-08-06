.. _chapter_8:

Coding Schemes
==============

`table_title <#table_8-1>`__ lists the coding schemes (and their
designators) defined for use in DICOM; `table_title <#table_8-2>`__
lists the HL7v3 coding schemes referenced for use in DICOM.
Additionally, any coding scheme may be used that has an entry in the HL7
Registry of Coding Schemes (HL7 v2 Table 0396, or the equivalent online
registry), in which case the HL7 Symbolic Name shall be used as the
value for the Coding Scheme Designator in DICOM, as long as it does not
conflict with an entry `table_title <#table_8-1>`__ and fits within the
Value Representation of the DICOM Coding Scheme Designator (0008,0102)
attribute. As specified in the HL7 v2 Table 0396, local or private
coding schemes shall be identified by an alphanumeric identifier
beginning with the characters "99".

.. note::

   1. An earlier version of this table was formerly contained in Annex D
      of .

   2. See for further description.

   3. The Coding Scheme UIDs are provided for reference only; the
      normative specification of UIDs and their associated meaning is
      the responsibility of the coding scheme developer and/or HL7.

   4. The current version of HL7 v2 Table 0396 is available at
      http://www.hl7.org/special/committees/vocab/table_0396/index.cfm.

   5. The HL7 registration of Coding Schemes is available at
      http://www.hl7.org/oid/index.cfm.

   6. Publication of codes or references to coding schemes within DICOM
      does not constitute a grant of intellectual property rights to
      implementers. Use of some Coding Schemes may require a license, or
      purchase of the relevant coding scheme publication. Implementers
      should consult the relevant coding scheme publisher; see also
      `Normative References <#chapter_2>`__.

   7. The values of Coding Scheme Name (0008,0115), Coding Scheme
      Responsible Organization (0008,0116) and Coding Scheme Resources
      Sequence (0008,0109), if available, may be used to fill the
      corresponding optional attributes of the Coding Scheme
      Identification Sequence (0008,0110) in the .

.. table:: Coding Schemes

   +----------+----------+----------+----------+----------+----------+
   | Coding   | Coding   | Coding   | Coding   | Coding   | Des      |
   | Scheme   | Scheme   | Scheme   | Scheme   | Scheme   | cription |
   | De       | UID      | Name     | Res      | R        |          |
   | signator | (00      | (00      | ponsible | esources |          |
   | (00      | 08,010C) | 08,0115) | Orga     | Sequence |          |
   | 08,0102) |          |          | nization | (00      |          |
   |          |          |          | (00      | 08,0109) |          |
   |          |          |          | 08,0116) | Type:    |          |
   |          |          |          |          | URL      |          |
   +==========+==========+==========+==========+==========+==========+
   | ACR      | 2.16.84  | ACR      | ACR      |          | ACR      |
   |          | 0.1.​113 | Index    |          |          | Index    |
   |          | 883.6.76 |          |          |          | for      |
   |          |          |          |          |          | Radi     |
   |          |          |          |          |          | ological |
   |          |          |          |          |          | D        |
   |          |          |          |          |          | iagnosis |
   |          |          |          |          |          | Revised, |
   |          |          |          |          |          | 3\ :     |
   |          |          |          |          |          | sup:`rd` |
   |          |          |          |          |          | Edition  |
   |          |          |          |          |          | 1986     |
   +----------+----------+----------+----------+----------+----------+
   | ASTM-si  | 1.2      | ASTM E   | ASTM     |          | `bibl    |
   | gpurpose | .840.100 | 2084     |          |          | ioentry_ |
   |          | 65.​1.12 |          |          |          | title <# |
   |          |          |          |          |          | biblio_A |
   |          |          |          |          |          | STM_E208 |
   |          |          |          |          |          | 4_00>`__ |
   |          |          |          |          |          | S        |
   |          |          |          |          |          | ignature |
   |          |          |          |          |          | Purpose  |
   |          |          |          |          |          | codes    |
   |          |          |          |          |          | (see     |
   |          |          |          |          |          | Annex A1 |
   |          |          |          |          |          | of ASTM  |
   |          |          |          |          |          | E 2084), |
   |          |          |          |          |          | ASTM     |
   |          |          |          |          |          | Subc     |
   |          |          |          |          |          | ommittee |
   |          |          |          |          |          | E 31.20  |
   |          |          |          |          |          | Data and |
   |          |          |          |          |          | System   |
   |          |          |          |          |          | Security |
   |          |          |          |          |          | for      |
   |          |          |          |          |          | Health   |
   |          |          |          |          |          | Inf      |
   |          |          |          |          |          | ormation |
   +----------+----------+----------+----------+----------+----------+
   | BARI     |          | BARI     |          |          | Bypass   |
   |          |          |          |          |          | Ang      |
   |          |          |          |          |          | ioplasty |
   |          |          |          |          |          | R        |
   |          |          |          |          |          | evascula |
   |          |          |          |          |          | rization |
   |          |          |          |          |          | Inves    |
   |          |          |          |          |          | tigation |
   |          |          |          |          |          | \ `bibli |
   |          |          |          |          |          | oentry_t |
   |          |          |          |          |          | itle <#b |
   |          |          |          |          |          | iblio_Al |
   |          |          |          |          |          | derman_1 |
   |          |          |          |          |          | 992>`__; |
   |          |          |          |          |          | endorsed |
   |          |          |          |          |          | by       |
   |          |          |          |          |          | ACC/AHA  |
   |          |          |          |          |          | Gu       |
   |          |          |          |          |          | idelines |
   |          |          |          |          |          | for      |
   |          |          |          |          |          | Coronary |
   |          |          |          |          |          | An       |
   |          |          |          |          |          | giograph |
   |          |          |          |          |          | y\ `bibl |
   |          |          |          |          |          | ioentry_ |
   |          |          |          |          |          | title <# |
   |          |          |          |          |          | biblio_S |
   |          |          |          |          |          | canlon_1 |
   |          |          |          |          |          | 999>`__. |
   +----------+----------+----------+----------+----------+----------+
   | BI       |          | BI-RADS  | ACR      |          | ACR      |
   |          |          |          |          |          | Breast   |
   |          |          |          |          |          | Imaging  |
   |          |          |          |          |          | R        |
   |          |          |          |          |          | eporting |
   |          |          |          |          |          | and Data |
   |          |          |          |          |          | System   |
   |          |          |          |          |          | `biblio  |
   |          |          |          |          |          | entry_ti |
   |          |          |          |          |          | tle <#bi |
   |          |          |          |          |          | blio_BIR |
   |          |          |          |          |          | ADS>`__, |
   |          |          |          |          |          | Coding   |
   |          |          |          |          |          | Scheme   |
   |          |          |          |          |          | Version  |
   |          |          |          |          |          | (00      |
   |          |          |          |          |          | 08,0103) |
   |          |          |          |          |          | is       |
   |          |          |          |          |          | r        |
   |          |          |          |          |          | equired; |
   |          |          |          |          |          | code     |
   |          |          |          |          |          | values   |
   |          |          |          |          |          | are      |
   |          |          |          |          |          | section  |
   |          |          |          |          |          | and      |
   |          |          |          |          |          | p        |
   |          |          |          |          |          | aragraph |
   |          |          |          |          |          | ide      |
   |          |          |          |          |          | ntifiers |
   |          |          |          |          |          | within   |
   |          |          |          |          |          | the      |
   |          |          |          |          |          | pub      |
   |          |          |          |          |          | lication |
   |          |          |          |          |          | where    |
   |          |          |          |          |          | the code |
   |          |          |          |          |          | meaning  |
   |          |          |          |          |          | is       |
   |          |          |          |          |          | defined  |
   |          |          |          |          |          | (e.g.,   |
   |          |          |          |          |          | "I.D.1", |
   |          |          |          |          |          | where I  |
   |          |          |          |          |          | = Breast |
   |          |          |          |          |          | Imaging  |
   |          |          |          |          |          | Lexicon, |
   |          |          |          |          |          | D =      |
   |          |          |          |          |          | Special  |
   |          |          |          |          |          | Cases, 1 |
   |          |          |          |          |          | =        |
   |          |          |          |          |          | Tubular  |
   |          |          |          |          |          | Density, |
   |          |          |          |          |          | as the   |
   |          |          |          |          |          | code     |
   |          |          |          |          |          | value    |
   |          |          |          |          |          | for      |
   |          |          |          |          |          | "Tubular |
   |          |          |          |          |          | De       |
   |          |          |          |          |          | nsity"). |
   |          |          |          |          |          |          |
   |          |          |          |          |          | .        |
   |          |          |          |          |          | . note:: |
   |          |          |          |          |          |          |
   |          |          |          |          |          |    In    |
   |          |          |          |          |          |    the   |
   |          |          |          |          |          |    HL7   |
   |          |          |          |          |          |    r     |
   |          |          |          |          |          | egistry, |
   |          |          |          |          |          |    the   |
   |          |          |          |          |          |    abbr  |
   |          |          |          |          |          | eviation |
   |          |          |          |          |          |    BI is |
   |          |          |          |          |          |          |
   |          |          |          |          |          | assigned |
   |          |          |          |          |          |    to a  |
   |          |          |          |          |          |    d     |
   |          |          |          |          |          | ifferent |
   |          |          |          |          |          |          |
   |          |          |          |          |          |   coding |
   |          |          |          |          |          |          |
   |          |          |          |          |          |  scheme, |
   |          |          |          |          |          |    spec  |
   |          |          |          |          |          | ifically |
   |          |          |          |          |          |    the   |
   |          |          |          |          |          |    Beth  |
   |          |          |          |          |          |          |
   |          |          |          |          |          |   Israel |
   |          |          |          |          |          |          |
   |          |          |          |          |          |  problem |
   |          |          |          |          |          |    list. |
   +----------+----------+----------+----------+----------+----------+
   | C4       | 2.16.84  | CPT-4    | AMA      |          | American |
   |          | 0.1.​113 |          |          |          | Medical  |
   |          | 883.6.12 |          |          |          | Assoc    |
   |          |          |          |          |          | iation's |
   |          |          |          |          |          | Current  |
   |          |          |          |          |          | P        |
   |          |          |          |          |          | rocedure |
   |          |          |          |          |          | Ter      |
   |          |          |          |          |          | minology |
   |          |          |          |          |          | 4        |
   |          |          |          |          |          | (CPT-4)  |
   +----------+----------+----------+----------+----------+----------+
   | C5       | 2.16.84  | CPT-5    | AMA      |          | American |
   |          | 0.1.​113 |          |          |          | Medical  |
   |          | 883.6.82 |          |          |          | Assoc    |
   |          |          |          |          |          | iation's |
   |          |          |          |          |          | Current  |
   |          |          |          |          |          | P        |
   |          |          |          |          |          | rocedure |
   |          |          |          |          |          | Ter      |
   |          |          |          |          |          | minology |
   |          |          |          |          |          | 5        |
   |          |          |          |          |          | (CPT-5)  |
   +----------+----------+----------+----------+----------+----------+
   | caDSR    | 2.16.840 | Cancer   | NCI      |          | The      |
   |          | .1.11388 | Data     |          |          | Public   |
   |          | 3.3.26.2 | Standard |          |          | ID is    |
   |          |          | Re       |          |          | used as  |
   |          |          | pository |          |          | the Code |
   |          |          |          |          |          | Value.   |
   |          |          |          |          |          |          |
   |          |          |          |          |          | These    |
   |          |          |          |          |          | can be   |
   |          |          |          |          |          | looked   |
   |          |          |          |          |          | up as in |
   |          |          |          |          |          | the      |
   |          |          |          |          |          | f        |
   |          |          |          |          |          | ollowing |
   |          |          |          |          |          | example  |
   |          |          |          |          |          | (the     |
   |          |          |          |          |          | version  |
   |          |          |          |          |          | is       |
   |          |          |          |          |          | re       |
   |          |          |          |          |          | quired): |
   |          |          |          |          |          | `http    |
   |          |          |          |          |          | ://​cdeb |
   |          |          |          |          |          | rowser.​ |
   |          |          |          |          |          | nci.​nih |
   |          |          |          |          |          | .​gov/​C |
   |          |          |          |          |          | DEBrowse |
   |          |          |          |          |          | r/​searc |
   |          |          |          |          |          | h?​dataE |
   |          |          |          |          |          | lementDe |
   |          |          |          |          |          | tails​=​ |
   |          |          |          |          |          | 9/​&cdeI |
   |          |          |          |          |          | d=217869 |
   |          |          |          |          |          | 3&​versi |
   |          |          |          |          |          | on=2.1​& |
   |          |          |          |          |          | ​PageId​ |
   |          |          |          |          |          | =DataEle |
   |          |          |          |          |          | mentsGro |
   |          |          |          |          |          | up <http |
   |          |          |          |          |          | ://cdebr |
   |          |          |          |          |          | owser.nc |
   |          |          |          |          |          | i.nih.go |
   |          |          |          |          |          | v/CDEBro |
   |          |          |          |          |          | wser/sea |
   |          |          |          |          |          | rch?data |
   |          |          |          |          |          | ElementD |
   |          |          |          |          |          | etails=9 |
   |          |          |          |          |          | /&cdeId= |
   |          |          |          |          |          | 2178693& |
   |          |          |          |          |          | version= |
   |          |          |          |          |          | 2.1&Page |
   |          |          |          |          |          | Id=DataE |
   |          |          |          |          |          | lementsG |
   |          |          |          |          |          | roup>`__ |
   +----------+----------+----------+----------+----------+----------+
   | CD2      | 2.16.84  | CDT-2    | ADA      |          | American |
   |          | 0.1.​113 |          |          |          | Dental   |
   |          | 883.6.13 |          |          |          | Assoc    |
   |          |          |          |          |          | iation's |
   |          |          |          |          |          | (ADA)    |
   |          |          |          |          |          | Current  |
   |          |          |          |          |          | Dental   |
   |          |          |          |          |          | Ter      |
   |          |          |          |          |          | minology |
   |          |          |          |          |          | 2        |
   |          |          |          |          |          | (CDT-2)  |
   +----------+----------+----------+----------+----------+----------+
   | CTV3     | 2.16.8   | Clinical | UK NHS   |          | Read     |
   |          | 40.1.​11 | Terms    |          |          | Codes    |
   |          | 3883.6.6 | Version  |          |          |          |
   |          |          | 3        |          |          |          |
   +----------+----------+----------+----------+----------+----------+
   | DC       | 1.2.840. | Dublin   | W3C      | DOC:     | Dublin   |
   |          | 10008.​2 | Core     |          | `http:/  | Code     |
   |          | .​16.​10 |          |          | /​dublin | Metadata |
   |          |          |          |          | core.​or | for      |
   |          |          |          |          | g/​docum | Resource |
   |          |          |          |          | ents/​19 | Di       |
   |          |          |          |          | 98/​09/​ | scovery. |
   |          |          |          |          | dces/ <h | The code |
   |          |          |          |          | ttp://du | value is |
   |          |          |          |          | blincore | the      |
   |          |          |          |          | .org/doc | Label    |
   |          |          |          |          | uments/1 | field,   |
   |          |          |          |          | 998/09/d | e.g.,    |
   |          |          |          |          | ces/>`__ | "        |
   |          |          |          |          |          | Creator" |
   |          |          |          |          | DOC:     | (capita  |
   |          |          |          |          | `h       | lization |
   |          |          |          |          | ttp://​w | signi    |
   |          |          |          |          | ww.​ietf | ficant). |
   |          |          |          |          | .​org/​r |          |
   |          |          |          |          | fc/​rfc2 |          |
   |          |          |          |          | 413.txt  |          |
   |          |          |          |          | <http:// |          |
   |          |          |          |          | www.ietf |          |
   |          |          |          |          | .org/rfc |          |
   |          |          |          |          | /rfc2413 |          |
   |          |          |          |          | .txt>`__ |          |
   +----------+----------+----------+----------+----------+----------+
   | DCM      | 1.2.8    | DICOM    | DICOM    | DOC:     | PS3.16   |
   |          | 40.10008 | Co       |          | `http    | Content  |
   |          | .​2.16.4 | ntrolled |          | ://​dico | Mapping  |
   |          |          | Ter      |          | m.​nema. | R        |
   |          |          | minology |          | ​org/​me | esource, |
   |          |          |          |          | dical/​d | Annex D  |
   |          |          |          |          | icom/​cu | (Note    |
   |          |          |          |          | rrent/​o | that HL7 |
   |          |          |          |          | utput/​c | also     |
   |          |          |          |          | html/​pa | s        |
   |          |          |          |          | rt16/​ch | pecifies |
   |          |          |          |          | apter_D. | an OID   |
   |          |          |          |          | html <ht | of       |
   |          |          |          |          | tp://dic | 2.16.840 |
   |          |          |          |          | om.nema. | .1.​1138 |
   |          |          |          |          | org/medi | 83.6.31, |
   |          |          |          |          | cal/dico | but      |
   |          |          |          |          | m/curren | de       |
   |          |          |          |          | t/output | precates |
   |          |          |          |          | /chtml/p | it in    |
   |          |          |          |          | art16/ch | favor of |
   |          |          |          |          | apter_D. | 1.2.840  |
   |          |          |          |          | html>`__ | .10008.​ |
   |          |          |          |          |          | 2.16.4). |
   |          |          |          |          | OWL:     |          |
   |          |          |          |          | `        |          |
   |          |          |          |          | ftp://​m |          |
   |          |          |          |          | edical.​ |          |
   |          |          |          |          | nema.​or |          |
   |          |          |          |          | g/​medic |          |
   |          |          |          |          | al/​dico |          |
   |          |          |          |          | m/​curre |          |
   |          |          |          |          | nt/​onto |          |
   |          |          |          |          | logy/​dc |          |
   |          |          |          |          | m.owl.zi |          |
   |          |          |          |          | p <ftp:/ |          |
   |          |          |          |          | /medical |          |
   |          |          |          |          | .nema.or |          |
   |          |          |          |          | g/medica |          |
   |          |          |          |          | l/dicom/ |          |
   |          |          |          |          | current/ |          |
   |          |          |          |          | ontology |          |
   |          |          |          |          | /dcm.owl |          |
   |          |          |          |          | .zip>`__ |          |
   +----------+----------+----------+----------+----------+----------+
   | DCMUID   | 1.2.     | DICOM    | DICOM    | DOC:     |          |
   |          | 840.1000 | UID      |          | `http    |          |
   |          | 8.​2.6.1 | Registry |          | ://​dico |          |
   |          |          |          |          | m.​nema. |          |
   |          |          |          |          | ​org/​me |          |
   |          |          |          |          | dical/​d |          |
   |          |          |          |          | icom/​cu |          |
   |          |          |          |          | rrent/​o |          |
   |          |          |          |          | utput/​c |          |
   |          |          |          |          | html/​pa |          |
   |          |          |          |          | rt06/​ch |          |
   |          |          |          |          | apter_A. |          |
   |          |          |          |          | html <ht |          |
   |          |          |          |          | tp://dic |          |
   |          |          |          |          | om.nema. |          |
   |          |          |          |          | org/medi |          |
   |          |          |          |          | cal/dico |          |
   |          |          |          |          | m/curren |          |
   |          |          |          |          | t/output |          |
   |          |          |          |          | /chtml/p |          |
   |          |          |          |          | art06/ch |          |
   |          |          |          |          | apter_A. |          |
   |          |          |          |          | html>`__ |          |
   +----------+----------+----------+----------+----------+----------+
   | FMA      | 2.16.840 | FMA      | Un       | DOC:     | Digital  |
   |          | .1.​1138 |          | iversity | `        | A        |
   |          | 83.6.119 |          | of       | http://​ | natomist |
   |          |          |          | Was      | sig.​bio | Foun     |
   |          |          |          | hington, | str.​was | dational |
   |          |          |          | Seattle  | hington. | Model of |
   |          |          |          |          | ​edu/​pr | Anatomy  |
   |          |          |          |          | ojects/​ |          |
   |          |          |          |          | fm/​Abou |          |
   |          |          |          |          | tFM.​htm |          |
   |          |          |          |          | l <http: |          |
   |          |          |          |          | //sig.bi |          |
   |          |          |          |          | ostr.was |          |
   |          |          |          |          | hington. |          |
   |          |          |          |          | edu/proj |          |
   |          |          |          |          | ects/fm/ |          |
   |          |          |          |          | AboutFM. |          |
   |          |          |          |          | html>`__ |          |
   |          |          |          |          |          |          |
   |          |          |          |          | OWL:     |          |
   |          |          |          |          | `http:// |          |
   |          |          |          |          | ​sig.​bi |          |
   |          |          |          |          | ostr.​wa |          |
   |          |          |          |          | shington |          |
   |          |          |          |          | .​edu/​s |          |
   |          |          |          |          | hare/​do |          |
   |          |          |          |          | wnloads/ |          |
   |          |          |          |          | ​fma/​re |          |
   |          |          |          |          | lease/​l |          |
   |          |          |          |          | atest/​f |          |
   |          |          |          |          | ma.​zip  |          |
   |          |          |          |          | <http:// |          |
   |          |          |          |          | sig.bios |          |
   |          |          |          |          | tr.washi |          |
   |          |          |          |          | ngton.ed |          |
   |          |          |          |          | u/share/ |          |
   |          |          |          |          | download |          |
   |          |          |          |          | s/fma/re |          |
   |          |          |          |          | lease/la |          |
   |          |          |          |          | test/fma |          |
   |          |          |          |          | .zip>`__ |          |
   +----------+----------+----------+----------+----------+----------+
   | HPC      | 2.16.84  |          |          |          | He       |
   |          | 0.1.​113 |          |          |          | althcare |
   |          | 883.6.14 |          |          |          | F        |
   |          |          |          |          |          | inancing |
   |          |          |          |          |          | Admini   |
   |          |          |          |          |          | stration |
   |          |          |          |          |          | (HCFA)   |
   |          |          |          |          |          | Common   |
   |          |          |          |          |          | P        |
   |          |          |          |          |          | rocedure |
   |          |          |          |          |          | Coding   |
   |          |          |          |          |          | System   |
   |          |          |          |          |          | (HCPCS)  |
   +----------+----------+----------+----------+----------+----------+
   | I10      | 2.16.8   | ICD-10   | WHO      |          | Inter    |
   |          | 40.1.​11 |          |          |          | national |
   |          | 3883.6.3 |          |          |          | Classi   |
   |          |          |          |          |          | fication |
   |          |          |          |          |          | of       |
   |          |          |          |          |          | Diseases |
   |          |          |          |          |          | revision |
   |          |          |          |          |          | 10       |
   |          |          |          |          |          | (ICD-10) |
   +----------+----------+----------+----------+----------+----------+
   | I10P     | 2.16.8   | IC       | US DHHS  |          | ICD-10   |
   |          | 40.1.​11 | D-10-PCS | CMS      |          | P        |
   |          | 3883.6.4 |          |          |          | rocedure |
   |          |          |          |          |          | Coding   |
   |          |          |          |          |          | System   |
   |          |          |          |          |          | (ICD 10  |
   |          |          |          |          |          | PCS)     |
   +----------+----------+----------+----------+----------+----------+
   | I11      | 1.2.840. | ICD-11   | WHO      | DOC:     | Inter    |
   |          | ​10008.2 |          |          | `http:/  | national |
   |          | .​16.​10 |          |          | /​icd.wh | Classi   |
   |          |          |          |          | o.int/​b | fication |
   |          |          |          |          | rowse11/ | of       |
   |          |          |          |          | ​l-m/​en | Diseases |
   |          |          |          |          |  <http:/ | revision |
   |          |          |          |          | /icd.who | 11       |
   |          |          |          |          | .int/bro | (ICD-11) |
   |          |          |          |          | wse11/l- |          |
   |          |          |          |          | m/en>`__ |          |
   +----------+----------+----------+----------+----------+----------+
   | I9       | 2.16.84  | ICD-9    | WHO      |          | Inter    |
   |          | 0.1.​113 |          |          |          | national |
   |          | 883.6.42 |          |          |          | Classi   |
   |          |          |          |          |          | fication |
   |          |          |          |          |          | of       |
   |          |          |          |          |          | Diseases |
   |          |          |          |          |          | revision |
   |          |          |          |          |          | 9        |
   |          |          |          |          |          | (ICD-9)  |
   +----------+----------+----------+----------+----------+----------+
   | I9C      | 2.16.8   | ICD-9-CM |          |          | Inter    |
   |          | 40.1.​11 |          |          |          | national |
   |          | 3883.6.2 |          |          |          | Classi   |
   |          |          |          |          |          | fication |
   |          |          |          |          |          | of       |
   |          |          |          |          |          | Diseases |
   |          |          |          |          |          | revision |
   |          |          |          |          |          | 9, with  |
   |          |          |          |          |          | Clinical |
   |          |          |          |          |          | Modif    |
   |          |          |          |          |          | ications |
   |          |          |          |          |          | (I       |
   |          |          |          |          |          | CD-9-CM) |
   +----------+----------+----------+----------+----------+----------+
   | IBSI     | 1.2.840  | Image    |          | DOC:     |          |
   |          | .10008.2 | B        |          | `http:// |          |
   |          | .​16.​13 | iomarker |          | ​arxiv.o |          |
   |          |          | Standar  |          | rg/​abs/ |          |
   |          |          | disation |          | ​1612.07 |          |
   |          |          | In       |          | 003 <htt |          |
   |          |          | itiative |          | p://arxi |          |
   |          |          |          |          | v.org/ab |          |
   |          |          |          |          | s/1612.0 |          |
   |          |          |          |          | 7003>`__ |          |
   +----------+----------+----------+----------+----------+----------+
   | IETF4646 |          | RFC 4646 | IETF     | DOC:     | `        |
   |          |          |          |          | `http:// | biblioen |
   |          |          |          |          | ​tools.​ | try_titl |
   |          |          |          |          | ietf.​or | e <#bibl |
   |          |          |          |          | g/​html/ | io_RFC_4 |
   |          |          |          |          | ​rfc4646 | 646>`__, |
   |          |          |          |          |  <http:/ | Tags for |
   |          |          |          |          | /tools.i | Ide      |
   |          |          |          |          | etf.org/ | ntifying |
   |          |          |          |          | html/rfc | La       |
   |          |          |          |          | 4646>`__ | nguages, |
   |          |          |          |          |          | The      |
   |          |          |          |          |          | Internet |
   |          |          |          |          |          | Society  |
   |          |          |          |          |          | (2005)   |
   |          |          |          |          |          |          |
   |          |          |          |          |          | `biblioe |
   |          |          |          |          |          | ntry_tit |
   |          |          |          |          |          | le <#bib |
   |          |          |          |          |          | lio_RFC_ |
   |          |          |          |          |          | 4646>`__ |
   |          |          |          |          |          | has been |
   |          |          |          |          |          | su       |
   |          |          |          |          |          | perceded |
   |          |          |          |          |          | by       |
   |          |          |          |          |          | `        |
   |          |          |          |          |          | biblioen |
   |          |          |          |          |          | try_titl |
   |          |          |          |          |          | e <#bibl |
   |          |          |          |          |          | io_RFC_5 |
   |          |          |          |          |          | 646>`__. |
   +----------+----------+----------+----------+----------+----------+
   | ISO639_1 | 2.16.84  | ISO      | ISO      |          | `biblioe |
   |          | 0.1.​113 | 639-1    |          |          | ntry_tit |
   |          | 883.6.99 |          |          |          | le <#bib |
   |          |          |          |          |          | lio_ISO6 |
   |          |          |          |          |          | 39-1>`__ |
   |          |          |          |          |          | Tw       |
   |          |          |          |          |          | o-letter |
   |          |          |          |          |          | language |
   |          |          |          |          |          | codes    |
   |          |          |          |          |          |          |
   |          |          |          |          |          | .        |
   |          |          |          |          |          | . note:: |
   |          |          |          |          |          |          |
   |          |          |          |          |          |    HL7   |
   |          |          |          |          |          |    uses  |
   |          |          |          |          |          |    "I    |
   |          |          |          |          |          | SO639-1" |
   |          |          |          |          |          |    for   |
   |          |          |          |          |          |    the   |
   |          |          |          |          |          |          |
   |          |          |          |          |          | symbolic |
   |          |          |          |          |          |    name, |
   |          |          |          |          |          |    with  |
   |          |          |          |          |          |    a     |
   |          |          |          |          |          |          |
   |          |          |          |          |          |   hyphen |
   |          |          |          |          |          |          |
   |          |          |          |          |          |   rather |
   |          |          |          |          |          |    than  |
   |          |          |          |          |          |    an    |
   |          |          |          |          |          |    un    |
   |          |          |          |          |          | derscore |
   +----------+----------+----------+----------+----------+----------+
   | ISO639_2 | 2.16.840 | ISO      | ISO      |          | `biblioe |
   |          | .1.​1138 | 639-2    |          |          | ntry_tit |
   |          | 83.6.100 |          |          |          | le <#bib |
   |          |          |          |          |          | lio_ISO6 |
   |          |          |          |          |          | 39-2>`__ |
   |          |          |          |          |          | Thre     |
   |          |          |          |          |          | e-letter |
   |          |          |          |          |          | language |
   |          |          |          |          |          | codes    |
   |          |          |          |          |          |          |
   |          |          |          |          |          | .        |
   |          |          |          |          |          | . note:: |
   |          |          |          |          |          |          |
   |          |          |          |          |          |    HL7   |
   |          |          |          |          |          |    uses  |
   |          |          |          |          |          |    "I    |
   |          |          |          |          |          | SO639-2" |
   |          |          |          |          |          |    for   |
   |          |          |          |          |          |    the   |
   |          |          |          |          |          |          |
   |          |          |          |          |          | symbolic |
   |          |          |          |          |          |    name, |
   |          |          |          |          |          |    with  |
   |          |          |          |          |          |    a     |
   |          |          |          |          |          |          |
   |          |          |          |          |          |   hyphen |
   |          |          |          |          |          |          |
   |          |          |          |          |          |   rather |
   |          |          |          |          |          |    than  |
   |          |          |          |          |          |    an    |
   |          |          |          |          |          |    un    |
   |          |          |          |          |          | derscore |
   +----------+----------+----------+----------+----------+----------+
   | I        | 2.16.1   | ISO      | ISO      |          | `        |
   | SO3166_1 |          | 3166-1   |          |          | biblioen |
   |          |          |          |          |          | try_titl |
   |          |          |          |          |          | e <#bibl |
   |          |          |          |          |          | io_ISO31 |
   |          |          |          |          |          | 66-1>`__ |
   |          |          |          |          |          | alpha-2  |
   |          |          |          |          |          | Country  |
   |          |          |          |          |          | Codes    |
   |          |          |          |          |          |          |
   |          |          |          |          |          | .        |
   |          |          |          |          |          | . note:: |
   |          |          |          |          |          |          |
   |          |          |          |          |          |    HL7   |
   |          |          |          |          |          |    uses  |
   |          |          |          |          |          |    "IS   |
   |          |          |          |          |          | O3166-1" |
   |          |          |          |          |          |    for   |
   |          |          |          |          |          |    the   |
   |          |          |          |          |          |          |
   |          |          |          |          |          | symbolic |
   |          |          |          |          |          |    name, |
   |          |          |          |          |          |    with  |
   |          |          |          |          |          |    a     |
   |          |          |          |          |          |          |
   |          |          |          |          |          |   hyphen |
   |          |          |          |          |          |          |
   |          |          |          |          |          |   rather |
   |          |          |          |          |          |    than  |
   |          |          |          |          |          |    an    |
   |          |          |          |          |          |    un    |
   |          |          |          |          |          | derscore |
   +----------+----------+----------+----------+----------+----------+
   | I        |          | ISO      | ISO      |          | Repres   |
   | SO5218_1 |          | 5218-1   |          |          | entation |
   |          |          |          |          |          | of Human |
   |          |          |          |          |          | Sexes    |
   |          |          |          |          |          | (not     |
   |          |          |          |          |          | used)    |
   |          |          |          |          |          |          |
   |          |          |          |          |          | IS       |
   |          |          |          |          |          | O5218_1, |
   |          |          |          |          |          | which    |
   |          |          |          |          |          | uses     |
   |          |          |          |          |          | numeric  |
   |          |          |          |          |          | codes,   |
   |          |          |          |          |          | was      |
   |          |          |          |          |          | im       |
   |          |          |          |          |          | properly |
   |          |          |          |          |          | s        |
   |          |          |          |          |          | pecified |
   |          |          |          |          |          | in CID   |
   |          |          |          |          |          | 7455 Sex |
   |          |          |          |          |          | in       |
   |          |          |          |          |          | earlier  |
   |          |          |          |          |          | editions |
   |          |          |          |          |          | of the   |
   |          |          |          |          |          | S        |
   |          |          |          |          |          | tandard. |
   |          |          |          |          |          | The      |
   |          |          |          |          |          | al       |
   |          |          |          |          |          | phabetic |
   |          |          |          |          |          | codes    |
   |          |          |          |          |          | im       |
   |          |          |          |          |          | properly |
   |          |          |          |          |          | at       |
   |          |          |          |          |          | tributed |
   |          |          |          |          |          | to that  |
   |          |          |          |          |          | coding   |
   |          |          |          |          |          | scheme   |
   |          |          |          |          |          | have     |
   |          |          |          |          |          | been     |
   |          |          |          |          |          | added to |
   |          |          |          |          |          | the      |
   |          |          |          |          |          | DICOM    |
   |          |          |          |          |          | Co       |
   |          |          |          |          |          | ntrolled |
   |          |          |          |          |          | Term     |
   |          |          |          |          |          | inology, |
   |          |          |          |          |          | and thus |
   |          |          |          |          |          | all      |
   |          |          |          |          |          | re       |
   |          |          |          |          |          | ferences |
   |          |          |          |          |          | to       |
   |          |          |          |          |          | coding   |
   |          |          |          |          |          | scheme   |
   |          |          |          |          |          | I        |
   |          |          |          |          |          | SO5218_1 |
   |          |          |          |          |          | should   |
   |          |          |          |          |          | be       |
   |          |          |          |          |          | co       |
   |          |          |          |          |          | nsidered |
   |          |          |          |          |          | eq       |
   |          |          |          |          |          | uivalent |
   |          |          |          |          |          | to       |
   |          |          |          |          |          | coding   |
   |          |          |          |          |          | scheme   |
   |          |          |          |          |          | DCM.     |
   +----------+----------+----------+----------+----------+----------+
   | ISO_OID  |          | ISO OID  | ISO      |          | `        |
   |          |          |          |          |          | biblioen |
   |          |          |          |          |          | try_titl |
   |          |          |          |          |          | e <#bibl |
   |          |          |          |          |          | io_ISO88 |
   |          |          |          |          |          | 24-1>`__ |
   |          |          |          |          |          | ISO/IEC  |
   |          |          |          |          |          | 8824-1-  |
   |          |          |          |          |          | Inf      |
   |          |          |          |          |          | ormation |
   |          |          |          |          |          | Te       |
   |          |          |          |          |          | chnology |
   |          |          |          |          |          | -        |
   |          |          |          |          |          | Abstract |
   |          |          |          |          |          | Syntax 1 |
   |          |          |          |          |          | (ASN.1): |
   |          |          |          |          |          | Speci    |
   |          |          |          |          |          | fication |
   |          |          |          |          |          | of Basic |
   |          |          |          |          |          | N        |
   |          |          |          |          |          | otation, |
   |          |          |          |          |          | and      |
   |          |          |          |          |          | `        |
   |          |          |          |          |          | biblioen |
   |          |          |          |          |          | try_titl |
   |          |          |          |          |          | e <#bibl |
   |          |          |          |          |          | io_ISO98 |
   |          |          |          |          |          | 34-1>`__ |
   |          |          |          |          |          | -        |
   |          |          |          |          |          | Inf      |
   |          |          |          |          |          | ormation |
   |          |          |          |          |          | te       |
   |          |          |          |          |          | chnology |
   |          |          |          |          |          | - Open   |
   |          |          |          |          |          | Systems  |
   |          |          |          |          |          | Interco  |
   |          |          |          |          |          | nnection |
   |          |          |          |          |          | -        |
   |          |          |          |          |          | Pr       |
   |          |          |          |          |          | ocedures |
   |          |          |          |          |          | for the  |
   |          |          |          |          |          | o        |
   |          |          |          |          |          | peration |
   |          |          |          |          |          | of OSI   |
   |          |          |          |          |          | Regi     |
   |          |          |          |          |          | stration |
   |          |          |          |          |          | Auth     |
   |          |          |          |          |          | orities: |
   |          |          |          |          |          | General  |
   |          |          |          |          |          | pr       |
   |          |          |          |          |          | ocedures |
   |          |          |          |          |          | and top  |
   |          |          |          |          |          | arcs of  |
   |          |          |          |          |          | the      |
   |          |          |          |          |          | ASN.1    |
   |          |          |          |          |          | Object   |
   |          |          |          |          |          | Id       |
   |          |          |          |          |          | entifier |
   |          |          |          |          |          | tree     |
   +----------+----------+----------+----------+----------+----------+
   | ITIS_TSN | 1.2.840  | ITIS TSN | ITIS     | DOC:     | A        |
   |          | .10008.​ |          |          | `http:// | T        |
   |          | 2.​16.​7 |          |          | ​www.​it | axonomic |
   |          |          |          |          | is.​gov  | Serial   |
   |          |          |          |          | <http:// | Number   |
   |          |          |          |          | www.itis | (TSN) is |
   |          |          |          |          | .gov>`__ | a        |
   |          |          |          |          |          | unique,  |
   |          |          |          |          |          | per      |
   |          |          |          |          |          | sistent, |
   |          |          |          |          |          | non-int  |
   |          |          |          |          |          | elligent |
   |          |          |          |          |          | id       |
   |          |          |          |          |          | entifier |
   |          |          |          |          |          | for a    |
   |          |          |          |          |          | sc       |
   |          |          |          |          |          | ientific |
   |          |          |          |          |          | name in  |
   |          |          |          |          |          | the      |
   |          |          |          |          |          | context  |
   |          |          |          |          |          | of the   |
   |          |          |          |          |          | In       |
   |          |          |          |          |          | tegrated |
   |          |          |          |          |          | T        |
   |          |          |          |          |          | axonomic |
   |          |          |          |          |          | Inf      |
   |          |          |          |          |          | ormation |
   |          |          |          |          |          | System   |
   |          |          |          |          |          | (ITIS).  |
   +----------+----------+----------+----------+----------+----------+
   | LN       | 2.16.8   | LOINC    | Reg      | DOC:     | `bibl    |
   |          | 40.1.​11 |          | enstrief | `ht      | ioentry_ |
   |          | 3883.6.1 |          | I        | tp://​lo | title <# |
   |          |          |          | nstitute | inc.​org | biblio_L |
   |          |          |          |          | / <http: | OINC>`__ |
   |          |          |          |          | //loinc. | Logical  |
   |          |          |          |          | org/>`__ | Obs      |
   |          |          |          |          |          | ervation |
   |          |          |          |          |          | Id       |
   |          |          |          |          |          | entifier |
   |          |          |          |          |          | Names    |
   |          |          |          |          |          | and      |
   |          |          |          |          |          | Codes    |
   +----------+----------+----------+----------+----------+----------+
   | MA       | 1.2.840  | Adult    | The      | DOC:     | Hayamizu |
   |          | .10008.​ | Mouse    | Jackson  | `        | TF,      |
   |          | 2.​16.​5 | Anatomy  | La       | http://​ | Mangan   |
   |          |          | Ontology | boratory | www.​inf | M,       |
   |          |          |          |          | ormatics | Corradi  |
   |          |          |          |          | .​jax.​o | JP,      |
   |          |          |          |          | rg/​sear | Kadin    |
   |          |          |          |          | ches/​AM | JA,      |
   |          |          |          |          | A.​cgi?​ | Ringwald |
   |          |          |          |          | id=MA:00 | M. The   |
   |          |          |          |          | 02405 <h | Adult    |
   |          |          |          |          | ttp://ww | Mouse    |
   |          |          |          |          | w.inform | An       |
   |          |          |          |          | atics.ja | atomical |
   |          |          |          |          | x.org/se | Dic      |
   |          |          |          |          | arches/A | tionary: |
   |          |          |          |          | MA.cgi?i | a tool   |
   |          |          |          |          | d=MA:000 | for      |
   |          |          |          |          | 2405>`__ | an       |
   |          |          |          |          |          | notating |
   |          |          |          |          |          | and      |
   |          |          |          |          |          | int      |
   |          |          |          |          |          | egrating |
   |          |          |          |          |          | data.    |
   |          |          |          |          |          | Genome   |
   |          |          |          |          |          | Biology  |
   |          |          |          |          |          | 2005;6   |
   |          |          |          |          |          | (3):R29. |
   |          |          |          |          |          | doi:     |
   |          |          |          |          |          | 10.1186/ |
   |          |          |          |          |          | gb-2005- |
   |          |          |          |          |          | 6-3-r29. |
   |          |          |          |          |          | `http:/  |
   |          |          |          |          |          | /​www.​n |
   |          |          |          |          |          | cbi.​nlm |
   |          |          |          |          |          | .​nih.​g |
   |          |          |          |          |          | ov/​pmc/ |
   |          |          |          |          |          | ​article |
   |          |          |          |          |          | s/​PMC10 |
   |          |          |          |          |          | 88948/ < |
   |          |          |          |          |          | http://w |
   |          |          |          |          |          | ww.ncbi. |
   |          |          |          |          |          | nlm.nih. |
   |          |          |          |          |          | gov/pmc/ |
   |          |          |          |          |          | articles |
   |          |          |          |          |          | /PMC1088 |
   |          |          |          |          |          | 948/>`__ |
   +----------+----------+----------+----------+----------+----------+
   | MAYOASRG | 1.2.840. | Mayo     |          |          | The      |
   |          | ​10008.2 | Clinic   |          |          | numeric  |
   |          | .​16.​12 | Non-radi |          |          | code of  |
   |          |          | ological |          |          | entries  |
   |          |          | Images   |          |          | in the   |
   |          |          | Specific |          |          | Mayo     |
   |          |          | Body     |          |          | Clinic   |
   |          |          | S        |          |          | Non-radi |
   |          |          | tructure |          |          | ological |
   |          |          | An       |          |          | Images   |
   |          |          | atomical |          |          | Specific |
   |          |          | Surface  |          |          | Body     |
   |          |          | Region   |          |          | S        |
   |          |          | Guide    |          |          | tructure |
   |          |          |          |          |          | An       |
   |          |          |          |          |          | atomical |
   |          |          |          |          |          | Surface  |
   |          |          |          |          |          | Region   |
   |          |          |          |          |          | Guide.   |
   +----------+----------+----------+----------+----------+----------+
   | MDC      | 2.16.84  |          |          |          | ISO/IEEE |
   |          | 0.1.​113 |          |          |          | 11073    |
   |          | 883.6.24 |          |          |          | Medical  |
   |          |          |          |          |          | Device   |
   |          |          |          |          |          | Nomen    |
   |          |          |          |          |          | clature, |
   |          |          |          |          |          | i        |
   |          |          |          |          |          | ncluding |
   |          |          |          |          |          | all its  |
   |          |          |          |          |          | sub      |
   |          |          |          |          |          | sections |
   |          |          |          |          |          | (`bib    |
   |          |          |          |          |          | lioentry |
   |          |          |          |          |          | _title < |
   |          |          |          |          |          | #biblio_ |
   |          |          |          |          |          | ISOIEEE_ |
   |          |          |          |          |          | 11073_10 |
   |          |          |          |          |          | 101>`__, |
   |          |          |          |          |          | `bibl    |
   |          |          |          |          |          | ioentry_ |
   |          |          |          |          |          | title <# |
   |          |          |          |          |          | biblio_I |
   |          |          |          |          |          | SOIEEE_1 |
   |          |          |          |          |          | 1073_101 |
   |          |          |          |          |          | 01a>`__, |
   |          |          |          |          |          | `bib     |
   |          |          |          |          |          | lioentry |
   |          |          |          |          |          | _title < |
   |          |          |          |          |          | #biblio_ |
   |          |          |          |          |          | ISOIEEE_ |
   |          |          |          |          |          | 11073_10 |
   |          |          |          |          |          | 102>`__, |
   |          |          |          |          |          | etc.),   |
   |          |          |          |          |          | encoded  |
   |          |          |          |          |          | as       |
   |          |          |          |          |          | decimal  |
   |          |          |          |          |          | strings  |
   |          |          |          |          |          | <part    |
   |          |          |          |          |          | ition>:< |
   |          |          |          |          |          | element> |
   +----------+----------+----------+----------+----------+----------+
   | MDNS     |          |          |          |          | U        |
   |          |          |          |          |          | niversal |
   |          |          |          |          |          | Medical  |
   |          |          |          |          |          | Device   |
   |          |          |          |          |          | (UMD)    |
   |          |          |          |          |          | Nome     |
   |          |          |          |          |          | nclature |
   |          |          |          |          |          | System   |
   +----------+----------+----------+----------+----------+----------+
   | MGI      | 1.2.840  | MGI      | The      | DOC:     | The MGI  |
   |          | .10008.​ |          | Jackson  | `http:/  | ID from  |
   |          | 2.​16.​8 |          | La       | /​www.​i | the      |
   |          |          |          | boratory | nformati | Mouse    |
   |          |          |          |          | cs.​jax. | Genome   |
   |          |          |          |          | ​org/​mg | In       |
   |          |          |          |          | ihome/​n | itiative |
   |          |          |          |          | omen/ <h | (MGI)    |
   |          |          |          |          | ttp://ww | nomen    |
   |          |          |          |          | w.inform | clature. |
   |          |          |          |          | atics.ja |          |
   |          |          |          |          | x.org/mg |          |
   |          |          |          |          | ihome/no |          |
   |          |          |          |          | men/>`__ |          |
   +----------+----------+----------+----------+----------+----------+
   | MSH      | 2.16.840 | MeSH     | NLM      | DOC:     | US       |
   |          | .1.​1138 |          |          | `http:// | National |
   |          | 83.6.177 |          |          | ​www.​nl | Library  |
   |          |          |          |          | m.​nih.​ | of       |
   |          |          |          |          | gov/​mes | Medicine |
   |          |          |          |          | h/​meshh | (NLM)    |
   |          |          |          |          | ome.​htm | Medical  |
   |          |          |          |          | l <http: | Subject  |
   |          |          |          |          | //www.nl | Headings |
   |          |          |          |          | m.nih.go | (MeSH)   |
   |          |          |          |          | v/mesh/m |          |
   |          |          |          |          | eshhome. |          |
   |          |          |          |          | html>`__ |          |
   +----------+----------+----------+----------+----------+----------+
   | NBD      | 2.16.84  |          |          |          | NA       |
   |          | 0.1.​113 |          |          |          | SPE/BPEG |
   |          | 883.15.2 |          |          |          | Defib    |
   |          |          |          |          |          | rillator |
   |          |          |          |          |          | Code     |
   |          |          |          |          |          |          |
   |          |          |          |          |          | B        |
   |          |          |          |          |          | ernstein |
   |          |          |          |          |          | AD, et   |
   |          |          |          |          |          | al."The  |
   |          |          |          |          |          | NA       |
   |          |          |          |          |          | SPE/BPEG |
   |          |          |          |          |          | Defib    |
   |          |          |          |          |          | rillator |
   |          |          |          |          |          | Code"    |
   |          |          |          |          |          | PACE,    |
   |          |          |          |          |          | 16:17    |
   |          |          |          |          |          | 76-1780, |
   |          |          |          |          |          | 1993     |
   +----------+----------+----------+----------+----------+----------+
   | NBG      | 2.16.84  |          |          | DOC:     | NA       |
   |          | 0.1.​113 |          |          | `ht      | SPE/BPEG |
   |          | 883.15.3 |          |          | tp://www | Generic  |
   |          |          |          |          | .​hrsonl | P        |
   |          |          |          |          | ine.​org | acemaker |
   |          |          |          |          | /​Practi | Code     |
   |          |          |          |          | ce-​Guid | (2000)   |
   |          |          |          |          | ance/​Cl |          |
   |          |          |          |          | inical-​ | B        |
   |          |          |          |          | Guidelin | ernstein |
   |          |          |          |          | es-​Docu | AD, et   |
   |          |          |          |          | ments/​2 | al."The  |
   |          |          |          |          | 002-​The | Revised  |
   |          |          |          |          | -​Revise | NA       |
   |          |          |          |          | d-​NASPE | SPE/BPEG |
   |          |          |          |          | -​BPEG​- | Generic  |
   |          |          |          |          | ​Generic | Code for |
   |          |          |          |          | -​Code-​ | antibrad |
   |          |          |          |          | for-​Ant | ycardia, |
   |          |          |          |          | ibradyca | adapti   |
   |          |          |          |          | rdia-​​A | ve-rate, |
   |          |          |          |          | daptiveR | and      |
   |          |          |          |          | ate-​and | m        |
   |          |          |          |          | -​Multis | ultisite |
   |          |          |          |          | ite-​Pac | pacing." |
   |          |          |          |          | ing <htt | Pacing   |
   |          |          |          |          | p://www. | Clin     |
   |          |          |          |          | hrsonlin | Electrop |
   |          |          |          |          | e.org/Pr | hysiol., |
   |          |          |          |          | actice-G | 25:      |
   |          |          |          |          | uidance/ | 260-264, |
   |          |          |          |          | Clinical | 2002     |
   |          |          |          |          | -Guideli |          |
   |          |          |          |          | nes-Docu | See      |
   |          |          |          |          | ments/20 | `http    |
   |          |          |          |          | 02-The-R | ://​www. |
   |          |          |          |          | evised-N | ​hrsonli |
   |          |          |          |          | ASPE-BPE | ne.​org/ |
   |          |          |          |          | G-Generi | ​Practic |
   |          |          |          |          | c-Code-f | e-​Guida |
   |          |          |          |          | or-Antib | nce/​Cli |
   |          |          |          |          | radycard | nical-​G |
   |          |          |          |          | ia-Adapt | uideline |
   |          |          |          |          | iveRate- | s-​Docum |
   |          |          |          |          | and-Mult | ents/​20 |
   |          |          |          |          | isite-Pa | 02-​The- |
   |          |          |          |          | cing>`__ | ​Revised |
   |          |          |          |          |          | -​NASPE- |
   |          |          |          |          |          | ​BPEG​-​ |
   |          |          |          |          |          | Generic- |
   |          |          |          |          |          | ​Code-​f |
   |          |          |          |          |          | or-​Anti |
   |          |          |          |          |          | bradycar |
   |          |          |          |          |          | dia-​​Ad |
   |          |          |          |          |          | aptiveRa |
   |          |          |          |          |          | te-​and- |
   |          |          |          |          |          | ​Multisi |
   |          |          |          |          |          | te-​Paci |
   |          |          |          |          |          | ng <http |
   |          |          |          |          |          | ://www.h |
   |          |          |          |          |          | rsonline |
   |          |          |          |          |          | .org/Pra |
   |          |          |          |          |          | ctice-Gu |
   |          |          |          |          |          | idance/C |
   |          |          |          |          |          | linical- |
   |          |          |          |          |          | Guidelin |
   |          |          |          |          |          | es-Docum |
   |          |          |          |          |          | ents/200 |
   |          |          |          |          |          | 2-The-Re |
   |          |          |          |          |          | vised-NA |
   |          |          |          |          |          | SPE-BPEG |
   |          |          |          |          |          | -Generic |
   |          |          |          |          |          | -Code-fo |
   |          |          |          |          |          | r-Antibr |
   |          |          |          |          |          | adycardi |
   |          |          |          |          |          | a-Adapti |
   |          |          |          |          |          | veRate-a |
   |          |          |          |          |          | nd-Multi |
   |          |          |          |          |          | site-Pac |
   |          |          |          |          |          | ing>`__. |
   +----------+----------+----------+----------+----------+----------+
   | NCDR     |          |          |          |          | American |
   |          |          |          |          |          | College  |
   |          |          |          |          |          | of       |
   |          |          |          |          |          | Ca       |
   |          |          |          |          |          | rdiology |
   |          |          |          |          |          | National |
   |          |          |          |          |          | Cardio   |
   |          |          |          |          |          | vascular |
   |          |          |          |          |          | Data     |
   |          |          |          |          |          | R        |
   |          |          |          |          |          | egistry™ |
   |          |          |          |          |          | Cath Lab |
   |          |          |          |          |          | Module   |
   |          |          |          |          |          | Version  |
   |          |          |          |          |          | 1.1,     |
   |          |          |          |          |          | 1997;    |
   |          |          |          |          |          | Version  |
   |          |          |          |          |          | 2.0b,    |
   |          |          |          |          |          | 1999     |
   +----------+----------+----------+----------+----------+----------+
   | NCIt     | 2.1      | NCI      | NCI      | DOC:     |          |
   |          | 6.840.1. | T        |          | `ht      |          |
   |          | ​113883. | hesaurus |          | tp://​nc |          |
   |          | 3.26.1.1 |          |          | it.​nci. |          |
   |          |          |          |          | ​nih.​go |          |
   |          |          |          |          | v/ <http |          |
   |          |          |          |          | ://ncit. |          |
   |          |          |          |          | nci.nih. |          |
   |          |          |          |          | gov/>`__ |          |
   +----------+----------+----------+----------+----------+----------+
   | NDC      | 2.16.8   | National | US FDA   | DOC:     | The code |
   |          | 40.1.113 | Drug     |          | `http:/  | value is |
   |          | 883.6.69 | Code     |          | /​www.fd | the 10   |
   |          |          | D        |          | a.gov/​D | digit 3  |
   |          |          | irectory |          | rugs/​In | segment  |
   |          |          |          |          | formatio | NDC code |
   |          |          |          |          | n​​OnDru | with "-" |
   |          |          |          |          | gs/​ucm1 | between  |
   |          |          |          |          | 42438.ht | segments |
   |          |          |          |          | m <http: | included |
   |          |          |          |          | //www.fd | and no   |
   |          |          |          |          | a.gov/Dr | asterisk |
   |          |          |          |          | ugs/Info | (leading |
   |          |          |          |          | rmationO | zero     |
   |          |          |          |          | nDrugs/u | place    |
   |          |          |          |          | cm142438 | holder). |
   |          |          |          |          | .htm>`__ |          |
   |          |          |          |          |          |          |
   |          |          |          |          | DOC:     |          |
   |          |          |          |          | `h       |          |
   |          |          |          |          | ttp://​w |          |
   |          |          |          |          | ww.hl7.o |          |
   |          |          |          |          | rg/​fhir |          |
   |          |          |          |          | /​ndc.ht |          |
   |          |          |          |          | ml <http |          |
   |          |          |          |          | ://www.h |          |
   |          |          |          |          | l7.org/f |          |
   |          |          |          |          | hir/ndc. |          |
   |          |          |          |          | html>`__ |          |
   +----------+----------+----------+----------+----------+----------+
   | NEU      | 2.16.840 | Ne       |          | DOC:     | The      |
   |          | .1.​1138 | uroNames |          | `htt     | numeric  |
   |          | 83.6.210 |          |          | p://​bra | bra      |
   |          |          |          |          | ininfo.​ | inInfoID |
   |          |          |          |          | rprc.​wa | is used  |
   |          |          |          |          | shington | as the   |
   |          |          |          |          | .​edu​/a | code     |
   |          |          |          |          | boutBrai | value.   |
   |          |          |          |          | nInfo.​a | See      |
   |          |          |          |          | spx​#Neu |          |
   |          |          |          |          | roNames  |          |
   |          |          |          |          | <http:// |          |
   |          |          |          |          | braininf |          |
   |          |          |          |          | o.rprc.w |          |
   |          |          |          |          | ashingto |          |
   |          |          |          |          | n.edu/ab |          |
   |          |          |          |          | outBrain |          |
   |          |          |          |          | Info.asp |          |
   |          |          |          |          | x#NeuroN |          |
   |          |          |          |          | ames>`__ |          |
   +----------+----------+----------+----------+----------+----------+
   | NICIP    | 2.16.840 | NICIP    | UK NHS   | DOC:     | UK       |
   |          | .1.​1138 |          |          | `http:   | National |
   |          | 83.2.1.​ |          |          | //​digit | Health   |
   |          | 3.2.4.21 |          |          | al.​nhs. | Service  |
   |          |          |          |          | ​uk/​art | National |
   |          |          |          |          | icle/​11 | Interim  |
   |          |          |          |          | 08/​Nati | Clinical |
   |          |          |          |          | onal-​In | Imaging  |
   |          |          |          |          | terim-​C | Pr       |
   |          |          |          |          | linical- | ocedures |
   |          |          |          |          | ​Imaging | (NICIP)  |
   |          |          |          |          | -​Proced | Short    |
   |          |          |          |          | ure-​NIC | Code     |
   |          |          |          |          | IP-​Code | (e.g.,   |
   |          |          |          |          | -​Set <h | "CCHAPC" |
   |          |          |          |          | ttp://di | for CT   |
   |          |          |          |          | gital.nh | Thorax   |
   |          |          |          |          | s.uk/art | abdomen  |
   |          |          |          |          | icle/110 | pelvis   |
   |          |          |          |          | 8/Nation | with     |
   |          |          |          |          | al-Inter | c        |
   |          |          |          |          | im-Clini | ontrast) |
   |          |          |          |          | cal-Imag |          |
   |          |          |          |          | ing-Proc |          |
   |          |          |          |          | edure-NI |          |
   |          |          |          |          | CIP-Code |          |
   |          |          |          |          | -Set>`__ |          |
   +----------+----------+----------+----------+----------+----------+
   | NPI      |          |          |          |          | HCFA     |
   |          |          |          |          |          | National |
   |          |          |          |          |          | Provider |
   |          |          |          |          |          | Id       |
   |          |          |          |          |          | entifier |
   +----------+----------+----------+----------+----------+----------+
   | NYUMCCG  | 1.2.840. | New York |          | DOC:     | The      |
   |          | ​10008.2 | Un       |          | `ht      | numeric  |
   |          | .​16.​11 | iversity |          | tp://​ww | code of  |
   |          |          | Melanoma |          | w.anatom | entries  |
   |          |          | Clinical |          | ymapper. | in the   |
   |          |          | Coo      |          | com/​nyu | New York |
   |          |          | perative |          | / <http: | Un       |
   |          |          | Group    |          | //www.an | iversity |
   |          |          |          |          | atomymap | Melanoma |
   |          |          |          |          | per.com/ | Clinical |
   |          |          |          |          | nyu/>`__ | Coo      |
   |          |          |          |          |          | perative |
   |          |          |          |          |          | Group's  |
   |          |          |          |          |          | n        |
   |          |          |          |          |          | umbering |
   |          |          |          |          |          | system.  |
   +----------+----------+----------+----------+----------+----------+
   | PATHLEX  | 1.       | PathLex  | IHE      | DOC:     | The      |
   |          | 3.6.1.4. |          |          | `h       | numeric  |
   |          | 1.​19376 |          |          | ttp://​w | pat      |
   |          | .1.8.2.1 |          |          | ww.ihe.n | hLexCode |
   |          |          |          |          | et/​Tech | is used  |
   |          |          |          |          | nical​_F | as the   |
   |          |          |          |          | ramework | code     |
   |          |          |          |          | /​upload | value.   |
   |          |          |          |          | /​IHE​_P |          |
   |          |          |          |          | AT​_Supp |          |
   |          |          |          |          | l​_APSR​ |          |
   |          |          |          |          | _Appendi |          |
   |          |          |          |          | x​_Value |          |
   |          |          |          |          | ​_Sets​_ |          |
   |          |          |          |          | 2011_03_ |          |
   |          |          |          |          | 31​.xls  |          |
   |          |          |          |          | <http:// |          |
   |          |          |          |          | www.ihe. |          |
   |          |          |          |          | net/Tech |          |
   |          |          |          |          | nical_Fr |          |
   |          |          |          |          | amework/ |          |
   |          |          |          |          | upload/I |          |
   |          |          |          |          | HE_PAT_S |          |
   |          |          |          |          | uppl_APS |          |
   |          |          |          |          | R_Append |          |
   |          |          |          |          | ix_Value |          |
   |          |          |          |          | _Sets_20 |          |
   |          |          |          |          | 11_03_31 |          |
   |          |          |          |          | .xls>`__ |          |
   |          |          |          |          |          |          |
   |          |          |          |          | DOC:     |          |
   |          |          |          |          | `h       |          |
   |          |          |          |          | ttp://​p |          |
   |          |          |          |          | url.bioo |          |
   |          |          |          |          | ntology. |          |
   |          |          |          |          | org/​ont |          |
   |          |          |          |          | ology/​P |          |
   |          |          |          |          | ATHLEX < |          |
   |          |          |          |          | http://p |          |
   |          |          |          |          | url.bioo |          |
   |          |          |          |          | ntology. |          |
   |          |          |          |          | org/onto |          |
   |          |          |          |          | logy/PAT |          |
   |          |          |          |          | HLEX>`__ |          |
   +----------+----------+----------+----------+----------+----------+
   | POS      | 2.16.84  |          |          |          | HCFA     |
   |          | 0.1.​113 |          |          |          | Place of |
   |          | 883.6.50 |          |          |          | Service  |
   |          |          |          |          |          | (POS)    |
   |          |          |          |          |          | Codes    |
   |          |          |          |          |          | for      |
   |          |          |          |          |          | Prof     |
   |          |          |          |          |          | essional |
   |          |          |          |          |          | Claims   |
   +----------+----------+----------+----------+----------+----------+
   | PUB      | 1.2.840  | PubChem  | NCBI     | DOC:     | US       |
   | CHEM_CID | .10008.​ |          |          | `htt     | National |
   |          | 2.​16.​9 |          |          | p://​pub | Center   |
   |          |          |          |          | chem.​nc | for      |
   |          |          |          |          | bi.​nlm. | Biote    |
   |          |          |          |          | ​nih.​go | chnology |
   |          |          |          |          | v/ <http | Inf      |
   |          |          |          |          | ://pubch | ormation |
   |          |          |          |          | em.ncbi. | (NCBI)   |
   |          |          |          |          | nlm.nih. | PubChem  |
   |          |          |          |          | gov/>`__ | Compound |
   |          |          |          |          |          | CID.     |
   +----------+----------+----------+----------+----------+----------+
   | RADLEX   | 2.16.840 | RadLex   | RSNA     | DOC:     | `bibli   |
   |          | .1.​1138 |          |          | `htt     | oentry_t |
   |          | 83.6.256 |          |          | p://​www | itle <#b |
   |          |          |          |          | .radlex. | iblio_Ra |
   |          |          |          |          | org/ <ht | dLex>`__ |
   |          |          |          |          | tp://www |          |
   |          |          |          |          | .radlex. |          |
   |          |          |          |          | org/>`__ |          |
   +----------+----------+----------+----------+----------+----------+
   | RA       | 1.2.840  | Ra       | RSNA     | DOC:     | `b       |
   | DELEMENT | .10008.2 | dElement |          | http:/   | iblioent |
   |          | .​16.​15 |          |          | /radelem | ry_title |
   |          |          |          |          | ent.org/ |  <#bibli |
   |          |          |          |          |          | o_RadEle |
   |          |          |          |          |          | ment>`__ |
   +----------+----------+----------+----------+----------+----------+
   | RFC3066  | 2.16.840 | RFC 3066 | IETF     | DOC:     | `        |
   |          | .1.​1138 |          |          | `http:   | biblioen |
   |          | 83.6.121 |          |          | //​tools | try_titl |
   |          |          |          |          | .ietf.or | e <#bibl |
   |          |          |          |          | g/​html/ | io_RFC_3 |
   |          |          |          |          | ​rfc3066 | 066>`__, |
   |          |          |          |          |  <http:/ | Tags for |
   |          |          |          |          | /tools.i | the      |
   |          |          |          |          | etf.org/ | Identi   |
   |          |          |          |          | html/rfc | fication |
   |          |          |          |          | 3066>`__ | of       |
   |          |          |          |          |          | La       |
   |          |          |          |          |          | nguages, |
   |          |          |          |          |          | Internet |
   |          |          |          |          |          | Eng      |
   |          |          |          |          |          | ineering |
   |          |          |          |          |          | Task     |
   |          |          |          |          |          | Force    |
   |          |          |          |          |          |          |
   |          |          |          |          |          | .        |
   |          |          |          |          |          | . note:: |
   |          |          |          |          |          |          |
   |          |          |          |          |          |    HL7   |
   |          |          |          |          |          |    uses  |
   |          |          |          |          |          |    "I    |
   |          |          |          |          |          | ETF3066" |
   |          |          |          |          |          |    for   |
   |          |          |          |          |          |    the   |
   |          |          |          |          |          |          |
   |          |          |          |          |          | symbolic |
   |          |          |          |          |          |    name. |
   |          |          |          |          |          |          |
   |          |          |          |          |          |          |
   |          |          |          |          |          | `biblioe |
   |          |          |          |          |          | ntry_tit |
   |          |          |          |          |          | le <#bib |
   |          |          |          |          |          | lio_RFC_ |
   |          |          |          |          |          | 3066>`__ |
   |          |          |          |          |          |    has   |
   |          |          |          |          |          |    been  |
   |          |          |          |          |          |    su    |
   |          |          |          |          |          | perseded |
   |          |          |          |          |          |    by    |
   |          |          |          |          |          |    `     |
   |          |          |          |          |          | biblioen |
   |          |          |          |          |          | try_titl |
   |          |          |          |          |          | e <#bibl |
   |          |          |          |          |          | io_RFC_4 |
   |          |          |          |          |          | 646>`__, |
   |          |          |          |          |          |    which |
   |          |          |          |          |          |    in    |
   |          |          |          |          |          |    turn  |
   |          |          |          |          |          |    has   |
   |          |          |          |          |          |    been  |
   |          |          |          |          |          |    su    |
   |          |          |          |          |          | perceded |
   |          |          |          |          |          |    by    |
   |          |          |          |          |          |    `     |
   |          |          |          |          |          | biblioen |
   |          |          |          |          |          | try_titl |
   |          |          |          |          |          | e <#bibl |
   |          |          |          |          |          | io_RFC_5 |
   |          |          |          |          |          | 646>`__. |
   +----------+----------+----------+----------+----------+----------+
   | RFC-3881 |          | RFC 3881 | IETF     | DOC:     | `        |
   |          |          |          |          | `http:   | biblioen |
   |          |          |          |          | //​tools | try_titl |
   |          |          |          |          | .ietf.or | e <#bibl |
   |          |          |          |          | g/​html/ | io_RFC_3 |
   |          |          |          |          | ​rfc3881 | 881>`__, |
   |          |          |          |          |  <http:/ | Security |
   |          |          |          |          | /tools.i | Audit    |
   |          |          |          |          | etf.org/ | and      |
   |          |          |          |          | html/rfc | Access   |
   |          |          |          |          | 3881>`__ | Accoun   |
   |          |          |          |          |          | tability |
   |          |          |          |          |          | Message  |
   |          |          |          |          |          | - XML    |
   |          |          |          |          |          | Data     |
   |          |          |          |          |          | Def      |
   |          |          |          |          |          | initions |
   |          |          |          |          |          | for      |
   |          |          |          |          |          | He       |
   |          |          |          |          |          | althcare |
   |          |          |          |          |          | Appl     |
   |          |          |          |          |          | ications |
   |          |          |          |          |          |          |
   |          |          |          |          |          | .        |
   |          |          |          |          |          | . note:: |
   |          |          |          |          |          |          |
   |          |          |          |          |          |    A     |
   |          |          |          |          |          |          |
   |          |          |          |          |          |   hyphen |
   |          |          |          |          |          |    is    |
   |          |          |          |          |          |    used  |
   |          |          |          |          |          |    in    |
   |          |          |          |          |          |    the   |
   |          |          |          |          |          |          |
   |          |          |          |          |          |   Coding |
   |          |          |          |          |          |          |
   |          |          |          |          |          |   Scheme |
   |          |          |          |          |          |    De    |
   |          |          |          |          |          | signator |
   |          |          |          |          |          |    for   |
   |          |          |          |          |          |    con   |
   |          |          |          |          |          | sistency |
   |          |          |          |          |          |    with  |
   |          |          |          |          |          |    hi    |
   |          |          |          |          |          | storical |
   |          |          |          |          |          |    use   |
   |          |          |          |          |          |    in    |
   |          |          |          |          |          |    IHE.  |
   |          |          |          |          |          |    See   |
   |          |          |          |          |          |    IHE   |
   |          |          |          |          |          |    ITI   |
   |          |          |          |          |          |    TF    |
   |          |          |          |          |          |          |
   |          |          |          |          |          |   Vol2a. |
   |          |          |          |          |          |          |
   |          |          |          |          |          |  Section |
   |          |          |          |          |          |    3.2   |
   |          |          |          |          |          | 0.7.1.3. |
   +----------+----------+----------+----------+----------+----------+
   | RFC5646  | 2.16.840 | RFC 5646 | IETF     | DOC:     | `        |
   |          | .1.​1138 |          |          | `http:   | biblioen |
   |          | 83.6.316 |          |          | //​tools | try_titl |
   |          |          |          |          | .ietf.or | e <#bibl |
   |          |          |          |          | g/​html/ | io_RFC_5 |
   |          |          |          |          | ​rfc5646 | 646>`__, |
   |          |          |          |          |  <http:/ | Tags for |
   |          |          |          |          | /tools.i | Ide      |
   |          |          |          |          | etf.org/ | ntifying |
   |          |          |          |          | html/rfc | La       |
   |          |          |          |          | 5646>`__ | nguages, |
   |          |          |          |          |          | The      |
   |          |          |          |          |          | Internet |
   |          |          |          |          |          | Society  |
   |          |          |          |          |          | (2009)   |
   |          |          |          |          |          |          |
   |          |          |          |          |          | .        |
   |          |          |          |          |          | . note:: |
   |          |          |          |          |          |          |
   |          |          |          |          |          |    The   |
   |          |          |          |          |          |    HL7   |
   |          |          |          |          |          |    OID   |
   |          |          |          |          |          |          |
   |          |          |          |          |          | Registry |
   |          |          |          |          |          |    s     |
   |          |          |          |          |          | pecifies |
   |          |          |          |          |          |    "r    |
   |          |          |          |          |          | fc5646", |
   |          |          |          |          |          |    not   |
   |          |          |          |          |          |    "ie   |
   |          |          |          |          |          | tf5646", |
   |          |          |          |          |          |    as    |
   |          |          |          |          |          |    the   |
   |          |          |          |          |          |          |
   |          |          |          |          |          |  Desired |
   |          |          |          |          |          |          |
   |          |          |          |          |          | Symbolic |
   |          |          |          |          |          |    Name  |
   |          |          |          |          |          |    (inco |
   |          |          |          |          |          | nsistent |
   |          |          |          |          |          |    with  |
   |          |          |          |          |          |    the   |
   |          |          |          |          |          |          |
   |          |          |          |          |          |  pattern |
   |          |          |          |          |          |    used  |
   |          |          |          |          |          |    for   |
   |          |          |          |          |          |    `b    |
   |          |          |          |          |          | iblioent |
   |          |          |          |          |          | ry_title |
   |          |          |          |          |          |  <#bibli |
   |          |          |          |          |          | o_RFC_46 |
   |          |          |          |          |          | 46>`__). |
   |          |          |          |          |          |          |
   |          |          |          |          |          |          |
   |          |          |          |          |          | `biblioe |
   |          |          |          |          |          | ntry_tit |
   |          |          |          |          |          | le <#bib |
   |          |          |          |          |          | lio_RFC_ |
   |          |          |          |          |          | 5646>`__ |
   |          |          |          |          |          |    con   |
   |          |          |          |          |          | stitutes |
   |          |          |          |          |          |    one   |
   |          |          |          |          |          |    part  |
   |          |          |          |          |          |    of    |
   |          |          |          |          |          |    IETF  |
   |          |          |          |          |          |    Best  |
   |          |          |          |          |          |          |
   |          |          |          |          |          |  Current |
   |          |          |          |          |          |          |
   |          |          |          |          |          | Practice |
   |          |          |          |          |          |    BCP   |
   |          |          |          |          |          |    47    |
   |          |          |          |          |          |    Tags  |
   |          |          |          |          |          |    for   |
   |          |          |          |          |          |    Ide   |
   |          |          |          |          |          | ntifying |
   |          |          |          |          |          |    La    |
   |          |          |          |          |          | nguages, |
   |          |          |          |          |          |    which |
   |          |          |          |          |          |    also  |
   |          |          |          |          |          |          |
   |          |          |          |          |          | includes |
   |          |          |          |          |          |          |
   |          |          |          |          |          | `biblioe |
   |          |          |          |          |          | ntry_tit |
   |          |          |          |          |          | le <#bib |
   |          |          |          |          |          | lio_RFC_ |
   |          |          |          |          |          | 4647>`__ |
   |          |          |          |          |          |          |
   |          |          |          |          |          | Matching |
   |          |          |          |          |          |    of    |
   |          |          |          |          |          |          |
   |          |          |          |          |          | Language |
   |          |          |          |          |          |    Tags; |
   |          |          |          |          |          |          |
   |          |          |          |          |          | `biblioe |
   |          |          |          |          |          | ntry_tit |
   |          |          |          |          |          | le <#bib |
   |          |          |          |          |          | lio_RFC_ |
   |          |          |          |          |          | 4647>`__ |
   |          |          |          |          |          |    is    |
   |          |          |          |          |          |    not   |
   |          |          |          |          |          |          |
   |          |          |          |          |          | relevant |
   |          |          |          |          |          |    in    |
   |          |          |          |          |          |    this  |
   |          |          |          |          |          |          |
   |          |          |          |          |          | context. |
   +----------+----------+----------+----------+----------+----------+
   | RO       | 1        | R        |          | DOC:     |          |
   |          | .2.840.​ | adiomics |          | `http:   |          |
   |          | 10008.​2 | Ontology |          | //​biopo |          |
   |          | .​16.​14 |          |          | rtal.bio |          |
   |          |          |          |          | ontology |          |
   |          |          |          |          | .org/​on |          |
   |          |          |          |          | tologies |          |
   |          |          |          |          | /​RO <ht |          |
   |          |          |          |          | tp://bio |          |
   |          |          |          |          | portal.b |          |
   |          |          |          |          | ioontolo |          |
   |          |          |          |          | gy.org/o |          |
   |          |          |          |          | ntologie |          |
   |          |          |          |          | s/RO>`__ |          |
   +----------+----------+----------+----------+----------+----------+
   | RXNORM   | 2.16.8   | RXNORM   | NLM      | DOC:     | RxNorm   |
   |          | 40.1.113 |          |          | `ht      | provides |
   |          | 883.6.88 |          |          | tp://​ww | no       |
   |          |          |          |          | w.nlm.ni | rmalized |
   |          |          |          |          | h.gov/​r | names    |
   |          |          |          |          | esearch/ | for      |
   |          |          |          |          | ​umls/​r | clinical |
   |          |          |          |          | xnorm/ < | drugs    |
   |          |          |          |          | http://w | and      |
   |          |          |          |          | ww.nlm.n | links    |
   |          |          |          |          | ih.gov/r | its      |
   |          |          |          |          | esearch/ | names to |
   |          |          |          |          | umls/rxn | many of  |
   |          |          |          |          | orm/>`__ | the drug |
   |          |          |          |          |          | voca     |
   |          |          |          |          |          | bularies |
   |          |          |          |          |          | commonly |
   |          |          |          |          |          | used in  |
   |          |          |          |          |          | pharmacy |
   |          |          |          |          |          | ma       |
   |          |          |          |          |          | nagement |
   |          |          |          |          |          | and drug |
   |          |          |          |          |          | int      |
   |          |          |          |          |          | eraction |
   |          |          |          |          |          | s        |
   |          |          |          |          |          | oftware. |
   +----------+----------+----------+----------+----------+----------+
   | 99SDM    | 2.16.84  | SDM      | DICOM    |          | SNOMED   |
   |          | 0.1.​113 |          |          |          | DICOM    |
   |          | 883.6.53 |          |          |          | Micro    |
   |          |          |          |          |          | glossary |
   |          |          |          |          |          | (        |
   |          |          |          |          |          | Retired) |
   |          |          |          |          |          | (see     |
   |          |          |          |          |          | `SNOMED  |
   |          |          |          |          |          | CT       |
   |          |          |          |          |          |  <#sect_ |
   |          |          |          |          |          | 8.1>`__) |
   +----------+----------+----------+----------+----------+----------+
   | SCPECG   |          |          |          |          | Standard |
   |          |          |          |          |          | Commun   |
   |          |          |          |          |          | ications |
   |          |          |          |          |          | Protocol |
   |          |          |          |          |          | for      |
   |          |          |          |          |          | C        |
   |          |          |          |          |          | omputer- |
   |          |          |          |          |          | Assisted |
   |          |          |          |          |          | Elec     |
   |          |          |          |          |          | trocardi |
   |          |          |          |          |          | ography, |
   |          |          |          |          |          | Draft    |
   |          |          |          |          |          | proposal |
   |          |          |          |          |          | for ISO  |
   |          |          |          |          |          | S        |
   |          |          |          |          |          | tandard, |
   |          |          |          |          |          | AAMI,    |
   |          |          |          |          |          | Revision |
   |          |          |          |          |          | 1.3      |
   +----------+----------+----------+----------+----------+----------+
   | SNM3     | 2.16.84  | SNOMED   | SNOMED   | DOC:     | SNOMED   |
   |          | 0.1.​113 | V3       | Inter    | `htt     | Inter    |
   |          | 883.6.51 |          | national | p://​www | national |
   |          |          |          |          | .snomed. | Version  |
   |          |          |          |          | org/ <ht | 3 (see   |
   |          |          |          |          | tp://www | `SNOMED  |
   |          |          |          |          | .snomed. | CT       |
   |          |          |          |          | org/>`__ |  <#sect_ |
   |          |          |          |          |          | 8.1>`__) |
   |          |          |          |          |          |          |
   |          |          |          |          |          | .        |
   |          |          |          |          |          | . note:: |
   |          |          |          |          |          |          |
   |          |          |          |          |          |    This  |
   |          |          |          |          |          |          |
   |          |          |          |          |          |   coding |
   |          |          |          |          |          |          |
   |          |          |          |          |          |   scheme |
   |          |          |          |          |          |    is    |
   |          |          |          |          |          |    dep   |
   |          |          |          |          |          | recated. |
   |          |          |          |          |          |    The   |
   |          |          |          |          |          |    use   |
   |          |          |          |          |          |    of    |
   |          |          |          |          |          |    "S    |
   |          |          |          |          |          | NOMED-RT |
   |          |          |          |          |          |          |
   |          |          |          |          |          |   style" |
   |          |          |          |          |          |    code  |
   |          |          |          |          |          |          |
   |          |          |          |          |          |   values |
   |          |          |          |          |          |    is no |
   |          |          |          |          |          |          |
   |          |          |          |          |          |   longer |
   |          |          |          |          |          |    au    |
   |          |          |          |          |          | thorized |
   |          |          |          |          |          |    by    |
   |          |          |          |          |          |          |
   |          |          |          |          |          |   SNOMED |
   |          |          |          |          |          |          |
   |          |          |          |          |          |   except |
   |          |          |          |          |          |    for   |
   |          |          |          |          |          |          |
   |          |          |          |          |          | creation |
   |          |          |          |          |          |    by    |
   |          |          |          |          |          |          |
   |          |          |          |          |          |   legacy |
   |          |          |          |          |          |          |
   |          |          |          |          |          | devices, |
   |          |          |          |          |          |          |
   |          |          |          |          |          |   legacy |
   |          |          |          |          |          |          |
   |          |          |          |          |          |  objects |
   |          |          |          |          |          |    in    |
   |          |          |          |          |          |    a     |
   |          |          |          |          |          | rchives, |
   |          |          |          |          |          |    and   |
   |          |          |          |          |          |    r     |
   |          |          |          |          |          | eceiving |
   |          |          |          |          |          |          |
   |          |          |          |          |          |  systems |
   |          |          |          |          |          |    that  |
   |          |          |          |          |          |    need  |
   |          |          |          |          |          |    to    |
   |          |          |          |          |          |    un    |
   |          |          |          |          |          | derstand |
   |          |          |          |          |          |    them. |
   +----------+----------+----------+----------+----------+----------+
   | SCT      | 2.16.84  | SNOMED   | SNOMED   | DOC:     | `biblio  |
   |          | 0.1.​113 | CT       | Inter    | `htt     | entry_ti |
   |          | 883.6.96 |          | national | p://​www | tle <#bi |
   |          |          |          |          | .snomed. | blio_SNO |
   |          |          |          |          | org/ <ht | MED>`__, |
   |          |          |          |          | tp://www | using    |
   |          |          |          |          | .snomed. | the CT   |
   |          |          |          |          | org/>`__ | code     |
   |          |          |          |          |          | values   |
   +----------+----------+----------+----------+----------+----------+
   | SRT      | 2.16.84  | SNOMED   | SNOMED   | DOC:     | `biblio  |
   |          | 0.1.​113 | CT       | Inter    | `htt     | entry_ti |
   |          | 883.6.96 |          | national | p://​www | tle <#bi |
   |          |          |          |          | .snomed. | blio_SNO |
   |          |          |          |          | org/ <ht | MED>`__, |
   |          |          |          |          | tp://www | using    |
   |          |          |          |          | .snomed. | the      |
   |          |          |          |          | org/>`__ | "S       |
   |          |          |          |          |          | NOMED-RT |
   |          |          |          |          |          | style"   |
   |          |          |          |          |          | code     |
   |          |          |          |          |          | values   |
   |          |          |          |          |          | (see     |
   |          |          |          |          |          | `SNOMED  |
   |          |          |          |          |          | CT       |
   |          |          |          |          |          |  <#sect_ |
   |          |          |          |          |          | 8.1>`__) |
   |          |          |          |          |          |          |
   |          |          |          |          |          | .        |
   |          |          |          |          |          | . note:: |
   |          |          |          |          |          |          |
   |          |          |          |          |          |          |
   |          |          |          |          |          |   1. HL7 |
   |          |          |          |          |          |          |
   |          |          |          |          |          |     uses |
   |          |          |          |          |          |          |
   |          |          |          |          |          |    "SNM" |
   |          |          |          |          |          |          |
   |          |          |          |          |          |      for |
   |          |          |          |          |          |          |
   |          |          |          |          |          |      the |
   |          |          |          |          |          |          |
   |          |          |          |          |          | symbolic |
   |          |          |          |          |          |          |
   |          |          |          |          |          |    name. |
   |          |          |          |          |          |          |
   |          |          |          |          |          |          |
   |          |          |          |          |          |  2. This |
   |          |          |          |          |          |          |
   |          |          |          |          |          |   coding |
   |          |          |          |          |          |          |
   |          |          |          |          |          |   scheme |
   |          |          |          |          |          |       is |
   |          |          |          |          |          |          |
   |          |          |          |          |          |      dep |
   |          |          |          |          |          | recated. |
   |          |          |          |          |          |          |
   |          |          |          |          |          |      The |
   |          |          |          |          |          |          |
   |          |          |          |          |          |      use |
   |          |          |          |          |          |       of |
   |          |          |          |          |          |       "S |
   |          |          |          |          |          | NOMED-RT |
   |          |          |          |          |          |          |
   |          |          |          |          |          |   style" |
   |          |          |          |          |          |          |
   |          |          |          |          |          |     code |
   |          |          |          |          |          |          |
   |          |          |          |          |          |   values |
   |          |          |          |          |          |       is |
   |          |          |          |          |          |       no |
   |          |          |          |          |          |          |
   |          |          |          |          |          |   longer |
   |          |          |          |          |          |       au |
   |          |          |          |          |          | thorized |
   |          |          |          |          |          |       by |
   |          |          |          |          |          |          |
   |          |          |          |          |          |   SNOMED |
   |          |          |          |          |          |          |
   |          |          |          |          |          |   except |
   |          |          |          |          |          |          |
   |          |          |          |          |          |      for |
   |          |          |          |          |          |          |
   |          |          |          |          |          | creation |
   |          |          |          |          |          |       by |
   |          |          |          |          |          |          |
   |          |          |          |          |          |   legacy |
   |          |          |          |          |          |          |
   |          |          |          |          |          | devices, |
   |          |          |          |          |          |          |
   |          |          |          |          |          |   legacy |
   |          |          |          |          |          |          |
   |          |          |          |          |          |  objects |
   |          |          |          |          |          |       in |
   |          |          |          |          |          |       a  |
   |          |          |          |          |          | rchives, |
   |          |          |          |          |          |          |
   |          |          |          |          |          |      and |
   |          |          |          |          |          |       r  |
   |          |          |          |          |          | eceiving |
   |          |          |          |          |          |          |
   |          |          |          |          |          |  systems |
   |          |          |          |          |          |          |
   |          |          |          |          |          |     that |
   |          |          |          |          |          |          |
   |          |          |          |          |          |     need |
   |          |          |          |          |          |       to |
   |          |          |          |          |          |       un |
   |          |          |          |          |          | derstand |
   |          |          |          |          |          |          |
   |          |          |          |          |          |    them. |
   +----------+----------+----------+----------+----------+----------+
   | UBERON   | 1.2.840  | UBERON   |          | DOC:     | The      |
   |          | .10008.​ |          |          | `htt     | Uberon   |
   |          | 2.​16.​6 |          |          | p://​ube | ID from  |
   |          |          |          |          | ron.org/ | the      |
   |          |          |          |          |  <http:/ | Uberon   |
   |          |          |          |          | /uberon. | in       |
   |          |          |          |          | org/>`__ | tegrated |
   |          |          |          |          |          | cross    |
   |          |          |          |          |          | -species |
   |          |          |          |          |          | ontology |
   |          |          |          |          |          | covering |
   |          |          |          |          |          | an       |
   |          |          |          |          |          | atomical |
   |          |          |          |          |          | st       |
   |          |          |          |          |          | ructures |
   |          |          |          |          |          | in       |
   |          |          |          |          |          | animals. |
   +----------+----------+----------+----------+----------+----------+
   | UCUM     | 2.16.8   | UCUM     | Reg      | DOC:     | `bib     |
   |          | 40.1.​11 |          | enstrief | `http:/  | lioentry |
   |          | 3883.6.8 |          | I        | /​unitso | _title < |
   |          |          |          | nstitute | fmeasure | #biblio_ |
   |          |          |          |          | .org/​uc | UCUM>`__ |
   |          |          |          |          | um.html  | Unified  |
   |          |          |          |          | <http:// | Code for |
   |          |          |          |          | unitsofm | Units of |
   |          |          |          |          | easure.o | Measure  |
   |          |          |          |          | rg/ucum. |          |
   |          |          |          |          | html>`__ |          |
   +----------+----------+----------+----------+----------+----------+
   | UMLS     | 2.16.84  | UMLS     | NLM      | DOC:     | UMLS     |
   |          | 0.1.​113 |          |          | `htt     | codes as |
   |          | 883.6.86 |          |          | p://​www | CUIs     |
   |          |          |          |          | .nlm.nih | making   |
   |          |          |          |          | .gov/​re | up the   |
   |          |          |          |          | search/​ | values   |
   |          |          |          |          | umls/ <h | in a     |
   |          |          |          |          | ttp://ww | coding   |
   |          |          |          |          | w.nlm.ni | system   |
   |          |          |          |          | h.gov/re |          |
   |          |          |          |          | search/u |          |
   |          |          |          |          | mls/>`__ |          |
   +----------+----------+----------+----------+----------+----------+
   | UPC      | 2.16.84  |          |          |          | U        |
   |          | 0.1.​113 |          |          |          | niversal |
   |          | 883.6.55 |          |          |          | Product  |
   |          |          |          |          |          | Code -   |
   |          |          |          |          |          | U        |
   |          |          |          |          |          | niversal |
   |          |          |          |          |          | Code     |
   |          |          |          |          |          | Council  |
   +----------+----------+----------+----------+----------+----------+

.. table:: HL7v3 Coding Schemes

   +----------------------+----------------------+----------------------+
   | Coding Scheme        | Coding Scheme UID    | Description          |
   | Designator           |                      |                      |
   +======================+======================+======================+
   | ActCode              | 2                    |                      |
   |                      | .16.840.1.113883.5.4 |                      |
   +----------------------+----------------------+----------------------+
   | ActPriority          | 2                    |                      |
   |                      | .16.840.1.113883.5.7 |                      |
   +----------------------+----------------------+----------------------+
   | AdministrativeGender | 2                    |                      |
   |                      | .16.840.1.113883.5.1 |                      |
   +----------------------+----------------------+----------------------+
   | mediaType            | 2.                   | `RFC2046             |
   |                      | 16.840.1.113883.5.79 | <http://www.ietf.org |
   |                      |                      | /rfc/rfc2046.txt>`__ |
   +----------------------+----------------------+----------------------+
   | NullFlavor           | 2.16                 |                      |
   |                      | .840.1.113883.5.1008 |                      |
   +----------------------+----------------------+----------------------+
   | Obser                | 2.                   |                      |
   | vationInterpretation | 16.840.1.113883.5.83 |                      |
   +----------------------+----------------------+----------------------+
   | Confidentiality      | 2.                   |                      |
   |                      | 16.840.1.113883.5.25 |                      |
   +----------------------+----------------------+----------------------+
   | ParticipationType    | 2.                   |                      |
   |                      | 16.840.1.113883.5.90 |                      |
   +----------------------+----------------------+----------------------+

.. _sect_8.1:

SNOMED CT
---------

SNOMED (the Systematized Nomenclature of Medicine) Clinical Terms (CT)
is the preferred coding system within DICOM for anatomy, clinical
findings, procedures, pharmaceutical/biologic products (including
contrast agents), and other clinical terms.

SNOMED has had various versions, including SNOMED International (Version
3), which was issued in 1993 and revised through 1998, SNOMED Reference
Terminology, the successor to SNOMED 3 that was published between 1999
and 2001, and SNOMED Clinical Terms, which has been the name since 2002.
The coding scheme is fully backward-compatible across SNOMED 3,
SNOMED-RT, and SNOMED CT. SNOMED CT introduced a solely numeric set of
codes (ConceptID) in addition to the former alphanumeric codes
(SnomedID), but all SNOMED terminology concepts have both a numeric and
an alphanumeric code.

In previous editions of the DICOM Standard, the following Coding Scheme
Designators were used for SNOMED codes in DICOM:

-  "99SDM", denoting the provisional SNOMED DICOM Microglossary

-  "SNM3", denoting SNOMED International (Version 3)

-  "SRT", originally denoting SNOMED-RT, but later used to identify
   SNOMED CT concepts using "SNOMED-RT style" alphanumeric code values

All uses of SNOMED CT coded terms in DICOM are now indicated by the
Coding Scheme Designator "SCT", identifying them as SNOMED CT numeric
Concept IDs as code values.

When a Coding Scheme Designator of "99SDM", "SNM3" or "SRT" is
encountered by a receiving system, the "SNOMED-RT style" alphanumeric
Code Value needs to be mapped to the corresponding concept designated by
the SNOMED CT Concept IDs assigned to the same concept.

.. note::

   "SRT" as a coding scheme designator was used only in the DICOM
   Standard. HL7v2 did not standardize a coding scheme designator for
   SNOMED-RT.

When interoperating with systems that use SNOMED CT codes, Application
Entities may receive and are expected to send Code Sequences with a
numeric ConceptID code. It is the responsibility of such Application
Entities to convert any alphanumeric SnomedID with Coding Scheme
Designator "SRT" used in old DICOM objects and services to the
corresponding numeric ConceptID code.

.. note::

   1. Some non-DICOM systems may use a Coding Scheme Designator of
      "SNOMED-CT" rather than "SCT" as is used in DICOM.

   2. The SNOMED organization's policy on the use of "antecedent
      versions", including the continued use of "SNOMED-RT style"
      alphanumeric code values is described at:
      `http://​www.snomed.org/​news-articles/​timetable-​for-​the-​withdrawal-​of-​legacy-​snomed-​codes <http://www.snomed.org/news-articles/timetable-for-the-withdrawal-of-legacy-snomed-codes>`__.

   3. Since the SNOMED organization no longer distributes a reference
      set that includes a mapping of "SNOMED-RT style" SNOMED IDs to
      SNOMED Concept IDs a complete mapping of those used in DICOM is
      provided in `SNOMED Concept ID to SNOMED ID
      Mapping <#chapter_O>`__ to allow implementers to process legacy
      objects from legacy devices and archives.

.. _sect_8.1.1:

Use of SNOMED Anatomic Concepts
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

In general, DICOM uses the anatomic concepts with the term "structure",
rather than with the term "entire". This is an important distinction in
SNOMED. "Entire" is a child concept to "structure", has a more
restricted meaning, and typically is used in conjunction with treatments
(e.g., "excision of *entire* right kidney"). It is used in distinction
to other sibling children of the parent concept that may identify parts
of the parent anatomic feature. Since imaging typically targets both the
anatomic feature and the area around it, or sometimes just part of the
anatomic feature, DICOM usually uses "structure" concepts that are more
inclusive than the "entire" concepts.

.. _sect_8.2:

ISO_OID
-------

`biblioentry_title <#biblio_ISO8824-1>`__ and
`biblioentry_title <#biblio_ISO9834-1>`__ are the standards defined for
the generation of object identifiers that are used as DICOM Unique
Identifiers (see ), can also serve as a general mechanism for
identifying organizations and objects defined by those organizations.

When the Coding Scheme Designator is ISO_OID, the Code Value shall be
the numeric (dot delimited) form of a valid object identifier.

A repository of known existing object identifiers can be found at
http://www.oid-info.com/index.htm. For example:

-  the ISO 9834-1 assigned numeric object identifier for the country
   France, is "1.0.3166.2.2.1.250" (since ISO 3166 defines a means for
   maintaining country codes using object identifiers)

-  the object identifier for the RIPEMD-160 cryptographic hash function
   is "1.0.10118.3.0.49"

-  the object identifier for the HL7 V2 table of codes for marital
   status is "2.16.840.1.113883.12.2"

The re-use of object identifiers for existing concepts that do not have
an alternative more appropriate coding scheme compatible with DICOM
provides a mechanism to avoid defining new codes. For example, HL7
assigned object identifiers can be found at
http://www.hl7.org/oid/index.cfm.

Though the intent of ISO_OID is to define organizational roots for the
hierarchical assignment of object identifiers, and not specifically to
identify organizations per se, the organizational root values can be
construed as identifying the organization. For example, the DICOM
Standards Organization itself can be identified by the value
"1.2.840.10008". See also `Organizations <#sect_CID_5002>`__.

.. _sect_8.3:

Retired Codes and Expected Behavior
-----------------------------------

As this Standard and external coding schemes are maintained, the codes
specified as Concept Names, Concept Values and in Conditions may change.
The previous codes are considered Retired but implementations may
continue to send them and receivers will be expected to be able to
continue to recognize the Retired codes, including the Code Value and
Coding Scheme Designator, even if the current Standard does not publish
them.

A notable example is the change throughout the Standard from using
"SNOMED-RT style" code values with a Coding Scheme Designator of "SRT",
"SNM3" or "99SDM", to the use of SNOMED CT numeric code values with a
Coding Scheme Designator of "SCT". A mapping of retired to new SNOMED
codes is found in `SNOMED Concept ID to SNOMED ID
Mapping <#chapter_O>`__.

