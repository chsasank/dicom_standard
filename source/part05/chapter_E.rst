.. _chapter_E:

DICOM Default Character Repertoire (Normative)
==============================================

The default repertoire for character strings in DICOM is the Basic G0
Set of the International Reference Version of ISO 646:1990 (ISO IR-6).
In addition, the Control Characters LF, FF, CR, TAB and ESC are
supported. These control characters are a subset of the C0 set defined
in ISO 646:1990 and ISO 6429:1990.

The byte encoding of the Default Character Repertoire is pictured in
Table E-1. This table can be used to derive both ISO column/row byte
values and hex values for encoded representations (see `Representation
of Encoded Character Values <#sect_6.1.1>`__).

.. table:: DICOM Default Character Repertoire Encoding

   == = = = == =========== === === == = = == == ==
   \           b\ :sub:`8` 0   0   0  0 0 0  0  0
   == = = = == =========== === === == = = == == ==
   0  0 0 0 00                     SP 0 @ P  \` p
   0  0 0 1 01                     !  1 A Q  a  q
   0  0 1 0 02                     "  2 B R  b  r
   0  0 1 1 03                     #  3 C S  c  s
   0  1 0 0 04                     $  4 D T  d  t
   0  1 0 1 05                     %  5 E U  e  u
   0  1 1 0 06                     &  6 F V  f  v
   0  1 1 1 07                     '  7 G W  g  w
   1  0 0 0 08                     (  8 H X  h  x
   1  0 0 1 09             TAB     )  9 I Y  i  y
   1  0 1 0 10             LF      \* : J Z  j  z
   1  0 1 1 11                 ESC +  ; K [  k  {
   1  1 0 0 12             FF      ,  < L \\ l  \|
   1  1 0 1 13             CR      -  = M ]  m  }
   1  1 1 0 14                     .  > N ^  n  ~
   1  1 1 1 15                     /  ? O \_ o  
   == = = = == =========== === === == = = == == ==

