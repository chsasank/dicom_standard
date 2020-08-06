.. _chapter_5:

Conventions
===========

Words are capitalized in this document to help the reader understand
that these words have been previously defined in Section 3 of this
document and are to be interpreted with that meaning.

A Tag is represented as (gggg,eeee), where gggg equates to the Group
Number and eeee equates to the Element Number within that Group. Tags
are represented in hexadecimal notation as specified in .

Attributes of File Meta Information are assigned a Type that indicates
if a specific Attribute is required depending on the Media Storage
Services. The following Type designations are derived from the
designations but take into account the Media Storage environment:

-  Type 1: Such Attributes shall be present with an explicit Value in
   files created by File-set Creators and File-set Updaters. They shall
   be supported by File-set Readers and File-set Updaters;

-  Type 1C: Such Attributes shall be present with an explicit Value in
   Files created by File-set Creators and File-set Updaters if the
   specified condition is met. They shall be supported by File-set
   Readers and File-set Updaters;

-  Type 2: Such Attributes shall be present with an explicit Value or
   with a zero-length Value if unknown, in Files created by File-set
   Creators and File-set Updaters. They shall be supported by File-set
   Readers and File-set Updaters;

-  Type 2C: Such Attributes shall be present with an explicit Value or
   with a zero-length if unknown, in Files created by File-set Creators
   and File-set Updaters if the specified condition is met. They shall
   be supported by File-set Readers and File-set Updaters;

-  Type 3: Such Attributes may be present with an explicit Value or a
   zero-length Value in Files created by File-set Creators and File-set
   Updaters. They may be supported or ignored by File-set Readers and
   File-set Updaters.

