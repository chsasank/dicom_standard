.. _chapter_8:

Coded Entry Usage in Service Specifications
===========================================

The Macros in this Section specify the usage of the Attributes that
correspond to Coded Entries as defined by .

Not all invocations make use of all the columns. For example, in some
invocations, only the "Requirement Type SCU/SCP" is relevant; in others,
only the Matching Key Type and Return Key Type columns are used.

.. table:: Enhanced SCU/SCP Coded Entry Macro with SCU Support, Matching
Key Support and Mandatory Meaning

   +-------------+-------------+-------------+-------------+-------------+
   | Attribute   | Tag         | Requirement | Matching    | Return Key  |
   | Name        |             | Type        | Key Type    | Type        |
   |             |             |             |             |             |
   |             |             | SCU/SCP     |             |             |
   +=============+=============+=============+=============+=============+
   | *Includ     |             |             |             |             |
   | e*\ `table_ |             |             |             |             |
   | title <#tab |             |             |             |             |
   | le_8-1b>`__ |             |             |             |             |
   +-------------+-------------+-------------+-------------+-------------+
   | Equivalent  | (0008,0121) | 3/3         | O           | 3           |
   | Code        |             |             |             |             |
   | Sequence    |             |             |             |             |
   +-------------+-------------+-------------+-------------+-------------+
   | *>Includ    |             |             |             |             |
   | e*\ `table_ |             |             |             |             |
   | title <#tab |             |             |             |             |
   | le_8-1b>`__ |             |             |             |             |
   +-------------+-------------+-------------+-------------+-------------+

