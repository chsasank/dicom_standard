.. _chapter_5:

Conventions
===========

This section defines conventions used throughout the rest of this Part
of the Standard.

.. _sect_5.1:

Message Syntax
--------------

The syntax of the request and response messages for transactions are
defined using the ABNF Grammar used in
`biblioentry_title <#biblio_RFC_7230>`__, which is based on the ABNF
defined in `biblioentry_title <#biblio_RFC_5234>`__. This Part of the
Standard also uses the ABNF extensions in
`biblioentry_title <#biblio_RFC_7405>`__, which defines '%s' prefix for
denoting case sensitive strings.

The syntax rules defined herein are valid for the US-ASCII character set
or character sets that are supersets of US-ASCII, e.g., Unicode UTF-8.

In the ABNF used to define the syntax of messages, the following
conventions are used:

1. Syntactic variables are lowercase.

2. Terminal rules are uppercase. For example, 'SP' stands for the
   US-ASCII space (0x20) literal character, and 'CRLF' stands for the
   ASCII carriage return (0xD) and line feed (0xA) literal characters.

3. Header Field names are capitalized and quotation marks that denote
   literal strings for header field names are omitted. The Header Field
   names are the only capitalized names used in the grammar. See
   `biblioentry_title <#biblio_RFC_7231>`__ `Section
   1.2 <http://tools.ietf.org/html/rfc7231#section-1.2>`__. For example:

   ::

      Accept: media-type CRLF

   is equivalent to

   ::

      "Accept:" media-type CRLF

In this Part of the Standard, as with HTTP in general, resources are
identified by URIs `biblioentry_title <#biblio_RFC_3986>`__. Each
service defines the resources it manages, and the URI Templates used to
define the structure of the URIs that reference them.

In HTTP RFCs, ABNF rules for obs-text and obs-fold denote "obsolete"
grammar rules that appear for historical reasons. These rules are not
used in DICOM Web Services syntax definitions.

See `Collected ABNF <#chapter_A>`__ for the Combined ABNF for DICOM Web
Services.

.. _sect_5.1.1:

Common Syntactic Rules For Data Types
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

`table_title <#table_5.1-1>`__ defines the syntax of some common rules
used in defining data values in this Part of the Standard.

.. table:: ABNF for Common Syntactic Values

   +-------------------+-------------------------------------------------+
   | Name              | Rule                                            |
   +===================+=================================================+
   | ::                | ::                                              |
   |                   |                                                 |
   |    int            |    = [+ / -] 1*DIGIT                            |
   |                   |                                                 |
   |                   | ::                                              |
   |                   |                                                 |
   |                   |    ; An integer                                 |
   +-------------------+-------------------------------------------------+
   | ::                | ::                                              |
   |                   |                                                 |
   |    uint           |    = 1*DIGIT                                    |
   |                   |                                                 |
   |                   | ::                                              |
   |                   |                                                 |
   |                   |    ; An unsigned integer                        |
   +-------------------+-------------------------------------------------+
   | ::                | ::                                              |
   |                   |                                                 |
   |    non-zero-digit |    = %31-39                                     |
   +-------------------+-------------------------------------------------+
   | ::                | ::                                              |
   |                   |                                                 |
   |    pos-int        |    = non-zero-digit *DIGIT                      |
   |                   |                                                 |
   |                   | ::                                              |
   |                   |                                                 |
   |                   |    ; An integer greater than zero               |
   +-------------------+-------------------------------------------------+
   | ::                | ::                                              |
   |                   |                                                 |
   |    decimal        |    =int ["." uint] [("E" / "e") int]            |
   |                   |                                                 |
   |                   | ::                                              |
   |                   |                                                 |
   |                   |    ; a fixed- or f                              |
   |                   | loating-point number with at most 16 characters |
   +-------------------+-------------------------------------------------+
   | ::                | ::                                              |
   |                   |                                                 |
   |    string         |    = %s 1*QCHAR                                 |
   |                   |                                                 |
   |                   | ::                                              |
   |                   |                                                 |
   |                   |    ; A case sensitive string                    |
   +-------------------+-------------------------------------------------+
   | ::                | ::                                              |
   |                   |                                                 |
   |    base64         |    ; Use base64 defined in  Section 5           |
   +-------------------+-------------------------------------------------+
   | ::                | ::                                              |
   |                   |                                                 |
   |    uid            |    = uid-root 1*("." uid-part)                  |
   +-------------------+-------------------------------------------------+
   | ::                | ::                                              |
   |                   |                                                 |
   |    uid-root       |    = "0" / "1" / "2"                            |
   +-------------------+-------------------------------------------------+
   | ::                | ::                                              |
   |                   |                                                 |
   |    uid-part       |    = "0" / pos-int                              |
   +-------------------+-------------------------------------------------+

.. _sect_5.1.2:

URI Templates
~~~~~~~~~~~~~

The URI Template `biblioentry_title <#biblio_RFC_6570>`__ syntax has
been extended to allow case sensitive variable names. This has been done
by modifying the varchar production (see
`biblioentry_title <#biblio_RFC_6570>`__ `Section
2.3 <http://tools.ietf.org/html/rfc6570#section-2.3>`__) as follows:

::

   varchar = %x20-21 / %x23-7E / pct-encoded

.. _sect_5.1.3:

List Rule('#')
~~~~~~~~~~~~~~

The ABNF has been extended with the List Rule, which is used to define
comma-separated lists. It does not allow empty lists, empty list
elements, or the legacy list rules defined in
`biblioentry_title <#biblio_RFC_7230>`__ `Section
7 <http://tools.ietf.org/html/rfc7230#section-7>`__.

::

   1#element = element *(OWS "," OWS element)

::

   #element = 1#element

::

   <n>#<m>element = element <n-1>*<m-1> (OWS "," OWS element)

Where

::

   n >= 1 and m > n

.. _sect_5.2:

Web Service Section Structure
-----------------------------

This Part of the Standard is organized so that new Services may be
appended as new numbered sections at the end of the document.

.. _sect_5.3:

Request and Response Header Field Tables
----------------------------------------

Request header field requirements are described using tables of the
following form:

.. table:: Request Header Fields

   ==== ===== ===== ===========
   Name Value Usage Description 
   ==== ===== ===== ===========
   ...                          
   ...                          
   ==== ===== ===== ===========

The Name column contains the name of the HTTP header field as defined in
[RFC7230, RFC7231].

The Value column defines either the value type or the specific value
contained in the header field.

The Usage User Agent column defines requirements for the user agent to
supply the header field in the request.

The Usage Origin Server column defines requirements for the origin
server to support the header field.

The content of the Usage columns is either:

M
   Mandatory

C
   Conditional

O
   Optional

The Description column of conditional request header fields specifies
the condition for the presence of the header field.

-  "Shall be present if <condition>" means that if the <condition> is
   true, then the header field shall be present; otherwise, it shall not
   be present.

-  "May be present otherwise" is added to the description if the header
   field may be present, even if the condition is not true.

Response header field requirements are described using tables of the
following form:

.. table:: Response Header Fields

   ==== ===== =================== ===========
   Name Value Origin Server Usage Description
   ==== ===== =================== ===========
   ...                            
   ...                            
   ==== ===== =================== ===========

For response header fields the Usage column defines requirements for the
origin server to supply the header field.

