.. _chapter_W:

Email Media (Normative)
=======================

.. _sect_W.1:

Email Media
-----------

This Media Format defines the interchange of other Media Formats, such
as DICOM MIME or ZIP File, using email.

A Standard or Private Application Profile that uses this Email Media
Format will specify the selection of the media profile to be
transported.

A Standard or Private Application Profile that uses this Email Media
Format specifies the MIME encoding requirements, to include:

a. The content identification to be used,

b. The attachment file identification to be used,

c. The disposition to be used,

d. Subject line content restrictions,

e. Other restrictions, especially use of MIME compression, encryption,
   and digital signatures.

.. note::

   Subject lines are often modified automatically, e.g., by the addition
   of "Re:". Other routing information such as "for Doctor Fred" is also
   often included. Automatic and human recognition of the special nature
   of this email can be improved by requiring that some phrase like
   "DICOM-ZIP" be part of the subject line.

.. _sect_W.2:

Media Interchange Application Entities
--------------------------------------

.. _sect_W.2.1:

Sender of the Email
~~~~~~~~~~~~~~~~~~~

The sender Application Entity composes an email and sends that email
using a standard email transmission protocol.

The sender shall compose an email in compliance with RFCs 2045 and 2046,
as a MIME Encoded email. RFC2046 defines both MIME encoding and the
mechanisms to be used for breaking up the email message if it is too
large for the email system to send as a single email. The sender may
request delivery acknowledgment and problem notification in accordance
with RFCs 3464 and 3798, but shall be prepared for email recipients that
do not implement RFCs 3464 and 3798. The sender shall send the email by
means of Simple Mail Transfer Protocol (RFC2821).

.. note::

   The sender Application Entity does not need to be a single software
   program. For example, the attachment file may be created
   independently and then a generic email program used to manage
   attaching the file and sending the email.

.. _sect_W.2.2:

Recipient of the Email
~~~~~~~~~~~~~~~~~~~~~~

The recipient Application Entity shall be able to receive an email by
means of one or more of POP3 (RFC1939), IMAP4 (RFC3501), or SMTP
(RFC2821), and extract the attachment specified in the Application
Profile. The recipient shall comply with RFC2046, and may comply with
RFCs 3464 and 3798.

