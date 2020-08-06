.. _chapter_10:

Conformance
===========

.. _sect_10.1:

Conformance Requirements
------------------------

.. _sect_10.1.1:

Retired
~~~~~~~

.. _sect_10.1.2:

TCP/IP Network Communication Support
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

An implementation claiming conformance to *DICOM TCP/IP Network
Communication Support*\ shall:

a. Meet the DICOM Upper Layers Protocol requirements as defined in
   Section 9.

b. Use registered Application Context Names, Abstract Syntax Names and
   Transfer Syntax Names as defined for OSI Object Identifiers (ISO 8824
   and ISO 9834-1).

   .. note::

      `DICOM UL Encoding Rules for Application Contexts, Abstract
      Syntaxes, Transfer Syntaxes (Normative) <#chapter_F>`__ defines
      the DICOM Upper Layer Protocol encoding for the Application
      Context Names, Abstract Syntax Names, and Transfer Syntax Names.
      ISO 8825 defined encoding is not used.

c. Use one of the published and approved RFCs defining the operation of
   TCP/IP over specific physical networks.

.. _sect_10.2:

Conformance Statement
---------------------

An implementation claiming conformance to DICOM for communication
support in a networked environment shall state DICOM V3.0 TCP/IP Network
Communication Support with the list of physical networks and
corresponding relevant implementation information. This implies that the
conformance requirements defined in `TCP/IP Network Communication
Support <#sect_10.1.2>`__ are met.

