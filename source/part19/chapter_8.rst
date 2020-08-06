.. _chapter_8:

Interfaces
==========

There are three base interfaces defined in this Part, as shown in
`figure_title <#figure_8-1>`__. One, named "Application", represents the
Hosted Application, and is utilized by the Hosting System to control the
Hosted Application. The second, named "Host", represents the Hosting
System, and is utilized by the Hosted Application to request services
from and to notify the Hosting System of events during the execution of
the Hosted Application. The third, named "DataExchange" is an interface
used by both the Hosting System and the Hosted Application to
communicate information about the data to be exchanged. Thus, the entire
Hosted Application ("ApplicationService") implementation consists of the
combination of the "Application" and "DataExchange" base interfaces,
while the entire Hosting System ("HostService") implementation consists
of the combination of the "Host" and "DataExchange" base interfaces.

The interfaces are defined as a set of methods using Web Services
Description Language (WSDL). The implementers shall change the end point
references (i.e., the "location" XML Attribute within the "address" XML
Element within the "port" XML Elements of a "service" XML Element) in
the WSDL specification as needed to deploy Hosted Applications and
Hosting Systems that utilize these interfaces.

.. note::

   The major (non-backward compatible) versions of the interfaces are
   reflected in the values of the "name" and "targetNamespace" XML
   Attributes of the "definitions" XML Element in the WSDL specification
   of the interfaces. Any changes to the interfaces that are not
   backward compatible will utilize new values for "name" and
   "targetNamespace" XML Attributes of the "definitions" XML Element.

Minor (backward compatible) versions of the interfaces may be reflected
in the values of the "targetNamespace" XML Attribute of any new "schema"
XML Element where new input or output data types are defined in the WSDL
specifications, and/or in the values of the "name" XML Attributes of the
"portType" and "service" XML Elements where new messages and operations
are associated as new services in the WSDL specifications of the
interfaces. To maintain backward compatibility, the names of existing
elements, messages, and operations in the WSDL specification of the
interfaces remain the same.

These methods utilize a set of basic data types and more complex data
structures to communicate parameters, which are defined using XML
Schemas. Later sections of this document provide more detailed
descriptions of the interfaces and data structures, along with sequence
diagrams illustrating how the interfaces are used.

The actual WSDL code and XML Schemas that specify this interface are
defined in `Interface Definitions <#chapter_B>`__.

.. note::

   1. WSDL is a platform and programming language independent means of
      specifying an interface between two cooperating applications. The
      applications need not be written in the same programming language.

   2. The interfaces do not directly address reporting of SOAP
      communications problems. If a problem occurs in the communications
      between the Hosting System and a Hosting Application during the
      execution of a WSDL interface call, this should be reported by the
      SOAP libraries utilized by an implementation, e.g., thrown as an
      exception.

.. _sect_8.1:

Application Interface
---------------------

The following sections describe the methods of the Application
interface.

.. _sect_8.1.1:

getState() : State
~~~~~~~~~~~~~~~~~~

The Hosted Application returns its current state to the caller.

This method may be called at any time.

.. note::

   1. A Hosting System may use this method as an alternative to tracking
      Hosted Application state changes reported by the
      notifyStateChanged() method call.

   2. A Hosting System may use this method to determine if a Hosted
      Application is still in operation (i.e., did not die without
      calling the notifyStateChanged() method with an EXIT state).

.. _sect_8.1.2:

setState(newState : State) : boolean
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

The Hosting System requests that the Hosted Application switch to the
newState.

The Hosted Application returns TRUE from the method if the Hosted
Application received the request, and the requested state change is
allowed in the state diagram. Otherwise, the method returns FALSE. A
return value of TRUE does not indicate that the state of the Hosted
Application has changed to the newState; it merely indicates that the
requested state change is valid, and will be made at the soonest
opportunity. Once the Hosted Application switches to the requested
state, it shall inform the Hosting System through the
notifyStateChanged() method of the Host interface.

.. note::

   The asynchronous response to a state change is intended to minimize
   blocking the Hosting System while waiting for a potentially
   time-consuming state change in the application.

