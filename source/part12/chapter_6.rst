.. _chapter_6:

Relationship to the DICOM Media Storage Model
=============================================

defines various media storage concepts. The implementation of these
generic concepts on a specific medium and file system is defined in an
annex. For each physical medium and file system a mapping is described
between these media storage concepts and the specific physical media and
file system facilities:

a. File-set ID - The method for providing a File-set ID

b. File ID - The method for mapping a DICOM File ID into a specific file
   system

c. File creation/update date and time - The specific file system
   mechanisms used to provide this information

d. File-set location

Processing of DICOM removable media requires that the DICOMDIR be in a
known location. Most file systems provide a hierarchical directory
structure with a root directory for an entire medium or medium
partition. The annex defines where the DICOMDIR(s) are located. When
only one File-set is permitted on one medium, the DICOMDIR shall be in
the root directory of that medium. When multiple File-sets are permitted
on a single medium, the annex will describe how File-sets are found and
identified. When a File-set is permitted to span multiple pieces of
physical media, the appropriate annex will describe how this is managed.

`figure_title <#figure_6-1>`__ illustrates the structure of a DICOM
removable medium that supports a single DICOM File-set per medium
partition. `figure_title <#figure_6-2>`__ illustrates the structure of a
DICOM medium that supports multiple File-sets per partition. DICOM
File-sets shall not intersect when media permit multiple File-sets.

Media and file systems that do not utilize the directory concept will
specify the equivalent usage in these annexes that describe these media.

.. note::

   Many applications will need to automatically create many image files
   and assign them unique File IDs. Maintaining File ID uniqueness
   without sacrificing performance will require some care. The approach
   of taking a basic name part, e.g., "IMAGE," and appending sequence
   numbers, e.g., "IMAGE001, IMAGE002, ..." can easily result in delays
   finding the next available File ID.

Some approaches that can rapidly generate unique File IDs include:

a. Generating a unique sub-directory per sequence, then using increasing
   file numbering within the sub-directory

b. Using a random number generator and seed, then using a prime hash
   function with probes to find unused file names. An eight character
   File ID component permits a large prime value for the hash

c. Using the current time (in seconds, milliseconds) as a pseudo-random
   number to generate one of the File ID components, and resolving
   collisions with sequential or prime hash probes

All of these approaches result in File IDs that are of limited semantic
content. The semantic information that describes file contents is in the
DICOMDIR and the file contents to which it points.

