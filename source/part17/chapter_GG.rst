.. _chapter_GG:

JPIP Referenced Pixel Data Transfer Syntax Negotiation (Informative)
====================================================================

The JPIP Referenced Pixel Data transfer syntaxes allow transfer of image
objects with a reference to a non-DICOM network service that provides
the pixel data rather than encoding the pixel data in (7FE0,0010).

The use cases for this extension to the Standard relate to an
application's desire to gain access to a portion of DICOM pixel data
without the need to wait for reception of all the pixel data. Examples
are:

1. Stack Navigation of a large CT Study.

   In this case, it is desirable to quickly scroll through this large
   set of data at a lower resolution and once the anatomy of interest is
   located the full resolution data is presented. Initially lower
   resolution images are requested from the server for the purpose of
   stack navigation. Once a specific image is identified the system
   requests the rest of the detail from the server.

2. Large Single Image Navigation.

   In cases such as microscopy, very large images may be generated. It
   is undesirable to wait for the complete pixel data to be loaded when
   only a small portion of the specific image is of interest.
   Additionally, this large image may exceed the display capabilities
   thus resulting in a decimation of the image when displayed. A lower
   resolution image (i.e., one that matches the resolution of the
   display) is all that is required, as additional data cannot be fully
   rendered. Once an area of interest is determined, the application can
   pan and zoom to this area and request additional detail to fill the
   screen resolution.

3. Thumbnails.

   It is desirable to generate thumbnail representations for a study.
   This has been accomplished through various means, many of which
   require the client to receive the complete pixel data from the server
   to generate the thumbnail image. This uses significant network
   bandwidth.

   The thumbnails can be considered low-resolution representations of
   the image. The application can request a low-resolution
   representation of the image for use as a thumbnail.

4. Display by Dimension.

   Multi-frame Images may encode multiple dimensions. It is desirable
   for an application to access only the specific frames of interest in
   a particular dimension without the need to receive the complete pixel
   data. By using the multi-dimensional description, applications using
   the JPIP protocol may request frames of the Multi-frame Image.

The association negotiation between the initiator and acceptor controls
when this method of transfer is used. An acceptor can potentially accept
both the JPIP Referenced Pixel Data transfer syntax and a non-JPIP
transfer syntax on different presentation contexts. When an acceptor
accepts both of these transfer syntaxes, the initiator chooses the
presentation context.

Examples:

For the following cases:

-  AE1 requests images from AE2

-  AE1 implements a C-MOVE SCU, as well as a C-STORE SCP. AE2 implements
   a C-MOVE SCP, as well as a C-STORE SCU

Case 1:

-  AE1 and AE2 both support both a JPIP Referenced Pixel Data Transfer
   Syntax and a non-JPIP Transfer Syntax

-  AE1 makes a C-MOVE request to AE2

-  AE2 proposes two presentation contexts to AE1, one for with a JPIP
   Referenced Pixel Data Transfer Syntax, and the other with a non-JPIP
   Transfer Syntax

-  AE1 accepts both presentation contexts

-  AE2 may choose either presentation context to send the object

-  AE1 must be able to either receive the pixel data in the C-STORE
   message, or to be able to obtain it from the provider URL

Case 2:

-  AE1 supports only the JPIP Referenced Pixel Data Transfer Syntax

-  AE2 supports both a JPIP Referenced Pixel Data Transfer Syntax and a
   non-JPIP Transfer Syntax

-  AE1 makes a C-MOVE request to AE2

-  AE2 proposes to AE1 either

   -  two presentation contexts, one for with a JPIP Referenced Pixel
      Data Transfer Syntax, and the other with a non-JPIP Transfer
      Syntax, or

   -  a single presentation context with both a JPIP Referenced Pixel
      Data Transfer Syntax and a non-JPIP Transfer Syntax

-  AE1 accepts only the presentation context with the JPIP Referenced
   Pixel Data Transfer Syntax, or only the JPIP Referenced Pixel Data
   Transfer Syntax within the single presentation context proposed

-  AE2 sends the object with the JPIP Referenced Pixel Data Transfer
   Syntax

-  AE1 must be able to either retrieve the pixel data from the provider
   URL

For the following cases:

-  AE1 requests images from AE2

-  AE1 implements a C-GET SCU. AE2 implements a C-GET SCP

Case 3:

-  AE1 and AE2 both support both a JPIP Referenced Pixel Data Transfer
   Syntax and a non-JPIP Transfer Syntax

-  In addition to the C-GET presentation context, AE2 proposes to AE1
   two presentation contexts for storage sub-operations, one for with a
   JPIP Referenced Pixel Data Transfer Syntax, and the other with a
   non-JPIP Transfer Syntax

-  AE2 accepts both storage presentation contexts

-  AE1 makes a C-GET request to AE2

-  AE2 may choose either presentation context to send the object

-  AE1 must be able to either receive the pixel data in the C-STORE
   message, or to be able to obtain it from the provider URL

Case 4:

-  AE1 supports only the JPIP Referenced Pixel Data Transfer Syntax

-  AE2 supports both a JPIP Referenced Pixel Data Transfer Syntax and a
   non-JPIP Transfer Syntax

-  In addition to the C-GET presentation context, AE2 proposes to AE1 a
   single presentation context for storage sub-operations with a JPIP
   Referenced Pixel Data Transfer Syntax

-  AE2 accepts the storage presentation context

-  AE1 makes a C-GET request to AE2

-  AE2 sends the object with the JPIP Referenced Pixel Data Transfer
   Syntax

-  AE1 must be able to either retrieve the pixel data from the provider
   URL

