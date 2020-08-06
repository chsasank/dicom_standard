.. _chapter_5:

Conventions
===========

Word(s) are capitalized in this document to help the reader understand
that these word(s) have been previously defined in Section 3 and are to
be interpreted with that meaning.

A Data Element Tag is represented as (gggg,eeee), where gggg equates to
the Group Number and eeee equates to the Element Number within that
Group. Data Element Tags are represented in hexadecimal notation as
specified for each named Data Element in this Standard.

Where an "x" is shown in a group or element number, e.g. (ggxx,eeee),
"x" means any value from 0 through F inclusive. The resulting group
number is still required to be even, as defined by , since these are
Standard Data Element Tags.

"RET" is used to indicate that the corresponding Data Element, SOP
Class, or Transfer Syntax has been retired. Retired items are shown
italicized. For retired items, the edition of the Standard in
parentheses is the edition in which the item last appeared before it was
retired. When the name of a retired Data Element has been reused, the
retired element has the qualifier "(Retired)" added, or "(Trial)" in the
cases in which the Data Element was used in a Draft For Trial
Implementation but not standardized.

.. note::

   The use of retired items is supported in this version of DICOM.
   However, new implementations are strongly encouraged to implement
   alternative Data Elements, SOP Classes or Transfer Syntaxes.

"Note n" is used to indicate that further information is provided at the
end of the corresponding table. The "n" is the consecutive number of the
note. This information is not inserted directly into the tables in order
to preserve their simple structure, e.g., for automatic processing of
the contents.

