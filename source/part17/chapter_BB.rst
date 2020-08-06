.. _chapter_BB:

Printing (Informative)
======================

.. _sect_BB.1:

Example of Print Management SCU Session (Informative)
-----------------------------------------------------

.. _sect_BB.1.1:

Simple Example
~~~~~~~~~~~~~~

This example of a Print Management SCU Session is provided for
informational purposes only. It illustrates the use of one of the Basic
Print Management Meta SOP Classes.

``A-ASSOCIATE``

``N-GET (PRINTER SOP Instance)``

``N-CREATE (Film Session SOP Instance)``

``for (each film of film session)``

``{``

-  ``N-CREATE (Film Box SOP Instance)``

-  ``for (each image of film)``

-  ``{``

   -  ``N-SET (Image Box SOP Instance that encapsulates a PREFORMATTED IMAGE SOP Instance)``

   ``}``

-  ``if (no collation)``

-  ``{``

   -  ``N-ACTION (PRINT, Film Box SOP Instance)``

   -  ``N-DELETE (Film Box SOP Instance)``

   ``}``

``}``

``if (collation)``

``{``

-  ``N-ACTION (PRINT, Film Session SOP Instance)``

-  ``N-DELETE (Film Session SOP Instance)``

``}``

``N-EVENT-REPORT (PRINTER SOP Instance)``

``A-RELEASE``

.. _sect_BB.1.2:

Advanced Example (Retired)
~~~~~~~~~~~~~~~~~~~~~~~~~~

This section was previously defined in DICOM. It is now retired. See
PS3.4-1998.

