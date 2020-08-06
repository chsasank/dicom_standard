.. _chapter_M:

Conformance Statement Sample DICOM-RTV Service Consumer (Informative)
=====================================================================

Disclaimer:

This document is an example DICOM Conformance Statement for a fictional
application service called EXAMPLE-RTV-DISPLAY produced by a fictional
vendor called EXAMPLE-Viewing Â­PRODUCTS.

As stated in the annex title, this document is truly informative, and
not normative. A conformance statement of an actual product might
implement additional services and options as appropriate for its
specific purpose. In addition, an actual product might implement the
services described in a different manner and, for example, with
different characteristics and/or sequencing of activities. In other
words, this conformance statement example does not intend to standardize
a particular manner that a product might implement DICOM-RTV
functionality.

.. _sect_M.0:

Cover Page
----------

Company Name: EXAMPLE-Viewing Â­PRODUCTS

Product Name: EXAMPLE-RTV-DISPLAY

Version: 1.0-rev. A.1

Internal document number: 1024-1960-xx-yy-zz rev 1

Date: YYYYMMDD

.. _sect_M.1:

Conformance Statement Overview
------------------------------

This fictional product EXAMPLE-RTV-DISPLAY implements the DICOM-RTV
services for consuming video, audio and associated metadata, provided by
another compliant device, and displaying the information in a window on
the screen. The EXAMPLE-RTV-DISPLAY is only available as a plug in
option for the EXAMPLE-INTEGRATED-MODALITY. All of the networking,
database, and other services are provided by the "SAMPLE DICOM Image
Viewer". This conformance claim refers to the conformance claim for the
"SAMPLE DICOM Image Viewer" for all such services.

`table_title <#table_M.1-1>`__ provides an overview of the network
services supported by EXAMPLE-RTV-DISPLAY.

.. table:: Network Services

   +----------------------+----------------------+----------------------+
   | **Network Service**  | **User of Service    | **Provider of        |
   |                      | (SCU)**              | Service (SCP)**      |
   +======================+======================+======================+
   | **DICOM Real-Time    |                      |                      |
   | Video (DICOM-RTV)**  |                      |                      |
   +----------------------+----------------------+----------------------+
   | DICOM-RTV            | Yes                  | No                   |
   +----------------------+----------------------+----------------------+

.. _sect_M.2:

Table of Contents
-----------------

A table of contents shall be provided to assist readers in easily
finding the needed information.

.. _sect_M.3:

Introduction
------------

.. _sect_M.3.1:

Revision History
~~~~~~~~~~~~~~~~

.. table:: Revision History

   +-----------------+-----------------+------------+-----------------+
   | **Document      | **Date of       | **Author** | **Description** |
   | Version**       | Issue**         |            |                 |
   +=================+=================+============+=================+
   | 1.1             | March 8         | ECR        | Initial version |
   |                 | :sup:`th`, 2018 |            | for PC          |
   +-----------------+-----------------+------------+-----------------+

.. _sect_M.3.2:

Audience, Remarks, Terms and Definitions, Basics of DICOM Communication, Abbreviations, References
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

*See example text in*\ `Introduction <#sect_A.3>`__\ *.*

.. _sect_M.3.3:

Additional Remarks for This Example
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

This document is a sample DICOM Conformance Statement created for DICOM
. It is to be used solely as an example to illustrate how to create a
DICOM Conformance Statement for a DICOM-RTV Service Provider. The
subject of the document, EXAMPLE-RTV-SERVICE, is a fictional product.

.. _sect_M.4:

Networking
----------

.. _sect_M.4.1:

Implementation Model
~~~~~~~~~~~~~~~~~~~~

.. _sect_M.4.1.1:

Application Data Flow
^^^^^^^^^^^^^^^^^^^^^

.. figure:: part02_fromword_files/image018_sup202.png
   :alt: Application Data Flow Diagram
   :name: figure_M.4.1-1

   Application Data Flow Diagram

The DICOM-RTV Service Application consumes one or multiple DICOM-RTV
compliant Flows, transported in RTP over IP, that is/are provided by one
other DICOM-RTV Service Application.

.. _sect_M.4.1.2:

Functional Definition of AEs
^^^^^^^^^^^^^^^^^^^^^^^^^^^^

.. _sect_M.4.1.2.1:

Functional Definition of RTV Service Application
''''''''''''''''''''''''''''''''''''''''''''''''

The DICOM-RTV Service is Active when the real-time display feature of
the equipment is running and some video and/or audio content is
provided.

.. _sect_M.4.2:

AE Specifications
~~~~~~~~~~~~~~~~~

This AE complies with , specification for DICOM-RTV.

.. _sect_M.4.2.1:

DICOM-RTV Application Entity Specifications
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

.. _sect_M.4.2.1.1:

