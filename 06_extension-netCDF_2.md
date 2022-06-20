# DAP4 Extension: Asynchronous Response

This document specifies the DAP4 Asynchronous HTTP Response extension.
It defines the set of HTTP mechanisms used by DAP4 clients and servers
when requesting or delivering asynchronous responses.

This extension provides DAP4 with a mechanism that allows servers to
handle requests where the construction or computation of the response
takes more time than a client may wish to wait.

## Contents

<span class="toctoggle"> \[<span class="togglelink" role="button"
tabindex="0">hide</span>\] </span>

-   [<span class="tocnumber">1</span> <span class="toctext">DAP4
    Extension
    Details</span>](https://docs.opendap.org/index.php?title=DAP4_Extension:_Asynchronous_Response#DAP4_Extension_Details)
-   [<span class="tocnumber">2</span> <span class="toctext">Summary of
    HTTP Mechanisms Used to Support Asynchronous HTTP
    Response</span>](https://docs.opendap.org/index.php?title=DAP4_Extension:_Asynchronous_Response#Summary_of_HTTP_Mechanisms_Used_to_Support_Asynchronous_HTTP_Response)
-   [<span class="tocnumber">3</span> <span class="toctext">Overview:
    Asynchronous Service Behavior and
    Responses</span>](https://docs.opendap.org/index.php?title=DAP4_Extension:_Asynchronous_Response#Overview:_Asynchronous_Service_Behavior_and_Responses)
-   [<span class="tocnumber">4</span> <span class="toctext">Client
    willingness to accept asynchronous
    responses</span>](https://docs.opendap.org/index.php?title=DAP4_Extension:_Asynchronous_Response#Client_willingness_to_accept_asynchronous_responses)
-   [<span class="tocnumber">5</span> <span class="toctext">Initial
    processing by the
    server</span>](https://docs.opendap.org/index.php?title=DAP4_Extension:_Asynchronous_Response#Initial_processing_by_the_server)
-   [<span class="tocnumber">6</span> <span class="toctext">Response
    retrieval by the
    client</span>](https://docs.opendap.org/index.php?title=DAP4_Extension:_Asynchronous_Response#Response_retrieval_by_the_client)
-   [<span class="tocnumber">7</span> <span class="toctext">Detail:
    Client
    requests</span>](https://docs.opendap.org/index.php?title=DAP4_Extension:_Asynchronous_Response#Detail:_Client_requests)
    -   [<span class="tocnumber">7.1</span> <span class="toctext">DAP4
        Constraint Expression extension for
        Async</span>](https://docs.opendap.org/index.php?title=DAP4_Extension:_Asynchronous_Response#DAP4_Constraint_Expression_extension_for_Async)
    -   [<span class="tocnumber">7.2</span> <span
        class="toctext">X-DAP-Async-Accept</span>](https://docs.opendap.org/index.php?title=DAP4_Extension:_Asynchronous_Response#X-DAP-Async-Accept)
-   [<span class="tocnumber">8</span> <span class="toctext">Detail:
    Server
    responses</span>](https://docs.opendap.org/index.php?title=DAP4_Extension:_Asynchronous_Response#Detail:_Server_responses)
    -   [<span class="tocnumber">8.1</span> <span class="toctext">HTTP
        Response
        Headers</span>](https://docs.opendap.org/index.php?title=DAP4_Extension:_Asynchronous_Response#HTTP_Response_Headers)
        -   [<span class="tocnumber">8.1.1</span> <span
            class="toctext">X-DAP-Async-Required</span>](https://docs.opendap.org/index.php?title=DAP4_Extension:_Asynchronous_Response#X-DAP-Async-Required)
        -   [<span class="tocnumber">8.1.2</span> <span
            class="toctext">X-DAP-Async-Accepted</span>](https://docs.opendap.org/index.php?title=DAP4_Extension:_Asynchronous_Response#X-DAP-Async-Accepted)
    -   [<span class="tocnumber">8.2</span> <span class="toctext">HTTP
        Response
        Codes</span>](https://docs.opendap.org/index.php?title=DAP4_Extension:_Asynchronous_Response#HTTP_Response_Codes)
        -   [<span class="tocnumber">8.2.1</span> <span
            class="toctext">202
            Accepted</span>](https://docs.opendap.org/index.php?title=DAP4_Extension:_Asynchronous_Response#202_Accepted)
        -   [<span class="tocnumber">8.2.2</span> <span
            class="toctext">400 DAP4 Asynchronous Response
            Required</span>](https://docs.opendap.org/index.php?title=DAP4_Extension:_Asynchronous_Response#400_DAP4_Asynchronous_Response_Required)
        -   [<span class="tocnumber">8.2.3</span> <span
            class="toctext">409 Conflict - DAP4 Response Not
            Ready</span>](https://docs.opendap.org/index.php?title=DAP4_Extension:_Asynchronous_Response#409_Conflict_-_DAP4_Response_Not_Ready)
        -   [<span class="tocnumber">8.2.4</span> <span
            class="toctext">410 Gone - DAP4 Response No Longer
            Available</span>](https://docs.opendap.org/index.php?title=DAP4_Extension:_Asynchronous_Response#410_Gone_-_DAP4_Response_No_Longer_Available)
        -   [<span class="tocnumber">8.2.5</span> <span
            class="toctext">412 Precondition
            Failed</span>](https://docs.opendap.org/index.php?title=DAP4_Extension:_Asynchronous_Response#412_Precondition_Failed)
        -   [<span class="tocnumber">8.2.6</span> <span
            class="toctext">500 Internal
            Error</span>](https://docs.opendap.org/index.php?title=DAP4_Extension:_Asynchronous_Response#500_Internal_Error)
    -   [<span class="tocnumber">8.3</span> <span
        class="toctext">Asynchronous Response
        Documents</span>](https://docs.opendap.org/index.php?title=DAP4_Extension:_Asynchronous_Response#Asynchronous_Response_Documents)
        -   [<span class="tocnumber">8.3.1</span> <span
            class="toctext">DAP4 Asynchronous Response
            Required</span>](https://docs.opendap.org/index.php?title=DAP4_Extension:_Asynchronous_Response#DAP4_Asynchronous_Response_Required)
        -   [<span class="tocnumber">8.3.2</span> <span
            class="toctext">DAP4 Asynchronous Request
            Accepted</span>](https://docs.opendap.org/index.php?title=DAP4_Extension:_Asynchronous_Response#DAP4_Asynchronous_Request_Accepted)
        -   [<span class="tocnumber">8.3.3</span> <span
            class="toctext">DAP4 Asynchronous Response Not (Yet)
            Available</span>](https://docs.opendap.org/index.php?title=DAP4_Extension:_Asynchronous_Response#DAP4_Asynchronous_Response_Not_.28Yet.29_Available)
        -   [<span class="tocnumber">8.3.4</span> <span
            class="toctext">DAP4 Asynchronous Response
            Gone</span>](https://docs.opendap.org/index.php?title=DAP4_Extension:_Asynchronous_Response#DAP4_Asynchronous_Response_Gone)
        -   [<span class="tocnumber">8.3.5</span> <span
            class="toctext">DAP4 Asynchronous Request
            Rejected</span>](https://docs.opendap.org/index.php?title=DAP4_Extension:_Asynchronous_Response#DAP4_Asynchronous_Request_Rejected)
        -   [<span class="tocnumber">8.3.6</span> <span
            class="toctext">DAP4
            Error</span>](https://docs.opendap.org/index.php?title=DAP4_Extension:_Asynchronous_Response#DAP4_Error)
-   [<span class="tocnumber">9</span> <span
    class="toctext">Examples</span>](https://docs.opendap.org/index.php?title=DAP4_Extension:_Asynchronous_Response#Examples)
    -   [<span class="tocnumber">9.1</span> <span
        class="toctext">Constrained Data Request-Response using
        GET</span>](https://docs.opendap.org/index.php?title=DAP4_Extension:_Asynchronous_Response#Constrained_Data_Request-Response_using_GET)
    -   [<span class="tocnumber">9.2</span> <span
        class="toctext">Constrained Data Request-Response with
        DAP-Async-Accept Request
        Header</span>](https://docs.opendap.org/index.php?title=DAP4_Extension:_Asynchronous_Response#Constrained_Data_Request-Response_with_DAP-Async-Accept_Request_Header)
    -   [<span class="tocnumber">9.3</span> <span
        class="toctext">Constrained Data Request-Response with
        conditional DAP-Async-Accept Request
        Headers</span>](https://docs.opendap.org/index.php?title=DAP4_Extension:_Asynchronous_Response#Constrained_Data_Request-Response_with_conditional_DAP-Async-Accept_Request_Headers)
    -   [<span class="tocnumber">9.4</span> <span
        class="toctext">Premature Request For Asynchronous
        Result</span>](https://docs.opendap.org/index.php?title=DAP4_Extension:_Asynchronous_Response#Premature_Request_For_Asynchronous_Result)
-   [<span class="tocnumber">10</span> <span class="toctext">Resource
    Role</span>](https://docs.opendap.org/index.php?title=DAP4_Extension:_Asynchronous_Response#Resource_Role)
-   [<span class="tocnumber">11</span> <span class="toctext">Normative
    Encoding of the Asynchronous
    Response</span>](https://docs.opendap.org/index.php?title=DAP4_Extension:_Asynchronous_Response#Normative_Encoding_of_the_Asynchronous_Response)

## <span id="DAP4_Extension_Details" class="mw-headline"><span class="mw-headline-number">1</span> DAP4 Extension Details</span>

The Role URI for the DAP4 Asynchronous HTTP Response extension is

    http://services.opendap.org/dap4/extension/asynchronous-http-response

DAP4 servers MUST include this role URI in a Dataset Service Response
\[DSR\] *extension* element to indicate that the DAP4 Asynchronous HTTP
Response extension is supported for the dataset (?represented by that
DSR?). DAP4 clients MAY check for DSR **extension** elements with this
role URI to determine if the DAP4 Asynchronous HTTP Response extension
is supported.

Dataset Service Response \[DSR\] *extension* elements must also contain
a name and a description. The following are recommended text for the
name and description:

Name  
DAP4 Asynchronous HTTP Response

<!-- -->

Description  
This extension provides DAP4 with a mechanism to support asynchronous
HTTP responses, e.g., when a request will take the server time to
fulfill.

## <span id="Summary_of_HTTP_Mechanisms_Used_to_Support_Asynchronous_HTTP_Response" class="mw-headline"><span class="mw-headline-number">2</span> Summary of HTTP Mechanisms Used to Support Asynchronous HTTP Response</span>

Role:
<a href="http://services.opendap.org/dap4/async" class="external free"
rel="nofollow">http://services.opendap.org/dap4/async</a>

Response:

-   DAP4 Asynch Response document:
    -   Media Type: application/vnd.opendap.dap4.async+xml
    -   XML Namespace:
        <a href="http://opendap.org/ns/dap/asynchronous" class="external free"
        rel="nofollow">http://opendap.org/ns/dap/asynchronous</a>
    -   Types of documents
        -   Required
        -   Accepted
        -   Not Yet Available
        -   Gone

HTTP Request Headers

HTTP Response Headers

URL Query String: dap4.async

## <span id="Overview:_Asynchronous_Service_Behavior_and_Responses" class="mw-headline"><span class="mw-headline-number">3</span> Overview: Asynchronous Service Behavior and Responses</span>

Asynchronous responses are responses that will take the server some time
to build. When a client is told that a response 'is asynchronous,' it
must know to come back at a later time to retrieve the response. The
concept is a very simple one, and the existing network infrastructure is
very good at supporting these kinds of interactions. A major factor in
the success of the proposed solution will be the level of uniform
support for the design. Secondly, as is often the case, the details will
be more complex than the underlying concept. In particular, the request
mechanism must be extended so that synchronous (regular) requests are
not affected by the addition of asynchronous requests and, at the same
time, clients do not inadvertently make asynchronous requests. another
detail is that the (asynchronous) responses are *ephemeral* because they
typically only persist for a period of time and then be purged.

A typical 'workflow' for an asynchronous request is:

1.  A client makes a data request that indicates that it will accept
    either an asynchronous or synchronous response. Optionally, the
    client can place a time constraint on the response, indicating that
    if the response will not be ready in a given period of time, it does
    not want the response.
2.  The server returns an initial response (without delay) that
    indicates the request has indeed resulted in an asynchronous
    response and provides the client with a URL and time estimate.
3.  The client reads the time estimate and waits...
4.  The client dereferences the URL and gets the response.

Examples  
A DAP4 server that is retrieving data content from a near-line tape
storage subsystem might take several minutes to access a particular data
holding.

A DAP4 server that is providing access to data held in an Amazon Web
Services Glacier Vault will have to wait ~4 hours before it can retrieve
a particular holding.

In these circumstances the server may return the DAP4 Asynchronous
Response.

The remainder of this section will expand on this basic workflow using
examples that focus on the HTTP protocol but that also allow for the use
of other transport protocols.

## <span id="Client_willingness_to_accept_asynchronous_responses" class="mw-headline"><span class="mw-headline-number">4</span> Client willingness to accept asynchronous responses</span>

A client can indicate willingness to accept asynchronous responses in
one of two ways:

-   By including the
    [X-DAP-Async-Accept](https://docs.opendap.org/index.php?title=DAP4_Extension:_Asynchronous_Response#Accept_DAP_Asynchronous_Response)
    HTTP header.
-   By adding the
    [async](https://docs.opendap.org/index.php?title=DAP4_Extension:_Asynchronous_Response#DAP4_Constraint_Expression_extension_for_Async)
    keyword to the DAP constraint expression.

If the client indicates that it must have access to the asynchronous
response content within a certain time (utilizing either the
[X-DAP-Async-Accept](https://docs.opendap.org/index.php?title=DAP4_Extension:_Asynchronous_Response#Accept_DAP_Asynchronous_Response)
HTTP header and/or the
[async](https://docs.opendap.org/index.php?title=DAP4_Extension:_Asynchronous_Response#DAP4_Constraint_Expression_extension_for_Async)
keyword in the constraint expression) and the response will not be
available in that time frame, the server MUST reject the request and
return an HTTP status of
[412](https://docs.opendap.org/index.php?title=DAP4_Extension:_Asynchronous_Response#412_Precondition_Failed)
and the [DAP Asynchronous Request
Rejected](https://docs.opendap.org/index.php?title=DAP4_Extension:_Asynchronous_Response#DAP_Asynchronous_Request_Rejected)
XML document.

If both the *X-DAP-Async-Accept* HTTP header and the *async* keyword are
used, the keyword takes precedence.

Servers must reject requests that require an asynchronous response if
the client has not indicated willingness to accept such a response.
Rejection of such requests is indicated by all three of the following:

1.  [HTTP status of
    400](https://docs.opendap.org/index.php?title=DAP4_Extension:_Asynchronous_Response#400_DAP_Asynchronous_Response_Required)
2.  Inclusion of the
    [X-DAP-Async-Required](https://docs.opendap.org/index.php?title=DAP4_Extension:_Asynchronous_Response#DAP_Asynchronous_Response_Required)
    HTTP response header
3.  The response body must contain the [DAP Asynchronous Response
    Required](https://docs.opendap.org/index.php?title=DAP4_Extension:_Asynchronous_Response#DAP_Asynchronous_Response_Required)
    XML document.

This safety check (requiring clients to explicitly indicate their
willingness to accept asynchronous responses) is required because
otherwise very simple clients might inadvertently make requests that
will result in an asynchronous responses, and these kinds of responses
are likely to use disproportionately (relative to synchronous responses)
more server resources. We want to make DAP4 so that simple clients work
well and don't encounter unexpected 'hiccups.'

## <span id="Initial_processing_by_the_server" class="mw-headline"><span class="mw-headline-number">5</span> Initial processing by the server</span>

When a request is accepted by the server and it will result in an
asynchronous response, the server MUST the server MUST return a 202
(Accepted) HTTP status code and the [DAP Asynchronous Request
Accepted](https://docs.opendap.org/index.php?title=DAP4_Extension:_Asynchronous_Response#DAP_Asynchronous_Request_Accepted)
XML document. This document contains a URL to the pending result of the
request.

Of course, this discussion is about the mechanism that enables a client
to make a request and the server to provide *information about* an
asynchronous response to that request. It does not cover any of the
nearly infinite ways a server might actually make the *content* of that
response. It is likely that servers will write the responses to files
and the URL returned to the client will be used to retrieve that file,
but there's no requirement that servers do that. The only requirements
on server are that:

1.  The URL returned asserts, using the [constraint expression syntax
    for
    async](https://docs.opendap.org/index.php?title=DAP4_Extension:_Asynchronous_Response#DAP4_Constraint_Expression_extension_for_Async)
    that the client accepts async responses.
2.  The URL returned can be dereferenced and that operation will return
    the response requested by the client.

## <span id="Response_retrieval_by_the_client" class="mw-headline"><span class="mw-headline-number">6</span> Response retrieval by the client</span>

When a client requests an asynchronous result that is ready, the server
MUST return a 200 (OK) HTTP status code and the resulting data response.
If the client attempts to access the asynchronous result prior to it's
availability, the server SHOULD return an HTTP response status of [409
(DAP Response Not
Ready)](https://docs.opendap.org/index.php?title=DAP4_Extension:_Asynchronous_Response#409_Conflict_-_DAP4_Response_Not_Ready)
along with the [DAP Asynchronous Response Not
Available](https://docs.opendap.org/index.php?title=DAP4_Extension:_Asynchronous_Response#DAP4_Asynchronous_Response_Not_.28Yet.29_Available)
XML document. If the server does not return the 409 response status then
it MUST return a 404 (Not Found) response along with whatever document
it deems fit as the response body.

If the client attempts to access the asynchronous result after it is no
longer available, the server SHOULD return an [HTTP response status of
410
(Gone)](https://docs.opendap.org/index.php?title=DAP4_Extension:_Asynchronous_Response#410_Gone_-_DAP4_Response_No_Longer_Available)
along with the [DAP4 Asynchronous Response
Gone](https://docs.opendap.org/index.php?title=DAP4_Extension:_Asynchronous_Response#DAP4_Asynchronous_Response_Gone)
document. If the server does not return the 410 response status then the
server MUST return a 404 (Not Found) response along with whatever
document it deems fit as the response body.

In each case above where the server SHOULD return a specific error code,
but may return a 404 code instead, the intent is for servers to provide
the most appropriate use of HTTP/1.1's error codes while also providing
servers with an 'out' when that is hard for them to do. For example,
knowing that a response, which is essentially ephemeral, is gone would,
in theory, require to server to keep a record of every URL ever issued
for an asynchronous response and that is not practical. At the same
time, it is easy to see that a client would really like to know that the
response has not yet been finished (i.e., it has not waited long enough)
or that it is gone (i.e., it waited too long).

## <span id="Detail:_Client_requests" class="mw-headline"><span class="mw-headline-number">7</span> Detail: Client requests</span>

### <span id="DAP4_Constraint_Expression_extension_for_Async" class="mw-headline"><span class="mw-headline-number">7.1</span> DAP4 Constraint Expression extension for Async</span>

By adding a keyword/value pair to the DAP4 query string we can allow a
client to encode it's willingness to accept an asynchronous response,
along with the a maximum amount of time the client can wait before it
can access the response.

dap4.async  
A value of zero indicates the client is willing to unconditionally
accept an asynchronous response. A positive integer value will be
interpreted as the number of seconds that the client will wait for
access to the response. If the value is negative the serve MUST return
an error.

<!-- -->

Examples  
Client is willing to unconditionally accept an asynchronous response

`?dap4.async=0`

Client is willing to wait for 60 seconds for access to the asynchronous
response

`?dap4.async=60`

### <span id="X-DAP-Async-Accept" class="mw-headline"><span class="mw-headline-number">7.2</span> X-DAP-Async-Accept</span>

A client may indicate willingness to accept asynchronous responses by
including the *X-DAP-Async-Accept* HTTP header. Clients can make
conditional requests for asynchronous responses by indicating the
maximum time they are willing to wait by using the
**X-DAP-Async-Accept** HTTP header with a value given in seconds. A
value of zero indicates that the client is willing to accept whatever
delay the server may encounter.

## <span id="Detail:_Server_responses" class="mw-headline"><span class="mw-headline-number">8</span> Detail: Server responses</span>

Several 'experimental' HTTP headers are used by this design. They convey
information either in the request (like the *X-DAP-Async-Accept*
described above) or they encode information for a response. While only
clients that intend to support asynchronous responses need to understand
all of these, *every* client SHOULD understand the
*X-DAP-Async-Required* header. Because we need to support clients like
web browsers, knowledge of that header is not required, but
DAP4-specific clients will provide the most information to users if they
know to look for at least that response header.

### <span id="HTTP_Response_Headers" class="mw-headline"><span class="mw-headline-number">8.1</span> HTTP Response Headers</span>

#### <span id="X-DAP-Async-Required" class="mw-headline"><span class="mw-headline-number">8.1.1</span> X-DAP-Async-Required</span>

The *X-DAP-Async-Required* HTTP response header is included in the
response if the request requires an asynchronous response and the client
has not indicated willingness to accept such a response. Rejection of
the request should also be indicated by the [400 DAP Asynchronous
Response
Required](https://docs.opendap.org/index.php?title=DAP4_Extension:_Asynchronous_Response#400_DAP4_Asynchronous_Response_Required)
HTTP response code.

#### <span id="X-DAP-Async-Accepted" class="mw-headline"><span class="mw-headline-number">8.1.2</span> X-DAP-Async-Accepted</span>

The *X-DAP-Async-Accepted* HTTP response header is included in the
response if the server has accepted an asynchronous request. Acceptance
of the request should also be indicated by the [202 Asynchronous Request
Accepted](https://docs.opendap.org/index.php?title=DAP4_Extension:_Asynchronous_Response#202_Accepted)
HTTP response code.

### <span id="HTTP_Response_Codes" class="mw-headline"><span class="mw-headline-number">8.2</span> HTTP Response Codes</span>

HTTP provides a number of response codes beyond the simple 200 (OK), 404
(Not Found) and 500 (Internal Server Error). In this design we describe
how those standard codes SHOULD be used by DAP4 servers. We don't
enumerate all of the possible codes, instead opting for a description of
those that most relevant.

#### <span id="202_Accepted" class="mw-headline"><span class="mw-headline-number">8.2.1</span> 202 Accepted</span>

A server indicates that a request has been accepted and will be handled
asynchronously by returning a '202 Accepted' HTTP response code. The
response body must contain a document in one of the asynchronous
information media types listed
[below](https://docs.opendap.org/index.php?title=DAP4_Extension:_Asynchronous_Response#Media_Types).
A server MUST return this response, and only do so, when a client has
indicated a willingness to process an asynchronous response and the
response will actually be returned using the asynchronous mechanism.

#### <span id="400_DAP4_Asynchronous_Response_Required" class="mw-headline"><span class="mw-headline-number">8.2.2</span> 400 DAP4 Asynchronous Response Required</span>

The '400 DAP Asynchronous Response Required' HTTP response code is used
to indicate that the DAP4 request has been rejected because an
asynchronous response is required and the client did not indicate
willingness to accept an asynchronous response.

The response code text is used to indicate the reason for the rejection.
However, since the '400' HTTP response code is not specific to
asynchronous DAP (the standard text for the '400' code is "Bad
Request"), the *X-DAP-Async-Required* HTTP response header is also
included in the response (see
[above](https://docs.opendap.org/index.php?title=DAP4_Extension:_Asynchronous_Response#Accept_DAP_Asynchronous_Response)).

**Note** that a standard 400 HTTP response code is returned. In this
way, a client that does not understand asynchronous DAP can fail
gracefully. The response code text message has been changed to be more
informative of the reason for the failure. For clients that are aware of
asynchronous DAP, the "DAP-Async-Required" header is set to "true". The
body of the response also returns some information the client can use to
decide on how it will continue.

#### <span id="409_Conflict_-_DAP4_Response_Not_Ready" class="mw-headline"><span class="mw-headline-number">8.2.3</span> 409 Conflict - DAP4 Response Not Ready</span>

The '409 Conflict' HTTP response code MAY be returned by a server to
indicate that the DA4P request has been rejected because a previous
asynchronous request has not been completed and the result is not ready
for access. If a server utilizes the '409 Conflict' HTTP response code
it must also return a [DAP4 Asynchronous Response Not Yet
Available](https://docs.opendap.org/index.php?title=DAP4_Extension:_Asynchronous_Response#DAP4_Asynchronous_Response_Not_.28Yet.29_Available)
document in the response body.

#### <span id="410_Gone_-_DAP4_Response_No_Longer_Available" class="mw-headline"><span class="mw-headline-number">8.2.4</span> 410 Gone - DAP4 Response No Longer Available</span>

The '410 Gone' HTTP response code MAY be used by a server to indicate
that the result of an asynchronous request is no longer available. If a
server utilizes the '410 Gone' HTTP response code it must also return a
[DAP4 Asynchronous Response
Gone](https://docs.opendap.org/index.php?title=DAP4_Extension:_Asynchronous_Response#DAP4_Asynchronous_Response_Gone)
document in the response body.

#### <span id="412_Precondition_Failed" class="mw-headline"><span class="mw-headline-number">8.2.5</span> 412 Precondition Failed</span>

The '412 Precondition Failed' HTTP response code is used to indicate
that the DAP request has been rejected because it did not meet the
**X-DAP-Async-Accept** condition (see
[above](https://docs.opendap.org/index.php?title=DAP4_Extension:_Asynchronous_Response#Accept_DAP_Asynchronous_Response_Conditionally_on_Estimated_Time_to_Completion))
that was specified in the request.

#### <span id="500_Internal_Error" class="mw-headline"><span class="mw-headline-number">8.2.6</span> 500 Internal Error</span>

The '500 Internal Error' HTTP response code is used to indicate that the
DAP request has caused an error on the server. The request body and
other headers must be compliant with the [DAP4 Error
Response](https://docs.opendap.org/index.php?title=DAP4_Web_Services_v3#DAP4_Error_Response "DAP4 Web Services v3")
and [Status
Codes](https://docs.opendap.org/index.php?title=DAP4_Web_Services_v3#Status_Codes "DAP4 Web Services v3")
sections of the [web services
specification](https://docs.opendap.org/index.php?title=DAP4_Web_Services_v3 "DAP4 Web Services v3").
The request should not be repeated.

### <span id="Asynchronous_Response_Documents" class="mw-headline"><span class="mw-headline-number">8.3</span> Asynchronous Response Documents</span>

The uses of these documents are:

-   to inform clients that a request will result in an asynchronous
    response;
-   to provide clients with the status of an an accepted asynchronous
    request; and
-   to inform clients that a request for and asynchronous response has
    been rejected.

These response documents are the payloads to various responses,
including errors. By using the HTTP 400-series error response codes, the
design ensures that generic web clients will understand that their
request was in error (even if they don't really understand why). The
text provided with the response code will be sufficient that person
could understand the gist of the problem, if not more. The response
documents described here, along with the *X-DAP* describe above, are a
way of providing additional information to a savvy client so that it can
take full advantage of the synchronous response system.

These documents are XML that follows the DAP Asynchronous XML schema and
are declared in the namespace
**http://opendap.org/ns/dap/asynchronous**.

#### <span id="DAP4_Asynchronous_Response_Required" class="mw-headline"><span class="mw-headline-number">8.3.1</span> DAP4 Asynchronous Response Required</span>

This document informs clients that a request will result in an
asynchronous response, and that the client has not yet indicated it's
willingness to accept an asynchronous response. It might seem
superfluous to include a document that clearly only a client
knowledgable about the asynchronous response features could parse, but
many such clients may not, as a matter of course, indicate they will
accept these responses. For example, a user-configurable parameter might
be turn off support for the feature. The *expectedDelay* and
*responseLifetime* elements convey information about conditions the
clients can expect if it submits an asynchronous request for the
response. As noted below, these are estimates made by the server since a
number of things that the server cannot predict can affect them in the
interleaving time between the client's requests. Additionally, a server
MAY return values of zero for either of the values, indicating that it
cannot make an accurate estimate.

    <AsynchronousResponse status="required">
      <expectedDelay seconds="600" />
      <responseLifetime seconds="3600"/>
    </AsynchronousResponse>

This response MUST be associated with the 400 HTTP response code and the
*X-DAP-Async-Required* response header.

#### <span id="DAP4_Asynchronous_Request_Accepted" class="mw-headline"><span class="mw-headline-number">8.3.2</span> DAP4 Asynchronous Request Accepted</span>

This response informs clients that a request resulting in an
asynchronous response has been accepted, along with operational
information about retrieving the asynchronous response result. Note that
the *expectedDelay* and *responseLifetime* elements are an estimate by
the server. A server SHOULD ensure that the response will remain
available for the time period given by *expectedDelay* and
*responseLifetime*. We say *SHOULD* and not *MUST* because we cannot
predict all possible operational situations where these kinds of
responses might be used. For example, a server might be providing access
for several types of users who might have different access priorities,
especially to limited resources like those typically involved with
asynchronous access, and thus some responses might be further delayed,
or removed early, to enable processing of requests from users with
higher priority. It should be kept in mind, however, that the usefulness
of the asynchronous responses will depend, in part, on servers providing
a facility on which clients can depend.

While the *expectedDelay* and *responseLifetime* elements are required,
a server MAY set their *seconds* attribute to *0* to indicate that it
cannot provide a reliable value. In this case, clients SHOULD poll every
300 seconds and servers SHOULD expect this behavior. This is the default
TCP user timeout period (see
<a href="http://tools.ietf.org/html/rfc5482" class="external free"
rel="nofollow">http://tools.ietf.org/html/rfc5482</a>).

    <AsynchronousResponse status="accepted">
      <expectedDelay seconds="600" />
      <responseLifetime seconds="3600"/>
      <link href="http://server.org/async/path/result" />
    </AsynchronousResponse>

This response document MUST be associated with the 202 HTTP status code
and the *X-DAP-Async-Accepted* response header.

#### <span id="DAP4_Asynchronous_Response_Not_(Yet)_Available"></span><span id="DAP4_Asynchronous_Response_Not_.28Yet.29_Available" class="mw-headline"><span class="mw-headline-number">8.3.3</span> DAP4 Asynchronous Response Not (Yet) Available</span>

This document informs clients that a while a previous request for an
asynchronous response has been accepted, the result is not available.

    <AsynchronousResponse status="pending"/>

This response document MUST be associated with the [409 HTTP response
code](https://docs.opendap.org/index.php?title=DAP4_Extension:_Asynchronous_Response#409_Conflict_-_DAP4_Response_Not_Ready).

Servers SHOULD return this response document and it's associated HTTP
status of 409, but servers MAY return any document in the response body
along with either a a 404 (Not Found) or a 400 (Bad Request) HTTP
status.

#### <span id="DAP4_Asynchronous_Response_Gone" class="mw-headline"><span class="mw-headline-number">8.3.4</span> DAP4 Asynchronous Response Gone</span>

This document informs clients that a while a previous request for an
asynchronous response has been accepted, the result is *no longer*
available.

    <AsynchronousResponse status="gone"/>

This response document MUST be associated with the [410 HTTP status
code](https://docs.opendap.org/index.php?title=DAP4_Extension:_Asynchronous_Response#410_Gone_-_DAP4_Response_No_Longer_Available).

Servers SHOULD return this response document and it's associated HTTP
status of 410, but servers MAY return any document in the response body
along with either a a 404 (Not Found) or a 400 (Bad Request) HTTP
status.

#### <span id="DAP4_Asynchronous_Request_Rejected" class="mw-headline"><span class="mw-headline-number">8.3.5</span> DAP4 Asynchronous Request Rejected</span>

This document informs clients that a request for an asynchronous
response has been rejected, even though the client said it is willing to
process an asynchronous response. There are at least as many reasons a
server might reject the request for an asynchronous response as there
are systems that might return such responses. However, this design
provides suggested response codes for cases that seem likely so that
clients can make educated decisions about the reason for the rejection.
The reason codes supported are:

time  
The client indicated that it was only willing to wait *X* seconds and
the server thought it would take more time to build the result.

unavailable  
A needed resource is not available. This might indicate that hardware,
like a robot tape system, cannot be currently accessed.

privileges  
The client is not allowed to make the request.

other  
Self evident...

In addition to the reason codes, this response will contain a text
description of the reason for rejection.

Servers SHOULD make every effort to use the correct reason codes and
provide cogent descriptions.

    <AsynchronousResponse status="rejected">
        <reason code="time"/>
        <description>Acceptable access delay was less than estimated delay.</description>
    </AsynchronousResponse>

This response document MUST associated with the 412 HTTP status code.

Servers SHOULD return this response document along with an HTTP status
of 412, but servers MAY return any document in the response body along
with an HTTP status of 404 (Not Found) or of 400 (Bad Request) in its
place.

#### <span id="DAP4_Error" class="mw-headline"><span class="mw-headline-number">8.3.6</span> DAP4 Error</span>

If the server encounters an error it must MUST (MAY?) return an HTTP
status of 500 (Internal Error) along with a request body and other
headers compliant with the [DAP4 Error
Response](https://docs.opendap.org/index.php?title=DAP4_Web_Services_v3#DAP4_Error_Response "DAP4 Web Services v3")
and [Status
Codes](https://docs.opendap.org/index.php?title=DAP4_Web_Services_v3#Status_Codes "DAP4 Web Services v3")
sections of the [web services
specification](https://docs.opendap.org/index.php?title=DAP4_Web_Services_v3 "DAP4 Web Services v3").
The request should not be repeated.

## <span id="Examples" class="mw-headline"><span class="mw-headline-number">9</span> Examples</span>

### <span id="Constrained_Data_Request-Response_using_GET" class="mw-headline"><span class="mw-headline-number">9.1</span> Constrained Data Request-Response using GET</span>

Simple Request  

    GET /dap/path/data.nc?dap4.ce=x,y,temp HTTP/1.1
    Host: server.org

If the server decides it needs to handle this request in an asynchronous
manner, it will refuse the request because it did not say it would
accept an asynchronous response.

Response  

    400 DAP Asynchronous Response Required
    X-DAP-Async-Required: true
    Content-Type: text/xml;charset=UTF-8
     
    <AsynchronousResponse status="required">
      <expectedDelay seconds="600" />
      <responseLifetime seconds="3600"/>
    </AsynchronousResponse>

### <span id="Constrained_Data_Request-Response_with_DAP-Async-Accept_Request_Header" class="mw-headline"><span class="mw-headline-number">9.2</span> Constrained Data Request-Response with DAP-Async-Accept Request Header</span>

Request:

    GET /dap/path/data.nc?dap4.ce=x,y,temp HTTP/1.1
    Host: server.org
    X-DAP-Async-Accept: 0

Alternately, this request would produce the same result using only the
URL:

    GET /dap/path/data.nc.dap?dap4.async=0&dap4.ce=x,y,temp HTTP/1.1
    Host: server.org

Response:

    202 Accepted
    Content-Type: text/xml;charset=UTF-8

    <AsynchronousResponse status="accepted">
      <expectedDelay seconds="600" />
      <responseLifetime seconds="3600"/>
      <link href="http://server.org/async/path/result" />
    </AsynchronousResponse>

**NB**: This example originally included an *Accept* header with the
value of *multipart/mixed*. However, that is not a good example. The
HTTP/1.1 specification says that when a specific media type is indicated
as the only one acceptable, a server must return a 406 response code if
it cannot return that media type. The meaning of *Accept: \*/\** is the
same as not including the header, so I have removed the header from
these examples. We need to be heads up in the ways that we suggest that
header should be used by clients

### <span id="Constrained_Data_Request-Response_with_conditional_DAP-Async-Accept_Request_Headers" class="mw-headline"><span class="mw-headline-number">9.3</span> Constrained Data Request-Response with conditional DAP-Async-Accept Request Headers</span>

Request:

    GET /dap/path/data.nc?dap4.ce=x,y,temp HTTP/1.1
    Host: server.org
    X-DAP-Async-Accept: 60

Alternately, this request would produce the same result using only the
URL:

    GET /dap/path/data.nc.dap?dap4.async=60&dap4.ce=x,y,temp HTTP/1.1
    Host: server.org

Response:

    412 Precondition Failed
    Content-Type: text/xml;charset=UTF-8
     
    <AsynchronousResponse status="rejected">
        <reason code="time"/>
        <description>Acceptable access delay was less than estimated delay.</description>
    </AsynchronousResponse>

### <span id="Premature_Request_For_Asynchronous_Result" class="mw-headline"><span class="mw-headline-number">9.4</span> Premature Request For Asynchronous Result</span>

Request:

    GET /async/path/data.nc?dap4.ce=x,y,temp HTTP/1.1
    Host: server.org

Alternately, this request would produce the same result using only the
URL:

    GET /async/path/data.nc?dap4.ce=x,y,temp HTTP/1.1
    Host: server.org

  
Response:

    409 Conflict
    Content-Type: text/xml;charset=UTF-8

    <AsynchronousResponse status="pending"/>

## <span id="Resource_Role" class="mw-headline"><span class="mw-headline-number">10</span> Resource Role</span>

DAP4 Asynchronous Responses are identified by the resource role:

**`http://services.opendap.org/dap4/async`**

## <span id="Normative_Encoding_of_the_Asynchronous_Response" class="mw-headline"><span class="mw-headline-number">11</span> Normative Encoding of the Asynchronous Response</span>

The normative XML representation for the Asynchronous Response is
defined in Appendix x "Normative XML Encoding of the Asynchronous
Response". The media type for the normative XML representation is:

`application/vnd.opendap.dap4.async.xml`
