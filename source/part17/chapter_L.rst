.. _chapter_L:

Hemodynamics Report Structure (Informative)
===========================================

The Hemodynamics Report is based on . The report contains one or more
measurement containers, each corresponding to a phase of the cath
procedure. Within each container may be one or more sub-containers, each
associated with a single measurement set. A measurement set consists of
measurements from a single anatomic location. The resulting hierarchical
structure is depicted in `figure_title <#figure_L-1>`__.

The container for each phase has an optional subsidiary container for
Clinical Context with a parent-child relationship of
has-acquisition-context. This Clinical Context container allows the
recording of pertinent patient state information that may be essential
to understanding the measurements made during that procedure phase. It
should be noted that any such patient state information is necessarily
only a summary; a more complete clinical picture may be obtained by
review of the cath procedure log.

The lowest level containers for the measurement sets are specialized by
the class of anatomic location - arterial, venous, atrial, ventricular -
for the particular measurements appropriate to that type of location.
These containers explicitly identify the anatomic location with a
has-acquisition-context relationship. Since such measurement sets are
typically measured on the same source (e.g., pressure waveform), the
container may also have a has-acquisition-context relationship with a
source DICOM waveform SOP Instance.

The "atomic" level of measurements within the measurement set containers
includes three types of data. First is the *specific measurement data*
acquired from waveforms related to the site. Second is *general
measurement data* that may include any hemodynamic, patient vital sign,
or blood chemistry data. Third, *derived data* are produced from a
combination of other data using a mathematical formula or table, and may
provide reference to the equation.

