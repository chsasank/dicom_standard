.. _chapter_6:

Application Hosting Overview
============================

This section describes the capabilities of the API, gives an example of
the sequence of operations, and summarizes the remaining sections of
this Part.

The APIs are shared by a Hosting System and one or more Hosted
Applications.

The API is agnostic to the hardware platform, the operating system, and
the GUI. The API supports requesting space in the GUI, if available. The
API supports headless operation (i.e., no GUI).

The APIs are defined using Web Services Definition Language (WSDL) to be
programming language, platform, and technology neutral. The APIs are
designed to maximize language independence while minimizing the impact
on efficiency of utilizing web services technology. The interfaces
support both a networked file-based and a shared-memory interaction
model. The API supports manual configuration, but not discovery.

The API can provide DICOM Data Sets and other data to the Hosted
Application and can accept DICOM Data Sets and other data created by the
Hosted Application, incrementally or upon completion. The Hosted
Application has granular access to data provided by the Hosting System
(e.g., single attributes, a subset of the pixel data, etc.) and only
that data. The API utilizes DICOM semantics, but not necessarily DICOM
network transfer syntax. The Hosting System provides a mechanism to the
Hosted Application for generating UIDs.

The API allows the Hosting System to suspend and/or cancel the operation
of the Hosted Application and regain user interface control. The API
supports returning status information from the Hosted Application to the
Hosting System and tracking the state of the Hosted Application.

The Hosting System has a mechanism to launch or connect to one or more
Hosted Applications, verify that the Hosted Application has started
successfully, and then pass the initial data objects. All interactions
start in the Hosting System. A typical sequence of events is as follows:

1.  The Hosting System identifies and locates the Hosted Application
    appropriate to the task and data using host-specific methods. Often
    the desired application is selected by the user of the system or is
    identified in a work list entry.

2.  The Hosting System launches the application, essentially issuing a
    'run' or 'exec' command, passing parameters that the Hosted
    Application uses to establish bilateral communications between the
    two.

3.  The Hosting System uses the API to initiate a processing task in the
    Hosted Application and notifies it of its input data.

4.  The Hosted Application uses the API to pull information from the
    Hosting System about the input data, including the location of the
    bulk pixel data.

5.  The Hosted Application may use file I/O, memory mapping, or any
    other appropriate method to gain access to the bulk pixel data.

6.  The Hosted Application may also use the API to inform the Hosting
    System of the status of the processing, for example progress, any
    warnings or errors encountered.

7.  The Hosting System might use the API to suspend or cancel processing
    in the Hosted Application.

8.  If the Hosting System suspended processing in the Hosted
    Application, it may use the API to instruct the Hosted Application
    to resume processing.

9.  The Hosted Application, as it processes the input data, might create
    output objects, and use the API to inform the Hosting System of
    their existence.

10. The Hosting System uses the API to pull information about the output
    objects from the Hosted Application, including the location of the
    bulk data.

11. The Hosting system might use file I/O, memory mapping, or any other
    appropriate method to gain access to the output bulk data, if
    needed.

12. Once the Hosting System has pulled the output data from the Hosted
    Application, it uses the API to instruct the Hosted Application to
    wait for the next processing task (i.e., tells the Hosted
    Application to idle).

13. If the Hosting System has another task for the Hosted Application to
    perform, it may use the API to start that task, following this
    sequence of events beginning at Step 3.

14. When the Hosting System no longer needs the Hosted Application, it
    may use the API to request that the Hosted Application exit.

`Hosted Application Life Cycle <#chapter_7>`__ describes in greater
detail the Hosted Application Life Cycle.

`Interfaces <#chapter_8>`__ describes the base interfaces between the
Hosting System and the Hosted Application.

`Data Types and Structures <#chapter_9>`__ describes the custom data
types and data structures used by the interfaces.

`Data Exchange Model Conventions <#chapter_10>`__ describes the general
form of models used by the model-based interfaces, and the conventions
used in defining those models. The models defined by this Standard are
described in the Annexes.

