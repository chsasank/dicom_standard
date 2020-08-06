.. _chapter_B:

Examples (Informative)
======================

.. _sect_B.1:

Retrieving a Simple DICOM Image in JPEG
---------------------------------------

::

   http://www.hospital-stmarco/radiology/wado.php?requestType=WADO
     &studyUID=1.2.250.1.59.40211.12345678.678910
     &seriesUID=1.2.250.1.59.40211.789001276.14556172.67789
     &objectUID=1.2.250.1.59.40211.2678810.87991027.899772.2

.. _sect_B.2:

Retrieving a DICOM SR in HTML
-----------------------------

::

   http://server234/script678.asp?requestType=WADO
     &studyUID=1.2.250.1.59.40211.12345678.678910
     &seriesUID=1.2.250.1.59.40211.789001276.14556172.67789
     &objectUID=1.2.250.1.59.40211.2678810.87991027.899772.2
     &charset=UTF-8

.. _sect_B.3:

Retrieving a Region of A DICOM Image
------------------------------------

Retrieving a region of a DICOM image, converted if possible in JPEG2000,
with annotations burned into the image containing the patient name and
technical information, and mapped into a defined image size:

::

   https://aspradio/imageaccess.js?requestType=WADO
     &studyUID=1.2.250.1.59.40211.12345678.678910
     &seriesUID=1.2.250.1.59.40211.789001276.14556172.67789
     &objectUID=1.2.250.1.59.40211.2678810.87991027.899772.2
     &contentType=image%2Fjp2;level=1,image%2Fjpeg;q=0.5
     &annotation=patient,technique
     &columns=400
     &rows=300
     &region=0.3,0.4,0.5,0.5
     &windowCenter=-1000
     &windowWidth=2500

.. _sect_B.4:

Retrieving As A DICOM Media Type
--------------------------------

Retrieving a DICOM image object using the baseline 8-bit lossy JPEG
transfer syntax, and de-identified:

::

   http://www.medical-webservice.st/RetrieveDocument?requestType=WADO
     &studyUID=1.2.250.1.59.40211.12345678.678910
     &seriesUID=1.2.250.1.59.40211.789001276.14556172.67789
     &objectUID=1.2.250.1.59.40211.2678810.87991027.899772.2
     &contentType=application%2Fdicom
     &anonymize=yes
     &transferSyntax=1.2.840.10008.1.2.4.50