.. table:: Basic SCU/SCP Coded Entry Macro with SCU Support, Matching
Key Support and Mandatory Meaning

   +-------------+-------------+-------------+-------------+-------------+
   | Attribute   | Tag         | Requirement | Matching    | Return Key  |
   | Name        |             | Type        | Key Type    | Type        |
   |             |             |             |             |             |
   |             |             | SCU/SCP     |             |             |
   +=============+=============+=============+=============+=============+
   | Code Value  | (0008,0100) | 1C/1C       | RC          | 1C          |
   |             |             |             |             |             |
   |             |             | Shall be    | Required if | Shall be    |
   |             |             | present if  | the code    | present if  |
   |             |             | the code    | value       | the code    |
   |             |             | value       | length is   | value       |
   |             |             | length is   | 16          | length is   |
   |             |             | 16          | characters  | 16          |
   |             |             | characters  | or less,    | characters  |
   |             |             | or less,    | and the     | or less,    |
   |             |             | and the     | code value  | and the     |
   |             |             | code value  | is not a    | code value  |
   |             |             | is not a    | URN or URL. | is not a    |
   |             |             | URN or URL. |             | URN or URL. |
   +-------------+-------------+-------------+-------------+-------------+
   | Coding      | (0008,0102) | 1C/1C       | RC          | 1C          |
   | Scheme      |             |             |             |             |
   | Designator  |             | Shall be    | Required if | Shall be    |
   |             |             | present if  | Code Value  | present if  |
   |             |             | Code Value  | (0008,0100) | Code Value  |
   |             |             | (0008,0100) | or Long     | (0008,0100) |
   |             |             | or Long     | Code Value  | or Long     |
   |             |             | Code Value  | (0008,0119) | Code Value  |
   |             |             | (0008,0119) | is present. | (0008,0119) |
   |             |             | is present. | May be      | is present. |
   |             |             | May be      | present     | May be      |
   |             |             | present     | otherwise.  | present     |
   |             |             | otherwise.  |             | otherwise.  |
   +-------------+-------------+-------------+-------------+-------------+
   | Coding      | (0008,0103) | 1C/1C       | RC          | 1C          |
   | Scheme      |             |             |             |             |
   | Version     |             | Required if | Required if | Required if |
   |             |             | the value   | the value   | the value   |
   |             |             | of Coding   | of Coding   | of Coding   |
   |             |             | Scheme      | Scheme      | Scheme      |
   |             |             | Designator  | Designator  | Designator  |
   |             |             | (0008,0102) | (0008,0102) | (0008,0102) |
   |             |             | is present  | is present  | is present  |
   |             |             | and is not  | and is not  | and is not  |
   |             |             | sufficient  | sufficient  | sufficient  |
   |             |             | to identify | to identify | to identify |
   |             |             | the Code    | the Code    | the Code    |
   |             |             | Value       | Value       | Value       |
   |             |             | (0008,0100) | (0008,0100) | (0008,0100) |
   |             |             | or Long     | or Long     | or Long     |
   |             |             | Code Value  | Code Value  | Code Value  |
   |             |             | (0008,0119) | (0008,0119) | (0008,0119) |
   |             |             | or URN Code | or URN Code | or URN Code |
   |             |             | Value       | Value       | Value       |
   |             |             | (0008,0120) | (0008,0120) | (0008,0120) |
   |             |             | una         | una         | una         |
   |             |             | mbiguously. | mbiguously. | mbiguously. |
   |             |             | Shall not   | Shall not   | Shall not   |
   |             |             | be present  | be present  | be present  |
   |             |             | if Coding   | if Coding   | if Coding   |
   |             |             | Scheme      | Scheme      | Scheme      |
   |             |             | Designator  | Designator  | Designator  |
   |             |             | (0008,0102) | (0008,0102) | (0008,0102) |
   |             |             | is absent.  | is absent.  | is absent.  |
   |             |             | May be      | May be      | May be      |
   |             |             | present     | present     | present     |
   |             |             | otherwise.  | otherwise.  | otherwise.  |
   +-------------+-------------+-------------+-------------+-------------+
   | Code        | (0008,0104) | 1/1         | -           | 1           |
   | Meaning     |             |             |             |             |
   +-------------+-------------+-------------+-------------+-------------+
   | Long Code   | (0008,0119) | 1C/1C       | RC          | 1C          |
   | Value       |             |             |             |             |
   |             |             | Shall be    | Required if | Required if |
   |             |             | present if  | Code Value  | Code Value  |
   |             |             | Code Value  | (0008,0100) | (0008,0100) |
   |             |             | (0008,0100) | is not      | is not      |
   |             |             | is not      | present,    | present,    |
   |             |             | present,    | and the     | and the     |
   |             |             | and the     | code value  | code value  |
   |             |             | code value  | is not a    | is not a    |
   |             |             | is not a    | URN or URL. | URN or URL. |
   |             |             | URN or URL. |             |             |
   +-------------+-------------+-------------+-------------+-------------+
   | URN Code    | (0008,0120) | 1C/1C       | RC          | 1C          |
   | Value       |             |             |             |             |
   |             |             | Shall be    | Required if | Require if  |
   |             |             | present if  | Code Value  | Code Value  |
   |             |             | Code Value  | (0008,0100) | (0008,0100) |
   |             |             | (0008,0100) | is not      | is not      |
   |             |             | is not      | present,    | present,    |
   |             |             | present,    | and the     | and the     |
   |             |             | and the     | code value  | code value  |
   |             |             | code value  | is a URN or | is a URN or |
   |             |             | is a URN or | URL.        | URL.        |
   |             |             | URL.        |             |             |
   +-------------+-------------+-------------+-------------+-------------+
   | Mapping     | (0008,0105) | 3/3         | -           | 3           |
   | Resource    |             |             |             |             |
   +-------------+-------------+-------------+-------------+-------------+
   | Mapping     | (0008,0118) | 3/3         | -           | 3           |
   | Resource    |             |             |             |             |
   | UID         |             |             |             |             |
   +-------------+-------------+-------------+-------------+-------------+
   | Context     | (0008,0118) | 3/3         | -           | 3           |
   | Group       |             |             |             |             |
   | Version     |             |             |             |             |
   +-------------+-------------+-------------+-------------+-------------+
   | Context     | (0008,010B) | 3/3         | -           | 3           |
   | Group       |             |             |             |             |
   | Extension   |             |             |             |             |
   | Flag        |             |             |             |             |
   +-------------+-------------+-------------+-------------+-------------+
   | Context     | (0008,0107) | 3/3         | -           | 3           |
   | Group Local |             |             |             |             |
   | Version     |             |             |             |             |
   +-------------+-------------+-------------+-------------+-------------+
   | Context     | (0008,010D) | 3/3         | -           | 3           |
   | Group       |             |             |             |             |
   | Extension   |             |             |             |             |
   | Creator UID |             |             |             |             |
   +-------------+-------------+-------------+-------------+-------------+