The Hosted Application shall ignore any setState() and return TRUE when
the Hosted Application is already in requested state (i.e., this is a
repeated call with the same state).

If the Hosted Application receives a second setState() request for a
different state prior to completing a previous request, then the Hosted
Application shall abort or ignore the previous request, and begin
processing the latest request.

This method may be called at any time, however may not have any effect
(other than a return of FALSE) if the requested new state is not an
allowed transition from the current state.

.. _sect_8.1.3:

bringToFront(requestedScreenArea : Rectangle) : boolean
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

By calling this method, the Hosting System is asking the Hosted
Application to take whatever steps are needed to make its GUI visible as
the topmost window, and to gain focus.

If possible, the Hosted Application shall resize and reposition itself
to the requestedScreenArea. If requestedScreenArea is missing or null,
the Hosted Application may retain its current size and location on the
screen.

The method returns TRUE if the Hosted Application received the request
and will act on it. Otherwise it returns FALSE.

A Hosted Application shall act on this method if the Hosted Application
is in the IDLE or INPROGRESS state. A Hosted Application is not required
to act on this method if the Hosted Application is not in the IDLE or
INPROGRESS state.

A Hosted Application that has no GUI (e.g., a headless analysis
application), where becoming visible and gaining focus has no meaning,
shall always return TRUE from this method.

.. _sect_8.2:

Host Interface
--------------

The following sections describe the methods of the Host interface.

.. _sect_8.2.1:

generateUID() : UID
~~~~~~~~~~~~~~~~~~~

Returns a newly created DICOM UID that the Hosted Application might use,
e.g., to create new data objects and structures.

This method may be called at any time.

.. _sect_8.2.2:

getAvailableScreen(appPreferredScreen : Rectangle) : Rectangle
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

The Hosted Application supplies its preferred screen size in the
appPreferredScreen parameter. The Hosting System may utilize this
information as a hint, but may return a window location and size that
best suits the Hosting System's GUI.

The method returns the window location and size that the Hosting System
would prefer that the Hosted Application utilize. However, there are no
requirements that the Hosted Application act on that information.

This method may be called at any time.

.. _sect_8.2.3:

getOutputLocation(preferredProtocols: ArrayOfString) : String
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

The method returns a URI that a Hosted Application may use to store
output that it may provide back to the Hosting System (e.g., in response
to a getData() call).

The Hosted Application indicates, in order of preference, the protocols
it can use to store data. The Hosted Application shall at least support
both the http: and the file: protocols. The Hosting System selects the
most appropriate protocol, potentially taking into account system or
security considerations as well as the order of preference. The Hosting
System uses the selected protocol in setting up the resources and
generating the URI returned to the Hosted Application.

.. note::

   1. There may be limitations when using the http: protocol when
      compared to the file: protocol. Some functions that might work
      with a file: protocol such as seek, rewrite, and delete, may not
      work with the http: protocol. The Hosted Application should assume
      that it can only write once in sequential order when the returned
      output location uses the http: protocol.

   2. If any authentication information is needed in order to access the
      data, this authentication information may be included in the URI.

The Hosting System shall keep the URI active while the Hosted
Application is in any state other than IDLE or EXIT, or until such time
that the Hosted Application returns the URI to the Hosting System (e.g.,
in an ObjectLocator returned to the Hosting System in response to a
getData() call). The disposition of the data that the Hosted Application
sends to this URI is the responsibility of the Hosting System after the
Hosted Application transitions to the IDLE state or after the Hosted
Application returns the URI to the Hosting System (e.g., in an
ObjectLocator returned to the Hosting System in response to a getData()
call). After the Hosted Application transitions to IDLE state, the
Hosting System need not keep the URI active.

The Hosted Application shall only call this method if the Hosted
Application is at the INPROGRESS or COMPLETED states.

.. _sect_8.2.4:

notifyStateChanged(state : State) : void
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

The Hosted Application shall invoke this method each time the Hosted
Application successfully transitions to a new state. The new state is
passed in the state parameter.

.. note::

   While all Hosting Systems need to accept this interface call method,
   they may track the current Application State in other ways, such as
   by polling for the state using the Application getState() method.

