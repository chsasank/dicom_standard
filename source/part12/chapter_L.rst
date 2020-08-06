.. _chapter_L:

RFC3240 - Digital Imaging and Communications in Medicine (dicom) - Application/dicom MIME Sub-type Registration (Informative)
=============================================================================================================================

::

   Network Working Group                                          D. Clunie
   Request for Comments: 3240                                 E. Cordonnier
   Category: Informational                                  DICOM Committee
                                                              February 2002


           Digital Imaging and Communications in Medicine (DICOM) -
                 Application/dicom MIME Sub-type Registration

   Status of this Memo

      This memo provides information for the Internet community.  It does
      not specify an Internet standard of any kind.  Distribution of this
      memo is unlimited.

   Copyright Notice

      Copyright (C) The Internet Society (2002).  All Rights Reserved.

   Abstract

      This document describes the registration of the MIME sub-type
      application/dicom (Digital Imaging and Communications in Medicine).
      The baseline encoding is defined by the DICOM Standards Committee in
      "Digital Imaging and Communications in Medicine".

   1. DICOM Definition

      Digital Imaging and Communications in Medicine (DICOM) specifies
      protocols and formats for the exchange of images, time-based
      waveforms, reports, and associated information for medical
      applications.

      Individual DICOM objects (such as images) may be encapsulated in
      files and exchanged by e-mail using the Media Type defined herein.
      In addition, a set of DICOM files may be described by an index file,
      DICOMDIR, which may accompany the files that it references.

   2.  IANA Registration

      MIME media type name: Application

      MIME subtype name: dicom

   Required parameters:

         "id" is constructed from a DICOM File ID (see DICOM PS3.11).  The
         total length is limited to 71 characters.  Each component is
         limited to 8 characters.  The delimiter is a forward slash "/".
         There is never a leading delimiter (i.e., this is not a
         traditional path from a root directory).

         If a DICOMDIR (which provides an index of files) is included, then
         it will refer to other DICOM files in the file set by use of this
         File ID.  The File ID is not encoded within each DICOM file.  If a
         DICOMDIR is not present, then the "id" parameter may be absent.
         Note that the DICOMDIR will also have a Media Type of
         application/dicom and is distinguished from other files by its ID
         of "DICOMDIR".

         For example:
          "ROOTDIR/SUBDIR1/MRSCAN/A789FD07/19991024/ST00234/S00003/I00023"

         Each component shall be character strings made of characters from
         a subset of the G0 repertoire of ISO 8859.  This subset consists
         of uppercase alphabetic characters, numeric characters and
         underscore.  The following characters are permissible:

         A, B, C, D, E, F, G, H, I, J, K, L, M, N, O, P, Q, R, S, T, U, V,
         W, X, Y, Z (uppercase)
         1, 2, 3, 4, 5, 6, 7, 8, 9, 0 and _ (underscore)

      Optional parameters:

         none

      Encoding considerations:

         The DICOM information is binary, therefore the encoding used shall
         support lossless transfer of binary information.  Typically, the
         Content-Transfer-Encoding would be set to "Base64".

         Multiple DICOM parts should be included as a Multipart/related
         entity [2387].  Receiving agents shall also support multiple parts
         as a Multipart/mixed entity.  When multiple DICOM parts are
         included, one of the parts may be a DICOMDIR, in which case, all
         the files referred to by the DICOMDIR shall also be present.  The
         DICOMDIR is not required to be the first Application/dicom part
         encoded in the message, in which case the optional "start"
         parameter should refer to the content-id of the part containing
         the DICOMDIR.

         Multiple DICOM Application/dicom parts may be included with other
         types of parts as a Multipart/mixed entity.

      Security considerations:

         Application/dicom parts contain medical information, including
         individual demographic information.  Accordingly, their exchange
         should be restricted to a secure network or within a secure
         wrapper that protects a patient's right to confidentiality
         according to local and national policy.  The specific security
         mechanisms are outside the scope of this proposal.  Such
         mechanisms as Secured MIME (S/MIME) [2633] or similar might be
         appropriate.

      Interoperability considerations:

         Because DICOM information is specific to the medical (imaging)
         domain, generic e-mail applications may not be able to interpret
         the information.

         The Media Type has been designed in order to allow for

         (i)   DICOM aware applications to interoperate,
         (ii)  generic applications to save the files in a form
               recognizable as DICOM files, that a DICOM application may
               subsequently use.

      Published specification:

         The Digital Imaging and Communications in Medicine (DICOM)
         Standard is a standard of the DICOM Standards Committee, published
         by the National Electrical Manufacturers Association (NEMA), 1300
         N. 17th Street, Rosslyn, Virginia 22209 USA,
         (http://medical.nema.org).

      Applications which use this media:

         Biomedical imaging applications.

      Additional information:

         1. Magic number(s): "DICM" after 128 byte preamble indicates DICOM
                               PS 3.10 file

         2. File extension(s): ".dcm" is recommended for files saved to
                                 disk (other than DICOMDIR)

         3. Macintosh file type code:  Macintosh File Type "DICM" is
                                        recommended

         4. Object Identifiers: none

      Person to contact for further information:

         1. Name: Howard Clark
         2. E-mail: how_clark@nema.org

      Intended usage:

         Common

         Interchange of biomedical images.

      Author/Change controller:

         DICOM Standards Committee

   3. References

      [DICOM]  DICOM Standards Committee, "Digital Imaging and
               Communications in Medicine", 2001.

      [2387]   Levinson, E., "The MIME Multipart/Related Content-type", RFC
               2387, August 1998.

      [2633]   Ramsdell, B., "S/MIME Version 3 Message Specification", RFC
               2633, June 1999.

   4. Authors' Addresses

      David Clunie
      RadPharm
      943 Heiden Road
      Bangor PA 18013
      USA

      Phone: +1-570-897-7123
      Fax:   +1-425-930-0171
      EMail: dclunie@dclunie.com


      Emmanuel Cordonnier
      Etiam
      20 rue du Pr J. Pecker
      35000 Rennes
      France

      Phone: +33(0)299 14 33 88
      Fax:   +33(0)299 14 33 80
      EMail: emmanuel.cordonnier@etiam.com

   5.  Full Copyright Statement

      Copyright (C) The Internet Society (2002).  All Rights Reserved.

      This document and translations of it may be copied and furnished to
      others, and derivative works that comment on or otherwise explain it
      or assist in its implementation may be prepared, copied, published
      and distributed, in whole or in part, without restriction of any
      kind, provided that the above copyright notice and this paragraph are
      included on all such copies and derivative works.  However, this
      document itself may not be modified in any way, such as by removing
      the copyright notice or references to the Internet Society or other
      Internet organizations, except as needed for the purpose of
      developing Internet standards in which case the procedures for
      copyrights defined in the Internet Standards process must be
      followed, or as required to translate it into languages other than
      English.

      The limited permissions granted above are perpetual and will not be
      revoked by the Internet Society or its successors or assigns.

      This document and the information contained herein is provided on an
      "AS IS" basis and THE INTERNET SOCIETY AND THE INTERNET ENGINEERING
      TASK FORCE DISCLAIMS ALL WARRANTIES, EXPRESS OR IMPLIED, INCLUDING
      BUT NOT LIMITED TO ANY WARRANTY THAT THE USE OF THE INFORMATION
      HEREIN WILL NOT INFRINGE ANY RIGHTS OR ANY IMPLIED WARRANTIES OF
      MERCHANTABILITY OR FITNESS FOR A PARTICULAR PURPOSE.

   Acknowledgment

      Funding for the RFC Editor function is currently provided by the
      Internet Society.

.. _sect_L.2:

Example 1: Simple DICOM File MIME Message (Informative)
-------------------------------------------------------

::

   From: "Dr Smith" <smith@provider1.com>
   To: "Dr Johnson" <johnson@provider2.com>
   Subject: test DICOM Mime Type
   Date: Fri, 5 Nov 1999 15:15:35 +0100
   MIME-Version: 1.0
   Content-Type: Multipart/mixed;
       boundary="----=_NextPart_000_0027_01BF27A0.9BE21980"

   This is a multi-part message in MIME format.

   ------=_NextPart_000_0027_01BF27A0.9BE21980
   Content-Type: text/plain;
       charset="iso-8859-1"
   Content-Transfer-Encoding: 7bit

   Message text: this is a DICOM MIME Type example for DICOM File.

   ------=_NextPart_000_0027_01BF27A0.9BE21980
   Content-Type: Application/dicom;
       id="i00023"; name="i00023.dcm"
   Content-Transfer-Encoding: base64

   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

   ------=_NextPart_000_0027_01BF27A0.9BE21980--

.. _sect_L.3:

Example 2: DICOM File Set MIME Message (Informative)
----------------------------------------------------

::

   From: "Dr Johnson" <drjohnson@provider.org>
   To: "Dr Smith" <drsmith@provider.org>
   Subject: DICOM MIME sub-type file set example
   Date: Sat, 9 Mar 2002 16:24:27 +0100
   MIME-Version: 1.0
   Content-Type: multipart/mixed;
       boundary="----=_NextPart_000_0062_01C1C786.EA262CC0";
       start="<header1@provider.org>";
       type="text/plain"

   This is a multi-part message in MIME format.

   ------=_NextPart_000_0062_01C1C786.EA262CC0
   Content-Type: text/plain;
       charset="iso-8859-1"
   Content-Transfer-Encoding: 7bit
   Content-ID: "<intro@provider.org>"

   This is an example message containing a DICOM file set encoded following the
   DICOM MIME sub-type (RFC3240).


   ------=_NextPart_000_0062_01C1C786.EA262CC0
   Content-Type: text/plain;
       name="header1.txt"
   Content-Transfer-Encoding: quoted-printable
   Content-Disposition: attachment;
       filename="header1.txt"
   Content-ID: "<header1@provider.org>"
   Content-Description: Header of the medical message

   This is the header part of the message, which contains:
   - a first text document (letter1)
   - a DICOM file set part (dicomfileset1) including an additional =
   complementary note
   This message was sent by Dr Johnson to Dr Smith.
   It relates to the patient: DICOM Nema (M) 01/01/1993
   ------=_NextPart_000_0062_01C1C786.EA262CC0
   Content-Type: multipart/related;
       boundary="----=_NextPart_000_0062_01C1C786.EA262CC1_13487";
       start="<dicomfileset1.dicomdir@provider.org>";
       type="application/dicom"

   ------=_NextPart_000_0062_01C1C786.EA262CC1_13487
   Content-Type: text/plain;
       name="dicomfileset1note1.txt"
   Content-Transfer-Encoding: 7bit
   Content-Disposition: attachment;
       filename="dicomfileset1note1.txt"
   Content-ID: "<dicomfileset1.note1@provider.org>"
   Content-Description: Note for the images use

   This is a simple note, for receivers who can not read images.
   These images are DICOM images and the DICOMDIR index related file.
   Please use a DICOM compatible application.
   DICOM is a Standard Mark of Nema (www.nema.org).
   ------=_NextPart_000_0062_01C1C786.EA262CC1_13487
   Content-Type: application/dicom;
       id="DICOMDIR";
       name="Dicomdir"
   Content-Transfer-Encoding: base64
   Content-Disposition: attachment;
       filename="Dicomdir";
   Content-ID: "<dicomfileset1.dicomdir@provider.org>"
   Content-Description: Index of the images (DICOMDIR)

   AAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAA
   AAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAA
   AAAAAAAAAAAAAAAAAABESUNNAgAAAFVMBACIAAAAAgABAE9CAAACAAAAAQACAAIAVUkUADEuMi44
   NDAuMTAwMDguMS4zLjEwAgADAFVJIAAxLjIuMjUwLjEuNTkuMi40Mi4yMDAyMDMwOTE2NDkyMAIA
   EABVSRQAMS4yLjg0MC4xMDAwOC4xLjIuMQACABIAVUkSADEuMi4yNTAuMS41OS4yLjQ0AAQAAABV
   TAQAdgMAAAQAMBFDUw4ARVRJQU1fREVZRTI0NAAEAAASVUwEAGgBAAAEAAISVUwEAGgBAAAEABIS
   VVMCAAAABAAgElNRAAAyAwAA/v8A4G4AAAAEAAAUVUwEAAAAAAAEABAUVVMCAP//BAAgFFVMBADe
   AQAABAAwFENTCABQQVRJRU5UIBAAEABQTgoARElDT01eTkVNQRAAIABMTwgARElDT00zMAAQADAA
   REEIADE5OTMwMTAxEABAAENTAgBNAP7/AOCmAAAABAAAFFVMBAAAAAAABAAQFFVTAgD//wQAIBRV
   TAQAjAIAAAQAMBRDUwYAU1RVRFkgCAAgAERBCAAyMDAyMDMwOQgAMABUTQYAMTYwMzI1CABQAFNI
   CABESUNPTTMwAAgAMBBMTxgARElDT00gTUlNRSB0eXBlIGV4YW1wbGUAIAANAFVJGAAxLjIuMjUw
   LjEuNTkuMTIzLjQ1Ni43ODkgABAAU0gAAP7/AOCGAAAABAAAFFVMBAAAAAAABAAQFFVTAgD//wQA
   IBRVTAQAGgMAAAQAMBRDUwYAU0VSSUVTCABgAENTAgBPVAgAgABMTwAACACBAFNUAAAIAD4QTE8A
   AAgAUBBQTgAAIAAOAFVJGgAxLjIuMjUwLjEuNTkuMTIzLjQ1Ni43ODkuMSAAEQBJUwIAMQD+/wDg
   uAAAAAQAABRVTAQA2gMAAAQAEBRVUwIA//8EACAUVUwEAAAAAAAEADAUQ1MGAElNQUdFIAQAABVD
   UwwAU0UwMDAxL0kwMDAxBAAQFVVJGgAxLjIuODQwLjEwMDA4LjUuMS40LjEuMS43AAQAERVVSRwA
   MS4yLjI1MC4xLjU5LjEyMy40NTYuNzg5LjEuMQQAEhVVSRQAMS4yLjg0MC4xMDAwOC4xLjIuMQAI
   AAgAQ1MAACAAEwBJUwIAMQD+/wDguAAAAAQAABRVTAQAAAAAAAQAEBRVUwIA//8EACAUVUwEAAAA
   AAAEADAUQ1MGAElNQUdFIAQAABVDUwwAU0UwMDAxL0kwMDAyBAAQFVVJGgAxLjIuODQwLjEwMDA4
   LjUuMS40LjEuMS43AAQAERVVSRwAMS4yLjI1MC4xLjU5LjEyMy40NTYuNzg5LjEuMgQAEhVVSRQA
   MS4yLjg0MC4xMDAwOC4xLjIuMQAIAAgAQ1MAACAAEwBJUwIAMgA=

   ------=_NextPart_000_0062_01C1C786.EA262CC1_13487
   Content-Type: application/dicom;
       id="SE0001/I0001";
       name="I0001.dcm"
   Content-Transfer-Encoding: base64
   Content-Disposition: attachment;
       filename="I0001.dcm"
   Content-ID: "<dicomfileset1.se0001.i0001@provider.org>"
   Content-Description: Color image


   AAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAA
   AAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAA
   AAAAAAAAAAAAAAAAAABESUNNAgAAAFVMBACmAAAAAgABAE9CAAACAAAAAQACAAIAVUkaADEuMi44
   NDAuMTAwMDguNS4xLjQuMS4xLjcAAgADAFVJHAAxLjIuMjUwLjEuNTkuMTIzLjQ1Ni43ODkuMS4x
   AgAQAFVJFAAxLjIuODQwLjEwMDA4LjEuMi4xAAIAEgBVSRgAMS4yLjI1MC4xLjU5LjIuNDMuODYu
   MjQzAgATAFNIDgBBQ1EtRVRJQU0tMi40MwgAAABVTAQAxAAAAAgABQBDUwoASVNPX0lSIDEwMAgA
   FgBVSRoAMS4yLjg0MC4xMDAwOC41LjEuNC4xLjEuNwAIABgAVUkcADEuMi4yNTAuMS41OS4xMjMu
   NDU2Ljc4OS4xLjEIACAAREEIADIwMDIwMzA5CAAwAFRNBgAxNjAzMjUIAFAAU0gIAERJQ09NMzAA
   CABgAENTAgBPVAgAZABDUwQAV1NEAAgAkABQTgAACAAwEExPGABESUNPTSBNSU1FIHR5cGUgZXhh
   bXBsZQAQAAAAVUwEADwAAAAQABAAUE4KAERJQ09NXk5lbWEQACAATE8IAERJQ09NMzAAEAAwAERB
   CAAxOTkzMDEwMRAAQABDUwIATQAgAAAAVUwEAF4AAAAgAA0AVUkYADEuMi4yNTAuMS41OS4xMjMu
   NDU2Ljc4OSAADgBVSRoAMS4yLjI1MC4xLjU5LjEyMy40NTYuNzg5LjEgABAAU0gAACAAEQBJUwIA
   MQAgABMASVMCADEAKAAAAFVMBABmAAAAKAACAFVTAgADACgABABDUwQAUkdCICgABgBVUwIAAAAo
   AAgASVMCADEAKAAQAFVTAgAIACgAEQBVUwIAGgAoAAABVVMCAAgAKAABAVVTAgAIACgAAgFVUwIA
   BwAoAAMBVVMCAAAA4H8AAFVMBAB8AgAA4H8QAE9CAABwAgAA////9fXs0NCivLx6zMyZ4uLG7/Hr
   6+/v7vHx/f39+vv77PDw+vv7+/z83+Xl5erq/f399ff33uTk+vv7/v7+9fb2/////v7+7fDw+/z8
   8PHlcYNRXnI5dIVPUm1ISmpYaoJpdY+HtMPDeJKS6O3tb4uL4ujoj6WlzdfXtcTEwc3Nm6+vyNPT
   cY2N6+/vhJ2d9ff33uTkjqSk9/j4zs6fVWw2coNQY3pUGUU8K1NKdY19i5+P/f79kKamu8nJb4yM
   v8zMiaCg/v7+/P39lKmpxdDQ/v7+j6Wlrb29aYeHpri4oLOzdZCQ////29u4l5k6RGJCnql/TW1b
   v8Wkh5yLg5mM/v7+ma2ty9XVb4yMyNLSdZCQ+fr6+/z8m6+vq7u7/v7+k6iou8jIo7W1YoKCsMDA
   b4yM////+/v4ycmTfoxQurt+r7WF4ODDorKodpGQuMbGs8LC8vT0h5+f5uvrpri4nbCwq7y83eTk
   kaentcTErb6+4efnu8jIq7y86+7uiqGh9ff3+/v4+Pjy5ubR3Ny74+PH8vLm+vr1+fn0+vr3+vr2
   +fn0+/v3+vr1+fn0+fn1+Pjz+vr1+fn0+Pn1+vr2/Pz59/fw+fnz+fn0+fn0/Pz66OjT0tKl1tau
   3Ny619ew2tq21tau1NSq5OTJ2dm03d294uLG2Niz2Nix2dmz19ex2Niz1NSq3t6+39+/5ubP0tKm
   09Oo2dm11tau8fHj////+/v4/v7+/////////v7++/v4/Pz6/f38////////////////////////
   ////////////////////////////////////////////

   ------=_NextPart_000_0062_01C1C786.EA262CC1_13487
   Content-Type: application/dicom;
       id="SE0001/I0002";
       name="I0002.dcm"
   Content-Transfer-Encoding: base64
   Content-Disposition: attachment;
       filename="I0002.dcm"
   Content-ID: "<dicomfileset1.se0001.i0002@provider.org>"
   Content-Description: B&W image

   AAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAA
   AAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAA
   AAAAAAAAAAAAAAAAAABESUNNAgAAAFVMBACmAAAAAgABAE9CAAACAAAAAQACAAIAVUkaADEuMi44
   NDAuMTAwMDguNS4xLjQuMS4xLjcAAgADAFVJHAAxLjIuMjUwLjEuNTkuMTIzLjQ1Ni43ODkuMS4y
   AgAQAFVJFAAxLjIuODQwLjEwMDA4LjEuMi4xAAIAEgBVSRgAMS4yLjI1MC4xLjU5LjIuNDMuODYu
   MjQzAgATAFNIDgBBQ1EtRVRJQU0tMi40MwgAAABVTAQAxAAAAAgABQBDUwoASVNPX0lSIDEwMAgA
   FgBVSRoAMS4yLjg0MC4xMDAwOC41LjEuNC4xLjEuNwAIABgAVUkcADEuMi4yNTAuMS41OS4xMjMu
   NDU2Ljc4OS4xLjIIACAAREEIADIwMDIwMzA4CAAwAFRNBgAwNzQ3NDAIAFAAU0gIAERJQ09NMzAA
   CABgAENTAgBPVAgAZABDUwQAV1NEAAgAkABQTgAACAAwEExPGABESUNPTSBNSU1FIHR5cGUgZXhh
   bXBsZQAQAAAAVUwEADwAAAAQABAAUE4KAERJQ09NXk5lbWEQACAATE8IAERJQ09NMzAAEAAwAERB
   CAAxOTkzMDEwMRAAQABDUwIATQAgAAAAVUwEAF4AAAAgAA0AVUkYADEuMi4yNTAuMS41OS4xMjMu
   NDU2Ljc4OSAADgBVSRoAMS4yLjI1MC4xLjU5LjEyMy40NTYuNzg5LjEgABAAU0gAACAAEQBJUwIA
   MQAgABMASVMCADIAKAAAAFVMBABkAAAAKAACAFVTAgABACgABABDUwwATU9OT0NIUk9NRTIAKAAI
   AElTAgAxACgAEABVUwIADwAoABEAVVMCADMAKAAAAVVTAgAIACgAAQFVUwIACAAoAAIBVVMCAAcA
   KAADAVVTAgAAAOB/AABVTAQACgMAAOB/EABPQgAA/gIAAP/////98dPX5O//////////////////
   /////////////////////////////////////////dCcjY2OnqW1yufa2tra6f///+Xa3f///+W5
   uc/2///xwLnn////+d7/////5Nfx///6oX53blKghHl6h5J8N72mT2Lo/+sktv/7fX/Mx3as/6l0
   0rhIgfz/51r////0Wdfn//+2WiM7YZFoJyMjIzt9V///92VX/f8k1P+ZWv3///rF0Tn4///hL6r/
   zSTP//+nJPj///uScylco6MwQCgmI2+hS/v//80j4f8k1P9ImP//////gnH/////aWD/rkJr//lp
   I9z///aOjHVqqZIoJGOSh7GrV/b//+Ujzv8k1P8/mP//////ZXT/////gUr/hLMl27KuPsP///+i
   jZQ4RLSiI5rFy7V+Uv3//9wq9f8k1P9VdP//////j0T9////boD/cvdreXH8WKT////kkI1sP9LH
   T7Xk6HQlRP///YaL//8k0v/AKbv///nQ4yux///wQtj/YP/PJqH/gIH/////5qB1g7O9vcbb291q
   QYmbgJz9/+A+ofb/vlZwf1/V/89adp93yv/dYOz/fvT/m2Pg//////vTppydq8Pa8/////j3////
   ///////////59/r/////+Pj/////////////////////////////////////////////////////
   ///////////////////////////////////JwdnRz9vQy9Xh3N3VzODx0drez8/k38/czNji0NXd
   2MrX2t/j2NH/u8DbxsfeyNnY//nPzcHRyMvi1cbUwLvXyrnzxs/K4tvd2sjN0sbLzsbayMHH0dLi
   08fz0dHNwsbc0cjg/////+79/////////PD//+79////////////////////////////////////
   ////////////////////////////////////////////////////////////////////////////
   /wA=

   ------=_NextPart_000_0062_01C1C786.EA262CC1_13487--
   ------=_NextPart_000_0062_01C1C786.EA262CC0--