.. table:: Enhanced Coded Entry Macro with Optional Matching Key Support
and Optional Meaning

   +-----------------+-------------+-----------------+-----------------+
   | Attribute Name  | Tag         | Matching Key    | Return Key Type |
   |                 |             | Type            |                 |
   +=================+=============+=================+=================+
   | *Include*\      |             |                 |                 |
   |  `table_title < |             |                 |                 |
   | #table_8-2b>`__ |             |                 |                 |
   +-----------------+-------------+-----------------+-----------------+
   | Equivalent Code | (0008,0121) | O               | 3               |
   | Sequence        |             |                 |                 |
   +-----------------+-------------+-----------------+-----------------+
   | *>Include*\     |             |                 |                 |
   |  `table_title < |             |                 |                 |
   | #table_8-2b>`__ |             |                 |                 |
   +-----------------+-------------+-----------------+-----------------+

.. table:: Basic Coded Entry Macro with Optional Matching Key Support
and Optional Meaning

   +-----------------+-------------+-----------------+-----------------+
   | Attribute Name  | Tag         | Matching Key    | Return Key Type |
   |                 |             | Type            |                 |
   +=================+=============+=================+=================+
   | Code Value      | (0008,0100) | O               | 1C              |
   |                 |             |                 |                 |
   |                 |             |                 | Shall be        |
   |                 |             |                 | present if the  |
   |                 |             |                 | code value      |
   |                 |             |                 | length is 16    |
   |                 |             |                 | characters or   |
   |                 |             |                 | less, and the   |
   |                 |             |                 | code value is   |
   |                 |             |                 | not a URN or    |
   |                 |             |                 | URL.            |
   +-----------------+-------------+-----------------+-----------------+
   | Coding Scheme   | (0008,0102) | O               | 1C              |
   | Designator      |             |                 |                 |
   |                 |             |                 | Shall be        |
   |                 |             |                 | present if Code |
   |                 |             |                 | Value           |
   |                 |             |                 | (0008,0100) or  |
   |                 |             |                 | Long Code Value |
   |                 |             |                 | (0008,0119) is  |
   |                 |             |                 | present.        |
   +-----------------+-------------+-----------------+-----------------+
   | Coding Scheme   | (0008,0103) | OC              | 3               |
   | Version         |             |                 |                 |
   |                 |             | May be present  | Applicable only |
   |                 |             | only if the     | if the value of |
   |                 |             | value of Coding | Coding Scheme   |
   |                 |             | Scheme          | Designator      |
   |                 |             | Designator      | (0008,0102) is  |
   |                 |             | (0008,0102) is  | present and is  |
   |                 |             | present and is  | not sufficient  |
   |                 |             | not sufficient  | to identify the |
   |                 |             | to identify the | Code Value      |
   |                 |             | Code Value      | (0008,0100) or  |
   |                 |             | (0008,0100) or  | Long Code Value |
   |                 |             | Long Code Value | (0008,0119) or  |
   |                 |             | (0008,0119) or  | URN Code Value  |
   |                 |             | URN Code Value  | (0008,0120)     |
   |                 |             | (0008,0120)     | unambiguously.  |
   |                 |             | unambiguously.  |                 |
   +-----------------+-------------+-----------------+-----------------+
   | Code Meaning    | (0008,0104) | O               | 3               |
   +-----------------+-------------+-----------------+-----------------+
   | Long Code Value | (0008,0119) | O               | 1C              |
   |                 |             |                 |                 |
   |                 |             |                 | Shall be        |
   |                 |             |                 | present if Code |
   |                 |             |                 | Value           |
   |                 |             |                 | (0008,0100) is  |
   |                 |             |                 | not present,    |
   |                 |             |                 | and the code    |
   |                 |             |                 | value is not a  |
   |                 |             |                 | URN or URL.     |
   +-----------------+-------------+-----------------+-----------------+
   | URN Code Value  | (0008,0120) | O               | 1C              |
   |                 |             |                 |                 |
   |                 |             |                 | Shall be        |
   |                 |             |                 | present only if |
   |                 |             |                 | Code Value      |
   |                 |             |                 | (0008,0100) is  |
   |                 |             |                 | not present,    |
   |                 |             |                 | and the code    |
   |                 |             |                 | value is a URN  |
   |                 |             |                 | or URL.         |
   +-----------------+-------------+-----------------+-----------------+
   | Mapping         | (0008,0105) | O               | 3               |
   | Resource        |             |                 |                 |
   +-----------------+-------------+-----------------+-----------------+
   | Mapping         | (0008,0118) | O               | 3               |
   | Resource UID    |             |                 |                 |
   +-----------------+-------------+-----------------+-----------------+
   | Context Group   | (0008,0118) | O               | 3               |
   | Version         |             |                 |                 |
   +-----------------+-------------+-----------------+-----------------+
   | Context Group   | (0008,010B) | O               | 3               |
   | Extension Flag  |             |                 |                 |
   +-----------------+-------------+-----------------+-----------------+
   | Context Group   | (0008,0107) | O               | 3               |
   | Local Version   |             |                 |                 |
   +-----------------+-------------+-----------------+-----------------+
   | Context Group   | (0008,010D) | O               | 3               |
   | Extension       |             |                 |                 |
   | Creator UID     |             |                 |                 |
   +-----------------+-------------+-----------------+-----------------+