.. _sect_8.2.5:

notifyStatus(status : Status) : void
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

The Hosted Application may inform the Hosting System of notable events
that occur during execution by invoking this method, passing the
information in the status parameter.

.. note::

   The Hosting System typically would log these events to facilitate
   debugging. It may, at its discretion, display the information to the
   user.

This method may be called at any time.

.. _sect_8.3:

DataExchange Interface
----------------------

The interface used to exchange information about data being transferred
between a source and a recipient is the same for both the Hosting System
and the Hosted Application. Implementations of the Application interface
shall also include the DataExchange interface. Implementations of the
Host interface shall also include the DataExchange interface. In other
words, the DataExchange interface is symmetric with respect to the
Hosting System and Hosting Application.

The data being exchanged between the Hosting System and the Hosted
Application can either be passed as files, or may be described in models
that might be queried by the recipient.

Recipients that can parse DICOM objects are able to request the
file-based methods. The sequence diagram in
`figure_title <#figure_8.3-1>`__ illustrates one potential exchange
using the file-based methods.

The advantage of using the model-based methods is that the recipient
need not know how to parse the data formats, but instead can use
commonly available tools for manipulating XML Infosets to extract data
from the models.

The model-based interfaces can work with a variety of models. Particular
models are identified by a UID. The models can either be an abstraction
of the data, or can be a model of some native format. Models defined by
the DICOM Standard are described in `Data Exchange
Models <#chapter_A>`__. Models are described as XML Infosets, even
though the original data might never be actually represented in XML
form. The source providing the data handles the mapping from the models
back to the original data format.

Abstract models allow a recipient to work with data without regard to
what its native form is. For example, data from a variety of image
formats, such as DICOM, TIFF, JPEG, NIfTI, or Analyze, could be included
in an abstract image model. The recipient can then work with the data
even though the recipient has no knowledge of how the data was natively
represented. Abstract models may have been derived from data referenced
in multiple ObjectDescriptors (e.g., multiple CT slices combined into a
single volume).

Abstract models generally do not include the full richness of data that
is available in native representations. For example, an abstract image
model derived from DICOM data normally would include references to
'cooked' pixel data and its spatial organization, but might not include
many of the modality-specific Attributes. To allow recipients to access
such details the supplier of an abstract model can provide references to
the ObjectDescriptors, in the form of UUIDs, from which that abstract
model was derived. The recipient may gain access to any attribute of the
original data formats through the source ObjectDescriptors.

The sequence diagram in `figure_title <#figure_8.3-2>`__ illustrates one
potential exchange using the model-based methods. It also illustrates
the Hosted Application returning partial outputs, one potential way a
Hosted Application might use the getOutputLocation() method, and
potential uses of the releaseModel() and releaseData() methods.

Hosting Systems shall support both the file-based and model-based
interfaces, both as a data source as well as a data recipient.

Hosted Applications shall support at least one of the file-based or
model-based interfaces, as either a data source or as a data recipient,
as needed by the Hosted Application. If a Hosted Application supports
the model-based interfaces, it shall support at least one of the models
defined in `Data Exchange Models <#chapter_A>`__. Hosted Applications
may choose to implement only those portions of those interfaces that the
Hosted Application actually uses; however, all interface methods that a
Hosting System may call must be available for the Hosting System to
call, even if the Hosted Application does not do anything but return
appropriately.

The following sections describe the methods of the DataExchange
interface.

.. _sect_8.3.1:

notifyDataAvailable(data : AvailableData, lastData : boolean) : boolean
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

The source of the data calls this method with descriptions of the
available data that it can provide to the recipient. If the source of
the data expects that additional data will become available, it shall
pass FALSE in the lastData parameter. Otherwise, it shall pass TRUE in
the lastData parameter, and shall not make any further calls to
notifyDataAvailable until after it has transitioned through the IDLE
state once more.

The source of the data shall be able to provide the data in the form
identified in the AvailableData structure.

A Hosting System uses this method to inform a Hosted Application of
input data that the Hosted Application should work with. A Hosted
Application uses this method to inform the Hosting System of outputs
produced by the Hosted Application.

