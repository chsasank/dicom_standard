.. _chapter_7:

Hosted Application Life Cycle
=============================

.. _sect_7.1:

Initialization
--------------

The Hosting System initializes a Hosted Application by issuing a run
command or its equivalent (e.g exec function in the C language) with
command line parameters to specify the end point references (URLs) to be
used for the interfaces. One end point reference is used by the Hosted
Application to access the Host interface provided by the Hosting System.
The second end point reference is where the Hosting System will look for
the Application interface provided by the Hosted Application. The Host
and Application interfaces are described in `Interfaces <#chapter_8>`__.
If issued from a command prompt or shell, the run command may appear as:

*app*--hostURL *url1*--applicationURL *url2*

.. note::

   1. In this startup methodology, it is the Hosting System, not the
      Hosted Application that specifies both URLs. The Hosted
      Application must respond at the URL assigned to it by the Hosting
      System.

   2. A Hosted Application implementation where the Hosted Application
      runs remotely or on an application server might utilize a startup
      or proxy application to appropriately map between the URL provided
      by the Hosting System and the actual URL that the Hosted
      Application is using.

`figure_title <#figure_7.1-1>`__ shows a sequence diagram of Hosted
Application initialization. Once the Hosted Application has initialized
and is ready to begin processing data, it changes its state to IDLE and
notifies the Hosting System of the state change using a call to the
notifyStateChanged() method, thus informing the Hosting System that the
Hosted Application is ready to go.

.. _sect_7.2:

States
------

`figure_title <#figure_7.2-1>`__ shows the state diagram for a Hosted
Application. The states are defined in `table_title <#table_7.2-1>`__.

.. table:: States

   +------------+--------------------------------------------------------+
   | State      | Description                                            |
   +============+========================================================+
   | IDLE       | In IDLE state the Hosted Application is waiting for a  |
   |            | new task assignment from the Hosting System. This is   |
   |            | the initial state when the Hosted Application starts.  |
   +------------+--------------------------------------------------------+
   | INPROGRESS | The Hosted Application is performing the assigned      |
   |            | task.                                                  |
   +------------+--------------------------------------------------------+
   | SUSPENDED  | The Hosted Application is stopping processing and is   |
   |            | releasing as many resources as it can, while still     |
   |            | preserving enough state to be able to resume           |
   |            | processing.                                            |
   +------------+--------------------------------------------------------+
   | COMPLETED  | The Hosted Application has completed processing, and   |
   |            | is waiting for the Hosting System to access and        |
   |            | release any output data from Hosted Application.       |
   +------------+--------------------------------------------------------+
   | CANCELED   | The Hosted Application is stopping processing, and is  |
   |            | releasing all resources with no chance to resume       |
   |            | processing.                                            |
   +------------+--------------------------------------------------------+
   | EXIT       | The terminal state of the Hosted Application.          |
   +------------+--------------------------------------------------------+

The transitions between states are described in
`table_title <#table_7.2-2>`__.

.. table:: Transitions Between States

   +-------------+-----------------------------------------+------------+
   | State       | Trigger                                 | New State  |
   +=============+=========================================+============+
   | not started | Hosting System launches the Hosted      | IDLE       |
   |             | Application (e.g., run, exec).          |            |
   +-------------+-----------------------------------------+------------+
   | IDLE        | Hosting System calls                    | EXIT       |
   |             | Application.setState (EXIT).            |            |
   +-------------+-----------------------------------------+------------+
   | IDLE        | Hosting System calls                    | INPROGRESS |
   |             | Application.setState (INPROGRESS).      |            |
   +-------------+-----------------------------------------+------------+
   | INPROGRESS  | Hosting System calls                    | SUSPENDED  |
   |             | Application.setState (SUSPENDED).       |            |
   +-------------+-----------------------------------------+------------+
   | INPROGRESS  | Hosting System calls                    | CANCELED   |
   |             | Application.setState (CANCELED).        |            |
   +-------------+-----------------------------------------+------------+
   | INPROGRESS  | Hosted Application encounters an error  | CANCELED   |
   |             | that prevents further processing, but   |            |
   |             | is still healthy enough to perhaps      |            |
   |             | start another task. The Hosted          |            |
   |             | Application shall report this error     |            |
   |             | through a call to notifyStatus() with a |            |
   |             | statusType of FATALERROR prior to       |            |
   |             | transitioning to the CANCELED state.    |            |
   +-------------+-----------------------------------------+------------+
   | INPROGRESS  | Hosted Application finishes its         | COMPLETED  |
   |             | processing.                             |            |
   +-------------+-----------------------------------------+------------+
   | SUSPENDED   | Hosting System calls                    | INPROGRESS |
   |             | Application.setState (INPROGRESS).      |            |
   +-------------+-----------------------------------------+------------+
   | SUSPENDED   | Hosted Application encounters an error  | CANCELED   |
   |             | (e.g., during suspension) that prevents |            |
   |             | further processing, but is still        |            |
   |             | healthy enough to perhaps start another |            |
   |             | task. The Hosted Application shall      |            |
   |             | report this error through a call to     |            |
   |             | notifyStatus() with a statusType of     |            |
   |             | FATALERROR prior to transitioning to    |            |
   |             | the CANCELED state.                     |            |
   +-------------+-----------------------------------------+------------+
   | SUSPENDED   | Hosting System calls                    | CANCELED   |
   |             | Application.setState (CANCELED).        |            |
   +-------------+-----------------------------------------+------------+
   | COMPLETED   | Hosting System calls                    | IDLE       |
   |             | Application.setState (IDLE), after      |            |
   |             | capturing all pertinent output data     |            |
   |             | from the Hosted Application.            |            |
   +-------------+-----------------------------------------+------------+
   | CANCELED    | Hosted Application releases all         | IDLE       |
   |             | resources and is ready for the next     |            |
   |             | task.                                   |            |
   +-------------+-----------------------------------------+------------+

The Hosted Application notifies the Hosting System of all state
transitions by calling the notifyStateChanged() method.

.. note::

   If a Hosted Application does not respond to state change requests
   made by the Hosting System, the Hosting System may 'hard abort' the
   Hosted Application in some implementation specific manner, such as by
   killing the process in which the Hosted Application is executing.

