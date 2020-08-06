.. _chapter_G:

Overview of the OSI Layer and Services Concepts (Informative)
=============================================================

In a layered communication model, such as the OSI 7 layer reference
model, each layer uses the service provided by the layer immediately
below. The operation of a protocol layer on top of the lower layer
service provides a new service to the layer above. The service is the
"glue" between the layers of protocols.

Services describe the resulting effects of the operation of a protocol
without requiring knowledge of the detailed specifications of the
protocol itself. A protocol specifies a horizontal dialogue between two
computing systems across a network, while a service describes a vertical
relationship within a system. See `figure_title <#figure_G-1>`__.

.. figure:: figures/PS3.8_G-1.svg
   :alt: Relationship of Services to Protocol
   :name: figure_G-1

   Relationship of Services to Protocol

The OSI Upper Layer Service is described by a number of service
primitives. They each model one of the functional interactions between
the service-user in the layer above and the service-provider. In the
context of this Standard, the service-user is called the DICOM
Application Service Element. The service-provider is called the Upper
Layer and performs the Upper Layer Protocol.

.. note::

   The OSI UL Services defined in this Standard are provided by the
   DICOM Upper Layer Protocol for TCP/IP (Section 9).

These service primitives cross the layer boundary at what is called a
Service Access Point (SAP). In most cases a direct relationship exists
between service primitives in two Application Entities (AEs). This is
reflected in the names of these primitives:

a. A request primitive in System A induces an indication primitive in
   System B.

b. If an indication primitive in System B requires a reply, a response
   primitive may be issued at the Service Access Point (SAP) in System
   B. This response primitive will induce a confirmation primitive in
   System A.

The different types of service primitives and their relationship are
shown in `figure_title <#figure_G-2>`__. The dotted lines represent the
exchange of Protocol Data Units that are triggered by request/response
primitives or generated indication/confirmation primitives.