This method returns TRUE if the recipient of the data successfully
received the AvailableData list. Otherwise this method returns FALSE.

.. note::

   A Hosted Application that is recipient of this call, but that was
   unsuccessful in receiving the AvailableData list might report a
   reason for the failure in a notifyStatus method call.

The source of the data shall not include in AvailableData any references
to data that were sent in a previous successful notifyDataAvailable call
(i.e., one where the method call returned TRUE).

A Hosted Application shall not transition into the COMPLETED state if it
has received or sent a notifyDataAvailable() call with a lastData
indicator of FALSE.

The source of the data may call notifyDataAvailable() with an empty data
list.

.. note::

   Calling notifyDataAvailable() with an empty list is useful for
   setting the lastData indicator to TRUE.

This method shall only be called if the Hosted Application is at the
INPROGRESS state.

.. _sect_8.3.2:

getData(objectUUIDs : ArrayOfUUID, acceptableTransferSyntaxUIDs : ArrayOfUID, includeBulkData : boolean) : ArrayOfObjectLocator
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

The recipient of data invokes this method to gain access to binary data
provided by the source of the data. The source of the data provides a
URI that the recipient may open as a byte stream to retrieve the data.

.. note::

   The provider of the data may delay the actual preparation of binary
   data until the recipient actually requests it.

The objectUUIDs array provides the UUIDs of the binary data that the
source wishes to retrieve. Each of the UUIDs in that array are drawn
either from the ObjectDescriptors provided in the AvailableData
structure received by the recipient in one or more notifyDataAvailable()
method calls, or from bulk data pointers in models accessed by the
recipient.

If the UUID came from an ObjectDescriptor, the source returns
ObjectLocators of the binary objects using the MIME content type and
class UID listed in the ObjectDescriptor within the AvailableData
structure associated with each UUID. If the UUID came from a Data
Exchange Model, then the source returns the binary bulk data described
within the model.

The recipient lists the desired Transfer Syntax for the bulk data via
the acceptableTransferSyntaxUIDs parameter. The recipient shall list in
order of preference in the acceptableTransferSyntaxUIDs parameter the
UIDs of the Transfer Syntaxes that it will accept for the data
represented by objectUUIDs. The provider of the data shall select and
use the first transfer syntax in the list that it supports. For DICOM
data, the provider of data shall as a minimum support the Explicit VR
Little Endian transfer syntax. The acceptableTransferSyntaxUIDs may be
empty for those MIME content types where Transfer Syntax has no meaning.

When retrieving binary data identified by a UUID from an
ObjectDescriptor, if the recipient sets the includeBulkData flag to
TRUE, then the source shall supply the bulk data within the data stream.
Otherwise, the source may, but is not required to, omit bulk data such
as pixel data.

.. note::

   The includeBulkData flag is useful, for example, when the recipient
   wishes to work with the description of the pixel data in binary DICOM
   form, in order to decide whether or not to retrieve the pixel data
   itself.

The method returns one ObjectLocator for each UUID passed into the
method within the objectUUIDs array. The ObjectLocator describes a file
where the recipient can read in the data referred to by that particular
object's UUID.

When the recipient is finished with data referred to by an ObjectLocator
URI, it may call the releaseData() method to free up the resources being
consumed to provide those URIs. Any data references not explicitly
released by the recipient of the data are released implicitly when the
Hosted Application enters the IDLE state.

The recipient may call getData() multiple times for data referenced by a
given ObjectDescriptor or bulk data UUID. Each call to getData() shall
be matched by either an explicit or implicit call to releaseData().

This method shall only be called if the Hosted Application is at the
INPROGRESS or COMPLETED states. A Hosting System may also call this
method when the Hosted Application is in the SUSPENDED state.

.. _sect_8.3.3:

getAsModels(objectUUIDs : ArrayOfUUID, classUID : UID, supportedInfosetTypes : ArrayOfMimeType) : ModelSetDescriptor
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

