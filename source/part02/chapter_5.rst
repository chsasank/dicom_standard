.. _chapter_5:

Conventions
===========

.. _sect_5.1:

Application Data Flow Diagram
-----------------------------

In a Conformance Statement, the relationships between Real-World
Activities and Application Entities are illustrated by an Application
Data Flow Diagram.

.. _sect_5.1.1:

Application Entity
~~~~~~~~~~~~~~~~~~

An Application Entity is depicted as a box in an Application Data Flow
Diagram, shown in `figure_title <#figure_5.1-1>`__

.. _sect_5.1.2:

Real-World Activity
~~~~~~~~~~~~~~~~~~~

A Real-World Activity is depicted as a circle in an Application Data
Flow Diagram, shown in `figure_title <#figure_5.1-2>`__.

Circles representing multiple Real-World Activities may overlap,
indicating a degree of overlap in the Real-World Activities.

.. _sect_5.1.3:

Local Relationships
~~~~~~~~~~~~~~~~~~~

A relationship between a local Real-World Activity and an Application
Entity is depicted within an Application Data Flow Diagram by placing
the local Real-World Activity to the left of the related Application
Entity with a dashed line between them as shown in
`figure_title <#figure_5.1-3>`__.

An Application Entity may be associated with multiple Real-World
Activities.

A Real-World Activity may be associated with multiple Application
Entities.

.. _sect_5.1.4:

Network-Associations
~~~~~~~~~~~~~~~~~~~~

An association between a local Application Entity and a remote
Application Entity over a network supporting a remote Real-World
Activity is depicted within an Application Data Flow Diagram by placing
the remote Real-World Activity to the right of the related local
Application Entity with one or two arrows drawn between them as shown in
`figure_title <#figure_5.1-4>`__. The dashed line represents the DICOM
Standard Interface between the local Application Entities, and whatever
remote Application Entities that handle the remote Real-World
Activities. An arrow from the local Application Entity to the remote
Real-World Activity indicates that an occurrence of the local Real-World
Activity will cause the local Application Entity to initiate an
association for the purpose of causing the remote Real-World Activity to
occur. An arrow from the remote Real-World Activity to the local
Application Entity indicates that the local Application Entity expects
to receive an association request when the remote Real-World Activity
occurs, causing the local Application Entity to perform the local
Real-World Activity.

.. _sect_5.1.5:

Media Storage File-Set Access
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

Application Entities exchanging information on media use the DICOM File
Service as specified in for access to, or creation of, File-sets. This
File Service provides operations that support three basic roles, which
are File-set Creator (FSC), File-set Reader (FSR), and File-set Updater
(FSU).

These roles are depicted on an Application Data Flow diagram by
directional arrows placed between the local Application Entities and the
DICOM Storage Media on which the roles are applied.

-  File-set Creator (FSC), denoted by |image1|

-  File-set Reader (FSR), denoted by |image2|

-  File-set Updater (FSU), denoted by |image3|

-  Physical movement of the medium, denoted by |image4| (with or without
   arrowhead)

`figure_title <#figure_5.1-5>`__ illustrates the three basic roles.

The local interactions shown on the left between a local Real-World
activity and a local Application Entity are depicted by a dashed line.
The arrows on the right represent access by the local Application Entity
to a File-set on the DICOM Storage Medium. When an Application Entity
supports several roles, this combination is depicted with multiple
arrows corresponding to each of the roles. The dotted arrow symbolizes
the removable nature of media for an interchange application.

.. note::

   The use of two arrows relative to an FSC and an FSR should be
   distinguished from the case where a double arrow relative to an FSU
   is used. For example, an FSU may update a File-set without creating a
   new File-set, whereas a combined FSC and FSR may be used to create
   and verify a File-set.