SOP Classes
'''''''''''

EXAMPLE-RTV-SERVICE provides Standard Conformance to the following SOP
Classes:

.. table:: SOP Classes for DICOM-RTV AE

   +-----------------------+--------------------+---------+---------+
   | **SOP Class Name**    | **SOP Class UID**  | **SCU** | **SCP** |
   +=======================+====================+=========+=========+
   | Video Photographic    | 1.2.840.10008.10.2 | Yes     | No      |
   | Image Real-Time       |                    |         |         |
   | Communication         |                    |         |         |
   +-----------------------+--------------------+---------+---------+
   | Audio Waveform        | 1.2.840.10008.10.3 | Yes     | No      |
   | Real-Time             |                    |         |         |
   | Communication         |                    |         |         |
   +-----------------------+--------------------+---------+---------+
   | Rendition Selection   | 1.2.840.10008.10.4 | Yes     | No      |
   | Document Real-Time    |                    |         |         |
   | Communication         |                    |         |         |
   +-----------------------+--------------------+---------+---------+

Some restrictions applies on the Real-Time Communications:

.. table:: DICOM-RTV Instances Specification

   +-----------------------------+---------------------------------------+
   | **Category**                | **Restrictions**                      |
   +=============================+=======================================+
   | Transfer Syntaxes Supported | SMPTE ST 2110-20 Uncompressed         |
   |                             | Progressive Active Video, SMPTE ST    |
   |                             | 2110-30 PCM Digital Audio             |
   +-----------------------------+---------------------------------------+
   | Photometric interpretation  | RGB                                   |
   +-----------------------------+---------------------------------------+
   | Bit depth (video)           | 10                                    |
   +-----------------------------+---------------------------------------+
   | Number of Waveform Channels | 2                                     |
   +-----------------------------+---------------------------------------+
   | Bit depth (audio)           | 16 (signed 16-bits linear)            |
   +-----------------------------+---------------------------------------+
   | Sampling Frequency          | 48 kHz                                |
   +-----------------------------+---------------------------------------+

.. table:: DICOM-RTV Screen Resolutions

   +----------+-------------+-------------+-------------+-------------+
   | **Rows** | **Columns** | **Frame     | **Video     | **          |
   |          |             | rate**      | Type**      | Progressive |
   |          |             |             |             | or          |
   |          |             |             |             | I           |
   |          |             |             |             | nterlaced** |
   +==========+=============+=============+=============+=============+
   | 1080     | 1920        | 25          | 25 Hz HD    | P           |
   +----------+-------------+-------------+-------------+-------------+
   | 1080     | 1920        | 29.97, 30   | 30 Hz HD    | P           |
   +----------+-------------+-------------+-------------+-------------+
   | 1080     | 1920        | 25          | 25 Hz HD    | I           |
   +----------+-------------+-------------+-------------+-------------+
   | 1080     | 1920        | 29.97, 30   | 30 Hz HD    | I           |
   +----------+-------------+-------------+-------------+-------------+
   | 720      | 1280        | 25          | 25 Hz HD    | P           |
   +----------+-------------+-------------+-------------+-------------+
   | 720      | 1280        | 29.97, 30   | 30 Hz HD    | P           |
   +----------+-------------+-------------+-------------+-------------+
   | 720      | 1280        | 50          | 50 Hz HD    | P           |
   +----------+-------------+-------------+-------------+-------------+
   | 720      | 1280        | 59.94, 60   | 60 Hz HD    | P           |
   +----------+-------------+-------------+-------------+-------------+

The resolution is automatically determined based on the one provided by
the sent video.

.. _sect_M.4.2.1.2:

Connection Policies
'''''''''''''''''''

.. _sect_M.4.2.1.2.1:

General
       

The URL to be accessed by the equipment to get the SDP object is set by
configuration.

.. _sect_ML.4.2.1.2.2:

Number of Connections
                     

EXAMPLE-RTV-DISPLAY is consuming multicast communication.

.. _sect_M.4.3:

Network Interfaces
~~~~~~~~~~~~~~~~~~

.. _sect_M.4.3.1:

Physical Network Interface
^^^^^^^^^^^^^^^^^^^^^^^^^^

**M.4.3.1 Physical Network Interface**

EXAMPLE-RTV-DISPLAY uses the network interface from the hosting "SAMPLE
DICOM Image Viewer". See its conformance claim for details.

.. _sect_M.4.3.2:

Additional Protocols
^^^^^^^^^^^^^^^^^^^^

EXAMPLE-RTV-DISPLAY uses the network services from the hosting "SAMPLE
DICOM Image Viewer". See its conformance claim for details.

.. _sect_M.4.3.3:

IPv4 and IPv6 Support
^^^^^^^^^^^^^^^^^^^^^

This product supports both IPv4 and IPv6 connections.

.. _sect_M.4.4:

Configuration
-------------

.. _sect_M.4.4.1:

DICOM-RTV Interface
~~~~~~~~~~~~~~~~~~~

The EXAMPLE-RTV-DISPLAY uses the network parameters (IP, portâ€¦)
defined in the SDP.

.. _sect_M.5:

Media Interchange
-----------------

Not applicable.

.. _sect_M.6:

Support of Character Sets
-------------------------

EXAMPLE-RTV-DISPLAY supports only Unicode UTF-8 for all communications.

.. _sect_M.7:

Security
--------

Has to be managed at the individual sites and installations.

.. _sect_M.8:

Annexes
-------

.. _sect_M.8.1:

IOD Contents
~~~~~~~~~~~~

Not Applicable.

.. _sect_M.8.2:

Data Dictionary of Private Attributes
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

No private Attributes are used.

.. _sect_M.8.3:

Coded Terminology and Templates
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

Not Applicable.

.. _sect_M.8.4:

Standard Extended / Specialized / Private SOP Classes
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

Not Applicable.

.. _sect_M.8.5:

Private Transfer Syntaxes
~~~~~~~~~~~~~~~~~~~~~~~~~

Private transfer syntaxes are not supported.

.. |image1| image:: figures/PS3.2_5.1-5A.svg
.. |image2| image:: figures/PS3.2_5.1-5B.svg
.. |image3| image:: figures/PS3.2_5.1-5C.svg
.. |image4| image:: figures/PS3.2_5.1-5D.svg
