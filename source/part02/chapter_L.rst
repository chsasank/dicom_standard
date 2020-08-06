.. _chapter_L:

Conformance Statement Sample DICOM-RTV Service Provider (Informative)
=====================================================================

Disclaimer:

This document is an example DICOM Conformance Statement for a fictional
application service called EXAMPLE-RTV-SERVICE produced by a fictional
vendor called EXAMPLE-IMAGING-PRODUCTS.

As stated in the annex title, this document is truly informative, and
not normative. A conformance statement of an actual product might
implement additional services and options as appropriate for its
specific purpose. In addition, an actual product might implement the
services described in a different manner and, for example, with
different characteristics and/or sequencing of activities. In other
words, this conformance statement example does not intend to standardize
a particular manner that a product might implement DICOM-RTV
functionality.

.. _sect_L.0:

Cover Page
----------

Company Name: EXAMPLE-IMAGING-PRODUCTS

Product Name: EXAMPLE-RTV-SERVICE

Version: 1.0-rev. A.1

Internal document number: 1024-1960-xx-yy-zz rev 1

Date: YYYYMMDD

.. _sect_L.1:

Conformance Statement Overview
------------------------------

This fictional product EXAMPLE-RTV-SERVICE implements the DICOM-RTV
services for sending video and associated metadata, to be consumed in
real-time by other compliant devices. The EXAMPLE-RTV-SERVICE is only
available as a plug in option for the EXAMPLE-INTEGRATED-MODALITY. All
of the networking, database, and other services are provided by the
EXAMPLE-INTEGRATED-MODALITY. This conformance claim refers to the
conformance claim for the EXAMPLE-INTEGRATED-MODALITY for all such
services.

`table_title <#table_L.1-1>`__ provides an overview of the network
services supported by EXAMPLE-RTV-SERVICE.

.. table:: Network Services

   +----------------------+----------------------+----------------------+
   | **Network Service**  | **User of Service    | **Provider of        |
   |                      | (SCU)**              | Service (SCP)**      |
   +======================+======================+======================+
   | DICOM Real-Time      |                      |                      |
   | Video (DICOM-RTV)    |                      |                      |
   +----------------------+----------------------+----------------------+
   | DICOM-RTV            | No                   | Yes                  |
   +----------------------+----------------------+----------------------+

.. _sect_L.2:

Table of Contents
-----------------

A table of contents shall be provided to assist readers in easily
finding the needed information.

.. _sect_L.3:

Introduction
------------

.. _sect_L.3.1:

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

.. _sect_L.3.2:

Audience, Remarks, Terms and Definitions, Basics of DICOM Communication, Abbreviations, References
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

*See example text in*\ `Introduction <#sect_A.3>`__\ *.*

.. _sect_L.3.3:

Additional Remarks for This Example
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

This document is a sample DICOM Conformance Statement created for DICOM
. It is to be used solely as an example to illustrate how to create a
DICOM Conformance Statement for a DICOM-RTV Service Provider. The
subject of the document, EXAMPLE-RTV-SERVICE, is a fictional product.

.. _sect_L.4:

Networking
----------

.. _sect_L.4.1:

Implementation Model
~~~~~~~~~~~~~~~~~~~~

.. _sect_L.4.1.1:

Application Data Flow
^^^^^^^^^^^^^^^^^^^^^

.. figure:: part02_fromword_files/image017_sup202.png
   :alt: Application Data Flow Diagram
   :name: figure_L.4.1-1

   Application Data Flow Diagram

The DICOM-RTV Service Application provides multiple DICOM-RTV compliant
Flows, transported in RTP over IP, that can be consumed by one or
multiple other DICOM-RTV Service Application(s).

.. _sect_L.4.1.2:

Functional Definition of AEs
^^^^^^^^^^^^^^^^^^^^^^^^^^^^

.. _sect_L.4.1.2.1:

Functional Definition of RTV Service Application
''''''''''''''''''''''''''''''''''''''''''''''''

The DICOM-RTV Service is Active when the equipment produces video
content.

.. _sect_L.4.2:

AE Specifications
~~~~~~~~~~~~~~~~~

This AE complies with , specification for DICOM-RTV.

.. _sect_L.4.2.1:

DICOM-RTV Application Entity Specifications
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

