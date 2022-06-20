# DAP4 Extension: CSV Data Encoding and Response

This document specifies the DAP4 CSV data encoding, how DAP4 servers can
advertise support for the DAP4 CSV encoding, and how DAP4 clients can
request DAP4 CSV encoded data responses.

The DAP4 CSV data encoding represents DAP4 data as structured
Comma-Separated Values (CSV) in UTF-8 text. Though based on the
*text/csv* media type described in RFC
4180<sup>\[[RFC\ 4180](https://docs.opendap.org/index.php?title=DAP4_Extension:_CSV_Data_Encoding_and_Response#RFC_4180)\]</sup>,
the DAP4 CSV is more complex so that it can fully represent the more
complex data structures of the DAP4 data model. Some structure beyond
simple CSV is necessary to capture the DAP4 data structures.

As with requests for data in the DAP4 binary data encoding described in
Volume 1 of the DAP4 specification
<sup>\[[DAP4\ Vol1](https://docs.opendap.org/index.php?title=DAP4_Extension:_CSV_Data_Encoding_and_Response#DAP4_Vol1)\]</sup>,
requests for DAP4 CSV encoded data can be constrained to a subset by
using a standard DAP4 Constraint Expression \[DAP4 CE\]

## Contents

<span class="toctoggle"> \[<span class="togglelink" role="button"
tabindex="0">hide</span>\] </span>

-   [<span class="tocnumber">1</span> <span class="toctext">DAP4
    Extension
    Details</span>](https://docs.opendap.org/index.php?title=DAP4_Extension:_CSV_Data_Encoding_and_Response#DAP4_Extension_Details)
-   [<span class="tocnumber">2</span> <span class="toctext">Requesting
    DAP4 CSV Encoded Data
    Response</span>](https://docs.opendap.org/index.php?title=DAP4_Extension:_CSV_Data_Encoding_and_Response#Requesting_DAP4_CSV_Encoded_Data_Response)
-   [<span class="tocnumber">3</span> <span class="toctext">DAP4 CSV
    Encoding</span>](https://docs.opendap.org/index.php?title=DAP4_Extension:_CSV_Data_Encoding_and_Response#DAP4_CSV_Encoding)
-   [<span class="tocnumber">4</span> <span class="toctext">Normative
    References</span>](https://docs.opendap.org/index.php?title=DAP4_Extension:_CSV_Data_Encoding_and_Response#Normative_References)

## <span id="DAP4_Extension_Details" class="mw-headline"><span class="mw-headline-number">1</span> DAP4 Extension Details</span>

The Role URI for the DAP4 CSV Data Encoding and Response extension is

    http://services.opendap.org/dap4/extension/text-csv-data

DAP4 servers MUST include this role URI in a Dataset Service Response
\[DSR\] *extension* element to indicate that the DAP4 CSV Data Encoding
and Response extension is supported for the dataset (?represented by
that DSR?). DAP4 clients MAY check for DSR **extension** elements with
this role URI to determine if the DAP4 CSV Data Encoding and Response
extension is supported.

Dataset Service Response \[DSR\] *extension* elements must also contain
a name and a description. The following are recommended text for the
name and description:

  

Name  
DAP4 CSV Data Encoding and Response

<!-- -->

Description  
This extension provides an encoding for representing DAP4 data as
structured Comma-Separated Values (CSV) in UTF-8 text.

## <span id="Requesting_DAP4_CSV_Encoded_Data_Response" class="mw-headline"><span class="mw-headline-number">2</span> Requesting DAP4 CSV Encoded Data Response</span>

> <table class="wikitable" style="font-size: 95%;" width="90%">
> <colgroup>
> <col style="width: 33%" />
> <col style="width: 33%" />
> <col style="width: 33%" />
> </colgroup>
> <tbody>
> <tr class="header">
> <th style="width: 15%">URL Suffix</th>
> <th style="width: 55%">Media Type</th>
> <th style="width: 30%">URL Example</th>
> </tr>
>
> <tr class="odd">
> <td>"<strong>.dap</strong>" or "<strong>.dap.csv</strong>"</td>
> <td><dl>
> <dt>application/vnd.opendap.dap4.data+csv</dt>
> <dd>
> DAP4 CSV encoding
> </dd>
> </dl></td>
> <td>http://server/path/dataset.nc<strong>.dap</strong>
> <p>http://server/path/dataset.nc<strong>.dap.csv</strong></p></td>
> </tr>
> <tr class="even">
> <td>"<strong>.dap.csv</strong>"</td>
> <td><dl>
> <dt>text/csv</dt>
> <dd>
> DAP4 CSV (UTF-8) Data encoding with generic media type
> </dd>
> </dl></td>
> <td>http://server/path/dataset.nc<strong>.dap.csv</strong></td>
> </tr>
> </tbody>
> </table>

## <span id="DAP4_CSV_Encoding" class="mw-headline"><span class="mw-headline-number">3</span> DAP4 CSV Encoding</span>

## <span id="Normative_References" class="mw-headline"><span class="mw-headline-number">4</span> Normative References</span>

\[RFC 4180\]
<a href="https://www.ietf.org/rfc/rfc4180.txt" class="external text"
rel="nofollow">Common Format and MIME Type for Comma-Separated Values
(CSV) Files</a>

\[DAP4 Vol1\] [DAP4 Volume 1: Data Model, Persistent Representations,
and
Constraints](https://docs.opendap.org/index.php?title=DAP4:_Specification_Volume_1 "DAP4: Specification Volume 1").

\[DAP4 Extensions\] \[DAP4:\_Specification\_Volume\_1#Extensions|DAP4
Volume 1, Section 9.3 Extensions\]
