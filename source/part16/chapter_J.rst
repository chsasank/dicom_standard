.. _chapter_J:

SNOMED Retired Codes
====================

This Annex identifies coded terms specified in earlier versions of the
Standard. These coded terms are retired. Some of the codes conflict with
codes defined in SNOMED. Additionally, some SNOMED coded terms specified
in earlier versions of the Standard have been retired and replaced by
SNOMED to avoid ambiguities in concept, and are noted here as well.

Implementers of the Standard are cautioned that:

-  some of the codes noted as retired are still valid (active) SNOMED
   codes, but with different meanings; it is thus the combination of
   code and meaning that is retired

-  not all of the codes that SNOMED International may have inactivated
   in any past, current or future SNOMED CT release have yet been
   retired from DICOM

-  some applications may continue to send retired codes with the meaning
   defined in this Annex

-  the retired codes may be associated with coding scheme designator
   99SDM, SNM3 or SRT

-  retired codes may be encountered in existing SOP Instances stored in
   archives

-  applications receiving SOP Instances should continue to support
   retired codes with the meaning defined in this Annex

-  some applications may not trigger expected behavior (e.g., hanging
   protocols, image processing) when receiving SOP Instances with the
   replacement codes

-  DICOM applications and SOP Instances shall never use the retired
   codes with a meaning other than that defined in this Annex

-  in some cases, the choice of replacement code for a retired code
   depends on the context of its use, and so one retired code may map to
   more than one replacement code

