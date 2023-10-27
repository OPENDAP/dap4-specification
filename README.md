# DAP4: Overview

Following two decades of stability and increasing use, DAP2 is being
superseded by DAP4, the first substantive revision in the history of the
Data Access Protocol (DAP), an open-source endeavor led by OPeNDAP, Inc.
The primary and continuing purpose of DAP is to realize *remote,
selective, data-retrieval as a widely-accepted and well-crafted Web
service*. This document outlines the fundamental concepts of DAP4, and
(targeting those who have already programmed DAP-compatible clients and
servers) it highlights how DAP4 differs from DAP2. <s>In the following,
DAP refers to DAP4 unless indicated otherwise.</s>

[TOC]

## Contents

-   [<span class="tocnumber">1</span> <span class="toctext">Data
    Retrieval as a Web
    Service</span>](#Data_Retrieval_as_a_Web_Service)
-   [<span class="tocnumber">2</span> <span class="toctext">Understanding the DAP Data
    Model</span>](#Understanding_the_DAP_Data_Model)
    -   [<span class="tocnumber">2.1</span> <span class="toctext">A
        Brief Data-Model
        Summary</span>](#A_Brief_Data-Model_Summary)
    -   [<span class="tocnumber">2.2</span> <span class="toctext">A
        Rough Glossary of Data-Model
        Entities</span>](#A_Rough_Glossary_of_Data-Model_Entities)
    -   [<span class="tocnumber">2.3</span> <span class="toctext">Higher-Level DAP Objects and
        Extensions</span>](#Higher-Level_DAP_Objects_and_Extensions)
-   [<span class="tocnumber">3</span> <span class="toctext">Client Use
    of a DAP Data
    Source</span>](https://#Client_Use_of_a_DAP_Data_Source)
    -   [<span class="tocnumber">3.1</span> <span class="toctext">High-Level Info about DAP Datasets: the
        DMR</span>](#High-Level_Info_about_DAP_Datasets:_the_DMR)
    -   [<span class="tocnumber">3.2</span> <span class="toctext">Retrieving Content from DAP Datasets: Posing DAP
        Requests</span>](#Retrieving_Content_from_DAP_Datasets:_Posing_DAP_Requests)
-   [<span class="tocnumber">4</span> <span class="toctext">The Formal
    DAP
    Specification</span>](#The_Formal_DAP_Specification)
-   [<span class="tocnumber">5</span> <span class="toctext">How DAP4
    Differs from
    DAP2</span>](#How_DAP4_Differs_from_DAP2)
    -   [<span class="tocnumber">5.1</span> <span class="toctext">Data-Model
        Changes</span>](#Data-Model_Changes)
    -   [<span class="tocnumber">5.2</span> <span class="toctext">Changed
        Responses</span>](#Changed_Responses)
    -   [<span class="tocnumber">5.3</span> <span class="toctext">Response-Encoding
        Changes</span>](#Response-Encoding_Changes)
    -   [<span class="tocnumber">5.4</span> <span lass="toctext">Changes in the Use of
        HTTP</span>](#Changes_in_the_Use_of_HTTP)
-   [<span class="tocnumber">6</span> <span class="toctext">Acknowledgments</span>](#Acknowledgments)

# <span id="Data_Retrieval_as_a_Web_Service" class="mw-headline"><span class="mw-headline-number">1</span> Data Retrieval as a Web Service</span>

The premise underlying DAP4 remains, as in DAP2, that values from data
sources—or, notably, from proper subsets—along with pertinent metadata
may be acquired remotely and effectively through an appropriately
defined Web service, operated near the source data. To a surprising
degree, DAP services shield users from idiosyncrasies in source-data
formats and storage, so DAP functions as middleware with a further
advantage: source-data and users may reside anyplace that has Internet
connectivity. OPeNDAP's commitment to open source has fostered several
DAP-compatible servers and an even larger number of DAP-compatible
client environments, several of which (i.e., servers, clients and
client-server libraries) are available at no cost.

DAP is designed for selectively retrieving (but not for storing) data
organized as variables or groups of variables. It is well suited to
cases where client computers retrieve data stored on remote computers
(i.e., servers) networked to the client, especially where data sources
are huge (comprising large arrays, e.g.) but clients typically need only
small subsets of them. The protocol is fundamentally stateless (some
might say “RESTful”), and it governs how clients pose requests and how
servers issue corresponding responses.

DAP's effectiveness is keyed on the underlying data model, which
embraces a rich variety of data types (including tabular and array
structures). Based on this model, DAP spells out the (type-specific)
retrieval operations that clients may request. The flexibility and
domain-neutrality of the DAP data model (which has changed modestly
between DAP2 and DAP4) make it effective—as middleware, per the
above—across a broad range of data types and disciplinary domains.
Stated another way, many kinds of data sources and schemas can be mapped
onto the DAP model for retrieval and use by client computers and
software.

# <span id="Understanding_the_DAP_Data_Model" class="mw-headline"><span class="mw-headline-number">2</span> Understanding the DAP Data Model</span>

## <span id="A_Brief_Data-Model_Summary" class="mw-headline"><span class="mw-headline-number">2.1</span> A Brief Data-Model Summary</span>

Unlike FTP and other protocols enabling clients to access whole files or
granules, DAP offers sub-granular retrievals, and this requires exposing
the detailed structure of each granule (called a “dataset” in DAP). To
this end, the structure of every DAP-accessible dataset is manifest in a
machine-readable document called the DMR. DMRs are declaration
statements that adhere formally to the DAP Data Model, which is
sufficiently general to make retrievable a variety of data granules and
data types whose semantics vary widely among the (potential) sources.

The DAP data model is built around a notion of “variables” that fall
into three classes—atoms, structures and sequences—and may be organized
as multidimensional arrays. As reflected in its DMR, all of a dataset's
variables are named, and they may optionally be grouped (in a hierarchy)
to add meaning and allow complex name-driven retrievals by clients. DAP
variables are (strongly) typed and optionally may have “attributes” and
“dimensions”, the former to clarify meaning and the latter to indicate a
variable's array shape (where relevant). Attributes resemble variables
except that the former may be assigned to the latter, but not vice
versa.

Much of DAP's power arises from its typing structure. The value(s) of an
atomic variable (whether or not dimensioned as an array) are all of the
same atomic type, indicated in the DMR to be integer, floating point,
character, string, etc. Structure variables are combinations of atom
variables joined for semantic reasons, such as to represent complex
numbers, vector-valued parameters, or other relationships among the
values of a dataset.

To address a difficult abstraction challenge—retrievals from both
array-oriented and database-oriented sources—DAP allows DMRs to declare
variables of type “Sequence”. A sequence is like a relation, i.e., a
table whose rows are “instances” or “records” and whose columns contain
the values of “fields”. In DAP, the content of a sequence may comprise
an arbitrary number of instances (i.e., records) whose “fields” are
values from other DAP variables.

For example, a sequence named “BirdTracking” might contain variables
named “BirdID”, “BandingEvent”, and “ObservedPosition”, and the contents
of BirdTracking would be instances that contain values of the specified
variables (fields). DAP allows arbitrary nesting of sequences and
structures, so in this example BandingEvent could be a structure
(containing date and location info for the bird's banding) and
ObservedPosition could be a sequence (containing equivalent date and
location info) whose instances represent subsequent bird observations.

Hypothetically, this is akin to making BirdTracking a structure with a
single dimension (though DAP does not allow arrays of indefinite
length). However, selective retrieval from an array would require
knowing the indices of desired instances, whereas a BirdTracking
sequence allows filtering-style retrievals that select instances on the
basis of their values.

## <span id="A_Rough_Glossary_of_Data-Model_Entities" class="mw-headline"><span class="mw-headline-number">2.2</span> A Rough Glossary of Data-Model Entities</span>

Much about DAP may be discerned from a dictionary or glossary-like list
of the key entities in its data model. Such a list follows, sequenced
for ease of understanding (rather than alphabetically). These
descriptions are not definitive, as the formal specification documents
take precedence over anything stated here.

**Data Source** - Though formally outside the DAP Data Model, the term
Data Source generally refers to all the datasets (see below) that may be
retrieved via DAP from a single server, identified by its domain name.
Servers sometimes offer (catalogs and/or inventories of) collections and
sub-collections, but the DAP Data Model focuses on granular and
sub-granular retrievals.

**Dataset** - Sometimes called a “granule” in catalog/inventory
parlance, a DAP Dataset is represented by a unique (unadorned) URL, and
is the highest-level entity (metadata as well as content) described by
the DAP Data Model. Clients invoke retrieval operations by adorning the
Dataset URL with suffixes and query strings interpreted by the server.

**Declarations and the DMR** - For a specific Dataset, all aspects of
the DAP Data Model (name assignments, structural definitions, etc) are
governed by a formal declarations document. Created as part of making a
Dataset DAP-retrievable, this document is dubbed the DMR (roughly:
Dataset Metadata Response), and clients may retrieve DMRs alongside or
independently of Dataset contents.

**Name** - Most entities in the DAP Data Model may or must be named.
With some constraints on the use of special characters (such as “.”), a
Name can be any character string. To avoid conflicts, DAP has scoping
rules. For example, a Variable and a Dimension may have the same Name
without ambiguity, but two Variables can have the same Name only if they
are declared in different Groups or structures.

**Variable** - The building blocks for the DAP Data Model are Variables,
which are strictly typed. Three classes of them (atoms, structures and
sequences) are described separately below, but in actuality these are
best distinguished by inspecting their Type declarations. Each Variable
must be assigned a Type and a Name, and it may optionally have a number
of Dimensions and Attributes, elaborated below.

**Type** - Underpinning DAP's “container” Types (Structure and Sequence,
implied above) are “atomic” Types akin to those of computer languages:
bytes, integers, floating-point values, strings, and URLs, plus an enum
type (permitting specified character strings, such as days of the week,
to be treated as variable values) and an opaque type (permitting
arbitrary blobs of bits). More detailed Type descriptions are provided
in Volume I of the DAP specification.

**(Atom) Variable** - A Variable whose Type is atomic (see above)
comprises a single value or an array of values, and all its values are
of the designated Type. A Variable is an array only if its declaration
includes Dimensions, which determine the array's shape and its
element-ordering (see below).

**(Structure) Variable** - A Variable of Type “Structure” is a container
for other variables, often implying relationships among them. For
example, a structure Variable named “Velocity” might contain a pair of
atom Variables (or fields) named “x” and “y,” representing components of
a velocity vector. These components would be retrieved via their
“qualified” Names, “Velocity.x” and “Velocity.y”.

*Notes on Structures:*

-   Structures may contain variables of any type, including other
    structures.
-   A contained variable can be used in the context of several
    containers, but these contexts create separate, independent
    instances.
-   If the semantics of a variable are altered by its context, it should
    be separately declared in each relevant context. For example,
    declarations for the atoms “Velocity.x” and “Displacement.x” should
    be distinct and separate (falling within “Velocity” and
    “Displacement” declarations respectively) despite reuse of the name
    “x”.
-   Though a dimensioned structure resembles a structure containing
    dimensioned variables (with the same shapes), these are not
    equivalent, and the means for referencing them differ. For example,
    array element i,j would be referenced as:
    -   Velocity\[i,j\].x if two dimensions are assigned to the Velocity
        structure.
    -   Velocity.x\[i,j\] if two dimensions are assigned to its
        x-component variable.

**(Sequence) Variable** - A Variable of Type “Sequence” is a container
holding multiple (unordered) instances of other DAP Variables. For
example, a sequence Variable named “TracerParticle” might contain a pair
of structures named “Velocity” and “Displacement”, each declared—as in
an earlier example—to have x and y components. The instances of
TracerParticle would be like a set of tabular records whose four fields,
Displacement.x, Displacement.y, Velocity.x, and Velocity.y are retrieved
via filter-style (rather than indexed) retrievals, as discussed in a
later section on Constraints.

*Notes on Sequences:*

-   Sequences may contain variables of any type, including other
    sequences.
-   Though a sequence is similar in some respects to a structure with a
    single (indexing) dimension, the differences are significant. For
    example, if a DAP server offers retrieval of records from a
    relational data base:
-   The most useful client retrievals may entail filtering based on the
    values in the fields, and this yields indexing gaps. In other words,
    indexing may have little or no utility.
-   The number of records may be hidden or dynamic, so a dimension
    length cannot be calculated, and the order in which records are
    returned may be volatile.

**Group** - The DAP Data Model has a hierarchical mechanism for grouping
Variables and carving out independent namespaces. Groups may be nested,
and all but one must have Names, the exception being the root of the
hierarchy, where the Dataset itself is a Group (needing no name).
Retrieving a Variable whose declaration falls within a Named Group
requires use of its fully qualified name (FQN), such as
GroupA.Group2.Velocity. Any Group (including the Dataset) may be
assigned Attributes but not Dimensions.

**Attribute** - Otherwise nearly indistinguishable from a Variable, an
Attribute must always be assigned to a specific Variable or Group. The
purpose of Attributes is to provide context or add meaning to the
assigned entities, whereas the purpose of Variables is to convey primary
content. Retrieving an Attribute always requires prepending the name of
the Variable or Group to which it is assigned, which implies that
Attribute Names (such as “Units”) enjoy unlimited reusability.

**Dimension** - A Dimension must have a size and may have a Name. A
Variable of any type may optionally be assigned a number of Dimensions,
in which case its (compound) values are organized and retrieved as an
indexible array of rank n, where n is the number of assigned Dimensions.

*Notes on Dimensions:*

-   Named Dimensions resemble named constants. Indeed, assigning a named
    dimension to multiple variables (within the scope of a single group)
    has the same effect on each, giving definition to that variable's
    array shape and array-element ordering.
-   Unlike attributes, dimensions often are declared outside the
    variables to which they are assigned. Groups may not accept
    dimension assignments, but groups limit the scope of the dimension
    names and sizes declared within them.
-   Dimensions names may be reused, with differing sizes across multiple
    groups.
-   The order of the dimension assignments in a variable declaration is
    significant, as this determines the variable's array-element
    ordering as well as its shape.
-   Retrieving a dimension may require prepending the name of the group
    in which it was declared but never the name of a variable to which
    it has been assigned.
-   A Dimension's size must be a positive integer less than 2^61.

## <span id="Higher-Level_DAP_Objects_and_Extensions" class="mw-headline"><span class="mw-headline-number">2.3</span> Higher-Level DAP Objects and Extensions</span>

Shared Dimensions that serve to indicate relations between different
arrays which can be used to build/represent Coverages...

Note: Though adoption to-date has been most pronounced in Earth
sciences, DAP's data types and structures (with the possible exception
of coverages, discussed in this section) are not at all specific to
these disciplines, so we think DAP is positioned for effective use in
many domains, scientific and otherwise.

# <span id="Client_Use_of_a_DAP_Data_Source" class="mw-headline"><span class="mw-headline-number">3</span> Client Use of a DAP Data Source</span>

## <span id="High-Level_Info_about_DAP_Datasets:_the_DMR" class="mw-headline"><span class="mw-headline-number">3.1</span> High-Level Info about DAP Datasets: the DMR</span>

A client's first step in selectively retrieving a data source often is
to discern the character (i.e., its schema) by requesting what DAP calls
the DMR (the data-source metadata response). A DMR provides a complete
characterization of the associated data source sans content, spelling
out its groups, variables, types, dimensions, and attributes as
discussed in the preceding two subsections. For ease of use in client
software, the DMR adheres to a formal syntax and most often is delivered
as an XML document, though other forms are anticipated as DAP4
*extensions*.

Though it is common to retrieve its DMR prior to requesting content from
a data source, this is not the only option. Indeed, a "Data Request"
under DAP returns both the DMR and the content (i.e., the *values* of
variables) for the designated data source, because the former is
critical for interpreting the latter.

## <span id="Retrieving_Content_from_DAP_Datasets:_Posing_DAP_Requests" class="mw-headline"><span class="mw-headline-number">3.2</span> Retrieving Content from DAP Datasets: Posing DAP Requests</span>

Under DAP, the requests clients make of servers, and the resulting
server responses, are all governed by the protocol specification. As
stated previously, the formal specification takes precedent over
anything stated here.

For each data source, a number of responses may elicited by a client,
determined by adding a suffix and/or a query string to the basic URL for
the desired data source. Passing the server a completely *unadorned* URL
yields a Dataset Services Response (DSR). This XML document describes
the various DAP services available for that source, and these always
include provision of a DMR and provision of *content* from the source.
Unlike the DMR, which is always textual, content (delivered in response
to a Data Request, as discussed above) may be conveyed in textual *or*
binary form, the latter minimizing data-transfer volumes, of course.

If the URL for a Data Request includes a query string, the server parses
this string to determine what data processing the server should perform
before constructing its Data Response. Though other classes of
pre-retrieval processing are anticipated to be defined via DAP
extensions, two forms are mandated by DAP4 for all servers, Index
Subsetting and Field Subsetting, and a third form, Filtering, is defined
in the core DAP specification, though its implementation by servers is
optional.

**Index Subsetting** - Choosing parts of an array based on the indexes
of that array's dimensions. This operation always returns an array of
the same rank as the original, although the size of the return array
will (likely) be smaller. Index subsetting uses the bracket syntax
described later.

**Field Subsetting** - Choosing specific variables or fields from the
dataset. A dataset in DAP4 is made up of a number of variables and those
may be Structures or Sequences that contain fields (and, in effect, the
Dataset is itself a Structure and all of its variables are fields - the
distinction is more convenience than formal). Field subsetting using the
brace syntax described later. One or more fields can be specified using
a semicolon (;) as the separator.

**Filtering** - A filter is a predicate that can be used to choose data
elements based on their values. the vertical bar (|) is used as a prefix
operator for the filter predicate. Filters can be applied to elements of
an Array or fields of a Sequence. A filter predicate consists of one or
more filter subexpressions. One or more subexpressions can be specified,
using a comma (,) as the separator.

Other services listed in the DSR might (at the server's option) include
the DAP Asynchronous Response. Where implemented (such as for near-line
data sources), this response is sent to the client when the requested
resource (DMR, Data Response, etc.) is not immediately available. If, in
turn, the client makes a "retrieve it" request, the server will respond
with a second Asynchronous Response informing the client about when and
where the requested resource may be retrieved.

In addition to the most common data objects, a DAP server *may* provide
additional "services," such as HTML-formatted representations of a data
source's structure and content. Such additional services are discussed
in Volume 2 of the specification.

# <span id="The_Formal_DAP_Specification" class="mw-headline"><span class="mw-headline-number">4</span> The Formal DAP Specification</span>

The DAP4 specification spans two volumes: one describes the Data Model
and DAP's Request/Response objects; the other volume describes how DAP
clients and servers communicate via HTTP and the modern Web. New volumes
about DAP Extensions will be added as they emerge.

Partitioning the specification into two primary documents reflects the
independence of DAP's data-retrieval functionality from the underlying
network transfer protocol. Indeed, DAP could be used with other
transports. However, utilizing HTTP eases the building of DAP servers
because they can take full advantage of widely used Web-server
frameworks such as Apache. Use of Extensions documents will enable
evolution of the protocol without the expense and complexity of another
major protocol-development project. Anticipated extensions include a
JSON encoding for DAP data/metadata and the provision of server
functions (beyond DAP's core subsetting and filtering operations).

**The specification is available at these links:**

-   [Volume 1: Data Model, Persistent Representation, and
    Constraints](https://docs.opendap.org/index.php?title=DAP4:_Specification_Volume_1 "DAP4: Specification Volume 1")
-   [Volume 2: Web Services
    Specification](https://docs.opendap.org/index.php?title=DAP4:_Specification_Volume_2 "DAP4: Specification Volume 2")
-   Extensions:
    -   [DAP4 Extension: CSV Data Encoding and
        Response](https://docs.opendap.org/index.php?title=DAP4_Extension:_CSV_Data_Encoding_and_Response "DAP4 Extension: CSV Data Encoding and Response")
    -   [DAP4 Extension: Asynchronous
        Response](https://docs.opendap.org/index.php?title=DAP4_Extension:_Asynchronous_Response "DAP4 Extension: Asynchronous Response")

# <span id="How_DAP4_Differs_from_DAP2" class="mw-headline"><span class="mw-headline-number">5</span> How DAP4 Differs from DAP2</span>

Though the protocol, per se, is maintained primarily by OPeNDAP, many
others have engaged in DAP2 realization. One implementation—by Unidata,
in the University Corp. for Atmospheric Research—includes the popular
THREDDS Data Server (TDS). A key motivation for DAP4, developed jointly
by OPeNDAP and Unidata, was to reduce differences that have arisen, and
impede interoperability, among DAP2 realizations. Our hope is that a
modernized, clearer and more comprehensive specification will facilitate
building clients and servers with greater interoperability, making such
ventures more rewarding and less risky.

This section covers changes to the data model, response formats, and
serialization, giving developers a roadmap to migration from DAP2 to
DAP4. E.g., the “Grid” type now supports a notion of discrete functions
similar to an OGC/ISO Discrete Coverage and to the Scientific Data Type
found in Unidata's Common Data Model (CDM). Also from this section,
users may learn of functionalities to seek in clients. E.g., DAP4
servers return checksums with each data response, but clients may
utilize these in varying degrees.

DAP4 is largely an extension of DAP2 concepts, including ideas that
emerged as DAP gained prominence across the Earth sciences. Therefore
DAP2-compatible software, in clients or servers, should be easy to adapt
to DAP4, and this has been affirmed in the OPeNDAP-Unidata realization
and testing work. Furthermore, DAP4 exhibits backward compatibility
sufficient to enable gradual transitioning. Substantive changes include
support for Groups, yielding greater compatibility with HDF and NetCDF4.

## <span id="Data-Model_Changes" class="mw-headline"><span class="mw-headline-number">5.1</span> Data-Model Changes</span>

**Summary**: DAP4 now supports groups, a generalized form of a grid
datatype and a few new atomic types.

The DAP4 data model is fundamentally similar to that for DAP2. New
atomic types include: enumeration, 64-bit integer, and opaque, and the
container types now include groups. Groups provide a way to organize
collections of variables and dimensions and to encode these
organizational relationships when they are present in the underlying
source data.

Dimensions may now be named, and the presence of shared dimensions
(i.e., several variables employ a dimension with a given name) along
with explicitly name 'maps' serves to indicate relationships among
arrays that can, in turn, be used to build/represent a more general form
of the DAP2 Grid datatype that resembles the OGC/ISO "discrete coverage"
datatype. These 'discrete coverages' subsume the role of DAP2 Grids, so
the latter have been removed from DAP4.

**Migrating from DAP2 to DAP4**

For servers: A DAP2 DDS/DAS (or DDX) is very close to a DAP4 DMR
(indeed, our C++ library contains a way to build a DMR from a DDS). The
set of datatypes supported by DAP4 is almost a proper superset of those
in DAP2, the exception being that DAP2's Grid type has been removed. To
represent a DAP2 Grid in DAP4, the components of the DAP2 Grid are
retained and the appropriate Shared Dimension and Map elements are added
to the dataset/group and array. Since the DAP4 'discrete coverage' type
subsumes the DAP2 Grid, it will always be possible to translate a DAP2
Grid into DAP4

For clients: Some of the new data types are more challenging to
implement than the types included with DAP2. Of particular note are
Enumerations and the expanded grid (aka 'discrete coverage') types.

## <span id="Changed_Responses" class="mw-headline"><span class="mw-headline-number">5.2</span> Changed Responses</span>

**Summary or the main changes between DAP2 and DAP4 Responses**:

-   DAP4 includes only one dataset *metadata* response, not two;
-   Several Sequences may be individually constrained in one access;
-   Predictable behavior for 'bare' URLs; and
-   Asynchronous responses

In DAP4 there is a single XML document that encodes the metadata for a
data source. This response is conceptually similar to, and in some ways
identical too, the *DDX* response that is supported by many DAP2
servers, so it's organization will be familiar to many people already.
As with DAP2, there is one data response that can be modified
(*constrained*) using a expression to limit the information it includes.
The basic concepts of slicing an array are unchanged in DAP4. We've
taken care to allow servers to extend the information passed into the
data retrieval web service, a topic that is covered in a bit more detail
below under *web services.* We have replaced the *selection* part of the
DAP2 constraint expression with a *filter* sub-expression that is
applied to specific variables. This enables two or more Sequences to
have their own filtering operations (before that was not possible). Our
expanded constraint language also provides a way to subset coverages,
and a proposed extension to the filtering sub-expression provides a way
to subset arrays/coverages by value.

We wanted DAP4 to fully embrace REST. DAP2, even though it predates the
term, including many, but not all, of the REST architecture's features.
One change from DAP2 was to explicitly define what happens when a client
dereferences a 'bare URL' (one without an extension used to ask for a
specific DAP4 response). When a DAP4 sever is asked to return
information at a bare URL, the result is a Dataset Services Response
(DSR) which contains links to all of the other responses for that
dataset. In addition, the DSR may contain other information such as
server operations that can be used with the dataset. The DSR is an XML
document but can contain a stylesheet that transforms it to HTML for a
web browser.

DAP4 servers can also support asynchronous access to data, which enables
access to data from near-line devices and can be used for some server
processing operations (e.g., operations that take a long time to
perform). Asynchronous responses are responses that contain a URL that
can be used to retrieve the actual data at some time in the future. The
protocol has been designed to reduce the chance that a client will
mistakenly make a large number of asynchronous requests since this could
present an undue burden on some kinds of near-line devices.

**Migrating from DAP2 to DAP4**

-   If your server or client already reads DAP2 DDX responses (which
    were never part of the official protocol but are widely used) then
    adapting to the DMR will be very easy since they are very close in
    structure.
-   Support for the new constraints may take a bit more work since now
    the Constraint Expression and Server Functions have been separated.
-   Clients will benefit from asynchronous response support, but this is
    a new behavior and may take some serious thought, particularly for
    clients that relied on the simpler semantics borrowed from file
    system accesses.

## <span id="Response-Encoding_Changes" class="mw-headline"><span class="mw-headline-number">5.3</span> Response-Encoding Changes</span>

**Summary**:

-   Checksums for data values;
-   Reliable delivery of error messages to clients;
-   Encode data using the server's native word order.

We have added three changes to the encoding of returned data values. All
top-level variables in a data response now include a CRC32 checksum of
their values. This enables people to see if a request is returning the
same data values as it did previously. The checksum values are encoded
in Attributes bound to the returned variables. We have added an encoding
scheme for data values that preserves compactness yet allows clients to
easily detect when a server has encountered an error while sending a
response. Similarly, we have adopted a *Reader Make Right* encoding
scheme instead of the *network byte order* scheme used by DAP2. The
latter has become more and more important as the predominance of
little-endian processors has increased.

**Migrating from DAP2 to DAP4**

In many ways the encoding scheme is simpler for servers because the data
response uses the server's native byte order. Clients must detect the
byte order and twiddle bytes as needed. However, the server must
correctly implement the chunking protocol used by the data response and
must correctly computer CRC32 checksums for each of the top level
variables.

## <span id="Changes_in_the_Use_of_HTTP" class="mw-headline"><span class="mw-headline-number">5.4</span> Changes in the Use of HTTP</span>

**Summary**: DAP4 is closer than DAP2 to the REST (Representational
State Transfer) architecture, and it uses HATEOS (Hypermedia As The
Engine Of Application State), making all of the server's responses
explicit via links in a document.

While DAP2 interwove the DAP and HTTP, using, for example, some of the
HTTP headers as the only source of information that was critical to the
DAP itself, DAP4 does not. Instead, DAP4 is completely isolated from
HTTP, enabling it to work with other protocols without change. However,
in as much as HTTP is a ubiquitous network transport protocol, the DAP4
specification includes a volume devoted solely to how a server should
implement DAP4 web services using HTTP.

The REST interface for the protocol is described in Volume 2, *Web
Services,* of the specification. DAP4 requires that a server implement
at least three responses for each dataset: The DSR; DMR; and Data
response. The DSR is a XML document that provides a *capabilities*
response for the dataset. This document provides links to all of the
other responses available for the dataset, along with other information.
The DSR provides information about alternative encodings for the
different responses in addition to enumerating the basic responses
themselves. The DSR may also list server functions that may be used
with/on the dataset.

DAP4 servers are encouraged to support HTTP content negotiation,
providing the standard DSR, DMR and Data responses in a variety of
forms.

**Migrating from DAP2 to DAP4**

The web service for DAP4 will likely need to be written from scratch,
but the good news is that those are easy to write. For clients, the
behavioral differences between DAP2 and DAP4 servers are small, with two
exceptions. Since DAP4 optionally supports asynchronous responses,
clients should be modified to access data available only using this new
feature. DAP4 also supports content negotiation and that means a larger
number of ways to get the different responses (even though each protocol
has three basic responses).

# <span id="Acknowledgments" class="mw-headline"><span class="mw-headline-number">6</span> Acknowledgments</span>

DAP4 is the result of a joint, multiyear development effort by OPeNDAP
and Unidata, funded by a generous grant from NOAA and guided by an
advisory committee comprising Mike Folk (THG), Jim Frew (UCSB), Steve
Hankin (NOAA), Eric Kihn (NOAA), Chris Lynnes (NASA) and Rich Signell
(USGS).

  

  

Retrieved from "<a
href="https://docs.opendap.org/index.php?title=DAP4:_Overview&amp;oldid=10530"
dir="ltr">https://docs.opendap.org/index.php?title=DAP4:_Overview&amp;oldid=10530</a>"