The recipient of data invokes this method to ask that the source of the
data provide the data referenced by objectUUIDs array as models of the
type referenced by classUID. The objectUUIDs are drawn from the
ObjectDescriptors passed to the recipient of the data in one or more
notifyDataAvailable() calls.

The recipient of the data shall list in supportedInfosetTypes in order
of preference the MIME types that the recipient can process as Infosets.
Recipients of data shall support the "text/xml" MIME type, which shall
always be included in the supportedInfosetTypes array. The provider of
data shall select the first entry in that array that it supports.

The ModelSetDescriptor returned by this method contains the UUIDs of the
models provided by the source, as well as the UUIDs of data objects
referred to by the objectUUIDs array that could not be represented in
the requested model.

The recipient may call getAsModels() multiple times for data referenced
by a given UUID. Each successful call returns a different model UUID.

When the recipient is finished with a set of models, it may call the
releaseModels() method to free up the resources being consumed to
provide those models. Any models not explicitly released by the
recipient of the data are released implicitly when the Hosted
Application enters the IDLE state.

This method shall only be called if the Hosted Application is at the
INPROGRESS or COMPLETED states. A Hosting System may also call this
method when the Hosted Application is in the SUSPENDED state.

.. _sect_8.3.4:

queryModel(models : ArrayOfUUID, xpaths : ArrayOfString) : ArrayOfQueryResult
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

The recipient of data invokes this method to request that the source of
the data return the subset of data referred to in each of the XPath
query strings passed in the xpath parameter from each of the models
identified by the UUIDs passed in the model array. Each of the XPath
query strings is applied to each of the models referred to in the model
array.

The UUIDs passed in the model array shall be chosen from those returned
by one or more getAsModels() method calls.

The results of the query are returned by the method as XML Infosets,
encoded in XML returned as a string. Each result from a particular model
UUID is returned as a QueryResult element in the returned array for each
xpath string. In other words, the number of QueryResults returned is the
number of UUIDs in the model array times the number of XPath queries
strings in the xpath array.

.. note::

   This method is principally used when the infoset type is "text/xml".

This method shall only be called if the Hosted Application is at the
INPROGRESS or COMPLETED states. A Hosting System may also call this
method when the Hosted Application is in the SUSPENDED state.

.. _sect_8.3.5:

queryInfoset(models : ArrayOfUUID, xpaths : ArrayOfString) : ArrayOfQueryResultInfoset
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

The recipient of data invokes this method to request that the source of
the data return the subset of data referred to in each of the XPath
query strings passed in the xpath parameter from each of the models
identified by the UUIDs passed in the model array. Each of the XPath
query strings is applied to each of the models referred to in the model
array.

The UUIDs passed in the model array shall be chosen from those returned
by one or more getAsModels() method calls.

The results of the query are returned by the method as XML Infosets,
encoded in XML, returned as a byte array encoded in the form negotiated
during the getAsModel() call. Each result from a particular model UUID
is returned as a QueryResultInfoset element in the returned array for
each xpath string. In other words, the number of QueryResultInfoset
structures returned is the number of UUIDs in the model array times the
number of XPath queries strings in the xpath array.

.. note::

   This method is principally used when the infoset type is not string
   based, for example a "application/fastinfoset". If called on a model
   using the "text/xml" infoset type, a conversion from a byte array to
   a string would be needed.

This method shall only be called if the Hosted Application is at the
INPROGRESS or COMPLETED states. A Hosting System may also call this
method when the Hosted Application is in the SUSPENDED state.

.. _sect_8.3.6:

releaseData(objectUUIDs : ArrayOfUUID) : void
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

The recipient of data invokes this method to release access to binary
data provided by the source of the data through a getData() call. The
ArrayOfUUID identifies the data streams that the recipient is releasing.
The UUIDs in this array shall be drawn from the locator fields in
ObjectLocators returned by calls to getData().

.. _sect_8.3.7:

releaseModels(objectUUIDs : ArrayOfUUID) : void
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

The recipient of data invokes this method to release access to models
provided by the source of the data. The ArrayOfUUID identifies the
models that the recipient is releasing. The UUIDs in this array shall be
drawn from the models fields in ModelSetDescriptors returned by calls to
getAsModels().