.. table:: Enhanced SCU/SCP Coded Entry Macro with no SCU Support and no
Matching Key Support

   +-------------+-------------+-------------+-------------+-------------+
   | Attribute   | Tag         | Requirement | Matching    | Return Key  |
   | Name        |             | Type        | Key Type    | Type        |
   |             |             |             |             |             |
   |             |             | SCU/SCP     |             |             |
   +=============+=============+=============+=============+=============+
   | *Includ     |             |             |             |             |
   | e*\ `table_ |             |             |             |             |
   | title <#tab |             |             |             |             |
   | le_8-3b>`__ |             |             |             |             |
   +-------------+-------------+-------------+-------------+-------------+
   | Equivalent  | (0008,0121) | -/3         | -           |             |
   | Code        |             |             |             |             |
   | Sequence    |             |             |             |             |
   +-------------+-------------+-------------+-------------+-------------+
   | *>Includ    |             |             |             |             |
   | e*\ `table_ |             |             |             |             |
   | title <#tab |             |             |             |             |
   | le_8-3b>`__ |             |             |             |             |
   +-------------+-------------+-------------+-------------+-------------+

.. table:: Basic SCU/SCP Coded Entry Macro with no SCU Support and no
Matching Key Support

   +-------------+-------------+-------------+-------------+-------------+
   | Attribute   | Tag         | Requirement | Matching    | Return Key  |
   | Name        |             | Type        | Key Type    | Type        |
   |             |             |             |             |             |
   |             |             | SCU/SCP     |             |             |
   +=============+=============+=============+=============+=============+
   | Code Value  | (0008,0100) | -/1C        | -           | 1C          |
   |             |             |             |             |             |
   |             |             | Shall be    |             | Shall be    |
   |             |             | present if  |             | present if  |
   |             |             | the code    |             | the code    |
   |             |             | value       |             | value       |
   |             |             | length is   |             | length is   |
   |             |             | 16          |             | 16          |
   |             |             | characters  |             | characters  |
   |             |             | or less,    |             | or less,    |
   |             |             | and the     |             | and the     |
   |             |             | code value  |             | code value  |
   |             |             | is not a    |             | is not a    |
   |             |             | URN or URL. |             | URN or URL. |
   +-------------+-------------+-------------+-------------+-------------+
   | Coding      | (0008,0102) | -/1C        | -           | 1C          |
   | Scheme      |             |             |             |             |
   | Designator  |             | Shall be    |             | Shall be    |
   |             |             | present if  |             | present if  |
   |             |             | Code Value  |             | Code Value  |
   |             |             | (0008,0100) |             | (0008,0100) |
   |             |             | or Long     |             | or Long     |
   |             |             | Code Value  |             | Code Value  |
   |             |             | (0008,0119) |             | (0008,0119) |
   |             |             | is present. |             | is present. |
   |             |             | May be      |             | May be      |
   |             |             | present     |             | present     |
   |             |             | otherwise.  |             | otherwise.  |
   +-------------+-------------+-------------+-------------+-------------+
   | Coding      | (0008,0103) | -/1C        | -           | 1C          |
   | Scheme      |             |             |             |             |
   | Version     |             | Required if |             | Shall be    |
   |             |             | the value   |             | present if  |
   |             |             | of Coding   |             | the value   |
   |             |             | Scheme      |             | of Coding   |
   |             |             | Designator  |             | Scheme      |
   |             |             | (0008,0102) |             | Designator  |
   |             |             | is present  |             | (0008,0102) |
   |             |             | and is not  |             | is present  |
   |             |             | sufficient  |             | and is not  |
   |             |             | to identify |             | sufficient  |
   |             |             | the Code    |             | to identify |
   |             |             | Value       |             | the Code    |
   |             |             | (0008,0100) |             | Value       |
   |             |             | or Long     |             | (0008,0100) |
   |             |             | Code Value  |             | or Long     |
   |             |             | (0008,0119) |             | Code Value  |
   |             |             | or URN Code |             | (0008,0119) |
   |             |             | Value       |             | or URN Code |
   |             |             | (0008,0120) |             | Value       |
   |             |             | una         |             | (0008,0120) |
   |             |             | mbiguously. |             | una         |
   |             |             | Shall not   |             | mbiguously. |
   |             |             | be present  |             | Shall not   |
   |             |             | if Coding   |             | be present  |
   |             |             | Scheme      |             | if Coding   |
   |             |             | Designator  |             | Scheme      |
   |             |             | (0008,0102) |             | Designator  |
   |             |             | is absent.  |             | (0008,0102) |
   |             |             | May be      |             | is absent.  |
   |             |             | present     |             | May be      |
   |             |             | otherwise.  |             | present     |
   |             |             |             |             | otherwise.  |
   +-------------+-------------+-------------+-------------+-------------+
   | Code        | (0008,0104) | -/1         | -           | 1           |
   | Meaning     |             |             |             |             |
   +-------------+-------------+-------------+-------------+-------------+
   | Long Code   | (0008,0119) | -/1C        | -           | 1C          |
   | Value       |             |             |             |             |
   |             |             | Shall be    |             | Shall be    |
   |             |             | present if  |             | present if  |
   |             |             | Code Value  |             | Code Value  |
   |             |             | (0008,0100) |             | (0008,0100) |
   |             |             | is not      |             | is not      |
   |             |             | present,    |             | present,    |
   |             |             | and the     |             | and the     |
   |             |             | code value  |             | code value  |
   |             |             | is not a    |             | is not a    |
   |             |             | URN or URL. |             | URN or URL. |
   +-------------+-------------+-------------+-------------+-------------+
   | URN Code    | (0008,0120) | -/1C        | -           | 1C          |
   | Value       |             |             |             |             |
   |             |             | Shall be    |             | Shall be    |
   |             |             | present if  |             | present if  |
   |             |             | Code Value  |             | Code Value  |
   |             |             | (0008,0100) |             | (0008,0100) |
   |             |             | is not      |             | is not      |
   |             |             | present,    |             | present,    |
   |             |             | and the     |             | and the     |
   |             |             | code value  |             | code value  |
   |             |             | is a URN or |             | is a URN or |
   |             |             | URL.        |             | URL.        |
   +-------------+-------------+-------------+-------------+-------------+
   | Mapping     | (0008,0105) | -/3         | -           | 3           |
   | Resource    |             |             |             |             |
   +-------------+-------------+-------------+-------------+-------------+
   | Mapping     | (0008,0118) | -/3         | -           | 3           |
   | Resource    |             |             |             |             |
   | UID         |             |             |             |             |
   +-------------+-------------+-------------+-------------+-------------+
   | Context     | (0008,0118) | -/3         | -           | 3           |
   | Group       |             |             |             |             |
   | Version     |             |             |             |             |
   +-------------+-------------+-------------+-------------+-------------+
   | Context     | (0008,010B) | -/3         | -           | 3           |
   | Group       |             |             |             |             |
   | Extension   |             |             |             |             |
   | Flag        |             |             |             |             |
   +-------------+-------------+-------------+-------------+-------------+
   | Context     | (0008,0107) | -/3         | -           | 3           |
   | Group Local |             |             |             |             |
   | Version     |             |             |             |             |
   +-------------+-------------+-------------+-------------+-------------+
   | Context     | (0008,010D) | -/3         | -           | 3           |
   | Group       |             |             |             |             |
   | Extension   |             |             |             |             |
   | Creator UID |             |             |             |             |
   +-------------+-------------+-------------+-------------+-------------+

