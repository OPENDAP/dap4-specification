# DAP4: Specification Volume 2

**The Data Access Protocol: DAP Version 4.0**

**Volume 2: DAP4 Web Services**

<table data-border="1" width="85%">
<tbody>
<tr class="odd">
<td width="20%">Date:</td>
<td>November 6, 2013</td>
</tr>
<tr class="even">
<td width="20%">Last Revised:</td>
<td>04 July 2014</td>
</tr>
<tr class="odd">
<td width="20%">Status:</td>
<td>Draft</td>
</tr>
<tr class="even">
<td width="20%">Authors:</td>
<td>John Caron (Unidata)</td>
</tr>
<tr class="odd">
<td width="20%"></td>
<td>Ethan Davis (Unidata)</td>
</tr>
<tr class="even">
<td width="20%"></td>
<td>David Fulker (OPeNDAP)</td>
</tr>
<tr class="odd">
<td width="20%"></td>
<td>James Gallagher (OPeNDAP)</td>
</tr>
<tr class="even">
<td width="20%"></td>
<td>Dennis Heimbigner (Unidata)</td>
</tr>
<tr class="odd">
<td width="20%"></td>
<td>Nathan Potter (OPeNDAP)</td>
</tr>
<tr class="even">
<td width="20%">Copyright:</td>
<td>2014 University Corporation for Atmospheric Research and
Opendap.org</td>
</tr>
</tbody>
</table>

  
***Abstract***

*While Volume 1 of the DAP4 specification addresses the detailed
semantics and structure of the DAP4 data and metadata content, this
volume (Volume 2) details the manner in which clients can request things
from a DAP4 server and what things the clients can expect to receive
from a DAP4 server in response to their requests. The description of
this interaction focuses on DAP4 clients and servers that are
communicating via HTTP, and while this is perceived by the authors as
the most common transport for DAP4 client/server interaction the
specification is written in a broad enough manner to allow for other
transport mechanisms.*

Distribution of this document is unlimited.

  
**Change List**

<table data-border="1" width="85%">
<tbody>
<tr class="odd">
<td width="25%">2013.09.06:</td>
<td>Initial Draft</td>
</tr>
<tr class="even" data-valign="top">
<td width="25%">2014.07.04</td>
<td>ASCII/.ascii changed to text/.txt; Removed most of the async text
since it is duplicate of the material in the extension; Created a volume
3 containing the extensions</td>
</tr>
</tbody>
</table>

  

## Contents

<span class="toctoggle"> \[<span class="togglelink" role="button"
tabindex="0">hide</span>\] </span>