.. table:: SNOMED Codes Retired from DICOM Use

   +----------------+----------------+----------------+----------------+
   | Retired Code   | Code Meaning   | Replacement    | Notes          |
   | Value          |                | Code           |                |
   +================+================+================+================+
   | G-5190         | Headfirst      | `1025          |                |
   |                |                | 40008 <http:// |                |
   |                |                | snomed.info/id |                |
   |                |                | /102540008>`__ |                |
   +----------------+----------------+----------------+----------------+
   | G-5191         | Feet-first     | `1025          |                |
   |                |                | 41007 <http:// |                |
   |                |                | snomed.info/id |                |
   |                |                | /102541007>`__ |                |
   +----------------+----------------+----------------+----------------+
   | G-A11A         | Mi             | `1033          |                |
   |                | d-longitudinal | 42007 <http:// |                |
   |                |                | snomed.info/id |                |
   |                |                | /103342007>`__ |                |
   +----------------+----------------+----------------+----------------+
   | G-A11B         | Parasagittal   | `1033          |                |
   |                |                | 43002 <http:// |                |
   |                |                | snomed.info/id |                |
   |                |                | /103343002>`__ |                |
   +----------------+----------------+----------------+----------------+
   | G-A12A         | Intraluminal   | `2640          |                |
   |                |                | 45001 <http:// |                |
   |                |                | snomed.info/id |                |
   |                |                | /264045001>`__ |                |
   +----------------+----------------+----------------+----------------+
   | G-A16A         | Capsule        | `11            | Replacement    |
   |                |                | 070000 <http:/ | code has       |
   |                |                | /snomed.info/i | meaning        |
   |                |                | d/11070000>`__ | "Capsular".    |
   |                |                |                |                |
   |                |                |                | (131184002,    |
   |                |                |                | SCT, "Area of  |
   |                |                |                | defined        |
   |                |                |                | region")       |
   |                |                |                | remains in     |
   |                |                |                | use.           |
   +----------------+----------------+----------------+----------------+
   | G-A16B         | Lumen          | `1133          |                |
   |                |                | 42003 <http:// |                |
   |                |                | snomed.info/id |                |
   |                |                | /113342003>`__ |                |
   +----------------+----------------+----------------+----------------+
   | G-A16C         | Contact        | `11            | Replacement    |
   |                |                | 723008 <http:/ | code has       |
   |                |                | /snomed.info/i | meaning        |
   |                |                | d/11723008>`__ | "Contact       |
   |                |                |                | with".         |
   |                |                |                |                |
   |                |                |                | Retired code   |
   |                |                |                | has meaning    |
   |                |                |                | "Part of       |
   |                |                |                | tooth", and is |
   |                |                |                | not used in    |
   |                |                |                | DICOM.         |
   +----------------+----------------+----------------+----------------+
   | G-A16D         | Parenchyma     | `91            |                |
   |                |                | 772007 <http:/ |                |
   |                |                | /snomed.info/i |                |
   |                |                | d/91772007>`__ |                |
   +----------------+----------------+----------------+----------------+
   | J-83250        | Metal (Lead)   | `2623          |                |
   |                | Marker         | 01009 <http:// |                |
   |                |                | snomed.info/id |                |
   |                |                | /262301009>`__ |                |
   +----------------+----------------+----------------+----------------+
   | R-102C9        | Transthoracic  | `2724          |                |
   |                |                | 76000 <http:// |                |
   |                |                | snomed.info/id |                |
   |                |                | /272476000>`__ |                |
   +----------------+----------------+----------------+----------------+
   | R-102CA        | Lordotic       | `2604          |                |
   |                |                | 50008 <http:// |                |
   |                |                | snomed.info/id |                |
   |                |                | /260450008>`__ |                |
   +----------------+----------------+----------------+----------------+
   | R-102CB        | Transforamenal | `2724          |                |
   |                |                | 66003 <http:// |                |
   |                |                | snomed.info/id |                |
   |                |                | /272466003>`__ |                |
   +----------------+----------------+----------------+----------------+
   | R-102CC        | Transoral      | `1184          |                |
   |                |                | 38002 <http:// |                |
   |                |                | snomed.info/id |                |
   |                |                | /118438002>`__ |                |
   +----------------+----------------+----------------+----------------+
   | R-102CE        | Transorbital   | `2783          |                |
   |                |                | 18001 <http:// |                |
   |                |                | snomed.info/id |                |
   |                |                | /278318001>`__ |                |
   +----------------+----------------+----------------+----------------+
   | R-11300        | Transverse     | `62            |                |
   |                |                | 824007 <http:/ |                |
   |                |                | /snomed.info/i |                |
   |                |                | d/62824007>`__ |                |
   +----------------+----------------+----------------+----------------+
   | Y-X1770        | Cranio-caudal  | `3991          |                |
   |                | exaggerated    | 92008 <http:// |                |
   |                | laterally      | snomed.info/id |                |
   |                |                | /399192008>`__ |                |
   +----------------+----------------+----------------+----------------+
   | Y-X1771        | Cranio-caudal  | `3991          |                |
   |                | exaggerated    | 01009 <http:// |                |
   |                | medially       | snomed.info/id |                |
   |                |                | /399101009>`__ |                |
   +----------------+----------------+----------------+----------------+
   | T-D1217        | Maxilla and    | `661005 <http  |                |
   |                | mandible       | ://snomed.info |                |
   |                |                | /id/661005>`__ |                |
   +----------------+----------------+----------------+----------------+
   | T-D1480        | Orbit          | `3636          |                |
   |                |                | 54007 <http:// |                |
   |                |                | snomed.info/id |                |
   |                |                | /363654007>`__ |                |
   +----------------+----------------+----------------+----------------+
   | T-D6151        | Uterus and     | `1106          |                |
   |                | fallopian      | 39002 <http:// |                |
   |                | tubes          | snomed.info/id |                |
   |                |                | /110639002>`__ |                |
   +----------------+----------------+----------------+----------------+
   | G-0371         | % Area         | `4087          |                |
   |                | Reduction      | 14007 <http:// |                |
   |                |                | snomed.info/id |                |
   |                |                | /408714007>`__ |                |
   +----------------+----------------+----------------+----------------+
   | G-0372         | % Diameter     | `4087          |                |
   |                | Reduction      | 15008 <http:// |                |
   |                |                | snomed.info/id |                |
   |                |                | /408715008>`__ |                |
   +----------------+----------------+----------------+----------------+
   | G-C295         | Route of       | `4106          |                |
   |                | Administration | 75002 <http:// |                |
   |                |                | snomed.info/id |                |
   |                |                | /410675002>`__ |                |
   +----------------+----------------+----------------+----------------+
   | G-D100         | Route of       | `4106          |                |
   |                | Administration | 75002 <http:// |                |
   |                |                | snomed.info/id |                |
   |                |                | /410675002>`__ |                |
   +----------------+----------------+----------------+----------------+
   | T-42501        | Abdominal      | `              |                |
   |                | Aorta          | 7832008 <http: |                |
   |                |                | //snomed.info/ |                |
   |                |                | id/7832008>`__ |                |
   +----------------+----------------+----------------+----------------+
   | T-42303        | Aortic Arch    | `57            |                |
   |                |                | 034009 <http:/ |                |
   |                |                | /snomed.info/i |                |
   |                |                | d/57034009>`__ |                |
   +----------------+----------------+----------------+----------------+
   | T-45011        | Carotid Artery | `69            |                |
   |                |                | 105007 <http:/ |                |
   |                |                | /snomed.info/i |                |
   |                |                | d/69105007>`__ |                |
   +----------------+----------------+----------------+----------------+
   | T-A600A        | Cerebellum     | `1133          |                |
   |                |                | 05005 <http:// |                |
   |                |                | snomed.info/id |                |
   |                |                | /113305005>`__ |                |
   +----------------+----------------+----------------+----------------+
   | T-D00CC        | Entire Spine   | T-D0146        |                |
   +----------------+----------------+----------------+----------------+
   | T-48500        | Pulmonary Vein | `1229          |                |
   |                |                | 72007 <http:// |                |
   |                |                | snomed.info/id |                |
   |                |                | /122972007>`__ |                |
   +----------------+----------------+----------------+----------------+
   | T-D8300        | Elbow          | `16            |                |
   |                |                | 953009 <http:/ |                |
   |                |                | /snomed.info/i |                |
   |                |                | d/16953009>`__ |                |
   +----------------+----------------+----------------+----------------+
   | T-12402        | Forearm        | `14            |                |
   |                |                | 975008 <http:/ |                |
   |                |                | /snomed.info/i |                |
   |                |                | d/14975008>`__ |                |
   +----------------+----------------+----------------+----------------+
   | T-D2500        | Hip            | `24            |                |
   |                |                | 136001 <http:/ |                |
   |                |                | /snomed.info/i |                |
   |                |                | d/24136001>`__ |                |
   +----------------+----------------+----------------+----------------+
   | T-D4909        | Kidney         | `64            |                |
   |                |                | 033007 <http:/ |                |
   |                |                | /snomed.info/i |                |
   |                |                | d/64033007>`__ |                |
   +----------------+----------------+----------------+----------------+
   | T-62002        | Liver          | `10            |                |
   |                |                | 200004 <http:/ |                |
   |                |                | /snomed.info/i |                |
   |                |                | d/10200004>`__ |                |
   +----------------+----------------+----------------+----------------+
   | T-D4034        | Pancreas       | `15            |                |
   |                |                | 776009 <http:/ |                |
   |                |                | /snomed.info/i |                |
   |                |                | d/15776009>`__ |                |
   +----------------+----------------+----------------+----------------+
   | T-55002        | Pharynx        | `54            |                |
   |                |                | 066008 <http:/ |                |
   |                |                | /snomed.info/i |                |
   |                |                | d/54066008>`__ |                |
   +----------------+----------------+----------------+----------------+
   | T-11500        | Spine          | `4210          | Was previously |
   |                |                | 60004 <http:// | replaced with  |
   |                |                | snomed.info/id | T-D0146, which |
   |                |                | /421060004>`__ | is no longer   |
   |                |                |                | an active      |
   |                |                |                | SNOMED CT      |
   |                |                |                | concept.       |
   |                |                |                |                |
   |                |                |                | Replacement    |
   |                |                |                | code has       |
   |                |                |                | meaning of     |
   |                |                |                | "Structure of  |
   |                |                |                | vertebral      |
   |                |                |                | column (body   |
   |                |                |                | structure)".   |
   +----------------+----------------+----------------+----------------+
   | T-D0146        | Spine          | `4210          | Replacement    |
   |                |                | 60004 <http:// | code has       |
   |                |                | snomed.info/id | meaning of     |
   |                |                | /421060004>`__ | "Structure of  |
   |                |                |                | vertebral      |
   |                |                |                | column (body   |
   |                |                |                | structure)".   |
   |                |                |                |                |
   |                |                |                | Retired code   |
   |                |                |                | is inactive in |
   |                |                |                | SNOMED CT      |
   |                |                |                | (Ambiguous).   |
   +----------------+----------------+----------------+----------------+
   | T-D4035        | Spleen         | `78            |                |
   |                |                | 961009 <http:/ |                |
   |                |                | /snomed.info/i |                |
   |                |                | d/78961009>`__ |                |
   +----------------+----------------+----------------+----------------+
   | T-9400F        | Testis         | `40            |                |
   |                |                | 689003 <http:/ |                |
   |                |                | /snomed.info/i |                |
   |                |                | d/40689003>`__ |                |
   +----------------+----------------+----------------+----------------+
   | T-4600A        | Thoracic aorta | `1132          |                |
   |                |                | 62008 <http:// |                |
   |                |                | snomed.info/id |                |
   |                |                | /113262008>`__ |                |
   +----------------+----------------+----------------+----------------+
   | T-C8001        | Thymus         | `              |                |
   |                |                | 9875009 <http: |                |
   |                |                | //snomed.info/ |                |
   |                |                | id/9875009>`__ |                |
   +----------------+----------------+----------------+----------------+
   | T-D6151        | Uterus and     | `1106          |                |
   |                | fallopian      | 39002 <http:// |                |
   |                | tubes          | snomed.info/id |                |
   |                |                | /110639002>`__ |                |
   +----------------+----------------+----------------+----------------+
   | T-73800        | Ureter         | `87            |                |
   |                |                | 953007 <http:/ |                |
   |                |                | /snomed.info/i |                |
   |                |                | d/87953007>`__ |                |
   +----------------+----------------+----------------+----------------+
   | T-83009        | Uterus         | `35            |                |
   |                |                | 039007 <http:/ |                |
   |                |                | /snomed.info/i |                |
   |                |                | d/35039007>`__ |                |
   +----------------+----------------+----------------+----------------+
   | T-D8600        | Wrist          | `74            |                |
   |                |                | 670003 <http:/ |                |
   |                |                | /snomed.info/i |                |
   |                |                | d/74670003>`__ |                |
   +----------------+----------------+----------------+----------------+
   | T-11167        | Zygoma         | `13            |                |
   |                |                | 881006 <http:/ |                |
   |                |                | /snomed.info/i |                |
   |                |                | d/13881006>`__ |                |
   +----------------+----------------+----------------+----------------+
   | P5-B3003       | Transthoracic  | `4332          | Retired code   |
   |                | ec             | 36007 <http:// | is inactive in |
   |                | hocardiography | snomed.info/id | SNOMED CT      |
   |                |                | /433236007>`__ | (Limited).     |
   +----------------+----------------+----------------+----------------+
   | P5-B3004       | Epicardial     | `4332          | Retired code   |
   |                | ec             | 32009 <http:// | is inactive in |
   |                | hocardiography | snomed.info/id | SNOMED CT      |
   |                |                | /433232009>`__ | (Retired       |
   |                |                |                | without stated |
   |                |                |                | reason).       |
   +----------------+----------------+----------------+----------------+
   | P5-B3082       | Pediatric      | `4318          |                |
   |                | ec             | 52008 <http:// |                |
   |                | hocardiography | snomed.info/id |                |
   |                |                | /431852008>`__ |                |
   +----------------+----------------+----------------+----------------+
   | P5-B3083       | Intraoperative | `4298          |                |
   |                | ec             | 84006 <http:// |                |
   |                | hocardiography | snomed.info/id |                |
   |                |                | /429884006>`__ |                |
   +----------------+----------------+----------------+----------------+
   | P5-01000       | Image          |                |                |
   |                | acquisition    |                |                |
   |                | procedure      |                |                |
   +----------------+----------------+----------------+----------------+
   | P5-01101       | Image          |                |                |
   |                | acquisition    |                |                |
   |                | after          |                |                |
   |                | administration |                |                |
   |                | of contrast    |                |                |
   |                | agent          |                |                |
   +----------------+----------------+----------------+----------------+
   | P5-01103       | Image          | `18            |                |
   |                | acquisition    | 590009 <http:/ |                |
   |                | during cardiac | /snomed.info/i |                |
   |                | pacing         | d/18590009>`__ |                |
   +----------------+----------------+----------------+----------------+
   | P5-01104       | Image          | `18            |                |
   |                | acquisition at | 590009 <http:/ |                |
   |                | user-defined   | /snomed.info/i |                |
   |                | cardiac pacing | d/18590009>`__ |                |
   |                | rate           |                |                |
   +----------------+----------------+----------------+----------------+
   | P5-01111       | Image          | `1289          |                |
   |                | acquisition    | 65002 <http:// |                |
   |                | during hand    | snomed.info/id |                |
   |                | grip maneuver  | /128965002>`__ |                |
   +----------------+----------------+----------------+----------------+
   | P5-01112       | Image          | `2610          |                |
   |                | acquisition    | 39008 <http:// |                |
   |                | during         | snomed.info/id |                |
   |                | Valsalva       | /261039008>`__ |                |
   +----------------+----------------+----------------+----------------+
   | P5-01113       | Image          |                |                |
   |                | acquisition    |                |                |
   |                | during         |                |                |
   |                | postural       |                |                |
   |                | maneuver       |                |                |
   +----------------+----------------+----------------+----------------+
   | P5-01120       | Pre-procedure  | `3071          |                |
   |                | image          | 53007 <http:// |                |
   |                | acquisition    | snomed.info/id |                |
   |                |                | /307153007>`__ |                |
   +----------------+----------------+----------------+----------------+
   | P5-01121       | Preoperative   | `3071          |                |
   |                | image          | 53007 <http:// |                |
   |                | acquisition    | snomed.info/id |                |
   |                |                | /307153007>`__ |                |
   +----------------+----------------+----------------+----------------+
   | P5-01130       | I              | `3071          |                |
   |                | ntra-procedure | 54001 <http:// |                |
   |                | image          | snomed.info/id |                |
   |                | acquisition    | /307154001>`__ |                |
   +----------------+----------------+----------------+----------------+
   | P5-01131       | I              | `3071          |                |
   |                | ntra-operative | 54001 <http:// |                |
   |                | image          | snomed.info/id |                |
   |                | acquisition    | /307154001>`__ |                |
   +----------------+----------------+----------------+----------------+
   | P5-01140       | Post-procedure | `3031          |                |
   |                | image          | 10006 <http:// |                |
   |                | acquisition    | snomed.info/id |                |
   |                |                | /303110006>`__ |                |
   +----------------+----------------+----------------+----------------+
   | P5-01141       | Post-operative | `3031          |                |
   |                | image          | 10006 <http:// |                |
   |                | acquisition    | snomed.info/id |                |
   |                |                | /303110006>`__ |                |
   +----------------+----------------+----------------+----------------+
   | P5-01142       | Image          | `3031          |                |
   |                | acquisition    | 10006 <http:// |                |
   |                | following      | snomed.info/id |                |
   |                | first          | /303110006>`__ |                |
   |                | c              |                |                |
   |                | ardiopulmonary |                |                |
   |                | bypass         |                |                |
   +----------------+----------------+----------------+----------------+
   | P5-01143       | Image          | `3031          |                |
   |                | acquisition    | 10006 <http:// |                |
   |                | following      | snomed.info/id |                |
   |                | second         | /303110006>`__ |                |
   |                | c              |                |                |
   |                | ardiopulmonary |                |                |
   |                | bypass         |                |                |
   +----------------+----------------+----------------+----------------+
   | P5-01144       | Image          | `3031          |                |
   |                | acquisition    | 10006 <http:// |                |
   |                | following      | snomed.info/id |                |
   |                | third          | /303110006>`__ |                |
   |                | c              |                |                |
   |                | ardiopulmonary |                |                |
   |                | bypass         |                |                |
   +----------------+----------------+----------------+----------------+
   | P5-01200       | Image          | `3071          |                |
   |                | acquisition    | 54001 <http:// |                |
   |                | during stress  | snomed.info/id |                |
   |                | procedure      | /307154001>`__ |                |
   +----------------+----------------+----------------+----------------+
   | P5-01201       | Image          | `1289          |                |
   |                | acquisition at | 74000 <http:// |                |
   |                | baseline       | snomed.info/id |                |
   |                |                | /128974000>`__ |                |
   +----------------+----------------+----------------+----------------+
   | P5-01202       | Pre-stress     | `1289          |                |
   |                | image          | 74000 <http:// |                |
   |                | acquisition    | snomed.info/id |                |
   |                |                | /128974000>`__ |                |
   +----------------+----------------+----------------+----------------+
   | P5-01203       | Mid-stress     | `4326          |                |
   |                | image          | 55005 <http:// |                |
   |                | acquisition    | snomed.info/id |                |
   |                |                | /432655005>`__ |                |
   +----------------+----------------+----------------+----------------+
   | P5-01204       | Peak-stress    | `4341          |                |
   |                | image          | 61005 <http:// |                |
   |                | acquisition    | snomed.info/id |                |
   |                |                | /434161005>`__ |                |
   +----------------+----------------+----------------+----------------+
   | P5-01205       | Image          | `4325          |                |
   |                | acquisition    | 54001 <http:// |                |
   |                | during         | snomed.info/id |                |
   |                | recovery       | /432554001>`__ |                |
   +----------------+----------------+----------------+----------------+
   | P5-01300       | Image          | `4326          |                |
   |                | acquisition    | 55005 <http:// |                |
   |                | after drug     | snomed.info/id |                |
   |                | administration | /432655005>`__ |                |
   +----------------+----------------+----------------+----------------+
   | P5-01310       | Image          | `4326          |                |
   |                | acquisition at | 55005 <http:// |                |
   |                | user-defined   | snomed.info/id |                |
   |                | dobutamine     | /432655005>`__ |                |
   |                | dose           |                |                |
   +----------------+----------------+----------------+----------------+
   | P5-01311       | Image          | `4326          |                |
   |                | acquisition at | 55005 <http:// |                |
   |                | low-dose       | snomed.info/id |                |
   |                | dobutamine     | /432655005>`__ |                |
   +----------------+----------------+----------------+----------------+
   | P5-01312       | Image          | `4326          |                |
   |                | acquisition at | 55005 <http:// |                |
   |                | mid-dose       | snomed.info/id |                |
   |                | dobutamine     | /432655005>`__ |                |
   +----------------+----------------+----------------+----------------+
   | P5-01313       | Image          | `4326          |                |
   |                | acquisition at | 55005 <http:// |                |
   |                | peak dose      | snomed.info/id |                |
   |                | dobutamine     | /432655005>`__ |                |
   +----------------+----------------+----------------+----------------+
   | P5-01314       | Image          | `4326          |                |
   |                | acquisition at | 55005 <http:// |                |
   |                | dobutamine 5   | snomed.info/id |                |
   |                | mcg/kg/min     | /432655005>`__ |                |
   +----------------+----------------+----------------+----------------+
   | P5-01315       | Image          | `4326          |                |
   |                | acquisition at | 55005 <http:// |                |
   |                | dobutamine 10  | snomed.info/id |                |
   |                | mcg/kg/min     | /432655005>`__ |                |
   +----------------+----------------+----------------+----------------+
   | P5-01316       | Image          | `4326          |                |
   |                | acquisition at | 55005 <http:// |                |
   |                | dobutamine 20  | snomed.info/id |                |
   |                | mcg/kg/min     | /432655005>`__ |                |
   +----------------+----------------+----------------+----------------+
   | P5-01317       | Image          | `4326          |                |
   |                | acquisition at | 55005 <http:// |                |
   |                | dobutamine 30  | snomed.info/id |                |
   |                | mcg/kg/min     | /432655005>`__ |                |
   +----------------+----------------+----------------+----------------+
   | P5-01318       | Image          | `4326          |                |
   |                | acquisition at | 55005 <http:// |                |
   |                | dobutamine 40  | snomed.info/id |                |
   |                | mcg/kg/min     | /432655005>`__ |                |
   +----------------+----------------+----------------+----------------+
   | P5-01319       | Image          | `4326          |                |
   |                | acquisition at | 55005 <http:// |                |
   |                | dobutamine 50  | snomed.info/id |                |
   |                | mcg/kg/min     | /432655005>`__ |                |
   +----------------+----------------+----------------+----------------+
   | P5-0131A       | Image at       | `4326          |                |
   |                | dobutamine 40  | 55005 <http:// |                |
   |                | mcg/kg/min     | snomed.info/id |                |
   |                | plus atropine  | /432655005>`__ |                |
   +----------------+----------------+----------------+----------------+
   | P5-0131B       | Image          | `4326          |                |
   |                | acquisition at | 55005 <http:// |                |
   |                | dobutamine 50  | snomed.info/id |                |
   |                | mcg/kg/min     | /432655005>`__ |                |
   |                | plus atropine  |                |                |
   +----------------+----------------+----------------+----------------+
   | P5-01323       | Image          | `4341          |                |
   |                | acquisition at | 61005 <http:// |                |
   |                | peak           | snomed.info/id |                |
   |                | Arbutamine     | /434161005>`__ |                |
   |                | dose           |                |                |
   +----------------+----------------+----------------+----------------+
   | P5-01333       | Image          | `4341          |                |
   |                | acquisition at | 61005 <http:// |                |
   |                | peak           | snomed.info/id |                |
   |                | dipyridamole   | /434161005>`__ |                |
   +----------------+----------------+----------------+----------------+
   | P5-01341       | Image          | `4326          |                |
   |                | acquisition    | 55005 <http:// |                |
   |                | after          | snomed.info/id |                |
   |                | nitroglycerin  | /432655005>`__ |                |
   +----------------+----------------+----------------+----------------+
   | P5-01342       | Image          | `4326          |                |
   |                | acquisition    | 55005 <http:// |                |
   |                | after amyl     | snomed.info/id |                |
   |                | nitrite        | /432655005>`__ |                |
   +----------------+----------------+----------------+----------------+
   | P5-01343       | Image          | `4326          |                |
   |                | acquisition    | 55005 <http:// |                |
   |                | after          | snomed.info/id |                |
   |                | adenosine      | /432655005>`__ |                |
   +----------------+----------------+----------------+----------------+
   | P5-B301F       | Limited M-mode | `40            |                |
   |                | only           | 701008 <http:/ |                |
   |                | ec             | /snomed.info/i |                |
   |                | hocardiography | d/40701008>`__ |                |
   +----------------+----------------+----------------+----------------+
   | P5-B303F       | Limited        | `40            |                |
   |                | Doppler only   | 701008 <http:/ |                |
   |                | ec             | /snomed.info/i |                |
   |                | hocardiography | d/40701008>`__ |                |
   +----------------+----------------+----------------+----------------+
   | P5-B3051       | Maximal stress | `4332          |                |
   |                | ec             | 33004 <http:// |                |
   |                | hocardiography | snomed.info/id |                |
   |                |                | /433233004>`__ |                |
   +----------------+----------------+----------------+----------------+
   | P5-B3052       | Submaximal     | `4332          |                |
   |                | stress         | 33004 <http:// |                |
   |                | ec             | snomed.info/id |                |
   |                | hocardiography | /433233004>`__ |                |
   +----------------+----------------+----------------+----------------+
   | P5-B3053       | Treadmill      | `4332          |                |
   |                | exercise       | 33004 <http:// |                |
   |                | stress         | snomed.info/id |                |
   |                | ec             | /433233004>`__ |                |
   |                | hocardiography |                |                |
   +----------------+----------------+----------------+----------------+
   | P5-B3054       | Bruce          | `1290          |                |
   |                | treadmill      | 95002 <http:// |                |
   |                | stress         | snomed.info/id |                |
   |                | ec             | /129095002>`__ |                |
   |                | hocardiography |                |                |
   +----------------+----------------+----------------+----------------+
   | P5-B3055       | Modified Bruce | `1290          |                |
   |                | treadmill      | 96001 <http:// |                |
   |                | stress         | snomed.info/id |                |
   |                | ec             | /129096001>`__ |                |
   |                | hocardiography |                |                |
   +----------------+----------------+----------------+----------------+
   | P5-B3056       | Naughton       | `1291          |                |
   |                | treadmill      | 01001 <http:// |                |
   |                | stress         | snomed.info/id |                |
   |                | ec             | /129101001>`__ |                |
   |                | hocardiography |                |                |
   +----------------+----------------+----------------+----------------+
   | P5-B3058       | Bicycle        | `26            |                |
   |                | exercise       | 046004 <http:/ |                |
   |                | stress         | /snomed.info/i |                |
   |                | ec             | d/26046004>`__ |                |
   |                | hocardiography |                |                |
   +----------------+----------------+----------------+----------------+
   | P5-B3060       | Ec             | `4240          |                |
   |                | hocardiography | 64009 <http:// |                |
   |                | with           | snomed.info/id |                |
   |                | administered   | /424064009>`__ |                |
   |                | drug stress    |                |                |
   +----------------+----------------+----------------+----------------+
   | P5-B3061       | Dobutamine     | `4242          |                |
   |                | stress         | 25000 <http:// |                |
   |                | ec             | snomed.info/id |                |
   |                | hocardiography | /424225000>`__ |                |
   +----------------+----------------+----------------+----------------+
   | P5-B3062       | High dose      | `4242          |                |
   |                | dobutamine     | 25000 <http:// |                |
   |                | stress         | snomed.info/id |                |
   |                | ec             | /424225000>`__ |                |
   |                | hocardiography |                |                |
   +----------------+----------------+----------------+----------------+
   | P5-B3063       | Low dose       | `4242          |                |
   |                | dobutamine     | 25000 <http:// |                |
   |                | stress         | snomed.info/id |                |
   |                | ec             | /424225000>`__ |                |
   |                | hocardiography |                |                |
   +----------------+----------------+----------------+----------------+
   | P5-B3065       | Arbutamine     | `4240          |                |
   |                | stress         | 64009 <http:// |                |
   |                | ec             | snomed.info/id |                |
   |                | hocardiography | /424064009>`__ |                |
   +----------------+----------------+----------------+----------------+
   | P5-B3066       | Dipyridamole   | `4226          |                |
   |                | stress         | 85009 <http:// |                |
   |                | ec             | snomed.info/id |                |
   |                | hocardiography | /422685009>`__ |                |
   +----------------+----------------+----------------+----------------+
   | P5-B3070       | Cardiac pacing | `4286          |                |
   |                | ec             | 85003 <http:// |                |
   |                | hocardiography | snomed.info/id |                |
   |                |                | /428685003>`__ |                |
   +----------------+----------------+----------------+----------------+
   | P5-B3081       | Adult          | `40            | Replacement    |
   |                | ec             | 701008 <http:/ | code has       |
   |                | hocardiography | /snomed.info/i | meaning        |
   |                |                | d/40701008>`__ | "Ech           |
   |                |                |                | ocardiography" |
   +----------------+----------------+----------------+----------------+
   | P5-B3081       | Adult          | `2524          | Replacement    |
   |                | ec             | 18006 <http:// | code has       |
   |                | hocardiography | snomed.info/id | meaning        |
   |                |                | /252418006>`__ | "Transthoracic |
   |                |                |                | ech            |
   |                |                |                | ocardiography" |
   +----------------+----------------+----------------+----------------+
   | P5-B3084       | Upright        | `2524          |                |
   |                | ec             | 18006 <http:// |                |
   |                | hocardiography | snomed.info/id |                |
   |                |                | /252418006>`__ |                |
   +----------------+----------------+----------------+----------------+
   | P5-B3085       | Supine         | `2524          |                |
   |                | ec             | 18006 <http:// |                |
   |                | hocardiography | snomed.info/id |                |
   |                |                | /252418006>`__ |                |
   +----------------+----------------+----------------+----------------+
   | P5-B3091       | Contrast left  | `4332          |                |
   |                | ventricular    | 31002 <http:// |                |
   |                | opacification  | snomed.info/id |                |
   |                | ec             | /433231002>`__ |                |
   |                | hocardiography |                |                |
   +----------------+----------------+----------------+----------------+
   | P5-B3092       | Contrast       | `4332          |                |
   |                | perfusion      | 31002 <http:// |                |
   |                | ec             | snomed.info/id |                |
   |                | hocardiography | /433231002>`__ |                |
   +----------------+----------------+----------------+----------------+
   | P5-B3093       | Contrast       | `4332          |                |
   |                | Doppler        | 31002 <http:// |                |
   |                | enhancement    | snomed.info/id |                |
   |                | ec             | /433231002>`__ |                |
   |                | hocardiography |                |                |
   +----------------+----------------+----------------+----------------+
   | P5-B3191       | 2D complete    | `2524          |                |
   |                | ec             | 18006 <http:// |                |
   |                | hocardiography | snomed.info/id |                |
   |                |                | /252418006>`__ |                |
   +----------------+----------------+----------------+----------------+
   | P5-B3192       | Limited 2D     | `2524          |                |
   |                | only           | 18006 <http:// |                |
   |                | ec             | snomed.info/id |                |
   |                | hocardiography | /252418006>`__ |                |
   +----------------+----------------+----------------+----------------+
   | F-F7102        | Valsalva       | `2610          |                |
   |                | maneuver       | 39008 <http:// |                |
   |                |                | snomed.info/id |                |
   |                |                | /261039008>`__ |                |
   +----------------+----------------+----------------+----------------+
   | L-8061A        | Sterling pig   | `1322          |                |
   |                | breed          | 00002 <http:// |                |
   |                |                | snomed.info/id |                |
   |                |                | /132200002>`__ |                |
   +----------------+----------------+----------------+----------------+
   | L-8061F        | Black          | `1332          |                |
   |                | Slavonian pig  | 04003 <http:// |                |
   |                | breed          | snomed.info/id |                |
   |                |                | /133204003>`__ |                |
   +----------------+----------------+----------------+----------------+
   | L-807E1        | Bizanian Hound | `1323          |                |
   |                | dog breed      | 72009 <http:// |                |
   |                |                | snomed.info/id |                |
   |                |                | /132372009>`__ |                |
   +----------------+----------------+----------------+----------------+
   | L-80B03        | Rideau Arcott  | `1327          |                |
   |                | sheep breed    | 03001 <http:// |                |
   |                |                | snomed.info/id |                |
   |                |                | /132703001>`__ |                |
   +----------------+----------------+----------------+----------------+
   | L-8BC43        | Beefalo bison  | `4251          |                |
   |                | X cattle breed | 81009 <http:// |                |
   |                |                | snomed.info/id |                |
   |                |                | /425181009>`__ |                |
   +----------------+----------------+----------------+----------------+
   | L-8BC44        | Beefalo bison  | `4247          |                |
   |                | X cattle breed | 05003 <http:// |                |
   |                |                | snomed.info/id |                |
   |                |                | /424705003>`__ |                |
   +----------------+----------------+----------------+----------------+
   | R-4041B        | Hypokinesis    | `37            |                |
   |                |                | 706002 <http:/ |                |
   |                |                | /snomed.info/i |                |
   |                |                | d/37706002>`__ |                |
   +----------------+----------------+----------------+----------------+
   | F-32056        | Mild           | `3718          |                |
   |                | hypokinesis    | 68005 <http:// |                |
   |                |                | snomed.info/id |                |
   |                |                | /371868005>`__ |                |
   +----------------+----------------+----------------+----------------+
   | P5-B3009       | Exercise       | `4332          |                |
   |                | stress         | 33004 <http:// |                |
   |                | ec             | snomed.info/id |                |
   |                | hocardiography | /433233004>`__ |                |
   +----------------+----------------+----------------+----------------+
   | R-10218        | right anterior | `3993          |                |
   |                | oblique        | 56000 <http:// |                |
   |                |                | snomed.info/id |                |
   |                |                | /399356000>`__ |                |
   +----------------+----------------+----------------+----------------+
   | R-10222        | sagittal       | `30            |                |
   |                |                | 730003 <http:/ |                |
   |                |                | /snomed.info/i |                |
   |                |                | d/30730003>`__ |                |
   +----------------+----------------+----------------+----------------+
   | T-51005        | Anterior 1     | `6994          | Central        |
   |                |                | 53001 <http:// | incisor region |
   |                |                | snomed.info/id |                |
   |                |                | /699453001>`__ |                |
   +----------------+----------------+----------------+----------------+
   | T-51006        | Anterior 2     | `6995          | Lateral        |
   |                |                | 11000 <http:// | incisor region |
   |                |                | snomed.info/id |                |
   |                |                | /699511000>`__ |                |
   +----------------+----------------+----------------+----------------+
   | T-51007        | Anterior 3     | `6995          | Canine region  |
   |                |                | 10004 <http:// |                |
   |                |                | snomed.info/id |                |
   |                |                | /699510004>`__ |                |
   +----------------+----------------+----------------+----------------+
   | T-51008        | Premolar 1     | `6995          | First premolar |
   |                |                | 09009 <http:// | region         |
   |                |                | snomed.info/id |                |
   |                |                | /699509009>`__ |                |
   +----------------+----------------+----------------+----------------+
   | T-51009        | Premolar 2     | `6995          | Second         |
   |                |                | 08001 <http:// | premolar       |
   |                |                | snomed.info/id | region         |
   |                |                | /699508001>`__ |                |
   +----------------+----------------+----------------+----------------+
   | T-5100A        | Molar 1        | `6995          | First molar    |
   |                |                | 07006 <http:// | region         |
   |                |                | snomed.info/id |                |
   |                |                | /699507006>`__ |                |
   +----------------+----------------+----------------+----------------+
   | T-5100B        | Molar 2        | `6995          | Second molar   |
   |                |                | 05003 <http:// | region         |
   |                |                | snomed.info/id |                |
   |                |                | /699505003>`__ |                |
   +----------------+----------------+----------------+----------------+
   | T-5100C        | Molar 3        | `6995          | Third molar    |
   |                |                | 03005 <http:// | region         |
   |                |                | snomed.info/id |                |
   |                |                | /699503005>`__ |                |
   +----------------+----------------+----------------+----------------+
   | T-5100D        | Occlusal       | `2604          | Occlusal       |
   |                |                | 99007 <http:// | Projection     |
   |                |                | snomed.info/id |                |
   |                |                | /260499007>`__ |                |
   +----------------+----------------+----------------+----------------+
   | L-85B00        | Homo sapiens   | `3379          | Replacement    |
   |                |                | 15000 <http:// | code has       |
   |                |                | snomed.info/id | meaning of     |
   |                |                | /337915000>`__ | "Homo sapiens  |
   |                |                |                | (organism)".   |
   |                |                |                |                |
   |                |                |                | Retired code   |
   |                |                |                | is inactive in |
   |                |                |                | SNOMED CT      |
   |                |                |                | (Ambiguous).   |
   +----------------+----------------+----------------+----------------+
   | L-80100        | Bovine species | `3881          | Replacement    |
   |                |                | 68008 <http:// | code has       |
   |                |                | snomed.info/id | meaning of     |
   |                |                | /388168008>`__ | "Genus Bos     |
   |                |                |                | (organism)".   |
   |                |                |                |                |
   |                |                |                | Retired code   |
   |                |                |                | is inactive in |
   |                |                |                | SNOMED CT      |
   |                |                |                | (Ambiguous).   |
   +----------------+----------------+----------------+----------------+
   | L-80200        | Caprine        | `3882          | Replacement    |
   |                | species        | 49000 <http:// | code has       |
   |                |                | snomed.info/id | meaning of     |
   |                |                | /388249000>`__ | "Genus Capra   |
   |                |                |                | (organism)".   |
   |                |                |                |                |
   |                |                |                | Retired code   |
   |                |                |                | is inactive in |
   |                |                |                | SNOMED CT      |
   |                |                |                | (Ambiguous).   |
   +----------------+----------------+----------------+----------------+
   | L-80300        | Ovine species  | `3882          | Replacement    |
   |                |                | 54009 <http:// | code has       |
   |                |                | snomed.info/id | meaning of     |
   |                |                | /388254009>`__ | "Genus Ovis    |
   |                |                |                | (organism)".   |
   |                |                |                |                |
   |                |                |                | Retired code   |
   |                |                |                | is inactive in |
   |                |                |                | SNOMED CT      |
   |                |                |                | (Ambiguous).   |
   +----------------+----------------+----------------+----------------+
   | L-80400        | Equine species | `3884          | Replacement    |
   |                |                | 45009 <http:// | code has       |
   |                |                | snomed.info/id | meaning of     |
   |                |                | /388445009>`__ | "Genus Equus   |
   |                |                |                | (organism)".   |
   |                |                |                |                |
   |                |                |                | Retired code   |
   |                |                |                | is inactive in |
   |                |                |                | SNOMED CT      |
   |                |                |                | (Ambiguous).   |
   +----------------+----------------+----------------+----------------+
   | L-80500        | Porcine        | `3883          | Replacement    |
   |                | species        | 93002 <http:// | code has       |
   |                |                | snomed.info/id | meaning of     |
   |                |                | /388393002>`__ | "Genus Sus     |
   |                |                |                | (organism)".   |
   |                |                |                |                |
   |                |                |                | Retired code   |
   |                |                |                | is inactive in |
   |                |                |                | SNOMED CT      |
   |                |                |                | (Ambiguous).   |
   +----------------+----------------+----------------+----------------+
   | L-80700        | Canine species | `3884          | Replacement    |
   |                |                | 90000 <http:// | code has       |
   |                |                | snomed.info/id | meaning of     |
   |                |                | /388490000>`__ | "Genus Canis   |
   |                |                |                | (organism)".   |
   |                |                |                |                |
   |                |                |                | Retired code   |
   |                |                |                | is inactive in |
   |                |                |                | SNOMED CT      |
   |                |                |                | (Ambiguous).   |
   +----------------+----------------+----------------+----------------+
   | L-80A00        | Feline species | `3886          | Replacement    |
   |                |                | 26009 <http:// | code has       |
   |                |                | snomed.info/id | meaning of     |
   |                |                | /388626009>`__ | "Genus Felis   |
   |                |                |                | (organism)".   |
   |                |                |                |                |
   |                |                |                | Retired code   |
   |                |                |                | is inactive in |
   |                |                |                | SNOMED CT      |
   |                |                |                | (Ambiguous).   |
   +----------------+----------------+----------------+----------------+
   | D-80515        | Thrombosis     | `3963          | Replacement    |
   |                |                | 39007 <http:// | code has       |
   |                |                | snomed.info/id | meaning of     |
   |                |                | /396339007>`__ | "Thrombus".    |
   |                |                |                |                |
   |                |                |                | Retired code   |
   |                |                |                | does not exist |
   |                |                |                | SNOMED CT.     |
   +----------------+----------------+----------------+----------------+
   | A-26A06        | Fixed object   |                | No             |
   |                |                |                | replacement.   |
   |                |                |                |                |
   |                |                |                | Retired code   |
   |                |                |                | does not exist |
   |                |                |                | SNOMED CT.     |
   +----------------+----------------+----------------+----------------+
   | A-26A08        | Grid           |                | No             |
   |                |                |                | replacement.   |
   |                |                |                |                |
   |                |                |                | Retired code   |
   |                |                |                | does not exist |
   |                |                |                | SNOMED CT.     |
   +----------------+----------------+----------------+----------------+
   | C-C2318        | Priscoline     | `19            | Replacement    |
   |                | hydrocholoride | 041007 <http:/ | code has       |
   |                | ampuls         | /snomed.info/i | meaning of     |
   |                |                | d/19041007>`__ | "Tolazoline    |
   |                |                |                | hy             |
   |                |                |                | drocholoride". |
   |                |                |                |                |
   |                |                |                | Retired code   |
   |                |                |                | does not exist |
   |                |                |                | SNOMED CT (was |
   |                |                |                | in SNOMED RT). |
   +----------------+----------------+----------------+----------------+
   | C-B03H2        | Iopromide      | `3539          | Replacement    |
   |                |                | 03006 <http:// | code has       |
   |                |                | snomed.info/id | meaning of     |
   |                |                | /353903006>`__ | "Iopromide".   |
   |                |                |                |                |
   |                |                |                | Retired code   |
   |                |                |                | does not exist |
   |                |                |                | SNOMED CT.     |
   +----------------+----------------+----------------+----------------+
   | G-929D         | Cardiac        | `3731          | Replacement    |
   |                | c              | 05002 <http:// | code has       |
   |                | atheterization | snomed.info/id | meaning of     |
   |                | te             | /373105002>`__ | "Cardiac       |
   |                | st/challenging |                | c              |
   |                | phase          |                | atheterization |
   |                |                |                | test/challenge |
   |                |                |                | phase".        |
   |                |                |                |                |
   |                |                |                | Retired code   |
   |                |                |                | does not exist |
   |                |                |                | SNOMED CT.     |
   +----------------+----------------+----------------+----------------+
   | D6-90600       | Marfan's       | `19            | Replacement    |
   |                | Syndrome       | 346006 <http:/ | code has       |
   |                |                | /snomed.info/i | meaning of     |
   |                |                | d/19346006>`__ | "Marfan's      |
   |                |                |                | Syndrome".     |
   |                |                |                |                |
   |                |                |                | Retired code   |
   |                |                |                | does not exist |
   |                |                |                | SNOMED CT.     |
   +----------------+----------------+----------------+----------------+
   | D3-30800       | Cardiac arrest | `4104          | Replacement    |
   |                |                | 29000 <http:// | code has       |
   |                |                | snomed.info/id | meaning of     |
   |                |                | /410429000>`__ | "Cardiac       |
   |                |                |                | arrest         |
   |                |                |                | (disorder)".   |
   |                |                |                |                |
   |                |                |                | Retired code   |
   |                |                |                | is inactive in |
   |                |                |                | SNOMED CT      |
   |                |                |                | (Ambiguous).   |
   +----------------+----------------+----------------+----------------+
   | L-8BB55        | Mere cattle    | `1334          | Replacement    |
   |                | breed          | 92008 <http:// | code has       |
   |                |                | snomed.info/id | meaning of     |
   |                |                | /133492008>`__ | "Lobi cattle   |
   |                |                |                | breed          |
   |                |                |                | (organism)".   |
   |                |                |                |                |
   |                |                |                | Retired code   |
   |                |                |                | is inactive in |
   |                |                |                | SNOMED CT      |
   |                |                |                | (Ambiguous).   |
   +----------------+----------------+----------------+----------------+
   | M-34200        | Stenosis       | `4155          | Replacement    |
   |                |                | 82006 <http:// | code has       |
   |                |                | snomed.info/id | meaning of     |
   |                |                | /415582006>`__ | "Stenosis      |
   |                |                |                | (morphologic   |
   |                |                |                | abnormality)". |
   |                |                |                |                |
   |                |                |                | Retired code   |
   |                |                |                | is inactive in |
   |                |                |                | SNOMED CT      |
   |                |                |                | (Ambiguous).   |
   +----------------+----------------+----------------+----------------+
   | M-33410        | Epidermal      | `4196          | Replacement    |
   |                | inclusion cyst | 70003 <http:// | code has       |
   |                |                | snomed.info/id | meaning of     |
   |                |                | /419670003>`__ | "Epidermoid    |
   |                |                |                | cyst           |
   |                |                |                | (morphologic   |
   |                |                |                | abnormality)". |
   |                |                |                |                |
   |                |                |                | Retired code   |
   |                |                |                | is inactive in |
   |                |                |                | SNOMED CT      |
   |                |                |                | (Ambiguous).   |
   +----------------+----------------+----------------+----------------+
   | P3-00048       | Smear          | `4488          | Replacement    |
   |                | procedure      | 95004 <http:// | code has       |
   |                |                | snomed.info/id | meaning of     |
   |                |                | /448895004>`__ | "Sampling for  |
   |                |                |                | smear          |
   |                |                |                | (procedure)".  |
   |                |                |                |                |
   |                |                |                | Retired code   |
   |                |                |                | is inactive in |
   |                |                |                | SNOMED CT      |
   |                |                |                | (Ambiguous).   |
   +----------------+----------------+----------------+----------------+
   | T-70000        | Urinary tract  | `4319          | Replacement    |
   |                |                | 38005 <http:// | code has       |
   |                |                | snomed.info/id | meaning of     |
   |                |                | /431938005>`__ | "Structure of  |
   |                |                |                | urinary tract  |
   |                |                |                | proper (body   |
   |                |                |                | structure)".   |
   |                |                |                |                |
   |                |                |                | Retired code   |
   |                |                |                | is inactive in |
   |                |                |                | SNOMED CT      |
   |                |                |                | (Ambiguous).   |
   +----------------+----------------+----------------+----------------+
   | G-D150         | By inhalation  | `4464          | Replacement    |
   |                |                | 06008 <http:// | code has       |
   |                |                | snomed.info/id | meaning of     |
   |                |                | /446406008>`__ | "Inhalation    |
   |                |                |                | technique      |
   |                |                |                | (qualifier     |
   |                |                |                | value)".       |
   |                |                |                |                |
   |                |                |                | Retired code   |
   |                |                |                | is inactive in |
   |                |                |                | SNOMED CT      |
   |                |                |                | (Ambiguous).   |
   +----------------+----------------+----------------+----------------+
   | P1-03005       | Lumpectomy     | `3920          | Replacement    |
   |                |                | 21009 <http:// | code has       |
   |                |                | snomed.info/id | meaning of     |
   |                |                | /392021009>`__ | "Lumpectomy of |
   |                |                |                | breast         |
   |                |                |                | (procedure)".  |
   |                |                |                |                |
   |                |                |                | Retired code   |
   |                |                |                | is inactive in |
   |                |                |                | SNOMED CT      |
   |                |                |                | (Ambiguous).   |
   +----------------+----------------+----------------+----------------+
   | G-A264         | Calcified      | `2378          | Replacement    |
   |                |                | 97009 <http:// | code has       |
   |                |                | snomed.info/id | meaning of     |
   |                |                | /237897009>`__ | "Vascular      |
   |                |                |                | calcification  |
   |                |                |                | (disorder)".   |
   |                |                |                |                |
   |                |                |                | Retired code   |
   |                |                |                | is inactive in |
   |                |                |                | SNOMED CT      |
   |                |                |                | (Ambiguous).   |
   +----------------+----------------+----------------+----------------+
   | D7-90360       | Cyst of breast | `3992          | Replacement    |
   |                |                | 94002 <http:// | code has       |
   |                |                | snomed.info/id | meaning of     |
   |                |                | /399294002>`__ | "Cyst of       |
   |                |                |                | breast         |
   |                |                |                | (disorder)".   |
   |                |                |                |                |
   |                |                |                | Retired code   |
   |                |                |                | is inactive in |
   |                |                |                | SNOMED CT      |
   |                |                |                | (Ambiguous).   |
   +----------------+----------------+----------------+----------------+
   | R-20681        | O/E -          | `2743          | Replacement    |
   |                | l              | 03007 <http:// | code has       |
   |                | ymphadenopathy | snomed.info/id | meaning of "On |
   |                | NOS            | /274303007>`__ | examination -  |
   |                |                |                | lymph nodes    |
   |                |                |                | (finding)".    |
   |                |                |                |                |
   |                |                |                | Retired code   |
   |                |                |                | is inactive in |
   |                |                |                | SNOMED CT      |
   |                |                |                | (Limited).     |
   +----------------+----------------+----------------+----------------+
   | R-411C5        | Muscle Bridge  | `4240          | Replacement    |
   |                |                | 45003 <http:// | code has       |
   |                |                | snomed.info/id | meaning of     |
   |                |                | /424045003>`__ | "Myocardial    |
   |                |                |                | bridge of      |
   |                |                |                | coronary       |
   |                |                |                | artery         |
   |                |                |                | (disorder)".   |
   |                |                |                |                |
   |                |                |                | Retired code   |
   |                |                |                | is inactive in |
   |                |                |                | SNOMED CT      |
   |                |                |                | (Ambiguous).   |
   +----------------+----------------+----------------+----------------+
   | F-618FF        | Amphetamine    | `7038          | Replacement    |
   |                |                | 42006 <http:// | code has       |
   |                |                | snomed.info/id | meaning of     |
   |                |                | /703842006>`__ | "1-phenyl      |
   |                |                |                | propan-2-amine |
   |                |                |                | (substance)".  |
   |                |                |                |                |
   |                |                |                | Retired code   |
   |                |                |                | is inactive in |
   |                |                |                | SNOMED CT      |
   |                |                |                | (Ambiguous).   |
   +----------------+----------------+----------------+----------------+
   | DD-00001       | trauma         | `4177          | Replacement    |
   |                |                | 46004 <http:// | code has       |
   |                |                | snomed.info/id | meaning of     |
   |                |                | /417746004>`__ | "Traumatic     |
   |                |                |                | injury         |
   |                |                |                | (disorder)".   |
   |                |                |                |                |
   |                |                |                | Retired code   |
   |                |                |                | is inactive in |
   |                |                |                | SNOMED CT      |
   |                |                |                | (Ambiguous).   |
   +----------------+----------------+----------------+----------------+
   | G-A168         | Surface        | `4106          | Replacement    |
   |                |                | 79008 <http:// | code has       |
   |                |                | snomed.info/id | meaning of     |
   |                |                | /410679008>`__ | "Surface       |
   |                |                |                | (qualifier     |
   |                |                |                | value)".       |
   |                |                |                |                |
   |                |                |                | Retired code   |
   |                |                |                | is inactive in |
   |                |                |                | SNOMED CT      |
   |                |                |                | (Ambiguous).   |
   +----------------+----------------+----------------+----------------+
   | D4-31159       | Ventricular    | `30            | Replacement    |
   |                | Septal Defect  | 288003 <http:/ | code has       |
   |                |                | /snomed.info/i | meaning of     |
   |                |                | d/30288003>`__ | "Ventricular   |
   |                |                |                | septal defect  |
   |                |                |                | (disorder)".   |
   |                |                |                |                |
   |                |                |                | Retired code   |
   |                |                |                | is inactive in |
   |                |                |                | SNOMED CT      |
   |                |                |                | (Ambiguous).   |
   +----------------+----------------+----------------+----------------+
   | P5-C0610       | Brachytherapy  | `3846          | Replacement    |
   |                |                | 92006 <http:// | code has       |
   |                |                | snomed.info/id | meaning of     |
   |                |                | /384692006>`__ | "Intracavitary |
   |                |                |                | brachytherapy  |
   |                |                |                | (procedure)".  |
   |                |                |                |                |
   |                |                |                | Retired code   |
   |                |                |                | is inactive in |
   |                |                |                | SNOMED CT      |
   |                |                |                | (Ambiguous).   |
   +----------------+----------------+----------------+----------------+
   | L-808C9        | Dingo dog      | `7098          | Replacement    |
   |                | breed          | 53007 <http:// | code has       |
   |                |                | snomed.info/id | meaning of     |
   |                |                | /709853007>`__ | "Canis lupus   |
   |                |                |                | dingo          |
   |                |                |                | (organism)".   |
   |                |                |                |                |
   |                |                |                | Retired code   |
   |                |                |                | is inactive in |
   |                |                |                | SNOMED CT      |
   |                |                |                | (Erroneous).   |
   +----------------+----------------+----------------+----------------+
   | G-A105         | Anterior       | `2555          | Replacement    |
   |                |                | 49009 <http:// | code has       |
   |                |                | snomed.info/id | meaning of     |
   |                |                | /255549009>`__ | "Anterior      |
   |                |                |                | (qualifier     |
   |                |                |                | value)".       |
   |                |                |                |                |
   |                |                |                | Retired code   |
   |                |                |                | is inactive in |
   |                |                |                | SNOMED CT      |
   |                |                |                | (Ambiguous).   |
   +----------------+----------------+----------------+----------------+
   | T-48052        | Basilic vein   | `19            | Replacement    |
   |                |                | 715009 <http:/ | code has       |
   |                |                | /snomed.info/i | meaning of     |
   |                |                | d/19715009>`__ | "Structure of  |
   |                |                |                | basilic vein   |
   |                |                |                | (body          |
   |                |                |                | structure)".   |
   |                |                |                |                |
   |                |                |                | Retired code   |
   |                |                |                | is inactive in |
   |                |                |                | SNOMED CT      |
   |                |                |                | (Ambiguous).   |
   +----------------+----------------+----------------+----------------+
   | G-A106         | Posterior      | `2555          | Replacement    |
   |                |                | 51008 <http:// | code has       |
   |                |                | snomed.info/id | meaning of     |
   |                |                | /255551008>`__ | "Posterior     |
   |                |                |                | (qualifier     |
   |                |                |                | value)".       |
   |                |                |                |                |
   |                |                |                | Retired code   |
   |                |                |                | is inactive in |
   |                |                |                | SNOMED CT      |
   |                |                |                | (Ambiguous).   |
   +----------------+----------------+----------------+----------------+
   | D3-29013       | Mitral valve   | `4097          | Replacement    |
   |                | prolapse       | 12001 <http:// | code has       |
   |                |                | snomed.info/id | meaning of     |
   |                |                | /409712001>`__ | "Mitral valve  |
   |                |                |                | prolapse       |
   |                |                |                | (disorder)".   |
   |                |                |                |                |
   |                |                |                | Retired code   |
   |                |                |                | is inactive in |
   |                |                |                | SNOMED CT      |
   |                |                |                | (Ambiguous).   |
   +----------------+----------------+----------------+----------------+
   | T-41040        | Iliac arterial | `2997          | Replacement    |
   |                | system         | 16001 <http:// | code has       |
   |                |                | snomed.info/id | meaning of     |
   |                |                | /299716001>`__ | "Iliac and/or  |
   |                |                |                | femoral artery |
   |                |                |                | structures     |
   |                |                |                | (body          |
   |                |                |                | structure)".   |
   |                |                |                |                |
   |                |                |                | Retired code   |
   |                |                |                | is inactive in |
   |                |                |                | SNOMED CT      |
   |                |                |                | (Ambiguous).   |
   +----------------+----------------+----------------+----------------+
   | G-A109         | Medial         | `2555          | Replacement    |
   |                |                | 61001 <http:// | code has       |
   |                |                | snomed.info/id | meaning of     |
   |                |                | /255561001>`__ | "Medial        |
   |                |                |                | (qualifier     |
   |                |                |                | value)".       |
   |                |                |                |                |
   |                |                |                | Retired code   |
   |                |                |                | is inactive in |
   |                |                |                | SNOMED CT      |
   |                |                |                | (Ambiguous).   |
   +----------------+----------------+----------------+----------------+
   | G-A109         | Median         |                | No replacement |
   |                |                |                | SNOMED code    |
   |                |                |                | exists.        |
   |                |                |                |                |
   |                |                |                | `(130290, DCM. |
   |                |                |                | "Median") <#   |
   |                |                |                | DCM_130290>`__ |
   |                |                |                | may be used    |
   |                |                |                | instead.       |
   |                |                |                |                |
   |                |                |                | Retired code   |
   |                |                |                | is inactive in |
   |                |                |                | SNOMED CT      |
   |                |                |                | (Ambiguous).   |
   +----------------+----------------+----------------+----------------+
   | G-A109         | Middle         |                | No replacement |
   |                |                |                | SNOMED code    |
   |                |                |                | exists.        |
   |                |                |                |                |
   |                |                |                | `(C25569,      |
   |                |                |                | NCIt,          |
   |                |                |                | "Middle")      |
   |                |                |                | <http://ncit.n |
   |                |                |                | ci.nih.gov/nci |
   |                |                |                | tbrowser/Conce |
   |                |                |                | ptReport.jsp?d |
   |                |                |                | ictionary=NCI_ |
   |                |                |                | Thesaurus&ns=N |
   |                |                |                | CI_Thesaurus&c |
   |                |                |                | ode=C25569>`__ |
   |                |                |                | may be used    |
   |                |                |                | instead.       |
   |                |                |                |                |
   |                |                |                | Retired code   |
   |                |                |                | is inactive in |
   |                |                |                | SNOMED CT      |
   |                |                |                | (Ambiguous).   |
   +----------------+----------------+----------------+----------------+
   | `R-            | Median         |                | No replacement |
   | 4081A <http:// |                |                | SNOMED code    |
   | snomed.info/id |                |                | exists.        |
   | /260528009>`__ |                |                |                |
   |                |                |                | `(130290, DCM. |
   |                |                |                | "Median") <#   |
   |                |                |                | DCM_130290>`__ |
   |                |                |                | may be used    |
   |                |                |                | instead.       |
   |                |                |                |                |
   |                |                |                | Retired code   |
   |                |                |                | is ambiguous   |
   |                |                |                | since it has   |
   |                |                |                | synomyms of    |
   |                |                |                | "middle" and   |
   |                |                |                | "median".      |
   +----------------+----------------+----------------+----------------+
   | `R-            | Middle         |                | No replacement |
   | 4081A <http:// |                |                | SNOMED code    |
   | snomed.info/id |                |                | exists.        |
   | /260528009>`__ |                |                |                |
   |                |                |                | `(C25569,      |
   |                |                |                | NCIt,          |
   |                |                |                | "Middle")      |
   |                |                |                | <http://ncit.n |
   |                |                |                | ci.nih.gov/nci |
   |                |                |                | tbrowser/Conce |
   |                |                |                | ptReport.jsp?d |
   |                |                |                | ictionary=NCI_ |
   |                |                |                | Thesaurus&ns=N |
   |                |                |                | CI_Thesaurus&c |
   |                |                |                | ode=C25569>`__ |
   |                |                |                | may be used    |
   |                |                |                | instead.       |
   |                |                |                |                |
   |                |                |                | Retired code   |
   |                |                |                | is ambiguous   |
   |                |                |                | since it has   |
   |                |                |                | synomyms of    |
   |                |                |                | "middle" and   |
   |                |                |                | "median".      |
   +----------------+----------------+----------------+----------------+
   | D4-32508       | Fistula        | `3730          | Retired code   |
   |                | coronary to    | 95005 <http:// | actually has   |
   |                | right atrium   | snomed.info/id | meaning in     |
   |                |                | /373095005>`__ | SNOMED CT of   |
   |                |                |                | "Coronary      |
   |                |                |                | artery arising |
   |                |                |                | from aorta     |
   |                |                |                | (disorder)".   |
   |                |                |                |                |
   |                |                |                | Replacement    |
   |                |                |                | code has       |
   |                |                |                | meaning of     |
   |                |                |                | "Coronary      |
   |                |                |                | artery fistula |
   |                |                |                | to right       |
   |                |                |                | atrium         |
   |                |                |                | (disorder)".   |
   |                |                |                |                |
   |                |                |                | Retired code   |
   |                |                |                | is inactive in |
   |                |                |                | SNOMED CT      |
   |                |                |                | (Ambiguous).   |
   +----------------+----------------+----------------+----------------+
   | G-A22A         | Length         | `4106          | Replacement    |
   |                |                | 68003 <http:// | code has       |
   |                |                | snomed.info/id | meaning of     |
   |                |                | /410668003>`__ | "Length        |
   |                |                |                | property       |
   |                |                |                | (qualifier     |
   |                |                |                | value)".       |
   |                |                |                |                |
   |                |                |                | Retired code   |
   |                |                |                | is inactive in |
   |                |                |                | SNOMED CT      |
   |                |                |                | (Ambiguous).   |
   +----------------+----------------+----------------+----------------+
   | T-D8100        | Axilla         | `91            | Replacement    |
   |                |                | 470000 <http:/ | code has       |
   |                |                | /snomed.info/i | meaning of     |
   |                |                | d/91470000>`__ | "Axillary      |
   |                |                |                | region         |
   |                |                |                | structure      |
   |                |                |                | (body          |
   |                |                |                | structure)".   |
   |                |                |                |                |
   |                |                |                | Retired code   |
   |                |                |                | is inactive in |
   |                |                |                | SNOMED CT      |
   |                |                |                | (Ambiguous).   |
   +----------------+----------------+----------------+----------------+
   | R-102BC        | Internal       | `6983          | Replacement    |
   |                | Carotid Artery | 48000 <http:// | code has       |
   |                | C6 segment     | snomed.info/id | meaning of     |
   |                |                | /698348000>`__ | "Structure of  |
   |                |                |                | ophthalmic     |
   |                |                |                | segment of     |
   |                |                |                | internal       |
   |                |                |                | carotid artery |
   |                |                |                | (body          |
   |                |                |                | structure)".   |
   |                |                |                |                |
   |                |                |                | Retired code   |
   |                |                |                | is inactive in |
   |                |                |                | SNOMED CT      |
   |                |                |                | (Ambiguous).   |
   +----------------+----------------+----------------+----------------+
   | L-80A50        | Shorthaired    | `1326          | Replacement    |
   |                | cat            | 65002 <http:// | code has       |
   |                |                | snomed.info/id | meaning of     |
   |                |                | /132665002>`__ | "Shorthair cat |
   |                |                |                | breed          |
   |                |                |                | (organism)".   |
   |                |                |                |                |
   |                |                |                | Retired code   |
   |                |                |                | is inactive in |
   |                |                |                | SNOMED CT      |
   |                |                |                | (Ambiguous).   |
   +----------------+----------------+----------------+----------------+
   | R-F5517        | Pulmonary      | `1112          | Replacement    |
   |                | arteriovenous  | 89009 <http:// | code has       |
   |                | fistula        | snomed.info/id | meaning of     |
   |                |                | /111289009>`__ | "Arteriovenous |
   |                |                |                | fistula of     |
   |                |                |                | pulmonary      |
   |                |                |                | vessels        |
   |                |                |                | (disorder)".   |
   |                |                |                |                |
   |                |                |                | Retired code   |
   |                |                |                | is inactive in |
   |                |                |                | SNOMED CT      |
   |                |                |                | (Ambiguous).   |
   +----------------+----------------+----------------+----------------+
   | F-B2110        | Epinephrine    | `3873          | Replacement    |
   |                |                | 62001 <http:// | code has       |
   |                |                | snomed.info/id | meaning of     |
   |                |                | /387362001>`__ | "Epinephrine   |
   |                |                |                | (substance)".  |
   |                |                |                |                |
   |                |                |                | Retired code   |
   |                |                |                | is inactive in |
   |                |                |                | SNOMED CT      |
   |                |                |                | (Ambiguous).   |
   +----------------+----------------+----------------+----------------+
   | T-70010        | Upper urinary  | `4314          | Replacement    |
   |                | tract          | 91007 <http:// | code has       |
   |                |                | snomed.info/id | meaning of     |
   |                |                | /431491007>`__ | "Structure of  |
   |                |                |                | upper urinary  |
   |                |                |                | tract proper   |
   |                |                |                | (body          |
   |                |                |                | structure)".   |
   |                |                |                |                |
   |                |                |                | Retired code   |
   |                |                |                | is inactive in |
   |                |                |                | SNOMED CT      |
   |                |                |                | (Ambiguous).   |
   +----------------+----------------+----------------+----------------+
   | C-21005        | Ethanol        | `4194          | Replacement    |
   |                |                | 42005 <http:// | code has       |
   |                |                | snomed.info/id | meaning of     |
   |                |                | /419442005>`__ | "Ethyl alcohol |
   |                |                |                | (substance)".  |
   |                |                |                |                |
   |                |                |                | Retired code   |
   |                |                |                | is inactive in |
   |                |                |                | SNOMED CT      |
   |                |                |                | (Ambiguous).   |
   +----------------+----------------+----------------+----------------+
   | D3-13000       | Coronary       | `53            | Replacement    |
   |                | artery disease | 741008 <http:/ | code has       |
   |                |                | /snomed.info/i | meaning of     |
   |                |                | d/53741008>`__ | "Coronary      |
   |                |                |                | ar             |
   |                |                |                | teriosclerosis |
   |                |                |                | (disorder)".   |
   |                |                |                |                |
   |                |                |                | Retired code   |
   |                |                |                | is inactive in |
   |                |                |                | SNOMED CT      |
   |                |                |                | (Ambiguous).   |
   +----------------+----------------+----------------+----------------+
   | T-C4510        | mesenteric     | `2797          | Replacement    |
   |                | lymph node     | 95009 <http:// | code has       |
   |                |                | snomed.info/id | meaning of     |
   |                |                | /279795009>`__ | "Structure of  |
   |                |                |                | lymph node of  |
   |                |                |                | mesentery      |
   |                |                |                | (body          |
   |                |                |                | structure)".   |
   |                |                |                |                |
   |                |                |                | Retired code   |
   |                |                |                | is inactive in |
   |                |                |                | SNOMED CT      |
   |                |                |                | (Ambiguous).   |
   +----------------+----------------+----------------+----------------+
   | C-A7040        | Thrombin       | `36            | Replacement    |
   |                | preparation    | 176003 <http:/ | code has       |
   |                |                | /snomed.info/i | meaning of     |
   |                |                | d/36176003>`__ | "Thrombin      |
   |                |                |                | (substance)".  |
   |                |                |                |                |
   |                |                |                | Retired code   |
   |                |                |                | is inactive in |
   |                |                |                | SNOMED CT      |
   |                |                |                | (Ambiguous).   |
   +----------------+----------------+----------------+----------------+
   | G-A112         | External       | `2610          | Replacement    |
   |                |                | 74009 <http:// | code has       |
   |                |                | snomed.info/id | meaning of     |
   |                |                | /261074009>`__ | "External      |
   |                |                |                | (qualifier     |
   |                |                |                | value)".       |
   |                |                |                |                |
   |                |                |                | Retired code   |
   |                |                |                | is inactive in |
   |                |                |                | SNOMED CT      |
   |                |                |                | (Ambiguous).   |
   +----------------+----------------+----------------+----------------+
   | G-A113         | Internal       | `2605          | Replacement    |
   |                |                | 21003 <http:// | code has       |
   |                |                | snomed.info/id | meaning of     |
   |                |                | /260521003>`__ | "Internal      |
   |                |                |                | (qualifier     |
   |                |                |                | value)".       |
   |                |                |                |                |
   |                |                |                | Retired code   |
   |                |                |                | is inactive in |
   |                |                |                | SNOMED CT      |
   |                |                |                | (Ambiguous).   |
   +----------------+----------------+----------------+----------------+
   | F-A5581        | Vasovagal      | `3986          | Replacement    |
   |                | attack         | 65005 <http:// | code has       |
   |                |                | snomed.info/id | meaning of     |
   |                |                | /398665005>`__ | "Vasovagal     |
   |                |                |                | syncope        |
   |                |                |                | (disorder)".   |
   |                |                |                |                |
   |                |                |                | Retired code   |
   |                |                |                | is inactive in |
   |                |                |                | SNOMED CT      |
   |                |                |                | (Ambiguous).   |
   +----------------+----------------+----------------+----------------+
   | C-2287C        | methyl violet  | `3872          | Replacement    |
   |                | stain          | 39001 <http:// | code has       |
   |                |                | snomed.info/id | meaning of     |
   |                |                | /387239001>`__ | "Gentian       |
   |                |                |                | violet         |
   |                |                |                | (substance)".  |
   |                |                |                |                |
   |                |                |                | Retired code   |
   |                |                |                | is inactive in |
   |                |                |                | SNOMED CT      |
   |                |                |                | (Ambiguous).   |
   +----------------+----------------+----------------+----------------+
   | T-41070        | Abdominal      | `              | Replacement    |
   |                | aorta and its  | 7832008 <http: | code has       |
   |                | branches       | //snomed.info/ | meaning of     |
   |                |                | id/7832008>`__ | "Abdominal     |
   |                |                |                | aorta          |
   |                |                |                | structure      |
   |                |                |                | (body          |
   |                |                |                | structure)".   |
   |                |                |                |                |
   |                |                |                | Retired code   |
   |                |                |                | is inactive in |
   |                |                |                | SNOMED CT      |
   |                |                |                | (Ambiguous).   |
   +----------------+----------------+----------------+----------------+
   | G-A115         | Inferior       | `2610          | Replacement    |
   |                |                | 89000 <http:// | code has       |
   |                |                | snomed.info/id | meaning of     |
   |                |                | /261089000>`__ | "Inferior      |
   |                |                |                | (qualifier     |
   |                |                |                | value)".       |
   |                |                |                |                |
   |                |                |                | Retired code   |
   |                |                |                | is inactive in |
   |                |                |                | SNOMED CT      |
   |                |                |                | (Ambiguous).   |
   +----------------+----------------+----------------+----------------+
   | C-80130        | Cardiac        | `3732          | Replacement    |
   |                | adrenergic     | 63004 <http:// | code has       |
   |                | blocking agent | snomed.info/id | meaning of     |
   |                |                | /373263004>`__ | "Cardiac       |
   |                |                |                | adrenergic     |
   |                |                |                | blocking agent |
   |                |                |                | (substance)".  |
   |                |                |                |                |
   |                |                |                | Retired code   |
   |                |                |                | is inactive in |
   |                |                |                | SNOMED CT      |
   |                |                |                | (Ambiguous).   |
   +----------------+----------------+----------------+----------------+
   | G-A116         | Superior       | `2642          | Replacement    |
   |                |                | 17000 <http:// | code has       |
   |                |                | snomed.info/id | meaning of     |
   |                |                | /264217000>`__ | "Superior      |
   |                |                |                | (qualifier     |
   |                |                |                | value)".       |
   |                |                |                |                |
   |                |                |                | Retired code   |
   |                |                |                | is inactive in |
   |                |                |                | SNOMED CT      |
   |                |                |                | (Ambiguous).   |
   +----------------+----------------+----------------+----------------+
   | M-35100        | Thrombus       | `3963          | Replacement    |
   |                |                | 39007 <http:// | code has       |
   |                |                | snomed.info/id | meaning of     |
   |                |                | /396339007>`__ | "Thrombus      |
   |                |                |                | (morphologic   |
   |                |                |                | abnormality)". |
   |                |                |                |                |
   |                |                |                | Retired code   |
   |                |                |                | is inactive in |
   |                |                |                | SNOMED CT      |
   |                |                |                | (Ambiguous).   |
   +----------------+----------------+----------------+----------------+
   | C-80125        | Cardiac        |                | Retired code   |
   |                | depressant     |                | is inactive in |
   |                | agent          |                | SNOMED CT      |
   |                |                |                | (Ambiguous).   |
   +----------------+----------------+----------------+----------------+
   | P1-31926       | Creation of    | `2330          | Replacement    |
   |                | conduit of     | 22006 <http:// | code has       |
   |                | right atrium   | snomed.info/id | meaning of     |
   |                | and pulmonary  | /233022006>`__ | "Construction  |
   |                | artery         |                | of conduit -   |
   |                |                |                | right atrium   |
   |                |                |                | to pulmonary   |
   |                |                |                | trunk".        |
   |                |                |                |                |
   |                |                |                | Retired code   |
   |                |                |                | is inactive in |
   |                |                |                | SNOMED CT      |
   |                |                |                | (Duplicate).   |
   +----------------+----------------+----------------+----------------+
   | T-D06B6        | Nuchal region  | `7000          | Replacement    |
   |                | of scalp       | 32006 <http:// | code has       |
   |                |                | snomed.info/id | meaning of     |
   |                |                | /700032006>`__ | "Structure of  |
   |                |                |                | occipital      |
   |                |                |                | region of      |
   |                |                |                | scalp".        |
   |                |                |                |                |
   |                |                |                | Retired code   |
   |                |                |                | is inactive in |
   |                |                |                | SNOMED CT      |
   |                |                |                | (Ambiguous).   |
   +----------------+----------------+----------------+----------------+
   | T-49423        | Lateral calf   | `7147          | Replacement    |
   |                | perforator     | 54004 <http:// | code has       |
   |                |                | snomed.info/id | meaning of     |
   |                |                | /714754004>`__ | "Structure of  |
   |                |                |                | lateral calf   |
   |                |                |                | perforator".   |
   |                |                |                |                |
   |                |                |                | Retired code   |
   |                |                |                | is inactive in |
   |                |                |                | SNOMED CT      |
   |                |                |                | (Ambiguous).   |
   +----------------+----------------+----------------+----------------+
   | T-4942C        | Thigh          | `7147          | Replacement    |
   |                | perforator     | 59009 <http:// | code has       |
   |                |                | snomed.info/id | meaning of     |
   |                |                | /714759009>`__ | "Structure of  |
   |                |                |                | thigh          |
   |                |                |                | perforator".   |
   |                |                |                |                |
   |                |                |                | Retired code   |
   |                |                |                | is inactive in |
   |                |                |                | SNOMED CT      |
   |                |                |                | (Ambiguous).   |
   +----------------+----------------+----------------+----------------+
   | G-A231         | Acute          | `3739          | Replacement    |
   |                |                | 33003 <http:// | code has       |
   |                |                | snomed.info/id | meaning of     |
   |                |                | /373933003>`__ | "Acute onset   |
   |                |                |                | (qualifier     |
   |                |                |                | value)".       |
   |                |                |                |                |
   |                |                |                | Retired code   |
   |                |                |                | is inactive in |
   |                |                |                | SNOMED CT      |
   |                |                |                | (Erroneous).   |
   +----------------+----------------+----------------+----------------+
   | D3-28012       | Subacute       | `73            | Replacement    |
   |                | bacterial      | 774007 <http:/ | code has       |
   |                | endocarditis   | /snomed.info/i | meaning of     |
   |                |                | d/73774007>`__ | "Subacute      |
   |                |                |                | bacterial      |
   |                |                |                | endocarditis   |
   |                |                |                | (disorder)".   |
   |                |                |                |                |
   |                |                |                | Retired code   |
   |                |                |                | was used       |
   |                |                |                | incorrectly    |
   |                |                |                | because of     |
   |                |                |                | digit          |
   |                |                |                | transposition  |
   |                |                |                | and means      |
   |                |                |                | something      |
   |                |                |                | else, and is   |
   |                |                |                | also inactive  |
   |                |                |                | in SNOMED CT   |
   |                |                |                | (Limited).     |
   +----------------+----------------+----------------+----------------+
   | C-2288B        | alcian blue    | `              | Replacement    |
   |                | stain          | 4656000 <http: | code has       |
   |                |                | //snomed.info/ | meaning of     |
   |                |                | id/4656000>`__ | "Alcian blue   |
   |                |                |                | 8GX stain      |
   |                |                |                | (substance)".  |
   |                |                |                |                |
   |                |                |                | Retired code   |
   |                |                |                | is inactive in |
   |                |                |                | SNOMED CT      |
   |                |                |                | (Duplicate).   |
   +----------------+----------------+----------------+----------------+
   | R-002CE        | Aneurysmal     | `2553          | Replacement    |
   |                |                | 78009 <http:// | code has       |
   |                |                | snomed.info/id | meaning of     |
   |                |                | /255378009>`__ | "Aneurysmal    |
   |                |                |                | (qualifier     |
   |                |                |                | value)".       |
   |                |                |                |                |
   |                |                |                | Retired code   |
   |                |                |                | is inactive in |
   |                |                |                | SNOMED CT      |
   |                |                |                | (Duplicate).   |
   +----------------+----------------+----------------+----------------+
   | L-80010        | Wuzhishan pig  | `1322          | Replacement    |
   |                | breed          | 22009 <http:// | code has       |
   |                |                | snomed.info/id | meaning of     |
   |                |                | /132222009>`__ | "Wuzhishan pig |
   |                |                |                | breed          |
   |                |                |                | (organism)".   |
   |                |                |                |                |
   |                |                |                | Retired code   |
   |                |                |                | was used       |
   |                |                |                | incorrectly    |
   |                |                |                | and means      |
   |                |                |                | something      |
   |                |                |                | else, and is   |
   |                |                |                | also inactive  |
   |                |                |                | in SNOMED CT   |
   |                |                |                | (Duplicate).   |
   +----------------+----------------+----------------+----------------+
   | T-41066        | Artery         | `51            | Replacement    |
   |                |                | 114001 <http:/ | code has       |
   |                |                | /snomed.info/i | meaning of     |
   |                |                | d/51114001>`__ | "Arterial      |
   |                |                |                | structure      |
   |                |                |                | (body          |
   |                |                |                | structure)".   |
   |                |                |                |                |
   |                |                |                | Retired code   |
   |                |                |                | is inactive in |
   |                |                |                | SNOMED CT      |
   |                |                |                | (Limited).     |
   +----------------+----------------+----------------+----------------+
   | L-80506        | Beltsville pig |                | No             |
   |                | #1 pig breed   |                | replacement.   |
   |                |                |                |                |
   |                |                |                | Retired code   |
   |                |                |                | is inactive in |
   |                |                |                | SNOMED CT      |
   |                |                |                | (Duplicate).   |
   +----------------+----------------+----------------+----------------+
   | L-80507        | Beltsville pig |                | No             |
   |                | #2 pig breed   |                | replacement.   |
   |                |                |                |                |
   |                |                |                | Retired code   |
   |                |                |                | is inactive in |
   |                |                |                | SNOMED CT      |
   |                |                |                | (Duplicate).   |
   +----------------+----------------+----------------+----------------+
   | L-807E6        | Bordeaux Dog   | `1323          | Replacement    |
   |                | breed          | 89001 <http:// | code has       |
   |                |                | snomed.info/id | meaning of     |
   |                |                | /132389001>`__ | "Dogue de      |
   |                |                |                | Bordeaux dog   |
   |                |                |                | breed          |
   |                |                |                | (organism)".   |
   |                |                |                |                |
   |                |                |                | Retired code   |
   |                |                |                | is inactive in |
   |                |                |                | SNOMED CT      |
   |                |                |                | (Duplicate).   |
   +----------------+----------------+----------------+----------------+
   | L-80551        | CPF pig #1 pig |                | No             |
   |                | breed          |                | replacement.   |
   |                |                |                |                |
   |                |                |                | Retired code   |
   |                |                |                | is inactive in |
   |                |                |                | SNOMED CT      |
   |                |                |                | (Duplicate).   |
   +----------------+----------------+----------------+----------------+
   | L-80552        | CPF pig #2 pig |                | No             |
   |                | breed          |                | replacement.   |
   |                |                |                |                |
   |                |                |                | Retired code   |
   |                |                |                | is inactive in |
   |                |                |                | SNOMED CT      |
   |                |                |                | (Duplicate).   |
   +----------------+----------------+----------------+----------------+
   | D4-31320       | Common Atrium  | `2532          | Replacement    |
   |                |                | 76007 <http:// | code has       |
   |                |                | snomed.info/id | meaning of     |
   |                |                | /253276007>`__ | "Cor           |
   |                |                |                | triloculare    |
   |                |                |                | biventriculare |
   |                |                |                | (disorder)".   |
   |                |                |                |                |
   |                |                |                | Retired code   |
   |                |                |                | is inactive in |
   |                |                |                | SNOMED CT      |
   |                |                |                | (Duplicate).   |
   +----------------+----------------+----------------+----------------+
   | M-32206        | Compound       | `85            | Replacement    |
   |                | Aneurysm       | 726003 <http:/ | code has       |
   |                |                | /snomed.info/i | meaning of     |
   |                |                | d/85726003>`__ | "Mixed         |
   |                |                |                | aneurysm       |
   |                |                |                | (morphologic   |
   |                |                |                | abnormality)". |
   |                |                |                |                |
   |                |                |                | Retired code   |
   |                |                |                | is inactive in |
   |                |                |                | SNOMED CT      |
   |                |                |                | (Duplicate).   |
   +----------------+----------------+----------------+----------------+
   | P5-B3008       | Contrast       | `4332          | Replacement    |
   |                | ec             | 31002 <http:// | code has       |
   |                | hocardiography | snomed.info/id | meaning of     |
   |                |                | /433231002>`__ | "Contrast      |
   |                |                |                | ec             |
   |                |                |                | hocardiography |
   |                |                |                | (procedure)".  |
   |                |                |                |                |
   |                |                |                | Retired code   |
   |                |                |                | is inactive in |
   |                |                |                | SNOMED CT      |
   |                |                |                | (Retired       |
   |                |                |                | without stated |
   |                |                |                | reason).       |
   +----------------+----------------+----------------+----------------+
   | C-2283D        | crystal violet | `3872          | Replacement    |
   |                | stain          | 39001 <http:// | code has       |
   |                |                | snomed.info/id | meaning of     |
   |                |                | /387239001>`__ | "Gentian       |
   |                |                |                | violet         |
   |                |                |                | (substance)".  |
   |                |                |                |                |
   |                |                |                | Retired code   |
   |                |                |                | is inactive in |
   |                |                |                | SNOMED CT      |
   |                |                |                | (Duplicate).   |
   +----------------+----------------+----------------+----------------+
   | P1-86101       | Decompression  |                | No             |
   |                | amniocentesis  |                | replacement.   |
   |                | [decompression |                |                |
   |                | of amnion]     |                | Retired code   |
   |                |                |                | is inactive in |
   |                |                |                | SNOMED CT      |
   |                |                |                | (Ambiguous).   |
   +----------------+----------------+----------------+----------------+
   | F-31120        | Diastolic      | `2716          | Replacement    |
   |                | Pressure       | 50006 <http:// | code has       |
   |                |                | snomed.info/id | meaning of     |
   |                |                | /271650006>`__ | "Diastolic     |
   |                |                |                | blood pressure |
   |                |                |                | (observable    |
   |                |                |                | entity)".      |
   |                |                |                |                |
   |                |                |                | Retired code   |
   |                |                |                | is inactive in |
   |                |                |                | SNOMED CT      |
   |                |                |                | (Duplicate).   |
   +----------------+----------------+----------------+----------------+
   | C-B03AA        | Dimeglumine    | `4048          | Replacement    |
   |                | gadopentetate  | 46007 <http:// | code has       |
   |                |                | snomed.info/id | meaning of     |
   |                |                | /404846007>`__ | "Gadopentetate |
   |                |                |                | dimeglumine    |
   |                |                |                | (product)".    |
   |                |                |                |                |
   |                |                |                | Retired code   |
   |                |                |                | is inactive in |
   |                |                |                | SNOMED CT      |
   |                |                |                | (Duplicate).   |
   +----------------+----------------+----------------+----------------+
   | R-002FE        | Double vessel  | `1948          | Replacement    |
   |                | coronary       | 43003 <http:// | code has       |
   |                | artery         | snomed.info/id | meaning of     |
   |                | disease.       | /194843003>`__ | "Double        |
   |                |                |                | coronary       |
   |                |                |                | vessel disease |
   |                |                |                | (disorder)".   |
   |                |                |                |                |
   |                |                |                | Retired code   |
   |                |                |                | is inactive in |
   |                |                |                | SNOMED CT      |
   |                |                |                | (Duplicate).   |
   +----------------+----------------+----------------+----------------+
   | F-32011        | End diastole   | `4161          | Replacement    |
   |                |                | 90007 <http:// | code has       |
   |                |                | snomed.info/id | meaning of     |
   |                |                | /416190007>`__ | "End diastole  |
   |                |                |                | (qualifier     |
   |                |                |                | value)".       |
   |                |                |                |                |
   |                |                |                | Retired code   |
   |                |                |                | is inactive in |
   |                |                |                | SNOMED CT      |
   |                |                |                | (Erroneous).   |
   +----------------+----------------+----------------+----------------+
   | T-D0788        | Carpus         | `              | Replacement    |
   |                |                | 8205005 <http: | code has       |
   |                |                | //snomed.info/ | meaning of     |
   |                |                | id/8205005>`__ | "Wrist region  |
   |                |                |                | structure      |
   |                |                |                | (body          |
   |                |                |                | structure)".   |
   |                |                |                |                |
   |                |                |                | Retired code   |
   |                |                |                | is inactive in |
   |                |                |                | SNOMED CT      |
   |                |                |                | (Duplicate).   |
   +----------------+----------------+----------------+----------------+
   | T-A1504        | Cranial        | `33            | Replacement    |
   |                | Subarachnoid   | 930006 <http:/ | code has       |
   |                | Space          | /snomed.info/i | meaning of     |
   |                |                | d/33930006>`__ | "Structure of  |
   |                |                |                | subarachnoid   |
   |                |                |                | space of brain |
   |                |                |                | (body          |
   |                |                |                | structure)".   |
   |                |                |                |                |
   |                |                |                | Retired code   |
   |                |                |                | is inactive in |
   |                |                |                | SNOMED CT      |
   |                |                |                | (Duplicate).   |
   +----------------+----------------+----------------+----------------+
   | T-11096        | Tarsus         | `1083          | Replacement    |
   |                |                | 71006 <http:// | code has       |
   |                |                | snomed.info/id | meaning of     |
   |                |                | /108371006>`__ | "Bone          |
   |                |                |                | structure of   |
   |                |                |                | tarsus (body   |
   |                |                |                | structure)".   |
   |                |                |                |                |
   |                |                |                | Retired code   |
   |                |                |                | is inactive in |
   |                |                |                | SNOMED CT      |
   |                |                |                | (Ambiguous).   |
   +----------------+----------------+----------------+----------------+
   | G-0325         | Family history | `4297          | Replacement    |
   |                | of breast      | 40004 <http:// | code has       |
   |                | cancer         | snomed.info/id | meaning of     |
   |                |                | /429740004>`__ | "Family        |
   |                |                |                | history of     |
   |                |                |                | malignant      |
   |                |                |                | neoplasm of    |
   |                |                |                | breast         |
   |                |                |                | (situation)".  |
   |                |                |                |                |
   |                |                |                | Retired code   |
   |                |                |                | is inactive in |
   |                |                |                | SNOMED CT      |
   |                |                |                | (Duplicate).   |
   +----------------+----------------+----------------+----------------+
   | F-0147C        | Hematoma -     | `2132          | Replacement    |
   |                | postoperative  | 62007 <http:// | code has       |
   |                |                | snomed.info/id | meaning of     |
   |                |                | /213262007>`__ | "Postoperative |
   |                |                |                | hematoma       |
   |                |                |                | formation      |
   |                |                |                | (disorder)".   |
   |                |                |                |                |
   |                |                |                | Retired code   |
   |                |                |                | is inactive in |
   |                |                |                | SNOMED CT      |
   |                |                |                | (Duplicate).   |
   +----------------+----------------+----------------+----------------+
   | PA-50032       | Pulmonary      | `1284          | Replacement    |
   |                | capillary      | 48001 <http:// | code has       |
   |                | wedge method   | snomed.info/id | meaning of     |
   |                |                | /128448001>`__ | "Pulmonary     |
   |                |                |                | capillary      |
   |                |                |                | wedge pressure |
   |                |                |                | waveform,      |
   |                |                |                | function       |
   |                |                |                | (observable    |
   |                |                |                | entity)".      |
   |                |                |                |                |
   |                |                |                | Retired code   |
   |                |                |                | is inactive in |
   |                |                |                | SNOMED CT      |
   |                |                |                | (Duplicate).   |
   +----------------+----------------+----------------+----------------+
   | C-A6920        | Injectable     | `4183          | Replacement    |
   |                | fibrinogen     | 26009 <http:// | code has       |
   |                |                | snomed.info/id | meaning of     |
   |                |                | /418326009>`__ | "Human         |
   |                |                |                | fibrinogen     |
   |                |                |                | (substance)".  |
   |                |                |                |                |
   |                |                |                | Retired code   |
   |                |                |                | is inactive in |
   |                |                |                | SNOMED CT      |
   |                |                |                | (Duplicate).   |
   +----------------+----------------+----------------+----------------+
   | G-D105         | Intracutaneous | `3724          | Replacement    |
   |                | route          | 64004 <http:// | code has       |
   |                |                | snomed.info/id | meaning of     |
   |                |                | /372464004>`__ | "Intradermal   |
   |                |                |                | route          |
   |                |                |                | (qualifier     |
   |                |                |                | value)".       |
   |                |                |                |                |
   |                |                |                | Retired code   |
   |                |                |                | is inactive in |
   |                |                |                | SNOMED CT      |
   |                |                |                | (Duplicate).   |
   +----------------+----------------+----------------+----------------+
   | F-00585        | Lesion Finding | `3005          | Replacement    |
   |                |                | 77008 <http:// | code has       |
   |                |                | snomed.info/id | meaning of     |
   |                |                | /300577008>`__ | "Finding of    |
   |                |                |                | lesion         |
   |                |                |                | (finding)".    |
   |                |                |                |                |
   |                |                |                | Retired code   |
   |                |                |                | is inactive in |
   |                |                |                | SNOMED CT      |
   |                |                |                | (Duplicate).   |
   +----------------+----------------+----------------+----------------+
   | P5-09100       | Magnetic       | `2416          | Replacement    |
   |                | resonance      | 63008 <http:// | code has       |
   |                | angiography    | snomed.info/id | meaning of     |
   |                |                | /241663008>`__ | "Magnetic      |
   |                |                |                | resonance      |
   |                |                |                | imaging of     |
   |                |                |                | vessels        |
   |                |                |                | (procedure)".  |
   |                |                |                |                |
   |                |                |                | Retired code   |
   |                |                |                | is inactive in |
   |                |                |                | SNOMED CT      |
   |                |                |                | (Duplicate).   |
   +----------------+----------------+----------------+----------------+
   | F-6166C        | Marijuana      | `3987          | Replacement    |
   |                | derivative     | 05004 <http:// | code has       |
   |                |                | snomed.info/id | meaning of     |
   |                |                | /398705004>`__ | "Cannabis      |
   |                |                |                | (substance)".  |
   |                |                |                |                |
   |                |                |                | Retired code   |
   |                |                |                | is inactive in |
   |                |                |                | SNOMED CT      |
   |                |                |                | (Ambiguous).   |
   +----------------+----------------+----------------+----------------+
   | F-6175A        | N-a            | `1153          | Replacement    |
   |                | cetylaspartate | 91007 <http:// | code has       |
   |                |                | snomed.info/id | meaning of     |
   |                |                | /115391007>`__ | "N-acet        |
   |                |                |                | yl-L-aspartate |
   |                |                |                | (substance)".  |
   |                |                |                |                |
   |                |                |                | Retired code   |
   |                |                |                | is inactive in |
   |                |                |                | SNOMED CT      |
   |                |                |                | (Duplicate).   |
   +----------------+----------------+----------------+----------------+
   | F-52760        | Nausea         | `4225          | Replacement    |
   |                |                | 87007 <http:// | code has       |
   |                |                | snomed.info/id | meaning of     |
   |                |                | /422587007>`__ | "Nausea        |
   |                |                |                | (finding)".    |
   |                |                |                |                |
   |                |                |                | Retired code   |
   |                |                |                | is inactive in |
   |                |                |                | SNOMED CT      |
   |                |                |                | (Erroneous).   |
   +----------------+----------------+----------------+----------------+
   | P5-D10F8       | Nuclear        | `68            | Replacement    |
   |                | medicine       | 796002 <http:/ | code has       |
   |                | diagnostic     | /snomed.info/i | meaning of     |
   |                | procedure on   | d/68796002>`__ | "Radioisotope  |
   |                | m              |                | study of       |
   |                | usculoskeletal |                | m              |
   |                | system         |                | usculoskeletal |
   |                |                |                | system         |
   |                |                |                | (procedure)".  |
   |                |                |                |                |
   |                |                |                | Retired code   |
   |                |                |                | is inactive in |
   |                |                |                | SNOMED CT      |
   |                |                |                | (Duplicate).   |
   +----------------+----------------+----------------+----------------+
   | T-3215A        | Ostium         | `2641          | Replacement    |
   |                |                | 14003 <http:// | code has       |
   |                |                | snomed.info/id | meaning of     |
   |                |                | /264114003>`__ | "Ostium        |
   |                |                |                | (qualifier     |
   |                |                |                | value)".       |
   |                |                |                |                |
   |                |                |                | Retired code   |
   |                |                |                | is inactive in |
   |                |                |                | SNOMED CT      |
   |                |                |                | (Ambiguous).   |
   +----------------+----------------+----------------+----------------+
   | R-00305        | Heart Valve    |                | No             |
   |                | Flail          |                | replacement.   |
   |                |                |                |                |
   |                |                |                | Retired code   |
   |                |                |                | means          |
   |                |                |                | something      |
   |                |                |                | completely     |
   |                |                |                | different,     |
   |                |                |                | "Other         |
   |                |                |                | surgical       |
   |                |                |                | margin site    |
   |                |                |                | involved by    |
   |                |                |                | malignant      |
   |                |                |                | neoplasm       |
   |                |                |                | (observable    |
   |                |                |                | entity)" and   |
   |                |                |                | is inactive in |
   |                |                |                | SNOMED CT      |
   |                |                |                | (Ambiguous).   |
   +----------------+----------------+----------------+----------------+
   | R-0039E        | Patient has    | `4415          | Replacement    |
   |                | pacemaker      | 09002 <http:// | code has       |
   |                |                | snomed.info/id | meaning of     |
   |                |                | /441509002>`__ | "Cardiac       |
   |                |                |                | pacemaker in   |
   |                |                |                | situ           |
   |                |                |                | (finding)".    |
   |                |                |                |                |
   |                |                |                | Retired code   |
   |                |                |                | is inactive in |
   |                |                |                | SNOMED CT      |
   |                |                |                | (Duplicate).   |
   +----------------+----------------+----------------+----------------+
   | T-D2236        | Pectoral       | `26            | Replacement    |
   |                | girdle         | 444007 <http:/ | code has       |
   |                |                | /snomed.info/i | meaning of     |
   |                |                | d/26444007>`__ | "Shoulder      |
   |                |                |                | girdle         |
   |                |                |                | structure      |
   |                |                |                | (body          |
   |                |                |                | structure)".   |
   |                |                |                |                |
   |                |                |                | Retired code   |
   |                |                |                | is inactive in |
   |                |                |                | SNOMED CT      |
   |                |                |                | (Duplicate).   |
   +----------------+----------------+----------------+----------------+
   | R-305E9        | Pediatric      | `3099          | Replacement    |
   |                | Surgery        | 91001 <http:// | code has       |
   |                |                | snomed.info/id | meaning of     |
   |                |                | /309991001>`__ | "Pediatric     |
   |                |                |                | surgical       |
   |                |                |                | department     |
   |                |                |                | (              |
   |                |                |                | environment)". |
   |                |                |                |                |
   |                |                |                | Retired code   |
   |                |                |                | is inactive in |
   |                |                |                | SNOMED CT      |
   |                |                |                | (Duplicate).   |
   +----------------+----------------+----------------+----------------+
   | P5-39050       | Percutaneous   | `2409          | Replacement    |
   |                | retrieval of   | 46003 <http:// | code has       |
   |                | intravascular  | snomed.info/id | meaning of     |
   |                | foreign body   | /240946003>`__ | "Percutaneous  |
   |                |                |                | removal of     |
   |                |                |                | endovascular   |
   |                |                |                | foreign body   |
   |                |                |                | (procedure)".  |
   |                |                |                |                |
   |                |                |                | Retired code   |
   |                |                |                | is inactive in |
   |                |                |                | SNOMED CT      |
   |                |                |                | (Duplicate).   |
   +----------------+----------------+----------------+----------------+
   | L-809E9        | Perro de       | `1325          | Replacement    |
   |                | Pressa Canario | 76008 <http:// | code has       |
   |                | dog breed      | snomed.info/id | meaning of     |
   |                |                | /132576008>`__ | "Presa Canario |
   |                |                |                | dog breed      |
   |                |                |                | (organism)".   |
   |                |                |                |                |
   |                |                |                | Retired code   |
   |                |                |                | is inactive in |
   |                |                |                | SNOMED CT      |
   |                |                |                | (Duplicate).   |
   +----------------+----------------+----------------+----------------+
   | L-80A96        | Pixiebob cat   | `4172          | Replacement    |
   |                | breed          | 77001 <http:// | code has       |
   |                |                | snomed.info/id | meaning of     |
   |                |                | /417277001>`__ | "Pixie-bob cat |
   |                |                |                | breed          |
   |                |                |                | (organism)".   |
   |                |                |                |                |
   |                |                |                | Retired code   |
   |                |                |                | is inactive in |
   |                |                |                | SNOMED CT      |
   |                |                |                | (Duplicate).   |
   +----------------+----------------+----------------+----------------+
   | T-A2790        | posterior      | `2793          | Replacement    |
   |                | commissure     | 36005 <http:// | code has       |
   |                |                | snomed.info/id | meaning of     |
   |                |                | /279336005>`__ | "Posterior     |
   |                |                |                | cerebral       |
   |                |                |                | commissure     |
   |                |                |                | (body          |
   |                |                |                | structure)".   |
   |                |                |                |                |
   |                |                |                | Retired code   |
   |                |                |                | is inactive in |
   |                |                |                | SNOMED CT      |
   |                |                |                | (Duplicate).   |
   +----------------+----------------+----------------+----------------+
   | R-10214        | po             | `2724          | Replacement    |
   |                | stero-anterior | 79007 <http:// | code has       |
   |                |                | snomed.info/id | meaning of     |
   |                |                | /272479007>`__ | "P             |
   |                |                |                | osteroanterior |
   |                |                |                | projection     |
   |                |                |                | (qualifier     |
   |                |                |                | value)".       |
   |                |                |                |                |
   |                |                |                | Retired code   |
   |                |                |                | is inactive in |
   |                |                |                | SNOMED CT      |
   |                |                |                | (Duplicate).   |
   +----------------+----------------+----------------+----------------+
   | P0-02180       | Prophylactic   | `3602          | Replacement    |
   |                | intent         | 71000 <http:// | code has       |
   |                |                | snomed.info/id | meaning of     |
   |                |                | /360271000>`__ | "Prophylaxis - |
   |                |                |                | procedure      |
   |                |                |                | intent         |
   |                |                |                | (qualifier     |
   |                |                |                | value)".       |
   |                |                |                |                |
   |                |                |                | Retired code   |
   |                |                |                | is inactive in |
   |                |                |                | SNOMED CT      |
   |                |                |                | (Duplicate).   |
   +----------------+----------------+----------------+----------------+
   | C-B0310        | Radiopaque     | `              | Replacement    |
   |                | medium         | 7140000 <http: | code has       |
   |                |                | //snomed.info/ | meaning of     |
   |                |                | id/7140000>`__ | "Radiographic  |
   |                |                |                | contrast media |
   |                |                |                | (product)".    |
   |                |                |                |                |
   |                |                |                | Retired code   |
   |                |                |                | is inactive in |
   |                |                |                | SNOMED CT      |
   |                |                |                | (Duplicate).   |
   +----------------+----------------+----------------+----------------+
   | F-043E7        | Respiration    | `86            | Replacement    |
   |                | rate           | 290005 <http:/ | code has       |
   |                |                | /snomed.info/i | meaning of     |
   |                |                | d/86290005>`__ | "Respiratory   |
   |                |                |                | rate           |
   |                |                |                | (observable    |
   |                |                |                | entity)".      |
   |                |                |                |                |
   |                |                |                | Retired code   |
   |                |                |                | is inactive in |
   |                |                |                | SNOMED CT      |
   |                |                |                | (Duplicate).   |
   +----------------+----------------+----------------+----------------+
   | C-22931        | safranine O    | `4069          | Replacement    |
   |                | stain          | 88004 <http:// | code has       |
   |                |                | snomed.info/id | meaning of     |
   |                |                | /406988004>`__ | "Safranin      |
   |                |                |                | stain          |
   |                |                |                | (substance)".  |
   |                |                |                |                |
   |                |                |                | Retired code   |
   |                |                |                | is inactive in |
   |                |                |                | SNOMED CT      |
   |                |                |                | (Duplicate).   |
   +----------------+----------------+----------------+----------------+
   | R-00374        | Single vessel  | `1948          | Replacement    |
   |                | coronary       | 42008 <http:// | code has       |
   |                | artery         | snomed.info/id | meaning of     |
   |                | disease.       | /194842008>`__ | "Single        |
   |                |                |                | coronary       |
   |                |                |                | vessel disease |
   |                |                |                | (disorder)".   |
   |                |                |                |                |
   |                |                |                | Retired code   |
   |                |                |                | is inactive in |
   |                |                |                | SNOMED CT      |
   |                |                |                | (Duplicate).   |
   +----------------+----------------+----------------+----------------+
   | C-B0349        | Sodium         | `1092          | Replacement    |
   |                | tyropanate     | 12003 <http:// | code has       |
   |                |                | snomed.info/id | meaning of     |
   |                |                | /109212003>`__ | "Tyropanoate   |
   |                |                |                | sodium         |
   |                |                |                | (substance)".  |
   |                |                |                |                |
   |                |                |                | Retired code   |
   |                |                |                | is inactive in |
   |                |                |                | SNOMED CT      |
   |                |                |                | (Duplicate).   |
   +----------------+----------------+----------------+----------------+
   | T-C4239        | anterior       | `1685          | Replacement    |
   |                | jugular lymph  | 57005 <http:// | code has       |
   |                | node           | snomed.info/id | meaning of     |
   |                |                | /168557005>`__ | "Structure of  |
   |                |                |                | superficial    |
   |                |                |                | anterior       |
   |                |                |                | cervical lymph |
   |                |                |                | node (body     |
   |                |                |                | structure)".   |
   |                |                |                |                |
   |                |                |                | Retired code   |
   |                |                |                | is inactive in |
   |                |                |                | SNOMED CT      |
   |                |                |                | (Duplicate).   |
   +----------------+----------------+----------------+----------------+
   | T-53131        | base of tongue | `47            | Replacement    |
   |                |                | 975008 <http:/ | code has       |
   |                |                | /snomed.info/i | meaning of     |
   |                |                | d/47975008>`__ | "Structure of  |
   |                |                |                | root of tongue |
   |                |                |                | (body          |
   |                |                |                | structure)".   |
   |                |                |                |                |
   |                |                |                | Retired code   |
   |                |                |                | is inactive in |
   |                |                |                | SNOMED CT      |
   |                |                |                | (Duplicate).   |
   +----------------+----------------+----------------+----------------+
   | T-D1212        | Hypoglossal    | `1708          | Replacement    |
   |                |                | 87008 <http:// | code has       |
   |                |                | snomed.info/id | meaning of     |
   |                |                | /170887008>`__ | "Submental     |
   |                |                |                | triangle       |
   |                |                |                | structure      |
   |                |                |                | (body          |
   |                |                |                | structure)".   |
   |                |                |                |                |
   |                |                |                | Retired code   |
   |                |                |                | is inactive in |
   |                |                |                | SNOMED CT      |
   |                |                |                | (Ambiguous).   |
   +----------------+----------------+----------------+----------------+
   | A-13510        | Suture         | `27            | Replacement    |
   |                | material       | 065002 <http:/ | code has       |
   |                |                | /snomed.info/i | meaning of     |
   |                |                | d/27065002>`__ | "Surgical      |
   |                |                |                | suture, device |
   |                |                |                | (physical      |
   |                |                |                | object)".      |
   |                |                |                |                |
   |                |                |                | Retired code   |
   |                |                |                | is inactive in |
   |                |                |                | SNOMED CT      |
   |                |                |                | (Duplicate).   |
   +----------------+----------------+----------------+----------------+
   | F-03E7E        | Systemic       | `3865          | Replacement    |
   |                | Vascular       | 30009 <http:// | code has       |
   |                | Resistance     | snomed.info/id | meaning of     |
   |                |                | /386530009>`__ | "Systemic      |
   |                |                |                | vascular       |
   |                |                |                | resistance     |
   |                |                |                | (observable    |
   |                |                |                | entity)".      |
   |                |                |                |                |
   |                |                |                | Retired code   |
   |                |                |                | is inactive in |
   |                |                |                | SNOMED CT      |
   |                |                |                | (Erroneous).   |
   +----------------+----------------+----------------+----------------+
   | C-2285A        | tartrate       | `2557          | Replacement    |
   |                | resistant acid | 92001 <http:// | code has       |
   |                | phosphatase    | snomed.info/id | meaning of     |
   |                |                | /255792001>`__ | "Acid          |
   |                |                |                | phosphatase    |
   |                |                |                | stain          |
   |                |                |                | (substance)".  |
   |                |                |                |                |
   |                |                |                | Retired code   |
   |                |                |                | was being      |
   |                |                |                | misused as a   |
   |                |                |                | stain but was  |
   |                |                |                | a substance,   |
   |                |                |                | and is also    |
   |                |                |                | inactive in    |
   |                |                |                | SNOMED CT      |
   |                |                |                | (Duplicate).   |
   +----------------+----------------+----------------+----------------+
   | C-B1212        | Technetium     | `96            | Replacement    |
   |                | Tc^99m^        | 390006 <http:/ | code has       |
   |                | medronate      | /snomed.info/i | meaning of     |
   |                |                | d/96390006>`__ | "Technetium    |
   |                |                |                | Tc^99m^        |
   |                |                |                | medronate      |
   |                |                |                | (substance)".  |
   |                |                |                |                |
   |                |                |                | Retired code   |
   |                |                |                | is inactive in |
   |                |                |                | SNOMED CT      |
   |                |                |                | (Erroneous).   |
   +----------------+----------------+----------------+----------------+
   | C-B1214        | Technetium     | `4302          | Replacement    |
   |                | Tc^99m^        | 76001 <http:// | code has       |
   |                | pentetate      | snomed.info/id | meaning of     |
   |                |                | /430276001>`__ | "Technetium    |
   |                |                |                | Tc^99m^        |
   |                |                |                | pentetate      |
   |                |                |                | (substance)".  |
   |                |                |                |                |
   |                |                |                | Retired code   |
   |                |                |                | is inactive in |
   |                |                |                | SNOMED CT      |
   |                |                |                | (Ambiguous).   |
   +----------------+----------------+----------------+----------------+
   | C-A7400        | Thrombolytic   | `3039          | Replacement    |
   |                | agent          | 60004 <http:// | code has       |
   |                |                | snomed.info/id | meaning of     |
   |                |                | /303960004>`__ | "Thrombolytic  |
   |                |                |                | (product)".    |
   |                |                |                |                |
   |                |                |                | Retired code   |
   |                |                |                | is inactive in |
   |                |                |                | SNOMED CT      |
   |                |                |                | (Duplicate).   |
   +----------------+----------------+----------------+----------------+
   | C-A7042        | Thromboplastin | `65            | Replacement    |
   |                | preparation    | 265006 <http:/ | code has       |
   |                |                | /snomed.info/i | meaning of     |
   |                |                | d/65265006>`__ | "              |
   |                |                |                | Thromboplastin |
   |                |                |                | (product)".    |
   |                |                |                |                |
   |                |                |                | Retired code   |
   |                |                |                | is inactive in |
   |                |                |                | SNOMED CT      |
   |                |                |                | (Duplicate).   |
   +----------------+----------------+----------------+----------------+
   | G-A1A9         | Trans-hepatic  | `1033          | Replacement    |
   |                |                | 81007 <http:// | code has       |
   |                |                | snomed.info/id | meaning of     |
   |                |                | /103381007>`__ | "Transhepatic  |
   |                |                |                | approach       |
   |                |                |                | (qualifier     |
   |                |                |                | value)".       |
   |                |                |                |                |
   |                |                |                | Retired code   |
   |                |                |                | is inactive in |
   |                |                |                | SNOMED CT      |
   |                |                |                | (Retired       |
   |                |                |                | without stated |
   |                |                |                | reason).       |
   +----------------+----------------+----------------+----------------+
   | G-A1A8         | Trans-orbital  | `1292          | Replacement    |
   |                |                | 26004 <http:// | code has       |
   |                |                | snomed.info/id | meaning of     |
   |                |                | /129226004>`__ | "Transorbital  |
   |                |                |                | approach       |
   |                |                |                | (qualifier     |
   |                |                |                | value)".       |
   |                |                |                |                |
   |                |                |                | Retired code   |
   |                |                |                | is inactive in |
   |                |                |                | SNOMED CT      |
   |                |                |                | (Retired       |
   |                |                |                | without stated |
   |                |                |                | reason).       |
   +----------------+----------------+----------------+----------------+
   | R-00386        | Triple vessel  | `2338          | Replacement    |
   |                | coronary       | 17007 <http:// | code has       |
   |                | artery         | snomed.info/id | meaning of     |
   |                | disease.       | /233817007>`__ | "Triple vessel |
   |                |                |                | disease of the |
   |                |                |                | heart          |
   |                |                |                | (disorder)".   |
   |                |                |                |                |
   |                |                |                | Retired code   |
   |                |                |                | is inactive in |
   |                |                |                | SNOMED CT      |
   |                |                |                | (Duplicate).   |
   +----------------+----------------+----------------+----------------+
   | T-40210        | Media          | `61            | Replacement    |
   |                |                | 695000 <http:/ | code has       |
   |                |                | /snomed.info/i | meaning of     |
   |                |                | d/61695000>`__ | "Tunica media  |
   |                |                |                | vasorum (body  |
   |                |                |                | structure)".   |
   |                |                |                |                |
   |                |                |                | Retired code   |
   |                |                |                | is inactive in |
   |                |                |                | SNOMED CT      |
   |                |                |                | (Duplicate).   |
   +----------------+----------------+----------------+----------------+
   | P5-B0099       | Ultrasound     | `16            | Replacement    |
   |                | procedure      | 310003 <http:/ | code has       |
   |                |                | /snomed.info/i | meaning of     |
   |                |                | d/16310003>`__ | "Diagnostic    |
   |                |                |                | u              |
   |                |                |                | ltrasonography |
   |                |                |                | (procedure)".  |
   |                |                |                |                |
   |                |                |                | Retired code   |
   |                |                |                | is inactive in |
   |                |                |                | SNOMED CT      |
   |                |                |                | (Retired       |
   |                |                |                | without stated |
   |                |                |                | reason).       |
   +----------------+----------------+----------------+----------------+
   | T-4806E        | Vein           | `29            | Replacement    |
   |                |                | 092000 <http:/ | code has       |
   |                |                | /snomed.info/i | meaning of     |
   |                |                | d/29092000>`__ | "Venous        |
   |                |                |                | structure      |
   |                |                |                | (body          |
   |                |                |                | structure)".   |
   |                |                |                |                |
   |                |                |                | Retired code   |
   |                |                |                | is inactive in |
   |                |                |                | SNOMED CT      |
   |                |                |                | (Limited).     |
   +----------------+----------------+----------------+----------------+
   | P2-2200A       | Ventilatory    | `2431          | Replacement    |
   |                | assistance     | 47009 <http:// | code has       |
   |                |                | snomed.info/id | meaning of     |
   |                |                | /243147009>`__ | "Controlled    |
   |                |                |                | ventilation    |
   |                |                |                | (procedure)".  |
   |                |                |                |                |
   |                |                |                | Retired code   |
   |                |                |                | is inactive in |
   |                |                |                | SNOMED CT      |
   |                |                |                | (Duplicate).   |
   +----------------+----------------+----------------+----------------+
   | D4-31022       | Left ventricle |                | No             |
   |                | outflow        |                | replacement.   |
   |                | chamber        |                |                |
   |                |                |                | Retired code   |
   |                |                |                | is inactive in |
   |                |                |                | SNOMED CT      |
   |                |                |                | (Ambiguous).   |
   +----------------+----------------+----------------+----------------+
   | D4-31032       | Right          |                | No             |
   |                | ventricle      |                | replacement.   |
   |                | outflow        |                |                |
   |                | chamber        |                | Retired code   |
   |                |                |                | is inactive in |
   |                |                |                | SNOMED CT      |
   |                |                |                | (Ambiguous).   |
   +----------------+----------------+----------------+----------------+
   | `F             | Voiding        |                | No SNOMED      |
   | -72230 <http:/ |                |                | replacement.   |
   | /snomed.info/i |                |                | Replaced by    |
   | d/28278009>`__ |                |                | `(109137, DCM, |
   |                |                |                | "During        |
   |                |                |                | voiding") <#   |
   |                |                |                | DCM_109137>`__ |
   |                |                |                |                |
   |                |                |                | Retired code   |
   |                |                |                | is inactive in |
   |                |                |                | SNOMED CT.     |
   +----------------+----------------+----------------+----------------+
   | `D8-           | Infant of      |                | No SNOMED      |
   | 60001 <http:// | Gestational    |                | replacement.   |
   | snomed.info/id | Diabetic       |                | Replaced by    |
   | /276556006>`__ | Mother (IGDM)  |                | `(C0456029,    |
   |                |                |                | UMLS, "Infant  |
   |                |                |                | of mother with |
   |                |                |                | gestational    |
   |                |                |                | diabetes") <ht |
   |                |                |                | tp://uts.nlm.n |
   |                |                |                | ih.gov/metathe |
   |                |                |                | saurus.html?cu |
   |                |                |                | i=C0456029>`__ |
   |                |                |                |                |
   |                |                |                | Retired code   |
   |                |                |                | is inactive in |
   |                |                |                | SNOMED CT.     |
   +----------------+----------------+----------------+----------------+
   | L-8BA68        | Mere cattle    |                | No             |
   |                | breed          |                | replacement.   |
   |                |                |                |                |
   |                |                |                | (133492008,    |
   |                |                |                | SCT, "Lobi     |
   |                |                |                | cattle breed") |
   |                |                |                | remains in     |
   |                |                |                | use.           |
   |                |                |                |                |
   |                |                |                | Potential      |
   |                |                |                | replacement    |
   |                |                |                | L-8BB55 is     |
   |                |                |                | inactive in    |
   |                |                |                | SNOMED CT      |
   |                |                |                | (Ambiguous).   |
   +----------------+----------------+----------------+----------------+
   | G-A385         | Normality      | `3719          | Replacement    |
   |                | Undetermined   | 34000 <http:// | code has       |
   |                |                | snomed.info/id | meaning of     |
   |                |                | /371934000>`__ | "Normality     |
   |                |                |                | undetermined   |
   |                |                |                | (qualifier     |
   |                |                |                | value)".       |
   |                |                |                |                |
   |                |                |                | (82334004,     |
   |                |                |                | SCT,           |
   |                |                |                | "I             |
   |                |                |                | ndeterminate") |
   |                |                |                | remains in     |
   |                |                |                | use.           |
   +----------------+----------------+----------------+----------------+
   | G-7292         | On admission   | `2783          | Replacement    |
   |                |                | 07001 <http:// | code has       |
   |                |                | snomed.info/id | meaning of "On |
   |                |                | /278307001>`__ | admission      |
   |                |                |                | (qualifier     |
   |                |                |                | value)".       |
   |                |                |                |                |
   |                |                |                | (128954007,    |
   |                |                |                | SCT,           |
   |                |                |                | "Procedure     |
   |                |                |                | phase")        |
   |                |                |                | remains in     |
   |                |                |                | use.           |
   +----------------+----------------+----------------+----------------+
   | C-22848        | bismark brown  | `44            | Replacement    |
   |                | R stain        | 488008 <http:/ | code has       |
   |                |                | /snomed.info/i | meaning of     |
   |                |                | d/44488008>`__ | "Bismark brown |
   |                |                |                | R stain        |
   |                |                |                | (substance)".  |
   |                |                |                |                |
   |                |                |                | (85190005,     |
   |                |                |                | SCT, "bismark  |
   |                |                |                | brown Y        |
   |                |                |                | stain")        |
   |                |                |                | remains in     |
   |                |                |                | use.           |
   +----------------+----------------+----------------+----------------+
   | R-10042        | Arrythmia      | `6982          | Retired code   |
   |                | Evaluation     | 47007 <http:// | actually has   |
   |                |                | snomed.info/id | meaning in     |
   |                |                | /698247007>`__ | SNOMED CT of   |
   |                |                |                | "Device        |
   |                |                |                | crossed septum |
   |                |                |                | (finding)".    |
   |                |                |                |                |
   |                |                |                | Replacement    |
   |                |                |                | code has       |
   |                |                |                | meaning of     |
   |                |                |                | "Arrythmia".   |
   +----------------+----------------+----------------+----------------+
   | T-48440        | Anterior       | `1949          | Replacement    |
   |                | cardiac vein   | 96006 <http:// | code has       |
   |                |                | snomed.info/id | meaning of     |
   |                |                | /194996006>`__ | "Structure of  |
   |                |                |                | anterior       |
   |                |                |                | cardiac vein   |
   |                |                |                | (body          |
   |                |                |                | structure)".   |
   +----------------+----------------+----------------+----------------+
   | T-1531B        | Atlantal-axial | `62            | Replacement    |
   |                | joint          | 555009 <http:/ | code has       |
   |                |                | /snomed.info/i | meaning of     |
   |                |                | d/62555009>`__ | "Structure of  |
   |                |                |                | atlantoaxial   |
   |                |                |                | joint (body    |
   |                |                |                | structure)".   |
   +----------------+----------------+----------------+----------------+
   | T-40501        | Blood Vessel   | `2812          | Replacement    |
   |                | of Head        | 31009 <http:// | code has       |
   |                |                | snomed.info/id | meaning of     |
   |                |                | /281231009>`__ | "Vascular      |
   |                |                |                | structure of   |
   |                |                |                | head (body     |
   |                |                |                | structure)".   |
   +----------------+----------------+----------------+----------------+
   | T-A6041        | Cerebellar     | `25            | Replacement    |
   |                | Cortex         | 991003 <http:/ | code has       |
   |                |                | /snomed.info/i | meaning of     |
   |                |                | d/25991003>`__ | "Cerebellar    |
   |                |                |                | cortex         |
   |                |                |                | structure      |
   |                |                |                | (body          |
   |                |                |                | structure)".   |
   +----------------+----------------+----------------+----------------+
   | T-45526        | Circle of      | `11            | Replacement    |
   |                | Willis         | 279006 <http:/ | code has       |
   |                |                | /snomed.info/i | meaning of     |
   |                |                | d/11279006>`__ | "Structure of  |
   |                |                |                | circle of      |
   |                |                |                | Willis (body   |
   |                |                |                | structure)".   |
   +----------------+----------------+----------------+----------------+
   | T-11B02        | Coccygeal      | `18            | Replacement    |
   |                | vertrebrae     | 149002 <http:/ | code has       |
   |                |                | /snomed.info/i | meaning of     |
   |                |                | d/18149002>`__ | "Coccygeal     |
   |                |                |                | vertebra       |
   |                |                |                | structure      |
   |                |                |                | (body          |
   |                |                |                | structure)".   |
   +----------------+----------------+----------------+----------------+
   | T-D1403        | Cranial Cavity | `              | Replacement    |
   |                |                | 1101003 <http: | code has       |
   |                |                | //snomed.info/ | meaning of     |
   |                |                | id/1101003>`__ | "Cranial       |
   |                |                |                | cavity         |
   |                |                |                | structure      |
   |                |                |                | (body          |
   |                |                |                | structure)".   |
   +----------------+----------------+----------------+----------------+
   | T-A0193        | Cranial venous | `1283          | Replacement    |
   |                | system         | 20002 <http:// | code has       |
   |                |                | snomed.info/id | meaning of     |
   |                |                | /128320002>`__ | "Structure of  |
   |                |                |                | intracranial   |
   |                |                |                | vein (body     |
   |                |                |                | structure)".   |
   +----------------+----------------+----------------+----------------+
   | T-110A2        | Distal phalanx |                | No replacement |
   |                |                |                | in SNOMED.     |
   |                |                |                |                |
   |                |                |                | An alternative |
   |                |                |                | concept        |
   |                |                |                | (C3669027,     |
   |                |                |                | UMLS, "Bone    |
   |                |                |                | structure of   |
   |                |                |                | distal         |
   |                |                |                | phalanx)"      |
   |                |                |                | exists.        |
   +----------------+----------------+----------------+----------------+
   | T-47741        | Dorsalis Pedis | `86            | Replacement    |
   |                | Artery         | 547008 <http:/ | code has       |
   |                |                | /snomed.info/i | meaning of     |
   |                |                | d/86547008>`__ | "Structure of  |
   |                |                |                | dorsalis pedis |
   |                |                |                | artery (body   |
   |                |                |                | structure)".   |
   +----------------+----------------+----------------+----------------+
   | T-F6806        | Ductus venosus | `3676          | Replacement    |
   |                |                | 24001 <http:// | code has       |
   |                |                | snomed.info/id | meaning of     |
   |                |                | /367624001>`__ | "Structure of  |
   |                |                |                | ductus venosus |
   |                |                |                | (body          |
   |                |                |                | structure)".   |
   +----------------+----------------+----------------+----------------+
   | T-AB000        | Ear            | `1175          | Replacement    |
   |                |                | 90005 <http:// | code has       |
   |                |                | snomed.info/id | meaning of     |
   |                |                | /117590005>`__ | "Ear structure |
   |                |                |                | (body          |
   |                |                |                | structure)".   |
   +----------------+----------------+----------------+----------------+
   | T-AA215        | Entire Cornea  | `28            | Replacement    |
   |                |                | 726007 <http:/ | code has       |
   |                |                | /snomed.info/i | meaning of     |
   |                |                | d/28726007>`__ | "Corneal       |
   |                |                |                | structure      |
   |                |                |                | (body          |
   |                |                |                | structure)".   |
   +----------------+----------------+----------------+----------------+
   | T-1416B        | External       | `53            | Replacement    |
   |                | intercostal    | 967007 <http:/ | code has       |
   |                | muscle         | /snomed.info/i | meaning of     |
   |                |                | d/53967007>`__ | "Structure of  |
   |                |                |                | external       |
   |                |                |                | intercostal    |
   |                |                |                | muscle (body   |
   |                |                |                | structure)".   |
   +----------------+----------------+----------------+----------------+
   | T-1553D        | Finger Joint   | `1256          | Replacement    |
   |                |                | 82004 <http:// | code has       |
   |                |                | snomed.info/id | meaning of     |
   |                |                | /125682004>`__ | "Finger joint  |
   |                |                |                | structure      |
   |                |                |                | (body          |
   |                |                |                | structure)".   |
   +----------------+----------------+----------------+----------------+
   | T-48470        | Inferior       | `1954          | Replacement    |
   |                | cardiac vein   | 16006 <http:// | code has       |
   |                |                | snomed.info/id | meaning of     |
   |                |                | /195416006>`__ | "Structure of  |
   |                |                |                | posterior vein |
   |                |                |                | of left        |
   |                |                |                | ventricle      |
   |                |                |                | (body          |
   |                |                |                | structure)".   |
   +----------------+----------------+----------------+----------------+
   | T-A1721        | Inferior Horn  | `53            | Replacement    |
   |                | of Lateral     | 118009 <http:/ | code has       |
   |                | Ventricle      | /snomed.info/i | meaning of     |
   |                |                | d/53118009>`__ | "Structure of  |
   |                |                |                | inferior horn  |
   |                |                |                | of lateral     |
   |                |                |                | ventricle      |
   |                |                |                | (body          |
   |                |                |                | structure)".   |
   +----------------+----------------+----------------+----------------+
   | T-14183        | Internal       | `41            | Replacement    |
   |                | intercostal    | 313007 <http:/ | code has       |
   |                | muscle         | /snomed.info/i | meaning of     |
   |                |                | d/41313007>`__ | "Structure of  |
   |                |                |                | internal       |
   |                |                |                | intercostal    |
   |                |                |                | muscle (body   |
   |                |                |                | structure)".   |
   +----------------+----------------+----------------+----------------+
   | T-C4351        | Intra-mammary  | `4438          | Replacement    |
   |                | lymph node     | 08008 <http:// | code has       |
   |                |                | snomed.info/id | meaning of     |
   |                |                | /443808008>`__ | "Structure of  |
   |                |                |                | intramammary   |
   |                |                |                | lymph node     |
   |                |                |                | (body          |
   |                |                |                | structure)".   |
   |                |                |                |                |
   |                |                |                | Retired code   |
   |                |                |                | was used       |
   |                |                |                | incorrectly    |
   |                |                |                | and means      |
   |                |                |                | something else |
   |                |                |                | ("Entire       |
   |                |                |                | internal       |
   |                |                |                | mammary lymph  |
   |                |                |                | node (body     |
   |                |                |                | structure)").  |
   +----------------+----------------+----------------+----------------+
   | T-47651        | lateral        | `44            | Replacement    |
   |                | plantar artery | 830000 <http:/ | code has       |
   |                |                | /snomed.info/i | meaning of     |
   |                |                | d/44830000>`__ | "Structure of  |
   |                |                |                | lateral        |
   |                |                |                | plantar artery |
   |                |                |                | (body          |
   |                |                |                | structure)".   |
   +----------------+----------------+----------------+----------------+
   | T-4881F        | Left Main      | `70            | Replacement    |
   |                | Branch of      | 253006 <http:/ | code has       |
   |                | Portal Vein    | /snomed.info/i | meaning of     |
   |                |                | d/70253006>`__ | "Structure of  |
   |                |                |                | left main      |
   |                |                |                | branch of      |
   |                |                |                | portal vein    |
   |                |                |                | (body          |
   |                |                |                | structure)".   |
   +----------------+----------------+----------------+----------------+
   | T-62002        | Liver          | `10            | Replacement    |
   |                |                | 200004 <http:/ | code has       |
   |                |                | /snomed.info/i | meaning of     |
   |                |                | d/10200004>`__ | "Liver         |
   |                |                |                | structure      |
   |                |                |                | (body          |
   |                |                |                | structure)".   |
   +----------------+----------------+----------------+----------------+
   | T-47661        | medial plantar | `74            | Replacement    |
   |                | artery         | 156002 <http:/ | code has       |
   |                |                | /snomed.info/i | meaning of     |
   |                |                | d/74156002>`__ | "Structure of  |
   |                |                |                | medial plantar |
   |                |                |                | artery (body   |
   |                |                |                | structure)".   |
   +----------------+----------------+----------------+----------------+
   | T-1254D        | Metacarpus     | `36            | Replacement    |
   |                |                | 455000 <http:/ | code has       |
   |                |                | /snomed.info/i | meaning of     |
   |                |                | d/36455000>`__ | "Bone          |
   |                |                |                | structure of   |
   |                |                |                | metacarpal     |
   |                |                |                | (body          |
   |                |                |                | structure)".   |
   +----------------+----------------+----------------+----------------+
   | T-35313        | Mitral Annulus | `65            | Replacement    |
   |                |                | 197004 <http:/ | code has       |
   |                |                | /snomed.info/i | meaning of     |
   |                |                | d/65197004>`__ | "Structure of  |
   |                |                |                | anulus         |
   |                |                |                | fibrosus of    |
   |                |                |                | mitral orifice |
   |                |                |                | (body          |
   |                |                |                | structure)".   |
   +----------------+----------------+----------------+----------------+
   | T-51000        | Mouth          | `1238          | Replacement    |
   |                |                | 51003 <http:// | code has       |
   |                |                | snomed.info/id | meaning of     |
   |                |                | /123851003>`__ | "Mouth region  |
   |                |                |                | structure      |
   |                |                |                | (body          |
   |                |                |                | structure)".   |
   +----------------+----------------+----------------+----------------+
   | T-D0772        | Myocardial     | `2726          | Replacement    |
   |                | Wall           | 57006 <http:// | code has       |
   |                |                | snomed.info/id | meaning of     |
   |                |                | /272657006>`__ | "Cardiac wall  |
   |                |                |                | structure      |
   |                |                |                | (body          |
   |                |                |                | structure)".   |
   +----------------+----------------+----------------+----------------+
   | T-127EC        | Navicular of   | `75            | Replacement    |
   |                | hindfoot       | 772009 <http:/ | code has       |
   |                |                | /snomed.info/i | meaning of     |
   |                |                | d/75772009>`__ | "Bone          |
   |                |                |                | structure of   |
   |                |                |                | navicular      |
   |                |                |                | (body          |
   |                |                |                | structure)".   |
   +----------------+----------------+----------------+----------------+
   | T-42231        | Non-coronary   | `24            | Replacement    |
   |                | Sinus          | 865005 <http:/ | code has       |
   |                |                | /snomed.info/i | meaning of     |
   |                |                | d/24865005>`__ | "Structure of  |
   |                |                |                | posterior      |
   |                |                |                | sinus of       |
   |                |                |                | Valsalva (body |
   |                |                |                | structure)".   |
   +----------------+----------------+----------------+----------------+
   | T-D14AD        | Orbital region | `3636          | Replacement    |
   |                |                | 54007 <http:// | code has       |
   |                |                | snomed.info/id | meaning of     |
   |                |                | /363654007>`__ | "Structure of  |
   |                |                |                | orbit proper   |
   |                |                |                | (body          |
   |                |                |                | structure)".   |
   +----------------+----------------+----------------+----------------+
   | T-9200B        | Prostate       | `41            | Replacement    |
   |                |                | 216001 <http:/ | code has       |
   |                |                | /snomed.info/i | meaning of     |
   |                |                | d/41216001>`__ | "Prostatic     |
   |                |                |                | structure      |
   |                |                |                | (body          |
   |                |                |                | structure)".   |
   +----------------+----------------+----------------+----------------+
   | T-43203        | Right Coronary | `13            | Replacement    |
   |                | Artery         | 647002 <http:/ | code has       |
   |                |                | /snomed.info/i | meaning of     |
   |                |                | d/13647002>`__ | "Right         |
   |                |                |                | coronary       |
   |                |                |                | artery         |
   |                |                |                | structure      |
   |                |                |                | (body          |
   |                |                |                | structure)".   |
   +----------------+----------------+----------------+----------------+
   | T-4882A        | Right Main     | `73            | Replacement    |
   |                | Branch of      | 931004 <http:/ | code has       |
   |                | Portal Vein    | /snomed.info/i | meaning of     |
   |                |                | d/73931004>`__ | "Structure of  |
   |                |                |                | right main     |
   |                |                |                | branch of      |
   |                |                |                | portal vein    |
   |                |                |                | (body          |
   |                |                |                | structure)".   |
   +----------------+----------------+----------------+----------------+
   | T-00009        | Skin           | `39            | Replacement    |
   |                |                | 937001 <http:/ | code has       |
   |                |                | /snomed.info/i | meaning of     |
   |                |                | d/39937001>`__ | "Skin          |
   |                |                |                | structure      |
   |                |                |                | (body          |
   |                |                |                | structure)".   |
   +----------------+----------------+----------------+----------------+
   | T-141A5        | Transversus    | `88            | Replacement    |
   |                | thoracis       | 454005 <http:/ | code has       |
   |                |                | /snomed.info/i | meaning of     |
   |                |                | d/88454005>`__ | "Structure of  |
   |                |                |                | transverse     |
   |                |                |                | thoracis       |
   |                |                |                | muscle (body   |
   |                |                |                | structure)".   |
   +----------------+----------------+----------------+----------------+
   | T-35111        | Tricuspid      | >T-35110       | Replacement    |
   |                | Annulus        |                | code has       |
   |                |                |                | meaning of     |
   |                |                |                | "Structure of  |
   |                |                |                | anulus         |
   |                |                |                | fibrosus of    |
   |                |                |                | tricuspid      |
   |                |                |                | orifice (body  |
   |                |                |                | structure)".   |
   +----------------+----------------+----------------+----------------+
   | T-48817        | Umbilical Vein | `2846          | Replacement    |
   |                |                | 39000 <http:// | code has       |
   |                |                | snomed.info/id | meaning of     |
   |                |                | /284639000>`__ | "Structure of  |
   |                |                |                | umbilical      |
   |                |                |                | portion of     |
   |                |                |                | portal vein    |
   |                |                |                | (body          |
   |                |                |                | structure)".   |
   +----------------+----------------+----------------+----------------+
   | D3-81310       | Arterial       | `7108          | Replaced code  |
   |                | dissection     | 64009 <http:// | had meaning    |
   |                |                | snomed.info/id | "Dissecting    |
   |                |                | /710864009>`__ | aneurysm of    |
   |                |                |                | artery         |
   |                |                |                | (disorder)".   |
   |                |                |                |                |
   |                |                |                | Replacement    |
   |                |                |                | code has       |
   |                |                |                | meaning        |
   |                |                |                | "Dissection of |
   |                |                |                | artery         |
   |                |                |                | (disorder)".   |
   |                |                |                |                |
   |                |                |                | Retired code   |
   |                |                |                | is inactive in |
   |                |                |                | SNOMED CT.     |
   +----------------+----------------+----------------+----------------+
   | M-32270        | dissecting     | `7108          | Replaced code  |
   |                | aneurysm       | 64009 <http:// | had meaning    |
   |                |                | snomed.info/id | "Dissecting    |
   |                |                | /710864009>`__ | aneurysm       |
   |                |                |                | (morphologic   |
   |                |                |                | abnormality)". |
   |                |                |                |                |
   |                |                |                | Replacement    |
   |                |                |                | code has       |
   |                |                |                | meaning        |
   |                |                |                | "Dissection of |
   |                |                |                | artery         |
   |                |                |                | (disorder)".   |
   |                |                |                |                |
   |                |                |                | Retired code   |
   |                |                |                | is inactive in |
   |                |                |                | SNOMED CT.     |
   +----------------+----------------+----------------+----------------+
   | T-43126        | Left Posterior | `91            | Replaced code  |
   |                | Descending     | 760001 <http:/ | had meaning    |
   |                | Artery         | /snomed.info/i | "Structure of  |
   |                |                | d/91760001>`__ | left posterior |
   |                |                |                | descending     |
   |                |                |                | branch of      |
   |                |                |                | circumflex     |
   |                |                |                | branch of left |
   |                |                |                | coronary       |
   |                |                |                | artery (body   |
   |                |                |                | structure)".   |
   |                |                |                |                |
   |                |                |                | Replacement    |
   |                |                |                | code has       |
   |                |                |                | meaning "Left  |
   |                |                |                | posterior      |
   |                |                |                | descending     |
   |                |                |                | circumflex     |
   |                |                |                | coronary       |
   |                |                |                | artery (body   |
   |                |                |                | structure)".   |
   |                |                |                |                |
   |                |                |                | Retired code   |
   |                |                |                | is inactive in |
   |                |                |                | SNOMED CT.     |
   +----------------+----------------+----------------+----------------+
   | M-24614        | berry aneurysm | `54            | Replaced code  |
   |                |                | 002007 <http:/ | had meaning    |
   |                |                | /snomed.info/i | "Berry         |
   |                |                | d/54002007>`__ | aneurysm       |
   |                |                |                | (morphologic   |
   |                |                |                | abnormality)". |
   |                |                |                |                |
   |                |                |                | Replacement    |
   |                |                |                | code has       |
   |                |                |                | meaning        |
   |                |                |                | "Saccular      |
   |                |                |                | aneurysm       |
   |                |                |                | (morphologic   |
   |                |                |                | abnormality)". |
   |                |                |                |                |
   |                |                |                | Retired code   |
   |                |                |                | is inactive in |
   |                |                |                | SNOMED CT.     |
   +----------------+----------------+----------------+----------------+
   | D3-80017       | Inflammatory   | `3141          | Replaced code  |
   |                | aneurysm       | 86008 <http:// | had meaning    |
   |                |                | snomed.info/id | "Inflammatory  |
   |                |                | /314186008>`__ | aneurysm       |
   |                |                |                | (disorder)".   |
   |                |                |                |                |
   |                |                |                | Replacement    |
   |                |                |                | code has       |
   |                |                |                | meaning        |
   |                |                |                | "Inflammatory  |
   |                |                |                | abdominal      |
   |                |                |                | aortic         |
   |                |                |                | aneurysm       |
   |                |                |                | (disorder)".   |
   |                |                |                |                |
   |                |                |                | Retired code   |
   |                |                |                | is inactive in |
   |                |                |                | SNOMED CT.     |
   +----------------+----------------+----------------+----------------+
   | R-002DA        | Averaged       | `3730          | Replaced code  |
   |                |                | 98007 <http:// | had meaning    |
   |                |                | snomed.info/id | "Averaged -    |
   |                |                | /373098007>`__ | numeric        |
   |                |                |                | estimation     |
   |                |                |                | technique      |
   |                |                |                | (qualifier     |
   |                |                |                | value)".       |
   |                |                |                |                |
   |                |                |                | Replacement    |
   |                |                |                | code has       |
   |                |                |                | meaning "Mean  |
   |                |                |                | - numeric      |
   |                |                |                | estimation     |
   |                |                |                | technique      |
   |                |                |                | (qualifier     |
   |                |                |                | value)".       |
   |                |                |                |                |
   |                |                |                | Retired code   |
   |                |                |                | is inactive in |
   |                |                |                | SNOMED CT.     |
   +----------------+----------------+----------------+----------------+
   | R-101B7        | Medial         |                | Replaced code  |
   |                | Dissection     |                | had meaning    |
   |                |                |                | "Medial        |
   |                |                |                | dissecting     |
   |                |                |                | aneurysm       |
   |                |                |                | (morphologic   |
   |                |                |                | abnormality)". |
   |                |                |                |                |
   |                |                |                | No replacement |
   |                |                |                | SNOMED code    |
   |                |                |                | exists.        |
   |                |                |                |                |
   |                |                |                | `(122399, DCM, |
   |                |                |                | "Medial        |
   |                |                |                | D              |
   |                |                |                | issection") <# |
   |                |                |                | DCM_122399>`__ |
   |                |                |                | may be used    |
   |                |                |                | instead.       |
   |                |                |                |                |
   |                |                |                | Retired code   |
   |                |                |                | is inactive in |
   |                |                |                | SNOMED CT.     |
   +----------------+----------------+----------------+----------------+
   | R-101B8        | Intimal        |                | Replaced code  |
   |                | Dissection     |                | has meaning    |
   |                |                |                | "Exposure to   |
   |                |                |                | biological     |
   |                |                |                | agent via      |
   |                |                |                | direct         |
   |                |                |                | penetration of |
   |                |                |                | skin (event)". |
   |                |                |                |                |
   |                |                |                | No replacement |
   |                |                |                | SNOMED code    |
   |                |                |                | exists.        |
   |                |                |                |                |
   |                |                |                | `(122398, DCM, |
   |                |                |                | "Intimal       |
   |                |                |                | D              |
   |                |                |                | issection") <# |
   |                |                |                | DCM_122398>`__ |
   |                |                |                | may be used    |
   |                |                |                | instead.       |
   +----------------+----------------+----------------+----------------+
   | R-101B9        | Adventitial    |                | Replaced code  |
   |                | Dissection     |                | has meaning    |
   |                |                |                | "Inhalational  |
   |                |                |                | exposure to    |
   |                |                |                | biological     |
   |                |                |                | agent          |
   |                |                |                | (event)".      |
   |                |                |                |                |
   |                |                |                | No replacement |
   |                |                |                | SNOMED code    |
   |                |                |                | exists.        |
   |                |                |                |                |
   |                |                |                | `(122397, DCM, |
   |                |                |                | "Adventitial   |
   |                |                |                | D              |
   |                |                |                | issection") <# |
   |                |                |                | DCM_122397>`__ |
   |                |                |                | may be used    |
   |                |                |                | instead.       |
   +----------------+----------------+----------------+----------------+
   | `2536          | Pulmonary      | `1112          | Replacement    |
   | 39004 <http:// | arteriovenous  | 89009 <http:// | code has       |
   | snomed.info/id | fistula        | snomed.info/id | meaning        |
   | /253639004>`__ |                | /111289009>`__ | "Arteriovenous |
   |                |                |                | fistula of     |
   |                |                |                | pulmonary      |
   |                |                |                | vessels        |
   |                |                |                | (disorder)".   |
   |                |                |                |                |
   |                |                |                | Retired code   |
   |                |                |                | is inactive in |
   |                |                |                | SNOMED CT      |
   |                |                |                | (Duplicate).   |
   +----------------+----------------+----------------+----------------+
   | `86            | Female         | `45            | Replacement    |
   | 969008 <http:/ | external       | 292006 <http:/ | code has       |
   | /snomed.info/i | genitalia      | /snomed.info/i | meaning        |
   | d/86969008>`__ |                | d/45292006>`__ | "Vulva".       |
   |                |                |                |                |
   |                |                |                | Retired code   |
   |                |                |                | is inactive in |
   |                |                |                | SNOMED CT      |
   |                |                |                | (Duplicate).   |
   +----------------+----------------+----------------+----------------+
   | `2578          | Internal       | `1184          | Replacement    |
   | 37004 <http:// | fixation using | 70002 <http:// | code has       |
   | snomed.info/id | internal       | snomed.info/id | meaning        |
   | /257837004>`__ | fixator system | /118470002>`__ | "Internal      |
   |                |                |                | skeletal       |
   |                |                |                | fixation".     |
   |                |                |                |                |
   |                |                |                | Retired code   |
   |                |                |                | is inactive in |
   |                |                |                | SNOMED CT      |
   |                |                |                | (Duplicate).   |
   +----------------+----------------+----------------+----------------+
   | `3473          | Lactated       |                | No replacement |
   | 79006 <http:// | Ringer's       |                | SNOMED code    |
   | snomed.info/id |                |                | exists.        |
   | /347379006>`__ |                |                |                |
   |                |                |                | `(D000077325,  |
   |                |                |                | MSH, "Lactated |
   |                |                |                | Ringer's")     |
   |                |                |                | <http://biopor |
   |                |                |                | tal.bioontolog |
   |                |                |                | y.org/ontologi |
   |                |                |                | es/MESH?p=clas |
   |                |                |                | ses&conceptid= |
   |                |                |                | D000077325>`__ |
   |                |                |                | may be used    |
   |                |                |                | instead.       |
   |                |                |                |                |
   |                |                |                | Retired code   |
   |                |                |                | is inactive in |
   |                |                |                | SNOMED CT (Non |
   |                |                |                | conformance to |
   |                |                |                | editorial      |
   |                |                |                | policy).       |
   +----------------+----------------+----------------+----------------+
   | `2620          | Saline         | `3737          | Replacement    |
   | 03004 <http:// |                | 57009 <http:// | code has       |
   | snomed.info/id |                | snomed.info/id | meaning        |
   | /262003004>`__ |                | /373757009>`__ | "Sodium        |
   |                |                |                | chloride       |
   |                |                |                | solution       |
   |                |                |                | (substance)".  |
   |                |                |                |                |
   |                |                |                | Retired code   |
   |                |                |                | is inactive in |
   |                |                |                | SNOMED CT      |
   |                |                |                | (Outdated).    |
   +----------------+----------------+----------------+----------------+
   | `6998          | Skin of axilla | `76            | Replacement    |
   | 91005 <http:// |                | 261009 <http:/ | code has       |
   | snomed.info/id |                | /snomed.info/i | meaning "Skin  |
   | /699891005>`__ |                | d/76261009>`__ | structure of   |
   |                |                |                | axilla (body   |
   |                |                |                | structure)".   |
   |                |                |                |                |
   |                |                |                | Retired code   |
   |                |                |                | is inactive in |
   |                |                |                | SNOMED CT      |
   |                |                |                | (Ambiguous).   |
   +----------------+----------------+----------------+----------------+
   | `4437          | Pulmonary Vein |                | No replacement |
   | 14006 <http:// | Right Middle   |                | SNOMED code    |
   | snomed.info/id | Segment        |                | exists.        |
   | /443714006>`__ |                |                |                |
   |                |                |                | Retired code   |
   |                |                |                | is inactive in |
   |                |                |                | SNOMED CT      |
   |                |                |                | (Ambiguous).   |
   |                |                |                |                |
   |                |                |                | Retired code   |
   |                |                |                | had meaning    |
   |                |                |                | "Structure of  |
   |                |                |                | right middle   |
   |                |                |                | pulmonary      |
   |                |                |                | vein".         |
   +----------------+----------------+----------------+----------------+
   | `1198          | Breast         | `3023          | Replacement    |
   | 53006 <http:// | implantation   | 43007 <http:// | code has       |
   | snomed.info/id |                | snomed.info/id | meaning        |
   | /119853006>`__ |                | /302343007>`__ | "Insertion of  |
   |                |                |                | prosthesis for |
   |                |                |                | breast         |
   |                |                |                | (procedure)".  |
   |                |                |                |                |
   |                |                |                | Retired code   |
   |                |                |                | is inactive in |
   |                |                |                | SNOMED CT      |
   |                |                |                | (Duplicate).   |
   +----------------+----------------+----------------+----------------+

.. table:: SNOMED Synonyms Retired from DICOM Use

   +----------------+----------------+----------------+----------------+
   | Code Value     | Retired Code   | Replacement    | Notes          |
   |                | Meaning        | Code Meaning   |                |
   +================+================+================+================+
   | M-01000        | Lesion         | M              | Retired        |
   |                |                | orphologically | synonym has    |
   |                |                | Abnormal       | status of      |
   |                |                | Structure      | "              |
   |                |                |                | inappropriate" |
   |                |                |                | in SNOMED CT.  |
   |                |                |                |                |
   |                |                |                | A different    |
   |                |                |                | SNOMED CT      |
   |                |                |                | concept is     |
   |                |                |                | used to refer  |
   |                |                |                | specifically   |
   |                |                |                | to lesions,    |
   |                |                |                | `(52988006,    |
   |                |                |                | SCT,           |
   |                |                |                | "Les           |
   |                |                |                | ion") <http:// |
   |                |                |                | snomed.info/id |
   |                |                |                | /52988006>`__. |
   +----------------+----------------+----------------+----------------+
   | `DD            | Infection as   | `DD-           | Replacement    |
   | -67700 <http:/ | complication   | 67703 <http:// | code has       |
   | /snomed.info/i | of medical     | snomed.info/id | meaning        |
   | d/69698001>`__ | care           | /408678008>`__ | "Healthcare    |
   |                |                |                | associated     |
   |                |                |                | infectious     |
   |                |                |                | disease        |
   |                |                |                | (disorder)".   |
   |                |                |                |                |
   |                |                |                | Retired code   |
   |                |                |                | is inactive in |
   |                |                |                | SNOMED CT      |
   |                |                |                | (Duplicate).   |
   +----------------+----------------+----------------+----------------+
   | `P1-           | Hip joint      | `P1-           | Replacement    |
   | 14505 <http:// | implantation   | 0558A <http:// | code has       |
   | snomed.info/id |                | snomed.info/id | meaning        |
   | /119610009>`__ |                | /398010007>`__ | "Insertion of  |
   |                |                |                | hip prosthesis |
   |                |                |                | (procedure)".  |
   |                |                |                |                |
   |                |                |                | Retired code   |
   |                |                |                | is inactive in |
   |                |                |                | SNOMED CT      |
   |                |                |                | (Duplicate).   |
   +----------------+----------------+----------------+----------------+
   | `T-            | femoral lymph  | `T             | Replacement    |
   | C4801 <http:// | node           | -C4820 <http:/ | code has       |
   | snomed.info/id |                | /snomed.info/i | meaning        |
   | /310545001>`__ |                | d/65266007>`__ | "Structure of  |
   |                |                |                | deep inguinal  |
   |                |                |                | lymph node     |
   |                |                |                | (body          |
   |                |                |                | structure)".   |
   |                |                |                |                |
   |                |                |                | Retired code   |
   |                |                |                | is inactive in |
   |                |                |                | SNOMED CT      |
   |                |                |                | (Duplicate).   |
   +----------------+----------------+----------------+----------------+
   | C-120F9        | Aluminum or    | 12503006       | Replacement    |
   |                | Aluminum       |                | code has       |
   |                | compound       |                | meaning of     |
   |                |                |                | "Aluminum      |
   |                |                |                | (substance)".  |
   |                |                |                |                |
   |                |                |                | Retired code   |
   |                |                |                | is inactive in |
   |                |                |                | SNOMED CT.     |
   +----------------+----------------+----------------+----------------+
   | C-127F9        | Copper or      | 66925006       | Replacement    |
   |                | Copper compund |                | code has       |
   |                |                |                | meaning of     |
   |                |                |                | "Copper        |
   |                |                |                | (substance)".  |
   |                |                |                |                |
   |                |                |                | Retired code   |
   |                |                |                | is inactive in |
   |                |                |                | SNOMED CT.     |
   +----------------+----------------+----------------+----------------+
   | C-167F9        | Rhodium or     | 59801003       | Replacement    |
   |                | Rhodium        |                | code has       |
   |                | compound       |                | meaning of     |
   |                |                |                | "Rhodium       |
   |                |                |                | (substance)".  |
   |                |                |                |                |
   |                |                |                | Retired code   |
   |                |                |                | is inactive in |
   |                |                |                | SNOMED CT.     |
   +----------------+----------------+----------------+----------------+
   | C-1190E        | Niobium or     | 767776000      | Replacement    |
   |                | Niobium        |                | code has       |
   |                | compound       |                | meaning of     |
   |                |                |                | "Niobium       |
   |                |                |                | (substance)".  |
   |                |                |                |                |
   |                |                |                | Retired code   |
   |                |                |                | is inactive in |
   |                |                |                | SNOMED CT.     |
   +----------------+----------------+----------------+----------------+
   | C-1190F        | Europium or    | 767775001      | Replacement    |
   |                | Europium       |                | code has       |
   |                | compound       |                | meaning of     |
   |                |                |                | "Europium      |
   |                |                |                | (substance)".  |
   |                |                |                |                |
   |                |                |                | Retired code   |
   |                |                |                | is inactive in |
   |                |                |                | SNOMED CT.     |
   +----------------+----------------+----------------+----------------+
   | C-132F9        | Lead or Lead   | 88488004       | Replacement    |
   |                | compound       |                | code has       |
   |                |                |                | meaning of     |
   |                |                |                | "Lead          |
   |                |                |                | (substance)".  |
   |                |                |                |                |
   |                |                |                | Retired code   |
   |                |                |                | is inactive in |
   |                |                |                | SNOMED CT.     |
   +----------------+----------------+----------------+----------------+
   | C-156F9        | Tantalum or    | 45215009       | Replacement    |
   |                | Tantalum       |                | code has       |
   |                | compound       |                | meaning of     |
   |                |                |                | "Tantalum      |
   |                |                |                | (substance)".  |
   |                |                |                |                |
   |                |                |                | Retired code   |
   |                |                |                | is inactive in |
   |                |                |                | SNOMED CT.     |
   +----------------+----------------+----------------+----------------+
   | C-137F9        | Silver or      | 41967008       | Replacement    |
   |                | Silver         |                | code has       |
   |                | compound       |                | meaning of     |
   |                |                |                | "Silver        |
   |                |                |                | (substance)".  |
   |                |                |                |                |
   |                |                |                | Retired code   |
   |                |                |                | is inactive in |
   |                |                |                | SNOMED CT.     |
   +----------------+----------------+----------------+----------------+
   | C-139F9        | Tin or Tin     | 12597001       | Replacement    |
   |                | compound       |                | code has       |
   |                |                |                | meaning of     |
   |                |                |                | "Tin           |
   |                |                |                | (substance)".  |
   |                |                |                |                |
   |                |                |                | Retired code   |
   |                |                |                | is inactive in |
   |                |                |                | SNOMED CT.     |
   +----------------+----------------+----------------+----------------+
   | C-164F9        | Tungsten or    | 26194003       | Replacement    |
   |                | Tungsten       |                | code has       |
   |                | compound       |                | meaning of     |
   |                |                |                | "Tungsten      |
   |                |                |                | (substance)".  |
   |                |                |                |                |
   |                |                |                | Retired code   |
   |                |                |                | is inactive in |
   |                |                |                | SNOMED CT.     |
   +----------------+----------------+----------------+----------------+
   | C-130F9        | Iron           | 3829006        | Replacement    |
   |                |                |                | code has       |
   |                |                |                | meaning of     |
   |                |                |                | "Iron          |
   |                |                |                | (substance)".  |
   |                |                |                |                |
   |                |                |                | Retired code   |
   |                |                |                | is inactive in |
   |                |                |                | SNOMED CT.     |
   +----------------+----------------+----------------+----------------+
   | F-618BA        | Anti-heparin   | 3361000        | Replacement    |
   |                | agent          |                | code has       |
   |                |                |                | meaning of     |
   |                |                |                | "Anti-heparin  |
   |                |                |                | agent          |
   |                |                |                | (product)".    |
   |                |                |                |                |
   |                |                |                | Retired code   |
   |                |                |                | is inactive in |
   |                |                |                | SNOMED CT.     |
   +----------------+----------------+----------------+----------------+
   | C-80610        | Bile acid      | 372872006      | Replacement    |
   |                | sequestrant    |                | code has       |
   |                |                |                | meaning of     |
   |                |                |                | "Bile acid     |
   |                |                |                | sequestrant    |
   |                |                |                | antilipemic    |
   |                |                |                | agent          |
   |                |                |                | (substance)".  |
   |                |                |                |                |
   |                |                |                | Retired code   |
   |                |                |                | is inactive in |
   |                |                |                | SNOMED CT.     |
   +----------------+----------------+----------------+----------------+
   | C-2286B        | carbol fuchsin | 764166003      | Replacement    |
   |                | stain          |                | code has       |
   |                |                |                | meaning of     |
   |                |                |                | "              |
   |                |                |                | Carbol-fuchsin |
   |                |                |                | (substance)".  |
   |                |                |                |                |
   |                |                |                | Retired code   |
   |                |                |                | is inactive in |
   |                |                |                | SNOMED CT.     |
   +----------------+----------------+----------------+----------------+
   | C-80123        | Cardiotonic    | NCIt:C78322    | Replacement    |
   |                | drug           |                | code has       |
   |                |                |                | meaning of     |
   |                |                |                | "Cardiotonic   |
   |                |                |                | agent".        |
   |                |                |                |                |
   |                |                |                | Retired code   |
   |                |                |                | is inactive in |
   |                |                |                | SNOMED CT.     |
   +----------------+----------------+----------------+----------------+
   | C-80680        | Fibrate        | NCIt:C98150    | Replacement    |
   |                |                |                | code has       |
   |                |                |                | meaning of     |
   |                |                |                | "Fibrate       |
   |                |                |                | Antilipidemic  |
   |                |                |                | Agent".        |
   |                |                |                |                |
   |                |                |                | Retired code   |
   |                |                |                | is inactive in |
   |                |                |                | SNOMED CT.     |
   +----------------+----------------+----------------+----------------+
   | C-B1304        | Cho            |                | No             |
   |                | lyl-carbon^14^ |                | replacement.   |
   |                | glycine        |                |                |
   |                |                |                | Retired code   |
   |                |                |                | is inactive in |
   |                |                |                | SNOMED CT.     |
   +----------------+----------------+----------------+----------------+
   | C-B1051        | Colloidal gold |                | No             |
   |                | Au^198^        |                | replacement.   |
   |                |                |                |                |
   |                |                |                | Retired code   |
   |                |                |                | is inactive in |
   |                |                |                | SNOMED CT.     |
   +----------------+----------------+----------------+----------------+
   | C-B1063        | Colloidal      |                | No             |
   |                | Indium^111^    |                | replacement.   |
   |                |                |                |                |
   |                |                |                | Retired code   |
   |                |                |                | is inactive in |
   |                |                |                | SNOMED CT.     |
   +----------------+----------------+----------------+----------------+
   | C-B1092        | Di             |                | No             |
   |                | iodofluorecein |                | replacement.   |
   |                | I^131^         |                |                |
   |                |                |                | Retired code   |
   |                |                |                | is inactive in |
   |                |                |                | SNOMED CT.     |
   +----------------+----------------+----------------+----------------+
   | C-B1062        | Disodium       |                | No             |
   |                | indium^111^    |                | replacement.   |
   |                |                |                |                |
   |                |                |                | Retired code   |
   |                |                |                | is inactive in |
   |                |                |                | SNOMED CT.     |
   +----------------+----------------+----------------+----------------+
   | C-B1072        | Indium^113m^   |                | No             |
   |                | oxoquinoline   |                | replacement.   |
   |                | platelet label |                |                |
   |                |                |                | Retired code   |
   |                |                |                | is inactive in |
   |                |                |                | SNOMED CT.     |
   +----------------+----------------+----------------+----------------+
   | C-B1073        | Indium^113m^   |                | No             |
   |                | oxoquinoline   |                | replacement.   |
   |                | RBC label      |                |                |
   |                |                |                | Retired code   |
   |                |                |                | is inactive in |
   |                |                |                | SNOMED CT.     |
   +----------------+----------------+----------------+----------------+
   | C-B1071        | Indium^113m^   |                | No             |
   |                | oxoquinoline   |                | replacement.   |
   |                | WBC label      |                |                |
   |                |                |                | Retired code   |
   |                |                |                | is inactive in |
   |                |                |                | SNOMED CT.     |
   +----------------+----------------+----------------+----------------+
   | C-B1094        | Iodinated      |                | No             |
   |                | I^125^         |                | replacement.   |
   |                | levothyroxine  |                |                |
   |                |                |                | Retired code   |
   |                |                |                | is inactive in |
   |                |                |                | SNOMED CT.     |
   +----------------+----------------+----------------+----------------+
   | C-B1093        | Iodinated      |                | No             |
   |                | I^125^ oleic   |                | replacement.   |
   |                | acid and       |                |                |
   |                | triolein       |                | Retired code   |
   |                |                |                | is inactive in |
   |                |                |                | SNOMED CT.     |
   +----------------+----------------+----------------+----------------+
   | C-B1097        | Iodinated      |                | No             |
   |                | I^125^ Rose    |                | replacement.   |
   |                | Bengal         |                |                |
   |                |                |                | Retired code   |
   |                |                |                | is inactive in |
   |                |                |                | SNOMED CT.     |
   +----------------+----------------+----------------+----------------+
   | C-B1098        | Iodinated      |                | No             |
   |                | I^125^ sealed  |                | replacement.   |
   |                | source         |                |                |
   |                |                |                | Retired code   |
   |                |                |                | is inactive in |
   |                |                |                | SNOMED CT.     |
   +----------------+----------------+----------------+----------------+
   | C-114B6        | Iodine^131     |                | No             |
   |                | Methyl         |                | replacement.   |
   |                | norcholestenol |                |                |
   |                |                |                | Retired code   |
   |                |                |                | is inactive in |
   |                |                |                | SNOMED CT.     |
   +----------------+----------------+----------------+----------------+
   | C-B1034        | Fluoro-L-dopa  | 5811000122108  | Replacement    |
   |                | F^18^          |                | code has       |
   |                |                |                | meaning of     |
   |                |                |                | "Fluorodopa    |
   |                |                |                | [18F]          |
   |                |                |                | (substance)".  |
   |                |                |                |                |
   |                |                |                | Retired code   |
   |                |                |                | is inactive in |
   |                |                |                | SNOMED CT.     |
   +----------------+----------------+----------------+----------------+
   | C-B1046        | Germanium      | 53315004       | Replacement    |
   |                | Ge^68^         |                | code has       |
   |                |                |                | meaning of     |
   |                |                |                | "^68^Germanium |
   |                |                |                | (substance)".  |
   |                |                |                |                |
   |                |                |                | Retired code   |
   |                |                |                | is inactive in |
   |                |                |                | SNOMED CT.     |
   +----------------+----------------+----------------+----------------+
   | C-B07E6        | Monoclonal     | 423249007      | Replacement    |
   |                | antibody       |                | code has       |
   |                | I^124^         |                | meaning of     |
   |                |                |                | "Monoclonal    |
   |                |                |                | antibody       |
   |                |                |                | I^124^         |
   |                |                |                | (substance)".  |
   |                |                |                |                |
   |                |                |                | Retired code   |
   |                |                |                | is inactive in |
   |                |                |                | SNOMED CT.     |
   +----------------+----------------+----------------+----------------+
   | C-B1172        | Selenium^75^   | 395894004      | Replacement    |
   |                | HCAT           |                | code has       |
   |                |                |                | meaning of     |
   |                |                |                | "              |
   |                |                |                | Tauroselcholic |
   |                |                |                | acid[75Se]     |
   |                |                |                | (substance)".  |
   |                |                |                |                |
   |                |                |                | Retired code   |
   |                |                |                | is inactive in |
   |                |                |                | SNOMED CT.     |
   +----------------+----------------+----------------+----------------+
   | C-B1047        | Sodium Na^22^  | 71633006       | Replacement    |
   |                |                |                | code has       |
   |                |                |                | meaning of     |
   |                |                |                | "^22^Sodium    |
   |                |                |                | (substance)".  |
   |                |                |                |                |
   |                |                |                | Retired code   |
   |                |                |                | is inactive in |
   |                |                |                | SNOMED CT.     |
   +----------------+----------------+----------------+----------------+
   | C-B1204        | Technetium     | 85693008       | Replacement    |
   |                | Tc^99m^        |                | code has       |
   |                | albumin        |                | meaning of     |
   |                | colloid        |                | "Technetium    |
   |                |                |                | Tc^99m^        |
   |                |                |                | aggregated     |
   |                |                |                | albumin        |
   |                |                |                | (substance)".  |
   |                |                |                |                |
   |                |                |                | Retired code   |
   |                |                |                | is inactive in |
   |                |                |                | SNOMED CT.     |
   +----------------+----------------+----------------+----------------+
   | C-163BD        | Technetium^99m | 24511001       | Replacement    |
   |                | Dime           |                | code has       |
   |                | rcaptosuccinic |                | meaning of     |
   |                | Acid DMSA      |                | "Technetium    |
   |                |                |                | Tc^99m^        |
   |                |                |                | succimer       |
   |                |                |                | (substance)".  |
   |                |                |                |                |
   |                |                |                | Retired code   |
   |                |                |                | is inactive in |
   |                |                |                | SNOMED CT.     |
   +----------------+----------------+----------------+----------------+
   | C-163B7        | Technetium^99m | 53951001       | Replacement    |
   |                | Hy             |                | code has       |
   |                | droxymethylene |                | meaning of     |
   |                | diphosphonate  |                | "Technetium    |
   |                | HMDP           |                | Tc^99m^        |
   |                |                |                | oxidronate     |
   |                |                |                | (substance)".  |
   |                |                |                |                |
   |                |                |                | Retired code   |
   |                |                |                | is inactive in |
   |                |                |                | SNOMED CT.     |
   +----------------+----------------+----------------+----------------+
   | C-B1215        | Technetium     | 764821009      | Replacement    |
   |                | Tc^99m^ pyro   |                | code has       |
   |                | and            |                | meaning of     |
   |                | polyphosphates |                | "Technetium    |
   |                |                |                | (99m-Tc)       |
   |                |                |                | pyrophosphate  |
   |                |                |                | (substance)".  |
   |                |                |                |                |
   |                |                |                | Retired code   |
   |                |                |                | is inactive in |
   |                |                |                | SNOMED CT.     |
   +----------------+----------------+----------------+----------------+
   | C-B05A3        | Mangafodipir   | RXNORM:236987  | Replacement    |
   |                | trisodium      |                | code has       |
   |                |                |                | meaning of     |
   |                |                |                | "              |
   |                |                |                | Mangafodipir". |
   |                |                |                |                |
   |                |                |                | Retired code   |
   |                |                |                | is inactive in |
   |                |                |                | SNOMED CT.     |
   +----------------+----------------+----------------+----------------+
   | F-61FDB        | Radio          | 349358000      | Replacement    |
   |                | pharmaceutical |                | code has       |
   |                | agent          |                | meaning of     |
   |                |                |                | "Radiop        |
   |                |                |                | harmaceuticals |
   |                |                |                | (product)".    |
   |                |                |                |                |
   |                |                |                | Retired code   |
   |                |                |                | is inactive in |
   |                |                |                | SNOMED CT.     |
   +----------------+----------------+----------------+----------------+
   | G-A13B         | Off axis       | 103341000      | Replacement    |
   |                |                |                | code has       |
   |                |                |                | meaning of     |
   |                |                |                | "Off axis      |
   |                |                |                | (qualifier     |
   |                |                |                | value)".       |
   |                |                |                |                |
   |                |                |                | Retired code   |
   |                |                |                | means          |
   |                |                |                | something      |
   |                |                |                | completely     |
   |                |                |                | different,     |
   |                |                |                | "Unilateral    |
   |                |                |                | left           |
   |                |                |                | (qualifier     |
   |                |                |                | value)".       |
   +----------------+----------------+----------------+----------------+
   | C-A7440        | Injectable     | 764170006      | Replacement    |
   |                | fibrinolysin   |                | code has       |
   |                |                |                | meaning of     |
   |                |                |                | "Fibrinolysin  |
   |                |                |                | (substance)".  |
   |                |                |                |                |
   |                |                |                | Retired code   |
   |                |                |                | is inactive in |
   |                |                |                | SNOMED CT.     |
   +----------------+----------------+----------------+----------------+
   | C-B0301        | Ionic          | R              | Replacement    |
   |                | iodinated      | ADLEX:RID11585 | code has       |
   |                | contrast agent |                | meaning of     |
   |                |                |                | "ionic         |
   |                |                |                | iodinated      |
   |                |                |                | contrast       |
   |                |                |                | agent".        |
   |                |                |                |                |
   |                |                |                | Retired code   |
   |                |                |                | is inactive in |
   |                |                |                | SNOMED CT.     |
   +----------------+----------------+----------------+----------------+
   | C-B0302        | Non-ionic      | R              | Replacement    |
   |                | iodinated      | ADLEX:RID38696 | code has       |
   |                | contrast agent |                | meaning of     |
   |                |                |                | "non-ionic     |
   |                |                |                | iodinated      |
   |                |                |                | contrast       |
   |                |                |                | agent".        |
   |                |                |                |                |
   |                |                |                | Retired code   |
   |                |                |                | is inactive in |
   |                |                |                | SNOMED CT.     |
   +----------------+----------------+----------------+----------------+
   | C-97302        | Nasal          | 96328007       | Replacement    |
   |                | decongestant   |                | code has       |
   |                |                |                | meaning of     |
   |                |                |                | "Decongestant  |
   |                |                |                | preparation    |
   |                |                |                | (product)".    |
   |                |                |                |                |
   |                |                |                | Retired code   |
   |                |                |                | is inactive in |
   |                |                |                | SNOMED CT.     |
   +----------------+----------------+----------------+----------------+
   | F-61D70        | Ocular         | 470091001      | Replacement    |
   |                | Lubricant      |                | code has       |
   |                |                |                | meaning of     |
   |                |                |                | "Eye lubricant |
   |                |                |                | (physical      |
   |                |                |                | object)".      |
   |                |                |                |                |
   |                |                |                | Retired code   |
   |                |                |                | is inactive in |
   |                |                |                | SNOMED CT.     |
   +----------------+----------------+----------------+----------------+
   | C-81520        | Nitrate        | 372700007      | Replacement    |
   |                | vasodilator    |                | code has       |
   |                |                |                | meaning of     |
   |                |                |                | "Nitrate-based |
   |                |                |                | vasodilating   |
   |                |                |                | agent          |
   |                |                |                | (substance)".  |
   |                |                |                |                |
   |                |                |                | Retired code   |
   |                |                |                | is inactive in |
   |                |                |                | SNOMED CT.     |
   +----------------+----------------+----------------+----------------+
   | C-A7420        | Streptokinase  | 395889004      | Replacement    |
   |                | preparation    |                | code has       |
   |                |                |                | meaning of     |
   |                |                |                | "Streptokinase |
   |                |                |                | (substance)".  |
   |                |                |                |                |
   |                |                |                | Retired code   |
   |                |                |                | is inactive in |
   |                |                |                | SNOMED CT.     |
   +----------------+----------------+----------------+----------------+
   | A-04831        | Silicone gel   | 465380004      | Replacement    |
   |                | implant        |                | code has       |
   |                |                |                | meaning of     |
   |                |                |                | "Silicone      |
   |                |                |                | gel-filled     |
   |                |                |                | breast implant |
   |                |                |                | (physical      |
   |                |                |                | object)".      |
   |                |                |                |                |
   |                |                |                | Retired code   |
   |                |                |                | is inactive in |
   |                |                |                | SNOMED CT.     |
   +----------------+----------------+----------------+----------------+
   | C-22870        | potassium      | 34763001       | Replacement    |
   |                | hydroxide      |                | code has       |
   |                | stain          |                | meaning of     |
   |                |                |                | "Potassium     |
   |                |                |                | hydroxide      |
   |                |                |                | (substance)".  |
   |                |                |                |                |
   |                |                |                | Retired code   |
   |                |                |                | is inactive in |
   |                |                |                | SNOMED CT.     |
   +----------------+----------------+----------------+----------------+
   | D3-02004       | Hypertensive   | 443482000      | Replacement    |
   |                | episode        |                | code has       |
   |                |                |                | meaning of     |
   |                |                |                | "Hypertensive  |
   |                |                |                | urgency        |
   |                |                |                | (disorder)".   |
   |                |                |                |                |
   |                |                |                | Retired code   |
   |                |                |                | is inactive in |
   |                |                |                | SNOMED CT.     |
   +----------------+----------------+----------------+----------------+
   | T-C4404        | gut-associated |                | No             |
   |                | lymph node     |                | replacement.   |
   |                |                |                |                |
   |                |                |                | Retired code   |
   |                |                |                | is inactive in |
   |                |                |                | SNOMED CT.     |
   +----------------+----------------+----------------+----------------+
   | T-C4157        | submaxillary   | 59503006       | Replacement    |
   |                | lymph node     |                | code has       |
   |                |                |                | meaning of     |
   |                |                |                | "Structure of  |
   |                |                |                | submandibular  |
   |                |                |                | lymph node     |
   |                |                |                | (body          |
   |                |                |                | structure)".   |
   |                |                |                |                |
   |                |                |                | Retired code   |
   |                |                |                | is inactive in |
   |                |                |                | SNOMED CT.     |
   +----------------+----------------+----------------+----------------+
   | T-C4616        | subiliac lymph | FMA:323407     | Replacement    |
   |                | node           |                | code has       |
   |                |                |                | meaning of     |
   |                |                |                | "subiliac      |
   |                |                |                | lymph node".   |
   |                |                |                |                |
   |                |                |                | Retired code   |
   |                |                |                | is moved to    |
   |                |                |                | extension      |
   |                |                |                | namespace in   |
   |                |                |                | SNOMED CT.     |
   +----------------+----------------+----------------+----------------+
   | T-C4352        | supramammary   | FMA:12785      | Replacement    |
   |                | lymph node     |                | code has       |
   |                |                |                | meaning of     |
   |                |                |                | "supramammary  |
   |                |                |                | lymph node".   |
   |                |                |                |                |
   |                |                |                | Retired code   |
   |                |                |                | is moved to    |
   |                |                |                | extension      |
   |                |                |                | namespace in   |
   |                |                |                | SNOMED CT.     |
   +----------------+----------------+----------------+----------------+
   | P5-0A001       | PET brain      | 764666002      | Replacement    |
   |                | study          |                | code has       |
   |                |                |                | meaning of     |
   |                |                |                | "Positron      |
   |                |                |                | emission       |
   |                |                |                | tomography of  |
   |                |                |                | brain          |
   |                |                |                | (procedure)".  |
   |                |                |                |                |
   |                |                |                | Retired code   |
   |                |                |                | is inactive in |
   |                |                |                | SNOMED CT.     |
   +----------------+----------------+----------------+----------------+
   | P5-08118       | PET/CT MET     | 764704008      | Replacement    |
   |                | imaging of     |                | code has       |
   |                | whole body     |                | meaning of     |
   |                |                |                | "Positron      |
   |                |                |                | emission       |
   |                |                |                | tomography and |
   |                |                |                | computed       |
   |                |                |                | tomography of  |
   |                |                |                | whole body     |
   |                |                |                | using          |
   |                |                |                | methionine     |
   |                |                |                | C-11           |
   |                |                |                | (procedure)".  |
   |                |                |                |                |
   |                |                |                | Retired code   |
   |                |                |                | is inactive in |
   |                |                |                | SNOMED CT.     |
   +----------------+----------------+----------------+----------------+
   | L-8056C        | Minnesota #4   | 61083001       | Replacement    |
   |                | pig breed      |                | code has       |
   |                |                |                | meaning of     |
   |                |                |                | "Minnesota pig |
   |                |                |                | breed".        |
   |                |                |                |                |
   |                |                |                | Retired code   |
   |                |                |                | is inactive in |
   |                |                |                | SNOMED CT      |
   |                |                |                | (duplicate).   |
   +----------------+----------------+----------------+----------------+
   | C-10001        | Electron       | NCIt:C597      | Replacement    |
   |                |                |                | code has       |
   |                |                |                | meaning of     |
   |                |                |                | "Ion".         |
   |                |                |                |                |
   |                |                |                | Retired code   |
   |                |                |                | means          |
   |                |                |                | something      |
   |                |                |                | completely     |
   |                |                |                | different,     |
   |                |                |                | "Ion           |
   |                |                |                | (substance)"   |
   |                |                |                | and is         |
   |                |                |                | inactive       |
   |                |                |                | (erroneous) in |
   |                |                |                | SNOMED CT.     |
   +----------------+----------------+----------------+----------------+
   | C-51450        | D              | 372682005      | Replacement    |
   |                | iphenhydramine |                | code has       |
   |                |                |                | meaning of     |
   |                |                |                | "D             |
   |                |                |                | iphenhydramine |
   |                |                |                | (substance)".  |
   |                |                |                |                |
   |                |                |                | Retired        |
   |                |                |                | product code   |
   |                |                |                | is active in   |
   |                |                |                | SNOMED CT but  |
   |                |                |                | replacement    |
   |                |                |                | substance code |
   |                |                |                | is already in  |
   |                |                |                | DICOM subset.  |
   +----------------+----------------+----------------+----------------+
   | C-913A4        | Dexamethasone  | 396017000      | Replacement    |
   |                | sodium sulfate |                | code has       |
   |                |                |                | meaning of     |
   |                |                |                | "Dexamethasone |
   |                |                |                | sodium         |
   |                |                |                | phosphate      |
   |                |                |                | (substance)".  |
   |                |                |                |                |
   |                |                |                | Retired        |
   |                |                |                | product code   |
   |                |                |                | is active in   |
   |                |                |                | SNOMED CT but  |
   |                |                |                | replacement    |
   |                |                |                | substance code |
   |                |                |                | is already in  |
   |                |                |                | DICOM subset.  |
   +----------------+----------------+----------------+----------------+
   | C-68050        | Ephedrine      | 387358007      | Replacement    |
   |                |                |                | code has       |
   |                |                |                | meaning of     |
   |                |                |                | "Ephedrine     |
   |                |                |                | (substance)".  |
   |                |                |                |                |
   |                |                |                | Retired        |
   |                |                |                | product code   |
   |                |                |                | is active in   |
   |                |                |                | SNOMED CT but  |
   |                |                |                | replacement    |
   |                |                |                | substance code |
   |                |                |                | is already in  |
   |                |                |                | DICOM subset.  |
   +----------------+----------------+----------------+----------------+
   | C-A01D1        | Meth           | 412248005      | Replacement    |
   |                | ylprednisolone |                | code has       |
   |                | sodium         |                | meaning of     |
   |                | succinate      |                | "Meth          |
   |                |                |                | ylprednisolone |
   |                |                |                | sodium         |
   |                |                |                | succinate      |
   |                |                |                | (substance)".  |
   |                |                |                |                |
   |                |                |                | Retired        |
   |                |                |                | product code   |
   |                |                |                | is active in   |
   |                |                |                | SNOMED CT but  |
   |                |                |                | replacement    |
   |                |                |                | substance code |
   |                |                |                | is already in  |
   |                |                |                | DICOM subset.  |
   +----------------+----------------+----------------+----------------+
   | C-51071        | H-1            | 373228009      | Replacement    |
   |                | Antihistamine  |                | code has       |
   |                |                |                | meaning of "H1 |
   |                |                |                | antihistamine  |
   |                |                |                | (substance)".  |
   |                |                |                |                |
   |                |                |                | Retired        |
   |                |                |                | product code   |
   |                |                |                | is active in   |
   |                |                |                | SNOMED CT but  |
   |                |                |                | replacement    |
   |                |                |                | substance code |
   |                |                |                | is already in  |
   |                |                |                | DICOM subset.  |
   +----------------+----------------+----------------+----------------+
   | F-0499A        | Drug induced   | 16932000       | Replacement    |
   |                | Nausea and     |                | code has       |
   |                | vomiting       |                | meaning of     |
   |                |                |                | "Nausea and    |
   |                |                |                | vomiting       |
   |                |                |                | (disorder)".   |
   |                |                |                |                |
   |                |                |                | Retired code   |
   |                |                |                | is active in   |
   |                |                |                | SNOMED CT but  |
   |                |                |                | replacement    |
   |                |                |                | code is        |
   |                |                |                | already in     |
   |                |                |                | DICOM subset.  |
   +----------------+----------------+----------------+----------------+
   | P1-0555A       | Abdominal      | 771453009      | Replacement    |
   |                | aortic         |                | code has       |
   |                | aneurysm       |                | meaning of     |
   |                | stenting       |                | "Repair of     |
   |                |                |                | abdominal      |
   |                |                |                | aortic         |
   |                |                |                | aneurysm with  |
   |                |                |                | insertion of   |
   |                |                |                | stent          |
   |                |                |                | (procedure)".  |
   |                |                |                |                |
   |                |                |                | Retired code   |
   |                |                |                | is inactive in |
   |                |                |                | SNOMED CT.     |
   +----------------+----------------+----------------+----------------+
   | C-A6900        | Coagulant      | 373746004      | Replacement    |
   |                |                |                | code has       |
   |                |                |                | meaning of     |
   |                |                |                | "Coagulant     |
   |                |                |                | (substance)".  |
   |                |                |                |                |
   |                |                |                | Retired code   |
   |                |                |                | is inactive in |
   |                |                |                | SNOMED CT.     |
   +----------------+----------------+----------------+----------------+
   | F-047E7        | Functional     | DCM:130324     | Replacement    |
   |                | observable     |                | code has       |
   |                |                |                | meaning of     |
   |                |                |                | "Functional    |
   |                |                |                | condition      |
   |                |                |                | present during |
   |                |                |                | acquisition".  |
   |                |                |                |                |
   |                |                |                | Retired code   |
   |                |                |                | is inactive in |
   |                |                |                | SNOMED CT.     |
   +----------------+----------------+----------------+----------------+
   | C-677B9        | Atropine       | 771928002      | Replacement    |
   |                |                |                | code has       |
   |                |                |                | meaning of     |
   |                |                |                | "Product       |
   |                |                |                | containing     |
   |                |                |                | atropine in    |
   |                |                |                | ocular dose    |
   |                |                |                | form           |
   |                |                |                | (medicinal     |
   |                |                |                | product        |
   |                |                |                | form)".        |
   |                |                |                |                |
   |                |                |                | Retired code   |
   |                |                |                | is inactive in |
   |                |                |                | SNOMED CT.     |
   +----------------+----------------+----------------+----------------+
   | C-B1069        | Indium^113m^   | 767418009      | Replacement    |
   |                | chloride       |                | code has       |
   |                |                |                | meaning of     |
   |                |                |                | "Indium        |
   |                |                |                | (113-In)       |
   |                |                |                | chloride       |
   |                |                |                | (substance)".  |
   |                |                |                |                |
   |                |                |                | Retired code   |
   |                |                |                | is inactive in |
   |                |                |                | SNOMED CT.     |
   +----------------+----------------+----------------+----------------+
   | C-B0339        | Ioxaglate      | 412228003      | Replacement    |
   |                |                |                | code has       |
   |                |                |                | meaning of     |
   |                |                |                | "Ioxaglate     |
   |                |                |                | meglumine      |
   |                |                |                | (substance)".  |
   |                |                |                |                |
   |                |                |                | Retired code   |
   |                |                |                | is inactive in |
   |                |                |                | SNOMED CT.     |
   +----------------+----------------+----------------+----------------+
   | F-D7B50        | Thromboplastin | 387124009      | Replacement    |
   |                |                |                | code has       |
   |                |                |                | meaning of     |
   |                |                |                | "              |
   |                |                |                | Thromboplastin |
   |                |                |                | (substance)".  |
   |                |                |                |                |
   |                |                |                | Retired code   |
   |                |                |                | is inactive in |
   |                |                |                | SNOMED CT.     |
   +----------------+----------------+----------------+----------------+
   | C-22820        | Prussian blue  | 406452004      | Replacement    |
   |                | stain          |                | code has       |
   |                |                |                | meaning of     |
   |                |                |                | "Ferric        |
   |                |                |                | hexac          |
   |                |                |                | yanoferrate-II |
   |                |                |                | (substance)".  |
   |                |                |                |                |
   |                |                |                | Retired code   |
   |                |                |                | is inactive in |
   |                |                |                | SNOMED CT.     |
   +----------------+----------------+----------------+----------------+
   | C-22925        | rose bengal    | 408742009      | Replacement    |
   |                | stain          |                | code has       |
   |                |                |                | meaning of     |
   |                |                |                | "Rose bengal   |
   |                |                |                | (substance)".  |
   |                |                |                |                |
   |                |                |                | Retired code   |
   |                |                |                | is inactive in |
   |                |                |                | SNOMED CT.     |
   +----------------+----------------+----------------+----------------+
   | T-01625        | Nail of fifth  | 770820003      | Replacement    |
   |                | toe            |                | code has       |
   |                |                |                | meaning of     |
   |                |                |                | "Structure of  |
   |                |                |                | nail unit of   |
   |                |                |                | fifth toe      |
   |                |                |                | (body          |
   |                |                |                | structure)".   |
   |                |                |                |                |
   |                |                |                | Retired code   |
   |                |                |                | is inactive in |
   |                |                |                | SNOMED CT.     |
   +----------------+----------------+----------------+----------------+
   | T-01614        | Nail of finger | 770809003      | Replacement    |
   |                |                |                | code has       |
   |                |                |                | meaning of     |
   |                |                |                | "Structure of  |
   |                |                |                | nail unit of   |
   |                |                |                | finger (body   |
   |                |                |                | structure)".   |
   |                |                |                |                |
   |                |                |                | Retired code   |
   |                |                |                | is inactive in |
   |                |                |                | SNOMED CT.     |
   +----------------+----------------+----------------+----------------+
   | T-01624        | Nail of fourth | 770821004      | Replacement    |
   |                | toe            |                | code has       |
   |                |                |                | meaning of     |
   |                |                |                | "Structure of  |
   |                |                |                | nail unit of   |
   |                |                |                | fourth toe     |
   |                |                |                | (body          |
   |                |                |                | structure)".   |
   |                |                |                |                |
   |                |                |                | Retired code   |
   |                |                |                | is inactive in |
   |                |                |                | SNOMED CT.     |
   +----------------+----------------+----------------+----------------+
   | T-01621        | Nail of great  | 770822006      | Replacement    |
   |                | toe            |                | code has       |
   |                |                |                | meaning of     |
   |                |                |                | "Structure of  |
   |                |                |                | nail unit of   |
   |                |                |                | great toe      |
   |                |                |                | (body          |
   |                |                |                | structure)".   |
   |                |                |                |                |
   |                |                |                | Retired code   |
   |                |                |                | is inactive in |
   |                |                |                | SNOMED CT.     |
   +----------------+----------------+----------------+----------------+
   | T-01616        | Nail of index  | 770815003      | Replacement    |
   |                | finger         |                | code has       |
   |                |                |                | meaning of     |
   |                |                |                | "Structure of  |
   |                |                |                | nail unit of   |
   |                |                |                | index finger   |
   |                |                |                | (body          |
   |                |                |                | structure)".   |
   |                |                |                |                |
   |                |                |                | Retired code   |
   |                |                |                | is inactive in |
   |                |                |                | SNOMED CT.     |
   +----------------+----------------+----------------+----------------+
   | T-01619        | Nail of little | 770818001      | Replacement    |
   |                | finger         |                | code has       |
   |                |                |                | meaning of     |
   |                |                |                | "Structure of  |
   |                |                |                | nail unit of   |
   |                |                |                | little finger  |
   |                |                |                | (body          |
   |                |                |                | structure)".   |
   |                |                |                |                |
   |                |                |                | Retired code   |
   |                |                |                | is inactive in |
   |                |                |                | SNOMED CT.     |
   +----------------+----------------+----------------+----------------+
   | T-01617        | Nail of middle | 770816002      | Replacement    |
   |                | finger         |                | code has       |
   |                |                |                | meaning of     |
   |                |                |                | "Structure of  |
   |                |                |                | nail unit of   |
   |                |                |                | middle finger  |
   |                |                |                | (body          |
   |                |                |                | structure)".   |
   |                |                |                |                |
   |                |                |                | Retired code   |
   |                |                |                | is inactive in |
   |                |                |                | SNOMED CT.     |
   +----------------+----------------+----------------+----------------+
   | T-01618        | Nail of ring   | 770817006      | Replacement    |
   |                | finger         |                | code has       |
   |                |                |                | meaning of     |
   |                |                |                | "Structure of  |
   |                |                |                | nail unit of   |
   |                |                |                | ring finger    |
   |                |                |                | (body          |
   |                |                |                | structure)".   |
   |                |                |                |                |
   |                |                |                | Retired code   |
   |                |                |                | is inactive in |
   |                |                |                | SNOMED CT.     |
   +----------------+----------------+----------------+----------------+
   | T-01622        | Nail of second | 770823001      | Replacement    |
   |                | toe            |                | code has       |
   |                |                |                | meaning of     |
   |                |                |                | "Structure of  |
   |                |                |                | nail unit of   |
   |                |                |                | second toe     |
   |                |                |                | (body          |
   |                |                |                | structure)".   |
   |                |                |                |                |
   |                |                |                | Retired code   |
   |                |                |                | is inactive in |
   |                |                |                | SNOMED CT.     |
   +----------------+----------------+----------------+----------------+
   | T-01623        | Nail of third  | 770825008      | Replacement    |
   |                | toe            |                | code has       |
   |                |                |                | meaning of     |
   |                |                |                | "Structure of  |
   |                |                |                | nail unit of   |
   |                |                |                | third toe      |
   |                |                |                | (body          |
   |                |                |                | structure)".   |
   |                |                |                |                |
   |                |                |                | Retired code   |
   |                |                |                | is inactive in |
   |                |                |                | SNOMED CT.     |
   +----------------+----------------+----------------+----------------+
   | T-01615        | Nail of thumb  | 770810008      | Replacement    |
   |                |                |                | code has       |
   |                |                |                | meaning of     |
   |                |                |                | "Structure of  |
   |                |                |                | nail unit of   |
   |                |                |                | thumb (body    |
   |                |                |                | structure)".   |
   |                |                |                |                |
   |                |                |                | Retired code   |
   |                |                |                | is inactive in |
   |                |                |                | SNOMED CT.     |
   +----------------+----------------+----------------+----------------+
   | T-01620        | Nail of toe    | 770805009      | Replacement    |
   |                |                |                | code has       |
   |                |                |                | meaning of     |
   |                |                |                | "Structure of  |
   |                |                |                | nail unit of   |
   |                |                |                | toe (body      |
   |                |                |                | structure)".   |
   |                |                |                |                |
   |                |                |                | Retired code   |
   |                |                |                | is inactive in |
   |                |                |                | SNOMED CT.     |
   +----------------+----------------+----------------+----------------+
   | A-26860        | Swann-Ganz     | 397755005      | Replacement    |
   |                | catheter       |                | code has       |
   |                |                |                | meaning of     |
   |                |                |                | "Pulmonary     |
   |                |                |                | artery         |
   |                |                |                | catheter       |
   |                |                |                | (physical      |
   |                |                |                | object)".      |
   |                |                |                |                |
   |                |                |                | Retired code   |
   |                |                |                | is inactive in |
   |                |                |                | SNOMED CT.     |
   +----------------+----------------+----------------+----------------+
   | C-B10A2        | Tc-99m         | 424299003      | Replacement    |
   |                | sestamibi      |                | code has       |
   |                |                |                | meaning of     |
   |                |                |                | "Technetium    |
   |                |                |                | Tc^99m^        |
   |                |                |                | sestamibi      |
   |                |                |                | (substance)".  |
   |                |                |                |                |
   |                |                |                | Retired code   |
   |                |                |                | is inactive in |
   |                |                |                | SNOMED CT.     |
   +----------------+----------------+----------------+----------------+
   | C-B10A4        | Tc-99m         | 424118002      | Replacement    |
   |                | tetrofosmin    |                | code has       |
   |                |                |                | meaning of     |
   |                |                |                | "Technetium    |
   |                |                |                | Tc^99m^        |
   |                |                |                | tetrofosmin    |
   |                |                |                | (substance)".  |
   |                |                |                |                |
   |                |                |                | Retired code   |
   |                |                |                | is inactive in |
   |                |                |                | SNOMED CT.     |
   +----------------+----------------+----------------+----------------+
   | `R-            | Papaverine     | `3727          | Replacement    |
   | F2989 <http:// |                | 84001 <http:// | code has       |
   | snomed.info/id |                | snomed.info/id | meaning of     |
   | /346607007>`__ |                | /372784001>`__ | "Papaverine    |
   |                |                |                | (substance)".  |
   |                |                |                |                |
   |                |                |                | Retired code   |
   |                |                |                | is inactive in |
   |                |                |                | SNOMED CT.     |
   +----------------+----------------+----------------+----------------+
   | `P5            | Percutaneous   | `2409          | Replacement    |
   | -39050 <http:/ | retrieval of   | 46003 <http:// | code has       |
   | /snomed.info/i | endovascular   | snomed.info/id | meaning of     |
   | d/37630009>`__ | foreign body   | /240946003>`__ | "Percutaneous  |
   |                |                |                | removal of     |
   |                |                |                | endovascular   |
   |                |                |                | foreign body   |
   |                |                |                | (procedure)".  |
   |                |                |                |                |
   |                |                |                | Retired code   |
   |                |                |                | is inactive in |
   |                |                |                | SNOMED CT.     |
   +----------------+----------------+----------------+----------------+
   | `1133          | Abdomen        | `8189          | Replacement    |
   | 45001 <http:// |                | 81001 <http:// | code has       |
   | snomed.info/id |                | snomed.info/id | meaning of     |
   | /113345001>`__ |                | /818981001>`__ | "Structure of  |
   |                |                |                | abdominal      |
   |                |                |                | c              |
   |                |                |                | ross-sectional |
   |                |                |                | segment of     |
   |                |                |                | trunk (body    |
   |                |                |                | structure)".   |
   |                |                |                |                |
   |                |                |                | Retired code   |
   |                |                |                | is inactive in |
   |                |                |                | SNOMED CT.     |
   +----------------+----------------+----------------+----------------+
   | `4169          | Abdomen and    | `8189          | Replacement    |
   | 49008 <http:// | Pelvis         | 82008 <http:// | code has       |
   | snomed.info/id |                | snomed.info/id | meaning of     |
   | /416949008>`__ |                | /818982008>`__ | "Structure of  |
   |                |                |                | abdominopelvic |
   |                |                |                | c              |
   |                |                |                | ross-sectional |
   |                |                |                | segment of     |
   |                |                |                | trunk (body    |
   |                |                |                | structure)".   |
   |                |                |                |                |
   |                |                |                | Retired code   |
   |                |                |                | is inactive in |
   |                |                |                | SNOMED CT.     |
   +----------------+----------------+----------------+----------------+
   | `51            | Chest          | `8160          | Replacement    |
   | 185008 <http:/ |                | 94009 <http:// | code has       |
   | /snomed.info/i |                | snomed.info/id | meaning of     |
   | d/51185008>`__ |                | /816094009>`__ | "Structure of  |
   |                |                |                | thoracic       |
   |                |                |                | c              |
   |                |                |                | ross-sectional |
   |                |                |                | segment of     |
   |                |                |                | trunk (body    |
   |                |                |                | structure)".   |
   |                |                |                |                |
   |                |                |                | Retired code   |
   |                |                |                | is still       |
   |                |                |                | active in      |
   |                |                |                | SNOMED CT.     |
   |                |                |                |                |
   |                |                |                | Also used in   |
   |                |                |                | DICOM with     |
   |                |                |                | synonym        |
   |                |                |                | "Thorax".      |
   +----------------+----------------+----------------+----------------+
   | `12            | Pelvis         | `8160          | Replacement    |
   | 921003 <http:/ |                | 92008 <http:// | code has       |
   | /snomed.info/i |                | snomed.info/id | meaning of     |
   | d/12921003>`__ |                | /816092008>`__ | "Structure of  |
   |                |                |                | pelvic         |
   |                |                |                | c              |
   |                |                |                | ross-sectional |
   |                |                |                | segment of     |
   |                |                |                | trunk (body    |
   |                |                |                | structure)".   |
   |                |                |                |                |
   |                |                |                | Retired code   |
   |                |                |                | is still       |
   |                |                |                | active in      |
   |                |                |                | SNOMED CT.     |
   +----------------+----------------+----------------+----------------+
   | `52            | I              | `8189          | Replacement    |
   | 731004 <http:/ | ntra-abdominal | 87002 <http:// | code has       |
   | /snomed.info/i |                | snomed.info/id | meaning of     |
   | d/52731004>`__ |                | /818987002>`__ | "Structure of  |
   |                |                |                | abdominopelvic |
   |                |                |                | cavity (body   |
   |                |                |                | structure)".   |
   |                |                |                |                |
   |                |                |                | Retired code   |
   |                |                |                | is inactive in |
   |                |                |                | SNOMED CT.     |
   |                |                |                |                |
   |                |                |                | Also used in   |
   |                |                |                | DICOM with     |
   |                |                |                | synonym        |
   |                |                |                | "              |
   |                |                |                | Abdominopelvic |
   |                |                |                | cavity".       |
   +----------------+----------------+----------------+----------------+
   | `21            | Intra-pelvic   | `8169          | Replacement    |
   | 844003 <http:/ |                | 89007 <http:// | code has       |
   | /snomed.info/i |                | snomed.info/id | meaning of     |
   | d/21844003>`__ |                | /816989007>`__ | "Structure of  |
   |                |                |                | cavity of      |
   |                |                |                | false and/or   |
   |                |                |                | true pelvis    |
   |                |                |                | (body          |
   |                |                |                | structure)".   |
   |                |                |                |                |
   |                |                |                | Retired code   |
   |                |                |                | is inactive in |
   |                |                |                | SNOMED CT.     |
   +----------------+----------------+----------------+----------------+
   | `51            | Intra-thoracic | `43            | Replacement    |
   | 185008 <http:/ |                | 799004 <http:/ | code has       |
   | /snomed.info/i |                | /snomed.info/i | meaning of     |
   | d/51185008>`__ |                | d/43799004>`__ | "Thoracic      |
   |                |                |                | cavity         |
   |                |                |                | structure      |
   |                |                |                | (body          |
   |                |                |                | structure)".   |
   |                |                |                |                |
   |                |                |                | Retired code   |
   |                |                |                | is still       |
   |                |                |                | active in      |
   |                |                |                | SNOMED CT.     |
   |                |                |                |                |
   |                |                |                | Also used in   |
   |                |                |                | DICOM with     |
   |                |                |                | synonym "Chest |
   |                |                |                | cavity"        |
   +----------------+----------------+----------------+----------------+

