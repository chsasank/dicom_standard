.. _chapter_HHHH:

Protocol Approval Examples and Concepts (Informative)
=====================================================

The following example is provided to illustrate the usage of the
Protocol Approval IOD.

This example shows approval of a pair of CT Protocols for routine adult
head studies. It is approved by the Chief of Radiology and by the
Physicist. The Instance UIDs of the two CT Protocols are 1.2.3.456.7.7
and 1.2.3.456.7.8.

Note that the Institution Code Sequence (0008,0082) inside the Asserter
Identification Sequence (0044,0103) communicates that Mercy Hospital is
the organization to which Dr. Welby is responsible. The Institution Code
Sequence (0008,0082) at the end of the first Approval Item communicates
that Mercy Hospital is the institution for which the protocols are
"Approved for use at the institution".

.. table:: Approval by Chief Radiologist

   +--------------------------+-------------+--------------------------+
   | **Attribute**            | **Tag**     | **Value**                |
   +==========================+=============+==========================+
   | Manufacturer             | (0008,0070) | Acme Corp.               |
   +--------------------------+-------------+--------------------------+
   | Manufacturer's Model     | (0008,1090) | Primo Protocol           |
   | Name                     |             | Management Workstation   |
   |                          |             | Plus                     |
   +--------------------------+-------------+--------------------------+
   | Device Serial Number     | (0018,1000) | A59848573                |
   +--------------------------+-------------+--------------------------+
   | Software Versions        | (0018,1020) | V2.3                     |
   +--------------------------+-------------+--------------------------+
   | SOP Class UID            | (0008,0016) | 1.2.8                    |
   |                          |             | 40.10008.5.1.4.1.1.200.3 |
   |                          |             | *(Protocol Approval)*    |
   +--------------------------+-------------+--------------------------+
   | SOP Instance UID         | (0008,0018) | 1.33.9.876.1.1.1         |
   +--------------------------+-------------+--------------------------+
   | Approval Subject         | (0044,0109) |                          |
   | Sequence                 |             |                          |
   +--------------------------+-------------+--------------------------+
   | *Item #1*                |             |                          |
   +--------------------------+-------------+--------------------------+
   | >Referenced SOP Class    | (0008,1150) | 1.2.8                    |
   | UID                      |             | 40.10008.5.1.4.1.1.200.1 |
   |                          |             | *(CT Defined Procedure   |
   |                          |             | Protocol)*               |
   +--------------------------+-------------+--------------------------+
   | >Referenced SOP Instance | (0008,1155) | 1.2.3.456.7.7            |
   | UID                      |             |                          |
   +--------------------------+-------------+--------------------------+
   | *Item #2*                |             |                          |
   +--------------------------+-------------+--------------------------+
   | >Referenced SOP Class    | (0008,1150) | 1.2.8                    |
   | UID                      |             | 40.10008.5.1.4.1.1.200.1 |
   |                          |             | *(CT Defined Procedure   |
   |                          |             | Protocol)*               |
   +--------------------------+-------------+--------------------------+
   | >Referenced SOP Instance | (0008,1155) | 1.2.3.456.7.8            |
   | UID                      |             |                          |
   +--------------------------+-------------+--------------------------+
   | Approval Sequence        | (0044,0100) |                          |
   +--------------------------+-------------+--------------------------+
   | *Item #1*                |             |                          |
   +--------------------------+-------------+--------------------------+
   | >Assertion Code Sequence | (0044,0101) | (128603, DCM, "Approved  |
   |                          |             | for use at the           |
   |                          |             | institution")            |
   +--------------------------+-------------+--------------------------+
   | >Assertion UID           | (0044,0102) | 1.2.33.9.876.5.5.5.5.21  |
   +--------------------------+-------------+--------------------------+
   | >Asserter Identification | (0044,0103) |                          |
   | Sequence                 |             |                          |
   +--------------------------+-------------+--------------------------+
   | >>Observer Type          | (0040,A084) | PSN                      |
   +--------------------------+-------------+--------------------------+
   | >>Person Name            | (0040,A123) | "Welby^Marcus^^Dr.^MD"   |
   +--------------------------+-------------+--------------------------+
   | >>Person Identification  | (0040,1101) | (12345, 99NPI,           |
   | Code Sequence            |             | "Welby^Marcus^^Dr.^MD")  |
   +--------------------------+-------------+--------------------------+
   | >>Organizational Role    | (0044,010A) | (128670, DCM, "Head of   |
   | Code Sequence            |             | Radiology")              |
   +--------------------------+-------------+--------------------------+
   | >>Institution Name       | (0008,0080) | Mercy Hospital,          |
   |                          |             | Centerville              |
   +--------------------------+-------------+--------------------------+
   | >>Institution Code       | (0008,0082) | (000011113, 99NPI,       |
   | Sequence                 |             | "Mercy Hospital,         |
   |                          |             | Centerville")            |
   +--------------------------+-------------+--------------------------+
   | >Assertion DateTime      | (0044,0104) | 20150601145327           |
   +--------------------------+-------------+--------------------------+
   | >Assertion Expiration    | (0044,0105) | 20200601000000 *(based   |
   | DateTime                 |             | on a 5 yearly review     |
   |                          |             | plan)*                   |
   +--------------------------+-------------+--------------------------+
   | >Institution Code        | (0008,0082) | (000011113, 99NPI,       |
   | Sequence                 |             | "Mercy Hospital,         |
   |                          |             | Centerville")            |
   +--------------------------+-------------+--------------------------+
   | *Item #2*                |             |                          |
   +--------------------------+-------------+--------------------------+
   | >Assertion Code Sequence | (0044,0101) | (128605, DCM, "Approved  |
   |                          |             | for use on pregnant      |
   |                          |             | patients")               |
   +--------------------------+-------------+--------------------------+
   | >Assertion UID           | (0044,0102) | 1.2.33.9.876.5.5.5.5.22  |
   +--------------------------+-------------+--------------------------+
   | >Asserter Identification | (0044,0103) |                          |
   | Sequence                 |             |                          |
   +--------------------------+-------------+--------------------------+
   | >>Observer Type          | (0040,A084) | PSN                      |
   +--------------------------+-------------+--------------------------+
   | >>Person Name            | (0040,A123) | "Welby^Marcus^^Dr.^MD"   |
   +--------------------------+-------------+--------------------------+
   | >>Person Identification  | (0040,1101) | (12345, 99NPI,           |
   | Code Sequence            |             | "Welby^Marcus^^Dr.^MD")  |
   +--------------------------+-------------+--------------------------+
   | >>Organizational Role    | (0044,010A) | (128670, DCM, "Head of   |
   | Code Sequence            |             | Radiology")              |
   +--------------------------+-------------+--------------------------+
   | >>Institution Name       | (0008,0080) | Mercy Hospital,          |
   |                          |             | Centerville              |
   +--------------------------+-------------+--------------------------+
   | >>Institution Code       | (0008,0082) | (000011113, 99NPI,       |
   | Sequence                 |             | "Mercy Hospital,         |
   |                          |             | Centerville")            |
   +--------------------------+-------------+--------------------------+
   | >Assertion DateTime      | (0044,0104) | 20150601145327           |
   +--------------------------+-------------+--------------------------+
   | >Assertion Expiration    | (0044,0105) | 20200601000000 *(based   |
   | DateTime                 |             | on a 5 yearly review     |
   |                          |             | plan)*                   |
   +--------------------------+-------------+--------------------------+
   | >Assertion Comments      | (0044,0106) | "Limited scan range and  |
   |                          |             | proper use of abdominal  |
   |                          |             | shielding result in      |
   |                          |             | negligible dose to the   |
   |                          |             | fetus."                  |
   +--------------------------+-------------+--------------------------+