-   [<span class="tocnumber">1</span> <span
    class="toctext">Introduction</span>](https://docs.opendap.org/index.php?title=DAP4:_Specification_Volume_2#Introduction)
-   [<span class="tocnumber">2</span> <span class="toctext">Terms and
    Definitions</span>](https://docs.opendap.org/index.php?title=DAP4:_Specification_Volume_2#Terms_and_Definitions)
    -   [<span class="tocnumber">2.1</span> <span class="toctext">DAP4
        Resource Roles and Media
        Types</span>](https://docs.opendap.org/index.php?title=DAP4:_Specification_Volume_2#DAP4_Resource_Roles_and_Media_Types)
    -   [<span class="tocnumber">2.2</span> <span class="toctext">DAP4
        Core Specification
        Documents</span>](https://docs.opendap.org/index.php?title=DAP4:_Specification_Volume_2#DAP4_Core_Specification_Documents)
    -   [<span class="tocnumber">2.3</span> <span
        class="toctext">Extensions to DAP4 Core
        Specifications</span>](https://docs.opendap.org/index.php?title=DAP4:_Specification_Volume_2#Extensions_to_DAP4_Core_Specifications)
-   [<span class="tocnumber">3</span> <span class="toctext">DAP4 Web
    Service
    Responses</span>](https://docs.opendap.org/index.php?title=DAP4:_Specification_Volume_2#DAP4_Web_Service_Responses)
    -   [<span class="tocnumber">3.1</span> <span class="toctext">DAP4
        Dataset Services
        Response</span>](https://docs.opendap.org/index.php?title=DAP4:_Specification_Volume_2#DAP4_Dataset_Services_Response)
        -   [<span class="tocnumber">3.1.1</span> <span
            class="toctext">DSR Resource
            Role</span>](https://docs.opendap.org/index.php?title=DAP4:_Specification_Volume_2#DSR_Resource_Role)
        -   [<span class="tocnumber">3.1.2</span> <span
            class="toctext">Normative Encoding of the
            DSR</span>](https://docs.opendap.org/index.php?title=DAP4:_Specification_Volume_2#Normative_Encoding_of_the_DSR)
        -   [<span class="tocnumber">3.1.3</span> <span
            class="toctext">Service
            Behavior</span>](https://docs.opendap.org/index.php?title=DAP4:_Specification_Volume_2#Service_Behavior)
            -   [<span class="tocnumber">3.1.3.1</span> <span
                class="toctext">Downgrading the Normative XML Encoding
                (Required)</span>](https://docs.opendap.org/index.php?title=DAP4:_Specification_Volume_2#Downgrading_the_Normative_XML_Encoding_.28Required.29)
        -   [<span class="tocnumber">3.1.4</span> <span
            class="toctext">Other Encodings of the
            DSR</span>](https://docs.opendap.org/index.php?title=DAP4:_Specification_Volume_2#Other_Encodings_of_the_DSR)
            -   [<span class="tocnumber">3.1.4.1</span> <span
                class="toctext">HTML Encoding
                (Optional)</span>](https://docs.opendap.org/index.php?title=DAP4:_Specification_Volume_2#HTML_Encoding_.28Optional.29)
    -   [<span class="tocnumber">3.2</span> <span
        class="toctext">Dataset Metadata
        Response</span>](https://docs.opendap.org/index.php?title=DAP4:_Specification_Volume_2#Dataset_Metadata_Response)
        -   [<span class="tocnumber">3.2.1</span> <span
            class="toctext">DMR Resource
            Role</span>](https://docs.opendap.org/index.php?title=DAP4:_Specification_Volume_2#DMR_Resource_Role)
        -   [<span class="tocnumber">3.2.2</span> <span
            class="toctext">Normative Encoding of the
            DMR</span>](https://docs.opendap.org/index.php?title=DAP4:_Specification_Volume_2#Normative_Encoding_of_the_DMR)
        -   [<span class="tocnumber">3.2.3</span> <span
            class="toctext">Service
            Behavior</span>](https://docs.opendap.org/index.php?title=DAP4:_Specification_Volume_2#Service_Behavior_2)
            -   [<span class="tocnumber">3.2.3.1</span> <span
                class="toctext">Downgrading the Normative XML Encoding
                (Required)</span>](https://docs.opendap.org/index.php?title=DAP4:_Specification_Volume_2#Downgrading_the_Normative_XML_Encoding_.28Required.29_2)
        -   [<span class="tocnumber">3.2.4</span> <span
            class="toctext">Other Encodings of the
            DMR</span>](https://docs.opendap.org/index.php?title=DAP4:_Specification_Volume_2#Other_Encodings_of_the_DMR)
            -   [<span class="tocnumber">3.2.4.1</span> <span
                class="toctext">HTML Encoding
                (Optional)</span>](https://docs.opendap.org/index.php?title=DAP4:_Specification_Volume_2#HTML_Encoding_.28Optional.29_2)
    -   [<span class="tocnumber">3.3</span> <span class="toctext">DAP4:
        Data
        Response</span>](https://docs.opendap.org/index.php?title=DAP4:_Specification_Volume_2#DAP4:_Data_Response)
        -   [<span class="tocnumber">3.3.1</span> <span
            class="toctext">Data Response Resource
            Role</span>](https://docs.opendap.org/index.php?title=DAP4:_Specification_Volume_2#Data_Response_Resource_Role)
        -   [<span class="tocnumber">3.3.2</span> <span
            class="toctext">Normative Encoding of the Data
            Response</span>](https://docs.opendap.org/index.php?title=DAP4:_Specification_Volume_2#Normative_Encoding_of_the_Data_Response)
        -   [<span class="tocnumber">3.3.3</span> <span
            class="toctext">Service
            Behavior</span>](https://docs.opendap.org/index.php?title=DAP4:_Specification_Volume_2#Service_Behavior_3)
        -   [<span class="tocnumber">3.3.4</span> <span
            class="toctext">Other Encodings of the Data
            Response</span>](https://docs.opendap.org/index.php?title=DAP4:_Specification_Volume_2#Other_Encodings_of_the_Data_Response)
            -   [<span class="tocnumber">3.3.4.1</span> <span
                class="toctext">Text Encoding
                (Optional)</span>](https://docs.opendap.org/index.php?title=DAP4:_Specification_Volume_2#Text_Encoding_.28Optional.29)
            -   [<span class="tocnumber">3.3.4.2</span> <span
                class="toctext">XML Encoding
                (Optional)</span>](https://docs.opendap.org/index.php?title=DAP4:_Specification_Volume_2#XML_Encoding_.28Optional.29)
            -   [<span class="tocnumber">3.3.4.3</span> <span
                class="toctext">NetCDF-3 Encoding
                (Optional)</span>](https://docs.opendap.org/index.php?title=DAP4:_Specification_Volume_2#NetCDF-3_Encoding_.28Optional.29)
            -   [<span class="tocnumber">3.3.4.4</span> <span
                class="toctext">NetCDF-4 Encoding
                (Optional)</span>](https://docs.opendap.org/index.php?title=DAP4:_Specification_Volume_2#NetCDF-4_Encoding_.28Optional.29)
    -   [<span class="tocnumber">3.4</span> <span class="toctext">DAP4
        Error
        Response</span>](https://docs.opendap.org/index.php?title=DAP4:_Specification_Volume_2#DAP4_Error_Response)
        -   [<span class="tocnumber">3.4.1</span> <span
            class="toctext">Error Response Resource
            Role</span>](https://docs.opendap.org/index.php?title=DAP4:_Specification_Volume_2#Error_Response_Resource_Role)
        -   [<span class="tocnumber">3.4.2</span> <span
            class="toctext">Normative Encoding of the Error
            Response</span>](https://docs.opendap.org/index.php?title=DAP4:_Specification_Volume_2#Normative_Encoding_of_the_Error_Response)
-   [<span class="tocnumber">4</span> <span
    class="toctext">HTTP</span>](https://docs.opendap.org/index.php?title=DAP4:_Specification_Volume_2#HTTP)
    -   [<span class="tocnumber">4.1</span> <span
        class="toctext">Content Negotiation and Media
        Types</span>](https://docs.opendap.org/index.php?title=DAP4:_Specification_Volume_2#Content_Negotiation_and_Media_Types)
    -   [<span class="tocnumber">4.2</span> <span
        class="toctext">Redirects</span>](https://docs.opendap.org/index.php?title=DAP4:_Specification_Volume_2#Redirects)
    -   [<span class="tocnumber">4.3</span> <span
        class="toctext">Caching of Responses and Conditional
        Requests</span>](https://docs.opendap.org/index.php?title=DAP4:_Specification_Volume_2#Caching_of_Responses_and_Conditional_Requests)
    -   [<span class="tocnumber">4.4</span> <span
        class="toctext">Authentication/Authorization</span>](https://docs.opendap.org/index.php?title=DAP4:_Specification_Volume_2#Authentication.2FAuthorization)
    -   [<span class="tocnumber">4.5</span> <span
        class="toctext">Headers</span>](https://docs.opendap.org/index.php?title=DAP4:_Specification_Volume_2#Headers)
        -   [<span class="tocnumber">4.5.1</span> <span
            class="toctext">Request
            Headers</span>](https://docs.opendap.org/index.php?title=DAP4:_Specification_Volume_2#Request_Headers)
            -   [<span class="tocnumber">4.5.1.1</span> <span
                class="toctext">General</span>](https://docs.opendap.org/index.php?title=DAP4:_Specification_Volume_2#General)
            -   [<span class="tocnumber">4.5.1.2</span> <span
                class="toctext">DAP
                Specific</span>](https://docs.opendap.org/index.php?title=DAP4:_Specification_Volume_2#DAP_Specific)
        -   [<span class="tocnumber">4.5.2</span> <span
            class="toctext">Response
            Headers</span>](https://docs.opendap.org/index.php?title=DAP4:_Specification_Volume_2#Response_Headers)
            -   [<span class="tocnumber">4.5.2.1</span> <span
                class="toctext">General</span>](https://docs.opendap.org/index.php?title=DAP4:_Specification_Volume_2#General_2)
            -   [<span class="tocnumber">4.5.2.2</span> <span
                class="toctext">DAP
                Specific</span>](https://docs.opendap.org/index.php?title=DAP4:_Specification_Volume_2#DAP_Specific_2)
    -   [<span class="tocnumber">4.6</span> <span class="toctext">Status
        Codes</span>](https://docs.opendap.org/index.php?title=DAP4:_Specification_Volume_2#Status_Codes)
        -   [<span class="tocnumber">4.6.1</span> <span
            class="toctext">200
            OK</span>](https://docs.opendap.org/index.php?title=DAP4:_Specification_Volume_2#200_OK)
        -   [<span class="tocnumber">4.6.2</span> <span
            class="toctext">400 Bad
            Request</span>](https://docs.opendap.org/index.php?title=DAP4:_Specification_Volume_2#400_Bad_Request)
            -   [<span class="tocnumber">4.6.2.1</span> <span
                class="toctext">400 Bad DAP4 Request
                Syntax</span>](https://docs.opendap.org/index.php?title=DAP4:_Specification_Volume_2#400_Bad_DAP4_Request_Syntax)
        -   [<span class="tocnumber">4.6.3</span> <span
            class="toctext">401
            Unauthorized</span>](https://docs.opendap.org/index.php?title=DAP4:_Specification_Volume_2#401_Unauthorized)
        -   [<span class="tocnumber">4.6.4</span> <span
            class="toctext">403
            Forbidden</span>](https://docs.opendap.org/index.php?title=DAP4:_Specification_Volume_2#403_Forbidden)
        -   [<span class="tocnumber">4.6.5</span> <span
            class="toctext">404 Not
            Found</span>](https://docs.opendap.org/index.php?title=DAP4:_Specification_Volume_2#404_Not_Found)
        -   [<span class="tocnumber">4.6.6</span> <span
            class="toctext">415 Unsupported Media
            Type</span>](https://docs.opendap.org/index.php?title=DAP4:_Specification_Volume_2#415_Unsupported_Media_Type)
        -   [<span class="tocnumber">4.6.7</span> <span
            class="toctext">500 Internal Server
            Error</span>](https://docs.opendap.org/index.php?title=DAP4:_Specification_Volume_2#500_Internal_Server_Error)
    -   [<span class="tocnumber">4.7</span> <span class="toctext">Verbs
        (aka
        Methods)</span>](https://docs.opendap.org/index.php?title=DAP4:_Specification_Volume_2#Verbs_.28aka_Methods.29)
        -   [<span class="tocnumber">4.7.1</span> <span
            class="toctext">GET</span>](https://docs.opendap.org/index.php?title=DAP4:_Specification_Volume_2#GET)
            -   [<span class="tocnumber">4.7.1.1</span> <span
                class="toctext">Examples</span>](https://docs.opendap.org/index.php?title=DAP4:_Specification_Volume_2#Examples)
-   [<span class="tocnumber">5</span> <span class="toctext">DAP4
    URLs</span>](https://docs.opendap.org/index.php?title=DAP4:_Specification_Volume_2#DAP4_URLs)
    -   [<span class="tocnumber">5.1</span> <span class="toctext">Query
        String
        Parameters</span>](https://docs.opendap.org/index.php?title=DAP4:_Specification_Volume_2#Query_String_Parameters)
-   [<span class="tocnumber">6</span> <span class="toctext">Normative
    References</span>](https://docs.opendap.org/index.php?title=DAP4:_Specification_Volume_2#Normative_References)
-   [<span class="tocnumber">7</span> <span
    class="toctext">Non-Normative
    References</span>](https://docs.opendap.org/index.php?title=DAP4:_Specification_Volume_2#Non-Normative_References)
-   [<span class="tocnumber">8</span> <span class="toctext">Appendix -
    Ancillary Web Services (Beyond
    DAP4)</span>](https://docs.opendap.org/index.php?title=DAP4:_Specification_Volume_2#Appendix_-_Ancillary_Web_Services_.28Beyond_DAP4.29)
    -   [<span class="tocnumber">8.1</span> <span class="toctext">DAP4:
        HTML DATA Request Form
        Service</span>](https://docs.opendap.org/index.php?title=DAP4:_Specification_Volume_2#DAP4:_HTML_DATA_Request_Form_Service)
    -   [<span class="tocnumber">8.2</span> <span class="toctext">DAP4:
        RDF
        Service</span>](https://docs.opendap.org/index.php?title=DAP4:_Specification_Volume_2#DAP4:_RDF_Service)
    -   [<span class="tocnumber">8.3</span> <span class="toctext">DAP4:
        ISO 19115
        Service</span>](https://docs.opendap.org/index.php?title=DAP4:_Specification_Volume_2#DAP4:_ISO_19115_Service)
    -   [<span class="tocnumber">8.4</span> <span class="toctext">DAP4:
        ISO Conformance Score
        Service</span>](https://docs.opendap.org/index.php?title=DAP4:_Specification_Volume_2#DAP4:_ISO_Conformance_Score_Service)
    -   [<span class="tocnumber">8.5</span> <span class="toctext">DAP4:
        NetCDF File-out
        Service</span>](https://docs.opendap.org/index.php?title=DAP4:_Specification_Volume_2#DAP4:_NetCDF_File-out_Service)
    -   [<span class="tocnumber">8.6</span> <span class="toctext">DAP4:
        ASCII Data
        Service</span>](https://docs.opendap.org/index.php?title=DAP4:_Specification_Volume_2#DAP4:_ASCII_Data_Service)
    -   [<span class="tocnumber">8.7</span> <span class="toctext">DAP4:
        XML Data
        Service</span>](https://docs.opendap.org/index.php?title=DAP4:_Specification_Volume_2#DAP4:_XML_Data_Service)
    -   [<span class="tocnumber">8.8</span> <span class="toctext">DAP4:
        Native File Access
        Service</span>](https://docs.opendap.org/index.php?title=DAP4:_Specification_Volume_2#DAP4:_Native_File_Access_Service)
    -   [<span class="tocnumber">8.9</span> <span class="toctext">DAP4:
        Server Version
        Service</span>](https://docs.opendap.org/index.php?title=DAP4:_Specification_Volume_2#DAP4:_Server_Version_Service)
    -   [<span class="tocnumber">8.10</span> <span class="toctext">DAP2
        Services</span>](https://docs.opendap.org/index.php?title=DAP4:_Specification_Volume_2#DAP2_Services)
        -   [<span class="tocnumber">8.10.1</span> <span
            class="toctext">DAP2: Data
            Service</span>](https://docs.opendap.org/index.php?title=DAP4:_Specification_Volume_2#DAP2:_Data_Service)
        -   [<span class="tocnumber">8.10.2</span> <span
            class="toctext">DAP2: DDX
            Service</span>](https://docs.opendap.org/index.php?title=DAP4:_Specification_Volume_2#DAP2:_DDX_Service)
        -   [<span class="tocnumber">8.10.3</span> <span
            class="toctext">DAP2: DDS
            Service</span>](https://docs.opendap.org/index.php?title=DAP4:_Specification_Volume_2#DAP2:_DDS_Service)
        -   [<span class="tocnumber">8.10.4</span> <span
            class="toctext">DAP2: DAS
            Service</span>](https://docs.opendap.org/index.php?title=DAP4:_Specification_Volume_2#DAP2:_DAS_Service)
        -   [<span class="tocnumber">8.10.5</span> <span
            class="toctext">DAP2: ASCII Data
            Service</span>](https://docs.opendap.org/index.php?title=DAP4:_Specification_Volume_2#DAP2:_ASCII_Data_Service)
        -   [<span class="tocnumber">8.10.6</span> <span
            class="toctext">DAP2: JSON Data
            Service</span>](https://docs.opendap.org/index.php?title=DAP4:_Specification_Volume_2#DAP2:_JSON_Data_Service)
        -   [<span class="tocnumber">8.10.7</span> <span
            class="toctext">DAP2: Info
            Service</span>](https://docs.opendap.org/index.php?title=DAP4:_Specification_Volume_2#DAP2:_Info_Service)
        -   [<span class="tocnumber">8.10.8</span> <span
            class="toctext">DAP2: NetCDF
            Service</span>](https://docs.opendap.org/index.php?title=DAP4:_Specification_Volume_2#DAP2:_NetCDF_Service)

## <span id="Introduction" class="mw-headline"><span class="mw-headline-number">1</span> Introduction</span>

This document defines the DAP4 Web Service protocol which DAP4-compliant
software MUST support when utilizing the HTTP protocol to transmit DAP4
requests and responses, along with additional optional services that
DAP4-compliant software SHOULD support.

The DAP4 protocol uses three basic responses to represent a data
resource. One response, the Dataset Metadata Response (DMR) contains
metadata information describing the structure of the data resource. That
is, it characterizes the variables, their datatypes, names and
attributes. The second response, the Data Response (DataDMR), contains
both the metadata about the requested data and the actual data that was
requested. The third basic response is the Dataset Services Response
(DSR) that provides a listing of services, any alternate media
representations if available, and all of the associated access URI's for
a particular data resource.

The DAP4 protocol uses a fourth basic resource, the Constraint/Query
Expression (CE), to represent subsetting of and, possibly,
transformations of the dataset requested.

The DAP4 protocol uses a fifth basic resource, the Error Response (ER),
to allow servers to communicate error information with clients. When a
request for any of the three basic responses cannot be completed, an
Error response is returned. If an error occurs before the standard
response is initiated, an error response is returned in place of the
standard response. If an error occurs after a data response has been
initiated, an Error Response is returned as the final chunked record as
described in Section 7 "DAP4 Chunked Data Representation" of the DAP4
Data Model
document.<sup>\[[DAP4\ Vol.1](https://docs.opendap.org/index.php?title=DAP4:_Specification_Volume_2#DAP4_Vol1)\]</sup>

The DAP4 Data Model, constraint/query language, dataset metadata XML
encoding, and binary data encoding are all defined in the DAP4 Volume 1:
"Data Model, Persistent Representations, and Constraints"
document.<sup>\[[DAP4\ Vol.1](https://docs.opendap.org/index.php?title=DAP4:_Specification_Volume_2#DAP4_Vol1)\]</sup>

Each of the three responses (Dataset Metadata, Data, and Dataset
Services) are complete in and of themselves so that, for example, the
Data response can be used by a client without ever requesting either of
the two other responses. In many cases, client programs will request the
Dataset Metadata response before requesting the Data response but there
is no requirement they do so and servers SHALL NOT require that behavior
on the part of clients.

These three standard dataset responses can each be accessed in two
different ways. First, similar to DAP2 URL construction and to support
client-driven content negotiation (see the section titled ["HTTP -
Content Negotiation and Media
Types"](https://docs.opendap.org/index.php?title=DAP4:_Specification_Volume_2#Content_Negotiation_and_Media_Types)
below), each dataset resource has a standard URL suffix that can be
added to the DAP4 dataset URL to retrieve the resource in its standard
(normative) encoding. This allows clients, given a base DAP4 dataset
URL, to construct DAP4 URLs in a simple and standard way for each of the
three standard dataset resources.

Second, to support server-driven content negotiation (see the ["HTTP -
Content Negotiation and Media
Types"](https://docs.opendap.org/index.php?title=DAP4:_Specification_Volume_2#Content_Negotiation_and_Media_Types)
section below) and hypermedia-driven style, a DAP4 resource role is
defined for each standard dataset resource and a DAP4 media type is
defined for each dataset resource encoding scheme.

Any particular instance of a DAP4 server MAY have one or more additional
services, alternate media representations of service responses, or
unique (to the server instance) server side functions. All of these
things, including the core services and their default representations
MUST be included in the *Dataset Services
Response*.<sup>\[[DAP4\ DSR](https://docs.opendap.org/index.php?title=DAP4:_Specification_Volume_2#DAP4_DSR)\]</sup>

The DAP4 web service is currently limited to HTTP GET requests though it
is expected that extensions (e.g., asynchronous access) will use other
HTTP methods (e.g., POST). This makes, for now, the DAP4 Constraint
Expression something of a pseudo-resource type given that they are
encoded as part of the URL query string rather than as an independent
document.

  

## <span id="Terms_and_Definitions" class="mw-headline"><span class="mw-headline-number">2</span> Terms and Definitions</span>

Dataset Service Response (DSR)  
The DAP4 response type that contains a list of DAP (and other) services
available for the dataset including any alternate media representations
and all the associated access URIs.

Dataset Metadata Response (DMR)  
The DAP4 response type that contains metadata information describing the
structure of the requested data. The metadata information characterizes
the requested data variables including their names, data types, shapes,
and attributes.

Dataset Data Response (Data)  
The DAP4 response type that contains both the dataset metadata and the
binary data for the requested data.

Resource role ID  
A URI that identifies the role of a resource, generally provided with a
link to allow clients to identify the type of resource the link
references. (For instance, an "atom:link" element has an optional
"atom:rel" attribute.)

Media Type  
A internet media type is a two-part identifier for resource encoding
schemes, e.g. "text/html", "text/plain", "application/octet-stream".
(See [section 1.1 DAP4 Resource Roles and Media
Types](https://docs.opendap.org/index.php?title=DAP4:_Specification_Volume_2#MediaTypes)
of this document)

DAP4 Constraint Expression (CE)  
The constraint expression that encapsulates various sub-setting of, and
possibly the application of server side functions to variables in a DAP4
dataset.

Query String (QS)  
Everything after the "`?`" character in a URL.

### <span id="DAP4_Resource_Roles_and_Media_Types" class="mw-headline"><span class="mw-headline-number">2.1</span> DAP4 Resource Roles and Media Types</span>

The standard DAP4 dataset resource roles and encodings (plus a few
alternate encodings) that are defined in the core DAP4 documents are:

**Dataset Services Response (DSR)**

> <table class="wikitable" style="font-size: 95%;" width="90%">
> <tbody>
> <tr class="header">
> <th style="text-align: left;">Resource Role</th>
> </tr>
>
> <tr class="odd">
> <td
> style="text-align: left;"><strong>http://services.opendap.org/dap4/dataset-service</strong></td>
> </tr>
> </tbody>
> </table>
>
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
> <td><em>none</em> or "<strong>.dsr</strong>"</td>
> <td><dl>
> <dt>application/vnd.opendap.dap4.dataset-services+xml</dt>
> <dd>
> Normative DSR encoding
> </dd>
> </dl></td>
> <td>http://server/path/dataset.nc
> <p>http://server/path/dataset.nc<strong>.dsr</strong></p></td>
> </tr>
> <tr class="even">
> <td>"<strong>.xml</strong>" or "<strong>.dsr.xml</strong>"</td>
> <td><dl>
> <dt>text/xml</dt>
> <dd>
> Normative DSR encoding with generic media type
> </dd>
> </dl></td>
> <td>http://server/path/dataset.nc<strong>.xml</strong>
> <p>http://server/path/dataset.nc<strong>.dsr.xml</strong></p></td>
> </tr>
> <tr class="odd">
> <td>"<strong>.html</strong>" or "<strong>.dsr.html</strong>"</td>
> <td><dl>
> <dt>text/html</dt>
> <dd>
> HTML DSR encoding
> </dd>
> </dl></td>
> <td>http://server/path/dataset.nc<strong>.html</strong>
> <p>http://server/path/dataset.nc<strong>.dsr.html</strong></p></td>
> </tr>
> </tbody>
> </table>

**Dataset Metadata Response (DMR)**

> <table class="wikitable" style="font-size: 95%;" width="90%">
> <tbody>
> <tr class="header">
> <th style="text-align: left;">Resource Role</th>
> </tr>
>
> <tr class="odd">
> <td
> style="text-align: left;"><strong>http://services.opendap.org/dap4/dataset-metadata</strong></td>
> </tr>
> </tbody>
> </table>
>
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
> <td>"<strong>.dmr</strong>"</td>
> <td><dl>
> <dt>application/vnd.opendap.dap4.dataset-metadata+xml</dt>
> <dd>
> Normative DMR encoding
> </dd>
> </dl></td>
> <td>http://server/path/dataset.nc<strong>.dmr</strong></td>
> </tr>
> <tr class="even">
> <td>"<strong>.dmr.xml</strong>"</td>
> <td><dl>
> <dt>text/xml</dt>
> <dd>
> Normative DMR encoding with generic media type
> </dd>
> </dl></td>
> <td>http://server/path/dataset.nc<strong>.dmr.xml</strong></td>
> </tr>
> <tr class="odd">
> <td>"<strong>.dmr.html</strong>"</td>
> <td><dl>
> <dt>text/html</dt>
> <dd>
> HTML DMR encoding
> </dd>
> </dl></td>
> <td>http://server/path/dataset.nc<strong>.dmr.html</strong></td>
> </tr>
> </tbody>
> </table>

**Dataset Data Response (Data)**

> <table class="wikitable" style="font-size: 95%;" width="90%">
> <tbody>
> <tr class="header">
> <th style="text-align: left;">Resource Role</th>
> </tr>
>
> <tr class="odd">
> <td
> style="text-align: left;"><strong>http://services.opendap.org/dap4/data</strong></td>
> </tr>
> </tbody>
> </table>
>
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
> <td>"<strong>.dap</strong>"</td>
> <td><dl>
> <dt>application/vnd.opendap.dap4.data</dt>
> <dd>
> Normative Data encoding
> </dd>
> </dl></td>
> <td>http://server/path/dataset.nc<strong>.dap</strong></td>
> </tr>
> <tr class="even">
> <td>"<strong>.dap.txt</strong>"</td>
> <td><dl>
> <dt>text/plain</dt>
> <dd>
> Text (UTF-8) Data encoding
> </dd>
> </dl></td>
> <td>http://server/path/dataset.nc<strong>.dap.txt</strong></td>
> </tr>
> <tr class="odd">
> <td>"<strong>.dap.xml</strong>"</td>
> <td><dl>
> <dt>text/xml</dt>
> <dd>
> XML Data encoding
> </dd>
> </dl></td>
> <td>http://server/path/dataset.nc<strong>.dap.xml</strong></td>
> </tr>
> </tbody>
> </table>

**Error Response (ER)**

> <table class="wikitable" style="font-size: 95%;" width="90%">
> <tbody>
> <tr class="header">
> <th style="text-align: left;">Resource Role</th>
> </tr>
>
> <tr class="odd">
> <td
> style="text-align: left;"><strong>http://services.opendap.org/dap4/error</strong></td>
> </tr>
> </tbody>
> </table>
>
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
> <td>N/A</td>
> <td><dl>
> <dt>application/vnd.opendap.dap4.error+xml</dt>
> <dd>
> Normative Error encoding
> </dd>
> </dl></td>
> <td>N/A</td>
> </tr>
> <tr class="even">
> <td>N/A</td>
> <td><dl>
> <dt>text/xml</dt>
> <dd>
> Normative Error encoding with generic media type
> </dd>
> </dl></td>
> <td>N/A</td>
> </tr>
> <tr class="odd">
> <td>N/A</td>
> <td><dl>
> <dt>text/html</dt>
> <dd>
> HTML Error encoding
> </dd>
> </dl></td>
> <td>N/A</td>
> </tr>
> </tbody>
> </table>

### <span id="DAP4_Core_Specification_Documents" class="mw-headline"><span class="mw-headline-number">2.2</span> DAP4 Core Specification Documents</span>

-   DAP4 Volume 1: "Data Model, Persistence Representations, and
    Constraints"
-   DAP4 Web Service (this document)
-   DAP4 Dataset Services
-   DAP4 Requirements for Server-side Functions

### <span id="Extensions_to_DAP4_Core_Specifications" class="mw-headline"><span class="mw-headline-number">2.3</span> Extensions to DAP4 Core Specifications</span>

Several types of extensions can be made to the DAP4 core including:

-   New encodings for the core DAP4 response types
-   New response types
-   New server-side functions.

## <span id="DAP4_Web_Service_Responses" class="mw-headline"><span class="mw-headline-number">3</span> DAP4 Web Service Responses</span>

The core of the DAP4 Web Service protocol consists of the four standard
response types: Dataset Services Response (DSR), Dataset Metadata
Response (DMR), Dataset Data Response (Data), DAP4 Error Response
(Error) Each dataset served by a DAP4 compliant server MUST provide the
DSR, DMR, and Data responses and MUST return errors documents as DAP4
Error Responses.

All of the example requests described below are based on the DAP4
dataset URL:

<a href="http://server.org:8080/dap/path/data.nc" class="external free"
rel="nofollow">http://server.org:8080/dap/path/data.nc</a>

### <span id="DAP4_Dataset_Services_Response" class="mw-headline"><span class="mw-headline-number">3.1</span> DAP4 Dataset Services Response</span>

The DAP4 Dataset Services Response
(DSR)<sup>\[[DAP4\ DSR](https://docs.opendap.org/index.php?title=DAP4:_Specification_Volume_2#DAP4_DSR)\]</sup>
provides clients with a listing of all available DAP4 services and all
the available encodings for those services as well as all available DAP4
extensions.

Each service (or response type) has a unique resource role (defined in
the appropriate specification), each link (alternate representation) for
a given service MUST fulfill that same role. This is not always a clear
distinction to make. For example, the DAP4 Dataset Metadata Response can
be mapped into ISO 19115 metadata. However, IS0 19115 is clearly a
different domain.

The DAP4 Dataset Services Response MUST contain the following
information:

-   List of DAP versions supported by server
-   The implementation version (e.g., "TDS 4.3.57" or "Hyrax 1.7.45")
-   List of all available DAP4 services for the dataset
-   For each DAP4 services listed, a list of all available links each
    with its corresponding media type
-   List of supported extensions
    -   Resource type extensions
    -   Media type extensions
    -   Server-side function extensions

If SHOULD contain the following information:

-   A human readable title for the dataset
-   A human readable title for each service

To take advantage of web caching, servers should try to keep DSRs light
weight (i.e., quick creation) and as stable as possible.

#### <span id="DSR_Resource_Role" class="mw-headline"><span class="mw-headline-number">3.1.1</span> DSR Resource Role</span>

DSRs are identified by the resource role:

**`http://services.opendap.org/dap4/dataset-services`**

#### <span id="Normative_Encoding_of_the_DSR" class="mw-headline"><span class="mw-headline-number">3.1.2</span> Normative Encoding of the DSR</span>

The normative XML representation for the Dataset Services Response is
defined in the "Normative XML Encoding of the DSR" appendix. The media
type for the normative XML representation is

`application/vnd.opendap.dataset-services+xml`

#### <span id="Service_Behavior" class="mw-headline"><span class="mw-headline-number">3.1.3</span> Service Behavior</span>

When an HTTP GET request is made on a base DAP4 dataset URL, all DAP4
servers MUST return the normative XML encoding of the DSR given these
conditions:

-   the request "Accept" header contains only the normative XML encoding
    media type,
-   the request "Accept" header equals "\*/\*", or
-   the request "Accept" header does not indicate a preference for
    another media type in which the server knows how to encode the DSR.

For example, the request:

    GET /dap/path/data.nc HTTP/1.1
    Host: server.org:8080
    Accept: */*

Might result in the following response:

    HTTP/1.1 200 OK
    Content-Type: application/vnd.opendap.dataset-services+xml
    Date: ...

##### <span id="Downgrading_the_Normative_XML_Encoding_(Required)"></span><span id="Downgrading_the_Normative_XML_Encoding_.28Required.29" class="mw-headline"><span class="mw-headline-number">3.1.3.1</span> Downgrading the Normative XML Encoding (Required)</span>

When an HTTP GET request is made on a base DAP dataset URL with the
suffix `.xml`  
added to it:

request url = `dataset_url.xml`  

the response MUST be the normative representation of the DSR along with
the HTTP `Content-Type` header set to `text/xml` . For example:

    GET /dap/path/data.nc.xml HTTP/1.1
    Host: server.org:8080
    Accept: */*

Might result in the following response:

    HTTP/1.1 200 OK
    Content-Type: text/xml; charset=utf-8
    Date: ...

The normative XML representation MUST also be returned when an HTTP GET
request is made on a base DAP4 dataset URL (without a suffix) and the
server uses server-driven content negotiation to decide that the best
response for the client would be an HTML encoded DSR. For example:

    GET /dap/path/data.nc HTTP/1.1
    Host: server.org:8080
    Accept: text/xml

#### <span id="Other_Encodings_of_the_DSR" class="mw-headline"><span class="mw-headline-number">3.1.4</span> Other Encodings of the DSR</span>

##### <span id="HTML_Encoding_(Optional)"></span><span id="HTML_Encoding_.28Optional.29" class="mw-headline"><span class="mw-headline-number">3.1.4.1</span> HTML Encoding (Optional)</span>

When an HTTP GET request is made on a base DAP dataset URL with the
suffix `.html`  
added to it:

request url = `dataset_url.html`  

the server MUST reply with an HTML representation of the DSR, **or**
return an HTTP status of 404 to indicate that an HTML representation of
the DSR is not available. For example:

    GET /dap/path/data.nc.html HTTP/1.1
    Host: server.org:8080
    Accept: */*

Might result in the following response:

    HTTP/1.1 200 OK
    Content-Type: text/html; charset=utf-8
    Date: ...

If available, the HTML representation MUST also be returned when an HTTP
GET request is made on a base DAP4 dataset URL (without a suffix) and
the server uses server-driven content negotiation to decide that the
best response for the client would be an HTML encoded DSR. For example
this request:

    GET /dap/path/data.nc HTTP/1.1
    Host: server.org:8080
    Accept: text/html

Must return the HTML representation of the DMR, if available. If no such
representation is available then the server MAY return an HTTP status of
404 or even 415.

### <span id="Dataset_Metadata_Response" class="mw-headline"><span class="mw-headline-number">3.2</span> Dataset Metadata Response</span>

The Dataset Metadata Service returns the Dataset Metadata Response (DMR)
which is a metadata description of the dataset. The normative
representation of the DMR is an XML document that contains both the
'syntactic' (structural) and 'semantic' metadata for the dataset,
persisted as a DAP4 data model representation of the dataset held at the
server.<sup>\[[DAP4\_Vol1](https://docs.opendap.org/index.php?title=DAP4:_Specification_Volume_2#DAP4_Vol1)\]</sup>
The DMR service accepts a query string (constraint expression) that
allows you to inspect the effects on the data structures when
sub-setting and/or server side functions are applied. If a constraint
expression has been successfully applied, the service will returned the
constrained view of the dap:Dataset object. The constrained view may
contain different data structures than the unconstrained view as the
constraint may alter the reasonable representation of the data set. Note
that all dap:Attribute objects have been removed from constrained
dap:Dataset objects. More information on the syntax of DAP4 constraint
expressions can be found in Volume 1 of the DAP4 specification.
<sup>\[[DAP4\_Vol1](https://docs.opendap.org/index.php?title=DAP4:_Specification_Volume_2#DAP4_Vol1)\]</sup>

#### <span id="DMR_Resource_Role" class="mw-headline"><span class="mw-headline-number">3.2.1</span> DMR Resource Role</span>

DMRs are identified by the resource role:

**`http://services.opendap.org/dap4/dataset-metadata`**

#### <span id="Normative_Encoding_of_the_DMR" class="mw-headline"><span class="mw-headline-number">3.2.2</span> Normative Encoding of the DMR</span>

The normative XML representation for the Dataset Metadata Response is
defined in Volume 1 of the DAP4
specification.<sup>\[[DAP4\_Vol1](https://docs.opendap.org/index.php?title=DAP4:_Specification_Volume_2#DAP4_Vol1)\]</sup>
The media type for the normative XML representation is:

`application/vnd.opendap.dap4.dataset-metadata+xml`  

#### <span id="Service_Behavior_2" class="mw-headline"><span class="mw-headline-number">3.2.3</span> Service Behavior</span>

Every DAP4 compliant server MUST return the normative representation of
the Dataset Metadata Response (an XML document described Volume 1 of the
DAP4 specification
<sup>\[[DAP4\_Vol1](https://docs.opendap.org/index.php?title=DAP4:_Specification_Volume_2#DAP4_Vol1)\]</sup>)
when a client attempts to access a dataset URL with the suffix "`.dmr`"
appended to it. The DAP4 server MAY return alternate representations if
the client indicates that it can accept them and the server can provide
them.

When an HTTP GET request is made on a base DAP dataset URL with the
suffix `.dmr` added to it:

request url = `dataset_url + '.dmr'+ [?dap_constraint]`  

the server MUST reply with an normative representation of the DMR for
the (possibly constrained) dataset given these conditions:

-   the request "Accept" header contains only the normative XML encoding
    media type (`application/vnd.opendap.dap4.dataset-metadata+xml`),
-   the request "Accept" header equals "\*/\*", or
-   the request "Accept" header does not indicate a preference for
    another media type in which the server knows how to encode the DMR.

For example, the request:

    GET /dap/path/data.nc.dmr HTTP/1.1
    Host: server.org:8080
    Accept: */*

Might result in the following response:

    HTTP/1.1 200 OK
    Content-Type: application/vnd.opendap.dataset-metadata+xml
    Date: ...

##### <span id="Downgrading_the_Normative_XML_Encoding_(Required)_2"></span><span id="Downgrading_the_Normative_XML_Encoding_.28Required.29_2" class="mw-headline"><span class="mw-headline-number">3.2.3.1</span> Downgrading the Normative XML Encoding (Required)</span>

While the normative representation of the the Dataset Metadata response
is already an XML document, the normative media type is
`application/vnd.opendap.dataset-metadata+xml` which may be unfamiliar
to many generic clients (such as web browsers) and it is quite
conceivable that such a client might ask for the more generic `text/xml`
media type.

When an HTTP GET request is made on a DAP DMR URL with the suffix
`.xml`  
added to it:

request url = `dataset_url.dmr.xml`  

the response MUST be the normative representation of the DMR along with
the HTTP `Content-Type` header set to `text/xml` . For example:

    GET /dap/path/data.nc.dmr.xml HTTP/1.1
    Host: server.org:8080
    Accept: */*

Might result in the following response:

    HTTP/1.1 200 OK
    Content-Type: text/xml; charset=utf-8
    Date: ...

The normative XML representation of the DMR MUST also be returned when
an HTTP GET request is made on a base DAP4 DMR URL ( and the server uses
server-driven content negotiation to decide that the best response for
the client would be an HTML encoded DSR. For example:

    GET /dap/path/data.nc.dmr HTTP/1.1
    Host: server.org:8080
    Accept: text/xml

#### <span id="Other_Encodings_of_the_DMR" class="mw-headline"><span class="mw-headline-number">3.2.4</span> Other Encodings of the DMR</span>

##### <span id="HTML_Encoding_(Optional)_2"></span><span id="HTML_Encoding_.28Optional.29_2" class="mw-headline"><span class="mw-headline-number">3.2.4.1</span> HTML Encoding (Optional)</span>

When an HTTP GET request is made on a DAP DMR URL with the suffix
`.html`  
added to it:

request url = `dataset_url.dmr.html`  

the server MUST reply with an HTML representation of the DMR, **or**
return an HTTP status of 404 (or 415) to indicate that an HTML
representation of the DMR is not available. For example:

    GET /dap/path/data.nc.dmr.html HTTP/1.1
    Host: server.org:8080
    Accept: */*

Might result in the following response:

    HTTP/1.1 200 OK
    Content-Type: text/html; charset=utf-8
    Date: ...

If available, the HTML representation MUST also be returned when an HTTP
GET request is made on a base DAP4 DMR URL (without an additional
suffix) and the server uses server-driven content negotiation to decide
that the best response for the client would be an HTML encoded DMR. For
example this request:

    GET /dap/path/data.nc.dmr HTTP/1.1
    Host: server.org:8080
    Accept: text/html

Must return the HTML representation of the DMR, if available. If no such
representation is available then the server MAY return an HTTP status of
404 or even 415.

### <span id="DAP4:_Data_Response" class="mw-headline"><span class="mw-headline-number">3.3</span> DAP4: Data Response</span>

The Data Service provides DAP4 data access to a dataset, and is the
(primary) way that DAP4 returns data to a client. The Data service
accepts a query string (constraint expression) which allows you to
subset the data and invoke server side functions. When the service is
invoked it returns the DAP4 data object. On the wire this is a binary
document with MIME type *application/vnd.opendap.dap4.data*. The payload
is broken into two logical parts: A DMR-type xml document that describes
the data and a BLOB that contains the actual data. For more on the
information on the Data response and the internal structure of its
payload along with a complete discussion of the DAP4 constraint
expression syntax see Volume 1 of the DAP4
specification.<sup>\[[DAP4\_Vol1](https://docs.opendap.org/index.php?title=DAP4:_Specification_Volume_2#DAP4_Vol1)\]</sup>

#### <span id="Data_Response_Resource_Role" class="mw-headline"><span class="mw-headline-number">3.3.1</span> Data Response Resource Role</span>

DAP4 Data Responses are identified by the resource role:

**`http://services.opendap.org/dap4/data`**

#### <span id="Normative_Encoding_of_the_Data_Response" class="mw-headline"><span class="mw-headline-number">3.3.2</span> Normative Encoding of the Data Response</span>

The normative XML representation for the Data Response is defined in
Volume 1 of the DAP4
specification.<sup>\[[DAP4\_Vol1](https://docs.opendap.org/index.php?title=DAP4:_Specification_Volume_2#DAP4_Vol1)\]</sup>
The media type for the normative XML representation is:

`application/vnd.opendap.dap4.data`  

  

#### <span id="Service_Behavior_3" class="mw-headline"><span class="mw-headline-number">3.3.3</span> Service Behavior</span>

Every DAP4 compliant server MUST return the normative representation of
the Data Response when a client attempts to access a dataset URL with
the suffix "`.dap`" appended to it. The DAP4 server MAY return alternate
representations if the client indicates that it can accept them and the
server can provide them. The normative representation of the Data
Response is described in Volume 1 of the DAP4
specification.<sup>\[[DAP4\_Vol1](https://docs.opendap.org/index.php?title=DAP4:_Specification_Volume_2#DAP4_Vol1)\]</sup>

When an HTTP GET request is made on a base DAP dataset URL with the
suffix `.dap` added to it:

request url = `dataset_url + '.dap'+ [?dap_constraint]`  

the server MUST reply with an normative representation of the (possibly
constrained) data response for the dataset given these conditions:

-   the request "Accept" header contains only the normative XML encoding
    media type (`application/vnd.opendap.dap4.data`),
-   the request "Accept" header equals "\*/\*", or
-   the request "Accept" header does not indicate a preference for
    another media type in which the server knows how to encode the Data
    Response.

For example, the request:

    GET /dap/path/data.nc.dap HTTP/1.1
    Host: server.org:8080
    Accept: */*

Might result in the following response:

    HTTP/1.1 200 OK
    Content-Type: application/vnd.opendap.data
    Date: ...

#### <span id="Other_Encodings_of_the_Data_Response" class="mw-headline"><span class="mw-headline-number">3.3.4</span> Other Encodings of the Data Response</span>

##### <span id="Text_Encoding_(Optional)"></span><span id="Text_Encoding_.28Optional.29" class="mw-headline"><span class="mw-headline-number">3.3.4.1</span> Text Encoding (Optional)</span>

When an HTTP GET request is made on a DAP Data Response URL with the
suffix `.txt`  
added to it:

request url = `dataset_url.dap.txt`  

the server MUST reply with the text representation of the Data Response
using the utf-8 character set, **or** return an HTTP status of 404 (or
415) to indicate that a text representation of the Data Response is not
available. For example:

    GET /dap/path/data.nc.dap.txt HTTP/1.1
    Host: server.org:8080
    Accept: */*

Might result in the following response:

    HTTP/1.1 200 OK
    Content-Type: text/plain; charset=utf-8
    Date: ...

If available, the text representation MUST also be returned when an HTTP
GET request is made on a base DAP4 Data Response URL (without an
additional suffix) and the server uses server-driven content negotiation
to decide that the best response for the client would be an text encoded
Data Response. For example this request:

    GET /dap/path/data.nc.dap HTTP/1.1
    Host: server.org:8080
    Accept: text/plain

Must return the text representation of the Data Response, if available.
If no such representation is available then the server MAY return an
HTTP status of 404 or even 415.

##### <span id="XML_Encoding_(Optional)"></span><span id="XML_Encoding_.28Optional.29" class="mw-headline"><span class="mw-headline-number">3.3.4.2</span> XML Encoding (Optional)</span>

When an HTTP GET request is made on a DAP Data Response URL with the
suffix `.xml`  
added to it:

request url = `dataset_url.dap.xml`  

the server MUST reply with the XML representation of the Data Response,
**or** return an HTTP status of 404 (or 415) to indicate that an XML
representation of the Data Response is not available. For example:

    GET /dap/path/data.nc.dap.xml HTTP/1.1
    Host: server.org:8080
    Accept: */*

Might result in the following response:

    HTTP/1.1 200 OK
    Content-Type: text/xml; charset=utf-8
    Date: ...

If available, the XML representation MUST also be returned when an HTTP
GET request is made on a base DAP4 Data Response URL (without an
additional suffix) and the server uses server-driven content negotiation
to decide that the best response for the client would be an XML encoded
data response. For example this request:

    GET /dap/path/data.nc.dap HTTP/1.1
    Host: server.org:8080
    Accept: text/xml

Must return the XML representation of the Data Response, if available.
If no such representation is available then the server MAY return an
HTTP status of 404 or even 415.

##### <span id="NetCDF-3_Encoding_(Optional)"></span><span id="NetCDF-3_Encoding_.28Optional.29" class="mw-headline"><span class="mw-headline-number">3.3.4.3</span> NetCDF-3 Encoding (Optional)</span>

When an HTTP GET request is made on a DAP Data Response URL with the
suffix `.nc`  
added to it:

request url = `dataset_url.dap.nc`  

the server MUST reply with a NetCDF-3 representation of the Data
Response, **or** return an HTTP status of 404 (or 415) to indicate that
a NetCDF-3 representation of the Data Response is not available. For
example:

    GET /dap/path/data.nc.dap.nc HTTP/1.1
    Host: server.org:8080
    Accept: */*

Might result in the following response:

    HTTP/1.1 200 OK
    Content-Type: application/x-netcdf
    Date: ...

If available, the NetCDF-3 representation MUST also be returned when an
HTTP GET request is made on a base DAP4 Data Response URL (without an
additional suffix) and the server uses server-driven content negotiation
to decide that the best response for the client would be an NetCDF-3
encoded data response. For example this request:

    GET /dap/path/data.nc.dap HTTP/1.1
    Host: server.org:8080
    Accept: application/x-netcdf

Must return the NetCDF-3 representation of the Data Response, if
available. If no such representation is available then the server MAY
return an HTTP status of 404 or even 415.

##### <span id="NetCDF-4_Encoding_(Optional)"></span><span id="NetCDF-4_Encoding_.28Optional.29" class="mw-headline"><span class="mw-headline-number">3.3.4.4</span> NetCDF-4 Encoding (Optional)</span>

When an HTTP GET request is made on a DAP Data Response URL with the
suffix `.nc4`  
added to it:

request url = `dataset_url.dap.nc4`  

the server MUST reply with a NetCDF-4 representation of the Data
Response, **or** return an HTTP status of 404 (or 415) to indicate that
a NetCDF-4 representation of the Data Response is not available. For
example:

    GET /dap/path/data.nc.dap.nc HTTP/1.1
    Host: server.org:8080
    Accept: */*

Might result in the following response:

    HTTP/1.1 200 OK
    Content-Type: application/x-netcdf;ver=4
    Date: ...

If available, the NetCDF-4 representation MUST also be returned when an
HTTP GET request is made on a base DAP4 Data Response URL (without an
additional suffix) and the server uses server-driven content negotiation
to decide that the best response for the client would be an NetCDF-4
encoded data response. For example this request:

    GET /dap/path/data.nc.dap HTTP/1.1
    Host: server.org:8080
    Accept: application/x-netcdf;ver=4

Must return the NetCDF-4 representation of the Data Response, if
available. If no such representation is available then the server MAY
return an HTTP status of 404 or even 415.

  

### <span id="DAP4_Error_Response" class="mw-headline"><span class="mw-headline-number">3.4</span> [DAP4 Error Response](https://docs.opendap.org/index.php?title=DAP4_Error_Response "DAP4 Error Response")</span>

The DAP4 protocol returns error information using an Error response. If
a request for any of the three basic responses cannot be completed then
an Error response is returned in its place.

The normative XML representation for the Error Response is defined by
the following RELAX-NG schema.

    <grammar xmlns="http://relaxng.org/ns/structure/1.0"
                    xmlns:doc="http://www.example.com/annotation"
                    datatypeLibrary="http://xml.opendap.org/datatypes/dap4"
                    ns="http://xml.opendap.org/ns/DAP/4.0#"
                    >
    <start>
      <ref name="errorresponse"/>
    </start>
    <define name="errorresponse">
      <element name="Error">
        <optional>
          <attribute name="httpcode"><data type="dap4_integer"/></attribute>
        </optional>
        <optional>
          <interleave>
            <element name = "Message"><text/></Message>
            <element name = "Context"><text/></Message>
            <element name = "OtherInformation"><text/></Message>
          </interleave>
        </optional>
      </element>
    </define>

The Error element has one optional attribute: the *httpcode* which is a
standard HTTP protocol return code indicating the general class of
error. When possible, this code should match the return code in the HTTP
headers for the response.

The body of the &lt;Error&gt; element may contain any or all of the
following inner elements each containing arbitrary text.

1.  &lt;Message&gt; — A short informative message describing the error.
2.  &lt;Context&gt; — Information describing the context in which the
    error occurred: position of a parse error in a constraint
    expression, for example.
3.  &lt;OtherInformation&gt; — Arbitrary additional text information: a
    Java stack trace, for example.

#### <span id="Error_Response_Resource_Role" class="mw-headline"><span class="mw-headline-number">3.4.1</span> Error Response Resource Role</span>

DAP4 Error Responses are identified by the resource role:

**`http://services.opendap.org/dap4/error`**

#### <span id="Normative_Encoding_of_the_Error_Response" class="mw-headline"><span class="mw-headline-number">3.4.2</span> Normative Encoding of the Error Response</span>

The normative XML representation for the Error Response is defined in
Appendix x "Normative XML Encoding of the Error Response". The media
type for the normative XML representation is:

`application/vnd.opendap.dap4.error.xml`

## <span id="HTTP" class="mw-headline"><span class="mw-headline-number">4</span> HTTP</span>

The DAP4 Web Services specification describes the features of HTTP that
are required to be a compliant DAP4 client or server. It does not
attempt to describe all aspects of HTTP that DAP4 servers might
implement or that DAP4 clients may see in response to DAP4 requests.
Similarly, it does not cover all issues related to the performance and
scalability of HTTP.

However, the following sections include both DAP4 requirements as well
as some suggestions of HTTP features that servers and clients are
encouraged to use.

### <span id="Content_Negotiation_and_Media_Types" class="mw-headline"><span class="mw-headline-number">4.1</span> Content Negotiation and Media Types</span>

Though the DAP4 core specifications only describe one encoding for each
type of resource, DAP4 web servers MAY have the ability to provide a
given resource in a number of different media types. All media types
available for a resource MUST be listed in the DAP4 Dataset Services
response document.

DAP4 responses MUST use the "Content-Type" header field to identify the
media type of the DAP4 response body. For example, the normative value
for the XML encoded DMR response is
*application/vnd.opendap.dap4.dataset-metadata+xml*.

The DAP4 Dataset Services response describes the available services and
their media types, and through this description provides DAP4 software
(client and/or server) with two different mechanisms to negotiate for
different kinds of media representations. The first mechanism is
server-driven content negotiation as described in the HTTP 1.1
specification, section 12, "Content
Negotiation".<sup>\[[HTTP\ RFC2616\ -\ Section\ 12](https://docs.opendap.org/index.php?title=DAP4:_Specification_Volume_2#HTTP_RFC2616_Section_12)\]</sup>
The second mechanism is similar to the agent-driven negotiation also
described in section 12 of the HTTP 1.1 specification. The difference
being that the "list of available representations ... \[each with\] its
own URI" is provided by the DAP4 Dataset Services response rather than
in response to an initial request.

Clients need not retrieve the Dataset Services response in order to
access the normative representations of either the Dataset Metadata or
Data responses, as these responses are required for every DAP4 server
and are mapped to well known URL patterns. If clients attempt to access
other representations or other services using agent-driven negotiation
without first checking the Dataset Services response, they should be
prepared to receive a 404 Not Found response.

When using server-driven negotiation, DAP4 clients are encouraged to, at
a minimum, include
"Accept"<sup>\[[HTTP\ RFC2616\ -\ Section\ 14.1](https://docs.opendap.org/index.php?title=DAP4:_Specification_Volume_2#HTTP_RFC2616_Section_14.1)\]</sup>and
"User-Agent"<sup>\[[HTTP\ RFC2616\ -\ Section\ 14.43](https://docs.opendap.org/index.php?title=DAP4:_Specification_Volume_2#HTTP_RFC2616_Section_14.43)\]</sup>
headers in their requests and to provide accurate and detailed
information in the values of those headers. However, when server-driven
negotiation is used, DAP4 servers are not limited to those headers for
determining the media type that is returned. DAP4 clients should also be
prepared to handle 415 "Unsupported Media type" response codes.

  

### <span id="Redirects" class="mw-headline"><span class="mw-headline-number">4.2</span> Redirects</span>

While HTTP redirects are not directly part of the DAP4 web protocol it
is strongly suggested that DAP4 client implementations be capable of
processing HTTP redirects as nominally described in the HTTP-1.1
specification sections on redirection status codes and redirection
response
headers.<sup>\[[HTTP\ RFC2616](https://docs.opendap.org/index.php?title=DAP4:_Specification_Volume_2#HTTP_RFC2616)\]\[[HTTP\ RFC2616\ -\ Section\ 10.3](https://docs.opendap.org/index.php?title=DAP4:_Specification_Volume_2#HTTP_RFC2616_Section_10.3)\]\[[HTTP\ RFC2616\ -\ Section\ 14.30](https://docs.opendap.org/index.php?title=DAP4:_Specification_Volume_2#HTTP_RFC2616_-_Section_14.30)\]</sup>
(It is suggested that implementers of DAP4 clients utilize an existing
robust HTTP client library that will manage this for them.)

### <span id="Caching_of_Responses_and_Conditional_Requests" class="mw-headline"><span class="mw-headline-number">4.3</span> Caching of Responses and Conditional Requests</span>

While, HTTP caching and conditional requests are not explicitly part of
the DAP4 web protocol, they do provide important tools for improving the
performance of both sides client server interaction. Therefore, it is
strongly suggested that DAP4 servers and client implementers be aware of
how HTTP caching
<sup>\[[HTTP\ RFC2616\ -\ Section\ 13](https://docs.opendap.org/index.php?title=DAP4:_Specification_Volume_2#HTTP_RFC2616_-_Section_13)\]</sup>
works, and utilize it for working with DAP servers.

### <span id="Authentication/Authorization"></span><span id="Authentication.2FAuthorization" class="mw-headline"><span class="mw-headline-number">4.4</span> Authentication/Authorization</span>

Authentication is the process by which a user agent establishes the
identity of the user to a server, and the server establishes it's
identity with the user agent. While, HTTP authentication is not
explicitly part of the DAP4 web protocol, it does provide important
tools for securing the client server interaction. Therefore, it is
strongly suggested that DAP4 servers and client implementers be aware of
how HTTP authentication works, and utilize it for working with DAP
servers.<sup>\[[HTTP\ RFC2617](https://docs.opendap.org/index.php?title=DAP4:_Specification_Volume_2#HTTP_RFC2617)\]</sup>
Server implementers should pay particular attention to HTTP security
considerations.<sup>\[[HTTP\ RFC2616\ -\ Section\ 15](https://docs.opendap.org/index.php?title=DAP4:_Specification_Volume_2#HTTP_RFC2616_Section_15)\]</sup>

Authorization is the process through which a server determines who/what
has access to its various holdings and services. The HTTP protocol does
not directly address the issue of authorization (even though HTTP
defines the 401 response status using the word "authorization" it does
not provide separate semantics for authentication and authorization
which we see as an important distinction for data access), but any DAP4
server implementer should be aware that some kind of mechanism for
controlling access to holdings and services will likely be desired by
the people that install and operate their software.

### <span id="Headers" class="mw-headline"><span class="mw-headline-number">4.5</span> Headers</span>

#### <span id="Request_Headers" class="mw-headline"><span class="mw-headline-number">4.5.1</span> Request Headers</span>

These are the HTTP request headers that DAP clients using HTTP MAY
utilize. DAP4 servers MUST accept these headers and act on them in a
manner consistent with their descriptions below.

##### <span id="General" class="mw-headline"><span class="mw-headline-number">4.5.1.1</span> General</span>

Accept  
The HTTP Accept header MAY be used by clients that wish to engage in
server-dirven content negotiation by requesting a particular
representation of a resource in the initial request. The server MUST
utilize this header, if present, in a manner consistent with the HTTP
content negotiation\]\]
specification.<sup>\[[HTTP\ RFC2616\ -\ Section\ 12](https://docs.opendap.org/index.php?title=DAP4:_Specification_Volume_2#HTTP_RFC2616_Section_12)\]</sup>

<!-- -->

User-Agent  
The HTTP User-Agent header MAY be used by clients to indicate their
"software identity" to the
server.<sup>\[[HTTP\ RFC2616\ -\ Section\ 14.43](https://docs.opendap.org/index.php?title=DAP4:_Specification_Volume_2#HTTP_RFC2616_Section_14.43)\]</sup>
The server MAY utilize this header, if present, to alter the
Content-Type of the response to something that is more likely to be
digestible by the requesting client
software.<sup>\[[HTTP\ RFC2616\ -\ Section\ 14.17](https://docs.opendap.org/index.php?title=DAP4:_Specification_Volume_2#HTTP_RFC2616_Section_14.17)\]</sup>

##### <span id="DAP_Specific" class="mw-headline"><span class="mw-headline-number">4.5.1.2</span> DAP Specific</span>

There are no DAP specific headers required to make a general DAP
request.

  

#### <span id="Response_Headers" class="mw-headline"><span class="mw-headline-number">4.5.2</span> Response Headers</span>

These are the HTTP response headers that DAP servers using HTTP MUST and
SHOULD (as indicated) return.

##### <span id="General_2" class="mw-headline"><span class="mw-headline-number">4.5.2.1</span> General</span>

Date  
DAP4 servers MUST return an HTTP **Date** header whose value is the time
of the response and which MUST be in RFC 1123 date/time
format.<sup>\[[RFC1123](https://docs.opendap.org/index.php?title=DAP4:_Specification_Volume_2#RFC1123)\]</sup>

  

Last-Modified  
DAP4 servers SHOULD return an HTTP **Last-Modified** header whose value
is the last modified time of the request resource and which MUST be in
RFC 1123 date/time
format.<sup>\[[RFC1123](https://docs.opendap.org/index.php?title=DAP4:_Specification_Volume_2#RFC1123)\]</sup>

  

Content-Type  
DAP4 servers MUST return an HTTP **Content-Type** header, the value of
which SHOULD be set in accordance with the Dap4 Resource Roles and Media
Types discussion in section 1.1 of this document.

<!-- -->

Content-Description  
DAP4 servers SHOULD return an HTTP **Content-Description** header.

<!-- -->

Content-Disposition  
DAP4 servers SHOULD return an HTTP **Content-Disposition** header when
transmitting file typed responses.

<!-- -->

Content-Encoding  
DAP4 servers MUST return an HTTP **Content-Encoding** header when the
content-coding of an entity is not "identity".

  

##### <span id="DAP_Specific_2" class="mw-headline"><span class="mw-headline-number">4.5.2.2</span> DAP Specific</span>

X-DAP-Server  
DAP4 servers SHOULD return the **X-DAP-Server** HTTP header. This HTTP
header is used in a response to communicate the software version of the
server. This may be a simple string with the server name and version
number, or multiple software component versions may be represented. The
value of this header is a string determined by the implementations
author(s).

**Example**

X-DAP-Server: bes/3.10.0, libdap/3.11.2, dap-server/ascii/4.1.2,
csv\_handler/1.0.2, freeform\_handler/3.8.4, fits\_handler/1.0.7,
fileout\_netcdf/1.1.2, gateway\_module/1.1.0, hdf4\_handler/3.9.4,
hdf5\_handler/1.5.0, netcdf\_handler/3.10.0, ncml\_module/1.2.1,
dap-server/usage/4.1.2, dap-server/www/4.1.2, xml\_data\_handler/1.0.1

**Example**

X-DAP-Server: TDS-4.19.3

X-DAP  
DAP4 servers MUST return the **X-DAP** HTTP header. This HTTP header is
used in a response to indicate the DAP protocol version used to encode
the content of the response. This value is constrained to a format of
*"major\_version" dot "minor version"*, where both major\_version and
minor\_version are represented by an integer value.

**Example**

X-DAP: 4.0

**Example**

X-DAP: 2.17

  

### <span id="Status_Codes" class="mw-headline"><span class="mw-headline-number">4.6</span> Status Codes</span>

DAP servers that provide an HTTP interface are expected to utilize the
HTTP response codes in a manner consistent with the HTTP 1.1
specification.<sup>\[[HTTP\ RFC2616](https://docs.opendap.org/index.php?title=DAP4:_Specification_Volume_2#HTTP_RFC2616)\]</sup>

The ones that are detailed here are used by the DAP in a manner
consistent with the specifications definition, but in support of
specific DAP server behavior.

#### <span id="200_OK" class="mw-headline"><span class="mw-headline-number">4.6.1</span> 200 OK</span>

A server MUST return an HTTP status of 200 when the request has been
successful and that the returned document contains the requested
resource. However since DAP responses can be quite large and since it is
also possible for the server to encounter any number of problems during
the marshaling, serialization, and subsequent transmission of the
response it is possible that the server may have committed/transmitted
the HTTP headers (in which the status value is transmitted) before a
subsequent error is encountered. These types of errors are transmitted
in the DAP4 over-the-wire protocol and all DAP4 clients MUST be able to
read and process these errors.

#### <span id="400_Bad_Request" class="mw-headline"><span class="mw-headline-number">4.6.2</span> 400 Bad Request</span>

The HTTP specification defines this status code as:

*The request could not be understood by the server due to malformed
syntax. The client SHOULD NOT repeat the request without
modifications.*<sup>\[[HTTP\ RFC2616\ -\ Section\ 10.4.1](https://docs.opendap.org/index.php?title=DAP4:_Specification_Volume_2#HTTP_RFC2616_Section_10.4.1)\]</sup>

DAP4 servers utilizes this code to mean the following.

##### <span id="400_Bad_DAP4_Request_Syntax" class="mw-headline"><span class="mw-headline-number">4.6.2.1</span> 400 Bad DAP4 Request Syntax</span>

The **400 Bad DAP4 Request Syntax** HTTP response code MUST be returned
by the server when there is a problem with the syntax of the OPeNDAP
URL. The problem could be in the formulation of the constraint
expression, or it may be that the URL extension did not match any that
are recognized by this server.

#### <span id="401_Unauthorized" class="mw-headline"><span class="mw-headline-number">4.6.3</span> 401 Unauthorized</span>

The **401 Unauthorized** HTTP response code MUST be returned by the
server when access to the requested resource requires (not previously
acquired) user authentication. See the HTTP specification-1.1 for usage
and
behavior.<sup>\[[HTTP\ RFC2616\ -\ Section\ 10.4.2](https://docs.opendap.org/index.php?title=DAP4:_Specification_Volume_2#HTTP_RFC2616_Section_10.4.2)\]</sup>

#### <span id="403_Forbidden" class="mw-headline"><span class="mw-headline-number">4.6.4</span> 403 Forbidden</span>

The **403 Forbidden** HTTP response code MUST be returned when the
server has understood the request, but is refusing to fulfill it.
Authorization will not help and the request SHOULD NOT be repeated. This
is appropriate to return if, for example, the server software does not
have read permission for the requested
resource.<sup>\[[HTTP\ RFC2616\ -\ Section\ 10.4.4](https://docs.opendap.org/index.php?title=DAP4:_Specification_Volume_2#HTTP_RFC2616_Section_10.4.4)\]</sup>

#### <span id="404_Not_Found" class="mw-headline"><span class="mw-headline-number">4.6.5</span> 404 Not Found</span>

The **404 Not Found** HTTP response code MUST be returned when the
server has not found anything matching the
Request-URI.<sup>\[[HTTP\ RFC2616\ -\ Section\ 10.4.5](https://docs.opendap.org/index.php?title=DAP4:_Specification_Volume_2#HTTP_RFC2616_Section_10.4.5)\]</sup>

#### <span id="415_Unsupported_Media_Type" class="mw-headline"><span class="mw-headline-number">4.6.6</span> 415 Unsupported Media Type</span>

The **415 Unsupported Media Type** HTTP response code MUST be returned
when the client requests a representation of the requested resource that
the server cannot
provide.<sup>\[[HTTP\ RFC2616\ -\ Section\ 10.4.16](https://docs.opendap.org/index.php?title=DAP4:_Specification_Volume_2#HTTP_RFC2616_Section_10.4.16)\]</sup>

#### <span id="500_Internal_Server_Error" class="mw-headline"><span class="mw-headline-number">4.6.7</span> 500 Internal Server Error</span>

The **500 Internal Server Error** status code SHOULD be returned when
the DAP server encounters internal problems when attempting to fulfill a
request.<sup>\[[HTTP\ RFC2616\ -\ Section\ 10.5.1](https://docs.opendap.org/index.php?title=DAP4:_Specification_Volume_2#HTTP_RFC2616_Section_10.5.1)\]</sup>

### <span id="Verbs_(aka_Methods)"></span><span id="Verbs_.28aka_Methods.29" class="mw-headline"><span class="mw-headline-number">4.7</span> Verbs (aka Methods)</span>

#### <span id="GET" class="mw-headline"><span class="mw-headline-number">4.7.1</span> GET</span>

A DAP4 request may be made using the HTTP GET request method utilizing a
Uniform Resource Identifier (URI) that encodes information specific to
the DAP4.

Each GET request MUST conform to the HTTP specification (which basically
says that a GET request MUST contain an HTTP protocol version number
followed by a MIME-like message containing various headers that further
describe the request.). While there are some optional DAP4 HTTP request
headers that may be used, DAP4 requests do not require specific HTTP
headers beyond those necessary for HTTP (see section 4.5.1 Request
Headers of this document for more). DAP4 servers SHOULD support the use
of the HTTP Accept request header to allow clients to engage in HTTP
content negotiation for specific representations of a requested DAP4
response.<sup>\[[HTTP\ RFC2616\ -\ Section\ 12](https://docs.opendap.org/index.php?title=DAP4:_Specification_Volume_2#HTTP_RFC2616_Section_12)\]</sup>

The DAP server responds to the GET request with an HTTP compliant
response (one that includes a status line containing the HTTP protocol
version and an error or success code, followed by HTTP response headers
and then response itself). There are two DAP specific HTTP headers that
are always included in a DAP response over HTTP: X-DAP-Server and X-DAP,
as described in section 4.5.2 of this document. The DAP response is the
payload of the HTTP response. Unless otherwise negotiated, the data
response payload is encoded using the chunked format as described in
\[[DAP4
Vol.1](https://docs.opendap.org/index.php?title=DAP4:_Specification_Volume_2#DAP4_Vol1)\],
while the other responses are simple HTTP responses.

##### <span id="Examples" class="mw-headline"><span class="mw-headline-number">4.7.1.1</span> Examples</span>

HTTP GET request.

    GET /dap/path/data.nc.dap?/u,/v[0:8:1024] HTTP/1.1
    Host: server.org
    Accept: application/vnd.opendap.dap4.data

  

## <span id="DAP4_URLs" class="mw-headline"><span class="mw-headline-number">5</span> DAP4 URLs</span>

In DAP4 we divide a dataset URL into two sections, the *identifier* and
the *query string*. The *identifier* section is everything up to "*?*"
character. The *query string* is the "*?*" character and everything
after it.

For example in the URL:

**http://test.opendap.org:8080/opendap/data/nc/fnoc1.nc.dmr?dap4.ce=/u;/lat;/lon**

We have:

*identifier =*
**http://test.opendap.org:8080/opendap/data/nc/fnoc1.nc.dmr**

*query string =* **?dap4.ce=/u;/lat;/lon**

Additionally DAP4 URLs conform to the web convention in which the query
string is decomposed as a set of key-value pairs (KVP) separated from
each other by "**&**" characters:

`?key=value&key=value&key=value ... `

Many web services utilize this pattern, including OGC. The DAP2
constraint expression subsumed the entire query string, so it did not
fit into the standard KVP model. Tomcat (and other web server
frameworks) provide specific API methods for collecting the KVP from the
query string, but again DAP2 doesn't play well with this. The DAP4
constraint is designed to operate in a KVP environment.

### <span id="Query_String_Parameters" class="mw-headline"><span class="mw-headline-number">5.1</span> Query String Parameters</span>

-   DAP4 query string parameters will always begin with the 5 character
    string "**dap4.**" In this way query string parameters associated
    with the DAP4 protocol can be easily identified by both people and
    software.
-   DAP4 query string keys are case sensitive.
-   DAP4 servers MUST treat ALL values of query string KVPs as case
    sensitive.
-   Each DAP4 key may appear once in each query string (request URL).
-   The order of the keys does not matter, and unrecognized keys are
    ignored, along with their values.

The DAP4 protocol reserves the exclusive use of all future query string
keys that begin with the 4 character token "**dap4.**" This way future
DAP4 service features may be added and invoked through the query string
section of the request URL without interfering with other features and
behaviors added to service implementations outside of the DAP4
development process.

The following keys are reserved.

dap4.ce  
The DAP4 constraint expression is contained in a single query string
parameter named "**dap4.ce**" This constraint expression contains all of
the subsetting information for the dataset include the projection (which
variables are to be returned), slicing (how the various arrays are to be
decimated), and filtering (conditional retrieval of values). The fill
discussion of the syntax of the constraint expression can be found in
Section 8 of Volume 1 of the DAP4 specification.
<sup>\[[DAP4\ Vol.1](https://docs.opendap.org/index.php?title=DAP4:_Specification_Volume_2#DAP4_Vol1)\]</sup>

<!-- -->

dap4.async  
The asynchronous response behavior is described in detail in Section 10
of Volume 1 of the DAP4
Specification.<sup>\[[DAP4\ Vol.1](https://docs.opendap.org/index.php?title=DAP4:_Specification_Volume_2#DAP4_Vol1)\]</sup>
While the a DAP4 server's asynchronous response behavior can be
controlled by a savvy client using HTTP headers it can also be managed
using the DAP4 query string parameter "**dap4.async**"

<!-- -->

dap4.func  
While server-side functions are not addressed in the initial DAP4
specification or constraint expression syntax we do anticipate them
being defined (in short order) in an extension to the DAP4
specification. For now we are working with a proposed server side
function syntax in which a server side function is invoked as a key
value pair, something like: **dap4.func=ugr5(0,v,z,”10&lt;lat&lt;30”)**

## <span id="Normative_References" class="mw-headline"><span class="mw-headline-number">6</span> Normative References</span>

\[DAP4 Vol1\] [DAP4 Volume 1: Data Model, Persistent Representations,
and
Constraints](https://docs.opendap.org/index.php?title=DAP4:_Specification_Volume_1 "DAP4: Specification Volume 1").

\[HTTP RFC2616\]
<a href="http://www.w3.org/Protocols/rfc2616/rfc2616.html"
class="external text" rel="nofollow">Hypertext Transfer Protocol --
HTTP/1.1</a> (as
<a href="http://www.ietf.org/rfc/rfc2616.txt" class="external text"
rel="nofollow">text</a>).

\[HTTP RFC2616 - Section 10.2.3\] <a
href="http://www.w3.org/Protocols/rfc2616/rfc2616-sec10.html#sec10.2.3"
class="external text" rel="nofollow">HTTP/1.1 Section 10.2.3 -
Accepted</a>

\[HTTP RFC2616 - Section 10.3\]
<a href="http://www.w3.org/Protocols/rfc2616/rfc2616-sec10.html#sec10.3"
class="external text" rel="nofollow">HTTP/1.1 Section 10.3 - Redirection
Status Codes</a>

\[HTTP RFC2616 - Section 10.4.1\] <a
href="http://www.w3.org/Protocols/rfc2616/rfc2616-sec10.html#sec10.4.1"
class="external text" rel="nofollow">HTTP/1.1 Section 10.4.1 - Bad
Request</a>

\[HTTP RFC2616 - Section 10.4.2\] <a
href="http://www.w3.org/Protocols/rfc2616/rfc2616-sec10.html#sec10.4.2"
class="external text" rel="nofollow">HTTP/1.1 Section 10.4.2 -
Unauthorized</a>

\[HTTP RFC2616 - Section 10.4.4\] <a
href="http://www.w3.org/Protocols/rfc2616/rfc2616-sec10.html#sec10.4.4"
class="external text" rel="nofollow">HTTP/1.1 Section 10.4.4 -
Forbidden</a>

\[HTTP RFC2616 - Section 10.4.5\] <a
href="http://www.w3.org/Protocols/rfc2616/rfc2616-sec10.html#sec10.4.5"
class="external text" rel="nofollow">HTTP/1.1 Section 10.4.5 - Not
Found</a>

\[HTTP RFC2616 - Section 10.4.10\] <a
href="http://www.w3.org/Protocols/rfc2616/rfc2616-sec10.html#sec10.4.10"
class="external text" rel="nofollow">HTTP/1.1 Section 10.4.10 -
Conflict</a>

\[HTTP RFC2616 - Section 10.4.13\] <a
href="http://www.w3.org/Protocols/rfc2616/rfc2616-sec10.html#sec10.4.13"
class="external text" rel="nofollow">HTTP/1.1 Section 10.4.13 -
Precondition Failed</a>

\[HTTP RFC2616 - Section 10.4.16\] <a
href="http://www.w3.org/Protocols/rfc2616/rfc2616-sec10.html#sec10.4.16"
class="external text" rel="nofollow">HTTP/1.1 Section 10.4.16 -
Unsupported Media Type</a>

\[HTTP RFC2616 - Section 10.5.1\] <a
href="http://www.w3.org/Protocols/rfc2616/rfc2616-sec10.html#sec10.5.1"
class="external text" rel="nofollow">HTTP/1.1 Section 10.5.1 - Internal
Server Error</a>

\[HTTP RFC2616 - Section 12\]
<a href="http://www.w3.org/Protocols/rfc2616/rfc2616-sec12.html"
class="external text" rel="nofollow">HTTP/1.1 Section 12 - Content
Negotiation</a>

\[HTTP RFC2616 - Section 13\]
<a href="http://www.w3.org/Protocols/rfc2616/rfc2616-sec13.html"
class="external text" rel="nofollow">HTTP/1.1 Section 13 - Caching</a>

\[HTTP RFC2616 - Section 14.1\]
<a href="http://www.w3.org/Protocols/rfc2616/rfc2616-sec14.html#sec14.1"
class="external text" rel="nofollow">HTTP/1.1 Section 14.1 - Accept
Header</a>

\[HTTP RFC2616 - Section 14.17\] <a
href="http://www.w3.org/Protocols/rfc2616/rfc2616-sec14.html#sec14.17"
class="external text" rel="nofollow">HTTP/1.1 Section 14.17 -
Content-Type Header</a>

\[HTTP RFC2616 - Section 14.30\] <a
href="http://www.w3.org/Protocols/rfc2616/rfc2616-sec14.html#sec14.30"
class="external text" rel="nofollow">HTTP/1.1 Section 14.30 -
Redirection Response Headers</a>

\[HTTP RFC2616 - Section 14.43\] <a
href="http://www.w3.org/Protocols/rfc2616/rfc2616-sec14.html#sec14.43"
class="external text" rel="nofollow">HTTP/1.1 Section 14.43 - User-Agent
Header</a>

\[HTTP RFC2616 - Section 15\]
<a href="http://www.w3.org/Protocols/rfc2616/rfc2616-sec15.html"
class="external text" rel="nofollow">HTTP/1.1 Section 15 - Security
Considerations</a>

\[HTTP RFC2617\]
<a href="http://www.ietf.org/rfc/rfc2617.txt" class="external text"
rel="nofollow">- HTTP Authentication</a>

\[RFC1123\]
<a href="http://www.ietf.org/rfc/rfc1123.txt" class="external text"
rel="nofollow">- Requirements for Internet Hosts</a>

## <span id="Non-Normative_References" class="mw-headline"><span class="mw-headline-number">7</span> Non-Normative References</span>

\[REST\] R. Fielding, UC Irvine Doctoral Thesis:
<a href="http://www.ics.uci.edu/~fielding/pubs/dissertation/top.htm%7C"
class="external text" rel="nofollow">"Architectural Styles and the
Design of Network-based Software Architectures"</a>

\[MediaType\] Wikipedia:
<a href="http://en.wikipedia.org/wiki/Internet_media_type"
class="external text" rel="nofollow">Internet Media Type</a>

------------------------------------------------------------------------

------------------------------------------------------------------------

## <span id="Appendix_-_Ancillary_Web_Services_(Beyond_DAP4)"></span><span id="Appendix_-_Ancillary_Web_Services_.28Beyond_DAP4.29" class="mw-headline"><span class="mw-headline-number">8</span> Appendix - Ancillary Web Services (Beyond DAP4)</span>

DAP4 servers MAY offer a number of other services that, while not
exactly DAP4 services per say, are commonly available. This section
lists some of the alternate services a DAP4 server might provide. By
enumerating the available services in the Dataset Services Response
servers can easily make software clients and the people that use them
aware of the server's ancillary capabilities.

#### <span id="DAP4:_HTML_DATA_Request_Form_Service" class="mw-headline"><span class="mw-headline-number">8.1</span> [DAP4: HTML DATA Request Form Service](https://docs.opendap.org/index.php?title=DAP4:_HTML_DATA_Request_Form_Service "DAP4: HTML DATA Request Form Service")</span>

The HTML DATA Request Form Service provides browser based access to the
Dataset. When invoked it returns a web-browser renderable document (in
html) that provides a form (or other UI) that can be used to constrain
and request data in accordance with the DAP4 specification as applied to
the dataset .

  
suffix = `.html`  
service url = `dataset_url + .html`  
role id = `http://services.opendap.org/dap4/data-request-form#`  

Default/primary media type: `text/html` | `text/xhtml`  

#### <span id="DAP4:_RDF_Service" class="mw-headline"><span class="mw-headline-number">8.2</span> [DAP4: RDF Service](https://docs.opendap.org/index.php?title=DAP4:_RDF_Service "DAP4: RDF Service")</span>

The RDF service provides an RDF representation of the Dataset document
(DDX). The RDF response is an XML document containing an RDF version of
the [DAP4: Dataset
Response.](https://docs.opendap.org/index.php?title=DAP4:_Responses#Dataset_Response "DAP4: Responses")

  
suffix = `.rdf`  
service url = `dataset_url + .rdf`  
role id = `http://services.opendap.org/dap4/rdf#`  

Default/primary media type: `application/rdf+xml`  
  

#### <span id="DAP4:_ISO_19115_Service" class="mw-headline"><span class="mw-headline-number">8.3</span> [DAP4: ISO 19115 Service](https://docs.opendap.org/index.php?title=DAP4:_ISO_19115_Service "DAP4: ISO 19115 Service") </span>

This service provides ISO 19115 metadata for the Dataset, if any can be
found. When invoked it returns an XML document containing ISO 19115
metadata located in the [DAP4: Dataset
Response.](https://docs.opendap.org/index.php?title=DAP4:_Responses#Dataset_Response "DAP4: Responses")

  
suffix = `.iso`  
service url = `dataset_url + .iso`  
role id = `http://services.opendap.org/dap4/iso-19115-metadata#`  

Default/primary media type: `text/xml`  
  

#### <span id="DAP4:_ISO_Conformance_Score_Service" class="mw-headline"><span class="mw-headline-number">8.4</span> [DAP4: ISO Conformance Score Service](https://docs.opendap.org/index.php?title=DAP4:_ISO_Conformance_Score_Service "DAP4: ISO Conformance Score Service") </span>

This service provides a browser renderable document that describes how
well the metadata held in the Dataset conforms to ISO 19115. When
invoked this service returns a browser renderable document that scores
how well the metadata held in the [Dataset
Response](https://docs.opendap.org/index.php?title=DAP4:_Responses#Dataset_Response "DAP4: Responses")
conforms to ISO 19115.

  
suffix = `.rubric`  
service url = `dataset_url + .rubric`  
role id = `http://services.opendap.org/dap4/iso-19115-score#`  

Default/primary media type: `text/html`  
  

#### <span id="DAP4:_NetCDF_File-out_Service" class="mw-headline"><span class="mw-headline-number">8.5</span> [DAP4: NetCDF File-out Service](https://docs.opendap.org/index.php?title=DAP4:_NetCDF_File-out_Service "DAP4: NetCDF File-out Service") </span>

This service provides data responses in NetCDF-4 file format. When
invoked the regular DAP data response will be repackaged as a NetCDF 4
file.

suffix = `.nc4`  
service url = `dataset_url + '.nc4' + [?dap_constraint]`  
role id = `http://services.opendap.org/dap4/netcdf-3#`  

Default/primary media type: `application/x-netcdf-4`  
  

#### <span id="DAP4:_ASCII_Data_Service" class="mw-headline"><span class="mw-headline-number">8.6</span> [DAP4: ASCII Data Service](https://docs.opendap.org/index.php?title=DAP4:_ASCII_Data_Service "DAP4: ASCII Data Service")</span>

This service provides data responses in ASCII format. When invoked the
regular DAP data response will be repackaged as an ASCII representation
of the data values.

  
suffix = `.ascii`  
service url = `dataset_url + '.ascii' + [?dap_constraint]`  
role id = `http://services.opendap.org/dap4/ascii#`  
  

Default/primary media type: `text/plain`  
  

#### <span id="DAP4:_XML_Data_Service" class="mw-headline"><span class="mw-headline-number">8.7</span> [DAP4: XML Data Service](https://docs.opendap.org/index.php?title=DAP4:_XML_Data_Service "DAP4: XML Data Service")</span>

This service provides data responses in XML format. When invoked the
constrained Dataset response document (DDX) will be marked up with the
data values of the request and returned. Large requests may be denied.

  
suffix = `.xdap`  
service url = `dataset_url + '.xdap' + [?dap_constraint]`  
role id = `http://services.opendap.org/dap4/xml-data#`  
  

Default/primary media type: `text/xml`  
  

#### <span id="DAP4:_Native_File_Access_Service" class="mw-headline"><span class="mw-headline-number">8.8</span> [DAP4: Native File Access Service](https://docs.opendap.org/index.php?title=DAP4:_Native_File_Access_Service "DAP4: Native File Access Service") </span>

This service provides direct access to the data source file (or whatever
else) that is creating the DAP dataset resource. When invoked it returns
the "native" data from whatever store (filesystem, etc.) it may be in.
Servers MAY elect to not support this response, for example, for
generated data, very large data, et cetera.

  
suffix = `.file`  
service url = `dataset_url + .file`  
role id = `http://services.opendap.org/dap4/file#`  
  

Default/primary media type: Type varies with file type.  

#### <span id="DAP4:_Server_Version_Service" class="mw-headline"><span class="mw-headline-number">8.9</span> [DAP4: Server Version Service](https://docs.opendap.org/index.php?title=DAP4:_Server_Version_Service "DAP4: Server Version Service") </span>

This service provides software versioning information. When invoked the
service returns an XML file containing a description of the version of
the server and it's components.

  
suffix = `.ver`  
service url = `dataset_url + .ver`  
role id = `http://services.opendap.org/dap4/version#`  
  

Default/primary media type: `text/xml`  
  

### <span id="DAP2_Services" class="mw-headline"><span class="mw-headline-number">8.10</span> DAP2 Services</span>

In order to support legacy client applications DAP4 server
implementations MAY support the DAP2 services stack. If they do so the
DAP2 services MUST be organized as described in this section.

  

#### <span id="DAP2:_Data_Service" class="mw-headline"><span class="mw-headline-number">8.10.1</span> [DAP2: Data Service](https://docs.opendap.org/index.php?title=DAP2:_Data_Service "DAP2: Data Service")</span>

The DAP2 data service provides DAP2 data access to the data resource.

  
suffix = `.dods`  
service url = `dataset_url + '.dods' + [?dap_constraint]`  
role id = `http://services.opendap.org/dap2/dods#`  
  

Default/primary media type: `application/octet-stream`  
  

#### <span id="DAP2:_DDX_Service" class="mw-headline"><span class="mw-headline-number">8.10.2</span> [DAP2: DDX Service](https://docs.opendap.org/index.php?title=DAP2:_DDX_Service "DAP2: DDX Service") </span>

The DAP2 DDX service provides DAP2 access to the data resource metadata.
When invoked the service returns an XML document containing both
syntactic and semantic dataset metadata in DAP2 XML format.

suffix = `.ddx`  
service url = `dataset_url + .ddx`  
role id = `http://services.opendap.org/dap2/ddx#`  

Default/primary media type: `text/xml`  
  

#### <span id="DAP2:_DDS_Service" class="mw-headline"><span class="mw-headline-number">8.10.3</span> [DAP2: DDS Service](https://docs.opendap.org/index.php?title=DAP2:_DDS_Service "DAP2: DDS Service") </span>

The DAP2 DDS service provides access to the 'syntactic' metadata (aka
use or structural metadata) for the data resource. When invoked returns
a DAP2 DDS response document conforming to the DDS part of the DAP2
specification.

  
suffix = `.dds`  
service url = `dataset_url + '.dds' + [?dap_constraint]`  
role id = `http://services.opendap.org/dap2/dds#`  

Default/primary media type: `text/plain`  
  

#### <span id="DAP2:_DAS_Service" class="mw-headline"><span class="mw-headline-number">8.10.4</span> [DAP2: DAS Service](https://docs.opendap.org/index.php?title=DAP2:_DAS_Service "DAP2: DAS Service") </span>

The DAP2 DAS service provides access to the 'semantic' metadata (aka
domain metadata) for the data resource. When invoked returns a DAP2 DAS
response document conforming to the DAS part of the DAP2 specification.

  
suffix = `.das`  
service url = `dataset_url + .das`  
role id = `http://services.opendap.org/dap2/das#`  

Default/primary media type: `text/plain`  
  

  

#### <span id="DAP2:_ASCII_Data_Service" class="mw-headline"><span class="mw-headline-number">8.10.5</span> <a
href="https://docs.opendap.org/index.php?title=DAP2:_ASCII_Data_Service&amp;action=edit&amp;redlink=1"
class="new" title="DAP2: ASCII Data Service (page does not exist)">DAP2:
ASCII Data Service</a></span>

This service provides DAP2 data responses in ASCII format. When invoked
the regular DAP2 data response will be repackaged as an ASCII
representation of the data values.

  
suffix = `.ascii`  
service url = `dataset_url + '.ascii' + [?dap_constraint]`  
role id = `http://services.opendap.org/dap2/ascii#`  
  

Default/primary media type: `text/plain`  
  

#### <span id="DAP2:_JSON_Data_Service" class="mw-headline"><span class="mw-headline-number">8.10.6</span> <a
href="https://docs.opendap.org/index.php?title=DAP2:_JSON_Data_Service&amp;action=edit&amp;redlink=1"
class="new" title="DAP2: JSON Data Service (page does not exist)">DAP2:
JSON Data Service</a></span>

This service provides DAP2 data responses in w10n JSON format. When
invoked the regular DAP2 data response will be repackaged as an w10n
JSON representation of the data values.

  
suffix = `.json`  
service url = `dataset_url + '.json' + [?dap_constraint]`  
role id = `http://services.opendap.org/dap2/json#`  
  

Default/primary media type: `text/plain`  
  

#### <span id="DAP2:_Info_Service" class="mw-headline"><span class="mw-headline-number">8.10.7</span> [DAP2: Info Service](https://docs.opendap.org/index.php?title=DAP2:_Info_Service "DAP2: Info Service") </span>

The DAP2 INFO service provides a browser renderable page that combines
both the DAP2 'syntactic' and 'semantic' metadata for the data resource
in a human readable way. When invoked this service returns a web browser
renderable document that combines both the DAP2 'syntactic' and
'semantic' metadata for the data resource in a human readable way.

  
suffix = `.info`  
service url = `dataset_url + .info`  
role id = `http://services.opendap.org/dap2/Info#`  

Default/primary media type: `text/html`  
  

#### <span id="DAP2:_NetCDF_Service" class="mw-headline"><span class="mw-headline-number">8.10.8</span> <a
href="https://docs.opendap.org/index.php?title=DAP2:_NetCDF_Service&amp;action=edit&amp;redlink=1"
class="new" title="DAP2: NetCDF Service (page does not exist)">DAP2:
NetCDF Service</a> </span>

This service provides data responses in NetCDF-3 file format. When
invoked the regular DAP data response will be repackaged as a NetCDF 3
file.

suffix = `.nc`  
service url = `dataset_url + '.nc' + [?dap_constraint]`  
role id = `http://services.opendap.org/dap4/netcdf-3#`  

Default/primary media type: `application/x-netcdf`  
  

  
[Template:
ServiceTemplate](https://docs.opendap.org/index.php?title=Template:ServiceTemplate "Template:ServiceTemplate")