.. _sect_L.4.2.1.1:

SOP Classes
'''''''''''

EXAMPLE-RTV-SERVICE provides Standard Conformance to the following SOP
Classes:

.. table:: SOP Classes for DICOM-RTV AE

   +-----------------------+--------------------+---------+---------+
   | **SOP Class Name**    | **SOP Class UID**  | **SCU** | **SCP** |
   +=======================+====================+=========+=========+
   | Video Photographic    | 1.2.840.10008.10.2 | No      | Yes     |
   | Image Real-Time       |                    |         |         |
   | Communication         |                    |         |         |
   +-----------------------+--------------------+---------+---------+

Some restrictions applies on the Real-Time Communications:

.. table:: DICOM-RTV Instances Specification

   +-----------------------------+---------------------------------------+
   | **Category**                | **Restrictions**                      |
   +=============================+=======================================+
   | Transfer Syntaxes Supported | SMPTE ST 2110-20 Uncompressed         |
   |                             | Progressive Active Video              |
   +-----------------------------+---------------------------------------+
   | Photometric interpretation  | RGB                                   |
   +-----------------------------+---------------------------------------+
   | Bit depth                   | 10                                    |
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

The resolution is defined by the equipment configuration, and is
reflected in the SDP object.

.. _sect_L.4.2.1.2:

Connection Policies
'''''''''''''''''''

.. _sect_L.4.2.1.2.1:

General
       

The consumer shall get the SDP object on the following URL:
http://<local-IP-address-of-the-device>/SDP.

.. _sect_L.4.2.1.2.2:

Number of Connections
                     

**L.4.2.1.2.2**

EXAMPLE-RTV-SERVICE is provided in multicast. The limit of simultaneous
connection depends on the local network infrastructure.

.. _sect_L.4.3:

Network Interfaces
~~~~~~~~~~~~~~~~~~

.. _sect_L.4.3.1:

Physical Network Interface
^^^^^^^^^^^^^^^^^^^^^^^^^^

EXAMPLE-RTV-SERVICE uses the network interface from the hosting
EXAMPLE-INTEGRATED-MODALITY. See its conformance claim for details.

.. _sect_L.4.3.2:

Additional Protocols
^^^^^^^^^^^^^^^^^^^^

EXAMPLE-RTV-SERVICE uses the network services from the hosting
EXAMPLE-INTEGRATED-MODALITY. See its conformance claim for details.

.. _sect_L.4.3.3:

IPv4 and IPv6 Support
^^^^^^^^^^^^^^^^^^^^^

This product supports both IPv4 and IPv6 connections.

.. _sect_L.4.4:

Configuration
-------------

.. _sect_L.4.4.1:

DICOM-RTV Interface
~~~~~~~~~~~~~~~~~~~

The EXAMPLE-RTV-SERVICE is configured to define the following parameters
expressed in the SDP object:

-  the RTP payload type (PT) used for the video is 96

-  the RTP payload type (PT) used for DICOM-RTV Metadata is 104.

.. _sect_L.5:

Media Interchange
-----------------

Not applicable.

.. _sect_L.6:

Support of Character Sets
-------------------------

All EXAMPLE-RTV-SERVICEs support Unicode UTF-8 for all communications.

.. _sect_L.7:

Security
--------

Has to be managed at the individual sites and installations.

.. _sect_L.8:

Annexes
-------

.. _sect_L.8.1:

IOD Contents
~~~~~~~~~~~~

See conformance claim for the EXAMPLE-INTEGRATED-MODALITY. The modules
and fields contained in the DICOM-RTV metadata are reflecting the values
of the corresponding ones in the EXAMPLE-INTEGRATED-MODALITY X-Ray
Radiofluoroscopic Image Storage IOD.

.. _sect_L.8.2:

Data Dictionary of Private Attributes
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

No private Attributes are used.

.. _sect_L.8.3:

Coded Terminology and Templates
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

See conformance claim for EXAMPLE-INTEGRATED-MODALITY.

.. _sect_L.8.4:

Standard Extended / Specialized / Private SOP Classes
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

Not Applicable.

.. _sect_L.8.5:

Private Transfer Syntaxes
~~~~~~~~~~~~~~~~~~~~~~~~~

Private transfer syntaxes are not supported.

