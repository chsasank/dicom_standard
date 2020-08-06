.. _chapter_G:

Explanation of Grouping Criteria For Multi-frame Functional Group IODs (Informative)
====================================================================================

This Annex was formerly located in in the 2003 and earlier revisions of
the Standard.

When considering how to group an Attribute, one needs to consider first
of all whether or not the values of an Attribute are different per
frame. The reasons to consider whether to allow an Attribute to change
include:

-  The more Attributes that change, the more parsing a receiving
   application has to do in order to determine if the multi-frame object
   has frames the application should deal with. The more choices, the
   more complex the application becomes, potentially resulting in
   interoperability problems.

-  The frequency of change of an Attribute must also be considered. If
   an Attribute could be changed every frame then obviously it is not a
   very good candidate for making it fixed, since this would result in a
   multi-frame size of 1.

-  The number of applications that depend on frame level Attribute
   grouping is another consideration. For example, one might imagine a
   pulse sequence being changed in a real-time acquisition, but the vast
   majority of acquisitions would leave this constant. Therefore, it was
   judged not too large a burden to force an acquisition device to start
   a new object when this happens. Obviously, this is a somewhat
   subjective decision, and one should take a close look at the
   Attributes that are required to be fixed in this document.

-  The Attributes from the image pixel module must not change in a
   multi-frame object due to legacy tool kits and implementations.

-  The potential frequency of change is dependent on the applications
   both now and likely during the life of this Standard. The penalty for
   failure to allow an Attribute to change is rather high since it will
   be hard/impossible to change later. Making an Attribute variable that
   is static is more complex and could result in more header space usage
   depending on how it is grouped. Thus there is a trade-off of
   complexity and potentially header size with not being able to take
   advantage of the multi-frame organization for an application that
   requires changes per frame.

Once it is decided which Attributes should be changed within a
multi-frame object then one needs to consider the criteria for grouping
Attributes together:

-  Groupings should be designed so those Attributes that are likely to
   vary together should be in the same sequence. The goal is to avoid
   the case where Attributes that are mostly static have to be included
   in a sequence that is repeated for every frame.

-  Care should be taken so that we define a manageable number of
   grouping sequences. Too few sequences could result in many static
   Attributes being repeated for each frame, when some other element in
   their sequence was varying, and too many sequences becomes unwieldy.

-  The groupings should be designed such that modality independent
   Attributes are kept separate from those that are MR specific. This
   will presumably allow future working groups to reuse the more general
   groupings. It also should allow software that operates on multi-frame
   objects from multiple objects maximize code reuse.

-  Grouping related Attributes together could convey some semantics of
   the overall contents of the multi-frame object to receiving
   applications. For instance, if a volumetric application finds the
   Plane Orientation Macro present in the Per-frame Functional Groups
   Sequence, it may decide to reject the object as inappropriate for
   volumetric calculations.

Specific notes on Attribute grouping:

-  Attributes not allowed to change: Image Pixel Module (due to legacy
   toolkit concerns); and Pulse Sequence Module Attributes (normally do
   not change except in real-time - it is expected real time
   applications can handle the complexity and speed of starting new IODs
   when pulse sequence changes).

-  Sequences not starting with the word "MR" could be applied to more
   modalities than just MR.

-  All Attributes that must be in a frame header were placed in the
   Frame Content Macro.

-  Position and orientation are in separate sequences since they are
   changed independently.

-  For real-time sequences there are contrast mechanisms that can be
   applied to base pulse sequences and are turned on and off by the
   operator depending on the anatomy being imaged and the time/contrast
   trade-off associated with these. Such modifiers include: IR, flow
   compensation, spoiled, MT, and T2 preparation… These probably are not
   changed in non-real-time scans. These are all kept in the MR Modifier
   Macro.

"Number of Averages" Attributes is in its own sequence because real-time
applications may start a new averaging process every time a slice
position/orientation changes. Each subsequent frame will average with
the preceding N frames where N is chosen based on motion and time. Each
frame collected at a particular position/orientation will have a
different number of averages, but all other Attributes are likely to
remain the same. This particular application drives this Attribute being
in its own group.