.. table:: Enhanced Coded Entry Macro with Optional Matching Key Support
and Mandatory Meaning

   +-----------------+-------------+-----------------+-----------------+
   | Attribute Name  | Tag         | Matching Key    | Return Key Type |
   |                 |             | Type            |                 |
   +=================+=============+=================+=================+
   | *Include*\      |             |                 |                 |
   |  `table_title < |             |                 |                 |
   | #table_8-4b>`__ |             |                 |                 |
   +-----------------+-------------+-----------------+-----------------+
   | Equivalent Code | (0008,0121) | O               | 3               |
   | Sequence        |             |                 |                 |
   +-----------------+-------------+-----------------+-----------------+
   | *>Include*\     |             |                 |                 |
   |  `table_title < |             |                 |                 |
   | #table_8-4b>`__ |             |                 |                 |
   +-----------------+-------------+-----------------+-----------------+

.. table:: Basic Coded Entry Macro with Optional Matching Key Support
and Mandatory Meaning

   +-----------------+-------------+-----------------+-----------------+
   | Attribute Name  | Tag         | Matching Key    | Return Key Type |
   |                 |             | Type            |                 |
   +=================+=============+=================+=================+
   | Code Value      | (0008,0100) | O               | 1C              |
   |                 |             |                 |                 |
   |                 |             |                 | Shall be        |
   |                 |             |                 | present if the  |
   |                 |             |                 | code value      |
   |                 |             |                 | length is 16    |
   |                 |             |                 | characters or   |
   |                 |             |                 | less, and the   |
   |                 |             |                 | code value is   |
   |                 |             |                 | not a URN or    |
   |                 |             |                 | URL.            |
   +-----------------+-------------+-----------------+-----------------+
   | Coding Scheme   | (0008,0102) | O               | 1C              |
   | Designator      |             |                 |                 |
   |                 |             |                 | Shall be        |
   |                 |             |                 | present if Code |
   |                 |             |                 | Value           |
   |                 |             |                 | (0008,0100) or  |
   |                 |             |                 | Long Code Value |
   |                 |             |                 | (0008,0119) is  |
   |                 |             |                 | present. May be |
   |                 |             |                 | present         |
   |                 |             |                 | otherwise.      |
   +-----------------+-------------+-----------------+-----------------+
   | Coding Scheme   | (0008,0103) | RC              | 1C              |
   | Version         |             |                 |                 |
   |                 |             | Required if the | Shall be        |
   |                 |             | value of Coding | present if the  |
   |                 |             | Scheme          | value of Coding |
   |                 |             | Designator      | Scheme          |
   |                 |             | (0008,0102) is  | Designator      |
   |                 |             | present and is  | (0008,0102) is  |
   |                 |             | not sufficient  | present and is  |
   |                 |             | to identify the | not sufficient  |
   |                 |             | Code Value      | to identify the |
   |                 |             | (0008,0100) or  | Code Value      |
   |                 |             | Long Code Value | (0008,0100) or  |
   |                 |             | (0008,0119) or  | Long Code Value |
   |                 |             | URN Code Value  | (0008,0119) or  |
   |                 |             | (0008,0120)     | URN Code Value  |
   |                 |             | unambiguously.  | (0008,0120)     |
   |                 |             | Shall not be    | unambiguously.  |
   |                 |             | present if      | Shall not be    |
   |                 |             | Coding Scheme   | present if      |
   |                 |             | Designator      | Coding Scheme   |
   |                 |             | (0008,0102) is  | Designator      |
   |                 |             | absent. May be  | (0008,0102) is  |
   |                 |             | present         | absent. May be  |
   |                 |             | otherwise.      | present         |
   |                 |             |                 | otherwise.      |
   +-----------------+-------------+-----------------+-----------------+
   | Code Meaning    | (0008,0104) | O               | 1               |
   +-----------------+-------------+-----------------+-----------------+
   | Long Code Value | (0008,0119) | O               | 1C              |
   |                 |             |                 |                 |
   |                 |             |                 | Shall be        |
   |                 |             |                 | present if Code |
   |                 |             |                 | Value           |
   |                 |             |                 | (0008,0100) is  |
   |                 |             |                 | not present,    |
   |                 |             |                 | and the code    |
   |                 |             |                 | value is not a  |
   |                 |             |                 | URN or URL.     |
   +-----------------+-------------+-----------------+-----------------+
   | URN Code Value  | (0008,0120) | O               | 1C              |
   |                 |             |                 |                 |
   |                 |             |                 | Shall be        |
   |                 |             |                 | present if Code |
   |                 |             |                 | Value           |
   |                 |             |                 | (0008,0100) is  |
   |                 |             |                 | not present,    |
   |                 |             |                 | and the code    |
   |                 |             |                 | value is a URN  |
   |                 |             |                 | or URL.         |
   +-----------------+-------------+-----------------+-----------------+
   | Mapping         | (0008,0105) | O               | 3               |
   | Resource        |             |                 |                 |
   +-----------------+-------------+-----------------+-----------------+
   | Mapping         | (0008,0118) | O               | 3               |
   | Resource UID    |             |                 |                 |
   +-----------------+-------------+-----------------+-----------------+
   | Context Group   | (0008,0118) | O               | 3               |
   | Version         |             |                 |                 |
   +-----------------+-------------+-----------------+-----------------+
   | Context Group   | (0008,010B) | O               | 3               |
   | Extension Flag  |             |                 |                 |
   +-----------------+-------------+-----------------+-----------------+
   | Context Group   | (0008,0107) | O               | 3               |
   | Local Version   |             |                 |                 |
   +-----------------+-------------+-----------------+-----------------+
   | Context Group   | (0008,010D) | O               | 3               |
   | Extension       |             |                 |                 |
   | Creator UID     |             |                 |                 |
   +-----------------+-------------+-----------------+-----------------+

.. table:: Enhanced SCU/SCP Coded Entry Macro with no SCU Support and
Optional Meaning for SCP

   ========================================= =========== ================
   Attribute Name                            Tag         Requirement Type
                                                         
                                                         SCU/SCP
   ========================================= =========== ================
   *Include*\ `table_title <#table_8-5b>`__              
   Equivalent Code Sequence                  (0008,0121) -/3
   *>Include*\ `table_title <#table_8-5b>`__             
   ========================================= =========== ================

.. table:: Basic SCU/SCP Coded Entry Macro with no SCU Support and
Optional Meaning for SCP

   +--------------------------+-------------+--------------------------+
   | Attribute Name           | Tag         | Requirement Type         |
   |                          |             |                          |
   |                          |             | SCU/SCP                  |
   +==========================+=============+==========================+
   | Code Value               | (0008,0100) | -/1C                     |
   |                          |             |                          |
   |                          |             | Shall be present if the  |
   |                          |             | code value length is 16  |
   |                          |             | characters or less, and  |
   |                          |             | the code value is not a  |
   |                          |             | URN or URL.              |
   +--------------------------+-------------+--------------------------+
   | Coding Scheme Designator | (0008,0102) | -/1C                     |
   |                          |             |                          |
   |                          |             | Shall be present if Code |
   |                          |             | Value (0008,0100) or     |
   |                          |             | Long Code Value          |
   |                          |             | (0008,0119) is present.  |
   |                          |             | May be present           |
   |                          |             | otherwise.               |
   +--------------------------+-------------+--------------------------+
   | Coding Scheme Version    | (0008,0103) | -/1C                     |
   |                          |             |                          |
   |                          |             | May be present if the    |
   |                          |             | value of Coding Scheme   |
   |                          |             | Designator (0008,0102)   |
   |                          |             | is present and is not    |
   |                          |             | sufficient to identify   |
   |                          |             | the Code Value           |
   |                          |             | (0008,0100) or Long Code |
   |                          |             | Value (0008,0119) or URN |
   |                          |             | Code Value (0008,0120)   |
   |                          |             | unambiguously. Shall not |
   |                          |             | be present if Coding     |
   |                          |             | Scheme Designator        |
   |                          |             | (0008,0102) is absent.   |
   |                          |             | May be present           |
   |                          |             | otherwise.               |
   +--------------------------+-------------+--------------------------+
   | Code Meaning             | (0008,0104) | -/3                      |
   +--------------------------+-------------+--------------------------+
   | Long Code Value          | (0008,0119) | -/1C                     |
   |                          |             |                          |
   |                          |             | Shall be present if Code |
   |                          |             | Value (0008,0100) is not |
   |                          |             | present, and the code    |
   |                          |             | value is not a URN or    |
   |                          |             | URL.                     |
   +--------------------------+-------------+--------------------------+
   | URN Code Value           | (0008,0120) | 1C/1C                    |
   |                          |             |                          |
   |                          |             | Shall be present if Code |
   |                          |             | Value (0008,0100) is not |
   |                          |             | present, and the code    |
   |                          |             | value is a URN or URL.   |
   +--------------------------+-------------+--------------------------+
   | Mapping Resource         | (0008,0105) | -/3                      |
   +--------------------------+-------------+--------------------------+
   | Mapping Resource UID     | (0008,0118) | -/3                      |
   +--------------------------+-------------+--------------------------+
   | Context Group Version    | (0008,0118) | -/3                      |
   +--------------------------+-------------+--------------------------+
   | Context Group Extension  | (0008,010B) | -/3                      |
   | Flag                     |             |                          |
   +--------------------------+-------------+--------------------------+
   | Context Group Local      | (0008,0107) | -/3                      |
   | Version                  |             |                          |
   +--------------------------+-------------+--------------------------+
   | Context Group Extension  | (0008,010D) | -/3                      |
   | Creator UID              |             |                          |
   +--------------------------+-------------+--------------------------+

